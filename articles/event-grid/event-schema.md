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
# <a name="event-grid-event-schema"></a>Esquema de eventos da Grade de Eventos

Este artigo fornece propriedades hello e o esquema de eventos. Os eventos consistem em um conjunto de cinco propriedades de cadeia de caracteres obrigatórias e um objeto **data** obrigatório. Propriedades de saudação são eventos tooall comuns de qualquer fornecedor. Olá **dados** objeto contém propriedades que são específicas tooeach publicador. Tópicos de sistema, essas propriedades são específicos toohello provedor de recursos, como armazenamento ou Hubs de eventos.

Eventos são enviados tooAzure grade de eventos em uma matriz, que pode conter vários objetos de evento. Se houver apenas um único evento, a matriz de saudação tem um comprimento de 1. 
 
## <a name="event-properties"></a>Propriedades do evento

Todos os eventos conterá Olá mesmo após os dados de nível superior.

| Propriedade | Tipo | Descrição |
| -------- | ---- | ----------- |
| topic | string | Fonte de evento toohello do caminho completo de recursos. Esse campo não é gravável. |
| subject | string | Assunto de evento de toohello de caminho definida Publisher. |
| eventType | string | Uma saudação registrado tipos de evento para esta fonte de evento. |
| eventTime | string | evento Olá Olá é gerado com base na hora de UTC do provedor de saudação. |
| ID | string | Identificador exclusivo do evento hello. |
| data | objeto | Provedor de recursos de toohello específicos de dados de evento. |

## <a name="available-event-sources"></a>Origens de evento disponíveis

Olá origens de eventos a seguir publica eventos para consumo por meio de grade de eventos:

* Grupos de recursos (operações de gerenciamento)
* Assinaturas do Azure (operações de gerenciamento)
* Hubs de Eventos
* Tópicos personalizados

## <a name="azure-subscriptions"></a>Assinaturas do Azure

As assinaturas do Azure agora podem emitir eventos de gerenciamento do Azure Resource Manager, como quando uma VM é criada ou uma conta de armazenamento é excluída.

### <a name="available-event-types"></a>Tipos de evento disponíveis

- **Microsoft.Resources.ResourceWriteSuccess**: gerado quando uma operação de criação ou atualização de recurso é bem-sucedida.  
- **Microsoft.Resources.ResourceWriteFailure**: gerado quando uma operação de criação ou atualização de recurso falha.  
- **Microsoft.Resources.ResourceWriteCancel**: gerado quando uma operação de criação ou atualização de recurso é cancelada.  
- **Microsoft.Resources.ResourceDeleteSuccess**: gerado quando uma operação de exclusão de recurso é bem-sucedida.  
- **Microsoft.Resources.ResourceDeleteFailure**: gerado quando uma operação de exclusão de recurso falha.  
- **Microsoft.Resources.ResourceDeleteCancel**: "gerado quando uma exclusão de recurso é cancelada. Isso ocorre quando a implantação de modelo é cancelada.

### <a name="example-event-schema"></a>Exemplo do esquema de evento

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



## <a name="resource-groups"></a>Grupos de recursos

Os Grupos de Recursos agora podem emitir eventos de gerenciamento do Azure Resource Manager, como quando uma VM é criada ou uma conta de armazenamento é excluída.

### <a name="available-event-types"></a>Tipos de evento disponíveis

- **Microsoft.Resources.ResourceWriteSuccess**: gerado quando uma operação de criação ou atualização de recurso é bem-sucedida.  
- **Microsoft.Resources.ResourceWriteFailure**: gerado quando uma operação de criação ou atualização de recurso falha.  
- **Microsoft.Resources.ResourceWriteCancel**: gerado quando uma operação de criação ou atualização de recurso é cancelada.  
- **Microsoft.Resources.ResourceDeleteSuccess**: gerado quando uma operação de exclusão de recurso é bem-sucedida.  
- **Microsoft.Resources.ResourceDeleteFailure**: gerado quando uma operação de exclusão de recurso falha.  
- **Microsoft.Resources.ResourceDeleteCancel**: "gerado quando uma exclusão de recurso é cancelada. Isso ocorre quando a implantação de modelo é cancelada.

### <a name="example-event"></a>Exemplo de evento

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



## <a name="event-hubs"></a>Hubs de Eventos

Eventos de Hubs de eventos estão atualmente emitido somente quando um arquivo é enviado automaticamente toostorage usando o recurso de captura hello.

### <a name="available-event-types"></a>Tipos de evento disponíveis

- **Microsoft.EventHub.CaptureFileCreated**: gerado quando um arquivo de captura é criado.

### <a name="example-event"></a>Exemplo de evento

Esse evento de exemplo mostra o esquema de saudação de um evento de Hubs de evento gerado quando a captura armazena um arquivo. 

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



## <a name="azure-blob-storage"></a>Armazenamento do Blobs do Azure

Armazenamento de Blobs do Azure na versão prévia privada com inscrição para integração à Grade de Eventos.

### <a name="available-event-types"></a>Tipos de evento disponíveis

- **Microsoft.Storage.BlobCreated**: gerado quando um blob é criado.
- **Microsoft.Storage.BlobDeleted**: gerado quando um blob é excluído.

### <a name="example-event"></a>Exemplo de evento

Esse evento de exemplo mostra o esquema de saudação de um evento de armazenamento gerado quando um blob é criado. 

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




## <a name="custom-topics"></a>Tópicos personalizados

carga de dados de saudação de seus eventos personalizados é definida por você e pode ser qualquer JSON formatado corretamente. dados de nível superior Olá devem conter Olá mesmo campos como eventos de recurso padrão definido. Ao publicar tópicos toocustom de eventos, você deve considerar o assunto de saudação do seu tooaid eventos em roteamento e filtragem de modelagem.

### <a name="example-event"></a>Exemplo de evento

saudação de exemplo a seguir mostra um evento para um tópico personalizado:
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

## <a name="next-steps"></a>Próximas etapas

* Para uma introdução tooEvent grade, consulte [o que é a grade de eventos?](overview.md)
* toolearn sobre como criar uma assinatura de grade de eventos, consulte [esquema de assinatura de grade de eventos](subscription-creation-schema.md).
