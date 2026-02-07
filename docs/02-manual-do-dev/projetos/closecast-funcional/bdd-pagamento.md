
# BDD pagamento

##### **Pagamento**

**Cenário:** Selecionar forma de pagamento

**Dado** que eu seja um usuário fã

**E** que eu esteja na página de pagamentos

**Quando** eu selecionar as opções disponíveis para pagamento

**Então** devo visualizar os campos correspondentes ao método selecionado

**Cenário:** Pagamento com boleto

**Dado** que eu seja um usuário fã

**E** que eu esteja na página de pagamentos

**Quando** eu selecione o método "Boleto"

**Então** devo visualizar o código de barras do boleto

**E** o código do boleto para realizar o pagamento

**E** o valor a ser pago deve corresponder ao informado na plataforma

