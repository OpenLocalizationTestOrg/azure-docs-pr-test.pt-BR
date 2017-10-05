---
title: "Visualização de dados em tempo real de dados de sensor do Hub IoT do Azure – Power BI | Microsoft Docs"
description: "Use o Power BI para visualizar dados de temperatura e umidade que são coletados do sensor e enviados para o Hub IoT do Azure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "visualização de dados em tempo real, visualização de dados dinâmicos, visualização de dados de sensor"
ms.assetid: e67c9c09-6219-4f0f-ad42-58edaaa74f61
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: xshi
ms.openlocfilehash: b190fea06ffc2406d781c7edad091f097cca9c2d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="visualize-real-time-sensor-data-from-azure-iot-hub-using-power-bi"></a><span data-ttu-id="20564-104">Visualizar dados de sensor em tempo real do Hub IoT usando o Power BI</span><span class="sxs-lookup"><span data-stu-id="20564-104">Visualize real-time sensor data from Azure IoT Hub using Power BI</span></span>

![Diagrama de ponta a ponta](media/iot-hub-get-started-e2e-diagram/4.png)


[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

## <a name="what-you-learn"></a><span data-ttu-id="20564-106">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="20564-106">What you learn</span></span>

<span data-ttu-id="20564-107">Você aprenderá a visualizar dados do sensor em tempo real que recebe o hub IoT do Azure pelo Power BI.</span><span class="sxs-lookup"><span data-stu-id="20564-107">You learn how to visualize real-time sensor data that your Azure IoT hub receives by Power BI.</span></span> <span data-ttu-id="20564-108">Se você quiser tentar visualizar os dados em seu Hub IoT com Aplicativos Web, consulte [Usar Aplicativos Web do Azure para visualizar dados de sensor em tempo real do Hub IoT do Azure](iot-hub-live-data-visualization-in-web-apps.md).</span><span class="sxs-lookup"><span data-stu-id="20564-108">If you want to try visualize the data in your IoT hub with Web Apps, please see [Use Azure Web Apps to visualize real-time sensor data from Azure IoT Hub](iot-hub-live-data-visualization-in-web-apps.md).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="20564-109">O que fazer</span><span class="sxs-lookup"><span data-stu-id="20564-109">What you do</span></span>

- <span data-ttu-id="20564-110">Preparar seu Hub IoT para acesso a dados, adicionando um grupo de consumidores.</span><span class="sxs-lookup"><span data-stu-id="20564-110">Get your IoT hub ready for data access by adding a consumer group.</span></span>
- <span data-ttu-id="20564-111">Criar, configurar e executar um trabalho do Stream Analytics para transferência de dados do seu hub IoT à sua conta do Power BI.</span><span class="sxs-lookup"><span data-stu-id="20564-111">Create, configure and run a Stream Analytics job for data transfer from your IoT hub to your Power BI account.</span></span>
- <span data-ttu-id="20564-112">Crie e publique um relatório do Power BI para visualizar os dados.</span><span class="sxs-lookup"><span data-stu-id="20564-112">Create and publish a Power BI report to visualize the data.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="20564-113">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="20564-113">What you need</span></span>

- <span data-ttu-id="20564-114">Tutorial [Configurar seu dispositivo](iot-hub-raspberry-pi-kit-node-get-started.md) concluído que aborda os seguintes requisitos:</span><span class="sxs-lookup"><span data-stu-id="20564-114">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers the following requirements:</span></span>
  - <span data-ttu-id="20564-115">Uma assinatura ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="20564-115">An active Azure subscription.</span></span>
  - <span data-ttu-id="20564-116">Um hub IoT do Azure em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="20564-116">An Azure IoT hub under your subscription.</span></span>
  - <span data-ttu-id="20564-117">O aplicativo cliente que envia mensagens para o hub IoT do Azure.</span><span class="sxs-lookup"><span data-stu-id="20564-117">A client application that sends messages to your Azure IoT hub.</span></span>
- <span data-ttu-id="20564-118">Uma conta do Power BI.</span><span class="sxs-lookup"><span data-stu-id="20564-118">A Power BI account.</span></span> <span data-ttu-id="20564-119">([Experimente gratuitamente o Power BI](https://powerbi.microsoft.com/))</span><span class="sxs-lookup"><span data-stu-id="20564-119">([Try Power BI for free](https://powerbi.microsoft.com/))</span></span>

[!INCLUDE [iot-hub-get-started-create-consumer-group](../../includes/iot-hub-get-started-create-consumer-group.md)]

## <a name="create-configure-and-run-a-stream-analytics-job"></a><span data-ttu-id="20564-120">Criar, configurar e executar um trabalho do Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="20564-120">Create, configure, and run a Stream Analytics job</span></span>

### <a name="create-a-stream-analytics-job"></a><span data-ttu-id="20564-121">Criar um trabalho de Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="20564-121">Create a Stream Analytics job</span></span>

1. <span data-ttu-id="20564-122">No portal do Azure, clique em novo > Internet das coisas > trabalho do Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="20564-122">In the Azure portal, click New > Internet of Things > Stream Analytics job.</span></span>
1. <span data-ttu-id="20564-123">Insira as seguintes informações para o trabalho.</span><span class="sxs-lookup"><span data-stu-id="20564-123">Enter the following information for the job.</span></span>

   <span data-ttu-id="20564-124">**Nome do trabalho**: o nome do trabalho.</span><span class="sxs-lookup"><span data-stu-id="20564-124">**Job name**: The name of the job.</span></span> <span data-ttu-id="20564-125">O nome deve ser globalmente exclusivo.</span><span class="sxs-lookup"><span data-stu-id="20564-125">The name must be globally unique.</span></span>

   <span data-ttu-id="20564-126">**Grupo de recursos**: use o mesmo grupo de recursos usado pelo seu hub IoT.</span><span class="sxs-lookup"><span data-stu-id="20564-126">**Resource group**: Use the same resource group that your IoT hub uses.</span></span>

   <span data-ttu-id="20564-127">**Local**: use o mesmo local do que o grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="20564-127">**Location**: Use the same location as your resource group.</span></span>

   <span data-ttu-id="20564-128">**Fixar no painel**: marque essa opção para facilitar o acesso ao seu hub IoT do painel.</span><span class="sxs-lookup"><span data-stu-id="20564-128">**Pin to dashboard**: Check this option for easy access to your IoT hub from the dashboard.</span></span>

   ![Criar um trabalho do Stream Analytics no Azure](media/iot-hub-live-data-visualization-in-power-bi/2_create-stream-analytics-job-azure.png)

1. <span data-ttu-id="20564-130">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="20564-130">Click **Create**.</span></span>

### <a name="add-an-input-to-the-stream-analytics-job"></a><span data-ttu-id="20564-131">Adicionar uma entrada ao trabalho do Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="20564-131">Add an input to the Stream Analytics job</span></span>

1. <span data-ttu-id="20564-132">Abra o trabalho do Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="20564-132">Open the Stream Analytics job.</span></span>
1. <span data-ttu-id="20564-133">Em **Topologia do Trabalho**, clique em **Entradas**.</span><span class="sxs-lookup"><span data-stu-id="20564-133">Under **Job Topology**, click **Inputs**.</span></span>
1. <span data-ttu-id="20564-134">No **entradas** painel, clique em **adicionar**e, em seguida, insira as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="20564-134">In the **Inputs** pane, click **Add**, and then enter the following information:</span></span>

   <span data-ttu-id="20564-135">**Alias de entrada**: o alias exclusivo para a entrada.</span><span class="sxs-lookup"><span data-stu-id="20564-135">**Input alias**: The unique alias for the input.</span></span>

   <span data-ttu-id="20564-136">**Origem**: selecione **hub IoT**.</span><span class="sxs-lookup"><span data-stu-id="20564-136">**Source**: Select **IoT hub**.</span></span>

   <span data-ttu-id="20564-137">**Grupo de consumidores**: selecione o grupo de consumidores que você acabou de criar.</span><span class="sxs-lookup"><span data-stu-id="20564-137">**Consumer group**: Select the consumer group you just created.</span></span>
1. <span data-ttu-id="20564-138">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="20564-138">Click **Create**.</span></span>

   ![Adicionar uma entrada a um trabalho do Stream Analytics no Azure](media/iot-hub-live-data-visualization-in-power-bi/3_add-input-to-stream-analytics-job-azure.png)

### <a name="add-an-output-to-the-stream-analytics-job"></a><span data-ttu-id="20564-140">Adicionar uma saída ao trabalho do Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="20564-140">Add an output to the Stream Analytics job</span></span>

1. <span data-ttu-id="20564-141">Em **Topologia do Trabalho**, clique em **Saídas**.</span><span class="sxs-lookup"><span data-stu-id="20564-141">Under **Job Topology**, click **Outputs**.</span></span>
1. <span data-ttu-id="20564-142">No **saídas** painel, clique em **adicionar**e, em seguida, insira as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="20564-142">In the **Outputs** pane, click **Add**, and then enter the following information:</span></span>

   <span data-ttu-id="20564-143">**Alias de saída**: o alias exclusivo para a saída.</span><span class="sxs-lookup"><span data-stu-id="20564-143">**Output alias**: The unique alias for the output.</span></span>

   <span data-ttu-id="20564-144">**Coletor**: selecione **Power BI**.</span><span class="sxs-lookup"><span data-stu-id="20564-144">**Sink**: Select **Power BI**.</span></span>
1. <span data-ttu-id="20564-145">Clique em **Autorizar** e depois entre na sua conta do Power BI.</span><span class="sxs-lookup"><span data-stu-id="20564-145">Click **Authorize**, and then sign into your Power BI account.</span></span>
1. <span data-ttu-id="20564-146">Uma vez autorizado, insira as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="20564-146">Once authorized, enter the following information:</span></span>

   <span data-ttu-id="20564-147">**Espaço de trabalho de grupo**: selecione o espaço de trabalho do grupo de destino.</span><span class="sxs-lookup"><span data-stu-id="20564-147">**Group Workspace**: Select your target group workspace.</span></span>

   <span data-ttu-id="20564-148">**Nome do Conjunto de Dados**: insira um nome de conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="20564-148">**Dataset Name**: Enter a dataset name.</span></span>

   <span data-ttu-id="20564-149">**Nome da Tabela**: insira um nome de tabela.</span><span class="sxs-lookup"><span data-stu-id="20564-149">**Table Name**: Enter a table name.</span></span>
1. <span data-ttu-id="20564-150">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="20564-150">Click **Create**.</span></span>

   ![Adicionar uma saída a um trabalho do Stream Analytics no Azure](media/iot-hub-live-data-visualization-in-power-bi/4_add-output-to-stream-analytics-job-azure.png)

### <a name="configure-the-query-of-the-stream-analytics-job"></a><span data-ttu-id="20564-152">Configurar a consulta do trabalho do Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="20564-152">Configure the query of the Stream Analytics job</span></span>

1. <span data-ttu-id="20564-153">Em **Topologia do Trabalho**, clique em **Consulta**.</span><span class="sxs-lookup"><span data-stu-id="20564-153">Under **Job Topology**, click **Query**.</span></span>
1. <span data-ttu-id="20564-154">Substitua `[YourInputAlias]` pelo alias de entrada do trabalho.</span><span class="sxs-lookup"><span data-stu-id="20564-154">Replace `[YourInputAlias]` with the input alias of the job.</span></span>
1. <span data-ttu-id="20564-155">Substitua `[YourOutputAlias]` pelo alias de saída do trabalho.</span><span class="sxs-lookup"><span data-stu-id="20564-155">Replace `[YourOutputAlias]` with the output alias of the job.</span></span>
1. <span data-ttu-id="20564-156">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="20564-156">Click **Save**.</span></span>

   ![Adicionar uma consulta a um trabalho do Stream Analytics no Azure](media/iot-hub-live-data-visualization-in-power-bi/5_add-query-stream-analytics-job-azure.png)

### <a name="run-the-stream-analytics-job"></a><span data-ttu-id="20564-158">Executar o trabalho do Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="20564-158">Run the Stream Analytics job</span></span>

<span data-ttu-id="20564-159">No trabalho do Stream Analytics, clique em **Iniciar** > **Agora** > **Iniciar**.</span><span class="sxs-lookup"><span data-stu-id="20564-159">In the Stream Analytics job, click **Start** > **Now** > **Start**.</span></span> <span data-ttu-id="20564-160">Depois que o trabalho é iniciado com êxito, o status do trabalho muda de **parado** para **executando**.</span><span class="sxs-lookup"><span data-stu-id="20564-160">Once the job successfully starts, the job status changes from **Stopped** to **Running**.</span></span>

![Executar um trabalho do Stream Analytics no Azure](media/iot-hub-live-data-visualization-in-power-bi/6_run-stream-analytics-job-azure.png)

## <a name="create-and-publish-a-power-bi-report-to-visualize-the-data"></a><span data-ttu-id="20564-162">Criar e publicar um relatório do Power BI para visualizar os dados</span><span class="sxs-lookup"><span data-stu-id="20564-162">Create and publish a Power BI report to visualize the data</span></span>

1. <span data-ttu-id="20564-163">Verifique se o aplicativo de exemplo está em execução em seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="20564-163">Ensure the sample application is running on your device.</span></span> <span data-ttu-id="20564-164">Se não, você pode consultar os tutoriais em [Configure seu dispositivo](https://docs.microsoft.com/azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started).</span><span class="sxs-lookup"><span data-stu-id="20564-164">If not, you can refer to the tutorials under [Setup your device](https://docs.microsoft.com/azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started).</span></span>
1. <span data-ttu-id="20564-165">Entre na sua conta do [Power BI](https://powerbi.microsoft.com/en-us/).</span><span class="sxs-lookup"><span data-stu-id="20564-165">Sign in to your [Power BI](https://powerbi.microsoft.com/en-us/) account.</span></span>
1. <span data-ttu-id="20564-166">Vá para o espaço de trabalho de grupo que você definiu quando criou a saída para o trabalho do Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="20564-166">Go to the group workspace that you set when you created the output for the Stream Analytics job.</span></span>
1. <span data-ttu-id="20564-167">Clique em **Conjuntos de dados de streaming**.</span><span class="sxs-lookup"><span data-stu-id="20564-167">Click **Streaming datasets**.</span></span>

   <span data-ttu-id="20564-168">Você deve ver o conjunto de dados relacionado que você especificou quando criou a saída para o trabalho do Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="20564-168">You should see the listed dataset that you specified when you created the output for the Stream Analytics job.</span></span>
1. <span data-ttu-id="20564-169">Em **AÇÕES**, clique no primeiro ícone para criar um relatório.</span><span class="sxs-lookup"><span data-stu-id="20564-169">Under **ACTIONS**, click the first icon to create a report.</span></span>

   ![Criar um relatório do Microsoft Power BI](media/iot-hub-live-data-visualization-in-power-bi/7_create-power-bi-report-microsoft.png)

1. <span data-ttu-id="20564-171">Crie um gráfico de linhas para mostrar a temperatura em tempo real ao longo do tempo.</span><span class="sxs-lookup"><span data-stu-id="20564-171">Create a line chart to show real-time temperature over time.</span></span>
   1. <span data-ttu-id="20564-172">Na página de criação de relatório, adicione um gráfico de linhas.</span><span class="sxs-lookup"><span data-stu-id="20564-172">On the report creation page, add a line chart.</span></span>
   1. <span data-ttu-id="20564-173">Sobre o **campos** painel, expanda a tabela que você especificou quando criou a saída para o trabalho do Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="20564-173">On the **Fields** pane, expand the table that you specified when you created the output for the Stream Analytics job.</span></span>
   1. <span data-ttu-id="20564-174">Arraste **EventEnqueuedUtcTime** para **eixo** sobre o **visualizações** painel.</span><span class="sxs-lookup"><span data-stu-id="20564-174">Drag **EventEnqueuedUtcTime** to **Axis** on the **Visualizations** pane.</span></span>
   1. <span data-ttu-id="20564-175">Arraste **temperatura** para **Valores**.</span><span class="sxs-lookup"><span data-stu-id="20564-175">Drag **temperature** to **Values**.</span></span>

      <span data-ttu-id="20564-176">Agora, um gráfico de linhas é criado.</span><span class="sxs-lookup"><span data-stu-id="20564-176">Now a line chart is created.</span></span> <span data-ttu-id="20564-177">O eixo x exibe a data e a hora no fuso horário UTC.</span><span class="sxs-lookup"><span data-stu-id="20564-177">The x-axis displays date and time in the UTC time zone.</span></span> <span data-ttu-id="20564-178">O eixo y mostra a temperatura do sensor.</span><span class="sxs-lookup"><span data-stu-id="20564-178">The y-axis displays temperature from the sensor.</span></span>

      ![Adicionar um gráfico de linhas para a temperatura a um relatório do Microsoft Power BI](media/iot-hub-live-data-visualization-in-power-bi/8_add-line-chart-for-temperature-to-power-bi-report-microsoft.png)

1. <span data-ttu-id="20564-180">Crie outro gráfico de linhas para mostrar umidade em tempo real ao longo do tempo.</span><span class="sxs-lookup"><span data-stu-id="20564-180">Create another line chart to show real-time humidity over time.</span></span> <span data-ttu-id="20564-181">Para fazer isso, siga as mesmas etapas acima e coloque **EventEnqueuedUtcTime** no eixo x e **umidade** no eixo y.</span><span class="sxs-lookup"><span data-stu-id="20564-181">To do this, follow the same steps above and place **EventEnqueuedUtcTime** on the x-axis and **humidity** on the y-axis.</span></span>

   ![Adicionar um gráfico de linhas para umidade a um relatório do Microsoft Power BI](media/iot-hub-live-data-visualization-in-power-bi/9_add-line-chart-for-humidity-to-power-bi-report-microsoft.png)

1. <span data-ttu-id="20564-183">Clique em **Salvar** para salvar o relatório.</span><span class="sxs-lookup"><span data-stu-id="20564-183">Click **Save** to save the report.</span></span>
1. <span data-ttu-id="20564-184">Clique em **Arquivo** > **Publicar na Web**.</span><span class="sxs-lookup"><span data-stu-id="20564-184">Click **File** > **Publish to web**.</span></span>
1. <span data-ttu-id="20564-185">Clique em **Criar código incorporado** e clique em **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="20564-185">Click **Create embed code**, and then click **Publish**.</span></span>

<span data-ttu-id="20564-186">São fornecidas no link do relatório que você pode compartilhar com ninguém para acesso a relatórios e um trecho de código para integrar o relatório em seu blog ou site.</span><span class="sxs-lookup"><span data-stu-id="20564-186">You're provided the report link that you can share with anyone for report access and a code snippet to integrate the report into your blog or website.</span></span>

![Publicar um relatório do Microsoft Power BI](media/iot-hub-live-data-visualization-in-power-bi/10_publish-power-bi-report-microsoft.png)

<span data-ttu-id="20564-188">A Microsoft também oferece o [aplicativos móveis do Power BI](https://powerbi.microsoft.com/en-us/documentation/powerbi-power-bi-apps-for-mobile-devices/) para exibir e interagir com seus relatórios e painéis do Power BI em seu dispositivo móvel.</span><span class="sxs-lookup"><span data-stu-id="20564-188">Microsoft also offers the [Power BI mobile apps](https://powerbi.microsoft.com/en-us/documentation/powerbi-power-bi-apps-for-mobile-devices/) for viewing and interacting with your Power BI dashboards and reports on your mobile device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="20564-189">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="20564-189">Next steps</span></span>

<span data-ttu-id="20564-190">Você usou com êxito o Power BI para visualizar dados do sensor em tempo real do seu Hub IoT do Azure.</span><span class="sxs-lookup"><span data-stu-id="20564-190">You’ve successfully used Power BI to visualize real-time sensor data from your Azure IoT hub.</span></span>
<span data-ttu-id="20564-191">Há uma maneira alternativa para visualizar dados do Hub IoT do Azure.</span><span class="sxs-lookup"><span data-stu-id="20564-191">There is an alternate way to visualize data from Azure IoT Hub.</span></span> <span data-ttu-id="20564-192">Veja [Usar Aplicativos Web do Azure para visualizar dados de sensor em tempo real do Hub IoT do Azure](iot-hub-live-data-visualization-in-web-apps.md).</span><span class="sxs-lookup"><span data-stu-id="20564-192">See [Use Azure Web Apps to visualize real-time sensor data from Azure IoT Hub](iot-hub-live-data-visualization-in-web-apps.md).</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
