
# BDD Tela: Resultados Gerais

**Funcionalidade**: Página de Resultados

 **Cenário**: Visualização do conteúdo da página de Resultados 

 **Dado** que eu seja um usuário   
 **Quando** eu acessar a página de Resultados   
 **Então** devo visualizar o título da página "Resultados"   
 **E** devo visualizar links para "Resultados - Hospitais Parceiros"   
 **E** devo visualizar links para "Resultados - Parceiros de Produção"

  
 **Cenário**: Visualização da estrutura da página de Resultados 

 **Dado** que eu seja um usuário   
 **Quando** eu acessar a página de Resultados   
 **Então** devo visualizar uma seção de cabeçalho   
 **E** devo visualizar o menu superior de navegação   
 **E** devo visualizar o rodapé da página   
 **E** a página deve estar responsiva para diferentes dispositivos

 **Esquema do Cenário**: Navegar para dashboards específicos 

 **Dado** que eu seja um usuário na página de Resultados   
 **Quando** eu clicar no link "&lt;Dashboard&gt;"   
 **Então** devo ser direcionado para a página "&lt;Destino&gt;"

 **Exemplos**: 

 | Dashboard | Destino | \}  
 | Resultados - Hospitais Parceiros | Resultados - Hospitais Parceiros |  
 | Resultados - Parceiros de Produção| Resultados - Parceiros de Produção|