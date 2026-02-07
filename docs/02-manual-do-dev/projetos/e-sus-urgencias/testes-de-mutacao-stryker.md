
# Testes de mutação - Stryker

## **Stryker**

Devido ao alto número de testes gerados por IA no sistema “E-SUS Urgência”, vê-se a necessidade de garantir não apenas a quantidade e cobertura de testes, mas também sua qualidade. Tendo isso em vista, podemos usar testes de mutação por meio de ferramentas como o STRYKER.

O Stryker integra automaticamente com a ferramente JEST, não sendo necessária nenhuma configuração adicional no caso de incremento do número de testes.

#### **Instalação**

O Stryker está contigo no arquivo package.json como uma dev dependency, e será instalado ao rodar o comando:

```bash
npm install -D
```

#### **Configuração**

O arquivo de configuração "stryker.config.json" está contido na raiz do projeto (/backend)

```json
{
  "$schema": "./node_modules/@stryker-mutator/core/schema/stryker-schema.json",
  "_comment": "This config was generated using 'stryker init'. Please take a look at: https://stryker-mutator.io/docs/stryker-js/configuration/ for more information.",
  "packageManager": "npm",
  "reporters": [
    "html",
    "clear-text",
    "progress"
  ],
  "testRunner": "jest",
  "testRunner_comment": "Take a look at https://stryker-mutator.io/docs/stryker-js/jest-runner for information about the jest plugin.",
  "coverageAnalysis": "perTest",
  "mutate": [
    "apps/api/src/**/*.ts"
  ],
  "jest": {
    "projectType": "custom",
    "configFile": "package.json"
  },
  "ignoreStatic": true
}
```

#### **Execução**

Para executar o stryker, basta acessar o diretório do backend do projeto e executar o comando:

```bash
npx stryker run
```

**OBS:** A execução do teste pode levar de 2 a 6 minutos

#### **Relatório**

Após a execução, o stryker gerará um relatório no diretório '/reports', na raíz do projeto. podemos visualizá-lo, por exemplo na forma de HTML:  
  
[![image.png](/img/testes-de-mutacao-stryker-1.png)](https://ajuda.digitalsys.com.br/uploads/images/gallery/2025-02/kZ6CIsoXnZqrAeTm-image.png)

Aqui podemos ver, por exemplo, nosso score de mutação simplificado:

**K / (K + N)**  
Onde:

K - Mutantes mortos;

N - Mutantes não mortos.

**OBS:** O ideal é termos um score de mutação acima de 90%

Também podemos ver, especificamente, quais mutantes foram mortos e quais sobreviveram:

[![image.png](/img/testes-de-mutacao-stryker-2.png)](https://ajuda.digitalsys.com.br/uploads/images/gallery/2025-02/h6N5OyTF12EqfORr-image.png)

####   