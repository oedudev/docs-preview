
# SvelteKit: Erro de build no Docker (Adapter Mismatch)

# SvelteKit: Erro de build no Docker (Adapter Mismatch)

## O Problema
O build do frontend falha no ambiente Docker de produção, embora funcione localmente ou em outros ambientes.

## Causa Raiz
Conflito de adapters do SvelteKit.
- O projeto estava configurado fixo com `adapter-static` (para ser servido pelo Django/Backend).
- O ambiente Docker de produção tentava executar como servidor Node.js puro, exigindo `adapter-node`.

## Solução
Implementação de **Adapter Dinâmico** no `svelte.config.js`.

O código agora verifica a variável de ambiente `USE_NODE_ADAPTER`:

```javascript
// svelte.config.js
import adapterStatic from '\@sveltejs/adapter-static';
import adapterNode from '\@sveltejs/adapter-node';

const useNode = process.env.USE_NODE_ADAPTER === 'true';

const config = {
    kit: {
        adapter: useNode ? adapterNode() : adapterStatic(),
        // ...
    }
};

export default config;
```

**Configuração do Docker:**
Certifique-se de que o Dockerfile ou docker-compose de produção define a variável:
`ENV USE_NODE_ADAPTER=true`