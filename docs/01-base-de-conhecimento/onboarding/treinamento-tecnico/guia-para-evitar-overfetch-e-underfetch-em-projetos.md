
# Guia para Evitar Overfetch e Underfetch em Projetos

### **1. Introdução**

No desenvolvimento de aplicações que consomem APIs, problemas de **overfetch** e **underfetch** são comuns e afetam diretamente:

- Performance (tempo de resposta maior, uso desnecessário de rede);
- Escalabilidade (mais carga no servidor e no cliente);
- Manutenção (código complexo e difícil de evoluir);
- Experiência do usuário (telas lentas ou inconsistentes).

Um caso crítico a ser evitado é a necessidade de **várias requisições para completar uma única ação**, como buscar dados já conhecidos apenas para poder enviá-los em outra chamada.

<u>***Este documento define boas práticas para evitar esses problemas.***</u>

### **2. Definições**

##### Overfetch

Quando a aplicação recebe **mais dados do que precisa** em uma requisição.  
Exemplo:

- Endpoint `/users/123` retorna nome, e-mail, telefone, endereço, lista de pedidos, amigos etc.
- A tela só precisa de **nome e foto**.

**Impactos:**

- Maior tráfego de rede;
- Maior tempo de processamento;
- Exposição de dados desnecessários.

##### Underfetch

Quando a aplicação recebe **menos dados do que precisa**, obrigando o frontend a fazer **múltiplas chamadas** para compor a mesma tela.  
Exemplo:

- `/users/123` → retorna só os dados básicos do usuário;
- `/users/123/orders` → retorna pedidos;
- `/users/123/friends` → retorna amigos;
- Resultado: várias chamadas só para exibir um perfil.

**Impactos:**

- Muitas requisições encadeadas;
- Latência acumulada;
- Lógica de montagem mais complexa no frontend.

##### Underfetch por Requisição Desnecessária

Situação em que o frontend precisa de uma informação já conhecida ou disponível no contexto (como o ID do usuário logado), mas mesmo assim faz uma chamada extra só para buscá-la.

**Exemplo ruim:**

- `GET /me` → busca o usuário logado para obter o id;
- `PUT /article/456` → com `{updatedBy: userId}`;

**Melhor prática:**

- O id do usuário já deve estar disponível no token JWT ou no contexto da sessão.
- Assim, o frontend já tem esse dado em memória e consegue enviar direto

### **3. Boas Práticas**

#### 3.1 Planejamento de Contratos (API Contracts)

- Definir em conjunto **frontend + backend** quais dados cada tela precisa.
- Evitar endpoints genéricos que retornam "tudo".
- Criar **DTOs (Data Transfer Objects)** específicos para cada caso de uso.

#### 3.2 Padronização de Endpoints

- **Evitar overfetch** criando endpoints otimizados:
    - `/users/123/summary` → retorna só dados resumidos.
- **Evitar underfetch** criando endpoints compostos:
    - `/users/123/profile` → retorna dados básicos, amigos e pedidos em uma única resposta.

#### 3.4 Versionamento e Evolução da API

- Se uma tela precisar de novos dados, **não adicionar campos desnecessários** a endpoints existentes.
- Criar novas rotas/queries ou **versões da API** para manter o contrato limpo.

#### 3.5 Monitoramento e Revisão Contínua

- Usar logs de requisições para detectar payloads muito grandes (sinais de overfetch).
- Monitorar quantidade de requests por tela (sinais de underfetch).
- Realizar revisões periódicas no contrato de API.

### **4. Design de API para Alteração de Status**

Em sistemas que trabalham com entidades que possuem **status mutáveis** (ex.: pedidos, tarefas, processos), é comum a necessidade de alterar esses estados via API.  
Existem duas formas principais de modelar essas alterações:

1. **Rota genérica com envio de status (enum)**
2. **Rotas específicas para cada ação de transição**

Essa seção explica a diferença entre elas, destacando vantagens, desvantagens e quando utilizar cada abordagem.

#### **1. Abordagem 1 – Rota Genérica (com Enum)**

##### Exemplo

```http
PUT /orders/{id}/status
{
  "status": "SHIPPED"
}
```

#####  **Vantagens**

- **Extensível** → novos status podem ser adicionados sem criar novas rotas.
- **Contrato único** → um endpoint centralizado para todas as alterações.
- **Mais limpo** → reduz quantidade de endpoints e facilita documentação.
- **Frontend simples** → só precisa enviar o valor do status.

##### **Desvantagens**

- Backend precisa validar se a **transição é permitida** (ex.: não pode voltar de `DELIVERED` → `PENDING`).
- Regras de negócio mais complexas devem ser tratadas na lógica do backend.

#### **2. Abordagem 2 – Rotas Específicas por Ação**

##### **Exemplo**

```http
POST /orders/{id}/separate
POST /orders/{id}/ship
POST /orders/{id}/deliver
```

##### **Vantagens**

- **Semântica clara** → a ação já fica explícita na URL.
- **Validação embutida** → cada rota representa apenas transições válidas.
- **Bom para workflows complexos**, em que cada status exige processos diferentes (ex.: integração com transportadora, emissão de nota fiscal etc.).

##### **Desvantagens**

- **Pouco escalável** → cada novo status exige uma nova rota.
- **Mais manutenção** → aumenta a complexidade da API e da documentação.
- **Frontend rígido** → precisa conhecer cada rota específica.

##### **3. Qual escolher?**

- **Workflow simples (fluxo previsível de status)**  
    Usar **rota genérica com enums**.  
    Exemplo de fluxo: `PENDING → SEPARATED → SHIPPED → DELIVERED`.
- **Workflow complexo (transições específicas com regras diferentes)**  
    Usar **rotas específicas por ação**.  
    Exemplo: mudança de status que dispara side-effects distintos (envio de notificações, geração de documentos fiscais, integrações externas etc.).

##### **4. Resumo**

<table class="align-center" id="bkmrk-rota-gen%C3%A9rica-%28enum%29"><colgroup><col></col><col></col><col></col></colgroup><tbody><tr><th class="align-center"></th><th class="align-center">**Rota Genérica (Enum)**

</th><th class="align-center">**Rotas Específicas**

</th></tr><tr><td class="align-center">**Escalabilidade**

</td><td class="align-center">Alta (fácil adicionar novos status)

</td><td class="align-center">Baixa (cada status precisa de rota)

</td></tr><tr><td class="align-center">**Clareza Semântica**

</td><td class="align-center">Média (precisa validar transições)

</td><td class="align-center">Alta (ação explícita na URL)

</td></tr><tr><td class="align-center">**Manutenção**

</td><td class="align-center">Mais simples

</td><td class="align-center">Mais complexa

</td></tr><tr><td class="align-center">**Casos ideais**

</td><td class="align-center">Workflows simples e previsíveis

</td><td class="align-center">Workflows complexos, com side-effects diferentes

</td></tr></tbody></table>

