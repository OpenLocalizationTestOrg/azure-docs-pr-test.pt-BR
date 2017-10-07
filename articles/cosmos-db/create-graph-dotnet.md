---
title: "aaaBuild um aplicativo .NET de banco de dados do Azure Cosmos usando Olá API do Graph | Microsoft Docs"
description: "Apresenta um exemplo de código do .NET podem usar tooconnect tooand consultar o banco de dados do Azure Cosmos"
services: cosmos-db
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: 
ms.assetid: daacbabf-1bb5-497f-92db-079910703046
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 07/28/2017
ms.author: denlee
ms.openlocfilehash: f28790fcb8c9f57c7bb3d844d8276fa04abcc39c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-net-application-using-hello-graph-api"></a>Cosmos do Azure DB: Criar um aplicativo .NET usando Olá API do Graph

O BD Cosmos do Azure é o serviço multimodelo de banco de dados distribuído globalmente da Microsoft. Você pode criar e consultar documentos, chave/valor e bancos de dados do gráfico, que se beneficiar de distribuição global hello e recursos de escala horizontal no núcleo de saudação do banco de dados do Azure Cosmos rapidamente. 

Este guia rápido demonstra como toocreate uma conta de banco de dados do Azure Cosmos, o banco de dados e o uso de gráfico (contêiner) Olá portal do Azure. Você, em seguida, compilar e executar um aplicativo de console criado em Olá [API do Graph](graph-sdk-dotnet.md) (visualização).  

## <a name="prerequisites"></a>Pré-requisitos

Se você ainda não tiver o Visual Studio de 2017 instalado, você pode baixar e usar o hello **livre** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/). Certifique-se de que você habilite **desenvolvimento do Azure** durante a instalação do Visual Studio hello.

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a>Criar uma conta de banco de dados

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <a name="add-a-graph"></a>Adicionar um gráfico

[!INCLUDE [cosmos-db-create-graph](../../includes/cosmos-db-create-graph.md)]

## <a name="clone-hello-sample-application"></a>Clonar um aplicativo de exemplo hello

Agora vamos aplicativo clone uma API do Graph do github, defina a cadeia de caracteres de conexão hello e executá-lo. Você verá como é fácil toowork com dados programaticamente. 

1. Abra uma janela de terminal de git, como git bash, e `cd` tooa diretório de trabalho.  

2. Execute Olá repositório de exemplo do comando tooclone Olá a seguir. 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-graph-dotnet-getting-started.git
    ```

3. Abra o Visual Studio e o arquivo de solução Olá aberto. 

## <a name="review-hello-code"></a>Examine o código de saudação

Vamos fazer uma rápida revisão do que está acontecendo no aplicativo hello. Arquivo Program.cs de saudação aberto e você descobrirá que essas linhas de código criam Olá recursos de banco de dados do Azure Cosmos. 

* Olá DocumentClient é inicializado. Na visualização de hello, adicionamos uma extensão de graph API no cliente de banco de dados do Azure Cosmos hello. Estamos trabalhando em um cliente de gráfico autônomo separado do cliente de banco de dados do Azure Cosmos hello e recursos.

    ```csharp
    using (DocumentClient client = new DocumentClient(
        new Uri(endpoint),
        authKey,
        new ConnectionPolicy { ConnectionMode = ConnectionMode.Direct, ConnectionProtocol = Protocol.Tcp }))
    ```

* Um novo banco de dados é criado.

    ```csharp
    Database database = await client.CreateDatabaseIfNotExistsAsync(new Database { Id = "graphdb" });
    ```

* Um novo gráfico é criado.

    ```csharp
    DocumentCollection graph = await client.CreateDocumentCollectionIfNotExistsAsync(
        UriFactory.CreateDatabaseUri("graphdb"),
        new DocumentCollection { Id = "graph" },
        new RequestOptions { OfferThroughput = 1000 });
    ```
* Uma série de etapas de Gremlin são executadas usando Olá `CreateGremlinQuery` método.

    ```csharp
    // hello CreateGremlinQuery method extensions allow you tooexecute Gremlin queries and iterate
    // results asychronously
    IDocumentQuery<dynamic> query = client.CreateGremlinQuery<dynamic>(graph, "g.V().count()");
    while (query.HasMoreResults)
    {
        foreach (dynamic result in await query.ExecuteNextAsync())
        {
            Console.WriteLine($"\t {JsonConvert.SerializeObject(result)}");
        }
    }

    ```

## <a name="update-your-connection-string"></a>Atualizar sua cadeia de conexão

Agora volte toohello tooget portal do Azure suas informações de cadeia de caracteres de conexão e copie-o em um aplicativo hello.

1. No Visual Studio de 2017, abra o arquivo App. config de saudação. 

2. No hello portal do Azure, na sua conta do banco de dados do Azure Cosmos, clique em **chaves** em Olá barra de navegação esquerda. 

    ![Exibir e copiar uma chave primária em Olá portal do Azure, na página de chaves de saudação](./media/create-graph-dotnet/keys.png)

3. Copiar seu **URI** valor no portal de saudação e torná-lo Olá o valor da chave do ponto de extremidade de saudação no App. config. Você pode usar o botão de cópia de saudação conforme Olá precede o valor de saudação toocopy captura de tela.

    `<add key="Endpoint" value="https://FILLME.documents.azure.com:443" />`

4. Copiar seu **chave primária** valor no portal de saudação e torná-lo Olá o valor da chave de AuthKey Olá no App. config e salve suas alterações. 

    `<add key="AuthKey" value="FILLME" />`

Agora que você atualizou seu aplicativo com todas as informações de saudação precisa toocommunicate com o banco de dados do Azure Cosmos. 

## <a name="run-hello-console-app"></a>Execute o aplicativo de console Olá

1. No Visual Studio, clique em Olá **GraphGetStarted** project no **Solution Explorer** e, em seguida, clique em **gerenciar pacotes NuGet**. 

2. Em Olá NuGet **procurar** , digite *Microsoft.Azure.Graphs* e verifique Olá **inclui a versão de pré-lançamento** caixa. 

3. Resultados de hello, instalar Olá **Microsoft.Azure.Graphs** biblioteca. Isso instala o pacote de biblioteca de extensão do hello Azure Cosmos DB gráfico e todas as dependências.

    Se você receber uma mensagem sobre Analisando alterações toohello solução, clique em **Okey**. Se receber uma mensagem sobre a aceitação da licença, clique em **Aceito**.

4. Clique em CTRL + F5 aplicativo hello de toorun.

   janela de console Olá exibe vértices hello e bordas que está sendo adicionadas toohello gráfico. Ao concluir script hello, pressione ENTER duas vezes tooclose janela do console de saudação. 

## <a name="browse-using-hello-data-explorer"></a>Procurar usando Olá Explorador de dados

Agora você pode voltar tooData Explorer no hello portal do Azure e procurar e consultar seus novos dados de gráfico.

1. No Explorador de dados, o novo banco de dados de saudação aparece no painel de gráficos de hello. Expanda **graphdb**, **graphcollz** e, depois, clique em **Gráfico**.

2. Clique em Olá **Aplicar filtro** padrão de saudação do botão toouse consultar tooview todos os verticies Olá no gráfico de saudação. dados de Olá gerados pelo aplicativo de exemplo hello são exibidos no painel de gráficos hello.

    Você pode aplicar zoom dentro e fora do gráfico hello, expanda o espaço de exibição de gráfico hello, adicionar verticies adicionais e mover a superfície de exibição verticies em hello.

    ![Exibir gráfico Olá no Explorador de dados em Olá portal do Azure](./media/create-graph-dotnet/graph-explorer.png)

## <a name="review-slas-in-hello-azure-portal"></a>Examine os SLAs em Olá portal do Azure

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a>Limpar recursos

Se você não vai toocontinue toouse este aplicativo, exclua todos os recursos criados por este guia de início rápido Olá portal do Azure com hello etapas a seguir: 

1. No menu esquerdo de saudação do hello portal do Azure, clique em **grupos de recursos** e clique em nome de saudação do recurso de saudação criado por você. 
2. Na sua página de grupo de recursos, clique em **excluir**, digite o nome de saudação do hello recurso toodelete na caixa de texto de saudação e, em seguida, clique em **excluir**.

## <a name="next-steps"></a>Próximas etapas

Este guia de início rápido, você aprendeu como toocreate uma conta de banco de dados do Azure Cosmos, criar um gráfico usando Olá Explorador de dados e executar o aplicativo. Agora, você pode criar consultas mais complexas e implementar uma lógica de passagem de gráfico avançada usando o Gremlin. 

> [!div class="nextstepaction"]
> [Consultar usando o Gremlin](tutorial-query-graph.md)

