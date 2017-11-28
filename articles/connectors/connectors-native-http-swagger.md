---
title: "pontos de extremidade REST de aaaCall com HTTP + Swagger connector para os aplicativos lógicos do Azure | Microsoft Docs"
description: "Conectar a pontos de extremidade de tooREST de aplicativos lógicos por meio de Swagger com Olá HTTP + Swagger conector"
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
tags: connectors
ms.assetid: eccfd87c-c5fe-4cf7-b564-9752775fd667
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: jehollan; LADocs
ms.openlocfilehash: baaa57689ff41fcd052f9d86086e36619ddec46e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-http--swagger-action"></a><span data-ttu-id="ca9b2-103">Introdução ao Olá HTTP + Swagger ação</span><span class="sxs-lookup"><span data-stu-id="ca9b2-103">Get started with hello HTTP + Swagger action</span></span>

<span data-ttu-id="ca9b2-104">Você pode criar um ponto de extremidade do conector de primeira classe tooany REST por meio de um [Swagger documento](https://swagger.io) quando você usa Olá HTTP + Swagger ação em um fluxo de trabalho de sua lógica do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ca9b2-104">You can create a first-class connector tooany REST endpoint through a [Swagger document](https://swagger.io) when you use hello HTTP + Swagger action in your logic app workflow.</span></span> <span data-ttu-id="ca9b2-105">Você também pode estender lógica aplicativos toocall qualquer ponto de extremidade REST com uma experiência de Designer do aplicativo de lógica de primeira classe.</span><span class="sxs-lookup"><span data-stu-id="ca9b2-105">You can also extend logic apps toocall any REST endpoint with a first-class Logic App Designer experience.</span></span>

<span data-ttu-id="ca9b2-106">toolearn como aplicativos de lógica de toocreate com conectores, consulte [criar um novo aplicativo de lógica](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="ca9b2-106">toolearn how toocreate logic apps with connectors, see [Create a new logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-http--swagger-as-a-trigger-or-an-action"></a><span data-ttu-id="ca9b2-107">Usar HTTP + Swagger como um gatilho ou uma ação</span><span class="sxs-lookup"><span data-stu-id="ca9b2-107">Use HTTP + Swagger as a trigger or an action</span></span>

<span data-ttu-id="ca9b2-108">Olá HTTP + trabalho de gatilho e a ação de Swagger Olá mesmo como Olá [ação HTTP](connectors-native-http.md) mas fornecer uma melhor experiência no Designer de lógica do aplicativo, expondo a estrutura de saudação API e saídas de saudação [Swagger metadados](https://swagger.io) .</span><span class="sxs-lookup"><span data-stu-id="ca9b2-108">hello HTTP + Swagger trigger and action work hello same as hello [HTTP action](connectors-native-http.md) but provide a better experience in Logic App Designer by exposing hello API structure and outputs from hello [Swagger metadata](https://swagger.io).</span></span> <span data-ttu-id="ca9b2-109">Você também pode usar Olá HTTP + Swagger conector como um disparador.</span><span class="sxs-lookup"><span data-stu-id="ca9b2-109">You can also use hello HTTP + Swagger connector as a trigger.</span></span> <span data-ttu-id="ca9b2-110">Se você quiser tooimplement um gatilho de sondagem, seguem o padrão de sondagem de saudação que é descrita em [criar toocall APIs personalizada outras APIs, serviços e sistemas de aplicativos lógicos](../logic-apps/logic-apps-create-api-app.md#polling-triggers).</span><span class="sxs-lookup"><span data-stu-id="ca9b2-110">If you want tooimplement a polling trigger, follow hello polling pattern that's described in [Create custom APIs toocall other APIs, services, and systems from logic apps](../logic-apps/logic-apps-create-api-app.md#polling-triggers).</span></span>

<span data-ttu-id="ca9b2-111">Saiba mais sobre [gatilhos e ações de aplicativo lógico](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ca9b2-111">Learn more about [logic app triggers and actions](connectors-overview.md).</span></span>

<span data-ttu-id="ca9b2-112">Aqui está um exemplo de como toouse Olá HTTP + Swagger operação como uma ação em um fluxo de trabalho em um aplicativo de lógica.</span><span class="sxs-lookup"><span data-stu-id="ca9b2-112">Here's an example of how toouse hello HTTP + Swagger operation as an action in a workflow in a logic app.</span></span>

1. <span data-ttu-id="ca9b2-113">Selecione Olá **nova etapa** botão.</span><span class="sxs-lookup"><span data-stu-id="ca9b2-113">Select hello **New Step** button.</span></span>
2. <span data-ttu-id="ca9b2-114">Escolha **Adicionar uma ação**.</span><span class="sxs-lookup"><span data-stu-id="ca9b2-114">Select **Add an action**.</span></span>
3. <span data-ttu-id="ca9b2-115">Na caixa de pesquisa de ação hello, digite **swagger** Olá toolist HTTP + Swagger ação.</span><span class="sxs-lookup"><span data-stu-id="ca9b2-115">In hello action search box, type **swagger** toolist hello HTTP + Swagger action.</span></span>
   
    ![Selecionar ação de HTTP + Swagger](./media/connectors-native-http-swagger/using-action-1.png)
4. <span data-ttu-id="ca9b2-117">Digite a URL para um documento de Swagger hello:</span><span class="sxs-lookup"><span data-stu-id="ca9b2-117">Type hello URL for a Swagger document:</span></span>
   
   * <span data-ttu-id="ca9b2-118">toowork de saudação lógica de aplicativo Designer, Olá URL deve ser um ponto de extremidade HTTPS e tiver habilitado CORS.</span><span class="sxs-lookup"><span data-stu-id="ca9b2-118">toowork from hello Logic App Designer, hello URL must be an HTTPS endpoint and have CORS enabled.</span></span>
   * <span data-ttu-id="ca9b2-119">Se o documento de Swagger de saudação não atender a esse requisito, você pode usar [armazenamento do Azure com CORS habilitado](#hosting-swagger-from-storage) toostore documento de saudação.</span><span class="sxs-lookup"><span data-stu-id="ca9b2-119">If hello Swagger document doesn't meet this requirement, you can use [Azure Storage with CORS enabled](#hosting-swagger-from-storage) toostore hello document.</span></span>
5. <span data-ttu-id="ca9b2-120">Clique em **próximo** tooread e renderização de Olá Swagger documento.</span><span class="sxs-lookup"><span data-stu-id="ca9b2-120">Click **Next** tooread and render from hello Swagger document.</span></span>
6. <span data-ttu-id="ca9b2-121">Adicione quaisquer parâmetros que são necessários para a chamada de saudação HTTP.</span><span class="sxs-lookup"><span data-stu-id="ca9b2-121">Add in any parameters that are required for hello HTTP call.</span></span>
   
    ![Concluir a ação HTTP](./media/connectors-native-http-swagger/using-action-2.png)
7. <span data-ttu-id="ca9b2-123">toosave e publicar seu aplicativo lógico, clique em **salvar** na barra de ferramentas do designer.</span><span class="sxs-lookup"><span data-stu-id="ca9b2-123">toosave and publish your logic app, click **Save** on designer toolbar.</span></span>

### <a name="host-swagger-from-azure-storage"></a><span data-ttu-id="ca9b2-124">Hospedar o Swagger do Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="ca9b2-124">Host Swagger from Azure Storage</span></span>
<span data-ttu-id="ca9b2-125">Talvez você queira tooreference um documento de Swagger que não está hospedado ou que não atende aos requisitos de segurança e entre origens de saudação do designer de saudação.</span><span class="sxs-lookup"><span data-stu-id="ca9b2-125">You might want tooreference a Swagger document that's not hosted, or that doesn't meet hello security and cross-origin requirements for hello designer.</span></span> <span data-ttu-id="ca9b2-126">tooresolve esse problema, você pode armazenar o documento de Swagger Olá no armazenamento do Azure e habilitar CORS tooreference Olá documentos.</span><span class="sxs-lookup"><span data-stu-id="ca9b2-126">tooresolve this issue, you can store hello Swagger document in Azure Storage and enable CORS tooreference hello document.</span></span>  

<span data-ttu-id="ca9b2-127">Aqui estão Olá etapas toocreate, configurar e armazenar documentos Swagger no armazenamento do Azure:</span><span class="sxs-lookup"><span data-stu-id="ca9b2-127">Here are hello steps toocreate, configure, and store Swagger documents in Azure Storage:</span></span>

1. <span data-ttu-id="ca9b2-128">[Crie uma conta de armazenamento do Azure com o armazenamento de Blobs do Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="ca9b2-128">[Create an Azure storage account with Azure Blob storage](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="ca9b2-129">tooperform essa etapa, defina as permissões muito**acesso público**.</span><span class="sxs-lookup"><span data-stu-id="ca9b2-129">tooperform this step, set permissions too**Public Access**.</span></span>

2. <span data-ttu-id="ca9b2-130">Habilite o CORS no blob de saudação.</span><span class="sxs-lookup"><span data-stu-id="ca9b2-130">Enable CORS on hello blob.</span></span> 

   <span data-ttu-id="ca9b2-131">tooautomatically definir essa configuração, você pode usar [este script do PowerShell](https://github.com/logicappsio/EnableCORSAzureBlob/blob/master/EnableCORSAzureBlob.ps1).</span><span class="sxs-lookup"><span data-stu-id="ca9b2-131">tooautomatically configure this setting, you can use [this PowerShell script](https://github.com/logicappsio/EnableCORSAzureBlob/blob/master/EnableCORSAzureBlob.ps1).</span></span>

3. <span data-ttu-id="ca9b2-132">Carregar um blob de toohello de arquivo hello Swagger.</span><span class="sxs-lookup"><span data-stu-id="ca9b2-132">Upload hello Swagger file toohello blob.</span></span> 

   <span data-ttu-id="ca9b2-133">Você pode executar essa etapa de saudação [portal do Azure](https://portal.azure.com) ou de uma ferramenta como [Azure Storage Explorer](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="ca9b2-133">You can perform this step from hello [Azure portal](https://portal.azure.com) or from a tool like [Azure Storage Explorer](http://storageexplorer.com/).</span></span>

4. <span data-ttu-id="ca9b2-134">Fazer referência a um documento de toohello link HTTPS no armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="ca9b2-134">Reference an HTTPS link toohello document in Azure Blob storage.</span></span> 

   <span data-ttu-id="ca9b2-135">link de saudação usa este formato:</span><span class="sxs-lookup"><span data-stu-id="ca9b2-135">hello link uses this format:</span></span>

   `https://*storageAccountName*.blob.core.windows.net/*container*/*filename*`

## <a name="technical-details"></a><span data-ttu-id="ca9b2-136">Detalhes técnicos</span><span class="sxs-lookup"><span data-stu-id="ca9b2-136">Technical details</span></span>
<span data-ttu-id="ca9b2-137">A seguir é Olá detalhes Olá gatilhos e ações que este HTTP + Swagger conector dá suporte a.</span><span class="sxs-lookup"><span data-stu-id="ca9b2-137">Following are hello details for hello triggers and actions that this HTTP + Swagger connector supports.</span></span>

## <a name="http--swagger-triggers"></a><span data-ttu-id="ca9b2-138">Gatilhos de HTTP + Swagger</span><span class="sxs-lookup"><span data-stu-id="ca9b2-138">HTTP + Swagger triggers</span></span>
<span data-ttu-id="ca9b2-139">Um gatilho é um evento que pode ser usado toostart Olá fluxo de trabalho é definido em um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="ca9b2-139">A trigger is an event that can be used toostart hello workflow that's defined in a logic app.</span></span> [<span data-ttu-id="ca9b2-140">Saiba mais sobre gatilhos.</span><span class="sxs-lookup"><span data-stu-id="ca9b2-140">Learn more about triggers.</span></span>](connectors-overview.md) <span data-ttu-id="ca9b2-141">Olá HTTP + Swagger conector tem um gatilho.</span><span class="sxs-lookup"><span data-stu-id="ca9b2-141">hello HTTP + Swagger connector has one trigger.</span></span>

| <span data-ttu-id="ca9b2-142">Gatilho</span><span class="sxs-lookup"><span data-stu-id="ca9b2-142">Trigger</span></span> | <span data-ttu-id="ca9b2-143">Descrição</span><span class="sxs-lookup"><span data-stu-id="ca9b2-143">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ca9b2-144">HTTP + Swagger</span><span class="sxs-lookup"><span data-stu-id="ca9b2-144">HTTP + Swagger</span></span> |<span data-ttu-id="ca9b2-145">Fazer uma chamada HTTP e retornar o conteúdo da resposta Olá</span><span class="sxs-lookup"><span data-stu-id="ca9b2-145">Make an HTTP call and return hello response content</span></span> |

## <a name="http--swagger-actions"></a><span data-ttu-id="ca9b2-146">Ações de HTTP + Swagger</span><span class="sxs-lookup"><span data-stu-id="ca9b2-146">HTTP + Swagger actions</span></span>
<span data-ttu-id="ca9b2-147">Uma ação é uma operação que é executada pelo fluxo de trabalho de saudação que é definido em um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="ca9b2-147">An action is an operation that's carried out by hello workflow that's defined in a logic app.</span></span> [<span data-ttu-id="ca9b2-148">Saiba mais sobre ações.</span><span class="sxs-lookup"><span data-stu-id="ca9b2-148">Learn more about actions.</span></span>](connectors-overview.md) <span data-ttu-id="ca9b2-149">Olá HTTP + Swagger connector tem uma ação possível.</span><span class="sxs-lookup"><span data-stu-id="ca9b2-149">hello HTTP + Swagger connector has one possible action.</span></span>

| <span data-ttu-id="ca9b2-150">Ação</span><span class="sxs-lookup"><span data-stu-id="ca9b2-150">Action</span></span> | <span data-ttu-id="ca9b2-151">Descrição</span><span class="sxs-lookup"><span data-stu-id="ca9b2-151">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ca9b2-152">HTTP + Swagger</span><span class="sxs-lookup"><span data-stu-id="ca9b2-152">HTTP + Swagger</span></span> |<span data-ttu-id="ca9b2-153">Fazer uma chamada HTTP e retornar o conteúdo da resposta Olá</span><span class="sxs-lookup"><span data-stu-id="ca9b2-153">Make an HTTP call and return hello response content</span></span> |

### <a name="action-details"></a><span data-ttu-id="ca9b2-154">Detalhes da ação</span><span class="sxs-lookup"><span data-stu-id="ca9b2-154">Action details</span></span>
<span data-ttu-id="ca9b2-155">Olá HTTP + Swagger conector vem com uma ação possível.</span><span class="sxs-lookup"><span data-stu-id="ca9b2-155">hello HTTP + Swagger connector comes with one possible action.</span></span> <span data-ttu-id="ca9b2-156">A seguir é informações sobre cada uma das ações hello, campos de entrada necessários e opcionais e Olá correspondente detalhes de saída que estão associados com o seu uso.</span><span class="sxs-lookup"><span data-stu-id="ca9b2-156">Following is information about each of hello actions, their required and optional input fields, and hello corresponding output details that are associated with their usage.</span></span>

#### <a name="http--swagger"></a><span data-ttu-id="ca9b2-157">HTTP + Swagger</span><span class="sxs-lookup"><span data-stu-id="ca9b2-157">HTTP + Swagger</span></span>
<span data-ttu-id="ca9b2-158">Faça uma solicitação de saída HTTP com a assistência dos metadados do Swagger.</span><span class="sxs-lookup"><span data-stu-id="ca9b2-158">Make an HTTP outbound request with assistance of Swagger metadata.</span></span>
<span data-ttu-id="ca9b2-159">Um asterisco (*) significa um campo obrigatório.</span><span class="sxs-lookup"><span data-stu-id="ca9b2-159">An asterisk (*) means a required field.</span></span>

| <span data-ttu-id="ca9b2-160">Nome de exibição</span><span class="sxs-lookup"><span data-stu-id="ca9b2-160">Display name</span></span> | <span data-ttu-id="ca9b2-161">Nome da propriedade</span><span class="sxs-lookup"><span data-stu-id="ca9b2-161">Property name</span></span> | <span data-ttu-id="ca9b2-162">Descrição</span><span class="sxs-lookup"><span data-stu-id="ca9b2-162">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ca9b2-163">Método*</span><span class="sxs-lookup"><span data-stu-id="ca9b2-163">Method*</span></span> |<span data-ttu-id="ca9b2-164">estático</span><span class="sxs-lookup"><span data-stu-id="ca9b2-164">method</span></span> |<span data-ttu-id="ca9b2-165">Toouse de verbo HTTP.</span><span class="sxs-lookup"><span data-stu-id="ca9b2-165">HTTP verb toouse.</span></span> |
| <span data-ttu-id="ca9b2-166">URI*</span><span class="sxs-lookup"><span data-stu-id="ca9b2-166">URI*</span></span> |<span data-ttu-id="ca9b2-167">uri</span><span class="sxs-lookup"><span data-stu-id="ca9b2-167">uri</span></span> |<span data-ttu-id="ca9b2-168">URI da solicitação HTTP de saudação.</span><span class="sxs-lookup"><span data-stu-id="ca9b2-168">URI for hello HTTP request.</span></span> |
| <span data-ttu-id="ca9b2-169">Cabeçalhos</span><span class="sxs-lookup"><span data-stu-id="ca9b2-169">Headers</span></span> |<span data-ttu-id="ca9b2-170">headers</span><span class="sxs-lookup"><span data-stu-id="ca9b2-170">headers</span></span> |<span data-ttu-id="ca9b2-171">Um objeto JSON de tooinclude de cabeçalhos HTTP.</span><span class="sxs-lookup"><span data-stu-id="ca9b2-171">A JSON object of HTTP headers tooinclude.</span></span> |
| <span data-ttu-id="ca9b2-172">Corpo</span><span class="sxs-lookup"><span data-stu-id="ca9b2-172">Body</span></span> |<span data-ttu-id="ca9b2-173">body</span><span class="sxs-lookup"><span data-stu-id="ca9b2-173">body</span></span> |<span data-ttu-id="ca9b2-174">Olá corpo da solicitação HTTP.</span><span class="sxs-lookup"><span data-stu-id="ca9b2-174">hello HTTP request body.</span></span> |
| <span data-ttu-id="ca9b2-175">Autenticação</span><span class="sxs-lookup"><span data-stu-id="ca9b2-175">Authentication</span></span> |<span data-ttu-id="ca9b2-176">Autenticação</span><span class="sxs-lookup"><span data-stu-id="ca9b2-176">authentication</span></span> |<span data-ttu-id="ca9b2-177">Toouse de autenticação para a solicitação.</span><span class="sxs-lookup"><span data-stu-id="ca9b2-177">Authentication toouse for request.</span></span> <span data-ttu-id="ca9b2-178">Para obter mais informações, consulte Olá [conector HTTP](connectors-native-http.md#authentication).</span><span class="sxs-lookup"><span data-stu-id="ca9b2-178">For more information, see hello [HTTP connector](connectors-native-http.md#authentication).</span></span> |

<span data-ttu-id="ca9b2-179">**Detalhes de saída**</span><span class="sxs-lookup"><span data-stu-id="ca9b2-179">**Output details**</span></span>

<span data-ttu-id="ca9b2-180">Resposta HTTP</span><span class="sxs-lookup"><span data-stu-id="ca9b2-180">HTTP response</span></span>

| <span data-ttu-id="ca9b2-181">Nome da propriedade</span><span class="sxs-lookup"><span data-stu-id="ca9b2-181">Property Name</span></span> | <span data-ttu-id="ca9b2-182">Tipo de dados</span><span class="sxs-lookup"><span data-stu-id="ca9b2-182">Data type</span></span> | <span data-ttu-id="ca9b2-183">Descrição</span><span class="sxs-lookup"><span data-stu-id="ca9b2-183">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ca9b2-184">headers</span><span class="sxs-lookup"><span data-stu-id="ca9b2-184">Headers</span></span> |<span data-ttu-id="ca9b2-185">objeto</span><span class="sxs-lookup"><span data-stu-id="ca9b2-185">object</span></span> |<span data-ttu-id="ca9b2-186">Cabeçalhos de resposta</span><span class="sxs-lookup"><span data-stu-id="ca9b2-186">Response headers</span></span> |
| <span data-ttu-id="ca9b2-187">Corpo</span><span class="sxs-lookup"><span data-stu-id="ca9b2-187">Body</span></span> |<span data-ttu-id="ca9b2-188">objeto</span><span class="sxs-lookup"><span data-stu-id="ca9b2-188">object</span></span> |<span data-ttu-id="ca9b2-189">Objeto de resposta</span><span class="sxs-lookup"><span data-stu-id="ca9b2-189">Response object</span></span> |
| <span data-ttu-id="ca9b2-190">Código de status</span><span class="sxs-lookup"><span data-stu-id="ca9b2-190">Status Code</span></span> |<span data-ttu-id="ca9b2-191">int</span><span class="sxs-lookup"><span data-stu-id="ca9b2-191">int</span></span> |<span data-ttu-id="ca9b2-192">Código de status HTTP</span><span class="sxs-lookup"><span data-stu-id="ca9b2-192">HTTP status code</span></span> |

### <a name="http-responses"></a><span data-ttu-id="ca9b2-193">Respostas HTTP</span><span class="sxs-lookup"><span data-stu-id="ca9b2-193">HTTP responses</span></span>
<span data-ttu-id="ca9b2-194">Ao fazer chamadas toovarious ações, você poderá obter respostas de determinados.</span><span class="sxs-lookup"><span data-stu-id="ca9b2-194">When making calls toovarious actions, you might get certain responses.</span></span> <span data-ttu-id="ca9b2-195">A seguir, uma tabela que descreve respostas e descrições correspondentes.</span><span class="sxs-lookup"><span data-stu-id="ca9b2-195">Following is a table that outlines corresponding responses and descriptions.</span></span>

| <span data-ttu-id="ca9b2-196">Name</span><span class="sxs-lookup"><span data-stu-id="ca9b2-196">Name</span></span> | <span data-ttu-id="ca9b2-197">Descrição</span><span class="sxs-lookup"><span data-stu-id="ca9b2-197">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ca9b2-198">200</span><span class="sxs-lookup"><span data-stu-id="ca9b2-198">200</span></span> |<span data-ttu-id="ca9b2-199">OK</span><span class="sxs-lookup"><span data-stu-id="ca9b2-199">OK</span></span> |
| <span data-ttu-id="ca9b2-200">202</span><span class="sxs-lookup"><span data-stu-id="ca9b2-200">202</span></span> |<span data-ttu-id="ca9b2-201">Aceita</span><span class="sxs-lookup"><span data-stu-id="ca9b2-201">Accepted</span></span> |
| <span data-ttu-id="ca9b2-202">400</span><span class="sxs-lookup"><span data-stu-id="ca9b2-202">400</span></span> |<span data-ttu-id="ca9b2-203">Solicitação incorreta</span><span class="sxs-lookup"><span data-stu-id="ca9b2-203">Bad request</span></span> |
| <span data-ttu-id="ca9b2-204">401</span><span class="sxs-lookup"><span data-stu-id="ca9b2-204">401</span></span> |<span data-ttu-id="ca9b2-205">Não Autorizado</span><span class="sxs-lookup"><span data-stu-id="ca9b2-205">Unauthorized</span></span> |
| <span data-ttu-id="ca9b2-206">403</span><span class="sxs-lookup"><span data-stu-id="ca9b2-206">403</span></span> |<span data-ttu-id="ca9b2-207">Proibido</span><span class="sxs-lookup"><span data-stu-id="ca9b2-207">Forbidden</span></span> |
| <span data-ttu-id="ca9b2-208">404</span><span class="sxs-lookup"><span data-stu-id="ca9b2-208">404</span></span> |<span data-ttu-id="ca9b2-209">Não encontrado</span><span class="sxs-lookup"><span data-stu-id="ca9b2-209">Not Found</span></span> |
| <span data-ttu-id="ca9b2-210">500</span><span class="sxs-lookup"><span data-stu-id="ca9b2-210">500</span></span> |<span data-ttu-id="ca9b2-211">Erro interno do servidor.</span><span class="sxs-lookup"><span data-stu-id="ca9b2-211">Internal server error.</span></span> <span data-ttu-id="ca9b2-212">Ocorreu um erro desconhecido.</span><span class="sxs-lookup"><span data-stu-id="ca9b2-212">Unknown error occurred.</span></span> |

- - -
## <a name="next-steps"></a><span data-ttu-id="ca9b2-213">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ca9b2-213">Next steps</span></span>

* [<span data-ttu-id="ca9b2-214">Criar um aplicativo lógico</span><span class="sxs-lookup"><span data-stu-id="ca9b2-214">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)
* [<span data-ttu-id="ca9b2-215">Localizar outros conectores</span><span class="sxs-lookup"><span data-stu-id="ca9b2-215">Find other connectors</span></span>](apis-list.md)