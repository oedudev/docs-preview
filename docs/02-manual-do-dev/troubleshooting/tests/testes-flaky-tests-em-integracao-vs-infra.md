
# Testes: Flaky Tests em Integração vs Infra

# Testes: Flaky Tests (Intermitentes)

## O Problema
Testes de integração que falham aleatoriamente ("flaky tests"): às vezes passam, às vezes falham, sem alteração de código.

## Causas Comuns
1. **Race Conditions:** O teste tenta verificar algo antes do banco de dados ou da API ter respondido.
2. **Estado Compartilhado:** Um teste anterior sujou o banco e não limpou.
3. **Recursos de Infra:** Timeout por lentidão do container/banco no CI.

## Estratégias de Mitigação
1. **Wait, don't sleep:** Nunca use `sleep(5)`. Use asserções de espera explícita (ex: `await page.waitForSelector()`, `retry_until_success`).
2. **Isolamento:** Garanta que cada teste roda em uma transação de banco que é revertida (rollback) ao final.
3. **Logs:** Aumente a verbosidade dos logs no CI para identificar se a falha é timeout ou lógica.