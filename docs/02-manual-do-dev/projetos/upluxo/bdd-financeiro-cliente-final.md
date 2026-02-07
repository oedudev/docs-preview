
# BDD financeiro: Cliente final

**Cenário:** Cliente final visualiza indicadores financeiros

**Dado** que eu seja um cliente final

**Quando** eu acessar a página de dados financeiros

**Então** devo visualizar os principais indicadores financeiros

**Cenário:** Cliente final exporta extrado de atividades financeiras

**Dado** que eu seja um cliente final

**E** que eu esteja na página de indicadores financeiros

**Quando** eu clicar em "Exportar dados"

**Então** devo ser solicitado qual formato desejo exportar (PDF, CSV, etc...)

**E** os dados financeiros devem ser baixados no formato selecionado

**E** os dados devem corresponder aos da plataforma, no momento da exportação

**Cenário:** Cliente final faz análise retrospectiva de dados financeiros

**Dado** que eu seja um cliente final

**E** que eu esteja na página de indicadores financeiros

**Quando** eu selecionar "Analise retrospectiva"

**Então** devo ver a evolução dos meus indicadores financeiros ao longo do tempo