---
title: "Solução pré-configurada de manutenção preditiva | Microsoft Docs"
description: "Uma descrição da solução pré-configurada de manutenção preditiva do Azure IoT Suite."
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
ms.openlocfilehash: 8bad198488c4940a83eb32ec02122a91d47ca86c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="predictive-maintenance-preconfigured-solution-overview"></a><span data-ttu-id="a234c-103">Visão geral da solução pré-configurada de manutenção preditiva</span><span class="sxs-lookup"><span data-stu-id="a234c-103">Predictive maintenance preconfigured solution overview</span></span>

<span data-ttu-id="a234c-104">A [solução pré-configurada][lnk_preconfigured_solutions] de *manutenção preditiva* é uma das soluções pré-configuradas lançadas como parte do [Microsoft Azure IoT Suite][lnk_iot_suite].</span><span class="sxs-lookup"><span data-stu-id="a234c-104">The *predictive maintenance* [preconfigured solution][lnk_preconfigured_solutions] is one of the [Microsoft Azure IoT Suite][lnk_iot_suite] preconfigured solutions.</span></span> <span data-ttu-id="a234c-105">Essa solução integra a coleta de telemetria do dispositivo em tempo real com um modelo preditivo criado com o [Azure Machine Learning][lnk-machine-learning].</span><span class="sxs-lookup"><span data-stu-id="a234c-105">This solution integrates real-time device telemetry collection with a predictive model created using [Azure Machine Learning][lnk-machine-learning].</span></span>

<span data-ttu-id="a234c-106">Com o Azure IoT Suite, você pode se conectar e monitorar ativos de forma rápida e fácil, além de analisar a telemetria em tempo real em painéis e visualizações.</span><span class="sxs-lookup"><span data-stu-id="a234c-106">With Azure IoT Suite, you can quickly and easily connect to and monitor assets, and analyze telemetry in real time in dashboards and visualizations.</span></span> <span data-ttu-id="a234c-107">Na solução de manutenção preditiva, os paineis e visualizações fornecem uma nova inteligência que pode promover ganhos de eficiência e aumentar os fluxos de receita.</span><span class="sxs-lookup"><span data-stu-id="a234c-107">In the predictive maintenance solution, the dashboards and visualizations provide you with new intelligence that can drive efficiencies and enhance revenue streams.</span></span>

## <a name="the-scenario"></a><span data-ttu-id="a234c-108">O cenário</span><span class="sxs-lookup"><span data-stu-id="a234c-108">The Scenario</span></span>

<span data-ttu-id="a234c-109">A Fabrikam é uma companhia aérea regional que se dedica a fornecer uma excelente experiência ao cliente a preços competitivos.</span><span class="sxs-lookup"><span data-stu-id="a234c-109">Fabrikam is a regional airline that focuses on great customer experience at competitive prices.</span></span> <span data-ttu-id="a234c-110">Uma das causas de atrasos de voos são problemas de manutenção e a manutenção dos motores de aeronave representa um desafio singular.</span><span class="sxs-lookup"><span data-stu-id="a234c-110">One cause of flight delays is maintenance issues and aircraft engine maintenance is particularly challenging.</span></span> <span data-ttu-id="a234c-111">A Fabrikam precisa evitar a falha do motor durante o voo a todo custo e, portanto, ela inspeciona seus motores regularmente e agenda a manutenção de acordo com um plano.</span><span class="sxs-lookup"><span data-stu-id="a234c-111">Fabrikam must avoid engine failure during flight at all costs, so it inspects its engines regularly and schedules maintenance according to a plan.</span></span> <span data-ttu-id="a234c-112">No entanto, os motores de aeronave nem sempre se desgastam da mesma forma.</span><span class="sxs-lookup"><span data-stu-id="a234c-112">However, aircraft engines don’t always wear the same.</span></span> <span data-ttu-id="a234c-113">Algum tipo de manutenção desnecessária é realizada nos motores.</span><span class="sxs-lookup"><span data-stu-id="a234c-113">Some unnecessary maintenance is performed on engines.</span></span> <span data-ttu-id="a234c-114">O mais importante é que problemas ocorrem, o que pode fazer com que uma aeronave permaneça em solo até que a manutenção seja realizada.</span><span class="sxs-lookup"><span data-stu-id="a234c-114">More importantly, issues arise which can ground an aircraft until maintenance is performed.</span></span> <span data-ttu-id="a234c-115">Uma aeronave estar em um local onde os técnicos certos ou as peças de reposição certas não estão disponíveis pode custar muito caro.</span><span class="sxs-lookup"><span data-stu-id="a234c-115">If an aircraft is at a location where the right technicians or spare parts are not available, these issues can be especially costly.</span></span>

<span data-ttu-id="a234c-116">Os motores de aeronave da Fabrikam são instrumentados com sensores que monitoram as condições do motor durante o voo.</span><span class="sxs-lookup"><span data-stu-id="a234c-116">The engines of Fabrikam’s aircraft are instrumented with sensors that monitor engine conditions during flight.</span></span> <span data-ttu-id="a234c-117">A Fabrikam usa a solução de manutenção preditiva para coletar os dados de sensor coletados durante o voo.</span><span class="sxs-lookup"><span data-stu-id="a234c-117">Fabrikam uses the predictive maintenance solution to collect the sensor data collected during the flight.</span></span> <span data-ttu-id="a234c-118">Após vários anos acumulando dados operacionais e de falha do motor, os cientistas de dados da Fabrikam modelaram uma maneira para prever a RUL (Vida Útil Restante) de um motor de aeronave.</span><span class="sxs-lookup"><span data-stu-id="a234c-118">After accumulating years of engine operational and failure data, Fabrikam’s data scientists have modeled a way to predict the Remaining Useful Life (RUL) of an aircraft engine.</span></span> <span data-ttu-id="a234c-119">O modelo usa uma correlação entre os dados de quatro sensores do motor e o desgaste do motor que leva a uma eventual falha.</span><span class="sxs-lookup"><span data-stu-id="a234c-119">The model uses a correlation between data from four of the engine sensors and engine wear that leads to eventual failure.</span></span> <span data-ttu-id="a234c-120">Embora a Fabrikam continue realizando inspeções regulares para garantir a segurança, ela agora pode usar os modelos para calcular a RUL para cada motor após cada voo.</span><span class="sxs-lookup"><span data-stu-id="a234c-120">While Fabrikam continues to perform regular inspections to ensure safety, it can now use the models to compute the RUL for each engine after every flight.</span></span> <span data-ttu-id="a234c-121">O modelo usa a telemetria coletada de mecanismos de durante o voo.</span><span class="sxs-lookup"><span data-stu-id="a234c-121">The model uses the telemetry collected from the engines during the flight.</span></span> <span data-ttu-id="a234c-122">A Fabrikam agora pode prever os futuros pontos de falha e planejar a manutenção e reparar antecipadamente.</span><span class="sxs-lookup"><span data-stu-id="a234c-122">Fabrikam can now predict future points of failure and plan for maintenance and repair in advance.</span></span>

> [!NOTE]
> <span data-ttu-id="a234c-123">O modelo de solução usa dados reais de desgaste do mecanismo.</span><span class="sxs-lookup"><span data-stu-id="a234c-123">The solution model uses actual engine wear data.</span></span>

<span data-ttu-id="a234c-124">Ao prever o momento em que a manutenção é necessária, a Fabrikam pode otimizar suas operações para reduzir os custos.</span><span class="sxs-lookup"><span data-stu-id="a234c-124">By predicting the point when maintenance is required, Fabrikam can optimize its operations to reduce costs.</span></span>

<span data-ttu-id="a234c-125">Coordenadores de manutenção trabalham com os agendadores para:</span><span class="sxs-lookup"><span data-stu-id="a234c-125">Maintenance coordinators work with schedulers to:</span></span>

- <span data-ttu-id="a234c-126">Planeje a manutenção para coincidir com uma aeronave parar em um local específico.</span><span class="sxs-lookup"><span data-stu-id="a234c-126">Plan maintenance to coincide with an aircraft stopping at a particular location.</span></span>
- <span data-ttu-id="a234c-127">Faça com que haja tempo suficiente para a aeronave ficar fora de serviço sem causar interrupções de agendamento.</span><span class="sxs-lookup"><span data-stu-id="a234c-127">Ensure sufficient time is available for the aircraft to be out of service without causing schedule disruption.</span></span>
- <span data-ttu-id="a234c-128">Para agendar técnicos para garantir que aeronave é atendidas com eficiência sem tempo de espera.</span><span class="sxs-lookup"><span data-stu-id="a234c-128">To schedule technicians to ensure that aircraft are serviced efficiently without wait time.</span></span>

<span data-ttu-id="a234c-129">Os gerentes de controle de inventário recebem planos de manutenção, para que possam otimizar seu processo de encomendas e inventário de peças de reposição.</span><span class="sxs-lookup"><span data-stu-id="a234c-129">Inventory control managers receive maintenance plans, so they can optimize their ordering process and spare parts inventory.</span></span>

<span data-ttu-id="a234c-130">Essas atividades permitem que a Fabrikam minimize o tempo de solo de aeronave e reduza os custos operacionais, ao mesmo tempo que garante a segurança dos passageiros e da tripulação.</span><span class="sxs-lookup"><span data-stu-id="a234c-130">These activities enable Fabrikam to minimize aircraft ground time and reduce operating costs while ensuring the safety of passengers and crew.</span></span>

<span data-ttu-id="a234c-131">Para entender como o [Azure IoT Suite][lnk_iot_suite] fornece recursos que os clientes precisam para aproveitar o potencial da manutenção preditiva, examine este [infográfico][lnk_infographic].</span><span class="sxs-lookup"><span data-stu-id="a234c-131">To understand how [Azure IoT Suite][lnk_iot_suite] provides the capabilities customers need to realize the potential of predictive maintenance, review this [infographic][lnk_infographic].</span></span>

## <a name="how-the-predictive-maintenance-solution-is-built"></a><span data-ttu-id="a234c-132">Como a solução de manutenção preditiva é criada</span><span class="sxs-lookup"><span data-stu-id="a234c-132">How the predictive maintenance solution is built</span></span>

<span data-ttu-id="a234c-133">A solução usa um modelo do Azure Machine Learning existente como modelo para mostrar esses recursos trabalhando desde a telemetria de dispositivo coletada até os serviços IoT Suite.</span><span class="sxs-lookup"><span data-stu-id="a234c-133">The solution uses an existing Azure Machine Learning model available as a template to show these capabilities working from device telemetry collected through IoT Suite services.</span></span> <span data-ttu-id="a234c-134">A Microsoft criou um [modelo de regressão][lnk_regression_model] de um mecanismo de aeronave baseado em dados<sup>\[1\]</sup> disponíveis ao público e diretrizes passo a passo sobre como usar o modelo.</span><span class="sxs-lookup"><span data-stu-id="a234c-134">Microsoft has built a [regression model][lnk_regression_model] of an aircraft engine based on publically available data<sup>\[1\]</sup>, and step-by-step guidance on how to use the model.</span></span>

<span data-ttu-id="a234c-135">A solução de manutenção preditiva de IoT do Azure usa o modelo de regressão criado com base neste modelo.</span><span class="sxs-lookup"><span data-stu-id="a234c-135">The Azure IoT predictive maintenance solution uses the regression model created from this template.</span></span> <span data-ttu-id="a234c-136">O modelo é implantado em sua assinatura do Azure e exposto por meio de uma API gerada automaticamente.</span><span class="sxs-lookup"><span data-stu-id="a234c-136">The model is deployed into your Azure subscription and exposed through an automatically generated API.</span></span> <span data-ttu-id="a234c-137">A solução inclui um subconjunto dos dados de teste que representa 4 (do total de 100) 4 (de total de 21) e de mecanismos de fluxos de dados de sensor.</span><span class="sxs-lookup"><span data-stu-id="a234c-137">The solution includes a subset of the testing data representing 4 (of 100 total) engines and the 4 (of 21 total) sensor data streams.</span></span> <span data-ttu-id="a234c-138">Esses dados são suficientes para fornecer um resultado preciso do modelo treinado.</span><span class="sxs-lookup"><span data-stu-id="a234c-138">This data is sufficient to provide an accurate result from the trained model.</span></span>

<span data-ttu-id="a234c-139">*\[1\] A. Saxena e K. Goebel (2008). “Turbofan Engine Degradation Simulation Data Set” (Conjunto de dados da simulação de degradação do turbofan), Repositório de dados de prognóstico da NASA Ames (http://ti.arc.nasa.gov/tech/dash/pcoe/prognostic-data-repository/), NASA Ames Research Center, Moffett Field, CA*</span><span class="sxs-lookup"><span data-stu-id="a234c-139">*\[1\] A. Saxena and K. Goebel (2008). "Turbofan Engine Degradation Simulation Data Set", NASA Ames Prognostics Data Repository (http://ti.arc.nasa.gov/tech/dash/pcoe/prognostic-data-repository/), NASA Ames Research Center, Moffett Field, CA*</span></span>

## <a name="get-started-with-predictive-maintenance"></a><span data-ttu-id="a234c-140">Introdução à manutenção de previsão</span><span class="sxs-lookup"><span data-stu-id="a234c-140">Get started with predictive maintenance</span></span>

<span data-ttu-id="a234c-141">Este tutorial mostra como provisionar a solução de previsão de manutenção.</span><span class="sxs-lookup"><span data-stu-id="a234c-141">This tutorial shows you how to provision the predictive maintenance solution.</span></span> <span data-ttu-id="a234c-142">Ele também explica os recursos básicos da solução de previsão de manutenção.</span><span class="sxs-lookup"><span data-stu-id="a234c-142">It also walks you through the basic features of the predictive maintenance solution.</span></span> <span data-ttu-id="a234c-143">Você pode acessar muitos desses recursos por meio do painel de solução que é implantado junto com a solução pré-configurada.</span><span class="sxs-lookup"><span data-stu-id="a234c-143">You can access many of these features through the solution dashboard that deploys along with the preconfigured solution.</span></span>

<span data-ttu-id="a234c-144">Para concluir este tutorial, você precisa de uma assinatura ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="a234c-144">To complete this tutorial, you need an active Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="a234c-145">Se você não tiver uma conta, poderá criar uma conta de avaliação gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="a234c-145">If you don’t have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="a234c-146">Para obter detalhes, consulte [Avaliação gratuita do Azure][lnk_free_trial].</span><span class="sxs-lookup"><span data-stu-id="a234c-146">For details, see [Azure Free Trial][lnk_free_trial].</span></span>

1. <span data-ttu-id="a234c-147">Faça logon em [azureiotsuite.com][lnk-azureiotsuite] usando as credenciais de sua conta do Azure e clique em **+** para criar uma nova solução.</span><span class="sxs-lookup"><span data-stu-id="a234c-147">Log on to [azureiotsuite.com][lnk-azureiotsuite] using your Azure account credentials, and click **+** to create a solution.</span></span>
1. <span data-ttu-id="a234c-148">Clique em **selecione** o **manutenção previsão** lado a lado.</span><span class="sxs-lookup"><span data-stu-id="a234c-148">Click **Select** the **Predictive maintenance** tile.</span></span>
1. <span data-ttu-id="a234c-149">Insira um **nome da solução** sua manutenção previsão pré-configurados de solução.</span><span class="sxs-lookup"><span data-stu-id="a234c-149">Enter a **Solution name** for your predictive maintenance preconfigured solution.</span></span>
1. <span data-ttu-id="a234c-150">Selecione a **Região** e a **Assinatura** que você deseja usar para provisionar a solução.</span><span class="sxs-lookup"><span data-stu-id="a234c-150">Select the **Region** and **Subscription** you want to use to provision the solution.</span></span>
1. <span data-ttu-id="a234c-151">Clique em **Criar Solução** para iniciar o processo de provisionamento.</span><span class="sxs-lookup"><span data-stu-id="a234c-151">Click **Create Solution** to begin the provisioning process.</span></span> <span data-ttu-id="a234c-152">Este processo normalmente leva vários minutos para ser executado.</span><span class="sxs-lookup"><span data-stu-id="a234c-152">This process typically takes several minutes to run.</span></span>

### <a name="wait-for-the-provisioning-process-to-complete"></a><span data-ttu-id="a234c-153">Aguarde o processo de provisionamento ser concluído</span><span class="sxs-lookup"><span data-stu-id="a234c-153">Wait for the provisioning process to complete</span></span>

1. <span data-ttu-id="a234c-154">Clique no bloco da sua solução com o status **Provisionamento** .</span><span class="sxs-lookup"><span data-stu-id="a234c-154">Click the tile for your solution with **Provisioning** status.</span></span>
1. <span data-ttu-id="a234c-155">Observe os **estados de Provisionamento** à medida que os serviços do Azure são implantados em sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="a234c-155">Notice the **Provisioning states** as Azure services are deployed in your Azure subscription.</span></span>
1. <span data-ttu-id="a234c-156">Após o provisionamento ser concluído, o status será alterado para **Pronto**.</span><span class="sxs-lookup"><span data-stu-id="a234c-156">Once provisioning completes, the status changes to **Ready**.</span></span>
1. <span data-ttu-id="a234c-157">Clique no bloco para ver os detalhes da solução no painel à direita.</span><span class="sxs-lookup"><span data-stu-id="a234c-157">Click the tile to see the details of your solution in the right-hand pane.</span></span> <span data-ttu-id="a234c-158">Nesse painel, você pode iniciar o painel de solução e acessar o espaço de trabalho do Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="a234c-158">From this pane, you can launch the solution dashboard and access the Machine Learning workspace.</span></span>

> [!NOTE]
> <span data-ttu-id="a234c-159">Se estiver tendo problemas para implantar a solução pré-configurada, dê uma olhada em [Permissões no site azureiotsuite.com][lnk-permissions] e nas [Perguntas frequentes][lnk-faq].</span><span class="sxs-lookup"><span data-stu-id="a234c-159">If you encounter issues deploying the preconfigured solution, review [Permissions on the azureiotsuite.com site][lnk-permissions] and the [FAQ][lnk-faq].</span></span> <span data-ttu-id="a234c-160">Se os problemas persistirem, crie um tíquete de serviço no [portal][lnk-portal].</span><span class="sxs-lookup"><span data-stu-id="a234c-160">If the issues persist, create a service ticket on the [portal][lnk-portal].</span></span>

<span data-ttu-id="a234c-161">Há detalhes que você esperaria ver e que não estão listados para sua solução?</span><span class="sxs-lookup"><span data-stu-id="a234c-161">Are there details you'd expect to see that aren't listed for your solution?</span></span> <span data-ttu-id="a234c-162">Envie sugestões de recursos no [User Voice](https://feedback.azure.com/forums/321918-azure-iot).</span><span class="sxs-lookup"><span data-stu-id="a234c-162">Give us feature suggestions on [User Voice](https://feedback.azure.com/forums/321918-azure-iot).</span></span>

## <a name="view-the-solution"></a><span data-ttu-id="a234c-163">Exibir a solução</span><span class="sxs-lookup"><span data-stu-id="a234c-163">View the solution</span></span>

<span data-ttu-id="a234c-164">Esta seção o orienta a solução da interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="a234c-164">This section guides you through the solution UI.</span></span>

### <a name="predictive-maintenance-dashboard"></a><span data-ttu-id="a234c-165">Painel Manutenção Preditiva</span><span class="sxs-lookup"><span data-stu-id="a234c-165">Predictive Maintenance Dashboard</span></span>

<span data-ttu-id="a234c-166">Esta página no aplicativo Web usa controles JavaScript do PowerBI (confira o [repositório de elementos visuais do PowerBI][lnk-powerbi]) para visualizar:</span><span class="sxs-lookup"><span data-stu-id="a234c-166">This page in the web application uses PowerBI JavaScript controls (see the [PowerBI-visuals repository][lnk-powerbi]) to visualize:</span></span>

* <span data-ttu-id="a234c-167">Os dados de saída de trabalhos do Stream Analytics no armazenamento de blobs.</span><span class="sxs-lookup"><span data-stu-id="a234c-167">The output data from the Stream Analytics jobs in blob storage.</span></span>
* <span data-ttu-id="a234c-168">O RUL e a contagem de ciclo por motor da aeronave.</span><span class="sxs-lookup"><span data-stu-id="a234c-168">The RUL and cycle count per aircraft engine.</span></span>

### <a name="observing-the-behavior-of-the-cloud-solution"></a><span data-ttu-id="a234c-169">Observando o comportamento da solução de nuvem</span><span class="sxs-lookup"><span data-stu-id="a234c-169">Observing the behavior of the cloud solution</span></span>

<span data-ttu-id="a234c-170">No portal do Azure, navegue até o grupo de recursos com o nome da solução escolhido para exibir os recursos provisionados.</span><span class="sxs-lookup"><span data-stu-id="a234c-170">In the Azure portal, navigate to the resource group with the solution name you chose to view your provisioned resources.</span></span>

![][img-resource-group]

<span data-ttu-id="a234c-171">Quando você provisiona a solução pré-configurada, recebe um email com um link para o espaço de trabalho do Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="a234c-171">When you provision the preconfigured solution, you receive an email with a link to the Machine Learning workspace.</span></span> <span data-ttu-id="a234c-172">Você também pode navegar até o Espaço de Trabalho do Machine Learning na página [azureiotsuite.com][lnk-azureiotsuite] para sua solução provisionada.</span><span class="sxs-lookup"><span data-stu-id="a234c-172">You can also navigate to the Machine Learning workspace from the [azureiotsuite.com][lnk-azureiotsuite] page for your provisioned solution.</span></span> <span data-ttu-id="a234c-173">Um bloco fica disponível nessa página quando a solução entra no estado **pronto**.</span><span class="sxs-lookup"><span data-stu-id="a234c-173">A tile is available on this page when the solution is in the **Ready** state.</span></span>

![][img-machine-learning]

<span data-ttu-id="a234c-174">No portal da solução, você pode ver que o exemplo é provisionado com quatro dispositivos simulados para representar duas aeronaves com dois motores por aeronave, cada um com quatro sensores.</span><span class="sxs-lookup"><span data-stu-id="a234c-174">In the solution portal, you can see that the sample is provisioned with four simulated devices to represent two aircraft with two engines per aircraft, each with four sensors.</span></span> <span data-ttu-id="a234c-175">Quando você navega pela primeira vez até o portal de solução, a simulação é interrompida.</span><span class="sxs-lookup"><span data-stu-id="a234c-175">When you first navigate to the solution portal, the simulation is stopped.</span></span>

![][img-simulation-stopped]

<span data-ttu-id="a234c-176">Clique em **Iniciar simulação** para iniciar a simulação.</span><span class="sxs-lookup"><span data-stu-id="a234c-176">Click **Start simulation** to begin the simulation.</span></span> <span data-ttu-id="a234c-177">O histórico de sensor, RUL, ciclos e histórico de RUL preenchem o painel.</span><span class="sxs-lookup"><span data-stu-id="a234c-177">The sensor history, RUL, Cycles, and RUL history populate the dashboard.</span></span>

![][img-simulation-running]

<span data-ttu-id="a234c-178">Quando a RUL for menor que 160 (um limite aleatório escolhido para fins de demonstração), o portal da solução exibirá um símbolo de aviso ao lado da exibição da RUL.</span><span class="sxs-lookup"><span data-stu-id="a234c-178">When RUL is less than 160 (an arbitrary threshold chosen for demonstration purposes), the solution portal displays a warning symbol next to the RUL display.</span></span> <span data-ttu-id="a234c-179">O portal da solução também destaca o motor de aeronave em amarelo.</span><span class="sxs-lookup"><span data-stu-id="a234c-179">The solution portal also highlights the aircraft engine in yellow.</span></span> <span data-ttu-id="a234c-180">Observe que os valores da RUL têm uma tendência descendente geral, mas tendem a subir e a descer.</span><span class="sxs-lookup"><span data-stu-id="a234c-180">Notice how the RUL values have a general downward trend overall, but tend to bounce up and down.</span></span> <span data-ttu-id="a234c-181">Este comportamento é resultado de durações variáveis do ciclo e da precisão do modelo.</span><span class="sxs-lookup"><span data-stu-id="a234c-181">This behavior results from the varying cycle lengths and the model accuracy.</span></span>

![][img-simulation-warning]

<span data-ttu-id="a234c-182">A simulação completa leva cerca de 35 minutos para concluir 148 ciclos.</span><span class="sxs-lookup"><span data-stu-id="a234c-182">The full simulation takes around 35 minutes to complete 148 cycles.</span></span> <span data-ttu-id="a234c-183">O limite de 160 do RUL é atingido pela primeira vez aproximadamente aos cinco minutos, e os dois motores atingem o limite aproximadamente aos oito minutos.</span><span class="sxs-lookup"><span data-stu-id="a234c-183">The 160 RUL threshold is met for the first time at around 5 minutes and both engines hit the threshold at around 8 minutes.</span></span>

<span data-ttu-id="a234c-184">A simulação percorre todo o conjunto de dados dos 148 ciclos e estabelece nos valores finais de RUL e de ciclo.</span><span class="sxs-lookup"><span data-stu-id="a234c-184">The simulation runs through the complete dataset for 148 cycles and settles on final RUL and cycle values.</span></span>

<span data-ttu-id="a234c-185">Você pode parar a simulação a qualquer momento, mas clicar em **Iniciar Simulação** repetirá a simulação desde o início do conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="a234c-185">You can stop the simulation at any point, but clicking **Start Simulation** replays the simulation from the start of the dataset.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a234c-186">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a234c-186">Next steps</span></span>

<span data-ttu-id="a234c-187">Para saber mais sobre como o Azure IoT habilita cenários de manutenção preditiva, leia [Capturar o valor da Internet das Coisas][lnk_capture_value].</span><span class="sxs-lookup"><span data-stu-id="a234c-187">To learn more about how Azure IoT enables predictive maintenance scenarios, read [Capture value from the Internet of Things][lnk_capture_value].</span></span>

<span data-ttu-id="a234c-188">Faça um [passo a passo][lnk-predictive-walkthrough] da solução de manutenção preditiva.</span><span class="sxs-lookup"><span data-stu-id="a234c-188">Take a [walkthrough][lnk-predictive-walkthrough] of the predictive maintenance solution.</span></span>

<span data-ttu-id="a234c-189">Você também pode explorar alguns dos outros recursos das soluções pré-configuradas do IoT Suite:</span><span class="sxs-lookup"><span data-stu-id="a234c-189">You can also explore some of the other features and capabilities of the IoT Suite preconfigured solutions:</span></span>

* <span data-ttu-id="a234c-190">[Perguntas frequentes sobre o IoT Suite][lnk-faq]</span><span class="sxs-lookup"><span data-stu-id="a234c-190">[Frequently asked questions for IoT Suite][lnk-faq]</span></span>
* <span data-ttu-id="a234c-191">[Segurança IoT desde o início][lnk-security-groundup]</span><span class="sxs-lookup"><span data-stu-id="a234c-191">[IoT security from the ground up][lnk-security-groundup]</span></span>

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