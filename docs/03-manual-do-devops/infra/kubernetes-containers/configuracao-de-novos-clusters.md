---
id: 148
title: "Configuração de novos clusters"
updated_at: 2025-10-14T20:50:31.000000Z
---

# Configuração de novos clusters

A configuração inicial de novos clusters é realizada automaticamente por meio do pipeline CI/CD do projeto [digitalsys-tecnologia/infra-kubernetes](https://github.com/digitalsys-tecnologia/infra-kubernetes).

**cert-manager**

Responsável pela emissão e renovação automática de certificados SSL/TLS, garantindo a comunicação segura entre os serviços do cluster.

---

**external-secrets**

Permite integrar e sincronizar segredos armazenados em provedores externos (como AWS Secrets Manager ou HashiCorp Vault) diretamente para o Kubernetes, de forma segura e automatizada.

---

**monitoring (Grafana + Prometheus)**

Conjunto de ferramentas para observabilidade do ambiente. O Prometheus coleta e armazena métricas de desempenho e disponibilidade, enquanto o Grafana oferece painéis visuais e personalizáveis para análise e monitoramento em tempo real.

---

**pushgateway**

Componente auxiliar do Prometheus utilizado para receber e expor métricas de aplicações que não são contínuas (por exemplo, jobs de curta duração), permitindo que esses dados também sejam monitorados.

---

**nginx-ingress**

Controlador de entrada (Ingress Controller) baseado no NGINX, responsável por gerenciar o roteamento de tráfego externo para os serviços internos do cluster

### Etapas para configurar o Cluster

---

Após a criação do Cluster você deve baixar o arquivo de configuração do cluster (kubeconfig), abrir este arquivo, copiar o seu conteudo e obter o base64 desse conteudo, conforme exemplo abaixo:

```bash
echo -n "<insira o conteudo do kubeconfig>" | base64
```

Em seguida, copie este conteúdo e cole na variável de ambiente **"KUBE\_CONFIG"** do projeto **infra-kubernetes**, conforme a imagem abaixo:

[![image.png](https://ajuda.digitalsys.com.br/uploads/images/gallery/2025-10/scaled-1680-/qUPp5xsRa8P01Hr2-image.png)](https://ajuda.digitalsys.com.br/uploads/images/gallery/2025-10/qUPp5xsRa8P01Hr2-image.png)

Após isso você precisará rodar o Job para configurar o Cluster e aguardar o mesmo finalizar com sucesso. Utilize a rota abaixo para rodar o Job:

[![image.png](https://ajuda.digitalsys.com.br/uploads/images/gallery/2025-10/scaled-1680-/5rV5vIrSpOACYkJy-image.png)](https://ajuda.digitalsys.com.br/uploads/images/gallery/2025-10/5rV5vIrSpOACYkJy-image.png)

### **Configurações na DigitalOcean**

---

#### **1. Network**

Caso exista algum firewall configurado (exemplo: Hashi Vaulticorp está disponível apenas para acesso via VPN ou dentro do cluster do Kubernetes) você deve liberar o acesso desse cluster também. Abaixo segue um exemplo de liberação:

[![image.png](https://ajuda.digitalsys.com.br/uploads/images/gallery/2025-10/scaled-1680-/KHPYHd8pBd8O94SB-image.png)](https://ajuda.digitalsys.com.br/uploads/images/gallery/2025-10/KHPYHd8pBd8O94SB-image.png)

[![image.png](https://ajuda.digitalsys.com.br/uploads/images/gallery/2025-10/scaled-1680-/DD6wOONsIZIshiCq-image.png)](https://ajuda.digitalsys.com.br/uploads/images/gallery/2025-10/DD6wOONsIZIshiCq-image.png)  
Busque pelo cluster que você quer configurar e permita o acesso.

#### **2. Container Registry**

---

A liberação do novo cluster ao Container Registry é essencial para que você consiga realizar push/pull das imagens dos projetos para a DigitalOcean.

Essa configuração é feita pela rota abaixo:

[![image.png](https://ajuda.digitalsys.com.br/uploads/images/gallery/2025-10/scaled-1680-/tJfdbzyHNWE1F6xA-image.png)](https://ajuda.digitalsys.com.br/uploads/images/gallery/2025-10/tJfdbzyHNWE1F6xA-image.png)

Busque pelo cluster que você quer configurar e permita o acesso.

#### **3. Banco de Dados**

---

Por fim você deve liberar o acesso do seu(s) banco de dado(s) ao cluster também, do contrário as aplicações dentro desse cluster não irá conseguir se conectar ao banco de dados.

Siga a rota abaixo para liberar o acesso:

[![image.png](https://ajuda.digitalsys.com.br/uploads/images/gallery/2025-10/scaled-1680-/8BLdtf6DwFlDqOv1-image.png)](https://ajuda.digitalsys.com.br/uploads/images/gallery/2025-10/8BLdtf6DwFlDqOv1-image.png)

[![image.png](https://ajuda.digitalsys.com.br/uploads/images/gallery/2025-10/scaled-1680-/9EJK8He67VOMqDQy-image.png)](https://ajuda.digitalsys.com.br/uploads/images/gallery/2025-10/9EJK8He67VOMqDQy-image.png)

Busque pelo cluster que você quer configurar e permita o acesso.

### **Utilizando o novo cluster**

---

Agora, com o cluster configurado, você já pode realizar o deploy dos seus projetos neste novo cluster.

```bash
echo -n "<insira o conteudo do kubeconfig>" | base64
```

Em seguida você deve alterar a variável de ambiente no Github Actions de acordo com o projeto que você quer incluir no Cluster.

Por exemplo, no projeto abaio a configuração do Kubeconfig está numa variável de ambiente chamada "KUBE\_CONFIG\_DEV", logo você deve alterar essa variável de ambiente com o conteúdo base64 que você copiou no passo anterior.

[![image.png](https://ajuda.digitalsys.com.br/uploads/images/gallery/2025-10/scaled-1680-/ox5rgKfH0VkUOKeB-image.png)](https://ajuda.digitalsys.com.br/uploads/images/gallery/2025-10/scaled-1680-/ox5rgKfH0VkUOKeB-image.png)

[![Captura de Tela 2025-10-14 às 17.46.36.png](https://ajuda.digitalsys.com.br/uploads/images/gallery/2025-10/scaled-1680-/cwlt8LE0EOlEOLpU-captura-de-tela-2025-10-14-as-17-46-36.png)](https://ajuda.digitalsys.com.br/uploads/images/gallery/2025-10/scaled-1680-/cwlt8LE0EOlEOLpU-captura-de-tela-2025-10-14-as-17-46-36.png)

**Atenção: ao alterar variáveis de ambiente no GitHub Actions, é importante entender a diferença entre os tipos de** ***Secrets*****:**

- **Organization Secrets: são variáveis globais, acessíveis por todos os repositórios da organização.**
- **Repository Secrets: são variáveis específicas de um único repositório, utilizadas apenas naquele projeto.**

**Exemplo:**

**Imagine que exista um cluster com 10 projetos e que você esteja criando um novo cluster para apenas 1 projeto.**

**Nesse caso, a configuração ideal seria:**

- **Criar uma variável de ambiente em Organization Secrets para ser compartilhada entre os 10 projetos do cluster existente.**
- **Criar uma variável de ambiente em Repository Secrets exclusivamente no repositório do novo projeto, para que apenas ele utilize essa configuração específica.**

**Assim, você garante o uso correto do escopo das variáveis e evita conflitos entre projetos.**