---
title: "aaaBatch processar mensagens como um grupo ou uma coleção - os aplicativos lógicos do Azure | Microsoft Docs"
description: "Enviar e receber mensagens para processamento em lotes em aplicativos lógicos"
keywords: lote, processo em lote
author: jonfancey
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/7/2017
ms.author: LADocs; estfan; jonfan
ms.openlocfilehash: 2603db71ee0659d5b6bf5ce3d32f1b0d13c34194
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="send-receive-and-batch-process-messages-in-logic-apps"></a><span data-ttu-id="9e063-104">Enviar, receber e processar mensagens em lote nos aplicativos lógicos</span><span class="sxs-lookup"><span data-stu-id="9e063-104">Send, receive, and batch process messages in logic apps</span></span>

<span data-ttu-id="9e063-105">mensagens de tooprocess juntas em grupos, você pode enviar dados tooa de itens ou mensagens de *lote*e depois processar os itens como um lote.</span><span class="sxs-lookup"><span data-stu-id="9e063-105">tooprocess messages together in groups, you can send data items, or messages, tooa *batch*, and then process those items as a batch.</span></span> <span data-ttu-id="9e063-106">Essa abordagem é útil quando você deseja toomake-se de itens de dados são agrupados de forma específica e são processados em conjunto.</span><span class="sxs-lookup"><span data-stu-id="9e063-106">This approach is useful when you want toomake sure data items are grouped in a specific way and are processed together.</span></span> 

<span data-ttu-id="9e063-107">Você pode criar aplicativos lógicos que recebem itens como um lote usando Olá **lote** gatilho.</span><span class="sxs-lookup"><span data-stu-id="9e063-107">You can create logic apps that receive items as a batch by using hello **Batch** trigger.</span></span> <span data-ttu-id="9e063-108">Você pode criar aplicativos lógicos que enviam itens tooa lote usando Olá **lote** ação.</span><span class="sxs-lookup"><span data-stu-id="9e063-108">You can then create logic apps that send items tooa batch by using hello **Batch** action.</span></span>

<span data-ttu-id="9e063-109">Este tópico mostra como você pode compilar uma solução de envio em lote executando estas tarefas:</span><span class="sxs-lookup"><span data-stu-id="9e063-109">This topic shows how you can build a batching solution by performing these tasks:</span></span> 

* <span data-ttu-id="9e063-110">[Criar um aplicativo lógico que receba e colete itens como um lote](#batch-receiver).</span><span class="sxs-lookup"><span data-stu-id="9e063-110">[Create a logic app that receives and collects items as a batch](#batch-receiver).</span></span> <span data-ttu-id="9e063-111">Este aplicativo de lógica de "destinatário lote" Especifica Olá lote nome e versão critérios toomeet antes Olá receptor lógica aplicativo libera e processa os itens.</span><span class="sxs-lookup"><span data-stu-id="9e063-111">This "batch receiver" logic app specifies hello batch name and release criteria toomeet before hello receiver logic app releases and processes items.</span></span> 

* <span data-ttu-id="9e063-112">[Criar um aplicativo de lógica que envia itens tooa lote](#batch-sender).</span><span class="sxs-lookup"><span data-stu-id="9e063-112">[Create a logic app that sends items tooa batch](#batch-sender).</span></span> <span data-ttu-id="9e063-113">Este aplicativo de lógica de "remetente lote" Especifica onde toosend itens, que devem ser um aplicativo de lógica de destinatário existente do lote.</span><span class="sxs-lookup"><span data-stu-id="9e063-113">This "batch sender" logic app specifies where toosend items, which must be an existing batch receiver logic app.</span></span> <span data-ttu-id="9e063-114">Você pode também especificar uma chave exclusiva, como um número de cliente, muito "partition" ou dividir o lote de destino Olá em subconjuntos com base na chave.</span><span class="sxs-lookup"><span data-stu-id="9e063-114">You can also specify a unique key, like a customer number, too"partition", or divide, hello target batch into subsets based on that key.</span></span> <span data-ttu-id="9e063-115">Dessa forma, todos os itens com essa chave serão coletados e processados em conjunto.</span><span class="sxs-lookup"><span data-stu-id="9e063-115">That way, all items with that key are collected and processed together.</span></span> 

## <a name="requirements"></a><span data-ttu-id="9e063-116">Requisitos</span><span class="sxs-lookup"><span data-stu-id="9e063-116">Requirements</span></span>

<span data-ttu-id="9e063-117">toofollow neste exemplo, você precisa dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="9e063-117">toofollow this example, you need these items:</span></span>

* <span data-ttu-id="9e063-118">Uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="9e063-118">An Azure subscription.</span></span> <span data-ttu-id="9e063-119">Se você não tiver uma assinatura, poderá [iniciar com uma conta gratuita do Azure](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="9e063-119">If you don't have a subscription, you can [start with a free Azure account](https://azure.microsoft.com/free/).</span></span> <span data-ttu-id="9e063-120">Caso contrário, você pode [inscrever-se para uma assinatura Pré-paga](https://azure.microsoft.com/pricing/purchase-options/).</span><span class="sxs-lookup"><span data-stu-id="9e063-120">Otherwise, you can [sign up for a Pay-As-You-Go subscription](https://azure.microsoft.com/pricing/purchase-options/).</span></span>

* <span data-ttu-id="9e063-121">Conhecimento básico sobre [como toocreate os aplicativos lógicos](../logic-apps/logic-apps-create-a-logic-app.md)</span><span class="sxs-lookup"><span data-stu-id="9e063-121">Basic knowledge about [how toocreate logic apps](../logic-apps/logic-apps-create-a-logic-app.md)</span></span> 

* <span data-ttu-id="9e063-122">Uma conta de email com qualquer [provedor de email com suporte do Aplicativo Lógico do Azure](../connectors/apis-list.md)</span><span class="sxs-lookup"><span data-stu-id="9e063-122">An email account with any [email provider supported by Azure Logic Apps](../connectors/apis-list.md)</span></span>

<a name="batch-receiver"></a>

## <a name="create-logic-apps-that-receive-messages-as-a-batch"></a><span data-ttu-id="9e063-123">Criar aplicativos lógicos que recebem mensagens como um lote</span><span class="sxs-lookup"><span data-stu-id="9e063-123">Create logic apps that receive messages as a batch</span></span>

<span data-ttu-id="9e063-124">Antes de enviar o lote de tooa de mensagens, você primeiro deve criar um aplicativo de lógica de "destinatário lote" com hello **lote** gatilho.</span><span class="sxs-lookup"><span data-stu-id="9e063-124">Before you can send messages tooa batch, you must first create a "batch receiver" logic app with hello **Batch** trigger.</span></span> <span data-ttu-id="9e063-125">Dessa forma, você pode selecionar este aplicativo de lógica do destinatário ao criar aplicativo de lógica de remetente hello.</span><span class="sxs-lookup"><span data-stu-id="9e063-125">That way, you can select this receiver logic app when you create hello sender logic app.</span></span> <span data-ttu-id="9e063-126">Para o receptor hello, você pode especificar nome do lote hello, critérios de liberação e outras configurações.</span><span class="sxs-lookup"><span data-stu-id="9e063-126">For hello receiver, you specify hello batch name, release criteria, and other settings.</span></span> 

<span data-ttu-id="9e063-127">Aplicativos de lógica de remetente precisam saber onde toosend itens, enquanto os aplicativos lógicos receptor não precisam tooknow nada sobre remetentes hello.</span><span class="sxs-lookup"><span data-stu-id="9e063-127">Sender logic apps need know where toosend items, while receiver logic apps don't need tooknow anything about hello senders.</span></span>

1. <span data-ttu-id="9e063-128">Em Olá [portal do Azure](https://portal.azure.com), crie um aplicativo de lógica com esse nome: "BatchReceiver"</span><span class="sxs-lookup"><span data-stu-id="9e063-128">In hello [Azure portal](https://portal.azure.com), create a logic app with this name: "BatchReceiver"</span></span> 

2. <span data-ttu-id="9e063-129">No Designer de aplicativos de lógica, adicionar Olá **lote** gatilho que inicia o fluxo de trabalho do aplicativo de lógica.</span><span class="sxs-lookup"><span data-stu-id="9e063-129">In Logic Apps Designer, add hello **Batch** trigger, which starts your logic app workflow.</span></span> <span data-ttu-id="9e063-130">Na caixa de pesquisa hello, digite "lote" como filtro.</span><span class="sxs-lookup"><span data-stu-id="9e063-130">In hello search box, enter "batch" as your filter.</span></span> <span data-ttu-id="9e063-131">Selecionar este gatilho: **Lote – Mensagens em lote**</span><span class="sxs-lookup"><span data-stu-id="9e063-131">Select this trigger: **Batch – Batch messages**</span></span>

   ![Adicionar o gatilho Lote](./media/logic-apps-batch-process-send-receive-messages/add-batch-receiver-trigger.png)

3. <span data-ttu-id="9e063-133">Forneça um nome para o lote hello e especificar critérios de liberação de lote hello, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="9e063-133">Provide a name for hello batch, and specify criteria for releasing hello batch, for example:</span></span>

   * <span data-ttu-id="9e063-134">**Nome do lote**: Olá nome usado tooidentify Olá lote, que é "TestBatch" neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="9e063-134">**Batch Name**: hello name used tooidentify hello batch, which is "TestBatch" in this example.</span></span>
   * <span data-ttu-id="9e063-135">**Contagem de mensagens**: Olá o número de mensagens toohold como um lote antes de liberar para processamento, o que é "5", neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="9e063-135">**Message Count**: hello number of messages toohold as a batch before releasing for processing, which is "5" in this example.</span></span>

   ![Fornecer detalhes sobre o gatilho Lote](./media/logic-apps-batch-process-send-receive-messages/receive-batch-trigger-details.png)

4. <span data-ttu-id="9e063-137">Adicione outra ação que envia um email quando Olá lote gatilho é acionado.</span><span class="sxs-lookup"><span data-stu-id="9e063-137">Add another action that sends an email when hello batch trigger fires.</span></span> <span data-ttu-id="9e063-138">Cada lote de saudação do tempo tiver cinco itens, Olá lógica aplicativo envia um email.</span><span class="sxs-lookup"><span data-stu-id="9e063-138">Each time hello batch has five items, hello logic app sends an email.</span></span>

   1. <span data-ttu-id="9e063-139">Em um gatilho de lote hello, escolha **+ nova etapa** > **adicionar uma ação**.</span><span class="sxs-lookup"><span data-stu-id="9e063-139">Under hello batch trigger, choose **+ New Step** > **Add an action**.</span></span>

   2. <span data-ttu-id="9e063-140">Na caixa de pesquisa hello, digite "email" como filtro.</span><span class="sxs-lookup"><span data-stu-id="9e063-140">In hello search box, enter "email" as your filter.</span></span>
   <span data-ttu-id="9e063-141">Com base em seu provedor de email, selecione um conector de email.</span><span class="sxs-lookup"><span data-stu-id="9e063-141">Based on your email provider, select an email connector.</span></span>
   
      <span data-ttu-id="9e063-142">Por exemplo, se você tiver uma conta corporativa ou de estudante, selecione Olá conector do Outlook do Office 365.</span><span class="sxs-lookup"><span data-stu-id="9e063-142">For example, if you have a work or school account, select hello Office 365 Outlook connector.</span></span> 
      <span data-ttu-id="9e063-143">Se você tiver uma conta do Gmail, selecione o conector do Gmail hello.</span><span class="sxs-lookup"><span data-stu-id="9e063-143">If you have a Gmail account, select hello Gmail connector.</span></span>

   3. <span data-ttu-id="9e063-144">Selecione essa ação para o conector:  **{*provedor de email*} – Enviar um email**</span><span class="sxs-lookup"><span data-stu-id="9e063-144">Select this action for your connector: **{*email provider*} - Send an email**</span></span>

      <span data-ttu-id="9e063-145">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="9e063-145">For example:</span></span>

      ![Selecione a ação "Enviar um email" para o seu provedor de email](./media/logic-apps-batch-process-send-receive-messages/add-send-email-action.png)

5. <span data-ttu-id="9e063-147">Se você não tiver criado uma conexão para o seu provedor de email, forneça suas credenciais de email para autenticação quando receber a solicitação.</span><span class="sxs-lookup"><span data-stu-id="9e063-147">If you didn't previously create a connection for your email provider, provide your email credentials for authentication when prompted.</span></span> <span data-ttu-id="9e063-148">Saiba mais sobre [como autenticar suas credenciais de email](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="9e063-148">Learn more about [authenticating your email credentials](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

6. <span data-ttu-id="9e063-149">Definir propriedades de saudação para ação Olá que você acabou de adicionar.</span><span class="sxs-lookup"><span data-stu-id="9e063-149">Set hello properties for hello action you just added.</span></span>

   * <span data-ttu-id="9e063-150">Em Olá **para** , digite o endereço de email do destinatário hello.</span><span class="sxs-lookup"><span data-stu-id="9e063-150">In hello **To** box, enter hello recipient's email address.</span></span> 
   <span data-ttu-id="9e063-151">Para fins de teste, você pode usar seu próprio endereço de email.</span><span class="sxs-lookup"><span data-stu-id="9e063-151">For testing purposes, you can use your own email address.</span></span>

   * <span data-ttu-id="9e063-152">Em Olá **assunto** caixa quando hello **conteúdo dinâmico** é exibida na lista, selecione Olá **nome da partição** campo.</span><span class="sxs-lookup"><span data-stu-id="9e063-152">In hello **Subject** box, when hello **Dynamic content** list appears, select hello **Partition Name** field.</span></span>

     ![Na lista de "Conteúdo dinâmico" Olá, selecione "Nome de partição"](./media/logic-apps-batch-process-send-receive-messages/send-email-action-details.png)

     <span data-ttu-id="9e063-154">Em uma seção posterior, você pode especificar uma chave de partição exclusivo que divide Olá lote de destino em lógica define toowhere, você pode enviar mensagens.</span><span class="sxs-lookup"><span data-stu-id="9e063-154">In a later section, you can specify a unique partition key that divides hello target batch into logical sets toowhere you can send messages.</span></span> 
     <span data-ttu-id="9e063-155">Cada conjunto tem um número exclusivo que é gerado pelo aplicativo de lógica de remetente hello.</span><span class="sxs-lookup"><span data-stu-id="9e063-155">Each set has a unique number that's generated by hello sender logic app.</span></span> 
     <span data-ttu-id="9e063-156">Esse recurso permite usar um único lote com várias subconjuntos e defina cada subconjunto com nome hello que você fornecer.</span><span class="sxs-lookup"><span data-stu-id="9e063-156">This capability lets you use a single batch with multiple subsets and define each subset with hello name that you provide.</span></span>

   * <span data-ttu-id="9e063-157">Em Olá **corpo** caixa quando hello **conteúdo dinâmico** é exibida na lista, selecione Olá **Id da mensagem** campo.</span><span class="sxs-lookup"><span data-stu-id="9e063-157">In hello **Body** box, when hello **Dynamic content** list appears, select hello **Message Id** field.</span></span>

     ![Para "Corpo", selecione "Id de Mensagem"](./media/logic-apps-batch-process-send-receive-messages/send-email-action-details-for-each.png)

     <span data-ttu-id="9e063-159">Como entrada Olá para ação de email de envio de saudação é uma matriz, designer de saudação adiciona automaticamente um **para cada** loop em torno de saudação **enviar um email** ação.</span><span class="sxs-lookup"><span data-stu-id="9e063-159">Because hello input for hello send email action is an array, hello designer automatically adds a **For each** loop around hello **Send an email** action.</span></span> 
     <span data-ttu-id="9e063-160">Esse loop age Olá interna em cada item no lote de saudação.</span><span class="sxs-lookup"><span data-stu-id="9e063-160">This loop performs hello inner action on each item in hello batch.</span></span> 
     <span data-ttu-id="9e063-161">Assim, com hello lote gatilho conjunto toofive itens, você tem cinco emails que cada gatilho de saudação do tempo é acionado.</span><span class="sxs-lookup"><span data-stu-id="9e063-161">So, with hello batch trigger set toofive items, you get five emails each time hello trigger fires.</span></span>

7.  <span data-ttu-id="9e063-162">Agora que você criou um aplicativo lógico destinatário do lote, salve-o.</span><span class="sxs-lookup"><span data-stu-id="9e063-162">Now that you created a batch receiver logic app, save your logic app.</span></span>

    ![Salve seu aplicativo lógico](./media/logic-apps-batch-process-send-receive-messages/save-batch-receiver-logic-app.png)

<a name="batch-sender"></a>

## <a name="create-logic-apps-that-send-messages-tooa-batch"></a><span data-ttu-id="9e063-164">Criar aplicativos lógicos que enviar mensagens tooa lote</span><span class="sxs-lookup"><span data-stu-id="9e063-164">Create logic apps that send messages tooa batch</span></span>

<span data-ttu-id="9e063-165">Agora, crie um ou mais aplicativos de lógica que enviar itens toohello lote definido pelo aplicativo de lógica de receptor de saudação.</span><span class="sxs-lookup"><span data-stu-id="9e063-165">Now create one or more logic apps that send items toohello batch defined by hello receiver logic app.</span></span> <span data-ttu-id="9e063-166">Para o remetente hello, você pode especificar Olá receptor lógica aplicativo e nome do lote, conteúdo da mensagem e outras configurações.</span><span class="sxs-lookup"><span data-stu-id="9e063-166">For hello sender, you specify hello receiver logic app and batch name, message content, and any other settings.</span></span> <span data-ttu-id="9e063-167">Opcionalmente, você pode fornecer um lote de saudação toodivide chave exclusiva de partição em itens de toocollect subconjuntos com essa chave.</span><span class="sxs-lookup"><span data-stu-id="9e063-167">You can optionally provide a unique partition key toodivide hello batch into subsets toocollect items with that key.</span></span>

<span data-ttu-id="9e063-168">Aplicativos de lógica de remetente precisam saber onde toosend itens, enquanto os aplicativos lógicos receptor não precisam tooknow nada sobre remetentes hello.</span><span class="sxs-lookup"><span data-stu-id="9e063-168">Sender logic apps need know where toosend items, while receiver logic apps don't need tooknow anything about hello senders.</span></span>

1. <span data-ttu-id="9e063-169">Crie outro aplicativo lógico com este nome: "RemetenteLote"</span><span class="sxs-lookup"><span data-stu-id="9e063-169">Create another logic app with this name: "BatchSender"</span></span>

   1. <span data-ttu-id="9e063-170">Na caixa de pesquisa hello, digite "recurrence" como filtro.</span><span class="sxs-lookup"><span data-stu-id="9e063-170">In hello search box, enter "recurrence" as your filter.</span></span> 
   <span data-ttu-id="9e063-171">Selecione este gatilho: **Agenda – Recorrência**</span><span class="sxs-lookup"><span data-stu-id="9e063-171">Select this trigger: **Schedule - Recurrence**</span></span>

      ![Adicionar gatilho hello "Agenda de recorrência"](./media/logic-apps-batch-process-send-receive-messages/add-schedule-trigger-batch-receiver.png)

   2. <span data-ttu-id="9e063-173">Definir Olá frequência e o aplicativo lógico de remetente de saudação do intervalo toorun a cada minuto.</span><span class="sxs-lookup"><span data-stu-id="9e063-173">Set hello frequency and interval toorun hello sender logic app every minute.</span></span>

      ![Defina a frequência e o intervalo do gatilho de recorrência](./media/logic-apps-batch-process-send-receive-messages/recurrence-trigger-batch-receiver-details.png)

2. <span data-ttu-id="9e063-175">Adicione uma nova etapa para enviar mensagens tooa lote.</span><span class="sxs-lookup"><span data-stu-id="9e063-175">Add a new step for sending messages tooa batch.</span></span>

   1. <span data-ttu-id="9e063-176">Em um gatilho de recorrência hello, escolha **+ nova etapa** > **adicionar uma ação**.</span><span class="sxs-lookup"><span data-stu-id="9e063-176">Under hello recurrence trigger, choose **+ New Step** > **Add an action**.</span></span>

   2. <span data-ttu-id="9e063-177">Na caixa de pesquisa hello, digite "lote" como filtro.</span><span class="sxs-lookup"><span data-stu-id="9e063-177">In hello search box, enter "batch" as your filter.</span></span> 

   3. <span data-ttu-id="9e063-178">Selecione esta ação: **enviar mensagens toobatch – escolha um fluxo de trabalho de aplicativos lógicos com o gatilho de lote**</span><span class="sxs-lookup"><span data-stu-id="9e063-178">Select this action: **Send messages toobatch – Choose a Logic Apps workflow with batch trigger**</span></span>

      ![Selecione "Enviar mensagens toobatch"](./media/logic-apps-batch-process-send-receive-messages/send-messages-batch-action.png)

   4. <span data-ttu-id="9e063-180">Agora, selecione seu aplicativo lógico "DestinatárioLote" que você criou anteriormente, e que agora aparece como uma ação.</span><span class="sxs-lookup"><span data-stu-id="9e063-180">Now select your "BatchReceiver" logic app that you previously created, which now appears as an action.</span></span>

      ![Selecione o aplicativo lógico "destinatário do lote"](./media/logic-apps-batch-process-send-receive-messages/send-batch-select-batch-receiver.png)

      > [!NOTE]
      > <span data-ttu-id="9e063-182">lista de saudação também mostra todos os outros aplicativos lógica que tenham um gatilho de lote.</span><span class="sxs-lookup"><span data-stu-id="9e063-182">hello list also shows any other logic apps that have batch triggers.</span></span>

3. <span data-ttu-id="9e063-183">Definir propriedades de lote de saudação.</span><span class="sxs-lookup"><span data-stu-id="9e063-183">Set hello batch properties.</span></span>

   * <span data-ttu-id="9e063-184">**Nome do lote**: nome do lote Olá definido pelo aplicativo lógico receptor hello, que é "TestBatch" neste exemplo e é validado no tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="9e063-184">**Batch Name**: hello batch name defined by hello receiver logic app, which is "TestBatch" in this example and is validated at runtime.</span></span>

     > [!IMPORTANT]
     > <span data-ttu-id="9e063-185">Certifique-se de que você não altere o nome do lote hello, que deve corresponder ao nome do lote Olá especificada pelo aplicativo de lógica de receptor de saudação.</span><span class="sxs-lookup"><span data-stu-id="9e063-185">Make sure that you don't change hello batch name, which must match hello batch name that's specified by hello receiver logic app.</span></span>
     > <span data-ttu-id="9e063-186">Alterar o nome hello lote faz com que remetente Olá lógica toofail de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="9e063-186">Changing hello batch name causes hello sender logic app toofail.</span></span>

   * <span data-ttu-id="9e063-187">**Conteúdo da mensagem**: Olá conteúdo da mensagem que você deseja toosend.</span><span class="sxs-lookup"><span data-stu-id="9e063-187">**Message Content**: hello message content that you want toosend.</span></span> 
   <span data-ttu-id="9e063-188">Neste exemplo, adicione essa expressão que inserções Olá data e hora atuais em mensagem de saudação do conteúdo que você enviar lote toohello:</span><span class="sxs-lookup"><span data-stu-id="9e063-188">For this example, add this expression that inserts hello current date and time into hello message content that you send toohello batch:</span></span>

     1. <span data-ttu-id="9e063-189">Olá quando **conteúdo dinâmico** lista é exibida, escolha **expressão**.</span><span class="sxs-lookup"><span data-stu-id="9e063-189">When hello **Dynamic content** list appears, choose **Expression**.</span></span> 
     2. <span data-ttu-id="9e063-190">Insira a expressão de saudação **utcnow()**e escolha **Okey**.</span><span class="sxs-lookup"><span data-stu-id="9e063-190">Enter hello expression **utcnow()**, and choose **OK**.</span></span> 

        ![Em "Conteúdo da Mensagem", escolha "Expressão".](./media/logic-apps-batch-process-send-receive-messages/send-batch-receiver-details.png)

4. <span data-ttu-id="9e063-193">Agora, configure uma partição para o lote de saudação.</span><span class="sxs-lookup"><span data-stu-id="9e063-193">Now set up a partition for hello batch.</span></span> <span data-ttu-id="9e063-194">No hello "BatchReceiver" ação, escolha **Mostrar opções avançadas**.</span><span class="sxs-lookup"><span data-stu-id="9e063-194">In hello "BatchReceiver" action, choose **Show advanced options**.</span></span>

   * <span data-ttu-id="9e063-195">**Nome da partição**: um toouse de chave de partição exclusivo opcional para a divisão do lote de destino hello.</span><span class="sxs-lookup"><span data-stu-id="9e063-195">**Partition Name**: An optional unique partition key toouse for dividing hello target batch.</span></span> <span data-ttu-id="9e063-196">Para este exemplo, adicione uma expressão que gera um número aleatório entre um e cinco.</span><span class="sxs-lookup"><span data-stu-id="9e063-196">For this example, add an expression that generates a random number between one and five.</span></span>
   
     1. <span data-ttu-id="9e063-197">Olá quando **conteúdo dinâmico** lista é exibida, escolha **expressão**.</span><span class="sxs-lookup"><span data-stu-id="9e063-197">When hello **Dynamic content** list appears, choose **Expression**.</span></span>
     2. <span data-ttu-id="9e063-198">Insira esta expressão: **rand(1,6)**</span><span class="sxs-lookup"><span data-stu-id="9e063-198">Enter this expression: **rand(1,6)**</span></span>

        ![Configurar uma partição para seu lote de destino](./media/logic-apps-batch-process-send-receive-messages/send-batch-receiver-partition-advanced-options.png)

        <span data-ttu-id="9e063-200">Essa função **rand** gera um número entre um e cinco.</span><span class="sxs-lookup"><span data-stu-id="9e063-200">This **rand** function generates a number between one and five.</span></span> 
        <span data-ttu-id="9e063-201">Portanto, você está dividindo esse lote em cinco partições numeradas, definidas dinamicamente por esta expressão.</span><span class="sxs-lookup"><span data-stu-id="9e063-201">So you are dividing this batch into five numbered partitions, which this expression dynamically sets.</span></span>

   * <span data-ttu-id="9e063-202">**Id da Mensagem**: um identificador de mensagem opcional, e um GUID gerado quando estiver vazio.</span><span class="sxs-lookup"><span data-stu-id="9e063-202">**Message Id**: An optional message identifier and is a generated GUID when empty.</span></span> 
   <span data-ttu-id="9e063-203">Neste exemplo, deixe essa caixa em branco.</span><span class="sxs-lookup"><span data-stu-id="9e063-203">For this example, leave this box blank.</span></span>

5. <span data-ttu-id="9e063-204">Salve seu aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="9e063-204">Save your logic app.</span></span> <span data-ttu-id="9e063-205">Seu aplicativo de lógica de remetente agora parece exemplo toothis semelhante:</span><span class="sxs-lookup"><span data-stu-id="9e063-205">Your sender logic app now looks similar toothis example:</span></span>

   ![Salve seu aplicativo lógico remetente](./media/logic-apps-batch-process-send-receive-messages/send-batch-receiver-details-finished.png)

## <a name="test-your-logic-apps"></a><span data-ttu-id="9e063-207">Testar seus aplicativos lógicos</span><span class="sxs-lookup"><span data-stu-id="9e063-207">Test your logic apps</span></span>

<span data-ttu-id="9e063-208">tootest o envio em lote solução, deixe a seus aplicativos lógicos em execução por alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="9e063-208">tootest your batching solution, leave your logic apps running for a few minutes.</span></span> <span data-ttu-id="9e063-209">Em breve, começar a receber emails em grupos de cinco, tudo com hello mesmo chave da partição.</span><span class="sxs-lookup"><span data-stu-id="9e063-209">Soon, you start getting emails in groups of five, all with hello same partition key.</span></span>

<span data-ttu-id="9e063-210">Seu aplicativo de lógica de BatchSender é executado a cada minuto, gera um número aleatório entre um e cinco e usa esse número gerado como chave de partição de saudação de lote de destino Olá onde as mensagens são enviadas.</span><span class="sxs-lookup"><span data-stu-id="9e063-210">Your BatchSender logic app runs every minute, generates a random number between one and five, and uses this generated number as hello partition key for hello target batch where messages are sent.</span></span> <span data-ttu-id="9e063-211">Cada vez lote Olá tem cinco itens com hello mesma chave de partição, seu aplicativo de lógica de BatchReceiver é acionado e envia mensagens para cada mensagem.</span><span class="sxs-lookup"><span data-stu-id="9e063-211">Each time hello batch has five items with hello same partition key, your BatchReceiver logic app fires and sends mail for each message.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9e063-212">Quando você terminar de teste, certifique-se de que você desative Olá BatchSender lógica aplicativo toostop enviar mensagens e evitar a sobrecarga de sua caixa de entrada.</span><span class="sxs-lookup"><span data-stu-id="9e063-212">When you're done testing, make sure that you disable hello BatchSender logic app toostop sending messages and avoid overloading your inbox.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9e063-213">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9e063-213">Next steps</span></span>

* [<span data-ttu-id="9e063-214">Compilar definições de aplicativo lógico usando JSON</span><span class="sxs-lookup"><span data-stu-id="9e063-214">Build on logic app definitions by using JSON</span></span>](../logic-apps/logic-apps-author-definitions.md)
* [<span data-ttu-id="9e063-215">Compilar um aplicativo sem servidor no Visual Studio com o Aplicativo Lógico do Azure e o Functions</span><span class="sxs-lookup"><span data-stu-id="9e063-215">Build a serverless app in Visual Studio with Azure Logic Apps and Functions</span></span>](../logic-apps/logic-apps-serverless-get-started-vs.md)
* [<span data-ttu-id="9e063-216">Tratamento de exceção e registro em log de erros para aplicativos lógicos</span><span class="sxs-lookup"><span data-stu-id="9e063-216">Exception handling and error logging for logic apps</span></span>](../logic-apps/logic-apps-scenario-error-and-exception-handling.md)
