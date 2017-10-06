---
title: "aaaSet o monitor de eventos com Hubs de eventos do Azure para os aplicativos lógicos do Azure | Microsoft Docs"
description: "Monitorar eventos de tooreceive de fluxos de dados e enviar eventos para os aplicativos lógicos do Azure com Hubs de eventos do Azure"
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
ms.openlocfilehash: 4aad2c2ac1134b4d4d440019b4773559e49be122
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-receive-and-send-events-with-hello-event-hubs-connector"></a><span data-ttu-id="d019b-104">Monitorar, receber e enviar eventos com o conector de Hubs de eventos Olá</span><span class="sxs-lookup"><span data-stu-id="d019b-104">Monitor, receive, and send events with hello Event Hubs connector</span></span>

<span data-ttu-id="d019b-105">tooset backup de um monitor de eventos para que seu aplicativo lógico pode detectar eventos, receber eventos e enviar eventos, conecte-se tooan [Hub de eventos do Azure](https://azure.microsoft.com/services/event-hubs) do seu aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="d019b-105">tooset up an event monitor so that your logic app can detect events, receive events, and send events, connect tooan [Azure Event Hub](https://azure.microsoft.com/services/event-hubs) from your logic app.</span></span> <span data-ttu-id="d019b-106">Saiba mais sobre [Hubs de Eventos do Azure](../event-hubs/event-hubs-what-is-event-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="d019b-106">Learn more about [Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md).</span></span>

## <a name="requirements"></a><span data-ttu-id="d019b-107">Requisitos</span><span class="sxs-lookup"><span data-stu-id="d019b-107">Requirements</span></span>

* <span data-ttu-id="d019b-108">Você tem toohave um [namespace de Hubs de eventos e Hub de eventos](../event-hubs/event-hubs-create.md) no Azure.</span><span class="sxs-lookup"><span data-stu-id="d019b-108">You have toohave an [Event Hubs namespace and Event Hub](../event-hubs/event-hubs-create.md) in Azure.</span></span> <span data-ttu-id="d019b-109">Saiba [como toocreate um namespace de Hubs de eventos e o Hub de eventos](../event-hubs/event-hubs-create.md).</span><span class="sxs-lookup"><span data-stu-id="d019b-109">Learn [how toocreate an Event Hubs namespace and Event Hub](../event-hubs/event-hubs-create.md).</span></span> 

* <span data-ttu-id="d019b-110">toouse [qualquer conector](https://docs.microsoft.com/azure/connectors/apis-list) em seu aplicativo lógico, você tem toocreate um lógica de aplicativo pela primeira vez.</span><span class="sxs-lookup"><span data-stu-id="d019b-110">toouse [any connector](https://docs.microsoft.com/azure/connectors/apis-list) in your logic app, you have toocreate a logic app first.</span></span> <span data-ttu-id="d019b-111">Saiba [como um aplicativo de lógica de toocreate](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="d019b-111">Learn [how toocreate a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

<a name="permissions-connection-string"></a>
## <a name="check-event-hubs-namespace-permissions-and-find-hello-connection-string"></a><span data-ttu-id="d019b-112">Verifique as permissões de namespace de Hubs de eventos e localizar a cadeia de caracteres de conexão Olá</span><span class="sxs-lookup"><span data-stu-id="d019b-112">Check Event Hubs namespace permissions and find hello connection string</span></span>

<span data-ttu-id="d019b-113">Para tooaccess de aplicativo sua lógica de qualquer serviço, você tem toocreate um [ *conexão* ](./connectors-overview.md) entre sua lógica aplicativo hello serviço e, se ainda não o fez.</span><span class="sxs-lookup"><span data-stu-id="d019b-113">For your logic app tooaccess any service, you have toocreate a [*connection*](./connectors-overview.md) between your logic app and hello service, if you haven't already.</span></span> <span data-ttu-id="d019b-114">Essa conexão autoriza seus dados de tooaccess lógica do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d019b-114">This connection authorizes your logic app tooaccess data.</span></span>
<span data-ttu-id="d019b-115">Para sua tooaccess de aplicativo lógica seu Hub de eventos, você tem toohave **gerenciar** permissões e a cadeia de caracteres de conexão de saudação para seu namespace de Hubs de eventos.</span><span class="sxs-lookup"><span data-stu-id="d019b-115">For your logic app tooaccess your Event Hub, you have toohave **Manage** permissions and hello connection string for your Event Hubs namespace.</span></span>

<span data-ttu-id="d019b-116">toocheck as permissões e a cadeia de conexão do get hello, siga estas etapas.</span><span class="sxs-lookup"><span data-stu-id="d019b-116">toocheck your permissions and get hello connection string, follow these steps.</span></span>

1.  <span data-ttu-id="d019b-117">Entrar toohello [portal do Azure](https://portal.azure.com "portal do Azure").</span><span class="sxs-lookup"><span data-stu-id="d019b-117">Sign in toohello [Azure portal](https://portal.azure.com "Azure portal").</span></span> 

2.  <span data-ttu-id="d019b-118">Vá Hubs de eventos tooyour *namespace*, não Olá Hub de eventos específico.</span><span class="sxs-lookup"><span data-stu-id="d019b-118">Go tooyour Event Hubs *namespace*, not hello specific Event Hub.</span></span> <span data-ttu-id="d019b-119">Na folha de namespace hello, em **configurações**, escolha **políticas de acesso compartilhado**.</span><span class="sxs-lookup"><span data-stu-id="d019b-119">On hello namespace blade, under **Settings**, choose **Shared access policies**.</span></span> <span data-ttu-id="d019b-120">Em **Declarações**, verifique se você tem permissões de **Gerenciamento** para esse namespace.</span><span class="sxs-lookup"><span data-stu-id="d019b-120">Under **Claims**, check that you have **Manage** permissions for that namespace.</span></span>

    ![Gerenciar permissões para seu namespace do Hub de Eventos](./media/connectors-create-api-azure-event-hubs/event-hubs-namespace.png)

3.  <span data-ttu-id="d019b-122">cadeia de conexão toocopy Olá para o namespace de Hubs de eventos hello, escolha **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="d019b-122">toocopy hello connection string for hello Event Hubs namespace, choose **RootManageSharedAccessKey**.</span></span> <span data-ttu-id="d019b-123">Tooyour próxima primária chave de cadeia de caracteres de conexão, escolha o botão de cópia de saudação.</span><span class="sxs-lookup"><span data-stu-id="d019b-123">Next tooyour primary key connection string, choose hello copy button.</span></span>

    ![Copie a cadeia de conexão do namespace dos Hubs de Eventos](media/connectors-create-api-azure-event-hubs/find-event-hub-namespace-connection-string.png)

    > [!TIP]
    > <span data-ttu-id="d019b-125">tooconfirm se a cadeia de conexão está associada com seu namespace de Hubs de eventos ou com um Hub de eventos específico, verifique cadeia de caracteres de conexão de saudação de saudação `EntityPath` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="d019b-125">tooconfirm whether your connection string is associated with your Event Hubs namespace or with a specific Event Hub, check hello connection string for hello `EntityPath` parameter.</span></span> <span data-ttu-id="d019b-126">Se você encontrar esse parâmetro, cadeia de caracteres de conexão de saudação é para um Hub de eventos específico "entidade" e não é Olá toouse de cadeia de caracteres correto com seu aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="d019b-126">If you find this parameter, hello connection string is for a specific Event Hub "entity", and is not hello correct string toouse with your logic app.</span></span>

4.  <span data-ttu-id="d019b-127">Agora, quando você for solicitado a fornecer credenciais depois de adicionar um aplicativo Hubs de eventos do gatilho ou ação tooyour lógica, você pode conectar tooyour namespace de Hubs de eventos.</span><span class="sxs-lookup"><span data-stu-id="d019b-127">Now when you're prompted for credentials after adding an Event Hubs trigger or action tooyour logic app, you can connect tooyour Event Hubs namespace.</span></span> <span data-ttu-id="d019b-128">Dê um nome de sua conexão, digite a cadeia de caracteres de conexão de saudação que você copiou e escolha **criar**.</span><span class="sxs-lookup"><span data-stu-id="d019b-128">Give your connection a name, enter hello connection string that you copied, and choose **Create**.</span></span>

    ![Insira a cadeia de conexão para o namespace dos Hubs de Eventos](./media/connectors-create-api-azure-event-hubs/event-hubs-connection.png)

    <span data-ttu-id="d019b-130">Depois de criar sua conexão, o nome de conexão de saudação deve aparecer em Olá gatilho de Hubs de evento ou ação.</span><span class="sxs-lookup"><span data-stu-id="d019b-130">After you create your connection, hello connection name should appear in hello Event Hubs trigger or action.</span></span> 
    <span data-ttu-id="d019b-131">Você pode continuar com hello outras etapas em seu aplicativo de lógica.</span><span class="sxs-lookup"><span data-stu-id="d019b-131">You can then continue with hello other steps in your logic app.</span></span>

    ![Conexão do namespace dos Hubs de Eventos criado](./media/connectors-create-api-azure-event-hubs/event-hubs-connection-created.png)

## <a name="start-workflow-when-your-event-hub-receives-new-events"></a><span data-ttu-id="d019b-133">Iniciar o fluxo de trabalho quando seu Hub de Eventos receber novos eventos</span><span class="sxs-lookup"><span data-stu-id="d019b-133">Start workflow when your Event Hub receives new events</span></span>

<span data-ttu-id="d019b-134">Um [*gatilho*](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) é um evento que inicia um fluxo de trabalho em seu aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="d019b-134">A [*trigger*](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) is an event that starts a workflow in your logic app.</span></span> <span data-ttu-id="d019b-135">Para iniciar um fluxo de trabalho quando novos eventos são enviados tooyour Hub de eventos, siga estas etapas para adicionar o gatilho Olá que detecta esse evento.</span><span class="sxs-lookup"><span data-stu-id="d019b-135">To start a workflow when new events are sent tooyour Event Hub, follow these steps for adding hello trigger that detects this event.</span></span>

1.  <span data-ttu-id="d019b-136">Em Olá [portal do Azure](https://portal.azure.com "portal do Azure"), vá tooyour aplicativo de lógica existente ou criar um aplicativo em branco lógica.</span><span class="sxs-lookup"><span data-stu-id="d019b-136">In hello [Azure portal](https://portal.azure.com "Azure portal"), go tooyour existing logic app or create a blank logic app.</span></span>

2.  <span data-ttu-id="d019b-137">Na caixa de pesquisa Olá Olá Designer de lógica do aplicativo, insira `event hubs` para seu filtro.</span><span class="sxs-lookup"><span data-stu-id="d019b-137">In hello search box for hello Logic App Designer, enter `event hubs` for your filter.</span></span> <span data-ttu-id="d019b-138">Selecione esse gatilho: **quando os eventos estiverem disponíveis no Hub de Eventos**</span><span class="sxs-lookup"><span data-stu-id="d019b-138">Select this trigger: **When events are available in Event Hub**</span></span>

    ![Selecionar o gatilho quando seu Hub de Eventos receber novos eventos](./media/connectors-create-api-azure-event-hubs/find-event-hubs-trigger.png)

    <span data-ttu-id="d019b-140">Se você ainda não tiver um namespace de Hubs de eventos de tooyour de conexão, será solicitado que você toocreate agora essa conexão.</span><span class="sxs-lookup"><span data-stu-id="d019b-140">If you don't already have a connection tooyour Event Hubs namespace, you're prompted toocreate this connection now.</span></span> <span data-ttu-id="d019b-141">Dê um nome de sua conexão e insira a cadeia de caracteres de conexão de saudação para seu namespace de Hubs de eventos.</span><span class="sxs-lookup"><span data-stu-id="d019b-141">Give your connection a name, and enter hello connection string for your Event Hubs namespace.</span></span> 
    <span data-ttu-id="d019b-142">Se necessário, saiba [como toofind sua cadeia de caracteres de conexão](#permissions-connection-string).</span><span class="sxs-lookup"><span data-stu-id="d019b-142">If necessary, learn [how toofind your connection string](#permissions-connection-string).</span></span>

    ![Insira a cadeia de conexão para o namespace dos Hubs de Eventos](./media/connectors-create-api-azure-event-hubs/event-hubs-connection.png)

    <span data-ttu-id="d019b-144">Depois de criar conexão hello, Olá configurações para Olá **quando um evento em disponíveis em um Hub de eventos** gatilho aparecem.</span><span class="sxs-lookup"><span data-stu-id="d019b-144">After you create hello connection, hello settings for hello **When an event in available in an Event Hub** trigger appear.</span></span>

    ![Configurações do gatilho quando seu Hub de Eventos receber novos eventos](./media/connectors-create-api-azure-event-hubs/event-hubs-trigger.png)

3.  <span data-ttu-id="d019b-146">Insira ou selecione o nome Olá Olá Hub de eventos que você deseja toomonitor.</span><span class="sxs-lookup"><span data-stu-id="d019b-146">Enter or select hello name for hello Event Hub that you want toomonitor.</span></span> <span data-ttu-id="d019b-147">Selecione a frequência de saudação e intervalo de frequência você deseja toocheck Olá Hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="d019b-147">Select hello frequency and interval for how often you want toocheck hello Event Hub.</span></span>

    > [!TIP]
    > <span data-ttu-id="d019b-148">toooptionally selecionar um grupo de consumidores para ler eventos, escolha **Mostrar opções avançadas**.</span><span class="sxs-lookup"><span data-stu-id="d019b-148">toooptionally select a consumer group for reading events, choose **Show advanced options**.</span></span> 

    ![Especifique o Hub de Evento ou grupo de consumidores](./media/connectors-create-api-azure-event-hubs/event-hubs-trigger-details.png)

    <span data-ttu-id="d019b-150">Você agora configurou um gatilho toostart um fluxo de trabalho para seu aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="d019b-150">You've now set up a trigger toostart a workflow for your logic app.</span></span> 
    <span data-ttu-id="d019b-151">Seu aplicativo lógica verifica Olá especificado Hub de eventos com base em agendamento Olá que você definir.</span><span class="sxs-lookup"><span data-stu-id="d019b-151">Your logic app checks hello specified Event Hub based on hello schedule that you set.</span></span> 
    <span data-ttu-id="d019b-152">Se seu aplicativo encontrar novos eventos no hello Hub de eventos, o gatilho Olá executa outras ações ou disparadores em seu aplicativo de lógica.</span><span class="sxs-lookup"><span data-stu-id="d019b-152">If your app finds new events in hello Event Hub, hello trigger runs other actions or triggers in your logic app.</span></span>

## <a name="send-events-tooyour-event-hub-from-your-logic-app"></a><span data-ttu-id="d019b-153">Enviar eventos tooyour Hub de eventos do aplicativo lógica</span><span class="sxs-lookup"><span data-stu-id="d019b-153">Send events tooyour Event Hub from your logic app</span></span>

<span data-ttu-id="d019b-154">Uma [*ação*](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) é uma tarefa executada pelo fluxo de trabalho do aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="d019b-154">An [*action*](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts) is a task performed by your logic app workflow.</span></span> <span data-ttu-id="d019b-155">Depois de adicionar um aplicativo de lógica do gatilho tooyour, você pode adicionar operações de tooperform uma ação com dados gerados por que o disparador.</span><span class="sxs-lookup"><span data-stu-id="d019b-155">After you add a trigger tooyour logic app, you can add an action tooperform operations with data generated by that trigger.</span></span> <span data-ttu-id="d019b-156">toosend um tooyour evento Hub de eventos do seu aplicativo lógico, siga estas etapas.</span><span class="sxs-lookup"><span data-stu-id="d019b-156">toosend an event tooyour Event Hub from your logic app, follow these steps.</span></span>

1.  <span data-ttu-id="d019b-157">No Designer de Aplicativo Lógico, no gatilho de seu aplicativo lógico, escolha **Nova etapa** > **Adicionar uma ação**.</span><span class="sxs-lookup"><span data-stu-id="d019b-157">In Logic App Designer, under your logic app trigger, choose **New step** > **Add an action**.</span></span>

    ![Escolha "Nova etapa", em seguida, "Adicionar uma ação"](./media/connectors-create-api-azure-event-hubs/add-action.png)

    <span data-ttu-id="d019b-159">Agora você pode localizar e selecionar uma ação tooperform.</span><span class="sxs-lookup"><span data-stu-id="d019b-159">Now you can find and select an action tooperform.</span></span> 
    <span data-ttu-id="d019b-160">Embora você possa selecionar qualquer ação, neste exemplo, queremos que eventos de toosend de ação do hello Hubs de eventos.</span><span class="sxs-lookup"><span data-stu-id="d019b-160">Although you can select any action, for this example, we want hello Event Hubs action toosend events.</span></span>

2.  <span data-ttu-id="d019b-161">Na caixa de pesquisa hello, digite `event hubs` para seu filtro.</span><span class="sxs-lookup"><span data-stu-id="d019b-161">In hello search box, enter `event hubs` for your filter.</span></span>
<span data-ttu-id="d019b-162">Selecione esta ação: **Enviar evento**</span><span class="sxs-lookup"><span data-stu-id="d019b-162">Select this action: **Send event**</span></span>

    ![Selecione a ação "Hubs de eventos - Enviar evento"](./media/connectors-create-api-azure-event-hubs/find-event-hubs-action.png)

3.  <span data-ttu-id="d019b-164">Insira os detalhes de saudação necessária para evento hello, como nome Olá Olá Hub de eventos onde você deseja que o evento de saudação toosend.</span><span class="sxs-lookup"><span data-stu-id="d019b-164">Enter hello required details for hello event, such as hello name for hello Event Hub where you want toosend hello event.</span></span> <span data-ttu-id="d019b-165">Insira os detalhes opcionais sobre o evento hello, como conteúdo para o evento.</span><span class="sxs-lookup"><span data-stu-id="d019b-165">Enter any other optional details about hello event, such as content for that event.</span></span>

    > [!TIP]
    > <span data-ttu-id="d019b-166">toooptionally especificar a partição do Hub de eventos Olá onde toosend Olá eventos, escolha **Mostrar opções avançadas**.</span><span class="sxs-lookup"><span data-stu-id="d019b-166">toooptionally specify hello Event Hub partition where toosend hello event, choose **Show advanced options**.</span></span> 

    ![Insira o nome do Hub de Eventos e detalhes opcionais do evento](./media/connectors-create-api-azure-event-hubs/event-hubs-send-event-action.png)

6.  <span data-ttu-id="d019b-168">Salve suas alterações.</span><span class="sxs-lookup"><span data-stu-id="d019b-168">Save your changes.</span></span>

    ![Salve seu aplicativo lógico](./media/connectors-create-api-azure-event-hubs/save-logic-app.png)

    <span data-ttu-id="d019b-170">Você configurou agora um toosend de eventos de ação de seu aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="d019b-170">You've now set up an action toosend events from your logic app.</span></span> 

## <a name="connector-specific-details"></a><span data-ttu-id="d019b-171">Detalhes específicos do conector</span><span class="sxs-lookup"><span data-stu-id="d019b-171">Connector-specific details</span></span>

<span data-ttu-id="d019b-172">Exibir quaisquer gatilhos e ações definidas em swagger Olá e também os limites de saudação [detalhes conector](/connectors/eventhubs/).</span><span class="sxs-lookup"><span data-stu-id="d019b-172">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/eventhubs/).</span></span> 

## <a name="get-help"></a><span data-ttu-id="d019b-173">Obter ajuda</span><span class="sxs-lookup"><span data-stu-id="d019b-173">Get help</span></span>

<span data-ttu-id="d019b-174">tooask perguntas, responder a perguntas e veja que outros usuários de aplicativos do Azure lógicos estão fazendo, visite Olá [Fórum de aplicativos do Azure lógica](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="d019b-174">tooask questions, answer questions, and see what other Azure Logic Apps users are doing, visit hello [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="d019b-175">toohelp melhorar a lógica de aplicativos e conectores, votar ou enviar ideias em Olá [site de comentários do usuário de aplicativos lógicos](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="d019b-175">toohelp improve Logic Apps and connectors, vote on or submit ideas at hello [Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d019b-176">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d019b-176">Next steps</span></span>

*  [<span data-ttu-id="d019b-177">Encontrar outros conectores de Aplicativos Lógicos do Azure</span><span class="sxs-lookup"><span data-stu-id="d019b-177">Find other connectors for Azure Logic apps</span></span>](./apis-list.md)