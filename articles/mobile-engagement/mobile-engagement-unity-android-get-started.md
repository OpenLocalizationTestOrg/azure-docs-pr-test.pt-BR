---
title: "Introdução ao Azure Mobile Engagement para implantação do Unity para Android"
description: "Saiba como usar o Azure Mobile Engagement com Análises e Notificações por Push para aplicativos Unity implantados em dispositivos iOS."
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
ms.openlocfilehash: bf0b758159d475b4ed7eadb84227e4824e11ba86
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-unity-android-deployment"></a><span data-ttu-id="37f38-103">Introdução ao Azure Mobile Engagement para implantação do Unity para Android</span><span class="sxs-lookup"><span data-stu-id="37f38-103">Get Started with Azure Mobile Engagement for Unity Android deployment</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="37f38-104">Este tópico mostra como usar o Azure Mobile Engagement para entender o uso de aplicativos e como enviar notificações por push a usuários segmentados de um aplicativo do Unity durante a implantação em um dispositivo Android.</span><span class="sxs-lookup"><span data-stu-id="37f38-104">This topic shows you how to use Azure Mobile Engagement to understand your app usage and how to send push notifications to segmented users of a Unity application when deploying to an Android device.</span></span>
<span data-ttu-id="37f38-105">Este tutorial usa o tutorial clássico Roll a Ball do Unity como ponto de partida.</span><span class="sxs-lookup"><span data-stu-id="37f38-105">This tutorial uses the classic Unity Roll a Ball tutorial as the starting point.</span></span> <span data-ttu-id="37f38-106">Você deve seguir as etapas deste [tutorial](mobile-engagement-unity-roll-a-ball.md) antes de prosseguir com a integração do Mobile Engagement que demonstramos no tutorial abaixo.</span><span class="sxs-lookup"><span data-stu-id="37f38-106">You should follow the steps in this [tutorial](mobile-engagement-unity-roll-a-ball.md) before proceeding with the Mobile Engagement integration we showcase in the tutorial below.</span></span> 

<span data-ttu-id="37f38-107">Este tutorial exige o seguinte:</span><span class="sxs-lookup"><span data-stu-id="37f38-107">This tutorial requires the following:</span></span>

* [<span data-ttu-id="37f38-108">Editor do Unity</span><span class="sxs-lookup"><span data-stu-id="37f38-108">Unity Editor</span></span>](http://unity3d.com/get-unity)
* [<span data-ttu-id="37f38-109">SDK do Unity do Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="37f38-109">Mobile Engagement Unity SDK</span></span>](https://aka.ms/azmeunitysdk)
* <span data-ttu-id="37f38-110">SDK do Android do Google</span><span class="sxs-lookup"><span data-stu-id="37f38-110">Google Android SDK</span></span>

> [!NOTE]
> <span data-ttu-id="37f38-111">Para concluir este tutorial, você precisa ter uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="37f38-111">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="37f38-112">Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="37f38-112">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="37f38-113">Para obter detalhes, consulte [Avaliação Gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-unity-android-get-started).</span><span class="sxs-lookup"><span data-stu-id="37f38-113">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-unity-android-get-started).</span></span>
> 
> 

## <span data-ttu-id="37f38-114"><a id="setup-azme"></a>Configuração do Mobile Engagement para seu aplicativo Android</span><span class="sxs-lookup"><span data-stu-id="37f38-114"><a id="setup-azme"></a>Setup Mobile Engagement for your Android app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="37f38-115"><a id="connecting-app"></a>Conecte o seu aplicativo ao back-end do Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="37f38-115"><a id="connecting-app"></a>Connect your app to the Mobile Engagement backend</span></span>
### <a name="import-the-unity-package"></a><span data-ttu-id="37f38-116">Importar o pacote do Unity</span><span class="sxs-lookup"><span data-stu-id="37f38-116">Import the Unity package</span></span>
1. <span data-ttu-id="37f38-117">Baixe o [pacote do Unity do Mobile Engagement](https://aka.ms/azmeunitysdk) e salve-o em seu computador local.</span><span class="sxs-lookup"><span data-stu-id="37f38-117">Download the [Mobile Engagement Unity package](https://aka.ms/azmeunitysdk) and save it to your local machine.</span></span> 
2. <span data-ttu-id="37f38-118">Vá para **Ativos -> Importar Pacote -> Pacote Personalizado** e selecione o pacote que você baixou na etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="37f38-118">Go to **Assets -> Import Package -> Custom Package** and select the package you downloaded in the above step.</span></span> 
   
    ![][70] 
3. <span data-ttu-id="37f38-119">Verifique se todos os arquivos estão selecionados e clique no botão **Importar** .</span><span class="sxs-lookup"><span data-stu-id="37f38-119">Make sure all files are selected and click **Import** button.</span></span> 
   
    ![][71] 
4. <span data-ttu-id="37f38-120">Depois que a importação for bem-sucedida, você verá os arquivos importados do SDK em seu projeto.</span><span class="sxs-lookup"><span data-stu-id="37f38-120">Once Import is successful, you will see the imported SDK files in your project.</span></span>  
   
    ![][72] 

### <a name="update-the-engagementconfiguration"></a><span data-ttu-id="37f38-121">Atualizar o EngagementConfiguration</span><span class="sxs-lookup"><span data-stu-id="37f38-121">Update the EngagementConfiguration</span></span>
1. <span data-ttu-id="37f38-122">Abra o arquivo de script **EngagementConfiguration** na pasta SDK e atualize **ANDROID\_CONNECTION\_STRING** cadeia de conexão obtida anteriormente no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="37f38-122">Open up the **EngagementConfiguration** script file from the SDK folder and update the **ANDROID\_CONNECTION\_STRING** with the connection string you obtained earlier from the Azure portal.</span></span>  
   
    ![][73]
2. <span data-ttu-id="37f38-123">Salve o arquivo</span><span class="sxs-lookup"><span data-stu-id="37f38-123">Save the file</span></span> 
3. <span data-ttu-id="37f38-124">Execute **Arquivo -> Envolvimento -> Gerar Manifesto Android**.</span><span class="sxs-lookup"><span data-stu-id="37f38-124">Execute **File -> Engagement -> Generate Android Manifest**.</span></span> <span data-ttu-id="37f38-125">Esse é o plug-in adicionado pelo SDK do Mobile Engagement, e quando você clicar nele, isso atualizará automaticamente as configurações do projeto.</span><span class="sxs-lookup"><span data-stu-id="37f38-125">This is the plugin added by the Mobile Engagement SDK and clicking on it will automatically update your project settings.</span></span> 
   
    ![][74]

> [!IMPORTANT]
> <span data-ttu-id="37f38-126">Execute isso sempre que você atualizar o arquivo **EngagementConfiguration** , caso contrário, suas alterações não serão refletidas no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="37f38-126">Make sure to execute this every time you update the **EngagementConfiguration** file otherwise your changes will not be reflected in the app.</span></span> 
> 
> 

### <a name="configure-the-app-for-basic-tracking"></a><span data-ttu-id="37f38-127">Configurar o aplicativo para o 	acompanhamento básico</span><span class="sxs-lookup"><span data-stu-id="37f38-127">Configure the app for basic tracking</span></span>
1. <span data-ttu-id="37f38-128">Abra o script **PlayerController** anexado ao objeto Player para edição.</span><span class="sxs-lookup"><span data-stu-id="37f38-128">Open up the **PlayerController** script attached to the Player object for editing.</span></span> 
2. <span data-ttu-id="37f38-129">Adicione a seguinte instrução usando:</span><span class="sxs-lookup"><span data-stu-id="37f38-129">Add the following using statement:</span></span>
   
        using Microsoft.Azure.Engagement.Unity;
3. <span data-ttu-id="37f38-130">Adicione o seguinte ao método `Start()`</span><span class="sxs-lookup"><span data-stu-id="37f38-130">Add the following to the `Start()` method</span></span>
   
        EngagementAgent.Initialize();
        EngagementAgent.StartActivity("Home");

### <a name="deploy-and-run-the-app"></a><span data-ttu-id="37f38-131">Implantar e executar o aplicativo</span><span class="sxs-lookup"><span data-stu-id="37f38-131">Deploy and run the app</span></span>
<span data-ttu-id="37f38-132">Verifique se você tem o SDK do Android instalado no computador antes de tentar implantar esse aplicativo Unity em seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="37f38-132">Make sure that you have Android SDK installed on your machine before attempting to deploy this Unity app to your device.</span></span> 

1. <span data-ttu-id="37f38-133">Conecte um dispositivo Android a seu computador.</span><span class="sxs-lookup"><span data-stu-id="37f38-133">Connect an Android device to your machine.</span></span> 
2. <span data-ttu-id="37f38-134">Abra **Arquivo -> Configurações de Compilação**</span><span class="sxs-lookup"><span data-stu-id="37f38-134">Open up **File -> Build Settings**</span></span> 
   
    ![][40]
3. <span data-ttu-id="37f38-135">Selecione **Android**, em seguida, clique na **Alternar Plataforma**</span><span class="sxs-lookup"><span data-stu-id="37f38-135">Select **Android** and then click on **Switch Platform**</span></span>
   
    ![][51]
   
    ![][52]
4. <span data-ttu-id="37f38-136">Clique em **Configurações do jogador** e forneça um Identificador de Pacote válido.</span><span class="sxs-lookup"><span data-stu-id="37f38-136">Click on **Player settings** and provide a valid Bundle Identifier.</span></span> 
   
    ![][53]
5. <span data-ttu-id="37f38-137">Finalmente, clique em **Compilar e Executar**</span><span class="sxs-lookup"><span data-stu-id="37f38-137">Finally click on **Build And Run**</span></span>
   
    ![][54]
6. <span data-ttu-id="37f38-138">Você poderá ser solicitado a fornecer um nome de pasta para armazenar o pacote do Android.</span><span class="sxs-lookup"><span data-stu-id="37f38-138">You may be asked to provide a folder name to store the Android package.</span></span> 
7. <span data-ttu-id="37f38-139">Se tudo correr bem, o pacote será implantado no dispositivo conectado e você verá o jogo Unity em seu telefone!</span><span class="sxs-lookup"><span data-stu-id="37f38-139">If everything goes fine, then the package will be deployed to your connected device and you should see your Unity game on your phone!</span></span> 

## <span data-ttu-id="37f38-140"><a id="monitor"></a>Conectar o aplicativo com monitoramento em tempo real</span><span class="sxs-lookup"><span data-stu-id="37f38-140"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="37f38-141"><a id="integrate-push"></a>Habilitar notificações por push e mensagens no aplicativo</span><span class="sxs-lookup"><span data-stu-id="37f38-141"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
[!INCLUDE [Enable Google Cloud Messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

### <a name="update-the-engagementconfiguration"></a><span data-ttu-id="37f38-142">Atualizar o EngagementConfiguration</span><span class="sxs-lookup"><span data-stu-id="37f38-142">Update the EngagementConfiguration</span></span>
1. <span data-ttu-id="37f38-143">Abra o arquivo de script **EngagementConfiguration** na pasta SDK e atualize **ANDROID\_GOOGLE\_NUMBER** com o **Número do Projeto Google** obtido anteriormente do portal do Desenvolvedor de Nuvem do Google.</span><span class="sxs-lookup"><span data-stu-id="37f38-143">Open up the **EngagementConfiguration** script file from the SDK folder and update the **ANDROID\_GOOGLE\_NUMBER** with the **Google Project Number** you obtained earlier from the Google Cloud Developer portal.</span></span> <span data-ttu-id="37f38-144">Esse é um valor de cadeia de caracteres, assim, coloque-o entre aspas duplas.</span><span class="sxs-lookup"><span data-stu-id="37f38-144">This is a string value so make sure to enclose it in double quotes.</span></span> 
   
    ![][75]
2. <span data-ttu-id="37f38-145">Salve o arquivo.</span><span class="sxs-lookup"><span data-stu-id="37f38-145">Save the file.</span></span> 
3. <span data-ttu-id="37f38-146">Execute **Arquivo -> Envolvimento -> Gerar Manifesto Android**.</span><span class="sxs-lookup"><span data-stu-id="37f38-146">Execute **File -> Engagement -> Generate Android Manifest**.</span></span> <span data-ttu-id="37f38-147">Esse é o plug-in adicionado pelo SDK do Mobile Engagement, e quando você clicar nele, isso atualizará automaticamente as configurações do projeto.</span><span class="sxs-lookup"><span data-stu-id="37f38-147">This is the plugin added by the Mobile Engagement SDK and clicking on it will automatically update your project settings.</span></span> 
   
    ![][74]

### <a name="configure-the-app-to-receive-notifications"></a><span data-ttu-id="37f38-148">Configurar o aplicativo para receber notificações</span><span class="sxs-lookup"><span data-stu-id="37f38-148">Configure the app to receive notifications</span></span>
1. <span data-ttu-id="37f38-149">Abra o script **PlayerController** anexado ao objeto Player para edição.</span><span class="sxs-lookup"><span data-stu-id="37f38-149">Open up the **PlayerController** script attached to the Player object for editing.</span></span> 
2. <span data-ttu-id="37f38-150">Adicione o seguinte ao método `Start()`</span><span class="sxs-lookup"><span data-stu-id="37f38-150">Add the following to the `Start()` method</span></span>
   
        EngagementReachAgent.Initialize();
3. <span data-ttu-id="37f38-151">Agora que o aplicativo está atualizado, implante e execute o aplicativo em um dispositivo de acordo com as instruções abaixo.</span><span class="sxs-lookup"><span data-stu-id="37f38-151">Now that the app is updated, deploy and run the app on a device per the instructions provided below.</span></span> 

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
