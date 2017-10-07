---
title: entrega de grade de eventos aaaAzure e repetir
description: "Descreve como a Grade de Eventos do Azure entrega eventos e como ela trata mensagens não entregues."
services: event-grid
author: djrosanova
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/11/2017
ms.author: darosa
ms.openlocfilehash: 874b3bf8892fbf803ef40f29d0ec10eb50150916
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="event-grid-message-delivery-and-retry"></a><span data-ttu-id="715fd-103">Entrega e repetição de mensagens da Grade de Eventos</span><span class="sxs-lookup"><span data-stu-id="715fd-103">Event Grid message delivery and retry</span></span> 

<span data-ttu-id="715fd-104">Este artigo descreve como a Grade de Eventos do Azure trata os eventos quando a entrega não é confirmada.</span><span class="sxs-lookup"><span data-stu-id="715fd-104">This article describes how Azure Event Grid handles events when delivery is not acknowledged.</span></span>

<span data-ttu-id="715fd-105">A entrega proporcionada pela Grade de Eventos tem um tempo de duração.</span><span class="sxs-lookup"><span data-stu-id="715fd-105">Event Grid provides durable delivery.</span></span> <span data-ttu-id="715fd-106">Cada mensagem é entregue pelo menos uma vez para cada assinatura.</span><span class="sxs-lookup"><span data-stu-id="715fd-106">It delivers each message at least once for each subscription.</span></span> <span data-ttu-id="715fd-107">Eventos são enviados imediatamente webhook toohello registrado de cada assinatura.</span><span class="sxs-lookup"><span data-stu-id="715fd-107">Events are sent toohello registered webhook of each subscription immediately.</span></span> <span data-ttu-id="715fd-108">Se um webhook não confirmar o recebimento de um evento dentro de 60 segundos de entrega de saudação primeira tentativa, grade de eventos tentativas de entrega de eventos de saudação.</span><span class="sxs-lookup"><span data-stu-id="715fd-108">If a webhook does not acknowledge receipt of an event within 60 seconds of hello first delivery attempt, Event Grid retries delivery of hello event.</span></span>

## <a name="message-delivery-status"></a><span data-ttu-id="715fd-109">Status de entrega da mensagem</span><span class="sxs-lookup"><span data-stu-id="715fd-109">Message delivery status</span></span>

<span data-ttu-id="715fd-110">Grade de eventos usa o recebimento de tooacknowledge de códigos de resposta HTTP de eventos.</span><span class="sxs-lookup"><span data-stu-id="715fd-110">Event Grid uses HTTP response codes tooacknowledge receipt of events.</span></span> 

### <a name="success-codes"></a><span data-ttu-id="715fd-111">Códigos de êxito</span><span class="sxs-lookup"><span data-stu-id="715fd-111">Success codes</span></span>

<span data-ttu-id="715fd-112">Olá seguintes códigos de resposta HTTP indicam que um evento foi entregue com êxito tooyour webhook.</span><span class="sxs-lookup"><span data-stu-id="715fd-112">hello following HTTP response codes indicate that an event has been delivered successfully tooyour webhook.</span></span> <span data-ttu-id="715fd-113">A Grade de Eventos considera entrega concluída.</span><span class="sxs-lookup"><span data-stu-id="715fd-113">Event Grid considers delivery complete.</span></span>

- <span data-ttu-id="715fd-114">200 OK</span><span class="sxs-lookup"><span data-stu-id="715fd-114">200 OK</span></span>
- <span data-ttu-id="715fd-115">202 Aceito</span><span class="sxs-lookup"><span data-stu-id="715fd-115">202 Accepted</span></span>

### <a name="failure-codes"></a><span data-ttu-id="715fd-116">Códigos de falha</span><span class="sxs-lookup"><span data-stu-id="715fd-116">Failure codes</span></span>

<span data-ttu-id="715fd-117">Olá códigos de resposta HTTP a seguir indica que houve falha na tentativa de entrega de eventos.</span><span class="sxs-lookup"><span data-stu-id="715fd-117">hello following HTTP response codes indicate that an event delivery attempt failed.</span></span> <span data-ttu-id="715fd-118">Grade de eventos tenta novamente o evento de saudação toosend.</span><span class="sxs-lookup"><span data-stu-id="715fd-118">Event Grid tries again toosend hello event.</span></span> 

- <span data-ttu-id="715fd-119">400 Solicitação Inválida</span><span class="sxs-lookup"><span data-stu-id="715fd-119">400 Bad Request</span></span>
- <span data-ttu-id="715fd-120">401 Não Autorizado</span><span class="sxs-lookup"><span data-stu-id="715fd-120">401 Unauthorized</span></span>
- <span data-ttu-id="715fd-121">404 Não Encontrado</span><span class="sxs-lookup"><span data-stu-id="715fd-121">404 Not Found</span></span>
- <span data-ttu-id="715fd-122">408 Tempo limite da solicitação</span><span class="sxs-lookup"><span data-stu-id="715fd-122">408 Request timeout</span></span>
- <span data-ttu-id="715fd-123">414 URI muito longo</span><span class="sxs-lookup"><span data-stu-id="715fd-123">414 URI Too Long</span></span>
- <span data-ttu-id="715fd-124">500 Erro Interno do Servidor</span><span class="sxs-lookup"><span data-stu-id="715fd-124">500 Internal Server Error</span></span>
- <span data-ttu-id="715fd-125">503 Serviço Indisponível</span><span class="sxs-lookup"><span data-stu-id="715fd-125">503 Service Unavailable</span></span>
- <span data-ttu-id="715fd-126">504 Tempo Limite do Gateway</span><span class="sxs-lookup"><span data-stu-id="715fd-126">504 Gateway Timeout</span></span>

<span data-ttu-id="715fd-127">Qualquer outro código de resposta ou à falta de uma resposta indica uma falha.</span><span class="sxs-lookup"><span data-stu-id="715fd-127">Any other response code or a lack of a response indicates a failure.</span></span> <span data-ttu-id="715fd-128">A Grade de Eventos repete a entrega.</span><span class="sxs-lookup"><span data-stu-id="715fd-128">Event Grid retries delivery.</span></span> 

## <a name="retry-intervals"></a><span data-ttu-id="715fd-129">Intervalos de repetição</span><span class="sxs-lookup"><span data-stu-id="715fd-129">Retry intervals</span></span>

<span data-ttu-id="715fd-130">A Grade de Eventos usa uma política de repetição de retirada exponencial para a entrega de eventos.</span><span class="sxs-lookup"><span data-stu-id="715fd-130">Event Grid uses an exponential backoff retry policy for event delivery.</span></span> <span data-ttu-id="715fd-131">Se o webhook não responde ou retorna um código de falha, grade de eventos tentativas de entrega em Olá agenda a seguir:</span><span class="sxs-lookup"><span data-stu-id="715fd-131">If your webhook does not respond or returns a failure code, Event Grid retries delivery on hello following schedule:</span></span>

1. <span data-ttu-id="715fd-132">10 segundos</span><span class="sxs-lookup"><span data-stu-id="715fd-132">10 seconds</span></span>
2. <span data-ttu-id="715fd-133">30 segundos</span><span class="sxs-lookup"><span data-stu-id="715fd-133">30 seconds</span></span>
3. <span data-ttu-id="715fd-134">1 minuto</span><span class="sxs-lookup"><span data-stu-id="715fd-134">1 minute</span></span>
4. <span data-ttu-id="715fd-135">5 minutos</span><span class="sxs-lookup"><span data-stu-id="715fd-135">5 minutes</span></span>
5. <span data-ttu-id="715fd-136">10 minutos</span><span class="sxs-lookup"><span data-stu-id="715fd-136">10 minutes</span></span>
6. <span data-ttu-id="715fd-137">30 minutos</span><span class="sxs-lookup"><span data-stu-id="715fd-137">30 minutes</span></span>
7. <span data-ttu-id="715fd-138">1 hora</span><span class="sxs-lookup"><span data-stu-id="715fd-138">1 hour</span></span>

<span data-ttu-id="715fd-139">Grade de eventos adiciona um intervalos de repetição tooall aleatória pequena.</span><span class="sxs-lookup"><span data-stu-id="715fd-139">Event Grid adds a small randomization tooall retry intervals.</span></span>

## <a name="retry-duration"></a><span data-ttu-id="715fd-140">Duração da repetição</span><span class="sxs-lookup"><span data-stu-id="715fd-140">Retry duration</span></span>

<span data-ttu-id="715fd-141">Durante a visualização de hello, a grade de eventos do Azure expirar todos os eventos que não são entregues dentro de duas horas.</span><span class="sxs-lookup"><span data-stu-id="715fd-141">During hello preview, Azure Event Grid expires all events that are not delivered within two hours.</span></span> <span data-ttu-id="715fd-142">Antes da disponibilidade geral, esse tempo será maior too24 horas.</span><span class="sxs-lookup"><span data-stu-id="715fd-142">Before General Availability, this time will be increased too24 hours.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="715fd-143">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="715fd-143">Next steps</span></span>

* <span data-ttu-id="715fd-144">Para uma introdução tooEvent grade, consulte [sobre o evento grade](overview.md).</span><span class="sxs-lookup"><span data-stu-id="715fd-144">For an introduction tooEvent Grid, see [About Event Grid](overview.md).</span></span>
* <span data-ttu-id="715fd-145">tooquickly começar a usar a grade de eventos, consulte [rota e criar eventos personalizados com a grade de eventos do Azure](custom-event-quickstart.md).</span><span class="sxs-lookup"><span data-stu-id="715fd-145">tooquickly get started using Event Grid, see [Create and route custom events with Azure Event Grid](custom-event-quickstart.md).</span></span>
