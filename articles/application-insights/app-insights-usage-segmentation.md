---
title: "Análise de usuários, sessões e eventos no Application Insights do Azure | Microsoft Docs"
description: "Análise demográfica dos usuários de seu aplicativo Web."
services: application-insights
documentationcenter: 
author: botatoes
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 05/03/2017
ms.author: bwren
ms.openlocfilehash: b154a01d1690bff4950ebc1ff5a5b89894d4d111
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="users-sessions-and-events-analysis-in-application-insights"></a><span data-ttu-id="a76d4-103">Análise de usuários, sessões e eventos no Application Insights</span><span class="sxs-lookup"><span data-stu-id="a76d4-103">Users, sessions, and events analysis in Application Insights</span></span>

<span data-ttu-id="a76d4-104">Descubra quando as pessoas usam seu aplicativo Web, em quais páginas elas estão mais interessadas, onde os usuários estão localizados e quais navegadores e sistemas operacionais eles usam.</span><span class="sxs-lookup"><span data-stu-id="a76d4-104">Find out when people use your web app, what pages they're most interested in, where your users are located, what browsers and operating systems they use.</span></span> <span data-ttu-id="a76d4-105">Analisar a telemetria de negócios e de uso com o [Application Insights do Azure](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a76d4-105">Analyze business and usage telemetry by using [Azure Application Insights](app-insights-overview.md).</span></span>

## <a name="get-started"></a><span data-ttu-id="a76d4-106">Introdução</span><span class="sxs-lookup"><span data-stu-id="a76d4-106">Get started</span></span>

<span data-ttu-id="a76d4-107">Caso ainda não veja dados nas folhas de usuários, sessões ou eventos no portal do Application Insights, [veja como começar a usar as ferramentas de uso](app-insights-usage-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a76d4-107">If you don't yet see data in the users, sessions, or events blades in the Application Insights portal, [learn how to get started with the usage tools](app-insights-usage-overview.md).</span></span>

## <a name="the-users-sessions-and-events-segmentation-tool"></a><span data-ttu-id="a76d4-108">A ferramenta de segmentação de Usuários, Sessões e Eventos</span><span class="sxs-lookup"><span data-stu-id="a76d4-108">The Users, Sessions, and Events segmentation tool</span></span>

<span data-ttu-id="a76d4-109">Três das folhas de uso usam a mesma ferramenta para dividir a telemetria do seu aplicativo Web em três perspectivas diferentes.</span><span class="sxs-lookup"><span data-stu-id="a76d4-109">Three of the usage blades use the same tool to slice and dice telemetry from your web app from three perspectives.</span></span> <span data-ttu-id="a76d4-110">Filtrando e dividindo os dados, você pode descobrir informações sobre o uso relativo de diferentes páginas e recursos.</span><span class="sxs-lookup"><span data-stu-id="a76d4-110">By filtering and splitting the data, you can uncover insights about the relative usage of different pages and features.</span></span>

* <span data-ttu-id="a76d4-111">**Ferramenta de Usuários**: quantas pessoas usaram seu aplicativo e seus recursos.</span><span class="sxs-lookup"><span data-stu-id="a76d4-111">**Users tool**: How many people used your app and its features.</span></span>  <span data-ttu-id="a76d4-112">Os usuários são contados usando IDs anônimas armazenadas em cookies do navegador.</span><span class="sxs-lookup"><span data-stu-id="a76d4-112">Users are counted by using anonymous IDs stored in browser cookies.</span></span> <span data-ttu-id="a76d4-113">Uma única pessoa que usar diferentes navegadores ou computadores será contada como mais de um usuário.</span><span class="sxs-lookup"><span data-stu-id="a76d4-113">A single person using different browsers or machines will be counted as more than one user.</span></span>
* <span data-ttu-id="a76d4-114">**Ferramenta de Sessões**: quantas sessões de atividade do usuário incluíram determinadas páginas e recursos de seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a76d4-114">**Sessions tool**: How many sessions of user activity have included certain pages and features of your app.</span></span> <span data-ttu-id="a76d4-115">Uma sessão é contada após meia hora de inatividade do usuário ou após 24 horas contínuas de uso.</span><span class="sxs-lookup"><span data-stu-id="a76d4-115">A session is counted after half an hour of user inactivity, or after continuous 24h of use.</span></span>
* <span data-ttu-id="a76d4-116">**Ferramenta de Eventos**: com que frequência determinadas páginas e recursos de seu aplicativo são usados.</span><span class="sxs-lookup"><span data-stu-id="a76d4-116">**Events tool**: How often certain pages and features of your app are used.</span></span> <span data-ttu-id="a76d4-117">Uma exibição de página é contada quando um navegador carrega uma página do seu aplicativo, desde que você a tenha [instrumentado](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="a76d4-117">A page view is counted when a browser loads a page from your app, provided you have [instrumented it](app-insights-javascript.md).</span></span> 

    <span data-ttu-id="a76d4-118">Um evento personalizado representa uma ocorrência de algo que esteja acontecendo em seu aplicativo, geralmente uma interação do usuário, como um clique de botão ou a conclusão de uma tarefa.</span><span class="sxs-lookup"><span data-stu-id="a76d4-118">A custom event represents one occurrence of something happening in your app, often a user interaction like a button click or the completion of some task.</span></span> <span data-ttu-id="a76d4-119">Insira o código em seu aplicativo para [gerar eventos personalizados](app-insights-api-custom-events-metrics.md#trackevent).</span><span class="sxs-lookup"><span data-stu-id="a76d4-119">You insert code in your app to [generate custom events](app-insights-api-custom-events-metrics.md#trackevent).</span></span>

![Ferramenta de uso](./media/app-insights-usage-segmentation/users.png)

## <a name="querying-for-certain-users"></a><span data-ttu-id="a76d4-121">Consultar determinados usuários</span><span class="sxs-lookup"><span data-stu-id="a76d4-121">Querying for Certain Users</span></span> 

<span data-ttu-id="a76d4-122">Explore diferentes grupos de usuários, ajustando as opções de consulta na parte superior da ferramenta de Usuários:</span><span class="sxs-lookup"><span data-stu-id="a76d4-122">Explore different groups of users by adjusting the query options at the top of the Users tool:</span></span> 

* <span data-ttu-id="a76d4-123">Quem usou: escolha exibições de página e eventos personalizados.</span><span class="sxs-lookup"><span data-stu-id="a76d4-123">Who used: Choose custom events and page views.</span></span> 
* <span data-ttu-id="a76d4-124">Durante: escolha um intervalo de tempo.</span><span class="sxs-lookup"><span data-stu-id="a76d4-124">During: Choose a time range.</span></span> 
* <span data-ttu-id="a76d4-125">Por: escolha como compartimentar os dados, seja segundo um período ou segundo outra propriedade, como navegador ou cidade.</span><span class="sxs-lookup"><span data-stu-id="a76d4-125">By: Choose how to bucket the data, either by a period of time or by another property such as browser or city.</span></span> 
* <span data-ttu-id="a76d4-126">Dividido por: escolha uma propriedade segundo a qual o segmento ou os dados deverão ser divididos.</span><span class="sxs-lookup"><span data-stu-id="a76d4-126">Split By: Choose a property by which to split or segment the data.</span></span> 
* <span data-ttu-id="a76d4-127">Adicionar filtros: limite a consulta a determinados usuários, sessões ou eventos com base em suas propriedades, como navegador ou cidade.</span><span class="sxs-lookup"><span data-stu-id="a76d4-127">Add Filters: Limit the query to certain users, sessions, or events based on their properties, such as browser or city.</span></span> 
 
## <a name="saving-and-sharing-reports"></a><span data-ttu-id="a76d4-128">Salvar e compartilhar relatórios</span><span class="sxs-lookup"><span data-stu-id="a76d4-128">Saving and sharing reports</span></span> 
<span data-ttu-id="a76d4-129">Você pode salvar relatórios de Usuários, de forma privada na seção Meus Relatórios ou de forma compartilhada com quem tiver acesso a esse recurso do Application Insights na seção Relatórios Compartilhados.</span><span class="sxs-lookup"><span data-stu-id="a76d4-129">You can save Users reports, either private just to you in the My Reports section, or shared with everyone else with access to this Application Insights resource in the Shared Reports section.</span></span>  
 
<span data-ttu-id="a76d4-130">Ao salvar um relatório ou editar suas propriedades, escolher "Intervalo de tempo relativo atual" para salvar um relatório atualizará continuamente os dados, voltando um período determinado.</span><span class="sxs-lookup"><span data-stu-id="a76d4-130">While saving a report or editing its properties, choose "Current Relative Time Range" to save a report will continuously refreshed data, going back some fixed amount of time.</span></span>  
 
<span data-ttu-id="a76d4-131">Escolha "Intervalo de tempo absoluto atual" para salvar um relatório com um conjunto fixo de dados.</span><span class="sxs-lookup"><span data-stu-id="a76d4-131">Choose "Current Absolute Time Range" to save a report with a fixed set of data.</span></span> <span data-ttu-id="a76d4-132">Tenha em mente que os dados no Application Insights são armazenados somente por 90 dias, portanto, se mais de 90 dias tiverem se passado desde um relatório com um intervalo de tempo absoluto foi salvo, o relatório aparecerá vazio.</span><span class="sxs-lookup"><span data-stu-id="a76d4-132">Keep in mind that data in Application Insights is only stored for 90 days, so if more than 90 days have passed since a report with an absolute time range was saved, the report will appear empty.</span></span> 
 
## <a name="example-instances"></a><span data-ttu-id="a76d4-133">Instâncias de exemplo</span><span class="sxs-lookup"><span data-stu-id="a76d4-133">Example instances</span></span>

<span data-ttu-id="a76d4-134">A seção de Instâncias do exemplo mostra informações sobre alguns eventos, sessões ou usuários individuais que correspondem à consulta atual.</span><span class="sxs-lookup"><span data-stu-id="a76d4-134">The Example instances section shows information about a handful of individual users, sessions, or events that are matched by the current query.</span></span> <span data-ttu-id="a76d4-135">Considerar e explorar os comportamentos de indivíduos, além de agregados, pode fornecer informações sobre como as pessoas realmente usam seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a76d4-135">Considering and exploring the behaviors of individuals, in addition to aggregates, can provide insights about how people actually use your app.</span></span> 
 
## <a name="insights"></a><span data-ttu-id="a76d4-136">Insights</span><span class="sxs-lookup"><span data-stu-id="a76d4-136">Insights</span></span> 

<span data-ttu-id="a76d4-137">A barra lateral Insights mostra grandes clusters de usuários que compartilham propriedades comuns.</span><span class="sxs-lookup"><span data-stu-id="a76d4-137">The Insights sidebar shows large clusters of users that share common properties.</span></span> <span data-ttu-id="a76d4-138">Esses clusters podem revelar tendências surpreendentes de como as pessoas usam seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a76d4-138">These clusters can uncover surprising trends in how people use your app.</span></span> <span data-ttu-id="a76d4-139">Por exemplo, se 40% de todo o uso do seu aplicativo vem de pessoas que usam um único recurso.</span><span class="sxs-lookup"><span data-stu-id="a76d4-139">For example, if 40% of all of the usage of your app comes from people using a single feature.</span></span>  


## <a name="next-steps"></a><span data-ttu-id="a76d4-140">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a76d4-140">Next steps</span></span>
- <span data-ttu-id="a76d4-141">Para habilitar as experiências de uso, comece enviando [eventos personalizados](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) ou [exibições de página](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span><span class="sxs-lookup"><span data-stu-id="a76d4-141">To enable usage experiences, start sending [custom events](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) or [page views](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span></span>
- <span data-ttu-id="a76d4-142">Se você já envia eventos personalizados ou exibições de página, explore as ferramentas de uso para saber como os usuários utilizam o seu serviço.</span><span class="sxs-lookup"><span data-stu-id="a76d4-142">If you already send custom events or page views, explore the Usage tools to learn how users use your service.</span></span>
    - [<span data-ttu-id="a76d4-143">Funis</span><span class="sxs-lookup"><span data-stu-id="a76d4-143">Funnels</span></span>](usage-funnels.md)
    - [<span data-ttu-id="a76d4-144">Retenção</span><span class="sxs-lookup"><span data-stu-id="a76d4-144">Retention</span></span>](app-insights-usage-retention.md)
    - [<span data-ttu-id="a76d4-145">Fluxos de Usuário</span><span class="sxs-lookup"><span data-stu-id="a76d4-145">User Flows</span></span>](app-insights-usage-flows.md)
    - [<span data-ttu-id="a76d4-146">Pastas de trabalho</span><span class="sxs-lookup"><span data-stu-id="a76d4-146">Workbooks</span></span>](app-insights-usage-workbooks.md)
    - [<span data-ttu-id="a76d4-147">Adicionar contexto de usuário</span><span class="sxs-lookup"><span data-stu-id="a76d4-147">Add user context</span></span>](app-insights-usage-send-user-context.md)

