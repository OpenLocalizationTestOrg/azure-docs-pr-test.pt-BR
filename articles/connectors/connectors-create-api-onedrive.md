---
title: "Adicionar o conector do OneDrive em seus Aplicativos Lógicos | Microsoft Docs"
description: "Visão geral do conector do OneDrive com os parâmetros da API REST"
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 47a8582a-1b1a-4fc3-beb5-97c60c4306fe
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 63bd33bf4e09b98aa53dcfec9fcc4a0109204952
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-onedrive-connector"></a><span data-ttu-id="7225c-103">Introdução ao conector do OneDrive</span><span class="sxs-lookup"><span data-stu-id="7225c-103">Get started with the OneDrive connector</span></span>
<span data-ttu-id="7225c-104">Conecte-se ao OneDrive para gerenciar seus arquivos, incluindo carregar, obter, excluir arquivos e muito mais.</span><span class="sxs-lookup"><span data-stu-id="7225c-104">Connect to OneDrive to manage your files, including upload, get, delete files, and more.</span></span> 

<span data-ttu-id="7225c-105">Com o OneDrive, você:</span><span class="sxs-lookup"><span data-stu-id="7225c-105">With OneDrive, you:</span></span> 

* <span data-ttu-id="7225c-106">Compile seu fluxo de trabalho armazenando os arquivos no OneDrive ou atualize os arquivos existentes no OneDrive.</span><span class="sxs-lookup"><span data-stu-id="7225c-106">Build your workflow by storing files in OneDrive, or update existing files in OneDrive.</span></span> 
* <span data-ttu-id="7225c-107">Use gatilhos para iniciar o fluxo de trabalho quando um arquivo é criado ou atualizado em seu OneDrive.</span><span class="sxs-lookup"><span data-stu-id="7225c-107">Use triggers to start your workflow when a file is created or updated within your OneDrive.</span></span>
* <span data-ttu-id="7225c-108">Usar ações para criar um arquivo, excluir um arquivo e muito mais.</span><span class="sxs-lookup"><span data-stu-id="7225c-108">Use actions to create a file, delete a file, and more.</span></span> <span data-ttu-id="7225c-109">Por exemplo, quando um novo email do Office 365 for recebido com um anexo (um gatilho), crie um novo arquivo no OneDrive (uma ação).</span><span class="sxs-lookup"><span data-stu-id="7225c-109">For example, when a new Office 365 email is received with an attachment (a trigger), create a new file in OneDrive (an action).</span></span>

<span data-ttu-id="7225c-110">Este tópico mostra como usar o conector do OneDrive em um aplicativo lógico, além de listar os gatilhos e as ações.</span><span class="sxs-lookup"><span data-stu-id="7225c-110">This topic shows you how to use the OneDrive connector in a logic app, and also lists the triggers and actions.</span></span>

<span data-ttu-id="7225c-111">Para saber mais sobre os Aplicativos Lógicos, consulte [O que são aplicativos lógicos](../logic-apps/logic-apps-what-are-logic-apps.md) e [Criar um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="7225c-111">To learn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-onedrive"></a><span data-ttu-id="7225c-112">Conectar o OneDrive</span><span class="sxs-lookup"><span data-stu-id="7225c-112">Connect to OneDrive</span></span>
<span data-ttu-id="7225c-113">Antes do aplicativo lógico poder acessar qualquer serviço, primeiro crie uma *conexão* com o serviço.</span><span class="sxs-lookup"><span data-stu-id="7225c-113">Before your logic app can access any service, you first create a *connection* to the service.</span></span> <span data-ttu-id="7225c-114">Uma conexão fornece uma conectividade entre um aplicativo lógico e outro serviço.</span><span class="sxs-lookup"><span data-stu-id="7225c-114">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="7225c-115">Por exemplo, para se conectar ao OneDrive, primeiramente é necessária uma *conexão* do OneDrive.</span><span class="sxs-lookup"><span data-stu-id="7225c-115">For example, to connect to OneDrive, you first need a OneDrive *connection*.</span></span> <span data-ttu-id="7225c-116">Para criar uma conexão, insira as credenciais que você normalmente usa para acessar o serviço ao qual deseja conectar-se.</span><span class="sxs-lookup"><span data-stu-id="7225c-116">To create a connection, enter the credentials you normally use to access the service you wish to connect to.</span></span> <span data-ttu-id="7225c-117">Assim, com o OneDrive, insira as credenciais de sua conta OneDrive para criar a conexão.</span><span class="sxs-lookup"><span data-stu-id="7225c-117">So, with OneDrive, enter the credentials to your OneDrive account  to create the connection.</span></span>

### <a name="create-the-connection"></a><span data-ttu-id="7225c-118">Criar a conexão</span><span class="sxs-lookup"><span data-stu-id="7225c-118">Create the connection</span></span>
> [!INCLUDE [Steps to create a connection to OneDrive](../../includes/connectors-create-api-onedrive.md)]
> 
> 

## <a name="use-a-trigger"></a><span data-ttu-id="7225c-119">Usar um gatilho</span><span class="sxs-lookup"><span data-stu-id="7225c-119">Use a trigger</span></span>
<span data-ttu-id="7225c-120">Um gatilho é um evento que pode ser usado para iniciar o fluxo de trabalho definido em um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="7225c-120">A trigger is an event that can be used to start the workflow defined in a logic app.</span></span> <span data-ttu-id="7225c-121">Gatilhos "sondam" o serviço no intervalo e na frequência desejados.</span><span class="sxs-lookup"><span data-stu-id="7225c-121">Triggers "poll" the service at an interval and frequency that you want.</span></span> <span data-ttu-id="7225c-122">[Saiba mais sobre gatilhos](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="7225c-122">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="7225c-123">No aplicativo lógico, digite "onedrive" para obter uma lista de gatilhos:</span><span class="sxs-lookup"><span data-stu-id="7225c-123">In the logic app, type "onedrive" to get a list of the triggers:</span></span>  
   
    ![](./media/connectors-create-api-onedrive/onedrive-1.png)
2. <span data-ttu-id="7225c-124">Escolha **Quando um arquivo é modificado**.</span><span class="sxs-lookup"><span data-stu-id="7225c-124">Select **When a file is modified**.</span></span> <span data-ttu-id="7225c-125">Se já existe uma conexão, escolha o botão Mostrar Seletor para selecionar uma pasta.</span><span class="sxs-lookup"><span data-stu-id="7225c-125">If a connection already exists, then select the Show Picker button to select a folder.</span></span>
   
    ![](./media/connectors-create-api-onedrive/sample-folder.png)
   
    <span data-ttu-id="7225c-126">Se você for solicitado a entrar, insira os detalhes do logon para criar a conexão.</span><span class="sxs-lookup"><span data-stu-id="7225c-126">If you are prompted to sign in, then enter the sign in details to create the connection.</span></span> <span data-ttu-id="7225c-127">[Criar a conexão](connectors-create-api-onedrive.md#create-the-connection) neste tópico lista as etapas.</span><span class="sxs-lookup"><span data-stu-id="7225c-127">[Create the connection](connectors-create-api-onedrive.md#create-the-connection) in this topic lists the steps.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="7225c-128">Neste exemplo, o aplicativo lógico é executado quando um arquivo na pasta escolhida é atualizado.</span><span class="sxs-lookup"><span data-stu-id="7225c-128">In this example, the logic app runs when a file in the folder you choose is updated.</span></span> <span data-ttu-id="7225c-129">Para ver os resultados deste gatilho, adicione outra ação que envia um email.</span><span class="sxs-lookup"><span data-stu-id="7225c-129">To see the results of this trigger, add another action that sends you an email.</span></span> <span data-ttu-id="7225c-130">Por exemplo, adicione a ação *Enviar um email* do Outlook do Office 365 que envia um email para você quando um arquivo é atualizado.</span><span class="sxs-lookup"><span data-stu-id="7225c-130">For example, add the Office 365 Outlook *Send an email* action that emails you when a file is updated.</span></span> 

3. <span data-ttu-id="7225c-131">Selecione o botão **Editar** e defina os valores **Frequência** e **Intervalo**.</span><span class="sxs-lookup"><span data-stu-id="7225c-131">Select the **Edit** button and set the **Frequency** and **Interval** values.</span></span> <span data-ttu-id="7225c-132">Por exemplo, se você quiser que o gatilho faça uma sondagem a cada 15 minutos, defina a **Frequência** como **Minuto** e **Intervalo** como **15**.</span><span class="sxs-lookup"><span data-stu-id="7225c-132">For example, if you want the trigger to poll every 15 minutes, then set the **Frequency** to **Minute**, and set the **Interval** to **15**.</span></span> 
   
    ![](./media/connectors-create-api-onedrive/trigger-properties.png)
4. <span data-ttu-id="7225c-133">**Salve** as alterações (canto superior esquerdo da barra de ferramentas).</span><span class="sxs-lookup"><span data-stu-id="7225c-133">**Save** your changes (top left corner of the toolbar).</span></span> <span data-ttu-id="7225c-134">Seu aplicativo lógico é salvo e pode ser habilitado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="7225c-134">Your logic app is saved and may be automatically enabled.</span></span>

## <a name="use-an-action"></a><span data-ttu-id="7225c-135">Usar uma ação</span><span class="sxs-lookup"><span data-stu-id="7225c-135">Use an action</span></span>
<span data-ttu-id="7225c-136">Uma ação é uma operação executada pelo fluxo de trabalho definido em um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="7225c-136">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="7225c-137">[Saiba mais sobre ações](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="7225c-137">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="7225c-138">Selecione o sinal de mais.</span><span class="sxs-lookup"><span data-stu-id="7225c-138">Select the plus sign.</span></span> <span data-ttu-id="7225c-139">Você tem várias opções: **adicionar uma ação**, **adicionar uma condição** ou uma das opções **Mais**.</span><span class="sxs-lookup"><span data-stu-id="7225c-139">You see several choices: **Add an action**, **Add a condition**, or one of the **More** options.</span></span>
   
    ![](./media/connectors-create-api-onedrive/add-action.png)
2. <span data-ttu-id="7225c-140">Escolha **Adicionar uma ação**.</span><span class="sxs-lookup"><span data-stu-id="7225c-140">Choose **Add an action**.</span></span>
3. <span data-ttu-id="7225c-141">Na caixa de texto, digite "onedrive" para obter uma lista de todas as ações disponíveis.</span><span class="sxs-lookup"><span data-stu-id="7225c-141">In the text box, type “onedrive” to get a list of all the available actions.</span></span>
   
    ![](./media/connectors-create-api-onedrive/onedrive-actions.png) 
4. <span data-ttu-id="7225c-142">Em nosso exemplo, escolha **OneDrive – criar arquivo**.</span><span class="sxs-lookup"><span data-stu-id="7225c-142">In our example, choose **OneDrive - Create file**.</span></span> <span data-ttu-id="7225c-143">Se já existir uma conexão, escolha o **Caminho da Pasta** para colocar o arquivo, insira o **Nome do Arquivo** e escolha o **Conteúdo do Arquivo** desejado:</span><span class="sxs-lookup"><span data-stu-id="7225c-143">If a connection already exists, then select the **Folder Path** to put the file, enter the **File Name**, and choose the **File Content** you want:</span></span>  
   
    ![](./media/connectors-create-api-onedrive/sample-action.png)
   
    <span data-ttu-id="7225c-144">Se as informações de conexão forem solicitadas, insira os detalhes para criar a conexão.</span><span class="sxs-lookup"><span data-stu-id="7225c-144">If you are prompted for the connection information, then enter the details to create the connection.</span></span> <span data-ttu-id="7225c-145">[Criar a conexão](connectors-create-api-onedrive.md#create-the-connection) neste tópico descreve estas propriedades.</span><span class="sxs-lookup"><span data-stu-id="7225c-145">[Create the connection](connectors-create-api-onedrive.md#create-the-connection) in this topic describes these properties.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="7225c-146">Neste exemplo, podemos criar um novo arquivo em uma pasta do OneDrive.</span><span class="sxs-lookup"><span data-stu-id="7225c-146">In this example, we create a new file in a OneDrive folder.</span></span> <span data-ttu-id="7225c-147">Você pode usar a saída de outro gatilho para criar o arquivo do OneDrive.</span><span class="sxs-lookup"><span data-stu-id="7225c-147">You can use output from another trigger to create the OneDrive file.</span></span> <span data-ttu-id="7225c-148">Por exemplo, adicione o gatilho *Quando um novo email chegar* do Outlook do Office 365.</span><span class="sxs-lookup"><span data-stu-id="7225c-148">For example, add the Office 365 Outlook *When a new email arrives* trigger.</span></span> <span data-ttu-id="7225c-149">Em seguida, adicione a ação *Criar arquivo* do OneDrive, que usa os campos Anexos e Tipo de Conteúdo em um ForEach para criar o novo arquivo no OneDrive.</span><span class="sxs-lookup"><span data-stu-id="7225c-149">Then add the OneDrive *Create file* action that uses the Attachments and Content-Type fields within a ForEach to create the new file in OneDrive.</span></span> 
   > 
   > ![](./media/connectors-create-api-onedrive/foreach-action.png)

5. <span data-ttu-id="7225c-150">**Salve** as alterações (canto superior esquerdo da barra de ferramentas).</span><span class="sxs-lookup"><span data-stu-id="7225c-150">**Save** your changes (top left corner of the toolbar).</span></span> <span data-ttu-id="7225c-151">Seu aplicativo lógico é salvo e pode ser habilitado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="7225c-151">Your logic app is saved and may be automatically enabled.</span></span>


## <a name="connector-specific-details"></a><span data-ttu-id="7225c-152">Detalhes específicos do conector</span><span class="sxs-lookup"><span data-stu-id="7225c-152">Connector-specific details</span></span>

<span data-ttu-id="7225c-153">Veja os gatilhos e ações definidos no swagger e também os limites nos [detalhes do conector](/connectors/onedriveconnector/).</span><span class="sxs-lookup"><span data-stu-id="7225c-153">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/onedriveconnector/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="7225c-154">Mais conectores</span><span class="sxs-lookup"><span data-stu-id="7225c-154">More connectors</span></span>
<span data-ttu-id="7225c-155">Volte para a [Lista de APIs](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="7225c-155">Go back to the [APIs list](apis-list.md).</span></span>