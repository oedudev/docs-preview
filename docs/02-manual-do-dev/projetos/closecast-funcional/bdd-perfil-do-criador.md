
# BDD perfil do criador

##### Criador mantem seu perfil (Informações básicas)

**Cenário:** Visualizar informações gerais

**Dado** que eu seja um usuário criador de conteúdo

**Quando** eu acessar meu perfil

**Então** devo iniciar na aba "Informações de perfil"

**E** devo ver todas as informações conforme preenchi previamente

**Cenário:** Alterar foto de perfil  
  
**Dado** que eu seja um usuário criador

**E** que eu esteja na aba "Informações de perfil"

**Quando** eu clicar em Mudar foto

**E** realizar upload de uma foto

**Então** a foto de perfil deve ser alterada

**E** a mudança deve ser visível a outros usuários

**Cenário**: Alterar links de mídias sociais

**Dado** que eu seja um usuário criador

**E** que eu esteja na aba "Informações de perfil"

**E** que eu edite os dados de "Links e mídias sociais"

**Quando** eu clicar em "Salvar alterações"

**Então** as informações devem persistir nos registros do banco de dados

**E** as alterações devem ser visíveis a outros usuários

**Cenário:** Editar meta mensal

**Dado** que eu seja um usuário criador

**E** que eu esteja na aba "Preços de Disponibilidade"

**E** que eu edite o valor do campo "Valor da Meta"

**Quando** eu clicar em "Atualizar"

**Então** o valor da minha meta mensal deve ser atualizada para o valor inserido

**E** todos os gráficos/elementos devem ser alterados para refletir o novo valor inserido

**Cenário:** Editar tempos de entrega

**Dado** que eu seja um usuário criador

**E** que eu esteja na aba "Preços de Disponibilidade"

**E** que eu edite o valores dos campos de "Tempos de Entrega"

**Quando** eu clicar em "Atualizar"

**Então** os valores dos meus tempos de entrega devem ser atualizados para o valor inserido

##### Criador mantem seu perfil (portifílio)

**Cenário:** realizar upload de vídeo/fotos

**Dado** que eu seja um usuário criador

**E** que eu esteja na aba "Portifólio"

**E** que eu tenha feito upload de uma foto/vídeo

**Quando** eu clicar em "Enviar vídeo/foto"

**Então** o vídeo/foto deve ficar disponível para visualização do meu protifílio

**E** deve ser acessível por qualquer usuário

**Cenário:** Criador edita configurações - Privacidade

**Dado** que eu seja um usuário criador

**E** que eu esteja na página "configurações"

**Quando** eu editar alguma opção de privacidade

**Então** as informações devem ser salvas

**E** as alterações que realizei devem ser refletidas para outros usuários