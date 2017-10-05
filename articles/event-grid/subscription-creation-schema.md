---
title: Esquema de assinatura de Grade de Eventos do Azure
description: Descreve as propriedades para assinar um evento com a grade de eventos do Azure.
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/17/2017
ms.author: babanisa
ms.openlocfilehash: eff2352066a76010d6d882a7b7e1961870cd2d46
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="event-grid-subscription-schema"></a><span data-ttu-id="f9c6b-103">Esquema de assinatura de Grade de Eventos</span><span class="sxs-lookup"><span data-stu-id="f9c6b-103">Event Grid subscription schema</span></span>

<span data-ttu-id="f9c6b-104">Para criar uma assinatura de grade de eventos, você envia uma solicitação para a operação de assinatura Create Event.</span><span class="sxs-lookup"><span data-stu-id="f9c6b-104">To create an Event Grid subscription, you send a request to the Create Event subscription operation.</span></span> <span data-ttu-id="f9c6b-105">Use o seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="f9c6b-105">Use the following format:</span></span>

```
PUT /subscriptions/{subscription-id}/resourceGroups/{group-name}/providers/{resource-provider}/{resource-type}/{resource-name}/Microsoft.EventGrid/eventSubscriptions/{event-type-definitions}?api-version=2017-06-15-preview
``` 

<span data-ttu-id="f9c6b-106">Por exemplo, para criar uma inscrição de evento para uma conta de armazenamento denominada `examplestorage` em um grupo de recursos denominado `examplegroup`, use o seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="f9c6b-106">For example, to create an event subscription for a storage account named `examplestorage` in a resource group named `examplegroup`, use the following format:</span></span>

```
PUT /subscriptions/{subscription-id}/resourceGroups/examplegroup/providers/Microsoft.Storage/storageaccounts/examplestorage/Microsoft.EventGrid/eventSubscriptions/{event-type-definitions}?api-version=2017-06-15-preview
``` 

<span data-ttu-id="f9c6b-107">O artigo descreve as propriedades e o esquema para o corpo da solicitação.</span><span class="sxs-lookup"><span data-stu-id="f9c6b-107">The article describes the properties and schema for the body of the request.</span></span>
 
## <a name="event-subscription-properties"></a><span data-ttu-id="f9c6b-108">Propriedades da assinatura do evento</span><span class="sxs-lookup"><span data-stu-id="f9c6b-108">Event subscription properties</span></span>

| <span data-ttu-id="f9c6b-109">Propriedade</span><span class="sxs-lookup"><span data-stu-id="f9c6b-109">Property</span></span> | <span data-ttu-id="f9c6b-110">Tipo</span><span class="sxs-lookup"><span data-stu-id="f9c6b-110">Type</span></span> | <span data-ttu-id="f9c6b-111">Descrição</span><span class="sxs-lookup"><span data-stu-id="f9c6b-111">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="f9c6b-112">destino</span><span class="sxs-lookup"><span data-stu-id="f9c6b-112">destination</span></span> | <span data-ttu-id="f9c6b-113">objeto</span><span class="sxs-lookup"><span data-stu-id="f9c6b-113">object</span></span> | <span data-ttu-id="f9c6b-114">O objeto que define o ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="f9c6b-114">The object that defines the endpoint.</span></span> |
| <span data-ttu-id="f9c6b-115">filtro</span><span class="sxs-lookup"><span data-stu-id="f9c6b-115">filter</span></span> | <span data-ttu-id="f9c6b-116">objeto</span><span class="sxs-lookup"><span data-stu-id="f9c6b-116">object</span></span> | <span data-ttu-id="f9c6b-117">Um campo opcional para filtrar os tipos de eventos.</span><span class="sxs-lookup"><span data-stu-id="f9c6b-117">An optional field for filtering the types of events.</span></span> |

### <a name="destination-object"></a><span data-ttu-id="f9c6b-118">objeto de destino</span><span class="sxs-lookup"><span data-stu-id="f9c6b-118">destination object</span></span>

| <span data-ttu-id="f9c6b-119">Propriedade</span><span class="sxs-lookup"><span data-stu-id="f9c6b-119">Property</span></span> | <span data-ttu-id="f9c6b-120">Tipo</span><span class="sxs-lookup"><span data-stu-id="f9c6b-120">Type</span></span> | <span data-ttu-id="f9c6b-121">Descrição</span><span class="sxs-lookup"><span data-stu-id="f9c6b-121">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="f9c6b-122">endpointType</span><span class="sxs-lookup"><span data-stu-id="f9c6b-122">endpointType</span></span> | <span data-ttu-id="f9c6b-123">string</span><span class="sxs-lookup"><span data-stu-id="f9c6b-123">string</span></span> | <span data-ttu-id="f9c6b-124">O tipo de ponto de extremidade para a assinatura (webhook/HTTP, o Hub de evento ou fila).</span><span class="sxs-lookup"><span data-stu-id="f9c6b-124">The type of endpoint for the subscription (webhook/HTTP, Event Hub, or queue).</span></span> | 
| <span data-ttu-id="f9c6b-125">endpointUrl</span><span class="sxs-lookup"><span data-stu-id="f9c6b-125">endpointUrl</span></span> | <span data-ttu-id="f9c6b-126">string</span><span class="sxs-lookup"><span data-stu-id="f9c6b-126">string</span></span> |  | 

### <a name="filter-object"></a><span data-ttu-id="f9c6b-127">objeto filter</span><span class="sxs-lookup"><span data-stu-id="f9c6b-127">filter object</span></span>

| <span data-ttu-id="f9c6b-128">Propriedade</span><span class="sxs-lookup"><span data-stu-id="f9c6b-128">Property</span></span> | <span data-ttu-id="f9c6b-129">Tipo</span><span class="sxs-lookup"><span data-stu-id="f9c6b-129">Type</span></span> | <span data-ttu-id="f9c6b-130">Descrição</span><span class="sxs-lookup"><span data-stu-id="f9c6b-130">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="f9c6b-131">includedEventTypes</span><span class="sxs-lookup"><span data-stu-id="f9c6b-131">includedEventTypes</span></span> | <span data-ttu-id="f9c6b-132">array</span><span class="sxs-lookup"><span data-stu-id="f9c6b-132">array</span></span> | <span data-ttu-id="f9c6b-133">Correspondência quando o tipo de evento na mensagem de evento é uma correspondência exata para esses nomes de tipo de evento.</span><span class="sxs-lookup"><span data-stu-id="f9c6b-133">Match when the event type in the event message is an exact match to one of these event type names.</span></span> <span data-ttu-id="f9c6b-134">Gera um erro quando o nome do evento não coincide com os nomes de tipo de evento registrados para a origem do evento.</span><span class="sxs-lookup"><span data-stu-id="f9c6b-134">Raises an error when event name does not match the registered event type names for the event source.</span></span> <span data-ttu-id="f9c6b-135">O padrão corresponde a todos os tipos de evento.</span><span class="sxs-lookup"><span data-stu-id="f9c6b-135">Default matches all event types.</span></span> |
| <span data-ttu-id="f9c6b-136">subjectBeginsWith</span><span class="sxs-lookup"><span data-stu-id="f9c6b-136">subjectBeginsWith</span></span> | <span data-ttu-id="f9c6b-137">string</span><span class="sxs-lookup"><span data-stu-id="f9c6b-137">string</span></span> | <span data-ttu-id="f9c6b-138">Uma correspondência de prefixo de filtro para o campo de assunto no evento mensagem.</span><span class="sxs-lookup"><span data-stu-id="f9c6b-138">A prefix-match filter to the subject field in the event message.</span></span> <span data-ttu-id="f9c6b-139">A cadeia de caracteres padrão ou vazia corresponde a tudo.</span><span class="sxs-lookup"><span data-stu-id="f9c6b-139">The default or empty string matches all.</span></span> | 
| <span data-ttu-id="f9c6b-140">subjectEndsWith</span><span class="sxs-lookup"><span data-stu-id="f9c6b-140">subjectEndsWith</span></span> | <span data-ttu-id="f9c6b-141">string</span><span class="sxs-lookup"><span data-stu-id="f9c6b-141">string</span></span> | <span data-ttu-id="f9c6b-142">Uma correspondência de sufixo de filtro para o campo de assunto no evento mensagem.</span><span class="sxs-lookup"><span data-stu-id="f9c6b-142">A suffix-match filter to the subject field in the event message.</span></span> <span data-ttu-id="f9c6b-143">A cadeia de caracteres padrão ou vazia corresponde a tudo.</span><span class="sxs-lookup"><span data-stu-id="f9c6b-143">The default or empty string matches all.</span></span> |
| <span data-ttu-id="f9c6b-144">subjectIsCaseSensitive</span><span class="sxs-lookup"><span data-stu-id="f9c6b-144">subjectIsCaseSensitive</span></span> | <span data-ttu-id="f9c6b-145">string</span><span class="sxs-lookup"><span data-stu-id="f9c6b-145">string</span></span> | <span data-ttu-id="f9c6b-146">Controla a correspondência que diferencia maiúsculas e minúsculas para filtros.</span><span class="sxs-lookup"><span data-stu-id="f9c6b-146">Controls case-sensitive matching for filters.</span></span> |


## <a name="example-subscription-schema"></a><span data-ttu-id="f9c6b-147">Esquema de assinatura de exemplo</span><span class="sxs-lookup"><span data-stu-id="f9c6b-147">Example subscription schema</span></span>

```json
{
  "properties": {
    "destination": {
      "endpointType": "webhook",
      "properties": {
          "endpointUrl": "https://example.azurewebsites.net/api/HttpTriggerCSharp1?code=VXbGWce53l48Mt8wuotr0GPmyJ/nDT4hgdFj9DpBiRt38qqnnm5OFg=="
      }
    },
    "filter": {
      "includedEventTypes": [ "blobCreated", "blobDeleted" ],
      "subjectBeginsWith": "blobServices/default/containers/mycontainer/log",
      "subjectEndsWith": ".jpg",
      "subjectIsCaseSensitive": "true"
    }
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="f9c6b-148">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f9c6b-148">Next steps</span></span>

* <span data-ttu-id="f9c6b-149">Para ver uma introdução à Grade de Eventos, confira [O que é uma Grade de eventos?](overview.md)</span><span class="sxs-lookup"><span data-stu-id="f9c6b-149">For an introduction to Event Grid, see [What is Event Grid?](overview.md)</span></span>