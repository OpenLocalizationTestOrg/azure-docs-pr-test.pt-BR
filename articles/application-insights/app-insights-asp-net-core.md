---
title: aaaAzure Application Insights para ASP.NET Core | Microsoft Docs
description: Monitorar aplicativos web de disponibilidade, desempenho e uso.
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 3b722e47-38bd-4667-9ba4-65b7006c074c
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: a7a27f9eef1daec5b0deae9fd88906e646980659
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-for-aspnet-core"></a><span data-ttu-id="bd64f-103">Application Insights para ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="bd64f-103">Application Insights for ASP.NET Core</span></span>
<span data-ttu-id="bd64f-104">O [Application Insights](app-insights-overview.md) permite que você monitore seu aplicativo Web quanto à disponibilidade, desempenho e uso.</span><span class="sxs-lookup"><span data-stu-id="bd64f-104">[Application Insights](app-insights-overview.md) lets you monitor your web application for availability, performance and usage.</span></span> <span data-ttu-id="bd64f-105">Feedback Olá que obter sobre desempenho hello e a eficácia do seu aplicativo em Olá curinga, você pode fazer escolhas informadas sobre a direção de saudação do design de saudação em cada ciclo de vida de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="bd64f-105">With hello feedback you get about hello performance and effectiveness of your app in hello wild, you can make informed choices about hello direction of hello design in each development lifecycle.</span></span>

![Exemplo](./media/app-insights-asp-net-core/sample.png)

<span data-ttu-id="bd64f-107">Precisa de uma assinatura do [Microsoft Azure](http://azure.com).</span><span class="sxs-lookup"><span data-stu-id="bd64f-107">You'll need a subscription with [Microsoft Azure](http://azure.com).</span></span> <span data-ttu-id="bd64f-108">Entre com uma conta da Microsoft, que você pode ter para o Windows, XBox Live ou outros serviços de nuvem da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="bd64f-108">Sign in with a Microsoft account, which you might have for Windows, XBox Live, or other Microsoft cloud services.</span></span> <span data-ttu-id="bd64f-109">Sua equipe pode ter uma assinatura organizacional tooAzure: peça Olá proprietário tooadd tooit usando sua conta da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="bd64f-109">Your team might have an organizational subscription tooAzure: ask hello owner tooadd you tooit using your Microsoft account.</span></span>

## <a name="getting-started"></a><span data-ttu-id="bd64f-110">Introdução</span><span class="sxs-lookup"><span data-stu-id="bd64f-110">Getting started</span></span>

* <span data-ttu-id="bd64f-111">No Gerenciador de Soluções do Visual Studio, clique com o botão direito do mouse no projeto e selecione **Configurar Application Insights** ou **Adicionar > Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="bd64f-111">In Visual Studio Solution Explorer, right-click your project and select **Configure Application Insights**, or **Add > Application Insights**.</span></span> <span data-ttu-id="bd64f-112">[Saiba mais](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="bd64f-112">[Learn more](app-insights-asp-net.md).</span></span>
* <span data-ttu-id="bd64f-113">Se você não vir os comandos de menu, siga Olá [manual guia de Introdução ao obter](https://github.com/Microsoft/ApplicationInsights-aspnetcore/wiki/Getting-Started).</span><span class="sxs-lookup"><span data-stu-id="bd64f-113">If you don't see those menu commands, follow hello [manual getting Started guide](https://github.com/Microsoft/ApplicationInsights-aspnetcore/wiki/Getting-Started).</span></span> <span data-ttu-id="bd64f-114">Talvez você precise toodo isso se seu projeto foi criado com uma versão do Visual Studio antes de 2017.</span><span class="sxs-lookup"><span data-stu-id="bd64f-114">You may need toodo this if your project was created with a version of Visual Studio before 2017.</span></span>

## <a name="using-application-insights"></a><span data-ttu-id="bd64f-115">Usando o Application Insights</span><span class="sxs-lookup"><span data-stu-id="bd64f-115">Using Application Insights</span></span>
<span data-ttu-id="bd64f-116">O logon no hello [portal do Microsoft Azure](https://portal.azure.com), selecione **todos os recursos** ou **Application Insights**e, em seguida, selecione o recurso de saudação criado toomonitor seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="bd64f-116">Sign into hello [Microsoft Azure portal](https://portal.azure.com), select **All Resources** or **Application Insights**, and then select hello resource you created toomonitor your app.</span></span>

<span data-ttu-id="bd64f-117">Em uma janela separada do navegador, use seu aplicativo por algum tempo.</span><span class="sxs-lookup"><span data-stu-id="bd64f-117">In a separate browser window, use your app for a while.</span></span> <span data-ttu-id="bd64f-118">Você verá os dados que aparecem nos gráficos do Application Insights hello.</span><span class="sxs-lookup"><span data-stu-id="bd64f-118">You'll see data appearing in hello Application Insights charts.</span></span> <span data-ttu-id="bd64f-119">(Talvez seja necessário tooclick atualização). Haverá uma pequena quantidade de dados enquanto você estiver desenvolvendo, mas estes gráficos realmente ganharão vida quando você publicar seu aplicativo e tiver muitos usuários.</span><span class="sxs-lookup"><span data-stu-id="bd64f-119">(You might have tooclick Refresh.) There will be only a small amount of data while you're developing, but these charts really come alive when you publish your app and have many users.</span></span> 

<span data-ttu-id="bd64f-120">página de visão geral de saudação mostra gráficos de desempenho principais: tempo de resposta do servidor, tempo de carregamento de página e as contagens de solicitações com falha.</span><span class="sxs-lookup"><span data-stu-id="bd64f-120">hello overview page shows key performance charts: server response time,  page load time, and counts of failed requests.</span></span> <span data-ttu-id="bd64f-121">Clique em qualquer toosee gráfico mais gráficos e dados.</span><span class="sxs-lookup"><span data-stu-id="bd64f-121">Click any chart toosee more charts and data.</span></span>

<span data-ttu-id="bd64f-122">Modos de exibição no portal de saudação se enquadram em três categorias principais:</span><span class="sxs-lookup"><span data-stu-id="bd64f-122">Views in hello portal fall into three main categories:</span></span>

* <span data-ttu-id="bd64f-123">[Do Metrics Explorer](app-insights-metrics-explorer.md) mostra gráficos e tabelas de métricas e contagens, como tempos de resposta, taxas de falha ou métricas criados por você com hello [API](app-insights-api-custom-events-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="bd64f-123">[Metrics Explorer](app-insights-metrics-explorer.md) shows graphs and tables of metrics and counts, such as response times, failure rates, or metrics you create yourself with hello [API](app-insights-api-custom-events-metrics.md).</span></span> <span data-ttu-id="bd64f-124">Filtrar e segmento de dados de saudação por tooget de valores de propriedade, uma melhor compreensão sobre seu aplicativo e seus usuários.</span><span class="sxs-lookup"><span data-stu-id="bd64f-124">Filter and segment hello data by property values tooget a better understanding of your app and its users.</span></span>
* <span data-ttu-id="bd64f-125">[Pesquisar Gerenciador](app-insights-diagnostic-search.md) lista os eventos individuais, como solicitações específicas, exceções, rastreamentos de log ou eventos que você criou por conta própria com hello [API](app-insights-api-custom-events-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="bd64f-125">[Search Explorer](app-insights-diagnostic-search.md) lists individual events, such as specific requests, exceptions, log traces, or events you created yourself with hello [API](app-insights-api-custom-events-metrics.md).</span></span> <span data-ttu-id="bd64f-126">Filtrar e pesquisar eventos hello e navegar em problemas de tooinvestigate eventos relacionados.</span><span class="sxs-lookup"><span data-stu-id="bd64f-126">Filter and search in hello events, and navigate among related events tooinvestigate issues.</span></span>
* <span data-ttu-id="bd64f-127">[Análise](app-insights-analytics.md) permite que você execute consultas SQL em sua telemetria e é uma poderosa ferramenta de análise e de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="bd64f-127">[Analytics](app-insights-analytics.md) lets you run SQL-like queries over your telemetry, and is a powerful analytical and diagnostic tool.</span></span>

## <a name="alerts"></a><span data-ttu-id="bd64f-128">Alertas</span><span class="sxs-lookup"><span data-stu-id="bd64f-128">Alerts</span></span>
* <span data-ttu-id="bd64f-129">Você obtém automaticamente [alertas proativos de diagnóstico](app-insights-proactive-diagnostics.md) que informam sobre alterações anômalas em taxas de falha e outras métricas.</span><span class="sxs-lookup"><span data-stu-id="bd64f-129">You automatically get [proactive diagnostic alerts](app-insights-proactive-diagnostics.md) that tell you about anomalous changes in failure rates and other metrics.</span></span>
* <span data-ttu-id="bd64f-130">Configurar [testes de disponibilidade](app-insights-monitor-web-app-availability.md) tootest emails em seu site continuamente em locais em todo o mundo e get, assim como qualquer teste falhar.</span><span class="sxs-lookup"><span data-stu-id="bd64f-130">Set up [availability tests](app-insights-monitor-web-app-availability.md) tootest your website continually from locations worldwide, and get emails as soon as any test fails.</span></span>
* <span data-ttu-id="bd64f-131">Configurar [alertas métricas](app-insights-monitor-web-app-availability.md) tooknow se métricas, como tempos de resposta ou taxas de exceção ficarem fora dos limites aceitáveis.</span><span class="sxs-lookup"><span data-stu-id="bd64f-131">Set up [metric alerts](app-insights-monitor-web-app-availability.md) tooknow if metrics such as response times or exception rates go outside acceptable limits.</span></span>

## <a name="video"></a><span data-ttu-id="bd64f-132">Vídeo</span><span class="sxs-lookup"><span data-stu-id="bd64f-132">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player] 

## <a name="open-source"></a><span data-ttu-id="bd64f-133">Código-fonte aberto</span><span class="sxs-lookup"><span data-stu-id="bd64f-133">Open source</span></span>
[<span data-ttu-id="bd64f-134">Ler e contribuir toohello código</span><span class="sxs-lookup"><span data-stu-id="bd64f-134">Read and contribute toohello code</span></span>](https://github.com/Microsoft/ApplicationInsights-aspnetcore#recent-updates)


## <a name="next-steps"></a><span data-ttu-id="bd64f-135">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="bd64f-135">Next steps</span></span>
* <span data-ttu-id="bd64f-136">[Adicionar páginas da web a telemetria tooyour](app-insights-javascript.md) toomonitor página desempenho e uso.</span><span class="sxs-lookup"><span data-stu-id="bd64f-136">[Add telemetry tooyour web pages](app-insights-javascript.md) toomonitor page usage and performance.</span></span>
* <span data-ttu-id="bd64f-137">[Monitorar dependências](app-insights-asp-net-dependencies.md) toosee se REST, SQL ou outros recursos externos são lentidão você.</span><span class="sxs-lookup"><span data-stu-id="bd64f-137">[Monitor dependencies](app-insights-asp-net-dependencies.md) toosee if REST, SQL or other external resources are slowing you down.</span></span>
* <span data-ttu-id="bd64f-138">[Use a API de saudação](app-insights-api-custom-events-metrics.md) toosend seus próprios eventos e métricas para uma exibição mais detalhada de uso e desempenho do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="bd64f-138">[Use hello API](app-insights-api-custom-events-metrics.md) toosend your own events and metrics for a more detailed view of your app's performance and usage.</span></span>
* <span data-ttu-id="bd64f-139">[Testes de disponibilidade](app-insights-monitor-web-app-availability.md) Verifique seu aplicativo constantemente do mundo hello.</span><span class="sxs-lookup"><span data-stu-id="bd64f-139">[Availability tests](app-insights-monitor-web-app-availability.md) check your app constantly from around hello world.</span></span> 

