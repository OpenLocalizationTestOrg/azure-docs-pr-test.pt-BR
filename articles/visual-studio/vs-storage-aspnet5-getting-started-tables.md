---
title: "aaaHow tooget de Introdução ao armazenamento de tabela e o Visual Studio serviços conectados (ASP.NET Core) | Microsoft Docs"
description: "Como tooget iniciada com o armazenamento de tabela do Azure em um projeto do ASP.NET Core no Visual Studio depois de conectar-se a conta de armazenamento tooa usando o Visual Studio conectada a serviços"
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: c3c451d1-71ff-4222-a348-c41c98a02b85
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: e3eb3f3e65456108dd3cde7e3e470f98ba456e35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooget-started-with-azure-table-storage-and-visual-studio-connected-services"></a><span data-ttu-id="ce83a-103">Como tooget iniciada com o armazenamento de tabela do Azure e o Visual Studio serviços conectados</span><span class="sxs-lookup"><span data-stu-id="ce83a-103">How tooget started with Azure Table storage and Visual Studio connected services</span></span>
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a><span data-ttu-id="ce83a-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="ce83a-104">Overview</span></span>
<span data-ttu-id="ce83a-105">Este artigo descreve como obter iniciado usando a tabela do Azure Olá de armazenamento no Visual Studio depois que você criou ou referenciados de uma conta de armazenamento do Azure em um projeto do ASP.NET Core usando Visual Studio **adicionar serviços conectados** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ce83a-105">This article describes how get started using Azure Table storage in Visual Studio after you have created or referenced an Azure storage account in an ASP.NET Core project by using hello Visual Studio **Add Connected Services** dialog.</span></span>

<span data-ttu-id="ce83a-106">saudação de serviço de armazenamento de tabela do Azure permite que você toostore grandes quantidades de dados estruturados.</span><span class="sxs-lookup"><span data-stu-id="ce83a-106">hello Azure Table storage service enables you toostore large amounts of structured data.</span></span> <span data-ttu-id="ce83a-107">serviço de saudação é um repositório de dados NoSQL que aceita chamadas autenticadas de dentro e fora hello nuvem do Azure.</span><span class="sxs-lookup"><span data-stu-id="ce83a-107">hello service is a NoSQL data store that accepts authenticated calls from inside and outside hello Azure cloud.</span></span> <span data-ttu-id="ce83a-108">As tabelas do Azure são ideais para armazenar dados estruturados não relacionais.</span><span class="sxs-lookup"><span data-stu-id="ce83a-108">Azure tables are ideal for storing structured, non-relational data.</span></span>

<span data-ttu-id="ce83a-109">Olá **adicionar serviços conectados** operação instala Olá apropriado NuGet pacotes tooaccess armazenamento do Azure em seu projeto e adiciona a cadeia de caracteres de conexão Olá para hello conta de armazenamento tooyour arquivos de configuração do projeto.</span><span class="sxs-lookup"><span data-stu-id="ce83a-109">hello **Add Connected Services** operation installs hello appropriate NuGet packages tooaccess Azure storage in your project and adds hello connection string for hello storage account tooyour project configuration files.</span></span>

<span data-ttu-id="ce83a-110">Para obter mais informações sobre como usar o Armazenamento de Tabelas do Azure, consulte [Introdução ao armazenamento de Tabelas do Azure usando o .NET](../storage/storage-dotnet-how-to-use-tables.md).</span><span class="sxs-lookup"><span data-stu-id="ce83a-110">For more general information about using Azure Table storage, see [Get started with Azure Table storage using .NET](../storage/storage-dotnet-how-to-use-tables.md).</span></span>

<span data-ttu-id="ce83a-111">tooget iniciado, você primeiro precisa toocreate uma tabela em sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="ce83a-111">tooget started, you first need toocreate a table in your storage account.</span></span> <span data-ttu-id="ce83a-112">Mostraremos como toocreate um Azure tabela no código.</span><span class="sxs-lookup"><span data-stu-id="ce83a-112">We'll show you how toocreate an Azure table in code.</span></span> <span data-ttu-id="ce83a-113">Também mostraremos como tabela básica tooperform e operações da entidade, como adicionar, modificar, ler e ler da tabela de entidades.</span><span class="sxs-lookup"><span data-stu-id="ce83a-113">We'll also show you how tooperform basic table and entity operations, such as adding, modifying, reading and reading table entities.</span></span> <span data-ttu-id="ce83a-114">exemplos de saudação são escritos em C\# de código e use Olá biblioteca de cliente de armazenamento do Azure para .NET.</span><span class="sxs-lookup"><span data-stu-id="ce83a-114">hello samples are written in C\# code and use hello Azure Storage Client Library for .NET.</span></span>

<span data-ttu-id="ce83a-115">**Observação** -algumas Olá APIs que executam chamadas tooAzure armazenamento no núcleo do ASP.NET são assíncronas.</span><span class="sxs-lookup"><span data-stu-id="ce83a-115">**NOTE** - Some of hello APIs that perform calls out tooAzure storage in ASP.NET Core are asynchronous.</span></span> <span data-ttu-id="ce83a-116">Confira [Programação assíncrona com Async e Await](http://msdn.microsoft.com/library/hh191443.aspx) para saber mais.</span><span class="sxs-lookup"><span data-stu-id="ce83a-116">See [Asynchronous Programming with Async and Await](http://msdn.microsoft.com/library/hh191443.aspx) for more information.</span></span> <span data-ttu-id="ce83a-117">código de saudação abaixo supõe que os métodos de programação assíncrona estão sendo usados.</span><span class="sxs-lookup"><span data-stu-id="ce83a-117">hello code below assumes Async programming methods are being used.</span></span>

## <a name="access-tables-in-code"></a><span data-ttu-id="ce83a-118">Acessar tabelas em código</span><span class="sxs-lookup"><span data-stu-id="ce83a-118">Access tables in code</span></span>
<span data-ttu-id="ce83a-119">tooaccess tabelas em projetos do ASP.NET Core, é necessário tooinclude Olá seguintes arquivos de origem do itens tooany c# que acessam o armazenamento de tabela do Azure.</span><span class="sxs-lookup"><span data-stu-id="ce83a-119">tooaccess tables in ASP.NET Core projects, you need tooinclude hello following items tooany C# source files that access Azure table storage.</span></span>

1. <span data-ttu-id="ce83a-120">Certifique-se de declarações de namespace Olá na parte superior de saudação do arquivo hello c# incluem-las **usando** instruções.</span><span class="sxs-lookup"><span data-stu-id="ce83a-120">Make sure hello namespace declarations at hello top of hello C# file include these **using** statements.</span></span>
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Table;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. <span data-ttu-id="ce83a-121">Obtenha um objeto **CloudStorageAccount** que represente as informações da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="ce83a-121">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="ce83a-122">Saudação de uso tooget de código a seguir Olá sua cadeia de caracteres de conexão de armazenamento e as informações de conta de armazenamento da configuração de serviço do Azure de saudação.</span><span class="sxs-lookup"><span data-stu-id="ce83a-122">Use hello following code tooget hello your storage connection string and storage account information from hello Azure service configuration.</span></span>
   
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
            CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
   
    <span data-ttu-id="ce83a-123">**Observação** -Use todos Olá acima código código Olá Olá exemplos a seguir.</span><span class="sxs-lookup"><span data-stu-id="ce83a-123">**NOTE** - Use all of hello above code in front of hello code in hello following samples.</span></span>
3. <span data-ttu-id="ce83a-124">Obter um **CloudTableClient** tooreference Olá tabela objetos na conta de armazenamento de objeto.</span><span class="sxs-lookup"><span data-stu-id="ce83a-124">Get a **CloudTableClient** object tooreference hello table objects in your storage account.</span></span>  
   
        // Create hello table client.
        CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
4. <span data-ttu-id="ce83a-125">Obter um **CloudTable** fazer referência a entidades e objeto tooreference uma tabela específica.</span><span class="sxs-lookup"><span data-stu-id="ce83a-125">Get a **CloudTable** reference object tooreference a specific table and entities.</span></span>
   
        // Get a reference tooa table named "peopleTable"
        CloudTable table = tableClient.GetTableReference("peopleTable");

## <a name="create-a-table-in-code"></a><span data-ttu-id="ce83a-126">Criar uma tabela em código</span><span class="sxs-lookup"><span data-stu-id="ce83a-126">Create a table in code</span></span>
<span data-ttu-id="ce83a-127">Olá toocreate tabela do Azure, basta adicionar uma chamada muito**CreateIfNotExistsAsync()**.</span><span class="sxs-lookup"><span data-stu-id="ce83a-127">toocreate hello Azure table, just add a call too**CreateIfNotExistsAsync()**.</span></span>

    // Create hello CloudTable if it does not exist
    await table.CreateIfNotExistsAsync();

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="ce83a-128">Adicionar uma tabela de entidade tooa</span><span class="sxs-lookup"><span data-stu-id="ce83a-128">Add an entity tooa table</span></span>
<span data-ttu-id="ce83a-129">tooadd uma tabela de tooa de entidade que você criar uma classe que define as propriedades de saudação da entidade.</span><span class="sxs-lookup"><span data-stu-id="ce83a-129">tooadd an entity tooa table you create a class that defines hello properties of your entity.</span></span> <span data-ttu-id="ce83a-130">Olá, código a seguir define uma classe de entidade chamada **CustomerEntity** que usa Olá nome do cliente como chave de linha de saudação e último nome como chave de partição hello.</span><span class="sxs-lookup"><span data-stu-id="ce83a-130">hello following code defines an entity class called **CustomerEntity** that uses hello customer's first name as hello row key and last name as hello partition key.</span></span>

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

<span data-ttu-id="ce83a-131">Operações de tabela que envolvem entidades são feitas usando Olá **CloudTable** objeto que você criou anteriormente no "Tabelas de acesso no código".</span><span class="sxs-lookup"><span data-stu-id="ce83a-131">Table operations involving entities are done using hello **CloudTable** object you created earlier in "Access tables in code."</span></span> <span data-ttu-id="ce83a-132">Olá **TableOperation** objeto representa Olá operação toobe feito.</span><span class="sxs-lookup"><span data-stu-id="ce83a-132">hello **TableOperation** object represents hello operation toobe done.</span></span> <span data-ttu-id="ce83a-133">Olá mostra exemplo de código a seguir como toocreate uma **CloudTable** objeto e um **CustomerEntity** objeto.</span><span class="sxs-lookup"><span data-stu-id="ce83a-133">hello following code example shows how toocreate a **CloudTable** object and a **CustomerEntity** object.</span></span> <span data-ttu-id="ce83a-134">operação de saudação tooprepare, uma **TableOperation** é criado entidade do cliente Olá tooinsert na tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="ce83a-134">tooprepare hello operation, a **TableOperation** is created tooinsert hello customer entity into hello table.</span></span> <span data-ttu-id="ce83a-135">Por fim, a operação de saudação é executada chamando CloudTable.ExecuteAsync.</span><span class="sxs-lookup"><span data-stu-id="ce83a-135">Finally, hello operation is executed by calling CloudTable.ExecuteAsync.</span></span>

    // Create a new customer entity.
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.Email = "Walter@contoso.com";
    customer1.PhoneNumber = "425-555-0101";

    // Create hello TableOperation that inserts hello customer entity.
    TableOperation insertOperation = TableOperation.Insert(customer1);

    // Execute hello insert operation.
    await peopleTable.ExecuteAsync(insertOperation);

## <a name="insert-a-batch-of-entities"></a><span data-ttu-id="ce83a-136">Inserir um lote de entidades</span><span class="sxs-lookup"><span data-stu-id="ce83a-136">Insert a batch of entities</span></span>
<span data-ttu-id="ce83a-137">Você pode inserir várias entidades em uma tabela em uma única operação de gravação.</span><span class="sxs-lookup"><span data-stu-id="ce83a-137">You can insert multiple entities into a table in a single write operation.</span></span> <span data-ttu-id="ce83a-138">Olá exemplo de código a seguir cria dois objetos de entidade ("Jeff Smith" e "Ben Smith"), adiciona tooa **TableBatchOperation** objeto usando Olá **inserir** método e, em seguida, inicia Olá operação por chamando CloudTable.ExecuteBatchAsync.</span><span class="sxs-lookup"><span data-stu-id="ce83a-138">hello following code example creates two entity objects ("Jeff Smith" and "Ben Smith"), adds them tooa **TableBatchOperation** object using hello **Insert** method, and then starts hello operation by calling CloudTable.ExecuteBatchAsync.</span></span>

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
    await peopleTable.ExecuteBatchAsync(batchOperation);

## <a name="get-all-of-hello-entities-in-a-partition"></a><span data-ttu-id="ce83a-139">Obter todas as entidades de saudação em uma partição</span><span class="sxs-lookup"><span data-stu-id="ce83a-139">Get all of hello entities in a partition</span></span>
<span data-ttu-id="ce83a-140">tooquery uma tabela para todas as entidades de saudação em uma partição, use um **TableQuery** objeto.</span><span class="sxs-lookup"><span data-stu-id="ce83a-140">tooquery a table for all of hello entities in a partition, use a **TableQuery** object.</span></span> <span data-ttu-id="ce83a-141">Olá, exemplo de código a seguir especifica um filtro para entidades onde 'Smith' é a chave de partição hello.</span><span class="sxs-lookup"><span data-stu-id="ce83a-141">hello following code example specifies a filter for entities where 'Smith' is hello partition key.</span></span> <span data-ttu-id="ce83a-142">Este exemplo imprime campos de saudação de cada entidade no console de toohello de resultados de consulta de saudação.</span><span class="sxs-lookup"><span data-stu-id="ce83a-142">This example prints hello fields of each entity in hello query results toohello console.</span></span>

    // Construct hello query operation for all customer entities where PartitionKey="Smith".
    TableQuery<CustomerEntity> query = new TableQuery<CustomerEntity>().Where(TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"));

    // Print hello fields for each customer.
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

## <a name="get-a-single-entity"></a><span data-ttu-id="ce83a-143">Obter uma única entidade</span><span class="sxs-lookup"><span data-stu-id="ce83a-143">Get a single entity</span></span>
<span data-ttu-id="ce83a-144">Você pode escrever uma consulta tooget uma entidade única e específica.</span><span class="sxs-lookup"><span data-stu-id="ce83a-144">You can write a query tooget a single, specific entity.</span></span> <span data-ttu-id="ce83a-145">código a seguir Olá usa um **TableOperation** toospecify um cliente chamado 'Ben Smith' do objeto.</span><span class="sxs-lookup"><span data-stu-id="ce83a-145">hello following code uses a **TableOperation** object toospecify a customer named 'Ben Smith'.</span></span> <span data-ttu-id="ce83a-146">Esse método retorna uma única entidade, em vez de uma coleção e Olá retornou o valor em **TableResult.Result** é um **CustomerEntity** objeto.</span><span class="sxs-lookup"><span data-stu-id="ce83a-146">This method returns just one entity, rather than a collection, and hello returned value in **TableResult.Result** is a **CustomerEntity** object.</span></span> <span data-ttu-id="ce83a-147">Especificar chaves de partição e de linha em uma consulta é tooretrieve de maneira mais rápida de saudação uma única entidade de saudação **tabela** serviço.</span><span class="sxs-lookup"><span data-stu-id="ce83a-147">Specifying both partition and row keys in a query is hello fastest way tooretrieve a single entity from hello **Table** service.</span></span>

    // Create a retrieve operation that takes a customer entity.
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

    // Execute hello retrieve operation.
    TableResult retrievedResult = await peopleTable.ExecuteAsync(retrieveOperation);

    // Print hello phone number of hello result.
    if (retrievedResult.Result != null)
       Console.WriteLine(((CustomerEntity)retrievedResult.Result).PhoneNumber);
    else
       Console.WriteLine("hello phone number could not be retrieved.");

## <a name="delete-an-entity"></a><span data-ttu-id="ce83a-148">Excluir uma entidade</span><span class="sxs-lookup"><span data-stu-id="ce83a-148">Delete an entity</span></span>
<span data-ttu-id="ce83a-149">Você poderá excluir uma entidade facilmente depois de encontrá-la.</span><span class="sxs-lookup"><span data-stu-id="ce83a-149">You can delete an entity after you find it.</span></span> <span data-ttu-id="ce83a-150">Olá código a seguir procura uma entidade customer denominada "Ben Smith" e se encontrá-lo, ele o excluirá.</span><span class="sxs-lookup"><span data-stu-id="ce83a-150">hello following code looks for a customer entity named "Ben Smith" and if it finds it, it deletes it.</span></span>

    // Create a retrieve operation that expects a customer entity.
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

    // Execute hello operation.
    TableResult retrievedResult = peopleTable.Execute(retrieveOperation);

    // Assign hello result tooa CustomerEntity object.
    CustomerEntity deleteEntity = (CustomerEntity)retrievedResult.Result;

    // Create hello Delete TableOperation and then execute it.
    if (deleteEntity != null)
    {
       TableOperation deleteOperation = TableOperation.Delete(deleteEntity);

       // Execute hello operation.
       await peopleTable.ExecuteAsync(deleteOperation);

       Console.WriteLine("Entity deleted.");
    }

    else
       Console.WriteLine("Couldn't delete hello entity.");

## <a name="next-steps"></a><span data-ttu-id="ce83a-151">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ce83a-151">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-tables-next-steps](../../includes/vs-storage-dotnet-tables-next-steps.md)]

