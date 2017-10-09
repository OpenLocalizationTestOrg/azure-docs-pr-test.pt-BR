---
title: aaaDevelop para armazenamento de arquivo do Azure com Python | Microsoft Docs
description: "Saiba como aplicativos de Python toodevelop e serviços que usam toostore de armazenamento do Azure arquivo dados de arquivos."
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
ms.openlocfilehash: 45623e6dbec6f140cedc4e58e56a93fb4af9054e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-for-azure-file-storage-with-python"></a>Desenvolvimento para o Armazenamento de Arquivos do Azure com Python
[!INCLUDE [storage-selector-file-include](../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-try-azure-tools-files](../../includes/storage-try-azure-tools-files.md)]

## <a name="about-this-tutorial"></a>Sobre este tutorial
Este tutorial demonstra Noções básicas de saudação do uso de aplicativos do Python toodevelop ou serviços que usam dados de arquivo de toostore de armazenamento de arquivo do Azure. Neste tutorial, vamos criar um aplicativo de console simples e mostram como ações básicas de tooperform com armazenamento Python e o arquivo do Azure:

* Criar Compartilhamentos de Arquivos do Azure
* Criar diretórios
* Enumerar arquivos e diretórios em um Compartilhamento de Arquivos do Azure
* Carregar, baixar e excluir um arquivo

> [!Note]  
> Como armazenamento de arquivo do Azure pode ser acessado via SMB, é possível toowrite aplicativos simples que acessar o compartilhamento de arquivo do Azure hello usando funções e classes de e/s do Python padrão hello. Este artigo descreve como aplicativos toowrite que usam Olá SDK de Python do armazenamento do Azure, que usa Olá [armazenamento de arquivo do Azure API REST](https://docs.microsoft.com/en-us/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure o armazenamento de arquivos.

### <a name="set-up-your-application-toouse-azure-file-storage"></a>Configurar seu aplicativo toouse armazenamento de arquivo do Azure
Adicione a seguinte Olá superior Olá qualquer Python do arquivo de origem no qual você deseja acesso tooprogrammatically armazenamento do Azure.

```python
from azure.storage.file import FileService
```

### <a name="set-up-a-connection-tooazure-file-storage"></a>Configurar uma conexão tooAzure armazenamento de arquivo 
Olá `FileService` objeto permite que você trabalhe com compartilhamentos, diretórios e arquivos. Olá código a seguir cria um `FileService` objeto usando a chave de nome e uma conta de conta de armazenamento do hello. Substitua `<myaccount>` e `<mykey>` pelo nome e pela chave da sua conta.

```python
file_service = FileService(account_name='myaccount', account_key='mykey')
```

### <a name="create-an-azure-file-share"></a>Criar um Compartilhamento de Arquivos do Azure
Olá exemplo de código a seguir, você pode usar um `FileService` compartilhamento de saudação do objeto toocreate se ele não existir.

```python
file_service.create_share('myshare')
```

### <a name="create-a-directory"></a>Criar um diretório
Você também pode organizar o armazenamento, colocando arquivos nos subdiretórios em vez de ter todos eles no diretório raiz de saudação. Armazenamento de arquivo do Azure permite que você toocreate como permitir que vários diretórios como será sua conta. saudação de código abaixo cria um subdiretório chamado **sampledir** no diretório raiz de saudação.

```python
file_service.create_directory('myshare', 'sampledir')
```

### <a name="enumerate-files-and-directories-in-an-azure-file-share"></a>Enumerar arquivos e diretórios em um Compartilhamento de Arquivos do Azure
arquivos de saudação do toolist e diretórios em um compartilhamento, use Olá **lista\_diretórios\_e\_arquivos** método. Esse método retorna um gerador. Olá, código a seguir gera Olá **nome** de cada arquivo e diretório em um console de toohello de compartilhamento.

```python
generator = file_service.list_directories_and_files('myshare')
for file_or_dir in generator:
    print(file_or_dir.name)
```

### <a name="upload-a-file"></a>Carregar um arquivo 
Arquivo do Azure compartilhamento contém em Olá muito menos, um diretório raiz onde os arquivos podem residir. Nesta seção, você aprenderá como o diretório de um compartilhamento de raiz tooupload um arquivo do armazenamento local para hello.

toocreate um arquivo e carregar dados, use Olá `create_file_from_path`, `create_file_from_stream`, `create_file_from_bytes` ou `create_file_from_text` métodos. Eles são métodos de alto nível que executam o agrupamento necessário hello quando o tamanho de saudação de dados Olá exceder 64 MB.

`create_file_from_path`carregamentos Olá conteúdo de um arquivo do caminho especificado hello e `create_file_from_stream` carregamentos Olá conteúdo de um arquivo já aberto/fluxo. `create_file_from_bytes`carrega uma matriz de bytes, e `create_file_from_text` carregamentos Olá especificado valor de texto usando Olá especificado codificação (padrões tooUTF-8).

Olá, exemplo a seguir carrega conteúdo Olá Olá **sunset.png** arquivo hello **myfile** arquivo.

```python
from azure.storage.file import ContentSettings
file_service.create_file_from_path(
    'myshare',
    None, # We want toocreate this blob in hello root directory, so we specify None for hello directory_name
    'myfile',
    'sunset.png',
    content_settings=ContentSettings(content_type='image/png'))
```

### <a name="download-a-file"></a>Baixar um arquivo
toodownload dados de um arquivo, use `get_file_to_path`, `get_file_to_stream`, `get_file_to_bytes`, ou `get_file_to_text`. Eles são métodos de alto nível que executam o agrupamento necessário hello quando o tamanho de saudação de dados Olá exceder 64 MB.

Olá exemplo a seguir demonstra o uso de `get_file_to_path` conteúdo toodownload Olá Olá **myfile** de arquivos e armazená-lo toohello **sunset.png fora** arquivo.

```python
file_service.get_file_to_path('myshare', None, 'myfile', 'out-sunset.png')
```

### <a name="delete-a-file"></a>Excluir um arquivo
Finalmente, toodelete um arquivo, chame `delete_file`.

```python
file_service.delete_file('myshare', None, 'myfile')
```

## <a name="next-steps"></a>Próximas etapas
Agora que você aprendeu como toomanipulate armazenamento de arquivo do Azure com o Python, siga essas toolearn links mais.

* [Centro de desenvolvedores do Python](/develop/python/)
* [API REST de serviços de armazenamento do Azure](http://msdn.microsoft.com/library/azure/dd179355)
* [SDK do Armazenamento do Microsoft Azure para Python](https://github.com/Azure/azure-storage-python)