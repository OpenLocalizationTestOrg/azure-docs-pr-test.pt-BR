---
title: "comportamento de alerta aaaSMS em grupos de ação | Microsoft Docs"
description: Formato de mensagem SMS e respondendo toounsubscribe tooSMS de mensagens, assinar novamente ou solicitar ajuda.
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: ancav
ms.openlocfilehash: 3cd09b1903e3472f6402f62b74409d97e7e7ea97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="sms-alert-behavior-in-action-groups"></a><span data-ttu-id="63d12-103">Comportamento dos alertas por SMS em grupos de ação</span><span class="sxs-lookup"><span data-stu-id="63d12-103">SMS Alert Behavior in Action Groups</span></span>
## <a name="overview"></a><span data-ttu-id="63d12-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="63d12-104">Overview</span></span> ##
<span data-ttu-id="63d12-105">Grupos de ação de habilitar tooconfigure uma lista de destinatários.</span><span class="sxs-lookup"><span data-stu-id="63d12-105">Action groups enable you tooconfigure a list of receivers.</span></span> <span data-ttu-id="63d12-106">Esses grupos podem ser aproveitados ao definir alertas de log de atividades; garantir que um grupo de ação em particular seja notificado quando hello atividade log alerta é disparado.</span><span class="sxs-lookup"><span data-stu-id="63d12-106">These groups can then be leveraged when defining activity log alerts; ensuring that a particular action group is notified when hello activity log alert is triggered.</span></span> <span data-ttu-id="63d12-107">Uma saudação suporte de mecanismos de alerta é SMS; alertas de saudação oferecem suporte a comunicação bidirecional.</span><span class="sxs-lookup"><span data-stu-id="63d12-107">One of hello alerting mechanisms supported is SMS; hello alerts support bi-directional communication.</span></span> <span data-ttu-id="63d12-108">Um usuário pode responder tooan do alerta:</span><span class="sxs-lookup"><span data-stu-id="63d12-108">A user can respond tooan alert to:</span></span>

- <span data-ttu-id="63d12-109">**Cancelar a assinatura de alertas:** um usuário pode cancelar a assinatura de todos os alertas por SMS de todos os grupos de ação ou de um grupo de ação individual.</span><span class="sxs-lookup"><span data-stu-id="63d12-109">**Unsubscribe from alerts:** A user can unsubscribe from all SMS alerts for all action groups, or a singular action group.</span></span>  
- <span data-ttu-id="63d12-110">**Assinar novamente tooalerts:** um usuário pode assinar novamente tooall alertas SMS para todos os grupos de ação ou um grupo de ação singular.</span><span class="sxs-lookup"><span data-stu-id="63d12-110">**Resubscribe tooalerts:** A user can resubscribe tooall SMS alerts for all action groups, or a singular action group.</span></span>  
- <span data-ttu-id="63d12-111">**Solicitar ajuda:** um usuário pode pedir para obter mais informações sobre Olá SMS.</span><span class="sxs-lookup"><span data-stu-id="63d12-111">**Request help:** A user can ask for more information on hello SMS.</span></span> <span data-ttu-id="63d12-112">Eles serão redirecionadas toothis artigo</span><span class="sxs-lookup"><span data-stu-id="63d12-112">They will be redirected toothis article</span></span>

<span data-ttu-id="63d12-113">Este artigo aborda o comportamento de saudação de alertas SMS hello e hello resposta ações Olá usuário pode executar com base na localidade de saudação do usuário hello:</span><span class="sxs-lookup"><span data-stu-id="63d12-113">This article covers hello behavior of hello SMS alerts and hello response actions hello user can take based on hello locale of hello user:</span></span>

## <a name="usacanada-sms-behavior"></a><span data-ttu-id="63d12-114">Comportamento de SMS nos EUA e no Canadá</span><span class="sxs-lookup"><span data-stu-id="63d12-114">USA/Canada SMS behavior</span></span>
### <a name="receiving-an-sms-alert"></a><span data-ttu-id="63d12-115">Recebendo um alerta por SMS</span><span class="sxs-lookup"><span data-stu-id="63d12-115">Receiving an SMS Alert</span></span>
<span data-ttu-id="63d12-116">Um receptor de SMS, configurado como parte de um grupo de ação, receberá um SMS quando um alerta for acionado.</span><span class="sxs-lookup"><span data-stu-id="63d12-116">An SMS receiver, who is configured as part of an action group, will receive an SMS when an alert fires.</span></span> <span data-ttu-id="63d12-117">Olá SMS realizará a saudação informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="63d12-117">hello SMS will carry hello following information:</span></span>
* <span data-ttu-id="63d12-118">Nome curto do grupo de ação Olá este alerta foi enviado para</span><span class="sxs-lookup"><span data-stu-id="63d12-118">Shortname of hello action group this alert was sent to</span></span>
- <span data-ttu-id="63d12-119">Título do alerta Olá</span><span class="sxs-lookup"><span data-stu-id="63d12-119">Title of hello alert</span></span>

### <a name="unsubscribing-from-sms-alerts-for-one-action-group"></a><span data-ttu-id="63d12-120">Cancelando a assinatura de alertas por SMS de um grupo de ação</span><span class="sxs-lookup"><span data-stu-id="63d12-120">Unsubscribing from SMS alerts for one action group</span></span>
<span data-ttu-id="63d12-121">Um usuário pode cancelar a assinatura do SMS para alertas para o grupo de uma ação por shortcode respondendo toohello 20873 com palavras-chave de saudação: "Desabilitar &lt;nome curto do grupo de ação&gt;".</span><span class="sxs-lookup"><span data-stu-id="63d12-121">A user can unsubscribe from SMS for alerts for one action group by responding toohello shortcode 20873 with hello keywords: “DISABLE &lt;Shortname of action group&gt;”.</span></span>

<span data-ttu-id="63d12-122">Ex.:</span><span class="sxs-lookup"><span data-stu-id="63d12-122">Ex.</span></span> <span data-ttu-id="63d12-123">Um usuário que toounsubscribe de alertas de um grupo com o nome curto do hello "Azure", poderia enviar um SMS toohello shortcode 20873 que diz "Desabilitar Azure"</span><span class="sxs-lookup"><span data-stu-id="63d12-123">A user wishing toounsubscribe from alerts for an action group with hello shortname “Azure”, would send an SMS toohello shortcode 20873 that says “DISABLE Azure”</span></span>

### <a name="unsubscribing-from-sms-alerts-for-all-action-groups"></a><span data-ttu-id="63d12-124">Cancelando a assinatura de alertas por SMS de todos os grupos de ação</span><span class="sxs-lookup"><span data-stu-id="63d12-124">Unsubscribing from SMS alerts for all action groups</span></span>
<span data-ttu-id="63d12-125">Um usuário pode cancelar a assinatura de todos os alertas SMS para todos os grupos de ação por shortcode respondendo toohello 20873 com qualquer um de saudação palavras-chave a seguir:</span><span class="sxs-lookup"><span data-stu-id="63d12-125">A user can unsubscribe from all SMS alerts for all action groups by responding toohello shortcode 20873 with any of hello following keywords:</span></span>
* <span data-ttu-id="63d12-126">STOP</span><span class="sxs-lookup"><span data-stu-id="63d12-126">STOP</span></span>

<span data-ttu-id="63d12-127">Ex.:</span><span class="sxs-lookup"><span data-stu-id="63d12-127">Ex.</span></span> <span data-ttu-id="63d12-128">Um usuário que toounsubscribe de todos os alertas SMS para todos os grupos de ação, poderia enviar um SMS toohello shortcode 20873 que diz "STOP"</span><span class="sxs-lookup"><span data-stu-id="63d12-128">A user wishing toounsubscribe from all SMS alerts for all action groups, would send an SMS toohello shortcode 20873 that says “STOP”</span></span>

>[!NOTE]
><span data-ttu-id="63d12-129">Se um usuário cancelou a assinatura de alertas SMS, mas é adicionado tooa novo grupo de ação. eles serão receber alertas SMS para esse novo grupo de ação, mas permanecem cancelados todos os grupos de ação anterior.</span><span class="sxs-lookup"><span data-stu-id="63d12-129">If a user has unsubscribed from SMS alerts, but is then added tooa new action group; they WILL receive SMS alerts for that new action group, but remain unsubscribed from all previous action groups.</span></span>
>
>

### <a name="resubscribing-toosms-alerts-for-one-action-group"></a><span data-ttu-id="63d12-130">Resubscribing tooSMS alertas para um grupo de ação</span><span class="sxs-lookup"><span data-stu-id="63d12-130">Resubscribing tooSMS alerts for one action group</span></span>
<span data-ttu-id="63d12-131">Um usuário pode assinar novamente tooSMS para alertas para o grupo de uma ação por shortcode respondendo toohello 20873 com palavras-chave de saudação: "habilitar &lt;nome curto do grupo de ação&gt;".</span><span class="sxs-lookup"><span data-stu-id="63d12-131">A user can resubscribe tooSMS for alerts for one action group by responding toohello shortcode 20873 with hello keywords: “ENABLE &lt;Shortname of action group&gt;”.</span></span>

<span data-ttu-id="63d12-132">Ex.:</span><span class="sxs-lookup"><span data-stu-id="63d12-132">Ex.</span></span> <span data-ttu-id="63d12-133">Um usuário que tooalerts tooresubscribe para um grupo de ação com o nome curto do hello "Azure", poderia enviar um SMS toohello shortcode 20873 que diz "Habilitar Azure"</span><span class="sxs-lookup"><span data-stu-id="63d12-133">A user wishing tooresubscribe tooalerts for an action group with hello shortname “Azure”, would send an SMS toohello shortcode 20873 that says “ENABLE Azure”</span></span>

### <a name="resubscribing-toosms-alerts-for-all-action-groups"></a><span data-ttu-id="63d12-134">Resubscribing tooSMS alertas para todos os grupos de ação</span><span class="sxs-lookup"><span data-stu-id="63d12-134">Resubscribing tooSMS alerts for all action groups</span></span>
<span data-ttu-id="63d12-135">Um usuário pode assinar novamente tooall SMS para alertas para todos os grupos de ação por shortcode respondendo toohello 20873 com qualquer um de saudação palavras-chave a seguir:</span><span class="sxs-lookup"><span data-stu-id="63d12-135">A user can resubscribe tooall SMS for alerts for all action groups by responding toohello shortcode 20873 with any of hello following keywords:</span></span>

* <span data-ttu-id="63d12-136">START</span><span class="sxs-lookup"><span data-stu-id="63d12-136">START</span></span>

<span data-ttu-id="63d12-137">Ex.:</span><span class="sxs-lookup"><span data-stu-id="63d12-137">Ex.</span></span> <span data-ttu-id="63d12-138">Um usuário que toounsubscribe de todos os alertas SMS para todos os grupos de ação, poderia enviar um SMS toohello shortcode 20873 que diz "Iniciar"</span><span class="sxs-lookup"><span data-stu-id="63d12-138">A user wishing toounsubscribe from all SMS alerts for all action groups, would send an SMS toohello shortcode 20873 that says “START”</span></span>

### <a name="requesting-help-via-sms"></a><span data-ttu-id="63d12-139">Solicitando ajuda por SMS</span><span class="sxs-lookup"><span data-stu-id="63d12-139">Requesting help via SMS</span></span>
<span data-ttu-id="63d12-140">Um usuário pode pedir para obter mais informações sobre Olá SMS recebeu por resposta toohello shortcode 20873 com qualquer Olá palavras-chave a seguir:</span><span class="sxs-lookup"><span data-stu-id="63d12-140">A user can ask for more information about hello SMS they have received by responding toohello shortcode 20873 with any of hello following keywords:</span></span>
* <span data-ttu-id="63d12-141">HELP</span><span class="sxs-lookup"><span data-stu-id="63d12-141">HELP</span></span>

<span data-ttu-id="63d12-142">Uma resposta será enviada toohello usuário com um artigo de toothis do link.</span><span class="sxs-lookup"><span data-stu-id="63d12-142">A response will be sent toohello user with a link toothis article.</span></span>

## <a name="next-steps"></a><span data-ttu-id="63d12-143">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="63d12-143">Next Steps</span></span>
<span data-ttu-id="63d12-144">Obter um [visão geral de alertas de log de atividade](monitoring-overview-alerts.md) e saiba como tooget alerta</span><span class="sxs-lookup"><span data-stu-id="63d12-144">Get an [overview of activity log alerts](monitoring-overview-alerts.md) and learn how tooget alerted</span></span>  
<span data-ttu-id="63d12-145">Saiba mais sobre a [limitação de taxa de SMS](monitoring-alerts-rate-limiting.md)</span><span class="sxs-lookup"><span data-stu-id="63d12-145">Learn more about [SMS rate limiting](monitoring-alerts-rate-limiting.md)</span></span>  
<span data-ttu-id="63d12-146">Saiba mais sobre [grupos de ação](monitoring-action-groups.md)</span><span class="sxs-lookup"><span data-stu-id="63d12-146">Learn more about [action groups](monitoring-action-groups.md)</span></span>
