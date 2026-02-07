
# BDD App Aluno

##### **Funcionalidade:** Login no Sistema

 Como um aluno

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

 **Quando** o usuário confirma sua presença na aula

 **Então** a presença do usuário deve ser confirmada na aula

 **Cenário:** Não Confirmar Presença na Aula

 **Dado** que o usuário está o está visualizando a descrição de uma aula

 **Quando** o usuário não confirma sua presença na aula

 **Então** a presença do usuário não deve ser confirmada na aula

 **Cenário:** Cancelar Presença na Aula

 **Dado** que o usuário está visualizando a descrição de uma aula

 **Quando** o usuário opta por cancelar sua presença na aula

 **Então** a presença do usuário deve ser removida da aula

 **E** o usuário deve receber uma confirmação de que o cancelamento foi bem-sucedido

##### **Funcionalidade:** Visualização da Evolução das Faixas

Como um usuário autenticado

Eu quero visualizar a evolução das minhas faixas

Para que eu possa acessar e revisar a linha do tempo do meu progresso

 **Cenário:** Visualizar Evolução das Faixas

 **Dado** que o usuário está na seção de Configurações

 **Quando** o usuário acessa sua evolução de faixas

  **Então** o usuário deve ver o histórico e progresso das suas faixas

 **Cenário:** Acessar e Visualizar Linha do Tempo da Evolução das Faixas

 **Dado** que o usuário está na seção de visualização de faixas

 **Quando** o usuário visualiza a linha do tempo da sua evolução

 **Então** o usuário deve ver o histórico detalhado das faixas que conquistou

##### **Funcionalidade:** Visualização dos Termos

Como um usuário autenticado

Eu quero visualizar os termos e condições

Para que eu possa revisar as políticas e regulamentos associados ao uso do sistema

 **Cenário:** Visualizar Termos

 **Dado** que o usuário está na seção de Configurações

 **E** o usuário acessa a opção para visualizar os termos

 **Quando** o usuário lê os termos

 **Então** o usuário deve ter acesso completo aos termos e condições

##### **Funcionalidade:** Recebimento de Credenciais de Login por E-mail

 Como um aluno

 Eu quero receber minhas credenciais de login por e-mail

 Para que eu possa acessar o sistema e utilizar os serviços disponíveis

 **Cenário:** Aluno recebe e-mail com credenciais de login após o cadastro

 **Dado** que o aluno foi cadastrado no sistema pelo instrutor

 **Quando** o sistema envia o e-mail de credenciais de login para o aluno

 **Então** o aluno deve receber o e-mail contendo seu nome de usuário e senha temporária

 **E** o e-mail deve fornecer instruções sobre como acessar o sistema e alterar a senha

