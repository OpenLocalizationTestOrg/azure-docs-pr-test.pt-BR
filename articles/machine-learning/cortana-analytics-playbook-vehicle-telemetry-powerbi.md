---
title: "aaaPower painel BI para integridade de veículo e orientar hábitos - Azure | Microsoft Docs"
description: "Usar recursos de saudação do insights de previsão e em tempo real de inteligência Cortana toogain na integridade do veículo e orientar hábitos."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: aaeb29a5-4a13-4eab-bbf1-885690d86c56
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/16/2016
ms.author: bradsev
ms.openlocfilehash: 0bd054d943387ecad7301236eebae22458173aba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="vehicle-telemetry-analytics-solution-template-power-bi-dashboard-setup-instructions"></a><span data-ttu-id="c29e5-103">Instruções de instalação do Painel de Power BI do modelo de solução de análise de telemetria do veículo</span><span class="sxs-lookup"><span data-stu-id="c29e5-103">Vehicle telemetry analytics solution template Power BI Dashboard setup instructions</span></span>
<span data-ttu-id="c29e5-104">Isso **menu** toohello capítulos neste guia estratégico de links.</span><span class="sxs-lookup"><span data-stu-id="c29e5-104">This **menu** links toohello chapters in this playbook.</span></span> 

[!INCLUDE [cap-vehicle-telemetry-playbook-selector](../../includes/cap-vehicle-telemetry-playbook-selector.md)]

<span data-ttu-id="c29e5-105">Olá solução de análise de telemetria do veículo demonstra como revendedores de carro, automóveis fabricantes e companhias podem aproveitar os recursos de saudação do Cortana Intelligence toogain em tempo real e previsão visões e integridade de veículo e orientar melhorias de toodrive hábitos na área de saudação do cliente experiência, R & D e campanhas de marketing.</span><span class="sxs-lookup"><span data-stu-id="c29e5-105">hello Vehicle Telemetry Analytics solution showcases how car dealerships, automobile manufacturers and insurance companies can leverage hello capabilities of Cortana Intelligence toogain real-time and predictive insights on vehicle health and driving habits toodrive improvements in hello area of customer experience, R&D and marketing campaigns.</span></span> <span data-ttu-id="c29e5-106">Este documento contém instruções passo a passo de como você pode configurar relatórios do Power BI hello e painel depois Olá solução é implantada em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="c29e5-106">This document contains step by step instructions on how you can configure hello Power BI reports and dashboard once hello solution is deployed in your subscription.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="c29e5-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="c29e5-107">Prerequisites</span></span>
1. <span data-ttu-id="c29e5-108">Implantar Olá [telemetria análise](https://gallery.cortanaintelligence.com/Solution/5bdb23f3abb448268b7402ab8907cc90) solução</span><span class="sxs-lookup"><span data-stu-id="c29e5-108">Deploy hello [Telemetry Analytics](https://gallery.cortanaintelligence.com/Solution/5bdb23f3abb448268b7402ab8907cc90) solution</span></span>  
2. [<span data-ttu-id="c29e5-109">Instalar o Microsoft Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="c29e5-109">Install Microsoft Power BI Desktop</span></span>](http://www.microsoft.com/download/details.aspx?id=45331)
3. <span data-ttu-id="c29e5-110">Uma [assinatura do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c29e5-110">An [Azure subscription](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="c29e5-111">Se você não tiver uma assinatura do Azure, comece com uma assinatura gratuita do Azure</span><span class="sxs-lookup"><span data-stu-id="c29e5-111">If you don't have an Azure subscription, get started with Azure free subscription</span></span>
4. <span data-ttu-id="c29e5-112">Conta do Microsoft Power BI</span><span class="sxs-lookup"><span data-stu-id="c29e5-112">Microsoft Power BI account</span></span>

## <a name="cortana-intelligence-suite-components"></a><span data-ttu-id="c29e5-113">Componentes do Cortana Intelligence Suite</span><span class="sxs-lookup"><span data-stu-id="c29e5-113">Cortana Intelligence Suite Components</span></span>
<span data-ttu-id="c29e5-114">Como parte do modelo de solução de análise de telemetria do veículo hello, Olá serviços Cortana Intelligence a seguir é implantado na sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="c29e5-114">As part of hello Vehicle Telemetry Analytics solution template, hello following Cortana Intelligence services are deployed in your subscription.</span></span>

* <span data-ttu-id="c29e5-115">**Hubs de Eventos** para ingerir milhões de eventos de telemetria do veículos no Azure.</span><span class="sxs-lookup"><span data-stu-id="c29e5-115">**Event Hub** for ingesting millions of vehicle telemetry events into Azure.</span></span>
* <span data-ttu-id="c29e5-116">**Stream Analytics** para obter informações em tempo real sobre a integridade do veículo e persistir esses dados no armazenamento de longo prazo para uma análise de lote mais avançada.</span><span class="sxs-lookup"><span data-stu-id="c29e5-116">**Stream Analytics** for gaining real-time insights on vehicle health and persists that data into long-term storage for richer batch analytics.</span></span>
* <span data-ttu-id="c29e5-117">**Aprendizado de máquina** para detecção de anomalias em tempo real e insights previsão toogain de processamento em lotes.</span><span class="sxs-lookup"><span data-stu-id="c29e5-117">**Machine Learning** for anomaly detection in real-time and batch processing toogain predictive insights.</span></span>
* <span data-ttu-id="c29e5-118">**HDInsight** tootransform utilizou dados em grande escala</span><span class="sxs-lookup"><span data-stu-id="c29e5-118">**HDInsight** is leveraged tootransform data at scale</span></span>
* <span data-ttu-id="c29e5-119">**Fábrica de dados** manipula orquestração, agendamento, gerenciamento de recursos e o monitoramento do pipeline de processamento de lote hello.</span><span class="sxs-lookup"><span data-stu-id="c29e5-119">**Data Factory** handles orchestration, scheduling, resource management and monitoring of hello batch processing pipeline.</span></span>

<span data-ttu-id="c29e5-120">**PowerBI** fornece essa solução a um painel avançado para os dados em tempo real e as visualizações da análise preditiva.</span><span class="sxs-lookup"><span data-stu-id="c29e5-120">**Power BI** gives this solution a rich dashboard for real-time data and predictive analytics visualizations.</span></span> 

<span data-ttu-id="c29e5-121">solução de saudação usa duas fontes de dados diferentes: **simulados veículo sinais e o conjunto de dados de diagnóstico** e **catálogo veículo**.</span><span class="sxs-lookup"><span data-stu-id="c29e5-121">hello solution uses two different data sources: **Simulated vehicle signals and diagnostic dataset** and **vehicle catalog**.</span></span>

<span data-ttu-id="c29e5-122">Um simulador de telemática do veículo é incluído como parte desta solução.</span><span class="sxs-lookup"><span data-stu-id="c29e5-122">A vehicle telematics simulator is included as part of this solution.</span></span> <span data-ttu-id="c29e5-123">Ele emite informações de diagnóstico e sinaliza o estado toohello correspondente de veículo hello e um padrão em um determinado ponto no tempo.</span><span class="sxs-lookup"><span data-stu-id="c29e5-123">It emits diagnostic information and signals corresponding toohello state of hello vehicle and driving pattern at a given point in time.</span></span> 

<span data-ttu-id="c29e5-124">Olá veículo catálogo é um mapeamento de toomodel Referência dataset contendo VIN</span><span class="sxs-lookup"><span data-stu-id="c29e5-124">hello Vehicle Catalog is a reference dataset containing VIN toomodel mapping</span></span>

## <a name="power-bi-dashboard-preparation"></a><span data-ttu-id="c29e5-125">Preparação do Painel do Power BI</span><span class="sxs-lookup"><span data-stu-id="c29e5-125">Power BI Dashboard Preparation</span></span>
### <a name="setup-power-bi-real-time-dashboard"></a><span data-ttu-id="c29e5-126">Instalação do Painel do Power BI em tempo real</span><span class="sxs-lookup"><span data-stu-id="c29e5-126">Setup Power BI Real-Time Dashboard</span></span>

<span data-ttu-id="c29e5-127">**Iniciar o aplicativo de painel em tempo real de hello** concluída a implantação hello, você deve seguir instruções de operação Olá Manual</span><span class="sxs-lookup"><span data-stu-id="c29e5-127">**Start hello real-time dashboard application** Once hello deployment is completed, you should follow hello Manual Operation Instructions</span></span>

* <span data-ttu-id="c29e5-128">Baixe o aplicativo de painel em tempo real RealtimeDashboardApp.zip e descompacte-o.</span><span class="sxs-lookup"><span data-stu-id="c29e5-128">Download real-time dashboard application RealtimeDashboardApp.zip, and unzip it.</span></span>
*  <span data-ttu-id="c29e5-129">Na pasta de descompactado hello, abra o arquivo de configuração do aplicativo 'RealtimeDashboardApp.exe.config' appSettings de substituição para Eventhub, armazenamento de Blob e ML conexões de serviço com valores hello no hello Manual de instruções de operação e salvar suas alterações.</span><span class="sxs-lookup"><span data-stu-id="c29e5-129">In hello unzipped folder, open app config file 'RealtimeDashboardApp.exe.config', replace appSettings for Eventhub, Blob Storage, and ML service connections with hello values in hello Manual Operation Instructions, and save your changes.</span></span>
* <span data-ttu-id="c29e5-130">Execute o aplicativo RealtimeDashboardApp.exe.</span><span class="sxs-lookup"><span data-stu-id="c29e5-130">Run application RealtimeDashboardApp.exe.</span></span> <span data-ttu-id="c29e5-131">Uma janela de logon será pop-up, forneça suas credenciais do Power BI válidas e clique em Olá **aceitar** botão.</span><span class="sxs-lookup"><span data-stu-id="c29e5-131">A login window will pop up, provide your valid PowerBI credentials and click hello **Accept** button.</span></span> <span data-ttu-id="c29e5-132">Em seguida, o aplicativo hello iniciará toorun.</span><span class="sxs-lookup"><span data-stu-id="c29e5-132">Then hello app will start toorun.</span></span>

   ![Entrar tooPower BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/5-sign-into-powerbi.png)
   
   ![Permissões do Painel do Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/6-powerbi-dashboard-permissions.png)

* <span data-ttu-id="c29e5-135">Site de tooPowerBI de logon e criar um painel em tempo real.</span><span class="sxs-lookup"><span data-stu-id="c29e5-135">Login tooPowerBI website, and create real-time dashboard.</span></span>

<span data-ttu-id="c29e5-136">Agora, você painel do Power BI Olá tooconfigure pronto com visualizações avançadas toogain em tempo real e hábitos de previsão ideias sobre a integridade de veículo e referências.</span><span class="sxs-lookup"><span data-stu-id="c29e5-136">Now, you are ready tooconfigure hello Power BI dashboard with rich visualizations toogain real-time and predictive insights on vehicle health and driving habits.</span></span> <span data-ttu-id="c29e5-137">Leva aproximadamente 45 minutos tooan horas toocreate hello todos os relatórios e configurar Olá painel.</span><span class="sxs-lookup"><span data-stu-id="c29e5-137">It takes about 45 minutes tooan hour toocreate all hello reports and configure hello dashboard.</span></span> 

### <a name="configure-power-bi-reports"></a><span data-ttu-id="c29e5-138">Configurar relatórios do Power BI</span><span class="sxs-lookup"><span data-stu-id="c29e5-138">Configure Power BI reports</span></span>
<span data-ttu-id="c29e5-139">relatórios em tempo real Hello e painel Olá levar cerca de 30 a 45 minutos toocomplete.</span><span class="sxs-lookup"><span data-stu-id="c29e5-139">hello real-time reports and hello dashboard take about 30-45 minutes toocomplete.</span></span> <span data-ttu-id="c29e5-140">Procurar muito[http://powerbi.com](http://powerbi.com) e logon.</span><span class="sxs-lookup"><span data-stu-id="c29e5-140">Browse too[http://powerbi.com](http://powerbi.com) and login.</span></span>

![Entrar tooPower BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/6-1-powerbi-signin.png)

<span data-ttu-id="c29e5-142">Um novo conjunto de dados é gerado no Power BI.</span><span class="sxs-lookup"><span data-stu-id="c29e5-142">A new dataset is generated in Power BI.</span></span> <span data-ttu-id="c29e5-143">Clique em Olá **ConnectedCarsRealtime** conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="c29e5-143">Click hello **ConnectedCarsRealtime** dataset.</span></span>

![Selecionar conjunto de dados de carros conectados em tempo real](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/7-select-connected-cars-realtime-dataset.png)

<span data-ttu-id="c29e5-145">Salvar a saudação de relatório em branco usando **Ctrl + s**.</span><span class="sxs-lookup"><span data-stu-id="c29e5-145">Save hello blank report using **Ctrl + s**.</span></span>

![Salvar relatório em branco](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/8-save-blank-report.png)

<span data-ttu-id="c29e5-147">Forneça o nome de relatório *Análise em tempo real de telemetria do veículo - Relatórios*.</span><span class="sxs-lookup"><span data-stu-id="c29e5-147">Provide report name *Vehicle Telemetry Analytics Real-time - Reports*.</span></span>

![Forneça o nome do relatório](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/9-provide-report-name.png)

## <a name="real-time-reports"></a><span data-ttu-id="c29e5-149">Relatórios em tempo real</span><span class="sxs-lookup"><span data-stu-id="c29e5-149">Real-time reports</span></span>
<span data-ttu-id="c29e5-150">Há três relatórios em tempo real nesta solução:</span><span class="sxs-lookup"><span data-stu-id="c29e5-150">There are three real-time reports in this solution:</span></span>

1. <span data-ttu-id="c29e5-151">Veículos em operação</span><span class="sxs-lookup"><span data-stu-id="c29e5-151">Vehicles in operation</span></span>
2. <span data-ttu-id="c29e5-152">Veículos que precisam de manutenção</span><span class="sxs-lookup"><span data-stu-id="c29e5-152">Vehicles Requiring Maintenance</span></span>
3. <span data-ttu-id="c29e5-153">Estatísticas de integridade de veículos</span><span class="sxs-lookup"><span data-stu-id="c29e5-153">Vehicles Health Statistics</span></span>

<span data-ttu-id="c29e5-154">Você pode escolher tooconfigure todos os relatórios em tempo real de três de saudação ou parar depois de qualquer estágio e continuar toohello próxima seção de configuração relatórios de lote de saudação.</span><span class="sxs-lookup"><span data-stu-id="c29e5-154">You can choose tooconfigure all hello three real-time reports or stop after any stage and proceed toohello next section of configuring hello batch reports.</span></span> <span data-ttu-id="c29e5-155">Recomendamos que você toocreate todos os Olá três relatórios insights completo do toovisualize saudação do caminho de saudação em tempo real de solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="c29e5-155">We recommend you toocreate all hello three reports toovisualize hello full insights of hello real-time path of hello solution.</span></span>  

### <a name="1-vehicles-in-operation"></a><span data-ttu-id="c29e5-156">1. Veículos em operação</span><span class="sxs-lookup"><span data-stu-id="c29e5-156">1. Vehicles in operation</span></span>
<span data-ttu-id="c29e5-157">Clique duas vezes em **página 1** e renomeá-lo muito "Veículos na operação"</span><span class="sxs-lookup"><span data-stu-id="c29e5-157">Double-click **Page 1** and rename it too“Vehicles in operation”</span></span>  
    <span data-ttu-id="c29e5-158">![Carros conectados - Veículos em operação](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4a.png)</span><span class="sxs-lookup"><span data-stu-id="c29e5-158">![Connected Cars - Vehicles in operation](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4a.png)</span></span>  

<span data-ttu-id="c29e5-159">Selecione o campo **vin** em **Campos** e escolha o tipo de visualização como **"Placa"**.</span><span class="sxs-lookup"><span data-stu-id="c29e5-159">Select **vin** field from **Fields** and choose visualization type as **“Card”**.</span></span>  

<span data-ttu-id="c29e5-160">A visualização de placa é criada como mostrado na figura.</span><span class="sxs-lookup"><span data-stu-id="c29e5-160">Card visualization is created as shown in figure.</span></span>  
    ![Carros conectados - Selecione vin](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4b.png)

<span data-ttu-id="c29e5-162">Clique em nova visualização do hello área em branco tooadd.</span><span class="sxs-lookup"><span data-stu-id="c29e5-162">Click hello blank area tooadd new visualization.</span></span>  

<span data-ttu-id="c29e5-163">Selecione **Cidade** e **vin** nos campos.</span><span class="sxs-lookup"><span data-stu-id="c29e5-163">Select **City** and **vin** from fields.</span></span> <span data-ttu-id="c29e5-164">Alterar a visualização muito**"Mapa"**.</span><span class="sxs-lookup"><span data-stu-id="c29e5-164">Change visualization too**“Map”**.</span></span> <span data-ttu-id="c29e5-165">Arraste o **vin** na área de valores.</span><span class="sxs-lookup"><span data-stu-id="c29e5-165">Drag **vin** in values area.</span></span> <span data-ttu-id="c29e5-166">Arraste **city** de campos muito**legenda** área.</span><span class="sxs-lookup"><span data-stu-id="c29e5-166">Drag **city** from fields too**Legend** area.</span></span>   
    <span data-ttu-id="c29e5-167">![Carros conectados - Visualização da placa](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4c.png)</span><span class="sxs-lookup"><span data-stu-id="c29e5-167">![Connected Cars - Card Visualization](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4c.png)</span></span>

<span data-ttu-id="c29e5-168">Selecione **formato** seção de **visualizações**, clique em **título** e alterar Olá **texto** muito**"veículos em operação por cidade"**.</span><span class="sxs-lookup"><span data-stu-id="c29e5-168">Select **format** section from **Visualizations**, click **Title** and change hello **Text** too**“Vehicles in operation by city”**.</span></span>  
    <span data-ttu-id="c29e5-169">![Carros conectados - Veículos em operação por cidade](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4d.png)</span><span class="sxs-lookup"><span data-stu-id="c29e5-169">![Connected Cars - Vehicles in operation by city](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4d.png)</span></span>   

<span data-ttu-id="c29e5-170">A visualização final será como mostrado na figura.</span><span class="sxs-lookup"><span data-stu-id="c29e5-170">Final visualization looks as shown in figure.</span></span>    
    ![Carros conectados - Visualização final](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4e.png)

<span data-ttu-id="c29e5-172">Clique em nova visualização do hello área em branco tooadd.</span><span class="sxs-lookup"><span data-stu-id="c29e5-172">Click hello blank area tooadd new visualization.</span></span>  

<span data-ttu-id="c29e5-173">Selecione **City** e **vin**, altere o tipo de visualização muito**gráfico de coluna clusterizado**.</span><span class="sxs-lookup"><span data-stu-id="c29e5-173">Select **City** and **vin**, change visualization type too**Clustered Column Chart**.</span></span> <span data-ttu-id="c29e5-174">Certifique-se de que o campo **Cidade** está na **Área do eixo** e o **vin** está na **Área do valor**</span><span class="sxs-lookup"><span data-stu-id="c29e5-174">Ensure **City** field in **Axis area** and **vin** in **Value area**</span></span>  

<span data-ttu-id="c29e5-175">Classificar gráfico por **"Contagem de vin"**</span><span class="sxs-lookup"><span data-stu-id="c29e5-175">Sort chart by **“Count of vin”**</span></span>  
    <span data-ttu-id="c29e5-176">![Carros conectados - Contagem de vin](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4f.png)</span><span class="sxs-lookup"><span data-stu-id="c29e5-176">![Connected Cars - Count of vin](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4f.png)</span></span>  

<span data-ttu-id="c29e5-177">Gráfico de alteração **título** muito**"Veículos em operação por cidade"**</span><span class="sxs-lookup"><span data-stu-id="c29e5-177">Change chart **Title** too**“Vehicles in operation by city”**</span></span>  

<span data-ttu-id="c29e5-178">Clique Olá **formato** seção e, em seguida, selecione **cores de dados**, clique em Olá **"Em"** muito**Mostrar tudo**</span><span class="sxs-lookup"><span data-stu-id="c29e5-178">Click hello **Format** section, then select **Data Colors**,  Click hello **“On”** too**Show All**</span></span>  
    <span data-ttu-id="c29e5-179">![Carros conectados - Mostrar todas as cores de dados](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4g.png)</span><span class="sxs-lookup"><span data-stu-id="c29e5-179">![Connected Cars - Show all Data Colors](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4g.png)</span></span>  

<span data-ttu-id="c29e5-180">Alterar a cor de saudação de cidade individual, clicando no ícone de cor.</span><span class="sxs-lookup"><span data-stu-id="c29e5-180">Change hello color of individual city by clicking on color icon.</span></span>  
    ![Carros conectados - Alterar cores](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4h.png)  

<span data-ttu-id="c29e5-182">Clique em nova visualização do hello área em branco tooadd.</span><span class="sxs-lookup"><span data-stu-id="c29e5-182">Click hello blank area tooadd new visualization.</span></span>  

<span data-ttu-id="c29e5-183">Selecione a visualização **Gráfico de Coluna Clusterizada** nas visualizações, arraste o campo **cidade** para a área do **Eixo**, **Modelo** para a área de **Legenda** e **vin** para a área **Valor**.</span><span class="sxs-lookup"><span data-stu-id="c29e5-183">Select **Clustered Column Chart** visualization from visualizations, drag **city** field in **Axis** area, **Model** in **Legend** area and **vin** in **Value** area.</span></span>  
    <span data-ttu-id="c29e5-184">![Carros conectados - Gráfico de colunas agrupadas](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4i.png)</span><span class="sxs-lookup"><span data-stu-id="c29e5-184">![Connected Cars - Clustered Column Chart](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4i.png)</span></span>  
    <span data-ttu-id="c29e5-185">![Carros conectados - Renderização](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4j.png)</span><span class="sxs-lookup"><span data-stu-id="c29e5-185">![Connected Cars - Rendering](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4j.png)</span></span>

<span data-ttu-id="c29e5-186">Reorganize todas as visualizações nesta página conforme mostrado na figura.</span><span class="sxs-lookup"><span data-stu-id="c29e5-186">Rearrange all visualization on this page as shown in figure.</span></span>  
    ![Carros conectados - Visualizações](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4k.png)

<span data-ttu-id="c29e5-188">Você configurou com êxito o relatório em tempo real do hello "Veículos na operação".</span><span class="sxs-lookup"><span data-stu-id="c29e5-188">You have successfully configured hello “Vehicles in operation” real-time report.</span></span> <span data-ttu-id="c29e5-189">Você pode continuar relatório em tempo real do toocreate Olá Avançar ou parar aqui e configurar Olá painel.</span><span class="sxs-lookup"><span data-stu-id="c29e5-189">You can proceed toocreate hello next real-time report or stop here and configure hello dashboard.</span></span> 

### <a name="2-vehicles-requiring-maintenance"></a><span data-ttu-id="c29e5-190">2. Veículos que precisam de manutenção</span><span class="sxs-lookup"><span data-stu-id="c29e5-190">2. Vehicles Requiring Maintenance</span></span>
<span data-ttu-id="c29e5-191">Clique em ![adicionar](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) tooadd um novo relatório, renomeá-lo muito**"Veículos necessidade de manutenção"**</span><span class="sxs-lookup"><span data-stu-id="c29e5-191">Click ![Add](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) tooadd a new report, rename it too**“Vehicles Requiring Maintenance”**</span></span>

![Carros conectados - Veículos que precisam de manutenção](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4l.png)  

<span data-ttu-id="c29e5-193">Selecione **vin** campo e altere o tipo de visualização muito**cartão**.</span><span class="sxs-lookup"><span data-stu-id="c29e5-193">Select **vin** field and change visualization type too**Card**.</span></span>  
    <span data-ttu-id="c29e5-194">![Carros conectados - Visualização da placa do vin](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4m.png)</span><span class="sxs-lookup"><span data-stu-id="c29e5-194">![Connected Cars - Vin Card Visualization](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4m.png)</span></span>  

<span data-ttu-id="c29e5-195">Temos um campo chamado "MaintenanceLabel" no conjunto de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="c29e5-195">We have a field named “MaintenanceLabel” In hello dataset.</span></span> <span data-ttu-id="c29e5-196">Esse campo pode ter um valor “0” ou “1”.</span><span class="sxs-lookup"><span data-stu-id="c29e5-196">This field can have a value of “0” or “1”.”</span></span> <span data-ttu-id="c29e5-197">Ele é definido pelo modelo de aprendizado de máquina do Azure Olá provisionado como parte da solução e integrados com caminho de saudação em tempo real.</span><span class="sxs-lookup"><span data-stu-id="c29e5-197">It is set by hello Azure Machine Learning model provisioned as part of solution and integrated with hello real-time path.</span></span> <span data-ttu-id="c29e5-198">o valor de Hello "1" indica que um veículo exige manutenção.</span><span class="sxs-lookup"><span data-stu-id="c29e5-198">hello value “1” indicates a vehicle requires maintenance.</span></span> 

<span data-ttu-id="c29e5-199">tooadd um **nível de página** filtro para mostrar dados de veículos, que exigem manutenção:</span><span class="sxs-lookup"><span data-stu-id="c29e5-199">tooadd a **Page Level** filter for showing vehicles data, which are requiring maintenance:</span></span> 

1. <span data-ttu-id="c29e5-200">Saudação de arrastar **"MaintenanceLabel"** para **filtros em nível de página**.</span><span class="sxs-lookup"><span data-stu-id="c29e5-200">Drag hello **“MaintenanceLabel”** field into **Page Level Filters**.</span></span>  
   <span data-ttu-id="c29e5-201">![Carros conectados - Filtros de página](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n1.png)</span><span class="sxs-lookup"><span data-stu-id="c29e5-201">![Connected Cars - Page Level Filters](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n1.png)</span></span>  
2. <span data-ttu-id="c29e5-202">Clique no menu **Filtragem Básica** presente na parte inferior do Filtro de página MaintenanceLabel.</span><span class="sxs-lookup"><span data-stu-id="c29e5-202">Click **Basic Filtering** menu present at bottom of MaintenanceLabel Page Level Filter.</span></span>  
   <span data-ttu-id="c29e5-203">![Carros conectados - Filtragem básica](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n2.png)</span><span class="sxs-lookup"><span data-stu-id="c29e5-203">![Connected Cars - Basic Filtering](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n2.png)</span></span>  
3. <span data-ttu-id="c29e5-204">Definir o valor de filtro muito**"1"**  </span><span class="sxs-lookup"><span data-stu-id="c29e5-204">Set its filter value too**“1”**  </span></span>  
   <span data-ttu-id="c29e5-205">![Carros conectados - Valor do filtro](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n3.png)</span><span class="sxs-lookup"><span data-stu-id="c29e5-205">![Connected Cars - Filter Value](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n3.png)</span></span>  

<span data-ttu-id="c29e5-206">Clique em nova visualização do hello área em branco tooadd.</span><span class="sxs-lookup"><span data-stu-id="c29e5-206">Click hello blank area tooadd new visualization.</span></span>  

<span data-ttu-id="c29e5-207">Selecione o **Gráfico de Coluna Clusterizada** das visualizações</span><span class="sxs-lookup"><span data-stu-id="c29e5-207">Select **Clustered Column Chart** from visualizations</span></span>  
<span data-ttu-id="c29e5-208">![Carros conectados - Visualização da placa do vind](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4o.png)</span><span class="sxs-lookup"><span data-stu-id="c29e5-208">![Connected Cars - Vind Card Visualization](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4o.png)</span></span>  
<span data-ttu-id="c29e5-209">![Carros conectados - Gráfico de colunas agrupadas](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4p.png)</span><span class="sxs-lookup"><span data-stu-id="c29e5-209">![Connected Cars - Clustered Column Chart](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4p.png)</span></span>

<span data-ttu-id="c29e5-210">Campo de arrastar **modelo** em **eixo** área, **Vin** muito**valor** área.</span><span class="sxs-lookup"><span data-stu-id="c29e5-210">Drag field **Model** into **Axis** area, **Vin** too**Value** area.</span></span> <span data-ttu-id="c29e5-211">Em seguida, classifique visualização por **Contagem de vin**.</span><span class="sxs-lookup"><span data-stu-id="c29e5-211">Then sort visualization by **Count of vin**.</span></span>  <span data-ttu-id="c29e5-212">Gráfico de alteração **título** muito**"Veículos que exigem manutenção pelo modelo"**</span><span class="sxs-lookup"><span data-stu-id="c29e5-212">Change chart **Title** too**“Vehicles requiring maintenance by model”**</span></span>  

<span data-ttu-id="c29e5-213">Arraste os campos **vin** para a **Saturação da cor** presente na seção **Campos**![Fields](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4field.png) da guia **Visualização**</span><span class="sxs-lookup"><span data-stu-id="c29e5-213">Drag **vin** fields into **Color Saturation** present at **Fields** ![Fields](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4field.png) section of **Visualization** tab</span></span>  
<span data-ttu-id="c29e5-214">![Carros conectados - Saturação de cor](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4q.png)</span><span class="sxs-lookup"><span data-stu-id="c29e5-214">![Connected Cars - Color Saturation](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4q.png)</span></span>  

<span data-ttu-id="c29e5-215">Alterar **Cores dos Dados** nas visualizações na seção **Formato**</span><span class="sxs-lookup"><span data-stu-id="c29e5-215">Change **Data Colors** in visualizations from **Format** section</span></span>  
<span data-ttu-id="c29e5-216">Alterar a cor do Mínimo para: **F2C812**</span><span class="sxs-lookup"><span data-stu-id="c29e5-216">Change Minimum color to: **F2C812**</span></span>  
<span data-ttu-id="c29e5-217">Alterar a cor do Máximo para: **FF6300**</span><span class="sxs-lookup"><span data-stu-id="c29e5-217">Change Maximum color to: **FF6300**</span></span>  
<span data-ttu-id="c29e5-218">![Carros conectados - Alterações de cor](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4r.png)</span><span class="sxs-lookup"><span data-stu-id="c29e5-218">![Connected Cars - Color Changes](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4r.png)</span></span>  
<span data-ttu-id="c29e5-219">![Carros conectados - Novas cores de visualização](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4s.png)</span><span class="sxs-lookup"><span data-stu-id="c29e5-219">![Connected Cars - New Visualization Colors](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4s.png)</span></span>  

<span data-ttu-id="c29e5-220">Clique em nova visualização do hello área em branco tooadd.</span><span class="sxs-lookup"><span data-stu-id="c29e5-220">Click hello blank area tooadd new visualization.</span></span>  

<span data-ttu-id="c29e5-221">Selecione **Gráfico de colunas clusterizado** das visualizações, arraste o campo **vin** para a área **Valor**, arraste o campo **Cidade** para a área **Eixo**.</span><span class="sxs-lookup"><span data-stu-id="c29e5-221">Select **Clustered column chart** from visualizations, drag **vin** field into **Value** area, drag **City** field into **Axis** area.</span></span> <span data-ttu-id="c29e5-222">Classificar gráfico por **"Contagem de vin"**.</span><span class="sxs-lookup"><span data-stu-id="c29e5-222">Sort chart by **“Count of vin”**.</span></span> <span data-ttu-id="c29e5-223">Gráfico de alteração **título** muito**"Veículos que necessitam de manutenção por cidade"** </span><span class="sxs-lookup"><span data-stu-id="c29e5-223">Change chart **Title** too**“Vehicles requiring maintenance by city”** </span></span>  
<span data-ttu-id="c29e5-224">![Carros conectados - Veículos que precisam de manutenção por cidade](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4t.png)</span><span class="sxs-lookup"><span data-stu-id="c29e5-224">![Connected Cars - Vehicles requiring maintenance by city](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4t.png)</span></span>  

<span data-ttu-id="c29e5-225">Clique em nova visualização do hello área em branco tooadd.</span><span class="sxs-lookup"><span data-stu-id="c29e5-225">Click hello blank area tooadd new visualization.</span></span>  

<span data-ttu-id="c29e5-226">Selecione **cartão de várias linhas** visualização de visualizações, arraste **modelo** e **vin** em Olá **campos** área.</span><span class="sxs-lookup"><span data-stu-id="c29e5-226">Select **Multi-Row Card** visualization from visualizations, drag **Model** and **vin** into hello **Fields** area.</span></span>  
<span data-ttu-id="c29e5-227">![Carros conectados - Placa com várias linhas](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4u.png)</span><span class="sxs-lookup"><span data-stu-id="c29e5-227">![Connected Cars - Multi-Row Card](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4u.png)</span></span>    

<span data-ttu-id="c29e5-228">Esse relatório final Olá reorganizar todos visualização hello, tem a seguinte aparência:</span><span class="sxs-lookup"><span data-stu-id="c29e5-228">Rearranging all of hello visualization, hello final report looks as follows:</span></span>  
![Carros conectados - Placa com várias linhas](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4v.png)  

<span data-ttu-id="c29e5-230">Você configurou com êxito o relatório em tempo real do hello "Veículos necessidade de manutenção".</span><span class="sxs-lookup"><span data-stu-id="c29e5-230">You have successfully configured hello “Vehicles Requiring Maintenance” real-time report.</span></span> <span data-ttu-id="c29e5-231">Você pode continuar relatório em tempo real do toocreate Olá Avançar ou parar aqui e configurar Olá painel.</span><span class="sxs-lookup"><span data-stu-id="c29e5-231">You can proceed toocreate hello next real-time report or stop here and configure hello dashboard.</span></span> 

### <a name="3-vehicles-health-statistics"></a><span data-ttu-id="c29e5-232">3. Estatísticas de integridade de veículos</span><span class="sxs-lookup"><span data-stu-id="c29e5-232">3. Vehicles Health Statistics</span></span>
<span data-ttu-id="c29e5-233">Clique em ![adicionar](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) tooadd novo relatório, renomeá-lo muito**"Estatísticas de integridade veículos"**</span><span class="sxs-lookup"><span data-stu-id="c29e5-233">Click ![Add](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) tooadd new report, rename it too**“Vehicles Health Statistics”**</span></span>  

<span data-ttu-id="c29e5-234">Selecione **medidor** visualização de visualizações, em seguida, arraste Olá **velocidade** para **, valor mínimo, máximo** áreas.</span><span class="sxs-lookup"><span data-stu-id="c29e5-234">Select **Gauge** visualization from visualizations, then drag hello **Speed** field into **Value, Minimum Value, Maximum Value** areas.</span></span>  
<span data-ttu-id="c29e5-235">![Carros conectados - Placa com várias linhas](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4w.png)</span><span class="sxs-lookup"><span data-stu-id="c29e5-235">![Connected Cars - Multi-Row Card](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4w.png)</span></span>  

<span data-ttu-id="c29e5-236">Alterar a agregação padrão de saudação do **velocidade** na **valor área** muito**médio**</span><span class="sxs-lookup"><span data-stu-id="c29e5-236">Change hello default aggregation of **speed** in **Value area** too**Average**</span></span> 

<span data-ttu-id="c29e5-237">Alterar a agregação padrão de saudação do **velocidade** na **área mínima** muito**mínimo**</span><span class="sxs-lookup"><span data-stu-id="c29e5-237">Change hello default aggregation of **speed** in **Minimum area** too**Minimum**</span></span>

<span data-ttu-id="c29e5-238">Alterar a agregação padrão de saudação do **velocidade** na **área máximo** muito**máximo**</span><span class="sxs-lookup"><span data-stu-id="c29e5-238">Change hello default aggregation of **speed** in **Maximum area** too**Maximum**</span></span>

![Carros conectados - Placa com várias linhas](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4x.png)  

<span data-ttu-id="c29e5-240">Renomear Olá **medidor título** muito**"Velocidade média"**</span><span class="sxs-lookup"><span data-stu-id="c29e5-240">Rename hello **Gauge Title** too**“Average speed”**</span></span> 

![Carros conectados - Medidor](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4y.png)  

<span data-ttu-id="c29e5-242">Clique em nova visualização do hello área em branco tooadd.</span><span class="sxs-lookup"><span data-stu-id="c29e5-242">Click hello blank area tooadd new visualization.</span></span>  

<span data-ttu-id="c29e5-243">Da mesma forma, adicione um **Medidor** para **média de óleo do motor**, **média de combustível** e **temperatura média do motor**.</span><span class="sxs-lookup"><span data-stu-id="c29e5-243">Similarly add a **Gauge** for **average engine oil**, **average fuel**, and **average engine temperate**.</span></span>  

<span data-ttu-id="c29e5-244">Alterar saudação padrão agregação dos campos em cada medidor conforme descrito acima etapas **"Velocidade média"** do medidor.</span><span class="sxs-lookup"><span data-stu-id="c29e5-244">Change hello default aggregation of fields in each gauge as per above steps in **“Average speed”** gauge.</span></span>

![Carros conectados - Medidores](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4z.png)

<span data-ttu-id="c29e5-246">Clique em nova visualização do hello área em branco tooadd.</span><span class="sxs-lookup"><span data-stu-id="c29e5-246">Click hello blank area tooadd new visualization.</span></span>

<span data-ttu-id="c29e5-247">Selecione **clusterizado gráfico de coluna e linha** de visualizações, em seguida, arraste **City** para **eixo compartilhado**, arraste **velocidade**, **campos tirepressure e engineoil** em **valores de coluna** área, alterar seu tipo de agregação também**médio**.</span><span class="sxs-lookup"><span data-stu-id="c29e5-247">Select **Line and Clustered Column Chart** from visualizations, then drag **City** field into **Shared Axis**, drag **speed**, **tirepressure and engineoil fields** into **Column Values** area, change their aggregation type too**Average**.</span></span> 

<span data-ttu-id="c29e5-248">Saudação de arrastar **engineTemperature** para **valores de linha** área, alterar o tipo de agregação de saudação muito**médio**.</span><span class="sxs-lookup"><span data-stu-id="c29e5-248">Drag hello **engineTemperature** field into **Line Values** area, change hello  aggregation type too**Average**.</span></span> 

![Carros conectados - Campos de visualizações](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4aa.png)

<span data-ttu-id="c29e5-250">Gráfico de saudação de alteração **título** muito**"Média de velocidade, pneu pressão, petróleo mecanismo e temperatura de mecanismo"**.</span><span class="sxs-lookup"><span data-stu-id="c29e5-250">Change hello chart **Title** too**“Average speed, tire pressure, engine oil and engine temperature”**.</span></span>  

![Carros conectados - Campos de visualizações](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4bb.png)

<span data-ttu-id="c29e5-252">Clique em nova visualização do hello área em branco tooadd.</span><span class="sxs-lookup"><span data-stu-id="c29e5-252">Click hello blank area tooadd new visualization.</span></span>

<span data-ttu-id="c29e5-253">Selecione **Treemap** visualização de visualizações, arraste Olá **modelo** para Olá **grupo** área e arraste Olá campo ** MaintenanceProbability** em Olá **valores** área.</span><span class="sxs-lookup"><span data-stu-id="c29e5-253">Select **Treemap** visualization from visualizations, drag hello **Model** field into hello **Group** area, and drag hello field **MaintenanceProbability** into hello **Values** area.</span></span>

<span data-ttu-id="c29e5-254">Gráfico de saudação de alteração **título** muito**"Modelos de veículo que necessitam de manutenção"**.</span><span class="sxs-lookup"><span data-stu-id="c29e5-254">Change hello chart **Title** too**“Vehicle models requiring maintenance”**.</span></span>

![Carros conectados - Alterar título do gráfico](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4cc.png)

<span data-ttu-id="c29e5-256">Clique em nova visualização do hello área em branco tooadd.</span><span class="sxs-lookup"><span data-stu-id="c29e5-256">Click hello blank area tooadd new visualization.</span></span>

<span data-ttu-id="c29e5-257">Selecione **gráfico de barras empilhadas 100%** de visualização, arraste Olá **city** para Olá **eixo** área e arraste Olá **MaintenanceProbability**, **RecallProbability** campos em Olá **valor** área.</span><span class="sxs-lookup"><span data-stu-id="c29e5-257">Select **100% Stacked Bar Chart** from visualization, drag hello **city** field into hello **Axis** area, and drag hello **MaintenanceProbability**, **RecallProbability** fields into hello **Value** area.</span></span>

![Carros conectados - Adicionar nova visualização](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4dd.png)

<span data-ttu-id="c29e5-259">Clique em **formato**, selecione **cores de dados**e conjunto hello **MaintenanceProbability** toohello valor de cor **"F2C80F"**.</span><span class="sxs-lookup"><span data-stu-id="c29e5-259">Click **Format**, select **Data Colors**, and set hello **MaintenanceProbability** color toohello value **“F2C80F”**.</span></span>

<span data-ttu-id="c29e5-260">Saudação de alteração **título** de saudação do gráfico muito**"Probabilidade de veículo manutenção e lembre-se por cidade"**.</span><span class="sxs-lookup"><span data-stu-id="c29e5-260">Change hello **Title** of hello chart too**“Probability of Vehicle Maintenance & Recall by City”**.</span></span>

![Carros conectados - Adicionar nova visualização](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4ee.png)

<span data-ttu-id="c29e5-262">Clique em nova visualização do hello área em branco tooadd.</span><span class="sxs-lookup"><span data-stu-id="c29e5-262">Click hello blank area tooadd new visualization.</span></span>

<span data-ttu-id="c29e5-263">Selecione **gráfico de área** de visualização de visualizações, arraste Olá **modelo** para Olá **eixo** área e arraste Olá **engineOil, tirepressure, velocidade e MaintenanceProbability** campos em Olá **valores** área.</span><span class="sxs-lookup"><span data-stu-id="c29e5-263">Select **Area Chart** from visualization from visualizations, drag hello **Model** field into hello **Axis** area, and drag hello **engineOil, tirepressure, speed and MaintenanceProbability** fields into hello **Values** area.</span></span> <span data-ttu-id="c29e5-264">Alterar o tipo de agregação muito**"Médio"**.</span><span class="sxs-lookup"><span data-stu-id="c29e5-264">Change their aggregation type too**“Average”**.</span></span> 

![Carros conectados - Alterar tipo de agregação](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4ff.png)

<span data-ttu-id="c29e5-266">Alterar o título de saudação do gráfico de saudação muito**"Média petróleo mecanismo, tire pressão, velocidade e manutenção de probabilidade pelo modelo"**.</span><span class="sxs-lookup"><span data-stu-id="c29e5-266">Change hello title of hello chart too**“Average engine oil, tire pressure, speed and maintenance probability by model”**.</span></span>

![Carros conectados - Alterar título do gráfico](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4gg.png)

<span data-ttu-id="c29e5-268">Clique em nova visualização do hello área em branco tooadd:</span><span class="sxs-lookup"><span data-stu-id="c29e5-268">Click hello blank area tooadd new visualization:</span></span>

1. <span data-ttu-id="c29e5-269">Selecione a visualização **Gráfico de Dispersão** em visualizações.</span><span class="sxs-lookup"><span data-stu-id="c29e5-269">Select **Scatter Chart** visualization from visualizations.</span></span>
2. <span data-ttu-id="c29e5-270">Saudação de arrastar **modelo** para Olá **detalhes** e **legenda** área.</span><span class="sxs-lookup"><span data-stu-id="c29e5-270">Drag hello **Model** field into hello **Details** and **Legend** area.</span></span>
3. <span data-ttu-id="c29e5-271">Saudação de arrastar **combustível** para Olá **eixo x** área, altere a agregação de saudação muito**médio**.</span><span class="sxs-lookup"><span data-stu-id="c29e5-271">Drag hello **fuel** field into hello **X-Axis** area, change hello aggregation too**Average**.</span></span>
4. <span data-ttu-id="c29e5-272">Arraste **engineTemparature** em **área de eixo y**, altere a agregação de saudação muito**médio**</span><span class="sxs-lookup"><span data-stu-id="c29e5-272">Drag **engineTemparature** into **Y-Axis area**, change hello aggregation too**Average**</span></span>
5. <span data-ttu-id="c29e5-273">Saudação de arrastar **vin** para Olá **tamanho** área.</span><span class="sxs-lookup"><span data-stu-id="c29e5-273">Drag hello **vin** field into hello **Size** area.</span></span>

![Carros conectados - Adicionar nova visualização](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4hh.png)

<span data-ttu-id="c29e5-275">Gráfico de saudação de alteração **título** muito**"Médias de combustível, temperatura mecanismo por modelo"**.</span><span class="sxs-lookup"><span data-stu-id="c29e5-275">Change hello chart **Title** too**“Averages of Fuel, Engine Temperature by Model”**.</span></span>

![Carros conectados - Alterar título do gráfico](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4ii.png)

<span data-ttu-id="c29e5-277">Esse relatório final Olá se parecerá com conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="c29e5-277">hello final report will look like as shown below.</span></span>

![Carros conectados-Relatório final](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4jj.png)

### <a name="pin-visualizations-from-hello-reports-toohello-real-time-dashboard"></a><span data-ttu-id="c29e5-279">Visualizações de PIN de painel em tempo real do hello relatórios toohello</span><span class="sxs-lookup"><span data-stu-id="c29e5-279">Pin visualizations from hello reports toohello real-time dashboard</span></span>
<span data-ttu-id="c29e5-280">Crie um painel em branco clicando no ícone de adição Olá tooDashboards Avançar.</span><span class="sxs-lookup"><span data-stu-id="c29e5-280">Create a blank dashboard by clicking on hello plus icon next tooDashboards.</span></span> <span data-ttu-id="c29e5-281">Você pode chamá-lo de "Painel de análise de telemetria do veículo"</span><span class="sxs-lookup"><span data-stu-id="c29e5-281">You can name it “Vehicle Telemetry Analytics Dashboard”</span></span>

![Carros conectados-Painel](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.5.png)

<span data-ttu-id="c29e5-283">Visualização de fixar Olá da saudação acima do painel de toohello de relatórios.</span><span class="sxs-lookup"><span data-stu-id="c29e5-283">Pin hello visualization from hello above reports toohello dashboard.</span></span> 

![Carros conectados-Painel](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.6.png)

<span data-ttu-id="c29e5-285">Painel de saudação se assemelhar ao seguinte quando todos os Olá três relatórios são criados e Olá correspondente visualizações são fixados toohello painel.</span><span class="sxs-lookup"><span data-stu-id="c29e5-285">hello dashboard should look as follows when all hello three reports are created and hello corresponding visualizations are pinned toohello dashboard.</span></span> <span data-ttu-id="c29e5-286">Se você não tiver criado todos os relatórios de saudação, seu painel pode ser diferente.</span><span class="sxs-lookup"><span data-stu-id="c29e5-286">If you have not created all hello reports, your dashboard could look different.</span></span> 

![Carros conectados-Painel](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-4.0.png)

<span data-ttu-id="c29e5-288">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="c29e5-288">Congratulations!</span></span> <span data-ttu-id="c29e5-289">Você criou com êxito o dashboard em tempo real de saudação.</span><span class="sxs-lookup"><span data-stu-id="c29e5-289">You have successfully created hello real-time dashboard.</span></span> <span data-ttu-id="c29e5-290">Enquanto você continua tooexecute CarEventGenerator.exe e RealtimeDashboardApp.exe, você deve ver atualizações dinâmicas no painel de saudação.</span><span class="sxs-lookup"><span data-stu-id="c29e5-290">As you continue tooexecute CarEventGenerator.exe and RealtimeDashboardApp.exe, you should see live updates on hello dashboard.</span></span> <span data-ttu-id="c29e5-291">Ele deve levar Olá de toocomplete minutos too15 10 etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="c29e5-291">It should take about 10 too15 minutes toocomplete hello following steps.</span></span>

## <a name="setup-power-bi-batch-processing-dashboard"></a><span data-ttu-id="c29e5-292">Instalação do painel de processamento em lote do Power BI</span><span class="sxs-lookup"><span data-stu-id="c29e5-292">Setup Power BI batch processing dashboard</span></span>
> [!NOTE]
> <span data-ttu-id="c29e5-293">Ele leva cerca de duas horas (de conclusão bem-sucedida de saudação da implantação Olá) para Olá final tooend processamento em lotes a execução do pipeline toofinish e processe a partir de um ano de dados gerados.</span><span class="sxs-lookup"><span data-stu-id="c29e5-293">It takes about two hours (from hello successful completion of hello deployment) for hello end tooend batch processing pipeline toofinish execution and process a year worth of generated data.</span></span> <span data-ttu-id="c29e5-294">Portanto, aguarde Olá processamento toofinish antes de continuar com as próximas etapas hello.</span><span class="sxs-lookup"><span data-stu-id="c29e5-294">So wait for hello processing toofinish before proceeding with hello next steps.</span></span> 
> 
> 

<span data-ttu-id="c29e5-295">**Baixe o arquivo de designer Olá Power BI**</span><span class="sxs-lookup"><span data-stu-id="c29e5-295">**Download hello Power BI designer file**</span></span>

* <span data-ttu-id="c29e5-296">Um arquivo de designer do Power BI pré-configurado é incluído como parte da implantação de saudação instruções de operação Manual</span><span class="sxs-lookup"><span data-stu-id="c29e5-296">A pre-configured Power BI designer file is included as part of hello deployment Manual Operation Instructions</span></span>
* <span data-ttu-id="c29e5-297">Procure por 2.</span><span class="sxs-lookup"><span data-stu-id="c29e5-297">Look for 2.</span></span> <span data-ttu-id="c29e5-298">Painel de processamento em lote instalação Power BI você pode baixar o modelo do Power BI Olá para o painel de processamento em lotes chamado **ConnectedCarsPbiReport.pbix**.</span><span class="sxs-lookup"><span data-stu-id="c29e5-298">Setup PowerBI batch processing dashboard You can download hello PowerBI template for batch processing dashboard here called **ConnectedCarsPbiReport.pbix**.</span></span>
* <span data-ttu-id="c29e5-299">Salve localmente</span><span class="sxs-lookup"><span data-stu-id="c29e5-299">Save locally</span></span>

<span data-ttu-id="c29e5-300">**Configurar relatórios do Power BI**</span><span class="sxs-lookup"><span data-stu-id="c29e5-300">**Configure Power BI reports**</span></span>

* <span data-ttu-id="c29e5-301">Arquivo de designer Olá aberto '**ConnectedCarsPbiReport.pbix**' usando o Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="c29e5-301">Open hello designer file ‘**ConnectedCarsPbiReport.pbix**’ using Power BI Desktop.</span></span> <span data-ttu-id="c29e5-302">Se você já não tiver, instale Olá Power BI Desktop de [instalação do Power BI Desktop](http://www.microsoft.com/download/details.aspx?id=45331).</span><span class="sxs-lookup"><span data-stu-id="c29e5-302">If you do not already have, install hello Power BI Desktop from [Power BI Desktop install](http://www.microsoft.com/download/details.aspx?id=45331).</span></span> 
* <span data-ttu-id="c29e5-303">Clique em Olá **editar consultas**.</span><span class="sxs-lookup"><span data-stu-id="c29e5-303">Click hello **Edit Queries**.</span></span>

![Editar consulta do Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/10-edit-powerbi-query.png)

* <span data-ttu-id="c29e5-305">Clique duas vezes em Olá **fonte**.</span><span class="sxs-lookup"><span data-stu-id="c29e5-305">Double-click hello **Source**.</span></span>

![Definir origem do Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/11-set-powerbi-source.png)

* <span data-ttu-id="c29e5-307">Atualize a cadeia de caracteres de conexão de servidor com hello Azure SQL server que foi configurado como parte da implantação de saudação.</span><span class="sxs-lookup"><span data-stu-id="c29e5-307">Update Server connection string with hello Azure SQL server that got provisioned as part of hello deployment.</span></span>  <span data-ttu-id="c29e5-308">Procure nas instruções de operação Olá Manual em</span><span class="sxs-lookup"><span data-stu-id="c29e5-308">Look in hello Manual Operation Instructions under</span></span> 

    4. <span data-ttu-id="c29e5-309">Banco de Dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="c29e5-309">Azure SQL Database</span></span>
    
    * <span data-ttu-id="c29e5-310">Servidor: somethingsrv.database.windows.net</span><span class="sxs-lookup"><span data-stu-id="c29e5-310">Server: somethingsrv.database.windows.net</span></span>
    * <span data-ttu-id="c29e5-311">Banco de dados: connectedcar</span><span class="sxs-lookup"><span data-stu-id="c29e5-311">Database: connectedcar</span></span>
    * <span data-ttu-id="c29e5-312">Nome de usuário: username</span><span class="sxs-lookup"><span data-stu-id="c29e5-312">Username: username</span></span>
    * <span data-ttu-id="c29e5-313">Senha: gerencie sua senha do SQL Server no Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="c29e5-313">Password: You can manage your SQL server password from Azure portal</span></span>

* <span data-ttu-id="c29e5-314">Deixe **Banco de dados** como *connectedcar*.</span><span class="sxs-lookup"><span data-stu-id="c29e5-314">Leave **Database** as *connectedcar*.</span></span>

![Definir banco de dados do Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/12-set-powerbi-database.png)

* <span data-ttu-id="c29e5-316">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="c29e5-316">Click **OK**.</span></span>
* <span data-ttu-id="c29e5-317">Você verá **credencial do Windows** guia é selecionada por padrão, alterá-la muito**credenciais de banco de dados** clicando em **banco de dados** guia à direita.</span><span class="sxs-lookup"><span data-stu-id="c29e5-317">You will see **Windows credential** tab selected by default, change it too**Database credentials** by clicking on **Database** tab at right.</span></span>
* <span data-ttu-id="c29e5-318">Fornecer Olá **Username** e **senha** do seu banco de dados de SQL do Azure que foi especificada durante a instalação de sua implantação.</span><span class="sxs-lookup"><span data-stu-id="c29e5-318">Provide hello **Username** and **Password** of your Azure SQL Database that was specified during its deployment setup.</span></span>

![Forneça as credenciais do banco de dados](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/13-provide-database-credentials.png)

* <span data-ttu-id="c29e5-320">Clique em **Conectar**</span><span class="sxs-lookup"><span data-stu-id="c29e5-320">Click **Connect**</span></span>
* <span data-ttu-id="c29e5-321">Repita Olá acima etapas para cada Olá três restantes consultas presentes no painel direito e, em seguida, atualizar detalhes de conexão de fonte de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="c29e5-321">Repeat hello above steps for each of hello three remaining queries present at right pane, and then update hello data source connection details.</span></span>
* <span data-ttu-id="c29e5-322">Clique em **Fechar e Carregar**.</span><span class="sxs-lookup"><span data-stu-id="c29e5-322">Click **Close and Load**.</span></span> <span data-ttu-id="c29e5-323">Conjuntos de dados de arquivo do Power BI Desktop são tabelas de banco de dados do Azure tooSQL conectado.</span><span class="sxs-lookup"><span data-stu-id="c29e5-323">Power BI Desktop file datasets are connected tooSQL Azure Database tables.</span></span>
* <span data-ttu-id="c29e5-324">**Fechar** arquivo do Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="c29e5-324">**Close** Power BI Desktop file.</span></span>

![Fechar o Power BI Desktop](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/14-close-powerbi-desktop.png)

* <span data-ttu-id="c29e5-326">Clique em **salvar** botão toosave alterações de saudação.</span><span class="sxs-lookup"><span data-stu-id="c29e5-326">Click **Save** button toosave hello changes.</span></span> 

<span data-ttu-id="c29e5-327">Você configurou agora todos os relatórios de saudação correspondente do caminho de processamento de lote toohello na solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="c29e5-327">You have now configured all hello reports corresponding toohello batch processing path in hello solution.</span></span> 

## <a name="upload-toopowerbicom"></a><span data-ttu-id="c29e5-328">Carregar muito*powerbi.com*</span><span class="sxs-lookup"><span data-stu-id="c29e5-328">Upload too*powerbi.com*</span></span>
1. <span data-ttu-id="c29e5-329">Navegue toohello portal de web do Power BI em http://powerbi.com e logon.</span><span class="sxs-lookup"><span data-stu-id="c29e5-329">Navigate toohello Power BI web portal at http://powerbi.com and login.</span></span>
2. <span data-ttu-id="c29e5-330">Clique em **Obter Dados**</span><span class="sxs-lookup"><span data-stu-id="c29e5-330">Click **Get Data**</span></span>  
3. <span data-ttu-id="c29e5-331">Carregar Olá arquivo do Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="c29e5-331">Upload hello Power BI Desktop File.</span></span>  
4. <span data-ttu-id="c29e5-332">tooupload, clique em **obter dados -> obter arquivos -> arquivo Local**</span><span class="sxs-lookup"><span data-stu-id="c29e5-332">tooupload, click **Get Data -> Files Get -> Local file**</span></span>  
5. <span data-ttu-id="c29e5-333">Navegue toohello **"**ConnectedCarsPbiReport.pbix**"**</span><span class="sxs-lookup"><span data-stu-id="c29e5-333">Navigate toohello **“**ConnectedCarsPbiReport.pbix**”**</span></span>  
6. <span data-ttu-id="c29e5-334">Uma vez carregado o arquivo hello, será navegado tooyour back espaço de trabalho do Power BI.</span><span class="sxs-lookup"><span data-stu-id="c29e5-334">Once hello file is uploaded, you will be navigated back tooyour Power BI work space.</span></span>  

<span data-ttu-id="c29e5-335">Um conjunto de dados, relatórios e um painel em branco serão criados para você.</span><span class="sxs-lookup"><span data-stu-id="c29e5-335">A dataset, report and a blank dashboard will be created for you.</span></span>  

<span data-ttu-id="c29e5-336">Fixar gráficos tooa novo painel chamado **painel de análise de telemetria do veículo** na **Power BI**.</span><span class="sxs-lookup"><span data-stu-id="c29e5-336">Pin charts tooa new dashboard called **Vehicle Telemetry Analytics Dashboard** in **Power BI**.</span></span> <span data-ttu-id="c29e5-337">Clique em Olá painel em branco criado acima e, em seguida, navegue toohello **relatórios** seção clique Olá carregado recentemente o relatório.</span><span class="sxs-lookup"><span data-stu-id="c29e5-337">Click hello blank dashboard created above and then navigate toohello **Reports** section click hello newly uploaded report.</span></span>  

![Telemetria do veículo Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard1.png) 

<span data-ttu-id="c29e5-339">**Observação Olá relatório tem seis páginas:**</span><span class="sxs-lookup"><span data-stu-id="c29e5-339">**Note hello report has six pages:**</span></span>  
<span data-ttu-id="c29e5-340">Página 1: densidade do veículo</span><span class="sxs-lookup"><span data-stu-id="c29e5-340">Page 1: Vehicle density</span></span>  
<span data-ttu-id="c29e5-341">Página 2: integridade do veículo em tempo real</span><span class="sxs-lookup"><span data-stu-id="c29e5-341">Page 2: Real-time vehicle health</span></span>  
<span data-ttu-id="c29e5-342">Página 3: veículos com direção agressiva</span><span class="sxs-lookup"><span data-stu-id="c29e5-342">Page 3: Aggressively Driven Vehicles</span></span>   
<span data-ttu-id="c29e5-343">Página 4: veículos que sofreram recall</span><span class="sxs-lookup"><span data-stu-id="c29e5-343">Page 4: Recalled vehicles</span></span>  
<span data-ttu-id="c29e5-344">Página 5: veículos com uso eficiente de combustível</span><span class="sxs-lookup"><span data-stu-id="c29e5-344">Page 5: Fuel Efficiently Driven Vehicles</span></span>  
<span data-ttu-id="c29e5-345">Página 6: logotipo da Contoso</span><span class="sxs-lookup"><span data-stu-id="c29e5-345">Page 6: Contoso Logo</span></span>  

![Carros conectados Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard2.png)

<span data-ttu-id="c29e5-347">**Na página 3**, fixar seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="c29e5-347">**From Page 3**, pin hello following:</span></span>  

1. <span data-ttu-id="c29e5-348">Contagem de vin</span><span class="sxs-lookup"><span data-stu-id="c29e5-348">Count of VIN</span></span>  
   ![Carros conectados Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard3.png) 
2. <span data-ttu-id="c29e5-350">Veículos de direção agressiva por modelo – Gráfico de cascata </span><span class="sxs-lookup"><span data-stu-id="c29e5-350">Aggressively driven vehicles by model – Waterfall chart</span></span>  
   ![Telemetria de veículo - Fixar gráficos 4](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard4.png)

<span data-ttu-id="c29e5-352">**Na página 5**, fixar seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="c29e5-352">**From Page 5**, pin hello following:</span></span> 

1. <span data-ttu-id="c29e5-353">Contagem de vin</span><span class="sxs-lookup"><span data-stu-id="c29e5-353">Count of vin</span></span>    
   ![Telemetria de veículo - Fixar gráficos 5](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard5.png)  
2. <span data-ttu-id="c29e5-355">Veículos com eficiência de combustível: Gráfico de colunas agrupadas </span><span class="sxs-lookup"><span data-stu-id="c29e5-355">Fuel efficient vehicles by model: Clustered column chart</span></span>  
   ![Telemetria de veículo - Fixar gráficos 6](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard6.png)

<span data-ttu-id="c29e5-357">**Na página 4**, fixar seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="c29e5-357">**From Page 4**, pin hello following:</span></span>  

1. <span data-ttu-id="c29e5-358">Contagem de vin</span><span class="sxs-lookup"><span data-stu-id="c29e5-358">Count of vin</span></span>  
   ![Telemetria de veículo - Fixar gráficos 7](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard7.png) 
2. <span data-ttu-id="c29e5-360">Veículos que tiveram recall por cidade, modelo : Treemap </span><span class="sxs-lookup"><span data-stu-id="c29e5-360">Recalled vehicles by city, model: Treemap</span></span>  
   ![Telemetria de veículo - Fixar gráficos 8](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard8.png)  

<span data-ttu-id="c29e5-362">**Na página 6**, fixar seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="c29e5-362">**From Page 6**, pin hello following:</span></span>  

1. <span data-ttu-id="c29e5-363">Logotipo da Contoso Motors </span><span class="sxs-lookup"><span data-stu-id="c29e5-363">Contoso Motors logo</span></span>  
   ![Telemetria de veículo - Fixar gráficos 9](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard9.png)

<span data-ttu-id="c29e5-365">**Organizar Olá painel**</span><span class="sxs-lookup"><span data-stu-id="c29e5-365">**Organize hello dashboard**</span></span>  

1. <span data-ttu-id="c29e5-366">Navegue toohello painel</span><span class="sxs-lookup"><span data-stu-id="c29e5-366">Navigate toohello dashboard</span></span>
2. <span data-ttu-id="c29e5-367">Passe o mouse sobre cada gráfico e renomear com base na nomenclatura Olá fornecido na imagem do painel completa Olá abaixo.</span><span class="sxs-lookup"><span data-stu-id="c29e5-367">Hover over each chart and rename it based on hello naming provided in hello complete dashboard image below.</span></span> <span data-ttu-id="c29e5-368">Também mova gráficos Olá em torno de toolook como Olá painel abaixo.</span><span class="sxs-lookup"><span data-stu-id="c29e5-368">Also move hello charts around toolook like hello dashboard below.</span></span>  
   ![Telemetria de veículo - Organizar painel 2](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-organize-dashboard2.png)  
   ![Telemetria do veículo Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard.png)
3. <span data-ttu-id="c29e5-371">Se você tiver criado todos os relatórios de saudação mencionados neste documento, hello painel concluído final deve ter aparência Olá figura a seguir.</span><span class="sxs-lookup"><span data-stu-id="c29e5-371">If you have created all hello reports as mentioned in this document, hello final completed dashboard should look like hello following figure.</span></span> 

![Telemetria de veículo - Organizar painel 2](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-organize-dashboard3.png)

<span data-ttu-id="c29e5-373">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="c29e5-373">Congratulations!</span></span> <span data-ttu-id="c29e5-374">Você criou com êxito o hello relatórios e Olá toogain painel em tempo real, previsão e ideias de lote de integridade de veículo e orientar hábitos.</span><span class="sxs-lookup"><span data-stu-id="c29e5-374">You have successfully created hello reports and hello dashboard toogain real-time, predictive and batch insights on vehicle health and driving habits.</span></span>  
