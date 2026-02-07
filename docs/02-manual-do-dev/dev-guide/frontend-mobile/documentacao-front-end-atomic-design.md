
# Documentação Front-End - Atomic Design

Este documento descreve a estrutura de componentes do front-end do projeto e-sus utilizando a metodologia Atomic Design para organizar e manter a escalabilidade e reutilização dos componentes.

#### **1 Componente**

#### **1.1 Componente: Input model 1**

**Tipo:** Molécula

**Descrição:**  
Componente de campo de entrada de dados que pode ser configurado via props para se adequar a diferentes contextos do projeto.

Props disponíveis:

<colgroup><col></col><col></col><col></col></colgroup>

#### Prop

#### Tipo

#### Descrição

- `label`

- string

- Texto exibido acima do campo como label.

- `placeholder`

- string

- Texto de sugestão dentro do campo.

- `icone`

- string

- Ícone exibido à esquerda do campo.

- `type`

- string

- Tipo de input. Se for 

`"password"`

, o campo se comporta como senha e exibe ícone à direita para mostrar/ocultar o valor.

[![image.png](assets/documentacao-front-end-atomic-design-1.png)](https://ajuda.digitalsys.com.br/uploads/images/gallery/2025-09/3lJ5VZG3hGTlab9p-image.png)

#### **1.2 Componente: Button model 1**

**Tipo:** Molécula

**Descrição:**  
Componente de Botão que pode ser configurado via props para se adequar a diferentes contextos do projeto.

<colgroup><col></col><col></col><col style="width: 320px;"></col></colgroup>

#### 

#### Tipo

#### Descrição

- `label`

- string

- Texto exibido no centro do botão.

- `icone`

- string

- Ícone exibido à esquerda do campo.

- `disabled`

- boolean

- Variável booleana para desabilitar/habilitar botão

[![image.png](assets/documentacao-front-end-atomic-design-2.png)](https://ajuda.digitalsys.com.br/uploads/images/gallery/2025-09/jleCTabRZF2eJ9XW-image.png)

#### **2. Requisições nos componentes**

**Problema:** Atualmente algumas requisições à API estão sendo feitas diretamente dentro de componentes. Isso fere o princípio de separação de responsabilidades do Atomic Design.

**Impacto:**

- Torna os componentes menos reutilizáveis, já que ficam acoplados a regras de negócio.
- Dificulta testes, manutenção e evolução do projeto.
- Quebra a hierarquia de responsabilidades esperada.

**Correção Recomendada:**

- Centralizar todas as requisições na Página.
- A Página deve buscar/enviar dados para a API e repassar os resultados via props para o Template e componentes filhos.
- Os componentes (organismos, moléculas e átomos) devem apenas exibir dados recebidos ou disparar eventos que a Página irá tratar.

Componentes Identificados com Requisições:

**atoms:**

- `technical-decision-table.vue`
- `change-status-modal.vue`
- `banner-description-MR.vue`

**moleculas:**

- `form-regulation.vue`
- `form-regulation-edit.vue`
- `form-patient-edit.vue`
- `form-occurrence-edit.vue`
- `form-conclusion-edit.vue`
- `form-basic-data-edit.vue`
- `banner-description-fleet.vue`
- `admin-users-table.vue`
- `admin-supply-table.vue`
- `admin-occurance-reason-table.vue`
- `admin-mobile-unit-table.vue`
- `admin-health-units-destination.vue`
- `admin-health-unit-table.vue`
- `admin-enquiry-table.vue`
- `admin-health-unit-table.vue`
- `admin-discriminator-table.vue`
- `admin-city-table.vue`
- `admin-health-unit-table.vue`
- `admin-health-unit-table.vue`
- `admin-health-unit-table.vue`

**organisms:**

- `select-occurrence-team.vue`
- `occurance-confirmation.vue`
- `fleet-incident-display.vue`
- `banner-operation.vue`

**templates:**

- `FleetOccurrence.vue`