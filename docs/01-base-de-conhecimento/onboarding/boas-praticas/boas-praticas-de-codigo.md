
# Boas Práticas de Código

Escrever um código limpo, claro e bem documentado é essencial para a manutenção, colaboração e evolução de qualquer projeto de software. As diretrizes abaixo ajudarão a manter o código legível e organizado, além de proporcionar uma comunicação clara entre os membros da equipe por meio de comentários relevantes.

#### 1. **Escreva código claro e autoexplicativo**

- O código deve ser fácil de entender por si só, sem a necessidade de comentários explicando o que ele faz. Nomes de variáveis, funções e classes devem ser descritivos e comunicar a intenção do que representam.
    - **Exemplo bom**: `calculateTotalAmount()`
    - **Exemplo ruim**: `calcAmt()`

#### 2. **Use convenções de nomenclatura consistentes**

- Siga as convenções de nomenclatura do idioma de programação que você está usando. Utilize um padrão consistente para o projeto inteiro, como o camelCase para variáveis e funções em linguagens como JavaScript, e o snake\_case em Python.
    - **Exemplo bom**: `userRegistrationForm` (camelCase)
    - **Exemplo ruim**: `user_registration_form` (mistura de convenções)

#### 3. **Mantenha funções pequenas e com responsabilidades únicas**

- Funções ou métodos devem ser pequenos e focados em uma única tarefa. Se uma função estiver fazendo muitas coisas diferentes, considere dividi-la em funções menores.
    - **Exemplo bom**: Uma função `sendEmail()` que apenas cuida do envio de e-mails.
    - **Exemplo ruim**: Uma função `handleUserAction()` que envia e-mails, salva dados no banco e atualiza a interface.

#### 4. **Evite duplicação de código**

- Não repita blocos de código em diferentes partes do sistema. Se você identificar duplicação, extraia o código repetido para uma função ou módulo reutilizável.
    - **Exemplo bom**: Uma função `calculateTax()` sendo chamada em diferentes partes do sistema.
    - **Exemplo ruim**: Cálculo de imposto repetido manualmente em várias funções.

#### 5. **Use comentários para explicar "por que", não "o que"**

- Comentários devem ser usados para explicar o **motivo** de uma decisão de design ou implementação, e não o que o código está fazendo. O código deve ser claro o suficiente para que "o que" está sendo feito seja óbvio.
    - **Exemplo bom**: `// Usamos um cache para evitar recalcular o valor a cada requisição.`
    - **Exemplo ruim**: `// Calcula o valor total.`

#### 6. **Comente somente quando necessário**

- Evite comentários excessivos ou desnecessários. Comentários devem ser usados com parcimônia para fornecer informações que o código não pode expressar diretamente.
    - **Exemplo bom**: Comentários que explicam hacks temporários ou decisões técnicas incomuns.
    - **Exemplo ruim**: Comentários óbvios ou redundantes, como `// Incrementa a variável`.

#### 7. **Mantenha o código simples (KISS: Keep It Simple, Stupid)**

- Escreva código simples e direto, evitando soluções complexas ou "inteligentes" que são difíceis de entender e manter. Sempre que possível, prefira a solução mais simples.
    - **Exemplo bom**: Código que resolve o problema de forma direta e compreensível.
    - **Exemplo ruim**: Uso excessivo de metaprogramação ou padrões complicados quando uma solução simples seria suficiente.

#### 8. **Evite comentários no estilo "To-Do" sem ações**

- Comentários como `// TODO` ou `// Fix this later` devem ser evitados sem uma clara atribuição ou plano de ação. Se for necessário incluir um "TODO", crie uma tarefa no sistema de gerenciamento de projetos e adicione um comentário com a referência ao ticket.
    - **Exemplo bom**: `// TODO: Revisar o algoritmo quando a API X estiver disponível. Ticket #123`
    - **Exemplo ruim**: `// TODO: Corrigir isso mais tarde.`

#### 9. **Documente as funções públicas e APIs**

- Funções públicas ou que fazem parte de uma API devem ser sempre documentadas com comentários de cabeçalho explicando seus parâmetros, retornos e possíveis exceções.
    - **Exemplo bom**:

```python
def calculate_total(price, tax_rate):
    """
    Calcula o valor total incluindo impostos.

    :param price: O preço do item.
    :param tax_rate: A taxa de imposto a ser aplicada.
    :return: O valor total com impostos.
    """
```

- **Exemplo ruim**: Funções públicas sem nenhuma documentação.

#### 10. **Seja consistente com o estilo de código**

- Utilize um estilo de código consistente em todo o projeto. Ferramentas como Prettier (para JavaScript) ou Black (para Python) ajudam a garantir que o estilo do código siga um padrão. Além disso, siga as diretrizes de estilo de código da sua equipe ou do próprio idioma de programação.

#### 11. **Evite código comentado**

- **Exemplo bom**: Código antigo foi removido do arquivo.
- **Exemplo ruim**: // Função antiga que não usamos mais. // def oldFunction(): pass

#### 12. **Mantenha os arquivos pequenos e coesos**

- Arquivos de código devem ser pequenos e ter uma responsabilidade clara. Evite arquivos que crescem muito com várias funcionalidades diferentes, pois isso dificulta a leitura e manutenção.
    - **Exemplo bom**: Um arquivo `user_controller.py` lidando apenas com o CRUD de usuários.
    - **Exemplo ruim**: Um arquivo `app_logic.py` lidando com usuários, produtos, transações e relatórios.

#### 13. **Atualize comentários ao modificar código**

- Se o código for alterado, os comentários também devem ser atualizados para refletir essas mudanças. Comentários desatualizados podem ser mais prejudiciais do que a ausência de comentários.