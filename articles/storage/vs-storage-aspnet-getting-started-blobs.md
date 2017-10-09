---
title: "aaaGet de Introdução ao armazenamento de BLOBs do Azure e o Visual Studio conectado serviços (ASP.NET) | Microsoft Docs"
description: Como tooget iniciado usando o armazenamento de BLOBs do Azure em um projeto do ASP.NET no Visual Studio depois de se conectar a conta de armazenamento tooa usando o Visual Studio conectado Services
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: b3497055-bef8-4c95-8567-181556b50d95
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/21/2016
ms.author: tarcher
ms.openlocfilehash: eb38889f239a63852d6928e8be10c3d3f1746e9c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-aspnet"></a><span data-ttu-id="28c98-103">Introdução ao Armazenamento de Blobs do Azure e aos Serviços Conectados do Visual Studio (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="28c98-103">Get started with Azure blob storage and Visual Studio Connected Services (ASP.NET)</span></span>
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="28c98-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="28c98-104">Overview</span></span>

<span data-ttu-id="28c98-105">Armazenamento de BLOBs do Azure é um serviço que armazena dados não estruturados em nuvem hello como objetos/blobs.</span><span class="sxs-lookup"><span data-stu-id="28c98-105">Azure blob storage is a service that stores unstructured data in hello cloud as objects/blobs.</span></span> <span data-ttu-id="28c98-106">O Armazenamento de Blobs pode conter qualquer tipo de texto ou de dados binários, como um documento, um arquivo de mídia ou um instalador de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="28c98-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="28c98-107">Armazenamento de blob também é chamado tooas armazenamento de objeto.</span><span class="sxs-lookup"><span data-stu-id="28c98-107">Blob storage is also referred tooas object storage.</span></span>

<span data-ttu-id="28c98-108">Este tutorial mostra como toowrite ASP.NET código em alguns cenários comuns usando o armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="28c98-108">This tutorial shows how toowrite ASP.NET code for some common scenarios using Azure blob storage.</span></span> <span data-ttu-id="28c98-109">Entre os cenários estão a criação de um contêiner de blobs, bem como carregamento, listagem, download e exclusão de blobs.</span><span class="sxs-lookup"><span data-stu-id="28c98-109">Scenarios include creating a blob container, and uploading, listing, downloading, and deleting blobs.</span></span>

##<a name="prerequisites"></a><span data-ttu-id="28c98-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="28c98-110">Prerequisites</span></span>

* [<span data-ttu-id="28c98-111">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="28c98-111">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="28c98-112">Conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="28c98-112">Azure storage account</span></span>](storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/vs-storage-aspnet-getting-started-create-azure-account.md)]

[!INCLUDE [storage-development-environment-include](../../includes/vs-storage-aspnet-getting-started-setup-dev-env.md)]

### <a name="create-an-mvc-controller"></a><span data-ttu-id="28c98-113">Criar um controlador MVC</span><span class="sxs-lookup"><span data-stu-id="28c98-113">Create an MVC controller</span></span> 

1. <span data-ttu-id="28c98-114">Em Olá **Gerenciador de soluções**, clique com botão direito **controladores**e, no menu de contexto hello, selecione **Adicionar -> controlador**.</span><span class="sxs-lookup"><span data-stu-id="28c98-114">In hello **Solution Explorer**, right-click **Controllers**, and, from hello context menu, select **Add->Controller**.</span></span>

    ![Adicionar um controlador tooan aplicativo ASP.NET MVC](./media/vs-storage-aspnet-getting-started-blobs/add-controller-menu.png)

1. <span data-ttu-id="28c98-116">Em Olá **adicionar Scaffold** caixa de diálogo, selecione **controlador MVC 5 - vazio**e selecione **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="28c98-116">On hello **Add Scaffold** dialog, select **MVC 5 Controller - Empty**, and select **Add**.</span></span>

    ![Especificar o tipo de controlador MVC](./media/vs-storage-aspnet-getting-started-blobs/add-controller.png)

1. <span data-ttu-id="28c98-118">Em Olá **Adicionar controlador** caixa de diálogo, o nome de controlador de saudação *BlobsController*e selecione **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="28c98-118">On hello **Add Controller** dialog, name hello controller *BlobsController*, and select **Add**.</span></span>

    ![Controlador MVC Olá nome](./media/vs-storage-aspnet-getting-started-blobs/add-controller-name.png)

1. <span data-ttu-id="28c98-120">Adicione o seguinte Olá *usando* diretivas toohello `BlobsController.cs` arquivo:</span><span class="sxs-lookup"><span data-stu-id="28c98-120">Add hello following *using* directives toohello `BlobsController.cs` file:</span></span>

    ```csharp
    using Microsoft.Azure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Auth;
    using Microsoft.WindowsAzure.Storage.Blob;
    ```

## <a name="create-a-blob-container"></a><span data-ttu-id="28c98-121">Criar um contêiner de blob</span><span class="sxs-lookup"><span data-stu-id="28c98-121">Create a blob container</span></span>

<span data-ttu-id="28c98-122">Um contêiner de blobs é uma hierarquia aninhada de blobs e as pastas.</span><span class="sxs-lookup"><span data-stu-id="28c98-122">A blob container is a nested hierarchy of blobs and folders.</span></span> <span data-ttu-id="28c98-123">Olá etapas a seguir ilustram como toocreate um contêiner de blob:</span><span class="sxs-lookup"><span data-stu-id="28c98-123">hello following steps illustrate how toocreate a blob container:</span></span>

> [!NOTE]
> 
> <span data-ttu-id="28c98-124">Olá código nesta seção pressupõe que você concluiu as etapas de saudação na seção hello, [configurar o ambiente de desenvolvimento Olá](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="28c98-124">hello code in this section assumes that you have completed hello steps in hello section, [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="28c98-125">Olá abrir `BlobsController.cs` arquivo.</span><span class="sxs-lookup"><span data-stu-id="28c98-125">Open hello `BlobsController.cs` file.</span></span>

1. <span data-ttu-id="28c98-126">Adicione um método chamado **CreateBlobContainer** que retorna um **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="28c98-126">Add a method called **CreateBlobContainer** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult CreateBlobContainer()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="28c98-127">Dentro de saudação **CreateBlobContainer** método, obter um **CloudStorageAccount** objeto que representa as informações da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="28c98-127">Within hello **CreateBlobContainer** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="28c98-128">Use Olá código tooget Olá conta de armazenamento conexão cadeia de caracteres e o armazenamento de informações a seguir da configuração de serviço do Azure de saudação.</span><span class="sxs-lookup"><span data-stu-id="28c98-128">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration.</span></span> <span data-ttu-id="28c98-129">(Alterar  *&lt;nome da conta de armazenamento >* toohello nome da saudação conta de armazenamento do Azure que você está acessando.)</span><span class="sxs-lookup"><span data-stu-id="28c98-129">(Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="28c98-130">Obtenha um objeto **CloudBlobClient** que representa um cliente do serviço de blob.</span><span class="sxs-lookup"><span data-stu-id="28c98-130">Get a **CloudBlobClient** object represents a blob service client.</span></span>
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="28c98-131">Obter um **CloudBlobContainer** objeto que representa um nome de contêiner de BLOBs desejado de toohello de referência.</span><span class="sxs-lookup"><span data-stu-id="28c98-131">Get a **CloudBlobContainer** object that represents a reference toohello desired blob container name.</span></span> <span data-ttu-id="28c98-132">Olá **CloudBlobClient.GetContainerReference** método não faz uma solicitação em relação ao armazenamento de blob.</span><span class="sxs-lookup"><span data-stu-id="28c98-132">hello **CloudBlobClient.GetContainerReference** method does not make a request against blob storage.</span></span> <span data-ttu-id="28c98-133">referência de saudação é retornada se o contêiner de blob Olá existe ou não.</span><span class="sxs-lookup"><span data-stu-id="28c98-133">hello reference is returned whether or not hello blob container exists.</span></span> 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. <span data-ttu-id="28c98-134">Chamar hello **CloudBlobContainer.CreateIfNotExists** contêiner de saudação do método toocreate se ele ainda não existir.</span><span class="sxs-lookup"><span data-stu-id="28c98-134">Call hello **CloudBlobContainer.CreateIfNotExists** method toocreate hello container if it does not yet exist.</span></span> <span data-ttu-id="28c98-135">Olá **CloudBlobContainer.CreateIfNotExists** método **true** se Olá contêiner não existe e foi criado com êxito.</span><span class="sxs-lookup"><span data-stu-id="28c98-135">hello **CloudBlobContainer.CreateIfNotExists** method returns **true** if hello container does not exist, and is successfully created.</span></span> <span data-ttu-id="28c98-136">Caso contrário, **false** será retornado.</span><span class="sxs-lookup"><span data-stu-id="28c98-136">Otherwise, **false** is returned.</span></span>    

    ```csharp
    ViewBag.Success = container.CreateIfNotExists();
    ```

1. <span data-ttu-id="28c98-137">Saudação de atualização **ViewBag** com nome Olá Olá do contêiner de blob.</span><span class="sxs-lookup"><span data-stu-id="28c98-137">Update hello **ViewBag** with hello name of hello blob container.</span></span>

    ```csharp
    ViewBag.BlobContainerName = container.Name;
    ```

1. <span data-ttu-id="28c98-138">Em hello **Solution Explorer**, expanda Olá **exibições** pasta, com o botão direito **Blobs**e no menu de contexto hello, selecione **Adicionar -> exibição**.</span><span class="sxs-lookup"><span data-stu-id="28c98-138">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Blobs**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="28c98-139">Em Olá **adicionar exibição** caixa de diálogo, digite **CreateBlobContainer** para o nome de exibição hello e selecione **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="28c98-139">On hello **Add View** dialog, enter **CreateBlobContainer** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="28c98-140">Abra `CreateBlobContainer.cshtml`e modifique-o para que ele se parece com hello trecho de código a seguir:</span><span class="sxs-lookup"><span data-stu-id="28c98-140">Open `CreateBlobContainer.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Create Blob Container";
    }
    
    <h2>Create Blob Container results</h2>

    Creation of @ViewBag.BlobContainerName @(ViewBag.Success == true ? "succeeded" : "failed")
    ```

1. <span data-ttu-id="28c98-141">Em Olá **Solution Explorer**, expanda Olá **exibições -> compartilhado** pasta e abra `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="28c98-141">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="28c98-142">Depois de saudação última **ActionLink**, adicione o seguinte de saudação **ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="28c98-142">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Create blob container", "CreateBlobContainer", "Blobs")</li>
    ```

1. <span data-ttu-id="28c98-143">Execute o aplicativo hello e selecione **criar contêiner de Blob** toosee resultados semelhante toohello captura de tela a seguir:</span><span class="sxs-lookup"><span data-stu-id="28c98-143">Run hello application, and select **Create Blob Container** toosee results similar toohello following screen shot:</span></span>
  
    ![Criar contêiner de blobs](./media/vs-storage-aspnet-getting-started-blobs/create-blob-container-results.png)

    <span data-ttu-id="28c98-145">Conforme mencionado anteriormente, Olá **CloudBlobContainer.CreateIfNotExists** método **true** somente quando o contêiner de saudação não existe e é criado.</span><span class="sxs-lookup"><span data-stu-id="28c98-145">As mentioned previously, hello **CloudBlobContainer.CreateIfNotExists** method returns **true** only when hello container doesn't exist and is created.</span></span> <span data-ttu-id="28c98-146">Portanto, se você executar o aplicativo hello quando Olá contêiner existe, método hello retorna **false**.</span><span class="sxs-lookup"><span data-stu-id="28c98-146">Therefore, if you run hello app when hello container exists, hello method returns **false**.</span></span> <span data-ttu-id="28c98-147">toorun Olá aplicativo várias vezes, você deve excluir o contêiner de saudação antes de executar novamente o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="28c98-147">toorun hello app multiple times, you must delete hello container before running hello app again.</span></span> <span data-ttu-id="28c98-148">Excluindo contêiner de saudação pode ser feito por meio de saudação **CloudBlobContainer.Delete** método.</span><span class="sxs-lookup"><span data-stu-id="28c98-148">Deleting hello container can be done via hello **CloudBlobContainer.Delete** method.</span></span> <span data-ttu-id="28c98-149">Você também pode excluir o contêiner de saudação usando Olá [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040) ou hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="28c98-149">You can also delete hello container using hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) or hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span></span>  

## <a name="upload-a-blob-into-a-blob-container"></a><span data-ttu-id="28c98-150">Carregar um blob em um contêiner de blobs</span><span class="sxs-lookup"><span data-stu-id="28c98-150">Upload a blob into a blob container</span></span>

<span data-ttu-id="28c98-151">Depois de [criar um contêiner de blobs](#create-a-blob-container), você pode carregar arquivos nele.</span><span class="sxs-lookup"><span data-stu-id="28c98-151">Once you've [created a blob container](#create-a-blob-container), you can upload files into that container.</span></span> <span data-ttu-id="28c98-152">Esta seção orienta o carregamento de um contêiner de blob tooa arquivo local.</span><span class="sxs-lookup"><span data-stu-id="28c98-152">This section walks you through uploading a local file tooa blob container.</span></span> <span data-ttu-id="28c98-153">etapas de saudação supõem que você criou um contêiner de blob denominado *contêiner de blob de teste*.</span><span class="sxs-lookup"><span data-stu-id="28c98-153">hello steps assume you've created a blob container named *test-blob-container*.</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="28c98-154">Olá código nesta seção pressupõe que você concluiu as etapas de saudação na seção hello, [configurar o ambiente de desenvolvimento Olá](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="28c98-154">hello code in this section assumes that you have completed hello steps in hello section, [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="28c98-155">Olá abrir `BlobsController.cs` arquivo.</span><span class="sxs-lookup"><span data-stu-id="28c98-155">Open hello `BlobsController.cs` file.</span></span>

1. <span data-ttu-id="28c98-156">Adicione um método chamado **UploadBlob** que retorna um **EmptyResult**.</span><span class="sxs-lookup"><span data-stu-id="28c98-156">Add a method called **UploadBlob** that returns an **EmptyResult**.</span></span>

    ```csharp
    public EmptyResult UploadBlob()
    {
        // hello code in this section goes here.

        return new EmptyResult();
    }
    ```
 
1. <span data-ttu-id="28c98-157">Dentro de saudação **UploadBlob** método, obter um **CloudStorageAccount** objeto que representa as informações da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="28c98-157">Within hello **UploadBlob** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="28c98-158">Tooget Olá conta de armazenamento conexão cadeia de caracteres e o armazenamento de informações de configuração de serviço do Azure Olá de código a seguir de saudação de uso: (alteração  *&lt;nome da conta de armazenamento >* toohello nome da saudação armazenamento do Azure conta que você está acessando.)</span><span class="sxs-lookup"><span data-stu-id="28c98-158">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="28c98-159">Obtenha um objeto **CloudBlobClient** que representa um cliente do serviço de blob.</span><span class="sxs-lookup"><span data-stu-id="28c98-159">Get a **CloudBlobClient** object represents a blob service client.</span></span>
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="28c98-160">Obter um **CloudBlobContainer** objeto que representa um nome de contêiner de blob de toohello de referência.</span><span class="sxs-lookup"><span data-stu-id="28c98-160">Get a **CloudBlobContainer** object that represents a reference toohello blob container name.</span></span> 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. <span data-ttu-id="28c98-161">Conforme explicado anteriormente, o Armazenamento do Azure oferece suporte a tipos diferentes de blob.</span><span class="sxs-lookup"><span data-stu-id="28c98-161">As explained earlier, Azure storage supports different blob types.</span></span> <span data-ttu-id="28c98-162">tooretrieve um blob de páginas de tooa de referência, chamada hello **CloudBlobContainer.GetPageBlobReference** método.</span><span class="sxs-lookup"><span data-stu-id="28c98-162">tooretrieve a reference tooa page blob, call hello **CloudBlobContainer.GetPageBlobReference** method.</span></span> <span data-ttu-id="28c98-163">tooretrieve um blob de blocos de tooa de referência, chamada hello **CloudBlobContainer.GetBlockBlobReference** método.</span><span class="sxs-lookup"><span data-stu-id="28c98-163">tooretrieve a reference tooa block blob, call hello **CloudBlobContainer.GetBlockBlobReference** method.</span></span> <span data-ttu-id="28c98-164">Geralmente, o blob de blocos é Olá recomendado toouse de tipo.</span><span class="sxs-lookup"><span data-stu-id="28c98-164">Usually, block blob is hello recommended type toouse.</span></span> <span data-ttu-id="28c98-165">(Alteração de < nome do blob > * toohello nome você deseja que o blob de saudação toogive carregado uma vez.)</span><span class="sxs-lookup"><span data-stu-id="28c98-165">(Change <blob-name>* toohello name you want toogive hello blob once uploaded.)</span></span>

    ```csharp
    CloudBlockBlob blob = container.GetBlockBlobReference(<blob-name>);
    ```

1. <span data-ttu-id="28c98-166">Quando você tem uma referência de blob, você pode carregar qualquer tooit de fluxo de dados por meio da chamada do objeto de referência do blob Olá **UploadFromStream** método.</span><span class="sxs-lookup"><span data-stu-id="28c98-166">Once you have a blob reference, you can upload any data stream tooit by calling hello blob reference object's **UploadFromStream** method.</span></span> <span data-ttu-id="28c98-167">Olá **UploadFromStream** método cria blob Olá se ele não existe ou substitui-lo se ele existir.</span><span class="sxs-lookup"><span data-stu-id="28c98-167">hello **UploadFromStream** method creates hello blob if it doesn't exist, or overwrites it if it does exist.</span></span> <span data-ttu-id="28c98-168">(Alterar  *&lt;carregamento do arquivo >* tooa totalmente qualificado caminho toohello arquivo desejado tooupload.)</span><span class="sxs-lookup"><span data-stu-id="28c98-168">(Change *&lt;file-to-upload>* tooa fully qualified path toohello file you want tooupload.)</span></span>

    ```csharp
    using (var fileStream = System.IO.File.OpenRead(<file-to-upload>))
    {
        blob.UploadFromStream(fileStream);
    }
    ```

1. <span data-ttu-id="28c98-169">Em hello **Solution Explorer**, expanda Olá **exibições** pasta, com o botão direito **Blobs**e no menu de contexto hello, selecione **Adicionar -> exibição**.</span><span class="sxs-lookup"><span data-stu-id="28c98-169">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Blobs**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="28c98-170">Em Olá **Solution Explorer**, expanda Olá **exibições -> compartilhado** pasta e abra `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="28c98-170">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="28c98-171">Depois de saudação última **ActionLink**, adicione o seguinte de saudação **ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="28c98-171">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Upload blob", "UploadBlob", "Blobs")</li>
    ```

1. <span data-ttu-id="28c98-172">Execute o aplicativo hello e selecione **carregar blob**.</span><span class="sxs-lookup"><span data-stu-id="28c98-172">Run hello application, and select **Upload blob**.</span></span>  
  
<span data-ttu-id="28c98-173">Olá seção - [lista Olá blobs em um contêiner de blob](#list-the-blobs-in-a-blob-container) -ilustra como Olá toolist blobs em um contêiner de blob.</span><span class="sxs-lookup"><span data-stu-id="28c98-173">hello section - [List hello blobs in a blob container](#list-the-blobs-in-a-blob-container) - illustrates how toolist hello blobs in a blob container.</span></span>  

## <a name="list-hello-blobs-in-a-blob-container"></a><span data-ttu-id="28c98-174">Saudação de listar blobs em um contêiner de blob</span><span class="sxs-lookup"><span data-stu-id="28c98-174">List hello blobs in a blob container</span></span>

<span data-ttu-id="28c98-175">Esta seção ilustra como Olá toolist blobs em um contêiner de blob.</span><span class="sxs-lookup"><span data-stu-id="28c98-175">This section illustrates how toolist hello blobs in a blob container.</span></span> <span data-ttu-id="28c98-176">código de exemplo Hello referencia Olá *contêiner de blob de teste* criado na seção hello, [criar um contêiner de blob](#create-a-blob-container).</span><span class="sxs-lookup"><span data-stu-id="28c98-176">hello sample code references hello *test-blob-container* created in hello section, [Create a blob container](#create-a-blob-container).</span></span>

> [!NOTE]
> 
> <span data-ttu-id="28c98-177">Olá código nesta seção pressupõe que você concluiu as etapas de saudação na seção hello, [configurar o ambiente de desenvolvimento Olá](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="28c98-177">hello code in this section assumes that you have completed hello steps in hello section, [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="28c98-178">Olá abrir `BlobsController.cs` arquivo.</span><span class="sxs-lookup"><span data-stu-id="28c98-178">Open hello `BlobsController.cs` file.</span></span>

1. <span data-ttu-id="28c98-179">Adicione um método chamado **ListBlobs** que retorna um **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="28c98-179">Add a method called **ListBlobs** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult ListBlobs()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="28c98-180">Dentro de saudação **ListBlobs** método, obter um **CloudStorageAccount** objeto que representa as informações da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="28c98-180">Within hello **ListBlobs** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="28c98-181">Tooget Olá conta de armazenamento conexão cadeia de caracteres e o armazenamento de informações de configuração de serviço do Azure Olá de código a seguir de saudação de uso: (alteração  *&lt;nome da conta de armazenamento >* toohello nome da saudação armazenamento do Azure conta que você está acessando.)</span><span class="sxs-lookup"><span data-stu-id="28c98-181">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="28c98-182">Obtenha um objeto **CloudBlobClient** que representa um cliente do serviço de blob.</span><span class="sxs-lookup"><span data-stu-id="28c98-182">Get a **CloudBlobClient** object represents a blob service client.</span></span>
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="28c98-183">Obter um **CloudBlobContainer** objeto que representa um nome de contêiner de blob de toohello de referência.</span><span class="sxs-lookup"><span data-stu-id="28c98-183">Get a **CloudBlobContainer** object that represents a reference toohello blob container name.</span></span> 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. <span data-ttu-id="28c98-184">blobs de saudação toolist em um contêiner de blob, use Olá **Cloudblobcontainer** método.</span><span class="sxs-lookup"><span data-stu-id="28c98-184">toolist hello blobs in a blob container, use hello **CloudBlobContainer.ListBlobs** method.</span></span> <span data-ttu-id="28c98-185">Olá **Cloudblobcontainer** método retorna um **IListBlobItem** do objeto que você converta tooa **CloudBlockBlob**, **CloudPageBlob**, ou **CloudBlobDirectory** objeto.</span><span class="sxs-lookup"><span data-stu-id="28c98-185">hello **CloudBlobContainer.ListBlobs** method returns an **IListBlobItem** object that you cast tooa **CloudBlockBlob**, **CloudPageBlob**, or **CloudBlobDirectory** object.</span></span> <span data-ttu-id="28c98-186">Olá trecho de código a seguir enumera todos os blobs de saudação em um contêiner de blob.</span><span class="sxs-lookup"><span data-stu-id="28c98-186">hello following code snippet enumerates all hello blobs in a blob container.</span></span> <span data-ttu-id="28c98-187">Cada blob é toohello converter objeto apropriado com base no seu tipo e seu nome (ou URI no caso de saudação de um **CloudBlobDirectory**) é adicionado tooa lista.</span><span class="sxs-lookup"><span data-stu-id="28c98-187">Each blob is cast toohello appropriate object based on its type, and its name (or URI in hello case of a **CloudBlobDirectory**) is added tooa list.</span></span>

    ```csharp
    List<string> blobs = new List<string>();

    foreach (IListBlobItem item in container.ListBlobs(null, false))
    {
        if (item.GetType() == typeof(CloudBlockBlob))
        {
            CloudBlockBlob blob = (CloudBlockBlob)item;
            blobs.Add(blob.Name);
        }
        else if (item.GetType() == typeof(CloudPageBlob))
        {
            CloudPageBlob blob = (CloudPageBlob)item;
            blobs.Add(blob.Name);
        }
        else if (item.GetType() == typeof(CloudBlobDirectory))
        {
            CloudBlobDirectory dir = (CloudBlobDirectory)item;
            blobs.Add(dir.Uri.ToString());
        }
    }

    return View(blobs);
    ```

    <span data-ttu-id="28c98-188">Em adição tooblobs, contêineres de blob podem conter diretórios.</span><span class="sxs-lookup"><span data-stu-id="28c98-188">In addition tooblobs, blob containers can contain directories.</span></span> <span data-ttu-id="28c98-189">Vamos supor que você tem um contêiner de blob chamado *contêiner de blob de teste* com hello hierarquia a seguir:</span><span class="sxs-lookup"><span data-stu-id="28c98-189">Let's suppose you have a blob container called *test-blob-container* with hello following hierarchy:</span></span>

        foo.png
        dir1/bar.png
        dir2/baz.png

    <span data-ttu-id="28c98-190">Usando Olá precede o exemplo de código, Olá **blobs** lista de cadeia de caracteres contém a seguir toohello semelhante valores:</span><span class="sxs-lookup"><span data-stu-id="28c98-190">Using hello preceding code example, hello **blobs** string list contains values similar toohello following:</span></span>

        foo.png
        <storage-account-url>/test-blob-container/dir1
        <storage-account-url>/test-blob-container/dir2

    <span data-ttu-id="28c98-191">Como você pode ver, lista de saudação inclui somente Olá nível superior entidades; Olá não aninhado aqueles (*bar.png* e *baz.png*).</span><span class="sxs-lookup"><span data-stu-id="28c98-191">As you can see, hello list includes only hello top-level entities; not hello nested ones (*bar.png* and *baz.png*).</span></span> <span data-ttu-id="28c98-192">toolist todos Olá entidades dentro de um contêiner de blob, você deve chamar hello **Cloudblobcontainer** método e passe **true** para Olá **useFlatBlobListing** parâmetro.</span><span class="sxs-lookup"><span data-stu-id="28c98-192">toolist all hello entities within a blob container, you must call hello **CloudBlobContainer.ListBlobs** method and pass **true** for hello **useFlatBlobListing** parameter.</span></span>    

    ```csharp
    ...
    foreach (IListBlobItem item in container.ListBlobs(useFlatBlobListing:true))
    ...
    ```

    <span data-ttu-id="28c98-193">Saudação de configuração **useFlatBlobListing** parâmetro muito**true** retorna uma lista simples de todas as entidades no contêiner de blob hello e produz Olá resultados a seguir:</span><span class="sxs-lookup"><span data-stu-id="28c98-193">Setting hello **useFlatBlobListing** parameter too**true** returns a flat listing of all entities in hello blob container, and yields hello following results:</span></span>

        foo.png
        dir1/bar.png
        dir2/baz.png

1. <span data-ttu-id="28c98-194">Em hello **Solution Explorer**, expanda Olá **exibições** pasta, com o botão direito **Blobs**e no menu de contexto hello, selecione **Adicionar -> exibição**.</span><span class="sxs-lookup"><span data-stu-id="28c98-194">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Blobs**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="28c98-195">Em Olá **adicionar exibição** caixa de diálogo, digite **ListBlobs** para o nome de exibição hello e selecione **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="28c98-195">On hello **Add View** dialog, enter **ListBlobs** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="28c98-196">Abra `ListBlobs.cshtml`e modifique-o para que ele se parece com hello trecho de código a seguir:</span><span class="sxs-lookup"><span data-stu-id="28c98-196">Open `ListBlobs.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```html
    @model List<string>
    @{
        ViewBag.Title = "List blobs";
    }
    
    <h2>List blobs</h2>
    
    <ul>
        @foreach (var item in Model)
        {
        <li>@item</li>
        }
    </ul>
    ```

1. <span data-ttu-id="28c98-197">Em Olá **Solution Explorer**, expanda Olá **exibições -> compartilhado** pasta e abra `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="28c98-197">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="28c98-198">Depois de saudação última **ActionLink**, adicione o seguinte de saudação **ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="28c98-198">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("List blobs", "ListBlobs", "Blobs")</li>
    ```

1. <span data-ttu-id="28c98-199">Execute o aplicativo hello e selecione **listar blobs** toosee resultados semelhante toohello captura de tela a seguir:</span><span class="sxs-lookup"><span data-stu-id="28c98-199">Run hello application, and select **List blobs** toosee results similar toohello following screen shot:</span></span>
  
    ![Listagem de blobs](./media/vs-storage-aspnet-getting-started-blobs/listblobs.png)

## <a name="download-blobs"></a><span data-ttu-id="28c98-201">Baixar blobs</span><span class="sxs-lookup"><span data-stu-id="28c98-201">Download blobs</span></span>

<span data-ttu-id="28c98-202">Esta seção ilustra como toodownload um blob e a mantê-lo toolocal conteúdo de saudação de armazenamento ou de leitura em uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="28c98-202">This section illustrates how toodownload a blob and either persist it toolocal storage or read hello contents into a string.</span></span> <span data-ttu-id="28c98-203">código de exemplo Hello referencia Olá *contêiner de blob de teste* criado na seção hello, [criar um contêiner de blob](#create-a-blob-container).</span><span class="sxs-lookup"><span data-stu-id="28c98-203">hello sample code references hello *test-blob-container* created in hello section, [Create a blob container](#create-a-blob-container).</span></span>

1. <span data-ttu-id="28c98-204">Olá abrir `BlobsController.cs` arquivo.</span><span class="sxs-lookup"><span data-stu-id="28c98-204">Open hello `BlobsController.cs` file.</span></span>

1. <span data-ttu-id="28c98-205">Adicione um método chamado **DownloadBlob** que retorna um **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="28c98-205">Add a method called **DownloadBlob** that returns an **ActionResult**.</span></span>

    ```csharp
    public EmptyResult DownloadBlob()
    {
        // hello code in this section goes here.

        return new EmptyResult();
    }
    ```
 
1. <span data-ttu-id="28c98-206">Dentro de saudação **DownloadBlob** método, obter um **CloudStorageAccount** objeto que representa as informações da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="28c98-206">Within hello **DownloadBlob** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="28c98-207">Tooget Olá conta de armazenamento conexão cadeia de caracteres e o armazenamento de informações de configuração de serviço do Azure Olá de código a seguir de saudação de uso: (alteração  *&lt;nome da conta de armazenamento >* toohello nome da saudação armazenamento do Azure conta que você está acessando.)</span><span class="sxs-lookup"><span data-stu-id="28c98-207">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="28c98-208">Obtenha um objeto **CloudBlobClient** que representa um cliente do serviço de blob.</span><span class="sxs-lookup"><span data-stu-id="28c98-208">Get a **CloudBlobClient** object represents a blob service client.</span></span>
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="28c98-209">Obter um **CloudBlobContainer** objeto que representa um nome de contêiner de blob de toohello de referência.</span><span class="sxs-lookup"><span data-stu-id="28c98-209">Get a **CloudBlobContainer** object that represents a reference toohello blob container name.</span></span> 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. <span data-ttu-id="28c98-210">Obtém um objeto de referência de blob chamando o método **CloudBlobContainer.GetBlockBlobReference** ou **CloudBlobContainer.GetPageBlobReference**.</span><span class="sxs-lookup"><span data-stu-id="28c98-210">Get a blob reference object by calling **CloudBlobContainer.GetBlockBlobReference** or **CloudBlobContainer.GetPageBlobReference** method.</span></span> <span data-ttu-id="28c98-211">(Alterar  *&lt;nome do blob >* toohello nome de blob Olá baixar.)</span><span class="sxs-lookup"><span data-stu-id="28c98-211">(Change *&lt;blob-name>* toohello name of hello blob you are downloading.)</span></span>

    ```csharp
    CloudBlockBlob blob = container.GetBlockBlobReference(<blob-name>);
    ```

1. <span data-ttu-id="28c98-212">toodownload um blob, use Olá **CloudBlockBlob.DownloadToStream** ou **CloudPageBlob.DownloadToStream** método, dependendo do tipo de blob hello.</span><span class="sxs-lookup"><span data-stu-id="28c98-212">toodownload a blob, use hello **CloudBlockBlob.DownloadToStream** or **CloudPageBlob.DownloadToStream** method, depending on hello blob type.</span></span> <span data-ttu-id="28c98-213">trecho de código a seguir Hello usa Olá **CloudBlockBlob.DownloadToStream** método tootransfer objeto de fluxo de tooa de conteúdo do blob que é então persistidos arquivo local tooa: (alteração  *&lt;nome de arquivo local >* toohello totalmente qualificado arquivo nome que representa onde você deseja que o blob Olá baixado.)</span><span class="sxs-lookup"><span data-stu-id="28c98-213">hello following code snippet uses hello **CloudBlockBlob.DownloadToStream** method tootransfer a blob's contents tooa stream object that is then persisted tooa local file: (Change *&lt;local-file-name>* toohello fully qualified file name representing where you want hello blob downloaded.)</span></span> 

    ```csharp
    using (var fileStream = System.IO.File.OpenWrite(<local-file-name>))
    {
        blob.DownloadToStream(fileStream);
    }
    ```

1. <span data-ttu-id="28c98-214">Em Olá **Solution Explorer**, expanda Olá **exibições -> compartilhado** pasta e abra `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="28c98-214">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="28c98-215">Depois de saudação última **ActionLink**, adicione o seguinte de saudação **ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="28c98-215">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Download blob", "DownloadBlob", "Blobs")</li>
    ```

1. <span data-ttu-id="28c98-216">Execute o aplicativo hello e selecione **Download blob** blob de saudação toodownload.</span><span class="sxs-lookup"><span data-stu-id="28c98-216">Run hello application, and select **Download blob** toodownload hello blob.</span></span> <span data-ttu-id="28c98-217">blob de saudação especificado no hello **CloudBlobContainer.GetBlockBlobReference** chamada de método downloads toohello local especificado no hello **File.OpenWrite** chamada de método.</span><span class="sxs-lookup"><span data-stu-id="28c98-217">hello blob specified in hello **CloudBlobContainer.GetBlockBlobReference** method call downloads toohello location you specify in hello **File.OpenWrite** method call.</span></span> 

## <a name="delete-blobs"></a><span data-ttu-id="28c98-218">Excluir blobs</span><span class="sxs-lookup"><span data-stu-id="28c98-218">Delete blobs</span></span>

<span data-ttu-id="28c98-219">Olá etapas a seguir ilustram como toodelete um blob:</span><span class="sxs-lookup"><span data-stu-id="28c98-219">hello following steps illustrate how toodelete a blob:</span></span>

> [!NOTE]
> 
> <span data-ttu-id="28c98-220">Olá código nesta seção pressupõe que você concluiu as etapas de saudação na seção hello, [configurar o ambiente de desenvolvimento Olá](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="28c98-220">hello code in this section assumes that you have completed hello steps in hello section, [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="28c98-221">Olá abrir `BlobsController.cs` arquivo.</span><span class="sxs-lookup"><span data-stu-id="28c98-221">Open hello `BlobsController.cs` file.</span></span>

1. <span data-ttu-id="28c98-222">Adicione um método chamado **DeleteBlob** que retorna um **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="28c98-222">Add a method called **DeleteBlob** that returns an **ActionResult**.</span></span>

    ```csharp
    public EmptyResult DeleteBlob()
    {
        // hello code in this section goes here.

        return new EmptyResult();
    }
    ```

1. <span data-ttu-id="28c98-223">Obtenha um objeto **CloudStorageAccount** que represente as informações da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="28c98-223">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="28c98-224">Tooget Olá conta de armazenamento conexão cadeia de caracteres e o armazenamento de informações de configuração de serviço do Azure Olá de código a seguir de saudação de uso: (alteração  *&lt;nome da conta de armazenamento >* toohello nome da saudação armazenamento do Azure conta que você está acessando.)</span><span class="sxs-lookup"><span data-stu-id="28c98-224">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="28c98-225">Obtenha um objeto **CloudBlobClient** que representa um cliente do serviço de blob.</span><span class="sxs-lookup"><span data-stu-id="28c98-225">Get a **CloudBlobClient** object represents a blob service client.</span></span>
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="28c98-226">Obter um **CloudBlobContainer** objeto que representa um nome de contêiner de blob de toohello de referência.</span><span class="sxs-lookup"><span data-stu-id="28c98-226">Get a **CloudBlobContainer** object that represents a reference toohello blob container name.</span></span> 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. <span data-ttu-id="28c98-227">Obtém um objeto de referência de blob chamando o método **CloudBlobContainer.GetBlockBlobReference** ou **CloudBlobContainer.GetPageBlobReference**.</span><span class="sxs-lookup"><span data-stu-id="28c98-227">Get a blob reference object by calling **CloudBlobContainer.GetBlockBlobReference** or **CloudBlobContainer.GetPageBlobReference** method.</span></span> <span data-ttu-id="28c98-228">(Alterar  *&lt;nome do blob >* toohello nome de blob Olá você está excluindo.)</span><span class="sxs-lookup"><span data-stu-id="28c98-228">(Change *&lt;blob-name>* toohello name of hello blob you are deleting.)</span></span>

    ```csharp
    CloudBlockBlob blob = container.GetBlockBlobReference(<blob-name>);
        ```

1. toodelete a blob, use hello **Delete** method.

    ```csharp
    blob.Delete();
    ```

1. <span data-ttu-id="28c98-229">Em Olá **Solution Explorer**, expanda Olá **exibições -> compartilhado** pasta e abra `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="28c98-229">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="28c98-230">Depois de saudação última **ActionLink**, adicione o seguinte de saudação **ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="28c98-230">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Delete blob", "DeleteBlob", "Blobs")</li>
    ```

1. <span data-ttu-id="28c98-231">Execute o aplicativo hello e selecione **excluir blob** toodelete blob de saudação especificado no hello **CloudBlobContainer.GetBlockBlobReference** chamada de método.</span><span class="sxs-lookup"><span data-stu-id="28c98-231">Run hello application, and select **Delete blob** toodelete hello blob specified in hello **CloudBlobContainer.GetBlockBlobReference** method call.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="28c98-232">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="28c98-232">Next steps</span></span>
<span data-ttu-id="28c98-233">Exiba toolearn de guias de recurso mais sobre opções adicionais para armazenar dados no Azure.</span><span class="sxs-lookup"><span data-stu-id="28c98-233">View more feature guides toolearn about additional options for storing data in Azure.</span></span>

  * [<span data-ttu-id="28c98-234">Introdução ao Armazenamento de Tabelas do Azure e aos Serviços Conectados do Visual Studio (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="28c98-234">Get started with Azure table storage and Visual Studio Connected Services (ASP.NET)</span></span>](./vs-storage-aspnet-getting-started-tables.md)
  * [<span data-ttu-id="28c98-235">Introdução ao Armazenamento de Filas do Azure e aos Serviços Conectados do Visual Studio (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="28c98-235">Get started with Azure queue storage and Visual Studio Connected Services (ASP.NET)</span></span>](./vs-storage-aspnet-getting-started-queues.md)
