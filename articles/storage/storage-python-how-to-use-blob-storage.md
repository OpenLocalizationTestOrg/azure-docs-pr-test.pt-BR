---
title: aaaHow toouse o armazenamento de BLOBs do Azure (armazenamento de objeto) do Python | Microsoft Docs
description: "Armazene dados não estruturados em nuvem Olá com armazenamento de BLOBs do Azure (armazenamento de objeto)."
services: storage
documentationcenter: python
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 0348e360-b24d-41fa-bb12-b8f18990d8bc
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 2/24/2017
ms.author: marsma
ms.openlocfilehash: 6efc61aa89e6d2544b7a18c80ce3546640f90462
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-blob-storage-from-python"></a>Como toouse armazenamento de BLOBs do Azure do Python
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>Visão geral
Armazenamento de BLOBs do Azure é um serviço que armazena dados não estruturados em nuvem hello como objetos/blobs. O Armazenamento de Blobs pode conter qualquer tipo de texto ou de dados binários, como um documento, um arquivo de mídia ou um instalador de aplicativo. Armazenamento de blob também é chamado tooas armazenamento de objeto.

Este artigo mostra como tooperform cenários comuns de usar o armazenamento de Blob. exemplos de saudação são escritos em Python e usar Olá [Microsoft Azure Storage SDK para Python]. cenários de saudação abordados incluem carregar, listar, baixar e exclusão de blobs.

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-container"></a>Criar um contêiner
Com base no tipo de saudação do blob que deseja toouse, crie um **BlockBlobService**, **AppendBlobService**, ou **PageBlobService** objeto. código a seguir Olá usa um **BlockBlobService** objeto. Adicione a seguinte Olá superior de saudação de qualquer arquivo Python no qual você deseja acesso tooprogrammatically armazenamento de Blob de bloco do Azure.

```python
from azure.storage.blob import BlockBlobService
```

Olá código a seguir cria um **BlockBlobService** objeto usando a chave de nome e uma conta de conta de armazenamento do hello.  Substitua “myaccount” e “mykey” pelo nome da sua conta e sua chave.

```python
block_blob_service = BlockBlobService(account_name='myaccount', account_key='mykey')
```

[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

Olá exemplo de código a seguir, você pode usar um **BlockBlobService** toocreate Olá contêiner se ele não existir.

```python
block_blob_service.create_container('mycontainer')
```

Por padrão, novo contêiner de saudação é privado, portanto, você deve especificar sua chave de acesso de armazenamento (como feito anteriormente) blobs toodownload desse contêiner. Se você quiser toomake blobs Olá Olá contêiner disponível tooeveryone, você pode criar contêiner de saudação e passar o nível de acesso público hello usando Olá código a seguir.

```python
from azure.storage.blob import PublicAccess
block_blob_service.create_container('mycontainer', public_access=PublicAccess.Container)
```

Como alternativa, você pode modificar um contêiner depois que você criou usando a saudação de código a seguir.

```python
block_blob_service.set_container_acl('mycontainer', public_access=PublicAccess.Container)
```

Após essa alteração, qualquer pessoa na Internet de saudação pode ver os blobs em um contêiner público, mas somente você pode modificar ou excluí-los.

## <a name="upload-a-blob-into-a-container"></a>Carregar um blob em um contêiner
toocreate um blob de bloco e carregar dados, use Olá **criar\_blob\_de\_caminho**, **criar\_blob\_de\_fluxo**, **criar\_blob\_de\_bytes** ou **criar\_blob\_de\_texto** métodos. Eles são métodos de alto nível que executam o agrupamento necessário hello quando o tamanho de saudação de dados Olá exceder 64 MB.

**criar\_blob\_de\_caminho** carregamentos Olá conteúdo de um arquivo do caminho especificado hello e **criar\_blob\_de\_fluxo** carregamentos Olá conteúdo de um arquivo já aberto/fluxo. **criar\_blob\_de\_bytes** carrega uma matriz de bytes, e **criar\_blob\_de\_texto** carrega Olá especificado valor de texto usando Olá especificado codificação (padrões tooUTF-8).

Olá, exemplo a seguir carrega conteúdo Olá Olá **sunset.png** arquivo hello **myblob** blob.

```python
from azure.storage.blob import ContentSettings
block_blob_service.create_blob_from_path(
    'mycontainer',
    'myblockblob',
    'sunset.png',
    content_settings=ContentSettings(content_type='image/png')
            )
```

## <a name="list-hello-blobs-in-a-container"></a>Saudação de listar blobs em um contêiner
blobs de saudação toolist em um contêiner, use Olá **lista\_blobs** método. Esse método retorna um gerador. Olá, código a seguir gera Olá **nome** de cada blob em um console de toohello do contêiner.

```python
generator = block_blob_service.list_blobs('mycontainer')
for blob in generator:
    print(blob.name)
```

## <a name="download-blobs"></a>Baixar blobs
toodownload dados de um blob, use **obter\_blob\_para\_caminho**, **obter\_blob\_para\_fluxo**, **obter\_blob\_para\_bytes**, ou **obter\_blob\_para\_texto**. Eles são métodos de alto nível que executam o agrupamento necessário hello quando o tamanho de saudação de dados Olá exceder 64 MB.

Olá exemplo a seguir demonstra o uso de **obter\_blob\_para\_caminho** conteúdo toodownload Olá Olá **myblob** blob e armazená-lo toohello **out sunset.png** arquivo.

```python
block_blob_service.get_blob_to_path('mycontainer', 'myblockblob', 'out-sunset.png')
```

## <a name="delete-a-blob"></a>Excluir um blob
Finalmente, toodelete um blob, chame **delete_blob**.

```python
block_blob_service.delete_blob('mycontainer', 'myblockblob')
```

## <a name="writing-tooan-append-blob"></a>Blob de acréscimo tooan de gravação
Um blob de acréscimo é otimizado para operações de acréscimo, como o registro em log. Como um blob de bloco, um blob de acréscimo é composto por blocos, mas quando você adiciona um novo blob de acréscimo de tooan de bloco, é sempre anexado toohello final de blob de saudação. Não é possível atualizar ou excluir um bloco existente em um blob de acréscimo. IDs de bloco Olá para um blob de acréscimo não são expostos como eles são para um blob de bloco.

Cada bloco em um blob de acréscimo pode ter um tamanho diferente, o máximo de tooa de 4 MB, e um blob de acréscimo pode incluir até 50.000 blocos. tamanho máximo de saudação de um blob de acréscimo, portanto, é um pouco mais de 195 GB (4 MB X 50.000 blocos).

exemplo Hello abaixo cria um novo blob de acréscimo e acrescenta alguns tooit de dados, com uma simulação de uma operação de log simples.

```python
from azure.storage.blob import AppendBlobService
append_blob_service = AppendBlobService(account_name='myaccount', account_key='mykey')

# hello same containers can hold all types of blobs
append_blob_service.create_container('mycontainer')

# Append blobs must be created before they are appended to
append_blob_service.create_blob('mycontainer', 'myappendblob')
append_blob_service.append_blob_from_text('mycontainer', 'myappendblob', u'Hello, world!')

append_blob = append_blob_service.get_blob_to_text('mycontainer', 'myappendblob')
```

## <a name="next-steps"></a>Próximas etapas
Agora que você aprendeu as Noções básicas de saudação do armazenamento de Blob, siga essas toolearn links mais.

* [Centro de desenvolvedores do Python](https://azure.microsoft.com/develop/python/)
* [API REST de serviços de armazenamento do Azure](http://msdn.microsoft.com/library/azure/dd179355)
* [Blog da equipe de Armazenamento do Azure]
* [Microsoft Azure Storage SDK para Python]

[Blog da equipe de Armazenamento do Azure]: http://blogs.msdn.com/b/windowsazurestorage/
[Microsoft Azure Storage SDK para Python]: https://github.com/Azure/azure-storage-python
