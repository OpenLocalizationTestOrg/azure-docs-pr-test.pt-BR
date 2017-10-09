---
title: "aaaGet Introdução aos aplicativos do Azure Mobile Engagement para Windows Phone Silverlight"
description: "Saiba como toouse do Azure Mobile Engagement com notificações de análise e enviar por push para aplicativos do Windows Phone Silverlight."
services: mobile-engagement
documentationcenter: windows
author: piyushjo
manager: erikre
editor: 
ms.assetid: aa34692f-87f7-47c6-a20c-a1972750bc25
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: b39a838ab03217b2dc845cbf59d7bf8b094dac1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-windows-phone-silverlight-apps"></a>Introdução ao Azure Mobile Engagement para aplicativos do Windows Phone Silverlight
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

Este tópico mostra como toouse do Azure Mobile Engagement toounderstand seu uso do aplicativo e enviar por push usuários de toosegmented de notificações de um aplicativo do Windows Phone Silverlight.
Este tutorial demonstra Olá cenário difusão simples usando o Mobile Engagement. Nele, você cria um aplicativo do Windows Phone Silverlight em branco que coleta dados básicos e recebe notificações por push usando o Serviço de Notificação por Push da Microsoft (MPNS).

> [!NOTE]
> serviço do Azure Mobile Engagement Olá será descontinuado de 2018 março e está apenas disponível tooexisting clientes. Para saber mais, confira [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).

> [!NOTE]
> Não há suporte para projetos do Windows Phone 8.1 e versões anteriores no Visual Studio 2017.  Para saber mais, confira [Direcionamento e compatibilidade da plataforma Visual Studio 2017](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).

> [!NOTE]
> Se você estiver direcionando o Windows Phone 8.1 (não Silverlight), consulte toohello [tutorial Windows Universal](mobile-engagement-windows-store-dotnet-get-started.md).
> 
> 

Este tutorial requer o seguinte hello:

* Visual Studio 2013
* [MicrosoftAzure.MobileEngagement] 

> [!NOTE]
> toocomplete neste tutorial, você deve ter uma conta ativa do Azure. Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos. Para obter detalhes, consulte [Avaliação Gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-windows-phone-get-started).
> 
> 

## <a id="setup-azme"></a>Configurar o Mobile Engagement para aplicativos do Windows Phone
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a>Conectar seu back-end do aplicativo toohello Mobile Engagement
Este tutorial apresenta uma "integração básica", que é Olá mínimo definido toocollect necessários dados e envia uma notificação por push. documentação de integração completa Olá pode ser encontrada no hello [integração do SDK do Mobile Engagement Windows Phone](mobile-engagement-windows-phone-sdk-overview.md)

Vamos criar um aplicativo básico com a integração do Visual Studio toodemonstrate hello.

### <a name="create-a-new-windows-phone-silverlight-project"></a>Criação de um novo projeto do Windows Phone Silverlight
Olá etapas a seguir pressupõem uso de saudação do Visual Studio 2015 que etapas Olá são semelhantes em versões anteriores do Visual Studio. 

1. Inicie o Visual Studio e em Olá **início** tela, selecione **novo projeto**.
2. No pop-up hello, selecione **Windows 8** -> **do Windows Phone** -> **aplicativo em branco (Windows Phone Silverlight)**. Preencha o aplicativo hello **nome** e **nome da solução**e, em seguida, clique em **Okey**.
   
    ![][1]
3. Você pode escolher tootarget ou **Windows Phone 8.0** ou **Windows Phone 8.1**.

Você criou um novo aplicativo do Windows Phone Silverlight para o qual integraremos Olá SDK do Azure Mobile Engagement.

### <a name="connect-your-app-toohello-mobile-engagement-backend"></a>Conectar seu back-end do aplicativo toohello Mobile Engagement
1. Instalar Olá [MicrosoftAzure.MobileEngagement] pacote nuget em seu projeto.
2. Abra `WMAppManifest.xml` (na pasta de propriedades de saudação) e certifique-se de seguir Olá é declarados (adicionado se eles não são) em Olá `<Capabilities />` marca:
   
        <Capability Name="ID_CAP_NETWORKING" />
        <Capability Name="ID_CAP_IDENTITY_DEVICE" />
   
    ![][2]
3. Cole a cadeia de caracteres de conexão de saudação que você copiou anteriormente para seu aplicativo do Mobile Engagement agora e colá-lo em Olá `Resources\EngagementConfiguration.xml` arquivo entre hello `<connectionString>` e `</connectionString>` marcas:
   
    ![][3]
4. Em Olá `App.xaml.cs` arquivo:
   
    a. Adicionar Olá `using` instrução:
   
            using Microsoft.Azure.Engagement;
   
    b. Inicializar Olá SDK no hello `Application_Launching` método:
   
            private void Application_Launching(object sender, LaunchingEventArgs e)
            {
              EngagementAgent.Instance.Init();
            }
   
    c. Inserir o seguinte Olá em hello `Application_Activated`:
   
            private void Application_Activated(object sender, ActivatedEventArgs e)
            {
               EngagementAgent.Instance.OnActivated(e);
            }

## <a id="monitor"></a>Habilitar monitoramento em tempo real
Em ordem toostart enviar dados e garantir que os usuários de saudação estão ativos, você deve enviar pelo menos uma tela (atividade) toohello Mobile Engagement backend.

1. Olá MainPage.xaml.cs, adiciona Olá `using` instrução:
   
        using Microsoft.Azure.Engagement;
2. Substitua a classe base Olá de **MainPage**, que é antes do **PhoneApplicationPage**, com **EngagementPage**.
   
        class MainPage : EngagementPage 
3. No arquivo `MainPage.xml`:
   
    a. Adicione declarações de namespaces tooyour:
   
            xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
   
    b. Substituir `phone:PhoneApplicationPage` no nome da marca XML Olá com `engagement:EngagementPage`.

## <a id="monitor"></a>Conectar o aplicativo com monitoramento em tempo real
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a>Habilitar notificações por push e mensagens no aplicativo
Mobile Engagement permite toointeract e alcançar seus usuários com notificações por Push e no aplicativo de mensagens do contexto de saudação de campanhas. Esse módulo é chamado alcance no portal do Mobile Engagement hello.
Olá seções a seguir configurar seu aplicativo tooreceive-los.

### <a name="enable-your-app-tooreceive-mpns-push-notifications"></a>Habilitar seu aplicativo tooreceive notificações por Push do MPNS
Adicionar novo tooyour de recursos `WMAppManifest.xml` arquivo:

        ID_CAP_PUSH_NOTIFICATION
        ID_CAP_WEBBROWSERCOMPONENT

   ![][5]

### <a name="initialize-hello-reach-sdk"></a>Inicializar Olá SDK do REACH
1. Em `App.xaml.cs`, chame `EngagementReach.Instance.Init();` em Olá **Application_Launching** função logo após a inicialização do agente de saudação:
   
        private void Application_Launching(object sender, LaunchingEventArgs e)
        {
           EngagementAgent.Instance.Init();
           EngagementReach.Instance.Init();
        }
2. Em `App.xaml.cs`, chame `EngagementReach.Instance.OnActivated(e);` em Olá **Application_Activated** função logo após a inicialização do agente de saudação:
   
        private void Application_Activated(object sender, ActivatedEventArgs e)
        {
           EngagementAgent.Instance.OnActivated(e);
           EngagementReach.Instance.OnActivated(e);
        }

Você está pronto. Agora vamos verificar se você criou corretamente essa integração básica.

## <a id="send"></a>Enviar um aplicativo de tooyour de notificação
[!INCLUDE [Create Windows Push campaign](../../includes/mobile-engagement-windows-push-campaign.md)]

Agora você verá uma notificação no seu dispositivo que serão exibidos como uma notificação no aplicativo se o aplicativo hello está aberto como uma notificação do sistema como Olá a seguir: 

![][6]

<!-- URLs. -->
[MicrosoftAzure.MobileEngagement]: http://go.microsoft.com/?linkid=9874664
[Mobile Engagement Windows Phone SDK documentation]: ../mobile-engagement-windows-phone-integrate-engagement/

<!-- Images. -->
[1]: ./media/mobile-engagement-windows-phone-get-started/project-properties.png
[2]: ./media/mobile-engagement-windows-phone-get-started/wmappmanifest-capabilities.png
[3]: ./media/mobile-engagement-windows-phone-get-started/add-connection-string.png
[5]: ./media/mobile-engagement-windows-phone-get-started/reach-capabilities.png
[6]: ./media/mobile-engagement-windows-phone-get-started/push-screenshot.png
