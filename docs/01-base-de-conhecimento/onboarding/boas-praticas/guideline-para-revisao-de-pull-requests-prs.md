
# Guideline para Revisão de Pull Requests (PRs)

## 📌 Objetivo

Ajudar quem está começando a revisar PRs a entender o que observar, como dar feedback e o que aprovar ou solicitar mudanças.

### 2. **Código**

- [ ] O código está legível e fácil de entender?
- [ ] Há nomes claros para variáveis, funções e classes?
- [ ] O código segue os padrões da equipe (lint, estilo, convenções)?
- [ ] Evita duplicação de código?
- [ ] Evita complexidade desnecessária?

### 4. **Segurança e Permissões (se aplicável)**

- [ ] O PR lida corretamente com permissões e autenticação?
- [ ] Evita vazamentos de dados sensíveis?
- [ ] Dados dos usuários estão protegidos?

### 6. **Testes**

- [ ] Há testes automatizados cobrindo as mudanças?
- [ ] Testes cobrem casos comuns e bordas?
- [ ] Os testes existentes continuam passando?

### 8. **Deploy e Riscos**

- [ ] Essa mudança pode quebrar algo em produção?
- [ ] É compatível com a versão atual?
- [ ] Se for necessário rollback, é simples?

## 💡 Dicas Finais

- Não precisa achar tudo sozinho. PRs são trabalho em equipe.
- Se tiver dúvida, comente! Melhor perguntar do que deixar passar algo crítico.
- Ao aprovar, revise se **você colocaria esse código em produção com confiança**