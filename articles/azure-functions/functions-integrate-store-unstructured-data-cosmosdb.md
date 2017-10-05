---
title: "Armazenar dados não estruturados usando o Azure Functions e o Cosmos DB"
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
ms.openlocfilehash: 7c18676ff94ec7da17094abc5f33fb3c6a79895f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="store-unstructured-data-using-azure-functions-and-cosmos-db"></a><span data-ttu-id="7e421-104">Armazenar dados não estruturados usando o Azure Functions e o Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="7e421-104">Store unstructured data using Azure Functions and Cosmos DB</span></span>

<span data-ttu-id="7e421-105">O [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) é uma ótima maneira de armazenar dados não estruturados e JSON.</span><span class="sxs-lookup"><span data-stu-id="7e421-105">[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) is a great way to store unstructured and JSON data.</span></span> <span data-ttu-id="7e421-106">Combinado com o Azure Functions, o Cosmos DB torna o armazenamento de dados rápido e fácil com muito menos código do que o necessário para armazenar dados em um banco de dados relacional.</span><span class="sxs-lookup"><span data-stu-id="7e421-106">Combined with Azure Functions, Cosmos DB makes storing data quick and easy with much less code than required for storing data in a relational database.</span></span>

<span data-ttu-id="7e421-107">No Azure Functions, associações de entrada e saída fornecem uma maneira declarativa para se conectar a dados de serviço externo de sua função.</span><span class="sxs-lookup"><span data-stu-id="7e421-107">In Azure Functions, input and output bindings provide a declarative way to connect to external service data from your function.</span></span> <span data-ttu-id="7e421-108">Neste tópico, saiba como atualizar uma função existente em C# a fim de adicionar uma associação de saída que armazena dados não estruturados em um documento do Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="7e421-108">In this topic, learn how to update an existing C# function to add an output binding that stores unstructured data in a Cosmos DB document.</span></span> 

![Banco de Dados Cosmos](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-cosmosdb.png)

## <a name="prerequisites"></a><span data-ttu-id="7e421-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="7e421-110">Prerequisites</span></span>

<span data-ttu-id="7e421-111">Para concluir este tutorial:</span><span class="sxs-lookup"><span data-stu-id="7e421-111">To complete this tutorial:</span></span>

[!INCLUDE [Previous quickstart note](../../includes/functions-quickstart-previous-topics.md)]

## <a name="add-an-output-binding"></a><span data-ttu-id="7e421-112">Adicionar uma associação de saída</span><span class="sxs-lookup"><span data-stu-id="7e421-112">Add an output binding</span></span>

1. <span data-ttu-id="7e421-113">Expanda seu aplicativo de funções e sua função.</span><span class="sxs-lookup"><span data-stu-id="7e421-113">Expand both your function app and your function.</span></span>

1. <span data-ttu-id="7e421-114">Selecione **Integrar** e **+Nova Saída**, que está na parte superior direita da página.</span><span class="sxs-lookup"><span data-stu-id="7e421-114">Select **Integrate** and **+ New Output**, which is at the top right of the page.</span></span> <span data-ttu-id="7e421-115">Escolha **Azure Cosmos DB** e clique em **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="7e421-115">Choose **Azure Cosmos DB**, and click **Select**.</span></span>

    ![Adicionar uma associação de saída do Cosmos DB](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-integrate-tab-add-new-output-binding.png)

3. <span data-ttu-id="7e421-117">Use a configuração **Saída do Azure Cosmos DB** conforme especificado na tabela:</span><span class="sxs-lookup"><span data-stu-id="7e421-117">Use the **Azure Cosmos DB output** settings as specified in the table:</span></span> 

    ![Configurar associação de saída do Cosmos DB](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-integrate-tab-configure-cosmosdb-binding.png)

    | <span data-ttu-id="7e421-119">Configuração</span><span class="sxs-lookup"><span data-stu-id="7e421-119">Setting</span></span>      | <span data-ttu-id="7e421-120">Valor sugerido</span><span class="sxs-lookup"><span data-stu-id="7e421-120">Suggested value</span></span>  | <span data-ttu-id="7e421-121">Descrição</span><span class="sxs-lookup"><span data-stu-id="7e421-121">Description</span></span>                                |
    | ------------ | ---------------- | ------------------------------------------ |
    | <span data-ttu-id="7e421-122">**Nome do parâmetro do documento**</span><span class="sxs-lookup"><span data-stu-id="7e421-122">**Document parameter name**</span></span> | <span data-ttu-id="7e421-123">taskDocument</span><span class="sxs-lookup"><span data-stu-id="7e421-123">taskDocument</span></span> | <span data-ttu-id="7e421-124">Nome que se refere ao objeto do Cosmos DB no código.</span><span class="sxs-lookup"><span data-stu-id="7e421-124">Name that refers to the Cosmos DB object in code.</span></span> |
    | <span data-ttu-id="7e421-125">**Nome do banco de dados**</span><span class="sxs-lookup"><span data-stu-id="7e421-125">**Database name**</span></span> | <span data-ttu-id="7e421-126">taskDatabase</span><span class="sxs-lookup"><span data-stu-id="7e421-126">taskDatabase</span></span> | <span data-ttu-id="7e421-127">Nome do banco de dados para salvar os documentos.</span><span class="sxs-lookup"><span data-stu-id="7e421-127">Name of database to save documents.</span></span> |
    | <span data-ttu-id="7e421-128">**Nome da coleção**</span><span class="sxs-lookup"><span data-stu-id="7e421-128">**Collection name**</span></span> | <span data-ttu-id="7e421-129">TaskCollection</span><span class="sxs-lookup"><span data-stu-id="7e421-129">TaskCollection</span></span> | <span data-ttu-id="7e421-130">Nome da coleção dos bancos de dados Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="7e421-130">Name of collection of Cosmos DB databases.</span></span> |
    | <span data-ttu-id="7e421-131">**Se for true, cria o banco de dados e a coleção do Cosmos DB**</span><span class="sxs-lookup"><span data-stu-id="7e421-131">**If true, creates the Cosmos DB database and collection**</span></span> | <span data-ttu-id="7e421-132">Verificado</span><span class="sxs-lookup"><span data-stu-id="7e421-132">Checked</span></span> | <span data-ttu-id="7e421-133">A coleção ainda não existe, então crie uma.</span><span class="sxs-lookup"><span data-stu-id="7e421-133">The collection doesn't already exist, so create it.</span></span> |

4. <span data-ttu-id="7e421-134">Selecione **Novo** ao lado do rótulo **Conexão de documento do Cosmos DB** e selecione **+ Criar novo**.</span><span class="sxs-lookup"><span data-stu-id="7e421-134">Select **New** next to the **Cosmos DB document connection** label, and select **+ Create new**.</span></span> 

5. <span data-ttu-id="7e421-135">Use a configuração de **Nova conta**, conforme especificado na tabela:</span><span class="sxs-lookup"><span data-stu-id="7e421-135">Use the **New account** settings as specified in the table:</span></span> 

    ![Configurar a conexão do Cosmos DB](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-create-CosmosDB.png)

    | <span data-ttu-id="7e421-137">Configuração</span><span class="sxs-lookup"><span data-stu-id="7e421-137">Setting</span></span>      | <span data-ttu-id="7e421-138">Valor sugerido</span><span class="sxs-lookup"><span data-stu-id="7e421-138">Suggested value</span></span>  | <span data-ttu-id="7e421-139">Descrição</span><span class="sxs-lookup"><span data-stu-id="7e421-139">Description</span></span>                                |
    | ------------ | ---------------- | ------------------------------------------ |
    | <span data-ttu-id="7e421-140">**ID**</span><span class="sxs-lookup"><span data-stu-id="7e421-140">**ID**</span></span> | <span data-ttu-id="7e421-141">Nome do banco de dados</span><span class="sxs-lookup"><span data-stu-id="7e421-141">Name of database</span></span> | <span data-ttu-id="7e421-142">ID exclusiva para o banco de dados do Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="7e421-142">Unique ID for the Cosmos DB database</span></span>  |
    | <span data-ttu-id="7e421-143">**API**</span><span class="sxs-lookup"><span data-stu-id="7e421-143">**API**</span></span> | <span data-ttu-id="7e421-144">SQL (DocumentDB)</span><span class="sxs-lookup"><span data-stu-id="7e421-144">SQL (DocumentDB)</span></span> | <span data-ttu-id="7e421-145">Selecione a API do banco de dados do documento.</span><span class="sxs-lookup"><span data-stu-id="7e421-145">Select the document database API.</span></span>  |
    | <span data-ttu-id="7e421-146">**Assinatura**</span><span class="sxs-lookup"><span data-stu-id="7e421-146">**Subscription**</span></span> | <span data-ttu-id="7e421-147">Assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="7e421-147">Azure Subscription</span></span> | <span data-ttu-id="7e421-148">Assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="7e421-148">Azure Subscription</span></span>  |
    | <span data-ttu-id="7e421-149">**Grupo de recursos**</span><span class="sxs-lookup"><span data-stu-id="7e421-149">**Resource Group**</span></span> | <span data-ttu-id="7e421-150">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="7e421-150">myResourceGroup</span></span> |  <span data-ttu-id="7e421-151">Use o grupo de recursos existente que contém seu aplicativo de função.</span><span class="sxs-lookup"><span data-stu-id="7e421-151">Use the existing resource group that contains your function app.</span></span> |
    | <span data-ttu-id="7e421-152">**Localidade**</span><span class="sxs-lookup"><span data-stu-id="7e421-152">**Location**</span></span>  | <span data-ttu-id="7e421-153">WestEurope</span><span class="sxs-lookup"><span data-stu-id="7e421-153">WestEurope</span></span> | <span data-ttu-id="7e421-154">Selecione um local próximo ao seu aplicativo de função ou a outros aplicativos que usam os documentos armazenados.</span><span class="sxs-lookup"><span data-stu-id="7e421-154">Select a location near to either your function app or to other apps that use the stored documents.</span></span>  |

6. <span data-ttu-id="7e421-155">Clique em **OK** para criar o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="7e421-155">Click **OK** to create the database.</span></span> <span data-ttu-id="7e421-156">A criação do banco de dados pode demorar alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="7e421-156">It may take a few minutes to create the database.</span></span> <span data-ttu-id="7e421-157">Após a criação do banco de dados, a cadeia de conexão de banco de dados é armazenada como uma configuração de aplicativo de função.</span><span class="sxs-lookup"><span data-stu-id="7e421-157">After the database is created, the database connection string is stored as a function app setting.</span></span> <span data-ttu-id="7e421-158">O nome dessa configuração de aplicativo é inserido na **conexão da conta do Cosmos DB**.</span><span class="sxs-lookup"><span data-stu-id="7e421-158">The name of this app setting is inserted in **Cosmos DB account connection**.</span></span> 
 
8. <span data-ttu-id="7e421-159">Após definir a cadeia de conexão, selecione **Salvar** para criar a associação.</span><span class="sxs-lookup"><span data-stu-id="7e421-159">After the connection string is set, select **Save** to create the binding.</span></span>

## <a name="update-the-function-code"></a><span data-ttu-id="7e421-160">Atualizar o código de função</span><span class="sxs-lookup"><span data-stu-id="7e421-160">Update the function code</span></span>

<span data-ttu-id="7e421-161">Substitua o código existente da função em C# pelo código a seguir:</span><span class="sxs-lookup"><span data-stu-id="7e421-161">Replace the existing C# function code with the following code:</span></span>

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
<span data-ttu-id="7e421-162">Esse exemplo de código lê as cadeias de consulta da Solicitação HTTP e as atribui a campos no objeto `taskDocument`.</span><span class="sxs-lookup"><span data-stu-id="7e421-162">This code sample reads the HTTP Request query strings and assigns them to fields in the `taskDocument` object.</span></span> <span data-ttu-id="7e421-163">A associação `taskDocument` envia os dados do objeto desse parâmetro de associação para armazenamento no banco de dados de documento associado.</span><span class="sxs-lookup"><span data-stu-id="7e421-163">The `taskDocument` binding sends the object data from this binding parameter to be stored in the bound document database.</span></span> <span data-ttu-id="7e421-164">O banco de dados é criado na primeira execução da função.</span><span class="sxs-lookup"><span data-stu-id="7e421-164">The database is created the first time the function runs.</span></span>

## <a name="test-the-function-and-database"></a><span data-ttu-id="7e421-165">Testar a função e o banco de dados</span><span class="sxs-lookup"><span data-stu-id="7e421-165">Test the function and database</span></span>

1. <span data-ttu-id="7e421-166">Expanda a janela direita e selecione **Testar**.</span><span class="sxs-lookup"><span data-stu-id="7e421-166">Expand the right window and select **Test**.</span></span> <span data-ttu-id="7e421-167">Em **Consulta**, clique em **+ Adicionar parâmetro** e adicione os seguintes parâmetros à cadeia de consulta:</span><span class="sxs-lookup"><span data-stu-id="7e421-167">Under **Query**, click **+ Add parameter** and add the following parameters to the query string:</span></span>

    + `name`
    + `task`
    + `duedate`

2. <span data-ttu-id="7e421-168">Clique em **Executar** e verifique se um status 200 retorna.</span><span class="sxs-lookup"><span data-stu-id="7e421-168">Click **Run** and verify that a 200 status is returned.</span></span>

    ![Configurar associação de saída do Cosmos DB](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-test-function.png)

1. <span data-ttu-id="7e421-170">No lado esquerdo do Portal do Azure, expanda a barra de ícones, digite `cosmos` no campo de pesquisa e selecione **Azure Cosmos DB**.</span><span class="sxs-lookup"><span data-stu-id="7e421-170">On the left side of the Azure portal, expand the icon bar, type `cosmos` in the search field, and select **Azure Cosmos DB**.</span></span>

    ![Procure o serviço do Cosmos DB](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-search-cosmos-db.png)

2. <span data-ttu-id="7e421-172">Selecione o banco de dados que você criou e **Data Explorer**.</span><span class="sxs-lookup"><span data-stu-id="7e421-172">Select the database you created, then select **Data Explorer**.</span></span> <span data-ttu-id="7e421-173">Expanda os nós **Coleções**, selecione o novo documento e confirme se o documento contém os valores de cadeia de consulta, juntamente com alguns metadados adicionais.</span><span class="sxs-lookup"><span data-stu-id="7e421-173">Expand the **Collections** nodes, select the new document, and confirm that the document contains your query string values, along with some additional metadata.</span></span> 

    ![Verifique a entrada do Cosmos DB](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-verify-cosmosdb-output.png)

<span data-ttu-id="7e421-175">Você adicionou com êxito uma associação ao gatilho HTTP que armazena dados não estruturados em um banco de dados do Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="7e421-175">You have successfully added a binding to your HTTP trigger that stores unstructured data in a Cosmos DB database.</span></span>

[!INCLUDE [Clean-up section](../../includes/clean-up-section-portal.md)]

## <a name="next-steps"></a><span data-ttu-id="7e421-176">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7e421-176">Next steps</span></span>

[!INCLUDE [functions-quickstart-next-steps](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="7e421-177">Para saber mais sobre a associação a um banco de dados Cosmos DB, veja [Associações do Azure Functions Cosmos DB](functions-bindings-documentdb.md).</span><span class="sxs-lookup"><span data-stu-id="7e421-177">For more information about binding to a Cosmos DB database, see [Azure Functions Cosmos DB bindings](functions-bindings-documentdb.md).</span></span>
