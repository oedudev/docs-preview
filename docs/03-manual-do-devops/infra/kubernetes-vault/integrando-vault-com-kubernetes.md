---
id: 61
title: "Integrando Vault com Kubernetes"
updated_at: 2026-01-30T19:53:04.000000Z
---

# Integrando Vault com Kubernetes

##### **ATENÇÃO, ESTE FLUXO É EXCLUSIVAMENTE PARA REALIZAR A INTEGRAÇÃO MANUALMENTE.**

##### **UTILIZE PREFERENCIALMENTE O BOT DO DISCORD PARA CRIAR OS PROJETOS E INTEGRAR O VAULT AUTOMATICAMENTE. ESTE FLUXO É APENAS UM ÚLTIMA INSTÂNCIA!**

No terminal do droplet do Vault você precisará rodar inicialmente o seguinte comando:

```bash
export VAULT_ADDR=https://hashicorp-vault.digitalsys.app 
```

Com isso você conseguirá utilizar os comandos do Vault utilizado pela empresa

Dito isso, as etapas são:

```bash
## 1. Habilitar AppRole
  vault auth enable approle

```

 

```bash
## 2. Criar um arquivo de policy com a nomenclatura "nome-da-policy.hcl" e estutura abaixo
  path "kv/data/apps/<ambiente>//*" {
    capabilities = ["read", "list"]
  }
  path "kv/metadata/apps/<ambiente>//*" {
    capabilities = ["list"]
  }
```

```bash
## 3. Aplicar a policy
  vault policy write <nome-da-policy> <nome-da-policy>.hcl
```

```bash
## 4. Criar role
  vault write auth/approle/role/<nome-da-role> \
    token_policies="<nome-da-policy>" \
    token_ttl=1h \
    token_max_ttl=4h
```

Obs.: note que &lt;nome-da-policy&gt; foi definido na etapa 3

```bash
## 5. Obtenha o valor de Role ID e Secret ID para utilizar no passo 6
  vault read auth/approle/role/<nome-da-role>/role-id           ## OBTÉM O ROLE ID
  vault write -f auth/approle/role/<nome-da-role>/secret-id.    ## OBTÉM O SECRET ID

```

```bash
## 6. Criar o secret no namespace. O exemplo abaixo foi gerado via kubectl, porém pode ser feito com outra ferramenta que te permita criar um secret

kubectl create secret generic <nome-do-secret> \
  -n <namespace> \
  --from-literal=roleId=<ROLE_ID> \
  --from-literal=secretId=<SECRET_ID>
```

```bash
## 7. Crie um arquivo de SecretStore (<nome-do-arquivo>.yml), com a estrutura abaixo
apiVersion: external-secrets.io/v1
kind: ClusterSecretStore
metadata:
  name: <nome da store>
spec:
  provider:
    vault:
      server: <URL do vault>
      path: kv
      version: v2
      auth:
        appRole:
          path: approle
          roleRef:
            name: <nome-do-secret>
            key: roleId
          secretRef:
            name: <nome-do-secret>
            key: secretId
```

```bash
## 8. Aplique esse SecretStore no seu cluster
kubectl apply -f <nome-do-arquivo>.yaml
```

```bash
## 9. Crie o arquivo de ExternalSecret (<nome-do-arquivo>.yml)
apiVersion: external-secrets.io/v1
kind: ExternalSecret
metadata:
  name: esus-api-secret
  namespace: <namespace a aplicar>
spec:
  secretStoreRef:
    name: <nome da store>  # 👈 exatamente o nome SecretStore, da etapa 7
    kind: SecretStore
  target:
    name: <nome da secret que será criado p/ salvar as informacoes>
    creationPolicy: Owner
  dataFrom:
    - extract:
        key: kv/data/apps/dev/esus/api #apenas um exemplo, aqui é o caminho que você criou no frontend do Vault
```

```bash
## 10. Aplique o arquivo de ExternalSecret
kubectl apply -f <nome do arquivo>
```

Agora é possível utilizar o secret no deploy do kubernetes, conforme exemplo abaixo:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: {{ .Values.esusWeb.appName }}
  namespace: {{ .Values.namespace }}
  labels:
    app: {{ .Values.esusWeb.appName }}
spec:
  replicas: 1
  selector:
    matchLabels:
      app: {{ .Values.esusWeb.appName }}
  template:
    metadata:
      labels:
        app: {{ .Values.esusWeb.appName }}
    spec:
      containers:
        - name: {{ .Values.esusWeb.appName }}
          image: {{ .Values.esusWeb.image }}
          ports:
            - containerPort: {{ .Values.esusWeb.ports | first }}
          envFrom:
            - secretRef:
                name: esus-web-env # <--- aqui vai o nome do secret , o mesmo que foi criado em target.name no item 7
```

Obs.: Caso dê erro ao dar apply no ExternalSecret, usar os comandos abaixo para habilitar o External Secret:

```bash
##### **🔧 1. Adicionar o repositório Helm:**
helm repo add external-secrets https://charts.external-secrets.io
helm repo update

##### **🔧 2. Instalar o ESO no cluster:**
helm upgrade --install external-secrets external-secrets/external-secrets \
  -n external-secrets \
  --create-namespace
```