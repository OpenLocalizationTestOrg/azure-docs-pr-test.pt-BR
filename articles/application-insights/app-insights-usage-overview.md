---
title: "Análise de uso para aplicativos Web com o Azure Application Insights | Microsoft Docs"
description: "Compreenda seus usuários e o que eles fazem com seu aplicativo Web."
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
ms.openlocfilehash: 63b74399790b718e14a5b6e09bc009a336caf928
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="usage-analysis-for-web-applications-with-application-insights"></a><span data-ttu-id="b0729-103">Análise de uso para aplicativos Web com o Application Insights</span><span class="sxs-lookup"><span data-stu-id="b0729-103">Usage analysis for web applications with Application Insights</span></span>

<span data-ttu-id="b0729-104">Quais recursos de seu aplicativo Web são mais populares?</span><span class="sxs-lookup"><span data-stu-id="b0729-104">Which features of your web app are most popular?</span></span> <span data-ttu-id="b0729-105">Os usuários atingem as metas deles com seu aplicativo?</span><span class="sxs-lookup"><span data-stu-id="b0729-105">Do your users achieve their goals with your app?</span></span> <span data-ttu-id="b0729-106">Eles deixam o aplicativo em determinados pontos? E retornam posteriormente?</span><span class="sxs-lookup"><span data-stu-id="b0729-106">Do they drop out at particular points, and do they return later?</span></span>  <span data-ttu-id="b0729-107">O [Application Insights do Azure](app-insights-overview.md) ajuda você a ter insights profundos sobre como as pessoas usam seu aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="b0729-107">[Azure Application Insights](app-insights-overview.md) helps you gain powerful insights into how people use your web app.</span></span> <span data-ttu-id="b0729-108">Sempre que atualiza seu aplicativo, você pode avaliar como ele funciona para os usuários.</span><span class="sxs-lookup"><span data-stu-id="b0729-108">Every time you update your app, you can assess how well it works for users.</span></span> <span data-ttu-id="b0729-109">Com esse conhecimento, você pode tomar decisões baseadas em dados sobre os próximos ciclos de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="b0729-109">With this knowledge, you can make data driven decisions about your next development cycles.</span></span>

## <a name="send-telemetry-from-your-app"></a><span data-ttu-id="b0729-110">Enviar telemetria de seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="b0729-110">Send telemetry from your app</span></span>

<span data-ttu-id="b0729-111">A melhor experiência é obtida, instalando o Application Insights tanto no código do servidor de aplicativos como nas suas páginas da Web.</span><span class="sxs-lookup"><span data-stu-id="b0729-111">The best experience is obtained by installing Application Insights both in your app server code, and in your web pages.</span></span> <span data-ttu-id="b0729-112">Os componentes do servidor e cliente do aplicativo retornam telemetria aoo portal Azure para análise.</span><span class="sxs-lookup"><span data-stu-id="b0729-112">The client and server components of your app send telemetry back to the Azure portal for analysis.</span></span>

1. <span data-ttu-id="b0729-113">**Código do servidor:** Instale o módulo apropriado para o [ASP.NET](app-insights-asp-net.md), [Azure](app-insights-azure.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md) ou [outro](app-insights-platforms.md) aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b0729-113">**Server code:** Install the appropriate module for your [ASP.NET](app-insights-asp-net.md), [Azure](app-insights-azure.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md), or [other](app-insights-platforms.md) app.</span></span>

    * <span data-ttu-id="b0729-114">*Não quer instalar o código do servidor? Apenas [crie um recurso do Azure Application Insights](app-insights-create-new-resource.md).*</span><span class="sxs-lookup"><span data-stu-id="b0729-114">*Don't want to install server code? Just [create an Azure Application Insights resource](app-insights-create-new-resource.md).*</span></span>

2. <span data-ttu-id="b0729-115"> **Código de página da Web:** Abra o [Portal do Azure](https://portal.azure.com), abra o recurso do Application Insights para seu aplicativo e abra o **Introdução > Monitorar e diagnosticar aplicativos do lado do cliente**.</span><span class="sxs-lookup"><span data-stu-id="b0729-115">**Web page code:** Open the [Azure portal](https://portal.azure.com), open the Application Insights resource for your app, and then open **Getting Started > Monitor and Diagnose Client-Side**.</span></span> 

    ![Copie o script no cabeçalho da página da web mestra.](./media/app-insights-usage-overview/02-monitor-web-page.png)


3. <span data-ttu-id="b0729-117">**Obter telemetria:** Execute seu projeto no modo de depuração por alguns minutos e, em seguida, procure resultados na folha Visão Geral em Application Insights.</span><span class="sxs-lookup"><span data-stu-id="b0729-117">**Get telemetry:** Run your project in debug mode for a few minutes, and then look for results in the Overview blade in Application Insights.</span></span>

    <span data-ttu-id="b0729-118">Publique seu aplicativo para monitorar o desempenho do aplicativo e descobrir o que seus usuários estão fazendo com o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b0729-118">Publish your app to monitor your app's performance and find out what your users are doing with your app.</span></span>

## <a name="include-user-and-session-id-in-your-telemetry"></a><span data-ttu-id="b0729-119">Incluir a ID de usuário e de sessão em sua telemetria</span><span class="sxs-lookup"><span data-stu-id="b0729-119">Include user and session ID in your telemetry</span></span>
<span data-ttu-id="b0729-120">Para controlar os usuários ao longo do tempo, o Application Insights requer um modo para identificá-los.</span><span class="sxs-lookup"><span data-stu-id="b0729-120">To track users over time, Application Insights requires a way to identify them.</span></span> <span data-ttu-id="b0729-121">A ferramenta Eventos é a única ferramenta de Uso que não requer uma ID de usuário ou uma ID de sessão.</span><span class="sxs-lookup"><span data-stu-id="b0729-121">The Events tool is the only Usage tool that does not require a user ID or a session ID.</span></span>

<span data-ttu-id="b0729-122">Comece a enviar essas IDs [aqui](https://docs.microsoft.com/azure/application-insights/app-insights-usage-send-user-context).</span><span class="sxs-lookup"><span data-stu-id="b0729-122">Start sending these IDs [here](https://docs.microsoft.com/azure/application-insights/app-insights-usage-send-user-context).</span></span>

## <a name="explore-usage-demographics-and-statistics"></a><span data-ttu-id="b0729-123">Explore as estatísticas e dados demográficos de uso</span><span class="sxs-lookup"><span data-stu-id="b0729-123">Explore usage demographics and statistics</span></span>
<span data-ttu-id="b0729-124">Descubra quando as pessoas usam seu aplicativo, em quais páginas elas estão mais interessadas, onde os usuários estão localizados e quais navegadores e sistemas operacionais eles usam.</span><span class="sxs-lookup"><span data-stu-id="b0729-124">Find out when people use your app, what pages they're most interested in, where your users are located, what browsers and operating systems they use.</span></span> 

<span data-ttu-id="b0729-125">Os relatórios de Usuários e Sessões filtram seus dados por páginas ou eventos personalizados e os segmentam segundo as propriedades, como local, ambiente e página.</span><span class="sxs-lookup"><span data-stu-id="b0729-125">The Users and Sessions reports filter your data by pages or custom events, and segment them by properties such as location, environment, and page.</span></span> <span data-ttu-id="b0729-126">Você também pode adicionar seus próprios filtros.</span><span class="sxs-lookup"><span data-stu-id="b0729-126">You can also add your own filters.</span></span>

![Usuários](./media/app-insights-usage-overview/users.png)  

<span data-ttu-id="b0729-128">Os insights à direita indicam padrões interessantes no conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="b0729-128">Insights on the right point out interesting patterns in the set of data.</span></span>  

* <span data-ttu-id="b0729-129">O relatório **Usuários** conta o número de usuários exclusivos que acessam suas páginas nos períodos escolhidos.</span><span class="sxs-lookup"><span data-stu-id="b0729-129">The **Users** report counts the numbers of unique users that access your pages within your chosen time periods.</span></span> <span data-ttu-id="b0729-130">(Os usuários são contados usando cookies.</span><span class="sxs-lookup"><span data-stu-id="b0729-130">(Users are counted by using cookies.</span></span> <span data-ttu-id="b0729-131">Se alguém acessar seu site usando computadores cliente ou navegadores diferentes ou limpar os cookies, essa pessoa será contada mais de uma vez.)</span><span class="sxs-lookup"><span data-stu-id="b0729-131">If someone accesses your site with different browsers or client machines, or clears their cookies, then they will be counted more than once.)</span></span>
* <span data-ttu-id="b0729-132">O relatório **Sessões** conta o número de sessões dos usuários que acessam seu site.</span><span class="sxs-lookup"><span data-stu-id="b0729-132">The **Sessions** report counts the number of user sessions that access your site.</span></span> <span data-ttu-id="b0729-133">Uma sessão é um período de atividade de um usuário, encerrada por um período de inatividade de mais de meia hora.</span><span class="sxs-lookup"><span data-stu-id="b0729-133">A session is a period of activity by a user, terminated by a period of inactivity of more than half an hour.</span></span>

[<span data-ttu-id="b0729-134">Mais informações sobre as ferramentas Usuários, Sessões e Eventos</span><span class="sxs-lookup"><span data-stu-id="b0729-134">More about the Users, Sessions, and Events tools</span></span>](app-insights-usage-segmentation.md)  

## <a name="page-views"></a><span data-ttu-id="b0729-135">Visualizações de página</span><span class="sxs-lookup"><span data-stu-id="b0729-135">Page views</span></span>

<span data-ttu-id="b0729-136">Na folha de Uso, clique no bloco de Visualizações de Página para obter uma análise das suas páginas mais populares:</span><span class="sxs-lookup"><span data-stu-id="b0729-136">From the Usage blade, click through the Page Views tile to get a breakdown of your most popular pages:</span></span>

![Na folha Visão Geral, clicar no gráfico Visualizações de página](./media/app-insights-usage-overview/05-games.png)

<span data-ttu-id="b0729-138">O exemplo acima é de um site da Web.</span><span class="sxs-lookup"><span data-stu-id="b0729-138">The example above is from a games web site.</span></span> <span data-ttu-id="b0729-139">A partir dos gráficos, imediatamente podemos ver:</span><span class="sxs-lookup"><span data-stu-id="b0729-139">From the charts, we can instantly see:</span></span>

* <span data-ttu-id="b0729-140">O uso não melhorou na última semana.</span><span class="sxs-lookup"><span data-stu-id="b0729-140">Usage hasn't improved in the past week.</span></span> <span data-ttu-id="b0729-141">Talvez devamos pensar em otimização do mecanismo de pesquisa?</span><span class="sxs-lookup"><span data-stu-id="b0729-141">Maybe we should think about search engine optimization?</span></span>
* <span data-ttu-id="b0729-142">Tênis é a página de jogo mais popular.</span><span class="sxs-lookup"><span data-stu-id="b0729-142">Tennis is the most popular game page.</span></span> <span data-ttu-id="b0729-143">Vamos manter o foco em melhorias adicionais para esta página.</span><span class="sxs-lookup"><span data-stu-id="b0729-143">Let's focus on further improvements to this page.</span></span>
* <span data-ttu-id="b0729-144">Em média, os usuários visitam a página Tênis aproximadamente três vezes por semana.</span><span class="sxs-lookup"><span data-stu-id="b0729-144">On average, users visit the Tennis page about three times per week.</span></span> <span data-ttu-id="b0729-145">(Há cerca de três vezes mais sessões do que usuários.)</span><span class="sxs-lookup"><span data-stu-id="b0729-145">(There are about three times more sessions than users.)</span></span>
* <span data-ttu-id="b0729-146">A maioria dos usuários visita o site durante a semana de trabalho dos EUA e, em horário de trabalho.</span><span class="sxs-lookup"><span data-stu-id="b0729-146">Most users visit the site during the U.S. working week, and in working hours.</span></span> <span data-ttu-id="b0729-147">Talvez devêssemos fornecer um botão "ocultar rápido" na página da Web.</span><span class="sxs-lookup"><span data-stu-id="b0729-147">Perhaps we should provide a "quick hide" button on the web page.</span></span>
* <span data-ttu-id="b0729-148">As [anotações](app-insights-annotations.md) no gráfico mostram quando novas versões do site foram implantadas.</span><span class="sxs-lookup"><span data-stu-id="b0729-148">The [annotations](app-insights-annotations.md) on the chart show when new versions of the website were deployed.</span></span> <span data-ttu-id="b0729-149">Nenhuma das implantações recentes teve um efeito notável no uso.</span><span class="sxs-lookup"><span data-stu-id="b0729-149">None of the recent deployments had a noticeable effect on usage.</span></span>

<span data-ttu-id="b0729-150">E se você quiser investigar o tráfego em seu site com mais detalhes, por exemplo, dividindo segundo uma propriedade personalizada que o site envia em sua telemetria de exibições de página?</span><span class="sxs-lookup"><span data-stu-id="b0729-150">What if you want to investigate the traffic to your site in more detail, like splitting by a custom property your site sends in its page view telemetry?</span></span>

1. <span data-ttu-id="b0729-151">Abra a ferramenta **Eventos** no menu de recursos do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="b0729-151">Open the **Events** tool in the Application Insights resource menu.</span></span> <span data-ttu-id="b0729-152">Essa ferramenta permite analisar quantas exibições de página e eventos personalizados foram enviados de seu aplicativo, com base em uma variedade de opções de filtragem, divisão em coortes e segmentação.</span><span class="sxs-lookup"><span data-stu-id="b0729-152">This tool lets you analyze how many page views and custom events were sent from your app, based on a variety of filtering, cohorting, and segmentation options.</span></span>
2. <span data-ttu-id="b0729-153">No menu suspenso "Quem usou", selecione "Qualquer exibição de página".</span><span class="sxs-lookup"><span data-stu-id="b0729-153">In the "Who used" dropdown, select "Any Page View".</span></span>
3. <span data-ttu-id="b0729-154">No menu suspenso "Dividir por", selecione uma propriedade segundo a qual deseja dividir sua telemetria de exibição de página.</span><span class="sxs-lookup"><span data-stu-id="b0729-154">In the "Split by" dropdown, select a property by which to split your page view telemetry.</span></span>

## <a name="retention---how-many-users-come-back"></a><span data-ttu-id="b0729-155">Retenção – quantos usuários voltam?</span><span class="sxs-lookup"><span data-stu-id="b0729-155">Retention - how many users come back?</span></span>

<span data-ttu-id="b0729-156">A retenção o ajuda a entender com que frequência os usuários voltam para usar o aplicativo, com base em coortes de usuários que executaram alguma ação de negócios durante um determinado bucket de tempo.</span><span class="sxs-lookup"><span data-stu-id="b0729-156">Retention helps you understand how often your users return to use their app, based on cohorts of users that performed some business action during a certain time bucket.</span></span> 

- <span data-ttu-id="b0729-157">Entenda quais recursos específicos fazem com que alguns usuários voltem mais que outros</span><span class="sxs-lookup"><span data-stu-id="b0729-157">Understand what specific features cause users to come back more than others</span></span> 
- <span data-ttu-id="b0729-158">Forme hipóteses com base em dados de usuários reais</span><span class="sxs-lookup"><span data-stu-id="b0729-158">Form hypotheses based on real user data</span></span> 
- <span data-ttu-id="b0729-159">Determine se a retenção é um problema para seu produto</span><span class="sxs-lookup"><span data-stu-id="b0729-159">Determine whether retention is a problem in your product</span></span> 

![Retenção](./media/app-insights-usage-overview/retention.png) 

<span data-ttu-id="b0729-161">Os controles de retenção na parte superior permitem que você defina eventos específicos o intervalo de tempo para calcular a retenção.</span><span class="sxs-lookup"><span data-stu-id="b0729-161">The retention controls on top allow you to define specific events and time range to calculate retention.</span></span> <span data-ttu-id="b0729-162">O gráfico no meio fornece uma representação visual do percentual geral de retenção, segundo o intervalo de tempo especificado.</span><span class="sxs-lookup"><span data-stu-id="b0729-162">The graph in the middle gives a visual representation of the overall retention percentage by the time range specified.</span></span> <span data-ttu-id="b0729-163">O gráfico na parte inferior representa a retenção individual em um determinado período.</span><span class="sxs-lookup"><span data-stu-id="b0729-163">The graph on the bottom represents individual retention in a given time period.</span></span> <span data-ttu-id="b0729-164">Esse nível de detalhamento permite entender o que os usuários estão fazendo e o que pode afetar usuários que retornam com uma granularidade mais detalhada.</span><span class="sxs-lookup"><span data-stu-id="b0729-164">This level of detail allows you to understand what your users are doing and what might affect returning users on a more detailed granularity.</span></span>  

[<span data-ttu-id="b0729-165">Mais informações sobre a ferramenta de Retenção</span><span class="sxs-lookup"><span data-stu-id="b0729-165">More about the Retention tool</span></span>](app-insights-usage-retention.md)

## <a name="custom-business-events"></a><span data-ttu-id="b0729-166">Eventos de negócios personalizados</span><span class="sxs-lookup"><span data-stu-id="b0729-166">Custom business events</span></span>

<span data-ttu-id="b0729-167">Para ter uma compreensão clara do que os usuários fazem com seu aplicativo Web, é útil inserir linhas de código para registrar eventos personalizados.</span><span class="sxs-lookup"><span data-stu-id="b0729-167">To get a clear understanding of what users do with your web app, it's useful to insert lines of code to log custom events.</span></span> <span data-ttu-id="b0729-168">Esses eventos podem controlar qualquer coisa, desde ações detalhadas do usuário, como clicar em botões específicos, até eventos de negócios mais significativos, como fazer uma compra ou vencer um jogo.</span><span class="sxs-lookup"><span data-stu-id="b0729-168">These events can track anything from detailed user actions such as clicking specific buttons, to more significant business events such as making a purchase or winning a game.</span></span> 

<span data-ttu-id="b0729-169">Embora em alguns casos as exibições de página possam representar eventos úteis, de modo geral não é esse o caso.</span><span class="sxs-lookup"><span data-stu-id="b0729-169">Although in some cases, page views can represent useful events, it isn't true in general.</span></span> <span data-ttu-id="b0729-170">Um usuário pode abrir uma página de produto sem adquirir o produto.</span><span class="sxs-lookup"><span data-stu-id="b0729-170">A user can open a product page without buying the product.</span></span> 

<span data-ttu-id="b0729-171">Com eventos de negócios específicos, você pode traçar um gráfico do progresso do dos usuários em seu site.</span><span class="sxs-lookup"><span data-stu-id="b0729-171">With specific business events, you can chart your users' progress through your site.</span></span> <span data-ttu-id="b0729-172">Você pode descobrir as preferências deles com relação a diferentes opções e quando eles desistem ou têm dificuldades.</span><span class="sxs-lookup"><span data-stu-id="b0729-172">You can find out their preferences for different options, and where they drop out or have difficulties.</span></span> <span data-ttu-id="b0729-173">Com esse conhecimento, é possível tomar decisões informadas sobre as prioridades em sua lista de pendências de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="b0729-173">With this knowledge, you can make informed decisions about the priorities in your development backlog.</span></span>

<span data-ttu-id="b0729-174">Eventos podem ser registrados na página da Web:</span><span class="sxs-lookup"><span data-stu-id="b0729-174">Events can be logged in the web page:</span></span>

```JavaScript

    appInsights.trackEvent("ExpandDetailTab", {DetailTab: tabName});
```

<span data-ttu-id="b0729-175">Ou no lado do servidor do aplicativo Web:</span><span class="sxs-lookup"><span data-stu-id="b0729-175">Or in the server side of the web app:</span></span>

```C#
    var tc = new Microsoft.ApplicationInsights.TelemetryClient();
    tc.TrackEvent("CreatedAccount", new Dictionary<string,string> {"AccountType":account.Type}, null);
    ...
    tc.TrackEvent("AddedItemToCart", new Dictionary<string,string> {"Item":item.Name}, null);
    ...
    tc.TrackEvent("CompletedPurchase");
```

<span data-ttu-id="b0729-176">Você pode anexar valores de propriedade a esses eventos, para que possa filtrar ou dividir os eventos quando inspecioná-los no portal.</span><span class="sxs-lookup"><span data-stu-id="b0729-176">You can attach property values to these events, so that you can filter or split the events when you inspect them in the portal.</span></span> <span data-ttu-id="b0729-177">Além disso, um conjunto padrão de propriedades é anexado a cada evento, como a ID de usuário anônimo, que permite rastrear a sequência de atividades de um usuário individual.</span><span class="sxs-lookup"><span data-stu-id="b0729-177">In addition, a standard set of properties is attached to each event, such as anonymous user ID, which allows you to trace the sequence of activities of an individual user.</span></span>

<span data-ttu-id="b0729-178">Saiba mais sobre [eventos personalizados](app-insights-api-custom-events-metrics.md#trackevent) e [propriedades](app-insights-api-custom-events-metrics.md#properties).</span><span class="sxs-lookup"><span data-stu-id="b0729-178">Learn more about [custom events](app-insights-api-custom-events-metrics.md#trackevent) and [properties](app-insights-api-custom-events-metrics.md#properties).</span></span>

### <a name="slice-and-dice-events"></a><span data-ttu-id="b0729-179">Fatiar e dividir eventos</span><span class="sxs-lookup"><span data-stu-id="b0729-179">Slice and dice events</span></span>

<span data-ttu-id="b0729-180">Com as ferramentas de Usuários, Sessões e Eventos, você pode fatiar e dividir eventos personalizados segundo o usuário, o nome do evento e as propriedades.</span><span class="sxs-lookup"><span data-stu-id="b0729-180">In the Users, Sessions, and Events tools, you can slice and dice custom events by user, event name, and properties.</span></span>
<span data-ttu-id="b0729-181">![Usuários](./media/app-insights-usage-overview/users.png)</span><span class="sxs-lookup"><span data-stu-id="b0729-181">![Users](./media/app-insights-usage-overview/users.png)</span></span>  
  
## <a name="design-the-telemetry-with-the-app"></a><span data-ttu-id="b0729-182">Design de telemetria com o aplicativo</span><span class="sxs-lookup"><span data-stu-id="b0729-182">Design the telemetry with the app</span></span>

<span data-ttu-id="b0729-183">Quando estiver criando cada recurso do aplicativo, considere como você vai medir seu sucesso com os usuários.</span><span class="sxs-lookup"><span data-stu-id="b0729-183">When you are designing each feature of your app, consider how you are going to measure its success with your users.</span></span> <span data-ttu-id="b0729-184">Decida quais eventos de negócios você precisa registrar e codifique as chamadas de rastreamento para esses eventos em seu aplicativo desde o início.</span><span class="sxs-lookup"><span data-stu-id="b0729-184">Decide what business events you need to record, and code the tracking calls for those events into your app from the start.</span></span>

## <a name="a--b-testing"></a><span data-ttu-id="b0729-185">Testando A | B</span><span class="sxs-lookup"><span data-stu-id="b0729-185">A | B Testing</span></span>
<span data-ttu-id="b0729-186">Se você não souber qual variante de um recurso terá mais êxito, libere ambas, tornando cada uma acessível para diferentes usuários.</span><span class="sxs-lookup"><span data-stu-id="b0729-186">If you don't know which variant of a feature will be more successful, release both of them, making each accessible to different users.</span></span> <span data-ttu-id="b0729-187">Avalie o sucesso de cada uma e então parta para uma versão unificada.</span><span class="sxs-lookup"><span data-stu-id="b0729-187">Measure the success of each, and then move to a unified version.</span></span>

<span data-ttu-id="b0729-188">Para essa técnica, você anexa valores de propriedade distintos para toda a telemetria que é enviada por cada versão do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b0729-188">For this technique, you attach distinct property values to all the telemetry that is sent by each version of your app.</span></span> <span data-ttu-id="b0729-189">Você pode fazer isso definindo propriedades no TelemetryContext ativo.</span><span class="sxs-lookup"><span data-stu-id="b0729-189">You can do that by defining properties in the active TelemetryContext.</span></span> <span data-ttu-id="b0729-190">Essas propriedades padrão são adicionadas a todas as mensagens de telemetria que o aplicativo envia - não apenas a suas mensagens personalizadas, mas também à telemetria padrão.</span><span class="sxs-lookup"><span data-stu-id="b0729-190">These default properties are added to every telemetry message that the application sends - not just your custom messages, but the standard telemetry as well.</span></span>

<span data-ttu-id="b0729-191">No portal do Application Insights, filtre e divida seus dados segundo os valores da propriedade, de modo a comparar as diferentes versões.</span><span class="sxs-lookup"><span data-stu-id="b0729-191">In the Application Insights portal, filter and split your data on the property values, so as to compare the different versions.</span></span>

<span data-ttu-id="b0729-192">Para fazer isso, [configure um inicializador de telemetria](app-insights-api-filtering-sampling.md##add-properties-itelemetryinitializer):</span><span class="sxs-lookup"><span data-stu-id="b0729-192">To do this, [set up a telemetry initializer](app-insights-api-filtering-sampling.md##add-properties-itelemetryinitializer):</span></span>

```C#


    // Telemetry initializer class
    public class MyTelemetryInitializer : ITelemetryInitializer
    {
        public void Initialize (ITelemetry telemetry)
        {
            telemetry.Properties["AppVersion"] = "v2.1";
        }
    }
```

<span data-ttu-id="b0729-193">No inicializador do aplicativo Web, como Global.asax.cs:</span><span class="sxs-lookup"><span data-stu-id="b0729-193">In the web app initializer such as Global.asax.cs:</span></span>

```C#

    protected void Application_Start()
    {
        // ...
        TelemetryConfiguration.Active.TelemetryInitializers
        .Add(new MyTelemetryInitializer());
    }
```

<span data-ttu-id="b0729-194">Todos os novos TelemetryClients adicionam automaticamente o valor da propriedade que você especificar.</span><span class="sxs-lookup"><span data-stu-id="b0729-194">All new TelemetryClients automatically add the property value you specify.</span></span> <span data-ttu-id="b0729-195">Eventos de telemetria individuais podem substituir os valores padrão.</span><span class="sxs-lookup"><span data-stu-id="b0729-195">Individual telemetry events can override the default values.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b0729-196">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b0729-196">Next steps</span></span>
   - [<span data-ttu-id="b0729-197">Usuários, Sessões, Eventos</span><span class="sxs-lookup"><span data-stu-id="b0729-197">Users, Sessions, Events</span></span>](app-insights-usage-segmentation.md)
   - [<span data-ttu-id="b0729-198">Funis</span><span class="sxs-lookup"><span data-stu-id="b0729-198">Funnels</span></span>](usage-funnels.md)
   - [<span data-ttu-id="b0729-199">Retenção</span><span class="sxs-lookup"><span data-stu-id="b0729-199">Retention</span></span>](app-insights-usage-retention.md)
   - [<span data-ttu-id="b0729-200">Fluxos de Usuário</span><span class="sxs-lookup"><span data-stu-id="b0729-200">User Flows</span></span>](app-insights-usage-flows.md)
   - [<span data-ttu-id="b0729-201">Pastas de trabalho</span><span class="sxs-lookup"><span data-stu-id="b0729-201">Workbooks</span></span>](app-insights-usage-workbooks.md)
   - [<span data-ttu-id="b0729-202">Adicionar contexto de usuário</span><span class="sxs-lookup"><span data-stu-id="b0729-202">Add user context</span></span>](app-insights-usage-send-user-context.md)
