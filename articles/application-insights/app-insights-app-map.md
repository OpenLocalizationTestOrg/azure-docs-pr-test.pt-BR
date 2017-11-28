---
title: aaaApplication mapa no Azure Application Insights | Microsoft Docs
description: "Uma apresentação visual de dependências de saudação entre componentes de aplicativo, rotulado com KPIs e alertas."
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
ms.openlocfilehash: 96ab753a100ea53ec7d367e3559b6622ab6fd182
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="application-map-in-application-insights"></a><span data-ttu-id="9450b-103">Mapa de Aplicativos no Application Insights</span><span class="sxs-lookup"><span data-stu-id="9450b-103">Application Map in Application Insights</span></span>
<span data-ttu-id="9450b-104">Em [Azure Application Insights](app-insights-overview.md), mapa de aplicativo é um layout visual de relações de dependência de saudação de componentes do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9450b-104">In [Azure Application Insights](app-insights-overview.md), Application Map is a visual layout of hello dependency relationships of your application components.</span></span> <span data-ttu-id="9450b-105">Cada componente mostra KPIs como toohelp de carga, desempenho, falhas e alertas, você descobrir qualquer componente causando um problema de desempenho ou falha.</span><span class="sxs-lookup"><span data-stu-id="9450b-105">Each component shows KPIs such as load, performance, failures, and alerts, toohelp you discover any component causing a performance issue or failure.</span></span> <span data-ttu-id="9450b-106">Você pode clicar por meio de qualquer componente toomore detalhadas de diagnóstico, como eventos do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="9450b-106">You can click through from any component toomore detailed diagnostics, such as Application Insights events.</span></span> <span data-ttu-id="9450b-107">Se seu aplicativo usa os serviços do Azure, você também pode clicar tooAzure diagnóstico, como as recomendações do Orientador de banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="9450b-107">If your app uses Azure services, you can also click through tooAzure diagnostics, such as SQL Database Advisor recommendations.</span></span>

<span data-ttu-id="9450b-108">Como outros gráficos, você pode fixar um toohello de mapa de aplicativo do painel do Azure, onde ela será totalmente funcional.</span><span class="sxs-lookup"><span data-stu-id="9450b-108">Like other charts, you can pin an application map toohello Azure dashboard, where it is fully functional.</span></span> 

## <a name="open-hello-application-map"></a><span data-ttu-id="9450b-109">Mapa de aplicativo hello aberto</span><span class="sxs-lookup"><span data-stu-id="9450b-109">Open hello application map</span></span>
<span data-ttu-id="9450b-110">Olá abrir o mapa da folha de visão geral de saudação para seu aplicativo:</span><span class="sxs-lookup"><span data-stu-id="9450b-110">Open hello map from hello overview blade for your application:</span></span>

![abrir mapa de aplicativos](./media/app-insights-app-map/01.png)

![mapa de aplicativos](./media/app-insights-app-map/02.png)

<span data-ttu-id="9450b-113">mapa de saudação mostra:</span><span class="sxs-lookup"><span data-stu-id="9450b-113">hello map shows:</span></span>

* <span data-ttu-id="9450b-114">Testes de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="9450b-114">Availability tests</span></span>
* <span data-ttu-id="9450b-115">Componente do lado do cliente (monitorado com hello SDK de JavaScript)</span><span class="sxs-lookup"><span data-stu-id="9450b-115">Client-side component (monitored with hello JavaScript SDK)</span></span>
* <span data-ttu-id="9450b-116">Componente do lado do servidor</span><span class="sxs-lookup"><span data-stu-id="9450b-116">Server-side component</span></span>
* <span data-ttu-id="9450b-117">Dependências de componentes de cliente e servidor de saudação</span><span class="sxs-lookup"><span data-stu-id="9450b-117">Dependencies of hello client and server components</span></span>

<span data-ttu-id="9450b-118">Você pode expandir e recolher grupos de link de dependência:</span><span class="sxs-lookup"><span data-stu-id="9450b-118">You can expand and collapse dependency link groups:</span></span>

![recolher](./media/app-insights-app-map/03.png)

<span data-ttu-id="9450b-120">Se você tiver muitas dependências de um tipo (SQL, HTTP, etc.), elas poderão aparecer agrupadas.</span><span class="sxs-lookup"><span data-stu-id="9450b-120">If you have many dependencies of one type (SQL, HTTP etc.), they may appear grouped.</span></span> 

![dependências agrupadas](./media/app-insights-app-map/03-2.png)

## <a name="spot-problems"></a><span data-ttu-id="9450b-122">Identificar problemas</span><span class="sxs-lookup"><span data-stu-id="9450b-122">Spot problems</span></span>
<span data-ttu-id="9450b-123">Cada nó tem indicadores de desempenho relevantes, como taxas de falha de carga e desempenho Olá para esse componente.</span><span class="sxs-lookup"><span data-stu-id="9450b-123">Each node has relevant performance indicators, such as hello load, performance, and failure rates for that component.</span></span> 

<span data-ttu-id="9450b-124">Ícones de aviso destacam possíveis problemas.</span><span class="sxs-lookup"><span data-stu-id="9450b-124">Warning icons highlight possible problems.</span></span> <span data-ttu-id="9450b-125">Um aviso laranja significa que existem falhas em solicitações, exibições de página ou chamadas de dependência.</span><span class="sxs-lookup"><span data-stu-id="9450b-125">An orange warning means there are failures in requests, page views or dependency calls.</span></span> <span data-ttu-id="9450b-126">Vermelho significa uma taxa de falha acima de 5%.</span><span class="sxs-lookup"><span data-stu-id="9450b-126">Red means a failure rate above 5%.</span></span> <span data-ttu-id="9450b-127">Se você quiser tooadjust esses limites, abra Opções.</span><span class="sxs-lookup"><span data-stu-id="9450b-127">If you want tooadjust these thresholds, open Options.</span></span>

![ícones de falha](./media/app-insights-app-map/04.png)

<span data-ttu-id="9450b-129">Alertas ativos também aparecem:</span><span class="sxs-lookup"><span data-stu-id="9450b-129">Active alerts also show up:</span></span> 

![alertas ativos](./media/app-insights-app-map/05.png)

<span data-ttu-id="9450b-131">Se você usa o SQL Azure, há um ícone que mostra quando há recomendações sobre como melhorar o desempenho.</span><span class="sxs-lookup"><span data-stu-id="9450b-131">If you use SQL Azure, there's an icon that shows when there are recommendations on how you can improve performance.</span></span> 

![Recomendações do Azure](./media/app-insights-app-map/06.png)

<span data-ttu-id="9450b-133">Clique em qualquer ícone tooget mais detalhes:</span><span class="sxs-lookup"><span data-stu-id="9450b-133">Click any icon tooget more details:</span></span>

![Recomendações do Azure](./media/app-insights-app-map/07.png)

## <a name="diagnostic-click-through"></a><span data-ttu-id="9450b-135">Clique para Diagnóstico</span><span class="sxs-lookup"><span data-stu-id="9450b-135">Diagnostic click through</span></span>
<span data-ttu-id="9450b-136">Cada um de nós de saudação no mapa de saudação oferece destino de cliques para diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="9450b-136">Each of hello nodes on hello map offers targeted click through for diagnostics.</span></span> <span data-ttu-id="9450b-137">Opções de saudação variam dependendo do tipo de saudação do nó de saudação.</span><span class="sxs-lookup"><span data-stu-id="9450b-137">hello options vary depending on hello type of hello node.</span></span>

![opções de servidor](./media/app-insights-app-map/09.png)

<span data-ttu-id="9450b-139">Para componentes que são hospedadas no Azure, as opções de saudação incluem toothem links diretos.</span><span class="sxs-lookup"><span data-stu-id="9450b-139">For components that are hosted in Azure, hello options include direct links toothem.</span></span>

## <a name="filters-and-time-range"></a><span data-ttu-id="9450b-140">Filtros e o intervalo de tempo</span><span class="sxs-lookup"><span data-stu-id="9450b-140">Filters and time range</span></span>
<span data-ttu-id="9450b-141">Por padrão, o mapa de Olá resume todos os dados de saudação disponíveis para Olá escolhido o intervalo de tempo.</span><span class="sxs-lookup"><span data-stu-id="9450b-141">By default, hello map summarizes all hello data available for hello chosen time range.</span></span> <span data-ttu-id="9450b-142">Mas você pode filtrar nomes de operação específica somente tooinclude ou dependências.</span><span class="sxs-lookup"><span data-stu-id="9450b-142">But you can filter it tooinclude only specific operation names or dependencies.</span></span>

* <span data-ttu-id="9450b-143">Nome da operação: isso inclui tipos de solicitação do lado servidor e exibições de página.</span><span class="sxs-lookup"><span data-stu-id="9450b-143">Operation name: This includes both page views and server-side request types.</span></span> <span data-ttu-id="9450b-144">Com essa opção, a saudação mapa mostra Olá KPI no nó de servidor/cliente Olá Olá selecionada apenas para operações.</span><span class="sxs-lookup"><span data-stu-id="9450b-144">With this option, hello map shows hello KPI on hello server/client-side node for hello selected operations only.</span></span> <span data-ttu-id="9450b-145">Ele mostra dependências Olá chamadas no contexto de saudação dessas operações específicas.</span><span class="sxs-lookup"><span data-stu-id="9450b-145">It shows hello dependencies called in hello context of those specific operations.</span></span>
* <span data-ttu-id="9450b-146">Nome de base de dependência: Isso inclui Olá AJAX navegador dependências e do lado do servidor.</span><span class="sxs-lookup"><span data-stu-id="9450b-146">Dependency base name: This includes hello AJAX browser dependencies and server-side dependencies.</span></span> <span data-ttu-id="9450b-147">Se o relatório de telemetria de dependência personalizada com hello TrackDependency API, elas também aparecerão aqui.</span><span class="sxs-lookup"><span data-stu-id="9450b-147">If you report custom dependency telemetry with hello TrackDependency API, they also appear here.</span></span> <span data-ttu-id="9450b-148">Você pode selecionar Olá dependências tooshow no mapa de saudação.</span><span class="sxs-lookup"><span data-stu-id="9450b-148">You can select hello dependencies tooshow on hello map.</span></span> <span data-ttu-id="9450b-149">Atualmente esta seleção não filtrar solicitações do lado do servidor de saudação ou exibições saudação do cliente.</span><span class="sxs-lookup"><span data-stu-id="9450b-149">Currently this selection does not filter hello server-side requests, or hello client-side page views.</span></span>

![Definir filtros](./media/app-insights-app-map/11.png)

## <a name="save-filters"></a><span data-ttu-id="9450b-151">Salvar filtros</span><span class="sxs-lookup"><span data-stu-id="9450b-151">Save filters</span></span>
<span data-ttu-id="9450b-152">filtros de saudação toosave você aplicou, Olá pin filtrados exibição para um [painel](app-insights-dashboards.md).</span><span class="sxs-lookup"><span data-stu-id="9450b-152">toosave hello filters you have applied, pin hello filtered view onto a [dashboard](app-insights-dashboards.md).</span></span>

![PIN toodashboard](./media/app-insights-app-map/12.png)

## <a name="error-pane"></a><span data-ttu-id="9450b-154">Painel de erros</span><span class="sxs-lookup"><span data-stu-id="9450b-154">Error pane</span></span>
<span data-ttu-id="9450b-155">Quando você clica em um nó no mapa Olá, um painel de erro é exibido no lado direito de saudação resumindo falhas para esse nó.</span><span class="sxs-lookup"><span data-stu-id="9450b-155">When you click a node in hello map, an error pane is displayed on hello right-hand side summarizing failures for that node.</span></span> <span data-ttu-id="9450b-156">As falhas são agrupadas primeiro segundo a ID da operação e, em seguida, segundo a ID do problema.</span><span class="sxs-lookup"><span data-stu-id="9450b-156">Failures are grouped first by operation ID and then grouped by problem ID.</span></span>

![Painel de erros](./media/app-insights-app-map/error-pane.png)

<span data-ttu-id="9450b-158">Clicando em uma falha de usa a instância mais recente toohello essa falha.</span><span class="sxs-lookup"><span data-stu-id="9450b-158">Clicking on a failure takes you toohello most recent instance of that failure.</span></span>

## <a name="resource-health"></a><span data-ttu-id="9450b-159">Integridade de recursos</span><span class="sxs-lookup"><span data-stu-id="9450b-159">Resource health</span></span>
<span data-ttu-id="9450b-160">Para alguns tipos de recurso, integridade de recursos é exibida na parte superior de saudação do painel de erro hello.</span><span class="sxs-lookup"><span data-stu-id="9450b-160">For some resource types, resource health is displayed at hello top of hello error pane.</span></span> <span data-ttu-id="9450b-161">Por exemplo, clicando em um nó do SQL mostrará integridade de banco de dados de saudação e todos os alertas que tenham disparado.</span><span class="sxs-lookup"><span data-stu-id="9450b-161">For example, clicking a SQL node will show hello database health and any alerts that have fired.</span></span>

![Integridade de recursos](./media/app-insights-app-map/resource-health.png)

<span data-ttu-id="9450b-163">Você pode clicar em métricas de visão geral padrão de tooview Olá recursos nome para esse recurso.</span><span class="sxs-lookup"><span data-stu-id="9450b-163">You can click hello resource name tooview standard overview metrics for that resource.</span></span>

## <a name="end-to-end-system-app-maps"></a><span data-ttu-id="9450b-164">Mapas de aplicativos do sistema de ponta a ponta</span><span class="sxs-lookup"><span data-stu-id="9450b-164">End-to-end system app maps</span></span>

<span data-ttu-id="9450b-165">*Requer o SDK versão 2.3 ou superior*</span><span class="sxs-lookup"><span data-stu-id="9450b-165">*Requires SDK version 2.3 or higher*</span></span>

<span data-ttu-id="9450b-166">Se seu aplicativo tiver vários componentes - por exemplo, um serviço back-end além de aplicativo da web de toohello - em seguida, você pode mostrá-los todos no mapa de um aplicativo integrado.</span><span class="sxs-lookup"><span data-stu-id="9450b-166">If your application has several components - for example, a back-end service in addition toohello web app - then you can show them all on one integrated app map.</span></span>

![Definir filtros](./media/app-insights-app-map/multi-component-app-map.png)

<span data-ttu-id="9450b-168">mapa de aplicativo Hello localiza nós de servidor seguindo qualquer chamada de dependência HTTP feita entre os servidores com hello que Application Insights SDK instalado.</span><span class="sxs-lookup"><span data-stu-id="9450b-168">hello app map finds server nodes by following any HTTP dependency calls made between servers with hello Application Insights SDK installed.</span></span> <span data-ttu-id="9450b-169">Cada recurso do Application Insights será considerado toocontain um servidor.</span><span class="sxs-lookup"><span data-stu-id="9450b-169">Each Application Insights resource is assumed toocontain one server.</span></span>

### <a name="multi-role-app-map-preview"></a><span data-ttu-id="9450b-170">Mapa do aplicativo com várias funções (versão prévia)</span><span class="sxs-lookup"><span data-stu-id="9450b-170">Multi-role app map (preview)</span></span>

<span data-ttu-id="9450b-171">recurso de mapa de aplicativo de várias funções de visualização Olá permite toouse Olá aplicativo mapa com vários servidores de envio de dados toohello mesmo recurso Application Insights / chave de instrumentação.</span><span class="sxs-lookup"><span data-stu-id="9450b-171">hello preview multi-role app map feature allows you toouse hello app map with multiple servers sending data toohello same Application Insights resource  / instrumentation key.</span></span> <span data-ttu-id="9450b-172">Servidores no mapa de saudação são segmentadas por propriedade de cloud_RoleName Olá em itens de telemetria.</span><span class="sxs-lookup"><span data-stu-id="9450b-172">Servers in hello map are segmented by hello cloud_RoleName property on telemetry items.</span></span> <span data-ttu-id="9450b-173">Definir *mapa de aplicativos de várias funções* muito*na* de Olá visualizações folha tooenable essa configuração.</span><span class="sxs-lookup"><span data-stu-id="9450b-173">Set *Multi-role Application Map* too*On* from hello Previews blade tooenable this configuration.</span></span>

<span data-ttu-id="9450b-174">Essa abordagem pode ser desejável em um aplicativo de microsserviços ou em outros cenários onde você deseja toocorrelate eventos em vários servidores em um único recurso do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="9450b-174">This approach may be desired in a micro-services application, or in other scenarios where you want toocorrelate events across multiple servers within a single Application Insights resource.</span></span>

## <a name="video"></a><span data-ttu-id="9450b-175">Vídeo</span><span class="sxs-lookup"><span data-stu-id="9450b-175">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player] 

## <a name="feedback"></a><span data-ttu-id="9450b-176">Comentários</span><span class="sxs-lookup"><span data-stu-id="9450b-176">Feedback</span></span>
<span data-ttu-id="9450b-177">Forneça comentários por meio da opção de comentários do portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="9450b-177">Please provide feedback through hello portal feedback option.</span></span>

![Imagem de MapLink-1](./media/app-insights-app-map/13.png)


## <a name="next-steps"></a><span data-ttu-id="9450b-179">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9450b-179">Next steps</span></span>

* [<span data-ttu-id="9450b-180">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="9450b-180">Azure portal</span></span>](https://portal.azure.com)
