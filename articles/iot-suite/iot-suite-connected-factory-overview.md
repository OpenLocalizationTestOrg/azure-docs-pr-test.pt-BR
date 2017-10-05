---
title: "Visão geral de fábrica conectada do Azure IoT Suite | Microsoft Docs"
description: "Uma descrição da solução pré-configurada de fábrica conectada do Azure IoT Suite."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 
ms.service: iot-suite
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/27/2017
ms.author: dobett
ms.openlocfilehash: d502c8e2e2715899279f6ebcf7ed89c19a1bb9a6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-the-connected-factory-preconfigured-solution"></a><span data-ttu-id="52ec6-103">Introdução à solução pré-configurada de fábrica conectada</span><span class="sxs-lookup"><span data-stu-id="52ec6-103">Get started with the connected factory preconfigured solution</span></span>

<span data-ttu-id="52ec6-104">As [soluções pré-configuradas][lnk-preconfigured-solutions] do Azure IoT Suite combinam vários serviços de IoT do Azure para fornecer soluções de ponta a ponta que implementam cenários comuns de negócios de IoT.</span><span class="sxs-lookup"><span data-stu-id="52ec6-104">Azure IoT Suite [preconfigured solutions][lnk-preconfigured-solutions] combine multiple Azure IoT services to deliver end-to-end solutions that implement common IoT business scenarios.</span></span> <span data-ttu-id="52ec6-105">A solução pré-configurada de *fábrica conectada* conecta aos dispositivos industriais e os monitora.</span><span class="sxs-lookup"><span data-stu-id="52ec6-105">The *connected factory* preconfigured solution connects to and monitors your industrial devices.</span></span> <span data-ttu-id="52ec6-106">Você pode usar a solução para analisar o fluxo de dados de dispositivos e promover a lucratividade e a produtividade operacionais.</span><span class="sxs-lookup"><span data-stu-id="52ec6-106">You can use the solution to analyze the stream of data from your devices and to drive operational productivity and profitability.</span></span>

<span data-ttu-id="52ec6-107">Este tutorial mostra como provisionar a solução pré-configurada de fábrica conectada.</span><span class="sxs-lookup"><span data-stu-id="52ec6-107">This tutorial shows you how to provision the connected factory preconfigured solution.</span></span> <span data-ttu-id="52ec6-108">Ele também explica os recursos básicos da solução pré-configurada.</span><span class="sxs-lookup"><span data-stu-id="52ec6-108">It also walks you through the basic features of the preconfigured solution.</span></span> <span data-ttu-id="52ec6-109">Você pode acessar muitos desses recursos no *painel* de solução que é implantado como parte da solução pré-configurada:</span><span class="sxs-lookup"><span data-stu-id="52ec6-109">You can access many of these features from the solution *dashboard* that deploys as part of the preconfigured solution:</span></span>

![Painel de solução pré-configurada de fábrica conectada][img-cf-home]

<span data-ttu-id="52ec6-111">Para concluir este tutorial, você precisa de uma assinatura ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="52ec6-111">To complete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="52ec6-112">Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="52ec6-112">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="52ec6-113">Para obter detalhes, consulte [Avaliação gratuita do Azure][lnk_free_trial].</span><span class="sxs-lookup"><span data-stu-id="52ec6-113">For details, see [Azure Free Trial][lnk_free_trial].</span></span>
> 
> 

## <a name="provision-the-solution"></a><span data-ttu-id="52ec6-114">Provisionar a solução</span><span class="sxs-lookup"><span data-stu-id="52ec6-114">Provision the solution</span></span>

1. <span data-ttu-id="52ec6-115">Faça logon em azureiotsuite.com usando as credenciais de sua conta do Azure e clique em "**+**" para criar uma nova solução.</span><span class="sxs-lookup"><span data-stu-id="52ec6-115">Log on to azureiotsuite.com using your Azure account credentials, and click "**+**" to create a solution.</span></span>
2. <span data-ttu-id="52ec6-116">Clique em **Selecionar** no bloco **Fábrica conectada**.</span><span class="sxs-lookup"><span data-stu-id="52ec6-116">Click **Select** on the **Connected factory** tile.</span></span>
3. <span data-ttu-id="52ec6-117">Digite um **Nome de solução** para a solução pré-configurada de fábrica conectada.</span><span class="sxs-lookup"><span data-stu-id="52ec6-117">Enter a **Solution name** for your connected factory preconfigured solution.</span></span>
4. <span data-ttu-id="52ec6-118">Selecione a **Assinatura** e a **Região** que você deseja usar para provisionar a solução.</span><span class="sxs-lookup"><span data-stu-id="52ec6-118">Select the **Subscription** and **Region** you want to use to provision the solution.</span></span>
5. <span data-ttu-id="52ec6-119">Clique em **Criar Solução** para iniciar o processo de provisionamento.</span><span class="sxs-lookup"><span data-stu-id="52ec6-119">Click **Create Solution** to begin the provisioning process.</span></span> <span data-ttu-id="52ec6-120">Este processo normalmente leva vários minutos para ser executado.</span><span class="sxs-lookup"><span data-stu-id="52ec6-120">This process typically takes several minutes to run.</span></span>

### <a name="while-you-wait-for-the-provisioning-process-to-complete"></a><span data-ttu-id="52ec6-121">Enquanto você aguarda até que o processo de provisionamento seja concluído</span><span class="sxs-lookup"><span data-stu-id="52ec6-121">While you wait for the provisioning process to complete</span></span>

1. <span data-ttu-id="52ec6-122">Clique no bloco da sua solução com o status **Provisionamento** .</span><span class="sxs-lookup"><span data-stu-id="52ec6-122">Click the tile for your solution with **Provisioning** status.</span></span>
2. <span data-ttu-id="52ec6-123">Observe os **estados de Provisionamento** à medida que os serviços do Azure são implantados em sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="52ec6-123">Notice the **Provisioning states** as Azure services are deployed in your Azure subscription.</span></span>
3. <span data-ttu-id="52ec6-124">Após o provisionamento ser concluído, o status será alterado para **Pronto**.</span><span class="sxs-lookup"><span data-stu-id="52ec6-124">Once provisioning completes, the status changes to **Ready**.</span></span>
4. <span data-ttu-id="52ec6-125">Clique no bloco para ver os detalhes da solução no painel à direita.</span><span class="sxs-lookup"><span data-stu-id="52ec6-125">Click the tile to see the details of your solution in the right-hand pane.</span></span>

> [!NOTE]
> <span data-ttu-id="52ec6-126">Se estiver tendo problemas para implantar a solução pré-configurada, dê uma olhada em [Permissões no site azureiotsuite.com][lnk-permissions] e nas [Perguntas frequentes sobre fábrica conectada](iot-suite-faq-cf.md).</span><span class="sxs-lookup"><span data-stu-id="52ec6-126">If you encounter issues deploying the preconfigured solution, review [Permissions on the azureiotsuite.com site][lnk-permissions] and the [Connected factory FAQ](iot-suite-faq-cf.md).</span></span> <span data-ttu-id="52ec6-127">Se os problemas persistirem, crie um tíquete de serviço no [portal][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="52ec6-127">If the issues persist, create a service ticket on the [portal][lnk-portal].</span></span>

<span data-ttu-id="52ec6-128">Há detalhes que você esperaria ver e que não estão listados para sua solução?</span><span class="sxs-lookup"><span data-stu-id="52ec6-128">Are there details you'd expect to see that aren't listed for your solution?</span></span> <span data-ttu-id="52ec6-129">Envie sugestões de recursos no [User Voice](https://feedback.azure.com/forums/321918-azure-iot).</span><span class="sxs-lookup"><span data-stu-id="52ec6-129">Give us feature suggestions on [User Voice](https://feedback.azure.com/forums/321918-azure-iot).</span></span>

## <a name="scenario-overview"></a><span data-ttu-id="52ec6-130">Visão geral do cenário</span><span class="sxs-lookup"><span data-stu-id="52ec6-130">Scenario overview</span></span>

<span data-ttu-id="52ec6-131">Quando você implantar a solução pré-configurada de fábrica conectada, ela será pré-populada com recursos que permitem que você percorra um cenário industrial comum.</span><span class="sxs-lookup"><span data-stu-id="52ec6-131">When you deploy the connected factory preconfigured solution, it is prepopulated with resources that enable you to step through a common industrial scenario.</span></span> <span data-ttu-id="52ec6-132">Nesse cenário, várias fábricas conectadas à solução relatam os valores de dados necessários para calcular a OEE (eficiência geral de equipamentos) e KPIs (indicadores chave de desempenho).</span><span class="sxs-lookup"><span data-stu-id="52ec6-132">In this scenario, several factories connected to the solution report the data values required to compute overall equipment efficiency (OEE) and key performance indicators (KPIs).</span></span> <span data-ttu-id="52ec6-133">As seções a seguir mostram como:</span><span class="sxs-lookup"><span data-stu-id="52ec6-133">The following sections show you how to:</span></span>

* <span data-ttu-id="52ec6-134">Monitorar fábrica, linhas de produção, OEE de estação e valores de KPI</span><span class="sxs-lookup"><span data-stu-id="52ec6-134">Monitor factory, production lines, station OEE, and KPI values</span></span>
* <span data-ttu-id="52ec6-135">Analisar os dados de telemetria gerados por esses dispositivos usando Análises de Séries Temporais do Azure</span><span class="sxs-lookup"><span data-stu-id="52ec6-135">Analyze the telemetry data generated from these devices using Azure Time Series Insights</span></span>
* <span data-ttu-id="52ec6-136">Agir sobre alertas para corrigir problemas</span><span class="sxs-lookup"><span data-stu-id="52ec6-136">Act on alerts to fix issues</span></span>

<span data-ttu-id="52ec6-137">Um recurso-chave desse cenário é que você pode executar todas essas ações remotamente no painel da solução.</span><span class="sxs-lookup"><span data-stu-id="52ec6-137">A key feature of this scenario is that you can perform all these actions remotely from the solution dashboard.</span></span> <span data-ttu-id="52ec6-138">Não é necessário acesso físico aos dispositivos.</span><span class="sxs-lookup"><span data-stu-id="52ec6-138">You do not need physical access to the devices.</span></span>

## <a name="view-the-solution-dashboard"></a><span data-ttu-id="52ec6-139">Exibir o painel de solução</span><span class="sxs-lookup"><span data-stu-id="52ec6-139">View the solution dashboard</span></span>

<span data-ttu-id="52ec6-140">O painel de solução permite que você gerencie a solução implantada.</span><span class="sxs-lookup"><span data-stu-id="52ec6-140">The solution dashboard enables you to manage the deployed solution.</span></span> <span data-ttu-id="52ec6-141">É uma representação hierárquica de uma configuração global de fábrica.</span><span class="sxs-lookup"><span data-stu-id="52ec6-141">It is a hierarchical representation of a global factory configuration.</span></span> <span data-ttu-id="52ec6-142">Por exemplo, você pode exibir KPIs e OEE, publicar novos nós para alertas de telemetria e de ação.</span><span class="sxs-lookup"><span data-stu-id="52ec6-142">For example, you can view OEE and KPIs, publish new nodes for telemetry and action alerts.</span></span>

1. <span data-ttu-id="52ec6-143">Quando o provisionamento for concluído e o bloco da solução pré-configurada indicar **Pronto**, escolha **Iniciar** para abrir o portal de solução de fábrica conectada em uma nova guia.</span><span class="sxs-lookup"><span data-stu-id="52ec6-143">When the provisioning is complete and the tile for your preconfigured solution indicates **Ready**, choose **Launch** to open your connected factory solution portal in a new tab.</span></span>

    ![Iniciar a solução pré-configurada][img-launch-solution]

1. <span data-ttu-id="52ec6-145">Por padrão, o portal de solução mostra o *painel*.</span><span class="sxs-lookup"><span data-stu-id="52ec6-145">By default, the solution portal shows the *dashboard*.</span></span> <span data-ttu-id="52ec6-146">Para navegar para outras áreas do portal, use o menu no lado esquerdo da página.</span><span class="sxs-lookup"><span data-stu-id="52ec6-146">To navigate to other areas of the portal, use the menu on the left-hand side of the page.</span></span>

    ![Painel de solução pré-configurada de fábrica conectada][cf-img-menu]

<span data-ttu-id="52ec6-148">O painel exibe as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="52ec6-148">The dashboard displays the following information:</span></span>

* <span data-ttu-id="52ec6-149">Um painel **Lista de fábricas** que mostra o status, o local e a configuração atual de produção na solução.</span><span class="sxs-lookup"><span data-stu-id="52ec6-149">A **Factory list** panel that shows the status, location, and current production configuration in the solution.</span></span> <span data-ttu-id="52ec6-150">Quando você executa a solução pela primeira vez, há vários dispositivos simulados.</span><span class="sxs-lookup"><span data-stu-id="52ec6-150">When you first run the solution, there are a number of simulated devices.</span></span> <span data-ttu-id="52ec6-151">A simulação de linha de produção é composta de três servidores OPC UA reais por linha de produção que executam tarefas simuladas e compartilham dados.</span><span class="sxs-lookup"><span data-stu-id="52ec6-151">The production line simulation is composed of three real OPC UA servers per production line that perform simulated tasks and share data.</span></span> <span data-ttu-id="52ec6-152">Para obter mais informações sobre o OPC UA, consulte as [Perguntas frequentes sobre fábrica conectada](iot-suite-faq-cf.md).</span><span class="sxs-lookup"><span data-stu-id="52ec6-152">For more information about OPC UA, see the [Connected factory FAQ](iot-suite-faq-cf.md).</span></span>
* <span data-ttu-id="52ec6-153">Um **mapa** que exibe o local de cada dispositivo conectado à solução.</span><span class="sxs-lookup"><span data-stu-id="52ec6-153">A **map** that displays the location of each device connected to the solution.</span></span> <span data-ttu-id="52ec6-154">A solução pode usar a API do Bing Maps para plotar informações no mapa.</span><span class="sxs-lookup"><span data-stu-id="52ec6-154">The solution can use the Bing Maps API to plot information on the map.</span></span> <span data-ttu-id="52ec6-155">Se sua assinatura estiver habilitada para a API do Bing Maps Enterprise, esse recurso será usado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="52ec6-155">If your subscription is enabled for Bing Maps Enterprise API, then this feature is used automatically.</span></span> <span data-ttu-id="52ec6-156">Caso contrário, confira as [Perguntas frequentes][lnk-faq] para aprender a fazer o mapa dinâmico.</span><span class="sxs-lookup"><span data-stu-id="52ec6-156">If not, see the [FAQ][lnk-faq] to learn how to make the map dynamic.</span></span>
* <span data-ttu-id="52ec6-157">Um painel **Alertas** que exibe alertas gerados quando um valor KPI/OEE ou de telemetria excede um limite específico.</span><span class="sxs-lookup"><span data-stu-id="52ec6-157">An **Alerts** panel that displays alerts generated when a telemetry or OEE/KPI value exceeds a specific threshold.</span></span>
* <span data-ttu-id="52ec6-158">Um painel **Eficiência Geral de Equipamento** que mostra os valores OEE para toda a empresa ou a fábrica/produção linha/estação que você está exibindo.</span><span class="sxs-lookup"><span data-stu-id="52ec6-158">An **Overall Equipment Efficiency** panel that shows the OEE values for the whole enterprise, or the factory/production line/station you are viewing.</span></span> <span data-ttu-id="52ec6-159">Esse valor é agregado da exibição de estação para o nível corporativo.</span><span class="sxs-lookup"><span data-stu-id="52ec6-159">This value is aggregated from the station view to the enterprise level.</span></span> <span data-ttu-id="52ec6-160">A figura de OEE e seus elementos constituintes podem ser mais analisados.</span><span class="sxs-lookup"><span data-stu-id="52ec6-160">The OEE figure and its constituent elements can be further analyzed.</span></span>
* <span data-ttu-id="52ec6-161">Painel **Indicadores Chave de Desempenho** que exibe o número de unidades produzidas e a energia usada por toda a empresa ou a linha de produção/fábrica/estação que você está exibindo.</span><span class="sxs-lookup"><span data-stu-id="52ec6-161">**Key Performance Indicators** panel that displays the number of units produced and energy used by the whole enterprise or the factory/production line/station you are viewing.</span></span> <span data-ttu-id="52ec6-162">Esses valores são agregados de uma exibição de estação para o nível corporativo.</span><span class="sxs-lookup"><span data-stu-id="52ec6-162">These values are aggregated from a station view to the enterprise level.</span></span>

## <a name="view-factories"></a><span data-ttu-id="52ec6-163">Exibir fábricas</span><span class="sxs-lookup"><span data-stu-id="52ec6-163">View factories</span></span>

<span data-ttu-id="52ec6-164">O painel *Fábricas* mostra a localização geográfica de todas as fábricas da solução, seus status e a configuração de produção atual.</span><span class="sxs-lookup"><span data-stu-id="52ec6-164">The *Factories* panel shows you the geographical location of all the factories in the solution, their status, and current production configuration.</span></span> <span data-ttu-id="52ec6-165">Na lista de locais, você pode navegar para os outros níveis na hierarquia de solução.</span><span class="sxs-lookup"><span data-stu-id="52ec6-165">From the locations list, you can navigate to the other levels in the solution hierarchy.</span></span> <span data-ttu-id="52ec6-166">As linhas na lista são hiperlinks que vinculam os detalhes das linhas de produção nesse local.</span><span class="sxs-lookup"><span data-stu-id="52ec6-166">The rows in the list are hyperlinks that link details of the production lines at that location.</span></span> <span data-ttu-id="52ec6-167">Em seguida, é possível analisar os detalhes da linha de produção e a exibição de nível de estação.</span><span class="sxs-lookup"><span data-stu-id="52ec6-167">It is then possible to drill into the production line details and down to the station level view.</span></span> <span data-ttu-id="52ec6-168">Você também pode aplicar um filtro à lista.</span><span class="sxs-lookup"><span data-stu-id="52ec6-168">You can also apply a filter to the list.</span></span>

![Fábricas de solução pré-configurada de fábrica conectada][cf-img-factories] 

1. <span data-ttu-id="52ec6-170">O **painel Fábrica** mostra a lista de fábricas para essa solução.</span><span class="sxs-lookup"><span data-stu-id="52ec6-170">The **Factory panel** shows the factory list for this solution.</span></span>

2. <span data-ttu-id="52ec6-171">A lista de fábrica inicialmente mostra seis fábricas criadas pelo processo de provisionamento.</span><span class="sxs-lookup"><span data-stu-id="52ec6-171">The factory list initially shows six factories created by the provisioning process.</span></span> <span data-ttu-id="52ec6-172">Você pode adicionar dispositivos simulados e físicos extras à solução.</span><span class="sxs-lookup"><span data-stu-id="52ec6-172">You can add additional simulated and physical devices to the solution.</span></span>

3. <span data-ttu-id="52ec6-173">Para exibir os detalhes de uma fábrica, clique na linha da lista de fábricas.</span><span class="sxs-lookup"><span data-stu-id="52ec6-173">To view the details of a factory, click the row in the factory list.</span></span>

4. <span data-ttu-id="52ec6-174">Para exibir os detalhes de uma linha de produção, clique na linha na lista.</span><span class="sxs-lookup"><span data-stu-id="52ec6-174">To view the details of a production line, click the row in the list.</span></span>

5. <span data-ttu-id="52ec6-175">Para exibir os nós OPC UA publicados de uma estação na linha de produção, clique na linha na lista.</span><span class="sxs-lookup"><span data-stu-id="52ec6-175">To view the published OPC UA nodes of a station on the production line, click the row in the list.</span></span>

6. <span data-ttu-id="52ec6-176">Para exibir detalhes sobre um nó específico na estação, clique na linha na lista.</span><span class="sxs-lookup"><span data-stu-id="52ec6-176">To view details on a specific node in the station, click the row in the list.</span></span> <span data-ttu-id="52ec6-177">Essa ação abre o painel de contexto com visualizações de Informações da Série Temporal.</span><span class="sxs-lookup"><span data-stu-id="52ec6-177">This action launches the context panel with Time Series Insights visualizations.</span></span> <span data-ttu-id="52ec6-178">Clique nesses gráficos para continuar a análise no ambiente do explorador de Análises de Séries Temporais.</span><span class="sxs-lookup"><span data-stu-id="52ec6-178">Click these graphs to do further analysis in the Time Series Insights explorer environment.</span></span>

## <a name="view-map"></a><span data-ttu-id="52ec6-179">Exibir mapa</span><span class="sxs-lookup"><span data-stu-id="52ec6-179">View map</span></span>

<span data-ttu-id="52ec6-180">Se sua assinatura tiver acesso à API do Bing Maps, o mapa de *Fábricas* mostrará a localização geográfica e o status de todas as fábricas na solução.</span><span class="sxs-lookup"><span data-stu-id="52ec6-180">If your subscription has access to the Bing Maps API, the *Factories* map shows you the geographical location and status of all the factories in the solution.</span></span> <span data-ttu-id="52ec6-181">Para analisar os detalhes de local, clique nos locais exibidos no mapa.</span><span class="sxs-lookup"><span data-stu-id="52ec6-181">To drill into the location details, click the locations displayed on the map.</span></span>

![Mapa de solução pré-configurada de fábrica conectada][cf-img-map]

## <a name="view-alerts"></a><span data-ttu-id="52ec6-183">Exibir alertas</span><span class="sxs-lookup"><span data-stu-id="52ec6-183">View alerts</span></span>

<span data-ttu-id="52ec6-184">O painel **Alerta** mostra os alertas gerados devido a um valor relatado ou a um valor calculado de OEE/KPI que excedeu seu limite configurado.</span><span class="sxs-lookup"><span data-stu-id="52ec6-184">The **Alert** panel shows you alerts generated due to a reported value or a calculated OEE/KPI value exceeding its configured threshold.</span></span> <span data-ttu-id="52ec6-185">Este painel exibe alertas em cada nível da hierarquia do modo de exibição de nível de estação para o modo de exibição global.</span><span class="sxs-lookup"><span data-stu-id="52ec6-185">This panel displays alerts at each level of the hierarchy, from the station level view to the global view.</span></span> <span data-ttu-id="52ec6-186">Os alertas contêm uma descrição do alerta, data, hora, local e número de ocorrências.</span><span class="sxs-lookup"><span data-stu-id="52ec6-186">The alerts contain a description of the alert, date, time, location, and number of occurrences.</span></span> <span data-ttu-id="52ec6-187">Você pode se aprofundar nos dados que causaram o alerta usando os dados de informações da série temporal.</span><span class="sxs-lookup"><span data-stu-id="52ec6-187">You can gain insights in to the data that caused the alert using the Time Series Insights data.</span></span> <span data-ttu-id="52ec6-188">Os dados de Informações de Série Temporal são visualizados em alertas, quando aplicável.</span><span class="sxs-lookup"><span data-stu-id="52ec6-188">The Time Series Insights data is visualized in the alerts where applicable.</span></span> <span data-ttu-id="52ec6-189">Se for Administrador, você poderá executar ações de padrão em relação aos alertas, como:</span><span class="sxs-lookup"><span data-stu-id="52ec6-189">If you are an Administrator, you can take default actions on the alerts such as:</span></span>

* <span data-ttu-id="52ec6-190">Feche o alerta.</span><span class="sxs-lookup"><span data-stu-id="52ec6-190">Close the alert.</span></span>
* <span data-ttu-id="52ec6-191">Reconhecer o alerta.</span><span class="sxs-lookup"><span data-stu-id="52ec6-191">Acknowledge the alert.</span></span>

<span data-ttu-id="52ec6-192">Opcionalmente, você pode executar ações mais complexas.</span><span class="sxs-lookup"><span data-stu-id="52ec6-192">Optionally, you can take more complex actions.</span></span> <span data-ttu-id="52ec6-193">Por exemplo, para o nó Pressure OPC UA do Assembly, você pode:</span><span class="sxs-lookup"><span data-stu-id="52ec6-193">For example, for the Pressure OPC UA Node of the Assembly you could:</span></span>

* <span data-ttu-id="52ec6-194">Exiba informações de suporte em uma página da Web em uma nova janela do navegador.</span><span class="sxs-lookup"><span data-stu-id="52ec6-194">Show supporting information in a web page in a new browser window.</span></span>
* <span data-ttu-id="52ec6-195">Mitigar a causa do alerta chamando um método de OPC UA no dispositivo.</span><span class="sxs-lookup"><span data-stu-id="52ec6-195">Mitigate the cause of the alert by calling an OPC UA method on the device.</span></span>
* <span data-ttu-id="52ec6-196">Suprima a disponibilidade das ações padrão.</span><span class="sxs-lookup"><span data-stu-id="52ec6-196">Suppress the availability of the default actions.</span></span>

    ![Alertas de solução pré-configurada de fábrica conectada][cf-img-alerts]

> [!NOTE]
> <span data-ttu-id="52ec6-198">Esses alertas são gerados por regras que são especificadas em um arquivo de configuração da solução pré-configurada.</span><span class="sxs-lookup"><span data-stu-id="52ec6-198">These alerts are generated by rules that are specified in a configuration file in the preconfigured solution.</span></span> <span data-ttu-id="52ec6-199">Essas regras podem gerar alertas quando os valores de nó de UA OPC ou valores de OEE ou KPI excedem o limite configurado.</span><span class="sxs-lookup"><span data-stu-id="52ec6-199">These rules can generate alerts when the OEE or KPI figures or OPC UA Node values are exceeding their configured threshold.</span></span>

1. <span data-ttu-id="52ec6-200">O **Painel de alertas** mostra os alertas gerados nesta solução.</span><span class="sxs-lookup"><span data-stu-id="52ec6-200">The **Alerts panel** shows the alerts generated in this solution.</span></span>

2. <span data-ttu-id="52ec6-201">Para exibir os detalhes de um alerta, clique no alerta no painel de alertas.</span><span class="sxs-lookup"><span data-stu-id="52ec6-201">To view the details of an alert, click the alert in the alerts panel.</span></span>

3. <span data-ttu-id="52ec6-202">Para analisar melhor os dados de alerta, clique no gráfico no painel de alerta para abrir o ambiente de soluções de informações da série temporal.</span><span class="sxs-lookup"><span data-stu-id="52ec6-202">To further analyze the alert data, click the graph in the alert panel to open the Time Series Insights explorer environment.</span></span>

4. <span data-ttu-id="52ec6-203">Para resolver o alerta, várias ações estão disponíveis no painel de alerta.</span><span class="sxs-lookup"><span data-stu-id="52ec6-203">To address the alert, several actions are available in the alert panel.</span></span> <span data-ttu-id="52ec6-204">Escolha a opção apropriada para você e clique no botão de comando de execução de ação.</span><span class="sxs-lookup"><span data-stu-id="52ec6-204">Choose the appropriate option for you and click the execute action command button.</span></span>

## <a name="view-overall-equipment-efficiency"></a><span data-ttu-id="52ec6-205">Exibir a eficiência geral do equipamento</span><span class="sxs-lookup"><span data-stu-id="52ec6-205">View overall equipment efficiency</span></span>

<span data-ttu-id="52ec6-206">O OEE classifica a eficiência do processo de fabricação, usando uma chave parâmetros operacionais relacionados à produção.</span><span class="sxs-lookup"><span data-stu-id="52ec6-206">OEE rates the efficiency of the manufacturing process using a key production-related operational parameters.</span></span> <span data-ttu-id="52ec6-207">OEE é um padrão de medida do setor calculado multiplicando-se a taxa de disponibilidade, a taxa de desempenho e a taxa de qualidade: OEE = disponibilidade x qualidade x desempenho.</span><span class="sxs-lookup"><span data-stu-id="52ec6-207">OEE is an industry standard measure calculated by multiplying the availability rate, performance rate, and quality rate: OEE = availability x performance x quality.</span></span>

![OEE de solução pré-configurada de fábrica conectada][cf-img-oee]

1. <span data-ttu-id="52ec6-209">Para exibir o OEE para qualquer nível na hierarquia, navegue até o modo de exibição específico de que você precisa.</span><span class="sxs-lookup"><span data-stu-id="52ec6-209">To view OEE for any level in the hierarchy, navigate to the specific view you require.</span></span> <span data-ttu-id="52ec6-210">O OEE para essa exibição é mostrado no painel junto com cada um dos elementos que compõem a porcentagem de OEE.</span><span class="sxs-lookup"><span data-stu-id="52ec6-210">The OEE for that view displays in the panel along with each of the elements that make up the OEE percentage.</span></span>

2. <span data-ttu-id="52ec6-211">Para analisar melhor o OEE para qualquer nível dos dados da hierarquia, clique na porcentagem de OEE, de disponibilidade, de desempenho ou de qualidade.</span><span class="sxs-lookup"><span data-stu-id="52ec6-211">To further analyze the OEE for any level in the hierarchy data, click either the OEE, availability, performance, or quality percentage.</span></span> <span data-ttu-id="52ec6-212">É exibido um painel de contexto com Informações da Série de Tempo com visualizações que mostra dados da última hora, das últimas 24 horas e dos últimos sete dias.</span><span class="sxs-lookup"><span data-stu-id="52ec6-212">A context panel appears with Time Series Insights powered visualizations that shows data from the last hour, last 24 hours, and last 7 days.</span></span>

    ![Visualização de TSI de solução pré-configurada de fábrica conectada][cf-img-tsi-visualization]

3. <span data-ttu-id="52ec6-214">Para analisar melhor os dados de alerta, clique no gráfico no painel de alerta.</span><span class="sxs-lookup"><span data-stu-id="52ec6-214">To further analyze the alert data, click the graph in the alert panel.</span></span> <span data-ttu-id="52ec6-215">Essa ação abre o ambiente de explorador Insights de Informações da Série Temporal.</span><span class="sxs-lookup"><span data-stu-id="52ec6-215">This action opens the Time Series Insights explorer environment.</span></span>

    ![Explorador de TSI de solução pré-configurada de fábrica conectada][cf-img-tsi-explorer]

## <a name="view-key-performance-indicators"></a><span data-ttu-id="52ec6-217">Exibir Indicadores Chave de Desempenho</span><span class="sxs-lookup"><span data-stu-id="52ec6-217">View Key Performance Indicators</span></span>

<span data-ttu-id="52ec6-218">A solução fornece dois indicadores-chave de desempenho, *unidades por hora* e *energia usada em kWh*.</span><span class="sxs-lookup"><span data-stu-id="52ec6-218">The solution provides two key performance indicators, *units per hour* and *energy used in kWh*.</span></span>

![KPI de solução pré-configurada de fábrica conectada][cf-img-kpi]

1. <span data-ttu-id="52ec6-220">Para exibir as unidades por hora ou energia usadas para qualquer nível na hierarquia, navegue até o modo de exibição específico de que você precisa.</span><span class="sxs-lookup"><span data-stu-id="52ec6-220">To view units per hour or energy used for any level in the hierarchy, navigate to the specific view you require.</span></span> <span data-ttu-id="52ec6-221">As unidades por hora e energia usadas são exibidas no painel.</span><span class="sxs-lookup"><span data-stu-id="52ec6-221">The units per hour and energy used display in the panel.</span></span>

2. <span data-ttu-id="52ec6-222">Para analisar melhor as unidades por hora ou a energia usada em qualquer nível na hierarquia, clique no medidor do painel **Indicadores chave de desempenho**.</span><span class="sxs-lookup"><span data-stu-id="52ec6-222">To analyze units per hour or energy used for any level in the hierarchy further, click the gauge in the **Key Performance Indicators** panel.</span></span> <span data-ttu-id="52ec6-223">É exibido um painel de contexto com Informações da Série de Tempo com visualizações, habilitando-o a exibir dados da última hora, das últimas 24 horas e dos últimos sete dias.</span><span class="sxs-lookup"><span data-stu-id="52ec6-223">A context panel appears with Time Series Insights powered visualizations enabling you to view data from the last hour, the last 24 hours, and last 7 days.</span></span>

## <a name="scenario-review"></a><span data-ttu-id="52ec6-224">Análise do cenário</span><span class="sxs-lookup"><span data-stu-id="52ec6-224">Scenario review</span></span>

<span data-ttu-id="52ec6-225">Nesse cenário, você monitorou os valores de OEE e KPIs de fábricas no painel.</span><span class="sxs-lookup"><span data-stu-id="52ec6-225">In this scenario, you monitored your factories OEE and KPIs values, in the dashboard.</span></span> <span data-ttu-id="52ec6-226">Você usou então Informações da Série Temporal para fornecer mais informações e analisar ainda mais os dados de telemetria de OEE e KPIs para ajudar na detecção de anomalias.</span><span class="sxs-lookup"><span data-stu-id="52ec6-226">You then used Time Series Insights to provide more information to help drill further into the telemetry data for OEE and KPIs to help with detecting anomalies.</span></span> <span data-ttu-id="52ec6-227">Você também usou o painel de alerta para exibir os problemas com as fábricas e usou as ações disponíveis para resolver o alerta.</span><span class="sxs-lookup"><span data-stu-id="52ec6-227">You also used the alert panel to view issues with your factories and you used the actions available to you to resolve the alert.</span></span>

## <a name="other-features"></a><span data-ttu-id="52ec6-228">Outros recursos</span><span class="sxs-lookup"><span data-stu-id="52ec6-228">Other features</span></span>

<span data-ttu-id="52ec6-229">As seções a seguir descrevem alguns recursos adicionais de solução de fábrica conectada que não são descritos no cenário anterior.</span><span class="sxs-lookup"><span data-stu-id="52ec6-229">The following sections describe some additional features of the connected factory solution that are not described in the previous scenario.</span></span>

## <a name="apply-filters"></a><span data-ttu-id="52ec6-230">Aplicar filtros</span><span class="sxs-lookup"><span data-stu-id="52ec6-230">Apply filters</span></span>

1. <span data-ttu-id="52ec6-231">Clique na **divisa** para exibir uma lista de filtros disponíveis no painel nos locais de fábrica ou no painel de alertas.</span><span class="sxs-lookup"><span data-stu-id="52ec6-231">Click the **chevron** to display a list of available filters in either the factory locations panel or the alerts panel.</span></span>

2. <span data-ttu-id="52ec6-232">O painel de filtros é exibido para você.</span><span class="sxs-lookup"><span data-stu-id="52ec6-232">The filters panel is displayed for you.</span></span> 

    ![Filtros de solução pré-configurados de fábrica conectada][cf-img-alert-filter]

3. <span data-ttu-id="52ec6-234">Escolha o filtro necessário.</span><span class="sxs-lookup"><span data-stu-id="52ec6-234">Choose the filter that you require.</span></span> <span data-ttu-id="52ec6-235">Também é possível digitar texto livre nos campos de filtro.</span><span class="sxs-lookup"><span data-stu-id="52ec6-235">It is also possible to type free text into the filter fields.</span></span>

4. <span data-ttu-id="52ec6-236">O filtro é aplicado para você.</span><span class="sxs-lookup"><span data-stu-id="52ec6-236">The filter is then applied for you.</span></span> <span data-ttu-id="52ec6-237">O estado do filtro também é mostrado no painel por meio de um funil que é exibido nas tabelas de fábricas e alertas.</span><span class="sxs-lookup"><span data-stu-id="52ec6-237">The filter state is also shown in the dashboard via a funnel that displays in the factories and alerts tables.</span></span>

    ![Filtros de solução pré-configurados de fábrica conectada][cf-img-alert-filter-funnel]

    > [!NOTE]
    > <span data-ttu-id="52ec6-239">Um filtro ativo não afeta os valores OEE e KPI exibidos. Ele apenas filtra o conteúdo da lista.</span><span class="sxs-lookup"><span data-stu-id="52ec6-239">An active filter does not affect the displayed OEE and KPI values, it only filters the list contents.</span></span>

5. <span data-ttu-id="52ec6-240">Para limpar um filtro, clique no funil e clique no filtro no painel de contexto de filtro.</span><span class="sxs-lookup"><span data-stu-id="52ec6-240">To clear a filter, click the funnel and click filter in the filter context panel.</span></span> <span data-ttu-id="52ec6-241">O texto **Tudo** é exibido nas tabelas de alertas e fábricas.</span><span class="sxs-lookup"><span data-stu-id="52ec6-241">The text **All** is displayed in the factories and alerts tables.</span></span>

## <a name="browse-an-opc-ua-server"></a><span data-ttu-id="52ec6-242">Procurar um servidor de OPC UA</span><span class="sxs-lookup"><span data-stu-id="52ec6-242">Browse an OPC UA server</span></span>

<span data-ttu-id="52ec6-243">Ao implantar a solução pré-configurada, você provisiona automaticamente servidores OPC UA simulados que pode procurar por meio do navegador de solução.</span><span class="sxs-lookup"><span data-stu-id="52ec6-243">When you deploy the preconfigured solution, you automatically provision simulated OPC UA servers that you can browse via the solution browser.</span></span> <span data-ttu-id="52ec6-244">Esses servidores são *servidores OPC UA simulados*.</span><span class="sxs-lookup"><span data-stu-id="52ec6-244">These servers are *simulated OPC UA servers*.</span></span> <span data-ttu-id="52ec6-245">Com os servidores simulados, você pode experimentar mais facilmente a solução pré-configurada sem a necessidade de implantar servidores físicos reais.</span><span class="sxs-lookup"><span data-stu-id="52ec6-245">Simulated servers make it easy for you to experiment with the preconfigured solution without the need to deploy real, physical servers.</span></span> <span data-ttu-id="52ec6-246">Se deseja conectar um servidor de OPC UA real à solução, confira o tutorial [Conectar seu dispositivo OPC UA à solução pré-configurada de fábrica conectada][lnk-connect-cf].</span><span class="sxs-lookup"><span data-stu-id="52ec6-246">If you do want to connect a real OPC UA server to the solution, see the [Connect your OPC UA device to the connected factory preconfigured solution][lnk-connect-cf] tutorial.</span></span>

1. <span data-ttu-id="52ec6-247">Clique no **ícone de fábrica** na barra de navegação do painel.</span><span class="sxs-lookup"><span data-stu-id="52ec6-247">Click the **factory icon** in the dashboard navigation bar.</span></span>

    ![Navegador de servidor de chamada de solução pré-configurada de fábrica conectada][cf-img-server-browser]

2. <span data-ttu-id="52ec6-249">Escolha um dos servidores na lista pré-configurada.</span><span class="sxs-lookup"><span data-stu-id="52ec6-249">Choose one of the servers from the preconfigured list.</span></span> <span data-ttu-id="52ec6-250">Esta lista mostra os servidores que são implantados na solução pré-configurada.</span><span class="sxs-lookup"><span data-stu-id="52ec6-250">This list shows the servers that are deployed for you in the preconfigured solution.</span></span>

    ![Seleção de chamada de solução pré-configurada de fábrica conectada][cf-img-server-choice]

3. <span data-ttu-id="52ec6-252">Clique em **Conectar**. Uma caixa de diálogo de segurança será exibida.</span><span class="sxs-lookup"><span data-stu-id="52ec6-252">Click **Connect**, a security dialog displays.</span></span> <span data-ttu-id="52ec6-253">Para a simulação, é seguro clicar em **Continuar**</span><span class="sxs-lookup"><span data-stu-id="52ec6-253">For the simulation, it is safe to click **Proceed**</span></span>

4. <span data-ttu-id="52ec6-254">Clique em um dos nós na árvore de servidor para expandi-lo.</span><span class="sxs-lookup"><span data-stu-id="52ec6-254">To expand any of the nodes in the server tree, click it.</span></span> <span data-ttu-id="52ec6-255">Nós que estão publicando telemetria têm uma marcação ao lado deles.</span><span class="sxs-lookup"><span data-stu-id="52ec6-255">Nodes that are publishing telemetry have a tick mark beside them.</span></span>

    ![Árvore de chamada de solução pré-configurada de fábrica conectada][cf-img-server-tree]

5. <span data-ttu-id="52ec6-257">Clique com o botão direito do mouse em um item para ler, gravar, publicar ou chamar esse nó.</span><span class="sxs-lookup"><span data-stu-id="52ec6-257">Right-click an item to read, write, publish, or call that node.</span></span> <span data-ttu-id="52ec6-258">As ações disponíveis para você dependem de suas permissões e dos atributos do nó.</span><span class="sxs-lookup"><span data-stu-id="52ec6-258">The actions available to you depend on your permissions and the attributes of the node.</span></span> <span data-ttu-id="52ec6-259">A opção de leitura de exibe um painel de contexto mostrando o valor de nó específico.</span><span class="sxs-lookup"><span data-stu-id="52ec6-259">The read option to displays a context panel showing the value of the specific node.</span></span> <span data-ttu-id="52ec6-260">A opção de gravação exibe um painel de contexto em que você pode inserir um novo valor.</span><span class="sxs-lookup"><span data-stu-id="52ec6-260">The write option displays a context panel where you can enter a new value.</span></span> <span data-ttu-id="52ec6-261">A opção de chamada exibe um nó em que você pode inserir os parâmetros para a chamada.</span><span class="sxs-lookup"><span data-stu-id="52ec6-261">The call option displays a node where you can enter the parameters for the call.</span></span>

## <a name="publish-a-node"></a><span data-ttu-id="52ec6-262">Publicar um nó</span><span class="sxs-lookup"><span data-stu-id="52ec6-262">Publish a node</span></span>

<span data-ttu-id="52ec6-263">Ao procurar um *servidor OPC UA simulado*, você também pode optar por publicar novos nós.</span><span class="sxs-lookup"><span data-stu-id="52ec6-263">When you browse a *simulated OPC UA server*, you can also choose to publish new nodes.</span></span> <span data-ttu-id="52ec6-264">Você pode analisar a telemetria desses nós na solução.</span><span class="sxs-lookup"><span data-stu-id="52ec6-264">You can analyze the telemetry from these nodes in the solution.</span></span> <span data-ttu-id="52ec6-265">Esses *servidores OPC UA simulados* facilitam o teste da solução pré-configurada sem implantar dispositivos físicos reais.</span><span class="sxs-lookup"><span data-stu-id="52ec6-265">These *simulated OPC UA servers* make it easy to experiment with the preconfigured solution without deploying real, physical devices.</span></span>

1. <span data-ttu-id="52ec6-266">Navegue até um nó na árvore do navegador de servidor OPC UA que você deseja publicar.</span><span class="sxs-lookup"><span data-stu-id="52ec6-266">Browse to a node in the OPC UA server browser tree that you wish to publish.</span></span>

2. <span data-ttu-id="52ec6-267">Clique com o botão direito do mouse no nó.</span><span class="sxs-lookup"><span data-stu-id="52ec6-267">Right-click the node.</span></span>

3. <span data-ttu-id="52ec6-268">Escolha **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="52ec6-268">Choose **Publish**.</span></span>

    ![A fábrica conectada publica o nó][cf-img-publish-node]

4. <span data-ttu-id="52ec6-270">É exibido um painel de contexto que informa que a publicação foi bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="52ec6-270">A context panel appears which tells you that the publish has succeeded.</span></span> <span data-ttu-id="52ec6-271">O nó aparece na exibição do nível de estação com uma marca de seleção ao lado dele.</span><span class="sxs-lookup"><span data-stu-id="52ec6-271">The node appears in the station level view with a check mark beside it.</span></span>

    ![Publicação com êxito de chamada de solução pré-configurada de fábrica conectada][cf-img-publish-success]

## <a name="command-and-control"></a><span data-ttu-id="52ec6-273">Comando e controle</span><span class="sxs-lookup"><span data-stu-id="52ec6-273">Command and control</span></span>

<span data-ttu-id="52ec6-274">A fábrica conectada permite que você comande e controle os dispositivos do setor diretamente da nuvem.</span><span class="sxs-lookup"><span data-stu-id="52ec6-274">The connected factory allows you command and control your industry devices directly from the cloud.</span></span> <span data-ttu-id="52ec6-275">Você pode usar esse recurso para responder aos alertas gerados pelo dispositivo.</span><span class="sxs-lookup"><span data-stu-id="52ec6-275">You can use this feature to respond to alerts generated by the device.</span></span> <span data-ttu-id="52ec6-276">Por exemplo, você pode enviar um comando para o dispositivo da nuvem.</span><span class="sxs-lookup"><span data-stu-id="52ec6-276">For example, you could send a command to the device from the cloud.</span></span> <span data-ttu-id="52ec6-277">Você pode encontrar os comandos disponíveis no nó **StationCommands** na árvore do navegador de servidores OPC UA.</span><span class="sxs-lookup"><span data-stu-id="52ec6-277">You can find the available commands in the **StationCommands** node in the OPC UA servers browser tree.</span></span> <span data-ttu-id="52ec6-278">Nesse cenário, você abre uma válvula de liberação de pressão na estação de montagem de uma linha de produção em Munique.</span><span class="sxs-lookup"><span data-stu-id="52ec6-278">In this scenario, you open a pressure release valve on the assembly station of a production line in Munich.</span></span> <span data-ttu-id="52ec6-279">Para usar a funcionalidade de comando e controle, você deve estar na função de **Administrador** para a implantação da solução pré-configurada.</span><span class="sxs-lookup"><span data-stu-id="52ec6-279">To use the command and control functionality, you must be in the **Administrator** role for the preconfigured solution deployment.</span></span>

1. <span data-ttu-id="52ec6-280">Navegue até o **StationCommands** nó na árvore do navegador do servidor UA OPC.</span><span class="sxs-lookup"><span data-stu-id="52ec6-280">Browse to the **StationCommands** node in the OPC UA server browser tree.</span></span>

2. <span data-ttu-id="52ec6-281">Escolha o comando que você deseja usar.</span><span class="sxs-lookup"><span data-stu-id="52ec6-281">Choose the command that you wish use.</span></span>

3. <span data-ttu-id="52ec6-282">Clique com o botão direito do mouse no nó.</span><span class="sxs-lookup"><span data-stu-id="52ec6-282">Right-click the node.</span></span>

4. <span data-ttu-id="52ec6-283">Escolha **Chamar**.</span><span class="sxs-lookup"><span data-stu-id="52ec6-283">Choose **Call**.</span></span>

    ![Comando de chamada de solução pré-configurada de fábrica conectada][cf-img-call-command]

5. <span data-ttu-id="52ec6-285">É exibido um painel de contexto que informa o método que você está prestes a chamar e quaisquer detalhes de parâmetros aplicáveis.</span><span class="sxs-lookup"><span data-stu-id="52ec6-285">A context panel appears informing you which method you are about to call and any parameter details is applicable.</span></span>

6. <span data-ttu-id="52ec6-286">Escolha **Chamar**.</span><span class="sxs-lookup"><span data-stu-id="52ec6-286">Choose **Call**.</span></span>

    ![Contexto de chamada de solução pré-configurada de fábrica conectada][cf-img-call-context]

7. <span data-ttu-id="52ec6-288">O painel de contexto é atualizado para informar que a chamada de método foi bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="52ec6-288">The context panel is updated to inform you that the method call succeeded.</span></span> <span data-ttu-id="52ec6-289">Você pode verificar se a chamada foi bem-sucedida lendo o valor do nó de pressão atualizado como resultado da chamada.</span><span class="sxs-lookup"><span data-stu-id="52ec6-289">You can verify the call succeeded by reading the value of the pressure node that updated as a result of the call.</span></span>

    ![Sucesso de chamada de solução pré-configurada de fábrica conectada][cf-img-call-success]


## <a name="behind-the-scenes"></a><span data-ttu-id="52ec6-291">Nos bastidores</span><span class="sxs-lookup"><span data-stu-id="52ec6-291">Behind the scenes</span></span>

<span data-ttu-id="52ec6-292">Ao implantar uma solução pré-configurada, o processo de implantação criará vários recursos na assinatura do Azure que você selecionou.</span><span class="sxs-lookup"><span data-stu-id="52ec6-292">When you deploy a preconfigured solution, the deployment process creates multiple resources in the Azure subscription you selected.</span></span> <span data-ttu-id="52ec6-293">Você pode exibir esses recursos no [portal][lnk-portal] do Azure.</span><span class="sxs-lookup"><span data-stu-id="52ec6-293">You can view these resources in the Azure [portal][lnk-portal].</span></span> <span data-ttu-id="52ec6-294">O processo de implantação cria um **grupo de recursos** com um nome baseado no nome escolhido para sua solução pré-configurada:</span><span class="sxs-lookup"><span data-stu-id="52ec6-294">The deployment process creates a **resource group** with a name based on the name you choose for your preconfigured solution:</span></span>

![Solução pré-configurada no portal do Azure][img-cf-portal]

<span data-ttu-id="52ec6-296">Você pode exibir as configurações de cada recurso selecionando-o na lista de recursos no grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="52ec6-296">You can view the settings of each resource by selecting it in the list of resources in the resource group.</span></span>

<span data-ttu-id="52ec6-297">Você também pode exibir o código-fonte para a solução pré-configurada.</span><span class="sxs-lookup"><span data-stu-id="52ec6-297">You can also view the source code for the preconfigured solution.</span></span> <span data-ttu-id="52ec6-298">O código-fonte da solução pré-configurada de fábrica conectada está no repositório do GitHub [azure-iot-connected-factory][lnk-cfgithub]:</span><span class="sxs-lookup"><span data-stu-id="52ec6-298">The connected factory preconfigured solution source code is in the [azure-iot-connected-factory][lnk-cfgithub] GitHub repository:</span></span>

<span data-ttu-id="52ec6-299">Quando você terminar, poderá excluir a solução pré-configurada de sua assinatura do Azure no site [azureiotsuite.com][lnk-azureiotsuite].</span><span class="sxs-lookup"><span data-stu-id="52ec6-299">When you are done, you can delete the preconfigured solution from your Azure subscription on the [azureiotsuite.com][lnk-azureiotsuite] site.</span></span> <span data-ttu-id="52ec6-300">Esse site permite que você exclua facilmente todos os recursos que foram provisionados quando criou a solução pré-configurada.</span><span class="sxs-lookup"><span data-stu-id="52ec6-300">This site enables you to easily delete all the resources that were provisioned when you created the preconfigured solution.</span></span>

> [!NOTE]
> <span data-ttu-id="52ec6-301">Para garantir que você exclua tudo relacionado à solução pré-configurada, exclua-a no site [azureiotsuite.com][lnk-azureiotsuite].</span><span class="sxs-lookup"><span data-stu-id="52ec6-301">To ensure that you delete everything related to the preconfigured solution, delete it on the [azureiotsuite.com][lnk-azureiotsuite] site.</span></span> <span data-ttu-id="52ec6-302">Não exclua o grupo de recursos no portal.</span><span class="sxs-lookup"><span data-stu-id="52ec6-302">Do not delete the resource group in the portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="52ec6-303">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="52ec6-303">Next Steps</span></span>

<span data-ttu-id="52ec6-304">Agora que você implantou uma solução de trabalho pré-configurada, poderá continuar a introdução ao Suite IoT lendo os seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="52ec6-304">Now that you’ve deployed a working preconfigured solution, you can continue getting started with IoT Suite by reading the following articles:</span></span>

* <span data-ttu-id="52ec6-305">[Passo a passo de solução pré-configurada de fábrica conectada][lnk-rm-walkthrough]</span><span class="sxs-lookup"><span data-stu-id="52ec6-305">[Connected factory preconfigured solution walkthrough][lnk-rm-walkthrough]</span></span>
* <span data-ttu-id="52ec6-306">[Conecte o dispositivo à solução pré-configurada de fábrica conectada][lnk-connect-cf]</span><span class="sxs-lookup"><span data-stu-id="52ec6-306">[Connect your device to the Connected factory preconfigured solution][lnk-connect-cf]</span></span>
* <span data-ttu-id="52ec6-307">[Permissões no site azureiotsuite.com][lnk-permissions]</span><span class="sxs-lookup"><span data-stu-id="52ec6-307">[Permissions on the azureiotsuite.com site][lnk-permissions]</span></span>

[img-cf-home]:media/iot-suite-connected-factory-overview/cf-dashboard.png
[img-launch-solution]: media/iot-suite-connected-factory-overview/launch-cf.png
[cf-img-menu]: media/iot-suite-connected-factory-overview/cf-dashboard-menu.png
[cf-img-factories]:media/iot-suite-connected-factory-overview/cf-dashboard-factory.png
[cf-img-map]:media/iot-suite-connected-factory-overview/cf-dashboard-map.png
[cf-img-alerts]:media/iot-suite-connected-factory-overview/cf-dashboard-alerts.png
[cf-img-oee]:media/iot-suite-connected-factory-overview/cf-dashboard-oee.png
[cf-img-kpi]:media/iot-suite-connected-factory-overview/cf-dashboard-kpi.png
[cf-img-tsi-visualization]:media/iot-suite-connected-factory-overview/cf-dashboard-tsi.png
[cf-img-tsi-explorer]:media/iot-suite-connected-factory-overview/tsi-explorer.png
[cf-img-server-browser]: media/iot-suite-connected-factory-overview/cf-dashboard-browser.png
[cf-img-server-choice]: media/iot-suite-connected-factory-overview/cf-select-server.png
[cf-img-server-tree]:media/iot-suite-connected-factory-overview/cf-server-tree.png
[cf-img-publish-node]:media/iot-suite-connected-factory-overview/cf-publish-node1.png
[cf-img-publish-success]:media/iot-suite-connected-factory-overview/cf-publish-success.png
[cf-img-call-command]:media/iot-suite-connected-factory-overview/cf-command-and-control-call.png
[cf-img-call-context]:media/iot-suite-connected-factory-overview/cf-command-and-control-call-button.png
[cf-img-call-success]:media/iot-suite-connected-factory-overview/cf-command-and-control-succeed.png
[img-cf-portal]:media/iot-suite-connected-factory-overview/cf-resource-group.png
[cf-img-alert-filter]:media/iot-suite-connected-factory-overview/cf-filter.png
[cf-img-alert-filter-funnel]:media/iot-suite-connected-factory-overview/cf-filter-funnel.png

[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-preconfigured-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-azureiotsuite]: https://www.azureiotsuite.com
[lnk-portal]: http://portal.azure.com/
[lnk-cfgithub]: https://github.com/Azure/azure-iot-connected-factory
[lnk-rm-walkthrough]: iot-suite-connected-factory-sample-walkthrough.md
[lnk-connect-cf]: iot-suite-connected-factory-gateway-deployment.md
[lnk-permissions]: iot-suite-permissions.md
[lnk-faq]: iot-suite-faq.md