---
id: 171
title: "Inventário de Recursos e Máquinas"
updated_at: 2026-01-31T17:02:07.000000Z
---

# Inventário de Recursos e Máquinas

Este documento centraliza as informações sobre a infraestrutura de servidores (Droplets) e clusters Kubernetes da empresa.

**Última atualização:** 31/01/2026

## Visão Geral da Infraestrutura

Abaixo segue a lista detalhada de máquinas, incluindo endereços IP, especificações de hardware (CPU/RAM) e status de utilização de disco.

### Servidores e Aplicações

<table id="bkmrk-nomeipcpuram-totalra">
<thead>
<tr>
<th>Nome</th>

<th>IP</th>

<th>CPU</th>

<th>RAM Total</th>

<th>RAM Uso</th>

<th>Disco Total</th>

<th>Disco Uso</th>

<th>OS</th>

<th>Status</th>
</tr>
</thead>

<tbody>
<tr>
<td>**BookStack**</td>

<td>`157.230.91.101`</td>

<td>1 vCPU</td>

<td>0.4 GB</td>

<td>0.2 GB</td>

<td>8.6 GB</td>

<td>⚠️ **56%**</td>

<td>Ubuntu 25.04</td>

<td>✅</td>
</tr>

<tr>
<td>**Mailhog**</td>

<td>`167.71.31.99`</td>

<td>1 vCPU</td>

<td>0.4 GB</td>

<td>0.3 GB</td>

<td>8.6 GB</td>

<td>✅ Resolvido\*</td>

<td>Ubuntu 25.04</td>

<td>✅</td>
</tr>

<tr>
<td>**Moltbot Cláudio**</td>

<td>`24.144.122.141`</td>

<td>4 vCPU</td>

<td>7.8 GB</td>

<td>1.0 GB</td>

<td>154 GB</td>

<td>22%</td>

<td>Ubuntu 24.04</td>

<td>✅</td>
</tr>

<tr>
<td>**Moltbot Clécio**</td>

<td>`64.227.6.71`</td>

<td>4 vCPU</td>

<td>7.8 GB</td>

<td>1.0 GB</td>

<td>154 GB</td>

<td>9%</td>

<td>Ubuntu 24.04</td>

<td>✅</td>
</tr>

<tr>
<td>**Moltbot Clóvis**</td>

<td>`157.230.233.52`</td>

<td>2 vCPU</td>

<td>3.8 GB</td>

<td>0.8 GB</td>

<td>24 GB</td>

<td>31%</td>

<td>Ubuntu 24.04</td>

<td>✅</td>
</tr>

<tr>
<td>**N8n**</td>

<td>`167.71.27.169`</td>

<td>1 vCPU</td>

<td>0.9 GB</td>

<td>0.6 GB</td>

<td>24 GB</td>

<td>25%</td>

<td>Ubuntu 24.04</td>

<td>✅</td>
</tr>

<tr>
<td>**OSTicket**</td>

<td>`198.199.66.32`</td>

<td>1 vCPU</td>

<td>1.9 GB</td>

<td>0.9 GB</td>

<td>24 GB</td>

<td>21%</td>

<td>Ubuntu 25.04</td>

<td>✅</td>
</tr>

<tr>
<td>**Outside Network**</td>

<td>`134.122.127.121`</td>

<td>1 vCPU</td>

<td>0.9 GB</td>

<td>0.4 GB</td>

<td>24 GB</td>

<td>10%</td>

<td>Ubuntu 24.04</td>

<td>✅</td>
</tr>

<tr>
<td>**Pritunl**</td>

<td>`157.230.7.129`</td>

<td>1 vCPU</td>

<td>0.9 GB</td>

<td>0.5 GB</td>

<td>25 GB</td>

<td>30%</td>

<td>Ubuntu 22.04</td>

<td>✅</td>
</tr>

<tr>
<td>**RabbitMQ**</td>

<td>`206.189.206.66`</td>

<td>1 vCPU</td>

<td>1.9 GB</td>

<td>0.5 GB</td>

<td>48 GB</td>

<td>8%</td>

<td>Ubuntu 24.04</td>

<td>✅</td>
</tr>

<tr>
<td>**Runner 142**</td>

<td>`142.93.8.39`</td>

<td>4 vCPU</td>

<td>7.8 GB</td>

<td>1.1 GB</td>

<td>154 GB</td>

<td>17%</td>

<td>Ubuntu 24.04</td>

<td>✅</td>
</tr>

<tr>
<td>**Runner 162**</td>

<td>`162.243.166.74`</td>

<td>4 vCPU</td>

<td>7.8 GB</td>

<td>1.1 GB</td>

<td>154 GB</td>

<td>16%</td>

<td>Ubuntu 24.04</td>

<td>✅</td>
</tr>

<tr>
<td>**Runner 165**</td>

<td>`165.227.202.28`</td>

<td>4 vCPU</td>

<td>7.8 GB</td>

<td>0.9 GB</td>

<td>154 GB</td>

<td>16%</td>

<td>Ubuntu 24.04</td>

<td>✅</td>
</tr>

<tr>
<td>**Runner 167**</td>

<td>`167.99.151.135`</td>

<td>4 vCPU</td>

<td>7.8 GB</td>

<td>1.2 GB</td>

<td>154 GB</td>

<td>16%</td>

<td>Ubuntu 24.04</td>

<td>✅</td>
</tr>

<tr>
<td>**TestLink**</td>

<td>`104.248.51.15`</td>

<td>2 vCPU</td>

<td>3.8 GB</td>

<td>0.5 GB</td>

<td>79 GB</td>

<td>8%</td>

<td>Debian 12</td>

<td>✅</td>
</tr>

<tr>
<td>**Vault**</td>

<td>`137.184.157.36`</td>

<td>1 vCPU</td>

<td>0.9 GB</td>

<td>0.3 GB</td>

<td>25 GB</td>

<td>29%</td>

<td>Ubuntu 22.04</td>

<td>✅</td>
</tr>
</tbody>
</table>

*\*Nota: O alerta de 95% de uso de disco no Mailhog foi reportado e resolvido em 31/01/2026.*

### Kubernetes Cluster (Nodes)

<table id="bkmrk-nomeipcpuram-totalra-1">
<thead>
<tr>
<th>Nome</th>

<th>IP</th>

<th>CPU</th>

<th>RAM Total</th>

<th>RAM Uso</th>

<th>OS</th>

<th>Status</th>
</tr>
</thead>

<tbody>
<tr>
<td>**K8s Node 1**</td>

<td>`161.35.115.69`</td>

<td>8 vCPU</td>

<td>15.6 GB</td>

<td>7.5 GB (54%)</td>

<td>Debian 12</td>

<td>✅</td>
</tr>

<tr>
<td>**K8s Node 2**</td>

<td>`157.230.2.112`</td>

<td>8 vCPU</td>

<td>15.6 GB</td>

<td>7.4 GB (54%)</td>

<td>Debian 12</td>

<td>✅</td>
</tr>

<tr>
<td>**K8s Node 3**</td>

<td>`137.184.142.70`</td>

<td>8 vCPU</td>

<td>15.6 GB</td>

<td>8.2 GB (60%)</td>

<td>Debian 12</td>

<td>✅</td>
</tr>
</tbody>
</table>

## Observações

- **Pontos de Atenção:**
    - O **BookStack** apresenta uso de disco acima de 50% (56%). Monitorar crescimento.
- **Saúde Geral:** Todos os nós do Kubernetes e Droplets reportam status saudável (✅).