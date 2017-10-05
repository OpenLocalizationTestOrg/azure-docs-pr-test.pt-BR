---
title: "Diagnóstico inteligente de alterações no desempenho do aplicativo Web no Azure Application Insights | Microsoft Docs"
description: "Diagnóstico automático de picos ou etapas em telemetria de desempenho do seu aplicativo Web."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 04/16/2017
ms.author: cfreeman
ms.openlocfilehash: 5e53bc714d89bf6204681349e7890e0b8fbc7046
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="diagnose-sudden-changes-in-your-app-telemetry"></a><span data-ttu-id="1f864-103">Diagnosticar alterações repentinas na telemetria do aplicativo</span><span class="sxs-lookup"><span data-stu-id="1f864-103">Diagnose sudden changes in your app telemetry</span></span>

<span data-ttu-id="1f864-104">*Esse recurso está em visualização.*</span><span class="sxs-lookup"><span data-stu-id="1f864-104">*This feature is in preview.*</span></span>

<span data-ttu-id="1f864-105">Faça o diagnóstico de alterações repentinas no uso ou no desempenho do seu aplicativo Web com um único clique!</span><span class="sxs-lookup"><span data-stu-id="1f864-105">Diagnose sudden changes in your web app’s performance or usage with a single click!</span></span> <span data-ttu-id="1f864-106">O recurso Smart Diagnostics está disponível sempre que você cria um gráfico no [Analytics](app-insights-analytics.md) em [Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1f864-106">The Smart Diagnostics feature is available whenever you create a time chart in [Analytics](app-insights-analytics.md) in [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="1f864-107">Sempre que houver uma alteração incomum de tendência dos seus resultados, como um pico ou um DIP, o Diagnóstico Inteligente identificará um padrão de dimensões e valores relacionados que poderão explicar a alteração.</span><span class="sxs-lookup"><span data-stu-id="1f864-107">Wherever there is an unusual change from the trend of your results, such as a spike or a dip, Smart Diagnostics identifies a pattern of dimensions and related values that might explain the change.</span></span> <span data-ttu-id="1f864-108">Isso ajuda a diagnosticar rapidamente o problema.</span><span class="sxs-lookup"><span data-stu-id="1f864-108">This helps you diagnose the problem quickly.</span></span> 

<span data-ttu-id="1f864-109">Nesse exemplo, o Diagnóstico Inteligente identificou um padrão de valores de propriedade relacionado à alteração e destaca a diferença entre resultados com e sem esse padrão:</span><span class="sxs-lookup"><span data-stu-id="1f864-109">In this example, Smart Diagnostics has identified a pattern of property values associated with the change, and highlights the difference between results with and without that pattern:</span></span>

![resultado de diagnóstico analítico de exemplo](./media/app-insights-analytics-diagnostics/analytics-result.png)
 

## <a name="diagnose-data-changes"></a><span data-ttu-id="1f864-111">Diagnosticar alterações de dados</span><span class="sxs-lookup"><span data-stu-id="1f864-111">Diagnose data changes</span></span>

1.  <span data-ttu-id="1f864-112">Execute uma consulta no Analytics e renderize-o como um gráfico de tempo.</span><span class="sxs-lookup"><span data-stu-id="1f864-112">Run a query in Analytics, and render it as a time chart.</span></span> 
2.  <span data-ttu-id="1f864-113">Clique em qualquer ponto de pico destacado, se houver.</span><span class="sxs-lookup"><span data-stu-id="1f864-113">Click any highlighted peak point, if there is one.</span></span>
 
    ![ponto de pico](./media/app-insights-analytics-diagnostics/peak.png)

    <span data-ttu-id="1f864-115">O diagnóstico leva alguns segundos para descobrir um padrão.</span><span class="sxs-lookup"><span data-stu-id="1f864-115">Diagnostics takes a few seconds to discover a pattern.</span></span>

3. <span data-ttu-id="1f864-116">A guia Resultados do Diagnóstico mostra um padrão que pode explicar a descontinuidade dos dados.</span><span class="sxs-lookup"><span data-stu-id="1f864-116">The Diagnostics Results tab shows a pattern which may explain your data discontinuity.</span></span>

    ![result](./media/app-insights-analytics-diagnostics/result.png)
 
    <span data-ttu-id="1f864-118">O texto mostra os valores de dimensão que parecem estar relacionados com a mudança.</span><span class="sxs-lookup"><span data-stu-id="1f864-118">The text shows the dimension values that appear to correlate with the shift.</span></span> <span data-ttu-id="1f864-119">Nesse exemplo, isso está associado a uma solicitação específica e uma versão específica do navegador.</span><span class="sxs-lookup"><span data-stu-id="1f864-119">In this example, it’s associated with a particular request and a particular browser version.</span></span>

    <span data-ttu-id="1f864-120">Observe também os dois componentes do gráfico, com o filtro verdadeiro e falso.</span><span class="sxs-lookup"><span data-stu-id="1f864-120">Notice also the two components of the chart, with the filter true and false.</span></span> <span data-ttu-id="1f864-121">O componente falso mostra uma tendência inalterada.</span><span class="sxs-lookup"><span data-stu-id="1f864-121">The false component shows an unchanged trend.</span></span> <span data-ttu-id="1f864-122">Em outras palavras, não há alteração nos resultados da telemetria se excluímos a combinação de dimensões problemática identificada pelo Diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="1f864-122">In other words, there is no change in the telemetry results, if we exclude the problematic combination of dimensions that Diagnostics has identified.</span></span> <span data-ttu-id="1f864-123">Em contrapartida, os resultados dentro dessa combinação apresenta uma alteração dramática dentro da área de investigação destacada.</span><span class="sxs-lookup"><span data-stu-id="1f864-123">By contrast, the results within that combination do show a dramatic change within the highlighted area of investigation.</span></span> <span data-ttu-id="1f864-124">Isso mostra que o Diagnóstico encontrou uma combinação de propriedades que explica a alteração.</span><span class="sxs-lookup"><span data-stu-id="1f864-124">This shows that Diagnostics has found a combination of properties that explains the change.</span></span>

4.  <span data-ttu-id="1f864-125">Se o padrão for complexo, será necessário passar o mouse sobre **Mostrar tudo** para visualizar as dimensões.</span><span class="sxs-lookup"><span data-stu-id="1f864-125">If the pattern is complex, you need to hover over **Show all** to see the dimensions.</span></span>

    ![mostrar tudo](./media/app-insights-analytics-diagnostics/show-all.png)
 
5.  <span data-ttu-id="1f864-127">Caso o Diagnóstico não encontre nenhum padrão significativo a ser notificado, a página "nenhum resultado" será apresentada.</span><span class="sxs-lookup"><span data-stu-id="1f864-127">In case Diagnostics finds no significant pattern to notify about, the ‘no results’ page will be presented.</span></span> <span data-ttu-id="1f864-128">Nesse momento, você pode alterar sua consulta.</span><span class="sxs-lookup"><span data-stu-id="1f864-128">At this point, you may change your query.</span></span> <span data-ttu-id="1f864-129">Por exemplo, você pode restringir o intervalo de tempo e o agrupamento na consulta do Analytics para uma análise mais detalhada e resultados potencialmente melhores.</span><span class="sxs-lookup"><span data-stu-id="1f864-129">For example, you could narrow the time range and binning in Analytics query, for a further analysis and potentially better results.</span></span>

<span data-ttu-id="1f864-130">Tendo o conhecimento de que uma página específica do seu site tem um problema em um navegador específico, você pode ir diretamente para a página do problema e investigar as alterações recentes.</span><span class="sxs-lookup"><span data-stu-id="1f864-130">Armed with the knowledge that a particular page of your website has a problem on a particular browser, you can now go straight to the problem page, and investigate recent changes.</span></span>

## <a name="try-the-demo"></a><span data-ttu-id="1f864-131">Experimente a demonstração</span><span class="sxs-lookup"><span data-stu-id="1f864-131">Try the demo</span></span>

<span data-ttu-id="1f864-132">[Clique aqui para ver uma demonstração](https://analytics.applicationinsights.io/demo?q=H4sIAAAAAAAAA3VSTY%2FTQAy991dYPXWlLf0QIO2KIiGWA3duiMPsxEnMzhe2p6WIH48nVUsuGylRNPOe3%2FOzN5vFZgPfRhL4VZHPIGM%2BCdgHdESgpMjOKx0RnsgNKYuSF%2BjRaWUE7xKMGIoBgTpMSv2Z0jBxOWc1QBWEPjM4EMUCP2uc0A3x8E5HKMi%2BEQNC7oHRbIgKdJWdUk5vmr9PvdkArildit%2Fcrk0lBDjnyhBzk%2FKVxdTy0QhNY6RhDPYqdlCy9XMV96NjBZc68IH8y6Tzuf01iZxeIZ%2FI5DqMOYmaQQRXNUdz6qGb5WOdSKEXnOozHtEFK%2Bh0qnq5YQzGF9DcoinoqbcigkO0NOZRNGOZaaBkMuat5xznFOtULKhG%2BdrGlVDhy%2B8SMlsETV8dD6gTd0YrbsBrFq6U1v%2Filv4C%2FsJpRJuwUrQTZ0P7eIDOHLeD1X67e7%2Fe7dbbB9htH%2Ffbu4vQDfvhFez%2B8a1h%2F1f3VSy%2BJ4Ol1oN8X4qN0qMZWv44HJanzKFLeJIltKcRpcbomP7gbHNkdV2Xe1uqO3g%2BwzOl1c3PvbmMlC7KjKlry2GX0w4s%2FgFoo5%2BhBAMAAA%3D%3D&timespan=PT24H) no dados de exemplo.</span><span class="sxs-lookup"><span data-stu-id="1f864-132">[Click here to see a demonstration](https://analytics.applicationinsights.io/demo?q=H4sIAAAAAAAAA3VSTY%2FTQAy991dYPXWlLf0QIO2KIiGWA3duiMPsxEnMzhe2p6WIH48nVUsuGylRNPOe3%2FOzN5vFZgPfRhL4VZHPIGM%2BCdgHdESgpMjOKx0RnsgNKYuSF%2BjRaWUE7xKMGIoBgTpMSv2Z0jBxOWc1QBWEPjM4EMUCP2uc0A3x8E5HKMi%2BEQNC7oHRbIgKdJWdUk5vmr9PvdkArildit%2Fcrk0lBDjnyhBzk%2FKVxdTy0QhNY6RhDPYqdlCy9XMV96NjBZc68IH8y6Tzuf01iZxeIZ%2FI5DqMOYmaQQRXNUdz6qGb5WOdSKEXnOozHtEFK%2Bh0qnq5YQzGF9DcoinoqbcigkO0NOZRNGOZaaBkMuat5xznFOtULKhG%2BdrGlVDhy%2B8SMlsETV8dD6gTd0YrbsBrFq6U1v%2Filv4C%2FsJpRJuwUrQTZ0P7eIDOHLeD1X67e7%2Fe7dbbB9htH%2Ffbu4vQDfvhFez%2B8a1h%2F1f3VSy%2BJ4Ol1oN8X4qN0qMZWv44HJanzKFLeJIltKcRpcbomP7gbHNkdV2Xe1uqO3g%2BwzOl1c3PvbmMlC7KjKlry2GX0w4s%2FgFoo5%2BhBAMAAA%3D%3D&timespan=PT24H) on sample data.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="1f864-133">Como ele funciona</span><span class="sxs-lookup"><span data-stu-id="1f864-133">How it works</span></span>

<span data-ttu-id="1f864-134">O Diagnóstico Inteligente usa um algoritmo de aprendizado de máquina não supervisionado avançado com base na operação [DiffPatterns](app-insights-analytics-reference.md).</span><span class="sxs-lookup"><span data-stu-id="1f864-134">Smart Diagnostics uses an advanced unsupervised machine learning algorithm based on the [DiffPatterns](app-insights-analytics-reference.md) operation.</span></span> <span data-ttu-id="1f864-135">Ele procura padrões candidatos que podem explicar a alteração de dados.</span><span class="sxs-lookup"><span data-stu-id="1f864-135">It looks for candidate patterns that might explain the data change.</span></span> <span data-ttu-id="1f864-136">Ele analisa o impacto de cada candidato na métrica e mostra o padrão que melhor se correlaciona com a alteração.</span><span class="sxs-lookup"><span data-stu-id="1f864-136">It analyses the impact of each candidate on the metric, and shows the pattern that best correlates with the change.</span></span>

## <a name="no-diagnostic-points"></a><span data-ttu-id="1f864-137">Não há pontos de diagnóstico?</span><span class="sxs-lookup"><span data-stu-id="1f864-137">No diagnostic points?</span></span>

<span data-ttu-id="1f864-138">O Diagnóstico Inteligente funciona somente quando os seguintes critérios forem atendidos:</span><span class="sxs-lookup"><span data-stu-id="1f864-138">Smart Diagnostics only works when the following criteria are satisfied:</span></span>

 * <span data-ttu-id="1f864-139">A configuração do Diagnóstico Inteligente está ativada.</span><span class="sxs-lookup"><span data-stu-id="1f864-139">Smart Diagnostics setting is switched on.</span></span> <span data-ttu-id="1f864-140">Procure o ícone de Configurações no Analytics.</span><span class="sxs-lookup"><span data-stu-id="1f864-140">Look under the Settings icon in Analytics.</span></span>
 * <span data-ttu-id="1f864-141">A opção de Diagnóstico Inteligente nas configurações do Analytics está selecionada.</span><span class="sxs-lookup"><span data-stu-id="1f864-141">The Smart Diagnostics option in Analytics settings is selected.</span></span> 
 * <span data-ttu-id="1f864-142">Eixo de tempo: o eixo X do gráfico deve ser do tipo `datetime`.</span><span class="sxs-lookup"><span data-stu-id="1f864-142">Time axis: The X-axis of the chart must be of type `datetime`.</span></span>
 * <span data-ttu-id="1f864-143">Gráfico de linha ou área: o diagnóstico funciona somente com esses tipos de gráfico.</span><span class="sxs-lookup"><span data-stu-id="1f864-143">Line or area chart: Diagnostics only works these types of chart.</span></span> <span data-ttu-id="1f864-144">Use `| render timechart` ou `| render areachart` no final da sua consulta; ou selecione Gráfico de Área ou Linha no seletor suspenso.</span><span class="sxs-lookup"><span data-stu-id="1f864-144">Use `| render timechart` or `| render areachart` at the end of your query; or select Line or Area Chart from the drop-down selector.</span></span>
 * <span data-ttu-id="1f864-145">Descontinuidade: deve haver uma descontinuidade significativa nos dados.</span><span class="sxs-lookup"><span data-stu-id="1f864-145">Discontinuity: There must be a significant discontinuity in the data.</span></span>
 * <span data-ttu-id="1f864-146">Pontos suficientes para analisar.</span><span class="sxs-lookup"><span data-stu-id="1f864-146">Sufficient points to analyze.</span></span>
 * <span data-ttu-id="1f864-147">Não mais que uma cláusula de resumo na consulta.</span><span class="sxs-lookup"><span data-stu-id="1f864-147">No more than one summarize clause in the query.</span></span>
 * <span data-ttu-id="1f864-148">Nenhuma cláusula de projeto que contenha uma definição de nome antes da cláusula de resumo.</span><span class="sxs-lookup"><span data-stu-id="1f864-148">No project clause that contains a name definition before the summarize clause.</span></span>

 
 ## <a name="related-articles"></a><span data-ttu-id="1f864-149">Artigos relacionados</span><span class="sxs-lookup"><span data-stu-id="1f864-149">Related articles</span></span>

 * [<span data-ttu-id="1f864-150">Tutorial do Analytics</span><span class="sxs-lookup"><span data-stu-id="1f864-150">Analytics tutorial</span></span>](app-insights-analytics-tour.md)
 * <span data-ttu-id="1f864-151">[Detecção inteligente](app-insights-proactive-diagnostics.md) alerta automaticamente para problemas de desempenho.</span><span class="sxs-lookup"><span data-stu-id="1f864-151">[Smart detection](app-insights-proactive-diagnostics.md) automatically alerts you to performance issues.</span></span>