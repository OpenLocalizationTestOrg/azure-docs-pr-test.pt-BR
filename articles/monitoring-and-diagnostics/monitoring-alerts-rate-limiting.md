---
title: "limitação de aaaRate para SMS, emails e webhooks | Microsoft Docs"
description: "Entenda como o Azure limita o número de saudação de notificações possíveis de webhook, e-mail ou SMS de um grupo de ação."
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
ms.openlocfilehash: 1cd08a5b982c82bb02e0bf93451aa1fcd9bc34af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="rate-limiting-for-sms-messages-emails-and-webhook-posts"></a><span data-ttu-id="eb8c4-103">Taxa de limitação mensagens SMS, emails e postagens de webhook postagens</span><span class="sxs-lookup"><span data-stu-id="eb8c4-103">Rate limiting for SMS messages, emails, and webhook posts</span></span>
<span data-ttu-id="eb8c4-104">A limitação de taxa é uma suspensão de notificações que ocorre quando há muitos notificações são enviadas a endereços de email ou número de telefone específico tooa.</span><span class="sxs-lookup"><span data-stu-id="eb8c4-104">Rate limiting is a suspension of notifications that occurs when too many notifications are sent tooa particular phone number or email address.</span></span> <span data-ttu-id="eb8c4-105">A limitação de taxa assegura que os alertas sejam gerenciáveis e acionáveis.</span><span class="sxs-lookup"><span data-stu-id="eb8c4-105">Rate limiting ensures that alerts are manageable and actionable.</span></span>

<span data-ttu-id="eb8c4-106">regras de saudação para SMS e email são Olá mesmo.</span><span class="sxs-lookup"><span data-stu-id="eb8c4-106">hello rules for SMS and email are hello same.</span></span> <span data-ttu-id="eb8c4-107">limite de taxa de saudação é:</span><span class="sxs-lookup"><span data-stu-id="eb8c4-107">hello rate limit threshold is:</span></span>

 - <span data-ttu-id="eb8c4-108">**SMS**: 10 mensagens em uma hora.</span><span class="sxs-lookup"><span data-stu-id="eb8c4-108">**SMS**: 10 messages in an hour.</span></span>
 - <span data-ttu-id="eb8c4-109">**Email**: 100 mensagens em uma hora.</span><span class="sxs-lookup"><span data-stu-id="eb8c4-109">**Email**: 100 messages in an hour.</span></span>

## <a name="rate-limit-rules"></a><span data-ttu-id="eb8c4-110">Regras do limite de taxa</span><span class="sxs-lookup"><span data-stu-id="eb8c4-110">Rate limit rules</span></span>
- <span data-ttu-id="eb8c4-111">Um determinado número de telefone ou email é limitada ao receber mais mensagens que permite que o limite de saudação de taxa.</span><span class="sxs-lookup"><span data-stu-id="eb8c4-111">A particular phone number or email is rate limited when it receives more messages than hello threshold allows.</span></span>
- <span data-ttu-id="eb8c4-112">Um número de telefone ou email pode fazer parte de grupos de ações em várias assinaturas.</span><span class="sxs-lookup"><span data-stu-id="eb8c4-112">A phone number or email can be part of action groups across many subscriptions.</span></span> <span data-ttu-id="eb8c4-113">A limitação de taxa aplica-se a todas as assinaturas.</span><span class="sxs-lookup"><span data-stu-id="eb8c4-113">Rate limiting applies across all subscriptions.</span></span> <span data-ttu-id="eb8c4-114">Ela se aplica, assim como Olá limite for atingido, mesmo se as mensagens são enviadas de várias assinaturas.</span><span class="sxs-lookup"><span data-stu-id="eb8c4-114">It applies as soon as hello threshold is reached, even if messages are sent from multiple subscriptions.</span></span>  
- <span data-ttu-id="eb8c4-115">Quando um número de telefone ou email é taxa limitada, um adicional de notificação é enviada toocommunicate Olá a limitação de taxa.</span><span class="sxs-lookup"><span data-stu-id="eb8c4-115">When a phone number or email is rate limited, an additional notification is sent toocommunicate hello rate limiting.</span></span> <span data-ttu-id="eb8c4-116">Olá notificação limitação de taxa de estados quando hello expira.</span><span class="sxs-lookup"><span data-stu-id="eb8c4-116">hello notification states when hello rate limiting expires.</span></span>

## <a name="rate-limit-of-webhooks"></a><span data-ttu-id="eb8c4-117">Limite de taxa de webhooks</span><span class="sxs-lookup"><span data-stu-id="eb8c4-117">Rate limit of webhooks</span></span> ##
<span data-ttu-id="eb8c4-118">Não há nenhuma limitação de taxa em vigor para webhooks.</span><span class="sxs-lookup"><span data-stu-id="eb8c4-118">There is no rate limiting in place for webhooks.</span></span>

## <a name="next-steps"></a><span data-ttu-id="eb8c4-119">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="eb8c4-119">Next steps</span></span> ##
* <span data-ttu-id="eb8c4-120">Saiba mais sobre o [comportamento de alertas por SMS](monitoring-sms-alert-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="eb8c4-120">Learn more about [SMS alert behavior](monitoring-sms-alert-behavior.md).</span></span>
* <span data-ttu-id="eb8c4-121">Obter um [visão geral de alertas de log de atividade](monitoring-overview-alerts.md)e saiba como tooreceive alertas.</span><span class="sxs-lookup"><span data-stu-id="eb8c4-121">Get an [overview of activity log alerts](monitoring-overview-alerts.md), and learn how tooreceive alerts.</span></span>  
* <span data-ttu-id="eb8c4-122">Saiba como muito[configurar alertas sempre que uma notificação de integridade do serviço é postada](monitoring-activity-log-alerts-on-service-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="eb8c4-122">Learn how too[configure alerts whenever a service health notification is posted](monitoring-activity-log-alerts-on-service-notifications.md).</span></span>
