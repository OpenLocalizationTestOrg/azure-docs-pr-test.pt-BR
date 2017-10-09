---
title: "aaaGet de Introdução ao armazenamento de tabela e o Visual Studio serviços conectados (serviços de nuvem) | Microsoft Docs"
description: "Como tooget iniciado usando o armazenamento de tabela do Azure em um projeto de serviço de nuvem no Visual Studio depois de conectar-se a conta de armazenamento tooa usando o Visual Studio conectada a serviços"
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
ms.openlocfilehash: efb16953e05764cb162cbdae4d0eab57f781682d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-table-storage-and-visual-studio-connected-services-cloud-services-projects"></a><span data-ttu-id="8663c-103">Introdução ao armazenamento de tabela do Azure e aos serviços conectados do Visual Studio (projetos de serviços de nuvem)</span><span class="sxs-lookup"><span data-stu-id="8663c-103">Getting started with Azure table storage and Visual Studio connected services (cloud services projects)</span></span>
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a><span data-ttu-id="8663c-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="8663c-104">Overview</span></span>
<span data-ttu-id="8663c-105">Este artigo descreve como tooget iniciado usando o armazenamento de tabela do Azure no Visual Studio depois que você criou ou referenciado uma conta de armazenamento do Azure em um projeto de serviços de nuvem usando o Visual Studio de saudação **adicionar serviços conectados** caixa de diálogo .</span><span class="sxs-lookup"><span data-stu-id="8663c-105">This article describes how tooget started using Azure table storage in Visual Studio after you have created or referenced an Azure storage account in a cloud services project by using hello Visual Studio **Add Connected Services** dialog.</span></span> <span data-ttu-id="8663c-106">Olá **adicionar serviços conectados** operação instala Olá apropriado NuGet pacotes tooaccess armazenamento do Azure em seu projeto e adiciona a cadeia de caracteres de conexão Olá para hello conta de armazenamento tooyour arquivos de configuração do projeto.</span><span class="sxs-lookup"><span data-stu-id="8663c-106">hello **Add Connected Services** operation installs hello appropriate NuGet packages tooaccess Azure storage in your project and adds hello connection string for hello storage account tooyour project configuration files.</span></span>

<span data-ttu-id="8663c-107">saudação de serviço de armazenamento de tabela do Azure permite que você toostore grandes quantidades de dados estruturados.</span><span class="sxs-lookup"><span data-stu-id="8663c-107">hello Azure Table storage service enables you toostore large amounts of structured data.</span></span> <span data-ttu-id="8663c-108">serviço de saudação é um repositório de dados NoSQL que aceita chamadas autenticadas de dentro e fora hello nuvem do Azure.</span><span class="sxs-lookup"><span data-stu-id="8663c-108">hello service is a NoSQL datastore that accepts authenticated calls from inside and outside hello Azure cloud.</span></span> <span data-ttu-id="8663c-109">As tabelas do Azure são ideais para armazenar dados estruturados não relacionais.</span><span class="sxs-lookup"><span data-stu-id="8663c-109">Azure tables are ideal for storing structured, non-relational data.</span></span>

<span data-ttu-id="8663c-110">tooget iniciado, você primeiro precisa toocreate uma tabela em sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="8663c-110">tooget started, you first need toocreate a table in your storage account.</span></span> <span data-ttu-id="8663c-111">Mostraremos como toocreate um Azure tabela no código e como tabela básica tooperform e operações da entidade, como adicionar, modificar, ler e ler da tabela de entidades.</span><span class="sxs-lookup"><span data-stu-id="8663c-111">We'll show you how toocreate an Azure table in code, and also how tooperform basic table and entity operations, such as adding, modifying, reading and reading table entities.</span></span> <span data-ttu-id="8663c-112">exemplos de saudação são escritos em C\# de código e use Olá [biblioteca de cliente de armazenamento do Microsoft Azure para .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span><span class="sxs-lookup"><span data-stu-id="8663c-112">hello samples are written in C\# code and use hello [Microsoft Azure Storage client library for .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span></span>

<span data-ttu-id="8663c-113">**Observação:** alguns Olá APIs que executam chamadas tooAzure armazenamento são assíncronas.</span><span class="sxs-lookup"><span data-stu-id="8663c-113">**NOTE:** Some of hello APIs that perform calls out tooAzure storage are asynchronous.</span></span> <span data-ttu-id="8663c-114">Confira [Programação assíncrona com Async e Await](http://msdn.microsoft.com/library/hh191443.aspx) para saber mais.</span><span class="sxs-lookup"><span data-stu-id="8663c-114">See [Asynchronous programming with Async and Await](http://msdn.microsoft.com/library/hh191443.aspx) for more information.</span></span> <span data-ttu-id="8663c-115">código de saudação abaixo supõe que os métodos de programação assíncrona estão sendo usados.</span><span class="sxs-lookup"><span data-stu-id="8663c-115">hello code below assumes async programming methods are being used.</span></span>

* <span data-ttu-id="8663c-116">Consulte [Introdução ao Armazenamento de Tabelas do Azure usando .NET](storage-dotnet-how-to-use-tables.md) para obter mais informações sobre como manipular tabelas com programação.</span><span class="sxs-lookup"><span data-stu-id="8663c-116">See [Get started with Azure Table storage using .NET](storage-dotnet-how-to-use-tables.md) for more information on programmatically manipulating tables.</span></span>
* <span data-ttu-id="8663c-117">Consulte a [Documentação de armazenamento](https://azure.microsoft.com/documentation/services/storage/) para obter informações gerais sobre o armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="8663c-117">See [Storage documentation](https://azure.microsoft.com/documentation/services/storage/) for general information about Azure Storage.</span></span>
* <span data-ttu-id="8663c-118">Consulte a [documentação de serviços de nuvem](https://azure.microsoft.com/documentation/services/cloud-services/) para obter informações gerais sobre os serviços de nuvem do Azure.</span><span class="sxs-lookup"><span data-stu-id="8663c-118">See [Cloud Services documentation](https://azure.microsoft.com/documentation/services/cloud-services/) for general information about Azure cloud services.</span></span>
* <span data-ttu-id="8663c-119">Consulte [ASP.NET](http://www.asp.net) para obter mais informações sobre como programar aplicativos ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="8663c-119">See [ASP.NET](http://www.asp.net) for more information about programming ASP.NET applications.</span></span>

## <a name="access-tables-in-code"></a><span data-ttu-id="8663c-120">Acessar tabelas em código</span><span class="sxs-lookup"><span data-stu-id="8663c-120">Access tables in code</span></span>
<span data-ttu-id="8663c-121">tooaccess tabelas em projetos de serviço de nuvem, você precisa de saudação tooinclude seguintes arquivos de origem do itens tooany c# que acessam o armazenamento de tabela do Azure.</span><span class="sxs-lookup"><span data-stu-id="8663c-121">tooaccess tables in cloud service projects, you need tooinclude hello following items tooany C# source files that access Azure table storage.</span></span>

1. <span data-ttu-id="8663c-122">Certifique-se de declarações de namespace Olá na parte superior de saudação do arquivo hello c# incluem-las **usando** instruções.</span><span class="sxs-lookup"><span data-stu-id="8663c-122">Make sure hello namespace declarations at hello top of hello C# file include these **using** statements.</span></span>
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Table;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. <span data-ttu-id="8663c-123">Obtenha um objeto **CloudStorageAccount** que represente as informações da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="8663c-123">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="8663c-124">Use Olá código tooget Olá conta de armazenamento conexão cadeia de caracteres e o armazenamento de informações a seguir da configuração de serviço do Azure de saudação.</span><span class="sxs-lookup"><span data-stu-id="8663c-124">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration.</span></span>
   
         CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
           CloudConfigurationManager.GetSetting("<storage account name>
         _AzureStorageConnectionString"));
   > [!NOTE]
   > <span data-ttu-id="8663c-125">Use todos Olá acima código código Olá no hello exemplos a seguir.</span><span class="sxs-lookup"><span data-stu-id="8663c-125">Use all of hello above code in front of hello code in hello following samples.</span></span>
   > 
   > 
3. <span data-ttu-id="8663c-126">Obter um **CloudTableClient** tooreference Olá tabela objetos na conta de armazenamento de objeto.</span><span class="sxs-lookup"><span data-stu-id="8663c-126">Get a **CloudTableClient** object tooreference hello table objects in your storage account.</span></span>
   
         // Create hello table client.
         CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
4. <span data-ttu-id="8663c-127">Obter um **CloudTable** fazer referência a entidades e objeto tooreference uma tabela específica.</span><span class="sxs-lookup"><span data-stu-id="8663c-127">Get a **CloudTable** reference object tooreference a specific table and entities.</span></span>
   
        // Get a reference tooa table named "peopleTable".
        CloudTable peopleTable = tableClient.GetTableReference("peopleTable");

## <a name="create-a-table-in-code"></a><span data-ttu-id="8663c-128">Criar uma tabela em código</span><span class="sxs-lookup"><span data-stu-id="8663c-128">Create a table in code</span></span>
<span data-ttu-id="8663c-129">Olá toocreate tabela do Azure, basta adicionar uma chamada muito**CreateIfNotExistsAsync** toohello depois de obter um **CloudTable** conforme descrito na seção de "Tabelas de acesso no código" de saudação do objeto.</span><span class="sxs-lookup"><span data-stu-id="8663c-129">toocreate hello Azure table, just add a call too**CreateIfNotExistsAsync** toohello after you get a **CloudTable** object as described in hello "Access tables in code" section.</span></span>

    // Create hello CloudTable if it does not exist.
    await peopleTable.CreateIfNotExistsAsync();

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="8663c-130">Adicionar uma tabela de entidade tooa</span><span class="sxs-lookup"><span data-stu-id="8663c-130">Add an entity tooa table</span></span>
<span data-ttu-id="8663c-131">tooadd uma tabela de tooa de entidade, crie uma classe que define as propriedades de saudação da entidade.</span><span class="sxs-lookup"><span data-stu-id="8663c-131">tooadd an entity tooa table, create a class that defines hello properties of your entity.</span></span> <span data-ttu-id="8663c-132">Olá, código a seguir define uma classe de entidade chamada **CustomerEntity** que usa Olá nome do cliente como chave de linha de saudação e sobrenome Olá como chave de partição hello.</span><span class="sxs-lookup"><span data-stu-id="8663c-132">hello following code defines an entity class called **CustomerEntity** that uses hello customer's first name as hello row key and hello last name as hello partition key.</span></span>

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

<span data-ttu-id="8663c-133">Operações de tabela que envolvem entidades são feitas usando Olá **CloudTable** objeto que você criou anteriormente no "Tabelas de acesso no código".</span><span class="sxs-lookup"><span data-stu-id="8663c-133">Table operations involving entities are done using hello **CloudTable** object that you created earlier in "Access tables in code."</span></span> <span data-ttu-id="8663c-134">Olá **TableOperation** objeto representa Olá operação toobe feito.</span><span class="sxs-lookup"><span data-stu-id="8663c-134">hello **TableOperation** object represents hello operation toobe done.</span></span> <span data-ttu-id="8663c-135">Olá mostra exemplo de código a seguir como toocreate uma **CloudTable** objeto e um **CustomerEntity** objeto.</span><span class="sxs-lookup"><span data-stu-id="8663c-135">hello following code example shows how toocreate a **CloudTable** object and a **CustomerEntity** object.</span></span> <span data-ttu-id="8663c-136">operação de saudação tooprepare, uma **TableOperation** é criado entidade do cliente Olá tooinsert na tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="8663c-136">tooprepare hello operation, a **TableOperation** is created tooinsert hello customer entity into hello table.</span></span> <span data-ttu-id="8663c-137">Por fim, a operação de saudação é executada chamando **CloudTable.ExecuteAsync**.</span><span class="sxs-lookup"><span data-stu-id="8663c-137">Finally, hello operation is executed by calling **CloudTable.ExecuteAsync**.</span></span>

    // Create a new customer entity.
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.Email = "Walter@contoso.com";
    customer1.PhoneNumber = "425-555-0101";

    // Create hello TableOperation that inserts hello customer entity.
    TableOperation insertOperation = TableOperation.Insert(customer1);

    // Execute hello insert operation.
    await peopleTable.ExecuteAsync(insertOperation);


## <a name="insert-a-batch-of-entities"></a><span data-ttu-id="8663c-138">Inserir um lote de entidades</span><span class="sxs-lookup"><span data-stu-id="8663c-138">Insert a batch of entities</span></span>
<span data-ttu-id="8663c-139">Você pode inserir várias entidades em uma tabela em uma única operação de gravação.</span><span class="sxs-lookup"><span data-stu-id="8663c-139">You can insert multiple entities into a table in a single write operation.</span></span> <span data-ttu-id="8663c-140">Olá exemplo de código a seguir cria dois objetos de entidade ("Jeff Smith" e "Ben Smith"), adiciona tooa **TableBatchOperation** objeto usando Olá método de inserção e, em seguida, inicia Olá operação chamando  **CloudTable.ExecuteBatchAsync**.</span><span class="sxs-lookup"><span data-stu-id="8663c-140">hello following code example creates two entity objects ("Jeff Smith" and "Ben Smith"), adds them tooa **TableBatchOperation** object using hello Insert method, and then starts hello operation by calling **CloudTable.ExecuteBatchAsync**.</span></span>

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

## <a name="get-all-of-hello-entities-in-a-partition"></a><span data-ttu-id="8663c-141">Obter todas as entidades de saudação em uma partição</span><span class="sxs-lookup"><span data-stu-id="8663c-141">Get all of hello entities in a partition</span></span>
<span data-ttu-id="8663c-142">tooquery uma tabela para todas as entidades de saudação em uma partição, use um **TableQuery** objeto.</span><span class="sxs-lookup"><span data-stu-id="8663c-142">tooquery a table for all of hello entities in a partition, use a **TableQuery** object.</span></span> <span data-ttu-id="8663c-143">Olá, exemplo de código a seguir especifica um filtro para entidades onde 'Smith' é a chave de partição hello.</span><span class="sxs-lookup"><span data-stu-id="8663c-143">hello following code example specifies a filter for entities where 'Smith' is hello partition key.</span></span> <span data-ttu-id="8663c-144">Este exemplo imprime campos de saudação de cada entidade no console de toohello de resultados de consulta de saudação.</span><span class="sxs-lookup"><span data-stu-id="8663c-144">This example prints hello fields of each entity in hello query results toohello console.</span></span>

    // Construct hello query operation for all customer entities where PartitionKey="Smith".
    TableQuery<CustomerEntity> query = new TableQuery<CustomerEntity>()
        .Where(TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"));

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

    return View();


## <a name="get-a-single-entity"></a><span data-ttu-id="8663c-145">Obter uma única entidade</span><span class="sxs-lookup"><span data-stu-id="8663c-145">Get a single entity</span></span>
<span data-ttu-id="8663c-146">Você pode escrever uma consulta tooget uma entidade única e específica.</span><span class="sxs-lookup"><span data-stu-id="8663c-146">You can write a query tooget a single, specific entity.</span></span> <span data-ttu-id="8663c-147">código a seguir Olá usa um **TableOperation** toospecify um cliente chamado 'Ben Smith' do objeto.</span><span class="sxs-lookup"><span data-stu-id="8663c-147">hello following code uses a **TableOperation** object toospecify a customer named 'Ben Smith'.</span></span> <span data-ttu-id="8663c-148">Esse método retorna uma única entidade, em vez de uma coleção e Olá retornou o valor em **TableResult.Result** é um **CustomerEntity** objeto.</span><span class="sxs-lookup"><span data-stu-id="8663c-148">This method returns just one entity, rather than a collection, and hello returned value in **TableResult.Result** is a **CustomerEntity** object.</span></span> <span data-ttu-id="8663c-149">Especificar chaves de partição e de linha em uma consulta é tooretrieve de maneira mais rápida de saudação uma única entidade de saudação **tabela** serviço.</span><span class="sxs-lookup"><span data-stu-id="8663c-149">Specifying both partition and row keys in a query is hello fastest way tooretrieve a single entity from hello **Table** service.</span></span>

    // Create a retrieve operation that takes a customer entity.
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

    // Execute hello retrieve operation.
    TableResult retrievedResult = await peopleTable.ExecuteAsync(retrieveOperation);

    // Print hello phone number of hello result.
    if (retrievedResult.Result != null)
       Console.WriteLine(((CustomerEntity)retrievedResult.Result).PhoneNumber);
    else
       Console.WriteLine("hello phone number could not be retrieved.");

## <a name="delete-an-entity"></a><span data-ttu-id="8663c-150">Excluir uma entidade</span><span class="sxs-lookup"><span data-stu-id="8663c-150">Delete an entity</span></span>
<span data-ttu-id="8663c-151">Você poderá excluir uma entidade facilmente depois de encontrá-la.</span><span class="sxs-lookup"><span data-stu-id="8663c-151">You can delete an entity after you find it.</span></span> <span data-ttu-id="8663c-152">Hello código a seguir procura uma entidade customer denominada "Ben Smith" e, se encontrá-lo, ele o excluirá.</span><span class="sxs-lookup"><span data-stu-id="8663c-152">hello following code looks for a customer entity named "Ben Smith", and if it finds it, it deletes it.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="8663c-153">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8663c-153">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-tables-next-steps](../../includes/vs-storage-dotnet-tables-next-steps.md)]

