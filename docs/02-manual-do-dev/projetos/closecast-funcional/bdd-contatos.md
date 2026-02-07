
# BDD Contatos

**Cenário:** Envio de contato com sucesso

**Dado** que eu esteja na página "Contato CloseCast"

**Quando** eu selecionar o tipo de contato "Dúvida"

**E** eu preencher o campo "Nome Completo" com um nome válido

**E** eu preencher o campo "CPF" com um CPF válido

**E** eu preencher o campo "Email" com um email válido

**E** eu preencher a "Descrição" com um texto dentro do limite de caracteres

**E** eu clicar no botão "Enviar Mensagem"

**Então** a mensagem deve ser enviada com sucesso

**E** devo visualizar uma mensagem de confirmação

**-------------------------------------**

**Cenário:** Tentativa de envio sem selecionar o tipo de contato

**Dado** que eu esteja na página "Contato CloseCast"

**E** que eu tenha preenchido todos os campos de informação

**Quando** eu clicar no botão "Enviar Mensagem" sem selecionar um "Tipo de Contato"

**Então** devo visualizar uma mensagem de erro indicando que a seleção do tipo de contato é obrigatória

**-------------------------------------**

**Cenário:** Tentativa de envio com nome em branco

**Dado** que eu esteja na página "Contato CloseCast"

**E** que eu tenha preenchido todos os campos, exceto o "Nome Completo"

**Quando** eu clicar no botão "Enviar Mensagem"

**Então** devo visualizar uma mensagem de erro indicando que o nome é obrigatório **E** a mensagem não deve ser enviada

**Cenário:** Tentativa de envio com formato de email inválido

**Dado** que eu esteja na página "Contato CloseCast"

**E** que eu tenha preenchido os campos de nome, CPF e descrição

**Quando** eu preencher o campo "Email" com um formato inválido

**E** eu clicar no botão "Enviar Mensagem"

**Então** devo visualizar uma mensagem de erro indicando que o formato do email é inválido

**-------------------------------------**

**Cenário:** Tentativa de envio com descrição excedendo o limite de caracteres

**Dado** que eu esteja na página "Contato CloseCast"

**Quando** eu preencher o campo "Descreva detalhadamente sua solicitação" com um texto maior que 500 caracteres

**Então** devo visualizar um alerta sobre o limite de caracteres

**-------------------------------------**

**Cenário:** Cancelamento do preenchimento do formulário

**Dado** que eu esteja na página "Contato CloseCast"

**E** que eu tenha preenchido alguns campos do formulário

 **Quando** eu clicar no botão "Cancelar"

**Então** devo ser redirecionado para a página anterior

**E** nenhuma mensagem deve ser enviada

**-------------------------------------**

**Cenário:** Navegação para a página anterior usando o botão "Voltar"

**Dado** que eu esteja na página "Contato CloseCast"

**Quando** eu clicar no botão "Voltar" no topo da página

**Então** devo ser redirecionado para a página anterior

