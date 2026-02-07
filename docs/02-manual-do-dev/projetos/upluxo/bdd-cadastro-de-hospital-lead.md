
# BDD Cadastro de Hospital Lead

**Funcionalidade:** Cadastramento de Hospitais Lead

 Como um hospital  
 Desejo cadastrar me cadastrar na plataforma  
 Para indicar o interesse meu interesse em me Hospital Parceiro  
 E submeter meus dados e documentação para análise   
  
\@CaminhoFeliz  
**Cenário:** Criação bem sucedida de Conta para Hospital Lead

 **Dado** que eu seja um Hospital Lead  
 **Quando** ele fornecer as seguintes informações válidas:  
 **| Campo |**  
 | E-mail Institucional |  
 | Nome do hospital |  
 | CNPJ |  
 | CEP |  
 | Logradouro e Número |  
 | Bairro, Cidade e Estado |  
 | Senha |  
 | Confirmação de Senha |  
 **E** anexar os documentos obrigatórios  
 **E** aceitar os Termos de Serviço  
 **E** submeter o cadastro  
 **Então** uma conta para o hospital deve ser criada com sucesso  
 **E** meu cadastro deve ser encaminhado para análise  
 **E** uma conta de Hospital Lead deve ser criada  
  
\#=====================ERROS POR VALIDAÇÃO=====================

  
 **Cenário:** Tentativa de cadastro de Hospital Parceiro com e-mail em branco

 **Dado** que eu seja um hospital e deseje criar uma conta  
 **Quando** eu não fornecer um e-mail  
 **E** submeter o cadastro  
 **Então** devo receber a mensagem de "É necessário informar o e-mail"  
 **E** meu cadastro não deve ser realizado  
  
  
**Cenário:** Tentativa de cadastro com formato de e-mail inválido

 **Dado** que eu seja um hospital e deseje criar uma conta  
 **Quando** eu fornecer um e-mail com formato inválido  
 **E** submeter o cadastro  
 **Então** devo receber a mensagem de "O e-mail informado não tem formato válido"  
 **E** meu cadastro não deve ser realizado  
  
  
 **Cenário:** Tentativa de cadastro com e-mail de domínio não institucional

  **Dado** que eu seja um hospital e deseje criar uma conta  
  **Quando** eu fornecer um e-mail não institucional  
  **E** submeter o cadastro  
  **Então** devo receber a mensagem de "O e-mail deve ser de uma instituição parceira"  
 **E** meu cadastro não deve ser realizado  
  
  
 **Cenário:** Tentativa de cadastro de com um e-mail já cadastrado

 **Dado** que eu seja um hospital e deseje criar uma conta  
 **Quando** eu fornecer um E-mail já em uso na plataforma  
 **E** submeter o cadastro  
 **Então** devo receber a mensagem de "Este e-mail já possui uma conta cadastrada"  
 **E** meu cadastro não deve ser realizado  
  
  
 **Cenário:** Tentativa de cadastro com Razão Social em branco

 **Dado** que eu seja um hospital e deseje criar uma conta  
 **Quando** não fornecer a Razão Social  
 **E** submeter o cadastro  
 **Então** devo receber a mensagem de "É necessário informar a Razão Social"  
 **E** meu cadastro não deve ser realizado  
  
 **Cenário:** Tentativa de cadastro com Nome Fantasia em branco

 **Dado** que eu seja um hospital e deseje criar uma conta  
 **Quando** não fornecer o Nome Fantasia  
 **E** submeter o cadastro  
 **Então** devo receber a mensagem de "É necessário informar o Nome Fantasia"  
 **E** meu cadastro não deve ser realizado  
  
  
 **Cenário:** Tentativa de cadastro com CNPJ em branco

 **Dado** que eu seja um representante de hospital e deseje criar uma conta  
 **Quando** eu não fornecer um CNPJ  
 **E** submeter o cadastro  
 **Então** devo receber a mensagem de "É necessário informar o CNPJ"  
 **E** meu cadastro não deve ser realizado  
  
  
 **Cenário:** Tentativa de cadastro com formato de CNPJ inválido

 **Dado** que eu seja um representante de hospital e deseje criar uma conta  
 **Quando** eu fornecer um CNPJ inválido  
 **E** submeter o cadastro  
 **Então** devo receber a mensagem de "O CNPJ informado não tem formato válido"  
 **E** meu cadastro não deve ser realizado  
  
  
 **Cenário:** Tentativa de cadastro com um CNPJ já cadastrado

 **Dado** que eu seja um representante de hospital e deseje criar uma conta  
 **Quando** eu fornecer um CNPJ já em uso na plataforma  
 **E** submeter o cadastro  
 **Então** devo receber a mensagem de "Este CNPJ já possui uma conta cadastrada"  
 **E** meu cadastro não deve ser realizado  
  
  
 **Cenário:** Tentativa de cadastro com CEP em branco  
  
 **Dado** que eu seja um representante de hospital e deseje criar uma conta  
 **Quando** eu não fornecer o CEP do endereço do hospital  
 **E** submeter o cadastro  
 **Então** devo receber a mensagem de "É necessário informar o CEP"  
 **E** meu cadastro não deve ser realizado  
  
  
 **Cenário:** Tentativa de cadastro com formato de CEP inválido

 **Dado** que eu seja um representante de hospital e deseje criar uma conta  
 **Quando** eu fornecer um CEP com formato inválido  
 **E** submeter o cadastro  
 **Então** devo receber a mensagem de "O CEP informado não tem formato válido"  
 **E** meu cadastro não deve ser realizado  
  
  
 **Cenário:** Tentativa de cadastro com Logradouro em branco  
  
 **Dado** que eu seja um representante de hospital e deseje criar uma conta  
 **Quando** eu não fornecer o Logradouro do endereço do hospital  
 **E** submeter o cadastro  
 **Então** devo receber a mensagem de "É necessário informar o logradouro"  
 **E** meu cadastro não deve ser realizado  
  
  
**Cenário:** Tentativa de cadastro com Número em branco

 **Dado** que eu seja um representante de hospital e deseje criar uma conta  
 **Quando** eu não fornecer o Número do endereço do hospital  
 **E** submeter o cadastro  
 **Então** devo receber a mensagem de "É necessário informar o número"  
 **E** meu cadastro não deve ser realizado  
  
  
 **Cenário:** Tentativa de cadastro com Bairro em branco

 **Dado** que eu seja um representante de hospital e deseje criar uma conta  
 **Quando** eu não fornecer o Bairro do endereço do hospital  
 **E** submeter o cadastro  
 **Então** devo receber a mensagem de "É necessário informar o bairro"  
 **E** meu cadastro não deve ser realizado  
  
  
 **Cenário:** Tentativa de cadastro com Cidade em branco

 **Dado** que eu seja um representante de hospital e deseje criar uma conta  
 **Quando** eu não fornecer a Cidade do endereço do hospital  
 **E** submeter o cadastro  
 **Então** devo receber a mensagem de "É necessário informar a cidade"  
 **E** meu cadastro não deve ser realizado  
  
  
 **Cenário:** Tentativa de cadastro com Estado em branco

 **Dado** que eu seja um representante de hospital e deseje criar uma conta  
 **Quando** eu não fornecer o Estado do endereço do hospital  
 **E** submeter o cadastro  
 **Então** devo receber a mensagem de "É necessário informar o estado"  
 **E** meu cadastro não deve ser realizado  
  
  
 **Cenário:** Tentativa de cadastro com País em branco

 **Dado** que eu seja um representante de hospital e deseje criar uma conta  
 **Quando** eu não fornecer o País do endereço do hospital  
 **E** submeter o cadastro  
 **Então** devo receber a mensagem de "É necessário informar o país"  
 **E** meu cadastro não deve ser realizado

 **Cenário:** Tentativa de cadastro com senha em branco  
  
 **Dado** que eu seja um representante de hospital e deseje criar uma conta  
 **Quando** eu não fornecer uma Senha  
 **E** submeter o cadastro  
 **Então** devo receber a mensagem de "É necessário informar a senha"  
 **E** meu cadastro não deve ser realizado

 **Cenário:** Tentativa de cadastro com senha muito curta

 **Dado** que eu seja um representante de hospital e deseje criar uma conta  
 **Quando** eu fornecer uma Senha com menos de 8 caracteres  
 **E** submeter o cadastro  
 **Então** devo receber a mensagem de "A senha deve ter pelo menos 8 caracteres"  
 **E** meu cadastro não deve ser realizado

  
 **Cenário:** Tentativa de cadastro com senha sem letra maiúscula  
  
 **Dado** que eu seja um representante de hospital e deseje criar uma conta  
 **Quando** eu fornecer uma Senha que não contenha nenhuma letra maiúscula  
 **E** submeter o cadastro  
 **Então** devo receber a mensagem de "A senha deve conter pelo menos uma letra maiúscula"  
 **E** meu cadastro não deve ser realizado

  
 **Cenário:** Tentativa de cadastro com senha sem letra minúscula

 **Dado** que eu seja um representante de hospital e deseje criar uma conta  
 **Quando** eu fornecer uma Senha que não contenha nenhuma letra minúscula  
 **E** submeter o cadastro  
 **Então** devo receber a mensagem de "A senha deve conter pelo menos uma letra minúscula"  
 **E** meu cadastro não deve ser realizado  
  
  
 **Cenário:** Tentativa de cadastro com senha sem número

 **Dado** que eu seja um representante de hospital e deseje criar uma conta  
 **Quando** eu fornecer uma Senha que não contenha nenhum número  
 **E** submeter o cadastro  
 **Então** devo receber a mensagem de "A senha deve conter pelo menos um número"  
 **E** meu cadastro não deve ser realizado

 **Cenário:** Tentativa de cadastro com senha sem caractere especial

 **Dado** que eu seja um representante de hospital e deseje criar uma conta  
 **Quando** eu fornecer uma Senha que não contenha nenhum caractere especial  
 **E** submeter o cadastro  
 **Então** devo receber a mensagem de "A senha deve conter pelo menos um caractere especial"  
 **E** meu cadastro não deve ser realizado

 **Cenário:** Tentativa de cadastro com confirmação de senha em branco

 **Dado** que eu seja um representante de hospital e deseje criar uma conta  
 **Quando** eu não fornecer uma Confirmação de Senha  
 **E** submeter o cadastro  
 **Então** devo receber a mensagem de "É necessário confirmar a senha"  
 **E** meu cadastro não deve ser realizado  
  
 **Cenário:** Tentativa de cadastro com senhas que não coincidem

 **Dado** que eu seja um representante de hospital e deseje criar uma conta  
 **Quando** eu fornecer uma Confirmação de Senha que seja divergente da Senha  
 **E** submeter o cadastro  
 **Então** devo receber a mensagem de "As senhas não coincidem"  
 **E** meu cadastro não deve ser realizado

 **Cenário:** Tentativa de cadastro sem aceitar os termos  
  
 **Dado** que eu seja um representante de hospital e deseje criar uma conta  
 **Quando** eu não marcar a opção de aceite dos Termos de Serviço  
 **E** submeter o cadastro  
 **Então** devo receber a mensagem de "É necessário aceitar os Termos de Serviço"  
 **E** meu cadastro não deve ser realizado  
  
 **Cenário:** Tentativa de cadastro sem upload de documentação obrigatória

 **Dado** que eu seja um hospital e deseje criar uma conta  
 **Quando** eu não anexar o documento obrigatório "&lt;documento&gt;"  
 **E** submeter o cadastro  
 **Então** devo receber a mensagem de "É necessário anexar o &lt;documento&gt;"  
 **E** meu cadastro não deve ser realizado