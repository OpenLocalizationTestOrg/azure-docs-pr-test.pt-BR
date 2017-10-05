---
title: "Comportamento dos alertas por SMS em grupos de ação | Microsoft Docs"
description: Formato de mensagem SMS e como responder a mensagens SMS para cancelar a assinatura, assinar novamente ou solicitar ajuda.
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
ms.openlocfilehash: 3e4eca174209eeb9cbce1d45111d1e5cc30af8b0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="sms-alert-behavior-in-action-groups"></a><span data-ttu-id="b2bb3-103">Comportamento dos alertas por SMS em grupos de ação</span><span class="sxs-lookup"><span data-stu-id="b2bb3-103">SMS Alert Behavior in Action Groups</span></span>
## <a name="overview"></a><span data-ttu-id="b2bb3-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="b2bb3-104">Overview</span></span> ##
<span data-ttu-id="b2bb3-105">Os grupos de ações permitem configurar uma lista de destinatários.</span><span class="sxs-lookup"><span data-stu-id="b2bb3-105">Action groups enable you to configure a list of receivers.</span></span> <span data-ttu-id="b2bb3-106">Esses grupos podem, então, ser utilizados ao definir alertas de log de atividades, garantindo que um grupo de ação específico seja notificado quando o alerta de log de atividades for disparado.</span><span class="sxs-lookup"><span data-stu-id="b2bb3-106">These groups can then be leveraged when defining activity log alerts; ensuring that a particular action group is notified when the activity log alert is triggered.</span></span> <span data-ttu-id="b2bb3-107">Um dos mecanismos de alerta com suporte é o SMS; os alertas dão suporte à comunicação bidirecional.</span><span class="sxs-lookup"><span data-stu-id="b2bb3-107">One of the alerting mechanisms supported is SMS; the alerts support bi-directional communication.</span></span> <span data-ttu-id="b2bb3-108">Um usuário pode responder a um alerta para:</span><span class="sxs-lookup"><span data-stu-id="b2bb3-108">A user can respond to an alert to:</span></span>

- <span data-ttu-id="b2bb3-109">**Cancelar a assinatura de alertas:** um usuário pode cancelar a assinatura de todos os alertas por SMS de todos os grupos de ação ou de um grupo de ação individual.</span><span class="sxs-lookup"><span data-stu-id="b2bb3-109">**Unsubscribe from alerts:** A user can unsubscribe from all SMS alerts for all action groups, or a singular action group.</span></span>  
- <span data-ttu-id="b2bb3-110">**Assinar os alertas novamente:** um usuário pode assinar novamente todos os alertas por SMS de todos os grupos de ação ou de um grupo de ação individual.</span><span class="sxs-lookup"><span data-stu-id="b2bb3-110">**Resubscribe to alerts:** A user can resubscribe to all SMS alerts for all action groups, or a singular action group.</span></span>  
- <span data-ttu-id="b2bb3-111">**Solicitar ajuda:** um usuário pode solicitar mais informações sobre o SMS.</span><span class="sxs-lookup"><span data-stu-id="b2bb3-111">**Request help:** A user can ask for more information on the SMS.</span></span> <span data-ttu-id="b2bb3-112">Ele será redirecionado para este artigo</span><span class="sxs-lookup"><span data-stu-id="b2bb3-112">They will be redirected to this article</span></span>

<span data-ttu-id="b2bb3-113">Este artigo aborda o comportamento dos alertas por SMS e as ações de resposta que o usuário pode executar de acordo com a localidade do usuário:</span><span class="sxs-lookup"><span data-stu-id="b2bb3-113">This article covers the behavior of the SMS alerts and the response actions the user can take based on the locale of the user:</span></span>

## <a name="usacanada-sms-behavior"></a><span data-ttu-id="b2bb3-114">Comportamento de SMS nos EUA e no Canadá</span><span class="sxs-lookup"><span data-stu-id="b2bb3-114">USA/Canada SMS behavior</span></span>
### <a name="receiving-an-sms-alert"></a><span data-ttu-id="b2bb3-115">Recebendo um alerta por SMS</span><span class="sxs-lookup"><span data-stu-id="b2bb3-115">Receiving an SMS Alert</span></span>
<span data-ttu-id="b2bb3-116">Um receptor de SMS, configurado como parte de um grupo de ação, receberá um SMS quando um alerta for acionado.</span><span class="sxs-lookup"><span data-stu-id="b2bb3-116">An SMS receiver, who is configured as part of an action group, will receive an SMS when an alert fires.</span></span> <span data-ttu-id="b2bb3-117">O SMS trará as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="b2bb3-117">The SMS will carry the following information:</span></span>
* <span data-ttu-id="b2bb3-118">Nome curto do grupo de ação ao qual esse alerta foi enviado</span><span class="sxs-lookup"><span data-stu-id="b2bb3-118">Shortname of the action group this alert was sent to</span></span>
- <span data-ttu-id="b2bb3-119">Título do alerta</span><span class="sxs-lookup"><span data-stu-id="b2bb3-119">Title of the alert</span></span>

### <a name="unsubscribing-from-sms-alerts-for-one-action-group"></a><span data-ttu-id="b2bb3-120">Cancelando a assinatura de alertas por SMS de um grupo de ação</span><span class="sxs-lookup"><span data-stu-id="b2bb3-120">Unsubscribing from SMS alerts for one action group</span></span>
<span data-ttu-id="b2bb3-121">Um usuário pode cancelar a assinatura do SMS para alertas de um grupo de ação respondendo ao código curto 20873 com as palavras-chave: “DISABLE &lt;Nome curto do grupo de ação&gt;”.</span><span class="sxs-lookup"><span data-stu-id="b2bb3-121">A user can unsubscribe from SMS for alerts for one action group by responding to the shortcode 20873 with the keywords: “DISABLE &lt;Shortname of action group&gt;”.</span></span>

<span data-ttu-id="b2bb3-122">Ex.:</span><span class="sxs-lookup"><span data-stu-id="b2bb3-122">Ex.</span></span> <span data-ttu-id="b2bb3-123">Um usuário que deseja cancelar a assinatura dos alertas de um grupo de ação com o nome curto “Azure” enviará um SMS para o código curto 20873 que indica “DISABLE Azure”</span><span class="sxs-lookup"><span data-stu-id="b2bb3-123">A user wishing to unsubscribe from alerts for an action group with the shortname “Azure”, would send an SMS to the shortcode 20873 that says “DISABLE Azure”</span></span>

### <a name="unsubscribing-from-sms-alerts-for-all-action-groups"></a><span data-ttu-id="b2bb3-124">Cancelando a assinatura de alertas por SMS de todos os grupos de ação</span><span class="sxs-lookup"><span data-stu-id="b2bb3-124">Unsubscribing from SMS alerts for all action groups</span></span>
<span data-ttu-id="b2bb3-125">Um usuário pode cancelar a assinatura de todos os alertas por SMS de todos os grupos de ação respondendo ao código curto 20873 com uma das seguintes palavras-chave:</span><span class="sxs-lookup"><span data-stu-id="b2bb3-125">A user can unsubscribe from all SMS alerts for all action groups by responding to the shortcode 20873 with any of the following keywords:</span></span>
* <span data-ttu-id="b2bb3-126">STOP</span><span class="sxs-lookup"><span data-stu-id="b2bb3-126">STOP</span></span>

<span data-ttu-id="b2bb3-127">Ex.:</span><span class="sxs-lookup"><span data-stu-id="b2bb3-127">Ex.</span></span> <span data-ttu-id="b2bb3-128">Um usuário que deseja cancelar a assinatura de todos os alertas por SMS de todos os grupos de ação enviará um SMS para o código curto 20873 que indica “STOP”</span><span class="sxs-lookup"><span data-stu-id="b2bb3-128">A user wishing to unsubscribe from all SMS alerts for all action groups, would send an SMS to the shortcode 20873 that says “STOP”</span></span>

>[!NOTE]
><span data-ttu-id="b2bb3-129">Se um usuário tiver cancelado a assinatura de alertas por SMS, mas, em seguida, ele for adicionado a um novo grupo de ação, ele receberá alertas por SMS para esse novo grupo de ação, mas a assinatura de todos os grupos de ação anteriores permanecerá cancelada.</span><span class="sxs-lookup"><span data-stu-id="b2bb3-129">If a user has unsubscribed from SMS alerts, but is then added to a new action group; they WILL receive SMS alerts for that new action group, but remain unsubscribed from all previous action groups.</span></span>
>
>

### <a name="resubscribing-to-sms-alerts-for-one-action-group"></a><span data-ttu-id="b2bb3-130">Assinando novamente alertas por SMS de um grupo de ação</span><span class="sxs-lookup"><span data-stu-id="b2bb3-130">Resubscribing to SMS alerts for one action group</span></span>
<span data-ttu-id="b2bb3-131">Um usuário pode assinar o SMS novamente para receber alertas de um grupo de ação respondendo ao código curto 20873 com as palavras-chave: “ENABLE &lt;Nome curto do grupo de ação&gt;”.</span><span class="sxs-lookup"><span data-stu-id="b2bb3-131">A user can resubscribe to SMS for alerts for one action group by responding to the shortcode 20873 with the keywords: “ENABLE &lt;Shortname of action group&gt;”.</span></span>

<span data-ttu-id="b2bb3-132">Ex.:</span><span class="sxs-lookup"><span data-stu-id="b2bb3-132">Ex.</span></span> <span data-ttu-id="b2bb3-133">Um usuário que deseja assinar novamente os alertas de um grupo de ação com o nome curto “Azure” enviará um SMS para o código curto 20873 que indica “ENABLE Azure”</span><span class="sxs-lookup"><span data-stu-id="b2bb3-133">A user wishing to resubscribe to alerts for an action group with the shortname “Azure”, would send an SMS to the shortcode 20873 that says “ENABLE Azure”</span></span>

### <a name="resubscribing-to-sms-alerts-for-all-action-groups"></a><span data-ttu-id="b2bb3-134">Assinando novamente alertas por SMS de todos os grupos de ação</span><span class="sxs-lookup"><span data-stu-id="b2bb3-134">Resubscribing to SMS alerts for all action groups</span></span>
<span data-ttu-id="b2bb3-135">Um usuário pode assinar todos os SMS novamente para receber alertas de todos os grupos de ação respondendo ao código curto 20873 com uma das seguintes palavras-chave:</span><span class="sxs-lookup"><span data-stu-id="b2bb3-135">A user can resubscribe to all SMS for alerts for all action groups by responding to the shortcode 20873 with any of the following keywords:</span></span>

* <span data-ttu-id="b2bb3-136">START</span><span class="sxs-lookup"><span data-stu-id="b2bb3-136">START</span></span>

<span data-ttu-id="b2bb3-137">Ex.:</span><span class="sxs-lookup"><span data-stu-id="b2bb3-137">Ex.</span></span> <span data-ttu-id="b2bb3-138">Um usuário que deseja cancelar a assinatura de todos os alertas por SMS de todos os grupos de ação enviará um SMS para o código curto 20873 que indica “START”</span><span class="sxs-lookup"><span data-stu-id="b2bb3-138">A user wishing to unsubscribe from all SMS alerts for all action groups, would send an SMS to the shortcode 20873 that says “START”</span></span>

### <a name="requesting-help-via-sms"></a><span data-ttu-id="b2bb3-139">Solicitando ajuda por SMS</span><span class="sxs-lookup"><span data-stu-id="b2bb3-139">Requesting help via SMS</span></span>
<span data-ttu-id="b2bb3-140">Um usuário pode solicitar mais informações sobre o SMS que recebeu respondendo ao código curto 20873 com uma das seguintes palavras-chave:</span><span class="sxs-lookup"><span data-stu-id="b2bb3-140">A user can ask for more information about the SMS they have received by responding to the shortcode 20873 with any of the following keywords:</span></span>
* <span data-ttu-id="b2bb3-141">HELP</span><span class="sxs-lookup"><span data-stu-id="b2bb3-141">HELP</span></span>

<span data-ttu-id="b2bb3-142">Uma resposta será enviada para o usuário com um link para este artigo.</span><span class="sxs-lookup"><span data-stu-id="b2bb3-142">A response will be sent to the user with a link to this article.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b2bb3-143">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b2bb3-143">Next Steps</span></span>
<span data-ttu-id="b2bb3-144">Obtenha uma [visão geral dos alertas do log de atividades](monitoring-overview-alerts.md) e saiba como receber alertas</span><span class="sxs-lookup"><span data-stu-id="b2bb3-144">Get an [overview of activity log alerts](monitoring-overview-alerts.md) and learn how to get alerted</span></span>  
<span data-ttu-id="b2bb3-145">Saiba mais sobre a [limitação de taxa de SMS](monitoring-alerts-rate-limiting.md)</span><span class="sxs-lookup"><span data-stu-id="b2bb3-145">Learn more about [SMS rate limiting](monitoring-alerts-rate-limiting.md)</span></span>  
<span data-ttu-id="b2bb3-146">Saiba mais sobre [grupos de ação](monitoring-action-groups.md)</span><span class="sxs-lookup"><span data-stu-id="b2bb3-146">Learn more about [action groups](monitoring-action-groups.md)</span></span>
