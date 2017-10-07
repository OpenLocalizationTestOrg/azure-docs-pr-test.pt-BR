---
title: "Cosmos do Azure DB: Criar um aplicativo web com o .NET e Olá MongoDB API | Microsoft Docs"
description: "Apresenta um exemplo de código do .NET podem usar tooconnect tooand consulta hello Azure Cosmos DB MongoDB API"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: c85cc47f772a19aaa7181611b75a8acaedbc4c42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-mongodb-api-web-app-with-net-and-hello-azure-portal"></a><span data-ttu-id="7c5d0-103">Banco de dados do Azure do Cosmos: Criar um aplicativo de web do MongoDB API com .NET e Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="7c5d0-103">Azure Cosmos DB: Build a MongoDB API web app with .NET and hello Azure portal</span></span>

<span data-ttu-id="7c5d0-104">O BD Cosmos do Azure é o serviço multimodelo de banco de dados distribuído globalmente da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="7c5d0-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="7c5d0-105">Você pode criar e consultar documentos, chave/valor e bancos de dados do gráfico, que se beneficiar de distribuição global hello e recursos de escala horizontal no núcleo de saudação do banco de dados do Azure Cosmos rapidamente.</span><span class="sxs-lookup"><span data-stu-id="7c5d0-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="7c5d0-106">Este guia rápido demonstra como toocreate uma conta de banco de dados do Azure Cosmos, o banco de dados de documento e a coleção usando Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="7c5d0-106">This quick start demonstrates how toocreate an Azure Cosmos DB account, document database, and collection using hello Azure portal.</span></span> <span data-ttu-id="7c5d0-107">Você, em seguida, criar e implantar um aplicativo web de lista de tarefas criado em Olá [driver MongoDB .NET](https://docs.mongodb.com/ecosystem/drivers/csharp/).</span><span class="sxs-lookup"><span data-stu-id="7c5d0-107">You'll then build and deploy a tasks list web app built on hello [MongoDB .NET driver](https://docs.mongodb.com/ecosystem/drivers/csharp/).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="7c5d0-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="7c5d0-108">Prerequisites</span></span>

<span data-ttu-id="7c5d0-109">Se você ainda não tiver o Visual Studio de 2017 instalado, você pode baixar e usar o hello **livre** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="7c5d0-109">If you don’t already have Visual Studio 2017 installed, you can download and use hello **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="7c5d0-110">Certifique-se de que você habilite **desenvolvimento do Azure** durante a instalação do Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="7c5d0-110">Make sure that you enable **Azure development** during hello Visual Studio setup.</span></span>
[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

<a id="create-account"></a>
## <a name="create-a-database-account"></a><span data-ttu-id="7c5d0-111">Criar uma conta de banco de dados</span><span class="sxs-lookup"><span data-stu-id="7c5d0-111">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount-mongodb.md)]

## <a name="clone-hello-sample-application"></a><span data-ttu-id="7c5d0-112">Clonar um aplicativo de exemplo hello</span><span class="sxs-lookup"><span data-stu-id="7c5d0-112">Clone hello sample application</span></span>

<span data-ttu-id="7c5d0-113">Agora vamos clone uma API do MongoDB aplicativo do github, defina a cadeia de caracteres de conexão hello e executá-lo.</span><span class="sxs-lookup"><span data-stu-id="7c5d0-113">Now let's clone a MongoDB API app from github, set hello connection string, and run it.</span></span> <span data-ttu-id="7c5d0-114">Você verá como é fácil toowork com dados programaticamente.</span><span class="sxs-lookup"><span data-stu-id="7c5d0-114">You'll see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="7c5d0-115">Abra uma janela de terminal de git, como git bash, e `cd` tooa diretório de trabalho.</span><span class="sxs-lookup"><span data-stu-id="7c5d0-115">Open a git terminal window, such as git bash, and `cd` tooa working directory.</span></span>  

2. <span data-ttu-id="7c5d0-116">Execute Olá repositório de exemplo do comando tooclone Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="7c5d0-116">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-mongodb-dotnet-getting-started.git
    ```

3. <span data-ttu-id="7c5d0-117">Em seguida, abra o arquivo de solução de saudação no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7c5d0-117">Then open hello solution file in Visual Studio.</span></span> 

## <a name="review-hello-code"></a><span data-ttu-id="7c5d0-118">Examine o código de saudação</span><span class="sxs-lookup"><span data-stu-id="7c5d0-118">Review hello code</span></span>

<span data-ttu-id="7c5d0-119">Vamos fazer uma rápida revisão do que está acontecendo no aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="7c5d0-119">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="7c5d0-120">Olá abrir **Dal.cs** arquivo hello **DAL** directory e você descobrirá que essas linhas de código criam Olá recursos de banco de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="7c5d0-120">Open hello **Dal.cs** file under hello **DAL** directory and you'll find that these lines of code create hello Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="7c5d0-121">Inicialize Olá Mongo cliente.</span><span class="sxs-lookup"><span data-stu-id="7c5d0-121">Initialize hello Mongo Client.</span></span>

    ```cs
        MongoClientSettings settings = new MongoClientSettings();
        settings.Server = new MongoServerAddress(host, 10255);
        settings.UseSsl = true;
        settings.SslSettings = new SslSettings();
        settings.SslSettings.EnabledSslProtocols = SslProtocols.Tls12;

        MongoIdentity identity = new MongoInternalIdentity(dbName, userName);
        MongoIdentityEvidence evidence = new PasswordEvidence(password);

        settings.Credentials = new List<MongoCredential>()
        {
            new MongoCredential("SCRAM-SHA-1", identity, evidence)
        };

        MongoClient client = new MongoClient(settings);
    ```

* <span data-ttu-id="7c5d0-122">Recupere o banco de dados de saudação e coleção de saudação.</span><span class="sxs-lookup"><span data-stu-id="7c5d0-122">Retrieve hello database and hello collection.</span></span>

    ```cs
    private string dbName = "Tasks";
    private string collectionName = "TasksList";

    var database = client.GetDatabase(dbName);
    var todoTaskCollection = database.GetCollection<MyTask>(collectionName);
    ```

* <span data-ttu-id="7c5d0-123">Recupere todos os documentos.</span><span class="sxs-lookup"><span data-stu-id="7c5d0-123">Retrieve all documents.</span></span>

    ```cs
    collection.Find(new BsonDocument()).ToList();
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="7c5d0-124">Atualizar sua cadeia de conexão</span><span class="sxs-lookup"><span data-stu-id="7c5d0-124">Update your connection string</span></span>

<span data-ttu-id="7c5d0-125">Agora volte toohello tooget portal do Azure suas informações de cadeia de caracteres de conexão e copie-o em um aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="7c5d0-125">Now go back toohello Azure portal tooget your connection string information and copy it into hello app.</span></span>

1. <span data-ttu-id="7c5d0-126">Em Olá [portal do Azure](http://portal.azure.com/), em seu banco de dados do Cosmos do Azure da conta, na barra de navegação esquerda de saudação, clique em **cadeia de caracteres de Conexão**e, em seguida, clique em **chaves de leitura-gravação**.</span><span class="sxs-lookup"><span data-stu-id="7c5d0-126">In hello [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in hello left navigation click **Connection String**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="7c5d0-127">Você usará botões de cópia Olá Olá direita da saudação toocopy da tela hello nome de usuário, senha e Host no arquivo de Dal.cs Olá na próxima etapa do hello.</span><span class="sxs-lookup"><span data-stu-id="7c5d0-127">You'll use hello copy buttons on hello right side of hello screen toocopy hello Username, Password, and Host into hello Dal.cs file in hello next step.</span></span>

2. <span data-ttu-id="7c5d0-128">Olá abrir **Dal.cs** arquivo hello **DAL** directory.</span><span class="sxs-lookup"><span data-stu-id="7c5d0-128">Open hello **Dal.cs** file in hello **DAL** directory.</span></span> 

3. <span data-ttu-id="7c5d0-129">Copiar seu **nome de usuário** valor no portal de saudação (usando o botão de cópia de saudação) e torná-lo Olá valor Olá **nome de usuário** no seu **Dal.cs** arquivo.</span><span class="sxs-lookup"><span data-stu-id="7c5d0-129">Copy your **username** value from hello portal (using hello copy button) and make it hello value of hello **username** in your **Dal.cs** file.</span></span> 

4. <span data-ttu-id="7c5d0-130">Copie seu **host** valor no portal de saudação e torná-lo Olá valor Olá **host** no seu **Dal.cs** arquivo.</span><span class="sxs-lookup"><span data-stu-id="7c5d0-130">Then copy your **host** value from hello portal and make it hello value of hello **host** in your **Dal.cs** file.</span></span> 

5. <span data-ttu-id="7c5d0-131">Finalmente copiar seu **senha** valor no portal de saudação e torná-lo Olá valor Olá **senha** no seu **Dal.cs** arquivo.</span><span class="sxs-lookup"><span data-stu-id="7c5d0-131">Finally copy your **password** value from hello portal and make it hello value of hello **password** in your **Dal.cs** file.</span></span> 

<span data-ttu-id="7c5d0-132">Agora que você atualizou seu aplicativo com todas as informações de saudação precisa toocommunicate com o banco de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="7c5d0-132">You've now updated your app with all hello info it needs toocommunicate with Azure Cosmos DB.</span></span> 
    
## <a name="run-hello-web-app"></a><span data-ttu-id="7c5d0-133">Executar o aplicativo da web de saudação</span><span class="sxs-lookup"><span data-stu-id="7c5d0-133">Run hello web app</span></span>

1. <span data-ttu-id="7c5d0-134">No Visual Studio, clique com botão direito no projeto Olá no **Solution Explorer** e, em seguida, clique em **gerenciar pacotes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="7c5d0-134">In Visual Studio, right-click on hello project in **Solution Explorer** and then click **Manage NuGet Packages**.</span></span> 

2. <span data-ttu-id="7c5d0-135">Em Olá NuGet **procurar** , digite *MongoDB.Driver*.</span><span class="sxs-lookup"><span data-stu-id="7c5d0-135">In hello NuGet **Browse** box, type *MongoDB.Driver*.</span></span>

3. <span data-ttu-id="7c5d0-136">Resultados de hello, instalar Olá **MongoDB.Driver** biblioteca.</span><span class="sxs-lookup"><span data-stu-id="7c5d0-136">From hello results, install hello **MongoDB.Driver** library.</span></span> <span data-ttu-id="7c5d0-137">Isso instala o pacote de MongoDB.Driver de saudação, bem como todas as dependências.</span><span class="sxs-lookup"><span data-stu-id="7c5d0-137">This installs hello MongoDB.Driver package as well as all dependencies.</span></span>

4. <span data-ttu-id="7c5d0-138">Clique em CTRL + F5 aplicativo hello de toorun.</span><span class="sxs-lookup"><span data-stu-id="7c5d0-138">Click CTRL + F5 toorun hello application.</span></span> <span data-ttu-id="7c5d0-139">Seu aplicativo é exibido no navegador.</span><span class="sxs-lookup"><span data-stu-id="7c5d0-139">Your app displays in your browser.</span></span> 

5. <span data-ttu-id="7c5d0-140">Clique em **criar** Olá navegador e criar algumas novas tarefas em seu aplicativo de lista de tarefas.</span><span class="sxs-lookup"><span data-stu-id="7c5d0-140">Click **Create** in hello browser and create a few new tasks in your task list app.</span></span>

## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="7c5d0-141">Examine os SLAs em Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="7c5d0-141">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="7c5d0-142">Limpar recursos</span><span class="sxs-lookup"><span data-stu-id="7c5d0-142">Clean up resources</span></span>

<span data-ttu-id="7c5d0-143">Se você não vai toocontinue toouse este aplicativo, exclua todos os recursos criados por este guia de início rápido Olá portal do Azure com hello etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="7c5d0-143">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span>

1. <span data-ttu-id="7c5d0-144">No menu esquerdo de saudação do hello portal do Azure, clique em **grupos de recursos** e clique em nome de saudação do recurso de saudação criado por você.</span><span class="sxs-lookup"><span data-stu-id="7c5d0-144">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="7c5d0-145">Na sua página de grupo de recursos, clique em **excluir**, digite o nome de saudação do hello recurso toodelete na caixa de texto de saudação e, em seguida, clique em **excluir**.</span><span class="sxs-lookup"><span data-stu-id="7c5d0-145">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7c5d0-146">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7c5d0-146">Next steps</span></span>

<span data-ttu-id="7c5d0-147">Este guia de início rápido, você aprendeu como toocreate uma conta de banco de dados do Azure Cosmos e executar um aplicativo web usando Olá API para o MongoDB.</span><span class="sxs-lookup"><span data-stu-id="7c5d0-147">In this quickstart, you've learned how toocreate an Azure Cosmos DB account and run a web app using hello API for MongoDB.</span></span> <span data-ttu-id="7c5d0-148">Agora você pode importar a conta de banco de dados do Cosmos tooyour dados adicionais.</span><span class="sxs-lookup"><span data-stu-id="7c5d0-148">You can now import additional data tooyour Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="7c5d0-149">Importe dados para o banco de dados do Azure Cosmos para Olá MongoDB API</span><span class="sxs-lookup"><span data-stu-id="7c5d0-149">Import data into Azure Cosmos DB for hello MongoDB API</span></span>](mongodb-migrate.md)

