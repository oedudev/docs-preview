
# Guia para Gerar o APK do Projeto (app-socorrista)

##### **Guia para Gerar o APK do Projeto** 

Siga as etapas abaixo para configurar o ambiente e gerar o APK do aplicativo.

##### **1. Instalar a extensão Ionic no VS Code**

No Visual Studio Code, abra o marketplace e procure por **Ionic**. Instale a extensão oficial.

##### **2. Instalar o Android Studio**

Baixe e instale o **Android Studio**, garantindo que os componentes do **Android SDK** e **Platform Tools** sejam instalados.

##### 3. Configurar variáveis no arquivo `.env`

Defina as chaves necessárias no arquivo `.env` do projeto

`VITE_API_URL=https://e-sus-urgencias-api.digitalsysdev.com.br`

`VITE_SOCKET_URL=wss://e-sus-urgencias-api.digitalsysdev.com.br`

(Chaves atualizadas em 24/11)

##### **4. Abrir a extensão Ionic**

No VS Code, clique na extensão do Ionic localizada na barra lateral.

[![image.png](/docs-preview/img/guia-para-gerar-o-apk-do-projeto-app-socorrista-1.png)](https://ajuda.digitalsys.com.br/uploads/images/gallery/2025-11/aFwiRTmuV1Y6Tj7a-image.png)

##### **5. Executar o comando de sincronização do Capacitor**

No terminal do VS Code, execute:

npx cap sync --inline

Se ocorrer algum erro, rode antes:

npm run build

##### **6. Gerar o build do frontend**

npm run build

##### **7. Abrir o Android Studio**

Na extensão do Ionic, selecione:

**Open in Android Studio**

[![image.png](/docs-preview/img/guia-para-gerar-o-apk-do-projeto-app-socorrista-2.png)](https://ajuda.digitalsys.com.br/uploads/images/gallery/2025-11/NpIqK3l2CScz8cQa-image.png)

##### **8. Gerar o APK**

No Android Studio, siga o caminho:

**Menu hambúrguer → Build → Build App → Build APK**

[![image.png](/docs-preview/img/guia-para-gerar-o-apk-do-projeto-app-socorrista-3.png)](https://ajuda.digitalsys.com.br/uploads/images/gallery/2025-11/rXYc1LtgxMdPXdul-image.png)

##### **9. Encontrar o APK**

Após a finalização do build, aparecerá um alerta no canto inferior direito indicando o local do arquivo.  
Clique em **Locate**.

  
[![image.png](/docs-preview/img/guia-para-gerar-o-apk-do-projeto-app-socorrista-4.png)](https://ajuda.digitalsys.com.br/uploads/images/gallery/2025-11/QP7Ed5BYL2mYWSWE-image.png)

##### **10. Pronto!**

O APK estará disponível na pasta exibida pelo Android Studio.

 [![image.png](/docs-preview/img/guia-para-gerar-o-apk-do-projeto-app-socorrista-5.png)](https://ajuda.digitalsys.com.br/uploads/images/gallery/2025-11/9UQdpRh05PP5znL0-image.png)