
# 4. Execução dos Testes

### **Durante a execução do teste:**

O QA deve validar:

- Cenários principais (happy path)
- Cenários alternativos
- Cenários negativos
- Possíveis impactos em outras áreas (testes exploratórios)
- Casos de uso citados no card ou solicitados pelo solicitante

###   
**4.1. Evidências Obrigatórias**

Durante todo o teste, **é obrigatório anexar prints** em cada cenário relevante, incluindo:

- Antes da alteração
- Depois da alteração
- Exceções ou erros
- Mensagens de sistema

### **4.2. Comentários no Card**

  
O QA deve registrar nos comentários do card filho **IN QA**:

- Como o teste foi realizado
- Quais cenários foram testados
- Quais dados foram utilizados
- Qual resultado foi observado
- Evidências anexadas

## **4.3 Resultado do Teste**

**5.1. Caso esteja OK (Teste Aprovado)**

Se o teste foi bem-sucedido e o bug/tarefa foi corrigido ou implementado conforme solicitado:

1. **Enviar o card filho “IN QA” para Done**
2. O **card pai** deve ser movido para **Waiting Regressive**

#### **Waiting Regressive**

Nesta coluna, o card aguarda:

- A escrita dos casos de teste no **TestLink**

Após criar os casos de teste:

3. Mover o **card pai para Done**

### **4.4 Caso NÃO esteja OK (Teste Reprovado)**

Quando o QA encontra um problema:

1. **Criar um novo card filho dentro do card pai com o nome:**
    - **TO FIX**
2. Dentro do card TO FIX, registrar:
    - Detalhamento claro do bug encontrado
    - Passo a passo para reproduzir
    - Cenário onde foi detectado
    - Ambiente utilizado
    - Prints obrigatórios mostrando o erro
    - A definição do que era esperado × o que ocorreu
3. Mover o **card pai** para a coluna **To Fix**, para que o desenvolvedor possa corrigir.

Após a correção do dev:

- O card retorna novamente para **Waiting QA**, reiniciando o ciclo.

## **4.5 Acompanhamento e Rastreabilidade**

Para garantir controle:

- Cada bug encontrado deve estar documentado no card TO FIX
- Todos os testes executados devem estar no card filho IN QA
- Evidências são obrigatórias nos dois tipos de cards
- A mudança entre colunas deve refletir exatamente o status real do trabalho

## **4.6 Conclusão**

O processo descrito garante:

- Padronização da atuação do QA
- Rastreabilidade completa do ciclo
- Documentação clara para desenvolvimento e gestão
- Garantia de qualidade e evidências consistentes
- Integração entre QA, Dev e gestão via Linear + TestLink