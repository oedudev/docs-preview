
# BDD Denúncias

**Bloco 1: Denuncia realizada por Usuários Fã**

**Cenário:** Envio de denúncia com sucesso

**Dado** que eu esteja logado no sistema como um Usuário Fã

**E** esteja na tela "Fazer Denúncia"

**E** tenha preenchido o campo "Nome Completo" com um nome válido

**E** eu preencher o campo "Email" com um e-mail válido

**E** eu preencher o campo "Descrição da Denúncia" com um texto dentro do limite de caracteres

**Quando** eu clicar no botão "Enviar Denúncia"

**Então** a denúncia deve ser registrada no sistema

**E** devo receber uma mensagem de confirmação do envio

**--------------------------------------**

**Cenário:** Tentativa de envio de denúncia com nome em branco

**Dado** que eu esteja logado no sistema como um Usuário Fã

**E** esteja na tela "Fazer Denúncia"

**E** não tenha preenchido o campo "Nome Completo"

**Quando** eu clicar no botão "Enviar Denúncia"

**Então** devo visualizar uma mensagem de erro indicando que o nome completo é obrigatório

**--------------------------------------**

**Cenário:** Tentativa de envio de denúncia com e-mail em branco

**Dado** que eu esteja logado no sistema como um Usuário Fã

**E** que eu esteja na tela "Fazer Denúncia"

**E** não tenha preenchido o campo "e-mail"

**Quando** eu clicar no botão "Enviar Denúncia" sem preencher o "Email"

**Então** devo visualizar uma mensagem de erro indicando que o e-mail é obrigatório

**--------------------------------------**

**Cenário:** Tentativa de envio de denúncia com formato de e-mail inválido

**Dado** que eu esteja logado no sistema como um Usuário Fã

**E** que eu esteja na tela "Fazer Denúncia"

**E** não tenha preenchido o campo "e-mail" com um e-mail inválido

**Quando** eu clicar no botão "Enviar Denúncia" sem preencher o "Email"

**Então** devo visualizar uma mensagem de erro indicando que o formato e-mail é inválido

**--------------------------------------**

**Cenário:** Tentativa de envio de denúncia com descrição em branco

**Dado** que eu esteja logado no sistema como um Usuário Fã

**E** que eu esteja na tela "Fazer Denúncia"

**E** não tenha preenchido o campo a "Descrição da Denúncia"

**Quando** eu clicar no botão "Enviar Denúncia"

**Então** devo visualizar uma mensagem de erro indicando que a descrição é obrigatória

**--------------------------------------**

**Cenário:** Tentativa de envio de denúncia excedendo o limite de caracteres na descrição

**Dado** que eu esteja logado no sistema como um Usuário Fã

 **E** que eu esteja na tela "Fazer Denúncia"

**Quando** eu preencher o campo "Descrição da Denúncia" com um texto maior que 500 caracteres

**Então** devo visualizar uma mensagem de erro indicando que a quantidade máxima de caracteres foi excedida

**--------------------------------------**

**Cenário:** Cancelamento do preenchimento da denúncia

**Dado** que eu esteja logado no sistema como um Usuário Fã

**E** que eu esteja na tela "Fazer Denúncia"

**E** que eu tenha preenchido alguns campos do formulário

**Quando** eu clicar no botão "Cancelar"

**Então** devo ser redirecionado para a página anterior

**--------------------------------------**

**Cenário:** Navegação para a página anterior usando o botão "Voltar"

**Dado** que eu esteja logado no sistema como um Usuário Fã

**E** que eu esteja na tela "Fazer Denúncia"

**Quando** eu clicar no botão "Voltar" no topo da página

**Então** devo ser redirecionado para a página anterior

**Bloco 2: Denuncia realizada por Usuários Criador**

**Cenário:** Envio de denúncia com sucesso

**Dado** que eu esteja logado no sistema como um Usuário Criador

**E** esteja na tela "Denunciar Cliente"

**E** tenha selecionado uma "Categoria da Denúncia"

**E** tenha selecionado uma opção em "Especifique o problema"

**E** tenha Preenchido o “Nome do Cliente”

**E** tenha preenchido o campo "Descrição da Denúncia" com um texto dentro do limite de caracteres

**Quando** eu clicar no botão "Enviar Denúncia"

**Então** a denúncia deve ser registrada no sistema

**E** devo receber uma mensagem de confirmação do envio

**--------------------------------------**

**Cenário:** Exibição da subcategoria ao selecionar a categoria principal

**Dado** que eu esteja logado no sistema como um Usuário Criador

**E** esteja na tela "Denunciar Cliente"

**Quando** eu selecionar a categoria “Categoria da Denúncia”

**Então** a seção "Especifique o problema:" deve exibir opções relacionadas à categoria de denúncia selecionada

**--------------------------------------**

**Cenário:** Tentativa de envio sem selecionar categoria de denúncia

**Dado** que eu esteja logado no sistema como um Usuário Criador

**E** esteja na tela "Denunciar Cliente"

**E** não tenha selecionado uma "Categoria da Denúncia"

**Quando** eu clicar no botão "Enviar Denúncia"

**Então** devo visualizar uma mensagem de erro indicando que a categoria é obrigatória

**--------------------------------------**

**Cenário:** Tentativa de envio sem selecionar a especificação do problema

**Dado** que eu esteja logado no sistema como um Usuário Criador

**E** esteja na tela "Denunciar Cliente"

**E** tenha selecionado a categoria "Problemas de Pagamento"

**E** não tenha selecionado uma opção em "Especifique o problema:"

**Quando** eu clicar no botão "Enviar Denúncia"

**Então** devo visualizar uma mensagem de erro indicando que a especificação do problema é obrigatória

**--------------------------------------**

**Cenário:** Tentativa de envio de denúncia se preenchimento da descrição da denúncia

**Dado** que eu esteja logado no sistema como um Usuário Criador

**E** que eu esteja na tela "Denunciar Cliente"

**E** não tenha preenchido o campo a "Descrição da Denúncia"

**Quando** eu clicar no botão "Enviar Denúncia"

**Então** devo visualizar uma mensagem de erro indicando que a descrição é obrigatória

**--------------------------------------**

**Cenário:** Tentativa de envio de denúncia excedendo o limite de caracteres na descrição

**Dado** que eu esteja logado no sistema como um Usuário Criador

**E** que eu esteja na tela "Denunciar Cliente"

**Quando** eu preencher o campo "Descrição da Denúncia" com um texto maior que 500 caracteres

**Então** devo visualizar uma mensagem de erro indicando que a quantidade máxima de caracteres foi excedida

**--------------------------------------**

**Cenário:** Cancelamento do preenchimento da denúncia

**Dado** que eu esteja logado no sistema como um Usuário Criador

**E** que eu esteja na tela "Denunciar Cliente"

**E** que eu tenha preenchido alguns campos do formulário

**Quando** eu clicar no botão "Cancelar"

**Então** devo ser redirecionado para a página anterior

**--------------------------------------**

**Cenário:** Navegação para a página anterior usando o botão "Voltar"

**Dado** que eu esteja logado no sistema como um Usuário Criador

**E** que eu esteja na tela "Denunciar Cliente"

**Quando** eu clicar no botão "Voltar" no topo da página

**Então** devo ser redirecionado para a página anterior