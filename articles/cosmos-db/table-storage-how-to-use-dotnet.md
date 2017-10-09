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
# <a name="get-started-with-azure-table-storage-using-net"></a><span data-ttu-id="a68b1-103">Introdução ao armazenamento de Tabelas do Azure usando o .NET</span><span class="sxs-lookup"><span data-stu-id="a68b1-103">Get started with Azure Table storage using .NET</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-tip-include](../../includes/storage-table-cosmos-db-tip-include.md)]

<span data-ttu-id="a68b1-104">Armazenamento de tabela do Azure é um serviço que armazena estruturado NoSQL armazenam dados na nuvem hello, fornecendo um atributo de chave/com um design schemaless.</span><span class="sxs-lookup"><span data-stu-id="a68b1-104">Azure Table storage is a service that stores structured NoSQL data in hello cloud, providing a key/attribute store with a schemaless design.</span></span> <span data-ttu-id="a68b1-105">Como o armazenamento de tabela é schemaless, é fácil tooadapt seus dados como Olá precisam de evolve seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a68b1-105">Because Table storage is schemaless, it's easy tooadapt your data as hello needs of your application evolve.</span></span> <span data-ttu-id="a68b1-106">Acessar dados de armazenamento tooTable é rápida e econômica para vários tipos de aplicativos e é geralmente inferiores no custo SQL tradicional para volumes semelhantes de dados.</span><span class="sxs-lookup"><span data-stu-id="a68b1-106">Access tooTable storage data is fast and cost-effective for many types of applications, and is typically lower in cost than traditional SQL for similar volumes of data.</span></span>

<span data-ttu-id="a68b1-107">Você pode usar a tabela armazenamento toostore flexíveis conjuntos de dados como dados de usuário para aplicativos web, catálogos de endereços, informações de dispositivo ou outros tipos de metadados, que seu serviço exigir.</span><span class="sxs-lookup"><span data-stu-id="a68b1-107">You can use Table storage toostore flexible datasets like user data for web applications, address books, device information, or other types of metadata your service requires.</span></span> <span data-ttu-id="a68b1-108">Você pode armazenar qualquer número de entidades em uma tabela, e uma conta de armazenamento pode conter qualquer número de tabelas, o limite de capacidade toohello Olá da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="a68b1-108">You can store any number of entities in a table, and a storage account may contain any number of tables, up toohello capacity limit of hello storage account.</span></span>

### <a name="about-this-tutorial"></a><span data-ttu-id="a68b1-109">Sobre este tutorial</span><span class="sxs-lookup"><span data-stu-id="a68b1-109">About this tutorial</span></span>
<span data-ttu-id="a68b1-110">Este tutorial mostra como Olá toouse [biblioteca de cliente de armazenamento do Azure para .NET](https://www.nuget.org/packages/WindowsAzure.Storage/) em alguns cenários comuns de armazenamento de tabela do Azure.</span><span class="sxs-lookup"><span data-stu-id="a68b1-110">This tutorial shows you how toouse hello [Azure Storage Client Library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage/) in some common Azure Table storage scenarios.</span></span> <span data-ttu-id="a68b1-111">Esses cenários são apresentados usando exemplos de C# para criar e excluir uma tabela e inserir, atualizar, excluir e consultar dados de tabela.</span><span class="sxs-lookup"><span data-stu-id="a68b1-111">These scenarios are presented using C# examples for creating and deleting a table, and inserting, updating, deleting, and querying table data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a68b1-112">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a68b1-112">Prerequisites</span></span>

<span data-ttu-id="a68b1-113">Você precisa Olá toocomplete a seguir este tutorial com êxito:</span><span class="sxs-lookup"><span data-stu-id="a68b1-113">You need hello following toocomplete this tutorial successfully:</span></span>

* [<span data-ttu-id="a68b1-114">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a68b1-114">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="a68b1-115">Biblioteca do Cliente de Armazenamento do Azure para .NET</span><span class="sxs-lookup"><span data-stu-id="a68b1-115">Azure Storage Client Library for .NET</span></span>](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [<span data-ttu-id="a68b1-116">Gerenciador de Configurações do Azure para .NET</span><span class="sxs-lookup"><span data-stu-id="a68b1-116">Azure Configuration Manager for .NET</span></span>](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)
* [<span data-ttu-id="a68b1-117">Conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="a68b1-117">Azure storage account</span></span>](../storage/common/storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-dotnet-client-library-version-include](../../includes/storage-dotnet-client-library-version-include.md)]

### <a name="more-samples"></a><span data-ttu-id="a68b1-118">Mais exemplos</span><span class="sxs-lookup"><span data-stu-id="a68b1-118">More samples</span></span>
<span data-ttu-id="a68b1-119">Para obter exemplos adicionais usando o Armazenamento de Tabelas, confira [Introdução ao Armazenamento de Tabelas do Azure no .NET](https://azure.microsoft.com/documentation/samples/storage-table-dotnet-getting-started/).</span><span class="sxs-lookup"><span data-stu-id="a68b1-119">For additional examples using Table storage, see [Getting Started with Azure Table Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-table-dotnet-getting-started/).</span></span> <span data-ttu-id="a68b1-120">Você pode baixar o aplicativo de exemplo hello e executá-lo ou procurar Olá código no GitHub.</span><span class="sxs-lookup"><span data-stu-id="a68b1-120">You can download hello sample application and run it, or browse hello code on GitHub.</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-development-environment-include](../../includes/storage-development-environment-include.md)]

### <a name="add-using-directives"></a><span data-ttu-id="a68b1-121">Adicionar diretivas using</span><span class="sxs-lookup"><span data-stu-id="a68b1-121">Add using directives</span></span>
<span data-ttu-id="a68b1-122">Adicione o seguinte Olá **usando** superior de toohello de diretivas de saudação `Program.cs` arquivo:</span><span class="sxs-lookup"><span data-stu-id="a68b1-122">Add hello following **using** directives toohello top of hello `Program.cs` file:</span></span>

```csharp
using Microsoft.Azure; // Namespace for CloudConfigurationManager
using Microsoft.WindowsAzure.Storage; // Namespace for CloudStorageAccount
using Microsoft.WindowsAzure.Storage.Table; // Namespace for Table storage types
```

### <a name="parse-hello-connection-string"></a><span data-ttu-id="a68b1-123">Analisar a cadeia de conexão Olá</span><span class="sxs-lookup"><span data-stu-id="a68b1-123">Parse hello connection string</span></span>
[!INCLUDE [storage-cloud-configuration-manager-include](../../includes/storage-cloud-configuration-manager-include.md)]

### <a name="create-hello-table-service-client"></a><span data-ttu-id="a68b1-124">Criar o cliente do serviço de tabela Olá</span><span class="sxs-lookup"><span data-stu-id="a68b1-124">Create hello Table service client</span></span>
<span data-ttu-id="a68b1-125">Olá [CloudTableClient] [ dotnet_CloudTableClient] classe permite que você tooretrieve tabelas e entidades armazenadas no armazenamento de tabela.</span><span class="sxs-lookup"><span data-stu-id="a68b1-125">hello [CloudTableClient][dotnet_CloudTableClient] class enables you tooretrieve tables and entities stored in Table storage.</span></span> <span data-ttu-id="a68b1-126">Aqui está o cliente do serviço de tabela toocreate unidirecional hello:</span><span class="sxs-lookup"><span data-stu-id="a68b1-126">Here's one way toocreate hello Table service client:</span></span>

```csharp
// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
```

<span data-ttu-id="a68b1-127">Agora você está pronto toowrite código lê e grava o armazenamento tooTable de dados.</span><span class="sxs-lookup"><span data-stu-id="a68b1-127">Now you are ready toowrite code that reads data from and writes data tooTable storage.</span></span>

## <a name="create-a-table"></a><span data-ttu-id="a68b1-128">Criar uma tabela</span><span class="sxs-lookup"><span data-stu-id="a68b1-128">Create a table</span></span>
<span data-ttu-id="a68b1-129">Este exemplo mostra como toocreate uma tabela se ela ainda não existir:</span><span class="sxs-lookup"><span data-stu-id="a68b1-129">This example shows how toocreate a table if it does not already exist:</span></span>

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

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="a68b1-130">Adicionar uma tabela de entidade tooa</span><span class="sxs-lookup"><span data-stu-id="a68b1-130">Add an entity tooa table</span></span>
<span data-ttu-id="a68b1-131">Entidades são mapeadas tooC # objetos por meio de uma classe personalizada derivada de [TableEntity][dotnet_TableEntity].</span><span class="sxs-lookup"><span data-stu-id="a68b1-131">Entities map tooC# objects by using a custom class derived from [TableEntity][dotnet_TableEntity].</span></span> <span data-ttu-id="a68b1-132">tooadd uma tabela de tooa de entidade, crie uma classe que define as propriedades de saudação da entidade.</span><span class="sxs-lookup"><span data-stu-id="a68b1-132">tooadd an entity tooa table, create a class that defines hello properties of your entity.</span></span> <span data-ttu-id="a68b1-133">Olá código a seguir define uma classe de entidade que usa o nome saudação do cliente como chave de linha de saudação e último nome como chave de partição de saudação.</span><span class="sxs-lookup"><span data-stu-id="a68b1-133">hello following code defines an entity class that uses hello customer's first name as hello row key and last name as hello partition key.</span></span> <span data-ttu-id="a68b1-134">Juntas, partição de uma entidade e a chave de linha identificá-lo exclusivamente na tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="a68b1-134">Together, an entity's partition and row key uniquely identify it in hello table.</span></span> <span data-ttu-id="a68b1-135">Entidades com hello a mesma chave de partição pode ser consultado mais rápido do que as entidades com diferentes chaves de partição, mas usar chaves de partição diversas permite maior escalabilidade de operações paralelas.</span><span class="sxs-lookup"><span data-stu-id="a68b1-135">Entities with hello same partition key can be queried faster than entities with different partition keys, but using diverse partition keys allows for greater scalability of parallel operations.</span></span> <span data-ttu-id="a68b1-136">Entidades toobe armazenado nas tabelas deve ser de um tipo com suporte, por exemplo derivado de saudação [TableEntity] [ dotnet_TableEntity] classe.</span><span class="sxs-lookup"><span data-stu-id="a68b1-136">Entities toobe stored in tables must be of a supported type, for example derived from hello [TableEntity][dotnet_TableEntity] class.</span></span> <span data-ttu-id="a68b1-137">Você gostaria que toostore em uma tabela de propriedades de entidade devem ser propriedades públicas do tipo hello e dar suporte a obtenção e configuração de valores de.</span><span class="sxs-lookup"><span data-stu-id="a68b1-137">Entity properties you'd like toostore in a table must be public properties of hello type, and support both getting and setting of values.</span></span> <span data-ttu-id="a68b1-138">Além disso, o tipo de entidade *deve* expor um construtor sem parâmetros.</span><span class="sxs-lookup"><span data-stu-id="a68b1-138">Also, your entity type *must* expose a parameter-less constructor.</span></span>

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

<span data-ttu-id="a68b1-139">Operações de tabela que envolvem entidades são realizadas por meio de saudação [CloudTable] [ dotnet_CloudTable] objeto que você criou anteriormente na seção "Criar uma tabela", Olá.</span><span class="sxs-lookup"><span data-stu-id="a68b1-139">Table operations that involve entities are performed via hello [CloudTable][dotnet_CloudTable] object that you created earlier in hello "Create a table" section.</span></span> <span data-ttu-id="a68b1-140">Olá toobe operação realizada é representado por um [TableOperation] [ dotnet_TableOperation] objeto.</span><span class="sxs-lookup"><span data-stu-id="a68b1-140">hello operation toobe performed is represented by a [TableOperation][dotnet_TableOperation] object.</span></span> <span data-ttu-id="a68b1-141">Olá, exemplo de código a seguir mostra a criação Olá de saudação [CloudTable] [ dotnet_CloudTable] objeto e, em seguida, um **CustomerEntity** objeto.</span><span class="sxs-lookup"><span data-stu-id="a68b1-141">hello following code example shows hello creation of hello [CloudTable][dotnet_CloudTable] object and then a **CustomerEntity** object.</span></span> <span data-ttu-id="a68b1-142">operação de saudação tooprepare, uma [TableOperation] [ dotnet_TableOperation] objeto é criado entidade do cliente Olá tooinsert na tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="a68b1-142">tooprepare hello operation, a [TableOperation][dotnet_TableOperation] object is created tooinsert hello customer entity into hello table.</span></span> <span data-ttu-id="a68b1-143">Por fim, a operação de saudação é executada chamando [CloudTable][dotnet_CloudTable].[ Executar][dotnet_CloudTable_Execute].</span><span class="sxs-lookup"><span data-stu-id="a68b1-143">Finally, hello operation is executed by calling [CloudTable][dotnet_CloudTable].[Execute][dotnet_CloudTable_Execute].</span></span>

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

## <a name="insert-a-batch-of-entities"></a><span data-ttu-id="a68b1-144">Inserir um lote de entidades</span><span class="sxs-lookup"><span data-stu-id="a68b1-144">Insert a batch of entities</span></span>
<span data-ttu-id="a68b1-145">Você pode inserir um lote de entidades em uma tabela em uma única operação de gravação.</span><span class="sxs-lookup"><span data-stu-id="a68b1-145">You can insert a batch of entities into a table in one write operation.</span></span> <span data-ttu-id="a68b1-146">Algumas outras observações sobre operações em lote:</span><span class="sxs-lookup"><span data-stu-id="a68b1-146">Some other notes on batch operations:</span></span>

* <span data-ttu-id="a68b1-147">Você pode executar inserções, atualizações e exclusões em Olá mesmo única operação em lote.</span><span class="sxs-lookup"><span data-stu-id="a68b1-147">You can perform updates, deletes, and inserts in hello same single batch operation.</span></span>
* <span data-ttu-id="a68b1-148">Uma operação em lote único pode incluir o too100 entidades.</span><span class="sxs-lookup"><span data-stu-id="a68b1-148">A single batch operation can include up too100 entities.</span></span>
* <span data-ttu-id="a68b1-149">Todas as entidades em uma única operação de lote devem ter Olá mesma chave de partição.</span><span class="sxs-lookup"><span data-stu-id="a68b1-149">All entities in a single batch operation must have hello same partition key.</span></span>
* <span data-ttu-id="a68b1-150">Embora seja possível tooperform uma consulta como uma operação em lote, deve ser a única operação Olá em lote de saudação.</span><span class="sxs-lookup"><span data-stu-id="a68b1-150">While it is possible tooperform a query as a batch operation, it must be hello only operation in hello batch.</span></span>

<span data-ttu-id="a68b1-151">Olá exemplo de código a seguir cria dois objetos de entidade e adiciona cada muito[TableBatchOperation] [ dotnet_TableBatchOperation] usando Olá [inserir] [ dotnet_TableBatchOperation_Insert] método.</span><span class="sxs-lookup"><span data-stu-id="a68b1-151">hello following code example creates two entity objects and adds each too[TableBatchOperation][dotnet_TableBatchOperation] by using hello [Insert][dotnet_TableBatchOperation_Insert] method.</span></span> <span data-ttu-id="a68b1-152">Em seguida, [CloudTable][dotnet_CloudTable].[ ExecuteBatch] [ dotnet_CloudTable_ExecuteBatch] é chamado de operação de saudação tooexecute.</span><span class="sxs-lookup"><span data-stu-id="a68b1-152">Then, [CloudTable][dotnet_CloudTable].[ExecuteBatch][dotnet_CloudTable_ExecuteBatch] is called tooexecute hello operation.</span></span>

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

## <a name="retrieve-all-entities-in-a-partition"></a><span data-ttu-id="a68b1-153">Recuperar todas as entidades em uma partição</span><span class="sxs-lookup"><span data-stu-id="a68b1-153">Retrieve all entities in a partition</span></span>
<span data-ttu-id="a68b1-154">tooquery uma tabela para todas as entidades em uma partição, use um [TableQuery] [ dotnet_TableQuery] objeto.</span><span class="sxs-lookup"><span data-stu-id="a68b1-154">tooquery a table for all entities in a partition, use a [TableQuery][dotnet_TableQuery] object.</span></span> <span data-ttu-id="a68b1-155">Olá, exemplo de código a seguir especifica um filtro para entidades onde 'Smith' é a chave de partição hello.</span><span class="sxs-lookup"><span data-stu-id="a68b1-155">hello following code example specifies a filter for entities where 'Smith' is hello partition key.</span></span> <span data-ttu-id="a68b1-156">Este exemplo imprime campos de saudação de cada entidade no console de toohello de resultados de consulta de saudação.</span><span class="sxs-lookup"><span data-stu-id="a68b1-156">This example prints hello fields of each entity in hello query results toohello console.</span></span>

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

## <a name="retrieve-a-range-of-entities-in-a-partition"></a><span data-ttu-id="a68b1-157">Recuperar um intervalo de entidades em uma partição</span><span class="sxs-lookup"><span data-stu-id="a68b1-157">Retrieve a range of entities in a partition</span></span>
<span data-ttu-id="a68b1-158">Se você não quiser tooquery todas as entidades em uma partição, você pode especificar um intervalo, combinando o filtro de chave de partição Olá com um filtro de linha de chave.</span><span class="sxs-lookup"><span data-stu-id="a68b1-158">If you don't want tooquery all entities in a partition, you can specify a range by combining hello partition key filter with a row key filter.</span></span> <span data-ttu-id="a68b1-159">Olá exemplo de código a seguir usa duas tooget de filtros todas as entidades na partição 'Smith' onde a chave de linha de saudação (nome) começa com uma letra antes 'E' alfabeto hello e imprime os resultados da consulta hello.</span><span class="sxs-lookup"><span data-stu-id="a68b1-159">hello following code example uses two filters tooget all entities in partition 'Smith' where hello row key (first name) starts with a letter before 'E' in hello alphabet, then prints hello query results.</span></span>

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

## <a name="retrieve-a-single-entity"></a><span data-ttu-id="a68b1-160">Recuperar uma única entidade</span><span class="sxs-lookup"><span data-stu-id="a68b1-160">Retrieve a single entity</span></span>
<span data-ttu-id="a68b1-161">Você pode escrever uma consulta tooretrieve uma entidade única e específica.</span><span class="sxs-lookup"><span data-stu-id="a68b1-161">You can write a query tooretrieve a single, specific entity.</span></span> <span data-ttu-id="a68b1-162">código a seguir Olá usa [TableOperation] [ dotnet_TableOperation] toospecify Prezado cliente 'Ben Smith'.</span><span class="sxs-lookup"><span data-stu-id="a68b1-162">hello following code uses [TableOperation][dotnet_TableOperation] toospecify hello customer 'Ben Smith'.</span></span> <span data-ttu-id="a68b1-163">Este método retorna apenas uma entidade em vez de uma coleção e Olá retornou o valor em [TableResult][dotnet_TableResult].[ Resultado] [ dotnet_TableResult_Result] é um **CustomerEntity** objeto.</span><span class="sxs-lookup"><span data-stu-id="a68b1-163">This method returns just one entity rather than a collection, and hello returned value in [TableResult][dotnet_TableResult].[Result][dotnet_TableResult_Result] is a **CustomerEntity** object.</span></span> <span data-ttu-id="a68b1-164">Especificar chaves de partição e de linha em uma consulta é tooretrieve de maneira mais rápida de Olá uma única entidade de serviço de tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="a68b1-164">Specifying both partition and row keys in a query is hello fastest way tooretrieve a single entity from hello Table service.</span></span>

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

## <a name="replace-an-entity"></a><span data-ttu-id="a68b1-165">Substituir uma entidade</span><span class="sxs-lookup"><span data-stu-id="a68b1-165">Replace an entity</span></span>
<span data-ttu-id="a68b1-166">tooupdate uma entidade, recuperá-lo do serviço de tabela hello, modificar o objeto de entidade hello e, em seguida, salvar as alterações de saudação fazer toohello serviço de tabela.</span><span class="sxs-lookup"><span data-stu-id="a68b1-166">tooupdate an entity, retrieve it from hello Table service, modify hello entity object, and then save hello changes back toohello Table service.</span></span> <span data-ttu-id="a68b1-167">Olá código a seguir altera o número de telefone de um cliente existente.</span><span class="sxs-lookup"><span data-stu-id="a68b1-167">hello following code changes an existing customer's phone number.</span></span> <span data-ttu-id="a68b1-168">Em vez de chamar [Insert][dotnet_TableOperation_Insert], esse código usa [Replace][dotnet_TableOperation_Replace].</span><span class="sxs-lookup"><span data-stu-id="a68b1-168">Instead of calling [Insert][dotnet_TableOperation_Insert], this code uses [Replace][dotnet_TableOperation_Replace].</span></span> <span data-ttu-id="a68b1-169">[Substituir] [ dotnet_TableOperation_Replace] causas Olá entidade toobe totalmente substituído no servidor de saudação, a menos que a entidade Olá no servidor de saudação foi alterado desde que foi recuperada, caso em que haverá falha na operação de saudação.</span><span class="sxs-lookup"><span data-stu-id="a68b1-169">[Replace][dotnet_TableOperation_Replace] causes hello entity toobe fully replaced on hello server, unless hello entity on hello server has changed since it was retrieved, in which case hello operation will fail.</span></span> <span data-ttu-id="a68b1-170">Essa falha é tooprevent seu aplicativo substitua inadvertidamente uma alteração feita entre Olá recuperação e atualizar por outro componente do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="a68b1-170">This failure is tooprevent your application from inadvertently overwriting a change made between hello retrieval and update by another component of your application.</span></span> <span data-ttu-id="a68b1-171">Hello manipulação adequada dessa falha é tooretrieve Olá entidade novamente, faça as alterações (se ainda é válida) e, em seguida, executar outro [substituir] [ dotnet_TableOperation_Replace] operação.</span><span class="sxs-lookup"><span data-stu-id="a68b1-171">hello proper handling of this failure is tooretrieve hello entity again, make your changes (if still valid), and then perform another [Replace][dotnet_TableOperation_Replace] operation.</span></span> <span data-ttu-id="a68b1-172">Olá próxima seção lhe mostrará como toooverride esse comportamento.</span><span class="sxs-lookup"><span data-stu-id="a68b1-172">hello next section will show you how toooverride this behavior.</span></span>

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

## <a name="insert-or-replace-an-entity"></a><span data-ttu-id="a68b1-173">Inserir ou substituir uma entidade</span><span class="sxs-lookup"><span data-stu-id="a68b1-173">Insert-or-replace an entity</span></span>
<span data-ttu-id="a68b1-174">[Substituir] [ dotnet_TableOperation_Replace] operações falharão se a entidade de saudação foi alterada desde que foi recuperada do servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="a68b1-174">[Replace][dotnet_TableOperation_Replace] operations will fail if hello entity has been changed since it was retrieved from hello server.</span></span> <span data-ttu-id="a68b1-175">Além disso, você deve recuperar a entidade saudação do servidor de saudação primeiro na ordem de saudação [substituir] [ dotnet_TableOperation_Replace] toobe de operação bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="a68b1-175">Furthermore, you must retrieve hello entity from hello server first in order for hello [Replace][dotnet_TableOperation_Replace] operation toobe successful.</span></span> <span data-ttu-id="a68b1-176">Às vezes, no entanto, você não sabe se a entidade Olá existe no servidor de saudação e valores atuais de saudação armazenados nela são irrelevantes.</span><span class="sxs-lookup"><span data-stu-id="a68b1-176">Sometimes, however, you don't know if hello entity exists on hello server and hello current values stored in it are irrelevant.</span></span> <span data-ttu-id="a68b1-177">A atualização deve substituir todos eles.</span><span class="sxs-lookup"><span data-stu-id="a68b1-177">Your update should overwrite them all.</span></span> <span data-ttu-id="a68b1-178">tooaccomplish isso, você usaria uma [InsertOrReplace] [ dotnet_TableOperation_InsertOrReplace] operação.</span><span class="sxs-lookup"><span data-stu-id="a68b1-178">tooaccomplish this, you would use an [InsertOrReplace][dotnet_TableOperation_InsertOrReplace] operation.</span></span> <span data-ttu-id="a68b1-179">Essa operação insere a entidade de saudação se ele não existe ou substitui-lo em caso afirmativo, independentemente de quando Olá última atualização foi feita.</span><span class="sxs-lookup"><span data-stu-id="a68b1-179">This operation inserts hello entity if it doesn't exist, or replaces it if it does, regardless of when hello last update was made.</span></span>

<span data-ttu-id="a68b1-180">Em Olá exemplo de código a seguir, uma entidade customer para 'Fred Jones' é criada e inserida na tabela de 'pessoas' hello.</span><span class="sxs-lookup"><span data-stu-id="a68b1-180">In hello following code example, a customer entity for 'Fred Jones' is created and inserted into hello 'people' table.</span></span> <span data-ttu-id="a68b1-181">Em seguida, usamos Olá [InsertOrReplace] [ dotnet_TableOperation_InsertOrReplace] operação toosave uma entidade com hello mesma chave de partição (Jones) e a linha de chave server de toohello (Fred), dessa vez com um valor diferente para Olá PhoneNumber propriedade.</span><span class="sxs-lookup"><span data-stu-id="a68b1-181">Next, we use hello [InsertOrReplace][dotnet_TableOperation_InsertOrReplace] operation toosave an entity with hello same partition key (Jones) and row key (Fred) toohello server, this time with a different value for hello PhoneNumber property.</span></span> <span data-ttu-id="a68b1-182">Como usamos [InsertOrReplace][dotnet_TableOperation_InsertOrReplace], todos os seus valores de propriedade serão substituídos.</span><span class="sxs-lookup"><span data-stu-id="a68b1-182">Because we use [InsertOrReplace][dotnet_TableOperation_InsertOrReplace], all of its property values are replaced.</span></span> <span data-ttu-id="a68b1-183">No entanto, se uma entidade 'Fred Jones' não tinha já existia na tabela hello, ele seria foram inserido.</span><span class="sxs-lookup"><span data-stu-id="a68b1-183">However, if a 'Fred Jones' entity hadn't already existed in hello table, it would have been inserted.</span></span>

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

## <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="a68b1-184">consultar um subconjunto de propriedades da entidade</span><span class="sxs-lookup"><span data-stu-id="a68b1-184">Query a subset of entity properties</span></span>
<span data-ttu-id="a68b1-185">Uma consulta de tabela pode recuperar apenas algumas propriedades de uma entidade em vez de todas as propriedades de entidade hello.</span><span class="sxs-lookup"><span data-stu-id="a68b1-185">A table query can retrieve just a few properties from an entity instead of all hello entity properties.</span></span> <span data-ttu-id="a68b1-186">Essa técnica, chamada projeção, reduz a largura de banda e pode melhorar o desempenho da consulta, principalmente para grandes entidades.</span><span class="sxs-lookup"><span data-stu-id="a68b1-186">This technique, called projection, reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="a68b1-187">consulta Olá Olá código a seguir retorna somente endereços de email de saudação de entidades na tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="a68b1-187">hello query in hello following code returns only hello email addresses of entities in hello table.</span></span> <span data-ttu-id="a68b1-188">Isso é feito por meio de uma consulta de [DynamicTableEntity][dotnet_DynamicTableEntity] e também de [EntityResolver][dotnet_EntityResolver].</span><span class="sxs-lookup"><span data-stu-id="a68b1-188">This is done by using a query of [DynamicTableEntity][dotnet_DynamicTableEntity] and also [EntityResolver][dotnet_EntityResolver].</span></span> <span data-ttu-id="a68b1-189">Você pode aprender mais sobre a projeção em Olá [Upsert apresentando e projeção de consulta postagem de blog][blog_post_upsert].</span><span class="sxs-lookup"><span data-stu-id="a68b1-189">You can learn more about projection in hello [Introducing Upsert and Query Projection blog post][blog_post_upsert].</span></span> <span data-ttu-id="a68b1-190">Não há suporte para projeção pelo emulador de armazenamento hello, para que este código seja executado somente quando você estiver usando uma conta de serviço de tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="a68b1-190">Projection is not supported by hello storage emulator, so this code runs only when you're using an account in hello Table service.</span></span>

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

## <a name="delete-an-entity"></a><span data-ttu-id="a68b1-191">Excluir uma entidade</span><span class="sxs-lookup"><span data-stu-id="a68b1-191">Delete an entity</span></span>
<span data-ttu-id="a68b1-192">Você pode facilmente excluir uma entidade após recuperá-lo usando Olá mesmo padrão mostrado para a atualização de uma entidade.</span><span class="sxs-lookup"><span data-stu-id="a68b1-192">You can easily delete an entity after you have retrieved it by using hello same pattern shown for updating an entity.</span></span> <span data-ttu-id="a68b1-193">saudação de código a seguir recupera e exclui uma entidade customer.</span><span class="sxs-lookup"><span data-stu-id="a68b1-193">hello following code retrieves and deletes a customer entity.</span></span>

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

## <a name="delete-a-table"></a><span data-ttu-id="a68b1-194">Excluir uma tabela</span><span class="sxs-lookup"><span data-stu-id="a68b1-194">Delete a table</span></span>
<span data-ttu-id="a68b1-195">Por fim, Olá exemplo de código a seguir exclui uma tabela de uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="a68b1-195">Finally, hello following code example deletes a table from a storage account.</span></span> <span data-ttu-id="a68b1-196">Uma tabela que tenha sido excluída será toobe indisponível recriado por um período de tempo após a exclusão de saudação.</span><span class="sxs-lookup"><span data-stu-id="a68b1-196">A table that has been deleted will be unavailable toobe re-created for a period of time following hello deletion.</span></span>

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

## <a name="retrieve-entities-in-pages-asynchronously"></a><span data-ttu-id="a68b1-197">Recuperar entidades nas páginas de forma assíncrona</span><span class="sxs-lookup"><span data-stu-id="a68b1-197">Retrieve entities in pages asynchronously</span></span>
<span data-ttu-id="a68b1-198">Se você está lendo um grande número de entidades, e você desejar entidades tooprocess/exibição como eles são recuperados, em vez de aguardar que eles todos os tooreturn, você pode recuperar entidades usando uma consulta segmentada.</span><span class="sxs-lookup"><span data-stu-id="a68b1-198">If you are reading a large number of entities, and you want tooprocess/display entities as they are retrieved rather than waiting for them all tooreturn, you can retrieve entities by using a segmented query.</span></span> <span data-ttu-id="a68b1-199">Este exemplo mostra como os resultados tooreturn nas páginas usando o padrão de saudação Async-Await para que a execução não é bloqueada enquanto você está esperando um grande conjunto de resultados tooreturn.</span><span class="sxs-lookup"><span data-stu-id="a68b1-199">This example shows how tooreturn results in pages by using hello Async-Await pattern so that execution is not blocked while you're waiting for a large set of results tooreturn.</span></span> <span data-ttu-id="a68b1-200">Para obter mais detalhes sobre como usar o hello padrão Async-Await no .NET, consulte [programação assíncrona com Async e Await (c# e Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx).</span><span class="sxs-lookup"><span data-stu-id="a68b1-200">For more details on using hello Async-Await pattern in .NET, see [Asynchronous programming with Async and Await (C# and Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx).</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="a68b1-201">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a68b1-201">Next steps</span></span>
<span data-ttu-id="a68b1-202">Agora que você aprendeu as Noções básicas de saudação do armazenamento de tabela, siga essas toolearn links sobre tarefas mais complexas de armazenamento:</span><span class="sxs-lookup"><span data-stu-id="a68b1-202">Now that you've learned hello basics of Table storage, follow these links toolearn about more complex storage tasks:</span></span>

* <span data-ttu-id="a68b1-203">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) é um aplicativo autônomo gratuito da Microsoft que permite que você toowork visualmente com dados de armazenamento do Azure no Linux, Windows e macOS.</span><span class="sxs-lookup"><span data-stu-id="a68b1-203">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you toowork visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* <span data-ttu-id="a68b1-204">Ver mais exemplos de Armazenamento de Tabelas na [Introdução ao Armazenamento de Tabelas do Azure no .NET](https://azure.microsoft.com/documentation/samples/storage-table-dotnet-getting-started/)</span><span class="sxs-lookup"><span data-stu-id="a68b1-204">See more Table storage samples in [Getting Started with Azure Table Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-table-dotnet-getting-started/)</span></span>
* <span data-ttu-id="a68b1-205">Exiba a documentação de referência de serviço Olá tabela para obter detalhes completos sobre as APIs disponíveis:</span><span class="sxs-lookup"><span data-stu-id="a68b1-205">View hello Table service reference documentation for complete details about available APIs:</span></span>
* [<span data-ttu-id="a68b1-206">Referência à Biblioteca de Cliente de Armazenamento para .NET</span><span class="sxs-lookup"><span data-stu-id="a68b1-206">Storage Client Library for .NET reference</span></span>](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)
* [<span data-ttu-id="a68b1-207">Referência da API REST</span><span class="sxs-lookup"><span data-stu-id="a68b1-207">REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* <span data-ttu-id="a68b1-208">Saiba como código de saudação toosimplify escrever toowork com armazenamento do Azure usando Olá [SDK do Azure WebJobs](../app-service-web/websites-dotnet-webjobs-sdk-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="a68b1-208">Learn how toosimplify hello code you write toowork with Azure Storage by using hello [Azure WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-get-started.md)</span></span>
* <span data-ttu-id="a68b1-209">Exiba toolearn de guias de recurso mais sobre opções adicionais para armazenar dados no Azure.</span><span class="sxs-lookup"><span data-stu-id="a68b1-209">View more feature guides toolearn about additional options for storing data in Azure.</span></span>
* <span data-ttu-id="a68b1-210">[Introdução ao armazenamento de BLOBs do Azure usando o .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) toostore dados não estruturados.</span><span class="sxs-lookup"><span data-stu-id="a68b1-210">[Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) toostore unstructured data.</span></span>
* <span data-ttu-id="a68b1-211">[Conecte-se tooSQL banco de dados usando o .NET (c#)](../sql-database/sql-database-develop-dotnet-simple.md) dados relacionais toostore.</span><span class="sxs-lookup"><span data-stu-id="a68b1-211">[Connect tooSQL Database by using .NET (C#)](../sql-database/sql-database-develop-dotnet-simple.md) toostore relational data.</span></span>

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
