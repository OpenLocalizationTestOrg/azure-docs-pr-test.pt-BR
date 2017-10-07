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
# <a name="azure-cosmos-db-connect-tooa-mongodb-app-using-net"></a>Cosmos do Azure DB: Conecte-se tooa MongoDB aplicativo usando o .NET

O BD Cosmos do Azure é o serviço multimodelo de banco de dados distribuído globalmente da Microsoft. Você pode criar e consultar documentos, chave/valor e bancos de dados do gráfico, que se beneficiar de distribuição global hello e recursos de escala horizontal no núcleo de saudação do banco de dados do Azure Cosmos rapidamente. 

Este tutorial demonstra como toocreate uma conta de banco de dados do Azure Cosmos usando Olá portal do Azure e como toocreate um banco de dados e coleta de dados de toostore usando Olá [MongoDB API](mongodb-introduction.md). 

Este tutorial aborda Olá tarefas a seguir:

> [!div class="checklist"]
> * Criar uma conta do Azure Cosmos DB 
> * Atualizar sua cadeia de conexão
> * Criar um aplicativo do MongoDB em uma máquina virtual 


## <a name="create-a-database-account"></a>Criar uma conta de banco de dados

Vamos começar criando uma conta de banco de dados do Azure Cosmos em Olá portal do Azure.  

> [!TIP]
> * Já tem uma conta do Azure Cosmos DB? Nesse caso, pular muito[configurar sua solução do Visual Studio](#SetupVS)
> * Você tinha uma conta do Azure DocumentDB? Se assim, sua conta agora é uma conta de banco de dados do Azure Cosmos e poderá pular muito[configurar sua solução do Visual Studio](#SetupVS).  
> * Se você estiver usando hello Azure Cosmos DB emulador, siga as etapas de saudação em [emulador de banco de dados do Azure Cosmos](local-emulator.md) toosetup Olá emulador e pular muito[configurar sua solução do Visual Studio](#SetupVS). 
>
>

[!INCLUDE [cosmos-db-create-dbaccount-mongodb](../../includes/cosmos-db-create-dbaccount-mongodb.md)]

## <a name="update-your-connection-string"></a>Atualizar sua cadeia de conexão

1. Em Olá portal do Azure, na Olá **banco de dados do Azure Cosmos** , selecione Olá API para a conta do MongoDB. 
2. Na barra à esquerda de Olá da folha de conta hello, clique **início rápido**. 
3. Escolha sua plataforma (*driver do .NET*, *driver do Node.js*, *Shell do MongoDB*, *driver do Java*, *driver do Python*). Caso não veja seu driver ou ferramenta na lista, não se preocupe, pois documentamos continuamente mais trechos de código de conexão. 
4. Copie e cole o trecho de código Olá em seu aplicativo do MongoDB, e você está pronto toogo.

## <a name="set-up-your-mongodb-app"></a>Configurar seu aplicativo MongoDB

Você pode usar o hello [criar um aplicativo web no Azure que se conecta tooMongoDB em execução em uma máquina virtual](../app-service-web/web-sites-dotnet-store-data-mongodb-vm.md) tutorial com a modificação mínimo, a instalação tooquickly um aplicativo do MongoDB (seja localmente ou aplicativo da web do Azure de tooan publicados) que conecta-se tooan API para a conta do MongoDB.  

1. Siga o tutorial hello, com uma modificação.  Substitua o código de Dal.cs de saudação com isso:

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

2. Modificar Olá variáveis no arquivo de Dal.cs Olá por suas configurações de conta a seguir na página de chaves de saudação em Olá portal do Azure:

    ```csharp   
    private string userName = "<your user name>";
    private string host = "<your host>";
    private string password = "<your password>";
    ```

3. Usar o aplicativo hello!

## <a name="clean-up-resources"></a>Limpar recursos

Se você não vai toocontinue toouse esse aplicativo, use Olá seguindo as etapas toodelete todos os recursos criados por esse tutorial Olá portal do Azure. 

1. No menu esquerdo de saudação do hello portal do Azure, clique em **grupos de recursos** e clique em nome de saudação do recurso de saudação criado por você. 
2. Na sua página de grupo de recursos, clique em **excluir**, digite o nome de saudação do hello recurso toodelete na caixa de texto de saudação e, em seguida, clique em **excluir**.

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você fez a seguir hello:

> [!div class="checklist"]
> * Criar uma conta do Azure Cosmos DB 
> * Atualizar sua cadeia de conexão
> * Criar um aplicativo do MongoDB em uma máquina virtual

Você pode continuar toohello tutorial de Avançar e importar sua tooAzure de dados do MongoDB Cosmos DB.  

> [!div class="nextstepaction"]
> [Importar dados do MongoDB no BD Cosmos do Azure](mongodb-migrate.md)

