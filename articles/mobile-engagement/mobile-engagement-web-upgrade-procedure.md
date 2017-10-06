---
title: "procedimentos de atualização de SDK do Mobile Engagement Web aaaAzure | Microsoft Docs"
description: "Olá procedimentos para Olá Web SDK e atualizações mais recentes para o Azure Mobile Engagement"
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
ms.openlocfilehash: a2df65904c6b56584ce6588ed26a9b79f3aa27ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-mobile-engagement-web-sdk-upgrade-procedures"></a><span data-ttu-id="d312f-103">Procedimentos de atualização do SDK para Web do Azure Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="d312f-103">Azure Mobile Engagement Web SDK upgrade procedures</span></span>
<span data-ttu-id="d312f-104">Se você já tiver integrado uma versão anterior do Olá Web SDK do Azure Mobile Engagement em seu aplicativo web, é necessário tooconsider Olá pontos a seguir quando você atualiza Olá SDK.</span><span class="sxs-lookup"><span data-stu-id="d312f-104">If you have already integrated an earlier version of hello Azure Mobile Engagement Web SDK into your web application, you need tooconsider hello following points when you upgrade hello SDK.</span></span>

<span data-ttu-id="d312f-105">Se você tiver ignorado a várias versões de Olá Web SDK do Mobile Engagement, talvez seja necessário toocomplete vários procedimentos durante o processo de atualização de saudação.</span><span class="sxs-lookup"><span data-stu-id="d312f-105">If you skipped multiple versions of hello Mobile Engagement Web SDK, you might need toocomplete several procedures during hello upgrade process.</span></span> <span data-ttu-id="d312f-106">Por exemplo, se você migrar de 1.4.0 too1.6.0, primeiro execute Olá procedimentos tooupgrade de 1.4.0 too1.5.0.</span><span class="sxs-lookup"><span data-stu-id="d312f-106">For example, if you migrate from 1.4.0 too1.6.0, first follow hello procedures tooupgrade from 1.4.0 too1.5.0.</span></span> <span data-ttu-id="d312f-107">Em seguida, siga Olá procedimentos tooupgrade de 1.5.0 too1.6.0.</span><span class="sxs-lookup"><span data-stu-id="d312f-107">Then, follow hello procedures tooupgrade from 1.5.0 too1.6.0.</span></span>

<span data-ttu-id="d312f-108">Qualquer versão de atualização, substitua qualquer versão anterior do arquivo de saudação do azure-engagement.js a versão mais recente de saudação do arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="d312f-108">Whichever version you upgrade from, replace any earlier version of hello file azure-engagement.js with hello latest version of hello file.</span></span>

## <a name="upgrade-from-121-too200"></a><span data-ttu-id="d312f-109">Atualização do 1.2.1 too2.0.0</span><span class="sxs-lookup"><span data-stu-id="d312f-109">Upgrade from 1.2.1 too2.0.0</span></span>
<span data-ttu-id="d312f-110">Esta seção descreve como toomigrate uma integração do SDK do Mobile Engagement Web do serviço de Capptain hello, oferecido pelo Capptain SAS, aplicativo do Azure Mobile Engagement tooan.</span><span class="sxs-lookup"><span data-stu-id="d312f-110">This section describes how toomigrate a Mobile Engagement Web SDK integration from hello Capptain service, offered by Capptain SAS, tooan Azure Mobile Engagement app.</span></span> <span data-ttu-id="d312f-111">Se você estiver migrando de uma versão anterior, por favor consulte Olá Capptain site toofirst migrar too1.2.1 e, em seguida, aplicar Olá procedimentos a seguir.</span><span class="sxs-lookup"><span data-stu-id="d312f-111">If you are migrating from an earlier version, please consult hello Capptain website toofirst migrate too1.2.1, and then apply hello following procedures.</span></span>

<span data-ttu-id="d312f-112">Não dá suporte a esta versão do Olá Web SDK do Mobile Engagement Samsung Smart TV, Opera TV, webOS ou recurso de alcance hello.</span><span class="sxs-lookup"><span data-stu-id="d312f-112">This version of hello Mobile Engagement Web SDK doesn't support Samsung Smart TV, Opera TV, webOS, or hello Reach feature.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d312f-113">Capptain e do Azure Mobile Engagement não são Olá mesmo serviço.</span><span class="sxs-lookup"><span data-stu-id="d312f-113">Capptain and Azure Mobile Engagement are not hello same service.</span></span> <span data-ttu-id="d312f-114">Olá procedimento a seguir realça apenas como toomigrate Olá aplicativo cliente.</span><span class="sxs-lookup"><span data-stu-id="d312f-114">hello following procedure highlights only how toomigrate hello client app.</span></span> <span data-ttu-id="d312f-115">Migrando Olá Web SDK do Mobile Engagement no aplicativo hello não serão migrados para os dados de um Capptain tooa Mobile Engagement server.</span><span class="sxs-lookup"><span data-stu-id="d312f-115">Migrating hello Mobile Engagement Web SDK in hello app will not migrate your data from a Capptain server tooa Mobile Engagement server.</span></span>
> 
> 

### <a name="javascript-files"></a><span data-ttu-id="d312f-116">Arquivos JavaScript</span><span class="sxs-lookup"><span data-stu-id="d312f-116">JavaScript files</span></span>
<span data-ttu-id="d312f-117">Substitua saudação de arquivo capptain-sdk.js com o arquivo de saudação do azure-engagement.js e atualize seu script importa adequadamente.</span><span class="sxs-lookup"><span data-stu-id="d312f-117">Replace hello file capptain-sdk.js with hello file azure-engagement.js, and then update your script imports accordingly.</span></span>

### <a name="remove-capptain-reach"></a><span data-ttu-id="d312f-118">Remover o Capptain Reach</span><span class="sxs-lookup"><span data-stu-id="d312f-118">Remove Capptain Reach</span></span>
<span data-ttu-id="d312f-119">Esta versão do Olá Web SDK do Mobile Engagement não dá suporte a recurso de alcance hello.</span><span class="sxs-lookup"><span data-stu-id="d312f-119">This version of hello Mobile Engagement Web SDK doesn't support hello Reach feature.</span></span> <span data-ttu-id="d312f-120">Se você tiver integrado Capptain alcance em seu aplicativo, você precisa tooremove-lo.</span><span class="sxs-lookup"><span data-stu-id="d312f-120">If you integrated Capptain Reach into your application, you need tooremove it.</span></span>

<span data-ttu-id="d312f-121">Remover Olá alcançar CSS importar sua página e excluir o arquivo. CSS relacionados de saudação (capptain-reach.css, por padrão).</span><span class="sxs-lookup"><span data-stu-id="d312f-121">Remove hello Reach CSS import from your page and delete hello related .css file (capptain-reach.css, by default).</span></span>

<span data-ttu-id="d312f-122">Excluir Olá alcance recursos a seguir: Olá fechar imagem (capptain-close.png, por padrão) e o ícone de marca de saudação (capptain--ícone de notificação, por padrão).</span><span class="sxs-lookup"><span data-stu-id="d312f-122">Delete hello following Reach resources: hello close image (capptain-close.png, by default) and hello brand icon (capptain-notification-icon, by default).</span></span>

<span data-ttu-id="d312f-123">Remova hello alcançar da interface do usuário para notificações no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d312f-123">Remove hello Reach UI for in-app notifications.</span></span> <span data-ttu-id="d312f-124">layout da saudação padrão tem esta aparência:</span><span class="sxs-lookup"><span data-stu-id="d312f-124">hello default layout looks like this:</span></span>

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

<span data-ttu-id="d312f-125">Remova Olá alcançar da interface do usuário para notificações de texto e da web e pesquisas.</span><span class="sxs-lookup"><span data-stu-id="d312f-125">Remove hello Reach UI for text and web announcements and polls.</span></span> <span data-ttu-id="d312f-126">layout da saudação padrão tem esta aparência:</span><span class="sxs-lookup"><span data-stu-id="d312f-126">hello default layout looks like this:</span></span>

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

<span data-ttu-id="d312f-127">Remover Olá `reach` do objeto de configuração, se ele existir.</span><span class="sxs-lookup"><span data-stu-id="d312f-127">Remove hello `reach` object from your configuration, if it exists.</span></span> <span data-ttu-id="d312f-128">Ele tem esta aparência:</span><span class="sxs-lookup"><span data-stu-id="d312f-128">It looks like this:</span></span>

    window.capptain = {
      [...]
      reach: {
        [...]
      }
    }

<span data-ttu-id="d312f-129">Remova qualquer outra personalização do Reach, como categorias.</span><span class="sxs-lookup"><span data-stu-id="d312f-129">Remove any other Reach customization, such as categories.</span></span>

### <a name="remove-deprecated-apis"></a><span data-ttu-id="d312f-130">Remover APIs substituídas</span><span class="sxs-lookup"><span data-stu-id="d312f-130">Remove deprecated APIs</span></span>
<span data-ttu-id="d312f-131">Algumas APIs de Capptain são preteridos no Olá Web SDK do Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="d312f-131">Some APIs from Capptain are deprecated in hello Mobile Engagement Web SDK.</span></span>

<span data-ttu-id="d312f-132">Remova qualquer toohello chamadas seguintes APIs: `agent.connect`, `agent.disconnect`, `agent.pause`, e `agent.sendMessageToDevice`.</span><span class="sxs-lookup"><span data-stu-id="d312f-132">Remove any calls toohello following APIs: `agent.connect`, `agent.disconnect`, `agent.pause`, and `agent.sendMessageToDevice`.</span></span>

<span data-ttu-id="d312f-133">Remover todas as instâncias de saudação retornos de chamada a seguir da configuração do seu Capptain: `onConnected`, `onDisconnected`, `onDeviceMessageReceived`, e `onPushMessageReceived`.</span><span class="sxs-lookup"><span data-stu-id="d312f-133">Remove any instances of hello following callbacks from your Capptain configuration: `onConnected`, `onDisconnected`, `onDeviceMessageReceived`, and `onPushMessageReceived`.</span></span>

### <a name="configuration"></a><span data-ttu-id="d312f-134">Configuração</span><span class="sxs-lookup"><span data-stu-id="d312f-134">Configuration</span></span>
<span data-ttu-id="d312f-135">Mobile Engagement usa uma conexão cadeia de caracteres tooconfigure SDK os identificadores, por exemplo, o identificador de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="d312f-135">Mobile Engagement uses a connection string tooconfigure SDK identifiers, for example, hello application identifier.</span></span>

<span data-ttu-id="d312f-136">Substitua a ID do aplicativo de saudação com a cadeia de caracteres de conexão.</span><span class="sxs-lookup"><span data-stu-id="d312f-136">Replace hello application ID with your connection string.</span></span> <span data-ttu-id="d312f-137">Observe o objeto global Olá de saudação configuração SDK é alterado de `capptain` muito`azureEngagement`.</span><span class="sxs-lookup"><span data-stu-id="d312f-137">Note that hello global object for hello SDK configuration changes from `capptain` too`azureEngagement`.</span></span>

<span data-ttu-id="d312f-138">Antes da migração:</span><span class="sxs-lookup"><span data-stu-id="d312f-138">Before migration:</span></span>

    window.capptain = {
      appId: ...,
      [...]
    };

<span data-ttu-id="d312f-139">Após a migração:</span><span class="sxs-lookup"><span data-stu-id="d312f-139">After migration:</span></span>

    window.azureEngagement = {
      connectionString: 'Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}',
      [...]
    };

<span data-ttu-id="d312f-140">cadeia de caracteres de conexão de saudação para seu aplicativo é exibida no hello Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="d312f-140">hello connection string for your application is displayed in hello Azure Portal.</span></span>

### <a name="javascript-apis"></a><span data-ttu-id="d312f-141">APIs do JavaScript</span><span class="sxs-lookup"><span data-stu-id="d312f-141">JavaScript APIs</span></span>
<span data-ttu-id="d312f-142">objeto de JavaScript global Olá `window.capptain` foi renomeado `window.azureEngagement` , mas você pode usar o hello `window.engagement` alias para chamadas de API.</span><span class="sxs-lookup"><span data-stu-id="d312f-142">hello global JavaScript object `window.capptain` has been renamed `window.azureEngagement` but you can use hello `window.engagement` alias for API calls.</span></span> <span data-ttu-id="d312f-143">Você não pode usar a configuração do SDK do hello alias toodefine hello.</span><span class="sxs-lookup"><span data-stu-id="d312f-143">You can't use hello alias toodefine hello SDK configuration.</span></span>

<span data-ttu-id="d312f-144">Por exemplo: `capptain.deviceId` se torna `engagement.deviceId`, `capptain.agent.startActivity` se torna `engagement.agent.startActivity` e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="d312f-144">For instance, `capptain.deviceId` becomes `engagement.deviceId`, `capptain.agent.startActivity` becomes `engagement.agent.startActivity`, and so on.</span></span>

