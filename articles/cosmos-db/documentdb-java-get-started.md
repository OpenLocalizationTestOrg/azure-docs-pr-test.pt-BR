---
title: 'Tutorial de NoSQL: API do DocumentDB para o SDK Java do Azure Cosmos DB | Microsoft Docs'
description: "Um tutorial NoSQL que cria um banco de dados online e o aplicativo de console de Java usando Olá API DocumentDB para o banco de dados do Azure Cosmos. O Azure DocumentDB é um banco de dados NoSQL para JSON."
keywords: tutorial do nosql, banco de dados online, aplicativo de console java
services: cosmos-db
documentationcenter: Java
author: arramac
manager: jhubbard
editor: monicar
ms.assetid: 75a9efa1-7edd-4fed-9882-c0177274cbb2
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 05/22/2017
ms.author: arramac
ms.openlocfilehash: 1a298a15ab911d140b9df30ad52cfe0fa07c55b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="nosql-tutorial-build-a-documentdb-api-java-console-application"></a>Tutorial do NoSQL: criar um aplicativo de console em Java da API do DocumentDB
> [!div class="op_single_selector"]
> * [.NET](documentdb-get-started.md)
> * [.NET Core](documentdb-dotnetcore-get-started.md)
> * [Node.js para MongoDB](mongodb-samples.md)
> * [Node.js](documentdb-nodejs-get-started.md)
> * [Java](documentdb-java-get-started.md)
> * [C++](documentdb-cpp-get-started.md)
>  
> 

Bem-vindo toohello NoSQL tutorial para Olá DocumentDB API do SDK de Java do Azure Cosmos DB! Após seguir este tutorial, você terá um aplicativo de console que cria e consulta recursos do Azure Cosmos DB.

Abordamos:

* Criar e conectar-se a conta de banco de dados do Azure Cosmos tooan
* Configurar a sua Solução do Visual Studio
* Criando um banco de dados online
* Criar uma coleção
* Criando documentos JSON
* Consultando Olá coleção
* Criando documentos JSON
* Consultando Olá coleção
* Substituição de um documento
* Exclusão de um documento
* Excluir banco de dados de saudação

Agora vamos começar!

## <a name="prerequisites"></a>Pré-requisitos
Verifique se que você tem o seguinte hello:

* Uma conta ativa do Azure. Se não tiver uma, você poderá se inscrever em uma [conta gratuita](https://azure.microsoft.com/free/). Como alternativa, você pode usar o hello [emulador de banco de dados do Azure Cosmos](local-emulator.md) para este tutorial.
* [Git](https://git-scm.com/downloads)
* [Java Development Kit (JDK) 7 +](http://www.oracle.com/technetwork/java/javase/downloads/index.html).
* [Maven](http://maven.apache.org/download.cgi).

## <a name="step-1-create-an-azure-cosmos-db-account"></a>Etapa 1: Criar uma conta de banco de dados do Azure Cosmos DB
Vamos criar uma conta do Azure Cosmos DB. Se você já tiver uma conta que você deseja toouse, poderá pular muito[projeto do Clone Olá GitHub](#GitClone). Se você estiver usando hello Azure Cosmos DB emulador, siga as etapas de saudação em [emulador de banco de dados do Azure Cosmos](local-emulator.md) tooset backup emulador hello e pular muito[projeto do Clone Olá GitHub](#GitClone).

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a id="GitClone"></a>Etapa 2: Clonar o projeto do GitHub Olá
Você pode começar pela clonagem de repositório do GitHub Olá para [começar a usar o banco de dados do Azure Cosmos e Java](https://github.com/Azure-Samples/documentdb-java-getting-started). Por exemplo, um diretório local execute Olá seguindo o projeto de exemplo de hello tooretrieve localmente.

    git clone git@github.com:Azure-Samples/azure-cosmos-db-documentdb-java-getting-started.git

    cd azure-cosmos-db-documentdb-java-getting-started

Olá diretório contém um `pom.xml` para projeto hello e um `src` pasta que contém o código de origem de Java incluindo `Program.java` que mostra como executar operações simples com o banco de dados do Azure Cosmos como criação de documentos e consultar dados dentro de um coleção. Olá `pom.xml` inclui uma dependência no hello [SDK de Java do DocumentDB em Maven](https://mvnrepository.com/artifact/com.microsoft.azure/azure-documentdb).

    <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>azure-documentdb</artifactId>
        <version>LATEST</version>
    </dependency>

## <a id="Connect"></a>Etapa 3: Conectar-se a conta de banco de dados do Azure Cosmos tooan
Em seguida, head fazer toohello [Portal do Azure](https://portal.azure.com) tooretrieve seu ponto de extremidade e a chave primária do mestre. Hello Azure Cosmos DB de ponto de extremidade e a chave primária são necessárias para seu aplicativo toounderstand onde tooconnect e para o banco de dados do Azure Cosmos tootrust conexão do seu aplicativo.

Olá Portal do Azure, navegue conta de banco de dados do Azure Cosmos tooyour e, em seguida, clique no **chaves**. Copie Olá URI do portal hello e cole-o na `https://FILLME.documents.azure.com` no arquivo de Program.java hello. Cópia Olá chave primária do portal hello e cole-o na `FILLME`.

    this.client = new DocumentClient(
        "https://FILLME.documents.azure.com",
        "FILLME"
        , new ConnectionPolicy(),
        ConsistencyLevel.Session);

![Captura de tela de saudação Portal do Azure usado pelo Olá NoSQL tutorial toocreate um aplicativo de console de Java. Mostra um banco de dados do Azure Cosmos conta, com o hub ACTIVE Olá realçado, Olá realçado na folha de conta do banco de dados do Azure Cosmos Olá de botão de chaves e valores URI, chave primária e SECUNDÁRIA Olá realçados em Olá folha de chaves][keys]

## <a name="step-4-create-a-database"></a>Etapa 4: criar um banco de dados
O banco de dados do Azure Cosmos [banco de dados](documentdb-resources.md#databases) podem ser criados usando Olá [createDatabase](/java/api/com.microsoft.azure.documentdb._document_client.createdatabase) método hello **DocumentClient** classe. Um banco de dados é um contêiner lógico de saudação do armazenamento de documentos JSON particionado em coleções.

    Database database = new Database();
    database.setId("familydb");
    this.client.createDatabase(database, null);

## <a id="CreateColl"></a>Etapa 5: Criar uma coleção
> [!WARNING]
> **createCollection** criará uma nova coleção com uma taxa de transferência reservada, que tem implicações de preço. Para obter mais detalhes, visite a nossa [página de preços](https://azure.microsoft.com/pricing/details/cosmos-db/).
> 
> 

Um [coleção](documentdb-resources.md#collections) podem ser criados usando Olá [createCollection](/java/api/com.microsoft.azure.documentdb._document_client.createcollection) método hello **DocumentClient** classe. Uma coleção é um contêiner de documentos JSON e uma lógica de aplicativo JavaScript associada.


    DocumentCollection collectionInfo = new DocumentCollection();
    collectionInfo.setId("familycoll");

    // Azure Cosmos DB collections can be reserved with throughput specified in request units/second. 
    // Here we create a collection with 400 RU/s.
    RequestOptions requestOptions = new RequestOptions();
    requestOptions.setOfferThroughput(400);

    this.client.createCollection("/dbs/familydb", collectionInfo, requestOptions);

## <a id="CreateDoc"></a>Etapa 6: Criar documentos JSON
Um [documento](documentdb-resources.md#documents) podem ser criados usando Olá [createDocument](/java/api/com.microsoft.azure.documentdb._document_client.createdocument) método hello **DocumentClient** classe. Os documentos são conteúdo JSON (arbitrário) definido pelo usuário. Agora podemos inserir um ou mais documentos. Se você já tiver dados você gostaria que toostore no banco de dados, você pode usar o Azure Cosmos DB [ferramenta de migração de dados](import-data.md) tooimport dados de saudação em um banco de dados.

    // Insert your Java objects as documents 
    Family andersenFamily = new Family();
    andersenFamily.setId("Andersen.1");
    andersenFamily.setLastName("Andersen")

    // More initialization skipped for brevity. You can have nested references
    andersenFamily.setParents(new Parent[] { parent1, parent2 });
    andersenFamily.setDistrict("WA5");
    Address address = new Address();
    address.setCity("Seattle");
    address.setCounty("King");
    address.setState("WA");

    andersenFamily.setAddress(address);
    andersenFamily.setRegistered(true);

    this.client.createDocument("/dbs/familydb/colls/familycoll", family, new RequestOptions(), true);

![Diagrama ilustrando uma relação hierárquica Olá entre conta Olá, banco de dados online Olá, coleção hello e documentos Olá usados pelo Olá NoSQL tutorial toocreate um aplicativo de console do Java](./media/documentdb-get-started/nosql-tutorial-account-database.png)

## <a id="Query"></a>Etapa 7: Consultar recursos do Azure Cosmos DB
O Azure Cosmos DB tem suporte para [consultas](documentdb-sql-query.md) avançadas de documentos JSON armazenados em cada coleção.  Olá, código de exemplo a seguir mostra como tooquery documentos no banco de dados do Azure Cosmos usando a sintaxe SQL com hello [queryDocuments](/java/api/com.microsoft.azure.documentdb._document_client.querydocuments) método.

    FeedResponse<Document> queryResults = this.client.queryDocuments(
        "/dbs/familydb/colls/familycoll",
        "SELECT * FROM Family WHERE Family.lastName = 'Andersen'", 
        null);

    System.out.println("Running SQL query...");
    for (Document family : queryResults.getQueryIterable()) {
        System.out.println(String.format("\tRead %s", family));
    }

## <a id="ReplaceDocument"></a>Etapa 8: substituir o documento JSON
Banco de dados do Azure Cosmos dá suporte à atualização documentos JSON usando Olá [replaceDocument](/java/api/com.microsoft.azure.documentdb._document_client.replacedocument) método.

    // Update a property
    andersenFamily.Children[0].Grade = 6;

    this.client.replaceDocument(
        "/dbs/familydb/colls/familycoll/docs/Andersen.1", 
        andersenFamily,
        null);

## <a id="DeleteDocument"></a>Etapa 9: excluir o documento JSON
Da mesma forma, o banco de dados do Azure Cosmos dá suporte a excluir documentos JSON usando Olá [deleteDocument](/java/api/com.microsoft.azure.documentdb._document_client.deletedocument) método.  

    this.client.delete("/dbs/familydb/colls/familycoll/docs/Andersen.1", null);

## <a id="DeleteDatabase"></a>Etapa 10: Excluir o banco de dados de saudação
Banco de dados excluindo Olá criado remove o banco de dados de saudação e todos os recursos de filhos (coleções, documentos, etc.).

    this.client.deleteDatabase("/dbs/familydb", null);

## <a id="Run"></a>Etapa 11: Executar o aplicativo de console Java inteiro!
aplicativo de hello toorun Olá no console do, navegue toohello a pasta do projeto e compilar usando Maven:
    
    mvn package

Executando `mvn package` baixa a biblioteca de banco de dados do Azure Cosmos mais recente de saudação do Maven e produz `GetStarted-0.0.1-SNAPSHOT.jar`. Em seguida, execute o aplicativo hello executando:

    mvn exec:java -D exec.mainClass=GetStarted.Program

Parabéns! Você concluiu este tutorial do NoSQL e tem um aplicativo de console em Java funcional!

## <a name="next-steps"></a>Próximas etapas
* Quer um tutorial do aplicativo Web Java? Veja [Criar um aplicativo Web com Java usando o Azure Cosmos DB](documentdb-java-application.md).
* Saiba como muito[monitorar uma conta de banco de dados do Azure Cosmos](monitor-accounts.md).
* Executar consultas em nosso conjunto de dados de exemplo hello [parque de consulta](https://www.documentdb.com/sql/demo).
* Saiba mais sobre o modelo de programação de Olá Olá seção desenvolver de saudação [página de documentação do banco de dados do Azure Cosmos](https://azure.microsoft.com/documentation/services/documentdb/).

[keys]: media/documentdb-get-started/nosql-tutorial-keys.png
