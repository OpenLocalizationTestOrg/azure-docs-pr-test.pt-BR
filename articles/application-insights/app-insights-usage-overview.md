---
title: "análise de aaaUsage para aplicativos web com o Azure Application Insights | Documentos da Microsoft"
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
ms.openlocfilehash: f7f9173cf411fa0d2dfb3b5ba99134a02bbc0e89
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="usage-analysis-for-web-applications-with-application-insights"></a><span data-ttu-id="9f10b-103">Análise de uso para aplicativos Web com o Application Insights</span><span class="sxs-lookup"><span data-stu-id="9f10b-103">Usage analysis for web applications with Application Insights</span></span>

<span data-ttu-id="9f10b-104">Quais recursos de seu aplicativo Web são mais populares?</span><span class="sxs-lookup"><span data-stu-id="9f10b-104">Which features of your web app are most popular?</span></span> <span data-ttu-id="9f10b-105">Os usuários atingem as metas deles com seu aplicativo?</span><span class="sxs-lookup"><span data-stu-id="9f10b-105">Do your users achieve their goals with your app?</span></span> <span data-ttu-id="9f10b-106">Eles deixam o aplicativo em determinados pontos? E retornam posteriormente?</span><span class="sxs-lookup"><span data-stu-id="9f10b-106">Do they drop out at particular points, and do they return later?</span></span>  <span data-ttu-id="9f10b-107">O [Application Insights do Azure](app-insights-overview.md) ajuda você a ter insights profundos sobre como as pessoas usam seu aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="9f10b-107">[Azure Application Insights](app-insights-overview.md) helps you gain powerful insights into how people use your web app.</span></span> <span data-ttu-id="9f10b-108">Sempre que atualiza seu aplicativo, você pode avaliar como ele funciona para os usuários.</span><span class="sxs-lookup"><span data-stu-id="9f10b-108">Every time you update your app, you can assess how well it works for users.</span></span> <span data-ttu-id="9f10b-109">Com esse conhecimento, você pode tomar decisões baseadas em dados sobre os próximos ciclos de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="9f10b-109">With this knowledge, you can make data driven decisions about your next development cycles.</span></span>

## <a name="send-telemetry-from-your-app"></a><span data-ttu-id="9f10b-110">Enviar telemetria de seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="9f10b-110">Send telemetry from your app</span></span>

<span data-ttu-id="9f10b-111">melhor experiência de saudação é obtida com a instalação do Application Insights no código do servidor de aplicativo e nas páginas da web.</span><span class="sxs-lookup"><span data-stu-id="9f10b-111">hello best experience is obtained by installing Application Insights both in your app server code, and in your web pages.</span></span> <span data-ttu-id="9f10b-112">componentes de cliente e servidor de saudação do seu aplicativo enviam telemetria back toohello portal do Azure para análise.</span><span class="sxs-lookup"><span data-stu-id="9f10b-112">hello client and server components of your app send telemetry back toohello Azure portal for analysis.</span></span>

1. <span data-ttu-id="9f10b-113">**Código do servidor:** instalar módulo apropriado do Olá para sua [ASP.NET](app-insights-asp-net.md), [Azure](app-insights-azure.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md), ou [outros](app-insights-platforms.md) aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9f10b-113">**Server code:** Install hello appropriate module for your [ASP.NET](app-insights-asp-net.md), [Azure](app-insights-azure.md), [Java](app-insights-java-get-started.md), [Node.js](app-insights-nodejs.md), or [other](app-insights-platforms.md) app.</span></span>

    * <span data-ttu-id="9f10b-114">*Não quer que o código de servidor tooinstall? Apenas [crie um recurso do Azure Application Insights](app-insights-create-new-resource.md).*</span><span class="sxs-lookup"><span data-stu-id="9f10b-114">*Don't want tooinstall server code? Just [create an Azure Application Insights resource](app-insights-create-new-resource.md).*</span></span>

2. <span data-ttu-id="9f10b-115">**Código de página da Web:** abrir Olá [portal do Azure](https://portal.azure.com), abra o recurso do Application Insights Olá para seu aplicativo e, em seguida, abra **Introdução > monitorar e diagnosticar cliente**.</span><span class="sxs-lookup"><span data-stu-id="9f10b-115">**Web page code:** Open hello [Azure portal](https://portal.azure.com), open hello Application Insights resource for your app, and then open **Getting Started > Monitor and Diagnose Client-Side**.</span></span> 

    ![Copie o script hello para head Olá mestre da página da web.](./media/app-insights-usage-overview/02-monitor-web-page.png)


3. <span data-ttu-id="9f10b-117">**Obtenha telemetria:** executar seu projeto no modo de depuração por alguns minutos e, em seguida, procure os resultados na folha de visão geral de saudação no Application Insights.</span><span class="sxs-lookup"><span data-stu-id="9f10b-117">**Get telemetry:** Run your project in debug mode for a few minutes, and then look for results in hello Overview blade in Application Insights.</span></span>

    <span data-ttu-id="9f10b-118">Publicar seu aplicativo toomonitor desempenho do aplicativo e descobrir o que seus usuários estão fazendo com que seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9f10b-118">Publish your app toomonitor your app's performance and find out what your users are doing with your app.</span></span>

## <a name="include-user-and-session-id-in-your-telemetry"></a><span data-ttu-id="9f10b-119">Incluir a ID de usuário e de sessão em sua telemetria</span><span class="sxs-lookup"><span data-stu-id="9f10b-119">Include user and session ID in your telemetry</span></span>
<span data-ttu-id="9f10b-120">tootrack usuários ao longo do tempo, Application Insights requer uma maneira tooidentify-los.</span><span class="sxs-lookup"><span data-stu-id="9f10b-120">tootrack users over time, Application Insights requires a way tooidentify them.</span></span> <span data-ttu-id="9f10b-121">Eventos de Olá, ferramenta é Olá única ferramenta de uso que não requer uma ID de usuário ou uma ID de sessão.</span><span class="sxs-lookup"><span data-stu-id="9f10b-121">hello Events tool is hello only Usage tool that does not require a user ID or a session ID.</span></span>

<span data-ttu-id="9f10b-122">Comece a enviar essas IDs [aqui](https://docs.microsoft.com/azure/application-insights/app-insights-usage-send-user-context).</span><span class="sxs-lookup"><span data-stu-id="9f10b-122">Start sending these IDs [here](https://docs.microsoft.com/azure/application-insights/app-insights-usage-send-user-context).</span></span>

## <a name="explore-usage-demographics-and-statistics"></a><span data-ttu-id="9f10b-123">Explore as estatísticas e dados demográficos de uso</span><span class="sxs-lookup"><span data-stu-id="9f10b-123">Explore usage demographics and statistics</span></span>
<span data-ttu-id="9f10b-124">Descubra quando as pessoas usam seu aplicativo, em quais páginas elas estão mais interessadas, onde os usuários estão localizados e quais navegadores e sistemas operacionais eles usam.</span><span class="sxs-lookup"><span data-stu-id="9f10b-124">Find out when people use your app, what pages they're most interested in, where your users are located, what browsers and operating systems they use.</span></span> 

<span data-ttu-id="9f10b-125">relatórios de usuários e sessões Olá filtrar seus dados por páginas ou eventos personalizados e segmento-los por propriedades, como local, ambiente e página.</span><span class="sxs-lookup"><span data-stu-id="9f10b-125">hello Users and Sessions reports filter your data by pages or custom events, and segment them by properties such as location, environment, and page.</span></span> <span data-ttu-id="9f10b-126">Você também pode adicionar seus próprios filtros.</span><span class="sxs-lookup"><span data-stu-id="9f10b-126">You can also add your own filters.</span></span>

![Usuários](./media/app-insights-usage-overview/users.png)  

<span data-ttu-id="9f10b-128">Ideias sobre Olá direita destacar padrões interessantes no conjunto de saudação de dados.</span><span class="sxs-lookup"><span data-stu-id="9f10b-128">Insights on hello right point out interesting patterns in hello set of data.</span></span>  

* <span data-ttu-id="9f10b-129">Olá **usuários** relatório conta os números de saudação de usuários exclusivos que acessam as páginas em seu períodos de tempo escolhido.</span><span class="sxs-lookup"><span data-stu-id="9f10b-129">hello **Users** report counts hello numbers of unique users that access your pages within your chosen time periods.</span></span> <span data-ttu-id="9f10b-130">(Os usuários são contados usando cookies.</span><span class="sxs-lookup"><span data-stu-id="9f10b-130">(Users are counted by using cookies.</span></span> <span data-ttu-id="9f10b-131">Se alguém acessar seu site usando computadores cliente ou navegadores diferentes ou limpar os cookies, essa pessoa será contada mais de uma vez.)</span><span class="sxs-lookup"><span data-stu-id="9f10b-131">If someone accesses your site with different browsers or client machines, or clears their cookies, then they will be counted more than once.)</span></span>
* <span data-ttu-id="9f10b-132">Olá **sessões** relatório conta o número de saudação de sessões de usuário que acessar seu site.</span><span class="sxs-lookup"><span data-stu-id="9f10b-132">hello **Sessions** report counts hello number of user sessions that access your site.</span></span> <span data-ttu-id="9f10b-133">Uma sessão é um período de atividade de um usuário, encerrada por um período de inatividade de mais de meia hora.</span><span class="sxs-lookup"><span data-stu-id="9f10b-133">A session is a period of activity by a user, terminated by a period of inactivity of more than half an hour.</span></span>

[<span data-ttu-id="9f10b-134">Mais sobre as ferramentas de usuários, sessões e eventos Olá</span><span class="sxs-lookup"><span data-stu-id="9f10b-134">More about hello Users, Sessions, and Events tools</span></span>](app-insights-usage-segmentation.md)  

## <a name="page-views"></a><span data-ttu-id="9f10b-135">Visualizações de página</span><span class="sxs-lookup"><span data-stu-id="9f10b-135">Page views</span></span>

<span data-ttu-id="9f10b-136">Na folha de uso de saudação, clique nas Olá modos de exibição de página bloco tooget uma análise das páginas mais populares:</span><span class="sxs-lookup"><span data-stu-id="9f10b-136">From hello Usage blade, click through hello Page Views tile tooget a breakdown of your most popular pages:</span></span>

![Na folha de visão geral de saudação, clique em Olá gráfico de modos de exibição de página](./media/app-insights-usage-overview/05-games.png)

<span data-ttu-id="9f10b-138">exemplo Hello acima é de um site de jogos.</span><span class="sxs-lookup"><span data-stu-id="9f10b-138">hello example above is from a games web site.</span></span> <span data-ttu-id="9f10b-139">Gráficos de hello, podemos instantaneamente ver:</span><span class="sxs-lookup"><span data-stu-id="9f10b-139">From hello charts, we can instantly see:</span></span>

* <span data-ttu-id="9f10b-140">Uso não melhorou em Olá semana passada.</span><span class="sxs-lookup"><span data-stu-id="9f10b-140">Usage hasn't improved in hello past week.</span></span> <span data-ttu-id="9f10b-141">Talvez devamos pensar em otimização do mecanismo de pesquisa?</span><span class="sxs-lookup"><span data-stu-id="9f10b-141">Maybe we should think about search engine optimization?</span></span>
* <span data-ttu-id="9f10b-142">Tênis é Olá página de jogo mais popular.</span><span class="sxs-lookup"><span data-stu-id="9f10b-142">Tennis is hello most popular game page.</span></span> <span data-ttu-id="9f10b-143">Vamos nos concentrar na página de toothis melhorias adicionais.</span><span class="sxs-lookup"><span data-stu-id="9f10b-143">Let's focus on further improvements toothis page.</span></span>
* <span data-ttu-id="9f10b-144">Em média, os usuários visitam Olá Tênis página cerca de três vezes por semana.</span><span class="sxs-lookup"><span data-stu-id="9f10b-144">On average, users visit hello Tennis page about three times per week.</span></span> <span data-ttu-id="9f10b-145">(Há cerca de três vezes mais sessões do que usuários.)</span><span class="sxs-lookup"><span data-stu-id="9f10b-145">(There are about three times more sessions than users.)</span></span>
* <span data-ttu-id="9f10b-146">A maioria dos usuários visite o site de saudação durante a semana de trabalho Olá dos Estados Unidos e no horário de trabalho.</span><span class="sxs-lookup"><span data-stu-id="9f10b-146">Most users visit hello site during hello U.S. working week, and in working hours.</span></span> <span data-ttu-id="9f10b-147">Talvez, deve fornecer um botão "Ocultar rápida" na página da web de saudação.</span><span class="sxs-lookup"><span data-stu-id="9f10b-147">Perhaps we should provide a "quick hide" button on hello web page.</span></span>
* <span data-ttu-id="9f10b-148">Olá [anotações](app-insights-annotations.md) em gráfico Olá Mostrar quando novas versões do site Olá foram implantadas.</span><span class="sxs-lookup"><span data-stu-id="9f10b-148">hello [annotations](app-insights-annotations.md) on hello chart show when new versions of hello website were deployed.</span></span> <span data-ttu-id="9f10b-149">Nenhuma das implantações recentes Olá tinha um efeito significativo no uso.</span><span class="sxs-lookup"><span data-stu-id="9f10b-149">None of hello recent deployments had a noticeable effect on usage.</span></span>

<span data-ttu-id="9f10b-150">Se quiser que o site de tooyour de tráfego tooinvestigate hello mais detalhadamente, como divisão por uma propriedade personalizada que envia seu site em sua telemetria de exibição de página?</span><span class="sxs-lookup"><span data-stu-id="9f10b-150">What if you want tooinvestigate hello traffic tooyour site in more detail, like splitting by a custom property your site sends in its page view telemetry?</span></span>

1. <span data-ttu-id="9f10b-151">Olá abrir **eventos** ferramenta no menu de recurso do Application Insights hello.</span><span class="sxs-lookup"><span data-stu-id="9f10b-151">Open hello **Events** tool in hello Application Insights resource menu.</span></span> <span data-ttu-id="9f10b-152">Essa ferramenta permite analisar quantas exibições de página e eventos personalizados foram enviados de seu aplicativo, com base em uma variedade de opções de filtragem, divisão em coortes e segmentação.</span><span class="sxs-lookup"><span data-stu-id="9f10b-152">This tool lets you analyze how many page views and custom events were sent from your app, based on a variety of filtering, cohorting, and segmentation options.</span></span>
2. <span data-ttu-id="9f10b-153">No hello "Que usado" suspensa, selecione "Qualquer exibição da página".</span><span class="sxs-lookup"><span data-stu-id="9f10b-153">In hello "Who used" dropdown, select "Any Page View".</span></span>
3. <span data-ttu-id="9f10b-154">No menu suspenso de "Divisão por" Olá, selecione uma propriedade pela qual toosplit sua página Exibir telemetria.</span><span class="sxs-lookup"><span data-stu-id="9f10b-154">In hello "Split by" dropdown, select a property by which toosplit your page view telemetry.</span></span>

## <a name="retention---how-many-users-come-back"></a><span data-ttu-id="9f10b-155">Retenção – quantos usuários voltam?</span><span class="sxs-lookup"><span data-stu-id="9f10b-155">Retention - how many users come back?</span></span>

<span data-ttu-id="9f10b-156">Retenção ajuda a entender a frequência na qual os usuários retornarem toouse seu aplicativo, com base em colaboradores de usuários que executou alguma ação de negócios durante um bucket de tempo determinado.</span><span class="sxs-lookup"><span data-stu-id="9f10b-156">Retention helps you understand how often your users return toouse their app, based on cohorts of users that performed some business action during a certain time bucket.</span></span> 

- <span data-ttu-id="9f10b-157">Entender quais recursos específicos com que os usuários toocome back mais do que outras pessoas</span><span class="sxs-lookup"><span data-stu-id="9f10b-157">Understand what specific features cause users toocome back more than others</span></span> 
- <span data-ttu-id="9f10b-158">Forme hipóteses com base em dados de usuários reais</span><span class="sxs-lookup"><span data-stu-id="9f10b-158">Form hypotheses based on real user data</span></span> 
- <span data-ttu-id="9f10b-159">Determine se a retenção é um problema para seu produto</span><span class="sxs-lookup"><span data-stu-id="9f10b-159">Determine whether retention is a problem in your product</span></span> 

![Retenção](./media/app-insights-usage-overview/retention.png) 

<span data-ttu-id="9f10b-161">controles de retenção de saudação na parte superior permitem que você toodefine eventos específicos e retenção de toocalculate de intervalo de tempo.</span><span class="sxs-lookup"><span data-stu-id="9f10b-161">hello retention controls on top allow you toodefine specific events and time range toocalculate retention.</span></span> <span data-ttu-id="9f10b-162">gráfico no meio Olá Olá fornece uma representação visual de saudação porcentagem total de retenção por Olá intervalo de tempo especificado.</span><span class="sxs-lookup"><span data-stu-id="9f10b-162">hello graph in hello middle gives a visual representation of hello overall retention percentage by hello time range specified.</span></span> <span data-ttu-id="9f10b-163">gráfico de saudação inferior Olá representa retenção individual em um determinado período de tempo.</span><span class="sxs-lookup"><span data-stu-id="9f10b-163">hello graph on hello bottom represents individual retention in a given time period.</span></span> <span data-ttu-id="9f10b-164">Esse nível de detalhe permite que você toounderstand que seus usuários estão fazendo e o que pode afetar usuários retorno em uma granularidade mais detalhada.</span><span class="sxs-lookup"><span data-stu-id="9f10b-164">This level of detail allows you toounderstand what your users are doing and what might affect returning users on a more detailed granularity.</span></span>  

[<span data-ttu-id="9f10b-165">Mais informações sobre a ferramenta de retenção Olá</span><span class="sxs-lookup"><span data-stu-id="9f10b-165">More about hello Retention tool</span></span>](app-insights-usage-retention.md)

## <a name="custom-business-events"></a><span data-ttu-id="9f10b-166">Eventos de negócios personalizados</span><span class="sxs-lookup"><span data-stu-id="9f10b-166">Custom business events</span></span>

<span data-ttu-id="9f10b-167">uma compreensão clara de que os usuários de tooget fazer com o seu aplicativo web, é útil tooinsert linhas de eventos personalizados do código toolog.</span><span class="sxs-lookup"><span data-stu-id="9f10b-167">tooget a clear understanding of what users do with your web app, it's useful tooinsert lines of code toolog custom events.</span></span> <span data-ttu-id="9f10b-168">Esses eventos podem controlar qualquer coisa detalhadas de ações de usuário, como clicar nos botões específicos, eventos de negócios significativa toomore como efetuar uma compra ou vencer um jogo.</span><span class="sxs-lookup"><span data-stu-id="9f10b-168">These events can track anything from detailed user actions such as clicking specific buttons, toomore significant business events such as making a purchase or winning a game.</span></span> 

<span data-ttu-id="9f10b-169">Embora em alguns casos as exibições de página possam representar eventos úteis, de modo geral não é esse o caso.</span><span class="sxs-lookup"><span data-stu-id="9f10b-169">Although in some cases, page views can represent useful events, it isn't true in general.</span></span> <span data-ttu-id="9f10b-170">Um usuário pode abrir uma página de produto sem adquirir o produto hello.</span><span class="sxs-lookup"><span data-stu-id="9f10b-170">A user can open a product page without buying hello product.</span></span> 

<span data-ttu-id="9f10b-171">Com eventos de negócios específicos, você pode traçar um gráfico do progresso do dos usuários em seu site.</span><span class="sxs-lookup"><span data-stu-id="9f10b-171">With specific business events, you can chart your users' progress through your site.</span></span> <span data-ttu-id="9f10b-172">Você pode descobrir as preferências deles com relação a diferentes opções e quando eles desistem ou têm dificuldades.</span><span class="sxs-lookup"><span data-stu-id="9f10b-172">You can find out their preferences for different options, and where they drop out or have difficulties.</span></span> <span data-ttu-id="9f10b-173">Com esse conhecimento, você pode tomar decisões informadas sobre prioridades Olá na sua lista de pendências de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="9f10b-173">With this knowledge, you can make informed decisions about hello priorities in your development backlog.</span></span>

<span data-ttu-id="9f10b-174">Eventos podem ser registrados na página da web de saudação:</span><span class="sxs-lookup"><span data-stu-id="9f10b-174">Events can be logged in hello web page:</span></span>

```JavaScript

    appInsights.trackEvent("ExpandDetailTab", {DetailTab: tabName});
```

<span data-ttu-id="9f10b-175">Ou, no lado do servidor de saudação do aplicativo web de saudação:</span><span class="sxs-lookup"><span data-stu-id="9f10b-175">Or in hello server side of hello web app:</span></span>

```C#
    var tc = new Microsoft.ApplicationInsights.TelemetryClient();
    tc.TrackEvent("CreatedAccount", new Dictionary<string,string> {"AccountType":account.Type}, null);
    ...
    tc.TrackEvent("AddedItemToCart", new Dictionary<string,string> {"Item":item.Name}, null);
    ...
    tc.TrackEvent("CompletedPurchase");
```

<span data-ttu-id="9f10b-176">Você pode anexar eventos de toothese de valores de propriedade, para que você pode filtrar ou dividir eventos hello quando inspecioná-los no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="9f10b-176">You can attach property values toothese events, so that you can filter or split hello events when you inspect them in hello portal.</span></span> <span data-ttu-id="9f10b-177">Além disso, um conjunto padrão de propriedades é o evento tooeach anexado, como ID de usuário anônimo, que permite que você tootrace sequência de saudação de atividades de um usuário individual.</span><span class="sxs-lookup"><span data-stu-id="9f10b-177">In addition, a standard set of properties is attached tooeach event, such as anonymous user ID, which allows you tootrace hello sequence of activities of an individual user.</span></span>

<span data-ttu-id="9f10b-178">Saiba mais sobre [eventos personalizados](app-insights-api-custom-events-metrics.md#trackevent) e [propriedades](app-insights-api-custom-events-metrics.md#properties).</span><span class="sxs-lookup"><span data-stu-id="9f10b-178">Learn more about [custom events](app-insights-api-custom-events-metrics.md#trackevent) and [properties](app-insights-api-custom-events-metrics.md#properties).</span></span>

### <a name="slice-and-dice-events"></a><span data-ttu-id="9f10b-179">Fatiar e dividir eventos</span><span class="sxs-lookup"><span data-stu-id="9f10b-179">Slice and dice events</span></span>

<span data-ttu-id="9f10b-180">Em ferramentas de usuários, sessões e eventos hello, você pode fatiar e nos dados de eventos personalizados pelo usuário, nome do evento e propriedades.</span><span class="sxs-lookup"><span data-stu-id="9f10b-180">In hello Users, Sessions, and Events tools, you can slice and dice custom events by user, event name, and properties.</span></span>
<span data-ttu-id="9f10b-181">![Usuários](./media/app-insights-usage-overview/users.png)</span><span class="sxs-lookup"><span data-stu-id="9f10b-181">![Users](./media/app-insights-usage-overview/users.png)</span></span>  
  
## <a name="design-hello-telemetry-with-hello-app"></a><span data-ttu-id="9f10b-182">Telemetria de saudação do design com o aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="9f10b-182">Design hello telemetry with hello app</span></span>

<span data-ttu-id="9f10b-183">Quando você estiver criando cada recurso do aplicativo, considere como você vai toomeasure seu sucesso com os usuários.</span><span class="sxs-lookup"><span data-stu-id="9f10b-183">When you are designing each feature of your app, consider how you are going toomeasure its success with your users.</span></span> <span data-ttu-id="9f10b-184">Decida quais eventos de negócios precisa toorecord e código Olá chamadas para esses eventos de rastreamento em seu aplicativo de saudação iniciar.</span><span class="sxs-lookup"><span data-stu-id="9f10b-184">Decide what business events you need toorecord, and code hello tracking calls for those events into your app from hello start.</span></span>

## <a name="a--b-testing"></a><span data-ttu-id="9f10b-185">Testando A | B</span><span class="sxs-lookup"><span data-stu-id="9f10b-185">A | B Testing</span></span>
<span data-ttu-id="9f10b-186">Se você não souber qual variante de um recurso será mais bem-sucedida, libere ambas, tornando cada usuários toodifferent acessível.</span><span class="sxs-lookup"><span data-stu-id="9f10b-186">If you don't know which variant of a feature will be more successful, release both of them, making each accessible toodifferent users.</span></span> <span data-ttu-id="9f10b-187">Medir o sucesso de saudação de cada e, em seguida, mova o versão unificada tooa.</span><span class="sxs-lookup"><span data-stu-id="9f10b-187">Measure hello success of each, and then move tooa unified version.</span></span>

<span data-ttu-id="9f10b-188">Para essa técnica, você deve anexar propriedade distintos valores tooall Olá da telemetria enviada por cada versão do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9f10b-188">For this technique, you attach distinct property values tooall hello telemetry that is sent by each version of your app.</span></span> <span data-ttu-id="9f10b-189">Você pode fazer isso definindo propriedades no hello TelemetryContext ativo.</span><span class="sxs-lookup"><span data-stu-id="9f10b-189">You can do that by defining properties in hello active TelemetryContext.</span></span> <span data-ttu-id="9f10b-190">Essas propriedades padrão são adicionadas a mensagem de telemetria tooevery Olá aplicativo envia - não apenas a mensagens personalizadas, mas também a telemetria de padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="9f10b-190">These default properties are added tooevery telemetry message that hello application sends - not just your custom messages, but hello standard telemetry as well.</span></span>

<span data-ttu-id="9f10b-191">No portal do Application Insights hello, filtrar e dividir os dados em valores de propriedade hello, assim como versões diferentes do toocompare hello.</span><span class="sxs-lookup"><span data-stu-id="9f10b-191">In hello Application Insights portal, filter and split your data on hello property values, so as toocompare hello different versions.</span></span>

<span data-ttu-id="9f10b-192">toodo, [configurar um inicializador de telemetria](app-insights-api-filtering-sampling.md##add-properties-itelemetryinitializer):</span><span class="sxs-lookup"><span data-stu-id="9f10b-192">toodo this, [set up a telemetry initializer](app-insights-api-filtering-sampling.md##add-properties-itelemetryinitializer):</span></span>

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

<span data-ttu-id="9f10b-193">Inicializador de aplicativo da web de hello como asax:</span><span class="sxs-lookup"><span data-stu-id="9f10b-193">In hello web app initializer such as Global.asax.cs:</span></span>

```C#

    protected void Application_Start()
    {
        // ...
        TelemetryConfiguration.Active.TelemetryInitializers
        .Add(new MyTelemetryInitializer());
    }
```

<span data-ttu-id="9f10b-194">TelemetryClients novo todos os adiciona automaticamente o valor da propriedade Olá que você especificar.</span><span class="sxs-lookup"><span data-stu-id="9f10b-194">All new TelemetryClients automatically add hello property value you specify.</span></span> <span data-ttu-id="9f10b-195">Eventos de telemetria individual podem substituir valores padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="9f10b-195">Individual telemetry events can override hello default values.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9f10b-196">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9f10b-196">Next steps</span></span>
   - [<span data-ttu-id="9f10b-197">Usuários, Sessões, Eventos</span><span class="sxs-lookup"><span data-stu-id="9f10b-197">Users, Sessions, Events</span></span>](app-insights-usage-segmentation.md)
   - [<span data-ttu-id="9f10b-198">Funis</span><span class="sxs-lookup"><span data-stu-id="9f10b-198">Funnels</span></span>](usage-funnels.md)
   - [<span data-ttu-id="9f10b-199">Retenção</span><span class="sxs-lookup"><span data-stu-id="9f10b-199">Retention</span></span>](app-insights-usage-retention.md)
   - [<span data-ttu-id="9f10b-200">Fluxos de Usuário</span><span class="sxs-lookup"><span data-stu-id="9f10b-200">User Flows</span></span>](app-insights-usage-flows.md)
   - [<span data-ttu-id="9f10b-201">Pastas de trabalho</span><span class="sxs-lookup"><span data-stu-id="9f10b-201">Workbooks</span></span>](app-insights-usage-workbooks.md)
   - [<span data-ttu-id="9f10b-202">Adicionar contexto de usuário</span><span class="sxs-lookup"><span data-stu-id="9f10b-202">Add user context</span></span>](app-insights-usage-send-user-context.md)
