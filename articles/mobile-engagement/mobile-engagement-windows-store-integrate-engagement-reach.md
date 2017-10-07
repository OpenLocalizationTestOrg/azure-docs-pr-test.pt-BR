---
title: "aaaWindows alcançar integração para o SDK do Universal aplicativos"
description: Como tooIntegrate do Azure Mobile Engagement atingir com aplicativos universais do Windows
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: a31ca1d6-856f-4aec-898a-07969ae5f7ec
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: af311c65940014083333853875a00173b8d6783e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="windows-universal-apps-reach-sdk-integration"></a><span data-ttu-id="2eb9b-103">Integração do SDK do Reach do Windows Universal</span><span class="sxs-lookup"><span data-stu-id="2eb9b-103">Windows Universal Apps Reach SDK Integration</span></span>
<span data-ttu-id="2eb9b-104">Você deve seguir Olá integração procedimento descrito em Olá [integração do SDK do Windows Universal contrato](mobile-engagement-windows-store-integrate-engagement.md) antes de seguir este guia.</span><span class="sxs-lookup"><span data-stu-id="2eb9b-104">You must follow hello integration procedure described in hello [Windows Universal Engagement SDK Integration](mobile-engagement-windows-store-integrate-engagement.md) before following this guide.</span></span>

## <a name="embed-hello-engagement-reach-sdk-into-your-windows-universal-project"></a><span data-ttu-id="2eb9b-105">Inserir saudação SDK do Reach contrato em seu projeto Universal do Windows</span><span class="sxs-lookup"><span data-stu-id="2eb9b-105">Embed hello Engagement Reach SDK into your Windows Universal project</span></span>
<span data-ttu-id="2eb9b-106">Você não tem nada tooadd.</span><span class="sxs-lookup"><span data-stu-id="2eb9b-106">You do not have anything tooadd.</span></span> <span data-ttu-id="2eb9b-107">`EngagementReach` já estão em seu projeto.</span><span class="sxs-lookup"><span data-stu-id="2eb9b-107">`EngagementReach` references and resources are already in your project.</span></span>

> [!TIP]
> <span data-ttu-id="2eb9b-108">Você poderá personalizar as imagens localizadas em Olá `Resources` pasta do seu projeto, especialmente Olá marca ícone (esse padrão toohello contrato).</span><span class="sxs-lookup"><span data-stu-id="2eb9b-108">You can customize images located in hello `Resources` folder of your project, especially hello brand icon (that default toohello Engagement icon).</span></span> <span data-ttu-id="2eb9b-109">Em aplicativos Universal, você também pode mover Olá `Resources` pasta no seu tooshare projeto compartilhado seu conteúdo entre aplicativos, mas você terá Olá tookeep `Resources\EngagementConfiguration.xml` em seu local padrão de arquivo à medida que é dependente de plataforma.</span><span class="sxs-lookup"><span data-stu-id="2eb9b-109">On Universal Apps you can also move hello `Resources` folder on your shared project tooshare its content between apps, but you will have tookeep hello `Resources\EngagementConfiguration.xml` file on its default location as it is platform dependent.</span></span>
> 
> 

## <a name="enable-hello-windows-notification-service"></a><span data-ttu-id="2eb9b-110">Habilitar Olá serviço de notificação do Windows</span><span class="sxs-lookup"><span data-stu-id="2eb9b-110">Enable hello Windows Notification Service</span></span>
### <a name="windows-8x-and-windows-phone-81-only"></a><span data-ttu-id="2eb9b-111">Somente Windows 8.x e Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="2eb9b-111">Windows 8.x and Windows Phone 8.1 only</span></span>
<span data-ttu-id="2eb9b-112">Na saudação de toouse ordem **serviço de notificação do Windows** (conhecido como WNS) em sua `Package.appxmanifest` de arquivo no `Application UI` clique em `All Image Assets` na caixa de bot esquerdo hello.</span><span class="sxs-lookup"><span data-stu-id="2eb9b-112">In order toouse hello **Windows Notification Service** (referred as WNS) in your `Package.appxmanifest` file on `Application UI` click on `All Image Assets` in hello left bot box.</span></span> <span data-ttu-id="2eb9b-113">A saudação à direita da caixa de saudação em `Notifications`, alterar `toast capable` de `(not set)` muito`(Yes)`.</span><span class="sxs-lookup"><span data-stu-id="2eb9b-113">At hello right of hello box in `Notifications`, change `toast capable` from `(not set)` too`(Yes)`.</span></span>

### <a name="all-platforms"></a><span data-ttu-id="2eb9b-114">Todas as plataformas</span><span class="sxs-lookup"><span data-stu-id="2eb9b-114">All platforms</span></span>
<span data-ttu-id="2eb9b-115">É necessário toosynchronize seu aplicativo tooyour conta e toohello contrato plataforma Microsoft.</span><span class="sxs-lookup"><span data-stu-id="2eb9b-115">You need toosynchronize your app tooyour Microsoft account and toohello engagement platform.</span></span> <span data-ttu-id="2eb9b-116">Para isso você precisa toocreate uma conta ou logon [Centro de desenvolvimento do windows](https://dev.windows.com).</span><span class="sxs-lookup"><span data-stu-id="2eb9b-116">For this you need toocreate an account or log on [windows dev center](https://dev.windows.com).</span></span> <span data-ttu-id="2eb9b-117">Depois que criar um novo aplicativo e localizar Olá SID e a chave secreta.</span><span class="sxs-lookup"><span data-stu-id="2eb9b-117">After that create a new application and find hello SID and secret key.</span></span> <span data-ttu-id="2eb9b-118">Em Olá contrato front-end, vá em sua configuração de aplicativo em `native push` e cole as suas credenciais.</span><span class="sxs-lookup"><span data-stu-id="2eb9b-118">On hello engagement frontend, go on your app setting in `native push` and paste your credentials.</span></span> <span data-ttu-id="2eb9b-119">Depois disso, clique com botão direito no projeto, selecione `store` e `Associate App with hello Store...`.</span><span class="sxs-lookup"><span data-stu-id="2eb9b-119">After that, right click on your project, select `store` and `Associate App with hello Store...`.</span></span> <span data-ttu-id="2eb9b-120">Você precisa apenas o aplicativo de hello tooselect ter criá antes de toosynchronize-lo.</span><span class="sxs-lookup"><span data-stu-id="2eb9b-120">You just need tooselect hello application you have create before toosynchronize it.</span></span>

## <a name="initialize-hello-engagement-reach-sdk"></a><span data-ttu-id="2eb9b-121">Inicializar Olá contrato SDK do Reach</span><span class="sxs-lookup"><span data-stu-id="2eb9b-121">Initialize hello Engagement Reach SDK</span></span>
<span data-ttu-id="2eb9b-122">Modificar Olá `App.xaml.cs`:</span><span class="sxs-lookup"><span data-stu-id="2eb9b-122">Modify hello `App.xaml.cs`:</span></span>

* <span data-ttu-id="2eb9b-123">Insira `EngagementReach.Instance.Init` logo após `EngagementAgent.Instance.Init` no método `InitEngagement`:</span><span class="sxs-lookup"><span data-stu-id="2eb9b-123">Insert `EngagementReach.Instance.Init` just after `EngagementAgent.Instance.Init` in your `InitEngagement` method:</span></span>
  
      private void InitEngagement(IActivatedEventArgs e)
      {
        EngagementAgent.Instance.Init(e);
        EngagementReach.Instance.Init(e);
      }
  
  <span data-ttu-id="2eb9b-124">Olá `EngagementReach.Instance.Init` é executado em um thread dedicado.</span><span class="sxs-lookup"><span data-stu-id="2eb9b-124">hello `EngagementReach.Instance.Init` runs in a dedicated thread.</span></span> <span data-ttu-id="2eb9b-125">Você não tem toodo-lo por conta própria.</span><span class="sxs-lookup"><span data-stu-id="2eb9b-125">You do not have toodo it yourself.</span></span>

> [!NOTE]
> <span data-ttu-id="2eb9b-126">Se você estiver usando notificações por push em outro lugar no seu aplicativo, você tem muito[compartilhar seu canal push](#push-channel-sharing) com contrato alcançar.</span><span class="sxs-lookup"><span data-stu-id="2eb9b-126">If you are using push notifications elsewhere in your application then you have too[share your push channel](#push-channel-sharing) with Engagement Reach.</span></span>
> 
> 

## <a name="integration"></a><span data-ttu-id="2eb9b-127">Integração</span><span class="sxs-lookup"><span data-stu-id="2eb9b-127">Integration</span></span>
<span data-ttu-id="2eb9b-128">Contrato fornece exibições intersticiais e as faixas duas maneiras tooadd Olá alcance no aplicativo para notificações e pesquisas em seu aplicativo: Olá sobreposição de integração e integração manual do Olá web modos de exibição.</span><span class="sxs-lookup"><span data-stu-id="2eb9b-128">Engagement provides two ways tooadd hello Reach in-app banners and interstitial views for announcements and polls in your application: hello overlay integration and hello web views manual integration.</span></span> <span data-ttu-id="2eb9b-129">Você não deve combinar ambas as abordagem Olá mesma página.</span><span class="sxs-lookup"><span data-stu-id="2eb9b-129">You should not combine both approach on hello same page.</span></span>

<span data-ttu-id="2eb9b-130">Escolha Olá entre integração dois Olá podia ser resumida desta forma:</span><span class="sxs-lookup"><span data-stu-id="2eb9b-130">hello choice between hello two integration could be summarized this way:</span></span>

* <span data-ttu-id="2eb9b-131">Você pode escolher Olá sobreposição integração se já herda a suas páginas de saudação agente `EngagementPage`, é simplesmente uma questão de substituição `EngagementPage` por `EngagementPageOverlay` e `xmlns:engagement="using:Microsoft.Azure.Engagement"` por `xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"` nas suas páginas.</span><span class="sxs-lookup"><span data-stu-id="2eb9b-131">You may choose hello overlay integration if your pages already inherits from hello Agent `EngagementPage`, it's just a matter of replacing `EngagementPage` by `EngagementPageOverlay` and `xmlns:engagement="using:Microsoft.Azure.Engagement"` by `xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"` in your pages.</span></span>
* <span data-ttu-id="2eb9b-132">Você pode optar integração manual do Olá web exibições tooprecisely local Olá alcançar da interface do usuário em suas páginas ou se você não quiser tooadd outro páginas de nível tooyour de herança.</span><span class="sxs-lookup"><span data-stu-id="2eb9b-132">You may choose hello web views manual integration if you want tooprecisely place hello Reach UI within your pages or if you don't want tooadd another inheritance level tooyour pages.</span></span> 

### <a name="overlay-integration"></a><span data-ttu-id="2eb9b-133">Integração de sobreposição</span><span class="sxs-lookup"><span data-stu-id="2eb9b-133">Overlay integration</span></span>
<span data-ttu-id="2eb9b-134">sobreposição de contrato Olá dinamicamente adiciona elementos de interface do usuário Olá usados campanhas de alcance toodisplay em sua página.</span><span class="sxs-lookup"><span data-stu-id="2eb9b-134">hello Engagement overlay dynamically adds hello UI elements used toodisplay Reach campaigns in your page.</span></span> <span data-ttu-id="2eb9b-135">Se Olá sobreposição não é adequado para seu layout considere modos de exibição de web hello integração manual em vez disso.</span><span class="sxs-lookup"><span data-stu-id="2eb9b-135">If hello overlay doesn't suit your layout you should consider hello web views manual integration instead.</span></span>

<span data-ttu-id="2eb9b-136">Em sua alteração de arquivo. XAML `EngagementPage` referência muito`EngagementPageOverlay`</span><span class="sxs-lookup"><span data-stu-id="2eb9b-136">In your .xaml file change `EngagementPage` reference too`EngagementPageOverlay`</span></span>

* <span data-ttu-id="2eb9b-137">Adicione declarações de namespaces tooyour:</span><span class="sxs-lookup"><span data-stu-id="2eb9b-137">Add tooyour namespaces declarations:</span></span>
  
      xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"
* <span data-ttu-id="2eb9b-138">Substituir `engagement:EngagementPage` por `engagement:EngagementPageOverlay`:</span><span class="sxs-lookup"><span data-stu-id="2eb9b-138">Replace `engagement:EngagementPage` with `engagement:EngagementPageOverlay`:</span></span>

<span data-ttu-id="2eb9b-139">**Com EngagementPage:**</span><span class="sxs-lookup"><span data-stu-id="2eb9b-139">**With EngagementPage:**</span></span>

        <engagement:EngagementPage 
            xmlns:engagement="using:Microsoft.Azure.Engagement">

            <!-- Your layout -->
        </engagement:EngagementPage>

<span data-ttu-id="2eb9b-140">**Com EngagementPageOverlay:**</span><span class="sxs-lookup"><span data-stu-id="2eb9b-140">**With EngagementPageOverlay:**</span></span>

        <engagement:EngagementPageOverlay 
            xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay">

            <!-- Your layout -->
        </engagement:EngagementPageOverlay>

<span data-ttu-id="2eb9b-141">No seu arquivo .cs, marque a página em `EngagementPageOverlay` em vez de `EngagementPage` e importe `Microsoft.Azure.Engagement.Overlay`.</span><span class="sxs-lookup"><span data-stu-id="2eb9b-141">Then in your .cs file tag your page in `EngagementPageOverlay` instead of `EngagementPage` and import `Microsoft.Azure.Engagement.Overlay`.</span></span>

            using Microsoft.Azure.Engagement.Overlay;

* <span data-ttu-id="2eb9b-142">Substituir `EngagementPage` por `EngagementPageOverlay`:</span><span class="sxs-lookup"><span data-stu-id="2eb9b-142">Replace `EngagementPage` with `EngagementPageOverlay`:</span></span>

<span data-ttu-id="2eb9b-143">**Com EngagementPage:**</span><span class="sxs-lookup"><span data-stu-id="2eb9b-143">**With EngagementPage:**</span></span>

            using Microsoft.Azure.Engagement;

            namespace Example
            {
              public sealed partial class ExamplePage : EngagementPage
              {
                [...]
              }
            }

<span data-ttu-id="2eb9b-144">**Com EngagementPageOverlay:**</span><span class="sxs-lookup"><span data-stu-id="2eb9b-144">**With EngagementPageOverlay:**</span></span>

            using Microsoft.Azure.Engagement.Overlay;

            namespace Example
            {
              public sealed partial class ExamplePage : EngagementPageOverlay 
              {
                [...]
              }
            }


<span data-ttu-id="2eb9b-145">Olá sobreposição de contrato adiciona um `Grid` elemento na parte superior da página é composto de seu layout e hello dois `WebView` elementos uma saudação banner e Olá outros uma exibição intersticiais hello.</span><span class="sxs-lookup"><span data-stu-id="2eb9b-145">hello Engagement overlay adds a `Grid` element on top of your page composed of your layout and hello two `WebView` elements one for hello banner and hello other one for hello interstitial view.</span></span>

<span data-ttu-id="2eb9b-146">Você pode personalizar elementos de sobreposição de saudação diretamente no hello `EngagementPageOverlay.cs` arquivo.</span><span class="sxs-lookup"><span data-stu-id="2eb9b-146">You can customize hello overlay elements directly in hello `EngagementPageOverlay.cs` file.</span></span>

### <a name="web-views-manual-integration"></a><span data-ttu-id="2eb9b-147">Integração manual de exibições da Web</span><span class="sxs-lookup"><span data-stu-id="2eb9b-147">Web views manual integration</span></span>
<span data-ttu-id="2eb9b-148">Alcance irá procurar as páginas para Olá dois `WebView` elementos responsáveis para exibir a faixa de saudação e exibição intersticiais hello.</span><span class="sxs-lookup"><span data-stu-id="2eb9b-148">Reach will be searching your pages for hello two `WebView` elements responsible for displaying hello banner and hello interstitial view.</span></span> <span data-ttu-id="2eb9b-149">Olá somente ter toodo é tooadd desses dois `WebView` elementos em algum lugar em suas páginas, aqui está um exemplo:</span><span class="sxs-lookup"><span data-stu-id="2eb9b-149">hello only thing you have toodo is tooadd those two `WebView` elements somewhere in your pages, here is an example:</span></span>

    <Grid x:Name="engagementGrid">

      <!-- Your layout -->

      <WebView x:Name="engagement_notification_content" Visibility="Collapsed" Height="80" HorizontalAlignment="Stretch" VerticalAlignment="Top"/>
      <WebView x:Name="engagement_announcement_content" Visibility="Collapsed"  HorizontalAlignment="Stretch"  VerticalAlignment="Stretch"/>
    </Grid>


<span data-ttu-id="2eb9b-150">Em Olá Este exemplo `WebView` elementos é toofit ampliada seus contêineres que automaticamente tamanhos-los novamente em caso de alteração de tamanho de rotação ou janela de tela.</span><span class="sxs-lookup"><span data-stu-id="2eb9b-150">In this example hello `WebView` elements are stretched toofit their container which automatically re-sizes them in case of screen rotation or window size change.</span></span>

> [!WARNING]
> <span data-ttu-id="2eb9b-151">É importante tookeep Olá nomenclatura mesmo `engagement_notification_content` e `engagement_announcement_content` para Olá `WebView` elementos.</span><span class="sxs-lookup"><span data-stu-id="2eb9b-151">It is important tookeep hello same naming `engagement_notification_content` and `engagement_announcement_content` for hello `WebView` elements.</span></span> <span data-ttu-id="2eb9b-152">O Reach os identifica por seu nome.</span><span class="sxs-lookup"><span data-stu-id="2eb9b-152">Reach is identifying them by their name.</span></span> 
> 
> 

## <a name="handle-datapush-optional"></a><span data-ttu-id="2eb9b-153">Manipular o push de dados (opcional)</span><span class="sxs-lookup"><span data-stu-id="2eb9b-153">Handle datapush (optional)</span></span>
<span data-ttu-id="2eb9b-154">Se você quiser envios por push os aplicativo toobe tooreceive capaz de alcançar dados, você tem tooimplement dois eventos de saudação EngagementReach classe:</span><span class="sxs-lookup"><span data-stu-id="2eb9b-154">If you want your application toobe able tooreceive Reach data pushes, you have tooimplement two events of hello EngagementReach class:</span></span>

<span data-ttu-id="2eb9b-155">Em App.xaml.cs no construtor de App() Olá adicione:</span><span class="sxs-lookup"><span data-stu-id="2eb9b-155">In App.xaml.cs in hello App() constructor add:</span></span>

            EngagementReach.Instance.DataPushStringReceived += (body) =>
            {
              Debug.WriteLine("String data push message received: " + body);
              return true;
            };

            EngagementReach.Instance.DataPushBase64Received += (decodedBody, encodedBody) =>
            {
              Debug.WriteLine("Base64 data push message received: " + encodedBody);
              // Do something useful with decodedBody like updating an image view
              return true;
            };

<span data-ttu-id="2eb9b-156">Você pode ver o retorno de chamada saudação de cada método retorna um valor booleano.</span><span class="sxs-lookup"><span data-stu-id="2eb9b-156">You can see that hello callback of each method returns a boolean.</span></span> <span data-ttu-id="2eb9b-157">Contrato envia um feedback tooits back-end após distribuir dados por push-Olá.</span><span class="sxs-lookup"><span data-stu-id="2eb9b-157">Engagement sends a feedback tooits back-end after dispatching hello data push.</span></span> <span data-ttu-id="2eb9b-158">Se o retorno de chamada hello retorna false, Olá `exit` comentários será enviado.</span><span class="sxs-lookup"><span data-stu-id="2eb9b-158">If hello callback returns false, hello `exit` feedback will be send.</span></span> <span data-ttu-id="2eb9b-159">Caso contrário, ele será `action`.</span><span class="sxs-lookup"><span data-stu-id="2eb9b-159">Otherwise, it will be `action`.</span></span> <span data-ttu-id="2eb9b-160">Se nenhum retorno de chamada for definido para eventos de hello, Olá `drop` comentários retornará tooEngagement.</span><span class="sxs-lookup"><span data-stu-id="2eb9b-160">If no callback is set for hello events, hello `drop` feedback will be returned tooEngagement.</span></span>

> [!WARNING]
> <span data-ttu-id="2eb9b-161">Contrato não é capaz de tooreceive comentários de múltiplos para um envio de dados.</span><span class="sxs-lookup"><span data-stu-id="2eb9b-161">Engagement is not able tooreceive multiples feedbacks for a data push.</span></span> <span data-ttu-id="2eb9b-162">Se você planejar tooset vários manipuladores em um evento, lembre-se de que comentários Olá corresponderá toohello última aquela enviada.</span><span class="sxs-lookup"><span data-stu-id="2eb9b-162">If you plan tooset several handlers on an event, be aware that hello feedback will correspond toohello last one sent.</span></span> <span data-ttu-id="2eb9b-163">Nesse caso, é recomendável tooalways retorna Olá mesmo tooavoid valor ter confuso comentários em Olá front-end.</span><span class="sxs-lookup"><span data-stu-id="2eb9b-163">In this case, we recommend tooalways returns hello same value tooavoid having confusing feedback on hello front-end.</span></span>
> 
> 

## <a name="customize-ui-optional"></a><span data-ttu-id="2eb9b-164">Personalizar a interface do usuário (opcional)</span><span class="sxs-lookup"><span data-stu-id="2eb9b-164">Customize UI (optional)</span></span>
### <a name="first-step"></a><span data-ttu-id="2eb9b-165">Primeira etapa</span><span class="sxs-lookup"><span data-stu-id="2eb9b-165">First step</span></span>
<span data-ttu-id="2eb9b-166">Permitir que você alcance de saudação toocustomize da interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="2eb9b-166">We allow you toocustomize hello reach UI.</span></span>

<span data-ttu-id="2eb9b-167">toodo assim, você tem toocreate uma subclasse de saudação `EngagementReachHandler` classe.</span><span class="sxs-lookup"><span data-stu-id="2eb9b-167">toodo so, you have toocreate a subclass of hello `EngagementReachHandler` class.</span></span>

<span data-ttu-id="2eb9b-168">**Exemplo de código :**</span><span class="sxs-lookup"><span data-stu-id="2eb9b-168">**Sample Code :**</span></span>

            using Microsoft.Azure.Engagement;

            namespace Example
            {
              internal class ExampleReachHandler : EngagementReachHandler
              {
               // Override EngagementReachHandler methods depending on your needs
              }
            }

<span data-ttu-id="2eb9b-169">Em seguida, defina o conteúdo de saudação do hello `EngagementReach.Instance.Handler` campo com seu objeto personalizado no seu `App.xaml.cs` classe dentro Olá `App()` método.</span><span class="sxs-lookup"><span data-stu-id="2eb9b-169">Then, set hello content of hello `EngagementReach.Instance.Handler` field with your custom object in your `App.xaml.cs` class within hello `App()` method.</span></span>

<span data-ttu-id="2eb9b-170">**Exemplo de código :**</span><span class="sxs-lookup"><span data-stu-id="2eb9b-170">**Sample Code :**</span></span>

            protected override void OnLaunched(LaunchActivatedEventArgs args)
            {
              // your app initialization 
              EngagementReach.Instance.Handler = new ExampleReachHandler();
              // Engagement Agent and Reach initialization
            }

> [!NOTE]
> <span data-ttu-id="2eb9b-171">Por padrão, o Engagement usa a sua própria implementação de `EngagementReachHandler`.</span><span class="sxs-lookup"><span data-stu-id="2eb9b-171">By default, Engagement uses its own implementation of `EngagementReachHandler`.</span></span>
> <span data-ttu-id="2eb9b-172">Você não tem toocreate seus próprios, e se você fizer isso, você não tem toooverride cada método.</span><span class="sxs-lookup"><span data-stu-id="2eb9b-172">You don't have toocreate your own, and if you do so, you don't have toooverride every method.</span></span> <span data-ttu-id="2eb9b-173">comportamento padrão de saudação é o objeto base do contrato tooselect hello.</span><span class="sxs-lookup"><span data-stu-id="2eb9b-173">hello default behavior is tooselect hello Engagement base object.</span></span>
> 
> 

### <a name="web-view"></a><span data-ttu-id="2eb9b-174">Modo de exibição da Web</span><span class="sxs-lookup"><span data-stu-id="2eb9b-174">Web View</span></span>
<span data-ttu-id="2eb9b-175">Por padrão, o alcance usará recursos de saudação inserido de notificações de Olá Olá DLL toodisplay e páginas.</span><span class="sxs-lookup"><span data-stu-id="2eb9b-175">By default, Reach will use hello embedded resources of hello DLL toodisplay hello notifications and pages.</span></span>

<span data-ttu-id="2eb9b-176">tooprovide completa possibilidades de personalização só usamos o modo de exibição da web.</span><span class="sxs-lookup"><span data-stu-id="2eb9b-176">tooprovide a full customization possibilities we only use web view.</span></span> <span data-ttu-id="2eb9b-177">Se você quiser toocustomize layouts, diretamente substituir arquivos de recursos de saudação `EngagementAnnouncement.html` e `EngagementNotification.html`.</span><span class="sxs-lookup"><span data-stu-id="2eb9b-177">If you want toocustomize layouts, override directly hello resources files `EngagementAnnouncement.html` and `EngagementNotification.html`.</span></span> <span data-ttu-id="2eb9b-178">Todo o código precisa de contrato `<body></body>` toorun corretamente.</span><span class="sxs-lookup"><span data-stu-id="2eb9b-178">Engagement needs all code in `<body></body>` toorun correctly.</span></span> <span data-ttu-id="2eb9b-179">Mas você pode adicionar a marca externa `engagement_webview_area`.</span><span class="sxs-lookup"><span data-stu-id="2eb9b-179">But you can add tag outer `engagement_webview_area`.</span></span>

<span data-ttu-id="2eb9b-180">No entanto, você pode decidir toouse seus próprios recursos.</span><span class="sxs-lookup"><span data-stu-id="2eb9b-180">However, you can decide toouse your own resources.</span></span>

<span data-ttu-id="2eb9b-181">Você pode substituir `EngagementReachHandler` métodos em seu toouse de contrato subclasse tootell os layouts, mas levar mecanismo de contrato cuidado tooembedded hello:</span><span class="sxs-lookup"><span data-stu-id="2eb9b-181">You can override `EngagementReachHandler` methods in your subclass tootell Engagement toouse your layouts, but take care tooembedded hello engagement mechanism:</span></span>

<span data-ttu-id="2eb9b-182">**Exemplo de código :**</span><span class="sxs-lookup"><span data-stu-id="2eb9b-182">**Sample Code :**</span></span>

            // In your subclass of EngagementReachHandler

            public override string GetAnnouncementHTML()
            {
              return base.GetAnnouncementHTML();
            }
            public override string GetAnnouncementName()
            {
              return base.GetAnnouncementName();
            }
            public override string GetNotfificationHTML()
            {
              return base.GetNotfificationHTML();
            }
            public override string GetNotfificationName()
            {
              return base.GetNotfificationName();
            }


<span data-ttu-id="2eb9b-183">Por padrão, AnnouncementHTML é `ms-appx-web:///Resources/EngagementAnnouncement.html`.</span><span class="sxs-lookup"><span data-stu-id="2eb9b-183">By default, AnnouncementHTML is `ms-appx-web:///Resources/EngagementAnnouncement.html`.</span></span> <span data-ttu-id="2eb9b-184">Ele representa o arquivo html Olá que cria o conteúdo de saudação de uma mensagem de envio (anúncio de texto, anoucement Web e notificação de sondagem).</span><span class="sxs-lookup"><span data-stu-id="2eb9b-184">It represents hello html file that design hello content of a push message (Text announcement, Web anoucement and Poll announcement).</span></span> <span data-ttu-id="2eb9b-185">AnnouncementName é `engagement_announcement_content`.</span><span class="sxs-lookup"><span data-stu-id="2eb9b-185">AnnouncementName is `engagement_announcement_content`.</span></span> <span data-ttu-id="2eb9b-186">É nome de saudação do design do webview Olá em sua página xaml.</span><span class="sxs-lookup"><span data-stu-id="2eb9b-186">It is hello name of hello webview design in your xaml page.</span></span>

<span data-ttu-id="2eb9b-187">NotfificationHTML é `ms-appx-web:///Resources/EngagementNotification.html`.</span><span class="sxs-lookup"><span data-stu-id="2eb9b-187">NotfificationHTML is `ms-appx-web:///Resources/EngagementNotification.html`.</span></span> <span data-ttu-id="2eb9b-188">Ele representa o arquivo html Olá que cria a notificação de saudação de uma mensagem de envio.</span><span class="sxs-lookup"><span data-stu-id="2eb9b-188">It represents hello html file that design hello notification of a push message.</span></span> <span data-ttu-id="2eb9b-189">NotfificationName é `engagement_notification_content`.</span><span class="sxs-lookup"><span data-stu-id="2eb9b-189">NotfificationName is `engagement_notification_content`.</span></span> <span data-ttu-id="2eb9b-190">É nome de saudação do design do webview Olá em sua página xaml.</span><span class="sxs-lookup"><span data-stu-id="2eb9b-190">It is hello name of hello webview design in your xaml page.</span></span>

### <a name="customization"></a><span data-ttu-id="2eb9b-191">Personalização</span><span class="sxs-lookup"><span data-stu-id="2eb9b-191">Customization</span></span>
<span data-ttu-id="2eb9b-192">Você pode personalizar o modo de exibição da web de notificação e anúncio como desejar se você preservar o objeto Engagement.</span><span class="sxs-lookup"><span data-stu-id="2eb9b-192">You can customize notification and announcement web view has you want if you preserve Engagement object.</span></span> <span data-ttu-id="2eb9b-193">Lembre-se que objeto webview está descrito três vezes - Olá primeira vez em seu xaml, segundo de tempo em seu arquivo. cs no método de "setwebview()" hello e terceiro tempo no arquivo de html hello.</span><span class="sxs-lookup"><span data-stu-id="2eb9b-193">Take care that webview object is described three times - hello first time in your xaml, second time in your .cs file in hello "setwebview()" method, and third time in hello html file.</span></span>

* <span data-ttu-id="2eb9b-194">O xaml, você descreve Olá layout gráfico webview componente.</span><span class="sxs-lookup"><span data-stu-id="2eb9b-194">In your xaml you describe hello current graphical layout webview component.</span></span>
* <span data-ttu-id="2eb9b-195">No seu arquivo. cs, você pode definir "setwebview()", na qual você definir a dimensão de saudação do webview dois de saudação (notificação, comunicado).</span><span class="sxs-lookup"><span data-stu-id="2eb9b-195">In your .cs file you can define "setwebview()" in which you set hello dimension of hello two webview (notification, announcement).</span></span> <span data-ttu-id="2eb9b-196">É muito eficiente ao aplicativo hello é redimensionar.</span><span class="sxs-lookup"><span data-stu-id="2eb9b-196">It is very effective when hello application is resizing.</span></span>
* <span data-ttu-id="2eb9b-197">No arquivo de html do contrato de saudação é descrever Olá webview conteúdo, design e Olá posições de elementos entre si.</span><span class="sxs-lookup"><span data-stu-id="2eb9b-197">In hello Engagement html file we describe hello webview content, design and hello elements positions between each other.</span></span>

### <a name="launch-message"></a><span data-ttu-id="2eb9b-198">Iniciar mensagem</span><span class="sxs-lookup"><span data-stu-id="2eb9b-198">Launch message</span></span>
<span data-ttu-id="2eb9b-199">Quando um usuário clica em um sistema de notificação (uma notificação do sistema), contrato inicia o aplicativo hello, conteúdo de saudação do carregamento de saudação por push as mensagens e exibir página Olá campanha correspondente hello.</span><span class="sxs-lookup"><span data-stu-id="2eb9b-199">When a user clicks on a system notification (a toast), Engagement launches hello application, load hello content of hello push messages, and display hello page for hello corresponding campaign.</span></span>

<span data-ttu-id="2eb9b-200">Há um atraso entre a inicialização de saudação da exibição de aplicativo e Olá Olá da página de saudação (dependendo da velocidade da saudação da sua rede).</span><span class="sxs-lookup"><span data-stu-id="2eb9b-200">There is a delay between hello launch of hello application and hello display of hello page (depending on hello speed of your network).</span></span>

<span data-ttu-id="2eb9b-201">tooindicate toohello o usuário que algo está sendo carregado, você deve fornecer uma informações visuais, como uma barra de progresso ou um indicador de progresso.</span><span class="sxs-lookup"><span data-stu-id="2eb9b-201">tooindicate toohello user that something is loading, you should provide a visual information, like a progress bar or a progress indicator.</span></span> <span data-ttu-id="2eb9b-202">O Engagement não pode manipular isto por conta própria, mas oferece alguns manipuladores para você.</span><span class="sxs-lookup"><span data-stu-id="2eb9b-202">Engagement cannot handle that itself, but provides a few handlers for you.</span></span>

<span data-ttu-id="2eb9b-203">Adicionar tooimplement Olá retorno de chamada, em App.xaml.cs "App() pública {}":</span><span class="sxs-lookup"><span data-stu-id="2eb9b-203">tooimplement hello callback, in App.xaml.cs in "Public App(){}" add:</span></span>

            /* hello application has launched and hello content is loading.
             * You should display an indicator here.
             */
            EngagementReach.Instance.RetrieveLaunchMessageStarted += () => { [...] };

            /* hello application has finished loading hello content and hello page
             * is about toobe displayed.
             * You should hide hello indicator here.
             */
            EngagementReach.Instance.RetrieveLaunchMessageCompleted += () => { [...] };

            /* hello content has been loaded, but an error has occurred.
             * You can provide an information toohello user.
             * You should hide hello indicator here.
             */
            EngagementReach.Instance.RetrieveLaunchMessageFailed += () => { [...] };

<span data-ttu-id="2eb9b-204">Você pode definir o retorno de chamada de saudação no método "App() pública {}" de seu `App.xaml.cs` arquivos, preferencialmente antes Olá `EngagementReach.Instance.Init()` chamar.</span><span class="sxs-lookup"><span data-stu-id="2eb9b-204">You can set hello callback in your "Public App(){}" method of your `App.xaml.cs` file, preferably before hello `EngagementReach.Instance.Init()` call.</span></span>

> [!TIP]
> <span data-ttu-id="2eb9b-205">Cada manipulador é chamado pelo Olá Thread de interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="2eb9b-205">Each handler is called by hello UI Thread.</span></span> <span data-ttu-id="2eb9b-206">Você não tem tooworry ao usar uma MessageBox ou algo relacionados à interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="2eb9b-206">You do not have tooworry when using a MessageBox or something UI-related.</span></span>
> 
> 

## <span data-ttu-id="2eb9b-207"><a id="push-channel-sharing"></a> Enviar o compartilhamento de canal por push</span><span class="sxs-lookup"><span data-stu-id="2eb9b-207"><a id="push-channel-sharing"></a> Push channel sharing</span></span>
<span data-ttu-id="2eb9b-208">Se você estiver usando notificações por push para outra finalidade em seu aplicativo, em seguida, você tem canal de push Olá toouse recurso de saudação SDK de contrato de compartilhamento.</span><span class="sxs-lookup"><span data-stu-id="2eb9b-208">If you are using push notifications for another purpose in your application then you have toouse hello push channel sharing feature of hello Engagement SDK.</span></span> <span data-ttu-id="2eb9b-209">Isso é tooavoid perdido push.</span><span class="sxs-lookup"><span data-stu-id="2eb9b-209">This is tooavoid missed push.</span></span>

* <span data-ttu-id="2eb9b-210">Você pode fornecer seu próprio push canal toohello contrato alcançar a inicialização.</span><span class="sxs-lookup"><span data-stu-id="2eb9b-210">You can provide your own push channel toohello Engagement Reach initialization.</span></span> <span data-ttu-id="2eb9b-211">Olá SDK usará em vez de solicitar uma nova.</span><span class="sxs-lookup"><span data-stu-id="2eb9b-211">hello SDK will use it instead of requesting a new one.</span></span>

<span data-ttu-id="2eb9b-212">Olá contrato alcançar inicialização da atualização com o canal de envio no hello `InitEngagement` método da saudação `App.xaml.cs` arquivo:</span><span class="sxs-lookup"><span data-stu-id="2eb9b-212">Update hello Engagement Reach initialization with your push channel in hello `InitEngagement` method from hello `App.xaml.cs` file:</span></span>

    /* Your own push channel logic... */
    var pushChannel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    /*...Engagement initialization */
    EngagementAgent.Instance.Init(e);
    EngagementReach.Instance.Init(e,pushChannel);

* <span data-ttu-id="2eb9b-213">Como alternativa, se você quiser apenas tooconsume Olá por push canal após a inicialização de alcance hello, em seguida, você pode definir um retorno de chamada no canal de push Olá de tooget contrato alcançar depois que ela é criada pelo Olá SDK.</span><span class="sxs-lookup"><span data-stu-id="2eb9b-213">Alternatively, if you just want tooconsume hello push channel after hello Reach initialization then you can set a callback on Engagement Reach tooget hello push channel once it is created by hello SDK.</span></span>

<span data-ttu-id="2eb9b-214">Definir o retorno de chamada em qualquer lugar **depois** Olá inicialização alcance:</span><span class="sxs-lookup"><span data-stu-id="2eb9b-214">Set your callback at any place **after** hello Reach initialization :</span></span>

    /* Set action on hello SDK push channel. */
    EngagementReach.Instance.SetActionOnPushChannel((PushNotificationChannel channel) => 
    {
      /* hello forwarded channel can be null if its creation fails for any reason. */
      if (channel != null)
      {
        /* Your own push channel logic... */
      });
    }

## <a name="custom-scheme-tip"></a><span data-ttu-id="2eb9b-215">Dica de esquema personalizado</span><span class="sxs-lookup"><span data-stu-id="2eb9b-215">Custom scheme tip</span></span>
<span data-ttu-id="2eb9b-216">Fornecemos o uso de esquema personalizado.</span><span class="sxs-lookup"><span data-stu-id="2eb9b-216">We provide custom scheme use.</span></span> <span data-ttu-id="2eb9b-217">Você pode enviar um tipo diferente de URI do contrato toobe de front-end usado em seu aplicativo do compromisso.</span><span class="sxs-lookup"><span data-stu-id="2eb9b-217">You can send different type of URI from engagement frontend toobe used in your engagement application.</span></span> <span data-ttu-id="2eb9b-218">Um esquema padrão como o `http, ftp, ...` é gerenciados pelo Windows, uma janela será solicitada se não houver aplicativo padrão instalado no dispositivo.</span><span class="sxs-lookup"><span data-stu-id="2eb9b-218">Default scheme like `http, ftp, ...` are manage by Windows, a window will prompt if they are no default application installed on device.</span></span> <span data-ttu-id="2eb9b-219">Você também pode criar seu próprio esquema personalizado para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2eb9b-219">You can also create your own custom scheme for your application.</span></span>

<span data-ttu-id="2eb9b-220">tooset de maneira simples de saudação um esquema personalizado em seu aplicativo é tooopen seu `Package.appxmanifest` vá em `Declarations` painel.</span><span class="sxs-lookup"><span data-stu-id="2eb9b-220">hello simple way tooset a custom scheme in your application is tooopen your `Package.appxmanifest` go in `Declarations` panel.</span></span> <span data-ttu-id="2eb9b-221">Selecione `Protocol` no hello Available Declarations Role caixa e adicioná-lo.</span><span class="sxs-lookup"><span data-stu-id="2eb9b-221">Select `Protocol` in hello Available Declarations scroll box and add it.</span></span> <span data-ttu-id="2eb9b-222">Editar saudação `Name` nome de campo com o novo protocolo desejado.</span><span class="sxs-lookup"><span data-stu-id="2eb9b-222">Edit hello `Name` field with your new protocol desired name.</span></span>

<span data-ttu-id="2eb9b-223">Agora toouse esse protocolo, edite seu `App.xaml.cs` com hello `OnActivated` método e não se esqueça de contrato de tooinitialize aqui também:</span><span class="sxs-lookup"><span data-stu-id="2eb9b-223">Now toouse this protocol, edit your `App.xaml.cs` with hello `OnActivated` method, and don't forget tooinitialize engagement here also:</span></span>

            /// <summary>
            /// Enter point when app his called by another way than user click
            /// </summary>
            /// <param name="args">Activation args</param>
            protected override void OnActivated(IActivatedEventArgs args)
            {
              /* Init engagement like it was launch by a custom uri scheme */
              EngagementAgent.Instance.Init(args);
              EngagementReach.Instance.Init(args);

              //TODO design action toodo when app is launch

              #region Custom scheme use
              if (args.Kind == ActivationKind.Protocol)
              {
                ProtocolActivatedEventArgs myProtocol = (ProtocolActivatedEventArgs)args;

                if (myProtocol.Uri.Scheme.Equals("protocolName"))
                {
                  string path = myProtocol.Uri.AbsolutePath;
                }
              }
              #endregion

