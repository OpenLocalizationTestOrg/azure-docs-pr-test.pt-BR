---
title: "aaaAzure correlação de telemetria do Application Insights | Microsoft Docs"
description: "Correlação no Application Insights Telemetry"
services: application-insights
documentationcenter: .net
author: SergeyKanzhelev
manager: carmonm
ms.service: application-insights
ms.workload: TBD
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 04/25/2017
ms.author: bwren
ms.openlocfilehash: 3ed8c589d237cac5daceac939ca893b7d81a2967
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="telemetry-correlation-in-application-insights"></a>Correlação de telemetria no Application Insights

Olá, mundo de serviços micro, cada operação lógica requer o trabalho feito em vários componentes do serviço de saudação. Cada um desses componentes pode ser monitorado separadamente pelo [Application Insights](app-insights-overview.md). componente de aplicativo web Hello se comunica com as credenciais do usuário toovalidate de componente de provedor de autenticação e dados de tooget de componente de API de saudação para visualização. componente de API de saudação em sua vez pode consultar dados de outros serviços e usar componentes de provedor de cache e notificar o componente de cobrança Olá sobre esta chamada. O Application Insights dá suporte à correlação de telemetria distribuída. Ele permite que você toodetect qual componente é responsável por falhas ou degradação de desempenho.

Este artigo explica o modelo de dados de saudação usado pelo telemetria do Application Insights toocorrelate enviados por vários componentes. Ele abrange protocolos e técnicas de propagação do contexto de saudação. Ele também aborda a implementação de saudação dos conceitos de correlação Olá nas plataformas e idiomas diferentes.

## <a name="telemetry-correlation-data-model"></a>Modelo de dados de correlação de telemetria

O Application Insights define um [modelo de dados](application-insights-data-model.md) para correlação de telemetria distribuída. Telemetria tooassociate com operação lógica hello, todos os itens de telemetria tem um campo de contexto chamado `operation_Id`. Esse identificador é compartilhado por todos os itens de telemetria em rastreamento Olá distribuída. Portanto, mesmo com a perda de telemetria de uma única camada, você ainda pode associar telemetria relatada por outros componentes.

Operação lógica distribuída normalmente é constituído de um conjunto de operações menores - solicitações processadas por um dos componentes de saudação. Essas operações são definidas por [telemetria de solicitação](application-insights-data-model-request-telemetry.md). Toda telemetria de solicitação tem seu próprio `id` que a identifica de modo exclusivo, globalmente. E toda a telemetria - rastreamentos, exceções, etc., associado a esta solicitação deve definir Olá `operation_parentId` toohello o valor da solicitação Olá `id`.

Cada operação de saída como componente de tooanother chamada http representado por [telemetria de dependência](application-insights-data-model-dependency-telemetry.md). A telemetria de dependência também define sua própria `id`, que é globalmente exclusiva. A telemetria de solicitação, iniciada por essa chamada de dependência, usa-a como `operation_parentId`.

Você pode criar modo de exibição de saudação de operação lógica distribuída usando `operation_Id`, `operation_parentId`, e `request.id` com `dependency.id`. Esses campos também definem a ordem de causalidade de saudação das chamadas de telemetria.

No ambiente de serviços micro rastreamentos de componentes podem ir armazenamentos diferentes toohello. Todo componente pode ter sua própria chave de instrumentação no Application Insights. tooget a telemetria para operação lógica hello, você precisa tooquery dados de cada armazenamento. Quando o número de armazenamento for grande, você precisa toohave uma dica sobre onde toolook Avançar.

Application Insights modelo de dados define dois campos toosolve esse problema: `request.source` e `dependency.target`. primeiro campo de saudação identifica o componente de saudação que iniciou a solicitação de dependência hello e Olá segundo identifica qual componente retornada uma resposta de chamada de dependência Olá Olá.


## <a name="example"></a>Exemplo

Vejamos um exemplo de preços de estoque de um aplicativo mostrando Olá preço de mercado atual de uma ação usando a API externa hello, chamada de API de ações. Olá aplicativo preços de estoque tem uma página `Stock page` aberto por meio do navegador da web do hello cliente `GET /Home/Stock`. consultas de aplicativo Olá Olá estoque API usando uma chamada HTTP `GET /api/stock/value`.

Você pode analisar telemetria resultante da execução de uma consulta:

```
(requests | union dependencies | union pageViews) 
| where operation_Id == "STYz"
| project timestamp, itemType, name, id, operation_ParentId, operation_Id
```

Na nota da exibição resultados Olá todos os itens de telemetria compartilham raiz Olá `operation_Id`. Quando chama ajax feitas na página Olá - nova id exclusiva de `qJSXU` é atribuído toohello telemetria de dependência e id da página é usada como `operation_ParentId`. A solicitação do servidor, por sua vez, usa a ID do AJAX como `operation_ParentId`, etc.

| itemType   | name                      | ID           | operation_ParentId | operation_Id |
|------------|---------------------------|--------------|--------------------|--------------|
| pageView   | Página de ações                |              | STYz               | STYz         |
| dependência | GET /Home/Stock           | qJSXU        | STYz               | STYz         |
| solicitação    | GET Home/Stock            | KqKwlrSt9PA= | qJSXU              | STYz         |
| dependência | GET /api/stock/value      | bBrf2L7mm2g= | KqKwlrSt9PA=       | STYz         |

Agora quando Olá chamada `GET /api/stock/value` feitas serviço externo tooan deseja tooknow identidade de saudação do servidor. Assim, você pode definir o campo `dependency.target` adequadamente. Quando o serviço externo Olá não suporta o monitoramento - `target` é definido toohello o nome do host do serviço, Olá como `stock-prices-api.com`. No entanto se esse serviço identifica-se ao retornar um cabeçalho HTTP - `target` contém Olá identidade de serviço que permite que o rastreamento de toobuild distribuído do Application Insights consultando telemetria desse serviço. 

## <a name="correlation-headers"></a>Cabeçalhos de correlação

Estamos trabalhando na proposta de RFC para Olá [correlação protocolo HTTP](https://github.com/lmolkova/correlation/blob/master/http_protocol_proposal_v1.md). Essa proposta define dois cabeçalhos:

- `Request-Id`executar o id exclusivo global de saudação da chamada de saudação
- `Correlation-Context`-realizar a coleção de pares de valor Olá nome das propriedades de rastreamento Olá distribuído

saudação padrão também define dois esquemas de `Request-Id` geração - simples e hierárquica. Com o esquema simples de Olá, há um conhecido `Id` chave definida para Olá `Correlation-Context` coleção.

Application Insights define Olá [extensão](https://github.com/lmolkova/correlation/blob/master/http_protocol_proposal_v2.md) para correlação Olá protocolo HTTP. Ele usa `Request-Context` nome pares de valor toopropagate coleção de saudação de propriedades usadas pelo chamador imediato saudação ou receptor. SDK do Application Insights usa esse cabeçalho tooset `dependency.target` e `request.source` campos.

## <a name="open-tracing-and-application-insights"></a>Rastreamento aberto e Application Insights

Aparência dos modelos de dados de [Rastreamento Aberto](http://opentracing.io/) e do Application Insights 

- `request`, `pageView` mapeia muito**alcance** com`span.kind = server`
- `dependency`mapeia muito**alcance** com`span.kind = client`
- `id`de um `request` e `dependency` mapeia muito**Span.Id**
- `operation_Id`mapeia muito**TraceId**
- `operation_ParentId`mapeia muito**referência** do tipo`ChileOf`

Consulte [modelo de dados](application-insights-data-model.md) para modelo de dados e tipos do Application Insights.

Consulte [especificação](https://github.com/opentracing/specification/blob/master/specification.md) e [semantic_conventions](https://github.com/opentracing/specification/blob/master/semantic_conventions.md) para obter definições dos conceitos de rastreamento aberto.


## <a name="telemetry-correlation-in-net"></a>Correlação de telemetria em .NET

Ao longo do tempo .NET definido pelo número de maneiras toocorrelate telemetria e diagnóstico logs. Não há `System.Diagnostics.CorrelationManager` permitindo tootrack [LogicalOperationStack e ActivityId](https://msdn.microsoft.com/library/system.diagnostics.correlationmanager.aspx). `System.Diagnostics.Tracing.EventSource`e Windows ETW definir método hello [SetCurrentThreadActivityId](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.setcurrentthreadactivityid.aspx). `ILogger` usa [Escopos de log](https://docs.microsoft.com/aspnet/core/fundamentals/logging#log-scopes). WCF e HTTP conectam a propagação de contexto "atual".

No entanto, esses métodos não habilitam o suporte a rastreamento distribuído automático. `DiagnosticsSource`é um toosupport de maneira automática entre correlação de máquina. Bibliotecas .NET oferecem suporte a origem de diagnóstico e permitem a propagação automática de máquina cruzada do contexto de correlação Olá por meio do transporte hello como http.

Olá [guia tooActivities](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/ActivityUserGuide.md) na fonte de diagnóstico explica conceitos básicos de saudação do rastreamento de atividades. 

Núcleo do ASP.NET 2.0 dá suporte à extração de cabeçalhos Http e iniciando Olá nova atividade. 

`System.Net.HttpClient`versão inicial `<fill in>` dá suporte à inclusão automática de correlação Olá cabeçalhos Http e Olá chamada de http como uma atividade de controle.

Há um novo módulo Http [Microsoft.AspNet.TelemetryCorrelation](https://www.nuget.org/packages/Microsoft.AspNet.TelemetryCorrelation/) para Olá ASP.NET clássico. Este módulo implementa a correlação de telemetria usando DiagnosticsSource. Ele inicia a atividade com base nos cabeçalhos de solicitação de entrada. Ele também correlaciona telemetria dos diferentes estágios de saudação do processamento da solicitação. Mesmo em casos de saudação quando todos os estágios do processamento do IIS é executado em um threads gerenciar diferentes.

Versão inicial do Application Insights SDK `2.4.0-beta1` usa a telemetria toocollect DiagnosticsSource e a atividade e associá-lo a atividade atual de saudação. 

## <a name="next-steps"></a>Próximas etapas

- [Escrever telemetria personalizada](app-insights-api-custom-events-metrics.md)
- Integrar todos os componentes do seu microsserviço no Application Insights. Confira as [plataformas com suporte](app-insights-platforms.md).
- Consulte [modelo de dados](application-insights-data-model.md) para modelo de dados e tipos do Application Insights.
- Saiba como muito[estender e filtrar telemetria](app-insights-api-filtering-sampling.md).
