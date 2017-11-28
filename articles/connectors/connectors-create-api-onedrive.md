---
title: "conector de OneDrive aaaAdd Olá em seus aplicativos lógicos | Microsoft Docs"
description: "Visão geral do conector do OneDrive Olá com parâmetros de API REST"
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
ms.openlocfilehash: 8303794bb3c2844de288f87f40639abb84c160fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-onedrive-connector"></a><span data-ttu-id="715d0-103">Introdução ao conector do OneDrive Olá</span><span class="sxs-lookup"><span data-stu-id="715d0-103">Get started with hello OneDrive connector</span></span>
<span data-ttu-id="715d0-104">Conecte tooOneDrive toomanage seus arquivos, incluindo o carregamento, get, excluir arquivos e muito mais.</span><span class="sxs-lookup"><span data-stu-id="715d0-104">Connect tooOneDrive toomanage your files, including upload, get, delete files, and more.</span></span> 

<span data-ttu-id="715d0-105">Com o OneDrive, você:</span><span class="sxs-lookup"><span data-stu-id="715d0-105">With OneDrive, you:</span></span> 

* <span data-ttu-id="715d0-106">Compile seu fluxo de trabalho armazenando os arquivos no OneDrive ou atualize os arquivos existentes no OneDrive.</span><span class="sxs-lookup"><span data-stu-id="715d0-106">Build your workflow by storing files in OneDrive, or update existing files in OneDrive.</span></span> 
* <span data-ttu-id="715d0-107">Use gatilhos toostart seu fluxo de trabalho quando um arquivo é criado ou atualizado no OneDrive.</span><span class="sxs-lookup"><span data-stu-id="715d0-107">Use triggers toostart your workflow when a file is created or updated within your OneDrive.</span></span>
* <span data-ttu-id="715d0-108">Use ações toocreate um arquivo, excluir um arquivo e muito mais.</span><span class="sxs-lookup"><span data-stu-id="715d0-108">Use actions toocreate a file, delete a file, and more.</span></span> <span data-ttu-id="715d0-109">Por exemplo, quando um novo email do Office 365 for recebido com um anexo (um gatilho), crie um novo arquivo no OneDrive (uma ação).</span><span class="sxs-lookup"><span data-stu-id="715d0-109">For example, when a new Office 365 email is received with an attachment (a trigger), create a new file in OneDrive (an action).</span></span>

<span data-ttu-id="715d0-110">Este tópico mostra como toouse Olá conector OneDrive em um aplicativo lógico e também lista Olá gatilhos e ações.</span><span class="sxs-lookup"><span data-stu-id="715d0-110">This topic shows you how toouse hello OneDrive connector in a logic app, and also lists hello triggers and actions.</span></span>

<span data-ttu-id="715d0-111">toolearn mais sobre aplicativos lógicos, consulte [quais são os aplicativos lógicos](../logic-apps/logic-apps-what-are-logic-apps.md) e [criar um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="715d0-111">toolearn more about Logic Apps, see [What are logic apps](../logic-apps/logic-apps-what-are-logic-apps.md) and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-tooonedrive"></a><span data-ttu-id="715d0-112">Conecte-se tooOneDrive</span><span class="sxs-lookup"><span data-stu-id="715d0-112">Connect tooOneDrive</span></span>
<span data-ttu-id="715d0-113">Antes de sua lógica de aplicativo pode acessar qualquer serviço, você primeiro crie um *conexão* toohello service.</span><span class="sxs-lookup"><span data-stu-id="715d0-113">Before your logic app can access any service, you first create a *connection* toohello service.</span></span> <span data-ttu-id="715d0-114">Uma conexão fornece uma conectividade entre um aplicativo lógico e outro serviço.</span><span class="sxs-lookup"><span data-stu-id="715d0-114">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="715d0-115">Por exemplo, tooconnect tooOneDrive, primeiro é necessário um OneDrive *conexão*.</span><span class="sxs-lookup"><span data-stu-id="715d0-115">For example, tooconnect tooOneDrive, you first need a OneDrive *connection*.</span></span> <span data-ttu-id="715d0-116">toocreate uma conexão, insira as credenciais de saudação você normalmente usa o serviço de saudação tooaccess desejar tooconnect para.</span><span class="sxs-lookup"><span data-stu-id="715d0-116">toocreate a connection, enter hello credentials you normally use tooaccess hello service you wish tooconnect to.</span></span> <span data-ttu-id="715d0-117">Portanto, com o OneDrive, digite conexão de saudação do hello credenciais tooyour OneDrive conta toocreate.</span><span class="sxs-lookup"><span data-stu-id="715d0-117">So, with OneDrive, enter hello credentials tooyour OneDrive account  toocreate hello connection.</span></span>

### <a name="create-hello-connection"></a><span data-ttu-id="715d0-118">Criar conexão Olá</span><span class="sxs-lookup"><span data-stu-id="715d0-118">Create hello connection</span></span>
> [!INCLUDE [Steps toocreate a connection tooOneDrive](../../includes/connectors-create-api-onedrive.md)]
> 
> 

## <a name="use-a-trigger"></a><span data-ttu-id="715d0-119">Usar um gatilho</span><span class="sxs-lookup"><span data-stu-id="715d0-119">Use a trigger</span></span>
<span data-ttu-id="715d0-120">Um gatilho é um evento que pode ser o fluxo de trabalho do hello toostart usado definido em um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="715d0-120">A trigger is an event that can be used toostart hello workflow defined in a logic app.</span></span> <span data-ttu-id="715d0-121">Gatilhos "sondagem" hello serviço em um intervalo e a frequência com que você deseja.</span><span class="sxs-lookup"><span data-stu-id="715d0-121">Triggers "poll" hello service at an interval and frequency that you want.</span></span> <span data-ttu-id="715d0-122">[Saiba mais sobre gatilhos](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="715d0-122">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="715d0-123">No aplicativo de lógica de hello, digite "onedrive" tooget uma lista dos gatilhos hello:</span><span class="sxs-lookup"><span data-stu-id="715d0-123">In hello logic app, type "onedrive" tooget a list of hello triggers:</span></span>  
   
    ![](./media/connectors-create-api-onedrive/onedrive-1.png)
2. <span data-ttu-id="715d0-124">Escolha **Quando um arquivo é modificado**.</span><span class="sxs-lookup"><span data-stu-id="715d0-124">Select **When a file is modified**.</span></span> <span data-ttu-id="715d0-125">Se uma conexão já existir, selecione Olá seletor Mostrar botão tooselect uma pasta.</span><span class="sxs-lookup"><span data-stu-id="715d0-125">If a connection already exists, then select hello Show Picker button tooselect a folder.</span></span>
   
    ![](./media/connectors-create-api-onedrive/sample-folder.png)
   
    <span data-ttu-id="715d0-126">Se você é solicitada toosign em, digite Olá logon na conexão de saudação toocreate detalhes.</span><span class="sxs-lookup"><span data-stu-id="715d0-126">If you are prompted toosign in, then enter hello sign in details toocreate hello connection.</span></span> <span data-ttu-id="715d0-127">[Criar conexão Olá](connectors-create-api-onedrive.md#create-the-connection) neste tópico lista as etapas de saudação.</span><span class="sxs-lookup"><span data-stu-id="715d0-127">[Create hello connection](connectors-create-api-onedrive.md#create-the-connection) in this topic lists hello steps.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="715d0-128">Neste exemplo, Olá lógica aplicativo é executado quando um arquivo na pasta Olá que preferir é atualizado.</span><span class="sxs-lookup"><span data-stu-id="715d0-128">In this example, hello logic app runs when a file in hello folder you choose is updated.</span></span> <span data-ttu-id="715d0-129">resultados de saudação toosee deste gatilho, adicione outra ação que envia um email.</span><span class="sxs-lookup"><span data-stu-id="715d0-129">toosee hello results of this trigger, add another action that sends you an email.</span></span> <span data-ttu-id="715d0-130">Por exemplo, adicionar Olá Outlook do Office 365 *enviar um email* ação que envia email quando um arquivo é atualizado.</span><span class="sxs-lookup"><span data-stu-id="715d0-130">For example, add hello Office 365 Outlook *Send an email* action that emails you when a file is updated.</span></span> 

3. <span data-ttu-id="715d0-131">Selecione Olá **editar** botão e defina Olá **frequência** e **intervalo** valores.</span><span class="sxs-lookup"><span data-stu-id="715d0-131">Select hello **Edit** button and set hello **Frequency** and **Interval** values.</span></span> <span data-ttu-id="715d0-132">Por exemplo, se você quiser Olá gatilho toopoll a cada 15 minutos, em seguida, definir Olá **frequência** muito**minuto**e conjunto hello **intervalo** muito**15**.</span><span class="sxs-lookup"><span data-stu-id="715d0-132">For example, if you want hello trigger toopoll every 15 minutes, then set hello **Frequency** too**Minute**, and set hello **Interval** too**15**.</span></span> 
   
    ![](./media/connectors-create-api-onedrive/trigger-properties.png)
4. <span data-ttu-id="715d0-133">**Salvar** as alterações (canto superior esquerdo da barra de ferramentas de saudação).</span><span class="sxs-lookup"><span data-stu-id="715d0-133">**Save** your changes (top left corner of hello toolbar).</span></span> <span data-ttu-id="715d0-134">Seu aplicativo lógico é salvo e pode ser habilitado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="715d0-134">Your logic app is saved and may be automatically enabled.</span></span>

## <a name="use-an-action"></a><span data-ttu-id="715d0-135">Usar uma ação</span><span class="sxs-lookup"><span data-stu-id="715d0-135">Use an action</span></span>
<span data-ttu-id="715d0-136">Uma ação é uma operação executada pelo fluxo de trabalho Olá definido em um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="715d0-136">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="715d0-137">[Saiba mais sobre ações](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="715d0-137">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

1. <span data-ttu-id="715d0-138">Selecione o sinal de adição hello.</span><span class="sxs-lookup"><span data-stu-id="715d0-138">Select hello plus sign.</span></span> <span data-ttu-id="715d0-139">Consulte várias opções: **adicionar uma ação**, **adicionar uma condição**, ou uma saudação **mais** opções.</span><span class="sxs-lookup"><span data-stu-id="715d0-139">You see several choices: **Add an action**, **Add a condition**, or one of hello **More** options.</span></span>
   
    ![](./media/connectors-create-api-onedrive/add-action.png)
2. <span data-ttu-id="715d0-140">Escolha **Adicionar uma ação**.</span><span class="sxs-lookup"><span data-stu-id="715d0-140">Choose **Add an action**.</span></span>
3. <span data-ttu-id="715d0-141">Na caixa de texto de saudação, digite "onedrive" tooget uma lista de todas as ações disponíveis de saudação.</span><span class="sxs-lookup"><span data-stu-id="715d0-141">In hello text box, type “onedrive” tooget a list of all hello available actions.</span></span>
   
    ![](./media/connectors-create-api-onedrive/onedrive-actions.png) 
4. <span data-ttu-id="715d0-142">Em nosso exemplo, escolha **OneDrive – criar arquivo**.</span><span class="sxs-lookup"><span data-stu-id="715d0-142">In our example, choose **OneDrive - Create file**.</span></span> <span data-ttu-id="715d0-143">Se uma conexão já existir, selecione Olá **caminho da pasta** tooput Olá do arquivo, digite Olá **nome de arquivo**e escolha Olá **conteúdo do arquivo** desejado:</span><span class="sxs-lookup"><span data-stu-id="715d0-143">If a connection already exists, then select hello **Folder Path** tooput hello file, enter hello **File Name**, and choose hello **File Content** you want:</span></span>  
   
    ![](./media/connectors-create-api-onedrive/sample-action.png)
   
    <span data-ttu-id="715d0-144">Se você for solicitado para obter informações de conexão do hello, digite conexão de Olá Olá detalhes toocreate.</span><span class="sxs-lookup"><span data-stu-id="715d0-144">If you are prompted for hello connection information, then enter hello details toocreate hello connection.</span></span> <span data-ttu-id="715d0-145">[Criar conexão Olá](connectors-create-api-onedrive.md#create-the-connection) neste tópico descreve essas propriedades.</span><span class="sxs-lookup"><span data-stu-id="715d0-145">[Create hello connection](connectors-create-api-onedrive.md#create-the-connection) in this topic describes these properties.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="715d0-146">Neste exemplo, podemos criar um novo arquivo em uma pasta do OneDrive.</span><span class="sxs-lookup"><span data-stu-id="715d0-146">In this example, we create a new file in a OneDrive folder.</span></span> <span data-ttu-id="715d0-147">Você pode usar a saída de outro arquivo do gatilho toocreate Olá OneDrive.</span><span class="sxs-lookup"><span data-stu-id="715d0-147">You can use output from another trigger toocreate hello OneDrive file.</span></span> <span data-ttu-id="715d0-148">Por exemplo, adicionar Olá Outlook do Office 365 *quando um novo email chega* gatilho.</span><span class="sxs-lookup"><span data-stu-id="715d0-148">For example, add hello Office 365 Outlook *When a new email arrives* trigger.</span></span> <span data-ttu-id="715d0-149">Em seguida, adicione Olá OneDrive *criar arquivo* ação que usa hello anexos e campos de tipo de conteúdo dentro de um arquivo ForEach toocreate Olá novo no OneDrive.</span><span class="sxs-lookup"><span data-stu-id="715d0-149">Then add hello OneDrive *Create file* action that uses hello Attachments and Content-Type fields within a ForEach toocreate hello new file in OneDrive.</span></span> 
   > 
   > ![](./media/connectors-create-api-onedrive/foreach-action.png)

5. <span data-ttu-id="715d0-150">**Salvar** as alterações (canto superior esquerdo da barra de ferramentas de saudação).</span><span class="sxs-lookup"><span data-stu-id="715d0-150">**Save** your changes (top left corner of hello toolbar).</span></span> <span data-ttu-id="715d0-151">Seu aplicativo lógico é salvo e pode ser habilitado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="715d0-151">Your logic app is saved and may be automatically enabled.</span></span>


## <a name="connector-specific-details"></a><span data-ttu-id="715d0-152">Detalhes específicos do conector</span><span class="sxs-lookup"><span data-stu-id="715d0-152">Connector-specific details</span></span>

<span data-ttu-id="715d0-153">Exibir quaisquer gatilhos e ações definidas em swagger Olá e também os limites de saudação [detalhes conector](/connectors/onedriveconnector/).</span><span class="sxs-lookup"><span data-stu-id="715d0-153">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/onedriveconnector/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="715d0-154">Mais conectores</span><span class="sxs-lookup"><span data-stu-id="715d0-154">More connectors</span></span>
<span data-ttu-id="715d0-155">Voltar toohello [lista APIs](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="715d0-155">Go back toohello [APIs list](apis-list.md).</span></span>
