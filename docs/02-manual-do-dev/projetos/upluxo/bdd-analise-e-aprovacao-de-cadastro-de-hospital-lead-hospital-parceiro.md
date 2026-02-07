
# BDD Análise e Aprovação de Cadastro de Hospital Lead -> Hospital Parceiro

**Funcionalidade:** Análise e Aprovação de Cadastro de Hospital

Como um administrador do sistema  
Desejo analisar as informações e documentos submetidos por um Hospital Lead  
Para aprovar seu cadastro, convertendo-o em Hospital Parceiro, ou reprová-lo caso não atenda aos critérios.  
  
 **Cenário:** Aprovação bem-sucedida de um Hospital Lead

 **Dado** que eu seja um Administrador logado no sistema  
 **E** exista um "Hospital Lead" com o cadastro submetido e com status "Em Análise"  
 **E** que todas as informações e documentos do hospital estejam corretos e válidos  
 **Quando** eu acessar a lista de cadastros pendentes  
 **E** selecionar o cadastro do Hospital Lead para análise  
 **E** revisar os dados e a documentação  
 **E** clicar na opção "Aprovar Cadastro"  
 **Então** o status do hospital deve ser alterado de "Hospital Lead" para "Hospital Parceiro"  
 **E** o status do seu cadastro deve ser atualizado para "Aprovado"  
 **E** o hospital deve receber uma notificação (por e-mail, por exemplo) informando sobre a aprovação e a liberação de seu acesso  
 **E** a conta do hospital deve ter acesso completo às funcionalidades de um Hospital Parceiro.  
  
  
 **Cenário:** Reprovação de um Hospital Lead por documentação inválida  
  
 **Dado** que eu seja um Administrador logado no sistema  
 **E** exista um "Hospital Lead" com o cadastro submetido e com status "Em Análise"  
 **E** que a documentação fornecida pelo hospital seja inválida ou insuficiente  
 **Quando** eu acessar a lista de cadastros pendentes  
 **E** selecionar o cadastro do Hospital Lead para análise  
 **E** identificar a inconsistência nos documentos  
 **E** clicar na opção "Reprovar Cadastro"  
 **E** eu preencher o motivo da reprovação (ex: "CNPJ ilegível")  
 **Então** o status do seu cadastro deve ser atualizado para "Reprovado"  
 **E** a conta do hospital não deve ser convertida para "Hospital Parceiro"  
 **E** o hospital deve receber uma notificação informando sobre a reprovação e o motivo  
 **E** seu acesso à plataforma deve permanecer restrito.