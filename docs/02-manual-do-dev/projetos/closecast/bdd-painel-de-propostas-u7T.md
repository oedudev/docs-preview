
# BDD Painel de Propostas

**Bloco 1: Navegação e Consulta de Propostas**

**Cenário:** Voltar

**Dado** que eu esteja logado no sistema como usuário Criador

**E** que eu esteja na tela "Minhas Propostas"

**Quando** eu clicar no botão “Voltar”

**Então** devo ser direcionado à página anterior

\---------------------------------

**Cenário:** Consulta de propostas pendentes

**Dado** que eu esteja logado no sistema como usuário Criador

**E** eu esteja na tela "Minhas Propostas"

**Q**uando eu clicar na aba “Pendentes”

**Então** deve ser exibida a lista de propostas cujo status é “Pendente”

\---------------------------------

**Cenário:** Consulta de propostas em produção

**Dado** que eu esteja logado no sistema como usuário Criador

**E** eu esteja na tela "Minhas Propostas"

**Quando** eu clicar na aba “Em produção”

**Então** deve ser exibida a lista de propostas cujo status é “Em Produção”

\---------------------------------

**Cenário:** Consulta de propostas concluídas

**Dado** que eu esteja logado no sistema como usuário Criador

**E** eu esteja na tela "Minhas Propostas"

**Quando** eu clicar na aba “Concluídos”

**Então** deve ser exibida a lista de propostas cujo status é “Concluído”

\---------------------------------

**Cenário:** Consulta de todas as propostas

**Dado** que eu esteja logado no sistema como usuário Criador

**E** eu esteja na tela "Minhas Propostas"

**Quando** eu clicar na aba “Todos”

**Então** deve ser exibida a lista de todas as propostas

**Bloco 3: Gerenciamento de Mídia (Propostas em Produção)**

**Cenário:** Upload de mídia de entrega – Clique botão + Arquivo válido

**Dado** que eu esteja logado no sistema como usuário Criador

**E** eu esteja na tela "Minhas Propostas"

**E** eu esteja com a aba “Em produção” selecionada

**E** eu tenha ao menos uma proposta em produção

**Quando** eu clicar no botão “Selecionar Arquivo” de uma das propostas

**E** selecionar um arquivo de mídia válido

**Então** deverá ser disparado o upload do arquivo de mídia de entrega

\---------------------------------

**Cenário:** Upload de mídia de entrega – Clique botão + Arquivo inválido

**Dado** que eu esteja logado no sistema como usuário Criador

**E** eu esteja na tela "Minhas Propostas"

**E** eu esteja com a aba “Em produção” selecionada

**E** eu tenha ao menos uma proposta em produção

**Quando** eu clicar no botão “Selecionar Arquivo” de uma das propostas

**E** selecionar um arquivo de mídia inválido

**Então** devo receber uma mensagem de erro informando tipos de arquivos aceitos

\---------------------------------

**Cenário:** Upload de mídia de entrega – Arrastar + Arquivo válido

**Dado** que eu esteja logado no sistema como usuário Criador

**E** eu esteja na tela "Minhas Propostas"

**E** eu esteja com a aba “Em produção” selecionada

**E** eu tenha ao menos uma proposta em produção

**Quando** eu arrastar um arquivo de mídia valido para a área delimitada de uma das propostas

**Então** deverá ser disparado o upload do arquivo de mídia de entrega

\---------------------------------

**Cenário:** Upload de mídia de entrega – Arrastar + Arquivo inválido

**Dado** que eu esteja logado no sistema como usuário Criador

**E** eu esteja na tela "Minhas Propostas"

**E** eu esteja com a aba “Em produção” selecionada

**E** eu tenha ao menos uma proposta em produção

**Quando** eu arrastar um arquivo de mídia invalido para a área delimitada de uma das propostas

**Então** devo receber uma mensagem de erro informando tipos de arquivos aceitos

\---------------------------------

**Cenário:** Exclusão de mídia de entrega – confirmado

**Dado** que eu esteja logado no sistema como usuário Criador

**E** eu esteja na tela "Minhas Propostas"

**E** eu esteja com a aba “Em produção” selecionada

**E** tenha ao menos uma proposta em produção

**E** eu tenha ao menos um arquivo de mídia enviado para a proposta

**Quando** eu clicar no botão “lixeira” de uma das mídias enviadas

**E** clicar em “Sim” na mensagem de confirmação de exclusão de mídia

**Então** a mídia deverá ser excluída

**E** devo receber uma mensagem de confirmação da exclusão da mídia

\---------------------------------

**Cenário:** Exclusão de mídia de entrega – cancelado

**Dado** que eu esteja logado no sistema como usuário Criador

**E** eu esteja na tela "Minhas Propostas"

**E** eu esteja com a aba “Em produção” selecionada

**E** eu tenha ao menos uma proposta em produção

**E** eu tenha ao menos um arquivo de mídia enviado para a proposta

**Quando** eu clicar no ícone “lixeira” de uma das mídias enviadas

**E** clicar em “Não” na mensagem de confirmação de exclusão de mídia

**Então** não devo receber mensagem de erro

\---------------------------------

**Cenário:** Visualização de mídia

**Dado** que eu esteja logado no sistema como usuário Criador

**E** eu esteja na tela "Minhas Propostas"

**E** eu esteja com a aba “Em produção” selecionada

**E** eu tenha ao menos uma proposta em produção

**E** eu tenha ao menos um arquivo de mídia enviado para a proposta

**Quando** eu clicar no ícone “olho” de uma das mídias enviadas

**Então** a mídia deve ser exibida em um diálogo flutuante

**Bloco 4: Ações em Propostas Concluídas**

**Cenário:** Denúncia de proposta concluída - confirmada

**Dado** que eu esteja logado no sistema como usuário Criador

**E** eu esteja na tela "Minhas Propostas"

**E** eu esteja com a aba “Concluídos” selecionada

**E** eu tenha ao menos uma proposta concluída

**E** eu clicar no botão “Denunciar” de uma das propostas

**E** clicar em “Sim” na mensagem de denúncia da proposta

**Então** o status da proposta aceita deve ser alterado para “Denunciada”

**E** ser direcionado para a página de denúncia

\---------------------------------

**Cenário:** Denúncia de proposta concluída - cancelada

**Dado** que eu esteja logado no sistema como usuário Criador

**E** eu esteja na tela "Minhas Propostas"

**E** eu esteja com a aba “Concluídos” selecionada

**E** eu tenha ao menos uma proposta concluída

**Quando** eu clicar no botão “Denunciar” de uma das propostas

**E** clicar em “Não” na mensagem de confirmação da denúncia da proposta

**Então** não devo receber erro

