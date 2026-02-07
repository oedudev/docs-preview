# 🦞 Guia Específico: Migrando Agentes OpenClaw para Kubernetes

Este guia complementa a migração geral, focando nas particularidades dos Bots OpenClaw (identidade, secrets e config).

## 🏗️ Arquitetura Alvo
No Kubernetes, o agente roda como um **Deployment** (Stateless/Stateful misto).
- **Código/Estado:** Persistido em PVC (`/root/.openclaw`).
- **Segredos:** Injetados via `ExternalSecret` (Vault AppRole) -> Env Vars.
- **Identidade:** Definida pelo Token do Discord (Cuidado com duplicidade!).

## 1. Preparação no Vault (Segurança)
Diferente dos droplets (onde usávamos token estático), no K8s usamos **AppRole**.

1.  Crie a Role no Vault:
    ```bash
    vault write auth/approle/role/agente-role token_policies="agents-nome"
    ```
2.  Gere `RoleID` e `SecretID`.
3.  Crie uma **Secret K8s** com o `SecretID`:
    ```bash
    kubectl create secret generic agente-vault-approle --from-literal=secret-id=...
    ```

## 2. Manifestos Kubernetes

### SecretStore & ExternalSecret
Configure o `SecretStore` apontando para o Vault e o `ExternalSecret` para baixar as chaves (`GH_TOKEN`, `DISCORD_TOKEN`, etc).

### Deployment (O Pulo do Gato 🐈)
Para evitar que o agente entre em loop de configuração ou tente abrir browser sem permissão, force o modo **local** no boot.

```yaml
    spec:
      containers:
      - name: agent
        image: registry.digitalocean.com/digitalsys/openclaw-agent:latest
        # Importante: Sem limites para cargas de trabalho pesadas (Dev/Build)
        # resources: {} 
        env:
        - name: OPENCLAW_GATEWAY_MODE
          value: "local"
        args:
        - "/bin/bash"
        - "-c"
        - |
          echo "🤖 Booting..."
          # Força configurações críticas que as vezes não pegam via ENV
          openclaw config set gateway.mode local
          openclaw config set plugins.entries.discord.enabled true
          
          # Inicia o Gateway
          openclaw gateway run --verbose
```

## 3. Migração de Dados (Cérebro)
Se o agente tem memória local importante (repositórios clonados, bases vetoriais):

1.  Suba o Pod no K8s.
2.  Pare o serviço no Droplet antigo (`systemctl stop openclaw-gateway`).
3.  Use `tar` via pipe para copiar:
    ```bash
    ssh root\@droplet "tar -C /root/.openclaw -cf - ." | kubectl exec -i pod-name -- tar -C /root/.openclaw -xf -
    ```
4.  Reinicie o Pod para carregar o estado atualizado.

## 4. A Virada (Kill Switch) 💀
**Crítico:** Jamais mantenha o Droplet ligado enquanto o Pod estiver subindo. O Discord bloqueará a conexão se detectar dois gateways com o mesmo token (flap).

1.  Verifique se o Pod está `Running`.
2.  Imediatamente desligue o Droplet: `poweroff`.
3.  Acompanhe os logs do Pod: `kubectl logs -f deployment/agente`.

---
*Adicionado via Cleiton (SRE) - Fev/2026*
