---
title: "aaaWindows Phone Silverlight alcançar SDK integração"
description: Como tooIntegrate do Azure Mobile Engagement atingir com aplicativos do Windows Phone Silverlight
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: d3516a6b-db9f-4cdb-a475-4148edf81af1
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: na
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 09c8767216e11963c5c600755ab8d4d11cd92034
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="windows-phone-silverlight-reach-sdk-integration"></a><span data-ttu-id="072e6-103">Integração do SDK do Windows Phone Silverlight para o Reach</span><span class="sxs-lookup"><span data-stu-id="072e6-103">Windows Phone Silverlight Reach SDK Integration</span></span>
<span data-ttu-id="072e6-104">Você deve seguir Olá integração procedimento descrito em Olá [integração do SDK do Windows Phone Silverlight contrato](mobile-engagement-windows-phone-integrate-engagement.md) antes de seguir este guia.</span><span class="sxs-lookup"><span data-stu-id="072e6-104">You must follow hello integration procedure described in hello [Windows Phone Silverlight Engagement SDK Integration](mobile-engagement-windows-phone-integrate-engagement.md) before following this guide.</span></span>

## <a name="embed-hello-engagement-reach-sdk-into-your-windows-phone-silverlight-project"></a><span data-ttu-id="072e6-105">Inserir saudação SDK do Reach contrato em seu projeto do Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="072e6-105">Embed hello Engagement Reach SDK into your Windows Phone Silverlight project</span></span>
<span data-ttu-id="072e6-106">Você não tem nada tooadd.</span><span class="sxs-lookup"><span data-stu-id="072e6-106">You do not have anything tooadd.</span></span> <span data-ttu-id="072e6-107">`EngagementReach` já estão em seu projeto.</span><span class="sxs-lookup"><span data-stu-id="072e6-107">`EngagementReach` references and resources are already in your project.</span></span>

> [!TIP]
> <span data-ttu-id="072e6-108">Você poderá personalizar as imagens localizadas em Olá `Resources` pasta do seu projeto, especialmente Olá marca ícone (esse padrão toohello contrato).</span><span class="sxs-lookup"><span data-stu-id="072e6-108">You can customize images located in hello `Resources` folder of your project, especially hello brand icon (that default toohello Engagement icon).</span></span>
> 
> 

## <a name="add-hello-capabilities"></a><span data-ttu-id="072e6-109">Adicionar recursos de saudação</span><span class="sxs-lookup"><span data-stu-id="072e6-109">Add hello capabilities</span></span>
<span data-ttu-id="072e6-110">Olá SDK do Reach contrato precisa de alguns recursos adicionais.</span><span class="sxs-lookup"><span data-stu-id="072e6-110">hello Engagement Reach SDK needs some additional capabilities.</span></span>

<span data-ttu-id="072e6-111">Abra sua `WMAppManifest.xml` de arquivo e certifique-se de que Olá recursos a seguir são declarados:</span><span class="sxs-lookup"><span data-stu-id="072e6-111">Open your `WMAppManifest.xml` file and be sure that hello following capabilities are declared:</span></span>

* `ID_CAP_PUSH_NOTIFICATION`
* `ID_CAP_WEBBROWSERCOMPONENT`

<span data-ttu-id="072e6-112">Olá primeiro um é usado pela exibição de saudação de tooallow Olá MPNS serviço de notificação do sistema.</span><span class="sxs-lookup"><span data-stu-id="072e6-112">hello first one is used by hello MPNS service tooallow hello display of toast notification.</span></span> <span data-ttu-id="072e6-113">Olá, um segundo é usado tooembed uma tarefa de navegador em Olá SDK.</span><span class="sxs-lookup"><span data-stu-id="072e6-113">hello second one is used tooembed a browser task into hello SDK.</span></span>

<span data-ttu-id="072e6-114">Editar saudação `WMAppManifest.xml` de arquivos e adicionar dentro Olá `<Capabilities />` marca:</span><span class="sxs-lookup"><span data-stu-id="072e6-114">Edit hello `WMAppManifest.xml` file and add inside hello `<Capabilities />` tag :</span></span>

    <Capability Name="ID_CAP_PUSH_NOTIFICATION" />
    <Capability Name="ID_CAP_WEBBROWSERCOMPONENT" />

## <a name="enable-hello-microsoft-push-notification-service"></a><span data-ttu-id="072e6-115">Habilitar Olá Microsoft Push Notification Service</span><span class="sxs-lookup"><span data-stu-id="072e6-115">Enable hello Microsoft Push Notification Service</span></span>
<span data-ttu-id="072e6-116">Na saudação de toouse ordem **Microsoft Push Notification Service** (conhecido como MPNS) seu `WMAppManifest.xml` arquivo deve ter uma `<App />` marca com um `Publisher` atributo definido toohello nome do seu projeto.</span><span class="sxs-lookup"><span data-stu-id="072e6-116">In order toouse hello **Microsoft Push Notification Service** (referred as MPNS) your `WMAppManifest.xml` file must have an `<App />` tag with a `Publisher` attribute set toohello name of your project.</span></span>

## <a name="initialize-hello-engagement-reach-sdk"></a><span data-ttu-id="072e6-117">Inicializar Olá contrato SDK do Reach</span><span class="sxs-lookup"><span data-stu-id="072e6-117">Initialize hello Engagement Reach SDK</span></span>
### <a name="engagement-configuration"></a><span data-ttu-id="072e6-118">Configuração do Engagement</span><span class="sxs-lookup"><span data-stu-id="072e6-118">Engagement configuration</span></span>
<span data-ttu-id="072e6-119">configuração do contrato de saudação é centralizada em Olá `Resources\EngagementConfiguration.xml` arquivo do projeto.</span><span class="sxs-lookup"><span data-stu-id="072e6-119">hello Engagement configuration is centralized in hello `Resources\EngagementConfiguration.xml` file of your project.</span></span>

<span data-ttu-id="072e6-120">Edite essa configuração do arquivo toospecify alcance:</span><span class="sxs-lookup"><span data-stu-id="072e6-120">Edit this file toospecify reach configuration :</span></span>

* <span data-ttu-id="072e6-121">*Opcional*, indique se o push nativo da saudação (MPNS) está ativado ou não entre `<enableNativePush>` e `</enableNativePush>` marcas, (`true` por padrão).</span><span class="sxs-lookup"><span data-stu-id="072e6-121">*Optional*, indicate whether hello native push (MPNS) is activated or not between `<enableNativePush>` and `</enableNativePush>` tags, (`true` by default).</span></span>
* <span data-ttu-id="072e6-122">*Opcional*, indicar o nome de saudação do canal de envio de saudação entre `<channelName>` e `</channelName>` marcas, forneça Olá mesmo que seu aplicativo pode usar ou deixe-o vazio no momento.</span><span class="sxs-lookup"><span data-stu-id="072e6-122">*Optional*, indicate hello name of hello push channel between `<channelName>` and `</channelName>` tags, provide hello same that your application may currently use or leave it empty.</span></span>

<span data-ttu-id="072e6-123">Se você quiser toospecify em tempo de execução em vez disso, você pode chamar a seguir Olá método antes da inicialização de agente do hello contrato:</span><span class="sxs-lookup"><span data-stu-id="072e6-123">If you want toospecify it at runtime instead, you can call hello following method before hello Engagement agent initialization :</span></span>

    /* Engagement configuration. */
    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();

    engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

    engagementConfiguration.Reach.EnableNativePush = true;                  
    /* [Optional] whether hello native push (MPNS) is activated or not. */

    engagementConfiguration.Reach.ChannelName = "YOUR_PUSH_CHANNEL_NAME";   
    /* [Optional] Provide hello same channel name that your application may currently use. */

    /* Initialize Engagement agent with above configuration. */
    EngagementAgent.Instance.Init(engagementConfiguration);

> [!TIP]
> <span data-ttu-id="072e6-124">Você pode especificar o nome de saudação do canal de push MPNS saudação do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="072e6-124">You can specify hello name of hello MPNS push channel of your application.</span></span> <span data-ttu-id="072e6-125">Por padrão, o contrato cria um nome com base no appId hello.</span><span class="sxs-lookup"><span data-stu-id="072e6-125">By default, Engagement creates a name based on hello appId.</span></span> <span data-ttu-id="072e6-126">Você não têm necessidade toospecify Olá nome por conta própria, exceto se você estiver planejando canal de push Olá toouse fora do contrato.</span><span class="sxs-lookup"><span data-stu-id="072e6-126">You have no need toospecify hello name yourself, except if you plan toouse hello push channel outside of Engagement.</span></span>
> 
> 

### <a name="engagement-initialization"></a><span data-ttu-id="072e6-127">Inicialização do Engagement</span><span class="sxs-lookup"><span data-stu-id="072e6-127">Engagement initialization</span></span>
<span data-ttu-id="072e6-128">Modificar Olá `App.xaml.cs`:</span><span class="sxs-lookup"><span data-stu-id="072e6-128">Modify hello `App.xaml.cs`:</span></span>

* <span data-ttu-id="072e6-129">Adicionar tooyour `using` instruções:</span><span class="sxs-lookup"><span data-stu-id="072e6-129">Add tooyour `using` statements :</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="072e6-130">Insira `EngagementReach.Instance.Init` logo após `EngagementAgent.Instance.Init` e `Application_Launching` :</span><span class="sxs-lookup"><span data-stu-id="072e6-130">Insert `EngagementReach.Instance.Init` just after `EngagementAgent.Instance.Init` in `Application_Launching` :</span></span>
  
      private void Application_Launching(object sender, LaunchingEventArgs e)
      {
         EngagementAgent.Instance.Init();
         EngagementReach.Instance.Init();
      }
* <span data-ttu-id="072e6-131">Inserir `EngagementReach.Instance.OnActivated` em Olá `Application_Activated` método:</span><span class="sxs-lookup"><span data-stu-id="072e6-131">Insert `EngagementReach.Instance.OnActivated` in hello `Application_Activated` method :</span></span>
  
      private void Application_Activated(object sender, ActivatedEventArgs e)
      {
         EngagementAgent.Instance.OnActivated(e);
         EngagementReach.Instance.OnActivated(e);
      }

> [!IMPORTANT]
> <span data-ttu-id="072e6-132">Olá `EngagementReach.Instance.Init` é executado em um thread dedicado.</span><span class="sxs-lookup"><span data-stu-id="072e6-132">hello `EngagementReach.Instance.Init` runs in a dedicated thread.</span></span> <span data-ttu-id="072e6-133">Você não tem toodo-lo por conta própria.</span><span class="sxs-lookup"><span data-stu-id="072e6-133">You do not have toodo it yourself.</span></span>
> 
> 

## <a name="app-store-submission-considerations"></a><span data-ttu-id="072e6-134">Considerações de envio de armazenamento de aplicativo</span><span class="sxs-lookup"><span data-stu-id="072e6-134">App store submission considerations</span></span>
<span data-ttu-id="072e6-135">Microsoft impõe algumas regras ao usar notificações por push de saudação:</span><span class="sxs-lookup"><span data-stu-id="072e6-135">Microsoft imposes some rules when using hello push notifications:</span></span>

<span data-ttu-id="072e6-136">De saudação Microsoft [políticas de aplicativo] documentação, seção 2.9:</span><span class="sxs-lookup"><span data-stu-id="072e6-136">From hello Microsoft [Application Policies] documentation, section 2.9:</span></span>

1) <span data-ttu-id="072e6-137">Você deve pedir notificações por push do hello usuário tooaccept tooreceive.</span><span class="sxs-lookup"><span data-stu-id="072e6-137">You must ask hello user tooaccept tooreceive push notifications.</span></span> <span data-ttu-id="072e6-138">Em seguida, em suas configurações, adicione notificações de push uma maneira toodisable hello.</span><span class="sxs-lookup"><span data-stu-id="072e6-138">Then, in your settings, add a way toodisable hello push notifications.</span></span>

<span data-ttu-id="072e6-139">Olá EngagementReach fornece dois métodos toomanage Olá aceitar-em/Recusar, `EnableNativePush()` e `DisableNativePush()`.</span><span class="sxs-lookup"><span data-stu-id="072e6-139">hello EngagementReach object provides two methods toomanage hello opt-in/opt-out, `EnableNativePush()` and `DisableNativePush()`.</span></span> <span data-ttu-id="072e6-140">Por exemplo, pode criar uma opção nas configurações de saudação com uma alternância toodisable ou habilitar MPNS.</span><span class="sxs-lookup"><span data-stu-id="072e6-140">You could, for example, create an option in hello settings with a toggle toodisable or enable MPNS.</span></span>

<span data-ttu-id="072e6-141">Você também pode decidir toodeactivate MPNS por meio da configuração de contrato Olá\<windows phone-sdk-alcance-configuração\>.</span><span class="sxs-lookup"><span data-stu-id="072e6-141">You can also decide toodeactivate MPNS through hello Engagement configuration\<windows-phone-sdk-reach-configuration\>.</span></span>

> <span data-ttu-id="072e6-142">2.9.1) aplicativo hello primeiro deve descrever Olá notificações toobe fornecido e **obter permissão expressa e do usuário da saudação (opt-in)**, e **deve fornecer um mecanismo pelo qual Olá usuário pode recusar recebimento notificações por push**.</span><span class="sxs-lookup"><span data-stu-id="072e6-142">2.9.1) hello application must first describe hello notifications toobe provided and **obtain hello user’s express permission (opt-in)**, and **must provide a mechanism through which hello user can opt out of receiving push notifications**.</span></span> <span data-ttu-id="072e6-143">Todas as notificações fornecidas usando Olá Microsoft Push Notification Service deve ser consistentes com hello descrição fornecida toohello usuário e deve estar em conformidade com todos os aplicável [políticas de aplicativo] [ Content Policies]e [requisitos adicionais para tipos específicos de aplicativo].</span><span class="sxs-lookup"><span data-stu-id="072e6-143">All notifications provided using hello Microsoft Push Notification Service must be consistent with hello description provided toohello user and must comply with all applicable [Application Policies][Content Policies] and [Additional Requirements for Specific Application Types].</span></span>
> 
> 

2) <span data-ttu-id="072e6-144">Você não deve usar muitas notificações por push.</span><span class="sxs-lookup"><span data-stu-id="072e6-144">You should not use too many push notifications.</span></span> <span data-ttu-id="072e6-145">O Engagement manipulará notificações para você.</span><span class="sxs-lookup"><span data-stu-id="072e6-145">Engagement will handle notifications for you.</span></span>

> <span data-ttu-id="072e6-146">2.9.2) aplicativo hello e seu uso da saudação Microsoft Push Notification Service não excessivamente use capacidade de rede ou de largura de banda de saudação Microsoft Push Notification Service, ou caso contrário indevidamente sobrecarregam um Windows Phone ou outro dispositivo da Microsoft ou o serviço com excessiva por push de notificações, conforme determinado pela Microsoft a seu critério e não deve danificar ou interferir com redes Microsoft ou servidores ou servidores de terceiros ou redes conectadas toohello Microsoft Push Notification Service.</span><span class="sxs-lookup"><span data-stu-id="072e6-146">2.9.2) hello application and its use of hello Microsoft Push Notification Service must not excessively use network capacity or bandwidth of hello Microsoft Push Notification Service, or otherwise unduly burden a Windows Phone or other Microsoft device or service with excessive push notifications, as determined by Microsoft in its reasonable discretion, and must not harm or interfere with any Microsoft networks or servers or any third party servers or networks connected toohello Microsoft Push Notification Service.</span></span>
> 
> 

3) <span data-ttu-id="072e6-147">Não confie em informações de criticals toosend MPNS.</span><span class="sxs-lookup"><span data-stu-id="072e6-147">Do not rely on MPNS toosend criticals information.</span></span> <span data-ttu-id="072e6-148">Contrato usa MPNS, portanto, esta regra também se aplica para campanhas Olá criadas dentro de saudação contrato front-end.</span><span class="sxs-lookup"><span data-stu-id="072e6-148">Engagement uses MPNS, so this rule also applies for hello campaigns created inside hello Engagement front-end.</span></span>

> <span data-ttu-id="072e6-149">2.9.3) Olá Microsoft Push Notification Service não pode ser usado toosend notificações que são de missão crítica ou não poderia afetar assuntos de vida ou morte, incluindo, sem dispositivo médico da limitação notificações críticas tooa relacionados ou condição.</span><span class="sxs-lookup"><span data-stu-id="072e6-149">2.9.3) hello Microsoft Push Notification Service may not be used toosend notifications that are mission critical or otherwise could affect matters of life or death, including without limitation critical notifications related tooa medical device or condition.</span></span> <span data-ttu-id="072e6-150">MICROSOFT expressamente se isenta de qualquer garantia que Olá uso de hello MICROSOFT PUSH notificação serviço ou entrega de MICROSOFT PUSH notificação serviço notificações serão ser ININTERRUPTAS, livre de erro, ou caso contrário garantido tooOCCUR ON A real-time base.</span><span class="sxs-lookup"><span data-stu-id="072e6-150">MICROSOFT EXPRESSLY DISCLAIMS ANY WARRANTIES THAT hello USE OF hello MICROSOFT PUSH NOTIFICATION SERVICE OR DELIVERY OF MICROSOFT PUSH NOTIFICATION SERVICE NOTIFICATIONS WILL BE UNINTERRUPTED, ERROR FREE, OR OTHERWISE GUARANTEED tooOCCUR ON A REAL-TIME BASIS.</span></span>
> 
> 

<span data-ttu-id="072e6-151">**Não podemos garantir que seu aplicativo passará o processo de validação Olá se você não respeitam essas recomendações.**</span><span class="sxs-lookup"><span data-stu-id="072e6-151">**We cannot guarantee that your application will pass hello validation process if you do not respect these recommendations.**</span></span>

## <a name="handle-data-push-optional"></a><span data-ttu-id="072e6-152">Manipular o push de dados (opcional)</span><span class="sxs-lookup"><span data-stu-id="072e6-152">Handle data push (optional)</span></span>
<span data-ttu-id="072e6-153">Se você quiser envios por push os aplicativo toobe tooreceive capaz de alcançar dados, você tem tooimplement dois eventos de saudação EngagementReach classe:</span><span class="sxs-lookup"><span data-stu-id="072e6-153">If you want your application toobe able tooreceive Reach data pushes, you have tooimplement two events of hello EngagementReach class:</span></span>

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

<span data-ttu-id="072e6-154">Você pode ver o retorno de chamada saudação de cada método retorna um valor booleano.</span><span class="sxs-lookup"><span data-stu-id="072e6-154">You can see that hello callback of each method returns a boolean.</span></span> <span data-ttu-id="072e6-155">Contrato envia um feedback tooits back-end após distribuir dados por push-Olá.</span><span class="sxs-lookup"><span data-stu-id="072e6-155">Engagement sends a feedback tooits back-end after dispatching hello data push.</span></span> <span data-ttu-id="072e6-156">Se o retorno de chamada hello retorna false, Olá `exit` comentários será enviado.</span><span class="sxs-lookup"><span data-stu-id="072e6-156">If hello callback returns false, hello `exit` feedback will be send.</span></span> <span data-ttu-id="072e6-157">Caso contrário, ele será `action`.</span><span class="sxs-lookup"><span data-stu-id="072e6-157">Otherwise, it will be `action`.</span></span> <span data-ttu-id="072e6-158">Se nenhum retorno de chamada for definido para eventos de hello, Olá `drop` comentários retornará tooEngagement.</span><span class="sxs-lookup"><span data-stu-id="072e6-158">If no callback is set for hello events, hello `drop` feedback will be returned tooEngagement.</span></span>

> [!WARNING]
> <span data-ttu-id="072e6-159">Contrato não é capaz de tooreceive comentários de múltiplos para um envio de dados.</span><span class="sxs-lookup"><span data-stu-id="072e6-159">Engagement is not able tooreceive multiples feedbacks for a data push.</span></span> <span data-ttu-id="072e6-160">Se você planejar tooset vários manipuladores em um evento, lembre-se de que comentários Olá corresponderá toohello última aquela enviada.</span><span class="sxs-lookup"><span data-stu-id="072e6-160">If you plan tooset several handlers on an event, be aware that hello feedback will correspond toohello last one sent.</span></span> <span data-ttu-id="072e6-161">Nesse caso, é recomendável tooalways retorna Olá mesmo tooavoid valor ter confuso comentários em Olá front-end.</span><span class="sxs-lookup"><span data-stu-id="072e6-161">In this case, we recommend tooalways returns hello same value tooavoid having confusing feedback on hello front-end.</span></span>
> 
> 

## <a name="customize-ui-optional"></a><span data-ttu-id="072e6-162">Personalizar a interface do usuário (opcional)</span><span class="sxs-lookup"><span data-stu-id="072e6-162">Customize UI (optional)</span></span>
### <a name="first-step"></a><span data-ttu-id="072e6-163">Primeira etapa</span><span class="sxs-lookup"><span data-stu-id="072e6-163">First step</span></span>
<span data-ttu-id="072e6-164">Permitir que você alcance de saudação toocustomize da interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="072e6-164">We allow you toocustomize hello reach UI.</span></span>

<span data-ttu-id="072e6-165">toodo assim, você tem toocreate uma subclasse de saudação `EngagementReachHandler` classe.</span><span class="sxs-lookup"><span data-stu-id="072e6-165">toodo so, you have toocreate a subclass of hello `EngagementReachHandler` class.</span></span>

<span data-ttu-id="072e6-166">**Exemplo de código :**</span><span class="sxs-lookup"><span data-stu-id="072e6-166">**Sample Code :**</span></span>

    using Microsoft.Azure.Engagement;

    namespace Example
    {
       internal class ExampleReachHandler : EngagementReachHandler
       {
          // Override EngagementReachHandler methods depending on your needs
       }
    }

<span data-ttu-id="072e6-167">Em seguida, defina o conteúdo de saudação do hello `EngagementReach.Instance.Handler` campo com seu objeto personalizado no seu `App.xaml.cs` classe dentro Olá `Application_Launching` método.</span><span class="sxs-lookup"><span data-stu-id="072e6-167">Then, set hello content of hello `EngagementReach.Instance.Handler` field with your custom object in your `App.xaml.cs` class within hello `Application_Launching` method.</span></span>

<span data-ttu-id="072e6-168">**Exemplo de código :**</span><span class="sxs-lookup"><span data-stu-id="072e6-168">**Sample Code :**</span></span>

    private void Application_Launching(object sender, LaunchingEventArgs e)
    {
       // your app initialization 
       EngagementReach.Instance.Handler = new ExampleReachHandler();
       // Engagement Agent and Reach initialization
    }

> [!NOTE]
> <span data-ttu-id="072e6-169">Por padrão, o Engagement usa a sua própria implementação de `EngagementReachHandler`.</span><span class="sxs-lookup"><span data-stu-id="072e6-169">By default, Engagement uses its own implementation of `EngagementReachHandler`.</span></span> <span data-ttu-id="072e6-170">Você não tem toocreate seus próprios, e se você fizer isso, você não tem toooverride cada método.</span><span class="sxs-lookup"><span data-stu-id="072e6-170">You don't have toocreate your own, and if you do so, you don't have toooverride every method.</span></span> <span data-ttu-id="072e6-171">comportamento padrão de saudação é o objeto base do contrato tooselect hello.</span><span class="sxs-lookup"><span data-stu-id="072e6-171">hello default behavior is tooselect hello Engagement base object.</span></span>
> 
> 

### <a name="layouts"></a><span data-ttu-id="072e6-172">Layouts</span><span class="sxs-lookup"><span data-stu-id="072e6-172">Layouts</span></span>
<span data-ttu-id="072e6-173">Por padrão, o alcance usará recursos de saudação inserido de notificações de Olá Olá DLL toodisplay e páginas.</span><span class="sxs-lookup"><span data-stu-id="072e6-173">By default, Reach will use hello embedded resources of hello DLL toodisplay hello notifications and pages.</span></span>

<span data-ttu-id="072e6-174">No entanto, você pode decidir toouse tooreflect seus próprios recursos sua marca nesses componentes.</span><span class="sxs-lookup"><span data-stu-id="072e6-174">However, you can decide toouse your own resources tooreflect your brand in these components.</span></span>

<span data-ttu-id="072e6-175">Você pode substituir `EngagementReachHandler` métodos no seu toouse de contrato subclasse tootell seus layouts:</span><span class="sxs-lookup"><span data-stu-id="072e6-175">You can override `EngagementReachHandler` methods in your subclass tootell Engagement toouse your layouts :</span></span>

<span data-ttu-id="072e6-176">**Exemplo de código :**</span><span class="sxs-lookup"><span data-stu-id="072e6-176">**Sample Code :**</span></span>

    // In your subclass of EngagementReachHandler

    public override string GetTextViewAnnouncementUri()
    {
       // return hello path of your own xaml
    }

    public override string GetWebViewAnnouncementUri()
    {
       // return hello path of your own xaml
    }

    public override string GetPollUri()
    {
       // return hello path of your own xaml
    }

    public override EngagementNotificationView CreateNotification(EngagementNotificationViewModel viewModel)
    {
       // return a new instance of your own notification
    }

> [!TIP]
> <span data-ttu-id="072e6-177">Olá `CreateNotification` método pode retornar nulo.</span><span class="sxs-lookup"><span data-stu-id="072e6-177">hello `CreateNotification` method can return null.</span></span> <span data-ttu-id="072e6-178">notificação de saudação não será exibida e campanha de alcance hello será descartada.</span><span class="sxs-lookup"><span data-stu-id="072e6-178">hello notification won't be displayed and hello reach campaign will be dropped.</span></span>
> 
> 

<span data-ttu-id="072e6-179">toosimplify sua implementação de layout, nós também fornecemos nossa própria xaml que pode servir como base para seu código.</span><span class="sxs-lookup"><span data-stu-id="072e6-179">toosimplify your layout implementation, we also provide our own xaml which can serve as a basis for your code.</span></span> <span data-ttu-id="072e6-180">Eles estão localizados no arquivo de projeto SDK hello (/ src alcance /).</span><span class="sxs-lookup"><span data-stu-id="072e6-180">They are located in hello Engagement SDK archive (/src/reach/).</span></span>

> [!WARNING]
> <span data-ttu-id="072e6-181">fontes de saudação que fornecemos são Olá exata que mesmo que usamos.</span><span class="sxs-lookup"><span data-stu-id="072e6-181">hello sources that we provide are hello exact same ones that we use.</span></span> <span data-ttu-id="072e6-182">Portanto toomodify-los diretamente, não esqueça toochange Olá namespace e Olá nome.</span><span class="sxs-lookup"><span data-stu-id="072e6-182">So if you want toomodify them directly, don't forget toochange hello namespace and hello name.</span></span>
> 
> 

### <a name="notification-position"></a><span data-ttu-id="072e6-183">Posição de notificação</span><span class="sxs-lookup"><span data-stu-id="072e6-183">Notification position</span></span>
<span data-ttu-id="072e6-184">Por padrão, uma notificação no aplicativo é exibida no lado Olá inferior esquerdo do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="072e6-184">By default, an in-app notification is displayed at hello bottom left side of hello application.</span></span> <span data-ttu-id="072e6-185">Você pode alterar esse comportamento, substituindo Olá `GetNotificationPosition` método hello `EngagementReachHandler` objeto.</span><span class="sxs-lookup"><span data-stu-id="072e6-185">You can change this behavior by overriding hello `GetNotificationPosition` method of hello `EngagementReachHandler` object.</span></span>

    // In your subclass of EngagementReachHandler

    public override EngagementReachHandler.NotificationPosition GetNotificationPosition(EngagementNotificationViewModel viewModel)
    {
       // return a value of hello EngagementReachHandler.NotificationPosition enum (TOP or BOTTOM)
    }

<span data-ttu-id="072e6-186">No momento, você pode escolher entre hello `BOTTOM` (padrão) e `TOP` posições.</span><span class="sxs-lookup"><span data-stu-id="072e6-186">Currently, you can choose between hello `BOTTOM` (default) and `TOP` positions.</span></span>

### <a name="launch-message"></a><span data-ttu-id="072e6-187">Iniciar mensagem</span><span class="sxs-lookup"><span data-stu-id="072e6-187">Launch message</span></span>
<span data-ttu-id="072e6-188">Quando um usuário clica em um sistema de notificação (uma notificação do sistema), inicia contrato Olá aplicativo, conteúdo de saudação do carregamento de saudação por push as mensagens e exibir página Olá Olá correspondente campanha.</span><span class="sxs-lookup"><span data-stu-id="072e6-188">When a user clicks on a system notification (a toast), Engagement launches hello app, load hello content of hello push messages, and display hello page for hello corresponding campaign.</span></span>

<span data-ttu-id="072e6-189">Há um atraso entre a inicialização de saudação da exibição de aplicativo e Olá Olá da página de saudação (dependendo da velocidade da saudação da sua rede).</span><span class="sxs-lookup"><span data-stu-id="072e6-189">There is a delay between hello launch of hello application and hello display of hello page (depending on hello speed of your network).</span></span>

<span data-ttu-id="072e6-190">tooindicate toohello o usuário que algo está sendo carregado, você deve fornecer uma informações visuais, como uma barra de progresso ou um indicador de progresso.</span><span class="sxs-lookup"><span data-stu-id="072e6-190">tooindicate toohello user that something is loading, you should provide a visual information, like a progress bar or a progress indicator.</span></span> <span data-ttu-id="072e6-191">O Engagement não pode manipular isto por conta própria, mas oferece alguns manipuladores para você.</span><span class="sxs-lookup"><span data-stu-id="072e6-191">Engagement cannot handle that itself, but provides a few handlers for you.</span></span>

<span data-ttu-id="072e6-192">tooimplement Olá retorno de chamada, execute:</span><span class="sxs-lookup"><span data-stu-id="072e6-192">tooimplement hello callback, do:</span></span>

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

<span data-ttu-id="072e6-193">Você pode definir o retorno de chamada de saudação seu `Application_Launching` método de sua `App.xaml.cs` arquivos, preferencialmente antes Olá `EngagementReach.Instance.Init()` chamar.</span><span class="sxs-lookup"><span data-stu-id="072e6-193">You can set hello callback in your `Application_Launching` method of your `App.xaml.cs` file, preferably before hello `EngagementReach.Instance.Init()` call.</span></span>

> [!TIP]
> <span data-ttu-id="072e6-194">Cada manipulador é chamado pelo Olá Thread de interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="072e6-194">Each handler is called by hello UI Thread.</span></span> <span data-ttu-id="072e6-195">Você não tem tooworry ao usar uma MessageBox ou algo relacionados à interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="072e6-195">You do not have tooworry when using a MessageBox or something UI-related.</span></span>
> 
> 

[políticas de aplicativo]:http://msdn.microsoft.com/library/windows/apps/hh184841(v=vs.105).aspx
[Content Policies]:http://msdn.microsoft.com/library/windows/apps/hh184842(v=vs.105).aspx
[requisitos adicionais para tipos específicos de aplicativo]:http://msdn.microsoft.com/library/windows/apps/hh184838(v=vs.105).aspx

