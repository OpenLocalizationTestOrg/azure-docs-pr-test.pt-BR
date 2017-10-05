---
title: "Adicionar o conector Outlook do Office 365 em seus Aplicativos Lógicos | Microsoft Docs"
description: "Crie aplicativos lógicos com o conector do Office 365 para permitir a interação com o Office 365. Por exemplo: criação, edição e atualização de itens de calendário e contatos."
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: b2f6cc2c-bba2-493a-b0ba-841785462a80
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 5335dae62e61659b68e8befb4ed0d404dffb800c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-office-365-outlook-connector"></a><span data-ttu-id="aa5aa-104">Introdução ao conector do Outlook do Office 365</span><span class="sxs-lookup"><span data-stu-id="aa5aa-104">Get started with the Office 365 Outlook connector</span></span>
<span data-ttu-id="aa5aa-105">O conector do Outlook do Office 365 permite interação com o Outlook no Office 365.</span><span class="sxs-lookup"><span data-stu-id="aa5aa-105">The Office 365 Outlook connector enables interaction with Outlook in Office 365.</span></span> <span data-ttu-id="aa5aa-106">Use esse conector para criar, editar e atualizar contatos e itens de calendário, bem como para obter, enviar e responder a emails.</span><span class="sxs-lookup"><span data-stu-id="aa5aa-106">Use this connector to create, edit, and update contacts and calendar items, and also get, send, and reply to email.</span></span>

<span data-ttu-id="aa5aa-107">Com o Outlook do Office 365, você pode:</span><span class="sxs-lookup"><span data-stu-id="aa5aa-107">With Office 365 Outlook, you:</span></span>

* <span data-ttu-id="aa5aa-108">Compilar o fluxo de trabalho usando os recursos de email e calendário no Office 365.</span><span class="sxs-lookup"><span data-stu-id="aa5aa-108">Build your workflow using the email and calendar features within Office 365.</span></span> 
* <span data-ttu-id="aa5aa-109">Usar gatilhos para iniciar o fluxo de trabalho quando houver um novo email, quando um item de calendário for atualizado e muito mais.</span><span class="sxs-lookup"><span data-stu-id="aa5aa-109">Use triggers to start your workflow when there is a new email, when a calendar item is updated, and more.</span></span>
* <span data-ttu-id="aa5aa-110">Usar ações que enviem um email, criem um novo evento de calendário e muito mais.</span><span class="sxs-lookup"><span data-stu-id="aa5aa-110">Use actions to send an email, create a new calendar event, and more.</span></span> <span data-ttu-id="aa5aa-111">Por exemplo, quando houver um novo objeto em Salesforce (um gatilho), envie um email ao seu Outlook do Office 365 (uma ação).</span><span class="sxs-lookup"><span data-stu-id="aa5aa-111">For example, when there is a new object in Salesforce (a trigger), send an email to your Office 365 Outlook (an action).</span></span> 

<span data-ttu-id="aa5aa-112">Este tópico mostra como usar o conector do Outlook do Office 365 em um aplicativo lógico, além de listar os gatilhos e as ações.</span><span class="sxs-lookup"><span data-stu-id="aa5aa-112">This topic shows you how to use the Office 365 Outlook connector in a logic app, and also lists the triggers and actions.</span></span>

> [!NOTE]
> <span data-ttu-id="aa5aa-113">Esta versão do artigo se aplica à disponibilidade de Aplicativos Lógicos em geral (GA).</span><span class="sxs-lookup"><span data-stu-id="aa5aa-113">This version of the article applies to Logic Apps general availability (GA).</span></span>
> 
> 

<span data-ttu-id="aa5aa-114">Para saber mais sobre os Aplicativos Lógicos, consulte [O que são aplicativos lógicos](../logic-apps/logic-apps-what-are-logic-apps.md) e [Criar um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="aa5aa-114">To learn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-office-365"></a><span data-ttu-id="aa5aa-115">Conectar ao Office 365</span><span class="sxs-lookup"><span data-stu-id="aa5aa-115">Connect to Office 365</span></span>
<span data-ttu-id="aa5aa-116">Antes do aplicativo lógico poder acessar qualquer serviço, primeiro crie uma *conexão* com o serviço.</span><span class="sxs-lookup"><span data-stu-id="aa5aa-116">Before your logic app can access any service, you first create a *connection* to the service.</span></span> <span data-ttu-id="aa5aa-117">Uma conexão fornece uma conectividade entre um aplicativo lógico e outro serviço.</span><span class="sxs-lookup"><span data-stu-id="aa5aa-117">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="aa5aa-118">Por exemplo, para se conectar ao Outlook do Office 365, primeiramente é necessária uma *conexão* do Office 365.</span><span class="sxs-lookup"><span data-stu-id="aa5aa-118">For example, to connect to Office 365 Outlook, you first need an Office 365 *connection*.</span></span> <span data-ttu-id="aa5aa-119">Para criar uma conexão, insira as credenciais que você normalmente usa para acessar o serviço ao qual deseja conectar-se.</span><span class="sxs-lookup"><span data-stu-id="aa5aa-119">To create a connection, enter the credentials you normally use to access the service you wish to connect to.</span></span> <span data-ttu-id="aa5aa-120">Assim, com o Outlook do Office 365, insira as credenciais de sua conta do Office 365 para criar a conexão.</span><span class="sxs-lookup"><span data-stu-id="aa5aa-120">So with Office 365 Outlook, enter the credentials to your Office 365 account to create the connection.</span></span>

## <a name="create-the-connection"></a><span data-ttu-id="aa5aa-121">Criar a conexão</span><span class="sxs-lookup"><span data-stu-id="aa5aa-121">Create the connection</span></span>
> [!INCLUDE [Steps to create a connection to Office 365](../../includes/connectors-create-api-office365-outlook.md)]
> 
> 

## <a name="use-a-trigger"></a><span data-ttu-id="aa5aa-122">Usar um gatilho</span><span class="sxs-lookup"><span data-stu-id="aa5aa-122">Use a trigger</span></span>
<span data-ttu-id="aa5aa-123">Um gatilho é um evento que pode ser usado para iniciar o fluxo de trabalho definido em um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="aa5aa-123">A trigger is an event that can be used to start the workflow defined in a logic app.</span></span> <span data-ttu-id="aa5aa-124">Gatilhos "sondam" o serviço no intervalo e na frequência desejados.</span><span class="sxs-lookup"><span data-stu-id="aa5aa-124">Triggers "poll" the service at an interval and frequency that you want.</span></span> <span data-ttu-id="aa5aa-125">[Saiba mais sobre gatilhos](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="aa5aa-125">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="aa5aa-126">No aplicativo lógico, digite "office 365" para obter uma lista de gatilhos:</span><span class="sxs-lookup"><span data-stu-id="aa5aa-126">In the logic app, type "office 365" to get a list of the triggers:</span></span>  
   
    ![](./media/connectors-create-api-office365-outlook/office365-trigger.png)
2. <span data-ttu-id="aa5aa-127">Escolha **Outlook do Office 365 – quando um evento futuro for iniciado em breve**.</span><span class="sxs-lookup"><span data-stu-id="aa5aa-127">Select **Office 365 Outlook - When an upcoming event is starting soon**.</span></span> <span data-ttu-id="aa5aa-128">Se já existir uma conexão, escolha um calendário na lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="aa5aa-128">If a connection already exists, then select a calendar from the drop-down list.</span></span>
   
    ![](./media/connectors-create-api-office365-outlook/sample-calendar.png)
   
    <span data-ttu-id="aa5aa-129">Se você for solicitado a entrar, insira os detalhes do logon para criar a conexão.</span><span class="sxs-lookup"><span data-stu-id="aa5aa-129">If you are prompted to sign in, then enter the sign in details to create the connection.</span></span> <span data-ttu-id="aa5aa-130">[Criar a conexão](connectors-create-api-office365-outlook.md#create-the-connection) neste tópico lista as etapas.</span><span class="sxs-lookup"><span data-stu-id="aa5aa-130">[Create the connection](connectors-create-api-office365-outlook.md#create-the-connection) in this topic lists the steps.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="aa5aa-131">Neste exemplo, o aplicativo lógico é executado quando um evento de calendário é atualizado.</span><span class="sxs-lookup"><span data-stu-id="aa5aa-131">In this example, the logic app runs when a calendar event is updated.</span></span> <span data-ttu-id="aa5aa-132">Para ver os resultados desse gatilho, adicione outra ação que envie uma mensagem de texto para você.</span><span class="sxs-lookup"><span data-stu-id="aa5aa-132">To see the results of this trigger, add another action that sends you a text message.</span></span> <span data-ttu-id="aa5aa-133">Por exemplo, adicione a ação *Enviar mensagem* do Twilio que avisa você, por texto, quando o evento de calendário estiver iniciando em 15 minutos.</span><span class="sxs-lookup"><span data-stu-id="aa5aa-133">For example, add the Twilio *Send message* action that texts you when the calendar event is starting in 15 minutes.</span></span> 
   > 
   > 
3. <span data-ttu-id="aa5aa-134">Selecione o botão **Editar** e defina os valores **Frequência** e **Intervalo**.</span><span class="sxs-lookup"><span data-stu-id="aa5aa-134">Select the **Edit** button and set the **Frequency** and **Interval** values.</span></span> <span data-ttu-id="aa5aa-135">Por exemplo, se você quiser que o gatilho faça uma sondagem a cada 15 minutos, defina a **Frequência** como **Minuto** e **Intervalo** como **15**.</span><span class="sxs-lookup"><span data-stu-id="aa5aa-135">For example, if you want the trigger to poll every 15 minutes, then set the **Frequency** to **Minute**, and set the **Interval** to **15**.</span></span> 
   
    ![](./media/connectors-create-api-office365-outlook/calendar-settings.png)
4. <span data-ttu-id="aa5aa-136">**Salve** as alterações (canto superior esquerdo da barra de ferramentas).</span><span class="sxs-lookup"><span data-stu-id="aa5aa-136">**Save** your changes (top left corner of the toolbar).</span></span> <span data-ttu-id="aa5aa-137">Seu aplicativo lógico é salvo e pode ser habilitado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="aa5aa-137">Your logic app is saved and may be automatically enabled.</span></span>

## <a name="use-an-action"></a><span data-ttu-id="aa5aa-138">Usar uma ação</span><span class="sxs-lookup"><span data-stu-id="aa5aa-138">Use an action</span></span>
<span data-ttu-id="aa5aa-139">Uma ação é uma operação executada pelo fluxo de trabalho definido em um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="aa5aa-139">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="aa5aa-140">[Saiba mais sobre ações](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="aa5aa-140">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="aa5aa-141">Selecione o sinal de mais.</span><span class="sxs-lookup"><span data-stu-id="aa5aa-141">Select the plus sign.</span></span> <span data-ttu-id="aa5aa-142">Você tem várias opções: **adicionar uma ação**, **adicionar uma condição** ou uma das opções **Mais**.</span><span class="sxs-lookup"><span data-stu-id="aa5aa-142">You see several choices: **Add an action**, **Add a condition**, or one of the **More** options.</span></span>
   
    ![](./media/connectors-create-api-office365-outlook/add-action.png)
2. <span data-ttu-id="aa5aa-143">Escolha **Adicionar uma ação**.</span><span class="sxs-lookup"><span data-stu-id="aa5aa-143">Choose **Add an action**.</span></span>
3. <span data-ttu-id="aa5aa-144">Na caixa de texto, digite "office 365" para obter uma lista de todas as ações disponíveis.</span><span class="sxs-lookup"><span data-stu-id="aa5aa-144">In the text box, type “office 365” to get a list of all the available actions.</span></span>
   
    ![](./media/connectors-create-api-office365-outlook/office365-actions.png) 
4. <span data-ttu-id="aa5aa-145">Em nosso exemplo, escolha **Outlook do Office 365 – Criar contato**.</span><span class="sxs-lookup"><span data-stu-id="aa5aa-145">In our example, choose **Office 365 Outlook - Create contact**.</span></span> <span data-ttu-id="aa5aa-146">Se já existir uma conexão, escolha **ID da Pasta**, **Nome Fornecido** e outras propriedades:</span><span class="sxs-lookup"><span data-stu-id="aa5aa-146">If a connection already exists, then choose the **Folder ID**, **Given Name**, and other properties:</span></span>  
   
    ![](./media/connectors-create-api-office365-outlook/office365-sampleaction.png)
   
    <span data-ttu-id="aa5aa-147">Se as informações de conexão forem solicitadas, insira os detalhes para criar a conexão.</span><span class="sxs-lookup"><span data-stu-id="aa5aa-147">If you are prompted for the connection information, then enter the details to create the connection.</span></span> <span data-ttu-id="aa5aa-148">[Criar a conexão](connectors-create-api-office365-outlook.md#create-the-connection) neste tópico descreve estas propriedades.</span><span class="sxs-lookup"><span data-stu-id="aa5aa-148">[Create the connection](connectors-create-api-office365-outlook.md#create-the-connection) in this topic describes these properties.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="aa5aa-149">Neste exemplo, criamos um novo contato no Outlook do Office 365.</span><span class="sxs-lookup"><span data-stu-id="aa5aa-149">In this example, we create a new contact in Office 365 Outlook.</span></span> <span data-ttu-id="aa5aa-150">Você pode usar a saída de outro gatilho para criar o contato.</span><span class="sxs-lookup"><span data-stu-id="aa5aa-150">You can use output from another trigger to create the contact.</span></span> <span data-ttu-id="aa5aa-151">Por exemplo, adicione o gatilho *Quando um objeto é criado* do SalesForce.</span><span class="sxs-lookup"><span data-stu-id="aa5aa-151">For example, add the SalesForce *When an object is created* trigger.</span></span> <span data-ttu-id="aa5aa-152">Em seguida, adicione a ação *Criar contato* do Outlook do Office 365 que usa os campos do SalesForce para criar o novo contato no Office 365.</span><span class="sxs-lookup"><span data-stu-id="aa5aa-152">Then add the Office 365 Outlook *Create contact* action that uses the SalesForce fields to create the new new contact in Office 365.</span></span> 
   > 
   > 
5. <span data-ttu-id="aa5aa-153">**Salve** as alterações (canto superior esquerdo da barra de ferramentas).</span><span class="sxs-lookup"><span data-stu-id="aa5aa-153">**Save** your changes (top left corner of the toolbar).</span></span> <span data-ttu-id="aa5aa-154">Seu aplicativo lógico é salvo e pode ser habilitado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="aa5aa-154">Your logic app is saved and may be automatically enabled.</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="aa5aa-155">Detalhes específicos do conector</span><span class="sxs-lookup"><span data-stu-id="aa5aa-155">Connector-specific details</span></span>

<span data-ttu-id="aa5aa-156">Veja os gatilhos e ações definidos no swagger e também os limites nos [detalhes do conector](/connectors/office365connector/).</span><span class="sxs-lookup"><span data-stu-id="aa5aa-156">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/office365connector/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="aa5aa-157">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="aa5aa-157">Next Steps</span></span>
<span data-ttu-id="aa5aa-158">[Criar um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="aa5aa-158">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="aa5aa-159">Explore os outros conectores disponíveis nos Aplicativos Lógicos em nossa [lista de APIs](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="aa5aa-159">Explore the other available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>

