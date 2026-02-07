
# Requisitos não funcionais

##### Arquitetura

- Domínio isolado sem dependências diretas de frameworks
- Adaptadores inbound/outbound em pacotes distintos
- Interfaces definidas no domínio (inversão de dependência)

##### Confiabilidade

- Health checks de liveness/readiness configurados
- Resiliência: timeouts, retries, circuit breakers

##### Escalabilidade

- Aplicações stateless (sem sessão em memória local)

##### Segurança

- Patches críticos ≤ 72h, altos ≤ 7d, médios ≤ 30d
- Atualizações mensais de dependências
- TLS 1.2+ obrigatório em todas as comunicações
- Segredos via Vault/Secrets Manager
- Rate-limit e proteção contra brute-force

##### Testabilidade

- Cobertura mínima de testes: Go Unit ≥ 80%, Integração ≥ 60%
- Cobertura mínima de testes: Svelte Unit ≥ 70%, e2e ≥ 50% das rotas críticas
- Pirâmide de testes respeitada (unit &gt; integração &gt; e2e)
- Criação de testes e2e pelo QA para cada ticket

##### Observabilidade

- Logs estruturados em JSON com traceId
- Métricas de latência, erro, saturação (SLI/SLO)

##### Manutenibilidade

- Código Go validado por linter
- Complexidade ciclomática média ≤ 10
- Commits no padrão Conventional Commits
- Code review obrigatório

##### Implantação

- Builds reprodutíveis (go mod verify, lockfiles)
- Imagens Docker multi-stage, rootless, user não-root
- Migrações idempotentes e reversíveis