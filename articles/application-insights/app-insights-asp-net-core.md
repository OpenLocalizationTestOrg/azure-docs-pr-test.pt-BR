---
title: Azure Application Insights para ASP.NET Core | Microsoft Docs
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
ms.openlocfilehash: d86495eea467977f6c079de72e2b49a2a1da2b60
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="application-insights-for-aspnet-core"></a><span data-ttu-id="9bce7-103">Application Insights para ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="9bce7-103">Application Insights for ASP.NET Core</span></span>
<span data-ttu-id="9bce7-104">O [Application Insights](app-insights-overview.md) permite que você monitore seu aplicativo Web quanto à disponibilidade, desempenho e uso.</span><span class="sxs-lookup"><span data-stu-id="9bce7-104">[Application Insights](app-insights-overview.md) lets you monitor your web application for availability, performance and usage.</span></span> <span data-ttu-id="9bce7-105">Com os comentários que você obtiver sobre o desempenho e a eficiência de seu aplicativo em uso, você pode fazer escolhas informadas sobre a direção do projeto em cada ciclo de vida de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="9bce7-105">With the feedback you get about the performance and effectiveness of your app in the wild, you can make informed choices about the direction of the design in each development lifecycle.</span></span>

![Exemplo](./media/app-insights-asp-net-core/sample.png)

<span data-ttu-id="9bce7-107">Precisa de uma assinatura do [Microsoft Azure](http://azure.com).</span><span class="sxs-lookup"><span data-stu-id="9bce7-107">You'll need a subscription with [Microsoft Azure](http://azure.com).</span></span> <span data-ttu-id="9bce7-108">Entre com uma conta da Microsoft, que você pode ter para o Windows, XBox Live ou outros serviços de nuvem da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="9bce7-108">Sign in with a Microsoft account, which you might have for Windows, XBox Live, or other Microsoft cloud services.</span></span> <span data-ttu-id="9bce7-109">Sua equipe pode ter uma assinatura organizacional do Azure: peça ao proprietário que adicione você a ela usando sua conta da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="9bce7-109">Your team might have an organizational subscription to Azure: ask the owner to add you to it using your Microsoft account.</span></span>

## <a name="getting-started"></a><span data-ttu-id="9bce7-110">Introdução</span><span class="sxs-lookup"><span data-stu-id="9bce7-110">Getting started</span></span>

* <span data-ttu-id="9bce7-111">No Gerenciador de Soluções do Visual Studio, clique com o botão direito do mouse no projeto e selecione **Configurar Application Insights** ou **Adicionar > Application Insights**.</span><span class="sxs-lookup"><span data-stu-id="9bce7-111">In Visual Studio Solution Explorer, right-click your project and select **Configure Application Insights**, or **Add > Application Insights**.</span></span> <span data-ttu-id="9bce7-112">[Saiba mais](app-insights-asp-net.md).</span><span class="sxs-lookup"><span data-stu-id="9bce7-112">[Learn more](app-insights-asp-net.md).</span></span>
* <span data-ttu-id="9bce7-113">Se esses comandos de menu não forem exibidos, siga o [manual Guia de Introdução](https://github.com/Microsoft/ApplicationInsights-aspnetcore/wiki/Getting-Started).</span><span class="sxs-lookup"><span data-stu-id="9bce7-113">If you don't see those menu commands, follow the [manual getting Started guide](https://github.com/Microsoft/ApplicationInsights-aspnetcore/wiki/Getting-Started).</span></span> <span data-ttu-id="9bce7-114">Talvez seja necessário fazer isso se o projeto foi criado com uma versão do Visual Studio anterior a 2017.</span><span class="sxs-lookup"><span data-stu-id="9bce7-114">You may need to do this if your project was created with a version of Visual Studio before 2017.</span></span>

## <a name="using-application-insights"></a><span data-ttu-id="9bce7-115">Usando o Application Insights</span><span class="sxs-lookup"><span data-stu-id="9bce7-115">Using Application Insights</span></span>
<span data-ttu-id="9bce7-116">Entre no [portal do Microsoft Azure](https://portal.azure.com), selecione **Todos os Recursos** ou **Application Insights** e, em seguida, selecione o recurso criado para monitorar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9bce7-116">Sign into the [Microsoft Azure portal](https://portal.azure.com), select **All Resources** or **Application Insights**, and then select the resource you created to monitor your app.</span></span>

<span data-ttu-id="9bce7-117">Em uma janela separada do navegador, use seu aplicativo por algum tempo.</span><span class="sxs-lookup"><span data-stu-id="9bce7-117">In a separate browser window, use your app for a while.</span></span> <span data-ttu-id="9bce7-118">Você verá os dados exibidos nos gráficos do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="9bce7-118">You'll see data appearing in the Application Insights charts.</span></span> <span data-ttu-id="9bce7-119">(Talvez você precise clicar em Atualizar.) Haverá uma pequena quantidade de dados enquanto você estiver desenvolvendo, mas estes gráficos realmente ganharão vida quando você publicar seu aplicativo e tiver muitos usuários.</span><span class="sxs-lookup"><span data-stu-id="9bce7-119">(You might have to click Refresh.) There will be only a small amount of data while you're developing, but these charts really come alive when you publish your app and have many users.</span></span> 

<span data-ttu-id="9bce7-120">A página de visão geral mostra gráficos de desempenho chave: tempo de resposta do servidor, tempo de carregamento de página e contagens de solicitações com falha.</span><span class="sxs-lookup"><span data-stu-id="9bce7-120">The overview page shows key performance charts: server response time,  page load time, and counts of failed requests.</span></span> <span data-ttu-id="9bce7-121">Clique em qualquer gráfico para ver mais gráficos e dados.</span><span class="sxs-lookup"><span data-stu-id="9bce7-121">Click any chart to see more charts and data.</span></span>

<span data-ttu-id="9bce7-122">As exibições no portal se enquadram em três categorias principais:</span><span class="sxs-lookup"><span data-stu-id="9bce7-122">Views in the portal fall into three main categories:</span></span>

* <span data-ttu-id="9bce7-123">O [Metrics Explorer](app-insights-metrics-explorer.md) mostra gráficos e tabelas de métricas e contagens, como tempos de resposta, taxas de falha ou métricas que você cria com a [API](app-insights-api-custom-events-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="9bce7-123">[Metrics Explorer](app-insights-metrics-explorer.md) shows graphs and tables of metrics and counts, such as response times, failure rates, or metrics you create yourself with the [API](app-insights-api-custom-events-metrics.md).</span></span> <span data-ttu-id="9bce7-124">Filtre e segmente os dados por valores de propriedade para obter uma compreensão melhor do seu aplicativo e seus usuários.</span><span class="sxs-lookup"><span data-stu-id="9bce7-124">Filter and segment the data by property values to get a better understanding of your app and its users.</span></span>
* <span data-ttu-id="9bce7-125">O [Search Explorer](app-insights-diagnostic-search.md) lista eventos individuais, como solicitações específicas, exceções, rastreamentos de log ou eventos que você criou com a [API](app-insights-api-custom-events-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="9bce7-125">[Search Explorer](app-insights-diagnostic-search.md) lists individual events, such as specific requests, exceptions, log traces, or events you created yourself with the [API](app-insights-api-custom-events-metrics.md).</span></span> <span data-ttu-id="9bce7-126">Filtre e pesquise nos eventos e navegue entre os eventos relacionados para investigar problemas.</span><span class="sxs-lookup"><span data-stu-id="9bce7-126">Filter and search in the events, and navigate among related events to investigate issues.</span></span>
* <span data-ttu-id="9bce7-127">[Análise](app-insights-analytics.md) permite que você execute consultas SQL em sua telemetria e é uma poderosa ferramenta de análise e de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="9bce7-127">[Analytics](app-insights-analytics.md) lets you run SQL-like queries over your telemetry, and is a powerful analytical and diagnostic tool.</span></span>

## <a name="alerts"></a><span data-ttu-id="9bce7-128">Alertas</span><span class="sxs-lookup"><span data-stu-id="9bce7-128">Alerts</span></span>
* <span data-ttu-id="9bce7-129">Você obtém automaticamente [alertas proativos de diagnóstico](app-insights-proactive-diagnostics.md) que informam sobre alterações anômalas em taxas de falha e outras métricas.</span><span class="sxs-lookup"><span data-stu-id="9bce7-129">You automatically get [proactive diagnostic alerts](app-insights-proactive-diagnostics.md) that tell you about anomalous changes in failure rates and other metrics.</span></span>
* <span data-ttu-id="9bce7-130">Configure [testes de disponibilidade](app-insights-monitor-web-app-availability.md) para testar seu site continuamente em locais em todo o mundo e receber emails assim que qualquer teste falhar.</span><span class="sxs-lookup"><span data-stu-id="9bce7-130">Set up [availability tests](app-insights-monitor-web-app-availability.md) to test your website continually from locations worldwide, and get emails as soon as any test fails.</span></span>
* <span data-ttu-id="9bce7-131">Configure [alertas de métrica](app-insights-monitor-web-app-availability.md) para saber se métricas, como tempos de resposta ou taxas de exceção, saem dos limites aceitáveis.</span><span class="sxs-lookup"><span data-stu-id="9bce7-131">Set up [metric alerts](app-insights-monitor-web-app-availability.md) to know if metrics such as response times or exception rates go outside acceptable limits.</span></span>

## <a name="video"></a><span data-ttu-id="9bce7-132">Vídeo</span><span class="sxs-lookup"><span data-stu-id="9bce7-132">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player] 

## <a name="open-source"></a><span data-ttu-id="9bce7-133">Código-fonte aberto</span><span class="sxs-lookup"><span data-stu-id="9bce7-133">Open source</span></span>
[<span data-ttu-id="9bce7-134">Ler e contribuir para o código</span><span class="sxs-lookup"><span data-stu-id="9bce7-134">Read and contribute to the code</span></span>](https://github.com/Microsoft/ApplicationInsights-aspnetcore#recent-updates)


## <a name="next-steps"></a><span data-ttu-id="9bce7-135">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9bce7-135">Next steps</span></span>
* <span data-ttu-id="9bce7-136">[Adicione telemetria às suas páginas da Web](app-insights-javascript.md) para monitorar o uso e o desempenho de páginas.</span><span class="sxs-lookup"><span data-stu-id="9bce7-136">[Add telemetry to your web pages](app-insights-javascript.md) to monitor page usage and performance.</span></span>
* <span data-ttu-id="9bce7-137">[Monitore dependências](app-insights-asp-net-dependencies.md) para ver se REST, SQL ou outros recursos externos estão causando lentidão.</span><span class="sxs-lookup"><span data-stu-id="9bce7-137">[Monitor dependencies](app-insights-asp-net-dependencies.md) to see if REST, SQL or other external resources are slowing you down.</span></span>
* <span data-ttu-id="9bce7-138">[Use a API](app-insights-api-custom-events-metrics.md) para enviar seus próprios eventos e métricas para uma exibição mais detalhada do desempenho e do uso do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9bce7-138">[Use the API](app-insights-api-custom-events-metrics.md) to send your own events and metrics for a more detailed view of your app's performance and usage.</span></span>
* <span data-ttu-id="9bce7-139">[Testes de disponibilidade](app-insights-monitor-web-app-availability.md) verificam seu aplicativo constantemente em todo o mundo.</span><span class="sxs-lookup"><span data-stu-id="9bce7-139">[Availability tests](app-insights-monitor-web-app-availability.md) check your app constantly from around the world.</span></span> 

