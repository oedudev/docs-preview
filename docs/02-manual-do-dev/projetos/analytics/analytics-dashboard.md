
# Analytics Dashboard

1. CONTEXTO E OBJETIVOS

- **Experiência Unificada:** Substituir o dashboard anterior por uma experiência única, responsiva e completa no admin.
- **Consolidação:** Consolidar métricas de uso, engajamento e desempenho em um único painel.
- **Exportação Fiel:** Entregar exports fiéis aos dados exibidos, incluindo snapshot completo em PDF.
- **Compatibilidade:** Garantir compatibilidade com o tema claro/escuro do Unfold e navegação simplificada (menu lateral atualizado).

2. IMPLEMENTAÇÕES PRINCIPAIS

- **Visualização:** Dois grids de KPIs, nove visualizações e tabelas responsivas.
- **Tema Adaptativo:** Gráficos Chart.js são recriados quando o usuário troca o tema.
- **Tooltip de Crescimento:** Descritivo no card de "Crescimento" explicando comparações com/sem filtro de data.
- **Export Dashboard:** Rotina com `html2canvas` + `jsPDF` que oculta controles, exibe resumo de filtros e gera PDF.
- **Exports Individuais:** CSV/XLSX/TSV/JSON/YAML/HTML com colunas alinhadas ao que aparece na UI (sem redundâncias, com percentuais quando relevante).
- **Limpeza:** Remoção do menu "Dashboard" legado e da view antiga de Métricas.

3. FILTROS E CONTROLES

- **Data Inicial / Data Final:** Intervalos absolutos; aplicam-se a praticamente todas as métricas baseadas em datas.
- **Tipo de Análise:** Filtra por `RegisteredAnalysis.name`, afetando cards e gráficos orientados a execuções.
- **Perfil de Usuário:** Restringe queries por `User.profile_id`; impacta métricas de usuários, SLAs, crescimento, brackets e recência.
- **Granularidade:** Seletor Diário/Mensal/Anual exclusivo do gráfico de "Volume Temporal" (também influencia o export temporal).
- **Notas:** Com filtro de data, o Crescimento compara períodos equivalentes; sem filtro, considera 30 dias atuais vs. 30 dias anteriores.

4. KPIS

- **Usuários Ativos:** Contagem de `User.is_active` respeitando `date_to` e perfil.
- **Total de Análises:** Volume de `Analysis` no intervalo filtrado.
- **Tempo Médio de Sessão:** Média de `UserSession.duration`.
- **Crescimento:** Variação percentual de novos usuários ativos frente ao período anterior equivalente.
- **Total de Usuários:** Soma de ativos + inativos + pendentes (pendentes limitados por `date_to` e perfil quando houver ligação).
- **SLA Ativação:** Média entre `PendingUser.created_at` e `updated_at` quando status = ativo.
- **SLA Primeira Análise:** Tempo médio entre ativação e primeira análise concluída.
- **Taxa de Sucesso:** Distribuição sucesso/erro/pendente das análises filtradas.

5. VISUALIZAÇÕES E TABELAS

- **Top 15 Usuários por Análises:** Ranking pelo número de execuções.
- **Distribuição de Status:** Barras empilhadas mostrando ativos com/sem análise e pendentes por status.
- **Top 15 Análises Mais Usadas:** Ranking por quantidade de execuções por tipo registrado.
- **Taxa de Sucesso das Análises:** Gráfico de pizza com sucesso/erro/pendente.
- **Usuários Ativos x Quantidade de Análises:** Faixas (0, 1-2, 3-10, etc.) com contagem e percentual.
- **Análises Realizadas por Período:** Faixas de recência (30 dias, 31-90, etc.) com contagem e percentual.
- **Range de Horário:** Série 24h com quantidade de análises por hora.
- **Volume Temporal de Análises:** Série temporal diária/mensal/anual dependendo da granularidade.
- **Top 15 Análises por Tempo de Execução:** Média de duração para análises bem-sucedidas (até 24h).

6. DETALHAMENTO POR ANÁLISE

- **Top 15 Usuários por Análises:** Usa `get_top_users_by_analysis`, anota `analysis_count` por usuário ativo, aplica filtros de data/tipo/perfil e ordena de forma decrescente limitando a 15 nomes.
- **Distribuição de Status:** Combina `get_user_status_distribution` (ativos com/sem análise + pendentes por status) e `get_user_status_distribution_stacked`, ambos filtrando por perfil e datas quando aplicável.
- **Top 15 Análises Mais Usadas:** `get_top_analyses` agrega `Analysis` por `type`, aplica filtros, cruza com `RegisteredAnalysis` para exibir descrição e retorna os 15 maiores contadores.
- **Taxa de Sucesso das Análises:** `get_analysis_success_rate` conta sucessos/erros/pendentes, calcula percentual relativo ao total filtrado e monta o dataset do gráfico de pizza.
- **Usuários Ativos x Quantidade de Análises:** `get_users_by_analysis_brackets_table` classifica usuários ativos (com filtros) em faixas de execução e calcula o percentual de cada bracket sobre o total.
- **Análises Realizadas por Período (Recência):** `get_analysis_recency_table` conta análises concluídas em janelas de dias (30, 31-90, etc.) e gera percentual relativo ao volume total do intervalo.
- **Range de Horário:** `get_hourly_usage` trunca `Analysis.created_at` por hora, preenche as 24 posições com zero quando necessário e aplica filtros de tipo/perfil.
- **Volume Temporal de Análises:** `get_temporal_volume` usa `TruncDate/TruncMonth/TruncYear` de acordo com a granularidade selecionada, ordena por período e devolve labels/valores para gráfico e export.
- **Top 15 Análises por Tempo de Execução:** `get_avg_execution_time` filtra apenas análises com sucesso (e tempo entre start/finish), descarta durações &gt;24h, calcula média por tipo e converte para texto amigável.

7. EXPORTAÇÕES

- **Formato:** Dropdown "Exportar" em cada card gera arquivos em CSV, XLSX, TSV, JSON, YAML ou HTML.
- **Mapeamento:** `_handle_analytics_export` mapeia cada análise para a função de serviço correspondente e define cabeçalhos.
- **Customização:** Exportações customizadas (status, sucesso, faixas, recência, horário, temporal) usam `_get_custom_export_rows` para formatar linhas.
- **Melhorias Recentes:** Brackets e recência incluem percentual; rankings removem a coluna "tipo" redundante; tempos de execução exportam descrição + tempo médio + quantidade.
- **Export Completo (PDF):** Usa `exportDashboard()` para capturar snapshot do painel respeitando o tema atual e exibindo os filtros aplicados.

**8. IMPACTO DOS FILTROS** 

[![image.png](/img/analytics-dashboard-1.png)](https://ajuda.digitalsys.com.br/uploads/images/gallery/2025-12/I0ieAyrNdFA8StEL-image.png)