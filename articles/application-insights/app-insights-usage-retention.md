---
title: "Análise de retenção de usuários para aplicativos Web com o Azure Application Insights | Microsoft Docs"
description: "Quantos usuários retornam ao seu aplicativo?"
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
ms.openlocfilehash: 7f7ca19ab171278bbd82f68e3822bc650b25373d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="user-retention-analysis-for-web-applications-with-application-insights"></a><span data-ttu-id="177ef-103">Análise de retenção de usuários para aplicativos Web com o Application Insights</span><span class="sxs-lookup"><span data-stu-id="177ef-103">User retention analysis for web applications with Application Insights</span></span>

<span data-ttu-id="177ef-104">O recurso de retenção no [Azure Application Insights](app-insights-overview.md) ajuda a analisar quantos usuários retornam ao seu aplicativo e com que frequência eles executam determinadas tarefas ou atingem metas.</span><span class="sxs-lookup"><span data-stu-id="177ef-104">The retention feature in [Azure Application Insights](app-insights-overview.md) helps you analyze how many users return to your app, and how often they perform particular tasks or achieve goals.</span></span> <span data-ttu-id="177ef-105">Por exemplo, caso gerencie um site de jogos, você pode comparar o número de usuários que retornam ao site após perder um jogo com o número de usuários que retornam após vencer.</span><span class="sxs-lookup"><span data-stu-id="177ef-105">For example, if you run a game site, you could compare the numbers of users who return to the site after losing a game with the number who return after winning.</span></span> <span data-ttu-id="177ef-106">Esse conhecimento pode ajudar a melhorar a experiência do usuário e sua estratégia de negócios.</span><span class="sxs-lookup"><span data-stu-id="177ef-106">This knowledge can help you improve both your user experience and your business strategy.</span></span>

## <a name="get-started"></a><span data-ttu-id="177ef-107">Introdução</span><span class="sxs-lookup"><span data-stu-id="177ef-107">Get started</span></span>

<span data-ttu-id="177ef-108">Caso ainda não veja dados na ferramenta de retenção do portal do Application Insights, [saiba como começar a usar as ferramentas de uso](app-insights-usage-overview.md).</span><span class="sxs-lookup"><span data-stu-id="177ef-108">If you don't yet see data in the retention tool in the Application Insights portal, [learn how to get started with the usage tools](app-insights-usage-overview.md).</span></span>

## <a name="the-retention-tool"></a><span data-ttu-id="177ef-109">A ferramenta de retenção</span><span class="sxs-lookup"><span data-stu-id="177ef-109">The Retention tool</span></span>

![Ferramenta de retenção](./media/app-insights-usage-retention/retention.png)

1. <span data-ttu-id="177ef-111">A barra de ferramentas permite aos usuários criar novos relatórios de retenção, abrir os relatórios de retenção existentes, salvar o relatório de retenção atual ou salvar como, reverter as alterações feitas nos relatórios salvos, atualizar dados no relatório, compartilhar relatórios por email ou link direto e acessar a página de documentação.</span><span class="sxs-lookup"><span data-stu-id="177ef-111">The toolbar allows users to create new retention reports, open existing retention reports, save current retention report or save as, revert changes made to saved reports, refresh data on the report, share report via email or direct link, and access the documentation page.</span></span> 
2. <span data-ttu-id="177ef-112">Por padrão, a retenção mostra todos os usuários que fizeram algo e então voltaram e fizeram outra coisa em um período.</span><span class="sxs-lookup"><span data-stu-id="177ef-112">By default, retention shows all users who did anything then came back and did anything else over a period.</span></span> <span data-ttu-id="177ef-113">Você pode selecionar diferentes combinações de eventos para estreitar o foco em atividades de usuário específico.</span><span class="sxs-lookup"><span data-stu-id="177ef-113">You can select different combination of events to narrow the focus on specific user activities.</span></span>
3. <span data-ttu-id="177ef-114">Adicione um ou mais filtros para as propriedades.</span><span class="sxs-lookup"><span data-stu-id="177ef-114">Add one or more filters on properties.</span></span> <span data-ttu-id="177ef-115">Por exemplo, você pode se concentrar em usuários de um determinado país ou região.</span><span class="sxs-lookup"><span data-stu-id="177ef-115">For example, you can focus on users in a particular country or region.</span></span> <span data-ttu-id="177ef-116">Clique em **Atualizar** depois de configurar os filtros.</span><span class="sxs-lookup"><span data-stu-id="177ef-116">Click **Update** after setting the filters.</span></span> 
4. <span data-ttu-id="177ef-117">O gráfico de retenção geral mostra um resumo de retenção de usuário entre o período selecionado.</span><span class="sxs-lookup"><span data-stu-id="177ef-117">The overall retention chart shows a summary of user retention across the selected time period.</span></span> 
5. <span data-ttu-id="177ef-118">A grade mostra o número de usuários retidos de acordo com o construtor de consultas no nº 2.</span><span class="sxs-lookup"><span data-stu-id="177ef-118">The grid shows the number of users retained according to the query builder in #2.</span></span> <span data-ttu-id="177ef-119">Cada linha representa um coorte de usuários que realizaram qualquer evento no período mostrado.</span><span class="sxs-lookup"><span data-stu-id="177ef-119">Each row represents a cohort of users who performed any event in the time period shown.</span></span> <span data-ttu-id="177ef-120">Cada célula na linha mostra quantas pessoas desse coorte retornaram pelo menos uma vez em um período posterior.</span><span class="sxs-lookup"><span data-stu-id="177ef-120">Each cell in the row shows how many of that cohort returned at least once in a later period.</span></span> <span data-ttu-id="177ef-121">Alguns usuários podem retornar em mais de um período.</span><span class="sxs-lookup"><span data-stu-id="177ef-121">Some users may return in more than one period.</span></span> 
6. <span data-ttu-id="177ef-122">Os cartões de informações mostram os cinco principais eventos de início e os cinco eventos principais retornados para dar aos usuários uma ideia melhor sobre seus relatórios de retenção.</span><span class="sxs-lookup"><span data-stu-id="177ef-122">The insights cards show top five initiating events, and top five returned events to give users a better understanding of their retention report.</span></span> 

![Foco de mouse de retenção](./media/app-insights-usage-retention/hover.png)

<span data-ttu-id="177ef-124">Os usuários podem focalize células sobre a ferramenta de retenção para acessar as dicas de ferramenta e o botão de análise explicando o que significa que a célula.</span><span class="sxs-lookup"><span data-stu-id="177ef-124">Users can hover over cells on the retention tool to access the analytics button and tool tips explaining what the cell means.</span></span> <span data-ttu-id="177ef-125">Botão análise leva o usuário para a ferramenta de análise com uma consulta preenchida previamente para gerar os usuários da célula.</span><span class="sxs-lookup"><span data-stu-id="177ef-125">The Analytics button takes users to the Analytics tool with a pre-populated query to generate users from the cell.</span></span> 

## <a name="use-business-events-to-track-retention"></a><span data-ttu-id="177ef-126">Usar eventos de negócios para monitorar a retenção</span><span class="sxs-lookup"><span data-stu-id="177ef-126">Use business events to track retention</span></span>

<span data-ttu-id="177ef-127">Para obter a análise de retenção mais útil, meça eventos que representam atividades de negócios significativas.</span><span class="sxs-lookup"><span data-stu-id="177ef-127">To get the most useful retention analysis, measure events that represent significant business activities.</span></span> 

<span data-ttu-id="177ef-128">Por exemplo, muitos usuários podem abrir uma página em seu aplicativo sem jogar o jogo que ela exibe.</span><span class="sxs-lookup"><span data-stu-id="177ef-128">For example, many users might open a page in your app without playing the game that it displays.</span></span> <span data-ttu-id="177ef-129">Monitorar apenas as exibições de página, portanto, forneceria uma estimativa imprecisa de quantas pessoas retornam para jogar o jogo após tê-lo jogado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="177ef-129">Tracking just the page views would therefore provide an inaccurate estimate of how many people return to play the game after enjoying it previously.</span></span> <span data-ttu-id="177ef-130">Para obter uma visão clara dos jogadores que retornam, seu aplicativo deve enviar um evento personalizado quando um usuário de fato jogar.</span><span class="sxs-lookup"><span data-stu-id="177ef-130">To get a clear picture of returning players, your app should send a custom event when a user actually plays.</span></span>  

<span data-ttu-id="177ef-131">É uma boa prática codificar eventos personalizados que representam ações de negócios essenciais e usá-los para sua análise de retenção.</span><span class="sxs-lookup"><span data-stu-id="177ef-131">It's good practice to code custom events that represent key business actions, and use these for your retention analysis.</span></span> <span data-ttu-id="177ef-132">Para capturar o resultado do jogo, você precisa escrever uma linha de código para enviar um evento personalizado para o Application Insights.</span><span class="sxs-lookup"><span data-stu-id="177ef-132">To capture the game outcome, you need to write a line of code to send a custom event to Application Insights.</span></span> <span data-ttu-id="177ef-133">Se você a escrever no código da página da Web ou no Node.JS, ela fica assim:</span><span class="sxs-lookup"><span data-stu-id="177ef-133">If you write it in the web page code or in Node.JS, it looks like this:</span></span>

```JavaScript
    appinsights.trackEvent("won game");
```

<span data-ttu-id="177ef-134">Ou no código de servidor do ASP.NET:</span><span class="sxs-lookup"><span data-stu-id="177ef-134">Or in ASP.NET server code:</span></span>

```C#
   telemetry.TrackEvent("won game");
```

<span data-ttu-id="177ef-135">[Saiba mais sobre como escrever eventos personalizados](app-insights-api-custom-events-metrics.md#trackevent).</span><span class="sxs-lookup"><span data-stu-id="177ef-135">[Learn more about writing custom events](app-insights-api-custom-events-metrics.md#trackevent).</span></span>


## <a name="next-steps"></a><span data-ttu-id="177ef-136">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="177ef-136">Next steps</span></span>
- <span data-ttu-id="177ef-137">Para habilitar as experiências de uso, comece enviando [eventos personalizados](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) ou [exibições de página](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span><span class="sxs-lookup"><span data-stu-id="177ef-137">To enable usage experiences, start sending [custom events](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) or [page views](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span></span>
- <span data-ttu-id="177ef-138">Se você já envia eventos personalizados ou exibições de página, explore as ferramentas de uso para saber como os usuários utilizam o seu serviço.</span><span class="sxs-lookup"><span data-stu-id="177ef-138">If you already send custom events or page views, explore the Usage tools to learn how users use your service.</span></span>
    - [<span data-ttu-id="177ef-139">Usuários, Sessões, Eventos</span><span class="sxs-lookup"><span data-stu-id="177ef-139">Users, Sessions, Events</span></span>](app-insights-usage-segmentation.md)
    - [<span data-ttu-id="177ef-140">Funis</span><span class="sxs-lookup"><span data-stu-id="177ef-140">Funnels</span></span>](usage-funnels.md)
    - [<span data-ttu-id="177ef-141">Fluxos de Usuário</span><span class="sxs-lookup"><span data-stu-id="177ef-141">User Flows</span></span>](app-insights-usage-flows.md)
    - [<span data-ttu-id="177ef-142">Pastas de trabalho</span><span class="sxs-lookup"><span data-stu-id="177ef-142">Workbooks</span></span>](app-insights-usage-workbooks.md)
    - [<span data-ttu-id="177ef-143">Adicionar contexto de usuário</span><span class="sxs-lookup"><span data-stu-id="177ef-143">Add user context</span></span>](app-insights-usage-send-user-context.md)


