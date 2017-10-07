---
title: "Visão geral da fábrica de conectado aaaAzure IoT Suite | Microsoft Docs"
description: "Uma descrição do hello Azure IoT Suite conectado solução pré-configurada de fábrica."
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
ms.openlocfilehash: 929b5ed41ef7d82c9b4480d02aa3f0db38931919
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-connected-factory-preconfigured-solution"></a><span data-ttu-id="bd2c5-103">Introdução à solução de fábrica pré-configurado Olá conectado</span><span class="sxs-lookup"><span data-stu-id="bd2c5-103">Get started with hello connected factory preconfigured solution</span></span>

<span data-ttu-id="bd2c5-104">Azure IoT Suite [soluções pré-configuradas] [ lnk-preconfigured-solutions] combinar várias IoT do Azure services toodeliver ponta a ponta soluções que implementam cenários comuns de negócios de IoT.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-104">Azure IoT Suite [preconfigured solutions][lnk-preconfigured-solutions] combine multiple Azure IoT services toodeliver end-to-end solutions that implement common IoT business scenarios.</span></span> <span data-ttu-id="bd2c5-105">Olá *fábrica conectada* solução pré-configurada conecta tooand monitora seus dispositivos industriais.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-105">hello *connected factory* preconfigured solution connects tooand monitors your industrial devices.</span></span> <span data-ttu-id="bd2c5-106">Você pode usar o fluxo de saudação do hello solução tooanalyze de dados de seus dispositivos e produtividade operacional toodrive e lucratividade.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-106">You can use hello solution tooanalyze hello stream of data from your devices and toodrive operational productivity and profitability.</span></span>

<span data-ttu-id="bd2c5-107">Este tutorial mostra como tooprovision Olá conectadas fábrica pré-configurado de solução.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-107">This tutorial shows you how tooprovision hello connected factory preconfigured solution.</span></span> <span data-ttu-id="bd2c5-108">Ele também orienta você por meio de recursos básicos de saudação da solução Olá pré-configurado.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-108">It also walks you through hello basic features of hello preconfigured solution.</span></span> <span data-ttu-id="bd2c5-109">Você pode acessar muitos desses recursos de solução de saudação *painel* que implanta como parte da solução Olá pré-configurados:</span><span class="sxs-lookup"><span data-stu-id="bd2c5-109">You can access many of these features from hello solution *dashboard* that deploys as part of hello preconfigured solution:</span></span>

![Painel de solução pré-configurada de fábrica conectada][img-cf-home]

<span data-ttu-id="bd2c5-111">toocomplete neste tutorial, você precisa de uma assinatura ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-111">toocomplete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="bd2c5-112">Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-112">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="bd2c5-113">Para obter detalhes, consulte [Avaliação gratuita do Azure][lnk_free_trial].</span><span class="sxs-lookup"><span data-stu-id="bd2c5-113">For details, see [Azure Free Trial][lnk_free_trial].</span></span>
> 
> 

## <a name="provision-hello-solution"></a><span data-ttu-id="bd2c5-114">Provisionar Olá solução</span><span class="sxs-lookup"><span data-stu-id="bd2c5-114">Provision hello solution</span></span>

1. <span data-ttu-id="bd2c5-115">Faça logon no tooazureiotsuite.com usando suas credenciais de conta do Azure e, em seguida, clique em "**+**" toocreate uma solução.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-115">Log on tooazureiotsuite.com using your Azure account credentials, and click "**+**" toocreate a solution.</span></span>
2. <span data-ttu-id="bd2c5-116">Clique em **selecione** em Olá **fábrica conectada** lado a lado.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-116">Click **Select** on hello **Connected factory** tile.</span></span>
3. <span data-ttu-id="bd2c5-117">Digite um **Nome de solução** para a solução pré-configurada de fábrica conectada.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-117">Enter a **Solution name** for your connected factory preconfigured solution.</span></span>
4. <span data-ttu-id="bd2c5-118">Selecione Olá **assinatura** e **região** deseja toouse tooprovision Olá solução.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-118">Select hello **Subscription** and **Region** you want toouse tooprovision hello solution.</span></span>
5. <span data-ttu-id="bd2c5-119">Clique em **criar solução** Olá toobegin processo de provisionamento.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-119">Click **Create Solution** toobegin hello provisioning process.</span></span> <span data-ttu-id="bd2c5-120">Normalmente, esse processo leva vários toorun de minutos.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-120">This process typically takes several minutes toorun.</span></span>

### <a name="while-you-wait-for-hello-provisioning-process-toocomplete"></a><span data-ttu-id="bd2c5-121">Enquanto aguarda Olá toocomplete do processo de provisionamento</span><span class="sxs-lookup"><span data-stu-id="bd2c5-121">While you wait for hello provisioning process toocomplete</span></span>

1. <span data-ttu-id="bd2c5-122">Clique em bloco de saudação para sua solução com **provisionamento** status.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-122">Click hello tile for your solution with **Provisioning** status.</span></span>
2. <span data-ttu-id="bd2c5-123">Saudação de aviso **provisionamento estados** como serviços do Azure são implantados na sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-123">Notice hello **Provisioning states** as Azure services are deployed in your Azure subscription.</span></span>
3. <span data-ttu-id="bd2c5-124">Após a conclusão do provisionamento, Olá alterações de status muito**pronto**.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-124">Once provisioning completes, hello status changes too**Ready**.</span></span>
4. <span data-ttu-id="bd2c5-125">Clique em Olá bloco toosee Olá detalhes de sua solução no painel direito da saudação.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-125">Click hello tile toosee hello details of your solution in hello right-hand pane.</span></span>

> [!NOTE]
> <span data-ttu-id="bd2c5-126">Se você encontrar problemas de implantação de solução Olá pré-configurado, examine [permissões no site do hello azureiotsuite.com] [ lnk-permissions] e hello [conectado perguntas Frequentes de fábrica](iot-suite-faq-cf.md).</span><span class="sxs-lookup"><span data-stu-id="bd2c5-126">If you encounter issues deploying hello preconfigured solution, review [Permissions on hello azureiotsuite.com site][lnk-permissions] and hello [Connected factory FAQ](iot-suite-faq-cf.md).</span></span> <span data-ttu-id="bd2c5-127">Se os problemas de saudação persistirem, criar um tíquete de serviço em Olá [portal][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="bd2c5-127">If hello issues persist, create a service ticket on hello [portal][lnk-portal].</span></span>

<span data-ttu-id="bd2c5-128">Há detalhes esperado toosee que não estejam listados para sua solução?</span><span class="sxs-lookup"><span data-stu-id="bd2c5-128">Are there details you'd expect toosee that aren't listed for your solution?</span></span> <span data-ttu-id="bd2c5-129">Envie sugestões de recursos no [User Voice](https://feedback.azure.com/forums/321918-azure-iot).</span><span class="sxs-lookup"><span data-stu-id="bd2c5-129">Give us feature suggestions on [User Voice](https://feedback.azure.com/forums/321918-azure-iot).</span></span>

## <a name="scenario-overview"></a><span data-ttu-id="bd2c5-130">Visão geral do cenário</span><span class="sxs-lookup"><span data-stu-id="bd2c5-130">Scenario overview</span></span>

<span data-ttu-id="bd2c5-131">Quando você implanta Olá conectado fábrica pré-configurado solução, ele será preenchido com recursos que permitem que você toostep por meio de um cenário industrial comum.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-131">When you deploy hello connected factory preconfigured solution, it is prepopulated with resources that enable you toostep through a common industrial scenario.</span></span> <span data-ttu-id="bd2c5-132">Nesse cenário, diversas fábricas conectado relatórios de solução de toohello toocompute necessária de valores de dados de saudação eficiência geral de equipamentos (OEE) e indicadores chave de desempenho (KPIs).</span><span class="sxs-lookup"><span data-stu-id="bd2c5-132">In this scenario, several factories connected toohello solution report hello data values required toocompute overall equipment efficiency (OEE) and key performance indicators (KPIs).</span></span> <span data-ttu-id="bd2c5-133">Olá seções a seguir mostram como para:</span><span class="sxs-lookup"><span data-stu-id="bd2c5-133">hello following sections show you how to:</span></span>

* <span data-ttu-id="bd2c5-134">Monitorar fábrica, linhas de produção, OEE de estação e valores de KPI</span><span class="sxs-lookup"><span data-stu-id="bd2c5-134">Monitor factory, production lines, station OEE, and KPI values</span></span>
* <span data-ttu-id="bd2c5-135">Analisar dados de telemetria Olá gerados a partir desses dispositivos usando o Azure Insights de série de tempo</span><span class="sxs-lookup"><span data-stu-id="bd2c5-135">Analyze hello telemetry data generated from these devices using Azure Time Series Insights</span></span>
* <span data-ttu-id="bd2c5-136">Agir sobre problemas de toofix de alertas</span><span class="sxs-lookup"><span data-stu-id="bd2c5-136">Act on alerts toofix issues</span></span>

<span data-ttu-id="bd2c5-137">Um recurso principal deste cenário é que você pode executar todas essas ações remotamente no painel de solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-137">A key feature of this scenario is that you can perform all these actions remotely from hello solution dashboard.</span></span> <span data-ttu-id="bd2c5-138">Dispositivos de toohello acesso físico não é necessário.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-138">You do not need physical access toohello devices.</span></span>

## <a name="view-hello-solution-dashboard"></a><span data-ttu-id="bd2c5-139">Painel de solução de saudação de View</span><span class="sxs-lookup"><span data-stu-id="bd2c5-139">View hello solution dashboard</span></span>

<span data-ttu-id="bd2c5-140">Painel de solução de saudação permite toomanage solução de saudação implantada.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-140">hello solution dashboard enables you toomanage hello deployed solution.</span></span> <span data-ttu-id="bd2c5-141">É uma representação hierárquica de uma configuração global de fábrica.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-141">It is a hierarchical representation of a global factory configuration.</span></span> <span data-ttu-id="bd2c5-142">Por exemplo, você pode exibir KPIs e OEE, publicar novos nós para alertas de telemetria e de ação.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-142">For example, you can view OEE and KPIs, publish new nodes for telemetry and action alerts.</span></span>

1. <span data-ttu-id="bd2c5-143">Quando Olá provisionamento for concluído e lado a lado para sua solução pré-configurada Olá indica **pronto**, escolha **iniciar** tooopen seu portal de solução de fábrica conectados em uma nova guia.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-143">When hello provisioning is complete and hello tile for your preconfigured solution indicates **Ready**, choose **Launch** tooopen your connected factory solution portal in a new tab.</span></span>

    ![Iniciar a solução de saudação pré-configurado][img-launch-solution]

1. <span data-ttu-id="bd2c5-145">Por padrão, o portal de solução Olá mostra Olá *painel*.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-145">By default, hello solution portal shows hello *dashboard*.</span></span> <span data-ttu-id="bd2c5-146">toonavigate tooother áreas do portal hello, use o menu de saudação no lado esquerdo de saudação da página de saudação.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-146">toonavigate tooother areas of hello portal, use hello menu on hello left-hand side of hello page.</span></span>

    ![Painel de solução pré-configurada de fábrica conectada][cf-img-menu]

<span data-ttu-id="bd2c5-148">Painel de saudação exibe Olá informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="bd2c5-148">hello dashboard displays hello following information:</span></span>

* <span data-ttu-id="bd2c5-149">Um **lista fábrica** painel que mostra o status de saudação, o local e a configuração atual de produção na solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-149">A **Factory list** panel that shows hello status, location, and current production configuration in hello solution.</span></span> <span data-ttu-id="bd2c5-150">Quando você executa solução hello, há um número de dispositivos simulados.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-150">When you first run hello solution, there are a number of simulated devices.</span></span> <span data-ttu-id="bd2c5-151">simulação de linha de produção de Hello é composta de três OPC UA servidores reais por linha de produção que executem tarefas simuladas e compartilham dados.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-151">hello production line simulation is composed of three real OPC UA servers per production line that perform simulated tasks and share data.</span></span> <span data-ttu-id="bd2c5-152">Para obter mais informações sobre OPC UA, consulte Olá [conectado perguntas Frequentes de fábrica](iot-suite-faq-cf.md).</span><span class="sxs-lookup"><span data-stu-id="bd2c5-152">For more information about OPC UA, see hello [Connected factory FAQ](iot-suite-faq-cf.md).</span></span>
* <span data-ttu-id="bd2c5-153">Um **mapa** exibe Olá local de cada dispositivo conectado toohello solução.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-153">A **map** that displays hello location of each device connected toohello solution.</span></span> <span data-ttu-id="bd2c5-154">solução de saudação pode usar informações de tooplot de API do Bing Maps Olá mapa hello.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-154">hello solution can use hello Bing Maps API tooplot information on hello map.</span></span> <span data-ttu-id="bd2c5-155">Se sua assinatura estiver habilitada para a API do Bing Maps Enterprise, esse recurso será usado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-155">If your subscription is enabled for Bing Maps Enterprise API, then this feature is used automatically.</span></span> <span data-ttu-id="bd2c5-156">Se não, consulte Olá [perguntas frequentes sobre] [ lnk-faq] toolearn como toomake Olá mapa dinâmico.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-156">If not, see hello [FAQ][lnk-faq] toolearn how toomake hello map dynamic.</span></span>
* <span data-ttu-id="bd2c5-157">Um painel **Alertas** que exibe alertas gerados quando um valor KPI/OEE ou de telemetria excede um limite específico.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-157">An **Alerts** panel that displays alerts generated when a telemetry or OEE/KPI value exceeds a specific threshold.</span></span>
* <span data-ttu-id="bd2c5-158">Um **eficiência geral de equipamento** painel que mostra valores OEE Olá Olá fábrica/produção ou empresa inteira Olá linha/estação que você está exibindo.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-158">An **Overall Equipment Efficiency** panel that shows hello OEE values for hello whole enterprise, or hello factory/production line/station you are viewing.</span></span> <span data-ttu-id="bd2c5-159">Esse valor é agregado de saudação estação exibição toohello de nível empresarial.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-159">This value is aggregated from hello station view toohello enterprise level.</span></span> <span data-ttu-id="bd2c5-160">a Figura OEE Hello e seus elementos constituintes podem ser analisados adicional.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-160">hello OEE figure and its constituent elements can be further analyzed.</span></span>
* <span data-ttu-id="bd2c5-161">**Indicadores chave de desempenho** painel que exibe o número de saudação de unidades produzidas e energia usada pela empresa inteira hello ou linha de fábrica/produção de hello/estação que você está exibindo.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-161">**Key Performance Indicators** panel that displays hello number of units produced and energy used by hello whole enterprise or hello factory/production line/station you are viewing.</span></span> <span data-ttu-id="bd2c5-162">Esses valores são agregados de um nível de empresa toohello estação exibição.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-162">These values are aggregated from a station view toohello enterprise level.</span></span>

## <a name="view-factories"></a><span data-ttu-id="bd2c5-163">Exibir fábricas</span><span class="sxs-lookup"><span data-stu-id="bd2c5-163">View factories</span></span>

<span data-ttu-id="bd2c5-164">Olá *fábricas* painel mostra Olá localização geográfica de todas as fábricas de Olá Olá solução, seus status e configuração de produção atual.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-164">hello *Factories* panel shows you hello geographical location of all hello factories in hello solution, their status, and current production configuration.</span></span> <span data-ttu-id="bd2c5-165">Na lista de locais de saudação, você pode navegar toohello outros níveis na hierarquia de solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-165">From hello locations list, you can navigate toohello other levels in hello solution hierarchy.</span></span> <span data-ttu-id="bd2c5-166">linhas de saudação na lista de saudação são hiperlinks que vinculam os detalhes das linhas de produção de hello nesse local.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-166">hello rows in hello list are hyperlinks that link details of hello production lines at that location.</span></span> <span data-ttu-id="bd2c5-167">É possível toodrill em detalhes da linha de produção de hello e para baixo de exibição de nível de estação de toohello.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-167">It is then possible toodrill into hello production line details and down toohello station level view.</span></span> <span data-ttu-id="bd2c5-168">Você também pode aplicar uma lista de toohello de filtro.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-168">You can also apply a filter toohello list.</span></span>

![Fábricas de solução pré-configurada de fábrica conectada][cf-img-factories] 

1. <span data-ttu-id="bd2c5-170">Olá **painel fábrica** Olá mostra a lista de fábrica para esta solução.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-170">hello **Factory panel** shows hello factory list for this solution.</span></span>

2. <span data-ttu-id="bd2c5-171">lista de fábrica Olá inicialmente mostra seis fábricas criadas pelo processo de provisionamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-171">hello factory list initially shows six factories created by hello provisioning process.</span></span> <span data-ttu-id="bd2c5-172">Você pode adicionar a solução de toohello de dispositivos adicionais simulada e físico.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-172">You can add additional simulated and physical devices toohello solution.</span></span>

3. <span data-ttu-id="bd2c5-173">tooview detalhes de saudação de uma fábrica, clique em lista de fábrica de saudação da linha de saudação.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-173">tooview hello details of a factory, click hello row in hello factory list.</span></span>

4. <span data-ttu-id="bd2c5-174">detalhes de saudação tooview de uma linha de produção, clique em lista de saudação da linha de saudação.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-174">tooview hello details of a production line, click hello row in hello list.</span></span>

5. <span data-ttu-id="bd2c5-175">Olá tooview publicado nós OPC UA da estação na linha de produção de hello, clique em linha hello na lista de saudação.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-175">tooview hello published OPC UA nodes of a station on hello production line, click hello row in hello list.</span></span>

6. <span data-ttu-id="bd2c5-176">tooview detalhes em um nó específico na estação Olá, clique em lista de saudação da linha de saudação.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-176">tooview details on a specific node in hello station, click hello row in hello list.</span></span> <span data-ttu-id="bd2c5-177">Essa ação inicia o painel de contexto Olá com visualizações de informações da série de tempo.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-177">This action launches hello context panel with Time Series Insights visualizations.</span></span> <span data-ttu-id="bd2c5-178">Clique nessas análises adicionais de toodo gráficos em ambiente de explorer Olá Insights de série de tempo.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-178">Click these graphs toodo further analysis in hello Time Series Insights explorer environment.</span></span>

## <a name="view-map"></a><span data-ttu-id="bd2c5-179">Exibir mapa</span><span class="sxs-lookup"><span data-stu-id="bd2c5-179">View map</span></span>

<span data-ttu-id="bd2c5-180">Se sua assinatura tiver acesso toohello API do Bing Maps, Olá *fábricas* mapa mostra localização geográfica hello e o status de todas as fábricas de saudação na solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-180">If your subscription has access toohello Bing Maps API, hello *Factories* map shows you hello geographical location and status of all hello factories in hello solution.</span></span> <span data-ttu-id="bd2c5-181">toodrill detalhes Olá local, clique em locais de saudação exibidos no mapa de saudação.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-181">toodrill into hello location details, click hello locations displayed on hello map.</span></span>

![Mapa de solução pré-configurada de fábrica conectada][cf-img-map]

## <a name="view-alerts"></a><span data-ttu-id="bd2c5-183">Exibir alertas</span><span class="sxs-lookup"><span data-stu-id="bd2c5-183">View alerts</span></span>

<span data-ttu-id="bd2c5-184">Olá **alerta** painel mostra alertas gerados devido tooa relatado valor ou um valor calculado de OEE/KPI exceder seu limite configurado.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-184">hello **Alert** panel shows you alerts generated due tooa reported value or a calculated OEE/KPI value exceeding its configured threshold.</span></span> <span data-ttu-id="bd2c5-185">Esse painel exibe alertas em cada nível da hierarquia de hello, da exibição global do toohello Olá estação exibição de nível.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-185">This panel displays alerts at each level of hello hierarchy, from hello station level view toohello global view.</span></span> <span data-ttu-id="bd2c5-186">alertas de saudação contêm uma descrição do alerta hello, data, hora, local e número de ocorrências.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-186">hello alerts contain a description of hello alert, date, time, location, and number of occurrences.</span></span> <span data-ttu-id="bd2c5-187">Você pode obter informações em dados toohello que causou o alerta de saudação usando Olá dados Insights de série de tempo.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-187">You can gain insights in toohello data that caused hello alert using hello Time Series Insights data.</span></span> <span data-ttu-id="bd2c5-188">Olá tempo série Insights dados são visualizados no hello alertas, onde aplicável.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-188">hello Time Series Insights data is visualized in hello alerts where applicable.</span></span> <span data-ttu-id="bd2c5-189">Se você for um administrador, você pode executar ações de padrão em alertas hello, como:</span><span class="sxs-lookup"><span data-stu-id="bd2c5-189">If you are an Administrator, you can take default actions on hello alerts such as:</span></span>

* <span data-ttu-id="bd2c5-190">Alerta de saudação fechar.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-190">Close hello alert.</span></span>
* <span data-ttu-id="bd2c5-191">Reconhece o alerta de saudação.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-191">Acknowledge hello alert.</span></span>

<span data-ttu-id="bd2c5-192">Opcionalmente, você pode executar ações mais complexas.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-192">Optionally, you can take more complex actions.</span></span> <span data-ttu-id="bd2c5-193">Por exemplo, para Olá pressão OPC UA nó de saudação Assembly, você pode:</span><span class="sxs-lookup"><span data-stu-id="bd2c5-193">For example, for hello Pressure OPC UA Node of hello Assembly you could:</span></span>

* <span data-ttu-id="bd2c5-194">Exiba informações de suporte em uma página da Web em uma nova janela do navegador.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-194">Show supporting information in a web page in a new browser window.</span></span>
* <span data-ttu-id="bd2c5-195">Mitigar a causa de saudação do alerta Olá chamando um método de OPC UA no dispositivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-195">Mitigate hello cause of hello alert by calling an OPC UA method on hello device.</span></span>
* <span data-ttu-id="bd2c5-196">Suprima a disponibilidade de saudação de ações de padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-196">Suppress hello availability of hello default actions.</span></span>

    ![Alertas de solução pré-configurada de fábrica conectada][cf-img-alerts]

> [!NOTE]
> <span data-ttu-id="bd2c5-198">Esses alertas são gerados por regras que são especificadas em um arquivo de configuração na solução Olá pré-configurado.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-198">These alerts are generated by rules that are specified in a configuration file in hello preconfigured solution.</span></span> <span data-ttu-id="bd2c5-199">Essas regras podem gerar alertas quando Olá OEE ou valores KPI ou valores de OPC UA nó estão excedendo o limite configurado.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-199">These rules can generate alerts when hello OEE or KPI figures or OPC UA Node values are exceeding their configured threshold.</span></span>

1. <span data-ttu-id="bd2c5-200">Olá **painel alertas** mostra Olá alertas gerados nesta solução.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-200">hello **Alerts panel** shows hello alerts generated in this solution.</span></span>

2. <span data-ttu-id="bd2c5-201">detalhes de saudação tooview de um alerta, clique no painel de alertas Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-201">tooview hello details of an alert, click hello alert in hello alerts panel.</span></span>

3. <span data-ttu-id="bd2c5-202">toofurther analisar dados de alerta de saudação, clique em gráfico de saudação no ambiente de explorer Olá painel alerta tooopen Olá Insights de série de tempo.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-202">toofurther analyze hello alert data, click hello graph in hello alert panel tooopen hello Time Series Insights explorer environment.</span></span>

4. <span data-ttu-id="bd2c5-203">tooaddress Olá alerta, várias ações estão disponíveis no painel alerta hello.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-203">tooaddress hello alert, several actions are available in hello alert panel.</span></span> <span data-ttu-id="bd2c5-204">Escolha a opção apropriada Olá para você e clique em Olá executar botão de comando de ação.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-204">Choose hello appropriate option for you and click hello execute action command button.</span></span>

## <a name="view-overall-equipment-efficiency"></a><span data-ttu-id="bd2c5-205">Exibir a eficiência geral do equipamento</span><span class="sxs-lookup"><span data-stu-id="bd2c5-205">View overall equipment efficiency</span></span>

<span data-ttu-id="bd2c5-206">Taxas OEE Olá eficiência do processo de produção de hello usando uma chave parâmetros operacionais relacionados à produção.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-206">OEE rates hello efficiency of hello manufacturing process using a key production-related operational parameters.</span></span> <span data-ttu-id="bd2c5-207">OEE é um padrão de medida calculada multiplicando a taxa de disponibilidade hello, a taxa de desempenho e a taxa de qualidade da indústria: OEE = disponibilidade x qualidade de desempenho x.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-207">OEE is an industry standard measure calculated by multiplying hello availability rate, performance rate, and quality rate: OEE = availability x performance x quality.</span></span>

![OEE de solução pré-configurada de fábrica conectada][cf-img-oee]

1. <span data-ttu-id="bd2c5-209">tooview OEE para qualquer nível da hierarquia hello, navegue toohello exibição específica que você precisa.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-209">tooview OEE for any level in hello hierarchy, navigate toohello specific view you require.</span></span> <span data-ttu-id="bd2c5-210">Olá OEE para essa exibição é exibido no painel de saudação junto com cada um dos elementos de saudação que compõem a saudação porcentagem OEE.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-210">hello OEE for that view displays in hello panel along with each of hello elements that make up hello OEE percentage.</span></span>

2. <span data-ttu-id="bd2c5-211">toofurther analisar hello OEE para qualquer nível de dados da hierarquia hello, clique Olá OEE, disponibilidade, desempenho ou porcentagem de qualidade.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-211">toofurther analyze hello OEE for any level in hello hierarchy data, click either hello OEE, availability, performance, or quality percentage.</span></span> <span data-ttu-id="bd2c5-212">Um painel de contexto é exibida com informações da série de tempo alimentadas visualizações que mostra dados de saudação última hora, últimas 24 horas e últimos 7 dias.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-212">A context panel appears with Time Series Insights powered visualizations that shows data from hello last hour, last 24 hours, and last 7 days.</span></span>

    ![Visualização de TSI de solução pré-configurada de fábrica conectada][cf-img-tsi-visualization]

3. <span data-ttu-id="bd2c5-214">toofurther analisar dados de alerta de saudação, clique em gráfico de saudação no painel alerta hello.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-214">toofurther analyze hello alert data, click hello graph in hello alert panel.</span></span> <span data-ttu-id="bd2c5-215">Essa ação abre o ambiente de explorer Olá Insights de série de tempo.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-215">This action opens hello Time Series Insights explorer environment.</span></span>

    ![Explorador de TSI de solução pré-configurada de fábrica conectada][cf-img-tsi-explorer]

## <a name="view-key-performance-indicators"></a><span data-ttu-id="bd2c5-217">Exibir Indicadores Chave de Desempenho</span><span class="sxs-lookup"><span data-stu-id="bd2c5-217">View Key Performance Indicators</span></span>

<span data-ttu-id="bd2c5-218">solução de saudação fornece dois indicadores chave de desempenho, *unidades por hora* e *energia usada em kWh*.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-218">hello solution provides two key performance indicators, *units per hour* and *energy used in kWh*.</span></span>

![KPI de solução pré-configurada de fábrica conectada][cf-img-kpi]

1. <span data-ttu-id="bd2c5-220">unidades de tooview por hora ou energia usada para qualquer nível da hierarquia hello, navegue toohello exibição específica que você precisa.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-220">tooview units per hour or energy used for any level in hello hierarchy, navigate toohello specific view you require.</span></span> <span data-ttu-id="bd2c5-221">unidades de saudação por hora e energia usadas exibição no painel de saudação.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-221">hello units per hour and energy used display in hello panel.</span></span>

2. <span data-ttu-id="bd2c5-222">unidades tooanalyze por hora ou energia usada para qualquer nível na hierarquia de saudação adicional, clique em Olá indicador em hello **indicadores chave de desempenho** painel.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-222">tooanalyze units per hour or energy used for any level in hello hierarchy further, click hello gauge in hello **Key Performance Indicators** panel.</span></span> <span data-ttu-id="bd2c5-223">Um painel de contexto é exibido com visualizações de Insights de série de tempo da plataforma, permitindo que você tooview dados Olá última hora, Olá últimas 24 horas e últimos 7 dias.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-223">A context panel appears with Time Series Insights powered visualizations enabling you tooview data from hello last hour, hello last 24 hours, and last 7 days.</span></span>

## <a name="scenario-review"></a><span data-ttu-id="bd2c5-224">Análise do cenário</span><span class="sxs-lookup"><span data-stu-id="bd2c5-224">Scenario review</span></span>

<span data-ttu-id="bd2c5-225">Nesse cenário, você monitorou os fábricas OEE KPIs valores e, no painel de saudação.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-225">In this scenario, you monitored your factories OEE and KPIs values, in hello dashboard.</span></span> <span data-ttu-id="bd2c5-226">Em seguida, usado tooprovide de informações da série de tempo mais informações toohelp aprofundar ainda mais em dados de telemetria Olá para KPIs e OEE toohelp com detecção de anomalias.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-226">You then used Time Series Insights tooprovide more information toohelp drill further into hello telemetry data for OEE and KPIs toohelp with detecting anomalies.</span></span> <span data-ttu-id="bd2c5-227">Você também usado problemas de tooview do painel alerta Olá com seu fábricas e você usou o alerta de Olá Olá ações disponíveis tooyou tooresolve.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-227">You also used hello alert panel tooview issues with your factories and you used hello actions available tooyou tooresolve hello alert.</span></span>

## <a name="other-features"></a><span data-ttu-id="bd2c5-228">Outros recursos</span><span class="sxs-lookup"><span data-stu-id="bd2c5-228">Other features</span></span>

<span data-ttu-id="bd2c5-229">Olá seções a seguir descreve alguns recursos adicionais de solução de fábrica Olá conectado que não são descritos no cenário anterior hello.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-229">hello following sections describe some additional features of hello connected factory solution that are not described in hello previous scenario.</span></span>

## <a name="apply-filters"></a><span data-ttu-id="bd2c5-230">Aplicar filtros</span><span class="sxs-lookup"><span data-stu-id="bd2c5-230">Apply filters</span></span>

1. <span data-ttu-id="bd2c5-231">Clique em Olá **divisa** toodisplay uma lista de filtros disponíveis no painel de locais de fábrica hello ou painel de alertas de saudação.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-231">Click hello **chevron** toodisplay a list of available filters in either hello factory locations panel or hello alerts panel.</span></span>

2. <span data-ttu-id="bd2c5-232">Painel de filtros de saudação é exibida para você.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-232">hello filters panel is displayed for you.</span></span> 

    ![Filtros de solução pré-configurados de fábrica conectada][cf-img-alert-filter]

3. <span data-ttu-id="bd2c5-234">Escolha o filtro de saudação que você precisa.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-234">Choose hello filter that you require.</span></span> <span data-ttu-id="bd2c5-235">Também é possível tootype o texto livre nos campos de filtro de saudação.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-235">It is also possible tootype free text into hello filter fields.</span></span>

4. <span data-ttu-id="bd2c5-236">saudação de filtro é aplicada para você.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-236">hello filter is then applied for you.</span></span> <span data-ttu-id="bd2c5-237">estado do filtro Olá também é exibido no painel de saudação por meio de um funil que exibe em fábricas hello e tabelas de alertas.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-237">hello filter state is also shown in hello dashboard via a funnel that displays in hello factories and alerts tables.</span></span>

    ![Filtros de solução pré-configurados de fábrica conectada][cf-img-alert-filter-funnel]

    > [!NOTE]
    > <span data-ttu-id="bd2c5-239">Um filtro ativo não afeta valores hello exibido OEE e um KPI, ela apenas filtra o conteúdo da lista de saudação.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-239">An active filter does not affect hello displayed OEE and KPI values, it only filters hello list contents.</span></span>

5. <span data-ttu-id="bd2c5-240">tooclear um filtro, clique em funil hello e filtro no painel de contexto de filtro de saudação.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-240">tooclear a filter, click hello funnel and click filter in hello filter context panel.</span></span> <span data-ttu-id="bd2c5-241">Olá texto **todos os** é exibido no fábricas hello e tabelas de alertas.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-241">hello text **All** is displayed in hello factories and alerts tables.</span></span>

## <a name="browse-an-opc-ua-server"></a><span data-ttu-id="bd2c5-242">Procurar um servidor de OPC UA</span><span class="sxs-lookup"><span data-stu-id="bd2c5-242">Browse an OPC UA server</span></span>

<span data-ttu-id="bd2c5-243">Quando você implanta a solução Olá pré-configurados, você automaticamente provisionar servidores OPC UA simulados que você pode procurar por meio do Gerenciador de soluções de saudação.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-243">When you deploy hello preconfigured solution, you automatically provision simulated OPC UA servers that you can browse via hello solution browser.</span></span> <span data-ttu-id="bd2c5-244">Esses servidores são *servidores OPC UA simulados*.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-244">These servers are *simulated OPC UA servers*.</span></span> <span data-ttu-id="bd2c5-245">Servidores simuladas tornam mais fácil para você tooexperiment com solução Olá pré-configurado sem Olá necessidade toodeploy real servidores físicos.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-245">Simulated servers make it easy for you tooexperiment with hello preconfigured solution without hello need toodeploy real, physical servers.</span></span> <span data-ttu-id="bd2c5-246">Se você quiser tooconnect uma solução de toohello servidor OPC UA real, consulte Olá [conectar sua solução de fábrica pré-configurado OPC UA dispositivo toohello conectado] [ lnk-connect-cf] tutorial.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-246">If you do want tooconnect a real OPC UA server toohello solution, see hello [Connect your OPC UA device toohello connected factory preconfigured solution][lnk-connect-cf] tutorial.</span></span>

1. <span data-ttu-id="bd2c5-247">Clique em Olá **ícone fábrica** na barra de navegação do painel de saudação.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-247">Click hello **factory icon** in hello dashboard navigation bar.</span></span>

    ![Navegador de servidor de chamada de solução pré-configurada de fábrica conectada][cf-img-server-browser]

2. <span data-ttu-id="bd2c5-249">Escolha um dos servidores de saudação lista pré-configurado de saudação.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-249">Choose one of hello servers from hello preconfigured list.</span></span> <span data-ttu-id="bd2c5-250">Esta lista mostra os servidores de saudação que são implantados na solução Olá pré-configurado.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-250">This list shows hello servers that are deployed for you in hello preconfigured solution.</span></span>

    ![Seleção de chamada de solução pré-configurada de fábrica conectada][cf-img-server-choice]

3. <span data-ttu-id="bd2c5-252">Clique em **Conectar**. Uma caixa de diálogo de segurança será exibida.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-252">Click **Connect**, a security dialog displays.</span></span> <span data-ttu-id="bd2c5-253">Simulação de Olá, é seguro tooclick **prosseguir**</span><span class="sxs-lookup"><span data-stu-id="bd2c5-253">For hello simulation, it is safe tooclick **Proceed**</span></span>

4. <span data-ttu-id="bd2c5-254">tooexpand qualquer um de nós de saudação na árvore de saudação do servidor, clique nele.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-254">tooexpand any of hello nodes in hello server tree, click it.</span></span> <span data-ttu-id="bd2c5-255">Nós que estão publicando telemetria têm uma marcação ao lado deles.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-255">Nodes that are publishing telemetry have a tick mark beside them.</span></span>

    ![Árvore de chamada de solução pré-configurada de fábrica conectada][cf-img-server-tree]

5. <span data-ttu-id="bd2c5-257">Clique com botão direito tooread um item, gravar, publicar ou chamar esse nó.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-257">Right-click an item tooread, write, publish, or call that node.</span></span> <span data-ttu-id="bd2c5-258">Olá ações disponíveis tooyou dependem de suas permissões e os atributos de saudação do nó de saudação.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-258">hello actions available tooyou depend on your permissions and hello attributes of hello node.</span></span> <span data-ttu-id="bd2c5-259">Olá ler opção toodisplays um painel de contexto que mostram o valor de saudação do nó específico hello.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-259">hello read option toodisplays a context panel showing hello value of hello specific node.</span></span> <span data-ttu-id="bd2c5-260">Olá gravar opção exibe um painel de contexto em que você pode inserir um novo valor.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-260">hello write option displays a context panel where you can enter a new value.</span></span> <span data-ttu-id="bd2c5-261">opção de chamada Hello exibe um nó onde você pode inserir parâmetros Olá para chamada de saudação.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-261">hello call option displays a node where you can enter hello parameters for hello call.</span></span>

## <a name="publish-a-node"></a><span data-ttu-id="bd2c5-262">Publicar um nó</span><span class="sxs-lookup"><span data-stu-id="bd2c5-262">Publish a node</span></span>

<span data-ttu-id="bd2c5-263">Quando você procura um *server simulada de OPC UA*, você também pode escolher toopublish novos nós.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-263">When you browse a *simulated OPC UA server*, you can also choose toopublish new nodes.</span></span> <span data-ttu-id="bd2c5-264">Você pode analisar a telemetria de saudação desses nós na solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-264">You can analyze hello telemetry from these nodes in hello solution.</span></span> <span data-ttu-id="bd2c5-265">Essas *simulados servidores OPC UA* torná-lo tooexperiment fácil com a solução Olá pré-configurado sem implantar dispositivos físicos reais.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-265">These *simulated OPC UA servers* make it easy tooexperiment with hello preconfigured solution without deploying real, physical devices.</span></span>

1. <span data-ttu-id="bd2c5-266">Procure nó tooa Olá árvore do navegador OPC UA server que você deseja toopublish.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-266">Browse tooa node in hello OPC UA server browser tree that you wish toopublish.</span></span>

2. <span data-ttu-id="bd2c5-267">Nó de saudação com o botão direito.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-267">Right-click hello node.</span></span>

3. <span data-ttu-id="bd2c5-268">Escolha **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-268">Choose **Publish**.</span></span>

    ![A fábrica conectada publica o nó][cf-img-publish-node]

4. <span data-ttu-id="bd2c5-270">Um painel de contexto é exibido que informa que Olá publicação foi bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-270">A context panel appears which tells you that hello publish has succeeded.</span></span> <span data-ttu-id="bd2c5-271">nó de saudação aparece na exibição de nível de estação Olá com uma marca de seleção ao lado dela.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-271">hello node appears in hello station level view with a check mark beside it.</span></span>

    ![Publicação com êxito de chamada de solução pré-configurada de fábrica conectada][cf-img-publish-success]

## <a name="command-and-control"></a><span data-ttu-id="bd2c5-273">Comando e controle</span><span class="sxs-lookup"><span data-stu-id="bd2c5-273">Command and control</span></span>

<span data-ttu-id="bd2c5-274">fábrica conectado Olá permite comando e controlar os dispositivos de setor diretamente da nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-274">hello connected factory allows you command and control your industry devices directly from hello cloud.</span></span> <span data-ttu-id="bd2c5-275">Você pode usar este tooalerts toorespond de recurso gerado pelo dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-275">You can use this feature toorespond tooalerts generated by hello device.</span></span> <span data-ttu-id="bd2c5-276">Por exemplo, você pode enviar um dispositivo de toohello do comando de nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-276">For example, you could send a command toohello device from hello cloud.</span></span> <span data-ttu-id="bd2c5-277">Você pode encontrar hello comandos disponíveis no hello **StationCommands** nó Olá árvore do navegador de servidores de OPC UA.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-277">You can find hello available commands in hello **StationCommands** node in hello OPC UA servers browser tree.</span></span> <span data-ttu-id="bd2c5-278">Nesse cenário, você deve abrir uma válvula de versão de pressão na estação de assembly de saudação de uma linha de produção em Munique.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-278">In this scenario, you open a pressure release valve on hello assembly station of a production line in Munich.</span></span> <span data-ttu-id="bd2c5-279">toouse Olá comando e controle de funcionalidade, você deve estar no hello **administrador** função hello pré-configurado a implantação da solução.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-279">toouse hello command and control functionality, you must be in hello **Administrator** role for hello preconfigured solution deployment.</span></span>

1. <span data-ttu-id="bd2c5-280">Procurar toohello **StationCommands** nó Olá árvore do navegador de servidor OPC UA.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-280">Browse toohello **StationCommands** node in hello OPC UA server browser tree.</span></span>

2. <span data-ttu-id="bd2c5-281">Escolha o comando Olá que você deseja usar.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-281">Choose hello command that you wish use.</span></span>

3. <span data-ttu-id="bd2c5-282">Nó de saudação com o botão direito.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-282">Right-click hello node.</span></span>

4. <span data-ttu-id="bd2c5-283">Escolha **Chamar**.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-283">Choose **Call**.</span></span>

    ![Comando de chamada de solução pré-configurada de fábrica conectada][cf-img-call-command]

5. <span data-ttu-id="bd2c5-285">Um painel de contexto é exibido informando a você qual método você sobre toocall e quaisquer detalhes de parâmetro é aplicável.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-285">A context panel appears informing you which method you are about toocall and any parameter details is applicable.</span></span>

6. <span data-ttu-id="bd2c5-286">Escolha **Chamar**.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-286">Choose **Call**.</span></span>

    ![Contexto de chamada de solução pré-configurada de fábrica conectada][cf-img-call-context]

7. <span data-ttu-id="bd2c5-288">Painel de contexto de saudação é atualizada tooinform que Olá chamada de método foi bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-288">hello context panel is updated tooinform you that hello method call succeeded.</span></span> <span data-ttu-id="bd2c5-289">Você pode verificar a chamada hello teve êxito ao ler o valor de saudação do nó de pressão Olá atualizados como resultado da chamada de saudação.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-289">You can verify hello call succeeded by reading hello value of hello pressure node that updated as a result of hello call.</span></span>

    ![Sucesso de chamada de solução pré-configurada de fábrica conectada][cf-img-call-success]


## <a name="behind-hello-scenes"></a><span data-ttu-id="bd2c5-291">Em segundo plano da saudação</span><span class="sxs-lookup"><span data-stu-id="bd2c5-291">Behind hello scenes</span></span>

<span data-ttu-id="bd2c5-292">Quando você implanta uma solução pré-configurada, o processo de implantação de saudação cria vários recursos no hello assinatura do Azure que você selecionou.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-292">When you deploy a preconfigured solution, hello deployment process creates multiple resources in hello Azure subscription you selected.</span></span> <span data-ttu-id="bd2c5-293">Você pode exibir esses recursos no hello Azure [portal][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="bd2c5-293">You can view these resources in hello Azure [portal][lnk-portal].</span></span> <span data-ttu-id="bd2c5-294">o processo de implantação Olá cria um **grupo de recursos** com um nome baseado no nome hello escolhido para sua solução pré-configurada:</span><span class="sxs-lookup"><span data-stu-id="bd2c5-294">hello deployment process creates a **resource group** with a name based on hello name you choose for your preconfigured solution:</span></span>

![Solução pré-configurada em Olá portal do Azure][img-cf-portal]

<span data-ttu-id="bd2c5-296">Você pode exibir configurações de saudação de cada recurso, selecionando-o na lista de saudação de recursos no grupo de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-296">You can view hello settings of each resource by selecting it in hello list of resources in hello resource group.</span></span>

<span data-ttu-id="bd2c5-297">Você também pode exibir o código-fonte Olá para solução de saudação pré-configurado.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-297">You can also view hello source code for hello preconfigured solution.</span></span> <span data-ttu-id="bd2c5-298">Olá conectado fábrica pré-configurado solução código-fonte está em Olá [azure iot-conectado-fábrica] [ lnk-cfgithub] repositório GitHub:</span><span class="sxs-lookup"><span data-stu-id="bd2c5-298">hello connected factory preconfigured solution source code is in hello [azure-iot-connected-factory][lnk-cfgithub] GitHub repository:</span></span>

<span data-ttu-id="bd2c5-299">Quando você terminar, você pode excluir solução Olá pré-configurado de sua assinatura do Azure em Olá [azureiotsuite.com] [ lnk-azureiotsuite] site.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-299">When you are done, you can delete hello preconfigured solution from your Azure subscription on hello [azureiotsuite.com][lnk-azureiotsuite] site.</span></span> <span data-ttu-id="bd2c5-300">Este site permite que você exclua tooeasily que todos os recursos que foram provisionados quando você criou a solução Olá pré-configurado de hello.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-300">This site enables you tooeasily delete all hello resources that were provisioned when you created hello preconfigured solution.</span></span>

> [!NOTE]
> <span data-ttu-id="bd2c5-301">tooensure excluir tudo relacionados à solução toohello pré-configurado, excluí-la em Olá [azureiotsuite.com] [ lnk-azureiotsuite] site.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-301">tooensure that you delete everything related toohello preconfigured solution, delete it on hello [azureiotsuite.com][lnk-azureiotsuite] site.</span></span> <span data-ttu-id="bd2c5-302">Não exclua o grupo de recursos de saudação no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="bd2c5-302">Do not delete hello resource group in hello portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bd2c5-303">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="bd2c5-303">Next Steps</span></span>

<span data-ttu-id="bd2c5-304">Agora que você implantou uma solução de trabalho pré-configurados, você pode continuar a guia de Introdução com IoT Suite lendo Olá artigos a seguir:</span><span class="sxs-lookup"><span data-stu-id="bd2c5-304">Now that you’ve deployed a working preconfigured solution, you can continue getting started with IoT Suite by reading hello following articles:</span></span>

* <span data-ttu-id="bd2c5-305">[Passo a passo de solução pré-configurada de fábrica conectada][lnk-rm-walkthrough]</span><span class="sxs-lookup"><span data-stu-id="bd2c5-305">[Connected factory preconfigured solution walkthrough][lnk-rm-walkthrough]</span></span>
* <span data-ttu-id="bd2c5-306">[Conectar sua solução do dispositivo toohello conectado fábrica pré-configurado][lnk-connect-cf]</span><span class="sxs-lookup"><span data-stu-id="bd2c5-306">[Connect your device toohello Connected factory preconfigured solution][lnk-connect-cf]</span></span>
* <span data-ttu-id="bd2c5-307">[Permissões no site de azureiotsuite.com Olá][lnk-permissions]</span><span class="sxs-lookup"><span data-stu-id="bd2c5-307">[Permissions on hello azureiotsuite.com site][lnk-permissions]</span></span>

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