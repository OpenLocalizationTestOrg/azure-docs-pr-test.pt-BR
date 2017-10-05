---
title: "Acompanhar operações personalizadas com o SDK do .NET do Azure Application Insights | Microsoft Docs"
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
ms.openlocfilehash: b31d38fe2f7060597956a1ee9c66f43ce39d7240
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="track-custom-operations-with-application-insights-net-sdk"></a><span data-ttu-id="8feaa-103">Acompanhar operações personalizadas com o SDK do .NET do Application Insights</span><span class="sxs-lookup"><span data-stu-id="8feaa-103">Track custom operations with Application Insights .NET SDK</span></span>

<span data-ttu-id="8feaa-104">SDKs do Azure Application Insights acompanham automaticamente as solicitações HTTP de entrada e chamadas para serviços dependentes, como solicitações HTTP e consultas SQL.</span><span class="sxs-lookup"><span data-stu-id="8feaa-104">Azure Application Insights SDKs automatically track incoming HTTP requests and calls to dependent services, such as HTTP requests and SQL queries.</span></span> <span data-ttu-id="8feaa-105">O acompanhamento e a correlação de solicitações e dependências fornecem visibilidade sobre a capacidade de resposta e a confiabilidade do aplicativo inteiro em todos os microsserviços que combinados nesse aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8feaa-105">Tracking and correlation of requests and dependencies give you visibility into the whole application's responsiveness and reliability across all microservices that combine this application.</span></span> 

<span data-ttu-id="8feaa-106">Há uma classe de padrões de aplicativo que não pode ter suporte de maneira genérica.</span><span class="sxs-lookup"><span data-stu-id="8feaa-106">There is a class of application patterns that can't be supported generically.</span></span> <span data-ttu-id="8feaa-107">O monitoramento adequado de tais padrões requer a instrumentação de código manual.</span><span class="sxs-lookup"><span data-stu-id="8feaa-107">Proper monitoring of such patterns requires manual code instrumentation.</span></span> <span data-ttu-id="8feaa-108">Este artigo aborda alguns padrões que podem exigir a instrumentação manual, tais como processamento de fila personalizada e execução de tarefas em segundo plano de longa execução.</span><span class="sxs-lookup"><span data-stu-id="8feaa-108">This article covers a few patterns that might require manual instrumentation, such as custom queue processing and running long-running background tasks.</span></span>

<span data-ttu-id="8feaa-109">Este documento fornece diretrizes sobre como controlar operações personalizadas com o SDK do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="8feaa-109">This document provides guidance on how to track custom operations with the Application Insights SDK.</span></span> <span data-ttu-id="8feaa-110">Esta documentação é relevante para:</span><span class="sxs-lookup"><span data-stu-id="8feaa-110">This documentation is relevant for:</span></span>

- <span data-ttu-id="8feaa-111">Application Insights para a .NET (também conhecido como o SDK de Base) versão 2.4+.</span><span class="sxs-lookup"><span data-stu-id="8feaa-111">Application Insights for .NET (also known as Base SDK) version 2.4+.</span></span>
- <span data-ttu-id="8feaa-112">Application Insights para aplicativos Web (executando ASP.NET) versão 2.4+.</span><span class="sxs-lookup"><span data-stu-id="8feaa-112">Application Insights for web applications (running ASP.NET) version 2.4+.</span></span>
- <span data-ttu-id="8feaa-113">Application Insights para ASP.NET Core versão 2.1+.</span><span class="sxs-lookup"><span data-stu-id="8feaa-113">Application Insights for ASP.NET Core version 2.1+.</span></span>

## <a name="overview"></a><span data-ttu-id="8feaa-114">Visão geral</span><span class="sxs-lookup"><span data-stu-id="8feaa-114">Overview</span></span>
<span data-ttu-id="8feaa-115">Uma operação é um trabalho lógico executado por um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8feaa-115">An operation is a logical piece of work run by an application.</span></span> <span data-ttu-id="8feaa-116">Ela tem nome, hora de início, duração e resultado, além de um contexto de execução como nome de usuário, propriedades e resultado.</span><span class="sxs-lookup"><span data-stu-id="8feaa-116">It has a name, start time, duration, result, and a context of execution like user name, properties, and result.</span></span> <span data-ttu-id="8feaa-117">Se a operação A tiver sido iniciada pela operação B, então a operação B será definida como pai para A. Uma operação pode ter somente um pai, mas pode ter muitas operações filhas.</span><span class="sxs-lookup"><span data-stu-id="8feaa-117">If operation A was initiated by operation B, then operation B is set as a parent for A. An operation can have only one parent, but it can have many child operations.</span></span> <span data-ttu-id="8feaa-118">Para obter mais informações sobre as operações e a correlação de telemetria, consulte [Correlação de telemetria do Azure Application Insights](application-insights-correlation.md).</span><span class="sxs-lookup"><span data-stu-id="8feaa-118">For more information on operations and telemetry correlation, see [Azure Application Insights telemetry correlation](application-insights-correlation.md).</span></span>

<span data-ttu-id="8feaa-119">No SDK do .NET do Application Insights, a operação é descrita pela classe abstrata [OperationTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/Extensibility/Implementation/OperationTelemetry.cs) e seus descendentes [RequestTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/DataContracts/RequestTelemetry.cs) e [DependencyTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/DataContracts/DependencyTelemetry.cs).</span><span class="sxs-lookup"><span data-stu-id="8feaa-119">In the Application Insights .NET SDK, the operation is described by the abstract class [OperationTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/Extensibility/Implementation/OperationTelemetry.cs) and its descendants [RequestTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/DataContracts/RequestTelemetry.cs) and [DependencyTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/DataContracts/DependencyTelemetry.cs).</span></span>

## <a name="incoming-operations-tracking"></a><span data-ttu-id="8feaa-120">Acompanhamento de operações de entrada</span><span class="sxs-lookup"><span data-stu-id="8feaa-120">Incoming operations tracking</span></span> 
<span data-ttu-id="8feaa-121">O SDK da Web do Application Insights coleta automaticamente as solicitações HTTP para aplicativos ASP.NET executados em um pipeline do IIS e para todos os aplicativos do ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="8feaa-121">The Application Insights web SDK automatically collects HTTP requests for ASP.NET applications that run in an IIS pipeline and all ASP.NET Core applications.</span></span> <span data-ttu-id="8feaa-122">Há soluções com suporte da comunidade para outras plataformas e estruturas.</span><span class="sxs-lookup"><span data-stu-id="8feaa-122">There are community-supported solutions for other platforms and frameworks.</span></span> <span data-ttu-id="8feaa-123">No entanto, se o aplicativo não tiver suporte por nenhuma das soluções padrão ou com suporte pela comunidade, você poderá instrumentá-lo manualmente.</span><span class="sxs-lookup"><span data-stu-id="8feaa-123">However, if the application isn't supported by any of the standard or community-supported solutions, you can instrument it manually.</span></span>

<span data-ttu-id="8feaa-124">Outro exemplo que requer um acompanhamento personalizado é o trabalho que recebe os itens da fila.</span><span class="sxs-lookup"><span data-stu-id="8feaa-124">Another example that requires custom tracking is the worker that receives items from the queue.</span></span> <span data-ttu-id="8feaa-125">Para alguns filas, a chamada para adicionar uma mensagem a essa fila é acompanhada como dependência.</span><span class="sxs-lookup"><span data-stu-id="8feaa-125">For some queues, the call to add a message to this queue is tracked as a dependency.</span></span> <span data-ttu-id="8feaa-126">No entanto, a operação de alto nível que descreve o processamento de mensagens não é automaticamente coletada.</span><span class="sxs-lookup"><span data-stu-id="8feaa-126">However, the high-level operation that describes message processing is not automatically collected.</span></span>

<span data-ttu-id="8feaa-127">Vamos ver como podemos acompanhar essas operações.</span><span class="sxs-lookup"><span data-stu-id="8feaa-127">Let's see how we can track such operations.</span></span>

<span data-ttu-id="8feaa-128">Em um nível alto, a tarefa é criar `RequestTelemetry` e definir propriedades conhecidas.</span><span class="sxs-lookup"><span data-stu-id="8feaa-128">On a high level, the task is to create `RequestTelemetry` and set known properties.</span></span> <span data-ttu-id="8feaa-129">Depois que a operação for concluída, você poderá acompanhar a telemetria.</span><span class="sxs-lookup"><span data-stu-id="8feaa-129">After the operation is finished, you track the telemetry.</span></span> <span data-ttu-id="8feaa-130">O exemplo a seguir demonstra essa tarefa.</span><span class="sxs-lookup"><span data-stu-id="8feaa-130">The following example demonstrates this task.</span></span>

### <a name="http-request-in-owin-self-hosted-app"></a><span data-ttu-id="8feaa-131">Solicitação HTTP no aplicativo autohospedado Owin</span><span class="sxs-lookup"><span data-stu-id="8feaa-131">HTTP request in Owin self-hosted app</span></span>
<span data-ttu-id="8feaa-132">Neste exemplo, seguimos o [Protocolo HTTP para correlação](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/HttpCorrelationProtocol.md).</span><span class="sxs-lookup"><span data-stu-id="8feaa-132">In this example, we follow the [HTTP Protocol for Correlation](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/HttpCorrelationProtocol.md).</span></span> <span data-ttu-id="8feaa-133">Espere receber cabeçalhos descritos lá.</span><span class="sxs-lookup"><span data-stu-id="8feaa-133">You should expect to receive headers that are described there.</span></span>

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

        // If there is a Request-Id received from the upstream service, set the telemetry context accordingly.
        if (context.Request.Headers.ContainsKey("Request-Id"))
        {
            var requestId = context.Request.Headers.Get("Request-Id");
            // Get the operation ID from the Request-Id (if you follow the HTTP Protocol for Correlation).
            requestTelemetry.Context.Operation.Id = GetOperationId(requestId);
            requestTelemetry.Context.Operation.ParentId = requestId;
        }

        // StartOperation is a helper method that allows correlation of 
        // current operations with nested operations/telemetry
        // and initializes start time and duration on telemetry items.
        var operation = telemetryClient.StartOperation(requestTelemetry);

        // Process the request.
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

            // Now it's time to stop the operation (and track telemetry).
            telemetryClient.StopOperation(operation);
        }
    }
    
    public static string GetOperationId(string id)
    {
        // Returns the root ID from the '|' to the first '.' if any.
        int rootEnd = id.IndexOf('.');
        if (rootEnd < 0)
            rootEnd = id.Length;

        int rootStart = id[0] == '|' ? 1 : 0;
        return id.Substring(rootStart, rootEnd - rootStart);
    }
}
```

<span data-ttu-id="8feaa-134">O protocolo HTTP para correlação também declara o cabeçalho `Correlation-Context`.</span><span class="sxs-lookup"><span data-stu-id="8feaa-134">The HTTP Protocol for Correlation also declares the `Correlation-Context` header.</span></span> <span data-ttu-id="8feaa-135">No entanto, é omitido aqui para manter a simplicidade.</span><span class="sxs-lookup"><span data-stu-id="8feaa-135">However, it's omitted here for simplicity.</span></span>

## <a name="queue-instrumentation"></a><span data-ttu-id="8feaa-136">Instrumentação de fila</span><span class="sxs-lookup"><span data-stu-id="8feaa-136">Queue instrumentation</span></span>
<span data-ttu-id="8feaa-137">Para a comunicação HTTP, criamos um protocolo para passar os detalhes de correlação.</span><span class="sxs-lookup"><span data-stu-id="8feaa-137">For HTTP communication, we've created a protocol to pass correlation details.</span></span> <span data-ttu-id="8feaa-138">Com alguns protocolos de filas, você pode passar metadados adicionais junto com a mensagem e, com outros, não.</span><span class="sxs-lookup"><span data-stu-id="8feaa-138">With some queues' protocols, you can pass additional metadata along with the message, and with others you can't.</span></span>

### <a name="service-bus-queue"></a><span data-ttu-id="8feaa-139">Fila do Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="8feaa-139">Service Bus queue</span></span>
<span data-ttu-id="8feaa-140">Com a [fila do Barramento de Serviço](../service-bus-messaging/index.md) do Azure, você pode passar um recipiente de propriedades junto com a mensagem.</span><span class="sxs-lookup"><span data-stu-id="8feaa-140">With the Azure [Service Bus queue](../service-bus-messaging/index.md), you can pass a property bag along with the message.</span></span> <span data-ttu-id="8feaa-141">É usada para passar a ID de correlação.</span><span class="sxs-lookup"><span data-stu-id="8feaa-141">We use it to pass the correlation ID.</span></span>

<span data-ttu-id="8feaa-142">A Fila do Barramento de Serviço usa protocolos baseados em TCP.</span><span class="sxs-lookup"><span data-stu-id="8feaa-142">The Service Bus queue uses TCP-based protocols.</span></span> <span data-ttu-id="8feaa-143">O Application Insights não acompanha automaticamente as operações de fila, então nós as acompanhamos manualmente.</span><span class="sxs-lookup"><span data-stu-id="8feaa-143">Application Insights doesn't automatically track queue operations, so we track them manually.</span></span> <span data-ttu-id="8feaa-144">A operação de remover da fila é uma API de estilo push e não é possível acompanhá-la.</span><span class="sxs-lookup"><span data-stu-id="8feaa-144">The dequeue operation is a push-style API, and we're unable to track it.</span></span>

#### <a name="enqueue"></a><span data-ttu-id="8feaa-145">Enfileirar</span><span class="sxs-lookup"><span data-stu-id="8feaa-145">Enqueue</span></span>

```C#
public async Task Enqueue(string payload)
{
    // StartOperation is a helper method that initializes the telemetry item
    // and allows correlation of this operation with its parent and children.
    var operation = telemetryClient.StartOperation<DependencyTelemetry>("enqueue " + queueName);
    operation.Telemetry.Type = "Queue";
    operation.Telemetry.Data = "Enqueue " + queueName;

    var message = new BrokeredMessage(payload);
    // Service Bus queue allows the property bag to pass along with the message.
    // We will use them to pass our correlation identifiers (and other context)
    // to the consumer.
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

#### <a name="process"></a><span data-ttu-id="8feaa-146">Processo</span><span class="sxs-lookup"><span data-stu-id="8feaa-146">Process</span></span>
```C#
public async Task Process(BrokeredMessage message)
{
    // After the message is taken from the queue, create RequestTelemetry to track its processing.
    // It might also make sense to get the name from the message.
    RequestTelemetry requestTelemetry = new RequestTelemetry { Name = "Dequeue " + queueName };

    var rootId = message.Properties["RootId"].ToString();
    var parentId = message.Properties["ParentId"].ToString();
    // Get the operation ID from the Request-Id (if you follow the HTTP Protocol for Correlation).
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

### <a name="azure-storage-queue"></a><span data-ttu-id="8feaa-147">Fila de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="8feaa-147">Azure Storage queue</span></span>
<span data-ttu-id="8feaa-148">O exemplo a seguir mostra como acompanhar operações da [fila de Armazenamento do Azure](../storage/queues/storage-dotnet-how-to-use-queues.md) e correlacionar telemetria entre o produtor, o consumidor e o Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="8feaa-148">The following example shows how to track the [Azure Storage queue](../storage/queues/storage-dotnet-how-to-use-queues.md) operations and correlate telemetry between the producer, the consumer, and Azure Storage.</span></span> 

<span data-ttu-id="8feaa-149">A fila de Armazenamento tem uma API HTTP.</span><span class="sxs-lookup"><span data-stu-id="8feaa-149">The Storage queue has an HTTP API.</span></span> <span data-ttu-id="8feaa-150">Todas as chamadas à fila são rastreadas pelo coletor de dependência do Application Insights para solicitações HTTP.</span><span class="sxs-lookup"><span data-stu-id="8feaa-150">All calls to the queue are tracked by the Application Insights Dependency Collector for HTTP requests.</span></span>
<span data-ttu-id="8feaa-151">Certifique-se de que `Microsoft.ApplicationInsights.DependencyCollector.HttpDependenciesParsingTelemetryInitializer` esteja em `applicationInsights.config`.</span><span class="sxs-lookup"><span data-stu-id="8feaa-151">Make sure you have `Microsoft.ApplicationInsights.DependencyCollector.HttpDependenciesParsingTelemetryInitializer` in `applicationInsights.config`.</span></span> <span data-ttu-id="8feaa-152">Se você não tem, adicione-o programaticamente, conforme descrito em [Filtragem e pré-processamento no SDK do Azure Application Insights](app-insights-api-filtering-sampling.md).</span><span class="sxs-lookup"><span data-stu-id="8feaa-152">If you don't have it, add it programmatically as described in [Filtering and Preprocessing in the Azure Application Insights SDK](app-insights-api-filtering-sampling.md).</span></span>

<span data-ttu-id="8feaa-153">Se você configurar o Application Insights manualmente, certifique-se de criar e inicializar `Microsoft.ApplicationInsights.DependencyCollector.DependencyTrackingTelemetryModule` de maneira similar a:</span><span class="sxs-lookup"><span data-stu-id="8feaa-153">If you configure Application Insights manually, make sure you create and initialize `Microsoft.ApplicationInsights.DependencyCollector.DependencyTrackingTelemetryModule` similarly to:</span></span>
 
``` C#
DependencyTrackingTelemetryModule module = new DependencyTrackingTelemetryModule();

// You can prevent correlation header injection to some domains by adding it to the excluded list.
// Make sure you add a Storage endpoint. Otherwise, you might experience request signature validation issues on the Storage service side.
module.ExcludeComponentCorrelationHttpHeadersOnDomains.Add("core.windows.net");
module.Initialize(TelemetryConfiguration.Active);

// Do not forget to dispose of the module during application shutdown.
```

<span data-ttu-id="8feaa-154">Também convém correlacionar a ID da operação do Application Insights à ID de solicitação de Armazenamento.</span><span class="sxs-lookup"><span data-stu-id="8feaa-154">You also might want to correlate the Application Insights operation ID with the Storage request ID.</span></span> <span data-ttu-id="8feaa-155">Para obter informações sobre como definir e obter um cliente de solicitação de Armazenamento e uma ID de solicitação do servidor, consulte [Monitorar, diagnosticar e solucionar problemas do Armazenamento do Azure](../storage/common/storage-monitoring-diagnosing-troubleshooting.md#end-to-end-tracing).</span><span class="sxs-lookup"><span data-stu-id="8feaa-155">For information on how to set and get a Storage request client and a server request ID, see [Monitor, diagnose, and troubleshoot Azure Storage](../storage/common/storage-monitoring-diagnosing-troubleshooting.md#end-to-end-tracing).</span></span>

#### <a name="enqueue"></a><span data-ttu-id="8feaa-156">Enfileirar</span><span class="sxs-lookup"><span data-stu-id="8feaa-156">Enqueue</span></span>
<span data-ttu-id="8feaa-157">Como as filas de Armazenamento do Azure dão suporte a API HTTP, todas as operações com a fila automaticamente são acompanhadas pelo Application Insights.</span><span class="sxs-lookup"><span data-stu-id="8feaa-157">Because Storage queues support the HTTP API, all operations with the queue are automatically tracked by Application Insights.</span></span> <span data-ttu-id="8feaa-158">Em muitos casos, essa instrumentação deve ser suficiente.</span><span class="sxs-lookup"><span data-stu-id="8feaa-158">In many cases, this instrumentation should be enough.</span></span> <span data-ttu-id="8feaa-159">No entanto, para correlacionar rastreamentos no lado do consumidor com rastreamentos de produtor, você deve passar algum contexto de correlação de forma similar a como fazemos em Protocolo HTTP para Correlação.</span><span class="sxs-lookup"><span data-stu-id="8feaa-159">However, to correlate traces on the consumer side with producer traces, you must pass some correlation context similarly to how we do it in the HTTP Protocol for Correlation.</span></span> 

<span data-ttu-id="8feaa-160">Neste exemplo, podemos acompanhar a operação opcional `Enqueue`.</span><span class="sxs-lookup"><span data-stu-id="8feaa-160">In this example, we track the optional `Enqueue` operation.</span></span> <span data-ttu-id="8feaa-161">Você pode:</span><span class="sxs-lookup"><span data-stu-id="8feaa-161">You can:</span></span>

 - <span data-ttu-id="8feaa-162">**Correlacionar novas tentativas (se houver)**: todas têm um pai comum que é a operação `Enqueue`.</span><span class="sxs-lookup"><span data-stu-id="8feaa-162">**Correlate retries (if any)**: They all have one common parent that's the `Enqueue` operation.</span></span> <span data-ttu-id="8feaa-163">Caso contrário, elas são acompanhadas como filhos da solicitação de entrada.</span><span class="sxs-lookup"><span data-stu-id="8feaa-163">Otherwise, they're tracked as children of the incoming request.</span></span> <span data-ttu-id="8feaa-164">Se houver várias solicitações lógicas para a fila, pode ser difícil descobrir qual chamada resultou em novas tentativas.</span><span class="sxs-lookup"><span data-stu-id="8feaa-164">If there are multiple logical requests to the queue, it might be difficult to find which call resulted in retries.</span></span>
 - <span data-ttu-id="8feaa-165">**Correlacione os logs do Armazenamento (se e quando necessário)**: são correlacionados à telemetria do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="8feaa-165">**Correlate Storage logs (if and when needed)**: They're correlated with Application Insights telemetry.</span></span>

<span data-ttu-id="8feaa-166">A operação `Enqueue` é filho de uma operação pai (por exemplo, uma solicitação de HTTP entrada).</span><span class="sxs-lookup"><span data-stu-id="8feaa-166">The `Enqueue` operation is the child of a parent operation (for example, an incoming HTTP request).</span></span> <span data-ttu-id="8feaa-167">A chamada de dependência de HTTP é o filho da operação `Enqueue` e o neto da solicitação de entrada:</span><span class="sxs-lookup"><span data-stu-id="8feaa-167">The HTTP dependency call is the child of the `Enqueue` operation and the grandchild of the incoming request:</span></span>

```C#
public async Task Enqueue(CloudQueue queue, string message)
{
    var operation = telemetryClient.StartOperation<DependencyTelemetry>("enqueue " + queue.Name);
    operation.Telemetry.Type = "Queue";
    operation.Telemetry.Data = "Enqueue " + queue.Name;

    // MessagePayload represents your custom message and also serializes correlation identifiers into payload.
    // For example, if you choose to pass payload serialized to JSON, it might look like
    // {'RootId' : 'some-id', 'ParentId' : '|some-id.1.2.3.', 'message' : 'your message to process'}
    var jsonPayload = JsonConvert.SerializeObject(new MessagePayload
    {
        RootId = operation.Telemetry.Context.Operation.Id,
        ParentId = operation.Telemetry.Id,
        Payload = message
    });
    
    CloudQueueMessage queueMessage = new CloudQueueMessage(jsonPayload);

    // Add operation.Telemetry.Id to the OperationContext to correlate Storage logs and Application Insights telemetry.
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

<span data-ttu-id="8feaa-168">Para reduzir a quantidade de telemetria que o seu aplicativo relata ou se você não quiser acompanhar a operação `Enqueue` por outros motivos, use a API `Activity` diretamente:</span><span class="sxs-lookup"><span data-stu-id="8feaa-168">To reduce the amount of telemetry your application reports or if you don't want to track the `Enqueue` operation for other reasons, use the `Activity` API directly:</span></span>

- <span data-ttu-id="8feaa-169">Crie (e inicie) um novo `Activity` em vez de iniciar a operação do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="8feaa-169">Create (and start) a new `Activity` instead of starting the Application Insights operation.</span></span> <span data-ttu-id="8feaa-170">Você *não* precisa atribuir nenhuma propriedade a ele, exceto o nome da operação.</span><span class="sxs-lookup"><span data-stu-id="8feaa-170">You do *not* need to assign any properties on it except the operation name.</span></span>
- <span data-ttu-id="8feaa-171">Serializar `yourActivity.Id` para o conteúdo da mensagem, em vez de `operation.Telemetry.Id`.</span><span class="sxs-lookup"><span data-stu-id="8feaa-171">Serialize `yourActivity.Id` into the message payload instead of `operation.Telemetry.Id`.</span></span> <span data-ttu-id="8feaa-172">Você também pode usar `Activity.Current.Id`.</span><span class="sxs-lookup"><span data-stu-id="8feaa-172">You can also use `Activity.Current.Id`.</span></span>


#### <a name="dequeue"></a><span data-ttu-id="8feaa-173">Remover da fila</span><span class="sxs-lookup"><span data-stu-id="8feaa-173">Dequeue</span></span>
<span data-ttu-id="8feaa-174">Da mesma forma que `Enqueue`, a solicitação HTTP real para a fila de Armazenamento é acompanhada automaticamente pelo Application Insights.</span><span class="sxs-lookup"><span data-stu-id="8feaa-174">Similarly to `Enqueue`, an actual HTTP request to the Storage queue is automatically tracked by Application Insights.</span></span> <span data-ttu-id="8feaa-175">No entanto, a operação `Enqueue` supostamente ocorre no contexto de pai, como um contexto de solicitação de entrada.</span><span class="sxs-lookup"><span data-stu-id="8feaa-175">However, the `Enqueue` operation presumably happens in the parent context, such as an incoming request context.</span></span> <span data-ttu-id="8feaa-176">Os SDKs do Application Insights correlacionam automaticamente tal operação (e a parte HTTP dela) com a solicitação pai e outra telemetria relatada no mesmo escopo.</span><span class="sxs-lookup"><span data-stu-id="8feaa-176">Application Insights SDKs automatically correlate such an operation (and its HTTP part) with the parent request and other telemetry reported in the same scope.</span></span>

<span data-ttu-id="8feaa-177">A operação `Dequeue` é complicada.</span><span class="sxs-lookup"><span data-stu-id="8feaa-177">The `Dequeue` operation is tricky.</span></span> <span data-ttu-id="8feaa-178">O SDK do Application Insights acompanha automaticamente as solicitações HTTP.</span><span class="sxs-lookup"><span data-stu-id="8feaa-178">The Application Insights SDK automatically tracks HTTP requests.</span></span> <span data-ttu-id="8feaa-179">No entanto, ele não sabe o contexto de correlação até que a mensagem seja analisada.</span><span class="sxs-lookup"><span data-stu-id="8feaa-179">However, it doesn't know the correlation context until the message is parsed.</span></span> <span data-ttu-id="8feaa-180">Não é possível correlacionar a solicitação HTTP para obter a mensagem com o restante da telemetria.</span><span class="sxs-lookup"><span data-stu-id="8feaa-180">It's not possible to correlate the HTTP request to get the message with the rest of the telemetry.</span></span>

<span data-ttu-id="8feaa-181">Em muitos casos, pode ser útil correlacionar a solicitação HTTP à fila em outros rastreamentos também.</span><span class="sxs-lookup"><span data-stu-id="8feaa-181">In many cases, it might be useful to correlate the HTTP request to the queue with other traces as well.</span></span> <span data-ttu-id="8feaa-182">O exemplo a seguir demonstra como fazer isso:</span><span class="sxs-lookup"><span data-stu-id="8feaa-182">The following example demonstrates how to do it:</span></span>

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

            // If there is a message, we want to correlate the Dequeue operation with processing.
            // However, we will only know what correlation ID to use after we get it from the message,
            // so we will report telemetry after we know the IDs.
            telemetry.Context.Operation.Id = payload.RootId;
            telemetry.Context.Operation.ParentId = payload.ParentId;

            // Delete the message.
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

#### <a name="process"></a><span data-ttu-id="8feaa-183">Processo</span><span class="sxs-lookup"><span data-stu-id="8feaa-183">Process</span></span>

<span data-ttu-id="8feaa-184">No exemplo a seguir, acompanharemos uma mensagem de entrada da mesma forma como podemos acompanhar uma solicitação HTTP de entrada:</span><span class="sxs-lookup"><span data-stu-id="8feaa-184">In the following example, we trace an incoming message in a manner similarly to how we trace an incoming HTTP request:</span></span>

```C#
public async Task Process(MessagePayload message)
{
    // After the message is dequeued from the queue, create RequestTelemetry to track its processing.
    RequestTelemetry requestTelemetry = new RequestTelemetry { Name = "Dequeue " + queueName };
    // It might also make sense to get the name from the message.
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

<span data-ttu-id="8feaa-185">Da mesma forma, outras operações de fila podem ser instrumentadas.</span><span class="sxs-lookup"><span data-stu-id="8feaa-185">Similarly, other queue operations can be instrumented.</span></span> <span data-ttu-id="8feaa-186">Uma operação de espiar deve ser instrumentada da mesma maneira que uma operação de remoção da fila.</span><span class="sxs-lookup"><span data-stu-id="8feaa-186">A peek operation should be instrumented in a similar way as a dequeue operation.</span></span> <span data-ttu-id="8feaa-187">A instrumentação de operações de gerenciamento de fila não é necessária.</span><span class="sxs-lookup"><span data-stu-id="8feaa-187">Instrumenting queue management operations isn't necessary.</span></span> <span data-ttu-id="8feaa-188">O Application Insights acompanha operações como HTTP e, na maioria dos casos, isso é suficiente.</span><span class="sxs-lookup"><span data-stu-id="8feaa-188">Application Insights tracks operations such as HTTP, and in most cases, it's enough.</span></span>

<span data-ttu-id="8feaa-189">Ao instrumentar a exclusão de mensagem, verifique se você definiu os identificadores da operação (correlação).</span><span class="sxs-lookup"><span data-stu-id="8feaa-189">When you instrument message deletion, make sure you set the operation (correlation) identifiers.</span></span> <span data-ttu-id="8feaa-190">Como alternativa, você pode usar a API `Activity`.</span><span class="sxs-lookup"><span data-stu-id="8feaa-190">Alternatively, you can use the `Activity` API.</span></span> <span data-ttu-id="8feaa-191">Assim, você não precisa definir identificadores de operação nos itens de telemetria porque o Application Insights faz isso para você:</span><span class="sxs-lookup"><span data-stu-id="8feaa-191">Then you don't need to set operation identifiers on the telemetry items because Application Insights does it for you:</span></span>

- <span data-ttu-id="8feaa-192">Crie um novo `Activity` depois que tiver obtido um item da fila.</span><span class="sxs-lookup"><span data-stu-id="8feaa-192">Create a new `Activity` after you've got an item from the queue.</span></span>
- <span data-ttu-id="8feaa-193">Use `Activity.SetParentId(message.ParentId)` para correlacionar os logs de produtor e consumidor.</span><span class="sxs-lookup"><span data-stu-id="8feaa-193">Use `Activity.SetParentId(message.ParentId)` to correlate consumer and producer logs.</span></span>
- <span data-ttu-id="8feaa-194">Inicie o `Activity`.</span><span class="sxs-lookup"><span data-stu-id="8feaa-194">Start the `Activity`.</span></span>
- <span data-ttu-id="8feaa-195">Acompanhe as operações de remoção da fila, processamento e exclusão usando auxiliares `Start/StopOperation`.</span><span class="sxs-lookup"><span data-stu-id="8feaa-195">Track dequeue, process, and delete operations by using `Start/StopOperation` helpers.</span></span> <span data-ttu-id="8feaa-196">Faça isso do mesmo fluxo de controle assíncrono (contexto de execução).</span><span class="sxs-lookup"><span data-stu-id="8feaa-196">Do it from the same asynchronous control flow (execution context).</span></span> <span data-ttu-id="8feaa-197">Dessa forma, elas são correlacionadas corretamente.</span><span class="sxs-lookup"><span data-stu-id="8feaa-197">In this way, they're correlated properly.</span></span>
- <span data-ttu-id="8feaa-198">Pare o `Activity`.</span><span class="sxs-lookup"><span data-stu-id="8feaa-198">Stop the `Activity`.</span></span>
- <span data-ttu-id="8feaa-199">Use `Start/StopOperation` ou chame a telemetria `Track` manualmente.</span><span class="sxs-lookup"><span data-stu-id="8feaa-199">Use `Start/StopOperation`, or call `Track` telemetry manually.</span></span>

### <a name="batch-processing"></a><span data-ttu-id="8feaa-200">Processamento em lotes</span><span class="sxs-lookup"><span data-stu-id="8feaa-200">Batch processing</span></span>
<span data-ttu-id="8feaa-201">Com algumas filas, você pode remover da fila várias mensagens com uma solicitação.</span><span class="sxs-lookup"><span data-stu-id="8feaa-201">With some queues, you can dequeue multiple messages with one request.</span></span> <span data-ttu-id="8feaa-202">O processamento dessas mensagens é supostamente independente e pertence a diferentes operações lógicas.</span><span class="sxs-lookup"><span data-stu-id="8feaa-202">Processing such messages is presumably independent and belongs to the different logical operations.</span></span> <span data-ttu-id="8feaa-203">Nesse caso, não é possível correlacionar a operação `Dequeue` a um processamento de mensagem específico.</span><span class="sxs-lookup"><span data-stu-id="8feaa-203">In this case, it's not possible to correlate the `Dequeue` operation to particular message processing.</span></span>

<span data-ttu-id="8feaa-204">Cada mensagem deve ser processada no seu próprio fluxo de controle assíncrono.</span><span class="sxs-lookup"><span data-stu-id="8feaa-204">Each message should be processed in its own asynchronous control flow.</span></span> <span data-ttu-id="8feaa-205">Para obter mais informações, consulte a seção [Acompanhamento de dependências de saída](#outgoing-dependencies-tracking).</span><span class="sxs-lookup"><span data-stu-id="8feaa-205">For more information, see the [Outgoing dependencies tracking](#outgoing-dependencies-tracking) section.</span></span>

## <a name="long-running-background-tasks"></a><span data-ttu-id="8feaa-206">Tarefas em segundo plano de execução longa</span><span class="sxs-lookup"><span data-stu-id="8feaa-206">Long-running background tasks</span></span>
<span data-ttu-id="8feaa-207">Alguns aplicativos iniciam operações de longa execução que podem ser causadas por solicitações de usuário.</span><span class="sxs-lookup"><span data-stu-id="8feaa-207">Some applications start long-running operations that might be caused by user requests.</span></span> <span data-ttu-id="8feaa-208">Da perspectiva do rastreamento/instrumentação, isso não é diferente da instrumentação de solicitação ou de dependência:</span><span class="sxs-lookup"><span data-stu-id="8feaa-208">From the tracing/instrumentation perspective, it's not different from request or dependency instrumentation:</span></span> 

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
            // Process the task.
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

<span data-ttu-id="8feaa-209">Neste exemplo, usamos `telemetryClient.StartOperation` para criar `RequestTelemetry` e preencher o contexto de correlação.</span><span class="sxs-lookup"><span data-stu-id="8feaa-209">In this example, we use `telemetryClient.StartOperation` to create `RequestTelemetry` and fill the correlation context.</span></span> <span data-ttu-id="8feaa-210">Digamos que você tem uma operação pai criada por solicitações de entrada que agendaram a operação.</span><span class="sxs-lookup"><span data-stu-id="8feaa-210">Let's say you have a parent operation that was created by incoming requests that scheduled the operation.</span></span> <span data-ttu-id="8feaa-211">Desde que `BackgroundTask` inicie no mesmo fluxo de controle assíncrono que uma solicitação de entrada, ela será correlacionada com essa operação pai.</span><span class="sxs-lookup"><span data-stu-id="8feaa-211">As long as `BackgroundTask` starts in the same asynchronous control flow as an incoming request, it's correlated with that parent operation.</span></span> <span data-ttu-id="8feaa-212">`BackgroundTask` e todos os itens de telemetria aninhados são automaticamente correlacionados com a solicitação a causou, mesmo após o término da solicitação.</span><span class="sxs-lookup"><span data-stu-id="8feaa-212">`BackgroundTask` and all nested telemetry items are automatically correlated with the request that caused it, even after the request ends.</span></span>

<span data-ttu-id="8feaa-213">Quando a tarefa inicia do thread em segundo plano que não tem nenhuma operação (`Activity`) associada a ele, `BackgroundTask` não tem nenhum pai.</span><span class="sxs-lookup"><span data-stu-id="8feaa-213">When the task starts from the background thread that doesn't have any operation (`Activity`) associated with it, `BackgroundTask` doesn't have any parent.</span></span> <span data-ttu-id="8feaa-214">No entanto, ela pode ter operações aninhadas.</span><span class="sxs-lookup"><span data-stu-id="8feaa-214">However, it can have nested operations.</span></span> <span data-ttu-id="8feaa-215">Todos os itens de telemetria relatados da tarefa estão correlacionados à `RequestTelemetry` criada na `BackgroundTask`.</span><span class="sxs-lookup"><span data-stu-id="8feaa-215">All telemetry items reported from the task are correlated to the `RequestTelemetry` created in `BackgroundTask`.</span></span>

## <a name="outgoing-dependencies-tracking"></a><span data-ttu-id="8feaa-216">Acompanhamento de dependências de saída</span><span class="sxs-lookup"><span data-stu-id="8feaa-216">Outgoing dependencies tracking</span></span>
<span data-ttu-id="8feaa-217">Você pode controlar sua própria variante de dependência ou uma operação sem suporte pelo Application Insights.</span><span class="sxs-lookup"><span data-stu-id="8feaa-217">You can track your own dependency kind or an operation that's not supported by Application Insights.</span></span>

<span data-ttu-id="8feaa-218">O método `Enqueue` na fila do Barramento de Serviço ou fila de Armazenamento pode servir como exemplos de tal acompanhamento personalizado.</span><span class="sxs-lookup"><span data-stu-id="8feaa-218">The `Enqueue` method in the Service Bus queue or the Storage queue can serve as examples for such custom tracking.</span></span>

<span data-ttu-id="8feaa-219">A abordagem geral ao acompanhamento de dependência personalizado é:</span><span class="sxs-lookup"><span data-stu-id="8feaa-219">The general approach for custom dependency tracking is to:</span></span>

- <span data-ttu-id="8feaa-220">Chamar o método `TelemetryClient.StartOperation` (extensão) que preencha as propriedades `DependencyTelemetry` necessárias para correlação e algumas outras propriedades (carimbo de data/hora de início, duração).</span><span class="sxs-lookup"><span data-stu-id="8feaa-220">Call the `TelemetryClient.StartOperation` (extension) method that fills the `DependencyTelemetry` properties that are needed for correlation and some other properties (start  time stamp, duration).</span></span>
- <span data-ttu-id="8feaa-221">Definir outras propriedades personalizadas no `DependencyTelemetry`: tais como nome e qualquer outro contexto necessário.</span><span class="sxs-lookup"><span data-stu-id="8feaa-221">Set other custom properties on the `DependencyTelemetry`, such as the name and any other context you need.</span></span>
- <span data-ttu-id="8feaa-222">Fazer uma chamada de dependência e esperar por ela.</span><span class="sxs-lookup"><span data-stu-id="8feaa-222">Make a dependency call and wait for it.</span></span>
- <span data-ttu-id="8feaa-223">Interromper a operação com `StopOperation` quando concluída.</span><span class="sxs-lookup"><span data-stu-id="8feaa-223">Stop the operation with `StopOperation` when it's finished.</span></span>
- <span data-ttu-id="8feaa-224">Tratar exceções.</span><span class="sxs-lookup"><span data-stu-id="8feaa-224">Handle exceptions.</span></span>

<span data-ttu-id="8feaa-225">`StopOperation` somente interrompe a operação que foi iniciada.</span><span class="sxs-lookup"><span data-stu-id="8feaa-225">`StopOperation` only stops the operation that was started.</span></span> <span data-ttu-id="8feaa-226">Se a operação de execução atual não corresponder à que você deseja interromper, `StopOperation` não fará nada.</span><span class="sxs-lookup"><span data-stu-id="8feaa-226">If the current running operation doesn't match the one you want to stop, `StopOperation` does nothing.</span></span> <span data-ttu-id="8feaa-227">Essa situação acontecer se você iniciar várias operações em paralelo no mesmo contexto de execução:</span><span class="sxs-lookup"><span data-stu-id="8feaa-227">This situation might happen if you start multiple operations in parallel in the same execution context:</span></span>

```C#
var firstOperation = telemetryClient.StartOperation<DependencyTelemetry>("task 1");
var firstOperation = telemetryClient.StartOperation<DependencyTelemetry>("task 1");
var firstTask = RunMyTaskAsync();

var secondOperation = telemetryClient.StartOperation<DependencyTelemetry>("task 2");
var secondTask = RunMyTaskAsync();

await firstTask;

// This will do nothing and will not report telemetry for the first operation
// as currently secondOperation is active.
telemetryClient.StopOperation(firstOperation); 

await secondTask;
```

<span data-ttu-id="8feaa-228">Certifique-se de sempre chamar `StartOperation` e executar a tarefa em seu próprio contexto:</span><span class="sxs-lookup"><span data-stu-id="8feaa-228">Make sure you always call `StartOperation` and run your task in its own context:</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="8feaa-229">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8feaa-229">Next steps</span></span>

- <span data-ttu-id="8feaa-230">Aprenda noções básicas de [correlação de telemetria](application-insights-correlation.md) no Application Insights.</span><span class="sxs-lookup"><span data-stu-id="8feaa-230">Learn the basics of [telemetry correlation](application-insights-correlation.md) in Application Insights.</span></span>
- <span data-ttu-id="8feaa-231">Consulte o [modelo de dados](application-insights-data-model.md) para modelo de dados e tipos do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="8feaa-231">See the [data model](application-insights-data-model.md) for Application Insights types and data model.</span></span>
- <span data-ttu-id="8feaa-232">Relate [eventos e métricas](app-insights-api-custom-events-metrics.md) personalizados para o Application Insights.</span><span class="sxs-lookup"><span data-stu-id="8feaa-232">Report custom [events and metrics](app-insights-api-custom-events-metrics.md) to Application Insights.</span></span>
- <span data-ttu-id="8feaa-233">Confira a [configuração](app-insights-configuration-with-applicationinsights-config.md#telemetry-initializers-aspnet) padrão para a coleção de propriedades de contexto.</span><span class="sxs-lookup"><span data-stu-id="8feaa-233">Check out standard [configuration](app-insights-configuration-with-applicationinsights-config.md#telemetry-initializers-aspnet) for context properties collection.</span></span>
- <span data-ttu-id="8feaa-234">Confira o [Guia do Usuário de System.Diagnostics.Activity](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/ActivityUserGuide.md) para ver como correlacionar telemetria.</span><span class="sxs-lookup"><span data-stu-id="8feaa-234">Check the [System.Diagnostics.Activity User Guide](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/ActivityUserGuide.md) to see how we correlate telemetry.</span></span>
