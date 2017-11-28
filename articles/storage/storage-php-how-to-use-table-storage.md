---
title: Como usar o armazenamento de tabelas do PHP | Microsoft Docs
description: "Saiba como usar o serviço Tabela do PHP para criar e excluir tabelas e inserir, excluir e consultar a tabela."
services: storage
documentationcenter: php
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 1e57f371-6208-4753-b2a0-05db4aede8e3
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: php
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: 15d3216ef5bb1d7ff312bd886837a3a7b0335afd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-table-storage-from-php"></a><span data-ttu-id="eba20-103">Como usar o armazenamento de tabela do PHP</span><span class="sxs-lookup"><span data-stu-id="eba20-103">How to use table storage from PHP</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a><span data-ttu-id="eba20-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="eba20-104">Overview</span></span>
<span data-ttu-id="eba20-105">Este guia mostra como executar cenários comuns usando o serviço Tabela do Azure.</span><span class="sxs-lookup"><span data-stu-id="eba20-105">This guide shows you how to perform common scenarios using the Azure Table service.</span></span> <span data-ttu-id="eba20-106">As amostras são escritas em PHP e usam o [SDK do Azure para PHP][download].</span><span class="sxs-lookup"><span data-stu-id="eba20-106">The samples are written in PHP and use the [Azure SDK for PHP][download].</span></span> <span data-ttu-id="eba20-107">Os cenários abrangidos incluem **criar e excluir uma tabela, e inserir, excluir e consultar entidades em uma tabela**.</span><span class="sxs-lookup"><span data-stu-id="eba20-107">The scenarios covered include **creating and deleting a table, and inserting, deleting, and querying entities in a table**.</span></span> <span data-ttu-id="eba20-108">Para obter mais informações sobre o serviço Tabela do Azure, consulte a seção [Próximas etapas](#next-steps) .</span><span class="sxs-lookup"><span data-stu-id="eba20-108">For more information on the Azure Table service, see the [Next steps](#next-steps) section.</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="eba20-109">Criar um aplicativo PHP</span><span class="sxs-lookup"><span data-stu-id="eba20-109">Create a PHP application</span></span>
<span data-ttu-id="eba20-110">O único requisito para a criação de um aplicativo PHP que acessa o serviço de Tabela do Azure é a referência das classes no SDK do Azure para PHP de dentro de seu código.</span><span class="sxs-lookup"><span data-stu-id="eba20-110">The only requirement for creating a PHP application that accesses the Azure Table service is the referencing of classes in the Azure SDK for PHP from within your code.</span></span> <span data-ttu-id="eba20-111">Você pode usar as ferramentas de desenvolvimento para criar seu aplicativo, incluindo o bloco de notas.</span><span class="sxs-lookup"><span data-stu-id="eba20-111">You can use any development tools to create your application, including Notepad.</span></span>

<span data-ttu-id="eba20-112">Neste guia, você usa os recursos de serviço Tabela que podem ser chamados de dentro de um aplicativo PHP localmente ou no código em execução dentro de um site, função de trabalho ou função web do Azure.</span><span class="sxs-lookup"><span data-stu-id="eba20-112">In this guide, you use Table service features which can be called from within a PHP application locally, or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-the-azure-client-libraries"></a><span data-ttu-id="eba20-113">Obter as bibliotecas de cliente do Azure</span><span class="sxs-lookup"><span data-stu-id="eba20-113">Get the Azure Client Libraries</span></span>
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-to-access-the-table-service"></a><span data-ttu-id="eba20-114">Configurar seu aplicativo para acessar o serviço de Tabela</span><span class="sxs-lookup"><span data-stu-id="eba20-114">Configure your application to access the Table service</span></span>
<span data-ttu-id="eba20-115">Para usar as APIs do serviço Tabela do Azure, você precisa:</span><span class="sxs-lookup"><span data-stu-id="eba20-115">To use the Azure Table service APIs, you need to:</span></span>

1. <span data-ttu-id="eba20-116">Fazer referência ao arquivo de carregador automático usando a instrução [require_once][require_once] e</span><span class="sxs-lookup"><span data-stu-id="eba20-116">Reference the autoloader file using the [require_once][require_once] statement, and</span></span>
2. <span data-ttu-id="eba20-117">Fazer referência a qualquer classe que você possa usar.</span><span class="sxs-lookup"><span data-stu-id="eba20-117">Reference any classes you might use.</span></span>

<span data-ttu-id="eba20-118">O exemplo a seguir mostra como incluir o arquivo de carregador automático e fazer referência à classe **ServicesBuilder** .</span><span class="sxs-lookup"><span data-stu-id="eba20-118">The following example shows how to include the autoloader file and reference the **ServicesBuilder** class.</span></span>

> [!NOTE]
> <span data-ttu-id="eba20-119">Os exemplos deste artigo pressupõem que você tenha instalado as Bibliotecas de Cliente do PHP para o Azure por meio do Criador.</span><span class="sxs-lookup"><span data-stu-id="eba20-119">The examples in this article assume you have installed the PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="eba20-120">Se tiver instalado as bibliotecas manualmente, você precisará fazer referência ao arquivo de carregador automático <code>WindowsAzure.php</code> .</span><span class="sxs-lookup"><span data-stu-id="eba20-120">If you installed the libraries manually, you need to reference the <code>WindowsAzure.php</code> autoloader file.</span></span>
>
>

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

<span data-ttu-id="eba20-121">Nos exemplos abaixo, a instrução `require_once` é mostrada sempre, mas somente as classes necessárias para executar o exemplo são referenciadas.</span><span class="sxs-lookup"><span data-stu-id="eba20-121">In the examples below, the `require_once` statement is always shown, but only the classes necessary for the example to execute are referenced.</span></span>

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="eba20-122">Configurar uma conexão de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="eba20-122">Set up an Azure storage connection</span></span>
<span data-ttu-id="eba20-123">Para criar uma instância de um cliente de serviço Tabela do Azure, você deve primeiramente ter uma cadeia de conexão válida.</span><span class="sxs-lookup"><span data-stu-id="eba20-123">To instantiate an Azure Table service client, you must first have a valid connection string.</span></span> <span data-ttu-id="eba20-124">O formato da cadeia de conexão do serviço Tabela é:</span><span class="sxs-lookup"><span data-stu-id="eba20-124">The format for the Table service connection string is:</span></span>

<span data-ttu-id="eba20-125">Para acessar um serviço ao vivo:</span><span class="sxs-lookup"><span data-stu-id="eba20-125">For accessing a live service:</span></span>

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

<span data-ttu-id="eba20-126">Para acessar o armazenamento do emulador:</span><span class="sxs-lookup"><span data-stu-id="eba20-126">For accessing the emulator storage:</span></span>

```php
UseDevelopmentStorage=true
```

<span data-ttu-id="eba20-127">Para criar qualquer cliente de serviço do Azure, é necessário usar a classe **ServicesBuilder** .</span><span class="sxs-lookup"><span data-stu-id="eba20-127">To create any Azure service client, you need to use the **ServicesBuilder** class.</span></span> <span data-ttu-id="eba20-128">Você pode:</span><span class="sxs-lookup"><span data-stu-id="eba20-128">You can:</span></span>

* <span data-ttu-id="eba20-129">passar a cadeia de conexão diretamente para ele ou</span><span class="sxs-lookup"><span data-stu-id="eba20-129">pass the connection string directly to it or</span></span>
* <span data-ttu-id="eba20-130">usar **CloudConfigurationManager (CCM)** para verificar várias fontes externas da cadeia de conexão:</span><span class="sxs-lookup"><span data-stu-id="eba20-130">use the **CloudConfigurationManager (CCM)** to check multiple external sources for the connection string:</span></span>
  * <span data-ttu-id="eba20-131">por padrão, ele é fornecido com suporte para uma fonte externa – variáveis de ambiente.</span><span class="sxs-lookup"><span data-stu-id="eba20-131">by default, it comes with support for one external source - environmental variables</span></span>
  * <span data-ttu-id="eba20-132">você pode adicionar novas origens ao estender a classe **ConnectionStringSource**</span><span class="sxs-lookup"><span data-stu-id="eba20-132">you can add new sources by extending the **ConnectionStringSource** class</span></span>

<span data-ttu-id="eba20-133">Para os exemplos descritos aqui, a cadeia de conexão será passada diretamente.</span><span class="sxs-lookup"><span data-stu-id="eba20-133">For the examples outlined here, the connection string will be passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);
```

## <a name="create-a-table"></a><span data-ttu-id="eba20-134">Criar uma tabela</span><span class="sxs-lookup"><span data-stu-id="eba20-134">Create a table</span></span>
<span data-ttu-id="eba20-135">O objeto **TableRestProxy** permite que você crie uma tabela com o método **createTable**.</span><span class="sxs-lookup"><span data-stu-id="eba20-135">A **TableRestProxy** object lets you create a table with the **createTable** method.</span></span> <span data-ttu-id="eba20-136">Ao criar uma tabela, você pode definir o tempo limite do serviço Tabela.</span><span class="sxs-lookup"><span data-stu-id="eba20-136">When creating a table, you can set the Table service timeout.</span></span> <span data-ttu-id="eba20-137">(Para obter mais informações sobre o tempo limite do serviço Tabela, consulte [Setting Timeouts for Table Service Operations][table-service-timeouts] [Definindo tempos limite para operações do serviço Tabela.])</span><span class="sxs-lookup"><span data-stu-id="eba20-137">(For more information about the Table service timeout, see [Setting Timeouts for Table Service Operations][table-service-timeouts].)</span></span>

```php
require_once 'vendor\autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

try    {
    // Create table.
    $tableRestProxy->createTable("mytable");
}
catch(ServiceException $e){
    $code = $e->getCode();
    $error_message = $e->getMessage();
    // Handle exception based on error codes and messages.
    // Error codes and messages can be found here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
}
```

<span data-ttu-id="eba20-138">Para obter informações sobre restrições em nomes de tabela, consulte [Understanding the Table Service Data Model][table-data-model] (Noções básicas sobre o modelo de dados do serviço Tabela).</span><span class="sxs-lookup"><span data-stu-id="eba20-138">For information about restrictions on table names, see [Understanding the Table Service Data Model][table-data-model].</span></span>

## <a name="add-an-entity-to-a-table"></a><span data-ttu-id="eba20-139">Adicionar uma entidade a uma tabela</span><span class="sxs-lookup"><span data-stu-id="eba20-139">Add an entity to a table</span></span>
<span data-ttu-id="eba20-140">Para adicionar uma entidade a uma tabela, crie um novo objeto **Entidade** e passá-lo para **TableRestProxy->insertEntity**.</span><span class="sxs-lookup"><span data-stu-id="eba20-140">To add an entity to a table, create a new **Entity** object and pass it to **TableRestProxy->insertEntity**.</span></span> <span data-ttu-id="eba20-141">Observe que ao criar uma entidade, você deve especificar um `PartitionKey` e `RowKey`.</span><span class="sxs-lookup"><span data-stu-id="eba20-141">Note that when you create an entity, you must specify a `PartitionKey` and `RowKey`.</span></span> <span data-ttu-id="eba20-142">Estes são os identificadores exclusivos para uma entidade e são os valores que podem ser consultados muito mais rápido que as outras propriedades da entidade.</span><span class="sxs-lookup"><span data-stu-id="eba20-142">These are the unique identifiers for an entity and are values that can be queried much faster than other entity properties.</span></span> <span data-ttu-id="eba20-143">O sistema usa `PartitionKey` para distribuir automaticamente as entidades das tabelas por vários nós de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="eba20-143">The system uses `PartitionKey` to automatically distribute the table's entities over many storage nodes.</span></span> <span data-ttu-id="eba20-144">As entidades com a mesma `PartitionKey` são armazenadas no mesmo nó.</span><span class="sxs-lookup"><span data-stu-id="eba20-144">Entities with the same `PartitionKey` are stored on the same node.</span></span> <span data-ttu-id="eba20-145">(As operações em várias entidades armazenadas no mesmo nó são executadas melhor do que em entidades armazenadas em nós diferentes.) `RowKey` é a ID exclusiva de uma entidade dentro de uma partição.</span><span class="sxs-lookup"><span data-stu-id="eba20-145">(Operations on multiple entities stored on the same node perform better than on entities stored across different nodes.) The `RowKey` is the unique ID of an entity within a partition.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Table\Models\Entity;
use MicrosoftAzure\Storage\Table\Models\EdmType;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

$entity = new Entity();
$entity->setPartitionKey("tasksSeattle");
$entity->setRowKey("1");
$entity->addProperty("Description", null, "Take out the trash.");
$entity->addProperty("DueDate",
                        EdmType::DATETIME,
                        new DateTime("2012-11-05T08:15:00-08:00"));
$entity->addProperty("Location", EdmType::STRING, "Home");

try{
    $tableRestProxy->insertEntity("mytable", $entity);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
}
```

<span data-ttu-id="eba20-146">Para obter informações sobre tipos e propriedades de Tabela, consulte [Understanding the Table Service Data Model][table-data-model] (Noções básicas sobre o modelo de dados do serviço Tabela).</span><span class="sxs-lookup"><span data-stu-id="eba20-146">For information about Table properties and types, see [Understanding the Table Service Data Model][table-data-model].</span></span>

<span data-ttu-id="eba20-147">A classe **TableRestProxy** oferece dois métodos alternativos para inserir entidades: **insertOrMergeEntity** e **insertOrReplaceEntity**.</span><span class="sxs-lookup"><span data-stu-id="eba20-147">The **TableRestProxy** class offers two alternative methods for inserting entities: **insertOrMergeEntity** and **insertOrReplaceEntity**.</span></span> <span data-ttu-id="eba20-148">Para usar esses métodos, crie uma nova **Entidade** e passe-a como um parâmetro para qualquer método.</span><span class="sxs-lookup"><span data-stu-id="eba20-148">To use these methods, create a new **Entity** and pass it as a parameter to either method.</span></span> <span data-ttu-id="eba20-149">Cada método vai inserir a entidade se ela não existir.</span><span class="sxs-lookup"><span data-stu-id="eba20-149">Each method will insert the entity if it does not exist.</span></span> <span data-ttu-id="eba20-150">Se a entidade já existir, **insertOrMergeEntity** atualiza os valores de propriedade se as propriedades já existirem e adiciona novas propriedades se elas não existirem, enquanto **insertOrReplaceEntity** substitui completamente uma entidade existente.</span><span class="sxs-lookup"><span data-stu-id="eba20-150">If the entity already exists, **insertOrMergeEntity** updates property values if the properties already exist and adds new properties if they do not exist, while **insertOrReplaceEntity** completely replaces an existing entity.</span></span> <span data-ttu-id="eba20-151">O exemplo a seguir mostra como usar o **insertOrMergeEntity**.</span><span class="sxs-lookup"><span data-stu-id="eba20-151">The following example shows how to use **insertOrMergeEntity**.</span></span> <span data-ttu-id="eba20-152">Se a entidade com `PartitionKey` "tasksSeattle" e `RowKey` "1" ainda não existir, ela será inserida.</span><span class="sxs-lookup"><span data-stu-id="eba20-152">If the entity with `PartitionKey` "tasksSeattle" and `RowKey` "1" does not already exist, it will be inserted.</span></span> <span data-ttu-id="eba20-153">No entanto, se ela tiver sido inserida anteriormente (conforme mostrado no exemplo acima), a propriedade `DueDate` será atualizada e a propriedade `Status` será adicionada.</span><span class="sxs-lookup"><span data-stu-id="eba20-153">However, if it has previously been inserted (as shown in the example above), the `DueDate` property will be updated, and the `Status` property will be added.</span></span> <span data-ttu-id="eba20-154">As propriedades `Description` e `Location` também são atualizadas, mas com valores que efetivamente as deixam inalteradas.</span><span class="sxs-lookup"><span data-stu-id="eba20-154">The `Description` and `Location` properties are also updated, but with values that effectively leave them unchanged.</span></span> <span data-ttu-id="eba20-155">Se essas duas últimas propriedades não foram adicionadas conforme mostrado no exemplo, mas existiam na entidade de destino, seus valores existentes permaneceriam inalterados.</span><span class="sxs-lookup"><span data-stu-id="eba20-155">If these latter two properties were not added as shown in the example, but existed on the target entity, their existing values would remain unchanged.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Table\Models\Entity;
use MicrosoftAzure\Storage\Table\Models\EdmType;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

//Create new entity.
$entity = new Entity();

// PartitionKey and RowKey are required.
$entity->setPartitionKey("tasksSeattle");
$entity->setRowKey("1");

// If entity exists, existing properties are updated with new values and
// new properties are added. Missing properties are unchanged.
$entity->addProperty("Description", null, "Take out the trash.");
$entity->addProperty("DueDate", EdmType::DATETIME, new DateTime()); // Modified the DueDate field.
$entity->addProperty("Location", EdmType::STRING, "Home");
$entity->addProperty("Status", EdmType::STRING, "Complete"); // Added Status field.

try    {
    // Calling insertOrReplaceEntity, instead of insertOrMergeEntity as shown,
    // would simply replace the entity with PartitionKey "tasksSeattle" and RowKey "1".
    $tableRestProxy->insertOrMergeEntity("mytable", $entity);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="retrieve-a-single-entity"></a><span data-ttu-id="eba20-156">Recuperar uma única entidade</span><span class="sxs-lookup"><span data-stu-id="eba20-156">Retrieve a single entity</span></span>
<span data-ttu-id="eba20-157">O método **TableRestProxy->getEntity** permite que você recupere uma única entidade consultando seu `PartitionKey` e `RowKey`.</span><span class="sxs-lookup"><span data-stu-id="eba20-157">The **TableRestProxy->getEntity** method allows you to retrieve a single entity by querying for its `PartitionKey` and `RowKey`.</span></span> <span data-ttu-id="eba20-158">No exemplo abaixo, a chave da partição `tasksSeattle` e a chave de linha `1` são passadas para o método **getEntity**.</span><span class="sxs-lookup"><span data-stu-id="eba20-158">In the example below, the partition key `tasksSeattle` and row key `1` are passed to the **getEntity** method.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

try    {
    $result = $tableRestProxy->getEntity("mytable", "tasksSeattle", 1);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}

$entity = $result->getEntity();

echo $entity->getPartitionKey().":".$entity->getRowKey();
```

## <a name="retrieve-all-entities-in-a-partition"></a><span data-ttu-id="eba20-159">Recuperar todas as entidades em uma partição</span><span class="sxs-lookup"><span data-stu-id="eba20-159">Retrieve all entities in a partition</span></span>
<span data-ttu-id="eba20-160">As consultas de entidade são construídas com filtros (para obter mais informações, consulte [Querying Tables and Entities][filters] [Consultando tabelas e entidades]).</span><span class="sxs-lookup"><span data-stu-id="eba20-160">Entity queries are constructed using filters (for more information, see [Querying Tables and Entities][filters]).</span></span> <span data-ttu-id="eba20-161">Para recuperar todas as entidades na partição, use o filtro "PartitionKey eq *nome_da_partição*".</span><span class="sxs-lookup"><span data-stu-id="eba20-161">To retrieve all entities in partition, use the filter "PartitionKey eq *partition_name*".</span></span> <span data-ttu-id="eba20-162">O exemplo a seguir mostra como recuperar todas as entidades na partição `tasksSeattle` passando um filtro para o método **queryEntities** .</span><span class="sxs-lookup"><span data-stu-id="eba20-162">The following example shows how to retrieve all entities in the `tasksSeattle` partition by passing a filter to the **queryEntities** method.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

$filter = "PartitionKey eq 'tasksSeattle'";

try    {
    $result = $tableRestProxy->queryEntities("mytable", $filter);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}

$entities = $result->getEntities();

foreach($entities as $entity){
    echo $entity->getPartitionKey().":".$entity->getRowKey()."<br />";
}
```

## <a name="retrieve-a-subset-of-entities-in-a-partition"></a><span data-ttu-id="eba20-163">Recuperar um subconjunto de entidades em uma partição</span><span class="sxs-lookup"><span data-stu-id="eba20-163">Retrieve a subset of entities in a partition</span></span>
<span data-ttu-id="eba20-164">O mesmo padrão usado no exemplo anterior pode ser usado para recuperar qualquer subconjunto de entidades em uma partição.</span><span class="sxs-lookup"><span data-stu-id="eba20-164">The same pattern used in the previous example can be used to retrieve any subset of entities in a partition.</span></span> <span data-ttu-id="eba20-165">O subconjunto de entidades recuperado é determinado pelo filtro usado (para obter mais informações, consulte [Querying Tables and Entities][filters] [Consultando tabelas e entidades]). O exemplo a seguir mostra como usar um filtro para recuperar todas as entidades com um `Location` específico e um `DueDate` menor que uma data especificada.</span><span class="sxs-lookup"><span data-stu-id="eba20-165">The subset of entities you retrieve are determined by the filter you use (for more information, see [Querying Tables and Entities][filters]).The following example shows how to use a filter to retrieve all entities with a specific `Location` and a `DueDate` less than a specified date.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

$filter = "Location eq 'Office' and DueDate lt '2012-11-5'";

try    {
    $result = $tableRestProxy->queryEntities("mytable", $filter);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}

$entities = $result->getEntities();

foreach($entities as $entity){
    echo $entity->getPartitionKey().":".$entity->getRowKey()."<br />";
}
```

## <a name="retrieve-a-subset-of-entity-properties"></a><span data-ttu-id="eba20-166">Recuperar um subconjunto de propriedades da entidade</span><span class="sxs-lookup"><span data-stu-id="eba20-166">Retrieve a subset of entity properties</span></span>
<span data-ttu-id="eba20-167">Uma consulta pode recuperar um subconjunto de propriedades da entidade.</span><span class="sxs-lookup"><span data-stu-id="eba20-167">A query can retrieve a subset of entity properties.</span></span> <span data-ttu-id="eba20-168">Essa técnica, chamada *projeção*, reduz a largura de banda e pode melhorar o desempenho da consulta, principalmente para grandes entidades.</span><span class="sxs-lookup"><span data-stu-id="eba20-168">This technique, called *projection*, reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="eba20-169">Para especificar uma propriedade a ser recuperada, passe o nome da propriedade para o método **Consulta->addSelectField**.</span><span class="sxs-lookup"><span data-stu-id="eba20-169">To specify a property to be retrieved, pass the name of the property to the **Query->addSelectField** method.</span></span> <span data-ttu-id="eba20-170">Você pode chamar esse método várias vezes para adicionar mais propriedades.</span><span class="sxs-lookup"><span data-stu-id="eba20-170">You can call this method multiple times to add more properties.</span></span> <span data-ttu-id="eba20-171">Depois da execução de **TableRestProxy->queryEntities**, as entidades retornadas somente terão as propriedades selecionadas.</span><span class="sxs-lookup"><span data-stu-id="eba20-171">After executing **TableRestProxy->queryEntities**, the returned entities will only have the selected properties.</span></span> <span data-ttu-id="eba20-172">(Se você desejar retornar um subconjunto de entidades de tabela, use um filtro conforme as consultas acima.)</span><span class="sxs-lookup"><span data-stu-id="eba20-172">(If you want to return a subset of Table entities, use a filter as shown in the queries above.)</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Table\Models\QueryEntitiesOptions;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

$options = new QueryEntitiesOptions();
$options->addSelectField("Description");

try    {
    $result = $tableRestProxy->queryEntities("mytable", $options);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}

// All entities in the table are returned, regardless of whether
// they have the Description field.
// To limit the results returned, use a filter.
$entities = $result->getEntities();

foreach($entities as $entity){
    $description = $entity->getProperty("Description")->getValue();
    echo $description."<br />";
}
```

## <a name="update-an-entity"></a><span data-ttu-id="eba20-173">Atualizar uma entidade</span><span class="sxs-lookup"><span data-stu-id="eba20-173">Update an entity</span></span>
<span data-ttu-id="eba20-174">Uma entidade existente pode ser atualizada usando os métodos **Entidade->setProperty** e **Entidade->addProperty** na entidade e, em seguida, chamando **TableRestProxy->updateEntity**.</span><span class="sxs-lookup"><span data-stu-id="eba20-174">An existing entity can be updated by using the **Entity->setProperty** and **Entity->addProperty** methods on the entity, and then calling **TableRestProxy->updateEntity**.</span></span> <span data-ttu-id="eba20-175">O exemplo a seguir recupera uma entidade, modifica uma propriedade, remove outra propriedade e adiciona uma nova propriedade.</span><span class="sxs-lookup"><span data-stu-id="eba20-175">The following example retrieves an entity, modifies one property, removes another property, and adds a new property.</span></span> <span data-ttu-id="eba20-176">Observe que você pode remover uma propriedade definindo seu valor como **null**.</span><span class="sxs-lookup"><span data-stu-id="eba20-176">Note that you can remove a property by setting its value to **null**.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Table\Models\Entity;
use MicrosoftAzure\Storage\Table\Models\EdmType;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

$result = $tableRestProxy->getEntity("mytable", "tasksSeattle", 1);

$entity = $result->getEntity();

$entity->setPropertyValue("DueDate", new DateTime()); //Modified DueDate.

$entity->setPropertyValue("Location", null); //Removed Location.

$entity->addProperty("Status", EdmType::STRING, "In progress"); //Added Status.

try    {
    $tableRestProxy->updateEntity("mytable", $entity);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="delete-an-entity"></a><span data-ttu-id="eba20-177">Excluir uma entidade</span><span class="sxs-lookup"><span data-stu-id="eba20-177">Delete an entity</span></span>
<span data-ttu-id="eba20-178">Para excluir uma entidade, passe o nome da tabela e a `PartitionKey` e `RowKey` da entidade para o método **TableRestProxy->deleteEntity**.</span><span class="sxs-lookup"><span data-stu-id="eba20-178">To delete an entity, pass the table name, and the entity's `PartitionKey` and `RowKey` to the **TableRestProxy->deleteEntity** method.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

try    {
    // Delete entity.
    $tableRestProxy->deleteEntity("mytable", "tasksSeattle", "2");
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

<span data-ttu-id="eba20-179">Observe que, para verificações de simultaneidade, você pode definir o Etag para uma entidade a ser excluída, usando o método **DeleteEntityOptions->setEtag** e passando o objeto **DeleteEntityOptions** para **deleteEntity** como um quarto parâmetro.</span><span class="sxs-lookup"><span data-stu-id="eba20-179">Note that for concurrency checks, you can set the Etag for an entity to be deleted by using the **DeleteEntityOptions->setEtag** method and passing the **DeleteEntityOptions** object to **deleteEntity** as a fourth parameter.</span></span>

## <a name="batch-table-operations"></a><span data-ttu-id="eba20-180">Operações de tabela em lote</span><span class="sxs-lookup"><span data-stu-id="eba20-180">Batch table operations</span></span>
<span data-ttu-id="eba20-181">O método **TableRestProxy->lote** permite que você execute várias operações em uma única solicitação.</span><span class="sxs-lookup"><span data-stu-id="eba20-181">The **TableRestProxy->batch** method allows you to execute multiple operations in a single request.</span></span> <span data-ttu-id="eba20-182">O padrão aqui envolve a adição de operações para o objeto **BatchRequest** e, em seguida, passa o objeto **BatchRequest** para o método **TableRestProxy->lote**.</span><span class="sxs-lookup"><span data-stu-id="eba20-182">The pattern here involves adding operations to **BatchRequest** object and then passing the **BatchRequest** object to the **TableRestProxy->batch** method.</span></span> <span data-ttu-id="eba20-183">Para adicionar uma operação a um objeto **BatchRequest** , você pode chamar várias vezes para qualquer um dos seguintes métodos:</span><span class="sxs-lookup"><span data-stu-id="eba20-183">To add an operation to a **BatchRequest** object, you can call any of the following methods multiple times:</span></span>

* <span data-ttu-id="eba20-184">**addInsertEntity** (adiciona uma operação insertEntity)</span><span class="sxs-lookup"><span data-stu-id="eba20-184">**addInsertEntity** (adds an insertEntity operation)</span></span>
* <span data-ttu-id="eba20-185">**addUpdateEntity** (adiciona uma operação updateEntity)</span><span class="sxs-lookup"><span data-stu-id="eba20-185">**addUpdateEntity** (adds an updateEntity operation)</span></span>
* <span data-ttu-id="eba20-186">**addMergeEntity** (adiciona uma operação mergeEntity)</span><span class="sxs-lookup"><span data-stu-id="eba20-186">**addMergeEntity** (adds a mergeEntity operation)</span></span>
* <span data-ttu-id="eba20-187">**addInsertOrReplaceEntity** (adiciona uma operação insertOrReplaceEntity)</span><span class="sxs-lookup"><span data-stu-id="eba20-187">**addInsertOrReplaceEntity** (adds an insertOrReplaceEntity operation)</span></span>
* <span data-ttu-id="eba20-188">**addInsertOrMergeEntity** (adiciona uma operação insertOrMergeEntity)</span><span class="sxs-lookup"><span data-stu-id="eba20-188">**addInsertOrMergeEntity** (adds an insertOrMergeEntity operation)</span></span>
* <span data-ttu-id="eba20-189">**addDeleteEntity** (adiciona uma operação deleteEntity)</span><span class="sxs-lookup"><span data-stu-id="eba20-189">**addDeleteEntity** (adds a deleteEntity operation)</span></span>

<span data-ttu-id="eba20-190">O exemplo a seguir mostra como executar as operações **insertEntity** e **deleteEntity** em uma única solicitação:</span><span class="sxs-lookup"><span data-stu-id="eba20-190">The following example shows how to execute **insertEntity** and **deleteEntity** operations in a single request:</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Table\Models\Entity;
use MicrosoftAzure\Storage\Table\Models\EdmType;
use MicrosoftAzure\Storage\Table\Models\BatchOperations;

    // Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

// Create list of batch operation.
$operations = new BatchOperations();

$entity1 = new Entity();
$entity1->setPartitionKey("tasksSeattle");
$entity1->setRowKey("2");
$entity1->addProperty("Description", null, "Clean roof gutters.");
$entity1->addProperty("DueDate",
                        EdmType::DATETIME,
                        new DateTime("2012-11-05T08:15:00-08:00"));
$entity1->addProperty("Location", EdmType::STRING, "Home");

// Add operation to list of batch operations.
$operations->addInsertEntity("mytable", $entity1);

// Add operation to list of batch operations.
$operations->addDeleteEntity("mytable", "tasksSeattle", "1");

try    {
    $tableRestProxy->batch($operations);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

<span data-ttu-id="eba20-191">Para obter mais informações sobre operações de Tabela de envio em lote, consulte [Performing Entity Group Transactions][entity-group-transactions] (Executando transações do grupo de entidade).</span><span class="sxs-lookup"><span data-stu-id="eba20-191">For more information about batching Table operations, see [Performing Entity Group Transactions][entity-group-transactions].</span></span>

## <a name="delete-a-table"></a><span data-ttu-id="eba20-192">Excluir uma tabela</span><span class="sxs-lookup"><span data-stu-id="eba20-192">Delete a table</span></span>
<span data-ttu-id="eba20-193">Finalmente, para excluir uma tabela, passe o nome da tabela para o método **TableRestProxy->deleteTable**.</span><span class="sxs-lookup"><span data-stu-id="eba20-193">Finally, to delete a table, pass the table name to the **TableRestProxy->deleteTable** method.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create table REST proxy.
$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);

try    {
    // Delete table.
    $tableRestProxy->deleteTable("mytable");
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179438.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="next-steps"></a><span data-ttu-id="eba20-194">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="eba20-194">Next steps</span></span>
<span data-ttu-id="eba20-195">Agora que você aprendeu os conceitos básicos do serviço Tabela do Azure, siga estes links para aprender sobre tarefas de armazenamento mais complexas.</span><span class="sxs-lookup"><span data-stu-id="eba20-195">Now that you've learned the basics of the Azure Table service, follow these links to learn about more complex storage tasks.</span></span>

* <span data-ttu-id="eba20-196">[O Gerenciador de Armazenamento do Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md) é um aplicativo autônomo e gratuito da Microsoft que possibilita o trabalho visual com os dados do Armazenamento do Azure no Windows, MacOS e Linux.</span><span class="sxs-lookup"><span data-stu-id="eba20-196">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you to work visually with Azure Storage data on Windows, macOS, and Linux.</span></span>

* <span data-ttu-id="eba20-197">[Central de Desenvolvimento do PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="eba20-197">[PHP Developer Center](/develop/php/).</span></span>

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
[require_once]: http://php.net/require_once
[table-service-timeouts]: http://msdn.microsoft.com/library/azure/dd894042.aspx

[table-data-model]: http://msdn.microsoft.com/library/azure/dd179338.aspx
[filters]: http://msdn.microsoft.com/library/azure/dd894031.aspx
[entity-group-transactions]: http://msdn.microsoft.com/library/azure/dd894038.aspx
