---
title: armazenamento de tabela toouse aaaHow do PHP | Microsoft Docs
description: "Saiba como toouse Olá serviço tabela do PHP toocreate e excluir uma tabela e insert, delete e tabela de saudação de consulta."
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
ms.openlocfilehash: 1e1036118e208280b4c205da7d7eea61e79359c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-table-storage-from-php"></a><span data-ttu-id="2d132-103">Como o armazenamento de PHP de tabela toouse</span><span class="sxs-lookup"><span data-stu-id="2d132-103">How toouse table storage from PHP</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a><span data-ttu-id="2d132-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="2d132-104">Overview</span></span>
<span data-ttu-id="2d132-105">Este guia mostra como os cenários comuns de tooperform usando Olá serviço tabela do Azure.</span><span class="sxs-lookup"><span data-stu-id="2d132-105">This guide shows you how tooperform common scenarios using hello Azure Table service.</span></span> <span data-ttu-id="2d132-106">exemplos de saudação são escritos em PHP e usar Olá [Azure SDK para PHP][download].</span><span class="sxs-lookup"><span data-stu-id="2d132-106">hello samples are written in PHP and use hello [Azure SDK for PHP][download].</span></span> <span data-ttu-id="2d132-107">Olá cenários abordados incluem **criar e excluir uma tabela e inserir, excluir e consultar entidades em uma tabela**.</span><span class="sxs-lookup"><span data-stu-id="2d132-107">hello scenarios covered include **creating and deleting a table, and inserting, deleting, and querying entities in a table**.</span></span> <span data-ttu-id="2d132-108">Para obter mais informações sobre Olá serviço tabela do Azure, consulte Olá [próximas etapas](#next-steps) seção.</span><span class="sxs-lookup"><span data-stu-id="2d132-108">For more information on hello Azure Table service, see hello [Next steps](#next-steps) section.</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="2d132-109">Criar um aplicativo PHP</span><span class="sxs-lookup"><span data-stu-id="2d132-109">Create a PHP application</span></span>
<span data-ttu-id="2d132-110">Olá apenas requisito para criar um aplicativo PHP que acessa o serviço de tabela do Azure Olá Olá referência de classes hello Azure SDK para PHP de dentro de seu código.</span><span class="sxs-lookup"><span data-stu-id="2d132-110">hello only requirement for creating a PHP application that accesses hello Azure Table service is hello referencing of classes in hello Azure SDK for PHP from within your code.</span></span> <span data-ttu-id="2d132-111">Você pode usar qualquer toocreate de ferramentas de desenvolvimento do aplicativo, incluindo o bloco de notas.</span><span class="sxs-lookup"><span data-stu-id="2d132-111">You can use any development tools toocreate your application, including Notepad.</span></span>

<span data-ttu-id="2d132-112">Neste guia, você usa os recursos de serviço Tabela que podem ser chamados de dentro de um aplicativo PHP localmente ou no código em execução dentro de um site, função de trabalho ou função web do Azure.</span><span class="sxs-lookup"><span data-stu-id="2d132-112">In this guide, you use Table service features which can be called from within a PHP application locally, or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-hello-azure-client-libraries"></a><span data-ttu-id="2d132-113">Obter bibliotecas de saudação do cliente do Azure</span><span class="sxs-lookup"><span data-stu-id="2d132-113">Get hello Azure Client Libraries</span></span>
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-tooaccess-hello-table-service"></a><span data-ttu-id="2d132-114">Configurar o serviço de tabela do aplicativo tooaccess Olá</span><span class="sxs-lookup"><span data-stu-id="2d132-114">Configure your application tooaccess hello Table service</span></span>
<span data-ttu-id="2d132-115">serviço de tabela do Azure toouse Olá APIs, você precisa:</span><span class="sxs-lookup"><span data-stu-id="2d132-115">toouse hello Azure Table service APIs, you need to:</span></span>

1. <span data-ttu-id="2d132-116">Arquivo de carregador automático de saudação de referência usando Olá [require_once] [ require_once] instrução, e</span><span class="sxs-lookup"><span data-stu-id="2d132-116">Reference hello autoloader file using hello [require_once][require_once] statement, and</span></span>
2. <span data-ttu-id="2d132-117">Fazer referência a qualquer classe que você possa usar.</span><span class="sxs-lookup"><span data-stu-id="2d132-117">Reference any classes you might use.</span></span>

<span data-ttu-id="2d132-118">Olá exemplo a seguir mostra como tooinclude Olá Olá de referência e o arquivo do carregador automático **ServicesBuilder** classe.</span><span class="sxs-lookup"><span data-stu-id="2d132-118">hello following example shows how tooinclude hello autoloader file and reference hello **ServicesBuilder** class.</span></span>

> [!NOTE]
> <span data-ttu-id="2d132-119">exemplos de Olá neste artigo presumem que você instalou Olá bibliotecas de cliente do PHP para o Azure por meio do criador.</span><span class="sxs-lookup"><span data-stu-id="2d132-119">hello examples in this article assume you have installed hello PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="2d132-120">Se você instalou bibliotecas Olá manualmente, você precisa Olá tooreference <code>WindowsAzure.php</code> arquivo do carregador automático.</span><span class="sxs-lookup"><span data-stu-id="2d132-120">If you installed hello libraries manually, you need tooreference hello <code>WindowsAzure.php</code> autoloader file.</span></span>
>
>

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

<span data-ttu-id="2d132-121">Nos exemplos de saudação abaixo, Olá `require_once` instrução sempre é mostrada, mas apenas Olá classes necessárias para tooexecute do exemplo hello são referenciadas.</span><span class="sxs-lookup"><span data-stu-id="2d132-121">In hello examples below, hello `require_once` statement is always shown, but only hello classes necessary for hello example tooexecute are referenced.</span></span>

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="2d132-122">Configurar uma conexão de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="2d132-122">Set up an Azure storage connection</span></span>
<span data-ttu-id="2d132-123">tooinstantiate um cliente do serviço tabela do Azure, primeiro você deve ter uma cadeia de caracteres de conexão válido.</span><span class="sxs-lookup"><span data-stu-id="2d132-123">tooinstantiate an Azure Table service client, you must first have a valid connection string.</span></span> <span data-ttu-id="2d132-124">formato Olá Olá a cadeia de conexão de serviço tabela é:</span><span class="sxs-lookup"><span data-stu-id="2d132-124">hello format for hello Table service connection string is:</span></span>

<span data-ttu-id="2d132-125">Para acessar um serviço ao vivo:</span><span class="sxs-lookup"><span data-stu-id="2d132-125">For accessing a live service:</span></span>

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

<span data-ttu-id="2d132-126">Para acessar o armazenamento de emulador hello:</span><span class="sxs-lookup"><span data-stu-id="2d132-126">For accessing hello emulator storage:</span></span>

```php
UseDevelopmentStorage=true
```

<span data-ttu-id="2d132-127">toocreate qualquer cliente de serviço do Azure, você precisa Olá toouse **ServicesBuilder** classe.</span><span class="sxs-lookup"><span data-stu-id="2d132-127">toocreate any Azure service client, you need toouse hello **ServicesBuilder** class.</span></span> <span data-ttu-id="2d132-128">Você pode:</span><span class="sxs-lookup"><span data-stu-id="2d132-128">You can:</span></span>

* <span data-ttu-id="2d132-129">passar conexão Olá tooit cadeia de caracteres diretamente ou</span><span class="sxs-lookup"><span data-stu-id="2d132-129">pass hello connection string directly tooit or</span></span>
* <span data-ttu-id="2d132-130">Use Olá **CloudConfigurationManager (CCM)** toocheck externo de várias fontes de cadeia de caracteres de conexão hello:</span><span class="sxs-lookup"><span data-stu-id="2d132-130">use hello **CloudConfigurationManager (CCM)** toocheck multiple external sources for hello connection string:</span></span>
  * <span data-ttu-id="2d132-131">por padrão, ele é fornecido com suporte para uma fonte externa – variáveis de ambiente.</span><span class="sxs-lookup"><span data-stu-id="2d132-131">by default, it comes with support for one external source - environmental variables</span></span>
  * <span data-ttu-id="2d132-132">Você pode adicionar novas fontes estendendo Olá **ConnectionStringSource** classe</span><span class="sxs-lookup"><span data-stu-id="2d132-132">you can add new sources by extending hello **ConnectionStringSource** class</span></span>

<span data-ttu-id="2d132-133">Para obter exemplos de saudação descritos aqui, cadeia de caracteres de conexão hello será passada diretamente.</span><span class="sxs-lookup"><span data-stu-id="2d132-133">For hello examples outlined here, hello connection string will be passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);
```

## <a name="create-a-table"></a><span data-ttu-id="2d132-134">Criar uma tabela</span><span class="sxs-lookup"><span data-stu-id="2d132-134">Create a table</span></span>
<span data-ttu-id="2d132-135">Um **TableRestProxy** objeto permite que você crie uma tabela com hello **createTable** método.</span><span class="sxs-lookup"><span data-stu-id="2d132-135">A **TableRestProxy** object lets you create a table with hello **createTable** method.</span></span> <span data-ttu-id="2d132-136">Ao criar uma tabela, você pode definir o tempo limite do serviço de tabela hello.</span><span class="sxs-lookup"><span data-stu-id="2d132-136">When creating a table, you can set hello Table service timeout.</span></span> <span data-ttu-id="2d132-137">(Para obter mais informações sobre o tempo limite do serviço de tabela hello, consulte [definindo tempos limite para operações do serviço tabela][table-service-timeouts].)</span><span class="sxs-lookup"><span data-stu-id="2d132-137">(For more information about hello Table service timeout, see [Setting Timeouts for Table Service Operations][table-service-timeouts].)</span></span>

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

<span data-ttu-id="2d132-138">Para obter informações sobre restrições nos nomes de tabela, consulte [Olá Noções básicas sobre modelo de dados do serviço de tabela][table-data-model].</span><span class="sxs-lookup"><span data-stu-id="2d132-138">For information about restrictions on table names, see [Understanding hello Table Service Data Model][table-data-model].</span></span>

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="2d132-139">Adicionar uma tabela de entidade tooa</span><span class="sxs-lookup"><span data-stu-id="2d132-139">Add an entity tooa table</span></span>
<span data-ttu-id="2d132-140">tooadd uma tabela de tooa de entidade, crie um novo **entidade** do objeto e passá-lo muito**TableRestProxy -> insertEntity**.</span><span class="sxs-lookup"><span data-stu-id="2d132-140">tooadd an entity tooa table, create a new **Entity** object and pass it too**TableRestProxy->insertEntity**.</span></span> <span data-ttu-id="2d132-141">Observe que ao criar uma entidade, você deve especificar um `PartitionKey` e `RowKey`.</span><span class="sxs-lookup"><span data-stu-id="2d132-141">Note that when you create an entity, you must specify a `PartitionKey` and `RowKey`.</span></span> <span data-ttu-id="2d132-142">Esses são Olá identificadores exclusivos para uma entidade e valores que podem ser consultados muito mais rápido do que outras propriedades de entidade.</span><span class="sxs-lookup"><span data-stu-id="2d132-142">These are hello unique identifiers for an entity and are values that can be queried much faster than other entity properties.</span></span> <span data-ttu-id="2d132-143">Olá sistema usa `PartitionKey` tooautomatically distribuir entidades da tabela Olá em vários nós de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="2d132-143">hello system uses `PartitionKey` tooautomatically distribute hello table's entities over many storage nodes.</span></span> <span data-ttu-id="2d132-144">Entidades com hello mesmo `PartitionKey` são armazenados em Olá mesmo nó.</span><span class="sxs-lookup"><span data-stu-id="2d132-144">Entities with hello same `PartitionKey` are stored on hello same node.</span></span> <span data-ttu-id="2d132-145">(Operações em várias entidades armazenadas em Olá mesmo nó executar melhor do que em entidades armazenadas em nós diferentes.) Olá `RowKey` é Olá a ID exclusiva de uma entidade dentro de uma partição.</span><span class="sxs-lookup"><span data-stu-id="2d132-145">(Operations on multiple entities stored on hello same node perform better than on entities stored across different nodes.) hello `RowKey` is hello unique ID of an entity within a partition.</span></span>

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
$entity->addProperty("Description", null, "Take out hello trash.");
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

<span data-ttu-id="2d132-146">Para obter informações sobre propriedades de tabela e tipos, consulte [Olá Noções básicas sobre modelo de dados do serviço de tabela][table-data-model].</span><span class="sxs-lookup"><span data-stu-id="2d132-146">For information about Table properties and types, see [Understanding hello Table Service Data Model][table-data-model].</span></span>

<span data-ttu-id="2d132-147">Olá **TableRestProxy** classe oferece dois métodos alternativos para a inserção de entidades: **insertOrMergeEntity** e **insertOrReplaceEntity**.</span><span class="sxs-lookup"><span data-stu-id="2d132-147">hello **TableRestProxy** class offers two alternative methods for inserting entities: **insertOrMergeEntity** and **insertOrReplaceEntity**.</span></span> <span data-ttu-id="2d132-148">toouse desses métodos, criar um novo **entidade** e passá-lo como um método de tooeither do parâmetro.</span><span class="sxs-lookup"><span data-stu-id="2d132-148">toouse these methods, create a new **Entity** and pass it as a parameter tooeither method.</span></span> <span data-ttu-id="2d132-149">Cada método irá inserir entidade Olá se ele não existe.</span><span class="sxs-lookup"><span data-stu-id="2d132-149">Each method will insert hello entity if it does not exist.</span></span> <span data-ttu-id="2d132-150">Se já existir uma entidade hello, **insertOrMergeEntity** atualiza valores de propriedade, se existirem propriedades hello e adiciona novas propriedades enquanto se elas não existirem, **insertOrReplaceEntity** completamente substitui uma entidade existente.</span><span class="sxs-lookup"><span data-stu-id="2d132-150">If hello entity already exists, **insertOrMergeEntity** updates property values if hello properties already exist and adds new properties if they do not exist, while **insertOrReplaceEntity** completely replaces an existing entity.</span></span> <span data-ttu-id="2d132-151">Olá mostrado no exemplo a seguir como toouse **insertOrMergeEntity**.</span><span class="sxs-lookup"><span data-stu-id="2d132-151">hello following example shows how toouse **insertOrMergeEntity**.</span></span> <span data-ttu-id="2d132-152">Se Olá entidade com `PartitionKey` "tasksSeattle" e `RowKey` "1" ainda não existir, ele será inserido.</span><span class="sxs-lookup"><span data-stu-id="2d132-152">If hello entity with `PartitionKey` "tasksSeattle" and `RowKey` "1" does not already exist, it will be inserted.</span></span> <span data-ttu-id="2d132-153">No entanto, se ela tiver sido inserida anteriormente (conforme mostrado no exemplo hello acima), Olá `DueDate` propriedade serão atualizados e Olá `Status` propriedade será adicionada.</span><span class="sxs-lookup"><span data-stu-id="2d132-153">However, if it has previously been inserted (as shown in hello example above), hello `DueDate` property will be updated, and hello `Status` property will be added.</span></span> <span data-ttu-id="2d132-154">Olá `Description` e `Location` propriedades também são atualizadas, mas com valores que deixá-los inalterados efetivamente.</span><span class="sxs-lookup"><span data-stu-id="2d132-154">hello `Description` and `Location` properties are also updated, but with values that effectively leave them unchanged.</span></span> <span data-ttu-id="2d132-155">Se essas duas últimas propriedades não foram adicionadas, conforme mostrado no exemplo hello, mas existia na entidade de destino hello, seus valores existentes seriam permanecem inalteradas.</span><span class="sxs-lookup"><span data-stu-id="2d132-155">If these latter two properties were not added as shown in hello example, but existed on hello target entity, their existing values would remain unchanged.</span></span>

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
$entity->addProperty("Description", null, "Take out hello trash.");
$entity->addProperty("DueDate", EdmType::DATETIME, new DateTime()); // Modified hello DueDate field.
$entity->addProperty("Location", EdmType::STRING, "Home");
$entity->addProperty("Status", EdmType::STRING, "Complete"); // Added Status field.

try    {
    // Calling insertOrReplaceEntity, instead of insertOrMergeEntity as shown,
    // would simply replace hello entity with PartitionKey "tasksSeattle" and RowKey "1".
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

## <a name="retrieve-a-single-entity"></a><span data-ttu-id="2d132-156">Recuperar uma única entidade</span><span class="sxs-lookup"><span data-stu-id="2d132-156">Retrieve a single entity</span></span>
<span data-ttu-id="2d132-157">Olá **TableRestProxy -> getEntity** método permite que você tooretrieve uma única entidade consultando seu `PartitionKey` e `RowKey`.</span><span class="sxs-lookup"><span data-stu-id="2d132-157">hello **TableRestProxy->getEntity** method allows you tooretrieve a single entity by querying for its `PartitionKey` and `RowKey`.</span></span> <span data-ttu-id="2d132-158">O exemplo hello abaixo, Olá chave de partição `tasksSeattle` e chave de linha `1` são passados toohello **getEntity** método.</span><span class="sxs-lookup"><span data-stu-id="2d132-158">In hello example below, hello partition key `tasksSeattle` and row key `1` are passed toohello **getEntity** method.</span></span>

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

## <a name="retrieve-all-entities-in-a-partition"></a><span data-ttu-id="2d132-159">Recuperar todas as entidades em uma partição</span><span class="sxs-lookup"><span data-stu-id="2d132-159">Retrieve all entities in a partition</span></span>
<span data-ttu-id="2d132-160">As consultas de entidade são construídas com filtros (para obter mais informações, consulte [Querying Tables and Entities][filters] [Consultando tabelas e entidades]).</span><span class="sxs-lookup"><span data-stu-id="2d132-160">Entity queries are constructed using filters (for more information, see [Querying Tables and Entities][filters]).</span></span> <span data-ttu-id="2d132-161">tooretrieve todas as entidades na partição, use o filtro de hello "PartitionKey eq *nome da partição*".</span><span class="sxs-lookup"><span data-stu-id="2d132-161">tooretrieve all entities in partition, use hello filter "PartitionKey eq *partition_name*".</span></span> <span data-ttu-id="2d132-162">Olá mostrado no exemplo a seguir como tooretrieve todas as entidades Olá `tasksSeattle` partição passando um filtro toohello **queryEntities** método.</span><span class="sxs-lookup"><span data-stu-id="2d132-162">hello following example shows how tooretrieve all entities in hello `tasksSeattle` partition by passing a filter toohello **queryEntities** method.</span></span>

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

## <a name="retrieve-a-subset-of-entities-in-a-partition"></a><span data-ttu-id="2d132-163">Recuperar um subconjunto de entidades em uma partição</span><span class="sxs-lookup"><span data-stu-id="2d132-163">Retrieve a subset of entities in a partition</span></span>
<span data-ttu-id="2d132-164">Olá mesmo padrão usado no exemplo anterior Olá pode ser usado tooretrieve qualquer subconjunto de entidades em uma partição.</span><span class="sxs-lookup"><span data-stu-id="2d132-164">hello same pattern used in hello previous example can be used tooretrieve any subset of entities in a partition.</span></span> <span data-ttu-id="2d132-165">subconjunto de saudação de entidades é recuperar são determinados pelo filtro Olá usar (para obter mais informações, consulte [consultar tabelas e entidades][filters]) .hello mostrado no exemplo a seguir como toouse tooretrieve um filtro todas as entidades com um determinado `Location` e um `DueDate` menor do que uma data especificada.</span><span class="sxs-lookup"><span data-stu-id="2d132-165">hello subset of entities you retrieve are determined by hello filter you use (for more information, see [Querying Tables and Entities][filters]).hello following example shows how toouse a filter tooretrieve all entities with a specific `Location` and a `DueDate` less than a specified date.</span></span>

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

## <a name="retrieve-a-subset-of-entity-properties"></a><span data-ttu-id="2d132-166">Recuperar um subconjunto de propriedades da entidade</span><span class="sxs-lookup"><span data-stu-id="2d132-166">Retrieve a subset of entity properties</span></span>
<span data-ttu-id="2d132-167">Uma consulta pode recuperar um subconjunto de propriedades da entidade.</span><span class="sxs-lookup"><span data-stu-id="2d132-167">A query can retrieve a subset of entity properties.</span></span> <span data-ttu-id="2d132-168">Essa técnica, chamada *projeção*, reduz a largura de banda e pode melhorar o desempenho da consulta, principalmente para grandes entidades.</span><span class="sxs-lookup"><span data-stu-id="2d132-168">This technique, called *projection*, reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="2d132-169">toospecify toobe uma propriedade recuperada, passe o nome de saudação do hello propriedade toohello **consulta -> addSelectField** método.</span><span class="sxs-lookup"><span data-stu-id="2d132-169">toospecify a property toobe retrieved, pass hello name of hello property toohello **Query->addSelectField** method.</span></span> <span data-ttu-id="2d132-170">Você pode chamar esse método tooadd várias vezes mais propriedades.</span><span class="sxs-lookup"><span data-stu-id="2d132-170">You can call this method multiple times tooadd more properties.</span></span> <span data-ttu-id="2d132-171">Depois de executar **TableRestProxy -> queryEntities**, Olá retornado entidades terá apenas propriedades de saudação selecionada.</span><span class="sxs-lookup"><span data-stu-id="2d132-171">After executing **TableRestProxy->queryEntities**, hello returned entities will only have hello selected properties.</span></span> <span data-ttu-id="2d132-172">(O se você quiser tooreturn um subconjunto de entidades de tabela, use um filtro como mostrado em consultas de saudação acima.)</span><span class="sxs-lookup"><span data-stu-id="2d132-172">(If you want tooreturn a subset of Table entities, use a filter as shown in hello queries above.)</span></span>

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

// All entities in hello table are returned, regardless of whether
// they have hello Description field.
// toolimit hello results returned, use a filter.
$entities = $result->getEntities();

foreach($entities as $entity){
    $description = $entity->getProperty("Description")->getValue();
    echo $description."<br />";
}
```

## <a name="update-an-entity"></a><span data-ttu-id="2d132-173">Atualizar uma entidade</span><span class="sxs-lookup"><span data-stu-id="2d132-173">Update an entity</span></span>
<span data-ttu-id="2d132-174">Uma entidade existente pode ser atualizada usando Olá **entidade -> setProperty** e **entidade -> addProperty** métodos na entidade hello e, em seguida, chamar **TableRestProxy -> updateEntity** .</span><span class="sxs-lookup"><span data-stu-id="2d132-174">An existing entity can be updated by using hello **Entity->setProperty** and **Entity->addProperty** methods on hello entity, and then calling **TableRestProxy->updateEntity**.</span></span> <span data-ttu-id="2d132-175">Olá exemplo a seguir recupera uma entidade, modifica uma propriedade, remove a outra propriedade e adiciona uma nova propriedade.</span><span class="sxs-lookup"><span data-stu-id="2d132-175">hello following example retrieves an entity, modifies one property, removes another property, and adds a new property.</span></span> <span data-ttu-id="2d132-176">Observe que você pode remover uma propriedade definindo seu valor muito**nulo**.</span><span class="sxs-lookup"><span data-stu-id="2d132-176">Note that you can remove a property by setting its value too**null**.</span></span>

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

## <a name="delete-an-entity"></a><span data-ttu-id="2d132-177">Excluir uma entidade</span><span class="sxs-lookup"><span data-stu-id="2d132-177">Delete an entity</span></span>
<span data-ttu-id="2d132-178">toodelete uma entidade, passa o nome da tabela hello e da entidade Olá `PartitionKey` e `RowKey` toohello **TableRestProxy -> deleteEntity** método.</span><span class="sxs-lookup"><span data-stu-id="2d132-178">toodelete an entity, pass hello table name, and hello entity's `PartitionKey` and `RowKey` toohello **TableRestProxy->deleteEntity** method.</span></span>

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

<span data-ttu-id="2d132-179">Observe que para verificações de simultaneidade, você pode definir hello Etag para um toobe entidade excluída usando Olá **DeleteEntityOptions -> setEtag** método e passando Olá **DeleteEntityOptions** objeto muito**deleteEntity** como um quarto parâmetro.</span><span class="sxs-lookup"><span data-stu-id="2d132-179">Note that for concurrency checks, you can set hello Etag for an entity toobe deleted by using hello **DeleteEntityOptions->setEtag** method and passing hello **DeleteEntityOptions** object too**deleteEntity** as a fourth parameter.</span></span>

## <a name="batch-table-operations"></a><span data-ttu-id="2d132-180">Operações de tabela em lote</span><span class="sxs-lookup"><span data-stu-id="2d132-180">Batch table operations</span></span>
<span data-ttu-id="2d132-181">Olá **TableRestProxy -> lote** método permite que você tooexecute várias operações em uma única solicitação.</span><span class="sxs-lookup"><span data-stu-id="2d132-181">hello **TableRestProxy->batch** method allows you tooexecute multiple operations in a single request.</span></span> <span data-ttu-id="2d132-182">Olá padrão aqui envolve a adição de operações muito**BatchRequest** objeto e, em seguida, passando Olá **BatchRequest** objeto toohello **TableRestProxy -> lote** método.</span><span class="sxs-lookup"><span data-stu-id="2d132-182">hello pattern here involves adding operations too**BatchRequest** object and then passing hello **BatchRequest** object toohello **TableRestProxy->batch** method.</span></span> <span data-ttu-id="2d132-183">tooadd tooa uma operação **BatchRequest** do objeto, você pode chamar qualquer Olá várias vezes métodos a seguir:</span><span class="sxs-lookup"><span data-stu-id="2d132-183">tooadd an operation tooa **BatchRequest** object, you can call any of hello following methods multiple times:</span></span>

* <span data-ttu-id="2d132-184">**addInsertEntity** (adiciona uma operação insertEntity)</span><span class="sxs-lookup"><span data-stu-id="2d132-184">**addInsertEntity** (adds an insertEntity operation)</span></span>
* <span data-ttu-id="2d132-185">**addUpdateEntity** (adiciona uma operação updateEntity)</span><span class="sxs-lookup"><span data-stu-id="2d132-185">**addUpdateEntity** (adds an updateEntity operation)</span></span>
* <span data-ttu-id="2d132-186">**addMergeEntity** (adiciona uma operação mergeEntity)</span><span class="sxs-lookup"><span data-stu-id="2d132-186">**addMergeEntity** (adds a mergeEntity operation)</span></span>
* <span data-ttu-id="2d132-187">**addInsertOrReplaceEntity** (adiciona uma operação insertOrReplaceEntity)</span><span class="sxs-lookup"><span data-stu-id="2d132-187">**addInsertOrReplaceEntity** (adds an insertOrReplaceEntity operation)</span></span>
* <span data-ttu-id="2d132-188">**addInsertOrMergeEntity** (adiciona uma operação insertOrMergeEntity)</span><span class="sxs-lookup"><span data-stu-id="2d132-188">**addInsertOrMergeEntity** (adds an insertOrMergeEntity operation)</span></span>
* <span data-ttu-id="2d132-189">**addDeleteEntity** (adiciona uma operação deleteEntity)</span><span class="sxs-lookup"><span data-stu-id="2d132-189">**addDeleteEntity** (adds a deleteEntity operation)</span></span>

<span data-ttu-id="2d132-190">Olá mostrado no exemplo a seguir como tooexecute **insertEntity** e **deleteEntity** operações em uma única solicitação:</span><span class="sxs-lookup"><span data-stu-id="2d132-190">hello following example shows how tooexecute **insertEntity** and **deleteEntity** operations in a single request:</span></span>

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

// Add operation toolist of batch operations.
$operations->addInsertEntity("mytable", $entity1);

// Add operation toolist of batch operations.
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

<span data-ttu-id="2d132-191">Para obter mais informações sobre operações de Tabela de envio em lote, consulte [Performing Entity Group Transactions][entity-group-transactions] (Executando transações do grupo de entidade).</span><span class="sxs-lookup"><span data-stu-id="2d132-191">For more information about batching Table operations, see [Performing Entity Group Transactions][entity-group-transactions].</span></span>

## <a name="delete-a-table"></a><span data-ttu-id="2d132-192">Excluir uma tabela</span><span class="sxs-lookup"><span data-stu-id="2d132-192">Delete a table</span></span>
<span data-ttu-id="2d132-193">Por fim, toodelete uma tabela, passar Olá tabela nome toohello **TableRestProxy -> tabela** método.</span><span class="sxs-lookup"><span data-stu-id="2d132-193">Finally, toodelete a table, pass hello table name toohello **TableRestProxy->deleteTable** method.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="2d132-194">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2d132-194">Next steps</span></span>
<span data-ttu-id="2d132-195">Agora que você aprendeu as Noções básicas sobre Olá Olá serviço tabela do Azure, siga essas toolearn links sobre tarefas mais complexas de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="2d132-195">Now that you've learned hello basics of hello Azure Table service, follow these links toolearn about more complex storage tasks.</span></span>

* <span data-ttu-id="2d132-196">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) é um aplicativo autônomo gratuito da Microsoft que permite que você toowork visualmente com dados de armazenamento do Azure no Linux, Windows e macOS.</span><span class="sxs-lookup"><span data-stu-id="2d132-196">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you toowork visually with Azure Storage data on Windows, macOS, and Linux.</span></span>

* <span data-ttu-id="2d132-197">[Central de Desenvolvimento do PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="2d132-197">[PHP Developer Center](/develop/php/).</span></span>

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
[require_once]: http://php.net/require_once
[table-service-timeouts]: http://msdn.microsoft.com/library/azure/dd894042.aspx

[table-data-model]: http://msdn.microsoft.com/library/azure/dd179338.aspx
[filters]: http://msdn.microsoft.com/library/azure/dd894031.aspx
[entity-group-transactions]: http://msdn.microsoft.com/library/azure/dd894038.aspx
