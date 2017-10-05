---
title: Salvar suas mensagens do hub IoT no armazenamento de dados do Azure | Microsoft Docs
description: "Use um aplicativo de funções do Azure para salvar as mensagens do hub IoT para seu armazenamento de tabela do Azure. As mensagens do hub IoT contêm informações como dados de sensor, que são enviadas do seu dispositivo IoT."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: armazenamento de dados iot, armazenamento de dados de sensor iot
ms.assetid: 62fd14fd-aaaa-4b3d-8367-75c1111b6269
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/16/2017
ms.author: xshi
ms.openlocfilehash: 06503f9564e00ef62587d02f2da4778974e246c5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="save-iot-hub-messages-that-contain-sensor-data-to-your-azure-table-storage"></a><span data-ttu-id="82bc3-105">Salvar mensagens do hub IoT que contêm dados de sensor para seu armazenamento de tabela do Azure</span><span class="sxs-lookup"><span data-stu-id="82bc3-105">Save IoT hub messages that contain sensor data to your Azure table storage</span></span>

![Diagrama de ponta a ponta](media/iot-hub-get-started-e2e-diagram/3.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

## <a name="what-you-learn"></a><span data-ttu-id="82bc3-107">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="82bc3-107">What you learn</span></span>

<span data-ttu-id="82bc3-108">Saiba como criar uma conta de armazenamento do Azure e um aplicativo de funções do Azure para armazenar mensagens do hub IoT no armazenamento de tabelas.</span><span class="sxs-lookup"><span data-stu-id="82bc3-108">You learn how to create an Azure storage account and an Azure function app to store IoT hub messages in your table storage.</span></span>

## <a name="what-you-do"></a><span data-ttu-id="82bc3-109">O que fazer</span><span class="sxs-lookup"><span data-stu-id="82bc3-109">What you do</span></span>

- <span data-ttu-id="82bc3-110">Crie uma conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="82bc3-110">Create an Azure storage account.</span></span>
- <span data-ttu-id="82bc3-111">Prepare a conexão do hub IoT para ler mensagens.</span><span class="sxs-lookup"><span data-stu-id="82bc3-111">Prepare your IoT hub connection to read messages.</span></span>
- <span data-ttu-id="82bc3-112">Criar e implantar um aplicativo de funções do Azure.</span><span class="sxs-lookup"><span data-stu-id="82bc3-112">Create and deploy an Azure function app.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="82bc3-113">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="82bc3-113">What you need</span></span>

- <span data-ttu-id="82bc3-114">[Configure seu dispositivo](iot-hub-raspberry-pi-kit-node-get-started.md) para abranger os seguintes requisitos:</span><span class="sxs-lookup"><span data-stu-id="82bc3-114">[Set up your device](iot-hub-raspberry-pi-kit-node-get-started.md) to cover the following requirements:</span></span>
  - <span data-ttu-id="82bc3-115">Uma assinatura ativa do Azure</span><span class="sxs-lookup"><span data-stu-id="82bc3-115">An active Azure subscription</span></span>
  - <span data-ttu-id="82bc3-116">Um hub IoT em sua assinatura</span><span class="sxs-lookup"><span data-stu-id="82bc3-116">An IoT hub under your subscription</span></span> 
  - <span data-ttu-id="82bc3-117">Um aplicativo em execução que envia mensagens ao seu hub IoT</span><span class="sxs-lookup"><span data-stu-id="82bc3-117">A running application that sends messages to your IoT hub</span></span>

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="82bc3-118">Criar uma conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="82bc3-118">Create an Azure storage account</span></span>

1. <span data-ttu-id="82bc3-119">No [portal do Azure](https://portal.azure.com/), clique em **Novo** > **Armazenamento** > **Conta de armazenamento** > **Criar**.</span><span class="sxs-lookup"><span data-stu-id="82bc3-119">In the [Azure portal](https://portal.azure.com/), click **New** > **Storage** > **Storage account** > **Create**.</span></span>

2. <span data-ttu-id="82bc3-120">Insira as informações necessárias para a conta de armazenamento:</span><span class="sxs-lookup"><span data-stu-id="82bc3-120">Enter the necessary information for the storage account:</span></span>

   ![Criar uma conta de armazenamento no portal do Azure](media\iot-hub-store-data-in-azure-table-storage\1_azure-portal-create-storage-account.png)

   * <span data-ttu-id="82bc3-122">**Name**: o nome da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="82bc3-122">**Name**: The name of the storage account.</span></span> <span data-ttu-id="82bc3-123">O nome deve ser globalmente exclusivo.</span><span class="sxs-lookup"><span data-stu-id="82bc3-123">The name must be globally unique.</span></span>

   * <span data-ttu-id="82bc3-124">**Grupo de recursos**: use o mesmo grupo de recursos usado pelo seu hub IoT.</span><span class="sxs-lookup"><span data-stu-id="82bc3-124">**Resource group**: Use the same resource group that your IoT hub uses.</span></span>

   * <span data-ttu-id="82bc3-125">**Fixar no painel**: selecione essa opção para ter fácil acesso ao Hub IoT no painel.</span><span class="sxs-lookup"><span data-stu-id="82bc3-125">**Pin to dashboard**: Select this option for easy access to your IoT hub from the dashboard.</span></span>

3. <span data-ttu-id="82bc3-126">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="82bc3-126">Click **Create**.</span></span>

## <a name="prepare-your-iot-hub-connection-to-read-messages"></a><span data-ttu-id="82bc3-127">Preparar a conexão do hub IoT para ler mensagens</span><span class="sxs-lookup"><span data-stu-id="82bc3-127">Prepare your IoT hub connection to read messages</span></span>

<span data-ttu-id="82bc3-128">O hub IoT expõe um ponto de extremidade compatível com o hub de eventos interno para permitir que os aplicativos leiam mensagens do hub IoT.</span><span class="sxs-lookup"><span data-stu-id="82bc3-128">IoT hub exposes a built-in event hub-compatible endpoint to enable applications to read IoT hub messages.</span></span> <span data-ttu-id="82bc3-129">Enquanto isso, os aplicativos usam grupos de consumidores para ler dados do hub IoT.</span><span class="sxs-lookup"><span data-stu-id="82bc3-129">Meanwhile, applications use consumer groups to read data from your IoT hub.</span></span> <span data-ttu-id="82bc3-130">Antes de criar um aplicativo de funções do Azure para ler dados do seu hub IoT, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="82bc3-130">Before you create an Azure function app to read data from your IoT hub, do the following:</span></span>

- <span data-ttu-id="82bc3-131">Obter a cadeia de conexão do ponto de extremidade de Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="82bc3-131">Get the connection string of your IoT hub endpoint.</span></span>
- <span data-ttu-id="82bc3-132">Criar um grupo de consumidores para o Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="82bc3-132">Create a consumer group for your IoT hub.</span></span>

### <a name="get-the-connection-string-of-your-iot-hub-endpoint"></a><span data-ttu-id="82bc3-133">Obter a cadeia de conexão do ponto de extremidade de Hub IoT</span><span class="sxs-lookup"><span data-stu-id="82bc3-133">Get the connection string of your IoT hub endpoint</span></span>

1. <span data-ttu-id="82bc3-134">Abrir seu Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="82bc3-134">Open your IoT hub.</span></span>

2. <span data-ttu-id="82bc3-135">No painel **Hub IoT**, clique em **Pontos de Extremidade** em **Mensagens**.</span><span class="sxs-lookup"><span data-stu-id="82bc3-135">On the **IoT Hub** pane, under **Messaging**, click **Endpoints**.</span></span>

3. <span data-ttu-id="82bc3-136">No painel direito, clique em **Eventos** em **Pontos de extremidade internos**.</span><span class="sxs-lookup"><span data-stu-id="82bc3-136">In the right pane, under **Built-in endpoints**, click **Events**.</span></span>

4. <span data-ttu-id="82bc3-137">No painel **Propriedades**, observe os seguintes valores:</span><span class="sxs-lookup"><span data-stu-id="82bc3-137">In the **Properties** pane, note the following values:</span></span>
   - <span data-ttu-id="82bc3-138">Ponto de extremidade compatível com o hub de eventos</span><span class="sxs-lookup"><span data-stu-id="82bc3-138">Event hub-compatible endpoint</span></span>
   - <span data-ttu-id="82bc3-139">Nome compatível com o hub de eventos</span><span class="sxs-lookup"><span data-stu-id="82bc3-139">Event hub-compatible name</span></span>

   ![Obter a cadeia de conexão do ponto de extremidade de Hub IoT no Portal do Azure](media\iot-hub-store-data-in-azure-table-storage\2_azure-portal-iot-hub-endpoint-connection-string.png)

5. <span data-ttu-id="82bc3-141">No painel **Hub IoT**, clique em **Políticas de acesso compartilhado** em **Configurações**.</span><span class="sxs-lookup"><span data-stu-id="82bc3-141">In the **IoT Hub** pane, under **Settings**, click **Shared access policies**.</span></span>

6. <span data-ttu-id="82bc3-142">Clique em **iothubowner**.</span><span class="sxs-lookup"><span data-stu-id="82bc3-142">Click **iothubowner**.</span></span>

7. <span data-ttu-id="82bc3-143">Observe o valor da **Chave primária**.</span><span class="sxs-lookup"><span data-stu-id="82bc3-143">Note the **Primary key** value.</span></span>

8. <span data-ttu-id="82bc3-144">Crie a cadeia de conexão do seu ponto de extremidade do hub IoT conforme descrito a seguir:</span><span class="sxs-lookup"><span data-stu-id="82bc3-144">Create the connection string of your IoT hub endpoint as follows:</span></span>

   `Endpoint=<Event Hub-compatible endpoint>;SharedAccessKeyName=iothubowner;SharedAccessKey=<Primary key>`

   > [!NOTE]
   > <span data-ttu-id="82bc3-145">Substituir `<Event Hub-compatible endpoint>` e `<Primary key>` pelos valores que você anotou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="82bc3-145">Replace `<Event Hub-compatible endpoint>` and `<Primary key>` with the values that you noted earlier.</span></span>

### <a name="create-a-consumer-group-for-your-iot-hub"></a><span data-ttu-id="82bc3-146">Criar um grupo de consumidores para o Hub IoT</span><span class="sxs-lookup"><span data-stu-id="82bc3-146">Create a consumer group for your IoT hub</span></span>

1. <span data-ttu-id="82bc3-147">Abrir seu Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="82bc3-147">Open your IoT hub.</span></span>

2. <span data-ttu-id="82bc3-148">No painel **Hub IoT**, clique em **Pontos de Extremidade** em **Mensagens**.</span><span class="sxs-lookup"><span data-stu-id="82bc3-148">In the **IoT Hub** pane, under **Messaging**, click **Endpoints**.</span></span>

3. <span data-ttu-id="82bc3-149">No painel direito, clique em **Eventos** em **Pontos de extremidade internos**.</span><span class="sxs-lookup"><span data-stu-id="82bc3-149">In the right pane, under **Built-in endpoints**, click **Events**.</span></span>

4. <span data-ttu-id="82bc3-150">No painel **Propriedades**, em **Grupos de consumidores**, insira um nome e, em seguida, anote-o.</span><span class="sxs-lookup"><span data-stu-id="82bc3-150">In the **Properties** pane, under **Consumer groups**, enter a name, and then make a note of it.</span></span>

5. <span data-ttu-id="82bc3-151">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="82bc3-151">Click **Save**.</span></span>

## <a name="create-and-deploy-an-azure-function-app"></a><span data-ttu-id="82bc3-152">Criar e implantar um aplicativo de funções do Azure</span><span class="sxs-lookup"><span data-stu-id="82bc3-152">Create and deploy an Azure function app</span></span>

1. <span data-ttu-id="82bc3-153">No [portal do Azure](https://portal.azure.com/), clique em **Novo** > **Computação** > **Aplicativo de Funções** > **Criar**.</span><span class="sxs-lookup"><span data-stu-id="82bc3-153">In the [Azure portal](https://portal.azure.com/), click **New** > **Compute** > **Function App** > **Create**.</span></span>

2. <span data-ttu-id="82bc3-154">Insira as informações necessárias para o aplicativo de funções.</span><span class="sxs-lookup"><span data-stu-id="82bc3-154">Enter the necessary information for the function app.</span></span>

   ![Criar um aplicativo de funções no portal do Azure](media\iot-hub-store-data-in-azure-table-storage\3_azure-portal-create-function-app.png)

   * <span data-ttu-id="82bc3-156">**Nome do aplicativo**: o nome do aplicativo de funções.</span><span class="sxs-lookup"><span data-stu-id="82bc3-156">**App name**: The name of the function app.</span></span> <span data-ttu-id="82bc3-157">O nome deve ser globalmente exclusivo.</span><span class="sxs-lookup"><span data-stu-id="82bc3-157">The name must be globally unique.</span></span>

   * <span data-ttu-id="82bc3-158">**Grupo de recursos**: use o mesmo grupo de recursos usado pelo seu hub IoT.</span><span class="sxs-lookup"><span data-stu-id="82bc3-158">**Resource group**: Use the same resource group that your IoT hub uses.</span></span>

   * <span data-ttu-id="82bc3-159">**Conta de Armazenamento**: a conta de armazenamento que você criou.</span><span class="sxs-lookup"><span data-stu-id="82bc3-159">**Storage Account**: The storage account that you created.</span></span>

   * <span data-ttu-id="82bc3-160">**Fixar ao painel**: marque essa opção para facilitar o acesso ao aplicativo de funções do painel.</span><span class="sxs-lookup"><span data-stu-id="82bc3-160">**Pin to dashboard**: Check this option for easy access to the function app from the dashboard.</span></span>

3. <span data-ttu-id="82bc3-161">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="82bc3-161">Click **Create**.</span></span>

4. <span data-ttu-id="82bc3-162">Após o aplicativo de funções ter sido criado, abra-o.</span><span class="sxs-lookup"><span data-stu-id="82bc3-162">After the function app has been created, open it.</span></span>

5. <span data-ttu-id="82bc3-163">No aplicativo de funções, crie uma nova função fazendo o seguinte:</span><span class="sxs-lookup"><span data-stu-id="82bc3-163">In the function app, create a new function by doing the following:</span></span>

   <span data-ttu-id="82bc3-164">a.</span><span class="sxs-lookup"><span data-stu-id="82bc3-164">a.</span></span> <span data-ttu-id="82bc3-165">Clique em **Nova Função**.</span><span class="sxs-lookup"><span data-stu-id="82bc3-165">Click **New Function**.</span></span>

   <span data-ttu-id="82bc3-166">b.</span><span class="sxs-lookup"><span data-stu-id="82bc3-166">b.</span></span> <span data-ttu-id="82bc3-167">Selecione **JavaScript** para **Linguagem** e **Processamento de Dados** para **Cenário**.</span><span class="sxs-lookup"><span data-stu-id="82bc3-167">Select **JavaScript** for **Language**, and **Data Processing** for **Scenario**.</span></span>

   <span data-ttu-id="82bc3-168">c.</span><span class="sxs-lookup"><span data-stu-id="82bc3-168">c.</span></span> <span data-ttu-id="82bc3-169">Clique em **Criar essa função** e depois clique em **Nova Função**.</span><span class="sxs-lookup"><span data-stu-id="82bc3-169">Click **Create this function**, and then click **New Function**.</span></span>

   <span data-ttu-id="82bc3-170">d.</span><span class="sxs-lookup"><span data-stu-id="82bc3-170">d.</span></span> <span data-ttu-id="82bc3-171">Selecione **JavaScript** para linguagem e **Processamento de Dados** para o cenário.</span><span class="sxs-lookup"><span data-stu-id="82bc3-171">Select **JavaScript** for the language, and **Data Processing** for the scenario.</span></span>

   <span data-ttu-id="82bc3-172">e.</span><span class="sxs-lookup"><span data-stu-id="82bc3-172">e.</span></span> <span data-ttu-id="82bc3-173">Clique no modelo **EventHubTrigger-JavaScript**.</span><span class="sxs-lookup"><span data-stu-id="82bc3-173">Click the **EventHubTrigger-JavaScript** template.</span></span>

   <span data-ttu-id="82bc3-174">f.</span><span class="sxs-lookup"><span data-stu-id="82bc3-174">f.</span></span> <span data-ttu-id="82bc3-175">Insira as informações necessárias para o modelo.</span><span class="sxs-lookup"><span data-stu-id="82bc3-175">Enter the necessary information for the template.</span></span>

      * <span data-ttu-id="82bc3-176">**Nomeie a função**: o nome da função.</span><span class="sxs-lookup"><span data-stu-id="82bc3-176">**Name your function**: The name of the function.</span></span>

      * <span data-ttu-id="82bc3-177">**Nome do Hub de Eventos**: nome compatível com o hub de eventos anotado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="82bc3-177">**Event Hub name**: The event hub-compatible name that you noted earlier.</span></span>

      * <span data-ttu-id="82bc3-178">**Conexão do Hub de Eventos**: clique em **Novo** para adicionar a cadeia de conexão do ponto de extremidade do hub IoT que você criou.</span><span class="sxs-lookup"><span data-stu-id="82bc3-178">**Event Hub connection**: To add the connection string of the IoT hub endpoint that you created, click **New**.</span></span>

   <span data-ttu-id="82bc3-179">g.</span><span class="sxs-lookup"><span data-stu-id="82bc3-179">g.</span></span> <span data-ttu-id="82bc3-180">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="82bc3-180">Click **Create**.</span></span>

6. <span data-ttu-id="82bc3-181">Configure uma saída da função fazendo o seguinte:</span><span class="sxs-lookup"><span data-stu-id="82bc3-181">Configure an output of the function by doing the following:</span></span>

   <span data-ttu-id="82bc3-182">a.</span><span class="sxs-lookup"><span data-stu-id="82bc3-182">a.</span></span> <span data-ttu-id="82bc3-183">Clique em **Integrar** > **Nova Saída** > **Armazenamento de Tabela do Azure** > **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="82bc3-183">Click **Integrate** > **New Output** > **Azure Table Storage** > **Select**.</span></span>

      ![Adicionar um armazenamento de tabelas ao aplicativo de funções no portal do Azure](media\iot-hub-store-data-in-azure-table-storage\4_azure-portal-function-app-add-output-table-storage.png)

   <span data-ttu-id="82bc3-185">b.</span><span class="sxs-lookup"><span data-stu-id="82bc3-185">b.</span></span> <span data-ttu-id="82bc3-186">Insira as informações necessárias.</span><span class="sxs-lookup"><span data-stu-id="82bc3-186">Enter the necessary information.</span></span>

      * <span data-ttu-id="82bc3-187">**Nome do parâmetro de tabela**: use `outputTable`, que será usado no código da função do Azure.</span><span class="sxs-lookup"><span data-stu-id="82bc3-187">**Table parameter name**: Use `outputTable`, which will be used in the Azure function's code.</span></span>
      
      * <span data-ttu-id="82bc3-188">**Nome da tabela**: use `deviceData`.</span><span class="sxs-lookup"><span data-stu-id="82bc3-188">**Table name**: Use `deviceData`.</span></span>

      * <span data-ttu-id="82bc3-189">**Conexão da conta de armazenamento**: clique em **Novo** e selecione ou insira sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="82bc3-189">**Storage account connection**: Click **New**, and then select or enter your storage account.</span></span> <span data-ttu-id="82bc3-190">Se a conta de armazenamento não for exibida, consulte [Requisitos da conta de armazenamento](https://docs.microsoft.com/azure/azure-functions/functions-create-function-app-portal#storage-account-requirements).</span><span class="sxs-lookup"><span data-stu-id="82bc3-190">If the storage account is not displayed, see [Storage account requirements](https://docs.microsoft.com/azure/azure-functions/functions-create-function-app-portal#storage-account-requirements).</span></span>
      
   <span data-ttu-id="82bc3-191">c.</span><span class="sxs-lookup"><span data-stu-id="82bc3-191">c.</span></span> <span data-ttu-id="82bc3-192">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="82bc3-192">Click **Save**.</span></span>

7. <span data-ttu-id="82bc3-193">Em **Gatilhos**, clique em **Hub de Eventos do Azure (eventHubMessages)**.</span><span class="sxs-lookup"><span data-stu-id="82bc3-193">Under **Triggers**, click **Azure Event Hub (eventHubMessages)**.</span></span>

8. <span data-ttu-id="82bc3-194">Em **Grupo de consumidores do Hub de Eventos**, digite o nome do grupo de consumidores que você criou anteriormente e clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="82bc3-194">Under **Event Hub consumer group**, enter the name of the consumer group that you created, and then click **Save**.</span></span>

9. <span data-ttu-id="82bc3-195">Clique na função que você criou no lado esquerdo e, em seguida, clique em **exibir arquivos** à direita.</span><span class="sxs-lookup"><span data-stu-id="82bc3-195">Click the function you've created on the left and then click **View Files** on the right.</span></span>

10. <span data-ttu-id="82bc3-196">Substitua o código em `index.js` pelo seguinte código:</span><span class="sxs-lookup"><span data-stu-id="82bc3-196">Replace the code in `index.js` with the following:</span></span>

   ```javascript
   'use strict';

   // This function is triggered each time a message is received in the IoT hub.
   // The message payload is persisted in an Azure storage table
 
   module.exports = function (context, iotHubMessage) {
    context.log('Message received: ' + JSON.stringify(iotHubMessage));
    var date = Date.now();
    var partitionKey = Math.floor(date / (24 * 60 * 60 * 1000)) + '';
    var rowKey = date + '';
    context.bindings.outputTable = {
     "partitionKey": partitionKey,
     "rowKey": rowKey,
     "message": JSON.stringify(iotHubMessage)
    };
    context.done();
   };
   ```

11. <span data-ttu-id="82bc3-197">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="82bc3-197">Click **Save**.</span></span>

<span data-ttu-id="82bc3-198">Agora você criou o aplicativo de funções.</span><span class="sxs-lookup"><span data-stu-id="82bc3-198">You have now created the function app.</span></span> <span data-ttu-id="82bc3-199">Ele armazena as mensagens que seu hub IoT recebe em seu armazenamento de tabelas.</span><span class="sxs-lookup"><span data-stu-id="82bc3-199">It stores messages that your IoT hub receives in your table storage.</span></span>

> [!NOTE]
> <span data-ttu-id="82bc3-200">Você pode usar o botão **Executar** para testar o aplicativo de funções.</span><span class="sxs-lookup"><span data-stu-id="82bc3-200">You can use the **Run** button to test the function app.</span></span> <span data-ttu-id="82bc3-201">Quando você clica em **Executar**, a mensagem de teste é enviada para o Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="82bc3-201">When you click **Run**, the test message is sent to your IoT hub.</span></span> <span data-ttu-id="82bc3-202">A chegada da mensagem deve disparar o início do aplicativo de funções e, em seguida, salvar a mensagem no armazenamento de tabelas.</span><span class="sxs-lookup"><span data-stu-id="82bc3-202">The arrival of the message should trigger the function app to start and then save the message to your table storage.</span></span> <span data-ttu-id="82bc3-203">O painel **Logs** registra os detalhes do processo.</span><span class="sxs-lookup"><span data-stu-id="82bc3-203">The **Logs** pane records the details of the process.</span></span>

## <a name="verify-your-message-in-your-table-storage"></a><span data-ttu-id="82bc3-204">Verificar a mensagem no armazenamento de tabelas</span><span class="sxs-lookup"><span data-stu-id="82bc3-204">Verify your message in your table storage</span></span>

1. <span data-ttu-id="82bc3-205">Execute o aplicativo de exemplo em seu dispositivo para enviar mensagens para o Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="82bc3-205">Run the sample application on your device to send messages to your IoT hub.</span></span>

2. <span data-ttu-id="82bc3-206">[Baixe e instale o Gerenciador de Armazenamento do Azure](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="82bc3-206">[Download and install Azure Storage Explorer](http://storageexplorer.com/).</span></span>

3. <span data-ttu-id="82bc3-207">Abra o Gerenciador de Armazenamento, clique em **Adicionar uma Conta do Azure** > **Entrar** e entre em sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="82bc3-207">Open Storage Explorer, click **Add an Azure Account** > **Sign in**, and then sign in to your Azure account.</span></span>

4. <span data-ttu-id="82bc3-208">Clique em sua assinatura do Azure > **Contas de Armazenamento** > sua conta de armazenamento > **Tabelas** > **deviceData**.</span><span class="sxs-lookup"><span data-stu-id="82bc3-208">Click your Azure subscription > **Storage Accounts** > your storage account > **Tables** > **deviceData**.</span></span>

   <span data-ttu-id="82bc3-209">Você deve ver as mensagens enviadas do seu dispositivo ao seu Hub IoT conectado à tabela `deviceData`.</span><span class="sxs-lookup"><span data-stu-id="82bc3-209">You should see messages sent from your device to your IoT hub logged in the `deviceData` table.</span></span>

## <a name="next-steps"></a><span data-ttu-id="82bc3-210">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="82bc3-210">Next steps</span></span>

<span data-ttu-id="82bc3-211">Você criou com êxito sua conta de armazenamento do Azure e o aplicativo de funções do Azure para armazenar mensagens que seu hub IoT recebe em seu armazenamento de tabelas.</span><span class="sxs-lookup"><span data-stu-id="82bc3-211">You’ve successfully created your Azure storage account and Azure function app, which stores messages that your IoT hub receives in your table storage.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
