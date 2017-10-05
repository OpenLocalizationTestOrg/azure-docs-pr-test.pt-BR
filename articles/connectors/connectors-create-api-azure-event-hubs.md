---
title: "Configurar o monitor de eventos com Hubs de Evento do Azure para Aplicativos Lógicos do Azure | Microsoft Docs"
description: "Monitorar fluxos de dados para receber eventos e enviar eventos para Aplicativos Lógicos do Azure com Hubs de Evento do Azure"
services: logic-apps
keywords: fluxo de dados, monitor de eventos, hubs de eventos
author: ecfan
manager: anneta
editor: 
documentationcenter: 
tags: connectors
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/31/2017
ms.author: estfan; LADocs
ms.openlocfilehash: 2ca27fb8269d1796fb1181fc4d0a8744a592d548
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-receive-and-send-events-with-the-event-hubs-connector"></a><span data-ttu-id="31c51-104">Monitorar, receber e enviar eventos com o conector do Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="31c51-104">Monitor, receive, and send events with the Event Hubs connector</span></span>

<span data-ttu-id="31c51-105">Para configurar um monitor de eventos para que seu aplicativo lógico possa detectar eventos, receber eventos e enviar eventos, conecte-se a um [Hub de Eventos do Azure](https://azure.microsoft.com/services/event-hubs) de seu aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="31c51-105">To set up an event monitor so that your logic app can detect events, receive events, and send events, connect to an [Azure Event Hub](https://azure.microsoft.com/services/event-hubs) from your logic app.</span></span> <span data-ttu-id="31c51-106">Saiba mais sobre [Hubs de Eventos do Azure](../event-hubs/event-hubs-what-is-event-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="31c51-106">Learn more about [Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md).</span></span>

## <a name="requirements"></a><span data-ttu-id="31c51-107">Requisitos</span><span class="sxs-lookup"><span data-stu-id="31c51-107">Requirements</span></span>

* <span data-ttu-id="31c51-108">Você precisa ter um [Namespace dos Hubs de Eventos e o Hub de Eventos](../event-hubs/event-hubs-create.md) no Azure.</span><span class="sxs-lookup"><span data-stu-id="31c51-108">You have to have an [Event Hubs namespace and Event Hub](../event-hubs/event-hubs-create.md) in Azure.</span></span> <span data-ttu-id="31c51-109">Saiba [como criar um namespace dos Hubs de Eventos e um Hub de Eventos](../event-hubs/event-hubs-create.md).</span><span class="sxs-lookup"><span data-stu-id="31c51-109">Learn [how to create an Event Hubs namespace and Event Hub](../event-hubs/event-hubs-create.md).</span></span> 

* <span data-ttu-id="31c51-110">Para usar [qualquer conector](https://docs.microsoft.com/azure/connectors/apis-list) em seu aplicativo lógico, você precisa criar primeiro um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="31c51-110">To use [any connector](https://docs.microsoft.com/azure/connectors/apis-list) in your logic app, you have to create a logic app first.</span></span> <span data-ttu-id="31c51-111">Saiba [como criar um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="31c51-111">Learn [how to create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

<a name="permissions-connection-string"></a>
## <a name="check-event-hubs-namespace-permissions-and-find-the-connection-string"></a><span data-ttu-id="31c51-112">Verifique as permissões de namespace dos Hubs de Eventos e encontre a cadeia de conexão</span><span class="sxs-lookup"><span data-stu-id="31c51-112">Check Event Hubs namespace permissions and find the connection string</span></span>

<span data-ttu-id="31c51-113">Para seu aplicativo lógico acessar qualquer serviço, você precisa criar uma [*conexão*](./connectors-overview.md) entre seu aplicativo lógico e o serviço, se você ainda não fez isso.</span><span class="sxs-lookup"><span data-stu-id="31c51-113">For your logic app to access any service, you have to create a [*connection*](./connectors-overview.md) between your logic app and the service, if you haven't already.</span></span> <span data-ttu-id="31c51-114">Essa conexão autoriza seu aplicativo lógico a acessar os dados.</span><span class="sxs-lookup"><span data-stu-id="31c51-114">This connection authorizes your logic app to access data.</span></span>
<span data-ttu-id="31c51-115">Para seu aplicativo lógico acessar o Hub de Eventos, você precisa ter permissões de **Gerenciamento** e a cadeia de conexão para seu namespace de Hubs de Eventos.</span><span class="sxs-lookup"><span data-stu-id="31c51-115">For your logic app to access your Event Hub, you have to have **Manage** permissions and the connection string for your Event Hubs namespace.</span></span>

<span data-ttu-id="31c51-116">Para verificar suas permissões e obter a cadeia de conexão, execute estas etapas.</span><span class="sxs-lookup"><span data-stu-id="31c51-116">To check your permissions and get the connection string, follow these steps.</span></span>

1.  <span data-ttu-id="31c51-117">Entre no [portal do Azure](https://portal.azure.com "portal do Azure").</span><span class="sxs-lookup"><span data-stu-id="31c51-117">Sign in to the [Azure portal](https://portal.azure.com "Azure portal").</span></span> 

2.  <span data-ttu-id="31c51-118">Acesse o *namespace* de seus Hubs de Evento, não o Hub de Eventos específico.</span><span class="sxs-lookup"><span data-stu-id="31c51-118">Go to your Event Hubs *namespace*, not the specific Event Hub.</span></span> <span data-ttu-id="31c51-119">Na folha do namespace, em **Configurações**, escolha **Políticas de acesso compartilhado**.</span><span class="sxs-lookup"><span data-stu-id="31c51-119">On the namespace blade, under **Settings**, choose **Shared access policies**.</span></span> <span data-ttu-id="31c51-120">Em **Declarações**, verifique se você tem permissões de **Gerenciamento** para esse namespace.</span><span class="sxs-lookup"><span data-stu-id="31c51-120">Under **Claims**, check that you have **Manage** permissions for that namespace.</span></span>

    ![Gerenciar permissões para seu namespace do Hub de Eventos](./media/connectors-create-api-azure-event-hubs/event-hubs-namespace.png)

3.  <span data-ttu-id="31c51-122">Para copiar a cadeia de conexão para o namespace de Hubs de Eventos, escolha **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="31c51-122">To copy the connection string for the Event Hubs namespace, choose **RootManageSharedAccessKey**.</span></span> <span data-ttu-id="31c51-123">Ao lado de sua cadeia de conexão de chave primária, escolha o botão de cópia.</span><span class="sxs-lookup"><span data-stu-id="31c51-123">Next to your primary key connection string, choose the copy button.</span></span>

    ![Copie a cadeia de conexão do namespace dos Hubs de Eventos](media/connectors-create-api-azure-event-hubs/find-event-hub-namespace-connection-string.png)

    > [!TIP]
    > <span data-ttu-id="31c51-125">Para confirmar se a cadeia de conexão está associada ao namespace dos seus Hubs de Eventos ou com um Hub de Eventos específico, verifique na cadeia de conexão o parâmetro `EntityPath`.</span><span class="sxs-lookup"><span data-stu-id="31c51-125">To confirm whether your connection string is associated with your Event Hubs namespace or with a specific Event Hub, check the connection string for the `EntityPath` parameter.</span></span> <span data-ttu-id="31c51-126">Se você encontrar esse parâmetro, a cadeia de conexão servirá para uma "entidade" de Hub de Eventos específica e não será a cadeia de caracteres correta a ser usada com seu aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="31c51-126">If you find this parameter, the connection string is for a specific Event Hub "entity", and is not the correct string to use with your logic app.</span></span>

4.  <span data-ttu-id="31c51-127">Agora, quando você receber uma solicitação por credenciais após a adição de um gatilho dos Hubs de Evento ou uma ação para o seu aplicativo lógico, você pode se conectar ao namespace de seus Hubs de Eventos.</span><span class="sxs-lookup"><span data-stu-id="31c51-127">Now when you're prompted for credentials after adding an Event Hubs trigger or action to your logic app, you can connect to your Event Hubs namespace.</span></span> <span data-ttu-id="31c51-128">Dê um nome à sua conexão, insira a cadeia de conexão que você copiou e escolha **Criar**.</span><span class="sxs-lookup"><span data-stu-id="31c51-128">Give your connection a name, enter the connection string that you copied, and choose **Create**.</span></span>

    ![Insira a cadeia de conexão para o namespace dos Hubs de Eventos](./media/connectors-create-api-azure-event-hubs/event-hubs-connection.png)

    <span data-ttu-id="31c51-130">Depois de criar a conexão, o nome da conexão deverá aparecer no gatilho ou ação dos Hubs de Evento.</span><span class="sxs-lookup"><span data-stu-id="31c51-130">After you create your connection, the connection name should appear in the Event Hubs trigger or action.</span></span> 
    <span data-ttu-id="31c51-131">Continue com as outras etapas em seu aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="31c51-131">You can then continue with the other steps in your logic app.</span></span>

    ![Conexão do namespace dos Hubs de Eventos criado](./media/connectors-create-api-azure-event-hubs/event-hubs-connection-created.png)

## <a name="start-workflow-when-your-event-hub-receives-new-events"></a><span data-ttu-id="31c51-133">Iniciar o fluxo de trabalho quando seu Hub de Eventos receber novos eventos</span><span class="sxs-lookup"><span data-stu-id="31c51-133">Start workflow when your Event Hub receives new events</span></span>

<span data-ttu-id="31c51-134">Um [*gatilho*](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) é um evento que inicia um fluxo de trabalho em seu aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="31c51-134">A [*trigger*](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) is an event that starts a workflow in your logic app.</span></span> <span data-ttu-id="31c51-135">Para iniciar um fluxo de trabalho quando novos eventos forem enviados ao seu Hub de Eventos, execute estas etapas para adicionar o gatilho que detecta esse evento.</span><span class="sxs-lookup"><span data-stu-id="31c51-135">To start a workflow when new events are sent to your Event Hub, follow these steps for adding the trigger that detects this event.</span></span>

1.  <span data-ttu-id="31c51-136">No [portal do Azure](https://portal.azure.com "portal do Azure"), acesse seu aplicativo lógico existente ou crie um aplicativo lógico em branco.</span><span class="sxs-lookup"><span data-stu-id="31c51-136">In the [Azure portal](https://portal.azure.com "Azure portal"), go to your existing logic app or create a blank logic app.</span></span>

2.  <span data-ttu-id="31c51-137">Na caixa de pesquisa do Designer de Aplicativo Lógico, insira `event hubs` para o seu filtro.</span><span class="sxs-lookup"><span data-stu-id="31c51-137">In the search box for the Logic App Designer, enter `event hubs` for your filter.</span></span> <span data-ttu-id="31c51-138">Selecione esse gatilho: **quando os eventos estiverem disponíveis no Hub de Eventos**</span><span class="sxs-lookup"><span data-stu-id="31c51-138">Select this trigger: **When events are available in Event Hub**</span></span>

    ![Selecionar o gatilho quando seu Hub de Eventos receber novos eventos](./media/connectors-create-api-azure-event-hubs/find-event-hubs-trigger.png)

    <span data-ttu-id="31c51-140">Se você ainda não tiver uma conexão para o namespace de seus Hubs de Eventos, receberá uma solicitação para criar essa conexão.</span><span class="sxs-lookup"><span data-stu-id="31c51-140">If you don't already have a connection to your Event Hubs namespace, you're prompted to create this connection now.</span></span> <span data-ttu-id="31c51-141">Dê um nome à sua conexão e insira a cadeia de conexão para seu namespace de Hubs de Eventos.</span><span class="sxs-lookup"><span data-stu-id="31c51-141">Give your connection a name, and enter the connection string for your Event Hubs namespace.</span></span> 
    <span data-ttu-id="31c51-142">Se for necessário, saiba [como localizar a cadeia de conexão](#permissions-connection-string).</span><span class="sxs-lookup"><span data-stu-id="31c51-142">If necessary, learn [how to find your connection string](#permissions-connection-string).</span></span>

    ![Insira a cadeia de conexão para o namespace dos Hubs de Eventos](./media/connectors-create-api-azure-event-hubs/event-hubs-connection.png)

    <span data-ttu-id="31c51-144">Depois de criar a conexão, as configurações para o gatilho **Quando um evento estiver disponível em um Hub de Eventos** aparecer.</span><span class="sxs-lookup"><span data-stu-id="31c51-144">After you create the connection, the settings for the **When an event in available in an Event Hub** trigger appear.</span></span>

    ![Configurações do gatilho quando seu Hub de Eventos receber novos eventos](./media/connectors-create-api-azure-event-hubs/event-hubs-trigger.png)

3.  <span data-ttu-id="31c51-146">Insira ou selecione o nome do Hub de Eventos que você deseja monitorar.</span><span class="sxs-lookup"><span data-stu-id="31c51-146">Enter or select the name for the Event Hub that you want to monitor.</span></span> <span data-ttu-id="31c51-147">Selecione a frequência e o intervalo da frequência com que você deseja verificar o Hub de Eventos.</span><span class="sxs-lookup"><span data-stu-id="31c51-147">Select the frequency and interval for how often you want to check the Event Hub.</span></span>

    > [!TIP]
    > <span data-ttu-id="31c51-148">Para selecionar, opcionalmente, um grupo de consumidores para ler eventos, escolha **Mostrar opções avançadas**.</span><span class="sxs-lookup"><span data-stu-id="31c51-148">To optionally select a consumer group for reading events, choose **Show advanced options**.</span></span> 

    ![Especifique o Hub de Evento ou grupo de consumidores](./media/connectors-create-api-azure-event-hubs/event-hubs-trigger-details.png)

    <span data-ttu-id="31c51-150">Agora, você definiu um gatilho para iniciar um fluxo de trabalho para seu aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="31c51-150">You've now set up a trigger to start a workflow for your logic app.</span></span> 
    <span data-ttu-id="31c51-151">Seu aplicativo lógico verifica o Hub de Eventos especificado com base no agendamento definido.</span><span class="sxs-lookup"><span data-stu-id="31c51-151">Your logic app checks the specified Event Hub based on the schedule that you set.</span></span> 
    <span data-ttu-id="31c51-152">Se o seu aplicativo encontrar novos eventos no Hub de Eventos, o gatilho executará outras ações ou gatilhos em seu aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="31c51-152">If your app finds new events in the Event Hub, the trigger runs other actions or triggers in your logic app.</span></span>

## <a name="send-events-to-your-event-hub-from-your-logic-app"></a><span data-ttu-id="31c51-153">Enviar eventos para seu Hub de Eventos de seu aplicativo lógico</span><span class="sxs-lookup"><span data-stu-id="31c51-153">Send events to your Event Hub from your logic app</span></span>

<span data-ttu-id="31c51-154">Uma [*ação*](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) é uma tarefa executada pelo fluxo de trabalho do aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="31c51-154">An [*action*](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) is a task performed by your logic app workflow.</span></span> <span data-ttu-id="31c51-155">Depois de adicionar um gatilho ao seu aplicativo lógico, você poderá adicionar uma ação para executar operações com os dados gerados por esse gatilho.</span><span class="sxs-lookup"><span data-stu-id="31c51-155">After you add a trigger to your logic app, you can add an action to perform operations with data generated by that trigger.</span></span> <span data-ttu-id="31c51-156">Para enviar um evento para seu Hub de Eventos de seu aplicativo lógico, execute estas etapas.</span><span class="sxs-lookup"><span data-stu-id="31c51-156">To send an event to your Event Hub from your logic app, follow these steps.</span></span>

1.  <span data-ttu-id="31c51-157">No Designer de Aplicativo Lógico, no gatilho de seu aplicativo lógico, escolha **Nova etapa** > **Adicionar uma ação**.</span><span class="sxs-lookup"><span data-stu-id="31c51-157">In Logic App Designer, under your logic app trigger, choose **New step** > **Add an action**.</span></span>

    ![Escolha "Nova etapa", em seguida, "Adicionar uma ação"](./media/connectors-create-api-azure-event-hubs/add-action.png)

    <span data-ttu-id="31c51-159">Agora você pode localizar e selecionar uma ação para execução.</span><span class="sxs-lookup"><span data-stu-id="31c51-159">Now you can find and select an action to perform.</span></span> 
    <span data-ttu-id="31c51-160">Embora você possa selecionar qualquer ação, neste exemplo, queremos que a ação Hubs de Eventos envie eventos.</span><span class="sxs-lookup"><span data-stu-id="31c51-160">Although you can select any action, for this example, we want the Event Hubs action to send events.</span></span>

2.  <span data-ttu-id="31c51-161">Na caixa de pesquisa, digite `event hubs` como seu filtro.</span><span class="sxs-lookup"><span data-stu-id="31c51-161">In the search box, enter `event hubs` for your filter.</span></span>
<span data-ttu-id="31c51-162">Selecione esta ação: **Enviar evento**</span><span class="sxs-lookup"><span data-stu-id="31c51-162">Select this action: **Send event**</span></span>

    ![Selecione a ação "Hubs de eventos - Enviar evento"](./media/connectors-create-api-azure-event-hubs/find-event-hubs-action.png)

3.  <span data-ttu-id="31c51-164">Insira os detalhes necessários para o evento, como o nome do Hub de Eventos no qual você deseja enviar o evento.</span><span class="sxs-lookup"><span data-stu-id="31c51-164">Enter the required details for the event, such as the name for the Event Hub where you want to send the event.</span></span> <span data-ttu-id="31c51-165">Insira outros detalhes opcionais sobre o evento, como o conteúdo desse evento.</span><span class="sxs-lookup"><span data-stu-id="31c51-165">Enter any other optional details about the event, such as content for that event.</span></span>

    > [!TIP]
    > <span data-ttu-id="31c51-166">Para especificar, opcionalmente, a partição do Hub de Eventos para onde enviar o evento, escolha **Mostrar opções avançadas de**.</span><span class="sxs-lookup"><span data-stu-id="31c51-166">To optionally specify the Event Hub partition where to send the event, choose **Show advanced options**.</span></span> 

    ![Insira o nome do Hub de Eventos e detalhes opcionais do evento](./media/connectors-create-api-azure-event-hubs/event-hubs-send-event-action.png)

6.  <span data-ttu-id="31c51-168">Salve suas alterações.</span><span class="sxs-lookup"><span data-stu-id="31c51-168">Save your changes.</span></span>

    ![Salve seu aplicativo lógico](./media/connectors-create-api-azure-event-hubs/save-logic-app.png)

    <span data-ttu-id="31c51-170">Agora você configurou uma ação para enviar eventos de seu aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="31c51-170">You've now set up an action to send events from your logic app.</span></span> 

## <a name="connector-specific-details"></a><span data-ttu-id="31c51-171">Detalhes específicos do conector</span><span class="sxs-lookup"><span data-stu-id="31c51-171">Connector-specific details</span></span>

<span data-ttu-id="31c51-172">Veja os gatilhos e ações definidos no swagger e também os limites nos [detalhes do conector](/connectors/eventhubs/).</span><span class="sxs-lookup"><span data-stu-id="31c51-172">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/eventhubs/).</span></span> 

## <a name="get-help"></a><span data-ttu-id="31c51-173">Obter ajuda</span><span class="sxs-lookup"><span data-stu-id="31c51-173">Get help</span></span>

<span data-ttu-id="31c51-174">Para fazer perguntas, responder a perguntas e saber o que os outros usuários dos Aplicativos Lógicos do Azure estão fazendo, visite o [fórum de Aplicativos Lógicos do Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="31c51-174">To ask questions, answer questions, and see what other Azure Logic Apps users are doing, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="31c51-175">Para ajudar a melhorar os Aplicativos Lógicos e conectores, vote ou envie ideias no [site de comentários do usuário dos Aplicativos Lógicos](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="31c51-175">To help improve Logic Apps and connectors, vote on or submit ideas at the [Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="31c51-176">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="31c51-176">Next steps</span></span>

*  [<span data-ttu-id="31c51-177">Encontrar outros conectores de Aplicativos Lógicos do Azure</span><span class="sxs-lookup"><span data-stu-id="31c51-177">Find other connectors for Azure Logic apps</span></span>](./apis-list.md)