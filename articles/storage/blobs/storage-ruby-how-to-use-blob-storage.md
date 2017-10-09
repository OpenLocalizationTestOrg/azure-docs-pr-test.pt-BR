---
title: aaaHow toouse armazenamento de Blob (objeto armazenamento) de Ruby | Microsoft Docs
description: "Armazene dados não estruturados em nuvem Olá com armazenamento de BLOBs do Azure (armazenamento de objeto)."
services: storage
documentationcenter: ruby
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: e2fe4c45-27b0-4d15-b3fb-e7eb574db717
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: 776e7d788e69d4960f8dde0b783513f6b39b7a47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-ruby"></a>Como toouse armazenamento de Blob do Ruby
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>Visão geral
Armazenamento de BLOBs do Azure é um serviço que armazena dados não estruturados em nuvem hello como objetos/blobs. O Armazenamento de Blobs pode conter qualquer tipo de texto ou de dados binários, como um documento, um arquivo de mídia ou um instalador de aplicativo. Armazenamento de blob também é chamado tooas armazenamento de objeto.

Este guia mostrará como tooperform cenários comuns de usar o armazenamento de Blob. exemplos de saudação são gravados usando Olá Ruby API. Olá cenários abordados incluem **carregar, listar, baixar,** e **excluindo** blobs.

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a>Criar um aplicativo Ruby
Crie um aplicativo Ruby. Para ver as instruções, confira [Aplicativo Web Ruby on Rails em uma VM do Azure](../../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md)

## <a name="configure-your-application-tooaccess-storage"></a>Configurar o armazenamento de tooaccess do aplicativo
toouse armazenamento do Azure, você precisa toodownload e use Olá Ruby pacote do azure, que inclui um conjunto de bibliotecas de conveniência que se comunicam com serviços da REST do armazenamento hello.

### <a name="use-rubygems-tooobtain-hello-package"></a>Use o pacote de saudação do RubyGems tooobtain
1. Use uma interface de linha de comando como **PowerShell** (Windows), **Terminal** (Mac) ou **Bash** (Unix).
2. Digite "gem instalar o azure" em gem de Olá Olá comando janela tooinstall e dependências.

### <a name="import-hello-package"></a>Importar o pacote de saudação
Usando seu editor de texto favorito, adicione Olá toohello superior de saudação arquivo Ruby onde você pretende toouse armazenamento a seguir:

```ruby
require "azure"
```

## <a name="set-up-an-azure-storage-connection"></a>Configurar uma conexão do Armazenamento do Azure
módulo de saudação do azure lerá variáveis de ambiente Olá **AZURE\_armazenamento\_conta** e **AZURE\_armazenamento\_ACCESS_KEY** para as informações necessárias a conta de armazenamento do Azure tooyour tooconnect. Se essas variáveis de ambiente não forem definidas, você deve especificar informações de conta de saudação antes de usar **Azure::Blob::BlobService** com hello código a seguir:

```ruby
Azure.config.storage_account_name = "<your azure storage account>"
Azure.config.storage_access_key = "<your azure storage access key>"
```

tooobtain esses valores de um clássico ou Gerenciador de recursos de armazenamento de conta no hello portal do Azure:

1. Faça logon no toohello [portal do Azure](https://portal.azure.com).
2. Navegue toohello conta de armazenamento que você deseja toouse.
3. Na folha de configurações de saudação em saudação à direita, clique em **chaves de acesso**.
4. Olá acesso folha de chaves que aparece, você verá a chave de acesso de saudação 1 e 2 de chave de acesso. Você pode usar qualquer uma das duas.
5. Clique em Olá copiar ícone toocopy Olá chave toohello área de transferência.

## <a name="create-a-container"></a>Criar um contêiner
[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

Olá **Azure::Blob::BlobService** objeto permite que você trabalhe com contêineres e blobs. toocreate um contêiner, use Olá **criar\_container()** método.

Olá exemplo de código a seguir cria um contêiner ou imprime erro Olá se houver algum.

```ruby
azure_blob_service = Azure::Blob::BlobService.new
begin
    container = azure_blob_service.create_container("test-container")
rescue
    puts $!
end
```

Se desejar toomake Olá arquivos no contêiner Olá público, você pode definir permissões do contêiner de saudação.

Você pode modificar apenas saudação <strong>criar\_container()</strong> chamada toopass Olá **: público\_acesso\_nível** opção:

```ruby
container = azure_blob_service.create_container("test-container",
    :public_access_level => "<public access level>")
```

Os valores válidos para Olá **: público\_acesso\_nível** opção são:

* **blob:** especifica o acesso de leitura público de blobs. Os dados do blob nesse contêiner podem ser lidos por meio de solicitação anônima, mas os dados do contêiner não estão disponíveis. Os clientes não podem enumerar blobs no contêiner Olá por solicitação anônima.
* **contêiner:** especifica o acesso de leitura público completo dos dados do contêiner e de blob. Os clientes podem enumerar blobs dentro do contêiner de saudação por solicitação anônima, mas não é possível enumerar os contêineres na conta de armazenamento hello.

Como alternativa, você pode modificar o nível de acesso público de saudação de um contêiner usando **definir\_contêiner\_acl()** nível de acesso público de saudação do método toospecify.

Olá alterações Olá nível de acesso público muito do exemplo de código a seguir**contêiner**:

```ruby
azure_blob_service.set_container_acl('test-container', "container")
```

## <a name="upload-a-blob-into-a-container"></a>Carregar um blob em um contêiner
blob de conteúdo tooa tooupload, use Olá **criar\_bloco\_blob()** blob de saudação do método toocreate, usar um arquivo ou de cadeia de caracteres como conteúdo de saudação do blob hello.

Olá, código a seguir carrega o arquivo de saudação **test.png** como um novo blob denominado "blob de imagem" no contêiner de saudação.

```ruby
content = File.open("test.png", "rb") { |file| file.read }
blob = azure_blob_service.create_block_blob(container.name,
    "image-blob", content)
puts blob.name
```

## <a name="list-hello-blobs-in-a-container"></a>Saudação de listar blobs em um contêiner
contêineres de saudação toolist, use **list_containers()** método.
blobs de saudação toolist dentro de um contêiner, use **lista\_blobs()** método.

Isso gera Olá urls de todos os blobs de saudação em todos os contêineres de saudação para conta de saudação.

```ruby
containers = azure_blob_service.list_containers()
containers.each do |container|
    blobs = azure_blob_service.list_blobs(container.name)
    blobs.each do |blob|
    puts blob.name
    end
end
```

## <a name="download-blobs"></a>Baixar blobs
blobs toodownload, use Olá **obter\_blob()** conteúdo de saudação do método tooretrieve.

Olá exemplo de código a seguir demonstra o uso de **obter\_blob()** toodownload Olá conteúdo do blob"imagem" e gravar arquivo local tooa.

```ruby
blob, content = azure_blob_service.get_blob(container.name,"image-blob")
File.open("download.png","wb") {|f| f.write(content)}
```

## <a name="delete-a-blob"></a>Excluir um blob
Por fim, toodelete um blob, use Olá **excluir\_blob()** método. Olá exemplo de código a seguir demonstra como toodelete um blob.

```ruby
azure_blob_service.delete_blob(container.name, "image-blob")
```

## <a name="next-steps"></a>Próximas etapas
toolearn sobre tarefas mais complexas de armazenamento, siga estes links:

* [Blog da equipe de Armazenamento do Azure](http://blogs.msdn.com/b/windowsazurestorage/)
* [SDK do Azure para repositório Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) no GitHub
* [Transferência de dados com hello AzCopy utilitário de linha de comando](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)

