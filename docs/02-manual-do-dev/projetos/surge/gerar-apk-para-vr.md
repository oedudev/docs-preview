
# Gerar APK para VR

Este guia fornece um passo a passo detalhado para configurar um ambiente de desenvolvimento e gerar um APK para VR utilizando a Unreal Engine 5.5.

### **1 - Instalar a Unreal Engine 5.5 com Suporte para Android**

Baixe e instale a **Unreal Engine 5.5** pelo **Epic Games Launcher**, garantindo que a opção de suporte para Android esteja habilitada durante a instalação.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdgSqMm3HJVImhJuuihxOPFEqpNXVR_QtVLie3DvC4Rw_HnLWDVeHrN-PZ9csEvLFOQlmCbdY3LB7qqbCVf_yOTtUefBkbjoaFDZkeVHJk1kJZNs3l5nGChdmjCwKSQm3Hcofef?key=FO33lLaciBDuFAVArqksYZgz)

### **2 - Instalar o Android Studio (Ladybug 2024.2.1)**

Baixe e instale o **Android Studio versão Ladybug 2024.2.1** no link oficial:[ <u>Download Android Studio</u>](https://developer.android.com/studio/archive)

Durante a instalação, certifique-se de incluir o SDK do Android.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdn6gued6DNQ2c87ONtnLxv66ZF1otjlJqNIOj0X4Whf80VEIEWRfGKxxTC4e1FrGsR5F4jbvK-jD-EpxFOg7_Oa16IRJqabZ59y2SoPcjuj6txnZih7lvo1jpCX1I39NNGg7XZjQ?key=FO33lLaciBDuFAVArqksYZgz)

### **3 - Instalar o Java SE Development Kit (JDK 17.0.6)**

A Unreal Engine requer o JDK para compilar projetos para Android. Faça o download e instale a versão **Java SE Development Kit 17.0.6** pelo link:[ <u>Download JDK 17.0.6</u>](https://www.oracle.com/java/technologies/javase/jdk17-archive-downloads.html)

### **4 - Configurar o Android SDK e NDK**

Após instalar o Android Studio:

1. Abra o **Android Studio** e vá até **More Actions &gt; SDK Manager**

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcrm0g14prMNVqEKUr5ULR8stj9XR9hxGc_LUhmpy0zXkh0QQvwV54DMAp7Lc-rCuQAEv4lH9idbq4kwTbNQLgkIPIVdKOOgYbbmMnysKP_o5HBCUg3F7yf_M3j0_ghcqHCUv1uqw?key=FO33lLaciBDuFAVArqksYZgz)

2. Na aba **SDK Platforms**, instale a versão Android 12L.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXceM7RTQ1FFmF2Hw3wBxhL9UkVaA256oqm80HYSAnSt1T3A6G31B399a7ayx9YWih98x8jnYiPy96utFwa1hc9oAWSQDXH8duLSU0Dzfhf7goM4yqGfm-qqLbrVl1cLkNLY2bCFtg?key=FO33lLaciBDuFAVArqksYZgz)

3. Na aba **SDK Tools**, instale:
4. - Android SDK Build Tools

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXd0ZUfPOeg4r1cFBz8RFjrRu3p77ue4qqP65JzCPaexQjoZBFptgvwr-m_VY1lmbPh4xTytPmhH1e2CYI4S2vyykXUq9JUNhHHZ02Q92p8XlN8QTVHu3y52oz3KCxxaa2hn51dzdw?key=FO33lLaciBDuFAVArqksYZgz)

- Android NDK 

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXc42CNnRkhNaM9QlwTJJWsJbiHBrN_tSMsan5sXlGkKT9z7cXL_XS2uG8FaaGmCP8d-YleiXtj4zi8_4LXvKIKQ4RDYl5OV5glFMMmSWeF1z9jN4JIY6q-e4IjIq_7N1iQhWLyuEw?key=FO33lLaciBDuFAVArqksYZgz)

- Android SDK Command-line Tools

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcpkF9gwMjxN_OpqHxVYGcaJ04_fC0125x1PXKxxULO_IhOTat1V103UllUeyIKEtYGQu_1nm1hcol0RkdpYWWSUQur__72YpzefzItJwganb24isuPPatq0wiKYglu-T0kSt0wmw?key=FO33lLaciBDuFAVArqksYZgz)

- CMake (versão compatível)

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfMvEZokXp7BH5hujWsV0Qnsi9IzUuQ4BuLZB2ECdEUZU4XVrjOpP6qwQyM4PMDZ6Ycq20CWccc23dVvYv9Qe9sXcBy0Fl_fDoLKzI9xpLa3MbNYGkXKiunYE_VtQnljExhVXbv?key=FO33lLaciBDuFAVArqksYZgz)

- Últimas configurações

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcMhtqu5A6SCnHN4KNFHon8yqy3gc8URmVqztstk52tXkZdIzAFYkFS6ySwVaqkw076vm0E3ClvfTtgLc0GCO0v0A5L0z2ELLPLqDTuYSsx-ijJr7GNSSw8pUnsRsdN77z_x4rq?key=FO33lLaciBDuFAVArqksYZgz)

### **5 - Configurar a Unreal Engine para Desenvolvimento Android**

1. Abra a **Unreal Engine** e vá até **Edit &gt; Project Settings**.
2. Navegue até **Platforms &gt; Android** e configure as opções:
3. - Defina o **Minimum SDK Version** e **Target SDK Version** para 32

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXevyckmwByD0bTASY12HYTcrPJTc-REgEozl-nYSJzI_K9d24DSiRjAR6sMo1SVTqBPzE-JsZVrcCIWFoYA51mbdzh_bXzSikqEmjeeJkBtyH0lh_innLFsHycda6bq4oS7aRlj?key=FO33lLaciBDuFAVArqksYZgz)

3. Navegue até **Platforms &gt; Android SDK** e configure as opções:
4. - Configure o **SDK** **e o NDK Path** apontando para os diretórios corretos dentro do Android Studio.
    - Configure o **Java Path** apontando para o diretório correto.
    - Configure o **SDK API Level** para matchndk.
    - Configure o **NDK API Level** para android-32.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcWl1EqpeDEU2ddrgE91mxy1KI3vNirmkq5XF2jRUhwoeWO4diyUK_UNF0Xs1FD0EV9SonR5rIAGCJ-qCkIewSKIiUZlb8I4UbIA1GExniipCCDYKgdyVmcFthkH2e3IAq8VfNa?key=FO33lLaciBDuFAVArqksYZgz)

### **6 - Configurar gerar APK**

1. Vá para **Plataformas &gt; Android**.
2. - Selecione a opção envio.
    - Selecione a opção **ASTC**.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdGdiJ8ub4_vsSJ_mG389-QWHICPgIAvblfsN9NhUAQjQp5dVX2K5kvjWEkzvxf60Lvbi8aORx4GeLja-Hxh9X1oWWR_c0OJ-z_J-35GQqYA7DKuOTkKO98DNCzqY9ehes8tAVstg?key=FO33lLaciBDuFAVArqksYZgz)

### **7 - Gerar APK**

2. Vá para **Plataformas &gt; Android**.
3. Selecione **Empacotar Projeto.**

Agora seu ambiente está configurado para desenvolver e exportar projetos VR na Unreal Engine!

### **8 - Help Links**

[<u>https://www.youtube.com/watch?v=mZ0yHY3X6OQ</u>](https://www.youtube.com/watch?v=mZ0yHY3X6OQ)

[<u>https://dev.epicgames.com/documentation/en-us/unreal-engine/set-up-android-sdk-ndk-and-android-studio-using-turnkey-for-unreal-engine</u>](https://dev.epicgames.com/documentation/en-us/unreal-engine/set-up-android-sdk-ndk-and-android-studio-using-turnkey-for-unreal-engine)

[<u>https://dev.epicgames.com/community/learning/tutorials/PYP7/unreal-engine-5-5-x-for-meta-quest-vr</u>](https://dev.epicgames.com/community/learning/tutorials/PYP7/unreal-engine-5-5-x-for-meta-quest-vr)