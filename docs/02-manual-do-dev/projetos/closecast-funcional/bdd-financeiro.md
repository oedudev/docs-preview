
# BDD financeiro

##### Relatório de vendas

**Cenário:** Visualizar gráfico vendas mensais vs meta

**Dado** que eu seja um usuário criador

**E** que esteja no meu painel administrativo"

**Quando** eu acessar a página de "relatório de vendas"

**Então** devo visualizar o gráfico de "Vendas mensais vs Meta"

**E** o gráfico deve mostrar os últimos 12 meses

**E** o gráfico deve ser do tipo Valor (reais) X mês

**E** cada mês deve contar 2 barras, a meta mensal e o valor de vendar realizadas

**E** a escala do gráfico deve ser tal que a maior barra defina o maior valor (eixo Y) do gráfico

**E** o eixo Y deve começar em 0

**E** devo visualizar meu crescimento anual (%)

**E** devo visualizar a quantidade de médias mensais atingidas nos últimos 12 meses

**E** devo visualizar meu valor de ticket médio

**Cenário:** Visualizar estatísticas de entrega

**Dado** que eu seja um usuário criador

**E** que esteja no meu painel administrativo"

**Quando** eu acessar a página de "relatório de vendas"

**Então** devo visualizar o número de vídeos entregues

**E** devo visualizar a quantidade de clientes únicos que possuo

**Cenário:** Visualizar valores a receber

**Dado** que eu seja um usuário administrador

**E** que eu esteja no painel administrativo

**Quando** eu acessar a aba "Dashboard financeiro"

**Então** devo visualizar o total de valores a receber pela plataforma

**E** devo ver os valores a receber dividos para cada meio de pagamento

**Cenário:** Atualizar valores

**Dado** que eu seja um usuário criador

**E** que eu esteja no painel administrativo

**E** acessar a aba "Dashboard financeiro"

**Quando** eu clicar no ícone para "recarregar valores"

**Então** os valores do grupo selecionados devem ser atualizados com os dados mais recentes

**Cenário:** Excluir criador

**Dado** que eu seja um usuário administrador

**E** que eu esteja no painel administrativo

**E** que eu esteja na aba "Ranking de Casts"

**E** que eu clique no ícone para "excluir" um criador

**Quando** eu confirmar a exclusão

**Então** a conta do criador deve ser desativada, não excluida do banco

**E** todos os conteúdos relacionados a esse criador devem desaparecer da plataforma

**E** esse criador não deverá poder receber novos pedidos

**Cenário:** Visualizar denúncias

**Dado** que eu seja um usuário administrador

**E** que eu esteja no painel administrativo

**Quando** eu acessar a aba "Denúncias"

**Então** devo visualizar todas as denúncias abertar no sistema

**E** as denúncias devem estar ordenadas pela métrica "Em aberto" &gt; "Em análise" &gt; "Finalizada"

**E** as denúncias dentro de um mesmo grupo devem estar ordenadas por data de criação (mais antigas aparecem primeiro)

**Cenário:** Resolver denúncia

**Dado** que eu seja um usuário administrador

**E** que eu esteja no painel administrativo

**E** que eu acesse a aba "Denúncias"

**Quando** eu clicar em "Resolver" uma denúncia

**Então** o status da denúncia deve ser alterado para "Finalizada"

**E** o usuário que realizou a denúncia deve ser notificado

**Cenário:** Visualizar total de usuários da plataforma

**Dado** que eu seja um usuário administrador

**E** que eu esteja no painel administrativo

**Quando** eu acessar a aba "Gestão de usuários"

**Então** devo visualizar o total de usuários na plataforma

**E** visualizar o total de usuários Ativos

**E** visualizar o total de usuários Suspensos

**E** visualizar o total de Clientes Novos

**Cenário**: Visualizar usuários - Filtros

**Dado** que eu seja um usuário administrador

**E** que eu esteja no painel administrativo

**E** esteja na página de "Gestão de usuários"

**Quando** eu aplicar filtros de busca

**Então** devo visualizar os usuários cadastrados na plataforma que correspondam aos filtros de busca que inseri

**Cenário:** Atualizar dados

**Dado** que eu seja um usuário administrador

**E** que eu esteja no painel administrativo

**E** esteja na página de "Gestão de usuários"

**Quando** eu clicar em "Atualizar"

**Então** todos os dados do meu painel de gestão devem ser atualizados com os dados mais recentes