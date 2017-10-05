---
title: Como usar o armazenamento de Tabelas (C++) | Microsoft Docs
description: "Armazene dados estruturados na nuvem usando o Armazenamento de Tabelas do Azure, um repositório de dados NoSQL."
services: cosmos-db
documentationcenter: .net
author: mimig1
manager: jahogg
editor: tysonn
ms.assetid: f191f308-e4b2-4de9-85cb-551b82b1ea7c
ms.service: cosmos-db
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/28/2017
ms.author: mimig
ms.openlocfilehash: 8314292cdb9b7a3f464c60119ed10f6b06ed4d10
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-table-storage-from-c"></a><span data-ttu-id="2a958-103">Como usar o armazenamento de Tabela por meio do C++</span><span class="sxs-lookup"><span data-stu-id="2a958-103">How to use Table storage from C++</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a><span data-ttu-id="2a958-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="2a958-104">Overview</span></span>
<span data-ttu-id="2a958-105">Este guia mostra como executar cenários comuns usando o serviço de Armazenamento de Tabela do Azure.</span><span class="sxs-lookup"><span data-stu-id="2a958-105">This guide will show you how to perform common scenarios by using the Azure Table storage service.</span></span> <span data-ttu-id="2a958-106">Os exemplos são escritos em C++ e usam a [Biblioteca do Cliente de Armazenamento do Azure para C++](https://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="2a958-106">The samples are written in C++ and use the [Azure Storage Client Library for C++](https://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span></span> <span data-ttu-id="2a958-107">Os cenários abordados incluem a **criação e a exclusão de uma tabela** e o **trabalho com entidades de tabela**.</span><span class="sxs-lookup"><span data-stu-id="2a958-107">The scenarios covered include **creating and deleting a table** and **working with table entities**.</span></span>

> [!NOTE]
> <span data-ttu-id="2a958-108">Este guia tem como alvo a Biblioteca do Cliente de Armazenamento do Azure para C++, versão 1.0.0 e superior.</span><span class="sxs-lookup"><span data-stu-id="2a958-108">This guide targets the Azure Storage Client Library for C++ version 1.0.0 and above.</span></span> <span data-ttu-id="2a958-109">A versão recomendada é a Biblioteca de Clientes de Armazenamento 2.2.0, que está disponível via [NuGet](http://www.nuget.org/packages/wastorage) ou [GitHub](https://github.com/Azure/azure-storage-cpp/).</span><span class="sxs-lookup"><span data-stu-id="2a958-109">The recommended version is Storage Client Library 2.2.0, which is available via [NuGet](http://www.nuget.org/packages/wastorage) or [GitHub](https://github.com/Azure/azure-storage-cpp/).</span></span>
> 
> 

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-c-application"></a><span data-ttu-id="2a958-110">Criar um aplicativo em C++</span><span class="sxs-lookup"><span data-stu-id="2a958-110">Create a C++ application</span></span>
<span data-ttu-id="2a958-111">Neste guia, você usará os recursos de armazenamento que podem ser executados em um aplicativo do C++.</span><span class="sxs-lookup"><span data-stu-id="2a958-111">In this guide, you will use storage features that can be run within a C++ application.</span></span> <span data-ttu-id="2a958-112">Para isso, você precisará instalar a Biblioteca do Cliente de Armazenamento do Azure para C++ e criar uma conta de armazenamento do Azure em sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="2a958-112">To do so, you will need to install the Azure Storage Client Library for C++ and create an Azure storage account in your Azure subscription.</span></span>  

<span data-ttu-id="2a958-113">Para instalar a Biblioteca do Cliente de Armazenamento do Azure para C++, você pode usar os seguintes métodos:</span><span class="sxs-lookup"><span data-stu-id="2a958-113">To install the Azure Storage Client Library for C++, you can use the following methods:</span></span>

* <span data-ttu-id="2a958-114">**Linux:** siga as instruções fornecidas na página [LEIAME da Biblioteca do Cliente de Armazenamento do Azure para C++](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) .</span><span class="sxs-lookup"><span data-stu-id="2a958-114">**Linux:** Follow the instructions given on the [Azure Storage Client Library for C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) page.</span></span>  
* <span data-ttu-id="2a958-115">**Windows:** no Visual Studio, clique em **Ferramentas > Gerenciador de Pacotes do NuGet > Console do Gerenciador de Pacotes**.</span><span class="sxs-lookup"><span data-stu-id="2a958-115">**Windows:** In Visual Studio, click **Tools > NuGet Package Manager > Package Manager Console**.</span></span> <span data-ttu-id="2a958-116">Digite o comando a seguir no [console do Gerenciador de Pacotes do NuGet](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) e pressione Enter.</span><span class="sxs-lookup"><span data-stu-id="2a958-116">Type the following command into the [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) and press Enter.</span></span>  
  
     <span data-ttu-id="2a958-117">Install-Package wastorage</span><span class="sxs-lookup"><span data-stu-id="2a958-117">Install-Package wastorage</span></span>

## <a name="configure-your-application-to-access-table-storage"></a><span data-ttu-id="2a958-118">Configurar seu aplicativo para acessar o armazenamento de tabela</span><span class="sxs-lookup"><span data-stu-id="2a958-118">Configure your application to access Table storage</span></span>
<span data-ttu-id="2a958-119">Adicione as seguintes instruções include à parte superior do arquivo C++ no qual deseja usar as APIs de armazenamento do Azure para acessar as tabelas:</span><span class="sxs-lookup"><span data-stu-id="2a958-119">Add the following include statements to the top of the C++ file where you want to use the Azure storage APIs to access tables:</span></span>  

```cpp
#include <was/storage_account.h>
#include <was/table.h>
```

## <a name="set-up-an-azure-storage-connection-string"></a><span data-ttu-id="2a958-120">Configurar uma cadeia de conexão de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="2a958-120">Set up an Azure storage connection string</span></span>
<span data-ttu-id="2a958-121">Um cliente de armazenamento do Azure usa uma cadeia de conexão para armazenar pontos de extremidade e credenciais para acessar serviços de gerenciamento de dados.</span><span class="sxs-lookup"><span data-stu-id="2a958-121">An Azure storage client uses a storage connection string to store endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="2a958-122">Ao executar um aplicativo cliente, você deve fornecer a cadeia de conexão de armazenamento no formato a seguir.</span><span class="sxs-lookup"><span data-stu-id="2a958-122">When running a client application, you must provide the storage connection string in the following format.</span></span> <span data-ttu-id="2a958-123">Use o nome de sua conta de armazenamento e a chave de acesso de armazenamento para a conta de armazenamento listada no [Portal do Azure](https://portal.azure.com) para os valores *AccountName* e *AccountKey*.</span><span class="sxs-lookup"><span data-stu-id="2a958-123">Use the name of your storage account and the storage access key for the storage account listed in the [Azure Portal](https://portal.azure.com) for the *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="2a958-124">Para obter informações sobre as contas de armazenamento e as teclas de acesso, veja [Sobre as contas de armazenamento do Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="2a958-124">For information on storage accounts and access keys, see [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="2a958-125">Este exemplo mostra como você pode declarar um campo estático para armazenar a cadeia de conexão:</span><span class="sxs-lookup"><span data-stu-id="2a958-125">This example shows how you can declare a static field to hold the connection string:</span></span>  

```cpp
// Define the connection string with your values.
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

<span data-ttu-id="2a958-126">Para testar seu aplicativo no computador local baseado em Windows, você pode usar o [emulador de armazenamento](../storage/common/storage-use-emulator.md) do Azure que é instalado com o [SDK do Azure](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="2a958-126">To test your application in your local Windows-based computer, you can use the Azure [storage emulator](../storage/common/storage-use-emulator.md) that is installed with the [Azure SDK](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="2a958-127">O emulador de armazenamento é um utilitário que simula os serviços de Blob, Fila e Tabela do Azure disponíveis em seu computador de desenvolvimento local.</span><span class="sxs-lookup"><span data-stu-id="2a958-127">The storage emulator is a utility that simulates the Azure Blob, Queue, and Table services available on your local development machine.</span></span> <span data-ttu-id="2a958-128">Este exemplo mostra como você pode declarar um campo estático para manter a cadeia de conexão em seu emulador de armazenamento local:</span><span class="sxs-lookup"><span data-stu-id="2a958-128">The following example shows how you can declare a static field to hold the connection string to your local storage emulator:</span></span>  

```cpp
// Define the connection string with Azure storage emulator.
const utility::string_t storage_connection_string(U("UseDevelopmentStorage=true;"));  
```

<span data-ttu-id="2a958-129">Para iniciar o emulador de armazenamento do Azure, clique no botão **Iniciar** ou pressione a tecla Windows.</span><span class="sxs-lookup"><span data-stu-id="2a958-129">To start the Azure storage emulator, click the **Start** button or press the Windows key.</span></span> <span data-ttu-id="2a958-130">Comece digitando **Emulador de Armazenamento do Azure** e selecione **Emulador de Armazenamento do Microsoft Azure** na lista de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="2a958-130">Begin typing **Azure Storage Emulator**, and then select **Microsoft Azure Storage Emulator** from the list of applications.</span></span>  

<span data-ttu-id="2a958-131">Os exemplos abaixo pressupõem que você usou um desses dois métodos para obter a cadeia de conexão do armazenamento.</span><span class="sxs-lookup"><span data-stu-id="2a958-131">The following samples assume that you have used one of these two methods to get the storage connection string.</span></span>  

## <a name="retrieve-your-connection-string"></a><span data-ttu-id="2a958-132">Recuperar sua cadeia de conexão</span><span class="sxs-lookup"><span data-stu-id="2a958-132">Retrieve your connection string</span></span>
<span data-ttu-id="2a958-133">É possível usar a classe **cloud_storage_account** para representar as informações da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="2a958-133">You can use the **cloud_storage_account** class to represent your storage account information.</span></span> <span data-ttu-id="2a958-134">Para recuperar as informações da conta de armazenamento na cadeia de conexão de armazenamento, você pode usar o método de analisar.</span><span class="sxs-lookup"><span data-stu-id="2a958-134">To retrieve your storage account information from the storage connection string, you can use the parse method.</span></span>

```cpp
// Retrieve the storage account from the connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);
```

<span data-ttu-id="2a958-135">Em seguida, obtenha uma referência a uma classe **cloud_table_client** que permita recuperar os objetos de referência para as tabelas e as entidades armazenadas no serviço de armazenamento de Tabelas.</span><span class="sxs-lookup"><span data-stu-id="2a958-135">Next, get a reference to a **cloud_table_client** class, as it lets you get reference objects for tables and entities stored within the Table storage service.</span></span> <span data-ttu-id="2a958-136">O seguinte código cria um objeto **cloud_table_client** usando o objeto da conta de armazenamento que recuperamos acima:</span><span class="sxs-lookup"><span data-stu-id="2a958-136">The following code creates a **cloud_table_client** object by using the storage account object we retrieved above:</span></span>  

```cpp
// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();
```

## <a name="create-a-table"></a><span data-ttu-id="2a958-137">Criar uma tabela</span><span class="sxs-lookup"><span data-stu-id="2a958-137">Create a table</span></span>
<span data-ttu-id="2a958-138">Um objeto **cloud_table_client** permite obter os objetos de referência para tabelas e entidades.</span><span class="sxs-lookup"><span data-stu-id="2a958-138">A **cloud_table_client** object lets you get reference objects for tables and entities.</span></span> <span data-ttu-id="2a958-139">O código a seguir cria um objeto **cloud_table_client** e utiliza-o para criar uma nova tabela.</span><span class="sxs-lookup"><span data-stu-id="2a958-139">The following code creates a **cloud_table_client** object and uses it to create a new table.</span></span>

```cpp
// Retrieve the storage account from the connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);  

// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Retrieve a reference to a table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create the table if it doesn't exist.
table.create_if_not_exists();  
```

## <a name="add-an-entity-to-a-table"></a><span data-ttu-id="2a958-140">Adicionar uma entidade a uma tabela</span><span class="sxs-lookup"><span data-stu-id="2a958-140">Add an entity to a table</span></span>
<span data-ttu-id="2a958-141">Para adicionar uma entidade a uma tabela, crie um novo objeto **cloud_table_client** e passe-o para **table_operation::insert_entity**.</span><span class="sxs-lookup"><span data-stu-id="2a958-141">To add an entity to a table, create a new **table_entity** object and pass it to **table_operation::insert_entity**.</span></span> <span data-ttu-id="2a958-142">O código a seguir usa o primeiro nome do cliente como a chave de linha e o último nome como a chave de partição.</span><span class="sxs-lookup"><span data-stu-id="2a958-142">The following code uses the customer's first name as the row key and last name as the partition key.</span></span> <span data-ttu-id="2a958-143">Juntas, uma chave de partição e uma chave de linha identificam exclusivamente a entidade na tabela.</span><span class="sxs-lookup"><span data-stu-id="2a958-143">Together, an entity's partition and row key uniquely identify the entity in the table.</span></span> <span data-ttu-id="2a958-144">As entidades com a mesma chave de partição podem ser consultadas mais rápido do que aquelas com chaves de partição diferentes, mas usar chaves de partição diferentes possibilita uma maior escalabilidade de operação paralela.</span><span class="sxs-lookup"><span data-stu-id="2a958-144">Entities with the same partition key can be queried faster than those with different partition keys, but using diverse partition keys allows for greater parallel operation scalability.</span></span> <span data-ttu-id="2a958-145">Para obter mais informações, veja [Lista de verificação de escalabilidade e desempenho do Armazenamento do Microsoft Azure](../storage/common/storage-performance-checklist.md).</span><span class="sxs-lookup"><span data-stu-id="2a958-145">For more information, see [Microsoft Azure storage performance and scalability checklist](../storage/common/storage-performance-checklist.md).</span></span>

<span data-ttu-id="2a958-146">O código a seguir cria uma nova instância de **table_entity** com alguns dados do cliente que serão armazenados.</span><span class="sxs-lookup"><span data-stu-id="2a958-146">The following code creates a new instance of **table_entity** with some customer data to be stored.</span></span> <span data-ttu-id="2a958-147">O próximo código chama **table_operation::insert_entity** para criar um objeto **table_operation** para inserir uma entidade em uma tabela e associa a nova entidade da tabela a ele.</span><span class="sxs-lookup"><span data-stu-id="2a958-147">The code next calls **table_operation::insert_entity** to create a **table_operation** object to insert an entity into a table, and associates the new table entity with it.</span></span> <span data-ttu-id="2a958-148">Por fim, o código chama o método execute no objeto **cloud_table**.</span><span class="sxs-lookup"><span data-stu-id="2a958-148">Finally, the code calls the execute method on the **cloud_table** object.</span></span> <span data-ttu-id="2a958-149">E o novo **table_operation**n envia uma solicitação ao serviço Tabela para inserir a nova entidade de cliente na tabela “pessoas”.</span><span class="sxs-lookup"><span data-stu-id="2a958-149">And the new **table_operation** sends a request to the Table service to insert the new customer entity into the "people" table.</span></span>  

```cpp
// Retrieve the storage account from the connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Retrieve a reference to a table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create the table if it doesn't exist.
table.create_if_not_exists();

// Create a new customer entity.
azure::storage::table_entity customer1(U("Harp"), U("Walter"));

azure::storage::table_entity::properties_type& properties = customer1.properties();
properties.reserve(2);
properties[U("Email")] = azure::storage::entity_property(U("Walter@contoso.com"));

properties[U("Phone")] = azure::storage::entity_property(U("425-555-0101"));

// Create the table operation that inserts the customer entity.
azure::storage::table_operation insert_operation = azure::storage::table_operation::insert_entity(customer1);

// Execute the insert operation.
azure::storage::table_result insert_result = table.execute(insert_operation);
```

## <a name="insert-a-batch-of-entities"></a><span data-ttu-id="2a958-150">Inserir um lote de entidades</span><span class="sxs-lookup"><span data-stu-id="2a958-150">Insert a batch of entities</span></span>
<span data-ttu-id="2a958-151">É possível inserir um lote de entidades ao serviço Tabela em uma operação de gravação.</span><span class="sxs-lookup"><span data-stu-id="2a958-151">You can insert a batch of entities to the Table service in one write operation.</span></span> <span data-ttu-id="2a958-152">O código a seguir cria um objeto **table_batch_operation** e adiciona três operações de inserção a ele.</span><span class="sxs-lookup"><span data-stu-id="2a958-152">The following code creates a **table_batch_operation** object, and then adds three insert operations to it.</span></span> <span data-ttu-id="2a958-153">Cada operação de inserção é adicionada criando um novo objeto de entidade, definindo seus valores, em seguida, chamando o método insert no objeto **table_batch_operation**n para associar a entidade a uma nova operação de inserção.</span><span class="sxs-lookup"><span data-stu-id="2a958-153">Each insert operation is added by creating a new entity object, setting its values, and then calling the insert method on the **table_batch_operation** object to associate the entity with a new insert operation.</span></span> <span data-ttu-id="2a958-154">Em seguida, **cloud_table.execute** é chamado para executar a operação.</span><span class="sxs-lookup"><span data-stu-id="2a958-154">Then, **cloud_table.execute** is called to execute the operation.</span></span>  

```cpp
// Retrieve the storage account from the connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for the table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Define a batch operation.
azure::storage::table_batch_operation batch_operation;

// Create a customer entity and add it to the table.
azure::storage::table_entity customer1(U("Smith"), U("Jeff"));

azure::storage::table_entity::properties_type& properties1 = customer1.properties();
properties1.reserve(2);
properties1[U("Email")] = azure::storage::entity_property(U("Jeff@contoso.com"));
properties1[U("Phone")] = azure::storage::entity_property(U("425-555-0104"));

// Create another customer entity and add it to the table.
azure::storage::table_entity customer2(U("Smith"), U("Ben"));

azure::storage::table_entity::properties_type& properties2 = customer2.properties();
properties2.reserve(2);
properties2[U("Email")] = azure::storage::entity_property(U("Ben@contoso.com"));
properties2[U("Phone")] = azure::storage::entity_property(U("425-555-0102"));

// Create a third customer entity to add to the table.
azure::storage::table_entity customer3(U("Smith"), U("Denise"));

azure::storage::table_entity::properties_type& properties3 = customer3.properties();
properties3.reserve(2);
properties3[U("Email")] = azure::storage::entity_property(U("Denise@contoso.com"));
properties3[U("Phone")] = azure::storage::entity_property(U("425-555-0103"));

// Add customer entities to the batch insert operation.
batch_operation.insert_or_replace_entity(customer1);
batch_operation.insert_or_replace_entity(customer2);
batch_operation.insert_or_replace_entity(customer3);

// Execute the batch operation.
std::vector<azure::storage::table_result> results = table.execute_batch(batch_operation);
```

<span data-ttu-id="2a958-155">Algumas outras observações sobre as operações em lote:</span><span class="sxs-lookup"><span data-stu-id="2a958-155">Some things to note on batch operations:</span></span>  

* <span data-ttu-id="2a958-156">Você pode executar até 100 operações de inserção, exclusão, mesclagem, substituição, inserção ou mesclagem e inserção ou substituição em qualquer combinação em um único lote.</span><span class="sxs-lookup"><span data-stu-id="2a958-156">You can perform up to 100 insert, delete, merge, replace, insert-or-merge, and insert-or-replace operations in any combination in a single batch.</span></span>  
* <span data-ttu-id="2a958-157">Uma operação em lote pode ter uma operação de recuperação se ela for a única operação no lote.</span><span class="sxs-lookup"><span data-stu-id="2a958-157">A batch operation can have a retrieve operation, if it is the only operation in the batch.</span></span>  
* <span data-ttu-id="2a958-158">Todas as entidades em uma única operação em lote devem ter a mesma chave de partição.</span><span class="sxs-lookup"><span data-stu-id="2a958-158">All entities in a single batch operation must have the same partition key.</span></span>  
* <span data-ttu-id="2a958-159">Uma operação em lote está limitada a uma carga de dados de 4 MB.</span><span class="sxs-lookup"><span data-stu-id="2a958-159">A batch operation is limited to a 4-MB data payload.</span></span>  

## <a name="retrieve-all-entities-in-a-partition"></a><span data-ttu-id="2a958-160">Recuperar todas as entidades em uma partição</span><span class="sxs-lookup"><span data-stu-id="2a958-160">Retrieve all entities in a partition</span></span>
<span data-ttu-id="2a958-161">Para consultar uma tabela de todas as entidades em uma partição, use um objeto **table_query**.</span><span class="sxs-lookup"><span data-stu-id="2a958-161">To query a table for all entities in a partition, use a **table_query** object.</span></span> <span data-ttu-id="2a958-162">O exemplo de código a seguir especifica um filtro para entidades onde 'Smith' é a chave da partição.</span><span class="sxs-lookup"><span data-stu-id="2a958-162">The following code example specifies a filter for entities where 'Smith' is the partition key.</span></span> <span data-ttu-id="2a958-163">Esse exemplo imprime os campos de cada entidade nos resultados da consulta no console.</span><span class="sxs-lookup"><span data-stu-id="2a958-163">This example prints the fields of each entity in the query results to the console.</span></span>  

```cpp
// Retrieve the storage account from the connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for the table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Construct the query operation for all customer entities where PartitionKey="Smith".
azure::storage::table_query query;

query.set_filter_string(azure::storage::table_query::generate_filter_condition(U("PartitionKey"), azure::storage::query_comparison_operator::equal, U("Smith")));

// Execute the query.
azure::storage::table_query_iterator it = table.execute_query(query);

// Print the fields for each customer.
azure::storage::table_query_iterator end_of_results;
for (; it != end_of_results; ++it)
{
    const azure::storage::table_entity::properties_type& properties = it->properties();

    std::wcout << U("PartitionKey: ") << it->partition_key() << U(", RowKey: ") << it->row_key()
        << U(", Property1: ") << properties.at(U("Email")).string_value()
        << U(", Property2: ") << properties.at(U("Phone")).string_value() << std::endl;
}  
```

<span data-ttu-id="2a958-164">A consulta neste exemplo traz todas as entidades que correspondem aos critérios do filtro.</span><span class="sxs-lookup"><span data-stu-id="2a958-164">The query in this example brings all the entities that match the filter criteria.</span></span> <span data-ttu-id="2a958-165">Se você tiver tabelas grandes e precisar baixar entidades de tabela com frequência, recomendamos que armazene seus dados nos blobs de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="2a958-165">If you have large tables and need to download the table entities often, we recommend that you store your data in Azure storage blobs instead.</span></span>

## <a name="retrieve-a-range-of-entities-in-a-partition"></a><span data-ttu-id="2a958-166">Recuperar um intervalo de entidades em uma partição</span><span class="sxs-lookup"><span data-stu-id="2a958-166">Retrieve a range of entities in a partition</span></span>
<span data-ttu-id="2a958-167">Se não desejar consultar todas as entidades em uma partição, você poderá especificar um intervalo combinando o filtro de chave de partição com um filtro de chave de linha.</span><span class="sxs-lookup"><span data-stu-id="2a958-167">If you don't want to query all the entities in a partition, you can specify a range by combining the partition key filter with a row key filter.</span></span> <span data-ttu-id="2a958-168">O exemplo de código a seguir usa dois filtros para obter todas as entidades na partição 'Smith' onde a chave de linha (nome) começa com uma letra anterior a 'E' do alfabeto e, em seguida, imprime os resultados da consulta.</span><span class="sxs-lookup"><span data-stu-id="2a958-168">The following code example uses two filters to get all entities in partition 'Smith' where the row key (first name) starts with a letter earlier than 'E' in the alphabet and then prints the query results.</span></span>  

```cpp
// Retrieve the storage account from the connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for the table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create the table query.
azure::storage::table_query query;

query.set_filter_string(azure::storage::table_query::combine_filter_conditions(
    azure::storage::table_query::generate_filter_condition(U("PartitionKey"),
    azure::storage::query_comparison_operator::equal, U("Smith")),
    azure::storage::query_logical_operator::op_and,
    azure::storage::table_query::generate_filter_condition(U("RowKey"), azure::storage::query_comparison_operator::less_than, U("E"))));

// Execute the query.
azure::storage::table_query_iterator it = table.execute_query(query);

// Loop through the results, displaying information about the entity.
azure::storage::table_query_iterator end_of_results;
for (; it != end_of_results; ++it)
{
    const azure::storage::table_entity::properties_type& properties = it->properties();

    std::wcout << U("PartitionKey: ") << it->partition_key() << U(", RowKey: ") << it->row_key()
        << U(", Property1: ") << properties.at(U("Email")).string_value()
        << U(", Property2: ") << properties.at(U("Phone")).string_value() << std::endl;
}  
```

## <a name="retrieve-a-single-entity"></a><span data-ttu-id="2a958-169">Recuperar uma única entidade</span><span class="sxs-lookup"><span data-stu-id="2a958-169">Retrieve a single entity</span></span>
<span data-ttu-id="2a958-170">Você pode escrever uma consulta para recuperar uma entidade única e específica.</span><span class="sxs-lookup"><span data-stu-id="2a958-170">You can write a query to retrieve a single, specific entity.</span></span> <span data-ttu-id="2a958-171">O código a seguir usa uma **table_operation::retrieve_entity** para especificar o cliente ‘Diogo Martins’.</span><span class="sxs-lookup"><span data-stu-id="2a958-171">The following code uses **table_operation::retrieve_entity** to specify the customer 'Jeff Smith'.</span></span> <span data-ttu-id="2a958-172">Esse método retorna uma única entidade, em vez de uma coleção, e o valor retornado está em **table_result**.</span><span class="sxs-lookup"><span data-stu-id="2a958-172">This method returns just one entity, rather than a collection, and the returned value is in **table_result**.</span></span> <span data-ttu-id="2a958-173">Especificar chaves de partição e de linha em uma consulta é a maneira mais rápida de recuperar uma única entidade de serviço Table.</span><span class="sxs-lookup"><span data-stu-id="2a958-173">Specifying both partition and row keys in a query is the fastest way to retrieve a single entity from the Table service.</span></span>  

```cpp
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for the table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Retrieve the entity with partition key of "Smith" and row key of "Jeff".
azure::storage::table_operation retrieve_operation = azure::storage::table_operation::retrieve_entity(U("Smith"), U("Jeff"));
azure::storage::table_result retrieve_result = table.execute(retrieve_operation);

// Output the entity.
azure::storage::table_entity entity = retrieve_result.entity();
const azure::storage::table_entity::properties_type& properties = entity.properties();

std::wcout << U("PartitionKey: ") << entity.partition_key() << U(", RowKey: ") << entity.row_key()
    << U(", Property1: ") << properties.at(U("Email")).string_value()
    << U(", Property2: ") << properties.at(U("Phone")).string_value() << std::endl;
```

## <a name="replace-an-entity"></a><span data-ttu-id="2a958-174">Substituir uma entidade</span><span class="sxs-lookup"><span data-stu-id="2a958-174">Replace an entity</span></span>
<span data-ttu-id="2a958-175">Para substituir uma entidade, recupere-a do serviço Tabela, modifique o objeto de entidade e salve as alterações novamente no serviço Tabela.</span><span class="sxs-lookup"><span data-stu-id="2a958-175">To replace an entity, retrieve it from the Table service, modify the entity object, and then save the changes back to the Table service.</span></span> <span data-ttu-id="2a958-176">O código a seguir altera o número de telefone e o endereço de email de um cliente existente.</span><span class="sxs-lookup"><span data-stu-id="2a958-176">The following code changes an existing customer's phone number and email address.</span></span> <span data-ttu-id="2a958-177">Em vez de chamar **table_operation::insert_entity**y, esse código usa **table_operation::replace_entity**.</span><span class="sxs-lookup"><span data-stu-id="2a958-177">Instead of calling **table_operation::insert_entity**, this code uses **table_operation::replace_entity**.</span></span> <span data-ttu-id="2a958-178">Isso faz com que a entidade seja totalmente substituída no servidor, a menos que a entidade no servidor tenha sido alterada desde que foi recuperada, caso em que haverá falha na operação.</span><span class="sxs-lookup"><span data-stu-id="2a958-178">This causes the entity to be fully replaced on the server, unless the entity on the server has changed since it was retrieved, in which case the operation will fail.</span></span> <span data-ttu-id="2a958-179">Essa falha é para impedir que seu aplicativo substitua inadvertidamente uma alteração feita entre a recuperação e a atualização por outro componente de seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2a958-179">This failure is to prevent your application from inadvertently overwriting a change made between the retrieval and update by another component of your application.</span></span> <span data-ttu-id="2a958-180">O tratamento correto dessa falha é recuperar a entidade novamente, fazer as alterações (se ainda válidas) e executar outra operação **table_operation::replace_entity**.</span><span class="sxs-lookup"><span data-stu-id="2a958-180">The proper handling of this failure is to retrieve the entity again, make your changes (if still valid), and then perform another **table_operation::replace_entity** operation.</span></span> <span data-ttu-id="2a958-181">A próxima seção mostrará como substituir esse comportamento.</span><span class="sxs-lookup"><span data-stu-id="2a958-181">The next section will show you how to override this behavior.</span></span>  

```cpp
// Retrieve the storage account from the connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for the table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Replace an entity.
azure::storage::table_entity entity_to_replace(U("Smith"), U("Jeff"));
azure::storage::table_entity::properties_type& properties_to_replace = entity_to_replace.properties();
properties_to_replace.reserve(2);

// Specify a new phone number.
properties_to_replace[U("Phone")] = azure::storage::entity_property(U("425-555-0106"));

// Specify a new email address.
properties_to_replace[U("Email")] = azure::storage::entity_property(U("JeffS@contoso.com"));

// Create an operation to replace the entity.
azure::storage::table_operation replace_operation = azure::storage::table_operation::replace_entity(entity_to_replace);

// Submit the operation to the Table service.
azure::storage::table_result replace_result = table.execute(replace_operation);
```

## <a name="insert-or-replace-an-entity"></a><span data-ttu-id="2a958-182">Inserir ou substituir uma entidade</span><span class="sxs-lookup"><span data-stu-id="2a958-182">Insert-or-replace an entity</span></span>
<span data-ttu-id="2a958-183">As operações **table_operation::replace_entity** falharão se a entidade tiver sido alterada desde que foi recuperada no servidor.</span><span class="sxs-lookup"><span data-stu-id="2a958-183">**table_operation::replace_entity** operations will fail if the entity has been changed since it was retrieved from the server.</span></span> <span data-ttu-id="2a958-184">Além disso, você deve primeiro recuperar a entidade do servidor para que **table_operation::replace_entity** seja bem-sucedido.</span><span class="sxs-lookup"><span data-stu-id="2a958-184">Furthermore, you must retrieve the entity from the server first in order for **table_operation::replace_entity** to be successful.</span></span> <span data-ttu-id="2a958-185">No entanto, às vezes, você não sabe se a entidade existe no servidor e se os valores atuais armazenados nela são irrelevantes – sua atualização deve substituir todos eles.</span><span class="sxs-lookup"><span data-stu-id="2a958-185">Sometimes, however, you don't know if the entity exists on the server and the current values stored in it are irrelevant—your update should overwrite them all.</span></span> <span data-ttu-id="2a958-186">Para fazer isso, você usaria uma operação **table_operation::insert_or_replace_entity**.</span><span class="sxs-lookup"><span data-stu-id="2a958-186">To accomplish this, you would use a **table_operation::insert_or_replace_entity** operation.</span></span> <span data-ttu-id="2a958-187">Essa operação insere a entidade, se ela não existir, ou a substitui, se ela existir, independentemente de quando foi feita a última atualização.</span><span class="sxs-lookup"><span data-stu-id="2a958-187">This operation inserts the entity if it doesn't exist, or replaces it if it does, regardless of when the last update was made.</span></span> <span data-ttu-id="2a958-188">No exemplo de código a seguir, a entidade cliente de João Rodrigues ainda é recuperada, mas é salva novamente no servidor por meio de **table_operation::insert_or_replace_entity**.</span><span class="sxs-lookup"><span data-stu-id="2a958-188">In the following code example, the customer entity for Jeff Smith is still retrieved, but it is then saved back to the server via **table_operation::insert_or_replace_entity**.</span></span> <span data-ttu-id="2a958-189">Todas as atualizações feitas na entidade entre a operação de recuperação e de atualização serão substituídas.</span><span class="sxs-lookup"><span data-stu-id="2a958-189">Any updates made to the entity between the retrieval and update operation will be overwritten.</span></span>  

```cpp
// Retrieve the storage account from the connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for the table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Insert-or-replace an entity.
azure::storage::table_entity entity_to_insert_or_replace(U("Smith"), U("Jeff"));
azure::storage::table_entity::properties_type& properties_to_insert_or_replace = entity_to_insert_or_replace.properties();

properties_to_insert_or_replace.reserve(2);

// Specify a phone number.
properties_to_insert_or_replace[U("Phone")] = azure::storage::entity_property(U("425-555-0107"));

// Specify an email address.
properties_to_insert_or_replace[U("Email")] = azure::storage::entity_property(U("Jeffsm@contoso.com"));

// Create an operation to insert-or-replace the entity.
azure::storage::table_operation insert_or_replace_operation = azure::storage::table_operation::insert_or_replace_entity(entity_to_insert_or_replace);

// Submit the operation to the Table service.
azure::storage::table_result insert_or_replace_result = table.execute(insert_or_replace_operation);
```

## <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="2a958-190">consultar um subconjunto de propriedades da entidade</span><span class="sxs-lookup"><span data-stu-id="2a958-190">Query a subset of entity properties</span></span>
<span data-ttu-id="2a958-191">Uma consulta a uma tabela pode recuperar apenas algumas propriedades de uma entidade.</span><span class="sxs-lookup"><span data-stu-id="2a958-191">A query to a table can retrieve just a few properties from an entity.</span></span> <span data-ttu-id="2a958-192">A consulta no código a seguir usa o método **table_query::set_select_columns** para retornar apenas os endereços de email das entidades na tabela.</span><span class="sxs-lookup"><span data-stu-id="2a958-192">The query in the following code uses the **table_query::set_select_columns** method to return only the email addresses of entities in the table.</span></span>  

```cpp
// Retrieve the storage account from the connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for the table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Define the query, and select only the Email property.
azure::storage::table_query query;
std::vector<utility::string_t> columns;

columns.push_back(U("Email"));
query.set_select_columns(columns);

// Execute the query.
azure::storage::table_query_iterator it = table.execute_query(query);

// Display the results.
azure::storage::table_query_iterator end_of_results;
for (; it != end_of_results; ++it)
{
    std::wcout << U("PartitionKey: ") << it->partition_key() << U(", RowKey: ") << it->row_key();

    const azure::storage::table_entity::properties_type& properties = it->properties();
    for (auto prop_it = properties.begin(); prop_it != properties.end(); ++prop_it)
    {
        std::wcout << ", " << prop_it->first << ": " << prop_it->second.str();
    }

    std::wcout << std::endl;
}
```

> [!NOTE]
> <span data-ttu-id="2a958-193">Consultar algumas propriedades de uma entidade é uma operação mais eficiente do que recuperar todas as propriedades.</span><span class="sxs-lookup"><span data-stu-id="2a958-193">Querying a few properties from an entity is a more efficient operation than retrieving all properties.</span></span>
> 
> 

## <a name="delete-an-entity"></a><span data-ttu-id="2a958-194">Excluir uma entidade</span><span class="sxs-lookup"><span data-stu-id="2a958-194">Delete an entity</span></span>
<span data-ttu-id="2a958-195">Você poderá excluir uma entidade facilmente depois que recuperá-la.</span><span class="sxs-lookup"><span data-stu-id="2a958-195">You can easily delete an entity after you have retrieved it.</span></span> <span data-ttu-id="2a958-196">Depois da entidade ser recuperada, chame **table_operation::delete_entity** com a entidade a excluir.</span><span class="sxs-lookup"><span data-stu-id="2a958-196">Once the entity is retrieved, call **table_operation::delete_entity** with the entity to delete.</span></span> <span data-ttu-id="2a958-197">Em seguida, chame o método **cloud_table.execute**.</span><span class="sxs-lookup"><span data-stu-id="2a958-197">Then call the **cloud_table.execute** method.</span></span> <span data-ttu-id="2a958-198">O código a seguir recupera e exclui uma entidade com uma chave de partição de “Rodrigues” e uma chave de linha de “João”.</span><span class="sxs-lookup"><span data-stu-id="2a958-198">The following code retrieves and deletes an entity with a partition key of "Smith" and a row key of "Jeff".</span></span>  

```cpp
// Retrieve the storage account from the connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for the table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create an operation to retrieve the entity with partition key of "Smith" and row key of "Jeff".
azure::storage::table_operation retrieve_operation = azure::storage::table_operation::retrieve_entity(U("Smith"), U("Jeff"));
azure::storage::table_result retrieve_result = table.execute(retrieve_operation);

// Create an operation to delete the entity.
azure::storage::table_operation delete_operation = azure::storage::table_operation::delete_entity(retrieve_result.entity());

// Submit the delete operation to the Table service.
azure::storage::table_result delete_result = table.execute(delete_operation);  
```

## <a name="delete-a-table"></a><span data-ttu-id="2a958-199">Excluir uma tabela</span><span class="sxs-lookup"><span data-stu-id="2a958-199">Delete a table</span></span>
<span data-ttu-id="2a958-200">Finalmente, o exemplo de código a seguir exclui uma tabela de uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="2a958-200">Finally, the following code example deletes a table from a storage account.</span></span> <span data-ttu-id="2a958-201">Uma tabela excluída não estará disponível para ser recriada durante um período após a exclusão.</span><span class="sxs-lookup"><span data-stu-id="2a958-201">A table that has been deleted will be unavailable to be re-created for a period of time following the deletion.</span></span>  

```cpp
// Retrieve the storage account from the connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for the table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create an operation to retrieve the entity with partition key of "Smith" and row key of "Jeff".
azure::storage::table_operation retrieve_operation = azure::storage::table_operation::retrieve_entity(U("Smith"), U("Jeff"));
azure::storage::table_result retrieve_result = table.execute(retrieve_operation);

// Create an operation to delete the entity.
azure::storage::table_operation delete_operation = azure::storage::table_operation::delete_entity(retrieve_result.entity());

// Submit the delete operation to the Table service.
azure::storage::table_result delete_result = table.execute(delete_operation);
```

## <a name="next-steps"></a><span data-ttu-id="2a958-202">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2a958-202">Next steps</span></span>
<span data-ttu-id="2a958-203">Agora que você aprendeu os conceitos básicos do armazenamento de tabela, siga estes links para saber mais sobre o Armazenamento do Azure:</span><span class="sxs-lookup"><span data-stu-id="2a958-203">Now that you've learned the basics of table storage, follow these links to learn more about Azure Storage:</span></span>  

* <span data-ttu-id="2a958-204">[O Gerenciador de Armazenamento do Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md) é um aplicativo autônomo e gratuito da Microsoft que possibilita o trabalho visual com os dados do Armazenamento do Azure no Windows, MacOS e Linux.</span><span class="sxs-lookup"><span data-stu-id="2a958-204">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you to work visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* [<span data-ttu-id="2a958-205">Como usar o armazenamento de Blob por meio do C++</span><span class="sxs-lookup"><span data-stu-id="2a958-205">How to use Blob storage from C++</span></span>](../storage/blobs/storage-c-plus-plus-how-to-use-blobs.md)
* [<span data-ttu-id="2a958-206">Como usar o armazenamento de Fila por meio do C++</span><span class="sxs-lookup"><span data-stu-id="2a958-206">How to use Queue storage from C++</span></span>](../storage/queues/storage-c-plus-plus-how-to-use-queues.md)
* [<span data-ttu-id="2a958-207">Listar recursos do Armazenamento do Azure no C++</span><span class="sxs-lookup"><span data-stu-id="2a958-207">List Azure Storage resources in C++</span></span>](../storage/common/storage-c-plus-plus-enumeration.md)
* [<span data-ttu-id="2a958-208">Referência da Biblioteca de Cliente de Armazenamento para C++</span><span class="sxs-lookup"><span data-stu-id="2a958-208">Storage Client Library for C++ reference</span></span>](http://azure.github.io/azure-storage-cpp)
* [<span data-ttu-id="2a958-209">Documentação do Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="2a958-209">Azure Storage documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)
