---
title: "Cosmos do Azure DB: Criar um aplicativo de console com o Java e Olá MongoDB API | Microsoft Docs"
description: "Apresenta um exemplo de código de Java que você pode usar tooconnect tooand consulta hello Azure Cosmos DB MongoDB API"
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
ms.devlang: java
ms.topic: hero-article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: fbe416f6b20ed2bb83a1d41eb70ffc6e3cee2b61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-mongodb-api-console-app-with-java-and-hello-azure-portal"></a>Banco de dados do Azure do Cosmos: Criar um aplicativo de console do MongoDB API com Java e Olá portal do Azure

O BD Cosmos do Azure é o serviço multimodelo de banco de dados distribuído globalmente da Microsoft. Você pode criar e consultar documentos, chave/valor e bancos de dados do gráfico, que se beneficiar de distribuição global hello e recursos de escala horizontal no núcleo de saudação do banco de dados do Azure Cosmos rapidamente. 

Este guia rápido demonstra como toocreate uma conta de banco de dados do Azure Cosmos, o banco de dados de documento e a coleção usando Olá portal do Azure. Você, em seguida, criar e implantar um aplicativo de console criado em Olá [driver MongoDB Java](https://docs.mongodb.com/ecosystem/drivers/java/). 

## <a name="prerequisites"></a>Pré-requisitos

* Antes de executar este exemplo, você deve ter Olá pré-requisitos a seguir:
   * JDK 1.7 + (execute `apt-get install default-jdk` se você não tiver o JDK)
   * Maven (execute `apt-get install maven` se você não tiver o Maven)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a>Crie uma conta de banco de dados

[!INCLUDE [mongodb-create-dbaccount](../../includes/cosmos-db-create-dbaccount-mongodb.md)]

## <a name="add-a-collection"></a>Adicionar uma coleção

Nomeie o novo banco de dados, **db** e sua nova coleção, **coll**.

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-hello-sample-application"></a>Clonar um aplicativo de exemplo hello

Agora vamos clone uma API do MongoDB aplicativo do github, defina a cadeia de caracteres de conexão hello e executá-lo. Você verá como é fácil toowork com dados programaticamente. 

1. Abra uma janela de terminal de git, como git bash, e `cd` tooa diretório de trabalho.  

2. Execute Olá repositório de exemplo do comando tooclone Olá a seguir. 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-mongodb-java-getting-started.git
    ```

3. Em seguida, abra o arquivo de solução de saudação no Visual Studio. 

## <a name="review-hello-code"></a>Examine o código de saudação

Vamos fazer uma rápida revisão do que está acontecendo no aplicativo hello. Olá abrir `Program.cs` de arquivo e você descobrirá que essas linhas de código criam Olá recursos de banco de dados do Azure Cosmos. 

* Olá DocumentClient é inicializado.

    ```java
    MongoClientURI uri = new MongoClientURI("FILLME");`

    MongoClient mongoClient = new MongoClient(uri);            
    ```

* Um novo banco de dados e uma nova coleção são criados.

    ```java
    MongoDatabase database = mongoClient.getDatabase("db");

    MongoCollection<Document> collection = database.getCollection("coll");
    ```

* Alguns documentos são inseridos usando `MongoCollection.insertOne`

    ```java
    Document document = new Document("fruit", "apple")
    collection.insertOne(document);
    ```

* Algumas consultas são executadas usando `MongoCollection.find`

    ```java
    Document queryResult = collection.find(Filters.eq("fruit", "apple")).first();
    System.out.println(queryResult.toJson());       
    ```

## <a name="update-your-connection-string"></a>Atualizar sua cadeia de conexão

Agora volte toohello tooget portal do Azure suas informações de cadeia de caracteres de conexão e copie-o em um aplicativo hello.

1. Olá conta, selecione **início rápido**, selecione o Java e copie a área de transferência tooyour cadeia de caracteres de conexão de saudação

2. Olá abrir `Program.java` de arquivo, substitua o construtor do hello argumento toohello MongoClientURI com a cadeia de caracteres de conexão de saudação. Agora que você atualizou seu aplicativo com todas as informações de saudação precisa toocommunicate com o banco de dados do Azure Cosmos. 
    
## <a name="run-hello-console-app"></a>Execute o aplicativo de console Olá

1. Executar `mvn package` em um terminal tooinstall necessário módulos npm

2. Executar `mvn exec:java -D exec.mainClass=GetStarted.Program` em um terminal toostart seu aplicativo Java.

Agora você pode usar [Robomongo](mongodb-robomongo.md) / [Studio 3T](mongodb-mongochef.md) tooquery, modificar e trabalhar com esses novos dados.

## <a name="review-slas-in-hello-azure-portal"></a>Examine os SLAs em Olá portal do Azure

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a>Limpar recursos

Se você não vai toocontinue toouse este aplicativo, exclua todos os recursos criados por este guia de início rápido Olá portal do Azure com hello etapas a seguir:

1. No menu esquerdo de saudação do hello portal do Azure, clique em **grupos de recursos** e clique em nome de saudação do recurso de saudação criado por você. 
2. Na sua página de grupo de recursos, clique em **excluir**, digite o nome de saudação do hello recurso toodelete na caixa de texto de saudação e, em seguida, clique em **excluir**.

## <a name="next-steps"></a>Próximas etapas

Este guia de início rápido, você aprendeu como toocreate uma conta de banco de dados do Azure Cosmos, criar uma coleção usando Olá Explorador de dados e executar um aplicativo de console. Agora você pode importar a conta de banco de dados do Cosmos tooyour dados adicionais. 

> [!div class="nextstepaction"]
> [Importar dados do MongoDB no BD Cosmos do Azure](mongodb-migrate.md)


