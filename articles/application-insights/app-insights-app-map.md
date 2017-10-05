---
title: Mapa de aplicativos no Azure Application Insights | Microsoft Docs
description: "Uma apresentação visual das dependências entre componentes do aplicativo, rotuladas com alertas e KPIs."
services: application-insights
documentationcenter: 
author: SoubhagyaDash
manager: carmonm
ms.assetid: 3bf37fe9-70d7-4229-98d6-4f624d256c36
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 207526b7a675f92134d045ebefb9a372749bce92
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="application-map-in-application-insights"></a><span data-ttu-id="6eacd-103">Mapa de Aplicativos no Application Insights</span><span class="sxs-lookup"><span data-stu-id="6eacd-103">Application Map in Application Insights</span></span>
<span data-ttu-id="6eacd-104">No [Azure Application Insights](app-insights-overview.md), o Mapa de Aplicativos é um layout visual das relações de dependência dos componentes de seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6eacd-104">In [Azure Application Insights](app-insights-overview.md), Application Map is a visual layout of the dependency relationships of your application components.</span></span> <span data-ttu-id="6eacd-105">Cada componente mostra KPIs, como carga, desempenho, falhas e alertas, para ajudá-lo a descobrir possíveis componentes que estejam causando uma falha ou um problema de desempenho.</span><span class="sxs-lookup"><span data-stu-id="6eacd-105">Each component shows KPIs such as load, performance, failures, and alerts, to help you discover any component causing a performance issue or failure.</span></span> <span data-ttu-id="6eacd-106">Você pode clicar em qualquer componente para obter diagnóstico mais detalhado, como eventos do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="6eacd-106">You can click through from any component to more detailed diagnostics, such as Application Insights events.</span></span> <span data-ttu-id="6eacd-107">Se seu aplicativo usar os serviços do Azure, você também poderá clicar no diagnóstico do Azure, como nas recomendações do Assistente do Banco de Dados SQL.</span><span class="sxs-lookup"><span data-stu-id="6eacd-107">If your app uses Azure services, you can also click through to Azure diagnostics, such as SQL Database Advisor recommendations.</span></span>

<span data-ttu-id="6eacd-108">Assim como outros gráficos, você pode fixar um mapa de aplicativos no painel do Azure, onde ele fica totalmente funcional.</span><span class="sxs-lookup"><span data-stu-id="6eacd-108">Like other charts, you can pin an application map to the Azure dashboard, where it is fully functional.</span></span> 

## <a name="open-the-application-map"></a><span data-ttu-id="6eacd-109">Abrir o mapa de aplicativos</span><span class="sxs-lookup"><span data-stu-id="6eacd-109">Open the application map</span></span>
<span data-ttu-id="6eacd-110">Abra o mapa na folha de visão geral do seu aplicativo:</span><span class="sxs-lookup"><span data-stu-id="6eacd-110">Open the map from the overview blade for your application:</span></span>

![abrir mapa de aplicativos](./media/app-insights-app-map/01.png)

![mapa de aplicativos](./media/app-insights-app-map/02.png)

<span data-ttu-id="6eacd-113">O mapa mostra:</span><span class="sxs-lookup"><span data-stu-id="6eacd-113">The map shows:</span></span>

* <span data-ttu-id="6eacd-114">Testes de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="6eacd-114">Availability tests</span></span>
* <span data-ttu-id="6eacd-115">Componente do lado do cliente (monitorado com o SDK do JavaScript)</span><span class="sxs-lookup"><span data-stu-id="6eacd-115">Client-side component (monitored with the JavaScript SDK)</span></span>
* <span data-ttu-id="6eacd-116">Componente do lado do servidor</span><span class="sxs-lookup"><span data-stu-id="6eacd-116">Server-side component</span></span>
* <span data-ttu-id="6eacd-117">Dependências dos componentes do cliente e do servidor</span><span class="sxs-lookup"><span data-stu-id="6eacd-117">Dependencies of the client and server components</span></span>

<span data-ttu-id="6eacd-118">Você pode expandir e recolher grupos de link de dependência:</span><span class="sxs-lookup"><span data-stu-id="6eacd-118">You can expand and collapse dependency link groups:</span></span>

![recolher](./media/app-insights-app-map/03.png)

<span data-ttu-id="6eacd-120">Se você tiver muitas dependências de um tipo (SQL, HTTP, etc.), elas poderão aparecer agrupadas.</span><span class="sxs-lookup"><span data-stu-id="6eacd-120">If you have many dependencies of one type (SQL, HTTP etc.), they may appear grouped.</span></span> 

![dependências agrupadas](./media/app-insights-app-map/03-2.png)

## <a name="spot-problems"></a><span data-ttu-id="6eacd-122">Identificar problemas</span><span class="sxs-lookup"><span data-stu-id="6eacd-122">Spot problems</span></span>
<span data-ttu-id="6eacd-123">Cada nó possui indicadores de desempenho relevantes, como as taxas de carga, de desempenho e de falha do componente.</span><span class="sxs-lookup"><span data-stu-id="6eacd-123">Each node has relevant performance indicators, such as the load, performance, and failure rates for that component.</span></span> 

<span data-ttu-id="6eacd-124">Ícones de aviso destacam possíveis problemas.</span><span class="sxs-lookup"><span data-stu-id="6eacd-124">Warning icons highlight possible problems.</span></span> <span data-ttu-id="6eacd-125">Um aviso laranja significa que existem falhas em solicitações, exibições de página ou chamadas de dependência.</span><span class="sxs-lookup"><span data-stu-id="6eacd-125">An orange warning means there are failures in requests, page views or dependency calls.</span></span> <span data-ttu-id="6eacd-126">Vermelho significa uma taxa de falha acima de 5%.</span><span class="sxs-lookup"><span data-stu-id="6eacd-126">Red means a failure rate above 5%.</span></span> <span data-ttu-id="6eacd-127">Se você quiser ajustar esses limites, abra Opções.</span><span class="sxs-lookup"><span data-stu-id="6eacd-127">If you want to adjust these thresholds, open Options.</span></span>

![ícones de falha](./media/app-insights-app-map/04.png)

<span data-ttu-id="6eacd-129">Alertas ativos também aparecem:</span><span class="sxs-lookup"><span data-stu-id="6eacd-129">Active alerts also show up:</span></span> 

![alertas ativos](./media/app-insights-app-map/05.png)

<span data-ttu-id="6eacd-131">Se você usa o SQL Azure, há um ícone que mostra quando há recomendações sobre como melhorar o desempenho.</span><span class="sxs-lookup"><span data-stu-id="6eacd-131">If you use SQL Azure, there's an icon that shows when there are recommendations on how you can improve performance.</span></span> 

![Recomendações do Azure](./media/app-insights-app-map/06.png)

<span data-ttu-id="6eacd-133">Clique em um ícone para obter mais detalhes:</span><span class="sxs-lookup"><span data-stu-id="6eacd-133">Click any icon to get more details:</span></span>

![Recomendações do Azure](./media/app-insights-app-map/07.png)

## <a name="diagnostic-click-through"></a><span data-ttu-id="6eacd-135">Clique para Diagnóstico</span><span class="sxs-lookup"><span data-stu-id="6eacd-135">Diagnostic click through</span></span>
<span data-ttu-id="6eacd-136">Cada um dos nós no mapa oferece cliques direcionados para diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="6eacd-136">Each of the nodes on the map offers targeted click through for diagnostics.</span></span> <span data-ttu-id="6eacd-137">As opções variam dependendo do tipo de nó.</span><span class="sxs-lookup"><span data-stu-id="6eacd-137">The options vary depending on the type of the node.</span></span>

![opções de servidor](./media/app-insights-app-map/09.png)

<span data-ttu-id="6eacd-139">Para componentes que são hospedados no Azure, as opções incluem links diretos para eles.</span><span class="sxs-lookup"><span data-stu-id="6eacd-139">For components that are hosted in Azure, the options include direct links to them.</span></span>

## <a name="filters-and-time-range"></a><span data-ttu-id="6eacd-140">Filtros e o intervalo de tempo</span><span class="sxs-lookup"><span data-stu-id="6eacd-140">Filters and time range</span></span>
<span data-ttu-id="6eacd-141">Por padrão, o mapa resume todos os dados disponíveis para o intervalo de tempo escolhido.</span><span class="sxs-lookup"><span data-stu-id="6eacd-141">By default, the map summarizes all the data available for the chosen time range.</span></span> <span data-ttu-id="6eacd-142">Mas você pode filtrá-lo para incluir apenas nomes de operação ou dependências específicas.</span><span class="sxs-lookup"><span data-stu-id="6eacd-142">But you can filter it to include only specific operation names or dependencies.</span></span>

* <span data-ttu-id="6eacd-143">Nome da operação: isso inclui tipos de solicitação do lado servidor e exibições de página.</span><span class="sxs-lookup"><span data-stu-id="6eacd-143">Operation name: This includes both page views and server-side request types.</span></span> <span data-ttu-id="6eacd-144">Com essa opção, o mapa mostra o KPI no nó do lado do servidor/cliente somente para operações selecionadas.</span><span class="sxs-lookup"><span data-stu-id="6eacd-144">With this option, the map shows the KPI on the server/client-side node for the selected operations only.</span></span> <span data-ttu-id="6eacd-145">Ele mostra as dependências chamadas no contexto dessas operações específicas.</span><span class="sxs-lookup"><span data-stu-id="6eacd-145">It shows the dependencies called in the context of those specific operations.</span></span>
* <span data-ttu-id="6eacd-146">Nome base de dependência: isso inclui as dependências de navegador do AJAX e dependências do lado do servidor.</span><span class="sxs-lookup"><span data-stu-id="6eacd-146">Dependency base name: This includes the AJAX browser dependencies and server-side dependencies.</span></span> <span data-ttu-id="6eacd-147">Se você relatar telemetria de dependência personalizada com a API TrackDependency, ela também será exibida aqui.</span><span class="sxs-lookup"><span data-stu-id="6eacd-147">If you report custom dependency telemetry with the TrackDependency API, they also appear here.</span></span> <span data-ttu-id="6eacd-148">Você pode selecionar quais dependências mostrar no mapa.</span><span class="sxs-lookup"><span data-stu-id="6eacd-148">You can select the dependencies to show on the map.</span></span> <span data-ttu-id="6eacd-149">Atualmente, essa seleção não filtra as solicitações do lado do servidor nem as exibições de página do lado do cliente.</span><span class="sxs-lookup"><span data-stu-id="6eacd-149">Currently this selection does not filter the server-side requests, or the client-side page views.</span></span>

![Definir filtros](./media/app-insights-app-map/11.png)

## <a name="save-filters"></a><span data-ttu-id="6eacd-151">Salvar filtros</span><span class="sxs-lookup"><span data-stu-id="6eacd-151">Save filters</span></span>
<span data-ttu-id="6eacd-152">Para salvar os filtros que você aplicou, fixe na exibição filtrada em um [painel](app-insights-dashboards.md).</span><span class="sxs-lookup"><span data-stu-id="6eacd-152">To save the filters you have applied, pin the filtered view onto a [dashboard](app-insights-dashboards.md).</span></span>

![Fixar no painel](./media/app-insights-app-map/12.png)

## <a name="error-pane"></a><span data-ttu-id="6eacd-154">Painel de erros</span><span class="sxs-lookup"><span data-stu-id="6eacd-154">Error pane</span></span>
<span data-ttu-id="6eacd-155">Quando você clica em um nó no mapa, é exibido no lado direito um painel de erros resumindo as falhas do nó.</span><span class="sxs-lookup"><span data-stu-id="6eacd-155">When you click a node in the map, an error pane is displayed on the right-hand side summarizing failures for that node.</span></span> <span data-ttu-id="6eacd-156">As falhas são agrupadas primeiro segundo a ID da operação e, em seguida, segundo a ID do problema.</span><span class="sxs-lookup"><span data-stu-id="6eacd-156">Failures are grouped first by operation ID and then grouped by problem ID.</span></span>

![Painel de erros](./media/app-insights-app-map/error-pane.png)

<span data-ttu-id="6eacd-158">Clicar em uma falha leva você até a instância mais recente dessa falha.</span><span class="sxs-lookup"><span data-stu-id="6eacd-158">Clicking on a failure takes you to the most recent instance of that failure.</span></span>

## <a name="resource-health"></a><span data-ttu-id="6eacd-159">Integridade de recursos</span><span class="sxs-lookup"><span data-stu-id="6eacd-159">Resource health</span></span>
<span data-ttu-id="6eacd-160">Para alguns tipos de recursos, sua integridade é exibida na parte superior do painel de erros.</span><span class="sxs-lookup"><span data-stu-id="6eacd-160">For some resource types, resource health is displayed at the top of the error pane.</span></span> <span data-ttu-id="6eacd-161">Por exemplo, clicar em um nó do SQL mostrará a integridade do banco de dados e todos os alertas que tiverem sido disparados.</span><span class="sxs-lookup"><span data-stu-id="6eacd-161">For example, clicking a SQL node will show the database health and any alerts that have fired.</span></span>

![Integridade de recursos](./media/app-insights-app-map/resource-health.png)

<span data-ttu-id="6eacd-163">Você pode clicar no nome do recurso para exibir as métricas de visão geral padrão para esse recurso.</span><span class="sxs-lookup"><span data-stu-id="6eacd-163">You can click the resource name to view standard overview metrics for that resource.</span></span>

## <a name="end-to-end-system-app-maps"></a><span data-ttu-id="6eacd-164">Mapas de aplicativos do sistema de ponta a ponta</span><span class="sxs-lookup"><span data-stu-id="6eacd-164">End-to-end system app maps</span></span>

<span data-ttu-id="6eacd-165">*Requer o SDK versão 2.3 ou superior*</span><span class="sxs-lookup"><span data-stu-id="6eacd-165">*Requires SDK version 2.3 or higher*</span></span>

<span data-ttu-id="6eacd-166">Se seu aplicativo tiver vários componentes (por exemplo, um serviço de back-end além do aplicativo Web), você poderá mostrá-los em um mapa de aplicativos integrado.</span><span class="sxs-lookup"><span data-stu-id="6eacd-166">If your application has several components - for example, a back-end service in addition to the web app - then you can show them all on one integrated app map.</span></span>

![Definir filtros](./media/app-insights-app-map/multi-component-app-map.png)

<span data-ttu-id="6eacd-168">O mapa do aplicativo localiza os nós do servidor seguindo qualquer chamada de dependência HTTP feita entre os servidores com o SDK do Application Insights instalado.</span><span class="sxs-lookup"><span data-stu-id="6eacd-168">The app map finds server nodes by following any HTTP dependency calls made between servers with the Application Insights SDK installed.</span></span> <span data-ttu-id="6eacd-169">Presume-se que cada recurso do Application Insights contenha um servidor.</span><span class="sxs-lookup"><span data-stu-id="6eacd-169">Each Application Insights resource is assumed to contain one server.</span></span>

### <a name="multi-role-app-map-preview"></a><span data-ttu-id="6eacd-170">Mapa do aplicativo com várias funções (versão prévia)</span><span class="sxs-lookup"><span data-stu-id="6eacd-170">Multi-role app map (preview)</span></span>

<span data-ttu-id="6eacd-171">O recurso de mapa do aplicativo com várias funções, em fase de versão prévia, permite usar o mapa do aplicativo com vários servidores enviando dados à mesma chave de instrumentação/recurso do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="6eacd-171">The preview multi-role app map feature allows you to use the app map with multiple servers sending data to the same Application Insights resource  / instrumentation key.</span></span> <span data-ttu-id="6eacd-172">Os servidores no mapa são segmentados segundo a propriedade cloud_RoleName nos itens de telemetria.</span><span class="sxs-lookup"><span data-stu-id="6eacd-172">Servers in the map are segmented by the cloud_RoleName property on telemetry items.</span></span> <span data-ttu-id="6eacd-173">Defina *Mapa do Aplicativo com Várias Funções* como *Ativado* na folha Versões prévias para habilitar essa configuração.</span><span class="sxs-lookup"><span data-stu-id="6eacd-173">Set *Multi-role Application Map* to *On* from the Previews blade to enable this configuration.</span></span>

<span data-ttu-id="6eacd-174">Essa abordagem pode ser desejável em um aplicativo de microsserviço ou em outros cenários em que você deseja correlacionar eventos entre vários servidores dentro de um único recurso do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="6eacd-174">This approach may be desired in a micro-services application, or in other scenarios where you want to correlate events across multiple servers within a single Application Insights resource.</span></span>

## <a name="video"></a><span data-ttu-id="6eacd-175">Vídeo</span><span class="sxs-lookup"><span data-stu-id="6eacd-175">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player] 

## <a name="feedback"></a><span data-ttu-id="6eacd-176">Comentários</span><span class="sxs-lookup"><span data-stu-id="6eacd-176">Feedback</span></span>
<span data-ttu-id="6eacd-177">Por favor, faça comentários por meio da opção Comentários no portal.</span><span class="sxs-lookup"><span data-stu-id="6eacd-177">Please provide feedback through the portal feedback option.</span></span>

![Imagem de MapLink-1](./media/app-insights-app-map/13.png)


## <a name="next-steps"></a><span data-ttu-id="6eacd-179">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6eacd-179">Next steps</span></span>

* [<span data-ttu-id="6eacd-180">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="6eacd-180">Azure portal</span></span>](https://portal.azure.com)
