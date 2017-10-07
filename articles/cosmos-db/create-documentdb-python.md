---
title: "Cosmos do Azure DB: Criar um aplicativo com Python e Olá API DocumentDB | Microsoft Docs"
description: "Apresenta um exemplo de código do Python pode usar tooconnect tooand consulta Olá API DocumentDB do Azure Cosmos DB"
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
ms.openlocfilehash: e66965ab493c6ef693e88a3767a401d39e1bde2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-documentdb-api-app-with-python-and-hello-azure-portal"></a><span data-ttu-id="ba839-103">Banco de dados do Azure do Cosmos: Criar um aplicativo de API de documentos com Python e Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="ba839-103">Azure Cosmos DB: Build a DocumentDB API app with Python and hello Azure portal</span></span>

<span data-ttu-id="ba839-104">O BD Cosmos do Azure é o serviço multimodelo de banco de dados distribuído globalmente da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="ba839-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="ba839-105">Você pode criar e consultar documentos, chave/valor e bancos de dados do gráfico, que se beneficiar de distribuição global hello e recursos de escala horizontal no núcleo de saudação do banco de dados do Azure Cosmos rapidamente.</span><span class="sxs-lookup"><span data-stu-id="ba839-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="ba839-106">Este guia rápido demonstra como toocreate uma conta de banco de dados do Azure Cosmos, o banco de dados de documento e a coleção usando Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ba839-106">This quick start demonstrates how toocreate an Azure Cosmos DB account, document database, and collection using hello Azure portal.</span></span> <span data-ttu-id="ba839-107">Você, em seguida, compilar e executar um aplicativo de console criado em Olá [API de Python do DocumentDB](documentdb-sdk-python.md).</span><span class="sxs-lookup"><span data-stu-id="ba839-107">You then build and run a console app built on hello [DocumentDB Python API](documentdb-sdk-python.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ba839-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="ba839-108">Prerequisites</span></span>

* <span data-ttu-id="ba839-109">Antes de executar este exemplo, você deve ter Olá pré-requisitos a seguir:</span><span class="sxs-lookup"><span data-stu-id="ba839-109">Before you can run this sample, you must have hello following prerequisites:</span></span>
    * <span data-ttu-id="ba839-110">[Visual Studio 2015](http://www.visualstudio.com/) ou superior.</span><span class="sxs-lookup"><span data-stu-id="ba839-110">[Visual Studio 2015](http://www.visualstudio.com/) or higher.</span></span>
    * <span data-ttu-id="ba839-111">Ferramentas Python para o Visual Studio do [GitHub](http://microsoft.github.io/PTVS/).</span><span class="sxs-lookup"><span data-stu-id="ba839-111">Python Tools for Visual Studio from [GitHub](http://microsoft.github.io/PTVS/).</span></span> <span data-ttu-id="ba839-112">Este tutorial usa as Ferramentas Python para o VS 2015.</span><span class="sxs-lookup"><span data-stu-id="ba839-112">This tutorial uses Python Tools for VS 2015.</span></span>
    * <span data-ttu-id="ba839-113">Python 2.7 de [python.org](https://www.python.org/downloads/release/python-2712/)</span><span class="sxs-lookup"><span data-stu-id="ba839-113">Python 2.7 from [python.org](https://www.python.org/downloads/release/python-2712/)</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="ba839-114">Crie uma conta de banco de dados</span><span class="sxs-lookup"><span data-stu-id="ba839-114">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a><span data-ttu-id="ba839-115">Adicionar uma coleção</span><span class="sxs-lookup"><span data-stu-id="ba839-115">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-hello-sample-application"></a><span data-ttu-id="ba839-116">Clonar um aplicativo de exemplo hello</span><span class="sxs-lookup"><span data-stu-id="ba839-116">Clone hello sample application</span></span>

<span data-ttu-id="ba839-117">Agora vamos clone uma API de documentos de aplicativo do github, defina a cadeia de caracteres de conexão hello e executá-lo.</span><span class="sxs-lookup"><span data-stu-id="ba839-117">Now let's clone a DocumentDB API app from github, set hello connection string, and run it.</span></span> <span data-ttu-id="ba839-118">Você verá como é fácil toowork com dados programaticamente.</span><span class="sxs-lookup"><span data-stu-id="ba839-118">You see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="ba839-119">Abra uma janela de terminal de git, como git bash, e `cd` tooa diretório de trabalho.</span><span class="sxs-lookup"><span data-stu-id="ba839-119">Open a git terminal window, such as git bash, and `cd` tooa working directory.</span></span>  

2. <span data-ttu-id="ba839-120">Execute Olá repositório de exemplo do comando tooclone Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="ba839-120">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-documentdb-python-getting-started.git
    ```  
## <a name="review-hello-code"></a><span data-ttu-id="ba839-121">Examine o código de saudação</span><span class="sxs-lookup"><span data-stu-id="ba839-121">Review hello code</span></span>

<span data-ttu-id="ba839-122">Vamos fazer uma rápida revisão do que está acontecendo no aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="ba839-122">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="ba839-123">Olá abrir DocumentDBGetStarted.py de arquivo e você encontrará que essas linhas de código criam Olá recursos de banco de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="ba839-123">Open hello DocumentDBGetStarted.py file and you'll find that these lines of code create hello Azure Cosmos DB resources.</span></span> 


* <span data-ttu-id="ba839-124">Olá DocumentClient é inicializado.</span><span class="sxs-lookup"><span data-stu-id="ba839-124">hello DocumentClient is initialized.</span></span>

    ```python
    # Initialize hello Python DocumentDB client
    client = document_client.DocumentClient(config['ENDPOINT'], {'masterKey': config['MASTERKEY']})
    ```

* <span data-ttu-id="ba839-125">Um novo banco de dados é criado.</span><span class="sxs-lookup"><span data-stu-id="ba839-125">A new database is created.</span></span>

    ```python
    # Create a database
    db = client.CreateDatabase({ 'id': config['DOCUMENTDB_DATABASE'] })
    ```

* <span data-ttu-id="ba839-126">Uma nova coleção é criada.</span><span class="sxs-lookup"><span data-stu-id="ba839-126">A new collection is created.</span></span>

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

* <span data-ttu-id="ba839-127">Alguns documentos são criados.</span><span class="sxs-lookup"><span data-stu-id="ba839-127">Some documents are created.</span></span>

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

* <span data-ttu-id="ba839-128">Uma consulta é executada usando SQL</span><span class="sxs-lookup"><span data-stu-id="ba839-128">A query is performed using SQL</span></span>

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

## <a name="update-your-connection-string"></a><span data-ttu-id="ba839-129">Atualizar sua cadeia de conexão</span><span class="sxs-lookup"><span data-stu-id="ba839-129">Update your connection string</span></span>

<span data-ttu-id="ba839-130">Agora volte toohello tooget portal do Azure suas informações de cadeia de caracteres de conexão e copie-o em um aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="ba839-130">Now go back toohello Azure portal tooget your connection string information and copy it into hello app.</span></span>

1. <span data-ttu-id="ba839-131">Em Olá [portal do Azure](http://portal.azure.com/), em seu banco de dados do Cosmos do Azure da conta, na barra de navegação esquerda de saudação, clique em **chaves**e, em seguida, clique em **chaves de leitura-gravação**.</span><span class="sxs-lookup"><span data-stu-id="ba839-131">In hello [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in hello left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="ba839-132">Você usará botões de cópia de saudação na direita de saudação do hello toocopy da tela hello URI e a chave primária em Olá `DocumentDBGetStarted.py` arquivo na próxima etapa do hello.</span><span class="sxs-lookup"><span data-stu-id="ba839-132">You'll use hello copy buttons on hello right side of hello screen toocopy hello URI and Primary Key into hello `DocumentDBGetStarted.py` file in hello next step.</span></span>

    ![Exibir e copiar uma folha de chaves, a chave de acesso no portal do Azure de saudação](./media/create-documentdb-dotnet/keys.png)

2. <span data-ttu-id="ba839-134">Em aberto Olá `DocumentDBGetStarted.py` arquivo.</span><span class="sxs-lookup"><span data-stu-id="ba839-134">In Open hello `DocumentDBGetStarted.py` file.</span></span> 

3. <span data-ttu-id="ba839-135">Copie o valor URI do portal de saudação (usando o botão de cópia de saudação) e torná-lo Olá o valor da chave do ponto de extremidade Olá no `DocumentDBGetStarted.py`.</span><span class="sxs-lookup"><span data-stu-id="ba839-135">Copy your URI value from hello portal (using hello copy button) and make it hello value of hello endpoint key in `DocumentDBGetStarted.py`.</span></span> 

    `config.ENDPOINT : "https://FILLME.documents.azure.com"`

4. <span data-ttu-id="ba839-136">Em seguida, copie o valor de chave primária do portal de saudação e torná-lo Olá valor Olá `config.MASTERKEY` em `DocumentDBGetStarted.py`.</span><span class="sxs-lookup"><span data-stu-id="ba839-136">Then copy your PRIMARY KEY value from hello portal and make it hello value of hello `config.MASTERKEY` in `DocumentDBGetStarted.py`.</span></span> <span data-ttu-id="ba839-137">Agora que você atualizou seu aplicativo com todas as informações de saudação precisa toocommunicate com o banco de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="ba839-137">You've now updated your app with all hello info it needs toocommunicate with Azure Cosmos DB.</span></span> 

    `config.MASTERKEY : "FILLME"`
    
## <a name="run-hello-app"></a><span data-ttu-id="ba839-138">Executar o aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="ba839-138">Run hello app</span></span>
1. <span data-ttu-id="ba839-139">No Visual Studio, clique com botão direito no projeto Olá no **Solution Explorer**, selecione o ambiente atual de Python hello e clique com botão direito.</span><span class="sxs-lookup"><span data-stu-id="ba839-139">In Visual Studio, right-click on hello project in **Solution Explorer**, select hello current Python environment, then right click.</span></span>

2. <span data-ttu-id="ba839-140">Selecione Instalar Pacote do Python e digite **pydocumentdb**</span><span class="sxs-lookup"><span data-stu-id="ba839-140">Select Install Python Package, then type in **pydocumentdb**</span></span>

3. <span data-ttu-id="ba839-141">Execute o aplicativo de hello toorun F5.</span><span class="sxs-lookup"><span data-stu-id="ba839-141">Run F5 toorun hello application.</span></span> <span data-ttu-id="ba839-142">Seu aplicativo é exibido no navegador.</span><span class="sxs-lookup"><span data-stu-id="ba839-142">Your app displays in your browser.</span></span> 

<span data-ttu-id="ba839-143">Agora você pode voltar tooData Explorer e consulte a consulta, modificar e trabalhar com esses novos dados.</span><span class="sxs-lookup"><span data-stu-id="ba839-143">You can now go back tooData Explorer and see query, modify, and work with this new data.</span></span> 

## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="ba839-144">Examine os SLAs em Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="ba839-144">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="ba839-145">Limpar recursos</span><span class="sxs-lookup"><span data-stu-id="ba839-145">Clean up resources</span></span>

<span data-ttu-id="ba839-146">Se você não vai toocontinue toouse este aplicativo, exclua todos os recursos criados por este guia de início rápido Olá portal do Azure com hello etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="ba839-146">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span>

1. <span data-ttu-id="ba839-147">No menu esquerdo de saudação do hello portal do Azure, clique em **grupos de recursos** e clique em nome de saudação do recurso de saudação criado por você.</span><span class="sxs-lookup"><span data-stu-id="ba839-147">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="ba839-148">Na sua página de grupo de recursos, clique em **excluir**, digite o nome de saudação do hello recurso toodelete na caixa de texto de saudação e, em seguida, clique em **excluir**.</span><span class="sxs-lookup"><span data-stu-id="ba839-148">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ba839-149">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ba839-149">Next steps</span></span>

<span data-ttu-id="ba839-150">Este guia de início rápido, você aprendeu como toocreate uma conta de banco de dados do Azure Cosmos, crie uma coleção usando Olá Explorador de dados e executar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ba839-150">In this quickstart, you've learned how toocreate an Azure Cosmos DB account, create a collection using hello Data Explorer, and run an app.</span></span> <span data-ttu-id="ba839-151">Agora você pode importar a conta de banco de dados do Cosmos tooyour dados adicionais.</span><span class="sxs-lookup"><span data-stu-id="ba839-151">You can now import additional data tooyour Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="ba839-152">Importe dados para o banco de dados do Azure Cosmos para Olá API DocumentDB</span><span class="sxs-lookup"><span data-stu-id="ba839-152">Import data into Azure Cosmos DB for hello DocumentDB API</span></span>](import-data.md)


