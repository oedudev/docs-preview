
# BDD Registro de movimentação e autenticação na blockchain

**Funcionalidade:** Registro de Proveniência de Produto em Blockchain  
  
Como um gestor da plataforma UpLuxo,   
Desejo garantir a rastreabilidade e a imutabilidade do histórico de movimentações dos Materiais de Reuso utilizando a Blockchain,   
Para que possamos oferecer transparência, segurança e auditabilidade sobre o ciclo de vida dos materiais para nossos clientes e auditores.

 **Cenário:** Registro da Primeira Movimentação de um Lote Novo

 **Dado** que um novo Lote de Material de Reuso é cadastrado no sistema e ainda não possui movimentações  
 **Quando** a primeira movimentação é registrada para este lote  
 **Então** o sistema deve gerar uma assinatura digital (hash) baseada unicamente nesta primeira movimentação  
  **E** deve iniciar o processo de registro desta assinatura na Blockchain.  
  
 **Cenário:** Geração da Assinatura Digital para uma Nova Movimentação  
  
 **Dado** que um Lote de Material de Reuso já possui um registro em sistema  
 **Quando** uma nova movimentação é registrada para este lote  
 **Então** o sistema deve consolidar todo o histórico de movimentação em um registro único  
 **E** deve gerar a partir dele uma assinatura digital única (hash) que representa a totalidade deste histórico consolidado.  
  
 **Cenário:** Tentativa de Registrar Movimentação para um Lote Inexistente  
  
 **Dado** que um gestor está na tela de registro de movimentação de lote  
 **Quando** ele informa um ID de um Lote de Material de Reuso que não existe no banco de dados  
 **E** tenta submeter o registro da movimentação  
 **Então** o sistema deve rejeitar a operação  
 **E** deve exibir uma mensagem de erro informando que "O lote especificado é inválido ou não foi encontrado".

 **Cenário**: Registro Bem-Sucedido da Assinatura Digital na Blockchain  
  
 **Dado** que uma assinatura digital (hash) foi gerada para o histórico completo de um lote  
 **Quando** esta assinatura é enviada para registro no Smart Contract da Blockchain  
 **E** a transação na Blockchain é confirmada com sucesso  
 **Então** o ID da Transação resultante deve ser salvo  
 **E** associado ao registro da movimentação no banco de dados local  
  
 **Cenário:** Falha e Retentativa de Registro na Blockchain  
  
 **Dado** que uma assinatura digital (hash) foi gerada para o histórico completo de um lote  
 **Quando** o envio desta assinatura para a Blockchain falha por um erro de conexão ou recusa da transação  
 **Então** a movimentação deve ser marcada com o status "Pendente de Sincronização"  
 **E** o sistema deve tentar reenviar o registro para a Blockchain automaticamente em intervalos definidos  
  
 **Cenário:** Tentativas de Reenvio Excedem o Limite Máximo  
  
 **Dado** que uma movimentação está marcada com o status "Pendente de Sincronização"  
 **E** o sistema já tentou reenviar o registro para a Blockchain o número máximo de vezes permitido  
 **Quando** a última tentativa de reenvio falha  
 **Então** o status da movimentação deve ser permanentemente alterado para "Falha de Sincronização"  
 **E** uma notificação de erro crítico deve ser enviada aos administradores para investigação e intervenção manual  
  
 **Cenário:** Validação de Integridade via Blockchain bem-sucedida  
  
 **Dado** que uma movimentação de um lote foi registrada na Blockchain com uma assinatura digital conhecida  
 **E** que não tenha havido qualquer adulteração no registro de movimentações do lote  
 **Quando** um auditor solicita a verificação da integridade do histórico daquele lote  
 **Então** o sistema deve ser capaz de recalcular a assinatura digital a partir do histórico armazenado localmente  
 **E** a assinatura recalculada deve ser idêntica àquela registrada permanentemente na Blockchain  
  
 **Cenário:** Geração de assinatura digital divergente para lote adulterado  
  
 **Dado** que uma movimentação de um lote foi registrada na Blockchain com uma assinatura digital conhecida  
 **E** tenha havido qualquer adulteração no registro de movimentações do lote  
 **Quando** um auditor solicita a verificação da integridade do histórico daquele lote  
 **Então** o sistema deve ser capaz de recalcular a assinatura digital a partir do histórico armazenado localmente  
 **E** a assinatura recalculada deve ser divergente àquela registrada permanentemente na Blockchain  
  
 **Cenário:** Falha na Verificação de Integridade via Blockchain (Hash Divergente)

 **Dado** que uma movimentação de um lote foi registrada na Blockchain com uma assinatura digital conhecida  
 **Quando** um auditor solicita a verificação da integridade do histórico daquele lote  
 **E** a assinatura recalculada a partir do histórico local é diferente daquela registrada na Blockchain  
 **Então** o sistema deve reportar uma falha crítica de integridade para aquele lote  
 **E** o histórico do lote deve ser marcado como "Comprometido"  
 **E** um alerta de segurança deve ser gerado para investigação imediata