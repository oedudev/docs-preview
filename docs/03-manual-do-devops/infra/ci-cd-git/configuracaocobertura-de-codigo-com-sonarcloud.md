---
id: 27
title: "Configuração/Cobertura de Código com SonarCloud"
updated_at: 2025-03-30T19:10:17.000000Z
---

# Configuração/Cobertura de Código com SonarCloud

Este guia tem como objetivo ajudar na configuração do SonarCloud em projetos multi-repo e monorepo, integrando-os com o GitHub Actions para rodar testes, gerar relatórios e enviá-los ao SonarCloud. Siga os passos abaixo para configurar corretamente em seu projeto.

#### **1. Criando um Projeto no SonarCloud**

- Acesse o [SonarCloud](https://sonarcloud.io) e faça login pela **sua conta do GitHub** que está na organização da DigitalSys
- Clique em **“+”** no menu superior e selecione **“Analyze new project”**

![](http://plane.digitalsys.com.br/uploads/d548ef5a-76b8-450b-b1c2-c98209a0d886/b128e97b2c8b415e864384c504aacde2-image.png)

- Certifique que em “organization” esteja selecionada a organização da DigitalSys e escolha o repositório que deseja analisar
- Se estiver configurando para um projeto monorepo, selecione a opção **"**Setup a <u>monorepo</u>**"** e escolha o repositório do seu projeto

![](http://plane.digitalsys.com.br/uploads/d548ef5a-76b8-450b-b1c2-c98209a0d886/2e413270ddaf4ca9b7c941bf03159a6a-image.png)

- Após selecionar seu projeto, clique em **“Set Up”**
- Na página seguinte, escolha o critério para o que será considerado novo código para as próximas análises
- Selecione **“Previous version”** para que cada nova versão do código no GitHub seja analisada
- Por fim, crie seu projeto clicando em **“Create Project”**

![](http://plane.digitalsys.com.br/uploads/d548ef5a-76b8-450b-b1c2-c98209a0d886/ac3a49599974434093b4c4e2a0b535b7-image.png)

#### **2. Adicionando Token do SonarCloud ao GitHub**

- Após Criar o projeto, selecione **“With GitHub Actions”** para o método de análise

![](http://plane.digitalsys.com.br/uploads/d548ef5a-76b8-450b-b1c2-c98209a0d886/8af9fde02c0d4c54a7fba71a8d599853-image.png)

- Na página seguinte copie o Sonar Token gerado

![](http://plane.digitalsys.com.br/uploads/d548ef5a-76b8-450b-b1c2-c98209a0d886/0cb9eab7c7bb47bb99713c4d51f0f471-image.png)

- No repositório do GitHub, vá para **Settings &gt; Secrets and variables &gt; Actions**

![](http://plane.digitalsys.com.br/uploads/d548ef5a-76b8-450b-b1c2-c98209a0d886/041f4bee2c7c42e091914861600c3391-image.png)

- No nome do Secret escreva `SONAR_TOKEN` e em secret cole o Token gerado pelo SonarCloud
- Por fim, Clique em **“Add secret”** para criar o Secret

![](http://plane.digitalsys.com.br/uploads/d548ef5a-76b8-450b-b1c2-c98209a0d886/c643536e816f4a6d8d0b44e39ab49052-image.png)

#### **3. Configurando o SonarCloud no Projeto**

- Voltando para a página do SonarCloud podemos acessar as informações do projeto no menu lateral clicando no botão **“Information”**
- Essa página contem as chaves de projeto e de organização

![](http://plane.digitalsys.com.br/uploads/d548ef5a-76b8-450b-b1c2-c98209a0d886/08c6e513e5fe4c9491b58d1f6b0f3797-image.png)

- Essas chaves devem estar presente em um arquivo `sonar-project.properties` na **raiz** do seu projeto, da seguinte forma

```
sonar.projectKey=DigitalsysTecnologia_exemplo
sonar.organization=digitalsys
```

- Caso o projeto analisado seja monorepo, **além do arquivo de propriedades da raiz,** cada módulo deve conter seu próprio `sonar-project.properties`, alterando entre eles o sonar.projectKey para o informado no seu repositório próprio do SonarCloud
- No arquivo de propriedades do SonarCloud também podem ser definidas algumas configurações, as mais utilizadas são:

<table id="bkmrk-comandodescri%C3%87%C3%83oexem"><colgroup><col style="width: 262px;"></col><col style="width: 356px;"></col><col style="width: 417px;"></col></colgroup>
<tbody>
<tr>
<td>**COMANDO**

</td>

<td>**DESCRIÇÃO**

</td>

<td>**EXEMPLO**

</td>
</tr>

<tr>
<td>`sonar.projectKey`

</td>

<td>Identificador único do projeto no SonarCloud

</td>

<td>`sonar.projectKey=my_project_key`

</td>
</tr>

<tr>
<td>`sonar.organization`

</td>

<td>Nome da organização no SonarCloud

</td>

<td>`sonar.organization=my_organization`

</td>
</tr>

<tr>
<td>`sonar.sources`

</td>

<td>Diretório(s) onde o código-fonte está localizado. Pode ser múltiplo, separado por vírgulas

</td>

<td>`sonar.sources=src`

</td>
</tr>

<tr>
<td>`sonar.tests`

</td>

<td>Diretório(s) onde os testes estão localizados. Pode ser múltiplo, separado por vírgulas

</td>

<td>`sonar.tests=tests`

</td>
</tr>

<tr>
<td>`sonar.language`

</td>

<td>Linguagem de programação principal do projeto

</td>

<td>`sonar.language=java`

</td>
</tr>

<tr>
<td>`sonar.exclusions`

</td>

<td>Arquivos ou diretórios a serem excluídos da análise

</td>

<td>`sonar.exclusions=**/*.xml`

</td>
</tr>

<tr>
<td>`sonar.inclusions`

</td>

<td>Especifica quais arquivos ou diretórios incluir na análise, se for diferente dos padrões

</td>

<td>`sonar.inclusions=src/**/*.java`

</td>
</tr>

<tr>
<td>`sonar.tests.inclusions`

</td>

<td>Especifica quais arquivos de teste incluir na análise

</td>

<td>`sonar.tests.inclusions=tests/**/*.java`

</td>
</tr>

<tr>
<td>`sonar.test.exclusions`

</td>

<td>Arquivos ou diretórios de teste a serem excluídos da análise

</td>

<td>`sonar.test.exclusions=tests/helpers/**`

</td>
</tr>

<tr>
<td>`sonar.coverage.exclusions`

</td>

<td>Arquivos ou diretórios a serem excluídos da análise de cobertura de código

</td>

<td>`sonar.coverage.exclusions=src/main/resources`

</td>
</tr>

<tr style="height: 10px;">
<td>sonar.go.coverage.reportPaths

</td>

<td>Caminho para o arquivo do relatório de cobertura de testes para projetos em Golang

</td>

<td>`sonar.go.coverage.reportPaths=reports/*coverage*.out`

</td>
</tr>

<tr>
<td>`sonar.python.coverage.reportPaths`

</td>

<td>Caminho para o arquivo do relatório de cobertura de testes para projetos em Python

</td>

<td>`sonar.python.coverage.reportPaths=reports/*coverage*.out`

</td>
</tr>
</tbody>
</table>

Mais comandos podem ser encontrados na [Documentação do SonarCloud](https://docs.sonarsource.com/sonarqube/latest/analyzing-source-code/analysis-parameters/)

Exemplo de arquivo `sonar-project.properties` comum

```
sonar.projectKey=DigitalsysTecnologia_exemplo
sonar.organization=digitalsys

sonar.qualitygate.wait=true

sonar.sources=.
sonar.python.coverage.reportPaths=reports/coverage.xml

sonar.coverage.exclusions=**/tests/**,Dockerfile
```

#### **4. Configurando Workflow do GitHub Actions**

- No repositório do projeto, crie um arquivo **“.github/workflows/”**
- Dentro dessa pasta, crie um arquivo YAML, por exemplo, `ci.yml`
- Nesse arquivo podemos definir ações que serão executadas pelo GitHub em definidas mudanças no repositório

Primeiro, podemos definir o nome do nosso workflow e quando ele será executado

```
name: Main Workflow

on:
  push:
    branches:
      - '**'
  pull_request:
    types: [opened, synchronize, reopened]
```

Com esse código definimos um workflow chamado **“**Main Workflow**”** que será executado sempre que houver um push em qualquer branch do projeto e sempre que um pull request for aberto, sincronizado ou reaberto

Agora podemos criar as ações que serão executadas nos momentos definidos na primeira parte do código. Em nosso caso precisamos:

1. Gerar o relatório de cobertura de testes;
2. Enviar para análise do SonarCloud;

Para cada ação precisamos especificar os passos do zero, então para gerar o relatório de testes precisamos iniciar o projeto como se estivéssemos o executando pela primeira vez, o exemplo abaixo apresenta os passos necessários para rodar um projeto em Python, dês de configurar a versão do Python que será utilizada até o comando para se gerar o arquivo do relatório pelo GitHub Actions

```
jobs:          
  run-tests:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v4

      - name: Set up Python 3.12
        uses: actions/setup-python@v5
        with:
          python-version: 3.12

      - name: Install dependencies
        run: |
          python -m pip install --upgrade pip
          pip install -r ./requirements.txt

      - name: Run tests
        run: |
          pytest tests --cov=./ --cov-report=xml:reports/coverage.xml

      - name: Store test reports
        uses: actions/upload-artifact@v4
        with:
          name: coverage-report
          path: ./reports/coverage.xml
          retention-days: 1
          if-no-files-found: error
```

Nesse código estamos criando um “job” chamado `run-tests`, nele começamos baixando uma versão compatível com o projeto do Python e baixamos suas dependências. No exemplo foi gerado a cobertura de testes pelo pytest, utilizando a flag `--cov-report=xml:reports/coverage.xml`, que está armazenando o arquivo de relatório em `reports/coverage.xml`

Por fim, utilizamos o “actions/upload-artifact” para armazenar o relatório, o tornando acessível para os próximos jobs

Agora podemos criar um novo job, com o objetivo de enviar o relatório gerado para a análise do SonarCloud

```
sonar-scan:
    needs: run-tests
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v4
        with:
          fetch-depth: 0

      - name: Download coverage artifact
        uses: actions/download-artifact@v4
        with:
          name: coverage-report
          path: ./reports/

      - name: SonarCloud Scan
        uses: sonarsource/sonarcloud-github-action@master
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
          SONAR_TOKEN: ${{ secrets.SONAR_TOKEN }}
```

É importante definir que esse job possui dependência no anterior (`needs: run-tests`), pois se não eles irão ser executados em paralelo, porém precisamos esperar o artefato da primeira ação ser gerado

Com isso, podemos baixar o relatório utilizando o “actions/download-artifact” e especificando o caminho de destino do arquivo. Nota: **O caminho de** **destino para o relatório deve ser o mesmo especificado no** `sonar-project.properties`

Por fim, podemos usar o módulo do actions do sonarcloud “sonarsource/sonarcloud-github-action@master” para realizar a análise e enviar o relatório automaticamente. É importante passar como variável o `GITHUB_TOKEN` e o `SONAR_TOKEN`, o Token do SonarCloud foi adicionado as secrets no passo 2., já o Token do GitHub é setado automaticamente pelo próprio GitHub nas secrets do repositório, para acessar uma secret pelo YAML de workflow do Actions basta utilizar `${{ secrets.SECRET_NAME }}`

Pronto, na próxima vez que for feito um push ou um pull request as análises de código e cobertura de testes deve estar presente no repositório do projeto no SonarCloud

Exemplo completo do arquivo `ci.yml`, para um projeto Python

```
name: Main Workflow

on:
  push:
    branches:
      - '**'
  pull_request:
    types: [opened, synchronize, reopened]

jobs:          
  run-tests:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v4

      - name: Set up Python 3.12
        uses: actions/setup-python@v5
        with:
          python-version: 3.12

      - name: Install dependencies
        run: |
          python -m pip install --upgrade pip
          pip install -r ./requirements.txt

      - name: Run tests
        run: |
          pytest tests --cov=./ --cov-report=xml:reports/coverage.xml

      - name: Store test reports
        uses: actions/upload-artifact@v4
        with:
          name: coverage-report
          path: ./reports/coverage.xml
          retention-days: 1
          if-no-files-found: error

  sonar-scan:
    needs: run-tests
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v4
        with:
          fetch-depth: 0

      - name: Download coverage artifact
        uses: actions/download-artifact@v4
        with:
          name: coverage-report
          path: ./reports/

      - name: SonarCloud Scan
        uses: sonarsource/sonarcloud-github-action@master
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
          SONAR_TOKEN: ${{ secrets.SONAR_TOKEN }}
```