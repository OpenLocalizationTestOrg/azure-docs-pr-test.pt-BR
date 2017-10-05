---
title: "Introdução ao Azure Mobile Engagement dos Aplicativos Windows Universal"
description: "Saiba como usar o Azure Mobile Engagement com análises e notificações por push para aplicativos universais do Windows."
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
ms.openlocfilehash: 40db7e4dd151ec391c754dc6d4145aeeb8058eca
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-windows-universal-apps"></a><span data-ttu-id="837b7-103">Introdução ao Azure Mobile Engagement para aplicativos universais do Windows</span><span class="sxs-lookup"><span data-stu-id="837b7-103">Get started with Azure Mobile Engagement for Windows Universal Apps</span></span>
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

<span data-ttu-id="837b7-104">Este tópico mostra como usar o Azure Mobile Engagement para entender o uso do aplicativo e enviar notificações por push para usuários segmentados de um aplicativo do Windows Universal.</span><span class="sxs-lookup"><span data-stu-id="837b7-104">This topic shows you how to use Azure Mobile Engagement to understand your app usage and send push notifications to segmented users of a Windows Universal application.</span></span>
<span data-ttu-id="837b7-105">Esse tutorial demonstra um cenário de transmissão simples usando o Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="837b7-105">This tutorial demonstrates the simple broadcast scenario using Mobile Engagement.</span></span> <span data-ttu-id="837b7-106">Você cria um Aplicativo Windows Universal em branco que coleta os dados básicos de uso do aplicativo e recebe notificações por push usando o Serviço de Notificação do Windows (WNS).</span><span class="sxs-lookup"><span data-stu-id="837b7-106">You create a blank Windows Universal App that collects basic app usage data and receives push notifications using Windows Notification Service (WNS).</span></span>

> [!NOTE]
> <span data-ttu-id="837b7-107">O serviço Azure Mobile Engagement será desativado em março de 2018 e, no momento, está disponível somente para os clientes existentes.</span><span class="sxs-lookup"><span data-stu-id="837b7-107">The Azure Mobile Engagement service will be retired March 2018 and is currently only available to existing customers.</span></span> <span data-ttu-id="837b7-108">Para saber mais, confira [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span><span class="sxs-lookup"><span data-stu-id="837b7-108">For more information, see [Mobile Engagement](https://azure.microsoft.com/en-us/services/mobile-engagement/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="837b7-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="837b7-109">Prerequisites</span></span>
[!INCLUDE [Prereqs](../../includes/mobile-engagement-windows-store-prereqs.md)]

## <a name="set-up-mobile-engagement-for-your-windows-universal-app"></a><span data-ttu-id="837b7-110">Configurar o Mobile Engagement para seu aplicativo Windows Universal</span><span class="sxs-lookup"><span data-stu-id="837b7-110">Set up Mobile Engagement for your Windows Universal app</span></span>
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <span data-ttu-id="837b7-111"><a id="connecting-app"></a>Conecte o seu aplicativo ao back-end do Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="837b7-111"><a id="connecting-app"></a>Connect your app to the Mobile Engagement backend</span></span>
<span data-ttu-id="837b7-112">Este tutorial apresenta uma "integração básica," que é o conjunto mínimo necessário para coletar dados e enviar uma notificação por push.</span><span class="sxs-lookup"><span data-stu-id="837b7-112">This tutorial presents a "basic integration," which is the minimal set required to collect data and send a push notification.</span></span> <span data-ttu-id="837b7-113">A documentação de integração completa pode ser encontrada na [integração do SDK Universal do Windows para o Mobile Engagement](mobile-engagement-windows-store-sdk-overview.md).</span><span class="sxs-lookup"><span data-stu-id="837b7-113">The complete integration documentation can be found in the [Mobile Engagement Windows Universal SDK integration](mobile-engagement-windows-store-sdk-overview.md).</span></span>

<span data-ttu-id="837b7-114">Você cria um aplicativo básico com o Visual Studio para demonstrar a integração.</span><span class="sxs-lookup"><span data-stu-id="837b7-114">You create a basic app with Visual Studio to demonstrate the integration.</span></span>

### <a name="create-a-windows-universal-app-project"></a><span data-ttu-id="837b7-115">Criar um projeto de Aplicativo Windows Universal</span><span class="sxs-lookup"><span data-stu-id="837b7-115">Create a Windows Universal App project</span></span>
<span data-ttu-id="837b7-116">As etapas a seguir pressupõem o uso do Visual Studio 2015, embora as etapas sejam semelhantes em versões anteriores do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="837b7-116">The following steps assume the use of Visual Studio 2015 though the steps are similar in earlier versions of Visual Studio.</span></span>

1. <span data-ttu-id="837b7-117">Inicie o Visual Studio e na tela **Início**, selecione **Novo Projeto**.</span><span class="sxs-lookup"><span data-stu-id="837b7-117">Start Visual Studio, and in the **Home** screen, select **New Project**.</span></span>
2. <span data-ttu-id="837b7-118">No menu pop-up, selecione **Windows** -> **Universal** -> **Aplicativo em Branco (Windows Universal)**.</span><span class="sxs-lookup"><span data-stu-id="837b7-118">In the pop-up, select **Windows** -> **Universal** -> **Blank App (Universal Windows)**.</span></span> <span data-ttu-id="837b7-119">Preencha o **Nome** e o **Nome da solução** do aplicativo, em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="837b7-119">Fill in the app **Name** and **Solution name**, and then click **OK**.</span></span>

    ![][1]

<span data-ttu-id="837b7-120">Agora, você criou um projeto Aplicativo Windows Universal no qual integrará o SDK do Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="837b7-120">You have now created a Windows Universal App project into which you next integrate the Azure Mobile Engagement SDK.</span></span>

### <a name="connect-your-app-to-mobile-engagement-backend"></a><span data-ttu-id="837b7-121">Conecte seu aplicativo ao back-end do Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="837b7-121">Connect your app to Mobile Engagement backend</span></span>
1. <span data-ttu-id="837b7-122">Instale o pacote Nuget [MicrosoftAzure.MobileEngagement] em seu projeto.</span><span class="sxs-lookup"><span data-stu-id="837b7-122">Install the [MicrosoftAzure.MobileEngagement] Nuget package in your project.</span></span> <span data-ttu-id="837b7-123">Se estiver visando as plataformas Windows e Windows Phone, precisará fazer isso em ambos os projetos.</span><span class="sxs-lookup"><span data-stu-id="837b7-123">If you are targeting both Windows and Windows Phone platforms, you need to do this for both projects.</span></span> <span data-ttu-id="837b7-124">Para o Windows 8.x e o Windows Phone 8.1, o mesmo pacote Nuget coloca os binários corretos específicos da plataforma em cada projeto.</span><span class="sxs-lookup"><span data-stu-id="837b7-124">For Windows 8.x and Windows Phone 8.1, the same Nuget package places the correct platform-specific binaries in each project.</span></span>
2. <span data-ttu-id="837b7-125">Abra **Package.appxmanifest** e verifique se a funcionalidade a seguir foi adicionada:</span><span class="sxs-lookup"><span data-stu-id="837b7-125">Open **Package.appxmanifest** and make sure that the following capability is added there:</span></span>

        Internet (Client)

    ![][2]
3. <span data-ttu-id="837b7-126">Agora, copie a cadeia de conexão que você copiou anteriormente para o seu Aplicativo Mobile Engagement e cole-o no arquivo `Resources\EngagementConfiguration.xml` entre as marcas `<connectionString>` e `</connectionString>`:</span><span class="sxs-lookup"><span data-stu-id="837b7-126">Now copy the connection string that you copied earlier for your Mobile Engagement App and paste it in the `Resources\EngagementConfiguration.xml` file, between the `<connectionString>` and `</connectionString>` tags:</span></span>

    ![][3]

    > [!TIP]
    > <span data-ttu-id="837b7-127">Se seu aplicativo for destinado para as plataformas Windows e Windows Phone, você ainda deverá criar dois Aplicativos do Mobile Engagement - um para cada plataforma com suporte.</span><span class="sxs-lookup"><span data-stu-id="837b7-127">If your App targets both Windows and Windows Phone platforms, you should still create two Mobile Engagement Applications - one for each supported platform.</span></span> <span data-ttu-id="837b7-128">Ter dois aplicativos garante que você pode criar uma segmentação correta do público e pode enviar notificações de destino apropriadamente para cada plataforma.</span><span class="sxs-lookup"><span data-stu-id="837b7-128">Having two apps ensures that you can create correct segmentation of the audience and can send appropriately targeted notifications for each platform.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="837b7-129">O NuGet ainda não copiará automaticamente os recursos do SDK em seu aplicativo UWP Windows 10.</span><span class="sxs-lookup"><span data-stu-id="837b7-129">NuGet does not automatically copy the SDK resources in your Windows 10 UWP application.</span></span> <span data-ttu-id="837b7-130">Você precisa fazê-lo manualmente seguindo as etapas que aparecem (readme.txt) quando o pacote Nuget é instalado.</span><span class="sxs-lookup"><span data-stu-id="837b7-130">You have to do it manually following the steps which show up (readme.txt) when the Nuget package is installed.</span></span>  

1. <span data-ttu-id="837b7-131">No arquivo `App.xaml.cs`:</span><span class="sxs-lookup"><span data-stu-id="837b7-131">In the `App.xaml.cs` file:</span></span>

    <span data-ttu-id="837b7-132">a.</span><span class="sxs-lookup"><span data-stu-id="837b7-132">a.</span></span> <span data-ttu-id="837b7-133">Adicione a instrução `using`:</span><span class="sxs-lookup"><span data-stu-id="837b7-133">Add the `using` statement:</span></span>

            using Microsoft.Azure.Engagement;

    <span data-ttu-id="837b7-134">b.</span><span class="sxs-lookup"><span data-stu-id="837b7-134">b.</span></span> <span data-ttu-id="837b7-135">Adicione um método que inicializa o Engagement:</span><span class="sxs-lookup"><span data-stu-id="837b7-135">Add a method that initializes the Engagement:</span></span>

           private void InitEngagement(IActivatedEventArgs e)
           {
             EngagementAgent.Instance.Init(e);

             //... rest of the code
           }

    <span data-ttu-id="837b7-136">c.</span><span class="sxs-lookup"><span data-stu-id="837b7-136">c.</span></span> <span data-ttu-id="837b7-137">Inicialize o SDK no método **OnLaunched** :</span><span class="sxs-lookup"><span data-stu-id="837b7-137">Initialize the SDK in the **OnLaunched** method:</span></span>

            protected override void OnLaunched(LaunchActivatedEventArgs e)
            {
              InitEngagement(e);

              //... rest of the code
            }

    <span data-ttu-id="837b7-138">c.</span><span class="sxs-lookup"><span data-stu-id="837b7-138">c.</span></span> <span data-ttu-id="837b7-139">Insira o seguinte no método **OnActivated** e adicione o método se ele não estiver presente:</span><span class="sxs-lookup"><span data-stu-id="837b7-139">Insert the following in the **OnActivated** method and add the method if it is not already present:</span></span>

            protected override void OnActivated(IActivatedEventArgs e)
            {
              InitEngagement(e);

              //... rest of the code
            }

## <span data-ttu-id="837b7-140"><a id="monitor"></a>Habilitar monitoramento em tempo real</span><span class="sxs-lookup"><span data-stu-id="837b7-140"><a id="monitor"></a>Enable real-time monitoring</span></span>
<span data-ttu-id="837b7-141">Para iniciar o envio dos dados e assegurar que os usuários estejam ativos, você deve enviar pelo menos uma tela (Atividade) para o back-end do Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="837b7-141">To start sending data and ensuring that the users are active, you must send at least one screen (Activity) to the Mobile Engagement backend.</span></span>

1. <span data-ttu-id="837b7-142">Em **MainPage.xaml.cs**, adicione a seguinte instrução `using`:</span><span class="sxs-lookup"><span data-stu-id="837b7-142">In the **MainPage.xaml.cs**, add the following `using` statement:</span></span>

    <span data-ttu-id="837b7-143">usando Microsoft.Azure.Engagement.Overlay;</span><span class="sxs-lookup"><span data-stu-id="837b7-143">using Microsoft.Azure.Engagement.Overlay;</span></span>
2. <span data-ttu-id="837b7-144">Altere a classe base **MainPage** de **Page** para **EngagementPageOverlay**:</span><span class="sxs-lookup"><span data-stu-id="837b7-144">Change the base class of **MainPage** from **Page** to **EngagementPageOverlay**:</span></span>

        class MainPage : EngagementPageOverlay
3. <span data-ttu-id="837b7-145">No arquivo `MainPage.xaml`:</span><span class="sxs-lookup"><span data-stu-id="837b7-145">In the `MainPage.xaml` file:</span></span>

    <span data-ttu-id="837b7-146">a.</span><span class="sxs-lookup"><span data-stu-id="837b7-146">a.</span></span> <span data-ttu-id="837b7-147">Adicione às suas declarações de namespaces:</span><span class="sxs-lookup"><span data-stu-id="837b7-147">Add to your namespaces declarations:</span></span>

        xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"

    <span data-ttu-id="837b7-148">b.</span><span class="sxs-lookup"><span data-stu-id="837b7-148">b.</span></span> <span data-ttu-id="837b7-149">Substitua **Page** no nome da marcação XML por **engagement:EngagementPageOverlay**</span><span class="sxs-lookup"><span data-stu-id="837b7-149">Replace the **Page** in the XML tag name with **engagement:EngagementPageOverlay**</span></span>

> [!IMPORTANT]
> <span data-ttu-id="837b7-150">Se sua página substitui o método `OnNavigatedTo`, certifique-se de chamar `base.OnNavigatedTo(e)`.</span><span class="sxs-lookup"><span data-stu-id="837b7-150">If your page overrides the `OnNavigatedTo` method, be sure to call `base.OnNavigatedTo(e)`.</span></span> <span data-ttu-id="837b7-151">Caso contrário, a atividade não será registrada (`EngagementPage` chama `StartActivity` dentro de seu método `OnNavigatedTo`).</span><span class="sxs-lookup"><span data-stu-id="837b7-151">Otherwise, the activity is not reported `EngagementPage` calls `StartActivity` inside its `OnNavigatedTo` method).</span></span> <span data-ttu-id="837b7-152">Isso é especialmente importante em um projeto do Windows Phone, no qual o modelo padrão tem um método `OnNavigatedTo` .</span><span class="sxs-lookup"><span data-stu-id="837b7-152">This is especially important in a Windows Phone project where the default template has an `OnNavigatedTo` method.</span></span>
>
> <span data-ttu-id="837b7-153">Para os **Aplicativos Universais do Windows 10**, use o método recomendado na seção "Método recomendado: sobrecarregar suas classes de Página" dos [Relatórios avançados com o SDK de Engajamento para Aplicativos Universais do Windows](mobile-engagement-windows-store-advanced-reporting.md), em vez do método mencionado acima.</span><span class="sxs-lookup"><span data-stu-id="837b7-153">For **Windows 10 Universal apps**, use the method recommended in the "Recommended method: overload your Page classes" section of [Advanced Reporting with the Windows Universal Apps Engagement SDK](mobile-engagement-windows-store-advanced-reporting.md), rather than the one mentioned above.</span></span>

## <span data-ttu-id="837b7-154"><a id="monitor"></a>Conectar o aplicativo com monitoramento em tempo real</span><span class="sxs-lookup"><span data-stu-id="837b7-154"><a id="monitor"></a>Connect app with real-time monitoring</span></span>
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <span data-ttu-id="837b7-155"><a id="integrate-push"></a>Habilitar notificações por push e mensagens no aplicativo</span><span class="sxs-lookup"><span data-stu-id="837b7-155"><a id="integrate-push"></a>Enable push notifications and in-app messaging</span></span>
<span data-ttu-id="837b7-156">O Mobile Engagement permite interagir e entrar em contato com usuários com notificações por push e mensagens no aplicativo no contexto de campanhas.</span><span class="sxs-lookup"><span data-stu-id="837b7-156">Mobile Engagement allows you to interact and reach your users with push notifications and in-app messaging in the context of campaigns.</span></span> <span data-ttu-id="837b7-157">Esse módulo é chamado de REACH no portal do Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="837b7-157">This module is called REACH in the Mobile Engagement portal.</span></span>
<span data-ttu-id="837b7-158">As seções a seguir configuram seu aplicativo para recebê-las.</span><span class="sxs-lookup"><span data-stu-id="837b7-158">The following sections set up your app to receive them.</span></span>

### <a name="enable-your-app-to-receive-wns-push-notifications"></a><span data-ttu-id="837b7-159">Habilitar o aplicativo para receber Notificações por Push do WNS</span><span class="sxs-lookup"><span data-stu-id="837b7-159">Enable your app to receive WNS Push Notifications</span></span>
1. <span data-ttu-id="837b7-160">No arquivo `Package.appxmanifest`, na guia **Aplicativo** em **Notificações**, defina **compatível com Toast:** para **Sim**</span><span class="sxs-lookup"><span data-stu-id="837b7-160">In the `Package.appxmanifest` file, in the **Application** tab, under **Notifications**, set **Toast capable:** to **Yes**</span></span>

    ![][5]

### <a name="initialize-the-reach-sdk"></a><span data-ttu-id="837b7-161">Inicializar o SDK do REACH</span><span class="sxs-lookup"><span data-stu-id="837b7-161">Initialize the REACH SDK</span></span>
<span data-ttu-id="837b7-162">Em `App.xaml.cs`, chame **EngagementReach.Instance.Init(e);** na função **InitEngagement** logo após a inicialização do agente:</span><span class="sxs-lookup"><span data-stu-id="837b7-162">In `App.xaml.cs`, call **EngagementReach.Instance.Init(e);** in the **InitEngagement** function right after the agent initialization:</span></span>

        private void InitEngagement(IActivatedEventArgs e)
        {
           EngagementAgent.Instance.Init(e);
           EngagementReach.Instance.Init(e);
        }

<span data-ttu-id="837b7-163">Você está pronto para enviar uma saudação.</span><span class="sxs-lookup"><span data-stu-id="837b7-163">You're ready to send a toast.</span></span> <span data-ttu-id="837b7-164">Em seguida, verificamos se você realizou corretamente essa integração básica.</span><span class="sxs-lookup"><span data-stu-id="837b7-164">Next we verify that you have correctly carried out this basic integration.</span></span>

### <a name="grant-access-to-mobile-engagement-to-send-notifications"></a><span data-ttu-id="837b7-165">Conceder acesso ao Mobile Engagement para enviar notificações</span><span class="sxs-lookup"><span data-stu-id="837b7-165">Grant access to Mobile Engagement to send notifications</span></span>
1. <span data-ttu-id="837b7-166">Abra [Centro de Desenvolvimento da Windows Store] no navegador da Web, faça logon e crie uma conta, se necessário.</span><span class="sxs-lookup"><span data-stu-id="837b7-166">Open [Windows Store Dev Center] in your web browser, login, and create an account if necessary.</span></span>
2. <span data-ttu-id="837b7-167">Clique em **Painel** no canto superior direito, em seguida, clique em **Criar um novo aplicativo** no menu do painel esquerdo.</span><span class="sxs-lookup"><span data-stu-id="837b7-167">Click **Dashboard** at the top right corner and then click **Create a new app** from the left panel menu.</span></span>

    ![][9]
3. <span data-ttu-id="837b7-168">Crie seu aplicativo ao reservar o nome dele.</span><span class="sxs-lookup"><span data-stu-id="837b7-168">Create your app by reserving its name.</span></span>

    ![][10]
4. <span data-ttu-id="837b7-169">Depois que o aplicativo tiver sido criado, navegue até **Serviços -> Notificações por push** no menu à esquerda.</span><span class="sxs-lookup"><span data-stu-id="837b7-169">Once the app has been created, navigate to **Services -> Push notifications** from the left menu.</span></span>

    ![][11]
5. <span data-ttu-id="837b7-170">Na seção Notificações por push, clique no link **site de Serviços Dinâmicos** .</span><span class="sxs-lookup"><span data-stu-id="837b7-170">In the Push notifications section, click the **Live Services site** link.</span></span>

    ![][12]
6. <span data-ttu-id="837b7-171">Você navegará para a seção Credenciais de push.</span><span class="sxs-lookup"><span data-stu-id="837b7-171">You navigate to the Push credentials section.</span></span> <span data-ttu-id="837b7-172">Verifique se você está na seção **Configurações do Aplicativo**, em seguida, copie o **SID do Pacote** e o **Segredo do cliente**</span><span class="sxs-lookup"><span data-stu-id="837b7-172">Make sure you are in the **App Settings** section and then copy your **Package SID** and **Client secret**</span></span>

    ![][13]
7. <span data-ttu-id="837b7-173">Navegue até **Configurações** do portal do Mobile Engagement e clique na seção **Push Nativo** à esquerda.</span><span class="sxs-lookup"><span data-stu-id="837b7-173">Navigate to the **Settings** of your Mobile Engagement portal, and click the **Native Push** section on the left.</span></span> <span data-ttu-id="837b7-174">Em seguida, clique no botão **Editar** para inserir seu **identificador de segurança (SID) do pacote** e sua **Chave Secreta** mostrado:</span><span class="sxs-lookup"><span data-stu-id="837b7-174">Then, click the **Edit** button to enter your **Package security identifier (SID)** and your **Secret Key** as shown:</span></span>

    ![][6]
8. <span data-ttu-id="837b7-175">Por fim, certifique-se de que você tenha associado o aplicativo do Visual Studio a este aplicativo criado na Loja de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="837b7-175">Finally make sure that you have associated your Visual Studio app with this created app in the App store.</span></span> <span data-ttu-id="837b7-176">Clique em **Associar Aplicativo à Loja** no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="837b7-176">Click **Associate App with Store** in Visual Studio.</span></span>

    ![][7]

## <span data-ttu-id="837b7-177"><a id="send"></a>Envie uma notificação para seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="837b7-177"><a id="send"></a>Send a notification to your app</span></span>
[!INCLUDE [Create Windows Push campaign](../../includes/mobile-engagement-windows-push-campaign.md)]

<span data-ttu-id="837b7-178">Se o aplicativo estiver em execução, você verá uma notificação no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="837b7-178">If the app is running, you see an in-app notification.</span></span> <span data-ttu-id="837b7-179">Caso contrário, se o aplicativo estiver fechado, verá uma notificação do toast.</span><span class="sxs-lookup"><span data-stu-id="837b7-179">otherwise if the app is closed, you see a toast notification.</span></span>
<span data-ttu-id="837b7-180">Se você vir uma notificação no aplicativo, mas não uma notificação do toast, e estiver executando o aplicativo no modo de depuração no Visual Studio, então, experimente **ventos do ciclo de vida -> Suspender** na barra de ferramentas para garantir que o aplicativo está suspenso.</span><span class="sxs-lookup"><span data-stu-id="837b7-180">If you see an in-app notification but not a toast notification, and you are running the app in debug mode in Visual Studio, then try **Lifecycle events -> Suspend** in the toolbar to ensure that the app is suspended.</span></span> <span data-ttu-id="837b7-181">Se você clicou no botão Início durante a depuração do aplicativo no Visual Studio, nem sempre ele será suspenso e embora você veja a notificação como no aplicativo, ela não aparecerá como uma notificação do sistema.</span><span class="sxs-lookup"><span data-stu-id="837b7-181">If you clicked the Home button while debugging the application in Visual Studio, then it doesn't always get suspended and while you see the notification as in-app, it doesn't show up as a toast notification.</span></span>  

![][8]

<!-- URLs. -->
[Mobile Engagement Windows Universal SDK documentation]: ../mobile-engagement-windows-store-integrate-engagement/
<span data-ttu-id="837b7-182">[MicrosoftAzure.MobileEngagement]: http://go.microsoft.com/?linkid=9864592</span><span class="sxs-lookup"><span data-stu-id="837b7-182">[MicrosoftAzure.MobileEngagement]: http://go.microsoft.com/?linkid=9864592</span></span>
<span data-ttu-id="837b7-183">[Centro de Desenvolvimento da Windows Store]: https://dev.windows.com</span><span class="sxs-lookup"><span data-stu-id="837b7-183">[Windows Store Dev Center]: https://dev.windows.com</span></span>
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
