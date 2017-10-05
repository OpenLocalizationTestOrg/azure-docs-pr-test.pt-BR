---
title: "Previsão do tempo usando o Azure Machine Learning com os dados do Hub IoT | Microsoft Docs"
description: Use o Azure Machine Learning para prever a possibilidade de chuva com base nos dados de temperatura e umidade coletados pelo Hub IoT de um sensor.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "Machine Learning de previsão do tempo"
ms.assetid: 8ba7d9e7-699c-4448-b353-0f3e1429d198
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: xshi
ms.openlocfilehash: 50ae54b9476c49b80236e295c0bf244df8236cff
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="weather-forecast-using-the-sensor-data-from-your-iot-hub-in-azure-machine-learning"></a><span data-ttu-id="1fe6d-104">Previsão do tempo usando os dados do sensor do Hub IoT no Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="1fe6d-104">Weather forecast using the sensor data from your IoT hub in Azure Machine Learning</span></span>

![Diagrama de ponta a ponta](media/iot-hub-get-started-e2e-diagram/6.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

<span data-ttu-id="1fe6d-106">O Machine Learning é uma técnica da ciência de dados que ajuda os computadores a aprenderem com os dados existentes para prever tendências, resultados e comportamentos futuros.</span><span class="sxs-lookup"><span data-stu-id="1fe6d-106">Machine learning is a technique of data science that helps computers learn from existing data to forecast future behaviors, outcomes, and trends.</span></span> <span data-ttu-id="1fe6d-107">O Azure Machine Learning é um serviço de análise preditiva na nuvem que permite criar rapidamente modelos preditivos e implantá-los como soluções de análise.</span><span class="sxs-lookup"><span data-stu-id="1fe6d-107">Azure Machine Learning is a cloud predictive analytics service that makes it possible to quickly create and deploy predictive models as analytics solutions.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="1fe6d-108">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="1fe6d-108">What you learn</span></span>

<span data-ttu-id="1fe6d-109">Saiba como usar o Azure Machine Learning para fazer uma previsão do tempo (possibilidade de chuva) usando os dados de temperatura e umidade do Hub IoT do Azure.</span><span class="sxs-lookup"><span data-stu-id="1fe6d-109">You learn how to use Azure Machine Learning to do weather forecast (chance of rain) using the temperature and humidity data from your Azure IoT hub.</span></span> <span data-ttu-id="1fe6d-110">A possibilidade de chuva é o resultado de um modelo de previsão de clima preparado.</span><span class="sxs-lookup"><span data-stu-id="1fe6d-110">The chance of rain is the output of a prepared weather prediction model.</span></span> <span data-ttu-id="1fe6d-111">O modelo se baseia em dados históricos para prever a possibilidade de chuva com base na temperatura e na umidade.</span><span class="sxs-lookup"><span data-stu-id="1fe6d-111">The model is built upon historic data to forecast chance of rain based on temperature and humidity.</span></span>

## <a name="what-you-do"></a><span data-ttu-id="1fe6d-112">O que fazer</span><span class="sxs-lookup"><span data-stu-id="1fe6d-112">What you do</span></span>

- <span data-ttu-id="1fe6d-113">Implante o modelo de previsão do tempo como um serviço Web.</span><span class="sxs-lookup"><span data-stu-id="1fe6d-113">Deploy the weather prediction model as a web service.</span></span>
- <span data-ttu-id="1fe6d-114">Preparar seu Hub IoT para acesso a dados, adicionando um grupo de consumidores.</span><span class="sxs-lookup"><span data-stu-id="1fe6d-114">Get your IoT hub ready for data access by adding a consumer group.</span></span>
- <span data-ttu-id="1fe6d-115">Crie um trabalho do Stream Analytics e configure o trabalho para:</span><span class="sxs-lookup"><span data-stu-id="1fe6d-115">Create a Stream Analytics job and configure the job to:</span></span>
  - <span data-ttu-id="1fe6d-116">Leia dados de temperatura e umidade no Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="1fe6d-116">Read temperature and humidity data from your IoT hub.</span></span>
  - <span data-ttu-id="1fe6d-117">Chame o serviço Web para obter a possibilidade de chuva.</span><span class="sxs-lookup"><span data-stu-id="1fe6d-117">Call the web service to get the rain chance.</span></span>
  - <span data-ttu-id="1fe6d-118">Salve o resultado em um armazenamento de blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="1fe6d-118">Save the result to an Azure blob storage.</span></span>
- <span data-ttu-id="1fe6d-119">Use o Gerenciador de Armazenamento do Microsoft Azure para exibir a previsão do tempo.</span><span class="sxs-lookup"><span data-stu-id="1fe6d-119">Use Microsoft Azure Storage Explorer to view the weather forecast.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="1fe6d-120">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="1fe6d-120">What you need</span></span>

- <span data-ttu-id="1fe6d-121">Tutorial [Configurar seu dispositivo](iot-hub-raspberry-pi-kit-node-get-started.md) concluído que aborda os seguintes requisitos:</span><span class="sxs-lookup"><span data-stu-id="1fe6d-121">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers the following requirements:</span></span>
  - <span data-ttu-id="1fe6d-122">Uma assinatura ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="1fe6d-122">An active Azure subscription.</span></span>
  - <span data-ttu-id="1fe6d-123">Um hub IoT do Azure em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="1fe6d-123">An Azure IoT hub under your subscription.</span></span>
  - <span data-ttu-id="1fe6d-124">O aplicativo cliente que envia mensagens para o hub IoT do Azure.</span><span class="sxs-lookup"><span data-stu-id="1fe6d-124">A client application that sends messages to your Azure IoT hub.</span></span>
- <span data-ttu-id="1fe6d-125">Uma conta do Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="1fe6d-125">An Azure Machine Learning Studio account.</span></span> <span data-ttu-id="1fe6d-126">([Experimente o Machine Learning Studio gratuitamente](https://studio.azureml.net/)).</span><span class="sxs-lookup"><span data-stu-id="1fe6d-126">([Try Machine Learning Studio for free](https://studio.azureml.net/)).</span></span>

## <a name="deploy-the-weather-prediction-model-as-a-web-service"></a><span data-ttu-id="1fe6d-127">Implantar o modelo de previsão do tempo como um serviço Web</span><span class="sxs-lookup"><span data-stu-id="1fe6d-127">Deploy the weather prediction model as a web service</span></span>

1. <span data-ttu-id="1fe6d-128">Acesse a [página do modelo de previsão do tempo](https://gallery.cortanaintelligence.com/Experiment/Weather-prediction-model-1).</span><span class="sxs-lookup"><span data-stu-id="1fe6d-128">Go to the [weather prediction model page](https://gallery.cortanaintelligence.com/Experiment/Weather-prediction-model-1).</span></span>
1. <span data-ttu-id="1fe6d-129">Clique em **Abrir no Studio** no Microsoft Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="1fe6d-129">Click **Open in Studio** in Microsoft Azure Machine Learning Studio.</span></span>
   <span data-ttu-id="1fe6d-130">![Abrir a página do modelo de previsão do tempo na Galeria do Cortana Intelligence](media/iot-hub-weather-forecast-machine-learning/2_weather-prediction-model-in-cortana-intelligence-gallery.png)</span><span class="sxs-lookup"><span data-stu-id="1fe6d-130">![Open the weather prediction model page in Cortana Intelligence Gallery](media/iot-hub-weather-forecast-machine-learning/2_weather-prediction-model-in-cortana-intelligence-gallery.png)</span></span>
1. <span data-ttu-id="1fe6d-131">Clique em **Executar** para validar as etapas no modelo.</span><span class="sxs-lookup"><span data-stu-id="1fe6d-131">Click **Run** to validate the steps in the model.</span></span> <span data-ttu-id="1fe6d-132">Esta etapa pode levar 2 minutos para ser concluída.</span><span class="sxs-lookup"><span data-stu-id="1fe6d-132">This step might take 2 minutes to complete.</span></span>
   <span data-ttu-id="1fe6d-133">![Abrir o modelo de previsão do tempo no Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/3_open-weather-prediction-model-in-azure-machine-learning-studio.png)</span><span class="sxs-lookup"><span data-stu-id="1fe6d-133">![Open the weather prediction model in Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/3_open-weather-prediction-model-in-azure-machine-learning-studio.png)</span></span>
1. <span data-ttu-id="1fe6d-134">Clique em **CONFIGURAR SERVIÇO WEB** > **Serviço Web Preditivo**.</span><span class="sxs-lookup"><span data-stu-id="1fe6d-134">Click **SET UP WEB SERVICE** > **Predictive Web Service**.</span></span>
   <span data-ttu-id="1fe6d-135">![Implantar o modelo de previsão do tempo no Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/4-deploy-weather-prediction-model-in-azure-machine-learning-studio.png)</span><span class="sxs-lookup"><span data-stu-id="1fe6d-135">![Deploy the weather prediction model in Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/4-deploy-weather-prediction-model-in-azure-machine-learning-studio.png)</span></span>
1. <span data-ttu-id="1fe6d-136">No diagrama, arraste o módulo **entrada do serviço Web** em algum lugar próximo ao módulo **Modelo de Pontuação**.</span><span class="sxs-lookup"><span data-stu-id="1fe6d-136">In the diagram, drag the **Web service input** module somewhere near the **Score Model** module.</span></span>
1. <span data-ttu-id="1fe6d-137">Conecte o módulo **entrada do serviço Web** ao módulo **Modelo de Pontuação**.</span><span class="sxs-lookup"><span data-stu-id="1fe6d-137">Connect the **Web service input** module to the **Score Model** module.</span></span>
   <span data-ttu-id="1fe6d-138">![Conectar dois módulos no Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/13_connect-modules-azure-machine-learning-studio.png)</span><span class="sxs-lookup"><span data-stu-id="1fe6d-138">![Connect two modules in Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/13_connect-modules-azure-machine-learning-studio.png)</span></span>
1. <span data-ttu-id="1fe6d-139">Clique em **EXECUTAR** para validar as etapas no modelo.</span><span class="sxs-lookup"><span data-stu-id="1fe6d-139">Click **RUN** to validate the steps in the model.</span></span>
1. <span data-ttu-id="1fe6d-140">Clique em **IMPLANTAR SERVIÇO WEB** para implantar o modelo como um serviço Web.</span><span class="sxs-lookup"><span data-stu-id="1fe6d-140">Click **DEPLOY WEB SERVICE** to deploy the model as a web service.</span></span>
1. <span data-ttu-id="1fe6d-141">No painel do modelo, baixe o **Excel 2010 ou a pasta de trabalho anterior** de **SOLICITAÇÃO/RESPOSTA**.</span><span class="sxs-lookup"><span data-stu-id="1fe6d-141">On the dashboard of the model, download the **Excel 2010 or earlier workbook** for **REQUEST/RESPONSE**.</span></span>

   > [!Note]
   > <span data-ttu-id="1fe6d-142">Lembre-se de baixar o **Excel 2010 ou a pasta de trabalho anterior** mesmo se estiver executando uma versão posterior do Excel no computador.</span><span class="sxs-lookup"><span data-stu-id="1fe6d-142">Ensure that you download the **Excel 2010 or earlier workbook** even if you are running a later version of Excel on your computer.</span></span>

   ![Baixar o Excel para obter o ponto de extremidade SOLICITAÇÃO/RESPOSTA](media/iot-hub-weather-forecast-machine-learning/5_download-endpoint-app-excel-for-request-response.png)

1. <span data-ttu-id="1fe6d-144">Abra a pasta de trabalho do Excel, anote a **URL DO SERVIÇO WEB** e a **TECLA DE ACESSO**.</span><span class="sxs-lookup"><span data-stu-id="1fe6d-144">Open the Excel workbook, make a note of the **WEB SERVICE URL** and **ACCESS KEY**.</span></span>

[!INCLUDE [iot-hub-get-started-create-consumer-group](../../includes/iot-hub-get-started-create-consumer-group.md)]

## <a name="create-configure-and-run-a-stream-analytics-job"></a><span data-ttu-id="1fe6d-145">Criar, configurar e executar um trabalho do Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="1fe6d-145">Create, configure, and run a Stream Analytics job</span></span>

### <a name="create-a-stream-analytics-job"></a><span data-ttu-id="1fe6d-146">Criar um trabalho de Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="1fe6d-146">Create a Stream Analytics job</span></span>

1. <span data-ttu-id="1fe6d-147">No [portal do Azure](https://ms.portal.azure.com/), clique em **Novo** > **Internet das Coisas** > **Trabalho do Stream Analytics**.</span><span class="sxs-lookup"><span data-stu-id="1fe6d-147">In the [Azure portal](https://ms.portal.azure.com/), click **New** > **Internet of Things** > **Stream Analytics job**.</span></span>
1. <span data-ttu-id="1fe6d-148">Insira as seguintes informações para o trabalho.</span><span class="sxs-lookup"><span data-stu-id="1fe6d-148">Enter the following information for the job.</span></span>

   <span data-ttu-id="1fe6d-149">**Nome do trabalho**: o nome do trabalho.</span><span class="sxs-lookup"><span data-stu-id="1fe6d-149">**Job name**: The name of the job.</span></span> <span data-ttu-id="1fe6d-150">O nome deve ser globalmente exclusivo.</span><span class="sxs-lookup"><span data-stu-id="1fe6d-150">The name must be globally unique.</span></span>

   <span data-ttu-id="1fe6d-151">**Grupo de recursos**: use o mesmo grupo de recursos usado pelo seu hub IoT.</span><span class="sxs-lookup"><span data-stu-id="1fe6d-151">**Resource group**: Use the same resource group that your IoT hub uses.</span></span>

   <span data-ttu-id="1fe6d-152">**Local**: use o mesmo local do que o grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="1fe6d-152">**Location**: Use the same location as your resource group.</span></span>

   <span data-ttu-id="1fe6d-153">**Fixar no painel**: marque essa opção para facilitar o acesso ao seu hub IoT do painel.</span><span class="sxs-lookup"><span data-stu-id="1fe6d-153">**Pin to dashboard**: Check this option for easy access to your IoT hub from the dashboard.</span></span>

   ![Criar um trabalho do Stream Analytics no Azure](media/iot-hub-weather-forecast-machine-learning/7_create-stream-analytics-job-azure.png)

1. <span data-ttu-id="1fe6d-155">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="1fe6d-155">Click **Create**.</span></span>

### <a name="add-an-input-to-the-stream-analytics-job"></a><span data-ttu-id="1fe6d-156">Adicionar uma entrada ao trabalho do Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="1fe6d-156">Add an input to the Stream Analytics job</span></span>

1. <span data-ttu-id="1fe6d-157">Abra o trabalho do Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="1fe6d-157">Open the Stream Analytics job.</span></span>
1. <span data-ttu-id="1fe6d-158">Em **Topologia do Trabalho**, clique em **Entradas**.</span><span class="sxs-lookup"><span data-stu-id="1fe6d-158">Under **Job Topology**, click **Inputs**.</span></span>
1. <span data-ttu-id="1fe6d-159">No **entradas** painel, clique em **adicionar**e, em seguida, insira as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="1fe6d-159">In the **Inputs** pane, click **Add**, and then enter the following information:</span></span>

   <span data-ttu-id="1fe6d-160">**Alias de entrada**: o alias exclusivo para a entrada.</span><span class="sxs-lookup"><span data-stu-id="1fe6d-160">**Input alias**: The unique alias for the input.</span></span>

   <span data-ttu-id="1fe6d-161">**Origem**: selecione **hub IoT**.</span><span class="sxs-lookup"><span data-stu-id="1fe6d-161">**Source**: Select **IoT hub**.</span></span>

   <span data-ttu-id="1fe6d-162">**Grupo de consumidores**: selecione o grupo de consumidores criado.</span><span class="sxs-lookup"><span data-stu-id="1fe6d-162">**Consumer group**: Select the consumer group you created.</span></span>

   ![Adicionar uma entrada ao trabalho do Stream Analytics no Azure](media/iot-hub-weather-forecast-machine-learning/8_add-input-stream-analytics-job-azure.png)

1. <span data-ttu-id="1fe6d-164">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="1fe6d-164">Click **Create**.</span></span>

### <a name="add-an-output-to-the-stream-analytics-job"></a><span data-ttu-id="1fe6d-165">Adicionar uma saída ao trabalho do Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="1fe6d-165">Add an output to the Stream Analytics job</span></span>

1. <span data-ttu-id="1fe6d-166">Em **Topologia do Trabalho**, clique em **Saídas**.</span><span class="sxs-lookup"><span data-stu-id="1fe6d-166">Under **Job Topology**, click **Outputs**.</span></span>
1. <span data-ttu-id="1fe6d-167">No **saídas** painel, clique em **adicionar**e, em seguida, insira as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="1fe6d-167">In the **Outputs** pane, click **Add**, and then enter the following information:</span></span>

   <span data-ttu-id="1fe6d-168">**Alias de saída**: o alias exclusivo para a saída.</span><span class="sxs-lookup"><span data-stu-id="1fe6d-168">**Output alias**: The unique alias for the output.</span></span>

   <span data-ttu-id="1fe6d-169">**Coletor**: selecione **Armazenamento de Blobs**.</span><span class="sxs-lookup"><span data-stu-id="1fe6d-169">**Sink**: Select **Blob Storage**.</span></span>

   <span data-ttu-id="1fe6d-170">**Conta de armazenamento**: a conta de armazenamento do armazenamento de blobs.</span><span class="sxs-lookup"><span data-stu-id="1fe6d-170">**Storage account**: The storage account for your blob storage.</span></span> <span data-ttu-id="1fe6d-171">Você pode criar uma conta de armazenamento ou usar uma existente.</span><span class="sxs-lookup"><span data-stu-id="1fe6d-171">You can create a storage account or use an existing one.</span></span>

   <span data-ttu-id="1fe6d-172">**Contêiner**: o contêiner em que o blob foi salvo.</span><span class="sxs-lookup"><span data-stu-id="1fe6d-172">**Container**: The container where the blob is saved.</span></span> <span data-ttu-id="1fe6d-173">Você pode criar um contêiner ou usar um existente.</span><span class="sxs-lookup"><span data-stu-id="1fe6d-173">You can create a container or use an existing one.</span></span>

   <span data-ttu-id="1fe6d-174">**Formato de serialização de evento**: selecione **CSV**.</span><span class="sxs-lookup"><span data-stu-id="1fe6d-174">**Event serialization format**: Select **CSV**.</span></span>

   ![Adicionar uma saída ao trabalho do Stream Analytics no Azure](media/iot-hub-weather-forecast-machine-learning/9_add-output-stream-analytics-job-azure.png)

1. <span data-ttu-id="1fe6d-176">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="1fe6d-176">Click **Create**.</span></span>

### <a name="add-a-function-to-the-stream-analytics-job-to-call-the-web-service-you-deployed"></a><span data-ttu-id="1fe6d-177">Adicionar uma função ao trabalho do Stream Analytics para chamar o serviço Web implantado</span><span class="sxs-lookup"><span data-stu-id="1fe6d-177">Add a function to the Stream Analytics job to call the web service you deployed</span></span>

1. <span data-ttu-id="1fe6d-178">Em **Topologia de Trabalho**, clique em **Funções** > **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="1fe6d-178">Under **Job Topology**, click **Functions** > **Add**.</span></span>
1. <span data-ttu-id="1fe6d-179">Insira as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="1fe6d-179">Enter the following information:</span></span>

   <span data-ttu-id="1fe6d-180">**Alias da Função**: insira `machinelearning`.</span><span class="sxs-lookup"><span data-stu-id="1fe6d-180">**Function Alias**: Enter `machinelearning`.</span></span>

   <span data-ttu-id="1fe6d-181">**Tipo de Função**: selecione **Azure ML**.</span><span class="sxs-lookup"><span data-stu-id="1fe6d-181">**Function Type**: Select **Azure ML**.</span></span>

   <span data-ttu-id="1fe6d-182">**Opção de importação**: selecione **Importar de outra assinatura**.</span><span class="sxs-lookup"><span data-stu-id="1fe6d-182">**Import option**: Select **Import from a different subscription**.</span></span>

   <span data-ttu-id="1fe6d-183">**URL**: insira a URL DO SERVIÇO WEB que você anotou da pasta de trabalho do Excel.</span><span class="sxs-lookup"><span data-stu-id="1fe6d-183">**URL**: Enter the WEB SERVICE URL that you noted down from the Excel workbook.</span></span>

   <span data-ttu-id="1fe6d-184">**Chave**: insira a TECLA DE ACESSO anotada da pasta de trabalho do Excel.</span><span class="sxs-lookup"><span data-stu-id="1fe6d-184">**Key**: Enter the ACCESS KEY that you noted down from the Excel workbook.</span></span>

   ![Adicionar uma função ao trabalho do Stream Analytics no Azure](media/iot-hub-weather-forecast-machine-learning/10_add-function-stream-analytics-job-azure.png)

1. <span data-ttu-id="1fe6d-186">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="1fe6d-186">Click **Create**.</span></span>

### <a name="configure-the-query-of-the-stream-analytics-job"></a><span data-ttu-id="1fe6d-187">Configurar a consulta do trabalho do Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="1fe6d-187">Configure the query of the Stream Analytics job</span></span>

1. <span data-ttu-id="1fe6d-188">Em **Topologia do Trabalho**, clique em **Consulta**.</span><span class="sxs-lookup"><span data-stu-id="1fe6d-188">Under **Job Topology**, click **Query**.</span></span>
1. <span data-ttu-id="1fe6d-189">Substitua o código existente pelo seguinte código:</span><span class="sxs-lookup"><span data-stu-id="1fe6d-189">Replace the existing code with the following code:</span></span>

   ```sql
   WITH machinelearning AS (
      SELECT EventEnqueuedUtcTime, temperature, humidity, machinelearning(temperature, humidity) as result from [YourInputAlias]
   )
   Select System.Timestamp time, CAST (result.[temperature] AS FLOAT) AS temperature, CAST (result.[humidity] AS FLOAT) AS humidity, CAST (result.[Scored Probabilities] AS FLOAT ) AS 'probabalities of rain'
   Into [YourOutputAlias]
   From machinelearning
   ```

   <span data-ttu-id="1fe6d-190">Substitua `[YourInputAlias]` pelo alias de entrada do trabalho.</span><span class="sxs-lookup"><span data-stu-id="1fe6d-190">Replace `[YourInputAlias]` with the input alias of the job.</span></span>

   <span data-ttu-id="1fe6d-191">Substitua `[YourOutputAlias]` pelo alias de saída do trabalho.</span><span class="sxs-lookup"><span data-stu-id="1fe6d-191">Replace `[YourOutputAlias]` with the output alias of the job.</span></span>

1. <span data-ttu-id="1fe6d-192">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="1fe6d-192">Click **Save**.</span></span>

### <a name="run-the-stream-analytics-job"></a><span data-ttu-id="1fe6d-193">Executar o trabalho do Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="1fe6d-193">Run the Stream Analytics job</span></span>

<span data-ttu-id="1fe6d-194">No trabalho do Stream Analytics, clique em **Iniciar** > **Agora** > **Iniciar**.</span><span class="sxs-lookup"><span data-stu-id="1fe6d-194">In the Stream Analytics job, click **Start** > **Now** > **Start**.</span></span> <span data-ttu-id="1fe6d-195">Depois que o trabalho é iniciado com êxito, o status do trabalho muda de **parado** para **executando**.</span><span class="sxs-lookup"><span data-stu-id="1fe6d-195">Once the job successfully starts, the job status changes from **Stopped** to **Running**.</span></span>

![Executar o trabalho do Stream Analytics](media/iot-hub-weather-forecast-machine-learning/11_run-stream-analytics-job-azure.png)

## <a name="use-microsoft-azure-storage-explorer-to-view-the-weather-forecast"></a><span data-ttu-id="1fe6d-197">Usar o Gerenciador de Armazenamento do Microsoft Azure para exibir a previsão do tempo</span><span class="sxs-lookup"><span data-stu-id="1fe6d-197">Use Microsoft Azure Storage Explorer to view the weather forecast</span></span>

<span data-ttu-id="1fe6d-198">Execute o aplicativo cliente para iniciar a coleta e o envio de dados de temperatura e umidade para o Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="1fe6d-198">Run the client application to start collecting and sending temperature and humidity data to your IoT hub.</span></span> <span data-ttu-id="1fe6d-199">Para cada mensagem recebida pelo Hub IoT, o trabalho do Stream Analytics chama o serviço Web de previsão do tempo para produzir a possibilidade de chuva.</span><span class="sxs-lookup"><span data-stu-id="1fe6d-199">For each message that your IoT hub receives, the Stream Analytics job calls the weather forecast web service to produce the chance of rain.</span></span> <span data-ttu-id="1fe6d-200">O resultado é então salvo no armazenamento de blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="1fe6d-200">The result is then saved to your Azure blob storage.</span></span> <span data-ttu-id="1fe6d-201">O Gerenciador de Armazenamento do Azure é uma ferramenta que pode ser usada para exibir o resultado.</span><span class="sxs-lookup"><span data-stu-id="1fe6d-201">Azure Storage Explorer is a tool that you can use to view the result.</span></span>

1. <span data-ttu-id="1fe6d-202">[Baixe e instale o Gerenciador de Armazenamento do Microsoft Azure](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="1fe6d-202">[Download and install Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>
1. <span data-ttu-id="1fe6d-203">Abra o Gerenciador de Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="1fe6d-203">Open Azure Storage Explorer.</span></span>
1. <span data-ttu-id="1fe6d-204">Entre na sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="1fe6d-204">Sign in to your Azure account.</span></span>
1. <span data-ttu-id="1fe6d-205">Selecione sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="1fe6d-205">Select your subscription.</span></span>
1. <span data-ttu-id="1fe6d-206">Clique em sua assinatura > **Contas de Armazenamento** > sua conta de armazenamento > **Contêineres de Blobs** > seu contêiner.</span><span class="sxs-lookup"><span data-stu-id="1fe6d-206">Click your subscription > **Storage Accounts** > your storage account > **Blob Containers** > your container.</span></span>
1. <span data-ttu-id="1fe6d-207">Abra um arquivo .csv para ver o resultado.</span><span class="sxs-lookup"><span data-stu-id="1fe6d-207">Open a .csv file to see the result.</span></span> <span data-ttu-id="1fe6d-208">A última coluna registra a possibilidade de chuva.</span><span class="sxs-lookup"><span data-stu-id="1fe6d-208">The last column records the chance of rain.</span></span>

   ![Obter resultados da previsão do tempo com o Azure Machine Learning](media/iot-hub-weather-forecast-machine-learning/12_get-weather-forecast-result-azure-machine-learning.png)

## <a name="summary"></a><span data-ttu-id="1fe6d-210">Resumo</span><span class="sxs-lookup"><span data-stu-id="1fe6d-210">Summary</span></span>

<span data-ttu-id="1fe6d-211">Você usou bem o Azure Machine Learning para produzir a possibilidade de chuva com base nos dados de temperatura e umidade recebidos pelo Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="1fe6d-211">You’ve successfully used Azure Machine Learning to produce the chance of rain based on the temperature and humidity data that your IoT hub receives.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]