
# Mapa de Rotas

  → Autenticado.

  → Autenticado como usuário.

  → Autenticado como criador.

#### Autenticação

/auth/login  → Login.

/auth/register  → Central de registro.

/auth/register/user   → Registro de usuários comum.

/auth/register/creator  → Registro de criadores.

#### Procurar criadores

/      → Landing Page.

/creators     → Lista de criadores.

/creators/:id     → Perfil do criador para um usuário.

#### Usuário

/user-profile/:id    → Perfil do usuário para um usuário.

#### Criador

/creator-profile/:id   → Perfil do criador para um criador.

/creator-profile/:id/sells   → Dashboard de vendas do criador.

/creator-profile/:id/proposals  → Propostas recebidas.

#### Notificações

/notifications    → Lista de notificações.

/notifications/:id    → Mostra a notificação.

#### Vídeos

/request-video/:creator-id  → Pedir vídeo.

/request-photo/:creator-id  → Pedir foto.

/video/:id     → Mostra o vídeo feito.

/video/:id/rate    → Avaliar o vídeo criado.

/video/:id/request-change   → Pedir mudança para o vídeo.

#### Pagamento

/payment    → Pagamento

O pagamento vai saber pelo o que está sendo pago através de um carrinho que vai ser salvo através de um stateManager, como o ZuStand.

#### Solicitações de alteração nos vídeos

/request-change/:id   → Pedido de mudança.

#### Mimos

/caress/:id     → Tela do Mimo.

Se estiver logado como criador que recebeu o mimo, mostra a tela de mimo recebido, se como o usuário, mostra a tela de mimo enviado.

#### Denúncia

/customer-complaint   → Cliente denunciar um criador.

/creator-complaint   → Criador denunciar cliente.

#### Contato

/contact     → Contato.