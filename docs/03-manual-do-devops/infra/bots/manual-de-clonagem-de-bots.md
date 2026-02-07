---
id: 172
title: "Manual de Clonagem de Bots"
updated_at: 2026-01-31T19:26:01.000000Z
---

# Manual de Clonagem de Bots

# Manual de Clonagem e Provisionamento de Bots (Moltbot)

## 1. Visão Geral
Este documento descreve o procedimento padrão para clonar um bot existente (ex: Cláudio) e provisionar uma nova instância (ex: Roberval) na infraestrutura DigitalSys. O processo garante que o novo bot tenha identidade própria, acesso à rede privada e conflitos de execução resolvidos.

## 2. Requisitos Prévios
- Chave de API da DigitalOcean (Read/Write).
- Novo Token do Discord (Developer Portal).
- Nome do Host (Hostname) desejado.
- Acesso SSH à máquina de controle.

## 3. Clone e Provisionamento (Hardware)
O método mais rápido é via **Snapshot** e recriação via API. Isso preserva todas as ferramentas instaladas.

**Script Python recomendado (reclone_bot.py) deve realizar:**
1. Localizar o ID do Droplet de origem (Cláudio).
2. Solicitar 'snapshot' via API da DigitalOcean.
3. Aguardar a conclusão do snapshot.
4. Criar novo Droplet usando o ID da imagem do snapshot.
5. **INJETAR 'User Data' (Cloud-Init)** para configuração inicial.

**Exemplo de User Data (Bash) para injeção:**
```bash
#!/bin/bash
hostnamectl set-hostname moltbot-roberval
# Atualizar Token do Bot (JSON)
python3 -c "import json; ... data['token']='NOVO_TOKEN'; ..."
systemctl restart clawdbot-gateway
```

## 4. Identidade e Memória (Software)
Após o boot, o bot ainda 'pensa' que é o original. Deve-se limpar sua memória e personalidade.

**Arquivos a editar em `/root/clawd/`:**
- **IDENTITY.md:** Alterar Name, Creature e Emoji.
- **SOUL.md:** Alterar a 'Persona' e diretrizes.
- **memory/YYYY-MM-DD.md:** Apagar logs herdados do dia.

## 5. Rede e Segurança (Firewall)
O novo Droplet nasce sem Tags. Para funcionar na VPC e acessar bancos de dados, ele precisa das mesmas tags do original.

**Ação:** Sincronizar tags via API.
- **Tag Obrigatória:** `internal-network`
- **Comando:**
  `POST /v2/tags/internal-network/resources {resource_id: NEW_DROPLET_ID}`

## 6. Discord Permissions (Erro 4014)
Se o bot conectar e cair com erro 4014, faltam permissões privilegiadas (Intents).

**Acessar Discord Developer Portal -> Bot -> Privileged Gateway Intents e ativar:**
- [x] PRESENCE INTENT
- [x] SERVER MEMBERS INTENT
- [x] MESSAGE CONTENT INTENT

## 7. Validação Final
1. Verificar status do serviço:
   `systemctl status clawdbot-gateway --user`
2. Verificar logs:
   `journalctl --user -u clawdbot-gateway -f`
3. Testar comando no Discord:
   `"Quem é você?"`