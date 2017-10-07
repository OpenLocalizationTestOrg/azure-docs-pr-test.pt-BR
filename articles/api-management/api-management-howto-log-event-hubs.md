---
title: aaaHow toolog eventos tooAzure Hubs de eventos de gerenciamento de API do Azure | Microsoft Docs
description: Saiba como toolog eventos tooAzure Hubs de eventos de gerenciamento de API do Azure.
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 88f6507d-7460-4eb2-bffd-76025b73f8c4
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 09ca65fc48a874467c6662858f7594e9b19fcdb9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toolog-events-tooazure-event-hubs-in-azure-api-management"></a>Como toolog eventos tooAzure Hubs de eventos de gerenciamento de API do Azure
Hubs de eventos do Azure é um serviço de entrada de dados altamente escalonável que pode acomodar milhões de eventos por segundo, para que você possa processar e analisar Olá grandes quantidades de dados produzidos por seus aplicativos e dispositivos conectados. Hubs de eventos age como hello "porta da frente" para um pipeline de eventos, e depois que os dados são coletados em um hub de eventos que pode ser transformado e armazenados usando qualquer provedor de análise em tempo real ou adaptadores de envio em lote/armazenamento. Hubs de eventos separa a produção de hello de um fluxo de eventos do consumo Olá desses eventos, para que os consumidores de evento possam acessar eventos de saudação em suas próprias agendas.

Este artigo é um complemento toohello [integrar o gerenciamento de API do Azure com Hubs de eventos](https://azure.microsoft.com/documentation/videos/integrate-azure-api-management-with-event-hubs/) vídeo e descreve como eventos de gerenciamento de API toolog usando Hubs de eventos do Azure.

## <a name="create-an-azure-event-hub"></a>Criar um Hub de Eventos do Azure
toocreate um novo Hub de eventos, entrar toohello [portal clássico do Azure](https://manage.windowsazure.com) e clique em **novo**->**serviços de aplicativos**->**barramento de serviço**  -> **Hub de eventos**->**criação rápida**. Insira um nome de Hub de Eventos, uma região, selecione uma assinatura e selecione um namespace. Se você ainda não criou um namespace você pode criar um, digitando um nome na Olá **Namespace** caixa de texto. Quando todas as propriedades são configuradas, clique em **criar um novo Hub de evento** toocreate Olá Hub de eventos.

![Criar hub de eventos][create-event-hub]

Em seguida, navegue toohello **configurar** guia para o novo Hub de eventos e criar duas **políticas de acesso compartilhado**. Nome hello primeiro **envio** e dê a ele **enviar** permissões.

![Política de envio][sending-policy]

Nome hello segunda **recebendo**, dê a ele **escutar** permissões e clique em **salvar**.

![Política de recebimento][receiving-policy]

Cada política de acesso compartilhado permite que aplicativos toosend e receba eventos tooand de saudação Hub de eventos. cadeias de conexão de saudação tooaccess para essas políticas, navegar toohello **painel** guia de saudação Hub de eventos e clique em **informações de Conexão**.

![Cadeia de conexão][event-hub-dashboard]

Olá **envio** cadeia de caracteres de conexão é usada quando o log de eventos e hello **recebendo** cadeia de caracteres de conexão é usada durante o download de eventos de saudação Hub de eventos.

![Cadeia de conexão][event-hub-connection-string]

## <a name="create-an-api-management-logger"></a>Criar um agente de Gerenciamento de API
Agora que você tem um Hub de eventos, Olá próxima etapa é tooconfigure uma [agente](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) no seu gerenciamento de API de serviço para que possa registrar eventos toohello Hub de eventos.

Agentes de gerenciamento de API são configurados usando Olá [API de REST de gerenciamento de API](http://aka.ms/smapi). Antes de usar o hello API REST para Olá primeira vez, examine Olá [pré-requisitos](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#Prerequisites) e certifique-se de que você tenha [habilitado acesso toohello API REST](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#EnableRESTAPI).

toocreate um agente, fazer uma solicitação HTTP PUT usando Olá modelo de URL a seguir.

`https://{your service}.management.azure-api.net/loggers/{new logger name}?api-version=2014-02-14-preview`

* Substituir `{your service}` com o nome de saudação da sua instância do serviço de gerenciamento de API.
* Substituir `{new logger name}` com o nome desejado para o novo agente hello. Você fará referência a esse nome ao configurar Olá [log-eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) política

Adicione Olá cabeçalhos toohello solicitação a seguir.

* Content-Type : application/json
* Authorization : SharedAccessSignature 58...
  * Para obter instruções sobre como gerar Olá `SharedAccessSignature` consulte [autenticação de API de REST de gerenciamento do Azure API](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-authentication).

Especifique o corpo da solicitação hello usando Olá modelo a seguir.

```json
{
  "type" : "AzureEventHub",
  "description" : "Sample logger description",
  "credentials" : {
    "name" : "Name of hello Event Hub from hello Azure Classic Portal",
    "connectionString" : "Endpoint=Event Hub Sender connection string"
    }
}
```

* `type`deve ser definido muito`AzureEventHub`.
* `description`Fornece uma descrição opcional do agente de log hello e pode ser uma cadeia de caracteres de comprimento zero, se desejado.
* `credentials`contém Olá `name` e `connectionString` do seu Hub de eventos do Azure.

Quando você faz a solicitação hello, se o agente de log de saudação é criado um código de status `201 Created` é retornado.

> [!NOTE]
> Para outros códigos de retorno possíveis e seus motivos, confira [Criar um agente](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity#PUT). toosee como executar outras operações, como lista, update e delete, consulte Olá [agente](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) documentação de entidade.
>
>

## <a name="configure-log-to-eventhubs-policies"></a>Configurar políticas log-to-eventhubs
Quando o agente de log está configurado no gerenciamento de API, você pode configurar os eventos do log-eventhubs políticas toolog Olá desejado. Olá log-eventhubs política pode ser usada em qualquer Olá Olá políticas seção quanto política de entrada.

políticas de tooconfigure, entrar toohello [portal do Azure](https://portal.azure.com), navegue tooyour serviço de gerenciamento de API e clique em **portal do publicador** tooaccess Olá portal do publicador.

![Portal do editor][publisher-portal]

Clique em **políticas** no menu de gerenciamento de API Olá Olá esquerda, selecione o produto desejado hello e API e clique em **adicionar política**. Neste exemplo, estamos adicionando uma política toohello **Echo API** em Olá **Unlimited** produto.

![Adicionar política][add-policy]

Posicione o cursor no hello `inbound` política seção e clique em Olá **Log tooEventHub** Olá de tooinsert política `log-to-eventhub` modelo de política de instrução.

![Editor de políticas][event-hub-policy]

```xml
<log-to-eventhub logger-id ='logger-id'>
  @( string.Join(",", DateTime.UtcNow, context.Deployment.ServiceName, context.RequestId, context.Request.IpAddress, context.Operation.Name))
</log-to-eventhub>
```

Substituir `logger-id` com o nome de saudação do agente de gerenciamento de API Olá configurada na etapa anterior hello.

Você pode usar qualquer expressão que retorna uma cadeia de caracteres como valor Olá Olá `log-to-eventhub` elemento. Neste exemplo, uma cadeia de caracteres que contém a saudação data e hora, nome do serviço, id da solicitação, endereço de ip da solicitação e o nome da operação é registrada.

Clique em **salvar** toosave Olá atualizados de configuração de política. Assim que ele é salvo Olá diretiva não estiver ativa e os eventos são registrado toohello designado Hub de eventos.

## <a name="next-steps"></a>Próximas etapas
* Saiba mais sobre Hubs de Eventos do Azure
  * [Introdução aos Hubs de Eventos do Azure](../event-hubs/event-hubs-c-getstarted-send.md)
  * [Receber mensagens com EventProcessorHost](../event-hubs/event-hubs-dotnet-standard-getstarted-receive-eph.md)
  * [Guia de programação dos Hubs de Eventos](../event-hubs/event-hubs-programming-guide.md)
* Saiba mais sobre a integração do Gerenciamento de API e Hubs de eventos
  * [Referência de entidade do agente](https://docs.microsoft.com/rest/api/apimanagement/loggers)
  * [referência de política de log ao hub de eventos](https://docs.microsoft.com/azure/api-management/api-management-advanced-policies#log-to-eventhub)
  * [Monitorar suas APIs com o Gerenciamento de API do Azure, Hubs de Eventos e Runscope](api-management-log-to-eventhub-sample.md)    

## <a name="watch-a-video-walkthrough"></a>Assista a um passo a passo em vídeo
> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Integrate-Azure-API-Management-with-Event-Hubs/player]
>
>

[publisher-portal]: ./media/api-management-howto-log-event-hubs/publisher-portal.png
[create-event-hub]: ./media/api-management-howto-log-event-hubs/create-event-hub.png
[event-hub-connection-string]: ./media/api-management-howto-log-event-hubs/event-hub-connection-string.png
[event-hub-dashboard]: ./media/api-management-howto-log-event-hubs/event-hub-dashboard.png
[receiving-policy]: ./media/api-management-howto-log-event-hubs/receiving-policy.png
[sending-policy]: ./media/api-management-howto-log-event-hubs/sending-policy.png
[event-hub-policy]: ./media/api-management-howto-log-event-hubs/event-hub-policy.png
[add-policy]: ./media/api-management-howto-log-event-hubs/add-policy.png
