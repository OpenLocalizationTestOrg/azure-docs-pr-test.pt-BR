---
title: aaaCreate um banco de dados de documento de banco de dados do Azure Cosmos com Java | Microsoft Docs | Microsoft Docs
description: "Apresenta um exemplo de código de Java que você pode usar tooconnect tooand consulta Olá API DocumentDB do Azure Cosmos DB"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 89ea62bb-c620-46d5-baa0-eefd9888557c
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: hero-article
ms.date: 08/02/2017
ms.author: mimig
ms.openlocfilehash: 400c9e7780034d3e28d749e734786e950edad22f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-create-a-document-database-using-java-and-hello-azure-portal"></a>Banco de dados do Azure do Cosmos: Criar um banco de dados de documento usando Java e Olá portal do Azure

O BD Cosmos do Azure é o serviço multimodelo de banco de dados distribuído globalmente da Microsoft. Você pode criar e consultar documentos, chave/valor e bancos de dados do gráfico, que se beneficiar de distribuição global hello e recursos de escala horizontal no núcleo de saudação do banco de dados do Azure Cosmos rapidamente. 

Este guia de início rápido cria um documento de banco de dados usando Olá ferramentas portais do Azure para o banco de dados do Azure Cosmos. Este guia de início rápido também mostra como tooquickly criar um aplicativo de console de Java usando Olá [API Java do DocumentDB](documentdb-sdk-java.md). instruções Olá este guia de início rápido podem ser seguidas em qualquer sistema operacional que é capaz de executar Java. Ao concluir esse início rápido será familiarizado com a criação e modificação de recursos de banco de dados de documento em Olá da interface do usuário ou através de programação, o que for sua preferência.

## <a name="prerequisites"></a>Pré-requisitos

* [Java Development Kit (JDK) 1.7 +](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
    * No Ubuntu, execute `apt-get install default-jdk` tooinstall Olá JDK.
    * Ser toohello tooset se Olá JAVA_HOME ambiente variável toopoint pasta onde Olá JDK está instalado.
* [Baixar](http://maven.apache.org/download.cgi) e [instalar](http://maven.apache.org/install.html) um armazenamento binário [Maven](http://maven.apache.org/)
    * No Ubuntu, você pode executar `apt-get install maven` tooinstall Maven.
* [Git](https://www.git-scm.com/)
    * No Ubuntu, você pode executar `sudo apt-get install git` tooinstall Git.

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a>Criar uma conta de banco de dados

Antes de criar um banco de dados de documento, você precisa toocreate uma conta de banco de dados SQL (documentos) com o banco de dados do Azure Cosmos.

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a>Adicionar uma coleção

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

<a id="add-sample-data"></a>
## <a name="add-sample-data"></a>Adicionar dados de exemplo

Agora você pode adicionar dados tooyour nova coleção usando o Gerenciador de dados.

1. No Explorador de dados, o novo banco de dados de saudação aparece no painel de coleções de hello. Expanda Olá **tarefas** de banco de dados, expanda Olá **itens** coleção, clique em **documentos**e, em seguida, clique em **novos documentos**. 

   ![Criar novos documentos no Explorador de dados no hello portal do Azure](./media/create-documentdb-dotnet/azure-cosmosdb-data-explorer-new-document.png)
  
2. Agora, adicione uma coleção de toohello de documento com hello estrutura a seguir.

     ```json
     {
         "id": "1",
         "category": "personal",
         "name": "groceries",
         "description": "Pick up apples and strawberries.",
         "isComplete": false
     }
     ```

3. Depois de adicionar Olá json toohello **documentos** , clique em **salvar**.

    ![Copiar dados json e clique em Salvar no Explorador de dados em Olá portal do Azure](./media/create-documentdb-dotnet/azure-cosmosdb-data-explorer-save-document.png)

4.  Crie e salve um documento mais onde você insere um valor exclusivo para Olá `id` propriedade e alteração Olá outras propriedades como desejar. Os novos documentos podem ter qualquer estrutura que você deseje, pois o Azure Cosmos DB não impõe nenhum esquema para seus dados.

     Você pode agora usar consultas no Explorador de dados tooretrieve seus dados clicando Olá **Editar filtro** e **Aplicar filtro** botões. Por padrão, o Gerenciador de dados usa `SELECT * FROM c` tooretrieve todos os documentos na coleção hello, mas você pode alterar esse tooa diferente [consulta SQL](documentdb-sql-query.md), como `SELECT * FROM c ORDER BY c._ts DESC`, tooreturn todos os documentos de saudação em ordem decrescente com base em o carimbo de hora. 
 
     Você também pode usar procedimentos de toocreate armazenado no Explorador de dados, UDFs e lógica de negócios do lado do servidor de tooperform de gatilhos, bem como a taxa de transferência de escala. No Explorador de dados expõe todos acesso a dados através de programação interno Olá disponível no hello APIs, mas fornece acesso fácil tooyour dados em Olá portal do Azure.

## <a name="clone-hello-sample-application"></a>Clonar um aplicativo de exemplo hello

Agora vamos alternar tooworking com o código. Vamos, clonar um aplicativo de API de documentos do GitHub, defina a cadeia de caracteres de conexão hello e executá-lo. Você verá como é fácil toowork com dados programaticamente. 

1. Abra uma janela de terminal de git, como git bash, e `CD` tooa diretório de trabalho.  

2. Execute Olá repositório de exemplo do comando tooclone Olá a seguir. 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-documentdb-java-getting-started.git
    ```

## <a name="review-hello-code"></a>Examine o código de saudação

Vamos fazer uma rápida revisão do que está acontecendo no aplicativo hello. Olá abrir `Program.java` arquivo da pasta de \src\GetStarted hello e encontrar essas linhas de código que cria Olá recursos de banco de dados do Azure Cosmos. 

* Olá `DocumentClient` é inicializado.

    ```java
    this.client = new DocumentClient("https://FILLME.documents.azure.com",
            "FILLME", 
            new ConnectionPolicy(),
            ConsistencyLevel.Session);
    ```

* Um novo banco de dados é criado.

    ```java
    Database database = new Database();
    database.setId(databaseName);
    
    this.client.createDatabase(database, null);
    ```

* Uma nova coleção é criada.

    ```java
    DocumentCollection collectionInfo = new DocumentCollection();
    collectionInfo.setId(collectionName);

    ...

    this.client.createCollection(databaseLink, collectionInfo, requestOptions);
    ```

* Alguns documentos são criados.

    ```java
    // Any Java object within your code can be serialized into JSON and written tooAzure Cosmos DB
    Family andersenFamily = new Family();
    andersenFamily.setId("Andersen.1");
    andersenFamily.setLastName("Andersen");
    // More properties

    String collectionLink = String.format("/dbs/%s/colls/%s", databaseName, collectionName);
    this.client.createDocument(collectionLink, family, new RequestOptions(), true);
    ```

* Uma consulta SQL no JSON é executada.

    ```java
    FeedOptions queryOptions = new FeedOptions();
    queryOptions.setPageSize(-1);
    queryOptions.setEnableCrossPartitionQuery(true);

    String collectionLink = String.format("/dbs/%s/colls/%s", databaseName, collectionName);
    FeedResponse<Document> queryResults = this.client.queryDocuments(
        collectionLink,
        "SELECT * FROM Family WHERE Family.lastName = 'Andersen'", queryOptions);

    System.out.println("Running SQL query...");
    for (Document family : queryResults.getQueryIterable()) {
        System.out.println(String.format("\tRead %s", family));
    }
    ```    

## <a name="update-your-connection-string"></a>Atualizar sua cadeia de conexão

Agora volte toohello tooget portal do Azure suas informações de cadeia de caracteres de conexão e copie-o em um aplicativo hello. Isso permitirá toocommunicate seu aplicativo com o banco de dados hospedado.

1. Em Olá [portal do Azure](http://portal.azure.com/), em seu banco de dados do Cosmos do Azure da conta, na barra de navegação esquerda de saudação, clique em **chaves**e, em seguida, clique em **chaves de leitura-gravação**. Você usará botões de cópia de saudação na direita de saudação do hello toocopy da tela hello URI e a chave primária em Olá `Program.java` arquivo na próxima etapa do hello.

    ![Exibir e copiar uma folha de chaves, a chave de acesso no portal do Azure de saudação](./media/create-documentdb-dotnet/keys.png)

2. Em Olá abrir `Program.java` de arquivo, copie o valor URI do portal de saudação (usando o botão de cópia de saudação) e torná-lo Olá valor Olá ponto de extremidade toohello DocumentClient construtor `Program.java`. 

    `"https://FILLME.documents.azure.com"`

4. Em seguida, copie o valor de chave primária do portal hello e cole-o em "FILLME", tornando-Olá segundo parâmetro no construtor de DocumentClient hello. Agora que você atualizou seu aplicativo com todas as informações de saudação precisa toocommunicate com o banco de dados do Azure Cosmos. 
    
## <a name="run-hello-app"></a>Executar o aplicativo hello

1. Na janela do terminal Olá git, `cd` pasta azure-cosmos-db-documentdb-java-getting-started toohello.

2. Na janela do terminal Olá git, digite `mvn package` tooinstall Olá necessário pacotes Java.

3. Na janela do terminal Olá git, execute `mvn exec:java -D exec.mainClass=GetStarted.Program` no hello janela do terminal toostart seu aplicativo Java.

    Na janela do terminal hello, você recebe notificação que Olá FamilyDB banco de dados foi criado e toopress toocontinue uma chave. Pressione um banco de dados de saudação toocreate chave, alterne toohello Explorador de dados e você verá que agora ele contém um banco de dados FamilyDB. Continuar toopress chaves toocreate Olá coleta e hello documentos e, em seguida, executar uma consulta. Quando o projeto de saudação for concluído, recursos de saudação são excluídos de sua conta. 

    ![Exibir e copiar uma folha de chaves, a chave de acesso no portal do Azure de saudação](./media/create-documentdb-java/console-output.png)


## <a name="review-slas-in-hello-azure-portal"></a>Examine os SLAs em Olá portal do Azure

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a>Limpar recursos

Se você não vai toocontinue toouse este aplicativo, exclua todos os recursos criados por este guia de início rápido Olá portal do Azure com hello etapas a seguir:

1. No menu esquerdo de saudação do hello portal do Azure, clique em **grupos de recursos** e clique em nome de saudação do recurso de saudação criado por você. 
2. Na sua página de grupo de recursos, clique em **excluir**, digite o nome de saudação do hello recurso toodelete na caixa de texto de saudação e, em seguida, clique em **excluir**.

## <a name="next-steps"></a>Próximas etapas

Este guia de início rápido, você aprendeu como toocreate uma conta de banco de dados do Azure Cosmos, o banco de dados de documento e a coleção usando Olá Explorador de dados e executar um aplicativo toodo Olá mesmo programaticamente. Agora você pode importar a conta de banco de dados do Cosmos tooyour dados adicionais. 

> [!div class="nextstepaction"]
> [Importar dados no Azure Cosmos DB](import-data.md)


