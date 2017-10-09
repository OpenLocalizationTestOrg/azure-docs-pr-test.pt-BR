---
title: "aaaGet iniciado com o Azure Mobile Engagement para Android Unity implantação"
description: "Saiba como toouse Azure Mobile Engagement com análises e notificações por Push para aplicativos do Unity Implantando tooiOS dispositivos."
services: mobile-engagement
documentationcenter: unity
author: piyushjo
manager: erikre
editor: 
ms.assetid: d5f0ef79-be00-4cec-97a5-a0b2fdaa380e
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-unity-android
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: c4d34691daeb7544b11c2d6895b2474af0f902b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-unity-android-deployment"></a>Introdução ao Azure Mobile Engagement para implantação do Unity para Android
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

Este tópico mostra como toouse do Azure Mobile Engagement toounderstand o uso de aplicativo e como toosend por push usuários de toosegmented de notificações de um aplicativo do Unity durante a implantação de dispositivo Android tooan.
Este tutorial usa Olá Roll-clássico Unity um tutorial de bola como Olá ponto de partida. Você deve seguir etapas Olá neste [tutorial](mobile-engagement-unity-roll-a-ball.md) antes de prosseguir com hello integração do Mobile Engagement é apresentar no tutorial de saudação abaixo. 

Este tutorial requer o seguinte hello:

* [Editor do Unity](http://unity3d.com/get-unity)
* [SDK do Unity do Mobile Engagement](https://aka.ms/azmeunitysdk)
* SDK do Android do Google

> [!NOTE]
> toocomplete neste tutorial, você deve ter uma conta ativa do Azure. Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos. Para obter detalhes, consulte [Avaliação Gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-unity-android-get-started).
> 
> 

## <a id="setup-azme"></a>Configuração do Mobile Engagement para seu aplicativo Android
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a>Conectar seu back-end do aplicativo toohello Mobile Engagement
### <a name="import-hello-unity-package"></a>Importar o pacote do Unity Olá
1. Baixar Olá [pacote Mobile Engagement Unity](https://aka.ms/azmeunitysdk) e salve-o computador local tooyour. 
2. Vá muito**ativos -> Importar pacote -> pacote personalizado** e Olá Selecione pacote baixado na Olá acima etapa. 
   
    ![][70] 
3. Verifique se todos os arquivos estão selecionados e clique no botão **Importar** . 
   
    ![][71] 
4. Depois que a importação for bem-sucedida, você verá Olá importado SDK arquivos em seu projeto.  
   
    ![][72] 

### <a name="update-hello-engagementconfiguration"></a>Saudação de atualização EngagementConfiguration
1. Olá, abra **EngagementConfiguration** arquivo de script de Olá Olá de pasta e atualização do SDK **ANDROID\_conexão\_cadeia de caracteres** com a cadeia de caracteres de conexão de saudação obtidos antes de saudação do portal do Azure.  
   
    ![][73]
2. Salve o arquivo hello 
3. Execute **Arquivo -> Envolvimento -> Gerar Manifesto Android**. Esse é o plug-in de saudação adicionado por Olá SDK do Mobile Engagement e clicando nele atualizará automaticamente as configurações do projeto. 
   
    ![][74]

> [!IMPORTANT]
> Tornar tooexecute-se de que isso toda vez que você atualizar Olá **EngagementConfiguration** arquivo caso contrário, suas alterações não serão refletidas no aplicativo hello. 
> 
> 

### <a name="configure-hello-app-for-basic-tracking"></a>Configurar aplicativo hello para básicas de rastreamento
1. Olá, abra **PlayerController** script anexado toohello objeto de Player para edição. 
2. Adicione o seguinte Olá usando a instrução:
   
        using Microsoft.Azure.Engagement.Unity;
3. Adicionar Olá após toohello `Start()` método
   
        EngagementAgent.Initialize();
        EngagementAgent.StartActivity("Home");

### <a name="deploy-and-run-hello-app"></a>Implantar e executar o aplicativo hello
Certifique-se de que você tenha instalado em seu computador antes de tentar toodeploy este dispositivo do Unity aplicativo tooyour SDK do Android. 

1. Conecte-se uma máquina de tooyour dispositivo Android. 
2. Abra **Arquivo -> Configurações de Compilação** 
   
    ![][40]
3. Selecione **Android**, em seguida, clique na **Alternar Plataforma**
   
    ![][51]
   
    ![][52]
4. Clique em **Configurações do jogador** e forneça um Identificador de Pacote válido. 
   
    ![][53]
5. Finalmente, clique em **Compilar e Executar**
   
    ![][54]
6. Você pode ser solicitado tooprovide um pacote Android Olá de toostore pasta nome. 
7. Se tudo bem, vai pacote hello serão implantado tooyour conectado dispositivo e você verá o jogo Unity em seu telefone! 

## <a id="monitor"></a>Conectar o aplicativo com monitoramento em tempo real
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a>Habilitar notificações por push e mensagens no aplicativo
[!INCLUDE [Enable Google Cloud Messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

### <a name="update-hello-engagementconfiguration"></a>Saudação de atualização EngagementConfiguration
1. Olá, abra **EngagementConfiguration** arquivo de script de Olá Olá de pasta e atualização do SDK **ANDROID\_GOOGLE\_número** com hello **projeto do Google Número** é obtido anteriormente do portal do desenvolvedor do Google nuvem hello. Isso é uma cadeia de valor, portanto, certifique-se de que tooenclose-lo entre aspas duplas. 
   
    ![][75]
2. Salve o arquivo hello. 
3. Execute **Arquivo -> Envolvimento -> Gerar Manifesto Android**. Esse é o plug-in de saudação adicionado por Olá SDK do Mobile Engagement e clicando nele atualizará automaticamente as configurações do projeto. 
   
    ![][74]

### <a name="configure-hello-app-tooreceive-notifications"></a>Configurar notificações de tooreceive aplicativo hello
1. Olá, abra **PlayerController** script anexado toohello objeto de Player para edição. 
2. Adicionar Olá após toohello `Start()` método
   
        EngagementReachAgent.Initialize();
3. Agora que hello aplicativo for atualizado, implantar e executar o aplicativo de saudação em um dispositivo por instruções de saudação fornecidas abaixo. 

[!INCLUDE [Send notification from portal](../../includes/mobile-engagement-android-send-push-from-portal.md)]

<!-- Images -->
[40]: ./media/mobile-engagement-unity-android-get-started/40.png
[70]: ./media/mobile-engagement-unity-android-get-started/70.png
[71]: ./media/mobile-engagement-unity-android-get-started/71.png
[72]: ./media/mobile-engagement-unity-android-get-started/72.png
[73]: ./media/mobile-engagement-unity-android-get-started/73.png
[74]: ./media/mobile-engagement-unity-android-get-started/74.png
[75]: ./media/mobile-engagement-unity-android-get-started/75.png
[51]: ./media/mobile-engagement-unity-android-get-started/51.png
[52]: ./media/mobile-engagement-unity-android-get-started/52.png
[53]: ./media/mobile-engagement-unity-android-get-started/53.png
[54]: ./media/mobile-engagement-unity-android-get-started/54.png
