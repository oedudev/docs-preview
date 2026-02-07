
# BDD Login

**Funcionalidade:** Login

Como um usuário da plataforma,   
Desejo realizar login,  
Para que eu possa acessar as funcionalidades reservadas a usuários logados.

 **Cenário**: Login bem sucedido 

 **Dado** que eu seja um usuário cadastrado na plataforma   
 **E** que não esteja logado   
 **Quando** eu fornecer meu e-mail cadastrado   
 **E** fornecer minha senha correta   
 **Então** eu devo ser logado na plataforma  
 **E** meu acesso às funcionalidades reservadas a usuários logados deve ser habilitado

 **Cenário:** Tentativa de login com e-mail em branco

 **Dado** que eu seja um usuário  
 **E** que não esteja logado na plataforma  
 **Quando** eu realizar uma tentativa de login  
 **E** não forneça e-mail  
 **Então** devo receber a mensagem de "É necessário informar o usuário"  
 **E** meu Login não deve ser realizado

 **Cenário:** Tentativa de login com e-mail não cadastrado

 **Dado** que eu seja um usuário  
 **E** que não esteja logado na plataforma  
 **Quando** eu realizar uma tentativa de login  
 **E** fornecer um e-mail não cadastrado  
 **Então** devo receber a mensagem de "Usuário e/ou senha inválidos"  
 **E** meu Login não deve ser realizado

 **Cenário:** Tentativa de login com formato de e-mail inválido

 **Dado** que eu seja um usuário  
 **E** que não esteja logado na plataforma  
 **Quando** eu realizar uma tentativa de login  
 **E** fornecer um e-mail com formato inválido  
 **Então** devo receber a mensagem de "O e-mail informado não tem formato válido"  
 **E** meu Login não deve ser realizado

 **Cenário:** Tentativa de login com e-mail de domínio não parceiro

 **Dado** que eu seja um usuário  
 **E** que não esteja logado na plataforma  
 **Quando** eu realizar uma tentativa de login  
 **E** fornecer um e-mail com domínio de uma instituição não parceira  
 **Então** devo receber a mensagem de "Domínio do e-mail fornecido não é de uma de instituição parceira"  
 **E** meu Login não deve ser realizado

 **Cenário:** Tentativa de login com senha em branco

 **Dado** que eu seja um usuário  
 **E** que não esteja logado na plataforma  
 **Quando** eu realizar uma tentativa de login  
 **E** não forneça senha  
 **Então** devo receber a mensagem de erro "É necessário fornecer a senha"  
 **E** meu Login não deve ser realizado

 **Cenário:** Tentativa de login com senha incorreta

 **Dado** que eu seja um usuário  
 **E** que não esteja logado na plataforma  
 **Quando** eu realizar uma tentativa de login  
 **E** fornecer uma senha incorreta para o usuário informado  
 **Então** devo receber a mensagem de "Usuário e/ou senha inválidos"  
 **E** meu Login não deve ser realizado

 **Cenário:** Tentativa de login para um usuário não cadastrado

 **Dado** que eu seja um usuário  
 **E** que não esteja logado na plataforma  
 **Quando** eu realizar uma tentativa de login  
 **E** não for um usuário cadastrado  
 **Então** devo receber a mensagem de "Usuário e/ou senha inválidos"  
 **E** meu Login não deve ser realizado