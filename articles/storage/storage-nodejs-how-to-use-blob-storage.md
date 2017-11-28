---
title: aaaHow toouse armazenamento de Blob do Node. js | Microsoft Docs
description: "Armazene dados não estruturados em nuvem Olá com armazenamento de BLOBs do Azure (armazenamento de objeto)."
services: storage
documentationcenter: nodejs
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 8b0df222-1ca8-4967-8248-6d6d720947b8
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: e405eecdc60cd1eaa77510e7b29b41269372b65e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-nodejs"></a><span data-ttu-id="74708-103">Como toouse armazenamento de Blob do Node. js</span><span class="sxs-lookup"><span data-stu-id="74708-103">How toouse Blob storage from Node.js</span></span>
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-check-out-samples-all](../../includes/storage-check-out-samples-all.md)]

## <a name="overview"></a><span data-ttu-id="74708-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="74708-104">Overview</span></span>
<span data-ttu-id="74708-105">Este artigo mostra como tooperform cenários comuns de usar o armazenamento de Blob.</span><span class="sxs-lookup"><span data-stu-id="74708-105">This article shows you how tooperform common scenarios using Blob storage.</span></span> <span data-ttu-id="74708-106">exemplos de saudação são gravados por meio de saudação API Node. js.</span><span class="sxs-lookup"><span data-stu-id="74708-106">hello samples are written via hello Node.js API.</span></span> <span data-ttu-id="74708-107">cenários de saudação abordados incluem como tooupload, listar, baixar e excluir blobs.</span><span class="sxs-lookup"><span data-stu-id="74708-107">hello scenarios covered include how tooupload, list, download, and delete blobs.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-nodejs-application"></a><span data-ttu-id="74708-108">Criar um aplicativo do Node.js</span><span class="sxs-lookup"><span data-stu-id="74708-108">Create a Node.js application</span></span>
<span data-ttu-id="74708-109">Para obter instruções sobre como toocreate um aplicativo Node. js, consulte [criar um aplicativo da web Node. js no serviço de aplicativo do Azure], [criar e implantar um aplicativo de Node. js tooan serviço de nuvem do Azure] – usando o Windows PowerShell , ou [criar e implantar um tooAzure de aplicativo web Node.js usando o Web Matrix].</span><span class="sxs-lookup"><span data-stu-id="74708-109">For instructions on how toocreate a Node.js application, see [Create a Node.js web app in Azure App Service], [Build and deploy a Node.js application tooan Azure Cloud Service] -- using Windows PowerShell, or [Build and deploy a Node.js web app tooAzure using Web Matrix].</span></span>

## <a name="configure-your-application-tooaccess-storage"></a><span data-ttu-id="74708-110">Configurar o armazenamento de tooaccess do aplicativo</span><span class="sxs-lookup"><span data-stu-id="74708-110">Configure your application tooaccess storage</span></span>
<span data-ttu-id="74708-111">toouse armazenamento do Azure, você precisa hello Azure Storage SDK para Node.js, que inclui um conjunto de bibliotecas de conveniência que se comunicam com serviços da REST do armazenamento Olá.</span><span class="sxs-lookup"><span data-stu-id="74708-111">toouse Azure storage, you need hello Azure Storage SDK for Node.js, which includes a set of convenience libraries that communicate with hello storage REST services.</span></span>

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a><span data-ttu-id="74708-112">Usar o pacote de saudação do Gerenciador de pacote de nó (NPM) tooobtain</span><span class="sxs-lookup"><span data-stu-id="74708-112">Use Node Package Manager (NPM) tooobtain hello package</span></span>
1. <span data-ttu-id="74708-113">Use uma interface de linha de comando como **PowerShell** (Windows), **Terminal** (Mac), ou **Bash** (Unix), toonavigate toohello pasta em que você criou seu exemplo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="74708-113">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix), toonavigate toohello folder where you created your sample application.</span></span>
2. <span data-ttu-id="74708-114">Tipo **npm instalar o armazenamento do azure** na janela de comando hello.</span><span class="sxs-lookup"><span data-stu-id="74708-114">Type **npm install azure-storage** in hello command window.</span></span> <span data-ttu-id="74708-115">A saída do comando de saudação é semelhante toohello exemplo de código a seguir.</span><span class="sxs-lookup"><span data-stu-id="74708-115">Output from hello command is similar toohello following code example.</span></span>

        azure-storage@0.5.0 node_modules\azure-storage
        +-- extend@1.2.1
        +-- xmlbuilder@0.4.3
        +-- mime@1.2.11
        +-- node-uuid@1.4.3
        +-- validator@3.22.2
        +-- underscore@1.4.4
        +-- readable-stream@1.0.33 (string_decoder@0.10.31, isarray@0.0.1, inherits@2.0.1, core-util-is@1.0.1)
        +-- xml2js@0.2.7 (sax@0.5.2)
        +-- request@2.57.0 (caseless@0.10.0, aws-sign2@0.5.0, forever-agent@0.6.1, stringstream@0.0.4, oauth-sign@0.8.0, tunnel-agent@0.4.1, isstream@0.1.2, json-stringify-safe@5.0.1, bl@0.9.4, combined-stream@1.0.5, qs@3.1.0, mime-types@2.0.14, form-data@0.2.0, http-signature@0.11.0, tough-cookie@2.0.0, hawk@2.3.1, har-validator@1.8.0)
3. <span data-ttu-id="74708-116">Você pode executar manualmente Olá **ls** tooverify de comando que um **nó\_módulos** pasta foi criada.</span><span class="sxs-lookup"><span data-stu-id="74708-116">You can manually run hello **ls** command tooverify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="74708-117">Dentro dessa pasta, localize Olá **armazenamento do azure** pacote, que contém as bibliotecas de saudação que você precisa de armazenamento de tooaccess.</span><span class="sxs-lookup"><span data-stu-id="74708-117">Inside that folder, find hello **azure-storage** package, which contains hello libraries that you need tooaccess storage.</span></span>

### <a name="import-hello-package"></a><span data-ttu-id="74708-118">Importar o pacote de saudação</span><span class="sxs-lookup"><span data-stu-id="74708-118">Import hello package</span></span>
<span data-ttu-id="74708-119">Usando o bloco de notas ou outro editor de texto, adicionar Olá após toohello superior de saudação **server.js** arquivo de aplicativo hello onde você pretende toouse armazenamento:</span><span class="sxs-lookup"><span data-stu-id="74708-119">Using Notepad or another text editor, add hello following toohello top of hello **server.js** file of hello application where you intend toouse storage:</span></span>

```nodejs
var azure = require('azure-storage');
```

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="74708-120">Configurar uma conexão do Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="74708-120">Set up an Azure Storage connection</span></span>
<span data-ttu-id="74708-121">Olá módulo do Azure lerá variáveis de ambiente Olá `AZURE_STORAGE_ACCOUNT` e `AZURE_STORAGE_ACCESS_KEY`, ou `AZURE_STORAGE_CONNECTION_STRING`, para obter informações necessárias tooconnect tooyour conta de armazenamento Azure.</span><span class="sxs-lookup"><span data-stu-id="74708-121">hello Azure module will read hello environment variables `AZURE_STORAGE_ACCOUNT` and `AZURE_STORAGE_ACCESS_KEY`, or `AZURE_STORAGE_CONNECTION_STRING`, for information required tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="74708-122">Se essas variáveis de ambiente não forem definidas, você deve especificar as informações de conta de saudação ao chamar **createBlobService**.</span><span class="sxs-lookup"><span data-stu-id="74708-122">If these environment variables are not set, you must specify hello account information when calling **createBlobService**.</span></span>

<span data-ttu-id="74708-123">Para obter um exemplo de configuração de variáveis de ambiente Olá no hello [portal do Azure](https://portal.azure.com) para um aplicativo web do Azure, consulte [usando o aplicativo web Node.js hello Azure serviço de tabela].</span><span class="sxs-lookup"><span data-stu-id="74708-123">For an example of setting hello environment variables in hello [Azure portal](https://portal.azure.com) for an Azure web app, see [Node.js web app using hello Azure Table Service].</span></span>

## <a name="create-a-container"></a><span data-ttu-id="74708-124">Criar um contêiner</span><span class="sxs-lookup"><span data-stu-id="74708-124">Create a container</span></span>
<span data-ttu-id="74708-125">Olá **BlobService** objeto permite que você trabalhe com contêineres e blobs.</span><span class="sxs-lookup"><span data-stu-id="74708-125">hello **BlobService** object lets you work with containers and blobs.</span></span> <span data-ttu-id="74708-126">Olá código a seguir cria um **BlobService** objeto.</span><span class="sxs-lookup"><span data-stu-id="74708-126">hello following code creates a **BlobService** object.</span></span> <span data-ttu-id="74708-127">Adicione a seguinte Olá superior de saudação do **server.js**:</span><span class="sxs-lookup"><span data-stu-id="74708-127">Add hello following near hello top of **server.js**:</span></span>

```nodejs
var blobSvc = azure.createBlobService();
```

> [!NOTE]
> <span data-ttu-id="74708-128">Você pode acessar um blob anonimamente usando **createBlobServiceAnonymous** e fornecendo o endereço do host hello.</span><span class="sxs-lookup"><span data-stu-id="74708-128">You can access a blob anonymously by using **createBlobServiceAnonymous** and providing hello host address.</span></span> <span data-ttu-id="74708-129">Por exemplo, use `var blobSvc = azure.createBlobServiceAnonymous('https://myblob.blob.core.windows.net/');`.</span><span class="sxs-lookup"><span data-stu-id="74708-129">For example, use `var blobSvc = azure.createBlobServiceAnonymous('https://myblob.blob.core.windows.net/');`.</span></span>
>
>

[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="74708-130">toocreate um novo contêiner, use **createContainerIfNotExists**.</span><span class="sxs-lookup"><span data-stu-id="74708-130">toocreate a new container, use **createContainerIfNotExists**.</span></span> <span data-ttu-id="74708-131">Olá, exemplo de código a seguir cria um novo contêiner denominado 'mycontainer':</span><span class="sxs-lookup"><span data-stu-id="74708-131">hello following code example creates a new container named 'mycontainer':</span></span>

```nodejs
blobSvc.createContainerIfNotExists('mycontainer', function(error, result, response){
    if(!error){
      // Container exists and is private
    }
});
```

<span data-ttu-id="74708-132">Se o contêiner de saudação for recém-criado, `result.created` é verdadeiro.</span><span class="sxs-lookup"><span data-stu-id="74708-132">If hello container is newly created, `result.created` is true.</span></span> <span data-ttu-id="74708-133">Se já existir um contêiner hello, `result.created` é false.</span><span class="sxs-lookup"><span data-stu-id="74708-133">If hello container already exists, `result.created` is false.</span></span> <span data-ttu-id="74708-134">`response`contém informações sobre a operação de hello, incluindo informações de ETag Olá para o contêiner de saudação.</span><span class="sxs-lookup"><span data-stu-id="74708-134">`response` contains information about hello operation, including hello ETag information for hello container.</span></span>

### <a name="container-security"></a><span data-ttu-id="74708-135">Segurança do contêiner</span><span class="sxs-lookup"><span data-stu-id="74708-135">Container security</span></span>
<span data-ttu-id="74708-136">Por padrão, novos contêineres são privados e não podem ser acessados ​​anonimamente.</span><span class="sxs-lookup"><span data-stu-id="74708-136">By default, new containers are private and cannot be accessed anonymously.</span></span> <span data-ttu-id="74708-137">contêiner de saudação toomake public para que você pode acessá-lo de forma anônima, você pode definir o nível de acesso do contêiner Olá muito**blob** ou **contêiner**.</span><span class="sxs-lookup"><span data-stu-id="74708-137">toomake hello container public so that you can access it anonymously, you can set hello container's access level too**blob** or **container**.</span></span>

* <span data-ttu-id="74708-138">**blob** -permite acesso de leitura anônimo tooblob conteúdo e metadados nesse contêiner, mas não toocontainer metadados como listar todos os blobs dentro de um contêiner</span><span class="sxs-lookup"><span data-stu-id="74708-138">**blob** - allows anonymous read access tooblob content and metadata within this container, but not toocontainer metadata such as listing all blobs within a container</span></span>
* <span data-ttu-id="74708-139">**contêiner** -permite acesso de leitura anônimo tooblob conteúdo e metadados, assim como metadados de contêiner</span><span class="sxs-lookup"><span data-stu-id="74708-139">**container** - allows anonymous read access tooblob content and metadata as well as container metadata</span></span>

<span data-ttu-id="74708-140">Olá exemplo de código a seguir demonstra o nível de acesso de saudação configuração muito**blob**:</span><span class="sxs-lookup"><span data-stu-id="74708-140">hello following code example demonstrates setting hello access level too**blob**:</span></span>

```nodejs
blobSvc.createContainerIfNotExists('mycontainer', {publicAccessLevel : 'blob'}, function(error, result, response){
    if(!error){
      // Container exists and allows
      // anonymous read access tooblob
      // content and metadata within this container
    }
});
```

<span data-ttu-id="74708-141">Como alternativa, você pode modificar o nível de acesso de saudação de um contêiner usando **setContainerAcl** toospecify nível de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="74708-141">Alternatively, you can modify hello access level of a container by using **setContainerAcl** toospecify hello access level.</span></span> <span data-ttu-id="74708-142">toocontainer nível de acesso para Olá exemplo alterações de código a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="74708-142">hello following code example changes hello access level toocontainer:</span></span>

```nodejs
blobSvc.setContainerAcl('mycontainer', null /* signedIdentifiers */, {publicAccessLevel : 'container'} /* publicAccessLevel*/, function(error, result, response){
  if(!error){
    // Container access level set too'container'
  }
});
```

<span data-ttu-id="74708-143">Hello, resultado contém informações sobre a operação hello, incluindo Olá atual **ETag** para contêiner hello.</span><span class="sxs-lookup"><span data-stu-id="74708-143">hello result contains information about hello operation, including hello current **ETag** for hello container.</span></span>

### <a name="filters"></a><span data-ttu-id="74708-144">Filtros</span><span class="sxs-lookup"><span data-stu-id="74708-144">Filters</span></span>
<span data-ttu-id="74708-145">Você pode aplicar opcional filtragem operações toooperations executada usando **BlobService**.</span><span class="sxs-lookup"><span data-stu-id="74708-145">You can apply optional filtering operations toooperations performed using **BlobService**.</span></span> <span data-ttu-id="74708-146">As operações de filtragem podem incluir registro em log, repetição automática, etc. Os filtros são objetos que implementam um método com assinatura hello:</span><span class="sxs-lookup"><span data-stu-id="74708-146">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with hello signature:</span></span>

```nodejs
function handle (requestOptions, next)
```

<span data-ttu-id="74708-147">Depois de fazer sua pré-processamento nas opções de solicitação hello, método hello precisa toocall "Avançar", passando um retorno de chamada com hello assinatura a seguir:</span><span class="sxs-lookup"><span data-stu-id="74708-147">After doing its preprocessing on hello request options, hello method needs toocall "next", passing a callback with hello following signature:</span></span>

```nodejs
function (returnObject, finalCallback, next)
```

<span data-ttu-id="74708-148">Esse retorno de chamada e após o processamento returnObject hello (resposta de saudação do servidor de toohello de solicitação de saudação), o retorno de chamada hello precisa tooeither invocar próximo se ela existe toocontinue outros filtros de processamento ou simplesmente invocar o serviço de saudação do finalCallback tooend invocação.</span><span class="sxs-lookup"><span data-stu-id="74708-148">In this callback, and after processing hello returnObject (hello response from hello request toohello server), hello callback needs tooeither invoke next if it exists toocontinue processing other filters or simply invoke finalCallback tooend hello service invocation.</span></span>

<span data-ttu-id="74708-149">Dois filtros que implementam a lógica de repetição são incluídos com hello Azure SDK para Node.js, **ExponentialRetryPolicyFilter** e **LinearRetryPolicyFilter**.</span><span class="sxs-lookup"><span data-stu-id="74708-149">Two filters that implement retry logic are included with hello Azure SDK for Node.js, **ExponentialRetryPolicyFilter** and **LinearRetryPolicyFilter**.</span></span> <span data-ttu-id="74708-150">Olá seguir cria um **BlobService** objeto que usa Olá **ExponentialRetryPolicyFilter**:</span><span class="sxs-lookup"><span data-stu-id="74708-150">hello following creates a **BlobService** object that uses hello **ExponentialRetryPolicyFilter**:</span></span>

```nodejs
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var blobSvc = azure.createBlobService().withFilter(retryOperations);
```

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="74708-151">Carregar um blob em um contêiner</span><span class="sxs-lookup"><span data-stu-id="74708-151">Upload a blob into a container</span></span>
<span data-ttu-id="74708-152">Há três tipos de blobs: blob de blocos, blob de páginas e blob de anexo.</span><span class="sxs-lookup"><span data-stu-id="74708-152">There are three types of blobs: block blobs, page blobs and append blobs.</span></span> <span data-ttu-id="74708-153">Blobs de bloco permitem que você toomore com eficiência carregar dados grandes.</span><span class="sxs-lookup"><span data-stu-id="74708-153">Block blobs allow you toomore efficiently upload large data.</span></span> <span data-ttu-id="74708-154">Blobs de anexo otimizados para operações de acréscimo.</span><span class="sxs-lookup"><span data-stu-id="74708-154">Append blobs are optimized for append operations.</span></span> <span data-ttu-id="74708-155">Blobs de página são otimizados para operações de leitura/gravação.</span><span class="sxs-lookup"><span data-stu-id="74708-155">Page blobs are optimized for read/write operations.</span></span> <span data-ttu-id="74708-156">Para saber mais, confira [Noções básicas sobre Blobs de bloco, Blobs de acréscimo e Blobs de página](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span><span class="sxs-lookup"><span data-stu-id="74708-156">For more information, see [Understanding Block Blobs, Append Blobs, and Page Blobs](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span></span>

### <a name="block-blobs"></a><span data-ttu-id="74708-157">Blobs de bloco</span><span class="sxs-lookup"><span data-stu-id="74708-157">Block blobs</span></span>
<span data-ttu-id="74708-158">blob de blocos de tooa de dados tooupload, Olá uso a seguir:</span><span class="sxs-lookup"><span data-stu-id="74708-158">tooupload data tooa block blob, use hello following:</span></span>

* <span data-ttu-id="74708-159">**createBlockBlobFromLocalFile** - cria um novo blob de bloco e carrega o conteúdo de saudação de um arquivo</span><span class="sxs-lookup"><span data-stu-id="74708-159">**createBlockBlobFromLocalFile** - creates a new block blob and uploads hello contents of a file</span></span>
* <span data-ttu-id="74708-160">**createBlockBlobFromStream** - cria um novo blob de bloco e carrega o conteúdo de saudação de um fluxo</span><span class="sxs-lookup"><span data-stu-id="74708-160">**createBlockBlobFromStream** - creates a new block blob and uploads hello contents of a stream</span></span>
* <span data-ttu-id="74708-161">**createBlockBlobFromText** - cria um novo blob de bloco e carrega o conteúdo de saudação de uma cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="74708-161">**createBlockBlobFromText** - creates a new block blob and uploads hello contents of a string</span></span>
* <span data-ttu-id="74708-162">**createWriteStreamToBlockBlob** -fornece um blob de blocos de tooa de fluxo de gravação</span><span class="sxs-lookup"><span data-stu-id="74708-162">**createWriteStreamToBlockBlob** - provides a write stream tooa block blob</span></span>

<span data-ttu-id="74708-163">Olá, exemplo de código a seguir carrega conteúdo Olá Olá **test.txt** o arquivo em **myblob**.</span><span class="sxs-lookup"><span data-stu-id="74708-163">hello following code example uploads hello contents of hello **test.txt** file into **myblob**.</span></span>

```nodejs
blobSvc.createBlockBlobFromLocalFile('mycontainer', 'myblob', 'test.txt', function(error, result, response){
  if(!error){
    // file uploaded
  }
});
```

<span data-ttu-id="74708-164">Olá `result` retornado por esses métodos contém informações sobre a operação de saudação, como Olá **ETag** de blob de saudação.</span><span class="sxs-lookup"><span data-stu-id="74708-164">hello `result` returned by these methods contains information on hello operation, such as hello **ETag** of hello blob.</span></span>

### <a name="append-blobs"></a><span data-ttu-id="74708-165">Blobs de acréscimo</span><span class="sxs-lookup"><span data-stu-id="74708-165">Append blobs</span></span>
<span data-ttu-id="74708-166">tooupload dados tooa novo blob de acréscimo, use o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="74708-166">tooupload data tooa new append blob, use hello following:</span></span>

* <span data-ttu-id="74708-167">**createAppendBlobFromLocalFile** - cria um novo blob de acréscimo e carrega o conteúdo de saudação de um arquivo</span><span class="sxs-lookup"><span data-stu-id="74708-167">**createAppendBlobFromLocalFile** - creates a new append blob and uploads hello contents of a file</span></span>
* <span data-ttu-id="74708-168">**createAppendBlobFromStream** - cria um novo blob de acréscimo e carrega o conteúdo de saudação de um fluxo</span><span class="sxs-lookup"><span data-stu-id="74708-168">**createAppendBlobFromStream** - creates a new append blob and uploads hello contents of a stream</span></span>
* <span data-ttu-id="74708-169">**createAppendBlobFromText** - cria um novo blob de acréscimo e carrega o conteúdo de saudação de uma cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="74708-169">**createAppendBlobFromText** - creates a new append blob and uploads hello contents of a string</span></span>
* <span data-ttu-id="74708-170">**createWriteStreamToNewAppendBlob** - cria um novo blob de acréscimo e, em seguida, fornece um tooit toowrite de fluxo</span><span class="sxs-lookup"><span data-stu-id="74708-170">**createWriteStreamToNewAppendBlob** - creates a new append blob and then provides a stream toowrite tooit</span></span>

<span data-ttu-id="74708-171">Olá, exemplo de código a seguir carrega conteúdo Olá Olá **test.txt** o arquivo em **myappendblob**.</span><span class="sxs-lookup"><span data-stu-id="74708-171">hello following code example uploads hello contents of hello **test.txt** file into **myappendblob**.</span></span>

```nodejs
blobSvc.createAppendBlobFromLocalFile('mycontainer', 'myappendblob', 'test.txt', function(error, result, response){
  if(!error){
    // file uploaded
  }
});
```

<span data-ttu-id="74708-172">tooappend um tooan de bloco existentes acrescentar blob, use Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="74708-172">tooappend a block tooan existing append blob, use hello following:</span></span>

* <span data-ttu-id="74708-173">**appendFromLocalFile** -Acrescente conteúdo de saudação do tooan arquivo existente acrescentar blob</span><span class="sxs-lookup"><span data-stu-id="74708-173">**appendFromLocalFile** - append hello contents of a file tooan existing append blob</span></span>
* <span data-ttu-id="74708-174">**appendFromStream** -Acrescente conteúdo de saudação do tooan fluxo existente acrescentar blob</span><span class="sxs-lookup"><span data-stu-id="74708-174">**appendFromStream** - append hello contents of a stream tooan existing append blob</span></span>
* <span data-ttu-id="74708-175">**appendFromText** -Acrescente conteúdo de saudação do tooan cadeia de caracteres existente acrescentar blob</span><span class="sxs-lookup"><span data-stu-id="74708-175">**appendFromText** - append hello contents of a string tooan existing append blob</span></span>
* <span data-ttu-id="74708-176">**appendBlockFromStream** -Acrescente conteúdo de saudação do tooan fluxo existente acrescentar blob</span><span class="sxs-lookup"><span data-stu-id="74708-176">**appendBlockFromStream** - append hello contents of a stream tooan existing append blob</span></span>
* <span data-ttu-id="74708-177">**appendBlockFromText** -Acrescente conteúdo de saudação do tooan cadeia de caracteres existente acrescentar blob</span><span class="sxs-lookup"><span data-stu-id="74708-177">**appendBlockFromText** - append hello contents of a string tooan existing append blob</span></span>

> [!NOTE]
> <span data-ttu-id="74708-178">appendFromXXX APIs fará algumas chamadas de servidor desnecessários validação do lado do cliente toofail tooavoid rápida.</span><span class="sxs-lookup"><span data-stu-id="74708-178">appendFromXXX APIs will do some client-side validation toofail fast tooavoid unnecessary server calls.</span></span> <span data-ttu-id="74708-179">appendBlockFromXXX não fará isso.</span><span class="sxs-lookup"><span data-stu-id="74708-179">appendBlockFromXXX won't.</span></span>
>
>

<span data-ttu-id="74708-180">Olá, exemplo de código a seguir carrega conteúdo Olá Olá **test.txt** o arquivo em **myappendblob**.</span><span class="sxs-lookup"><span data-stu-id="74708-180">hello following code example uploads hello contents of hello **test.txt** file into **myappendblob**.</span></span>

```nodejs
blobSvc.appendFromText('mycontainer', 'myappendblob', 'text toobe appended', function(error, result, response){
  if(!error){
    // text appended
  }
});
```

### <a name="page-blobs"></a><span data-ttu-id="74708-181">Blobs de página</span><span class="sxs-lookup"><span data-stu-id="74708-181">Page blobs</span></span>
<span data-ttu-id="74708-182">blob de páginas de tooa de dados tooupload, Olá uso a seguir:</span><span class="sxs-lookup"><span data-stu-id="74708-182">tooupload data tooa page blob, use hello following:</span></span>

* <span data-ttu-id="74708-183">**createPageBlob** – cria um novo blob de páginas de um comprimento específico</span><span class="sxs-lookup"><span data-stu-id="74708-183">**createPageBlob** - creates a new page blob of a specific length</span></span>
* <span data-ttu-id="74708-184">**createPageBlobFromLocalFile** - cria um novo blob de página e carrega o conteúdo de saudação de um arquivo</span><span class="sxs-lookup"><span data-stu-id="74708-184">**createPageBlobFromLocalFile** - creates a new page blob and uploads hello contents of a file</span></span>
* <span data-ttu-id="74708-185">**createPageBlobFromStream** - cria um novo blob de página e carrega o conteúdo de saudação de um fluxo</span><span class="sxs-lookup"><span data-stu-id="74708-185">**createPageBlobFromStream** - creates a new page blob and uploads hello contents of a stream</span></span>
* <span data-ttu-id="74708-186">**createWriteStreamToExistingPageBlob** -fornece um blob de página existente do gravação fluxo tooan</span><span class="sxs-lookup"><span data-stu-id="74708-186">**createWriteStreamToExistingPageBlob** - provides a write stream tooan existing page blob</span></span>
* <span data-ttu-id="74708-187">**createWriteStreamToNewPageBlob** - cria um novo blob de página e, em seguida, fornece um tooit toowrite de fluxo</span><span class="sxs-lookup"><span data-stu-id="74708-187">**createWriteStreamToNewPageBlob** - creates a new page blob and then provides a stream toowrite tooit</span></span>

<span data-ttu-id="74708-188">Olá, exemplo de código a seguir carrega conteúdo Olá Olá **test.txt** o arquivo em **mypageblob**.</span><span class="sxs-lookup"><span data-stu-id="74708-188">hello following code example uploads hello contents of hello **test.txt** file into **mypageblob**.</span></span>

```nodejs
blobSvc.createPageBlobFromLocalFile('mycontainer', 'mypageblob', 'test.txt', function(error, result, response){
  if(!error){
    // file uploaded
  }
});
```

> [!NOTE]
> <span data-ttu-id="74708-189">Blobs de página consistem em 'páginas’ de 512 bytes.</span><span class="sxs-lookup"><span data-stu-id="74708-189">Page blobs consist of 512-byte 'pages'.</span></span> <span data-ttu-id="74708-190">Você receberá um erro ao carregar dados com um tamanho que não seja um múltiplo de 512.</span><span class="sxs-lookup"><span data-stu-id="74708-190">You will receive an error when uploading data with a size that is not a multiple of 512.</span></span>
>
>

## <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="74708-191">Saudação de listar blobs em um contêiner</span><span class="sxs-lookup"><span data-stu-id="74708-191">List hello blobs in a container</span></span>
<span data-ttu-id="74708-192">blobs de saudação toolist em um contêiner, use Olá **listBlobsSegmented** método.</span><span class="sxs-lookup"><span data-stu-id="74708-192">toolist hello blobs in a container, use hello **listBlobsSegmented** method.</span></span> <span data-ttu-id="74708-193">Se você desejar tooreturn blobs com um prefixo específico, use **listBlobsSegmentedWithPrefix**.</span><span class="sxs-lookup"><span data-stu-id="74708-193">If you'd like tooreturn blobs with a specific prefix, use **listBlobsSegmentedWithPrefix**.</span></span>

```nodejs
blobSvc.listBlobsSegmented('mycontainer', null, function(error, result, response){
  if(!error){
      // result.entries contains hello entries
      // If not all blobs were returned, result.continuationToken has hello continuation token.
  }
});
```

<span data-ttu-id="74708-194">Olá `result` contém um `entries` coleção, que é uma matriz de objetos que descrevem cada blob.</span><span class="sxs-lookup"><span data-stu-id="74708-194">hello `result` contains an `entries` collection, which is an array of objects that describe each blob.</span></span> <span data-ttu-id="74708-195">Se todos os blobs não podem ser retornados, Olá `result` também fornece um `continuationToken`, que pode ser usado como Olá segundo parâmetro tooretrieve entradas adicionais.</span><span class="sxs-lookup"><span data-stu-id="74708-195">If all blobs cannot be returned, hello `result` also provides a `continuationToken`, which you may use as hello second parameter tooretrieve additional entries.</span></span>

## <a name="download-blobs"></a><span data-ttu-id="74708-196">Baixar blobs</span><span class="sxs-lookup"><span data-stu-id="74708-196">Download blobs</span></span>
<span data-ttu-id="74708-197">dados toodownload de um blob, use o seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="74708-197">toodownload data from a blob, use hello following:</span></span>

* <span data-ttu-id="74708-198">**getBlobToLocalFile** -grava Olá toofile de conteúdo de blob</span><span class="sxs-lookup"><span data-stu-id="74708-198">**getBlobToLocalFile** - writes hello blob contents toofile</span></span>
* <span data-ttu-id="74708-199">**getBlobToStream** -grava o fluxo de tooa de conteúdo de blob Olá</span><span class="sxs-lookup"><span data-stu-id="74708-199">**getBlobToStream** - writes hello blob contents tooa stream</span></span>
* <span data-ttu-id="74708-200">**getBlobToText** -grava o conteúdo de blob Olá tooa de cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="74708-200">**getBlobToText** - writes hello blob contents tooa string</span></span>
* <span data-ttu-id="74708-201">**createReadStream** -fornece um tooread de fluxo de blob Olá</span><span class="sxs-lookup"><span data-stu-id="74708-201">**createReadStream** - provides a stream tooread from hello blob</span></span>

<span data-ttu-id="74708-202">Olá exemplo de código a seguir demonstra o uso de **getBlobToStream** conteúdo toodownload Olá Olá **myblob** blob e armazená-lo toohello **txt** arquivo usando um fluxo:</span><span class="sxs-lookup"><span data-stu-id="74708-202">hello following code example demonstrates using **getBlobToStream** toodownload hello contents of hello **myblob** blob and store it toohello **output.txt** file by using a stream:</span></span>

```nodejs
var fs = require('fs');
blobSvc.getBlobToStream('mycontainer', 'myblob', fs.createWriteStream('output.txt'), function(error, result, response){
  if(!error){
    // blob retrieved
  }
});
```

<span data-ttu-id="74708-203">Olá `result` contém informações sobre Olá blob, incluindo **ETag** informações.</span><span class="sxs-lookup"><span data-stu-id="74708-203">hello `result` contains information about hello blob, including **ETag** information.</span></span>

## <a name="delete-a-blob"></a><span data-ttu-id="74708-204">Excluir um blob</span><span class="sxs-lookup"><span data-stu-id="74708-204">Delete a blob</span></span>
<span data-ttu-id="74708-205">Finalmente, toodelete um blob, chame **deleteBlob**.</span><span class="sxs-lookup"><span data-stu-id="74708-205">Finally, toodelete a blob, call **deleteBlob**.</span></span> <span data-ttu-id="74708-206">Olá exclusões Olá blob denominado de exemplo de código a seguir **myblob**.</span><span class="sxs-lookup"><span data-stu-id="74708-206">hello following code example deletes hello blob named **myblob**.</span></span>

```nodejs
blobSvc.deleteBlob(containerName, 'myblob', function(error, response){
  if(!error){
    // Blob has been deleted
  }
});
```

## <a name="concurrent-access"></a><span data-ttu-id="74708-207">Acesso simultâneo</span><span class="sxs-lookup"><span data-stu-id="74708-207">Concurrent access</span></span>
<span data-ttu-id="74708-208">blob de tooa toosupport acesso simultâneo de vários clientes ou várias instâncias do processo, você pode usar **ETags** ou **concessões**.</span><span class="sxs-lookup"><span data-stu-id="74708-208">toosupport concurrent access tooa blob from multiple clients or multiple process instances, you can use **ETags** or **leases**.</span></span>

* <span data-ttu-id="74708-209">**ETag** -fornece um toodetect de forma que Olá contêiner ou blob foi modificado por outro processo</span><span class="sxs-lookup"><span data-stu-id="74708-209">**Etag** - provides a way toodetect that hello blob or container has been modified by another process</span></span>
* <span data-ttu-id="74708-210">**Concessão** - fornece uma gravação de maneira tooobtain exclusivo, renovável, ou excluir o blob de tooa de acesso para um período de tempo</span><span class="sxs-lookup"><span data-stu-id="74708-210">**Lease** - provides a way tooobtain exclusive, renewable, write or delete access tooa blob for a period of time</span></span>

### <a name="etag"></a><span data-ttu-id="74708-211">ETag</span><span class="sxs-lookup"><span data-stu-id="74708-211">ETag</span></span>
<span data-ttu-id="74708-212">Use ETags, se você precisar tooallow vários clientes ou instâncias toowrite toohello bloco Blob ou página Blob simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="74708-212">Use ETags if you need tooallow multiple clients or instances toowrite toohello block Blob or page Blob simultaneously.</span></span> <span data-ttu-id="74708-213">Olá ETag permite toodetermine se hello contêiner ou blob tiver sido modificado desde que inicialmente ler ou criado, o que permite que você tooavoid substituindo as alterações confirmadas por outro processo ou cliente.</span><span class="sxs-lookup"><span data-stu-id="74708-213">hello ETag allows you toodetermine if hello container or blob was modified since you initially read or created it, which allows you tooavoid overwriting changes committed by another client or process.</span></span>

<span data-ttu-id="74708-214">Você pode definir condições de ETag usando Olá opcional `options.accessConditions` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="74708-214">You can set ETag conditions by using hello optional `options.accessConditions` parameter.</span></span> <span data-ttu-id="74708-215">Hello exemplo de código a seguir só carrega Olá **test.txt** arquivo se o blob Olá já existe e tem o valor de ETag Olá contido pelo `etagToMatch`.</span><span class="sxs-lookup"><span data-stu-id="74708-215">hello following code example only uploads hello **test.txt** file if hello blob already exists and has hello ETag value contained by `etagToMatch`.</span></span>

```nodejs
blobSvc.createBlockBlobFromLocalFile('mycontainer', 'myblob', 'test.txt', { accessConditions: { EtagMatch: etagToMatch} }, function(error, result, response){
    if(!error){
    // file uploaded
  }
});
```

<span data-ttu-id="74708-216">Quando você estiver usando ETags, padrão geral de saudação é:</span><span class="sxs-lookup"><span data-stu-id="74708-216">When you're using ETags, hello general pattern is:</span></span>

1. <span data-ttu-id="74708-217">Obter Olá ETag como resultado de saudação de criar, lista ou operação de obtenção.</span><span class="sxs-lookup"><span data-stu-id="74708-217">Obtain hello ETag as hello result of a create, list, or get operation.</span></span>
2. <span data-ttu-id="74708-218">Executar uma ação, esse valor de ETag Olá a verificação não foi modificada.</span><span class="sxs-lookup"><span data-stu-id="74708-218">Perform an action, checking that hello ETag value has not been modified.</span></span>

<span data-ttu-id="74708-219">Se o valor de saudação tiver sido modificado, isso indica que outro cliente ou instância modificada Olá blob ou contêiner desde que você obteve o valor de ETag Olá.</span><span class="sxs-lookup"><span data-stu-id="74708-219">If hello value was modified, this indicates that another client or instance modified hello blob or container since you obtained hello ETag value.</span></span>

### <a name="lease"></a><span data-ttu-id="74708-220">Concessão</span><span class="sxs-lookup"><span data-stu-id="74708-220">Lease</span></span>
<span data-ttu-id="74708-221">Você pode adquirir uma nova concessão usando Olá **acquireLease** método, especificando Olá contêiner ou blob que você deseja tooobtain uma concessão no.</span><span class="sxs-lookup"><span data-stu-id="74708-221">You can acquire a new lease by using hello **acquireLease** method, specifying hello blob or container that you wish tooobtain a lease on.</span></span> <span data-ttu-id="74708-222">Por exemplo, a saudação de código a seguir adquire uma concessão em **myblob**.</span><span class="sxs-lookup"><span data-stu-id="74708-222">For example, hello following code acquires a lease on **myblob**.</span></span>

```nodejs
blobSvc.acquireLease('mycontainer', 'myblob', function(error, result, response){
  if(!error) {
    console.log('leaseId: ' + result.id);
  }
});
```

<span data-ttu-id="74708-223">As operações subsequentes na **myblob** deve fornecer Olá `options.leaseId` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="74708-223">Subsequent operations on **myblob** must provide hello `options.leaseId` parameter.</span></span> <span data-ttu-id="74708-224">concessão Olá ID é retornado como `result.id` de **acquireLease**.</span><span class="sxs-lookup"><span data-stu-id="74708-224">hello lease ID is returned as `result.id` from **acquireLease**.</span></span>

> [!NOTE]
> <span data-ttu-id="74708-225">Por padrão, a duração da concessão Olá é infinita.</span><span class="sxs-lookup"><span data-stu-id="74708-225">By default, hello lease duration is infinite.</span></span> <span data-ttu-id="74708-226">Você pode especificar uma duração não infinita (entre 15 e 60 segundos), fornecendo Olá `options.leaseDuration` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="74708-226">You can specify a non-infinite duration (between 15 and 60 seconds) by providing hello `options.leaseDuration` parameter.</span></span>
>
>

<span data-ttu-id="74708-227">use tooremove uma concessão, **releaseLease**.</span><span class="sxs-lookup"><span data-stu-id="74708-227">tooremove a lease, use **releaseLease**.</span></span> <span data-ttu-id="74708-228">toobreak uma concessão, mas impede que outras pessoas obtenham uma nova concessão até que a duração de saudação original tiver expirado, use **breakLease**.</span><span class="sxs-lookup"><span data-stu-id="74708-228">toobreak a lease, but prevent others from obtaining a new lease until hello original duration has expired, use **breakLease**.</span></span>

## <a name="work-with-shared-access-signatures"></a><span data-ttu-id="74708-229">Trabalhar com assinaturas de acesso compartilhado</span><span class="sxs-lookup"><span data-stu-id="74708-229">Work with shared access signatures</span></span>
<span data-ttu-id="74708-230">Assinaturas de acesso compartilhado (SAS) são uma tooblobs de acesso granular de tooprovide de maneira segura e contêineres sem fornecer o nome da conta de armazenamento ou chaves.</span><span class="sxs-lookup"><span data-stu-id="74708-230">Shared access signatures (SAS) are a secure way tooprovide granular access tooblobs and containers without providing your storage account name or keys.</span></span> <span data-ttu-id="74708-231">Assinaturas de acesso compartilhado geralmente são usados tooprovide limitado acessar tooyour os dados, como permitir que um aplicativo móvel tooaccess blobs.</span><span class="sxs-lookup"><span data-stu-id="74708-231">Shared access signatures are often used tooprovide limited access tooyour data, such as allowing a mobile app tooaccess blobs.</span></span>

> [!NOTE]
> <span data-ttu-id="74708-232">Enquanto você também pode permitir acesso anônimo tooblobs, assinaturas de acesso compartilhado permitem acesso tooprovide mais controlado, você deve gerar Olá SAS.</span><span class="sxs-lookup"><span data-stu-id="74708-232">While you can also allow anonymous access tooblobs, shared access signatures allow you tooprovide more controlled access, as you must generate hello SAS.</span></span>
>
>

<span data-ttu-id="74708-233">Um aplicativo confiável como um serviço baseado em nuvem gera assinaturas de acesso compartilhado usando Olá **generateSharedAccessSignature** de saudação **BlobService**e fornece-tooan não confiável ou aplicativo de confiança parcial, como um aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="74708-233">A trusted application such as a cloud-based service generates shared access signatures using hello **generateSharedAccessSignature** of hello **BlobService**, and provides it tooan untrusted or semi-trusted application such as a mobile app.</span></span> <span data-ttu-id="74708-234">Assinaturas geradas usando uma política, que descreve o início de saudação de acesso compartilhado e datas finais durante o qual Olá assinaturas de acesso compartilhado são válidas, bem como Olá acessar nível proprietário de assinaturas de acesso compartilhado toohello concedido.</span><span class="sxs-lookup"><span data-stu-id="74708-234">Shared access signatures are generated using a policy, which describes hello start and end dates during which hello shared access signatures are valid, as well as hello access level granted toohello shared access signatures holder.</span></span>

<span data-ttu-id="74708-235">Olá, exemplo de código a seguir gera uma nova política de acesso compartilhado que permite Olá compartilhado acesso assinaturas detentor tooperform operações de leitura no hello **myblob** blob e expira 100 minutos após o tempo de saudação é criado.</span><span class="sxs-lookup"><span data-stu-id="74708-235">hello following code example generates a new shared access policy that allows hello shared access signatures holder tooperform read operations on hello **myblob** blob, and expires 100 minutes after hello time it is created.</span></span>

```nodejs
var startDate = new Date();
var expiryDate = new Date(startDate);
expiryDate.setMinutes(startDate.getMinutes() + 100);
startDate.setMinutes(startDate.getMinutes() - 100);

var sharedAccessPolicy = {
  AccessPolicy: {
    Permissions: azure.BlobUtilities.SharedAccessPermissions.READ,
    Start: startDate,
    Expiry: expiryDate
  },
};

var blobSAS = blobSvc.generateSharedAccessSignature('mycontainer', 'myblob', sharedAccessPolicy);
var host = blobSvc.host;
```

<span data-ttu-id="74708-236">Observe que informações do host Olá devem ser fornecido, além disso, como é necessário quando proprietário de assinaturas de acesso compartilhado Olá tentativas de contêiner de saudação tooaccess.</span><span class="sxs-lookup"><span data-stu-id="74708-236">Note that hello host information must be provided also, as it is required when hello shared access signatures holder attempts tooaccess hello container.</span></span>

<span data-ttu-id="74708-237">Olá, em seguida, o aplicativo do cliente usa assinaturas de acesso compartilhado com **BlobServiceWithSAS** tooperform operações blob hello.</span><span class="sxs-lookup"><span data-stu-id="74708-237">hello client application then uses shared access signatures with **BlobServiceWithSAS** tooperform operations against hello blob.</span></span> <span data-ttu-id="74708-238">Olá a seguir obtém informações sobre **myblob**.</span><span class="sxs-lookup"><span data-stu-id="74708-238">hello following gets information about **myblob**.</span></span>

```nodejs
var sharedBlobSvc = azure.createBlobServiceWithSas(host, blobSAS);
sharedBlobSvc.getBlobProperties('mycontainer', 'myblob', function (error, result, response) {
  if(!error) {
    // retrieved info
  }
});
```

<span data-ttu-id="74708-239">Desde que as assinaturas de acesso compartilhada de saudação foram geradas com acesso somente leitura, se uma tentativa de blob de saudação toomodify, um erro será retornado.</span><span class="sxs-lookup"><span data-stu-id="74708-239">Since hello shared access signatures were generated with read-only access, if an attempt is made toomodify hello blob, an error will be returned.</span></span>

### <a name="access-control-lists"></a><span data-ttu-id="74708-240">Listas de controle de acesso</span><span class="sxs-lookup"><span data-stu-id="74708-240">Access control lists</span></span>
<span data-ttu-id="74708-241">Você também pode usar uma política de acesso do acesso controle ACL (lista) tooset Olá SAS.</span><span class="sxs-lookup"><span data-stu-id="74708-241">You can also use an access control list (ACL) tooset hello access policy for SAS.</span></span> <span data-ttu-id="74708-242">Isso é útil se você quiser tooallow vários clientes tooaccess um contêiner, mas fornece as políticas de acesso diferentes para cada cliente.</span><span class="sxs-lookup"><span data-stu-id="74708-242">This is useful if you wish tooallow multiple clients tooaccess a container but provide different access policies for each client.</span></span>

<span data-ttu-id="74708-243">Uma ACL é implementada através de um conjunto de políticas de acesso, com uma ID associada a cada política.</span><span class="sxs-lookup"><span data-stu-id="74708-243">An ACL is implemented using an array of access policies, with an ID associated with each policy.</span></span> <span data-ttu-id="74708-244">saudação de exemplo de código a seguir define duas políticas, uma para 'user1' e outra para o 'Usuário2':</span><span class="sxs-lookup"><span data-stu-id="74708-244">hello following code example defines two policies, one for 'user1' and one for 'user2':</span></span>

```nodejs
var sharedAccessPolicy = {
  user1: {
    Permissions: azure.BlobUtilities.SharedAccessPermissions.READ,
    Start: startDate,
    Expiry: expiryDate
  },
  user2: {
    Permissions: azure.BlobUtilities.SharedAccessPermissions.WRITE,
    Start: startDate,
    Expiry: expiryDate
  }
};
```

<span data-ttu-id="74708-245">Olá obtém de exemplo de código a seguir Olá ACL atual para **mycontainer**e, em seguida, adiciona novas políticas de saudação usando **setBlobAcl**.</span><span class="sxs-lookup"><span data-stu-id="74708-245">hello following code example gets hello current ACL for **mycontainer**, and then adds hello new policies using **setBlobAcl**.</span></span> <span data-ttu-id="74708-246">Essa abordagem permite:</span><span class="sxs-lookup"><span data-stu-id="74708-246">This approach allows:</span></span>

```nodejs
var extend = require('extend');
blobSvc.getBlobAcl('mycontainer', function(error, result, response) {
  if(!error){
    var newSignedIdentifiers = extend(true, result.signedIdentifiers, sharedAccessPolicy);
    blobSvc.setBlobAcl('mycontainer', newSignedIdentifiers, function(error, result, response){
      if(!error){
        // ACL set
      }
    });
  }
});
```

<span data-ttu-id="74708-247">Uma vez Olá que ACL é definida, você pode criar assinaturas de acesso compartilhado com base na ID de saudação de uma política.</span><span class="sxs-lookup"><span data-stu-id="74708-247">Once hello ACL is set, you can then create shared access signatures based on hello ID for a policy.</span></span> <span data-ttu-id="74708-248">saudação de exemplo de código a seguir cria novas assinaturas de acesso compartilhado para o 'Usuário2':</span><span class="sxs-lookup"><span data-stu-id="74708-248">hello following code example creates new shared access signatures for 'user2':</span></span>

```nodejs
blobSAS = blobSvc.generateSharedAccessSignature('mycontainer', { Id: 'user2' });
```

## <a name="next-steps"></a><span data-ttu-id="74708-249">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="74708-249">Next steps</span></span>
<span data-ttu-id="74708-250">Para obter mais informações, consulte Olá recursos a seguir.</span><span class="sxs-lookup"><span data-stu-id="74708-250">For more information, see hello following resources.</span></span>

* <span data-ttu-id="74708-251">[Azure Storage SDK for Node API Reference][Azure Storage SDK for Node API Reference] (Referência do SDK do Armazenamento do Azure para API do Nó )</span><span class="sxs-lookup"><span data-stu-id="74708-251">[Azure Storage SDK for Node API Reference][Azure Storage SDK for Node API Reference]</span></span>
* <span data-ttu-id="74708-252">[Microsoft Azure Storage Team Blog][Azure Storage Team Blog] (Blog da equipe de Armazenamento do Microsoft Azure)</span><span class="sxs-lookup"><span data-stu-id="74708-252">[Azure Storage Team Blog][Azure Storage Team Blog]</span></span>
* <span data-ttu-id="74708-253">Repositório [Microsoft Azure Storage SDK for Node.js][Azure Storage SDK for Node] (SDK do Armazenamento do Microsoft Azure para Node.js) no GitHub</span><span class="sxs-lookup"><span data-stu-id="74708-253">[Azure Storage SDK for Node][Azure Storage SDK for Node] repository on GitHub</span></span>
* [<span data-ttu-id="74708-254">Centro de Desenvolvedores do Node.js</span><span class="sxs-lookup"><span data-stu-id="74708-254">Node.js Developer Center</span></span>](https://azure.microsoft.com/develop/nodejs/)
* [<span data-ttu-id="74708-255">Transferência de dados com hello AzCopy utilitário de linha de comando</span><span class="sxs-lookup"><span data-stu-id="74708-255">Transfer data with hello AzCopy command-line utility</span></span>](storage-use-azcopy.md)

[Azure Storage SDK for Node]: https://github.com/Azure/azure-storage-node

[criar um aplicativo da web Node. js no serviço de aplicativo do Azure]: ../app-service-web/app-service-web-get-started-nodejs.md
[usando o aplicativo web Node.js hello Azure serviço de tabela]: ../app-service-web/storage-nodejs-use-table-storage-web-site.md
[criar e implantar um tooAzure de aplicativo web Node.js usando o Web Matrix]: ../app-service-web/web-sites-nodejs-use-webmatrix.md
[Using hello REST API]: http://msdn.microsoft.com/library/azure/hh264518.aspx
[Azure portal]: https://portal.azure.com
[criar e implantar um aplicativo de Node. js tooan serviço de nuvem do Azure]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
[Azure Storage SDK for Node API Reference]: http://dl.windowsazure.com/nodestoragedocs/index.html
