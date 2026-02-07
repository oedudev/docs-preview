# 🤖 Arquitetura de Agentes de IA no Kubernetes

Este documento descreve como os agentes (Clóvis, Roberval, Clementina) são implantados e gerenciados no cluster Kubernetes da DigitalSys.

## Visão Geral

Os agentes não são mais Droplets isolados. Eles são **Deployments Kubernetes** stateless (no código) mas stateful na persistência, rodando em um pool de nós dedicados (`bots`).

### Componentes Chave

1.  **Imagem Base Unificada:**
    *   Todos os agentes usam a mesma imagem Docker: `registry.digitalocean.com/digitalsys/openclaw-agent:latest`.
    *   Esta imagem é baseada em `node:22-bookworm` e contém:
        *   `openclaw` (Core)
        *   `@google/gemini-cli` (LLM)
        *   `gh` (GitHub CLI)
        *   `ffmpeg`, `python3`, `jq`, `curl`
    *   **Build:** O build é automático via GitHub Actions no repositório `agents` sempre que a pasta `base/` é alterada.

2.  **Persistência (PVC):**
    *   Cada agente tem seu próprio **PersistentVolumeClaim (PVC)** de 10Gi a 25Gi (`do-block-storage`).
    *   Montado em `/root/.openclaw`.
    *   Garante que memórias (`MEMORY.md`), sessões e configurações persistam entre restarts.

3.  **Configuração e Segredos:**
    *   Nenhuma credencial fica hardcoded no Git.
    *   Todas as variáveis sensíveis (`GITHUB_TOKEN`, `LINEAR_API_KEY`, Tokens do Gateway) vêm do **HashiCorp Vault**.
    *   O **External Secrets Operator (ESO)** sincroniza esses segredos para Secrets nativos do K8s (`<agente>-env`), que são injetados no Pod via `envFrom`.

## Estrutura do Repositório (`agents`)

O repositório `digitalsys-tecnologia/agents` é a fonte da verdade.

```
agents/
├── base/                  # Dockerfile único para todos
├── clovis/
│   └── k8s/               # Manifestos (Deployment, PVC, Secrets)
├── roberval/
│   └── k8s/
└── clementina/
    └── k8s/
```

## Ciclo de Vida

1.  **Atualização de Código/Ferramentas:**
    *   Push no `agents/base/Dockerfile` -> GitHub Actions builda nova imagem -> `registry.digitalocean.com/...:latest`.
    *   Para aplicar: `kubectl rollout restart deployment/<agente> -n bots`.

2.  **Atualização de Configuração:**
    *   Alterar `.yaml` no repo `agents` -> `kubectl apply -f agents/<agente>/k8s/`.

3.  **Atualização de Segredos:**
    *   Editar no Vault (`kv/agents/<agente>`) -> ESO sincroniza em 1 min -> Restart do Pod (se necessário para ler nova ENV).
