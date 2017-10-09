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
# <a name="get-started-with-azure-mobile-engagement-for-unity-android-deployment"></a><span data-ttu-id="155b3-103">Introdução ao Azure Mobile Engagement para implantação do Unity para Android</span><span class="sxs-lookup"><span data-stu-id="155b3-103">Get Started with Azure Mobile Engagement for Unity Android deployment</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="155b3-104">Este tópico mostra como toouse do Azure Mobile Engagement toounderstand o uso de aplicativo e como toosend por push usuários de toosegmented de notificações de um aplicativo do Unity durante a implantação de dispositivo Android tooan.</span><span class="sxs-lookup"><span data-stu-id="155b3-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and how toosend push notifications toosegmented users of a Unity application when deploying tooan Android device.</span></span>
<span data-ttu-id="155b3-105">Este tutorial usa Olá Roll-clássico Unity um tutorial de bola como Olá ponto de partida.</span><span class="sxs-lookup"><span data-stu-id="155b3-105">This tutorial uses hello classic Unity Roll a Ball tutorial as hello starting point.</span></span> <span data-ttu-id="155b3-106">Você deve seguir etapas Olá neste [tutorial](mobile-engagement-unity-roll-a-ball.md) antes de prosseguir com hello integração do Mobile Engagement é apresentar no tutorial de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="155b3-106">You should follow hello steps in this [tutorial](mobile-engagement-unity-roll-a-ball.md) before proceeding with hello Mobile Engagement integration we showcase in hello tutorial below.</span></span> 

<span data-ttu-id="155b3-107">Este tutorial requer o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="155b3-107">This tutorial requires hello following:</span></span>

* [<span data-ttu-id="155b3-108">Editor do Unity</span><span class="sxs-lookup"><span data-stu-id="155b3-108">Unity Editor</span></span>](http://unity3d.com/get-unity)
* [<span data-ttu-id="155b3-109">SDK do Unity do Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="155b3-109">Mobile Engagement Unity SDK</span></span>](https://aka.ms/azmeunitysdk)
* <span data-ttu-id="155b3-110">SDK do Android do Google</span><span class="sxs-lookup"><span data-stu-id="155b3-110">Google Android SDK</span></span>

> [!NOTE]
> <span data-ttu-id="155b3-111">toocomplete neste tutorial, você deve ter uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="155b3-111">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="155b3-112">Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="155b3-112">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="155b3-113">Para obter detalhes, consulte [Avaliação Gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-unity-android-get-started).</span><span class="sxs-lookup"><span data-stu-id="155b3-113">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-unity-android-get-started).</span></span>
> 
> 

## <span data-ttu-id="155b3-114"><a id="setup-azme"></a>Configuração do Mobile Engagement para seu aplicativo Android</span><span class="sxs-lookup"><span data-stu-id="155b3-114"><a id="setup-azme"></a>Setup Mobile Engagement for your Android app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="155b3-115"><a id="connecting-app"></a>Conectar seu back-end do aplicativo toohello Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="155b3-115"><a id="connecting-app"></a>Connect your app toohello Mobile Engagement backend</span></span>
### <a name="import-hello-unity-package"></a><span data-ttu-id="155b3-116">Importar o pacote do Unity Olá</span><span class="sxs-lookup"><span data-stu-id="155b3-116">Import hello Unity package</span></span>
1. <span data-ttu-id="155b3-117">Baixar Olá [pacote Mobile Engagement Unity](https://aka.ms/azmeunitysdk) e salve-o computador local tooyour.</span><span class="sxs-lookup"><span data-stu-id="155b3-117">Download hello [Mobile Engagement Unity package](https://aka.ms/azmeunitysdk) and save it tooyour local machine.</span></span> 
2. <span data-ttu-id="155b3-118">Vá muito**ativos -> Importar pacote -> pacote personalizado** e Olá Selecione pacote baixado na Olá acima etapa.</span><span class="sxs-lookup"><span data-stu-id="155b3-118">Go too**Assets -> Import Package -> Custom Package** and select hello package you downloaded in hello above step.</span></span> 
   
    ![][70] 
3. <span data-ttu-id="155b3-119">Verifique se todos os arquivos estão selecionados e clique no botão **Importar** .</span><span class="sxs-lookup"><span data-stu-id="155b3-119">Make sure all files are selected and click **Import** button.</span></span> 
   
    ![][71] 
4. <span data-ttu-id="155b3-120">Depois que a importação for bem-sucedida, você verá Olá importado SDK arquivos em seu projeto.</span><span class="sxs-lookup"><span data-stu-id="155b3-120">Once Import is successful, you will see hello imported SDK files in your project.</span></span>  
   
    ![][72] 

### <a name="update-hello-engagementconfiguration"></a><span data-ttu-id="155b3-121">Saudação de atualização EngagementConfiguration</span><span class="sxs-lookup"><span data-stu-id="155b3-121">Update hello EngagementConfiguration</span></span>
1. <span data-ttu-id="155b3-122">Olá, abra **EngagementConfiguration** arquivo de script de Olá Olá de pasta e atualização do SDK **ANDROID\_conexão\_cadeia de caracteres** com a cadeia de caracteres de conexão de saudação obtidos antes de saudação do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="155b3-122">Open up hello **EngagementConfiguration** script file from hello SDK folder and update hello **ANDROID\_CONNECTION\_STRING** with hello connection string you obtained earlier from hello Azure portal.</span></span>  
   
    ![][73]
2. <span data-ttu-id="155b3-123">Salve o arquivo hello</span><span class="sxs-lookup"><span data-stu-id="155b3-123">Save hello file</span></span> 
3. <span data-ttu-id="155b3-124">Execute **Arquivo -> Envolvimento -> Gerar Manifesto Android**.</span><span class="sxs-lookup"><span data-stu-id="155b3-124">Execute **File -> Engagement -> Generate Android Manifest**.</span></span> <span data-ttu-id="155b3-125">Esse é o plug-in de saudação adicionado por Olá SDK do Mobile Engagement e clicando nele atualizará automaticamente as configurações do projeto.</span><span class="sxs-lookup"><span data-stu-id="155b3-125">This is hello plugin added by hello Mobile Engagement SDK and clicking on it will automatically update your project settings.</span></span> 
   
    ![][74]

> [!IMPORTANT]
> <span data-ttu-id="155b3-126">Tornar tooexecute-se de que isso toda vez que você atualizar Olá **EngagementConfiguration** arquivo caso contrário, suas alterações não serão refletidas no aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="155b3-126">Make sure tooexecute this every time you update hello **EngagementConfiguration** file otherwise your changes will not be reflected in hello app.</span></span> 
> 
> 

### <a name="configure-hello-app-for-basic-tracking"></a><span data-ttu-id="155b3-127">Configurar aplicativo hello para básicas de rastreamento</span><span class="sxs-lookup"><span data-stu-id="155b3-127">Configure hello app for basic tracking</span></span>
1. <span data-ttu-id="155b3-128">Olá, abra **PlayerController** script anexado toohello objeto de Player para edição.</span><span class="sxs-lookup"><span data-stu-id="155b3-128">Open up hello **PlayerController** script attached toohello Player object for editing.</span></span> 
2. <span data-ttu-id="155b3-129">Adicione o seguinte Olá usando a instrução:</span><span class="sxs-lookup"><span data-stu-id="155b3-129">Add hello following using statement:</span></span>
   
        using Microsoft.Azure.Engagement.Unity;
3. <span data-ttu-id="155b3-130">Adicionar Olá após toohello `Start()` método</span><span class="sxs-lookup"><span data-stu-id="155b3-130">Add hello following toohello `Start()` method</span></span>
   
        EngagementAgent.Initialize();
        EngagementAgent.StartActivity("Home");

### <a name="deploy-and-run-hello-app"></a><span data-ttu-id="155b3-131">Implantar e executar o aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="155b3-131">Deploy and run hello app</span></span>
<span data-ttu-id="155b3-132">Certifique-se de que você tenha instalado em seu computador antes de tentar toodeploy este dispositivo do Unity aplicativo tooyour SDK do Android.</span><span class="sxs-lookup"><span data-stu-id="155b3-132">Make sure that you have Android SDK installed on your machine before attempting toodeploy this Unity app tooyour device.</span></span> 

1. <span data-ttu-id="155b3-133">Conecte-se uma máquina de tooyour dispositivo Android.</span><span class="sxs-lookup"><span data-stu-id="155b3-133">Connect an Android device tooyour machine.</span></span> 
2. <span data-ttu-id="155b3-134">Abra **Arquivo -> Configurações de Compilação**</span><span class="sxs-lookup"><span data-stu-id="155b3-134">Open up **File -> Build Settings**</span></span> 
   
    ![][40]
3. <span data-ttu-id="155b3-135">Selecione **Android**, em seguida, clique na **Alternar Plataforma**</span><span class="sxs-lookup"><span data-stu-id="155b3-135">Select **Android** and then click on **Switch Platform**</span></span>
   
    ![][51]
   
    ![][52]
4. <span data-ttu-id="155b3-136">Clique em **Configurações do jogador** e forneça um Identificador de Pacote válido.</span><span class="sxs-lookup"><span data-stu-id="155b3-136">Click on **Player settings** and provide a valid Bundle Identifier.</span></span> 
   
    ![][53]
5. <span data-ttu-id="155b3-137">Finalmente, clique em **Compilar e Executar**</span><span class="sxs-lookup"><span data-stu-id="155b3-137">Finally click on **Build And Run**</span></span>
   
    ![][54]
6. <span data-ttu-id="155b3-138">Você pode ser solicitado tooprovide um pacote Android Olá de toostore pasta nome.</span><span class="sxs-lookup"><span data-stu-id="155b3-138">You may be asked tooprovide a folder name toostore hello Android package.</span></span> 
7. <span data-ttu-id="155b3-139">Se tudo bem, vai pacote hello serão implantado tooyour conectado dispositivo e você verá o jogo Unity em seu telefone!</span><span class="sxs-lookup"><span data-stu-id="155b3-139">If everything goes fine, then hello package will be deployed tooyour connected device and you should see your Unity game on your phone!</span></span> 

## <span data-ttu-id="155b3-140"><a id="monitor"></a>Conectar o aplicativo com monitoramento em tempo real</span><span class="sxs-lookup"><span data-stu-id="155b3-140"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="155b3-141"><a id="integrate-push"></a>Habilitar notificações por push e mensagens no aplicativo</span><span class="sxs-lookup"><span data-stu-id="155b3-141"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
[!INCLUDE [Enable Google Cloud Messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

### <a name="update-hello-engagementconfiguration"></a><span data-ttu-id="155b3-142">Saudação de atualização EngagementConfiguration</span><span class="sxs-lookup"><span data-stu-id="155b3-142">Update hello EngagementConfiguration</span></span>
1. <span data-ttu-id="155b3-143">Olá, abra **EngagementConfiguration** arquivo de script de Olá Olá de pasta e atualização do SDK **ANDROID\_GOOGLE\_número** com hello **projeto do Google Número** é obtido anteriormente do portal do desenvolvedor do Google nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="155b3-143">Open up hello **EngagementConfiguration** script file from hello SDK folder and update hello **ANDROID\_GOOGLE\_NUMBER** with hello **Google Project Number** you obtained earlier from hello Google Cloud Developer portal.</span></span> <span data-ttu-id="155b3-144">Isso é uma cadeia de valor, portanto, certifique-se de que tooenclose-lo entre aspas duplas.</span><span class="sxs-lookup"><span data-stu-id="155b3-144">This is a string value so make sure tooenclose it in double quotes.</span></span> 
   
    ![][75]
2. <span data-ttu-id="155b3-145">Salve o arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="155b3-145">Save hello file.</span></span> 
3. <span data-ttu-id="155b3-146">Execute **Arquivo -> Envolvimento -> Gerar Manifesto Android**.</span><span class="sxs-lookup"><span data-stu-id="155b3-146">Execute **File -> Engagement -> Generate Android Manifest**.</span></span> <span data-ttu-id="155b3-147">Esse é o plug-in de saudação adicionado por Olá SDK do Mobile Engagement e clicando nele atualizará automaticamente as configurações do projeto.</span><span class="sxs-lookup"><span data-stu-id="155b3-147">This is hello plugin added by hello Mobile Engagement SDK and clicking on it will automatically update your project settings.</span></span> 
   
    ![][74]

### <a name="configure-hello-app-tooreceive-notifications"></a><span data-ttu-id="155b3-148">Configurar notificações de tooreceive aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="155b3-148">Configure hello app tooreceive notifications</span></span>
1. <span data-ttu-id="155b3-149">Olá, abra **PlayerController** script anexado toohello objeto de Player para edição.</span><span class="sxs-lookup"><span data-stu-id="155b3-149">Open up hello **PlayerController** script attached toohello Player object for editing.</span></span> 
2. <span data-ttu-id="155b3-150">Adicionar Olá após toohello `Start()` método</span><span class="sxs-lookup"><span data-stu-id="155b3-150">Add hello following toohello `Start()` method</span></span>
   
        EngagementReachAgent.Initialize();
3. <span data-ttu-id="155b3-151">Agora que hello aplicativo for atualizado, implantar e executar o aplicativo de saudação em um dispositivo por instruções de saudação fornecidas abaixo.</span><span class="sxs-lookup"><span data-stu-id="155b3-151">Now that hello app is updated, deploy and run hello app on a device per hello instructions provided below.</span></span> 

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
