---
title: 'Azure Cosmos DB: compilar um aplicativo com Python e com a API do DocumentDB | Microsoft Docs'
description: "Apresenta um exemplo de código Python que pode ser usado para se conectar à API do DocumentDB do Azure Cosmos DB e consultá-la"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 51c11be2-af6d-425f-a86a-39cbfe61da29
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: hero-article
ms.date: 05/13/2017
ms.author: mimig
ms.openlocfilehash: 08d467ea27484e7d1d07d6c21b2e04b6525fbcd8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-build-a-documentdb-api-app-with-python-and-the-azure-portal"></a><span data-ttu-id="6148d-103">Azure Cosmos DB: compilar um aplicativo de API do DocumentDB com o Python e com o Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="6148d-103">Azure Cosmos DB: Build a DocumentDB API app with Python and the Azure portal</span></span>

<span data-ttu-id="6148d-104">O Azure Cosmos DB é o serviço multimodelo de banco de dados distribuído globalmente da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="6148d-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="6148d-105">É possível criar e consultar rapidamente documentos, chave/valor e bancos de dados do gráfico. Todos se beneficiam de recursos de escala horizontal e distribuição global no núcleo do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="6148d-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="6148d-106">Este início rápido demonstra como criar uma conta do Azure Cosmos DB, um banco de dados de documento e uma coleção usando o Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="6148d-106">This quick start demonstrates how to create an Azure Cosmos DB account, document database, and collection using the Azure portal.</span></span> <span data-ttu-id="6148d-107">Em seguida, você compila e executa um aplicativo de console criado na [API do Python do DocumentDB](documentdb-sdk-python.md).</span><span class="sxs-lookup"><span data-stu-id="6148d-107">You then build and run a console app built on the [DocumentDB Python API](documentdb-sdk-python.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6148d-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="6148d-108">Prerequisites</span></span>

* <span data-ttu-id="6148d-109">Antes que possa executar esta amostra, você deverá ter os seguintes pré-requisitos:</span><span class="sxs-lookup"><span data-stu-id="6148d-109">Before you can run this sample, you must have the following prerequisites:</span></span>
    * <span data-ttu-id="6148d-110">[Visual Studio 2015](http://www.visualstudio.com/) ou superior.</span><span class="sxs-lookup"><span data-stu-id="6148d-110">[Visual Studio 2015](http://www.visualstudio.com/) or higher.</span></span>
    * <span data-ttu-id="6148d-111">Ferramentas Python para o Visual Studio do [GitHub](http://microsoft.github.io/PTVS/).</span><span class="sxs-lookup"><span data-stu-id="6148d-111">Python Tools for Visual Studio from [GitHub](http://microsoft.github.io/PTVS/).</span></span> <span data-ttu-id="6148d-112">Este tutorial usa as Ferramentas Python para o VS 2015.</span><span class="sxs-lookup"><span data-stu-id="6148d-112">This tutorial uses Python Tools for VS 2015.</span></span>
    * <span data-ttu-id="6148d-113">Python 2.7 de [python.org](https://www.python.org/downloads/release/python-2712/)</span><span class="sxs-lookup"><span data-stu-id="6148d-113">Python 2.7 from [python.org](https://www.python.org/downloads/release/python-2712/)</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="6148d-114">Crie uma conta de banco de dados</span><span class="sxs-lookup"><span data-stu-id="6148d-114">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a><span data-ttu-id="6148d-115">Adicionar uma coleção</span><span class="sxs-lookup"><span data-stu-id="6148d-115">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-the-sample-application"></a><span data-ttu-id="6148d-116">Clonar o aplicativo de exemplo</span><span class="sxs-lookup"><span data-stu-id="6148d-116">Clone the sample application</span></span>

<span data-ttu-id="6148d-117">Agora, vamos clonar um aplicativo de API do DocumentDB do GitHub, defina a cadeia de conexão e execute-o.</span><span class="sxs-lookup"><span data-stu-id="6148d-117">Now let's clone a DocumentDB API app from github, set the connection string, and run it.</span></span> <span data-ttu-id="6148d-118">Você verá como é fácil trabalhar usando dados de forma programática.</span><span class="sxs-lookup"><span data-stu-id="6148d-118">You see how easy it is to work with data programmatically.</span></span> 

1. <span data-ttu-id="6148d-119">Abra uma janela de terminal do Git, como git bash, e `cd` para um diretório de trabalho.</span><span class="sxs-lookup"><span data-stu-id="6148d-119">Open a git terminal window, such as git bash, and `cd` to a working directory.</span></span>  

2. <span data-ttu-id="6148d-120">Execute o comando a seguir para clonar o repositório de exemplo.</span><span class="sxs-lookup"><span data-stu-id="6148d-120">Run the following command to clone the sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-documentdb-python-getting-started.git
    ```  
## <a name="review-the-code"></a><span data-ttu-id="6148d-121">Examine o código</span><span class="sxs-lookup"><span data-stu-id="6148d-121">Review the code</span></span>

<span data-ttu-id="6148d-122">Façamos uma rápida análise do que está acontecendo no aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6148d-122">Let's make a quick review of what's happening in the app.</span></span> <span data-ttu-id="6148d-123">Abra o arquivo DocumentDBGetStarted.py e você verá que essas linhas de código criam os recursos do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="6148d-123">Open the DocumentDBGetStarted.py file and you'll find that these lines of code create the Azure Cosmos DB resources.</span></span> 


* <span data-ttu-id="6148d-124">O DocumentClient é inicializado.</span><span class="sxs-lookup"><span data-stu-id="6148d-124">The DocumentClient is initialized.</span></span>

    ```python
    # Initialize the Python DocumentDB client
    client = document_client.DocumentClient(config['ENDPOINT'], {'masterKey': config['MASTERKEY']})
    ```

* <span data-ttu-id="6148d-125">Um novo banco de dados é criado.</span><span class="sxs-lookup"><span data-stu-id="6148d-125">A new database is created.</span></span>

    ```python
    # Create a database
    db = client.CreateDatabase({ 'id': config['DOCUMENTDB_DATABASE'] })
    ```

* <span data-ttu-id="6148d-126">Uma nova coleção é criada.</span><span class="sxs-lookup"><span data-stu-id="6148d-126">A new collection is created.</span></span>

    ```python
    # Create collection options
    options = {
        'offerEnableRUPerMinuteThroughput': True,
        'offerVersion': "V2",
        'offerThroughput': 400
    }

    # Create a collection
    collection = client.CreateCollection(db['_self'], { 'id': config['DOCUMENTDB_COLLECTION'] }, options)
    ```

* <span data-ttu-id="6148d-127">Alguns documentos são criados.</span><span class="sxs-lookup"><span data-stu-id="6148d-127">Some documents are created.</span></span>

    ```python
    # Create some documents
    document1 = client.CreateDocument(collection['_self'],
        { 
            'id': 'server1',
            'Web Site': 0,
            'Cloud Service': 0,
            'Virtual Machine': 0,
            'name': 'some' 
        })
    ```

* <span data-ttu-id="6148d-128">Uma consulta é executada usando SQL</span><span class="sxs-lookup"><span data-stu-id="6148d-128">A query is performed using SQL</span></span>

    ```python
    # Query them in SQL
    query = { 'query': 'SELECT * FROM server s' }    
            
    options = {} 
    options['enableCrossPartitionQuery'] = True
    options['maxItemCount'] = 2

    result_iterable = client.QueryDocuments(collection['_self'], query, options)
    results = list(result_iterable);

    print(results)
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="6148d-129">Atualizar sua cadeia de conexão</span><span class="sxs-lookup"><span data-stu-id="6148d-129">Update your connection string</span></span>

<span data-ttu-id="6148d-130">Agora, volte ao portal do Azure para obter informações sobre a cadeia de conexão e copiá-las para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6148d-130">Now go back to the Azure portal to get your connection string information and copy it into the app.</span></span>

1. <span data-ttu-id="6148d-131">No [Portal do Azure](http://portal.azure.com/), na sua conta do Azure Cosmos DB, no painel de navegação esquerdo, clique em **Chaves** e, em seguida, clique em **Chaves de leitura/gravação**.</span><span class="sxs-lookup"><span data-stu-id="6148d-131">In the [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in the left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="6148d-132">Você usará os botões de cópia no lado direito da tela para copiar o URI e a Chave Primária para o arquivo `DocumentDBGetStarted.py` na próxima etapa.</span><span class="sxs-lookup"><span data-stu-id="6148d-132">You'll use the copy buttons on the right side of the screen to copy the URI and Primary Key into the `DocumentDBGetStarted.py` file in the next step.</span></span>

    ![Exibir e copiar uma chave de acesso no Portal do Azure, folha Chaves](./media/create-documentdb-dotnet/keys.png)

2. <span data-ttu-id="6148d-134">Abra o arquivo `DocumentDBGetStarted.py`.</span><span class="sxs-lookup"><span data-stu-id="6148d-134">In Open the `DocumentDBGetStarted.py` file.</span></span> 

3. <span data-ttu-id="6148d-135">Copie o valor do URI do portal (usando o botão de cópia) e transforme-o no valor da chave do ponto de extremidade em `DocumentDBGetStarted.py`.</span><span class="sxs-lookup"><span data-stu-id="6148d-135">Copy your URI value from the portal (using the copy button) and make it the value of the endpoint key in `DocumentDBGetStarted.py`.</span></span> 

    `config.ENDPOINT : "https://FILLME.documents.azure.com"`

4. <span data-ttu-id="6148d-136">Em seguida, copie o valor da CHAVE PRIMÁRIA do portal e transforme-o no valor de `config.MASTERKEY` em `DocumentDBGetStarted.py`.</span><span class="sxs-lookup"><span data-stu-id="6148d-136">Then copy your PRIMARY KEY value from the portal and make it the value of the `config.MASTERKEY` in `DocumentDBGetStarted.py`.</span></span> <span data-ttu-id="6148d-137">Agora, você atualizou o aplicativo com todas as informações necessárias para se comunicar com o Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="6148d-137">You've now updated your app with all the info it needs to communicate with Azure Cosmos DB.</span></span> 

    `config.MASTERKEY : "FILLME"`
    
## <a name="run-the-app"></a><span data-ttu-id="6148d-138">Execute o aplicativo</span><span class="sxs-lookup"><span data-stu-id="6148d-138">Run the app</span></span>
1. <span data-ttu-id="6148d-139">No Visual Studio, clique com o botão direito do mouse no projeto no **Gerenciador de Soluções**, selecione o ambiente atual do Python e, em seguida, clique com o botão direito do mouse.</span><span class="sxs-lookup"><span data-stu-id="6148d-139">In Visual Studio, right-click on the project in **Solution Explorer**, select the current Python environment, then right click.</span></span>

2. <span data-ttu-id="6148d-140">Selecione Instalar Pacote do Python e digite **pydocumentdb**</span><span class="sxs-lookup"><span data-stu-id="6148d-140">Select Install Python Package, then type in **pydocumentdb**</span></span>

3. <span data-ttu-id="6148d-141">Pressione F5 para executar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6148d-141">Run F5 to run the application.</span></span> <span data-ttu-id="6148d-142">Seu aplicativo é exibido no navegador.</span><span class="sxs-lookup"><span data-stu-id="6148d-142">Your app displays in your browser.</span></span> 

<span data-ttu-id="6148d-143">Agora, é possível voltar ao Data Explorer e ver a consulta, modificar e trabalhar com esses novos dados.</span><span class="sxs-lookup"><span data-stu-id="6148d-143">You can now go back to Data Explorer and see query, modify, and work with this new data.</span></span> 

## <a name="review-slas-in-the-azure-portal"></a><span data-ttu-id="6148d-144">Examinar SLAs no Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="6148d-144">Review SLAs in the Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="6148d-145">Limpar recursos</span><span class="sxs-lookup"><span data-stu-id="6148d-145">Clean up resources</span></span>

<span data-ttu-id="6148d-146">Se você não continuar usando este aplicativo, exclua todos os recursos criados por esse início rápido no portal do Azure com as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="6148d-146">If you're not going to continue to use this app, delete all resources created by this quickstart in the Azure portal with the following steps:</span></span>

1. <span data-ttu-id="6148d-147">No menu à esquerda no Portal do Azure, clique em **Grupos de recursos** e depois clique no nome do recurso criado.</span><span class="sxs-lookup"><span data-stu-id="6148d-147">From the left-hand menu in the Azure portal, click **Resource groups** and then click the name of the resource you created.</span></span> 
2. <span data-ttu-id="6148d-148">Em sua página de grupo de recursos, clique em **Excluir**, digite o nome do recurso para excluir na caixa de texto e depois clique em **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="6148d-148">On your resource group page, click **Delete**, type the name of the resource to delete in the text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6148d-149">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6148d-149">Next steps</span></span>

<span data-ttu-id="6148d-150">Neste início rápido, você aprendeu como criar uma conta do Azure Cosmos DB, como criar uma coleção usando o Data Explorer e como executar um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6148d-150">In this quickstart, you've learned how to create an Azure Cosmos DB account, create a collection using the Data Explorer, and run an app.</span></span> <span data-ttu-id="6148d-151">Agora, é possível importar outros dados para sua conta do BD Cosmos.</span><span class="sxs-lookup"><span data-stu-id="6148d-151">You can now import additional data to your Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="6148d-152">Importar dados para o Azure Cosmos DB para a API do DocumentDB</span><span class="sxs-lookup"><span data-stu-id="6148d-152">Import data into Azure Cosmos DB for the DocumentDB API</span></span>](import-data.md)


