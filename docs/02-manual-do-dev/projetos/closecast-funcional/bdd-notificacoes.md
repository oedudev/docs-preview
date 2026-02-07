
# BDD Notificações

**Bloco 1: Perspectiva do Usuário Fã – Notificações**

**Cenário:** Acessar tela de notificações

**Dado** que eu esteja logado no sistema como um Usuário Fã

**Quando** eu clicar no ícone do “sino”

**Então** devo ser direcionado para a tela “Notificações”

**E** a aba “Todas” deve estar selecionada por padrão

**--------------------------------------**

**Cenário:** Consulta de todas as notificações do Usuário Fã – com notificações

**Dado** que eu esteja logado no sistema como um Usuário Fã

**E** que eu tenha recebido ao menos uma notificação de atividades

**Quando** eu acessar a tela de "Notificações"

**Então** devo visualizar a lista com todas as minhas notificações

**--------------------------------------**

**Cenário:** Consulta de todas as notificações do Usuário Fã – sem notificações

**Dado** que eu esteja logado no sistema como um Usuário Fã

**E** que eu não tenha recebido nenhuma notificação de atividades

**Quando** eu acessar a tela de "Notificações"

**Então** devo visualizar o campo de lista com a mensagem “Não há notificações”

**--------------------------------------**

**Cenário:** Filtro de notificações não lidas – com notificações não lidas

**Dado** que eu esteja logado no sistema como um Usuário Fã

**E** que eu esteja na tela de "Notificações"

**E** que eu tenha ao menos uma notificação não lida

**Quando** eu selecionar a aba "Não Lidas"

**Então** a lista deve exibir apenas as notificações cujo status é “não lida”

\--------------------------------------

**Cenário:** Filtro de notificações não lidas – sem notificações não lidas

**Dado** que eu esteja logado no sistema como um Usuário Fã

**E** que eu esteja na tela de "Notificações"

**E** que eu não tenha notificações não lidas

**Quando** eu selecionar a aba "Não Lidas"

**Então** devo visualizar o campo de lista com a mensagem “Não há notificações”

\--------------------------------------

**Cenário:** Visualizar notificação - genérico

**Dado** que eu esteja logado no sistema como um Usuário Fã

**E** que eu esteja na tela de "Notificações" na aba “Todos” ou “Não lida”

**E** que eu tenha ao menos uma notificação

**Quando** no botão “Visualizar” de uma notificação deste tipo

**Então** devo ser direcionado para a página com os detalhes da notificação

\--------------------------------------

**Cenário:** Visualizar notificação não lida

**Dado** que eu esteja logado no sistema como um Usuário Fã

**E** que eu esteja na tela de "Notificações" com a aba "Não Lidas" selecionada

**E** que eu tenha ao menos uma notificação não lida na lista

**Quando** eu clicar para visualizar o conteúdo desta notificação

**E** retornar para a tela de "Notificações"

**Então** devo ser direcionado para a tela apropriada para o tipo de notificação

**E** o status da notificação deve ser alterado para “lida”

\--------------------------------------

**Cenário:** Acesso à tela de recebimento de vídeo via notificação

**Dado** que eu esteja logado no sistema como um Usuário Fã

**E** que eu esteja na tela de "Notificações"

**E** que eu tenha uma notificação do tipo "Seu vídeo está pronto!"

**Quando** eu clicar no botão "Visualizar" da notificação correspondente

**Então** devo ser direcionado para a tela de "Assistir Vídeo"

\--------------------------------------

**Cenário:** Filtro de notificações: pagamentos – com notificações

**Dado** que eu esteja logado no sistema como um Usuário Fã

**E** que eu esteja na tela de "Notificações"

**E** eu tenha ao menos uma notificação relacionada a pagamentos

**Quando** eu selecionar a aba "Pagamentos"

**Então** a lista deve exibir apenas as notificações relacionadas a pagamentos

\--------------------------------------

**Cenário:** Filtro de notificações: pagamentos – com notificações

**Dado** que eu esteja logado no sistema como um Usuário Fã

**E** que eu esteja na tela de "Notificações"

**E** eu não tenha notificações relacionadas a pagamentos

**Quando** eu selecionar a aba "Pagamentos"

**Então** devo visualizar o campo de lista com a mensagem “Não há notificações”

**Bloco 2: Perspectiva do Usuário Fã - Fluxo de Recebimento e Avaliação**

**Cenário:** Visualização de vídeo recebido

**Dado** que eu esteja logado no sistema como um Usuário Fã

**E** que eu tenha recebido um vídeo de um Usuário Criador

**E** que eu esteja na tela "Assistir Vídeo"

**Quando** eu clicar no botão "Play"

**Então** o vídeo recebido deve ser reproduzido

\--------------------------------------

**Cenário:** Aprovação de vídeo recebido

**Dado** que eu esteja logado no sistema como um Usuário Fã

**E** que eu tenha recebido um vídeo de um Usuário Criador

**E** que eu esteja na tela "Assistir Vídeo"

**Quando** eu clicar no botão "Avaliar e Aprovar"

**Então** devo ser direcionado para a tela de avaliação do pedido

\--------------------------------------

**Cenário:** Criar solicitação de alteração

**Dado** que eu esteja logado no sistema como um Usuário Fã

**E** que eu tenha recebido um vídeo de um Usuário Criador

**E** que eu esteja na tela "Assistir Vídeo"

**Quando** eu clicar no botão "Solicitar Alteração"

**Então** devo ser direcionado para a tela “Solicitar Alteração”

\--------------------------------------

**Cenário:** Envio de solicitação de alteração com sucesso

**Dado** que eu esteja logado no sistema como um Usuário Fã

**E** que eu esteja na tela "Solicitar Alteração"

**Quando** eu preencher o campo de descrição com um texto sobre a alteração desejada contendo entre 10 e 500 caracteres\*

**E** clicar no botão "Enviar Avaliação"

**Então** a solicitação de alteração deve ser enviada para o Usuário Criador

**E** devo receber uma mensagem de confirmação do envio

\--------------------------------------

**Cenário:** Tentativa de enviar solicitação de alteração com campo de descrição vazio

 **Dado** que eu esteja logado no sistema como um Usuário Fã

**E** que eu esteja na tela "Solicitar Alteração"

**E** que o campo de descrição da alteração esteja vazio

**Quando** eu clicar no botão "Enviar Avaliação"

**Então** devo visualizar uma mensagem de erro indicando que a descrição é obrigatória

\--------------------------------------

**Cenário:** Tentativa de enviar solicitação de alteração excedendo o limite de caracteres

**Dado** que eu esteja logado no sistema como um Usuário Fã

**E** que eu esteja na tela "Solicitar Alteração"

**Quando** eu preencher o campo de descrição com um texto maior que 500 caracteres

**Então** devo visualizar um alerta sobre o limite de caracteres

\--------------------------------------

**Cenário:** Cancelamento da solicitação de alteração

**Dado** que eu esteja logado no sistema como um Usuário Fã

**E** que eu esteja na tela "Solicitar Alteração"

**Quando** eu clicar no botão "Voltar"

**Então** devo ser redirecionado de volta para a tela "Assistir Vídeo"

**Bloco 3: Perspectiva do Usuário Criador – Notificações**

**Cenário:** Acessar tela de notificações

**Dado** que eu esteja logado no sistema como um Usuário Criador

**Quando** eu clicar no ícone do “sino”

**Então** devo ser direcionado para a tela “Central do Criador”

**E** a aba "Todas" deve estar selecionada por padrão

**--------------------------------------**

**Cenário:** Consulta de todas as notificações do Usuário Criador – com notificações

**Dado** que eu esteja logado no sistema como um Usuário Criador

**E** eu esteja na tela de "Central do Criador"

**E** que eu tenha recebido ao menos uma notificação de atividades

**Quando** eu selecionar a aba "Todas"

**Então** devo visualizar a lista com todas as minhas notificações

**--------------------------------------**

**Cenário:** Consulta de todas as notificações do Criador – sem notificações

**Dado** que eu esteja logado no sistema como um Usuário Criador

**E** eu esteja na tela de "Central do Criador"

**E** que eu tenha recebido ao menos uma notificação de atividades

**Quando** eu selecionar a aba "Todas"

**Então** devo visualizar o campo de lista com a mensagem “Não há notificações”

**--------------------------------------**

**Cenário:** Filtro de notificações não lidas – com notificações não lidas

**Dado** que eu esteja logado no sistema como um Usuário Criador

**E** que eu esteja na tela de "Central do Criador"

**E** que eu tenha ao menos uma notificação não lida

**Quando** eu selecionar a aba "Não Lidas"

**Então** a lista deve exibir apenas as notificações cujo status é “não lida”

\--------------------------------------

**Cenário:** Filtro de notificações não lidas – sem notificações não lidas

**Dado** que eu esteja logado no sistema como um Usuário Criador

**E** que eu esteja na tela de "Notificações"

**E** que eu não tenha notificações não lidas

**Quando** eu selecionar a aba "Não Lidas"

**Então** devo visualizar o campo de lista com a mensagem “Não há notificações”

\--------------------------------------

**Cenário:** Visualizar notificação não lida

**Dado** que eu esteja logado no sistema como um Usuário Criador

**E** que eu esteja na tela de "Notificações" com a aba "Não Lidas" selecionada

**E** que eu tenha ao menos uma notificação não lida na lista

**Quando** eu clicar para visualizar o conteúdo desta notificação

**E** retornar para a tela de "Central do Criador"

**Então** devo ser direcionado para a tela apropriada para o tipo de notificação

**E** o status da notificação deve ser alterado para “lida”

\--------------------------------------

**Cenário:** Filtro de notificações propostas – com notificações

**Dado** que eu esteja logado no sistema como um Usuário Criador

**E** que eu esteja na tela de "Central do Criador"

**E** que eu tenha ao menos uma do tipo “Notificação de Proposta”

**Quando** eu selecionar a aba "Propostas"

**Então** a lista deve exibir apenas as notificações cujo tipo é “Notificação de Proposta”

\--------------------------------------

**Cenário:** Filtro de notificações propostas – sem notificações

**Dado** que eu esteja logado no sistema como um Usuário Criador

**E** que eu esteja na tela de "Central do Criador"

**E** que eu não tenha notificações do tipo “Notificação de Proposta”

**Quando** eu selecionar a aba "Propostas"

**Então** devo visualizar o campo de lista com a mensagem “Não há notificações”

\--------------------------------------

**Cenário:** Filtro de notificações: pagamentos – com notificações

**Dado** que eu esteja logado no sistema como um Usuário Criador

**E** que eu esteja na tela de "Central do Criador"

**E** eu tenha ao menos uma notificação relacionada a pagamentos

**Quando** eu selecionar a aba "Pagamentos"

**Então** a lista deve exibir apenas as notificações relacionadas a pagamentos

\--------------------------------------

**Cenário:** Filtro de notificações: pagamentos – sem notificações

**Dado** que eu esteja logado no sistema como um Usuário Criador

**E** que eu esteja na tela de "Central do Criador"

**E** eu não tenha notificações relacionadas a pagamentos

**Quando** eu selecionar a aba "Pagamentos"

**Então** devo visualizar o campo de lista com a mensagem “Não há notificações”

\--------------------------------------

**Cenário:** Acesso à tela de Solicitação de Alteração via notificação

**Dado** que eu esteja logado no sistema como um Usuário Criador

**E** que eu esteja na tela de "Central do Criador"

**E** que eu tenha uma notificação do tipo "Solicitação de Alteração”

**Quando** eu clicar no botão "Visualizar" da notificação correspondente

**Então** devo ser direcionado para a tela “Resposta à Solicitação de Alteração”

\--------------------------------------

**Cenário:** Acesso à tela de Minhas Propostas via notificação

**Dado** que eu esteja logado no sistema como um Usuário Criador

**E** que eu esteja na tela de "Central do Criador"

**E** que eu tenha uma notificação do tipo "Notificação de Proposta”

**Quando** eu clicar no botão "Visualizar" da notificação correspondente

**Então** devo ser direcionado para a tela “Minhas Propostas”

**Bloco 4: Perspectiva do Usuário Criador - Fluxo de Resposta à Solicitação de Alteração**

**Cenário:** Aceitação de uma solicitação de alteração

**Dado** que eu esteja logado no sistema como um Usuário Criador

**E** que eu tenha recebido uma solicitação de alteração de um Usuário Fã

**E** que eu esteja na tela "Resposta à Solicitação de Alteração"

**Quando** eu selecionar a opção "Concordo com a alteração"

**E** clicar no botão "Confirmar Escolha"

**Então** a minha concordância deve ser registrada no sistema

**E** o status do pedido deve ser atualizado para "Em alteração"

\--------------------------------------

**Cenário:** Recusa de uma solicitação de alteração com justificativa

**Dado** que eu esteja logado no sistema como um Usuário Criador

**E** que eu esteja na tela "Resposta à Solicitação de Alteração"

**Quando** eu selecionar a opção "Discordo da alteração"

**E** preencher o campo de justificativa com o motivo da recusa

**E** clicar no botão "Confirmar Escolha"

**Então** a minha recusa e justificativa devem ser registradas no sistema

**E** o Usuário Fã deve ser notificado da decisão\*

\--------------------------------------

**Cenário:** Tentativa de recusar uma alteração sem justificativa

**Dado** que eu esteja logado no sistema como um Usuário Criador

**E** que eu esteja na tela "Resposta à Solicitação de Alteração"

**Quando** eu selecionar a opção "Discordo da alteração"

**E** clicar no botão "Confirmar Escolha" sem preencher a justificativa

**Então** devo visualizar uma mensagem de erro indicando que a justificativa é obrigatória

\--------------------------------------

**Cenário:** Tentativa de confirmar resposta sem selecionar uma opção

**Dado** que eu esteja logado no sistema como um Usuário Criador

**E** que eu esteja na tela "Resposta à Solicitação de Alteração"

**E** que nenhuma opção ("Concordo" ou "Discordo") esteja selecionada

**Quando** eu clicar no botão "Confirmar Escolha"

**Então** devo visualizar uma mensagem de erro solicitando a seleção de uma opção

\--------------------------------------