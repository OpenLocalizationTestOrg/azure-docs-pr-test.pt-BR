---
title: "Visão geral do Mobile Engagement Web SDK do aaaAzure | Microsoft Docs"
description: "Olá procedimentos para Olá Web SDK e atualizações mais recentes para o Azure Mobile Engagement"
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
ms.openlocfilehash: 9e60a232b5eb2c41c405041a88e09d7137563513
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-mobile-engagement-web-sdk"></a><span data-ttu-id="a50c7-103">SDK Web do Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="a50c7-103">Azure Mobile Engagement Web SDK</span></span>
<span data-ttu-id="a50c7-104">Comece aqui para todos os detalhes sobre como de hello toointegrate do Azure Mobile Engagement em um aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="a50c7-104">Start here for all hello details about how toointegrate Azure Mobile Engagement in a web app.</span></span> <span data-ttu-id="a50c7-105">Se você quiser toogive-lo um bloco try antes da introdução com seu próprio aplicativo web, consulte nosso [tutorial de 15 minutos](mobile-engagement-web-app-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="a50c7-105">If you'd like toogive it a try before getting started with your own web app, see our [15-minute tutorial](mobile-engagement-web-app-get-started.md).</span></span>

## <a name="integration-procedures"></a><span data-ttu-id="a50c7-106">Procedimentos de integração</span><span class="sxs-lookup"><span data-stu-id="a50c7-106">Integration procedures</span></span>
1. <span data-ttu-id="a50c7-107">Saiba [como toointegrate Mobile Engagement em seu aplicativo web](mobile-engagement-web-integrate-engagement.md).</span><span class="sxs-lookup"><span data-stu-id="a50c7-107">Learn [how toointegrate Mobile Engagement in your web app](mobile-engagement-web-integrate-engagement.md).</span></span>
2. <span data-ttu-id="a50c7-108">Para a implementação do plano de marca, saiba [como toouse Olá avançado marcação API em seu aplicativo web do Mobile Engagement](mobile-engagement-web-use-engagement-api.md).</span><span class="sxs-lookup"><span data-stu-id="a50c7-108">For tag plan implementation, learn [how toouse hello advanced Mobile Engagement tagging API in your web app](mobile-engagement-web-use-engagement-api.md).</span></span>

## <a name="release-notes"></a><span data-ttu-id="a50c7-109">Notas de versão</span><span class="sxs-lookup"><span data-stu-id="a50c7-109">Release notes</span></span>
### <a name="202-10182016"></a><span data-ttu-id="a50c7-110">2.0.2 (18/10/2016)</span><span class="sxs-lookup"><span data-stu-id="a50c7-110">2.0.2 (10/18/2016)</span></span>
* <span data-ttu-id="a50c7-111">Falha corrigida na navegação particular (Safari).</span><span class="sxs-lookup"><span data-stu-id="a50c7-111">Fixed crash on private browsing (Safari).</span></span>
* <span data-ttu-id="a50c7-112">Falha corrigida em navegadores com cookies desabilitados.</span><span class="sxs-lookup"><span data-stu-id="a50c7-112">Fixed crash on browsers with cookies disabled.</span></span>

<span data-ttu-id="a50c7-113">Para todas as versões, consulte Olá [concluir notas de versão](mobile-engagement-web-release-notes.md).</span><span class="sxs-lookup"><span data-stu-id="a50c7-113">For all versions, please see hello [complete release notes](mobile-engagement-web-release-notes.md).</span></span>

## <a name="upgrade-procedures"></a><span data-ttu-id="a50c7-114">Procedimentos de atualização</span><span class="sxs-lookup"><span data-stu-id="a50c7-114">Upgrade procedures</span></span>
### <a name="upgrade-from-121-too200"></a><span data-ttu-id="a50c7-115">Atualização do 1.2.1 too2.0.0</span><span class="sxs-lookup"><span data-stu-id="a50c7-115">Upgrade from 1.2.1 too2.0.0</span></span>
<span data-ttu-id="a50c7-116">Olá seções a seguir descrevem como toomigrate uma integração do SDK do Mobile Engagement Web do serviço de Capptain hello, oferecido pelo Capptain SAS, aplicativo do Azure Mobile Engagement tooan.</span><span class="sxs-lookup"><span data-stu-id="a50c7-116">hello following sections describe how toomigrate a Mobile Engagement Web SDK integration from hello Capptain service, offered by Capptain SAS, tooan Azure Mobile Engagement app.</span></span> <span data-ttu-id="a50c7-117">Se você estiver migrando de uma versão anterior que 1.2.1, consulte Olá Capptain site toomigrate too1.2.1 pela primeira vez e aplique Olá procedimentos a seguir.</span><span class="sxs-lookup"><span data-stu-id="a50c7-117">If you are migrating from a version earlier than 1.2.1, please consult hello Capptain website toomigrate too1.2.1 first, and then apply hello following procedures.</span></span>

<span data-ttu-id="a50c7-118">Não dá suporte a esta versão do Olá Web SDK do Mobile Engagement Samsung Smart TV, Opera TV, webOS ou recurso de alcance hello.</span><span class="sxs-lookup"><span data-stu-id="a50c7-118">This version of hello Mobile Engagement Web SDK doesn't support Samsung Smart TV, Opera TV, webOS, or hello Reach feature.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a50c7-119">Capptain e do Azure Mobile Engagement não são Olá mesmo serviço e Olá procedimentos realce apenas como toomigrate Olá aplicativo cliente.</span><span class="sxs-lookup"><span data-stu-id="a50c7-119">Capptain and Azure Mobile Engagement are not hello same service, and hello following procedures highlight only how toomigrate hello client app.</span></span> <span data-ttu-id="a50c7-120">Migrando Olá Web SDK do Mobile Engagement no aplicativo hello não serão migrados para os dados de um Capptain tooa Mobile Engagement server.</span><span class="sxs-lookup"><span data-stu-id="a50c7-120">Migrating hello Mobile Engagement Web SDK in hello app will not migrate your data from a Capptain server tooa Mobile Engagement server.</span></span>
> 
> 

#### <a name="javascript-files"></a><span data-ttu-id="a50c7-121">Arquivos JavaScript</span><span class="sxs-lookup"><span data-stu-id="a50c7-121">JavaScript files</span></span>
<span data-ttu-id="a50c7-122">Substitua saudação de arquivo capptain-sdk.js com o arquivo de saudação do azure-engagement.js e atualize seu script importa adequadamente.</span><span class="sxs-lookup"><span data-stu-id="a50c7-122">Replace hello file capptain-sdk.js with hello file azure-engagement.js, and then update your script imports accordingly.</span></span>

#### <a name="remove-capptain-reach"></a><span data-ttu-id="a50c7-123">Remover o Capptain Reach</span><span class="sxs-lookup"><span data-stu-id="a50c7-123">Remove Capptain Reach</span></span>
<span data-ttu-id="a50c7-124">Esta versão do Olá Web SDK do Mobile Engagement não dá suporte a recurso de alcance hello.</span><span class="sxs-lookup"><span data-stu-id="a50c7-124">This version of hello Mobile Engagement Web SDK doesn't support hello Reach feature.</span></span> <span data-ttu-id="a50c7-125">Se você tiver integrado o alcance de Capptain em seu aplicativo, você precisa tooremove-lo.</span><span class="sxs-lookup"><span data-stu-id="a50c7-125">If you have integrated Capptain Reach into your application, you need tooremove it.</span></span>

<span data-ttu-id="a50c7-126">Remover Olá alcançar CSS importar sua página e excluir o arquivo. CSS relacionados de saudação (capptain-reach.css, por padrão).</span><span class="sxs-lookup"><span data-stu-id="a50c7-126">Remove hello Reach CSS import from your page and delete hello related .css file (capptain-reach.css, by default).</span></span>

<span data-ttu-id="a50c7-127">Excluir Olá alcance recursos a seguir: Olá fechar imagem (capptain-close.png, por padrão) e o ícone de marca de saudação (capptain--ícone de notificação, por padrão).</span><span class="sxs-lookup"><span data-stu-id="a50c7-127">Delete hello following Reach resources: hello close image (capptain-close.png, by default) and hello brand icon (capptain-notification-icon, by default).</span></span>

<span data-ttu-id="a50c7-128">Remova hello alcançar da interface do usuário para notificações no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a50c7-128">Remove hello Reach UI for in-app notifications.</span></span> <span data-ttu-id="a50c7-129">layout da saudação padrão tem esta aparência:</span><span class="sxs-lookup"><span data-stu-id="a50c7-129">hello default layout looks like this:</span></span>

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

<span data-ttu-id="a50c7-130">Remova Olá alcançar da interface do usuário para notificações de texto e da web e pesquisas.</span><span class="sxs-lookup"><span data-stu-id="a50c7-130">Remove hello Reach UI for text and web announcements and polls.</span></span> <span data-ttu-id="a50c7-131">layout da saudação padrão tem esta aparência:</span><span class="sxs-lookup"><span data-stu-id="a50c7-131">hello default layout looks like this:</span></span>

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

<span data-ttu-id="a50c7-132">Remover Olá `reach` do objeto de configuração, se ele existir.</span><span class="sxs-lookup"><span data-stu-id="a50c7-132">Remove hello `reach` object from your configuration, if it exists.</span></span> <span data-ttu-id="a50c7-133">Ele tem esta aparência:</span><span class="sxs-lookup"><span data-stu-id="a50c7-133">It looks like this:</span></span>

    window.capptain = {
      [...]
      reach: {
        [...]
      }
    }

<span data-ttu-id="a50c7-134">Remova qualquer outra personalização do Reach, como categorias.</span><span class="sxs-lookup"><span data-stu-id="a50c7-134">Remove any other Reach customization, such as categories.</span></span>

#### <a name="remove-deprecated-apis"></a><span data-ttu-id="a50c7-135">Remover APIs substituídas</span><span class="sxs-lookup"><span data-stu-id="a50c7-135">Remove deprecated APIs</span></span>
<span data-ttu-id="a50c7-136">Algumas APIs de Capptain são preteridos no Olá Web SDK do Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="a50c7-136">Some APIs from Capptain are deprecated in hello Mobile Engagement Web SDK.</span></span>

<span data-ttu-id="a50c7-137">Remova qualquer toohello chamadas seguintes APIs: `agent.connect`, `agent.disconnect`, `agent.pause`, e `agent.sendMessageToDevice`.</span><span class="sxs-lookup"><span data-stu-id="a50c7-137">Remove any calls toohello following APIs: `agent.connect`, `agent.disconnect`, `agent.pause`, and `agent.sendMessageToDevice`.</span></span>

<span data-ttu-id="a50c7-138">Remova qualquer Olá retornos de chamada a seguir da configuração do seu Capptain: `onConnected`, `onDisconnected`, `onDeviceMessageReceived`, e `onPushMessageReceived`.</span><span class="sxs-lookup"><span data-stu-id="a50c7-138">Remove any of hello following callbacks from your Capptain configuration: `onConnected`, `onDisconnected`, `onDeviceMessageReceived`, and `onPushMessageReceived`.</span></span>

#### <a name="configuration"></a><span data-ttu-id="a50c7-139">Configuração</span><span class="sxs-lookup"><span data-stu-id="a50c7-139">Configuration</span></span>
<span data-ttu-id="a50c7-140">Mobile Engagement usa uma conexão cadeia de caracteres tooconfigure SDK os identificadores, por exemplo, o identificador de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="a50c7-140">Mobile Engagement uses a connection string tooconfigure SDK identifiers, for example, hello application identifier.</span></span>

<span data-ttu-id="a50c7-141">Substitua a ID do aplicativo de saudação com a cadeia de caracteres de conexão.</span><span class="sxs-lookup"><span data-stu-id="a50c7-141">Replace hello application ID with your connection string.</span></span> <span data-ttu-id="a50c7-142">Observe o objeto global Olá de saudação configuração SDK é alterado de `capptain` muito`azureEngagement`.</span><span class="sxs-lookup"><span data-stu-id="a50c7-142">Note that hello global object for hello SDK configuration changes from `capptain` too`azureEngagement`.</span></span>

<span data-ttu-id="a50c7-143">Antes da migração:</span><span class="sxs-lookup"><span data-stu-id="a50c7-143">Before migration:</span></span>

    window.capptain = {
      appId: ...,
      [...]
    };

<span data-ttu-id="a50c7-144">Após a migração:</span><span class="sxs-lookup"><span data-stu-id="a50c7-144">After migration:</span></span>

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      [...]
    };

<span data-ttu-id="a50c7-145">cadeia de caracteres de conexão de saudação para seu aplicativo é exibida no portal do Azure de saudação.</span><span class="sxs-lookup"><span data-stu-id="a50c7-145">hello connection string for your application is displayed in hello Azure portal.</span></span>

#### <a name="javascript-apis"></a><span data-ttu-id="a50c7-146">APIs do JavaScript</span><span class="sxs-lookup"><span data-stu-id="a50c7-146">JavaScript APIs</span></span>
<span data-ttu-id="a50c7-147">objeto de JavaScript global Olá `window.capptain` foi renomeado `window.azureEngagement`, mas você pode usar o hello `window.engagement` alias para chamadas de API.</span><span class="sxs-lookup"><span data-stu-id="a50c7-147">hello global JavaScript object `window.capptain` has been renamed `window.azureEngagement`, but you can use hello `window.engagement` alias for API calls.</span></span> <span data-ttu-id="a50c7-148">Você não pode usar essa configuração de SDK do alias toodefine hello.</span><span class="sxs-lookup"><span data-stu-id="a50c7-148">You can't use this alias toodefine hello SDK configuration.</span></span>

<span data-ttu-id="a50c7-149">Por exemplo: `capptain.deviceId` se torna `engagement.deviceId`, `capptain.agent.startActivity` se torna `engagement.agent.startActivity` e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="a50c7-149">For instance, `capptain.deviceId` becomes `engagement.deviceId`, `capptain.agent.startActivity` becomes `engagement.agent.startActivity`, and so on.</span></span>

<span data-ttu-id="a50c7-150">Se você já tiver integrado uma versão anterior do Olá Web SDK do Azure Mobile Engagement em seu aplicativo, leia sobre [atualizar procedimentos](mobile-engagement-web-upgrade-procedure.md).</span><span class="sxs-lookup"><span data-stu-id="a50c7-150">If you have already integrated an earlier version of hello Azure Mobile Engagement Web SDK into your application, please read about [upgrade procedures](mobile-engagement-web-upgrade-procedure.md).</span></span>

