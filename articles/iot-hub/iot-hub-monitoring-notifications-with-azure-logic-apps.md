---
title: "Monitoramento remoto de IoT e notificações com o Aplicativo Lógico do Azure | Microsoft Docs"
description: "Use o Aplicativo Lógico do Azure para monitoramento de temperatura de IoT em seu hub IoT e envio automático de notificações por email à sua caixa de correio sobre quaisquer anomalias detectadas."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: "monitoramento de iot, notificações de iot, monitoramento de temperatura de iot"
ms.assetid: 43043067-2e1f-42c9-953d-e2dce8fd86df
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: xshi
ms.openlocfilehash: 7a611912ae55eb22103539dbba9f1a06aaa543b7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="iot-remote-monitoring-and-notifications-with-azure-logic-apps-connecting-your-iot-hub-and-mailbox"></a><span data-ttu-id="3d970-104">Monitoramento remoto IoT e notificações com o Aplicativo Lógico do Azure conectando o hub IoT e a caixa de correio</span><span class="sxs-lookup"><span data-stu-id="3d970-104">IoT remote monitoring and notifications with Azure Logic Apps connecting your IoT hub and mailbox</span></span>

![Diagrama de ponta a ponta](media/iot-hub-get-started-e2e-diagram/7.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

<span data-ttu-id="3d970-106">O Aplicativo Lógico do Azure fornecem uma maneira de automatizar processos como uma série de etapas.</span><span class="sxs-lookup"><span data-stu-id="3d970-106">Azure Logic Apps provides a way to automate processes as a series of steps.</span></span> <span data-ttu-id="3d970-107">Um aplicativo lógico pode se conectar com vários serviços e protocolos.</span><span class="sxs-lookup"><span data-stu-id="3d970-107">A logic app can connect across various services and protocols.</span></span> <span data-ttu-id="3d970-108">Ele começa com um gatilho como “Quando uma conta é adicionada”, seguido por uma combinação de ações semelhantes a “enviar uma notificação por push”.</span><span class="sxs-lookup"><span data-stu-id="3d970-108">It begins with a trigger such as 'When an account is added', and followed by a combination of actions, one like 'sending a push notification'.</span></span> <span data-ttu-id="3d970-109">Esse recurso torna os aplicativos lógicos uma solução de IoT perfeita para monitoramento de IoT, como alertas a anomalias, entre outros cenários de uso.</span><span class="sxs-lookup"><span data-stu-id="3d970-109">This feature makes Logic Apps a perfect IoT solution for IoT monitoring, such as staying alert for anomalies, among other usage scenarios.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="3d970-110">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="3d970-110">What you learn</span></span>

<span data-ttu-id="3d970-111">Aprenda a criar um aplicativo lógico que conecta o hub IoT e a caixa de correio para monitoramento e notificações de temperatura.</span><span class="sxs-lookup"><span data-stu-id="3d970-111">You learn how to create a logic app that connects your IoT hub and your mailbox for temperature monitoring and notifications.</span></span> <span data-ttu-id="3d970-112">Quando a temperatura está acima de 30 C, o aplicativo cliente marca `temperatureAlert = "true"` na mensagem enviada para o hub IoT.</span><span class="sxs-lookup"><span data-stu-id="3d970-112">When the temperature is above 30 C, the client application marks `temperatureAlert = "true"` in the message it sends to your IoT hub.</span></span> <span data-ttu-id="3d970-113">A mensagem dispara o aplicativo lógico para enviar uma notificação por email a você.</span><span class="sxs-lookup"><span data-stu-id="3d970-113">The message triggers the logic app to send you an email notification.</span></span>

## <a name="what-you-do"></a><span data-ttu-id="3d970-114">O que fazer</span><span class="sxs-lookup"><span data-stu-id="3d970-114">What you do</span></span>

* <span data-ttu-id="3d970-115">Crie um namespace de barramento de serviço e adicione uma fila a ele.</span><span class="sxs-lookup"><span data-stu-id="3d970-115">Create a service bus namespace and add a queue to it.</span></span>
* <span data-ttu-id="3d970-116">Adicione um ponto de extremidade e uma regra de roteamento ao hub IoT.</span><span class="sxs-lookup"><span data-stu-id="3d970-116">Add an endpoint and a routing rule to your IoT hub.</span></span>
* <span data-ttu-id="3d970-117">Crie, configure e teste um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="3d970-117">Create, configure, and test a logic app.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="3d970-118">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="3d970-118">What you need</span></span>

* <span data-ttu-id="3d970-119">Tutorial [Configurar seu dispositivo](iot-hub-raspberry-pi-kit-node-get-started.md) concluído que aborda os seguintes requisitos:</span><span class="sxs-lookup"><span data-stu-id="3d970-119">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers the following requirements:</span></span>
  * <span data-ttu-id="3d970-120">Uma assinatura ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="3d970-120">An active Azure subscription.</span></span>
  * <span data-ttu-id="3d970-121">Um hub IoT do Azure em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="3d970-121">An Azure IoT hub under your subscription.</span></span>
  * <span data-ttu-id="3d970-122">O aplicativo cliente que envia mensagens para o hub IoT do Azure.</span><span class="sxs-lookup"><span data-stu-id="3d970-122">A client application that sends messages to your Azure IoT hub.</span></span>

## <a name="create-service-bus-namespace-and-add-a-queue-to-it"></a><span data-ttu-id="3d970-123">Criar um namespace de barramento de serviço e adicionar uma fila a ele</span><span class="sxs-lookup"><span data-stu-id="3d970-123">Create service bus namespace and add a queue to it</span></span>

### <a name="create-a-service-bus-namespace"></a><span data-ttu-id="3d970-124">Criar um namespace de barramento de serviço</span><span class="sxs-lookup"><span data-stu-id="3d970-124">Create a service bus namespace</span></span>

1. <span data-ttu-id="3d970-125">No [portal do Azure](https://portal.azure.com/), clique em **Novo** > **Integração de Empresas** > **Barramento de Serviço**.</span><span class="sxs-lookup"><span data-stu-id="3d970-125">On the [Azure portal](https://portal.azure.com/), click **New** > **Enterprise Integration** > **Service Bus**.</span></span>
1. <span data-ttu-id="3d970-126">Forneça as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="3d970-126">Provide the following information:</span></span>

   <span data-ttu-id="3d970-127">**Nome**: o nome do barramento de serviço.</span><span class="sxs-lookup"><span data-stu-id="3d970-127">**Name**: The name of the service bus.</span></span>

   <span data-ttu-id="3d970-128">**Tipo de preço**: clique em **Básico** > **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="3d970-128">**Pricing tier**: Click **Basic** > **Select**.</span></span> <span data-ttu-id="3d970-129">A camada básica é suficiente para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="3d970-129">The Basic tier is sufficient for this tutorial.</span></span>

   <span data-ttu-id="3d970-130">**Grupo de recursos**: use o mesmo grupo de recursos usado pelo seu hub IoT.</span><span class="sxs-lookup"><span data-stu-id="3d970-130">**Resource group**: Use the same resource group that your IoT hub uses.</span></span>

   <span data-ttu-id="3d970-131">**Local**: use o mesmo local que o hub IoT usa.</span><span class="sxs-lookup"><span data-stu-id="3d970-131">**Location**: Use the same location that your IoT hub uses.</span></span>
1. <span data-ttu-id="3d970-132">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="3d970-132">Click **Create**.</span></span>

   ![Criar um namespace de barramento de serviço no portal do Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/1_create-service-bus-namespace-azure-portal.png)

### <a name="add-a-service-bus-queue"></a><span data-ttu-id="3d970-134">Adicionar uma fila do barramento de serviço</span><span class="sxs-lookup"><span data-stu-id="3d970-134">Add a service bus queue</span></span>

1. <span data-ttu-id="3d970-135">Abra o namespace do barramento de serviço e, em seguida, clique em **+ Fila**.</span><span class="sxs-lookup"><span data-stu-id="3d970-135">Open the service bus namespace, and then click **+ Queue**.</span></span>
1. <span data-ttu-id="3d970-136">Insira um nome para a fila e, em seguida, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="3d970-136">Enter a name for the queue and then click **Create**.</span></span>
1. <span data-ttu-id="3d970-137">Abra a fila do barramento de serviço e, em seguida, clique em **Políticas de acesso compartilhado** > **+ Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="3d970-137">Open the service bus queue, and then click **Shared access policies** > **+ Add**.</span></span>
1. <span data-ttu-id="3d970-138">Insira um nome para a política, marque **Gerenciar** e clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="3d970-138">Enter a name for the policy, check **Manage**, and then click **Create**.</span></span>

   ![Adicionar uma fila do barramento de serviço ao portal do Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/2_add-service-bus-queue-azure-portal.png)

## <a name="add-an-endpoint-and-a-routing-rule-to-your-iot-hub"></a><span data-ttu-id="3d970-140">Adicionar um ponto de extremidade e uma regra de roteamento ao hub IoT</span><span class="sxs-lookup"><span data-stu-id="3d970-140">Add an endpoint and a routing rule to your IoT hub</span></span>

### <a name="add-an-endpoint"></a><span data-ttu-id="3d970-141">Adicionar um ponto de extremidade</span><span class="sxs-lookup"><span data-stu-id="3d970-141">Add an endpoint</span></span>

1. <span data-ttu-id="3d970-142">Abra o hub IoT, clique em Pontos de Extremidade > + Adicionar.</span><span class="sxs-lookup"><span data-stu-id="3d970-142">Open your IoT hub, click Endpoints > + Add.</span></span>
1. <span data-ttu-id="3d970-143">Insira as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="3d970-143">Enter the following information:</span></span>

   <span data-ttu-id="3d970-144">**Nome**: o nome do ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="3d970-144">**Name**: The name of the endpoint.</span></span>

   <span data-ttu-id="3d970-145">**Tipo de ponto de extremidade**: selecione **Fila do Barramento de Serviço**.</span><span class="sxs-lookup"><span data-stu-id="3d970-145">**Endpoint type**: Select **Service Bus Queue**.</span></span>

   <span data-ttu-id="3d970-146">**Namespace do Barramento de Serviço**: selecione o namespace que você criou.</span><span class="sxs-lookup"><span data-stu-id="3d970-146">**Service Bus namespace**: Select the namespace you created.</span></span>

   <span data-ttu-id="3d970-147">**Fila do Barramento de Serviço**: selecione a fila que você criou.</span><span class="sxs-lookup"><span data-stu-id="3d970-147">**Service Bus queue**: Select the queue you created.</span></span>
1. <span data-ttu-id="3d970-148">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="3d970-148">Click **OK**.</span></span>

   ![Adicionar um ponto de extremidade ao hub IoT no portal do Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/3_add-iot-hub-endpoint-azure-portal.png)

### <a name="add-a-routing-rule"></a><span data-ttu-id="3d970-150">Adicionar uma regra de roteamento</span><span class="sxs-lookup"><span data-stu-id="3d970-150">Add a routing rule</span></span>

1. <span data-ttu-id="3d970-151">No hub IoT, clique em **Rotas** > **+ Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="3d970-151">In your IoT hub, click **Routes** > **+ Add**.</span></span>
1. <span data-ttu-id="3d970-152">Insira as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="3d970-152">Enter the following information:</span></span>

   <span data-ttu-id="3d970-153">**Nome**: o nome da regra de roteamento.</span><span class="sxs-lookup"><span data-stu-id="3d970-153">**Name**: The name of the routing rule.</span></span>

   <span data-ttu-id="3d970-154">**Fonte de dados**: selecione **DeviceMessages**.</span><span class="sxs-lookup"><span data-stu-id="3d970-154">**Data source**: Select **DeviceMessages**.</span></span>

   <span data-ttu-id="3d970-155">**Ponto de extremidade**: selecione o ponto de extremidade que você criou.</span><span class="sxs-lookup"><span data-stu-id="3d970-155">**Endpoint**: Select the endpoint you created.</span></span>

   <span data-ttu-id="3d970-156">**Cadeia de caracteres de consulta**: insira `temperatureAlert = "true"`.</span><span class="sxs-lookup"><span data-stu-id="3d970-156">**Query string**: Enter `temperatureAlert = "true"`.</span></span>
1. <span data-ttu-id="3d970-157">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="3d970-157">Click **Save**.</span></span>

   ![Adicionar uma regra de roteamento no portal do Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/4_add-routing-rule-azure-portal.png)

## <a name="create-and-configure-a-logic-app"></a><span data-ttu-id="3d970-159">Criar e configurar um aplicativo lógico</span><span class="sxs-lookup"><span data-stu-id="3d970-159">Create and configure a logic app</span></span>

### <a name="create-a-logic-app"></a><span data-ttu-id="3d970-160">Criar um aplicativo lógico</span><span class="sxs-lookup"><span data-stu-id="3d970-160">Create a logic app</span></span>

1. <span data-ttu-id="3d970-161">No [portal do Azure](https://portal.azure.com/), clique em **Novo** > **Integração de Empresas** > **Aplicativo Lógico**.</span><span class="sxs-lookup"><span data-stu-id="3d970-161">In the [Azure portal](https://portal.azure.com/), click **New** > **Enterprise Integration** > **Logic App**.</span></span>
1. <span data-ttu-id="3d970-162">Insira as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="3d970-162">Enter the following information:</span></span>

   <span data-ttu-id="3d970-163">**Nome**: o nome do aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="3d970-163">**Name**: The name of the logic app.</span></span>

   <span data-ttu-id="3d970-164">**Grupo de recursos**: use o mesmo grupo de recursos usado pelo seu hub IoT.</span><span class="sxs-lookup"><span data-stu-id="3d970-164">**Resource group**: Use the same resource group that your IoT hub uses.</span></span>

   <span data-ttu-id="3d970-165">**Local**: use o mesmo local que o hub IoT usa.</span><span class="sxs-lookup"><span data-stu-id="3d970-165">**Location**: Use the same location that your IoT hub uses.</span></span>
1. <span data-ttu-id="3d970-166">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="3d970-166">Click **Create**.</span></span>

### <a name="configure-the-logic-app"></a><span data-ttu-id="3d970-167">Configurar o aplicativo lógico</span><span class="sxs-lookup"><span data-stu-id="3d970-167">Configure the logic app</span></span>

1. <span data-ttu-id="3d970-168">Abra o aplicativo lógico que é aberto no Designer de aplicativos lógicos.</span><span class="sxs-lookup"><span data-stu-id="3d970-168">Open the logic app that opens into the Logic Apps Designer.</span></span>
1. <span data-ttu-id="3d970-169">No Designer de aplicativos lógicos, clique em **Aplicativo Lógico em Branco**.</span><span class="sxs-lookup"><span data-stu-id="3d970-169">In the Logic Apps Designer, click **Blank Logic App**.</span></span>

   ![Iniciar com um aplicativo lógico em branco no portal do Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/5_start-with-blank-logic-app-azure-portal.png)

1. <span data-ttu-id="3d970-171">Clique em **Barramento de Serviço**.</span><span class="sxs-lookup"><span data-stu-id="3d970-171">Click **Service Bus**.</span></span>

   ![Selecionar o barramento de serviço para começar a criar o aplicativo lógico no portal do Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/6_select-service-bus-when-creating-blank-logic-app-azure-portal.png)

1. <span data-ttu-id="3d970-173">Clique em **Fila do Barramento de Serviço – quando uma ou mais mensagens chegam em uma fila (conclusão automática)**.</span><span class="sxs-lookup"><span data-stu-id="3d970-173">Click **Service Bus – When one or more messages arrive in a queue (auto-complete)**.</span></span>
1. <span data-ttu-id="3d970-174">Crie uma conexão do barramento de serviço.</span><span class="sxs-lookup"><span data-stu-id="3d970-174">Create a service bus connection.</span></span>
   1. <span data-ttu-id="3d970-175">Insira um nome de conexão.</span><span class="sxs-lookup"><span data-stu-id="3d970-175">Enter a connection name.</span></span>
   1. <span data-ttu-id="3d970-176">Clique no namespace do barramento de serviço > a política do barramento de serviço > **Criar**.</span><span class="sxs-lookup"><span data-stu-id="3d970-176">Click the service bus namespace > the service bus policy > **Create**.</span></span>

      ![Criar uma conexão do barramento de serviço para o aplicativo lógico no portal do Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/7_create-service-bus-connection-in-logic-app-azure-portal.png)

   1. <span data-ttu-id="3d970-178">Clique em **Continuar** depois que a conexão do barramento de serviço é criada.</span><span class="sxs-lookup"><span data-stu-id="3d970-178">Click **Continue** after the service bus connection is created.</span></span>
   1. <span data-ttu-id="3d970-179">Selecione a fila que você criou e insira `175` para **Contagem máxima de mensagens**</span><span class="sxs-lookup"><span data-stu-id="3d970-179">Select the queue that you created and enter `175` for **Maximum message count**</span></span>

      ![Especificar a contagem máxima de mensagens para a conexão do barramento de serviço no aplicativo lógico](media/iot-hub-monitoring-notifications-with-azure-logic-apps/8_specify-maximum-message-count-for-service-bus-connection-logic-app-azure-portal.png)
   1. <span data-ttu-id="3d970-181">Clique em Salvar para salvar as alterações.</span><span class="sxs-lookup"><span data-stu-id="3d970-181">Click "Save" button to save the changes.</span></span>

1. <span data-ttu-id="3d970-182">Crie uma conexão de serviço SMTP.</span><span class="sxs-lookup"><span data-stu-id="3d970-182">Create an SMTP service connection.</span></span>
   1. <span data-ttu-id="3d970-183">Clique em **Nova etapa** > **Adicionar uma ação**.</span><span class="sxs-lookup"><span data-stu-id="3d970-183">Click **New step** > **Add an action**.</span></span>
   1. <span data-ttu-id="3d970-184">Digite `SMTP`, clique no serviço **SMTP** no resultado da pesquisa e, em seguida, clique em **SMTP – Enviar Email**.</span><span class="sxs-lookup"><span data-stu-id="3d970-184">Type `SMTP`, click the **SMTP** service in the search result, and then click **SMTP - Send Email**.</span></span>

      ![Criar uma conexão SMTP em seu aplicativo lógico no portal do Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/9_create-smtp-connection-logic-app-azure-portal.png)

   1. <span data-ttu-id="3d970-186">Insira as informações de SMTP da caixa de correio e, em seguida, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="3d970-186">Enter the SMTP information of your mailbox, and then click **Create**.</span></span>

      ![Inserir informações de conexão SMTP em seu aplicativo lógico no portal do Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/10_enter-smtp-connection-info-logic-app-azure-portal.png)

      <span data-ttu-id="3d970-188">Obtenha as informações de SMTP para [Hotmail/Outlook.com](https://support.office.com/en-us/article/Add-your-Outlook-com-account-to-another-mail-app-73f3b178-0009-41ae-aab1-87b80fa94970), [Gmail](https://support.google.com/a/answer/176600?hl=en) e [Yahoo Mail](https://help.yahoo.com/kb/SLN4075.html).</span><span class="sxs-lookup"><span data-stu-id="3d970-188">Get the SMTP information for [Hotmail/Outlook.com](https://support.office.com/en-us/article/Add-your-Outlook-com-account-to-another-mail-app-73f3b178-0009-41ae-aab1-87b80fa94970), [Gmail](https://support.google.com/a/answer/176600?hl=en), and [Yahoo Mail](https://help.yahoo.com/kb/SLN4075.html).</span></span>
   1. <span data-ttu-id="3d970-189">Insira seu endereço de email para **De** e **Para**, e `High temperature detected` para **Assunto** e **Corpo**.</span><span class="sxs-lookup"><span data-stu-id="3d970-189">Enter your email address for **From** and **To**, and `High temperature detected` for **Subject** and **Body**.</span></span>
   1. <span data-ttu-id="3d970-190">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="3d970-190">Click **Save**.</span></span>

<span data-ttu-id="3d970-191">O aplicativo lógico está em funcionamento quando você o salva.</span><span class="sxs-lookup"><span data-stu-id="3d970-191">The logic app is in working order when you save it.</span></span>

## <a name="test-the-logic-app"></a><span data-ttu-id="3d970-192">Testar o aplicativo lógico</span><span class="sxs-lookup"><span data-stu-id="3d970-192">Test the logic app</span></span>

1. <span data-ttu-id="3d970-193">Inicie o aplicativo cliente que você implantar no dispositivo em [Conectar ESP8266 ao Hub IoT do Azure](iot-hub-arduino-huzzah-esp8266-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="3d970-193">Start the client application that you deploy to your device in [Connect ESP8266 to Azure IoT Hub](iot-hub-arduino-huzzah-esp8266-get-started.md).</span></span>
1. <span data-ttu-id="3d970-194">Aumente a temperatura ambiente em torno de SensorTag acima 30 C. Por exemplo, acenda uma vela em torno do SensorTag.</span><span class="sxs-lookup"><span data-stu-id="3d970-194">Increase the environment temperature around the SensorTag to be above 30 C. For example, light a candle around your SensorTag.</span></span>
1. <span data-ttu-id="3d970-195">Você deve receber uma notificação por email enviada pelo aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="3d970-195">You should receive an email notification sent by the logic app.</span></span>

   > [!NOTE]
   > <span data-ttu-id="3d970-196">O provedor de serviços de email talvez precise verificar a identidade do remetente para garantir que é você que envia o email.</span><span class="sxs-lookup"><span data-stu-id="3d970-196">Your email service provider may need to verify the sender identity to make sure it is you who sends the email.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3d970-197">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3d970-197">Next steps</span></span>

<span data-ttu-id="3d970-198">Você criou com êxito um aplicativo lógico que conecta o hub IoT e sua caixa de correio para monitoramento e notificações de temperatura.</span><span class="sxs-lookup"><span data-stu-id="3d970-198">You have successfully created a logic app that connects your IoT hub and your mailbox for temperature monitoring and notifications.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
