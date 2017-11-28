---
title: "análise de retenção aaaUser para aplicativos web com o Azure Application Insights | Documentos da Microsoft"
description: "Quantos usuários retornarem tooyour aplicativo?"
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
ms.openlocfilehash: 8bcee5f1611afbd69016ec3eef27832c304762a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="user-retention-analysis-for-web-applications-with-application-insights"></a><span data-ttu-id="4e1ad-103">Análise de retenção de usuários para aplicativos Web com o Application Insights</span><span class="sxs-lookup"><span data-stu-id="4e1ad-103">User retention analysis for web applications with Application Insights</span></span>

<span data-ttu-id="4e1ad-104">recurso de retenção de saudação do [Azure Application Insights](app-insights-overview.md) ajuda a analisar quantos usuários retorna tooyour aplicativo e frequência executar determinadas tarefas ou atingir as metas.</span><span class="sxs-lookup"><span data-stu-id="4e1ad-104">hello retention feature in [Azure Application Insights](app-insights-overview.md) helps you analyze how many users return tooyour app, and how often they perform particular tasks or achieve goals.</span></span> <span data-ttu-id="4e1ad-105">Por exemplo, se você executar um site de jogos, você poderá comparar números de saudação de usuários que retornam toohello site depois de perder um jogo com número de saudação que retornam após o vencedor.</span><span class="sxs-lookup"><span data-stu-id="4e1ad-105">For example, if you run a game site, you could compare hello numbers of users who return toohello site after losing a game with hello number who return after winning.</span></span> <span data-ttu-id="4e1ad-106">Esse conhecimento pode ajudar a melhorar a experiência do usuário e sua estratégia de negócios.</span><span class="sxs-lookup"><span data-stu-id="4e1ad-106">This knowledge can help you improve both your user experience and your business strategy.</span></span>

## <a name="get-started"></a><span data-ttu-id="4e1ad-107">Introdução</span><span class="sxs-lookup"><span data-stu-id="4e1ad-107">Get started</span></span>

<span data-ttu-id="4e1ad-108">Se você ainda não vir dados na ferramenta de retenção Olá no portal do Application Insights hello, [Saiba como tooget iniciada com ferramentas de uso de saudação](app-insights-usage-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4e1ad-108">If you don't yet see data in hello retention tool in hello Application Insights portal, [learn how tooget started with hello usage tools](app-insights-usage-overview.md).</span></span>

## <a name="hello-retention-tool"></a><span data-ttu-id="4e1ad-109">ferramenta de retenção Olá</span><span class="sxs-lookup"><span data-stu-id="4e1ad-109">hello Retention tool</span></span>

![Ferramenta de retenção](./media/app-insights-usage-retention/retention.png)

1. <span data-ttu-id="4e1ad-111">barra de ferramentas Olá permite que os usuários toocreate novos relatórios de retenção, abra relatórios existentes de retenção, salvar o relatório de retenção atual ou salvar como, reverter as alterações feitas toosaved relatórios, atualizar dados no relatório hello, relatório de compartilhamento via email ou link direto e saudação de acesso página de documentação.</span><span class="sxs-lookup"><span data-stu-id="4e1ad-111">hello toolbar allows users toocreate new retention reports, open existing retention reports, save current retention report or save as, revert changes made toosaved reports, refresh data on hello report, share report via email or direct link, and access hello documentation page.</span></span> 
2. <span data-ttu-id="4e1ad-112">Por padrão, a retenção mostra todos os usuários que fizeram algo e então voltaram e fizeram outra coisa em um período.</span><span class="sxs-lookup"><span data-stu-id="4e1ad-112">By default, retention shows all users who did anything then came back and did anything else over a period.</span></span> <span data-ttu-id="4e1ad-113">Você pode selecionar diferentes combinações de eventos toonarrow Olá enfocam atividades específicas do usuário.</span><span class="sxs-lookup"><span data-stu-id="4e1ad-113">You can select different combination of events toonarrow hello focus on specific user activities.</span></span>
3. <span data-ttu-id="4e1ad-114">Adicione um ou mais filtros para as propriedades.</span><span class="sxs-lookup"><span data-stu-id="4e1ad-114">Add one or more filters on properties.</span></span> <span data-ttu-id="4e1ad-115">Por exemplo, você pode se concentrar em usuários de um determinado país ou região.</span><span class="sxs-lookup"><span data-stu-id="4e1ad-115">For example, you can focus on users in a particular country or region.</span></span> <span data-ttu-id="4e1ad-116">Clique em **atualização** depois de definir filtros de saudação.</span><span class="sxs-lookup"><span data-stu-id="4e1ad-116">Click **Update** after setting hello filters.</span></span> 
4. <span data-ttu-id="4e1ad-117">Olá geral retenção gráfico mostra um resumo de retenção de usuário em Olá período de tempo selecionado.</span><span class="sxs-lookup"><span data-stu-id="4e1ad-117">hello overall retention chart shows a summary of user retention across hello selected time period.</span></span> 
5. <span data-ttu-id="4e1ad-118">grade de Olá mostra o número Olá de usuários retidos acordo construtor de consultas toohello # 2.</span><span class="sxs-lookup"><span data-stu-id="4e1ad-118">hello grid shows hello number of users retained according toohello query builder in #2.</span></span> <span data-ttu-id="4e1ad-119">Cada linha representa um cohort de usuários que realizou a qualquer evento no tempo de saudação período mostrado.</span><span class="sxs-lookup"><span data-stu-id="4e1ad-119">Each row represents a cohort of users who performed any event in hello time period shown.</span></span> <span data-ttu-id="4e1ad-120">Cada célula na linha de saudação mostra quantas que cohort retornadas pelo menos uma vez em um período mais recente.</span><span class="sxs-lookup"><span data-stu-id="4e1ad-120">Each cell in hello row shows how many of that cohort returned at least once in a later period.</span></span> <span data-ttu-id="4e1ad-121">Alguns usuários podem retornar em mais de um período.</span><span class="sxs-lookup"><span data-stu-id="4e1ad-121">Some users may return in more than one period.</span></span> 
6. <span data-ttu-id="4e1ad-122">cartões de insights Olá mostram eventos iniciante cinco principais e cinco principais retornados os usuários de toogive eventos melhor compreensão de seus relatórios de retenção.</span><span class="sxs-lookup"><span data-stu-id="4e1ad-122">hello insights cards show top five initiating events, and top five returned events toogive users a better understanding of their retention report.</span></span> 

![Foco de mouse de retenção](./media/app-insights-usage-retention/hover.png)

<span data-ttu-id="4e1ad-124">Os usuários podem focalize células no botão de análise de Olá Olá retenção ferramenta tooaccess e dicas de ferramenta explicando célula Olá significa.</span><span class="sxs-lookup"><span data-stu-id="4e1ad-124">Users can hover over cells on hello retention tool tooaccess hello analytics button and tool tips explaining what hello cell means.</span></span> <span data-ttu-id="4e1ad-125">botão de análise de Olá leva a ferramenta de análise de toohello usuários com usuários de toogenerate uma consulta preenchida previamente da célula de saudação.</span><span class="sxs-lookup"><span data-stu-id="4e1ad-125">hello Analytics button takes users toohello Analytics tool with a pre-populated query toogenerate users from hello cell.</span></span> 

## <a name="use-business-events-tootrack-retention"></a><span data-ttu-id="4e1ad-126">Use a retenção de tootrack de eventos de negócios</span><span class="sxs-lookup"><span data-stu-id="4e1ad-126">Use business events tootrack retention</span></span>

<span data-ttu-id="4e1ad-127">tooget hello mais úteis retenção análise, eventos de medidas que representam as atividades de negócios significativa.</span><span class="sxs-lookup"><span data-stu-id="4e1ad-127">tooget hello most useful retention analysis, measure events that represent significant business activities.</span></span> 

<span data-ttu-id="4e1ad-128">Por exemplo, muitos usuários podem abrir uma página em seu aplicativo sem jogo Olá exibido.</span><span class="sxs-lookup"><span data-stu-id="4e1ad-128">For example, many users might open a page in your app without playing hello game that it displays.</span></span> <span data-ttu-id="4e1ad-129">Apenas as exibições de página Olá de controle, portanto, podem fornecer uma estimativa precisa de quantas pessoas retornam tooplay jogo Olá após ele anteriormente.</span><span class="sxs-lookup"><span data-stu-id="4e1ad-129">Tracking just hello page views would therefore provide an inaccurate estimate of how many people return tooplay hello game after enjoying it previously.</span></span> <span data-ttu-id="4e1ad-130">tooget uma visão clara de retorno de players, o aplicativo deve enviar um evento personalizado quando um usuário é reproduzido.</span><span class="sxs-lookup"><span data-stu-id="4e1ad-130">tooget a clear picture of returning players, your app should send a custom event when a user actually plays.</span></span>  

<span data-ttu-id="4e1ad-131">É uma boa prática toocode eventos personalizados que representam as ações de negócios e usá-los para sua análise de retenção.</span><span class="sxs-lookup"><span data-stu-id="4e1ad-131">It's good practice toocode custom events that represent key business actions, and use these for your retention analysis.</span></span> <span data-ttu-id="4e1ad-132">resultado de jogos do toocapture Olá, é necessário toowrite uma linha de código toosend tooApplication um evento personalizado Insights.</span><span class="sxs-lookup"><span data-stu-id="4e1ad-132">toocapture hello game outcome, you need toowrite a line of code toosend a custom event tooApplication Insights.</span></span> <span data-ttu-id="4e1ad-133">Se você escrever em código de página da web hello ou Node. js, ele é semelhante a:</span><span class="sxs-lookup"><span data-stu-id="4e1ad-133">If you write it in hello web page code or in Node.JS, it looks like this:</span></span>

```JavaScript
    appinsights.trackEvent("won game");
```

<span data-ttu-id="4e1ad-134">Ou no código de servidor do ASP.NET:</span><span class="sxs-lookup"><span data-stu-id="4e1ad-134">Or in ASP.NET server code:</span></span>

```C#
   telemetry.TrackEvent("won game");
```

<span data-ttu-id="4e1ad-135">[Saiba mais sobre como escrever eventos personalizados](app-insights-api-custom-events-metrics.md#trackevent).</span><span class="sxs-lookup"><span data-stu-id="4e1ad-135">[Learn more about writing custom events](app-insights-api-custom-events-metrics.md#trackevent).</span></span>


## <a name="next-steps"></a><span data-ttu-id="4e1ad-136">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4e1ad-136">Next steps</span></span>
- <span data-ttu-id="4e1ad-137">uso de tooenable experiências, comece a enviar [eventos personalizados](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) ou [exibições de página](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span><span class="sxs-lookup"><span data-stu-id="4e1ad-137">tooenable usage experiences, start sending [custom events](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) or [page views](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span></span>
- <span data-ttu-id="4e1ad-138">Se você já enviar eventos personalizados ou modos de exibição de página, explorar Olá uso ferramentas toolearn como os usuários usar seu serviço.</span><span class="sxs-lookup"><span data-stu-id="4e1ad-138">If you already send custom events or page views, explore hello Usage tools toolearn how users use your service.</span></span>
    - [<span data-ttu-id="4e1ad-139">Usuários, Sessões, Eventos</span><span class="sxs-lookup"><span data-stu-id="4e1ad-139">Users, Sessions, Events</span></span>](app-insights-usage-segmentation.md)
    - [<span data-ttu-id="4e1ad-140">Funis</span><span class="sxs-lookup"><span data-stu-id="4e1ad-140">Funnels</span></span>](usage-funnels.md)
    - [<span data-ttu-id="4e1ad-141">Fluxos de Usuário</span><span class="sxs-lookup"><span data-stu-id="4e1ad-141">User Flows</span></span>](app-insights-usage-flows.md)
    - [<span data-ttu-id="4e1ad-142">Pastas de trabalho</span><span class="sxs-lookup"><span data-stu-id="4e1ad-142">Workbooks</span></span>](app-insights-usage-workbooks.md)
    - [<span data-ttu-id="4e1ad-143">Adicionar contexto de usuário</span><span class="sxs-lookup"><span data-stu-id="4e1ad-143">Add user context</span></span>](app-insights-usage-send-user-context.md)


