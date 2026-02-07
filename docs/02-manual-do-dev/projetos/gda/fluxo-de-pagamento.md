
# Fluxo de Pagamento

#### **Fluxo de Pagamento (Visão do Aluno)**

##### **Acesso ao módulo financeiro**

1. - O aluno entra no app e escolhe a opção “Pagamentos” ou “Financeiro”.
    - O sistema carrega as informações de mensalidades em aberto e/ou opções de planos disponíveis.
2. **Escolha do tipo de pagamento**
3. - **Opção A – Mensalidade:** aluno visualiza o valor do mês atual (e eventuais atrasados).
    - **Opção B – Plano:** aluno pode escolher pacotes (ex.: 3, 6 ou 12 meses) com desconto aplicado.
4. **Confirmação do pagamento**
5. - O aluno escolhe a forma de pagamento (cartão de crédito, PIX, boleto, carteira digital etc.).
    - O sistema mostra resumo: valor, período coberto, descontos, data de vencimento.
6. **Processamento do pagamento**
7. - O app redireciona para a integração com o gateway de pagamento 
    - O gateway retorna o status: aprovado, pendente, recusado.
8. **Retorno para o app**
9. - Em caso de **sucesso**: o sistema atualiza o status da mensalidade ou gera o crédito dos meses pagos.
    - Em caso de **falha**: o aluno recebe notificação e pode tentar novamente.
10. **Confirmação e recibo**
11. - O aluno recebe confirmação dentro do app.
    - No histórico financeiro, o pagamento aparece com status e período quitado.

#### **Pontos de Decisão Importantes**

- O aluno pode **parcelar** planos longos no cartão ou é sempre pagamento à vista?
- O desconto dos planos deve ser **fixo** (ex.: 10% em 6 meses) ou **configurável pelo admin**?
- O sistema deve suportar **renovação automática** (assinatura recorrente)?
- Haverá **multa e juros** em caso de atraso, e isso deve ser calculado automaticamente?  
      
    [![image.png](pathname:///docs-preview/img/fluxo-de-pagamento-1.png)](https://ajuda.digitalsys.com.br/uploads/images/gallery/2025-09/CXDcKkGEw4Vyv0OC-image.png)

