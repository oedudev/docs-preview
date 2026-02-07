
# CallBack

## 1. Objetivo do Callback na Porto Seguro

No fluxo de contratação do Seguro Aluguel Fiança da Porto. Após o nosso sistema iniciar uma proposta, a Porto Seguro precisa de um meio para nos notificar sobre o resultado (aprovado, pendente ou recusado).

O objetivo do callback (webhook) é exatamente este: fornecer um mecanismo para que a Porto Seguro envie uma notificação automática (um evento) para o nosso sistema assim que o processo de análise for concluído. Isso permite que nosso sistema dê continuidade ao fluxo de emissão da proposta de forma automatizada, sem a necessidade de consultas manuais .

## 2. Passos Necessários Lado Porto Seguro(Futuramente)

Para que a Porto Seguro possa nos enviar notificações, é preciso registrar nosso endpoint de callback em seu sistema. Isso é feito através da **API de Cadastro do Webhook** deles.

1. **Obter Credenciais**: É necessário ter um `Client ID` e `Client Secret` válidos para o ambiente desejado (Homologação ou Produção), obtidos através do Portal do Desenvolvedor da Porto.
2. **Registrar o Webhook**: Realizar uma chamada `POST` para a API de Cadastro de Webhook da Porto:
    - **Endpoint**: `https://weebhook-parceiros.riscos-financeiros[AMBIENTE].com/envio/v1/inclusaoCadastro`
    - **Payload**: No corpo da requisição, devemos enviar um JSON contendo, entre outras coisas:
        - `nomeParceiro`: Um identificador para a nossa integração (ex: `Review.HML.INT`).
        - `clientId`: Nosso Client ID.
        - `apiCallback`: Um objeto que descreve nosso endpoint. É aqui que informamos a URL do nosso sistema que receberá a notificação.
            - **URL**: `https://[URL_DO_NOSSO_SISTEMA]/callback/{dsTenantId}/porto`

**Esse ponto não precisamos nos preocupar por enquanto, só com a parte de recebimento dos updates de proposta**

##### Fluxo proposto:

- Usuário acessa a página de integrações (ex.: http://localhost:3000/admin/integracao).

- Na tabela de integrações, cada item tem um botão "Cadastrar Callback" e um campo booleano is\_callback\_active para indicar se o callback está ativo.

- Ao clicar no botão, o sistema chama uma função interna ex; RegisterCallback que:

-Gera ou token Basic fixo(pedido no endpoint de cadastro da porto), armazenado na collection Token(ja existente) com tokenType registerCallback.

- Monta o payload da requisição com os detalhes dos nossos endpoints (auth e callback), incluindo o token Basic no campo tokenApi.

- Faz uma chamada POST para a API de Cadastro de Webhook da Porto (https://weebhook-parceiros.riscos-financeiros\[AMBIENTE\].com/envio/v1/inclusaoCadastro).

- Se a resposta for sucesso (status 200), atualiza o campo is\_callback\_active da integration para true no banco de dados.

- O token Basic é usado pela Porto para autenticar chamadas ao nosso endpoint de auth (/callback/auth), que responde com um JWT válido.

#### 3. Arquitetura da Funcionalidade Implementada (Nosso Sistema)

#####  1 - Fluxo Resumido

1. Seguradora → POST `/callback/:dsTenantId/:insuranceCompany`
2. Handler identifica seguradora, lê payload bruto.
3. Seleciona o parser da seguradora.
4. Parser valida e traduz payload externo → [model.Callback](about:blank).
5. Handler injeta [DsTenantID](about:blank) (da url) no objeto.
6. Chama o metodo para processar o callback, criado em proposalFacade: `ProcessProposalCallback()`.
7. Façade:
    - Valida integridade (tenant, proposta, estado).
    - Atualiza proposta / histórico / eventos.
    - Aplica regras (finalização, remoção de fila, notificações).
8. Resposta HTTP 200 em caso de sucesso (ou código de erro contextualizado)

##### 2 - Handler

1. Validar parâmetros da requisição.
2. Ler payload.
3. Resolver parser pelo identificador da seguradora com um if(ou switch para ficar menos verboso).
4. Executar Parse().
5. Popular DsTenantID no objeto.
6. Encaminhar para a facade, proposalFacade -&gt; ProcessProposalCallback()
7. Tratar e converter erros em seus status HTTP.

##### 3 - Parsers

Vão ser criados em rest/handlers/callback/parsers  separando em arquivos diferentes para cada seguradora. 

- `porto_parser.go`
- `tokio_parser.go`
- `too_parser.go`

1. Recebe o payload da seguradora
2. Instancia o objeto de /model/callback.go
3. Mapping dos status possiveis que a seguradora pode enviar, apontando para os nossos.
4. Função Parse(), que traduz os campos do payload, preenchendo os campos do nosso objeto.
5. Retorna para o handler.

##### 4 - Facade

1. Metodo em proposalFacade, que recebe nosso objeto interno preenchido.
2. Valida alguns campos essenciais
3. Localiza a proposta, utilizando dsTenantId como indice + o proposalID
4. Valida as transições de status. compara o antigo com o atual
5. Atualiza a proposta
6. Atualiza o historico de integração
7. Verifica se deve ser removida da fila
8. Dispara email