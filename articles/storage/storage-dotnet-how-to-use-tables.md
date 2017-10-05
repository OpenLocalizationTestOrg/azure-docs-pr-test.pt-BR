---
title: "Introdução ao armazenamento de Tabelas do Azure usando o .NET | Microsoft Docs"
description: "Armazene dados estruturados na nuvem usando o Armazenamento de Tabelas do Azure, um repositório de dados NoSQL."
services: storage
documentationcenter: .net
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: fe46d883-7bed-49dd-980e-5c71df36adb3
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 04/10/2017
ms.author: marsma
ms.openlocfilehash: 16a9dad1b01fdbef5ec8949bf9ff25497f33d994
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-with-azure-table-storage-using-net"></a><span data-ttu-id="c9cc0-103">Introdução ao armazenamento de Tabelas do Azure usando o .NET</span><span class="sxs-lookup"><span data-stu-id="c9cc0-103">Get started with Azure Table storage using .NET</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-tip-include](../../includes/storage-table-cosmos-db-tip-include.md)]

<span data-ttu-id="c9cc0-104">O Armazenamento de Tabelas do Azure é um serviço que armazena dados NoSQL estruturados na nuvem, fornecendo um repositório chave/atributo com um design sem esquema.</span><span class="sxs-lookup"><span data-stu-id="c9cc0-104">Azure Table storage is a service that stores structured NoSQL data in the cloud, providing a key/attribute store with a schemaless design.</span></span> <span data-ttu-id="c9cc0-105">Como o armazenamento de Tabelas não tem um esquema, é fácil adaptar seus dados à medida que as necessidades de seu aplicativo evoluem.</span><span class="sxs-lookup"><span data-stu-id="c9cc0-105">Because Table storage is schemaless, it's easy to adapt your data as the needs of your application evolve.</span></span> <span data-ttu-id="c9cc0-106">O acesso aos dados do Armazenamento de Tabelas é rápido e econômico para muitos tipos de aplicativos e normalmente tem um custo mais baixo que o SQL tradicional para volumes de dados semelhantes.</span><span class="sxs-lookup"><span data-stu-id="c9cc0-106">Access to Table storage data is fast and cost-effective for many types of applications, and is typically lower in cost than traditional SQL for similar volumes of data.</span></span>

<span data-ttu-id="c9cc0-107">Você pode usar o armazenamento de tabelas para armazenar conjuntos de dados flexíveis, como dados de usuário para aplicativos web, catálogos de endereços, informações sobre dispositivos ou outros tipos de metadados exigidos pelo serviço.</span><span class="sxs-lookup"><span data-stu-id="c9cc0-107">You can use Table storage to store flexible datasets like user data for web applications, address books, device information, or other types of metadata your service requires.</span></span> <span data-ttu-id="c9cc0-108">Você pode armazenar qualquer número de entidades em uma tabela e uma conta de armazenamento pode conter um número ilimitado de tabelas, até o limite de capacidade da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="c9cc0-108">You can store any number of entities in a table, and a storage account may contain any number of tables, up to the capacity limit of the storage account.</span></span>

### <a name="about-this-tutorial"></a><span data-ttu-id="c9cc0-109">Sobre este tutorial</span><span class="sxs-lookup"><span data-stu-id="c9cc0-109">About this tutorial</span></span>
<span data-ttu-id="c9cc0-110">Este tutorial mostra como usar a [Biblioteca do Cliente de Armazenamento do Azure para .NET](https://www.nuget.org/packages/WindowsAzure.Storage/) em alguns cenários comuns do Armazenamento de tabelas do Azure.</span><span class="sxs-lookup"><span data-stu-id="c9cc0-110">This tutorial shows you how to use the [Azure Storage Client Library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage/) in some common Azure Table storage scenarios.</span></span> <span data-ttu-id="c9cc0-111">Esses cenários são apresentados usando exemplos de C# para criar e excluir uma tabela e inserir, atualizar, excluir e consultar dados de tabela.</span><span class="sxs-lookup"><span data-stu-id="c9cc0-111">These scenarios are presented using C# examples for creating and deleting a table, and inserting, updating, deleting, and querying table data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c9cc0-112">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="c9cc0-112">Prerequisites</span></span>

<span data-ttu-id="c9cc0-113">Você precisará do seguinte para concluir este tutorial com sucesso:</span><span class="sxs-lookup"><span data-stu-id="c9cc0-113">You need the following to complete this tutorial successfully:</span></span>

* [<span data-ttu-id="c9cc0-114">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c9cc0-114">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="c9cc0-115">Biblioteca do Cliente de Armazenamento do Azure para .NET</span><span class="sxs-lookup"><span data-stu-id="c9cc0-115">Azure Storage Client Library for .NET</span></span>](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [<span data-ttu-id="c9cc0-116">Gerenciador de Configurações do Azure para .NET</span><span class="sxs-lookup"><span data-stu-id="c9cc0-116">Azure Configuration Manager for .NET</span></span>](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)
* [<span data-ttu-id="c9cc0-117">Conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="c9cc0-117">Azure storage account</span></span>](storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-dotnet-client-library-version-include](../../includes/storage-dotnet-client-library-version-include.md)]

### <a name="more-samples"></a><span data-ttu-id="c9cc0-118">Mais exemplos</span><span class="sxs-lookup"><span data-stu-id="c9cc0-118">More samples</span></span>
<span data-ttu-id="c9cc0-119">Para obter exemplos adicionais usando o Armazenamento de Tabelas, confira [Introdução ao Armazenamento de Tabelas do Azure no .NET](https://azure.microsoft.com/documentation/samples/storage-table-dotnet-getting-started/).</span><span class="sxs-lookup"><span data-stu-id="c9cc0-119">For additional examples using Table storage, see [Getting Started with Azure Table Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-table-dotnet-getting-started/).</span></span> <span data-ttu-id="c9cc0-120">Você pode baixar o aplicativo de exemplo e executá-lo ou procurar o código no GitHub.</span><span class="sxs-lookup"><span data-stu-id="c9cc0-120">You can download the sample application and run it, or browse the code on GitHub.</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-development-environment-include](../../includes/storage-development-environment-include.md)]

### <a name="add-using-directives"></a><span data-ttu-id="c9cc0-121">Adicionar diretivas using</span><span class="sxs-lookup"><span data-stu-id="c9cc0-121">Add using directives</span></span>
<span data-ttu-id="c9cc0-122">Adicione as seguintes diretivas **using** à parte superior do arquivo `Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="c9cc0-122">Add the following **using** directives to the top of the `Program.cs` file:</span></span>

```csharp
using Microsoft.Azure; // Namespace for CloudConfigurationManager
using Microsoft.WindowsAzure.Storage; // Namespace for CloudStorageAccount
using Microsoft.WindowsAzure.Storage.Table; // Namespace for Table storage types
```

### <a name="parse-the-connection-string"></a><span data-ttu-id="c9cc0-123">Analisar a cadeia de conexão</span><span class="sxs-lookup"><span data-stu-id="c9cc0-123">Parse the connection string</span></span>
[!INCLUDE [storage-cloud-configuration-manager-include](../../includes/storage-cloud-configuration-manager-include.md)]

### <a name="create-the-table-service-client"></a><span data-ttu-id="c9cc0-124">Criar o cliente do serviço Tabela</span><span class="sxs-lookup"><span data-stu-id="c9cc0-124">Create the Table service client</span></span>
<span data-ttu-id="c9cc0-125">A classe [CloudTableClient][dotnet_CloudTableClient] permite que você recupere as tabelas e entidades armazenadas no Armazenamento de tabelas.</span><span class="sxs-lookup"><span data-stu-id="c9cc0-125">The [CloudTableClient][dotnet_CloudTableClient] class enables you to retrieve tables and entities stored in Table storage.</span></span> <span data-ttu-id="c9cc0-126">Veja uma maneira de criar o cliente do serviço Tabela:</span><span class="sxs-lookup"><span data-stu-id="c9cc0-126">Here's one way to create the Table service client:</span></span>

```csharp
// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
```

<span data-ttu-id="c9cc0-127">Agora você está pronto para escrever um código que lê e grava dados no Armazenamento de Tabelas.</span><span class="sxs-lookup"><span data-stu-id="c9cc0-127">Now you are ready to write code that reads data from and writes data to Table storage.</span></span>

## <a name="create-a-table"></a><span data-ttu-id="c9cc0-128">Criar uma tabela</span><span class="sxs-lookup"><span data-stu-id="c9cc0-128">Create a table</span></span>
<span data-ttu-id="c9cc0-129">Este exemplo mostra como criar uma tabela se ela ainda não existe:</span><span class="sxs-lookup"><span data-stu-id="c9cc0-129">This example shows how to create a table if it does not already exist:</span></span>

```csharp
// Retrieve the storage account from the connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Retrieve a reference to the table.
CloudTable table = tableClient.GetTableReference("people");

// Create the table if it doesn't exist.
table.CreateIfNotExists();
```

## <a name="add-an-entity-to-a-table"></a><span data-ttu-id="c9cc0-130">Adicionar uma entidade a uma tabela</span><span class="sxs-lookup"><span data-stu-id="c9cc0-130">Add an entity to a table</span></span>
<span data-ttu-id="c9cc0-131">As entidades são mapeadas para objetos C# usando uma classe personalizada derivada de [TableEntity][dotnet_TableEntity].</span><span class="sxs-lookup"><span data-stu-id="c9cc0-131">Entities map to C# objects by using a custom class derived from [TableEntity][dotnet_TableEntity].</span></span> <span data-ttu-id="c9cc0-132">Para adicionar uma entidade a uma tabela, crie uma classe que defina as propriedades da sua entidade.</span><span class="sxs-lookup"><span data-stu-id="c9cc0-132">To add an entity to a table, create a class that defines the properties of your entity.</span></span> <span data-ttu-id="c9cc0-133">O código a seguir define uma classe de entidade que usa o nome do cliente como a chave de linha e o sobrenome como a chave de partição.</span><span class="sxs-lookup"><span data-stu-id="c9cc0-133">The following code defines an entity class that uses the customer's first name as the row key and last name as the partition key.</span></span> <span data-ttu-id="c9cc0-134">Juntas, uma chave de partição e uma chave de linha identificam exclusivamente a entidade na tabela.</span><span class="sxs-lookup"><span data-stu-id="c9cc0-134">Together, an entity's partition and row key uniquely identify it in the table.</span></span> <span data-ttu-id="c9cc0-135">As entidades com a mesma chave de partição podem ser consultadas mais rápido do que aquelas com chaves de partição diferentes, mas usar chaves de partição diferentes permite uma escalabilidade maior de operações paralelas.</span><span class="sxs-lookup"><span data-stu-id="c9cc0-135">Entities with the same partition key can be queried faster than entities with different partition keys, but using diverse partition keys allows for greater scalability of parallel operations.</span></span> <span data-ttu-id="c9cc0-136">As entidades que serão armazenadas em tabelas deverão ser de um tipo com suporte, por exemplo, derivado da classe [TableEntity][dotnet_TableEntity].</span><span class="sxs-lookup"><span data-stu-id="c9cc0-136">Entities to be stored in tables must be of a supported type, for example derived from the [TableEntity][dotnet_TableEntity] class.</span></span> <span data-ttu-id="c9cc0-137">As propriedades de entidade que você gostaria de armazenar em uma tabela precisam ser propriedades públicas do tipo e dar suporte à obtenção e à definição dos valores.</span><span class="sxs-lookup"><span data-stu-id="c9cc0-137">Entity properties you'd like to store in a table must be public properties of the type, and support both getting and setting of values.</span></span> <span data-ttu-id="c9cc0-138">Além disso, o tipo de entidade *deve* expor um construtor sem parâmetros.</span><span class="sxs-lookup"><span data-stu-id="c9cc0-138">Also, your entity type *must* expose a parameter-less constructor.</span></span>

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

<span data-ttu-id="c9cc0-139">As operações de tabela que envolvam entidades são executadas usando o objeto [CloudTable][dotnet_CloudTable] que você criou na seção “Criar uma tabela”.</span><span class="sxs-lookup"><span data-stu-id="c9cc0-139">Table operations that involve entities are performed via the [CloudTable][dotnet_CloudTable] object that you created earlier in the "Create a table" section.</span></span> <span data-ttu-id="c9cc0-140">A operação a ser executada é representada por um objeto [TableOperation][dotnet_TableOperation].</span><span class="sxs-lookup"><span data-stu-id="c9cc0-140">The operation to be performed is represented by a [TableOperation][dotnet_TableOperation] object.</span></span> <span data-ttu-id="c9cc0-141">O exemplo de código a seguir mostra a criação do objeto [CloudTable][dotnet_CloudTable] e, em seguida, de um objeto **CustomerEntity**.</span><span class="sxs-lookup"><span data-stu-id="c9cc0-141">The following code example shows the creation of the [CloudTable][dotnet_CloudTable] object and then a **CustomerEntity** object.</span></span> <span data-ttu-id="c9cc0-142">Para preparar a operação, um objeto [TableOperation][dotnet_TableOperation] é criado para inserir a entidade customer na tabela.</span><span class="sxs-lookup"><span data-stu-id="c9cc0-142">To prepare the operation, a [TableOperation][dotnet_TableOperation] object is created to insert the customer entity into the table.</span></span> <span data-ttu-id="c9cc0-143">Finalmente, a operação é executada chamando [CloudTable][dotnet_CloudTable].[Execute][dotnet_CloudTable_Execute].</span><span class="sxs-lookup"><span data-stu-id="c9cc0-143">Finally, the operation is executed by calling [CloudTable][dotnet_CloudTable].[Execute][dotnet_CloudTable_Execute].</span></span>

```csharp
// Retrieve the storage account from the connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create the CloudTable object that represents the "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create a new customer entity.
CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
customer1.Email = "Walter@contoso.com";
customer1.PhoneNumber = "425-555-0101";

// Create the TableOperation object that inserts the customer entity.
TableOperation insertOperation = TableOperation.Insert(customer1);

// Execute the insert operation.
table.Execute(insertOperation);
```

## <a name="insert-a-batch-of-entities"></a><span data-ttu-id="c9cc0-144">Inserir um lote de entidades</span><span class="sxs-lookup"><span data-stu-id="c9cc0-144">Insert a batch of entities</span></span>
<span data-ttu-id="c9cc0-145">Você pode inserir um lote de entidades em uma tabela em uma única operação de gravação.</span><span class="sxs-lookup"><span data-stu-id="c9cc0-145">You can insert a batch of entities into a table in one write operation.</span></span> <span data-ttu-id="c9cc0-146">Algumas outras observações sobre operações em lote:</span><span class="sxs-lookup"><span data-stu-id="c9cc0-146">Some other notes on batch operations:</span></span>

* <span data-ttu-id="c9cc0-147">Você pode executar atualizações, exclusões e inserções em uma única operação em lote.</span><span class="sxs-lookup"><span data-stu-id="c9cc0-147">You can perform updates, deletes, and inserts in the same single batch operation.</span></span>
* <span data-ttu-id="c9cc0-148">Uma única operação em lotes pode incluir até 100 entidades.</span><span class="sxs-lookup"><span data-stu-id="c9cc0-148">A single batch operation can include up to 100 entities.</span></span>
* <span data-ttu-id="c9cc0-149">Todas as entidades em uma única operação em lote devem ter a mesma chave de partição.</span><span class="sxs-lookup"><span data-stu-id="c9cc0-149">All entities in a single batch operation must have the same partition key.</span></span>
* <span data-ttu-id="c9cc0-150">Embora seja possível executar uma consulta como uma operação em lotes, ele deve ser a única operação em lote.</span><span class="sxs-lookup"><span data-stu-id="c9cc0-150">While it is possible to perform a query as a batch operation, it must be the only operation in the batch.</span></span>

<span data-ttu-id="c9cc0-151">O exemplo de código a seguir cria dois objetos de entidade e adiciona cada um a uma [TableBatchOperation][dotnet_TableBatchOperation] usando o método [Insert][dotnet_TableBatchOperation_Insert].</span><span class="sxs-lookup"><span data-stu-id="c9cc0-151">The following code example creates two entity objects and adds each to [TableBatchOperation][dotnet_TableBatchOperation] by using the [Insert][dotnet_TableBatchOperation_Insert] method.</span></span> <span data-ttu-id="c9cc0-152">Em seguida, [CloudTable][dotnet_CloudTable].[ExecuteBatch][dotnet_CloudTable_ExecuteBatch] é chamado para executar a operação.</span><span class="sxs-lookup"><span data-stu-id="c9cc0-152">Then, [CloudTable][dotnet_CloudTable].[ExecuteBatch][dotnet_CloudTable_ExecuteBatch] is called to execute the operation.</span></span>

```csharp
// Retrieve the storage account from the connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create the CloudTable object that represents the "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create the batch operation.
TableBatchOperation batchOperation = new TableBatchOperation();

// Create a customer entity and add it to the table.
CustomerEntity customer1 = new CustomerEntity("Smith", "Jeff");
customer1.Email = "Jeff@contoso.com";
customer1.PhoneNumber = "425-555-0104";

// Create another customer entity and add it to the table.
CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
customer2.Email = "Ben@contoso.com";
customer2.PhoneNumber = "425-555-0102";

// Add both customer entities to the batch insert operation.
batchOperation.Insert(customer1);
batchOperation.Insert(customer2);

// Execute the batch operation.
table.ExecuteBatch(batchOperation);
```

## <a name="retrieve-all-entities-in-a-partition"></a><span data-ttu-id="c9cc0-153">Recuperar todas as entidades em uma partição</span><span class="sxs-lookup"><span data-stu-id="c9cc0-153">Retrieve all entities in a partition</span></span>
<span data-ttu-id="c9cc0-154">Para consultar uma tabela de todas as entidades em uma partição, use um objeto [TableQuery][dotnet_TableQuery].</span><span class="sxs-lookup"><span data-stu-id="c9cc0-154">To query a table for all entities in a partition, use a [TableQuery][dotnet_TableQuery] object.</span></span> <span data-ttu-id="c9cc0-155">O exemplo de código a seguir especifica um filtro para as entidades em que 'Smith’ é a chave de partição.</span><span class="sxs-lookup"><span data-stu-id="c9cc0-155">The following code example specifies a filter for entities where 'Smith' is the partition key.</span></span> <span data-ttu-id="c9cc0-156">Esse exemplo imprime os campos de cada entidade nos resultados da consulta no console.</span><span class="sxs-lookup"><span data-stu-id="c9cc0-156">This example prints the fields of each entity in the query results to the console.</span></span>

```csharp
// Retrieve the storage account from the connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create the CloudTable object that represents the "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Construct the query operation for all customer entities where PartitionKey="Smith".
TableQuery<CustomerEntity> query = new TableQuery<CustomerEntity>().Where(TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"));

// Print the fields for each customer.
foreach (CustomerEntity entity in table.ExecuteQuery(query))
{
    Console.WriteLine("{0}, {1}\t{2}\t{3}", entity.PartitionKey, entity.RowKey,
        entity.Email, entity.PhoneNumber);
}
```

## <a name="retrieve-a-range-of-entities-in-a-partition"></a><span data-ttu-id="c9cc0-157">Recuperar um intervalo de entidades em uma partição</span><span class="sxs-lookup"><span data-stu-id="c9cc0-157">Retrieve a range of entities in a partition</span></span>
<span data-ttu-id="c9cc0-158">Se não desejar consultar todas as entidades em uma partição, você poderá especificar um intervalo combinando o filtro de chave de partição com um filtro de chave de linha.</span><span class="sxs-lookup"><span data-stu-id="c9cc0-158">If you don't want to query all entities in a partition, you can specify a range by combining the partition key filter with a row key filter.</span></span> <span data-ttu-id="c9cc0-159">O exemplo de código a seguir usa dois filtros para obter todas as entidades na partição 'Smith' onde a chave de linha (nome) começa com uma letra anterior a 'E' do alfabeto e imprime os resultados da consulta.</span><span class="sxs-lookup"><span data-stu-id="c9cc0-159">The following code example uses two filters to get all entities in partition 'Smith' where the row key (first name) starts with a letter before 'E' in the alphabet, then prints the query results.</span></span>

```csharp
// Retrieve the storage account from the connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create the CloudTable object that represents the "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create the table query.
TableQuery<CustomerEntity> rangeQuery = new TableQuery<CustomerEntity>().Where(
    TableQuery.CombineFilters(
        TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"),
        TableOperators.And,
        TableQuery.GenerateFilterCondition("RowKey", QueryComparisons.LessThan, "E")));

// Loop through the results, displaying information about the entity.
foreach (CustomerEntity entity in table.ExecuteQuery(rangeQuery))
{
    Console.WriteLine("{0}, {1}\t{2}\t{3}", entity.PartitionKey, entity.RowKey,
        entity.Email, entity.PhoneNumber);
}
```

## <a name="retrieve-a-single-entity"></a><span data-ttu-id="c9cc0-160">Recuperar uma única entidade</span><span class="sxs-lookup"><span data-stu-id="c9cc0-160">Retrieve a single entity</span></span>
<span data-ttu-id="c9cc0-161">Você pode escrever uma consulta para recuperar uma entidade única e específica.</span><span class="sxs-lookup"><span data-stu-id="c9cc0-161">You can write a query to retrieve a single, specific entity.</span></span> <span data-ttu-id="c9cc0-162">O código a seguir usa [TableOperation][dotnet_TableOperation] para especificar o cliente 'Mateus Rodrigues'.</span><span class="sxs-lookup"><span data-stu-id="c9cc0-162">The following code uses [TableOperation][dotnet_TableOperation] to specify the customer 'Ben Smith'.</span></span> <span data-ttu-id="c9cc0-163">Este método retorna uma única entidade, em vez de uma coleção, e o valor retornado no [TableResult][dotnet_TableResult].[Result][dotnet_TableResult_Result] é um objeto **CustomerEntity**.</span><span class="sxs-lookup"><span data-stu-id="c9cc0-163">This method returns just one entity rather than a collection, and the returned value in [TableResult][dotnet_TableResult].[Result][dotnet_TableResult_Result] is a **CustomerEntity** object.</span></span> <span data-ttu-id="c9cc0-164">Especificar chaves de partição e de linha em uma consulta é a maneira mais rápida de recuperar uma única entidade de serviço Table.</span><span class="sxs-lookup"><span data-stu-id="c9cc0-164">Specifying both partition and row keys in a query is the fastest way to retrieve a single entity from the Table service.</span></span>

```csharp
// Retrieve the storage account from the connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create the CloudTable object that represents the "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create a retrieve operation that takes a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute the retrieve operation.
TableResult retrievedResult = table.Execute(retrieveOperation);

// Print the phone number of the result.
if (retrievedResult.Result != null)
{
    Console.WriteLine(((CustomerEntity)retrievedResult.Result).PhoneNumber);
}
else
{
    Console.WriteLine("The phone number could not be retrieved.");
}
```

## <a name="replace-an-entity"></a><span data-ttu-id="c9cc0-165">Substituir uma entidade</span><span class="sxs-lookup"><span data-stu-id="c9cc0-165">Replace an entity</span></span>
<span data-ttu-id="c9cc0-166">Para atualizar uma entidade, recupere-a do serviço Tabela, modifique o objeto de entidade e, em seguida, salve as alterações novamente no serviço Tabela.</span><span class="sxs-lookup"><span data-stu-id="c9cc0-166">To update an entity, retrieve it from the Table service, modify the entity object, and then save the changes back to the Table service.</span></span> <span data-ttu-id="c9cc0-167">O código a seguir altera o número de telefone de um cliente existente.</span><span class="sxs-lookup"><span data-stu-id="c9cc0-167">The following code changes an existing customer's phone number.</span></span> <span data-ttu-id="c9cc0-168">Em vez de chamar [Insert][dotnet_TableOperation_Insert], esse código usa [Replace][dotnet_TableOperation_Replace].</span><span class="sxs-lookup"><span data-stu-id="c9cc0-168">Instead of calling [Insert][dotnet_TableOperation_Insert], this code uses [Replace][dotnet_TableOperation_Replace].</span></span> <span data-ttu-id="c9cc0-169">[Replace][dotnet_TableOperation_Replace] faz com que a entidade seja totalmente substituída no servidor, a menos que a entidade no servidor tenha sido alterada desde que foi recuperada, caso em que haverá falha na operação.</span><span class="sxs-lookup"><span data-stu-id="c9cc0-169">[Replace][dotnet_TableOperation_Replace] causes the entity to be fully replaced on the server, unless the entity on the server has changed since it was retrieved, in which case the operation will fail.</span></span> <span data-ttu-id="c9cc0-170">Essa falha é para impedir que seu aplicativo substitua inadvertidamente uma alteração feita entre a recuperação e a atualização por outro componente de seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c9cc0-170">This failure is to prevent your application from inadvertently overwriting a change made between the retrieval and update by another component of your application.</span></span> <span data-ttu-id="c9cc0-171">O tratamento correto dessa falha é recuperar a entidade novamente, fazer as alterações (se ainda forem válidas) e executar outra operação [Replace][dotnet_TableOperation_Replace].</span><span class="sxs-lookup"><span data-stu-id="c9cc0-171">The proper handling of this failure is to retrieve the entity again, make your changes (if still valid), and then perform another [Replace][dotnet_TableOperation_Replace] operation.</span></span> <span data-ttu-id="c9cc0-172">A próxima seção mostrará como substituir esse comportamento.</span><span class="sxs-lookup"><span data-stu-id="c9cc0-172">The next section will show you how to override this behavior.</span></span>

```csharp
// Retrieve the storage account from the connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create the CloudTable object that represents the "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create a retrieve operation that takes a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute the operation.
TableResult retrievedResult = table.Execute(retrieveOperation);

// Assign the result to a CustomerEntity object.
CustomerEntity updateEntity = (CustomerEntity)retrievedResult.Result;

if (updateEntity != null)
{
    // Change the phone number.
    updateEntity.PhoneNumber = "425-555-0105";

    // Create the Replace TableOperation.
    TableOperation updateOperation = TableOperation.Replace(updateEntity);

    // Execute the operation.
    table.Execute(updateOperation);

    Console.WriteLine("Entity updated.");
}
else
{
    Console.WriteLine("Entity could not be retrieved.");
}
```

## <a name="insert-or-replace-an-entity"></a><span data-ttu-id="c9cc0-173">Inserir ou substituir uma entidade</span><span class="sxs-lookup"><span data-stu-id="c9cc0-173">Insert-or-replace an entity</span></span>
<span data-ttu-id="c9cc0-174">A operação [Replace][dotnet_TableOperation_Replace] falhará se a entidade tiver sido alterada depois de ter sido recuperada do servidor.</span><span class="sxs-lookup"><span data-stu-id="c9cc0-174">[Replace][dotnet_TableOperation_Replace] operations will fail if the entity has been changed since it was retrieved from the server.</span></span> <span data-ttu-id="c9cc0-175">Além disso, primeiro você precisa recuperar a entidade do servidor para que a operação [Replace][dotnet_TableOperation_Replace] seja bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="c9cc0-175">Furthermore, you must retrieve the entity from the server first in order for the [Replace][dotnet_TableOperation_Replace] operation to be successful.</span></span> <span data-ttu-id="c9cc0-176">No entanto, às vezes você não sabe se a entidade existe no servidor, e se os valores atuais armazenados nela são irrelevantes.</span><span class="sxs-lookup"><span data-stu-id="c9cc0-176">Sometimes, however, you don't know if the entity exists on the server and the current values stored in it are irrelevant.</span></span> <span data-ttu-id="c9cc0-177">A atualização deve substituir todos eles.</span><span class="sxs-lookup"><span data-stu-id="c9cc0-177">Your update should overwrite them all.</span></span> <span data-ttu-id="c9cc0-178">Para fazer isso, você deve usar uma operação [InsertOrReplace][dotnet_TableOperation_InsertOrReplace].</span><span class="sxs-lookup"><span data-stu-id="c9cc0-178">To accomplish this, you would use an [InsertOrReplace][dotnet_TableOperation_InsertOrReplace] operation.</span></span> <span data-ttu-id="c9cc0-179">Essa operação insere a entidade, se ela não existir, ou a substitui, se ela existir, independentemente de quando foi feita a última atualização.</span><span class="sxs-lookup"><span data-stu-id="c9cc0-179">This operation inserts the entity if it doesn't exist, or replaces it if it does, regardless of when the last update was made.</span></span>

<span data-ttu-id="c9cc0-180">No exemplo de código a seguir, uma entidade de cliente 'Vinicius Monte' é criada e inserida na tabela 'pessoas'.</span><span class="sxs-lookup"><span data-stu-id="c9cc0-180">In the following code example, a customer entity for 'Fred Jones' is created and inserted into the 'people' table.</span></span> <span data-ttu-id="c9cc0-181">Em seguida, usamos a operação [InsertOrReplace][dotnet_TableOperation_InsertOrReplace] para salvar uma entidade com a mesma chave de partição (Monte) e chave de linha (Vinicius) para o servidor, dessa vez com um valor diferente para a propriedade PhoneNumber.</span><span class="sxs-lookup"><span data-stu-id="c9cc0-181">Next, we use the [InsertOrReplace][dotnet_TableOperation_InsertOrReplace] operation to save an entity with the same partition key (Jones) and row key (Fred) to the server, this time with a different value for the PhoneNumber property.</span></span> <span data-ttu-id="c9cc0-182">Como usamos [InsertOrReplace][dotnet_TableOperation_InsertOrReplace], todos os seus valores de propriedade serão substituídos.</span><span class="sxs-lookup"><span data-stu-id="c9cc0-182">Because we use [InsertOrReplace][dotnet_TableOperation_InsertOrReplace], all of its property values are replaced.</span></span> <span data-ttu-id="c9cc0-183">No entanto, se uma entidade 'Vinicius Monte' já não existia na tabela, ela foi inserida.</span><span class="sxs-lookup"><span data-stu-id="c9cc0-183">However, if a 'Fred Jones' entity hadn't already existed in the table, it would have been inserted.</span></span>

```csharp
// Retrieve the storage account from the connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create the CloudTable object that represents the "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create a customer entity.
CustomerEntity customer3 = new CustomerEntity("Jones", "Fred");
customer3.Email = "Fred@contoso.com";
customer3.PhoneNumber = "425-555-0106";

// Create the TableOperation object that inserts the customer entity.
TableOperation insertOperation = TableOperation.Insert(customer3);

// Execute the operation.
table.Execute(insertOperation);

// Create another customer entity with the same partition key and row key.
// We've already created a 'Fred Jones' entity and saved it to the
// 'people' table, but here we're specifying a different value for the
// PhoneNumber property.
CustomerEntity customer4 = new CustomerEntity("Jones", "Fred");
customer4.Email = "Fred@contoso.com";
customer4.PhoneNumber = "425-555-0107";

// Create the InsertOrReplace TableOperation.
TableOperation insertOrReplaceOperation = TableOperation.InsertOrReplace(customer4);

// Execute the operation. Because a 'Fred Jones' entity already exists in the
// 'people' table, its property values will be overwritten by those in this
// CustomerEntity. If 'Fred Jones' didn't already exist, the entity would be
// added to the table.
table.Execute(insertOrReplaceOperation);
```

## <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="c9cc0-184">consultar um subconjunto de propriedades da entidade</span><span class="sxs-lookup"><span data-stu-id="c9cc0-184">Query a subset of entity properties</span></span>
<span data-ttu-id="c9cc0-185">Uma consulta de tabela pode recuperar apenas algumas propriedades de uma entidade em vez de todas as propriedades da entidade.</span><span class="sxs-lookup"><span data-stu-id="c9cc0-185">A table query can retrieve just a few properties from an entity instead of all the entity properties.</span></span> <span data-ttu-id="c9cc0-186">Essa técnica, chamada projeção, reduz a largura de banda e pode melhorar o desempenho da consulta, principalmente para grandes entidades.</span><span class="sxs-lookup"><span data-stu-id="c9cc0-186">This technique, called projection, reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="c9cc0-187">A consulta no código a seguir retorna somente os endereços de email das entidades na tabela.</span><span class="sxs-lookup"><span data-stu-id="c9cc0-187">The query in the following code returns only the email addresses of entities in the table.</span></span> <span data-ttu-id="c9cc0-188">Isso é feito por meio de uma consulta de [DynamicTableEntity][dotnet_DynamicTableEntity] e também de [EntityResolver][dotnet_EntityResolver].</span><span class="sxs-lookup"><span data-stu-id="c9cc0-188">This is done by using a query of [DynamicTableEntity][dotnet_DynamicTableEntity] and also [EntityResolver][dotnet_EntityResolver].</span></span> <span data-ttu-id="c9cc0-189">Saiba mais sobre projeção na [postagem de blog Apresentando a projeção de upsert e de consulta][blog_post_upsert].</span><span class="sxs-lookup"><span data-stu-id="c9cc0-189">You can learn more about projection in the [Introducing Upsert and Query Projection blog post][blog_post_upsert].</span></span> <span data-ttu-id="c9cc0-190">A projeção não tem suporte pelo emulador de armazenamento e, portanto, esse código é executado somente ao usar uma conta no serviço Tabela.</span><span class="sxs-lookup"><span data-stu-id="c9cc0-190">Projection is not supported by the storage emulator, so this code runs only when you're using an account in the Table service.</span></span>

```csharp
// Retrieve the storage account from the connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create the CloudTable that represents the "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Define the query, and select only the Email property.
TableQuery<DynamicTableEntity> projectionQuery = new TableQuery<DynamicTableEntity>().Select(new string[] { "Email" });

// Define an entity resolver to work with the entity after retrieval.
EntityResolver<string> resolver = (pk, rk, ts, props, etag) => props.ContainsKey("Email") ? props["Email"].StringValue : null;

foreach (string projectedEmail in table.ExecuteQuery(projectionQuery, resolver, null, null))
{
    Console.WriteLine(projectedEmail);
}
```

## <a name="delete-an-entity"></a><span data-ttu-id="c9cc0-191">Excluir uma entidade</span><span class="sxs-lookup"><span data-stu-id="c9cc0-191">Delete an entity</span></span>
<span data-ttu-id="c9cc0-192">Você pode excluir facilmente uma entidade após a recuperação usando o mesmo padrão mostrado para a atualização de uma entidade.</span><span class="sxs-lookup"><span data-stu-id="c9cc0-192">You can easily delete an entity after you have retrieved it by using the same pattern shown for updating an entity.</span></span> <span data-ttu-id="c9cc0-193">O código a seguir recupera e exclui uma entidade de cliente.</span><span class="sxs-lookup"><span data-stu-id="c9cc0-193">The following code retrieves and deletes a customer entity.</span></span>

```csharp
// Retrieve the storage account from the connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create the CloudTable that represents the "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create a retrieve operation that expects a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute the operation.
TableResult retrievedResult = table.Execute(retrieveOperation);

// Assign the result to a CustomerEntity.
CustomerEntity deleteEntity = (CustomerEntity)retrievedResult.Result;

// Create the Delete TableOperation.
if (deleteEntity != null)
{
    TableOperation deleteOperation = TableOperation.Delete(deleteEntity);

    // Execute the operation.
    table.Execute(deleteOperation);

    Console.WriteLine("Entity deleted.");
}
else
{
    Console.WriteLine("Could not retrieve the entity.");
}
```

## <a name="delete-a-table"></a><span data-ttu-id="c9cc0-194">Excluir uma tabela</span><span class="sxs-lookup"><span data-stu-id="c9cc0-194">Delete a table</span></span>
<span data-ttu-id="c9cc0-195">Finalmente, o exemplo de código a seguir exclui uma tabela de uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="c9cc0-195">Finally, the following code example deletes a table from a storage account.</span></span> <span data-ttu-id="c9cc0-196">Uma tabela excluída não estará disponível para ser recriada durante um período após a exclusão.</span><span class="sxs-lookup"><span data-stu-id="c9cc0-196">A table that has been deleted will be unavailable to be re-created for a period of time following the deletion.</span></span>

```csharp
// Retrieve the storage account from the connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create the CloudTable that represents the "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Delete the table it if exists.
table.DeleteIfExists();
```

## <a name="retrieve-entities-in-pages-asynchronously"></a><span data-ttu-id="c9cc0-197">Recuperar entidades nas páginas de forma assíncrona</span><span class="sxs-lookup"><span data-stu-id="c9cc0-197">Retrieve entities in pages asynchronously</span></span>
<span data-ttu-id="c9cc0-198">Se estiver lendo um grande número de entidades e quiser processar/exibir as entidades quando elas forem recuperadas em vez de esperar que todas sejam retornadas, você pode recuperar as entidades usando uma consulta segmentada.</span><span class="sxs-lookup"><span data-stu-id="c9cc0-198">If you are reading a large number of entities, and you want to process/display entities as they are retrieved rather than waiting for them all to return, you can retrieve entities by using a segmented query.</span></span> <span data-ttu-id="c9cc0-199">Este exemplo mostra como retornar resultados nas páginas usando o padrão Async-Await para que a execução não fique bloqueada enquanto você espera o retorno de um grande conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="c9cc0-199">This example shows how to return results in pages by using the Async-Await pattern so that execution is not blocked while you're waiting for a large set of results to return.</span></span> <span data-ttu-id="c9cc0-200">Para obter mais detalhes sobre como usar o padrão Async-Await no .NET, consulte [Programação assíncrona com Async e Await (C# e Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)</span><span class="sxs-lookup"><span data-stu-id="c9cc0-200">For more details on using the Async-Await pattern in .NET, see [Asynchronous programming with Async and Await (C# and Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx).</span></span>

```csharp
// Initialize a default TableQuery to retrieve all the entities in the table.
TableQuery<CustomerEntity> tableQuery = new TableQuery<CustomerEntity>();

// Initialize the continuation token to null to start from the beginning of the table.
TableContinuationToken continuationToken = null;

do
{
    // Retrieve a segment (up to 1,000 entities).
    TableQuerySegment<CustomerEntity> tableQueryResult =
        await table.ExecuteQuerySegmentedAsync(tableQuery, continuationToken);

    // Assign the new continuation token to tell the service where to
    // continue on the next iteration (or null if it has reached the end).
    continuationToken = tableQueryResult.ContinuationToken;

    // Print the number of rows retrieved.
    Console.WriteLine("Rows retrieved {0}", tableQueryResult.Results.Count);

// Loop until a null continuation token is received, indicating the end of the table.
} while(continuationToken != null);
```

## <a name="next-steps"></a><span data-ttu-id="c9cc0-201">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c9cc0-201">Next steps</span></span>
<span data-ttu-id="c9cc0-202">Agora que você aprendeu os conceitos básicos do armazenamento de Tabela, siga estes links para saber mais sobre tarefas de armazenamento mais complexas:</span><span class="sxs-lookup"><span data-stu-id="c9cc0-202">Now that you've learned the basics of Table storage, follow these links to learn about more complex storage tasks:</span></span>

* <span data-ttu-id="c9cc0-203">[O Gerenciador de Armazenamento do Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md) é um aplicativo autônomo e gratuito da Microsoft que possibilita o trabalho visual com os dados do Armazenamento do Azure no Windows, MacOS e Linux.</span><span class="sxs-lookup"><span data-stu-id="c9cc0-203">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you to work visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* <span data-ttu-id="c9cc0-204">Ver mais exemplos de Armazenamento de Tabelas na [Introdução ao Armazenamento de Tabelas do Azure no .NET](https://azure.microsoft.com/documentation/samples/storage-table-dotnet-getting-started/)</span><span class="sxs-lookup"><span data-stu-id="c9cc0-204">See more Table storage samples in [Getting Started with Azure Table Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-table-dotnet-getting-started/)</span></span>
* <span data-ttu-id="c9cc0-205">Consulte a documentação de referência do serviço Tabela para obter detalhes completos sobre as APIs disponíveis:</span><span class="sxs-lookup"><span data-stu-id="c9cc0-205">View the Table service reference documentation for complete details about available APIs:</span></span>
* [<span data-ttu-id="c9cc0-206">Referência à Biblioteca de Cliente de Armazenamento para .NET</span><span class="sxs-lookup"><span data-stu-id="c9cc0-206">Storage Client Library for .NET reference</span></span>](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)
* [<span data-ttu-id="c9cc0-207">Referência da API REST</span><span class="sxs-lookup"><span data-stu-id="c9cc0-207">REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* <span data-ttu-id="c9cc0-208">Saiba como simplificar o código que você escreve para  trabalhar com o Armazenamento do Azure usando o [SDK do Azure WebJobs](../app-service-web/websites-dotnet-webjobs-sdk-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="c9cc0-208">Learn how to simplify the code you write to work with Azure Storage by using the [Azure WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-get-started.md)</span></span>
* <span data-ttu-id="c9cc0-209">Consulte outros guias de recursos para obter informações sobre opções adicionais para armazenar dados no Azure.</span><span class="sxs-lookup"><span data-stu-id="c9cc0-209">View more feature guides to learn about additional options for storing data in Azure.</span></span>
* <span data-ttu-id="c9cc0-210">[Introdução ao armazenamento de Blobs do Azure usando o .NET](storage-dotnet-how-to-use-blobs.md) para armazenar dados não estruturados.</span><span class="sxs-lookup"><span data-stu-id="c9cc0-210">[Get started with Azure Blob storage using .NET](storage-dotnet-how-to-use-blobs.md) to store unstructured data.</span></span>
* <span data-ttu-id="c9cc0-211">[Conectar-se ao Banco de Dados SQL usando .NET (C#)](../sql-database/sql-database-develop-dotnet-simple.md) para armazenar dados relacionais.</span><span class="sxs-lookup"><span data-stu-id="c9cc0-211">[Connect to SQL Database by using .NET (C#)](../sql-database/sql-database-develop-dotnet-simple.md) to store relational data.</span></span>

[Download and install the Azure SDK for .NET]: /develop/net/
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
