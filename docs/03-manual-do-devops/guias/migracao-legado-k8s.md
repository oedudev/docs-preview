# 🚚 Guia de Migração: Legado (Droplet) para Kubernetes

Este guia descreve o processo utilizado para migrar serviços stateful (como n8n e Bots) de Droplets isolados para o Cluster Kubernetes.

## Pré-requisitos
*   Acesso `kubectl` ao cluster.
*   Acesso SSH ao Droplet de origem.
*   Manifestos K8s preparados (Deployment, PVC, Service).

## Passo a Passo

### 1. Preparação (Sem Downtime)
1.  Crie o **PVC** no Kubernetes.
2.  Aplique o **Deployment** com `replicas: 0` (apenas para registrar, não subir).
3.  Crie um Pod temporário de transferência (ex: `ubuntu` ou `busybox`) que monte o PVC em `/data`.

```yaml
# restore-pod.yaml
apiVersion: v1
kind: Pod
metadata: { name: restore, namespace: tools }
spec:
  volumes: [{ name: data, persistentVolumeClaim: { claimName: n8n-pvc } }]
  containers: [{ name: restore, image: ubuntu, command: ["sleep", "infinity"], volumeMounts: [{ mountPath: "/data", name: data }] }]
```

### 2. Janela de Manutenção (Com Downtime)
1.  **Parar o serviço no Droplet:**
    ```bash
    systemctl stop n8n # ou docker stop ...
    ```
    *Isso garante a integridade do banco de dados (SQLite/arquivos).*

2.  **Copiar os Dados:**
    Use `scp` para baixar do Droplet para sua máquina local (buffer) e `kubectl cp` para enviar para o Pod de restore.
    ```bash
    # Droplet -> Local
    scp -r root\@droplet:/var/lib/docker/volumes/n8n_data/_data/* ./temp_data/
    
    # Local -> K8s PVC
    kubectl cp ./temp_data/ tools/restore:/data/
    ```

3.  **Ajustar Permissões:**
    No Pod de restore, ajuste o dono dos arquivos (ex: `1000:1000` para node/n8n).
    ```bash
    kubectl exec -n tools restore -- chown -R 1000:1000 /data
    ```

### 3. Virada de Chave
1.  **Deletar o Pod de Restore.**
2.  **Escalar o Deployment:** `kubectl scale deployment n8n --replicas=1`.
3.  **Validar Logs:** `kubectl logs -f deployment/n8n`.
4.  **Atualizar DNS:** Aponte o domínio para o IP do Load Balancer (Ingress).

### 4. Limpeza
Após validar o funcionamento no K8s por 24h, o Droplet antigo pode ser desligado e, posteriormente, excluído (snapshot recomendado antes).
