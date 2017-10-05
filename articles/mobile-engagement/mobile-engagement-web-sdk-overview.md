---
title: "Visão geral do SDK para Web do Azure Mobile Engagement | Microsoft Docs"
description: "As atualizações e procedimentos mais recentes do SDK para Web do Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 5bbc2fda-0f3f-43d0-a73d-0f2c0f8dc25b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: web
ms.devlang: js
ms.topic: article
ms.date: 10/18/2016
ms.author: piyushjo
ms.openlocfilehash: 770a83131a3e661771db50b22ce7de25b2d541cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-mobile-engagement-web-sdk"></a><span data-ttu-id="acc7e-103">SDK Web do Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="acc7e-103">Azure Mobile Engagement Web SDK</span></span>
<span data-ttu-id="acc7e-104">Comece aqui para obter todos os detalhes sobre como integrar o Azure Mobile Engagement em um aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="acc7e-104">Start here for all the details about how to integrate Azure Mobile Engagement in a web app.</span></span> <span data-ttu-id="acc7e-105">Se você gostaria de experimentá-lo antes de começar com seu próprio aplicativo Web, confira nosso [tutorial de 15 minutos](mobile-engagement-web-app-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="acc7e-105">If you'd like to give it a try before getting started with your own web app, see our [15-minute tutorial](mobile-engagement-web-app-get-started.md).</span></span>

## <a name="integration-procedures"></a><span data-ttu-id="acc7e-106">Procedimentos de integração</span><span class="sxs-lookup"><span data-stu-id="acc7e-106">Integration procedures</span></span>
1. <span data-ttu-id="acc7e-107">Saiba [Como integrar o Mobile Engagement ao seu aplicativo Web](mobile-engagement-web-integrate-engagement.md).</span><span class="sxs-lookup"><span data-stu-id="acc7e-107">Learn [how to integrate Mobile Engagement in your web app](mobile-engagement-web-integrate-engagement.md).</span></span>
2. <span data-ttu-id="acc7e-108">Para a implementação do plano de marcação, saiba [Como usar a API de marcação avançada do Mobile Engagement em seu aplicativo Web](mobile-engagement-web-use-engagement-api.md).</span><span class="sxs-lookup"><span data-stu-id="acc7e-108">For tag plan implementation, learn [how to use the advanced Mobile Engagement tagging API in your web app](mobile-engagement-web-use-engagement-api.md).</span></span>

## <a name="release-notes"></a><span data-ttu-id="acc7e-109">Notas de versão</span><span class="sxs-lookup"><span data-stu-id="acc7e-109">Release notes</span></span>
### <a name="202-10182016"></a><span data-ttu-id="acc7e-110">2.0.2 (18/10/2016)</span><span class="sxs-lookup"><span data-stu-id="acc7e-110">2.0.2 (10/18/2016)</span></span>
* <span data-ttu-id="acc7e-111">Falha corrigida na navegação particular (Safari).</span><span class="sxs-lookup"><span data-stu-id="acc7e-111">Fixed crash on private browsing (Safari).</span></span>
* <span data-ttu-id="acc7e-112">Falha corrigida em navegadores com cookies desabilitados.</span><span class="sxs-lookup"><span data-stu-id="acc7e-112">Fixed crash on browsers with cookies disabled.</span></span>

<span data-ttu-id="acc7e-113">Para obter todas as versões, veja as [notas de versão completas](mobile-engagement-web-release-notes.md).</span><span class="sxs-lookup"><span data-stu-id="acc7e-113">For all versions, please see the [complete release notes](mobile-engagement-web-release-notes.md).</span></span>

## <a name="upgrade-procedures"></a><span data-ttu-id="acc7e-114">Procedimentos de atualização</span><span class="sxs-lookup"><span data-stu-id="acc7e-114">Upgrade procedures</span></span>
### <a name="upgrade-from-121-to-200"></a><span data-ttu-id="acc7e-115">Atualizar da 1.2.1 para a 2.0.0</span><span class="sxs-lookup"><span data-stu-id="acc7e-115">Upgrade from 1.2.1 to 2.0.0</span></span>
<span data-ttu-id="acc7e-116">As seções a seguir descrevem como migrar uma integração do SDK para Web do Mobile Engagement do serviço Capptain, oferecido pelo Capptain SAS, para um aplicativo do Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="acc7e-116">The following sections describe how to migrate a Mobile Engagement Web SDK integration from the Capptain service, offered by Capptain SAS, to an Azure Mobile Engagement app.</span></span> <span data-ttu-id="acc7e-117">Se você estiver migrando de uma versão anterior à 1.2.1, consulte o site do Capptain para migrar primeiro para 1.2.1 e depois aplicar o procedimento a seguir.</span><span class="sxs-lookup"><span data-stu-id="acc7e-117">If you are migrating from a version earlier than 1.2.1, please consult the Capptain website to migrate to 1.2.1 first, and then apply the following procedures.</span></span>

<span data-ttu-id="acc7e-118">Essa versão do SDK para Web do Mobile Engagement não dá suporte para Samsung Smart TV, Opera TV, webOS ou com o recurso Reach.</span><span class="sxs-lookup"><span data-stu-id="acc7e-118">This version of the Mobile Engagement Web SDK doesn't support Samsung Smart TV, Opera TV, webOS, or the Reach feature.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="acc7e-119">O Capptain e o Azure Mobile Engagement não são o mesmo serviço e os procedimentos a seguir destacam apenas como migrar o aplicativo cliente.</span><span class="sxs-lookup"><span data-stu-id="acc7e-119">Capptain and Azure Mobile Engagement are not the same service, and the following procedures highlight only how to migrate the client app.</span></span> <span data-ttu-id="acc7e-120">Migrar o SDK para Web do Mobile Engagement no aplicativo não migrará os dados de um servidor do Capptain para um servidor do Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="acc7e-120">Migrating the Mobile Engagement Web SDK in the app will not migrate your data from a Capptain server to a Mobile Engagement server.</span></span>
> 
> 

#### <a name="javascript-files"></a><span data-ttu-id="acc7e-121">Arquivos JavaScript</span><span class="sxs-lookup"><span data-stu-id="acc7e-121">JavaScript files</span></span>
<span data-ttu-id="acc7e-122">Substitua o arquivo capptain-sdk.js pelo arquivo azure-engagement.js e atualize suas importações de script adequadamente.</span><span class="sxs-lookup"><span data-stu-id="acc7e-122">Replace the file capptain-sdk.js with the file azure-engagement.js, and then update your script imports accordingly.</span></span>

#### <a name="remove-capptain-reach"></a><span data-ttu-id="acc7e-123">Remover o Capptain Reach</span><span class="sxs-lookup"><span data-stu-id="acc7e-123">Remove Capptain Reach</span></span>
<span data-ttu-id="acc7e-124">Essa versão do SDK para Web do Mobile Engagement não dá suporte ao recurso Reach.</span><span class="sxs-lookup"><span data-stu-id="acc7e-124">This version of the Mobile Engagement Web SDK doesn't support the Reach feature.</span></span> <span data-ttu-id="acc7e-125">Se você integrou o Capptain Reach ao aplicativo, será necessário removê-lo.</span><span class="sxs-lookup"><span data-stu-id="acc7e-125">If you have integrated Capptain Reach into your application, you need to remove it.</span></span>

<span data-ttu-id="acc7e-126">Remova a importação de CSS do Reach da sua página e exclua o arquivo .css relacionado (capptain-reach.css, por padrão).</span><span class="sxs-lookup"><span data-stu-id="acc7e-126">Remove the Reach CSS import from your page and delete the related .css file (capptain-reach.css, by default).</span></span>

<span data-ttu-id="acc7e-127">Exclua os seguintes recursos do Reach: a imagem de fechamento (capptain-close.png, por padrão) e o ícone da marca (capptain-notification-icon, por padrão).</span><span class="sxs-lookup"><span data-stu-id="acc7e-127">Delete the following Reach resources: the close image (capptain-close.png, by default) and the brand icon (capptain-notification-icon, by default).</span></span>

<span data-ttu-id="acc7e-128">Remova a interface do usuário do Reach para notificações no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="acc7e-128">Remove the Reach UI for in-app notifications.</span></span> <span data-ttu-id="acc7e-129">O layout padrão tem esta aparência:</span><span class="sxs-lookup"><span data-stu-id="acc7e-129">The default layout looks like this:</span></span>

    <!-- capptain notification -->
    <div id="capptain_notification_area" class="capptain_category_default">
      <div class="icon">
        <img src="capptain-notification-icon.png" alt="icon" />
      </div>
      <div class="content">
        <div class="title" id="capptain_notification_title"></div>
        <div class="message" id="capptain_notification_message"></div>
      </div>
      <div id="capptain_notification_image"></div>
      <div>
        <button id="capptain_notification_close">Close</button>
      </div>
    </div>

<span data-ttu-id="acc7e-130">Remova a interface do usuário do Reach para anúncios da Web e pesquisas.</span><span class="sxs-lookup"><span data-stu-id="acc7e-130">Remove the Reach UI for text and web announcements and polls.</span></span> <span data-ttu-id="acc7e-131">O layout padrão tem esta aparência:</span><span class="sxs-lookup"><span data-stu-id="acc7e-131">The default layout looks like this:</span></span>

    <div id="capptain_overlay" class="capptain_category_default">
      <button id="capptain_overlay_close">x</button>
      <div id="capptain_overlay_title"></div>
      <div id="capptain_overlay_body"></div>
      <div id="capptain_overlay_poll"></div>
      <div id="capptain_overlay_buttons">
        <button id="capptain_overlay_exit"></button>
        <button id="capptain_overlay_action"></button>
      </div>
    </div>

<span data-ttu-id="acc7e-132">Remova o objeto `reach` da sua configuração, se ele existir.</span><span class="sxs-lookup"><span data-stu-id="acc7e-132">Remove the `reach` object from your configuration, if it exists.</span></span> <span data-ttu-id="acc7e-133">Ele tem esta aparência:</span><span class="sxs-lookup"><span data-stu-id="acc7e-133">It looks like this:</span></span>

    window.capptain = {
      [...]
      reach: {
        [...]
      }
    }

<span data-ttu-id="acc7e-134">Remova qualquer outra personalização do Reach, como categorias.</span><span class="sxs-lookup"><span data-stu-id="acc7e-134">Remove any other Reach customization, such as categories.</span></span>

#### <a name="remove-deprecated-apis"></a><span data-ttu-id="acc7e-135">Remover APIs substituídas</span><span class="sxs-lookup"><span data-stu-id="acc7e-135">Remove deprecated APIs</span></span>
<span data-ttu-id="acc7e-136">Algumas das APIs do Capptain foram preteridas na versão do SDK para Web do Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="acc7e-136">Some APIs from Capptain are deprecated in the Mobile Engagement Web SDK.</span></span>

<span data-ttu-id="acc7e-137">Remova todas as chamadas para as seguintes APIs: `agent.connect`, `agent.disconnect`, `agent.pause` e `agent.sendMessageToDevice`.</span><span class="sxs-lookup"><span data-stu-id="acc7e-137">Remove any calls to the following APIs: `agent.connect`, `agent.disconnect`, `agent.pause`, and `agent.sendMessageToDevice`.</span></span>

<span data-ttu-id="acc7e-138">Remova todos os seguintes retornos de chamada da sua configuração do Capptain: `onConnected`, `onDisconnected`, `onDeviceMessageReceived` e `onPushMessageReceived`.</span><span class="sxs-lookup"><span data-stu-id="acc7e-138">Remove any of the following callbacks from your Capptain configuration: `onConnected`, `onDisconnected`, `onDeviceMessageReceived`, and `onPushMessageReceived`.</span></span>

#### <a name="configuration"></a><span data-ttu-id="acc7e-139">Configuração</span><span class="sxs-lookup"><span data-stu-id="acc7e-139">Configuration</span></span>
<span data-ttu-id="acc7e-140">O Mobile Engagement usa uma cadeia de conexão para configurar os identificadores do SDK, por exemplo, o identificador do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="acc7e-140">Mobile Engagement uses a connection string to configure SDK identifiers, for example, the application identifier.</span></span>

<span data-ttu-id="acc7e-141">Substitua a ID do aplicativo pela cadeia de conexão.</span><span class="sxs-lookup"><span data-stu-id="acc7e-141">Replace the application ID with your connection string.</span></span> <span data-ttu-id="acc7e-142">Observe que o objeto global para a configuração do SDK muda de `capptain` para `azureEngagement`.</span><span class="sxs-lookup"><span data-stu-id="acc7e-142">Note that the global object for the SDK configuration changes from `capptain` to `azureEngagement`.</span></span>

<span data-ttu-id="acc7e-143">Antes da migração:</span><span class="sxs-lookup"><span data-stu-id="acc7e-143">Before migration:</span></span>

    window.capptain = {
      appId: ...,
      [...]
    };

<span data-ttu-id="acc7e-144">Após a migração:</span><span class="sxs-lookup"><span data-stu-id="acc7e-144">After migration:</span></span>

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      [...]
    };

<span data-ttu-id="acc7e-145">A cadeia de conexão para o seu aplicativo é exibida no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="acc7e-145">The connection string for your application is displayed in the Azure portal.</span></span>

#### <a name="javascript-apis"></a><span data-ttu-id="acc7e-146">APIs do JavaScript</span><span class="sxs-lookup"><span data-stu-id="acc7e-146">JavaScript APIs</span></span>
<span data-ttu-id="acc7e-147">O objeto `window.capptain` global do JavaScript foi renomeado para `window.azureEngagement`, mas você pode usar o alias `window.engagement` para chamadas à API.</span><span class="sxs-lookup"><span data-stu-id="acc7e-147">The global JavaScript object `window.capptain` has been renamed `window.azureEngagement`, but you can use the `window.engagement` alias for API calls.</span></span> <span data-ttu-id="acc7e-148">Você não pode usar o alias para definir a configuração do SDK.</span><span class="sxs-lookup"><span data-stu-id="acc7e-148">You can't use this alias to define the SDK configuration.</span></span>

<span data-ttu-id="acc7e-149">Por exemplo: `capptain.deviceId` se torna `engagement.deviceId`, `capptain.agent.startActivity` se torna `engagement.agent.startActivity` e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="acc7e-149">For instance, `capptain.deviceId` becomes `engagement.deviceId`, `capptain.agent.startActivity` becomes `engagement.agent.startActivity`, and so on.</span></span>

<span data-ttu-id="acc7e-150">Se você já tiver integrado uma versão anterior do SDK Web do Azure Mobile Engagement ao seu aplicativo, leia sobre [procedimentos de atualização](mobile-engagement-web-upgrade-procedure.md).</span><span class="sxs-lookup"><span data-stu-id="acc7e-150">If you have already integrated an earlier version of the Azure Mobile Engagement Web SDK into your application, please read about [upgrade procedures](mobile-engagement-web-upgrade-procedure.md).</span></span>

