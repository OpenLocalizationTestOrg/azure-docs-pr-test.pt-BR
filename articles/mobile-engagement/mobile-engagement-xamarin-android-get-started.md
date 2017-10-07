---
title: aaaGet iniciado com o Azure Mobile Engagement para xamarin
description: "Saiba como toouse Azure Mobile Engagement com análises e notificações por Push para aplicativos xamarin."
services: mobile-engagement
documentationcenter: xamarin
author: piyushjo
manager: erikre
editor: 
ms.assetid: fb68cf98-08a2-41b5-8e59-757469de3fe7
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 06/16/2016
ms.author: piyushjo
ms.openlocfilehash: 9d584fea8e8153d511258cf9b6f87f31dac6aeca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-xamarinandroid-apps"></a>Introdução ao Azure Mobile Engagement para aplicativos Xamarin.Android
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

Este tópico mostra como toouse do Azure Mobile Engagement toounderstand o uso do aplicativo e como toosend envio usuários de toosegmented de notificações de um aplicativo xamarin.
Este tutorial demonstra Olá cenário difusão simples usando o Mobile Engagement. Nele, você cria um aplicativo Xamarin.Android em branco que coleta dados básicos e recebe notificações por push usando o GCM (Google Cloud Messaging).

> [!NOTE]
> serviço do Azure Mobile Engagement Olá será descontinuado de 2018 março e está apenas disponível tooexisting clientes. Para saber mais, confira [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).

Este tutorial requer o seguinte hello:

* [Xamarin Studio](http://xamarin.com/studio). Você também pode usar o Visual Studio com Xamarin, mas este tutorial usa o Xamarin Studio. Para obter instruções de instalação, confira [Instalar e configurar para Visual Studio e Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).
* [SDK do Xamarin do Mobile Engagement](https://www.nuget.org/packages/Microsoft.Azure.Engagement.Xamarin/)

> [!NOTE]
> toocomplete neste tutorial, você deve ter uma conta ativa do Azure. Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos. Para obter detalhes, consulte [Avaliação Gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-xamarin-android-get-started).
> 
> 

## <a id="setup-azme"></a>Configuração do Mobile Engagement para seu aplicativo Android
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a>Conectar seu back-end do aplicativo toohello Mobile Engagement
Este tutorial apresenta uma "integração básica", que é Olá mínimo definido toocollect necessários dados e envia uma notificação por push. 

Vamos criar um aplicativo básico com a integração de saudação toodemonstrate Xamarin Studio.

### <a name="create-a-new-xamarinandroid-project"></a>Criar um novo projeto Xamarin.Android
1. Iniciar **Xamarin Studio** ir muito**arquivo** -> **novo** -> **solução** 
   
    ![][1]
2. Selecione **aplicativo Android** , em seguida, certifique-se de idioma Olá selecionado é **c#** e clique em **próximo**.
   
    ![][2]
3. Preencha Olá **nome do aplicativo** e hello **identificador de organização**. Certifique-se de que toocheckmark **Google executar serviços** e, em seguida, clique em **próximo**. 
   
    ![][3]
4. Saudação de atualização **nome do projeto**, **nome da solução** e **local** se necessário e clique em **criar**.
   
    ![][4]

Xamarin Studio criará o aplicativo hello no qual integraremos Mobile Engagement. 

### <a name="connect-your-app-toomobile-engagement-backend"></a>Conectar seu back-end do aplicativo tooMobile contrato
1. Clique com botão direito Olá **pacotes** pasta no windows de solução hello e selecione **adicionar pacotes de...**
   
    ![][5]
2. Pesquise Olá **SDK do Microsoft Azure Mobile Engagement Xamarin** e adicioná-lo tooyour solução.  
   
    ![][6]
3. Abra **MainActivity.cs** e adicione Olá seguinte usando instruções:
   
        using Microsoft.Azure.Engagement;
        using Microsoft.Azure.Engagement.Activity;
4. Em Olá `OnCreate` método, adicione Olá após a conexão de saudação tooinitialize com back-end do compromisso de mobilidade. Certifique-se de que tooadd seu **ConnectionString**. 
   
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.ConnectionString = "YourConnectionStringFromAzurePortal";
        EngagementAgent.Init(engagementConfiguration);

### <a name="add-permissions-and-a-service-declaration"></a>Adicionar permissões e uma declaração de serviço
1. Olá, abra **Manifest.xml** arquivo na pasta de propriedades de saudação. Selecione a guia fonte para que você atualizar o código-fonte Olá XML diretamente.
2. Adicionar toohello essas permissões manifest (que podem ser encontrado em Olá **propriedades** pasta) do projeto imediatamente antes ou após Olá `<application>` marca:
   
        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
        <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
        <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
        <uses-permission android:name="android.permission.VIBRATE" />
        <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION"/>
3. Adicione a seguinte Olá entre hello `<application>` e `</application>` marcas de serviço de agente toodeclare hello:
   
        <service
             android:name="com.microsoft.azure.engagement.service.EngagementService"
             android:exported="false"
             android:label="<Your application name>"
             android:process=":Engagement"/>
4. No código de saudação que você acabou de colar, substitua `"<Your application name>"` no rótulo de saudação. Isso é exibido no hello **configurações** onde os usuários podem ver os serviços em execução no dispositivo de saudação do menu. Por exemplo você pode adicionar palavra hello "Serviço" nesse rótulo.

### <a name="send-a-screen-toomobile-engagement"></a>Enviar um tooMobile tela Contrato
Em ordem toostart enviar dados e garantir que os usuários de saudação estão ativos, você deve enviar pelo menos uma tela toohello Mobile Engagement backend. Para fazer isso-certifique-se de que Olá `MainActivity` herda de `EngagementActivity` em vez de `Activity`.

    public class MainActivity : EngagementActivity

Como alternativa, se você não puder herdar de `EngagementActivity`, então, deverá adicionar os métodos `.StartActivity` e `.EndActivity` em `OnResume` e `OnPause`, respectivamente.  

        protected override void OnResume()
            {
                EngagementAgent.StartActivity(EngagementAgentUtils.BuildEngagementActivityName(Java.Lang.Class.FromType(this.GetType())), null);
                base.OnResume();             
            }

            protected override void OnPause()
            {
                EngagementAgent.EndActivity();
                base.OnPause();            
            }

## <a id="monitor"></a>Conectar o aplicativo com monitoramento em tempo real
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a>Habilitar notificações por push e mensagens no aplicativo
Mobile Engagement permite toointeract com e alcançar os usuários com as notificações por push e no aplicativo mensagens no contexto de saudação de campanhas. Esse módulo é chamado alcance no portal do Mobile Engagement hello.
Olá seções a seguir define o seu aplicativo tooreceive-los.

[!INCLUDE [Enable Google Cloud Messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

[!INCLUDE [Enable in-app messaging](../../includes/mobile-engagement-android-send-push.md)]

[!INCLUDE [Send notification from portal](../../includes/mobile-engagement-android-send-push-from-portal.md)]

<!-- Images -->
[1]: ./media/mobile-engagement-xamarin-android-get-started/1.png
[2]: ./media/mobile-engagement-xamarin-android-get-started/2.png
[3]: ./media/mobile-engagement-xamarin-android-get-started/3.png
[4]: ./media/mobile-engagement-xamarin-android-get-started/4.png
[5]: ./media/mobile-engagement-xamarin-android-get-started/5.png
[6]: ./media/mobile-engagement-xamarin-android-get-started/6.png
