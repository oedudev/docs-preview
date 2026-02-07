
# Gerar APK para VR

Este guia fornece um passo a passo detalhado para configurar um ambiente de desenvolvimento e gerar um APK para VR utilizando a Unreal Engine 5.5.

### **1 - Instalar a Unreal Engine 5.5 com Suporte para Android**

Baixe e instale a **Unreal Engine 5.5** pelo **Epic Games Launcher**, garantindo que a opção de suporte para Android esteja habilitada durante a instalação.

![](/docs-preview/img/gerar-apk-para-vr-1.png)

### **2 - Instalar o Android Studio (Ladybug 2024.2.1)**

Baixe e instale o **Android Studio versão Ladybug 2024.2.1** no link oficial:[ <u>Download Android Studio</u>](https://developer.android.com/studio/archive)

Durante a instalação, certifique-se de incluir o SDK do Android.

![](/docs-preview/img/gerar-apk-para-vr-2.png)

### **3 - Instalar o Java SE Development Kit (JDK 17.0.6)**

A Unreal Engine requer o JDK para compilar projetos para Android. Faça o download e instale a versão **Java SE Development Kit 17.0.6** pelo link:[ <u>Download JDK 17.0.6</u>](https://www.oracle.com/java/technologies/javase/jdk17-archive-downloads.html)

### **4 - Configurar o Android SDK e NDK**

Após instalar o Android Studio:

1. Abra o **Android Studio** e vá até **More Actions &gt; SDK Manager**

![](/docs-preview/img/gerar-apk-para-vr-3.png)

2. Na aba **SDK Platforms**, instale a versão Android 12L.

![](/docs-preview/img/gerar-apk-para-vr-4.png)

3. Na aba **SDK Tools**, instale:
4. - Android SDK Build Tools

![](/docs-preview/img/gerar-apk-para-vr-5.png)

- Android NDK 

![](/docs-preview/img/gerar-apk-para-vr-6.png)

- Android SDK Command-line Tools

![](/docs-preview/img/gerar-apk-para-vr-7.png)

- CMake (versão compatível)

![](/docs-preview/img/gerar-apk-para-vr-8.png)

- Últimas configurações

![](/docs-preview/img/gerar-apk-para-vr-9.png)

### **5 - Configurar a Unreal Engine para Desenvolvimento Android**

1. Abra a **Unreal Engine** e vá até **Edit &gt; Project Settings**.
2. Navegue até **Platforms &gt; Android** e configure as opções:
3. - Defina o **Minimum SDK Version** e **Target SDK Version** para 32

![](/docs-preview/img/gerar-apk-para-vr-10.png)

3. Navegue até **Platforms &gt; Android SDK** e configure as opções:
4. - Configure o **SDK** **e o NDK Path** apontando para os diretórios corretos dentro do Android Studio.
    - Configure o **Java Path** apontando para o diretório correto.
    - Configure o **SDK API Level** para matchndk.
    - Configure o **NDK API Level** para android-32.

![](/docs-preview/img/gerar-apk-para-vr-11.png)

### **6 - Configurar gerar APK**

1. Vá para **Plataformas &gt; Android**.
2. - Selecione a opção envio.
    - Selecione a opção **ASTC**.

![](/docs-preview/img/gerar-apk-para-vr-12.png)

### **7 - Gerar APK**

2. Vá para **Plataformas &gt; Android**.
3. Selecione **Empacotar Projeto.**

Agora seu ambiente está configurado para desenvolver e exportar projetos VR na Unreal Engine!

### **8 - Help Links**

[<u>https://www.youtube.com/watch?v=mZ0yHY3X6OQ</u>](https://www.youtube.com/watch?v=mZ0yHY3X6OQ)

[<u>https://dev.epicgames.com/documentation/en-us/unreal-engine/set-up-android-sdk-ndk-and-android-studio-using-turnkey-for-unreal-engine</u>](https://dev.epicgames.com/documentation/en-us/unreal-engine/set-up-android-sdk-ndk-and-android-studio-using-turnkey-for-unreal-engine)

[<u>https://dev.epicgames.com/community/learning/tutorials/PYP7/unreal-engine-5-5-x-for-meta-quest-vr</u>](https://dev.epicgames.com/community/learning/tutorials/PYP7/unreal-engine-5-5-x-for-meta-quest-vr)