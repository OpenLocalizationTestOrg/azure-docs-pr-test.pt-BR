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
# <a name="how-toouse-blob-storage-from-ruby"></a><span data-ttu-id="ef55b-103">Como toouse armazenamento de Blob do Ruby</span><span class="sxs-lookup"><span data-stu-id="ef55b-103">How toouse Blob storage from Ruby</span></span>
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="ef55b-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="ef55b-104">Overview</span></span>
<span data-ttu-id="ef55b-105">Armazenamento de BLOBs do Azure é um serviço que armazena dados não estruturados em nuvem hello como objetos/blobs.</span><span class="sxs-lookup"><span data-stu-id="ef55b-105">Azure Blob storage is a service that stores unstructured data in hello cloud as objects/blobs.</span></span> <span data-ttu-id="ef55b-106">O Armazenamento de Blobs pode conter qualquer tipo de texto ou de dados binários, como um documento, um arquivo de mídia ou um instalador de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ef55b-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="ef55b-107">Armazenamento de blob também é chamado tooas armazenamento de objeto.</span><span class="sxs-lookup"><span data-stu-id="ef55b-107">Blob storage is also referred tooas object storage.</span></span>

<span data-ttu-id="ef55b-108">Este guia mostrará como tooperform cenários comuns de usar o armazenamento de Blob.</span><span class="sxs-lookup"><span data-stu-id="ef55b-108">This guide will show you how tooperform common scenarios using Blob storage.</span></span> <span data-ttu-id="ef55b-109">exemplos de saudação são gravados usando Olá Ruby API.</span><span class="sxs-lookup"><span data-stu-id="ef55b-109">hello samples are written using hello Ruby API.</span></span> <span data-ttu-id="ef55b-110">Olá cenários abordados incluem **carregar, listar, baixar,** e **excluindo** blobs.</span><span class="sxs-lookup"><span data-stu-id="ef55b-110">hello scenarios covered include **uploading, listing, downloading,** and **deleting** blobs.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a><span data-ttu-id="ef55b-111">Criar um aplicativo Ruby</span><span class="sxs-lookup"><span data-stu-id="ef55b-111">Create a Ruby application</span></span>
<span data-ttu-id="ef55b-112">Crie um aplicativo Ruby.</span><span class="sxs-lookup"><span data-stu-id="ef55b-112">Create a Ruby application.</span></span> <span data-ttu-id="ef55b-113">Para ver as instruções, confira [Aplicativo Web Ruby on Rails em uma VM do Azure](../../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md)</span><span class="sxs-lookup"><span data-stu-id="ef55b-113">For instructions, see [Ruby on Rails Web application on an Azure VM](../../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md)</span></span>

## <a name="configure-your-application-tooaccess-storage"></a><span data-ttu-id="ef55b-114">Configurar o armazenamento de tooaccess do aplicativo</span><span class="sxs-lookup"><span data-stu-id="ef55b-114">Configure your application tooaccess Storage</span></span>
<span data-ttu-id="ef55b-115">toouse armazenamento do Azure, você precisa toodownload e use Olá Ruby pacote do azure, que inclui um conjunto de bibliotecas de conveniência que se comunicam com serviços da REST do armazenamento hello.</span><span class="sxs-lookup"><span data-stu-id="ef55b-115">toouse Azure Storage, you need toodownload and use hello Ruby azure package, which includes a set of convenience libraries that communicate with hello storage REST services.</span></span>

### <a name="use-rubygems-tooobtain-hello-package"></a><span data-ttu-id="ef55b-116">Use o pacote de saudação do RubyGems tooobtain</span><span class="sxs-lookup"><span data-stu-id="ef55b-116">Use RubyGems tooobtain hello package</span></span>
1. <span data-ttu-id="ef55b-117">Use uma interface de linha de comando como **PowerShell** (Windows), **Terminal** (Mac) ou **Bash** (Unix).</span><span class="sxs-lookup"><span data-stu-id="ef55b-117">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix).</span></span>
2. <span data-ttu-id="ef55b-118">Digite "gem instalar o azure" em gem de Olá Olá comando janela tooinstall e dependências.</span><span class="sxs-lookup"><span data-stu-id="ef55b-118">Type "gem install azure" in hello command window tooinstall hello gem and dependencies.</span></span>

### <a name="import-hello-package"></a><span data-ttu-id="ef55b-119">Importar o pacote de saudação</span><span class="sxs-lookup"><span data-stu-id="ef55b-119">Import hello package</span></span>
<span data-ttu-id="ef55b-120">Usando seu editor de texto favorito, adicione Olá toohello superior de saudação arquivo Ruby onde você pretende toouse armazenamento a seguir:</span><span class="sxs-lookup"><span data-stu-id="ef55b-120">Using your favorite text editor, add hello following toohello top of hello Ruby file where you intend toouse storage:</span></span>

```ruby
require "azure"
```

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="ef55b-121">Configurar uma conexão do Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="ef55b-121">Set up an Azure Storage Connection</span></span>
<span data-ttu-id="ef55b-122">módulo de saudação do azure lerá variáveis de ambiente Olá **AZURE\_armazenamento\_conta** e **AZURE\_armazenamento\_ACCESS_KEY** para as informações necessárias a conta de armazenamento do Azure tooyour tooconnect.</span><span class="sxs-lookup"><span data-stu-id="ef55b-122">hello azure module will read hello environment variables **AZURE\_STORAGE\_ACCOUNT** and **AZURE\_STORAGE\_ACCESS_KEY** for information required tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="ef55b-123">Se essas variáveis de ambiente não forem definidas, você deve especificar informações de conta de saudação antes de usar **Azure::Blob::BlobService** com hello código a seguir:</span><span class="sxs-lookup"><span data-stu-id="ef55b-123">If these environment variables are not set, you must specify hello account information before using **Azure::Blob::BlobService** with hello following code:</span></span>

```ruby
Azure.config.storage_account_name = "<your azure storage account>"
Azure.config.storage_access_key = "<your azure storage access key>"
```

<span data-ttu-id="ef55b-124">tooobtain esses valores de um clássico ou Gerenciador de recursos de armazenamento de conta no hello portal do Azure:</span><span class="sxs-lookup"><span data-stu-id="ef55b-124">tooobtain these values from a classic or Resource Manager storage account in hello Azure portal:</span></span>

1. <span data-ttu-id="ef55b-125">Faça logon no toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ef55b-125">Log in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="ef55b-126">Navegue toohello conta de armazenamento que você deseja toouse.</span><span class="sxs-lookup"><span data-stu-id="ef55b-126">Navigate toohello storage account you want toouse.</span></span>
3. <span data-ttu-id="ef55b-127">Na folha de configurações de saudação em saudação à direita, clique em **chaves de acesso**.</span><span class="sxs-lookup"><span data-stu-id="ef55b-127">In hello Settings blade on hello right, click **Access Keys**.</span></span>
4. <span data-ttu-id="ef55b-128">Olá acesso folha de chaves que aparece, você verá a chave de acesso de saudação 1 e 2 de chave de acesso.</span><span class="sxs-lookup"><span data-stu-id="ef55b-128">In hello Access keys blade that appears, you'll see hello access key 1 and access key 2.</span></span> <span data-ttu-id="ef55b-129">Você pode usar qualquer uma das duas.</span><span class="sxs-lookup"><span data-stu-id="ef55b-129">You can use either of these.</span></span>
5. <span data-ttu-id="ef55b-130">Clique em Olá copiar ícone toocopy Olá chave toohello área de transferência.</span><span class="sxs-lookup"><span data-stu-id="ef55b-130">Click hello copy icon toocopy hello key toohello clipboard.</span></span>

## <a name="create-a-container"></a><span data-ttu-id="ef55b-131">Criar um contêiner</span><span class="sxs-lookup"><span data-stu-id="ef55b-131">Create a container</span></span>
[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="ef55b-132">Olá **Azure::Blob::BlobService** objeto permite que você trabalhe com contêineres e blobs.</span><span class="sxs-lookup"><span data-stu-id="ef55b-132">hello **Azure::Blob::BlobService** object lets you work with containers and blobs.</span></span> <span data-ttu-id="ef55b-133">toocreate um contêiner, use Olá **criar\_container()** método.</span><span class="sxs-lookup"><span data-stu-id="ef55b-133">toocreate a container, use hello **create\_container()** method.</span></span>

<span data-ttu-id="ef55b-134">Olá exemplo de código a seguir cria um contêiner ou imprime erro Olá se houver algum.</span><span class="sxs-lookup"><span data-stu-id="ef55b-134">hello following code example creates a container or prints hello error if there is any.</span></span>

```ruby
azure_blob_service = Azure::Blob::BlobService.new
begin
    container = azure_blob_service.create_container("test-container")
rescue
    puts $!
end
```

<span data-ttu-id="ef55b-135">Se desejar toomake Olá arquivos no contêiner Olá público, você pode definir permissões do contêiner de saudação.</span><span class="sxs-lookup"><span data-stu-id="ef55b-135">If you want toomake hello files in hello container public, you can set hello container's permissions.</span></span>

<span data-ttu-id="ef55b-136">Você pode modificar apenas saudação <strong>criar\_container()</strong> chamada toopass Olá **: público\_acesso\_nível** opção:</span><span class="sxs-lookup"><span data-stu-id="ef55b-136">You can just modify hello <strong>create\_container()</strong> call toopass hello **:public\_access\_level** option:</span></span>

```ruby
container = azure_blob_service.create_container("test-container",
    :public_access_level => "<public access level>")
```

<span data-ttu-id="ef55b-137">Os valores válidos para Olá **: público\_acesso\_nível** opção são:</span><span class="sxs-lookup"><span data-stu-id="ef55b-137">Valid values for hello **:public\_access\_level** option are:</span></span>

* <span data-ttu-id="ef55b-138">**blob:** especifica o acesso de leitura público de blobs.</span><span class="sxs-lookup"><span data-stu-id="ef55b-138">**blob:** Specifies public read access for blobs.</span></span> <span data-ttu-id="ef55b-139">Os dados do blob nesse contêiner podem ser lidos por meio de solicitação anônima, mas os dados do contêiner não estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="ef55b-139">Blob data within this container can be read via anonymous request, but container data is not available.</span></span> <span data-ttu-id="ef55b-140">Os clientes não podem enumerar blobs no contêiner Olá por solicitação anônima.</span><span class="sxs-lookup"><span data-stu-id="ef55b-140">Clients cannot enumerate blobs within hello container via anonymous request.</span></span>
* <span data-ttu-id="ef55b-141">**contêiner:** especifica o acesso de leitura público completo dos dados do contêiner e de blob.</span><span class="sxs-lookup"><span data-stu-id="ef55b-141">**container:** Specifies full public read access for container and blob data.</span></span> <span data-ttu-id="ef55b-142">Os clientes podem enumerar blobs dentro do contêiner de saudação por solicitação anônima, mas não é possível enumerar os contêineres na conta de armazenamento hello.</span><span class="sxs-lookup"><span data-stu-id="ef55b-142">Clients can enumerate blobs within hello container via anonymous request, but cannot enumerate containers within hello storage account.</span></span>

<span data-ttu-id="ef55b-143">Como alternativa, você pode modificar o nível de acesso público de saudação de um contêiner usando **definir\_contêiner\_acl()** nível de acesso público de saudação do método toospecify.</span><span class="sxs-lookup"><span data-stu-id="ef55b-143">Alternatively, you can modify hello public access level of a container by using **set\_container\_acl()** method toospecify hello public access level.</span></span>

<span data-ttu-id="ef55b-144">Olá alterações Olá nível de acesso público muito do exemplo de código a seguir**contêiner**:</span><span class="sxs-lookup"><span data-stu-id="ef55b-144">hello following code example changes hello public access level too**container**:</span></span>

```ruby
azure_blob_service.set_container_acl('test-container', "container")
```

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="ef55b-145">Carregar um blob em um contêiner</span><span class="sxs-lookup"><span data-stu-id="ef55b-145">Upload a blob into a container</span></span>
<span data-ttu-id="ef55b-146">blob de conteúdo tooa tooupload, use Olá **criar\_bloco\_blob()** blob de saudação do método toocreate, usar um arquivo ou de cadeia de caracteres como conteúdo de saudação do blob hello.</span><span class="sxs-lookup"><span data-stu-id="ef55b-146">tooupload content tooa blob, use hello **create\_block\_blob()** method toocreate hello blob, use a file or string as hello content of hello blob.</span></span>

<span data-ttu-id="ef55b-147">Olá, código a seguir carrega o arquivo de saudação **test.png** como um novo blob denominado "blob de imagem" no contêiner de saudação.</span><span class="sxs-lookup"><span data-stu-id="ef55b-147">hello following code uploads hello file **test.png** as a new blob named "image-blob" in hello container.</span></span>

```ruby
content = File.open("test.png", "rb") { |file| file.read }
blob = azure_blob_service.create_block_blob(container.name,
    "image-blob", content)
puts blob.name
```

## <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="ef55b-148">Saudação de listar blobs em um contêiner</span><span class="sxs-lookup"><span data-stu-id="ef55b-148">List hello blobs in a container</span></span>
<span data-ttu-id="ef55b-149">contêineres de saudação toolist, use **list_containers()** método.</span><span class="sxs-lookup"><span data-stu-id="ef55b-149">toolist hello containers, use **list_containers()** method.</span></span>
<span data-ttu-id="ef55b-150">blobs de saudação toolist dentro de um contêiner, use **lista\_blobs()** método.</span><span class="sxs-lookup"><span data-stu-id="ef55b-150">toolist hello blobs within a container, use **list\_blobs()** method.</span></span>

<span data-ttu-id="ef55b-151">Isso gera Olá urls de todos os blobs de saudação em todos os contêineres de saudação para conta de saudação.</span><span class="sxs-lookup"><span data-stu-id="ef55b-151">This outputs hello urls of all hello blobs in all hello containers for hello account.</span></span>

```ruby
containers = azure_blob_service.list_containers()
containers.each do |container|
    blobs = azure_blob_service.list_blobs(container.name)
    blobs.each do |blob|
    puts blob.name
    end
end
```

## <a name="download-blobs"></a><span data-ttu-id="ef55b-152">Baixar blobs</span><span class="sxs-lookup"><span data-stu-id="ef55b-152">Download blobs</span></span>
<span data-ttu-id="ef55b-153">blobs toodownload, use Olá **obter\_blob()** conteúdo de saudação do método tooretrieve.</span><span class="sxs-lookup"><span data-stu-id="ef55b-153">toodownload blobs, use hello **get\_blob()** method tooretrieve hello contents.</span></span>

<span data-ttu-id="ef55b-154">Olá exemplo de código a seguir demonstra o uso de **obter\_blob()** toodownload Olá conteúdo do blob"imagem" e gravar arquivo local tooa.</span><span class="sxs-lookup"><span data-stu-id="ef55b-154">hello following code example demonstrates using **get\_blob()** toodownload hello contents of "image-blob" and write it tooa local file.</span></span>

```ruby
blob, content = azure_blob_service.get_blob(container.name,"image-blob")
File.open("download.png","wb") {|f| f.write(content)}
```

## <a name="delete-a-blob"></a><span data-ttu-id="ef55b-155">Excluir um blob</span><span class="sxs-lookup"><span data-stu-id="ef55b-155">Delete a Blob</span></span>
<span data-ttu-id="ef55b-156">Por fim, toodelete um blob, use Olá **excluir\_blob()** método.</span><span class="sxs-lookup"><span data-stu-id="ef55b-156">Finally, toodelete a blob, use hello **delete\_blob()** method.</span></span> <span data-ttu-id="ef55b-157">Olá exemplo de código a seguir demonstra como toodelete um blob.</span><span class="sxs-lookup"><span data-stu-id="ef55b-157">hello following code example demonstrates how toodelete a blob.</span></span>

```ruby
azure_blob_service.delete_blob(container.name, "image-blob")
```

## <a name="next-steps"></a><span data-ttu-id="ef55b-158">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ef55b-158">Next steps</span></span>
<span data-ttu-id="ef55b-159">toolearn sobre tarefas mais complexas de armazenamento, siga estes links:</span><span class="sxs-lookup"><span data-stu-id="ef55b-159">toolearn about more complex storage tasks, follow these links:</span></span>

* [<span data-ttu-id="ef55b-160">Blog da equipe de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="ef55b-160">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)
* <span data-ttu-id="ef55b-161">[SDK do Azure para repositório Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) no GitHub</span><span class="sxs-lookup"><span data-stu-id="ef55b-161">[Azure SDK for Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) repository on GitHub</span></span>
* [<span data-ttu-id="ef55b-162">Transferência de dados com hello AzCopy utilitário de linha de comando</span><span class="sxs-lookup"><span data-stu-id="ef55b-162">Transfer data with hello AzCopy Command-Line Utility</span></span>](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)

