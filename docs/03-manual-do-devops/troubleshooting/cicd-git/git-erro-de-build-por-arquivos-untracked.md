---
id: 166
title: "Git: Erro de build por arquivos untracked"
updated_at: 2026-01-31T02:22:05.000000Z
---

# Git: Erro de build por arquivos untracked

# Git: Erro de build por arquivos untracked

## O Problema
Um erro comum ocorre quando novos arquivos são criados mas não são incluídos no commit, quebrando o build de outros desenvolvedores ou do CI/CD.

Isso acontece frequentemente ao usar o comando:
```bash
git commit -am "mensagem"
```
O flag `-a` (all) adiciona apenas arquivos *modificados* que já são rastreados. Ele **ignora** arquivos novos (untracked).

## Solução
Adote o **SOP (Standard Operating Procedure)** sagrado:

1. Sempre verifique o status antes de comitar:
   ```bash
   git status
   ```
2. Se houver arquivos novos (vermelhos em "Untracked files"), adicione-os explicitamente:
   ```bash
   git add .
   # ou
   git add nome-do-arquivo
   ```
3. Só então faça o commit.