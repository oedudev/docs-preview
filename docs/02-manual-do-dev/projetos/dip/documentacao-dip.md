
# Documentação DIP

### **Visão e entendimento** 

O DIP (Plataforma de Seguros DigitalSys) tem como objetivo funcionar de forma similar ao sistema HSoares, atendendo as necessidades das imobiliárias no gerenciamento de seguros para locação de imóveis. 

Por meio da plataforma, as imobiliárias poderão cadastrar os dados de seus clientes e suas respectivas demandas de seguro de forma simples e estruturada. Essas informações serão enviadas primeiramente para a corretora de seguros, que encaminha as propostas para as seguradoras responsáveis pela análise de risco. Após essa etapa, a seguradora retorna com a precificação e o parecer final da proposta, resultados que serão enviados diretamente para a imobiliária via e-mail, garantindo um fluxo ágil e transparente.

O sistema está sendo projetado para lidar com múltiplas propostas simultaneamente, permitindo que o locador do imóvel possa avaliar diferentes opções e escolher aquela que oferece o melhor custo-benefício, visto que o locador busca sempre maximizar seus lucros. Também é importante considerar que algumas propostas podem ser negadas, e a plataforma facilita a gestão dessas devolutivas, permitindo uma comunicação eficiente entre imobiliária, corretora e seguradora.

Com o DIP, todo esse processo de cotação, análise e retorno das propostas será simplificado e automatizado, reduzindo a necessidade de intervenções manuais e tornando a experiência mais ágil, segura e eficiente para as imobiliárias e seus clientes.

### **Estrutura do projeto - Backend**

└── 📁backend

 └── 📁go

 └── 📁cmd

 └── 📁api

 └── 📁pkg

 └── 📁adapter

 └── 📁db

 └── 📁intf

 └── 📁nosql

 └── 📁repo

 └── 📁bootstrap

 └── 📁client

 └── 📁config

 └── 📁facade

 └── 📁logger

 └── 📁mocks

 └── 📁model

 └── 📁parser

 └── 📁port

 └── 📁graph

 └── 📁model

 └── 📁schemas

 └── 📁service

 └── 📁tests

 └── 📁integration

 └── 📁pkg

 └── 📁broker

 └── 📁unit

 └── 📁pkg

 └── 📁service

 └── 📁tmp

#### **Descrição:** 

- **cmd/** → Diretório principal onde a aplicação é iniciada
- - **api/** Contém o ponto de entrada da aplicação (main.go)
- **pkg/** → Pacotes reutilizáveis que compõem a lógica da aplicação.
- - **adapter/** → Gerencia a comunicação com bancos de dados e APIs externas
    - - **db/**→ Diretório que possui contato com o banco de dados.
        - - **intf/**→ Contém as assinaturas das funções do repo que serão utilizadas no service.
            - **nosql/**→ Contém as implementações das interações em si, funções que terão contato com o banco de dados NoSQL (MongoDB).
    - **bootstrap/** → Configuração e inicialização dos componentes principais da aplicação.
    - **client/** → Implementação de conexões com serviços externos
    - **config/** → Arquivos de configuração da aplicação
    - **facade/** → Camada de abstração para serviços da aplicação
    - **logger/** → Sistema de registro de logs da aplicação
    - **mocks/** → Implementação de mocks para testes unitários
    - **model/** → Definição dos modelos de dados
    - **parser/** → Interpretação e conversão de dados entre diferentes formatos
    - **port/** → Camada de interfaces externas, incluindo GraphQL
    - - **graph/** → Diretório do GraphQL
        - - **model/** → Modelos gerados a partir dos schemas do GraphQL
            - **schemas/**→ Arquivos que definem como os dados vão ser consultados e manipulados no GraphQL
    - **service/** → Implementação da lógica de negócios
- **tests/** → Testes automatizados do sistema
- - **integration/** → Testes que verificam se diferentes partes do sistema funcionam bem juntas
    - **unit/** → Testes que verificam se partes isoladas do código funcionam corretamente

**tmp/** → Diretório para arquivos temporários

### **Camadas do sistema**

**Repo → Service → Facade → Resolvers**

**Repo:** Responsável por interagir com o banco de dados. Contendo a lógica da persistência desses dados. Ex:

![](assets/documentacao-dip-1.png)

**Service:** Responsável pela aplicação das transformações necessárias para a manipulação dos dados. Ex:

![](assets/documentacao-dip-2.png)

**Facade:** Responsável por simplificar a interação com vários componentes, expondo funcionalidades de serviços sem expor detalhes internos. Ex:

![](assets/documentacao-dip-3.png)

**Resolvers:** Invoca o Facede para atender as requisições da API, obtendo os dados e, consequentemente, realizando as operações necessárias. Ex:

![](assets/documentacao-dip-4.png)

### **Conteinerização**

#### **Dockerfile do Backend**

![](assets/documentacao-dip-5.png)

O Dockerfile define como a imagem do backend será construída e configurada. Ele segue um processo de duas etapas:

1. **Fase de build (builder) - Linhas 1 a 8**:
2. - Utiliza a imagem base golang:1.23.5.
    - Define /app como diretório de trabalho.
    - Copia os arquivos go.mod e go.sum e baixa as dependências.
    - Copia o código-fonte completo.
    - Compila o código, gerando um binário chamado main.

2. **Fase de execução (runtime) - linhas 10 a 15**:
3. - Usa uma imagem minimalista alpine:latest.
    - Adiciona certificados SSL necessários.
    - Define /root/ como diretório de trabalho.
    - Copia o binário gerado na fase anterior para dentro da imagem final.
    - Expõe a porta 8080.
    - Define ./main como o comando de entrada.

#### **Docker-compose.yml**

![](assets/documentacao-dip-6.png)

O arquivo docker-compose.yml é responsável por orquestrar os containers do backend, frontend e banco de dados.

**Backend (**backend**) - linhas 13 a 22**

- Constrói a imagem a partir do diretório ./backend/go, usando o Dockerfile.
- Expõe a porta 8080:8080.
- Define variáveis de ambiente, incluindo:
- - GO\_ENV=production: Define o ambiente de execução.
    - MONGO\_CONNECTION\_STRING: String de conexão com o MongoDB.
    - MONGO\_DATABASE=dip: Define o nome do banco de dados usado pelo backend.

**Banco de Dados (**mongodb**) - linhas 24 a 31**

- Usa a imagem oficial mongo:6.0.
- Reinicia automaticamente caso pare (restart: always).
- Define as credenciais do banco de dados:
- Persiste os dados do MongoDB no volume mongo-data, garantindo que os dados não sejam perdidos caso o container seja reiniciado.

**Comandos Úteis**

O Docker Compose permite rodar os containers juntos ou individualmente.

**Subir todos os containers (backend, banco e frontend)**:  
 docker-compose up -d

**Parar todos os containers**:  
 docker-compose down

**Subir apenas o backend**:  
 docker-compose up -d backend

**Subir apenas o banco de dados**:  
 docker-compose up -d mongodb

**Parar apenas o backend**:  
 docker-compose down backend

**Parar apenas o banco de dados**:  
 docker-compose down mongodb

