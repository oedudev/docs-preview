
# Como criar Token de API Somente Leitura (Read-Only)

# 🔐 Como criar Token de API Somente Leitura (Read-Only)

Por padrão, os tokens de API do Bookstack herdam as permissões do usuário que os criou. Para criar um token seguro para integrações (ex: outros bots que apenas consomem conteúdo), siga este procedimento.

<div class="callout warning" id="bkmrk-%E2%9A%A0%EF%B8%8F-regra-de-ouro-ape">#### ⚠️ Regra de Ouro

**Apenas o Clóvis (Bot Bibliotecário) deve ter permissão de escrita na documentação.** Todos os outros bots e integrações devem usar tokens Read-Only.

</div>---

## Passo 1: Criar um Papel (Role) Restritivo

1. Acesse **Configurações** &gt; **Papéis**.
2. Clique em **"Criar novo Papel"**.
3. Nome: `Bot Read-Only` (ou similar).
4. Em **Permissões de Sistema**, marque: 
    - ✅ *Acessar API do sistema*
    - (Opcional) *Acessar conteúdo público* se a instância for fechada.
5. Em **Permissões de Ativos** (Livros, Capítulos, Páginas): 
    - Marque APENAS a coluna **Visualizar** (View).
    - **Desmarque todas** as colunas de Criar, Editar e Excluir.
6. Salve o Papel.

## Passo 3: Gerar o Token

1. Faça logout e logue com o novo usuário `Bot Leitor`.
2. Clique no avatar no canto superior direito &gt; **Editar Perfil**.
3. Role até **Tokens de API** e clique em **"Criar Token"**.
4. Dê um nome (ex: `Integração Clécio`) e defina a validade (ou deixe vazio para expirar nunca, se a política permitir).
5. **Copie o "Token ID" e o "Token Secret" imediatamente.** O segredo não será mostrado novamente.

