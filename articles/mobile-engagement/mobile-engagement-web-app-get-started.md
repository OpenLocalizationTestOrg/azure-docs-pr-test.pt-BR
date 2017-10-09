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
# <a name="get-started-with-azure-mobile-engagement-for-web-apps"></a><span data-ttu-id="b474a-103">Introdução ao Azure Mobile Engagement para Aplicativos Web</span><span class="sxs-lookup"><span data-stu-id="b474a-103">Get started with Azure Mobile Engagement for Web Apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="b474a-104">Este tópico mostra como toouse do Azure Mobile Engagement toounderstand o uso do aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="b474a-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your Web App usage.</span></span>

> [!NOTE]
> <span data-ttu-id="b474a-105">serviço do Azure Mobile Engagement Olá será descontinuado de 2018 março e está apenas disponível tooexisting clientes.</span><span class="sxs-lookup"><span data-stu-id="b474a-105">hello Azure Mobile Engagement service will be retired March 2018 and is currently only available tooexisting customers.</span></span> <span data-ttu-id="b474a-106">Para saber mais, confira [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span><span class="sxs-lookup"><span data-stu-id="b474a-106">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

<span data-ttu-id="b474a-107">Este tutorial requer o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="b474a-107">This tutorial requires hello following:</span></span>

* <span data-ttu-id="b474a-108">Visual Studio 2015 ou qualquer outro editor de sua escolha</span><span class="sxs-lookup"><span data-stu-id="b474a-108">Visual Studio 2015 or any other editor of your choice</span></span>
* [<span data-ttu-id="b474a-109">SDK da Web</span><span class="sxs-lookup"><span data-stu-id="b474a-109">Web SDK</span></span>](http://aka.ms/P7b453)

<span data-ttu-id="b474a-110">Esse SDK da Web está na visualização e só dá suporte a análises no momento de saudação e ainda não suporta enviadas notificações de push de navegador ou no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b474a-110">This Web SDK is in Preview and only supports Analytics at hello moment and doesn't support sending browser or in-app push notifications yet.</span></span> 

> [!NOTE]
> <span data-ttu-id="b474a-111">toocomplete neste tutorial, você deve ter uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="b474a-111">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="b474a-112">Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="b474a-112">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="b474a-113">Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-web-app-get-started).</span><span class="sxs-lookup"><span data-stu-id="b474a-113">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-web-app-get-started).</span></span>
> 
> 

## <a name="setup-mobile-engagement-for-your-web-app"></a><span data-ttu-id="b474a-114">Configurar o Mobile Engagement para seu aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="b474a-114">Setup Mobile Engagement for your Web app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="b474a-115"><a id="connecting-app"></a>Conectar seu back-end do aplicativo toohello Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="b474a-115"><a id="connecting-app"></a>Connect your app toohello Mobile Engagement backend</span></span>
<span data-ttu-id="b474a-116">Este tutorial apresenta uma "integração básica," que é Olá conjunto mínimo necessário toocollect dados.</span><span class="sxs-lookup"><span data-stu-id="b474a-116">This tutorial presents a "basic integration," which is hello minimal set required toocollect data.</span></span>

<span data-ttu-id="b474a-117">Vamos criar um aplicativo web básico com a integração do Visual Studio toodemonstrate Olá que você pode seguir as etapas de saudação com qualquer aplicativo web criado fora do Visual Studio também.</span><span class="sxs-lookup"><span data-stu-id="b474a-117">We will create a basic web app with Visual Studio toodemonstrate hello integration though you can follow hello steps with any web application created outside of Visual Studio also.</span></span> 

### <a name="create-a-new-web-app"></a><span data-ttu-id="b474a-118">Criar um novo aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="b474a-118">Create a new Web App</span></span>
<span data-ttu-id="b474a-119">Olá etapas a seguir pressupõem uso de saudação do Visual Studio 2015 que etapas Olá são semelhantes em versões anteriores do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b474a-119">hello following steps assume hello use of Visual Studio 2015 though hello steps are similar in earlier versions of Visual Studio.</span></span> 

1. <span data-ttu-id="b474a-120">Inicie o Visual Studio e em Olá **início** tela, selecione **novo projeto**.</span><span class="sxs-lookup"><span data-stu-id="b474a-120">Start Visual Studio, and in hello **Home** screen, select **New Project**.</span></span>
2. <span data-ttu-id="b474a-121">No pop-up hello, selecione **Web** -> **aplicativo Web ASP.Net**.</span><span class="sxs-lookup"><span data-stu-id="b474a-121">In hello pop-up, select **Web** -> **ASP.Net Web Application**.</span></span> <span data-ttu-id="b474a-122">Preencha o aplicativo hello **nome**, **local** e **nome da solução**e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="b474a-122">Fill in hello app **Name**, **Location** and  **Solution name**, and then click **OK**.</span></span>
3. <span data-ttu-id="b474a-123">Em Olá **selecionar um modelo de** pop-up, selecione **vazio** em **ASP.Net 4.5 modelos** e clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="b474a-123">In hello **Select a template** popup, select **Empty** under **ASP.Net 4.5 Templates** and click **OK**.</span></span> 

<span data-ttu-id="b474a-124">Você criou um novo projeto de aplicativo Web em branco no qual integraremos Olá Web SDK do Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="b474a-124">You have now created a new blank Web App project into which we will integrate hello Azure Mobile Engagement Web SDK.</span></span>

### <a name="connect-your-app-toomobile-engagement-backend"></a><span data-ttu-id="b474a-125">Conectar seu back-end do aplicativo tooMobile contrato</span><span class="sxs-lookup"><span data-stu-id="b474a-125">Connect your app tooMobile Engagement backend</span></span>
1. <span data-ttu-id="b474a-126">Criar uma nova pasta chamada **javascript** em sua solução e adicione o arquivo de Web SDK JS Olá **engagement.js azure** nele.</span><span class="sxs-lookup"><span data-stu-id="b474a-126">Create a new folder called **javascript** in your solution and add hello Web SDK JS file **azure-engagement.js** into it.</span></span> 
2. <span data-ttu-id="b474a-127">Adicionar um novo arquivo chamado **js** nesta pasta de javascript com hello código a seguir.</span><span class="sxs-lookup"><span data-stu-id="b474a-127">Add a new file called **main.js** in this javascript folder with hello following code.</span></span> <span data-ttu-id="b474a-128">Certifique-se de cadeia de conexão de saudação tooupdate.</span><span class="sxs-lookup"><span data-stu-id="b474a-128">Make sure tooupdate hello connection string.</span></span> <span data-ttu-id="b474a-129">Isso `azureEngagement` objeto será usado tooaccess métodos Web SDK.</span><span class="sxs-lookup"><span data-stu-id="b474a-129">This `azureEngagement` object will be used tooaccess Web SDK methods.</span></span> 
   
        var azureEngagement = {
            debug: true,
            connectionString: 'xxxxx'
        };
   
    ![Visual Studio com arquivos js][1]

## <a name="enable-real-time-monitoring"></a><span data-ttu-id="b474a-131">Habilitar o monitoramento em tempo real</span><span class="sxs-lookup"><span data-stu-id="b474a-131">Enable real-time monitoring</span></span>
<span data-ttu-id="b474a-132">Em ordem toostart enviar dados e garantir que os usuários de saudação estão ativos, você deve enviar pelo menos uma atividade toohello Mobile Engagement backend.</span><span class="sxs-lookup"><span data-stu-id="b474a-132">In order toostart sending data and ensuring that hello users are active, you must send at least one Activity toohello Mobile Engagement backend.</span></span> <span data-ttu-id="b474a-133">Uma atividade no contexto de saudação de um aplicativo web é uma página da web.</span><span class="sxs-lookup"><span data-stu-id="b474a-133">An activity in hello context of a web app is a web page.</span></span> 

1. <span data-ttu-id="b474a-134">Crie uma nova página chamada **home.html** em sua solução e é definido como a saudação inicial da página para seu aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="b474a-134">Create a new page called **home.html** in your solution and set it as hello starting page for your web app.</span></span> 
2. <span data-ttu-id="b474a-135">Inclua Olá dois javascripts que nós adicionados anteriormente nesta página adicionando Olá seguinte na marca de corpo de saudação.</span><span class="sxs-lookup"><span data-stu-id="b474a-135">Include hello two javascripts we added earlier in this page by adding hello following within hello body tag.</span></span> 
   
        <script type="text/javascript" src="javascript/main.js"></script>
        <script type="text/javascript" src="javascript/azure-engagement.js"></script>
3. <span data-ttu-id="b474a-136">Atualização do EngagementAgent do toocall marca body Olá `startActivity` método</span><span class="sxs-lookup"><span data-stu-id="b474a-136">Update hello body tag toocall EngagementAgent's `startActivity` method</span></span>
   
        <body onload="engagement.agent.startActivity('Home')">
4. <span data-ttu-id="b474a-137">Sua **home.html** ficará assim</span><span class="sxs-lookup"><span data-stu-id="b474a-137">Here is what your **home.html** will look like</span></span>
   
        <html>
        <head>
            ...
        </head>
        <body onload="engagement.agent.startActivity('Home')">
            <script type="text/javascript" src="javascript/main.js"></script>
            <script type="text/javascript" src="javascript/azure-engagement.js"></script>
        </body>
        </html>

## <a name="connect-app-with-real-time-monitoring"></a><span data-ttu-id="b474a-138">Conectar o aplicativo com monitoramento em tempo real</span><span class="sxs-lookup"><span data-stu-id="b474a-138">Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

  ![][2]

## <a name="extend-analytics"></a><span data-ttu-id="b474a-139">Estender a análise</span><span class="sxs-lookup"><span data-stu-id="b474a-139">Extend analytics</span></span>
<span data-ttu-id="b474a-140">Aqui estão todos os métodos de saudação disponível atualmente com o SDK da Web que você pode usar para análise:</span><span class="sxs-lookup"><span data-stu-id="b474a-140">Here are all hello methods currently available with Web SDK that you can use for analytics:</span></span>

1. <span data-ttu-id="b474a-141">Páginas de atividades/Web:</span><span class="sxs-lookup"><span data-stu-id="b474a-141">Activities/Web pages:</span></span>
   
        engagement.agent.startActivity(name);
        engagement.agent.endActivity();
2. <span data-ttu-id="b474a-142">Eventos</span><span class="sxs-lookup"><span data-stu-id="b474a-142">Events</span></span>
   
        engagement.agent.sendEvent(name, extras);
3. <span data-ttu-id="b474a-143">Erros</span><span class="sxs-lookup"><span data-stu-id="b474a-143">Errors</span></span>
   
        engagement.agent.sendError(name, extras);
4. <span data-ttu-id="b474a-144">Trabalhos</span><span class="sxs-lookup"><span data-stu-id="b474a-144">Jobs</span></span>
   
        engagement.agent.startJob(name);
        engagement.agent.endJob(name);

<!-- Images. -->
[1]: ./media/mobile-engagement-web-app-get-started/visual-studio-solution-js.png
[2]: ./media/mobile-engagement-web-app-get-started/session.png

