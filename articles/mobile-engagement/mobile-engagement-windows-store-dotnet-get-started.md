---
title: aaaGet iniciado com o Windows Universal aplicativos do Azure Mobile Engagement
description: "Saiba como toouse do Azure Mobile Engagement com notificações de análise e enviar por push para aplicativos Universal do Windows."
services: mobile-engagement
documentationcenter: windows
author: piyushjo
manager: erikre
editor: 
ms.assetid: 48103867-7f64-4646-b019-42bd797d38e2
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/12/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: 8224a6d3789cfe4784bbc9472005f9eddb94a8b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-windows-universal-apps"></a><span data-ttu-id="94c56-103">Introdução ao Azure Mobile Engagement para aplicativos universais do Windows</span><span class="sxs-lookup"><span data-stu-id="94c56-103">Get started with Azure Mobile Engagement for Windows Universal Apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="94c56-104">Este tópico mostra como toouse do Azure Mobile Engagement toounderstand seu uso do aplicativo e enviar por push usuários de toosegmented de notificações de um aplicativo Universal do Windows.</span><span class="sxs-lookup"><span data-stu-id="94c56-104">This topic shows you how toouse Azure Mobile Engagement toounderstand your app usage and send push notifications toosegmented users of a Windows Universal application.</span></span>
<span data-ttu-id="94c56-105">Este tutorial demonstra Olá cenário difusão simples usando o Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="94c56-105">This tutorial demonstrates hello simple broadcast scenario using Mobile Engagement.</span></span> <span data-ttu-id="94c56-106">Você cria um Aplicativo Windows Universal em branco que coleta os dados básicos de uso do aplicativo e recebe notificações por push usando o Serviço de Notificação do Windows (WNS).</span><span class="sxs-lookup"><span data-stu-id="94c56-106">You create a blank Windows Universal App that collects basic app usage data and receives push notifications using Windows Notification Service (WNS).</span></span>

> [!NOTE]
> <span data-ttu-id="94c56-107">serviço do Azure Mobile Engagement Olá será descontinuado de 2018 março e está apenas disponível tooexisting clientes.</span><span class="sxs-lookup"><span data-stu-id="94c56-107">hello Azure Mobile Engagement service will be retired March 2018 and is currently only available tooexisting customers.</span></span> <span data-ttu-id="94c56-108">Para saber mais, confira [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span><span class="sxs-lookup"><span data-stu-id="94c56-108">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="94c56-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="94c56-109">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-windows-store-prereqs.md)]

## <a name="set-up-mobile-engagement-for-your-windows-universal-app"></a><span data-ttu-id="94c56-110">Configurar o Mobile Engagement para seu aplicativo Windows Universal</span><span class="sxs-lookup"><span data-stu-id="94c56-110">Set up Mobile Engagement for your Windows Universal app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="94c56-111"><a id="connecting-app"></a>Conectar seu back-end do aplicativo toohello Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="94c56-111"><a id="connecting-app"></a>Connect your app toohello Mobile Engagement backend</span></span>
<span data-ttu-id="94c56-112">Este tutorial apresenta uma "integração básica," hello mínimo definido toocollect necessários dados e envia uma notificação por push.</span><span class="sxs-lookup"><span data-stu-id="94c56-112">This tutorial presents a "basic integration," which is hello minimal set required toocollect data and send a push notification.</span></span> <span data-ttu-id="94c56-113">documentação de integração completa Olá pode ser encontrada no hello [integração do SDK do Mobile Engagement Windows Universal](mobile-engagement-windows-store-sdk-overview.md).</span><span class="sxs-lookup"><span data-stu-id="94c56-113">hello complete integration documentation can be found in hello [Mobile Engagement Windows Universal SDK integration](mobile-engagement-windows-store-sdk-overview.md).</span></span>

<span data-ttu-id="94c56-114">Você pode criar um aplicativo básico com a integração do Visual Studio toodemonstrate hello.</span><span class="sxs-lookup"><span data-stu-id="94c56-114">You create a basic app with Visual Studio toodemonstrate hello integration.</span></span>

### <a name="create-a-windows-universal-app-project"></a><span data-ttu-id="94c56-115">Criar um projeto de Aplicativo Windows Universal</span><span class="sxs-lookup"><span data-stu-id="94c56-115">Create a Windows Universal App project</span></span>
<span data-ttu-id="94c56-116">Olá etapas a seguir pressupõem uso de saudação do Visual Studio 2015 que etapas Olá são semelhantes em versões anteriores do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="94c56-116">hello following steps assume hello use of Visual Studio 2015 though hello steps are similar in earlier versions of Visual Studio.</span></span>

1. <span data-ttu-id="94c56-117">Inicie o Visual Studio e em Olá **início** tela, selecione **novo projeto**.</span><span class="sxs-lookup"><span data-stu-id="94c56-117">Start Visual Studio, and in hello **Home** screen, select **New Project**.</span></span>
2. <span data-ttu-id="94c56-118">No pop-up hello, selecione **Windows** -> **Universal** -> **(Universal do Windows) do aplicativo em branco**.</span><span class="sxs-lookup"><span data-stu-id="94c56-118">In hello pop-up, select **Windows** -> **Universal** -> **Blank App (Universal Windows)**.</span></span> <span data-ttu-id="94c56-119">Preencha o aplicativo hello **nome** e **nome da solução**e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="94c56-119">Fill in hello app **Name** and **Solution name**, and then click **OK**.</span></span>

    ![][1]

<span data-ttu-id="94c56-120">Você criou um projeto de aplicativo Universal do Windows na qual você integrar lado Olá SDK do Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="94c56-120">You have now created a Windows Universal App project into which you next integrate hello Azure Mobile Engagement SDK.</span></span>

### <a name="connect-your-app-toomobile-engagement-backend"></a><span data-ttu-id="94c56-121">Conectar seu back-end do aplicativo tooMobile contrato</span><span class="sxs-lookup"><span data-stu-id="94c56-121">Connect your app tooMobile Engagement backend</span></span>
1. <span data-ttu-id="94c56-122">Instalar Olá [MicrosoftAzure.MobileEngagement] pacote Nuget em seu projeto.</span><span class="sxs-lookup"><span data-stu-id="94c56-122">Install hello [MicrosoftAzure.MobileEngagement] Nuget package in your project.</span></span> <span data-ttu-id="94c56-123">Se você estiver direcionando plataformas Windows e Windows Phone, você precisa toodo isso para os dois projetos.</span><span class="sxs-lookup"><span data-stu-id="94c56-123">If you are targeting both Windows and Windows Phone platforms, you need toodo this for both projects.</span></span> <span data-ttu-id="94c56-124">Para o Windows 8. x e Windows Phone 8.1, Olá mesmo Nuget pacote casas Olá correto específico da plataforma binários em cada projeto.</span><span class="sxs-lookup"><span data-stu-id="94c56-124">For Windows 8.x and Windows Phone 8.1, hello same Nuget package places hello correct platform-specific binaries in each project.</span></span>
2. <span data-ttu-id="94c56-125">Abra **Package. appxmanifest** e certifique-se de que Olá funcionalidade a seguir é adicionada existe:</span><span class="sxs-lookup"><span data-stu-id="94c56-125">Open **Package.appxmanifest** and make sure that hello following capability is added there:</span></span>

        Internet (Client)

    ![][2]
3. <span data-ttu-id="94c56-126">Copiar a cadeia de caracteres de conexão de saudação que você copiou anteriormente para seu aplicativo do Mobile Engagement agora e colá-lo em Olá `Resources\EngagementConfiguration.xml` arquivo entre hello `<connectionString>` e `</connectionString>` marcas:</span><span class="sxs-lookup"><span data-stu-id="94c56-126">Now copy hello connection string that you copied earlier for your Mobile Engagement App and paste it in hello `Resources\EngagementConfiguration.xml` file, between hello `<connectionString>` and `</connectionString>` tags:</span></span>

    ![][3]

    > [!TIP]
    > <span data-ttu-id="94c56-127">Se seu aplicativo for destinado para as plataformas Windows e Windows Phone, você ainda deverá criar dois Aplicativos do Mobile Engagement - um para cada plataforma com suporte.</span><span class="sxs-lookup"><span data-stu-id="94c56-127">If your App targets both Windows and Windows Phone platforms, you should still create two Mobile Engagement Applications - one for each supported platform.</span></span> <span data-ttu-id="94c56-128">Ter dois aplicativos garante que você pode criar segmentação correta do público-alvo hello e pode enviar notificações de destino corretamente para cada plataforma.</span><span class="sxs-lookup"><span data-stu-id="94c56-128">Having two apps ensures that you can create correct segmentation of hello audience and can send appropriately targeted notifications for each platform.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="94c56-129">NuGet não copiar recursos do SDK Olá automaticamente em seu aplicativo de UWP do Windows 10.</span><span class="sxs-lookup"><span data-stu-id="94c56-129">NuGet does not automatically copy hello SDK resources in your Windows 10 UWP application.</span></span> <span data-ttu-id="94c56-130">Você tem toodo-o manualmente após a etapas Olá que aparecem (Leiame. txt) quando o pacote do Nuget hello está instalado.</span><span class="sxs-lookup"><span data-stu-id="94c56-130">You have toodo it manually following hello steps which show up (readme.txt) when hello Nuget package is installed.</span></span>  

1. <span data-ttu-id="94c56-131">Em Olá `App.xaml.cs` arquivo:</span><span class="sxs-lookup"><span data-stu-id="94c56-131">In hello `App.xaml.cs` file:</span></span>

    <span data-ttu-id="94c56-132">a.</span><span class="sxs-lookup"><span data-stu-id="94c56-132">a.</span></span> <span data-ttu-id="94c56-133">Adicionar Olá `using` instrução:</span><span class="sxs-lookup"><span data-stu-id="94c56-133">Add hello `using` statement:</span></span>

            using Microsoft.Azure.Engagement;

    <span data-ttu-id="94c56-134">b.</span><span class="sxs-lookup"><span data-stu-id="94c56-134">b.</span></span> <span data-ttu-id="94c56-135">Adicione um método que inicializa Olá contrato:</span><span class="sxs-lookup"><span data-stu-id="94c56-135">Add a method that initializes hello Engagement:</span></span>

           private void InitEngagement(IActivatedEventArgs e)
           {
             EngagementAgent.Instance.Init(e);

             //... rest of hello code
           }

    <span data-ttu-id="94c56-136">c.</span><span class="sxs-lookup"><span data-stu-id="94c56-136">c.</span></span> <span data-ttu-id="94c56-137">Inicializar Olá SDK no hello **OnLaunched** método:</span><span class="sxs-lookup"><span data-stu-id="94c56-137">Initialize hello SDK in hello **OnLaunched** method:</span></span>

            protected override void OnLaunched(LaunchActivatedEventArgs e)
            {
              InitEngagement(e);

              //... rest of hello code
            }

    <span data-ttu-id="94c56-138">c.</span><span class="sxs-lookup"><span data-stu-id="94c56-138">c.</span></span> <span data-ttu-id="94c56-139">Inserir o seguinte Olá em hello **OnActivated** método e adicione o método hello se ele não ainda estiver presente:</span><span class="sxs-lookup"><span data-stu-id="94c56-139">Insert hello following in hello **OnActivated** method and add hello method if it is not already present:</span></span>

            protected override void OnActivated(IActivatedEventArgs e)
            {
              InitEngagement(e);

              //... rest of hello code
            }

## <span data-ttu-id="94c56-140"><a id="monitor"></a>Habilitar monitoramento em tempo real</span><span class="sxs-lookup"><span data-stu-id="94c56-140"><a id="monitor"></a>Enable real-time monitoring</span></span>
<span data-ttu-id="94c56-141">toostart enviar dados e garantir que os usuários de saudação estão ativos, você deve enviar pelo menos uma tela (atividade) toohello Mobile Engagement backend.</span><span class="sxs-lookup"><span data-stu-id="94c56-141">toostart sending data and ensuring that hello users are active, you must send at least one screen (Activity) toohello Mobile Engagement backend.</span></span>

1. <span data-ttu-id="94c56-142">Em Olá **MainPage.xaml.cs**, adicione o seguinte Olá `using` instrução:</span><span class="sxs-lookup"><span data-stu-id="94c56-142">In hello **MainPage.xaml.cs**, add hello following `using` statement:</span></span>

    <span data-ttu-id="94c56-143">usando Microsoft.Azure.Engagement.Overlay;</span><span class="sxs-lookup"><span data-stu-id="94c56-143">using Microsoft.Azure.Engagement.Overlay;</span></span>
2. <span data-ttu-id="94c56-144">Alterar a classe base de saudação do **MainPage** de **página** muito**EngagementPageOverlay**:</span><span class="sxs-lookup"><span data-stu-id="94c56-144">Change hello base class of **MainPage** from **Page** too**EngagementPageOverlay**:</span></span>

        class MainPage : EngagementPageOverlay
3. <span data-ttu-id="94c56-145">Em Olá `MainPage.xaml` arquivo:</span><span class="sxs-lookup"><span data-stu-id="94c56-145">In hello `MainPage.xaml` file:</span></span>

    <span data-ttu-id="94c56-146">a.</span><span class="sxs-lookup"><span data-stu-id="94c56-146">a.</span></span> <span data-ttu-id="94c56-147">Adicione declarações de namespaces tooyour:</span><span class="sxs-lookup"><span data-stu-id="94c56-147">Add tooyour namespaces declarations:</span></span>

        xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"

    <span data-ttu-id="94c56-148">b.</span><span class="sxs-lookup"><span data-stu-id="94c56-148">b.</span></span> <span data-ttu-id="94c56-149">Substituir saudação **página** no nome da marca XML Olá com **contrato: EngagementPageOverlay**</span><span class="sxs-lookup"><span data-stu-id="94c56-149">Replace hello **Page** in hello XML tag name with **engagement:EngagementPageOverlay**</span></span>

> [!IMPORTANT]
> <span data-ttu-id="94c56-150">Se sua página substitui Olá `OnNavigatedTo` método, ser toocall se `base.OnNavigatedTo(e)`.</span><span class="sxs-lookup"><span data-stu-id="94c56-150">If your page overrides hello `OnNavigatedTo` method, be sure toocall `base.OnNavigatedTo(e)`.</span></span> <span data-ttu-id="94c56-151">Caso contrário, a atividade de saudação não é informada `EngagementPage` chamadas `StartActivity` dentro de seu `OnNavigatedTo` método).</span><span class="sxs-lookup"><span data-stu-id="94c56-151">Otherwise, hello activity is not reported `EngagementPage` calls `StartActivity` inside its `OnNavigatedTo` method).</span></span> <span data-ttu-id="94c56-152">Isso é especialmente importante em um projeto do Windows Phone onde saudação padrão modelo tem um `OnNavigatedTo` método.</span><span class="sxs-lookup"><span data-stu-id="94c56-152">This is especially important in a Windows Phone project where hello default template has an `OnNavigatedTo` method.</span></span>
>
> <span data-ttu-id="94c56-153">Para **aplicativos universais do Windows 10**, usar o método hello recomendado em hello "recomendado método: sobrecarregar suas classes de página" seção [avançado relatar Olá SDK de contrato de aplicativos Universal do Windows](mobile-engagement-windows-store-advanced-reporting.md) , em vez da saudação mencionados acima.</span><span class="sxs-lookup"><span data-stu-id="94c56-153">For **Windows 10 Universal apps**, use hello method recommended in hello "Recommended method: overload your Page classes" section of [Advanced Reporting with hello Windows Universal Apps Engagement SDK](mobile-engagement-windows-store-advanced-reporting.md), rather than hello one mentioned above.</span></span>

## <span data-ttu-id="94c56-154"><a id="monitor"></a>Conectar o aplicativo com monitoramento em tempo real</span><span class="sxs-lookup"><span data-stu-id="94c56-154"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="94c56-155"><a id="integrate-push"></a>Habilitar notificações por push e mensagens no aplicativo</span><span class="sxs-lookup"><span data-stu-id="94c56-155"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="94c56-156">Mobile Engagement permite toointeract e alcançar os usuários com as notificações por push e no aplicativo mensagens no contexto de saudação de campanhas.</span><span class="sxs-lookup"><span data-stu-id="94c56-156">Mobile Engagement allows you toointeract and reach your users with push notifications and in-app messaging in hello context of campaigns.</span></span> <span data-ttu-id="94c56-157">Esse módulo é chamado alcance no portal do Mobile Engagement hello.</span><span class="sxs-lookup"><span data-stu-id="94c56-157">This module is called REACH in hello Mobile Engagement portal.</span></span>
<span data-ttu-id="94c56-158">Olá seções a seguir configurar seu aplicativo tooreceive-los.</span><span class="sxs-lookup"><span data-stu-id="94c56-158">hello following sections set up your app tooreceive them.</span></span>

### <a name="enable-your-app-tooreceive-wns-push-notifications"></a><span data-ttu-id="94c56-159">Habilitar seu aplicativo tooreceive notificações por Push do WNS</span><span class="sxs-lookup"><span data-stu-id="94c56-159">Enable your app tooreceive WNS Push Notifications</span></span>
1. <span data-ttu-id="94c56-160">Em Olá `Package.appxmanifest` no arquivo, em Olá **aplicativo** guia em **notificações**, defina **compatíveis com notificação do sistema:** muito**Sim**</span><span class="sxs-lookup"><span data-stu-id="94c56-160">In hello `Package.appxmanifest` file, in hello **Application** tab, under **Notifications**, set **Toast capable:** too**Yes**</span></span>

    ![][5]

### <a name="initialize-hello-reach-sdk"></a><span data-ttu-id="94c56-161">Inicializar Olá SDK do REACH</span><span class="sxs-lookup"><span data-stu-id="94c56-161">Initialize hello REACH SDK</span></span>
<span data-ttu-id="94c56-162">Em `App.xaml.cs`, chame **EngagementReach.Instance.Init(e);** em Olá **InitEngagement** função logo após a inicialização do agente de saudação:</span><span class="sxs-lookup"><span data-stu-id="94c56-162">In `App.xaml.cs`, call **EngagementReach.Instance.Init(e);** in hello **InitEngagement** function right after hello agent initialization:</span></span>

        private void InitEngagement(IActivatedEventArgs e)
        {
           EngagementAgent.Instance.Init(e);
           EngagementReach.Instance.Init(e);
        }

<span data-ttu-id="94c56-163">Você está pronto toosend uma notificação do sistema.</span><span class="sxs-lookup"><span data-stu-id="94c56-163">You're ready toosend a toast.</span></span> <span data-ttu-id="94c56-164">Em seguida, verificamos se você realizou corretamente essa integração básica.</span><span class="sxs-lookup"><span data-stu-id="94c56-164">Next we verify that you have correctly carried out this basic integration.</span></span>

### <a name="grant-access-toomobile-engagement-toosend-notifications"></a><span data-ttu-id="94c56-165">Conceder acesso tooMobile contrato toosend notificações</span><span class="sxs-lookup"><span data-stu-id="94c56-165">Grant access tooMobile Engagement toosend notifications</span></span>
1. <span data-ttu-id="94c56-166">Abra [Centro de Desenvolvimento da Windows Store] no navegador da Web, faça logon e crie uma conta, se necessário.</span><span class="sxs-lookup"><span data-stu-id="94c56-166">Open [Windows Store Dev Center] in your web browser, login, and create an account if necessary.</span></span>
2. <span data-ttu-id="94c56-167">Clique em **painel** na parte superior de saudação à direita de canto e, em seguida, clique em **criar um novo aplicativo** Olá esquerdo no menu do painel.</span><span class="sxs-lookup"><span data-stu-id="94c56-167">Click **Dashboard** at hello top right corner and then click **Create a new app** from hello left panel menu.</span></span>

    ![][9]
3. <span data-ttu-id="94c56-168">Crie seu aplicativo ao reservar o nome dele.</span><span class="sxs-lookup"><span data-stu-id="94c56-168">Create your app by reserving its name.</span></span>

    ![][10]
4. <span data-ttu-id="94c56-169">Depois que o aplicativo hello foi criado, navegar muito**serviços -> notificações por Push** no menu esquerdo hello.</span><span class="sxs-lookup"><span data-stu-id="94c56-169">Once hello app has been created, navigate too**Services -> Push notifications** from hello left menu.</span></span>

    ![][11]
5. <span data-ttu-id="94c56-170">Em Olá seção notificações de Push, clique em Olá **site de serviços do Live** link.</span><span class="sxs-lookup"><span data-stu-id="94c56-170">In hello Push notifications section, click hello **Live Services site** link.</span></span>

    ![][12]
6. <span data-ttu-id="94c56-171">Você navegar toohello seção de credenciais de Push.</span><span class="sxs-lookup"><span data-stu-id="94c56-171">You navigate toohello Push credentials section.</span></span> <span data-ttu-id="94c56-172">Verifique se você está no hello **configurações do aplicativo** seção e, em seguida, copie o **SID do pacote** e **segredo do cliente**</span><span class="sxs-lookup"><span data-stu-id="94c56-172">Make sure you are in hello **App Settings** section and then copy your **Package SID** and **Client secret**</span></span>

    ![][13]
7. <span data-ttu-id="94c56-173">Navegue toohello **configurações** de seu portal do Mobile Engagement e clique em Olá **Push nativo** seção Olá esquerda.</span><span class="sxs-lookup"><span data-stu-id="94c56-173">Navigate toohello **Settings** of your Mobile Engagement portal, and click hello **Native Push** section on hello left.</span></span> <span data-ttu-id="94c56-174">Em seguida, clique em Olá **editar** tooenter botão seu **identificador de segurança (SID) do pacote** e sua **chave secreta** conforme mostrado:</span><span class="sxs-lookup"><span data-stu-id="94c56-174">Then, click hello **Edit** button tooenter your **Package security identifier (SID)** and your **Secret Key** as shown:</span></span>

    ![][6]
8. <span data-ttu-id="94c56-175">Por fim, certifique-se de que você associou o aplicativo do Visual Studio com este aplicativo criado no repositório de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="94c56-175">Finally make sure that you have associated your Visual Studio app with this created app in hello App store.</span></span> <span data-ttu-id="94c56-176">Clique em **Associar Aplicativo à Loja** no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="94c56-176">Click **Associate App with Store** in Visual Studio.</span></span>

    ![][7]

## <span data-ttu-id="94c56-177"><a id="send"></a>Enviar um aplicativo de tooyour de notificação</span><span class="sxs-lookup"><span data-stu-id="94c56-177"><a id="send"></a>Send a notification tooyour app</span></span>
[!INCLUDE [Create Windows Push campaign](../../includes/mobile-engagement-windows-push-campaign.md)]

<span data-ttu-id="94c56-178">Se o aplicativo hello está em execução, você verá uma notificação no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="94c56-178">If hello app is running, you see an in-app notification.</span></span> <span data-ttu-id="94c56-179">Caso contrário, se aplicativo hello estiver fechado, você verá uma notificação do sistema.</span><span class="sxs-lookup"><span data-stu-id="94c56-179">otherwise if hello app is closed, you see a toast notification.</span></span>
<span data-ttu-id="94c56-180">Se você vir uma notificação no aplicativo, mas não uma notificação do sistema, e você estiver executando o aplicativo hello no modo de depuração no Visual Studio, em seguida, tente **eventos de ciclo de vida -> Suspender** no hello tooensure de barra de ferramentas que o aplicativo hello é suspensa.</span><span class="sxs-lookup"><span data-stu-id="94c56-180">If you see an in-app notification but not a toast notification, and you are running hello app in debug mode in Visual Studio, then try **Lifecycle events -> Suspend** in hello toolbar tooensure that hello app is suspended.</span></span> <span data-ttu-id="94c56-181">Se você clicou o botão de início Olá durante a depuração de aplicativo hello no Visual Studio, em seguida, ele não sempre obter suspenso e enquanto você receber a notificação de saudação como no aplicativo, ele não aparece como uma notificação do sistema.</span><span class="sxs-lookup"><span data-stu-id="94c56-181">If you clicked hello Home button while debugging hello application in Visual Studio, then it doesn't always get suspended and while you see hello notification as in-app, it doesn't show up as a toast notification.</span></span>  

![][8]

<!-- URLs. -->
[Mobile Engagement Windows Universal SDK documentation]: ../mobile-engagement-windows-store-integrate-engagement/
[MicrosoftAzure.MobileEngagement]: http://go.microsoft.com/?linkid=9864592
[Centro de Desenvolvimento da Windows Store]: https://dev.windows.com
[Windows Universal Apps - Overlay integration]: ../mobile-engagement-windows-store-integrate-engagement-reach/#overlay-integration

<!-- Images. -->
[1]: ./media/mobile-engagement-windows-store-dotnet-get-started/universal-app-creation.png
[2]: ./media/mobile-engagement-windows-store-dotnet-get-started/manifest-capabilities.png
[3]: ./media/mobile-engagement-windows-store-dotnet-get-started/add-connection-info.png
[5]: ./media/mobile-engagement-windows-store-dotnet-get-started/manifest-toast.png
[6]: ./media/mobile-engagement-windows-store-dotnet-get-started/enter-credentials.png
[7]: ./media/mobile-engagement-windows-store-dotnet-get-started/associate-app-store.png
[8]: ./media/mobile-engagement-windows-store-dotnet-get-started/vs-suspend.png
[9]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_create_app.png
[10]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_app_name.png
[11]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_services_push.png
[12]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_services_push_1.png
[13]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_services_push_creds.png
