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
# <a name="application-and-service-level-event-and-log-generation"></a>Geração de logs e eventos de nível de aplicativo e serviço

## <a name="instrumenting-hello-code-with-custom-events"></a>Código de instrumentação Olá com eventos personalizados

Instrumentação de código Olá é a base de Olá para a maioria dos outros aspectos de seus serviços de monitoramento. Instrumentação é única forma de saudação que você possa saber que algo está errado e toodiagnose que precisa toobe fixa. Embora seja tecnicamente possível tooconnect um serviço de produção do depurador tooa, não é uma prática comum. Portanto, é importante ter dados de instrumentação detalhados.

Alguns produtos instrumentam automaticamente seu código. Embora essas soluções podem funcionar bem, quase sempre a instrumentação manual é necessária. No final do hello, você deve ter suficiente tooforensically informações depurar o aplicativo hello. Este documento descreve abordagens diferentes tooinstrumenting seu código, e quando toochoose uma abordagem em detrimento de outro.

## <a name="eventsource"></a>EventSource
Quando você cria uma solução do Service Fabric de um modelo do Visual Studio, uma classe derivada de **EventSource** (**ServiceEventSource** ou **ActorEventSource**) é gerada. Um modelo é criado, no qual você pode adicionar eventos para seu aplicativo ou serviço. Olá **EventSource** nome **deve** ser exclusivo e deve ser renomeado de cadeia de caracteres de saudação padrão modelo MyCompany -&lt;solução&gt; - &lt; projeto&gt;. Ter várias **EventSource** definições que usam Olá mesmo nome faz com que um problema no tempo de execução. Cada evento definido deve ter um identificador exclusivo. Se um identificador não for exclusivo, ocorrerá uma falha de tempo de execução. Algumas organizações preassign intervalos de valores para conflitos de tooavoid de identificadores entre as equipes de desenvolvimento separado. Para obter mais informações, consulte [blog de Vance](https://blogs.msdn.microsoft.com/vancem/2012/07/09/introduction-tutorial-logging-etw-events-in-c-system-diagnostics-tracing-eventsource/) ou hello [documentação MSDN](https://msdn.microsoft.com/library/dn774985(v=pandp.20).aspx).

### <a name="using-structured-eventsource-events"></a>Usando eventos estruturados de EventSource

Cada um dos eventos de saudação nos exemplos de código Olá nesta seção são definidas para um caso específico, por exemplo, quando um tipo de serviço é registrado. Quando você definir mensagens pelo caso de uso, dados podem ser empacotados com o texto de saudação do erro hello e você pode mais facilmente de pesquisa e filtro com base em nomes de saudação ou valores de saudação as propriedades especificadas. Estruturar a saída de instrumentação Olá torna mais fácil tooconsume, mas exige mais trabalho e hora toodefine um novo evento para cada caso de uso. Algumas definições de evento podem ser compartilhadas em todo o aplicativo hello. Por exemplo, um evento de início ou de parada de método seria reutilizado em vários serviços em um aplicativo. Um serviço de domínio específico, como um sistema de pedidos, pode ter um evento **CreateOrder**, que terá seu próprio evento exclusivo. Essa abordagem pode gerar muitos eventos e potencialmente requer a coordenação de identificadores entre as equipes de projeto. 

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

### <a name="using-eventsource-generically"></a>Usando o EventSource de forma genérica

Como definir eventos específicos pode ser difícil, muitas pessoas definem alguns eventos com um conjunto comum de parâmetros que geralmente emitem suas informações como uma cadeia de caracteres. Muito aspecto Olá estruturado é perdido e é mais difícil toosearch e filtro Olá resultados. Nessa abordagem, alguns eventos que geralmente correspondem a níveis de log toohello são definidos. saudação de trecho de código a seguir define uma mensagem de erro e de depuração:

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

Usar uma mistura de instrumentação genérica e não estruturados também pode funcionar bem. A instrumentação estruturada é usada para relatar erros e métricas. Eventos genéricos podem ser usados para Olá detalhada log que é consumida pelos engenheiros para solução de problemas.

## <a name="aspnet-core-logging"></a>Registro em log de ASP.NET Core

É importante toocarefully planeje como você instruirá o seu código. plano de instrumentação direita Olá pode ajudar a evitar potencialmente desestabilizar sua base de código e, em seguida, a necessidade de código de saudação tooreinstrument. tooreduce risco, você pode escolher uma biblioteca de instrumentação como [Microsoft.Extensions.Logging](https://www.nuget.org/packages/Microsoft.Extensions.Logging/), que faz parte do Microsoft ASP.NET Core. ASP.NET Core tem um [ILogger](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.ilogger) interface que você pode usar com o provedor de saudação de sua escolha, minimizando o efeito de saudação em código existente. Você pode usar código de saudação em ASP.NET Core no Windows e Linux e no hello completa do .NET Framework, para que seu código de instrumentação é padronizado. Isso é explorado em mais detalhes abaixo:

### <a name="using-microsoftextensionslogging-in-service-fabric"></a>Uso de Microsoft.Extensions.Logging no Service Fabric

1. Adicione Olá Microsoft.Extensions.Logging NuGet pacote toohello projeto você deseja tooinstrument. Além disso, adicionar todos os pacotes de provedor (para um pacote de terceiros, consulte Olá exemplo a seguir). Para saber mais, veja [Entrar no ASP.NET Core](https://docs.microsoft.com/aspnet/core/fundamentals/logging).
2. Adicionar um **usando** diretiva para o arquivo de serviço tooyour Microsoft.Extensions.Logging.
3. Definir uma variável privada em sua classe de serviço.

  ```csharp
  private ILogger _logger = null;

  ```
4. No construtor de saudação da sua classe de serviço, adicione este código:

  ```csharp
  _logger = new LoggerFactory().CreateLogger<Stateless>();

  ```
5. Iniciar a instrumentação do código em seus métodos. Veja alguns exemplos:

  ```csharp
  _logger.LogDebug("Debug-level event from Microsoft.Logging");
  _logger.LogInformation("Informational-level event from Microsoft.Logging");

  // In this variant, we're adding structured properties RequestName and Duration, which have values MyRequest and hello duration of hello request.
  // Later in hello article, we discuss why this step is useful.
  _logger.LogInformation("{RequestName} {Duration}", "MyRequest", requestDuration);

  ```

## <a name="using-other-logging-providers"></a>Usando outros provedores de registro log

Alguns provedores de terceiros abordagem Olá descrito em Olá anterior seção, incluindo [Serilog](https://serilog.net/), [NLog](http://nlog-project.org/), e [Loggr](https://github.com/imobile3/Loggr.Extensions.Logging). Você pode conectar cada uma delas no log do ASP.NET Core, ou pode usá-las separadamente. O Serilog tem um recurso que aprimora todas as mensagens enviadas de um agente de log. Esse recurso pode ser útil toooutput Olá nome, tipo e informações de partição. toouse esse recurso no hello infraestrutura do ASP.NET Core, siga estas etapas:

1. Adicione Olá Serilog, Serilog.Extensions.Logging, e pacotes do Serilog.Sinks.Observable NuGet toohello projeto. Para o exemplo a seguir hello, também adicione Serilog.Sinks.Literate. Uma abordagem melhor será mostrada posteriormente neste artigo.
2. Serilog, cria uma instância de agente LoggerConfiguration e hello.

  ```csharp
  Log.Logger = new LoggerConfiguration().WriteTo.LiterateConsole().CreateLogger();
  ```

3. Adicione um construtor de serviço Serilog.ILogger argumento toohello e passar Olá recém-criado agente de log.

  ```csharp
  ServiceRuntime.RegisterServiceAsync("StatelessType", context => new Stateless(context, Log.Logger)).GetAwaiter().GetResult();
  ```

4. No construtor de serviço hello, adicionar Olá seguindo o código, que cria Olá enrichers de propriedade para Olá **ServiceTypeName**, **ServiceName**, **PartitionId**e  **InstanceId** propriedades do serviço de saudação. Ele também adiciona uma toohello enricher de propriedade fábrica de registro do ASP.NET Core, então você pode usar Microsoft.Extensions.Logging.ILogger no seu código.

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

5. Código do instrumento Olá Olá mesmo como se estivesse usando o ASP.NET Core sem Serilog.

  >[!NOTE]
  >É recomendável que você não use Olá estático Log.Logger com hello anterior de exemplo. Serviço de malha pode hospedar várias instâncias de saudação do mesmo serviço tipo em um único processo. Se você usar Olá Log.Logger estático, último gravador saudação do enrichers de propriedade Olá mostrará valores para todas as instâncias que estão em execução. Este é um motivo por que a variável logger de saudação é uma variável de membro particular da classe de serviço hello. Além disso, você deve tornar o código de toocommon disponíveis do hello Logger, que pode ser usado em serviços.

## <a name="choosing-a-logging-provider"></a>Escolher um provedor de log

Se o aplicativo depende de alto desempenho, o **EventSource** geralmente é uma boa abordagem. **EventSource** *geralmente* usa menos recursos e é melhor do que o ASP.NET Core log ou qualquer uma das soluções de terceiros disponíveis hello.  Isso não é um problema para muitos serviços, mas se o seu serviço for orientado ao desempenho, usar o **EventSource** poderá ser uma opção melhor. No entanto, tooget esses benefícios de estruturado de registro em log, **EventSource** requer um investimento maior da sua equipe de engenharia. Se possível, siga um protótipo rápido algumas das opções de log e escolha Olá que melhor atenda às suas necessidades.

## <a name="next-steps"></a>Próximas etapas

Depois de ter escolhido o tooinstrument do provedor de log de seus aplicativos e serviços, seus logs e eventos necessário toobe agregado para que eles possam ser enviados tooany plataforma de análise. Leia sobre [EventFlow](service-fabric-diagnostics-event-aggregation-eventflow.md) e [WAD](service-fabric-diagnostics-event-aggregation-wad.md) toobetter entender alguns dos Olá opções recomendada.
