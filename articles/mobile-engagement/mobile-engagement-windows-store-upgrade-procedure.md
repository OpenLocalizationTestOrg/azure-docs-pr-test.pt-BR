---
title: "aaaWindows procedimentos de atualização do SDK de aplicativos Universal"
description: "Procedimentos de atualização do SDK do Windows Universal para o Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 4c898175-2cd6-43db-b350-bb408332f24d
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 95aba5d55cd65d4190aad35737f872414b5ed443
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="windows-universal-apps-sdk-upgrade-procedures"></a><span data-ttu-id="67066-103">Procedimentos de atualização de aplicativos do Windows Universal</span><span class="sxs-lookup"><span data-stu-id="67066-103">Windows Universal Apps SDK Upgrade Procedures</span></span>
<span data-ttu-id="67066-104">Se você já tiver integrado uma versão mais antiga do contrato em seu aplicativo, você tem Olá tooconsider pontos a seguir ao atualizar Olá SDK.</span><span class="sxs-lookup"><span data-stu-id="67066-104">If you already have integrated an older version of Engagement into your application, you have tooconsider hello following points when upgrading hello SDK.</span></span>

<span data-ttu-id="67066-105">Você pode ter vários procedimentos de toofollow se perdidas várias versões do SDK de saudação.</span><span class="sxs-lookup"><span data-stu-id="67066-105">You may have toofollow several procedures if you missed several versions of hello SDK.</span></span> <span data-ttu-id="67066-106">Por exemplo, se você migrar de 0.10.1 too0.11.0 ter toofirst siga hello "de 0.9.0 too0.10.1" procedimento e hello "de 0.10.1 too0.11.0" procedimento.</span><span class="sxs-lookup"><span data-stu-id="67066-106">For example if you migrate from 0.10.1 too0.11.0 you have toofirst follow hello "from 0.9.0 too0.10.1" procedure then hello "from 0.10.1 too0.11.0" procedure.</span></span>

## <a name="from-330-too340"></a><span data-ttu-id="67066-107">De 3.3.0 too3.4.0</span><span class="sxs-lookup"><span data-stu-id="67066-107">From 3.3.0 too3.4.0</span></span>
### <a name="test-logs"></a><span data-ttu-id="67066-108">Logs de teste</span><span class="sxs-lookup"><span data-stu-id="67066-108">Test logs</span></span>
<span data-ttu-id="67066-109">Logs do console produzidos pelo Olá SDK agora podem ser habilitado/desabilitado/filtradas.</span><span class="sxs-lookup"><span data-stu-id="67066-109">Console logs produced by hello SDK can now be enabled/disabled/filtered.</span></span> <span data-ttu-id="67066-110">toocustomize, propriedade de saudação update `EngagementAgent.Instance.TestLogEnabled` tooone do valor de saudação disponível de saudação `EngagementTestLogLevel` enumeração, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="67066-110">toocustomize this, update hello property `EngagementAgent.Instance.TestLogEnabled` tooone of hello value available from hello `EngagementTestLogLevel` enumeration, for instance:</span></span>

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

### <a name="resources"></a><span data-ttu-id="67066-111">Recursos</span><span class="sxs-lookup"><span data-stu-id="67066-111">Resources</span></span>
<span data-ttu-id="67066-112">sobreposição de alcance Olá foi aprimorada.</span><span class="sxs-lookup"><span data-stu-id="67066-112">hello Reach overlay has been improved.</span></span> <span data-ttu-id="67066-113">Ele faz parte dos recursos de pacote do NuGet do SDK hello.</span><span class="sxs-lookup"><span data-stu-id="67066-113">It is part of hello SDK NuGet package resources.</span></span>

<span data-ttu-id="67066-114">Durante a atualização toohello nova versão de hello SDK, você pode escolher que se deseja tookeep os arquivos existentes do hello sobreposição de pasta de seus recursos ou não:</span><span class="sxs-lookup"><span data-stu-id="67066-114">While upgrading toohello new version of hello SDK you can choose whether you want tookeep your existing files from hello overlay folder of your resources or not:</span></span>

* <span data-ttu-id="67066-115">Se sobreposição anterior hello está funcionando para você ou você estiver integrando Olá `WebView` elementos manualmente e em seguida, você pode decidir tookeep os arquivos existentes, continuará a funcionar.</span><span class="sxs-lookup"><span data-stu-id="67066-115">If hello previous overlay is working for you or you are integrating hello `WebView` elements manually then you can decide tookeep your exiting files, it will still work.</span></span> 
* <span data-ttu-id="67066-116">Se você quiser tooupdate toohello nova sobreposição, substituir apenas Olá todo `overlay` pasta de seus recursos com hello um novo pacote do SDK de saudação (aplicativos UWP: após a atualização de hello, você pode obter nova pasta de sobreposição de saudação do % USERPROFILE %\\. nuget\ packages\MicrosoftAzure.MobileEngagement\3.4.0\content\win81\Resources).</span><span class="sxs-lookup"><span data-stu-id="67066-116">If you want tooupdate toohello new overlay, just replace hello whole `overlay` folder from your resources with hello new one from hello SDK package (UWP apps: after hello upgrade, you can get hello new overlay folder from %USERPROFILE%\\.nuget\packages\MicrosoftAzure.MobileEngagement\3.4.0\content\win81\Resources).</span></span>

> [!WARNING]
> <span data-ttu-id="67066-117">Usando a sobreposição de novo Olá substituirá todas as personalizações feitas na versão anterior do hello.</span><span class="sxs-lookup"><span data-stu-id="67066-117">Using hello new overlay will overwrite any customizations made on hello previous version.</span></span>
> 
> 

## <a name="from-320-too330"></a><span data-ttu-id="67066-118">De 3.2.0 too3.3.0</span><span class="sxs-lookup"><span data-stu-id="67066-118">From 3.2.0 too3.3.0</span></span>
### <a name="resources"></a><span data-ttu-id="67066-119">Recursos</span><span class="sxs-lookup"><span data-stu-id="67066-119">Resources</span></span>
<span data-ttu-id="67066-120">Esta etapa aborda apenas os recursos personalizados.</span><span class="sxs-lookup"><span data-stu-id="67066-120">This step concerns customized resources only.</span></span> <span data-ttu-id="67066-121">Se você tiver personalizado o recursos de Olá fornecidos por Olá SDK (html, imagens, sobreposição), você terá que toobackup-los antes de atualizar e reaplicar a personalização em atualizado recursos.</span><span class="sxs-lookup"><span data-stu-id="67066-121">If you have customized hello resources provided by hello SDK (html, images, overlay) then you have toobackup them before upgrading and reapply your customization on upgraded resources.</span></span>

## <a name="from-310-too320"></a><span data-ttu-id="67066-122">De 3.1.0 too3.2.0</span><span class="sxs-lookup"><span data-stu-id="67066-122">From 3.1.0 too3.2.0</span></span>
### <a name="resources"></a><span data-ttu-id="67066-123">Recursos</span><span class="sxs-lookup"><span data-stu-id="67066-123">Resources</span></span>
<span data-ttu-id="67066-124">Esta etapa aborda apenas os recursos personalizados.</span><span class="sxs-lookup"><span data-stu-id="67066-124">This step concerns customized resources only.</span></span> <span data-ttu-id="67066-125">Se você tiver personalizado o recursos de Olá fornecidos por Olá SDK (html, imagens, sobreposição), você terá que toobackup-los antes de atualizar e reaplicar a personalização em atualizado recursos.</span><span class="sxs-lookup"><span data-stu-id="67066-125">If you have customized hello resources provided by hello SDK (html, images, overlay) then you have toobackup them before upgrading and reapply your customization on upgraded resources.</span></span>

### <a name="webview-integration"></a><span data-ttu-id="67066-126">Integração do Modo de exibição da Web</span><span class="sxs-lookup"><span data-stu-id="67066-126">Webview integration</span></span>
<span data-ttu-id="67066-127">Algumas melhorias toomatch diferentes fatores foram introduzidos nesta versão.</span><span class="sxs-lookup"><span data-stu-id="67066-127">Some improvements toomatch different device form factors were introduced in this version.</span></span> <span data-ttu-id="67066-128">Certifique-se de que a integração do webview Olá corresponde seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="67066-128">Make sure that your integration of hello webview match hello following:</span></span>

<span data-ttu-id="67066-129">Na página XAML ():</span><span class="sxs-lookup"><span data-stu-id="67066-129">In your XAML page ():</span></span>

            <WebView x:Name="engagement_notification_content" Visibility="Collapsed" Height="80" HorizontalAlignment="Right" VerticalAlignment="Top"/>
            <WebView x:Name="engagement_announcement_content" Visibility="Collapsed" HorizontalAlignment="Right" VerticalAlignment="Top"/> 

<span data-ttu-id="67066-130">E no arquivo .cs associado:</span><span class="sxs-lookup"><span data-stu-id="67066-130">And in your associated .cs file:</span></span>

    using Microsoft.Azure.Engagement;
    using System;
    using Windows.ApplicationModel.Core;
    using Windows.UI.ViewManagement;
    using Windows.UI.Xaml;
    using Windows.UI.Xaml.Navigation;

    namespace My.Namespace.Example
    {
            /// <summary>
            /// An empty page that can be used on its own or navigated toowithin a Frame.
            /// </summary>
            public sealed partial class ExampleEngagementReachPage : EngagementPage
            {
              public ExampleEngagementReachPage()
              {
                this.InitializeComponent();

                /* Set your webview elements toohello correct size. */
                SetWebView(width, height);
              }

              #region tooimplement
              /* Attach events when page is navigated. */
              protected override void OnNavigatedTo(NavigationEventArgs e)
              {
                /* Update hello webview when hello app window is resized. */
                Window.Current.SizeChanged += DisplayProperties_OrientationChanged;

                /* Update hello webview when hello app/status bar is resized. */
    #if WINDOWS_PHONE_APP || WINDOWS_UWP
                ApplicationView.GetForCurrentView().VisibleBoundsChanged += DisplayProperties_VisibleBoundsChanged; 
    #endif
                base.OnNavigatedTo(e);
              }

              /* When page is left ensure toodetach SizeChanged handler. */
              protected override void OnNavigatedFrom(NavigationEventArgs e)
              {
                Window.Current.SizeChanged -= DisplayProperties_OrientationChanged;
    #if WINDOWS_PHONE_APP || WINDOWS_UWP
                ApplicationView.GetForCurrentView().VisibleBoundsChanged -= DisplayProperties_VisibleBoundsChanged;
    #endif
                base.OnNavigatedFrom(e);
              }

              /* "width" and "height" are hello current size of your application display. */
    #if WINDOWS_PHONE_APP || WINDOWS_UWP
              double width = ApplicationView.GetForCurrentView().VisibleBounds.Width;
              double height = ApplicationView.GetForCurrentView().VisibleBounds.Height;
    #else
              double width =  Window.Current.Bounds.Width;
              double height =  Window.Current.Bounds.Height;
    #endif

              /// <summary>
              /// Set your webview elements toohello correct size.
              /// </summary>
              /// <param name="width">hello width of your current display.</param>
              /// <param name="height">hello height of your current display.</param>
              private void SetWebView(double width, double height)
              {
                #pragma warning disable 4014
                CoreApplication.MainView.CoreWindow.Dispatcher.RunAsync(Windows.UI.Core.CoreDispatcherPriority.Normal,
                        () =>
                        {
                          this.engagement_notification_content.Width = width;
                          this.engagement_announcement_content.Width = width;
                          this.engagement_announcement_content.Height = height;
                        });
              }

              /// <summary>
              /// Handler that takes hello Windows.Current.SizeChanged and indicates that webviews have toobe resized.
              /// </summary>
              /// <param name="sender">Original event trigger.</param>
              /// <param name="e">Window Size Changed Event arguments.</param>
              private void DisplayProperties_OrientationChanged(object sender, Windows.UI.Core.WindowSizeChangedEventArgs e)
              {
                double width = e.Size.Width;
                double height = e.Size.Height;

                /* Set your webview elements toohello correct size. */
                SetWebView(width, height);
              }

    #if WINDOWS_PHONE_APP || WINDOWS_UWP              
              /// <summary>
              /// Handler that takes hello ApplicationView.VisibleBoundsChanged and indicates that webviews have toobe resized
              /// </summary>
              /// <param name="sender">hello related application view.</param>
              /// <param name="e">Related event arguments.</param>
              private void DisplayProperties_VisibleBoundsChanged(ApplicationView sender, Object e)
              {
                double width = sender.VisibleBounds.Width;
                double height = sender.VisibleBounds.Height;

                /* Set your webview elements toohello correct size. */
                SetWebView(width, height);
              }
    #endif
              #endregion
            }
    }

## <a name="from-200-too300"></a><span data-ttu-id="67066-131">De 2.0.0 too3.0.0</span><span class="sxs-lookup"><span data-stu-id="67066-131">From 2.0.0 too3.0.0</span></span>
### <a name="resources"></a><span data-ttu-id="67066-132">Recursos</span><span class="sxs-lookup"><span data-stu-id="67066-132">Resources</span></span>
<span data-ttu-id="67066-133">Esta etapa aborda apenas os recursos personalizados.</span><span class="sxs-lookup"><span data-stu-id="67066-133">This step concerns customized resources only.</span></span> <span data-ttu-id="67066-134">Se você tiver personalizado o recursos de Olá fornecidos por Olá SDK (html, imagens, sobreposição), você terá que toobackup-los antes de atualizar e reaplicar a personalização em atualizado recursos.</span><span class="sxs-lookup"><span data-stu-id="67066-134">If you have customized hello resources provided by hello SDK (html, images, overlay) then you have toobackup them before upgrading and reapply your customization on upgraded resources.</span></span>

## <a name="from-111-too200"></a><span data-ttu-id="67066-135">De 1.1.1 too2.0.0</span><span class="sxs-lookup"><span data-stu-id="67066-135">From 1.1.1 too2.0.0</span></span>
<span data-ttu-id="67066-136">Olá a seguir descrevem como toomigrate uma integração SDK da saudação Capptain serviço oferecido pelo Capptain SAS em um aplicativo da plataforma do Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="67066-136">hello following describes how toomigrate an SDK integration from hello Capptain service offered by Capptain SAS into an app powered by Azure Mobile Engagement.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="67066-137">Capptain e o compromisso de mobilidade não são Olá mesmos serviços e procedimento Olá indicado abaixo só destaca como toomigrate Olá aplicativo cliente.</span><span class="sxs-lookup"><span data-stu-id="67066-137">Capptain and Mobile Engagement are not hello same services and hello procedure given below only highlights how toomigrate hello client app.</span></span> <span data-ttu-id="67066-138">Migrando Olá SDK no aplicativo hello não vai migrar seus dados do hello Capptain toohello Mobile Engagement de servidores</span><span class="sxs-lookup"><span data-stu-id="67066-138">Migrating hello SDK in hello app will NOT migrate your data from hello Capptain servers toohello Mobile Engagement servers</span></span>
> 
> 

<span data-ttu-id="67066-139">Se você estiver migrando de uma versão anterior, consulte Olá Capptain site da web toomigrate too1.1.1 primeiro e aplicar Olá procedimento</span><span class="sxs-lookup"><span data-stu-id="67066-139">If you are migrating from an earlier version, please consult hello Capptain web site toomigrate too1.1.1 first then apply hello following procedure</span></span>

### <a name="nuget-package"></a><span data-ttu-id="67066-140">Pacote NuGet</span><span class="sxs-lookup"><span data-stu-id="67066-140">Nuget package</span></span>
<span data-ttu-id="67066-141">Substitua **Capptain.WindowsPhone** pelo pacote Nuget **MicrosoftAzure.MobileEngagement**.</span><span class="sxs-lookup"><span data-stu-id="67066-141">Replace **Capptain.WindowsPhone** by **MicrosoftAzure.MobileEngagement** Nuget package.</span></span>

### <a name="applying-mobile-engagement"></a><span data-ttu-id="67066-142">Aplicando o Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="67066-142">Applying Mobile Engagement</span></span>
<span data-ttu-id="67066-143">Olá SDK usa o termo Olá `Engagement`.</span><span class="sxs-lookup"><span data-stu-id="67066-143">hello SDK uses hello term `Engagement`.</span></span> <span data-ttu-id="67066-144">Você precisa tooupdate toomatch seu projeto essa alteração.</span><span class="sxs-lookup"><span data-stu-id="67066-144">You need tooupdate your project toomatch this change.</span></span>

<span data-ttu-id="67066-145">É necessário toouninstall seu pacote do nuget Capptain atual.</span><span class="sxs-lookup"><span data-stu-id="67066-145">You need toouninstall your current Capptain nuget package.</span></span> <span data-ttu-id="67066-146">Considere que todas as alterações na pasta de recursos Capptain serão removidas.</span><span class="sxs-lookup"><span data-stu-id="67066-146">Consider that all your changes in Capptain Resources folder will be removed.</span></span> <span data-ttu-id="67066-147">Se você quiser tookeep esses arquivos, em seguida, faça uma cópia deles.</span><span class="sxs-lookup"><span data-stu-id="67066-147">If you want tookeep those files then make a copy of them.</span></span>

<span data-ttu-id="67066-148">Depois disso, instale o novo pacote de nuget de contrato do Microsoft Azure Olá no seu projeto.</span><span class="sxs-lookup"><span data-stu-id="67066-148">After that, install hello new Microsoft Azure Engagement nuget package on your project.</span></span> <span data-ttu-id="67066-149">Você pode encontrá-lo diretamente no [site do nuget].</span><span class="sxs-lookup"><span data-stu-id="67066-149">You can find it directly on [nuget website].</span></span> <span data-ttu-id="67066-150">ou aqui no índice.</span><span class="sxs-lookup"><span data-stu-id="67066-150">or here index.</span></span> <span data-ttu-id="67066-151">Substitui essa ação, todos os arquivos de recursos usado pelo contrato e adiciona Olá novo contrato DLL tooyour referências de projeto.</span><span class="sxs-lookup"><span data-stu-id="67066-151">This action replaces all resources files used by Engagement and adds hello new Engagement DLL tooyour project References.</span></span>

<span data-ttu-id="67066-152">Você tem as referências do projeto tooclean excluindo referências Capptain DLL.</span><span class="sxs-lookup"><span data-stu-id="67066-152">You have tooclean your project references by deleting Capptain DLL references.</span></span> <span data-ttu-id="67066-153">Se você não fizer isso, versão de saudação do Capptain entrarão em conflito e ocorrerão erros.</span><span class="sxs-lookup"><span data-stu-id="67066-153">If you do not make this, hello version of Capptain will conflict and errors will happen.</span></span>

<span data-ttu-id="67066-154">Se você tiver personalizado Capptain recursos, copie o conteúdo de arquivos antigos e colá-los em novos arquivos de contrato hello.</span><span class="sxs-lookup"><span data-stu-id="67066-154">If you have customized Capptain resources, copy your old files content and paste them in hello new Engagement files.</span></span> <span data-ttu-id="67066-155">Observe que os arquivos xaml e o cs toobe atualizado.</span><span class="sxs-lookup"><span data-stu-id="67066-155">Please note that both xaml and cs files have toobe updated.</span></span>

<span data-ttu-id="67066-156">Quando essas etapas forem concluídas, você só tem referências antigas de Capptain tooreplace por novas referências de contrato hello.</span><span class="sxs-lookup"><span data-stu-id="67066-156">When those steps are completed you only have tooreplace old Capptain references by hello new Engagement references.</span></span>

1. <span data-ttu-id="67066-157">Todos os namespaces Capptain ter toobe atualizado.</span><span class="sxs-lookup"><span data-stu-id="67066-157">All Capptain namespaces have toobe updated.</span></span>
   
    <span data-ttu-id="67066-158">Antes da migração:</span><span class="sxs-lookup"><span data-stu-id="67066-158">Before migration:</span></span>
   
        using Capptain.Agent;
        using Capptain.Reach;
   
    <span data-ttu-id="67066-159">Após a migração:</span><span class="sxs-lookup"><span data-stu-id="67066-159">After migration:</span></span>
   
        using Microsoft.Azure.Engagement;
2. <span data-ttu-id="67066-160">Todas as classes Capptain que contêm "Capptain" devem conter “Engagement".</span><span class="sxs-lookup"><span data-stu-id="67066-160">All Capptain classes that contain "Capptain" should contain "Engagement".</span></span>
   
    <span data-ttu-id="67066-161">Antes da migração:</span><span class="sxs-lookup"><span data-stu-id="67066-161">Before migration:</span></span>
   
        public sealed partial class MainPage : CapptainPage
        {
          protected override string GetCapptainPageName()
          {
            return "Capptain Demo";
          }
          ...
        }
   
    <span data-ttu-id="67066-162">Após a migração:</span><span class="sxs-lookup"><span data-stu-id="67066-162">After migration:</span></span>
   
        public sealed partial class MainPage : EngagementPage
        {
          protected override string GetEngagementPageName()
          {
            return "Engagement Demo";
          }
          ...
        }
3. <span data-ttu-id="67066-163">Para os arquivos xaml o namespace e atributos Capptain também se alteram.</span><span class="sxs-lookup"><span data-stu-id="67066-163">For xaml files Capptain namespace and attributes also change.</span></span>
   
    <span data-ttu-id="67066-164">Antes da migração:</span><span class="sxs-lookup"><span data-stu-id="67066-164">Before migration:</span></span>
   
        <capptain:CapptainPage
        ...
        xmlns:capptain="clr-namespace:Capptain.Agent;assembly=Capptain.Agent.WP"
        ...
        </capptain:CapptainPage>
   
    <span data-ttu-id="67066-165">Após a migração:</span><span class="sxs-lookup"><span data-stu-id="67066-165">After migration:</span></span>
   
        <engagement:EngagementPage
        ...
        xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
        ...
        </engagement:EngagementPage>
4. <span data-ttu-id="67066-166">Alterações na página de sobreposição</span><span class="sxs-lookup"><span data-stu-id="67066-166">Overlay page changes</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="67066-167">A sobreposição também será alterada.</span><span class="sxs-lookup"><span data-stu-id="67066-167">Overlay also changes.</span></span> <span data-ttu-id="67066-168">O novo namespace é `Microsoft.Azure.Engagement.Overlay`.</span><span class="sxs-lookup"><span data-stu-id="67066-168">Its new namespace is `Microsoft.Azure.Engagement.Overlay`.</span></span> <span data-ttu-id="67066-169">Ele tem toobe usado nos arquivos xaml e o cs.</span><span class="sxs-lookup"><span data-stu-id="67066-169">It has toobe used in both xaml and cs files.</span></span> <span data-ttu-id="67066-170">Além disso `CapptainGrid` toobe chamado `EngagementGrid`, `capptain_notification_content` e `capptain_announcement_content` são nomeados `engagement_notification_content` e `engagement_announcement_content`.</span><span class="sxs-lookup"><span data-stu-id="67066-170">Moreover `CapptainGrid` is toobe named `EngagementGrid`, `capptain_notification_content` and `capptain_announcement_content` are named `engagement_notification_content` and `engagement_announcement_content`.</span></span>
   > 
   > 
   
    <span data-ttu-id="67066-171">Para sobreposição:</span><span class="sxs-lookup"><span data-stu-id="67066-171">For overlay :</span></span>
   
        <capptain:CapptainPageOverlay
          xmlns:capptain="using:Capptain.Overlay"
          ...
        </capptain:CapptainPageOverlay>
   
    <span data-ttu-id="67066-172">Torna-se:</span><span class="sxs-lookup"><span data-stu-id="67066-172">It becomes :</span></span>
   
        <EngagementPageOverlay
          engagement="using:Microsoft.Azure.Engagement.Overlay"
          ...
        </engagement:EngagementPageOverlay>
5. <span data-ttu-id="67066-173">Para Olá a outros recursos como Capptain imagens e arquivos HTML, observe que eles foram renomeado toouse "Contrato".</span><span class="sxs-lookup"><span data-stu-id="67066-173">For hello other resources like Capptain pictures and HTML files, please note that they also have been renamed toouse "Engagement".</span></span>

### <a name="project-declaration"></a><span data-ttu-id="67066-174">Declaração do projeto</span><span class="sxs-lookup"><span data-stu-id="67066-174">Project declaration</span></span>
<span data-ttu-id="67066-175">Em Package.appxmanifest `File Type Associations` foi atualizado a partir de:</span><span class="sxs-lookup"><span data-stu-id="67066-175">On Package.appxmanifest `File Type Associations` has been updated from :</span></span>

* <span data-ttu-id="67066-176">capptain\_alcançar\_tooengagement conteúdo\_alcançar\_conteúdo</span><span class="sxs-lookup"><span data-stu-id="67066-176">capptain\_reach\_content tooengagement\_reach\_content</span></span>
* <span data-ttu-id="67066-177">capptain\_log\_arquivo tooengagement\_log\_arquivo</span><span class="sxs-lookup"><span data-stu-id="67066-177">capptain\_log\_file tooengagement\_log\_file</span></span>

### <a name="application-id--sdk-key"></a><span data-ttu-id="67066-178">ID do aplicativo / chave do SDK</span><span class="sxs-lookup"><span data-stu-id="67066-178">Application ID / SDK Key</span></span>
<span data-ttu-id="67066-179">O Engagement usa uma cadeia de conexão.</span><span class="sxs-lookup"><span data-stu-id="67066-179">Engagement uses a connection string.</span></span> <span data-ttu-id="67066-180">Você não tem toospecify uma ID de aplicativo e uma chave do SDK com o Mobile Engagement, tiver apenas toospecify uma cadeia de caracteres de conexão.</span><span class="sxs-lookup"><span data-stu-id="67066-180">You don't have toospecify an application ID and an SDK key with Mobile Engagement, you only have toospecify a connection string.</span></span> <span data-ttu-id="67066-181">Você pode configurá-la em seu arquivo EngagementConfiguration.</span><span class="sxs-lookup"><span data-stu-id="67066-181">You can set it up on your EngagementConfiguration file.</span></span>

<span data-ttu-id="67066-182">configuração do contrato Olá pode ser definida em sua `Resources\EngagementConfiguration.xml` arquivo do projeto.</span><span class="sxs-lookup"><span data-stu-id="67066-182">hello Engagement configuration can be set in your `Resources\EngagementConfiguration.xml` file of your project.</span></span>

<span data-ttu-id="67066-183">Edite esse arquivo toospecify:</span><span class="sxs-lookup"><span data-stu-id="67066-183">Edit this file toospecify:</span></span>

* <span data-ttu-id="67066-184">A cadeia de conexão do aplicativo entre as marcas `<connectionString>` and `<\connectionString>`.</span><span class="sxs-lookup"><span data-stu-id="67066-184">Your application connection string between tags `<connectionString>` and `<\connectionString>`.</span></span>

<span data-ttu-id="67066-185">Se você quiser toospecify em tempo de execução em vez disso, você pode chamar a seguir Olá método antes da inicialização de agente do hello contrato:</span><span class="sxs-lookup"><span data-stu-id="67066-185">If you want toospecify it at runtime instead, you can call hello following method before hello Engagement agent initialization:</span></span>

    /* Engagement configuration. */
    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

    /* Initialize Engagement agent with above configuration. */
    EngagementAgent.Instance.Init(args, engagementConfiguration);

<span data-ttu-id="67066-186">cadeia de caracteres de conexão de saudação para seu aplicativo é exibida em Olá Portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="67066-186">hello connection string for your application is displayed on hello Azure Classic Portal.</span></span>

### <a name="items-name-change"></a><span data-ttu-id="67066-187">Alteração do nome de itens</span><span class="sxs-lookup"><span data-stu-id="67066-187">Items name change</span></span>
<span data-ttu-id="67066-188">Todos os itens chamados *capptain* foram nomeados como *engagement*.</span><span class="sxs-lookup"><span data-stu-id="67066-188">All items named *capptain* have been named *engagement*.</span></span> <span data-ttu-id="67066-189">Da mesma forma para *Capptain* muito*contrato*.</span><span class="sxs-lookup"><span data-stu-id="67066-189">Similarly for *Capptain* too*Engagement*.</span></span>

<span data-ttu-id="67066-190">Exemplos de itens do Capptain usados normalmente :</span><span class="sxs-lookup"><span data-stu-id="67066-190">Examples of commonly used Capptain items :</span></span>

* <span data-ttu-id="67066-191">CapptainConfiguration agora denominado EngagementConfiguration</span><span class="sxs-lookup"><span data-stu-id="67066-191">CapptainConfiguration now named EngagementConfiguration</span></span>
* <span data-ttu-id="67066-192">CapptainAgent agora denominado EngagementAgent</span><span class="sxs-lookup"><span data-stu-id="67066-192">CapptainAgent now named EngagementAgent</span></span>
* <span data-ttu-id="67066-193">CapptainReach agora denominado EngagementReach</span><span class="sxs-lookup"><span data-stu-id="67066-193">CapptainReach now named EngagementReach</span></span>
* <span data-ttu-id="67066-194">CapptainHttpConfig agora denominado EngagementHttpConfig</span><span class="sxs-lookup"><span data-stu-id="67066-194">CapptainHttpConfig now named EngagementHttpConfig</span></span>
* <span data-ttu-id="67066-195">GetCapptainPageName agora denominado GetEngagementPageName</span><span class="sxs-lookup"><span data-stu-id="67066-195">GetCapptainPageName now named GetEngagementPageName</span></span>

<span data-ttu-id="67066-196">Observe que renomear também afeta métodos substituídos.</span><span class="sxs-lookup"><span data-stu-id="67066-196">Note that rename also affects overridden methods.</span></span>

