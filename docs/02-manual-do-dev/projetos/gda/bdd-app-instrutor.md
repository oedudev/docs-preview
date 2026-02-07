
# BDD App Instrutor

##### **Funcionalidade:** Login no Sistema

 Como um instrutor

 Eu quero fazer login no aplicativo

 Para que eu possa acessar o aplicativo

 **Cenário:** Login com credenciais válidas

  **Dado** que o usuário está na página de login

  **E** ele insere um nome de usuário e senha válidos

  **Quando** o usuário realiza o login

  **Então** ele é autenticado com sucesso

  **E** é redirecionado para a home screen

 **Cenário:** Login com credenciais inválidas

  **Dado** que o usuário está na página de login

  **E** ele insere um nome de usuário ou senha inválidos

  **Quando** o usuário realiza o login

  **Então** ele vê uma mensagem de erro informando que as credenciais estão incorretas

 **Cenário:** Tentativa de login com campos em branco

  **Dado** que o usuário está na página de login

  **E** ele não preenche o nome de usuário ou a senha

  **Quando** o usuário realiza o login

  **Então** ele vê uma mensagem de alerta pedindo para preencher todos os campos obrigatórios

 **Cenário:** Recuperação de senha

  **Dado** que o usuário está na página de login

  **E** esqueceu sua senha

  **Quando** o usuário seleciona o opção esqueci minha senha

  **Então** ele é redirecionado para a página de recuperação de senha

  **E** pode solicitar um e-mail de redefinição de senha

##### **Funcionalidade:** Acessar Alunos

 Como um instrutor autenticado

 Eu quero acessar os dados dos alunos

 Para que eu possa gerencia-los

 **Cenário:** O instrutor acessa a lista de alunos cadastrados

 **Dado** que o instrutor está logado no sistema

 **Quando** acessa a seção de alunos

 **Então** o sistema exibe a lista de alunos cadastrados

 **Cenário:** O instrutor visualiza a timeline de evolução de um aluno

 **Dado** que o instrutor está na lista de alunos cadastrados

 **Quando** seleciona um aluno específico

 **Então** o sistema exibe a timeline com a evolução do aluno, incluindo mudanças de faixa, grau, e outros marcos importantes

 **Cenário:** O instrutor cadastra um novo aluno no sistema

 **Dado** que o instrutor está na seção de alunos

 **Quando** seleciona a opção de cadastrar novo aluno

 **Então** o sistema abre o formulário de cadastro do aluno

 **E** o instrutor preenche os dados necessários, incluindo a seleção da faixa e grau do aluno

 **Quando** o cadastro é submetido

 **Então** o sistema registra o novo aluno na lista de alunos cadastrados

 **Cenário:** O instrutor visualiza os dados de um aluno específico

 **Dado** que o instrutor está na lista de alunos cadastrados

 **Quando** seleciona um aluno específico

 **Então** o sistema exibe os dados do aluno, incluindo a faixa e o grau

  **E** o instrutor pode atualizar essas informações se necessário

 **Cenário:** O instrutor exclui o perfil de um aluno do sistema

 **Dado** que o instrutor está na lista de alunos cadastrados

 **Quando** seleciona um aluno para exclusão

  **Então** o sistema exibe uma confirmação de exclusão

 **E** ao confirmar, o sistema remove o perfil do aluno da lista de alunos cadastrados

##### **Funcionalidade:** Visualizar Perfil

 Como um instrutor autenticado

 Quero visualizar meu perfil 

 Para acessar minhas informações pessoais e realizar possíveis alterações

 **Cenário:** O usuário visualiza o seu perfil

 **Dado** que o usuário está logado no sistema

 **Quando** acessa a seção de perfil

 **Então** o sistema exibe as informações pessoais e opções de edição

##### **Funcionalidade:** Modificar Senha

 Como um instrutor autenticado

 Quero modificar minha senha 

 Para garantir a segurança da minha conta

 **Cenário:** O usuário modifica sua senha

 **Dado** que o usuário está na seção de perfil

 **E** deseja modificar sua senha por segurança

 **Quando** seleciona a opção de modificar senha

 **Então** o sistema permite que o usuário insira a nova senha e confirme a alteração

##### **Funcionalidade:** Sair do Sistema

 Como um instrutor autenticado

 Quero sair do sistema 

 Para encerrar minha sessão

 **Cenário:** O usuário sai do sistema

 **Dado** que o usuário está na seção de perfil

 **E** deseja encerrar sua sessão

 **Quando** seleciona a opção de sair do sistema

 **Então** o sistema encerra a sessão do usuário e o redireciona para a tela de login

