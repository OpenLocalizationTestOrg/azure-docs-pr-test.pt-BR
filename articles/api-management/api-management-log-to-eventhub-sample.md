---
title: aaaMonitor APIs com gerenciamento de API do Azure, os Hubs de eventos e Runscope | Microsoft Docs
description: "Aplicativo de exemplo demonstra a política de log para eventhub Olá por conexão gerenciamento de API do Azure, os Hubs de eventos do Azure e Runscope para HTTP, logs e monitoramento"
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
ms.openlocfilehash: 7456a2436f3a2d7b815b70b65fca9481d39c5fe9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-your-apis-with-azure-api-management-event-hubs-and-runscope"></a><span data-ttu-id="140ea-103">Monitorar suas APIs com o Gerenciamento de API do Azure, Hubs de Eventos e Runscope</span><span class="sxs-lookup"><span data-stu-id="140ea-103">Monitor your APIs with Azure API Management, Event Hubs and Runscope</span></span>
<span data-ttu-id="140ea-104">Olá [serviço de gerenciamento de API](api-management-key-concepts.md) fornece muitos recursos tooenhance Olá processamento de solicitações enviadas de HTTP tooyour API HTTP.</span><span class="sxs-lookup"><span data-stu-id="140ea-104">hello [API Management service](api-management-key-concepts.md) provides many capabilities tooenhance hello processing of HTTP requests sent tooyour HTTP API.</span></span> <span data-ttu-id="140ea-105">Olá no entanto, a existência de saudação solicitações e respostas são transitórias.</span><span class="sxs-lookup"><span data-stu-id="140ea-105">However, hello existence of hello requests and responses are transient.</span></span> <span data-ttu-id="140ea-106">Olá solicitação é feita e ela flui através de serviço de gerenciamento de API Olá backend do tooyour API.</span><span class="sxs-lookup"><span data-stu-id="140ea-106">hello request is made and it flows through hello API Management service tooyour backend API.</span></span> <span data-ttu-id="140ea-107">Sua API processa a solicitação de saudação e uma resposta flui através de consumidor toohello API.</span><span class="sxs-lookup"><span data-stu-id="140ea-107">Your API processes hello request and a response flows back through toohello API consumer.</span></span> <span data-ttu-id="140ea-108">Olá serviço de gerenciamento de API mantém algumas estatísticas importantes sobre Olá APIs para exibição no painel do portal do publicador hello, mas Além disso, detalhes de saudação serão excluídos.</span><span class="sxs-lookup"><span data-stu-id="140ea-108">hello API Management service keeps some important statistics about hello APIs for display in hello Publisher portal dashboard, but beyond that, hello details are gone.</span></span>

<span data-ttu-id="140ea-109">Usando Olá [log-eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) [política](api-management-howto-policies.md) em Olá serviço de gerenciamento de API pode enviar todos os detalhes do tooan de solicitação e resposta Olá [Hub de eventos do Azure](../event-hubs/event-hubs-what-is-event-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="140ea-109">By using hello [log-to-eventhub](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub) [policy](api-management-howto-policies.md) in hello API Management service you can send any details from hello request and response tooan [Azure Event Hub](../event-hubs/event-hubs-what-is-event-hubs.md).</span></span> <span data-ttu-id="140ea-110">Há uma variedade de motivos pelos quais você pode querer toogenerate eventos de mensagens HTTP enviadas tooyour APIs.</span><span class="sxs-lookup"><span data-stu-id="140ea-110">There are a variety of reasons why you may want toogenerate events from HTTP messages being sent tooyour APIs.</span></span> <span data-ttu-id="140ea-111">Alguns exemplos incluem trilha de auditoria de atualizações, análise de uso, alerta de exceção e integrações de terceiros.</span><span class="sxs-lookup"><span data-stu-id="140ea-111">Some examples include audit trail of updates, usage analytics, exception alerting and 3rd party integrations.</span></span>   

<span data-ttu-id="140ea-112">Este artigo demonstra como toocapture Olá toda solicitação e resposta de mensagem HTTP, enviá-lo tooan Hub de eventos e, em seguida, esse serviço de terceiros tooa de mensagem que fornece HTTP log e monitoramento dos serviços de retransmissão.</span><span class="sxs-lookup"><span data-stu-id="140ea-112">This article demonstrates how toocapture hello entire HTTP request and response message, send it tooan Event Hub and then relay that message tooa third party service that provides HTTP logging and monitoring services.</span></span>

## <a name="why-send-from-api-management-service"></a><span data-ttu-id="140ea-113">Por que enviar do serviço Gerenciamento de API?</span><span class="sxs-lookup"><span data-stu-id="140ea-113">Why Send From API Management Service?</span></span>
<span data-ttu-id="140ea-114">É possível toowrite HTTP middleware que conecte API HTTP estruturas toocapture solicitações e respostas HTTP e alimentam o registro e monitoramento de sistemas.</span><span class="sxs-lookup"><span data-stu-id="140ea-114">It is possible toowrite HTTP middleware that can plug into HTTP API frameworks toocapture HTTP requests and responses and feed them into logging and monitoring systems.</span></span> <span data-ttu-id="140ea-115">Olá desvantagem toothis consiste Olá HTTP middleware precisa toobe integrado a API de back-end hello e deve coincidir com a plataforma de saudação do hello API.</span><span class="sxs-lookup"><span data-stu-id="140ea-115">hello downside toothis approach is hello HTTP middleware needs toobe integrated into hello backend API and must match hello platform of hello API.</span></span> <span data-ttu-id="140ea-116">Se houver várias APIs cada um deles deve implantar Olá middleware.</span><span class="sxs-lookup"><span data-stu-id="140ea-116">If there are multiple APIs then each one must deploy hello middleware.</span></span> <span data-ttu-id="140ea-117">Normalmente, há motivos pelos quais as APIs de back-end não podem ser atualizadas.</span><span class="sxs-lookup"><span data-stu-id="140ea-117">Often there are reasons why backend APIs cannot be updated.</span></span>

<span data-ttu-id="140ea-118">Usando Olá toointegrate de serviço de gerenciamento de API do Azure com a infraestrutura de log fornece uma solução centralizada e independente de plataforma.</span><span class="sxs-lookup"><span data-stu-id="140ea-118">Using hello Azure API Management service toointegrate with logging infrastructure provides a centralized and platform-independent solution.</span></span> <span data-ttu-id="140ea-119">Também é escalonável, em parte devido toohello [georeplicação](api-management-howto-deploy-multi-region.md) recursos de gerenciamento de API do Azure.</span><span class="sxs-lookup"><span data-stu-id="140ea-119">It is also scalable, in part due toohello [geo-replication](api-management-howto-deploy-multi-region.md) capabilities of Azure API Management.</span></span>

## <a name="why-send-tooan-azure-event-hub"></a><span data-ttu-id="140ea-120">Por que enviar tooan Hub de eventos do Azure?</span><span class="sxs-lookup"><span data-stu-id="140ea-120">Why send tooan Azure Event Hub?</span></span>
<span data-ttu-id="140ea-121">É um tooask razoável, por que criar uma política de Hubs de eventos específico tooAzure?</span><span class="sxs-lookup"><span data-stu-id="140ea-121">It is a reasonable tooask, why create a policy that is specific tooAzure Event Hubs?</span></span> <span data-ttu-id="140ea-122">Há muitos lugares diferentes em que eu possa querer toolog Minhas solicitações.</span><span class="sxs-lookup"><span data-stu-id="140ea-122">There are many different places where I might want toolog my requests.</span></span> <span data-ttu-id="140ea-123">Por que não basta enviar Olá diretamente solicitações destino final toohello?</span><span class="sxs-lookup"><span data-stu-id="140ea-123">Why not just send hello requests directly toohello final destination?</span></span>  <span data-ttu-id="140ea-124">Essa é uma opção.</span><span class="sxs-lookup"><span data-stu-id="140ea-124">That is an option.</span></span> <span data-ttu-id="140ea-125">No entanto, ao fazer o registro em log solicitações de um serviço de gerenciamento de API, é necessário tooconsider como mensagens de log afetará o desempenho de saudação do hello API.</span><span class="sxs-lookup"><span data-stu-id="140ea-125">However, when making logging requests from an API management service, it is necessary tooconsider how logging messages will impact hello performance of hello API.</span></span> <span data-ttu-id="140ea-126">Os aumentos graduais na carga podem ser tratados aumentando as instâncias disponíveis dos componentes do sistema ou aproveitando a replicação geográfica.</span><span class="sxs-lookup"><span data-stu-id="140ea-126">Gradual increases in load can be handled by increasing available instances of system components or by taking advantage of geo-replication.</span></span> <span data-ttu-id="140ea-127">No entanto, curtos picos no tráfego podem causar solicitações toobe significativamente atrasada se a infra-estrutura de toologging solicitações iniciar tooslow sob carga.</span><span class="sxs-lookup"><span data-stu-id="140ea-127">However, short spikes in traffic can cause requests toobe significantly delayed if requests toologging infrastructure start tooslow under load.</span></span>

<span data-ttu-id="140ea-128">Olá Hubs de eventos do Azure é projetado tooingress grandes volumes de dados, com capacidade para lidar com um número muito maior de eventos que número de saudação do HTTP solicita a maioria dos processos APIs.</span><span class="sxs-lookup"><span data-stu-id="140ea-128">hello Azure Event Hubs is designed tooingress huge volumes of data, with capacity for dealing with a far higher number of events than hello number of HTTP requests most APIs process.</span></span> <span data-ttu-id="140ea-129">Olá Hub de eventos atua como um tipo de buffer sofisticado entre sua API serviço e hello infraestrutura de gerenciamento que armazenar e processar mensagens de saudação.</span><span class="sxs-lookup"><span data-stu-id="140ea-129">hello Event Hub acts as a kind of sophisticated buffer between your API management service and hello infrastructure that will store and process hello messages.</span></span> <span data-ttu-id="140ea-130">Isso garante que o desempenho de API não sofrerão devido a infraestrutura de log toohello.</span><span class="sxs-lookup"><span data-stu-id="140ea-130">This ensures that your API performance will not suffer due toohello logging infrastructure.</span></span>  

<span data-ttu-id="140ea-131">Quando dados saudação passou tooan Hub de eventos, ele é persistente e aguardará tooprocess de consumidores do Hub de eventos-lo.</span><span class="sxs-lookup"><span data-stu-id="140ea-131">Once hello data has been passed tooan Event Hub it is persisted and will wait for Event Hub consumers tooprocess it.</span></span> <span data-ttu-id="140ea-132">Olá Hub de eventos, não importa como ele será processado, apenas importantes sobre como verificar se a mensagem será entregue com êxito.</span><span class="sxs-lookup"><span data-stu-id="140ea-132">hello Event Hub does not care how it will be processed, it just cares about making sure hello message will be successfully delivered.</span></span>     

<span data-ttu-id="140ea-133">Hubs de eventos tem grupos de consumidores de toomultiple Olá capacidade toostream eventos.</span><span class="sxs-lookup"><span data-stu-id="140ea-133">Event Hubs have hello ability toostream events toomultiple consumer groups.</span></span> <span data-ttu-id="140ea-134">Isso permite que toobe eventos processado por sistemas completamente diferentes.</span><span class="sxs-lookup"><span data-stu-id="140ea-134">This allows events toobe processed by completely different systems.</span></span> <span data-ttu-id="140ea-135">Isso permite que o suporte a vários cenários de integração sem colocar os atrasos de adição Olá de processamento de solicitação de API Olá no serviço de gerenciamento de API hello como apenas um evento precisa toobe gerado na.</span><span class="sxs-lookup"><span data-stu-id="140ea-135">This enables supporting many integration scenarios without putting addition delays on hello processing of hello API request within hello API Management service as only one event needs toobe generated.</span></span>

## <a name="a-policy-toosend-applicationhttp-messages"></a><span data-ttu-id="140ea-136">Mensagens de aplicativo/http de toosend uma política</span><span class="sxs-lookup"><span data-stu-id="140ea-136">A policy toosend application/http messages</span></span>
<span data-ttu-id="140ea-137">Um Hub de Eventos aceita dados de evento como uma cadeia de caracteres simples.</span><span class="sxs-lookup"><span data-stu-id="140ea-137">An Event Hub accepts event data as a simple string.</span></span> <span data-ttu-id="140ea-138">conteúdo de saudação dessa cadeia de caracteres são completamente o tooyou.</span><span class="sxs-lookup"><span data-stu-id="140ea-138">hello contents of that string are completely up tooyou.</span></span> <span data-ttu-id="140ea-139">toopackage capaz de toobe até uma solicitação HTTP e enviá-la tooEvent Hubs precisamos tooformat cadeia de caracteres de saudação com informações de solicitação ou resposta hello.</span><span class="sxs-lookup"><span data-stu-id="140ea-139">toobe able toopackage up an HTTP request and send it off tooEvent Hubs we need tooformat hello string with hello request or response information.</span></span> <span data-ttu-id="140ea-140">Em situações como essa, se houver um formato existente que pode ser reutilizado, em seguida, pode não temos toowrite nosso própria análise de código.</span><span class="sxs-lookup"><span data-stu-id="140ea-140">In situations like this, if there is an existing format we can reuse, then we may not have toowrite our own parsing code.</span></span> <span data-ttu-id="140ea-141">Inicialmente, considerado usando Olá [HAR](http://www.softwareishard.com/blog/har-12-spec/) para enviar solicitações e respostas HTTP.</span><span class="sxs-lookup"><span data-stu-id="140ea-141">Initially I considered using hello [HAR](http://www.softwareishard.com/blog/har-12-spec/) for sending HTTP requests and responses.</span></span> <span data-ttu-id="140ea-142">No entanto, esse formato é otimizado para armazenar uma sequência de solicitações HTTP em um formato baseado em JSON.</span><span class="sxs-lookup"><span data-stu-id="140ea-142">However, this format is optimized for storing a sequence of HTTP requests in a JSON based format.</span></span> <span data-ttu-id="140ea-143">Continha um número de elementos obrigatórios que mais complexidade desnecessária para cenário de saudação de passar a mensagem de saudação HTTP conexão hello.</span><span class="sxs-lookup"><span data-stu-id="140ea-143">It contained a number of mandatory elements that added unnecessary complexity for hello scenario of passing hello HTTP message over hello wire.</span></span>  

<span data-ttu-id="140ea-144">Uma opção alternativa foi Olá toouse `application/http` tipo de mídia, conforme descrito na especificação de saudação HTTP [7230 RFC](http://tools.ietf.org/html/rfc7230).</span><span class="sxs-lookup"><span data-stu-id="140ea-144">An alternative option was toouse hello `application/http` media type as described in hello HTTP specification [RFC 7230](http://tools.ietf.org/html/rfc7230).</span></span> <span data-ttu-id="140ea-145">Esse tipo de mídia usa Olá exatamente o mesmo formato que é usado tooactually enviar mensagens de HTTP conexão hello, mas a mensagem de saudação do inteiro pode ser colocada no corpo de saudação da outra solicitação HTTP.</span><span class="sxs-lookup"><span data-stu-id="140ea-145">This media type uses hello exact same format that is used tooactually send HTTP messages over hello wire, but hello entire message can be put in hello body of another HTTP request.</span></span> <span data-ttu-id="140ea-146">Em nosso caso vamos apenas corpo de saudação toouse como tooEvent de toosend nossa mensagem Hubs.</span><span class="sxs-lookup"><span data-stu-id="140ea-146">In our case we are just going toouse hello body as our message toosend tooEvent Hubs.</span></span> <span data-ttu-id="140ea-147">Convenientemente, há um analisador que existe em [cliente do Microsoft ASP.NET Web API 2.2](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Client/) bibliotecas que podem analisar esse formato e convertê-la em Olá nativo `HttpRequestMessage` e `HttpResponseMessage` objetos.</span><span class="sxs-lookup"><span data-stu-id="140ea-147">Conveniently, there is a parser that exists in [Microsoft ASP.NET Web API 2.2 Client](https://www.nuget.org/packages/Microsoft.AspNet.WebApi.Client/) libraries that can parse this format and convert it into hello native `HttpRequestMessage` and `HttpResponseMessage` objects.</span></span>

<span data-ttu-id="140ea-148">toocreate capaz de toobe essa mensagem precisamos tootake aproveitar com base em c# [expressões de política](https://msdn.microsoft.com/library/azure/dn910913.aspx) no gerenciamento de API do Azure.</span><span class="sxs-lookup"><span data-stu-id="140ea-148">toobe able toocreate this message we need tootake advantage of C# based [Policy expressions](https://msdn.microsoft.com/library/azure/dn910913.aspx) in Azure API Management.</span></span> <span data-ttu-id="140ea-149">Aqui está a política Olá que envia um tooAzure de mensagem de solicitação HTTP Hubs de eventos.</span><span class="sxs-lookup"><span data-stu-id="140ea-149">Here is hello policy which sends a HTTP request message tooAzure Event Hubs.</span></span>

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

### <a name="policy-declaration"></a><span data-ttu-id="140ea-150">Declaração de política</span><span class="sxs-lookup"><span data-stu-id="140ea-150">Policy declaration</span></span>
<span data-ttu-id="140ea-151">Existem alguns itens específicos sobre essa expressão de política que vale a pena mencionar.</span><span class="sxs-lookup"><span data-stu-id="140ea-151">There a few particular things worth mentioning about this policy expression.</span></span> <span data-ttu-id="140ea-152">política de log para eventhub Olá tem um atributo chamado id de agente que se refere a toohello nome do agente de log que foi criado no hello serviço de gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="140ea-152">hello log-to-eventhub policy has an attribute called logger-id which refers toohello name of logger that has been created within hello API Management service.</span></span> <span data-ttu-id="140ea-153">Olá detalhes de como toosetup um agente de Hub de eventos no serviço de gerenciamento de API Olá pode ser encontrado no documento hello [como toolog eventos tooAzure Hubs de eventos de gerenciamento de API do Azure](api-management-howto-log-event-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="140ea-153">hello details of how toosetup an Event Hub logger in hello API Management service can be found in hello document [How toolog events tooAzure Event Hubs in Azure API Management](api-management-howto-log-event-hubs.md).</span></span> <span data-ttu-id="140ea-154">atributo segundo Olá é um parâmetro opcional que instrui o qual mensagem de saudação do toostore de partição em Hubs de eventos.</span><span class="sxs-lookup"><span data-stu-id="140ea-154">hello second attribute is an optional parameter that instructs Event Hubs which partition toostore hello message in.</span></span> <span data-ttu-id="140ea-155">Hubs de eventos usam partições tooenable scalabilty e exigem um mínimo de dois.</span><span class="sxs-lookup"><span data-stu-id="140ea-155">Event Hubs use partitions tooenable scalabilty and require a minimum of two.</span></span> <span data-ttu-id="140ea-156">Olá ordenados de entrega de mensagens é garantida apenas dentro de uma partição.</span><span class="sxs-lookup"><span data-stu-id="140ea-156">hello ordered delivery of messages is only guaranteed within a partition.</span></span> <span data-ttu-id="140ea-157">Se não podemos instruir o Hub de eventos na mensagem de saudação de tooplace qual partição, ele usará um algoritmo de round-robin toodistribute Olá de carga.</span><span class="sxs-lookup"><span data-stu-id="140ea-157">If we do not instruct Event Hub in which partition tooplace hello message, it will use a round-robin algorithm toodistribute hello load.</span></span> <span data-ttu-id="140ea-158">No entanto, que podem causar alguns dos nossos toobe de mensagens processada fora de ordem.</span><span class="sxs-lookup"><span data-stu-id="140ea-158">However, that may cause some of our messages toobe processed out of order.</span></span>  

### <a name="partitions"></a><span data-ttu-id="140ea-159">Partições</span><span class="sxs-lookup"><span data-stu-id="140ea-159">Partitions</span></span>
<span data-ttu-id="140ea-160">tooensure nossas mensagens são entregues tooconsumers em ordem e aproveitar o recurso de distribuição de carga de saudação de partições, escolhi partição tooone de mensagens de solicitação do toosend HTTP e HTTP resposta mensagens tooa segunda partição.</span><span class="sxs-lookup"><span data-stu-id="140ea-160">tooensure our messages are delivered tooconsumers in order and take advantage of hello load distribution capability of partitions, I chose toosend HTTP request messages tooone partition and HTTP response messages tooa second partition.</span></span> <span data-ttu-id="140ea-161">Isso garantirá uma distribuição de carga uniforme e que todas as solicitações e respostas sejam consumidas na ordem.</span><span class="sxs-lookup"><span data-stu-id="140ea-161">This will ensure an even load distribution and we can guarantee that all requests will be consumed in order and all responses will be consumed in order.</span></span> <span data-ttu-id="140ea-162">É possível que um toobe resposta consumido antes de solicitação correspondente hello, mas já que não é um problema porque temos um mecanismo diferente para correlacionar solicitações tooresponses e sabemos que solicitações vêm sempre antes de respostas.</span><span class="sxs-lookup"><span data-stu-id="140ea-162">It is possible for a response toobe consumed before hello corresponding request, but as that is not a problem as we have a different mechanism for correlating requests tooresponses and we know that requests always come before responses.</span></span>

### <a name="http-payloads"></a><span data-ttu-id="140ea-163">Cargas HTTP</span><span class="sxs-lookup"><span data-stu-id="140ea-163">HTTP payloads</span></span>
<span data-ttu-id="140ea-164">Depois de criar hello `requestLine` verificamos toosee se o corpo da solicitação Olá deve ser truncado.</span><span class="sxs-lookup"><span data-stu-id="140ea-164">After building hello `requestLine` we check toosee if hello request body should be truncated.</span></span> <span data-ttu-id="140ea-165">corpo da solicitação de saudação é truncado tooonly 1024.</span><span class="sxs-lookup"><span data-stu-id="140ea-165">hello request body is truncated tooonly 1024.</span></span> <span data-ttu-id="140ea-166">Isso pode ser aumentado, porém mensagens individuais do Hub de eventos são too256KB limitado, portanto, é provável que algumas mensagens HTTP agências será não caber em uma única mensagem.</span><span class="sxs-lookup"><span data-stu-id="140ea-166">This could be increased, however individual Event Hub messages are limited too256KB, so it is likely that some HTTP message bodies will not fit in a single message.</span></span> <span data-ttu-id="140ea-167">Ao fazer o registro em log e análise de uma quantidade significativa de informações podem ser derivadas de apenas a linha de solicitação HTTP hello e cabeçalhos.</span><span class="sxs-lookup"><span data-stu-id="140ea-167">When doing logging and analytics a significant amount of information can be derived from just hello HTTP request line and headers.</span></span> <span data-ttu-id="140ea-168">Além disso, muitas solicitações de API retornam somente os corpos de pequenos e perda de saudação do valor de informações truncando corpos grandes é mínima em redução de toohello de comparação de transferência, processamento e armazenamento custos tookeep todo o conteúdo do corpo.</span><span class="sxs-lookup"><span data-stu-id="140ea-168">Also, many API requests only return small bodies and so hello loss of information value by truncating large bodies is fairly minimal in comparison toohello reduction in transfer, processing and storage costs tookeep all body contents.</span></span> <span data-ttu-id="140ea-169">Uma observação final sobre processamento Olá corpo é que precisamos toopass `true` toohello como<string>método () porque ler o conteúdo do corpo hello, mas foi também deseja Olá API back-end toobe tooread capaz de saudação corpo.</span><span class="sxs-lookup"><span data-stu-id="140ea-169">One final note about processing hello body is that we need toopass `true` toohello As<string>() method because we are reading hello body contents, but was also want hello backend API toobe able tooread hello body.</span></span> <span data-ttu-id="140ea-170">Ao passar true toothis método fazemos o hello corpo toobe em buffer para que ele possa ser lido pela segunda vez.</span><span class="sxs-lookup"><span data-stu-id="140ea-170">By passing true toothis method we cause hello body toobe buffered so that it can be read a second time.</span></span> <span data-ttu-id="140ea-171">Isso é importante toobe atento se você tiver uma API que não o upload de arquivos muito grandes ou usa a sondagem longa.</span><span class="sxs-lookup"><span data-stu-id="140ea-171">This is important toobe aware of if you have an API that does uploading of very large files or uses long polling.</span></span> <span data-ttu-id="140ea-172">Nesses casos, seria melhor tooavoid ler o corpo da saudação em todos os.</span><span class="sxs-lookup"><span data-stu-id="140ea-172">In these cases it would be best tooavoid reading hello body at all.</span></span>   

### <a name="http-headers"></a><span data-ttu-id="140ea-173">Cabeçalhos HTTP</span><span class="sxs-lookup"><span data-stu-id="140ea-173">HTTP headers</span></span>
<span data-ttu-id="140ea-174">Cabeçalhos HTTP podem ser simplesmente transferidos por em formato de mensagem de saudação em um formato de par chave/valor simples.</span><span class="sxs-lookup"><span data-stu-id="140ea-174">HTTP Headers can be simply transferred over into hello message format in a simple key/value pair format.</span></span> <span data-ttu-id="140ea-175">Escolhemos toostrip determinados segurança confidenciais campos, tooavoid desnecessariamente vazamento de informações de credencial.</span><span class="sxs-lookup"><span data-stu-id="140ea-175">We have chosen toostrip out certain security sensitive fields, tooavoid unnecessarily leaking credential information.</span></span> <span data-ttu-id="140ea-176">É improvável que as chaves da API e outras credenciais sejam usadas para fins de análise.</span><span class="sxs-lookup"><span data-stu-id="140ea-176">It is unlikely that API keys and other credentials would be used for analytics purposes.</span></span> <span data-ttu-id="140ea-177">Se desejamos toodo análise no usuário hello e produto em particular Olá eles estão usando, foi possível obter que Olá `context` do objeto e adicionar mensagem toohello.</span><span class="sxs-lookup"><span data-stu-id="140ea-177">If we wish toodo analysis on hello user and hello particular product they are using then we could get that from hello `context` object and add that toohello message.</span></span>     

### <a name="message-metadata"></a><span data-ttu-id="140ea-178">Metadados da mensagem</span><span class="sxs-lookup"><span data-stu-id="140ea-178">Message Metadata</span></span>
<span data-ttu-id="140ea-179">Ao criar o hub de eventos do hello mensagem completa toosend toohello, a primeira linha de saudação não é parte da saudação `application/http` mensagem.</span><span class="sxs-lookup"><span data-stu-id="140ea-179">When building hello complete message toosend toohello event hub, hello first line is not actually part of hello `application/http` message.</span></span> <span data-ttu-id="140ea-180">Olá primeira linha é metadados adicionais que consiste em se a mensagem de saudação é uma mensagem de solicitação ou resposta e uma id de mensagem que é usado toocorrelate solicita tooresponses.</span><span class="sxs-lookup"><span data-stu-id="140ea-180">hello first line is additional metadata consisting of whether hello message is a request or response message and a message id which is used toocorrelate requests tooresponses.</span></span> <span data-ttu-id="140ea-181">id de mensagem de saudação é criada usando outra política que tem esta aparência:</span><span class="sxs-lookup"><span data-stu-id="140ea-181">hello message id is created by using another policy that looks like this:</span></span>

```xml
<set-variable name="message-id" value="@(Guid.NewGuid())" />
```

<span data-ttu-id="140ea-182">Poderíamos criar mensagem de solicitação hello, armazenada que em uma variável até Olá resposta foi retornada e simplesmente enviada Olá solicitação e resposta como uma única mensagem.</span><span class="sxs-lookup"><span data-stu-id="140ea-182">We could have created hello request message, stored that in a variable until hello response was returned and then simply sent hello request and response as a single message.</span></span> <span data-ttu-id="140ea-183">No entanto, envio de resposta e solicitação Olá independentemente e usando um toocorrelate de id de mensagem Olá dois, obtemos um pouco mais flexibilidade no tamanho da mensagem de saudação, Olá capacidade tootake aproveitar várias partições mantendo hello e ordem de mensagem solicitação será exibida em nosso painel log antecipadamente.</span><span class="sxs-lookup"><span data-stu-id="140ea-183">However, by sending hello request and response independently and using a message id toocorrelate hello two, we get a bit more flexibility in hello message size, hello ability tootake advantage of multiple partitions whilst maintaining message order and hello request will appear in our logging dashboard sooner.</span></span> <span data-ttu-id="140ea-184">Também pode haver alguns cenários em que uma resposta válida nunca é enviada para o hub de eventos toohello, possivelmente devido a erro de solicitação fatal tooa no serviço de gerenciamento de API hello, mas ainda teremos um registro de solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="140ea-184">There also may be some scenarios where a valid response is never sent toohello event hub, possibly due tooa fatal request error in hello API Management service, but we still will have a record of hello request.</span></span>

<span data-ttu-id="140ea-185">mensagem de HTTP de resposta Olá política toosend Olá parece muito semelhante solicitação de toohello e portanto Olá concluir configuração da política tem esta aparência:</span><span class="sxs-lookup"><span data-stu-id="140ea-185">hello policy toosend hello response HTTP message looks very similar toohello request and so hello complete policy configuration looks like this:</span></span>

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

<span data-ttu-id="140ea-186">Olá `set-variable` política cria um valor que é acessível por ambos os Olá `log-to-eventhub` política no hello `<inbound>` seção e hello `<outbound>` seção.</span><span class="sxs-lookup"><span data-stu-id="140ea-186">hello `set-variable` policy creates a value that is accessible by both hello `log-to-eventhub` policy in hello `<inbound>` section and hello `<outbound>` section.</span></span>  

## <a name="receiving-events-from-event-hubs"></a><span data-ttu-id="140ea-187">Recebendo eventos dos Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="140ea-187">Receiving events from Event Hubs</span></span>
<span data-ttu-id="140ea-188">Eventos do Hub de eventos do Azure são recebidos usando Olá [protocolo AMQP](http://www.amqp.org/).</span><span class="sxs-lookup"><span data-stu-id="140ea-188">Events from Azure Event Hub are received using hello [AMQP protocol](http://www.amqp.org/).</span></span> <span data-ttu-id="140ea-189">equipe do barramento de serviço do Microsoft Hello fez cliente Olá toomake disponíveis de bibliotecas consumindo eventos mais fácil.</span><span class="sxs-lookup"><span data-stu-id="140ea-189">hello Microsoft Service Bus team have made client libraries available toomake hello consuming events easier.</span></span> <span data-ttu-id="140ea-190">Há duas abordagens diferentes de suporte, um está sendo um *consumidor direto* e Olá outros usando Olá `EventProcessorHost` classe.</span><span class="sxs-lookup"><span data-stu-id="140ea-190">There are two different approaches supported, one is being a *Direct Consumer* and hello other is using hello `EventProcessorHost` class.</span></span> <span data-ttu-id="140ea-191">Exemplos dessas duas abordagens podem ser encontrados no hello [guia de programação de Hubs de evento](../event-hubs/event-hubs-programming-guide.md).</span><span class="sxs-lookup"><span data-stu-id="140ea-191">Examples of these two approaches can be found in hello [Event Hubs Programming Guide](../event-hubs/event-hubs-programming-guide.md).</span></span> <span data-ttu-id="140ea-192">é a versão curta Olá das diferenças hello, `Direct Consumer` lhe dá controle total e hello `EventProcessorHost` realiza-parte do trabalho Olá para você mas faz algumas suposições sobre como você processará os eventos.</span><span class="sxs-lookup"><span data-stu-id="140ea-192">hello short version of hello differences is, `Direct Consumer` gives you complete control and hello `EventProcessorHost` does some of hello plumbing work for you but makes certain assumptions about how you will process those events.</span></span>  

### <a name="eventprocessorhost"></a><span data-ttu-id="140ea-193">EventProcessorHost</span><span class="sxs-lookup"><span data-stu-id="140ea-193">EventProcessorHost</span></span>
<span data-ttu-id="140ea-194">Neste exemplo, usaremos Olá `EventProcessorHost` para manter a simplicidade, porém ele pode não Olá melhor opção para esse cenário específico.</span><span class="sxs-lookup"><span data-stu-id="140ea-194">In this sample, we will use hello `EventProcessorHost` for simplicity, however it may not hello best choice for this particular scenario.</span></span> <span data-ttu-id="140ea-195">`EventProcessorHost`Olá difícil trabalho de certificar-se de que você não tem tooworry sobre threading problemas dentro de uma classe de processador de determinado evento.</span><span class="sxs-lookup"><span data-stu-id="140ea-195">`EventProcessorHost` does hello hard work of making sure you don't have tooworry about threading issues within a particular event processor class.</span></span> <span data-ttu-id="140ea-196">No entanto, em nosso cenário, estamos simplesmente converter o formato de tooanother de mensagem de saudação e passá-lo ao longo do serviço de tooanother usando um método assíncrono.</span><span class="sxs-lookup"><span data-stu-id="140ea-196">However, in our scenario, we are simply converting hello message tooanother format and passing it along tooanother service using an async method.</span></span> <span data-ttu-id="140ea-197">Não há necessidade de atualizar o estado compartilhado e, portanto, nenhum risco de ter problemas de threading.</span><span class="sxs-lookup"><span data-stu-id="140ea-197">There is no need for updating shared state and therefore no risk of threading issues.</span></span> <span data-ttu-id="140ea-198">Na maioria dos cenários, `EventProcessorHost` provavelmente é Olá melhor opção e é certamente opção mais fácil de saudação.</span><span class="sxs-lookup"><span data-stu-id="140ea-198">For most scenarios, `EventProcessorHost` is probably hello best choice and it is certainly hello easier option.</span></span>     

### <a name="ieventprocessor"></a><span data-ttu-id="140ea-199">IEventProcessor</span><span class="sxs-lookup"><span data-stu-id="140ea-199">IEventProcessor</span></span>
<span data-ttu-id="140ea-200">conceito de saudação central ao usar `EventProcessorHost` é toocreate um uma implementação de saudação `IEventProcessor` interface que contém o método hello `ProcessEventAsync`.</span><span class="sxs-lookup"><span data-stu-id="140ea-200">hello central concept when using `EventProcessorHost` is toocreate a an implementation of hello `IEventProcessor` interface which contains hello method `ProcessEventAsync`.</span></span> <span data-ttu-id="140ea-201">essência Olá desse método é mostrada aqui:</span><span class="sxs-lookup"><span data-stu-id="140ea-201">hello essence of that method is shown here:</span></span>

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

<span data-ttu-id="140ea-202">Uma lista de objetos EventData são passados para o método hello e estamos iterar pela lista.</span><span class="sxs-lookup"><span data-stu-id="140ea-202">A list of EventData objects are passed into hello method and we iterate over that list.</span></span> <span data-ttu-id="140ea-203">bytes de saudação de cada método são analisadas em um objeto Mensagemhttp e esse objeto é passado a instância de tooan do IHttpMessageProcessor.</span><span class="sxs-lookup"><span data-stu-id="140ea-203">hello bytes of each method are parsed into a HttpMessage object and that object is passed tooan instance of IHttpMessageProcessor.</span></span>

### <a name="httpmessage"></a><span data-ttu-id="140ea-204">HttpMessage</span><span class="sxs-lookup"><span data-stu-id="140ea-204">HttpMessage</span></span>
<span data-ttu-id="140ea-205">Olá `HttpMessage` instância contém três partes de dados:</span><span class="sxs-lookup"><span data-stu-id="140ea-205">hello `HttpMessage` instance contains three pieces of data:</span></span>

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

<span data-ttu-id="140ea-206">Olá `HttpMessage` instância contém um `MessageId` GUID que nos permite solicitação de saudação HTTP tooconnect toohello resposta HTTP correspondente e um valor booleano de valor que identifica se o objeto Olá contém uma instância de uma HttpRequestMessage e HttpResponseMessage.</span><span class="sxs-lookup"><span data-stu-id="140ea-206">hello `HttpMessage` instance contains a `MessageId` GUID that allows us tooconnect hello HTTP request toohello corresponding HTTP response and a boolean value that identifies if hello object contains an instance of a HttpRequestMessage and HttpResponseMessage.</span></span> <span data-ttu-id="140ea-207">Usando Olá criado nas classes HTTP de `System.Net.Http`, foi tootake capaz de aproveitar Olá `application/http` análise de código que está incluído no `System.Net.Http.Formatting`.</span><span class="sxs-lookup"><span data-stu-id="140ea-207">By using hello built in HTTP classes from `System.Net.Http`, I was able tootake advantage of hello `application/http` parsing code that is included in `System.Net.Http.Formatting`.</span></span>  

### <a name="ihttpmessageprocessor"></a><span data-ttu-id="140ea-208">IHttpMessageProcessor</span><span class="sxs-lookup"><span data-stu-id="140ea-208">IHttpMessageProcessor</span></span>
<span data-ttu-id="140ea-209">Olá `HttpMessage` instância é então encaminhada tooimplementation de `IHttpMessageProcessor` que é uma interface que criei recebimento de saudação toodecouple e interpretação de evento de saudação do Hub de eventos do Azure e hello real de processamento dele.</span><span class="sxs-lookup"><span data-stu-id="140ea-209">hello `HttpMessage` instance is then forwarded tooimplementation of `IHttpMessageProcessor` which is an interface I created toodecouple hello receiving and interpretation of hello event from Azure Event Hub and hello actual processing of it.</span></span>

## <a name="forwarding-hello-http-message"></a><span data-ttu-id="140ea-210">Encaminhamento de mensagens HTTP de saudação</span><span class="sxs-lookup"><span data-stu-id="140ea-210">Forwarding hello HTTP message</span></span>
<span data-ttu-id="140ea-211">Para este exemplo, decidi seria interessante toopush Olá solicitação HTTP sobre muito[Runscope](http://www.runscope.com).</span><span class="sxs-lookup"><span data-stu-id="140ea-211">For this sample, I decided it would be interesting toopush hello HTTP Request over too[Runscope](http://www.runscope.com).</span></span> <span data-ttu-id="140ea-212">O Runscope é um serviço baseado em nuvem especializado em depuração, registro em log e monitoramento de HTTP.</span><span class="sxs-lookup"><span data-stu-id="140ea-212">Runscope is a cloud based service that specializes in HTTP debugging, logging and monitoring.</span></span> <span data-ttu-id="140ea-213">Eles têm uma camada gratuita, portanto, é fácil tootry e nos permite solicitações HTTP toosee Olá no fluxo em tempo real por meio de nosso serviço de gerenciamento de API.</span><span class="sxs-lookup"><span data-stu-id="140ea-213">They have a free tier, so it is easy tootry and it allows us toosee hello HTTP requests in real-time flowing through our API Management service.</span></span>

<span data-ttu-id="140ea-214">Olá `IHttpMessageProcessor` implementação parecida com esta,</span><span class="sxs-lookup"><span data-stu-id="140ea-214">hello `IHttpMessageProcessor` implementation looks like this,</span></span>

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
       _Logger.LogDebug("Request sent tooRunscope");
   }
}
```

<span data-ttu-id="140ea-215">Foi tootake capaz de aproveitar um [biblioteca de cliente existente para Runscope](http://www.nuget.org/packages/Runscope.net.hapikit/0.9.0-alpha) que torna mais fácil toopush `HttpRequestMessage` e `HttpResponseMessage` instâncias backup em seus serviços.</span><span class="sxs-lookup"><span data-stu-id="140ea-215">I was able tootake advantage of an [existing client library for Runscope](http://www.nuget.org/packages/Runscope.net.hapikit/0.9.0-alpha) that makes it easy toopush `HttpRequestMessage` and `HttpResponseMessage` instances up into their service.</span></span> <span data-ttu-id="140ea-216">Em ordem tooaccess Olá API Runscope você precisará de uma conta e uma chave de API.</span><span class="sxs-lookup"><span data-stu-id="140ea-216">In order tooaccess hello Runscope API you will need an account and an API Key.</span></span> <span data-ttu-id="140ea-217">Instruções sobre como obter uma chave de API pode ser encontrado no hello [criando aplicativos tooAccess Runscope API](http://blog.runscope.com/posts/creating-applications-to-access-the-runscope-api) screencast.</span><span class="sxs-lookup"><span data-stu-id="140ea-217">Instructions for getting an API key can be found in hello [Creating Applications tooAccess Runscope API](http://blog.runscope.com/posts/creating-applications-to-access-the-runscope-api) screencast.</span></span>

## <a name="complete-sample"></a><span data-ttu-id="140ea-218">Exemplo completo</span><span class="sxs-lookup"><span data-stu-id="140ea-218">Complete sample</span></span>
<span data-ttu-id="140ea-219">Olá [código-fonte](https://github.com/darrelmiller/ApimEventProcessor) e testes de exemplo hello no GitHub.</span><span class="sxs-lookup"><span data-stu-id="140ea-219">hello [source code](https://github.com/darrelmiller/ApimEventProcessor) and tests for hello sample are on GitHub.</span></span> <span data-ttu-id="140ea-220">Você precisará de um [serviço de gerenciamento de API](api-management-get-started.md), [um Hub de eventos conectado](api-management-howto-log-event-hubs.md)e um [conta de armazenamento](../storage/common/storage-create-storage-account.md) exemplo hello de toorun por conta própria.</span><span class="sxs-lookup"><span data-stu-id="140ea-220">You will need an [API Management Service](api-management-get-started.md), [a connected Event Hub](api-management-howto-log-event-hubs.md), and a [Storage Account](../storage/common/storage-create-storage-account.md) toorun hello sample for yourself.</span></span>   

<span data-ttu-id="140ea-221">exemplo Hello é apenas um aplicativo de Console simples que escuta para eventos do Hub de eventos, converte-os em uma `HttpRequestMessage` e `HttpResponseMessage` objetos e, em seguida, encaminha-os em toohello Runscope API.</span><span class="sxs-lookup"><span data-stu-id="140ea-221">hello sample is just a simple Console application that listens for events coming from Event Hub, converts them into a `HttpRequestMessage` and `HttpResponseMessage` objects and then forwards them on toohello Runscope API.</span></span>

<span data-ttu-id="140ea-222">Olá imagem animada a seguir, você pode ver uma solicitação seja feita tooan API no hello Portal do desenvolvedor, Olá Console aplicativo mostrando Olá recebimento de mensagem, processada e encaminhados e hello, em seguida, a solicitação e resposta aparecendo no hello tráfego Runscope Inspetor de propriedades.</span><span class="sxs-lookup"><span data-stu-id="140ea-222">In hello following animated image, you can see a request being made tooan API in hello Developer Portal, hello Console application showing hello message being received, processed and forwarded and then hello request and response showing up in hello Runscope Traffic inspector.</span></span>

![Demonstração de solicitação que está sendo encaminhada tooRunscope](./media/api-management-log-to-eventhub-sample/apim-eventhub-runscope.gif)

## <a name="summary"></a><span data-ttu-id="140ea-224">Resumo</span><span class="sxs-lookup"><span data-stu-id="140ea-224">Summary</span></span>
<span data-ttu-id="140ea-225">Serviço de gerenciamento de API do Azure fornece um local ideal toocapture Olá HTTP o tráfego entre períodos tooand de suas APIs.</span><span class="sxs-lookup"><span data-stu-id="140ea-225">Azure API Management service provides an ideal place toocapture hello HTTP traffic travelling tooand from your APIs.</span></span> <span data-ttu-id="140ea-226">Os Hubs de Eventos do Azure são uma solução escalonável de baixo custo para capturar esse tráfego e mantê-lo em sistemas de processamento secundários para registro em log, monitoramento e outras análise sofisticadas.</span><span class="sxs-lookup"><span data-stu-id="140ea-226">Azure Event Hubs is a highly scalable, low cost solution for capturing that traffic and feeding it into secondary processing systems for logging, monitoring and other sophisticated analytics.</span></span> <span data-ttu-id="140ea-227">Conectando too3rd sistemas como Runscope é um simples como algumas dezenas linhas de código de monitoramento de tráfego de terceiros.</span><span class="sxs-lookup"><span data-stu-id="140ea-227">Connecting too3rd party traffic monitoring systems like Runscope is a simple as a few dozen lines of code.</span></span>

## <a name="next-steps"></a><span data-ttu-id="140ea-228">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="140ea-228">Next steps</span></span>
* <span data-ttu-id="140ea-229">Saiba mais sobre Hubs de Eventos do Azure</span><span class="sxs-lookup"><span data-stu-id="140ea-229">Learn more about Azure Event Hubs</span></span>
  * [<span data-ttu-id="140ea-230">Introdução aos Hubs de Eventos do Azure</span><span class="sxs-lookup"><span data-stu-id="140ea-230">Get started with Azure Event Hubs</span></span>](../event-hubs/event-hubs-c-getstarted-send.md)
  * [<span data-ttu-id="140ea-231">Receber mensagens com EventProcessorHost</span><span class="sxs-lookup"><span data-stu-id="140ea-231">Receive messages with EventProcessorHost</span></span>](../event-hubs/event-hubs-dotnet-standard-getstarted-receive-eph.md)
  * [<span data-ttu-id="140ea-232">Guia de programação dos Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="140ea-232">Event Hubs programming guide</span></span>](../event-hubs/event-hubs-programming-guide.md)
* <span data-ttu-id="140ea-233">Saiba mais sobre a integração do Gerenciamento de API e Hubs de eventos</span><span class="sxs-lookup"><span data-stu-id="140ea-233">Learn more about API Management and Event Hubs integration</span></span>
  * [<span data-ttu-id="140ea-234">Como toolog eventos tooAzure Hubs de eventos de gerenciamento de API do Azure</span><span class="sxs-lookup"><span data-stu-id="140ea-234">How toolog events tooAzure Event Hubs in Azure API Management</span></span>](api-management-howto-log-event-hubs.md)
  * [<span data-ttu-id="140ea-235">Referência de entidade do agente</span><span class="sxs-lookup"><span data-stu-id="140ea-235">Logger entity reference</span></span>](https://msdn.microsoft.com/library/azure/mt592020.aspx)
  * [<span data-ttu-id="140ea-236">referência de política de log ao hub de eventos</span><span class="sxs-lookup"><span data-stu-id="140ea-236">log-to-eventhub policy reference</span></span>](https://msdn.microsoft.com/library/azure/dn894085.aspx#log-to-eventhub)
