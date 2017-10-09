---
title: aaaGet iniciada com o Azure Mobile Engagement para aplicativos Web | Microsoft Docs
description: "Saiba como toouse do Azure Mobile Engagement com notificações de análise e enviar por push para aplicativos Web."
services: mobile-engagement
documentationcenter: Mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 04afe53a-4caf-4c80-bd75-20cc630cd75c
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: js
ms.topic: hero-article
ms.date: 06/01/2016
ms.author: piyushjo
ms.openlocfilehash: a84c96cac13bf3b85e72aef55da5c91693e1766c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-web-apps"></a>Introdução ao Azure Mobile Engagement para Aplicativos Web
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

Este tópico mostra como toouse do Azure Mobile Engagement toounderstand o uso do aplicativo Web.

> [!NOTE]
> serviço do Azure Mobile Engagement Olá será descontinuado de 2018 março e está apenas disponível tooexisting clientes. Para saber mais, confira [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).

Este tutorial requer o seguinte hello:

* Visual Studio 2015 ou qualquer outro editor de sua escolha
* [SDK da Web](http://aka.ms/P7b453)

Esse SDK da Web está na visualização e só dá suporte a análises no momento de saudação e ainda não suporta enviadas notificações de push de navegador ou no aplicativo. 

> [!NOTE]
> toocomplete neste tutorial, você deve ter uma conta ativa do Azure. Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos. Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-web-app-get-started).
> 
> 

## <a name="setup-mobile-engagement-for-your-web-app"></a>Configurar o Mobile Engagement para seu aplicativo Web
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a>Conectar seu back-end do aplicativo toohello Mobile Engagement
Este tutorial apresenta uma "integração básica," que é Olá conjunto mínimo necessário toocollect dados.

Vamos criar um aplicativo web básico com a integração do Visual Studio toodemonstrate Olá que você pode seguir as etapas de saudação com qualquer aplicativo web criado fora do Visual Studio também. 

### <a name="create-a-new-web-app"></a>Criar um novo aplicativo Web
Olá etapas a seguir pressupõem uso de saudação do Visual Studio 2015 que etapas Olá são semelhantes em versões anteriores do Visual Studio. 

1. Inicie o Visual Studio e em Olá **início** tela, selecione **novo projeto**.
2. No pop-up hello, selecione **Web** -> **aplicativo Web ASP.Net**. Preencha o aplicativo hello **nome**, **local** e **nome da solução**e, em seguida, clique em **Okey**.
3. Em Olá **selecionar um modelo de** pop-up, selecione **vazio** em **ASP.Net 4.5 modelos** e clique em **Okey**. 

Você criou um novo projeto de aplicativo Web em branco no qual integraremos Olá Web SDK do Azure Mobile Engagement.

### <a name="connect-your-app-toomobile-engagement-backend"></a>Conectar seu back-end do aplicativo tooMobile contrato
1. Criar uma nova pasta chamada **javascript** em sua solução e adicione o arquivo de Web SDK JS Olá **engagement.js azure** nele. 
2. Adicionar um novo arquivo chamado **js** nesta pasta de javascript com hello código a seguir. Certifique-se de cadeia de conexão de saudação tooupdate. Isso `azureEngagement` objeto será usado tooaccess métodos Web SDK. 
   
        var azureEngagement = {
            debug: true,
            connectionString: 'xxxxx'
        };
   
    ![Visual Studio com arquivos js][1]

## <a name="enable-real-time-monitoring"></a>Habilitar o monitoramento em tempo real
Em ordem toostart enviar dados e garantir que os usuários de saudação estão ativos, você deve enviar pelo menos uma atividade toohello Mobile Engagement backend. Uma atividade no contexto de saudação de um aplicativo web é uma página da web. 

1. Crie uma nova página chamada **home.html** em sua solução e é definido como a saudação inicial da página para seu aplicativo web. 
2. Inclua Olá dois javascripts que nós adicionados anteriormente nesta página adicionando Olá seguinte na marca de corpo de saudação. 
   
        <script type="text/javascript" src="javascript/main.js"></script>
        <script type="text/javascript" src="javascript/azure-engagement.js"></script>
3. Atualização do EngagementAgent do toocall marca body Olá `startActivity` método
   
        <body onload="engagement.agent.startActivity('Home')">
4. Sua **home.html** ficará assim
   
        <html>
        <head>
            ...
        </head>
        <body onload="engagement.agent.startActivity('Home')">
            <script type="text/javascript" src="javascript/main.js"></script>
            <script type="text/javascript" src="javascript/azure-engagement.js"></script>
        </body>
        </html>

## <a name="connect-app-with-real-time-monitoring"></a>Conectar o aplicativo com monitoramento em tempo real
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

  ![][2]

## <a name="extend-analytics"></a>Estender a análise
Aqui estão todos os métodos de saudação disponível atualmente com o SDK da Web que você pode usar para análise:

1. Páginas de atividades/Web:
   
        engagement.agent.startActivity(name);
        engagement.agent.endActivity();
2. Eventos
   
        engagement.agent.sendEvent(name, extras);
3. Erros
   
        engagement.agent.sendError(name, extras);
4. Trabalhos
   
        engagement.agent.startJob(name);
        engagement.agent.endJob(name);

<!-- Images. -->
[1]: ./media/mobile-engagement-web-app-get-started/visual-studio-solution-js.png
[2]: ./media/mobile-engagement-web-app-get-started/session.png

