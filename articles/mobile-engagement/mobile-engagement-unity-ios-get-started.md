---
title: "aaaGet iniciado com o Azure Mobile Engagement para implantação de iOS do Unity"
description: "Saiba como toouse Azure Mobile Engagement com análises e notificações por Push para aplicativos do Unity Implantando tooiOS dispositivos."
services: mobile-engagement
documentationcenter: unity
author: piyushjo
manager: erikre
editor: 
ms.assetid: 7ddfbac3-8d13-4ebe-b061-c865f357297f
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-unity-ios
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: f4247b0a9240cbe2bf1a6618388919d3554c07fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-unity-ios-deployment"></a>Introdução ao Azure Mobile Engagement para implantação do Unity para iOS
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

Este tópico mostra como toouse do Azure Mobile Engagement toounderstand o uso de aplicativo e como toosend por push usuários de toosegmented de notificações de um aplicativo do Unity ao implantar o dispositivo iOS tooan.
Este tutorial usa Olá Roll-clássico Unity um tutorial de bola como Olá ponto de partida. Você deve seguir etapas Olá neste [tutorial](mobile-engagement-unity-roll-a-ball.md) antes de prosseguir com hello integração do Mobile Engagement é apresentar no tutorial de saudação abaixo. 

Este tutorial requer o seguinte hello:

* [Editor do Unity](http://unity3d.com/get-unity)
* [SDK do Unity do Mobile Engagement](https://aka.ms/azmeunitysdk)
* Editor do XCode

> [!NOTE]
> toocomplete neste tutorial, você deve ter uma conta ativa do Azure. Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos. Para obter detalhes, consulte [Avaliação Gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-unity-ios-get-started).
> 
> 

## <a id="setup-azme"></a>Configurar o Mobile Engagement para seu aplicativo iOS
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
1. Olá, abra **EngagementConfiguration** arquivo de script de Olá Olá de pasta e atualização do SDK **IOS\_conexão\_cadeia de caracteres** com a cadeia de caracteres de conexão de saudação obtidos anteriormente de saudação do portal do Azure.  
   
    ![][73]
2. Salve o arquivo hello. 

### <a name="configure-hello-app-for-basic-tracking"></a>Configurar aplicativo hello para básicas de rastreamento
1. Olá, abra **PlayerController** script anexado toohello objeto de Player para edição. 
2. Adicione o seguinte Olá usando a instrução:
   
        using Microsoft.Azure.Engagement.Unity;
3. Adicionar Olá após toohello `Start()` método
   
        EngagementAgent.Initialize();
        EngagementAgent.StartActivity("Home");

### <a name="deploy-and-run-hello-app"></a>Implantar e executar o aplicativo hello
1. Conecte-se uma máquina de tooyour do dispositivo iOS. 
2. Abra **Arquivo -> Configurações de Compilação** 
   
    ![][40]
3. Selecione **iOS**, em seguida, clique em **Alternar Plataforma**
   
    ![][41]
   
    ![][42]
4. Clique em **Configurações do jogador** e forneça um Identificador de Pacote válido. 
   
    ![][53]
5. Finalmente, clique em **Compilar e Executar**
   
    ![][54]
6. Você pode ser solicitado tooprovide um pacote de iOS pasta nome toostore hello. 
   
    ![][43]
7. Se tudo correr bem, projeto Olá será compilado, e abra-em seu aplicativo do XCode. 
8. Certifique-se de que Olá **identificador de pacote** está correto no projeto de saudação.  
   
    ![][75]
9. Agora execute o aplicativo hello no XCode para que o pacote de saudação é dispositivo conectado tooyour implantado e você deverá ver o jogo Unity em seu telefone! 

## <a id="monitor"></a>Conectar o aplicativo com monitoramento em tempo real
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a>Habilitar notificações por push e mensagens no aplicativo
Mobile Engagement permite toointeract com os usuários e o alcance com notificações por push e no aplicativo mensagens no contexto de saudação de campanhas. Esse módulo é chamado alcance no portal do Mobile Engagement hello.
Você não tem nenhuma configuração adicional de toodo em notificações de tooreceive seu aplicativo e ele já esteja configurado para ele.

[!INCLUDE [mobile-engagement-ios-send-push-push](../../includes/mobile-engagement-ios-send-push.md)]

<!-- Images. -->
[40]: ./media/mobile-engagement-unity-ios-get-started/40.png
[41]: ./media/mobile-engagement-unity-ios-get-started/41.png
[42]: ./media/mobile-engagement-unity-ios-get-started/42.png
[43]: ./media/mobile-engagement-unity-ios-get-started/43.png
[53]: ./media/mobile-engagement-unity-ios-get-started/53.png
[54]: ./media/mobile-engagement-unity-ios-get-started/54.png
[70]: ./media/mobile-engagement-unity-ios-get-started/70.png
[71]: ./media/mobile-engagement-unity-ios-get-started/71.png
[72]: ./media/mobile-engagement-unity-ios-get-started/72.png
[73]: ./media/mobile-engagement-unity-ios-get-started/73.png
[74]: ./media/mobile-engagement-unity-ios-get-started/74.png
[75]: ./media/mobile-engagement-unity-ios-get-started/75.png
