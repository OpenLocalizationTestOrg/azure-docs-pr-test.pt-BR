---
title: "Conector SMTP no Aplicativo Lógico do Azure | Microsoft Docs"
description: "Crie aplicativos lógicos com o serviço de Aplicativo do Azure. Conecte-se ao SMTP para enviar email."
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
ms.openlocfilehash: 1cf96bbf8bd215d7ddb3c99860a5cb4e668be3c2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-smtp-connector"></a><span data-ttu-id="933e7-104">Introdução ao conector do SMTP</span><span class="sxs-lookup"><span data-stu-id="933e7-104">Get started with the SMTP connector</span></span>
<span data-ttu-id="933e7-105">Conecte-se ao SMTP para enviar email.</span><span class="sxs-lookup"><span data-stu-id="933e7-105">Connect to SMTP to send email.</span></span>

<span data-ttu-id="933e7-106">Para usar [qualquer conector](apis-list.md), primeiro é preciso criar um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="933e7-106">To use [any connector](apis-list.md), you first need to create a logic app.</span></span> <span data-ttu-id="933e7-107">Você pode começar [criando um aplicativo lógico agora mesmo](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="933e7-107">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-smtp"></a><span data-ttu-id="933e7-108">Conectar-se ao SMTP</span><span class="sxs-lookup"><span data-stu-id="933e7-108">Connect to SMTP</span></span>
<span data-ttu-id="933e7-109">Para que o aplicativo lógico possa acessar qualquer serviço, crie primeiro uma *conexão* com o serviço.</span><span class="sxs-lookup"><span data-stu-id="933e7-109">Before your logic app can access any service, you first need to create a *connection* to the service.</span></span> <span data-ttu-id="933e7-110">Uma [conexão](connectors-overview.md) fornece uma conectividade entre um aplicativo lógico e outro serviço.</span><span class="sxs-lookup"><span data-stu-id="933e7-110">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="933e7-111">Por exemplo, para se conectar ao SMTP, é preciso ter uma *conexão* do SMTP.</span><span class="sxs-lookup"><span data-stu-id="933e7-111">For example, to connect to SMTP, you first need an SMTP *connection*.</span></span> <span data-ttu-id="933e7-112">Para criar uma conexão, insira as credenciais que você normalmente usa para acessar o serviço ao qual se conecta.</span><span class="sxs-lookup"><span data-stu-id="933e7-112">To create a connection, enter the credentials you normally use to access the service you connect to.</span></span> <span data-ttu-id="933e7-113">Assim, no exemplo de SMTP, insira as credenciais de seu nome de conexão, do endereço do servidor SMTP e das informações de logon do usuário para criar a conexão com o SMTP.</span><span class="sxs-lookup"><span data-stu-id="933e7-113">So, in the SMTP example, enter the credentials to your connection name, SMTP server address, and user login information to create the connection to SMTP.</span></span>  

### <a name="create-a-connection-to-smtp"></a><span data-ttu-id="933e7-114">Criar uma conexão com o SMTP</span><span class="sxs-lookup"><span data-stu-id="933e7-114">Create a connection to SMTP</span></span>
> [!INCLUDE [Steps to create a connection to SMTP](../../includes/connectors-create-api-smtp.md)]
> 
> 

## <a name="use-an-smtp-trigger"></a><span data-ttu-id="933e7-115">Usar um gatilho de SMTP</span><span class="sxs-lookup"><span data-stu-id="933e7-115">Use an SMTP trigger</span></span>
<span data-ttu-id="933e7-116">Um gatilho é um evento que pode ser usado para iniciar o fluxo de trabalho definido em um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="933e7-116">A trigger is an event that can be used to start the workflow defined in a logic app.</span></span> <span data-ttu-id="933e7-117">[Saiba mais sobre gatilhos](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="933e7-117">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="933e7-118">Neste exemplo, como o SMTP não tem seu próprio gatilho, usaremos o gatilho **Salesforce – quando um objeto é criado**.</span><span class="sxs-lookup"><span data-stu-id="933e7-118">In this example, because SMTP does not have a trigger of its own, we'll use the **Salesforce - When an object is created** trigger.</span></span> <span data-ttu-id="933e7-119">Esse gatilho é ativado quando um novo objeto é criado no Salesforce.</span><span class="sxs-lookup"><span data-stu-id="933e7-119">This trigger activates when a new object is created in Salesforce.</span></span> <span data-ttu-id="933e7-120">Em nosso exemplo, nós o configuraremos de modo que toda vez que um novo cliente potencial for criado no Salesforce, uma ação *enviar email* ocorrerá por meio do conector de SMTP com uma notificação do novo cliente potencial que está sendo criado.</span><span class="sxs-lookup"><span data-stu-id="933e7-120">For our example, we'll set it up such that every time a new lead is created in Salesforce, a *send email* action occurs via the SMTP connector with a notification of the new lead being created.</span></span>

1. <span data-ttu-id="933e7-121">Digite *salesforce* na caixa de pesquisa no designer de aplicativos lógicos e escolha o gatilho **Salesforce — Quando um objeto é criado** .</span><span class="sxs-lookup"><span data-stu-id="933e7-121">Enter *salesforce* in the search box on the logic apps designer then select the **Salesforce - When an object is created** trigger.</span></span>  
   ![](../../includes/media/connectors-create-api-salesforce/trigger-1.png)  
2. <span data-ttu-id="933e7-122">O controle **Quando um objeto é criado** é exibido.</span><span class="sxs-lookup"><span data-stu-id="933e7-122">The **When an object is created** control is displayed.</span></span>
   ![](../../includes/media/connectors-create-api-salesforce/trigger-2.png)  
3. <span data-ttu-id="933e7-123">Escolha o **Tipo de Objeto** e selecione *Cliente Potencial* na lista de objetos.</span><span class="sxs-lookup"><span data-stu-id="933e7-123">Select the **Object Type** then select *Lead* from the list of objects.</span></span> <span data-ttu-id="933e7-124">Nessa etapa, instruímos sobre a criação de um gatilho que notificará seu aplicativo lógico sempre que um novo cliente potencial for criado no Salesforce.</span><span class="sxs-lookup"><span data-stu-id="933e7-124">In this step you are indicating that you are creating a trigger that will notify your logic app whenever a new lead is created in Salesforce.</span></span>  
   ![](../../includes/media/connectors-create-api-salesforce/trigger3.png)  
4. <span data-ttu-id="933e7-125">O gatilho foi criado.</span><span class="sxs-lookup"><span data-stu-id="933e7-125">The trigger has been created.</span></span>  
   ![](../../includes/media/connectors-create-api-salesforce/trigger-4.png)  

## <a name="use-an-smtp-action"></a><span data-ttu-id="933e7-126">Usar uma ação de SMTP</span><span class="sxs-lookup"><span data-stu-id="933e7-126">Use an SMTP action</span></span>
<span data-ttu-id="933e7-127">Uma ação é uma operação executada pelo fluxo de trabalho definido em um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="933e7-127">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="933e7-128">[Saiba mais sobre ações](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="933e7-128">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="933e7-129">Agora que o gatilho foi adicionado, siga estas etapas para adicionar uma ação de SMTP que ocorrerá quando um novo cliente potencial for criado no Salesforce.</span><span class="sxs-lookup"><span data-stu-id="933e7-129">Now that the trigger has been added, follow these steps to add an SMTP action that will occur when a new lead is created in Salesforce.</span></span>

1. <span data-ttu-id="933e7-130">Escolha **+ Nova etapa** para adicionar a ação que deseja executar quando um novo cliente potencial é criado.</span><span class="sxs-lookup"><span data-stu-id="933e7-130">Select **+ New Step** to add the action you would like to take when a new lead is created.</span></span>  
   ![](../../includes/media/connectors-create-api-salesforce/trigger4.png)  
2. <span data-ttu-id="933e7-131">Escolha **Adicionar uma ação**.</span><span class="sxs-lookup"><span data-stu-id="933e7-131">Select **Add an action**.</span></span> <span data-ttu-id="933e7-132">Isso abre a caixa de pesquisa, na qual é possível procurar qualquer ação que você deseja realizar.</span><span class="sxs-lookup"><span data-stu-id="933e7-132">This opens the search box where you can search for any action you would like to take.</span></span>  
   ![](../../includes/media/connectors-create-api-smtp/using-smtp-action-2.png)  
3. <span data-ttu-id="933e7-133">Digite *smtp* para pesquisar todas as ações relacionadas ao SMTP.</span><span class="sxs-lookup"><span data-stu-id="933e7-133">Enter *smtp* to search for actions related to SMTP.</span></span>  
4. <span data-ttu-id="933e7-134">Escolha **SMTP - enviar email** como a ação a ser tomada quando o novo cliente potencial é criado.</span><span class="sxs-lookup"><span data-stu-id="933e7-134">Select **SMTP - Send Email** as the action to take when the new lead is created.</span></span> <span data-ttu-id="933e7-135">O bloco de controle de ação é aberto.</span><span class="sxs-lookup"><span data-stu-id="933e7-135">The action control block opens.</span></span> <span data-ttu-id="933e7-136">Você terá que estabelecer a conexão smtp no bloco de designer, caso não tenha feito isso anteriormente.</span><span class="sxs-lookup"><span data-stu-id="933e7-136">You will have to establish your smtp connection in the designer block if you have not done so previously.</span></span>  
   ![](../../includes/media/connectors-create-api-smtp/smtp-2.png)    
5. <span data-ttu-id="933e7-137">Insira suas informações de email desejadas no bloco **SMTP – enviar email**.</span><span class="sxs-lookup"><span data-stu-id="933e7-137">Input your desired email information in the **SMTP - Send Email** block.</span></span>  
   ![](../../includes/media/connectors-create-api-smtp/using-smtp-action-4.PNG)  
6. <span data-ttu-id="933e7-138">Salve seu trabalho para ativar o fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="933e7-138">Save your work in order to activate your workflow.</span></span>  

## <a name="connector-specific-details"></a><span data-ttu-id="933e7-139">Detalhes específicos do conector</span><span class="sxs-lookup"><span data-stu-id="933e7-139">Connector-specific details</span></span>

<span data-ttu-id="933e7-140">Veja os gatilhos e ações definidos no swagger e também os limites nos [detalhes do conector](/connectors/smtpconnector/).</span><span class="sxs-lookup"><span data-stu-id="933e7-140">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/smtpconnector/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="933e7-141">Mais conectores</span><span class="sxs-lookup"><span data-stu-id="933e7-141">More connectors</span></span>
<span data-ttu-id="933e7-142">Volte para a [Lista de APIs](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="933e7-142">Go back to the [APIs list](apis-list.md).</span></span>