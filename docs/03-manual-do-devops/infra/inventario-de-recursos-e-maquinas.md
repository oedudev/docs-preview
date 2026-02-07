# Inventário de Recursos e Máquinas

Este documento centraliza as informações sobre a infraestrutura de servidores (Droplets) e clusters Kubernetes da empresa.

**Última atualização:** 31/01/2026

## Visão Geral da Infraestrutura

Abaixo segue a lista detalhada de máquinas, incluindo endereços IP, especificações de hardware (CPU/RAM) e status de utilização de disco.

### Servidores e Aplicações

| Nome | IP | CPU | RAM Total | RAM Uso | Disco Total | Disco Uso | OS | Status |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **BookStack** | `157.230.91.101` | 1 vCPU | 0.4 GB | 0.2 GB | 8.6 GB | ⚠️ **56%** | Ubuntu 25.04 | ✅ |
| **Mailhog** | `167.71.31.99` | 1 vCPU | 0.4 GB | 0.3 GB | 8.6 GB | ✅ Resolvido* | Ubuntu 25.04 | ✅ |
| **Moltbot Cláudio** | `24.144.122.141` | 4 vCPU | 7.8 GB | 1.0 GB | 154 GB | 22% | Ubuntu 24.04 | ✅ |
| **Moltbot Clécio** | `64.227.6.71` | 4 vCPU | 7.8 GB | 1.0 GB | 154 GB | 9% | Ubuntu 24.04 | ✅ |
| **Moltbot Clóvis** | `157.230.233.52` | 2 vCPU | 3.8 GB | 0.8 GB | 24 GB | 31% | Ubuntu 24.04 | ✅ |
| **N8n** | `167.71.27.169` | 1 vCPU | 0.9 GB | 0.6 GB | 24 GB | 25% | Ubuntu 24.04 | ✅ |
| **OSTicket** | `198.199.66.32` | 1 vCPU | 1.9 GB | 0.9 GB | 24 GB | 21% | Ubuntu 25.04 | ✅ |
| **Outside Network** | `134.122.127.121` | 1 vCPU | 0.9 GB | 0.4 GB | 24 GB | 10% | Ubuntu 24.04 | ✅ |
| **Pritunl** | `157.230.7.129` | 1 vCPU | 0.9 GB | 0.5 GB | 25 GB | 30% | Ubuntu 22.04 | ✅ |
| **RabbitMQ** | `206.189.206.66` | 1 vCPU | 1.9 GB | 0.5 GB | 48 GB | 8% | Ubuntu 24.04 | ✅ |
| **Runner 142** | `142.93.8.39` | 4 vCPU | 7.8 GB | 1.1 GB | 154 GB | 17% | Ubuntu 24.04 | ✅ |
| **Runner 162** | `162.243.166.74` | 4 vCPU | 7.8 GB | 1.1 GB | 154 GB | 16% | Ubuntu 24.04 | ✅ |
| **Runner 165** | `165.227.202.28` | 4 vCPU | 7.8 GB | 0.9 GB | 154 GB | 16% | Ubuntu 24.04 | ✅ |
| **Runner 167** | `167.99.151.135` | 4 vCPU | 7.8 GB | 1.2 GB | 154 GB | 16% | Ubuntu 24.04 | ✅ |
| **TestLink** | `104.248.51.15` | 2 vCPU | 3.8 GB | 0.5 GB | 79 GB | 8% | Debian 12 | ✅ |
| **Vault** | `137.184.157.36` | 1 vCPU | 0.9 GB | 0.3 GB | 25 GB | 29% | Ubuntu 22.04 | ✅ |

*\*Nota: O alerta de 95% de uso de disco no Mailhog foi reportado e resolvido em 31/01/2026.*

### Kubernetes Cluster (Nodes)

| Nome | IP | CPU | RAM Total | RAM Uso | OS | Status |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **K8s Node 1** | `161.35.115.69` | 8 vCPU | 15.6 GB | 7.5 GB (54%) | Debian 12 | ✅ |
| **K8s Node 2** | `157.230.2.112` | 8 vCPU | 15.6 GB | 7.4 GB (54%) | Debian 12 | ✅ |
| **K8s Node 3** | `137.184.142.70` | 8 vCPU | 15.6 GB | 8.2 GB (60%) | Debian 12 | ✅ |

## Observações
- **Pontos de Atenção:**
  - O **BookStack** apresenta uso de disco acima de 50% (56%). Monitorar crescimento.
- **Saúde Geral:** Todos os nós do Kubernetes e Droplets reportam status saudável (✅).
