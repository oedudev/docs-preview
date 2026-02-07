
# Desenvolvimento FrontEnd (NextJS e NuxtJS)

#### 1. **Estrutura de Pastas e Componentes**

- **Componentização:** Utilize componentes pequenos, reutilizáveis e de responsabilidade única. Evite criar componentes que façam mais de uma coisa.
- **Estrutura de Pastas:** Organize as pastas de forma clara. Separe componentes, páginas, assets, layouts e stores (se aplicável).
- Exemplo de estrutura:

```
├── components/
├── pages/
├── assets/
├── layouts/
├── store/ (para NuxtJS)
├── middleware/
```

#### 2. **Padrão de Nomenclatura**

- **Arquivos e pastas:** Use nomes em **kebab-case** para arquivos e pastas (ex: `my-component.vue`).
- **Componentes:** Use nomes claros e descritivos para componentes (ex: `BaseButton.vue`, `UserCard.vue`).
- **Classes CSS:** Utilize o padrão BEM (Block Element Modifier) para nomeação de classes CSS (ex: `.block__element--modifier`).

#### 3. **Uso de CSS**

- **CSS modular:** Prefira o uso de CSS Modules ou SCSS, principalmente em projetos NextJS.
- **Tailwind CSS:** Para projetos que utilizam Tailwind, agrupe classes quando possível e use o `\@apply` para evitar redundâncias.
- **Estilos Globais:** Evite o uso de estilos globais extensivos, a não ser que sejam realmente necessários (ex: reset.css, normalize.css).

#### 4. **Boas Práticas de Vue/React**

- **Estado Global:** Em Nuxt, use o `Vuex` apenas quando necessário. Evite centralizar tudo no estado global.
- **Hooks e Lifecycle Methods:** Em Next.js, organize os hooks React de forma que o código seja limpo e fácil de entender. Prefira `useEffect` e `useState` para a maioria das operações.
- **Server-Side Rendering (SSR):** Em ambos os frameworks, tenha cuidado com o uso de recursos que dependem do lado do cliente em páginas SSR, usando `process.client` (Nuxt) ou `typeof window !== 'undefined'` (Next.js).

#### 5. **Carregamento e Performance**

- **Lazy loading:** Utilize o lazy loading para componentes e imagens pesadas.
- **Code splitting:** Aproveite o suporte nativo de code splitting para otimizar o carregamento das páginas.
- **Imagem otimizada:** Use o componente `<nuxt-img>` (NuxtJS) ou o `` do Next.js para servir imagens otimizadas.

#### 6. **Boas Práticas de SEO**

- **Meta Tags:** Certifique-se de configurar corretamente as meta tags em todas as páginas.
    - Nuxt: Utilize `head()` em páginas e componentes.
    - Next.js: Use o `next/head` para definir meta tags.
- **Sitemaps:** Gere sitemaps automaticamente para facilitar a indexação do site.
- **URLs limpas:** Use URLs amigáveis e evite parâmetros longos ou confusos.

#### 7. **Validação e Segurança**

- **Sanitização de Inputs:** Sempre sanitize os inputs do usuário para evitar XSS (Cross-Site Scripting).
- **Autenticação:** Utilize soluções como o `\@nuxt/auth` (Nuxt) ou `next-auth` (Next.js) para gerenciar autenticação de forma segura.
- **CSRF e CORS:** Certifique-se de configurar corretamente as políticas de segurança de Cross-Site Request Forgery (CSRF) e Cross-Origin Resource Sharing (CORS).

#### 8. **Boas Práticas de Testes**

- <s>**Testes Unitários:**</s><s> Crie testes para componentes utilizando frameworks como </s>`Jest`<s> ou </s>`Testing Library`<s>.</s>
- **Testes de Integração:** Para projetos em Nuxt, use o Cypress para testar fluxos de navegação. Para Next.js, também pode-se usar o Cypress ou o Playwright.

#### 9. **Versionamento e Git**

- **Commits semânticos:** Siga convenções como Conventional Commits para manter o histórico claro. Exemplos:
    - `feat: add new login page`
    - `fix: resolve issue with user token validation`
- **Branches organizadas:** Sempre utilize um padrão de nomeação para branches, conforme documento de padronização de branches

#### 10. **Configurações de Build e Deploy**

- **Environment Variables:** Mantenha variáveis sensíveis fora do código e utilize variáveis de ambiente com `.env` corretamente configurados.
- **Deploy Automatizado:** Configure deploy automatizado usando plataformas como Vercel (para Next.js) ou Netlify (para NuxtJS).

#### 11. **Atomic Design**

- O **Atomic Design** ajuda a organizar componentes em níveis hierárquicos, promovendo a reutilização e escalabilidade:
    - **Átomos:** Componentes simples e indivisíveis.
    - **Moléculas:** Combinações de átomos que formam unidades funcionais.
    - **Organismos:** Estruturas maiores que compõem partes da interface.
    - **Templates:** Layouts que combinam diferentes organismos.
    - **Páginas:** Instâncias completas com conteúdo real.
- **Boas práticas:**
    - Organize a estrutura de pastas do projeto com base nos níveis do Atomic Design:
    
    ```
    ├── components/
        ├── atoms/
        ├── molecules/
        ├── organisms/
        ├── templates/
        ├── pages/
    ```

#### 12. **Geração de Imagens Docker com Conteúdo Estático**

- **Padrão:** Sempre gere imagens Docker com o conteúdo estático para evitar o uso do motor do NuxtJS/NextJS em produção.
- **Dockerfile para NuxtJS:**

```
# Etapa de build
FROM node:18-alpine AS builder
WORKDIR /app
COPY . .
RUN npm install
RUN npm run generate

# Etapa de deploy
FROM nginx:alpine
COPY --from=builder /app/dist /usr/share/nginx/html
EXPOSE 80
```

- **Dockerfile para Next.js**

```
# Etapa de build
FROM node:18-alpine AS builder
WORKDIR /app
COPY . .
RUN npm install
RUN npm run build
RUN npm run export

# Etapa de deploy
FROM nginx:alpine
COPY --from=builder /app/out /usr/share/nginx/html
EXPOSE 80
```

- **Boas práticas:**
    - Utilize **multi-stage builds** para otimizar o tamanho da imagem.
    - Sirva o conteúdo estático via NGINX para obter melhor performance, segurança e menor overhead.