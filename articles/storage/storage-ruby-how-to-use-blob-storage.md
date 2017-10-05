---
title: Como usar o Armazenamento de Blobs (armazenamento de objeto) do Ruby | Microsoft Docs
description: "Armazene dados não estruturados na nuvem com o armazenamento de blobs do Azure (armazenamento de objeto)."
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
ms.openlocfilehash: 7f7d0c52b2b50a360711477e8e0eafc07ddcf374
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-blob-storage-from-ruby"></a><span data-ttu-id="f8e91-103">Como usar o Armazenamento de blob no Ruby</span><span class="sxs-lookup"><span data-stu-id="f8e91-103">How to use Blob storage from Ruby</span></span>
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="f8e91-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="f8e91-104">Overview</span></span>
<span data-ttu-id="f8e91-105">O Armazenamento de Blobs do Azure é um serviço que armazena dados não estruturados na nuvem como objetos/blobs.</span><span class="sxs-lookup"><span data-stu-id="f8e91-105">Azure Blob storage is a service that stores unstructured data in the cloud as objects/blobs.</span></span> <span data-ttu-id="f8e91-106">O Armazenamento de Blobs pode conter qualquer tipo de texto ou de dados binários, como um documento, um arquivo de mídia ou um instalador de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f8e91-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="f8e91-107">O Armazenamento de Blobs também é chamado de armazenamento de objeto.</span><span class="sxs-lookup"><span data-stu-id="f8e91-107">Blob storage is also referred to as object storage.</span></span>

<span data-ttu-id="f8e91-108">Este guia mostra como executar cenários comuns usando o Armazenamento de Blobs.</span><span class="sxs-lookup"><span data-stu-id="f8e91-108">This guide will show you how to perform common scenarios using Blob storage.</span></span> <span data-ttu-id="f8e91-109">Os exemplos de código são gravados com a API do Ruby.</span><span class="sxs-lookup"><span data-stu-id="f8e91-109">The samples are written using the Ruby API.</span></span> <span data-ttu-id="f8e91-110">Os cenários abrangidos incluem **carregar, listar, baixar** e **excluir** blobs.</span><span class="sxs-lookup"><span data-stu-id="f8e91-110">The scenarios covered include **uploading, listing, downloading,** and **deleting** blobs.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a><span data-ttu-id="f8e91-111">Criar um aplicativo Ruby</span><span class="sxs-lookup"><span data-stu-id="f8e91-111">Create a Ruby application</span></span>
<span data-ttu-id="f8e91-112">Crie um aplicativo Ruby.</span><span class="sxs-lookup"><span data-stu-id="f8e91-112">Create a Ruby application.</span></span> <span data-ttu-id="f8e91-113">Para ver as instruções, confira [Aplicativo Web Ruby on Rails em uma VM do Azure](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md)</span><span class="sxs-lookup"><span data-stu-id="f8e91-113">For instructions, see [Ruby on Rails Web application on an Azure VM](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md)</span></span>

## <a name="configure-your-application-to-access-storage"></a><span data-ttu-id="f8e91-114">Configurar seu aplicativo para acessar o Armazenamento</span><span class="sxs-lookup"><span data-stu-id="f8e91-114">Configure your application to access Storage</span></span>
<span data-ttu-id="f8e91-115">Para usar o Armazenamento do Azure, você deverá baixar e usar o pacote do Azure do Ruby, que inclui um conjunto de bibliotecas convenientes que se comunicam com os serviços REST do armazenamento.</span><span class="sxs-lookup"><span data-stu-id="f8e91-115">To use Azure Storage, you need to download and use the Ruby azure package, which includes a set of convenience libraries that communicate with the storage REST services.</span></span>

### <a name="use-rubygems-to-obtain-the-package"></a><span data-ttu-id="f8e91-116">Usar RubyGems para obter o pacote</span><span class="sxs-lookup"><span data-stu-id="f8e91-116">Use RubyGems to obtain the package</span></span>
1. <span data-ttu-id="f8e91-117">Use uma interface de linha de comando como **PowerShell** (Windows), **Terminal** (Mac) ou **Bash** (Unix).</span><span class="sxs-lookup"><span data-stu-id="f8e91-117">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix).</span></span>
2. <span data-ttu-id="f8e91-118">Digite "gem install azure" na janela de comandos para instalar a gema e as dependências.</span><span class="sxs-lookup"><span data-stu-id="f8e91-118">Type "gem install azure" in the command window to install the gem and dependencies.</span></span>

### <a name="import-the-package"></a><span data-ttu-id="f8e91-119">Importar o pacote</span><span class="sxs-lookup"><span data-stu-id="f8e91-119">Import the package</span></span>
<span data-ttu-id="f8e91-120">Usando seu editor de texto favorito, adicione o seguinte na parte superior do arquivo do Ruby no qual você pretende usar o armazenamento:</span><span class="sxs-lookup"><span data-stu-id="f8e91-120">Using your favorite text editor, add the following to the top of the Ruby file where you intend to use storage:</span></span>

```ruby
require "azure"
```

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="f8e91-121">Configurar uma conexão do Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="f8e91-121">Set up an Azure Storage Connection</span></span>
<span data-ttu-id="f8e91-122">O módulo do Azure lerá as variáveis de ambiente **AZURE\_STORAGE\_ACCOUNT** e **AZURE\_STORAGE\_ACCESS_KEY** para obter as informações necessárias para se conectar à sua conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="f8e91-122">The azure module will read the environment variables **AZURE\_STORAGE\_ACCOUNT** and **AZURE\_STORAGE\_ACCESS_KEY** for information required to connect to your Azure storage account.</span></span> <span data-ttu-id="f8e91-123">Se essas variáveis de ambiente não forem definidas, você deverá especificar as informações da conta antes de usar **Azure::Blob::BlobService** com o seguinte código:</span><span class="sxs-lookup"><span data-stu-id="f8e91-123">If these environment variables are not set, you must specify the account information before using **Azure::Blob::BlobService** with the following code:</span></span>

```ruby
Azure.config.storage_account_name = "<your azure storage account>"
Azure.config.storage_access_key = "<your azure storage access key>"
```

<span data-ttu-id="f8e91-124">Para obter esses valores de uma conta de armazenamento clássico ou do Resource Manager no Portal do Azure:</span><span class="sxs-lookup"><span data-stu-id="f8e91-124">To obtain these values from a classic or Resource Manager storage account in the Azure portal:</span></span>

1. <span data-ttu-id="f8e91-125">Faça logon no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f8e91-125">Log in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="f8e91-126">Navegue até a conta de armazenamento que você deseja usar.</span><span class="sxs-lookup"><span data-stu-id="f8e91-126">Navigate to the storage account you want to use.</span></span>
3. <span data-ttu-id="f8e91-127">Na folha Configurações no lado direito, clique em **Chaves de Acesso**.</span><span class="sxs-lookup"><span data-stu-id="f8e91-127">In the Settings blade on the right, click **Access Keys**.</span></span>
4. <span data-ttu-id="f8e91-128">Na folha Acessar chaves exibida, você verá as teclas de acesso 1 e 2.</span><span class="sxs-lookup"><span data-stu-id="f8e91-128">In the Access keys blade that appears, you'll see the access key 1 and access key 2.</span></span> <span data-ttu-id="f8e91-129">Você pode usar qualquer uma das duas.</span><span class="sxs-lookup"><span data-stu-id="f8e91-129">You can use either of these.</span></span>
5. <span data-ttu-id="f8e91-130">Clique no ícone de cópia para copiar a chave para a área de transferência.</span><span class="sxs-lookup"><span data-stu-id="f8e91-130">Click the copy icon to copy the key to the clipboard.</span></span>

<span data-ttu-id="f8e91-131">Para obter esses valores de uma conta de armazenamento clássico no Portal Clássico do Azure:</span><span class="sxs-lookup"><span data-stu-id="f8e91-131">To obtain these values from a classic storage account in the classic Azure portal:</span></span>

1. <span data-ttu-id="f8e91-132">Faça logon no [Portal Clássico do Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="f8e91-132">Log in to the [classic Azure portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="f8e91-133">Navegue até a conta de armazenamento que você deseja usar.</span><span class="sxs-lookup"><span data-stu-id="f8e91-133">Navigate to the storage account you want to use.</span></span>
3. <span data-ttu-id="f8e91-134">Clique em **GERENCIAR CHAVES DE ACESSO** na parte inferior do painel de navegação.</span><span class="sxs-lookup"><span data-stu-id="f8e91-134">Click **MANAGE ACCESS KEYS** at the bottom of the navigation pane.</span></span>
4. <span data-ttu-id="f8e91-135">Na caixa de diálogo pop-up, você verá o nome da conta de armazenamento, a tecla de acesso primária e a tecla de acesso secundária.</span><span class="sxs-lookup"><span data-stu-id="f8e91-135">In the pop-up dialog, you'll see the storage account name, primary access key and secondary access key.</span></span> <span data-ttu-id="f8e91-136">Para a chave de acesso, você pode usar tanto a primária quanto a secundária.</span><span class="sxs-lookup"><span data-stu-id="f8e91-136">For access key, you can use either the primary one or the secondary one.</span></span>
5. <span data-ttu-id="f8e91-137">Clique no ícone de cópia para copiar a chave para a área de transferência.</span><span class="sxs-lookup"><span data-stu-id="f8e91-137">Click the copy icon to copy the key to the clipboard.</span></span>

## <a name="create-a-container"></a><span data-ttu-id="f8e91-138">Criar um contêiner</span><span class="sxs-lookup"><span data-stu-id="f8e91-138">Create a container</span></span>
[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="f8e91-139">O objeto **Azure::Blob::BlobService** permite que você trabalhe com contêineres e blobs.</span><span class="sxs-lookup"><span data-stu-id="f8e91-139">The **Azure::Blob::BlobService** object lets you work with containers and blobs.</span></span> <span data-ttu-id="f8e91-140">Para criar um contêiner, use o método **create\_container()**.</span><span class="sxs-lookup"><span data-stu-id="f8e91-140">To create a container, use the **create\_container()** method.</span></span>

<span data-ttu-id="f8e91-141">O exemplo de código a seguir cria um contêiner ou imprime o erro, se houver.</span><span class="sxs-lookup"><span data-stu-id="f8e91-141">The following code example creates a container or prints the error if there is any.</span></span>

```ruby
azure_blob_service = Azure::Blob::BlobService.new
begin
    container = azure_blob_service.create_container("test-container")
rescue
    puts $!
end
```

<span data-ttu-id="f8e91-142">Se desejar tornar públicos os arquivos do contêiner, você pode definir as permissões do contêiner.</span><span class="sxs-lookup"><span data-stu-id="f8e91-142">If you want to make the files in the container public, you can set the container's permissions.</span></span>

<span data-ttu-id="f8e91-143">Você pode modificar apenas a chamada <strong>create\_container()</strong> para passar a opção **:public\_access\_level**:</span><span class="sxs-lookup"><span data-stu-id="f8e91-143">You can just modify the <strong>create\_container()</strong> call to pass the **:public\_access\_level** option:</span></span>

```ruby
container = azure_blob_service.create_container("test-container",
    :public_access_level => "<public access level>")
```

<span data-ttu-id="f8e91-144">Os valores válidos da opção **:public\_access\_level** são:</span><span class="sxs-lookup"><span data-stu-id="f8e91-144">Valid values for the **:public\_access\_level** option are:</span></span>

* <span data-ttu-id="f8e91-145">**blob:** especifica o acesso de leitura público de blobs.</span><span class="sxs-lookup"><span data-stu-id="f8e91-145">**blob:** Specifies public read access for blobs.</span></span> <span data-ttu-id="f8e91-146">Os dados do blob nesse contêiner podem ser lidos por meio de solicitação anônima, mas os dados do contêiner não estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="f8e91-146">Blob data within this container can be read via anonymous request, but container data is not available.</span></span> <span data-ttu-id="f8e91-147">Os clientes não podem enumerar os blobs no contêiner por meio de uma solicitação anônima.</span><span class="sxs-lookup"><span data-stu-id="f8e91-147">Clients cannot enumerate blobs within the container via anonymous request.</span></span>
* <span data-ttu-id="f8e91-148">**contêiner:** especifica o acesso de leitura público completo dos dados do contêiner e de blob.</span><span class="sxs-lookup"><span data-stu-id="f8e91-148">**container:** Specifies full public read access for container and blob data.</span></span> <span data-ttu-id="f8e91-149">Os clientes podem enumerar os blobs no contêiner por meio de uma solicitação anônima, mas não podem enumerar os contêineres em uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="f8e91-149">Clients can enumerate blobs within the container via anonymous request, but cannot enumerate containers within the storage account.</span></span>

<span data-ttu-id="f8e91-150">Você também pode modificar o nível de acesso público de um contêiner usando **set\_container\_acl()** para especificar o nível de acesso público.</span><span class="sxs-lookup"><span data-stu-id="f8e91-150">Alternatively, you can modify the public access level of a container by using **set\_container\_acl()** method to specify the public access level.</span></span>

<span data-ttu-id="f8e91-151">O exemplo a seguir altera o nível de acesso público para **contêiner**:</span><span class="sxs-lookup"><span data-stu-id="f8e91-151">The following code example changes the public access level to **container**:</span></span>

```ruby
azure_blob_service.set_container_acl('test-container', "container")
```

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="f8e91-152">Carregar um blob em um contêiner</span><span class="sxs-lookup"><span data-stu-id="f8e91-152">Upload a blob into a container</span></span>
<span data-ttu-id="f8e91-153">Para carregar o conteúdo em um blob, use o método **create\_block\_blob()** para criar o blob e use um arquivo ou uma cadeia como o conteúdo do blob.</span><span class="sxs-lookup"><span data-stu-id="f8e91-153">To upload content to a blob, use the **create\_block\_blob()** method to create the blob, use a file or string as the content of the blob.</span></span>

<span data-ttu-id="f8e91-154">O código a seguir carrega o arquivo **test.png** como um novo blob chamado "image-blob" no contêiner.</span><span class="sxs-lookup"><span data-stu-id="f8e91-154">The following code uploads the file **test.png** as a new blob named "image-blob" in the container.</span></span>

```ruby
content = File.open("test.png", "rb") { |file| file.read }
blob = azure_blob_service.create_block_blob(container.name,
    "image-blob", content)
puts blob.name
```

## <a name="list-the-blobs-in-a-container"></a><span data-ttu-id="f8e91-155">Listar os blobs em um contêiner</span><span class="sxs-lookup"><span data-stu-id="f8e91-155">List the blobs in a container</span></span>
<span data-ttu-id="f8e91-156">Para listar os contêineres, use o método **list_containers()**.</span><span class="sxs-lookup"><span data-stu-id="f8e91-156">To list the containers, use **list_containers()** method.</span></span>
<span data-ttu-id="f8e91-157">Para listar os blobs em um contêiner, use o método **list\_blobs()**.</span><span class="sxs-lookup"><span data-stu-id="f8e91-157">To list the blobs within a container, use **list\_blobs()** method.</span></span>

<span data-ttu-id="f8e91-158">Ele envia as urls de todos os blobs em todos os contêineres à conta.</span><span class="sxs-lookup"><span data-stu-id="f8e91-158">This outputs the urls of all the blobs in all the containers for the account.</span></span>

```ruby
containers = azure_blob_service.list_containers()
containers.each do |container|
    blobs = azure_blob_service.list_blobs(container.name)
    blobs.each do |blob|
    puts blob.name
    end
end
```

## <a name="download-blobs"></a><span data-ttu-id="f8e91-159">Baixar blobs</span><span class="sxs-lookup"><span data-stu-id="f8e91-159">Download blobs</span></span>
<span data-ttu-id="f8e91-160">Para baixar blobs, use o método **get\_blob()** para recuperar o conteúdo.</span><span class="sxs-lookup"><span data-stu-id="f8e91-160">To download blobs, use the **get\_blob()** method to retrieve the contents.</span></span>

<span data-ttu-id="f8e91-161">O exemplo a seguir demonstra o uso de **get\_blob()** para baixar o conteúdo de "image-blob" e gravá-lo em um arquivo local.</span><span class="sxs-lookup"><span data-stu-id="f8e91-161">The following code example demonstrates using **get\_blob()** to download the contents of "image-blob" and write it to a local file.</span></span>

```ruby
blob, content = azure_blob_service.get_blob(container.name,"image-blob")
File.open("download.png","wb") {|f| f.write(content)}
```

## <a name="delete-a-blob"></a><span data-ttu-id="f8e91-162">Excluir um blob</span><span class="sxs-lookup"><span data-stu-id="f8e91-162">Delete a Blob</span></span>
<span data-ttu-id="f8e91-163">Finalmente, para excluir um blob, use o método **delete\_blob()**.</span><span class="sxs-lookup"><span data-stu-id="f8e91-163">Finally, to delete a blob, use the **delete\_blob()** method.</span></span> <span data-ttu-id="f8e91-164">O exemplo de código a seguir demonstra como excluir um blob.</span><span class="sxs-lookup"><span data-stu-id="f8e91-164">The following code example demonstrates how to delete a blob.</span></span>

```ruby
azure_blob_service.delete_blob(container.name, "image-blob")
```

## <a name="next-steps"></a><span data-ttu-id="f8e91-165">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f8e91-165">Next steps</span></span>
<span data-ttu-id="f8e91-166">Para saber mais sobre tarefas complexas de armazenamento, siga estes links:</span><span class="sxs-lookup"><span data-stu-id="f8e91-166">To learn about more complex storage tasks, follow these links:</span></span>

* [<span data-ttu-id="f8e91-167">Blog da equipe de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="f8e91-167">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)
* <span data-ttu-id="f8e91-168">[SDK do Azure para repositório Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) no GitHub</span><span class="sxs-lookup"><span data-stu-id="f8e91-168">[Azure SDK for Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) repository on GitHub</span></span>
* [<span data-ttu-id="f8e91-169">Transferir dados com o Utilitário de Linha de Comando AzCopy</span><span class="sxs-lookup"><span data-stu-id="f8e91-169">Transfer data with the AzCopy Command-Line Utility</span></span>](storage-use-azcopy.md)

