---
title: "monitoramento remoto de aaaIoT e notificações com os aplicativos lógicos do Azure | Microsoft Docs"
description: "Uso do Azure lógica de aplicativos para o monitoramento de temperatura de IoT em seu hub IoT e automaticamente enviar caixa de correio de tooyour notificações de email para todas as anomalias detectado."
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
ms.openlocfilehash: 89396528ed63c37258e1b49f342f0723e686ecb3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="iot-remote-monitoring-and-notifications-with-azure-logic-apps-connecting-your-iot-hub-and-mailbox"></a><span data-ttu-id="8f606-104">Monitoramento remoto IoT e notificações com o Aplicativo Lógico do Azure conectando o hub IoT e a caixa de correio</span><span class="sxs-lookup"><span data-stu-id="8f606-104">IoT remote monitoring and notifications with Azure Logic Apps connecting your IoT hub and mailbox</span></span>

![Diagrama de ponta a ponta](media/iot-hub-get-started-e2e-diagram/7.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

<span data-ttu-id="8f606-106">Aplicativos lógicos do Azure fornece uma maneira tooautomate processos como uma série de etapas.</span><span class="sxs-lookup"><span data-stu-id="8f606-106">Azure Logic Apps provides a way tooautomate processes as a series of steps.</span></span> <span data-ttu-id="8f606-107">Um aplicativo lógico pode se conectar com vários serviços e protocolos.</span><span class="sxs-lookup"><span data-stu-id="8f606-107">A logic app can connect across various services and protocols.</span></span> <span data-ttu-id="8f606-108">Ele começa com um gatilho como “Quando uma conta é adicionada”, seguido por uma combinação de ações semelhantes a “enviar uma notificação por push”.</span><span class="sxs-lookup"><span data-stu-id="8f606-108">It begins with a trigger such as 'When an account is added', and followed by a combination of actions, one like 'sending a push notification'.</span></span> <span data-ttu-id="8f606-109">Esse recurso torna os aplicativos lógicos uma solução de IoT perfeita para monitoramento de IoT, como alertas a anomalias, entre outros cenários de uso.</span><span class="sxs-lookup"><span data-stu-id="8f606-109">This feature makes Logic Apps a perfect IoT solution for IoT monitoring, such as staying alert for anomalies, among other usage scenarios.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="8f606-110">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="8f606-110">What you learn</span></span>

<span data-ttu-id="8f606-111">Você aprenderá como toocreate um aplicativo lógico que conecta o hub IoT e sua caixa de correio para monitoramento de temperatura e notificações.</span><span class="sxs-lookup"><span data-stu-id="8f606-111">You learn how toocreate a logic app that connects your IoT hub and your mailbox for temperature monitoring and notifications.</span></span> <span data-ttu-id="8f606-112">Quando a temperatura Olá estiver acima de 30 C, Olá marcas de aplicativo cliente `temperatureAlert = "true"` na mensagem de saudação envia tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="8f606-112">When hello temperature is above 30 C, hello client application marks `temperatureAlert = "true"` in hello message it sends tooyour IoT hub.</span></span> <span data-ttu-id="8f606-113">mensagem de saudação gatilhos Olá lógica aplicativo toosend você uma notificação por email.</span><span class="sxs-lookup"><span data-stu-id="8f606-113">hello message triggers hello logic app toosend you an email notification.</span></span>

## <a name="what-you-do"></a><span data-ttu-id="8f606-114">O que fazer</span><span class="sxs-lookup"><span data-stu-id="8f606-114">What you do</span></span>

* <span data-ttu-id="8f606-115">Criar um namespace de barramento de serviço e adicione um tooit de fila.</span><span class="sxs-lookup"><span data-stu-id="8f606-115">Create a service bus namespace and add a queue tooit.</span></span>
* <span data-ttu-id="8f606-116">Adicione um ponto de extremidade e um hub de IoT roteamento regra tooyour.</span><span class="sxs-lookup"><span data-stu-id="8f606-116">Add an endpoint and a routing rule tooyour IoT hub.</span></span>
* <span data-ttu-id="8f606-117">Crie, configure e teste um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="8f606-117">Create, configure, and test a logic app.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="8f606-118">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="8f606-118">What you need</span></span>

* <span data-ttu-id="8f606-119">Tutorial [configurar seu dispositivo](iot-hub-raspberry-pi-kit-node-get-started.md) concluída que abrange Olá requisitos a seguir:</span><span class="sxs-lookup"><span data-stu-id="8f606-119">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers hello following requirements:</span></span>
  * <span data-ttu-id="8f606-120">Uma assinatura ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="8f606-120">An active Azure subscription.</span></span>
  * <span data-ttu-id="8f606-121">Um hub IoT do Azure em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="8f606-121">An Azure IoT hub under your subscription.</span></span>
  * <span data-ttu-id="8f606-122">Um aplicativo cliente que envia o hub do mensagens tooyour IoT do Azure.</span><span class="sxs-lookup"><span data-stu-id="8f606-122">A client application that sends messages tooyour Azure IoT hub.</span></span>

## <a name="create-service-bus-namespace-and-add-a-queue-tooit"></a><span data-ttu-id="8f606-123">Criar um namespace de barramento de serviço e adicione um tooit de fila</span><span class="sxs-lookup"><span data-stu-id="8f606-123">Create service bus namespace and add a queue tooit</span></span>

### <a name="create-a-service-bus-namespace"></a><span data-ttu-id="8f606-124">Criar um namespace de barramento de serviço</span><span class="sxs-lookup"><span data-stu-id="8f606-124">Create a service bus namespace</span></span>

1. <span data-ttu-id="8f606-125">Em Olá [portal do Azure](https://portal.azure.com/), clique em **novo** > **integração corporativa** > **barramento de serviço**.</span><span class="sxs-lookup"><span data-stu-id="8f606-125">On hello [Azure portal](https://portal.azure.com/), click **New** > **Enterprise Integration** > **Service Bus**.</span></span>
1. <span data-ttu-id="8f606-126">Fornece Olá informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="8f606-126">Provide hello following information:</span></span>

   <span data-ttu-id="8f606-127">**Nome**: nome Olá Olá do barramento do serviço.</span><span class="sxs-lookup"><span data-stu-id="8f606-127">**Name**: hello name of hello service bus.</span></span>

   <span data-ttu-id="8f606-128">**Tipo de preço**: clique em **Básico** > **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="8f606-128">**Pricing tier**: Click **Basic** > **Select**.</span></span> <span data-ttu-id="8f606-129">a camada básica Olá é suficiente para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="8f606-129">hello Basic tier is sufficient for this tutorial.</span></span>

   <span data-ttu-id="8f606-130">**Grupo de recursos**: Use Olá mesmo grupo de recursos que usa o hub IoT.</span><span class="sxs-lookup"><span data-stu-id="8f606-130">**Resource group**: Use hello same resource group that your IoT hub uses.</span></span>

   <span data-ttu-id="8f606-131">**Local**: Use Olá mesmo local que usa o hub IoT.</span><span class="sxs-lookup"><span data-stu-id="8f606-131">**Location**: Use hello same location that your IoT hub uses.</span></span>
1. <span data-ttu-id="8f606-132">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="8f606-132">Click **Create**.</span></span>

   ![Criar um namespace de barramento de serviço no portal do Azure de saudação](media/iot-hub-monitoring-notifications-with-azure-logic-apps/1_create-service-bus-namespace-azure-portal.png)

### <a name="add-a-service-bus-queue"></a><span data-ttu-id="8f606-134">Adicionar uma fila do barramento de serviço</span><span class="sxs-lookup"><span data-stu-id="8f606-134">Add a service bus queue</span></span>

1. <span data-ttu-id="8f606-135">Abrir o namespace de barramento de serviço hello e, em seguida, clique em **+ fila**.</span><span class="sxs-lookup"><span data-stu-id="8f606-135">Open hello service bus namespace, and then click **+ Queue**.</span></span>
1. <span data-ttu-id="8f606-136">Insira um nome para a fila de saudação e, em seguida, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="8f606-136">Enter a name for hello queue and then click **Create**.</span></span>
1. <span data-ttu-id="8f606-137">Abrir a fila do barramento de serviço hello e, em seguida, clique em **políticas de acesso compartilhado** > **+ adicionar**.</span><span class="sxs-lookup"><span data-stu-id="8f606-137">Open hello service bus queue, and then click **Shared access policies** > **+ Add**.</span></span>
1. <span data-ttu-id="8f606-138">Insira um nome para a política de saudação, verifique **gerenciar**e, em seguida, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="8f606-138">Enter a name for hello policy, check **Manage**, and then click **Create**.</span></span>

   ![Adicionar uma fila do barramento de serviço no portal do Azure de saudação](media/iot-hub-monitoring-notifications-with-azure-logic-apps/2_add-service-bus-queue-azure-portal.png)

## <a name="add-an-endpoint-and-a-routing-rule-tooyour-iot-hub"></a><span data-ttu-id="8f606-140">Adicionar um ponto de extremidade e um hub de IoT roteamento regra tooyour</span><span class="sxs-lookup"><span data-stu-id="8f606-140">Add an endpoint and a routing rule tooyour IoT hub</span></span>

### <a name="add-an-endpoint"></a><span data-ttu-id="8f606-141">Adicionar um ponto final</span><span class="sxs-lookup"><span data-stu-id="8f606-141">Add an endpoint</span></span>

1. <span data-ttu-id="8f606-142">Abra o hub IoT, clique em Pontos de Extremidade > + Adicionar.</span><span class="sxs-lookup"><span data-stu-id="8f606-142">Open your IoT hub, click Endpoints > + Add.</span></span>
1. <span data-ttu-id="8f606-143">Digite hello informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="8f606-143">Enter hello following information:</span></span>

   <span data-ttu-id="8f606-144">**Nome**: nome de saudação do ponto de extremidade de saudação.</span><span class="sxs-lookup"><span data-stu-id="8f606-144">**Name**: hello name of hello endpoint.</span></span>

   <span data-ttu-id="8f606-145">**Tipo de ponto de extremidade**: selecione **Fila do Barramento de Serviço**.</span><span class="sxs-lookup"><span data-stu-id="8f606-145">**Endpoint type**: Select **Service Bus Queue**.</span></span>

   <span data-ttu-id="8f606-146">**Namespace de barramento de serviço**: selecione Olá namespace criado por você.</span><span class="sxs-lookup"><span data-stu-id="8f606-146">**Service Bus namespace**: Select hello namespace you created.</span></span>

   <span data-ttu-id="8f606-147">**Fila do barramento de serviço**: fila Olá selecione criada por você.</span><span class="sxs-lookup"><span data-stu-id="8f606-147">**Service Bus queue**: Select hello queue you created.</span></span>
1. <span data-ttu-id="8f606-148">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="8f606-148">Click **OK**.</span></span>

   ![Adicionar um hub do ponto de extremidade tooyour IoT em Olá portal do Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/3_add-iot-hub-endpoint-azure-portal.png)

### <a name="add-a-routing-rule"></a><span data-ttu-id="8f606-150">Adicionar uma regra de roteamento</span><span class="sxs-lookup"><span data-stu-id="8f606-150">Add a routing rule</span></span>

1. <span data-ttu-id="8f606-151">No hub IoT, clique em **Rotas** > **+ Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="8f606-151">In your IoT hub, click **Routes** > **+ Add**.</span></span>
1. <span data-ttu-id="8f606-152">Digite hello informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="8f606-152">Enter hello following information:</span></span>

   <span data-ttu-id="8f606-153">**Nome**: nome de saudação da regra de roteamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="8f606-153">**Name**: hello name of hello routing rule.</span></span>

   <span data-ttu-id="8f606-154">**Fonte de dados**: selecione **DeviceMessages**.</span><span class="sxs-lookup"><span data-stu-id="8f606-154">**Data source**: Select **DeviceMessages**.</span></span>

   <span data-ttu-id="8f606-155">**Ponto de extremidade**: Selecionar ponto de extremidade de saudação que você criou.</span><span class="sxs-lookup"><span data-stu-id="8f606-155">**Endpoint**: Select hello endpoint you created.</span></span>

   <span data-ttu-id="8f606-156">**Cadeia de caracteres de consulta**: insira `temperatureAlert = "true"`.</span><span class="sxs-lookup"><span data-stu-id="8f606-156">**Query string**: Enter `temperatureAlert = "true"`.</span></span>
1. <span data-ttu-id="8f606-157">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="8f606-157">Click **Save**.</span></span>

   ![Adicionar uma regra de roteamento no hello portal do Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/4_add-routing-rule-azure-portal.png)

## <a name="create-and-configure-a-logic-app"></a><span data-ttu-id="8f606-159">Criar e configurar um aplicativo lógico</span><span class="sxs-lookup"><span data-stu-id="8f606-159">Create and configure a logic app</span></span>

### <a name="create-a-logic-app"></a><span data-ttu-id="8f606-160">Criar um aplicativo lógico</span><span class="sxs-lookup"><span data-stu-id="8f606-160">Create a logic app</span></span>

1. <span data-ttu-id="8f606-161">Em Olá [portal do Azure](https://portal.azure.com/), clique em **novo** > **integração corporativa** > **aplicativo lógico**.</span><span class="sxs-lookup"><span data-stu-id="8f606-161">In hello [Azure portal](https://portal.azure.com/), click **New** > **Enterprise Integration** > **Logic App**.</span></span>
1. <span data-ttu-id="8f606-162">Digite hello informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="8f606-162">Enter hello following information:</span></span>

   <span data-ttu-id="8f606-163">**Nome**: nome de saudação do aplicativo de lógica de saudação.</span><span class="sxs-lookup"><span data-stu-id="8f606-163">**Name**: hello name of hello logic app.</span></span>

   <span data-ttu-id="8f606-164">**Grupo de recursos**: Use Olá mesmo grupo de recursos que usa o hub IoT.</span><span class="sxs-lookup"><span data-stu-id="8f606-164">**Resource group**: Use hello same resource group that your IoT hub uses.</span></span>

   <span data-ttu-id="8f606-165">**Local**: Use Olá mesmo local que usa o hub IoT.</span><span class="sxs-lookup"><span data-stu-id="8f606-165">**Location**: Use hello same location that your IoT hub uses.</span></span>
1. <span data-ttu-id="8f606-166">Clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="8f606-166">Click **Create**.</span></span>

### <a name="configure-hello-logic-app"></a><span data-ttu-id="8f606-167">Configurar o aplicativo de lógica de saudação</span><span class="sxs-lookup"><span data-stu-id="8f606-167">Configure hello logic app</span></span>

1. <span data-ttu-id="8f606-168">Abra o aplicativo de lógica de saudação que é aberta em Olá lógica do Designer de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="8f606-168">Open hello logic app that opens into hello Logic Apps Designer.</span></span>
1. <span data-ttu-id="8f606-169">No hello lógica do Designer de aplicativos, clique em **aplicativo lógica em branco**.</span><span class="sxs-lookup"><span data-stu-id="8f606-169">In hello Logic Apps Designer, click **Blank Logic App**.</span></span>

   ![Iniciar com um aplicativo em branco lógica em Olá portal do Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/5_start-with-blank-logic-app-azure-portal.png)

1. <span data-ttu-id="8f606-171">Clique em **Barramento de Serviço**.</span><span class="sxs-lookup"><span data-stu-id="8f606-171">Click **Service Bus**.</span></span>

   ![Selecione o barramento de serviço toostart criando seu aplicativo lógico no hello portal do Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/6_select-service-bus-when-creating-blank-logic-app-azure-portal.png)

1. <span data-ttu-id="8f606-173">Clique em **Fila do Barramento de Serviço – quando uma ou mais mensagens chegam em uma fila (conclusão automática)**.</span><span class="sxs-lookup"><span data-stu-id="8f606-173">Click **Service Bus – When one or more messages arrive in a queue (auto-complete)**.</span></span>
1. <span data-ttu-id="8f606-174">Crie uma conexão do barramento de serviço.</span><span class="sxs-lookup"><span data-stu-id="8f606-174">Create a service bus connection.</span></span>
   1. <span data-ttu-id="8f606-175">Insira um nome de conexão.</span><span class="sxs-lookup"><span data-stu-id="8f606-175">Enter a connection name.</span></span>
   1. <span data-ttu-id="8f606-176">Clique em namespace de barramento de serviço hello > Olá política de barramento de serviço > **criar**.</span><span class="sxs-lookup"><span data-stu-id="8f606-176">Click hello service bus namespace > hello service bus policy > **Create**.</span></span>

      ![Criar uma conexão de barramento de serviço para seu aplicativo lógica no hello portal do Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/7_create-service-bus-connection-in-logic-app-azure-portal.png)

   1. <span data-ttu-id="8f606-178">Clique em **continuar** após a conexão de barramento de serviço Olá é criado.</span><span class="sxs-lookup"><span data-stu-id="8f606-178">Click **Continue** after hello service bus connection is created.</span></span>
   1. <span data-ttu-id="8f606-179">Selecione a fila de saudação que você criou e insira `175` para **contagem máxima de mensagem**</span><span class="sxs-lookup"><span data-stu-id="8f606-179">Select hello queue that you created and enter `175` for **Maximum message count**</span></span>

      ![Especificar a contagem de máximo de mensagem de saudação para conexão de barramento de serviço Olá em seu aplicativo de lógica](media/iot-hub-monitoring-notifications-with-azure-logic-apps/8_specify-maximum-message-count-for-service-bus-connection-logic-app-azure-portal.png)
   1. <span data-ttu-id="8f606-181">Clique em "Salvar" botão toosave Olá alterações.</span><span class="sxs-lookup"><span data-stu-id="8f606-181">Click "Save" button toosave hello changes.</span></span>

1. <span data-ttu-id="8f606-182">Crie uma conexão de serviço SMTP.</span><span class="sxs-lookup"><span data-stu-id="8f606-182">Create an SMTP service connection.</span></span>
   1. <span data-ttu-id="8f606-183">Clique em **Nova etapa** > **Adicionar uma ação**.</span><span class="sxs-lookup"><span data-stu-id="8f606-183">Click **New step** > **Add an action**.</span></span>
   1. <span data-ttu-id="8f606-184">Tipo `SMTP`, clique em Olá **SMTP** no resultado da pesquisa de saudação do serviço e, em seguida, clique em **SMTP - Enviar Email**.</span><span class="sxs-lookup"><span data-stu-id="8f606-184">Type `SMTP`, click hello **SMTP** service in hello search result, and then click **SMTP - Send Email**.</span></span>

      ![Criar uma conexão SMTP no seu aplicativo lógica Olá portal do Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/9_create-smtp-connection-logic-app-azure-portal.png)

   1. <span data-ttu-id="8f606-186">Insira informações de saudação SMTP da caixa de correio e, em seguida, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="8f606-186">Enter hello SMTP information of your mailbox, and then click **Create**.</span></span>

      ![Insira informações de conexão SMTP em seu aplicativo de lógica em Olá portal do Azure](media/iot-hub-monitoring-notifications-with-azure-logic-apps/10_enter-smtp-connection-info-logic-app-azure-portal.png)

      <span data-ttu-id="8f606-188">Obter informações de saudação SMTP para [Hotmail/Outlook.com](https://support.office.com/en-us/article/Add-your-Outlook-com-account-to-another-mail-app-73f3b178-0009-41ae-aab1-87b80fa94970), [Gmail](https://support.google.com/a/answer/176600?hl=en), e [Yahoo Mail](https://help.yahoo.com/kb/SLN4075.html).</span><span class="sxs-lookup"><span data-stu-id="8f606-188">Get hello SMTP information for [Hotmail/Outlook.com](https://support.office.com/en-us/article/Add-your-Outlook-com-account-to-another-mail-app-73f3b178-0009-41ae-aab1-87b80fa94970), [Gmail](https://support.google.com/a/answer/176600?hl=en), and [Yahoo Mail](https://help.yahoo.com/kb/SLN4075.html).</span></span>
   1. <span data-ttu-id="8f606-189">Insira seu endereço de email para **De** e **Para**, e `High temperature detected` para **Assunto** e **Corpo**.</span><span class="sxs-lookup"><span data-stu-id="8f606-189">Enter your email address for **From** and **To**, and `High temperature detected` for **Subject** and **Body**.</span></span>
   1. <span data-ttu-id="8f606-190">Clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="8f606-190">Click **Save**.</span></span>

<span data-ttu-id="8f606-191">Olá lógica aplicativo está em funcionamento quando você salvá-lo.</span><span class="sxs-lookup"><span data-stu-id="8f606-191">hello logic app is in working order when you save it.</span></span>

## <a name="test-hello-logic-app"></a><span data-ttu-id="8f606-192">Aplicativo de lógica de saudação do teste</span><span class="sxs-lookup"><span data-stu-id="8f606-192">Test hello logic app</span></span>

1. <span data-ttu-id="8f606-193">Iniciar aplicativo cliente Olá que você implantar o dispositivo tooyour no [tooAzure ESP8266 conectar IoT Hub](iot-hub-arduino-huzzah-esp8266-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="8f606-193">Start hello client application that you deploy tooyour device in [Connect ESP8266 tooAzure IoT Hub](iot-hub-arduino-huzzah-esp8266-get-started.md).</span></span>
1. <span data-ttu-id="8f606-194">Aumentar a temperatura do ambiente Olá em torno de saudação SensorTag toobe acima c 30. Por exemplo, claro uma vela em torno de seu SensorTag.</span><span class="sxs-lookup"><span data-stu-id="8f606-194">Increase hello environment temperature around hello SensorTag toobe above 30 C. For example, light a candle around your SensorTag.</span></span>
1. <span data-ttu-id="8f606-195">Você deve receber uma notificação por email enviada pelo aplicativo de lógica de saudação.</span><span class="sxs-lookup"><span data-stu-id="8f606-195">You should receive an email notification sent by hello logic app.</span></span>

   > [!NOTE]
   > <span data-ttu-id="8f606-196">O provedor de serviços de email pode ser necessário tooverify Olá remetente identidade toomake que é você quem envia email hello.</span><span class="sxs-lookup"><span data-stu-id="8f606-196">Your email service provider may need tooverify hello sender identity toomake sure it is you who sends hello email.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8f606-197">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8f606-197">Next steps</span></span>

<span data-ttu-id="8f606-198">Você criou com êxito um aplicativo lógico que conecta o hub IoT e sua caixa de correio para monitoramento e notificações de temperatura.</span><span class="sxs-lookup"><span data-stu-id="8f606-198">You have successfully created a logic app that connects your IoT hub and your mailbox for temperature monitoring and notifications.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
