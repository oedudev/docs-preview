
# Introdução ao Atomic Design no Hsoares

## **1. Introdução ao Atomic Design**

O Atomic Design é uma metodologia de criação de interfaces que organiza os componentes em diferentes níveis de complexidade, inspirada na estrutura da natureza (átomos → moléculas → organismos → templates → páginas).

![](https://ajuda.digitalsys.com.br/uploads/images/gallery/2025-09/JMj4HBuVvtATC8v5-embedded-image-q1fg1qfp.png)

A ideia central é criar componentes reutilizáveis e padronizados que podem ser combinados para formar estruturas mais complexas sem perder consistência. Isso traz benefícios como: Escalabilidade, Reutilização, Padronização e Facilidade de manutenção e evolução.

Referencia: [Atomic Design by Brad Frost](https://atomicdesign.bradfrost.com/)

## **2. Aplicação no Projeto Hsoares**

O projeto Hsoares já utiliza conceitos do Atomic Design, mas ainda de forma parcial. O objetivo é aplicar a metodologia corretamente, criando uma estrutura clara e escalável para todos os componentes.

Para entender melhor, observe a tela de Fiança locatícia como exemplo prático.

Nas imagens que acompanham este documento, os elementos estão destacados pelas cores:

- **Verde:** Átomo
- **Azul:** Molécula
- **Laranja:** Organismo
- **Vermelho:** Página

![](https://ajuda.digitalsys.com.br/uploads/images/gallery/2025-09/GWg3C8rf2qMhFDwM-embedded-image-agq9mxoy.png)

Observe com maior detalhe o formulário, já que a lógica aplicada a ele será a mesma para os outros componentes.

![](https://ajuda.digitalsys.com.br/uploads/images/gallery/2025-09/13UNro0tanrU4kkm-embedded-image-nxemsclh.png)

Pode-se observar que ele é construído a partir de moléculas, que são componentes formados pela combinação de um **input** e um átomo. Já os demais **inputs** e **selects** não destacados também são considerados organismos.

Atomo: 

![](https://ajuda.digitalsys.com.br/uploads/images/gallery/2025-09/2RlUUfPPVdke0Hep-embedded-image-hwmvnw4b.png)

Molecula:

![](https://ajuda.digitalsys.com.br/uploads/images/gallery/2025-09/SV8mnSpMfJ6KNbVR-embedded-image-rjgdxxwc.png)

## **3. Exemplo prático – Tela de Fiança Locatícia**

Imagine que nossa pagina vai ser construída a partir de diferentes “blocos”, onde não precisamos utilizar somente nessa página podemos usar esses blocos em qualquer parte do sistema, mudando somente os dados que enviamos.

![](https://ajuda.digitalsys.com.br/uploads/images/gallery/2025-09/gJS72kghbI6zjz2z-embedded-image-rqaxysic.png)

### **3.1 Átomos**

Os átomos são os **elementos básicos** da interface.  
 Exemplos na tela:

- Tipografia (título **“Fiança Locatícia”**, rótulos dos inputs).
- Campos simples (**input**, **select**).
- Ícones (seta do botão, ícones do menu lateral).
- Indicador de obrigatório (\*).

### **3.2 Moléculas**

As moléculas são **combinações simples de átomos** que formam um bloco funcional.  
 Exemplos:

- Campo de formulário (label + input + indicador obrigatório).
- Botão com ícone (texto + ícone de seta).
- Item do stepper (número + texto + linha de progresso).
- Item do menu lateral (ícone + fundo ativo/passivo).

### **3.3 Organismos**

Os organismos são **blocos completos**, compostos por moléculas e/ou átomos.  
 Exemplos:

- Formulário “Endereço”: agrupa vários campos em um bloco coeso.
- Stepper (barra de progresso): conjunto dos steps **Locação, Inquilino, Vigência**.
- Sidebar de navegação: itens de menu e avatar do usuário.
- Barra de ações: botão principal “Próximo”.

### **3.4 Templates**

Os templates organizam os organismos e definem a estrutura da página.

  
 Exemplo:

- Layout de formulário multi-etapas, que inclui: título, sidebar, stepper, formulário e barra de ações.

### **3.4 Página**

As páginas são a aplicação real dos templates com conteúdo específico.  
 Exemplo:

- Página “Fiança Locatícia – Etapa 1 (Locação)”, que utiliza o template de formulário multi-etapas preenchido com os campos de endereço.

Veja a seguir um exemplo de como montar a página com os componentes criados.

![](https://ajuda.digitalsys.com.br/uploads/images/gallery/2025-09/zHUtL0NigPeiylo4-embedded-image-qmv0dunb.png)

## **4. Boas práticas de dados**

Um ponto essencial no uso do Atomic Design é a separação de responsabilidades. Isso garante que cada camada do sistema tenha um papel bem definido, evitando a mistura de lógica de negócio com apresentação:

- **Página:** responsável por buscar e enviar dados (requisições à API).

 ![](https://ajuda.digitalsys.com.br/uploads/images/gallery/2025-09/SqCPTeZla7D9nxIS-embedded-image-4e9h6c6o.png)

- **Template:** recebe dados da página via **props** e os distribui para seus filhos.

![](https://ajuda.digitalsys.com.br/uploads/images/gallery/2025-09/jBoJf3Ksb8EH0uAe-embedded-image-bersbyyf.png)

- **Organismos e moléculas:** apenas exibem os dados recebidos ou disparam eventos para a página quando necessário.

![](https://ajuda.digitalsys.com.br/uploads/images/gallery/2025-09/7mmyW5u9nid9uuKk-embedded-image-1coh02zn.png)

![](https://ajuda.digitalsys.com.br/uploads/images/gallery/2025-09/VeGht0YM00nmk1zU-embedded-image-bathwrno.png)

Dessa forma, garantimos que os componentes sejam **desacoplados e reutilizáveis**, mantendo a lógica de negócios sempre no nível da página.

## **5. Layout**

A **sidebar** e o **footer** podem ou não estar presentes no layout do sistema. Quando existem, fazem parte da estrutura global da aplicação e, por isso, não precisam ser representados na árvore de componentes. Diferente de átomos, moléculas ou organismos, esses elementos são parte do layout principal e não de componentes reutilizáveis, ficando definidos de forma centralizada no template do sistema.