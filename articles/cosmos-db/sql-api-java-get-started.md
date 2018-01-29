---
title: 'Tutorial de NoSQL: API do SQL para o SDK Java do Azure Cosmos DB | Microsoft Docs'
description: "Um tutorial do NoSQL que cria um banco de dados online e um aplicativo de console Java usando a API do SQL para o Azure Cosmos DB. O SQL do Azure é um banco de dados NoSQL para JSON."
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
ms.openlocfilehash: 9714234411e96074daae17b4711a52991768bd7b
ms.sourcegitcommit: 821b6306aab244d2feacbd722f60d99881e9d2a4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/18/2017
---
# <a name="nosql-tutorial-build-a-sql-api-java-console-application"></a>Tutorial do NoSQL: criar um aplicativo de console em Java da API do SQL
> [!div class="op_single_selector"]
> * [.NET](sql-api-get-started.md)
> * [.NET Core](sql-api-dotnetcore-get-started.md)
> * [Node.js para MongoDB](mongodb-samples.md)
> * [Node.js](sql-api-nodejs-get-started.md)
> * [Java](sql-api-java-get-started.md)
> * [C++](sql-api-cpp-get-started.md)
>  
> 

[!INCLUDE [cosmos-db-sql-api](../../includes/cosmos-db-sql-api.md)]

Bem-vindo ao tutorial do NoSQL para a API do SQL para o SDK Java do Azure Cosmos DB! Após seguir este tutorial, você terá um aplicativo de console que cria e consulta recursos do Azure Cosmos DB.

Abordamos:

* Criar e conectar-se a uma conta do Azure Cosmos DB
* Configurar a sua Solução do Visual Studio
* Criando um banco de dados online
* Criar uma coleção
* Criando documentos JSON
* Consultar a coleção
* Criando documentos JSON
* Consultar a coleção
* Substituição de um documento
* Exclusão de um documento
* Excluir o banco de dados

Agora vamos começar!

## <a name="prerequisites"></a>pré-requisitos
Verifique se você tem o seguinte:

* Uma conta ativa do Azure. Se não tiver uma, você poderá se inscrever em uma [conta gratuita](https://azure.microsoft.com/free/). 

  [!INCLUDE [cosmos-db-emulator-docdb-api](../../includes/cosmos-db-emulator-docdb-api.md)]

* [Git](https://git-scm.com/downloads).
* [Java Development Kit (JDK) 7 +](http://www.oracle.com/technetwork/java/javase/downloads/index.html).
* [Maven](http://maven.apache.org/download.cgi).

## <a name="step-1-create-an-azure-cosmos-db-account"></a>Etapa 1: Criar uma conta de banco de dados do Azure Cosmos DB
Vamos criar uma conta do Azure Cosmos DB. Se você já tiver uma conta que deseja usar, poderá pular para [Clonar o projeto do GitHub](#GitClone). Se você estiver usando o Emulador do Azure Cosmos DB, siga as etapas no [Emulador do Azure Cosmos DB](local-emulator.md) para configurar o emulador e pular para [Clonar o projeto do GitHub](#GitClone).

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a id="GitClone"></a>Etapa 2: Clonar o projeto do GitHub
Você pode começar clonando o repositório do GitHub para a [Introdução ao Azure Cosmos DB e Java](https://github.com/Azure-Samples/documentdb-java-getting-started). Por exemplo, de um diretório local, execute o seguinte para recuperar o projeto de exemplo localmente.

    git clone git@github.com:Azure-Samples/azure-cosmos-db-documentdb-java-getting-started.git

    cd azure-cosmos-db-documentdb-java-getting-started

O diretório contém um `pom.xml` para o projeto e uma pasta `src` que contém o código-fonte em Java incluindo `Program.java`, que mostra como executar operações simples com o Azure Cosmos DB, como criação de documentos e consulta de dados em uma coleção. O `pom.xml` inclui uma dependência no [SDK do Java do Azure Cosmos DB no Maven](https://mvnrepository.com/artifact/com.microsoft.azure/azure-documentdb).

    <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>azure-documentdb</artifactId>
        <version>LATEST</version>
    </dependency>

## <a id="Connect"></a>Etapa 3: Conectar-se a uma conta do Azure Cosmos DB
Em seguida, retorne ao [Portal do Azure](https://portal.azure.com) para recuperar o ponto de extremidade e a chave mestra primária. O ponto de extremidade e a chave primária do Azure Cosmos DB são necessários para que seu aplicativo reconheça onde deve se conectar e para que o Azure Cosmos DB confie na conexão do seu aplicativo.

No Portal do Azure, navegue até sua conta do Azure Cosmos DB e clique em **Chaves**. Copie o URI do portal e cole-o em `https://FILLME.documents.azure.com` no arquivo Program.java. Em seguida, copie a CHAVE PRIMÁRIA do portal e cole-a em `FILLME`.

    this.client = new DocumentClient(
        "https://FILLME.documents.azure.com",
        "FILLME"
        , new ConnectionPolicy(),
        ConsistencyLevel.Session);

![Captura de tela do Portal do Azure usado pelo tutorial do NoSQL para criar um aplicativo de console em Java. Mostra uma conta do Azure Cosmos DB com o hub ATIVO realçado, o botão CHAVES realçado na folha da conta do Azure Cosmos DB e os valores de URI, de CHAVE PRIMÁRIA e de CHAVE SECUNDÁRIA realçados na folha Chaves][keys]

## <a name="step-4-create-a-database"></a>Etapa 4: criar um banco de dados
Seu [banco de dados](sql-api-resources.md#databases) do Azure Cosmos DB pode ser criado usando o método [createDatabase](/java/api/com.microsoft.azure.documentdb._document_client.createdatabase) da classe **DocumentClient**. Um banco de dados é o contêiner lógico de armazenamento de documentos JSON particionado em coleções.

    Database database = new Database();
    database.setId("familydb");
    this.client.createDatabase(database, null);

## <a id="CreateColl"></a>Etapa 5: Criar uma coleção
> [!WARNING]
> **createCollection** criará uma nova coleção com uma taxa de transferência reservada, que tem implicações de preço. Para obter mais detalhes, visite a nossa [página de preços](https://azure.microsoft.com/pricing/details/cosmos-db/).
> 
> 

Uma [coleção](sql-api-resources.md#collections) pode ser criada usando o método [createCollection](/java/api/com.microsoft.azure.documentdb._document_client.createcollection) da classe **DocumentClient**. Uma coleção é um contêiner de documentos JSON e uma lógica de aplicativo JavaScript associada.


    DocumentCollection collectionInfo = new DocumentCollection();
    collectionInfo.setId("familycoll");

    // Azure Cosmos DB collections can be reserved with throughput specified in request units/second. 
    // Here we create a collection with 400 RU/s.
    RequestOptions requestOptions = new RequestOptions();
    requestOptions.setOfferThroughput(400);

    this.client.createCollection("/dbs/familydb", collectionInfo, requestOptions);

## <a id="CreateDoc"></a>Etapa 6: Criar documentos JSON
Um [documento](sql-api-resources.md#documents) pode ser criado usando o método [createDocument](/java/api/com.microsoft.azure.documentdb._document_client.createdocument) da classe **DocumentClient**. Os documentos são conteúdo JSON (arbitrário) definido pelo usuário. Agora podemos inserir um ou mais documentos. Se já tiver dados que deseje armazenar no banco de dados, você poderá usar a [ferramenta de migração de dados](import-data.md) do Azure Cosmos DB para importar os dados para um banco de dados.

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

![Diagrama que ilustra a relação hierárquica entre a conta, o banco de dados online, a coleção e os documentos usados pelo tutorial do NoSQL para criar um aplicativo de console em Java](./media/sql-api-get-started/nosql-tutorial-account-database.png)

## <a id="Query"></a>Etapa 7: Consultar recursos do Azure Cosmos DB
O Azure Cosmos DB tem suporte para [consultas](sql-api-sql-query.md) avançadas de documentos JSON armazenados em cada coleção.  O código de exemplo a seguir mostra como consultar documentos no Azure Cosmos DB usando a sintaxe SQL com o método [queryDocuments](/java/api/com.microsoft.azure.documentdb._document_client.querydocuments).

    FeedResponse<Document> queryResults = this.client.queryDocuments(
        "/dbs/familydb/colls/familycoll",
        "SELECT * FROM Family WHERE Family.lastName = 'Andersen'", 
        null);

    System.out.println("Running SQL query...");
    for (Document family : queryResults.getQueryIterable()) {
        System.out.println(String.format("\tRead %s", family));
    }

## <a id="ReplaceDocument"></a>Etapa 8: substituir o documento JSON
O Azure Cosmos DB dá suporte à atualização de documentos JSON usando o método [replaceDocument](/java/api/com.microsoft.azure.documentdb._document_client.replacedocument).

    // Update a property
    andersenFamily.Children[0].Grade = 6;

    this.client.replaceDocument(
        "/dbs/familydb/colls/familycoll/docs/Andersen.1", 
        andersenFamily,
        null);

## <a id="DeleteDocument"></a>Etapa 9: excluir o documento JSON
Da mesma forma, o Azure Cosmos DB dá suporte à exclusão de documentos JSON usando o método [deleteDocument](/java/api/com.microsoft.azure.documentdb._document_client.deletedocument).  

    this.client.delete("/dbs/familydb/colls/familycoll/docs/Andersen.1", null);

## <a id="DeleteDatabase"></a>Etapa 10: excluir o banco de dados
Excluir o banco de dados criado remove o banco de dados e todos os recursos filhos (coleções, documentos etc.).

    this.client.deleteDatabase("/dbs/familydb", null);

## <a id="Run"></a>Etapa 11: Executar o aplicativo de console Java inteiro!
Para executar o aplicativo de console, navegue até a pasta de projeto e compile usando o Maven:
    
    mvn package

A execução de `mvn package` baixa a biblioteca mais recente do Azure Cosmos DB do Maven e produz `GetStarted-0.0.1-SNAPSHOT.jar`. Em seguida, execute o aplicativo por meio de:

    mvn exec:java -D exec.mainClass=GetStarted.Program

Parabéns! Você concluiu este tutorial do NoSQL e tem um aplicativo de console em Java funcional!

## <a name="next-steps"></a>Próximas etapas
* Quer um tutorial do aplicativo Web Java? Veja [Criar um aplicativo Web com Java usando o Azure Cosmos DB](sql-api-java-application.md).
* Saiba como [monitorar uma conta do Azure Cosmos DB](monitor-accounts.md).
* Executar consultas em nosso conjunto de dados de exemplo no [Query Playground](https://www.documentdb.com/sql/demo).

[keys]: media/sql-api-get-started/nosql-tutorial-keys.png
