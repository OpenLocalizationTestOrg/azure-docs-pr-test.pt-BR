---
title: "Limitação de taxa para SMS, emails e webhooks | Microsoft Docs"
description: "Entenda como o Azure limita o número de notificações possíveis de webhook, email ou SMS de um grupo de ações."
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
ms.openlocfilehash: bde645624ab1860d19ba18470f55845855a7d1fb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="rate-limiting-for-sms-messages-emails-and-webhook-posts"></a><span data-ttu-id="3d0e6-103">Taxa de limitação mensagens SMS, emails e postagens de webhook postagens</span><span class="sxs-lookup"><span data-stu-id="3d0e6-103">Rate limiting for SMS messages, emails, and webhook posts</span></span>
<span data-ttu-id="3d0e6-104">A limitação de taxa é uma suspensão de notificações que ocorre quando um excesso de notificações é enviado para determinado número de telefone ou endereço de email.</span><span class="sxs-lookup"><span data-stu-id="3d0e6-104">Rate limiting is a suspension of notifications that occurs when too many notifications are sent to a particular phone number or email address.</span></span> <span data-ttu-id="3d0e6-105">A limitação de taxa assegura que os alertas sejam gerenciáveis e acionáveis.</span><span class="sxs-lookup"><span data-stu-id="3d0e6-105">Rate limiting ensures that alerts are manageable and actionable.</span></span>

<span data-ttu-id="3d0e6-106">As regras de SMS e Email são iguais.</span><span class="sxs-lookup"><span data-stu-id="3d0e6-106">The rules for SMS and email are the same.</span></span> <span data-ttu-id="3d0e6-107">O limite de taxa é:</span><span class="sxs-lookup"><span data-stu-id="3d0e6-107">The rate limit threshold is:</span></span>

 - <span data-ttu-id="3d0e6-108">**SMS**: 10 mensagens em uma hora.</span><span class="sxs-lookup"><span data-stu-id="3d0e6-108">**SMS**: 10 messages in an hour.</span></span>
 - <span data-ttu-id="3d0e6-109">**Email**: 100 mensagens em uma hora.</span><span class="sxs-lookup"><span data-stu-id="3d0e6-109">**Email**: 100 messages in an hour.</span></span>

## <a name="rate-limit-rules"></a><span data-ttu-id="3d0e6-110">Regras do limite de taxa</span><span class="sxs-lookup"><span data-stu-id="3d0e6-110">Rate limit rules</span></span>
- <span data-ttu-id="3d0e6-111">Um número de telefone ou email específico tem um limite de taxa imposto quando recebe mais mensagens do que o limite permite.</span><span class="sxs-lookup"><span data-stu-id="3d0e6-111">A particular phone number or email is rate limited when it receives more messages than the threshold allows.</span></span>
- <span data-ttu-id="3d0e6-112">Um número de telefone ou email pode fazer parte de grupos de ações em várias assinaturas.</span><span class="sxs-lookup"><span data-stu-id="3d0e6-112">A phone number or email can be part of action groups across many subscriptions.</span></span> <span data-ttu-id="3d0e6-113">A limitação de taxa aplica-se a todas as assinaturas.</span><span class="sxs-lookup"><span data-stu-id="3d0e6-113">Rate limiting applies across all subscriptions.</span></span> <span data-ttu-id="3d0e6-114">Ela se aplica assim que o limite é atingido, mesmo se as mensagens forem enviadas de várias assinaturas.</span><span class="sxs-lookup"><span data-stu-id="3d0e6-114">It applies as soon as the threshold is reached, even if messages are sent from multiple subscriptions.</span></span>  
- <span data-ttu-id="3d0e6-115">Quando um número de telefone ou email tem uma limitação de taxa, uma notificação adicional é enviada para comunicar a limitação de taxa.</span><span class="sxs-lookup"><span data-stu-id="3d0e6-115">When a phone number or email is rate limited, an additional notification is sent to communicate the rate limiting.</span></span> <span data-ttu-id="3d0e6-116">A notificação indica quando a limitação de taxa expira.</span><span class="sxs-lookup"><span data-stu-id="3d0e6-116">The notification states when the rate limiting expires.</span></span>

## <a name="rate-limit-of-webhooks"></a><span data-ttu-id="3d0e6-117">Limite de taxa de webhooks</span><span class="sxs-lookup"><span data-stu-id="3d0e6-117">Rate limit of webhooks</span></span> ##
<span data-ttu-id="3d0e6-118">Não há nenhuma limitação de taxa em vigor para webhooks.</span><span class="sxs-lookup"><span data-stu-id="3d0e6-118">There is no rate limiting in place for webhooks.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3d0e6-119">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3d0e6-119">Next steps</span></span> ##
* <span data-ttu-id="3d0e6-120">Saiba mais sobre o [comportamento de alertas por SMS](monitoring-sms-alert-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="3d0e6-120">Learn more about [SMS alert behavior](monitoring-sms-alert-behavior.md).</span></span>
* <span data-ttu-id="3d0e6-121">Obtenha uma [visão geral dos alertas do log de atividades](monitoring-overview-alerts.md) e saiba como receber alertas.</span><span class="sxs-lookup"><span data-stu-id="3d0e6-121">Get an [overview of activity log alerts](monitoring-overview-alerts.md), and learn how to receive alerts.</span></span>  
* <span data-ttu-id="3d0e6-122">Saiba como [configurar alertas sempre que uma notificação de integridade do serviço é postada](monitoring-activity-log-alerts-on-service-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="3d0e6-122">Learn how to [configure alerts whenever a service health notification is posted](monitoring-activity-log-alerts-on-service-notifications.md).</span></span>
