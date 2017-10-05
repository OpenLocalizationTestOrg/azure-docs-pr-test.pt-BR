---
title: "Introdução ao Azure Mobile Engagement para implantação do Unity para iOS"
description: "Saiba como usar o Azure Mobile Engagement com Análises e Notificações por Push para aplicativos Unity implantados em dispositivos iOS."
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
ms.openlocfilehash: c8f50404771965ec636065346ac04e059d264c3d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-unity-ios-deployment"></a><span data-ttu-id="9a50d-103">Introdução ao Azure Mobile Engagement para implantação do Unity para iOS</span><span class="sxs-lookup"><span data-stu-id="9a50d-103">Get Started with Azure Mobile Engagement for Unity iOS deployment</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="9a50d-104">Este tópico mostra como usar o Azure Mobile Engagement para entender o uso de aplicativos e como enviar notificações por push a usuários segmentados de um aplicativo do Unity durante a implantação em um dispositivo iOS.</span><span class="sxs-lookup"><span data-stu-id="9a50d-104">This topic shows you how to use Azure Mobile Engagement to understand your app usage and how to send push notifications to segmented users of a Unity application when deploying to an iOS device.</span></span>
<span data-ttu-id="9a50d-105">Este tutorial usa o tutorial clássico Roll a Ball do Unity como ponto de partida.</span><span class="sxs-lookup"><span data-stu-id="9a50d-105">This tutorial uses the classic Unity Roll a Ball tutorial as the starting point.</span></span> <span data-ttu-id="9a50d-106">Você deve seguir as etapas deste [tutorial](mobile-engagement-unity-roll-a-ball.md) antes de prosseguir com a integração do Mobile Engagement que demonstramos no tutorial abaixo.</span><span class="sxs-lookup"><span data-stu-id="9a50d-106">You should follow the steps in this [tutorial](mobile-engagement-unity-roll-a-ball.md) before proceeding with the Mobile Engagement integration we showcase in the tutorial below.</span></span> 

<span data-ttu-id="9a50d-107">Este tutorial exige o seguinte:</span><span class="sxs-lookup"><span data-stu-id="9a50d-107">This tutorial requires the following:</span></span>

* [<span data-ttu-id="9a50d-108">Editor do Unity</span><span class="sxs-lookup"><span data-stu-id="9a50d-108">Unity Editor</span></span>](http://unity3d.com/get-unity)
* [<span data-ttu-id="9a50d-109">SDK do Unity do Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="9a50d-109">Mobile Engagement Unity SDK</span></span>](https://aka.ms/azmeunitysdk)
* <span data-ttu-id="9a50d-110">Editor do XCode</span><span class="sxs-lookup"><span data-stu-id="9a50d-110">XCode Editor</span></span>

> [!NOTE]
> <span data-ttu-id="9a50d-111">Para concluir este tutorial, você precisa ter uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="9a50d-111">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="9a50d-112">Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="9a50d-112">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="9a50d-113">Para obter detalhes, consulte [Avaliação Gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-unity-ios-get-started).</span><span class="sxs-lookup"><span data-stu-id="9a50d-113">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-unity-ios-get-started).</span></span>
> 
> 

## <span data-ttu-id="9a50d-114"><a id="setup-azme"></a>Configurar o Mobile Engagement para seu aplicativo iOS</span><span class="sxs-lookup"><span data-stu-id="9a50d-114"><a id="setup-azme"></a>Setup Mobile Engagement for your iOS app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="9a50d-115"><a id="connecting-app"></a>Conecte o seu aplicativo ao back-end do Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="9a50d-115"><a id="connecting-app"></a>Connect your app to the Mobile Engagement backend</span></span>
### <a name="import-the-unity-package"></a><span data-ttu-id="9a50d-116">Importar o pacote do Unity</span><span class="sxs-lookup"><span data-stu-id="9a50d-116">Import the Unity package</span></span>
1. <span data-ttu-id="9a50d-117">Baixe o [pacote do Unity do Mobile Engagement](https://aka.ms/azmeunitysdk) e salve-o em seu computador local.</span><span class="sxs-lookup"><span data-stu-id="9a50d-117">Download the [Mobile Engagement Unity package](https://aka.ms/azmeunitysdk) and save it to your local machine.</span></span> 
2. <span data-ttu-id="9a50d-118">Vá para **Ativos -> Importar Pacote -> Pacote Personalizado** e selecione o pacote que você baixou na etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="9a50d-118">Go to **Assets -> Import Package -> Custom Package** and select the package you downloaded in the above step.</span></span> 
   
    ![][70] 
3. <span data-ttu-id="9a50d-119">Verifique se todos os arquivos estão selecionados e clique no botão **Importar** .</span><span class="sxs-lookup"><span data-stu-id="9a50d-119">Make sure all files are selected and click **Import** button.</span></span> 
   
    ![][71] 
4. <span data-ttu-id="9a50d-120">Depois que a importação for bem-sucedida, você verá os arquivos importados do SDK em seu projeto.</span><span class="sxs-lookup"><span data-stu-id="9a50d-120">Once Import is successful, you will see the imported SDK files in your project.</span></span>  
   
    ![][72] 

### <a name="update-the-engagementconfiguration"></a><span data-ttu-id="9a50d-121">Atualizar o EngagementConfiguration</span><span class="sxs-lookup"><span data-stu-id="9a50d-121">Update the EngagementConfiguration</span></span>
1. <span data-ttu-id="9a50d-122">Abra o arquivo de script **EngagementConfiguration** na pasta SDK e atualize **IOS\_CONNECTION\_STRING** com a cadeia de conexão obtida anteriormente no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="9a50d-122">Open up the **EngagementConfiguration** script file from the SDK folder and update the **IOS\_CONNECTION\_STRING** with the connection string you obtained earlier from the Azure portal.</span></span>  
   
    ![][73]
2. <span data-ttu-id="9a50d-123">Salve o arquivo.</span><span class="sxs-lookup"><span data-stu-id="9a50d-123">Save the file.</span></span> 

### <a name="configure-the-app-for-basic-tracking"></a><span data-ttu-id="9a50d-124">Configurar o aplicativo para o 	acompanhamento básico</span><span class="sxs-lookup"><span data-stu-id="9a50d-124">Configure the app for basic tracking</span></span>
1. <span data-ttu-id="9a50d-125">Abra o script **PlayerController** anexado ao objeto Player para edição.</span><span class="sxs-lookup"><span data-stu-id="9a50d-125">Open up the **PlayerController** script attached to the Player object for editing.</span></span> 
2. <span data-ttu-id="9a50d-126">Adicione a seguinte instrução usando:</span><span class="sxs-lookup"><span data-stu-id="9a50d-126">Add the following using statement:</span></span>
   
        using Microsoft.Azure.Engagement.Unity;
3. <span data-ttu-id="9a50d-127">Adicione o seguinte ao método `Start()`</span><span class="sxs-lookup"><span data-stu-id="9a50d-127">Add the following to the `Start()` method</span></span>
   
        EngagementAgent.Initialize();
        EngagementAgent.StartActivity("Home");

### <a name="deploy-and-run-the-app"></a><span data-ttu-id="9a50d-128">Implantar e executar o aplicativo</span><span class="sxs-lookup"><span data-stu-id="9a50d-128">Deploy and run the app</span></span>
1. <span data-ttu-id="9a50d-129">Conecte um dispositivo iOS a seu computador.</span><span class="sxs-lookup"><span data-stu-id="9a50d-129">Connect an iOS device to your machine.</span></span> 
2. <span data-ttu-id="9a50d-130">Abra **Arquivo -> Configurações de Compilação**</span><span class="sxs-lookup"><span data-stu-id="9a50d-130">Open up **File -> Build Settings**</span></span> 
   
    ![][40]
3. <span data-ttu-id="9a50d-131">Selecione **iOS**, em seguida, clique em **Alternar Plataforma**</span><span class="sxs-lookup"><span data-stu-id="9a50d-131">Select **iOS** and then click on **Switch Platform**</span></span>
   
    ![][41]
   
    ![][42]
4. <span data-ttu-id="9a50d-132">Clique em **Configurações do jogador** e forneça um Identificador de Pacote válido.</span><span class="sxs-lookup"><span data-stu-id="9a50d-132">Click on **Player settings** and provide a valid Bundle Identifier.</span></span> 
   
    ![][53]
5. <span data-ttu-id="9a50d-133">Finalmente, clique em **Compilar e Executar**</span><span class="sxs-lookup"><span data-stu-id="9a50d-133">Finally click on **Build And Run**</span></span>
   
    ![][54]
6. <span data-ttu-id="9a50d-134">Você poderá ser solicitado a fornecer um nome de pasta para armazenar o pacote do iOS.</span><span class="sxs-lookup"><span data-stu-id="9a50d-134">You may be asked to provide a folder name to store the iOS package.</span></span> 
   
    ![][43]
7. <span data-ttu-id="9a50d-135">Se tudo correr bem, o projeto será compilado e você deverá abri-lo em seu aplicativo do XCode.</span><span class="sxs-lookup"><span data-stu-id="9a50d-135">If everything goes fine, then the project will be compiled and you should open it up on your XCode application.</span></span> 
8. <span data-ttu-id="9a50d-136">Verifique se o **Identificador de pacote** está correto no projeto.</span><span class="sxs-lookup"><span data-stu-id="9a50d-136">Make sure that the **Bundle identifier** is correct in the project.</span></span>  
   
    ![][75]
9. <span data-ttu-id="9a50d-137">Agora execute o aplicativo no XCode para que o pacote seja implantado em seu dispositivo conectado e você verá o jogo Unity em seu telefone!</span><span class="sxs-lookup"><span data-stu-id="9a50d-137">Now run the app in XCode so that the package is deployed to your connected device and you should see your Unity game on your phone!</span></span> 

## <span data-ttu-id="9a50d-138"><a id="monitor"></a>Conectar o aplicativo com monitoramento em tempo real</span><span class="sxs-lookup"><span data-stu-id="9a50d-138"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="9a50d-139"><a id="integrate-push"></a>Habilitar notificações por push e mensagens no aplicativo</span><span class="sxs-lookup"><span data-stu-id="9a50d-139"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="9a50d-140">O Mobile Engagement permite interagir com seus usuários e o REACH com notificações por push e mensagens no aplicativo no contexto das campanhas.</span><span class="sxs-lookup"><span data-stu-id="9a50d-140">Mobile Engagement allows you to interact with your users and REACH with push notifications and in-app messaging in the context of campaigns.</span></span> <span data-ttu-id="9a50d-141">Esse módulo é chamado REACH no portal do Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="9a50d-141">This module is called REACH in the Mobile Engagement portal.</span></span>
<span data-ttu-id="9a50d-142">Você não precisa fazer qualquer configuração adicional no aplicativo para receber notificações, e ele já está configurado para isso.</span><span class="sxs-lookup"><span data-stu-id="9a50d-142">You don't have to do any additional configuration in your app to receive notifications and it is already setup for it.</span></span>

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
