---
title: os logs de rastreamento de .NET aaaExplore no Application Insights
description: Pesquise logs gerados com Trace, NLog ou Log4Net.
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 0c2a084f-6e71-467b-a6aa-4ab222f17153
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/3/2017
ms.author: bwren
ms.openlocfilehash: 6bfcd9e5751c3656236d7eb2fc09321740171a70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="explore-net-trace-logs-in-application-insights"></a>Explorar os logs de rastreamento do .NET no Application Insights
Se você usar NLog, log4Net ou Trace para rastreamento de diagnóstico em seu aplicativo ASP.NET, você pode ter seus logs enviados muito[Azure Application Insights][start], onde você pode explorar e pesquisar -los. Os logs serão mesclados com outros Olá telemetria provenientes de seu aplicativo, para que você possa identificar Olá rastreamentos associados com cada solicitação de usuário de serviço e correlacioná-los com outros eventos e relatórios de exceção.

> [!NOTE]
> Você precisa de módulo de captura de log Olá? É um adaptador útil para agentes de terceiros, mas se você ainda não usa o NLog, log4Net ou System.Diagnostics.Trace, convém chamar apenas o [TrackTrace() do Application Insights](app-insights-api-custom-events-metrics.md#tracktrace) diretamente.
>
>

## <a name="install-logging-on-your-app"></a>Instalar o log no seu aplicativo
Instale a estrutura de registros escolhida no seu projeto. Isso deve resultar em uma entrada no app.config ou web.config.

Se você estiver usando o Trace, você precisa tooadd um tooweb.config de entrada:

```XML

    <configuration>
     <system.diagnostics>
       <trace autoflush="false" indentsize="4">
         <listeners>
           <add name="myListener"
             type="System.Diagnostics.TextWriterTraceListener"
             initializeData="TextWriterOutput.log" />
           <remove name="Default" />
         </listeners>
       </trace>
     </system.diagnostics>
   </configuration>
```
## <a name="configure-application-insights-toocollect-logs"></a>Configurar logs de toocollect Application Insights
**[Adicionar projeto do Application Insights tooyour](app-insights-asp-net.md)**  se você ainda não tiver feito isso. Você verá um coletor de log opção tooinclude hello.

Ou então **Configure o Application Insights** clicando com o botão direito no seu projeto no Gerenciador de Soluções. Selecione a opção de saudação muito**configurar coleta de rastreamento**.

*Não consegue ver o menu do Application Insights nem a opção de coletor de logs?* Experimente [Solucionar problemas](#troubleshooting).

## <a name="manual-installation"></a>Instalação manual
Use este método se o tipo de projeto não é suportado pelo instalador do Application Insights hello (por exemplo um área de trabalho projeto do Windows).

1. Se você planejar toouse log4Net ou NLog, instalá-lo em seu projeto.
2. No Gerenciador de Soluções, clique com o botão direito do mouse no seu projeto e escolha **Gerenciar Pacotes NuGet**.
3. Pesquise “Application Insights”
4. Selecione o pacote apropriado Olá - um de:

   * Microsoft.ApplicationInsights.TraceListener (toocapture Trace chamadas)
   * Microsoft.ApplicationInsights.EventSourceListener (toocapture EventSource eventos)
   * Microsoft.ApplicationInsights.EtwListener (eventos ETW toocapture)
   * Microsoft.ApplicationInsights.NLogTarget
   * Microsoft.ApplicationInsights.Log4NetAppender

pacote do NuGet Olá instala os assemblies necessários hello e modifica Web. config ou App. config.

## <a name="insert-diagnostic-log-calls"></a>Inserir chamadas de log de diagnóstico
Se você usa System.Diagnostics.Trace, uma chamada típica é semelhante a:

    System.Diagnostics.Trace.TraceWarning("Slow response - database01");

Se você preferir log4net ou NLog:

    logger.Warn("Slow response - database01");

## <a name="using-eventsource-events"></a>Usando eventos EventSource
Você pode configurar [Tracing](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx) eventos toobe enviado tooApplication Insights como rastreamentos. Primeiro, instale Olá `Microsoft.ApplicationInsights.EventSourceListener` pacote NuGet. Edite `TelemetryModules` seção Olá [Applicationinsights](app-insights-configuration-with-applicationinsights-config.md) arquivo.

```xml
    <Add Type="Microsoft.ApplicationInsights.EventSourceListener.EventSourceTelemetryModule, Microsoft.ApplicationInsights.EventSourceListener">
      <Sources>
        <Add Name="MyCompany" Level="Verbose" />
      </Sources>
    </Add>
```

Para cada fonte, você pode definir Olá parâmetros a seguir:
 * `Name`Especifica o nome de saudação do hello EventSource toocollect.
 * `Level`Especifica a saudação toocollect nível de log. Pode ser `Critical`, `Error`, `Informational`, `LogAlways`, `Verbose` ou `Warning`.
 * `Keywords`(Opcional) Especifica o valor de inteiro de saudação do toouse de combinações de palavras-chave.

## <a name="using-diagnosticsource-events"></a>Usando eventos DiagnosticSource
Você pode configurar [System.Diagnostics.DiagnosticSource](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/DiagnosticSourceUsersGuide.md) eventos toobe enviado tooApplication Insights como rastreamentos. Primeiro, instale Olá [ `Microsoft.ApplicationInsights.DiagnosticSourceListener` ](https://www.nuget.org/packages/Microsoft.ApplicationInsights.DiagnosticSourceListener) pacote NuGet. Edite Olá `TelemetryModules` seção Olá [Applicationinsights](app-insights-configuration-with-applicationinsights-config.md) arquivo.

```xml
    <Add Type="Microsoft.ApplicationInsights.DiagnsoticSourceListener.DiagnosticSourceTelemetryModule, Microsoft.ApplicationInsights.DiagnosticSourceListener">
      <Sources>
        <Add Name="MyDiagnosticSourceName" />
      </Sources>
    </Add>
```

Para cada DiagnosticSource você deseja tootrace, adicione uma entrada com hello `Name` toohello nome do seu DiagnosticSource do conjunto de atributo.

## <a name="using-etw-events"></a>Usando eventos ETW
Você pode configurar toobe de eventos ETW enviado tooApplication Insights como rastreamentos. Primeiro, instale Olá `Microsoft.ApplicationInsights.EtwCollector` pacote NuGet. Edite `TelemetryModules` seção Olá [Applicationinsights](app-insights-configuration-with-applicationinsights-config.md) arquivo.

> [!NOTE] 
> Eventos ETW só podem ser obtidos se Olá Olá de hospedagem de processo SDK está sendo executado sob uma identidade que é um membro de administradores ou "usuários de Log de desempenho".

```xml
    <Add Type="Microsoft.ApplicationInsights.EtwCollector.EtwCollectorTelemetryModule, Microsoft.ApplicationInsights.EtwCollector">
      <Sources>
        <Add ProviderName="MyCompanyEventSourceName" Level="Verbose" />
      </Sources>
    </Add>
```

Para cada fonte, você pode definir Olá parâmetros a seguir:
 * `ProviderName`é o nome de saudação do hello toocollect de provedor ETW.
 * `ProviderGuid`Especifica a saudação GUID da saudação toocollect de provedor ETW, pode ser usado em vez de `ProviderName`.
 * `Level`Define Olá toocollect nível de log. Pode ser `Critical`, `Error`, `Informational`, `LogAlways`, `Verbose` ou `Warning`.
 * `Keywords`(Opcional) define Olá valor inteiro toouse de combinações de palavra-chave.

## <a name="using-hello-trace-api-directly"></a>Usando Olá rastreamento API diretamente
Você pode chamar hello Application Insights rastreamento API diretamente. adaptadores de registro em log Olá usam essa API.

Por exemplo:

    var telemetry = new Microsoft.ApplicationInsights.TelemetryClient();
    telemetry.TrackTrace("Slow response - database01");

Uma vantagem de TrackTrace é que você pode colocar dados relativamente longos na mensagem de saudação. Por exemplo, você pode codificar dados POST.

Além disso, você pode adicionar uma mensagem de tooyour nível de severidade. E, como outros telemetria, você pode adicionar valores de propriedade que você pode usar o filtro de toohelp ou pesquisa para diferentes conjuntos de rastreamentos. Por exemplo:

    var telemetry = new Microsoft.ApplicationInsights.TelemetryClient();
    telemetry.TrackTrace("Slow database response",
                   SeverityLevel.Warning,
                   new Dictionary<string,string> { {"database", db.ID} });

Isso permitiria que você, em [pesquisa][diagnostic], tooeasily filtrar todas as mensagens de saudação de um nível de severidade específico relacionado tooa determinado banco de dados.

## <a name="explore-your-logs"></a>Explorar seus logs
Execute o aplicativo no modo de depuração ou implante-o dinamicamente.

Na folha de visão geral do aplicativo em [portal do Application Insights Olá][portal], escolha [pesquisa][diagnostic].

![No Application Insights, escolha Pesquisar](./media/app-insights-asp-net-trace-logs/020-diagnostic-search.png)

![Pesquisa](./media/app-insights-asp-net-trace-logs/10-diagnostics.png)

Por exemplo, você pode:

* Filtrar rastreamentos de log ou itens com propriedades específicas
* Inspecionar um item específico em detalhes.
* Localizar outros telemetria relacionados toohello mesma solicitação de usuário (ou seja, com hello mesmo OperationId)
* Salvar configuração de saudação desta página como um favorito

> [!NOTE]
> **Amostragem.** Se seu aplicativo envia um lote de dados e você estiver usando Olá SDK do Application Insights para ASP.NET versão 2.0.0-beta3 ou posterior, o recurso de amostragem adaptável de saudação pode operar e enviar apenas uma porcentagem da sua telemetria. [Saiba mais sobre amostragem.](app-insights-sampling.md)
>
>

## <a name="next-steps"></a>Próximas etapas
[Diagnosticar falhas e exceções no ASP.NET][exceptions]

[Saiba mais sobre o Search][diagnostic].

## <a name="troubleshooting"></a>Solucionar problemas
### <a name="how-do-i-do-this-for-java"></a>Como faço isso no Java?
Saudação de uso [adaptadores do log de Java](app-insights-java-trace-logs.md).

### <a name="theres-no-application-insights-option-on-hello-project-context-menu"></a>Não há nenhuma opção Application Insights no menu de contexto do projeto de saudação
* Verifique se as ferramentas do Application Insights estão instaladas neste computador de desenvolvimento. No menu Ferramentas do Visual Studio, em Extensões e Atualizações, procure pelas Ferramentas do Application Insights. Se não estiver na guia do hello instalado, abra Olá Online guia e instalá-lo.
* Este pode ser um tipo de projeto sem suporte pelas ferramentas do Application Insights. Use a [instalação manual](#manual-installation).

### <a name="no-log-adapter-option-in-hello-configuration-tool"></a>Nenhuma opção de adaptador de log na ferramenta de configuração de saudação
* Você precisa de estrutura de tooinstall Olá log primeiro.
* Se estiver usando System.Diagnostics.Trace, verifique se você o [configurou no `web.config`](https://msdn.microsoft.com/library/system.diagnostics.eventlogtracelistener.aspx).
* Você tem a versão mais recente de saudação do Application Insights? No Visual Studio **ferramentas** menu, escolha **extensões e atualizações**e abra hello **atualizações** guia. Se as ferramentas de análise do desenvolvedor está lá, clique em tooupdate-lo.

### <a name="emptykey"></a>Recebo um erro "Chave de instrumentação não pode ser vazio"
Parece que você instalou Olá log de pacote de Nuget de adaptador sem instalar o Application Insights.

No Gerenciador de Soluções, clique com o botão direito do mouse em `ApplicationInsights.config` e escolha **Atualizar o Application Insights**. Você obterá uma caixa de diálogo que solicita a você toosign no tooAzure e crie um recurso do Application Insights, ou use novamente um existente. Isso deve corrigir o erro.

### <a name="i-can-see-traces-in-diagnostic-search-but-not-hello-other-events"></a>Eu podem ver rastreamentos em busca de diagnóstico, mas não Olá outros eventos
Às vezes, pode levar algum tempo para que todos os tooget de eventos e solicitações de saudação por meio do pipeline de saudação.

### <a name="limits"></a>Que quantidade de dados é mantida?
Vários fatores afetam a quantidade de saudação de dados retidos. Consulte Olá [limites](app-insights-api-custom-events-metrics.md#limits) seção da página de métricas de evento Olá cliente para obter mais informações. 

### <a name="im-not-seeing-some-of-hello-log-entries-that-i-expect"></a>Não ver algumas das entradas de log Olá esperados
Se seu aplicativo envia um lote de dados e você estiver usando Olá SDK do Application Insights para ASP.NET versão 2.0.0-beta3 ou posterior, o recurso de amostragem adaptável de saudação pode operar e enviar apenas uma porcentagem da sua telemetria. [Saiba mais sobre amostragem.](app-insights-sampling.md)

## <a name="add"></a>Próximas etapas
* [Configurar testes de disponibilidade e capacidade de resposta][availability]
* [Solução de problemas][qna]

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[exceptions]: app-insights-asp-net-exceptions.md
[portal]: https://portal.azure.com/
[qna]: app-insights-troubleshoot-faq.md
[start]: app-insights-overview.md
