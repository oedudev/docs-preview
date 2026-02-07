
# Configuração de novos clusters

A configuração inicial de novos clusters é realizada automaticamente por meio do pipeline CI/CD do projeto [digitalsys-tecnologia/infra-kubernetes](https://github.com/digitalsys-tecnologia/infra-kubernetes).

**cert-manager**

Responsável pela emissão e renovação automática de certificados SSL/TLS, garantindo a comunicação segura entre os serviços do cluster.

**monitoring (Grafana + Prometheus)**

Conjunto de ferramentas para observabilidade do ambiente. O Prometheus coleta e armazena métricas de desempenho e disponibilidade, enquanto o Grafana oferece painéis visuais e personalizáveis para análise e monitoramento em tempo real.

**nginx-ingress**

Controlador de entrada (Ingress Controller) baseado no NGINX, responsável por gerenciar o roteamento de tráfego externo para os serviços internos do cluster

### Etapas para configurar o Cluster

#### **1. Network**

Caso exista algum firewall configurado (exemplo: Hashi Vaulticorp está disponível apenas para acesso via VPN ou dentro do cluster do Kubernetes) você deve liberar o acesso desse cluster também. Abaixo segue um exemplo de liberação:

[![image.png](/img/configuracao-de-novos-clusters-3.png)](https://ajuda.digitalsys.com.br/uploads/images/gallery/2025-10/KHPYHd8pBd8O94SB-image.png)

[![image.png](/img/configuracao-de-novos-clusters-4.png)](https://ajuda.digitalsys.com.br/uploads/images/gallery/2025-10/DD6wOONsIZIshiCq-image.png)  
Busque pelo cluster que você quer configurar e permita o acesso.

#### **2. Container Registry**

Por fim você deve liberar o acesso do seu(s) banco de dado(s) ao cluster também, do contrário as aplicações dentro desse cluster não irá conseguir se conectar ao banco de dados.

Siga a rota abaixo para liberar o acesso:

[![image.png](/img/configuracao-de-novos-clusters-6.png)](https://ajuda.digitalsys.com.br/uploads/images/gallery/2025-10/8BLdtf6DwFlDqOv1-image.png)

[![image.png](/img/configuracao-de-novos-clusters-7.png)](https://ajuda.digitalsys.com.br/uploads/images/gallery/2025-10/9EJK8He67VOMqDQy-image.png)

Busque pelo cluster que você quer configurar e permita o acesso.

### **Utilizando o novo cluster**

