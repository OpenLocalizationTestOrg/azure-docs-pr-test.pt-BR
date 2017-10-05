---
title: "Introdução ao armazenamento de tabelas e aos serviços conectados do Visual Studio (ASP.NET Core) | Microsoft Docs"
description: "Como começar a usar o armazenamento de Tabela do Azure em um projeto do ASP.NET Core no Visual Studio após a conexão a uma conta de armazenamento usando os serviços conectados do Visual Studio"
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: c3c451d1-71ff-4222-a348-c41c98a02b85
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: b64d4f7e55977c7ce144987f7600e5ddcb25596c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-get-started-with-azure-table-storage-and-visual-studio-connected-services"></a><span data-ttu-id="eef0d-103">Introdução ao armazenamento de Tabela do Azure e serviços conectados do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="eef0d-103">How to get started with Azure Table storage and Visual Studio connected services</span></span>
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a><span data-ttu-id="eef0d-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="eef0d-104">Overview</span></span>
<span data-ttu-id="eef0d-105">Este artigo descreve como começar a usar o Armazenamento de Tabelas do Azure no Visual Studio depois de ter criado ou referenciado uma conta de armazenamento do Azure em um projeto ASP.NET Core, usando a caixa de diálogo **Adicionar Serviços Conectados** do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="eef0d-105">This article describes how get started using Azure Table storage in Visual Studio after you have created or referenced an Azure storage account in an ASP.NET Core project by using the Visual Studio **Add Connected Services** dialog.</span></span>

<span data-ttu-id="eef0d-106">O serviço de armazenamento de Tabela do Azure armazena grandes quantidades de dados estruturados.</span><span class="sxs-lookup"><span data-stu-id="eef0d-106">The Azure Table storage service enables you to store large amounts of structured data.</span></span> <span data-ttu-id="eef0d-107">O serviço é um armazenamento de dados NoSQL que aceita chamadas autenticadas de dentro e de fora da nuvem do Azure.</span><span class="sxs-lookup"><span data-stu-id="eef0d-107">The service is a NoSQL data store that accepts authenticated calls from inside and outside the Azure cloud.</span></span> <span data-ttu-id="eef0d-108">As tabelas do Azure são ideais para armazenar dados estruturados não relacionais.</span><span class="sxs-lookup"><span data-stu-id="eef0d-108">Azure tables are ideal for storing structured, non-relational data.</span></span>

<span data-ttu-id="eef0d-109">A operação **Adicionar Serviços Conectados** instala os pacotes NuGet apropriados para acessar o armazenamento do Azure no seu projeto e adiciona a cadeia de conexão para a conta de armazenamento aos arquivos de configuração do projeto.</span><span class="sxs-lookup"><span data-stu-id="eef0d-109">The **Add Connected Services** operation installs the appropriate NuGet packages to access Azure storage in your project and adds the connection string for the storage account to your project configuration files.</span></span>

<span data-ttu-id="eef0d-110">Para obter mais informações sobre como usar o Armazenamento de Tabelas do Azure, consulte [Introdução ao armazenamento de Tabelas do Azure usando o .NET](storage-dotnet-how-to-use-tables.md).</span><span class="sxs-lookup"><span data-stu-id="eef0d-110">For more general information about using Azure Table storage, see [Get started with Azure Table storage using .NET](storage-dotnet-how-to-use-tables.md).</span></span>

<span data-ttu-id="eef0d-111">Para começar, primeiramente, você precisa criar uma tabela em sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="eef0d-111">To get started, you first need to create a table in your storage account.</span></span> <span data-ttu-id="eef0d-112">Mostraremos como criar uma tabela do Azure em código.</span><span class="sxs-lookup"><span data-stu-id="eef0d-112">We'll show you how to create an Azure table in code.</span></span> <span data-ttu-id="eef0d-113">Também mostraremos como realizar operações básicas de tabela e entidade, como adicionar, modificar, ler e ler entidades de tabela.</span><span class="sxs-lookup"><span data-stu-id="eef0d-113">We'll also show you how to perform basic table and entity operations, such as adding, modifying, reading and reading table entities.</span></span> <span data-ttu-id="eef0d-114">Os exemplos são escritos em C\# e usam a biblioteca do cliente de armazenamento do Azure para .NET.</span><span class="sxs-lookup"><span data-stu-id="eef0d-114">The samples are written in C\# code and use the Azure Storage Client Library for .NET.</span></span>

<span data-ttu-id="eef0d-115">**OBSERVAÇÃO** – algumas APIs que executam chamadas para o armazenamento do Azure no ASP.NET Core são assíncronas.</span><span class="sxs-lookup"><span data-stu-id="eef0d-115">**NOTE** - Some of the APIs that perform calls out to Azure storage in ASP.NET Core are asynchronous.</span></span> <span data-ttu-id="eef0d-116">Confira [Programação assíncrona com Async e Await](http://msdn.microsoft.com/library/hh191443.aspx) para saber mais.</span><span class="sxs-lookup"><span data-stu-id="eef0d-116">See [Asynchronous Programming with Async and Await](http://msdn.microsoft.com/library/hh191443.aspx) for more information.</span></span> <span data-ttu-id="eef0d-117">O código a seguir pressupõe que os métodos de programação Assíncrona estão sendo usados.</span><span class="sxs-lookup"><span data-stu-id="eef0d-117">The code below assumes Async programming methods are being used.</span></span>

## <a name="access-tables-in-code"></a><span data-ttu-id="eef0d-118">Acessar tabelas em código</span><span class="sxs-lookup"><span data-stu-id="eef0d-118">Access tables in code</span></span>
<span data-ttu-id="eef0d-119">Para acessar tabelas em projetos do ASP.NET Core, você precisa incluir os itens a seguir para quaisquer arquivos de origem de C# que acessam o armazenamento de tabelas do Azure.</span><span class="sxs-lookup"><span data-stu-id="eef0d-119">To access tables in ASP.NET Core projects, you need to include the following items to any C# source files that access Azure table storage.</span></span>

1. <span data-ttu-id="eef0d-120">Verifique se as declarações de namespace na parte superior do arquivo de C# incluem estas instruções de **uso** .</span><span class="sxs-lookup"><span data-stu-id="eef0d-120">Make sure the namespace declarations at the top of the C# file include these **using** statements.</span></span>
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Table;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. <span data-ttu-id="eef0d-121">Obtenha um objeto **CloudStorageAccount** que represente as informações da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="eef0d-121">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="eef0d-122">Use o seguinte código para obter a sua cadeia de conexão de armazenamento e informações de conta de armazenamento da configuração do serviço do Azure.</span><span class="sxs-lookup"><span data-stu-id="eef0d-122">Use the following code to get the your storage connection string and storage account information from the Azure service configuration.</span></span>
   
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
            CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
   
    <span data-ttu-id="eef0d-123">**OBSERVAÇÃO** - use todos os códigos acima antes do código nos exemplos a seguir.</span><span class="sxs-lookup"><span data-stu-id="eef0d-123">**NOTE** - Use all of the above code in front of the code in the following samples.</span></span>
3. <span data-ttu-id="eef0d-124">Obtenha um objeto **CloudTableClient** para fazer referência aos objetos de tabela em sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="eef0d-124">Get a **CloudTableClient** object to reference the table objects in your storage account.</span></span>  
   
        // Create the table client.
        CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
4. <span data-ttu-id="eef0d-125">Obtenha um objeto de referência **CloudTable** para fazer referência a entidades e a uma tabela específica.</span><span class="sxs-lookup"><span data-stu-id="eef0d-125">Get a **CloudTable** reference object to reference a specific table and entities.</span></span>
   
        // Get a reference to a table named "peopleTable"
        CloudTable table = tableClient.GetTableReference("peopleTable");

## <a name="create-a-table-in-code"></a><span data-ttu-id="eef0d-126">Criar uma tabela em código</span><span class="sxs-lookup"><span data-stu-id="eef0d-126">Create a table in code</span></span>
<span data-ttu-id="eef0d-127">Para criar a tabela do Azure, basta adicionar uma chamada para **CreateIfNotExistsAsync()**.</span><span class="sxs-lookup"><span data-stu-id="eef0d-127">To create the Azure table, just add a call to **CreateIfNotExistsAsync()**.</span></span>

    // Create the CloudTable if it does not exist
    await table.CreateIfNotExistsAsync();

## <a name="add-an-entity-to-a-table"></a><span data-ttu-id="eef0d-128">Adicionar uma entidade a uma tabela</span><span class="sxs-lookup"><span data-stu-id="eef0d-128">Add an entity to a table</span></span>
<span data-ttu-id="eef0d-129">Para adicionar uma entidade a uma tabela, crie uma classe que defina as propriedades da sua entidade.</span><span class="sxs-lookup"><span data-stu-id="eef0d-129">To add an entity to a table you create a class that defines the properties of your entity.</span></span> <span data-ttu-id="eef0d-130">O código a seguir define uma classe chamada **CustomerEntity** que usa o nome do cliente como a chave de linha e o sobrenome como a chave de partição.</span><span class="sxs-lookup"><span data-stu-id="eef0d-130">The following code defines an entity class called **CustomerEntity** that uses the customer's first name as the row key and last name as the partition key.</span></span>

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

<span data-ttu-id="eef0d-131">As operações de tabela que envolvem entidades são executadas usando o objeto **CloudTable** criado anteriormente em “Acessar tabelas no código”.</span><span class="sxs-lookup"><span data-stu-id="eef0d-131">Table operations involving entities are done using the **CloudTable** object you created earlier in "Access tables in code."</span></span> <span data-ttu-id="eef0d-132">O objeto **TableOperation** representa a operação a ser realizada.</span><span class="sxs-lookup"><span data-stu-id="eef0d-132">The **TableOperation** object represents the operation to be done.</span></span> <span data-ttu-id="eef0d-133">O exemplo de código a seguir mostra como criar um objeto **CloudTable** e um objeto **CustomerEntity**.</span><span class="sxs-lookup"><span data-stu-id="eef0d-133">The following code example shows how to create a **CloudTable** object and a **CustomerEntity** object.</span></span> <span data-ttu-id="eef0d-134">Para preparar a operação, um **TableOperation** é criado para inserir a entidade de cliente na tabela.</span><span class="sxs-lookup"><span data-stu-id="eef0d-134">To prepare the operation, a **TableOperation** is created to insert the customer entity into the table.</span></span> <span data-ttu-id="eef0d-135">Finalmente, a operação é executada chamando CloudTable.ExecuteAsync.</span><span class="sxs-lookup"><span data-stu-id="eef0d-135">Finally, the operation is executed by calling CloudTable.ExecuteAsync.</span></span>

    // Create a new customer entity.
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.Email = "Walter@contoso.com";
    customer1.PhoneNumber = "425-555-0101";

    // Create the TableOperation that inserts the customer entity.
    TableOperation insertOperation = TableOperation.Insert(customer1);

    // Execute the insert operation.
    await peopleTable.ExecuteAsync(insertOperation);

## <a name="insert-a-batch-of-entities"></a><span data-ttu-id="eef0d-136">Inserir um lote de entidades</span><span class="sxs-lookup"><span data-stu-id="eef0d-136">Insert a batch of entities</span></span>
<span data-ttu-id="eef0d-137">Você pode inserir várias entidades em uma tabela em uma única operação de gravação.</span><span class="sxs-lookup"><span data-stu-id="eef0d-137">You can insert multiple entities into a table in a single write operation.</span></span> <span data-ttu-id="eef0d-138">O exemplo de código a seguir cria dois objetos de entidade ("Mateus Rodrigues" e "Alberto Rodrigues") e os adiciona a um objeto **TableBatchOperation** usando o método **Insert** e depois inicia a operação chamando CloudTable.ExecuteBatchAsync.</span><span class="sxs-lookup"><span data-stu-id="eef0d-138">The following code example creates two entity objects ("Jeff Smith" and "Ben Smith"), adds them to a **TableBatchOperation** object using the **Insert** method, and then starts the operation by calling CloudTable.ExecuteBatchAsync.</span></span>

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
    await peopleTable.ExecuteBatchAsync(batchOperation);

## <a name="get-all-of-the-entities-in-a-partition"></a><span data-ttu-id="eef0d-139">Obter todas as entidades em uma partição</span><span class="sxs-lookup"><span data-stu-id="eef0d-139">Get all of the entities in a partition</span></span>
<span data-ttu-id="eef0d-140">Para consultar uma tabela de todas as entidades em uma partição, use um objeto **TableQuery** .</span><span class="sxs-lookup"><span data-stu-id="eef0d-140">To query a table for all of the entities in a partition, use a **TableQuery** object.</span></span> <span data-ttu-id="eef0d-141">O exemplo de código a seguir especifica um filtro para entidades onde 'Smith' é a chave da partição.</span><span class="sxs-lookup"><span data-stu-id="eef0d-141">The following code example specifies a filter for entities where 'Smith' is the partition key.</span></span> <span data-ttu-id="eef0d-142">Esse exemplo imprime os campos de cada entidade nos resultados da consulta no console.</span><span class="sxs-lookup"><span data-stu-id="eef0d-142">This example prints the fields of each entity in the query results to the console.</span></span>

    // Construct the query operation for all customer entities where PartitionKey="Smith".
    TableQuery<CustomerEntity> query = new TableQuery<CustomerEntity>().Where(TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"));

    // Print the fields for each customer.
    TableContinuationToken token = null;
    do
    {
        TableQuerySegment<CustomerEntity> resultSegment = await peopleTable.ExecuteQuerySegmentedAsync(query, token);
        token = resultSegment.ContinuationToken;

        foreach (CustomerEntity entity in resultSegment.Results)
        {
            Console.WriteLine("{0}, {1}\t{2}\t{3}", entity.PartitionKey, entity.RowKey,
            entity.Email, entity.PhoneNumber);
        }
    } while (token != null);

## <a name="get-a-single-entity"></a><span data-ttu-id="eef0d-143">Obter uma única entidade</span><span class="sxs-lookup"><span data-stu-id="eef0d-143">Get a single entity</span></span>
<span data-ttu-id="eef0d-144">Você pode escrever uma consulta para obter uma entidade única e específica.</span><span class="sxs-lookup"><span data-stu-id="eef0d-144">You can write a query to get a single, specific entity.</span></span> <span data-ttu-id="eef0d-145">O código a seguir usa um objeto **TableOperation** para especificar o cliente chamado 'Ben Smith'.</span><span class="sxs-lookup"><span data-stu-id="eef0d-145">The following code uses a **TableOperation** object to specify a customer named 'Ben Smith'.</span></span> <span data-ttu-id="eef0d-146">Esse método retorna uma única entidade, em vez de uma coleção, e o valor retornado no **TableResult.Result** é um objeto **CustomerEntity**.</span><span class="sxs-lookup"><span data-stu-id="eef0d-146">This method returns just one entity, rather than a collection, and the returned value in **TableResult.Result** is a **CustomerEntity** object.</span></span> <span data-ttu-id="eef0d-147">Especificar chaves de partição e de linha em uma consulta é a maneira mais rápida de recuperar uma única entidade de serviço **Table** .</span><span class="sxs-lookup"><span data-stu-id="eef0d-147">Specifying both partition and row keys in a query is the fastest way to retrieve a single entity from the **Table** service.</span></span>

    // Create a retrieve operation that takes a customer entity.
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

    // Execute the retrieve operation.
    TableResult retrievedResult = await peopleTable.ExecuteAsync(retrieveOperation);

    // Print the phone number of the result.
    if (retrievedResult.Result != null)
       Console.WriteLine(((CustomerEntity)retrievedResult.Result).PhoneNumber);
    else
       Console.WriteLine("The phone number could not be retrieved.");

## <a name="delete-an-entity"></a><span data-ttu-id="eef0d-148">Excluir uma entidade</span><span class="sxs-lookup"><span data-stu-id="eef0d-148">Delete an entity</span></span>
<span data-ttu-id="eef0d-149">Você poderá excluir uma entidade facilmente depois de encontrá-la.</span><span class="sxs-lookup"><span data-stu-id="eef0d-149">You can delete an entity after you find it.</span></span> <span data-ttu-id="eef0d-150">O código a seguir busca uma entidade de cliente chamada "Ben Smith", excluindo-a caso a encontre.</span><span class="sxs-lookup"><span data-stu-id="eef0d-150">The following code looks for a customer entity named "Ben Smith" and if it finds it, it deletes it.</span></span>

    // Create a retrieve operation that expects a customer entity.
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

    // Execute the operation.
    TableResult retrievedResult = peopleTable.Execute(retrieveOperation);

    // Assign the result to a CustomerEntity object.
    CustomerEntity deleteEntity = (CustomerEntity)retrievedResult.Result;

    // Create the Delete TableOperation and then execute it.
    if (deleteEntity != null)
    {
       TableOperation deleteOperation = TableOperation.Delete(deleteEntity);

       // Execute the operation.
       await peopleTable.ExecuteAsync(deleteOperation);

       Console.WriteLine("Entity deleted.");
    }

    else
       Console.WriteLine("Couldn't delete the entity.");

## <a name="next-steps"></a><span data-ttu-id="eef0d-151">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="eef0d-151">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-tables-next-steps](../../includes/vs-storage-dotnet-tables-next-steps.md)]

