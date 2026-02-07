
# BDD Perfil de Usuário Fã

**Cenário:** Logout

**Dado** que eu esteja **logado** no sistema

**E** que eu esteja na minha **página de perfil**

**Quando** eu clicar no botão “**Sair**”

**Então** devo ser **deslogado**

**E** direcionado à **página principal** do site

 -------------------------------------------

**Cenário:** Edição de perfil

**Dado** que eu esteja **logado** no sistema

**E** que eu esteja na minha **página de perfil**

**Quando** eu clicar no botão “**Editar Perfil**”

**Então** direcionado para a página de **edição** de perfil de **Usuário Fã**

 -------------------------------------------

**Cenário:** Listar vídeos Solicitados – Com histórico de pedidos

**Dado** que eu esteja **logado** no sistema

**E** que eu esteja na minha **página de perfil**

**Quando** eu clicar no botão “**\_ Vídeos Solicitados**”

**Então** a sessão “**Meus Pedidos**” deve ser populada a **lista** de pedidos que já realizei

 -------------------------------------------

**Cenário:** Listar vídeos Solicitados – Sem histórico de pedidos

**Dado** que eu esteja **logado** no sistema

**E** que eu esteja na minha **página de perfil**

**Quando** eu clicar no botão “**\_ Vídeos Solicitados**”

**Então** a sessão “**Meus Pedidos**” deve ser exibida

 -------------------------------------------

**Cenário:** Listar vídeos recebidos – Com histórico de pedidos concluídos

**Dado** que eu esteja **logado** no sistema

**E** que eu esteja na minha **página de perfil**

**Quando** eu clicar no botão “**\_ Vídeos Recebidos**”

**Então** a sessão “Meus Pedidos” deve ser populada a com **lista completa** de pedidos cujo estado é **concluído**

  -------------------------------------------

**Cenário:** Listar vídeos recebidos – Sem histórico de pedidos concluídos

**Dado** que eu esteja **logado** no sistema

**E** que eu esteja na minha **página de perfil**

**Quando** eu clicar no botão “**\_ Vídeos Recebidos**”

**Então** a sessão “**Meus Pedidos**” deve ser exibida vazia

 -------------------------------------------

**Cenário:** Download de pedido concluído via página de perfil

**Dado** que eu esteja **logado** no sistema

**E** que eu esteja na minha **página de perfil**

**E** que o pedido que eu desejo baixar esteja **concluído**

**Quando** eu clicar no botão “**Baixar**”

**Então** o **download** da mídia referente ao meu pedido deve disparado

 -------------------------------------------

**Cenário:** Acessar tela “Assistir Vídeo”

**Dado** que eu esteja **logado** no sistema

**E** que eu esteja na minha **página de perfil**

**E** que o pedido que eu desejo assistir esteja **concluído**

**Quando** eu clicar no botão “**Assistir**”

**Então** devo ser **direcionado** para a tela “**Assistir Vídeo**” relativa ao pedido selecionado

 -------------------------------------------

**Cenário:** Reprodução de vídeo na tela “Assistir Vídeo”

**Dado** que eu esteja **logado** no sistema

**E** que eu esteja na tela “**Assistir Vídeo**”

**Quando** eu clicar no botão “**Play**”

**Então** o vídeo referente ao pedido deve ser reproduzido

 -------------------------------------------

**Cenário:** Acessar tela “Avaliar Pedido”

**Dado** que eu esteja **logado** no sistema

**E** que eu esteja na tela “**Assistir Vídeo**”

**Quando** eu clicar no botão “**Enviar Avaliação**”

**Então** devo ser **direcionado** à tela “**Avaliar Vídeo**”

 -------------------------------------------

**Cenário:** Download de pedido concluído via tela “Assistir Vídeo”

**Dado** que eu esteja **logado** no sistema

**E** que eu esteja na tela “**Assistir Vídeo**”

**Quando** eu clicar no botão “**Baixar**”

**Então** o **download** da mídia referente ao meu pedido deve disparado

 -------------------------------------------

**Cenário:** Compartilhar vídeo via tela “Assistir Vídeo”

**Dado** que eu esteja **logado** no sistema

**E** que eu esteja na tela “**Assistir Vídeo**”

**Quando** eu clicar no botão “**Compartilhar**”

**Então** o diálogo flutuante com as opções de compartilhamento deverá ser exibido

 -------------------------------------------

**Cenário:** Reportar vídeo via tela “Assistir Vídeo” - Confirmado

**Dado** que eu esteja **logado** no sistema

**E** que eu esteja na tela “**Assistir Vídeo**”

**Quando** eu clicar no botão “**Reportar**”

E eu **confirmar** na mensagem de confirmação

**Então** devo ser direcionado para a tela de “Reportar Criador”

 -------------------------------------------

**Cenário:** Acessar perfil do Criador via tela “Assistir Vídeo” - Foto

**Dado** que eu esteja **logado** no sistema

**E** que eu esteja na tela “**Assistir Vídeo**”

**Quando** eu clicar na foto de **perfil do criador**

**Então** devo ser **direcionado** para a página de perfil do criador

 -------------------------------------------

**Cenário:** Acessar perfil do Criador via tela “Assistir Vídeo” - Nome

**Dado** que eu esteja **logado** no sistema

**E** que eu esteja na tela “**Assistir Vídeo**”

**Quando** eu clicar no nome de **perfil do criador**

**Então** devo ser **direcionado** para a página de perfil do criador

 -------------------------------------------

**Cenário:** Voltar para perfil do usuário fã via tela “Assistir Vídeo”

**Dado** que eu esteja **logado** no sistema

**E** que eu esteja na tela “**Assistir Vídeo**”

**Quando** eu clicar no botão “Voltar”

**Então** devo ser **direcionado** para minha página de perfil de usuário fã

 -------------------------------------------

**Cenário:** Avaliação de Pedido bem-sucedida

**Dado** que eu esteja **logado** no sistema

**E** que eu esteja na tela “**Avaliar Vídeo**”

**E** que tenha atribuído **nota** para o pedido

**E** que tenha **selecionado** uma **opção de privacidade**

**E** que o campo **comentário** contenha **menos de 501 caracteres**

**Quando** eu clicar no botão “**Enviar Avaliação**”

E eu **confirmar** o envio na mensagem de confirmação

**Então** a avaliação do pedido deve ser registrada

 -------------------------------------------

**Cenário:** Avaliação de Pedido cancelada

**Dado** que eu esteja **logado** no sistema

**E** que eu esteja na tela “**Avaliar Vídeo**”

**E** que **tenha** atribuído **nota** para o pedido

**E** que tenha **selecionado** uma **opção de privacidade**

**E** que o campo comentário contenha **menos de 501 caracteres**

**Quando** eu clicar no botão “**Enviar Avaliação**”

E eu **cancelar** o envio na mensagem de confirmação

**Então** uma mensagem de **cancelamento** deve ser exibida

 -------------------------------------------

**Cenário:** Avaliação de Pedido sem atribuição de nota

**Dado** que eu esteja **logado** no sistema

**E** que eu esteja na tela “**Avaliar Vídeo**”

**E** que **não** **tenha** atribuído **nota** para o pedido

**E** que tenha **selecionado** uma **opção de privacidade**

**E** que o campo comentário contenha **menos de 501 caracteres**

**Quando** eu clicar no botão “**Enviar Avaliação**”

**Então** uma mensagem de **erro** informando a obrigatoriedade de atribuição de nota deve ser exibida

 -------------------------------------------

**Cenário:** Avaliação de Pedido com comentário muito longo

**Dado** que eu esteja **logado** no sistema

**E** que eu esteja na tela “**Avaliar Vídeo**”

**E** que **tenha** atribuído **nota** para o pedido

**E** que tenha **selecionado** uma **opção de privacidade**

**E** que o campo comentário contenha **mais de 500 caracteres**

**Quando** eu clicar no botão “**Enviar Avaliação**”

**Então** uma mensagem de **erro** informando que o comentário deve ter até 500 caracteres

 -------------------------------------------

**Cenário:** Envio de Mimo via tela "Avaliar Vídeo"

**Dado** que eu esteja **logado** no sistema

**E** que eu esteja na tela “**Avaliar Vídeo**”

**Quando** eu clicar no botão “**Enviar Mimo**”

**Então** devo ser **direcionado** para a tela de envio de mimo

 -------------------------------------------

**Cenário:** Voltar para tela “Assistir Vídeo” via tela “Avaliar Vídeo”

**Dado** que eu esteja **logado** no sistema

**E** que eu esteja na tela “**Avaliar Vídeo**”

**Quando** eu clicar no botão “Voltar”

**Então** devo ser **direcionado** a tela “**Assistir Vídeo**”

 -------------------------------------------

**Cenário:** Acessar perfil do Criador via tela “Avaliar Vídeo” - Foto

**Dado** que eu esteja **logado** no sistema

**E** que eu esteja na tela “**Avaliar Vídeo**”

**Quando** eu clicar na foto de **perfil do criador**

**Então** devo ser **direcionado** para a página de perfil do criador

 -------------------------------------------

**Cenário:** Acessar perfil do Criador via tela “Avaliar Vídeo” - Nome

**Dado** que eu esteja **logado** no sistema

**E** que eu esteja na tela “**Avaliar Vídeo**”

**Quando** eu clicar no nome de **perfil do criador**

**Então** devo ser **direcionado** para a página de perfil do criador

 -------------------------------------------

**Cenário:** Reprodução de vídeo na tela “Avaliar Vídeo”

**Dado** que eu esteja **logado** no sistema

**E** que eu esteja na tela “**Avaliar Vídeo**”

**Quando** eu clicar no botão “**Play**” na miniatura do vídeo

**Então** o vídeo referente ao pedido deve ser reproduzido

 -------------------------------------------