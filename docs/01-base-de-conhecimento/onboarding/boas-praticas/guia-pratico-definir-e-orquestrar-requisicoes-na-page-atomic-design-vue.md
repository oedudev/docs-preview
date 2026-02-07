
# Guia prático: definir e orquestrar requisições na Page (Atomic Design + Vue)

### Guia prático: definir e orquestrar requisições na **Page** (Atomic Design + Vue)

Este guia explica, passo a passo e de forma bem detalhada, onde e como concentrar as requisições na Page, mantendo Templates/Organisms/Molecules/Atoms puros e reutilizáveis.

#### 1. Por que a requisição deve ficar na Page?

Separação de responsabilidades (SRP) é um pilar do Atomic Design:

- Page: **fonte da verdade** para dados e efeitos colaterais (requisições). Decide quando buscar dados, com que parâmetros e o que fazer com os resultados.
- Template: organiza layout/slots e distribui props/events. Não busca dados.
- Organisms/Molecules/Atoms: componentes presentacionais/controlados. Recebem dados por props e emitem eventos; não sabem de APIs.

Benefícios:

- Reuso: as mesmas moléculas/organismos funcionam em qualquer página.
- Teste: fica fácil testar Page (integração) e componentes (unitário).
- Evolução: trocar API ou regra de busca não quebra UI.

#### 2. Mapeamento do código de exemplo às camadas

Utilizando um exemplo simples, podemos observar como os componentes se comportam quando aplicamos a separação de responsabilidades. Nesse caso, o valor retornado chega até o template, mas, para fins de simplificação, não será utilizado. A seguir, apresentamos o que cada trecho de código representa.

UsersPage.vue -&gt; Page (requisições,estado,orquestração)

UsersTemplate.vue -&gt; Template (layout, repassa props/events)

SearchField.vue -&gt; Molecule (Input + Button)

Input.vue -&gt; Atom

Button.vue -&gt; Atom

**Quem sabe o quê?**

**UsersPage:** conhece users, query, loading e a função fetchUsers().

**UsersTemplate:** só recebe users, query, loading e reemite eventos.

**SearchField:** recebe modelValue e reemite update:modelValue/search.

**Input/Button:** somente UI e eventos nativos.

#### 3. Exemplo de fluxo de dados

**UsersPage:** Aqui fica a responsabilidade de buscar os dados na API e controlar estado**.**

![](/img/30070a-GXlmHnLHmSEvdaSC-embedded-image-svm3mier.png)

No Vue, o símbolo @ é atalho para v-on, usado para ouvir eventos emitidos por componentes ou elementos. Então vamos utilizar para emitir eventos para o componente filho.

**@update:query="query = $event"**: O filho emite update:query quando o input muda. O pai atualiza a variável query com $event (novo valor).

**@search=”fetchUsers”**: O filho emite search (por exemplo, quando o usuário clica em um botão). O pai executa fetchUsers para atualizar a lista.

**UserTemplate:** Recebe props da Page e emite eventos para a Page e usa SearchField, que é uma molécula, passando query e repassando eventos.

[![image.png](/img/1c576e-BnErKoKpFdPTpBOA-image.png)](https://ajuda.digitalsys.com.br/uploads/images/gallery/2025-09/BnErKoKpFdPTpBOA-image.png)

**defineEmits(\["update:query", "search"\]):** No Vue 3 (com &lt;script setup&gt;), defineEmits é usado para declarar os eventos que o componente pode emitir para o pai.

 <colgroup><col></col><col></col></colgroup>   Evento

  Função

    `update:query`

  Indica que o valor da query mudou (por exemplo, quando o usuário digita algo)

    `search`

  Indica que o usuário quer iniciar a busca

    

**SearchField:** recebe modelValue e reemite update:modelValue/search.

[![image.png](/img/f8413d-YPvcbCi1l4BAvgDB-image.png)](https://ajuda.digitalsys.com.br/uploads/images/gallery/2025-09/YPvcbCi1l4BAvgDB-image.png)

**Input/Button:** somente UI e eventos nativos.

[![image.png](/img/3d304c-gtuW8P8PFbZB1zu0-image.png)](https://ajuda.digitalsys.com.br/uploads/images/gallery/2025-09/gtuW8P8PFbZB1zu0-image.png)

#### 3. Fluxo de ponta a ponta (do clique até os dados)

Podemos observar na imagem que os eventos sempre sobem até o componente Page, enquanto os dados têm sua origem na própria Page e descem para os demais componentes.

[![image.png](/img/96c4cc-M1RmVi6xP5XBhyFK-image.png)](https://ajuda.digitalsys.com.br/uploads/images/gallery/2025-09/M1RmVi6xP5XBhyFK-image.png)

**Regra de ouro:**

- Props descem (dados): Page → Template → Molécula → Átomos.
- Eventos sobem (interações): Átomos → Molécula → Template → Page.
- Page é o único lugar que tem estado e faz requisições.
- Templates e Moleculas apenas reemitem eventos e repassam props.

#### 4. Quando extrair para um composable?

Um composable no Vue 3 é uma função reutilizável que centraliza lógica reativa, como estados, requisições ou cálculos, utilizando a Composition API. Diferente de um componente, que é voltado para interface e interação com o usuário, o composable serve apenas para organizar e compartilhar regras de negócio, mantendo as páginas e templates mais limpos e facilitando a reutilização dessa lógica em diferentes partes do projeto

Em apps grandes, a Page pode ficar "pesada". Você pode mover a lógica de dados para um composable (ex.: src/composables/useUsers.ts) sem mudar o princípio: a Page chama o composable e continua decidindo quando buscar.

Regras para considerar um composable:

- A mesma busca é usada em várias Pages.
- A lógica tem cache, paginação ou normalização complexas.
- Precisa compartilhar estado entre telas.

Mesmo no composable, não invoque API dentro de Template/Organism/Molecule.

#### 4. Anti-padrões a evitar

- Fazer fetch dentro de Template/Organism/Molecule/Atom.
- Passar fetchUsers como prop para ser chamado por baixo (inverte controle).
- Misturar transformações de dados pesadas nos componentes de UI.
- Deixar loading/error escondidos (sem feedback visual).