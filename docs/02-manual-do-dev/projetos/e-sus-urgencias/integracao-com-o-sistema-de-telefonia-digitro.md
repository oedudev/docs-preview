
# Integração com o sistema de Telefonia (Digitro)

Este documento descreve a integração do sistema de telefonia com o frontend da aplicação, realizada em parceria com a empresa **Digitro**. O objetivo principal dessa integração é permitir que os usuários efetuem e recebam chamadas diretamente pela interface web.

A implementação foi feita utilizando a biblioteca **jSSIP**, um cliente **SIP (Session Initiation Protocol)** desenvolvido em JavaScript que opera sobre **WebRTC**. Essa biblioteca possibilita a comunicação em tempo real (voz e vídeo) diretamente pelo navegador, sem a necessidade de softwares externos.

#### **Principais aspectos da integração**

- **Protocolo SIP:** utilizado para o controle de sessão e estabelecimento das chamadas.
- **WebRTC:** tecnologia base para transmissão de áudio via navegador, garantindo baixa latência e segurança.
- **Autenticação e Registro:** o frontend realiza o registro SIP com as credenciais fornecidas pela Digitro, permitindo o gerenciamento das extensões e status de disponibilidade.
- **Eventos de Chamada:** o jSSIP gerencia eventos como chamada recebida, em andamento, encerrada ou perdida, permitindo ao frontend atualizar a interface conforme o estado da ligação.
- **Interface de Usuário:** foram adicionados componentes para discagem, exibição de número, controle de microfone, e encerramento de chamada.

### **Variáveis de Ambiente**

O sistema de telefonia da Digitro utiliza um canal de comunicação baseado em SSE (Server-Sent Events) para o envio de eventos em tempo real, como chamadas recebidas, encerramentos e alterações de estado dos agentes.

Cada agente é vinculado a um channel\_id, definido a partir do seu user\_id no sistema. Esse canal é aberto no frontend por meio do endpoint ***PHONE\_SYSTEM\_OPEN\_CHANNEL***.

Após a abertura, o canal é assinado através do endpoint ***PHONE\_SYSTEM\_SUBSCRIBE\_CHANNEL***, permitindo o recebimento dos eventos relacionados especificamente àquele agente.

Durante o processo de inicialização (initPhoneSystemService), o sistema verifica se já existe uma assinatura ativa para o mesmo canal antes de criar uma nova. Caso exista, a assinatura é reutilizada.

Essa estratégia é fundamental, pois a Digitro impõe limites de licenças e de canais ativos. O reaproveitamento de assinaturas evita exceder esse limite, garantindo a estabilidade da integração e prevenindo erros como “canal duplicado” ou “assinaturas excedidas”.

**Além disso, todas as ações de telefonia (como atender, transferir ou encerrar chamadas) devem ser realizadas exclusivamente por meio dos endpoints oficiais da Digitro.**

**Embora a biblioteca jSSIP ofereça funções que poderiam executar algumas dessas operações diretamente, não é recomendado utilizá-las isoladamente, pois o sistema depende das informações retornadas pelos endpoints (como o call\_id) para identificar chamadas e associar suas respectivas gravações posteriormente.**

##### **Lista de Eventos**

Durante o processo de autenticação e registro do agente no sistema de telefonia, é utilizada uma credencial específica chamada ***webrtc\_password***.

Essa senha é responsável por autenticar o agente na camada SIP/WebRTC, permitindo que a biblioteca jSSIP estabeleça a sessão de comunicação com o servidor da Digitro.

No backend, o valor do webrtc\_password é definido a partir da variável de ambiente **WEBRTC\_DEFAULT\_PASSWORD e não é exposto diretamente ao frontend.**

Durante a criação do usuário de telefonia, o backend executa as seguintes etapas:

1. Recupera o valor de WEBRTC\_DEFAULT\_PASSWORD.
2. Gera um IV (vetor de inicialização) aleatório para criptografia.
3. Criptografa tanto a senha principal (senha do próprio usuário que vai logar no sistema de telefonia, a mesma que ela usa no Interact MultiAgent) quanto o webrtc\_password (senha para se conectar a máquina da Digitro).
4. Armazena ambas as senhas de forma segura no banco de dados.

Quando o frontend solicita as credenciais do agente, o backend realiza a descriptografia e retorna apenas as informações necessárias para o registro SIP.

**A rota que retorna as credenciais descriptografadas (GET /:id/credentials) utiliza os guardas AuthGuard e OwnerGuard, garantindo que cada usuário só consiga visualizar as próprias credenciais.** Mesmo que outro agente tente acessar o endpoint de outro usuário (exemplo: usuário com id 1 tenta acessar /23/credentials), o sistema retorna 403 - Acesso negado, preservando a confidencialidade das senhas.

Essa abordagem garante que nenhuma senha sensível fique exposta no frontend e que todo o processo de autenticação WebRTC siga boas práticas de segurança, mantendo a integridade das conexões e a confidencialidade das credenciais.

### **Referências**

**Edson Machado (Digitro) - Integração:** (48) 9628-0268

**Rodrigo (Digitro) - Integração:** (48) 3281-7344

**Lucas Ribeiro (Digitro) - Atendimento ao cliente (normalmente auxilia nas configurações de cadastro de novos usuários, criação de ramal interno específico para um tipo de perfil e basicamente tudo que refere-se ao Interact Manager):** (85) 9842-9746

**Sidney (DataSUS) - T.I. alocado dentro de onde o SAMU atende em Fortaleza:** (85) 9112-0254