
# BDD Sessão

<u>**Funcionalidade: Obter e manter tokens de sessão**</u>

Como um usuário

Eu quero poder realizar login

E ter uma sessão ativa no sistema

E ser identificado quando estiver logado

**Cenário:** Início de sessão

**Dado** que um usuário realize login no sistema

**E** que suas credenciais estejam corretas

**Quando** eu realizar login

**Então** devo receber um token de refresh e acesso  
  
**E** meu token de acesso deve ser armazenado em memória

**E** meu token de refresh deve ser armazenado como cookie httpOnly

**E** meu token de refresh deve ter os atributos **Secure** e **Domain** apontando para o backend

**E** devo conseguir acessar o sistema normalmente

**Cenário:** Renovação de sessão - Token de acesso expirou

**Dado** que estou logado no sistema

**E** que meu token refresh seja válido

**E** que meu token de acesso tenha expirado

**Quando** eu realizar uma requisição

**Então** devo receber um erro **401 - Unauthorized**

**E** devo solicitar um novo token de acesso, por meio do meu token de refresh

**E** o novo token de acesso deve ser usado para realizar a request original novamente

**Cenário:** Logout

**Dado** que estou logado no sistema

**Quando** eu clicar em "Deslogar"

**Então** devo retornar à página de login

**E** meu token de acesso e refresh devem ser desativados

**E** meu token de acesso e refresh devem ser removidos do meu storage

