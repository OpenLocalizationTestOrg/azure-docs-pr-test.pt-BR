---
title: "Conector do Dropbox no Aplicativo Lógico do Azure | Microsoft Docs"
description: "Crie Aplicativos Lógicos com o serviço de Aplicativo do Azure. Conecte-se ao Dropbox para gerenciar seus arquivos. Você pode executar várias ações, como carregar, atualizar, obter e excluir arquivos no Dropbox."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: cb0ae033-aba7-4ac9-beaa-be561a0f0cac
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/15/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 0d09580c60fd620811b539147439d0922839fe7e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-dropbox-connector"></a><span data-ttu-id="e7bab-105">Introdução ao conector do Dropbox</span><span class="sxs-lookup"><span data-stu-id="e7bab-105">Get started with the Dropbox connector</span></span>
<span data-ttu-id="e7bab-106">Conecte-se ao Dropbox para gerenciar seus arquivos.</span><span class="sxs-lookup"><span data-stu-id="e7bab-106">Connect to Dropbox to manage your files.</span></span> <span data-ttu-id="e7bab-107">Você pode executar várias ações, como carregar, atualizar, obter e excluir arquivos no Dropbox.</span><span class="sxs-lookup"><span data-stu-id="e7bab-107">You can perform various actions such as upload, update, get, and delete files in Dropbox.</span></span>

<span data-ttu-id="e7bab-108">Para usar [qualquer conector](apis-list.md), primeiro é preciso criar um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="e7bab-108">To use [any connector](apis-list.md), you first need to create a logic app.</span></span> <span data-ttu-id="e7bab-109">Você pode começar [criando um aplicativo lógico agora](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="e7bab-109">You can get started by [creating a Logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-dropbox"></a><span data-ttu-id="e7bab-110">Conectar-se ao Dropbox</span><span class="sxs-lookup"><span data-stu-id="e7bab-110">Connect to Dropbox</span></span>
<span data-ttu-id="e7bab-111">Para que o aplicativo lógico possa acessar qualquer serviço, crie primeiro uma *conexão* com o serviço.</span><span class="sxs-lookup"><span data-stu-id="e7bab-111">Before your logic app can access any service, you first need to create a *connection* to the service.</span></span> <span data-ttu-id="e7bab-112">Uma conexão fornece uma conectividade entre um aplicativo lógico e outro serviço.</span><span class="sxs-lookup"><span data-stu-id="e7bab-112">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="e7bab-113">Por exemplo, para se conectar ao Dropbox, é preciso ter uma *conexão* com o Dropbox.</span><span class="sxs-lookup"><span data-stu-id="e7bab-113">For example, in order to connect to Dropbox, you first need a Dropbox *connection*.</span></span> <span data-ttu-id="e7bab-114">Para criar uma conexão, é preciso fornecer as credenciais normalmente usadas para acessar o serviço ao qual você deseja se conectar.</span><span class="sxs-lookup"><span data-stu-id="e7bab-114">To create a connection, you would need to provide the credentials you normally use to access the service you wish to connect to.</span></span> <span data-ttu-id="e7bab-115">Desse modo, no exemplo do Dropbox, são necessárias as credenciais da sua conta no Dropbox para criar a conexão com o Dropbox.</span><span class="sxs-lookup"><span data-stu-id="e7bab-115">So, in the Dropbox example, you would need the credentials to your Dropbox account in order to create the connection to Dropbox.</span></span> [<span data-ttu-id="e7bab-116">Saiba mais sobre conexões</span><span class="sxs-lookup"><span data-stu-id="e7bab-116">Learn more about connections</span></span>]()

### <a name="create-a-connection-to-dropbox"></a><span data-ttu-id="e7bab-117">Criar uma conexão com o Dropbox</span><span class="sxs-lookup"><span data-stu-id="e7bab-117">Create a connection to Dropbox</span></span>
> [!INCLUDE [Steps to create a connection to Dropbox](../../includes/connectors-create-api-dropbox.md)]
> 
> 

## <a name="use-a-dropbox-trigger"></a><span data-ttu-id="e7bab-118">Usar um gatilho do Dropbox</span><span class="sxs-lookup"><span data-stu-id="e7bab-118">Use a Dropbox trigger</span></span>
<span data-ttu-id="e7bab-119">Um gatilho é um evento que pode ser usado para iniciar o fluxo de trabalho definido em um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="e7bab-119">A trigger is an event that can be used to start the workflow defined in a logic app.</span></span> <span data-ttu-id="e7bab-120">[Saiba mais sobre gatilhos](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="e7bab-120">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="e7bab-121">Neste exemplo, usaremos o gatilho **Quando um arquivo é criado**.</span><span class="sxs-lookup"><span data-stu-id="e7bab-121">In this example, we will use the **When a file is created** trigger.</span></span> <span data-ttu-id="e7bab-122">Quando esse gatilho ocorrer, chamaremos a ação do Dropbox **Obter conteúdo do arquivo usando o caminho**.</span><span class="sxs-lookup"><span data-stu-id="e7bab-122">When this trigger occurs, we will call the **Get file content using path** Dropbox action.</span></span> 

1. <span data-ttu-id="e7bab-123">Insira *dropbox* na caixa de pesquisa no designer de Aplicativos Lógicos e selecione o gatilho **Dropbox - Quando um arquivo é criado**.</span><span class="sxs-lookup"><span data-stu-id="e7bab-123">Enter *dropbox* in the search box on the Logic Apps designer, then select the **Dropbox - When a file is created** trigger.</span></span>      
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-trigger.PNG)  
2. <span data-ttu-id="e7bab-124">Escolha a pasta na qual você deseja controlar a criação do arquivo.</span><span class="sxs-lookup"><span data-stu-id="e7bab-124">Select the folder in which you want to track file creation.</span></span> <span data-ttu-id="e7bab-125">Escolha ... (identificado na caixa vermelha) e navegue até a pasta que deseja selecionar para entrada do gatilho.</span><span class="sxs-lookup"><span data-stu-id="e7bab-125">Select ... (identified in the red box) and browse to the folder you wish to select for the trigger's input.</span></span>  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-trigger-2.PNG)  

## <a name="use-a-dropbox-action"></a><span data-ttu-id="e7bab-126">Usar uma ação do Dropbox</span><span class="sxs-lookup"><span data-stu-id="e7bab-126">Use a Dropbox action</span></span>
<span data-ttu-id="e7bab-127">Uma ação é uma operação executada pelo fluxo de trabalho definido em um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="e7bab-127">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="e7bab-128">[Saiba mais sobre ações](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="e7bab-128">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="e7bab-129">Agora que o gatilho foi adicionado, siga estas etapas para adicionar uma ação que obterá o novo conteúdo do arquivo.</span><span class="sxs-lookup"><span data-stu-id="e7bab-129">Now that the trigger has been added, follow these steps to add an action that will get the new file's content.</span></span>

1. <span data-ttu-id="e7bab-130">Escolha **+ Nova Etapa** para adicionar a ação que deseja executar quando um novo arquivo for criado.</span><span class="sxs-lookup"><span data-stu-id="e7bab-130">Select **+ New Step** to add the action you would like to take when a new file is created.</span></span>  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action.PNG)
2. <span data-ttu-id="e7bab-131">Escolha **Adicionar uma ação**.</span><span class="sxs-lookup"><span data-stu-id="e7bab-131">Select **Add an action**.</span></span> <span data-ttu-id="e7bab-132">Isso abre a caixa de pesquisa, na qual é possível procurar qualquer ação que você deseja realizar.</span><span class="sxs-lookup"><span data-stu-id="e7bab-132">This opens the search box where you can search for any action you would like to take.</span></span>  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action-2.PNG)
3. <span data-ttu-id="e7bab-133">Insira *dropbox* para pesquisar as ações relacionadas ao Dropbox.</span><span class="sxs-lookup"><span data-stu-id="e7bab-133">Enter *dropbox* to search for actions related to Dropbox.</span></span>  
4. <span data-ttu-id="e7bab-134">Escolha **Dropbox - Obter conteúdo do arquivo usando o caminho** como a ação a ser executada quando um novo arquivo for criado na pasta Dropbox selecionada.</span><span class="sxs-lookup"><span data-stu-id="e7bab-134">Select **Dropbox - Get file content using path** as the action to take when a new file is created in the selected Dropbox folder.</span></span> <span data-ttu-id="e7bab-135">O bloco de controle de ação é aberto.</span><span class="sxs-lookup"><span data-stu-id="e7bab-135">The action control block opens.</span></span> <span data-ttu-id="e7bab-136">Será solicitado que você autorize o aplicativo lógico a acessar sua conta no Dropbox, caso não tenha feito isso antes.</span><span class="sxs-lookup"><span data-stu-id="e7bab-136">You will be prompted to authorize your logic app to access your Dropbox account if you have not done so previously.</span></span>  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action-3.PNG)  
5. <span data-ttu-id="e7bab-137">Escolha ... (localizado no lado direito do controle **Caminho do Arquivo**) e navegue até o caminho do arquivo que deseja usar.</span><span class="sxs-lookup"><span data-stu-id="e7bab-137">Select ... (located at the right side of the **File Path** control) and browse to the file path you would like to use.</span></span> <span data-ttu-id="e7bab-138">Ou use o token do **caminho do arquivo** para agilizar a criação do aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="e7bab-138">Or, use the **file path** token to speed up your logic app creation.</span></span>  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action-4.PNG)  
6. <span data-ttu-id="e7bab-139">Salve seu trabalho e crie um novo arquivo no Dropbox para ativar o fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="e7bab-139">Save your work and create a new file in Dropbox to activate your workflow.</span></span>  

## <a name="connector-specific-details"></a><span data-ttu-id="e7bab-140">Detalhes específicos do conector</span><span class="sxs-lookup"><span data-stu-id="e7bab-140">Connector-specific details</span></span>

<span data-ttu-id="e7bab-141">Veja os gatilhos e ações definidos no swagger e também os limites nos [detalhes do conector](/connectors/dropbox/).</span><span class="sxs-lookup"><span data-stu-id="e7bab-141">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/dropbox/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="e7bab-142">Mais conectores</span><span class="sxs-lookup"><span data-stu-id="e7bab-142">More connectors</span></span>
<span data-ttu-id="e7bab-143">Volte para a [Lista de APIs](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="e7bab-143">Go back to the [APIs list](apis-list.md).</span></span>