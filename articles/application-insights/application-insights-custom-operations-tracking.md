---
title: "operações de aaaTrack personalizadas com o SDK do .NET do Azure Application Insights | Microsoft Docs"
description: "Acompanhar operações personalizadas com o SDK do .NET do Azure Application Insights"
services: application-insights
documentationcenter: .net
author: SergeyKanzhelev
manager: carmonm
ms.service: application-insights
ms.workload: TBD
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 06/31/2017
ms.author: sergkanz
ms.openlocfilehash: fe338d3e2b17a3dae43c96c60a19f57b3f46f0a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="track-custom-operations-with-application-insights-net-sdk"></a><span data-ttu-id="97c86-103">Acompanhar operações personalizadas com o SDK do .NET do Application Insights</span><span class="sxs-lookup"><span data-stu-id="97c86-103">Track custom operations with Application Insights .NET SDK</span></span>

<span data-ttu-id="97c86-104">Azure SDKs do Application Insights automaticamente acompanhar solicitações de HTTP de entrada e chama toodependent serviços, como solicitações HTTP e consultas SQL.</span><span class="sxs-lookup"><span data-stu-id="97c86-104">Azure Application Insights SDKs automatically track incoming HTTP requests and calls toodependent services, such as HTTP requests and SQL queries.</span></span> <span data-ttu-id="97c86-105">Rastreamento e a correlação de solicitações e dependências ofereçam visibilidade em capacidade de resposta e a confiabilidade do aplicativo inteiro hello em todos os microservices que combinam este aplicativo.</span><span class="sxs-lookup"><span data-stu-id="97c86-105">Tracking and correlation of requests and dependencies give you visibility into hello whole application's responsiveness and reliability across all microservices that combine this application.</span></span> 

<span data-ttu-id="97c86-106">Há uma classe de padrões de aplicativo que não pode ter suporte de maneira genérica.</span><span class="sxs-lookup"><span data-stu-id="97c86-106">There is a class of application patterns that can't be supported generically.</span></span> <span data-ttu-id="97c86-107">O monitoramento adequado de tais padrões requer a instrumentação de código manual.</span><span class="sxs-lookup"><span data-stu-id="97c86-107">Proper monitoring of such patterns requires manual code instrumentation.</span></span> <span data-ttu-id="97c86-108">Este artigo aborda alguns padrões que podem exigir a instrumentação manual, tais como processamento de fila personalizada e execução de tarefas em segundo plano de longa execução.</span><span class="sxs-lookup"><span data-stu-id="97c86-108">This article covers a few patterns that might require manual instrumentation, such as custom queue processing and running long-running background tasks.</span></span>

<span data-ttu-id="97c86-109">Este documento fornece orientação sobre como operações personalizadas de tootrack com hello SDK do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="97c86-109">This document provides guidance on how tootrack custom operations with hello Application Insights SDK.</span></span> <span data-ttu-id="97c86-110">Esta documentação é relevante para:</span><span class="sxs-lookup"><span data-stu-id="97c86-110">This documentation is relevant for:</span></span>

- <span data-ttu-id="97c86-111">Application Insights para a .NET (também conhecido como o SDK de Base) versão 2.4+.</span><span class="sxs-lookup"><span data-stu-id="97c86-111">Application Insights for .NET (also known as Base SDK) version 2.4+.</span></span>
- <span data-ttu-id="97c86-112">Application Insights para aplicativos Web (executando ASP.NET) versão 2.4+.</span><span class="sxs-lookup"><span data-stu-id="97c86-112">Application Insights for web applications (running ASP.NET) version 2.4+.</span></span>
- <span data-ttu-id="97c86-113">Application Insights para ASP.NET Core versão 2.1+.</span><span class="sxs-lookup"><span data-stu-id="97c86-113">Application Insights for ASP.NET Core version 2.1+.</span></span>

## <a name="overview"></a><span data-ttu-id="97c86-114">Visão geral</span><span class="sxs-lookup"><span data-stu-id="97c86-114">Overview</span></span>
<span data-ttu-id="97c86-115">Uma operação é um trabalho lógico executado por um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="97c86-115">An operation is a logical piece of work run by an application.</span></span> <span data-ttu-id="97c86-116">Ela tem nome, hora de início, duração e resultado, além de um contexto de execução como nome de usuário, propriedades e resultado.</span><span class="sxs-lookup"><span data-stu-id="97c86-116">It has a name, start time, duration, result, and a context of execution like user name, properties, and result.</span></span> <span data-ttu-id="97c86-117">Se a operação A tiver sido iniciada pela operação B, então a operação B será definida como pai para A. Uma operação pode ter somente um pai, mas pode ter muitas operações filhas.</span><span class="sxs-lookup"><span data-stu-id="97c86-117">If operation A was initiated by operation B, then operation B is set as a parent for A. An operation can have only one parent, but it can have many child operations.</span></span> <span data-ttu-id="97c86-118">Para obter mais informações sobre as operações e a correlação de telemetria, consulte [Correlação de telemetria do Azure Application Insights](application-insights-correlation.md).</span><span class="sxs-lookup"><span data-stu-id="97c86-118">For more information on operations and telemetry correlation, see [Azure Application Insights telemetry correlation](application-insights-correlation.md).</span></span>

<span data-ttu-id="97c86-119">Olá SDK .NET do Application Insights, operação Olá é descrita por classe abstrata Olá [OperationTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/Extensibility/Implementation/OperationTelemetry.cs) e seus descendentes [RequestTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/DataContracts/RequestTelemetry.cs) e [DependencyTelemetry ](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/DataContracts/DependencyTelemetry.cs).</span><span class="sxs-lookup"><span data-stu-id="97c86-119">In hello Application Insights .NET SDK, hello operation is described by hello abstract class [OperationTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/Extensibility/Implementation/OperationTelemetry.cs) and its descendants [RequestTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/DataContracts/RequestTelemetry.cs) and [DependencyTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/DataContracts/DependencyTelemetry.cs).</span></span>

## <a name="incoming-operations-tracking"></a><span data-ttu-id="97c86-120">Acompanhamento de operações de entrada</span><span class="sxs-lookup"><span data-stu-id="97c86-120">Incoming operations tracking</span></span> 
<span data-ttu-id="97c86-121">Olá web Application Insights que SDK coleta automaticamente as solicitações HTTP para aplicativos ASP.NET executados em um pipeline IIS e todos os aplicativos do ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="97c86-121">hello Application Insights web SDK automatically collects HTTP requests for ASP.NET applications that run in an IIS pipeline and all ASP.NET Core applications.</span></span> <span data-ttu-id="97c86-122">Há soluções com suporte da comunidade para outras plataformas e estruturas.</span><span class="sxs-lookup"><span data-stu-id="97c86-122">There are community-supported solutions for other platforms and frameworks.</span></span> <span data-ttu-id="97c86-123">No entanto, se o aplicativo hello não é suportado por qualquer uma das padrão hello ou soluções com suporte da comunidade, você pode instrumentá-lo manualmente.</span><span class="sxs-lookup"><span data-stu-id="97c86-123">However, if hello application isn't supported by any of hello standard or community-supported solutions, you can instrument it manually.</span></span>

<span data-ttu-id="97c86-124">Outro exemplo que requer um controle personalizado é trabalho Olá que recebe os itens da fila de saudação.</span><span class="sxs-lookup"><span data-stu-id="97c86-124">Another example that requires custom tracking is hello worker that receives items from hello queue.</span></span> <span data-ttu-id="97c86-125">Para alguns filas, Olá chamar tooadd uma mensagem na fila de toothis é controlada como uma dependência.</span><span class="sxs-lookup"><span data-stu-id="97c86-125">For some queues, hello call tooadd a message toothis queue is tracked as a dependency.</span></span> <span data-ttu-id="97c86-126">No entanto, operação Olá de alto nível que descreve o processamento de mensagens não é automaticamente coletada.</span><span class="sxs-lookup"><span data-stu-id="97c86-126">However, hello high-level operation that describes message processing is not automatically collected.</span></span>

<span data-ttu-id="97c86-127">Vamos ver como podemos acompanhar essas operações.</span><span class="sxs-lookup"><span data-stu-id="97c86-127">Let's see how we can track such operations.</span></span>

<span data-ttu-id="97c86-128">Em um nível alto, a tarefa de saudação é toocreate `RequestTelemetry` e definir propriedades conhecidas.</span><span class="sxs-lookup"><span data-stu-id="97c86-128">On a high level, hello task is toocreate `RequestTelemetry` and set known properties.</span></span> <span data-ttu-id="97c86-129">Após a conclusão da operação de hello, você pode acompanhar telemetria hello.</span><span class="sxs-lookup"><span data-stu-id="97c86-129">After hello operation is finished, you track hello telemetry.</span></span> <span data-ttu-id="97c86-130">saudação de exemplo a seguir demonstra essa tarefa.</span><span class="sxs-lookup"><span data-stu-id="97c86-130">hello following example demonstrates this task.</span></span>

### <a name="http-request-in-owin-self-hosted-app"></a><span data-ttu-id="97c86-131">Solicitação HTTP no aplicativo autohospedado Owin</span><span class="sxs-lookup"><span data-stu-id="97c86-131">HTTP request in Owin self-hosted app</span></span>
<span data-ttu-id="97c86-132">Neste exemplo, seguimos Olá [protocolo HTTP para correlação](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/HttpCorrelationProtocol.md).</span><span class="sxs-lookup"><span data-stu-id="97c86-132">In this example, we follow hello [HTTP Protocol for Correlation](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/HttpCorrelationProtocol.md).</span></span> <span data-ttu-id="97c86-133">Você deve esperar cabeçalhos tooreceive descritos existe.</span><span class="sxs-lookup"><span data-stu-id="97c86-133">You should expect tooreceive headers that are described there.</span></span>

``` C#
public class ApplicationInsightsMiddleware : OwinMiddleware
{
    private readonly TelemetryClient telemetryClient = new TelemetryClient(TelemetryConfiguration.Active);
    
    public ApplicationInsightsMiddleware(OwinMiddleware next) : base(next) {}

    public override async Task Invoke(IOwinContext context)
    {
        // Let's create and start RequestTelemetry.
        var requestTelemetry = new RequestTelemetry
        {
            Name = $"{context.Request.Method} {context.Request.Uri.GetLeftPart(UriPartial.Path)}"
        };

        // If there is a Request-Id received from hello upstream service, set hello telemetry context accordingly.
        if (context.Request.Headers.ContainsKey("Request-Id"))
        {
            var requestId = context.Request.Headers.Get("Request-Id");
            // Get hello operation ID from hello Request-Id (if you follow hello HTTP Protocol for Correlation).
            requestTelemetry.Context.Operation.Id = GetOperationId(requestId);
            requestTelemetry.Context.Operation.ParentId = requestId;
        }

        // StartOperation is a helper method that allows correlation of 
        // current operations with nested operations/telemetry
        // and initializes start time and duration on telemetry items.
        var operation = telemetryClient.StartOperation(requestTelemetry);

        // Process hello request.
        try
        {
            await Next.Invoke(context);
        }
        catch (Exception e)
        {
            requestTelemetry.Success = false;
            telemetryClient.TrackException(e);
            throw;
        }
        finally
        {
            // Update status code and success as appropriate.
            if (context.Response != null)
            {
                requestTelemetry.ResponseCode = context.Response.StatusCode.ToString();
                requestTelemetry.Success = context.Response.StatusCode >= 200 && context.Response.StatusCode <= 299;
            }
            else
            {
                requestTelemetry.Success = false;
            }

            // Now it's time toostop hello operation (and track telemetry).
            telemetryClient.StopOperation(operation);
        }
    }
    
    public static string GetOperationId(string id)
    {
        // Returns hello root ID from hello '|' toohello first '.' if any.
        int rootEnd = id.IndexOf('.');
        if (rootEnd < 0)
            rootEnd = id.Length;

        int rootStart = id[0] == '|' ? 1 : 0;
        return id.Substring(rootStart, rootEnd - rootStart);
    }
}
```

<span data-ttu-id="97c86-134">Olá protocolo HTTP para correlação também declara Olá `Correlation-Context` cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="97c86-134">hello HTTP Protocol for Correlation also declares hello `Correlation-Context` header.</span></span> <span data-ttu-id="97c86-135">No entanto, é omitido aqui para manter a simplicidade.</span><span class="sxs-lookup"><span data-stu-id="97c86-135">However, it's omitted here for simplicity.</span></span>

## <a name="queue-instrumentation"></a><span data-ttu-id="97c86-136">Instrumentação de fila</span><span class="sxs-lookup"><span data-stu-id="97c86-136">Queue instrumentation</span></span>
<span data-ttu-id="97c86-137">Para comunicação HTTP, criamos um protocolo toopass detalhes de correlação.</span><span class="sxs-lookup"><span data-stu-id="97c86-137">For HTTP communication, we've created a protocol toopass correlation details.</span></span> <span data-ttu-id="97c86-138">Com protocolos de alguns dos filas, você pode transmitir metadados adicionais junto com a mensagem de saudação e com outras pessoas que não é possível.</span><span class="sxs-lookup"><span data-stu-id="97c86-138">With some queues' protocols, you can pass additional metadata along with hello message, and with others you can't.</span></span>

### <a name="service-bus-queue"></a><span data-ttu-id="97c86-139">Fila do Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="97c86-139">Service Bus queue</span></span>
<span data-ttu-id="97c86-140">Com hello Azure [fila do barramento de serviço](../service-bus-messaging/index.md), você pode passar um recipiente de propriedades, junto com a mensagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="97c86-140">With hello Azure [Service Bus queue](../service-bus-messaging/index.md), you can pass a property bag along with hello message.</span></span> <span data-ttu-id="97c86-141">Nós usamos uma ID de correlação toopass hello.</span><span class="sxs-lookup"><span data-stu-id="97c86-141">We use it toopass hello correlation ID.</span></span>

<span data-ttu-id="97c86-142">fila do barramento de serviço Olá usa protocolos baseados em TCP.</span><span class="sxs-lookup"><span data-stu-id="97c86-142">hello Service Bus queue uses TCP-based protocols.</span></span> <span data-ttu-id="97c86-143">O Application Insights não acompanha automaticamente as operações de fila, então nós as acompanhamos manualmente.</span><span class="sxs-lookup"><span data-stu-id="97c86-143">Application Insights doesn't automatically track queue operations, so we track them manually.</span></span> <span data-ttu-id="97c86-144">Olá dequeue operação é uma API de estilo push e estamos não é possível tootrack-lo.</span><span class="sxs-lookup"><span data-stu-id="97c86-144">hello dequeue operation is a push-style API, and we're unable tootrack it.</span></span>

#### <a name="enqueue"></a><span data-ttu-id="97c86-145">Enfileirar</span><span class="sxs-lookup"><span data-stu-id="97c86-145">Enqueue</span></span>

```C#
public async Task Enqueue(string payload)
{
    // StartOperation is a helper method that initializes hello telemetry item
    // and allows correlation of this operation with its parent and children.
    var operation = telemetryClient.StartOperation<DependencyTelemetry>("enqueue " + queueName);
    operation.Telemetry.Type = "Queue";
    operation.Telemetry.Data = "Enqueue " + queueName;

    var message = new BrokeredMessage(payload);
    // Service Bus queue allows hello property bag toopass along with hello message.
    // We will use them toopass our correlation identifiers (and other context)
    // toohello consumer.
    message.Properties.Add("ParentId", operation.Telemetry.Id);
    message.Properties.Add("RootId", operation.Telemetry.Context.Operation.Id);

    try
    {
        await queue.SendAsync(message);
        
        // Set operation.Telemetry Success and ResponseCode here.
        operation.Telemetry.Success = true;
    }
    catch (Exception e)
    {
        telemetryClient.TrackException(e);
        // Set operation.Telemetry Success and ResponseCode here.
        operation.Telemetry.Success = false;
        throw;
    }
    finally
    {
        telemetryClient.StopOperation(operation);
    }
}
```

#### <a name="process"></a><span data-ttu-id="97c86-146">Processo</span><span class="sxs-lookup"><span data-stu-id="97c86-146">Process</span></span>
```C#
public async Task Process(BrokeredMessage message)
{
    // After hello message is taken from hello queue, create RequestTelemetry tootrack its processing.
    // It might also make sense tooget hello name from hello message.
    RequestTelemetry requestTelemetry = new RequestTelemetry { Name = "Dequeue " + queueName };

    var rootId = message.Properties["RootId"].ToString();
    var parentId = message.Properties["ParentId"].ToString();
    // Get hello operation ID from hello Request-Id (if you follow hello HTTP Protocol for Correlation).
    requestTelemetry.Context.Operation.Id = rootId;
    requestTelemetry.Context.Operation.ParentId = parentId;

    var operation = telemetryClient.StartOperation(requestTelemetry);

    try
    {
        await ProcessMessage();
    }
    catch (Exception e)
    {
        telemetryClient.TrackException(e);
        throw;
    }
    finally
    {
        // Update status code and success as appropriate.
        telemetryClient.StopOperation(operation);
    }
}
```

### <a name="azure-storage-queue"></a><span data-ttu-id="97c86-147">Fila de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="97c86-147">Azure Storage queue</span></span>
<span data-ttu-id="97c86-148">Olá mostrado no exemplo a seguir como Olá tootrack [fila de armazenamento do Azure](../storage/queues/storage-dotnet-how-to-use-queues.md) operações e correlacionar telemetria entre o produtor hello, consumidor hello e armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="97c86-148">hello following example shows how tootrack hello [Azure Storage queue](../storage/queues/storage-dotnet-how-to-use-queues.md) operations and correlate telemetry between hello producer, hello consumer, and Azure Storage.</span></span> 

<span data-ttu-id="97c86-149">fila de armazenamento Olá tem uma API HTTP.</span><span class="sxs-lookup"><span data-stu-id="97c86-149">hello Storage queue has an HTTP API.</span></span> <span data-ttu-id="97c86-150">Fila de toohello todas as chamadas são controladas pelo hello coletor de dependência do Application Insights para solicitações HTTP.</span><span class="sxs-lookup"><span data-stu-id="97c86-150">All calls toohello queue are tracked by hello Application Insights Dependency Collector for HTTP requests.</span></span>
<span data-ttu-id="97c86-151">Certifique-se de que `Microsoft.ApplicationInsights.DependencyCollector.HttpDependenciesParsingTelemetryInitializer` esteja em `applicationInsights.config`.</span><span class="sxs-lookup"><span data-stu-id="97c86-151">Make sure you have `Microsoft.ApplicationInsights.DependencyCollector.HttpDependenciesParsingTelemetryInitializer` in `applicationInsights.config`.</span></span> <span data-ttu-id="97c86-152">Se você não o fez, adicione-o programaticamente, conforme descrito em [filtragem e o pré-processamento de saudação do Azure SDK do Application Insights](app-insights-api-filtering-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="97c86-152">If you don't have it, add it programmatically as described in [Filtering and Preprocessing in hello Azure Application Insights SDK](app-insights-api-filtering-sampling.md).</span></span>

<span data-ttu-id="97c86-153">Se você configurar o Application Insights manualmente, certifique-se de criar e inicializar `Microsoft.ApplicationInsights.DependencyCollector.DependencyTrackingTelemetryModule` de maneira similar a:</span><span class="sxs-lookup"><span data-stu-id="97c86-153">If you configure Application Insights manually, make sure you create and initialize `Microsoft.ApplicationInsights.DependencyCollector.DependencyTrackingTelemetryModule` similarly to:</span></span>
 
``` C#
DependencyTrackingTelemetryModule module = new DependencyTrackingTelemetryModule();

// You can prevent correlation header injection toosome domains by adding it toohello excluded list.
// Make sure you add a Storage endpoint. Otherwise, you might experience request signature validation issues on hello Storage service side.
module.ExcludeComponentCorrelationHttpHeadersOnDomains.Add("core.windows.net");
module.Initialize(TelemetryConfiguration.Active);

// Do not forget toodispose of hello module during application shutdown.
```

<span data-ttu-id="97c86-154">Você também poderá toocorrelate Olá ID da operação do Application Insights com ID de solicitação de armazenamento hello.</span><span class="sxs-lookup"><span data-stu-id="97c86-154">You also might want toocorrelate hello Application Insights operation ID with hello Storage request ID.</span></span> <span data-ttu-id="97c86-155">Para obter informações sobre como tooset e obter um armazenamento de solicitação de cliente e uma ID de solicitação do servidor, consulte [monitorar, diagnosticar e solucionar problemas de armazenamento do Azure](../storage/common/storage-monitoring-diagnosing-troubleshooting.md#end-to-end-tracing).</span><span class="sxs-lookup"><span data-stu-id="97c86-155">For information on how tooset and get a Storage request client and a server request ID, see [Monitor, diagnose, and troubleshoot Azure Storage](../storage/common/storage-monitoring-diagnosing-troubleshooting.md#end-to-end-tracing).</span></span>

#### <a name="enqueue"></a><span data-ttu-id="97c86-156">Enfileirar</span><span class="sxs-lookup"><span data-stu-id="97c86-156">Enqueue</span></span>
<span data-ttu-id="97c86-157">Como as filas de armazenamento oferecem suporte a saudação API HTTP, todas as operações com fila Olá automaticamente são rastreadas pelo Application Insights.</span><span class="sxs-lookup"><span data-stu-id="97c86-157">Because Storage queues support hello HTTP API, all operations with hello queue are automatically tracked by Application Insights.</span></span> <span data-ttu-id="97c86-158">Em muitos casos, essa instrumentação deve ser suficiente.</span><span class="sxs-lookup"><span data-stu-id="97c86-158">In many cases, this instrumentation should be enough.</span></span> <span data-ttu-id="97c86-159">No entanto, toocorrelate rastreamentos no lado do consumidor Olá com rastreamentos de produtor, você deve passar algum contexto de correlação da mesma forma toohow fazemos isso no hello protocolo HTTP para correlação.</span><span class="sxs-lookup"><span data-stu-id="97c86-159">However, toocorrelate traces on hello consumer side with producer traces, you must pass some correlation context similarly toohow we do it in hello HTTP Protocol for Correlation.</span></span> 

<span data-ttu-id="97c86-160">Neste exemplo, podemos controlar Olá opcional `Enqueue` operação.</span><span class="sxs-lookup"><span data-stu-id="97c86-160">In this example, we track hello optional `Enqueue` operation.</span></span> <span data-ttu-id="97c86-161">Você pode:</span><span class="sxs-lookup"><span data-stu-id="97c86-161">You can:</span></span>

 - <span data-ttu-id="97c86-162">**Correlacionar tentativas (se houver)**: tiverem um pai comum que é hello `Enqueue` operação.</span><span class="sxs-lookup"><span data-stu-id="97c86-162">**Correlate retries (if any)**: They all have one common parent that's hello `Enqueue` operation.</span></span> <span data-ttu-id="97c86-163">Caso contrário, eles são rastreados como filhos da solicitação de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="97c86-163">Otherwise, they're tracked as children of hello incoming request.</span></span> <span data-ttu-id="97c86-164">Se houver várias filas de toohello solicitações lógico, talvez seja difícil toofind chamada resultou em novas tentativas.</span><span class="sxs-lookup"><span data-stu-id="97c86-164">If there are multiple logical requests toohello queue, it might be difficult toofind which call resulted in retries.</span></span>
 - <span data-ttu-id="97c86-165">**Correlacione os logs do Armazenamento (se e quando necessário)**: são correlacionados à telemetria do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="97c86-165">**Correlate Storage logs (if and when needed)**: They're correlated with Application Insights telemetry.</span></span>

<span data-ttu-id="97c86-166">Olá `Enqueue` operação é filho de saudação de uma operação do pai (por exemplo, uma solicitação de HTTP entrada).</span><span class="sxs-lookup"><span data-stu-id="97c86-166">hello `Enqueue` operation is hello child of a parent operation (for example, an incoming HTTP request).</span></span> <span data-ttu-id="97c86-167">chamada de dependência Olá HTTP é filho Olá Olá `Enqueue` neto hello e de operação de solicitação de entrada hello:</span><span class="sxs-lookup"><span data-stu-id="97c86-167">hello HTTP dependency call is hello child of hello `Enqueue` operation and hello grandchild of hello incoming request:</span></span>

```C#
public async Task Enqueue(CloudQueue queue, string message)
{
    var operation = telemetryClient.StartOperation<DependencyTelemetry>("enqueue " + queue.Name);
    operation.Telemetry.Type = "Queue";
    operation.Telemetry.Data = "Enqueue " + queue.Name;

    // MessagePayload represents your custom message and also serializes correlation identifiers into payload.
    // For example, if you choose toopass payload serialized tooJSON, it might look like
    // {'RootId' : 'some-id', 'ParentId' : '|some-id.1.2.3.', 'message' : 'your message tooprocess'}
    var jsonPayload = JsonConvert.SerializeObject(new MessagePayload
    {
        RootId = operation.Telemetry.Context.Operation.Id,
        ParentId = operation.Telemetry.Id,
        Payload = message
    });
    
    CloudQueueMessage queueMessage = new CloudQueueMessage(jsonPayload);

    // Add operation.Telemetry.Id toohello OperationContext toocorrelate Storage logs and Application Insights telemetry.
    OperationContext context = new OperationContext { ClientRequestID = operation.Telemetry.Id};

    try
    {
        await queue.AddMessageAsync(queueMessage, null, null, new QueueRequestOptions(), context);
    }
    catch (StorageException e)
    {
        operation.Telemetry.Properties.Add("AzureServiceRequestID", e.RequestInformation.ServiceRequestID);
        operation.Telemetry.Success = false;
        operation.Telemetry.ResultCode = e.RequestInformation.HttpStatusCode.ToString();
        telemetryClient.TrackException(e);
    }
    finally
    {
        // Update status code and success as appropriate.
        telemetryClient.StopOperation(operation);
    }
}  
```

<span data-ttu-id="97c86-168">relatórios de seu aplicativo com a quantidade de saudação tooreduce de telemetria ou se você não quiser Olá tootrack `Enqueue` operação por outros motivos, use Olá `Activity` API diretamente:</span><span class="sxs-lookup"><span data-stu-id="97c86-168">tooreduce hello amount of telemetry your application reports or if you don't want tootrack hello `Enqueue` operation for other reasons, use hello `Activity` API directly:</span></span>

- <span data-ttu-id="97c86-169">Criar (e iniciar) um novo `Activity` em vez de começar a operação do Application Insights hello.</span><span class="sxs-lookup"><span data-stu-id="97c86-169">Create (and start) a new `Activity` instead of starting hello Application Insights operation.</span></span> <span data-ttu-id="97c86-170">Fazer *não* necessário tooassign as propriedades nele, exceto o nome da operação hello.</span><span class="sxs-lookup"><span data-stu-id="97c86-170">You do *not* need tooassign any properties on it except hello operation name.</span></span>
- <span data-ttu-id="97c86-171">Serializar `yourActivity.Id` na carga de mensagem de saudação em vez de `operation.Telemetry.Id`.</span><span class="sxs-lookup"><span data-stu-id="97c86-171">Serialize `yourActivity.Id` into hello message payload instead of `operation.Telemetry.Id`.</span></span> <span data-ttu-id="97c86-172">Você também pode usar `Activity.Current.Id`.</span><span class="sxs-lookup"><span data-stu-id="97c86-172">You can also use `Activity.Current.Id`.</span></span>


#### <a name="dequeue"></a><span data-ttu-id="97c86-173">Remover da fila</span><span class="sxs-lookup"><span data-stu-id="97c86-173">Dequeue</span></span>
<span data-ttu-id="97c86-174">Da mesma forma muito`Enqueue`, automaticamente, uma fila de armazenamento real toohello de solicitação HTTP é controlada pelo Application Insights.</span><span class="sxs-lookup"><span data-stu-id="97c86-174">Similarly too`Enqueue`, an actual HTTP request toohello Storage queue is automatically tracked by Application Insights.</span></span> <span data-ttu-id="97c86-175">No entanto, Olá `Enqueue` operação supostamente ocorre no contexto de pai hello, como um contexto de solicitação de entrada.</span><span class="sxs-lookup"><span data-stu-id="97c86-175">However, hello `Enqueue` operation presumably happens in hello parent context, such as an incoming request context.</span></span> <span data-ttu-id="97c86-176">SDKs do Application Insights correlacionar automaticamente essa operação (e sua parte HTTP) com a solicitação de pai hello e outros telemetria relatado no hello mesmo escopo.</span><span class="sxs-lookup"><span data-stu-id="97c86-176">Application Insights SDKs automatically correlate such an operation (and its HTTP part) with hello parent request and other telemetry reported in hello same scope.</span></span>

<span data-ttu-id="97c86-177">Olá `Dequeue` operação é complicada.</span><span class="sxs-lookup"><span data-stu-id="97c86-177">hello `Dequeue` operation is tricky.</span></span> <span data-ttu-id="97c86-178">Olá SDK do Application Insights controla automaticamente as solicitações HTTP.</span><span class="sxs-lookup"><span data-stu-id="97c86-178">hello Application Insights SDK automatically tracks HTTP requests.</span></span> <span data-ttu-id="97c86-179">No entanto, ele não sabe o contexto de correlação de saudação até que a mensagem de saudação é analisada.</span><span class="sxs-lookup"><span data-stu-id="97c86-179">However, it doesn't know hello correlation context until hello message is parsed.</span></span> <span data-ttu-id="97c86-180">Não é uma mensagem de saudação toocorrelate possíveis Olá HTTP solicitação tooget com rest Olá de telemetria hello.</span><span class="sxs-lookup"><span data-stu-id="97c86-180">It's not possible toocorrelate hello HTTP request tooget hello message with hello rest of hello telemetry.</span></span>

<span data-ttu-id="97c86-181">Em muitos casos, talvez seja útil toocorrelate fila de toohello da solicitação de Olá HTTP com outros rastreamentos também.</span><span class="sxs-lookup"><span data-stu-id="97c86-181">In many cases, it might be useful toocorrelate hello HTTP request toohello queue with other traces as well.</span></span> <span data-ttu-id="97c86-182">Olá exemplo a seguir demonstra como toodo-lo:</span><span class="sxs-lookup"><span data-stu-id="97c86-182">hello following example demonstrates how toodo it:</span></span>

``` C#
public async Task<MessagePayload> Dequeue(CloudQueue queue)
{
    var telemetry = new DependencyTelemetry
    {
        Type = "Queue",
        Name = "Dequeue " + queue.Name
    };

    telemetry.Start();

    try
    {
        var message = await queue.GetMessageAsync();

        if (message != null)
        {
            var payload = JsonConvert.DeserializeObject<MessagePayload>(message.AsString);

            // If there is a message, we want toocorrelate hello Dequeue operation with processing.
            // However, we will only know what correlation ID toouse after we get it from hello message,
            // so we will report telemetry after we know hello IDs.
            telemetry.Context.Operation.Id = payload.RootId;
            telemetry.Context.Operation.ParentId = payload.ParentId;

            // Delete hello message.
            return payload;
        }
    }
    catch (StorageException e)
    {
        telemetry.Properties.Add("AzureServiceRequestID", e.RequestInformation.ServiceRequestID);
        telemetry.Success = false;
        telemetry.ResultCode = e.RequestInformation.HttpStatusCode.ToString();
        telemetryClient.TrackException(e);
    }
    finally
    {
        // Update status code and success as appropriate.
        telemetry.Stop();
        telemetryClient.Track(telemetry);
    }

    return null;
}
```

#### <a name="process"></a><span data-ttu-id="97c86-183">Processo</span><span class="sxs-lookup"><span data-stu-id="97c86-183">Process</span></span>

<span data-ttu-id="97c86-184">Em Olá exemplo a seguir, é uma mensagem de entrada de rastreamento de uma maneira da mesma forma toohow é um HTTP de entrada de rastreamento de solicitação:</span><span class="sxs-lookup"><span data-stu-id="97c86-184">In hello following example, we trace an incoming message in a manner similarly toohow we trace an incoming HTTP request:</span></span>

```C#
public async Task Process(MessagePayload message)
{
    // After hello message is dequeued from hello queue, create RequestTelemetry tootrack its processing.
    RequestTelemetry requestTelemetry = new RequestTelemetry { Name = "Dequeue " + queueName };
    // It might also make sense tooget hello name from hello message.
    requestTelemetry.Context.Operation.Id = message.RootId;
    requestTelemetry.Context.Operation.ParentId = message.ParentId;

    var operation = telemetryClient.StartOperation(requestTelemetry);

    try
    {
        await ProcessMessage();
    }
    catch (Exception e)
    {
        telemetryClient.TrackException(e);
        throw;
    }
    finally
    {
        // Update status code and success as appropriate.
        telemetryClient.StopOperation(operation);
    }
}
```

<span data-ttu-id="97c86-185">Da mesma forma, outras operações de fila podem ser instrumentadas.</span><span class="sxs-lookup"><span data-stu-id="97c86-185">Similarly, other queue operations can be instrumented.</span></span> <span data-ttu-id="97c86-186">Uma operação de espiar deve ser instrumentada da mesma maneira que uma operação de remoção da fila.</span><span class="sxs-lookup"><span data-stu-id="97c86-186">A peek operation should be instrumented in a similar way as a dequeue operation.</span></span> <span data-ttu-id="97c86-187">A instrumentação de operações de gerenciamento de fila não é necessária.</span><span class="sxs-lookup"><span data-stu-id="97c86-187">Instrumenting queue management operations isn't necessary.</span></span> <span data-ttu-id="97c86-188">O Application Insights acompanha operações como HTTP e, na maioria dos casos, isso é suficiente.</span><span class="sxs-lookup"><span data-stu-id="97c86-188">Application Insights tracks operations such as HTTP, and in most cases, it's enough.</span></span>

<span data-ttu-id="97c86-189">Quando você instrumentar a exclusão de mensagem, verifique se que definiu operação Olá identificadores (correlação).</span><span class="sxs-lookup"><span data-stu-id="97c86-189">When you instrument message deletion, make sure you set hello operation (correlation) identifiers.</span></span> <span data-ttu-id="97c86-190">Como alternativa, você pode usar o hello `Activity` API.</span><span class="sxs-lookup"><span data-stu-id="97c86-190">Alternatively, you can use hello `Activity` API.</span></span> <span data-ttu-id="97c86-191">Em seguida, você não precisa tooset identificadores de operação em itens de telemetria Olá porque Application Insights faz isso para você:</span><span class="sxs-lookup"><span data-stu-id="97c86-191">Then you don't need tooset operation identifiers on hello telemetry items because Application Insights does it for you:</span></span>

- <span data-ttu-id="97c86-192">Criar um novo `Activity` depois que você tem um item da fila de saudação.</span><span class="sxs-lookup"><span data-stu-id="97c86-192">Create a new `Activity` after you've got an item from hello queue.</span></span>
- <span data-ttu-id="97c86-193">Use `Activity.SetParentId(message.ParentId)` toocorrelate logs de produtor e consumidor.</span><span class="sxs-lookup"><span data-stu-id="97c86-193">Use `Activity.SetParentId(message.ParentId)` toocorrelate consumer and producer logs.</span></span>
- <span data-ttu-id="97c86-194">Iniciar Olá `Activity`.</span><span class="sxs-lookup"><span data-stu-id="97c86-194">Start hello `Activity`.</span></span>
- <span data-ttu-id="97c86-195">Acompanhe as operações de remoção da fila, processamento e exclusão usando auxiliares `Start/StopOperation`.</span><span class="sxs-lookup"><span data-stu-id="97c86-195">Track dequeue, process, and delete operations by using `Start/StopOperation` helpers.</span></span> <span data-ttu-id="97c86-196">Fazer isso da saudação mesmo assíncrona (contexto de execução) do fluxo de controle.</span><span class="sxs-lookup"><span data-stu-id="97c86-196">Do it from hello same asynchronous control flow (execution context).</span></span> <span data-ttu-id="97c86-197">Dessa forma, elas são correlacionadas corretamente.</span><span class="sxs-lookup"><span data-stu-id="97c86-197">In this way, they're correlated properly.</span></span>
- <span data-ttu-id="97c86-198">Saudação de parada `Activity`.</span><span class="sxs-lookup"><span data-stu-id="97c86-198">Stop hello `Activity`.</span></span>
- <span data-ttu-id="97c86-199">Use `Start/StopOperation` ou chame a telemetria `Track` manualmente.</span><span class="sxs-lookup"><span data-stu-id="97c86-199">Use `Start/StopOperation`, or call `Track` telemetry manually.</span></span>

### <a name="batch-processing"></a><span data-ttu-id="97c86-200">Processamento em lotes</span><span class="sxs-lookup"><span data-stu-id="97c86-200">Batch processing</span></span>
<span data-ttu-id="97c86-201">Com algumas filas, você pode remover da fila várias mensagens com uma solicitação.</span><span class="sxs-lookup"><span data-stu-id="97c86-201">With some queues, you can dequeue multiple messages with one request.</span></span> <span data-ttu-id="97c86-202">Processar essas mensagens supostamente independente e pertence toohello diferentes operações lógicas.</span><span class="sxs-lookup"><span data-stu-id="97c86-202">Processing such messages is presumably independent and belongs toohello different logical operations.</span></span> <span data-ttu-id="97c86-203">Nesse caso, não é possível toocorrelate Olá `Dequeue` processamento de mensagem de operação tooparticular.</span><span class="sxs-lookup"><span data-stu-id="97c86-203">In this case, it's not possible toocorrelate hello `Dequeue` operation tooparticular message processing.</span></span>

<span data-ttu-id="97c86-204">Cada mensagem deve ser processada no seu próprio fluxo de controle assíncrono.</span><span class="sxs-lookup"><span data-stu-id="97c86-204">Each message should be processed in its own asynchronous control flow.</span></span> <span data-ttu-id="97c86-205">Para obter mais informações, consulte Olá [dependências de saída de rastreamento](#outgoing-dependencies-tracking) seção.</span><span class="sxs-lookup"><span data-stu-id="97c86-205">For more information, see hello [Outgoing dependencies tracking](#outgoing-dependencies-tracking) section.</span></span>

## <a name="long-running-background-tasks"></a><span data-ttu-id="97c86-206">Tarefas em segundo plano de execução longa</span><span class="sxs-lookup"><span data-stu-id="97c86-206">Long-running background tasks</span></span>
<span data-ttu-id="97c86-207">Alguns aplicativos iniciam operações de longa execução que podem ser causadas por solicitações de usuário.</span><span class="sxs-lookup"><span data-stu-id="97c86-207">Some applications start long-running operations that might be caused by user requests.</span></span> <span data-ttu-id="97c86-208">Da perspectiva do rastreamento/instrumentação hello, não é diferente da instrumentação de solicitação ou de dependência:</span><span class="sxs-lookup"><span data-stu-id="97c86-208">From hello tracing/instrumentation perspective, it's not different from request or dependency instrumentation:</span></span> 

``` C#
async Task BackgroundTask()
{
    var operation = telemetryClient.StartOperation<RequestTelemetry>(taskName);
    operation.Telemetry.Type = "Background";
    try
    {
        int progress = 0;
        while (progress < 100)
        {
            // Process hello task.
            telemetryClient.TrackTrace($"done {progress++}%");
        }
        // Update status code and success as appropriate.
    }
    catch (Exception e)
    {
        telemetryClient.TrackException(e);
        // Update status code and success as appropriate.
        throw;
    }
    finally
    {
        telemetryClient.StopOperation(operation);
    }
}
```

<span data-ttu-id="97c86-209">Neste exemplo, usamos `telemetryClient.StartOperation` toocreate `RequestTelemetry` e o contexto de correlação de saudação do preenchimento.</span><span class="sxs-lookup"><span data-stu-id="97c86-209">In this example, we use `telemetryClient.StartOperation` toocreate `RequestTelemetry` and fill hello correlation context.</span></span> <span data-ttu-id="97c86-210">Digamos que você tenha uma operação de pai que foi criada por solicitações de entrada que Olá operação agendada.</span><span class="sxs-lookup"><span data-stu-id="97c86-210">Let's say you have a parent operation that was created by incoming requests that scheduled hello operation.</span></span> <span data-ttu-id="97c86-211">Enquanto `BackgroundTask` inicia no Olá mesmo fluxo de controle assíncrono como uma solicitação de entrada, ele está correlacionado a operação pai.</span><span class="sxs-lookup"><span data-stu-id="97c86-211">As long as `BackgroundTask` starts in hello same asynchronous control flow as an incoming request, it's correlated with that parent operation.</span></span> <span data-ttu-id="97c86-212">`BackgroundTask`e todos os itens de telemetria aninhados são automaticamente correlacionados a solicitação de saudação que fez com que ele, mesmo depois do término solicitação hello.</span><span class="sxs-lookup"><span data-stu-id="97c86-212">`BackgroundTask` and all nested telemetry items are automatically correlated with hello request that caused it, even after hello request ends.</span></span>

<span data-ttu-id="97c86-213">Quando a tarefa de saudação inicia de thread em segundo plano Olá que não tem qualquer operação (`Activity`) associado a ele, `BackgroundTask` não tem nenhum pai.</span><span class="sxs-lookup"><span data-stu-id="97c86-213">When hello task starts from hello background thread that doesn't have any operation (`Activity`) associated with it, `BackgroundTask` doesn't have any parent.</span></span> <span data-ttu-id="97c86-214">No entanto, ela pode ter operações aninhadas.</span><span class="sxs-lookup"><span data-stu-id="97c86-214">However, it can have nested operations.</span></span> <span data-ttu-id="97c86-215">Todos os itens de telemetria informados da tarefa de saudação são correlacionado toohello `RequestTelemetry` criado no `BackgroundTask`.</span><span class="sxs-lookup"><span data-stu-id="97c86-215">All telemetry items reported from hello task are correlated toohello `RequestTelemetry` created in `BackgroundTask`.</span></span>

## <a name="outgoing-dependencies-tracking"></a><span data-ttu-id="97c86-216">Acompanhamento de dependências de saída</span><span class="sxs-lookup"><span data-stu-id="97c86-216">Outgoing dependencies tracking</span></span>
<span data-ttu-id="97c86-217">Você pode controlar sua própria variante de dependência ou uma operação sem suporte pelo Application Insights.</span><span class="sxs-lookup"><span data-stu-id="97c86-217">You can track your own dependency kind or an operation that's not supported by Application Insights.</span></span>

<span data-ttu-id="97c86-218">Olá `Enqueue` método na fila do barramento de serviço hello ou fila de armazenamento Olá pode servir como exemplos de tal personalizado de controle.</span><span class="sxs-lookup"><span data-stu-id="97c86-218">hello `Enqueue` method in hello Service Bus queue or hello Storage queue can serve as examples for such custom tracking.</span></span>

<span data-ttu-id="97c86-219">a abordagem geral Olá para controle de dependência personalizada é:</span><span class="sxs-lookup"><span data-stu-id="97c86-219">hello general approach for custom dependency tracking is to:</span></span>

- <span data-ttu-id="97c86-220">Chamar hello `TelemetryClient.StartOperation` método (extensão) que preenche Olá `DependencyTelemetry` propriedades necessárias para correlação e algumas outras propriedades (hora de início do carimbo, duração).</span><span class="sxs-lookup"><span data-stu-id="97c86-220">Call hello `TelemetryClient.StartOperation` (extension) method that fills hello `DependencyTelemetry` properties that are needed for correlation and some other properties (start  time stamp, duration).</span></span>
- <span data-ttu-id="97c86-221">Definir outras propriedades personalizadas em Olá `DependencyTelemetry`, como nome de saudação e qualquer outro contexto é necessário.</span><span class="sxs-lookup"><span data-stu-id="97c86-221">Set other custom properties on hello `DependencyTelemetry`, such as hello name and any other context you need.</span></span>
- <span data-ttu-id="97c86-222">Fazer uma chamada de dependência e esperar por ela.</span><span class="sxs-lookup"><span data-stu-id="97c86-222">Make a dependency call and wait for it.</span></span>
- <span data-ttu-id="97c86-223">Parar a operação de saudação com `StopOperation` quando ele for concluído.</span><span class="sxs-lookup"><span data-stu-id="97c86-223">Stop hello operation with `StopOperation` when it's finished.</span></span>
- <span data-ttu-id="97c86-224">Tratar exceções.</span><span class="sxs-lookup"><span data-stu-id="97c86-224">Handle exceptions.</span></span>

<span data-ttu-id="97c86-225">`StopOperation`somente para operação de saudação que foi iniciada.</span><span class="sxs-lookup"><span data-stu-id="97c86-225">`StopOperation` only stops hello operation that was started.</span></span> <span data-ttu-id="97c86-226">Se operação em execução atual de saudação não corresponder a saudação um toostop, você deseja `StopOperation` não fará nada.</span><span class="sxs-lookup"><span data-stu-id="97c86-226">If hello current running operation doesn't match hello one you want toostop, `StopOperation` does nothing.</span></span> <span data-ttu-id="97c86-227">Essa situação pode ocorrer se você iniciar várias operações em paralelo no hello mesmo contexto de execução:</span><span class="sxs-lookup"><span data-stu-id="97c86-227">This situation might happen if you start multiple operations in parallel in hello same execution context:</span></span>

```C#
var firstOperation = telemetryClient.StartOperation<DependencyTelemetry>("task 1");
var firstOperation = telemetryClient.StartOperation<DependencyTelemetry>("task 1");
var firstTask = RunMyTaskAsync();

var secondOperation = telemetryClient.StartOperation<DependencyTelemetry>("task 2");
var secondTask = RunMyTaskAsync();

await firstTask;

// This will do nothing and will not report telemetry for hello first operation
// as currently secondOperation is active.
telemetryClient.StopOperation(firstOperation); 

await secondTask;
```

<span data-ttu-id="97c86-228">Certifique-se de sempre chamar `StartOperation` e executar a tarefa em seu próprio contexto:</span><span class="sxs-lookup"><span data-stu-id="97c86-228">Make sure you always call `StartOperation` and run your task in its own context:</span></span>
```C#
public async Task RunMyTaskAsync()
{
    var operation = telemetryClient.StartOperation<DependencyTelemetry>("task 1");
    try 
    {
        var myTask = await StartMyTaskAsync();
        // Update status code and success as appropriate.
    }
    catch(...) 
    {
        // Update status code and success as appropriate.
    }
    finally 
    {
        telemetryClient.StopOperation(operation);
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="97c86-229">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="97c86-229">Next steps</span></span>

- <span data-ttu-id="97c86-230">Conheça os fundamentos de saudação do [correlação de telemetria](application-insights-correlation.md) no Application Insights.</span><span class="sxs-lookup"><span data-stu-id="97c86-230">Learn hello basics of [telemetry correlation](application-insights-correlation.md) in Application Insights.</span></span>
- <span data-ttu-id="97c86-231">Consulte Olá [modelo de dados](application-insights-data-model.md) para modelo de dados e tipos de informações do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="97c86-231">See hello [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="97c86-232">Relatório personalizado [eventos e métricas](app-insights-api-custom-events-metrics.md) tooApplication Insights.</span><span class="sxs-lookup"><span data-stu-id="97c86-232">Report custom [events and metrics](app-insights-api-custom-events-metrics.md) tooApplication Insights.</span></span>
- <span data-ttu-id="97c86-233">Confira a [configuração](app-insights-configuration-with-applicationinsights-config.md#telemetry-initializers-aspnet) padrão para a coleção de propriedades de contexto.</span><span class="sxs-lookup"><span data-stu-id="97c86-233">Check out standard [configuration](app-insights-configuration-with-applicationinsights-config.md#telemetry-initializers-aspnet) for context properties collection.</span></span>
- <span data-ttu-id="97c86-234">Verificar Olá [guia do usuário System.Diagnostics.Activity](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/ActivityUserGuide.md) toosee como correlacionamos telemetria.</span><span class="sxs-lookup"><span data-stu-id="97c86-234">Check hello [System.Diagnostics.Activity User Guide](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/ActivityUserGuide.md) toosee how we correlate telemetry.</span></span>
