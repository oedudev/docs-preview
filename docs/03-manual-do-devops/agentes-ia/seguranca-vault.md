# 🔐 Gestão de Segredos: Vault & External Secrets

A segurança dos agentes e runners depende da centralização de credenciais no HashiCorp Vault e sua injeção segura no Kubernetes via External Secrets Operator (ESO).

## Fluxo de Credenciais

1.  **Origem (Vault):**
    *   Endereço: `http://137.184.157.36:8200` (Acesso via VPC interna `10.116.0.30` recomendado).
    *   Engine: KV v2 (`kv/`).
    *   Caminho Padrão: `kv/data/agents/&lt;nome-do-agente>`.

2.  **Ponte (External Secrets Operator - ESO):**
    *   O ESO roda no cluster K8s.
    *   **SecretStore:** Define *como* acessar o Vault (Token ou AppRole). Existe um por namespace ou global.
    *   **ExternalSecret:** Define *quais* dados buscar.
        ```yaml
        dataFrom:
        - extract:
            key: kv/data/agents/roberval
        ```

3.  **Destino (Kubernetes Secret):**
    *   O ESO cria um Secret nativo (ex: `roberval-env`) com os dados decifrados.
    *   O Deployment monta esse secret como variáveis de ambiente:
        ```yaml
        envFrom:
        - secretRef:
            name: roberval-env
        ```

## Como Adicionar/Rotacionar uma Chave

1.  **Acesse o Vault:**
    Via UI ou CLI (requer token com permissão de escrita).
    ```bash
    export VAULT_ADDR=http://137.184.157.36:8200
    export VAULT_TOKEN=...
    vault kv patch kv/agents/roberval NOVA_CHAVE=valor_super_secreto
    ```

2.  **Sincronização:**
    O ESO verifica mudanças a cada 1 minuto (padrão).
    Verifique se sincronizou:
    ```bash
    kubectl get externalsecret roberval-env-secret -n bots
    # Deve mostrar "SecretSynced"
    ```

3.  **Aplicação:**
    Se a aplicação não suporta *hot-reload* de variáveis de ambiente (a maioria não suporta), reinicie o Pod:
    ```bash
    kubectl rollout restart deployment/roberval -n bots
    ```

## Troubleshooting

*   **SecretSynced = False:** Verifique se o Token do Vault no `SecretStore` expirou ou se o caminho no `ExternalSecret` está correto.
*   **Permissão Negada:** O token usado pelo ESO deve ter policy de `read` no path `kv/data/*`.
