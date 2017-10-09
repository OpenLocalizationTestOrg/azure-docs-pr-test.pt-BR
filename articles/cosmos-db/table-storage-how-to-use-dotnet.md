---
title: "aaaGet de Introdução ao armazenamento de tabela do Azure usando o .NET | Microsoft Docs"
description: "Armazene dados estruturados em nuvem hello usando o armazenamento de tabela do Azure, um repositório de dados NoSQL."
services: cosmos-db
documentationcenter: .net
author: mimig1
manager: jhubbard
editor: tysonn
ms.assetid: fe46d883-7bed-49dd-980e-5c71df36adb3
ms.service: cosmos-db
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 04/10/2017
ms.author: mimig
ms.openlocfilehash: a3e9a4c6f6fd5e724535b86a3f99cd4c161de6de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-table-storage-using-net"></a>Introdução ao armazenamento de Tabelas do Azure usando o .NET
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-tip-include](../../includes/storage-table-cosmos-db-tip-include.md)]

Armazenamento de tabela do Azure é um serviço que armazena estruturado NoSQL armazenam dados na nuvem hello, fornecendo um atributo de chave/com um design schemaless. Como o armazenamento de tabela é schemaless, é fácil tooadapt seus dados como Olá precisam de evolve seu aplicativo. Acessar dados de armazenamento tooTable é rápida e econômica para vários tipos de aplicativos e é geralmente inferiores no custo SQL tradicional para volumes semelhantes de dados.

Você pode usar a tabela armazenamento toostore flexíveis conjuntos de dados como dados de usuário para aplicativos web, catálogos de endereços, informações de dispositivo ou outros tipos de metadados, que seu serviço exigir. Você pode armazenar qualquer número de entidades em uma tabela, e uma conta de armazenamento pode conter qualquer número de tabelas, o limite de capacidade toohello Olá da conta de armazenamento.

### <a name="about-this-tutorial"></a>Sobre este tutorial
Este tutorial mostra como Olá toouse [biblioteca de cliente de armazenamento do Azure para .NET](https://www.nuget.org/packages/WindowsAzure.Storage/) em alguns cenários comuns de armazenamento de tabela do Azure. Esses cenários são apresentados usando exemplos de C# para criar e excluir uma tabela e inserir, atualizar, excluir e consultar dados de tabela.

## <a name="prerequisites"></a>Pré-requisitos

Você precisa Olá toocomplete a seguir este tutorial com êxito:

* [Microsoft Visual Studio](https://www.visualstudio.com/downloads/)
* [Biblioteca do Cliente de Armazenamento do Azure para .NET](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [Gerenciador de Configurações do Azure para .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)
* [Conta de armazenamento do Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-dotnet-client-library-version-include](../../includes/storage-dotnet-client-library-version-include.md)]

### <a name="more-samples"></a>Mais exemplos
Para obter exemplos adicionais usando o Armazenamento de Tabelas, confira [Introdução ao Armazenamento de Tabelas do Azure no .NET](https://azure.microsoft.com/documentation/samples/storage-table-dotnet-getting-started/). Você pode baixar o aplicativo de exemplo hello e executá-lo ou procurar Olá código no GitHub.

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-development-environment-include](../../includes/storage-development-environment-include.md)]

### <a name="add-using-directives"></a>Adicionar diretivas using
Adicione o seguinte Olá **usando** superior de toohello de diretivas de saudação `Program.cs` arquivo:

```csharp
using Microsoft.Azure; // Namespace for CloudConfigurationManager
using Microsoft.WindowsAzure.Storage; // Namespace for CloudStorageAccount
using Microsoft.WindowsAzure.Storage.Table; // Namespace for Table storage types
```

### <a name="parse-hello-connection-string"></a>Analisar a cadeia de conexão Olá
[!INCLUDE [storage-cloud-configuration-manager-include](../../includes/storage-cloud-configuration-manager-include.md)]

### <a name="create-hello-table-service-client"></a>Criar o cliente do serviço de tabela Olá
Olá [CloudTableClient] [ dotnet_CloudTableClient] classe permite que você tooretrieve tabelas e entidades armazenadas no armazenamento de tabela. Aqui está o cliente do serviço de tabela toocreate unidirecional hello:

```csharp
// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
```

Agora você está pronto toowrite código lê e grava o armazenamento tooTable de dados.

## <a name="create-a-table"></a>Criar uma tabela
Este exemplo mostra como toocreate uma tabela se ela ainda não existir:

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Retrieve a reference toohello table.
CloudTable table = tableClient.GetTableReference("people");

// Create hello table if it doesn't exist.
table.CreateIfNotExists();
```

## <a name="add-an-entity-tooa-table"></a>Adicionar uma tabela de entidade tooa
Entidades são mapeadas tooC # objetos por meio de uma classe personalizada derivada de [TableEntity][dotnet_TableEntity]. tooadd uma tabela de tooa de entidade, crie uma classe que define as propriedades de saudação da entidade. Olá código a seguir define uma classe de entidade que usa o nome saudação do cliente como chave de linha de saudação e último nome como chave de partição de saudação. Juntas, partição de uma entidade e a chave de linha identificá-lo exclusivamente na tabela de saudação. Entidades com hello a mesma chave de partição pode ser consultado mais rápido do que as entidades com diferentes chaves de partição, mas usar chaves de partição diversas permite maior escalabilidade de operações paralelas. Entidades toobe armazenado nas tabelas deve ser de um tipo com suporte, por exemplo derivado de saudação [TableEntity] [ dotnet_TableEntity] classe. Você gostaria que toostore em uma tabela de propriedades de entidade devem ser propriedades públicas do tipo hello e dar suporte a obtenção e configuração de valores de. Além disso, o tipo de entidade *deve* expor um construtor sem parâmetros.

```csharp
public class CustomerEntity : TableEntity
{
    public CustomerEntity(string lastName, string firstName)
    {
        this.PartitionKey = lastName;
        this.RowKey = firstName;
    }

    public CustomerEntity() { }

    public string Email { get; set; }

    public string PhoneNumber { get; set; }
}
```

Operações de tabela que envolvem entidades são realizadas por meio de saudação [CloudTable] [ dotnet_CloudTable] objeto que você criou anteriormente na seção "Criar uma tabela", Olá. Olá toobe operação realizada é representado por um [TableOperation] [ dotnet_TableOperation] objeto. Olá, exemplo de código a seguir mostra a criação Olá de saudação [CloudTable] [ dotnet_CloudTable] objeto e, em seguida, um **CustomerEntity** objeto. operação de saudação tooprepare, uma [TableOperation] [ dotnet_TableOperation] objeto é criado entidade do cliente Olá tooinsert na tabela de saudação. Por fim, a operação de saudação é executada chamando [CloudTable][dotnet_CloudTable].[ Executar][dotnet_CloudTable_Execute].

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable object that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create a new customer entity.
CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
customer1.Email = "Walter@contoso.com";
customer1.PhoneNumber = "425-555-0101";

// Create hello TableOperation object that inserts hello customer entity.
TableOperation insertOperation = TableOperation.Insert(customer1);

// Execute hello insert operation.
table.Execute(insertOperation);
```

## <a name="insert-a-batch-of-entities"></a>Inserir um lote de entidades
Você pode inserir um lote de entidades em uma tabela em uma única operação de gravação. Algumas outras observações sobre operações em lote:

* Você pode executar inserções, atualizações e exclusões em Olá mesmo única operação em lote.
* Uma operação em lote único pode incluir o too100 entidades.
* Todas as entidades em uma única operação de lote devem ter Olá mesma chave de partição.
* Embora seja possível tooperform uma consulta como uma operação em lote, deve ser a única operação Olá em lote de saudação.

Olá exemplo de código a seguir cria dois objetos de entidade e adiciona cada muito[TableBatchOperation] [ dotnet_TableBatchOperation] usando Olá [inserir] [ dotnet_TableBatchOperation_Insert] método. Em seguida, [CloudTable][dotnet_CloudTable].[ ExecuteBatch] [ dotnet_CloudTable_ExecuteBatch] é chamado de operação de saudação tooexecute.

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable object that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create hello batch operation.
TableBatchOperation batchOperation = new TableBatchOperation();

// Create a customer entity and add it toohello table.
CustomerEntity customer1 = new CustomerEntity("Smith", "Jeff");
customer1.Email = "Jeff@contoso.com";
customer1.PhoneNumber = "425-555-0104";

// Create another customer entity and add it toohello table.
CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
customer2.Email = "Ben@contoso.com";
customer2.PhoneNumber = "425-555-0102";

// Add both customer entities toohello batch insert operation.
batchOperation.Insert(customer1);
batchOperation.Insert(customer2);

// Execute hello batch operation.
table.ExecuteBatch(batchOperation);
```

## <a name="retrieve-all-entities-in-a-partition"></a>Recuperar todas as entidades em uma partição
tooquery uma tabela para todas as entidades em uma partição, use um [TableQuery] [ dotnet_TableQuery] objeto. Olá, exemplo de código a seguir especifica um filtro para entidades onde 'Smith' é a chave de partição hello. Este exemplo imprime campos de saudação de cada entidade no console de toohello de resultados de consulta de saudação.

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable object that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Construct hello query operation for all customer entities where PartitionKey="Smith".
TableQuery<CustomerEntity> query = new TableQuery<CustomerEntity>().Where(TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"));

// Print hello fields for each customer.
foreach (CustomerEntity entity in table.ExecuteQuery(query))
{
    Console.WriteLine("{0}, {1}\t{2}\t{3}", entity.PartitionKey, entity.RowKey,
        entity.Email, entity.PhoneNumber);
}
```

## <a name="retrieve-a-range-of-entities-in-a-partition"></a>Recuperar um intervalo de entidades em uma partição
Se você não quiser tooquery todas as entidades em uma partição, você pode especificar um intervalo, combinando o filtro de chave de partição Olá com um filtro de linha de chave. Olá exemplo de código a seguir usa duas tooget de filtros todas as entidades na partição 'Smith' onde a chave de linha de saudação (nome) começa com uma letra antes 'E' alfabeto hello e imprime os resultados da consulta hello.

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable object that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create hello table query.
TableQuery<CustomerEntity> rangeQuery = new TableQuery<CustomerEntity>().Where(
    TableQuery.CombineFilters(
        TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"),
        TableOperators.And,
        TableQuery.GenerateFilterCondition("RowKey", QueryComparisons.LessThan, "E")));

// Loop through hello results, displaying information about hello entity.
foreach (CustomerEntity entity in table.ExecuteQuery(rangeQuery))
{
    Console.WriteLine("{0}, {1}\t{2}\t{3}", entity.PartitionKey, entity.RowKey,
        entity.Email, entity.PhoneNumber);
}
```

## <a name="retrieve-a-single-entity"></a>Recuperar uma única entidade
Você pode escrever uma consulta tooretrieve uma entidade única e específica. código a seguir Olá usa [TableOperation] [ dotnet_TableOperation] toospecify Prezado cliente 'Ben Smith'. Este método retorna apenas uma entidade em vez de uma coleção e Olá retornou o valor em [TableResult][dotnet_TableResult].[ Resultado] [ dotnet_TableResult_Result] é um **CustomerEntity** objeto. Especificar chaves de partição e de linha em uma consulta é tooretrieve de maneira mais rápida de Olá uma única entidade de serviço de tabela de saudação.

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable object that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create a retrieve operation that takes a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute hello retrieve operation.
TableResult retrievedResult = table.Execute(retrieveOperation);

// Print hello phone number of hello result.
if (retrievedResult.Result != null)
{
    Console.WriteLine(((CustomerEntity)retrievedResult.Result).PhoneNumber);
}
else
{
    Console.WriteLine("hello phone number could not be retrieved.");
}
```

## <a name="replace-an-entity"></a>Substituir uma entidade
tooupdate uma entidade, recuperá-lo do serviço de tabela hello, modificar o objeto de entidade hello e, em seguida, salvar as alterações de saudação fazer toohello serviço de tabela. Olá código a seguir altera o número de telefone de um cliente existente. Em vez de chamar [Insert][dotnet_TableOperation_Insert], esse código usa [Replace][dotnet_TableOperation_Replace]. [Substituir] [ dotnet_TableOperation_Replace] causas Olá entidade toobe totalmente substituído no servidor de saudação, a menos que a entidade Olá no servidor de saudação foi alterado desde que foi recuperada, caso em que haverá falha na operação de saudação. Essa falha é tooprevent seu aplicativo substitua inadvertidamente uma alteração feita entre Olá recuperação e atualizar por outro componente do seu aplicativo. Hello manipulação adequada dessa falha é tooretrieve Olá entidade novamente, faça as alterações (se ainda é válida) e, em seguida, executar outro [substituir] [ dotnet_TableOperation_Replace] operação. Olá próxima seção lhe mostrará como toooverride esse comportamento.

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable object that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create a retrieve operation that takes a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute hello operation.
TableResult retrievedResult = table.Execute(retrieveOperation);

// Assign hello result tooa CustomerEntity object.
CustomerEntity updateEntity = (CustomerEntity)retrievedResult.Result;

if (updateEntity != null)
{
    // Change hello phone number.
    updateEntity.PhoneNumber = "425-555-0105";

    // Create hello Replace TableOperation.
    TableOperation updateOperation = TableOperation.Replace(updateEntity);

    // Execute hello operation.
    table.Execute(updateOperation);

    Console.WriteLine("Entity updated.");
}
else
{
    Console.WriteLine("Entity could not be retrieved.");
}
```

## <a name="insert-or-replace-an-entity"></a>Inserir ou substituir uma entidade
[Substituir] [ dotnet_TableOperation_Replace] operações falharão se a entidade de saudação foi alterada desde que foi recuperada do servidor de saudação. Além disso, você deve recuperar a entidade saudação do servidor de saudação primeiro na ordem de saudação [substituir] [ dotnet_TableOperation_Replace] toobe de operação bem-sucedida. Às vezes, no entanto, você não sabe se a entidade Olá existe no servidor de saudação e valores atuais de saudação armazenados nela são irrelevantes. A atualização deve substituir todos eles. tooaccomplish isso, você usaria uma [InsertOrReplace] [ dotnet_TableOperation_InsertOrReplace] operação. Essa operação insere a entidade de saudação se ele não existe ou substitui-lo em caso afirmativo, independentemente de quando Olá última atualização foi feita.

Em Olá exemplo de código a seguir, uma entidade customer para 'Fred Jones' é criada e inserida na tabela de 'pessoas' hello. Em seguida, usamos Olá [InsertOrReplace] [ dotnet_TableOperation_InsertOrReplace] operação toosave uma entidade com hello mesma chave de partição (Jones) e a linha de chave server de toohello (Fred), dessa vez com um valor diferente para Olá PhoneNumber propriedade. Como usamos [InsertOrReplace][dotnet_TableOperation_InsertOrReplace], todos os seus valores de propriedade serão substituídos. No entanto, se uma entidade 'Fred Jones' não tinha já existia na tabela hello, ele seria foram inserido.

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable object that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create a customer entity.
CustomerEntity customer3 = new CustomerEntity("Jones", "Fred");
customer3.Email = "Fred@contoso.com";
customer3.PhoneNumber = "425-555-0106";

// Create hello TableOperation object that inserts hello customer entity.
TableOperation insertOperation = TableOperation.Insert(customer3);

// Execute hello operation.
table.Execute(insertOperation);

// Create another customer entity with hello same partition key and row key.
// We've already created a 'Fred Jones' entity and saved it toothe
// 'people' table, but here we're specifying a different value for the
// PhoneNumber property.
CustomerEntity customer4 = new CustomerEntity("Jones", "Fred");
customer4.Email = "Fred@contoso.com";
customer4.PhoneNumber = "425-555-0107";

// Create hello InsertOrReplace TableOperation.
TableOperation insertOrReplaceOperation = TableOperation.InsertOrReplace(customer4);

// Execute hello operation. Because a 'Fred Jones' entity already exists in the
// 'people' table, its property values will be overwritten by those in this
// CustomerEntity. If 'Fred Jones' didn't already exist, hello entity would be
// added toohello table.
table.Execute(insertOrReplaceOperation);
```

## <a name="query-a-subset-of-entity-properties"></a>consultar um subconjunto de propriedades da entidade
Uma consulta de tabela pode recuperar apenas algumas propriedades de uma entidade em vez de todas as propriedades de entidade hello. Essa técnica, chamada projeção, reduz a largura de banda e pode melhorar o desempenho da consulta, principalmente para grandes entidades. consulta Olá Olá código a seguir retorna somente endereços de email de saudação de entidades na tabela de saudação. Isso é feito por meio de uma consulta de [DynamicTableEntity][dotnet_DynamicTableEntity] e também de [EntityResolver][dotnet_EntityResolver]. Você pode aprender mais sobre a projeção em Olá [Upsert apresentando e projeção de consulta postagem de blog][blog_post_upsert]. Não há suporte para projeção pelo emulador de armazenamento hello, para que este código seja executado somente quando você estiver usando uma conta de serviço de tabela de saudação.

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Define hello query, and select only hello Email property.
TableQuery<DynamicTableEntity> projectionQuery = new TableQuery<DynamicTableEntity>().Select(new string[] { "Email" });

// Define an entity resolver toowork with hello entity after retrieval.
EntityResolver<string> resolver = (pk, rk, ts, props, etag) => props.ContainsKey("Email") ? props["Email"].StringValue : null;

foreach (string projectedEmail in table.ExecuteQuery(projectionQuery, resolver, null, null))
{
    Console.WriteLine(projectedEmail);
}
```

## <a name="delete-an-entity"></a>Excluir uma entidade
Você pode facilmente excluir uma entidade após recuperá-lo usando Olá mesmo padrão mostrado para a atualização de uma entidade. saudação de código a seguir recupera e exclui uma entidade customer.

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create a retrieve operation that expects a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute hello operation.
TableResult retrievedResult = table.Execute(retrieveOperation);

// Assign hello result tooa CustomerEntity.
CustomerEntity deleteEntity = (CustomerEntity)retrievedResult.Result;

// Create hello Delete TableOperation.
if (deleteEntity != null)
{
    TableOperation deleteOperation = TableOperation.Delete(deleteEntity);

    // Execute hello operation.
    table.Execute(deleteOperation);

    Console.WriteLine("Entity deleted.");
}
else
{
    Console.WriteLine("Could not retrieve hello entity.");
}
```

## <a name="delete-a-table"></a>Excluir uma tabela
Por fim, Olá exemplo de código a seguir exclui uma tabela de uma conta de armazenamento. Uma tabela que tenha sido excluída será toobe indisponível recriado por um período de tempo após a exclusão de saudação.

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Delete hello table it if exists.
table.DeleteIfExists();
```

## <a name="retrieve-entities-in-pages-asynchronously"></a>Recuperar entidades nas páginas de forma assíncrona
Se você está lendo um grande número de entidades, e você desejar entidades tooprocess/exibição como eles são recuperados, em vez de aguardar que eles todos os tooreturn, você pode recuperar entidades usando uma consulta segmentada. Este exemplo mostra como os resultados tooreturn nas páginas usando o padrão de saudação Async-Await para que a execução não é bloqueada enquanto você está esperando um grande conjunto de resultados tooreturn. Para obter mais detalhes sobre como usar o hello padrão Async-Await no .NET, consulte [programação assíncrona com Async e Await (c# e Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx).

```csharp
// Initialize a default TableQuery tooretrieve all hello entities in hello table.
TableQuery<CustomerEntity> tableQuery = new TableQuery<CustomerEntity>();

// Initialize hello continuation token toonull toostart from hello beginning of hello table.
TableContinuationToken continuationToken = null;

do
{
    // Retrieve a segment (up too1,000 entities).
    TableQuerySegment<CustomerEntity> tableQueryResult =
        await table.ExecuteQuerySegmentedAsync(tableQuery, continuationToken);

    // Assign hello new continuation token tootell hello service where to
    // continue on hello next iteration (or null if it has reached hello end).
    continuationToken = tableQueryResult.ContinuationToken;

    // Print hello number of rows retrieved.
    Console.WriteLine("Rows retrieved {0}", tableQueryResult.Results.Count);

// Loop until a null continuation token is received, indicating hello end of hello table.
} while(continuationToken != null);
```

## <a name="next-steps"></a>Próximas etapas
Agora que você aprendeu as Noções básicas de saudação do armazenamento de tabela, siga essas toolearn links sobre tarefas mais complexas de armazenamento:

* [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) é um aplicativo autônomo gratuito da Microsoft que permite que você toowork visualmente com dados de armazenamento do Azure no Linux, Windows e macOS.
* Ver mais exemplos de Armazenamento de Tabelas na [Introdução ao Armazenamento de Tabelas do Azure no .NET](https://azure.microsoft.com/documentation/samples/storage-table-dotnet-getting-started/)
* Exiba a documentação de referência de serviço Olá tabela para obter detalhes completos sobre as APIs disponíveis:
* [Referência à Biblioteca de Cliente de Armazenamento para .NET](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)
* [Referência da API REST](http://msdn.microsoft.com/library/azure/dd179355)
* Saiba como código de saudação toosimplify escrever toowork com armazenamento do Azure usando Olá [SDK do Azure WebJobs](../app-service-web/websites-dotnet-webjobs-sdk-get-started.md)
* Exiba toolearn de guias de recurso mais sobre opções adicionais para armazenar dados no Azure.
* [Introdução ao armazenamento de BLOBs do Azure usando o .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) toostore dados não estruturados.
* [Conecte-se tooSQL banco de dados usando o .NET (c#)](../sql-database/sql-database-develop-dotnet-simple.md) dados relacionais toostore.

[Download and install hello Azure SDK for .NET]: /develop/net/
[Creating an Azure Project in Visual Studio]: http://msdn.microsoft.com/library/azure/ee405487.aspx

[blog_post_upsert]: http://blogs.msdn.com/b/windowsazurestorage/archive/2011/09/15/windows-azure-tables-introducing-upsert-and-query-projection.aspx

[dotnet_api_ref]: https://msdn.microsoft.com/library/azure/mt347887.aspx
[dotnet_CloudTableClient]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.cloudtableclient.aspx
[dotnet_CloudTable]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.cloudtable.aspx
[dotnet_CloudTable_Execute]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.cloudtable.execute.aspx
[dotnet_CloudTable_ExecuteBatch]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.cloudtable.executebatch.aspx
[dotnet_DynamicTableEntity]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.dynamictableentity.aspx
[dotnet_EntityResolver]: https://msdn.microsoft.com/library/jj733144.aspx
[dotnet_TableBatchOperation]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tablebatchoperation.aspx
[dotnet_TableBatchOperation_Insert]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tablebatchoperation.insert.aspx
[dotnet_TableEntity]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tableentity.aspx
[dotnet_TableOperation]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tableoperation.aspx
[dotnet_TableOperation_Insert]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tableoperation.insert.aspx
[dotnet_TableOperation_InsertOrReplace]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tableoperation.insertorreplace.aspx
[dotnet_TableOperation_Replace]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tableoperation.replace.aspx
[dotnet_TableQuery]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tablequery.aspx
[dotnet_TableResult]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tableresult.aspx
[dotnet_TableResult_Result]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tableresult.result.aspx
