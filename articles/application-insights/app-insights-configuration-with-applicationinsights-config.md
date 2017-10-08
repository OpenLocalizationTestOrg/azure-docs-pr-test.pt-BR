---
title: "referência de aaaApplicationInsights.config - Azure | Microsoft Docs"
description: "Habilitar ou desabilitar módulos de coleta de dados e adicionar contadores de desempenho e outros parâmetros."
services: application-insights
documentationcenter: 
author: OlegAnaniev-MSFT
editor: alancameronwills
manager: carmonm
ms.assetid: 6e397752-c086-46e9-8648-a1196e8078c2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/3/2017
ms.author: bwren
ms.openlocfilehash: 76cb11349d87dfc508ec8b1c454259a0b079c48a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-hello-application-insights-sdk-with-applicationinsightsconfig-or-xml"></a>Configurar Olá SDK do Application Insights com applicationinsights. config ou. XML
Olá SDK .NET do Application Insights consiste em um número de pacotes do NuGet. O [pacote core](http://www.nuget.org/packages/Microsoft.ApplicationInsights) fornece a API de hello para enviar telemetria à saudação do Application Insights. Os [pacotes adicionais](http://www.nuget.org/packages?q=Microsoft.ApplicationInsights) fornecem *módulos* e *inicializadores* de telemetria para rastreamento automático de telemetria do seu aplicativo e respectivo contexto. Ajustando o arquivo de configuração hello, habilitar ou desabilitar inicializadores e módulos de telemetria e definir parâmetros para algumas delas.

arquivo de configuração de saudação é nomeado `ApplicationInsights.config` ou `ApplicationInsights.xml`, dependendo do tipo de saudação do seu aplicativo. Ele é adicionado automaticamente tooyour projeto quando você [instalar a maioria das versões do SDK do hello][start]. Ele também é adicionado tooa web aplicativo por [Monitor de Status em um servidor IIS][redfield], ou quando você seleciona Olá aplicativo Insights [extensão para um site do Azure ou VM](app-insights-azure-web-apps.md).

Não há uma saudação de toocontrol arquivo equivalente [SDK em uma página da web][client].

Este documento descreve as seções de saudação que você vê na configuração de saudação do arquivo, como controlar os componentes de saudação do hello SDK, e os pacotes do NuGet carregar esses componentes.

## <a name="telemetry-modules-aspnet"></a>Módulos de telemetria (ASP.NET)
Cada módulo de telemetria coleta um tipo específico de dados e usa o núcleo de saudação dados de saudação toosend API. módulos de saudação são instalados por diferentes pacotes do NuGet, que também adicionar o arquivo. config do hello linhas necessárias toohello.

Há um nó no arquivo de configuração de saudação para cada módulo. toodisable um módulo, exclua o nó hello ou comente-o.

### <a name="dependency-tracking"></a>Acompanhamento de dependência
[Controle de dependência](app-insights-asp-net-dependencies.md) coleta a telemetria sobre chamadas de seu aplicativo torna toodatabases e bancos de dados e serviços externos. tooallow toowork esse módulo em um servidor IIS, é necessário muito[instalar o Monitor de Status][redfield]. toouse-la em aplicativos web do Azure ou máquinas virtuais, [Selecionar extensão do Application Insights Olá](app-insights-azure-web-apps.md).

Você também pode escrever seu próprio controle de código usando a saudação de dependência [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency).

* `Microsoft.ApplicationInsights.DependencyCollector.DependencyTrackingTelemetryModule`
* [Microsoft.ApplicationInsights.DependencyCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.DependencyCollector) .

### <a name="performance-collector"></a>Coletor de desempenho
[Coleta contadores de desempenho do sistema](app-insights-performance-counters.md), como CPU, memória e carga de rede de instalações do IIS. Você pode especificar quais toocollect contadores, incluindo contadores de desempenho que você configurou por conta própria.

* `Microsoft.ApplicationInsights.Extensibility.PerfCounterCollector.PerformanceCollectorModule`
* [Microsoft.ApplicationInsights.PerfCounterCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.PerfCounterCollector) .

### <a name="application-insights-diagnostics-telemetry"></a>Telemetria de diagnóstico do Application Insights
Olá `DiagnosticsTelemetryModule` relata erros em Olá próprio código de instrumentação do Application Insights. Por exemplo, se o código de saudação não pode acessar os contadores de desempenho ou se um `ITelemetryInitializer` lança uma exceção. Telemetria de rastreamento controlada por esse módulo aparece no hello [pesquisa diagnóstico][diagnostic]. Envia dados de diagnóstico toodc.services.vsallin.net.

* `Microsoft.ApplicationInsights.Extensibility.Implementation.Tracing.DiagnosticsTelemetryModule`
* [Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) . Se você só pode instalar esse pacote, arquivo applicationinsights. config de saudação não será criado automaticamente.

### <a name="developer-mode"></a>Modo de desenvolvedor
`DeveloperModeWithDebuggerAttachedTelemetryModule`força Olá Application Insights `TelemetryChannel` toosend dados imediatamente, item de um telemetria por vez, quando um depurador é anexado toohello o processo do aplicativo. Isso reduz a quantidade de saudação de tempo entre o momento de saudação quando seu aplicativo controla a telemetria e quando ele aparece no portal do Application Insights hello. Faz com uma sobrecarga significativa na largura de banda de CPU e rede.

* `Microsoft.ApplicationInsights.WindowsServer.DeveloperModeWithDebuggerAttachedTelemetryModule`
* [Application Insights Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) .

### <a name="web-request-tracking"></a>Acompanhamento de solicitação da Web
Olá relatórios [código de tempo e o resultado da resposta](app-insights-asp-net.md) de solicitações HTTP.

* `Microsoft.ApplicationInsights.Web.RequestTrackingTelemetryModule`
* [Microsoft.ApplicationInsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web) .

### <a name="exception-tracking"></a>Acompanhamento de exceções
`ExceptionTrackingTelemetryModule` rastreia exceção sem tratamento no seu aplicativo Web. Consulte [Falhas e exceções][exceptions].

* `Microsoft.ApplicationInsights.Web.ExceptionTrackingTelemetryModule`
* [Microsoft.ApplicationInsights.Web](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web) .
* `Microsoft.ApplicationInsights.WindowsServer.UnobservedExceptionTelemetryModule` -rastreia [exceções de tarefa não observada](http://blogs.msdn.com/b/pfxteam/archive/2011/09/28/task-exception-handling-in-net-4-5.aspx).
* `Microsoft.ApplicationInsights.WindowsServer.UnhandledExceptionTelemetryModule` -rastreia as exceções sem tratamento para funções de trabalho, serviços do Windows e aplicativos de console.
* [Application Insights Windows Server](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) .

### <a name="eventsource-tracking"></a>Monitoramento de EventSource
`EventSourceTelemetryModule`permite que você tooconfigure EventSource eventos toobe enviado tooApplication Insights como rastreamentos. Para obter informações sobre o monitoramento de eventos EventSource, consulte [Usando eventos EventSource](app-insights-asp-net-trace-logs.md#using-eventsource-events).

* `Microsoft.ApplicationInsights.EventSourceListener.EventSourceTelemetryModule`
* [Microsoft.ApplicationInsights.EventSourceListener](http://www.nuget.org/packages/Microsoft.ApplicationInsights.EventSourceListener) 

### <a name="etw-event-tracking"></a>Monitoramento de eventos ETW
`EtwCollectorTelemetryModule`permite que você tooconfigure eventos do ETW provedores toobe enviados tooApplication Insights como rastreamentos. Para obter informações sobre o monitoramento de eventos ETW, consulte [Usando eventos ETW](app-insights-asp-net-trace-logs.md#using-etw-events).

* `Microsoft.ApplicationInsights.EtwCollector.EtwCollectorTelemetryModule`
* [Microsoft.ApplicationInsights.EtwCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.EtwCollector) 

### <a name="microsoftapplicationinsights"></a>Microsoft.ApplicationInsights
pacote de Microsoft.ApplicationInsights Olá fornece Olá [core API](https://msdn.microsoft.com/library/mt420197.aspx) de saudação SDK. Olá outros módulos de telemetria usam isso, e você também pode [usá-lo toodefine sua telemetria](app-insights-api-custom-events-metrics.md).

* Nenhuma entrada em ApplicationInsights.config.
* [Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) . Se você acabou de instalar este NuGet, nenhum arquivo. config será gerado.

## <a name="telemetry-channel"></a>Canal de telemetria
canal de telemetria Olá gerencia o buffer e transmissão de telemetria toohello serviço Application Insights.

* `Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.ServerTelemetryChannel`é o canal de padrão de saudação para serviços. Ele armazena em buffer dados na memória.
* `Microsoft.ApplicationInsights.PersistenceChannel` é uma alternativa para aplicativos de console. Ele pode salvar qualquer armazenamento de dados unflushed toopersistent quando seu aplicativo encerra e será enviado quando o aplicativo hello começa novamente.

## <a name="telemetry-initializers-aspnet"></a>Inicializadores de telemetria (ASP.NET)
Os inicializadores de telemetria definem propriedades de contexto que são enviadas com cada item de telemetria.

Você pode [gravar seus próprio inicializadores](app-insights-api-filtering-sampling.md#add-properties) tooset propriedades de contexto.

inicializadores padrão Olá estão definidos por pacotes de Web ou WindowsServer NuGet hello:

* `AccountIdTelemetryInitializer`Define a propriedade AccountId hello.
* `AuthenticatedUserIdTelemetryInitializer`Define propriedades de AuthenticatedUserId hello como conjunto de por Olá SDK de JavaScript.
* `AzureRoleEnvironmentTelemetryInitializer`saudação de atualizações `RoleName` e `RoleInstance` propriedades de saudação `Device` contexto para todos os itens de telemetria com informações extraídas do ambiente de tempo de execução do Azure hello.
* `BuildInfoConfigComponentVersionTelemetryInitializer`saudação de atualizações `Version` propriedade Olá `Component` contexto para todos os itens de telemetria com valor de saudação extraídos da saudação `BuildInfo.config` arquivo produzido pelo MS Build.
* `ClientIpHeaderTelemetryInitializer`atualizações `Ip` propriedade Olá `Location` contexto de todos os itens de telemetria com base em Olá `X-Forwarded-For` cabeçalho HTTP de solicitação de saudação.
* `DeviceTelemetryInitializer`Olá atualizações seguintes propriedades de saudação `Device` contexto para todos os itens de telemetria.
  * `Type`está definido muito "Computador"
  * `Id`é definido toohello nome de domínio Olá computador onde o aplicativo da web hello está sendo executado.
  * `OemName`é definir o valor de toohello extraído da saudação `Win32_ComputerSystem.Manufacturer` campo usando o WMI.
  * `Model`é definir o valor de toohello extraído da saudação `Win32_ComputerSystem.Model` campo usando o WMI.
  * `NetworkType`é definir o valor de toohello extraído da saudação `NetworkInterface`.
  * `Language`é definir o nome toohello Olá `CurrentCulture`.
* `DomainNameRoleInstanceTelemetryInitializer`saudação de atualizações `RoleInstance` propriedade Olá `Device` contexto para todos os itens de telemetria com nome de domínio de saudação do computador Olá onde o aplicativo da web hello está sendo executado.
* `OperationNameTelemetryInitializer`saudação de atualizações `Name` propriedade Olá `RequestTelemetry` e hello `Name` propriedade Olá `Operation` contexto de todos os itens de telemetria com base no método hello HTTP, bem como nomes de saudação do ASP.NET MVC controlador e ação tooprocess invocado solicitação.
* `OperationIdTelemetryInitializer`ou `OperationCorrelationTelemetryInitializer` Olá atualizações `Operation.Id` propriedade de contexto de todos os itens de telemetria controlada ao tratar uma solicitação com hello gerado automaticamente `RequestTelemetry.Id`.
* `SessionTelemetryInitializer`saudação de atualizações `Id` propriedade Olá `Session` contexto para todos os itens de telemetria com valor extraído da saudação `ai_session` cookie gerado o código de instrumentação ApplicationInsights JavaScript em execução no navegador do usuário Olá Olá.
* `SyntheticTelemetryInitializer`ou `SyntheticUserAgentTelemetryInitializer` Olá atualizações `User`, `Session` e `Operation` propriedades de contextos de todos os itens de telemetria rastreadas ao lidar com uma solicitação de uma fonte sintética, como uma disponibilidade de teste ou o bot do mecanismo de pesquisa. Por padrão, o [Metrics Explorer](app-insights-metrics-explorer.md) não exibe telemetria sintética.

    Olá `<Filters>` definir identificando as propriedades das solicitações de saudação.
* `UserAgentTelemetryInitializer`saudação de atualizações `UserAgent` propriedade Olá `User` contexto de todos os itens de telemetria com base em Olá `User-Agent` cabeçalho HTTP de solicitação de saudação.
* `UserTelemetryInitializer`saudação de atualizações `Id` e `AcquisitionDate` propriedades de `User` contexto para todos os itens de telemetria com valores extraídos de saudação `ai_user` cookie gerada pelo código de instrumentação do hello Application Insights JavaScript em execução no Olá navegador do usuário.
* `WebTestTelemetryInitializer`conjuntos de Olá id de usuário, id de sessão e as propriedades de fonte sintético para solicitações de HTTP que venham de [testes de disponibilidade](app-insights-monitor-web-app-availability.md).
  Olá `<Filters>` definir identificando as propriedades das solicitações de saudação.

Para aplicativos .NET em execução no serviço de malha, você pode incluir Olá `Microsoft.ApplicationInsights.ServiceFabric` pacote NuGet. Este pacote inclui um `FabricTelemetryInitializer`, que adiciona propriedades tootelemetry itens de malha do serviço. Para obter mais informações, consulte Olá [página GitHub](https://go.microsoft.com/fwlink/?linkid=848457) sobre as propriedades de saudação adicionadas por este pacote do NuGet.

## <a name="telemetry-processors-aspnet"></a>Processadores de Telemetria (ASP.NET)
Processadores de telemetria podem filtrar e modificar cada item de telemetria apenas antes de serem enviado no portal de toohello Olá SDK.

Você pode [escrever seus próprios processadores de telemetria](app-insights-api-filtering-sampling.md#filtering).

#### <a name="adaptive-sampling-telemetry-processor-from-200-beta3"></a>Processador de telemetria de amostragem adaptável (da 2.0.0-beta3)
Isso é habilitado por padrão. Se o seu aplicativo envia muita telemetria, esse processador remove parte dela.

```xml

    <TelemetryProcessors>
      <Add Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.AdaptiveSamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">
        <MaxTelemetryItemsPerSecond>5</MaxTelemetryItemsPerSecond>
      </Add>
    </TelemetryProcessors>

```

parâmetro Hello fornece destino Olá Olá algoritmo tenta tooachieve. Cada instância de saudação que SDK funciona independentemente, portanto, se o servidor for um cluster de vários computadores, volume real de saudação de telemetria será multiplicado adequadamente.

[Saiba mais sobre a amostragem](app-insights-sampling.md).

#### <a name="fixed-rate-sampling-telemetry-processor-from-200-beta1"></a>Processador de telemetria de amostragem de taxa fixa (da 2.0.0-beta1)
Também há um [processador de telemetria de amostra](app-insights-api-filtering-sampling.md) padrão (de 2.0.1):

```XML

    <TelemetryProcessors>
     <Add Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.SamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">

     <!-- Set a percentage close too100/N where N is an integer. -->
     <!-- E.g. 50 (=100/2), 33.33 (=100/3), 25 (=100/4), 20, 1 (=100/100), 0.1 (=100/1000) -->
     <SamplingPercentage>10</SamplingPercentage>
     </Add>
   </TelemetryProcessors>

```



## <a name="channel-parameters-java"></a>Parâmetros de canal (Java)
Esses parâmetros afetam como hello Java SDK deve armazenar e liberar dados de telemetria Olá que coleta.

#### <a name="maxtelemetrybuffercapacity"></a>MaxTelemetryBufferCapacity
número de saudação de itens de telemetria que podem ser armazenados no armazenamento em memória de saudação do SDK. Quando esse número for atingido, Olá telemetria seja liberado - isto é, itens de telemetria de saudação são enviados server do Application Insights toohello.

* Mín.: 1
* Máx.: 1.000
* Padrão: 500

```

  <ApplicationInsights>
      ...
      <Channel>
       <MaxTelemetryBufferCapacity>100</MaxTelemetryBufferCapacity>
      </Channel>
      ...
  </ApplicationInsights>
```

#### <a name="flushintervalinseconds"></a>FlushIntervalInSeconds
Determina com que frequência hello dados armazenados no armazenamento em memória de saudação devem ser liberado (enviada tooApplication Insights).

* Mín.: 1
* Máx.: 300
* Padrão: 5

```

    <ApplicationInsights>
      ...
      <Channel>
        <FlushIntervalInSeconds>100</FlushIntervalInSeconds>
      </Channel>
      ...
    </ApplicationInsights>
```

#### <a name="maxtransmissionstoragecapacityinmb"></a>MaxTransmissionStorageCapacityInMB
Determina o tamanho máximo de saudação em MB alocado toohello o armazenamento persistente no disco local hello. Esse armazenamento é usado para persistir itens de telemetria que falharam toobe transmitido toohello Application Insights ponto de extremidade. Quando o tamanho do armazenamento Olá tem sido atendido, novos itens de telemetria serão descartados.

* Mín.: 1
* Máx.: 100
* Padrão: 10

```

   <ApplicationInsights>
      ...
      <Channel>
        <MaxTransmissionStorageCapacityInMB>50</MaxTransmissionStorageCapacityInMB>
      </Channel>
      ...
   </ApplicationInsights>
```



## <a name="instrumentationkey"></a>InstrumentationKey
Isso determina o recurso do Application Insights Olá na qual seus dados é exibida. Normalmente um recurso separado, com uma chave separada, é criado para cada um dos seus aplicativos.

Se você deseja tooset Olá chave dinamicamente - por exemplo, se você deseja que os resultados de toosend de seus recursos do aplicativo toodifferent - omitir chave Olá Olá do arquivo de configuração e defini-la no código.

chave de saudação tooset para todas as instâncias de TelemetryClient, incluindo módulos de telemetria padrão, defina a chave de saudação no TelemetryConfiguration.Active. Faça isso em um método de inicialização como global.aspx.cs em um serviço ASP.NET:

```C#

    protected void Application_Start()
    {
      Microsoft.ApplicationInsights.Extensibility.
        TelemetryConfiguration.Active.InstrumentationKey =
          // - for example -
          WebConfigurationManager.Settings["ikey"];
      //...
```

Se você quiser apenas toosend um conjunto específico de recursos diferente de tooa de eventos, você pode definir a chave de saudação para um TelemetryClient específico:

```C#

    var tc = new TelemetryClient();
    tc.Context.InstrumentationKey = "----- my key ----";
    tc.TrackEvent("myEvent");
    // ...

```

uma nova chave de tooget [criar um novo recurso no portal do Application Insights Olá][new].

## <a name="next-steps"></a>Próximas etapas
[Saiba mais sobre Olá API][api].

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[client]: app-insights-javascript.md
[diagnostic]: app-insights-diagnostic-search.md
[exceptions]: app-insights-asp-net-exceptions.md
[netlogs]: app-insights-asp-net-trace-logs.md
[new]: app-insights-create-new-resource.md
[redfield]: app-insights-monitor-performance-live-website-now.md
[start]: app-insights-overview.md
