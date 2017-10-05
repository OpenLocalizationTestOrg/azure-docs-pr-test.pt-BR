---
title: Usar a API do Azure Cosmos DB para MongoDB para compilar um aplicativo Web | Microsoft Docs
description: Um tutorial do Azure Cosmos DB que cria um aplicativo Web de banco de dados online usando a API do MongoDB.
keywords: exemplos do mongodb
services: cosmos-db
author: AndrewHoh
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: 61a2ab3a-2fc3-4d49-a263-ed87c66628f6
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: anhoh
ms.custom: mvc
ms.openlocfilehash: ff277c7f88359cd977424f2e0958c69e2547a2af
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-cosmos-db-connect-to-a-mongodb-app-using-net"></a><span data-ttu-id="44acb-104">Azure Cosmos DB: Conectar-se a um aplicativo do MongoDB usando .NET</span><span class="sxs-lookup"><span data-stu-id="44acb-104">Azure Cosmos DB: Connect to a MongoDB app using .NET</span></span>

<span data-ttu-id="44acb-105">O Azure Cosmos DB é o serviço de banco de dados multimodelo distribuído globalmente da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="44acb-105">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="44acb-106">É possível criar e consultar rapidamente documentos, chave/valor e bancos de dados do gráfico. Todos se beneficiam de recursos de escala horizontal e distribuição global no núcleo do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="44acb-106">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="44acb-107">Este tutorial demonstra como criar uma conta do Azure Cosmos DB usando o Portal do Azure e como criar um banco de dados e coleção para armazenar dados usando a [API do MongoDB](mongodb-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="44acb-107">This tutorial demonstrates how to create an Azure Cosmos DB account using the Azure portal, and how to create a database and collection to store data using the [MongoDB API](mongodb-introduction.md).</span></span> 

<span data-ttu-id="44acb-108">Este tutorial cobre as seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="44acb-108">This tutorial covers the following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="44acb-109">Criar uma conta do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="44acb-109">Create an Azure Cosmos DB account</span></span> 
> * <span data-ttu-id="44acb-110">Atualizar sua cadeia de conexão</span><span class="sxs-lookup"><span data-stu-id="44acb-110">Update your connection string</span></span>
> * <span data-ttu-id="44acb-111">Criar um aplicativo do MongoDB em uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="44acb-111">Create a MongoDB app on a virtual machine</span></span> 


## <a name="create-a-database-account"></a><span data-ttu-id="44acb-112">Crie uma conta de banco de dados</span><span class="sxs-lookup"><span data-stu-id="44acb-112">Create a database account</span></span>

<span data-ttu-id="44acb-113">Vamos começar criando uma conta do Azure Cosmos DB no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="44acb-113">Let's start by creating an Azure Cosmos DB account in the Azure portal.</span></span>  

> [!TIP]
> * <span data-ttu-id="44acb-114">Já tem uma conta do Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="44acb-114">Already have an Azure Cosmos DB account?</span></span> <span data-ttu-id="44acb-115">Nesse caso, pule para [Configurar sua solução do Visual Studio](#SetupVS)</span><span class="sxs-lookup"><span data-stu-id="44acb-115">If so, skip ahead to [Set up your Visual Studio solution](#SetupVS)</span></span>
> * <span data-ttu-id="44acb-116">Você tinha uma conta do Azure DocumentDB?</span><span class="sxs-lookup"><span data-stu-id="44acb-116">Did you have an Azure DocumentDB account?</span></span> <span data-ttu-id="44acb-117">Se sua conta agora é uma conta do Azure Cosmos DB, você pode pular para [Configurar sua solução do Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="44acb-117">If so, your account is now an Azure Cosmos DB account and you can skip ahead to [Set up your Visual Studio solution](#SetupVS).</span></span>  
> * <span data-ttu-id="44acb-118">Se estiver usando o Emulador do Azure Cosmos DB, execute as etapas em [Emulador do Azure Cosmos DB](local-emulator.md) para configurar o emulador e pule para [Configurar sua solução do Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="44acb-118">If you are using the Azure Cosmos DB Emulator, please follow the steps at [Azure Cosmos DB Emulator](local-emulator.md) to setup the emulator and skip ahead to [Set up your Visual Studio Solution](#SetupVS).</span></span> 
>
>

[!INCLUDE [cosmos-db-create-dbaccount-mongodb](../../includes/cosmos-db-create-dbaccount-mongodb.md)]

## <a name="update-your-connection-string"></a><span data-ttu-id="44acb-119">Atualizar sua cadeia de conexão</span><span class="sxs-lookup"><span data-stu-id="44acb-119">Update your connection string</span></span>

1. <span data-ttu-id="44acb-120">No Portal do Azure, na página **Azure Cosmos DB**, selecione a API para a conta do MongoDB.</span><span class="sxs-lookup"><span data-stu-id="44acb-120">In the Azure portal, in the **Azure Cosmos DB** page, select the API for MongoDB account.</span></span> 
2. <span data-ttu-id="44acb-121">Na barra esquerda da folha da conta, clique em **Início rápido**.</span><span class="sxs-lookup"><span data-stu-id="44acb-121">In the left bar of the account blade, click **Quick start**.</span></span> 
3. <span data-ttu-id="44acb-122">Escolha sua plataforma (*driver do .NET*, *driver do Node.js*, *Shell do MongoDB*, *driver do Java*, *driver do Python*).</span><span class="sxs-lookup"><span data-stu-id="44acb-122">Choose your platform (*.NET driver*, *Node.js driver*, *MongoDB Shell*, *Java driver*, *Python driver*).</span></span> <span data-ttu-id="44acb-123">Caso não veja seu driver ou ferramenta na lista, não se preocupe, pois documentamos continuamente mais trechos de código de conexão.</span><span class="sxs-lookup"><span data-stu-id="44acb-123">If you don't see your driver or tool listed, don't worry, we continuously document more connection code snippets.</span></span> 
4. <span data-ttu-id="44acb-124">Copie e cole o trecho de código no seu aplicativo MongoDB e você estará pronto para seguir adiante.</span><span class="sxs-lookup"><span data-stu-id="44acb-124">Copy and paste the code snippet into your MongoDB app, and you are ready to go.</span></span>

## <a name="set-up-your-mongodb-app"></a><span data-ttu-id="44acb-125">Configurar seu aplicativo MongoDB</span><span class="sxs-lookup"><span data-stu-id="44acb-125">Set up your MongoDB app</span></span>

<span data-ttu-id="44acb-126">Você pode usar o tutorial [Criar um aplicativo Web do Azure que se conecte ao MongoDB em execução em uma máquina virtual](../app-service-web/web-sites-dotnet-store-data-mongodb-vm.md), com modificação mínima, para configurar rapidamente um aplicativo MongoDB (localmente ou publicado em um aplicativo Web do Azure) que se conecte a uma conta da API do MongoDB.</span><span class="sxs-lookup"><span data-stu-id="44acb-126">You can use the [Create a web app in Azure that connects to MongoDB running on a virtual machine](../app-service-web/web-sites-dotnet-store-data-mongodb-vm.md) tutorial, with minimal modification, to quickly setup a MongoDB application (either locally or published to an Azure web app) that connects to an API for MongoDB account.</span></span>  

1. <span data-ttu-id="44acb-127">Siga o tutorial, com uma modificação.</span><span class="sxs-lookup"><span data-stu-id="44acb-127">Follow the tutorial, with one modification.</span></span>  <span data-ttu-id="44acb-128">Substitua o código Dal.cs por este:</span><span class="sxs-lookup"><span data-stu-id="44acb-128">Replace the Dal.cs code with this:</span></span>

    ```csharp   
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Web;
    using MyTaskListApp.Models;
    using MongoDB.Driver;
    using MongoDB.Bson;
    using System.Configuration;
    using System.Security.Authentication;
   
    namespace MyTaskListApp
    {
        public class Dal : IDisposable
        {
            //private MongoServer mongoServer = null;
            private bool disposed = false;
   
            // To do: update the connection string with the DNS name
            // or IP address of your server. 
            //For example, "mongodb://testlinux.cloudapp.net
            private string connectionString = "mongodb://localhost:27017";
            private string userName = "<your user name>";
            private string host = "<your host>";
            private string password = "<your password>";
   
            // This sample uses a database named "Tasks" and a 
            //collection named "TasksList".  The database and collection 
            //will be automatically created if they don't already exist.
            private string dbName = "Tasks";
            private string collectionName = "TasksList";
   
            // Default constructor.        
            public Dal()
            {
            }
   
            // Gets all Task items from the MongoDB server.        
            public List<MyTask> GetAllTasks()
            {
                try
                {
                    var collection = GetTasksCollection();
                    return collection.Find(new BsonDocument()).ToList();
                }
                catch (MongoConnectionException)
                {
                    return new List<MyTask>();
                }
            }
   
            // Creates a Task and inserts it into the collection in MongoDB.
            public void CreateTask(MyTask task)
            {
                var collection = GetTasksCollectionForEdit();
                try
                {
                    collection.InsertOne(task);
                }
                catch (MongoCommandException ex)
                {
                    string msg = ex.Message;
                }
            }
   
            private IMongoCollection<MyTask> GetTasksCollection()
            {
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
                var database = client.GetDatabase(dbName);
                var todoTaskCollection = database.GetCollection<MyTask>(collectionName);
                return todoTaskCollection;
            }
   
            private IMongoCollection<MyTask> GetTasksCollectionForEdit()
            {
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
                var database = client.GetDatabase(dbName);
                var todoTaskCollection = database.GetCollection<MyTask>(collectionName);
                return todoTaskCollection;
            }
   
            # region IDisposable
   
            public void Dispose()
            {
                this.Dispose(true);
                GC.SuppressFinalize(this);
            }
   
            protected virtual void Dispose(bool disposing)
            {
                if (!this.disposed)
                {
                    if (disposing)
                    {
                    }
                }
   
                this.disposed = true;
            }
   
            # endregion
        }
    }
    ```

2. <span data-ttu-id="44acb-129">Modifique as seguintes variáveis no arquivo Dal.cs de acordo com as configurações da sua conta na página Chaves do Portal do Azure:</span><span class="sxs-lookup"><span data-stu-id="44acb-129">Modify the following variables in the Dal.cs file per your account settings from the Keys page in the Azure portal:</span></span>

    ```csharp   
    private string userName = "<your user name>";
    private string host = "<your host>";
    private string password = "<your password>";
    ```

3. <span data-ttu-id="44acb-130">Use o aplicativo!</span><span class="sxs-lookup"><span data-stu-id="44acb-130">Use the app!</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="44acb-131">Limpar recursos</span><span class="sxs-lookup"><span data-stu-id="44acb-131">Clean up resources</span></span>

<span data-ttu-id="44acb-132">Se você não continuar usando este aplicativo, siga as seguintes etapas para excluir todos os recursos criados neste tutorial no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="44acb-132">If you're not going to continue to use this app, use the following steps to delete all resources created by this tutorial in the Azure portal.</span></span> 

1. <span data-ttu-id="44acb-133">No menu à esquerda no portal do Azure, clique em **Grupos de recursos** e depois clique no nome do recurso criado.</span><span class="sxs-lookup"><span data-stu-id="44acb-133">From the left-hand menu in the Azure portal, click **Resource groups** and then click the name of the resource you created.</span></span> 
2. <span data-ttu-id="44acb-134">Em sua página de grupo de recursos, clique em **Excluir**, digite o nome do recurso para excluir na caixa de texto e depois clique em **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="44acb-134">On your resource group page, click **Delete**, type the name of the resource to delete in the text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="44acb-135">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="44acb-135">Next steps</span></span>

<span data-ttu-id="44acb-136">Neste tutorial, você fez o seguinte:</span><span class="sxs-lookup"><span data-stu-id="44acb-136">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="44acb-137">Criar uma conta do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="44acb-137">Create an Azure Cosmos DB account</span></span> 
> * <span data-ttu-id="44acb-138">Atualizar sua cadeia de conexão</span><span class="sxs-lookup"><span data-stu-id="44acb-138">Update your connection string</span></span>
> * <span data-ttu-id="44acb-139">Criar um aplicativo do MongoDB em uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="44acb-139">Create a MongoDB app on a virtual machine</span></span>

<span data-ttu-id="44acb-140">Você pode prosseguir para o próximo tutorial e importar seus dados do MongoDB para o Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="44acb-140">You can proceed to the next tutorial and import your MongoDB data to Azure Cosmos DB.</span></span>  

> [!div class="nextstepaction"]
> [<span data-ttu-id="44acb-141">Importar dados do MongoDB no Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="44acb-141">Import MongoDB data into Azure Cosmos DB</span></span>](mongodb-migrate.md)

