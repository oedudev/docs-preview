---
id: 138
title: "Resolução: Erros de Autenticação do Vault (Secret ID)"
updated_at: 2025-10-03T14:58:38.000000Z
---

# Resolução: Erros de Autenticação do Vault (Secret ID)

## 📋 Descrição do Problema

Erros de autenticação ocorriam ao tentar acessar secrets do Vault.

**Sintomas:**

- Falhas de autenticação nas aplicações ao buscar secrets do Vault
- Erros relacionados a Secret ID inválido ou expirado

---

## 🔍 Causa Raiz

O **Secret ID** do AppRole estava sendo criado automaticamente pelo bot do Discord pelo comando **/create-projeto &lt;nome-do-projeto&gt;** com um **TTL (Time To Live) de 24 horas**.

Após esse período, o Secret ID expirava, causando falhas de autenticação pois as aplicações não conseguiam mais se autenticar no Vault para recuperar as secrets necessárias.

---

## ✅ Solução Implementada

O TTL do Secret ID foi ajustado no Vault para um valor sem expiração para que garanta a continuidade do funcionamento das aplicações depois das 24 horas.

### Configuração Anterior

- **TTL do Secret ID:** 24 horas (configurado automaticamente pelo bot do Discord)

### Configuração Atual

- **TTL do Secret ID:** 0s (sem expiração)

---

## 🔧 Como Resolver em Casos Futuros

SSe ocorrerem novos erros de autenticação relacionados ao Vault:

1. **Configuração inicial:**

bash

```bash
 # Exportar endereço do Vault
 export VAULT_ADDR=https://hashicorp-vault.digitalsys.app
 
 # Exibir policies (para ver se já existe a policy)
 vault policy list
 
 # Exibir roles (para pegar os valores posteriores, provavelmente é <nome-do-projeto>-<ambiente>-role)
 vault list auth/approle/role
```

2. **Verifique o TTL do Secret ID:**

bash

```bash
vault read auth/approle/role/<role-name>/secret-id-ttl
```

3. **Ajuste o TTL se necessário:**

bash

```bash
vault write auth/approle/role/<role-name> secret_id_ttl=<novo-valor>
```

4. **Gere um novo Secret ID (se o atual expirou):**

bash

```bash
vault write -f auth/approle/role/<role-name>/secret-id
```

5. Se necessário, atualize o **VAULT\_APPROLE\_SECRETID** do ambiente mudado no GitHub Actions com o novo valor do **secret\_id.**