---
title: Monitorar APIs com o Gerenciamento de API do Azure, Hubs de Eventos e Runscope | Microsoft Docs
description: "O exemplo de aplicativo que demonstra a política log-to-eventhub, conectando o Gerenciamento de API do Azure, os Hubs de Eventos do Azure e o Runscope para registro em log e monitoramento de HTTP"
services: api-management
documentationcenter: 
author: darrelmiller
manager: erikre
editor: 
ms.assetid: c528cf6f-5f16-4a06-beea-fa1207541a47
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 70ee752c5639c90f77dde104ce85eec0a1062300
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="monitor-your-apis-with-azure-api-management-event-hubs-and-runscope"></a><span data-ttu-id="846c5-103">Monitorar suas APIs com o Gerenciamento de API do Azure, Hubs de Eventos e Runscope</span><span class="sxs-lookup"><span data-stu-id="846c5-103">Monitor your APIs with Azure API Management, Event Hubs and Runscope</span></span>
<span data-ttu-id="846c5-104">O [serviço Gerenciamento de API](api-management-key-concepts.md) oferece muitos recursos para aprimorar o processamento de solicitações HTTP enviadas à API do HTTP.</span><span class="sxs-lookup"><span data-stu-id="846c5-104">The [API Management service](api-management-key-concepts.md) provides many capabilities to enhance the processing of HTTP requests sent to your HTTP API.</span></span> <span data-ttu-id="846c5-105">No entanto, a existência das solicitações e respostas é transitória.</span><span class="sxs-lookup"><span data-stu-id="846c5-105">However, the existence of the requests and responses are transient.</span></span> <span data-ttu-id="846c5-106">A solicitação é feita e flui pelo serviço Gerenciamento de API para a API de back-end.</span><span class="sxs-lookup"><span data-stu-id="846c5-106">The request is made and it flows through the API Management service to your backend API.</span></span> <span data-ttu-id="846c5-107">Sua API processa a solicitação e uma resposta flui de volta para o consumidor da API.</span><span class="sxs-lookup"><span data-stu-id="846c5-107">Your API processes the request and a response flows back through to the API consumer.</span></span> <span data-ttu-id="846c5-108">O serviço Gerenciamento de API mantém algumas estatísticas importantes sobre as APIs para exibição no painel do Portal do publicador, mas fora isso, os detalhes são apagados.</span><span class="sxs-lookup"><span data-stu-id="846c5-108">The API Management service keeps some important statistics about the APIs for display in the Publisher portal dashboard, but beyond that, the details are gone.</span></span>

<span data-ttu-id="846c5-109">Ao usar a [política](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) [log-to-eventhub](api-management-howto-policies.md) no serviço Gerenciamento de API, você poderá enviar todos os detalhes da solicitação e da resposta para um [Hub de Eventos do Azure](../event-hubs/event-hubs-what-is-event-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="846c5-109">By using the [log-to-eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) [policy](api-management-howto-policies.md) in the API Management service you can send any details from the request and response to an [Azure Event Hub](../event-hubs/event-hubs-what-is-event-hubs.md).</span></span> <span data-ttu-id="846c5-110">Existem vários motivos pelos quais você pode querer gerar eventos de mensagens HTTP enviadas para suas APIs.</span><span class="sxs-lookup"><span data-stu-id="846c5-110">There are a variety of reasons why you may want to generate events from HTTP messages being sent to your APIs.</span></span> <span data-ttu-id="846c5-111">Alguns exemplos incluem trilha de auditoria de atualizações, análise de uso, alerta de exceção e integrações de terceiros.</span><span class="sxs-lookup"><span data-stu-id="846c5-111">Some examples include audit trail of updates, usage analytics, exception alerting and 3rd party integrations.</span></span>   

<span data-ttu-id="846c5-112">Este artigo demonstra como capturar a mensagem inteira de solicitação e resposta HTTP, como enviá-la a um Hub de Eventos e como retransmitir essa mensagem a um serviço terceirizado que forneça serviços de registro em log e monitoramento de HTTP.</span><span class="sxs-lookup"><span data-stu-id="846c5-112">This article demonstrates how to capture the entire HTTP request and response message, send it to an Event Hub and then relay that message to a third party service that provides HTTP logging and monitoring services.</span></span>

## <a name="why-send-from-api-management-service"></a><span data-ttu-id="846c5-113">Por que enviar do serviço Gerenciamento de API?</span><span class="sxs-lookup"><span data-stu-id="846c5-113">Why Send From API Management Service?</span></span>
<span data-ttu-id="846c5-114">É possível escrever middleware HTTP que possa se conectar à estrutura de API HTTP para capturar solicitações e respostas HTTP e mantê-las em sistemas de registro em log e monitoramento.</span><span class="sxs-lookup"><span data-stu-id="846c5-114">It is possible to write HTTP middleware that can plug into HTTP API frameworks to capture HTTP requests and responses and feed them into logging and monitoring systems.</span></span> <span data-ttu-id="846c5-115">A desvantagem dessa abordagem é que o middleware HTTP precisa ser integrado à API de back-end e deve corresponder à plataforma da API.</span><span class="sxs-lookup"><span data-stu-id="846c5-115">The downside to this approach is the HTTP middleware needs to be integrated into the backend API and must match the platform of the API.</span></span> <span data-ttu-id="846c5-116">Se houver várias APIs, cada uma delas deverá implantar o middleware.</span><span class="sxs-lookup"><span data-stu-id="846c5-116">If there are multiple APIs then each one must deploy the middleware.</span></span> <span data-ttu-id="846c5-117">Normalmente, há motivos pelos quais as APIs de back-end não podem ser atualizadas.</span><span class="sxs-lookup"><span data-stu-id="846c5-117">Often there are reasons why backend APIs cannot be updated.</span></span>

<span data-ttu-id="846c5-118">O uso do serviço Gerenciamento de API do Azure para se integrar à infraestrutura de registro em log fornece uma solução centralizada independente de plataforma.</span><span class="sxs-lookup"><span data-stu-id="846c5-118">Using the Azure API Management service to integrate with logging infrastructure provides a centralized and platform-independent solution.</span></span> <span data-ttu-id="846c5-119">Ela também é escalonável, em parte devido aos recursos de [replicação geográfica](api-management-howto-deploy-multi-region.md) do Gerenciamento de API do Azure.</span><span class="sxs-lookup"><span data-stu-id="846c5-119">It is also scalable, in part due to the [geo-replication](api-management-howto-deploy-multi-region.md) capabilities of Azure API Management.</span></span>

## <a name="why-send-to-an-azure-event-hub"></a><span data-ttu-id="846c5-120">Por que enviar a um Hub de Eventos do Azure?</span><span class="sxs-lookup"><span data-stu-id="846c5-120">Why send to an Azure Event Hub?</span></span>
<span data-ttu-id="846c5-121">É pertinente perguntar, por que criar uma política que seja específica dos Hubs de Evento do Azure?</span><span class="sxs-lookup"><span data-stu-id="846c5-121">It is a reasonable to ask, why create a policy that is specific to Azure Event Hubs?</span></span> <span data-ttu-id="846c5-122">Há muitos locais diferentes onde eu posso querer registrar em log minhas solicitações.</span><span class="sxs-lookup"><span data-stu-id="846c5-122">There are many different places where I might want to log my requests.</span></span> <span data-ttu-id="846c5-123">Por que não basta enviar as solicitações diretamente para o destino final?</span><span class="sxs-lookup"><span data-stu-id="846c5-123">Why not just send the requests directly to the final destination?</span></span>  <span data-ttu-id="846c5-124">Essa é uma opção.</span><span class="sxs-lookup"><span data-stu-id="846c5-124">That is an option.</span></span> <span data-ttu-id="846c5-125">No entanto, ao registrar em log as solicitações de um serviço de gerenciamento de API, será necessário considerar como as mensagens de log afetarão o desempenho da API.</span><span class="sxs-lookup"><span data-stu-id="846c5-125">However, when making logging requests from an API management service, it is necessary to consider how logging messages will impact the performance of the API.</span></span> <span data-ttu-id="846c5-126">Os aumentos graduais na carga podem ser tratados aumentando as instâncias disponíveis dos componentes do sistema ou aproveitando a replicação geográfica.</span><span class="sxs-lookup"><span data-stu-id="846c5-126">Gradual increases in load can be handled by increasing available instances of system components or by taking advantage of geo-replication.</span></span> <span data-ttu-id="846c5-127">No entanto, picos curtos no tráfego podem fazer com que as solicitações sejam significativamente atrasadas caso as solicitações para infraestrutura de registro em log comecem a ficar lentas sob carga.</span><span class="sxs-lookup"><span data-stu-id="846c5-127">However, short spikes in traffic can cause requests to be significantly delayed if requests to logging infrastructure start to slow under load.</span></span>

<span data-ttu-id="846c5-128">Os Hubs de Eventos do Azure foram desenvolvidos para acomodar volumes gigantes de dados, com capacidade para lidar com um número muito maior de eventos do que o número de solicitações HTTP processadas pelas APIs.</span><span class="sxs-lookup"><span data-stu-id="846c5-128">The Azure Event Hubs is designed to ingress huge volumes of data, with capacity for dealing with a far higher number of events than the number of HTTP requests most APIs process.</span></span> <span data-ttu-id="846c5-129">O Hub de Eventos atua como um tipo de buffer sofisticado entre o serviço Gerenciamento de API e a infraestrutura que vai armazenar e processar as mensagens.</span><span class="sxs-lookup"><span data-stu-id="846c5-129">The Event Hub acts as a kind of sophisticated buffer between your API management service and the infrastructure that will store and process the messages.</span></span> <span data-ttu-id="846c5-130">Isso garante que o desempenho da API não sofrerá devido à infraestrutura de log.</span><span class="sxs-lookup"><span data-stu-id="846c5-130">This ensures that your API performance will not suffer due to the logging infrastructure.</span></span>  

<span data-ttu-id="846c5-131">Depois que os dados tiverem sido passados para um Hub de Eventos, eles serão mantidos e ficam aguardando que os consumidores do Hub de Eventos os processem.</span><span class="sxs-lookup"><span data-stu-id="846c5-131">Once the data has been passed to an Event Hub it is persisted and will wait for Event Hub consumers to process it.</span></span> <span data-ttu-id="846c5-132">O Hub de Eventos não se importa em como eles serão processados; seu único interesse é ter certeza de que a mensagem será entregue com êxito.</span><span class="sxs-lookup"><span data-stu-id="846c5-132">The Event Hub does not care how it will be processed, it just cares about making sure the message will be successfully delivered.</span></span>     

<span data-ttu-id="846c5-133">Os Hubs de Eventos têm a capacidade de transmitir eventos a vários grupos de consumidores.</span><span class="sxs-lookup"><span data-stu-id="846c5-133">Event Hubs have the ability to stream events to multiple consumer groups.</span></span> <span data-ttu-id="846c5-134">Isso permite que os eventos sejam processados por sistemas completamente diferentes.</span><span class="sxs-lookup"><span data-stu-id="846c5-134">This allows events to be processed by completely different systems.</span></span> <span data-ttu-id="846c5-135">Desse modo, é possível oferecer suporte a muitos cenários de integração, sem impor atrasos adicionais no processamento da solicitação de API no serviço Gerenciamento de API, pois somente um evento precisa ser gerado.</span><span class="sxs-lookup"><span data-stu-id="846c5-135">This enables supporting many integration scenarios without putting addition delays on the processing of the API request within the API Management service as only one event needs to be generated.</span></span>

## <a name="a-policy-to-send-applicationhttp-messages"></a><span data-ttu-id="846c5-136">Uma política para enviar mensagens de aplicativo/http</span><span class="sxs-lookup"><span data-stu-id="846c5-136">A policy to send application/http messages</span></span>
<span data-ttu-id="846c5-137">Um Hub de Eventos aceita dados de evento como uma cadeia de caracteres simples.</span><span class="sxs-lookup"><span data-stu-id="846c5-137">An Event Hub accepts event data as a simple string.</span></span> <span data-ttu-id="846c5-138">O conteúdo dessa cadeia de caracteres é de sua inteira responsabilidade.</span><span class="sxs-lookup"><span data-stu-id="846c5-138">The contents of that string are completely up to you.</span></span> <span data-ttu-id="846c5-139">Para poder empacotar uma solicitação HTTP e enviá-la para os Hubs de Eventos, precisamos formatar a cadeia de caracteres com as informações da solicitação ou da resposta.</span><span class="sxs-lookup"><span data-stu-id="846c5-139">To be able to package up an HTTP request and send it off to Event Hubs we need to format the string with the request or response information.</span></span> <span data-ttu-id="846c5-140">Em situações como essa, se houver um formato existente que possamos reutilizar, talvez não seja necessário escrever nosso próprio código de análise.</span><span class="sxs-lookup"><span data-stu-id="846c5-140">In situations like this, if there is an existing format we can reuse, then we may not have to write our own parsing code.</span></span> <span data-ttu-id="846c5-141">Inicialmente, considerei o uso do [HAR](http://www.softwareishard.com/blog/har-12-spec/) para enviar solicitações e respostas HTTP.</span><span class="sxs-lookup"><span data-stu-id="846c5-141">Initially I considered using the [HAR](http://www.softwareishard.com/blog/har-12-spec/) for sending HTTP requests and responses.</span></span> <span data-ttu-id="846c5-142">No entanto, esse formato é otimizado para armazenar uma sequência de solicitações HTTP em um formato baseado em JSON.</span><span class="sxs-lookup"><span data-stu-id="846c5-142">However, this format is optimized for storing a sequence of HTTP requests in a JSON based format.</span></span> <span data-ttu-id="846c5-143">Ele continha vários elementos obrigatórios que adicionaram complexidade desnecessária ao cenário de transmitir a mensagem HTTP por cabo.</span><span class="sxs-lookup"><span data-stu-id="846c5-143">It contained a number of mandatory elements that added unnecessary complexity for the scenario of passing the HTTP message over the wire.</span></span>  

<span data-ttu-id="846c5-144">Uma opção alternativa foi usar o tipo de mídia `application/http` , como descrito na [RFC 7230](http://tools.ietf.org/html/rfc7230)da especificação HTTP.</span><span class="sxs-lookup"><span data-stu-id="846c5-144">An alternative option was to use the `application/http` media type as described in the HTTP specification [RFC 7230](http://tools.ietf.org/html/rfc7230).</span></span> <span data-ttu-id="846c5-145">Esse tipo de mídia usa o mesmo formato que é utilizado para enviar de fato mensagens HTTP por cabo, mas toda a mensagem pode ser colocada no corpo de outra solicitação HTTP.</span><span class="sxs-lookup"><span data-stu-id="846c5-145">This media type uses the exact same format that is used to actually send HTTP messages over the wire, but the entire message can be put in the body of another HTTP request.</span></span> <span data-ttu-id="846c5-146">Em nosso caso, vamos usar o corpo como nossa mensagem para envio aos Hubs de Eventos.</span><span class="sxs-lookup"><span data-stu-id="846c5-146">In our case we are just going to use the body as our message to send to Event Hubs.</span></span> <span data-ttu-id="846c5-147">Para sua conveniência, há um analisador nas bibliotecas do [Microsoft ASP.NET Web API 2.2 Client](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Client/) que pode analisar esse formato e convertê-lo nos objetos nativos `HttpRequestMessage` e `HttpResponseMessage`.</span><span class="sxs-lookup"><span data-stu-id="846c5-147">Conveniently, there is a parser that exists in [Microsoft ASP.NET Web API 2.2 Client](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Client/) libraries that can parse this format and convert it into the native `HttpRequestMessage` and `HttpResponseMessage` objects.</span></span>

<span data-ttu-id="846c5-148">Para poder criar essa mensagem, precisamos aproveitar as [Expressões de política](https://msdn.microsoft.com/library/azure/dn910913.aspx) baseadas em C# no Gerenciamento de API do Azure.</span><span class="sxs-lookup"><span data-stu-id="846c5-148">To be able to create this message we need to take advantage of C# based [Policy expressions](https://msdn.microsoft.com/library/azure/dn910913.aspx) in Azure API Management.</span></span> <span data-ttu-id="846c5-149">Veja a política que envia uma mensagem de solicitação HTTP aos Hubs de Eventos do Azure.</span><span class="sxs-lookup"><span data-stu-id="846c5-149">Here is the policy which sends a HTTP request message to Azure Event Hubs.</span></span>

```xml
<log-to-eventhub logger-id="conferencelogger" partition-id="0">
@{
   var requestLine = string.Format("{0} {1} HTTP/1.1\r\n",
                                               context.Request.Method,
                                               context.Request.Url.Path + context.Request.Url.QueryString);

   var body = context.Request.Body?.As<string>(true);
   if (body != null && body.Length > 1024)
   {
       body = body.Substring(0, 1024);
   }

   var headers = context.Request.Headers
                          .Where(h => h.Key != "Authorization" && h.Key != "Ocp-Apim-Subscription-Key")
                          .Select(h => string.Format("{0}: {1}", h.Key, String.Join(", ", h.Value)))
                          .ToArray<string>();

   var headerString = (headers.Any()) ? string.Join("\r\n", headers) + "\r\n" : string.Empty;

   return "request:"   + context.Variables["message-id"] + "\n"
                       + requestLine + headerString + "\r\n" + body;
}
</log-to-eventhub>
```

### <a name="policy-declaration"></a><span data-ttu-id="846c5-150">Declaração de política</span><span class="sxs-lookup"><span data-stu-id="846c5-150">Policy declaration</span></span>
<span data-ttu-id="846c5-151">Existem alguns itens específicos sobre essa expressão de política que vale a pena mencionar.</span><span class="sxs-lookup"><span data-stu-id="846c5-151">There a few particular things worth mentioning about this policy expression.</span></span> <span data-ttu-id="846c5-152">A política log-to-eventhub tem um atributo chamado logger-id, que se refere ao nome do agente que foi criado no serviço Gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="846c5-152">The log-to-eventhub policy has an attribute called logger-id which refers to the name of logger that has been created within the API Management service.</span></span> <span data-ttu-id="846c5-153">Os detalhes de como configurar um agente do Hub de Eventos no serviço Gerenciamento de API podem ser encontrados no documento [Como registrar em log eventos nos Hubs de Eventos do Azure no Gerenciamento de API do Azure](api-management-howto-log-event-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="846c5-153">The details of how to setup an Event Hub logger in the API Management service can be found in the document [How to log events to Azure Event Hubs in Azure API Management](api-management-howto-log-event-hubs.md).</span></span> <span data-ttu-id="846c5-154">O segundo atributo é um parâmetro opcional que indica aos Hubs de Eventos em qual partição armazenar a mensagem.</span><span class="sxs-lookup"><span data-stu-id="846c5-154">The second attribute is an optional parameter that instructs Event Hubs which partition to store the message in.</span></span> <span data-ttu-id="846c5-155">Os Hubs de Eventos usam partições para habilitar a escalabilidade e exigem no mínimo duas.</span><span class="sxs-lookup"><span data-stu-id="846c5-155">Event Hubs use partitions to enable scalabilty and require a minimum of two.</span></span> <span data-ttu-id="846c5-156">A entrega ordenada das mensagens é garantida apenas dentro de uma partição.</span><span class="sxs-lookup"><span data-stu-id="846c5-156">The ordered delivery of messages is only guaranteed within a partition.</span></span> <span data-ttu-id="846c5-157">Se não orientarmos o Hub de Eventos em qual partição colocar a mensagem, ele usará um algoritmo de round robin para distribuir a carga.</span><span class="sxs-lookup"><span data-stu-id="846c5-157">If we do not instruct Event Hub in which partition to place the message, it will use a round-robin algorithm to distribute the load.</span></span> <span data-ttu-id="846c5-158">No entanto, isso pode fazer com que algumas das nossas mensagens sejam processadas fora de ordem.</span><span class="sxs-lookup"><span data-stu-id="846c5-158">However, that may cause some of our messages to be processed out of order.</span></span>  

### <a name="partitions"></a><span data-ttu-id="846c5-159">Partições</span><span class="sxs-lookup"><span data-stu-id="846c5-159">Partitions</span></span>
<span data-ttu-id="846c5-160">Para garantir que nossas mensagens sejam entregues aos consumidores em ordem e aproveitar o recurso de distribuição de carga das partições, optei por enviar mensagens de solicitação HTTP a uma partição e mensagens de resposta HTTP a uma segunda partição.</span><span class="sxs-lookup"><span data-stu-id="846c5-160">To ensure our messages are delivered to consumers in order and take advantage of the load distribution capability of partitions, I chose to send HTTP request messages to one partition and HTTP response messages to a second partition.</span></span> <span data-ttu-id="846c5-161">Isso garantirá uma distribuição de carga uniforme e que todas as solicitações e respostas sejam consumidas na ordem.</span><span class="sxs-lookup"><span data-stu-id="846c5-161">This will ensure an even load distribution and we can guarantee that all requests will be consumed in order and all responses will be consumed in order.</span></span> <span data-ttu-id="846c5-162">É possível que uma resposta seja consumida antes da solicitação correspondente, mas isso não é um problema, pois temos um mecanismo diferente para correlacionar solicitações com respostas e sabemos que as solicitações sempre vêm antes das respostas.</span><span class="sxs-lookup"><span data-stu-id="846c5-162">It is possible for a response to be consumed before the corresponding request, but as that is not a problem as we have a different mechanism for correlating requests to responses and we know that requests always come before responses.</span></span>

### <a name="http-payloads"></a><span data-ttu-id="846c5-163">Cargas HTTP</span><span class="sxs-lookup"><span data-stu-id="846c5-163">HTTP payloads</span></span>
<span data-ttu-id="846c5-164">Depois de criar `requestLine` , verificamos se o corpo da solicitação deve ser truncado.</span><span class="sxs-lookup"><span data-stu-id="846c5-164">After building the `requestLine` we check to see if the request body should be truncated.</span></span> <span data-ttu-id="846c5-165">O corpo da solicitação é truncado a apenas 1024.</span><span class="sxs-lookup"><span data-stu-id="846c5-165">The request body is truncated to only 1024.</span></span> <span data-ttu-id="846c5-166">Esse número poderá ser aumentado, embora as mensagens individuais do Hub de Eventos estejam limitadas a 256 KB, de modo que é provável que alguns corpos de mensagem HTTP não caibam em uma única mensagem.</span><span class="sxs-lookup"><span data-stu-id="846c5-166">This could be increased, however individual Event Hub messages are limited to 256KB, so it is likely that some HTTP message bodies will not fit in a single message.</span></span> <span data-ttu-id="846c5-167">Ao registrar em log e analisar, uma quantidade significativa de informações só poderá ser derivada da linha e dos cabeçalhos da solicitação HTTP.</span><span class="sxs-lookup"><span data-stu-id="846c5-167">When doing logging and analytics a significant amount of information can be derived from just the HTTP request line and headers.</span></span> <span data-ttu-id="846c5-168">Além disso, muitas solicitações API retornam apenas corpos pequenos e, portanto, a perda do valor das informações ao truncar corpos grandes é razoavelmente mínima em comparação com a redução nos custos de transferir, processar e armazenar para manter todo o conteúdo do corpo.</span><span class="sxs-lookup"><span data-stu-id="846c5-168">Also, many API requests only return small bodies and so the loss of information value by truncating large bodies is fairly minimal in comparison to the reduction in transfer, processing and storage costs to keep all body contents.</span></span> <span data-ttu-id="846c5-169">Uma observação final sobre o processamento do corpo é que precisamos passar `true` para o método As<string>(), pois estamos lendo o conteúdo do corpo, mas também queremos que a API de back-end seja capaz de ler o corpo.</span><span class="sxs-lookup"><span data-stu-id="846c5-169">One final note about processing the body is that we need to pass `true` to the As<string>() method because we are reading the body contents, but was also want the backend API to be able to read the body.</span></span> <span data-ttu-id="846c5-170">Ao passar true para esse método, fazemos com que o corpo seja armazenado em buffer, de modo que ele possa ser lido uma segunda vez.</span><span class="sxs-lookup"><span data-stu-id="846c5-170">By passing true to this method we cause the body to be buffered so that it can be read a second time.</span></span> <span data-ttu-id="846c5-171">Será importante lembrar-se disso, caso você tenha uma API que carregue arquivos muito grandes ou use sondagens longas.</span><span class="sxs-lookup"><span data-stu-id="846c5-171">This is important to be aware of if you have an API that does uploading of very large files or uses long polling.</span></span> <span data-ttu-id="846c5-172">Nesses casos, é melhor evitar a leitura do corpo.</span><span class="sxs-lookup"><span data-stu-id="846c5-172">In these cases it would be best to avoid reading the body at all.</span></span>   

### <a name="http-headers"></a><span data-ttu-id="846c5-173">Cabeçalhos HTTP</span><span class="sxs-lookup"><span data-stu-id="846c5-173">HTTP headers</span></span>
<span data-ttu-id="846c5-174">Os cabeçalhos HTTP podem ser simplesmente transferidos para o formato da mensagem em um formato de pares simples de chave/valor.</span><span class="sxs-lookup"><span data-stu-id="846c5-174">HTTP Headers can be simply transferred over into the message format in a simple key/value pair format.</span></span> <span data-ttu-id="846c5-175">Optamos por retirar determinados campos sensíveis à segurança, a fim de evitar vazamento desnecessário das informações credenciais.</span><span class="sxs-lookup"><span data-stu-id="846c5-175">We have chosen to strip out certain security sensitive fields, to avoid unnecessarily leaking credential information.</span></span> <span data-ttu-id="846c5-176">É improvável que as chaves da API e outras credenciais sejam usadas para fins de análise.</span><span class="sxs-lookup"><span data-stu-id="846c5-176">It is unlikely that API keys and other credentials would be used for analytics purposes.</span></span> <span data-ttu-id="846c5-177">Se desejarmos analisar o usuário e o produto específico que ele está usando, poderemos obter isso no objeto `context` e adicionar à mensagem.</span><span class="sxs-lookup"><span data-stu-id="846c5-177">If we wish to do analysis on the user and the particular product they are using then we could get that from the `context` object and add that to the message.</span></span>     

### <a name="message-metadata"></a><span data-ttu-id="846c5-178">Metadados da mensagem</span><span class="sxs-lookup"><span data-stu-id="846c5-178">Message Metadata</span></span>
<span data-ttu-id="846c5-179">Quando criamos a mensagem completa a ser enviada ao hub de eventos, a primeira linha não fará realmente parte da mensagem `application/http` .</span><span class="sxs-lookup"><span data-stu-id="846c5-179">When building the complete message to send to the event hub, the first line is not actually part of the `application/http` message.</span></span> <span data-ttu-id="846c5-180">A primeira linha é composta de metadados adicionais que consistem em apontar se a mensagem é de solicitação ou de resposta e em uma id de mensagem usada para correlacionar solicitações com as respostas.</span><span class="sxs-lookup"><span data-stu-id="846c5-180">The first line is additional metadata consisting of whether the message is a request or response message and a message id which is used to correlate requests to responses.</span></span> <span data-ttu-id="846c5-181">A id da mensagem é criada usando outra política que se parece com esta:</span><span class="sxs-lookup"><span data-stu-id="846c5-181">The message id is created by using another policy that looks like this:</span></span>

```xml
<set-variable name="message-id" value="@(Guid.NewGuid())" />
```

<span data-ttu-id="846c5-182">Poderíamos ter criado a mensagem de solicitação, tê-la armazenado em uma variável até que a resposta fosse retornada e, em seguida, simplesmente enviado a solicitação e a resposta como uma única mensagem.</span><span class="sxs-lookup"><span data-stu-id="846c5-182">We could have created the request message, stored that in a variable until the response was returned and then simply sent the request and response as a single message.</span></span> <span data-ttu-id="846c5-183">No entanto, ao enviarmos a solicitação e a resposta de modo independente e usando uma id de mensagem para correlacionar as duas, obtemos um pouco mais de flexibilidade no tamanho da mensagem, a capacidade de aproveitar várias partições enquanto mantemos a ordem da mensagem, e a solicitação aparecerá em nosso painel de log em pouco tempo.</span><span class="sxs-lookup"><span data-stu-id="846c5-183">However, by sending the request and response independently and using a message id to correlate the two, we get a bit more flexibility in the message size, the ability to take advantage of multiple partitions whilst maintaining message order and the request will appear in our logging dashboard sooner.</span></span> <span data-ttu-id="846c5-184">Também pode haver alguns cenários em que uma resposta válida nunca é enviada para o hub de evento, possivelmente devido a um erro fatal de solicitação no serviço Gerenciamento de API, mas ainda teremos um registro da solicitação.</span><span class="sxs-lookup"><span data-stu-id="846c5-184">There also may be some scenarios where a valid response is never sent to the event hub, possibly due to a fatal request error in the API Management service, but we still will have a record of the request.</span></span>

<span data-ttu-id="846c5-185">A política para enviar a mensagem de resposta HTTP é muito semelhante à solicitação e, portanto, a configuração da política completa se parece com esta:</span><span class="sxs-lookup"><span data-stu-id="846c5-185">The policy to send the response HTTP message looks very similar to the request and so the complete policy configuration looks like this:</span></span>

```xml
<policies>
  <inbound>
      <set-variable name="message-id" value="@(Guid.NewGuid())" />
      <log-to-eventhub logger-id="conferencelogger" partition-id="0">
      @{
          var requestLine = string.Format("{0} {1} HTTP/1.1\r\n",
                                                      context.Request.Method,
                                                      context.Request.Url.Path + context.Request.Url.QueryString);

          var body = context.Request.Body?.As<string>(true);
          if (body != null && body.Length > 1024)
          {
              body = body.Substring(0, 1024);
          }

          var headers = context.Request.Headers
                               .Where(h => h.Key != "Authorization" && h.Key != "Ocp-Apim-Subscription-Key")
                               .Select(h => string.Format("{0}: {1}", h.Key, String.Join(", ", h.Value)))
                               .ToArray<string>();

          var headerString = (headers.Any()) ? string.Join("\r\n", headers) + "\r\n" : string.Empty;

          return "request:"   + context.Variables["message-id"] + "\n"
                              + requestLine + headerString + "\r\n" + body;
      }
  </log-to-eventhub>
  </inbound>
  <backend>
      <forward-request follow-redirects="true" />
  </backend>
  <outbound>
      <log-to-eventhub logger-id="conferencelogger" partition-id="1">
      @{
          var statusLine = string.Format("HTTP/1.1 {0} {1}\r\n",
                                              context.Response.StatusCode,
                                              context.Response.StatusReason);

          var body = context.Response.Body?.As<string>(true);
          if (body != null && body.Length > 1024)
          {
              body = body.Substring(0, 1024);
          }

          var headers = context.Response.Headers
                                          .Select(h => string.Format("{0}: {1}", h.Key, String.Join(", ", h.Value)))
                                          .ToArray<string>();

          var headerString = (headers.Any()) ? string.Join("\r\n", headers) + "\r\n" : string.Empty;

          return "response:"  + context.Variables["message-id"] + "\n"
                              + statusLine + headerString + "\r\n" + body;
     }
  </log-to-eventhub>
  </outbound>
</policies>
```

<span data-ttu-id="846c5-186">A política `set-variable` cria um valor que pode ser acessado pela política `log-to-eventhub` na seção `<inbound>` e na seção `<outbound>`.</span><span class="sxs-lookup"><span data-stu-id="846c5-186">The `set-variable` policy creates a value that is accessible by both the `log-to-eventhub` policy in the `<inbound>` section and the `<outbound>` section.</span></span>  

## <a name="receiving-events-from-event-hubs"></a><span data-ttu-id="846c5-187">Recebendo eventos dos Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="846c5-187">Receiving events from Event Hubs</span></span>
<span data-ttu-id="846c5-188">Os eventos do Hub de Eventos do Azure são recebidos usando o [protocolo AMQP](http://www.amqp.org/).</span><span class="sxs-lookup"><span data-stu-id="846c5-188">Events from Azure Event Hub are received using the [AMQP protocol](http://www.amqp.org/).</span></span> <span data-ttu-id="846c5-189">A equipe do Barramento de Serviço da Microsoft disponibilizou bibliotecas de cliente para facilitar o consumo de eventos.</span><span class="sxs-lookup"><span data-stu-id="846c5-189">The Microsoft Service Bus team have made client libraries available to make the consuming events easier.</span></span> <span data-ttu-id="846c5-190">Duas abordagens diferentes são aceitas, uma é ser um *Consumidor Direto* e a outra é usar a classe `EventProcessorHost`.</span><span class="sxs-lookup"><span data-stu-id="846c5-190">There are two different approaches supported, one is being a *Direct Consumer* and the other is using the `EventProcessorHost` class.</span></span> <span data-ttu-id="846c5-191">Exemplos dessas duas abordagens podem ser encontrados no [Guia de Programação dos Hubs de Eventos](../event-hubs/event-hubs-programming-guide.md).</span><span class="sxs-lookup"><span data-stu-id="846c5-191">Examples of these two approaches can be found in the [Event Hubs Programming Guide](../event-hubs/event-hubs-programming-guide.md).</span></span> <span data-ttu-id="846c5-192">A principal diferença é: o `Direct Consumer` dá a você controle total e o `EventProcessorHost` executa alguns trabalhos para você, mas faz determinadas suposições sobre como você processará esses eventos.</span><span class="sxs-lookup"><span data-stu-id="846c5-192">The short version of the differences is, `Direct Consumer` gives you complete control and the `EventProcessorHost` does some of the plumbing work for you but makes certain assumptions about how you will process those events.</span></span>  

### <a name="eventprocessorhost"></a><span data-ttu-id="846c5-193">EventProcessorHost</span><span class="sxs-lookup"><span data-stu-id="846c5-193">EventProcessorHost</span></span>
<span data-ttu-id="846c5-194">Neste exemplo, usaremos o `EventProcessorHost` para simplificar, porém, ele pode não ser a melhor opção para esse cenário específico.</span><span class="sxs-lookup"><span data-stu-id="846c5-194">In this sample, we will use the `EventProcessorHost` for simplicity, however it may not the best choice for this particular scenario.</span></span> <span data-ttu-id="846c5-195">`EventProcessorHost` faz o trabalho difícil, para que você não precise se preocupar com problemas de threading em uma classe específica de processador de eventos.</span><span class="sxs-lookup"><span data-stu-id="846c5-195">`EventProcessorHost` does the hard work of making sure you don't have to worry about threading issues within a particular event processor class.</span></span> <span data-ttu-id="846c5-196">Entretanto, em nosso cenário, estamos simplesmente convertendo a mensagem em outro formato e passando-a para outro serviço usando um método assíncrono.</span><span class="sxs-lookup"><span data-stu-id="846c5-196">However, in our scenario, we are simply converting the message to another format and passing it along to another service using an async method.</span></span> <span data-ttu-id="846c5-197">Não há necessidade de atualizar o estado compartilhado e, portanto, nenhum risco de ter problemas de threading.</span><span class="sxs-lookup"><span data-stu-id="846c5-197">There is no need for updating shared state and therefore no risk of threading issues.</span></span> <span data-ttu-id="846c5-198">Na maioria dos cenários, `EventProcessorHost` provavelmente é a melhor opção e, certamente, a mais fácil.</span><span class="sxs-lookup"><span data-stu-id="846c5-198">For most scenarios, `EventProcessorHost` is probably the best choice and it is certainly the easier option.</span></span>     

### <a name="ieventprocessor"></a><span data-ttu-id="846c5-199">IEventProcessor</span><span class="sxs-lookup"><span data-stu-id="846c5-199">IEventProcessor</span></span>
<span data-ttu-id="846c5-200">O conceito central ao usar `EventProcessorHost` é criar uma implementação da interface `IEventProcessor` que contenha o método `ProcessEventAsync`.</span><span class="sxs-lookup"><span data-stu-id="846c5-200">The central concept when using `EventProcessorHost` is to create a an implementation of the `IEventProcessor` interface which contains the method `ProcessEventAsync`.</span></span> <span data-ttu-id="846c5-201">A essência desse método é mostrada aqui:</span><span class="sxs-lookup"><span data-stu-id="846c5-201">The essence of that method is shown here:</span></span>

```c#
async Task IEventProcessor.ProcessEventsAsync(PartitionContext context, IEnumerable<EventData> messages)
{

   foreach (EventData eventData in messages)
   {
       _Logger.LogInfo(string.Format("Event received from partition: {0} - {1}", context.Lease.PartitionId,eventData.PartitionKey));

       try
       {
           var httpMessage = HttpMessage.Parse(eventData.GetBodyStream());
           await _MessageContentProcessor.ProcessHttpMessage(httpMessage);
       }
       catch (Exception ex)
       {
           _Logger.LogError(ex.Message);
       }
   }
    ... checkpointing code snipped ...
}
```

<span data-ttu-id="846c5-202">Uma lista de objetos EventData é passada no método e nós iteramos essa lista.</span><span class="sxs-lookup"><span data-stu-id="846c5-202">A list of EventData objects are passed into the method and we iterate over that list.</span></span> <span data-ttu-id="846c5-203">Os bytes de cada método são analisados em um objeto HttpMessage e esse objeto é passado para uma instância de IHttpMessageProcessor.</span><span class="sxs-lookup"><span data-stu-id="846c5-203">The bytes of each method are parsed into a HttpMessage object and that object is passed to an instance of IHttpMessageProcessor.</span></span>

### <a name="httpmessage"></a><span data-ttu-id="846c5-204">HttpMessage</span><span class="sxs-lookup"><span data-stu-id="846c5-204">HttpMessage</span></span>
<span data-ttu-id="846c5-205">A instância de `HttpMessage` contém três partes de dados:</span><span class="sxs-lookup"><span data-stu-id="846c5-205">The `HttpMessage` instance contains three pieces of data:</span></span>

```c#
public class HttpMessage
{
   public Guid MessageId { get; set; }
   public bool IsRequest { get; set; }
   public HttpRequestMessage HttpRequestMessage { get; set; }
   public HttpResponseMessage HttpResponseMessage { get; set; }

... parsing code snipped ...

}
```

<span data-ttu-id="846c5-206">A instância `HttpMessage` contém um GUID `MessageId` que nos permite conectar a solicitação HTTP à resposta HTTP correspondente e um valor booliano que identifica se o objeto contém uma instância de HttpRequestMessage e HttpResponseMessage.</span><span class="sxs-lookup"><span data-stu-id="846c5-206">The `HttpMessage` instance contains a `MessageId` GUID that allows us to connect the HTTP request to the corresponding HTTP response and a boolean value that identifies if the object contains an instance of a HttpRequestMessage and HttpResponseMessage.</span></span> <span data-ttu-id="846c5-207">Ao usar a compilação nas classes HTTP de `System.Net.Http`, pude aproveitar o código de análise `application/http` que é incluído em `System.Net.Http.Formatting`.</span><span class="sxs-lookup"><span data-stu-id="846c5-207">By using the built in HTTP classes from `System.Net.Http`, I was able to take advantage of the `application/http` parsing code that is included in `System.Net.Http.Formatting`.</span></span>  

### <a name="ihttpmessageprocessor"></a><span data-ttu-id="846c5-208">IHttpMessageProcessor</span><span class="sxs-lookup"><span data-stu-id="846c5-208">IHttpMessageProcessor</span></span>
<span data-ttu-id="846c5-209">A instância `HttpMessage` é então encaminhada para implementação de `IHttpMessageProcessor`, que é uma interface que criei para separar o recebimento e a interpretação do evento do Hub de Eventos do Azure e o processamento real dele.</span><span class="sxs-lookup"><span data-stu-id="846c5-209">The `HttpMessage` instance is then forwarded to implementation of `IHttpMessageProcessor` which is an interface I created to decouple the receiving and interpretation of the event from Azure Event Hub and the actual processing of it.</span></span>

## <a name="forwarding-the-http-message"></a><span data-ttu-id="846c5-210">Encaminhando a mensagem HTTP</span><span class="sxs-lookup"><span data-stu-id="846c5-210">Forwarding the HTTP message</span></span>
<span data-ttu-id="846c5-211">Para esse exemplo, decidi que seria interessante enviar a solicitação HTTP pelo [Runscope](http://www.runscope.com).</span><span class="sxs-lookup"><span data-stu-id="846c5-211">For this sample, I decided it would be interesting to push the HTTP Request over to [Runscope](http://www.runscope.com).</span></span> <span data-ttu-id="846c5-212">O Runscope é um serviço baseado em nuvem especializado em depuração, registro em log e monitoramento de HTTP.</span><span class="sxs-lookup"><span data-stu-id="846c5-212">Runscope is a cloud based service that specializes in HTTP debugging, logging and monitoring.</span></span> <span data-ttu-id="846c5-213">Ele tem uma camada gratuita para ser fácil testá-lo e nos permite ver as solicitações HTTP em tempo real fluindo pelo nosso serviço Gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="846c5-213">They have a free tier, so it is easy to try and it allows us to see the HTTP requests in real-time flowing through our API Management service.</span></span>

<span data-ttu-id="846c5-214">A implementação de `IHttpMessageProcessor` se parece com esta:</span><span class="sxs-lookup"><span data-stu-id="846c5-214">The `IHttpMessageProcessor` implementation looks like this,</span></span>

```c#
public class RunscopeHttpMessageProcessor : IHttpMessageProcessor
{
   private HttpClient _HttpClient;
   private ILogger _Logger;
   private string _BucketKey;
   public RunscopeHttpMessageProcessor(HttpClient httpClient, ILogger logger)
   {
       _HttpClient = httpClient;
       var key = Environment.GetEnvironmentVariable("APIMEVENTS-RUNSCOPE-KEY", EnvironmentVariableTarget.User);
       _HttpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("bearer", key);
       _HttpClient.BaseAddress = new Uri("https://api.runscope.com");
       _BucketKey = Environment.GetEnvironmentVariable("APIMEVENTS-RUNSCOPE-BUCKET", EnvironmentVariableTarget.User);
       _Logger = logger;
   }

   public async Task ProcessHttpMessage(HttpMessage message)
   {
       var runscopeMessage = new RunscopeMessage()
       {
           UniqueIdentifier = message.MessageId
       };

       if (message.IsRequest)
       {
           _Logger.LogInfo("Sending HTTP request " + message.MessageId.ToString());
           runscopeMessage.Request = await RunscopeRequest.CreateFromAsync(message.HttpRequestMessage);
       }
       else
       {
           _Logger.LogInfo("Sending HTTP response " + message.MessageId.ToString());
           runscopeMessage.Response = await RunscopeResponse.CreateFromAsync(message.HttpResponseMessage);
       }

       var messagesLink = new MessagesLink() { Method = HttpMethod.Post };
       messagesLink.BucketKey = _BucketKey;
       messagesLink.RunscopeMessage = runscopeMessage;
       var runscopeResponse = await _HttpClient.SendAsync(messagesLink.CreateRequest());
       _Logger.LogDebug("Request sent to Runscope");
   }
}
```

<span data-ttu-id="846c5-215">Eu pude usar uma [biblioteca de cliente existente do Runscope](http://www.nuget.org/packages/Runscope.net.hapikit/0.9.0-alpha) que facilita o envio por push instâncias de `HttpRequestMessage` e `HttpResponseMessage` para o respectivo serviço.</span><span class="sxs-lookup"><span data-stu-id="846c5-215">I was able to take advantage of an [existing client library for Runscope](http://www.nuget.org/packages/Runscope.net.hapikit/0.9.0-alpha) that makes it easy to push `HttpRequestMessage` and `HttpResponseMessage` instances up into their service.</span></span> <span data-ttu-id="846c5-216">Para acessar a API do Runscope, você precisará de uma conta e uma chave de API.</span><span class="sxs-lookup"><span data-stu-id="846c5-216">In order to access the Runscope API you will need an account and an API Key.</span></span> <span data-ttu-id="846c5-217">Instruções sobre como obter uma chave API podem ser encontradas no screencast [Criando aplicativos para acessar a API do Runscope](http://blog.runscope.com/posts/creating-applications-to-access-the-runscope-api) .</span><span class="sxs-lookup"><span data-stu-id="846c5-217">Instructions for getting an API key can be found in the [Creating Applications to Access Runscope API](http://blog.runscope.com/posts/creating-applications-to-access-the-runscope-api) screencast.</span></span>

## <a name="complete-sample"></a><span data-ttu-id="846c5-218">Exemplo completo</span><span class="sxs-lookup"><span data-stu-id="846c5-218">Complete sample</span></span>
<span data-ttu-id="846c5-219">O [código-fonte](https://github.com/darrelmiller/ApimEventProcessor) e os testes do exemplo estão no GitHub.</span><span class="sxs-lookup"><span data-stu-id="846c5-219">The [source code](https://github.com/darrelmiller/ApimEventProcessor) and tests for the sample are on GitHub.</span></span> <span data-ttu-id="846c5-220">Para executar o exemplo, você precisará de um [Serviço de Gerenciamento de API](api-management-get-started.md), de um [Hub de Eventos conectado](api-management-howto-log-event-hubs.md) e de uma [Conta de Armazenamento](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="846c5-220">You will need an [API Management Service](api-management-get-started.md), [a connected Event Hub](api-management-howto-log-event-hubs.md), and a [Storage Account](../storage/common/storage-create-storage-account.md) to run the sample for yourself.</span></span>   

<span data-ttu-id="846c5-221">O exemplo é apenas um aplicativo de console simples que escuta eventos originados no Hub de Eventos, os converte em objetos `HttpRequestMessage` e `HttpResponseMessage` e os encaminha para a API do Runscope.</span><span class="sxs-lookup"><span data-stu-id="846c5-221">The sample is just a simple Console application that listens for events coming from Event Hub, converts them into a `HttpRequestMessage` and `HttpResponseMessage` objects and then forwards them on to the Runscope API.</span></span>

<span data-ttu-id="846c5-222">Na imagem animada a seguir, você pode ver uma solicitação sendo feita em uma API no Portal do Desenvolvedor e o aplicativo de console que mostra a mensagem sendo recebida, processada e encaminhada. Em seguida, a solicitação e a resposta serão mostradas no Inspetor de tráfego do Runscope.</span><span class="sxs-lookup"><span data-stu-id="846c5-222">In the following animated image, you can see a request being made to an API in the Developer Portal, the Console application showing the message being received, processed and forwarded and then the request and response showing up in the Runscope Traffic inspector.</span></span>

![Demonstração da solicitação sendo encaminhada para o Runscope](./media/api-management-log-to-eventhub-sample/apim-eventhub-runscope.gif)

## <a name="summary"></a><span data-ttu-id="846c5-224">Resumo</span><span class="sxs-lookup"><span data-stu-id="846c5-224">Summary</span></span>
<span data-ttu-id="846c5-225">O serviço Gerenciamento de API do Azure fornece um lugar ideal para capturar o tráfego HTTP que entra e sai de suas APIs.</span><span class="sxs-lookup"><span data-stu-id="846c5-225">Azure API Management service provides an ideal place to capture the HTTP traffic travelling to and from your APIs.</span></span> <span data-ttu-id="846c5-226">Os Hubs de Eventos do Azure são uma solução escalonável de baixo custo para capturar esse tráfego e mantê-lo em sistemas de processamento secundários para registro em log, monitoramento e outras análise sofisticadas.</span><span class="sxs-lookup"><span data-stu-id="846c5-226">Azure Event Hubs is a highly scalable, low cost solution for capturing that traffic and feeding it into secondary processing systems for logging, monitoring and other sophisticated analytics.</span></span> <span data-ttu-id="846c5-227">A conexão a sistemas de monitoramento de tráfego de terceiros, como o Runscope, usa apenas algumas dezenas de linhas de código.</span><span class="sxs-lookup"><span data-stu-id="846c5-227">Connecting to 3rd party traffic monitoring systems like Runscope is a simple as a few dozen lines of code.</span></span>

## <a name="next-steps"></a><span data-ttu-id="846c5-228">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="846c5-228">Next steps</span></span>
* <span data-ttu-id="846c5-229">Saiba mais sobre Hubs de Eventos do Azure</span><span class="sxs-lookup"><span data-stu-id="846c5-229">Learn more about Azure Event Hubs</span></span>
  * [<span data-ttu-id="846c5-230">Introdução aos Hubs de Eventos do Azure</span><span class="sxs-lookup"><span data-stu-id="846c5-230">Get started with Azure Event Hubs</span></span>](../event-hubs/event-hubs-c-getstarted-send.md)
  * [<span data-ttu-id="846c5-231">Receber mensagens com EventProcessorHost</span><span class="sxs-lookup"><span data-stu-id="846c5-231">Receive messages with EventProcessorHost</span></span>](../event-hubs/event-hubs-dotnet-standard-getstarted-receive-eph.md)
  * [<span data-ttu-id="846c5-232">Guia de programação dos Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="846c5-232">Event Hubs programming guide</span></span>](../event-hubs/event-hubs-programming-guide.md)
* <span data-ttu-id="846c5-233">Saiba mais sobre a integração do Gerenciamento de API e Hubs de eventos</span><span class="sxs-lookup"><span data-stu-id="846c5-233">Learn more about API Management and Event Hubs integration</span></span>
  * [<span data-ttu-id="846c5-234">Como registrar eventos em log para Hubs de Eventos do Azure no Gerenciamento de API do Azure</span><span class="sxs-lookup"><span data-stu-id="846c5-234">How to log events to Azure Event Hubs in Azure API Management</span></span>](api-management-howto-log-event-hubs.md)
  * [<span data-ttu-id="846c5-235">Referência de entidade do agente</span><span class="sxs-lookup"><span data-stu-id="846c5-235">Logger entity reference</span></span>](https://msdn.microsoft.com/library/azure/mt592020.aspx)
  * [<span data-ttu-id="846c5-236">referência de política de log ao hub de eventos</span><span class="sxs-lookup"><span data-stu-id="846c5-236">log-to-eventhub policy reference</span></span>](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub)
