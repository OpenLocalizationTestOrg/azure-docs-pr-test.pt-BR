---
title: aaaHow toouse armazenamento de tabela do Azure com Python | Microsoft Docs
description: "Armazene dados estruturados em nuvem hello usando o armazenamento de tabela do Azure, um repositório de dados NoSQL."
services: storage
documentationcenter: python
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 7ddb9f3e-4e6d-4103-96e6-f0351d69a17b
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 05/16/2017
ms.author: marsma
ms.openlocfilehash: fd0e1b05cc12618f348eaf2d85d0dce5ac32702a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-table-storage-in-python"></a><span data-ttu-id="4a2ac-103">Como toouse o armazenamento de tabela em Python</span><span class="sxs-lookup"><span data-stu-id="4a2ac-103">How toouse Table storage in Python</span></span>

[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

<span data-ttu-id="4a2ac-104">Este guia mostra como tooperform comuns cenários de armazenamento de tabela do Azure em Python usando Olá [Microsoft Azure Storage SDK para Python](https://github.com/Azure/azure-storage-python).</span><span class="sxs-lookup"><span data-stu-id="4a2ac-104">This guide shows you how tooperform common Azure Table storage scenarios in Python using hello [Microsoft Azure Storage SDK for Python](https://github.com/Azure/azure-storage-python).</span></span> <span data-ttu-id="4a2ac-105">cenários de saudação abordados incluem a criação e exclusão de uma tabela e inserir e consultar entidades.</span><span class="sxs-lookup"><span data-stu-id="4a2ac-105">hello scenarios covered include creating and deleting a table, and inserting and querying entities.</span></span>

<span data-ttu-id="4a2ac-106">Enquanto trabalham em cenários de saudação neste tutorial, você poderá toorefer toohello [SDK de armazenamento do Azure para referência de API do Python](https://azure-storage.readthedocs.io/en/latest/index.html).</span><span class="sxs-lookup"><span data-stu-id="4a2ac-106">While working through hello scenarios in this tutorial, you may wish toorefer toohello [Azure Storage SDK for Python API reference](https://azure-storage.readthedocs.io/en/latest/index.html).</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="install-hello-azure-storage-sdk-for-python"></a><span data-ttu-id="4a2ac-107">Instalar hello Azure Storage SDK para Python</span><span class="sxs-lookup"><span data-stu-id="4a2ac-107">Install hello Azure Storage SDK for Python</span></span>

<span data-ttu-id="4a2ac-108">Depois de criar uma conta de armazenamento, a próxima etapa é Olá tooinstall [Microsoft Azure Storage SDK para Python](https://github.com/Azure/azure-storage-python).</span><span class="sxs-lookup"><span data-stu-id="4a2ac-108">Once you've created a storage account, your next step is tooinstall hello [Microsoft Azure Storage SDK for Python](https://github.com/Azure/azure-storage-python).</span></span> <span data-ttu-id="4a2ac-109">Para obter detalhes sobre como instalar hello SDK, consulte toohello [README.rst](https://github.com/Azure/azure-storage-python/blob/master/README.rst) arquivo no hello Storage SDK para o repositório de Python no GitHub.</span><span class="sxs-lookup"><span data-stu-id="4a2ac-109">For details on installing hello SDK, refer toohello [README.rst](https://github.com/Azure/azure-storage-python/blob/master/README.rst) file in hello Storage SDK for Python repository on GitHub.</span></span>

## <a name="create-a-table"></a><span data-ttu-id="4a2ac-110">Criar uma tabela</span><span class="sxs-lookup"><span data-stu-id="4a2ac-110">Create a table</span></span>

<span data-ttu-id="4a2ac-111">toowork com hello de Python do serviço tabela do Azure, você deve importar Olá [TableService] [ py_TableService] módulo.</span><span class="sxs-lookup"><span data-stu-id="4a2ac-111">toowork with hello Azure Table service in Python, you must import hello [TableService][py_TableService] module.</span></span> <span data-ttu-id="4a2ac-112">Desde que você estará trabalhando com entidades de tabela, você também precisa Olá [entidade] [ py_Entity] classe.</span><span class="sxs-lookup"><span data-stu-id="4a2ac-112">Since you'll be working with Table entities, you also need hello [Entity][py_Entity] class.</span></span> <span data-ttu-id="4a2ac-113">Adicione este código superior Olá seu arquivo do Python tooimport ambos:</span><span class="sxs-lookup"><span data-stu-id="4a2ac-113">Add this code near hello top your Python file tooimport both:</span></span>

```python
from azure.storage.table import TableService, Entity
```

<span data-ttu-id="4a2ac-114">Crie um objeto [TableService][py_TableService], passando o nome da conta de armazenamento e a chave de conta.</span><span class="sxs-lookup"><span data-stu-id="4a2ac-114">Create a [TableService][py_TableService] object, passing in your storage account name and account key.</span></span> <span data-ttu-id="4a2ac-115">Substituir `myaccount` e `mykey` com seu nome de conta e a chave e a chamada [create_table] [ py_create_table] toocreate tabela de saudação no armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="4a2ac-115">Replace `myaccount` and `mykey` with your account name and key, and call [create_table][py_create_table] toocreate hello table in Azure Storage.</span></span>

```python
table_service = TableService(account_name='myaccount', account_key='mykey')

table_service.create_table('tasktable')
```

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="4a2ac-116">Adicionar uma tabela de entidade tooa</span><span class="sxs-lookup"><span data-stu-id="4a2ac-116">Add an entity tooa table</span></span>

<span data-ttu-id="4a2ac-117">tooadd uma entidade, você primeiro crie um objeto que representa a entidade, em seguida, passe Olá objeto toohello [TableService][py_TableService].[ insert_entity] [ py_insert_entity] método.</span><span class="sxs-lookup"><span data-stu-id="4a2ac-117">tooadd an entity, you first create an object that represents your entity, then pass hello object toohello [TableService][py_TableService].[insert_entity][py_insert_entity] method.</span></span> <span data-ttu-id="4a2ac-118">objeto de entidade Olá pode ser um dicionário ou um objeto do tipo [entidade][py_Entity]e define valores e nomes de propriedade da entidade.</span><span class="sxs-lookup"><span data-stu-id="4a2ac-118">hello entity object can be a dictionary or an object of type [Entity][py_Entity], and defines your entity's property names and values.</span></span> <span data-ttu-id="4a2ac-119">Cada entidade deve incluir Olá necessário [PartitionKey e RowKey](#partitionkey-and-rowkey) propriedades, em adição tooany outras propriedades que você define para entidade hello.</span><span class="sxs-lookup"><span data-stu-id="4a2ac-119">Every entity must include hello required [PartitionKey and RowKey](#partitionkey-and-rowkey) properties, in addition tooany other properties you define for hello entity.</span></span>

<span data-ttu-id="4a2ac-120">Este exemplo cria um objeto de dicionário que representa uma entidade, em seguida, passa toohello [insert_entity] [ py_insert_entity] método tooadd-toohello tabela:</span><span class="sxs-lookup"><span data-stu-id="4a2ac-120">This example creates a dictionary object representing an entity, then passes it toohello [insert_entity][py_insert_entity] method tooadd it toohello table:</span></span>

```python
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out hello trash', 'priority' : 200}
table_service.insert_entity('tasktable', task)
```

<span data-ttu-id="4a2ac-121">Este exemplo cria um [entidade] [ py_Entity] do objeto, em seguida, passa-toohello [insert_entity] [ py_insert_entity] método tooadd-toohello tabela:</span><span class="sxs-lookup"><span data-stu-id="4a2ac-121">This example creates an [Entity][py_Entity] object, then passes it toohello [insert_entity][py_insert_entity] method tooadd it toohello table:</span></span>

```python
task = Entity()
task.PartitionKey = 'tasksSeattle'
task.RowKey = '002'
task.description = 'Wash hello car'
task.priority = 100
table_service.insert_entity('tasktable', task)
```

### <a name="partitionkey-and-rowkey"></a><span data-ttu-id="4a2ac-122">PartitionKey e RowKey</span><span class="sxs-lookup"><span data-stu-id="4a2ac-122">PartitionKey and RowKey</span></span>

<span data-ttu-id="4a2ac-123">Você deve especificar uma propriedade **PartitionKey** e uma **RowKey** para cada entidade.</span><span class="sxs-lookup"><span data-stu-id="4a2ac-123">You must specify both a **PartitionKey** and a **RowKey** property for every entity.</span></span> <span data-ttu-id="4a2ac-124">Esses são identificadores exclusivos de saudação de suas entidades, como juntos eles formam Olá a chave primária de uma entidade.</span><span class="sxs-lookup"><span data-stu-id="4a2ac-124">These are hello unique identifiers of your entities, as together they form hello primary key of an entity.</span></span> <span data-ttu-id="4a2ac-125">Você pode consultar usando esses valores muito mais rápido do que pode consultar quaisquer outras propriedades de entidade porque somente essas propriedades são indexadas.</span><span class="sxs-lookup"><span data-stu-id="4a2ac-125">You can query using these values much faster than you can query any other entity properties because only these properties are indexed.</span></span>

<span data-ttu-id="4a2ac-126">Olá serviço tabela usa **PartitionKey** toointelligently distribuir entidades de tabela em nós de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="4a2ac-126">hello Table service uses **PartitionKey** toointelligently distribute table entities across storage nodes.</span></span> <span data-ttu-id="4a2ac-127">Entidades que tenham Olá mesmo **PartitionKey** são armazenados em Olá mesmo nó.</span><span class="sxs-lookup"><span data-stu-id="4a2ac-127">Entities that have hello same  **PartitionKey** are stored on hello same node.</span></span> <span data-ttu-id="4a2ac-128">**RowKey** é Olá a ID exclusiva da entidade de saudação na partição Olá pertence a.</span><span class="sxs-lookup"><span data-stu-id="4a2ac-128">**RowKey** is hello unique ID of hello entity within hello partition it belongs to.</span></span>

## <a name="update-an-entity"></a><span data-ttu-id="4a2ac-129">Atualizar uma entidade</span><span class="sxs-lookup"><span data-stu-id="4a2ac-129">Update an entity</span></span>

<span data-ttu-id="4a2ac-130">tooupdate todos os valores de propriedade da entidade, chamada hello [update_entity] [ py_update_entity] método.</span><span class="sxs-lookup"><span data-stu-id="4a2ac-130">tooupdate all of an entity's property values, call hello [update_entity][py_update_entity] method.</span></span> <span data-ttu-id="4a2ac-131">Este exemplo mostra como uma entidade existente com uma versão atualizada do tooreplace:</span><span class="sxs-lookup"><span data-stu-id="4a2ac-131">This example shows how tooreplace an existing entity with an updated version:</span></span>

```python
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out hello garbage', 'priority' : 250}
table_service.update_entity('tasktable', task)
```

<span data-ttu-id="4a2ac-132">Se a entidade de saudação que está sendo atualizada não existir, Olá operação de atualização falhará.</span><span class="sxs-lookup"><span data-stu-id="4a2ac-132">If hello entity that is being updated doesn't already exist, then hello update operation will fail.</span></span> <span data-ttu-id="4a2ac-133">Se você quiser toostore uma entidade se ele existe ou não, use [insert_or_replace_entity][py_insert_or_replace_entity].</span><span class="sxs-lookup"><span data-stu-id="4a2ac-133">If you want toostore an entity whether it exists or not, use [insert_or_replace_entity][py_insert_or_replace_entity].</span></span> <span data-ttu-id="4a2ac-134">Em Olá exemplo a seguir, primeira chamada de saudação substituirá entidade existente hello.</span><span class="sxs-lookup"><span data-stu-id="4a2ac-134">In hello following example, hello first call will replace hello existing entity.</span></span> <span data-ttu-id="4a2ac-135">segunda chamada de saudação inserirá uma nova entidade, pois nenhuma entidade com hello especificado PartitionKey e RowKey existe na tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="4a2ac-135">hello second call will insert a new entity, since no entity with hello specified PartitionKey and RowKey exists in hello table.</span></span>

```python
# Replace hello entity created earlier
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out hello garbage again', 'priority' : 250}
table_service.insert_or_replace_entity('tasktable', task)

# Insert a new entity
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '003', 'description' : 'Buy detergent', 'priority' : 300}
table_service.insert_or_replace_entity('tasktable', task)
```

> [!TIP]
> <span data-ttu-id="4a2ac-136">Olá [update_entity] [ py_update_entity] método substitui todas as propriedades e valores de uma entidade existente, você também pode usar propriedades tooremove de uma entidade existente.</span><span class="sxs-lookup"><span data-stu-id="4a2ac-136">hello [update_entity][py_update_entity] method replaces all properties and values of an existing entity, which you can also use tooremove properties from an existing entity.</span></span> <span data-ttu-id="4a2ac-137">Você pode usar o hello [merge_entity] [ py_merge_entity] método tooupdate uma entidade existente com valores de propriedade novos ou modificados sem substituir totalmente entidade hello.</span><span class="sxs-lookup"><span data-stu-id="4a2ac-137">You can use hello [merge_entity][py_merge_entity] method tooupdate an existing entity with new or modified property values without completely replacing hello entity.</span></span>

## <a name="modify-multiple-entities"></a><span data-ttu-id="4a2ac-138">Modificar várias entidades</span><span class="sxs-lookup"><span data-stu-id="4a2ac-138">Modify multiple entities</span></span>

<span data-ttu-id="4a2ac-139">tooensure Olá processamento atômica de uma solicitação de serviço de tabela hello, você pode enviar várias operações em um lote.</span><span class="sxs-lookup"><span data-stu-id="4a2ac-139">tooensure hello atomic processing of a request by hello Table service, you can submit multiple operations together in a batch.</span></span> <span data-ttu-id="4a2ac-140">Primeiro, use Olá [TableBatch] [ py_TableBatch] classe tooadd várias operações tooa único lote.</span><span class="sxs-lookup"><span data-stu-id="4a2ac-140">First, use hello [TableBatch][py_TableBatch] class tooadd multiple operations tooa single batch.</span></span> <span data-ttu-id="4a2ac-141">Em seguida, chame [TableService][py_TableService].[ commit_batch] [ py_commit_batch] toosubmit operações de saudação em uma operação atômica.</span><span class="sxs-lookup"><span data-stu-id="4a2ac-141">Next, call [TableService][py_TableService].[commit_batch][py_commit_batch] toosubmit hello operations in an atomic operation.</span></span> <span data-ttu-id="4a2ac-142">Todos os toobe entidades modificadas no lote deve estar no hello mesma partição.</span><span class="sxs-lookup"><span data-stu-id="4a2ac-142">All entities toobe modified in batch must be in hello same partition.</span></span>

<span data-ttu-id="4a2ac-143">Esse exemplo adiciona duas entidades juntas em um lote:</span><span class="sxs-lookup"><span data-stu-id="4a2ac-143">This example adds two entities together in a batch:</span></span>

```python
from azure.storage.table import TableBatch
batch = TableBatch()
task004 = {'PartitionKey': 'tasksSeattle', 'RowKey': '004', 'description' : 'Go grocery shopping', 'priority' : 400}
task005 = {'PartitionKey': 'tasksSeattle', 'RowKey': '005', 'description' : 'Clean hello bathroom', 'priority' : 100}
batch.insert_entity(task004)
batch.insert_entity(task005)
table_service.commit_batch('tasktable', batch)
```

<span data-ttu-id="4a2ac-144">Lotes também podem ser usados com a sintaxe do Gerenciador de contexto hello:</span><span class="sxs-lookup"><span data-stu-id="4a2ac-144">Batches can also be used with hello context manager syntax:</span></span>

```python
task006 = {'PartitionKey': 'tasksSeattle', 'RowKey': '006', 'description' : 'Go grocery shopping', 'priority' : 400}
task007 = {'PartitionKey': 'tasksSeattle', 'RowKey': '007', 'description' : 'Clean hello bathroom', 'priority' : 100}

with table_service.batch('tasktable') as batch:
    batch.insert_entity(task006)
    batch.insert_entity(task007)
```

## <a name="query-for-an-entity"></a><span data-ttu-id="4a2ac-145">Consultar uma entidade</span><span class="sxs-lookup"><span data-stu-id="4a2ac-145">Query for an entity</span></span>

<span data-ttu-id="4a2ac-146">tooquery para uma entidade em uma tabela, passe seu toohello PartitionKey e RowKey [TableService][py_TableService].[ get_entity] [ py_get_entity] método.</span><span class="sxs-lookup"><span data-stu-id="4a2ac-146">tooquery for an entity in a table, pass its PartitionKey and RowKey toohello [TableService][py_TableService].[get_entity][py_get_entity] method.</span></span>

```python
task = table_service.get_entity('tasktable', 'tasksSeattle', '001')
print(task.description)
print(task.priority)
```

## <a name="query-a-set-of-entities"></a><span data-ttu-id="4a2ac-147">Consultar um conjunto de entidades</span><span class="sxs-lookup"><span data-stu-id="4a2ac-147">Query a set of entities</span></span>

<span data-ttu-id="4a2ac-148">Você pode consultar um conjunto de entidades, fornecendo uma cadeia de caracteres de filtro com hello **filtro** parâmetro.</span><span class="sxs-lookup"><span data-stu-id="4a2ac-148">You can query for a set of entities by supplying a filter string with hello **filter** parameter.</span></span> <span data-ttu-id="4a2ac-149">Este exemplo localiza todas as tarefas em Seattle aplicando um filtro em PartitionKey:</span><span class="sxs-lookup"><span data-stu-id="4a2ac-149">This example finds all tasks in Seattle by applying a filter on PartitionKey:</span></span>

```python
tasks = table_service.query_entities('tasktable', filter="PartitionKey eq 'tasksSeattle'")
for task in tasks:
    print(task.description)
    print(task.priority)
```

## <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="4a2ac-150">consultar um subconjunto de propriedades da entidade</span><span class="sxs-lookup"><span data-stu-id="4a2ac-150">Query a subset of entity properties</span></span>

<span data-ttu-id="4a2ac-151">Você também pode restringir quais propriedades são retornadas para cada entidade em uma consulta.</span><span class="sxs-lookup"><span data-stu-id="4a2ac-151">You can also restrict which properties are returned for each entity in a query.</span></span> <span data-ttu-id="4a2ac-152">Essa técnica, chamada *projeção*, reduz a largura de banda e pode melhorar o desempenho da consulta, principalmente para entidades ou conjuntos de resultados grandes.</span><span class="sxs-lookup"><span data-stu-id="4a2ac-152">This technique, called *projection*, reduces bandwidth and can improve query performance, especially for large entities or result sets.</span></span> <span data-ttu-id="4a2ac-153">Saudação de uso **selecione** parâmetro e passar nomes de Olá das propriedades Olá desejadas retornados toohello cliente.</span><span class="sxs-lookup"><span data-stu-id="4a2ac-153">Use hello **select** parameter and pass hello names of hello properties you want returned toohello client.</span></span>

<span data-ttu-id="4a2ac-154">consulta Olá Olá código a seguir retorna apenas as descrições de saudação de entidades na tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="4a2ac-154">hello query in hello following code returns only hello descriptions of entities in hello table.</span></span>

> [!NOTE]
> <span data-ttu-id="4a2ac-155">Olá seguindo o trecho de código funciona apenas em relação a saudação armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="4a2ac-155">hello following snippet works only against hello Azure Storage.</span></span> <span data-ttu-id="4a2ac-156">Não há suporte pelo emulador de armazenamento hello.</span><span class="sxs-lookup"><span data-stu-id="4a2ac-156">It is not supported by hello storage emulator.</span></span>

```python
tasks = table_service.query_entities('tasktable', filter="PartitionKey eq 'tasksSeattle'", select='description')
for task in tasks:
    print(task.description)
```

## <a name="delete-an-entity"></a><span data-ttu-id="4a2ac-157">Excluir uma entidade</span><span class="sxs-lookup"><span data-stu-id="4a2ac-157">Delete an entity</span></span>

<span data-ttu-id="4a2ac-158">Excluir uma entidade, passando o toohello PartitionKey e RowKey [delete_entity] [ py_delete_entity] método.</span><span class="sxs-lookup"><span data-stu-id="4a2ac-158">Delete an entity by passing its PartitionKey and RowKey toohello [delete_entity][py_delete_entity] method.</span></span>

```python
table_service.delete_entity('tasktable', 'tasksSeattle', '001')
```

## <a name="delete-a-table"></a><span data-ttu-id="4a2ac-159">Excluir uma tabela</span><span class="sxs-lookup"><span data-stu-id="4a2ac-159">Delete a table</span></span>

<span data-ttu-id="4a2ac-160">Se você não precisar mais uma tabela ou qualquer uma das entidades hello dentro dele, chame Olá [delete_table] [ py_delete_table] método toopermanently excluir tabela de saudação do armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="4a2ac-160">If you no longer need a table or any of hello entities within it, call hello [delete_table][py_delete_table] method toopermanently delete hello table from Azure Storage.</span></span>

```python
table_service.delete_table('tasktable')
```

## <a name="next-steps"></a><span data-ttu-id="4a2ac-161">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4a2ac-161">Next steps</span></span>

* [<span data-ttu-id="4a2ac-162">Referência do SDK do Armazenamento do Azure para API do Python</span><span class="sxs-lookup"><span data-stu-id="4a2ac-162">Azure Storage SDK for Python API reference</span></span>](https://azure-storage.readthedocs.io/en/latest/index.html)
* [<span data-ttu-id="4a2ac-163">SDK do Armazenamento do Azure para Python</span><span class="sxs-lookup"><span data-stu-id="4a2ac-163">Azure Storage SDK for Python</span></span>](https://github.com/Azure/azure-storage-python)
* [<span data-ttu-id="4a2ac-164">Centro de desenvolvedores do Python</span><span class="sxs-lookup"><span data-stu-id="4a2ac-164">Python Developer Center</span></span>](https://azure.microsoft.com/develop/python/)
* <span data-ttu-id="4a2ac-165">[Gerenciador de Armazenamento do Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md): um aplicativo gratuito de plataforma cruzada para trabalhar visualmente com os dados do Armazenamento do Azure no Windows, macOS e Linux.</span><span class="sxs-lookup"><span data-stu-id="4a2ac-165">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md): A free, cross-platform application for working visually with Azure Storage data on Windows, macOS, and Linux.</span></span>

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
