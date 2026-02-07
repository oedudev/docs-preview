
# BDD Menu superior de navegação

**Funcionalidade:** Menu Superior

 Como um usuário do site  
 Desejo ter um menu de navegação claro e funcional em todas as páginas  
 Para que eu possa acessar facilmente as seções principais do site.

 **Regra:** O menu superior deve estar presente em todas as páginas públicas e conter os mesmos elementos de navegação.

 **Cenário:** Visualização completa do menu na página inicial

 **Dado** que eu seja um usuário na página inicial  
 **Quando** eu olhar a porção superior da página  
 **Então** eu devo visualizar um menu de navegação  
  **E** o menu deve conter links para as diferentes sessões do site  
  **E** o menu deve conter um link para abetura do diálogo de login/criação de conta

 **Cenário:** Navegar para uma tela a partir de um link do menu

 **Dado** que eu estou em uma página pública  
 **Quando** eu clicar em um link no menu superior  
  **Então** eu devo ser direcionado para a página relacionada ao link escolhido

  **Cenário:** Exibir Diálogo de Login

  **Dado** que eu estou em uma página pública  
 **E** não estou logado na plataforma  
  **Quando** eu clicar no link de login no menu superior  
  **Então** devo visualizar um diálogo que me permita realizar o login