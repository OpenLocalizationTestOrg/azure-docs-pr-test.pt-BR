---
title: "Cosmos do Azure DB: Criar um aplicativo web com o .NET e Olá API DocumentDB | Microsoft Docs"
description: "Apresenta um exemplo de código do .NET podem usar tooconnect tooand consulta Olá API DocumentDB do Azure Cosmos DB"
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
ms.openlocfilehash: 35517e35d80c48662a51a99814652ffa1121fc5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-documentdb-api-web-app-with-net-and-hello-azure-portal"></a>Banco de dados do Azure do Cosmos: Criar um aplicativo da web API DocumentDB com o .NET e Olá portal do Azure

O BD Cosmos do Azure é o serviço multimodelo de banco de dados distribuído globalmente da Microsoft. Você pode criar e consultar documentos, chave/valor e bancos de dados do gráfico, que se beneficiar de distribuição global hello e recursos de escala horizontal no núcleo de saudação do banco de dados do Azure Cosmos rapidamente. 

Este guia rápido demonstra como toocreate uma conta de banco de dados do Azure Cosmos, o banco de dados de documento e a coleção usando Olá portal do Azure. Você, em seguida, criar e implantar um aplicativo da web lista todo baseado Olá [API .NET do DocumentDB](documentdb-sdk-dotnet.md), conforme mostrado no hello captura de tela a seguir. 

![Aplicativo de tarefas pendentes com os dados de exemplo](./media/create-documentdb-dotnet/azure-comosdb-todo-app-list.png)

## <a name="prerequisites"></a>Pré-requisitos

Se você ainda não tiver o Visual Studio de 2017 instalado, você pode baixar e usar o hello **livre** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/). Certifique-se de que você habilite **desenvolvimento do Azure** durante a instalação do Visual Studio hello.

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

<a id="create-account"></a>
## <a name="create-a-database-account"></a>Criar uma conta de banco de dados

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

<a id="create-collection"></a>
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

     Agora você pode usar consultas no Explorador de dados tooretrieve seus dados. Por padrão, o Gerenciador de dados usa `SELECT * FROM c` tooretrieve todos os documentos na coleção hello, mas você pode alterar esse tooa diferente [consulta SQL](documentdb-sql-query.md), como `SELECT * FROM c ORDER BY c._ts DESC`, tooreturn todos os documentos de saudação em ordem decrescente com base em o carimbo de hora.
 
     Você também pode usar procedimentos de toocreate armazenado no Explorador de dados, UDFs e lógica de negócios do lado do servidor de tooperform de gatilhos, bem como a taxa de transferência de escala. No Explorador de dados expõe todos acesso a dados através de programação interno Olá disponível no hello APIs, mas fornece acesso fácil tooyour dados em Olá portal do Azure.

## <a name="clone-hello-sample-application"></a>Clonar um aplicativo de exemplo hello

Agora vamos alternar tooworking com o código. Vamos, clonar um aplicativo de API de documentos do GitHub, defina a cadeia de caracteres de conexão hello e executá-lo. Você verá como é fácil toowork com dados programaticamente. 

1. Abra uma janela de terminal de git, como git bash, e `CD` tooa diretório de trabalho.  

2. Execute Olá repositório de exemplo do comando tooclone Olá a seguir. 

    ```bash
    git clone https://github.com/Azure-Samples/documentdb-dotnet-todo-app.git
    ```

3. Abra o arquivo de solução de todo Olá no Visual Studio. 

## <a name="review-hello-code"></a>Examine o código de saudação

Vamos fazer uma rápida revisão do que está acontecendo no aplicativo hello. Olá abrir DocumentDBRepository.cs de arquivo e você encontrará que essas linhas de código criam Olá recursos de banco de dados do Azure Cosmos. 

* Olá DocumentClient é inicializada na linha 73.

    ```csharp
    client = new DocumentClient(new Uri(ConfigurationManager.AppSettings["endpoint"]), ConfigurationManager.AppSettings["authKey"]);`
    ```

* Um novo banco de dados é criado na linha 88.

    ```csharp
    await client.CreateDatabaseAsync(new Database { Id = DatabaseId });
    ```

* Uma nova coleção é criada na linha 107.

    ```csharp
    await client.CreateDocumentCollectionAsync(
        UriFactory.CreateDatabaseUri(DatabaseId),
        new DocumentCollection { Id = CollectionId },
        new RequestOptions { OfferThroughput = 1000 });
    ```

## <a name="update-your-connection-string"></a>Atualizar sua cadeia de conexão

Agora volte toohello tooget portal do Azure suas informações de cadeia de caracteres de conexão e copie-o em um aplicativo hello.

1. Em Olá [portal do Azure](http://portal.azure.com/), em seu banco de dados do Cosmos do Azure da conta, na barra de navegação esquerda de saudação, clique em **chaves**e, em seguida, clique em **chaves de leitura-gravação**. Você usará botões de cópia Olá Olá direita da saudação toocopy da tela hello URI e a chave primária no arquivo Web. config de saudação na próxima etapa do hello.

    ![Exibir e copiar uma folha de chaves, a chave de acesso no portal do Azure de saudação](./media/create-documentdb-dotnet/keys.png)

2. No Visual Studio de 2017, abra o arquivo Web. config de saudação. 

3. Copie o valor URI do portal de saudação (usando o botão de cópia de saudação) e torná-lo Olá o valor da chave do ponto de extremidade de Olá no Web. config. 

    `<add key="endpoint" value="FILLME" />`

4. Em seguida, copie o valor de chave primária do portal de saudação e torná-lo Olá valor Olá authKey em Web. config. Agora que você atualizou seu aplicativo com todas as informações de saudação precisa toocommunicate com o banco de dados do Azure Cosmos. 

    `<add key="authKey" value="FILLME" />`
    
## <a name="run-hello-web-app"></a>Executar o aplicativo da web de saudação
1. No Visual Studio, clique com botão direito no projeto Olá no **Solution Explorer** e, em seguida, clique em **gerenciar pacotes NuGet**. 

2. Em Olá NuGet **procurar** , digite *DocumentDB*.

3. Resultados de hello, instalar Olá **Microsoft.Azure.DocumentDB** biblioteca. Isso instala o pacote de Microsoft.Azure.DocumentDB de saudação, bem como todas as dependências.

4. Clique em CTRL + F5 aplicativo hello de toorun. Seu aplicativo é exibido no navegador. 

5. Clique em **criar novo** Olá navegador e criar algumas novas tarefas em seu aplicativo de tarefas pendentes.

   ![Aplicativo de tarefas pendentes com os dados de exemplo](./media/create-documentdb-dotnet/azure-comosdb-todo-app-list.png)

Agora você pode voltar tooData Explorer e consulte a consulta, modificar e trabalhar com esses novos dados. 

## <a name="review-slas-in-hello-azure-portal"></a>Examine os SLAs em Olá portal do Azure

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a>Limpar recursos

Se você não vai toocontinue toouse este aplicativo, exclua todos os recursos criados por este guia de início rápido Olá portal do Azure com hello etapas a seguir:

1. No menu esquerdo de saudação do hello portal do Azure, clique em **grupos de recursos** e clique em nome de saudação do recurso de saudação criado por você. 
2. Na sua página de grupo de recursos, clique em **excluir**, digite o nome de saudação do hello recurso toodelete na caixa de texto de saudação e, em seguida, clique em **excluir**.

## <a name="next-steps"></a>Próximas etapas

Este guia de início rápido, você aprendeu como toocreate uma conta de banco de dados do Azure Cosmos, crie uma coleção usando Olá Explorador de dados e executar um aplicativo web. Agora você pode importar a conta de banco de dados do Cosmos tooyour dados adicionais. 

> [!div class="nextstepaction"]
> [Importar dados no Azure Cosmos DB](import-data.md)


