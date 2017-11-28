---
title: "aaaStore dados não estruturados usando funções do Azure e banco de dados do Cosmos"
description: "Armazenar dados não estruturados usando o Azure Functions e o Cosmos DB"
services: functions
documentationcenter: functions
author: rachelappel
manager: erikre
editor: 
tags: 
keywords: "azure functions, functions, processamento de eventos, Cosmos DB, computação dinâmica, arquitetura sem servidor"
ms.assetid: 
ms.service: functions
ms.devlang: csharp
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 08/03/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 48d6899c20d3e6f6b062725fca329972ead3c696
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="store-unstructured-data-using-azure-functions-and-cosmos-db"></a><span data-ttu-id="6ffee-104">Armazenar dados não estruturados usando o Azure Functions e o Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="6ffee-104">Store unstructured data using Azure Functions and Cosmos DB</span></span>

<span data-ttu-id="6ffee-105">[Banco de dados do Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/) é uma ótima maneira toostore não estruturado e dados JSON.</span><span class="sxs-lookup"><span data-stu-id="6ffee-105">[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) is a great way toostore unstructured and JSON data.</span></span> <span data-ttu-id="6ffee-106">Combinado com o Azure Functions, o Cosmos DB torna o armazenamento de dados rápido e fácil com muito menos código do que o necessário para armazenar dados em um banco de dados relacional.</span><span class="sxs-lookup"><span data-stu-id="6ffee-106">Combined with Azure Functions, Cosmos DB makes storing data quick and easy with much less code than required for storing data in a relational database.</span></span>

<span data-ttu-id="6ffee-107">Em funções do Azure, as associações de entrada e saídas fornecem um forma declarativa tooconnect tooexternal serviço de dados de sua função.</span><span class="sxs-lookup"><span data-stu-id="6ffee-107">In Azure Functions, input and output bindings provide a declarative way tooconnect tooexternal service data from your function.</span></span> <span data-ttu-id="6ffee-108">Neste tópico, Aprenda como tooupdate um existente c# função tooadd uma associação de saída que armazena dados não estruturados em um documento de banco de dados do Cosmos.</span><span class="sxs-lookup"><span data-stu-id="6ffee-108">In this topic, learn how tooupdate an existing C# function tooadd an output binding that stores unstructured data in a Cosmos DB document.</span></span> 

![Banco de Dados Cosmos](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-cosmosdb.png)

## <a name="prerequisites"></a><span data-ttu-id="6ffee-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="6ffee-110">Prerequisites</span></span>

<span data-ttu-id="6ffee-111">toocomplete este tutorial:</span><span class="sxs-lookup"><span data-stu-id="6ffee-111">toocomplete this tutorial:</span></span>

[!INCLUDE [Previous quickstart note](../../includes/functions-quickstart-previous-topics.md)]

## <a name="add-an-output-binding"></a><span data-ttu-id="6ffee-112">Adicionar uma associação de saída</span><span class="sxs-lookup"><span data-stu-id="6ffee-112">Add an output binding</span></span>

1. <span data-ttu-id="6ffee-113">Expanda seu aplicativo de funções e sua função.</span><span class="sxs-lookup"><span data-stu-id="6ffee-113">Expand both your function app and your function.</span></span>

1. <span data-ttu-id="6ffee-114">Selecione **integrar** e **+ nova saída**, que está no hello parte superior direita da página de saudação.</span><span class="sxs-lookup"><span data-stu-id="6ffee-114">Select **Integrate** and **+ New Output**, which is at hello top right of hello page.</span></span> <span data-ttu-id="6ffee-115">Escolha **Azure Cosmos DB** e clique em **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="6ffee-115">Choose **Azure Cosmos DB**, and click **Select**.</span></span>

    ![Adicionar uma associação de saída do Cosmos DB](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-integrate-tab-add-new-output-binding.png)

3. <span data-ttu-id="6ffee-117">Saudação de uso **saída de banco de dados do Azure Cosmos** configurações conforme especificado na tabela de saudação:</span><span class="sxs-lookup"><span data-stu-id="6ffee-117">Use hello **Azure Cosmos DB output** settings as specified in hello table:</span></span> 

    ![Configurar associação de saída do Cosmos DB](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-integrate-tab-configure-cosmosdb-binding.png)

    | <span data-ttu-id="6ffee-119">Configuração</span><span class="sxs-lookup"><span data-stu-id="6ffee-119">Setting</span></span>      | <span data-ttu-id="6ffee-120">Valor sugerido</span><span class="sxs-lookup"><span data-stu-id="6ffee-120">Suggested value</span></span>  | <span data-ttu-id="6ffee-121">Descrição</span><span class="sxs-lookup"><span data-stu-id="6ffee-121">Description</span></span>                                |
    | ------------ | ---------------- | ------------------------------------------ |
    | <span data-ttu-id="6ffee-122">**Nome do parâmetro do documento**</span><span class="sxs-lookup"><span data-stu-id="6ffee-122">**Document parameter name**</span></span> | <span data-ttu-id="6ffee-123">taskDocument</span><span class="sxs-lookup"><span data-stu-id="6ffee-123">taskDocument</span></span> | <span data-ttu-id="6ffee-124">Nome que se refere o objeto de banco de dados do Cosmos toohello no código.</span><span class="sxs-lookup"><span data-stu-id="6ffee-124">Name that refers toohello Cosmos DB object in code.</span></span> |
    | <span data-ttu-id="6ffee-125">**Nome do banco de dados**</span><span class="sxs-lookup"><span data-stu-id="6ffee-125">**Database name**</span></span> | <span data-ttu-id="6ffee-126">taskDatabase</span><span class="sxs-lookup"><span data-stu-id="6ffee-126">taskDatabase</span></span> | <span data-ttu-id="6ffee-127">Nome de documentos de toosave do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="6ffee-127">Name of database toosave documents.</span></span> |
    | <span data-ttu-id="6ffee-128">**Nome da coleção**</span><span class="sxs-lookup"><span data-stu-id="6ffee-128">**Collection name**</span></span> | <span data-ttu-id="6ffee-129">TaskCollection</span><span class="sxs-lookup"><span data-stu-id="6ffee-129">TaskCollection</span></span> | <span data-ttu-id="6ffee-130">Nome da coleção dos bancos de dados Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="6ffee-130">Name of collection of Cosmos DB databases.</span></span> |
    | <span data-ttu-id="6ffee-131">**Se true, cria a coleção e o banco de dados de banco de dados do Cosmos Olá**</span><span class="sxs-lookup"><span data-stu-id="6ffee-131">**If true, creates hello Cosmos DB database and collection**</span></span> | <span data-ttu-id="6ffee-132">Verificado</span><span class="sxs-lookup"><span data-stu-id="6ffee-132">Checked</span></span> | <span data-ttu-id="6ffee-133">coleção de saudação não existir, então criá-lo.</span><span class="sxs-lookup"><span data-stu-id="6ffee-133">hello collection doesn't already exist, so create it.</span></span> |

4. <span data-ttu-id="6ffee-134">Selecione **novo** toohello próximo **conexão do banco de dados do Cosmos documento** rótulo e selecione **+ criar novo**.</span><span class="sxs-lookup"><span data-stu-id="6ffee-134">Select **New** next toohello **Cosmos DB document connection** label, and select **+ Create new**.</span></span> 

5. <span data-ttu-id="6ffee-135">Saudação de uso **nova conta** configurações conforme especificado na tabela de saudação:</span><span class="sxs-lookup"><span data-stu-id="6ffee-135">Use hello **New account** settings as specified in hello table:</span></span> 

    ![Configurar a conexão do Cosmos DB](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-create-CosmosDB.png)

    | <span data-ttu-id="6ffee-137">Configuração</span><span class="sxs-lookup"><span data-stu-id="6ffee-137">Setting</span></span>      | <span data-ttu-id="6ffee-138">Valor sugerido</span><span class="sxs-lookup"><span data-stu-id="6ffee-138">Suggested value</span></span>  | <span data-ttu-id="6ffee-139">Descrição</span><span class="sxs-lookup"><span data-stu-id="6ffee-139">Description</span></span>                                |
    | ------------ | ---------------- | ------------------------------------------ |
    | <span data-ttu-id="6ffee-140">**ID**</span><span class="sxs-lookup"><span data-stu-id="6ffee-140">**ID**</span></span> | <span data-ttu-id="6ffee-141">Nome do banco de dados</span><span class="sxs-lookup"><span data-stu-id="6ffee-141">Name of database</span></span> | <span data-ttu-id="6ffee-142">ID exclusiva para o banco de dados de banco de dados do Cosmos Olá</span><span class="sxs-lookup"><span data-stu-id="6ffee-142">Unique ID for hello Cosmos DB database</span></span>  |
    | <span data-ttu-id="6ffee-143">**API**</span><span class="sxs-lookup"><span data-stu-id="6ffee-143">**API**</span></span> | <span data-ttu-id="6ffee-144">SQL (DocumentDB)</span><span class="sxs-lookup"><span data-stu-id="6ffee-144">SQL (DocumentDB)</span></span> | <span data-ttu-id="6ffee-145">Selecione Olá API de banco de dados de documento.</span><span class="sxs-lookup"><span data-stu-id="6ffee-145">Select hello document database API.</span></span>  |
    | <span data-ttu-id="6ffee-146">**Assinatura**</span><span class="sxs-lookup"><span data-stu-id="6ffee-146">**Subscription**</span></span> | <span data-ttu-id="6ffee-147">Assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="6ffee-147">Azure Subscription</span></span> | <span data-ttu-id="6ffee-148">Assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="6ffee-148">Azure Subscription</span></span>  |
    | <span data-ttu-id="6ffee-149">**Grupo de recursos**</span><span class="sxs-lookup"><span data-stu-id="6ffee-149">**Resource Group**</span></span> | <span data-ttu-id="6ffee-150">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="6ffee-150">myResourceGroup</span></span> |  <span data-ttu-id="6ffee-151">Use Olá grupo de recursos existente que contém seu aplicativo de função.</span><span class="sxs-lookup"><span data-stu-id="6ffee-151">Use hello existing resource group that contains your function app.</span></span> |
    | <span data-ttu-id="6ffee-152">**Localidade**</span><span class="sxs-lookup"><span data-stu-id="6ffee-152">**Location**</span></span>  | <span data-ttu-id="6ffee-153">WestEurope</span><span class="sxs-lookup"><span data-stu-id="6ffee-153">WestEurope</span></span> | <span data-ttu-id="6ffee-154">Selecione um local perto tooeither seu aplicativo de função ou tooother aplicativos que usam Olá documentos armazenados.</span><span class="sxs-lookup"><span data-stu-id="6ffee-154">Select a location near tooeither your function app or tooother apps that use hello stored documents.</span></span>  |

6. <span data-ttu-id="6ffee-155">Clique em **Okey** o banco de dados do toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="6ffee-155">Click **OK** toocreate hello database.</span></span> <span data-ttu-id="6ffee-156">Ele pode levar o banco de dados Olá toocreate de alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="6ffee-156">It may take a few minutes toocreate hello database.</span></span> <span data-ttu-id="6ffee-157">Após a criação do banco de dados hello, cadeia de conexão de banco de dados de saudação é armazenada como uma configuração de aplicativo de função.</span><span class="sxs-lookup"><span data-stu-id="6ffee-157">After hello database is created, hello database connection string is stored as a function app setting.</span></span> <span data-ttu-id="6ffee-158">nome da saudação dessa configuração de aplicativo é inserido no **conexão de conta do banco de dados do Cosmos**.</span><span class="sxs-lookup"><span data-stu-id="6ffee-158">hello name of this app setting is inserted in **Cosmos DB account connection**.</span></span> 
 
8. <span data-ttu-id="6ffee-159">Após definir a cadeia de caracteres de conexão Olá, selecione **salvar** toocreate associação de saudação.</span><span class="sxs-lookup"><span data-stu-id="6ffee-159">After hello connection string is set, select **Save** toocreate hello binding.</span></span>

## <a name="update-hello-function-code"></a><span data-ttu-id="6ffee-160">Atualizar o código de função hello</span><span class="sxs-lookup"><span data-stu-id="6ffee-160">Update hello function code</span></span>

<span data-ttu-id="6ffee-161">Substitua Olá c# função código existente pelo Olá código a seguir:</span><span class="sxs-lookup"><span data-stu-id="6ffee-161">Replace hello existing C# function code with hello following code:</span></span>

```csharp
using System.Net;

public static HttpResponseMessage Run(HttpRequestMessage req, out object taskDocument, TraceWriter log)
{
    string name = req.GetQueryNameValuePairs()
        .FirstOrDefault(q => string.Compare(q.Key, "name", true) == 0)
        .Value;

    string task = req.GetQueryNameValuePairs()
        .FirstOrDefault(q => string.Compare(q.Key, "task", true) == 0)
        .Value;

    string duedate = req.GetQueryNameValuePairs()
        .FirstOrDefault(q => string.Compare(q.Key, "duedate", true) == 0)
        .Value;

    taskDocument = new {
        name = name,
        duedate = duedate.ToString(),
        task = task
    };

    if (name != "" && task != "") {
        return req.CreateResponse(HttpStatusCode.OK);
    }
    else {
        return req.CreateResponse(HttpStatusCode.BadRequest);
    }
}

```
<span data-ttu-id="6ffee-162">Este exemplo de código lê Olá solicitação HTTP cadeias de caracteres de consulta e os atribui toofields em Olá `taskDocument` objeto.</span><span class="sxs-lookup"><span data-stu-id="6ffee-162">This code sample reads hello HTTP Request query strings and assigns them toofields in hello `taskDocument` object.</span></span> <span data-ttu-id="6ffee-163">Olá `taskDocument` associação envia dados de objeto de saudação de toobe de parâmetro essa associação armazenado no banco de dados de documento de saudação.</span><span class="sxs-lookup"><span data-stu-id="6ffee-163">hello `taskDocument` binding sends hello object data from this binding parameter toobe stored in hello bound document database.</span></span> <span data-ttu-id="6ffee-164">Olá banco de dados criado Olá primeira vez Olá função é executada.</span><span class="sxs-lookup"><span data-stu-id="6ffee-164">hello database is created hello first time hello function runs.</span></span>

## <a name="test-hello-function-and-database"></a><span data-ttu-id="6ffee-165">Função de saudação do teste e o banco de dados</span><span class="sxs-lookup"><span data-stu-id="6ffee-165">Test hello function and database</span></span>

1. <span data-ttu-id="6ffee-166">Expanda a janela direita hello e selecione **teste**.</span><span class="sxs-lookup"><span data-stu-id="6ffee-166">Expand hello right window and select **Test**.</span></span> <span data-ttu-id="6ffee-167">Em **consulta**, clique em **+ Adicionar parâmetro** e adicione Olá cadeia de caracteres de consulta de toohello parâmetros a seguir:</span><span class="sxs-lookup"><span data-stu-id="6ffee-167">Under **Query**, click **+ Add parameter** and add hello following parameters toohello query string:</span></span>

    + `name`
    + `task`
    + `duedate`

2. <span data-ttu-id="6ffee-168">Clique em **Executar** e verifique se um status 200 retorna.</span><span class="sxs-lookup"><span data-stu-id="6ffee-168">Click **Run** and verify that a 200 status is returned.</span></span>

    ![Configurar associação de saída do Cosmos DB](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-test-function.png)

1. <span data-ttu-id="6ffee-170">Na Olá lado esquerdo da saudação portal do Azure, expanda a barra de ícones Olá, tipo `cosmos` em Olá pesquisar o campo e selecione **o banco de dados do Azure Cosmos**.</span><span class="sxs-lookup"><span data-stu-id="6ffee-170">On hello left side of hello Azure portal, expand hello icon bar, type `cosmos` in hello search field, and select **Azure Cosmos DB**.</span></span>

    ![Pesquisar Olá serviço de banco de dados do Cosmos](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-search-cosmos-db.png)

2. <span data-ttu-id="6ffee-172">Banco de dados selecione Olá criado por você, em seguida, selecione **Data Explorer**.</span><span class="sxs-lookup"><span data-stu-id="6ffee-172">Select hello database you created, then select **Data Explorer**.</span></span> <span data-ttu-id="6ffee-173">Expanda Olá **coleções** nós, selecione Olá novo documento e confirmar esse documento hello contém os valores de cadeia de caracteres de consulta, juntamente com alguns metadados adicionais.</span><span class="sxs-lookup"><span data-stu-id="6ffee-173">Expand hello **Collections** nodes, select hello new document, and confirm that hello document contains your query string values, along with some additional metadata.</span></span> 

    ![Verifique a entrada do Cosmos DB](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-verify-cosmosdb-output.png)

<span data-ttu-id="6ffee-175">Você adicionou com êxito um gatilho HTTP tooyour de associação que armazena dados não estruturados em um banco de dados do banco de dados do Cosmos.</span><span class="sxs-lookup"><span data-stu-id="6ffee-175">You have successfully added a binding tooyour HTTP trigger that stores unstructured data in a Cosmos DB database.</span></span>

[!INCLUDE [Clean-up section](../../includes/clean-up-section-portal.md)]

## <a name="next-steps"></a><span data-ttu-id="6ffee-176">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6ffee-176">Next steps</span></span>

[!INCLUDE [functions-quickstart-next-steps](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="6ffee-177">Para obter mais informações sobre o banco de dados de banco de dados do Cosmos de tooa associação, consulte [associações de banco de dados do Azure funções Cosmos](functions-bindings-documentdb.md).</span><span class="sxs-lookup"><span data-stu-id="6ffee-177">For more information about binding tooa Cosmos DB database, see [Azure Functions Cosmos DB bindings](functions-bindings-documentdb.md).</span></span>
