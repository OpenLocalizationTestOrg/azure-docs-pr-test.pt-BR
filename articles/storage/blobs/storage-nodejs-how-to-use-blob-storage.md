---
title: Como usar o armazenamento de Blobs do Node.js | Microsoft Docs
description: "Armazene dados não estruturados na nuvem com o armazenamento de blobs do Azure (armazenamento de objeto)."
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
ms.openlocfilehash: e83ad647f6b7c70f34ef0c69b5bf322da5b6d60d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-blob-storage-from-nodejs"></a><span data-ttu-id="66982-103">Como usar o armazenamento de Blob do Node.js</span><span class="sxs-lookup"><span data-stu-id="66982-103">How to use Blob storage from Node.js</span></span>
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-check-out-samples-all](../../../includes/storage-check-out-samples-all.md)]

## <a name="overview"></a><span data-ttu-id="66982-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="66982-104">Overview</span></span>
<span data-ttu-id="66982-105">Este artigo mostra como executar cenários comuns usando o Armazenamento de Blobs.</span><span class="sxs-lookup"><span data-stu-id="66982-105">This article shows you how to perform common scenarios using Blob storage.</span></span> <span data-ttu-id="66982-106">Os exemplos são escritos usando a API do Node.js.</span><span class="sxs-lookup"><span data-stu-id="66982-106">The samples are written via the Node.js API.</span></span> <span data-ttu-id="66982-107">Os cenários abordados incluem como carregar, listar, baixar e excluir blobs.</span><span class="sxs-lookup"><span data-stu-id="66982-107">The scenarios covered include how to upload, list, download, and delete blobs.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-nodejs-application"></a><span data-ttu-id="66982-108">Criar um aplicativo do Node.js</span><span class="sxs-lookup"><span data-stu-id="66982-108">Create a Node.js application</span></span>
<span data-ttu-id="66982-109">Para obter instruções sobre como criar um aplicativo do Node.js, confira [Criar um aplicativo Web do Node.js no Serviço de Aplicativo do Azure], [Criar e implantar um aplicativo Node.js para um Serviço de Nuvem do Azure](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) usando o Windows PowerShell ou [Criar e implantar um aplicativo Web Node.js no Azure usando a Matriz da Web](https://www.microsoft.com/web/webmatrix/).</span><span class="sxs-lookup"><span data-stu-id="66982-109">For instructions on how to create a Node.js application, see [Create a Node.js web app in Azure App Service], [Build and deploy a Node.js application to an Azure Cloud Service](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) -- using Windows PowerShell, or [Build and deploy a Node.js web app to Azure using Web Matrix](https://www.microsoft.com/web/webmatrix/).</span></span>

## <a name="configure-your-application-to-access-storage"></a><span data-ttu-id="66982-110">Configurar seu aplicativo para acessar o armazenamento</span><span class="sxs-lookup"><span data-stu-id="66982-110">Configure your application to access storage</span></span>
<span data-ttu-id="66982-111">Para usar o armazenamento do Azure, você precisa do SDK de Armazenamento do Azure para Node.js, que inclui um conjunto de bibliotecas convenientes que se comunicam com os serviços REST do armazenamento.</span><span class="sxs-lookup"><span data-stu-id="66982-111">To use Azure storage, you need the Azure Storage SDK for Node.js, which includes a set of convenience libraries that communicate with the storage REST services.</span></span>

### <a name="use-node-package-manager-npm-to-obtain-the-package"></a><span data-ttu-id="66982-112">Usar o NPM (gerenciador de pacotes de nós) para obter o pacote</span><span class="sxs-lookup"><span data-stu-id="66982-112">Use Node Package Manager (NPM) to obtain the package</span></span>
1. <span data-ttu-id="66982-113">Use uma interface de linha de comando, como **PowerShell** (Windows), **Terminal** (Mac) ou **Bash** (Unix), para navegar até a pasta onde você criou o aplicativo de exemplo.</span><span class="sxs-lookup"><span data-stu-id="66982-113">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix), to navigate to the folder where you created your sample application.</span></span>
2. <span data-ttu-id="66982-114">Digite **npm install azure-storage** na janela de comando.</span><span class="sxs-lookup"><span data-stu-id="66982-114">Type **npm install azure-storage** in the command window.</span></span> <span data-ttu-id="66982-115">A saída do comando é semelhante ao exemplo de código a seguir.</span><span class="sxs-lookup"><span data-stu-id="66982-115">Output from the command is similar to the following code example.</span></span>

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
3. <span data-ttu-id="66982-116">Você pode executar manualmente o comando **ls** para verificar se uma pasta **node\_modules** foi criada.</span><span class="sxs-lookup"><span data-stu-id="66982-116">You can manually run the **ls** command to verify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="66982-117">Dentro dessa pasta, localize o pacote **azure-storage** , que contém as bibliotecas necessárias para acessar o armazenamento.</span><span class="sxs-lookup"><span data-stu-id="66982-117">Inside that folder, find the **azure-storage** package, which contains the libraries that you need to access storage.</span></span>

### <a name="import-the-package"></a><span data-ttu-id="66982-118">Importar o pacote</span><span class="sxs-lookup"><span data-stu-id="66982-118">Import the package</span></span>
<span data-ttu-id="66982-119">Usando o Bloco de Notas ou outro editor de texto, adicione o seguinte à parte superior do arquivo **server.js** do aplicativo no qual você pretende usar o armazenamento:</span><span class="sxs-lookup"><span data-stu-id="66982-119">Using Notepad or another text editor, add the following to the top of the **server.js** file of the application where you intend to use storage:</span></span>

```nodejs
var azure = require('azure-storage');
```

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="66982-120">Configurar uma conexão do Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="66982-120">Set up an Azure Storage connection</span></span>
<span data-ttu-id="66982-121">O módulo do Azure lerá as variáveis do ambiente `AZURE_STORAGE_ACCOUNT` e `AZURE_STORAGE_ACCESS_KEY` ou `AZURE_STORAGE_CONNECTION_STRING`, a fim de obter as informações necessárias para se conectar à sua conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="66982-121">The Azure module will read the environment variables `AZURE_STORAGE_ACCOUNT` and `AZURE_STORAGE_ACCESS_KEY`, or `AZURE_STORAGE_CONNECTION_STRING`, for information required to connect to your Azure storage account.</span></span> <span data-ttu-id="66982-122">Se essas variáveis de ambiente não estiverem definidas, você deverá especificar as informações da conta chamando **createBlobService**.</span><span class="sxs-lookup"><span data-stu-id="66982-122">If these environment variables are not set, you must specify the account information when calling **createBlobService**.</span></span>

<span data-ttu-id="66982-123">Para obter um exemplo de como definir as variáveis de ambiente no [portal do Azure](https://portal.azure.com) para um aplicativo Web do Azure, consulte [Aplicativo Web Node.js com o Serviço Tabela do Azure](../../app-service-web/storage-nodejs-use-table-storage-web-site.md).</span><span class="sxs-lookup"><span data-stu-id="66982-123">For an example of setting the environment variables in the [Azure portal](https://portal.azure.com) for an Azure web app, see [Node.js web app using the Azure Table Service](../../app-service-web/storage-nodejs-use-table-storage-web-site.md).</span></span>

## <a name="create-a-container"></a><span data-ttu-id="66982-124">Criar um contêiner</span><span class="sxs-lookup"><span data-stu-id="66982-124">Create a container</span></span>
<span data-ttu-id="66982-125">O objeto **serviço Blob** permite que você trabalhe com contêineres e blobs.</span><span class="sxs-lookup"><span data-stu-id="66982-125">The **BlobService** object lets you work with containers and blobs.</span></span> <span data-ttu-id="66982-126">O código a seguir cria um objeto **BlobService** .</span><span class="sxs-lookup"><span data-stu-id="66982-126">The following code creates a **BlobService** object.</span></span> <span data-ttu-id="66982-127">Adicione o seguinte próximo à parte superior do **server.js**:</span><span class="sxs-lookup"><span data-stu-id="66982-127">Add the following near the top of **server.js**:</span></span>

```nodejs
var blobSvc = azure.createBlobService();
```

> [!NOTE]
> <span data-ttu-id="66982-128">Você pode acessar um blob anonimamente usando **createBlobServiceAnonymous** e fornecendo o endereço do host.</span><span class="sxs-lookup"><span data-stu-id="66982-128">You can access a blob anonymously by using **createBlobServiceAnonymous** and providing the host address.</span></span> <span data-ttu-id="66982-129">Por exemplo, use `var blobSvc = azure.createBlobServiceAnonymous('https://myblob.blob.core.windows.net/');`.</span><span class="sxs-lookup"><span data-stu-id="66982-129">For example, use `var blobSvc = azure.createBlobServiceAnonymous('https://myblob.blob.core.windows.net/');`.</span></span>
>
>

[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="66982-130">Para criar um novo contêiner, use **createContainerIfNotExists**.</span><span class="sxs-lookup"><span data-stu-id="66982-130">To create a new container, use **createContainerIfNotExists**.</span></span> <span data-ttu-id="66982-131">O exemplo de código a seguir cria um novo contêiner denominado 'mycontainer':</span><span class="sxs-lookup"><span data-stu-id="66982-131">The following code example creates a new container named 'mycontainer':</span></span>

```nodejs
blobSvc.createContainerIfNotExists('mycontainer', function(error, result, response){
    if(!error){
      // Container exists and is private
    }
});
```

<span data-ttu-id="66982-132">Se o contêiner tiver sido criado recentemente, `result.created` será verdadeiro.</span><span class="sxs-lookup"><span data-stu-id="66982-132">If the container is newly created, `result.created` is true.</span></span> <span data-ttu-id="66982-133">Se o contêiner já existir, `result.created` será falso.</span><span class="sxs-lookup"><span data-stu-id="66982-133">If the container already exists, `result.created` is false.</span></span> <span data-ttu-id="66982-134">`response` contém informações sobre a operação, incluindo as informações de Etag do contêiner.</span><span class="sxs-lookup"><span data-stu-id="66982-134">`response` contains information about the operation, including the ETag information for the container.</span></span>

### <a name="container-security"></a><span data-ttu-id="66982-135">Segurança do contêiner</span><span class="sxs-lookup"><span data-stu-id="66982-135">Container security</span></span>
<span data-ttu-id="66982-136">Por padrão, novos contêineres são privados e não podem ser acessados ​​anonimamente.</span><span class="sxs-lookup"><span data-stu-id="66982-136">By default, new containers are private and cannot be accessed anonymously.</span></span> <span data-ttu-id="66982-137">Para tornar o contêiner público, de modo que seja possível acessá-lo anonimamente, você poderá definir o nível de acesso do contêiner como **blob** ou **contêiner**.</span><span class="sxs-lookup"><span data-stu-id="66982-137">To make the container public so that you can access it anonymously, you can set the container's access level to **blob** or **container**.</span></span>

* <span data-ttu-id="66982-138">**blob** – permite o acesso anônimo de leitura ao conteúdo e aos metadados do blob dentro desse contêiner, mas não aos metadados do contêiner, como a listagem de todos os blobs de um contêiner</span><span class="sxs-lookup"><span data-stu-id="66982-138">**blob** - allows anonymous read access to blob content and metadata within this container, but not to container metadata such as listing all blobs within a container</span></span>
* <span data-ttu-id="66982-139">**contêiner** – permite o acesso anônimo de leitura ao conteúdo e aos metadados do blob e também aos metadados do contêiner</span><span class="sxs-lookup"><span data-stu-id="66982-139">**container** - allows anonymous read access to blob content and metadata as well as container metadata</span></span>

<span data-ttu-id="66982-140">O exemplo de código a seguir demonstra a configuração do nível de acesso para **blob**:</span><span class="sxs-lookup"><span data-stu-id="66982-140">The following code example demonstrates setting the access level to **blob**:</span></span>

```nodejs
blobSvc.createContainerIfNotExists('mycontainer', {publicAccessLevel : 'blob'}, function(error, result, response){
    if(!error){
      // Container exists and allows
      // anonymous read access to blob
      // content and metadata within this container
    }
});
```

<span data-ttu-id="66982-141">Como alternativa, você poderá modificar o nível de acesso de um contêiner, usando **setContainerAcl** para especificar o nível de acesso.</span><span class="sxs-lookup"><span data-stu-id="66982-141">Alternatively, you can modify the access level of a container by using **setContainerAcl** to specify the access level.</span></span> <span data-ttu-id="66982-142">O exemplo de código a seguir altera o nível de acesso para contêiner:</span><span class="sxs-lookup"><span data-stu-id="66982-142">The following code example changes the access level to container:</span></span>

```nodejs
blobSvc.setContainerAcl('mycontainer', null /* signedIdentifiers */, {publicAccessLevel : 'container'} /* publicAccessLevel*/, function(error, result, response){
  if(!error){
    // Container access level set to 'container'
  }
});
```

<span data-ttu-id="66982-143">O resultado contém informações sobre a operação, incluindo o **ETag** atual do contêiner.</span><span class="sxs-lookup"><span data-stu-id="66982-143">The result contains information about the operation, including the current **ETag** for the container.</span></span>

### <a name="filters"></a><span data-ttu-id="66982-144">Filtros</span><span class="sxs-lookup"><span data-stu-id="66982-144">Filters</span></span>
<span data-ttu-id="66982-145">Você pode aplicar operações de filtragem opcionais às operações executadas usando o **BlobService**.</span><span class="sxs-lookup"><span data-stu-id="66982-145">You can apply optional filtering operations to operations performed using **BlobService**.</span></span> <span data-ttu-id="66982-146">As operações de filtragem podem incluir registro em log, repetição automática, etc. Os filtros são objetos que implementam um método com a assinatura:</span><span class="sxs-lookup"><span data-stu-id="66982-146">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with the signature:</span></span>

```nodejs
function handle (requestOptions, next)
```

<span data-ttu-id="66982-147">Após fazer seu pré-processamento nas opções de solicitação, o método precisará chamar "next", passando um retorno de chamada com a assinatura abaixo:</span><span class="sxs-lookup"><span data-stu-id="66982-147">After doing its preprocessing on the request options, the method needs to call "next", passing a callback with the following signature:</span></span>

```nodejs
function (returnObject, finalCallback, next)
```

<span data-ttu-id="66982-148">Nesse retorno de chamada, e após processar o returnObject (a resposta da solicitação ao servidor), o retorno de chamada precisará invocar next, se ele existir, para continuar processando outros filtros ou simplesmente invocar finalCallback para terminar a invocação de serviço.</span><span class="sxs-lookup"><span data-stu-id="66982-148">In this callback, and after processing the returnObject (the response from the request to the server), the callback needs to either invoke next if it exists to continue processing other filters or simply invoke finalCallback to end the service invocation.</span></span>

<span data-ttu-id="66982-149">Dois filtros que implementam a lógica de repetição estão incluídos no SDK do Azure para Node.js, **ExponentialRetryPolicyFilter** e **LinearRetryPolicyFilter**.</span><span class="sxs-lookup"><span data-stu-id="66982-149">Two filters that implement retry logic are included with the Azure SDK for Node.js, **ExponentialRetryPolicyFilter** and **LinearRetryPolicyFilter**.</span></span> <span data-ttu-id="66982-150">O seguinte código cria um objeto **BlobService** que usa **ExponentialRetryPolicyFilter**:</span><span class="sxs-lookup"><span data-stu-id="66982-150">The following creates a **BlobService** object that uses the **ExponentialRetryPolicyFilter**:</span></span>

```nodejs
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var blobSvc = azure.createBlobService().withFilter(retryOperations);
```

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="66982-151">Carregar um blob em um contêiner</span><span class="sxs-lookup"><span data-stu-id="66982-151">Upload a blob into a container</span></span>
<span data-ttu-id="66982-152">Há três tipos de blobs: blob de blocos, blob de páginas e blob de anexo.</span><span class="sxs-lookup"><span data-stu-id="66982-152">There are three types of blobs: block blobs, page blobs and append blobs.</span></span> <span data-ttu-id="66982-153">Blobs de bloco permitem que você carregue grandes volumes de dados com mais eficiência.</span><span class="sxs-lookup"><span data-stu-id="66982-153">Block blobs allow you to more efficiently upload large data.</span></span> <span data-ttu-id="66982-154">Blobs de anexo otimizados para operações de acréscimo.</span><span class="sxs-lookup"><span data-stu-id="66982-154">Append blobs are optimized for append operations.</span></span> <span data-ttu-id="66982-155">Blobs de página são otimizados para operações de leitura/gravação.</span><span class="sxs-lookup"><span data-stu-id="66982-155">Page blobs are optimized for read/write operations.</span></span> <span data-ttu-id="66982-156">Para saber mais, confira [Noções básicas sobre Blobs de bloco, Blobs de acréscimo e Blobs de página](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span><span class="sxs-lookup"><span data-stu-id="66982-156">For more information, see [Understanding Block Blobs, Append Blobs, and Page Blobs](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span></span>

### <a name="block-blobs"></a><span data-ttu-id="66982-157">Blobs de bloco</span><span class="sxs-lookup"><span data-stu-id="66982-157">Block blobs</span></span>
<span data-ttu-id="66982-158">Para transferir dados para um blob de bloco, use o seguinte:</span><span class="sxs-lookup"><span data-stu-id="66982-158">To upload data to a block blob, use the following:</span></span>

* <span data-ttu-id="66982-159">**createBlockBlobFromLocalFile** – cria um novo blob de blocos e carrega o conteúdo de um arquivo</span><span class="sxs-lookup"><span data-stu-id="66982-159">**createBlockBlobFromLocalFile** - creates a new block blob and uploads the contents of a file</span></span>
* <span data-ttu-id="66982-160">**createBlockBlobFromStream** – cria um novo blob de blocos e carrega o conteúdo de um fluxo</span><span class="sxs-lookup"><span data-stu-id="66982-160">**createBlockBlobFromStream** - creates a new block blob and uploads the contents of a stream</span></span>
* <span data-ttu-id="66982-161">**createBlockBlobFromText** – cria um novo blob de blocos e carrega o conteúdo de uma cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="66982-161">**createBlockBlobFromText** - creates a new block blob and uploads the contents of a string</span></span>
* <span data-ttu-id="66982-162">**createWriteStreamToBlockBlob** – fornece um fluxo de gravação para um blob de blocos</span><span class="sxs-lookup"><span data-stu-id="66982-162">**createWriteStreamToBlockBlob** - provides a write stream to a block blob</span></span>

<span data-ttu-id="66982-163">O exemplo de código a seguir carrega o conteúdo do arquivo **test.txt** em **myblob**.</span><span class="sxs-lookup"><span data-stu-id="66982-163">The following code example uploads the contents of the **test.txt** file into **myblob**.</span></span>

```nodejs
blobSvc.createBlockBlobFromLocalFile('mycontainer', 'myblob', 'test.txt', function(error, result, response){
  if(!error){
    // file uploaded
  }
});
```

<span data-ttu-id="66982-164">O `result` retornado por esses métodos contém informações sobre a operação, como o **ETag** do blob.</span><span class="sxs-lookup"><span data-stu-id="66982-164">The `result` returned by these methods contains information on the operation, such as the **ETag** of the blob.</span></span>

### <a name="append-blobs"></a><span data-ttu-id="66982-165">Blobs de acréscimo</span><span class="sxs-lookup"><span data-stu-id="66982-165">Append blobs</span></span>
<span data-ttu-id="66982-166">Para carregar dados para um novo blob de acréscimo, use o seguinte:</span><span class="sxs-lookup"><span data-stu-id="66982-166">To upload data to a new append blob, use the following:</span></span>

* <span data-ttu-id="66982-167">**createAppendBlobFromLocalFile** – cria um novo blob de acréscimo e carrega o conteúdo de um arquivo</span><span class="sxs-lookup"><span data-stu-id="66982-167">**createAppendBlobFromLocalFile** - creates a new append blob and uploads the contents of a file</span></span>
* <span data-ttu-id="66982-168">**createAppendBlobFromStream** – cria um novo blob de acréscimo e carrega o conteúdo de uma transmissão</span><span class="sxs-lookup"><span data-stu-id="66982-168">**createAppendBlobFromStream** - creates a new append blob and uploads the contents of a stream</span></span>
* <span data-ttu-id="66982-169">**createAppendBlobFromText** – cria um novo blob de acréscimo e carrega o conteúdo de uma cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="66982-169">**createAppendBlobFromText** - creates a new append blob and uploads the contents of a string</span></span>
* <span data-ttu-id="66982-170">**createWriteStreamToNewAppendBlob** – cria um novo blob de acréscimo e, então, fornece uma transmissão para gravar nela</span><span class="sxs-lookup"><span data-stu-id="66982-170">**createWriteStreamToNewAppendBlob** - creates a new append blob and then provides a stream to write to it</span></span>

<span data-ttu-id="66982-171">O exemplo de código a seguir carrega o conteúdo do arquivo **test.txt** em **myappendblob**.</span><span class="sxs-lookup"><span data-stu-id="66982-171">The following code example uploads the contents of the **test.txt** file into **myappendblob**.</span></span>

```nodejs
blobSvc.createAppendBlobFromLocalFile('mycontainer', 'myappendblob', 'test.txt', function(error, result, response){
  if(!error){
    // file uploaded
  }
});
```

<span data-ttu-id="66982-172">Para acrescentar um bloco em um blob de acréscimo existente, use o seguinte:</span><span class="sxs-lookup"><span data-stu-id="66982-172">To append a block to an existing append blob, use the following:</span></span>

* <span data-ttu-id="66982-173">**appendFromLocalFile** – acrescentar o conteúdo de um arquivo para um blob de acréscimo</span><span class="sxs-lookup"><span data-stu-id="66982-173">**appendFromLocalFile** - append the contents of a file to an existing append blob</span></span>
* <span data-ttu-id="66982-174">**appendFromStream** – acrescentar o conteúdo de uma transmissão para um blob de acréscimo existente</span><span class="sxs-lookup"><span data-stu-id="66982-174">**appendFromStream** - append the contents of a stream to an existing append blob</span></span>
* <span data-ttu-id="66982-175">**appendFromText** – acrescentar o conteúdo de uma cadeia de caracteres para um blob de acréscimo existente</span><span class="sxs-lookup"><span data-stu-id="66982-175">**appendFromText** - append the contents of a string to an existing append blob</span></span>
* <span data-ttu-id="66982-176">**appendBlockFromStream** – acrescentar o conteúdo de uma transmissão para um blob de acréscimo existente</span><span class="sxs-lookup"><span data-stu-id="66982-176">**appendBlockFromStream** - append the contents of a stream to an existing append blob</span></span>
* <span data-ttu-id="66982-177">**appendBlockFromText** – acrescentar o conteúdo de uma cadeia de caracteres para um blob de acréscimo existente</span><span class="sxs-lookup"><span data-stu-id="66982-177">**appendBlockFromText** - append the contents of a string to an existing append blob</span></span>

> [!NOTE]
> <span data-ttu-id="66982-178">As APIs appendFromXXX causarão uma falha rápida da validação do lado do cliente para evitar chamadas de servidor desnecessárias.</span><span class="sxs-lookup"><span data-stu-id="66982-178">appendFromXXX APIs will do some client-side validation to fail fast to avoid unnecessary server calls.</span></span> <span data-ttu-id="66982-179">appendBlockFromXXX não fará isso.</span><span class="sxs-lookup"><span data-stu-id="66982-179">appendBlockFromXXX won't.</span></span>
>
>

<span data-ttu-id="66982-180">O exemplo de código a seguir carrega o conteúdo do arquivo **test.txt** em **myappendblob**.</span><span class="sxs-lookup"><span data-stu-id="66982-180">The following code example uploads the contents of the **test.txt** file into **myappendblob**.</span></span>

```nodejs
blobSvc.appendFromText('mycontainer', 'myappendblob', 'text to be appended', function(error, result, response){
  if(!error){
    // text appended
  }
});
```

### <a name="page-blobs"></a><span data-ttu-id="66982-181">Blobs de página</span><span class="sxs-lookup"><span data-stu-id="66982-181">Page blobs</span></span>
<span data-ttu-id="66982-182">Para carregar dados para um blob de página, use o seguinte:</span><span class="sxs-lookup"><span data-stu-id="66982-182">To upload data to a page blob, use the following:</span></span>

* <span data-ttu-id="66982-183">**createPageBlob** – cria um novo blob de páginas de um comprimento específico</span><span class="sxs-lookup"><span data-stu-id="66982-183">**createPageBlob** - creates a new page blob of a specific length</span></span>
* <span data-ttu-id="66982-184">**createPageBlobFromLocalFile** – cria um novo blob de páginas e carrega o conteúdo de um arquivo</span><span class="sxs-lookup"><span data-stu-id="66982-184">**createPageBlobFromLocalFile** - creates a new page blob and uploads the contents of a file</span></span>
* <span data-ttu-id="66982-185">**createPageBlobFromStream** – cria um novo blob de páginas e carrega o conteúdo de um fluxo</span><span class="sxs-lookup"><span data-stu-id="66982-185">**createPageBlobFromStream** - creates a new page blob and uploads the contents of a stream</span></span>
* <span data-ttu-id="66982-186">**createWriteStreamToExistingPageBlob** – fornece um fluxo de gravação para um blob de páginas</span><span class="sxs-lookup"><span data-stu-id="66982-186">**createWriteStreamToExistingPageBlob** - provides a write stream to an existing page blob</span></span>
* <span data-ttu-id="66982-187">**createWriteStreamToNewPageBlob** – cria um novo blob de páginas e, então, fornece uma transmissão para gravar nela</span><span class="sxs-lookup"><span data-stu-id="66982-187">**createWriteStreamToNewPageBlob** - creates a new page blob and then provides a stream to write to it</span></span>

<span data-ttu-id="66982-188">O exemplo de código a seguir carrega o conteúdo do arquivo **test.txt** em **mypageblob**.</span><span class="sxs-lookup"><span data-stu-id="66982-188">The following code example uploads the contents of the **test.txt** file into **mypageblob**.</span></span>

```nodejs
blobSvc.createPageBlobFromLocalFile('mycontainer', 'mypageblob', 'test.txt', function(error, result, response){
  if(!error){
    // file uploaded
  }
});
```

> [!NOTE]
> <span data-ttu-id="66982-189">Blobs de página consistem em 'páginas’ de 512 bytes.</span><span class="sxs-lookup"><span data-stu-id="66982-189">Page blobs consist of 512-byte 'pages'.</span></span> <span data-ttu-id="66982-190">Você receberá um erro ao carregar dados com um tamanho que não seja um múltiplo de 512.</span><span class="sxs-lookup"><span data-stu-id="66982-190">You will receive an error when uploading data with a size that is not a multiple of 512.</span></span>
>
>

## <a name="list-the-blobs-in-a-container"></a><span data-ttu-id="66982-191">Listar os blobs em um contêiner</span><span class="sxs-lookup"><span data-stu-id="66982-191">List the blobs in a container</span></span>
<span data-ttu-id="66982-192">Para listar os blobs em um contêiner, use o método **listBlobsSegmented** .</span><span class="sxs-lookup"><span data-stu-id="66982-192">To list the blobs in a container, use the **listBlobsSegmented** method.</span></span> <span data-ttu-id="66982-193">Se você quiser retornar blobs com um prefixo específico, use **listBlobsSegmentedWithPrefix**.</span><span class="sxs-lookup"><span data-stu-id="66982-193">If you'd like to return blobs with a specific prefix, use **listBlobsSegmentedWithPrefix**.</span></span>

```nodejs
blobSvc.listBlobsSegmented('mycontainer', null, function(error, result, response){
  if(!error){
      // result.entries contains the entries
      // If not all blobs were returned, result.continuationToken has the continuation token.
  }
});
```

<span data-ttu-id="66982-194">O `result` contém uma coleção de `entries`, que é uma matriz de objetos que descrevem cada blob.</span><span class="sxs-lookup"><span data-stu-id="66982-194">The `result` contains an `entries` collection, which is an array of objects that describe each blob.</span></span> <span data-ttu-id="66982-195">Se todos os blobs não puderem ser retornados, o `result` também fornecerá um `continuationToken`, que poderá ser usado como o segundo parâmetro para recuperação de entradas adicionais.</span><span class="sxs-lookup"><span data-stu-id="66982-195">If all blobs cannot be returned, the `result` also provides a `continuationToken`, which you may use as the second parameter to retrieve additional entries.</span></span>

## <a name="download-blobs"></a><span data-ttu-id="66982-196">Baixar blobs</span><span class="sxs-lookup"><span data-stu-id="66982-196">Download blobs</span></span>
<span data-ttu-id="66982-197">Para baixar dados de um blob, use o seguinte:</span><span class="sxs-lookup"><span data-stu-id="66982-197">To download data from a blob, use the following:</span></span>

* <span data-ttu-id="66982-198">**getBlobToLocalFile** – grava o conteúdo do blob em um arquivo</span><span class="sxs-lookup"><span data-stu-id="66982-198">**getBlobToLocalFile** - writes the blob contents to file</span></span>
* <span data-ttu-id="66982-199">**getBlobToStream** – grava o conteúdo do blob em um fluxo</span><span class="sxs-lookup"><span data-stu-id="66982-199">**getBlobToStream** - writes the blob contents to a stream</span></span>
* <span data-ttu-id="66982-200">**getBlobToText** – grava o conteúdo do blob em uma cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="66982-200">**getBlobToText** - writes the blob contents to a string</span></span>
* <span data-ttu-id="66982-201">**createReadStream** – fornece um fluxo de leitura a partir do blob</span><span class="sxs-lookup"><span data-stu-id="66982-201">**createReadStream** - provides a stream to read from the blob</span></span>

<span data-ttu-id="66982-202">O exemplo de código a seguir demonstra como usar **getBlobToStream** para baixar o conteúdo do blob **myblob** e armazená-lo no arquivo **output.txt** usando um fluxo:</span><span class="sxs-lookup"><span data-stu-id="66982-202">The following code example demonstrates using **getBlobToStream** to download the contents of the **myblob** blob and store it to the **output.txt** file by using a stream:</span></span>

```nodejs
var fs = require('fs');
blobSvc.getBlobToStream('mycontainer', 'myblob', fs.createWriteStream('output.txt'), function(error, result, response){
  if(!error){
    // blob retrieved
  }
});
```

<span data-ttu-id="66982-203">O `result` contém informações sobre o blob, incluindo informações do **ETag** .</span><span class="sxs-lookup"><span data-stu-id="66982-203">The `result` contains information about the blob, including **ETag** information.</span></span>

## <a name="delete-a-blob"></a><span data-ttu-id="66982-204">Excluir um blob</span><span class="sxs-lookup"><span data-stu-id="66982-204">Delete a blob</span></span>
<span data-ttu-id="66982-205">Finalmente, para excluir um blob, chame **deleteBlob**.</span><span class="sxs-lookup"><span data-stu-id="66982-205">Finally, to delete a blob, call **deleteBlob**.</span></span> <span data-ttu-id="66982-206">O exemplo de código a seguir exclui o blob denominado **myblob**.</span><span class="sxs-lookup"><span data-stu-id="66982-206">The following code example deletes the blob named **myblob**.</span></span>

```nodejs
blobSvc.deleteBlob(containerName, 'myblob', function(error, response){
  if(!error){
    // Blob has been deleted
  }
});
```

## <a name="concurrent-access"></a><span data-ttu-id="66982-207">Acesso simultâneo</span><span class="sxs-lookup"><span data-stu-id="66982-207">Concurrent access</span></span>
<span data-ttu-id="66982-208">Para suportar o acesso simultâneo a uma blob por meio de vários clientes ou várias instâncias do processo, você pode usar **ETags** ou **concessões**.</span><span class="sxs-lookup"><span data-stu-id="66982-208">To support concurrent access to a blob from multiple clients or multiple process instances, you can use **ETags** or **leases**.</span></span>

* <span data-ttu-id="66982-209">**Etag** – fornece uma maneira de detectar se o blob ou o contêiner foi modificado por outro processo</span><span class="sxs-lookup"><span data-stu-id="66982-209">**Etag** - provides a way to detect that the blob or container has been modified by another process</span></span>
* <span data-ttu-id="66982-210">**Concessão** – fornece acesso exclusivo e renovável para a gravação ou a exclusão de um blob por determinado período</span><span class="sxs-lookup"><span data-stu-id="66982-210">**Lease** - provides a way to obtain exclusive, renewable, write or delete access to a blob for a period of time</span></span>

### <a name="etag"></a><span data-ttu-id="66982-211">ETag</span><span class="sxs-lookup"><span data-stu-id="66982-211">ETag</span></span>
<span data-ttu-id="66982-212">Use ETags se você precisar permitir que vários clientes ou instâncias realizem gravações no Blob de blocos ou Blob de páginas simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="66982-212">Use ETags if you need to allow multiple clients or instances to write to the block Blob or page Blob simultaneously.</span></span> <span data-ttu-id="66982-213">O ETag permite determinar se o contêiner ou o blob foi modificado desde que foi criado ou lido, o que permite evitar a substituição de alterações aplicadas por outro cliente ou processo.</span><span class="sxs-lookup"><span data-stu-id="66982-213">The ETag allows you to determine if the container or blob was modified since you initially read or created it, which allows you to avoid overwriting changes committed by another client or process.</span></span>

<span data-ttu-id="66982-214">Você pode definir condições de ETag usando o parâmetro `options.accessConditions` opcional.</span><span class="sxs-lookup"><span data-stu-id="66982-214">You can set ETag conditions by using the optional `options.accessConditions` parameter.</span></span> <span data-ttu-id="66982-215">O exemplo de código a seguir só carregará o arquivo **test.txt** se o blob já existir e tiver o valor de ETag contido por `etagToMatch`.</span><span class="sxs-lookup"><span data-stu-id="66982-215">The following code example only uploads the **test.txt** file if the blob already exists and has the ETag value contained by `etagToMatch`.</span></span>

```nodejs
blobSvc.createBlockBlobFromLocalFile('mycontainer', 'myblob', 'test.txt', { accessConditions: { EtagMatch: etagToMatch} }, function(error, result, response){
    if(!error){
    // file uploaded
  }
});
```

<span data-ttu-id="66982-216">O padrão geral ao usar ETags é:</span><span class="sxs-lookup"><span data-stu-id="66982-216">When you're using ETags, the general pattern is:</span></span>

1. <span data-ttu-id="66982-217">Obter a ETag como o resultado de uma operação de criação, lista ou obtenção.</span><span class="sxs-lookup"><span data-stu-id="66982-217">Obtain the ETag as the result of a create, list, or get operation.</span></span>
2. <span data-ttu-id="66982-218">Executar uma ação, verificando se o valor da ETag não foi modificado.</span><span class="sxs-lookup"><span data-stu-id="66982-218">Perform an action, checking that the ETag value has not been modified.</span></span>

<span data-ttu-id="66982-219">Se o valor tiver sido modificado, isso indica que outro cliente ou instância modificou o blob ou o contêiner desde que você obteve o valor do ETag.</span><span class="sxs-lookup"><span data-stu-id="66982-219">If the value was modified, this indicates that another client or instance modified the blob or container since you obtained the ETag value.</span></span>

### <a name="lease"></a><span data-ttu-id="66982-220">Concessão</span><span class="sxs-lookup"><span data-stu-id="66982-220">Lease</span></span>
<span data-ttu-id="66982-221">Você pode adquirir uma nova concessão usando o método **acquireLease** especificando o blob ou o contêiner para o qual você deseja obter uma concessão.</span><span class="sxs-lookup"><span data-stu-id="66982-221">You can acquire a new lease by using the **acquireLease** method, specifying the blob or container that you wish to obtain a lease on.</span></span> <span data-ttu-id="66982-222">Por exemplo, o código a seguir adquire uma concessão em **myblob**.</span><span class="sxs-lookup"><span data-stu-id="66982-222">For example, the following code acquires a lease on **myblob**.</span></span>

```nodejs
blobSvc.acquireLease('mycontainer', 'myblob', function(error, result, response){
  if(!error) {
    console.log('leaseId: ' + result.id);
  }
});
```

<span data-ttu-id="66982-223">As operações posteriores em **myblob** devem fornecer o parâmetro `options.leaseId`.</span><span class="sxs-lookup"><span data-stu-id="66982-223">Subsequent operations on **myblob** must provide the `options.leaseId` parameter.</span></span> <span data-ttu-id="66982-224">A ID de concessão é retornada de **acquireLease** como `result.id`.</span><span class="sxs-lookup"><span data-stu-id="66982-224">The lease ID is returned as `result.id` from **acquireLease**.</span></span>

> [!NOTE]
> <span data-ttu-id="66982-225">Por padrão, a duração da concessão é infinita.</span><span class="sxs-lookup"><span data-stu-id="66982-225">By default, the lease duration is infinite.</span></span> <span data-ttu-id="66982-226">Você pode especificar uma duração não infinita (entre 15 e 60 segundos) fornecendo o parâmetro `options.leaseDuration` .</span><span class="sxs-lookup"><span data-stu-id="66982-226">You can specify a non-infinite duration (between 15 and 60 seconds) by providing the `options.leaseDuration` parameter.</span></span>
>
>

<span data-ttu-id="66982-227">Para remover uma concessão, use **releaseLease**.</span><span class="sxs-lookup"><span data-stu-id="66982-227">To remove a lease, use **releaseLease**.</span></span> <span data-ttu-id="66982-228">Para interromper uma concessão, mas evitar que outras pessoas obtenham uma nova concessão até a expiração da duração original, use **breakLease**.</span><span class="sxs-lookup"><span data-stu-id="66982-228">To break a lease, but prevent others from obtaining a new lease until the original duration has expired, use **breakLease**.</span></span>

## <a name="work-with-shared-access-signatures"></a><span data-ttu-id="66982-229">Trabalhar com assinaturas de acesso compartilhado</span><span class="sxs-lookup"><span data-stu-id="66982-229">Work with shared access signatures</span></span>
<span data-ttu-id="66982-230">As assinaturas de acesso compartilhado (SAS) são uma forma segura de fornecer acesso granular a blobs e contêiner sem fornecer o nome ou as chaves da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="66982-230">Shared access signatures (SAS) are a secure way to provide granular access to blobs and containers without providing your storage account name or keys.</span></span> <span data-ttu-id="66982-231">As assinaturas de acesso compartilhado são frequentemente usadas para fornecer acesso limitado aos seus dados, por exemplo, ao permitir que um aplicativo móvel acesse os blobs.</span><span class="sxs-lookup"><span data-stu-id="66982-231">Shared access signatures are often used to provide limited access to your data, such as allowing a mobile app to access blobs.</span></span>

> [!NOTE]
> <span data-ttu-id="66982-232">Embora você também possa permitir o acesso anônimo aos blobs, a assinatura de acesso compartilhado permite que você ofereça um acesso mais controlado, pois é necessário gerar a SAS.</span><span class="sxs-lookup"><span data-stu-id="66982-232">While you can also allow anonymous access to blobs, shared access signatures allow you to provide more controlled access, as you must generate the SAS.</span></span>
>
>

<span data-ttu-id="66982-233">Um aplicativo confiável, como um serviço baseado em nuvem, gera uma assinatura de acesso compartilhado usando **generateSharedAccessSignature** de **BlobService** e o oferece a um aplicativo não confiável ou semiconfiável, como um aplicativo móvel.</span><span class="sxs-lookup"><span data-stu-id="66982-233">A trusted application such as a cloud-based service generates shared access signatures using the **generateSharedAccessSignature** of the **BlobService**, and provides it to an untrusted or semi-trusted application such as a mobile app.</span></span> <span data-ttu-id="66982-234">As assinaturas de acesso compartilhado são geradas usando uma política, que descreve as datas de início e de término da validade das assinaturas de acesso compartilhado, além do nível de acesso concedido ao titular das assinaturas.</span><span class="sxs-lookup"><span data-stu-id="66982-234">Shared access signatures are generated using a policy, which describes the start and end dates during which the shared access signatures are valid, as well as the access level granted to the shared access signatures holder.</span></span>

<span data-ttu-id="66982-235">O exemplo de código a seguir gera uma nova política de acesso compartilhado que permite ao titular das assinaturas de acesso compartilhado executar operações de leitura no blob **myblob** e expira 100 minutos após a hora de sua criação.</span><span class="sxs-lookup"><span data-stu-id="66982-235">The following code example generates a new shared access policy that allows the shared access signatures holder to perform read operations on the **myblob** blob, and expires 100 minutes after the time it is created.</span></span>

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

<span data-ttu-id="66982-236">Observe que também devem ser fornecidas as informações do host, já que elas são necessárias quando o titular das assinaturas de acesso compartilhado tenta acessar o contêiner.</span><span class="sxs-lookup"><span data-stu-id="66982-236">Note that the host information must be provided also, as it is required when the shared access signatures holder attempts to access the container.</span></span>

<span data-ttu-id="66982-237">Em seguida, o aplicativo cliente usa as assinaturas de acesso compartilhado com **BlobServiceWithSAS** para executar operações no blob.</span><span class="sxs-lookup"><span data-stu-id="66982-237">The client application then uses shared access signatures with **BlobServiceWithSAS** to perform operations against the blob.</span></span> <span data-ttu-id="66982-238">O seguinte obtém informações sobre **myblob**.</span><span class="sxs-lookup"><span data-stu-id="66982-238">The following gets information about **myblob**.</span></span>

```nodejs
var sharedBlobSvc = azure.createBlobServiceWithSas(host, blobSAS);
sharedBlobSvc.getBlobProperties('mycontainer', 'myblob', function (error, result, response) {
  if(!error) {
    // retrieved info
  }
});
```

<span data-ttu-id="66982-239">Como as assinaturas de acesso compartilhado foram geradas com acesso somente leitura, se for feita uma tentativa de modificar o blob, será retornado um erro.</span><span class="sxs-lookup"><span data-stu-id="66982-239">Since the shared access signatures were generated with read-only access, if an attempt is made to modify the blob, an error will be returned.</span></span>

### <a name="access-control-lists"></a><span data-ttu-id="66982-240">Listas de controle de acesso</span><span class="sxs-lookup"><span data-stu-id="66982-240">Access control lists</span></span>
<span data-ttu-id="66982-241">Você também pode usar uma lista de controle de acesso (ACL) para definir a política de acesso das SAS.</span><span class="sxs-lookup"><span data-stu-id="66982-241">You can also use an access control list (ACL) to set the access policy for SAS.</span></span> <span data-ttu-id="66982-242">Isso será útil se você quiser permitir que vários clientes acessem um contêiner, mas com políticas de acesso diferentes para cada cliente.</span><span class="sxs-lookup"><span data-stu-id="66982-242">This is useful if you wish to allow multiple clients to access a container but provide different access policies for each client.</span></span>

<span data-ttu-id="66982-243">Uma ACL é implementada através de um conjunto de políticas de acesso, com uma ID associada a cada política.</span><span class="sxs-lookup"><span data-stu-id="66982-243">An ACL is implemented using an array of access policies, with an ID associated with each policy.</span></span> <span data-ttu-id="66982-244">O exemplo de código a seguir define duas políticas, uma para "user1" e outra para 'user2':</span><span class="sxs-lookup"><span data-stu-id="66982-244">The following code example defines two policies, one for 'user1' and one for 'user2':</span></span>

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

<span data-ttu-id="66982-245">O exemplo de código a seguir obtém a ACL atual para **mycontainer** e adiciona as novas políticas usando **setBlobAcl**.</span><span class="sxs-lookup"><span data-stu-id="66982-245">The following code example gets the current ACL for **mycontainer**, and then adds the new policies using **setBlobAcl**.</span></span> <span data-ttu-id="66982-246">Essa abordagem permite:</span><span class="sxs-lookup"><span data-stu-id="66982-246">This approach allows:</span></span>

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

<span data-ttu-id="66982-247">Após a definição da ACL, você poderá criar assinaturas de acesso compartilhado com base na ID de uma política.</span><span class="sxs-lookup"><span data-stu-id="66982-247">Once the ACL is set, you can then create shared access signatures based on the ID for a policy.</span></span> <span data-ttu-id="66982-248">O exemplo de código a seguir cria novas assinaturas de acesso compartilhado para ‘user2’:</span><span class="sxs-lookup"><span data-stu-id="66982-248">The following code example creates new shared access signatures for 'user2':</span></span>

```nodejs
blobSAS = blobSvc.generateSharedAccessSignature('mycontainer', { Id: 'user2' });
```

## <a name="next-steps"></a><span data-ttu-id="66982-249">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="66982-249">Next steps</span></span>
<span data-ttu-id="66982-250">Para saber mais, consulte os recursos a seguir.</span><span class="sxs-lookup"><span data-stu-id="66982-250">For more information, see the following resources.</span></span>

* <span data-ttu-id="66982-251">[SDK de Armazenamento do Azure para Referência de API de Nó][SDK de Armazenamento do Azure para Referência de API de Nó]</span><span class="sxs-lookup"><span data-stu-id="66982-251">[Azure Storage SDK for Node API Reference][Azure Storage SDK for Node API Reference]</span></span>
* <span data-ttu-id="66982-252">[Blog da equipe de Armazenamento do Azure][Blog da equipe de Armazenamento do Azure]</span><span class="sxs-lookup"><span data-stu-id="66982-252">[Azure Storage Team Blog][Azure Storage Team Blog]</span></span>
* <span data-ttu-id="66982-253">Repositório [Microsoft Azure Storage SDK for Node.js][Azure Storage SDK for Node] (SDK do Armazenamento do Microsoft Azure para Node.js) no GitHub</span><span class="sxs-lookup"><span data-stu-id="66982-253">[Azure Storage SDK for Node][Azure Storage SDK for Node] repository on GitHub</span></span>
* [<span data-ttu-id="66982-254">Centro de Desenvolvedores do Node.js</span><span class="sxs-lookup"><span data-stu-id="66982-254">Node.js Developer Center</span></span>](https://azure.microsoft.com/develop/nodejs/)
* [<span data-ttu-id="66982-255">Transferir dados com o utilitário de linha de comando AzCopy</span><span class="sxs-lookup"><span data-stu-id="66982-255">Transfer data with the AzCopy command-line utility</span></span>](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)

[Azure Storage SDK for Node]: https://github.com/Azure/azure-storage-node

<span data-ttu-id="66982-256">[Aplicativo Web Node.js com o Serviço Tabela do Azure](../../app-service-web/storage-nodejs-use-table-storage-web-site.md)  </span><span class="sxs-lookup"><span data-stu-id="66982-256">[Node.js web app using the Azure Table Service](../../app-service-web/storage-nodejs-use-table-storage-web-site.md)  </span></span>  
<span data-ttu-id="66982-257">[Criar e implantar um aplicativo Web Node.js no Azure usando o WebMatrix]: https://www.microsoft.com/web/webmatrix/</span><span class="sxs-lookup"><span data-stu-id="66982-257">[Build and deploy a Node.js web app to Azure using Web Matrix]: https://www.microsoft.com/web/webmatrix/</span></span>  
<span data-ttu-id="66982-258">[Usando a API REST]: http://msdn.microsoft.com/library/azure/hh264518.aspx [Portal do Azure]: https://portal.azure.com [Criar e implantar um aplicativo Node.js para um Serviço de Nuvem do Azure](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) [Blog da equipe de Armazenamento do Azure]: http://blogs.msdn.com/b/windowsazurestorage/ [SDK de Armazenamento do Azure para Referência de API de Nó]: http://dl.windowsazure.com/nodestoragedocs/index.html</span><span class="sxs-lookup"><span data-stu-id="66982-258">[Using the REST API]: http://msdn.microsoft.com/library/azure/hh264518.aspx [Azure portal]: https://portal.azure.com [Build and deploy a Node.js application to an Azure Cloud Service](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) [Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/ [Azure Storage SDK for Node API Reference]: http://dl.windowsazure.com/nodestoragedocs/index.html</span></span>
