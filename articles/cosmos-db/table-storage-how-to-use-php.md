---
title: armazenamento de tabela toouse aaaHow do PHP | Microsoft Docs
description: "Saiba como toouse Olá serviço tabela do PHP toocreate e excluir uma tabela e insert, delete e tabela de saudação de consulta."
services: cosmos-db
documentationcenter: php
author: mimig1
manager: jhubbard
editor: tysonn
ms.assetid: 1e57f371-6208-4753-b2a0-05db4aede8e3
ms.service: cosmos-db
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: php
ms.topic: article
ms.date: 12/08/2016
ms.author: mimig
ms.openlocfilehash: 5b7c92221069d1c2a6ca951c06ae8eea8bb8478c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-table-storage-from-php"></a>Como o armazenamento de PHP de tabela toouse
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a>Visão geral
Este guia mostra como os cenários comuns de tooperform usando Olá serviço tabela do Azure. exemplos de saudação são escritos em PHP e usar Olá [Azure SDK para PHP][download]. Olá cenários abordados incluem **criar e excluir uma tabela e inserir, excluir e consultar entidades em uma tabela**. Para obter mais informações sobre Olá serviço tabela do Azure, consulte Olá [próximas etapas](#next-steps) seção.

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a>Criar um aplicativo PHP
Olá apenas requisito para criar um aplicativo PHP que acessa o serviço de tabela do Azure Olá Olá referência de classes hello Azure SDK para PHP de dentro de seu código. Você pode usar qualquer toocreate de ferramentas de desenvolvimento do aplicativo, incluindo o bloco de notas.

Neste guia, você usa os recursos de serviço Tabela que podem ser chamados de dentro de um aplicativo PHP localmente ou no código em execução dentro de um site, função de trabalho ou função web do Azure.

## <a name="get-hello-azure-client-libraries"></a>Obter bibliotecas de saudação do cliente do Azure
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-tooaccess-hello-table-service"></a>Configurar o serviço de tabela do aplicativo tooaccess Olá
serviço de tabela do Azure toouse Olá APIs, você precisa:

1. Arquivo de carregador automático de saudação de referência usando Olá [require_once] [ require_once] instrução, e
2. Fazer referência a qualquer classe que você possa usar.

Olá exemplo a seguir mostra como tooinclude Olá Olá de referência e o arquivo do carregador automático **ServicesBuilder** classe.

> [!NOTE]
> exemplos de Olá neste artigo presumem que você instalou Olá bibliotecas de cliente do PHP para o Azure por meio do criador. Se você instalou bibliotecas Olá manualmente, você precisa Olá tooreference <code>WindowsAzure.php</code> arquivo do carregador automático.
>
>

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

Nos exemplos de saudação abaixo, Olá `require_once` instrução sempre é mostrada, mas apenas Olá classes necessárias para tooexecute do exemplo hello são referenciadas.

## <a name="set-up-an-azure-storage-connection"></a>Configurar uma conexão de armazenamento do Azure
tooinstantiate um cliente do serviço tabela do Azure, primeiro você deve ter uma cadeia de caracteres de conexão válido. formato Olá Olá a cadeia de conexão de serviço tabela é:

Para acessar um serviço ao vivo:

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

Para acessar o armazenamento de emulador hello:

```php
UseDevelopmentStorage=true
```

toocreate qualquer cliente de serviço do Azure, você precisa Olá toouse **ServicesBuilder** classe. Você pode:

* passar conexão Olá tooit cadeia de caracteres diretamente ou
* Use Olá **CloudConfigurationManager (CCM)** toocheck externo de várias fontes de cadeia de caracteres de conexão hello:
  * por padrão, ele é fornecido com suporte para uma fonte externa – variáveis de ambiente.
  * Você pode adicionar novas fontes estendendo Olá **ConnectionStringSource** classe

Para obter exemplos de saudação descritos aqui, cadeia de caracteres de conexão hello será passada diretamente.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);
```

## <a name="create-a-table"></a>Criar uma tabela
Um **TableRestProxy** objeto permite que você crie uma tabela com hello **createTable** método. Ao criar uma tabela, você pode definir o tempo limite do serviço de tabela hello. (Para obter mais informações sobre o tempo limite do serviço de tabela hello, consulte [definindo tempos limite para operações do serviço tabela][table-service-timeouts].)

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

Para obter informações sobre restrições nos nomes de tabela, consulte [Olá Noções básicas sobre modelo de dados do serviço de tabela][table-data-model].

## <a name="add-an-entity-tooa-table"></a>Adicionar uma tabela de entidade tooa
tooadd uma tabela de tooa de entidade, crie um novo **entidade** do objeto e passá-lo muito**TableRestProxy -> insertEntity**. Observe que ao criar uma entidade, você deve especificar um `PartitionKey` e `RowKey`. Esses são Olá identificadores exclusivos para uma entidade e valores que podem ser consultados muito mais rápido do que outras propriedades de entidade. Olá sistema usa `PartitionKey` tooautomatically distribuir entidades da tabela Olá em vários nós de armazenamento. Entidades com hello mesmo `PartitionKey` são armazenados em Olá mesmo nó. (Operações em várias entidades armazenadas em Olá mesmo nó executar melhor do que em entidades armazenadas em nós diferentes.) Olá `RowKey` é Olá a ID exclusiva de uma entidade dentro de uma partição.

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

Para obter informações sobre propriedades de tabela e tipos, consulte [Olá Noções básicas sobre modelo de dados do serviço de tabela][table-data-model].

Olá **TableRestProxy** classe oferece dois métodos alternativos para a inserção de entidades: **insertOrMergeEntity** e **insertOrReplaceEntity**. toouse desses métodos, criar um novo **entidade** e passá-lo como um método de tooeither do parâmetro. Cada método irá inserir entidade Olá se ele não existe. Se já existir uma entidade hello, **insertOrMergeEntity** atualiza valores de propriedade, se existirem propriedades hello e adiciona novas propriedades enquanto se elas não existirem, **insertOrReplaceEntity** completamente substitui uma entidade existente. Olá mostrado no exemplo a seguir como toouse **insertOrMergeEntity**. Se Olá entidade com `PartitionKey` "tasksSeattle" e `RowKey` "1" ainda não existir, ele será inserido. No entanto, se ela tiver sido inserida anteriormente (conforme mostrado no exemplo hello acima), Olá `DueDate` propriedade serão atualizados e Olá `Status` propriedade será adicionada. Olá `Description` e `Location` propriedades também são atualizadas, mas com valores que deixá-los inalterados efetivamente. Se essas duas últimas propriedades não foram adicionadas, conforme mostrado no exemplo hello, mas existia na entidade de destino hello, seus valores existentes seriam permanecem inalteradas.

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

## <a name="retrieve-a-single-entity"></a>Recuperar uma única entidade
Olá **TableRestProxy -> getEntity** método permite que você tooretrieve uma única entidade consultando seu `PartitionKey` e `RowKey`. O exemplo hello abaixo, Olá chave de partição `tasksSeattle` e chave de linha `1` são passados toohello **getEntity** método.

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

## <a name="retrieve-all-entities-in-a-partition"></a>Recuperar todas as entidades em uma partição
As consultas de entidade são construídas com filtros (para obter mais informações, consulte [Querying Tables and Entities][filters] [Consultando tabelas e entidades]). tooretrieve todas as entidades na partição, use o filtro de hello "PartitionKey eq *nome da partição*". Olá mostrado no exemplo a seguir como tooretrieve todas as entidades Olá `tasksSeattle` partição passando um filtro toohello **queryEntities** método.

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

## <a name="retrieve-a-subset-of-entities-in-a-partition"></a>Recuperar um subconjunto de entidades em uma partição
Olá mesmo padrão usado no exemplo anterior Olá pode ser usado tooretrieve qualquer subconjunto de entidades em uma partição. subconjunto de saudação de entidades é recuperar são determinados pelo filtro Olá usar (para obter mais informações, consulte [consultar tabelas e entidades][filters]) .hello mostrado no exemplo a seguir como toouse tooretrieve um filtro todas as entidades com um determinado `Location` e um `DueDate` menor do que uma data especificada.

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

## <a name="retrieve-a-subset-of-entity-properties"></a>Recuperar um subconjunto de propriedades da entidade
Uma consulta pode recuperar um subconjunto de propriedades da entidade. Essa técnica, chamada *projeção*, reduz a largura de banda e pode melhorar o desempenho da consulta, principalmente para grandes entidades. toospecify toobe uma propriedade recuperada, passe o nome de saudação do hello propriedade toohello **consulta -> addSelectField** método. Você pode chamar esse método tooadd várias vezes mais propriedades. Depois de executar **TableRestProxy -> queryEntities**, Olá retornado entidades terá apenas propriedades de saudação selecionada. (O se você quiser tooreturn um subconjunto de entidades de tabela, use um filtro como mostrado em consultas de saudação acima.)

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

## <a name="update-an-entity"></a>Atualizar uma entidade
Uma entidade existente pode ser atualizada usando Olá **entidade -> setProperty** e **entidade -> addProperty** métodos na entidade hello e, em seguida, chamar **TableRestProxy -> updateEntity** . Olá exemplo a seguir recupera uma entidade, modifica uma propriedade, remove a outra propriedade e adiciona uma nova propriedade. Observe que você pode remover uma propriedade definindo seu valor muito**nulo**.

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

## <a name="delete-an-entity"></a>Excluir uma entidade
toodelete uma entidade, passa o nome da tabela hello e da entidade Olá `PartitionKey` e `RowKey` toohello **TableRestProxy -> deleteEntity** método.

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

Observe que para verificações de simultaneidade, você pode definir hello Etag para um toobe entidade excluída usando Olá **DeleteEntityOptions -> setEtag** método e passando Olá **DeleteEntityOptions** objeto muito**deleteEntity** como um quarto parâmetro.

## <a name="batch-table-operations"></a>Operações de tabela em lote
Olá **TableRestProxy -> lote** método permite que você tooexecute várias operações em uma única solicitação. Olá padrão aqui envolve a adição de operações muito**BatchRequest** objeto e, em seguida, passando Olá **BatchRequest** objeto toohello **TableRestProxy -> lote** método. tooadd tooa uma operação **BatchRequest** do objeto, você pode chamar qualquer Olá várias vezes métodos a seguir:

* **addInsertEntity** (adiciona uma operação insertEntity)
* **addUpdateEntity** (adiciona uma operação updateEntity)
* **addMergeEntity** (adiciona uma operação mergeEntity)
* **addInsertOrReplaceEntity** (adiciona uma operação insertOrReplaceEntity)
* **addInsertOrMergeEntity** (adiciona uma operação insertOrMergeEntity)
* **addDeleteEntity** (adiciona uma operação deleteEntity)

Olá mostrado no exemplo a seguir como tooexecute **insertEntity** e **deleteEntity** operações em uma única solicitação:

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

Para obter mais informações sobre operações de Tabela de envio em lote, consulte [Performing Entity Group Transactions][entity-group-transactions] (Executando transações do grupo de entidade).

## <a name="delete-a-table"></a>Excluir uma tabela
Por fim, toodelete uma tabela, passar Olá tabela nome toohello **TableRestProxy -> tabela** método.

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

## <a name="next-steps"></a>Próximas etapas
Agora que você aprendeu as Noções básicas sobre Olá Olá serviço tabela do Azure, siga essas toolearn links sobre tarefas mais complexas de armazenamento.

* [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) é um aplicativo autônomo gratuito da Microsoft que permite que você toowork visualmente com dados de armazenamento do Azure no Linux, Windows e macOS.

* [Central de Desenvolvimento do PHP](/develop/php/).

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
[require_once]: http://php.net/require_once
[table-service-timeouts]: http://msdn.microsoft.com/library/azure/dd894042.aspx

[table-data-model]: http://msdn.microsoft.com/library/azure/dd179338.aspx
[filters]: http://msdn.microsoft.com/library/azure/dd894031.aspx
[entity-group-transactions]: http://msdn.microsoft.com/library/azure/dd894038.aspx
