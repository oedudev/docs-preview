
# Visão Geral Técnica (README)

# DIS - DigitalSys Influencer System

#### ℹ️ Nota de Nomenclatura (Linguagem Ubíqua)

Para manter a consistência na comunicação, esteja ciente da dualidade de nomes:

- **DIS (DigitalSys Influencer System):** É o nome técnico/interno do projeto e do repositório.
- **CloseCast:** É o nome comercial provisório (Go-to-Market).
 
Embora o código e a infraestrutura usem `DIS`, telas e materiais de produto podem referenciar `CloseCast`. Tratamos como sinônimos até o lançamento oficial.

 Este documento detalha o funcionamento técnico do projeto DIS, um monorepo que centraliza a gestão de influenciadores da DigitalSys.

## Visão Geral da Arquitetura

O projeto foi migrado de Go para uma arquitetura moderna baseada em Python e JavaScript:

- **Backend:** Django 6.0 servindo uma API GraphQL (Strawberry). Foca em robustez e facilidade de manutenção.
- **Frontend:** SvelteKit 5, oferecendo alta performance e renderização híbrida (SSR/CSR).
- **Infraestrutura:** Containerizada com Docker, orquestrada via Helm e Skaffold para ambientes Kubernetes.
 
## Estrutura do Repositório

O código está organizado como um monorepo para facilitar a gestão de dependências e deploys unificados:

 
<table class="table table-bordered" id="bkmrk-diret%C3%B3rio-prop%C3%B3sito-"> 
<thead> 
<tr> 
<th>Diretório</th>
 
<th>Propósito</th>
 </tr>
 </thead>
 
<tbody> 
<tr> 
<td>`backend/django`</td>
 
<td>Núcleo da API, regras de negócio e persistência de dados.</td>
 </tr>
 
<tr> 
<td>`ui/web/app`</td>
 
<td>Aplicação web para usuários finais e adminstradores.</td>
 </tr>
 
<tr> 
<td>`infra/`</td>
 
<td>Manifestos Kubernetes (Helm) e pipelines Skaffold.</td>
 </tr>
 
<tr> 
<td>`conductor/`</td>
 
<td>Registro de decisões de arquitetura (ADRs) e histórico de migração.</td>
 </tr>
 </tbody>
 </table>

## Como Executar (Desenvolvimento)

O projeto utiliza a ferramenta **Task** para padronizar comandos. O fluxo para novos desenvolvedores é:

1. Instalar pré-requisitos: Docker, Python 3.12+, Node 20+ e Task.
2. Configurar ambiente: `task setup`
3. Rodar aplicação: `task dev` (Sobe Backend na 4100 e Frontend na 4200).
 
## Integração Contínua (CI/CD)

Os workflows do GitHub Actions garantem a qualidade:

- **Validate:** Roda em todo PR. Executa testes (pytest) e linters (ruff).
- **Deploy:** Automatizado via Helm para os clusters de Dev, Staging e Prod.
 
*Atualizado por Clóvis em 30/01/2026 com notas de nomenclatura.*