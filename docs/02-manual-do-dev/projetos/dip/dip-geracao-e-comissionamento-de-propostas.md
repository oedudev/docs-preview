
# DIP - Geração e Comissionamento de propostas

**Regras Gerais de Negócio**

1. **Imobiliária e Corretora:** Cada Imobiliária deve estar vinculada a uma, e somente uma, Corretora. Uma Corretora pode estar vinculada a várias Imobiliárias.
2. - **Cardinalidade: Imobiliária (N) -&gt; (1) Corretora. Vínculo obrigatório.**
3. **Corretora e Seguradoras:** Cada Corretora deve ter integração ativa com uma ou mais Seguradoras.
4. - **Cardinalidade: Corretora (1) -&gt; (N) Seguradoras. Vínculo obrigatório.**
5. **Comissão Padrão:** Cada par Corretora + Seguradora deve ter uma única comissão padrão cadastrada.
6. - **Cardinalidade: (1:1). Vínculo obrigatório.**
7. **Comissão Específica (Opcional):** Um trio Imobiliária + Corretora + Seguradora pode ter uma comissão específica cadastrada, que sobrepõe a comissão padrão.
8. - **Cardinalidade: (1:1). Vínculo opcional.**
9. **Proposta e Imobiliária:** Cada Proposta Matriz criada no sistema (DIP) deve ser vinculada a uma única Imobiliária no momento de sua criação no Frontend.
10. - **Cardinalidade: (1:1).**
11. **Origem do Grupo de Propostas:** Cada Proposta Matriz dará origem a um, e somente um, Grupo de Propostas no Backend.
12. - **Cardinalidade: (1:1).**
13. **Vínculo do Grupo de Propostas:** Cada Grupo de Propostas deve estar vinculado a um único par Imobiliária + Corretora.
14. - **Cardinalidade: (1:1).**
15. **Conteúdo do Grupo de Propostas:** Cada Grupo de Propostas conterá uma Proposta de Seguro para cada Seguradora integrada à Corretora de origem.
16. - **Cardinalidade: (1:N).**

**Fluxo Resumido da Geração de Propostas**

**Input do Usuário na UI** ➔ **Criação da Proposta Matriz** ➔ **Identificação da Imobiliária** (Input usuário) ➔ **Busca da Corretora** vinculada à Imobiliária ➔ **Busca das Seguradoras** integradas à Corretora ➔ **Busca de Comissionamento** para cada Seguradora (ver fluxo detalhado abaixo) ➔ **Criação do Grupo de Propostas** ➔ **Geração e Envio** das Propostas de Seguro individuais para cada Seguradora.

**Fluxo Detalhado: Busca de Comissionamento**

Este fluxo é executado para **cada Seguradora** encontrada no passo anterior.

1. O sistema busca por uma comissão específica cadastrada para o trio: **Imobiliária + Corretora + Seguradora**.
2. - **Se encontrada (SIM):** A comissão específica é retornada e o fluxo encerra com sucesso para esta seguradora.
    - **Se não encontrada (NÃO):** O sistema prossegue para o passo 2.
3. O sistema busca pela comissão padrão cadastrada para o par: **Corretora + Seguradora**.
4. - **Se encontrada (SIM):** A comissão padrão é retornada e o fluxo encerra com sucesso para esta seguradora.
    - **Se não encontrada (NÃO):** O sistema retorna um **ERRO**.
5. **Tratamento do Erro:** A ausência de uma comissão (tanto específica quanto padrão) é considerada uma falha de configuração crítica. A geração do Grupo de Propostas é **interrompida** e nenhuma Proposta de Seguro é enviada. O sistema deve registrar o erro e notificar o usuário/administrador sobre a necessidade de cadastrar a comissão faltante.  
      
    Busca trio **Imobiliária+Corretora+Seguradora** -&gt; Comissão cadastrada? (SIM) -&gt; Retorna comissão  
                    |  
                    (NÃO)  
                    |   
                 Busca par **Corretora+Seguradora**  
                    |   
                  Comissão cadastrada?  
                  \_\_\_\_\_\_\_\_\_\_\_\_\_|\_\_\_\_\_\_\_\_\_\_\_\_\_   
                  |       |  
                 (SIM)     (NÃO)  
                 |       |  
                Retorna Comissão   Retona Erro

**Glossário de Termos**

- **Proposta Matriz:** A proposta original cadastrada no Frontend, contendo os dados fornecidos pelo usuário para a cotação do seguro.
- **Grupo de Propostas:** Um contêiner lógico que agrupa todas as Propostas de Seguro geradas a partir de uma única Proposta Matriz. Possui um identificador único.
- **Proposta de Seguro:** Cada proposta individual, gerada a partir da Proposta Matriz e enviada para uma das seguradoras integradas.

