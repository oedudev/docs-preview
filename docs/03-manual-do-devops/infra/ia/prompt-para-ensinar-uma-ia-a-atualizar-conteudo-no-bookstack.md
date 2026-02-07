---
id: 58
title: "Prompt para Ensinar uma IA a Atualizar Conteúdo no BookStack"
updated_at: 2025-05-12T03:23:18.000000Z
---

# Prompt para Ensinar uma IA a Atualizar Conteúdo no BookStack

**Objetivo Principal:**
Sua tarefa é interagir com uma instância específica do BookStack para atualizar conteúdos existentes, como páginas e metadados de livros, utilizando a API REST fornecida.

**Detalhes da Instância BookStack Alvo:**

*   **URL Base da Instância:** `https://ajuda.digitalsys.com.br`
*   **Documentação de Referência da API:** `https://demo.bookstackapp.com/api/docs` (Utilize esta documentação para entender os endpoints, parâmetros e formatos de requisição/resposta.)

**Autenticação na API:**

*   **Método:** Autenticação baseada em Token.
*   **Cabeçalho HTTP Necessário:** `Authorization: Token <SEU_TOKEN_ID>:<SEU_TOKEN_SECRET>`
*   **⚠️ Nota de Segurança Importante:** Os valores `<SEU_TOKEN_ID>` e `<SEU_TOKEN_SECRET>` são placeholders. Em uma implementação real, estes tokens NUNCA devem ser codificados diretamente no prompt ou no código. Eles devem ser fornecidos de forma segura à IA no momento da execução (por exemplo, através de variáveis de ambiente ou um sistema de gerenciamento de segredos).

**Fluxo Geral para Atualizar uma Página no BookStack:**

1.  **Identificar a Página a Ser Atualizada:**
    *   **Opção A (ID da Página Conhecido):** Se você já possui o `ID` numérico da página, pode usá-lo diretamente.
    *   **Opção B (ID da Página Desconhecido):**
        *   Liste páginas dentro de um livro específico (se o `book_id` for conhecido): `GET {URL_BASE}/api/pages?filter[book_id]={book_id}&filter[name:like]=%Nome Parcial da Página%`
        *   Liste todas as páginas e filtre pelo nome: `GET {URL_BASE}/api/pages?filter[name:like]=%Nome da Página%`
        *   A resposta para listagens geralmente inclui um array `data` com os objetos da página, cada um contendo um `id`.

2.  **(Opcional, mas Recomendado) Obter Detalhes da Página Atual:**
    *   Endpoint: `GET {URL_BASE}/api/pages/{page_id}`
    *   Isso permite verificar o conteúdo atual (seja em `html` ou `markdown`) antes de modificá-lo.

3.  **Atualizar a Página:**
    *   Endpoint: `PUT {URL_BASE}/api/pages/{page_id}`
    *   Método HTTP: `PUT`
    *   Cabeçalhos: `Content-Type: application/json`, `Authorization: Token <SEU_TOKEN_ID>:<SEU_TOKEN_SECRET>`
    *   Corpo da Requisição (JSON). Campos comuns para atualização:
        *   `book_id` (integer, opcional): ID do livro ao qual a página pertence. Mude apenas se for mover a página.
        *   `name` (string, opcional): Novo nome para a página.
        *   `markdown` (string): Conteúdo da página em formato Markdown. (A API também aceita `html`.)
        *   `tags` (array, opcional): Array de objetos de tag. Ex: `[{"name": "Status", "value": "Revisado"}]`

    *   Exemplo de Corpo da Requisição para atualizar o conteúdo Markdown e o nome de uma página:
        ```json
        {
          "name": "Novo Título da Página",
          "markdown": "# Novo Conteúdo da Página\n\nEste é o conteúdo atualizado da página em Markdown.",
          "book_id": 123 
        }
        ```

**Fluxo Geral para Atualizar Metadados de um Livro:**

1.  **Identificar o Livro a Ser Atualizado:**
    *   **Opção A (ID do Livro Conhecido):** Use o `ID` numérico do livro.
    *   **Opção B (ID do Livro Desconhecido):** `GET {URL_BASE}/api/books?filter[name:like]=%Nome do Livro%`

2.  **Atualizar o Livro:**
    *   Endpoint: `PUT {URL_BASE}/api/books/{book_id}`
    *   Método HTTP: `PUT`
    *   Cabeçalhos: `Content-Type: application/json`, `Authorization: Token <SEU_TOKEN_ID>:<SEU_TOKEN_SECRET>`
    *   Corpo da Requisição (JSON). Campos comuns para atualização:
        *   `name` (string): Novo nome para o livro.
        *   `description` (string): Nova descrição para o livro.
        *   `tags` (array, opcional): Array de objetos de tag.

    *   Exemplo de Corpo da Requisição para atualizar nome e descrição:
        ```json
        {
          "name": "Título Atualizado do Livro",
          "description": "Esta é a nova descrição detalhada do livro."
        }
        ```

**Exemplo de Código (Python com a biblioteca `requests`):**

```python
import requests
import json

TOKEN_ID = "<SEU_TOKEN_ID>"  # Substituir de forma segura
TOKEN_SECRET = "<SEU_TOKEN_SECRET>"  # Substituir de forma segura
BASE_URL = "https://ajuda.digitalsys.com.br"
PAGE_ID_TO_UPDATE = 57  # Exemplo de ID da página

HEADERS = {
    "Authorization": f"Token {TOKEN_ID}:{TOKEN_SECRET}",
    "Content-Type": "application/json"
}

# Dados para atualizar a página
page_update_payload = {
    "name": "Ouvir Estrelas - Versão Atualizada",
    "markdown": "# Ouvir Estrelas (Atualizado)\n\n\\"Ora (direis) ouvir estrelas! Certo... (conteúdo completo do poema aqui)\\"\n\n_(Fonte: Brasil Escola - UOL)_\nRevisado em: DD/MM/AAAA",
    # "book_id": 5 # Opcional, se precisar mudar o livro
}

update_url = f"{BASE_URL}/api/pages/{PAGE_ID_TO_UPDATE}"

try:
    # Lembre-se de desabilitar a verificação SSL apenas se estritamente necessário e ciente dos riscos:
    # response = requests.put(update_url, headers=HEADERS, json=page_update_payload, timeout=30, verify=False)
    response = requests.put(update_url, headers=HEADERS, json=page_update_payload, timeout=30)
    response.raise_for_status()  # Levanta um erro para respostas 4xx/5xx

    updated_page_data = response.json()
    print(f"Página atualizada com sucesso: ID {updated_page_data.get(	"id	")}, Nome: {updated_page_data.get(	"name	")}")
    # print(f"URL da Página: {updated_page_data.get(	"url	")}") # A API pode não retornar a URL diretamente na atualização

except requests.exceptions.RequestException as e:
    print(f"Erro ao atualizar a página: {e}")
    if response is not None:
        print(f"Conteúdo da Resposta (Erro): {response.text}")

```

**Considerações Importantes para a IA:**

*   **Tratamento de Erros:** Sempre verifique os códigos de status HTTP das respostas. A API do BookStack retorna erros em formato JSON que podem ser parseados para obter mais detalhes.
*   **Rate Limiting:** Esteja ciente dos limites de taxa da API (padrão: 180 requisições por minuto) para evitar bloqueios.
*   **Formato do Conteúdo:** Certifique-se de que o conteúdo enviado (especialmente `markdown` ou `html`) está corretamente formatado.
*   **Confirmação do Usuário:** Para operações que alteram dados, considere implementar um passo de confirmação com o usuário antes de executar a chamada à API, especialmente se a IA não tiver certeza sobre o alvo ou o conteúdo da atualização.
*   **Verificação SSL:** No exemplo de código Python, a linha `verify=False` está comentada. Ela só deve ser usada em ambientes de desenvolvimento controlados se houver problemas com o certificado SSL do servidor e após o usuário confirmar explicitamente que entende os riscos. Para produção, o certificado SSL do servidor deve ser válido.

**Próximos Passos para a IA:**

1.  Solicite ao usuário o `ID da Página` ou `ID do Livro` que precisa ser atualizado, ou os nomes para que você possa pesquisá-los.
2.  Solicite o novo conteúdo ou as alterações específicas a serem aplicadas.
3.  Confirme os detalhes com o usuário antes de prosseguir com a chamada `PUT`.
4.  Execute a atualização e informe o usuário sobre o resultado (sucesso ou falha, com detalhes do erro se houver).