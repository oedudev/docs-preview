
# Plano de Refatoração – Overfetch, Underfetch e Boas Práticas em Requests

### **1. Objetivo**

Este documento tem como objetivo identificar, no projeto, todos os pontos em que ocorrem problemas relacionados a **overfetch**, **underfetch** e outras falhas ou vulnerabilidades no consumo de **requests**.

A partir desse diagnóstico, será elaborado um **plano de refatoração** com propostas de correção alinhadas às boas práticas já estabelecidas na equipe.

Para referência, consulte também o material: [Guia para Evitar Overf... | Ajuda DigitalSys](https://ajuda.digitalsys.com.br/books/manual-do-novo-funcionario/page/guia-para-evitar-overfetch-e-underfetch-em-projetos)

### **2. Critérios de Análise**

Durante a revisão, foram considerados casos como:

- **Overfetch:** endpoints que retornam mais dados do que o necessário para a tela/funcionalidade.
- **Underfetch:** endpoints que obrigam o frontend a realizar múltiplas requisições para montar uma tela ou completar uma ação.

### **3. Ocorrências Identificadas Página Home (TARM)**

Na **HomePage** foram identificadas diversas requests durante a renderização, algumas delas inclusive **repetidas**, resultando em problemas de **overfetch** e **uso desnecessário de rede**.

network da homePage

![](/docs-preview/img/plano-de-refatoracao-overfetch-underfetch-e-boas-praticas-em-requests-1.png)

#### **Requests UserID**

#### **3.1 Ocorrência 1 – Recuperação de** `user_id`**

**Local:** Função

![](/docs-preview/img/plano-de-refatoracao-overfetch-underfetch-e-boas-praticas-em-requests-2.png)   
**Descrição:**

- Recupera o token do `localStorage`.
- Decodifica o token com `getUserIdByToken`.
- Faz uma chamada a `getUsers()` para obter todos os usuários.
- Executa um `.find()` para localizar o usuário pelo `user_id`.
- Atualiza variáveis reativas (`responsibleTarm`, `currentUserName`) com o nome do usuário.

**Problema:**

- Uma chamada completa para `getUsers()` é feita apenas para recuperar dados do usuário logado.
- Esse comportamento gera **overfetch**, pois carrega todos os usuários desnecessariamente.
- Além disso, já existe no backend a capacidade de identificar o usuário a partir do token da requisição.

**Solução proposta:**

- Utilizar a rota `/shared/possible-values` para incluir o retorno do nome do usuário e id autenticado.
- Dessa forma, evitamos múltiplas requests e eliminamos a necessidade de buscar todos os usuários apenas para identificar o logado.

#### **3.2 Ocorrência 2 – Variável** `userId` **não utilizada**

**Local:** Função:

![](/docs-preview/img/plano-de-refatoracao-overfetch-underfetch-e-boas-praticas-em-requests-3.png)  
**Descrição:**

- O sistema realiza uma request para buscar o `user_id`.
- O valor é armazenado em uma variável (`userId`) que não é utilizada posteriormente.

**Problema:**

- Request desnecessária.
- Consumo de recurso sem efeito prático no sistema.

**Solução proposta:**

- Remover a request e a variável, já que o valor não é utilizado.

#### **3.3 Ocorrência 3 – Recuperação de** `user_id`**

**Local:** Função (composables/usePhoneSystemService.ts):

![](/docs-preview/img/plano-de-refatoracao-overfetch-underfetch-e-boas-praticas-em-requests-4.png)  
**Descrição:**

- O sistema realiza uma request para buscar o `user_id`.
- O valor é utilizado em uma nova request (`getPhoneCredentials`).

**Problema:**

- Request desnecessária.
- Consumo de recurso sem efeito prático no sistema.

**Solução proposta:**

- Remover a request, no backend existe uma função para pegar o id do usuario pelo token da request.

<u>obs: Essa ocorrência ira existir em todos as paginas que utilizam o componente </u><u>**callSystem**</u><u> pode ser resolvida posteriormente</u>

#### **Requests User**

#### **3.4 Ocorrência 4 – Recuperação de nome do usuário logado**

**Local:** Funções que utilizam `getUsers()` apenas para obter o usuário autenticado.

**Descrição:**

- O frontend realiza uma chamada completa para `getUsers()`.
- Usa o retorno apenas para identificar o nome do usuário logado.

**Problema:**

- **Overfetch**: todos os usuários são carregados sem necessidade.
- Requisições redundantes, já que esse caso foi mapeado e será resolvido na **Ocorrência 1 do modulo UserID**.

**Solução proposta:**

- Reutilizar a solução implementada via `/shared/possible-values`, retornando diretamente o nome do usuário autenticado.
- Assim, elimina-se a necessidade dessa chamada extra.

#### **3.5 Ocorrência 5 – Request e Processamento de usuários em** `fetchOptions`**

**Local:** Função `fetchOptions` processo/request utilizado para popular o campo ***Enviar para***

[![image.png](/docs-preview/img/plano-de-refatoracao-overfetch-underfetch-e-boas-praticas-em-requests-5.png)](https://ajuda.digitalsys.com.br/uploads/images/gallery/2025-09/rNIJdscMwvTrQQdn-image.png)

[![image.png](/docs-preview/img/plano-de-refatoracao-overfetch-underfetch-e-boas-praticas-em-requests-6.png)](https://ajuda.digitalsys.com.br/uploads/images/gallery/2025-09/HSN7zydx91yrWeAi-image.png)

**Descrição:**

- O sistema realiza uma request para buscar o `user`.
- A rota retorna um volume muito grande de dados (todos os usuários).
- Função processAvailableEmployees recebe os dados de `getUsers()`.
- Filtra usuários com `status = ativo` e `profile = médico regulador`.
- Cria objetos `{ key: id, label: nome }`.
- Ordena alfabeticamente.
- O frontend carrega a lista completa e aplica filtros conforme o usuário digita.

**Problema:**

- **Overfetch**: todos os usuários são retornados e filtrados no frontend.
- Carga de dados excessiva e perda de performance.
- O frontend executa lógica de negócio que deveria estar no backend.
- A lógica de filtro está no frontend, tornando o sistema mais lento e pesado.

**Solução proposta:**

- Implementar busca incremental no backend.
- Ao digitar, o frontend deve disparar uma request com debounce (ex.: 300–500ms) para retornar apenas os usuários compatíveis com o termo buscado.
- A resposta deve conter **apenas os campos necessários** para uso no frontend (ex.: `id`, `descriptive_name`).

#### **3.6 Ocorrência 6 – Exposição indevida de login de usuário**

**Local:** Rota `GET /user`

**Descrição:**

- O endpoint retorna informações do usuário, incluindo o campo `name`, que contém o login utilizado para autenticação.
- Atualmente, qualquer usuário do sistema consegue acessar essa rota e visualizar o login de outros usuários.
- Exemplo de resposta:

```json
{
  "id": 2,
  "descriptive_name": "Marcio Sobral",
  "status": "ativo",
  "name": "admin.tarm",
  "profile": {
    "id": 2,
    "title": "TARM",
    "text": "Profile for Operador TARM"
  },
  "professional_type": null,
  "team": null
}
```

**Problema:**

- O campo `name` expõe o login do usuário, que é uma informação sensível.
- Acesso a esse dado deveria ser restrito apenas a perfis **administrativos**.
- Usuários comuns não deveriam ter visibilidade do login interno de outros usuários.

**Solução proposta:**

- Ajustar a rota para que o campo `name` não seja retornado para usuários comuns.
- Implementar **controle de acesso por perfil**: somente administradores podem visualizar logins de outros usuários.
- Avaliar a necessidade de mover ou anonimizar esse campo, expondo apenas o `descriptive_name` para não-admins.

####   

#### **3.7 Ocorrência 7 – Filtro de incidentes no frontend**

**Local:** Rota `GET /incident/mask` Rota utilizada para popular o campo ***Relacionar ocorrência existente***

[![image.png](/docs-preview/img/plano-de-refatoracao-overfetch-underfetch-e-boas-praticas-em-requests-7.png)](https://ajuda.digitalsys.com.br/uploads/images/gallery/2025-09/ho0MtIUGxNOsroJ0-image.png)

**Descrição:**

- A rota retorna uma lista extensa de incidentes.
- O frontend recebe todos os dados e filtra apenas quando o usuário digita.

**Problema:**

- **Overfetch** semelhante ao caso de usuários.
- Maior tempo de carregamento e consumo de memória no navegador.
- Risco de inconsistência caso a base cresça ainda mais.

**Solução proposta:**

- Alterar a rota para suportar **busca por termo**.
- O frontend envia a string digitada pelo usuário (com debounce) e recebe apenas os incidentes que correspondem à busca.
- Limitar o retorno aos campos realmente utilizados pelo frontend.

#### **3.8 Ocorrência 8 – Dados desnecessários no retorno**

**Local:** Rota `GET /shared/possible-values`

**Descrição:**

- A rota atualmente retorna diversos elementos, incluindo `employee` e `open_incident`.
- No frontend, esses dados **não são/serão utilizados** na construção da página.

**Problema:**

- **Overfetch:** envia dados desnecessários para o frontend, aumentando o tráfego e processamento.
- Dificulta manutenção futura e aumenta risco de inconsistência.

**Solução proposta:**

- Remover os campos `employee` e `open_incident` do retorno da rota.
- Garantir que a rota entregue **somente os elementos realmente utilizados** para popular a página.

obs: a remoção de employee deve ser feita depois da implementação/correção da <u>**Ocorrência 2**</u>

#### **3.9 Ocorrência 9 – Problema com Requests repetidas**

**Local:** Home (TARM)

**Descrição:**

- Ao editar/criar uma ocorrência criada pelo usuário **TARM**, ao navegar entre os formulários **"Dados básicos"**, **"Ocorrência"** e **"Paciente"**, o sistema executa repetidas requisições para:
    - `GET /shared/possible-values`
    - `GET /user`
    - `GET /incident/mask`
- O problema ocorre porque dentro dos **componentes de formulário de edição** existem chamadas desnecessárias para buscar dados que já haviam sido carregados quando a página foi construída.

**Problema:**

- **Requisições duplicadas** aumentam o consumo de rede e tornam a navegação mais lenta.
- O frontend perde eficiência ao não reutilizar os dados já disponíveis no estado da página.

**Obs: Esse comportamento já foi apontado como um problema recorrente na documentação** [**Documentação Front-End... | Ajuda DigitalSys**](https://ajuda.digitalsys.com.br/books/manual-do-desenvolvedor/page/documentacao-front-end-atomic-design) <u>**2. Requisições nos componentes.**</u>

**Solução proposta:**

- Remover requisições desnecessárias dos componentes de formulário.
- Consumir diretamente os dados que já foram carregados ao inicializar a página.
- Reforçar a prática de **não disparar requests dentro de componentes**.

#### **3.10 Ocorrência 10 – Problema com Polling**

**Local:** Formulário de Ocorrência

**Descrição:**

- Ao clicar em editar uma ocorrência, o sistema utiliza **polling** para buscar atualizações constantes da ocorrência.
- Essa solução foi implementada como medida temporária devido ao prazo de entrega do projeto.
- Após clicar no botão **Voltar**, o sistema continua realizando requests para a ocorrência anterior, mesmo que o usuário já tenha saído do formulário.

**Problema:**

- Consumo desnecessário de rede e processamento.
- Possibilidade de inconsistências, já que o sistema continua atualizando dados que não estão mais sendo visualizados.
- Impacto negativo na performance geral da aplicação.

**Solução proposta:**

- Corrigir o comportamento de polling para que seja interrompido ao sair do formulário.
- Substituir futuramente a estratégia de polling pela implementação de **WebSockets**, garantindo atualização em tempo real apenas quando necessário.

#### **3.11 Ocorrência 11 – Requisições redundantes na página TARM**

**Descrição:**  
Durante a renderização e navegação dentro da página **TARM**, foram identificadas diversas requisições executadas de forma redundante.  
Todas as requests são disparadas assim que a página é carregada e também sempre que o usuário interage com determinados componentes ou filtros, ocasionando chamadas repetidas às mesmas rotas e resultando em **overfetch**, uso desnecessário de banda e aumento no tempo de resposta da interface.

[![image.png](/docs-preview/img/plano-de-refatoracao-overfetch-underfetch-e-boas-praticas-em-requests-8.png)](https://ajuda.digitalsys.com.br/uploads/images/gallery/2025-10/HI2TPzRdFPSFKck1-image.png)

**Problema:**

- Execução repetida de múltiplas requisições durante a renderização e navegação na página TARM.
- Falta de cache e reaproveitamento dos dados já carregados.
- Requisições desnecessárias para informações que não sofreram alteração.
- Impacto direto na performance geral e no tempo de carregamento dos componentes.

**Solução proposta:**

- Consolidar todas as informações necessárias da página **TARM** em uma **única requisição de inicialização**, eliminando chamadas redundantes.
- Implementar **mecanismos de cache ou armazenamento em estado global** para evitar novas requisições ao interagir com filtros ou elementos que dependem dos mesmos dados.
- Revisar os watchers e eventos da página para garantir que as chamadas à API ocorram apenas quando houver efetiva mudança de parâmetros.
- Centralizar a obtenção dos dados compartilhados (ex.: informações do usuário logado, status e possíveis valores) em uma rota única como `/shared/possible-values`.

obs: mesmo problema relatado em Medico Regulador **4.5 Ocorrência 5 – Requisições redundantes na OccurrenceView**

### **4. Ocorrências Identificadas Médico Regulador (MR)**

####   

Na **RegulationMenu** foram identificadas diversas requests durante a renderização, algumas delas inclusive **repetidas**, resultando em problemas de **overfetch** e **uso desnecessário de rede**.

[![image.png](/docs-preview/img/plano-de-refatoracao-overfetch-underfetch-e-boas-praticas-em-requests-9.png)](https://ajuda.digitalsys.com.br/uploads/images/gallery/2025-10/iUVbKGiCgafMm227-image.png)

#### **Requests UserID**

#### **4.1 Ocorrência 1 – Recuperação de** `user_id`**

**Local:** Função

[![image.png](/docs-preview/img/plano-de-refatoracao-overfetch-underfetch-e-boas-praticas-em-requests-10.png)](https://ajuda.digitalsys.com.br/uploads/images/gallery/2025-10/ImsUBo8u28CGbjLa-image.png)**Local:**

- Função `loadUserId`
- Função `getUserIdByToken`
- Arquivo `usePhoneSystemService.ts`
- Componente `banner-description-MR.vue`

**Descrição:**

- O sistema possui **três pontos distintos** onde o `user_id` é buscado ou processado de forma redundante.
- Essas implementações duplicam a mesma lógica em locais diferentes, dificultando manutenção e aumentando o risco de inconsistências.

**Problema:**

- **Requests e funções duplicadas** para recuperar o mesmo dado.
- Complexidade desnecessária para uma informação que já pode ser obtida diretamente a partir do token da requisição.
- Aumenta a chance de bugs e dificulta centralizar regras de autenticação/autorização.

**Solução proposta:**

- Remover funções e variáveis redundantes nos arquivos citados.
- Caso seja necessário utilizar o `user_id` no frontend, expor essa informação diretamente em uma rota apropriada (ex.: `/shared/possible-values` já apontada) em vez de múltiplas funções repetidas.

obs: As requisições para buscar o `id` do funcionário logado são desnecessárias. Sempre que for preciso acessar informações do usuário logado, esses dados devem ser atribuídos diretamente na rota `/shared/possible-values`. Além disso, nenhuma rota precisa mais receber o `id` do usuário manualmente, pois o backend já pode extrair essa informação do \*\*token da request\*\* de forma segura e padronizada.

#### **4.2 Ocorrência 2 – Requisições possible-values e user**

**Local:**  
Página Médico regulador.

**Descrição:**  
As requisições `GET /shared/possible-values` e `GET /user` apresentam problemas já identificados nas **Ocorrência 2** e **Ocorrência 4** (Página Home (TARM)). Ambas trazem dados redundantes, em excesso e em pontos onde não são necessários, resultando em sobrecarga de requests e processamento desnecessário no front-end.

**Solução proposta:**  
Aplicar a mesma estratégia de correção definida para as ocorrências anteriores:

- Centralizar os dados necessários na rota `GET /shared/possible-values`, evitando duplicidade com `GET /user`.
- Restringir o retorno das rotas para apenas os campos realmente usados pelo front.
- Eliminar chamadas redundantes, reaproveitando os dados já carregados na página.

**Obs:**  
Esta ocorrência não exige uma nova solução técnica, mas sim a **aplicação da mesma refatoração já descrita nas Ocorrências 2 e 4**. Ambas as requisições tem a mesma correção da **Ocorrência 2 e Ocorrência 4 do médico regulador.**

#### **4.3 Ocorrência 3 – Requisições desnecessárias** `/user/{id}` **e** `/employee/user_id/{id}`**

**Local:**  
Pontos do sistema Médico Regulador onde são feitas consultas individuais ao usuário logado.

**Descrição:**  
As rotas `GET /user/{id}` e `GET /employee/user_id/{id}` estão sendo chamadas passando o ID do usuário apenas para recuperar informações que não são relevantes ou já estão disponíveis em outras partes do sistema.  
Esse comportamento gera requests redundantes e aumenta o tempo de carregamento das páginas.

**Solução proposta:**

- Remover o uso das rotas `GET /user/{id}` e `GET /employee/user_id/{id}`.
- Centralizar as informações do usuário logado diretamente no retorno da rota `GET /shared/possible-values`.
- Garantir que todas as páginas e componentes que necessitem de informações do usuário logado consumam exclusivamente essa rota.

#### **4.4 Ocorrência 4 – Requisições redundantes de incident**

**Local:**  
Página Médico Regulador (MR) – Detalhamento de Ocorrências

**Descrição:**  
Foram identificadas três requisições distintas sendo executadas ao acessar o detalhe de uma ocorrência:

- `GET /incident/362?include_history=true`
- `GET /mobile-unit/incident/362`
- `GET /incident/prank-calls/(43)%2099806-8708`

[![image.png](/docs-preview/img/plano-de-refatoracao-overfetch-underfetch-e-boas-praticas-em-requests-11.png)](https://ajuda.digitalsys.com.br/uploads/images/gallery/2025-10/i6PKd6GttlJkO1nd-image.png)

[![image.png](/docs-preview/img/plano-de-refatoracao-overfetch-underfetch-e-boas-praticas-em-requests-12.png)](https://ajuda.digitalsys.com.br/uploads/images/gallery/2025-10/QN3NEyZsKBqgLYij-image.png)

Essas chamadas ocorrem simultaneamente, trazendo informações sobre o mesmo incidente ou dados complementares que poderiam ser obtidos em uma única resposta consolidada. Além disso, sempre que o usuário clica novamente em uma ocorrência já aberta, as mesmas requisições são executadas novamente, mesmo com os dados já carregados, resultando em consumo desnecessário de rede e processamento.

#### **4.4 Ocorrência 5** **Occurrence-view**

Na **OccurrenceView** foram identificadas diversas requests durante a renderização, algumas delas inclusive **repetidas**, resultando em problemas de **overfetch** e **uso desnecessário de rede**, todas as requisições são feitas ao entrar nessa pagina.

**Descrição:**  
Durante a renderização da página OccurrenceView, foram identificadas diversas requisições executadas simultaneamente, incluindo chamadas repetidas e algumas desnecessárias, conforme registrado na inspeção de rede. Todas essas requests são disparadas assim que a página é carregada, ocasionando **overfetch** e uso excessivo de rede.

[![image.png](/docs-preview/img/plano-de-refatoracao-overfetch-underfetch-e-boas-praticas-em-requests-13.png)](https://ajuda.digitalsys.com.br/uploads/images/gallery/2025-10/i3XCtSGCadBpCzS9-image.png)

Além disso, há requisições voltadas apenas para recuperar o ID ou nome do usuário logado, informação que já está disponível de forma centralizada e não precisa ser buscada novamente.

**Problema:**

- Execução de múltiplas requisições redundantes na renderização inicial.
- Falta de controle de cache ou reutilização de dados já carregados.
- Requisições desnecessárias para dados do usuário logado, impactando desempenho.

**Solução proposta:**

- Consolidar os dados necessários da OccurrenceView em **uma única request** de inicialização, eliminando duplicidades.
- Garantir que as informações do usuário logado (ex.: nome, ID) sejam obtidas a partir da rota `/shared/possible-values`, conforme definido nas ocorrências anteriores.
- Revisar os serviços de sincronização (`incident_sync`, `incident_type_sync`, etc.) para que sejam executados apenas quando realmente necessários.

#### **4.5 Ocorrência 5 – Requisições redundantes na OccurrenceView**

**Local:**  
Componente/página **OccurrenceView**

**Descrição:**  
Durante a renderização e navegação dentro da página **OccurrenceView**, foram identificadas diversas requisições executadas de forma redundante.  
Todas as requests são disparadas assim que a página é carregada e também **sempre que o usuário alterna entre os formulários internos** (ex.: **Dados Básicos**, **Ocorrência**, **Paciente**, **Regulação** e **Conclusão**).

A análise de rede mostra repetição de chamadas para as mesmas rotas a cada troca de aba ou formulário, conforme evidenciado na captura de rede. Esse comportamento gera **overfetch**, uso desnecessário de banda e aumento no tempo de resposta da interface.

[![image.png](/docs-preview/img/plano-de-refatoracao-overfetch-underfetch-e-boas-praticas-em-requests-14.png)](https://ajuda.digitalsys.com.br/uploads/images/gallery/2025-10/tFvjaIzSoDukGvDo-image.png)

A imagem abaixo é referente as requisições do fluxo de clicar em cada aba somente uma vez. 

[![image.png](/docs-preview/img/plano-de-refatoracao-overfetch-underfetch-e-boas-praticas-em-requests-15.png)](https://ajuda.digitalsys.com.br/uploads/images/gallery/2025-10/QRStDPnUoiGhr3W1-image.png)

**Problema:**

- Execução repetida de múltiplas requisições mesmo em fluxo de navegação simples.
- Falta de cache e de reaproveitamento de dados entre as abas.
- Requisições desnecessárias para informações já carregadas (usuário logado e dados de incidente).
- Impacto direto na performance e tempo de carregamento das seções.

**Solução proposta:**

- Consolidar todas as informações necessárias da **OccurrenceView** em **uma única requisição de inicialização**.

#### **4.6 unit-selection**

**Local:**  
Componente/página **UnitSelection**

**Descrição:**  
Na tela **UnitSelection**, foi identificado que as funções **onMounted** e **fetchData** (chamada dentro do **watch**) executam as mesmas requisições de forma redundante.  
Isso faz com que, ao montar o componente e sempre que o **watch** é acionado, os mesmos dados sejam buscados novamente, gerando **requisições duplicadas** e consumo desnecessário de rede.

Esse comportamento é recorrente ao entrar na página e também ao alterar parâmetros observados pelo **watch**, mesmo quando as informações já foram previamente carregadas.

[![image.png](/docs-preview/img/plano-de-refatoracao-overfetch-underfetch-e-boas-praticas-em-requests-16.png)](https://ajuda.digitalsys.com.br/uploads/images/gallery/2025-10/PPkTbfSqTjIVPhqM-image.png)[![image.png](/docs-preview/img/plano-de-refatoracao-overfetch-underfetch-e-boas-praticas-em-requests-17.png)](https://ajuda.digitalsys.com.br/uploads/images/gallery/2025-10/r1xiKaRXwVN9af7C-image.png)

[![image.png](/docs-preview/img/plano-de-refatoracao-overfetch-underfetch-e-boas-praticas-em-requests-18.png)](https://ajuda.digitalsys.com.br/uploads/images/gallery/2025-10/oAzftgBM6sbbuk7M-image.png)

**Problema:**

- Execução de duas requisições idênticas (em **onMounted** e **watch**).
- Falta de controle para evitar chamadas repetidas.
- Impacto negativo no desempenho e tempo de carregamento da tela.

**Solução proposta:**

- Unificar a lógica de carregamento de dados, mantendo apenas uma das abordagens (**onMounted** **ou** **watch**).
- Caso seja necessário atualizar os dados dinamicamente via **watch**, remover a chamada redundante em **onMounted**, garantindo que apenas o **watch** seja responsável pelo carregamento quando houver mudança real de parâmetros.

#### **4.7 Ocorrência 7 – Requisições redundantes na UnitSelection**

[![image.png](/docs-preview/img/plano-de-refatoracao-overfetch-underfetch-e-boas-praticas-em-requests-19.png)](https://ajuda.digitalsys.com.br/uploads/images/gallery/2025-10/hByFZcFQnusNIzwR-image.png)

**Local:**  
Componente/página **UnitSelection**

**Descrição:**  
Durante o carregamento da página **UnitSelection**, são realizadas três requisições para popular as informações iniciais:

- `GET /technical-decision/incident/{id}`
- `GET /incident/{id}?include_history=false`
- `GET /mobile-unit-type`

As duas primeiras rotas (`/technical-decision/incident/{id}` e `/incident/{id}?include_history=false`) retornam dados sobre o mesmo incidente, resultando em **duplicidade de informação** e **requisições desnecessárias**.  
Essas chamadas poderiam ser consolidadas em uma única rota que trouxesse apenas os dados realmente necessários para popular a tela, incluindo as informações do paciente associadas ao veículo selecionado anteriormente.

**Problema:**

- Execução de requisições redundantes para o mesmo contexto de incidente.
- Uso ineficiente de rede e aumento do tempo de resposta.
- Dificuldade de manutenção devido à sobreposição de dados entre endpoints diferentes.

**Solução proposta:**

- Manter apenas **duas rotas essenciais** para a página:
    1. `/mobile-unit-type` – para carregar os tipos de viatura disponíveis.
    2. Uma nova rota unificada que retorne as informações do paciente e do veículo associado ao incidente selecionado (substituindo as chamadas para `/technical-decision/incident/{id}` e `/incident/{id}?include_history=false`).
- Ajustar o backend para retornar somente os campos realmente utilizados pela interface, evitando sobrecarga de dados.
- Atualizar o frontend para consumir exclusivamente essas duas rotas, removendo chamadas redundantes e simplificando o fluxo de inicialização da tela.

#### **4.8 Ocorrência 8 – Falta de filtragem de tipos de viaturas na rota** `/mobile-unit-type`

**Local:**  
Componente/página **UnitSelection**  
Rota: `GET /mobile-unit-type`

**Descrição:**  
Atualmente, a rota **/mobile-unit-type** retorna todos os tipos de viaturas cadastrados no sistema, sem aplicar nenhum critério de filtragem quanto ao status (ativo/inativo).  
Esse comportamento faz com que veículos inativos também sejam listados na tela **UnitSelection**, obrigando o front a realizar a filtragem.

**Problema:**

- Retorno de dados desnecessários (viaturas inativas).
- Aumento desnecessário no volume de dados trafegados.

**Solução proposta:**

- Adicionar uma **flag de filtragem** na rota `/mobile-unit-type` para permitir o retorno apenas de tipos de veículos ativos (ex.: `GET /mobile-unit-type?active=true`). por padrão retorna todos para não gerar problemas com as rotas do admin
- Garantir que o frontend consuma essa flag, exibindo exclusivamente os tipos de viaturas disponíveis para uso operacional.

#### **4.9 Ocorrência 9 – Retorno excessivo e falta de filtragem nas rotas da aba Conclusão**

**Local:**  
Componente/página **OccurrenceView** → Aba **Conclusão**  
Rotas envolvidas:

- `GET /technical-decision-action`
- `GET /intercurrence`
- `GET /health-unit`

**Descrição:**  
Na aba **Conclusão** do formulário, foram identificadas três rotas com problemas relacionados à ausência de filtragem e volume excessivo de dados retornados.

As rotas **/technical-decision-action** e **/intercurrence** estão retornando registros **excluídos ou inativos**, exigindo que o frontend realize a filtragem manual para ocultá-los — comportamento que aumenta a complexidade da aplicação e o tempo de carregamento.

Já a rota **/health-unit** retorna um **JSON com aproximadamente 7.458 objetos**, enviado integralmente a cada requisição, apenas para popular o campo **“Destino Paciente”**. Esse volume é desnecessário e causa lentidão perceptível na renderização e busca.

**Problema:**

- Falta de filtragem de registros ativos nas rotas `/technical-decision-action` e `/intercurrence`.
- Retorno de dados massivo na rota `/health-unit`.
- Processamento excessivo no frontend e impacto negativo no desempenho da aba Conclusão.

**Solução proposta:**

- Aplicar filtro diretamente no backend para que as rotas **/technical-decision-action** e **/intercurrence** retornem apenas registros **ativos**, eliminando a necessidade de filtragem no frontend.
- Alterar a rota **/health-unit** para funcionar com **busca dinâmica (lazy load)**, adotando a mesma lógica já utilizada em outros campos de busca:
    - O usuário digita parte do nome;
    - A API retorna apenas as unidades que correspondem à concordância;
    - O resultado deve ser limitado a **no máximo 20 registros** por requisição.

### **5. Ocorrências Identificadas Operador de frota**

Na **FleetOperations.vue** foram identificadas diversas requests durante a renderização, resultando em problemas de **overfetch** e **uso desnecessário de rede**.

[![image.png](/docs-preview/img/plano-de-refatoracao-overfetch-underfetch-e-boas-praticas-em-requests-20.png)](https://ajuda.digitalsys.com.br/uploads/images/gallery/2025-10/UrTj4b5qECfmTpHS-image.png)

Algumas dessas ocorrências já haviam sido relatadas em outros módulos, como **Médico Regulador** e **TARM**. Um exemplo são as buscas nas rotas `user` e `possible-values`.

Vale destacar que a rota `possible-values` está sendo substituída pela `shared/default-values`, que já retorna os valores relacionados ao usuário, evitando requisições redundantes.

#### **5.1 Ocorrência 1 – Requests redundantes ao selecionar a mesma ocorrência**

**Local:**  
Componente/página FleetOperations.vue → Tabela de Ocorrências

**Descrição:**  
Ao selecionar uma ocorrência na tabela, é feita uma requisição para a rota `/incident/{id}?include_history=false`. No entanto, se a **mesma ocorrência for selecionada mais de uma vez**, novas requests continuam sendo disparadas, gerando **overfetch** e consumo desnecessário de rede.

Além disso, atualmente a rota retorna um JSON completo com todos os detalhes da ocorrência, muitos dos quais não são necessários para o **Operador de Frota**, resultando em carregamento e processamento excessivo no frontend.

[![image.png](/docs-preview/img/plano-de-refatoracao-overfetch-underfetch-e-boas-praticas-em-requests-21.png)](https://ajuda.digitalsys.com.br/uploads/images/gallery/2025-10/pGPeYFgADxvgP3lW-image.png)

**Problema:**

- Requests redundantes ao selecionar a mesma ocorrência mais de uma vez.
- Retorno de dados completo, incluindo informações não utilizadas pelo Operador de Frota.
- Processamento desnecessário no frontend e impacto negativo no desempenho da tabela de ocorrências.

**Solução proposta:**

- Implementar controle de seleção no frontend para que a mesma ocorrência não dispare múltiplas requisições.
- Criar uma rota dedicada que retorne **apenas os dados básicos necessários** para o Operador de Frota, reduzindo o volume de dados transferidos e melhorando a performance.

#### **5.2 Ocorrência 2** **- Dados do campo “Transferir para”** 

**Local:**  
Componente/página FleetOperations.vue → Formulário de Ocorrência → Campo “Transferir para”

[![image.png](/docs-preview/img/plano-de-refatoracao-overfetch-underfetch-e-boas-praticas-em-requests-22.png)](https://ajuda.digitalsys.com.br/uploads/images/gallery/2025-10/C0ZLNj8wBsdbo8Ge-image.png)

**Rotas envolvidas:**  
GET /employee/search?query={termo}

**Descrição:**  
O campo **“Transferir para”** atualmente busca dados na rota `/possible-values`, que **não retorna informações corretas para este caso**. Existe uma rota específica, `/employee/search?query=`, destinada a fornecer os dados corretos de funcionários conforme o termo digitado pelo usuário.

**Problema:**

- Dados incorretos sendo retornados pelo campo “Transferir para”.
- Uso inadequado da rota `/possible-values` para buscar informações de funcionários.

**Solução proposta:**

- Alterar o campo “Transferir para” para consumir a rota `/employee/search?query=`, garantindo que apenas funcionários correspondentes ao termo digitado sejam retornados.
- Implementar **lazy loading** para reduzir o volume de dados transferidos e otimizar a performance.

#### **5.3 Ocorrência 3** **- Pagina fleet-occurrence**

**Rotas envolvidas:**  
GET /dispatch/bff/dispatch-data/{id}  
GET /incident/{id}?include\_history=false  
GET /dispatch/incident/{id}

**Descrição:**  
Durante a renderização da página **FleetOccurrence**, foram identificadas diversas requisições executadas para popular os dados da ocorrência. Algumas delas são **repetidas**, resultando em sobrecarga de rede e processamento desnecessário.

O problema se agrava ao selecionar uma ocorrência que **já possui veículo despachado**, pois o número de requisições duplicadas aumenta consideravelmente.

Além disso, ao **selecionar um checklist**, o mesmo comportamento se repete, indicando que há **falta de controle na lógica de carregamento de dados** e ausência de reaproveitamento das informações já obtidas.

[![image.png](/docs-preview/img/plano-de-refatoracao-overfetch-underfetch-e-boas-praticas-em-requests-23.png)](https://ajuda.digitalsys.com.br/uploads/images/gallery/2025-10/tuImrPX15q5ImKkP-image.png)

**Problema:**

- Execução de múltiplas requisições redundantes para a mesma ocorrência.
- Aumento do número de requests em ocorrências com veículo despachado.
- Requisições repetidas também ao selecionar checklists.

**Solução proposta:**

- Criar uma **rota unificada** para retornar todos os dados necessários à página **FleetOccurrence**, eliminando a necessidade de múltiplas chamadas.
- Revisar a **lógica de carregamento e renderização** para evitar requisições repetidas, especialmente ao selecionar ocorrências já carregadas ou clicar em um checklists.
- Avaliar a consolidação das rotas `/dispatch/bff/dispatch-data/{id}` e `/dispatch/incident/{id}`.

#### **5.4 Ocorrência 4** **- Falta de filtragem e uso de rotas redundantes na página ManageFleet**

**Local:**  
Componente/página ManageFleet.vue

**Rotas envolvidas:**  
GET /mobile-unit-type  
GET /mobile-unit-type?active=true  
GET /mobile-unit?active\_only=true  
GET /mobile-unit

**Descrição:**  
Na página **ManageFleet**, foram identificados problemas relacionados à ausência de filtragem no backend e ao uso de rotas redundantes para carregar informações sobre **unidades móveis**.

A rota `/mobile-unit-type` atualmente retorna **todos os tipos de unidade móvel**, e o frontend realiza a filtragem manual para exibir apenas os ativos. Esse comportamento deveria ser tratado diretamente no backend, por meio de um parâmetro, conforme já implementado em outras rotas:

[![image.png](/docs-preview/img/plano-de-refatoracao-overfetch-underfetch-e-boas-praticas-em-requests-24.png)](https://ajuda.digitalsys.com.br/uploads/images/gallery/2025-10/Gas4nomlBzJUlFaw-image.png)

Além disso, foram identificadas duas rotas distintas para obtenção de unidades móveis

**https://e-sus-urgencias-api.digitalsysdev.com.br/mobile-unit?active\_only=true**

**https://e-sus-urgencias-api.digitalsysdev.com.br/mobile-unit**

Atualmente ambas são utilizadas, sendo que apenas uma deveria ser suficiente.

Outro ponto observado é o uso de uma rota que retorna um **objeto extenso com diversos dados desnecessários** apenas para popular o campo de seleção **“Selecione uma unidade móvel”**. Para esse caso, seria suficiente retornar apenas os campos **id** e **nome**, evitando tráfego e processamento excessivo.

**Problema:**

- Falta de filtragem no backend da rota `/mobile-unit-type`, obrigando o frontend a tratar registros inativos.
- Uso redundante das rotas `/mobile-unit` e `/mobile-unit?active_only=true`.
- Carregamento excessivo de dados para popular campos simples de seleção.

**Solução proposta:**

- Ajustar a rota `/mobile-unit-type` para suportar o parâmetro `?active=true`, retornando apenas registros ativos.
- Consolidar o uso de uma única rota para listagem de unidades móveis, preferencialmente `/mobile-unit?active_only=true`.
- Criar uma rota específica e otimizada para o select **“Selecione uma unidade móvel”**, retornando apenas `o necessario`.
- Eliminar filtragens e tratamentos redundantes no frontend, reduzindo o número de requests e o volume de dados processados.

#### **5.5 Ocorrência 5** **- Falta de filtragem e repetição de requisições na página Team**

**Local:**  
Componente/página Team.vue

**Rotas envolvidas:**  
GET /professional-type  
GET /user  
GET /unallocated  
GET /unallocated?page={n}&amp;page\_size={n}  
GET /unallocated?include\_self={true|false}

[![image.png](/docs-preview/img/plano-de-refatoracao-overfetch-underfetch-e-boas-praticas-em-requests-25.png)](https://ajuda.digitalsys.com.br/uploads/images/gallery/2025-10/iJ4UDlsvLUdOPUWx-image.png)**Descrição:**  
Na página **Team**, foram identificadas falhas relacionadas à ausência de filtragem no backend e à repetição de requisições para as rotas de **unallocated**.

A rota `/professional-type` atualmente retorna todos os tipos de profissionais, e o frontend realiza a filtragem manual para exibir apenas os ativos. Esse comportamento deve ser tratado diretamente no backend, utilizando o parâmetro `?active_only=true`, conforme já adotado em outras rotas.

Além disso, a rota `/user` (getUser) está sendo chamada sem necessidade (é possivel adaptar a logica sem a utilização dessa rota) e deve ser removida da página.

Também foi observada **repetição de chamadas** nas rotas `/unallocated`, inclusive com variações de parâmetros (`page`, `include_self`), gerando múltiplas requisições redundantes para obter os mesmos dados.

**Problema:**

- Falta de filtragem de registros ativos na rota `/professional-type`.
- Uso desnecessário da rota `/user` (getUser).
- Requisições duplicadas e redundantes nas rotas `/unallocated`.

**Solução proposta:**

- Ajustar a rota `/professional-type` para suportar o parâmetro `?active_only=true`, eliminando a necessidade de filtragem no frontend.
- Remover a chamada da rota `/user` (getUser) da página.
- Revisar a lógica de carregamento das rotas `/unallocated` para evitar repetições desnecessárias
- Consolidar as chamadas de `/unallocated` em uma única requisição otimizada, garantindo eficiência e consistência dos dados.