---
title: "Integração do SDK do Windows Phone Silverlight para o Reach"
description: Como integrar o Azure Mobile Engagement com aplicativos do Windows Phone Silverlight
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
ms.openlocfilehash: 0738f33df94d14fbb393bfaaf09e94c6560213cc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="windows-phone-silverlight-reach-sdk-integration"></a><span data-ttu-id="5c7ce-103">Integração do SDK do Windows Phone Silverlight para o Reach</span><span class="sxs-lookup"><span data-stu-id="5c7ce-103">Windows Phone Silverlight Reach SDK Integration</span></span>
<span data-ttu-id="5c7ce-104">Você deve seguir o procedimento de integração descrito na [Integração do SDK do Engagement do Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md) , antes de seguir este guia.</span><span class="sxs-lookup"><span data-stu-id="5c7ce-104">You must follow the integration procedure described in the [Windows Phone Silverlight Engagement SDK Integration](mobile-engagement-windows-phone-integrate-engagement.md) before following this guide.</span></span>

## <a name="embed-the-engagement-reach-sdk-into-your-windows-phone-silverlight-project"></a><span data-ttu-id="5c7ce-105">Incorpore o SDK do Engagement Reach em seu projeto do Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="5c7ce-105">Embed the Engagement Reach SDK into your Windows Phone Silverlight project</span></span>
<span data-ttu-id="5c7ce-106">Você não tem nada a adicionar.</span><span class="sxs-lookup"><span data-stu-id="5c7ce-106">You do not have anything to add.</span></span> <span data-ttu-id="5c7ce-107">`EngagementReach` já estão em seu projeto.</span><span class="sxs-lookup"><span data-stu-id="5c7ce-107">`EngagementReach` references and resources are already in your project.</span></span>

> [!TIP]
> <span data-ttu-id="5c7ce-108">Você pode personalizar imagens localizadas na pasta `Resources` do seu projeto, especialmente o ícone de marca (esse padrão para o ícone do Engagement).</span><span class="sxs-lookup"><span data-stu-id="5c7ce-108">You can customize images located in the `Resources` folder of your project, especially the brand icon (that default to the Engagement icon).</span></span>
> 
> 

## <a name="add-the-capabilities"></a><span data-ttu-id="5c7ce-109">Adicione recursos</span><span class="sxs-lookup"><span data-stu-id="5c7ce-109">Add the capabilities</span></span>
<span data-ttu-id="5c7ce-110">O SDK do Engagement Reach precisa de alguns recursos adicionais.</span><span class="sxs-lookup"><span data-stu-id="5c7ce-110">The Engagement Reach SDK needs some additional capabilities.</span></span>

<span data-ttu-id="5c7ce-111">Abra o seu arquivo `WMAppManifest.xml` e certifique-se de que os seguintes recursos estão declarados:</span><span class="sxs-lookup"><span data-stu-id="5c7ce-111">Open your `WMAppManifest.xml` file and be sure that the following capabilities are declared:</span></span>

* `ID_CAP_PUSH_NOTIFICATION`
* `ID_CAP_WEBBROWSERCOMPONENT`

<span data-ttu-id="5c7ce-112">O primeiro deles é usado pelo serviço MPNS para permitir a exibição de notificação do sistema.</span><span class="sxs-lookup"><span data-stu-id="5c7ce-112">The first one is used by the MPNS service to allow the display of toast notification.</span></span> <span data-ttu-id="5c7ce-113">O segundo é usado para inserir uma tarefa de navegador no SDK.</span><span class="sxs-lookup"><span data-stu-id="5c7ce-113">The second one is used to embed a browser task into the SDK.</span></span>

<span data-ttu-id="5c7ce-114">Editar o arquivo `WMAppManifest.xml` e adicione dentro da marca `<Capabilities />` :</span><span class="sxs-lookup"><span data-stu-id="5c7ce-114">Edit the `WMAppManifest.xml` file and add inside the `<Capabilities />` tag :</span></span>

    <Capability Name="ID_CAP_PUSH_NOTIFICATION" />
    <Capability Name="ID_CAP_WEBBROWSERCOMPONENT" />

## <a name="enable-the-microsoft-push-notification-service"></a><span data-ttu-id="5c7ce-115">Habilitar o serviço de notificação por push da Microsoft</span><span class="sxs-lookup"><span data-stu-id="5c7ce-115">Enable the Microsoft Push Notification Service</span></span>
<span data-ttu-id="5c7ce-116">Para usar o **Serviço de Notificação por Push da Microsoft** (chamado MPNS), seu arquivo `WMAppManifest.xml` deverá ter uma marca `<App />` com um atributo `Publisher` definido como o nome do seu projeto.</span><span class="sxs-lookup"><span data-stu-id="5c7ce-116">In order to use the **Microsoft Push Notification Service** (referred as MPNS) your `WMAppManifest.xml` file must have an `<App />` tag with a `Publisher` attribute set to the name of your project.</span></span>

## <a name="initialize-the-engagement-reach-sdk"></a><span data-ttu-id="5c7ce-117">Inicializar o SDK do Engagement Reach</span><span class="sxs-lookup"><span data-stu-id="5c7ce-117">Initialize the Engagement Reach SDK</span></span>
### <a name="engagement-configuration"></a><span data-ttu-id="5c7ce-118">Configuração do Engagement</span><span class="sxs-lookup"><span data-stu-id="5c7ce-118">Engagement configuration</span></span>
<span data-ttu-id="5c7ce-119">A configuração do Engagement está centralizada no arquivo `Resources\EngagementConfiguration.xml` do seu projeto.</span><span class="sxs-lookup"><span data-stu-id="5c7ce-119">The Engagement configuration is centralized in the `Resources\EngagementConfiguration.xml` file of your project.</span></span>

<span data-ttu-id="5c7ce-120">Edite esse arquivo para especificar a configuração de alcance:</span><span class="sxs-lookup"><span data-stu-id="5c7ce-120">Edit this file to specify reach configuration :</span></span>

* <span data-ttu-id="5c7ce-121">*Opcional*, indique se o push nativo (MPNS) está ativado ou não entre as marcas `<enableNativePush>` e `</enableNativePush>`, (`true` por padrão).</span><span class="sxs-lookup"><span data-stu-id="5c7ce-121">*Optional*, indicate whether the native push (MPNS) is activated or not between `<enableNativePush>` and `</enableNativePush>` tags, (`true` by default).</span></span>
* <span data-ttu-id="5c7ce-122">*Opcional*, indique o nome do canal push entre as marcas `<channelName>` e `</channelName>`, forneça o mesmo que seu aplicativo possa usar no momento ou deixo-o vazio.</span><span class="sxs-lookup"><span data-stu-id="5c7ce-122">*Optional*, indicate the name of the push channel between `<channelName>` and `</channelName>` tags, provide the same that your application may currently use or leave it empty.</span></span>

<span data-ttu-id="5c7ce-123">Se você quiser especificá-lo em tempo de execução, você pode chamar o método a seguir antes da inicialização do agente do Engagement:</span><span class="sxs-lookup"><span data-stu-id="5c7ce-123">If you want to specify it at runtime instead, you can call the following method before the Engagement agent initialization :</span></span>

    /* Engagement configuration. */
    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();

    engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

    engagementConfiguration.Reach.EnableNativePush = true;                  
    /* [Optional] whether the native push (MPNS) is activated or not. */

    engagementConfiguration.Reach.ChannelName = "YOUR_PUSH_CHANNEL_NAME";   
    /* [Optional] Provide the same channel name that your application may currently use. */

    /* Initialize Engagement agent with above configuration. */
    EngagementAgent.Instance.Init(engagementConfiguration);

> [!TIP]
> <span data-ttu-id="5c7ce-124">Você pode especificar o nome do canal de notificação MPNS do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5c7ce-124">You can specify the name of the MPNS push channel of your application.</span></span> <span data-ttu-id="5c7ce-125">Por padrão, o Engagement cria um nome baseado na appId.</span><span class="sxs-lookup"><span data-stu-id="5c7ce-125">By default, Engagement creates a name based on the appId.</span></span> <span data-ttu-id="5c7ce-126">Você não precisa especificar o nome, exceto se você planeja usar o canal de notificação fora do Engagement.</span><span class="sxs-lookup"><span data-stu-id="5c7ce-126">You have no need to specify the name yourself, except if you plan to use the push channel outside of Engagement.</span></span>
> 
> 

### <a name="engagement-initialization"></a><span data-ttu-id="5c7ce-127">Inicialização do Engagement</span><span class="sxs-lookup"><span data-stu-id="5c7ce-127">Engagement initialization</span></span>
<span data-ttu-id="5c7ce-128">Modifique o `App.xaml.cs`:</span><span class="sxs-lookup"><span data-stu-id="5c7ce-128">Modify the `App.xaml.cs`:</span></span>

* <span data-ttu-id="5c7ce-129">Adicione às suas instruções `using`:</span><span class="sxs-lookup"><span data-stu-id="5c7ce-129">Add to your `using` statements :</span></span>
  
      using Microsoft.Azure.Engagement;
* <span data-ttu-id="5c7ce-130">Insira `EngagementReach.Instance.Init` logo após `EngagementAgent.Instance.Init` e `Application_Launching` :</span><span class="sxs-lookup"><span data-stu-id="5c7ce-130">Insert `EngagementReach.Instance.Init` just after `EngagementAgent.Instance.Init` in `Application_Launching` :</span></span>
  
      private void Application_Launching(object sender, LaunchingEventArgs e)
      {
         EngagementAgent.Instance.Init();
         EngagementReach.Instance.Init();
      }
* <span data-ttu-id="5c7ce-131">Insira `EngagementReach.Instance.OnActivated` no método `Application_Activated` :</span><span class="sxs-lookup"><span data-stu-id="5c7ce-131">Insert `EngagementReach.Instance.OnActivated` in the `Application_Activated` method :</span></span>
  
      private void Application_Activated(object sender, ActivatedEventArgs e)
      {
         EngagementAgent.Instance.OnActivated(e);
         EngagementReach.Instance.OnActivated(e);
      }

> [!IMPORTANT]
> <span data-ttu-id="5c7ce-132">O `EngagementReach.Instance.Init` é executado em um thread dedicado.</span><span class="sxs-lookup"><span data-stu-id="5c7ce-132">The `EngagementReach.Instance.Init` runs in a dedicated thread.</span></span> <span data-ttu-id="5c7ce-133">Você não precisa fazê-lo.</span><span class="sxs-lookup"><span data-stu-id="5c7ce-133">You do not have to do it yourself.</span></span>
> 
> 

## <a name="app-store-submission-considerations"></a><span data-ttu-id="5c7ce-134">Considerações de envio de armazenamento de aplicativo</span><span class="sxs-lookup"><span data-stu-id="5c7ce-134">App store submission considerations</span></span>
<span data-ttu-id="5c7ce-135">A Microsoft impõe algumas regras ao usar as notificações de push:</span><span class="sxs-lookup"><span data-stu-id="5c7ce-135">Microsoft imposes some rules when using the push notifications:</span></span>

<span data-ttu-id="5c7ce-136">Na documentação de [Políticas de aplicativo] da Microsoft, seção 2.9:</span><span class="sxs-lookup"><span data-stu-id="5c7ce-136">From the Microsoft [Application Policies] documentation, section 2.9:</span></span>

1) <span data-ttu-id="5c7ce-137">Você deve perguntar ao usuário para aceitar para receber notificações por push.</span><span class="sxs-lookup"><span data-stu-id="5c7ce-137">You must ask the user to accept to receive push notifications.</span></span> <span data-ttu-id="5c7ce-138">Em seguida, em suas configurações, adicione uma forma de desativar as notificações de envio.</span><span class="sxs-lookup"><span data-stu-id="5c7ce-138">Then, in your settings, add a way to disable the push notifications.</span></span>

<span data-ttu-id="5c7ce-139">O objeto EngagementReach fornece dois métodos para gerenciar o opt-in/opt-out, `EnableNativePush()` e `DisableNativePush()`.</span><span class="sxs-lookup"><span data-stu-id="5c7ce-139">The EngagementReach object provides two methods to manage the opt-in/opt-out, `EnableNativePush()` and `DisableNativePush()`.</span></span> <span data-ttu-id="5c7ce-140">Você pode, por exemplo, criar uma opção nas configurações com uma alternância para desabilitar ou habilitar o MPNS.</span><span class="sxs-lookup"><span data-stu-id="5c7ce-140">You could, for example, create an option in the settings with a toggle to disable or enable MPNS.</span></span>

<span data-ttu-id="5c7ce-141">Também é possível decidir desativar o MPNS por meio da configuração do Engajamento \<windows-phone-sdk-reach-configuration\>.</span><span class="sxs-lookup"><span data-stu-id="5c7ce-141">You can also decide to deactivate MPNS through the Engagement configuration\<windows-phone-sdk-reach-configuration\>.</span></span>

> <span data-ttu-id="5c7ce-142">2.9.1) O aplicativo deve primeiro descrever as notificações a serem fornecidas e **obter a permissão expressa do usuário (opt-in)** e **deve fornecer um mecanismo pelo qual o usuário pode optar por parar de receber notificações por push**.</span><span class="sxs-lookup"><span data-stu-id="5c7ce-142">2.9.1) The application must first describe the notifications to be provided and **obtain the user’s express permission (opt-in)**, and **must provide a mechanism through which the user can opt out of receiving push notifications**.</span></span> <span data-ttu-id="5c7ce-143">Todas as notificações fornecidas usando o Serviço de Notificação por Push da Microsoft devem ser consistentes com a descrição fornecida ao usuário e devem estar em conformidade com todas as [Políticas de aplicativo][Content Policies] e [Requisitos adicionais para tipos específicos de aplicativo] aplicáveis.</span><span class="sxs-lookup"><span data-stu-id="5c7ce-143">All notifications provided using the Microsoft Push Notification Service must be consistent with the description provided to the user and must comply with all applicable [Application Policies][Content Policies] and [Additional Requirements for Specific Application Types].</span></span>
> 
> 

2) <span data-ttu-id="5c7ce-144">Você não deve usar muitas notificações por push.</span><span class="sxs-lookup"><span data-stu-id="5c7ce-144">You should not use too many push notifications.</span></span> <span data-ttu-id="5c7ce-145">O Engagement manipulará notificações para você.</span><span class="sxs-lookup"><span data-stu-id="5c7ce-145">Engagement will handle notifications for you.</span></span>

> <span data-ttu-id="5c7ce-146">2.9.2) O aplicativo e o uso do Serviço de notificação por push da Microsoft não devem usar excessivamente a capacidade de rede ou de largura de banda do serviço de notificação por push da Microsoft, ou caso contrário indevidamente sobrecarregam o Windows Phone ou outros dispositivos Microsoft ou serviço com notificações por push excessivo, conforme determinado pela Microsoft a seu critério lógico e não devem prejudicar ou interferir com nenhuma rede Microsoft ou servidores ou quaisquer servidores de terceiros ou redes conectadas ao do serviço de notificação por push da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="5c7ce-146">2.9.2) The application and its use of the Microsoft Push Notification Service must not excessively use network capacity or bandwidth of the Microsoft Push Notification Service, or otherwise unduly burden a Windows Phone or other Microsoft device or service with excessive push notifications, as determined by Microsoft in its reasonable discretion, and must not harm or interfere with any Microsoft networks or servers or any third party servers or networks connected to the Microsoft Push Notification Service.</span></span>
> 
> 

3) <span data-ttu-id="5c7ce-147">Não confie no MPNS para enviar informações muito sérias.</span><span class="sxs-lookup"><span data-stu-id="5c7ce-147">Do not rely on MPNS to send criticals information.</span></span> <span data-ttu-id="5c7ce-148">O Engagement usa o MPNS, portanto, essa regra também se aplica para campanhas criadas dentro do projeto front-end.</span><span class="sxs-lookup"><span data-stu-id="5c7ce-148">Engagement uses MPNS, so this rule also applies for the campaigns created inside the Engagement front-end.</span></span>

> <span data-ttu-id="5c7ce-149">2.9.3) O serviço de notificação por push da Microsoft não pode ser usado para enviar notificações que são de missão crítica ou que poderiam afetar assuntos de vida ou morte, incluindo, sem limitação, relacionadas a um dispositivo médico ou condição de notificações críticas.</span><span class="sxs-lookup"><span data-stu-id="5c7ce-149">2.9.3) The Microsoft Push Notification Service may not be used to send notifications that are mission critical or otherwise could affect matters of life or death, including without limitation critical notifications related to a medical device or condition.</span></span> <span data-ttu-id="5c7ce-150">A MICROSOFT EXPRESSAMENTE SE ISENTA DE QUAISQUER GARANTIAS DE QUE O USO DO SERVIÇO DE NOTIFICAÇÃO POR PUSH OU ENVIO DE NOTIFICAÇÕES DO SERVIÇO DE NOTIFICAÇÃO POR PUSH DA MICROSOFT SERÁ ININTERRUPTO, SEM ERRO, OU CASO CONTRÁRIO GARANTIDO QUE OCORRA EM TEMPO REAL.</span><span class="sxs-lookup"><span data-stu-id="5c7ce-150">MICROSOFT EXPRESSLY DISCLAIMS ANY WARRANTIES THAT THE USE OF THE MICROSOFT PUSH NOTIFICATION SERVICE OR DELIVERY OF MICROSOFT PUSH NOTIFICATION SERVICE NOTIFICATIONS WILL BE UNINTERRUPTED, ERROR FREE, OR OTHERWISE GUARANTEED TO OCCUR ON A REAL-TIME BASIS.</span></span>
> 
> 

<span data-ttu-id="5c7ce-151">**Não podemos garantir que seu aplicativo passará o processo de validação se você não respeita essas recomendações.**</span><span class="sxs-lookup"><span data-stu-id="5c7ce-151">**We cannot guarantee that your application will pass the validation process if you do not respect these recommendations.**</span></span>

## <a name="handle-data-push-optional"></a><span data-ttu-id="5c7ce-152">Manipular o push de dados (opcional)</span><span class="sxs-lookup"><span data-stu-id="5c7ce-152">Handle data push (optional)</span></span>
<span data-ttu-id="5c7ce-153">Se desejar que o aplicativo seja capaz de receber push de dados do Reach, você precisa implementar dois eventos da classe EngagementReach:</span><span class="sxs-lookup"><span data-stu-id="5c7ce-153">If you want your application to be able to receive Reach data pushes, you have to implement two events of the EngagementReach class:</span></span>

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

<span data-ttu-id="5c7ce-154">Você pode ver que o retorno de chamada de cada método retorna um valor booleano.</span><span class="sxs-lookup"><span data-stu-id="5c7ce-154">You can see that the callback of each method returns a boolean.</span></span> <span data-ttu-id="5c7ce-155">O Engagement envia um comentário ao seu back-end após distribuir o push de dados.</span><span class="sxs-lookup"><span data-stu-id="5c7ce-155">Engagement sends a feedback to its back-end after dispatching the data push.</span></span> <span data-ttu-id="5c7ce-156">Se o retorno de chamada retorna false, o comentário `exit` será enviado.</span><span class="sxs-lookup"><span data-stu-id="5c7ce-156">If the callback returns false, the `exit` feedback will be send.</span></span> <span data-ttu-id="5c7ce-157">Caso contrário, ele será `action`.</span><span class="sxs-lookup"><span data-stu-id="5c7ce-157">Otherwise, it will be `action`.</span></span> <span data-ttu-id="5c7ce-158">Se nenhum retorno de chamada for definido para os eventos, o comentário `drop` retornará ao Engagement.</span><span class="sxs-lookup"><span data-stu-id="5c7ce-158">If no callback is set for the events, the `drop` feedback will be returned to Engagement.</span></span>

> [!WARNING]
> <span data-ttu-id="5c7ce-159">O Engagement não é capaz de receber múltiplos comentários para um push de dados.</span><span class="sxs-lookup"><span data-stu-id="5c7ce-159">Engagement is not able to receive multiples feedbacks for a data push.</span></span> <span data-ttu-id="5c7ce-160">Se você pretende definir vários manipuladores em um evento, lembre-se de que os comentários corresponderá ao último enviado.</span><span class="sxs-lookup"><span data-stu-id="5c7ce-160">If you plan to set several handlers on an event, be aware that the feedback will correspond to the last one sent.</span></span> <span data-ttu-id="5c7ce-161">Nesse caso, é recomendável sempre retornar o mesmo valor para evitar que os comentários sejam confusos no front-end.</span><span class="sxs-lookup"><span data-stu-id="5c7ce-161">In this case, we recommend to always returns the same value to avoid having confusing feedback on the front-end.</span></span>
> 
> 

## <a name="customize-ui-optional"></a><span data-ttu-id="5c7ce-162">Personalizar a interface do usuário (opcional)</span><span class="sxs-lookup"><span data-stu-id="5c7ce-162">Customize UI (optional)</span></span>
### <a name="first-step"></a><span data-ttu-id="5c7ce-163">Primeira etapa</span><span class="sxs-lookup"><span data-stu-id="5c7ce-163">First step</span></span>
<span data-ttu-id="5c7ce-164">Permitir que você personalize a interface do usuário do reach.</span><span class="sxs-lookup"><span data-stu-id="5c7ce-164">We allow you to customize the reach UI.</span></span>

<span data-ttu-id="5c7ce-165">Para fazer isso, você precisa criar uma subclasse da classe `EngagementReachHandler` .</span><span class="sxs-lookup"><span data-stu-id="5c7ce-165">To do so, you have to create a subclass of the `EngagementReachHandler` class.</span></span>

<span data-ttu-id="5c7ce-166">**Exemplo de código :**</span><span class="sxs-lookup"><span data-stu-id="5c7ce-166">**Sample Code :**</span></span>

    using Microsoft.Azure.Engagement;

    namespace Example
    {
       internal class ExampleReachHandler : EngagementReachHandler
       {
          // Override EngagementReachHandler methods depending on your needs
       }
    }

<span data-ttu-id="5c7ce-167">Depois, defina o conteúdo do campo `EngagementReach.Instance.Handler` com seu objeto personalizado em sua classe `App.xaml.cs` dentro do método `Application_Launching`.</span><span class="sxs-lookup"><span data-stu-id="5c7ce-167">Then, set the content of the `EngagementReach.Instance.Handler` field with your custom object in your `App.xaml.cs` class within the `Application_Launching` method.</span></span>

<span data-ttu-id="5c7ce-168">**Exemplo de código :**</span><span class="sxs-lookup"><span data-stu-id="5c7ce-168">**Sample Code :**</span></span>

    private void Application_Launching(object sender, LaunchingEventArgs e)
    {
       // your app initialization 
       EngagementReach.Instance.Handler = new ExampleReachHandler();
       // Engagement Agent and Reach initialization
    }

> [!NOTE]
> <span data-ttu-id="5c7ce-169">Por padrão, o Engagement usa a sua própria implementação de `EngagementReachHandler`.</span><span class="sxs-lookup"><span data-stu-id="5c7ce-169">By default, Engagement uses its own implementation of `EngagementReachHandler`.</span></span> <span data-ttu-id="5c7ce-170">Você não precisa criar sua própria e se você fizer isso, você não precisa substituir cada método.</span><span class="sxs-lookup"><span data-stu-id="5c7ce-170">You don't have to create your own, and if you do so, you don't have to override every method.</span></span> <span data-ttu-id="5c7ce-171">O comportamento padrão é selecionar o objeto base do Engagement.</span><span class="sxs-lookup"><span data-stu-id="5c7ce-171">The default behavior is to select the Engagement base object.</span></span>
> 
> 

### <a name="layouts"></a><span data-ttu-id="5c7ce-172">Layouts</span><span class="sxs-lookup"><span data-stu-id="5c7ce-172">Layouts</span></span>
<span data-ttu-id="5c7ce-173">Por padrão, o Reach usará os recursos incorporados da DLL para exibir as notificações e páginas.</span><span class="sxs-lookup"><span data-stu-id="5c7ce-173">By default, Reach will use the embedded resources of the DLL to display the notifications and pages.</span></span>

<span data-ttu-id="5c7ce-174">No entanto, você pode optar por usar seus próprios recursos para refletir sua marca desses componentes.</span><span class="sxs-lookup"><span data-stu-id="5c7ce-174">However, you can decide to use your own resources to reflect your brand in these components.</span></span>

<span data-ttu-id="5c7ce-175">Você pode substituir os métodos `EngagementReachHandler` em sua subclasse para informar o Engagement para usar seus layouts:</span><span class="sxs-lookup"><span data-stu-id="5c7ce-175">You can override `EngagementReachHandler` methods in your subclass to tell Engagement to use your layouts :</span></span>

<span data-ttu-id="5c7ce-176">**Exemplo de código :**</span><span class="sxs-lookup"><span data-stu-id="5c7ce-176">**Sample Code :**</span></span>

    // In your subclass of EngagementReachHandler

    public override string GetTextViewAnnouncementUri()
    {
       // return the path of your own xaml
    }

    public override string GetWebViewAnnouncementUri()
    {
       // return the path of your own xaml
    }

    public override string GetPollUri()
    {
       // return the path of your own xaml
    }

    public override EngagementNotificationView CreateNotification(EngagementNotificationViewModel viewModel)
    {
       // return a new instance of your own notification
    }

> [!TIP]
> <span data-ttu-id="5c7ce-177">O método `CreateNotification` pode retornar nulo.</span><span class="sxs-lookup"><span data-stu-id="5c7ce-177">The `CreateNotification` method can return null.</span></span> <span data-ttu-id="5c7ce-178">A notificação não será exibida e a campanha de alcance será descartada.</span><span class="sxs-lookup"><span data-stu-id="5c7ce-178">The notification won't be displayed and the reach campaign will be dropped.</span></span>
> 
> 

<span data-ttu-id="5c7ce-179">Para simplificar a implementação de layout, também fornecemos nossa própria xaml que pode servir como base para o seu código.</span><span class="sxs-lookup"><span data-stu-id="5c7ce-179">To simplify your layout implementation, we also provide our own xaml which can serve as a basis for your code.</span></span> <span data-ttu-id="5c7ce-180">Eles estão localizados no arquivo do SDK do Engagement (/src/reach/).</span><span class="sxs-lookup"><span data-stu-id="5c7ce-180">They are located in the Engagement SDK archive (/src/reach/).</span></span>

> [!WARNING]
> <span data-ttu-id="5c7ce-181">As fontes que fornecemos são exatamente as mesmas que usamos.</span><span class="sxs-lookup"><span data-stu-id="5c7ce-181">The sources that we provide are the exact same ones that we use.</span></span> <span data-ttu-id="5c7ce-182">Portanto, se você quiser modificá-las diretamente, não se esqueça de alterar o namespace e o nome.</span><span class="sxs-lookup"><span data-stu-id="5c7ce-182">So if you want to modify them directly, don't forget to change the namespace and the name.</span></span>
> 
> 

### <a name="notification-position"></a><span data-ttu-id="5c7ce-183">Posição de notificação</span><span class="sxs-lookup"><span data-stu-id="5c7ce-183">Notification position</span></span>
<span data-ttu-id="5c7ce-184">Por padrão, uma notificação no aplicativo é exibida na parte inferior esquerda do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="5c7ce-184">By default, an in-app notification is displayed at the bottom left side of the application.</span></span> <span data-ttu-id="5c7ce-185">Você pode alterar esse comportamento, substituindo o método `GetNotificationPosition` do objeto `EngagementReachHandler`.</span><span class="sxs-lookup"><span data-stu-id="5c7ce-185">You can change this behavior by overriding the `GetNotificationPosition` method of the `EngagementReachHandler` object.</span></span>

    // In your subclass of EngagementReachHandler

    public override EngagementReachHandler.NotificationPosition GetNotificationPosition(EngagementNotificationViewModel viewModel)
    {
       // return a value of the EngagementReachHandler.NotificationPosition enum (TOP or BOTTOM)
    }

<span data-ttu-id="5c7ce-186">No momento, você pode escolher entre as posições `BOTTOM`(padrão) e `TOP`.</span><span class="sxs-lookup"><span data-stu-id="5c7ce-186">Currently, you can choose between the `BOTTOM` (default) and `TOP` positions.</span></span>

### <a name="launch-message"></a><span data-ttu-id="5c7ce-187">Iniciar mensagem</span><span class="sxs-lookup"><span data-stu-id="5c7ce-187">Launch message</span></span>
<span data-ttu-id="5c7ce-188">Quando um usuário clica em um sistema de notificação (um toast), o Engagement inicia o aplicativo, carrega o conteúdo das mensagens de envio por push e exibe a página da campanha correspondente.</span><span class="sxs-lookup"><span data-stu-id="5c7ce-188">When a user clicks on a system notification (a toast), Engagement launches the app, load the content of the push messages, and display the page for the corresponding campaign.</span></span>

<span data-ttu-id="5c7ce-189">Há um atraso entre a inicialização do aplicativo e a exibição da página (dependendo da velocidade da sua rede).</span><span class="sxs-lookup"><span data-stu-id="5c7ce-189">There is a delay between the launch of the application and the display of the page (depending on the speed of your network).</span></span>

<span data-ttu-id="5c7ce-190">Para indicar ao usuário que algo está sendo carregado, você deve fornecer informações visuais, como uma barra de progresso ou um indicador de progresso.</span><span class="sxs-lookup"><span data-stu-id="5c7ce-190">To indicate to the user that something is loading, you should provide a visual information, like a progress bar or a progress indicator.</span></span> <span data-ttu-id="5c7ce-191">O Engagement não pode manipular isto por conta própria, mas oferece alguns manipuladores para você.</span><span class="sxs-lookup"><span data-stu-id="5c7ce-191">Engagement cannot handle that itself, but provides a few handlers for you.</span></span>

<span data-ttu-id="5c7ce-192">Para implementar o retorno de chamada, execute:</span><span class="sxs-lookup"><span data-stu-id="5c7ce-192">To implement the callback, do:</span></span>

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

<span data-ttu-id="5c7ce-193">Você pode definir o retorno de chamada em seu método `Application_Launching` de seu arquivo `App.xaml.cs`, de preferência antes da chamada de `EngagementReach.Instance.Init()`.</span><span class="sxs-lookup"><span data-stu-id="5c7ce-193">You can set the callback in your `Application_Launching` method of your `App.xaml.cs` file, preferably before the `EngagementReach.Instance.Init()` call.</span></span>

> [!TIP]
> <span data-ttu-id="5c7ce-194">Cada manipulador é chamado pelo Thread de interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="5c7ce-194">Each handler is called by the UI Thread.</span></span> <span data-ttu-id="5c7ce-195">Você não precisa se preocupar ao usar uma MessageBox ou algo relacionado à interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="5c7ce-195">You do not have to worry when using a MessageBox or something UI-related.</span></span>
> 
> 

<span data-ttu-id="5c7ce-196">[Políticas de aplicativo]:http://msdn.microsoft.com/library/windows/apps/hh184841(v=vs.105).aspx</span><span class="sxs-lookup"><span data-stu-id="5c7ce-196">[Application Policies]:http://msdn.microsoft.com/library/windows/apps/hh184841(v=vs.105).aspx</span></span>
[Content Policies]:http://msdn.microsoft.com/library/windows/apps/hh184842(v=vs.105).aspx
<span data-ttu-id="5c7ce-197">[Requisitos adicionais para tipos específicos de aplicativo]:http://msdn.microsoft.com/library/windows/apps/hh184838(v=vs.105).aspx</span><span class="sxs-lookup"><span data-stu-id="5c7ce-197">[Additional Requirements for Specific Application Types]:http://msdn.microsoft.com/library/windows/apps/hh184838(v=vs.105).aspx</span></span>

