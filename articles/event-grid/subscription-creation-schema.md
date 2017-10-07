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
# <a name="event-grid-subscription-schema"></a>Esquema de assinatura de Grade de Eventos

toocreate uma assinatura de grade de eventos, você envia uma solicitação toohello operação de assinatura de Create Event. Use Olá formato a seguir:

```
PUT /subscriptions/{subscription-id}/resourceGroups/{group-name}/providers/{resource-provider}/{resource-type}/{resource-name}/Microsoft.EventGrid/eventSubscriptions/{event-type-definitions}?api-version=2017-06-15-preview
``` 

Por exemplo, toocreate uma inscrição de evento para uma conta de armazenamento denominada `examplestorage` em um grupo de recursos denominado `examplegroup`, use Olá seguinte formato:

```
PUT /subscriptions/{subscription-id}/resourceGroups/examplegroup/providers/Microsoft.Storage/storageaccounts/examplestorage/Microsoft.EventGrid/eventSubscriptions/{event-type-definitions}?api-version=2017-06-15-preview
``` 

Olá descreve as propriedades de saudação e esquema de corpo de saudação da solicitação de saudação.
 
## <a name="event-subscription-properties"></a>Propriedades da assinatura do evento

| Propriedade | Tipo | Descrição |
| -------- | ---- | ----------- |
| destino | objeto | objeto de saudação que define o ponto de extremidade de saudação. |
| filtro | objeto | Um campo opcional para filtragem de tipos de saudação de eventos. |

### <a name="destination-object"></a>objeto de destino

| Propriedade | Tipo | Descrição |
| -------- | ---- | ----------- |
| endpointType | string | tipo de saudação do ponto de extremidade para a assinatura de saudação (webhook/HTTP, o Hub de evento ou fila). | 
| endpointUrl | string |  | 

### <a name="filter-object"></a>objeto filter

| Propriedade | Tipo | Descrição |
| -------- | ---- | ----------- |
| includedEventTypes | array | Corresponde ao tipo de evento de saudação na mensagem de saudação do evento é tooone uma correspondência exata desses nomes de tipo de evento. Gera um erro quando o nome do evento não coincide com nomes de tipo de evento Olá registrado para a origem do evento hello. O padrão corresponde a todos os tipos de evento. |
| subjectBeginsWith | string | Um correspondência de prefixo filtro toohello campo assunto na mensagem de saudação do evento. padrão de saudação ou cadeia de caracteres vazia corresponde a todos. | 
| subjectEndsWith | string | Um sufixo correspondência filtro toohello campo assunto na mensagem de saudação do evento. padrão de saudação ou cadeia de caracteres vazia corresponde a todos. |
| subjectIsCaseSensitive | string | Controla a correspondência que diferencia maiúsculas e minúsculas para filtros. |


## <a name="example-subscription-schema"></a>Esquema de assinatura de exemplo

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

## <a name="next-steps"></a>Próximas etapas

* Para uma introdução tooEvent grade, consulte [o que é a grade de eventos?](overview.md)
