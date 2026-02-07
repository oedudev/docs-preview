
# Build dos apps no expo

 Este tutorial tem como objetivo descrever os passos para realizar o build dos apps do projeto.

#### 1 - Crie uma conta 'digitalsys' na expo

- Acesse [https://expo.dev/](https://expo.dev/) , registre com o email da empresa e solicite para algum administrador a alteração de sua nova conta para 'develop'

#### 2 - Verifique se todas as dependências estão instaladas

- Na pasta raiz do seu projeto, pode-se fazer isso executando o seguinte comando: **yarn install**

#### 3 - Verifique se o EAS está instalado 

- Pode-ser verificar a versão com o comando: **eas --version**
- Caso não encontre uma instalação, execute a instalação por meio do seguinte comando: **npm install -g eas-cli**

#### 4 - Faça login com conta Expo

- Para realizar o build deve-se estar autenticado, portanto, execute o seguinte comando: **eas login**
- Se deseja verificar qual usuário está logado e informações da sua conta, execute: **eas whoami**

#### 5 - Faça o build dos apps

- Na raiz do seu projeto e c om os passos anteriores bem sucedidos, execute: **eas build --profile preview --platform android**
- Ao finalizar o build, deve ser possível observar o QR code e o link que redirecionam para o APK atualizado gerado