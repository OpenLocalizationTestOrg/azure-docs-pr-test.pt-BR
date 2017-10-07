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
# <a name="how-toolog-events-tooazure-event-hubs-in-azure-api-management"></a><span data-ttu-id="59638-103">Como toolog eventos tooAzure Hubs de eventos de gerenciamento de API do Azure</span><span class="sxs-lookup"><span data-stu-id="59638-103">How toolog events tooAzure Event Hubs in Azure API Management</span></span>
<span data-ttu-id="59638-104">Hubs de eventos do Azure é um serviço de entrada de dados altamente escalonável que pode acomodar milhões de eventos por segundo, para que você possa processar e analisar Olá grandes quantidades de dados produzidos por seus aplicativos e dispositivos conectados.</span><span class="sxs-lookup"><span data-stu-id="59638-104">Azure Event Hubs is a highly scalable data ingress service that can ingest millions of events per second so that you can process and analyze hello massive amounts of data produced by your connected devices and applications.</span></span> <span data-ttu-id="59638-105">Hubs de eventos age como hello "porta da frente" para um pipeline de eventos, e depois que os dados são coletados em um hub de eventos que pode ser transformado e armazenados usando qualquer provedor de análise em tempo real ou adaptadores de envio em lote/armazenamento.</span><span class="sxs-lookup"><span data-stu-id="59638-105">Event Hubs acts as hello "front door" for an event pipeline, and once data is collected into an event hub, it can be transformed and stored using any real-time analytics provider or batching/storage adapters.</span></span> <span data-ttu-id="59638-106">Hubs de eventos separa a produção de hello de um fluxo de eventos do consumo Olá desses eventos, para que os consumidores de evento possam acessar eventos de saudação em suas próprias agendas.</span><span class="sxs-lookup"><span data-stu-id="59638-106">Event Hubs decouples hello production of a stream of events from hello consumption of those events, so that event consumers can access hello events on their own schedule.</span></span>

<span data-ttu-id="59638-107">Este artigo é um complemento toohello [integrar o gerenciamento de API do Azure com Hubs de eventos](https://azure.microsoft.com/documentation/videos/integrate-azure-api-management-with-event-hubs/) vídeo e descreve como eventos de gerenciamento de API toolog usando Hubs de eventos do Azure.</span><span class="sxs-lookup"><span data-stu-id="59638-107">This article is a companion toohello [Integrate Azure API Management with Event Hubs](https://azure.microsoft.com/documentation/videos/integrate-azure-api-management-with-event-hubs/) video and describes how toolog API Management events using Azure Event Hubs.</span></span>

## <a name="create-an-azure-event-hub"></a><span data-ttu-id="59638-108">Criar um Hub de Eventos do Azure</span><span class="sxs-lookup"><span data-stu-id="59638-108">Create an Azure Event Hub</span></span>
<span data-ttu-id="59638-109">toocreate um novo Hub de eventos, entrar toohello [portal clássico do Azure](https://manage.windowsazure.com) e clique em **novo**->**serviços de aplicativos**->**barramento de serviço**  -> **Hub de eventos**->**criação rápida**.</span><span class="sxs-lookup"><span data-stu-id="59638-109">toocreate a new Event Hub, sign-in toohello [Azure classic portal](https://manage.windowsazure.com) and click **New**->**App Services**->**Service Bus**->**Event Hub**->**Quick Create**.</span></span> <span data-ttu-id="59638-110">Insira um nome de Hub de Eventos, uma região, selecione uma assinatura e selecione um namespace.</span><span class="sxs-lookup"><span data-stu-id="59638-110">Enter an Event Hub name, region, select a subscription, and select a namespace.</span></span> <span data-ttu-id="59638-111">Se você ainda não criou um namespace você pode criar um, digitando um nome na Olá **Namespace** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="59638-111">If you haven't previously created a namespace you can create one by typing a name in hello **Namespace** textbox.</span></span> <span data-ttu-id="59638-112">Quando todas as propriedades são configuradas, clique em **criar um novo Hub de evento** toocreate Olá Hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="59638-112">Once all properties are configured, click **Create a new Event Hub** toocreate hello Event Hub.</span></span>

![Criar hub de eventos][create-event-hub]

<span data-ttu-id="59638-114">Em seguida, navegue toohello **configurar** guia para o novo Hub de eventos e criar duas **políticas de acesso compartilhado**.</span><span class="sxs-lookup"><span data-stu-id="59638-114">Next, navigate toohello **Configure** tab for your new Event Hub and create two **shared access policies**.</span></span> <span data-ttu-id="59638-115">Nome hello primeiro **envio** e dê a ele **enviar** permissões.</span><span class="sxs-lookup"><span data-stu-id="59638-115">Name hello first one **Sending** and give it **Send** permissions.</span></span>

![Política de envio][sending-policy]

<span data-ttu-id="59638-117">Nome hello segunda **recebendo**, dê a ele **escutar** permissões e clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="59638-117">Name hello second one **Receiving**, give it **Listen** permissions, and click **Save**.</span></span>

![Política de recebimento][receiving-policy]

<span data-ttu-id="59638-119">Cada política de acesso compartilhado permite que aplicativos toosend e receba eventos tooand de saudação Hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="59638-119">Each shared access policy allows applications toosend and receive events tooand from hello Event Hub.</span></span> <span data-ttu-id="59638-120">cadeias de conexão de saudação tooaccess para essas políticas, navegar toohello **painel** guia de saudação Hub de eventos e clique em **informações de Conexão**.</span><span class="sxs-lookup"><span data-stu-id="59638-120">tooaccess hello connection strings for these policies, navigate toohello **Dashboard** tab of hello Event Hub and click **Connection information**.</span></span>

![Cadeia de conexão][event-hub-dashboard]

<span data-ttu-id="59638-122">Olá **envio** cadeia de caracteres de conexão é usada quando o log de eventos e hello **recebendo** cadeia de caracteres de conexão é usada durante o download de eventos de saudação Hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="59638-122">hello **Sending** connection string is used when logging events, and hello **Receiving** connection string is used when downloading events from hello Event Hub.</span></span>

![Cadeia de conexão][event-hub-connection-string]

## <a name="create-an-api-management-logger"></a><span data-ttu-id="59638-124">Criar um agente de Gerenciamento de API</span><span class="sxs-lookup"><span data-stu-id="59638-124">Create an API Management logger</span></span>
<span data-ttu-id="59638-125">Agora que você tem um Hub de eventos, Olá próxima etapa é tooconfigure uma [agente](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) no seu gerenciamento de API de serviço para que possa registrar eventos toohello Hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="59638-125">Now that you have an Event Hub, hello next step is tooconfigure a [Logger](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) in your API Management service so that it can log events toohello Event Hub.</span></span>

<span data-ttu-id="59638-126">Agentes de gerenciamento de API são configurados usando Olá [API de REST de gerenciamento de API](http://aka.ms/smapi).</span><span class="sxs-lookup"><span data-stu-id="59638-126">API Management loggers are configured using hello [API Management REST API](http://aka.ms/smapi).</span></span> <span data-ttu-id="59638-127">Antes de usar o hello API REST para Olá primeira vez, examine Olá [pré-requisitos](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#Prerequisites) e certifique-se de que você tenha [habilitado acesso toohello API REST](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#EnableRESTAPI).</span><span class="sxs-lookup"><span data-stu-id="59638-127">Before using hello REST API for hello first time, review hello [prerequisites](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#Prerequisites) and ensure that you have [enabled access toohello REST API](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#EnableRESTAPI).</span></span>

<span data-ttu-id="59638-128">toocreate um agente, fazer uma solicitação HTTP PUT usando Olá modelo de URL a seguir.</span><span class="sxs-lookup"><span data-stu-id="59638-128">toocreate a logger, make an HTTP PUT request using hello following URL template.</span></span>

`https://{your service}.management.azure-api.net/loggers/{new logger name}?api-version=2014-02-14-preview`

* <span data-ttu-id="59638-129">Substituir `{your service}` com o nome de saudação da sua instância do serviço de gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="59638-129">Replace `{your service}` with hello name of your API Management service instance.</span></span>
* <span data-ttu-id="59638-130">Substituir `{new logger name}` com o nome desejado para o novo agente hello.</span><span class="sxs-lookup"><span data-stu-id="59638-130">Replace `{new logger name}` with hello desired name for your new logger.</span></span> <span data-ttu-id="59638-131">Você fará referência a esse nome ao configurar Olá [log-eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) política</span><span class="sxs-lookup"><span data-stu-id="59638-131">You will reference this name when you configure hello [log-to-eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) policy</span></span>

<span data-ttu-id="59638-132">Adicione Olá cabeçalhos toohello solicitação a seguir.</span><span class="sxs-lookup"><span data-stu-id="59638-132">Add hello following headers toohello request.</span></span>

* <span data-ttu-id="59638-133">Content-Type : application/json</span><span class="sxs-lookup"><span data-stu-id="59638-133">Content-Type : application/json</span></span>
* <span data-ttu-id="59638-134">Authorization : SharedAccessSignature 58...</span><span class="sxs-lookup"><span data-stu-id="59638-134">Authorization : SharedAccessSignature 58...</span></span>
  * <span data-ttu-id="59638-135">Para obter instruções sobre como gerar Olá `SharedAccessSignature` consulte [autenticação de API de REST de gerenciamento do Azure API](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-authentication).</span><span class="sxs-lookup"><span data-stu-id="59638-135">For instructions on generating hello `SharedAccessSignature` see [Azure API Management REST API Authentication](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-authentication).</span></span>

<span data-ttu-id="59638-136">Especifique o corpo da solicitação hello usando Olá modelo a seguir.</span><span class="sxs-lookup"><span data-stu-id="59638-136">Specify hello request body using hello following template.</span></span>

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

* <span data-ttu-id="59638-137">`type`deve ser definido muito`AzureEventHub`.</span><span class="sxs-lookup"><span data-stu-id="59638-137">`type` must be set too`AzureEventHub`.</span></span>
* <span data-ttu-id="59638-138">`description`Fornece uma descrição opcional do agente de log hello e pode ser uma cadeia de caracteres de comprimento zero, se desejado.</span><span class="sxs-lookup"><span data-stu-id="59638-138">`description` provides an optional description of hello logger and can be a zero length string if desired.</span></span>
* <span data-ttu-id="59638-139">`credentials`contém Olá `name` e `connectionString` do seu Hub de eventos do Azure.</span><span class="sxs-lookup"><span data-stu-id="59638-139">`credentials` contains hello `name` and `connectionString` of your Azure Event Hub.</span></span>

<span data-ttu-id="59638-140">Quando você faz a solicitação hello, se o agente de log de saudação é criado um código de status `201 Created` é retornado.</span><span class="sxs-lookup"><span data-stu-id="59638-140">When you make hello request, if hello logger is created a status code of `201 Created` is returned.</span></span>

> [!NOTE]
> <span data-ttu-id="59638-141">Para outros códigos de retorno possíveis e seus motivos, confira [Criar um agente](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity#PUT).</span><span class="sxs-lookup"><span data-stu-id="59638-141">For other possible return codes and their reasons, see [Create a Logger](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity#PUT).</span></span> <span data-ttu-id="59638-142">toosee como executar outras operações, como lista, update e delete, consulte Olá [agente](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) documentação de entidade.</span><span class="sxs-lookup"><span data-stu-id="59638-142">toosee how perform other operations such as list, update, and delete, see hello [Logger](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) entity documentation.</span></span>
>
>

## <a name="configure-log-to-eventhubs-policies"></a><span data-ttu-id="59638-143">Configurar políticas log-to-eventhubs</span><span class="sxs-lookup"><span data-stu-id="59638-143">Configure log-to-eventhubs policies</span></span>
<span data-ttu-id="59638-144">Quando o agente de log está configurado no gerenciamento de API, você pode configurar os eventos do log-eventhubs políticas toolog Olá desejado.</span><span class="sxs-lookup"><span data-stu-id="59638-144">Once your logger is configured in API Management, you can configure your log-to-eventhubs policies toolog hello desired events.</span></span> <span data-ttu-id="59638-145">Olá log-eventhubs política pode ser usada em qualquer Olá Olá políticas seção quanto política de entrada.</span><span class="sxs-lookup"><span data-stu-id="59638-145">hello log-to-eventhubs policy can be used in either hello inbound policy section or hello outbound policy section.</span></span>

<span data-ttu-id="59638-146">políticas de tooconfigure, entrar toohello [portal do Azure](https://portal.azure.com), navegue tooyour serviço de gerenciamento de API e clique em **portal do publicador** tooaccess Olá portal do publicador.</span><span class="sxs-lookup"><span data-stu-id="59638-146">tooconfigure policies, sign-in toohello [Azure portal](https://portal.azure.com), navigate tooyour API Management service, and click **Publisher portal** tooaccess hello publisher portal.</span></span>

![Portal do editor][publisher-portal]

<span data-ttu-id="59638-148">Clique em **políticas** no menu de gerenciamento de API Olá Olá esquerda, selecione o produto desejado hello e API e clique em **adicionar política**.</span><span class="sxs-lookup"><span data-stu-id="59638-148">Click **Policies** in hello API Management menu on hello left, select hello desired product and API, and click **Add policy**.</span></span> <span data-ttu-id="59638-149">Neste exemplo, estamos adicionando uma política toohello **Echo API** em Olá **Unlimited** produto.</span><span class="sxs-lookup"><span data-stu-id="59638-149">In this example we're adding a policy toohello **Echo API** in hello **Unlimited** product.</span></span>

![Adicionar política][add-policy]

<span data-ttu-id="59638-151">Posicione o cursor no hello `inbound` política seção e clique em Olá **Log tooEventHub** Olá de tooinsert política `log-to-eventhub` modelo de política de instrução.</span><span class="sxs-lookup"><span data-stu-id="59638-151">Position your cursor in hello `inbound` policy section and click hello **Log tooEventHub** policy tooinsert hello `log-to-eventhub` policy statement template.</span></span>

![Editor de políticas][event-hub-policy]

```xml
<log-to-eventhub logger-id ='logger-id'>
  @( string.Join(",", DateTime.UtcNow, context.Deployment.ServiceName, context.RequestId, context.Request.IpAddress, context.Operation.Name))
</log-to-eventhub>
```

<span data-ttu-id="59638-153">Substituir `logger-id` com o nome de saudação do agente de gerenciamento de API Olá configurada na etapa anterior hello.</span><span class="sxs-lookup"><span data-stu-id="59638-153">Replace `logger-id` with hello name of hello API Management logger you configured in hello previous step.</span></span>

<span data-ttu-id="59638-154">Você pode usar qualquer expressão que retorna uma cadeia de caracteres como valor Olá Olá `log-to-eventhub` elemento.</span><span class="sxs-lookup"><span data-stu-id="59638-154">You can use any expression that returns a string as hello value for hello `log-to-eventhub` element.</span></span> <span data-ttu-id="59638-155">Neste exemplo, uma cadeia de caracteres que contém a saudação data e hora, nome do serviço, id da solicitação, endereço de ip da solicitação e o nome da operação é registrada.</span><span class="sxs-lookup"><span data-stu-id="59638-155">In this example a string containing hello date and time, service name, request id, request ip address, and operation name is logged.</span></span>

<span data-ttu-id="59638-156">Clique em **salvar** toosave Olá atualizados de configuração de política.</span><span class="sxs-lookup"><span data-stu-id="59638-156">Click **Save** toosave hello updated policy configuration.</span></span> <span data-ttu-id="59638-157">Assim que ele é salvo Olá diretiva não estiver ativa e os eventos são registrado toohello designado Hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="59638-157">As soon as it is saved hello policy is active and events are logged toohello designated Event Hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="59638-158">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="59638-158">Next steps</span></span>
* <span data-ttu-id="59638-159">Saiba mais sobre Hubs de Eventos do Azure</span><span class="sxs-lookup"><span data-stu-id="59638-159">Learn more about Azure Event Hubs</span></span>
  * [<span data-ttu-id="59638-160">Introdução aos Hubs de Eventos do Azure</span><span class="sxs-lookup"><span data-stu-id="59638-160">Get started with Azure Event Hubs</span></span>](../event-hubs/event-hubs-c-getstarted-send.md)
  * [<span data-ttu-id="59638-161">Receber mensagens com EventProcessorHost</span><span class="sxs-lookup"><span data-stu-id="59638-161">Receive messages with EventProcessorHost</span></span>](../event-hubs/event-hubs-dotnet-standard-getstarted-receive-eph.md)
  * [<span data-ttu-id="59638-162">Guia de programação dos Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="59638-162">Event Hubs programming guide</span></span>](../event-hubs/event-hubs-programming-guide.md)
* <span data-ttu-id="59638-163">Saiba mais sobre a integração do Gerenciamento de API e Hubs de eventos</span><span class="sxs-lookup"><span data-stu-id="59638-163">Learn more about API Management and Event Hubs integration</span></span>
  * [<span data-ttu-id="59638-164">Referência de entidade do agente</span><span class="sxs-lookup"><span data-stu-id="59638-164">Logger entity reference</span></span>](https://docs.microsoft.com/rest/api/apimanagement/loggers)
  * [<span data-ttu-id="59638-165">referência de política de log ao hub de eventos</span><span class="sxs-lookup"><span data-stu-id="59638-165">log-to-eventhub policy reference</span></span>](https://docs.microsoft.com/azure/api-management/api-management-advanced-policies#log-to-eventhub)
  * [<span data-ttu-id="59638-166">Monitorar suas APIs com o Gerenciamento de API do Azure, Hubs de Eventos e Runscope</span><span class="sxs-lookup"><span data-stu-id="59638-166">Monitor your APIs with Azure API Management, Event Hubs and Runscope</span></span>](api-management-log-to-eventhub-sample.md)    

## <a name="watch-a-video-walkthrough"></a><span data-ttu-id="59638-167">Assista a um passo a passo em vídeo</span><span class="sxs-lookup"><span data-stu-id="59638-167">Watch a video walkthrough</span></span>
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
