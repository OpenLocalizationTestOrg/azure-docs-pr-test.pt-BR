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
# <a name="track-custom-operations-with-application-insights-net-sdk"></a>Acompanhar operações personalizadas com o SDK do .NET do Application Insights

Azure SDKs do Application Insights automaticamente acompanhar solicitações de HTTP de entrada e chama toodependent serviços, como solicitações HTTP e consultas SQL. Rastreamento e a correlação de solicitações e dependências ofereçam visibilidade em capacidade de resposta e a confiabilidade do aplicativo inteiro hello em todos os microservices que combinam este aplicativo. 

Há uma classe de padrões de aplicativo que não pode ter suporte de maneira genérica. O monitoramento adequado de tais padrões requer a instrumentação de código manual. Este artigo aborda alguns padrões que podem exigir a instrumentação manual, tais como processamento de fila personalizada e execução de tarefas em segundo plano de longa execução.

Este documento fornece orientação sobre como operações personalizadas de tootrack com hello SDK do Application Insights. Esta documentação é relevante para:

- Application Insights para a .NET (também conhecido como o SDK de Base) versão 2.4+.
- Application Insights para aplicativos Web (executando ASP.NET) versão 2.4+.
- Application Insights para ASP.NET Core versão 2.1+.

## <a name="overview"></a>Visão geral
Uma operação é um trabalho lógico executado por um aplicativo. Ela tem nome, hora de início, duração e resultado, além de um contexto de execução como nome de usuário, propriedades e resultado. Se a operação A tiver sido iniciada pela operação B, então a operação B será definida como pai para A. Uma operação pode ter somente um pai, mas pode ter muitas operações filhas. Para obter mais informações sobre as operações e a correlação de telemetria, consulte [Correlação de telemetria do Azure Application Insights](application-insights-correlation.md).

Olá SDK .NET do Application Insights, operação Olá é descrita por classe abstrata Olá [OperationTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/Extensibility/Implementation/OperationTelemetry.cs) e seus descendentes [RequestTelemetry](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/DataContracts/RequestTelemetry.cs) e [DependencyTelemetry ](https://github.com/Microsoft/ApplicationInsights-dotnet/blob/develop/src/Core/Managed/Shared/DataContracts/DependencyTelemetry.cs).

## <a name="incoming-operations-tracking"></a>Acompanhamento de operações de entrada 
Olá web Application Insights que SDK coleta automaticamente as solicitações HTTP para aplicativos ASP.NET executados em um pipeline IIS e todos os aplicativos do ASP.NET Core. Há soluções com suporte da comunidade para outras plataformas e estruturas. No entanto, se o aplicativo hello não é suportado por qualquer uma das padrão hello ou soluções com suporte da comunidade, você pode instrumentá-lo manualmente.

Outro exemplo que requer um controle personalizado é trabalho Olá que recebe os itens da fila de saudação. Para alguns filas, Olá chamar tooadd uma mensagem na fila de toothis é controlada como uma dependência. No entanto, operação Olá de alto nível que descreve o processamento de mensagens não é automaticamente coletada.

Vamos ver como podemos acompanhar essas operações.

Em um nível alto, a tarefa de saudação é toocreate `RequestTelemetry` e definir propriedades conhecidas. Após a conclusão da operação de hello, você pode acompanhar telemetria hello. saudação de exemplo a seguir demonstra essa tarefa.

### <a name="http-request-in-owin-self-hosted-app"></a>Solicitação HTTP no aplicativo autohospedado Owin
Neste exemplo, seguimos Olá [protocolo HTTP para correlação](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/HttpCorrelationProtocol.md). Você deve esperar cabeçalhos tooreceive descritos existe.

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

Olá protocolo HTTP para correlação também declara Olá `Correlation-Context` cabeçalho. No entanto, é omitido aqui para manter a simplicidade.

## <a name="queue-instrumentation"></a>Instrumentação de fila
Para comunicação HTTP, criamos um protocolo toopass detalhes de correlação. Com protocolos de alguns dos filas, você pode transmitir metadados adicionais junto com a mensagem de saudação e com outras pessoas que não é possível.

### <a name="service-bus-queue"></a>Fila do Barramento de Serviço
Com hello Azure [fila do barramento de serviço](../service-bus-messaging/index.md), você pode passar um recipiente de propriedades, junto com a mensagem de saudação. Nós usamos uma ID de correlação toopass hello.

fila do barramento de serviço Olá usa protocolos baseados em TCP. O Application Insights não acompanha automaticamente as operações de fila, então nós as acompanhamos manualmente. Olá dequeue operação é uma API de estilo push e estamos não é possível tootrack-lo.

#### <a name="enqueue"></a>Enfileirar

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

#### <a name="process"></a>Processo
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

### <a name="azure-storage-queue"></a>Fila de Armazenamento do Azure
Olá mostrado no exemplo a seguir como Olá tootrack [fila de armazenamento do Azure](../storage/queues/storage-dotnet-how-to-use-queues.md) operações e correlacionar telemetria entre o produtor hello, consumidor hello e armazenamento do Azure. 

fila de armazenamento Olá tem uma API HTTP. Fila de toohello todas as chamadas são controladas pelo hello coletor de dependência do Application Insights para solicitações HTTP.
Certifique-se de que `Microsoft.ApplicationInsights.DependencyCollector.HttpDependenciesParsingTelemetryInitializer` esteja em `applicationInsights.config`. Se você não o fez, adicione-o programaticamente, conforme descrito em [filtragem e o pré-processamento de saudação do Azure SDK do Application Insights](app-insights-api-filtering-sampling.md).

Se você configurar o Application Insights manualmente, certifique-se de criar e inicializar `Microsoft.ApplicationInsights.DependencyCollector.DependencyTrackingTelemetryModule` de maneira similar a:
 
``` C#
DependencyTrackingTelemetryModule module = new DependencyTrackingTelemetryModule();

// You can prevent correlation header injection toosome domains by adding it toohello excluded list.
// Make sure you add a Storage endpoint. Otherwise, you might experience request signature validation issues on hello Storage service side.
module.ExcludeComponentCorrelationHttpHeadersOnDomains.Add("core.windows.net");
module.Initialize(TelemetryConfiguration.Active);

// Do not forget toodispose of hello module during application shutdown.
```

Você também poderá toocorrelate Olá ID da operação do Application Insights com ID de solicitação de armazenamento hello. Para obter informações sobre como tooset e obter um armazenamento de solicitação de cliente e uma ID de solicitação do servidor, consulte [monitorar, diagnosticar e solucionar problemas de armazenamento do Azure](../storage/common/storage-monitoring-diagnosing-troubleshooting.md#end-to-end-tracing).

#### <a name="enqueue"></a>Enfileirar
Como as filas de armazenamento oferecem suporte a saudação API HTTP, todas as operações com fila Olá automaticamente são rastreadas pelo Application Insights. Em muitos casos, essa instrumentação deve ser suficiente. No entanto, toocorrelate rastreamentos no lado do consumidor Olá com rastreamentos de produtor, você deve passar algum contexto de correlação da mesma forma toohow fazemos isso no hello protocolo HTTP para correlação. 

Neste exemplo, podemos controlar Olá opcional `Enqueue` operação. Você pode:

 - **Correlacionar tentativas (se houver)**: tiverem um pai comum que é hello `Enqueue` operação. Caso contrário, eles são rastreados como filhos da solicitação de entrada hello. Se houver várias filas de toohello solicitações lógico, talvez seja difícil toofind chamada resultou em novas tentativas.
 - **Correlacione os logs do Armazenamento (se e quando necessário)**: são correlacionados à telemetria do Application Insights.

Olá `Enqueue` operação é filho de saudação de uma operação do pai (por exemplo, uma solicitação de HTTP entrada). chamada de dependência Olá HTTP é filho Olá Olá `Enqueue` neto hello e de operação de solicitação de entrada hello:

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

relatórios de seu aplicativo com a quantidade de saudação tooreduce de telemetria ou se você não quiser Olá tootrack `Enqueue` operação por outros motivos, use Olá `Activity` API diretamente:

- Criar (e iniciar) um novo `Activity` em vez de começar a operação do Application Insights hello. Fazer *não* necessário tooassign as propriedades nele, exceto o nome da operação hello.
- Serializar `yourActivity.Id` na carga de mensagem de saudação em vez de `operation.Telemetry.Id`. Você também pode usar `Activity.Current.Id`.


#### <a name="dequeue"></a>Remover da fila
Da mesma forma muito`Enqueue`, automaticamente, uma fila de armazenamento real toohello de solicitação HTTP é controlada pelo Application Insights. No entanto, Olá `Enqueue` operação supostamente ocorre no contexto de pai hello, como um contexto de solicitação de entrada. SDKs do Application Insights correlacionar automaticamente essa operação (e sua parte HTTP) com a solicitação de pai hello e outros telemetria relatado no hello mesmo escopo.

Olá `Dequeue` operação é complicada. Olá SDK do Application Insights controla automaticamente as solicitações HTTP. No entanto, ele não sabe o contexto de correlação de saudação até que a mensagem de saudação é analisada. Não é uma mensagem de saudação toocorrelate possíveis Olá HTTP solicitação tooget com rest Olá de telemetria hello.

Em muitos casos, talvez seja útil toocorrelate fila de toohello da solicitação de Olá HTTP com outros rastreamentos também. Olá exemplo a seguir demonstra como toodo-lo:

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

#### <a name="process"></a>Processo

Em Olá exemplo a seguir, é uma mensagem de entrada de rastreamento de uma maneira da mesma forma toohow é um HTTP de entrada de rastreamento de solicitação:

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

Da mesma forma, outras operações de fila podem ser instrumentadas. Uma operação de espiar deve ser instrumentada da mesma maneira que uma operação de remoção da fila. A instrumentação de operações de gerenciamento de fila não é necessária. O Application Insights acompanha operações como HTTP e, na maioria dos casos, isso é suficiente.

Quando você instrumentar a exclusão de mensagem, verifique se que definiu operação Olá identificadores (correlação). Como alternativa, você pode usar o hello `Activity` API. Em seguida, você não precisa tooset identificadores de operação em itens de telemetria Olá porque Application Insights faz isso para você:

- Criar um novo `Activity` depois que você tem um item da fila de saudação.
- Use `Activity.SetParentId(message.ParentId)` toocorrelate logs de produtor e consumidor.
- Iniciar Olá `Activity`.
- Acompanhe as operações de remoção da fila, processamento e exclusão usando auxiliares `Start/StopOperation`. Fazer isso da saudação mesmo assíncrona (contexto de execução) do fluxo de controle. Dessa forma, elas são correlacionadas corretamente.
- Saudação de parada `Activity`.
- Use `Start/StopOperation` ou chame a telemetria `Track` manualmente.

### <a name="batch-processing"></a>Processamento em lotes
Com algumas filas, você pode remover da fila várias mensagens com uma solicitação. Processar essas mensagens supostamente independente e pertence toohello diferentes operações lógicas. Nesse caso, não é possível toocorrelate Olá `Dequeue` processamento de mensagem de operação tooparticular.

Cada mensagem deve ser processada no seu próprio fluxo de controle assíncrono. Para obter mais informações, consulte Olá [dependências de saída de rastreamento](#outgoing-dependencies-tracking) seção.

## <a name="long-running-background-tasks"></a>Tarefas em segundo plano de execução longa
Alguns aplicativos iniciam operações de longa execução que podem ser causadas por solicitações de usuário. Da perspectiva do rastreamento/instrumentação hello, não é diferente da instrumentação de solicitação ou de dependência: 

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

Neste exemplo, usamos `telemetryClient.StartOperation` toocreate `RequestTelemetry` e o contexto de correlação de saudação do preenchimento. Digamos que você tenha uma operação de pai que foi criada por solicitações de entrada que Olá operação agendada. Enquanto `BackgroundTask` inicia no Olá mesmo fluxo de controle assíncrono como uma solicitação de entrada, ele está correlacionado a operação pai. `BackgroundTask`e todos os itens de telemetria aninhados são automaticamente correlacionados a solicitação de saudação que fez com que ele, mesmo depois do término solicitação hello.

Quando a tarefa de saudação inicia de thread em segundo plano Olá que não tem qualquer operação (`Activity`) associado a ele, `BackgroundTask` não tem nenhum pai. No entanto, ela pode ter operações aninhadas. Todos os itens de telemetria informados da tarefa de saudação são correlacionado toohello `RequestTelemetry` criado no `BackgroundTask`.

## <a name="outgoing-dependencies-tracking"></a>Acompanhamento de dependências de saída
Você pode controlar sua própria variante de dependência ou uma operação sem suporte pelo Application Insights.

Olá `Enqueue` método na fila do barramento de serviço hello ou fila de armazenamento Olá pode servir como exemplos de tal personalizado de controle.

a abordagem geral Olá para controle de dependência personalizada é:

- Chamar hello `TelemetryClient.StartOperation` método (extensão) que preenche Olá `DependencyTelemetry` propriedades necessárias para correlação e algumas outras propriedades (hora de início do carimbo, duração).
- Definir outras propriedades personalizadas em Olá `DependencyTelemetry`, como nome de saudação e qualquer outro contexto é necessário.
- Fazer uma chamada de dependência e esperar por ela.
- Parar a operação de saudação com `StopOperation` quando ele for concluído.
- Tratar exceções.

`StopOperation`somente para operação de saudação que foi iniciada. Se operação em execução atual de saudação não corresponder a saudação um toostop, você deseja `StopOperation` não fará nada. Essa situação pode ocorrer se você iniciar várias operações em paralelo no hello mesmo contexto de execução:

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

Certifique-se de sempre chamar `StartOperation` e executar a tarefa em seu próprio contexto:
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

## <a name="next-steps"></a>Próximas etapas

- Conheça os fundamentos de saudação do [correlação de telemetria](application-insights-correlation.md) no Application Insights.
- Consulte Olá [modelo de dados](application-insights-data-model.md) para modelo de dados e tipos de informações do aplicativo.
- Relatório personalizado [eventos e métricas](app-insights-api-custom-events-metrics.md) tooApplication Insights.
- Confira a [configuração](app-insights-configuration-with-applicationinsights-config.md#telemetry-initializers-aspnet) padrão para a coleção de propriedades de contexto.
- Verificar Olá [guia do usuário System.Diagnostics.Activity](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/ActivityUserGuide.md) toosee como correlacionamos telemetria.
