---
title: API da aaaUse Azure Cosmos banco de dados para o MongoDB toobuild um aplicativo web | Microsoft Docs
description: "Um tutorial do banco de dados do Azure Cosmos que cria um aplicativo web do banco de dados online usando a API de saudação para o MongoDB."
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
ms.openlocfilehash: 6dfa7fef49fc53ea2fcfcfbad3b3fcf97ac18e94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-connect-tooa-mongodb-app-using-net"></a><span data-ttu-id="53ccf-104">Cosmos do Azure DB: Conecte-se tooa MongoDB aplicativo usando o .NET</span><span class="sxs-lookup"><span data-stu-id="53ccf-104">Azure Cosmos DB: Connect tooa MongoDB app using .NET</span></span>

<span data-ttu-id="53ccf-105">O BD Cosmos do Azure é o serviço multimodelo de banco de dados distribuído globalmente da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="53ccf-105">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="53ccf-106">Você pode criar e consultar documentos, chave/valor e bancos de dados do gráfico, que se beneficiar de distribuição global hello e recursos de escala horizontal no núcleo de saudação do banco de dados do Azure Cosmos rapidamente.</span><span class="sxs-lookup"><span data-stu-id="53ccf-106">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="53ccf-107">Este tutorial demonstra como toocreate uma conta de banco de dados do Azure Cosmos usando Olá portal do Azure e como toocreate um banco de dados e coleta de dados de toostore usando Olá [MongoDB API](mongodb-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="53ccf-107">This tutorial demonstrates how toocreate an Azure Cosmos DB account using hello Azure portal, and how toocreate a database and collection toostore data using hello [MongoDB API](mongodb-introduction.md).</span></span> 

<span data-ttu-id="53ccf-108">Este tutorial aborda Olá tarefas a seguir:</span><span class="sxs-lookup"><span data-stu-id="53ccf-108">This tutorial covers hello following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="53ccf-109">Criar uma conta do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="53ccf-109">Create an Azure Cosmos DB account</span></span> 
> * <span data-ttu-id="53ccf-110">Atualizar sua cadeia de conexão</span><span class="sxs-lookup"><span data-stu-id="53ccf-110">Update your connection string</span></span>
> * <span data-ttu-id="53ccf-111">Criar um aplicativo do MongoDB em uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="53ccf-111">Create a MongoDB app on a virtual machine</span></span> 


## <a name="create-a-database-account"></a><span data-ttu-id="53ccf-112">Criar uma conta de banco de dados</span><span class="sxs-lookup"><span data-stu-id="53ccf-112">Create a database account</span></span>

<span data-ttu-id="53ccf-113">Vamos começar criando uma conta de banco de dados do Azure Cosmos em Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="53ccf-113">Let's start by creating an Azure Cosmos DB account in hello Azure portal.</span></span>  

> [!TIP]
> * <span data-ttu-id="53ccf-114">Já tem uma conta do Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="53ccf-114">Already have an Azure Cosmos DB account?</span></span> <span data-ttu-id="53ccf-115">Nesse caso, pular muito[configurar sua solução do Visual Studio](#SetupVS)</span><span class="sxs-lookup"><span data-stu-id="53ccf-115">If so, skip ahead too[Set up your Visual Studio solution](#SetupVS)</span></span>
> * <span data-ttu-id="53ccf-116">Você tinha uma conta do Azure DocumentDB?</span><span class="sxs-lookup"><span data-stu-id="53ccf-116">Did you have an Azure DocumentDB account?</span></span> <span data-ttu-id="53ccf-117">Se assim, sua conta agora é uma conta de banco de dados do Azure Cosmos e poderá pular muito[configurar sua solução do Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="53ccf-117">If so, your account is now an Azure Cosmos DB account and you can skip ahead too[Set up your Visual Studio solution](#SetupVS).</span></span>  
> * <span data-ttu-id="53ccf-118">Se você estiver usando hello Azure Cosmos DB emulador, siga as etapas de saudação em [emulador de banco de dados do Azure Cosmos](local-emulator.md) toosetup Olá emulador e pular muito[configurar sua solução do Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="53ccf-118">If you are using hello Azure Cosmos DB Emulator, please follow hello steps at [Azure Cosmos DB Emulator](local-emulator.md) toosetup hello emulator and skip ahead too[Set up your Visual Studio Solution](#SetupVS).</span></span> 
>
>

[!INCLUDE [cosmos-db-create-dbaccount-mongodb](../../includes/cosmos-db-create-dbaccount-mongodb.md)]

## <a name="update-your-connection-string"></a><span data-ttu-id="53ccf-119">Atualizar sua cadeia de conexão</span><span class="sxs-lookup"><span data-stu-id="53ccf-119">Update your connection string</span></span>

1. <span data-ttu-id="53ccf-120">Em Olá portal do Azure, na Olá **banco de dados do Azure Cosmos** , selecione Olá API para a conta do MongoDB.</span><span class="sxs-lookup"><span data-stu-id="53ccf-120">In hello Azure portal, in hello **Azure Cosmos DB** page, select hello API for MongoDB account.</span></span> 
2. <span data-ttu-id="53ccf-121">Na barra à esquerda de Olá da folha de conta hello, clique **início rápido**.</span><span class="sxs-lookup"><span data-stu-id="53ccf-121">In hello left bar of hello account blade, click **Quick start**.</span></span> 
3. <span data-ttu-id="53ccf-122">Escolha sua plataforma (*driver do .NET*, *driver do Node.js*, *Shell do MongoDB*, *driver do Java*, *driver do Python*).</span><span class="sxs-lookup"><span data-stu-id="53ccf-122">Choose your platform (*.NET driver*, *Node.js driver*, *MongoDB Shell*, *Java driver*, *Python driver*).</span></span> <span data-ttu-id="53ccf-123">Caso não veja seu driver ou ferramenta na lista, não se preocupe, pois documentamos continuamente mais trechos de código de conexão.</span><span class="sxs-lookup"><span data-stu-id="53ccf-123">If you don't see your driver or tool listed, don't worry, we continuously document more connection code snippets.</span></span> 
4. <span data-ttu-id="53ccf-124">Copie e cole o trecho de código Olá em seu aplicativo do MongoDB, e você está pronto toogo.</span><span class="sxs-lookup"><span data-stu-id="53ccf-124">Copy and paste hello code snippet into your MongoDB app, and you are ready toogo.</span></span>

## <a name="set-up-your-mongodb-app"></a><span data-ttu-id="53ccf-125">Configurar seu aplicativo MongoDB</span><span class="sxs-lookup"><span data-stu-id="53ccf-125">Set up your MongoDB app</span></span>

<span data-ttu-id="53ccf-126">Você pode usar o hello [criar um aplicativo web no Azure que se conecta tooMongoDB em execução em uma máquina virtual](../app-service-web/web-sites-dotnet-store-data-mongodb-vm.md) tutorial com a modificação mínimo, a instalação tooquickly um aplicativo do MongoDB (seja localmente ou aplicativo da web do Azure de tooan publicados) que conecta-se tooan API para a conta do MongoDB.</span><span class="sxs-lookup"><span data-stu-id="53ccf-126">You can use hello [Create a web app in Azure that connects tooMongoDB running on a virtual machine](../app-service-web/web-sites-dotnet-store-data-mongodb-vm.md) tutorial, with minimal modification, tooquickly setup a MongoDB application (either locally or published tooan Azure web app) that connects tooan API for MongoDB account.</span></span>  

1. <span data-ttu-id="53ccf-127">Siga o tutorial hello, com uma modificação.</span><span class="sxs-lookup"><span data-stu-id="53ccf-127">Follow hello tutorial, with one modification.</span></span>  <span data-ttu-id="53ccf-128">Substitua o código de Dal.cs de saudação com isso:</span><span class="sxs-lookup"><span data-stu-id="53ccf-128">Replace hello Dal.cs code with this:</span></span>

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
   
            // toodo: update hello connection string with hello DNS name
            // or IP address of your server. 
            //For example, "mongodb://testlinux.cloudapp.net
            private string connectionString = "mongodb://localhost:27017";
            private string userName = "<your user name>";
            private string host = "<your host>";
            private string password = "<your password>";
   
            // This sample uses a database named "Tasks" and a 
            //collection named "TasksList".  hello database and collection 
            //will be automatically created if they don't already exist.
            private string dbName = "Tasks";
            private string collectionName = "TasksList";
   
            // Default constructor.        
            public Dal()
            {
            }
   
            // Gets all Task items from hello MongoDB server.        
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
   
            // Creates a Task and inserts it into hello collection in MongoDB.
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

2. <span data-ttu-id="53ccf-129">Modificar Olá variáveis no arquivo de Dal.cs Olá por suas configurações de conta a seguir na página de chaves de saudação em Olá portal do Azure:</span><span class="sxs-lookup"><span data-stu-id="53ccf-129">Modify hello following variables in hello Dal.cs file per your account settings from hello Keys page in hello Azure portal:</span></span>

    ```csharp   
    private string userName = "<your user name>";
    private string host = "<your host>";
    private string password = "<your password>";
    ```

3. <span data-ttu-id="53ccf-130">Usar o aplicativo hello!</span><span class="sxs-lookup"><span data-stu-id="53ccf-130">Use hello app!</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="53ccf-131">Limpar recursos</span><span class="sxs-lookup"><span data-stu-id="53ccf-131">Clean up resources</span></span>

<span data-ttu-id="53ccf-132">Se você não vai toocontinue toouse esse aplicativo, use Olá seguindo as etapas toodelete todos os recursos criados por esse tutorial Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="53ccf-132">If you're not going toocontinue toouse this app, use hello following steps toodelete all resources created by this tutorial in hello Azure portal.</span></span> 

1. <span data-ttu-id="53ccf-133">No menu esquerdo de saudação do hello portal do Azure, clique em **grupos de recursos** e clique em nome de saudação do recurso de saudação criado por você.</span><span class="sxs-lookup"><span data-stu-id="53ccf-133">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="53ccf-134">Na sua página de grupo de recursos, clique em **excluir**, digite o nome de saudação do hello recurso toodelete na caixa de texto de saudação e, em seguida, clique em **excluir**.</span><span class="sxs-lookup"><span data-stu-id="53ccf-134">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="53ccf-135">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="53ccf-135">Next steps</span></span>

<span data-ttu-id="53ccf-136">Neste tutorial, você fez a seguir hello:</span><span class="sxs-lookup"><span data-stu-id="53ccf-136">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="53ccf-137">Criar uma conta do Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="53ccf-137">Create an Azure Cosmos DB account</span></span> 
> * <span data-ttu-id="53ccf-138">Atualizar sua cadeia de conexão</span><span class="sxs-lookup"><span data-stu-id="53ccf-138">Update your connection string</span></span>
> * <span data-ttu-id="53ccf-139">Criar um aplicativo do MongoDB em uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="53ccf-139">Create a MongoDB app on a virtual machine</span></span>

<span data-ttu-id="53ccf-140">Você pode continuar toohello tutorial de Avançar e importar sua tooAzure de dados do MongoDB Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="53ccf-140">You can proceed toohello next tutorial and import your MongoDB data tooAzure Cosmos DB.</span></span>  

> [!div class="nextstepaction"]
> [<span data-ttu-id="53ccf-141">Importar dados do MongoDB no BD Cosmos do Azure</span><span class="sxs-lookup"><span data-stu-id="53ccf-141">Import MongoDB data into Azure Cosmos DB</span></span>](mongodb-migrate.md)

