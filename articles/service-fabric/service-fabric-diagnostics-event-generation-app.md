---
title: "Monitoramento de nível de aplicativo do Service Fabric do Azure | Microsoft Docs"
description: "Saiba mais sobre eventos e logs de nível de aplicativo e serviço usados para monitorar e diagnosticar clusters do Service Fabric do Azure."
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
ms.openlocfilehash: 3c472904641108b7383cd0f1416c47460f8de11a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="application-and-service-level-event-and-log-generation"></a><span data-ttu-id="65658-103">Geração de logs e eventos de nível de aplicativo e serviço</span><span class="sxs-lookup"><span data-stu-id="65658-103">Application and service level event and log generation</span></span>

## <a name="instrumenting-the-code-with-custom-events"></a><span data-ttu-id="65658-104">Instrumentação do código com eventos personalizados</span><span class="sxs-lookup"><span data-stu-id="65658-104">Instrumenting the code with custom events</span></span>

<span data-ttu-id="65658-105">Instrumentar o código é a base para a maioria dos outros aspectos do monitoramento de seus serviços.</span><span class="sxs-lookup"><span data-stu-id="65658-105">Instrumenting the code is the basis for most other aspects of monitoring your services.</span></span> <span data-ttu-id="65658-106">A instrumentação é a única maneira que você possa saber que algo está errado e para diagnosticar o que precisa ser corrigido.</span><span class="sxs-lookup"><span data-stu-id="65658-106">Instrumentation is the only way you can know that something is wrong, and to diagnose what needs to be fixed.</span></span> <span data-ttu-id="65658-107">Embora tecnicamente é possível conectar um depurador a um serviço de produção, ele não é uma prática comum.</span><span class="sxs-lookup"><span data-stu-id="65658-107">Although technically it's possible to connect a debugger to a production service, it's not a common practice.</span></span> <span data-ttu-id="65658-108">Portanto, é importante ter dados de instrumentação detalhados.</span><span class="sxs-lookup"><span data-stu-id="65658-108">So, having detailed instrumentation data is important.</span></span>

<span data-ttu-id="65658-109">Alguns produtos instrumentam automaticamente seu código.</span><span class="sxs-lookup"><span data-stu-id="65658-109">Some products automatically instrument your code.</span></span> <span data-ttu-id="65658-110">Embora essas soluções podem funcionar bem, quase sempre a instrumentação manual é necessária.</span><span class="sxs-lookup"><span data-stu-id="65658-110">Although these solutions can work well, manual instrumentation is almost always required.</span></span> <span data-ttu-id="65658-111">No fim das contas, você deve ter informações suficientes para depurar legalmente o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="65658-111">In the end, you must have enough information to forensically debug the application.</span></span> <span data-ttu-id="65658-112">Este documento descreve as diferentes abordagens para instrumentar seu código quando for necessário escolher uma abordagem em vez de outra.</span><span class="sxs-lookup"><span data-stu-id="65658-112">This document describes different approaches to instrumenting your code, and when to choose one approach over another.</span></span>

## <a name="eventsource"></a><span data-ttu-id="65658-113">EventSource</span><span class="sxs-lookup"><span data-stu-id="65658-113">EventSource</span></span>
<span data-ttu-id="65658-114">Quando você cria uma solução do Service Fabric de um modelo do Visual Studio, uma classe derivada de **EventSource** (**ServiceEventSource** ou **ActorEventSource**) é gerada.</span><span class="sxs-lookup"><span data-stu-id="65658-114">When you create a Service Fabric solution from a template in Visual Studio, an **EventSource**-derived class (**ServiceEventSource** or **ActorEventSource**) is generated.</span></span> <span data-ttu-id="65658-115">Um modelo é criado, no qual você pode adicionar eventos para seu aplicativo ou serviço.</span><span class="sxs-lookup"><span data-stu-id="65658-115">A template is created, in which you can add events for your application or service.</span></span> <span data-ttu-id="65658-116">O nome **EventSource** **deve** ser exclusivo e deve ser renomeado na cadeia de caracteres do modelo padrão MyCompany-&lt;solution&gt;-&lt;project&gt;.</span><span class="sxs-lookup"><span data-stu-id="65658-116">The **EventSource** name **must** be unique, and should be renamed from the default template string MyCompany-&lt;solution&gt;-&lt;project&gt;.</span></span> <span data-ttu-id="65658-117">Ter várias definições de **EventSource** que usam o mesmo nome causa um problema no tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="65658-117">Having multiple **EventSource** definitions that use the same name causes an issue at run time.</span></span> <span data-ttu-id="65658-118">Cada evento definido deve ter um identificador exclusivo.</span><span class="sxs-lookup"><span data-stu-id="65658-118">Each defined event must have a unique identifier.</span></span> <span data-ttu-id="65658-119">Se um identificador não for exclusivo, ocorrerá uma falha de tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="65658-119">If an identifier is not unique, a runtime failure occurs.</span></span> <span data-ttu-id="65658-120">Algumas organizações atribuem antecipadamente intervalos de valores para evitar conflitos entre equipes de desenvolvimento separadas.</span><span class="sxs-lookup"><span data-stu-id="65658-120">Some organizations preassign ranges of values for identifiers to avoid conflicts between separate development teams.</span></span> <span data-ttu-id="65658-121">Para saber mais, veja [blog do Vance](https://blogs.msdn.microsoft.com/vancem/2012/07/09/introduction-tutorial-logging-etw-events-in-c-system-diagnostics-tracing-eventsource/) ou a [documentação do MSDN](https://msdn.microsoft.com/library/dn774985(v=pandp.20).aspx).</span><span class="sxs-lookup"><span data-stu-id="65658-121">For more information, see [Vance's blog](https://blogs.msdn.microsoft.com/vancem/2012/07/09/introduction-tutorial-logging-etw-events-in-c-system-diagnostics-tracing-eventsource/) or the [MSDN documentation](https://msdn.microsoft.com/library/dn774985(v=pandp.20).aspx).</span></span>

### <a name="using-structured-eventsource-events"></a><span data-ttu-id="65658-122">Usando eventos estruturados de EventSource</span><span class="sxs-lookup"><span data-stu-id="65658-122">Using structured EventSource events</span></span>

<span data-ttu-id="65658-123">Cada um dos eventos nos exemplos de código nesta seção são definidos para um caso específico, por exemplo, quando um tipo de serviço é registrado.</span><span class="sxs-lookup"><span data-stu-id="65658-123">Each of the events in the code examples in this section are defined for a specific case, for example, when a service type is registered.</span></span> <span data-ttu-id="65658-124">Quando você definir mensagens pelo caso de uso, dados podem ser empacotados com o texto do erro e mais, você pode facilmente procurar e filtrar com base nos nomes ou valores das propriedades especificadas.</span><span class="sxs-lookup"><span data-stu-id="65658-124">When you define messages by use case, data can be packaged with the text of the error, and you can more easily search and filter based on the names or values of the specified properties.</span></span> <span data-ttu-id="65658-125">Estruturar a saída de instrumentação torna o consumo mais fácil, mas exige mais ideias e mais tempo para definir um novo evento para cada caso de uso.</span><span class="sxs-lookup"><span data-stu-id="65658-125">Structuring the instrumentation output makes it easier to consume, but requires more thought and time to define a new event for each use case.</span></span> <span data-ttu-id="65658-126">Algumas definições de eventos podem ser compartilhadas em todo o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="65658-126">Some event definitions can be shared across the entire application.</span></span> <span data-ttu-id="65658-127">Por exemplo, um evento de início ou de parada de método seria reutilizado em vários serviços em um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="65658-127">For example, a method start or stop event would be reused across many services within an application.</span></span> <span data-ttu-id="65658-128">Um serviço de domínio específico, como um sistema de pedidos, pode ter um evento **CreateOrder**, que terá seu próprio evento exclusivo.</span><span class="sxs-lookup"><span data-stu-id="65658-128">A domain-specific service, like an order system, might have a **CreateOrder** event, which has its own unique event.</span></span> <span data-ttu-id="65658-129">Essa abordagem pode gerar muitos eventos e potencialmente requer a coordenação de identificadores entre as equipes de projeto.</span><span class="sxs-lookup"><span data-stu-id="65658-129">This approach might generate many events, and potentially require coordination of identifiers across project teams.</span></span> 

```csharp
    [EventSource(Name = "MyCompany-VotingState-VotingStateService")]
    internal sealed class ServiceEventSource : EventSource
    {
        public static readonly ServiceEventSource Current = new ServiceEventSource();

        // The instance constructor is private to enforce singleton semantics.
        private ServiceEventSource() : base() { }

        ...

        // The ServiceTypeRegistered event contains a unique identifier, an event attribute that defined the event, and the code implementation of the event.
        private const int ServiceTypeRegisteredEventId = 3;
        [Event(ServiceTypeRegisteredEventId, Level = EventLevel.Informational, Message = "Service host process {0} registered service type {1}", Keywords = Keywords.ServiceInitialization)]
        public void ServiceTypeRegistered(int hostProcessId, string serviceType)
        {
            WriteEvent(ServiceTypeRegisteredEventId, hostProcessId, serviceType);
        }

        // The ServiceHostInitializationFailed event contains a unique identifier, an event attribute that defined the event, and the code implementation of the event.
        private const int ServiceHostInitializationFailedEventId = 4;
        [Event(ServiceHostInitializationFailedEventId, Level = EventLevel.Error, Message = "Service host initialization failed", Keywords = Keywords.ServiceInitialization)]
        public void ServiceHostInitializationFailed(string exception)
        {
            WriteEvent(ServiceHostInitializationFailedEventId, exception);
        }
```

### <a name="using-eventsource-generically"></a><span data-ttu-id="65658-130">Usando o EventSource de forma genérica</span><span class="sxs-lookup"><span data-stu-id="65658-130">Using EventSource generically</span></span>

<span data-ttu-id="65658-131">Como definir eventos específicos pode ser difícil, muitas pessoas definem alguns eventos com um conjunto comum de parâmetros que geralmente emitem suas informações como uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="65658-131">Because defining specific events can be difficult, many people define a few events with a common set of parameters that generally output their information as a string.</span></span> <span data-ttu-id="65658-132">Grande parte do aspecto estruturado é perdida, tornando mais difícil pesquisar e filtrar os resultados.</span><span class="sxs-lookup"><span data-stu-id="65658-132">Much of the structured aspect is lost, and it's more difficult to search and filter the results.</span></span> <span data-ttu-id="65658-133">Alguns eventos, geralmente correspondentes aos níveis de registro de log, são definidos com essa abordagem.</span><span class="sxs-lookup"><span data-stu-id="65658-133">In this approach, a few events that usually correspond to the logging levels are defined.</span></span> <span data-ttu-id="65658-134">O trecho a seguir define uma mensagem de erro e de depuração:</span><span class="sxs-lookup"><span data-stu-id="65658-134">The following snippet defines a debug and error message:</span></span>

```csharp
    [EventSource(Name = "MyCompany-VotingState-VotingStateService")]
    internal sealed class ServiceEventSource : EventSource
    {
        public static readonly ServiceEventSource Current = new ServiceEventSource();

        // The Instance constructor is private, to enforce singleton semantics.
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

<span data-ttu-id="65658-135">Usar uma mistura de instrumentação genérica e não estruturados também pode funcionar bem.</span><span class="sxs-lookup"><span data-stu-id="65658-135">Using a hybrid of structured and generic instrumentation also can work well.</span></span> <span data-ttu-id="65658-136">A instrumentação estruturada é usada para relatar erros e métricas.</span><span class="sxs-lookup"><span data-stu-id="65658-136">Structured instrumentation is used for reporting errors and metrics.</span></span> <span data-ttu-id="65658-137">Eventos genéricos podem ser usados para o log detalhado que é consumido pelos engenheiros para solução de problemas.</span><span class="sxs-lookup"><span data-stu-id="65658-137">Generic events can be used for the detailed logging that is consumed by engineers for troubleshooting.</span></span>

## <a name="aspnet-core-logging"></a><span data-ttu-id="65658-138">Registro em log de ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="65658-138">ASP.NET Core logging</span></span>

<span data-ttu-id="65658-139">É importante planejar cuidadosamente como você instrumentará o seu código.</span><span class="sxs-lookup"><span data-stu-id="65658-139">It's important to carefully plan how you will instrument your code.</span></span> <span data-ttu-id="65658-140">O plano de instrumentação certa pode ajudar a evitar potencialmente desestabilizar sua base de código e, em seguida, precisar reinstrument o código.</span><span class="sxs-lookup"><span data-stu-id="65658-140">The right instrumentation plan can help you avoid potentially destabilizing your code base, and then needing to reinstrument the code.</span></span> <span data-ttu-id="65658-141">Para reduzir o risco, você pode escolher uma biblioteca de instrumentação como [Microsoft.Extensions.Logging](https://www.nuget.org/packages/Microsoft.Extensions.Logging/), que faz parte do Microsoft ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="65658-141">To reduce risk, you can choose an instrumentation library like [Microsoft.Extensions.Logging](https://www.nuget.org/packages/Microsoft.Extensions.Logging/), which is part of Microsoft ASP.NET Core.</span></span> <span data-ttu-id="65658-142">Núcleo do ASP.NET tem um [ILogger](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.ilogger) interface que você pode usar com o provedor de sua escolha, minimizando o efeito no código existente.</span><span class="sxs-lookup"><span data-stu-id="65658-142">ASP.NET Core has an [ILogger](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.ilogger) interface that you can use with the provider of your choice, while minimizing the effect on existing code.</span></span> <span data-ttu-id="65658-143">Você pode usar o código ASP.NET Core no Windows e Linux e no .NET Framework completo, então o código de instrumentação é padronizado.</span><span class="sxs-lookup"><span data-stu-id="65658-143">You can use the code in ASP.NET Core on Windows and Linux, and in the full .NET Framework, so your instrumentation code is standardized.</span></span> <span data-ttu-id="65658-144">Isso é explorado em mais detalhes abaixo:</span><span class="sxs-lookup"><span data-stu-id="65658-144">This is further explored below:</span></span>

### <a name="using-microsoftextensionslogging-in-service-fabric"></a><span data-ttu-id="65658-145">Uso de Microsoft.Extensions.Logging no Service Fabric</span><span class="sxs-lookup"><span data-stu-id="65658-145">Using Microsoft.Extensions.Logging in Service Fabric</span></span>

1. <span data-ttu-id="65658-146">Adicione o pacote NuGet Microsoft.Extensions.Logging ao projeto que você deseja instrumentar.</span><span class="sxs-lookup"><span data-stu-id="65658-146">Add the Microsoft.Extensions.Logging NuGet package to the project you want to instrument.</span></span> <span data-ttu-id="65658-147">Além disso, adicione os pacotes de provedor (para um pacote de produtos de terceiros, veja o exemplo a seguir).</span><span class="sxs-lookup"><span data-stu-id="65658-147">Also, add any provider packages (for a third-party package, see the following example).</span></span> <span data-ttu-id="65658-148">Para saber mais, veja [Entrar no ASP.NET Core](https://docs.microsoft.com/aspnet/core/fundamentals/logging).</span><span class="sxs-lookup"><span data-stu-id="65658-148">For more information, see [Logging in ASP.NET Core](https://docs.microsoft.com/aspnet/core/fundamentals/logging).</span></span>
2. <span data-ttu-id="65658-149">Adicione uma diretiva **using** para Microsoft.Extensions.Logging ao seu arquivo de serviço.</span><span class="sxs-lookup"><span data-stu-id="65658-149">Add a **using** directive for Microsoft.Extensions.Logging to your service file.</span></span>
3. <span data-ttu-id="65658-150">Definir uma variável privada em sua classe de serviço.</span><span class="sxs-lookup"><span data-stu-id="65658-150">Define a private variable within your service class.</span></span>

  ```csharp
  private ILogger _logger = null;

  ```
4. <span data-ttu-id="65658-151">No construtor da sua classe de serviço, adicione este código:</span><span class="sxs-lookup"><span data-stu-id="65658-151">In the constructor of your service class, add this code:</span></span>

  ```csharp
  _logger = new LoggerFactory().CreateLogger<Stateless>();

  ```
5. <span data-ttu-id="65658-152">Iniciar a instrumentação do código em seus métodos.</span><span class="sxs-lookup"><span data-stu-id="65658-152">Start instrumenting your code in your methods.</span></span> <span data-ttu-id="65658-153">Veja alguns exemplos:</span><span class="sxs-lookup"><span data-stu-id="65658-153">Here are a few samples:</span></span>

  ```csharp
  _logger.LogDebug("Debug-level event from Microsoft.Logging");
  _logger.LogInformation("Informational-level event from Microsoft.Logging");

  // In this variant, we're adding structured properties RequestName and Duration, which have values MyRequest and the duration of the request.
  // Later in the article, we discuss why this step is useful.
  _logger.LogInformation("{RequestName} {Duration}", "MyRequest", requestDuration);

  ```

## <a name="using-other-logging-providers"></a><span data-ttu-id="65658-154">Usando outros provedores de registro log</span><span class="sxs-lookup"><span data-stu-id="65658-154">Using other logging providers</span></span>

<span data-ttu-id="65658-155">Alguns provedores de terceiros usam a abordagem descrita na seção anterior, incluindo [Serilog](https://serilog.net/), [NLog](http://nlog-project.org/) e [Loggr](https://github.com/imobile3/Loggr.Extensions.Logging).</span><span class="sxs-lookup"><span data-stu-id="65658-155">Some third-party providers use the approach described in the preceding section, including [Serilog](https://serilog.net/), [NLog](http://nlog-project.org/), and [Loggr](https://github.com/imobile3/Loggr.Extensions.Logging).</span></span> <span data-ttu-id="65658-156">Você pode conectar cada uma delas no log do ASP.NET Core, ou pode usá-las separadamente.</span><span class="sxs-lookup"><span data-stu-id="65658-156">You can plug each of these into ASP.NET Core logging, or you can use them separately.</span></span> <span data-ttu-id="65658-157">O Serilog tem um recurso que aprimora todas as mensagens enviadas de um agente de log.</span><span class="sxs-lookup"><span data-stu-id="65658-157">Serilog has a feature that enriches all messages sent from a logger.</span></span> <span data-ttu-id="65658-158">Esse recurso pode ser útil para saída do nome do serviço, do tipo e das informações de partição.</span><span class="sxs-lookup"><span data-stu-id="65658-158">This feature can be useful to output the service name, type, and partition information.</span></span> <span data-ttu-id="65658-159">Para usar esse recurso na infra-estrutura do ASP.NET Core, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="65658-159">To use this capability in the ASP.NET Core infrastructure, do these steps:</span></span>

1. <span data-ttu-id="65658-160">Adicione os pacotes NuGet Serilog, Serilog.Extensions.Logging e Serilog.Sinks.Observable ao projeto.</span><span class="sxs-lookup"><span data-stu-id="65658-160">Add the Serilog, Serilog.Extensions.Logging, and Serilog.Sinks.Observable NuGet packages to the project.</span></span> <span data-ttu-id="65658-161">No próximo exemplo, adicione também Serilog.Sinks.Literate.</span><span class="sxs-lookup"><span data-stu-id="65658-161">For the next example, also add Serilog.Sinks.Literate.</span></span> <span data-ttu-id="65658-162">Uma abordagem melhor será mostrada posteriormente neste artigo.</span><span class="sxs-lookup"><span data-stu-id="65658-162">A better approach is shown later in this article.</span></span>
2. <span data-ttu-id="65658-163">No Serilog, crie uma LoggerConfiguration e a instância do agente.</span><span class="sxs-lookup"><span data-stu-id="65658-163">In Serilog, create a LoggerConfiguration and the logger instance.</span></span>

  ```csharp
  Log.Logger = new LoggerConfiguration().WriteTo.LiterateConsole().CreateLogger();
  ```

3. <span data-ttu-id="65658-164">Adicione um argumento SeriLog.ILogger ao construtor do serviço e passe o agente recém-criado.</span><span class="sxs-lookup"><span data-stu-id="65658-164">Add a Serilog.ILogger argument to the service constructor, and pass the newly created logger.</span></span>

  ```csharp
  ServiceRuntime.RegisterServiceAsync("StatelessType", context => new Stateless(context, Log.Logger)).GetAwaiter().GetResult();
  ```

4. <span data-ttu-id="65658-165">No construtor de serviço, adicione o código a seguir, que cria os enriquecedores de propriedade para as propriedades **ServiceTypeName**, **ServiceName**, **PartitionId** e **InstanceId** do serviço.</span><span class="sxs-lookup"><span data-stu-id="65658-165">In the service constructor, add the following code, which creates the property enrichers for the **ServiceTypeName**, **ServiceName**, **PartitionId**, and **InstanceId** properties of the service.</span></span> <span data-ttu-id="65658-166">Ele também adiciona um aprimorador de propriedade para a fábrica de logs do ASP.NET Core, para que você possa usar Microsoft.Extensions.Logging.ILogger no seu código.</span><span class="sxs-lookup"><span data-stu-id="65658-166">It also adds a property enricher to the ASP.NET Core logging factory, so you can use Microsoft.Extensions.Logging.ILogger in your code.</span></span>

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

5. <span data-ttu-id="65658-167">Instrumente o código da mesma forma com se você estivesse usando o ASP.NET Core sem SeriLog.</span><span class="sxs-lookup"><span data-stu-id="65658-167">Instrument the code the same as if you were using ASP.NET Core without Serilog.</span></span>

  >[!NOTE]
  ><span data-ttu-id="65658-168">É recomendável que você não use o Log.Logger estático com o exemplo anterior.</span><span class="sxs-lookup"><span data-stu-id="65658-168">We recommend that you don't use the static Log.Logger with the preceding example.</span></span> <span data-ttu-id="65658-169">O Service Fabric pode hospedar várias instâncias do mesmo tipo de serviço em um único processo.</span><span class="sxs-lookup"><span data-stu-id="65658-169">Service Fabric can host multiple instances of the same service type within a single process.</span></span> <span data-ttu-id="65658-170">Se você usar o Log.Logger estático, o último gravador de aprimoradores de propriedade mostrará valores para todas as instâncias em execução.</span><span class="sxs-lookup"><span data-stu-id="65658-170">If you use the static Log.Logger, the last writer of the property enrichers will show values for all instances that are running.</span></span> <span data-ttu-id="65658-171">É por isso que a variável _logger é uma variável de membro particular da classe de serviço.</span><span class="sxs-lookup"><span data-stu-id="65658-171">This is one reason why the _logger variable is a private member variable of the service class.</span></span> <span data-ttu-id="65658-172">Além disso, você deve disponibilizar o _logger para código comum, que pode ser usado entre serviços.</span><span class="sxs-lookup"><span data-stu-id="65658-172">Also, you must make the _logger available to common code, which might be used across services.</span></span>

## <a name="choosing-a-logging-provider"></a><span data-ttu-id="65658-173">Escolher um provedor de log</span><span class="sxs-lookup"><span data-stu-id="65658-173">Choosing a logging provider</span></span>

<span data-ttu-id="65658-174">Se o aplicativo depende de alto desempenho, o **EventSource** geralmente é uma boa abordagem.</span><span class="sxs-lookup"><span data-stu-id="65658-174">If your application relies on high performance, **EventSource** is usually a good approach.</span></span> <span data-ttu-id="65658-175">**EventSource** *geralmente* usa menos recursos e é melhor do que o ASP.NET Core log ou qualquer das soluções de terceiros disponíveis.</span><span class="sxs-lookup"><span data-stu-id="65658-175">**EventSource** *generally* uses fewer resources and performs better than ASP.NET Core logging or any of the available third-party solutions.</span></span>  <span data-ttu-id="65658-176">Isso não é um problema para muitos serviços, mas se o seu serviço for orientado ao desempenho, usar o **EventSource** poderá ser uma opção melhor.</span><span class="sxs-lookup"><span data-stu-id="65658-176">This isn't an issue for many services, but if your service is performance-oriented, using **EventSource** might be a better choice.</span></span> <span data-ttu-id="65658-177">No entanto, para obter esses benefícios do registro em log estruturado, o **EventSource** requer um grande investimento da equipe de engenharia.</span><span class="sxs-lookup"><span data-stu-id="65658-177">However, to get these benefits of structured logging, **EventSource** requires a larger investment from your engineering team.</span></span> <span data-ttu-id="65658-178">Se possível, crie um protótipo rápido de algumas opções de log e escolha a que melhor atende às suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="65658-178">If possible, do a quick prototype of a few logging options, and then choose the one that best meets your needs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="65658-179">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="65658-179">Next steps</span></span>

<span data-ttu-id="65658-180">Após escolher o provedor de log para instrumentar os aplicativos e serviços, os logs e eventos precisam ser agregados para que possam ser enviados a qualquer plataforma de análise.</span><span class="sxs-lookup"><span data-stu-id="65658-180">Once you have chosen your logging provider to instrument your applications and services, your logs and events need to be aggregated before they can be sent to any analysis platform.</span></span> <span data-ttu-id="65658-181">Leia sobre o [EventFlow](service-fabric-diagnostics-event-aggregation-eventflow.md) e o [WAD](service-fabric-diagnostics-event-aggregation-wad.md) para entender melhor algumas das opções recomendadas.</span><span class="sxs-lookup"><span data-stu-id="65658-181">Read about [EventFlow](service-fabric-diagnostics-event-aggregation-eventflow.md) and [WAD](service-fabric-diagnostics-event-aggregation-wad.md) to better understand some of the recommended options.</span></span>
