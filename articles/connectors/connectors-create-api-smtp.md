---
title: "conector de aaaSMTP em aplicativos do Azure lógica | Microsoft Docs"
description: "Crie aplicativos lógicos com o serviço de Aplicativo do Azure. Conecte-se tooSMTP toosend email."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: d4141c08-88d7-4e59-a757-c06d0dc74300
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/15/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 36bb836851014d24f2e069fda8376ad7a08c943b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-smtp-connector"></a><span data-ttu-id="44d3d-104">Introdução ao conector de SMTP Olá</span><span class="sxs-lookup"><span data-stu-id="44d3d-104">Get started with hello SMTP connector</span></span>
<span data-ttu-id="44d3d-105">Conecte-se tooSMTP toosend email.</span><span class="sxs-lookup"><span data-stu-id="44d3d-105">Connect tooSMTP toosend email.</span></span>

<span data-ttu-id="44d3d-106">toouse [qualquer conector](apis-list.md), primeiro é necessário toocreate um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="44d3d-106">toouse [any connector](apis-list.md), you first need toocreate a logic app.</span></span> <span data-ttu-id="44d3d-107">Você pode começar [criando um aplicativo lógico agora mesmo](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="44d3d-107">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-toosmtp"></a><span data-ttu-id="44d3d-108">Conecte-se tooSMTP</span><span class="sxs-lookup"><span data-stu-id="44d3d-108">Connect tooSMTP</span></span>
<span data-ttu-id="44d3d-109">Antes de sua lógica de aplicativo pode acessar qualquer serviço, primeiro é necessário toocreate um *conexão* toohello service.</span><span class="sxs-lookup"><span data-stu-id="44d3d-109">Before your logic app can access any service, you first need toocreate a *connection* toohello service.</span></span> <span data-ttu-id="44d3d-110">Uma [conexão](connectors-overview.md) fornece uma conectividade entre um aplicativo lógico e outro serviço.</span><span class="sxs-lookup"><span data-stu-id="44d3d-110">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="44d3d-111">Por exemplo, tooconnect tooSMTP, primeiro é necessário um SMTP *conexão*.</span><span class="sxs-lookup"><span data-stu-id="44d3d-111">For example, tooconnect tooSMTP, you first need an SMTP *connection*.</span></span> <span data-ttu-id="44d3d-112">toocreate uma conexão, insira as credenciais de saudação você normalmente usa o serviço de saudação tooaccess você se conectar ao.</span><span class="sxs-lookup"><span data-stu-id="44d3d-112">toocreate a connection, enter hello credentials you normally use tooaccess hello service you connect to.</span></span> <span data-ttu-id="44d3d-113">Assim, no exemplo hello SMTP, insira o nome de conexão de tooyour de credenciais de Olá, endereço do servidor SMTP e usuário logon informações toocreate Olá conexão tooSMTP.</span><span class="sxs-lookup"><span data-stu-id="44d3d-113">So, in hello SMTP example, enter hello credentials tooyour connection name, SMTP server address, and user login information toocreate hello connection tooSMTP.</span></span>  

### <a name="create-a-connection-toosmtp"></a><span data-ttu-id="44d3d-114">Criar uma conexão tooSMTP</span><span class="sxs-lookup"><span data-stu-id="44d3d-114">Create a connection tooSMTP</span></span>
> [!INCLUDE [Steps toocreate a connection tooSMTP](../../includes/connectors-create-api-smtp.md)]
> 
> 

## <a name="use-an-smtp-trigger"></a><span data-ttu-id="44d3d-115">Usar um gatilho de SMTP</span><span class="sxs-lookup"><span data-stu-id="44d3d-115">Use an SMTP trigger</span></span>
<span data-ttu-id="44d3d-116">Um gatilho é um evento que pode ser o fluxo de trabalho do hello toostart usado definido em um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="44d3d-116">A trigger is an event that can be used toostart hello workflow defined in a logic app.</span></span> <span data-ttu-id="44d3d-117">[Saiba mais sobre gatilhos](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="44d3d-117">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="44d3d-118">Neste exemplo, porque o SMTP não tem um gatilho de seu próprio, vamos usar Olá **Salesforce - quando um objeto é criado** gatilho.</span><span class="sxs-lookup"><span data-stu-id="44d3d-118">In this example, because SMTP does not have a trigger of its own, we'll use hello **Salesforce - When an object is created** trigger.</span></span> <span data-ttu-id="44d3d-119">Esse gatilho é ativado quando um novo objeto é criado no Salesforce.</span><span class="sxs-lookup"><span data-stu-id="44d3d-119">This trigger activates when a new object is created in Salesforce.</span></span> <span data-ttu-id="44d3d-120">Para nosso exemplo, vamos defini-lo, de modo que toda vez que um novo cliente potencial é criado no Salesforce, uma *enviar email* ação ocorre por meio do conector SMTP de saudação com uma notificação de saudação novo cliente potencial que está sendo criado.</span><span class="sxs-lookup"><span data-stu-id="44d3d-120">For our example, we'll set it up such that every time a new lead is created in Salesforce, a *send email* action occurs via hello SMTP connector with a notification of hello new lead being created.</span></span>

1. <span data-ttu-id="44d3d-121">Digite *salesforce* na caixa de pesquisa Olá no designer de aplicativos de lógica de saudação selecione Olá **Salesforce - quando um objeto é criado** gatilho.</span><span class="sxs-lookup"><span data-stu-id="44d3d-121">Enter *salesforce* in hello search box on hello logic apps designer then select hello **Salesforce - When an object is created** trigger.</span></span>  
   ![](../../includes/media/connectors-create-api-salesforce/trigger-1.png)  
2. <span data-ttu-id="44d3d-122">Olá **quando um objeto é criado** controle é exibido.</span><span class="sxs-lookup"><span data-stu-id="44d3d-122">hello **When an object is created** control is displayed.</span></span>
   ![](../../includes/media/connectors-create-api-salesforce/trigger-2.png)  
3. <span data-ttu-id="44d3d-123">Selecione Olá **tipo de objeto** , em seguida, selecione *levar* da lista de saudação de objetos.</span><span class="sxs-lookup"><span data-stu-id="44d3d-123">Select hello **Object Type** then select *Lead* from hello list of objects.</span></span> <span data-ttu-id="44d3d-124">Nessa etapa, instruímos sobre a criação de um gatilho que notificará seu aplicativo lógico sempre que um novo cliente potencial for criado no Salesforce.</span><span class="sxs-lookup"><span data-stu-id="44d3d-124">In this step you are indicating that you are creating a trigger that will notify your logic app whenever a new lead is created in Salesforce.</span></span>  
   ![](../../includes/media/connectors-create-api-salesforce/trigger3.png)  
4. <span data-ttu-id="44d3d-125">gatilho Olá foi criado.</span><span class="sxs-lookup"><span data-stu-id="44d3d-125">hello trigger has been created.</span></span>  
   ![](../../includes/media/connectors-create-api-salesforce/trigger-4.png)  

## <a name="use-an-smtp-action"></a><span data-ttu-id="44d3d-126">Usar uma ação de SMTP</span><span class="sxs-lookup"><span data-stu-id="44d3d-126">Use an SMTP action</span></span>
<span data-ttu-id="44d3d-127">Uma ação é uma operação executada pelo fluxo de trabalho Olá definido em um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="44d3d-127">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="44d3d-128">[Saiba mais sobre ações](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="44d3d-128">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="44d3d-129">Agora que hello gatilho foi adicionado, siga estes passos tooadd um SMTP ação que ocorrerá quando um novo cliente potencial é criado no Salesforce.</span><span class="sxs-lookup"><span data-stu-id="44d3d-129">Now that hello trigger has been added, follow these steps tooadd an SMTP action that will occur when a new lead is created in Salesforce.</span></span>

1. <span data-ttu-id="44d3d-130">Selecione **+ nova etapa** ação de saudação tooadd você gostaria que tootake quando um novo cliente potencial é criado.</span><span class="sxs-lookup"><span data-stu-id="44d3d-130">Select **+ New Step** tooadd hello action you would like tootake when a new lead is created.</span></span>  
   ![](../../includes/media/connectors-create-api-salesforce/trigger4.png)  
2. <span data-ttu-id="44d3d-131">Escolha **Adicionar uma ação**.</span><span class="sxs-lookup"><span data-stu-id="44d3d-131">Select **Add an action**.</span></span> <span data-ttu-id="44d3d-132">Essa caixa de pesquisa de Olá abre onde você pode procurar qualquer ação que você gostaria de tootake.</span><span class="sxs-lookup"><span data-stu-id="44d3d-132">This opens hello search box where you can search for any action you would like tootake.</span></span>  
   ![](../../includes/media/connectors-create-api-smtp/using-smtp-action-2.png)  
3. <span data-ttu-id="44d3d-133">Digite *smtp* toosearch para tooSMTP de ações relacionadas.</span><span class="sxs-lookup"><span data-stu-id="44d3d-133">Enter *smtp* toosearch for actions related tooSMTP.</span></span>  
4. <span data-ttu-id="44d3d-134">Selecione **SMTP - Enviar Email** como Olá tootake ação quando o cliente potencial Olá é criado.</span><span class="sxs-lookup"><span data-stu-id="44d3d-134">Select **SMTP - Send Email** as hello action tootake when hello new lead is created.</span></span> <span data-ttu-id="44d3d-135">bloco de controle de ação de saudação é aberto.</span><span class="sxs-lookup"><span data-stu-id="44d3d-135">hello action control block opens.</span></span> <span data-ttu-id="44d3d-136">Você terá tooestablish sua conexão smtp em bloco designer Olá se você não tiver feito isso anteriormente.</span><span class="sxs-lookup"><span data-stu-id="44d3d-136">You will have tooestablish your smtp connection in hello designer block if you have not done so previously.</span></span>  
   ![](../../includes/media/connectors-create-api-smtp/smtp-2.png)    
5. <span data-ttu-id="44d3d-137">Insira suas informações de email desejados no hello **SMTP - Enviar Email** bloco.</span><span class="sxs-lookup"><span data-stu-id="44d3d-137">Input your desired email information in hello **SMTP - Send Email** block.</span></span>  
   ![](../../includes/media/connectors-create-api-smtp/using-smtp-action-4.PNG)  
6. <span data-ttu-id="44d3d-138">Salve seu trabalho na ordem tooactivate seu fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="44d3d-138">Save your work in order tooactivate your workflow.</span></span>  

## <a name="connector-specific-details"></a><span data-ttu-id="44d3d-139">Detalhes específicos do conector</span><span class="sxs-lookup"><span data-stu-id="44d3d-139">Connector-specific details</span></span>

<span data-ttu-id="44d3d-140">Exibir quaisquer gatilhos e ações definidas em swagger Olá e também os limites de saudação [detalhes conector](/connectors/smtpconnector/).</span><span class="sxs-lookup"><span data-stu-id="44d3d-140">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/smtpconnector/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="44d3d-141">Mais conectores</span><span class="sxs-lookup"><span data-stu-id="44d3d-141">More connectors</span></span>
<span data-ttu-id="44d3d-142">Voltar toohello [lista APIs](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="44d3d-142">Go back toohello [APIs list](apis-list.md).</span></span>
