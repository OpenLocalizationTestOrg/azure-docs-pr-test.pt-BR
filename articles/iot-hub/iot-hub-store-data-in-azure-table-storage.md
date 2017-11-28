---
title: aaaSave tooAzure armazenamento de dados de mensagens de seu hub IoT | Microsoft Docs
description: "Use um toosave do aplicativo de função do Azure seu tooyour de mensagens do hub IoT armazenamento de tabela do Azure. mensagens de saudação do hub IoT contêm informações, como dados de sensor, que são enviadas do seu dispositivo IoT."
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
ms.openlocfilehash: be72d9ba9a781822926364351b50f58f5d96e94a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="save-iot-hub-messages-that-contain-sensor-data-tooyour-azure-table-storage"></a><span data-ttu-id="5ea71-105">Salvar mensagens de hub IoT que contêm o armazenamento de tabela do Azure do sensor dados tooyour</span><span class="sxs-lookup"><span data-stu-id="5ea71-105">Save IoT hub messages that contain sensor data tooyour Azure table storage</span></span>

![Diagrama de ponta a ponta](media/iot-hub-get-started-e2e-diagram/3.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

## <a name="what-you-learn"></a><span data-ttu-id="5ea71-107">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="5ea71-107">What you learn</span></span>

<span data-ttu-id="5ea71-108">Você aprenderá como toocreate uma conta de armazenamento do Azure e um Azure funcionam mensagens do aplicativo toostore IoT hub em seu armazenamento de tabela.</span><span class="sxs-lookup"><span data-stu-id="5ea71-108">You learn how toocreate an Azure storage account and an Azure function app toostore IoT hub messages in your table storage.</span></span>

## <a name="what-you-do"></a><span data-ttu-id="5ea71-109">O que fazer</span><span class="sxs-lookup"><span data-stu-id="5ea71-109">What you do</span></span>

- <span data-ttu-id="5ea71-110">Crie uma conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="5ea71-110">Create an Azure storage account.</span></span>
- <span data-ttu-id="5ea71-111">Prepare seu hub IoT mensagens de tooread de conexão.</span><span class="sxs-lookup"><span data-stu-id="5ea71-111">Prepare your IoT hub connection tooread messages.</span></span>
- <span data-ttu-id="5ea71-112">Criar e implantar um aplicativo de funções do Azure.</span><span class="sxs-lookup"><span data-stu-id="5ea71-112">Create and deploy an Azure function app.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="5ea71-113">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="5ea71-113">What you need</span></span>

- <span data-ttu-id="5ea71-114">[Configurar o seu dispositivo](iot-hub-raspberry-pi-kit-node-get-started.md) toocover Olá requisitos a seguir:</span><span class="sxs-lookup"><span data-stu-id="5ea71-114">[Set up your device](iot-hub-raspberry-pi-kit-node-get-started.md) toocover hello following requirements:</span></span>
  - <span data-ttu-id="5ea71-115">Uma assinatura ativa do Azure</span><span class="sxs-lookup"><span data-stu-id="5ea71-115">An active Azure subscription</span></span>
  - <span data-ttu-id="5ea71-116">Um hub IoT em sua assinatura</span><span class="sxs-lookup"><span data-stu-id="5ea71-116">An IoT hub under your subscription</span></span> 
  - <span data-ttu-id="5ea71-117">Um aplicativo em execução que envia o hub de IoT tooyour mensagens</span><span class="sxs-lookup"><span data-stu-id="5ea71-117">A running application that sends messages tooyour IoT hub</span></span>

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="5ea71-118">Criar uma conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="5ea71-118">Create an Azure storage account</span></span>

1. <span data-ttu-id="5ea71-119">Em Olá [portal do Azure](https://portal.azure.com/), clique em **novo** > **armazenamento** > **conta de armazenamento**  >   **Criar**.</span><span class="sxs-lookup"><span data-stu-id="5ea71-119">In hello [Azure portal](https://portal.azure.com/), click **New** > **Storage** > **Storage account** > **Create**.</span></span>

2. <span data-ttu-id="5ea71-120">Insira as informações necessárias para a conta de armazenamento Olá Olá:</span><span class="sxs-lookup"><span data-stu-id="5ea71-120">Enter hello necessary information for hello storage account:</span></span>

   ![Criar uma conta de armazenamento no hello portal do Azure](media\iot-hub-store-data-in-azure-table-storage\1_azure-portal-create-storage-account.png)

   * <span data-ttu-id="5ea71-122">**Nome**: nome Olá Olá da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="5ea71-122">**Name**: hello name of hello storage account.</span></span> <span data-ttu-id="5ea71-123">Olá nome deve ser exclusivo.</span><span class="sxs-lookup"><span data-stu-id="5ea71-123">hello name must be globally unique.</span></span>

   * <span data-ttu-id="5ea71-124">**Grupo de recursos**: Use Olá mesmo grupo de recursos que usa o hub IoT.</span><span class="sxs-lookup"><span data-stu-id="5ea71-124">**Resource group**: Use hello same resource group that your IoT hub uses.</span></span>

   * <span data-ttu-id="5ea71-125">**PIN toodashboard**: Selecione esta opção para o hub de IoT tooyour fácil acesso do painel de saudação.</span><span class="sxs-lookup"><span data-stu-id="5ea71-125">**Pin toodashboard**: Select this option for easy access tooyour IoT hub from hello dashboard.</span></span>

3. <span data-ttu-id="5ea71-126">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="5ea71-126">Click **Create**.</span></span>

## <a name="prepare-your-iot-hub-connection-tooread-messages"></a><span data-ttu-id="5ea71-127">Preparar o hub IoT mensagens de tooread de conexão</span><span class="sxs-lookup"><span data-stu-id="5ea71-127">Prepare your IoT hub connection tooread messages</span></span>

<span data-ttu-id="5ea71-128">Hub IoT expõe um evento interno ponto de extremidade compatível com o hub tooenable aplicativos tooread IoT hub as mensagens.</span><span class="sxs-lookup"><span data-stu-id="5ea71-128">IoT hub exposes a built-in event hub-compatible endpoint tooenable applications tooread IoT hub messages.</span></span> <span data-ttu-id="5ea71-129">Enquanto isso, os aplicativos usam dados do seu hub IoT tooread de grupos de consumidor.</span><span class="sxs-lookup"><span data-stu-id="5ea71-129">Meanwhile, applications use consumer groups tooread data from your IoT hub.</span></span> <span data-ttu-id="5ea71-130">Antes de criar um função do Azure aplicativo tooread de dados do seu hub IoT, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="5ea71-130">Before you create an Azure function app tooread data from your IoT hub, do hello following:</span></span>

- <span data-ttu-id="5ea71-131">Obter cadeia de caracteres de conexão de saudação do seu ponto de extremidade de hub IoT.</span><span class="sxs-lookup"><span data-stu-id="5ea71-131">Get hello connection string of your IoT hub endpoint.</span></span>
- <span data-ttu-id="5ea71-132">Criar um grupo de consumidores para o Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="5ea71-132">Create a consumer group for your IoT hub.</span></span>

### <a name="get-hello-connection-string-of-your-iot-hub-endpoint"></a><span data-ttu-id="5ea71-133">Obter cadeia de caracteres de conexão de saudação do seu ponto de extremidade de hub IoT</span><span class="sxs-lookup"><span data-stu-id="5ea71-133">Get hello connection string of your IoT hub endpoint</span></span>

1. <span data-ttu-id="5ea71-134">Abrir seu Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="5ea71-134">Open your IoT hub.</span></span>

2. <span data-ttu-id="5ea71-135">Em Olá **IoT Hub** painel, em **mensagens**, clique em **pontos de extremidade**.</span><span class="sxs-lookup"><span data-stu-id="5ea71-135">On hello **IoT Hub** pane, under **Messaging**, click **Endpoints**.</span></span>

3. <span data-ttu-id="5ea71-136">Em Olá direita painel, em **pontos de extremidade internos**, clique em **eventos**.</span><span class="sxs-lookup"><span data-stu-id="5ea71-136">In hello right pane, under **Built-in endpoints**, click **Events**.</span></span>

4. <span data-ttu-id="5ea71-137">Em Olá **propriedades** painel, Olá Observação valores a seguir:</span><span class="sxs-lookup"><span data-stu-id="5ea71-137">In hello **Properties** pane, note hello following values:</span></span>
   - <span data-ttu-id="5ea71-138">Ponto de extremidade compatível com o hub de eventos</span><span class="sxs-lookup"><span data-stu-id="5ea71-138">Event hub-compatible endpoint</span></span>
   - <span data-ttu-id="5ea71-139">Nome compatível com o hub de eventos</span><span class="sxs-lookup"><span data-stu-id="5ea71-139">Event hub-compatible name</span></span>

   ![Obter cadeia de caracteres de conexão de saudação de seu ponto de extremidade de hub IoT em Olá portal do Azure](media\iot-hub-store-data-in-azure-table-storage\2_azure-portal-iot-hub-endpoint-connection-string.png)

5. <span data-ttu-id="5ea71-141">Em Olá **IoT Hub** painel, em **configurações**, clique em **políticas de acesso compartilhado**.</span><span class="sxs-lookup"><span data-stu-id="5ea71-141">In hello **IoT Hub** pane, under **Settings**, click **Shared access policies**.</span></span>

6. <span data-ttu-id="5ea71-142">Clique em **iothubowner**.</span><span class="sxs-lookup"><span data-stu-id="5ea71-142">Click **iothubowner**.</span></span>

7. <span data-ttu-id="5ea71-143">Saudação de Observação **chave primária** valor.</span><span class="sxs-lookup"><span data-stu-id="5ea71-143">Note hello **Primary key** value.</span></span>

8. <span data-ttu-id="5ea71-144">Crie cadeia de caracteres de conexão de saudação de seu ponto de extremidade de hub IoT da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="5ea71-144">Create hello connection string of your IoT hub endpoint as follows:</span></span>

   `Endpoint=<Event Hub-compatible endpoint>;SharedAccessKeyName=iothubowner;SharedAccessKey=<Primary key>`

   > [!NOTE]
   > <span data-ttu-id="5ea71-145">Substituir `<Event Hub-compatible endpoint>` e `<Primary key>` com valores hello que você anotou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="5ea71-145">Replace `<Event Hub-compatible endpoint>` and `<Primary key>` with hello values that you noted earlier.</span></span>

### <a name="create-a-consumer-group-for-your-iot-hub"></a><span data-ttu-id="5ea71-146">Criar um grupo de consumidores para o Hub IoT</span><span class="sxs-lookup"><span data-stu-id="5ea71-146">Create a consumer group for your IoT hub</span></span>

1. <span data-ttu-id="5ea71-147">Abrir seu Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="5ea71-147">Open your IoT hub.</span></span>

2. <span data-ttu-id="5ea71-148">Em Olá **IoT Hub** painel, em **mensagens**, clique em **pontos de extremidade**.</span><span class="sxs-lookup"><span data-stu-id="5ea71-148">In hello **IoT Hub** pane, under **Messaging**, click **Endpoints**.</span></span>

3. <span data-ttu-id="5ea71-149">Em Olá direita painel, em **pontos de extremidade internos**, clique em **eventos**.</span><span class="sxs-lookup"><span data-stu-id="5ea71-149">In hello right pane, under **Built-in endpoints**, click **Events**.</span></span>

4. <span data-ttu-id="5ea71-150">Em Olá **propriedades** painel, em **grupos de consumidores**, insira um nome e, em seguida, anote-lo.</span><span class="sxs-lookup"><span data-stu-id="5ea71-150">In hello **Properties** pane, under **Consumer groups**, enter a name, and then make a note of it.</span></span>

5. <span data-ttu-id="5ea71-151">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="5ea71-151">Click **Save**.</span></span>

## <a name="create-and-deploy-an-azure-function-app"></a><span data-ttu-id="5ea71-152">Criar e implantar um aplicativo de funções do Azure</span><span class="sxs-lookup"><span data-stu-id="5ea71-152">Create and deploy an Azure function app</span></span>

1. <span data-ttu-id="5ea71-153">Em Olá [portal do Azure](https://portal.azure.com/), clique em **novo** > **de computação** > **aplicativo função**  >   **Criar**.</span><span class="sxs-lookup"><span data-stu-id="5ea71-153">In hello [Azure portal](https://portal.azure.com/), click **New** > **Compute** > **Function App** > **Create**.</span></span>

2. <span data-ttu-id="5ea71-154">Insira as informações necessárias para o aplicativo de função Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="5ea71-154">Enter hello necessary information for hello function app.</span></span>

   ![Criar um aplicativo de função em Olá portal do Azure](media\iot-hub-store-data-in-azure-table-storage\3_azure-portal-create-function-app.png)

   * <span data-ttu-id="5ea71-156">**Nome do aplicativo**: nome de saudação do aplicativo de função hello.</span><span class="sxs-lookup"><span data-stu-id="5ea71-156">**App name**: hello name of hello function app.</span></span> <span data-ttu-id="5ea71-157">Olá nome deve ser exclusivo.</span><span class="sxs-lookup"><span data-stu-id="5ea71-157">hello name must be globally unique.</span></span>

   * <span data-ttu-id="5ea71-158">**Grupo de recursos**: Use Olá mesmo grupo de recursos que usa o hub IoT.</span><span class="sxs-lookup"><span data-stu-id="5ea71-158">**Resource group**: Use hello same resource group that your IoT hub uses.</span></span>

   * <span data-ttu-id="5ea71-159">**Conta de armazenamento**: Olá conta de armazenamento que você criou.</span><span class="sxs-lookup"><span data-stu-id="5ea71-159">**Storage Account**: hello storage account that you created.</span></span>

   * <span data-ttu-id="5ea71-160">**PIN toodashboard**: marque esta opção para fácil acesso toohello função aplicativo de painel de saudação.</span><span class="sxs-lookup"><span data-stu-id="5ea71-160">**Pin toodashboard**: Check this option for easy access toohello function app from hello dashboard.</span></span>

3. <span data-ttu-id="5ea71-161">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="5ea71-161">Click **Create**.</span></span>

4. <span data-ttu-id="5ea71-162">Após a função hello aplicativo foi criado, abra-o.</span><span class="sxs-lookup"><span data-stu-id="5ea71-162">After hello function app has been created, open it.</span></span>

5. <span data-ttu-id="5ea71-163">No aplicativo de função hello, crie uma nova função hello seguinte:</span><span class="sxs-lookup"><span data-stu-id="5ea71-163">In hello function app, create a new function by doing hello following:</span></span>

   <span data-ttu-id="5ea71-164">a.</span><span class="sxs-lookup"><span data-stu-id="5ea71-164">a.</span></span> <span data-ttu-id="5ea71-165">Clique em **Nova Função**.</span><span class="sxs-lookup"><span data-stu-id="5ea71-165">Click **New Function**.</span></span>

   <span data-ttu-id="5ea71-166">b.</span><span class="sxs-lookup"><span data-stu-id="5ea71-166">b.</span></span> <span data-ttu-id="5ea71-167">Selecione **JavaScript** para **Linguagem** e **Processamento de Dados** para **Cenário**.</span><span class="sxs-lookup"><span data-stu-id="5ea71-167">Select **JavaScript** for **Language**, and **Data Processing** for **Scenario**.</span></span>

   <span data-ttu-id="5ea71-168">c.</span><span class="sxs-lookup"><span data-stu-id="5ea71-168">c.</span></span> <span data-ttu-id="5ea71-169">Clique em **Criar essa função** e depois clique em **Nova Função**.</span><span class="sxs-lookup"><span data-stu-id="5ea71-169">Click **Create this function**, and then click **New Function**.</span></span>

   <span data-ttu-id="5ea71-170">d.</span><span class="sxs-lookup"><span data-stu-id="5ea71-170">d.</span></span> <span data-ttu-id="5ea71-171">Selecione **JavaScript** idioma Olá, e **processamento de dados** para o cenário de saudação.</span><span class="sxs-lookup"><span data-stu-id="5ea71-171">Select **JavaScript** for hello language, and **Data Processing** for hello scenario.</span></span>

   <span data-ttu-id="5ea71-172">e.</span><span class="sxs-lookup"><span data-stu-id="5ea71-172">e.</span></span> <span data-ttu-id="5ea71-173">Clique em Olá **EventHubTrigger JavaScript** modelo.</span><span class="sxs-lookup"><span data-stu-id="5ea71-173">Click hello **EventHubTrigger-JavaScript** template.</span></span>

   <span data-ttu-id="5ea71-174">f.</span><span class="sxs-lookup"><span data-stu-id="5ea71-174">f.</span></span> <span data-ttu-id="5ea71-175">Insira as informações necessárias para o modelo de Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="5ea71-175">Enter hello necessary information for hello template.</span></span>

      * <span data-ttu-id="5ea71-176">**Nome de sua função**: nome de saudação do função hello.</span><span class="sxs-lookup"><span data-stu-id="5ea71-176">**Name your function**: hello name of hello function.</span></span>

      * <span data-ttu-id="5ea71-177">**Nome do Hub de evento**: nome de compatível com o hub de evento Olá que você anotou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="5ea71-177">**Event Hub name**: hello event hub-compatible name that you noted earlier.</span></span>

      * <span data-ttu-id="5ea71-178">**Conexão de Hub de evento**: cadeia de caracteres de conexão Olá de tooadd de ponto de extremidade do hello IoT hub que você criou, clique em **novo**.</span><span class="sxs-lookup"><span data-stu-id="5ea71-178">**Event Hub connection**: tooadd hello connection string of hello IoT hub endpoint that you created, click **New**.</span></span>

   <span data-ttu-id="5ea71-179">g.</span><span class="sxs-lookup"><span data-stu-id="5ea71-179">g.</span></span> <span data-ttu-id="5ea71-180">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="5ea71-180">Click **Create**.</span></span>

6. <span data-ttu-id="5ea71-181">Configure uma saída de função Olá Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="5ea71-181">Configure an output of hello function by doing hello following:</span></span>

   <span data-ttu-id="5ea71-182">a.</span><span class="sxs-lookup"><span data-stu-id="5ea71-182">a.</span></span> <span data-ttu-id="5ea71-183">Clique em **Integrar** > **Nova Saída** > **Armazenamento de Tabela do Azure** > **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="5ea71-183">Click **Integrate** > **New Output** > **Azure Table Storage** > **Select**.</span></span>

      ![Adicionar o aplicativo de função de tooyour de armazenamento de tabela no Olá portal do Azure](media\iot-hub-store-data-in-azure-table-storage\4_azure-portal-function-app-add-output-table-storage.png)

   <span data-ttu-id="5ea71-185">b.</span><span class="sxs-lookup"><span data-stu-id="5ea71-185">b.</span></span> <span data-ttu-id="5ea71-186">Insira as informações necessárias Olá.</span><span class="sxs-lookup"><span data-stu-id="5ea71-186">Enter hello necessary information.</span></span>

      * <span data-ttu-id="5ea71-187">**Nome do parâmetro de tabela**: Use `outputTable`, que será usado na hello Azure código da função.</span><span class="sxs-lookup"><span data-stu-id="5ea71-187">**Table parameter name**: Use `outputTable`, which will be used in hello Azure function's code.</span></span>
      
      * <span data-ttu-id="5ea71-188">**Nome da tabela**: use `deviceData`.</span><span class="sxs-lookup"><span data-stu-id="5ea71-188">**Table name**: Use `deviceData`.</span></span>

      * <span data-ttu-id="5ea71-189">**Conexão da conta de armazenamento**: clique em **Novo** e selecione ou insira sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="5ea71-189">**Storage account connection**: Click **New**, and then select or enter your storage account.</span></span> <span data-ttu-id="5ea71-190">Se a conta de armazenamento de saudação não for exibida, consulte [requisitos de conta de armazenamento](https://docs.microsoft.com/azure/azure-functions/functions-create-function-app-portal#storage-account-requirements).</span><span class="sxs-lookup"><span data-stu-id="5ea71-190">If hello storage account is not displayed, see [Storage account requirements](https://docs.microsoft.com/azure/azure-functions/functions-create-function-app-portal#storage-account-requirements).</span></span>
      
   <span data-ttu-id="5ea71-191">c.</span><span class="sxs-lookup"><span data-stu-id="5ea71-191">c.</span></span> <span data-ttu-id="5ea71-192">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="5ea71-192">Click **Save**.</span></span>

7. <span data-ttu-id="5ea71-193">Em **Gatilhos**, clique em **Hub de Eventos do Azure (eventHubMessages)**.</span><span class="sxs-lookup"><span data-stu-id="5ea71-193">Under **Triggers**, click **Azure Event Hub (eventHubMessages)**.</span></span>

8. <span data-ttu-id="5ea71-194">Em **grupo de consumidores do Hub de eventos**, insira o nome de saudação do grupo de consumidores Olá que você criou e, em seguida, clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="5ea71-194">Under **Event Hub consumer group**, enter hello name of hello consumer group that you created, and then click **Save**.</span></span>

9. <span data-ttu-id="5ea71-195">Clique em função hello tenha sido criado nos saudação à esquerda e, em seguida, clique em **exibir arquivos** em saudação à direita.</span><span class="sxs-lookup"><span data-stu-id="5ea71-195">Click hello function you've created on hello left and then click **View Files** on hello right.</span></span>

10. <span data-ttu-id="5ea71-196">Substitua Olá código em `index.js` com os seguintes hello:</span><span class="sxs-lookup"><span data-stu-id="5ea71-196">Replace hello code in `index.js` with hello following:</span></span>

   ```javascript
   'use strict';

   // This function is triggered each time a message is received in hello IoT hub.
   // hello message payload is persisted in an Azure storage table
 
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

11. <span data-ttu-id="5ea71-197">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="5ea71-197">Click **Save**.</span></span>

<span data-ttu-id="5ea71-198">Agora você criou o aplicativo de função hello.</span><span class="sxs-lookup"><span data-stu-id="5ea71-198">You have now created hello function app.</span></span> <span data-ttu-id="5ea71-199">Ele armazena as mensagens que seu hub IoT recebe em seu armazenamento de tabelas.</span><span class="sxs-lookup"><span data-stu-id="5ea71-199">It stores messages that your IoT hub receives in your table storage.</span></span>

> [!NOTE]
> <span data-ttu-id="5ea71-200">Você pode usar o hello **executar** botão tootest Olá função app.</span><span class="sxs-lookup"><span data-stu-id="5ea71-200">You can use hello **Run** button tootest hello function app.</span></span> <span data-ttu-id="5ea71-201">Quando você clica em **executar**, mensagem de saudação do teste é enviada tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="5ea71-201">When you click **Run**, hello test message is sent tooyour IoT hub.</span></span> <span data-ttu-id="5ea71-202">chegada de saudação de mensagem de saudação deve disparar Olá função aplicativo toostart e, em seguida, salve o armazenamento de tabela de tooyour de mensagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="5ea71-202">hello arrival of hello message should trigger hello function app toostart and then save hello message tooyour table storage.</span></span> <span data-ttu-id="5ea71-203">Olá **Logs** painel registra os detalhes de saudação do processo de saudação.</span><span class="sxs-lookup"><span data-stu-id="5ea71-203">hello **Logs** pane records hello details of hello process.</span></span>

## <a name="verify-your-message-in-your-table-storage"></a><span data-ttu-id="5ea71-204">Verificar a mensagem no armazenamento de tabelas</span><span class="sxs-lookup"><span data-stu-id="5ea71-204">Verify your message in your table storage</span></span>

1. <span data-ttu-id="5ea71-205">Execute o aplicativo de exemplo hello em seu hub IoT do dispositivo toosend mensagens tooyour.</span><span class="sxs-lookup"><span data-stu-id="5ea71-205">Run hello sample application on your device toosend messages tooyour IoT hub.</span></span>

2. <span data-ttu-id="5ea71-206">[Baixe e instale o Gerenciador de Armazenamento do Azure](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="5ea71-206">[Download and install Azure Storage Explorer](http://storageexplorer.com/).</span></span>

3. <span data-ttu-id="5ea71-207">Abra o Gerenciador de armazenamento, clique em **adicionar uma conta do Azure** > **entrar**e entre tooyour conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="5ea71-207">Open Storage Explorer, click **Add an Azure Account** > **Sign in**, and then sign in tooyour Azure account.</span></span>

4. <span data-ttu-id="5ea71-208">Clique em sua assinatura do Azure > **Contas de Armazenamento** > sua conta de armazenamento > **Tabelas** > **deviceData**.</span><span class="sxs-lookup"><span data-stu-id="5ea71-208">Click your Azure subscription > **Storage Accounts** > your storage account > **Tables** > **deviceData**.</span></span>

   <span data-ttu-id="5ea71-209">Você deve ver as mensagens enviadas do seu hub IoT de tooyour de dispositivo conectado Olá `deviceData` tabela.</span><span class="sxs-lookup"><span data-stu-id="5ea71-209">You should see messages sent from your device tooyour IoT hub logged in hello `deviceData` table.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5ea71-210">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5ea71-210">Next steps</span></span>

<span data-ttu-id="5ea71-211">Você criou com êxito sua conta de armazenamento do Azure e o aplicativo de funções do Azure para armazenar mensagens que seu hub IoT recebe em seu armazenamento de tabelas.</span><span class="sxs-lookup"><span data-stu-id="5ea71-211">You’ve successfully created your Azure storage account and Azure function app, which stores messages that your IoT hub receives in your table storage.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
