
# Padrão de Arquitetura & Atomic Design

# 🚀 Manual de Desenvolvimento: Arquitetura e Atomic Design

Este guia estabelece os padrões de desenvolvimento para garantir que nossa interface seja escalável, testável e fácil de manter. **Todos os desenvolvedores devem seguir estas diretrizes.**

## 🧠 2. Gestão de Estado e "Injeção de Cérebro"

Para manter os componentes reutilizáveis, seguimos o princípio do desacoplamento:

- **Componentes Burros (Atoms/Molecules/Organisms):** Não conhecem Redux, Context API ou Axios. Eles recebem dados via `props` e comunicam ações via `callbacks` (ex: `onClick`).
- **Componentes Inteligentes (Pages/Containers):** São os únicos autorizados a acessar o **Estado Global** e realizar chamadas de API. Eles "injetam" a lógica nos componentes visuais.

## 🧪 4. Estratégia de Testes

1. **Unitários (Jest/Testing Library):** Foco em Átomos e Moléculas (comportamento de clique, renderização de props).
2. **Integração:** Foco em Organismos e Páginas (fluxo entre múltiplos componentes).
3. **Visual:** Use Snapshots para garantir que mudanças no CSS global não alteraram componentes estáveis.

## 🛠️ Resumo: Onde colocar meu código?

- Se é um **HTML básico ou estilo puro**: `src/components/atoms`
- Se é um **conjunto de inputs com validação visual**: `src/components/molecules`
- Se define o **posicionamento da Sidebar e Main Content**: `src/components/templates`
- Se faz um **useEffect para buscar dados**: `src/pages`

