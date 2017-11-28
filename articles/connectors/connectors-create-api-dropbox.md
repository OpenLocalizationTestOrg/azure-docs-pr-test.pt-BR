---
title: "conector de aaaDropbox em aplicativos do Azure lógica | Microsoft Docs"
description: "Crie Aplicativos Lógicos com o serviço de Aplicativo do Azure. Conecte tooDropbox toomanage seus arquivos. Você pode executar várias ações, como carregar, atualizar, obter e excluir arquivos no Dropbox."
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
ms.openlocfilehash: 1f307477836104c0bc0008341604a1400860987f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-dropbox-connector"></a><span data-ttu-id="f7f17-105">Introdução ao conector do Dropbox Olá</span><span class="sxs-lookup"><span data-stu-id="f7f17-105">Get started with hello Dropbox connector</span></span>
<span data-ttu-id="f7f17-106">Conecte tooDropbox toomanage seus arquivos.</span><span class="sxs-lookup"><span data-stu-id="f7f17-106">Connect tooDropbox toomanage your files.</span></span> <span data-ttu-id="f7f17-107">Você pode executar várias ações, como carregar, atualizar, obter e excluir arquivos no Dropbox.</span><span class="sxs-lookup"><span data-stu-id="f7f17-107">You can perform various actions such as upload, update, get, and delete files in Dropbox.</span></span>

<span data-ttu-id="f7f17-108">toouse [qualquer conector](apis-list.md), primeiro é necessário toocreate um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="f7f17-108">toouse [any connector](apis-list.md), you first need toocreate a logic app.</span></span> <span data-ttu-id="f7f17-109">Você pode começar [criando um aplicativo lógico agora](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="f7f17-109">You can get started by [creating a Logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-toodropbox"></a><span data-ttu-id="f7f17-110">Conecte-se tooDropbox</span><span class="sxs-lookup"><span data-stu-id="f7f17-110">Connect tooDropbox</span></span>
<span data-ttu-id="f7f17-111">Antes de sua lógica de aplicativo pode acessar qualquer serviço, primeiro é necessário toocreate um *conexão* toohello service.</span><span class="sxs-lookup"><span data-stu-id="f7f17-111">Before your logic app can access any service, you first need toocreate a *connection* toohello service.</span></span> <span data-ttu-id="f7f17-112">Uma conexão fornece uma conectividade entre um aplicativo lógico e outro serviço.</span><span class="sxs-lookup"><span data-stu-id="f7f17-112">A connection provides connectivity between a logic app and another service.</span></span> <span data-ttu-id="f7f17-113">Por exemplo, em ordem tooconnect tooDropbox, primeiro é necessário um Dropbox *conexão*.</span><span class="sxs-lookup"><span data-stu-id="f7f17-113">For example, in order tooconnect tooDropbox, you first need a Dropbox *connection*.</span></span> <span data-ttu-id="f7f17-114">toocreate uma conexão, você precisaria de credenciais de saudação tooprovide você normalmente usa o serviço de saudação tooaccess para que desejar tooconnect.</span><span class="sxs-lookup"><span data-stu-id="f7f17-114">toocreate a connection, you would need tooprovide hello credentials you normally use tooaccess hello service you wish tooconnect to.</span></span> <span data-ttu-id="f7f17-115">Assim, no exemplo do Dropbox hello, seria necessário Olá credenciais tooyour conta do Dropbox na ordem toocreate Olá conexão tooDropbox.</span><span class="sxs-lookup"><span data-stu-id="f7f17-115">So, in hello Dropbox example, you would need hello credentials tooyour Dropbox account in order toocreate hello connection tooDropbox.</span></span> [<span data-ttu-id="f7f17-116">Saiba mais sobre conexões</span><span class="sxs-lookup"><span data-stu-id="f7f17-116">Learn more about connections</span></span>]()

### <a name="create-a-connection-toodropbox"></a><span data-ttu-id="f7f17-117">Criar uma conexão tooDropbox</span><span class="sxs-lookup"><span data-stu-id="f7f17-117">Create a connection tooDropbox</span></span>
> [!INCLUDE [Steps toocreate a connection tooDropbox](../../includes/connectors-create-api-dropbox.md)]
> 
> 

## <a name="use-a-dropbox-trigger"></a><span data-ttu-id="f7f17-118">Usar um gatilho do Dropbox</span><span class="sxs-lookup"><span data-stu-id="f7f17-118">Use a Dropbox trigger</span></span>
<span data-ttu-id="f7f17-119">Um gatilho é um evento que pode ser o fluxo de trabalho do hello toostart usado definido em um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="f7f17-119">A trigger is an event that can be used toostart hello workflow defined in a logic app.</span></span> <span data-ttu-id="f7f17-120">[Saiba mais sobre gatilhos](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="f7f17-120">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="f7f17-121">Neste exemplo, usaremos Olá **quando um arquivo é criado** gatilho.</span><span class="sxs-lookup"><span data-stu-id="f7f17-121">In this example, we will use hello **When a file is created** trigger.</span></span> <span data-ttu-id="f7f17-122">Quando ocorre esse gatilho, chamaremos Olá **obter conteúdo do arquivo usando o caminho** ação Dropbox.</span><span class="sxs-lookup"><span data-stu-id="f7f17-122">When this trigger occurs, we will call hello **Get file content using path** Dropbox action.</span></span> 

1. <span data-ttu-id="f7f17-123">Digite *dropbox* na caixa de pesquisa Olá no designer de aplicativos lógicos hello, selecione Olá **Dropbox - quando um arquivo é criado** gatilho.</span><span class="sxs-lookup"><span data-stu-id="f7f17-123">Enter *dropbox* in hello search box on hello Logic Apps designer, then select hello **Dropbox - When a file is created** trigger.</span></span>      
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-trigger.PNG)  
2. <span data-ttu-id="f7f17-124">Selecione a pasta de saudação no qual você deseja tootrack criação de arquivos.</span><span class="sxs-lookup"><span data-stu-id="f7f17-124">Select hello folder in which you want tootrack file creation.</span></span> <span data-ttu-id="f7f17-125">Selecione... (identificado na caixa Olá vermelho) e procurar toohello pasta tooselect para gatilho de saudação da entrada.</span><span class="sxs-lookup"><span data-stu-id="f7f17-125">Select ... (identified in hello red box) and browse toohello folder you wish tooselect for hello trigger's input.</span></span>  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-trigger-2.PNG)  

## <a name="use-a-dropbox-action"></a><span data-ttu-id="f7f17-126">Usar uma ação do Dropbox</span><span class="sxs-lookup"><span data-stu-id="f7f17-126">Use a Dropbox action</span></span>
<span data-ttu-id="f7f17-127">Uma ação é uma operação executada pelo fluxo de trabalho Olá definido em um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="f7f17-127">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="f7f17-128">[Saiba mais sobre ações](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="f7f17-128">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

<span data-ttu-id="f7f17-129">Agora que hello gatilho foi adicionado, siga essas etapas tooadd uma ação que receberá o conteúdo do arquivo hello novo.</span><span class="sxs-lookup"><span data-stu-id="f7f17-129">Now that hello trigger has been added, follow these steps tooadd an action that will get hello new file's content.</span></span>

1. <span data-ttu-id="f7f17-130">Selecione **+ nova etapa** ação de saudação tooadd você gostaria que tootake quando um novo arquivo é criado.</span><span class="sxs-lookup"><span data-stu-id="f7f17-130">Select **+ New Step** tooadd hello action you would like tootake when a new file is created.</span></span>  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action.PNG)
2. <span data-ttu-id="f7f17-131">Escolha **Adicionar uma ação**.</span><span class="sxs-lookup"><span data-stu-id="f7f17-131">Select **Add an action**.</span></span> <span data-ttu-id="f7f17-132">Essa caixa de pesquisa de Olá abre onde você pode procurar qualquer ação que você gostaria de tootake.</span><span class="sxs-lookup"><span data-stu-id="f7f17-132">This opens hello search box where you can search for any action you would like tootake.</span></span>  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action-2.PNG)
3. <span data-ttu-id="f7f17-133">Digite *dropbox* toosearch para tooDropbox de ações relacionadas.</span><span class="sxs-lookup"><span data-stu-id="f7f17-133">Enter *dropbox* toosearch for actions related tooDropbox.</span></span>  
4. <span data-ttu-id="f7f17-134">Selecione **Dropbox - obter conteúdo do arquivo usando o caminho** como Olá tootake ação quando um novo arquivo é criado no hello selecionado pasta Dropbox.</span><span class="sxs-lookup"><span data-stu-id="f7f17-134">Select **Dropbox - Get file content using path** as hello action tootake when a new file is created in hello selected Dropbox folder.</span></span> <span data-ttu-id="f7f17-135">bloco de controle de ação de saudação é aberto.</span><span class="sxs-lookup"><span data-stu-id="f7f17-135">hello action control block opens.</span></span> <span data-ttu-id="f7f17-136">Você será solicitado tooauthorize tooaccess de aplicativo sua lógica seu Dropbox conta se você não tiver feito isso anteriormente.</span><span class="sxs-lookup"><span data-stu-id="f7f17-136">You will be prompted tooauthorize your logic app tooaccess your Dropbox account if you have not done so previously.</span></span>  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action-3.PNG)  
5. <span data-ttu-id="f7f17-137">Selecione... (localizado no lado direito de saudação do hello **caminho do arquivo** controle) e procure o caminho do arquivo toohello você gostaria que toouse.</span><span class="sxs-lookup"><span data-stu-id="f7f17-137">Select ... (located at hello right side of hello **File Path** control) and browse toohello file path you would like toouse.</span></span> <span data-ttu-id="f7f17-138">Ou use Olá **caminho do arquivo** token toospeed a sua criação de lógica de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f7f17-138">Or, use hello **file path** token toospeed up your logic app creation.</span></span>  
   ![](../../includes/media/connectors-create-api-dropbox/using-dropbox-action-4.PNG)  
6. <span data-ttu-id="f7f17-139">Salve seu trabalho e criar um novo arquivo no Dropbox tooactivate seu fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="f7f17-139">Save your work and create a new file in Dropbox tooactivate your workflow.</span></span>  

## <a name="connector-specific-details"></a><span data-ttu-id="f7f17-140">Detalhes específicos do conector</span><span class="sxs-lookup"><span data-stu-id="f7f17-140">Connector-specific details</span></span>

<span data-ttu-id="f7f17-141">Exibir quaisquer gatilhos e ações definidas em swagger Olá e também os limites de saudação [detalhes conector](/connectors/dropbox/).</span><span class="sxs-lookup"><span data-stu-id="f7f17-141">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/dropbox/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="f7f17-142">Mais conectores</span><span class="sxs-lookup"><span data-stu-id="f7f17-142">More connectors</span></span>
<span data-ttu-id="f7f17-143">Voltar toohello [lista APIs](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="f7f17-143">Go back toohello [APIs list](apis-list.md).</span></span>
