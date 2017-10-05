---
title: Como registrar eventos nos Hubs de Eventos do Azure no Gerenciamento de API do Azure | Microsoft Docs
description: Saiba como registrar eventos em log para Hubs de Eventos do Azure no Gerenciamento de API do Azure
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
ms.openlocfilehash: a310236179677046ec49930b07cfdffdadc37974
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-log-events-to-azure-event-hubs-in-azure-api-management"></a><span data-ttu-id="3a164-103">Como registrar eventos em log para Hubs de Eventos do Azure no Gerenciamento de API do Azure</span><span class="sxs-lookup"><span data-stu-id="3a164-103">How to log events to Azure Event Hubs in Azure API Management</span></span>
<span data-ttu-id="3a164-104">Hub de Eventos do Azure é um serviço de entrada de dados altamente escalonável que pode incluir milhões de eventos por segundo, para que você possa processar e analisar grandes quantidades de dados produzidos por seus aplicativos e dispositivos conectados.</span><span class="sxs-lookup"><span data-stu-id="3a164-104">Azure Event Hubs is a highly scalable data ingress service that can ingest millions of events per second so that you can process and analyze the massive amounts of data produced by your connected devices and applications.</span></span> <span data-ttu-id="3a164-105">Hub de Eventos age como a "porta de entrada” para um pipeline de eventos e depois que os dados são coletados em um hub de eventos, ele pode ser transformado e armazenado usando qualquer provedor de análise em tempo real ou adaptadores de envio em lote/armazenamento.</span><span class="sxs-lookup"><span data-stu-id="3a164-105">Event Hubs acts as the "front door" for an event pipeline, and once data is collected into an event hub, it can be transformed and stored using any real-time analytics provider or batching/storage adapters.</span></span> <span data-ttu-id="3a164-106">Hub de Eventos separa a produção de um fluxo de eventos do consumo desses eventos, para que os consumidores de eventos possam acessar os eventos em seu próprio cronograma.</span><span class="sxs-lookup"><span data-stu-id="3a164-106">Event Hubs decouples the production of a stream of events from the consumption of those events, so that event consumers can access the events on their own schedule.</span></span>

<span data-ttu-id="3a164-107">Este artigo é um complemento para o [integrar o Gerenciamento de API do Azure com vídeos dos Hubs de eventos](https://azure.microsoft.com/documentation/videos/integrate-azure-api-management-with-event-hubs/) e descreve como registrar eventos de Gerenciamento de API usando Hubs de eventos do Azure.</span><span class="sxs-lookup"><span data-stu-id="3a164-107">This article is a companion to the [Integrate Azure API Management with Event Hubs](https://azure.microsoft.com/documentation/videos/integrate-azure-api-management-with-event-hubs/) video and describes how to log API Management events using Azure Event Hubs.</span></span>

## <a name="create-an-azure-event-hub"></a><span data-ttu-id="3a164-108">Criar um Hub de Eventos do Azure</span><span class="sxs-lookup"><span data-stu-id="3a164-108">Create an Azure Event Hub</span></span>
<span data-ttu-id="3a164-109">Para criar um novo Hub de Eventos, entre no [portal clássico do Azure](https://manage.windowsazure.com) e clique em **Novo**->**Serviços de Aplicativos**->**Barramento de Serviço**->**Hub de Eventos**->**Criação Rápida**.</span><span class="sxs-lookup"><span data-stu-id="3a164-109">To create a new Event Hub, sign-in to the [Azure classic portal](https://manage.windowsazure.com) and click **New**->**App Services**->**Service Bus**->**Event Hub**->**Quick Create**.</span></span> <span data-ttu-id="3a164-110">Insira um nome de Hub de Eventos, uma região, selecione uma assinatura e selecione um namespace.</span><span class="sxs-lookup"><span data-stu-id="3a164-110">Enter an Event Hub name, region, select a subscription, and select a namespace.</span></span> <span data-ttu-id="3a164-111">Se você ainda não tiver criado um namespace, poderá criar um inserindo um nome na caixa de texto **Namespace** .</span><span class="sxs-lookup"><span data-stu-id="3a164-111">If you haven't previously created a namespace you can create one by typing a name in the **Namespace** textbox.</span></span> <span data-ttu-id="3a164-112">Depois que todas as propriedades estiverem configuradas, clique em **Criar um novo Hub de Eventos** para criar o Hub de Eventos.</span><span class="sxs-lookup"><span data-stu-id="3a164-112">Once all properties are configured, click **Create a new Event Hub** to create the Event Hub.</span></span>

![Criar hub de eventos][create-event-hub]

<span data-ttu-id="3a164-114">Em seguida, navegue até a guia **Configurar** do novo Hub de Eventos e crie duas **políticas de acesso compartilhado**.</span><span class="sxs-lookup"><span data-stu-id="3a164-114">Next, navigate to the **Configure** tab for your new Event Hub and create two **shared access policies**.</span></span> <span data-ttu-id="3a164-115">Nomeie a primeira como **Envio** e conceda a ela permissões de **Envio**.</span><span class="sxs-lookup"><span data-stu-id="3a164-115">Name the first one **Sending** and give it **Send** permissions.</span></span>

![Política de envio][sending-policy]

<span data-ttu-id="3a164-117">Nomeie a segunda como **Recebimento**, conceda a ela permissões de **Escuta** e clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="3a164-117">Name the second one **Receiving**, give it **Listen** permissions, and click **Save**.</span></span>

![Política de recebimento][receiving-policy]

<span data-ttu-id="3a164-119">Cada política de acesso compartilhado permite que aplicativos enviem e recebam eventos de e para o Hub de Eventos.</span><span class="sxs-lookup"><span data-stu-id="3a164-119">Each shared access policy allows applications to send and receive events to and from the Event Hub.</span></span> <span data-ttu-id="3a164-120">Para acessar as cadeias de conexão dessas políticas, navegue até a guia **Painel** do Hub de Eventos e clique em **Informações de conexão**.</span><span class="sxs-lookup"><span data-stu-id="3a164-120">To access the connection strings for these policies, navigate to the **Dashboard** tab of the Event Hub and click **Connection information**.</span></span>

![Cadeia de conexão][event-hub-dashboard]

<span data-ttu-id="3a164-122">A cadeia de conexão de **Envio** é usada ao registrar eventos em log e a cadeia de conexão de **Recebimento** é usada ao baixar eventos do Hub de Eventos.</span><span class="sxs-lookup"><span data-stu-id="3a164-122">The **Sending** connection string is used when logging events, and the **Receiving** connection string is used when downloading events from the Event Hub.</span></span>

![Cadeia de conexão][event-hub-connection-string]

## <a name="create-an-api-management-logger"></a><span data-ttu-id="3a164-124">Criar um agente de Gerenciamento de API</span><span class="sxs-lookup"><span data-stu-id="3a164-124">Create an API Management logger</span></span>
<span data-ttu-id="3a164-125">Agora que você tem um Hub de Eventos, a próxima etapa será configurar um [Agente](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) no seu serviço de Gerenciamento de API para que ele possa registrar eventos em log para o Hub de Eventos.</span><span class="sxs-lookup"><span data-stu-id="3a164-125">Now that you have an Event Hub, the next step is to configure a [Logger](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) in your API Management service so that it can log events to the Event Hub.</span></span>

<span data-ttu-id="3a164-126">Os agentes do Gerenciamento de API são configurados usando a [API REST do Gerenciamento de API](http://aka.ms/smapi).</span><span class="sxs-lookup"><span data-stu-id="3a164-126">API Management loggers are configured using the [API Management REST API](http://aka.ms/smapi).</span></span> <span data-ttu-id="3a164-127">Antes de usar a API REST pela primeira vez, examine os [pré-requisitos](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#Prerequisites) e verifique se você [habilitou o acesso à API REST](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#EnableRESTAPI).</span><span class="sxs-lookup"><span data-stu-id="3a164-127">Before using the REST API for the first time, review the [prerequisites](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#Prerequisites) and ensure that you have [enabled access to the REST API](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/api-management-rest#EnableRESTAPI).</span></span>

<span data-ttu-id="3a164-128">Para criar um agente de log, faça uma solicitação HTTP PUT usando o modelo de URL a seguir.</span><span class="sxs-lookup"><span data-stu-id="3a164-128">To create a logger, make an HTTP PUT request using the following URL template.</span></span>

`https://{your service}.management.azure-api.net/loggers/{new logger name}?api-version=2014-02-14-preview`

* <span data-ttu-id="3a164-129">Substitua `{your service}` pelo nome da sua instância do serviço de Gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="3a164-129">Replace `{your service}` with the name of your API Management service instance.</span></span>
* <span data-ttu-id="3a164-130">Substitua `{new logger name}` pelo nome desejado para o novo agente.</span><span class="sxs-lookup"><span data-stu-id="3a164-130">Replace `{new logger name}` with the desired name for your new logger.</span></span> <span data-ttu-id="3a164-131">Você fará referência a esse nome quando configurar a política [log-to-eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub)</span><span class="sxs-lookup"><span data-stu-id="3a164-131">You will reference this name when you configure the [log-to-eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) policy</span></span>

<span data-ttu-id="3a164-132">Adicione os cabeçalhos a seguir à solicitação.</span><span class="sxs-lookup"><span data-stu-id="3a164-132">Add the following headers to the request.</span></span>

* <span data-ttu-id="3a164-133">Content-Type : application/json</span><span class="sxs-lookup"><span data-stu-id="3a164-133">Content-Type : application/json</span></span>
* <span data-ttu-id="3a164-134">Authorization : SharedAccessSignature 58...</span><span class="sxs-lookup"><span data-stu-id="3a164-134">Authorization : SharedAccessSignature 58...</span></span>
  * <span data-ttu-id="3a164-135">Para saber mais sobre como gerar a `SharedAccessSignature` , confira [Autenticação da API REST do Gerenciamento de API do Azure](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-authentication).</span><span class="sxs-lookup"><span data-stu-id="3a164-135">For instructions on generating the `SharedAccessSignature` see [Azure API Management REST API Authentication](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-authentication).</span></span>

<span data-ttu-id="3a164-136">Especifique o corpo da solicitação usando o modelo a seguir.</span><span class="sxs-lookup"><span data-stu-id="3a164-136">Specify the request body using the following template.</span></span>

```json
{
  "type" : "AzureEventHub",
  "description" : "Sample logger description",
  "credentials" : {
    "name" : "Name of the Event Hub from the Azure Classic Portal",
    "connectionString" : "Endpoint=Event Hub Sender connection string"
    }
}
```

* <span data-ttu-id="3a164-137">`type` deve ser definido como `AzureEventHub`.</span><span class="sxs-lookup"><span data-stu-id="3a164-137">`type` must be set to `AzureEventHub`.</span></span>
* <span data-ttu-id="3a164-138">`description` fornece uma descrição opcional do agente e pode ser uma cadeia de caracteres de comprimento zero, se desejado.</span><span class="sxs-lookup"><span data-stu-id="3a164-138">`description` provides an optional description of the logger and can be a zero length string if desired.</span></span>
* <span data-ttu-id="3a164-139">`credentials` contém `name` e `connectionString` do seu Hub de Eventos do Azure.</span><span class="sxs-lookup"><span data-stu-id="3a164-139">`credentials` contains the `name` and `connectionString` of your Azure Event Hub.</span></span>

<span data-ttu-id="3a164-140">Quando você fizer a solicitação, se o agente for criado, um código de status `201 Created` será retornado</span><span class="sxs-lookup"><span data-stu-id="3a164-140">When you make the request, if the logger is created a status code of `201 Created` is returned.</span></span>

> [!NOTE]
> <span data-ttu-id="3a164-141">Para outros códigos de retorno possíveis e seus motivos, confira [Criar um agente](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity#PUT).</span><span class="sxs-lookup"><span data-stu-id="3a164-141">For other possible return codes and their reasons, see [Create a Logger](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity#PUT).</span></span> <span data-ttu-id="3a164-142">Para saber como executar outras operações, por exemplo, listar, atualizar e excluir, confira a documentação da entidade [Agente](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) .</span><span class="sxs-lookup"><span data-stu-id="3a164-142">To see how perform other operations such as list, update, and delete, see the [Logger](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-logger-entity) entity documentation.</span></span>
>
>

## <a name="configure-log-to-eventhubs-policies"></a><span data-ttu-id="3a164-143">Configurar políticas log-to-eventhubs</span><span class="sxs-lookup"><span data-stu-id="3a164-143">Configure log-to-eventhubs policies</span></span>
<span data-ttu-id="3a164-144">Depois que o agente de log estiver configurado no Gerenciamento de API, você poderá configurar suas políticas log-to-eventhubs para registrar os eventos desejados em log.</span><span class="sxs-lookup"><span data-stu-id="3a164-144">Once your logger is configured in API Management, you can configure your log-to-eventhubs policies to log the desired events.</span></span> <span data-ttu-id="3a164-145">A política log-to-eventhubs pode ser usada na seção de política de entrada ou na seção de política de saída.</span><span class="sxs-lookup"><span data-stu-id="3a164-145">The log-to-eventhubs policy can be used in either the inbound policy section or the outbound policy section.</span></span>

<span data-ttu-id="3a164-146">Para configurar as políticas, entre no [portal do Azure](https://portal.azure.com), navegue até seu serviço de Gerenciamento de API e clique em **portal do Editor** para acessar o portal do editor.</span><span class="sxs-lookup"><span data-stu-id="3a164-146">To configure policies, sign-in to the [Azure portal](https://portal.azure.com), navigate to your API Management service, and click **Publisher portal** to access the publisher portal.</span></span>

![Portal do editor][publisher-portal]

<span data-ttu-id="3a164-148">Clique em **Políticas** no menu do Gerenciamento de API à esquerda, selecione o produto e a API desejados e clique em **Adicionar política**.</span><span class="sxs-lookup"><span data-stu-id="3a164-148">Click **Policies** in the API Management menu on the left, select the desired product and API, and click **Add policy**.</span></span> <span data-ttu-id="3a164-149">Neste exemplo, estamos adicionando uma política à **API de Eco** no produto **Unlimited**.</span><span class="sxs-lookup"><span data-stu-id="3a164-149">In this example we're adding a policy to the **Echo API** in the **Unlimited** product.</span></span>

![Adicionar política][add-policy]

<span data-ttu-id="3a164-151">Posicione o cursor na seção da política `inbound` e clique na política **Registrar no EventHub** para inserir o modelo de instrução da política `log-to-eventhub`.</span><span class="sxs-lookup"><span data-stu-id="3a164-151">Position your cursor in the `inbound` policy section and click the **Log to EventHub** policy to insert the `log-to-eventhub` policy statement template.</span></span>

![Editor de políticas][event-hub-policy]

```xml
<log-to-eventhub logger-id ='logger-id'>
  @( string.Join(",", DateTime.UtcNow, context.Deployment.ServiceName, context.RequestId, context.Request.IpAddress, context.Operation.Name))
</log-to-eventhub>
```

<span data-ttu-id="3a164-153">Substitua `logger-id` pelo nome do agente de Gerenciamento de API que você configurou na etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="3a164-153">Replace `logger-id` with the name of the API Management logger you configured in the previous step.</span></span>

<span data-ttu-id="3a164-154">Você pode usar qualquer expressão que retorne uma cadeia de caracteres como o valor do elemento `log-to-eventhub` .</span><span class="sxs-lookup"><span data-stu-id="3a164-154">You can use any expression that returns a string as the value for the `log-to-eventhub` element.</span></span> <span data-ttu-id="3a164-155">Neste exemplo, é registrada em log uma cadeia de caracteres que com a data e hora, o nome do serviço, a ID da solicitação, o endereço IP da solicitação e o nome da operação.</span><span class="sxs-lookup"><span data-stu-id="3a164-155">In this example a string containing the date and time, service name, request id, request ip address, and operation name is logged.</span></span>

<span data-ttu-id="3a164-156">Clique em **Salvar** para salvar a configuração da política atualizada.</span><span class="sxs-lookup"><span data-stu-id="3a164-156">Click **Save** to save the updated policy configuration.</span></span> <span data-ttu-id="3a164-157">Assim que for salva, a política estará ativa e os eventos serão registrados em log para o Hub de Eventos designado.</span><span class="sxs-lookup"><span data-stu-id="3a164-157">As soon as it is saved the policy is active and events are logged to the designated Event Hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3a164-158">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3a164-158">Next steps</span></span>
* <span data-ttu-id="3a164-159">Saiba mais sobre Hubs de Eventos do Azure</span><span class="sxs-lookup"><span data-stu-id="3a164-159">Learn more about Azure Event Hubs</span></span>
  * [<span data-ttu-id="3a164-160">Introdução aos Hubs de Eventos do Azure</span><span class="sxs-lookup"><span data-stu-id="3a164-160">Get started with Azure Event Hubs</span></span>](../event-hubs/event-hubs-c-getstarted-send.md)
  * [<span data-ttu-id="3a164-161">Receber mensagens com EventProcessorHost</span><span class="sxs-lookup"><span data-stu-id="3a164-161">Receive messages with EventProcessorHost</span></span>](../event-hubs/event-hubs-dotnet-standard-getstarted-receive-eph.md)
  * [<span data-ttu-id="3a164-162">Guia de programação dos Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="3a164-162">Event Hubs programming guide</span></span>](../event-hubs/event-hubs-programming-guide.md)
* <span data-ttu-id="3a164-163">Saiba mais sobre a integração do Gerenciamento de API e Hubs de eventos</span><span class="sxs-lookup"><span data-stu-id="3a164-163">Learn more about API Management and Event Hubs integration</span></span>
  * [<span data-ttu-id="3a164-164">Referência de entidade do agente</span><span class="sxs-lookup"><span data-stu-id="3a164-164">Logger entity reference</span></span>](https://docs.microsoft.com/rest/api/apimanagement/loggers)
  * [<span data-ttu-id="3a164-165">referência de política de log ao hub de eventos</span><span class="sxs-lookup"><span data-stu-id="3a164-165">log-to-eventhub policy reference</span></span>](https://docs.microsoft.com/azure/api-management/api-management-advanced-policies#log-to-eventhub)
  * [<span data-ttu-id="3a164-166">Monitorar suas APIs com o Gerenciamento de API do Azure, Hubs de Eventos e Runscope</span><span class="sxs-lookup"><span data-stu-id="3a164-166">Monitor your APIs with Azure API Management, Event Hubs and Runscope</span></span>](api-management-log-to-eventhub-sample.md)    

## <a name="watch-a-video-walkthrough"></a><span data-ttu-id="3a164-167">Assista a um passo a passo em vídeo</span><span class="sxs-lookup"><span data-stu-id="3a164-167">Watch a video walkthrough</span></span>
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
