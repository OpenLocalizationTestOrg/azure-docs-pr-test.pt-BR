---
title: 'Cosmos do Azure DB: Desenvolver com hello API do Graph em .NET | Microsoft Docs'
description: Saiba como toodevelop com a API de documentos do Azure Cosmos DB usando .NET
services: cosmos-db
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: 
ms.assetid: cc8df0be-672b-493e-95a4-26dd52632261
ms.service: cosmos-db
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/10/2017
ms.author: denlee
ms.custom: mvc
ms.openlocfilehash: 12e435d8169aeee6e818dac4a3b66c7a0ec5f2d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-develop-with-hello-graph-api-in-net"></a>Cosmos do Azure DB: Desenvolver com hello API do Graph em .NET
O Azure Cosmos DB é o serviço de banco de dados multimodelo distribuído globalmente da Microsoft. Você pode criar e consultar documentos, chave/valor e bancos de dados do gráfico, que se beneficiar de distribuição global hello e recursos de escala horizontal no núcleo de saudação do banco de dados do Azure Cosmos rapidamente. 

Este tutorial demonstra como toocreate uma conta de banco de dados do Azure Cosmos usando Olá portal do Azure e toocreate um banco de dados do gráfico e o contêiner. aplicativo Hello cria uma rede social simple com quatro pessoas usando Olá [API do Graph](graph-sdk-dotnet.md) (visualização), então atravessa e consultas gráfico hello usando Gremlin.

Este tutorial aborda Olá tarefas a seguir:

> [!div class="checklist"]
> * Criar uma conta do Azure Cosmos DB 
> * Criar um banco de dados do gráfico e um contêiner
> * Serializar objetos too.NET de vértices e bordas
> * Adicionar vértices e bordas
> * Gráfico de saudação de consulta usando Gremlin

## <a name="graphs-in-azure-cosmos-db"></a>Gráficos no Azure Cosmos DB
Você pode usar o banco de dados do Azure Cosmos toocreate, atualizar e gráficos de consulta usando Olá [Microsoft.Azure.Graphs](graph-sdk-dotnet.md) biblioteca. biblioteca de Microsoft.Azure.Graph Olá fornece um método de extensão único `CreateGremlinQuery<T>` sobre Olá `DocumentClient` consultas de Gremlin tooexecute de classe.

Gremlin é uma linguagem de programação funcional que oferece suporte a operações de gravação (DML) e operações de consulta e passagem. Abordaremos alguns exemplos neste artigo tooget seu iniciada com Gremlin. Veja [consultas Gremlin](gremlin-support.md) para obter uma explicação detalhada dos recursos Gremlin disponíveis no Azure Cosmos DB. 

## <a name="prerequisites"></a>Pré-requisitos
Verifique se que você tem o seguinte hello:

* Uma conta ativa do Azure. Se não tiver uma, você poderá se inscrever em uma [conta gratuita](https://azure.microsoft.com/free/). 
    * Como alternativa, você pode usar o hello [emulador do Azure DocumentDB](local-emulator.md) para este tutorial.
* [Visual Studio](http://www.visualstudio.com/).

## <a name="create-database-account"></a>Criar uma conta de banco de dados

Vamos começar criando uma conta de banco de dados do Azure Cosmos em Olá portal do Azure.  

> [!TIP]
> * Já tem uma conta do Azure Cosmos DB? Nesse caso, pular muito[configurar sua solução do Visual Studio](#SetupVS)
> * Você tinha uma conta do Azure DocumentDB? Se assim, sua conta agora é uma conta de banco de dados do Azure Cosmos e poderá pular muito[configurar sua solução do Visual Studio](#SetupVS).  
> * Se você estiver usando hello Azure Cosmos DB emulador, siga as etapas de saudação em [emulador de banco de dados do Azure Cosmos](local-emulator.md) toosetup Olá emulador e pular muito[configurar sua solução do Visual Studio](#SetupVS). 
>
> 

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <a id="SetupVS"></a>Configurar sua solução do Visual Studio
1. Abra o **Visual Studio** no seu computador.
2. Em Olá **arquivo** menu, selecione **novo**e, em seguida, escolha **projeto**.
3. Em Olá **novo projeto** caixa de diálogo, selecione **modelos** / **Visual C#** / **aplicativo de Console (.NET Framework)**, nomeie o projeto e, em seguida, clique em **Okey**.
4. Em Olá **Solution Explorer**, clique com o botão direito no seu novo aplicativo de console, que está em sua solução do Visual Studio, e, em seguida, clique em **gerenciar pacotes NuGet...**
5. Em Olá **NuGet** , clique em **procurar**e o tipo **Microsoft.Azure.Graphs** na caixa de pesquisa hello e seleção Olá **incluem as versões de pré-lançamento**.
6. Nos resultados de saudação localizar **Microsoft.Azure.Graphs** e clique em **instalar**.
   
   Se você receber uma mensagem sobre Analisando alterações toohello solução, clique em **Okey**. Se receber uma mensagem sobre a aceitação da licença, clique em **Aceito**.
   
    Olá `Microsoft.Azure.Graphs` biblioteca fornece um método de extensão único `CreateGremlinQuery<T>` para executar as operações de Gremlin. Gremlin é uma linguagem de programação funcional que oferece suporte a operações de gravação (DML) e operações de consulta e passagem. Abordaremos alguns exemplos neste artigo tooget seu iniciada com Gremlin. [Consultas Gremlin](gremlin-support.md) possui uma explicação detalhada dos recursos Gremlin no Azure Cosmos DB.

## <a id="add-references"></a>Conecte seu aplicativo

Adicionar essas duas constantes e sua variável de *cliente* no seu aplicativo. 

```csharp
string endpoint = ConfigurationManager.AppSettings["Endpoint"]; 
string authKey = ConfigurationManager.AppSettings["AuthKey"]; 
``` 
Em seguida, head fazer toohello [portal do Azure](https://portal.azure.com) tooretrieve sua URL de ponto de extremidade e a chave primária. URL de ponto de extremidade de saudação e a chave primária são necessárias para seu aplicativo toounderstand onde tooconnect e para o banco de dados do Azure Cosmos tootrust conexão do seu aplicativo. 

Olá portal do Azure, navegue conta de banco de dados do Azure Cosmos tooyour em, clique em **chaves**e, em seguida, clique em **chaves de leitura-gravação**. 

Copiar Olá URI do portal de saudação e cole-o sobre `Endpoint` na propriedade do ponto de extremidade de saudação acima. Em seguida, copie Olá chave primária do portal hello e cole-a saudação `AuthKey` propriedade acima. 

! [Captura de tela de saudação portal do Azure usado pelo toocreate tutorial Olá um aplicativo c#. Mostra uma saudação de conta do banco de dados do Azure Cosmos botão chaves realçado em hello Azure Cosmos DB navegação e os valores de chave primária e URI Olá realçados em Olá folha de chaves] [chaves] 
 
## <a id="instantiate"></a>Criar uma instância de saudação DocumentClient 
Em seguida, crie uma nova instância da saudação **DocumentClient**.  

```csharp 
DocumentClient client = new DocumentClient(new Uri(endpoint), authKey); 
``` 

## <a id="create-database"></a>Criar um banco de dados 

Agora, crie um banco de dados do Azure Cosmos [banco de dados](documentdb-resources.md#databases) usando Olá [CreateDatabaseAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) método ou [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) método hello  **DocumentClient** classe da saudação [SDK .NET do DocumentDB](documentdb-sdk-dotnet.md).  

```csharp 
Database database = await client.CreateDatabaseIfNotExistsAsync(new Database { Id = "graphdb" }); 
``` 
 
## <a name="create-a-graph"></a>Criar um gráfico 

Em seguida, crie um contêiner de gráfico usando hello usando Olá [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) método ou [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) método hello **DocumentClient**  classe. Uma coleção é um contêiner de entidades de gráfico. 

```csharp 
DocumentCollection graph = await client.CreateDocumentCollectionIfNotExistsAsync( 
    UriFactory.CreateDatabaseUri("graphdb"), 
    new DocumentCollection { Id = "graphcollz" }, 
    new RequestOptions { OfferThroughput = 1000 }); 
``` 

## <a id="serializing"></a>Serializar objetos too.NET de vértices e bordas
Banco de dados do Azure Cosmos usa Olá [formato com fio GraphSON](gremlin-support.md), que define um esquema JSON para vértices, bordas e propriedades. Hello Azure Cosmos DB .NET SDK inclui JSON.NET como uma dependência, e isso nos permite tooserialize/desserializar GraphSON em objetos .NET que possamos trabalhar com código.

Por exemplo, vamos trabalhar com uma rede social simples com quatro pessoas. Vamos examinar como toocreate `Person` vértices, adicionar `Knows` relações entre elas, em seguida, consultar e percorrer as relações de "friend de amigo" hello gráfico toofind. 

Olá `Microsoft.Azure.Graphs.Elements` namespace fornece `Vertex`, `Edge`, `Property` e `VertexProperty` classes para desserializar objetos do GraphSON respostas toowell definidos pelo .NET.

## <a name="run-gremlin-using-creategremlinquery"></a>Executar Gremlin usando CreateGremlinQuery
Gremlin, assim como o SQL, oferece suporte a operações de consulta, gravação e leitura. Por exemplo, hello trecho a seguir mostra como toocreate vértices, bordas, executam alguns exemplos de consultas usando `CreateGremlinQuery<T>`e iterar assincronamente esses resultados usando `ExecuteNextAsync` e ' HasMoreResults.

```cs
Dictionary<string, string> gremlinQueries = new Dictionary<string, string>
{
    { "Cleanup",        "g.V().drop()" },
    { "AddVertex 1",    "g.addV('person').property('id', 'thomas').property('firstName', 'Thomas').property('age', 44)" },
    { "AddVertex 2",    "g.addV('person').property('id', 'mary').property('firstName', 'Mary').property('lastName', 'Andersen').property('age', 39)" },
    { "AddVertex 3",    "g.addV('person').property('id', 'ben').property('firstName', 'Ben').property('lastName', 'Miller')" },
    { "AddVertex 4",    "g.addV('person').property('id', 'robin').property('firstName', 'Robin').property('lastName', 'Wakefield')" },
    { "AddEdge 1",      "g.V('thomas').addE('knows').to(g.V('mary'))" },
    { "AddEdge 2",      "g.V('thomas').addE('knows').to(g.V('ben'))" },
    { "AddEdge 3",      "g.V('ben').addE('knows').to(g.V('robin'))" },
    { "UpdateVertex",   "g.V('thomas').property('age', 44)" },
    { "CountVertices",  "g.V().count()" },
    { "Filter Range",   "g.V().hasLabel('person').has('age', gt(40))" },
    { "Project",        "g.V().hasLabel('person').values('firstName')" },
    { "Sort",           "g.V().hasLabel('person').order().by('firstName', decr)" },
    { "Traverse",       "g.V('thomas').outE('knows').inV().hasLabel('person')" },
    { "Traverse 2x",    "g.V('thomas').outE('knows').inV().hasLabel('person').outE('knows').inV().hasLabel('person')" },
    { "Loop",           "g.V('thomas').repeat(out()).until(has('id', 'robin')).path()" },
    { "DropEdge",       "g.V('thomas').outE('knows').where(inV().has('id', 'mary')).drop()" },
    { "CountEdges",     "g.E().count()" },
    { "DropVertex",     "g.V('thomas').drop()" },
};

foreach (KeyValuePair<string, string> gremlinQuery in gremlinQueries)
{
    Console.WriteLine($"Running {gremlinQuery.Key}: {gremlinQuery.Value}");

    // hello CreateGremlinQuery method extensions allow you tooexecute Gremlin queries and iterate
    // results asychronously
    IDocumentQuery<dynamic> query = client.CreateGremlinQuery<dynamic>(graph, gremlinQuery.Value);
    while (query.HasMoreResults)
    {
        foreach (dynamic result in await query.ExecuteNextAsync())
        {
            Console.WriteLine($"\t {JsonConvert.SerializeObject(result)}");
        }
    }

    Console.WriteLine();
}
```

## <a name="add-vertices-and-edges"></a>Adicionar vértices e bordas

Vamos dar uma olhada em instruções de Gremlin Olá mostradas na saudação anterior seção mais detalhes. Primeiro, temos alguns vértices usando o método `addV` do Gremlin. Por exemplo, hello trecho a seguir cria um vértice "Thomas Andersen" do tipo "Pessoa", com propriedades de nome, sobrenome e idade.

```cs
// Create a vertex
IDocumentQuery<Vertex> createVertexQuery = client.CreateGremlinQuery<Vertex>(
    graphCollection, 
    "g.addV('person').property('firstName', 'Thomas')");

while (createVertexQuery.HasMoreResults)
{
    Vertex thomas = (await create.ExecuteNextAsync<Vertex>()).First();
}
```

Em seguida, podemos criar algumas arestas entre esses vértices usando o método `addE` do Gremlin. 

```cs
// Add a "knows" edge
IDocumentQuery<Edge> createEdgeQuery = client.CreateGremlinQuery<Edge>(
    graphCollection, 
    "g.V('thomas').addE('knows').to(g.V('mary'))");

while (create.HasMoreResults)
{
    Edge thomasKnowsMaryEdge = (await create.ExecuteNextAsync<Edge>()).First();
}
```

Podemos atualizar um vértice existente usando a etapa `properties` no Gremlin. Podemos ignorar Olá chamada tooexecute Olá consulta `HasMoreResults` e `ExecuteNextAsync` para rest Olá dos exemplos de saudação.

```cs
// Update a vertex
client.CreateGremlinQuery<Vertex>(
    graphCollection, 
    "g.V('thomas').property('age', 45)");
```

Você pode remover bordas e vértices usando a etapa `drop` do Gremlin. Aqui está um trecho de código que mostra como toodelete um vértice e uma borda. Observe que o descarte de um vértice realiza uma exclusão em cascata de saudação associados bordas.

```cs
// Drop an edge
client.CreateGremlinQuery(graphCollection, "g.E('thomasKnowsRobin').drop()");

// Drop a vertex
client.CreateGremlinQuery(graphCollection, "g.V('robin').drop()");
```

## <a name="query-hello-graph"></a>Gráfico de saudação de consulta

Você também pode executar consultas e passagens usando Gremlin. Por exemplo, a saudação trecho de código a seguir mostra como toocount Olá número de vértices no gráfico de saudação:

```cs
// Run a query toocount vertices
IDocumentQuery<int> countQuery = client.CreateGremlinQuery<int>(graphCollection, "g.V().count()");
```
Você pode executar filtros usando do Gremlin `has` e `hasLabel` etapas e combiná-los usando `and`, `or`, e `not` toobuild mais complexo filtros:

```cs
// Run a query with filter
IDocumentQuery<Vertex> personsByAge = client.CreateGremlinQuery<Vertex>(
  graphCollection, 
  "g.V().hasLabel('person').has('age', gt(40))");
```

Você pode projetar determinadas propriedades em resultados da consulta hello usando Olá `values` etapa:

```cs
// Run a query with projection
IDocumentQuery<string> firstNames = client.CreateGremlinQuery<string>(
  graphCollection, 
  $"g.V().hasLabel('person').values('firstName')");
```

Até agora, só vimos operadores de consulta que funcionam em qualquer banco de dados. Gráficos são rápidos e eficientes para operações de passagem quando você precisa toonavigate toorelated bordas e vértices. Vamos encontrar todos os amigos de Thomas. Podemos fazer isso por meio do Gremlin `outE` etapa toofind Olá todas as out-bordas de Thomas, em seguida, passar toohello nos vértices das bordas usando do Gremlin `inV` etapa:

```cs
// Run a traversal (find friends of Thomas)
IDocumentQuery<Vertex> friendsOfThomas = client.CreateGremlinQuery<Vertex>(
  graphCollection,
  "g.V('thomas').outE('knows').inV().hasLabel('person')");
```

executa a consulta seguinte Olá toofind de dois saltos todos "amigos Thomas intitulado dos amigos", chamando `outE` e `inV` duas vezes. 

```cs
// Run a traversal (find friends of friends of Thomas)
IDocumentQuery<Vertex> friendsOfFriendsOfThomas = client.CreateGremlinQuery<Vertex>(
  graphCollection,
  "g.V('thomas').outE('knows').inV().hasLabel('person').outE('knows').inV().hasLabel('person')");
```

Você pode criar consultas mais complexas e implementar a lógica de passagem de gráfico avançado usando Gremlin, incluindo filtro combinação expressões, executar um loop usando Olá `loop` etapa e implementação navegação condicional usando Olá `choose` etapa. Saiba mais sobre o que você pode fazer com o [Suporte do Gremlin](gremlin-support.md)!

Isso é tudo, este tutorial do Azure Cosmos DB está concluído! 

## <a name="clean-up-resources"></a>Limpar recursos

Se você não vai toocontinue toouse esse aplicativo, use Olá seguindo as etapas toodelete todos os recursos criados por esse tutorial Olá portal do Azure.  

1. No menu esquerdo de saudação do hello portal do Azure, clique em **grupos de recursos** e clique em nome de saudação do recurso de saudação criado por você. 
2. Na sua página de grupo de recursos, clique em **excluir**, digite o nome de saudação do hello recurso toodelete na caixa de texto de saudação e, em seguida, clique em **excluir**.

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você fez a seguir hello:

> [!div class="checklist"]
> * Criou uma conta do Azure Cosmos DB 
> * Criou um banco de dados do gráfico e um contêiner
> * Objetos serializados de too.NET de vértices e bordas
> * Adicionou vértices e bordas
> * Gráfico de saudação consultados usando Gremlin

Agora, você pode criar consultas mais complexas e implementar uma lógica de passagem de gráfico avançada usando o Gremlin. 

> [!div class="nextstepaction"]
> [Consultar usando o Gremlin](tutorial-query-graph.md)
