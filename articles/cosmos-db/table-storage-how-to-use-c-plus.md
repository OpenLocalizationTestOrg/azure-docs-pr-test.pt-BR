---
title: aaaHow toouse armazenamento de tabela (C++) | Microsoft Docs
description: "Armazene dados estruturados em nuvem hello usando o armazenamento de tabela do Azure, um repositório de dados NoSQL."
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
ms.openlocfilehash: 8096fe531427ba4858f7f4cb7f664f941892d1c9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-table-storage-from-c"></a><span data-ttu-id="effd5-103">Como toouse o armazenamento de tabela do C++</span><span class="sxs-lookup"><span data-stu-id="effd5-103">How toouse Table storage from C++</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a><span data-ttu-id="effd5-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="effd5-104">Overview</span></span>
<span data-ttu-id="effd5-105">Este guia mostrará como cenários comuns de tooperform usando Olá serviço de armazenamento de tabela do Azure.</span><span class="sxs-lookup"><span data-stu-id="effd5-105">This guide will show you how tooperform common scenarios by using hello Azure Table storage service.</span></span> <span data-ttu-id="effd5-106">exemplos de saudação são escritos em C++ e usam Olá [biblioteca de cliente de armazenamento do Azure para C++](https://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="effd5-106">hello samples are written in C++ and use hello [Azure Storage Client Library for C++](https://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span></span> <span data-ttu-id="effd5-107">Olá cenários abordados incluem **criação e exclusão de uma tabela** e **trabalhando com entidades de tabela**.</span><span class="sxs-lookup"><span data-stu-id="effd5-107">hello scenarios covered include **creating and deleting a table** and **working with table entities**.</span></span>

> [!NOTE]
> <span data-ttu-id="effd5-108">Destino dessa guia Olá biblioteca de cliente de armazenamento do Azure para a versão 1.0.0 de C++ e acima.</span><span class="sxs-lookup"><span data-stu-id="effd5-108">This guide targets hello Azure Storage Client Library for C++ version 1.0.0 and above.</span></span> <span data-ttu-id="effd5-109">Olá recomendado versão é a biblioteca de cliente de armazenamento 2.2.0, que está disponível por meio de [NuGet](http://www.nuget.org/packages/wastorage) ou [GitHub](https://github.com/Azure/azure-storage-cpp/).</span><span class="sxs-lookup"><span data-stu-id="effd5-109">hello recommended version is Storage Client Library 2.2.0, which is available via [NuGet](http://www.nuget.org/packages/wastorage) or [GitHub](https://github.com/Azure/azure-storage-cpp/).</span></span>
> 
> 

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-c-application"></a><span data-ttu-id="effd5-110">Criar um aplicativo em C++</span><span class="sxs-lookup"><span data-stu-id="effd5-110">Create a C++ application</span></span>
<span data-ttu-id="effd5-111">Neste guia, você usará os recursos de armazenamento que podem ser executados em um aplicativo do C++.</span><span class="sxs-lookup"><span data-stu-id="effd5-111">In this guide, you will use storage features that can be run within a C++ application.</span></span> <span data-ttu-id="effd5-112">toodo assim, você precisará tooinstall hello biblioteca de cliente de armazenamento do Azure para C++ e criar uma conta de armazenamento do Azure em sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="effd5-112">toodo so, you will need tooinstall hello Azure Storage Client Library for C++ and create an Azure storage account in your Azure subscription.</span></span>  

<span data-ttu-id="effd5-113">Olá tooinstall biblioteca de cliente de armazenamento do Azure para C++, você pode usar o hello métodos a seguir:</span><span class="sxs-lookup"><span data-stu-id="effd5-113">tooinstall hello Azure Storage Client Library for C++, you can use hello following methods:</span></span>

* <span data-ttu-id="effd5-114">**Linux:** siga instruções Olá fornecidas na Olá [biblioteca de cliente de armazenamento do Azure para C++ Leiame](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) página.</span><span class="sxs-lookup"><span data-stu-id="effd5-114">**Linux:** Follow hello instructions given on hello [Azure Storage Client Library for C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) page.</span></span>  
* <span data-ttu-id="effd5-115">**Windows:** no Visual Studio, clique em **Ferramentas > Gerenciador de Pacotes do NuGet > Console do Gerenciador de Pacotes**.</span><span class="sxs-lookup"><span data-stu-id="effd5-115">**Windows:** In Visual Studio, click **Tools > NuGet Package Manager > Package Manager Console**.</span></span> <span data-ttu-id="effd5-116">Digite o seguinte Olá comando em Olá [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) e pressione Enter.</span><span class="sxs-lookup"><span data-stu-id="effd5-116">Type hello following command into hello [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) and press Enter.</span></span>  
  
     <span data-ttu-id="effd5-117">Install-Package wastorage</span><span class="sxs-lookup"><span data-stu-id="effd5-117">Install-Package wastorage</span></span>

## <a name="configure-your-application-tooaccess-table-storage"></a><span data-ttu-id="effd5-118">Configurar seu aplicativo tooaccess armazenamento de tabela</span><span class="sxs-lookup"><span data-stu-id="effd5-118">Configure your application tooaccess Table storage</span></span>
<span data-ttu-id="effd5-119">Adicione a seguinte Olá incluem superior de toohello de instruções do arquivo de C++ de saudação onde você deseja que as tabelas de tooaccess APIs de armazenamento do Azure do toouse Olá:</span><span class="sxs-lookup"><span data-stu-id="effd5-119">Add hello following include statements toohello top of hello C++ file where you want toouse hello Azure storage APIs tooaccess tables:</span></span>  

```cpp
#include <was/storage_account.h>
#include <was/table.h>
```

## <a name="set-up-an-azure-storage-connection-string"></a><span data-ttu-id="effd5-120">Configurar uma cadeia de conexão de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="effd5-120">Set up an Azure storage connection string</span></span>
<span data-ttu-id="effd5-121">Um cliente de armazenamento do Azure usa um pontos de extremidade de toostore de cadeia de caracteres de conexão de armazenamento e as credenciais para acessar os serviços de gerenciamento de dados.</span><span class="sxs-lookup"><span data-stu-id="effd5-121">An Azure storage client uses a storage connection string toostore endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="effd5-122">Ao executar um aplicativo cliente, você deve fornecer a cadeia de conexão de armazenamento Olá no hello formato a seguir.</span><span class="sxs-lookup"><span data-stu-id="effd5-122">When running a client application, you must provide hello storage connection string in hello following format.</span></span> <span data-ttu-id="effd5-123">Use o nome da sua conta e hello armazenamento acesso chave de armazenamento para conta de armazenamento Olá Olá listados no hello [Portal do Azure](https://portal.azure.com) para Olá *AccountName* e *AccountKey* valores.</span><span class="sxs-lookup"><span data-stu-id="effd5-123">Use hello name of your storage account and hello storage access key for hello storage account listed in hello [Azure Portal](https://portal.azure.com) for hello *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="effd5-124">Para obter informações sobre as contas de armazenamento e as teclas de acesso, veja [Sobre as contas de armazenamento do Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="effd5-124">For information on storage accounts and access keys, see [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="effd5-125">Este exemplo mostra como você pode declarar uma cadeia de caracteres de conexão do campo estático toohold hello:</span><span class="sxs-lookup"><span data-stu-id="effd5-125">This example shows how you can declare a static field toohold hello connection string:</span></span>  

```cpp
// Define hello connection string with your values.
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

<span data-ttu-id="effd5-126">tootest seu aplicativo no seu computador local com base em Windows, você pode usar o hello Azure [emulador de armazenamento](../storage/common/storage-use-emulator.md) que é instalada com hello [SDK do Azure](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="effd5-126">tootest your application in your local Windows-based computer, you can use hello Azure [storage emulator](../storage/common/storage-use-emulator.md) that is installed with hello [Azure SDK](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="effd5-127">emulador de armazenamento Olá é um utilitário que simula hello Azure Blob, fila e tabela de serviços disponíveis no computador de desenvolvimento local.</span><span class="sxs-lookup"><span data-stu-id="effd5-127">hello storage emulator is a utility that simulates hello Azure Blob, Queue, and Table services available on your local development machine.</span></span> <span data-ttu-id="effd5-128">Olá exemplo a seguir mostra como você pode declarar um emulador de armazenamento local do campo estático toohold Olá cadeia de caracteres conexão tooyour:</span><span class="sxs-lookup"><span data-stu-id="effd5-128">hello following example shows how you can declare a static field toohold hello connection string tooyour local storage emulator:</span></span>  

```cpp
// Define hello connection string with Azure storage emulator.
const utility::string_t storage_connection_string(U("UseDevelopmentStorage=true;"));  
```

<span data-ttu-id="effd5-129">toostart Olá emulador de armazenamento do Azure, clique em Olá **iniciar** botão ou pressione tecla do Windows hello.</span><span class="sxs-lookup"><span data-stu-id="effd5-129">toostart hello Azure storage emulator, click hello **Start** button or press hello Windows key.</span></span> <span data-ttu-id="effd5-130">Comece digitando **emulador de armazenamento do Azure**e, em seguida, selecione **emulador de armazenamento do Microsoft Azure** da lista de saudação de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="effd5-130">Begin typing **Azure Storage Emulator**, and then select **Microsoft Azure Storage Emulator** from hello list of applications.</span></span>  

<span data-ttu-id="effd5-131">Olá exemplos a seguir pressupõem que você usou uma cadeia de conexão de armazenamento esses dois métodos tooget hello.</span><span class="sxs-lookup"><span data-stu-id="effd5-131">hello following samples assume that you have used one of these two methods tooget hello storage connection string.</span></span>  

## <a name="retrieve-your-connection-string"></a><span data-ttu-id="effd5-132">Recuperar sua cadeia de conexão</span><span class="sxs-lookup"><span data-stu-id="effd5-132">Retrieve your connection string</span></span>
<span data-ttu-id="effd5-133">Você pode usar o hello **cloud_storage_account** classe toorepresent suas informações de conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="effd5-133">You can use hello **cloud_storage_account** class toorepresent your storage account information.</span></span> <span data-ttu-id="effd5-134">tooretrieve informações de cadeia de caracteres de conexão de armazenamento Olá da conta de armazenamento, você pode usar o método de análise de saudação.</span><span class="sxs-lookup"><span data-stu-id="effd5-134">tooretrieve your storage account information from hello storage connection string, you can use hello parse method.</span></span>

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);
```

<span data-ttu-id="effd5-135">Em seguida, obtenha uma referência tooa **cloud_table_client** de classe, que permite que você obtenha os objetos de referência para tabelas e entidades armazenados em hello, o serviço de armazenamento de tabela.</span><span class="sxs-lookup"><span data-stu-id="effd5-135">Next, get a reference tooa **cloud_table_client** class, as it lets you get reference objects for tables and entities stored within hello Table storage service.</span></span> <span data-ttu-id="effd5-136">Olá código a seguir cria um **cloud_table_client** objeto usando o objeto de conta de armazenamento Olá recuperamos acima:</span><span class="sxs-lookup"><span data-stu-id="effd5-136">hello following code creates a **cloud_table_client** object by using hello storage account object we retrieved above:</span></span>  

```cpp
// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();
```

## <a name="create-a-table"></a><span data-ttu-id="effd5-137">Criar uma tabela</span><span class="sxs-lookup"><span data-stu-id="effd5-137">Create a table</span></span>
<span data-ttu-id="effd5-138">Um objeto **cloud_table_client** permite obter os objetos de referência para tabelas e entidades.</span><span class="sxs-lookup"><span data-stu-id="effd5-138">A **cloud_table_client** object lets you get reference objects for tables and entities.</span></span> <span data-ttu-id="effd5-139">Olá código a seguir cria um **cloud_table_client** do objeto e o utiliza toocreate uma nova tabela.</span><span class="sxs-lookup"><span data-stu-id="effd5-139">hello following code creates a **cloud_table_client** object and uses it toocreate a new table.</span></span>

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);  

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Retrieve a reference tooa table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create hello table if it doesn't exist.
table.create_if_not_exists();  
```

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="effd5-140">Adicionar uma tabela de entidade tooa</span><span class="sxs-lookup"><span data-stu-id="effd5-140">Add an entity tooa table</span></span>
<span data-ttu-id="effd5-141">tooadd uma tabela de tooa de entidade, crie um novo **table_entity** do objeto e passá-lo muito**table_operation:: insert_entity**.</span><span class="sxs-lookup"><span data-stu-id="effd5-141">tooadd an entity tooa table, create a new **table_entity** object and pass it too**table_operation::insert_entity**.</span></span> <span data-ttu-id="effd5-142">Olá código a seguir usa nome saudação do cliente como a chave de linha de saudação e último nome como chave de partição hello.</span><span class="sxs-lookup"><span data-stu-id="effd5-142">hello following code uses hello customer's first name as hello row key and last name as hello partition key.</span></span> <span data-ttu-id="effd5-143">Juntas, chave de linha e de partição da entidade identificam exclusivamente Olá entidade na tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="effd5-143">Together, an entity's partition and row key uniquely identify hello entity in hello table.</span></span> <span data-ttu-id="effd5-144">Entidades com hello a mesma chave de partição pode ser consultado mais rápido do que aquelas com diferentes chaves de partição, mas usar chaves de partição diversas permite maior escalabilidade de operação em paralelo.</span><span class="sxs-lookup"><span data-stu-id="effd5-144">Entities with hello same partition key can be queried faster than those with different partition keys, but using diverse partition keys allows for greater parallel operation scalability.</span></span> <span data-ttu-id="effd5-145">Para obter mais informações, veja [Lista de verificação de escalabilidade e desempenho do Armazenamento do Microsoft Azure](../storage/common/storage-performance-checklist.md).</span><span class="sxs-lookup"><span data-stu-id="effd5-145">For more information, see [Microsoft Azure storage performance and scalability checklist](../storage/common/storage-performance-checklist.md).</span></span>

<span data-ttu-id="effd5-146">Olá, código a seguir cria uma nova instância da **table_entity** com alguns toobe de dados do cliente armazenado.</span><span class="sxs-lookup"><span data-stu-id="effd5-146">hello following code creates a new instance of **table_entity** with some customer data toobe stored.</span></span> <span data-ttu-id="effd5-147">Olá chamadas próximas código **table_operation:: insert_entity** toocreate um **table_operation** tooinsert uma entidade do objeto em uma tabela, e associa Olá nova entidade de tabela com ele.</span><span class="sxs-lookup"><span data-stu-id="effd5-147">hello code next calls **table_operation::insert_entity** toocreate a **table_operation** object tooinsert an entity into a table, and associates hello new table entity with it.</span></span> <span data-ttu-id="effd5-148">Por fim, Olá chamadas de código Olá executar o método no hello **cloud_table** objeto.</span><span class="sxs-lookup"><span data-stu-id="effd5-148">Finally, hello code calls hello execute method on hello **cloud_table** object.</span></span> <span data-ttu-id="effd5-149">E hello novo **table_operation** envia uma solicitação toohello tabela tooinsert Olá novo cliente entidade de serviço na tabela de "people" hello.</span><span class="sxs-lookup"><span data-stu-id="effd5-149">And hello new **table_operation** sends a request toohello Table service tooinsert hello new customer entity into hello "people" table.</span></span>  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Retrieve a reference tooa table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create hello table if it doesn't exist.
table.create_if_not_exists();

// Create a new customer entity.
azure::storage::table_entity customer1(U("Harp"), U("Walter"));

azure::storage::table_entity::properties_type& properties = customer1.properties();
properties.reserve(2);
properties[U("Email")] = azure::storage::entity_property(U("Walter@contoso.com"));

properties[U("Phone")] = azure::storage::entity_property(U("425-555-0101"));

// Create hello table operation that inserts hello customer entity.
azure::storage::table_operation insert_operation = azure::storage::table_operation::insert_entity(customer1);

// Execute hello insert operation.
azure::storage::table_result insert_result = table.execute(insert_operation);
```

## <a name="insert-a-batch-of-entities"></a><span data-ttu-id="effd5-150">Inserir um lote de entidades</span><span class="sxs-lookup"><span data-stu-id="effd5-150">Insert a batch of entities</span></span>
<span data-ttu-id="effd5-151">Você pode inserir um lote de entidades toohello serviço de tabela em uma operação de gravação.</span><span class="sxs-lookup"><span data-stu-id="effd5-151">You can insert a batch of entities toohello Table service in one write operation.</span></span> <span data-ttu-id="effd5-152">Olá código a seguir cria um **table_batch_operation** de objeto e, em seguida, adiciona três tooit de operações de inserção.</span><span class="sxs-lookup"><span data-stu-id="effd5-152">hello following code creates a **table_batch_operation** object, and then adds three insert operations tooit.</span></span> <span data-ttu-id="effd5-153">Cada operação de inserção é adicionada ao criar um novo objeto de entidade, definir seus valores, e, em seguida, chamar hello Inserir método hello **table_batch_operation** entidade de saudação do objeto tooassociate com uma nova operação de inserção.</span><span class="sxs-lookup"><span data-stu-id="effd5-153">Each insert operation is added by creating a new entity object, setting its values, and then calling hello insert method on hello **table_batch_operation** object tooassociate hello entity with a new insert operation.</span></span> <span data-ttu-id="effd5-154">Em seguida, **cloud_table.execute** é chamado de operação de saudação tooexecute.</span><span class="sxs-lookup"><span data-stu-id="effd5-154">Then, **cloud_table.execute** is called tooexecute hello operation.</span></span>  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Define a batch operation.
azure::storage::table_batch_operation batch_operation;

// Create a customer entity and add it toohello table.
azure::storage::table_entity customer1(U("Smith"), U("Jeff"));

azure::storage::table_entity::properties_type& properties1 = customer1.properties();
properties1.reserve(2);
properties1[U("Email")] = azure::storage::entity_property(U("Jeff@contoso.com"));
properties1[U("Phone")] = azure::storage::entity_property(U("425-555-0104"));

// Create another customer entity and add it toohello table.
azure::storage::table_entity customer2(U("Smith"), U("Ben"));

azure::storage::table_entity::properties_type& properties2 = customer2.properties();
properties2.reserve(2);
properties2[U("Email")] = azure::storage::entity_property(U("Ben@contoso.com"));
properties2[U("Phone")] = azure::storage::entity_property(U("425-555-0102"));

// Create a third customer entity tooadd toohello table.
azure::storage::table_entity customer3(U("Smith"), U("Denise"));

azure::storage::table_entity::properties_type& properties3 = customer3.properties();
properties3.reserve(2);
properties3[U("Email")] = azure::storage::entity_property(U("Denise@contoso.com"));
properties3[U("Phone")] = azure::storage::entity_property(U("425-555-0103"));

// Add customer entities toohello batch insert operation.
batch_operation.insert_or_replace_entity(customer1);
batch_operation.insert_or_replace_entity(customer2);
batch_operation.insert_or_replace_entity(customer3);

// Execute hello batch operation.
std::vector<azure::storage::table_result> results = table.execute_batch(batch_operation);
```

<span data-ttu-id="effd5-155">Toonote algumas coisas em operações em lote:</span><span class="sxs-lookup"><span data-stu-id="effd5-155">Some things toonote on batch operations:</span></span>  

* <span data-ttu-id="effd5-156">Você pode executar os too100 insert, delete, merge, substituir, operações de inserção ou mesclagem e inserir ou substituir em qualquer combinação em um único lote.</span><span class="sxs-lookup"><span data-stu-id="effd5-156">You can perform up too100 insert, delete, merge, replace, insert-or-merge, and insert-or-replace operations in any combination in a single batch.</span></span>  
* <span data-ttu-id="effd5-157">Uma operação em lote pode ter uma operação de recuperação, se for a única operação Olá em lote de saudação.</span><span class="sxs-lookup"><span data-stu-id="effd5-157">A batch operation can have a retrieve operation, if it is hello only operation in hello batch.</span></span>  
* <span data-ttu-id="effd5-158">Todas as entidades em uma única operação de lote devem ter Olá mesma chave de partição.</span><span class="sxs-lookup"><span data-stu-id="effd5-158">All entities in a single batch operation must have hello same partition key.</span></span>  
* <span data-ttu-id="effd5-159">Uma operação em lote é limitada tooa carga de dados de 4 MB.</span><span class="sxs-lookup"><span data-stu-id="effd5-159">A batch operation is limited tooa 4-MB data payload.</span></span>  

## <a name="retrieve-all-entities-in-a-partition"></a><span data-ttu-id="effd5-160">Recuperar todas as entidades em uma partição</span><span class="sxs-lookup"><span data-stu-id="effd5-160">Retrieve all entities in a partition</span></span>
<span data-ttu-id="effd5-161">tooquery uma tabela para todas as entidades em uma partição, use um **table_query** objeto.</span><span class="sxs-lookup"><span data-stu-id="effd5-161">tooquery a table for all entities in a partition, use a **table_query** object.</span></span> <span data-ttu-id="effd5-162">Olá, exemplo de código a seguir especifica um filtro para entidades onde 'Smith' é a chave de partição hello.</span><span class="sxs-lookup"><span data-stu-id="effd5-162">hello following code example specifies a filter for entities where 'Smith' is hello partition key.</span></span> <span data-ttu-id="effd5-163">Este exemplo imprime campos de saudação de cada entidade no console de toohello de resultados de consulta de saudação.</span><span class="sxs-lookup"><span data-stu-id="effd5-163">This example prints hello fields of each entity in hello query results toohello console.</span></span>  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Construct hello query operation for all customer entities where PartitionKey="Smith".
azure::storage::table_query query;

query.set_filter_string(azure::storage::table_query::generate_filter_condition(U("PartitionKey"), azure::storage::query_comparison_operator::equal, U("Smith")));

// Execute hello query.
azure::storage::table_query_iterator it = table.execute_query(query);

// Print hello fields for each customer.
azure::storage::table_query_iterator end_of_results;
for (; it != end_of_results; ++it)
{
    const azure::storage::table_entity::properties_type& properties = it->properties();

    std::wcout << U("PartitionKey: ") << it->partition_key() << U(", RowKey: ") << it->row_key()
        << U(", Property1: ") << properties.at(U("Email")).string_value()
        << U(", Property2: ") << properties.at(U("Phone")).string_value() << std::endl;
}  
```

<span data-ttu-id="effd5-164">consulta neste exemplo Hello traz todas as entidades de saudação que correspondem aos critérios de filtro de saudação.</span><span class="sxs-lookup"><span data-stu-id="effd5-164">hello query in this example brings all hello entities that match hello filter criteria.</span></span> <span data-ttu-id="effd5-165">Se você tiver grandes tabelas e precisa de entidades de tabela toodownload Olá geralmente, é recomendável que você armazena seus dados em blobs de armazenamento do Azure em vez disso.</span><span class="sxs-lookup"><span data-stu-id="effd5-165">If you have large tables and need toodownload hello table entities often, we recommend that you store your data in Azure storage blobs instead.</span></span>

## <a name="retrieve-a-range-of-entities-in-a-partition"></a><span data-ttu-id="effd5-166">Recuperar um intervalo de entidades em uma partição</span><span class="sxs-lookup"><span data-stu-id="effd5-166">Retrieve a range of entities in a partition</span></span>
<span data-ttu-id="effd5-167">Se você não quiser tooquery todas as entidades de saudação em uma partição, você pode especificar um intervalo, combinando o filtro de chave de partição Olá com um filtro de linha de chave.</span><span class="sxs-lookup"><span data-stu-id="effd5-167">If you don't want tooquery all hello entities in a partition, you can specify a range by combining hello partition key filter with a row key filter.</span></span> <span data-ttu-id="effd5-168">Olá exemplo de código a seguir usa duas tooget de filtros todas as entidades na partição 'Smith' onde a chave de linha de saudação (nome) começa com uma letra anteriores E alfabeto hello e imprime os resultados da consulta hello.</span><span class="sxs-lookup"><span data-stu-id="effd5-168">hello following code example uses two filters tooget all entities in partition 'Smith' where hello row key (first name) starts with a letter earlier than 'E' in hello alphabet and then prints hello query results.</span></span>  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create hello table query.
azure::storage::table_query query;

query.set_filter_string(azure::storage::table_query::combine_filter_conditions(
    azure::storage::table_query::generate_filter_condition(U("PartitionKey"),
    azure::storage::query_comparison_operator::equal, U("Smith")),
    azure::storage::query_logical_operator::op_and,
    azure::storage::table_query::generate_filter_condition(U("RowKey"), azure::storage::query_comparison_operator::less_than, U("E"))));

// Execute hello query.
azure::storage::table_query_iterator it = table.execute_query(query);

// Loop through hello results, displaying information about hello entity.
azure::storage::table_query_iterator end_of_results;
for (; it != end_of_results; ++it)
{
    const azure::storage::table_entity::properties_type& properties = it->properties();

    std::wcout << U("PartitionKey: ") << it->partition_key() << U(", RowKey: ") << it->row_key()
        << U(", Property1: ") << properties.at(U("Email")).string_value()
        << U(", Property2: ") << properties.at(U("Phone")).string_value() << std::endl;
}  
```

## <a name="retrieve-a-single-entity"></a><span data-ttu-id="effd5-169">Recuperar uma única entidade</span><span class="sxs-lookup"><span data-stu-id="effd5-169">Retrieve a single entity</span></span>
<span data-ttu-id="effd5-170">Você pode escrever uma consulta tooretrieve uma entidade única e específica.</span><span class="sxs-lookup"><span data-stu-id="effd5-170">You can write a query tooretrieve a single, specific entity.</span></span> <span data-ttu-id="effd5-171">código a seguir Olá usa **table_operation:: retrieve_entity** toospecify Prezado cliente 'Jeff Smith'.</span><span class="sxs-lookup"><span data-stu-id="effd5-171">hello following code uses **table_operation::retrieve_entity** toospecify hello customer 'Jeff Smith'.</span></span> <span data-ttu-id="effd5-172">Esse método retorna uma única entidade, em vez de uma coleção e hello valor retornado está na **table_result**.</span><span class="sxs-lookup"><span data-stu-id="effd5-172">This method returns just one entity, rather than a collection, and hello returned value is in **table_result**.</span></span> <span data-ttu-id="effd5-173">Especificar chaves de partição e de linha em uma consulta é tooretrieve de maneira mais rápida de Olá uma única entidade de serviço de tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="effd5-173">Specifying both partition and row keys in a query is hello fastest way tooretrieve a single entity from hello Table service.</span></span>  

```cpp
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Retrieve hello entity with partition key of "Smith" and row key of "Jeff".
azure::storage::table_operation retrieve_operation = azure::storage::table_operation::retrieve_entity(U("Smith"), U("Jeff"));
azure::storage::table_result retrieve_result = table.execute(retrieve_operation);

// Output hello entity.
azure::storage::table_entity entity = retrieve_result.entity();
const azure::storage::table_entity::properties_type& properties = entity.properties();

std::wcout << U("PartitionKey: ") << entity.partition_key() << U(", RowKey: ") << entity.row_key()
    << U(", Property1: ") << properties.at(U("Email")).string_value()
    << U(", Property2: ") << properties.at(U("Phone")).string_value() << std::endl;
```

## <a name="replace-an-entity"></a><span data-ttu-id="effd5-174">Substituir uma entidade</span><span class="sxs-lookup"><span data-stu-id="effd5-174">Replace an entity</span></span>
<span data-ttu-id="effd5-175">tooreplace uma entidade, recuperá-lo do serviço de tabela hello, modificar o objeto de entidade hello e, em seguida, salvar as alterações de saudação fazer toohello serviço de tabela.</span><span class="sxs-lookup"><span data-stu-id="effd5-175">tooreplace an entity, retrieve it from hello Table service, modify hello entity object, and then save hello changes back toohello Table service.</span></span> <span data-ttu-id="effd5-176">Olá código a seguir altera telefone e endereço de um cliente existente de email.</span><span class="sxs-lookup"><span data-stu-id="effd5-176">hello following code changes an existing customer's phone number and email address.</span></span> <span data-ttu-id="effd5-177">Em vez de chamar **table_operation::insert_entity**y, esse código usa **table_operation::replace_entity**.</span><span class="sxs-lookup"><span data-stu-id="effd5-177">Instead of calling **table_operation::insert_entity**, this code uses **table_operation::replace_entity**.</span></span> <span data-ttu-id="effd5-178">Isso faz com que Olá entidade toobe totalmente substituído no servidor de saudação, a menos que a entidade Olá no servidor de saudação foi alterado desde que foi recuperada, caso em que haverá falha na operação de saudação.</span><span class="sxs-lookup"><span data-stu-id="effd5-178">This causes hello entity toobe fully replaced on hello server, unless hello entity on hello server has changed since it was retrieved, in which case hello operation will fail.</span></span> <span data-ttu-id="effd5-179">Essa falha é tooprevent seu aplicativo substitua inadvertidamente uma alteração feita entre Olá recuperação e atualizar por outro componente do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="effd5-179">This failure is tooprevent your application from inadvertently overwriting a change made between hello retrieval and update by another component of your application.</span></span> <span data-ttu-id="effd5-180">Hello manipulação adequada dessa falha é tooretrieve Olá entidade novamente, faça as alterações (se ainda é válida) e, em seguida, executar outro **table_operation:: replace_entity** operação.</span><span class="sxs-lookup"><span data-stu-id="effd5-180">hello proper handling of this failure is tooretrieve hello entity again, make your changes (if still valid), and then perform another **table_operation::replace_entity** operation.</span></span> <span data-ttu-id="effd5-181">Olá próxima seção lhe mostrará como toooverride esse comportamento.</span><span class="sxs-lookup"><span data-stu-id="effd5-181">hello next section will show you how toooverride this behavior.</span></span>  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Replace an entity.
azure::storage::table_entity entity_to_replace(U("Smith"), U("Jeff"));
azure::storage::table_entity::properties_type& properties_to_replace = entity_to_replace.properties();
properties_to_replace.reserve(2);

// Specify a new phone number.
properties_to_replace[U("Phone")] = azure::storage::entity_property(U("425-555-0106"));

// Specify a new email address.
properties_to_replace[U("Email")] = azure::storage::entity_property(U("JeffS@contoso.com"));

// Create an operation tooreplace hello entity.
azure::storage::table_operation replace_operation = azure::storage::table_operation::replace_entity(entity_to_replace);

// Submit hello operation toohello Table service.
azure::storage::table_result replace_result = table.execute(replace_operation);
```

## <a name="insert-or-replace-an-entity"></a><span data-ttu-id="effd5-182">Inserir ou substituir uma entidade</span><span class="sxs-lookup"><span data-stu-id="effd5-182">Insert-or-replace an entity</span></span>
<span data-ttu-id="effd5-183">**table_operation:: replace_entity** operações falharão se a entidade de saudação foi alterada desde que foi recuperada do servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="effd5-183">**table_operation::replace_entity** operations will fail if hello entity has been changed since it was retrieved from hello server.</span></span> <span data-ttu-id="effd5-184">Além disso, você deve recuperar a entidade de saudação do servidor de saudação primeiro na ordem de **table_operation:: replace_entity** toobe com êxito.</span><span class="sxs-lookup"><span data-stu-id="effd5-184">Furthermore, you must retrieve hello entity from hello server first in order for **table_operation::replace_entity** toobe successful.</span></span> <span data-ttu-id="effd5-185">Às vezes, no entanto, você não souber se a entidade Olá existe no servidor de saudação e valores atuais de saudação armazenados nela são irrelevantes — a atualização deve substituir todos eles.</span><span class="sxs-lookup"><span data-stu-id="effd5-185">Sometimes, however, you don't know if hello entity exists on hello server and hello current values stored in it are irrelevant—your update should overwrite them all.</span></span> <span data-ttu-id="effd5-186">tooaccomplish isso, você usaria uma **table_operation:: insert_or_replace_entity** operação.</span><span class="sxs-lookup"><span data-stu-id="effd5-186">tooaccomplish this, you would use a **table_operation::insert_or_replace_entity** operation.</span></span> <span data-ttu-id="effd5-187">Essa operação insere a entidade de saudação se ele não existe ou substitui-lo em caso afirmativo, independentemente de quando Olá última atualização foi feita.</span><span class="sxs-lookup"><span data-stu-id="effd5-187">This operation inserts hello entity if it doesn't exist, or replaces it if it does, regardless of when hello last update was made.</span></span> <span data-ttu-id="effd5-188">Em Olá exemplo de código a seguir, entidade customer de saudação de Jeff Smith ainda é recuperada, mas, em seguida, ele será salvo toohello back servidor via **table_operation:: insert_or_replace_entity**.</span><span class="sxs-lookup"><span data-stu-id="effd5-188">In hello following code example, hello customer entity for Jeff Smith is still retrieved, but it is then saved back toohello server via **table_operation::insert_or_replace_entity**.</span></span> <span data-ttu-id="effd5-189">Todas as atualizações feitas toohello entidade entre as operações de recuperação e atualização de saudação serão substituídas.</span><span class="sxs-lookup"><span data-stu-id="effd5-189">Any updates made toohello entity between hello retrieval and update operation will be overwritten.</span></span>  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Insert-or-replace an entity.
azure::storage::table_entity entity_to_insert_or_replace(U("Smith"), U("Jeff"));
azure::storage::table_entity::properties_type& properties_to_insert_or_replace = entity_to_insert_or_replace.properties();

properties_to_insert_or_replace.reserve(2);

// Specify a phone number.
properties_to_insert_or_replace[U("Phone")] = azure::storage::entity_property(U("425-555-0107"));

// Specify an email address.
properties_to_insert_or_replace[U("Email")] = azure::storage::entity_property(U("Jeffsm@contoso.com"));

// Create an operation tooinsert-or-replace hello entity.
azure::storage::table_operation insert_or_replace_operation = azure::storage::table_operation::insert_or_replace_entity(entity_to_insert_or_replace);

// Submit hello operation toohello Table service.
azure::storage::table_result insert_or_replace_result = table.execute(insert_or_replace_operation);
```

## <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="effd5-190">consultar um subconjunto de propriedades da entidade</span><span class="sxs-lookup"><span data-stu-id="effd5-190">Query a subset of entity properties</span></span>
<span data-ttu-id="effd5-191">Uma tabela de consulta tooa pode recuperar apenas algumas propriedades de uma entidade.</span><span class="sxs-lookup"><span data-stu-id="effd5-191">A query tooa table can retrieve just a few properties from an entity.</span></span> <span data-ttu-id="effd5-192">Olá, consulta em Olá código a seguir usa Olá **table_query:: set_select_columns** método tooreturn somente Olá endereços de email de entidades na tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="effd5-192">hello query in hello following code uses hello **table_query::set_select_columns** method tooreturn only hello email addresses of entities in hello table.</span></span>  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Define hello query, and select only hello Email property.
azure::storage::table_query query;
std::vector<utility::string_t> columns;

columns.push_back(U("Email"));
query.set_select_columns(columns);

// Execute hello query.
azure::storage::table_query_iterator it = table.execute_query(query);

// Display hello results.
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
> <span data-ttu-id="effd5-193">Consultar algumas propriedades de uma entidade é uma operação mais eficiente do que recuperar todas as propriedades.</span><span class="sxs-lookup"><span data-stu-id="effd5-193">Querying a few properties from an entity is a more efficient operation than retrieving all properties.</span></span>
> 
> 

## <a name="delete-an-entity"></a><span data-ttu-id="effd5-194">Excluir uma entidade</span><span class="sxs-lookup"><span data-stu-id="effd5-194">Delete an entity</span></span>
<span data-ttu-id="effd5-195">Você poderá excluir uma entidade facilmente depois que recuperá-la.</span><span class="sxs-lookup"><span data-stu-id="effd5-195">You can easily delete an entity after you have retrieved it.</span></span> <span data-ttu-id="effd5-196">Depois que a entidade de saudação é recuperada, chamar **table_operation:: delete_entity** com hello toodelete de entidade.</span><span class="sxs-lookup"><span data-stu-id="effd5-196">Once hello entity is retrieved, call **table_operation::delete_entity** with hello entity toodelete.</span></span> <span data-ttu-id="effd5-197">Em seguida, chamar hello **cloud_table.execute** método.</span><span class="sxs-lookup"><span data-stu-id="effd5-197">Then call hello **cloud_table.execute** method.</span></span> <span data-ttu-id="effd5-198">Olá código a seguir recupera e exclui uma entidade com uma chave de partição de "Smith" e uma chave de linha de "Jeff".</span><span class="sxs-lookup"><span data-stu-id="effd5-198">hello following code retrieves and deletes an entity with a partition key of "Smith" and a row key of "Jeff".</span></span>  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create an operation tooretrieve hello entity with partition key of "Smith" and row key of "Jeff".
azure::storage::table_operation retrieve_operation = azure::storage::table_operation::retrieve_entity(U("Smith"), U("Jeff"));
azure::storage::table_result retrieve_result = table.execute(retrieve_operation);

// Create an operation toodelete hello entity.
azure::storage::table_operation delete_operation = azure::storage::table_operation::delete_entity(retrieve_result.entity());

// Submit hello delete operation toohello Table service.
azure::storage::table_result delete_result = table.execute(delete_operation);  
```

## <a name="delete-a-table"></a><span data-ttu-id="effd5-199">Excluir uma tabela</span><span class="sxs-lookup"><span data-stu-id="effd5-199">Delete a table</span></span>
<span data-ttu-id="effd5-200">Por fim, Olá exemplo de código a seguir exclui uma tabela de uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="effd5-200">Finally, hello following code example deletes a table from a storage account.</span></span> <span data-ttu-id="effd5-201">Uma tabela que tenha sido excluída será toobe indisponível recriado por um período de tempo após a exclusão de saudação.</span><span class="sxs-lookup"><span data-stu-id="effd5-201">A table that has been deleted will be unavailable toobe re-created for a period of time following hello deletion.</span></span>  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create an operation tooretrieve hello entity with partition key of "Smith" and row key of "Jeff".
azure::storage::table_operation retrieve_operation = azure::storage::table_operation::retrieve_entity(U("Smith"), U("Jeff"));
azure::storage::table_result retrieve_result = table.execute(retrieve_operation);

// Create an operation toodelete hello entity.
azure::storage::table_operation delete_operation = azure::storage::table_operation::delete_entity(retrieve_result.entity());

// Submit hello delete operation toohello Table service.
azure::storage::table_result delete_result = table.execute(delete_operation);
```

## <a name="next-steps"></a><span data-ttu-id="effd5-202">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="effd5-202">Next steps</span></span>
<span data-ttu-id="effd5-203">Agora que você aprendeu as Noções básicas de saudação do armazenamento de tabela, siga essas toolearn links mais sobre o armazenamento do Azure:</span><span class="sxs-lookup"><span data-stu-id="effd5-203">Now that you've learned hello basics of table storage, follow these links toolearn more about Azure Storage:</span></span>  

* <span data-ttu-id="effd5-204">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) é um aplicativo autônomo gratuito da Microsoft que permite que você toowork visualmente com dados de armazenamento do Azure no Linux, Windows e macOS.</span><span class="sxs-lookup"><span data-stu-id="effd5-204">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you toowork visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* [<span data-ttu-id="effd5-205">Como toouse armazenamento de Blob de C++</span><span class="sxs-lookup"><span data-stu-id="effd5-205">How toouse Blob storage from C++</span></span>](../storage/blobs/storage-c-plus-plus-how-to-use-blobs.md)
* [<span data-ttu-id="effd5-206">Como toouse armazenamento de fila de C++</span><span class="sxs-lookup"><span data-stu-id="effd5-206">How toouse Queue storage from C++</span></span>](../storage/queues/storage-c-plus-plus-how-to-use-queues.md)
* [<span data-ttu-id="effd5-207">Listar recursos do Armazenamento do Azure no C++</span><span class="sxs-lookup"><span data-stu-id="effd5-207">List Azure Storage resources in C++</span></span>](../storage/common/storage-c-plus-plus-enumeration.md)
* [<span data-ttu-id="effd5-208">Referência da Biblioteca de Cliente de Armazenamento para C++</span><span class="sxs-lookup"><span data-stu-id="effd5-208">Storage Client Library for C++ reference</span></span>](http://azure.github.io/azure-storage-cpp)
* [<span data-ttu-id="effd5-209">Documentação do Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="effd5-209">Azure Storage documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)
