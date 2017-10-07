---
title: "diagnóstico aaaSmart das alterações de desempenho de aplicativo web no Azure Application Insights | Microsoft Docs"
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
ms.openlocfilehash: 8891762c4a4bfdb08b647fe3b702349eb30ec9c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-sudden-changes-in-your-app-telemetry"></a><span data-ttu-id="30ac2-103">Diagnosticar alterações repentinas na telemetria do aplicativo</span><span class="sxs-lookup"><span data-stu-id="30ac2-103">Diagnose sudden changes in your app telemetry</span></span>

<span data-ttu-id="30ac2-104">*Esse recurso está em visualização.*</span><span class="sxs-lookup"><span data-stu-id="30ac2-104">*This feature is in preview.*</span></span>

<span data-ttu-id="30ac2-105">Faça o diagnóstico de alterações repentinas no uso ou no desempenho do seu aplicativo Web com um único clique!</span><span class="sxs-lookup"><span data-stu-id="30ac2-105">Diagnose sudden changes in your web app’s performance or usage with a single click!</span></span> <span data-ttu-id="30ac2-106">recurso de diagnóstico inteligente de saudação está disponível sempre que você cria um gráfico de tempo em [análise](app-insights-analytics.md) na [Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="30ac2-106">hello Smart Diagnostics feature is available whenever you create a time chart in [Analytics](app-insights-analytics.md) in [Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="30ac2-107">Sempre que houver uma alteração incomum de tendência de saudação de resultados, como um aumento ou um dip, diagnóstico inteligente identifica um padrão de dimensões e valores relacionados que possam explicar a alteração de saudação.</span><span class="sxs-lookup"><span data-stu-id="30ac2-107">Wherever there is an unusual change from hello trend of your results, such as a spike or a dip, Smart Diagnostics identifies a pattern of dimensions and related values that might explain hello change.</span></span> <span data-ttu-id="30ac2-108">Isso ajuda você a diagnosticar o problema de saudação rapidamente.</span><span class="sxs-lookup"><span data-stu-id="30ac2-108">This helps you diagnose hello problem quickly.</span></span> 

<span data-ttu-id="30ac2-109">Neste exemplo, diagnóstico inteligente identificou um padrão de valores de propriedade associados a alteração hello e realça Olá diferença entre os resultados com e sem esse padrão:</span><span class="sxs-lookup"><span data-stu-id="30ac2-109">In this example, Smart Diagnostics has identified a pattern of property values associated with hello change, and highlights hello difference between results with and without that pattern:</span></span>

![resultado de diagnóstico analítico de exemplo](./media/app-insights-analytics-diagnostics/analytics-result.png)
 

## <a name="diagnose-data-changes"></a><span data-ttu-id="30ac2-111">Diagnosticar alterações de dados</span><span class="sxs-lookup"><span data-stu-id="30ac2-111">Diagnose data changes</span></span>

1.  <span data-ttu-id="30ac2-112">Execute uma consulta no Analytics e renderize-o como um gráfico de tempo.</span><span class="sxs-lookup"><span data-stu-id="30ac2-112">Run a query in Analytics, and render it as a time chart.</span></span> 
2.  <span data-ttu-id="30ac2-113">Clique em qualquer ponto de pico destacado, se houver.</span><span class="sxs-lookup"><span data-stu-id="30ac2-113">Click any highlighted peak point, if there is one.</span></span>
 
    ![ponto de pico](./media/app-insights-analytics-diagnostics/peak.png)

    <span data-ttu-id="30ac2-115">Diagnóstico leva alguns segundos toodiscover um padrão.</span><span class="sxs-lookup"><span data-stu-id="30ac2-115">Diagnostics takes a few seconds toodiscover a pattern.</span></span>

3. <span data-ttu-id="30ac2-116">Guia de resultados do diagnóstico de saudação mostra um padrão que pode explicar descontinuidade seus dados.</span><span class="sxs-lookup"><span data-stu-id="30ac2-116">hello Diagnostics Results tab shows a pattern which may explain your data discontinuity.</span></span>

    ![result](./media/app-insights-analytics-diagnostics/result.png)
 
    <span data-ttu-id="30ac2-118">texto de saudação mostra os valores de dimensão Olá exibidos toocorrelate com shift hello.</span><span class="sxs-lookup"><span data-stu-id="30ac2-118">hello text shows hello dimension values that appear toocorrelate with hello shift.</span></span> <span data-ttu-id="30ac2-119">Nesse exemplo, isso está associado a uma solicitação específica e uma versão específica do navegador.</span><span class="sxs-lookup"><span data-stu-id="30ac2-119">In this example, it’s associated with a particular request and a particular browser version.</span></span>

    <span data-ttu-id="30ac2-120">Observe também componentes Olá dois de gráfico hello, com hello filtro true e false.</span><span class="sxs-lookup"><span data-stu-id="30ac2-120">Notice also hello two components of hello chart, with hello filter true and false.</span></span> <span data-ttu-id="30ac2-121">componente de saudação false mostra uma tendência inalterada.</span><span class="sxs-lookup"><span data-stu-id="30ac2-121">hello false component shows an unchanged trend.</span></span> <span data-ttu-id="30ac2-122">Em outras palavras, não há nenhuma alteração nos resultados de telemetria hello, se excluímos combinação problemático Olá dimensões diagnóstico identificou.</span><span class="sxs-lookup"><span data-stu-id="30ac2-122">In other words, there is no change in hello telemetry results, if we exclude hello problematic combination of dimensions that Diagnostics has identified.</span></span> <span data-ttu-id="30ac2-123">Por outro lado, os resultados de saudação em combinação mostram uma alteração radical na área de saudação realçada da investigação.</span><span class="sxs-lookup"><span data-stu-id="30ac2-123">By contrast, hello results within that combination do show a dramatic change within hello highlighted area of investigation.</span></span> <span data-ttu-id="30ac2-124">Isso mostra que o diagnóstico encontrou uma combinação das propriedades que explica a alteração de saudação.</span><span class="sxs-lookup"><span data-stu-id="30ac2-124">This shows that Diagnostics has found a combination of properties that explains hello change.</span></span>

4.  <span data-ttu-id="30ac2-125">Se o padrão de saudação é complexo, você precisa toohover pela **Mostrar tudo** toosee dimensões de saudação.</span><span class="sxs-lookup"><span data-stu-id="30ac2-125">If hello pattern is complex, you need toohover over **Show all** toosee hello dimensions.</span></span>

    ![mostrar tudo](./media/app-insights-analytics-diagnostics/show-all.png)
 
5.  <span data-ttu-id="30ac2-127">No caso de diagnóstico não localiza toonotify nenhum padrão significativo sobre Olá que será exibida a página 'Nenhum resultado'.</span><span class="sxs-lookup"><span data-stu-id="30ac2-127">In case Diagnostics finds no significant pattern toonotify about, hello ‘no results’ page will be presented.</span></span> <span data-ttu-id="30ac2-128">Nesse momento, você pode alterar sua consulta.</span><span class="sxs-lookup"><span data-stu-id="30ac2-128">At this point, you may change your query.</span></span> <span data-ttu-id="30ac2-129">Por exemplo, você pode restringir o intervalo de tempo de saudação e agrupamento na consulta de análise, para uma análise adicional e potencialmente melhores resultados.</span><span class="sxs-lookup"><span data-stu-id="30ac2-129">For example, you could narrow hello time range and binning in Analytics query, for a further analysis and potentially better results.</span></span>

<span data-ttu-id="30ac2-130">Armado com conhecimento de saudação que uma página específica do site tem um problema em um navegador específico, você pode agora vá reta toohello problema página e investigar alterações recentes.</span><span class="sxs-lookup"><span data-stu-id="30ac2-130">Armed with hello knowledge that a particular page of your website has a problem on a particular browser, you can now go straight toohello problem page, and investigate recent changes.</span></span>

## <a name="try-hello-demo"></a><span data-ttu-id="30ac2-131">Experimente Olá demonstração</span><span class="sxs-lookup"><span data-stu-id="30ac2-131">Try hello demo</span></span>

<span data-ttu-id="30ac2-132">[Clique aqui toosee uma demonstração](https://analytics.applicationinsights.io/demo?q=H4sIAAAAAAAAA3VSTY%2FTQAy991dYPXWlLf0QIO2KIiGWA3duiMPsxEnMzhe2p6WIH48nVUsuGylRNPOe3%2FOzN5vFZgPfRhL4VZHPIGM%2BCdgHdESgpMjOKx0RnsgNKYuSF%2BjRaWUE7xKMGIoBgTpMSv2Z0jBxOWc1QBWEPjM4EMUCP2uc0A3x8E5HKMi%2BEQNC7oHRbIgKdJWdUk5vmr9PvdkArildit%2Fcrk0lBDjnyhBzk%2FKVxdTy0QhNY6RhDPYqdlCy9XMV96NjBZc68IH8y6Tzuf01iZxeIZ%2FI5DqMOYmaQQRXNUdz6qGb5WOdSKEXnOozHtEFK%2Bh0qnq5YQzGF9DcoinoqbcigkO0NOZRNGOZaaBkMuat5xznFOtULKhG%2BdrGlVDhy%2B8SMlsETV8dD6gTd0YrbsBrFq6U1v%2Filv4C%2FsJpRJuwUrQTZ0P7eIDOHLeD1X67e7%2Fe7dbbB9htH%2Ffbu4vQDfvhFez%2B8a1h%2F1f3VSy%2BJ4Ol1oN8X4qN0qMZWv44HJanzKFLeJIltKcRpcbomP7gbHNkdV2Xe1uqO3g%2BwzOl1c3PvbmMlC7KjKlry2GX0w4s%2FgFoo5%2BhBAMAAA%3D%3D&timespan=PT24H) em dados de exemplo.</span><span class="sxs-lookup"><span data-stu-id="30ac2-132">[Click here toosee a demonstration](https://analytics.applicationinsights.io/demo?q=H4sIAAAAAAAAA3VSTY%2FTQAy991dYPXWlLf0QIO2KIiGWA3duiMPsxEnMzhe2p6WIH48nVUsuGylRNPOe3%2FOzN5vFZgPfRhL4VZHPIGM%2BCdgHdESgpMjOKx0RnsgNKYuSF%2BjRaWUE7xKMGIoBgTpMSv2Z0jBxOWc1QBWEPjM4EMUCP2uc0A3x8E5HKMi%2BEQNC7oHRbIgKdJWdUk5vmr9PvdkArildit%2Fcrk0lBDjnyhBzk%2FKVxdTy0QhNY6RhDPYqdlCy9XMV96NjBZc68IH8y6Tzuf01iZxeIZ%2FI5DqMOYmaQQRXNUdz6qGb5WOdSKEXnOozHtEFK%2Bh0qnq5YQzGF9DcoinoqbcigkO0NOZRNGOZaaBkMuat5xznFOtULKhG%2BdrGlVDhy%2B8SMlsETV8dD6gTd0YrbsBrFq6U1v%2Filv4C%2FsJpRJuwUrQTZ0P7eIDOHLeD1X67e7%2Fe7dbbB9htH%2Ffbu4vQDfvhFez%2B8a1h%2F1f3VSy%2BJ4Ol1oN8X4qN0qMZWv44HJanzKFLeJIltKcRpcbomP7gbHNkdV2Xe1uqO3g%2BwzOl1c3PvbmMlC7KjKlry2GX0w4s%2FgFoo5%2BhBAMAAA%3D%3D&timespan=PT24H) on sample data.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="30ac2-133">Como ele funciona</span><span class="sxs-lookup"><span data-stu-id="30ac2-133">How it works</span></span>

<span data-ttu-id="30ac2-134">O diagnóstico inteligente usa um algoritmo de aprendizado de máquina sem supervisão avançado baseado em Olá [DiffPatterns](app-insights-analytics-reference.md) operação.</span><span class="sxs-lookup"><span data-stu-id="30ac2-134">Smart Diagnostics uses an advanced unsupervised machine learning algorithm based on hello [DiffPatterns](app-insights-analytics-reference.md) operation.</span></span> <span data-ttu-id="30ac2-135">Ele procura por padrões de candidato que podem explicar Olá alteração de dados.</span><span class="sxs-lookup"><span data-stu-id="30ac2-135">It looks for candidate patterns that might explain hello data change.</span></span> <span data-ttu-id="30ac2-136">Ele analisa o impacto de saudação de cada candidato na métrica hello e mostra o padrão de saudação que melhor se correlaciona com alteração de saudação.</span><span class="sxs-lookup"><span data-stu-id="30ac2-136">It analyses hello impact of each candidate on hello metric, and shows hello pattern that best correlates with hello change.</span></span>

## <a name="no-diagnostic-points"></a><span data-ttu-id="30ac2-137">Não há pontos de diagnóstico?</span><span class="sxs-lookup"><span data-stu-id="30ac2-137">No diagnostic points?</span></span>

<span data-ttu-id="30ac2-138">Diagnóstico inteligente só funciona quando Olá critérios a seguir forem atendida:</span><span class="sxs-lookup"><span data-stu-id="30ac2-138">Smart Diagnostics only works when hello following criteria are satisfied:</span></span>

 * <span data-ttu-id="30ac2-139">A configuração do Diagnóstico Inteligente está ativada.</span><span class="sxs-lookup"><span data-stu-id="30ac2-139">Smart Diagnostics setting is switched on.</span></span> <span data-ttu-id="30ac2-140">Procure o ícone de configurações de saudação na análise.</span><span class="sxs-lookup"><span data-stu-id="30ac2-140">Look under hello Settings icon in Analytics.</span></span>
 * <span data-ttu-id="30ac2-141">Olá opção diagnóstico inteligente nas configurações de análise é selecionado.</span><span class="sxs-lookup"><span data-stu-id="30ac2-141">hello Smart Diagnostics option in Analytics settings is selected.</span></span> 
 * <span data-ttu-id="30ac2-142">Eixo de tempo: Olá eixo x do gráfico de saudação deve ser do tipo `datetime`.</span><span class="sxs-lookup"><span data-stu-id="30ac2-142">Time axis: hello X-axis of hello chart must be of type `datetime`.</span></span>
 * <span data-ttu-id="30ac2-143">Gráfico de linha ou área: o diagnóstico funciona somente com esses tipos de gráfico.</span><span class="sxs-lookup"><span data-stu-id="30ac2-143">Line or area chart: Diagnostics only works these types of chart.</span></span> <span data-ttu-id="30ac2-144">Use `| render timechart` ou `| render areachart` no final de saudação de sua consulta; ou selecione a linha ou um gráfico de área de seletor de lista suspensa de saudação.</span><span class="sxs-lookup"><span data-stu-id="30ac2-144">Use `| render timechart` or `| render areachart` at hello end of your query; or select Line or Area Chart from hello drop-down selector.</span></span>
 * <span data-ttu-id="30ac2-145">Descontinuidade: Deve haver uma interrupção significativa nos dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="30ac2-145">Discontinuity: There must be a significant discontinuity in hello data.</span></span>
 * <span data-ttu-id="30ac2-146">Tooanalyze de pontos suficientes.</span><span class="sxs-lookup"><span data-stu-id="30ac2-146">Sufficient points tooanalyze.</span></span>
 * <span data-ttu-id="30ac2-147">Não mais de um resumir cláusula na consulta de saudação.</span><span class="sxs-lookup"><span data-stu-id="30ac2-147">No more than one summarize clause in hello query.</span></span>
 * <span data-ttu-id="30ac2-148">Nenhuma cláusula de projeto que contém uma definição de nome antes de saudação resumir cláusula.</span><span class="sxs-lookup"><span data-stu-id="30ac2-148">No project clause that contains a name definition before hello summarize clause.</span></span>

 
 ## <a name="related-articles"></a><span data-ttu-id="30ac2-149">Artigos relacionados</span><span class="sxs-lookup"><span data-stu-id="30ac2-149">Related articles</span></span>

 * [<span data-ttu-id="30ac2-150">Tutorial do Analytics</span><span class="sxs-lookup"><span data-stu-id="30ac2-150">Analytics tutorial</span></span>](app-insights-analytics-tour.md)
 * <span data-ttu-id="30ac2-151">[Detecção de Smart](app-insights-proactive-diagnostics.md) alerta automaticamente tooperformance problemas.</span><span class="sxs-lookup"><span data-stu-id="30ac2-151">[Smart detection](app-insights-proactive-diagnostics.md) automatically alerts you tooperformance issues.</span></span>
