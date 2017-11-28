---
title: "Introdução ao Azure Mobile Engagement para os Aplicativos Web | Microsoft Docs"
description: "Saiba como usar o Azure Mobile Engagement com a análise e as notificações por push para os Aplicativos Web."
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
ms.openlocfilehash: abcb04e4e0a3ae4fdba3a4ded20b3846ac3b21e6
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-web-apps"></a><span data-ttu-id="d8378-103">Introdução ao Azure Mobile Engagement para Aplicativos Web</span><span class="sxs-lookup"><span data-stu-id="d8378-103">Get started with Azure Mobile Engagement for Web Apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="d8378-104">Este tópico mostra como usar o Azure Mobile Engagement para entender o uso do aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="d8378-104">This topic shows you how to use Azure Mobile Engagement to understand your Web App usage.</span></span>

> [!NOTE]
> <span data-ttu-id="d8378-105">O serviço Azure Mobile Engagement será desativado em março de 2018 e, no momento, está disponível somente para os clientes existentes.</span><span class="sxs-lookup"><span data-stu-id="d8378-105">The Azure Mobile Engagement service will be retired March 2018 and is currently only available to existing customers.</span></span> <span data-ttu-id="d8378-106">Para saber mais, confira [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span><span class="sxs-lookup"><span data-stu-id="d8378-106">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

<span data-ttu-id="d8378-107">Este tutorial exige o seguinte:</span><span class="sxs-lookup"><span data-stu-id="d8378-107">This tutorial requires the following:</span></span>

* <span data-ttu-id="d8378-108">Visual Studio 2015 ou qualquer outro editor de sua escolha</span><span class="sxs-lookup"><span data-stu-id="d8378-108">Visual Studio 2015 or any other editor of your choice</span></span>
* [<span data-ttu-id="d8378-109">SDK da Web</span><span class="sxs-lookup"><span data-stu-id="d8378-109">Web SDK</span></span>](http://aka.ms/P7b453)

<span data-ttu-id="d8378-110">Esse SDK da Web está na Visualização, só dá suporte à Análise no momento e ainda não suporta enviar notificações por push no aplicativo ou no navegador.</span><span class="sxs-lookup"><span data-stu-id="d8378-110">This Web SDK is in Preview and only supports Analytics at the moment and doesn't support sending browser or in-app push notifications yet.</span></span> 

> [!NOTE]
> <span data-ttu-id="d8378-111">Para concluir este tutorial, você precisa ter uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="d8378-111">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="d8378-112">Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="d8378-112">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="d8378-113">Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-web-app-get-started).</span><span class="sxs-lookup"><span data-stu-id="d8378-113">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-web-app-get-started).</span></span>
> 
> 

## <a name="setup-mobile-engagement-for-your-web-app"></a><span data-ttu-id="d8378-114">Configurar o Mobile Engagement para seu aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="d8378-114">Setup Mobile Engagement for your Web app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="d8378-115"><a id="connecting-app"></a>Conecte o seu aplicativo ao back-end do Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="d8378-115"><a id="connecting-app"></a>Connect your app to the Mobile Engagement backend</span></span>
<span data-ttu-id="d8378-116">Este tutorial apresenta uma "integração básica", que é o conjunto mínimo exigido para coletar dados.</span><span class="sxs-lookup"><span data-stu-id="d8378-116">This tutorial presents a "basic integration," which is the minimal set required to collect data.</span></span>

<span data-ttu-id="d8378-117">Criaremos um aplicativo Web básico com o Visual Studio para demonstrar a integração, embora você possa seguir as etapas com qualquer aplicativo Web criado fora do Visual Studio também.</span><span class="sxs-lookup"><span data-stu-id="d8378-117">We will create a basic web app with Visual Studio to demonstrate the integration though you can follow the steps with any web application created outside of Visual Studio also.</span></span> 

### <a name="create-a-new-web-app"></a><span data-ttu-id="d8378-118">Criar um novo aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="d8378-118">Create a new Web App</span></span>
<span data-ttu-id="d8378-119">As etapas a seguir pressupõem o uso do Visual Studio 2015, embora as etapas sejam semelhantes em versões anteriores do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d8378-119">The following steps assume the use of Visual Studio 2015 though the steps are similar in earlier versions of Visual Studio.</span></span> 

1. <span data-ttu-id="d8378-120">Inicie o Visual Studio e na tela **Início**, selecione **Novo Projeto**.</span><span class="sxs-lookup"><span data-stu-id="d8378-120">Start Visual Studio, and in the **Home** screen, select **New Project**.</span></span>
2. <span data-ttu-id="d8378-121">No menu pop-up, selecione **Web** -> **Aplicativo Web do ASP.Net**.</span><span class="sxs-lookup"><span data-stu-id="d8378-121">In the pop-up, select **Web** -> **ASP.Net Web Application**.</span></span> <span data-ttu-id="d8378-122">Preencha o **Nome** do aplicativo, **Local** e **Nome da solução**, em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="d8378-122">Fill in the app **Name**, **Location** and  **Solution name**, and then click **OK**.</span></span>
3. <span data-ttu-id="d8378-123">No pop-up **Selecionar um modelo**, selecione **Vazio** em **Modelos do ASP.Net 4.5** e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="d8378-123">In the **Select a template** popup, select **Empty** under **ASP.Net 4.5 Templates** and click **OK**.</span></span> 

<span data-ttu-id="d8378-124">Agora, você criou um novo projeto de Aplicativo Web em branco no qual integraremos o SDK do Azure Mobile Engagement da Web.</span><span class="sxs-lookup"><span data-stu-id="d8378-124">You have now created a new blank Web App project into which we will integrate the Azure Mobile Engagement Web SDK.</span></span>

### <a name="connect-your-app-to-mobile-engagement-backend"></a><span data-ttu-id="d8378-125">Conecte seu aplicativo ao back-end do Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="d8378-125">Connect your app to Mobile Engagement backend</span></span>
1. <span data-ttu-id="d8378-126">Crie uma nova pasta denominada **javascript** em sua solução e adicione o arquivo JS SDK da Web **azure-engagement.js** a ela.</span><span class="sxs-lookup"><span data-stu-id="d8378-126">Create a new folder called **javascript** in your solution and add the Web SDK JS file **azure-engagement.js** into it.</span></span> 
2. <span data-ttu-id="d8378-127">Adicione um novo arquivo denominado **main.js** a essa pasta javascript com o código a seguir.</span><span class="sxs-lookup"><span data-stu-id="d8378-127">Add a new file called **main.js** in this javascript folder with the following code.</span></span> <span data-ttu-id="d8378-128">Atualize a cadeia de conexão.</span><span class="sxs-lookup"><span data-stu-id="d8378-128">Make sure to update the connection string.</span></span> <span data-ttu-id="d8378-129">Este objeto `azureEngagement` será usado para acessar os métodos SDK da Web.</span><span class="sxs-lookup"><span data-stu-id="d8378-129">This `azureEngagement` object will be used to access Web SDK methods.</span></span> 
   
        var azureEngagement = {
            debug: true,
            connectionString: 'xxxxx'
        };
   
    ![Visual Studio com arquivos js][1]

## <a name="enable-real-time-monitoring"></a><span data-ttu-id="d8378-131">Habilitar o monitoramento em tempo real</span><span class="sxs-lookup"><span data-stu-id="d8378-131">Enable real-time monitoring</span></span>
<span data-ttu-id="d8378-132">Para começar a enviar dados e assegurar que os usuários estejam ativos, você deve enviar, pelo menos, uma Atividade para o back-end do Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="d8378-132">In order to start sending data and ensuring that the users are active, you must send at least one Activity to the Mobile Engagement backend.</span></span> <span data-ttu-id="d8378-133">Uma atividade no contexto de um aplicativo Web é uma página da Web.</span><span class="sxs-lookup"><span data-stu-id="d8378-133">An activity in the context of a web app is a web page.</span></span> 

1. <span data-ttu-id="d8378-134">Crie uma nova página denominada **home.html** em sua solução e configure-a como a página inicial de seu aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="d8378-134">Create a new page called **home.html** in your solution and set it as the starting page for your web app.</span></span> 
2. <span data-ttu-id="d8378-135">Inclua os dois javascripts adicionados anteriormente nesta página acrescentando o seguinte na marcação body.</span><span class="sxs-lookup"><span data-stu-id="d8378-135">Include the two javascripts we added earlier in this page by adding the following within the body tag.</span></span> 
   
        <script type="text/javascript" src="javascript/main.js"></script>
        <script type="text/javascript" src="javascript/azure-engagement.js"></script>
3. <span data-ttu-id="d8378-136">Atualize a marcação body para chamar o método `startActivity` do EngagementAgent</span><span class="sxs-lookup"><span data-stu-id="d8378-136">Update the body tag to call EngagementAgent's `startActivity` method</span></span>
   
        <body onload="engagement.agent.startActivity('Home')">
4. <span data-ttu-id="d8378-137">Sua **home.html** ficará assim</span><span class="sxs-lookup"><span data-stu-id="d8378-137">Here is what your **home.html** will look like</span></span>
   
        <html>
        <head>
            ...
        </head>
        <body onload="engagement.agent.startActivity('Home')">
            <script type="text/javascript" src="javascript/main.js"></script>
            <script type="text/javascript" src="javascript/azure-engagement.js"></script>
        </body>
        </html>

## <a name="connect-app-with-real-time-monitoring"></a><span data-ttu-id="d8378-138">Conectar o aplicativo com monitoramento em tempo real</span><span class="sxs-lookup"><span data-stu-id="d8378-138">Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

  ![][2]

## <a name="extend-analytics"></a><span data-ttu-id="d8378-139">Estender a análise</span><span class="sxs-lookup"><span data-stu-id="d8378-139">Extend analytics</span></span>
<span data-ttu-id="d8378-140">Aqui estão todos os métodos disponíveis no momento com o SDK da Web que você pode usar para a análise:</span><span class="sxs-lookup"><span data-stu-id="d8378-140">Here are all the methods currently available with Web SDK that you can use for analytics:</span></span>

1. <span data-ttu-id="d8378-141">Páginas de atividades/Web:</span><span class="sxs-lookup"><span data-stu-id="d8378-141">Activities/Web pages:</span></span>
   
        engagement.agent.startActivity(name);
        engagement.agent.endActivity();
2. <span data-ttu-id="d8378-142">Eventos</span><span class="sxs-lookup"><span data-stu-id="d8378-142">Events</span></span>
   
        engagement.agent.sendEvent(name, extras);
3. <span data-ttu-id="d8378-143">Erros</span><span class="sxs-lookup"><span data-stu-id="d8378-143">Errors</span></span>
   
        engagement.agent.sendError(name, extras);
4. <span data-ttu-id="d8378-144">Trabalhos</span><span class="sxs-lookup"><span data-stu-id="d8378-144">Jobs</span></span>
   
        engagement.agent.startJob(name);
        engagement.agent.endJob(name);

<!-- Images. -->
[1]: ./media/mobile-engagement-web-app-get-started/visual-studio-solution-js.png
[2]: ./media/mobile-engagement-web-app-get-started/session.png

