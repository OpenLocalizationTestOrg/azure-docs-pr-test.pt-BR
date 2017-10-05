---
title: Como usar o Armazenamento de Tabelas do Azure com Python | Microsoft Docs
description: "Armazene dados estruturados na nuvem usando o Armazenamento de Tabelas do Azure, um repositório de dados NoSQL."
services: cosmos-db
documentationcenter: python
author: mimig1
manager: jhubbard
editor: tysonn
ms.assetid: 7ddb9f3e-4e6d-4103-96e6-f0351d69a17b
ms.service: cosmos-db
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 05/16/2017
ms.author: mimig
ms.openlocfilehash: 0c46f04786ba4b62bd7ca22c5e25643123e6e136
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-table-storage-in-python"></a><span data-ttu-id="705c0-103">Como usar o Armazenamento de Tabelas no Python</span><span class="sxs-lookup"><span data-stu-id="705c0-103">How to use Table storage in Python</span></span>

[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

<span data-ttu-id="705c0-104">Este guia mostra como executar cenários comuns do Armazenamento de Tabelas do Azure no Python usando o [SDK do Armazenamento do Microsoft Azure para Python](https://github.com/Azure/azure-storage-python).</span><span class="sxs-lookup"><span data-stu-id="705c0-104">This guide shows you how to perform common Azure Table storage scenarios in Python using the [Microsoft Azure Storage SDK for Python](https://github.com/Azure/azure-storage-python).</span></span> <span data-ttu-id="705c0-105">Os cenários abordados incluem a criação e a exclusão de uma tabela e a inserção e consulta de entidades.</span><span class="sxs-lookup"><span data-stu-id="705c0-105">The scenarios covered include creating and deleting a table, and inserting and querying entities.</span></span>

<span data-ttu-id="705c0-106">Enquanto estiver trabalhando nos cenários deste tutorial, talvez você queira consultar a [Referência do SDK do Armazenamento do Azure para API do Python](https://azure-storage.readthedocs.io/en/latest/index.html).</span><span class="sxs-lookup"><span data-stu-id="705c0-106">While working through the scenarios in this tutorial, you may wish to refer to the [Azure Storage SDK for Python API reference](https://azure-storage.readthedocs.io/en/latest/index.html).</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="install-the-azure-storage-sdk-for-python"></a><span data-ttu-id="705c0-107">Instalar o SDK do Armazenamento do Azure para Python</span><span class="sxs-lookup"><span data-stu-id="705c0-107">Install the Azure Storage SDK for Python</span></span>

<span data-ttu-id="705c0-108">Depois de criar uma conta de armazenamento, a próxima etapa é instalar o [SDK do Armazenamento do Microsoft Azure para Python](https://github.com/Azure/azure-storage-python).</span><span class="sxs-lookup"><span data-stu-id="705c0-108">Once you've created a storage account, your next step is to install the [Microsoft Azure Storage SDK for Python](https://github.com/Azure/azure-storage-python).</span></span> <span data-ttu-id="705c0-109">Para obter detalhes sobre como instalar o SDK, consulte o arquivo [README.rst](https://github.com/Azure/azure-storage-python/blob/master/README.rst) no repositório do SDK do Armazenamento para Python no GitHub.</span><span class="sxs-lookup"><span data-stu-id="705c0-109">For details on installing the SDK, refer to the [README.rst](https://github.com/Azure/azure-storage-python/blob/master/README.rst) file in the Storage SDK for Python repository on GitHub.</span></span>

## <a name="create-a-table"></a><span data-ttu-id="705c0-110">Criar uma tabela</span><span class="sxs-lookup"><span data-stu-id="705c0-110">Create a table</span></span>

<span data-ttu-id="705c0-111">Para trabalhar com o serviço Tabela do Azure no Python, você deve importar o módulo [TableService][py_TableService].</span><span class="sxs-lookup"><span data-stu-id="705c0-111">To work with the Azure Table service in Python, you must import the [TableService][py_TableService] module.</span></span> <span data-ttu-id="705c0-112">Como você estará trabalhando com entidades de tabela, também precisará da classe [Entity][py_Entity].</span><span class="sxs-lookup"><span data-stu-id="705c0-112">Since you'll be working with Table entities, you also need the [Entity][py_Entity] class.</span></span> <span data-ttu-id="705c0-113">Adicione este código próximo à parte superior seu arquivo Python para importar ambos:</span><span class="sxs-lookup"><span data-stu-id="705c0-113">Add this code near the top your Python file to import both:</span></span>

```python
from azure.storage.table import TableService, Entity
```

<span data-ttu-id="705c0-114">Crie um objeto [TableService][py_TableService], passando o nome da conta de armazenamento e a chave de conta.</span><span class="sxs-lookup"><span data-stu-id="705c0-114">Create a [TableService][py_TableService] object, passing in your storage account name and account key.</span></span> <span data-ttu-id="705c0-115">Substitua `myaccount` e `mykey` por seu nome de conta e a chave e chame [create_table][py_create_table] para criar a tabela no Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="705c0-115">Replace `myaccount` and `mykey` with your account name and key, and call [create_table][py_create_table] to create the table in Azure Storage.</span></span>

```python
table_service = TableService(account_name='myaccount', account_key='mykey')

table_service.create_table('tasktable')
```

## <a name="add-an-entity-to-a-table"></a><span data-ttu-id="705c0-116">Adicionar uma entidade a uma tabela</span><span class="sxs-lookup"><span data-stu-id="705c0-116">Add an entity to a table</span></span>

<span data-ttu-id="705c0-117">Para adicionar uma entidade, primeiro crie um objeto que representa a entidade, em seguida, passe o objeto para o método [TableService][py_TableService].[insert_entity][py_insert_entity].</span><span class="sxs-lookup"><span data-stu-id="705c0-117">To add an entity, you first create an object that represents your entity, then pass the object to the [TableService][py_TableService].[insert_entity][py_insert_entity] method.</span></span> <span data-ttu-id="705c0-118">O objeto de entidade pode ser um dicionário ou um objeto do tipo [Entity][py_Entity] e define os valores e nomes de propriedade da entidade.</span><span class="sxs-lookup"><span data-stu-id="705c0-118">The entity object can be a dictionary or an object of type [Entity][py_Entity], and defines your entity's property names and values.</span></span> <span data-ttu-id="705c0-119">Cada entidade deve incluir as propriedades [PartitionKey e RowKey](#partitionkey-and-rowkey) necessárias, além de quaisquer outras propriedades que você definir para a entidade.</span><span class="sxs-lookup"><span data-stu-id="705c0-119">Every entity must include the required [PartitionKey and RowKey](#partitionkey-and-rowkey) properties, in addition to any other properties you define for the entity.</span></span>

<span data-ttu-id="705c0-120">Este exemplo cria um objeto de dicionário que representa uma entidade, em seguida, o passa para o método [insert_entity][py_insert_entity] para adicioná-lo à tabela:</span><span class="sxs-lookup"><span data-stu-id="705c0-120">This example creates a dictionary object representing an entity, then passes it to the [insert_entity][py_insert_entity] method to add it to the table:</span></span>

```python
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out the trash', 'priority' : 200}
table_service.insert_entity('tasktable', task)
```

<span data-ttu-id="705c0-121">Este exemplo cria um objeto [Entity][py_Entity], em seguida, o passa para o método [insert_entity][py_insert_entity] para adicioná-lo à tabela:</span><span class="sxs-lookup"><span data-stu-id="705c0-121">This example creates an [Entity][py_Entity] object, then passes it to the [insert_entity][py_insert_entity] method to add it to the table:</span></span>

```python
task = Entity()
task.PartitionKey = 'tasksSeattle'
task.RowKey = '002'
task.description = 'Wash the car'
task.priority = 100
table_service.insert_entity('tasktable', task)
```

### <a name="partitionkey-and-rowkey"></a><span data-ttu-id="705c0-122">PartitionKey e RowKey</span><span class="sxs-lookup"><span data-stu-id="705c0-122">PartitionKey and RowKey</span></span>

<span data-ttu-id="705c0-123">Você deve especificar uma propriedade **PartitionKey** e uma **RowKey** para cada entidade.</span><span class="sxs-lookup"><span data-stu-id="705c0-123">You must specify both a **PartitionKey** and a **RowKey** property for every entity.</span></span> <span data-ttu-id="705c0-124">Esses são os identificadores exclusivos das entidades, uma vez que juntos eles formam a chave primária de uma entidade.</span><span class="sxs-lookup"><span data-stu-id="705c0-124">These are the unique identifiers of your entities, as together they form the primary key of an entity.</span></span> <span data-ttu-id="705c0-125">Você pode consultar usando esses valores muito mais rápido do que pode consultar quaisquer outras propriedades de entidade porque somente essas propriedades são indexadas.</span><span class="sxs-lookup"><span data-stu-id="705c0-125">You can query using these values much faster than you can query any other entity properties because only these properties are indexed.</span></span>

<span data-ttu-id="705c0-126">O serviço Tabela usa **PartitionKey** para distribuir de forma inteligente as entidades de tabela entre os nós de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="705c0-126">The Table service uses **PartitionKey** to intelligently distribute table entities across storage nodes.</span></span> <span data-ttu-id="705c0-127">As entidades com o mesmo **PartitionKey** são armazenadas no mesmo nó.</span><span class="sxs-lookup"><span data-stu-id="705c0-127">Entities that have the same  **PartitionKey** are stored on the same node.</span></span> <span data-ttu-id="705c0-128">O **RowKey** é a ID exclusiva da entidade na partição à qual pertence.</span><span class="sxs-lookup"><span data-stu-id="705c0-128">**RowKey** is the unique ID of the entity within the partition it belongs to.</span></span>

## <a name="update-an-entity"></a><span data-ttu-id="705c0-129">Atualizar uma entidade</span><span class="sxs-lookup"><span data-stu-id="705c0-129">Update an entity</span></span>

<span data-ttu-id="705c0-130">Para atualizar todos os valores de propriedade da entidade, chame o método [update_entity][py_update_entity].</span><span class="sxs-lookup"><span data-stu-id="705c0-130">To update all of an entity's property values, call the [update_entity][py_update_entity] method.</span></span> <span data-ttu-id="705c0-131">Este exemplo mostra como substituir uma entidade existente pela versão atualizada:</span><span class="sxs-lookup"><span data-stu-id="705c0-131">This example shows how to replace an existing entity with an updated version:</span></span>

```python
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out the garbage', 'priority' : 250}
table_service.update_entity('tasktable', task)
```

<span data-ttu-id="705c0-132">Se a entidade que está sendo atualizada ainda não existir, a operação de atualização falhará.</span><span class="sxs-lookup"><span data-stu-id="705c0-132">If the entity that is being updated doesn't already exist, then the update operation will fail.</span></span> <span data-ttu-id="705c0-133">Se você quiser armazenar uma entidade quer ela exista ou não, use [insert_or_replace_entity][py_insert_or_replace_entity].</span><span class="sxs-lookup"><span data-stu-id="705c0-133">If you want to store an entity whether it exists or not, use [insert_or_replace_entity][py_insert_or_replace_entity].</span></span> <span data-ttu-id="705c0-134">No exemplo a seguir, a primeira chamada substituirá a entidade existente.</span><span class="sxs-lookup"><span data-stu-id="705c0-134">In the following example, the first call will replace the existing entity.</span></span> <span data-ttu-id="705c0-135">A segunda chamada vai inserir uma nova entidade, contanto que não exista na tabela nenhuma entidade com o PartitionKey e o RowKey especificados.</span><span class="sxs-lookup"><span data-stu-id="705c0-135">The second call will insert a new entity, since no entity with the specified PartitionKey and RowKey exists in the table.</span></span>

```python
# Replace the entity created earlier
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out the garbage again', 'priority' : 250}
table_service.insert_or_replace_entity('tasktable', task)

# Insert a new entity
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '003', 'description' : 'Buy detergent', 'priority' : 300}
table_service.insert_or_replace_entity('tasktable', task)
```

> [!TIP]
> <span data-ttu-id="705c0-136">O método [update_entity][py_update_entity] substitui todas as propriedades e valores de uma entidade existente, que você também pode usar para remover propriedades de uma entidade existente.</span><span class="sxs-lookup"><span data-stu-id="705c0-136">The [update_entity][py_update_entity] method replaces all properties and values of an existing entity, which you can also use to remove properties from an existing entity.</span></span> <span data-ttu-id="705c0-137">Você pode usar o método [merge_entity][py_merge_entity] para atualizar uma entidade existente com valores de propriedade novos ou modificados sem substituir totalmente a entidade.</span><span class="sxs-lookup"><span data-stu-id="705c0-137">You can use the [merge_entity][py_merge_entity] method to update an existing entity with new or modified property values without completely replacing the entity.</span></span>

## <a name="modify-multiple-entities"></a><span data-ttu-id="705c0-138">Modificar várias entidades</span><span class="sxs-lookup"><span data-stu-id="705c0-138">Modify multiple entities</span></span>

<span data-ttu-id="705c0-139">Para garantir o processamento atômico de uma solicitação pelo serviço Tabela, você pode enviar várias operações juntas em um lote.</span><span class="sxs-lookup"><span data-stu-id="705c0-139">To ensure the atomic processing of a request by the Table service, you can submit multiple operations together in a batch.</span></span> <span data-ttu-id="705c0-140">Primeiro, use a classe [TableBatch][py_TableBatch] para adicionar várias operações a um único lote.</span><span class="sxs-lookup"><span data-stu-id="705c0-140">First, use the [TableBatch][py_TableBatch] class to add multiple operations to a single batch.</span></span> <span data-ttu-id="705c0-141">Em seguida, chame [TableService][py_TableService].[commit_batch][py_commit_batch] para enviar as operações em uma operação atômica.</span><span class="sxs-lookup"><span data-stu-id="705c0-141">Next, call [TableService][py_TableService].[commit_batch][py_commit_batch] to submit the operations in an atomic operation.</span></span> <span data-ttu-id="705c0-142">Todas as entidades a serem modificadas em lote devem estar na mesma partição.</span><span class="sxs-lookup"><span data-stu-id="705c0-142">All entities to be modified in batch must be in the same partition.</span></span>

<span data-ttu-id="705c0-143">Esse exemplo adiciona duas entidades juntas em um lote:</span><span class="sxs-lookup"><span data-stu-id="705c0-143">This example adds two entities together in a batch:</span></span>

```python
from azure.storage.table import TableBatch
batch = TableBatch()
task004 = {'PartitionKey': 'tasksSeattle', 'RowKey': '004', 'description' : 'Go grocery shopping', 'priority' : 400}
task005 = {'PartitionKey': 'tasksSeattle', 'RowKey': '005', 'description' : 'Clean the bathroom', 'priority' : 100}
batch.insert_entity(task004)
batch.insert_entity(task005)
table_service.commit_batch('tasktable', batch)
```

<span data-ttu-id="705c0-144">Os lotes também podem ser usados com a sintaxe do gerenciador de contexto:</span><span class="sxs-lookup"><span data-stu-id="705c0-144">Batches can also be used with the context manager syntax:</span></span>

```python
task006 = {'PartitionKey': 'tasksSeattle', 'RowKey': '006', 'description' : 'Go grocery shopping', 'priority' : 400}
task007 = {'PartitionKey': 'tasksSeattle', 'RowKey': '007', 'description' : 'Clean the bathroom', 'priority' : 100}

with table_service.batch('tasktable') as batch:
    batch.insert_entity(task006)
    batch.insert_entity(task007)
```

## <a name="query-for-an-entity"></a><span data-ttu-id="705c0-145">Consultar uma entidade</span><span class="sxs-lookup"><span data-stu-id="705c0-145">Query for an entity</span></span>

<span data-ttu-id="705c0-146">Para consultar uma entidade em uma tabela, passe seu PartitionKey e RowKey para o método [TableService][py_TableService].[get_entity][py_get_entity].</span><span class="sxs-lookup"><span data-stu-id="705c0-146">To query for an entity in a table, pass its PartitionKey and RowKey to the [TableService][py_TableService].[get_entity][py_get_entity] method.</span></span>

```python
task = table_service.get_entity('tasktable', 'tasksSeattle', '001')
print(task.description)
print(task.priority)
```

## <a name="query-a-set-of-entities"></a><span data-ttu-id="705c0-147">Consultar um conjunto de entidades</span><span class="sxs-lookup"><span data-stu-id="705c0-147">Query a set of entities</span></span>

<span data-ttu-id="705c0-148">Você pode consultar um conjunto de entidades fornecendo uma cadeia de caracteres de filtro com o parâmetro **filtro**.</span><span class="sxs-lookup"><span data-stu-id="705c0-148">You can query for a set of entities by supplying a filter string with the **filter** parameter.</span></span> <span data-ttu-id="705c0-149">Este exemplo localiza todas as tarefas em Seattle aplicando um filtro em PartitionKey:</span><span class="sxs-lookup"><span data-stu-id="705c0-149">This example finds all tasks in Seattle by applying a filter on PartitionKey:</span></span>

```python
tasks = table_service.query_entities('tasktable', filter="PartitionKey eq 'tasksSeattle'")
for task in tasks:
    print(task.description)
    print(task.priority)
```

## <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="705c0-150">consultar um subconjunto de propriedades da entidade</span><span class="sxs-lookup"><span data-stu-id="705c0-150">Query a subset of entity properties</span></span>

<span data-ttu-id="705c0-151">Você também pode restringir quais propriedades são retornadas para cada entidade em uma consulta.</span><span class="sxs-lookup"><span data-stu-id="705c0-151">You can also restrict which properties are returned for each entity in a query.</span></span> <span data-ttu-id="705c0-152">Essa técnica, chamada *projeção*, reduz a largura de banda e pode melhorar o desempenho da consulta, principalmente para entidades ou conjuntos de resultados grandes.</span><span class="sxs-lookup"><span data-stu-id="705c0-152">This technique, called *projection*, reduces bandwidth and can improve query performance, especially for large entities or result sets.</span></span> <span data-ttu-id="705c0-153">Use o parâmetro **select** e transmita os nomes das propriedades que você deseja que sejam retornadas para o cliente.</span><span class="sxs-lookup"><span data-stu-id="705c0-153">Use the **select** parameter and pass the names of the properties you want returned to the client.</span></span>

<span data-ttu-id="705c0-154">A consulta no código a seguir retorna apenas as descrições das entidades na tabela.</span><span class="sxs-lookup"><span data-stu-id="705c0-154">The query in the following code returns only the descriptions of entities in the table.</span></span>

> [!NOTE]
> <span data-ttu-id="705c0-155">O trecho a seguir funciona apenas no Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="705c0-155">The following snippet works only against the Azure Storage.</span></span> <span data-ttu-id="705c0-156">Não há suporte para ele no emulador de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="705c0-156">It is not supported by the storage emulator.</span></span>

```python
tasks = table_service.query_entities('tasktable', filter="PartitionKey eq 'tasksSeattle'", select='description')
for task in tasks:
    print(task.description)
```

## <a name="delete-an-entity"></a><span data-ttu-id="705c0-157">Excluir uma entidade</span><span class="sxs-lookup"><span data-stu-id="705c0-157">Delete an entity</span></span>

<span data-ttu-id="705c0-158">Exclua uma entidade passando seu PartitionKey e RowKey para o método [delete_entity][py_delete_entity].</span><span class="sxs-lookup"><span data-stu-id="705c0-158">Delete an entity by passing its PartitionKey and RowKey to the [delete_entity][py_delete_entity] method.</span></span>

```python
table_service.delete_entity('tasktable', 'tasksSeattle', '001')
```

## <a name="delete-a-table"></a><span data-ttu-id="705c0-159">Excluir uma tabela</span><span class="sxs-lookup"><span data-stu-id="705c0-159">Delete a table</span></span>

<span data-ttu-id="705c0-160">Se você não precisar mais de uma tabela ou qualquer uma das entidades dentro dela, chame o método [delete_table][py_delete_table] para excluir permanentemente a tabela do Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="705c0-160">If you no longer need a table or any of the entities within it, call the [delete_table][py_delete_table] method to permanently delete the table from Azure Storage.</span></span>

```python
table_service.delete_table('tasktable')
```

## <a name="next-steps"></a><span data-ttu-id="705c0-161">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="705c0-161">Next steps</span></span>

* [<span data-ttu-id="705c0-162">Referência do SDK do Armazenamento do Azure para API do Python</span><span class="sxs-lookup"><span data-stu-id="705c0-162">Azure Storage SDK for Python API reference</span></span>](https://azure-storage.readthedocs.io/en/latest/index.html)
* [<span data-ttu-id="705c0-163">SDK do Armazenamento do Azure para Python</span><span class="sxs-lookup"><span data-stu-id="705c0-163">Azure Storage SDK for Python</span></span>](https://github.com/Azure/azure-storage-python)
* [<span data-ttu-id="705c0-164">Centro de desenvolvedores do Python</span><span class="sxs-lookup"><span data-stu-id="705c0-164">Python Developer Center</span></span>](https://azure.microsoft.com/develop/python/)
* <span data-ttu-id="705c0-165">[Gerenciador de Armazenamento do Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md): um aplicativo gratuito de plataforma cruzada para trabalhar visualmente com os dados do Armazenamento do Azure no Windows, macOS e Linux.</span><span class="sxs-lookup"><span data-stu-id="705c0-165">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md): A free, cross-platform application for working visually with Azure Storage data on Windows, macOS, and Linux.</span></span>

[py_commit_batch]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.commit_batch
[py_create_table]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.create_table
[py_delete_entity]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.delete_entity
[py_delete_table]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.delete_table
[py_Entity]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.models.html#azure.storage.table.models.Entity
[py_get_entity]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.get_entity
[py_insert_entity]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.insert_entity
[py_insert_or_replace_entity]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.insert_or_replace_entity
[py_merge_entity]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.merge_entity
[py_update_entity]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.update_entity
[py_TableService]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html
[py_TableBatch]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tablebatch.html#azure.storage.table.tablebatch.TableBatch
