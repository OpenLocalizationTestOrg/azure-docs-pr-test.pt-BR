---
title: "Integração do SDK do Reach do Windows Universal"
description: Como integrar o Azure Mobile Engagement Reach com aplicativos do Windows Universal
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
ms.openlocfilehash: 9311e998e67d8d0d56da68fc9460df32ce7ce5a9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="windows-universal-apps-reach-sdk-integration"></a><span data-ttu-id="d89bf-103">Integração do SDK do Reach do Windows Universal</span><span class="sxs-lookup"><span data-stu-id="d89bf-103">Windows Universal Apps Reach SDK Integration</span></span>
<span data-ttu-id="d89bf-104">Você deve seguir o procedimento de integração descrito na [Integração do SDK do Engagement do Windows Universal](mobile-engagement-windows-store-integrate-engagement.md) , antes de seguir este guia.</span><span class="sxs-lookup"><span data-stu-id="d89bf-104">You must follow the integration procedure described in the [Windows Universal Engagement SDK Integration](mobile-engagement-windows-store-integrate-engagement.md) before following this guide.</span></span>

## <a name="embed-the-engagement-reach-sdk-into-your-windows-universal-project"></a><span data-ttu-id="d89bf-105">Incorporação o SDK do Engagement Reach em seu projeto do Windows Universal</span><span class="sxs-lookup"><span data-stu-id="d89bf-105">Embed the Engagement Reach SDK into your Windows Universal project</span></span>
<span data-ttu-id="d89bf-106">Você não tem nada a adicionar.</span><span class="sxs-lookup"><span data-stu-id="d89bf-106">You do not have anything to add.</span></span> <span data-ttu-id="d89bf-107">`EngagementReach` já estão em seu projeto.</span><span class="sxs-lookup"><span data-stu-id="d89bf-107">`EngagementReach` references and resources are already in your project.</span></span>

> [!TIP]
> <span data-ttu-id="d89bf-108">Você pode personalizar imagens localizadas na pasta `Resources` do seu projeto, especialmente o ícone de marca (esse padrão para o ícone do Engagement).</span><span class="sxs-lookup"><span data-stu-id="d89bf-108">You can customize images located in the `Resources` folder of your project, especially the brand icon (that default to the Engagement icon).</span></span> <span data-ttu-id="d89bf-109">Em Aplicativos do Universal também é possível mover a pasta `Resources` em seu projeto compartilhado para compartilhar o seu conteúdo entre aplicativos, mas você precisa manter o arquivo `Resources\EngagementConfiguration.xml` em seu local padrão já que o mesmo é dependente da plataforma.</span><span class="sxs-lookup"><span data-stu-id="d89bf-109">On Universal Apps you can also move the `Resources` folder on your shared project to share its content between apps, but you will have to keep the `Resources\EngagementConfiguration.xml` file on its default location as it is platform dependent.</span></span>
> 
> 

## <a name="enable-the-windows-notification-service"></a><span data-ttu-id="d89bf-110">Habilitar o Serviço de Notificação do Windows</span><span class="sxs-lookup"><span data-stu-id="d89bf-110">Enable the Windows Notification Service</span></span>
### <a name="windows-8x-and-windows-phone-81-only"></a><span data-ttu-id="d89bf-111">Somente Windows 8.x e Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="d89bf-111">Windows 8.x and Windows Phone 8.1 only</span></span>
<span data-ttu-id="d89bf-112">Para usar o **Serviço de Notificação do Windows** (chamado de WNS) em seu arquivo `Package.appxmanifest` em `Application UI`, clique em `All Image Assets` na caixa bot à esquerda.</span><span class="sxs-lookup"><span data-stu-id="d89bf-112">In order to use the **Windows Notification Service** (referred as WNS) in your `Package.appxmanifest` file on `Application UI` click on `All Image Assets` in the left bot box.</span></span> <span data-ttu-id="d89bf-113">À direita da caixa do `Notifications`, alterar `toast capable` de `(not set)` para `(Yes)`.</span><span class="sxs-lookup"><span data-stu-id="d89bf-113">At the right of the box in `Notifications`, change `toast capable` from `(not set)` to `(Yes)`.</span></span>

### <a name="all-platforms"></a><span data-ttu-id="d89bf-114">Todas as plataformas</span><span class="sxs-lookup"><span data-stu-id="d89bf-114">All platforms</span></span>
<span data-ttu-id="d89bf-115">Você precisa sincronizar seu aplicativo com sua conta da Microsoft e com a plataforma de compromisso.</span><span class="sxs-lookup"><span data-stu-id="d89bf-115">You need to synchronize your app to your Microsoft account and to the engagement platform.</span></span> <span data-ttu-id="d89bf-116">Para isso, você precisa criar uma conta ou fazer logon no [centro de desenvolvimento do Windows](https://dev.windows.com).</span><span class="sxs-lookup"><span data-stu-id="d89bf-116">For this you need to create an account or log on [windows dev center](https://dev.windows.com).</span></span> <span data-ttu-id="d89bf-117">Depois que criar um novo aplicativo e localizar o SID e a chave secreta.</span><span class="sxs-lookup"><span data-stu-id="d89bf-117">After that create a new application and find the SID and secret key.</span></span> <span data-ttu-id="d89bf-118">No front-end do engagement vá para sua configuração de aplicativo em `native push` e cole suas credenciais.</span><span class="sxs-lookup"><span data-stu-id="d89bf-118">On the engagement frontend, go on your app setting in `native push` and paste your credentials.</span></span> <span data-ttu-id="d89bf-119">Depois disso, clique com botão direito no projeto, selecione `store` e `Associate App with the Store...`.</span><span class="sxs-lookup"><span data-stu-id="d89bf-119">After that, right click on your project, select `store` and `Associate App with the Store...`.</span></span> <span data-ttu-id="d89bf-120">Basta selecionar o aplicativo que você criou antes de sincronizá-la.</span><span class="sxs-lookup"><span data-stu-id="d89bf-120">You just need to select the application you have create before to synchronize it.</span></span>

## <a name="initialize-the-engagement-reach-sdk"></a><span data-ttu-id="d89bf-121">Inicializar o SDK do Engagement Reach</span><span class="sxs-lookup"><span data-stu-id="d89bf-121">Initialize the Engagement Reach SDK</span></span>
<span data-ttu-id="d89bf-122">Modifique o `App.xaml.cs`:</span><span class="sxs-lookup"><span data-stu-id="d89bf-122">Modify the `App.xaml.cs`:</span></span>

* <span data-ttu-id="d89bf-123">Insira `EngagementReach.Instance.Init` logo após `EngagementAgent.Instance.Init` no método `InitEngagement`:</span><span class="sxs-lookup"><span data-stu-id="d89bf-123">Insert `EngagementReach.Instance.Init` just after `EngagementAgent.Instance.Init` in your `InitEngagement` method:</span></span>
  
      private void InitEngagement(IActivatedEventArgs e)
      {
        EngagementAgent.Instance.Init(e);
        EngagementReach.Instance.Init(e);
      }
  
  <span data-ttu-id="d89bf-124">O `EngagementReach.Instance.Init` é executado em um thread dedicado.</span><span class="sxs-lookup"><span data-stu-id="d89bf-124">The `EngagementReach.Instance.Init` runs in a dedicated thread.</span></span> <span data-ttu-id="d89bf-125">Você não precisa fazê-lo.</span><span class="sxs-lookup"><span data-stu-id="d89bf-125">You do not have to do it yourself.</span></span>

> [!NOTE]
> <span data-ttu-id="d89bf-126">Se estiver usando notificações por push em outro lugar em seu aplicativo, você precisará [compartilhar seu canal push](#push-channel-sharing) com o Engagement Reach.</span><span class="sxs-lookup"><span data-stu-id="d89bf-126">If you are using push notifications elsewhere in your application then you have to [share your push channel](#push-channel-sharing) with Engagement Reach.</span></span>
> 
> 

## <a name="integration"></a><span data-ttu-id="d89bf-127">Integração</span><span class="sxs-lookup"><span data-stu-id="d89bf-127">Integration</span></span>
<span data-ttu-id="d89bf-128">O Engagement oferece duas maneiras de adicionar banners no aplicativo e exibições intersticiais do Reach para anúncios e pesquisas em seu aplicativo: a integração de sobreposição e a integração manual de exibições da Web.</span><span class="sxs-lookup"><span data-stu-id="d89bf-128">Engagement provides two ways to add the Reach in-app banners and interstitial views for announcements and polls in your application: the overlay integration and the web views manual integration.</span></span> <span data-ttu-id="d89bf-129">Não combine as duas abordagens na mesma página.</span><span class="sxs-lookup"><span data-stu-id="d89bf-129">You should not combine both approach on the same page.</span></span>

<span data-ttu-id="d89bf-130">A escolha entre as duas integrações pode ser resumida desta forma:</span><span class="sxs-lookup"><span data-stu-id="d89bf-130">The choice between the two integration could be summarized this way:</span></span>

* <span data-ttu-id="d89bf-131">Escolha a integração de sobreposição se suas páginas já herdam do Agente `EngagementPage`, é apenas uma questão de substituir `EngagementPage` por `EngagementPageOverlay` e `xmlns:engagement="using:Microsoft.Azure.Engagement"` por `xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"` nas páginas.</span><span class="sxs-lookup"><span data-stu-id="d89bf-131">You may choose the overlay integration if your pages already inherits from the Agent `EngagementPage`, it's just a matter of replacing `EngagementPage` by `EngagementPageOverlay` and `xmlns:engagement="using:Microsoft.Azure.Engagement"` by `xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"` in your pages.</span></span>
* <span data-ttu-id="d89bf-132">Escolha a integração manual de exibições da Web se quiser colocar precisamente a interface do usuário do Reach dentro de suas páginas ou se não quiser adicionar outro nível de herança às páginas.</span><span class="sxs-lookup"><span data-stu-id="d89bf-132">You may choose the web views manual integration if you want to precisely place the Reach UI within your pages or if you don't want to add another inheritance level to your pages.</span></span> 

### <a name="overlay-integration"></a><span data-ttu-id="d89bf-133">Integração de sobreposição</span><span class="sxs-lookup"><span data-stu-id="d89bf-133">Overlay integration</span></span>
<span data-ttu-id="d89bf-134">A sobreposição do Engagement adiciona dinamicamente os elementos de interface do usuário usados para exibir as campanhas do Reach em sua página.</span><span class="sxs-lookup"><span data-stu-id="d89bf-134">The Engagement overlay dynamically adds the UI elements used to display Reach campaigns in your page.</span></span> <span data-ttu-id="d89bf-135">Se a sobreposição não for adequada para seu layout, considere a integração manual de exibições da Web.</span><span class="sxs-lookup"><span data-stu-id="d89bf-135">If the overlay doesn't suit your layout you should consider the web views manual integration instead.</span></span>

<span data-ttu-id="d89bf-136">Em seu arquivo .xaml, altere a referência `EngagementPage` para `EngagementPageOverlay`</span><span class="sxs-lookup"><span data-stu-id="d89bf-136">In your .xaml file change `EngagementPage` reference to `EngagementPageOverlay`</span></span>

* <span data-ttu-id="d89bf-137">Adicione às suas declarações de namespaces:</span><span class="sxs-lookup"><span data-stu-id="d89bf-137">Add to your namespaces declarations:</span></span>
  
      xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"
* <span data-ttu-id="d89bf-138">Substituir `engagement:EngagementPage` por `engagement:EngagementPageOverlay`:</span><span class="sxs-lookup"><span data-stu-id="d89bf-138">Replace `engagement:EngagementPage` with `engagement:EngagementPageOverlay`:</span></span>

<span data-ttu-id="d89bf-139">**Com EngagementPage:**</span><span class="sxs-lookup"><span data-stu-id="d89bf-139">**With EngagementPage:**</span></span>

        <engagement:EngagementPage 
            xmlns:engagement="using:Microsoft.Azure.Engagement">

            <!-- Your layout -->
        </engagement:EngagementPage>

<span data-ttu-id="d89bf-140">**Com EngagementPageOverlay:**</span><span class="sxs-lookup"><span data-stu-id="d89bf-140">**With EngagementPageOverlay:**</span></span>

        <engagement:EngagementPageOverlay 
            xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay">

            <!-- Your layout -->
        </engagement:EngagementPageOverlay>

<span data-ttu-id="d89bf-141">No seu arquivo .cs, marque a página em `EngagementPageOverlay` em vez de `EngagementPage` e importe `Microsoft.Azure.Engagement.Overlay`.</span><span class="sxs-lookup"><span data-stu-id="d89bf-141">Then in your .cs file tag your page in `EngagementPageOverlay` instead of `EngagementPage` and import `Microsoft.Azure.Engagement.Overlay`.</span></span>

            using Microsoft.Azure.Engagement.Overlay;

* <span data-ttu-id="d89bf-142">Substituir `EngagementPage` por `EngagementPageOverlay`:</span><span class="sxs-lookup"><span data-stu-id="d89bf-142">Replace `EngagementPage` with `EngagementPageOverlay`:</span></span>

<span data-ttu-id="d89bf-143">**Com EngagementPage:**</span><span class="sxs-lookup"><span data-stu-id="d89bf-143">**With EngagementPage:**</span></span>

            using Microsoft.Azure.Engagement;

            namespace Example
            {
              public sealed partial class ExamplePage : EngagementPage
              {
                [...]
              }
            }

<span data-ttu-id="d89bf-144">**Com EngagementPageOverlay:**</span><span class="sxs-lookup"><span data-stu-id="d89bf-144">**With EngagementPageOverlay:**</span></span>

            using Microsoft.Azure.Engagement.Overlay;

            namespace Example
            {
              public sealed partial class ExamplePage : EngagementPageOverlay 
              {
                [...]
              }
            }


<span data-ttu-id="d89bf-145">A sobreposição do Engagement adiciona um elemento `Grid` sobre a página, composto de seu layout e dos dois elementos `WebView`, um para a faixa e outro para a exibição intersticial.</span><span class="sxs-lookup"><span data-stu-id="d89bf-145">The Engagement overlay adds a `Grid` element on top of your page composed of your layout and the two `WebView` elements one for the banner and the other one for the interstitial view.</span></span>

<span data-ttu-id="d89bf-146">Você pode personalizar os elementos da sobreposição diretamente no arquivo `EngagementPageOverlay.cs`.</span><span class="sxs-lookup"><span data-stu-id="d89bf-146">You can customize the overlay elements directly in the `EngagementPageOverlay.cs` file.</span></span>

### <a name="web-views-manual-integration"></a><span data-ttu-id="d89bf-147">Integração manual de exibições da Web</span><span class="sxs-lookup"><span data-stu-id="d89bf-147">Web views manual integration</span></span>
<span data-ttu-id="d89bf-148">O Reach pesquisará em suas páginas os dois elementos `WebView` responsáveis por exibir a faixa e a exibição intersticial.</span><span class="sxs-lookup"><span data-stu-id="d89bf-148">Reach will be searching your pages for the two `WebView` elements responsible for displaying the banner and the interstitial view.</span></span> <span data-ttu-id="d89bf-149">A única coisa que você precisa fazer é adicionar esses dois elementos `WebView` a algum lugar de suas páginas. Veja um exemplo:</span><span class="sxs-lookup"><span data-stu-id="d89bf-149">The only thing you have to do is to add those two `WebView` elements somewhere in your pages, here is an example:</span></span>

    <Grid x:Name="engagementGrid">

      <!-- Your layout -->

      <WebView x:Name="engagement_notification_content" Visibility="Collapsed" Height="80" HorizontalAlignment="Stretch" VerticalAlignment="Top"/>
      <WebView x:Name="engagement_announcement_content" Visibility="Collapsed"  HorizontalAlignment="Stretch"  VerticalAlignment="Stretch"/>
    </Grid>


<span data-ttu-id="d89bf-150">Neste exemplo, os elementos `WebView` são alongados para se ajustarem a seus contêineres, o que automaticamente os dimensiona novamente em caso de alteração de tamanho de janela ou rotação de tela.</span><span class="sxs-lookup"><span data-stu-id="d89bf-150">In this example the `WebView` elements are stretched to fit their container which automatically re-sizes them in case of screen rotation or window size change.</span></span>

> [!WARNING]
> <span data-ttu-id="d89bf-151">É importante manter a mesma nomenclatura `engagement_notification_content` e `engagement_announcement_content` para os elementos `WebView`.</span><span class="sxs-lookup"><span data-stu-id="d89bf-151">It is important to keep the same naming `engagement_notification_content` and `engagement_announcement_content` for the `WebView` elements.</span></span> <span data-ttu-id="d89bf-152">O Reach os identifica por seu nome.</span><span class="sxs-lookup"><span data-stu-id="d89bf-152">Reach is identifying them by their name.</span></span> 
> 
> 

## <a name="handle-datapush-optional"></a><span data-ttu-id="d89bf-153">Manipular o push de dados (opcional)</span><span class="sxs-lookup"><span data-stu-id="d89bf-153">Handle datapush (optional)</span></span>
<span data-ttu-id="d89bf-154">Se desejar que o aplicativo seja capaz de receber push de dados do Reach, você precisa implementar dois eventos da classe EngagementReach:</span><span class="sxs-lookup"><span data-stu-id="d89bf-154">If you want your application to be able to receive Reach data pushes, you have to implement two events of the EngagementReach class:</span></span>

<span data-ttu-id="d89bf-155">Em App.xaml.cs no construtor App(), adicione:</span><span class="sxs-lookup"><span data-stu-id="d89bf-155">In App.xaml.cs in the App() constructor add:</span></span>

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

<span data-ttu-id="d89bf-156">Você pode ver que o retorno de chamada de cada método retorna um valor booleano.</span><span class="sxs-lookup"><span data-stu-id="d89bf-156">You can see that the callback of each method returns a boolean.</span></span> <span data-ttu-id="d89bf-157">O Engagement envia um comentário ao seu back-end após distribuir o push de dados.</span><span class="sxs-lookup"><span data-stu-id="d89bf-157">Engagement sends a feedback to its back-end after dispatching the data push.</span></span> <span data-ttu-id="d89bf-158">Se o retorno de chamada retorna false, o comentário `exit` será enviado.</span><span class="sxs-lookup"><span data-stu-id="d89bf-158">If the callback returns false, the `exit` feedback will be send.</span></span> <span data-ttu-id="d89bf-159">Caso contrário, ele será `action`.</span><span class="sxs-lookup"><span data-stu-id="d89bf-159">Otherwise, it will be `action`.</span></span> <span data-ttu-id="d89bf-160">Se nenhum retorno de chamada for definido para os eventos, o comentário `drop` retornará ao Engagement.</span><span class="sxs-lookup"><span data-stu-id="d89bf-160">If no callback is set for the events, the `drop` feedback will be returned to Engagement.</span></span>

> [!WARNING]
> <span data-ttu-id="d89bf-161">O Engagement não é capaz de receber múltiplos comentários para um push de dados.</span><span class="sxs-lookup"><span data-stu-id="d89bf-161">Engagement is not able to receive multiples feedbacks for a data push.</span></span> <span data-ttu-id="d89bf-162">Se você pretende definir vários manipuladores em um evento, lembre-se de que os comentários corresponderá ao último enviado.</span><span class="sxs-lookup"><span data-stu-id="d89bf-162">If you plan to set several handlers on an event, be aware that the feedback will correspond to the last one sent.</span></span> <span data-ttu-id="d89bf-163">Nesse caso, é recomendável sempre retornar o mesmo valor para evitar que os comentários sejam confusos no front-end.</span><span class="sxs-lookup"><span data-stu-id="d89bf-163">In this case, we recommend to always returns the same value to avoid having confusing feedback on the front-end.</span></span>
> 
> 

## <a name="customize-ui-optional"></a><span data-ttu-id="d89bf-164">Personalizar a interface do usuário (opcional)</span><span class="sxs-lookup"><span data-stu-id="d89bf-164">Customize UI (optional)</span></span>
### <a name="first-step"></a><span data-ttu-id="d89bf-165">Primeira etapa</span><span class="sxs-lookup"><span data-stu-id="d89bf-165">First step</span></span>
<span data-ttu-id="d89bf-166">Permitir que você personalize a interface do usuário do reach.</span><span class="sxs-lookup"><span data-stu-id="d89bf-166">We allow you to customize the reach UI.</span></span>

<span data-ttu-id="d89bf-167">Para fazer isso, você precisa criar uma subclasse da classe `EngagementReachHandler` .</span><span class="sxs-lookup"><span data-stu-id="d89bf-167">To do so, you have to create a subclass of the `EngagementReachHandler` class.</span></span>

<span data-ttu-id="d89bf-168">**Exemplo de código :**</span><span class="sxs-lookup"><span data-stu-id="d89bf-168">**Sample Code :**</span></span>

            using Microsoft.Azure.Engagement;

            namespace Example
            {
              internal class ExampleReachHandler : EngagementReachHandler
              {
               // Override EngagementReachHandler methods depending on your needs
              }
            }

<span data-ttu-id="d89bf-169">Depois, defina o conteúdo do campo `EngagementReach.Instance.Handler` com seu objeto personalizado em sua classe `App.xaml.cs` dentro do método `App()`.</span><span class="sxs-lookup"><span data-stu-id="d89bf-169">Then, set the content of the `EngagementReach.Instance.Handler` field with your custom object in your `App.xaml.cs` class within the `App()` method.</span></span>

<span data-ttu-id="d89bf-170">**Exemplo de código :**</span><span class="sxs-lookup"><span data-stu-id="d89bf-170">**Sample Code :**</span></span>

            protected override void OnLaunched(LaunchActivatedEventArgs args)
            {
              // your app initialization 
              EngagementReach.Instance.Handler = new ExampleReachHandler();
              // Engagement Agent and Reach initialization
            }

> [!NOTE]
> <span data-ttu-id="d89bf-171">Por padrão, o Engagement usa a sua própria implementação de `EngagementReachHandler`.</span><span class="sxs-lookup"><span data-stu-id="d89bf-171">By default, Engagement uses its own implementation of `EngagementReachHandler`.</span></span>
> <span data-ttu-id="d89bf-172">Você não precisa criar sua própria e se você fizer isso, você não precisa substituir cada método.</span><span class="sxs-lookup"><span data-stu-id="d89bf-172">You don't have to create your own, and if you do so, you don't have to override every method.</span></span> <span data-ttu-id="d89bf-173">O comportamento padrão é selecionar o objeto base do Engagement.</span><span class="sxs-lookup"><span data-stu-id="d89bf-173">The default behavior is to select the Engagement base object.</span></span>
> 
> 

### <a name="web-view"></a><span data-ttu-id="d89bf-174">Modo de exibição da Web</span><span class="sxs-lookup"><span data-stu-id="d89bf-174">Web View</span></span>
<span data-ttu-id="d89bf-175">Por padrão, o Reach usará os recursos incorporados da DLL para exibir as notificações e páginas.</span><span class="sxs-lookup"><span data-stu-id="d89bf-175">By default, Reach will use the embedded resources of the DLL to display the notifications and pages.</span></span>

<span data-ttu-id="d89bf-176">Para fornecer possibilidades de personalização completa possibilidades usamos somente o modo de exibição da web.</span><span class="sxs-lookup"><span data-stu-id="d89bf-176">To provide a full customization possibilities we only use web view.</span></span> <span data-ttu-id="d89bf-177">Se você desejar personalizar layouts substitua diretamente os arquivos de recursos `EngagementAnnouncement.html` e `EngagementNotification.html`.</span><span class="sxs-lookup"><span data-stu-id="d89bf-177">If you want to customize layouts, override directly the resources files `EngagementAnnouncement.html` and `EngagementNotification.html`.</span></span> <span data-ttu-id="d89bf-178">O Engagement precisa de todos os códigos em `<body></body>` para executar corretamente.</span><span class="sxs-lookup"><span data-stu-id="d89bf-178">Engagement needs all code in `<body></body>` to run correctly.</span></span> <span data-ttu-id="d89bf-179">Mas você pode adicionar a marca externa `engagement_webview_area`.</span><span class="sxs-lookup"><span data-stu-id="d89bf-179">But you can add tag outer `engagement_webview_area`.</span></span>

<span data-ttu-id="d89bf-180">No entanto, você pode optar por usar seus próprios recursos.</span><span class="sxs-lookup"><span data-stu-id="d89bf-180">However, you can decide to use your own resources.</span></span>

<span data-ttu-id="d89bf-181">Você pode substituir os métodos `EngagementReachHandler` em sua subclasse para informar o Engagement para usar seus layouts, mas tome cuidado com o mecanismo incorporado do engagement:</span><span class="sxs-lookup"><span data-stu-id="d89bf-181">You can override `EngagementReachHandler` methods in your subclass to tell Engagement to use your layouts, but take care to embedded the engagement mechanism:</span></span>

<span data-ttu-id="d89bf-182">**Exemplo de código :**</span><span class="sxs-lookup"><span data-stu-id="d89bf-182">**Sample Code :**</span></span>

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


<span data-ttu-id="d89bf-183">Por padrão, AnnouncementHTML é `ms-appx-web:///Resources/EngagementAnnouncement.html`.</span><span class="sxs-lookup"><span data-stu-id="d89bf-183">By default, AnnouncementHTML is `ms-appx-web:///Resources/EngagementAnnouncement.html`.</span></span> <span data-ttu-id="d89bf-184">Representa o arquivo html que cria o conteúdo de uma mensagem de envio por push (anúncio de texto, anúncio da web e anúncio de pesquisa).</span><span class="sxs-lookup"><span data-stu-id="d89bf-184">It represents the html file that design the content of a push message (Text announcement, Web anoucement and Poll announcement).</span></span> <span data-ttu-id="d89bf-185">AnnouncementName é `engagement_announcement_content`.</span><span class="sxs-lookup"><span data-stu-id="d89bf-185">AnnouncementName is `engagement_announcement_content`.</span></span> <span data-ttu-id="d89bf-186">É o nome do design do modo de exibição da web em sua página xaml.</span><span class="sxs-lookup"><span data-stu-id="d89bf-186">It is the name of the webview design in your xaml page.</span></span>

<span data-ttu-id="d89bf-187">NotfificationHTML é `ms-appx-web:///Resources/EngagementNotification.html`.</span><span class="sxs-lookup"><span data-stu-id="d89bf-187">NotfificationHTML is `ms-appx-web:///Resources/EngagementNotification.html`.</span></span> <span data-ttu-id="d89bf-188">Representa o arquivo html que cria a notificação de uma mensagem de envio por push.</span><span class="sxs-lookup"><span data-stu-id="d89bf-188">It represents the html file that design the notification of a push message.</span></span> <span data-ttu-id="d89bf-189">NotfificationName é `engagement_notification_content`.</span><span class="sxs-lookup"><span data-stu-id="d89bf-189">NotfificationName is `engagement_notification_content`.</span></span> <span data-ttu-id="d89bf-190">É o nome do design do modo de exibição da web em sua página xaml.</span><span class="sxs-lookup"><span data-stu-id="d89bf-190">It is the name of the webview design in your xaml page.</span></span>

### <a name="customization"></a><span data-ttu-id="d89bf-191">Personalização</span><span class="sxs-lookup"><span data-stu-id="d89bf-191">Customization</span></span>
<span data-ttu-id="d89bf-192">Você pode personalizar o modo de exibição da web de notificação e anúncio como desejar se você preservar o objeto Engagement.</span><span class="sxs-lookup"><span data-stu-id="d89bf-192">You can customize notification and announcement web view has you want if you preserve Engagement object.</span></span> <span data-ttu-id="d89bf-193">Atenção, pois o objeto de exibição da web é descrito três vezes - a primeira vez no xaml, a segunda vez no arquivo .cs no método "setwebview()" e a terceira vez no arquivo html.</span><span class="sxs-lookup"><span data-stu-id="d89bf-193">Take care that webview object is described three times - the first time in your xaml, second time in your .cs file in the "setwebview()" method, and third time in the html file.</span></span>

* <span data-ttu-id="d89bf-194">Em seu xaml você descreve o componente do modo de exibição da web do layout gráfico atual.</span><span class="sxs-lookup"><span data-stu-id="d89bf-194">In your xaml you describe the current graphical layout webview component.</span></span>
* <span data-ttu-id="d89bf-195">Em seu arquivo .cs, você pode definir "setwebview()" no qual você define a dimensão dos dois modos de exibição da web (notificação, anúncio).</span><span class="sxs-lookup"><span data-stu-id="d89bf-195">In your .cs file you can define "setwebview()" in which you set the dimension of the two webview (notification, announcement).</span></span> <span data-ttu-id="d89bf-196">É muito eficiente quando o aplicativo é redimensionado.</span><span class="sxs-lookup"><span data-stu-id="d89bf-196">It is very effective when the application is resizing.</span></span>
* <span data-ttu-id="d89bf-197">No arquivo html do Engagement descrevemos o conteúdo do modo de exibição da web, o design e as posições dos elementos entre si.</span><span class="sxs-lookup"><span data-stu-id="d89bf-197">In the Engagement html file we describe the webview content, design and the elements positions between each other.</span></span>

### <a name="launch-message"></a><span data-ttu-id="d89bf-198">Iniciar mensagem</span><span class="sxs-lookup"><span data-stu-id="d89bf-198">Launch message</span></span>
<span data-ttu-id="d89bf-199">Quando um usuário clica em um sistema de notificação (um toast), o Engagement inicia o aplicativo, carrega o conteúdo das mensagens de envio por push e exibe a página da campanha correspondente.</span><span class="sxs-lookup"><span data-stu-id="d89bf-199">When a user clicks on a system notification (a toast), Engagement launches the application, load the content of the push messages, and display the page for the corresponding campaign.</span></span>

<span data-ttu-id="d89bf-200">Há um atraso entre a inicialização do aplicativo e a exibição da página (dependendo da velocidade da sua rede).</span><span class="sxs-lookup"><span data-stu-id="d89bf-200">There is a delay between the launch of the application and the display of the page (depending on the speed of your network).</span></span>

<span data-ttu-id="d89bf-201">Para indicar ao usuário que algo está sendo carregado, você deve fornecer informações visuais, como uma barra de progresso ou um indicador de progresso.</span><span class="sxs-lookup"><span data-stu-id="d89bf-201">To indicate to the user that something is loading, you should provide a visual information, like a progress bar or a progress indicator.</span></span> <span data-ttu-id="d89bf-202">O Engagement não pode manipular isto por conta própria, mas oferece alguns manipuladores para você.</span><span class="sxs-lookup"><span data-stu-id="d89bf-202">Engagement cannot handle that itself, but provides a few handlers for you.</span></span>

<span data-ttu-id="d89bf-203">Para implementar o retorno de chamada, em App.xaml.cs em "Public App(){}" adicione:</span><span class="sxs-lookup"><span data-stu-id="d89bf-203">To implement the callback, in App.xaml.cs in "Public App(){}" add:</span></span>

            /* The application has launched and the content is loading.
             * You should display an indicator here.
             */
            EngagementReach.Instance.RetrieveLaunchMessageStarted += () => { [...] };

            /* The application has finished loading the content and the page
             * is about to be displayed.
             * You should hide the indicator here.
             */
            EngagementReach.Instance.RetrieveLaunchMessageCompleted += () => { [...] };

            /* The content has been loaded, but an error has occurred.
             * You can provide an information to the user.
             * You should hide the indicator here.
             */
            EngagementReach.Instance.RetrieveLaunchMessageFailed += () => { [...] };

<span data-ttu-id="d89bf-204">Você pode definir o retorno de chamada em seu método "Public App() {}" de seu arquivo `App.xaml.cs`, de preferência antes da chamada `EngagementReach.Instance.Init()`.</span><span class="sxs-lookup"><span data-stu-id="d89bf-204">You can set the callback in your "Public App(){}" method of your `App.xaml.cs` file, preferably before the `EngagementReach.Instance.Init()` call.</span></span>

> [!TIP]
> <span data-ttu-id="d89bf-205">Cada manipulador é chamado pelo Thread de interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="d89bf-205">Each handler is called by the UI Thread.</span></span> <span data-ttu-id="d89bf-206">Você não precisa se preocupar ao usar uma MessageBox ou algo relacionado à interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="d89bf-206">You do not have to worry when using a MessageBox or something UI-related.</span></span>
> 
> 

## <span data-ttu-id="d89bf-207"><a id="push-channel-sharing"></a> Enviar o compartilhamento de canal por push</span><span class="sxs-lookup"><span data-stu-id="d89bf-207"><a id="push-channel-sharing"></a> Push channel sharing</span></span>
<span data-ttu-id="d89bf-208">Se estiver usando notificações por push para outra finalidade em seu aplicativo, você terá que usar o recurso de compartilhamento de canal de push do SDK do Engagement.</span><span class="sxs-lookup"><span data-stu-id="d89bf-208">If you are using push notifications for another purpose in your application then you have to use the push channel sharing feature of the Engagement SDK.</span></span> <span data-ttu-id="d89bf-209">Isso é para evitar notificações por push perdidas.</span><span class="sxs-lookup"><span data-stu-id="d89bf-209">This is to avoid missed push.</span></span>

* <span data-ttu-id="d89bf-210">Você pode oferecer seu próprio canal de push para inicializar o Engagement Reach.</span><span class="sxs-lookup"><span data-stu-id="d89bf-210">You can provide your own push channel to the Engagement Reach initialization.</span></span> <span data-ttu-id="d89bf-211">O SDK usará seu canal em vez de solicitar um novo.</span><span class="sxs-lookup"><span data-stu-id="d89bf-211">The SDK will use it instead of requesting a new one.</span></span>

<span data-ttu-id="d89bf-212">Atualize a inicialização do Engagement Reach com o canal de push no método `InitEngagement` começando pelo arquivo `App.xaml.cs`:</span><span class="sxs-lookup"><span data-stu-id="d89bf-212">Update the Engagement Reach initialization with your push channel in the `InitEngagement` method from the `App.xaml.cs` file:</span></span>

    /* Your own push channel logic... */
    var pushChannel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    /*...Engagement initialization */
    EngagementAgent.Instance.Init(e);
    EngagementReach.Instance.Init(e,pushChannel);

* <span data-ttu-id="d89bf-213">Como alternativa, se só quiser consumir o canal de push após a inicialização do Reach, você poderá configurar um retorno de chamada no Engagement Reach para obter o canal de push após ele ser criado pelo SDK.</span><span class="sxs-lookup"><span data-stu-id="d89bf-213">Alternatively, if you just want to consume the push channel after the Reach initialization then you can set a callback on Engagement Reach to get the push channel once it is created by the SDK.</span></span>

<span data-ttu-id="d89bf-214">Configure o retorno de chamada em qualquer lugar **após** a inicialização do Reach:</span><span class="sxs-lookup"><span data-stu-id="d89bf-214">Set your callback at any place **after** the Reach initialization :</span></span>

    /* Set action on the SDK push channel. */
    EngagementReach.Instance.SetActionOnPushChannel((PushNotificationChannel channel) => 
    {
      /* The forwarded channel can be null if its creation fails for any reason. */
      if (channel != null)
      {
        /* Your own push channel logic... */
      });
    }

## <a name="custom-scheme-tip"></a><span data-ttu-id="d89bf-215">Dica de esquema personalizado</span><span class="sxs-lookup"><span data-stu-id="d89bf-215">Custom scheme tip</span></span>
<span data-ttu-id="d89bf-216">Fornecemos o uso de esquema personalizado.</span><span class="sxs-lookup"><span data-stu-id="d89bf-216">We provide custom scheme use.</span></span> <span data-ttu-id="d89bf-217">Você pode enviar o tipo de URI diferente do front-end do Engagement para ser usado em seu aplicativo do engagement.</span><span class="sxs-lookup"><span data-stu-id="d89bf-217">You can send different type of URI from engagement frontend to be used in your engagement application.</span></span> <span data-ttu-id="d89bf-218">Um esquema padrão como o `http, ftp, ...` é gerenciados pelo Windows, uma janela será solicitada se não houver aplicativo padrão instalado no dispositivo.</span><span class="sxs-lookup"><span data-stu-id="d89bf-218">Default scheme like `http, ftp, ...` are manage by Windows, a window will prompt if they are no default application installed on device.</span></span> <span data-ttu-id="d89bf-219">Você também pode criar seu próprio esquema personalizado para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d89bf-219">You can also create your own custom scheme for your application.</span></span>

<span data-ttu-id="d89bf-220">A maneira simples de definir um esquema personalizado em seu aplicativo é abrir `Package.appxmanifest` no painel `Declarations`.</span><span class="sxs-lookup"><span data-stu-id="d89bf-220">The simple way to set a custom scheme in your application is to open your `Package.appxmanifest` go in `Declarations` panel.</span></span> <span data-ttu-id="d89bf-221">Selecione `Protocol` na caixa de rolagem de Declarações Disponíveis e adicione-o.</span><span class="sxs-lookup"><span data-stu-id="d89bf-221">Select `Protocol` in the Available Declarations scroll box and add it.</span></span> <span data-ttu-id="d89bf-222">Edite o campo `Name` com o novo nome de protocolo desejado.</span><span class="sxs-lookup"><span data-stu-id="d89bf-222">Edit the `Name` field with your new protocol desired name.</span></span>

<span data-ttu-id="d89bf-223">Agora, para usar esses protocolo edite seu `App.xaml.cs` método com o método `OnActivated` e não se esqueça de inicializar o engagement aqui também:</span><span class="sxs-lookup"><span data-stu-id="d89bf-223">Now to use this protocol, edit your `App.xaml.cs` with the `OnActivated` method, and don't forget to initialize engagement here also:</span></span>

            /// <summary>
            /// Enter point when app his called by another way than user click
            /// </summary>
            /// <param name="args">Activation args</param>
            protected override void OnActivated(IActivatedEventArgs args)
            {
              /* Init engagement like it was launch by a custom uri scheme */
              EngagementAgent.Instance.Init(args);
              EngagementReach.Instance.Init(args);

              //TODO design action to do when app is launch

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

