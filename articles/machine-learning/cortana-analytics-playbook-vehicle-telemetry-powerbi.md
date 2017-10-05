---
title: "Painel do Power BI sobre a integridade do veículo e hábitos de condução - Azure | Microsoft Docs"
description: "Use os recursos do Cortana Intelligence para obter informações preditivas em tempo real sobre a integridade do veículo e hábitos de condução."
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
ms.openlocfilehash: f880aceb1657ffdfe909b73f175b9673d9ab02cd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="vehicle-telemetry-analytics-solution-template-power-bi-dashboard-setup-instructions"></a><span data-ttu-id="44265-103">Instruções de instalação do Painel de Power BI do modelo de solução de análise de telemetria do veículo</span><span class="sxs-lookup"><span data-stu-id="44265-103">Vehicle telemetry analytics solution template Power BI Dashboard setup instructions</span></span>
<span data-ttu-id="44265-104">Este **menu** fornece links para os capítulos deste manual.</span><span class="sxs-lookup"><span data-stu-id="44265-104">This **menu** links to the chapters in this playbook.</span></span> 

[!INCLUDE [cap-vehicle-telemetry-playbook-selector](../../includes/cap-vehicle-telemetry-playbook-selector.md)]

<span data-ttu-id="44265-105">A solução de análise de telemetria do veículo demonstra como revendedores de carros, fabricantes de automóveis e seguradoras podem aproveitar os recursos do Cortana Intelligence para obter uma visão em tempo real e uma previsão sobre a integridade do veículo e os hábitos de direção para promover melhorias na área do cliente, em pesquisa e desenvolvimento e em campanhas de marketing.</span><span class="sxs-lookup"><span data-stu-id="44265-105">The Vehicle Telemetry Analytics solution showcases how car dealerships, automobile manufacturers and insurance companies can leverage the capabilities of Cortana Intelligence to gain real-time and predictive insights on vehicle health and driving habits to drive improvements in the area of customer experience, R&D and marketing campaigns.</span></span> <span data-ttu-id="44265-106">Este documento contém instruções passo a passo de como você pode configurar os painéis e relatórios do Power BI depois que a solução é implantada na sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="44265-106">This document contains step by step instructions on how you can configure the Power BI reports and dashboard once the solution is deployed in your subscription.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="44265-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="44265-107">Prerequisites</span></span>
1. <span data-ttu-id="44265-108">Implantar a solução de [Análise de Telemetria](https://gallery.cortanaintelligence.com/Solution/5bdb23f3abb448268b7402ab8907cc90)</span><span class="sxs-lookup"><span data-stu-id="44265-108">Deploy the [Telemetry Analytics](https://gallery.cortanaintelligence.com/Solution/5bdb23f3abb448268b7402ab8907cc90) solution</span></span>  
2. [<span data-ttu-id="44265-109">Instalar o Microsoft Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="44265-109">Install Microsoft Power BI Desktop</span></span>](http://www.microsoft.com/download/details.aspx?id=45331)
3. <span data-ttu-id="44265-110">Uma [assinatura do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="44265-110">An [Azure subscription](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="44265-111">Se você não tiver uma assinatura do Azure, comece com uma assinatura gratuita do Azure</span><span class="sxs-lookup"><span data-stu-id="44265-111">If you don't have an Azure subscription, get started with Azure free subscription</span></span>
4. <span data-ttu-id="44265-112">Conta do Microsoft Power BI</span><span class="sxs-lookup"><span data-stu-id="44265-112">Microsoft Power BI account</span></span>

## <a name="cortana-intelligence-suite-components"></a><span data-ttu-id="44265-113">Componentes do Cortana Intelligence Suite</span><span class="sxs-lookup"><span data-stu-id="44265-113">Cortana Intelligence Suite Components</span></span>
<span data-ttu-id="44265-114">Como parte do modelo de solução de análise de telemetria de veículo, os serviços a seguir do Cortana Intelligence são implantados em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="44265-114">As part of the Vehicle Telemetry Analytics solution template, the following Cortana Intelligence services are deployed in your subscription.</span></span>

* <span data-ttu-id="44265-115">**Hubs de Eventos** para ingerir milhões de eventos de telemetria do veículos no Azure.</span><span class="sxs-lookup"><span data-stu-id="44265-115">**Event Hub** for ingesting millions of vehicle telemetry events into Azure.</span></span>
* <span data-ttu-id="44265-116">**Stream Analytics** para obter informações em tempo real sobre a integridade do veículo e persistir esses dados no armazenamento de longo prazo para uma análise de lote mais avançada.</span><span class="sxs-lookup"><span data-stu-id="44265-116">**Stream Analytics** for gaining real-time insights on vehicle health and persists that data into long-term storage for richer batch analytics.</span></span>
* <span data-ttu-id="44265-117">
            **Machine Learning** para detecção de anomalias em tempo real e processamento em lote para obter previsões.</span><span class="sxs-lookup"><span data-stu-id="44265-117">**Machine Learning** for anomaly detection in real-time and batch processing to gain predictive insights.</span></span>
* <span data-ttu-id="44265-118">**HDInsight** é utilizado para transformar dados em escala</span><span class="sxs-lookup"><span data-stu-id="44265-118">**HDInsight** is leveraged to transform data at scale</span></span>
* <span data-ttu-id="44265-119">**Data Factory** lida com a orquestração, o agendamento, o gerenciamento de recursos e o monitoramento do pipeline de processamento em lote.</span><span class="sxs-lookup"><span data-stu-id="44265-119">**Data Factory** handles orchestration, scheduling, resource management and monitoring of the batch processing pipeline.</span></span>

<span data-ttu-id="44265-120">**PowerBI** fornece essa solução a um painel avançado para os dados em tempo real e as visualizações da análise preditiva.</span><span class="sxs-lookup"><span data-stu-id="44265-120">**Power BI** gives this solution a rich dashboard for real-time data and predictive analytics visualizations.</span></span> 

<span data-ttu-id="44265-121">A solução usa duas fontes de dados diferentes: **Sinais de veículo simulados e conjunto de dados de diagnóstico** e **catálogo de veículo**.</span><span class="sxs-lookup"><span data-stu-id="44265-121">The solution uses two different data sources: **Simulated vehicle signals and diagnostic dataset** and **vehicle catalog**.</span></span>

<span data-ttu-id="44265-122">Um simulador de telemática do veículo é incluído como parte desta solução.</span><span class="sxs-lookup"><span data-stu-id="44265-122">A vehicle telematics simulator is included as part of this solution.</span></span> <span data-ttu-id="44265-123">Ele emite informações de diagnóstico e sinais correspondentes ao estado do veículo e ao padrão de condução em um determinado ponto no tempo.</span><span class="sxs-lookup"><span data-stu-id="44265-123">It emits diagnostic information and signals corresponding to the state of the vehicle and driving pattern at a given point in time.</span></span> 

<span data-ttu-id="44265-124">O Catálogo do veículo é um conjunto de dados de referência que contém um VIN para o mapeamento do modelo.</span><span class="sxs-lookup"><span data-stu-id="44265-124">The Vehicle Catalog is a reference dataset containing VIN to model mapping</span></span>

## <a name="power-bi-dashboard-preparation"></a><span data-ttu-id="44265-125">Preparação do Painel do Power BI</span><span class="sxs-lookup"><span data-stu-id="44265-125">Power BI Dashboard Preparation</span></span>
### <a name="setup-power-bi-real-time-dashboard"></a><span data-ttu-id="44265-126">Instalação do Painel do Power BI em tempo real</span><span class="sxs-lookup"><span data-stu-id="44265-126">Setup Power BI Real-Time Dashboard</span></span>

<span data-ttu-id="44265-127">**Iniciar o aplicativo de painel em tempo real** Depois que a implantação for concluída, você deve seguir as instruções de operação manual</span><span class="sxs-lookup"><span data-stu-id="44265-127">**Start the real-time dashboard application** Once the deployment is completed, you should follow the Manual Operation Instructions</span></span>

* <span data-ttu-id="44265-128">Baixe o aplicativo de painel em tempo real RealtimeDashboardApp.zip e descompacte-o.</span><span class="sxs-lookup"><span data-stu-id="44265-128">Download real-time dashboard application RealtimeDashboardApp.zip, and unzip it.</span></span>
*  <span data-ttu-id="44265-129">Na pasta descompactada, abra o arquivo de configuração do aplicativo “RealtimeDashboardApp.exe.config”, substitua appSettings por conexões de serviço de Eventhub, Armazenamento de Blobs e AM pelos valores nas instruções de operação manual e salve suas alterações.</span><span class="sxs-lookup"><span data-stu-id="44265-129">In the unzipped folder, open app config file 'RealtimeDashboardApp.exe.config', replace appSettings for Eventhub, Blob Storage, and ML service connections with the values in the Manual Operation Instructions, and save your changes.</span></span>
* <span data-ttu-id="44265-130">Execute o aplicativo RealtimeDashboardApp.exe.</span><span class="sxs-lookup"><span data-stu-id="44265-130">Run application RealtimeDashboardApp.exe.</span></span> <span data-ttu-id="44265-131">Uma janela de logon será mostrada, forneça suas credenciais válidas do Power BI e clique no botão **Aceitar**.</span><span class="sxs-lookup"><span data-stu-id="44265-131">A login window will pop up, provide your valid PowerBI credentials and click the **Accept** button.</span></span> <span data-ttu-id="44265-132">Em seguida, a execução do aplicativo começará.</span><span class="sxs-lookup"><span data-stu-id="44265-132">Then the app will start to run.</span></span>

   ![Entre no Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/5-sign-into-powerbi.png)
   
   ![Permissões do Painel do Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/6-powerbi-dashboard-permissions.png)

* <span data-ttu-id="44265-135">Faça logon no site do Power BI e crie um painel em tempo real.</span><span class="sxs-lookup"><span data-stu-id="44265-135">Login to PowerBI website, and create real-time dashboard.</span></span>

<span data-ttu-id="44265-136">Agora, você está pronto para configurar o painel do Power BI com visualizações avançadas para obter uma visão em tempo real e previsões sobre a integridade do veículo e os hábitos de direção.</span><span class="sxs-lookup"><span data-stu-id="44265-136">Now, you are ready to configure the Power BI dashboard with rich visualizations to gain real-time and predictive insights on vehicle health and driving habits.</span></span> <span data-ttu-id="44265-137">Demora aproximadamente 45 minutos a uma hora para a criação de todos os relatórios e configuração do painel.</span><span class="sxs-lookup"><span data-stu-id="44265-137">It takes about 45 minutes to an hour to create all the reports and configure the dashboard.</span></span> 

### <a name="configure-power-bi-reports"></a><span data-ttu-id="44265-138">Configurar relatórios do Power BI</span><span class="sxs-lookup"><span data-stu-id="44265-138">Configure Power BI reports</span></span>
<span data-ttu-id="44265-139">Os relatórios em tempo real e o painel demoram cerca de 30 a 45 minutos para serem concluídos.</span><span class="sxs-lookup"><span data-stu-id="44265-139">The real-time reports and the dashboard take about 30-45 minutes to complete.</span></span> <span data-ttu-id="44265-140">Navegue até [http://powerbi.com](http://powerbi.com) e faça logon.</span><span class="sxs-lookup"><span data-stu-id="44265-140">Browse to [http://powerbi.com](http://powerbi.com) and login.</span></span>

![Entre no Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/6-1-powerbi-signin.png)

<span data-ttu-id="44265-142">Um novo conjunto de dados é gerado no Power BI.</span><span class="sxs-lookup"><span data-stu-id="44265-142">A new dataset is generated in Power BI.</span></span> <span data-ttu-id="44265-143">Clique no conjunto de dados **ConnectedCarsRealtime** .</span><span class="sxs-lookup"><span data-stu-id="44265-143">Click the **ConnectedCarsRealtime** dataset.</span></span>

![Selecionar conjunto de dados de carros conectados em tempo real](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/7-select-connected-cars-realtime-dataset.png)

<span data-ttu-id="44265-145">Salve o relatório em branco usando **Ctrl + s**.</span><span class="sxs-lookup"><span data-stu-id="44265-145">Save the blank report using **Ctrl + s**.</span></span>

![Salvar relatório em branco](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/8-save-blank-report.png)

<span data-ttu-id="44265-147">Forneça o nome de relatório *Análise em tempo real de telemetria do veículo - Relatórios*.</span><span class="sxs-lookup"><span data-stu-id="44265-147">Provide report name *Vehicle Telemetry Analytics Real-time - Reports*.</span></span>

![Forneça o nome do relatório](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/9-provide-report-name.png)

## <a name="real-time-reports"></a><span data-ttu-id="44265-149">Relatórios em tempo real</span><span class="sxs-lookup"><span data-stu-id="44265-149">Real-time reports</span></span>
<span data-ttu-id="44265-150">Há três relatórios em tempo real nesta solução:</span><span class="sxs-lookup"><span data-stu-id="44265-150">There are three real-time reports in this solution:</span></span>

1. <span data-ttu-id="44265-151">Veículos em operação</span><span class="sxs-lookup"><span data-stu-id="44265-151">Vehicles in operation</span></span>
2. <span data-ttu-id="44265-152">Veículos que precisam de manutenção</span><span class="sxs-lookup"><span data-stu-id="44265-152">Vehicles Requiring Maintenance</span></span>
3. <span data-ttu-id="44265-153">Estatísticas de integridade de veículos</span><span class="sxs-lookup"><span data-stu-id="44265-153">Vehicles Health Statistics</span></span>

<span data-ttu-id="44265-154">Você pode escolher configurar todos os três relatórios em tempo real ou parar após qualquer estágio e prosseguir para a próxima seção da configuração dos relatórios em lote.</span><span class="sxs-lookup"><span data-stu-id="44265-154">You can choose to configure all the three real-time reports or stop after any stage and proceed to the next section of configuring the batch reports.</span></span> <span data-ttu-id="44265-155">Recomendamos que você crie todos os três relatórios para visualizar todas as informações do caminho da solução em tempo real.</span><span class="sxs-lookup"><span data-stu-id="44265-155">We recommend you to create all the three reports to visualize the full insights of the real-time path of the solution.</span></span>  

### <a name="1-vehicles-in-operation"></a><span data-ttu-id="44265-156">1. Veículos em operação</span><span class="sxs-lookup"><span data-stu-id="44265-156">1. Vehicles in operation</span></span>
<span data-ttu-id="44265-157">Clique duas vezes na **Página 1** e a renomeie como "Veículos em operação"</span><span class="sxs-lookup"><span data-stu-id="44265-157">Double-click **Page 1** and rename it to “Vehicles in operation”</span></span>  
    <span data-ttu-id="44265-158">![Carros conectados - Veículos em operação](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4a.png)</span><span class="sxs-lookup"><span data-stu-id="44265-158">![Connected Cars - Vehicles in operation](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4a.png)</span></span>  

<span data-ttu-id="44265-159">Selecione o campo **vin** em **Campos** e escolha o tipo de visualização como **"Placa"**.</span><span class="sxs-lookup"><span data-stu-id="44265-159">Select **vin** field from **Fields** and choose visualization type as **“Card”**.</span></span>  

<span data-ttu-id="44265-160">A visualização de placa é criada como mostrado na figura.</span><span class="sxs-lookup"><span data-stu-id="44265-160">Card visualization is created as shown in figure.</span></span>  
    ![Carros conectados - Selecione vin](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4b.png)

<span data-ttu-id="44265-162">Clique na área em branco para adicionar a nova visualização.</span><span class="sxs-lookup"><span data-stu-id="44265-162">Click the blank area to add new visualization.</span></span>  

<span data-ttu-id="44265-163">Selecione **Cidade** e **vin** nos campos.</span><span class="sxs-lookup"><span data-stu-id="44265-163">Select **City** and **vin** from fields.</span></span> <span data-ttu-id="44265-164">Altere a visualização para **"Mapa"**.</span><span class="sxs-lookup"><span data-stu-id="44265-164">Change visualization to **“Map”**.</span></span> <span data-ttu-id="44265-165">Arraste o **vin** na área de valores.</span><span class="sxs-lookup"><span data-stu-id="44265-165">Drag **vin** in values area.</span></span> <span data-ttu-id="44265-166">Arraste **cidade** de campos para a área **Legenda**.</span><span class="sxs-lookup"><span data-stu-id="44265-166">Drag **city** from fields to **Legend** area.</span></span>   
    <span data-ttu-id="44265-167">![Carros conectados - Visualização da placa](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4c.png)</span><span class="sxs-lookup"><span data-stu-id="44265-167">![Connected Cars - Card Visualization](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4c.png)</span></span>

<span data-ttu-id="44265-168">Selecione a seção **formato** em **Visualizações**, clique em **Título** e altere o **Texto** para **"Veículos em operação por cidade"**.</span><span class="sxs-lookup"><span data-stu-id="44265-168">Select **format** section from **Visualizations**, click **Title** and change the **Text** to **“Vehicles in operation by city”**.</span></span>  
    <span data-ttu-id="44265-169">![Carros conectados - Veículos em operação por cidade](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4d.png)</span><span class="sxs-lookup"><span data-stu-id="44265-169">![Connected Cars - Vehicles in operation by city](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4d.png)</span></span>   

<span data-ttu-id="44265-170">A visualização final será como mostrado na figura.</span><span class="sxs-lookup"><span data-stu-id="44265-170">Final visualization looks as shown in figure.</span></span>    
    ![Carros conectados - Visualização final](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4e.png)

<span data-ttu-id="44265-172">Clique na área em branco para adicionar a nova visualização.</span><span class="sxs-lookup"><span data-stu-id="44265-172">Click the blank area to add new visualization.</span></span>  

<span data-ttu-id="44265-173">Selecione **Cidade** e **vin**, altere o tipo de visualização para **Gráfico de coluna clusterizada**.</span><span class="sxs-lookup"><span data-stu-id="44265-173">Select **City** and **vin**, change visualization type to **Clustered Column Chart**.</span></span> <span data-ttu-id="44265-174">Certifique-se de que o campo **Cidade** está na **Área do eixo** e o **vin** está na **Área do valor**</span><span class="sxs-lookup"><span data-stu-id="44265-174">Ensure **City** field in **Axis area** and **vin** in **Value area**</span></span>  

<span data-ttu-id="44265-175">Classificar gráfico por **"Contagem de vin"**</span><span class="sxs-lookup"><span data-stu-id="44265-175">Sort chart by **“Count of vin”**</span></span>  
    <span data-ttu-id="44265-176">![Carros conectados - Contagem de vin](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4f.png)</span><span class="sxs-lookup"><span data-stu-id="44265-176">![Connected Cars - Count of vin](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4f.png)</span></span>  

<span data-ttu-id="44265-177">Alterar **Título** do gráfico para **"Veículos em operação por cidade"**</span><span class="sxs-lookup"><span data-stu-id="44265-177">Change chart **Title** to **“Vehicles in operation by city”**</span></span>  

<span data-ttu-id="44265-178">Clique na seção **Formato**, selecione **Cores dos Dados**, clique em **"Ativada"** para **Mostrar Tudo**</span><span class="sxs-lookup"><span data-stu-id="44265-178">Click the **Format** section, then select **Data Colors**,  Click the **“On”** to **Show All**</span></span>  
    <span data-ttu-id="44265-179">![Carros conectados - Mostrar todas as cores de dados](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4g.png)</span><span class="sxs-lookup"><span data-stu-id="44265-179">![Connected Cars - Show all Data Colors](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4g.png)</span></span>  

<span data-ttu-id="44265-180">Altere a cor de uma cidade específica, clicando no ícone de cor.</span><span class="sxs-lookup"><span data-stu-id="44265-180">Change the color of individual city by clicking on color icon.</span></span>  
    ![Carros conectados - Alterar cores](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4h.png)  

<span data-ttu-id="44265-182">Clique na área em branco para adicionar a nova visualização.</span><span class="sxs-lookup"><span data-stu-id="44265-182">Click the blank area to add new visualization.</span></span>  

<span data-ttu-id="44265-183">Selecione a visualização **Gráfico de Coluna Clusterizada** nas visualizações, arraste o campo **cidade** para a área do **Eixo**, **Modelo** para a área de **Legenda** e **vin** para a área **Valor**.</span><span class="sxs-lookup"><span data-stu-id="44265-183">Select **Clustered Column Chart** visualization from visualizations, drag **city** field in **Axis** area, **Model** in **Legend** area and **vin** in **Value** area.</span></span>  
    <span data-ttu-id="44265-184">![Carros conectados - Gráfico de colunas agrupadas](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4i.png)</span><span class="sxs-lookup"><span data-stu-id="44265-184">![Connected Cars - Clustered Column Chart](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4i.png)</span></span>  
    <span data-ttu-id="44265-185">![Carros conectados - Renderização](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4j.png)</span><span class="sxs-lookup"><span data-stu-id="44265-185">![Connected Cars - Rendering](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4j.png)</span></span>

<span data-ttu-id="44265-186">Reorganize todas as visualizações nesta página conforme mostrado na figura.</span><span class="sxs-lookup"><span data-stu-id="44265-186">Rearrange all visualization on this page as shown in figure.</span></span>  
    ![Carros conectados - Visualizações](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4k.png)

<span data-ttu-id="44265-188">Você configurou com êxito o relatório em tempo real "Veículos em operação".</span><span class="sxs-lookup"><span data-stu-id="44265-188">You have successfully configured the “Vehicles in operation” real-time report.</span></span> <span data-ttu-id="44265-189">Você pode continuar e criar o próximo relatório em tempo real ou parar aqui e configurar o painel.</span><span class="sxs-lookup"><span data-stu-id="44265-189">You can proceed to create the next real-time report or stop here and configure the dashboard.</span></span> 

### <a name="2-vehicles-requiring-maintenance"></a><span data-ttu-id="44265-190">2. Veículos que precisam de manutenção</span><span class="sxs-lookup"><span data-stu-id="44265-190">2. Vehicles Requiring Maintenance</span></span>
<span data-ttu-id="44265-191">Clique em ![Adicionar](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) para adicionar um novo relatório, renomeie-o como **"Veículos que precisam de manutenção"**</span><span class="sxs-lookup"><span data-stu-id="44265-191">Click ![Add](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) to add a new report, rename it to **“Vehicles Requiring Maintenance”**</span></span>

![Carros conectados - Veículos que precisam de manutenção](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4l.png)  

<span data-ttu-id="44265-193">Selecione o campo **vin** e altere o tipo de visualização para **Placa**.</span><span class="sxs-lookup"><span data-stu-id="44265-193">Select **vin** field and change visualization type to **Card**.</span></span>  
    <span data-ttu-id="44265-194">![Carros conectados - Visualização da placa do vin](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4m.png)</span><span class="sxs-lookup"><span data-stu-id="44265-194">![Connected Cars - Vin Card Visualization](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4m.png)</span></span>  

<span data-ttu-id="44265-195">Temos um campo chamado "MaintenanceLabel", no conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="44265-195">We have a field named “MaintenanceLabel” In the dataset.</span></span> <span data-ttu-id="44265-196">Esse campo pode ter um valor “0” ou “1”.</span><span class="sxs-lookup"><span data-stu-id="44265-196">This field can have a value of “0” or “1”.”</span></span> <span data-ttu-id="44265-197">Ele é definido pelo modelo de Azure Machine Learning provisionado como parte da solução e integrado ao caminho em tempo real.</span><span class="sxs-lookup"><span data-stu-id="44265-197">It is set by the Azure Machine Learning model provisioned as part of solution and integrated with the real-time path.</span></span> <span data-ttu-id="44265-198">O valor "1" indica que um veículo requer manutenção.</span><span class="sxs-lookup"><span data-stu-id="44265-198">The value “1” indicates a vehicle requires maintenance.</span></span> 

<span data-ttu-id="44265-199">Para adicionar um filtro de **Página** para mostrar os dados de veículos que necessitam de manutenção:</span><span class="sxs-lookup"><span data-stu-id="44265-199">To add a **Page Level** filter for showing vehicles data, which are requiring maintenance:</span></span> 

1. <span data-ttu-id="44265-200">Arraste o campo **"MaintenanceLabel"** para dentro dos **Filtros de página**.</span><span class="sxs-lookup"><span data-stu-id="44265-200">Drag the **“MaintenanceLabel”** field into **Page Level Filters**.</span></span>  
   <span data-ttu-id="44265-201">![Carros conectados - Filtros de página](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n1.png)</span><span class="sxs-lookup"><span data-stu-id="44265-201">![Connected Cars - Page Level Filters](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n1.png)</span></span>  
2. <span data-ttu-id="44265-202">Clique no menu **Filtragem Básica** presente na parte inferior do Filtro de página MaintenanceLabel.</span><span class="sxs-lookup"><span data-stu-id="44265-202">Click **Basic Filtering** menu present at bottom of MaintenanceLabel Page Level Filter.</span></span>  
   <span data-ttu-id="44265-203">![Carros conectados - Filtragem básica](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n2.png)</span><span class="sxs-lookup"><span data-stu-id="44265-203">![Connected Cars - Basic Filtering](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n2.png)</span></span>  
3. <span data-ttu-id="44265-204">Defina o valor do filtro como **"1"**  </span><span class="sxs-lookup"><span data-stu-id="44265-204">Set its filter value to **“1”**  </span></span>  
   <span data-ttu-id="44265-205">![Carros conectados - Valor do filtro](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n3.png)</span><span class="sxs-lookup"><span data-stu-id="44265-205">![Connected Cars - Filter Value](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4n3.png)</span></span>  

<span data-ttu-id="44265-206">Clique na área em branco para adicionar a nova visualização.</span><span class="sxs-lookup"><span data-stu-id="44265-206">Click the blank area to add new visualization.</span></span>  

<span data-ttu-id="44265-207">Selecione o **Gráfico de Coluna Clusterizada** das visualizações</span><span class="sxs-lookup"><span data-stu-id="44265-207">Select **Clustered Column Chart** from visualizations</span></span>  
<span data-ttu-id="44265-208">![Carros conectados - Visualização da placa do vind](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4o.png)</span><span class="sxs-lookup"><span data-stu-id="44265-208">![Connected Cars - Vind Card Visualization](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4o.png)</span></span>  
<span data-ttu-id="44265-209">![Carros conectados - Gráfico de colunas agrupadas](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4p.png)</span><span class="sxs-lookup"><span data-stu-id="44265-209">![Connected Cars - Clustered Column Chart](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4p.png)</span></span>

<span data-ttu-id="44265-210">Arraste o campo **Modelo** para a área de **Eixo**, **Vin** para a área de **Valor**.</span><span class="sxs-lookup"><span data-stu-id="44265-210">Drag field **Model** into **Axis** area, **Vin** to **Value** area.</span></span> <span data-ttu-id="44265-211">Em seguida, classifique visualização por **Contagem de vin**.</span><span class="sxs-lookup"><span data-stu-id="44265-211">Then sort visualization by **Count of vin**.</span></span>  <span data-ttu-id="44265-212">Alterar o **Título** do gráfico **"Veículos que exigem manutenção pelo modelo"**</span><span class="sxs-lookup"><span data-stu-id="44265-212">Change chart **Title** to **“Vehicles requiring maintenance by model”**</span></span>  

<span data-ttu-id="44265-213">Arraste os campos **vin** para a **Saturação da cor** presente na seção **Campos**![Fields](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4field.png) da guia **Visualização**</span><span class="sxs-lookup"><span data-stu-id="44265-213">Drag **vin** fields into **Color Saturation** present at **Fields** ![Fields](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4field.png) section of **Visualization** tab</span></span>  
<span data-ttu-id="44265-214">![Carros conectados - Saturação de cor](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4q.png)</span><span class="sxs-lookup"><span data-stu-id="44265-214">![Connected Cars - Color Saturation](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4q.png)</span></span>  

<span data-ttu-id="44265-215">Alterar **Cores dos Dados** nas visualizações na seção **Formato**</span><span class="sxs-lookup"><span data-stu-id="44265-215">Change **Data Colors** in visualizations from **Format** section</span></span>  
<span data-ttu-id="44265-216">Alterar a cor do Mínimo para: **F2C812**</span><span class="sxs-lookup"><span data-stu-id="44265-216">Change Minimum color to: **F2C812**</span></span>  
<span data-ttu-id="44265-217">Alterar a cor do Máximo para: **FF6300**</span><span class="sxs-lookup"><span data-stu-id="44265-217">Change Maximum color to: **FF6300**</span></span>  
<span data-ttu-id="44265-218">![Carros conectados - Alterações de cor](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4r.png)</span><span class="sxs-lookup"><span data-stu-id="44265-218">![Connected Cars - Color Changes](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4r.png)</span></span>  
<span data-ttu-id="44265-219">![Carros conectados - Novas cores de visualização](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4s.png)</span><span class="sxs-lookup"><span data-stu-id="44265-219">![Connected Cars - New Visualization Colors](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4s.png)</span></span>  

<span data-ttu-id="44265-220">Clique na área em branco para adicionar a nova visualização.</span><span class="sxs-lookup"><span data-stu-id="44265-220">Click the blank area to add new visualization.</span></span>  

<span data-ttu-id="44265-221">Selecione **Gráfico de colunas clusterizado** das visualizações, arraste o campo **vin** para a área **Valor**, arraste o campo **Cidade** para a área **Eixo**.</span><span class="sxs-lookup"><span data-stu-id="44265-221">Select **Clustered column chart** from visualizations, drag **vin** field into **Value** area, drag **City** field into **Axis** area.</span></span> <span data-ttu-id="44265-222">Classificar gráfico por **"Contagem de vin"**.</span><span class="sxs-lookup"><span data-stu-id="44265-222">Sort chart by **“Count of vin”**.</span></span> <span data-ttu-id="44265-223">Altere o **Título** do gráfico **"Veículos que exigem manutenção por cidade"** </span><span class="sxs-lookup"><span data-stu-id="44265-223">Change chart **Title** to **“Vehicles requiring maintenance by city”** </span></span>  
<span data-ttu-id="44265-224">![Carros conectados - Veículos que precisam de manutenção por cidade](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4t.png)</span><span class="sxs-lookup"><span data-stu-id="44265-224">![Connected Cars - Vehicles requiring maintenance by city](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4t.png)</span></span>  

<span data-ttu-id="44265-225">Clique na área em branco para adicionar a nova visualização.</span><span class="sxs-lookup"><span data-stu-id="44265-225">Click the blank area to add new visualization.</span></span>  

<span data-ttu-id="44265-226">Selecione a visualização **Placa com várias linhas** em visualizações, arraste **Modelo** e **vin** para a área **Campos**.</span><span class="sxs-lookup"><span data-stu-id="44265-226">Select **Multi-Row Card** visualization from visualizations, drag **Model** and **vin** into the **Fields** area.</span></span>  
<span data-ttu-id="44265-227">![Carros conectados - Placa com várias linhas](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4u.png)</span><span class="sxs-lookup"><span data-stu-id="44265-227">![Connected Cars - Multi-Row Card](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4u.png)</span></span>    

<span data-ttu-id="44265-228">Reorganizando toda a visualização, o relatório final terá esta aparência: </span><span class="sxs-lookup"><span data-stu-id="44265-228">Rearranging all of the visualization, the final report looks as follows:</span></span>  
![Carros conectados - Placa com várias linhas](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4v.png)  

<span data-ttu-id="44265-230">Você configurou com êxito o relatório em tempo real "Veículos que precisam de manutenção".</span><span class="sxs-lookup"><span data-stu-id="44265-230">You have successfully configured the “Vehicles Requiring Maintenance” real-time report.</span></span> <span data-ttu-id="44265-231">Você pode continuar e criar o próximo relatório em tempo real ou parar aqui e configurar o painel.</span><span class="sxs-lookup"><span data-stu-id="44265-231">You can proceed to create the next real-time report or stop here and configure the dashboard.</span></span> 

### <a name="3-vehicles-health-statistics"></a><span data-ttu-id="44265-232">3. Estatísticas de integridade de veículos</span><span class="sxs-lookup"><span data-stu-id="44265-232">3. Vehicles Health Statistics</span></span>
<span data-ttu-id="44265-233">Clique em ![Adicionar](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) para adicionar um novo relatório, renomeie-o para **"Estatísticas de integridade de veículos"**</span><span class="sxs-lookup"><span data-stu-id="44265-233">Click ![Add](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4add.png) to add new report, rename it to **“Vehicles Health Statistics”**</span></span>  

<span data-ttu-id="44265-234">Selecione a visualização **Medidor** em visualizações, arraste o campo **Velocidade** para as áreas **Valor, Valor Mínimo, Valor Máximo**.</span><span class="sxs-lookup"><span data-stu-id="44265-234">Select **Gauge** visualization from visualizations, then drag the **Speed** field into **Value, Minimum Value, Maximum Value** areas.</span></span>  
<span data-ttu-id="44265-235">![Carros conectados - Placa com várias linhas](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4w.png)</span><span class="sxs-lookup"><span data-stu-id="44265-235">![Connected Cars - Multi-Row Card](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4w.png)</span></span>  

<span data-ttu-id="44265-236">Alterar a agregação padrão de **velocidade** na **Área de valor** para **Média**</span><span class="sxs-lookup"><span data-stu-id="44265-236">Change the default aggregation of **speed** in **Value area** to **Average**</span></span> 

<span data-ttu-id="44265-237">Alterar a agregação padrão de **velocidade** na **Área mínima** para **Mínima**</span><span class="sxs-lookup"><span data-stu-id="44265-237">Change the default aggregation of **speed** in **Minimum area** to **Minimum**</span></span>

<span data-ttu-id="44265-238">Alterar a agregação padrão de **velocidade** na **Área máxima** para **Máxima**</span><span class="sxs-lookup"><span data-stu-id="44265-238">Change the default aggregation of **speed** in **Maximum area** to **Maximum**</span></span>

![Carros conectados - Placa com várias linhas](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4x.png)  

<span data-ttu-id="44265-240">Renomeie o **Título do Medidor** para **"Velocidade média"**</span><span class="sxs-lookup"><span data-stu-id="44265-240">Rename the **Gauge Title** to **“Average speed”**</span></span> 

![Carros conectados - Medidor](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4y.png)  

<span data-ttu-id="44265-242">Clique na área em branco para adicionar a nova visualização.</span><span class="sxs-lookup"><span data-stu-id="44265-242">Click the blank area to add new visualization.</span></span>  

<span data-ttu-id="44265-243">Da mesma forma, adicione um **Medidor** para **média de óleo do motor**, **média de combustível** e **temperatura média do motor**.</span><span class="sxs-lookup"><span data-stu-id="44265-243">Similarly add a **Gauge** for **average engine oil**, **average fuel**, and **average engine temperate**.</span></span>  

<span data-ttu-id="44265-244">Altere a agregação padrão dos campos em cada medidor conforme as etapas acima no medidor de **"Velocidade média"** .</span><span class="sxs-lookup"><span data-stu-id="44265-244">Change the default aggregation of fields in each gauge as per above steps in **“Average speed”** gauge.</span></span>

![Carros conectados - Medidores](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4z.png)

<span data-ttu-id="44265-246">Clique na área em branco para adicionar a nova visualização.</span><span class="sxs-lookup"><span data-stu-id="44265-246">Click the blank area to add new visualization.</span></span>

<span data-ttu-id="44265-247">Selecione **Gráfico de coluna e linha clusterizado** em visualizações, arraste o campo **Cidade** para o **Eixo compartilhado**, arraste os campos **velocidade**, **pressãodopneu** e **óleodomotor** para a área Valores de Coluna e altere o tipo de agregação para **Média**.</span><span class="sxs-lookup"><span data-stu-id="44265-247">Select **Line and Clustered Column Chart** from visualizations, then drag **City** field into **Shared Axis**, drag **speed**, **tirepressure and engineoil fields** into **Column Values** area, change their aggregation type to **Average**.</span></span> 

<span data-ttu-id="44265-248">Arraste o campo **temperaturadoMotor** para a área **Valores de Linha**, altere o tipo de agregação para **Média**.</span><span class="sxs-lookup"><span data-stu-id="44265-248">Drag the **engineTemperature** field into **Line Values** area, change the  aggregation type to **Average**.</span></span> 

![Carros conectados - Campos de visualizações](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4aa.png)

<span data-ttu-id="44265-250">Altere o **Título** do gráfico para **"Velocidade média, pressão do pneu, óleo do motor e temperatura do motor"**.</span><span class="sxs-lookup"><span data-stu-id="44265-250">Change the chart **Title** to **“Average speed, tire pressure, engine oil and engine temperature”**.</span></span>  

![Carros conectados - Campos de visualizações](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4bb.png)

<span data-ttu-id="44265-252">Clique na área em branco para adicionar a nova visualização.</span><span class="sxs-lookup"><span data-stu-id="44265-252">Click the blank area to add new visualization.</span></span>

<span data-ttu-id="44265-253">Selecione a visualização **Treemap** nas visualizações, arraste o campo **Modelo** para a área **Grupo** e arraste o campo **ProbabilidadeDeManutenção** para a área de **Valores**.</span><span class="sxs-lookup"><span data-stu-id="44265-253">Select **Treemap** visualization from visualizations, drag the **Model** field into the **Group** area, and drag the field **MaintenanceProbability** into the **Values** area.</span></span>

<span data-ttu-id="44265-254">Altere o **Título do gráfico** para **"Modelos de veículo que exigem manutenção"**.</span><span class="sxs-lookup"><span data-stu-id="44265-254">Change the chart **Title** to **“Vehicle models requiring maintenance”**.</span></span>

![Carros conectados - Alterar título do gráfico](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4cc.png)

<span data-ttu-id="44265-256">Clique na área em branco para adicionar a nova visualização.</span><span class="sxs-lookup"><span data-stu-id="44265-256">Click the blank area to add new visualization.</span></span>

<span data-ttu-id="44265-257">Selecione **Gráfico de barras empilhadas 100%** na visualização, arraste o campo **cidade** para a área de **Eixo** e arraste os campos **ProbabilidadeDeManutenção**, **ProbabilidadeDeRecall** para a área **Valor**.</span><span class="sxs-lookup"><span data-stu-id="44265-257">Select **100% Stacked Bar Chart** from visualization, drag the **city** field into the **Axis** area, and drag the **MaintenanceProbability**, **RecallProbability** fields into the **Value** area.</span></span>

![Carros conectados - Adicionar nova visualização](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4dd.png)

<span data-ttu-id="44265-259">Clique em **Formato**, selecione **Cores dos Dados**, altere a cor **ProbabilidadeDeManutenção** para o valor **"F2C80F"**.</span><span class="sxs-lookup"><span data-stu-id="44265-259">Click **Format**, select **Data Colors**, and set the **MaintenanceProbability** color to the value **“F2C80F”**.</span></span>

<span data-ttu-id="44265-260">Altere o **Título** do gráfico para **"Probabilidade de manutenção e recall do veículo por cidade"**.</span><span class="sxs-lookup"><span data-stu-id="44265-260">Change the **Title** of the chart to **“Probability of Vehicle Maintenance & Recall by City”**.</span></span>

![Carros conectados - Adicionar nova visualização](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4ee.png)

<span data-ttu-id="44265-262">Clique na área em branco para adicionar a nova visualização.</span><span class="sxs-lookup"><span data-stu-id="44265-262">Click the blank area to add new visualization.</span></span>

<span data-ttu-id="44265-263">Selecione o **Gráfico de Área** na visualização em visualizações, arraste o campo **Modelo** para a área do **Eixo** e arraste os campos **óleodoMotor, pressãodopneu, velocidade e ProbabilidadeDeManutenção** para a área **Valores**.</span><span class="sxs-lookup"><span data-stu-id="44265-263">Select **Area Chart** from visualization from visualizations, drag the **Model** field into the **Axis** area, and drag the **engineOil, tirepressure, speed and MaintenanceProbability** fields into the **Values** area.</span></span> <span data-ttu-id="44265-264">Altere o tipo de agregação para **"Média"**.</span><span class="sxs-lookup"><span data-stu-id="44265-264">Change their aggregation type to **“Average”**.</span></span> 

![Carros conectados - Alterar tipo de agregação](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4ff.png)

<span data-ttu-id="44265-266">Altere o Título do gráfico para **"Média do óleo do motor, pressão do pneu, velocidade e probabilidade de manutenção por modelo"**.</span><span class="sxs-lookup"><span data-stu-id="44265-266">Change the title of the chart to **“Average engine oil, tire pressure, speed and maintenance probability by model”**.</span></span>

![Carros conectados - Alterar título do gráfico](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4gg.png)

<span data-ttu-id="44265-268">Clique na área em branco para adicionar a nova visualização:</span><span class="sxs-lookup"><span data-stu-id="44265-268">Click the blank area to add new visualization:</span></span>

1. <span data-ttu-id="44265-269">Selecione a visualização **Gráfico de Dispersão** em visualizações.</span><span class="sxs-lookup"><span data-stu-id="44265-269">Select **Scatter Chart** visualization from visualizations.</span></span>
2. <span data-ttu-id="44265-270">Arraste o campo **Modelo** para a área de **Detalhes** e **Legenda**.</span><span class="sxs-lookup"><span data-stu-id="44265-270">Drag the **Model** field into the **Details** and **Legend** area.</span></span>
3. <span data-ttu-id="44265-271">Arraste o campo **combustível** para a área **Eixo X**, altere a agregação para **Média**.</span><span class="sxs-lookup"><span data-stu-id="44265-271">Drag the **fuel** field into the **X-Axis** area, change the aggregation to **Average**.</span></span>
4. <span data-ttu-id="44265-272">Arraste **temperaturadoMotor** para a área **Eixo Y**, altere a agregação para **Média**</span><span class="sxs-lookup"><span data-stu-id="44265-272">Drag **engineTemparature** into **Y-Axis area**, change the aggregation to **Average**</span></span>
5. <span data-ttu-id="44265-273">Arraste o campo **vin** para a área **Tamanho**.</span><span class="sxs-lookup"><span data-stu-id="44265-273">Drag the **vin** field into the **Size** area.</span></span>

![Carros conectados - Adicionar nova visualização](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4hh.png)

<span data-ttu-id="44265-275">Altere o **Título** do gráfico para **"Médias de combustível, temperatura do motor por modelo"**.</span><span class="sxs-lookup"><span data-stu-id="44265-275">Change the chart **Title** to **“Averages of Fuel, Engine Temperature by Model”**.</span></span>

![Carros conectados - Alterar título do gráfico](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4ii.png)

<span data-ttu-id="44265-277">O relatório final será semelhante ao mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="44265-277">The final report will look like as shown below.</span></span>

![Carros conectados-Relatório final](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.4jj.png)

### <a name="pin-visualizations-from-the-reports-to-the-real-time-dashboard"></a><span data-ttu-id="44265-279">Fixar visualizações de relatórios para o painel em tempo real</span><span class="sxs-lookup"><span data-stu-id="44265-279">Pin visualizations from the reports to the real-time dashboard</span></span>
<span data-ttu-id="44265-280">Crie um painel em branco clicando no sinal de adição ao lado dos Painéis.</span><span class="sxs-lookup"><span data-stu-id="44265-280">Create a blank dashboard by clicking on the plus icon next to Dashboards.</span></span> <span data-ttu-id="44265-281">Você pode chamá-lo de "Painel de análise de telemetria do veículo"</span><span class="sxs-lookup"><span data-stu-id="44265-281">You can name it “Vehicle Telemetry Analytics Dashboard”</span></span>

![Carros conectados-Painel](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.5.png)

<span data-ttu-id="44265-283">Fixe a visualização dos relatórios acima no painel.</span><span class="sxs-lookup"><span data-stu-id="44265-283">Pin the visualization from the above reports to the dashboard.</span></span> 

![Carros conectados-Painel](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-3.6.png)

<span data-ttu-id="44265-285">O painel deve ter a aparência a seguir quando todos os três relatórios tiverem sido criados e as visualizações correspondentes estiverem fixadas no painel.</span><span class="sxs-lookup"><span data-stu-id="44265-285">The dashboard should look as follows when all the three reports are created and the corresponding visualizations are pinned to the dashboard.</span></span> <span data-ttu-id="44265-286">Se você não tiver criado todos os relatórios, o painel poderá parecer diferente .</span><span class="sxs-lookup"><span data-stu-id="44265-286">If you have not created all the reports, your dashboard could look different.</span></span> 

![Carros conectados-Painel](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/connected-cars-4.0.png)

<span data-ttu-id="44265-288">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="44265-288">Congratulations!</span></span> <span data-ttu-id="44265-289">Você criou o painel em tempo real.</span><span class="sxs-lookup"><span data-stu-id="44265-289">You have successfully created the real-time dashboard.</span></span> <span data-ttu-id="44265-290">Durante a execução de CarEventGenerator.exe e RealtimeDashboardApp.exe, você verá atualizações dinâmicas no painel.</span><span class="sxs-lookup"><span data-stu-id="44265-290">As you continue to execute CarEventGenerator.exe and RealtimeDashboardApp.exe, you should see live updates on the dashboard.</span></span> <span data-ttu-id="44265-291">Deve demorar cerca de 10 a 15 minutos para concluir as etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="44265-291">It should take about 10 to 15 minutes to complete the following steps.</span></span>

## <a name="setup-power-bi-batch-processing-dashboard"></a><span data-ttu-id="44265-292">Instalação do painel de processamento em lote do Power BI</span><span class="sxs-lookup"><span data-stu-id="44265-292">Setup Power BI batch processing dashboard</span></span>
> [!NOTE]
> <span data-ttu-id="44265-293">Demora cerca de duas horas (após a conclusão bem-sucedida da implantação) para concluir a execução da pipeline de processamento em lote de ponta a ponta e processar um ano de dados gerados.</span><span class="sxs-lookup"><span data-stu-id="44265-293">It takes about two hours (from the successful completion of the deployment) for the end to end batch processing pipeline to finish execution and process a year worth of generated data.</span></span> <span data-ttu-id="44265-294">Aguarde até que o processamento seja concluído antes de prosseguir para as próximas etapas.</span><span class="sxs-lookup"><span data-stu-id="44265-294">So wait for the processing to finish before proceeding with the next steps.</span></span> 
> 
> 

<span data-ttu-id="44265-295">**Baixe o arquivo de designer do Power BI**</span><span class="sxs-lookup"><span data-stu-id="44265-295">**Download the Power BI designer file**</span></span>

* <span data-ttu-id="44265-296">Um arquivo de designer pré-configurado do Power BI é incluído como parte das instruções de operação manual de implantação</span><span class="sxs-lookup"><span data-stu-id="44265-296">A pre-configured Power BI designer file is included as part of the deployment Manual Operation Instructions</span></span>
* <span data-ttu-id="44265-297">Procure por 2.</span><span class="sxs-lookup"><span data-stu-id="44265-297">Look for 2.</span></span> <span data-ttu-id="44265-298">Instalar o painel de processamento em lote do PowerBI Baixe o modelo do Power BI para o painel de processamento em lote chamado **ConnectedCarsPbiReport.pbix**.</span><span class="sxs-lookup"><span data-stu-id="44265-298">Setup PowerBI batch processing dashboard You can download the PowerBI template for batch processing dashboard here called **ConnectedCarsPbiReport.pbix**.</span></span>
* <span data-ttu-id="44265-299">Salve localmente</span><span class="sxs-lookup"><span data-stu-id="44265-299">Save locally</span></span>

<span data-ttu-id="44265-300">**Configurar relatórios do Power BI**</span><span class="sxs-lookup"><span data-stu-id="44265-300">**Configure Power BI reports**</span></span>

* <span data-ttu-id="44265-301">Abra o arquivo de designer “**ConnectedCarsPbiReport.pbix**” usando o Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="44265-301">Open the designer file ‘**ConnectedCarsPbiReport.pbix**’ using Power BI Desktop.</span></span> <span data-ttu-id="44265-302">Caso ainda não tenha feito isso, instale o Power BI Desktop de [Instalar Power BI Desktop](http://www.microsoft.com/download/details.aspx?id=45331).</span><span class="sxs-lookup"><span data-stu-id="44265-302">If you do not already have, install the Power BI Desktop from [Power BI Desktop install](http://www.microsoft.com/download/details.aspx?id=45331).</span></span> 
* <span data-ttu-id="44265-303">Clique em **Editar Consultas**.</span><span class="sxs-lookup"><span data-stu-id="44265-303">Click the **Edit Queries**.</span></span>

![Editar consulta do Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/10-edit-powerbi-query.png)

* <span data-ttu-id="44265-305">Clique duas vezes na **Origem**.</span><span class="sxs-lookup"><span data-stu-id="44265-305">Double-click the **Source**.</span></span>

![Definir origem do Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/11-set-powerbi-source.png)

* <span data-ttu-id="44265-307">Atualize a cadeia de conexão do servidor com o servidor do SQL Azure provisionado como parte da implantação.</span><span class="sxs-lookup"><span data-stu-id="44265-307">Update Server connection string with the Azure SQL server that got provisioned as part of the deployment.</span></span>  <span data-ttu-id="44265-308">Examine as instruções de operação manual em</span><span class="sxs-lookup"><span data-stu-id="44265-308">Look in the Manual Operation Instructions under</span></span> 

    4. <span data-ttu-id="44265-309">Banco de Dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="44265-309">Azure SQL Database</span></span>
    
    * <span data-ttu-id="44265-310">Servidor: somethingsrv.database.windows.net</span><span class="sxs-lookup"><span data-stu-id="44265-310">Server: somethingsrv.database.windows.net</span></span>
    * <span data-ttu-id="44265-311">Banco de dados: connectedcar</span><span class="sxs-lookup"><span data-stu-id="44265-311">Database: connectedcar</span></span>
    * <span data-ttu-id="44265-312">Nome de usuário: username</span><span class="sxs-lookup"><span data-stu-id="44265-312">Username: username</span></span>
    * <span data-ttu-id="44265-313">Senha: gerencie sua senha do SQL Server no Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="44265-313">Password: You can manage your SQL server password from Azure portal</span></span>

* <span data-ttu-id="44265-314">Deixe **Banco de dados** como *connectedcar*.</span><span class="sxs-lookup"><span data-stu-id="44265-314">Leave **Database** as *connectedcar*.</span></span>

![Definir banco de dados do Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/12-set-powerbi-database.png)

* <span data-ttu-id="44265-316">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="44265-316">Click **OK**.</span></span>
* <span data-ttu-id="44265-317">Você verá a guia **Credencial do Windows** selecionada por padrão, altere-a para **Credenciais de banco de dados** clicando na guia **Banco de Dados** no lado direito.</span><span class="sxs-lookup"><span data-stu-id="44265-317">You will see **Windows credential** tab selected by default, change it to **Database credentials** by clicking on **Database** tab at right.</span></span>
* <span data-ttu-id="44265-318">Forneça o **Nome de usuário** e a **Senha** de seu Banco de Dados SQL do Azure especificado durante a configuração da implantação.</span><span class="sxs-lookup"><span data-stu-id="44265-318">Provide the **Username** and **Password** of your Azure SQL Database that was specified during its deployment setup.</span></span>

![Forneça as credenciais do banco de dados](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/13-provide-database-credentials.png)

* <span data-ttu-id="44265-320">Clique em **Conectar**</span><span class="sxs-lookup"><span data-stu-id="44265-320">Click **Connect**</span></span>
* <span data-ttu-id="44265-321">Repita as etapas acima para cada uma das 3 consultas restantes presentes no painel direito e atualize os detalhes de conexão da fonte de dados.</span><span class="sxs-lookup"><span data-stu-id="44265-321">Repeat the above steps for each of the three remaining queries present at right pane, and then update the data source connection details.</span></span>
* <span data-ttu-id="44265-322">Clique em **Fechar e Carregar**.</span><span class="sxs-lookup"><span data-stu-id="44265-322">Click **Close and Load**.</span></span> <span data-ttu-id="44265-323">Os conjuntos de dados de arquivo do Power BI Desktop são conectados às tabelas de banco de dados do SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="44265-323">Power BI Desktop file datasets are connected to SQL Azure Database tables.</span></span>
* <span data-ttu-id="44265-324">**Fechar** arquivo do Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="44265-324">**Close** Power BI Desktop file.</span></span>

![Fechar o Power BI Desktop](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/14-close-powerbi-desktop.png)

* <span data-ttu-id="44265-326">Use o botão **Salvar** para salvar as alterações.</span><span class="sxs-lookup"><span data-stu-id="44265-326">Click **Save** button to save the changes.</span></span> 

<span data-ttu-id="44265-327">Você configurou todos os relatórios correspondentes ao caminho de processamento em lotes na solução.</span><span class="sxs-lookup"><span data-stu-id="44265-327">You have now configured all the reports corresponding to the batch processing path in the solution.</span></span> 

## <a name="upload-to-powerbicom"></a><span data-ttu-id="44265-328">Carregar no *powerbi.com*</span><span class="sxs-lookup"><span data-stu-id="44265-328">Upload to *powerbi.com*</span></span>
1. <span data-ttu-id="44265-329">Navegue até o portal da Web do Power BI em http://powerbi.com e faça logon.</span><span class="sxs-lookup"><span data-stu-id="44265-329">Navigate to the Power BI web portal at http://powerbi.com and login.</span></span>
2. <span data-ttu-id="44265-330">Clique em **Obter Dados**</span><span class="sxs-lookup"><span data-stu-id="44265-330">Click **Get Data**</span></span>  
3. <span data-ttu-id="44265-331">Carregue o arquivo do Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="44265-331">Upload the Power BI Desktop File.</span></span>  
4. <span data-ttu-id="44265-332">Para carregar, clique em **Obter Dados -> Obter Arquivos -> Arquivo local**</span><span class="sxs-lookup"><span data-stu-id="44265-332">To upload, click **Get Data -> Files Get -> Local file**</span></span>  
5. <span data-ttu-id="44265-333">Navegue para o **“**ConnectedCarsPbiReport.pbix**”**</span><span class="sxs-lookup"><span data-stu-id="44265-333">Navigate to the **“**ConnectedCarsPbiReport.pbix**”**</span></span>  
6. <span data-ttu-id="44265-334">Depois que o arquivo é carregado, você será direcionado para o espaço de trabalho do Power BI.</span><span class="sxs-lookup"><span data-stu-id="44265-334">Once the file is uploaded, you will be navigated back to your Power BI work space.</span></span>  

<span data-ttu-id="44265-335">Um conjunto de dados, relatórios e um painel em branco serão criados para você.</span><span class="sxs-lookup"><span data-stu-id="44265-335">A dataset, report and a blank dashboard will be created for you.</span></span>  

<span data-ttu-id="44265-336">Fixe os gráficos no novo painel chamado **Painel de Análise de Telemetria do Veículo** no **Power BI**.</span><span class="sxs-lookup"><span data-stu-id="44265-336">Pin charts to a new dashboard called **Vehicle Telemetry Analytics Dashboard** in **Power BI**.</span></span> <span data-ttu-id="44265-337">Clique no painel em branco criado acima e navegue até a seção **Relatórios** e clique no relatório que acabou de ser carregado.</span><span class="sxs-lookup"><span data-stu-id="44265-337">Click the blank dashboard created above and then navigate to the **Reports** section click the newly uploaded report.</span></span>  

![Telemetria do veículo Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard1.png) 

<span data-ttu-id="44265-339">**Observe que o relatório tem seis páginas:**</span><span class="sxs-lookup"><span data-stu-id="44265-339">**Note the report has six pages:**</span></span>  
<span data-ttu-id="44265-340">Página 1: densidade do veículo</span><span class="sxs-lookup"><span data-stu-id="44265-340">Page 1: Vehicle density</span></span>  
<span data-ttu-id="44265-341">Página 2: integridade do veículo em tempo real</span><span class="sxs-lookup"><span data-stu-id="44265-341">Page 2: Real-time vehicle health</span></span>  
<span data-ttu-id="44265-342">Página 3: veículos com direção agressiva</span><span class="sxs-lookup"><span data-stu-id="44265-342">Page 3: Aggressively Driven Vehicles</span></span>   
<span data-ttu-id="44265-343">Página 4: veículos que sofreram recall</span><span class="sxs-lookup"><span data-stu-id="44265-343">Page 4: Recalled vehicles</span></span>  
<span data-ttu-id="44265-344">Página 5: veículos com uso eficiente de combustível</span><span class="sxs-lookup"><span data-stu-id="44265-344">Page 5: Fuel Efficiently Driven Vehicles</span></span>  
<span data-ttu-id="44265-345">Página 6: logotipo da Contoso</span><span class="sxs-lookup"><span data-stu-id="44265-345">Page 6: Contoso Logo</span></span>  

![Carros conectados Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard2.png)

<span data-ttu-id="44265-347">**Na Página 3**, fixe o seguinte:</span><span class="sxs-lookup"><span data-stu-id="44265-347">**From Page 3**, pin the following:</span></span>  

1. <span data-ttu-id="44265-348">Contagem de vin</span><span class="sxs-lookup"><span data-stu-id="44265-348">Count of VIN</span></span>  
   ![Carros conectados Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard3.png) 
2. <span data-ttu-id="44265-350">Veículos de direção agressiva por modelo – Gráfico de cascata </span><span class="sxs-lookup"><span data-stu-id="44265-350">Aggressively driven vehicles by model – Waterfall chart</span></span>  
   ![Telemetria de veículo - Fixar gráficos 4](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard4.png)

<span data-ttu-id="44265-352">**Na Página 5**, fixe o seguinte:</span><span class="sxs-lookup"><span data-stu-id="44265-352">**From Page 5**, pin the following:</span></span> 

1. <span data-ttu-id="44265-353">Contagem de vin</span><span class="sxs-lookup"><span data-stu-id="44265-353">Count of vin</span></span>    
   ![Telemetria de veículo - Fixar gráficos 5](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard5.png)  
2. <span data-ttu-id="44265-355">Veículos com eficiência de combustível: Gráfico de colunas agrupadas </span><span class="sxs-lookup"><span data-stu-id="44265-355">Fuel efficient vehicles by model: Clustered column chart</span></span>  
   ![Telemetria de veículo - Fixar gráficos 6](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard6.png)

<span data-ttu-id="44265-357">**Na Página 4**, fixe o seguinte:</span><span class="sxs-lookup"><span data-stu-id="44265-357">**From Page 4**, pin the following:</span></span>  

1. <span data-ttu-id="44265-358">Contagem de vin</span><span class="sxs-lookup"><span data-stu-id="44265-358">Count of vin</span></span>  
   ![Telemetria de veículo - Fixar gráficos 7](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard7.png) 
2. <span data-ttu-id="44265-360">Veículos que tiveram recall por cidade, modelo : Treemap </span><span class="sxs-lookup"><span data-stu-id="44265-360">Recalled vehicles by city, model: Treemap</span></span>  
   ![Telemetria de veículo - Fixar gráficos 8](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard8.png)  

<span data-ttu-id="44265-362">**Na Página 6**, fixe o seguinte:</span><span class="sxs-lookup"><span data-stu-id="44265-362">**From Page 6**, pin the following:</span></span>  

1. <span data-ttu-id="44265-363">Logotipo da Contoso Motors </span><span class="sxs-lookup"><span data-stu-id="44265-363">Contoso Motors logo</span></span>  
   ![Telemetria de veículo - Fixar gráficos 9](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard9.png)

<span data-ttu-id="44265-365">**Organizar o painel**</span><span class="sxs-lookup"><span data-stu-id="44265-365">**Organize the dashboard**</span></span>  

1. <span data-ttu-id="44265-366">Navegue até o painel</span><span class="sxs-lookup"><span data-stu-id="44265-366">Navigate to the dashboard</span></span>
2. <span data-ttu-id="44265-367">Passe a seta do mouse sobre cada gráfico e renomeie-com base na nomenclatura fornecida na imagem do painel completo abaixo.</span><span class="sxs-lookup"><span data-stu-id="44265-367">Hover over each chart and rename it based on the naming provided in the complete dashboard image below.</span></span> <span data-ttu-id="44265-368">Mova os gráficos conforme o painel abaixo.</span><span class="sxs-lookup"><span data-stu-id="44265-368">Also move the charts around to look like the dashboard below.</span></span>  
   ![Telemetria de veículo - Organizar painel 2](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-organize-dashboard2.png)  
   ![Telemetria do veículo Power BI.com](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-dashboard.png)
3. <span data-ttu-id="44265-371">O painel final preenchido deve ser semelhante ao mostrado abaixo se você tiver criado todos os relatórios, como mencionadas neste documento.</span><span class="sxs-lookup"><span data-stu-id="44265-371">If you have created all the reports as mentioned in this document, the final completed dashboard should look like the following figure.</span></span> 

![Telemetria de veículo - Organizar painel 2](./media/cortana-analytics-playbook-vehicle-telemetry-powerbi-dashboard/vehicle-telemetry-organize-dashboard3.png)

<span data-ttu-id="44265-373">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="44265-373">Congratulations!</span></span> <span data-ttu-id="44265-374">Você criou com êxito os relatórios e o painel para obter informações preditivas, em lote e em tempo real sobre a integridade do veículo e hábitos de condução.</span><span class="sxs-lookup"><span data-stu-id="44265-374">You have successfully created the reports and the dashboard to gain real-time, predictive and batch insights on vehicle health and driving habits.</span></span>  
