# 🏃‍♂️ GitHub Actions Runners no Kubernetes (ARC)

Utilizamos o **Actions Runner Controller (ARC)** para gerenciar runners auto-hospedados no cluster Kubernetes. Isso permite escalabilidade dinâmica e economia de custos.

## Arquitetura

*   **Controller:** Roda no cluster e monitora a fila de jobs do GitHub.
*   **ScaleSet:** Define um grupo de runners que escalam juntos.
*   **Runner Pods:** Pods efêmeros criados para executar jobs.

## Tipos de Runners

### 1. Runner Padrão (`runs-on: self-hosted`)
*   **Pool:** `shared` (Nodes `s-8vcpu-16gb`).
*   **Características:** Leves, rápidos de subir.
*   **Uso:** Linter, Testes Unitários, Builds simples.

### 2. Runner Docker-in-Docker (`dind`)
*   **Pool:** `runner-general` (Nodes `s-4vcpu-8gb`).
*   **Características:** General Purpose, custo-benefício otimizado.
*   **Autoscaling:** Mínimo 1 runner sempre ativo (resposta rápida).
*   **Privilégio:** `privileged: true`.
*   **Uso:** Builds de imagens Docker (`docker build`, `docker push`).

## Autoscaling

O ARC está configurado para escalar de **0 a N** réplicas.
*   **Min Replicas:** 0 (Economia total quando ocioso).
*   **Max Replicas:** Definido no `AutoscalingRunnerSet`.

Quando um job entra na fila, o ARC cria um Pod. Quando o job termina, o Pod é destruído.

## Manutenção

### Verificar Status
```bash
kubectl get autoscalingrunnerset -n runners
kubectl get pods -n runners
```

### Logs de Erro
Se um runner não sobe:
```bash
kubectl describe pod <runner-pod> -n runners
kubectl logs -n runners-system deployment/arc-gha-rs-controller
```

### Atualização da Imagem do Runner
As imagens dos runners são definidas no CRD `AutoscalingRunnerSet`. Para atualizar a versão do runner ou ferramentas, edite o manifesto e aplique.
