---
title: "Saiba como usar o conector do MQ no Aplicativo Lógico do Azure | Microsoft Docs"
description: "Conectar-se a um local ou servidor MQ do Azure do seu fluxo de trabalho do aplicativo lógico para procurar, receber e enviar mensagens para o WebSphere MQ"
services: logic-apps
author: valthom
manager: anneta
documentationcenter: 
editor: 
tags: connectors
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 06/01/2017
ms.author: valthom; ladocs
ms.openlocfilehash: 17c651585b56dae186286f5d8c68c363ae9c524d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="connect-to-an-ibm-mq-server-from-logic-apps-using-the-mq-connector"></a><span data-ttu-id="a4899-103">Conectar-se a um servidor do IBM MQ de aplicativos lógicos usando o conector MQ</span><span class="sxs-lookup"><span data-stu-id="a4899-103">Connect to an IBM MQ server from logic apps using the MQ connector</span></span> 

<span data-ttu-id="a4899-104">O Conector Microsoft para MQ envia e recupera mensagens armazenadas em um servidor MQ local ou no Azure.</span><span class="sxs-lookup"><span data-stu-id="a4899-104">Microsoft Connector for MQ sends and retrieves messages stored in an MQ Server on-premises, or in Azure.</span></span> <span data-ttu-id="a4899-105">Esse conector inclui um cliente Microsoft MQ para se comunicar com um servidor MQ IBM remoto em uma rede TCP/IP.</span><span class="sxs-lookup"><span data-stu-id="a4899-105">This connector includes a Microsoft MQ client that communicates with a remote IBM MQ server across a TCP/IP network.</span></span> <span data-ttu-id="a4899-106">Este documento é um guia introdutório para usar o conector MQ.</span><span class="sxs-lookup"><span data-stu-id="a4899-106">This document is a starter guide to use the MQ connector.</span></span> <span data-ttu-id="a4899-107">É recomendável que você comece procurando uma única mensagem em uma fila e, em seguida, tente as outras ações.</span><span class="sxs-lookup"><span data-stu-id="a4899-107">We recommended you begin by browsing a single message on a queue, and then trying the other actions.</span></span>    

<span data-ttu-id="a4899-108">O Conector do MQ inclui as ações a seguir.</span><span class="sxs-lookup"><span data-stu-id="a4899-108">The MQ connector includes the following actions.</span></span> <span data-ttu-id="a4899-109">Não há nenhum gatilho.</span><span class="sxs-lookup"><span data-stu-id="a4899-109">There are no triggers.</span></span>

-   <span data-ttu-id="a4899-110">Procurar uma única mensagem sem excluí-la do servidor IBM MQ</span><span class="sxs-lookup"><span data-stu-id="a4899-110">Browse a single message without deleting the message from the IBM MQ Server</span></span>
-   <span data-ttu-id="a4899-111">Procurar um lote de mensagens sem excluí-las do servidor IBM MQ</span><span class="sxs-lookup"><span data-stu-id="a4899-111">Browse a batch of messages without deleting the messages from the IBM MQ Server</span></span>
-   <span data-ttu-id="a4899-112">Receber uma única mensagem e excluí-la do servidor IBM MQ</span><span class="sxs-lookup"><span data-stu-id="a4899-112">Receive a single message and delete the message from the IBM MQ Server</span></span>
-   <span data-ttu-id="a4899-113">Receber um lote de mensagens e excluí-las do servidor IBM MQ</span><span class="sxs-lookup"><span data-stu-id="a4899-113">Receive a batch of messages and delete the messages from the IBM MQ Server</span></span>
-   <span data-ttu-id="a4899-114">Enviar uma única mensagem ao servidor IBM MQ</span><span class="sxs-lookup"><span data-stu-id="a4899-114">Send a single message to the IBM MQ Server</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="a4899-115">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a4899-115">Prerequisites</span></span>

* <span data-ttu-id="a4899-116">Se você usar um servidor MQ local, [instale o gateway de dados local](../logic-apps/logic-apps-gateway-install.md) em um servidor dentro de sua rede.</span><span class="sxs-lookup"><span data-stu-id="a4899-116">If using an on-premises MQ server, [install the on-premises data gateway](../logic-apps/logic-apps-gateway-install.md) on a server within your network.</span></span> <span data-ttu-id="a4899-117">Se o servidor MQ está publicamente disponível ou disponível no Azure, o gateway de dados não é usado nem necessário.</span><span class="sxs-lookup"><span data-stu-id="a4899-117">If the MQ Server is publicly available, or available within Azure, then the data gateway is not used or required.</span></span>

    > [!NOTE]
    > <span data-ttu-id="a4899-118">O servidor em que o gateway de dados local está instalado também deve ter o .NET Framework 4.6 instalado para que o conector MQ funcione.</span><span class="sxs-lookup"><span data-stu-id="a4899-118">The server where the On-Premises Data Gateway is installed must also have .Net Framework 4.6 installed for the MQ Connector to function.</span></span>

* <span data-ttu-id="a4899-119">Criar o recurso do Azure para o gateway de dados local – [configurar a conexão de gateway de dados](../logic-apps/logic-apps-gateway-connection.md).</span><span class="sxs-lookup"><span data-stu-id="a4899-119">Create the Azure resource for the on-premises data gateway - [Set up the data gateway connection](../logic-apps/logic-apps-gateway-connection.md).</span></span>

* <span data-ttu-id="a4899-120">Versões do IBM WebSphere MQ oficialmente com suporte:</span><span class="sxs-lookup"><span data-stu-id="a4899-120">Officially supported IBM WebSphere MQ versions:</span></span>
   * <span data-ttu-id="a4899-121">MQ 7.5</span><span class="sxs-lookup"><span data-stu-id="a4899-121">MQ 7.5</span></span>
   * <span data-ttu-id="a4899-122">MQ 8.0</span><span class="sxs-lookup"><span data-stu-id="a4899-122">MQ 8.0</span></span>

## <a name="create-a-logic-app"></a><span data-ttu-id="a4899-123">Criar um aplicativo lógico</span><span class="sxs-lookup"><span data-stu-id="a4899-123">Create a logic app</span></span>

1. <span data-ttu-id="a4899-124">Na **tela inicial do Azure**, selecione **+** (sinal de mais), **Web + Móvel**, e então, **Aplicativo Lógico**.</span><span class="sxs-lookup"><span data-stu-id="a4899-124">In the **Azure start board**, select **+** (plus sign), **Web + Mobile**, and then **Logic App**.</span></span> 
2. <span data-ttu-id="a4899-125">Insira o **Nome**, tal como MQTestApp, **Assinatura**, **Grupo de recursos** e **Localização** (use a localização em que a conexão de gateway de dados local está configurada).</span><span class="sxs-lookup"><span data-stu-id="a4899-125">Enter the **Name**, such as MQTestApp, **Subscription**, **Resource group**, and **Location** (use the location where the on-premises Data Gateway connection is configured).</span></span> <span data-ttu-id="a4899-126">Selecione **Fixar no painel** e selecione **Criar**.</span><span class="sxs-lookup"><span data-stu-id="a4899-126">Select **Pin to dashboard**, and select **Create**.</span></span>  
<span data-ttu-id="a4899-127">![Criar Aplicativo Lógico](media/connectors-create-api-mq/Create_Logic_App.png)</span><span class="sxs-lookup"><span data-stu-id="a4899-127">![Create Logic App](media/connectors-create-api-mq/Create_Logic_App.png)</span></span>

## <a name="add-a-trigger"></a><span data-ttu-id="a4899-128">Adicionar um gatilho</span><span class="sxs-lookup"><span data-stu-id="a4899-128">Add a trigger</span></span>

> [!NOTE]
> <span data-ttu-id="a4899-129">O conector MQ não tem gatilhos.</span><span class="sxs-lookup"><span data-stu-id="a4899-129">The MQ Connector does not have any triggers.</span></span> <span data-ttu-id="a4899-130">Portanto, use outro gatilho para iniciar seu aplicativo lógico, tal como o gatilho **Recorrência**.</span><span class="sxs-lookup"><span data-stu-id="a4899-130">So, use another trigger to start your logic app, such as the **Recurrence** trigger.</span></span> 

1. <span data-ttu-id="a4899-131">O **Designer de Aplicativos Lógicos** é aberto, selecione **Recorrência** na lista de gatilhos comuns.</span><span class="sxs-lookup"><span data-stu-id="a4899-131">The **Logic Apps Designer** opens, select **Recurrence** in the list of common triggers.</span></span>
2. <span data-ttu-id="a4899-132">Selecione **Editar** dentro do gatilho Recorrência.</span><span class="sxs-lookup"><span data-stu-id="a4899-132">Select **Edit** within the Recurrence Trigger.</span></span> 
3. <span data-ttu-id="a4899-133">Defina a **Frequência** para **Dia** e defina o **Intervalo** como **7**.</span><span class="sxs-lookup"><span data-stu-id="a4899-133">Set the **Frequency** to **Day**, and set the **Interval** to **7**.</span></span> 

## <a name="browse-a-single-message"></a><span data-ttu-id="a4899-134">Procurar uma única mensagem</span><span class="sxs-lookup"><span data-stu-id="a4899-134">Browse a single message</span></span>
1. <span data-ttu-id="a4899-135">Selecione **+ Nova etapa** e selecione **Adicionar uma ação**.</span><span class="sxs-lookup"><span data-stu-id="a4899-135">Select **+ New step**, and select **Add an action**.</span></span>
2. <span data-ttu-id="a4899-136">Na caixa de pesquisa, digite `mq` e, em seguida, selecione **MQ – procurar mensagem**.</span><span class="sxs-lookup"><span data-stu-id="a4899-136">In the search box, type `mq`, and then select **MQ - Browse message**.</span></span>  
<span data-ttu-id="a4899-137">![Procurar mensagem](media/connectors-create-api-mq/Browse_message.png)</span><span class="sxs-lookup"><span data-stu-id="a4899-137">![Browse message](media/connectors-create-api-mq/Browse_message.png)</span></span>

3. <span data-ttu-id="a4899-138">Se não houver uma conexão MQ existente, crie a conexão:</span><span class="sxs-lookup"><span data-stu-id="a4899-138">If there isn't an existing MQ connection, then create the connection:</span></span>  

    1. <span data-ttu-id="a4899-139">Selecione **Conectar-se por meio do gateway de dados local** e insira as propriedades do servidor MQ.</span><span class="sxs-lookup"><span data-stu-id="a4899-139">Select **Connect via on-premises data gateway**, and enter the properties of your MQ server.</span></span>  
    <span data-ttu-id="a4899-140">Para **Servidor**, você pode digitar o nome do servidor MQ ou digitar o endereço IP seguido por dois-pontos e o número da porta.</span><span class="sxs-lookup"><span data-stu-id="a4899-140">For **Server**, you can enter the MQ server name, or enter the IP address followed by a colon and the port number.</span></span> 
    2. <span data-ttu-id="a4899-141">A lista suspensa **gateway** lista quaisquer conexões de gateway existentes que tenham sido configuradas.</span><span class="sxs-lookup"><span data-stu-id="a4899-141">The **gateway** dropdown lists any existing gateway connections that have been configured.</span></span> <span data-ttu-id="a4899-142">Selecione seu gateway.</span><span class="sxs-lookup"><span data-stu-id="a4899-142">Select your gateway.</span></span>
    3. <span data-ttu-id="a4899-143">Selecione **Criar** quando terminar.</span><span class="sxs-lookup"><span data-stu-id="a4899-143">Select **Create** when finished.</span></span> <span data-ttu-id="a4899-144">A conexão é semelhante ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="a4899-144">Your connection looks similar to the following:</span></span>   
    <span data-ttu-id="a4899-145">![Propriedades da Conexão](media/connectors-create-api-mq/Connection_Properties.png)</span><span class="sxs-lookup"><span data-stu-id="a4899-145">![Connection Properties](media/connectors-create-api-mq/Connection_Properties.png)</span></span>

4. <span data-ttu-id="a4899-146">Nas propriedades da ação, você pode:</span><span class="sxs-lookup"><span data-stu-id="a4899-146">In the action properties, you can:</span></span>  

    * <span data-ttu-id="a4899-147">Use a propriedade **Fila** para acessar um nome fila diferente do que está definido na conexão</span><span class="sxs-lookup"><span data-stu-id="a4899-147">Use the **Queue** property to access a different queue name than what is defined in the connection</span></span>
    * <span data-ttu-id="a4899-148">Use **MessageId**, **CorrelationId**, **GroupId**e outras propriedades para procurar uma mensagem com base nas propriedades de mensagem do MQ diferentes</span><span class="sxs-lookup"><span data-stu-id="a4899-148">Use the **MessageId**, **CorrelationId**, **GroupId**, and other properties to browse for a message based on the different MQ message properties</span></span>
    * <span data-ttu-id="a4899-149">Defina **IncludeInfo** como **True** para incluir informações adicionais da mensagem na saída.</span><span class="sxs-lookup"><span data-stu-id="a4899-149">Set **IncludeInfo** to **True** to include additional message information in the output.</span></span> <span data-ttu-id="a4899-150">Ou defina-o como **False** para não incluir informações adicionais da mensagem na saída.</span><span class="sxs-lookup"><span data-stu-id="a4899-150">Or, set it to **False** to not include additional message information in the output.</span></span>
    * <span data-ttu-id="a4899-151">Insira um valor de **Tempo limite** para determinar por quanto tempo aguardar até que uma mensagem chegue em uma fila vazia.</span><span class="sxs-lookup"><span data-stu-id="a4899-151">Enter a **Timeout** value to determine how long to wait for a message to arrive in an empty queue.</span></span> <span data-ttu-id="a4899-152">Se nada for inserido, a primeira mensagem na fila será recuperada e não nenhum tempo será perdido esperando que uma mensagem apareça.</span><span class="sxs-lookup"><span data-stu-id="a4899-152">If nothing is entered, the first message in the queue is retrieved, and there is no time spent waiting for a message to appear.</span></span>  
    <span data-ttu-id="a4899-153">![Procurar propriedades de mensagem](media/connectors-create-api-mq/Browse_message_Props.png)</span><span class="sxs-lookup"><span data-stu-id="a4899-153">![Browse Message Properties](media/connectors-create-api-mq/Browse_message_Props.png)</span></span>

5. <span data-ttu-id="a4899-154">**Salve** suas alterações e, em seguida, **execute** seu aplicativo lógico:</span><span class="sxs-lookup"><span data-stu-id="a4899-154">**Save** your changes, and then **Run** your logic app:</span></span>  
<span data-ttu-id="a4899-155">![Salvar e Executar](media/connectors-create-api-mq/Save_Run.png)</span><span class="sxs-lookup"><span data-stu-id="a4899-155">![Save and run](media/connectors-create-api-mq/Save_Run.png)</span></span>

6. <span data-ttu-id="a4899-156">Depois de alguns segundos, as etapas da execução são mostradas e você pode examinar a saída.</span><span class="sxs-lookup"><span data-stu-id="a4899-156">After a few seconds, the steps of the run are shown, and you can look at the output.</span></span> <span data-ttu-id="a4899-157">Selecione a marca de seleção verde para ver os detalhes de cada etapa.</span><span class="sxs-lookup"><span data-stu-id="a4899-157">Select the green checkmark to see details of each step.</span></span> <span data-ttu-id="a4899-158">Selecione **Ver saídas brutas** para ver detalhes adicionais sobre os dados de saída.</span><span class="sxs-lookup"><span data-stu-id="a4899-158">Select **See raw outputs** to see additional details on the output data.</span></span>  
<span data-ttu-id="a4899-159">![Procurar saída de mensagem](media/connectors-create-api-mq/Browse_message_output.png)</span><span class="sxs-lookup"><span data-stu-id="a4899-159">![Browse message output](media/connectors-create-api-mq/Browse_message_output.png)</span></span>  

    <span data-ttu-id="a4899-160">Saída bruta:</span><span class="sxs-lookup"><span data-stu-id="a4899-160">Raw output:</span></span>  
    ![Procurar saída bruta de mensagem](media/connectors-create-api-mq/Browse_message_raw_output.png)

7. <span data-ttu-id="a4899-162">Quando a opção **IncludeInfo** é definida como true, a seguinte saída é exibida:</span><span class="sxs-lookup"><span data-stu-id="a4899-162">When the **IncludeInfo** option is set to true, the following output is displayed:</span></span>  
<span data-ttu-id="a4899-163">![Procurar informações de inclusão da mensagem](media/connectors-create-api-mq/Browse_message_Include_Info.png)</span><span class="sxs-lookup"><span data-stu-id="a4899-163">![Browse message include info](media/connectors-create-api-mq/Browse_message_Include_Info.png)</span></span>

## <a name="browse-multiple-messages"></a><span data-ttu-id="a4899-164">Procurar várias mensagens</span><span class="sxs-lookup"><span data-stu-id="a4899-164">Browse multiple messages</span></span>
<span data-ttu-id="a4899-165">A ação **Procurar mensagens** inclui uma opção **BatchSize** para indicar quantas mensagens devem ser retornadas da fila.</span><span class="sxs-lookup"><span data-stu-id="a4899-165">The **Browse messages** action includes a **BatchSize** option to indicate how many messages should be returned from the queue.</span></span>  <span data-ttu-id="a4899-166">Se **BatchSize** não tem nenhuma entrada, todas as mensagens são retornadas.</span><span class="sxs-lookup"><span data-stu-id="a4899-166">If **BatchSize** has no entry, all messages are returned.</span></span> <span data-ttu-id="a4899-167">A saída retornada é uma matriz de mensagens.</span><span class="sxs-lookup"><span data-stu-id="a4899-167">The returned output is an array of messages.</span></span>

1. <span data-ttu-id="a4899-168">Ao adicionar a ação **Procurar mensagens**, a primeira conexão configurada é selecionada por padrão.</span><span class="sxs-lookup"><span data-stu-id="a4899-168">When adding the **Browse messages** action, the first connection that is configured is selected by default.</span></span> <span data-ttu-id="a4899-169">Selecione **Alterar conexão** para criar uma nova conexão ou selecione uma conexão diferente.</span><span class="sxs-lookup"><span data-stu-id="a4899-169">Select **Change connection** to create a new connection, or select a different connection.</span></span>

2. <span data-ttu-id="a4899-170">A saída de Procurar mensagens mostra:</span><span class="sxs-lookup"><span data-stu-id="a4899-170">The output of Browse messages shows:</span></span>  
![Saída de Procurar mensagens](media/connectors-create-api-mq/Browse_messages_output.png)

## <a name="receive-a-single-message"></a><span data-ttu-id="a4899-172">Receber uma única mensagem</span><span class="sxs-lookup"><span data-stu-id="a4899-172">Receive a single message</span></span>
<span data-ttu-id="a4899-173">A ação **Receber mensagem** tem as mesmas entradas e saídas que a ação **Procurar mensagem**.</span><span class="sxs-lookup"><span data-stu-id="a4899-173">The **Receive message** action has the same inputs and outputs as the **Browse message** action.</span></span> <span data-ttu-id="a4899-174">Ao usar **Receber mensagem**, a mensagem é excluída da fila.</span><span class="sxs-lookup"><span data-stu-id="a4899-174">When using **Receive message**, the message is deleted from the queue.</span></span>

## <a name="receive-multiple-messages"></a><span data-ttu-id="a4899-175">Receber várias mensagens</span><span class="sxs-lookup"><span data-stu-id="a4899-175">Receive multiple messages</span></span>
<span data-ttu-id="a4899-176">A ação **Receber mensagens** tem as mesmas entradas e saídas que a ação **Procurar mensagens**.</span><span class="sxs-lookup"><span data-stu-id="a4899-176">The **Receive messages** action has the same inputs and outputs as the **Browse messages** action.</span></span> <span data-ttu-id="a4899-177">Ao usar **Receber mensagens**, as mensagens são excluídas da fila.</span><span class="sxs-lookup"><span data-stu-id="a4899-177">When using **Receive messages**, the messages are deleted from the queue.</span></span>

<span data-ttu-id="a4899-178">Se não houver nenhuma mensagem na fila ao fazer uma pesquisa ou um recebimento, a etapa falhará com a seguinte saída:</span><span class="sxs-lookup"><span data-stu-id="a4899-178">If there are no messages in the queue when doing a browse or a receive, the step fails with the following output:</span></span>  
![Erro MQ Nenhuma Mensagem](media/connectors-create-api-mq/MQ_No_Msg_Error.png)

## <a name="send-a-message"></a><span data-ttu-id="a4899-180">Enviar uma mensagem</span><span class="sxs-lookup"><span data-stu-id="a4899-180">Send a message</span></span>
1. <span data-ttu-id="a4899-181">Ao adicionar a ação **Enviar mensagem**, a primeira conexão configurada é selecionada por padrão.</span><span class="sxs-lookup"><span data-stu-id="a4899-181">When adding the **Send message** action, the first connection that is configured is selected by default.</span></span> <span data-ttu-id="a4899-182">Selecione **Alterar conexão** para criar uma nova conexão ou selecione uma conexão diferente.</span><span class="sxs-lookup"><span data-stu-id="a4899-182">Select **Change connection** to create a new connection, or select a different connection.</span></span> <span data-ttu-id="a4899-183">Os **Tipos de Mensagem** válidos são **Datagrama**, **Resposta** ou **Solicitação**.</span><span class="sxs-lookup"><span data-stu-id="a4899-183">The valid **Message Types** are **Datagram**, **Reply**, or **Request**.</span></span>  
<span data-ttu-id="a4899-184">![Send Msg Props](media/connectors-create-api-mq/Send_Msg_Props.png)</span><span class="sxs-lookup"><span data-stu-id="a4899-184">![Send Msg Props](media/connectors-create-api-mq/Send_Msg_Props.png)</span></span>

2. <span data-ttu-id="a4899-185">A saída de Enviar mensagem se parece com o seguinte:</span><span class="sxs-lookup"><span data-stu-id="a4899-185">The output of Send message looks like the following:</span></span>  
![Send Msg Output](media/connectors-create-api-mq/Send_Msg_Output.png)

## <a name="connector-specific-details"></a><span data-ttu-id="a4899-187">Detalhes específicos do conector</span><span class="sxs-lookup"><span data-stu-id="a4899-187">Connector-specific details</span></span>

<span data-ttu-id="a4899-188">Exiba os gatilhos e ações definidos no swagger e também os limites nos [detalhes do conector](/connectors/mq/).</span><span class="sxs-lookup"><span data-stu-id="a4899-188">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/mq/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a4899-189">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a4899-189">Next steps</span></span>
<span data-ttu-id="a4899-190">[Criar um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="a4899-190">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="a4899-191">Explore os outros conectores disponíveis nos Aplicativos Lógicos em nossa [lista de APIs](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="a4899-191">Explore the other available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>
