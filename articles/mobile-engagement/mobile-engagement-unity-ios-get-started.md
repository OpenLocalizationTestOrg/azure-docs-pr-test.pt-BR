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
# <a name="get-started-with-azure-mobile-engagement-for-unity-ios-deployment"></a><span data-ttu-id="08b8e-103">Introdução ao Azure Mobile Engagement para implantação do Unity para iOS</span><span class="sxs-lookup"><span data-stu-id="08b8e-103">Get Started with Azure Mobile Engagement for Unity iOS deployment</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="08b8e-104">Este tópico mostra como toouse do Azure Mobile Engagement toounderstand o uso de aplicativo e como toosend por push usuários de toosegmented de notificações de um aplicativo do Unity ao implantar o dispositivo iOS tooan.</span><span class="sxs-lookup"><span data-stu-id="08b8e-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and how toosend push notifications toosegmented users of a Unity application when deploying tooan iOS device.</span></span>
<span data-ttu-id="08b8e-105">Este tutorial usa Olá Roll-clássico Unity um tutorial de bola como Olá ponto de partida.</span><span class="sxs-lookup"><span data-stu-id="08b8e-105">This tutorial uses hello classic Unity Roll a Ball tutorial as hello starting point.</span></span> <span data-ttu-id="08b8e-106">Você deve seguir etapas Olá neste [tutorial](mobile-engagement-unity-roll-a-ball.md) antes de prosseguir com hello integração do Mobile Engagement é apresentar no tutorial de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="08b8e-106">You should follow hello steps in this [tutorial](mobile-engagement-unity-roll-a-ball.md) before proceeding with hello Mobile Engagement integration we showcase in hello tutorial below.</span></span> 

<span data-ttu-id="08b8e-107">Este tutorial requer o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="08b8e-107">This tutorial requires hello following:</span></span>

* [<span data-ttu-id="08b8e-108">Editor do Unity</span><span class="sxs-lookup"><span data-stu-id="08b8e-108">Unity Editor</span></span>](http://unity3d.com/get-unity)
* [<span data-ttu-id="08b8e-109">SDK do Unity do Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="08b8e-109">Mobile Engagement Unity SDK</span></span>](https://aka.ms/azmeunitysdk)
* <span data-ttu-id="08b8e-110">Editor do XCode</span><span class="sxs-lookup"><span data-stu-id="08b8e-110">XCode Editor</span></span>

> [!NOTE]
> <span data-ttu-id="08b8e-111">toocomplete neste tutorial, você deve ter uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="08b8e-111">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="08b8e-112">Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="08b8e-112">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="08b8e-113">Para obter detalhes, consulte [Avaliação Gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-unity-ios-get-started).</span><span class="sxs-lookup"><span data-stu-id="08b8e-113">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-unity-ios-get-started).</span></span>
> 
> 

## <span data-ttu-id="08b8e-114"><a id="setup-azme"></a>Configurar o Mobile Engagement para seu aplicativo iOS</span><span class="sxs-lookup"><span data-stu-id="08b8e-114"><a id="setup-azme"></a>Setup Mobile Engagement for your iOS app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="08b8e-115"><a id="connecting-app"></a>Conectar seu back-end do aplicativo toohello Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="08b8e-115"><a id="connecting-app"></a>Connect your app toohello Mobile Engagement backend</span></span>
### <a name="import-hello-unity-package"></a><span data-ttu-id="08b8e-116">Importar o pacote do Unity Olá</span><span class="sxs-lookup"><span data-stu-id="08b8e-116">Import hello Unity package</span></span>
1. <span data-ttu-id="08b8e-117">Baixar Olá [pacote Mobile Engagement Unity](https://aka.ms/azmeunitysdk) e salve-o computador local tooyour.</span><span class="sxs-lookup"><span data-stu-id="08b8e-117">Download hello [Mobile Engagement Unity package](https://aka.ms/azmeunitysdk) and save it tooyour local machine.</span></span> 
2. <span data-ttu-id="08b8e-118">Vá muito**ativos -> Importar pacote -> pacote personalizado** e Olá Selecione pacote baixado na Olá acima etapa.</span><span class="sxs-lookup"><span data-stu-id="08b8e-118">Go too**Assets -> Import Package -> Custom Package** and select hello package you downloaded in hello above step.</span></span> 
   
    ![][70] 
3. <span data-ttu-id="08b8e-119">Verifique se todos os arquivos estão selecionados e clique no botão **Importar** .</span><span class="sxs-lookup"><span data-stu-id="08b8e-119">Make sure all files are selected and click **Import** button.</span></span> 
   
    ![][71] 
4. <span data-ttu-id="08b8e-120">Depois que a importação for bem-sucedida, você verá Olá importado SDK arquivos em seu projeto.</span><span class="sxs-lookup"><span data-stu-id="08b8e-120">Once Import is successful, you will see hello imported SDK files in your project.</span></span>  
   
    ![][72] 

### <a name="update-hello-engagementconfiguration"></a><span data-ttu-id="08b8e-121">Saudação de atualização EngagementConfiguration</span><span class="sxs-lookup"><span data-stu-id="08b8e-121">Update hello EngagementConfiguration</span></span>
1. <span data-ttu-id="08b8e-122">Olá, abra **EngagementConfiguration** arquivo de script de Olá Olá de pasta e atualização do SDK **IOS\_conexão\_cadeia de caracteres** com a cadeia de caracteres de conexão de saudação obtidos anteriormente de saudação do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="08b8e-122">Open up hello **EngagementConfiguration** script file from hello SDK folder and update hello **IOS\_CONNECTION\_STRING** with hello connection string you obtained earlier from hello Azure portal.</span></span>  
   
    ![][73]
2. <span data-ttu-id="08b8e-123">Salve o arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="08b8e-123">Save hello file.</span></span> 

### <a name="configure-hello-app-for-basic-tracking"></a><span data-ttu-id="08b8e-124">Configurar aplicativo hello para básicas de rastreamento</span><span class="sxs-lookup"><span data-stu-id="08b8e-124">Configure hello app for basic tracking</span></span>
1. <span data-ttu-id="08b8e-125">Olá, abra **PlayerController** script anexado toohello objeto de Player para edição.</span><span class="sxs-lookup"><span data-stu-id="08b8e-125">Open up hello **PlayerController** script attached toohello Player object for editing.</span></span> 
2. <span data-ttu-id="08b8e-126">Adicione o seguinte Olá usando a instrução:</span><span class="sxs-lookup"><span data-stu-id="08b8e-126">Add hello following using statement:</span></span>
   
        using Microsoft.Azure.Engagement.Unity;
3. <span data-ttu-id="08b8e-127">Adicionar Olá após toohello `Start()` método</span><span class="sxs-lookup"><span data-stu-id="08b8e-127">Add hello following toohello `Start()` method</span></span>
   
        EngagementAgent.Initialize();
        EngagementAgent.StartActivity("Home");

### <a name="deploy-and-run-hello-app"></a><span data-ttu-id="08b8e-128">Implantar e executar o aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="08b8e-128">Deploy and run hello app</span></span>
1. <span data-ttu-id="08b8e-129">Conecte-se uma máquina de tooyour do dispositivo iOS.</span><span class="sxs-lookup"><span data-stu-id="08b8e-129">Connect an iOS device tooyour machine.</span></span> 
2. <span data-ttu-id="08b8e-130">Abra **Arquivo -> Configurações de Compilação**</span><span class="sxs-lookup"><span data-stu-id="08b8e-130">Open up **File -> Build Settings**</span></span> 
   
    ![][40]
3. <span data-ttu-id="08b8e-131">Selecione **iOS**, em seguida, clique em **Alternar Plataforma**</span><span class="sxs-lookup"><span data-stu-id="08b8e-131">Select **iOS** and then click on **Switch Platform**</span></span>
   
    ![][41]
   
    ![][42]
4. <span data-ttu-id="08b8e-132">Clique em **Configurações do jogador** e forneça um Identificador de Pacote válido.</span><span class="sxs-lookup"><span data-stu-id="08b8e-132">Click on **Player settings** and provide a valid Bundle Identifier.</span></span> 
   
    ![][53]
5. <span data-ttu-id="08b8e-133">Finalmente, clique em **Compilar e Executar**</span><span class="sxs-lookup"><span data-stu-id="08b8e-133">Finally click on **Build And Run**</span></span>
   
    ![][54]
6. <span data-ttu-id="08b8e-134">Você pode ser solicitado tooprovide um pacote de iOS pasta nome toostore hello.</span><span class="sxs-lookup"><span data-stu-id="08b8e-134">You may be asked tooprovide a folder name toostore hello iOS package.</span></span> 
   
    ![][43]
7. <span data-ttu-id="08b8e-135">Se tudo correr bem, projeto Olá será compilado, e abra-em seu aplicativo do XCode.</span><span class="sxs-lookup"><span data-stu-id="08b8e-135">If everything goes fine, then hello project will be compiled and you should open it up on your XCode application.</span></span> 
8. <span data-ttu-id="08b8e-136">Certifique-se de que Olá **identificador de pacote** está correto no projeto de saudação.</span><span class="sxs-lookup"><span data-stu-id="08b8e-136">Make sure that hello **Bundle identifier** is correct in hello project.</span></span>  
   
    ![][75]
9. <span data-ttu-id="08b8e-137">Agora execute o aplicativo hello no XCode para que o pacote de saudação é dispositivo conectado tooyour implantado e você deverá ver o jogo Unity em seu telefone!</span><span class="sxs-lookup"><span data-stu-id="08b8e-137">Now run hello app in XCode so that hello package is deployed tooyour connected device and you should see your Unity game on your phone!</span></span> 

## <span data-ttu-id="08b8e-138"><a id="monitor"></a>Conectar o aplicativo com monitoramento em tempo real</span><span class="sxs-lookup"><span data-stu-id="08b8e-138"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="08b8e-139"><a id="integrate-push"></a>Habilitar notificações por push e mensagens no aplicativo</span><span class="sxs-lookup"><span data-stu-id="08b8e-139"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="08b8e-140">Mobile Engagement permite toointeract com os usuários e o alcance com notificações por push e no aplicativo mensagens no contexto de saudação de campanhas.</span><span class="sxs-lookup"><span data-stu-id="08b8e-140">Mobile Engagement allows you toointeract with your users and REACH with push notifications and in-app messaging in hello context of campaigns.</span></span> <span data-ttu-id="08b8e-141">Esse módulo é chamado alcance no portal do Mobile Engagement hello.</span><span class="sxs-lookup"><span data-stu-id="08b8e-141">This module is called REACH in hello Mobile Engagement portal.</span></span>
<span data-ttu-id="08b8e-142">Você não tem nenhuma configuração adicional de toodo em notificações de tooreceive seu aplicativo e ele já esteja configurado para ele.</span><span class="sxs-lookup"><span data-stu-id="08b8e-142">You don't have toodo any additional configuration in your app tooreceive notifications and it is already setup for it.</span></span>

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
