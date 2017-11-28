---
title: "análise de aaaUser, sessão e eventos no Azure Application Insights | Documentos da Microsoft"
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
ms.openlocfilehash: 152ab90e9a25c03087d3ebbde1263ec72acb227e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="users-sessions-and-events-analysis-in-application-insights"></a><span data-ttu-id="a2367-103">Análise de usuários, sessões e eventos no Application Insights</span><span class="sxs-lookup"><span data-stu-id="a2367-103">Users, sessions, and events analysis in Application Insights</span></span>

<span data-ttu-id="a2367-104">Descubra quando as pessoas usam seu aplicativo Web, em quais páginas elas estão mais interessadas, onde os usuários estão localizados e quais navegadores e sistemas operacionais eles usam.</span><span class="sxs-lookup"><span data-stu-id="a2367-104">Find out when people use your web app, what pages they're most interested in, where your users are located, what browsers and operating systems they use.</span></span> <span data-ttu-id="a2367-105">Analisar a telemetria de negócios e de uso com o [Application Insights do Azure](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a2367-105">Analyze business and usage telemetry by using [Azure Application Insights](app-insights-overview.md).</span></span>

## <a name="get-started"></a><span data-ttu-id="a2367-106">Introdução</span><span class="sxs-lookup"><span data-stu-id="a2367-106">Get started</span></span>

<span data-ttu-id="a2367-107">Se você ainda não vir dados Olá usuários, sessões ou folhas de eventos no portal do Application Insights hello, [Saiba como tooget iniciada com ferramentas de uso de saudação](app-insights-usage-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a2367-107">If you don't yet see data in hello users, sessions, or events blades in hello Application Insights portal, [learn how tooget started with hello usage tools](app-insights-usage-overview.md).</span></span>

## <a name="hello-users-sessions-and-events-segmentation-tool"></a><span data-ttu-id="a2367-108">ferramenta de segmentação de usuários, sessões e eventos de saudação</span><span class="sxs-lookup"><span data-stu-id="a2367-108">hello Users, Sessions, and Events segmentation tool</span></span>

<span data-ttu-id="a2367-109">Três usam folhas de uso de Olá Olá mesma ferramenta tooslice e dos dados da telemetria do seu aplicativo web de três perspectivas diferentes.</span><span class="sxs-lookup"><span data-stu-id="a2367-109">Three of hello usage blades use hello same tool tooslice and dice telemetry from your web app from three perspectives.</span></span> <span data-ttu-id="a2367-110">Filtrando e dividir os dados Olá, você pode revelar informações sobre o uso de saudação relativo de diferentes páginas e recursos.</span><span class="sxs-lookup"><span data-stu-id="a2367-110">By filtering and splitting hello data, you can uncover insights about hello relative usage of different pages and features.</span></span>

* <span data-ttu-id="a2367-111">**Ferramenta de Usuários**: quantas pessoas usaram seu aplicativo e seus recursos.</span><span class="sxs-lookup"><span data-stu-id="a2367-111">**Users tool**: How many people used your app and its features.</span></span>  <span data-ttu-id="a2367-112">Os usuários são contados usando IDs anônimas armazenadas em cookies do navegador.</span><span class="sxs-lookup"><span data-stu-id="a2367-112">Users are counted by using anonymous IDs stored in browser cookies.</span></span> <span data-ttu-id="a2367-113">Uma única pessoa que usar diferentes navegadores ou computadores será contada como mais de um usuário.</span><span class="sxs-lookup"><span data-stu-id="a2367-113">A single person using different browsers or machines will be counted as more than one user.</span></span>
* <span data-ttu-id="a2367-114">**Ferramenta de Sessões**: quantas sessões de atividade do usuário incluíram determinadas páginas e recursos de seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a2367-114">**Sessions tool**: How many sessions of user activity have included certain pages and features of your app.</span></span> <span data-ttu-id="a2367-115">Uma sessão é contada após meia hora de inatividade do usuário ou após 24 horas contínuas de uso.</span><span class="sxs-lookup"><span data-stu-id="a2367-115">A session is counted after half an hour of user inactivity, or after continuous 24h of use.</span></span>
* <span data-ttu-id="a2367-116">**Ferramenta de Eventos**: com que frequência determinadas páginas e recursos de seu aplicativo são usados.</span><span class="sxs-lookup"><span data-stu-id="a2367-116">**Events tool**: How often certain pages and features of your app are used.</span></span> <span data-ttu-id="a2367-117">Uma exibição de página é contada quando um navegador carrega uma página do seu aplicativo, desde que você a tenha [instrumentado](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="a2367-117">A page view is counted when a browser loads a page from your app, provided you have [instrumented it](app-insights-javascript.md).</span></span> 

    <span data-ttu-id="a2367-118">Um evento personalizado representa uma ocorrência de algo que esteja acontecendo em seu aplicativo, geralmente uma interação do usuário como um botão, clique em ou Olá conclusão de uma tarefa.</span><span class="sxs-lookup"><span data-stu-id="a2367-118">A custom event represents one occurrence of something happening in your app, often a user interaction like a button click or hello completion of some task.</span></span> <span data-ttu-id="a2367-119">Inserir código em seu aplicativo muito[gerar eventos personalizados](app-insights-api-custom-events-metrics.md#trackevent).</span><span class="sxs-lookup"><span data-stu-id="a2367-119">You insert code in your app too[generate custom events](app-insights-api-custom-events-metrics.md#trackevent).</span></span>

![Ferramenta de uso](./media/app-insights-usage-segmentation/users.png)

## <a name="querying-for-certain-users"></a><span data-ttu-id="a2367-121">Consultar determinados usuários</span><span class="sxs-lookup"><span data-stu-id="a2367-121">Querying for Certain Users</span></span> 

<span data-ttu-id="a2367-122">Explore a diferentes grupos de usuários, ajustando as opções de consulta Olá na parte superior de saudação da ferramenta de usuários hello:</span><span class="sxs-lookup"><span data-stu-id="a2367-122">Explore different groups of users by adjusting hello query options at hello top of hello Users tool:</span></span> 

* <span data-ttu-id="a2367-123">Quem usou: escolha exibições de página e eventos personalizados.</span><span class="sxs-lookup"><span data-stu-id="a2367-123">Who used: Choose custom events and page views.</span></span> 
* <span data-ttu-id="a2367-124">Durante: escolha um intervalo de tempo.</span><span class="sxs-lookup"><span data-stu-id="a2367-124">During: Choose a time range.</span></span> 
* <span data-ttu-id="a2367-125">: Escolha como toobucket Olá dados, por um período de tempo ou por outra propriedade, como navegador ou uma cidade.</span><span class="sxs-lookup"><span data-stu-id="a2367-125">By: Choose how toobucket hello data, either by a period of time or by another property such as browser or city.</span></span> 
* <span data-ttu-id="a2367-126">Dividir por: Escolha uma propriedade de dados Olá toosplit ou segmento.</span><span class="sxs-lookup"><span data-stu-id="a2367-126">Split By: Choose a property by which toosplit or segment hello data.</span></span> 
* <span data-ttu-id="a2367-127">Adicionar filtros: Limite Olá consultar toocertain usuários, sessões ou eventos com base em suas propriedades, como navegador ou uma cidade.</span><span class="sxs-lookup"><span data-stu-id="a2367-127">Add Filters: Limit hello query toocertain users, sessions, or events based on their properties, such as browser or city.</span></span> 
 
## <a name="saving-and-sharing-reports"></a><span data-ttu-id="a2367-128">Salvar e compartilhar relatórios</span><span class="sxs-lookup"><span data-stu-id="a2367-128">Saving and sharing reports</span></span> 
<span data-ttu-id="a2367-129">Você pode salvar os relatórios de usuários, ou privada tooyou apenas na seção de meus relatórios hello, ou compartilhados com qualquer outra pessoa com acesso toothis recurso do Application Insights Olá seção relatórios compartilhados.</span><span class="sxs-lookup"><span data-stu-id="a2367-129">You can save Users reports, either private just tooyou in hello My Reports section, or shared with everyone else with access toothis Application Insights resource in hello Shared Reports section.</span></span>  
 
<span data-ttu-id="a2367-130">Ao salvar um relatório ou editar suas propriedades, escolha "Atual intervalo de tempo relativo" toosave que um relatório será continuamente atualizada dados, voltando alguma quantidade fixa de tempo.</span><span class="sxs-lookup"><span data-stu-id="a2367-130">While saving a report or editing its properties, choose "Current Relative Time Range" toosave a report will continuously refreshed data, going back some fixed amount of time.</span></span>  
 
<span data-ttu-id="a2367-131">Escolha "Atual intervalo de tempo absoluto" toosave um relatório com um conjunto fixo de dados.</span><span class="sxs-lookup"><span data-stu-id="a2367-131">Choose "Current Absolute Time Range" toosave a report with a fixed set of data.</span></span> <span data-ttu-id="a2367-132">Tenha em mente que os dados no Application Insights são armazenados somente por 90 dias, portanto, se mais de 90 dias passaram desde um relatório com um intervalo de tempo absoluto foi salvo, relatório Olá aparecerá vazio.</span><span class="sxs-lookup"><span data-stu-id="a2367-132">Keep in mind that data in Application Insights is only stored for 90 days, so if more than 90 days have passed since a report with an absolute time range was saved, hello report will appear empty.</span></span> 
 
## <a name="example-instances"></a><span data-ttu-id="a2367-133">Instâncias de exemplo</span><span class="sxs-lookup"><span data-stu-id="a2367-133">Example instances</span></span>

<span data-ttu-id="a2367-134">Olá seção de instâncias de exemplo mostra informações sobre uma série de eventos que correspondem a consulta atual hello, sessões ou usuários individuais.</span><span class="sxs-lookup"><span data-stu-id="a2367-134">hello Example instances section shows information about a handful of individual users, sessions, or events that are matched by hello current query.</span></span> <span data-ttu-id="a2367-135">Considerar e explorar os comportamentos de saudação de indivíduos, na inclusão tooaggregates, podem fornecer informações sobre como as pessoas usam, na verdade, seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a2367-135">Considering and exploring hello behaviors of individuals, in addition tooaggregates, can provide insights about how people actually use your app.</span></span> 
 
## <a name="insights"></a><span data-ttu-id="a2367-136">Insights</span><span class="sxs-lookup"><span data-stu-id="a2367-136">Insights</span></span> 

<span data-ttu-id="a2367-137">barra lateral de Insights Olá mostra grandes clusters de usuários que compartilham propriedades comuns.</span><span class="sxs-lookup"><span data-stu-id="a2367-137">hello Insights sidebar shows large clusters of users that share common properties.</span></span> <span data-ttu-id="a2367-138">Esses clusters podem revelar tendências surpreendentes de como as pessoas usam seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a2367-138">These clusters can uncover surprising trends in how people use your app.</span></span> <span data-ttu-id="a2367-139">Por exemplo, se 40% de uso de saudação do seu aplicativo todos vêm de pessoas que usam um único recurso.</span><span class="sxs-lookup"><span data-stu-id="a2367-139">For example, if 40% of all of hello usage of your app comes from people using a single feature.</span></span>  


## <a name="next-steps"></a><span data-ttu-id="a2367-140">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a2367-140">Next steps</span></span>
- <span data-ttu-id="a2367-141">uso de tooenable experiências, comece a enviar [eventos personalizados](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) ou [exibições de página](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span><span class="sxs-lookup"><span data-stu-id="a2367-141">tooenable usage experiences, start sending [custom events](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) or [page views](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span></span>
- <span data-ttu-id="a2367-142">Se você já enviar eventos personalizados ou modos de exibição de página, explorar Olá uso ferramentas toolearn como os usuários usar seu serviço.</span><span class="sxs-lookup"><span data-stu-id="a2367-142">If you already send custom events or page views, explore hello Usage tools toolearn how users use your service.</span></span>
    - [<span data-ttu-id="a2367-143">Funis</span><span class="sxs-lookup"><span data-stu-id="a2367-143">Funnels</span></span>](usage-funnels.md)
    - [<span data-ttu-id="a2367-144">Retenção</span><span class="sxs-lookup"><span data-stu-id="a2367-144">Retention</span></span>](app-insights-usage-retention.md)
    - [<span data-ttu-id="a2367-145">Fluxos de Usuário</span><span class="sxs-lookup"><span data-stu-id="a2367-145">User Flows</span></span>](app-insights-usage-flows.md)
    - [<span data-ttu-id="a2367-146">Pastas de trabalho</span><span class="sxs-lookup"><span data-stu-id="a2367-146">Workbooks</span></span>](app-insights-usage-workbooks.md)
    - [<span data-ttu-id="a2367-147">Adicionar contexto de usuário</span><span class="sxs-lookup"><span data-stu-id="a2367-147">Add user context</span></span>](app-insights-usage-send-user-context.md)

