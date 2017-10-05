---
title: Desenvolvimento para o Armazenamento de Arquivos do Azure com Python | Microsoft Docs
description: "Saiba como desenvolver aplicativos e serviços Python que usam o Armazenamento de Arquivos do Azure para armazenar dados de arquivo."
services: storage
documentationcenter: python
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 297f3a14-6b3a-48b0-9da4-db5907827fb5
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: 3dd14e8d3ea7d1e50f41633a7920a6d36becf789
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="develop-for-azure-file-storage-with-python"></a>Desenvolvimento para o Armazenamento de Arquivos do Azure com Python
[!INCLUDE [storage-selector-file-include](../../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-try-azure-tools-files](../../../includes/storage-try-azure-tools-files.md)]

## <a name="about-this-tutorial"></a>Sobre este tutorial
Este tutorial demonstrará as noções básicas para usar o Python para desenvolver aplicativos ou serviços que usam o Armazenamento de Arquivos do Azure para armazenar dados de arquivo. Neste tutorial, criaremos um aplicativo de console simples e mostraremos como executar ações básicas com Python e o Armazenamento de Arquivos do Azure:

* Criar Compartilhamentos de Arquivos do Azure
* Criar diretórios
* Enumerar arquivos e diretórios em um Compartilhamento de Arquivos do Azure
* Carregar, baixar e excluir um arquivo

> [!Note]  
> Como o Armazenamento de Arquivos do Azure pode ser acessado via SMB, é possível criar aplicativos simples que acessam o Compartilhamento de Arquivos do Azure usando as classes e funções padrão de E/S do Python. Este artigo descreverá como criar aplicativos que usam o SDK do Python do Armazenamento do Azure, que usa a [API REST do Armazenamento de Arquivos do Azure](https://docs.microsoft.com/en-us/rest/api/storageservices/fileservices/file-service-rest-api) para se comunicar com o Armazenamento de Arquivos do Azure.

### <a name="set-up-your-application-to-use-azure-file-storage"></a>Configurar seu aplicativo para usar o Armazenamento de Arquivos do Azure
Adicione o seguinte próximo à parte superior de qualquer arquivo de origem Python no qual você deseja acessar o Armazenamento do Azure com programação.

```python
from azure.storage.file import FileService
```

### <a name="set-up-a-connection-to-azure-file-storage"></a>Configurar uma conexão com o Armazenamento de Arquivos do Azure 
O objeto `FileService` permite que você trabalhe com compartilhamentos, diretórios e arquivos. O código a seguir cria um objeto `FileService` usando o nome da conta de armazenamento e a chave de conta. Substitua `<myaccount>` e `<mykey>` pelo nome e pela chave da sua conta.

```python
file_service = FileService(account_name='myaccount', account_key='mykey')
```

### <a name="create-an-azure-file-share"></a>Criar um Compartilhamento de Arquivos do Azure
No exemplo de código a seguir, é possível usar um objeto `FileService` para criar o compartilhamento, se ele não existir.

```python
file_service.create_share('myshare')
```

### <a name="create-a-directory"></a>Criar um diretório
Você também pode organizar o armazenamento colocando arquivos em subdiretórios em vez de manter todos eles no diretório raiz. O Armazenamento de Arquivos do Azure permite que você crie quantos diretórios a conta permitir. O código a seguir criará um subdiretório chamado **sampledir** no diretório raiz.

```python
file_service.create_directory('myshare', 'sampledir')
```

### <a name="enumerate-files-and-directories-in-an-azure-file-share"></a>Enumerar arquivos e diretórios em um Compartilhamento de Arquivos do Azure
Para listar os arquivos e diretórios em um compartilhamento, use o método **list\_directories\_and\_files**. Esse método retorna um gerador. O código a seguir produz o **nome** de cada arquivo e diretório em um compartilhamento para o console.

```python
generator = file_service.list_directories_and_files('myshare')
for file_or_dir in generator:
    print(file_or_dir.name)
```

### <a name="upload-a-file"></a>Carregar um arquivo 
Um Compartilhamento de Arquivos do Azure contém, no mínimo, um diretório raiz em que os arquivos podem residir. Nesta seção, você aprenderá a carregar um arquivo do armazenamento local para o diretório raiz de um compartilhamento.

Para criar um arquivo e carregar dados, use os métodos `create_file_from_path`, `create_file_from_stream`, `create_file_from_bytes` ou `create_file_from_text`. Esses são métodos de alto nível que realizam a separação por partes necessária quando o tamanho do arquivo excede 64 MB.

`create_file_from_path` carrega o conteúdo de um arquivo do caminho especificado e `create_file_from_stream` carrega o conteúdo de um arquivo/fluxo já aberto. `create_file_from_bytes` carrega uma matriz de bytes e `create_file_from_text` carrega o valor do texto especificado usando a codificação especificada (padronizada para UTF-8).

O exemplo a seguir carrega o conteúdo do arquivo **sunset.png** no arquivo **myfile**.

```python
from azure.storage.file import ContentSettings
file_service.create_file_from_path(
    'myshare',
    None, # We want to create this blob in the root directory, so we specify None for the directory_name
    'myfile',
    'sunset.png',
    content_settings=ContentSettings(content_type='image/png'))
```

### <a name="download-a-file"></a>Baixar um arquivo
Para baixar dados de um arquivo, use `get_file_to_path`, `get_file_to_stream`, `get_file_to_bytes` ou `get_file_to_text`. Esses são métodos de alto nível que realizam a separação por partes necessária quando o tamanho do arquivo excede 64 MB.

O exemplo a seguir demonstra como usar `get_file_to_path` para baixar o conteúdo do arquivo **myfile** e armazená-lo no arquivo **out-sunset.png**.

```python
file_service.get_file_to_path('myshare', None, 'myfile', 'out-sunset.png')
```

### <a name="delete-a-file"></a>Excluir um arquivo
Por fim, para excluir um arquivo, chame `delete_file`.

```python
file_service.delete_file('myshare', None, 'myfile')
```

## <a name="next-steps"></a>Próximas etapas
Agora que você aprendeu como manipular o Armazenamento de Arquivos do Azure com o Python, siga estes links para saber mais.

* [Centro de desenvolvedores do Python](/develop/python/)
* [API REST de serviços de armazenamento do Azure](http://msdn.microsoft.com/library/azure/dd179355)
* [SDK do Armazenamento do Microsoft Azure para Python](https://github.com/Azure/azure-storage-python)