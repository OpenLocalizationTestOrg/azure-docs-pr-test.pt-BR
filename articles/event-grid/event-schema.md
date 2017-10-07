---
title: esquema de evento de grade de eventos aaaAzure
description: "Descreve as propriedades de saudação que são fornecidas para eventos com a grade de eventos do Azure."
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/15/2017
ms.author: babanisa
ms.openlocfilehash: 37178a5650b93fd9072d9cff3333aae14b2a2ba7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="event-grid-event-schema"></a><span data-ttu-id="f7d90-103">Esquema de eventos da Grade de Eventos</span><span class="sxs-lookup"><span data-stu-id="f7d90-103">Event Grid event schema</span></span>

<span data-ttu-id="f7d90-104">Este artigo fornece propriedades hello e o esquema de eventos.</span><span class="sxs-lookup"><span data-stu-id="f7d90-104">This article provides hello properties and schema for events.</span></span> <span data-ttu-id="f7d90-105">Os eventos consistem em um conjunto de cinco propriedades de cadeia de caracteres obrigatórias e um objeto **data** obrigatório.</span><span class="sxs-lookup"><span data-stu-id="f7d90-105">Events consist of a set of five required string properties and a required **data** object.</span></span> <span data-ttu-id="f7d90-106">Propriedades de saudação são eventos tooall comuns de qualquer fornecedor.</span><span class="sxs-lookup"><span data-stu-id="f7d90-106">hello properties are common tooall events from any publisher.</span></span> <span data-ttu-id="f7d90-107">Olá **dados** objeto contém propriedades que são específicas tooeach publicador.</span><span class="sxs-lookup"><span data-stu-id="f7d90-107">hello **data** object contains properties that are specific tooeach publisher.</span></span> <span data-ttu-id="f7d90-108">Tópicos de sistema, essas propriedades são específicos toohello provedor de recursos, como armazenamento ou Hubs de eventos.</span><span class="sxs-lookup"><span data-stu-id="f7d90-108">For system topics, these properties are specific toohello resource provider, such as Storage or Event Hubs.</span></span>

<span data-ttu-id="f7d90-109">Eventos são enviados tooAzure grade de eventos em uma matriz, que pode conter vários objetos de evento.</span><span class="sxs-lookup"><span data-stu-id="f7d90-109">Events are sent tooAzure Event Grid in an array, which can contain multiple event objects.</span></span> <span data-ttu-id="f7d90-110">Se houver apenas um único evento, a matriz de saudação tem um comprimento de 1.</span><span class="sxs-lookup"><span data-stu-id="f7d90-110">If there is only a single event, hello array has a length of 1.</span></span> 
 
## <a name="event-properties"></a><span data-ttu-id="f7d90-111">Propriedades do evento</span><span class="sxs-lookup"><span data-stu-id="f7d90-111">Event properties</span></span>

<span data-ttu-id="f7d90-112">Todos os eventos conterá Olá mesmo após os dados de nível superior.</span><span class="sxs-lookup"><span data-stu-id="f7d90-112">All events will contain hello same following top level data.</span></span>

| <span data-ttu-id="f7d90-113">Propriedade</span><span class="sxs-lookup"><span data-stu-id="f7d90-113">Property</span></span> | <span data-ttu-id="f7d90-114">Tipo</span><span class="sxs-lookup"><span data-stu-id="f7d90-114">Type</span></span> | <span data-ttu-id="f7d90-115">Descrição</span><span class="sxs-lookup"><span data-stu-id="f7d90-115">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="f7d90-116">topic</span><span class="sxs-lookup"><span data-stu-id="f7d90-116">topic</span></span> | <span data-ttu-id="f7d90-117">string</span><span class="sxs-lookup"><span data-stu-id="f7d90-117">string</span></span> | <span data-ttu-id="f7d90-118">Fonte de evento toohello do caminho completo de recursos.</span><span class="sxs-lookup"><span data-stu-id="f7d90-118">Full resource path toohello event source.</span></span> <span data-ttu-id="f7d90-119">Esse campo não é gravável.</span><span class="sxs-lookup"><span data-stu-id="f7d90-119">This field is not writeable.</span></span> |
| <span data-ttu-id="f7d90-120">subject</span><span class="sxs-lookup"><span data-stu-id="f7d90-120">subject</span></span> | <span data-ttu-id="f7d90-121">string</span><span class="sxs-lookup"><span data-stu-id="f7d90-121">string</span></span> | <span data-ttu-id="f7d90-122">Assunto de evento de toohello de caminho definida Publisher.</span><span class="sxs-lookup"><span data-stu-id="f7d90-122">Publisher defined path toohello event subject.</span></span> |
| <span data-ttu-id="f7d90-123">eventType</span><span class="sxs-lookup"><span data-stu-id="f7d90-123">eventType</span></span> | <span data-ttu-id="f7d90-124">string</span><span class="sxs-lookup"><span data-stu-id="f7d90-124">string</span></span> | <span data-ttu-id="f7d90-125">Uma saudação registrado tipos de evento para esta fonte de evento.</span><span class="sxs-lookup"><span data-stu-id="f7d90-125">One of hello registered event types for this event source.</span></span> |
| <span data-ttu-id="f7d90-126">eventTime</span><span class="sxs-lookup"><span data-stu-id="f7d90-126">eventTime</span></span> | <span data-ttu-id="f7d90-127">string</span><span class="sxs-lookup"><span data-stu-id="f7d90-127">string</span></span> | <span data-ttu-id="f7d90-128">evento Olá Olá é gerado com base na hora de UTC do provedor de saudação.</span><span class="sxs-lookup"><span data-stu-id="f7d90-128">hello time hello event is generated based on hello provider's UTC time.</span></span> |
| <span data-ttu-id="f7d90-129">ID</span><span class="sxs-lookup"><span data-stu-id="f7d90-129">id</span></span> | <span data-ttu-id="f7d90-130">string</span><span class="sxs-lookup"><span data-stu-id="f7d90-130">string</span></span> | <span data-ttu-id="f7d90-131">Identificador exclusivo do evento hello.</span><span class="sxs-lookup"><span data-stu-id="f7d90-131">Unique identifier for hello event.</span></span> |
| <span data-ttu-id="f7d90-132">data</span><span class="sxs-lookup"><span data-stu-id="f7d90-132">data</span></span> | <span data-ttu-id="f7d90-133">objeto</span><span class="sxs-lookup"><span data-stu-id="f7d90-133">object</span></span> | <span data-ttu-id="f7d90-134">Provedor de recursos de toohello específicos de dados de evento.</span><span class="sxs-lookup"><span data-stu-id="f7d90-134">Event data specific toohello resource provider.</span></span> |

## <a name="available-event-sources"></a><span data-ttu-id="f7d90-135">Origens de evento disponíveis</span><span class="sxs-lookup"><span data-stu-id="f7d90-135">Available event sources</span></span>

<span data-ttu-id="f7d90-136">Olá origens de eventos a seguir publica eventos para consumo por meio de grade de eventos:</span><span class="sxs-lookup"><span data-stu-id="f7d90-136">hello following event sources publish events for consumption via Event Grid:</span></span>

* <span data-ttu-id="f7d90-137">Grupos de recursos (operações de gerenciamento)</span><span class="sxs-lookup"><span data-stu-id="f7d90-137">Resource Groups (management operations)</span></span>
* <span data-ttu-id="f7d90-138">Assinaturas do Azure (operações de gerenciamento)</span><span class="sxs-lookup"><span data-stu-id="f7d90-138">Azure Subscriptions (management operations)</span></span>
* <span data-ttu-id="f7d90-139">Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="f7d90-139">Event Hubs</span></span>
* <span data-ttu-id="f7d90-140">Tópicos personalizados</span><span class="sxs-lookup"><span data-stu-id="f7d90-140">Custom Topics</span></span>

## <a name="azure-subscriptions"></a><span data-ttu-id="f7d90-141">Assinaturas do Azure</span><span class="sxs-lookup"><span data-stu-id="f7d90-141">Azure Subscriptions</span></span>

<span data-ttu-id="f7d90-142">As assinaturas do Azure agora podem emitir eventos de gerenciamento do Azure Resource Manager, como quando uma VM é criada ou uma conta de armazenamento é excluída.</span><span class="sxs-lookup"><span data-stu-id="f7d90-142">Azure subscriptions can now emit management events from Azure Resource Manager such as when a VM is created or a storage account is deleted.</span></span>

### <a name="available-event-types"></a><span data-ttu-id="f7d90-143">Tipos de evento disponíveis</span><span class="sxs-lookup"><span data-stu-id="f7d90-143">Available event types</span></span>

- <span data-ttu-id="f7d90-144">**Microsoft.Resources.ResourceWriteSuccess**: gerado quando uma operação de criação ou atualização de recurso é bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="f7d90-144">**Microsoft.Resources.ResourceWriteSuccess**: Raised when a resource create or update operation succeeds.</span></span>  
- <span data-ttu-id="f7d90-145">**Microsoft.Resources.ResourceWriteFailure**: gerado quando uma operação de criação ou atualização de recurso falha.</span><span class="sxs-lookup"><span data-stu-id="f7d90-145">**Microsoft.Resources.ResourceWriteFailure**: Raised when a resource create or update operation fails.</span></span>  
- <span data-ttu-id="f7d90-146">**Microsoft.Resources.ResourceWriteCancel**: gerado quando uma operação de criação ou atualização de recurso é cancelada.</span><span class="sxs-lookup"><span data-stu-id="f7d90-146">**Microsoft.Resources.ResourceWriteCancel**: Raised when a resource create or update operation is cancelled.</span></span>  
- <span data-ttu-id="f7d90-147">**Microsoft.Resources.ResourceDeleteSuccess**: gerado quando uma operação de exclusão de recurso é bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="f7d90-147">**Microsoft.Resources.ResourceDeleteSuccess**: Raised when a resource deletion operation succeeds.</span></span>  
- <span data-ttu-id="f7d90-148">**Microsoft.Resources.ResourceDeleteFailure**: gerado quando uma operação de exclusão de recurso falha.</span><span class="sxs-lookup"><span data-stu-id="f7d90-148">**Microsoft.Resources.ResourceDeleteFailure**: Raised when a resource delete operation fails.</span></span>  
- <span data-ttu-id="f7d90-149">**Microsoft.Resources.ResourceDeleteCancel**: "gerado quando uma exclusão de recurso é cancelada.</span><span class="sxs-lookup"><span data-stu-id="f7d90-149">**Microsoft.Resources.ResourceDeleteCancel**: "Raised when a resource delete is cancelled.</span></span> <span data-ttu-id="f7d90-150">Isso ocorre quando a implantação de modelo é cancelada.</span><span class="sxs-lookup"><span data-stu-id="f7d90-150">This happens when template deployment is cancelled.</span></span>

### <a name="example-event-schema"></a><span data-ttu-id="f7d90-151">Exemplo do esquema de evento</span><span class="sxs-lookup"><span data-stu-id="f7d90-151">Example event schema</span></span>

```json
[
    {
    "topic":"/subscriptions/{subscription-id}",
    "subject":"/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.EventGrid/eventSubscriptions/LogicAppdd584bdf-8347-49c9-b9a9-d1f980783501",
    "eventType":"Microsoft.Resources.ResourceWriteSuccess",
    "eventTime":"2017-08-16T03:54:38.2696833Z",
    "id":"25b3b0d0-d79b-44d5-9963-440d4e6a9bba",
    "data": {
        "authorization":"{azure_resource_manager_authorizations}",
        "claims":"{azure_resource_manager_claims}",
        "correlationId":"54ef1e39-6a82-44b3-abc1-bdeb6ce4d3c6",
        "httpRequest":"",
        "resourceProvider":"Microsoft.EventGrid",
        "resourceUri":"/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.EventGrid/eventSubscriptions/LogicAppdd584bdf-8347-49c9-b9a9-d1f980783501",
        "operationName":"Microsoft.EventGrid/eventSubscriptions/write",
        "status":"Succeeded",
        "subscriptionId":"{subscription-id}",
        "tenantId":"72f988bf-86f1-41af-91ab-2d7cd011db47"
        },
    }
]
```



## <a name="resource-groups"></a><span data-ttu-id="f7d90-152">Grupos de recursos</span><span class="sxs-lookup"><span data-stu-id="f7d90-152">Resource Groups</span></span>

<span data-ttu-id="f7d90-153">Os Grupos de Recursos agora podem emitir eventos de gerenciamento do Azure Resource Manager, como quando uma VM é criada ou uma conta de armazenamento é excluída.</span><span class="sxs-lookup"><span data-stu-id="f7d90-153">Resource Groups can now emit management events from Azure Resource Manager such as when a VM is created or a storage account is deleted.</span></span>

### <a name="available-event-types"></a><span data-ttu-id="f7d90-154">Tipos de evento disponíveis</span><span class="sxs-lookup"><span data-stu-id="f7d90-154">Available event types</span></span>

- <span data-ttu-id="f7d90-155">**Microsoft.Resources.ResourceWriteSuccess**: gerado quando uma operação de criação ou atualização de recurso é bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="f7d90-155">**Microsoft.Resources.ResourceWriteSuccess**: Raised when a resource create or update operation succeeds.</span></span>  
- <span data-ttu-id="f7d90-156">**Microsoft.Resources.ResourceWriteFailure**: gerado quando uma operação de criação ou atualização de recurso falha.</span><span class="sxs-lookup"><span data-stu-id="f7d90-156">**Microsoft.Resources.ResourceWriteFailure**: Raised when a resource create or update operation fails.</span></span>  
- <span data-ttu-id="f7d90-157">**Microsoft.Resources.ResourceWriteCancel**: gerado quando uma operação de criação ou atualização de recurso é cancelada.</span><span class="sxs-lookup"><span data-stu-id="f7d90-157">**Microsoft.Resources.ResourceWriteCancel**: Raised when a resource create or update operation is cancelled.</span></span>  
- <span data-ttu-id="f7d90-158">**Microsoft.Resources.ResourceDeleteSuccess**: gerado quando uma operação de exclusão de recurso é bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="f7d90-158">**Microsoft.Resources.ResourceDeleteSuccess**: Raised when a resource deletion operation succeeds.</span></span>  
- <span data-ttu-id="f7d90-159">**Microsoft.Resources.ResourceDeleteFailure**: gerado quando uma operação de exclusão de recurso falha.</span><span class="sxs-lookup"><span data-stu-id="f7d90-159">**Microsoft.Resources.ResourceDeleteFailure**: Raised when a resource delete operation fails.</span></span>  
- <span data-ttu-id="f7d90-160">**Microsoft.Resources.ResourceDeleteCancel**: "gerado quando uma exclusão de recurso é cancelada.</span><span class="sxs-lookup"><span data-stu-id="f7d90-160">**Microsoft.Resources.ResourceDeleteCancel**: "Raised when a resource delete is cancelled.</span></span> <span data-ttu-id="f7d90-161">Isso ocorre quando a implantação de modelo é cancelada.</span><span class="sxs-lookup"><span data-stu-id="f7d90-161">This happens when template deployment is cancelled.</span></span>

### <a name="example-event"></a><span data-ttu-id="f7d90-162">Exemplo de evento</span><span class="sxs-lookup"><span data-stu-id="f7d90-162">Example event</span></span>

```json
[
    {
    "topic":"/subscriptions/{subscription-id}/resourceGroups/{resource-group}",
    "subject":"/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.EventGrid/eventSubscriptions/LogicAppdd584bdf-8347-49c9-b9a9-d1f980783501",
    "eventType":"Microsoft.Resources.ResourceWriteSuccess",
    "eventTime":"2017-08-16T03:54:38.2696833Z",
    "id":"25b3b0d0-d79b-44d5-9963-440d4e6a9bba",
    "data": {
        "authorization":"{azure_resource_manager_authorizations}",
        "claims":"{azure_resource_manager_claims}",
        "correlationId":"54ef1e39-6a82-44b3-abc1-bdeb6ce4d3c6",
        "httpRequest":"",
        "resourceProvider":"Microsoft.EventGrid",
        "resourceUri":"/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.EventGrid/eventSubscriptions/LogicAppdd584bdf-8347-49c9-b9a9-d1f980783501",
        "operationName":"Microsoft.EventGrid/eventSubscriptions/write",
        "status":"Succeeded",
        "subscriptionId":"{subscription-id}",
        "tenantId":"72f988bf-86f1-41af-91ab-2d7cd011db47"
        },
    }
]
```



## <a name="event-hubs"></a><span data-ttu-id="f7d90-163">Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="f7d90-163">Event Hubs</span></span>

<span data-ttu-id="f7d90-164">Eventos de Hubs de eventos estão atualmente emitido somente quando um arquivo é enviado automaticamente toostorage usando o recurso de captura hello.</span><span class="sxs-lookup"><span data-stu-id="f7d90-164">Event Hubs events are currently only emitted when a file is automatically sent toostorage using hello Capture feature.</span></span>

### <a name="available-event-types"></a><span data-ttu-id="f7d90-165">Tipos de evento disponíveis</span><span class="sxs-lookup"><span data-stu-id="f7d90-165">Available event types</span></span>

- <span data-ttu-id="f7d90-166">**Microsoft.EventHub.CaptureFileCreated**: gerado quando um arquivo de captura é criado.</span><span class="sxs-lookup"><span data-stu-id="f7d90-166">**Microsoft.EventHub.CaptureFileCreated**: Raised when a capture file is created.</span></span>

### <a name="example-event"></a><span data-ttu-id="f7d90-167">Exemplo de evento</span><span class="sxs-lookup"><span data-stu-id="f7d90-167">Example event</span></span>

<span data-ttu-id="f7d90-168">Esse evento de exemplo mostra o esquema de saudação de um evento de Hubs de evento gerado quando a captura armazena um arquivo.</span><span class="sxs-lookup"><span data-stu-id="f7d90-168">This sample event shows hello schema of an Event Hubs event raised when Capture stores a file.</span></span> 

```json
[
    {
        "topic": "/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/Microsoft.EventHub/namespaces/{event-hubs-ns}",
        "subject": "eventhubs/eh1",
        "eventType": "Microsoft.EventHub.CaptureFileCreated",
        "eventTime": "2017-07-11T00:55:55.0120485Z",
        "id": "bd440490-a65e-4c97-8298-ef1eb325673c",
        "data": {
            "fileUrl": "https://gridtest1.blob.core.windows.net/acontainer/eventgridtest1/eh1/1/2017/07/11/00/54/54.avro",
            "fileType": "AzureBlockBlob",
            "partitionId": "1",
            "sizeInBytes": 0,
            "eventCount": 0,
            "firstSequenceNumber": -1,
            "lastSequenceNumber": -1,
            "firstEnqueueTime": "0001-01-01T00:00:00",
            "lastEnqueueTime": "0001-01-01T00:00:00"
        },
    }
]

```



## <a name="azure-blob-storage"></a><span data-ttu-id="f7d90-169">Armazenamento do Blobs do Azure</span><span class="sxs-lookup"><span data-stu-id="f7d90-169">Azure Blob Storage</span></span>

<span data-ttu-id="f7d90-170">Armazenamento de Blobs do Azure na versão prévia privada com inscrição para integração à Grade de Eventos.</span><span class="sxs-lookup"><span data-stu-id="f7d90-170">Azure Blob Storage in private preview with sign-up for integration with Event Grid.</span></span>

### <a name="available-event-types"></a><span data-ttu-id="f7d90-171">Tipos de evento disponíveis</span><span class="sxs-lookup"><span data-stu-id="f7d90-171">Available event types</span></span>

- <span data-ttu-id="f7d90-172">**Microsoft.Storage.BlobCreated**: gerado quando um blob é criado.</span><span class="sxs-lookup"><span data-stu-id="f7d90-172">**Microsoft.Storage.BlobCreated**: Raised when a blob is created.</span></span>
- <span data-ttu-id="f7d90-173">**Microsoft.Storage.BlobDeleted**: gerado quando um blob é excluído.</span><span class="sxs-lookup"><span data-stu-id="f7d90-173">**Microsoft.Storage.BlobDeleted**: Raised when a blob is deleted.</span></span>

### <a name="example-event"></a><span data-ttu-id="f7d90-174">Exemplo de evento</span><span class="sxs-lookup"><span data-stu-id="f7d90-174">Example event</span></span>

<span data-ttu-id="f7d90-175">Esse evento de exemplo mostra o esquema de saudação de um evento de armazenamento gerado quando um blob é criado.</span><span class="sxs-lookup"><span data-stu-id="f7d90-175">This sample event shows hello schema of a storage event raised when a blob is created.</span></span> 

```json
[
  {
    "topic": "/subscriptions/{subscription-id}/resourceGroups/Storage/providers/Microsoft.Storage/storageAccounts/xstoretestaccount",
    "subject": "/blobServices/default/containers/oc2d2817345i200097container/blobs/oc2d2817345i20002296blob",
    "eventType": "Microsoft.Storage.BlobCreated",
    "eventTime": "2017-06-26T18:41:00.9584103Z",
    "id": "831e1650-001e-001b-66ab-eeb76e069631",
    "data": {
      "api": "PutBlockList",
      "clientRequestId": "6d79dbfb-0e37-4fc4-981f-442c9ca65760",
      "requestId": "831e1650-001e-001b-66ab-eeb76e000000",
      "eTag": "0x8D4BCC2E4835CD0",
      "contentType": "application/octet-stream",
      "contentLength": 524288,
      "blobType": "BlockBlob",
      "url": "https://oc2d2817345i60006.blob.core.windows.net/oc2d2817345i200097container/oc2d2817345i20002296blob",
      "sequencer": "00000000000004420000000000028963",
      "storageDiagnostics": {
        "batchId": "b68529f3-68cd-4744-baa4-3c0498ec19f0"
      }
    }
  }
]
```




## <a name="custom-topics"></a><span data-ttu-id="f7d90-176">Tópicos personalizados</span><span class="sxs-lookup"><span data-stu-id="f7d90-176">Custom Topics</span></span>

<span data-ttu-id="f7d90-177">carga de dados de saudação de seus eventos personalizados é definida por você e pode ser qualquer JSON formatado corretamente.</span><span class="sxs-lookup"><span data-stu-id="f7d90-177">hello data payload of your custom events is defined by you and can be any well formated JSON.</span></span> <span data-ttu-id="f7d90-178">dados de nível superior Olá devem conter Olá mesmo campos como eventos de recurso padrão definido.</span><span class="sxs-lookup"><span data-stu-id="f7d90-178">hello top level data should contain hello same fields as standard resource defined events.</span></span> <span data-ttu-id="f7d90-179">Ao publicar tópicos toocustom de eventos, você deve considerar o assunto de saudação do seu tooaid eventos em roteamento e filtragem de modelagem.</span><span class="sxs-lookup"><span data-stu-id="f7d90-179">When publishing events toocustom topics you should consider modeling hello subject of your events tooaid in routing and filtering.</span></span>

### <a name="example-event"></a><span data-ttu-id="f7d90-180">Exemplo de evento</span><span class="sxs-lookup"><span data-stu-id="f7d90-180">Example event</span></span>

<span data-ttu-id="f7d90-181">saudação de exemplo a seguir mostra um evento para um tópico personalizado:</span><span class="sxs-lookup"><span data-stu-id="f7d90-181">hello following example shows an event for a custom topic:</span></span>
````json
[
  {
    "topic": "/subscriptions/{subscription-id}/resourceGroups/Storage/providers/Microsoft.EventGrid/topics/myeventgridtopic",
    "subject": "/myapp/vehicles/motorcycles",    
    "id": "b68529f3-68cd-4744-baa4-3c0498ec19e2",
    "eventType": "recordInserted",
    "eventTime": "2017-06-26T18:41:00.9584103Z",
    "data":{
      "make": "Ducati",
      "model": "Monster"
    }
  }
]

````

## <a name="next-steps"></a><span data-ttu-id="f7d90-182">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f7d90-182">Next steps</span></span>

* <span data-ttu-id="f7d90-183">Para uma introdução tooEvent grade, consulte [o que é a grade de eventos?](overview.md)</span><span class="sxs-lookup"><span data-stu-id="f7d90-183">For an introduction tooEvent Grid, see [What is Event Grid?](overview.md)</span></span>
* <span data-ttu-id="f7d90-184">toolearn sobre como criar uma assinatura de grade de eventos, consulte [esquema de assinatura de grade de eventos](subscription-creation-schema.md).</span><span class="sxs-lookup"><span data-stu-id="f7d90-184">toolearn about creating an Event Grid subscription, see [Event Grid subscription schema](subscription-creation-schema.md).</span></span>
