---
title: "aaaSearch análise de tráfego de pesquisa do Azure | Microsoft Docs"
description: "Habilite a análise de tráfego de pesquisa para pesquisa do Azure, um serviço de pesquisa de nuvem hospedado no Microsoft Azure, toounlock insights sobre seus usuários e seus dados."
services: search
documentationcenter: 
author: bernitorres
manager: jlembicz
editor: 
ms.assetid: b31d79cf-5924-4522-9276-a1bb5d527b13
ms.service: search
ms.devlang: multiple
ms.workload: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 04/05/2017
ms.author: betorres
ms.openlocfilehash: 1d16aa63d05c1c3df1bbfbb4f09ac77705ed9d9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-search-traffic-analytics"></a>O que é análise de tráfego de pesquisa
Análise de tráfego de pesquisa é um padrão de implementação de um loop de comentários para seu serviço de pesquisa. Esse padrão descreve os dados necessários hello e como toocollect-lo usando o Application Insights, líder de mercado para monitorar serviços em várias plataformas.

A análise de tráfego de pesquisa permite que você ganhe visibilidade em seu serviço de pesquisa e tenha ideias sobre os usuários e seus comportamentos. Por meio de dados sobre o que seus usuários escolhem, é possível toomake decisões que melhoram a experiência de pesquisa e tooback off quando os resultados de saudação não são o que esperava.

A pesquisa do Azure oferece uma solução de telemetria que integra o Power BI e o Azure Application Insights tooprovide detalhada monitoramento e controle. Como a interação com a pesquisa do Azure é por meio de APIs, telemetria Olá deve ser implementada por desenvolvedores hello usando a pesquisa, seguindo as instruções de saudação nesta página.

## <a name="identify-hello-relevant-search-data"></a>Identificar dados de pesquisa relevantes Olá

métricas de pesquisa úteis do toohave, é necessário toolog alguns sinais de usuários Olá Olá do aplicativo de pesquisa. Estes sinais significam conteúdo que os usuários estão interessados em e que eles considerem precisa tootheir relevante.

Há dois sinais necessários para a Análise do Tráfego de Pesquisa:

1. Eventos de pesquisa gerados pelo usuário: somente as consultas de pesquisa iniciadas por um usuário são interessantes. Pesquisar solicitações usadas toopopulate facetas, o conteúdo adicional ou qualquer informação interna, não são importantes e afetar e influenciar os resultados.

2. Eventos de clique gerado pelo usuário: por cliques neste documento, nos referimos tooa usuário selecionar um resultado de pesquisa específica retornado de uma consulta de pesquisa. Um clique geralmente significa que um documento é um resultado relevante para uma consulta de pesquisa específica.

Vinculando a pesquisa e clique em eventos com uma id de correlação, é possível tooanalyze comportamentos de saudação de usuários em seu aplicativo. Essas informações de pesquisa são tooobtain impossível com apenas os logs de tráfego de pesquisa.

## <a name="how-tooimplement-search-traffic-analytics"></a>Como tooimplement a pesquisa de análise de tráfego

Olá sinais mencionado Olá anterior seção deve ser obtida do aplicativo de pesquisa hello como Olá usuário interagisse com ele. O Application Insights é uma solução monitoramento extensível, disponível para várias plataformas e com opções flexíveis de instrumentação. Uso do Application Insights permite aproveitar os relatórios de pesquisa do Power BI Olá criado pela análise de saudação toomake pesquisa do Azure de dados.

Em Olá [portal](https://portal.azure.com) página para seu serviço de pesquisa do Azure, folha de análise de tráfego de pesquisa Olá contém um roteiro para esse padrão de telemetria. Também pode selecionar ou criar um recurso do Application Insights e ver os dados necessários hello, em um só lugar.

![Instruções da Análise do Tráfego de Pesquisa][1]

### <a name="1-select-an-application-insights-resource"></a>1. Selecione um recurso do Application Insights

Você precisa tooselect um toouse de recurso do Application Insights ou cria um se você não tiver uma. Você pode usar um recurso que já tem em uso toolog Olá necessário eventos personalizados.

Ao criar um novo recurso do Application Insights, todos os tipos de aplicativo são válidos para esse cenário. Selecione Olá um que melhor se adapta plataforma Olá que você está usando.

Você precisa chave de instrumentação Olá para criar o cliente de telemetria Olá para seu aplicativo. Você pode obtê-lo do painel do portal do Application Insights hello, ou você poderá obtê-lo na página de análise de tráfego de pesquisa hello, selecionando Olá instância toouse.

### <a name="2-instrument-your-application"></a>2. Instrumentar seu aplicativo

Essa fase é onde você instrumentar seu próprio aplicativo de pesquisa, usando o recurso do Application Insights Olá seu Olá criado na etapa acima. Há quatro etapas toothis processo:

**I. Criar um cliente de telemetria** é objeto Olá que envia eventos toohello recurso do Application Insights.

*C#*

    private TelemetryClient telemetryClient = new TelemetryClient();
    telemetryClient.InstrumentationKey = "<YOUR INSTRUMENTATION KEY>";

*JavaScript*

    <script type="text/javascript">var appInsights=window.appInsights||function(config){function r(config){t[config]=function(){var i=arguments;t.queue.push(function(){t[config].apply(t,i)})}}var t={config:config},u=document,e=window,o="script",s=u.createElement(o),i,f;s.src=config.url||"//az416426.vo.msecnd.net/scripts/a/ai.0.js";u.getElementsByTagName(o)[0].parentNode.appendChild(s);try{t.cookie=u.cookie}catch(h){}for(t.queue=[],i=["Event","Exception","Metric","PageView","Trace","Dependency"];i.length;)r("track"+i.pop());return r("setAuthenticatedUserContext"),r("clearAuthenticatedUserContext"),config.disableExceptionTracking||(i="onerror",r("_"+i),f=e[i],e[i]=function(config,r,u,e,o){var s=f&&f(config,r,u,e,o);return s!==!0&&t["_"+i](config,r,u,e,o),s}),t}
    ({
    instrumentationKey: "<YOUR INSTRUMENTATION KEY>"
    });
    window.appInsights=appInsights;
    </script>

Para outros idiomas e plataformas, consulte Olá completa [lista](https://docs.microsoft.com/azure/application-insights/app-insights-platforms).

**II. Uma ID de pesquisa para correlação da solicitação** toocorrelate pesquisa solicitações com cliques, é necessário toohave uma id de correlação que relaciona esses dois eventos. O Azure Search fornece uma ID de Pesquisa quando você a solicita com um cabeçalho:

*C#*

    // This sample uses hello Azure Search .NET SDK https://www.nuget.org/packages/Microsoft.Azure.Search

    var client = new SearchIndexClient(<ServiceName>, <IndexName>, new SearchCredentials(<QueryKey>)
    var headers = new Dictionary<string, List<string>>() { { "x-ms-azs-return-searchid", new List<string>() { "true" } } };
    var response = await client.Documents.SearchWithHttpMessagesAsync(searchText: searchText, searchParameters: parameters, customHeaders: headers);
    IEnumerable<string> headerValues;
    string searchId = string.Empty;
    if (response.Response.Headers.TryGetValues("x-ms-azs-searchid", out headerValues)){
     searchId = headerValues.FirstOrDefault();
    }

*JavaScript*

    request.setRequestHeader("x-ms-azs-return-searchid", "true");
    request.setRequestHeader("Access-Control-Expose-Headers", "x-ms-azs-searchid");
    var searchId = request.getResponseHeader('x-ms-azs-searchid');

**III. Registrar eventos de pesquisa**

Toda vez que uma solicitação de pesquisa é emitida por um usuário, você deveria registrar que um evento de pesquisa com hello esquema a seguir em um evento personalizado do Application Insights:

**ServiceName**: nome do serviço de pesquisa (string) **SearchId**: o identificador exclusivo (guid) da consulta de pesquisa de saudação (vem na resposta da pesquisa Olá) **IndexName**: índice de serviço de pesquisa (string) toobe consultado **QueryTerms**: termos de pesquisa (string) inseridos pelo usuário Olá **ResultCount**: (int) o número de documentos que foram retornados (vem na resposta da pesquisa Olá)  **ScoringProfile**: nome (string) de saudação pontuação perfil usado, se houver

> [!NOTE]
> Solicitar contagem em consultas de usuário gerado adicionando $count = true tooyour consulta de pesquisa. Confira mais informações [aqui](https://docs.microsoft.com/rest/api/searchservice/search-documents#request)
>

> [!NOTE]
> Lembre-se de consultas de pesquisa de log de tooonly que são geradas pelos usuários.
>

*C#*

    var properties = new Dictionary <string, string> {
    {"SearchServiceName", <service name>},
    {"SearchId", <search Id>},
    {"IndexName", <index name>},
    {"QueryTerms", <search terms>},
    {"ResultCount", <results count>},
    {"ScoringProfile", <scoring profile used>}
    };
    telemetryClient.TrackEvent("Search", properties);

*JavaScript*

    appInsights.trackEvent("Search", {
    SearchServiceName: <service name>,
    SearchId: <search id>,
    IndexName: <index name>,
    QueryTerms: <search terms>,
    ResultCount: <results count>,
    ScoringProfile: <scoring profile used>
    });

**IV. Registrar eventos de clique**

Sempre que um usuário clica em um documento, esse é um sinal que deve ser registrado para fins de análise de pesquisa. Use toolog de eventos personalizados do Application Insights esses eventos com hello esquema a seguir:

**ServiceName**: nome do serviço de pesquisa (string) **SearchId**: o identificador exclusivo (guid) de consulta de pesquisa relacionada Olá **DocId**: identificador de documento (string) **posição** : página de resultados de classificação (int) do documento hello na pesquisa de saudação

> [!NOTE]
> Posição refere-se a ordem de toohello cardeal em seu aplicativo. Você é livre tooset esse número, desde que ele sempre tem Olá mesmo, tooallow para comparação.
>

*C#*

    var properties = new Dictionary <string, string> {
    {"SearchServiceName", <service name>},
    {"SearchId", <search id>},
    {"ClickedDocId", <clicked document id>},
    {"Rank", <clicked document position>}
    };
    telemetryClient.TrackEvent("Click", properties);

*JavaScript*

    appInsights.TrackEvent("Click", {
        SearchServiceName: <service name>,
        SearchId: <search id>,
        ClickedDocId: <clicked document id>,
        Rank: <clicked document position>
    });

### <a name="3-analyze-with-power-bi-desktop"></a>3. Analisar com o Power BI Desktop

Após ter instrumentado seu aplicativo e verificar que seu aplicativo está conectado corretamente tooApplication Insights, você pode usar um modelo predefinido criado pela pesquisa do Azure para o Power BI desktop.
Este modelo contém gráficos e tabelas que ajudarão a fazem tooimprove de decisões mais fundamentada o desempenho da pesquisa e a relevância.

modelo da área de trabalho do tooinstantiate Olá Power BI, você precisará de três informações sobre o Application Insights. Esses dados podem ser encontrados na página de análise de tráfego de pesquisa hello, quando você seleciona Olá recursos toouse

![Dados do Application Insights na folha de análise de tráfego de pesquisa Olá][2]

Métricas incluídas no modelo da área de trabalho do Power BI hello:

*   Clique em por meio de taxa (CTR): taxa de usuários que clicar em um número de toohello de documento específico de pesquisas de total.
*   Pesquisa sem cliques: termos das principais consultas que não registraram nenhum clique
*   Clicado mais documentos: clicado mais documentos por ID em Olá últimas 24 horas, 7 dias e 30 dias.
*   Pares de documento de termo populares: termos que resultam em Olá mesmo documento é clicado, ordenados por cliques.
*   Tempo tooclick: cliques classificados pelo tempo desde a consulta de pesquisa Olá

![Modelo do Power BI para leitura do Application Insights][3]


## <a name="next-steps"></a>Próximas etapas
Instrumentar seu aplicativo tooget avançado e criteriosos dados de pesquisa sobre o serviço de pesquisa.

Encontre mais informações sobre o Application Insights [aqui](https://go.microsoft.com/fwlink/?linkid=842905). Visite o Application Insights [página de preços](https://azure.microsoft.com/pricing/details/application-insights/) toolearn mais informações sobre seus diferentes camadas de serviço.

Saiba mais sobre como criar relatórios incríveis. Confira [Introdução ao Power BI Desktop](https://powerbi.microsoft.com/en-us/documentation/powerbi-desktop-getting-started/) para obter detalhes

<!--Image references-->
[1]: ./media/search-traffic-analytics/AzureSearch-TrafficAnalytics.png
[2]: ./media/search-traffic-analytics/AzureSearch-AppInsightsData.png
[3]: ./media/search-traffic-analytics/AzureSearch-PBITemplate.png
