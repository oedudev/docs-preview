---
id: 56
title: "Integração do Kubernetes com Vault via External Secrets Operator"
updated_at: 2026-01-30T19:53:03.000000Z
---

# Integração do Kubernetes com Vault via External Secrets Operator

## Objetivo

Este guia descreve o processo de integração do Kubernetes com o HashiCorp Vault para gerenciar secrets de forma segura e automatizada, usando o **External Secrets Operator (ESO)** e o **Stakater Reloader** para reiniciar pods automaticamente quando secrets mudarem.

---

## 1. Instalação dos componentes necessários

### External Secrets Operator (ESO)

```
helm repo add external-secrets https://charts.external-secrets.io
helm repo update
helm install external-secrets external-secrets/external-secrets --namespace external-secrets --create-namespace
```

### Stakater Reloader

```
helm repo add stakater https://stakater.github.io/stakater-charts
helm repo update
helm install reloader stakater/reloader --namespace reloader --create-namespace
```

---

## 2. Configuração do Vault

### Criar policy para acesso aos secrets

Arquivo `external-secrets-access.hcl`:

```
path "kv/data/dev/*" {
  capabilities = ["read", "list"]
}

path "kv/metadata/dev/" {
  capabilities = ["list"]
}

path "kv/metadata/dev/*" {
  capabilities = ["list"]
}
```

Aplicar a policy:

```
vault policy write external-secrets-access external-secrets-access.hcl
```

### Criar token renovável no Vault

```
vault token create -policy="external-secrets-access" -period=24h
```

**Importante:** O token deve ter `renewable: true`.

### Verificar token

```
vault token lookup s.XXXXXXXX
```

---

## 3. Configuração no Kubernetes

### Criar Secret com o token do Vault

```
kubectl create secret generic vault-token \
  --from-literal=token='s.XXXXXXXX' \
  -n external-secrets
```

### Criar ClusterSecretStore apontando para o Vault

```
apiVersion: external-secrets.io/v1beta1
kind: ClusterSecretStore
metadata:
  name: vault-backend
spec:
  provider:
    vault:
      server: "https://vault.seusite.com"
      path: "kv"
      version: "v2"
      auth:
        tokenSecretRef:
          name: vault-token
          key: token
          namespace: external-secrets
```

**Observação:** Não é necessário configurar `tokenRenewalDuration`. O ESO renova automaticamente se o token for renovável.

### Criar ExternalSecret em cada namespace de aplicação

```
apiVersion: external-secrets.io/v1beta1
kind: ExternalSecret
metadata:
  name: minha-api-secret
  namespace: dev
spec:
  refreshInterval: "1m"
  secretStoreRef:
    name: vault-backend
    kind: ClusterSecretStore
  target:
    name: minha-api-secret-k8s
    creationPolicy: Owner
  dataFrom:
  - extract:
      key: dev/apps/statis/api
```

### Adicionar anotacao de reload no Deployment

```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: meu-app
  namespace: dev
spec:
  replicas: 1
  selector:
    matchLabels:
      app: meu-app
  template:
    metadata:
      labels:
        app: meu-app
      annotations:
        secret.reloader.stakater.com/reload: "minha-api-secret-k8s"
    spec:
      containers:
      - name: meu-container
        image: alpine:latest
        command: ["/bin/sh", "-c"]
        args:
          - |
            echo "Variáveis de Ambiente:" && env && echo "Aguardando 5 minutos..." && sleep 300
        envFrom:
        - secretRef:
            name: minha-api-secret-k8s
```

---

## 4. Fluxo de atualização

1. Alterações no Vault atualizam o Secret no Kubernetes automaticamente via ESO.
2. O Stakater Reloader detecta a mudança no Secret.
3. O Deployment da aplicação é reiniciado automaticamente para carregar as novas variáveis de ambiente.

---

## 5. Considerações futuras

- **Rotacionar tokens periodicamente** (boa prática de segurança).
- **Considerar uso de AppRole** para ambientes de produção de alta segurança.
- **Adicionar monitoramento** para verificar falhas de renovação do token ou falhas no ESO.

---

**Status atual:** Configuração segura, com atualização automática de secrets e renovação automática do token Vault.