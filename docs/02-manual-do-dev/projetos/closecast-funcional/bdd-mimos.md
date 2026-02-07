
# BDD Mimos

**Cenário:** Agradecer mimo - Personalizado

**Dado** que eu seja um usuário criador

**E** um usuário fã me enviou um mimo

**E** que eu tenho escrito uma nota de agradecimento

**Quando** eu clicar em "Enviar Personalizado"

**Então** o usuário fã deve ser notificado

**E** deve visualizar a mensagem escrita pelo criador

**E** deve visualizar a qual mimo o agradecimento se refere

**Cenário:** Enviar mimo

**Dado** que eu sou um usuário fã

**E** que eu acesse o perfil de um criador

**E** que eu clique em "Enviar mimo"

**E** que eu selecione mimos dentre as opções

**E** que eu escreva uma mensagem anexa aos mimos

**Quando** eu concluir o pagamento

**Então** devo ser direcionado à uma pagina de "Mimo enviado com sucesso"

**E** o criador destinatário deve ser notificado

**E** a soma do valor dos mimos enviados devem ser adicionados à conta do criador

**Cenário:** Atualizar dados

**Dado** que eu seja um usuário criador

**E** que eu esteja na página de relatório de vendas (mimos)

**Quando** eu clicar em "Atualizar"

**Então** os dados da página devem ser atualizados com as informações mais recentes