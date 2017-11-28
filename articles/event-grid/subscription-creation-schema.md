---
title: esquema de assinatura de grade de eventos aaaAzure
description: "Descreve as propriedades de saudação para assinar eventos tooan com a grade de eventos do Azure."
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/17/2017
ms.author: babanisa
ms.openlocfilehash: 6a96d67975a5a733c5ea3c56ea54501f94ea4cd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="event-grid-subscription-schema"></a><span data-ttu-id="b3dcd-103">Esquema de assinatura de Grade de Eventos</span><span class="sxs-lookup"><span data-stu-id="b3dcd-103">Event Grid subscription schema</span></span>

<span data-ttu-id="b3dcd-104">toocreate uma assinatura de grade de eventos, você envia uma solicitação toohello operação de assinatura de Create Event.</span><span class="sxs-lookup"><span data-stu-id="b3dcd-104">toocreate an Event Grid subscription, you send a request toohello Create Event subscription operation.</span></span> <span data-ttu-id="b3dcd-105">Use Olá formato a seguir:</span><span class="sxs-lookup"><span data-stu-id="b3dcd-105">Use hello following format:</span></span>

```
PUT /subscriptions/{subscription-id}/resourceGroups/{group-name}/providers/{resource-provider}/{resource-type}/{resource-name}/Microsoft.EventGrid/eventSubscriptions/{event-type-definitions}?api-version=2017-06-15-preview
``` 

<span data-ttu-id="b3dcd-106">Por exemplo, toocreate uma inscrição de evento para uma conta de armazenamento denominada `examplestorage` em um grupo de recursos denominado `examplegroup`, use Olá seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="b3dcd-106">For example, toocreate an event subscription for a storage account named `examplestorage` in a resource group named `examplegroup`, use hello following format:</span></span>

```
PUT /subscriptions/{subscription-id}/resourceGroups/examplegroup/providers/Microsoft.Storage/storageaccounts/examplestorage/Microsoft.EventGrid/eventSubscriptions/{event-type-definitions}?api-version=2017-06-15-preview
``` 

<span data-ttu-id="b3dcd-107">Olá descreve as propriedades de saudação e esquema de corpo de saudação da solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="b3dcd-107">hello article describes hello properties and schema for hello body of hello request.</span></span>
 
## <a name="event-subscription-properties"></a><span data-ttu-id="b3dcd-108">Propriedades da assinatura do evento</span><span class="sxs-lookup"><span data-stu-id="b3dcd-108">Event subscription properties</span></span>

| <span data-ttu-id="b3dcd-109">Propriedade</span><span class="sxs-lookup"><span data-stu-id="b3dcd-109">Property</span></span> | <span data-ttu-id="b3dcd-110">Tipo</span><span class="sxs-lookup"><span data-stu-id="b3dcd-110">Type</span></span> | <span data-ttu-id="b3dcd-111">Descrição</span><span class="sxs-lookup"><span data-stu-id="b3dcd-111">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="b3dcd-112">destino</span><span class="sxs-lookup"><span data-stu-id="b3dcd-112">destination</span></span> | <span data-ttu-id="b3dcd-113">objeto</span><span class="sxs-lookup"><span data-stu-id="b3dcd-113">object</span></span> | <span data-ttu-id="b3dcd-114">objeto de saudação que define o ponto de extremidade de saudação.</span><span class="sxs-lookup"><span data-stu-id="b3dcd-114">hello object that defines hello endpoint.</span></span> |
| <span data-ttu-id="b3dcd-115">filtro</span><span class="sxs-lookup"><span data-stu-id="b3dcd-115">filter</span></span> | <span data-ttu-id="b3dcd-116">objeto</span><span class="sxs-lookup"><span data-stu-id="b3dcd-116">object</span></span> | <span data-ttu-id="b3dcd-117">Um campo opcional para filtragem de tipos de saudação de eventos.</span><span class="sxs-lookup"><span data-stu-id="b3dcd-117">An optional field for filtering hello types of events.</span></span> |

### <a name="destination-object"></a><span data-ttu-id="b3dcd-118">objeto de destino</span><span class="sxs-lookup"><span data-stu-id="b3dcd-118">destination object</span></span>

| <span data-ttu-id="b3dcd-119">Propriedade</span><span class="sxs-lookup"><span data-stu-id="b3dcd-119">Property</span></span> | <span data-ttu-id="b3dcd-120">Tipo</span><span class="sxs-lookup"><span data-stu-id="b3dcd-120">Type</span></span> | <span data-ttu-id="b3dcd-121">Descrição</span><span class="sxs-lookup"><span data-stu-id="b3dcd-121">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="b3dcd-122">endpointType</span><span class="sxs-lookup"><span data-stu-id="b3dcd-122">endpointType</span></span> | <span data-ttu-id="b3dcd-123">string</span><span class="sxs-lookup"><span data-stu-id="b3dcd-123">string</span></span> | <span data-ttu-id="b3dcd-124">tipo de saudação do ponto de extremidade para a assinatura de saudação (webhook/HTTP, o Hub de evento ou fila).</span><span class="sxs-lookup"><span data-stu-id="b3dcd-124">hello type of endpoint for hello subscription (webhook/HTTP, Event Hub, or queue).</span></span> | 
| <span data-ttu-id="b3dcd-125">endpointUrl</span><span class="sxs-lookup"><span data-stu-id="b3dcd-125">endpointUrl</span></span> | <span data-ttu-id="b3dcd-126">string</span><span class="sxs-lookup"><span data-stu-id="b3dcd-126">string</span></span> |  | 

### <a name="filter-object"></a><span data-ttu-id="b3dcd-127">objeto filter</span><span class="sxs-lookup"><span data-stu-id="b3dcd-127">filter object</span></span>

| <span data-ttu-id="b3dcd-128">Propriedade</span><span class="sxs-lookup"><span data-stu-id="b3dcd-128">Property</span></span> | <span data-ttu-id="b3dcd-129">Tipo</span><span class="sxs-lookup"><span data-stu-id="b3dcd-129">Type</span></span> | <span data-ttu-id="b3dcd-130">Descrição</span><span class="sxs-lookup"><span data-stu-id="b3dcd-130">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="b3dcd-131">includedEventTypes</span><span class="sxs-lookup"><span data-stu-id="b3dcd-131">includedEventTypes</span></span> | <span data-ttu-id="b3dcd-132">array</span><span class="sxs-lookup"><span data-stu-id="b3dcd-132">array</span></span> | <span data-ttu-id="b3dcd-133">Corresponde ao tipo de evento de saudação na mensagem de saudação do evento é tooone uma correspondência exata desses nomes de tipo de evento.</span><span class="sxs-lookup"><span data-stu-id="b3dcd-133">Match when hello event type in hello event message is an exact match tooone of these event type names.</span></span> <span data-ttu-id="b3dcd-134">Gera um erro quando o nome do evento não coincide com nomes de tipo de evento Olá registrado para a origem do evento hello.</span><span class="sxs-lookup"><span data-stu-id="b3dcd-134">Raises an error when event name does not match hello registered event type names for hello event source.</span></span> <span data-ttu-id="b3dcd-135">O padrão corresponde a todos os tipos de evento.</span><span class="sxs-lookup"><span data-stu-id="b3dcd-135">Default matches all event types.</span></span> |
| <span data-ttu-id="b3dcd-136">subjectBeginsWith</span><span class="sxs-lookup"><span data-stu-id="b3dcd-136">subjectBeginsWith</span></span> | <span data-ttu-id="b3dcd-137">string</span><span class="sxs-lookup"><span data-stu-id="b3dcd-137">string</span></span> | <span data-ttu-id="b3dcd-138">Um correspondência de prefixo filtro toohello campo assunto na mensagem de saudação do evento.</span><span class="sxs-lookup"><span data-stu-id="b3dcd-138">A prefix-match filter toohello subject field in hello event message.</span></span> <span data-ttu-id="b3dcd-139">padrão de saudação ou cadeia de caracteres vazia corresponde a todos.</span><span class="sxs-lookup"><span data-stu-id="b3dcd-139">hello default or empty string matches all.</span></span> | 
| <span data-ttu-id="b3dcd-140">subjectEndsWith</span><span class="sxs-lookup"><span data-stu-id="b3dcd-140">subjectEndsWith</span></span> | <span data-ttu-id="b3dcd-141">string</span><span class="sxs-lookup"><span data-stu-id="b3dcd-141">string</span></span> | <span data-ttu-id="b3dcd-142">Um sufixo correspondência filtro toohello campo assunto na mensagem de saudação do evento.</span><span class="sxs-lookup"><span data-stu-id="b3dcd-142">A suffix-match filter toohello subject field in hello event message.</span></span> <span data-ttu-id="b3dcd-143">padrão de saudação ou cadeia de caracteres vazia corresponde a todos.</span><span class="sxs-lookup"><span data-stu-id="b3dcd-143">hello default or empty string matches all.</span></span> |
| <span data-ttu-id="b3dcd-144">subjectIsCaseSensitive</span><span class="sxs-lookup"><span data-stu-id="b3dcd-144">subjectIsCaseSensitive</span></span> | <span data-ttu-id="b3dcd-145">string</span><span class="sxs-lookup"><span data-stu-id="b3dcd-145">string</span></span> | <span data-ttu-id="b3dcd-146">Controla a correspondência que diferencia maiúsculas e minúsculas para filtros.</span><span class="sxs-lookup"><span data-stu-id="b3dcd-146">Controls case-sensitive matching for filters.</span></span> |


## <a name="example-subscription-schema"></a><span data-ttu-id="b3dcd-147">Esquema de assinatura de exemplo</span><span class="sxs-lookup"><span data-stu-id="b3dcd-147">Example subscription schema</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="b3dcd-148">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b3dcd-148">Next steps</span></span>

* <span data-ttu-id="b3dcd-149">Para uma introdução tooEvent grade, consulte [o que é a grade de eventos?](overview.md)</span><span class="sxs-lookup"><span data-stu-id="b3dcd-149">For an introduction tooEvent Grid, see [What is Event Grid?](overview.md)</span></span>
