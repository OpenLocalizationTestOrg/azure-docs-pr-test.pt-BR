---
title: contadores de aaaPerformance no Application Insights | Microsoft Docs
description: Monitore o sistema e contadores de desempenho .NET personalizados no Application Insights.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 5b816f4c-a77a-4674-ae36-802ee3a2f56d
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/11/2016
ms.author: bwren
ms.openlocfilehash: 0a51c225f1d1124c9e7fe89f34e747cb26a3589e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="system-performance-counters-in-application-insights"></a>Contadores de desempenho do sistema no Application Insights
O Windows fornece uma ampla variedade de [contadores de desempenho](http://www.codeproject.com/Articles/8590/An-Introduction-To-Performance-Counters) como ocupação da CPU, memória, disco e uso da rede. Você também pode definir seus próprios. [Application Insights](app-insights-overview.md) pode mostrar esses contadores de desempenho se seu aplicativo estiver em execução no IIS em um toowhich de host ou máquina virtual local têm acesso administrativo. gráficos de saudação indicam aplicativos em tempo real do hello recursos tooyour disponíveis e podem ajudar a tooidentify sem balanceamento de carga entre instâncias do servidor.

Contadores de desempenho aparecem na folha de servidores de saudação, que inclui uma tabela que segmentos por instância de servidor.

![Contadores de desempenho reportados no Application Insights](./media/app-insights-performance-counters/counters-by-server-instance.png)

(Os contadores de desempenho não estão disponíveis para aplicativos Web do Azure. Mas você pode [enviar o diagnóstico do Azure tooApplication Insights](app-insights-azure-diagnostics.md).)

## <a name="view-counters"></a>Visualizar contadores
folha de servidores Olá mostra um conjunto padrão de contadores de desempenho. 

toosee outros contadores, em editar gráficos Olá na folha de servidores hello, ou abra uma nova [Metrics Explorer](app-insights-metrics-explorer.md) folha e adicionar novos gráficos. 

contadores disponíveis Olá são listados como métricas de quando você edita um gráfico.

![Contadores de desempenho reportados no Application Insights](./media/app-insights-performance-counters/choose-performance-counters.png)

toosee todos os gráficos mais úteis em um único local, crie um [painel](app-insights-dashboards.md) e fixá-los tooit.

## <a name="add-counters"></a>Adicionar contadores
Se o contador de desempenho de saudação desejado não é mostrado na lista de saudação de métricas, é porque Olá SDK do Application Insights não coletá-lo no seu servidor web. Você pode configurá-lo toodo assim.

1. Descubra quais contadores estão disponíveis no seu servidor usando esse comando do PowerShell no servidor de saudação:
   
    `Get-Counter -ListSet *`
   
    (Consulte [`Get-Counter`](https://technet.microsoft.com/library/hh849685.aspx).)
2. Abra o ApplicationInsights.config.
   
   * Se você adicionou o Application Insights tooyour aplicativo durante o desenvolvimento, edite o applicationinsights. config em seu projeto e, em seguida, implantá-lo novamente tooyour servidores.
   * Se você usou o Monitor de Status tooinstrument um aplicativo web em tempo de execução, encontre o applicationinsights. config no diretório raiz de saudação do aplicativo hello no IIS. Atualize-o em cada instância de servidor.
3. Edite diretiva de coletor de desempenho hello:
   
```XML
   
    <Add Type="Microsoft.ApplicationInsights.Extensibility.PerfCounterCollector.PerformanceCollectorModule, Microsoft.AI.PerfCounterCollector">
      <Counters>
        <Add PerformanceCounter="\Objects\Processes"/>
        <Add PerformanceCounter="\Sales(photo)\# Items Sold" ReportAs="Photo sales"/>
      </Counters>
    </Add>

```

Você pode capturar os contadores padrão e aqueles implementados por conta própria. `\Objects\Processes` é um exemplo de um contador padrão, disponível em todos os sistemas Windows. `\Sales(photo)\# Items Sold` é um exemplo de um contador personalizado que pode ser implementado em um serviço Web. 

formato de saudação é `\Category(instance)\Counter"`, ou por categorias que não têm instâncias, apenas `\Category\Counter`.

`ReportAs`é necessário para os nomes de contadores que não correspondem a `[a-zA-Z()/-_ \.]+` -ou seja, eles contêm caracteres que não estão em Olá conjuntos a seguir: letras, round colchetes, barra invertida, hífen, sublinhado, espaço, ponto.

Se você especificar uma instância, ele será coletado como uma dimensão "CounterInstanceName" de saudação relatado métrica.

### <a name="collecting-performance-counters-in-code"></a>Coletando contadores de desempenho no código
contadores de desempenho do sistema toocollect e enviá-los tooApplication Insights, você pode adaptar trechos de saudação abaixo:


``` C#

    var perfCollectorModule = new PerformanceCollectorModule();
    perfCollectorModule.Counters.Add(new PerformanceCounterCollectionRequest(
      @"\.NET CLR Memory([replace-with-application-process-name])\# GC Handles", "GC Handles")));
    perfCollectorModule.Initialize(TelemetryConfiguration.Active);
```

Ou você pode fazer Olá com métricas personalizadas que você criou a mesma coisa:

``` C#
    var perfCollectorModule = new PerformanceCollectorModule();
    perfCollectorModule.Counters.Add(new PerformanceCounterCollectionRequest(
      @"\Sales(photo)\# Items Sold", "Photo sales"));
    perfCollectorModule.Initialize(TelemetryConfiguration.Active);
```

## <a name="performance-counters-in-analytics"></a>Contadores de desempenho no Analytics
Você pode pesquisar e exibir relatórios do contador de desempenho no [Analytics](app-insights-analytics.md).

Olá **performanceCounters** esquema expõe Olá `category`, `counter` nome, e `instance` nome de contador de desempenho.  Telemetria Olá para cada aplicativo, você verá apenas os contadores Olá para o aplicativo. Por exemplo, toosee quais contadores estão disponíveis: 

![Contadores de desempenho na análise do Application Insights](./media/app-insights-performance-counters/analytics-performance-counters.png)

(Aqui 'Instance' se refere a instância do contador de desempenho toohello, Olá não funções ou servidores de instância de máquina. nome de instância do contador de desempenho Olá segmentos normalmente contadores, como tempo de processador por nome de saudação do aplicativo ou processo hello.)

tooget um gráfico de memória disponível em Olá período recente: 

![Gráfico de tempo da memória na análise do Application Insights](./media/app-insights-performance-counters/analytics-available-memory.png)

Como outros telemetria **performanceCounters** também tem uma coluna `cloud_RoleInstance` que indica a identidade Olá Olá host da instância do servidor no qual o aplicativo está em execução. Por exemplo, toocompare Olá desempenho do aplicativo em máquinas diferentes hello: 

![Desempenho segmentado por instância de função na análise do Application Insights](./media/app-insights-performance-counters/analytics-metrics-role-instance.png)

## <a name="aspnet-and-application-insights-counts"></a>Contadores do ASP.NET e do Application Insights
*Qual é a diferença de saudação entre métricas de exceções e taxa de exceções Olá?*

* *Taxa de exceções* é um contador de desempenho do sistema. Olá CLR conta todos os Olá tratados e exceções sem tratamento que são geradas e divide o total de saudação em um intervalo de amostragem por comprimento de saudação do intervalo de saudação. Olá SDK do Application Insights coleta esse resultado e o envia toohello portal.
* *Exceções* é uma contagem de saudação TrackException relatórios recebidos pelo portal Olá no intervalo de amostragem de saudação do gráfico de saudação. Ele inclui somente Olá tratados exceções em que você tenha escrito TrackException chama em seu código e não inclui todos os [exceções sem tratamento](app-insights-asp-net-exceptions.md). 

## <a name="alerts"></a>Alertas
Como outras métricas, você pode [definir um alerta](app-insights-alerts.md) toowarn se um contador de desempenho ficar fora de um limite especificado. Abra a folha de alertas de saudação e clique em Adicionar alertas.

## <a name="next"></a>Próximas etapas
* [Acompanhamento de dependência](app-insights-asp-net-dependencies.md)
* [Acompanhamento de exceções](app-insights-asp-net-exceptions.md)

