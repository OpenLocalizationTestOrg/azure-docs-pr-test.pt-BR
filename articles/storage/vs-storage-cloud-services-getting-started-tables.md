---
title: "Introdução ao armazenamento de tabelas e aos serviços conectados do Visual Studio (serviços de nuvem) | Microsoft Docs"
description: "Como começar a usar o armazenamento de Tabela do Azure em um projeto de serviço de nuvem no Visual Studio após a conexão a uma conta de armazenamento usando os serviços conectados do Visual Studio"
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: a3a11ed8-ba7f-4193-912b-e555f5b72184
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: 3208ddb1a1246a5ff25d272bfc7d8ba842348a36
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-azure-table-storage-and-visual-studio-connected-services-cloud-services-projects"></a><span data-ttu-id="d67b1-103">Introdução ao armazenamento de tabela do Azure e aos serviços conectados do Visual Studio (projetos de serviços de nuvem)</span><span class="sxs-lookup"><span data-stu-id="d67b1-103">Getting started with Azure table storage and Visual Studio connected services (cloud services projects)</span></span>
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a><span data-ttu-id="d67b1-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="d67b1-104">Overview</span></span>
<span data-ttu-id="d67b1-105">Este artigo descreve como começar a usar o armazenamento de tabelas do Azure no Visual Studio depois de ter criado ou referenciado uma conta de armazenamento do Azure em um projeto de serviços de nuvem usando a caixa de diálogo **Adicionar Serviços Conectados** do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d67b1-105">This article describes how to get started using Azure table storage in Visual Studio after you have created or referenced an Azure storage account in a cloud services project by using the Visual Studio **Add Connected Services** dialog.</span></span> <span data-ttu-id="d67b1-106">A operação **Adicionar Serviços Conectados** instala os pacotes NuGet apropriados para acessar o armazenamento do Azure no seu projeto e adiciona a cadeia de conexão para a conta de armazenamento aos arquivos de configuração do projeto.</span><span class="sxs-lookup"><span data-stu-id="d67b1-106">The **Add Connected Services** operation installs the appropriate NuGet packages to access Azure storage in your project and adds the connection string for the storage account to your project configuration files.</span></span>

<span data-ttu-id="d67b1-107">O serviço de armazenamento de Tabela do Azure armazena grandes quantidades de dados estruturados.</span><span class="sxs-lookup"><span data-stu-id="d67b1-107">The Azure Table storage service enables you to store large amounts of structured data.</span></span> <span data-ttu-id="d67b1-108">O serviço é um repositório de dados NoSQL que aceita chamadas autenticadas de dentro e de fora da nuvem do Azure.</span><span class="sxs-lookup"><span data-stu-id="d67b1-108">The service is a NoSQL datastore that accepts authenticated calls from inside and outside the Azure cloud.</span></span> <span data-ttu-id="d67b1-109">As tabelas do Azure são ideais para armazenar dados estruturados não relacionais.</span><span class="sxs-lookup"><span data-stu-id="d67b1-109">Azure tables are ideal for storing structured, non-relational data.</span></span>

<span data-ttu-id="d67b1-110">Para começar, primeiramente, você precisa criar uma tabela em sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="d67b1-110">To get started, you first need to create a table in your storage account.</span></span> <span data-ttu-id="d67b1-111">Mostraremos como criar uma tabela do Azure com código e também como realizar operações básicas de tabela e entidade, como adicionar, modificar, ler e ler entidades de tabela.</span><span class="sxs-lookup"><span data-stu-id="d67b1-111">We'll show you how to create an Azure table in code, and also how to perform basic table and entity operations, such as adding, modifying, reading and reading table entities.</span></span> <span data-ttu-id="d67b1-112">Os exemplos são escritos em código C\# e usam a [Biblioteca de cliente do Armazenamento do Microsoft Azure para .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span><span class="sxs-lookup"><span data-stu-id="d67b1-112">The samples are written in C\# code and use the [Microsoft Azure Storage client library for .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span></span>

<span data-ttu-id="d67b1-113">**OBSERVAÇÃO:** algumas APIs que executam chamadas para o armazenamento do Azure são assíncronas.</span><span class="sxs-lookup"><span data-stu-id="d67b1-113">**NOTE:** Some of the APIs that perform calls out to Azure storage are asynchronous.</span></span> <span data-ttu-id="d67b1-114">Confira [Programação assíncrona com Async e Await](http://msdn.microsoft.com/library/hh191443.aspx) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="d67b1-114">See [Asynchronous programming with Async and Await](http://msdn.microsoft.com/library/hh191443.aspx) for more information.</span></span> <span data-ttu-id="d67b1-115">O código a seguir pressupõe que os métodos de programação assíncrona estão sendo usados.</span><span class="sxs-lookup"><span data-stu-id="d67b1-115">The code below assumes async programming methods are being used.</span></span>

* <span data-ttu-id="d67b1-116">Consulte [Introdução ao Armazenamento de Tabelas do Azure usando .NET](storage-dotnet-how-to-use-tables.md) para obter mais informações sobre como manipular tabelas com programação.</span><span class="sxs-lookup"><span data-stu-id="d67b1-116">See [Get started with Azure Table storage using .NET](storage-dotnet-how-to-use-tables.md) for more information on programmatically manipulating tables.</span></span>
* <span data-ttu-id="d67b1-117">Consulte a [Documentação de armazenamento](https://azure.microsoft.com/documentation/services/storage/) para obter informações gerais sobre o armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="d67b1-117">See [Storage documentation](https://azure.microsoft.com/documentation/services/storage/) for general information about Azure Storage.</span></span>
* <span data-ttu-id="d67b1-118">Consulte a [documentação de serviços de nuvem](https://azure.microsoft.com/documentation/services/cloud-services/) para obter informações gerais sobre os serviços de nuvem do Azure.</span><span class="sxs-lookup"><span data-stu-id="d67b1-118">See [Cloud Services documentation](https://azure.microsoft.com/documentation/services/cloud-services/) for general information about Azure cloud services.</span></span>
* <span data-ttu-id="d67b1-119">Consulte [ASP.NET](http://www.asp.net) para obter mais informações sobre como programar aplicativos ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="d67b1-119">See [ASP.NET](http://www.asp.net) for more information about programming ASP.NET applications.</span></span>

## <a name="access-tables-in-code"></a><span data-ttu-id="d67b1-120">Acessar tabelas em código</span><span class="sxs-lookup"><span data-stu-id="d67b1-120">Access tables in code</span></span>
<span data-ttu-id="d67b1-121">Para acessar tabelas em projetos de serviço de nuvem, você precisa incluir os itens a seguir para quaisquer arquivos de origem de C# que acessam o armazenamento de tabela do Azure.</span><span class="sxs-lookup"><span data-stu-id="d67b1-121">To access tables in cloud service projects, you need to include the following items to any C# source files that access Azure table storage.</span></span>

1. <span data-ttu-id="d67b1-122">Verifique se as declarações de namespace na parte superior do arquivo de C# incluem estas instruções de **uso** .</span><span class="sxs-lookup"><span data-stu-id="d67b1-122">Make sure the namespace declarations at the top of the C# file include these **using** statements.</span></span>
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Table;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. <span data-ttu-id="d67b1-123">Obtenha um objeto **CloudStorageAccount** que represente as informações da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="d67b1-123">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="d67b1-124">Use o seguinte código para obter a cadeia de conexão de armazenamento e informações de conta de armazenamento da configuração do serviço do Azure.</span><span class="sxs-lookup"><span data-stu-id="d67b1-124">Use the following code to get the storage connection string and storage account information from the Azure service configuration.</span></span>
   
         CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
           CloudConfigurationManager.GetSetting("<storage account name>
         _AzureStorageConnectionString"));
   > [!NOTE]
   > <span data-ttu-id="d67b1-125">Use todo o código acima antes do código dos exemplos a seguir.</span><span class="sxs-lookup"><span data-stu-id="d67b1-125">Use all of the above code in front of the code in the following samples.</span></span>
   > 
   > 
3. <span data-ttu-id="d67b1-126">Obtenha um objeto **CloudTableClient** para fazer referência aos objetos de tabela em sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="d67b1-126">Get a **CloudTableClient** object to reference the table objects in your storage account.</span></span>
   
         // Create the table client.
         CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
4. <span data-ttu-id="d67b1-127">Obtenha um objeto de referência **CloudTable** para fazer referência a entidades e a uma tabela específica.</span><span class="sxs-lookup"><span data-stu-id="d67b1-127">Get a **CloudTable** reference object to reference a specific table and entities.</span></span>
   
        // Get a reference to a table named "peopleTable".
        CloudTable peopleTable = tableClient.GetTableReference("peopleTable");

## <a name="create-a-table-in-code"></a><span data-ttu-id="d67b1-128">Criar uma tabela em código</span><span class="sxs-lookup"><span data-stu-id="d67b1-128">Create a table in code</span></span>
<span data-ttu-id="d67b1-129">Para criar a tabela do Azure, basta adicionar uma chamada para **CreateIfNotExistsAsync** após obter um objeto **CloudTable**, como descrito na seção "Acessar tabelas em código".</span><span class="sxs-lookup"><span data-stu-id="d67b1-129">To create the Azure table, just add a call to **CreateIfNotExistsAsync** to the after you get a **CloudTable** object as described in the "Access tables in code" section.</span></span>

    // Create the CloudTable if it does not exist.
    await peopleTable.CreateIfNotExistsAsync();

## <a name="add-an-entity-to-a-table"></a><span data-ttu-id="d67b1-130">Adicionar uma entidade a uma tabela</span><span class="sxs-lookup"><span data-stu-id="d67b1-130">Add an entity to a table</span></span>
<span data-ttu-id="d67b1-131">Para adicionar uma entidade a uma tabela, crie uma classe que defina as propriedades da sua entidade.</span><span class="sxs-lookup"><span data-stu-id="d67b1-131">To add an entity to a table, create a class that defines the properties of your entity.</span></span> <span data-ttu-id="d67b1-132">O código a seguir define uma classe de entidade chamada **CustomerEntity** que usa o nome do cliente como a chave de linha e o sobrenome como a chave de partição.</span><span class="sxs-lookup"><span data-stu-id="d67b1-132">The following code defines an entity class called **CustomerEntity** that uses the customer's first name as the row key and the last name as the partition key.</span></span>

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

<span data-ttu-id="d67b1-133">As operações de tabela que envolvem entidades são executadas usando o objeto **CloudTable** , criado anteriormente em "Acessar tabelas no código".</span><span class="sxs-lookup"><span data-stu-id="d67b1-133">Table operations involving entities are done using the **CloudTable** object that you created earlier in "Access tables in code."</span></span> <span data-ttu-id="d67b1-134">O objeto **TableOperation** representa a operação a ser realizada.</span><span class="sxs-lookup"><span data-stu-id="d67b1-134">The **TableOperation** object represents the operation to be done.</span></span> <span data-ttu-id="d67b1-135">O exemplo de código a seguir mostra como criar um objeto **CloudTable** e um objeto **CustomerEntity**.</span><span class="sxs-lookup"><span data-stu-id="d67b1-135">The following code example shows how to create a **CloudTable** object and a **CustomerEntity** object.</span></span> <span data-ttu-id="d67b1-136">Para preparar a operação, um **TableOperation** é criado para inserir a entidade de cliente na tabela.</span><span class="sxs-lookup"><span data-stu-id="d67b1-136">To prepare the operation, a **TableOperation** is created to insert the customer entity into the table.</span></span> <span data-ttu-id="d67b1-137">Finalmente, a operação é executada chamando **CloudTable.ExecuteAsync**.</span><span class="sxs-lookup"><span data-stu-id="d67b1-137">Finally, the operation is executed by calling **CloudTable.ExecuteAsync**.</span></span>

    // Create a new customer entity.
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.Email = "Walter@contoso.com";
    customer1.PhoneNumber = "425-555-0101";

    // Create the TableOperation that inserts the customer entity.
    TableOperation insertOperation = TableOperation.Insert(customer1);

    // Execute the insert operation.
    await peopleTable.ExecuteAsync(insertOperation);


## <a name="insert-a-batch-of-entities"></a><span data-ttu-id="d67b1-138">Inserir um lote de entidades</span><span class="sxs-lookup"><span data-stu-id="d67b1-138">Insert a batch of entities</span></span>
<span data-ttu-id="d67b1-139">Você pode inserir várias entidades em uma tabela em uma única operação de gravação.</span><span class="sxs-lookup"><span data-stu-id="d67b1-139">You can insert multiple entities into a table in a single write operation.</span></span> <span data-ttu-id="d67b1-140">O exemplo de código a seguir cria dois objetos de entidade ("Mateus Rodrigues" e "Alberto Rodrigues") e os adiciona a um objeto **TableBatchOperation** usando o método Insert e depois inicia a operação chamando **CloudTable.ExecuteBatchAsync**.</span><span class="sxs-lookup"><span data-stu-id="d67b1-140">The following code example creates two entity objects ("Jeff Smith" and "Ben Smith"), adds them to a **TableBatchOperation** object using the Insert method, and then starts the operation by calling **CloudTable.ExecuteBatchAsync**.</span></span>

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

## <a name="get-all-of-the-entities-in-a-partition"></a><span data-ttu-id="d67b1-141">Obter todas as entidades em uma partição</span><span class="sxs-lookup"><span data-stu-id="d67b1-141">Get all of the entities in a partition</span></span>
<span data-ttu-id="d67b1-142">Para consultar uma tabela de todas as entidades em uma partição, use um objeto **TableQuery** .</span><span class="sxs-lookup"><span data-stu-id="d67b1-142">To query a table for all of the entities in a partition, use a **TableQuery** object.</span></span> <span data-ttu-id="d67b1-143">O exemplo de código a seguir especifica um filtro para entidades onde 'Smith' é a chave da partição.</span><span class="sxs-lookup"><span data-stu-id="d67b1-143">The following code example specifies a filter for entities where 'Smith' is the partition key.</span></span> <span data-ttu-id="d67b1-144">Esse exemplo imprime os campos de cada entidade nos resultados da consulta no console.</span><span class="sxs-lookup"><span data-stu-id="d67b1-144">This example prints the fields of each entity in the query results to the console.</span></span>

    // Construct the query operation for all customer entities where PartitionKey="Smith".
    TableQuery<CustomerEntity> query = new TableQuery<CustomerEntity>()
        .Where(TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"));

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

    return View();


## <a name="get-a-single-entity"></a><span data-ttu-id="d67b1-145">Obter uma única entidade</span><span class="sxs-lookup"><span data-stu-id="d67b1-145">Get a single entity</span></span>
<span data-ttu-id="d67b1-146">Você pode escrever uma consulta para obter uma entidade única e específica.</span><span class="sxs-lookup"><span data-stu-id="d67b1-146">You can write a query to get a single, specific entity.</span></span> <span data-ttu-id="d67b1-147">O código a seguir usa um objeto **TableOperation** para especificar o cliente chamado 'Ben Smith'.</span><span class="sxs-lookup"><span data-stu-id="d67b1-147">The following code uses a **TableOperation** object to specify a customer named 'Ben Smith'.</span></span> <span data-ttu-id="d67b1-148">Esse método retorna uma única entidade, em vez de uma coleção, e o valor retornado no **TableResult.Result** é um objeto **CustomerEntity**.</span><span class="sxs-lookup"><span data-stu-id="d67b1-148">This method returns just one entity, rather than a collection, and the returned value in **TableResult.Result** is a **CustomerEntity** object.</span></span> <span data-ttu-id="d67b1-149">Especificar chaves de partição e de linha em uma consulta é a maneira mais rápida de recuperar uma única entidade de serviço **Table** .</span><span class="sxs-lookup"><span data-stu-id="d67b1-149">Specifying both partition and row keys in a query is the fastest way to retrieve a single entity from the **Table** service.</span></span>

    // Create a retrieve operation that takes a customer entity.
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

    // Execute the retrieve operation.
    TableResult retrievedResult = await peopleTable.ExecuteAsync(retrieveOperation);

    // Print the phone number of the result.
    if (retrievedResult.Result != null)
       Console.WriteLine(((CustomerEntity)retrievedResult.Result).PhoneNumber);
    else
       Console.WriteLine("The phone number could not be retrieved.");

## <a name="delete-an-entity"></a><span data-ttu-id="d67b1-150">Excluir uma entidade</span><span class="sxs-lookup"><span data-stu-id="d67b1-150">Delete an entity</span></span>
<span data-ttu-id="d67b1-151">Você poderá excluir uma entidade facilmente depois de encontrá-la.</span><span class="sxs-lookup"><span data-stu-id="d67b1-151">You can delete an entity after you find it.</span></span> <span data-ttu-id="d67b1-152">O código a seguir busca uma entidade customer chamada "Mateus Rodrigues", excluindo-a caso a encontre.</span><span class="sxs-lookup"><span data-stu-id="d67b1-152">The following code looks for a customer entity named "Ben Smith", and if it finds it, it deletes it.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="d67b1-153">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d67b1-153">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-tables-next-steps](../../includes/vs-storage-dotnet-tables-next-steps.md)]

