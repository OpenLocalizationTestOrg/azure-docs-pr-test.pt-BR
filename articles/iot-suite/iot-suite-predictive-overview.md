---
title: "manutenção aaaPredictive pré-configurado solução | Microsoft Docs"
description: "Uma descrição da manutenção preditiva do hello Azure IoT Suite pré-configurado solução."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: b370b3d7-2ce5-4906-9818-3aeedd471ee3
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 2d09801467d33db6b7d6333fa071aea2bf573f20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="predictive-maintenance-preconfigured-solution-overview"></a><span data-ttu-id="6be8f-103">Visão geral da solução pré-configurada de manutenção preditiva</span><span class="sxs-lookup"><span data-stu-id="6be8f-103">Predictive maintenance preconfigured solution overview</span></span>

<span data-ttu-id="6be8f-104">Olá *manutenção preditiva* [pré-configurado solução] [ lnk_preconfigured_solutions] é uma saudação [Microsoft Azure IoT Suite] [ lnk_iot_suite] soluções pré-configuradas.</span><span class="sxs-lookup"><span data-stu-id="6be8f-104">hello *predictive maintenance* [preconfigured solution][lnk_preconfigured_solutions] is one of hello [Microsoft Azure IoT Suite][lnk_iot_suite] preconfigured solutions.</span></span> <span data-ttu-id="6be8f-105">Essa solução integra a coleta de telemetria do dispositivo em tempo real com um modelo preditivo criado com o [Azure Machine Learning][lnk-machine-learning].</span><span class="sxs-lookup"><span data-stu-id="6be8f-105">This solution integrates real-time device telemetry collection with a predictive model created using [Azure Machine Learning][lnk-machine-learning].</span></span>

<span data-ttu-id="6be8f-106">Com o Azure IoT Suite, você pode rapidamente e facilmente conectam tooand monitor ativos e analisar a telemetria em tempo real em painéis e visualizações.</span><span class="sxs-lookup"><span data-stu-id="6be8f-106">With Azure IoT Suite, you can quickly and easily connect tooand monitor assets, and analyze telemetry in real time in dashboards and visualizations.</span></span> <span data-ttu-id="6be8f-107">Solução de manutenção preditiva hello, visualizações e painéis Olá fornecem nova inteligência que pode gerar eficiência e aumentar a fluxos de receita.</span><span class="sxs-lookup"><span data-stu-id="6be8f-107">In hello predictive maintenance solution, hello dashboards and visualizations provide you with new intelligence that can drive efficiencies and enhance revenue streams.</span></span>

## <a name="hello-scenario"></a><span data-ttu-id="6be8f-108">Olá cenário</span><span class="sxs-lookup"><span data-stu-id="6be8f-108">hello Scenario</span></span>

<span data-ttu-id="6be8f-109">A Fabrikam é uma companhia aérea regional que se dedica a fornecer uma excelente experiência ao cliente a preços competitivos.</span><span class="sxs-lookup"><span data-stu-id="6be8f-109">Fabrikam is a regional airline that focuses on great customer experience at competitive prices.</span></span> <span data-ttu-id="6be8f-110">Uma das causas de atrasos de voos são problemas de manutenção e a manutenção dos motores de aeronave representa um desafio singular.</span><span class="sxs-lookup"><span data-stu-id="6be8f-110">One cause of flight delays is maintenance issues and aircraft engine maintenance is particularly challenging.</span></span> <span data-ttu-id="6be8f-111">A Fabrikam deve evitar falha do mecanismo durante o voo todo custo, portanto ele inspeciona seus mecanismos regularmente e agenda de manutenção de acordo com o plano de tooa.</span><span class="sxs-lookup"><span data-stu-id="6be8f-111">Fabrikam must avoid engine failure during flight at all costs, so it inspects its engines regularly and schedules maintenance according tooa plan.</span></span> <span data-ttu-id="6be8f-112">No entanto, aeronave mecanismos sempre não desempenham Olá mesmo.</span><span class="sxs-lookup"><span data-stu-id="6be8f-112">However, aircraft engines don’t always wear hello same.</span></span> <span data-ttu-id="6be8f-113">Algum tipo de manutenção desnecessária é realizada nos motores.</span><span class="sxs-lookup"><span data-stu-id="6be8f-113">Some unnecessary maintenance is performed on engines.</span></span> <span data-ttu-id="6be8f-114">O mais importante é que problemas ocorrem, o que pode fazer com que uma aeronave permaneça em solo até que a manutenção seja realizada.</span><span class="sxs-lookup"><span data-stu-id="6be8f-114">More importantly, issues arise which can ground an aircraft until maintenance is performed.</span></span> <span data-ttu-id="6be8f-115">Se um avião estiver em um local onde Olá técnicos direita ou peças de reposição não estiverem disponíveis, esses problemas podem ser especialmente dispendiosos.</span><span class="sxs-lookup"><span data-stu-id="6be8f-115">If an aircraft is at a location where hello right technicians or spare parts are not available, these issues can be especially costly.</span></span>

<span data-ttu-id="6be8f-116">mecanismos de saudação do aeronave da Fabrikam são instrumentados com sensores que monitoram as condições de mecanismo durante o trânsito.</span><span class="sxs-lookup"><span data-stu-id="6be8f-116">hello engines of Fabrikam’s aircraft are instrumented with sensors that monitor engine conditions during flight.</span></span> <span data-ttu-id="6be8f-117">A Fabrikam usa Olá manutenção preditiva solução toocollect Olá sensor dados coletados durante o voo Olá.</span><span class="sxs-lookup"><span data-stu-id="6be8f-117">Fabrikam uses hello predictive maintenance solution toocollect hello sensor data collected during hello flight.</span></span> <span data-ttu-id="6be8f-118">Após acumulando anos de mecanismo operacional e dados de falha, os cientistas de dados da Fabrikam têm modelada uma saudação toopredict de maneira vida útil restante (regra) de um mecanismo de aeronave.</span><span class="sxs-lookup"><span data-stu-id="6be8f-118">After accumulating years of engine operational and failure data, Fabrikam’s data scientists have modeled a way toopredict hello Remaining Useful Life (RUL) of an aircraft engine.</span></span> <span data-ttu-id="6be8f-119">modelo de saudação usa uma correlação entre dados de quatro sensores de mecanismo hello e desgaste mecanismo que leva tooeventual falha.</span><span class="sxs-lookup"><span data-stu-id="6be8f-119">hello model uses a correlation between data from four of hello engine sensors and engine wear that leads tooeventual failure.</span></span> <span data-ttu-id="6be8f-120">Enquanto a Fabrikam continua a segurança de tooensure tooperform inspeções regular, podem ser usadas Olá modelos toocompute Olá regra para cada mecanismo após cada voo.</span><span class="sxs-lookup"><span data-stu-id="6be8f-120">While Fabrikam continues tooperform regular inspections tooensure safety, it can now use hello models toocompute hello RUL for each engine after every flight.</span></span> <span data-ttu-id="6be8f-121">modelo de saudação usa telemetria Olá coletada de mecanismos de saudação durante o voo hello.</span><span class="sxs-lookup"><span data-stu-id="6be8f-121">hello model uses hello telemetry collected from hello engines during hello flight.</span></span> <span data-ttu-id="6be8f-122">A Fabrikam agora pode prever os futuros pontos de falha e planejar a manutenção e reparar antecipadamente.</span><span class="sxs-lookup"><span data-stu-id="6be8f-122">Fabrikam can now predict future points of failure and plan for maintenance and repair in advance.</span></span>

> [!NOTE]
> <span data-ttu-id="6be8f-123">modelo de solução de saudação usa dados de desgaste de mecanismo real.</span><span class="sxs-lookup"><span data-stu-id="6be8f-123">hello solution model uses actual engine wear data.</span></span>

<span data-ttu-id="6be8f-124">Por prever ponto hello quando a manutenção seja necessária, Fabrikam pode otimizar os custos de tooreduce de operações.</span><span class="sxs-lookup"><span data-stu-id="6be8f-124">By predicting hello point when maintenance is required, Fabrikam can optimize its operations tooreduce costs.</span></span>

<span data-ttu-id="6be8f-125">Coordenadores de manutenção trabalham com os agendadores para:</span><span class="sxs-lookup"><span data-stu-id="6be8f-125">Maintenance coordinators work with schedulers to:</span></span>

- <span data-ttu-id="6be8f-126">Plano de manutenção toocoincide com um avião parar em um local específico.</span><span class="sxs-lookup"><span data-stu-id="6be8f-126">Plan maintenance toocoincide with an aircraft stopping at a particular location.</span></span>
- <span data-ttu-id="6be8f-127">Certifique-se de tempo suficiente está disponível para Olá aeronave toobe fora de serviço sem causar interrupções de agenda.</span><span class="sxs-lookup"><span data-stu-id="6be8f-127">Ensure sufficient time is available for hello aircraft toobe out of service without causing schedule disruption.</span></span>
- <span data-ttu-id="6be8f-128">os técnicos de tooschedule tooensure que aeronave é atendida com eficiência sem tempo de espera.</span><span class="sxs-lookup"><span data-stu-id="6be8f-128">tooschedule technicians tooensure that aircraft are serviced efficiently without wait time.</span></span>

<span data-ttu-id="6be8f-129">Os gerentes de controle de inventário recebem planos de manutenção, para que possam otimizar seu processo de encomendas e inventário de peças de reposição.</span><span class="sxs-lookup"><span data-stu-id="6be8f-129">Inventory control managers receive maintenance plans, so they can optimize their ordering process and spare parts inventory.</span></span>

<span data-ttu-id="6be8f-130">Essas atividades habilitar horário de início do Fabrikam toominimize aeronave e reduzem os custos operacionais, garantindo a segurança Olá de passageiros e equipe.</span><span class="sxs-lookup"><span data-stu-id="6be8f-130">These activities enable Fabrikam toominimize aircraft ground time and reduce operating costs while ensuring hello safety of passengers and crew.</span></span>

<span data-ttu-id="6be8f-131">toounderstand como [Azure IoT Suite] [ lnk_iot_suite] fornece recursos que os clientes Olá precisam potencial de saudação toorealize manutenção preditiva, examine [infográfico] [lnk_infographic].</span><span class="sxs-lookup"><span data-stu-id="6be8f-131">toounderstand how [Azure IoT Suite][lnk_iot_suite] provides hello capabilities customers need toorealize hello potential of predictive maintenance, review this [infographic][lnk_infographic].</span></span>

## <a name="how-hello-predictive-maintenance-solution-is-built"></a><span data-ttu-id="6be8f-132">Como solução de manutenção preditiva Olá é criada</span><span class="sxs-lookup"><span data-stu-id="6be8f-132">How hello predictive maintenance solution is built</span></span>

<span data-ttu-id="6be8f-133">solução de saudação usa um modelo de aprendizado de máquina do Azure existente como um modelo tooshow esses recursos trabalhando de telemetria do dispositivo coletada por meio de serviços do IoT Suite.</span><span class="sxs-lookup"><span data-stu-id="6be8f-133">hello solution uses an existing Azure Machine Learning model available as a template tooshow these capabilities working from device telemetry collected through IoT Suite services.</span></span> <span data-ttu-id="6be8f-134">A Microsoft criou um [modelo de regressão] [ lnk_regression_model] de um mecanismo de aeronave com base nos dados publicamente disponíveis<sup>\[1\]</sup>e passo a passo orientação sobre como toouse Olá modelo.</span><span class="sxs-lookup"><span data-stu-id="6be8f-134">Microsoft has built a [regression model][lnk_regression_model] of an aircraft engine based on publically available data<sup>\[1\]</sup>, and step-by-step guidance on how toouse hello model.</span></span>

<span data-ttu-id="6be8f-135">Olá solução de manutenção preditiva IoT do Azure usa o modelo de regressão de saudação criado com base neste modelo.</span><span class="sxs-lookup"><span data-stu-id="6be8f-135">hello Azure IoT predictive maintenance solution uses hello regression model created from this template.</span></span> <span data-ttu-id="6be8f-136">modelo de saudação é implantado em sua assinatura do Azure e exposto por meio de uma API gerada automaticamente.</span><span class="sxs-lookup"><span data-stu-id="6be8f-136">hello model is deployed into your Azure subscription and exposed through an automatically generated API.</span></span> <span data-ttu-id="6be8f-137">solução de saudação inclui um subconjunto de saudação representando 4 (do total de 100) de dados de teste mecanismos e fluxos de dados de sensor Olá 4 (do total de 21).</span><span class="sxs-lookup"><span data-stu-id="6be8f-137">hello solution includes a subset of hello testing data representing 4 (of 100 total) engines and hello 4 (of 21 total) sensor data streams.</span></span> <span data-ttu-id="6be8f-138">Esses dados são suficiente tooprovide um resultado preciso do modelo treinado hello.</span><span class="sxs-lookup"><span data-stu-id="6be8f-138">This data is sufficient tooprovide an accurate result from hello trained model.</span></span>

<span data-ttu-id="6be8f-139">*\[1\] A. Saxena e K. Goebel (2008). “Turbofan Engine Degradation Simulation Data Set” (Conjunto de dados da simulação de degradação do turbofan), Repositório de dados de prognóstico da NASA Ames (http://ti.arc.nasa.gov/tech/dash/pcoe/prognostic-data-repository/), NASA Ames Research Center, Moffett Field, CA*</span><span class="sxs-lookup"><span data-stu-id="6be8f-139">*\[1\] A. Saxena and K. Goebel (2008). "Turbofan Engine Degradation Simulation Data Set", NASA Ames Prognostics Data Repository (http://ti.arc.nasa.gov/tech/dash/pcoe/prognostic-data-repository/), NASA Ames Research Center, Moffett Field, CA*</span></span>

## <a name="get-started-with-predictive-maintenance"></a><span data-ttu-id="6be8f-140">Introdução à manutenção de previsão</span><span class="sxs-lookup"><span data-stu-id="6be8f-140">Get started with predictive maintenance</span></span>

<span data-ttu-id="6be8f-141">Este tutorial mostra como tooprovision Olá solução manutenção preditiva.</span><span class="sxs-lookup"><span data-stu-id="6be8f-141">This tutorial shows you how tooprovision hello predictive maintenance solution.</span></span> <span data-ttu-id="6be8f-142">Ele também orienta você por meio de recursos básicos de saudação de solução de manutenção preditiva hello.</span><span class="sxs-lookup"><span data-stu-id="6be8f-142">It also walks you through hello basic features of hello predictive maintenance solution.</span></span> <span data-ttu-id="6be8f-143">Você pode acessar muitos desses recursos por meio do painel de solução de saudação implanta junto com a solução Olá pré-configurado.</span><span class="sxs-lookup"><span data-stu-id="6be8f-143">You can access many of these features through hello solution dashboard that deploys along with hello preconfigured solution.</span></span>

<span data-ttu-id="6be8f-144">toocomplete neste tutorial, você precisa de uma assinatura ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="6be8f-144">toocomplete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="6be8f-145">Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="6be8f-145">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="6be8f-146">Para obter detalhes, consulte [Avaliação gratuita do Azure][lnk_free_trial].</span><span class="sxs-lookup"><span data-stu-id="6be8f-146">For details, see [Azure Free Trial][lnk_free_trial].</span></span>

1. <span data-ttu-id="6be8f-147">Faça logon no muito[azureiotsuite.com] [ lnk-azureiotsuite] usando o Azure, as credenciais de conta e clique em  **+**  toocreate uma solução.</span><span class="sxs-lookup"><span data-stu-id="6be8f-147">Log on too[azureiotsuite.com][lnk-azureiotsuite] using your Azure account credentials, and click **+** toocreate a solution.</span></span>
1. <span data-ttu-id="6be8f-148">Clique em **selecione** Olá **manutenção preditiva** lado a lado.</span><span class="sxs-lookup"><span data-stu-id="6be8f-148">Click **Select** hello **Predictive maintenance** tile.</span></span>
1. <span data-ttu-id="6be8f-149">Insira um **nome da solução** sua manutenção previsão pré-configurados de solução.</span><span class="sxs-lookup"><span data-stu-id="6be8f-149">Enter a **Solution name** for your predictive maintenance preconfigured solution.</span></span>
1. <span data-ttu-id="6be8f-150">Selecione Olá **região** e **assinatura** deseja toouse tooprovision Olá solução.</span><span class="sxs-lookup"><span data-stu-id="6be8f-150">Select hello **Region** and **Subscription** you want toouse tooprovision hello solution.</span></span>
1. <span data-ttu-id="6be8f-151">Clique em **criar solução** Olá toobegin processo de provisionamento.</span><span class="sxs-lookup"><span data-stu-id="6be8f-151">Click **Create Solution** toobegin hello provisioning process.</span></span> <span data-ttu-id="6be8f-152">Normalmente, esse processo leva vários toorun de minutos.</span><span class="sxs-lookup"><span data-stu-id="6be8f-152">This process typically takes several minutes toorun.</span></span>

### <a name="wait-for-hello-provisioning-process-toocomplete"></a><span data-ttu-id="6be8f-153">Aguarde a saudação toocomplete do processo de provisionamento</span><span class="sxs-lookup"><span data-stu-id="6be8f-153">Wait for hello provisioning process toocomplete</span></span>

1. <span data-ttu-id="6be8f-154">Clique em bloco de saudação para sua solução com **provisionamento** status.</span><span class="sxs-lookup"><span data-stu-id="6be8f-154">Click hello tile for your solution with **Provisioning** status.</span></span>
1. <span data-ttu-id="6be8f-155">Saudação de aviso **provisionamento estados** como serviços do Azure são implantados na sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="6be8f-155">Notice hello **Provisioning states** as Azure services are deployed in your Azure subscription.</span></span>
1. <span data-ttu-id="6be8f-156">Após a conclusão do provisionamento, Olá alterações de status muito**pronto**.</span><span class="sxs-lookup"><span data-stu-id="6be8f-156">Once provisioning completes, hello status changes too**Ready**.</span></span>
1. <span data-ttu-id="6be8f-157">Clique em Olá bloco toosee Olá detalhes de sua solução no painel direito da saudação.</span><span class="sxs-lookup"><span data-stu-id="6be8f-157">Click hello tile toosee hello details of your solution in hello right-hand pane.</span></span> <span data-ttu-id="6be8f-158">Nesse painel, você pode iniciar Olá solução painel de controle e acesso Olá aprendizado de máquina espaço de trabalho.</span><span class="sxs-lookup"><span data-stu-id="6be8f-158">From this pane, you can launch hello solution dashboard and access hello Machine Learning workspace.</span></span>

> [!NOTE]
> <span data-ttu-id="6be8f-159">Se você encontrar problemas de implantação de solução Olá pré-configurado, examine [permissões no site do hello azureiotsuite.com] [ lnk-permissions] e hello [perguntas frequentes sobre] [ lnk-faq].</span><span class="sxs-lookup"><span data-stu-id="6be8f-159">If you encounter issues deploying hello preconfigured solution, review [Permissions on hello azureiotsuite.com site][lnk-permissions] and hello [FAQ][lnk-faq].</span></span> <span data-ttu-id="6be8f-160">Se os problemas de saudação persistirem, criar um tíquete de serviço em Olá [portal][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="6be8f-160">If hello issues persist, create a service ticket on hello [portal][lnk-portal].</span></span>

<span data-ttu-id="6be8f-161">Há detalhes esperado toosee que não estejam listados para sua solução?</span><span class="sxs-lookup"><span data-stu-id="6be8f-161">Are there details you'd expect toosee that aren't listed for your solution?</span></span> <span data-ttu-id="6be8f-162">Envie sugestões de recursos no [User Voice](https://feedback.azure.com/forums/321918-azure-iot).</span><span class="sxs-lookup"><span data-stu-id="6be8f-162">Give us feature suggestions on [User Voice](https://feedback.azure.com/forums/321918-azure-iot).</span></span>

## <a name="view-hello-solution"></a><span data-ttu-id="6be8f-163">Solução de saudação do modo de exibição</span><span class="sxs-lookup"><span data-stu-id="6be8f-163">View hello solution</span></span>

<span data-ttu-id="6be8f-164">Esta seção orienta você por meio da solução de saudação da interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="6be8f-164">This section guides you through hello solution UI.</span></span>

### <a name="predictive-maintenance-dashboard"></a><span data-ttu-id="6be8f-165">Painel Manutenção Preditiva</span><span class="sxs-lookup"><span data-stu-id="6be8f-165">Predictive Maintenance Dashboard</span></span>

<span data-ttu-id="6be8f-166">Esta página no aplicativo da web hello usa PowerBI JavaScript controles (consulte Olá [repositório PowerBI-visuals][lnk-powerbi]) toovisualize:</span><span class="sxs-lookup"><span data-stu-id="6be8f-166">This page in hello web application uses PowerBI JavaScript controls (see hello [PowerBI-visuals repository][lnk-powerbi]) toovisualize:</span></span>

* <span data-ttu-id="6be8f-167">dados de saída de saudação de trabalhos do Stream Analytics Olá no armazenamento de blob.</span><span class="sxs-lookup"><span data-stu-id="6be8f-167">hello output data from hello Stream Analytics jobs in blob storage.</span></span>
* <span data-ttu-id="6be8f-168">Olá regra e ciclo de contagem por mecanismo aeronave.</span><span class="sxs-lookup"><span data-stu-id="6be8f-168">hello RUL and cycle count per aircraft engine.</span></span>

### <a name="observing-hello-behavior-of-hello-cloud-solution"></a><span data-ttu-id="6be8f-169">Observar o comportamento de saudação da solução de nuvem Olá</span><span class="sxs-lookup"><span data-stu-id="6be8f-169">Observing hello behavior of hello cloud solution</span></span>

<span data-ttu-id="6be8f-170">Em Olá portal do Azure, navegue até o grupo de recursos toohello com o nome da solução Olá você escolheu tooview seus recursos provisionados.</span><span class="sxs-lookup"><span data-stu-id="6be8f-170">In hello Azure portal, navigate toohello resource group with hello solution name you chose tooview your provisioned resources.</span></span>

![][img-resource-group]

<span data-ttu-id="6be8f-171">Quando você provisiona solução Olá pré-configurados, você recebe um email com um espaço de trabalho do aprendizado de máquina de toohello do link.</span><span class="sxs-lookup"><span data-stu-id="6be8f-171">When you provision hello preconfigured solution, you receive an email with a link toohello Machine Learning workspace.</span></span> <span data-ttu-id="6be8f-172">Você também pode navegar toohello o espaço de trabalho de aprendizado de máquina da saudação [azureiotsuite.com] [ lnk-azureiotsuite] página para sua solução provisionada.</span><span class="sxs-lookup"><span data-stu-id="6be8f-172">You can also navigate toohello Machine Learning workspace from hello [azureiotsuite.com][lnk-azureiotsuite] page for your provisioned solution.</span></span> <span data-ttu-id="6be8f-173">Um bloco está disponível nesta página quando Olá solução no hello **pronto** estado.</span><span class="sxs-lookup"><span data-stu-id="6be8f-173">A tile is available on this page when hello solution is in hello **Ready** state.</span></span>

![][img-machine-learning]

<span data-ttu-id="6be8f-174">No portal de solução hello, você pode ver que esse exemplo hello está provisionado com dois aeronave de toorepresent de quatro dispositivos simulada com dois mecanismos por aeronave, cada um com quatro sensores.</span><span class="sxs-lookup"><span data-stu-id="6be8f-174">In hello solution portal, you can see that hello sample is provisioned with four simulated devices toorepresent two aircraft with two engines per aircraft, each with four sensors.</span></span> <span data-ttu-id="6be8f-175">Quando você navega pela primeira vez o portal de solução toohello, simulação Olá será interrompida.</span><span class="sxs-lookup"><span data-stu-id="6be8f-175">When you first navigate toohello solution portal, hello simulation is stopped.</span></span>

![][img-simulation-stopped]

<span data-ttu-id="6be8f-176">Clique em **iniciar simulação** toobegin simulação de saudação.</span><span class="sxs-lookup"><span data-stu-id="6be8f-176">Click **Start simulation** toobegin hello simulation.</span></span> <span data-ttu-id="6be8f-177">Olá histórico de sensor, regra, ciclos e regra de histórico de preencher o painel de saudação.</span><span class="sxs-lookup"><span data-stu-id="6be8f-177">hello sensor history, RUL, Cycles, and RUL history populate hello dashboard.</span></span>

![][img-simulation-running]

<span data-ttu-id="6be8f-178">Quando a regra for menor que 160 (um limite arbitrário escolhido para fins de demonstração), o portal de solução de saudação exibe um toohello próximo de símbolo de aviso regra exibir.</span><span class="sxs-lookup"><span data-stu-id="6be8f-178">When RUL is less than 160 (an arbitrary threshold chosen for demonstration purposes), hello solution portal displays a warning symbol next toohello RUL display.</span></span> <span data-ttu-id="6be8f-179">portal de solução Olá também destaca o mecanismo de aeronave Olá em amarelo.</span><span class="sxs-lookup"><span data-stu-id="6be8f-179">hello solution portal also highlights hello aircraft engine in yellow.</span></span> <span data-ttu-id="6be8f-180">Observe como os valores de regra Olá têm uma tendência descendente geral geral, mas tendem a toobounce para cima e para baixo.</span><span class="sxs-lookup"><span data-stu-id="6be8f-180">Notice how hello RUL values have a general downward trend overall, but tend toobounce up and down.</span></span> <span data-ttu-id="6be8f-181">Esse comportamento resulta de comprimentos de ciclo de variáveis hello e precisão do modelo hello.</span><span class="sxs-lookup"><span data-stu-id="6be8f-181">This behavior results from hello varying cycle lengths and hello model accuracy.</span></span>

![][img-simulation-warning]

<span data-ttu-id="6be8f-182">simulação completa Olá leva cerca de 35 toocomplete de minutos 148 ciclos.</span><span class="sxs-lookup"><span data-stu-id="6be8f-182">hello full simulation takes around 35 minutes toocomplete 148 cycles.</span></span> <span data-ttu-id="6be8f-183">Olá 160 regra cumprimento do limite para Olá primeira vez em cerca de 5 minutos e ambos os mecanismos de atingido o limite de saudação aproximadamente 8 minutos.</span><span class="sxs-lookup"><span data-stu-id="6be8f-183">hello 160 RUL threshold is met for hello first time at around 5 minutes and both engines hit hello threshold at around 8 minutes.</span></span>

<span data-ttu-id="6be8f-184">simulação de saudação é executada por meio do conjunto de dados completo Olá para 148 ciclos e estabelece nos valores de regra e ciclo de final.</span><span class="sxs-lookup"><span data-stu-id="6be8f-184">hello simulation runs through hello complete dataset for 148 cycles and settles on final RUL and cycle values.</span></span>

<span data-ttu-id="6be8f-185">Você pode parar a simulação de saudação em qualquer ponto, mas clicar em **iniciar simulação** reproduções Olá simulação a partir do início de saudação do conjunto de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="6be8f-185">You can stop hello simulation at any point, but clicking **Start Simulation** replays hello simulation from hello start of hello dataset.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6be8f-186">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6be8f-186">Next steps</span></span>

<span data-ttu-id="6be8f-187">mais sobre como o Azure IoT permite cenários de manutenção preditiva, leitura de toolearn [capturar o valor da saudação Internet das coisas][lnk_capture_value].</span><span class="sxs-lookup"><span data-stu-id="6be8f-187">toolearn more about how Azure IoT enables predictive maintenance scenarios, read [Capture value from hello Internet of Things][lnk_capture_value].</span></span>

<span data-ttu-id="6be8f-188">Tirar uma [passo a passo] [ lnk-predictive-walkthrough] de solução de manutenção preditiva hello.</span><span class="sxs-lookup"><span data-stu-id="6be8f-188">Take a [walkthrough][lnk-predictive-walkthrough] of hello predictive maintenance solution.</span></span>

<span data-ttu-id="6be8f-189">Você também pode explorar alguns Olá outros recursos e capacidades de soluções do IoT Suite pré-configurado hello:</span><span class="sxs-lookup"><span data-stu-id="6be8f-189">You can also explore some of hello other features and capabilities of hello IoT Suite preconfigured solutions:</span></span>

* <span data-ttu-id="6be8f-190">[Perguntas frequentes sobre o IoT Suite][lnk-faq]</span><span class="sxs-lookup"><span data-stu-id="6be8f-190">[Frequently asked questions for IoT Suite][lnk-faq]</span></span>
* <span data-ttu-id="6be8f-191">[Segurança de IoT da saudação de plano de fundo para cima][lnk-security-groundup]</span><span class="sxs-lookup"><span data-stu-id="6be8f-191">[IoT security from hello ground up][lnk-security-groundup]</span></span>

[img-resource-group]: media/iot-suite-predictive-overview/resource-group.png
[img-simulation-stopped]: media/iot-suite-predictive-overview/simulation-stopped.png
[img-simulation-running]: media/iot-suite-predictive-overview/simulation-running.png
[img-simulation-warning]: media/iot-suite-predictive-overview/simulation-warning.png
[img-machine-learning]: media/iot-suite-predictive-overview/machine-learning.png

[lnk-powerbi]: https://www.github.com/Microsoft/PowerBI-visuals
[lnk-predictive-walkthrough]: iot-suite-predictive-walkthrough.md
[lnk_preconfigured_solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk_iot_suite]: iot-suite-overview.md
[lnk_infographic]: https://www.microsoft.com/server-cloud/predictivemaintenance/Index.html
[lnk_regression_model]: http://gallery.cortanaanalytics.com/Collection/Predictive-Maintenance-Template-3

[lnk_capture_value]: http://download.microsoft.com/download/0/7/D/07D394CE-185D-4B96-AC3C-9B61179F7080/Capture_value_from_the_Internet%20of%20Things_with_Predictive_Maintenance.PDF
[lnk-faq]: iot-suite-faq.md
[lnk-security-groundup]: securing-iot-ground-up.md
[lnk-azureiotsuite]: https://www.azureiotsuite.com/
[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-azureiotsuite]: https://www.azureiotsuite.com
[lnk-permissions]: iot-suite-permissions.md
[lnk-portal]: http://portal.azure.com/
[lnk-machine-learning]: https://azure.microsoft.com/services/machine-learning/