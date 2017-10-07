---
title: aplicativos web do aaaAzure Application Insights para JavaScript | Microsoft Docs
description: "Obter contagens de sessões e exibições de páginas e dados de clientes da Web e acompanhar padrões de uso. Detecte exceções e problemas de desempenho em páginas da Web do JavaScript."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 3b710d09-6ab4-4004-b26a-4fa840039500
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 986db3c3776471f9f8556f4e09f2d02aad022549
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-for-web-pages"></a>Application Insights para páginas da Web
Saiba mais sobre o desempenho de saudação e o uso de seu aplicativo ou página da web. Se você adicionar [Application Insights](app-insights-overview.md) tooyour script de página, você obter intervalos de página for carregada e chamadas AJAX, contagens e detalhes de exceções de navegador e falhas de AJAX, bem como os usuários e contagens de sessão. Todos esses itens podem ser segmentados por página, sistema operacional cliente e versão do navegador, localização geográfica e outras dimensões. Você pode definir alertas para contagens de falhas ou carregamento de páginas lento. E inserindo chamadas de rastreamento no seu código JavaScript, você pode controlar como os diferentes recursos de saudação do seu aplicativo de página da web são usados.

O Application Insights pode ser usado com todas as páginas da Web: basta adicionar um breve trecho de JavaScript. Se o serviço Web for [Java](app-insights-java-get-started.md) ou [ASP.NET](app-insights-asp-net.md), você poderá integrar a telemetria de seu servidor e clientes.

![Em portal.azure.com, abra o recurso do aplicativo e clique em Navegador](./media/app-insights-javascript/03.png)

Você precisa de uma assinatura muito[Microsoft Azure](https://azure.com). Se sua equipe tem uma assinatura organizacional, peça ao Olá proprietário tooadd seu tooit Account da Microsoft. O desenvolvimento e o uso em pequena escala não custam nada.

## <a name="set-up-application-insights-for-your-web-page"></a>Configurar o Application Insights para sua página da Web
Adicione páginas Olá carregador código trecho tooyour da web, da seguinte maneira.

### <a name="open-or-create-application-insights-resource"></a>Abrir ou criar um recurso do Application Insights
saudação de recurso do Application Insights é onde os dados sobre o desempenho e o uso da página são exibidos. 

Entre no [portal do Azure](https://portal.azure.com).

Se você definiu o monitoramento do lado do servidor de saudação do seu aplicativo, você já tem um recurso:

![Escolha Procurar, Serviços de Desenvolvedor, Application Insights.](./media/app-insights-javascript/01-find.png)

Se não tiver um, crie-o:

![Escolha Novo, Serviços de Desenvolvedor, Application Insights.](./media/app-insights-javascript/01-create.png)

*Tem dúvidas?* [Mais informações sobre a criação de um recurso](app-insights-create-new-resource.md).

### <a name="add-hello-sdk-script-tooyour-app-or-web-pages"></a>Adicionar Olá SDK script tooyour aplicativo ou páginas da web
No início rápido, obter o script hello para páginas da web:

![Na folha de visão geral sobre seu aplicativo, selecione início rápido, obter código toomonitor minhas páginas da web. Copie o script hello.](./media/app-insights-javascript/02-monitor-web-page.png)

Inserir o script hello antes Olá `</head>` marca de cada página que você deseja tootrack. Se o site tiver uma página mestre, você pode colocar o script hello existe. Por exemplo:

* Em um projeto MVC ASP.NET, você deve colocá-lo em `View\Shared\_Layout.cshtml`
* Em um site do SharePoint, no painel de controle do hello, abra [configurações do Site / página mestra](app-insights-sharepoint.md).

script Hello contém a chave de instrumentação Olá que direciona o recurso do Application Insights do hello dados tooyour. 

([Explicação mais profunda sobre script hello. ](http://apmtips.com/blog/2015/03/18/javascript-snippet-explained/))

*(Se você estiver usando uma estrutura de página da Web conhecida, procure adaptadores do Application Insights. Por exemplo, há [um módulo AngularJS](http://ngmodules.org/modules/angular-appinsights).)*

## <a name="detailed-configuration"></a>Configuração detalhada
Há vários [parâmetros](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) que você pode definir, embora, na maioria dos casos, isso não seja preciso. Por exemplo, você pode desabilitar ou limitar o número de saudação de chamadas Ajax relatado por modo de exibição de página (tooreduce tráfego). Ou você pode configurar depuração modo toohave telemetria mover rapidamente por meio do pipeline de saudação sem sendo processadas em lotes.

tooset esses parâmetros, pesquisar esta linha no trecho de código hello e adicionar mais itens separados por vírgula após:

    })({
      instrumentationKey: "..."
      // Insert here
    });

Olá [parâmetros disponíveis](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config) incluem:

    // Send telemetry immediately without batching.
    // Remember tooremove this when no longer required, as it
    // can affect browser performance.
    enableDebug: boolean,

    // Don't log browser exceptions.
    disableExceptionTracking: boolean,

    // Don't log ajax calls.
    disableAjaxTracking: boolean,

    // Limit number of Ajax calls logged, tooreduce traffic.
    maxAjaxCallsPerView: 10, // default is 500

    // Time page load up tooexecution of first trackPageView().
    overridePageViewDuration: boolean,

    // Set these dynamically for an authenticated user.
    appUserId: string,
    accountId: string,



## <a name="run"></a>Executar seu aplicativo
Executar seu aplicativo web, usam um enquanto toogenerate telemetria e aguarde um pouco. Você pode executar usando Olá **F5** da chave no computador de desenvolvimento, ou publicá-lo e permitir que os usuários brincar com ele.

Se você quiser toocheck telemetria de saudação que um aplicativo web está enviando tooApplication Insights, use as ferramentas de depuração do seu navegador (**F12** em muitos navegadores). Dados são enviados toodc.services.visualstudio.com.

## <a name="explore-your-browser-performance-data"></a>Explorar seus dados de desempenho do navegador
Olá abrir navegador folha tooshow agregados dados de desempenho de navegadores dos usuários.

![Em portal.azure.com, abra o recurso do aplicativo e clique em Configurações, Navegador](./media/app-insights-javascript/03.png)

*Não há dados ainda? Clique em **atualização** no início de saudação da página de saudação. Nada mesmo assim? Consulte [Solução de problemas](app-insights-troubleshoot-faq.md).*

Olá navegador folha é um [folha do Metrics Explorer](app-insights-metrics-explorer.md) com filtros predefinidos e as opções de gráfico. Você pode editar o intervalo de tempo de saudação, filtros e configuração de gráfico se desejar e salvar o resultado da saudação como um favorito. Clique em **restaurar padrões** configuração de folha tooget toohello back original.

## <a name="page-load-performance"></a>Desempenho de carregamento de página
Em Olá superior é um gráfico segmentado de tempos de carregamento de página. altura total de saudação do gráfico de saudação representa Olá tempo médio tooload e exibir páginas de seu aplicativo nos navegadores dos usuários. tempo de saudação é medido a partir quando navegador Olá envia a solicitação HTTP inicial de saudação até que a carga síncrona todos os eventos tiverem sido processados, incluindo o layout e a execução de scripts. Ele não inclui tarefas assíncronas, como carregar Web parts de chamadas AJAX.

gráfico de saudação segmentos tempo de carregamento de página total Olá em hello [intervalos padrão definidos pelo W3C](http://www.w3.org/TR/navigation-timing/#processing-model). 

![](./media/app-insights-javascript/08-client-split.png)

Observe que Olá *de conexão de rede* tempo geralmente é menor do que o esperado, pois é uma média sobre todas as solicitações do servidor de toohello navegador hello. Muitas solicitações individuais têm um tempo de conexão de 0 porque já existe um servidor de toohello conexão ativa.

### <a name="slow-loading"></a>Carregamento lento?
O carregamento de página lento é uma grande fonte de insatisfação para seus usuários. Se o gráfico de saudação indica carregamentos de página lento, é fácil toodo algumas pesquisas de diagnóstica.

gráfico de saudação mostra a média de saudação de todas as cargas de página em seu aplicativo. toosee se o problema de saudação confinados tooparticular páginas, aparência ainda mais para baixo folha hello, onde há uma grade segmentada por URL da página:

![](./media/app-insights-javascript/09-page-perf.png)

Observe a contagem de exibição de página hello e o desvio padrão. Se a contagem de páginas de saudação é muito baixa, em seguida, problema de saudação não está afetando usuários muito. Desvio padrão (média de toohello comparável em si) alta indica muita variação entre medidas individuais.

**Aplicar zoom em uma URL e uma exibição de página.** Clique em qualquer nome de página toosee uma folha de navegador gráficos filtrados toothat apenas URL; e, em seguida, em uma instância de uma exibição de página.

![](./media/app-insights-javascript/35.png)

Clique em `...` para obter uma lista completa de propriedades para esse evento, ou inspecionar chamadas Ajax de saudação e eventos relacionados. Chamadas lentas do Ajax afetam Olá tempo de carregamento de página geral, se eles são síncronos. Relacionados a eventos incluem solicitações do servidor de saudação mesma URL (se você configurou o Application Insights no seu servidor web).

**Desempenho da página ao longo do tempo.** Na folha de navegadores hello, altere grade de tempo de carregamento da exibição de página de saudação em uma toosee de gráfico de linha se houvesse picos em momentos específicos:

![Clique em cabeçalho Olá da grade de saudação e selecione um novo tipo de gráfico](./media/app-insights-javascript/10-page-perf-area.png)

**Segmentar por outras dimensões.** Talvez as páginas estão tooload mais lento em uma localidade específica do navegador, do sistema operacional cliente ou usuário? Adicionar um novo gráfico e fazer experiências com hello **Agrupar por** dimensão.

![](./media/app-insights-javascript/21.png)

## <a name="ajax-performance"></a>Desempenho do AJAX
Verifique se chamadas AJAX em páginas da Web estão tendo um bom desempenho. Elas geralmente são usados toofill partes da página de forma assíncrona. Embora hello página geral pode carregar imediatamente, os usuários podem ser frustrados diante de partes da web em branco, aguardando tooappear dados neles.

Chamadas AJAX feitas na página da web são mostradas na folha de navegadores hello como dependências.

Gráficos de resumo na parte superior de saudação da folha de saudação são:

![](./media/app-insights-javascript/31.png)

e grades detalhadas mais abaixo:

![](./media/app-insights-javascript/33.png)

Clique em qualquer linha para obter detalhes específicos.

> [!NOTE]
> Se você excluir o filtro de navegadores Olá na folha hello, servidor e dependências de AJAX inclusos nesses gráficos. Clique em filtro de saudação tooreconfigure restaurar padrões.
> 
> 

**toodrill em chamadas Ajax com falha** Role para baixo da grade de falhas de dependência de toohello e, em seguida, clique em um instâncias específicas de toosee de linha.

![](./media/app-insights-javascript/37.png)


Clique em `...` de telemetria de saudação completo para uma chamada Ajax.

### <a name="no-ajax-calls-reported"></a>Nenhuma chamada Ajax foi relatada?
Chamadas AJAX incluem todas as chamadas HTTP/HTTPS feitas do script hello da página da web. Se você não vê-los relatado, verifique desse trecho de código Olá não definida Olá `disableAjaxTracking` ou `maxAjaxCallsPerView` [parâmetros](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config).

## <a name="browser-exceptions"></a>Exceções de navegador
Na folha de navegadores hello, há um gráfico de resumo de exceções e uma grade dos tipos de exceção ainda mais para baixo de folha de saudação.

![](./media/app-insights-javascript/39.png)

Se você não vir as exceções de navegador relatadas, verifique desse trecho de código Olá não define Olá `disableExceptionTracking` [parâmetro](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#config).

## <a name="inspect-individual-page-view-events"></a>Inspecionar eventos de exibição de páginas individuais

Normalmente a telemetria de exibição da página é analisada pelo Application Insights e você vê somente relatórios cumulativos, calculados sobre todos os seus usuários. Mas para a finalidade de depuração, você também pode olhar para os eventos de exibição da página individua.

Na folha de diagnóstico pesquisa hello, defina filtros tooPage exibição.

![](./media/app-insights-javascript/12-search-pages.png)

Selecione qualquer evento toosee mais detalhes. Na página de detalhes do hello, clique em "…" toosee ainda mais detalhes.

> [!NOTE]
> Se você usar [pesquisa](app-insights-diagnostic-search.md), observe que você tenha palavras inteiras toomatch: "Sobre" e "sobre" não coincidem "Sobre".
> 
> 

Você também pode usar Olá poderoso [linguagem de consulta de análise de Log](https://docs.microsoft.com/azure/application-insights/app-insights-analytics-tour#browser-timings-table) toosearch modos de exibição de página.

### <a name="page-view-properties"></a>Propriedades de exibição de página
* **Duração do modo de exibição de página** 
  
  * Por padrão, Olá tempo que demora tooload Olá página, carga de toofull de solicitação de cliente (incluindo arquivos auxiliares, mas excluindo tarefas assíncronas, como chamadas Ajax). 
  * Se você definir `overridePageViewDuration` em Olá [configuração de página](#detailed-configuration), Olá intervalo entre tooexecution de solicitação de cliente de saudação primeiro `trackPageView`. Se você tiver movido trackPageView de sua posição normal após a inicialização de saudação do script hello, ele refletirá um valor diferente.
  * Se `overridePageViewDuration` é definido e uma duração argumento for fornecido no hello `trackPageView()` chamar, em seguida, o valor do argumento Olá é usado em vez disso. 

## <a name="custom-page-counts"></a>Contagens da página personalizada
Por padrão, uma contagem de página ocorre sempre que uma nova página carrega no navegador de saudação do cliente.  Mas talvez você queira toocount exibições de página adicionais. Por exemplo, uma página pode exibir seu conteúdo de guias e desejar toocount uma página quando o usuário Olá alterna guias. Ou código JavaScript na página Olá pode carregar um novo conteúdo sem alterar a URL do navegador hello.

Inserir uma chamada de JavaScript como esta no ponto de apropriado Olá no código do cliente:

    appInsights.trackPageView(myPageName);

nome da página Olá pode conter Olá mesmo caracteres como uma URL, mas nada após "#" ou "?" será ignorado.

## <a name="usage-tracking"></a>Acompanhamento de uso
Deseja toofind out que seus usuários fazem com seu aplicativo?

* [Saiba mais sobre acompanhamento de uso](app-insights-web-track-usage.md)
* [Saiba mais sobre os eventos e as métricas personalizados de API](app-insights-api-custom-events-metrics.md).

## <a name="video"></a> Vídeo


> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]



## <a name="next"></a> Próximas etapas
* [Acompanhar uso](app-insights-web-track-usage.md)
* [Eventos e métricas personalizados](app-insights-api-custom-events-metrics.md)
* [Build-measure-learn](app-insights-web-track-usage.md)

