---
title: "conector do Outlook do Office 365 aaaAdd Olá em seus aplicativos lógicos | Microsoft Docs"
description: "Crie aplicativos lógicos interação de tooenable de conector do Office 365 com o Office 365. Por exemplo: criação, edição e atualização de itens de calendário e contatos."
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
ms.openlocfilehash: 86a573c9c54701de3d3f0500d19eaf545e0710ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-office-365-outlook-connector"></a><span data-ttu-id="09914-104">Introdução ao conector do Outlook do Office 365 Olá</span><span class="sxs-lookup"><span data-stu-id="09914-104">Get started with hello Office 365 Outlook connector</span></span>
<span data-ttu-id="09914-105">conector do Outlook do Office 365 Olá permite interação com o Outlook no Office 365.</span><span class="sxs-lookup"><span data-stu-id="09914-105">hello Office 365 Outlook connector enables interaction with Outlook in Office 365.</span></span> <span data-ttu-id="09914-106">Usar este conector toocreate, editar, contatos de atualização e itens de calendário e também obter, enviar e responder tooemail.</span><span class="sxs-lookup"><span data-stu-id="09914-106">Use this connector toocreate, edit, and update contacts and calendar items, and also get, send, and reply tooemail.</span></span>

<span data-ttu-id="09914-107">Com o Outlook do Office 365, você pode:</span><span class="sxs-lookup"><span data-stu-id="09914-107">With Office 365 Outlook, you:</span></span>

* <span data-ttu-id="09914-108">Crie o fluxo de trabalho usando recursos de email e calendário Olá no Office 365.</span><span class="sxs-lookup"><span data-stu-id="09914-108">Build your workflow using hello email and calendar features within Office 365.</span></span> 
* <span data-ttu-id="09914-109">Use gatilhos toostart seu fluxo de trabalho quando há um novo email, quando um item de calendário é atualizado e muito mais.</span><span class="sxs-lookup"><span data-stu-id="09914-109">Use triggers toostart your workflow when there is a new email, when a calendar item is updated, and more.</span></span>
* <span data-ttu-id="09914-110">Use ações toosend um email, criar um novo evento de calendário e muito mais.</span><span class="sxs-lookup"><span data-stu-id="09914-110">Use actions toosend an email, create a new calendar event, and more.</span></span> <span data-ttu-id="09914-111">Por exemplo, quando há um novo objeto no Salesforce (um gatilho), envie um email tooyour Outlook do Office 365 (uma ação).</span><span class="sxs-lookup"><span data-stu-id="09914-111">For example, when there is a new object in Salesforce (a trigger), send an email tooyour Office 365 Outlook (an action).</span></span> 

<span data-ttu-id="09914-112">Este tópico mostra como toouse Olá conector do Outlook do Office 365 em um aplicativo lógico e também lista Olá gatilhos e ações.</span><span class="sxs-lookup"><span data-stu-id="09914-112">This topic shows you how toouse hello Office 365 Outlook connector in a logic app, and also lists hello triggers and actions.</span></span>

> [!NOTE]
> <span data-ttu-id="09914-113">Esta versão do artigo Olá aplica tooLogic aplicativos GA (disponibilidade geral).</span><span class="sxs-lookup"><span data-stu-id="09914-113">This version of hello article applies tooLogic Apps general availability (GA).</span></span>
> 
> 

<span data-ttu-id="09914-114">toolearn mais sobre aplicativos lógicos, consulte [quais são os aplicativos lógicos](../logic-apps/logic-apps-what-are-logic-apps.md) e [criar um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="09914-114">toolearn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-toooffice-365"></a><span data-ttu-id="09914-115">Conecte-se tooOffice 365</span><span class="sxs-lookup"><span data-stu-id="09914-115">Connect tooOffice 365</span></span>
<span data-ttu-id="09914-116">Antes de sua lógica de aplicativo pode acessar qualquer serviço, você primeiro crie um *conexão* toohello service.</span><span class="sxs-lookup"><span data-stu-id="09914-116">Before your logic app can access any service, you first create a *connection* toohello service.</span></span> <span data-ttu-id="09914-117">Uma conexão fornece uma conectividade entre um aplicativo lógico e outro serviço.</span><span class="sxs-lookup"><span data-stu-id="09914-117">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="09914-118">Por exemplo, tooconnect tooOffice 365 Outlook, primeiro é necessário um Office 365 *conexão*.</span><span class="sxs-lookup"><span data-stu-id="09914-118">For example, tooconnect tooOffice 365 Outlook, you first need an Office 365 *connection*.</span></span> <span data-ttu-id="09914-119">toocreate uma conexão, insira as credenciais de saudação você normalmente usa o serviço de saudação tooaccess desejar tooconnect para.</span><span class="sxs-lookup"><span data-stu-id="09914-119">toocreate a connection, enter hello credentials you normally use tooaccess hello service you wish tooconnect to.</span></span> <span data-ttu-id="09914-120">Portanto com o Outlook do Office 365, digite Olá credenciais tooyour conexão de saudação do Office 365 conta toocreate.</span><span class="sxs-lookup"><span data-stu-id="09914-120">So with Office 365 Outlook, enter hello credentials tooyour Office 365 account toocreate hello connection.</span></span>

## <a name="create-hello-connection"></a><span data-ttu-id="09914-121">Criar conexão Olá</span><span class="sxs-lookup"><span data-stu-id="09914-121">Create hello connection</span></span>
> [!INCLUDE [Steps toocreate a connection tooOffice 365](../../includes/connectors-create-api-office365-outlook.md)]
> 
> 

## <a name="use-a-trigger"></a><span data-ttu-id="09914-122">Usar um gatilho</span><span class="sxs-lookup"><span data-stu-id="09914-122">Use a trigger</span></span>
<span data-ttu-id="09914-123">Um gatilho é um evento que pode ser o fluxo de trabalho do hello toostart usado definido em um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="09914-123">A trigger is an event that can be used toostart hello workflow defined in a logic app.</span></span> <span data-ttu-id="09914-124">Gatilhos "sondagem" hello serviço em um intervalo e a frequência com que você deseja.</span><span class="sxs-lookup"><span data-stu-id="09914-124">Triggers "poll" hello service at an interval and frequency that you want.</span></span> <span data-ttu-id="09914-125">[Saiba mais sobre gatilhos](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="09914-125">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="09914-126">No aplicativo de lógica de hello, digite "office 365" tooget uma lista dos gatilhos hello:</span><span class="sxs-lookup"><span data-stu-id="09914-126">In hello logic app, type "office 365" tooget a list of hello triggers:</span></span>  
   
    ![](./media/connectors-create-api-office365-outlook/office365-trigger.png)
2. <span data-ttu-id="09914-127">Escolha **Outlook do Office 365 – quando um evento futuro for iniciado em breve**.</span><span class="sxs-lookup"><span data-stu-id="09914-127">Select **Office 365 Outlook - When an upcoming event is starting soon**.</span></span> <span data-ttu-id="09914-128">Se uma conexão já existir, selecione um calendário na lista suspensa de saudação.</span><span class="sxs-lookup"><span data-stu-id="09914-128">If a connection already exists, then select a calendar from hello drop-down list.</span></span>
   
    ![](./media/connectors-create-api-office365-outlook/sample-calendar.png)
   
    <span data-ttu-id="09914-129">Se você é solicitada toosign em, digite Olá logon na conexão de saudação toocreate detalhes.</span><span class="sxs-lookup"><span data-stu-id="09914-129">If you are prompted toosign in, then enter hello sign in details toocreate hello connection.</span></span> <span data-ttu-id="09914-130">[Criar conexão Olá](connectors-create-api-office365-outlook.md#create-the-connection) neste tópico lista as etapas de saudação.</span><span class="sxs-lookup"><span data-stu-id="09914-130">[Create hello connection](connectors-create-api-office365-outlook.md#create-the-connection) in this topic lists hello steps.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="09914-131">Neste exemplo, o aplicativo de lógica de saudação é executado quando um evento de calendário é atualizado.</span><span class="sxs-lookup"><span data-stu-id="09914-131">In this example, hello logic app runs when a calendar event is updated.</span></span> <span data-ttu-id="09914-132">resultados de saudação toosee deste gatilho, adicione outra ação que envia uma mensagem de texto.</span><span class="sxs-lookup"><span data-stu-id="09914-132">toosee hello results of this trigger, add another action that sends you a text message.</span></span> <span data-ttu-id="09914-133">Por exemplo, adicionar Olá Twilio *enviar mensagem* ação textos quando hello evento de calendário está iniciando em 15 minutos.</span><span class="sxs-lookup"><span data-stu-id="09914-133">For example, add hello Twilio *Send message* action that texts you when hello calendar event is starting in 15 minutes.</span></span> 
   > 
   > 
3. <span data-ttu-id="09914-134">Selecione Olá **editar** botão e defina Olá **frequência** e **intervalo** valores.</span><span class="sxs-lookup"><span data-stu-id="09914-134">Select hello **Edit** button and set hello **Frequency** and **Interval** values.</span></span> <span data-ttu-id="09914-135">Por exemplo, se você quiser Olá gatilho toopoll a cada 15 minutos, em seguida, definir Olá **frequência** muito**minuto**e conjunto hello **intervalo** muito**15**.</span><span class="sxs-lookup"><span data-stu-id="09914-135">For example, if you want hello trigger toopoll every 15 minutes, then set hello **Frequency** too**Minute**, and set hello **Interval** too**15**.</span></span> 
   
    ![](./media/connectors-create-api-office365-outlook/calendar-settings.png)
4. <span data-ttu-id="09914-136">**Salvar** as alterações (canto superior esquerdo da barra de ferramentas de saudação).</span><span class="sxs-lookup"><span data-stu-id="09914-136">**Save** your changes (top left corner of hello toolbar).</span></span> <span data-ttu-id="09914-137">Seu aplicativo lógico é salvo e pode ser habilitado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="09914-137">Your logic app is saved and may be automatically enabled.</span></span>

## <a name="use-an-action"></a><span data-ttu-id="09914-138">Usar uma ação</span><span class="sxs-lookup"><span data-stu-id="09914-138">Use an action</span></span>
<span data-ttu-id="09914-139">Uma ação é uma operação executada pelo fluxo de trabalho Olá definido em um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="09914-139">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="09914-140">[Saiba mais sobre ações](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="09914-140">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="09914-141">Selecione o sinal de adição hello.</span><span class="sxs-lookup"><span data-stu-id="09914-141">Select hello plus sign.</span></span> <span data-ttu-id="09914-142">Consulte várias opções: **adicionar uma ação**, **adicionar uma condição**, ou uma saudação **mais** opções.</span><span class="sxs-lookup"><span data-stu-id="09914-142">You see several choices: **Add an action**, **Add a condition**, or one of hello **More** options.</span></span>
   
    ![](./media/connectors-create-api-office365-outlook/add-action.png)
2. <span data-ttu-id="09914-143">Escolha **Adicionar uma ação**.</span><span class="sxs-lookup"><span data-stu-id="09914-143">Choose **Add an action**.</span></span>
3. <span data-ttu-id="09914-144">Na caixa de texto de saudação, digite "office 365" tooget uma lista de todas as ações disponíveis de saudação.</span><span class="sxs-lookup"><span data-stu-id="09914-144">In hello text box, type “office 365” tooget a list of all hello available actions.</span></span>
   
    ![](./media/connectors-create-api-office365-outlook/office365-actions.png) 
4. <span data-ttu-id="09914-145">Em nosso exemplo, escolha **Outlook do Office 365 – Criar contato**.</span><span class="sxs-lookup"><span data-stu-id="09914-145">In our example, choose **Office 365 Outlook - Create contact**.</span></span> <span data-ttu-id="09914-146">Se uma conexão já existir, escolha Olá **ID da pasta**, **nome**e outras propriedades:</span><span class="sxs-lookup"><span data-stu-id="09914-146">If a connection already exists, then choose hello **Folder ID**, **Given Name**, and other properties:</span></span>  
   
    ![](./media/connectors-create-api-office365-outlook/office365-sampleaction.png)
   
    <span data-ttu-id="09914-147">Se você for solicitado para obter informações de conexão do hello, digite conexão de Olá Olá detalhes toocreate.</span><span class="sxs-lookup"><span data-stu-id="09914-147">If you are prompted for hello connection information, then enter hello details toocreate hello connection.</span></span> <span data-ttu-id="09914-148">[Criar conexão Olá](connectors-create-api-office365-outlook.md#create-the-connection) neste tópico descreve essas propriedades.</span><span class="sxs-lookup"><span data-stu-id="09914-148">[Create hello connection](connectors-create-api-office365-outlook.md#create-the-connection) in this topic describes these properties.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="09914-149">Neste exemplo, criamos um novo contato no Outlook do Office 365.</span><span class="sxs-lookup"><span data-stu-id="09914-149">In this example, we create a new contact in Office 365 Outlook.</span></span> <span data-ttu-id="09914-150">Você pode usar a saída de outro disparador toocreate Olá entre em contato com.</span><span class="sxs-lookup"><span data-stu-id="09914-150">You can use output from another trigger toocreate hello contact.</span></span> <span data-ttu-id="09914-151">Por exemplo, adicionar Olá SalesForce *quando um objeto é criado* gatilho.</span><span class="sxs-lookup"><span data-stu-id="09914-151">For example, add hello SalesForce *When an object is created* trigger.</span></span> <span data-ttu-id="09914-152">Em seguida, adicione Olá Outlook do Office 365 *criar contato* ação que usa Olá SalesForce campos toocreate Olá novo novo contato no Office 365.</span><span class="sxs-lookup"><span data-stu-id="09914-152">Then add hello Office 365 Outlook *Create contact* action that uses hello SalesForce fields toocreate hello new new contact in Office 365.</span></span> 
   > 
   > 
5. <span data-ttu-id="09914-153">**Salvar** as alterações (canto superior esquerdo da barra de ferramentas de saudação).</span><span class="sxs-lookup"><span data-stu-id="09914-153">**Save** your changes (top left corner of hello toolbar).</span></span> <span data-ttu-id="09914-154">Seu aplicativo lógico é salvo e pode ser habilitado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="09914-154">Your logic app is saved and may be automatically enabled.</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="09914-155">Detalhes específicos do conector</span><span class="sxs-lookup"><span data-stu-id="09914-155">Connector-specific details</span></span>

<span data-ttu-id="09914-156">Exibir quaisquer gatilhos e ações definidas em swagger Olá e também os limites de saudação [detalhes conector](/connectors/office365connector/).</span><span class="sxs-lookup"><span data-stu-id="09914-156">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/office365connector/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="09914-157">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="09914-157">Next Steps</span></span>
<span data-ttu-id="09914-158">[Criar um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="09914-158">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="09914-159">Explorar Olá outros conectores disponíveis na lógica de aplicativos no nosso [lista APIs](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="09914-159">Explore hello other available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>

