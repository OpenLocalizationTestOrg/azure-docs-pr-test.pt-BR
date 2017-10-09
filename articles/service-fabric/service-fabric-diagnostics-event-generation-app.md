---
title: "Monitoramento de nível de aplicativos do serviço de malha de aaaAzure | Microsoft Docs"
description: "Saiba mais sobre aplicativos e logs e eventos de nível de serviço usado toomonitor e diagnosticar os clusters de malha do serviço do Azure."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 05/26/2017
ms.author: dekapur
ms.openlocfilehash: 4f4da1eaad4b88428eaa3a2100ac25c8a285a727
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="application-and-service-level-event-and-log-generation"></a><span data-ttu-id="a0a15-103">Geração de logs e eventos de nível de aplicativo e serviço</span><span class="sxs-lookup"><span data-stu-id="a0a15-103">Application and service level event and log generation</span></span>

## <a name="instrumenting-hello-code-with-custom-events"></a><span data-ttu-id="a0a15-104">Código de instrumentação Olá com eventos personalizados</span><span class="sxs-lookup"><span data-stu-id="a0a15-104">Instrumenting hello code with custom events</span></span>

<span data-ttu-id="a0a15-105">Instrumentação de código Olá é a base de Olá para a maioria dos outros aspectos de seus serviços de monitoramento.</span><span class="sxs-lookup"><span data-stu-id="a0a15-105">Instrumenting hello code is hello basis for most other aspects of monitoring your services.</span></span> <span data-ttu-id="a0a15-106">Instrumentação é única forma de saudação que você possa saber que algo está errado e toodiagnose que precisa toobe fixa.</span><span class="sxs-lookup"><span data-stu-id="a0a15-106">Instrumentation is hello only way you can know that something is wrong, and toodiagnose what needs toobe fixed.</span></span> <span data-ttu-id="a0a15-107">Embora seja tecnicamente possível tooconnect um serviço de produção do depurador tooa, não é uma prática comum.</span><span class="sxs-lookup"><span data-stu-id="a0a15-107">Although technically it's possible tooconnect a debugger tooa production service, it's not a common practice.</span></span> <span data-ttu-id="a0a15-108">Portanto, é importante ter dados de instrumentação detalhados.</span><span class="sxs-lookup"><span data-stu-id="a0a15-108">So, having detailed instrumentation data is important.</span></span>

<span data-ttu-id="a0a15-109">Alguns produtos instrumentam automaticamente seu código.</span><span class="sxs-lookup"><span data-stu-id="a0a15-109">Some products automatically instrument your code.</span></span> <span data-ttu-id="a0a15-110">Embora essas soluções podem funcionar bem, quase sempre a instrumentação manual é necessária.</span><span class="sxs-lookup"><span data-stu-id="a0a15-110">Although these solutions can work well, manual instrumentation is almost always required.</span></span> <span data-ttu-id="a0a15-111">No final do hello, você deve ter suficiente tooforensically informações depurar o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="a0a15-111">In hello end, you must have enough information tooforensically debug hello application.</span></span> <span data-ttu-id="a0a15-112">Este documento descreve abordagens diferentes tooinstrumenting seu código, e quando toochoose uma abordagem em detrimento de outro.</span><span class="sxs-lookup"><span data-stu-id="a0a15-112">This document describes different approaches tooinstrumenting your code, and when toochoose one approach over another.</span></span>

## <a name="eventsource"></a><span data-ttu-id="a0a15-113">EventSource</span><span class="sxs-lookup"><span data-stu-id="a0a15-113">EventSource</span></span>
<span data-ttu-id="a0a15-114">Quando você cria uma solução do Service Fabric de um modelo do Visual Studio, uma classe derivada de **EventSource** (**ServiceEventSource** ou **ActorEventSource**) é gerada.</span><span class="sxs-lookup"><span data-stu-id="a0a15-114">When you create a Service Fabric solution from a template in Visual Studio, an **EventSource**-derived class (**ServiceEventSource** or **ActorEventSource**) is generated.</span></span> <span data-ttu-id="a0a15-115">Um modelo é criado, no qual você pode adicionar eventos para seu aplicativo ou serviço.</span><span class="sxs-lookup"><span data-stu-id="a0a15-115">A template is created, in which you can add events for your application or service.</span></span> <span data-ttu-id="a0a15-116">Olá **EventSource** nome **deve** ser exclusivo e deve ser renomeado de cadeia de caracteres de saudação padrão modelo MyCompany -&lt;solução&gt; - &lt; projeto&gt;.</span><span class="sxs-lookup"><span data-stu-id="a0a15-116">hello **EventSource** name **must** be unique, and should be renamed from hello default template string MyCompany-&lt;solution&gt;-&lt;project&gt;.</span></span> <span data-ttu-id="a0a15-117">Ter várias **EventSource** definições que usam Olá mesmo nome faz com que um problema no tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="a0a15-117">Having multiple **EventSource** definitions that use hello same name causes an issue at run time.</span></span> <span data-ttu-id="a0a15-118">Cada evento definido deve ter um identificador exclusivo.</span><span class="sxs-lookup"><span data-stu-id="a0a15-118">Each defined event must have a unique identifier.</span></span> <span data-ttu-id="a0a15-119">Se um identificador não for exclusivo, ocorrerá uma falha de tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="a0a15-119">If an identifier is not unique, a runtime failure occurs.</span></span> <span data-ttu-id="a0a15-120">Algumas organizações preassign intervalos de valores para conflitos de tooavoid de identificadores entre as equipes de desenvolvimento separado.</span><span class="sxs-lookup"><span data-stu-id="a0a15-120">Some organizations preassign ranges of values for identifiers tooavoid conflicts between separate development teams.</span></span> <span data-ttu-id="a0a15-121">Para obter mais informações, consulte [blog de Vance](https://blogs.msdn.microsoft.com/vancem/2012/07/09/introduction-tutorial-logging-etw-events-in-c-system-diagnostics-tracing-eventsource/) ou hello [documentação MSDN](https://msdn.microsoft.com/library/dn774985(v=pandp.20).aspx).</span><span class="sxs-lookup"><span data-stu-id="a0a15-121">For more information, see [Vance's blog](https://blogs.msdn.microsoft.com/vancem/2012/07/09/introduction-tutorial-logging-etw-events-in-c-system-diagnostics-tracing-eventsource/) or hello [MSDN documentation](https://msdn.microsoft.com/library/dn774985(v=pandp.20).aspx).</span></span>

### <a name="using-structured-eventsource-events"></a><span data-ttu-id="a0a15-122">Usando eventos estruturados de EventSource</span><span class="sxs-lookup"><span data-stu-id="a0a15-122">Using structured EventSource events</span></span>

<span data-ttu-id="a0a15-123">Cada um dos eventos de saudação nos exemplos de código Olá nesta seção são definidas para um caso específico, por exemplo, quando um tipo de serviço é registrado.</span><span class="sxs-lookup"><span data-stu-id="a0a15-123">Each of hello events in hello code examples in this section are defined for a specific case, for example, when a service type is registered.</span></span> <span data-ttu-id="a0a15-124">Quando você definir mensagens pelo caso de uso, dados podem ser empacotados com o texto de saudação do erro hello e você pode mais facilmente de pesquisa e filtro com base em nomes de saudação ou valores de saudação as propriedades especificadas.</span><span class="sxs-lookup"><span data-stu-id="a0a15-124">When you define messages by use case, data can be packaged with hello text of hello error, and you can more easily search and filter based on hello names or values of hello specified properties.</span></span> <span data-ttu-id="a0a15-125">Estruturar a saída de instrumentação Olá torna mais fácil tooconsume, mas exige mais trabalho e hora toodefine um novo evento para cada caso de uso.</span><span class="sxs-lookup"><span data-stu-id="a0a15-125">Structuring hello instrumentation output makes it easier tooconsume, but requires more thought and time toodefine a new event for each use case.</span></span> <span data-ttu-id="a0a15-126">Algumas definições de evento podem ser compartilhadas em todo o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="a0a15-126">Some event definitions can be shared across hello entire application.</span></span> <span data-ttu-id="a0a15-127">Por exemplo, um evento de início ou de parada de método seria reutilizado em vários serviços em um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a0a15-127">For example, a method start or stop event would be reused across many services within an application.</span></span> <span data-ttu-id="a0a15-128">Um serviço de domínio específico, como um sistema de pedidos, pode ter um evento **CreateOrder**, que terá seu próprio evento exclusivo.</span><span class="sxs-lookup"><span data-stu-id="a0a15-128">A domain-specific service, like an order system, might have a **CreateOrder** event, which has its own unique event.</span></span> <span data-ttu-id="a0a15-129">Essa abordagem pode gerar muitos eventos e potencialmente requer a coordenação de identificadores entre as equipes de projeto.</span><span class="sxs-lookup"><span data-stu-id="a0a15-129">This approach might generate many events, and potentially require coordination of identifiers across project teams.</span></span> 

```csharp
    [EventSource(Name = "MyCompany-VotingState-VotingStateService")]
    internal sealed class ServiceEventSource : EventSource
    {
        public static readonly ServiceEventSource Current = new ServiceEventSource();

        // hello instance constructor is private tooenforce singleton semantics.
        private ServiceEventSource() : base() { }

        ...

        // hello ServiceTypeRegistered event contains a unique identifier, an event attribute that defined hello event, and hello code implementation of hello event.
        private const int ServiceTypeRegisteredEventId = 3;
        [Event(ServiceTypeRegisteredEventId, Level = EventLevel.Informational, Message = "Service host process {0} registered service type {1}", Keywords = Keywords.ServiceInitialization)]
        public void ServiceTypeRegistered(int hostProcessId, string serviceType)
        {
            WriteEvent(ServiceTypeRegisteredEventId, hostProcessId, serviceType);
        }

        // hello ServiceHostInitializationFailed event contains a unique identifier, an event attribute that defined hello event, and hello code implementation of hello event.
        private const int ServiceHostInitializationFailedEventId = 4;
        [Event(ServiceHostInitializationFailedEventId, Level = EventLevel.Error, Message = "Service host initialization failed", Keywords = Keywords.ServiceInitialization)]
        public void ServiceHostInitializationFailed(string exception)
        {
            WriteEvent(ServiceHostInitializationFailedEventId, exception);
        }
```

### <a name="using-eventsource-generically"></a><span data-ttu-id="a0a15-130">Usando o EventSource de forma genérica</span><span class="sxs-lookup"><span data-stu-id="a0a15-130">Using EventSource generically</span></span>

<span data-ttu-id="a0a15-131">Como definir eventos específicos pode ser difícil, muitas pessoas definem alguns eventos com um conjunto comum de parâmetros que geralmente emitem suas informações como uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="a0a15-131">Because defining specific events can be difficult, many people define a few events with a common set of parameters that generally output their information as a string.</span></span> <span data-ttu-id="a0a15-132">Muito aspecto Olá estruturado é perdido e é mais difícil toosearch e filtro Olá resultados.</span><span class="sxs-lookup"><span data-stu-id="a0a15-132">Much of hello structured aspect is lost, and it's more difficult toosearch and filter hello results.</span></span> <span data-ttu-id="a0a15-133">Nessa abordagem, alguns eventos que geralmente correspondem a níveis de log toohello são definidos.</span><span class="sxs-lookup"><span data-stu-id="a0a15-133">In this approach, a few events that usually correspond toohello logging levels are defined.</span></span> <span data-ttu-id="a0a15-134">saudação de trecho de código a seguir define uma mensagem de erro e de depuração:</span><span class="sxs-lookup"><span data-stu-id="a0a15-134">hello following snippet defines a debug and error message:</span></span>

```csharp
    [EventSource(Name = "MyCompany-VotingState-VotingStateService")]
    internal sealed class ServiceEventSource : EventSource
    {
        public static readonly ServiceEventSource Current = new ServiceEventSource();

        // hello Instance constructor is private, tooenforce singleton semantics.
        private ServiceEventSource() : base() { }

        ...

        private const int DebugEventId = 10;
        [Event(DebugEventId, Level = EventLevel.Verbose, Message = "{0}")]
        public void Debug(string msg)
        {
            WriteEvent(DebugEventId, msg);
        }

        private const int ErrorEventId = 11;
        [Event(ErrorEventId, Level = EventLevel.Error, Message = "Error: {0} - {1}")]
        public void Error(string error, string msg)
        {
            WriteEvent(ErrorEventId, error, msg);
        }
```

<span data-ttu-id="a0a15-135">Usar uma mistura de instrumentação genérica e não estruturados também pode funcionar bem.</span><span class="sxs-lookup"><span data-stu-id="a0a15-135">Using a hybrid of structured and generic instrumentation also can work well.</span></span> <span data-ttu-id="a0a15-136">A instrumentação estruturada é usada para relatar erros e métricas.</span><span class="sxs-lookup"><span data-stu-id="a0a15-136">Structured instrumentation is used for reporting errors and metrics.</span></span> <span data-ttu-id="a0a15-137">Eventos genéricos podem ser usados para Olá detalhada log que é consumida pelos engenheiros para solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="a0a15-137">Generic events can be used for hello detailed logging that is consumed by engineers for troubleshooting.</span></span>

## <a name="aspnet-core-logging"></a><span data-ttu-id="a0a15-138">Registro em log de ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="a0a15-138">ASP.NET Core logging</span></span>

<span data-ttu-id="a0a15-139">É importante toocarefully planeje como você instruirá o seu código.</span><span class="sxs-lookup"><span data-stu-id="a0a15-139">It's important toocarefully plan how you will instrument your code.</span></span> <span data-ttu-id="a0a15-140">plano de instrumentação direita Olá pode ajudar a evitar potencialmente desestabilizar sua base de código e, em seguida, a necessidade de código de saudação tooreinstrument.</span><span class="sxs-lookup"><span data-stu-id="a0a15-140">hello right instrumentation plan can help you avoid potentially destabilizing your code base, and then needing tooreinstrument hello code.</span></span> <span data-ttu-id="a0a15-141">tooreduce risco, você pode escolher uma biblioteca de instrumentação como [Microsoft.Extensions.Logging](https://www.nuget.org/packages/Microsoft.Extensions.Logging/), que faz parte do Microsoft ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="a0a15-141">tooreduce risk, you can choose an instrumentation library like [Microsoft.Extensions.Logging](https://www.nuget.org/packages/Microsoft.Extensions.Logging/), which is part of Microsoft ASP.NET Core.</span></span> <span data-ttu-id="a0a15-142">ASP.NET Core tem um [ILogger](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.ilogger) interface que você pode usar com o provedor de saudação de sua escolha, minimizando o efeito de saudação em código existente.</span><span class="sxs-lookup"><span data-stu-id="a0a15-142">ASP.NET Core has an [ILogger](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.ilogger) interface that you can use with hello provider of your choice, while minimizing hello effect on existing code.</span></span> <span data-ttu-id="a0a15-143">Você pode usar código de saudação em ASP.NET Core no Windows e Linux e no hello completa do .NET Framework, para que seu código de instrumentação é padronizado.</span><span class="sxs-lookup"><span data-stu-id="a0a15-143">You can use hello code in ASP.NET Core on Windows and Linux, and in hello full .NET Framework, so your instrumentation code is standardized.</span></span> <span data-ttu-id="a0a15-144">Isso é explorado em mais detalhes abaixo:</span><span class="sxs-lookup"><span data-stu-id="a0a15-144">This is further explored below:</span></span>

### <a name="using-microsoftextensionslogging-in-service-fabric"></a><span data-ttu-id="a0a15-145">Uso de Microsoft.Extensions.Logging no Service Fabric</span><span class="sxs-lookup"><span data-stu-id="a0a15-145">Using Microsoft.Extensions.Logging in Service Fabric</span></span>

1. <span data-ttu-id="a0a15-146">Adicione Olá Microsoft.Extensions.Logging NuGet pacote toohello projeto você deseja tooinstrument.</span><span class="sxs-lookup"><span data-stu-id="a0a15-146">Add hello Microsoft.Extensions.Logging NuGet package toohello project you want tooinstrument.</span></span> <span data-ttu-id="a0a15-147">Além disso, adicionar todos os pacotes de provedor (para um pacote de terceiros, consulte Olá exemplo a seguir).</span><span class="sxs-lookup"><span data-stu-id="a0a15-147">Also, add any provider packages (for a third-party package, see hello following example).</span></span> <span data-ttu-id="a0a15-148">Para saber mais, veja [Entrar no ASP.NET Core](https://docs.microsoft.com/aspnet/core/fundamentals/logging).</span><span class="sxs-lookup"><span data-stu-id="a0a15-148">For more information, see [Logging in ASP.NET Core](https://docs.microsoft.com/aspnet/core/fundamentals/logging).</span></span>
2. <span data-ttu-id="a0a15-149">Adicionar um **usando** diretiva para o arquivo de serviço tooyour Microsoft.Extensions.Logging.</span><span class="sxs-lookup"><span data-stu-id="a0a15-149">Add a **using** directive for Microsoft.Extensions.Logging tooyour service file.</span></span>
3. <span data-ttu-id="a0a15-150">Definir uma variável privada em sua classe de serviço.</span><span class="sxs-lookup"><span data-stu-id="a0a15-150">Define a private variable within your service class.</span></span>

  ```csharp
  private ILogger _logger = null;

  ```
4. <span data-ttu-id="a0a15-151">No construtor de saudação da sua classe de serviço, adicione este código:</span><span class="sxs-lookup"><span data-stu-id="a0a15-151">In hello constructor of your service class, add this code:</span></span>

  ```csharp
  _logger = new LoggerFactory().CreateLogger<Stateless>();

  ```
5. <span data-ttu-id="a0a15-152">Iniciar a instrumentação do código em seus métodos.</span><span class="sxs-lookup"><span data-stu-id="a0a15-152">Start instrumenting your code in your methods.</span></span> <span data-ttu-id="a0a15-153">Veja alguns exemplos:</span><span class="sxs-lookup"><span data-stu-id="a0a15-153">Here are a few samples:</span></span>

  ```csharp
  _logger.LogDebug("Debug-level event from Microsoft.Logging");
  _logger.LogInformation("Informational-level event from Microsoft.Logging");

  // In this variant, we're adding structured properties RequestName and Duration, which have values MyRequest and hello duration of hello request.
  // Later in hello article, we discuss why this step is useful.
  _logger.LogInformation("{RequestName} {Duration}", "MyRequest", requestDuration);

  ```

## <a name="using-other-logging-providers"></a><span data-ttu-id="a0a15-154">Usando outros provedores de registro log</span><span class="sxs-lookup"><span data-stu-id="a0a15-154">Using other logging providers</span></span>

<span data-ttu-id="a0a15-155">Alguns provedores de terceiros abordagem Olá descrito em Olá anterior seção, incluindo [Serilog](https://serilog.net/), [NLog](http://nlog-project.org/), e [Loggr](https://github.com/imobile3/Loggr.Extensions.Logging).</span><span class="sxs-lookup"><span data-stu-id="a0a15-155">Some third-party providers use hello approach described in hello preceding section, including [Serilog](https://serilog.net/), [NLog](http://nlog-project.org/), and [Loggr](https://github.com/imobile3/Loggr.Extensions.Logging).</span></span> <span data-ttu-id="a0a15-156">Você pode conectar cada uma delas no log do ASP.NET Core, ou pode usá-las separadamente.</span><span class="sxs-lookup"><span data-stu-id="a0a15-156">You can plug each of these into ASP.NET Core logging, or you can use them separately.</span></span> <span data-ttu-id="a0a15-157">O Serilog tem um recurso que aprimora todas as mensagens enviadas de um agente de log.</span><span class="sxs-lookup"><span data-stu-id="a0a15-157">Serilog has a feature that enriches all messages sent from a logger.</span></span> <span data-ttu-id="a0a15-158">Esse recurso pode ser útil toooutput Olá nome, tipo e informações de partição.</span><span class="sxs-lookup"><span data-stu-id="a0a15-158">This feature can be useful toooutput hello service name, type, and partition information.</span></span> <span data-ttu-id="a0a15-159">toouse esse recurso no hello infraestrutura do ASP.NET Core, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="a0a15-159">toouse this capability in hello ASP.NET Core infrastructure, do these steps:</span></span>

1. <span data-ttu-id="a0a15-160">Adicione Olá Serilog, Serilog.Extensions.Logging, e pacotes do Serilog.Sinks.Observable NuGet toohello projeto.</span><span class="sxs-lookup"><span data-stu-id="a0a15-160">Add hello Serilog, Serilog.Extensions.Logging, and Serilog.Sinks.Observable NuGet packages toohello project.</span></span> <span data-ttu-id="a0a15-161">Para o exemplo a seguir hello, também adicione Serilog.Sinks.Literate.</span><span class="sxs-lookup"><span data-stu-id="a0a15-161">For hello next example, also add Serilog.Sinks.Literate.</span></span> <span data-ttu-id="a0a15-162">Uma abordagem melhor será mostrada posteriormente neste artigo.</span><span class="sxs-lookup"><span data-stu-id="a0a15-162">A better approach is shown later in this article.</span></span>
2. <span data-ttu-id="a0a15-163">Serilog, cria uma instância de agente LoggerConfiguration e hello.</span><span class="sxs-lookup"><span data-stu-id="a0a15-163">In Serilog, create a LoggerConfiguration and hello logger instance.</span></span>

  ```csharp
  Log.Logger = new LoggerConfiguration().WriteTo.LiterateConsole().CreateLogger();
  ```

3. <span data-ttu-id="a0a15-164">Adicione um construtor de serviço Serilog.ILogger argumento toohello e passar Olá recém-criado agente de log.</span><span class="sxs-lookup"><span data-stu-id="a0a15-164">Add a Serilog.ILogger argument toohello service constructor, and pass hello newly created logger.</span></span>

  ```csharp
  ServiceRuntime.RegisterServiceAsync("StatelessType", context => new Stateless(context, Log.Logger)).GetAwaiter().GetResult();
  ```

4. <span data-ttu-id="a0a15-165">No construtor de serviço hello, adicionar Olá seguindo o código, que cria Olá enrichers de propriedade para Olá **ServiceTypeName**, **ServiceName**, **PartitionId**e  **InstanceId** propriedades do serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="a0a15-165">In hello service constructor, add hello following code, which creates hello property enrichers for hello **ServiceTypeName**, **ServiceName**, **PartitionId**, and **InstanceId** properties of hello service.</span></span> <span data-ttu-id="a0a15-166">Ele também adiciona uma toohello enricher de propriedade fábrica de registro do ASP.NET Core, então você pode usar Microsoft.Extensions.Logging.ILogger no seu código.</span><span class="sxs-lookup"><span data-stu-id="a0a15-166">It also adds a property enricher toohello ASP.NET Core logging factory, so you can use Microsoft.Extensions.Logging.ILogger in your code.</span></span>

  ```csharp
  public Stateless(StatelessServiceContext context, Serilog.ILogger serilog)
      : base(context)
  {
      PropertyEnricher[] properties = new PropertyEnricher[]
      {
          new PropertyEnricher("ServiceTypeName", context.ServiceTypeName),
          new PropertyEnricher("ServiceName", context.ServiceName),
          new PropertyEnricher("PartitionId", context.PartitionId),
          new PropertyEnricher("InstanceId", context.ReplicaOrInstanceId),
      };

      serilog.ForContext(properties);

      _logger = new LoggerFactory().AddSerilog(serilog.ForContext(properties)).CreateLogger<Stateless>();
  }
  ```

5. <span data-ttu-id="a0a15-167">Código do instrumento Olá Olá mesmo como se estivesse usando o ASP.NET Core sem Serilog.</span><span class="sxs-lookup"><span data-stu-id="a0a15-167">Instrument hello code hello same as if you were using ASP.NET Core without Serilog.</span></span>

  >[!NOTE]
  ><span data-ttu-id="a0a15-168">É recomendável que você não use Olá estático Log.Logger com hello anterior de exemplo.</span><span class="sxs-lookup"><span data-stu-id="a0a15-168">We recommend that you don't use hello static Log.Logger with hello preceding example.</span></span> <span data-ttu-id="a0a15-169">Serviço de malha pode hospedar várias instâncias de saudação do mesmo serviço tipo em um único processo.</span><span class="sxs-lookup"><span data-stu-id="a0a15-169">Service Fabric can host multiple instances of hello same service type within a single process.</span></span> <span data-ttu-id="a0a15-170">Se você usar Olá Log.Logger estático, último gravador saudação do enrichers de propriedade Olá mostrará valores para todas as instâncias que estão em execução.</span><span class="sxs-lookup"><span data-stu-id="a0a15-170">If you use hello static Log.Logger, hello last writer of hello property enrichers will show values for all instances that are running.</span></span> <span data-ttu-id="a0a15-171">Este é um motivo por que a variável logger de saudação é uma variável de membro particular da classe de serviço hello.</span><span class="sxs-lookup"><span data-stu-id="a0a15-171">This is one reason why hello _logger variable is a private member variable of hello service class.</span></span> <span data-ttu-id="a0a15-172">Além disso, você deve tornar o código de toocommon disponíveis do hello Logger, que pode ser usado em serviços.</span><span class="sxs-lookup"><span data-stu-id="a0a15-172">Also, you must make hello _logger available toocommon code, which might be used across services.</span></span>

## <a name="choosing-a-logging-provider"></a><span data-ttu-id="a0a15-173">Escolher um provedor de log</span><span class="sxs-lookup"><span data-stu-id="a0a15-173">Choosing a logging provider</span></span>

<span data-ttu-id="a0a15-174">Se o aplicativo depende de alto desempenho, o **EventSource** geralmente é uma boa abordagem.</span><span class="sxs-lookup"><span data-stu-id="a0a15-174">If your application relies on high performance, **EventSource** is usually a good approach.</span></span> <span data-ttu-id="a0a15-175">**EventSource** *geralmente* usa menos recursos e é melhor do que o ASP.NET Core log ou qualquer uma das soluções de terceiros disponíveis hello.</span><span class="sxs-lookup"><span data-stu-id="a0a15-175">**EventSource** *generally* uses fewer resources and performs better than ASP.NET Core logging or any of hello available third-party solutions.</span></span>  <span data-ttu-id="a0a15-176">Isso não é um problema para muitos serviços, mas se o seu serviço for orientado ao desempenho, usar o **EventSource** poderá ser uma opção melhor.</span><span class="sxs-lookup"><span data-stu-id="a0a15-176">This isn't an issue for many services, but if your service is performance-oriented, using **EventSource** might be a better choice.</span></span> <span data-ttu-id="a0a15-177">No entanto, tooget esses benefícios de estruturado de registro em log, **EventSource** requer um investimento maior da sua equipe de engenharia.</span><span class="sxs-lookup"><span data-stu-id="a0a15-177">However, tooget these benefits of structured logging, **EventSource** requires a larger investment from your engineering team.</span></span> <span data-ttu-id="a0a15-178">Se possível, siga um protótipo rápido algumas das opções de log e escolha Olá que melhor atenda às suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="a0a15-178">If possible, do a quick prototype of a few logging options, and then choose hello one that best meets your needs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a0a15-179">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a0a15-179">Next steps</span></span>

<span data-ttu-id="a0a15-180">Depois de ter escolhido o tooinstrument do provedor de log de seus aplicativos e serviços, seus logs e eventos necessário toobe agregado para que eles possam ser enviados tooany plataforma de análise.</span><span class="sxs-lookup"><span data-stu-id="a0a15-180">Once you have chosen your logging provider tooinstrument your applications and services, your logs and events need toobe aggregated before they can be sent tooany analysis platform.</span></span> <span data-ttu-id="a0a15-181">Leia sobre [EventFlow](service-fabric-diagnostics-event-aggregation-eventflow.md) e [WAD](service-fabric-diagnostics-event-aggregation-wad.md) toobetter entender alguns dos Olá opções recomendada.</span><span class="sxs-lookup"><span data-stu-id="a0a15-181">Read about [EventFlow](service-fabric-diagnostics-event-aggregation-eventflow.md) and [WAD](service-fabric-diagnostics-event-aggregation-wad.md) toobetter understand some of hello recommended options.</span></span>
