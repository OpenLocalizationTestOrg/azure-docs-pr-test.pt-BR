---
title: "Chamar pontos de extremidade REST com conector HTTP + Swagger para Aplicativo Lógico do Azure | Microsoft Docs"
description: "Conectar-se aos pontos de extremidade REST de aplicativos lógicos por meio de Swagger com o conector HTTP + Swagger"
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
ms.openlocfilehash: 3e9229d94e96aad7b769d0e55d208d856e3b80bc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-the-http--swagger-action"></a><span data-ttu-id="351c3-103">Introdução à ação de HTTP + Swagger</span><span class="sxs-lookup"><span data-stu-id="351c3-103">Get started with the HTTP + Swagger action</span></span>

<span data-ttu-id="351c3-104">Você pode criar um conector de primeira classe para qualquer ponto de extremidade REST por meio de um [documento Swagger](https://swagger.io) quando você usa a ação HTTP + Swagger no fluxo de trabalho de seu aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="351c3-104">You can create a first-class connector to any REST endpoint through a [Swagger document](https://swagger.io) when you use the HTTP + Swagger action in your logic app workflow.</span></span> <span data-ttu-id="351c3-105">Você também pode estender aplicativos lógicos para chamar qualquer ponto de extremidade REST com uma experiência de Designer de Aplicativo Lógico de primeira classe.</span><span class="sxs-lookup"><span data-stu-id="351c3-105">You can also extend logic apps to call any REST endpoint with a first-class Logic App Designer experience.</span></span>

<span data-ttu-id="351c3-106">Para saber como criar aplicativos lógicos com conectores, consulte [Criar um novo aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="351c3-106">To learn how to create logic apps with connectors, see [Create a new logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-http--swagger-as-a-trigger-or-an-action"></a><span data-ttu-id="351c3-107">Usar HTTP + Swagger como um gatilho ou uma ação</span><span class="sxs-lookup"><span data-stu-id="351c3-107">Use HTTP + Swagger as a trigger or an action</span></span>

<span data-ttu-id="351c3-108">O gatilho e ação HTTP + Swagger funcionam da mesma forma que a [ação HTTP](connectors-native-http.md), porém, proporcionam uma melhor experiência no Designer do Aplicativo Lógico mostrando a estrutura da API e as saídas dos [metadados do Swagger](https://swagger.io).</span><span class="sxs-lookup"><span data-stu-id="351c3-108">The HTTP + Swagger trigger and action work the same as the [HTTP action](connectors-native-http.md) but provide a better experience in Logic App Designer by exposing the API structure and outputs from the [Swagger metadata](https://swagger.io).</span></span> <span data-ttu-id="351c3-109">Você também pode usar o conector HTTP + Swagger como um gatilho.</span><span class="sxs-lookup"><span data-stu-id="351c3-109">You can also use the HTTP + Swagger connector as a trigger.</span></span> <span data-ttu-id="351c3-110">Se você quiser implementar um gatilho de sondagem, siga o padrão de sondagem descrito em [Criar APIs personalizadas para chamar outras APIs, serviços e sistemas de aplicativos lógicos](../logic-apps/logic-apps-create-api-app.md#polling-triggers).</span><span class="sxs-lookup"><span data-stu-id="351c3-110">If you want to implement a polling trigger, follow the polling pattern that's described in [Create custom APIs to call other APIs, services, and systems from logic apps](../logic-apps/logic-apps-create-api-app.md#polling-triggers).</span></span>

<span data-ttu-id="351c3-111">Saiba mais sobre [gatilhos e ações de aplicativo lógico](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="351c3-111">Learn more about [logic app triggers and actions](connectors-overview.md).</span></span>

<span data-ttu-id="351c3-112">Veja um exemplo de como usar a operação HTTP + Swagger como uma ação em um fluxo de trabalho em um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="351c3-112">Here's an example of how to use the HTTP + Swagger operation as an action in a workflow in a logic app.</span></span>

1. <span data-ttu-id="351c3-113">Selecione o botão **Nova Etapa** .</span><span class="sxs-lookup"><span data-stu-id="351c3-113">Select the **New Step** button.</span></span>
2. <span data-ttu-id="351c3-114">Escolha **Adicionar uma ação**.</span><span class="sxs-lookup"><span data-stu-id="351c3-114">Select **Add an action**.</span></span>
3. <span data-ttu-id="351c3-115">Na caixa de pesquisa de ação, digite **swagger** para listar a ação de HTTP + Swagger.</span><span class="sxs-lookup"><span data-stu-id="351c3-115">In the action search box, type **swagger** to list the HTTP + Swagger action.</span></span>
   
    ![Selecionar ação de HTTP + Swagger](./media/connectors-native-http-swagger/using-action-1.png)
4. <span data-ttu-id="351c3-117">Digite a URL para um documento do Swagger:</span><span class="sxs-lookup"><span data-stu-id="351c3-117">Type the URL for a Swagger document:</span></span>
   
   * <span data-ttu-id="351c3-118">Para trabalhar do Designer de Aplicativo Lógico, a URL deverá ser um ponto de extremidade HTTPS e ter CORS habilitado.</span><span class="sxs-lookup"><span data-stu-id="351c3-118">To work from the Logic App Designer, the URL must be an HTTPS endpoint and have CORS enabled.</span></span>
   * <span data-ttu-id="351c3-119">Se o documento do swagger não atender a este requisito, você poderá usar [o Armazenamento do Azure com CORS habilitado](#hosting-swagger-from-storage) para armazenar o documento.</span><span class="sxs-lookup"><span data-stu-id="351c3-119">If the Swagger document doesn't meet this requirement, you can use [Azure Storage with CORS enabled](#hosting-swagger-from-storage) to store the document.</span></span>
5. <span data-ttu-id="351c3-120">Clique em **Avançar** para leitura e renderização do documento do Swagger.</span><span class="sxs-lookup"><span data-stu-id="351c3-120">Click **Next** to read and render from the Swagger document.</span></span>
6. <span data-ttu-id="351c3-121">Adicione todos os parâmetros necessários para a chamada HTTP.</span><span class="sxs-lookup"><span data-stu-id="351c3-121">Add in any parameters that are required for the HTTP call.</span></span>
   
    ![Concluir a ação HTTP](./media/connectors-native-http-swagger/using-action-2.png)
7. <span data-ttu-id="351c3-123">Para salvar e publicar seu aplicativo lógico, clique em **salvar** na barra de ferramentas do designer.</span><span class="sxs-lookup"><span data-stu-id="351c3-123">To save and publish your logic app, click **Save** on designer toolbar.</span></span>

### <a name="host-swagger-from-azure-storage"></a><span data-ttu-id="351c3-124">Hospedar o Swagger do Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="351c3-124">Host Swagger from Azure Storage</span></span>
<span data-ttu-id="351c3-125">Talvez você queira fazer referência a um documento do Swagger que não esteja hospedado ou que não atenda aos requisitos de segurança e entre origens do designer.</span><span class="sxs-lookup"><span data-stu-id="351c3-125">You might want to reference a Swagger document that's not hosted, or that doesn't meet the security and cross-origin requirements for the designer.</span></span> <span data-ttu-id="351c3-126">Para resolver esse problema, você pode armazenar o documento do Swagger no Armazenamento do Azure e habilitar o CORS para fazer referência ao documento.</span><span class="sxs-lookup"><span data-stu-id="351c3-126">To resolve this issue, you can store the Swagger document in Azure Storage and enable CORS to reference the document.</span></span>  

<span data-ttu-id="351c3-127">Veja as etapas para criar, configurar e armazenar documentos do Swagger no Armazenamento do Azure:</span><span class="sxs-lookup"><span data-stu-id="351c3-127">Here are the steps to create, configure, and store Swagger documents in Azure Storage:</span></span>

1. <span data-ttu-id="351c3-128">[Crie uma conta de armazenamento do Azure com o armazenamento de Blobs do Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="351c3-128">[Create an Azure storage account with Azure Blob storage](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="351c3-129">Para realizar essa etapa, defina as permissões como **Acesso Público**.</span><span class="sxs-lookup"><span data-stu-id="351c3-129">To perform this step, set permissions to **Public Access**.</span></span>

2. <span data-ttu-id="351c3-130">Habilite o CORS no blob.</span><span class="sxs-lookup"><span data-stu-id="351c3-130">Enable CORS on the blob.</span></span> 

   <span data-ttu-id="351c3-131">Você pode usar [este script do PowerShell](https://github.com/logicappsio/EnableCORSAzureBlob/blob/master/EnableCORSAzureBlob.ps1) para definir essa configuração automaticamente.</span><span class="sxs-lookup"><span data-stu-id="351c3-131">To automatically configure this setting, you can use [this PowerShell script](https://github.com/logicappsio/EnableCORSAzureBlob/blob/master/EnableCORSAzureBlob.ps1).</span></span>

3. <span data-ttu-id="351c3-132">Carregue o arquivo do Swagger no blob.</span><span class="sxs-lookup"><span data-stu-id="351c3-132">Upload the Swagger file to the blob.</span></span> 

   <span data-ttu-id="351c3-133">Você pode realizar essa etapa do [Portal do Azure](https://portal.azure.com) ou de uma ferramenta como o [Gerenciador de Armazenamento do Azure](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="351c3-133">You can perform this step from the [Azure portal](https://portal.azure.com) or from a tool like [Azure Storage Explorer](http://storageexplorer.com/).</span></span>

4. <span data-ttu-id="351c3-134">Faça referência a um link HTTPS para o documento no armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="351c3-134">Reference an HTTPS link to the document in Azure Blob storage.</span></span> 

   <span data-ttu-id="351c3-135">O link usa este formato:</span><span class="sxs-lookup"><span data-stu-id="351c3-135">The link uses this format:</span></span>

   `https://*storageAccountName*.blob.core.windows.net/*container*/*filename*`

## <a name="technical-details"></a><span data-ttu-id="351c3-136">Detalhes técnicos</span><span class="sxs-lookup"><span data-stu-id="351c3-136">Technical details</span></span>
<span data-ttu-id="351c3-137">A seguir, os detalhes dos gatilhos e das ações com suporte deste conector HTTP + Swagger.</span><span class="sxs-lookup"><span data-stu-id="351c3-137">Following are the details for the triggers and actions that this HTTP + Swagger connector supports.</span></span>

## <a name="http--swagger-triggers"></a><span data-ttu-id="351c3-138">Gatilhos de HTTP + Swagger</span><span class="sxs-lookup"><span data-stu-id="351c3-138">HTTP + Swagger triggers</span></span>
<span data-ttu-id="351c3-139">Um gatilho é um evento que pode ser usado para iniciar o fluxo de trabalho definido em um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="351c3-139">A trigger is an event that can be used to start the workflow that's defined in a logic app.</span></span> [<span data-ttu-id="351c3-140">Saiba mais sobre gatilhos.</span><span class="sxs-lookup"><span data-stu-id="351c3-140">Learn more about triggers.</span></span>](connectors-overview.md) <span data-ttu-id="351c3-141">O conector HTTP + Swagger tem um gatilho.</span><span class="sxs-lookup"><span data-stu-id="351c3-141">The HTTP + Swagger connector has one trigger.</span></span>

| <span data-ttu-id="351c3-142">Gatilho</span><span class="sxs-lookup"><span data-stu-id="351c3-142">Trigger</span></span> | <span data-ttu-id="351c3-143">Descrição</span><span class="sxs-lookup"><span data-stu-id="351c3-143">Description</span></span> |
| --- | --- |
| <span data-ttu-id="351c3-144">HTTP + Swagger</span><span class="sxs-lookup"><span data-stu-id="351c3-144">HTTP + Swagger</span></span> |<span data-ttu-id="351c3-145">Faz uma chamada HTTP e retorna o conteúdo da resposta</span><span class="sxs-lookup"><span data-stu-id="351c3-145">Make an HTTP call and return the response content</span></span> |

## <a name="http--swagger-actions"></a><span data-ttu-id="351c3-146">Ações de HTTP + Swagger</span><span class="sxs-lookup"><span data-stu-id="351c3-146">HTTP + Swagger actions</span></span>
<span data-ttu-id="351c3-147">Uma ação é uma operação executada pelo fluxo de trabalho definido em um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="351c3-147">An action is an operation that's carried out by the workflow that's defined in a logic app.</span></span> [<span data-ttu-id="351c3-148">Saiba mais sobre ações.</span><span class="sxs-lookup"><span data-stu-id="351c3-148">Learn more about actions.</span></span>](connectors-overview.md) <span data-ttu-id="351c3-149">O conector HTTP + Swagger tem uma ação possível.</span><span class="sxs-lookup"><span data-stu-id="351c3-149">The HTTP + Swagger connector has one possible action.</span></span>

| <span data-ttu-id="351c3-150">Ação</span><span class="sxs-lookup"><span data-stu-id="351c3-150">Action</span></span> | <span data-ttu-id="351c3-151">Descrição</span><span class="sxs-lookup"><span data-stu-id="351c3-151">Description</span></span> |
| --- | --- |
| <span data-ttu-id="351c3-152">HTTP + Swagger</span><span class="sxs-lookup"><span data-stu-id="351c3-152">HTTP + Swagger</span></span> |<span data-ttu-id="351c3-153">Faz uma chamada HTTP e retorna o conteúdo da resposta</span><span class="sxs-lookup"><span data-stu-id="351c3-153">Make an HTTP call and return the response content</span></span> |

### <a name="action-details"></a><span data-ttu-id="351c3-154">Detalhes da ação</span><span class="sxs-lookup"><span data-stu-id="351c3-154">Action details</span></span>
<span data-ttu-id="351c3-155">O conector HTTP + Swagger vem uma ação possível.</span><span class="sxs-lookup"><span data-stu-id="351c3-155">The HTTP + Swagger connector comes with one possible action.</span></span> <span data-ttu-id="351c3-156">A seguir, as informações sobre cada uma das ações, seus campos de entrada obrigatórios e opcionais, bem como os detalhes da saída correspondente associada ao uso delas.</span><span class="sxs-lookup"><span data-stu-id="351c3-156">Following is information about each of the actions, their required and optional input fields, and the corresponding output details that are associated with their usage.</span></span>

#### <a name="http--swagger"></a><span data-ttu-id="351c3-157">HTTP + Swagger</span><span class="sxs-lookup"><span data-stu-id="351c3-157">HTTP + Swagger</span></span>
<span data-ttu-id="351c3-158">Faça uma solicitação de saída HTTP com a assistência dos metadados do Swagger.</span><span class="sxs-lookup"><span data-stu-id="351c3-158">Make an HTTP outbound request with assistance of Swagger metadata.</span></span>
<span data-ttu-id="351c3-159">Um asterisco (*) significa um campo obrigatório.</span><span class="sxs-lookup"><span data-stu-id="351c3-159">An asterisk (*) means a required field.</span></span>

| <span data-ttu-id="351c3-160">Nome de exibição</span><span class="sxs-lookup"><span data-stu-id="351c3-160">Display name</span></span> | <span data-ttu-id="351c3-161">Nome da propriedade</span><span class="sxs-lookup"><span data-stu-id="351c3-161">Property name</span></span> | <span data-ttu-id="351c3-162">Descrição</span><span class="sxs-lookup"><span data-stu-id="351c3-162">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="351c3-163">Método*</span><span class="sxs-lookup"><span data-stu-id="351c3-163">Method*</span></span> |<span data-ttu-id="351c3-164">estático</span><span class="sxs-lookup"><span data-stu-id="351c3-164">method</span></span> |<span data-ttu-id="351c3-165">Verbo HTTP a ser usado.</span><span class="sxs-lookup"><span data-stu-id="351c3-165">HTTP verb to use.</span></span> |
| <span data-ttu-id="351c3-166">URI*</span><span class="sxs-lookup"><span data-stu-id="351c3-166">URI*</span></span> |<span data-ttu-id="351c3-167">uri</span><span class="sxs-lookup"><span data-stu-id="351c3-167">uri</span></span> |<span data-ttu-id="351c3-168">URI da solicitação HTTP.</span><span class="sxs-lookup"><span data-stu-id="351c3-168">URI for the HTTP request.</span></span> |
| <span data-ttu-id="351c3-169">Cabeçalhos</span><span class="sxs-lookup"><span data-stu-id="351c3-169">Headers</span></span> |<span data-ttu-id="351c3-170">Cabeçalhos</span><span class="sxs-lookup"><span data-stu-id="351c3-170">headers</span></span> |<span data-ttu-id="351c3-171">Um objeto JSON de cabeçalhos HTTP a serem incluídos.</span><span class="sxs-lookup"><span data-stu-id="351c3-171">A JSON object of HTTP headers to include.</span></span> |
| <span data-ttu-id="351c3-172">Corpo</span><span class="sxs-lookup"><span data-stu-id="351c3-172">Body</span></span> |<span data-ttu-id="351c3-173">Corpo</span><span class="sxs-lookup"><span data-stu-id="351c3-173">body</span></span> |<span data-ttu-id="351c3-174">O corpo da solicitação HTTP.</span><span class="sxs-lookup"><span data-stu-id="351c3-174">The HTTP request body.</span></span> |
| <span data-ttu-id="351c3-175">Autenticação</span><span class="sxs-lookup"><span data-stu-id="351c3-175">Authentication</span></span> |<span data-ttu-id="351c3-176">Autenticação</span><span class="sxs-lookup"><span data-stu-id="351c3-176">authentication</span></span> |<span data-ttu-id="351c3-177">A autenticação a ser usada para solicitação.</span><span class="sxs-lookup"><span data-stu-id="351c3-177">Authentication to use for request.</span></span> <span data-ttu-id="351c3-178">Para obter mais informações, consulte [Conector HTTP](connectors-native-http.md#authentication).</span><span class="sxs-lookup"><span data-stu-id="351c3-178">For more information, see the [HTTP connector](connectors-native-http.md#authentication).</span></span> |

<span data-ttu-id="351c3-179">**Detalhes de saída**</span><span class="sxs-lookup"><span data-stu-id="351c3-179">**Output details**</span></span>

<span data-ttu-id="351c3-180">Resposta HTTP</span><span class="sxs-lookup"><span data-stu-id="351c3-180">HTTP response</span></span>

| <span data-ttu-id="351c3-181">Nome da propriedade</span><span class="sxs-lookup"><span data-stu-id="351c3-181">Property Name</span></span> | <span data-ttu-id="351c3-182">Tipo de dados</span><span class="sxs-lookup"><span data-stu-id="351c3-182">Data type</span></span> | <span data-ttu-id="351c3-183">Descrição</span><span class="sxs-lookup"><span data-stu-id="351c3-183">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="351c3-184">headers</span><span class="sxs-lookup"><span data-stu-id="351c3-184">Headers</span></span> |<span data-ttu-id="351c3-185">objeto</span><span class="sxs-lookup"><span data-stu-id="351c3-185">object</span></span> |<span data-ttu-id="351c3-186">Cabeçalhos de resposta</span><span class="sxs-lookup"><span data-stu-id="351c3-186">Response headers</span></span> |
| <span data-ttu-id="351c3-187">Corpo</span><span class="sxs-lookup"><span data-stu-id="351c3-187">Body</span></span> |<span data-ttu-id="351c3-188">objeto</span><span class="sxs-lookup"><span data-stu-id="351c3-188">object</span></span> |<span data-ttu-id="351c3-189">Objeto de resposta</span><span class="sxs-lookup"><span data-stu-id="351c3-189">Response object</span></span> |
| <span data-ttu-id="351c3-190">Código de status</span><span class="sxs-lookup"><span data-stu-id="351c3-190">Status Code</span></span> |<span data-ttu-id="351c3-191">int</span><span class="sxs-lookup"><span data-stu-id="351c3-191">int</span></span> |<span data-ttu-id="351c3-192">Código de status HTTP</span><span class="sxs-lookup"><span data-stu-id="351c3-192">HTTP status code</span></span> |

### <a name="http-responses"></a><span data-ttu-id="351c3-193">Respostas HTTP</span><span class="sxs-lookup"><span data-stu-id="351c3-193">HTTP responses</span></span>
<span data-ttu-id="351c3-194">Ao fazer chamadas a várias ações, você pode obter determinadas respostas.</span><span class="sxs-lookup"><span data-stu-id="351c3-194">When making calls to various actions, you might get certain responses.</span></span> <span data-ttu-id="351c3-195">A seguir, uma tabela que descreve respostas e descrições correspondentes.</span><span class="sxs-lookup"><span data-stu-id="351c3-195">Following is a table that outlines corresponding responses and descriptions.</span></span>

| <span data-ttu-id="351c3-196">Name</span><span class="sxs-lookup"><span data-stu-id="351c3-196">Name</span></span> | <span data-ttu-id="351c3-197">Descrição</span><span class="sxs-lookup"><span data-stu-id="351c3-197">Description</span></span> |
| --- | --- |
| <span data-ttu-id="351c3-198">200</span><span class="sxs-lookup"><span data-stu-id="351c3-198">200</span></span> |<span data-ttu-id="351c3-199">OK</span><span class="sxs-lookup"><span data-stu-id="351c3-199">OK</span></span> |
| <span data-ttu-id="351c3-200">202</span><span class="sxs-lookup"><span data-stu-id="351c3-200">202</span></span> |<span data-ttu-id="351c3-201">Aceita</span><span class="sxs-lookup"><span data-stu-id="351c3-201">Accepted</span></span> |
| <span data-ttu-id="351c3-202">400</span><span class="sxs-lookup"><span data-stu-id="351c3-202">400</span></span> |<span data-ttu-id="351c3-203">Solicitação incorreta</span><span class="sxs-lookup"><span data-stu-id="351c3-203">Bad request</span></span> |
| <span data-ttu-id="351c3-204">401</span><span class="sxs-lookup"><span data-stu-id="351c3-204">401</span></span> |<span data-ttu-id="351c3-205">Não Autorizado</span><span class="sxs-lookup"><span data-stu-id="351c3-205">Unauthorized</span></span> |
| <span data-ttu-id="351c3-206">403</span><span class="sxs-lookup"><span data-stu-id="351c3-206">403</span></span> |<span data-ttu-id="351c3-207">Proibido</span><span class="sxs-lookup"><span data-stu-id="351c3-207">Forbidden</span></span> |
| <span data-ttu-id="351c3-208">404</span><span class="sxs-lookup"><span data-stu-id="351c3-208">404</span></span> |<span data-ttu-id="351c3-209">Não encontrado</span><span class="sxs-lookup"><span data-stu-id="351c3-209">Not Found</span></span> |
| <span data-ttu-id="351c3-210">500</span><span class="sxs-lookup"><span data-stu-id="351c3-210">500</span></span> |<span data-ttu-id="351c3-211">Erro interno do servidor.</span><span class="sxs-lookup"><span data-stu-id="351c3-211">Internal server error.</span></span> <span data-ttu-id="351c3-212">Ocorreu um erro desconhecido.</span><span class="sxs-lookup"><span data-stu-id="351c3-212">Unknown error occurred.</span></span> |

- - -
## <a name="next-steps"></a><span data-ttu-id="351c3-213">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="351c3-213">Next steps</span></span>

* [<span data-ttu-id="351c3-214">Criar um aplicativo lógico</span><span class="sxs-lookup"><span data-stu-id="351c3-214">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)
* [<span data-ttu-id="351c3-215">Localizar outros conectores</span><span class="sxs-lookup"><span data-stu-id="351c3-215">Find other connectors</span></span>](apis-list.md)