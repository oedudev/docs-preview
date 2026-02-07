
# Padrões de Nomenclatura de Branches

As branches de desenvolvimento devem seguir um padrão que facilite a rastreabilidade das tarefas e a organização do fluxo de trabalho. Para garantir isso, todas as branches devem ser nomeadas de acordo com as seguintes diretrizes:

#### Diretrizes para nomeação de branches:

1. **ID da tarefa**: Cada branch deve começar com o ID da tarefa associado à funcionalidade ou correção que está sendo desenvolvida. Esse ID deve ser o mesmo utilizado na ferramenta de gerenciamento de tarefas.
2. **Breve descrição**: Após o ID da tarefa, adicione uma breve descrição da tarefa em questão. A descrição deve ser clara e concisa, separada do ID por uma barra `/`.
3. **Idioma**: Tanto o nome da branch quanto a descrição da tarefa **devem sempre estar em inglês** para manter a consistência e facilitar a colaboração com equipes internacionais.
4. **Exemplos de nomes de branch aceitáveis**:
    - `DS-450/reset-password` – Para uma tarefa de redefinição de senha associada à tarefa DS-450.
    - `DS-430/user-register-form` – Para o desenvolvimento de um formulário de registro de usuários associado à tarefa DS-430.
5. **Nomes de branch não aceitáveis**:
    - `reset-password`
    - `new-feature`
    - `DS-450/redefinir-senha` (devido ao uso de outro idioma)
6. **Recomendações adicionais**:
    - Use sempre letras minúsculas e `-` (hífen) para separar palavras na descrição da tarefa.
    - Evite descrições genéricas ou vagas. O nome da branch deve permitir que outros desenvolvedores identifiquem facilmente o propósito da branch.
    - Branches que envolvem múltiplas funcionalidades ou correções devem ser evitadas. Cada branch deve se concentrar em uma única tarefa.