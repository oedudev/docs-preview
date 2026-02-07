
# BDD Web

##### Login com senha

**Cenário:** Login bem sucedido

**Dado** que eu esteja na página de login

**E** que eu insira o usuário **correto**

**E** que eu insira a senha **correta**

**Quando** eu clicar no botão “**entrar**”

**Então** não devo receber nenhuma mensagem de erro

**E** devo poder acessar o sistema com o meu usuário

**Cenário:** Senha incorreta

**Dado** que eu esteja na página de login

**E** que eu insira o usuário **correto**

**E** que eu insira a senha **incorreta**

**Quando** eu clicar no botão “**entrar**”

**Então** devo receber uma mensagem de erro

**E** a mensagem **não deve indicar** se eu inseri a senha e/ou o usuário incorreto

##### Login com Google

**Cenário**: Login bem sucedido

**Dado** que eu esteja na página de login

**E** que eu escolha uma fazer o login por meio do Google

**Quando** eu inserir corretamente minhas informações

**Então** não devo receber uma mensagem de erro

**E** devo acessar o sistema com o meu usuário

**E** o campo **email da conta deve ser preenchido com o email do Google**

**E** o campo nome da conta deve ser preenchido com o nome d**o Google**

**E** o ícone de usuário da conta deve ser preenchido com o nome d**o Google**

##### Criação de conta de fã

**Cenário**: Não visualizar inputs para influencer quando criando conta comum  
  
**Dado** que eu esteja na página de criação de contas

**E** que eu selecione a opção “**Sou Fã**”

**Quando** eu entrar nas páginas para input de dados

**Então** não devo ver nenhum campo referente a informações para influencer

**Cenário**: Campo obrigatório faltante/inválido

**Dado** que eu esteja na página de criação de contas

**E** que eu selecione a opção “**Sou Fã**”

**E** entro nas páginas para input de dados

**E** deixo um campo obrigatório em branco ou com dados inválidos

**Quando** eu clicar em “Próximo” ou “Finalizar”

**Então** o sistema não deve me deixar avançar

**E** devo receber uma mensagem descrevendo o que está errado

**E** o campo problemático deve ficar em destaque

##### Criação de conta para criadores

**Cenário**: Visualização de campos para influencer

**Dado** que eu esteja na página de criação de contas

**E** que eu selecione a opção “**Sou criador**”

**Quando** eu acessar a pagina de input de dados

**Então** devo poder visualizar os campos de input exclusivos para criadores

**Cenário**: Campo obrigatório faltante/inválido

**Dado** que eu esteja na página de criação de contas

**E** que eu selecione a opção “**Sou criador**”

**E** entro nas páginas para input de dados

**E** deixo um campo obrigatório em branco ou com dados inválidos

**Quando** eu clicar em “Próximo” ou “Finalizar”

**Então** o sistema não deve me deixar avançar

**E** devo receber uma mensagem descrevendo o que está errado

**E** o campo problemático deve ficar em destaque

