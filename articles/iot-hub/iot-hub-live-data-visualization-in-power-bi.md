---
title: "tempo de aaaReal visualização de dados de sensor do Azure IoT Hub – Power BI | Microsoft Docs"
description: Use o Power BI toovisualize temperatura e umidade dados coletados de sensor hello e enviados tooyour Azure IoT hub.
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
ms.openlocfilehash: d79ce757a9f2ab7a4744e8a0c523106e0f72cecd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-real-time-sensor-data-from-azure-iot-hub-using-power-bi"></a><span data-ttu-id="3afa8-104">Visualizar dados de sensor em tempo real do Hub IoT usando o Power BI</span><span class="sxs-lookup"><span data-stu-id="3afa8-104">Visualize real-time sensor data from Azure IoT Hub using Power BI</span></span>

![Diagrama de ponta a ponta](media/iot-hub-get-started-e2e-diagram/4.png)


[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

## <a name="what-you-learn"></a><span data-ttu-id="3afa8-106">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="3afa8-106">What you learn</span></span>

<span data-ttu-id="3afa8-107">Você aprenderá como dados de sensor em tempo real de toovisualize que recebe o hub IoT do Azure pelo Power BI.</span><span class="sxs-lookup"><span data-stu-id="3afa8-107">You learn how toovisualize real-time sensor data that your Azure IoT hub receives by Power BI.</span></span> <span data-ttu-id="3afa8-108">Se você quiser tootry visualizar dados saudação em seu hub IoT com aplicativos da Web, consulte [dados do sensor em tempo real do toovisualize aplicativos de Web do Azure de uso do Azure IoT Hub](iot-hub-live-data-visualization-in-web-apps.md).</span><span class="sxs-lookup"><span data-stu-id="3afa8-108">If you want tootry visualize hello data in your IoT hub with Web Apps, please see [Use Azure Web Apps toovisualize real-time sensor data from Azure IoT Hub](iot-hub-live-data-visualization-in-web-apps.md).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="3afa8-109">O que fazer</span><span class="sxs-lookup"><span data-stu-id="3afa8-109">What you do</span></span>

- <span data-ttu-id="3afa8-110">Preparar seu Hub IoT para acesso a dados, adicionando um grupo de consumidores.</span><span class="sxs-lookup"><span data-stu-id="3afa8-110">Get your IoT hub ready for data access by adding a consumer group.</span></span>
- <span data-ttu-id="3afa8-111">Criar, configurar e executar um trabalho do Stream Analytics para transferência de dados de sua tooyour de hub IoT conta do Power BI.</span><span class="sxs-lookup"><span data-stu-id="3afa8-111">Create, configure and run a Stream Analytics job for data transfer from your IoT hub tooyour Power BI account.</span></span>
- <span data-ttu-id="3afa8-112">Criar e publicar um dado de saudação do Power BI relatório toovisualize.</span><span class="sxs-lookup"><span data-stu-id="3afa8-112">Create and publish a Power BI report toovisualize hello data.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="3afa8-113">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="3afa8-113">What you need</span></span>

- <span data-ttu-id="3afa8-114">Tutorial [configurar seu dispositivo](iot-hub-raspberry-pi-kit-node-get-started.md) concluída que abrange Olá requisitos a seguir:</span><span class="sxs-lookup"><span data-stu-id="3afa8-114">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers hello following requirements:</span></span>
  - <span data-ttu-id="3afa8-115">Uma assinatura ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="3afa8-115">An active Azure subscription.</span></span>
  - <span data-ttu-id="3afa8-116">Um hub IoT do Azure em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="3afa8-116">An Azure IoT hub under your subscription.</span></span>
  - <span data-ttu-id="3afa8-117">Um aplicativo cliente que envia o hub do mensagens tooyour IoT do Azure.</span><span class="sxs-lookup"><span data-stu-id="3afa8-117">A client application that sends messages tooyour Azure IoT hub.</span></span>
- <span data-ttu-id="3afa8-118">Uma conta do Power BI.</span><span class="sxs-lookup"><span data-stu-id="3afa8-118">A Power BI account.</span></span> <span data-ttu-id="3afa8-119">([Experimente gratuitamente o Power BI](https://powerbi.microsoft.com/))</span><span class="sxs-lookup"><span data-stu-id="3afa8-119">([Try Power BI for free](https://powerbi.microsoft.com/))</span></span>

[!INCLUDE [iot-hub-get-started-create-consumer-group](../../includes/iot-hub-get-started-create-consumer-group.md)]

## <a name="create-configure-and-run-a-stream-analytics-job"></a><span data-ttu-id="3afa8-120">Criar, configurar e executar um trabalho do Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="3afa8-120">Create, configure, and run a Stream Analytics job</span></span>

### <a name="create-a-stream-analytics-job"></a><span data-ttu-id="3afa8-121">Criar um trabalho de Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="3afa8-121">Create a Stream Analytics job</span></span>

1. <span data-ttu-id="3afa8-122">No hello portal do Azure, clique em Novo > Internet das coisas > trabalho do Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="3afa8-122">In hello Azure portal, click New > Internet of Things > Stream Analytics job.</span></span>
1. <span data-ttu-id="3afa8-123">Digite hello informações de trabalho Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="3afa8-123">Enter hello following information for hello job.</span></span>

   <span data-ttu-id="3afa8-124">**Nome do trabalho**: nome de saudação do trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="3afa8-124">**Job name**: hello name of hello job.</span></span> <span data-ttu-id="3afa8-125">Olá nome deve ser exclusivo.</span><span class="sxs-lookup"><span data-stu-id="3afa8-125">hello name must be globally unique.</span></span>

   <span data-ttu-id="3afa8-126">**Grupo de recursos**: Use Olá mesmo grupo de recursos que usa o hub IoT.</span><span class="sxs-lookup"><span data-stu-id="3afa8-126">**Resource group**: Use hello same resource group that your IoT hub uses.</span></span>

   <span data-ttu-id="3afa8-127">**Local**: Use Olá mesmo local que o grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="3afa8-127">**Location**: Use hello same location as your resource group.</span></span>

   <span data-ttu-id="3afa8-128">**PIN toodashboard**: Selecione essa opção para o hub de IoT tooyour fácil acesso no painel de saudação.</span><span class="sxs-lookup"><span data-stu-id="3afa8-128">**Pin toodashboard**: Check this option for easy access tooyour IoT hub from hello dashboard.</span></span>

   ![Criar um trabalho do Stream Analytics no Azure](media/iot-hub-live-data-visualization-in-power-bi/2_create-stream-analytics-job-azure.png)

1. <span data-ttu-id="3afa8-130">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="3afa8-130">Click **Create**.</span></span>

### <a name="add-an-input-toohello-stream-analytics-job"></a><span data-ttu-id="3afa8-131">Adicionar um trabalho de análise de fluxo de entrada toohello</span><span class="sxs-lookup"><span data-stu-id="3afa8-131">Add an input toohello Stream Analytics job</span></span>

1. <span data-ttu-id="3afa8-132">Trabalho de análise de fluxo aberto hello.</span><span class="sxs-lookup"><span data-stu-id="3afa8-132">Open hello Stream Analytics job.</span></span>
1. <span data-ttu-id="3afa8-133">Em **Topologia do Trabalho**, clique em **Entradas**.</span><span class="sxs-lookup"><span data-stu-id="3afa8-133">Under **Job Topology**, click **Inputs**.</span></span>
1. <span data-ttu-id="3afa8-134">Em Olá **entradas** painel, clique em **adicionar**e, em seguida, digite Olá informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="3afa8-134">In hello **Inputs** pane, click **Add**, and then enter hello following information:</span></span>

   <span data-ttu-id="3afa8-135">**Alias de entrada**: alias exclusivo Olá Olá entrada.</span><span class="sxs-lookup"><span data-stu-id="3afa8-135">**Input alias**: hello unique alias for hello input.</span></span>

   <span data-ttu-id="3afa8-136">**Origem**: selecione **hub IoT**.</span><span class="sxs-lookup"><span data-stu-id="3afa8-136">**Source**: Select **IoT hub**.</span></span>

   <span data-ttu-id="3afa8-137">**Grupo de consumidores**: grupo de consumidores Olá selecione você acabou de criar.</span><span class="sxs-lookup"><span data-stu-id="3afa8-137">**Consumer group**: Select hello consumer group you just created.</span></span>
1. <span data-ttu-id="3afa8-138">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="3afa8-138">Click **Create**.</span></span>

   ![Adicionar um trabalho de análise de fluxo de entrada tooa no Azure](media/iot-hub-live-data-visualization-in-power-bi/3_add-input-to-stream-analytics-job-azure.png)

### <a name="add-an-output-toohello-stream-analytics-job"></a><span data-ttu-id="3afa8-140">Adicionar um trabalho de análise de fluxo de toohello de saída</span><span class="sxs-lookup"><span data-stu-id="3afa8-140">Add an output toohello Stream Analytics job</span></span>

1. <span data-ttu-id="3afa8-141">Em **Topologia do Trabalho**, clique em **Saídas**.</span><span class="sxs-lookup"><span data-stu-id="3afa8-141">Under **Job Topology**, click **Outputs**.</span></span>
1. <span data-ttu-id="3afa8-142">Em Olá **saídas** painel, clique em **adicionar**e, em seguida, digite Olá informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="3afa8-142">In hello **Outputs** pane, click **Add**, and then enter hello following information:</span></span>

   <span data-ttu-id="3afa8-143">**Alias de saída**: alias exclusivo de saudação para saída de hello.</span><span class="sxs-lookup"><span data-stu-id="3afa8-143">**Output alias**: hello unique alias for hello output.</span></span>

   <span data-ttu-id="3afa8-144">**Coletor**: selecione **Power BI**.</span><span class="sxs-lookup"><span data-stu-id="3afa8-144">**Sink**: Select **Power BI**.</span></span>
1. <span data-ttu-id="3afa8-145">Clique em **Autorizar** e depois entre na sua conta do Power BI.</span><span class="sxs-lookup"><span data-stu-id="3afa8-145">Click **Authorize**, and then sign into your Power BI account.</span></span>
1. <span data-ttu-id="3afa8-146">Uma vez autorizado, digite Olá informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="3afa8-146">Once authorized, enter hello following information:</span></span>

   <span data-ttu-id="3afa8-147">**Espaço de trabalho de grupo**: selecione o espaço de trabalho do grupo de destino.</span><span class="sxs-lookup"><span data-stu-id="3afa8-147">**Group Workspace**: Select your target group workspace.</span></span>

   <span data-ttu-id="3afa8-148">**Nome do Conjunto de Dados**: insira um nome de conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="3afa8-148">**Dataset Name**: Enter a dataset name.</span></span>

   <span data-ttu-id="3afa8-149">**Nome da Tabela**: insira um nome de tabela.</span><span class="sxs-lookup"><span data-stu-id="3afa8-149">**Table Name**: Enter a table name.</span></span>
1. <span data-ttu-id="3afa8-150">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="3afa8-150">Click **Create**.</span></span>

   ![Adicionar um trabalho de análise de fluxo de tooa de saída no Azure](media/iot-hub-live-data-visualization-in-power-bi/4_add-output-to-stream-analytics-job-azure.png)

### <a name="configure-hello-query-of-hello-stream-analytics-job"></a><span data-ttu-id="3afa8-152">Configurar consulta de saudação do trabalho do Stream Analytics Olá</span><span class="sxs-lookup"><span data-stu-id="3afa8-152">Configure hello query of hello Stream Analytics job</span></span>

1. <span data-ttu-id="3afa8-153">Em **Topologia do Trabalho**, clique em **Consulta**.</span><span class="sxs-lookup"><span data-stu-id="3afa8-153">Under **Job Topology**, click **Query**.</span></span>
1. <span data-ttu-id="3afa8-154">Substituir `[YourInputAlias]` com alias Olá de entrada do trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="3afa8-154">Replace `[YourInputAlias]` with hello input alias of hello job.</span></span>
1. <span data-ttu-id="3afa8-155">Substituir `[YourOutputAlias]` com hello alias de saída do trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="3afa8-155">Replace `[YourOutputAlias]` with hello output alias of hello job.</span></span>
1. <span data-ttu-id="3afa8-156">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="3afa8-156">Click **Save**.</span></span>

   ![Adicionar um trabalho de análise de fluxo de tooa de consulta no Azure](media/iot-hub-live-data-visualization-in-power-bi/5_add-query-stream-analytics-job-azure.png)

### <a name="run-hello-stream-analytics-job"></a><span data-ttu-id="3afa8-158">Executar trabalho do Stream Analytics Olá</span><span class="sxs-lookup"><span data-stu-id="3afa8-158">Run hello Stream Analytics job</span></span>

<span data-ttu-id="3afa8-159">No trabalho de análise de fluxo de saudação, clique em **iniciar** > **agora** > **iniciar**.</span><span class="sxs-lookup"><span data-stu-id="3afa8-159">In hello Stream Analytics job, click **Start** > **Now** > **Start**.</span></span> <span data-ttu-id="3afa8-160">Depois que o trabalho de saudação é iniciado com êxito, o status do trabalho Olá muda de **parado** muito**executando**.</span><span class="sxs-lookup"><span data-stu-id="3afa8-160">Once hello job successfully starts, hello job status changes from **Stopped** too**Running**.</span></span>

![Executar um trabalho do Stream Analytics no Azure](media/iot-hub-live-data-visualization-in-power-bi/6_run-stream-analytics-job-azure.png)

## <a name="create-and-publish-a-power-bi-report-toovisualize-hello-data"></a><span data-ttu-id="3afa8-162">Criar e publicar um dado de saudação do Power BI relatório toovisualize</span><span class="sxs-lookup"><span data-stu-id="3afa8-162">Create and publish a Power BI report toovisualize hello data</span></span>

1. <span data-ttu-id="3afa8-163">Certifique-se de que o aplicativo de exemplo hello está em execução no seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="3afa8-163">Ensure hello sample application is running on your device.</span></span> <span data-ttu-id="3afa8-164">Se não, você pode consultar toohello tutoriais em [configurar seu dispositivo](https://docs.microsoft.com/azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started).</span><span class="sxs-lookup"><span data-stu-id="3afa8-164">If not, you can refer toohello tutorials under [Setup your device](https://docs.microsoft.com/azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started).</span></span>
1. <span data-ttu-id="3afa8-165">Entrar tooyour [Power BI](https://powerbi.microsoft.com/en-us/) conta.</span><span class="sxs-lookup"><span data-stu-id="3afa8-165">Sign in tooyour [Power BI](https://powerbi.microsoft.com/en-us/) account.</span></span>
1. <span data-ttu-id="3afa8-166">Acesse o espaço de trabalho de grupo de toohello que você definiu quando criou saída Olá para o trabalho de análise de fluxo de saudação.</span><span class="sxs-lookup"><span data-stu-id="3afa8-166">Go toohello group workspace that you set when you created hello output for hello Stream Analytics job.</span></span>
1. <span data-ttu-id="3afa8-167">Clique em **Conjuntos de dados de streaming**.</span><span class="sxs-lookup"><span data-stu-id="3afa8-167">Click **Streaming datasets**.</span></span>

   <span data-ttu-id="3afa8-168">Você deve ver o dataset Olá listado que você especificou quando criou a saudação de saída para o trabalho de análise de fluxo de saudação.</span><span class="sxs-lookup"><span data-stu-id="3afa8-168">You should see hello listed dataset that you specified when you created hello output for hello Stream Analytics job.</span></span>
1. <span data-ttu-id="3afa8-169">Em **ações**, clique em toocreate de ícone Olá primeiro um relatório.</span><span class="sxs-lookup"><span data-stu-id="3afa8-169">Under **ACTIONS**, click hello first icon toocreate a report.</span></span>

   ![Criar um relatório do Microsoft Power BI](media/iot-hub-live-data-visualization-in-power-bi/7_create-power-bi-report-microsoft.png)

1. <span data-ttu-id="3afa8-171">Crie uma temperatura em tempo real do tooshow de gráfico de linha ao longo do tempo.</span><span class="sxs-lookup"><span data-stu-id="3afa8-171">Create a line chart tooshow real-time temperature over time.</span></span>
   1. <span data-ttu-id="3afa8-172">Na página de criação de relatório hello, adicione um gráfico de linhas.</span><span class="sxs-lookup"><span data-stu-id="3afa8-172">On hello report creation page, add a line chart.</span></span>
   1. <span data-ttu-id="3afa8-173">Em Olá **campos** painel, expanda a tabela Olá que você especificou quando criou a saída Olá para o trabalho de análise de fluxo de saudação.</span><span class="sxs-lookup"><span data-stu-id="3afa8-173">On hello **Fields** pane, expand hello table that you specified when you created hello output for hello Stream Analytics job.</span></span>
   1. <span data-ttu-id="3afa8-174">Arraste **EventEnqueuedUtcTime** muito**eixo** em Olá **visualizações** painel.</span><span class="sxs-lookup"><span data-stu-id="3afa8-174">Drag **EventEnqueuedUtcTime** too**Axis** on hello **Visualizations** pane.</span></span>
   1. <span data-ttu-id="3afa8-175">Arraste **temperatura** muito**valores**.</span><span class="sxs-lookup"><span data-stu-id="3afa8-175">Drag **temperature** too**Values**.</span></span>

      <span data-ttu-id="3afa8-176">Agora, um gráfico de linhas é criado.</span><span class="sxs-lookup"><span data-stu-id="3afa8-176">Now a line chart is created.</span></span> <span data-ttu-id="3afa8-177">eixo x da saudação exibe a data e hora no fuso horário UTC hello.</span><span class="sxs-lookup"><span data-stu-id="3afa8-177">hello x-axis displays date and time in hello UTC time zone.</span></span> <span data-ttu-id="3afa8-178">eixo y da saudação mostra a temperatura do sensor de saudação.</span><span class="sxs-lookup"><span data-stu-id="3afa8-178">hello y-axis displays temperature from hello sensor.</span></span>

      ![Adicionar um gráfico de linhas de temperatura tooa relatório do Microsoft Power BI](media/iot-hub-live-data-visualization-in-power-bi/8_add-line-chart-for-temperature-to-power-bi-report-microsoft.png)

1. <span data-ttu-id="3afa8-180">Crie outra linha gráfico tooshow em tempo real umidade ao longo do tempo.</span><span class="sxs-lookup"><span data-stu-id="3afa8-180">Create another line chart tooshow real-time humidity over time.</span></span> <span data-ttu-id="3afa8-181">toodo isso, siga Olá mesmo as etapas acima e coloque **EventEnqueuedUtcTime** no eixo x do hello e **umidade** no eixo y da saudação.</span><span class="sxs-lookup"><span data-stu-id="3afa8-181">toodo this, follow hello same steps above and place **EventEnqueuedUtcTime** on hello x-axis and **humidity** on hello y-axis.</span></span>

   ![Adicionar um gráfico de linhas para umidade tooa relatório do Microsoft Power BI](media/iot-hub-live-data-visualization-in-power-bi/9_add-line-chart-for-humidity-to-power-bi-report-microsoft.png)

1. <span data-ttu-id="3afa8-183">Clique em **salvar** toosave relatório de saudação.</span><span class="sxs-lookup"><span data-stu-id="3afa8-183">Click **Save** toosave hello report.</span></span>
1. <span data-ttu-id="3afa8-184">Clique em **arquivo** > **publicar tooweb**.</span><span class="sxs-lookup"><span data-stu-id="3afa8-184">Click **File** > **Publish tooweb**.</span></span>
1. <span data-ttu-id="3afa8-185">Clique em **Criar código incorporado** e clique em **Publicar**.</span><span class="sxs-lookup"><span data-stu-id="3afa8-185">Click **Create embed code**, and then click **Publish**.</span></span>

<span data-ttu-id="3afa8-186">Você receberá o link do relatório Olá que você pode compartilhar com qualquer pessoa para acesso ao relatório e um relatório de saudação de toointegrate de trecho de código em seu blog ou site.</span><span class="sxs-lookup"><span data-stu-id="3afa8-186">You're provided hello report link that you can share with anyone for report access and a code snippet toointegrate hello report into your blog or website.</span></span>

![Publicar um relatório do Microsoft Power BI](media/iot-hub-live-data-visualization-in-power-bi/10_publish-power-bi-report-microsoft.png)

<span data-ttu-id="3afa8-188">A Microsoft também oferece Olá [aplicativos móveis Power BI](https://powerbi.microsoft.com/en-us/documentation/powerbi-power-bi-apps-for-mobile-devices/) para exibir e interagir com seus relatórios e dashboards do Power BI em seu dispositivo móvel.</span><span class="sxs-lookup"><span data-stu-id="3afa8-188">Microsoft also offers hello [Power BI mobile apps](https://powerbi.microsoft.com/en-us/documentation/powerbi-power-bi-apps-for-mobile-devices/) for viewing and interacting with your Power BI dashboards and reports on your mobile device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3afa8-189">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3afa8-189">Next steps</span></span>

<span data-ttu-id="3afa8-190">Você usou com êxito os dados do Power BI toovisualize sensor em tempo real do seu hub IoT do Azure.</span><span class="sxs-lookup"><span data-stu-id="3afa8-190">You’ve successfully used Power BI toovisualize real-time sensor data from your Azure IoT hub.</span></span>
<span data-ttu-id="3afa8-191">Há um maneira alternativa toovisualize dados Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="3afa8-191">There is an alternate way toovisualize data from Azure IoT Hub.</span></span> <span data-ttu-id="3afa8-192">Consulte [dados do sensor em tempo real do toovisualize aplicativos de Web do Azure de uso do Azure IoT Hub](iot-hub-live-data-visualization-in-web-apps.md).</span><span class="sxs-lookup"><span data-stu-id="3afa8-192">See [Use Azure Web Apps toovisualize real-time sensor data from Azure IoT Hub](iot-hub-live-data-visualization-in-web-apps.md).</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
