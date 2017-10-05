---
title: "Procedimentos de atualização do SDK para Web do Azure Mobile Engagement | Microsoft Docs"
description: "As atualizações e procedimentos mais recentes do SDK para Web do Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: a20529b4-ec8d-4503-8ae9-09b5f0846d5b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: web
ms.devlang: js
ms.topic: article
ms.date: 06/07/2016
ms.author: piyushjo
ms.openlocfilehash: afa8037dcb7a53042fa606e2c4014b442d4be326
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-mobile-engagement-web-sdk-upgrade-procedures"></a><span data-ttu-id="4e874-103">Procedimentos de atualização do SDK para Web do Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="4e874-103">Azure Mobile Engagement Web SDK upgrade procedures</span></span>
<span data-ttu-id="4e874-104">Se você já tiver integrado uma versão anterior do SDK para Web do Azure Mobile Engagement em seu aplicativo Web, precisará considerar os seguintes pontos ao atualizar o SDK.</span><span class="sxs-lookup"><span data-stu-id="4e874-104">If you have already integrated an earlier version of the Azure Mobile Engagement Web SDK into your web application, you need to consider the following points when you upgrade the SDK.</span></span>

<span data-ttu-id="4e874-105">Se você tiver ignorado várias versões do SDK para Web do Mobile Engagement, talvez seja necessário concluir vários procedimentos durante o processo de atualização.</span><span class="sxs-lookup"><span data-stu-id="4e874-105">If you skipped multiple versions of the Mobile Engagement Web SDK, you might need to complete several procedures during the upgrade process.</span></span> <span data-ttu-id="4e874-106">Por exemplo, se você migrar da 1.4.0 para a 1.6.0, primeiro siga os procedimentos para atualizar da 1.4.0 para a 1.5.0.</span><span class="sxs-lookup"><span data-stu-id="4e874-106">For example, if you migrate from 1.4.0 to 1.6.0, first follow the procedures to upgrade from 1.4.0 to 1.5.0.</span></span> <span data-ttu-id="4e874-107">Em seguida, siga os procedimentos para atualizar da 1.5.0 para a 1.6.0.</span><span class="sxs-lookup"><span data-stu-id="4e874-107">Then, follow the procedures to upgrade from 1.5.0 to 1.6.0.</span></span>

<span data-ttu-id="4e874-108">Seja qual for a versão da qual você está realizando a atualização, substitua qualquer versão anterior do arquivo azure-engagement.js pela versão mais recente dele.</span><span class="sxs-lookup"><span data-stu-id="4e874-108">Whichever version you upgrade from, replace any earlier version of the file azure-engagement.js with the latest version of the file.</span></span>

## <a name="upgrade-from-121-to-200"></a><span data-ttu-id="4e874-109">Atualizar da 1.2.1 para a 2.0.0</span><span class="sxs-lookup"><span data-stu-id="4e874-109">Upgrade from 1.2.1 to 2.0.0</span></span>
<span data-ttu-id="4e874-110">Esta seção descreve como migrar uma integração do SDK para Web do Mobile Engagement do serviço Capptain, oferecido pelo Capptain SAS, para um aplicativo do Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="4e874-110">This section describes how to migrate a Mobile Engagement Web SDK integration from the Capptain service, offered by Capptain SAS, to an Azure Mobile Engagement app.</span></span> <span data-ttu-id="4e874-111">Se você estiver migrando de uma versão anterior, consulte o site do Capptain para migrar primeiro para 1.2.1 e depois aplicar os procedimentos a seguir.</span><span class="sxs-lookup"><span data-stu-id="4e874-111">If you are migrating from an earlier version, please consult the Capptain website to first migrate to 1.2.1, and then apply the following procedures.</span></span>

<span data-ttu-id="4e874-112">Essa versão do SDK para Web do Mobile Engagement não dá suporte para Samsung Smart TV, Opera TV, webOS ou com o recurso Reach.</span><span class="sxs-lookup"><span data-stu-id="4e874-112">This version of the Mobile Engagement Web SDK doesn't support Samsung Smart TV, Opera TV, webOS, or the Reach feature.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4e874-113">O Capptain e o Azure Mobile Engagement não são o mesmo serviço.</span><span class="sxs-lookup"><span data-stu-id="4e874-113">Capptain and Azure Mobile Engagement are not the same service.</span></span> <span data-ttu-id="4e874-114">O procedimento a seguir destaca apenas como migrar o aplicativo cliente.</span><span class="sxs-lookup"><span data-stu-id="4e874-114">The following procedure highlights only how to migrate the client app.</span></span> <span data-ttu-id="4e874-115">Migrar o SDK para Web do Mobile Engagement no aplicativo não migrará os dados de um servidor do Capptain para um servidor do Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="4e874-115">Migrating the Mobile Engagement Web SDK in the app will not migrate your data from a Capptain server to a Mobile Engagement server.</span></span>
> 
> 

### <a name="javascript-files"></a><span data-ttu-id="4e874-116">Arquivos JavaScript</span><span class="sxs-lookup"><span data-stu-id="4e874-116">JavaScript files</span></span>
<span data-ttu-id="4e874-117">Substitua o arquivo capptain-sdk.js pelo arquivo azure-engagement.js e atualize suas importações de script adequadamente.</span><span class="sxs-lookup"><span data-stu-id="4e874-117">Replace the file capptain-sdk.js with the file azure-engagement.js, and then update your script imports accordingly.</span></span>

### <a name="remove-capptain-reach"></a><span data-ttu-id="4e874-118">Remover o Capptain Reach</span><span class="sxs-lookup"><span data-stu-id="4e874-118">Remove Capptain Reach</span></span>
<span data-ttu-id="4e874-119">Essa versão do SDK para Web do Mobile Engagement não dá suporte ao recurso Reach.</span><span class="sxs-lookup"><span data-stu-id="4e874-119">This version of the Mobile Engagement Web SDK doesn't support the Reach feature.</span></span> <span data-ttu-id="4e874-120">Se você tiver integrado o Capptain Reach ao aplicativo, será necessário removê-lo.</span><span class="sxs-lookup"><span data-stu-id="4e874-120">If you integrated Capptain Reach into your application, you need to remove it.</span></span>

<span data-ttu-id="4e874-121">Remova a importação de CSS do Reach da sua página e exclua o arquivo .css relacionado (capptain-reach.css, por padrão).</span><span class="sxs-lookup"><span data-stu-id="4e874-121">Remove the Reach CSS import from your page and delete the related .css file (capptain-reach.css, by default).</span></span>

<span data-ttu-id="4e874-122">Exclua os seguintes recursos do Reach: a imagem de fechamento (capptain-close.png, por padrão) e o ícone da marca (capptain-notification-icon, por padrão).</span><span class="sxs-lookup"><span data-stu-id="4e874-122">Delete the following Reach resources: the close image (capptain-close.png, by default) and the brand icon (capptain-notification-icon, by default).</span></span>

<span data-ttu-id="4e874-123">Remova a interface do usuário do Reach para notificações no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4e874-123">Remove the Reach UI for in-app notifications.</span></span> <span data-ttu-id="4e874-124">O layout padrão tem esta aparência:</span><span class="sxs-lookup"><span data-stu-id="4e874-124">The default layout looks like this:</span></span>

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

<span data-ttu-id="4e874-125">Remova a interface do usuário do Reach para anúncios da Web e pesquisas.</span><span class="sxs-lookup"><span data-stu-id="4e874-125">Remove the Reach UI for text and web announcements and polls.</span></span> <span data-ttu-id="4e874-126">O layout padrão tem esta aparência:</span><span class="sxs-lookup"><span data-stu-id="4e874-126">The default layout looks like this:</span></span>

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

<span data-ttu-id="4e874-127">Remova o objeto `reach` da sua configuração, se ele existir.</span><span class="sxs-lookup"><span data-stu-id="4e874-127">Remove the `reach` object from your configuration, if it exists.</span></span> <span data-ttu-id="4e874-128">Ele tem esta aparência:</span><span class="sxs-lookup"><span data-stu-id="4e874-128">It looks like this:</span></span>

    window.capptain = {
      [...]
      reach: {
        [...]
      }
    }

<span data-ttu-id="4e874-129">Remova qualquer outra personalização do Reach, como categorias.</span><span class="sxs-lookup"><span data-stu-id="4e874-129">Remove any other Reach customization, such as categories.</span></span>

### <a name="remove-deprecated-apis"></a><span data-ttu-id="4e874-130">Remover APIs substituídas</span><span class="sxs-lookup"><span data-stu-id="4e874-130">Remove deprecated APIs</span></span>
<span data-ttu-id="4e874-131">Algumas das APIs do Capptain foram preteridas na versão do SDK para Web do Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="4e874-131">Some APIs from Capptain are deprecated in the Mobile Engagement Web SDK.</span></span>

<span data-ttu-id="4e874-132">Remova todas as chamadas para as seguintes APIs: `agent.connect`, `agent.disconnect`, `agent.pause` e `agent.sendMessageToDevice`.</span><span class="sxs-lookup"><span data-stu-id="4e874-132">Remove any calls to the following APIs: `agent.connect`, `agent.disconnect`, `agent.pause`, and `agent.sendMessageToDevice`.</span></span>

<span data-ttu-id="4e874-133">Remova as instâncias dos seguintes retornos de chamada da sua configuração do Capptain: `onConnected`, `onDisconnected`, `onDeviceMessageReceived` e `onPushMessageReceived`.</span><span class="sxs-lookup"><span data-stu-id="4e874-133">Remove any instances of the following callbacks from your Capptain configuration: `onConnected`, `onDisconnected`, `onDeviceMessageReceived`, and `onPushMessageReceived`.</span></span>

### <a name="configuration"></a><span data-ttu-id="4e874-134">Configuração</span><span class="sxs-lookup"><span data-stu-id="4e874-134">Configuration</span></span>
<span data-ttu-id="4e874-135">O Mobile Engagement usa uma cadeia de conexão para configurar os identificadores do SDK, por exemplo, o identificador do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4e874-135">Mobile Engagement uses a connection string to configure SDK identifiers, for example, the application identifier.</span></span>

<span data-ttu-id="4e874-136">Substitua a ID do aplicativo pela cadeia de conexão.</span><span class="sxs-lookup"><span data-stu-id="4e874-136">Replace the application ID with your connection string.</span></span> <span data-ttu-id="4e874-137">Observe que o objeto global para a configuração do SDK muda de `capptain` para `azureEngagement`.</span><span class="sxs-lookup"><span data-stu-id="4e874-137">Note that the global object for the SDK configuration changes from `capptain` to `azureEngagement`.</span></span>

<span data-ttu-id="4e874-138">Antes da migração:</span><span class="sxs-lookup"><span data-stu-id="4e874-138">Before migration:</span></span>

    window.capptain = {
      appId: ...,
      [...]
    };

<span data-ttu-id="4e874-139">Após a migração:</span><span class="sxs-lookup"><span data-stu-id="4e874-139">After migration:</span></span>

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      [...]
    };

<span data-ttu-id="4e874-140">A cadeia de conexão para o seu aplicativo é exibida no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="4e874-140">The connection string for your application is displayed in the Azure Portal.</span></span>

### <a name="javascript-apis"></a><span data-ttu-id="4e874-141">APIs do JavaScript</span><span class="sxs-lookup"><span data-stu-id="4e874-141">JavaScript APIs</span></span>
<span data-ttu-id="4e874-142">O objeto `window.capptain` global do JavaScript foi renomeado para `window.azureEngagement`, mas você pode usar o alias `window.engagement` para chamadas à API.</span><span class="sxs-lookup"><span data-stu-id="4e874-142">The global JavaScript object `window.capptain` has been renamed `window.azureEngagement` but you can use the `window.engagement` alias for API calls.</span></span> <span data-ttu-id="4e874-143">Você não pode usar o alias para definir a configuração do SDK.</span><span class="sxs-lookup"><span data-stu-id="4e874-143">You can't use the alias to define the SDK configuration.</span></span>

<span data-ttu-id="4e874-144">Por exemplo: `capptain.deviceId` se torna `engagement.deviceId`, `capptain.agent.startActivity` se torna `engagement.agent.startActivity` e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="4e874-144">For instance, `capptain.deviceId` becomes `engagement.deviceId`, `capptain.agent.startActivity` becomes `engagement.agent.startActivity`, and so on.</span></span>

