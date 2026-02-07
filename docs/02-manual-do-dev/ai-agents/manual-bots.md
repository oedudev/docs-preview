# Manual do Bot Desenvolvedor 🤖

*A Constituição Digital para a Excelência do Código.*

## 1. O Ritual da Alvorada 🌅
Todo bot, ao iniciar sua jornada (sessão), deve:
1.  **Ler o Contexto:** Absorver `SOUL.md` (identidade), `USER.md` (quem servimos) e `MEMORY.md` (o que já aprendemos).
2.  **Situar-se:** Executar `ls -F` e `git status` para entender o terreno.
3.  **Verificar a Missão:** Ler o último `memory/YYYY-MM-DD.md` para não repetir erros de ontem.

## 2. Os Mandamentos do Código 📜
1.  **Não Comitarás Segredos:** `.env` e chaves de API são sagrados e invisíveis.
2.  **Mensagens com Propósito:** Commits devem contar uma história ("feat: adiciona...", "fix: corrige..."), não apenas apontar um fato ("update").
3.  **Limpeza é Virtude:** Código morto é peso morto. Remova-o.
4.  **O Teste é a Prova:** Se não foi testado, não existe.
5.  **A Regra de Ouro do Commit:** Todo commit deve ser testado localmente antes de subir. Código quebrado não sai da máquina.
6.  **O Fluxo Sagrado:** Jamais comitarás na `main`. Crie uma branch, faça suas alterações e abra um Pull Request (PR).
7.  **Documentação Viva:** Se o código mudou, a documentação deve mudar junto. Atualize o manual imediatamente.

## 3. Protocolos de Colaboração 🤝
1.  **Chame pelo Nome:** Ao falar com humanos, use o nome (Edu).
2.  **Peça Ajuda (com Brio):** Se travar, explique o obstáculo com precisão técnica, não com desculpas.
3.  **Documente a Vitória:** Ao concluir, atualize a documentação pertinente. Conhecimento não compartilhado é perdido.

## 4. Diretrizes Específicas (Itens do Edu)

### 4.1. Como obter comentários de Pull Requests (GitHub CLI)
O comando `gh pr view` padrão não exibe comentários inline (feitos em linhas específicas do código). Para ter visibilidade total do que bots (como Sentry, Devin) ou humanos estão comentando, utilize a API GraphQL do GitHub.

**Comando Mágico:**
```bash
gh api graphql -F owner='{owner}' -F name='{repo}' -F number={pr_number} -f query='
query($owner: String!, $name: String!, $number: Int!) {
  repository(owner: $owner, name: $name) {
    pullRequest(number: $number) {
      reviews(first: 20) {
        nodes {
          author { login }
          state
          body
          comments(first: 20) {
            nodes {
              body
              path
              line
            }
          }
        }
      }
    }
  }
}'
```

**Por que usar isso?**
- Permite ver o **arquivo** (`path`) e a **linha** (`line`) onde o problema foi apontado.
- Revela comentários de ferramentas automatizadas que muitas vezes ficam ocultos no resumo geral.
- Garante que nenhum feedback crítico de segurança ou bug passe despercebido antes do merge.
