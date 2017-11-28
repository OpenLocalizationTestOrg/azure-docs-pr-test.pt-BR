---
title: "aaaWeather previsão usando o aprendizado de máquina do Azure com dados de IoT Hub | Microsoft Docs"
description: "Use o aprendizado de máquina do Azure toopredict Olá chance de chuva com base em umidade e temperatura Olá seu hub IoT coleta de um sensor de dados."
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
ms.openlocfilehash: 04abe97558ccfc152bae2e0d435033433c0023dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="weather-forecast-using-hello-sensor-data-from-your-iot-hub-in-azure-machine-learning"></a><span data-ttu-id="f6ce3-104">Previsão do tempo usando dados de sensor de saudação do seu hub IoT no aprendizado de máquina do Azure</span><span class="sxs-lookup"><span data-stu-id="f6ce3-104">Weather forecast using hello sensor data from your IoT hub in Azure Machine Learning</span></span>

![Diagrama de ponta a ponta](media/iot-hub-get-started-e2e-diagram/6.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

<span data-ttu-id="f6ce3-106">Aprendizado de máquina é uma técnica de ciência de dados que ajuda os computadores a aprender com as tendências, resultados e existente comportamentos futuras tooforecast de dados.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-106">Machine learning is a technique of data science that helps computers learn from existing data tooforecast future behaviors, outcomes, and trends.</span></span> <span data-ttu-id="f6ce3-107">O aprendizado de máquina do Azure é um serviço em nuvem análise preditiva que torna possível tooquickly criar e implantar modelos de previsão como soluções de análise.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-107">Azure Machine Learning is a cloud predictive analytics service that makes it possible tooquickly create and deploy predictive models as analytics solutions.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="f6ce3-108">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="f6ce3-108">What you learn</span></span>

<span data-ttu-id="f6ce3-109">Você aprenderá como toouse aprendizado de máquina do Azure toodo previsão do tempo (chance de chuva) usando Olá temperatura e umidade dados de seu hub IoT do Azure.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-109">You learn how toouse Azure Machine Learning toodo weather forecast (chance of rain) using hello temperature and humidity data from your Azure IoT hub.</span></span> <span data-ttu-id="f6ce3-110">chance de saudação de chuva é saída de saudação de um modelo de previsão do tempo preparada.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-110">hello chance of rain is hello output of a prepared weather prediction model.</span></span> <span data-ttu-id="f6ce3-111">modelo de saudação se baseia a chance de tooforecast dados históricos de chuva com base em temperatura e umidade.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-111">hello model is built upon historic data tooforecast chance of rain based on temperature and humidity.</span></span>

## <a name="what-you-do"></a><span data-ttu-id="f6ce3-112">O que fazer</span><span class="sxs-lookup"><span data-stu-id="f6ce3-112">What you do</span></span>

- <span data-ttu-id="f6ce3-113">Implante o modelo de previsão do tempo de saudação como um serviço web.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-113">Deploy hello weather prediction model as a web service.</span></span>
- <span data-ttu-id="f6ce3-114">Preparar seu Hub IoT para acesso a dados, adicionando um grupo de consumidores.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-114">Get your IoT hub ready for data access by adding a consumer group.</span></span>
- <span data-ttu-id="f6ce3-115">Criar um trabalho de análise de fluxo e configurar o trabalho Olá para:</span><span class="sxs-lookup"><span data-stu-id="f6ce3-115">Create a Stream Analytics job and configure hello job to:</span></span>
  - <span data-ttu-id="f6ce3-116">Leia dados de temperatura e umidade no Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-116">Read temperature and humidity data from your IoT hub.</span></span>
  - <span data-ttu-id="f6ce3-117">Chame a chance de chuva Olá web serviço tooget hello.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-117">Call hello web service tooget hello rain chance.</span></span>
  - <span data-ttu-id="f6ce3-118">Salve o armazenamento de BLOBs do Azure tooan resultados da saudação.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-118">Save hello result tooan Azure blob storage.</span></span>
- <span data-ttu-id="f6ce3-119">Use a previsão do tempo de saudação do Microsoft Azure Storage Explorer tooview.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-119">Use Microsoft Azure Storage Explorer tooview hello weather forecast.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="f6ce3-120">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="f6ce3-120">What you need</span></span>

- <span data-ttu-id="f6ce3-121">Tutorial [configurar seu dispositivo](iot-hub-raspberry-pi-kit-node-get-started.md) concluída que abrange Olá requisitos a seguir:</span><span class="sxs-lookup"><span data-stu-id="f6ce3-121">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers hello following requirements:</span></span>
  - <span data-ttu-id="f6ce3-122">Uma assinatura ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-122">An active Azure subscription.</span></span>
  - <span data-ttu-id="f6ce3-123">Um hub IoT do Azure em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-123">An Azure IoT hub under your subscription.</span></span>
  - <span data-ttu-id="f6ce3-124">Um aplicativo cliente que envia o hub do mensagens tooyour IoT do Azure.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-124">A client application that sends messages tooyour Azure IoT hub.</span></span>
- <span data-ttu-id="f6ce3-125">Uma conta do Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-125">An Azure Machine Learning Studio account.</span></span> <span data-ttu-id="f6ce3-126">([Experimente o Machine Learning Studio gratuitamente](https://studio.azureml.net/)).</span><span class="sxs-lookup"><span data-stu-id="f6ce3-126">([Try Machine Learning Studio for free](https://studio.azureml.net/)).</span></span>

## <a name="deploy-hello-weather-prediction-model-as-a-web-service"></a><span data-ttu-id="f6ce3-127">Implantar o modelo de previsão do tempo de saudação como um serviço web</span><span class="sxs-lookup"><span data-stu-id="f6ce3-127">Deploy hello weather prediction model as a web service</span></span>

1. <span data-ttu-id="f6ce3-128">Vá toohello [página de modelo de previsão do tempo](https://gallery.cortanaintelligence.com/Experiment/Weather-prediction-model-1).</span><span class="sxs-lookup"><span data-stu-id="f6ce3-128">Go toohello [weather prediction model page](https://gallery.cortanaintelligence.com/Experiment/Weather-prediction-model-1).</span></span>
1. <span data-ttu-id="f6ce3-129">Clique em **Abrir no Studio** no Microsoft Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-129">Click **Open in Studio** in Microsoft Azure Machine Learning Studio.</span></span>
   <span data-ttu-id="f6ce3-130">![Página de modelo de previsão Olá abrir clima na Galeria de inteligência de Cortana](media/iot-hub-weather-forecast-machine-learning/2_weather-prediction-model-in-cortana-intelligence-gallery.png)</span><span class="sxs-lookup"><span data-stu-id="f6ce3-130">![Open hello weather prediction model page in Cortana Intelligence Gallery](media/iot-hub-weather-forecast-machine-learning/2_weather-prediction-model-in-cortana-intelligence-gallery.png)</span></span>
1. <span data-ttu-id="f6ce3-131">Clique em **executar** toovalidate Olá etapas no modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-131">Click **Run** toovalidate hello steps in hello model.</span></span> <span data-ttu-id="f6ce3-132">Esta etapa pode levar toocomplete 2 minutos.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-132">This step might take 2 minutes toocomplete.</span></span>
   <span data-ttu-id="f6ce3-133">![Modelo de previsão de clima Olá abrir no estúdio de aprendizado de máquina do Azure](media/iot-hub-weather-forecast-machine-learning/3_open-weather-prediction-model-in-azure-machine-learning-studio.png)</span><span class="sxs-lookup"><span data-stu-id="f6ce3-133">![Open hello weather prediction model in Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/3_open-weather-prediction-model-in-azure-machine-learning-studio.png)</span></span>
1. <span data-ttu-id="f6ce3-134">Clique em **CONFIGURAR SERVIÇO WEB** > **Serviço Web Preditivo**.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-134">Click **SET UP WEB SERVICE** > **Predictive Web Service**.</span></span>
   <span data-ttu-id="f6ce3-135">![Implantar o modelo de previsão de clima Olá no estúdio de aprendizado de máquina do Azure](media/iot-hub-weather-forecast-machine-learning/4-deploy-weather-prediction-model-in-azure-machine-learning-studio.png)</span><span class="sxs-lookup"><span data-stu-id="f6ce3-135">![Deploy hello weather prediction model in Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/4-deploy-weather-prediction-model-in-azure-machine-learning-studio.png)</span></span>
1. <span data-ttu-id="f6ce3-136">No diagrama de hello, arraste Olá **Web serviço entrada** módulo em algum lugar próximo Olá **modelo de pontuação** módulo.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-136">In hello diagram, drag hello **Web service input** module somewhere near hello **Score Model** module.</span></span>
1. <span data-ttu-id="f6ce3-137">Conectar Olá **Web serviço entrada** módulo toohello **modelo de pontuação** módulo.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-137">Connect hello **Web service input** module toohello **Score Model** module.</span></span>
   <span data-ttu-id="f6ce3-138">![Conectar dois módulos no Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/13_connect-modules-azure-machine-learning-studio.png)</span><span class="sxs-lookup"><span data-stu-id="f6ce3-138">![Connect two modules in Azure Machine Learning Studio](media/iot-hub-weather-forecast-machine-learning/13_connect-modules-azure-machine-learning-studio.png)</span></span>
1. <span data-ttu-id="f6ce3-139">Clique em **executar** toovalidate Olá etapas no modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-139">Click **RUN** toovalidate hello steps in hello model.</span></span>
1. <span data-ttu-id="f6ce3-140">Clique em **IMPLANTAR o serviço da WEB** modelo de saudação toodeploy como um serviço web.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-140">Click **DEPLOY WEB SERVICE** toodeploy hello model as a web service.</span></span>
1. <span data-ttu-id="f6ce3-141">No painel de saudação do modelo hello, baixe Olá **Excel 2010 ou pasta de trabalho anterior** para **solicitação/resposta**.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-141">On hello dashboard of hello model, download hello **Excel 2010 or earlier workbook** for **REQUEST/RESPONSE**.</span></span>

   > [!Note]
   > <span data-ttu-id="f6ce3-142">Certifique-se de que você baixe Olá **Excel 2010 ou pasta de trabalho anterior** mesmo se você estiver executando uma versão posterior do Excel em seu computador.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-142">Ensure that you download hello **Excel 2010 or earlier workbook** even if you are running a later version of Excel on your computer.</span></span>

   ![Baixar hello Excel para o ponto de extremidade de resposta da solicitação de saudação](media/iot-hub-weather-forecast-machine-learning/5_download-endpoint-app-excel-for-request-response.png)

1. <span data-ttu-id="f6ce3-144">Abra a pasta de trabalho do Excel hello, anote Olá **URL do serviço WEB** e **chave de acesso**.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-144">Open hello Excel workbook, make a note of hello **WEB SERVICE URL** and **ACCESS KEY**.</span></span>

[!INCLUDE [iot-hub-get-started-create-consumer-group](../../includes/iot-hub-get-started-create-consumer-group.md)]

## <a name="create-configure-and-run-a-stream-analytics-job"></a><span data-ttu-id="f6ce3-145">Criar, configurar e executar um trabalho do Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="f6ce3-145">Create, configure, and run a Stream Analytics job</span></span>

### <a name="create-a-stream-analytics-job"></a><span data-ttu-id="f6ce3-146">Criar um trabalho de Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="f6ce3-146">Create a Stream Analytics job</span></span>

1. <span data-ttu-id="f6ce3-147">Em Olá [portal do Azure](https://ms.portal.azure.com/), clique em **novo** > **Internet das coisas** > **trabalho do Stream Analytics**.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-147">In hello [Azure portal](https://ms.portal.azure.com/), click **New** > **Internet of Things** > **Stream Analytics job**.</span></span>
1. <span data-ttu-id="f6ce3-148">Digite hello informações de trabalho Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-148">Enter hello following information for hello job.</span></span>

   <span data-ttu-id="f6ce3-149">**Nome do trabalho**: nome de saudação do trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-149">**Job name**: hello name of hello job.</span></span> <span data-ttu-id="f6ce3-150">Olá nome deve ser exclusivo.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-150">hello name must be globally unique.</span></span>

   <span data-ttu-id="f6ce3-151">**Grupo de recursos**: Use Olá mesmo grupo de recursos que usa o hub IoT.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-151">**Resource group**: Use hello same resource group that your IoT hub uses.</span></span>

   <span data-ttu-id="f6ce3-152">**Local**: Use Olá mesmo local que o grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-152">**Location**: Use hello same location as your resource group.</span></span>

   <span data-ttu-id="f6ce3-153">**PIN toodashboard**: Selecione essa opção para o hub de IoT tooyour fácil acesso no painel de saudação.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-153">**Pin toodashboard**: Check this option for easy access tooyour IoT hub from hello dashboard.</span></span>

   ![Criar um trabalho do Stream Analytics no Azure](media/iot-hub-weather-forecast-machine-learning/7_create-stream-analytics-job-azure.png)

1. <span data-ttu-id="f6ce3-155">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-155">Click **Create**.</span></span>

### <a name="add-an-input-toohello-stream-analytics-job"></a><span data-ttu-id="f6ce3-156">Adicionar um trabalho de análise de fluxo de entrada toohello</span><span class="sxs-lookup"><span data-stu-id="f6ce3-156">Add an input toohello Stream Analytics job</span></span>

1. <span data-ttu-id="f6ce3-157">Trabalho de análise de fluxo aberto hello.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-157">Open hello Stream Analytics job.</span></span>
1. <span data-ttu-id="f6ce3-158">Em **Topologia do Trabalho**, clique em **Entradas**.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-158">Under **Job Topology**, click **Inputs**.</span></span>
1. <span data-ttu-id="f6ce3-159">Em Olá **entradas** painel, clique em **adicionar**e, em seguida, digite Olá informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="f6ce3-159">In hello **Inputs** pane, click **Add**, and then enter hello following information:</span></span>

   <span data-ttu-id="f6ce3-160">**Alias de entrada**: alias exclusivo Olá Olá entrada.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-160">**Input alias**: hello unique alias for hello input.</span></span>

   <span data-ttu-id="f6ce3-161">**Origem**: selecione **hub IoT**.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-161">**Source**: Select **IoT hub**.</span></span>

   <span data-ttu-id="f6ce3-162">**Grupo de consumidores**: grupo de consumidores Olá selecione criado por você.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-162">**Consumer group**: Select hello consumer group you created.</span></span>

   ![Adicionar um trabalho de análise de fluxo de entrada toohello no Azure](media/iot-hub-weather-forecast-machine-learning/8_add-input-stream-analytics-job-azure.png)

1. <span data-ttu-id="f6ce3-164">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-164">Click **Create**.</span></span>

### <a name="add-an-output-toohello-stream-analytics-job"></a><span data-ttu-id="f6ce3-165">Adicionar um trabalho de análise de fluxo de toohello de saída</span><span class="sxs-lookup"><span data-stu-id="f6ce3-165">Add an output toohello Stream Analytics job</span></span>

1. <span data-ttu-id="f6ce3-166">Em **Topologia do Trabalho**, clique em **Saídas**.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-166">Under **Job Topology**, click **Outputs**.</span></span>
1. <span data-ttu-id="f6ce3-167">Em Olá **saídas** painel, clique em **adicionar**e, em seguida, digite Olá informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="f6ce3-167">In hello **Outputs** pane, click **Add**, and then enter hello following information:</span></span>

   <span data-ttu-id="f6ce3-168">**Alias de saída**: alias exclusivo de saudação para saída de hello.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-168">**Output alias**: hello unique alias for hello output.</span></span>

   <span data-ttu-id="f6ce3-169">**Coletor**: selecione **Armazenamento de Blobs**.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-169">**Sink**: Select **Blob Storage**.</span></span>

   <span data-ttu-id="f6ce3-170">**Conta de armazenamento**: Olá conta de armazenamento para o armazenamento de blob.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-170">**Storage account**: hello storage account for your blob storage.</span></span> <span data-ttu-id="f6ce3-171">Você pode criar uma conta de armazenamento ou usar uma existente.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-171">You can create a storage account or use an existing one.</span></span>

   <span data-ttu-id="f6ce3-172">**Contêiner**: contêiner Olá onde blob Olá é salvo.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-172">**Container**: hello container where hello blob is saved.</span></span> <span data-ttu-id="f6ce3-173">Você pode criar um contêiner ou usar um existente.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-173">You can create a container or use an existing one.</span></span>

   <span data-ttu-id="f6ce3-174">**Formato de serialização de evento**: selecione **CSV**.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-174">**Event serialization format**: Select **CSV**.</span></span>

   ![Adicionar um trabalho de análise de fluxo de toohello de saída no Azure](media/iot-hub-weather-forecast-machine-learning/9_add-output-stream-analytics-job-azure.png)

1. <span data-ttu-id="f6ce3-176">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-176">Click **Create**.</span></span>

### <a name="add-a-function-toohello-stream-analytics-job-toocall-hello-web-service-you-deployed"></a><span data-ttu-id="f6ce3-177">Adicionar uma função toohello serviço Stream Analytics trabalho toocall Olá web implantado</span><span class="sxs-lookup"><span data-stu-id="f6ce3-177">Add a function toohello Stream Analytics job toocall hello web service you deployed</span></span>

1. <span data-ttu-id="f6ce3-178">Em **Topologia de Trabalho**, clique em **Funções** > **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-178">Under **Job Topology**, click **Functions** > **Add**.</span></span>
1. <span data-ttu-id="f6ce3-179">Digite hello informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="f6ce3-179">Enter hello following information:</span></span>

   <span data-ttu-id="f6ce3-180">**Alias da Função**: insira `machinelearning`.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-180">**Function Alias**: Enter `machinelearning`.</span></span>

   <span data-ttu-id="f6ce3-181">**Tipo de Função**: selecione **Azure ML**.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-181">**Function Type**: Select **Azure ML**.</span></span>

   <span data-ttu-id="f6ce3-182">**Opção de importação**: selecione **Importar de outra assinatura**.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-182">**Import option**: Select **Import from a different subscription**.</span></span>

   <span data-ttu-id="f6ce3-183">**URL**: insira Olá URL do serviço WEB que você anotou para baixo da pasta de trabalho do Excel hello.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-183">**URL**: Enter hello WEB SERVICE URL that you noted down from hello Excel workbook.</span></span>

   <span data-ttu-id="f6ce3-184">**Chave**: insira Olá chave de acesso que você anotou para baixo da pasta de trabalho do Excel hello.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-184">**Key**: Enter hello ACCESS KEY that you noted down from hello Excel workbook.</span></span>

   ![Adicionar um trabalho de análise de fluxo de toohello de função no Azure](media/iot-hub-weather-forecast-machine-learning/10_add-function-stream-analytics-job-azure.png)

1. <span data-ttu-id="f6ce3-186">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-186">Click **Create**.</span></span>

### <a name="configure-hello-query-of-hello-stream-analytics-job"></a><span data-ttu-id="f6ce3-187">Configurar consulta de saudação do trabalho do Stream Analytics Olá</span><span class="sxs-lookup"><span data-stu-id="f6ce3-187">Configure hello query of hello Stream Analytics job</span></span>

1. <span data-ttu-id="f6ce3-188">Em **Topologia do Trabalho**, clique em **Consulta**.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-188">Under **Job Topology**, click **Query**.</span></span>
1. <span data-ttu-id="f6ce3-189">Substitua código existente Olá Olá código a seguir:</span><span class="sxs-lookup"><span data-stu-id="f6ce3-189">Replace hello existing code with hello following code:</span></span>

   ```sql
   WITH machinelearning AS (
      SELECT EventEnqueuedUtcTime, temperature, humidity, machinelearning(temperature, humidity) as result from [YourInputAlias]
   )
   Select System.Timestamp time, CAST (result.[temperature] AS FLOAT) AS temperature, CAST (result.[humidity] AS FLOAT) AS humidity, CAST (result.[Scored Probabilities] AS FLOAT ) AS 'probabalities of rain'
   Into [YourOutputAlias]
   From machinelearning
   ```

   <span data-ttu-id="f6ce3-190">Substituir `[YourInputAlias]` com alias Olá de entrada do trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-190">Replace `[YourInputAlias]` with hello input alias of hello job.</span></span>

   <span data-ttu-id="f6ce3-191">Substituir `[YourOutputAlias]` com hello alias de saída do trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-191">Replace `[YourOutputAlias]` with hello output alias of hello job.</span></span>

1. <span data-ttu-id="f6ce3-192">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-192">Click **Save**.</span></span>

### <a name="run-hello-stream-analytics-job"></a><span data-ttu-id="f6ce3-193">Executar trabalho do Stream Analytics Olá</span><span class="sxs-lookup"><span data-stu-id="f6ce3-193">Run hello Stream Analytics job</span></span>

<span data-ttu-id="f6ce3-194">No trabalho de análise de fluxo de saudação, clique em **iniciar** > **agora** > **iniciar**.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-194">In hello Stream Analytics job, click **Start** > **Now** > **Start**.</span></span> <span data-ttu-id="f6ce3-195">Depois que o trabalho de saudação é iniciado com êxito, o status do trabalho Olá muda de **parado** muito**executando**.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-195">Once hello job successfully starts, hello job status changes from **Stopped** too**Running**.</span></span>

![Executar trabalho do Stream Analytics Olá](media/iot-hub-weather-forecast-machine-learning/11_run-stream-analytics-job-azure.png)

## <a name="use-microsoft-azure-storage-explorer-tooview-hello-weather-forecast"></a><span data-ttu-id="f6ce3-197">Usar a previsão do tempo de saudação do Microsoft Azure Storage Explorer tooview</span><span class="sxs-lookup"><span data-stu-id="f6ce3-197">Use Microsoft Azure Storage Explorer tooview hello weather forecast</span></span>

<span data-ttu-id="f6ce3-198">Execute Olá cliente aplicativo toostart coletar e enviar temperatura e umidade hub de IoT tooyour de dados.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-198">Run hello client application toostart collecting and sending temperature and humidity data tooyour IoT hub.</span></span> <span data-ttu-id="f6ce3-199">Para cada mensagem que recebe o hub IoT, o trabalho do Stream Analytics Olá chama Olá previsão do tempo da web serviço tooproduce Olá chance de chuva.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-199">For each message that your IoT hub receives, hello Stream Analytics job calls hello weather forecast web service tooproduce hello chance of rain.</span></span> <span data-ttu-id="f6ce3-200">resultado de saudação é salvo, em seguida, tooyour armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-200">hello result is then saved tooyour Azure blob storage.</span></span> <span data-ttu-id="f6ce3-201">Azure Storage Explorer é uma ferramenta que você pode usar o resultado de saudação tooview.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-201">Azure Storage Explorer is a tool that you can use tooview hello result.</span></span>

1. <span data-ttu-id="f6ce3-202">[Baixe e instale o Gerenciador de Armazenamento do Microsoft Azure](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="f6ce3-202">[Download and install Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>
1. <span data-ttu-id="f6ce3-203">Abra o Gerenciador de Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-203">Open Azure Storage Explorer.</span></span>
1. <span data-ttu-id="f6ce3-204">Entre tooyour conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-204">Sign in tooyour Azure account.</span></span>
1. <span data-ttu-id="f6ce3-205">Selecione sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-205">Select your subscription.</span></span>
1. <span data-ttu-id="f6ce3-206">Clique em sua assinatura > **Contas de Armazenamento** > sua conta de armazenamento > **Contêineres de Blobs** > seu contêiner.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-206">Click your subscription > **Storage Accounts** > your storage account > **Blob Containers** > your container.</span></span>
1. <span data-ttu-id="f6ce3-207">Abra um resultado de saudação do toosee de arquivo. csv.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-207">Open a .csv file toosee hello result.</span></span> <span data-ttu-id="f6ce3-208">os registros de última coluna Olá Olá chance de chuva.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-208">hello last column records hello chance of rain.</span></span>

   ![Obter resultados da previsão do tempo com o Azure Machine Learning](media/iot-hub-weather-forecast-machine-learning/12_get-weather-forecast-result-azure-machine-learning.png)

## <a name="summary"></a><span data-ttu-id="f6ce3-210">Resumo</span><span class="sxs-lookup"><span data-stu-id="f6ce3-210">Summary</span></span>

<span data-ttu-id="f6ce3-211">Você usou com êxito a chance de saudação do aprendizado de máquina do Azure tooproduce de chuva com base nos dados de temperatura e umidade Olá que recebe o hub IoT.</span><span class="sxs-lookup"><span data-stu-id="f6ce3-211">You’ve successfully used Azure Machine Learning tooproduce hello chance of rain based on hello temperature and humidity data that your IoT hub receives.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]