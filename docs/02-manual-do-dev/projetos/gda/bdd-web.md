
# BDD Web

##### **Funcionalidade:** Gerenciamento de Academias

 Como um administrador

 Eu quero adicionar novas academias

 Para que elas possam ser gerenciadas no sistema

 **Cenário:** Adicionar uma nova academia com sucesso

 **Dado** que o administrador tem os dados válidos da nova academia

 **Quando** o administrador adiciona a nova academia ao sistema

 **Então** a academia é registrada com sucesso

 **E** a nova academia é incluída na lista de academias cadastradas

 **Cenário:** Excluir uma academia existente

 **Dado** que o administrador deseja remover uma academia existente

 **Quando** o administrador solicita a exclusão da academia

 **Então** o sistema deve verificar a solicitação de remoção

 **E** o sistema deve remover a academia da lista de academias cadastradas

 **E** a exclusão é confirmada com sucesso

 **Cenário:** Editar os dados de uma academia existente

 **Dado** que o administrador deseja modificar os dados de uma academia existente

 **Quando** o administrador atualiza os dados da academia no sistema

 **Então** o sistema deve processar a atualização dos dados da academia

 **E** a academia é atualizada com sucesso no sistema

##### **Funcionalidade:** Gerenciamento de Alunos

 Como um administrador

 Eu quero adicionar novos alunos

 Para que eles possam acessar os recursos do sistema

 **Cenário:** Adicionar um novo aluno com sucesso

 **Dado** que o administrador possui os dados válidos do novo aluno

 **Quando** o administrador registra o aluno no sistema

 **Então** o aluno é registrado com sucesso

 **E** o novo aluno é incluído na lista de alunos cadastrados

 **Cenário:** Excluir um aluno existente

 **Dado** que o administrador deseja remover um aluno do sistema

 **Quando** o administrador solicita a exclusão do aluno

 **Então** o sistema deve solicitar a confirmação da exclusão

 **E** quando o administrador confirma a exclusão

 **Então** o aluno é removido do sistema com sucesso

 **E** o sistema confirma a exclusão com uma mensagem

 **Cenário**: Editar os dados de um aluno existente

 **Dado** que o administrador deseja modificar os dados de um aluno existente

 **Quando** o administrador atualiza as informações do aluno no sistema

 **Então** os dados do aluno são atualizados com sucesso

 **E** o sistema confirma a atualização com uma mensagem

##### **Funcionalidade:** Gerenciamento de Clientes

 Como um administrador

 Eu quero adicionar novos clientes

 Para que eles possam acessar os serviços oferecidos

 **Cenário:** Adicionar um novo cliente com sucesso

 **Dado** que o administrador possui os dados válidos do novo cliente

 **Quando** o administrador registra o cliente no sistema

 **Então** o cliente é registrado com sucesso

 **E** o novo cliente é incluído na lista de clientes cadastrados

 **Cenário:** Excluir um cliente existente

 **Dado** que o administrador deseja remover um cliente do sistema

 **Quando** o administrador solicita a exclusão do cliente

 **Então** o sistema deve solicitar a confirmação da exclusão

 **E** quando o administrador confirma a exclusão

 **Então** o cliente é removido do sistema com sucesso

 **E** o sistema confirma a exclusão com uma mensagem

 **Cenário:** Editar os dados de um cliente existente

 **Dado** que o administrador deseja modificar os dados de um cliente existente

 **Quando** o administrador atualiza as informações do cliente no sistema

 **Então** os dados do cliente são atualizados com sucesso

 **E** o sistema confirma a atualização com uma mensagem

##### **Funcionalidade:** Gerenciamento de Perfil

 Como um usuário

 Eu quero gerenciar meus dados pessoais e acessar os termos de uso

 Para que eu possa manter minhas informações atualizadas e estar ciente das políticas do sistema

 **Cenário:** Visualizar dados pessoais

 **Dado** que o usuário tem acesso ao gerenciamento de perfil

 **Quando** o usuário solicita a visualização de seus dados pessoais

 **Então** o sistema deve retornar os dados pessoais armazenados do usuário

 **Cenário:** Modificar dados pessoais

 **Dado** que o usuário está visualizando seus dados pessoais

 **Quando** o usuário altera alguma informação pessoal

 **Então** o sistema deve detectar as alterações

 **E** permitir que as mudanças sejam salvas

 **Cenário:** Nenhuma mudança nos dados pessoais

 **Dado** que o usuário está visualizando seus dados pessoais

 **Quando** o usuário não faz nenhuma alteração

 **Então** o sistema não deve permitir a solicitação de salvamento de dados

 **E** as informações devem permanecer inalteradas

 **Cenário:** Visualizar termos de uso

 **Dado** que o usuário tem acesso ao gerenciamento de perfil

 **Quando** o usuário solicita a visualização dos termos de uso

 **Então** o sistema deve fornecer os termos de uso atualizados

 **Cenário:** Encerrar sessão

 **Dado** que o usuário está autenticado no sistema

 **Quando** o usuário solicita o encerramento da sessão

 **Então** o sistema deve encerrar a sessão do usuário

