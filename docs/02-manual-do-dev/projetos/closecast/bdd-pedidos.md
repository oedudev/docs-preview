
# BDD pedidos

##### **Manejo de pedidos**

**Cenário:** Criação de pedido

**Dado** que eu seja um usuário fã

**E** que eu deseje realizar um pedido

**E** eu preencha todas as informações obrigatórias

**Quando** clicar em "Continuar para o pagamento"

**Então** um pedido deve ser criado

**E** deve conter todas as informações que eu preenchi

**E** o status deve ser "Aguardando pagamento"

**E** devo ser redirecionado à página de pagamento

**Cenário**: Preços para diferentes tipos de fotos

**Dado** que eu seja um usuário fã

**E** que eu deseje realizar um pedido do tipo foto

**Quando** eu selecionar o tipo de foto que desejo (Selfie Personalizada, Pose específica, etc...)

**Então** o preço a ser pago deve alterar de acordo com o que selecionei

**Cenário:** Pronúncia do nome - Outro

**Dado** que eu seja um usuário fã

**E** que eu deseje realizar um pedido

**E** que eu opte pela opção "Outro"

**E** que eu preencha o campo com "Exemplo apelido"

**Quando** clicar em "Continuar para o pagamento"  
  
**E** o pedido não deve ser criado

**E** deve conter o que inseri na pronúncia do nome

