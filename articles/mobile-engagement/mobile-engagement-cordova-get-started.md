---
title: aaaGet iniciado com o Azure Mobile Engagement para Cordova/Phonegap
description: "Saiba como toouse Azure Mobile Engagement com análises e notificações por Push para aplicativos Cordova/Phonegap."
services: mobile-engagement
documentationcenter: Mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 54fe9113-e239-4ed7-9fd1-a502d7ac7f47
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-phonegap
ms.devlang: js
ms.topic: hero-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: e67dabbdf7886802bb058f38964e558d5ae6854c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-cordovaphonegap"></a>Introdução ao Azure Mobile Engagement para Cordova/Phonegap
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

Este tópico mostra como toouse do Azure Mobile Engagement toounderstand seu aplicativo uso e enviar por push notificações toosegmented usuários para um aplicativo móvel desenvolvidos com o Cordova.

Neste tutorial, criamos um aplicativo do Cordova em branco usando o Mac e integramos o SDK do Mobile Engagement. Ele coleta dados de análise básica e recebe notificações por push usando o sistema de notificações de Push da Apple (APNS) para iOS e Google Cloud Messaging (GCM) para o Android. Podemos implantará essa tooan dispositivo iOS ou Android para teste. 

> [!NOTE]
> toocomplete neste tutorial, você deve ter uma conta ativa do Azure. Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos. Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-cordova-get-started).
> 
> 

Este tutorial requer o seguinte hello:

* XCode, que você pode instalar da loja de aplicativos do Mac (para a implantação tooiOS)
* [Android SDK & emulador](http://developer.android.com/sdk/installing/index.html) (para a implantação tooAndroid)
* Certificado de notificação por push (.p12) que pode ser obtido no seu centro de desenvolvimento da Apple para APNS
* Número do projeto do GCM que pode ser obtido seu Console de Desenvolvedor do Google para GCM
* [Plug-in do Mobile Engagement Cordova](https://www.npmjs.com/package/cordova-plugin-ms-azure-mobile-engagement)

> [!NOTE]
> Você pode localizar o código-fonte hello e hello Leiame para o plug-in Cordova de saudação em [GitHub](https://github.com/Azure/azure-mobile-engagement-cordova)
> 
> 

## <a id="setup-azme"></a>Configurar o Mobile Engagement para seu aplicativo Cordova
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a>Conectar seu back-end do aplicativo toohello Mobile Engagement
Este tutorial apresenta uma "integração básica" hello mínimo definido toocollect necessários dados e envia uma notificação por push. 

Vamos criar um aplicativo básico com a integração de saudação do Cordova toodemonstrate:

### <a name="create-a-new-cordova-project"></a>Crie um novo projeto com Cordova
1. Iniciar *Terminal* janela no seu Olá Mac máquina e o tipo que criará um novo projeto do Cordova do modelo de padrão de saudação a seguir. Certifique-se de que a publicação Olá perfil você eventualmente use toodeploy seu aplicativo iOS está usando 'com.mycompany.myapp' como Olá ID do aplicativo. 
   
        $ cordova create azme-cordova com.mycompany.myapp
        $ cd azme-cordova
2. Executar Olá tooconfigure a seguir em seu projeto para **iOS** e executá-lo no simulador de iOS hello:
   
        $ cordova platform add ios 
        $ cordova run ios
3. Executar Olá tooconfigure a seguir em seu projeto para **Android** e executá-lo no emulador Android hello. Verifique se as configurações de emulador do Android SDK tem seu destino como APIs do Google (Google Inc.) com hello CPU / ABI como Google APIs ARM.  
   
        $ cordova platform add android
        $ cordova run android
4. Adicione Olá plug-in do Console do Cordova. 

    ```
    $ cordova plugin add cordova-plugin-console
    ``` 

### <a name="connect-your-app-toomobile-engagement-backend"></a>Conectar seu back-end do aplicativo tooMobile contrato
1. Instale o plug-in do Azure Mobile Engagement Cordova Olá proporcionando Olá valores de variáveis tooconfigure Olá plug-in:
   
        cordova plugin add cordova-plugin-ms-azure-mobile-engagement    
             --variable AZME_IOS_CONNECTION_STRING=<iOS Connection String> 
            --variable AZME_IOS_REACH_ICON=... (icon name WITH extension) 
            --variable AZME_ANDROID_CONNECTION_STRING=<Android Connection String> 
            --variable AZME_ANDROID_REACH_ICON=... (icon name WITHOUT extension)       
            --variable AZME_ANDROID_GOOGLE_PROJECT_NUMBER=... (From your Google Cloud console for sending push notifications) 
            --variable AZME_ACTION_URL =... (URL scheme which triggers hello app for deep linking)
            --variable AZME_ENABLE_NATIVE_LOG=true|false
            --variable AZME_ENABLE_PLUGIN_LOG=true|false

*Ícone de alcançar Android* : deve ser o nome de saudação do recurso de saudação sem qualquer extensão, nem o prefixo drawable (ex: mynotificationicon), e o arquivo de ícone Olá deve ser copiado para o projeto android (plataformas/android/res/drawable)

*iOS alcançar ícone* : deve ser o nome de saudação do recurso de saudação com a extensão (ex: mynotificationicon.png), e o arquivo de ícone de saudação deve ser adicionado ao seu projeto do iOS com o XCode (usando Olá adicionar arquivos Menu)

## <a id="monitor"></a>Habilitar monitoramento em tempo real
1. No projeto do Cordova Olá - editar **www/js/index.js** tooadd chamada de saudação tooMobile contrato toodeclare uma nova atividade de uma vez Olá *deviceReady* evento é recebido.
   
         onDeviceReady: function() {
                Engagement.startActivity("myPage",{});
            }
2. Execute o aplicativo hello:
   
   * **Para iOS**
     
       Em `Terminal` janela inicie seu aplicativo em uma nova instância de simulador executando Olá seguinte:
     
           cordova run ios
   * **Para Android**
     
       Em `Terminal` janela inicie seu aplicativo em uma nova instância do emulador executando Olá seguinte:
     
           cordova run android
3. Você pode ver o seguinte Olá Olá logs do console:
   
        [Engagement] Agent: Session started
        [Engagement] Agent: Activity 'myPage' started
        [Engagement] Connection: Established
        [Engagement] Connection: Sent: appInfo
        [Engagement] Connection: Sent: startSession
        [Engagement] Connection: Sent: activity name='myPage'

## <a id="monitor"></a>Conectar o aplicativo com monitoramento em tempo real
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a>Habilitar Notificações por Push e mensagens no aplicativo
Mobile Engagement permite que você toointeract com seus usuários usando notificações por Push e no aplicativo mensagens no contexto de saudação de campanhas. Esse módulo é chamado alcance no portal do Mobile Engagement hello.
Olá seções a seguir irá configurar seu aplicativo tooreceive-los.

### <a name="configure-push-credentials-for-mobile-engagement"></a>Configure credenciais de Push para o Mobile Engagement
tooallow Mobile Engagement toosend notificações por Push em seu nome, é necessário toogrant acessar o certificado de iOS da Apple tooyour ou chave de API de servidor do GCM. 

1. Navegue tooyour portal do compromisso de mobilidade. Verifique se você estiver no aplicativo hello podemos está usando para este projeto e, em seguida, clique em hello **Engage** botão na parte inferior da saudação:
   
    ![][1]
2. Você fará com que apareça na página de configurações de saudação em seu Portal do compromisso. De lá, clique em Olá **Push nativo** seção:
   
    ![][2]
3. Configure o certificado do iOS/a chave da API do servidor de GCM 
   
    **[iOS]**
   
    a. Selecione seu .p12, carregue-o e digite sua senha:
   
    ![][3]
   
    **[Android]**
   
    a. Clique em Editar saudação na frente do **chave API** na seção configurações do GCM de hello e Olá janela pop-up que aparece, cole a chave do servidor GCM de hello e clique em **Okey**. 
   
    ![][4]

### <a name="enable-push-notifications-in-hello-cordova-app"></a>Habilitar notificações por push no aplicativo Cordova de saudação
Editar **www/js/index.js** tooadd Olá chamada tooMobile contrato toorequest notificações por push e declarar um manipulador:

     onDeviceReady: function() {
           Engagement.initializeReach(  
                 // on OpenUrl  
                 function(_url) {   
                 alert(_url);   
                 });  
            Engagement.startActivity("myPage",{});  
        }

### <a name="run-hello-app"></a>Executar o aplicativo hello
**[iOS]**

1. Vamos usar XCode toobuild e implantar o aplicativo hello em notificações por push do hello dispositivo tootest porque iOS permite apenas o dispositivo real de tooan de notificações de push. Vá toohello local onde o projeto do Cordova é criado e navegue muito**...\platforms\ios** local. Abra o arquivo de .xcodeproj nativo Olá no XCode. 
2. Criar e implantar Olá Cordova aplicativo toohello o dispositivo iOS usando conta Olá que tem Olá que contém o certificado Olá recém-carregado toohello portal do compromisso de mobilidade e hello Id do aplicativo que corresponde a saudação fornecido durante a criação de perfil de provisionamento Olá Cordova app. Consulte Olá *identificador de pacote* no seu **recursos\*-Info. plist** arquivo no XCode toomatch-lo para cima. 
3. Você verá um pop-up do hello iOS padrão em seu dispositivo dizendo que o aplicativo hello solicita notificações de toosend de permissão. Conceda permissão de saudação. 

**[Android]**

Você pode simplesmente usar o aplicativo Android do Olá Olá emulador toorun como notificações GCM têm suporte no emulador Android hello. 

    cordova run android

## <a id="send"></a>Enviar um aplicativo de tooyour de notificação
Agora, vamos criar uma campanha de notificação por Push simple que enviará um aplicativo de tooyour por push em execução no dispositivo hello:

1. Navegue toohello **alcançar** no seu portal do compromisso de mobilidade
2. Clique em **novo comunicado** toocreate sua campanha de push
   
    ![][6]
3. Fornecer entradas toocreate sua campanha **[Android]**
   
   * Forneça um **Nome** para sua campanha. 
   * Selecione Olá **tipo de entrega** como *notificação do sistema* *simples*
   * Selecione Olá **tempo de entrega** como *"Qualquer hora"*
   * Forneça um **título** para a notificação que será a primeira linha hello push hello.
   * Forneça um **mensagem** para a notificação que servirá como o corpo da mensagem de saudação. 
     
     ![][11]
4. Fornecer entradas toocreate sua campanha **[iOS]**
   
   * Forneça um **Nome** para sua campanha. 
   * Selecione Olá **tempo de entrega** como *"fora do aplicativo"*
   * Forneça um **título** para a notificação que será a primeira linha hello push hello.
   * Forneça um **mensagem** para a notificação que servirá como o corpo da mensagem de saudação. 
     
     ![][12]
5. Role para baixo e em Olá seção conteúda selecione **somente notificação**
   
    ![][8]
6. [Opcional] Você também pode fornecer uma URL de ação. Certifique-se de que ele usa um esquema de URL fornecido durante a configuração de saudação do plug-in **AZME\_REDIRECIONAR\_URL** variável, por exemplo, *myapp://test*.  
7. Você concluiu possíveis de campanha configuração hello mais básica. Agora, role para baixo novamente e clique em Olá **criar** botão toosave sua campanha.
8. Por fim, **Ative** sua campanha
   
    ![][10]
9. Agora você deve ver uma notificação por push em seu dispositivo ou emulador como parte desta campanha. 

## <a id="next-steps"></a>Próximas etapas
[Visão geral de todos os métodos disponíveis no SDK do Cordova Mobile Engagement](https://github.com/Azure/azure-mobile-engagement-cordova)

<!-- Images. -->

[1]: ./media/mobile-engagement-cordova-get-started/engage-button.png
[2]: ./media/mobile-engagement-cordova-get-started/engagement-portal.png
[3]: ./media/mobile-engagement-cordova-get-started/native-push-settings.png
[4]: ./media/mobile-engagement-cordova-get-started/api-key.png
[6]: ./media/mobile-engagement-cordova-get-started/new-announcement.png
[8]: ./media/mobile-engagement-cordova-get-started/campaign-content.png
[10]: ./media/mobile-engagement-cordova-get-started/campaign-activate.png
[11]: ./media/mobile-engagement-cordova-get-started/campaign-first-params-android.png
[12]: ./media/mobile-engagement-cordova-get-started/campaign-first-params-ios.png

