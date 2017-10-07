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
# <a name="how-toouse-table-storage-in-python"></a>Como toouse o armazenamento de tabela em Python

[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

Este guia mostra como tooperform comuns cenários de armazenamento de tabela do Azure em Python usando Olá [Microsoft Azure Storage SDK para Python](https://github.com/Azure/azure-storage-python). cenários de saudação abordados incluem a criação e exclusão de uma tabela e inserir e consultar entidades.

Enquanto trabalham em cenários de saudação neste tutorial, você poderá toorefer toohello [SDK de armazenamento do Azure para referência de API do Python](https://azure-storage.readthedocs.io/en/latest/index.html).

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="install-hello-azure-storage-sdk-for-python"></a>Instalar hello Azure Storage SDK para Python

Depois de criar uma conta de armazenamento, a próxima etapa é Olá tooinstall [Microsoft Azure Storage SDK para Python](https://github.com/Azure/azure-storage-python). Para obter detalhes sobre como instalar hello SDK, consulte toohello [README.rst](https://github.com/Azure/azure-storage-python/blob/master/README.rst) arquivo no hello Storage SDK para o repositório de Python no GitHub.

## <a name="create-a-table"></a>Criar uma tabela

toowork com hello de Python do serviço tabela do Azure, você deve importar Olá [TableService] [ py_TableService] módulo. Desde que você estará trabalhando com entidades de tabela, você também precisa Olá [entidade] [ py_Entity] classe. Adicione este código superior Olá seu arquivo do Python tooimport ambos:

```python
from azure.storage.table import TableService, Entity
```

Crie um objeto [TableService][py_TableService], passando o nome da conta de armazenamento e a chave de conta. Substituir `myaccount` e `mykey` com seu nome de conta e a chave e a chamada [create_table] [ py_create_table] toocreate tabela de saudação no armazenamento do Azure.

```python
table_service = TableService(account_name='myaccount', account_key='mykey')

table_service.create_table('tasktable')
```

## <a name="add-an-entity-tooa-table"></a>Adicionar uma tabela de entidade tooa

tooadd uma entidade, você primeiro crie um objeto que representa a entidade, em seguida, passe Olá objeto toohello [TableService][py_TableService].[ insert_entity] [ py_insert_entity] método. objeto de entidade Olá pode ser um dicionário ou um objeto do tipo [entidade][py_Entity]e define valores e nomes de propriedade da entidade. Cada entidade deve incluir Olá necessário [PartitionKey e RowKey](#partitionkey-and-rowkey) propriedades, em adição tooany outras propriedades que você define para entidade hello.

Este exemplo cria um objeto de dicionário que representa uma entidade, em seguida, passa toohello [insert_entity] [ py_insert_entity] método tooadd-toohello tabela:

```python
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out hello trash', 'priority' : 200}
table_service.insert_entity('tasktable', task)
```

Este exemplo cria um [entidade] [ py_Entity] do objeto, em seguida, passa-toohello [insert_entity] [ py_insert_entity] método tooadd-toohello tabela:

```python
task = Entity()
task.PartitionKey = 'tasksSeattle'
task.RowKey = '002'
task.description = 'Wash hello car'
task.priority = 100
table_service.insert_entity('tasktable', task)
```

### <a name="partitionkey-and-rowkey"></a>PartitionKey e RowKey

Você deve especificar uma propriedade **PartitionKey** e uma **RowKey** para cada entidade. Esses são identificadores exclusivos de saudação de suas entidades, como juntos eles formam Olá a chave primária de uma entidade. Você pode consultar usando esses valores muito mais rápido do que pode consultar quaisquer outras propriedades de entidade porque somente essas propriedades são indexadas.

Olá serviço tabela usa **PartitionKey** toointelligently distribuir entidades de tabela em nós de armazenamento. Entidades que tenham Olá mesmo **PartitionKey** são armazenados em Olá mesmo nó. **RowKey** é Olá a ID exclusiva da entidade de saudação na partição Olá pertence a.

## <a name="update-an-entity"></a>Atualizar uma entidade

tooupdate todos os valores de propriedade da entidade, chamada hello [update_entity] [ py_update_entity] método. Este exemplo mostra como uma entidade existente com uma versão atualizada do tooreplace:

```python
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out hello garbage', 'priority' : 250}
table_service.update_entity('tasktable', task)
```

Se a entidade de saudação que está sendo atualizada não existir, Olá operação de atualização falhará. Se você quiser toostore uma entidade se ele existe ou não, use [insert_or_replace_entity][py_insert_or_replace_entity]. Em Olá exemplo a seguir, primeira chamada de saudação substituirá entidade existente hello. segunda chamada de saudação inserirá uma nova entidade, pois nenhuma entidade com hello especificado PartitionKey e RowKey existe na tabela de saudação.

```python
# Replace hello entity created earlier
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out hello garbage again', 'priority' : 250}
table_service.insert_or_replace_entity('tasktable', task)

# Insert a new entity
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '003', 'description' : 'Buy detergent', 'priority' : 300}
table_service.insert_or_replace_entity('tasktable', task)
```

> [!TIP]
> Olá [update_entity] [ py_update_entity] método substitui todas as propriedades e valores de uma entidade existente, você também pode usar propriedades tooremove de uma entidade existente. Você pode usar o hello [merge_entity] [ py_merge_entity] método tooupdate uma entidade existente com valores de propriedade novos ou modificados sem substituir totalmente entidade hello.

## <a name="modify-multiple-entities"></a>Modificar várias entidades

tooensure Olá processamento atômica de uma solicitação de serviço de tabela hello, você pode enviar várias operações em um lote. Primeiro, use Olá [TableBatch] [ py_TableBatch] classe tooadd várias operações tooa único lote. Em seguida, chame [TableService][py_TableService].[ commit_batch] [ py_commit_batch] toosubmit operações de saudação em uma operação atômica. Todos os toobe entidades modificadas no lote deve estar no hello mesma partição.

Esse exemplo adiciona duas entidades juntas em um lote:

```python
from azure.storage.table import TableBatch
batch = TableBatch()
task004 = {'PartitionKey': 'tasksSeattle', 'RowKey': '004', 'description' : 'Go grocery shopping', 'priority' : 400}
task005 = {'PartitionKey': 'tasksSeattle', 'RowKey': '005', 'description' : 'Clean hello bathroom', 'priority' : 100}
batch.insert_entity(task004)
batch.insert_entity(task005)
table_service.commit_batch('tasktable', batch)
```

Lotes também podem ser usados com a sintaxe do Gerenciador de contexto hello:

```python
task006 = {'PartitionKey': 'tasksSeattle', 'RowKey': '006', 'description' : 'Go grocery shopping', 'priority' : 400}
task007 = {'PartitionKey': 'tasksSeattle', 'RowKey': '007', 'description' : 'Clean hello bathroom', 'priority' : 100}

with table_service.batch('tasktable') as batch:
    batch.insert_entity(task006)
    batch.insert_entity(task007)
```

## <a name="query-for-an-entity"></a>Consultar uma entidade

tooquery para uma entidade em uma tabela, passe seu toohello PartitionKey e RowKey [TableService][py_TableService].[ get_entity] [ py_get_entity] método.

```python
task = table_service.get_entity('tasktable', 'tasksSeattle', '001')
print(task.description)
print(task.priority)
```

## <a name="query-a-set-of-entities"></a>Consultar um conjunto de entidades

Você pode consultar um conjunto de entidades, fornecendo uma cadeia de caracteres de filtro com hello **filtro** parâmetro. Este exemplo localiza todas as tarefas em Seattle aplicando um filtro em PartitionKey:

```python
tasks = table_service.query_entities('tasktable', filter="PartitionKey eq 'tasksSeattle'")
for task in tasks:
    print(task.description)
    print(task.priority)
```

## <a name="query-a-subset-of-entity-properties"></a>consultar um subconjunto de propriedades da entidade

Você também pode restringir quais propriedades são retornadas para cada entidade em uma consulta. Essa técnica, chamada *projeção*, reduz a largura de banda e pode melhorar o desempenho da consulta, principalmente para entidades ou conjuntos de resultados grandes. Saudação de uso **selecione** parâmetro e passar nomes de Olá das propriedades Olá desejadas retornados toohello cliente.

consulta Olá Olá código a seguir retorna apenas as descrições de saudação de entidades na tabela de saudação.

> [!NOTE]
> Olá seguindo o trecho de código funciona apenas em relação a saudação armazenamento do Azure. Não há suporte pelo emulador de armazenamento hello.

```python
tasks = table_service.query_entities('tasktable', filter="PartitionKey eq 'tasksSeattle'", select='description')
for task in tasks:
    print(task.description)
```

## <a name="delete-an-entity"></a>Excluir uma entidade

Excluir uma entidade, passando o toohello PartitionKey e RowKey [delete_entity] [ py_delete_entity] método.

```python
table_service.delete_entity('tasktable', 'tasksSeattle', '001')
```

## <a name="delete-a-table"></a>Excluir uma tabela

Se você não precisar mais uma tabela ou qualquer uma das entidades hello dentro dele, chame Olá [delete_table] [ py_delete_table] método toopermanently excluir tabela de saudação do armazenamento do Azure.

```python
table_service.delete_table('tasktable')
```

## <a name="next-steps"></a>Próximas etapas

* [Referência do SDK do Armazenamento do Azure para API do Python](https://azure-storage.readthedocs.io/en/latest/index.html)
* [SDK do Armazenamento do Azure para Python](https://github.com/Azure/azure-storage-python)
* [Centro de desenvolvedores do Python](https://azure.microsoft.com/develop/python/)
* [Gerenciador de Armazenamento do Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md): um aplicativo gratuito de plataforma cruzada para trabalhar visualmente com os dados do Armazenamento do Azure no Windows, macOS e Linux.

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
