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
# <a name="azure-cosmos-db-build-a-mongodb-api-web-app-with-net-and-hello-azure-portal"></a>Banco de dados do Azure do Cosmos: Criar um aplicativo de web do MongoDB API com .NET e Olá portal do Azure

O BD Cosmos do Azure é o serviço multimodelo de banco de dados distribuído globalmente da Microsoft. Você pode criar e consultar documentos, chave/valor e bancos de dados do gráfico, que se beneficiar de distribuição global hello e recursos de escala horizontal no núcleo de saudação do banco de dados do Azure Cosmos rapidamente. 

Este guia rápido demonstra como toocreate uma conta de banco de dados do Azure Cosmos, o banco de dados de documento e a coleção usando Olá portal do Azure. Você, em seguida, criar e implantar um aplicativo web de lista de tarefas criado em Olá [driver MongoDB .NET](https://docs.mongodb.com/ecosystem/drivers/csharp/). 

## <a name="prerequisites"></a>Pré-requisitos

Se você ainda não tiver o Visual Studio de 2017 instalado, você pode baixar e usar o hello **livre** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/). Certifique-se de que você habilite **desenvolvimento do Azure** durante a instalação do Visual Studio hello.
[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

<a id="create-account"></a>
## <a name="create-a-database-account"></a>Criar uma conta de banco de dados

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount-mongodb.md)]

## <a name="clone-hello-sample-application"></a>Clonar um aplicativo de exemplo hello

Agora vamos clone uma API do MongoDB aplicativo do github, defina a cadeia de caracteres de conexão hello e executá-lo. Você verá como é fácil toowork com dados programaticamente. 

1. Abra uma janela de terminal de git, como git bash, e `cd` tooa diretório de trabalho.  

2. Execute Olá repositório de exemplo do comando tooclone Olá a seguir. 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-mongodb-dotnet-getting-started.git
    ```

3. Em seguida, abra o arquivo de solução de saudação no Visual Studio. 

## <a name="review-hello-code"></a>Examine o código de saudação

Vamos fazer uma rápida revisão do que está acontecendo no aplicativo hello. Olá abrir **Dal.cs** arquivo hello **DAL** directory e você descobrirá que essas linhas de código criam Olá recursos de banco de dados do Azure Cosmos. 

* Inicialize Olá Mongo cliente.

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

* Recupere o banco de dados de saudação e coleção de saudação.

    ```cs
    private string dbName = "Tasks";
    private string collectionName = "TasksList";

    var database = client.GetDatabase(dbName);
    var todoTaskCollection = database.GetCollection<MyTask>(collectionName);
    ```

* Recupere todos os documentos.

    ```cs
    collection.Find(new BsonDocument()).ToList();
    ```

## <a name="update-your-connection-string"></a>Atualizar sua cadeia de conexão

Agora volte toohello tooget portal do Azure suas informações de cadeia de caracteres de conexão e copie-o em um aplicativo hello.

1. Em Olá [portal do Azure](http://portal.azure.com/), em seu banco de dados do Cosmos do Azure da conta, na barra de navegação esquerda de saudação, clique em **cadeia de caracteres de Conexão**e, em seguida, clique em **chaves de leitura-gravação**. Você usará botões de cópia Olá Olá direita da saudação toocopy da tela hello nome de usuário, senha e Host no arquivo de Dal.cs Olá na próxima etapa do hello.

2. Olá abrir **Dal.cs** arquivo hello **DAL** directory. 

3. Copiar seu **nome de usuário** valor no portal de saudação (usando o botão de cópia de saudação) e torná-lo Olá valor Olá **nome de usuário** no seu **Dal.cs** arquivo. 

4. Copie seu **host** valor no portal de saudação e torná-lo Olá valor Olá **host** no seu **Dal.cs** arquivo. 

5. Finalmente copiar seu **senha** valor no portal de saudação e torná-lo Olá valor Olá **senha** no seu **Dal.cs** arquivo. 

Agora que você atualizou seu aplicativo com todas as informações de saudação precisa toocommunicate com o banco de dados do Azure Cosmos. 
    
## <a name="run-hello-web-app"></a>Executar o aplicativo da web de saudação

1. No Visual Studio, clique com botão direito no projeto Olá no **Solution Explorer** e, em seguida, clique em **gerenciar pacotes NuGet**. 

2. Em Olá NuGet **procurar** , digite *MongoDB.Driver*.

3. Resultados de hello, instalar Olá **MongoDB.Driver** biblioteca. Isso instala o pacote de MongoDB.Driver de saudação, bem como todas as dependências.

4. Clique em CTRL + F5 aplicativo hello de toorun. Seu aplicativo é exibido no navegador. 

5. Clique em **criar** Olá navegador e criar algumas novas tarefas em seu aplicativo de lista de tarefas.

## <a name="review-slas-in-hello-azure-portal"></a>Examine os SLAs em Olá portal do Azure

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a>Limpar recursos

Se você não vai toocontinue toouse este aplicativo, exclua todos os recursos criados por este guia de início rápido Olá portal do Azure com hello etapas a seguir:

1. No menu esquerdo de saudação do hello portal do Azure, clique em **grupos de recursos** e clique em nome de saudação do recurso de saudação criado por você. 
2. Na sua página de grupo de recursos, clique em **excluir**, digite o nome de saudação do hello recurso toodelete na caixa de texto de saudação e, em seguida, clique em **excluir**.

## <a name="next-steps"></a>Próximas etapas

Este guia de início rápido, você aprendeu como toocreate uma conta de banco de dados do Azure Cosmos e executar um aplicativo web usando Olá API para o MongoDB. Agora você pode importar a conta de banco de dados do Cosmos tooyour dados adicionais. 

> [!div class="nextstepaction"]
> [Importe dados para o banco de dados do Azure Cosmos para Olá MongoDB API](mongodb-migrate.md)

