---
title: "aaaLearn como toouse Olá conector MQ em aplicativos do Azure lógica | Microsoft Docs"
description: "Conectar-se tooan no local ou servidor do Azure MQ de toobrowse de fluxo de trabalho de aplicativo sua lógica, receber e enviar mensagens tooWebSphere MQ"
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
ms.openlocfilehash: 8b36d53b457ced1a7461c229aecfcf8e4ae668a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooan-ibm-mq-server-from-logic-apps-using-hello-mq-connector"></a><span data-ttu-id="4b1a4-103">Conecte-se tooan servidor IBM MQ de aplicativos lógicos usando Olá MQ conector</span><span class="sxs-lookup"><span data-stu-id="4b1a4-103">Connect tooan IBM MQ server from logic apps using hello MQ connector</span></span> 

<span data-ttu-id="4b1a4-104">O Conector Microsoft para MQ envia e recupera mensagens armazenadas em um servidor MQ local ou no Azure.</span><span class="sxs-lookup"><span data-stu-id="4b1a4-104">Microsoft Connector for MQ sends and retrieves messages stored in an MQ Server on-premises, or in Azure.</span></span> <span data-ttu-id="4b1a4-105">Esse conector inclui um cliente Microsoft MQ para se comunicar com um servidor MQ IBM remoto em uma rede TCP/IP.</span><span class="sxs-lookup"><span data-stu-id="4b1a4-105">This connector includes a Microsoft MQ client that communicates with a remote IBM MQ server across a TCP/IP network.</span></span> <span data-ttu-id="4b1a4-106">Este documento é um conector MQ starter guia toouse hello.</span><span class="sxs-lookup"><span data-stu-id="4b1a4-106">This document is a starter guide toouse hello MQ connector.</span></span> <span data-ttu-id="4b1a4-107">É recomendável começar navegando em uma única mensagem em uma fila e, em seguida, tentar Olá outras ações.</span><span class="sxs-lookup"><span data-stu-id="4b1a4-107">We recommended you begin by browsing a single message on a queue, and then trying hello other actions.</span></span>    

<span data-ttu-id="4b1a4-108">conector MQ Olá inclui Olá ações a seguir.</span><span class="sxs-lookup"><span data-stu-id="4b1a4-108">hello MQ connector includes hello following actions.</span></span> <span data-ttu-id="4b1a4-109">Não há nenhum gatilho.</span><span class="sxs-lookup"><span data-stu-id="4b1a4-109">There are no triggers.</span></span>

-   <span data-ttu-id="4b1a4-110">Procurar uma única mensagem sem excluir a mensagem de saudação do hello IBM MQ Server</span><span class="sxs-lookup"><span data-stu-id="4b1a4-110">Browse a single message without deleting hello message from hello IBM MQ Server</span></span>
-   <span data-ttu-id="4b1a4-111">Procurar um lote de mensagens sem excluir mensagens de saudação do hello IBM MQ Server</span><span class="sxs-lookup"><span data-stu-id="4b1a4-111">Browse a batch of messages without deleting hello messages from hello IBM MQ Server</span></span>
-   <span data-ttu-id="4b1a4-112">Uma única mensagem de recebimento e excluir a mensagem de saudação do hello IBM MQ Server</span><span class="sxs-lookup"><span data-stu-id="4b1a4-112">Receive a single message and delete hello message from hello IBM MQ Server</span></span>
-   <span data-ttu-id="4b1a4-113">Receber um lote de mensagens e excluir mensagens de saudação da saudação IBM MQ Server</span><span class="sxs-lookup"><span data-stu-id="4b1a4-113">Receive a batch of messages and delete hello messages from hello IBM MQ Server</span></span>
-   <span data-ttu-id="4b1a4-114">Enviar uma única mensagem toohello IBM MQ Server</span><span class="sxs-lookup"><span data-stu-id="4b1a4-114">Send a single message toohello IBM MQ Server</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="4b1a4-115">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="4b1a4-115">Prerequisites</span></span>

* <span data-ttu-id="4b1a4-116">Se usar um servidor do local MQ, [instalar o gateway de dados local Olá](../logic-apps/logic-apps-gateway-install.md) em um servidor dentro de sua rede.</span><span class="sxs-lookup"><span data-stu-id="4b1a4-116">If using an on-premises MQ server, [install hello on-premises data gateway](../logic-apps/logic-apps-gateway-install.md) on a server within your network.</span></span> <span data-ttu-id="4b1a4-117">Se Olá MQ Server está publicamente disponível ou disponível no Azure, em seguida, Olá data gateway não está usado ou necessárias.</span><span class="sxs-lookup"><span data-stu-id="4b1a4-117">If hello MQ Server is publicly available, or available within Azure, then hello data gateway is not used or required.</span></span>

    > [!NOTE]
    > <span data-ttu-id="4b1a4-118">servidor de saudação onde Olá Gateway de dados local está instalado também deve ter .net Framework 4.6 instalado para Olá MQ conector toofunction.</span><span class="sxs-lookup"><span data-stu-id="4b1a4-118">hello server where hello On-Premises Data Gateway is installed must also have .Net Framework 4.6 installed for hello MQ Connector toofunction.</span></span>

* <span data-ttu-id="4b1a4-119">Criar hello recursos do Azure para gateway de dados local Olá - [configurar a conexão de gateway de dados Olá](../logic-apps/logic-apps-gateway-connection.md).</span><span class="sxs-lookup"><span data-stu-id="4b1a4-119">Create hello Azure resource for hello on-premises data gateway - [Set up hello data gateway connection](../logic-apps/logic-apps-gateway-connection.md).</span></span>

* <span data-ttu-id="4b1a4-120">Versões do IBM WebSphere MQ oficialmente com suporte:</span><span class="sxs-lookup"><span data-stu-id="4b1a4-120">Officially supported IBM WebSphere MQ versions:</span></span>
   * <span data-ttu-id="4b1a4-121">MQ 7.5</span><span class="sxs-lookup"><span data-stu-id="4b1a4-121">MQ 7.5</span></span>
   * <span data-ttu-id="4b1a4-122">MQ 8.0</span><span class="sxs-lookup"><span data-stu-id="4b1a4-122">MQ 8.0</span></span>

## <a name="create-a-logic-app"></a><span data-ttu-id="4b1a4-123">Criar um aplicativo lógico</span><span class="sxs-lookup"><span data-stu-id="4b1a4-123">Create a logic app</span></span>

1. <span data-ttu-id="4b1a4-124">Em Olá **Azure iniciar placa**, selecione  **+**  (sinal de adição), **Web + móvel**e, em seguida, **aplicativo lógico**.</span><span class="sxs-lookup"><span data-stu-id="4b1a4-124">In hello **Azure start board**, select **+** (plus sign), **Web + Mobile**, and then **Logic App**.</span></span> 
2. <span data-ttu-id="4b1a4-125">Digite hello **nome**, como MQTestApp, **assinatura**, **grupo de recursos**, e **local** (usar Olá local onde hello conexão de Gateway de dados local está configurado).</span><span class="sxs-lookup"><span data-stu-id="4b1a4-125">Enter hello **Name**, such as MQTestApp, **Subscription**, **Resource group**, and **Location** (use hello location where hello on-premises Data Gateway connection is configured).</span></span> <span data-ttu-id="4b1a4-126">Selecione **Pin toodashboard**e selecione **criar**.</span><span class="sxs-lookup"><span data-stu-id="4b1a4-126">Select **Pin toodashboard**, and select **Create**.</span></span>  
<span data-ttu-id="4b1a4-127">![Criar Aplicativo Lógico](media/connectors-create-api-mq/Create_Logic_App.png)</span><span class="sxs-lookup"><span data-stu-id="4b1a4-127">![Create Logic App](media/connectors-create-api-mq/Create_Logic_App.png)</span></span>

## <a name="add-a-trigger"></a><span data-ttu-id="4b1a4-128">Adicionar um gatilho</span><span class="sxs-lookup"><span data-stu-id="4b1a4-128">Add a trigger</span></span>

> [!NOTE]
> <span data-ttu-id="4b1a4-129">Olá MQ conector não tem todos os gatilhos.</span><span class="sxs-lookup"><span data-stu-id="4b1a4-129">hello MQ Connector does not have any triggers.</span></span> <span data-ttu-id="4b1a4-130">Assim, use outra toostart de gatilho seu aplicativo lógico, como Olá **recorrência** gatilho.</span><span class="sxs-lookup"><span data-stu-id="4b1a4-130">So, use another trigger toostart your logic app, such as hello **Recurrence** trigger.</span></span> 

1. <span data-ttu-id="4b1a4-131">Olá **lógica aplicativos Designer** é aberta, selecione **recorrência** na lista de saudação de gatilhos comuns.</span><span class="sxs-lookup"><span data-stu-id="4b1a4-131">hello **Logic Apps Designer** opens, select **Recurrence** in hello list of common triggers.</span></span>
2. <span data-ttu-id="4b1a4-132">Selecione **editar** dentro Olá gatilho de recorrência.</span><span class="sxs-lookup"><span data-stu-id="4b1a4-132">Select **Edit** within hello Recurrence Trigger.</span></span> 
3. <span data-ttu-id="4b1a4-133">Saudação de conjunto **frequência** muito**dia**e conjunto hello **intervalo** muito**7**.</span><span class="sxs-lookup"><span data-stu-id="4b1a4-133">Set hello **Frequency** too**Day**, and set hello **Interval** too**7**.</span></span> 

## <a name="browse-a-single-message"></a><span data-ttu-id="4b1a4-134">Procurar uma única mensagem</span><span class="sxs-lookup"><span data-stu-id="4b1a4-134">Browse a single message</span></span>
1. <span data-ttu-id="4b1a4-135">Selecione **+ Nova etapa** e selecione **Adicionar uma ação**.</span><span class="sxs-lookup"><span data-stu-id="4b1a4-135">Select **+ New step**, and select **Add an action**.</span></span>
2. <span data-ttu-id="4b1a4-136">Na caixa de pesquisa hello, digite `mq`e, em seguida, selecione **MQ - procurar mensagem**.</span><span class="sxs-lookup"><span data-stu-id="4b1a4-136">In hello search box, type `mq`, and then select **MQ - Browse message**.</span></span>  
<span data-ttu-id="4b1a4-137">![Procurar mensagem](media/connectors-create-api-mq/Browse_message.png)</span><span class="sxs-lookup"><span data-stu-id="4b1a4-137">![Browse message](media/connectors-create-api-mq/Browse_message.png)</span></span>

3. <span data-ttu-id="4b1a4-138">Se não houver uma conexão MQ existente, em seguida, crie conexão hello:</span><span class="sxs-lookup"><span data-stu-id="4b1a4-138">If there isn't an existing MQ connection, then create hello connection:</span></span>  

    1. <span data-ttu-id="4b1a4-139">Selecione **conectar por meio do gateway de dados local**e insira as propriedades de saudação do servidor MQ.</span><span class="sxs-lookup"><span data-stu-id="4b1a4-139">Select **Connect via on-premises data gateway**, and enter hello properties of your MQ server.</span></span>  
    <span data-ttu-id="4b1a4-140">Para **Server**, você pode inserir nome do servidor de saudação MQ ou Inserir endereço IP hello seguido por um número de porta de dois-pontos e hello.</span><span class="sxs-lookup"><span data-stu-id="4b1a4-140">For **Server**, you can enter hello MQ server name, or enter hello IP address followed by a colon and hello port number.</span></span> 
    2. <span data-ttu-id="4b1a4-141">Olá **gateway** suspensa lista as conexões de gateway existentes que foram configuradas.</span><span class="sxs-lookup"><span data-stu-id="4b1a4-141">hello **gateway** dropdown lists any existing gateway connections that have been configured.</span></span> <span data-ttu-id="4b1a4-142">Selecione seu gateway.</span><span class="sxs-lookup"><span data-stu-id="4b1a4-142">Select your gateway.</span></span>
    3. <span data-ttu-id="4b1a4-143">Selecione **Criar** quando terminar.</span><span class="sxs-lookup"><span data-stu-id="4b1a4-143">Select **Create** when finished.</span></span> <span data-ttu-id="4b1a4-144">A conexão tem a aparência a seguir toohello semelhante:</span><span class="sxs-lookup"><span data-stu-id="4b1a4-144">Your connection looks similar toohello following:</span></span>   
    <span data-ttu-id="4b1a4-145">![Propriedades da Conexão](media/connectors-create-api-mq/Connection_Properties.png)</span><span class="sxs-lookup"><span data-stu-id="4b1a4-145">![Connection Properties](media/connectors-create-api-mq/Connection_Properties.png)</span></span>

4. <span data-ttu-id="4b1a4-146">Nas propriedades de ação de saudação, você pode:</span><span class="sxs-lookup"><span data-stu-id="4b1a4-146">In hello action properties, you can:</span></span>  

    * <span data-ttu-id="4b1a4-147">Saudação de uso **fila** propriedade tooaccess um nome de outra fila que está definida na conexão Olá</span><span class="sxs-lookup"><span data-stu-id="4b1a4-147">Use hello **Queue** property tooaccess a different queue name than what is defined in hello connection</span></span>
    * <span data-ttu-id="4b1a4-148">Saudação de uso **MessageId**, **CorrelationId**, **GroupId**e toobrowse outras propriedades de uma mensagem com base nas propriedades da mensagem MQ diferentes Olá</span><span class="sxs-lookup"><span data-stu-id="4b1a4-148">Use hello **MessageId**, **CorrelationId**, **GroupId**, and other properties toobrowse for a message based on hello different MQ message properties</span></span>
    * <span data-ttu-id="4b1a4-149">Definir **IncludeInfo** muito**True** tooinclude informações de mensagem adicionais na saída de hello.</span><span class="sxs-lookup"><span data-stu-id="4b1a4-149">Set **IncludeInfo** too**True** tooinclude additional message information in hello output.</span></span> <span data-ttu-id="4b1a4-150">Ou, defina-o muito**False** toonot incluir informações adicionais de mensagem na saída de hello.</span><span class="sxs-lookup"><span data-stu-id="4b1a4-150">Or, set it too**False** toonot include additional message information in hello output.</span></span>
    * <span data-ttu-id="4b1a4-151">Insira um **Timeout** toodetermine valor toowait quanto para tooarrive uma mensagem em uma fila vazia.</span><span class="sxs-lookup"><span data-stu-id="4b1a4-151">Enter a **Timeout** value toodetermine how long toowait for a message tooarrive in an empty queue.</span></span> <span data-ttu-id="4b1a4-152">Se nada for inserido, mensagem de saudação do primeiro na fila de saudação é recuperada e não há nenhum tempo gasto aguardando tooappear uma mensagem.</span><span class="sxs-lookup"><span data-stu-id="4b1a4-152">If nothing is entered, hello first message in hello queue is retrieved, and there is no time spent waiting for a message tooappear.</span></span>  
    <span data-ttu-id="4b1a4-153">![Procurar propriedades de mensagem](media/connectors-create-api-mq/Browse_message_Props.png)</span><span class="sxs-lookup"><span data-stu-id="4b1a4-153">![Browse Message Properties](media/connectors-create-api-mq/Browse_message_Props.png)</span></span>

5. <span data-ttu-id="4b1a4-154">**Salve** suas alterações e, em seguida, **execute** seu aplicativo lógico:</span><span class="sxs-lookup"><span data-stu-id="4b1a4-154">**Save** your changes, and then **Run** your logic app:</span></span>  
<span data-ttu-id="4b1a4-155">![Salvar e Executar](media/connectors-create-api-mq/Save_Run.png)</span><span class="sxs-lookup"><span data-stu-id="4b1a4-155">![Save and run](media/connectors-create-api-mq/Save_Run.png)</span></span>

6. <span data-ttu-id="4b1a4-156">Depois de alguns segundos, etapas Olá Olá executar são mostradas, e você pode examinar a saída de hello.</span><span class="sxs-lookup"><span data-stu-id="4b1a4-156">After a few seconds, hello steps of hello run are shown, and you can look at hello output.</span></span> <span data-ttu-id="4b1a4-157">Selecione Olá marca de seleção verde toosee detalhes de cada etapa.</span><span class="sxs-lookup"><span data-stu-id="4b1a4-157">Select hello green checkmark toosee details of each step.</span></span> <span data-ttu-id="4b1a4-158">Selecione **consulte saídas brutas** toosee obter detalhes adicionais sobre Olá dados de saída.</span><span class="sxs-lookup"><span data-stu-id="4b1a4-158">Select **See raw outputs** toosee additional details on hello output data.</span></span>  
<span data-ttu-id="4b1a4-159">![Procurar saída de mensagem](media/connectors-create-api-mq/Browse_message_output.png)</span><span class="sxs-lookup"><span data-stu-id="4b1a4-159">![Browse message output](media/connectors-create-api-mq/Browse_message_output.png)</span></span>  

    <span data-ttu-id="4b1a4-160">Saída bruta:</span><span class="sxs-lookup"><span data-stu-id="4b1a4-160">Raw output:</span></span>  
    ![Procurar saída bruta de mensagem](media/connectors-create-api-mq/Browse_message_raw_output.png)

7. <span data-ttu-id="4b1a4-162">Olá quando **IncludeInfo** opção é definida tootrue, Olá saída a seguir será exibida:</span><span class="sxs-lookup"><span data-stu-id="4b1a4-162">When hello **IncludeInfo** option is set tootrue, hello following output is displayed:</span></span>  
<span data-ttu-id="4b1a4-163">![Procurar informações de inclusão da mensagem](media/connectors-create-api-mq/Browse_message_Include_Info.png)</span><span class="sxs-lookup"><span data-stu-id="4b1a4-163">![Browse message include info](media/connectors-create-api-mq/Browse_message_Include_Info.png)</span></span>

## <a name="browse-multiple-messages"></a><span data-ttu-id="4b1a4-164">Procurar várias mensagens</span><span class="sxs-lookup"><span data-stu-id="4b1a4-164">Browse multiple messages</span></span>
<span data-ttu-id="4b1a4-165">Olá **procurar mensagens** ação inclui um **BatchSize** tooindicate opção quantas mensagens devem ser retornadas da fila de saudação.</span><span class="sxs-lookup"><span data-stu-id="4b1a4-165">hello **Browse messages** action includes a **BatchSize** option tooindicate how many messages should be returned from hello queue.</span></span>  <span data-ttu-id="4b1a4-166">Se **BatchSize** não tem nenhuma entrada, todas as mensagens são retornadas.</span><span class="sxs-lookup"><span data-stu-id="4b1a4-166">If **BatchSize** has no entry, all messages are returned.</span></span> <span data-ttu-id="4b1a4-167">Olá retornado a saída é uma matriz de mensagens.</span><span class="sxs-lookup"><span data-stu-id="4b1a4-167">hello returned output is an array of messages.</span></span>

1. <span data-ttu-id="4b1a4-168">Ao adicionar Olá **procurar mensagens** ação, a conexão de primeira Olá configurado é selecionada por padrão.</span><span class="sxs-lookup"><span data-stu-id="4b1a4-168">When adding hello **Browse messages** action, hello first connection that is configured is selected by default.</span></span> <span data-ttu-id="4b1a4-169">Selecione **alterar conexão** toocreate uma nova conexão, ou selecione uma conexão diferente.</span><span class="sxs-lookup"><span data-stu-id="4b1a4-169">Select **Change connection** toocreate a new connection, or select a different connection.</span></span>

2. <span data-ttu-id="4b1a4-170">saída de Hello da procurar mensagens mostra:</span><span class="sxs-lookup"><span data-stu-id="4b1a4-170">hello output of Browse messages shows:</span></span>  
![Saída de Procurar mensagens](media/connectors-create-api-mq/Browse_messages_output.png)

## <a name="receive-a-single-message"></a><span data-ttu-id="4b1a4-172">Receber uma única mensagem</span><span class="sxs-lookup"><span data-stu-id="4b1a4-172">Receive a single message</span></span>
<span data-ttu-id="4b1a4-173">Olá **receber mensagem** ação tem Olá mesmo entradas e saídas como Olá **procurar mensagem** ação.</span><span class="sxs-lookup"><span data-stu-id="4b1a4-173">hello **Receive message** action has hello same inputs and outputs as hello **Browse message** action.</span></span> <span data-ttu-id="4b1a4-174">Ao usar **receber mensagem**, mensagem de saudação é excluída da fila de saudação.</span><span class="sxs-lookup"><span data-stu-id="4b1a4-174">When using **Receive message**, hello message is deleted from hello queue.</span></span>

## <a name="receive-multiple-messages"></a><span data-ttu-id="4b1a4-175">Receber várias mensagens</span><span class="sxs-lookup"><span data-stu-id="4b1a4-175">Receive multiple messages</span></span>
<span data-ttu-id="4b1a4-176">Olá **receber mensagens** ação tem Olá mesmo entradas e saídas como Olá **procurar mensagens** ação.</span><span class="sxs-lookup"><span data-stu-id="4b1a4-176">hello **Receive messages** action has hello same inputs and outputs as hello **Browse messages** action.</span></span> <span data-ttu-id="4b1a4-177">Ao usar **receber mensagens**, mensagens de saudação são excluídas da fila de saudação.</span><span class="sxs-lookup"><span data-stu-id="4b1a4-177">When using **Receive messages**, hello messages are deleted from hello queue.</span></span>

<span data-ttu-id="4b1a4-178">Se não houver nenhuma mensagem na fila de saudação ao fazer uma pesquisa ou receive, Olá falhar com hello saída a seguir:</span><span class="sxs-lookup"><span data-stu-id="4b1a4-178">If there are no messages in hello queue when doing a browse or a receive, hello step fails with hello following output:</span></span>  
![Erro MQ Nenhuma Mensagem](media/connectors-create-api-mq/MQ_No_Msg_Error.png)

## <a name="send-a-message"></a><span data-ttu-id="4b1a4-180">Enviar uma mensagem</span><span class="sxs-lookup"><span data-stu-id="4b1a4-180">Send a message</span></span>
1. <span data-ttu-id="4b1a4-181">Ao adicionar Olá **enviar mensagem** ação, a conexão de primeira Olá configurado é selecionada por padrão.</span><span class="sxs-lookup"><span data-stu-id="4b1a4-181">When adding hello **Send message** action, hello first connection that is configured is selected by default.</span></span> <span data-ttu-id="4b1a4-182">Selecione **alterar conexão** toocreate uma nova conexão, ou selecione uma conexão diferente.</span><span class="sxs-lookup"><span data-stu-id="4b1a4-182">Select **Change connection** toocreate a new connection, or select a different connection.</span></span> <span data-ttu-id="4b1a4-183">Olá válido **tipos de mensagem** são **datagrama**, **resposta**, ou **solicitação**.</span><span class="sxs-lookup"><span data-stu-id="4b1a4-183">hello valid **Message Types** are **Datagram**, **Reply**, or **Request**.</span></span>  
<span data-ttu-id="4b1a4-184">![Send Msg Props](media/connectors-create-api-mq/Send_Msg_Props.png)</span><span class="sxs-lookup"><span data-stu-id="4b1a4-184">![Send Msg Props](media/connectors-create-api-mq/Send_Msg_Props.png)</span></span>

2. <span data-ttu-id="4b1a4-185">Olá saída de enviar mensagem hello seguinte aparência:</span><span class="sxs-lookup"><span data-stu-id="4b1a4-185">hello output of Send message looks like hello following:</span></span>  
![Send Msg Output](media/connectors-create-api-mq/Send_Msg_Output.png)

## <a name="connector-specific-details"></a><span data-ttu-id="4b1a4-187">Detalhes específicos do conector</span><span class="sxs-lookup"><span data-stu-id="4b1a4-187">Connector-specific details</span></span>

<span data-ttu-id="4b1a4-188">Exibir quaisquer gatilhos e ações definidas em swagger Olá e também os limites de saudação [detalhes conector](/connectors/mq/).</span><span class="sxs-lookup"><span data-stu-id="4b1a4-188">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/mq/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4b1a4-189">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4b1a4-189">Next steps</span></span>
<span data-ttu-id="4b1a4-190">[Criar um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="4b1a4-190">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="4b1a4-191">Explorar Olá outros conectores disponíveis na lógica de aplicativos no nosso [lista APIs](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="4b1a4-191">Explore hello other available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>
