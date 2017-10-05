---
title: "Introdução ao Armazenamento de Blobs do Azure e aos Serviços Conectados do Visual Studio (ASP.NET) | Microsoft Docs"
description: "Como começar a usar o Armazenamento de Blobs do Azure em um projeto ASP.NET no Visual Studio após a conexão a uma conta de armazenamento usando os Serviços Conectados do Visual Studio"
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
ms.openlocfilehash: 8fd13efdbdd98c6d7dff1b88a6b232a08aa5a13d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-aspnet"></a><span data-ttu-id="8c72b-103">Introdução ao Armazenamento de Blobs do Azure e aos Serviços Conectados do Visual Studio (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="8c72b-103">Get started with Azure blob storage and Visual Studio Connected Services (ASP.NET)</span></span>
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="8c72b-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="8c72b-104">Overview</span></span>

<span data-ttu-id="8c72b-105">O Armazenamento de Blobs do Azure é um serviço que armazena dados não estruturados na nuvem como objetos/blobs.</span><span class="sxs-lookup"><span data-stu-id="8c72b-105">Azure blob storage is a service that stores unstructured data in the cloud as objects/blobs.</span></span> <span data-ttu-id="8c72b-106">O Armazenamento de Blobs pode conter qualquer tipo de texto ou de dados binários, como um documento, um arquivo de mídia ou um instalador de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8c72b-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="8c72b-107">O Armazenamento de Blobs também é chamado de armazenamento de objetos.</span><span class="sxs-lookup"><span data-stu-id="8c72b-107">Blob storage is also referred to as object storage.</span></span>

<span data-ttu-id="8c72b-108">Este tutorial mostra como gravar um código ASP.NET para alguns cenários comuns usando o Armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="8c72b-108">This tutorial shows how to write ASP.NET code for some common scenarios using Azure blob storage.</span></span> <span data-ttu-id="8c72b-109">Entre os cenários estão a criação de um contêiner de blobs, bem como carregamento, listagem, download e exclusão de blobs.</span><span class="sxs-lookup"><span data-stu-id="8c72b-109">Scenarios include creating a blob container, and uploading, listing, downloading, and deleting blobs.</span></span>

##<a name="prerequisites"></a><span data-ttu-id="8c72b-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="8c72b-110">Prerequisites</span></span>

* [<span data-ttu-id="8c72b-111">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8c72b-111">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="8c72b-112">Conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="8c72b-112">Azure storage account</span></span>](storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/vs-storage-aspnet-getting-started-create-azure-account.md)]

[!INCLUDE [storage-development-environment-include](../../includes/vs-storage-aspnet-getting-started-setup-dev-env.md)]

### <a name="create-an-mvc-controller"></a><span data-ttu-id="8c72b-113">Criar um controlador MVC</span><span class="sxs-lookup"><span data-stu-id="8c72b-113">Create an MVC controller</span></span> 

1. <span data-ttu-id="8c72b-114">No **Gerenciador de Soluções**, clique com o botão direito do mouse em **Controladores** e, no menu de contexto, selecione **Adicionar-> Controlador**.</span><span class="sxs-lookup"><span data-stu-id="8c72b-114">In the **Solution Explorer**, right-click **Controllers**, and, from the context menu, select **Add->Controller**.</span></span>

    ![Adicionar um controlador a um aplicativo ASP.NET MVC](./media/vs-storage-aspnet-getting-started-blobs/add-controller-menu.png)

1. <span data-ttu-id="8c72b-116">Na caixa de diálogo **Adicionar Scaffold**, clique em **Controlador MVC 5 – Vazio** e selecione **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="8c72b-116">On the **Add Scaffold** dialog, select **MVC 5 Controller - Empty**, and select **Add**.</span></span>

    ![Especificar o tipo de controlador MVC](./media/vs-storage-aspnet-getting-started-blobs/add-controller.png)

1. <span data-ttu-id="8c72b-118">Na caixa de diálogo **Adicionar Controlador**, nomeie o controlador *BlobsController* e selecione **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="8c72b-118">On the **Add Controller** dialog, name the controller *BlobsController*, and select **Add**.</span></span>

    ![Dê um nome ao controlador MVC](./media/vs-storage-aspnet-getting-started-blobs/add-controller-name.png)

1. <span data-ttu-id="8c72b-120">Adicione as seguintes diretivas *using* ao arquivo `BlobsController.cs`:</span><span class="sxs-lookup"><span data-stu-id="8c72b-120">Add the following *using* directives to the `BlobsController.cs` file:</span></span>

    ```csharp
    using Microsoft.Azure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Auth;
    using Microsoft.WindowsAzure.Storage.Blob;
    ```

## <a name="create-a-blob-container"></a><span data-ttu-id="8c72b-121">Criar um contêiner de blob</span><span class="sxs-lookup"><span data-stu-id="8c72b-121">Create a blob container</span></span>

<span data-ttu-id="8c72b-122">Um contêiner de blobs é uma hierarquia aninhada de blobs e as pastas.</span><span class="sxs-lookup"><span data-stu-id="8c72b-122">A blob container is a nested hierarchy of blobs and folders.</span></span> <span data-ttu-id="8c72b-123">As seguintes etapas ilustram como criar um contêiner de blobs:</span><span class="sxs-lookup"><span data-stu-id="8c72b-123">The following steps illustrate how to create a blob container:</span></span>

> [!NOTE]
> 
> <span data-ttu-id="8c72b-124">O código nesta seção pressupõe que você concluiu as etapas na seção, [Configurar o ambiente de desenvolvimento](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="8c72b-124">The code in this section assumes that you have completed the steps in the section, [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="8c72b-125">Abra o arquivo `BlobsController.cs` .</span><span class="sxs-lookup"><span data-stu-id="8c72b-125">Open the `BlobsController.cs` file.</span></span>

1. <span data-ttu-id="8c72b-126">Adicione um método chamado **CreateBlobContainer** que retorna um **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="8c72b-126">Add a method called **CreateBlobContainer** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult CreateBlobContainer()
    {
        // The code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="8c72b-127">Dentro do método **CreateBlobContainer** obtenha um objeto **CloudStorageAccount** que represente as informações de sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="8c72b-127">Within the **CreateBlobContainer** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="8c72b-128">Use o seguinte código para obter a cadeia de conexão de armazenamento e informações de conta de armazenamento da configuração do serviço do Azure.</span><span class="sxs-lookup"><span data-stu-id="8c72b-128">Use the following code to get the storage connection string and storage account information from the Azure service configuration.</span></span> <span data-ttu-id="8c72b-129">(Mude *&lt;nome-da-conta-de-armazenamento>* para o nome da conta de armazenamento do Azure que você está acessando.)</span><span class="sxs-lookup"><span data-stu-id="8c72b-129">(Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="8c72b-130">Obtenha um objeto **CloudBlobClient** que representa um cliente do serviço de blob.</span><span class="sxs-lookup"><span data-stu-id="8c72b-130">Get a **CloudBlobClient** object represents a blob service client.</span></span>
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="8c72b-131">Obtenha um objeto **CloudBlobContainer** que representa uma referência ao nome do contêiner de blobs desejado.</span><span class="sxs-lookup"><span data-stu-id="8c72b-131">Get a **CloudBlobContainer** object that represents a reference to the desired blob container name.</span></span> <span data-ttu-id="8c72b-132">O método **CloudBlobClient.GetContainerReference** não faz uma solicitação ao Armazenamento de Blobs.</span><span class="sxs-lookup"><span data-stu-id="8c72b-132">The **CloudBlobClient.GetContainerReference** method does not make a request against blob storage.</span></span> <span data-ttu-id="8c72b-133">A referência retorna mesmo se o contêiner de blobs não existir.</span><span class="sxs-lookup"><span data-stu-id="8c72b-133">The reference is returned whether or not the blob container exists.</span></span> 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. <span data-ttu-id="8c72b-134">Chame o método **CloudBlobContainer.CreateIfNotExists** para criar o contêiner se ele ainda não existir.</span><span class="sxs-lookup"><span data-stu-id="8c72b-134">Call the **CloudBlobContainer.CreateIfNotExists** method to create the container if it does not yet exist.</span></span> <span data-ttu-id="8c72b-135">O método **CloudBlobContainer.CreateIfNotExists** retornará **true** se o contêiner não existir e for criado com êxito.</span><span class="sxs-lookup"><span data-stu-id="8c72b-135">The **CloudBlobContainer.CreateIfNotExists** method returns **true** if the container does not exist, and is successfully created.</span></span> <span data-ttu-id="8c72b-136">Caso contrário, **false** será retornado.</span><span class="sxs-lookup"><span data-stu-id="8c72b-136">Otherwise, **false** is returned.</span></span>    

    ```csharp
    ViewBag.Success = container.CreateIfNotExists();
    ```

1. <span data-ttu-id="8c72b-137">Atualize o **ViewBag** com o nome do contêiner de blobs.</span><span class="sxs-lookup"><span data-stu-id="8c72b-137">Update the **ViewBag** with the name of the blob container.</span></span>

    ```csharp
    ViewBag.BlobContainerName = container.Name;
    ```

1. <span data-ttu-id="8c72b-138">No **Gerenciador de Soluções**, expanda a pasta **Exibições**, clique com o botão direito do mouse em **Blobs** e, no menu de contexto, selecione **Adicionar-> Exibir**.</span><span class="sxs-lookup"><span data-stu-id="8c72b-138">In the **Solution Explorer**, expand the **Views** folder, right-click **Blobs**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="8c72b-139">Na caixa de diálogo **Adicionar Exibição**, digite **CreateBlobContainer** para o nome da exibição e selecione **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="8c72b-139">On the **Add View** dialog, enter **CreateBlobContainer** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="8c72b-140">Abra `CreateBlobContainer.cshtml` e modifique-o para que se pareça com o seguinte trecho de código:</span><span class="sxs-lookup"><span data-stu-id="8c72b-140">Open `CreateBlobContainer.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Create Blob Container";
    }
    
    <h2>Create Blob Container results</h2>

    Creation of @ViewBag.BlobContainerName @(ViewBag.Success == true ? "succeeded" : "failed")
    ```

1. <span data-ttu-id="8c72b-141">No **Gerenciador de Soluções**, expanda a pasta **Exibições->Compartilhadas** e abra `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="8c72b-141">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="8c72b-142">Após o último **Html.ActionLink**, adicione o seguinte **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="8c72b-142">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Create blob container", "CreateBlobContainer", "Blobs")</li>
    ```

1. <span data-ttu-id="8c72b-143">Execute o aplicativo e selecione **Criar Contêiner de Blobs** para ver resultados semelhantes à seguinte captura de tela:</span><span class="sxs-lookup"><span data-stu-id="8c72b-143">Run the application, and select **Create Blob Container** to see results similar to the following screen shot:</span></span>
  
    ![Criar contêiner de blobs](./media/vs-storage-aspnet-getting-started-blobs/create-blob-container-results.png)

    <span data-ttu-id="8c72b-145">Conforme mencionado anteriormente, o método **CloudBlobContainer.CreateIfNotExists** retornará **true** apenas quando o contêiner não existir e for criado.</span><span class="sxs-lookup"><span data-stu-id="8c72b-145">As mentioned previously, the **CloudBlobContainer.CreateIfNotExists** method returns **true** only when the container doesn't exist and is created.</span></span> <span data-ttu-id="8c72b-146">Portanto, se você executar o aplicativo quando o contêiner existir, o método retornará **false**.</span><span class="sxs-lookup"><span data-stu-id="8c72b-146">Therefore, if you run the app when the container exists, the method returns **false**.</span></span> <span data-ttu-id="8c72b-147">Para executar o aplicativo várias vezes, exclua o contêiner antes de executar o aplicativo novamente.</span><span class="sxs-lookup"><span data-stu-id="8c72b-147">To run the app multiple times, you must delete the container before running the app again.</span></span> <span data-ttu-id="8c72b-148">A exclusão do contêiner pode ser feita com o método **CloudBlobContainer.Delete**.</span><span class="sxs-lookup"><span data-stu-id="8c72b-148">Deleting the container can be done via the **CloudBlobContainer.Delete** method.</span></span> <span data-ttu-id="8c72b-149">Também é possível excluir o contêiner usando o [Portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040) ou o [Gerenciador do Armazenamento do Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="8c72b-149">You can also delete the container using the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) or the [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span></span>  

## <a name="upload-a-blob-into-a-blob-container"></a><span data-ttu-id="8c72b-150">Carregar um blob em um contêiner de blobs</span><span class="sxs-lookup"><span data-stu-id="8c72b-150">Upload a blob into a blob container</span></span>

<span data-ttu-id="8c72b-151">Depois de [criar um contêiner de blobs](#create-a-blob-container), você pode carregar arquivos nele.</span><span class="sxs-lookup"><span data-stu-id="8c72b-151">Once you've [created a blob container](#create-a-blob-container), you can upload files into that container.</span></span> <span data-ttu-id="8c72b-152">Esta seção explica como carregar um arquivo local em um contêiner de blobs.</span><span class="sxs-lookup"><span data-stu-id="8c72b-152">This section walks you through uploading a local file to a blob container.</span></span> <span data-ttu-id="8c72b-153">Estas etapas presumem que você criou um contêiner de blobs chamado *test-blob-container*.</span><span class="sxs-lookup"><span data-stu-id="8c72b-153">The steps assume you've created a blob container named *test-blob-container*.</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="8c72b-154">O código nesta seção pressupõe que você concluiu as etapas na seção, [Configurar o ambiente de desenvolvimento](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="8c72b-154">The code in this section assumes that you have completed the steps in the section, [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="8c72b-155">Abra o arquivo `BlobsController.cs` .</span><span class="sxs-lookup"><span data-stu-id="8c72b-155">Open the `BlobsController.cs` file.</span></span>

1. <span data-ttu-id="8c72b-156">Adicione um método chamado **UploadBlob** que retorna um **EmptyResult**.</span><span class="sxs-lookup"><span data-stu-id="8c72b-156">Add a method called **UploadBlob** that returns an **EmptyResult**.</span></span>

    ```csharp
    public EmptyResult UploadBlob()
    {
        // The code in this section goes here.

        return new EmptyResult();
    }
    ```
 
1. <span data-ttu-id="8c72b-157">Dentro do método **UploadBlob** obtenha um objeto **CloudStorageAccount** que represente as informações de sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="8c72b-157">Within the **UploadBlob** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="8c72b-158">Use o seguinte código para obter as informações da cadeia de conexão e da conta de armazenamento da configuração de serviço do Azure: (Altere *&lt;nome-da-conta-de-armazenamento>* para o nome da conta de armazenamento do Azure que você está acessando.)</span><span class="sxs-lookup"><span data-stu-id="8c72b-158">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="8c72b-159">Obtenha um objeto **CloudBlobClient** que representa um cliente do serviço de blob.</span><span class="sxs-lookup"><span data-stu-id="8c72b-159">Get a **CloudBlobClient** object represents a blob service client.</span></span>
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="8c72b-160">Obtenha um objeto **CloudBlobContainer** que representa uma referência ao nome do contêiner de blobs.</span><span class="sxs-lookup"><span data-stu-id="8c72b-160">Get a **CloudBlobContainer** object that represents a reference to the blob container name.</span></span> 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. <span data-ttu-id="8c72b-161">Conforme explicado anteriormente, o Armazenamento do Azure oferece suporte a tipos diferentes de blob.</span><span class="sxs-lookup"><span data-stu-id="8c72b-161">As explained earlier, Azure storage supports different blob types.</span></span> <span data-ttu-id="8c72b-162">Para recuperar uma referência a um blob de páginas, chame o método **CloudBlobContainer.GetPageBlobReference**.</span><span class="sxs-lookup"><span data-stu-id="8c72b-162">To retrieve a reference to a page blob, call the **CloudBlobContainer.GetPageBlobReference** method.</span></span> <span data-ttu-id="8c72b-163">Para recuperar uma referência a um blob de blocos, chame o método **CloudBlobContainer.GetBlockBlobReference**.</span><span class="sxs-lookup"><span data-stu-id="8c72b-163">To retrieve a reference to a block blob, call the **CloudBlobContainer.GetBlockBlobReference** method.</span></span> <span data-ttu-id="8c72b-164">Normalmente, o blob de blocos é o tipo recomendado.</span><span class="sxs-lookup"><span data-stu-id="8c72b-164">Usually, block blob is the recommended type to use.</span></span> <span data-ttu-id="8c72b-165">(Mude <nome-do-blob>* para o nome que você quer dar ao blob após o carregamento.)</span><span class="sxs-lookup"><span data-stu-id="8c72b-165">(Change <blob-name>* to the name you want to give the blob once uploaded.)</span></span>

    ```csharp
    CloudBlockBlob blob = container.GetBlockBlobReference(<blob-name>);
    ```

1. <span data-ttu-id="8c72b-166">Quando tiver uma referência de blob, você poderá transferir qualquer fluxo de dados para ele, chamando o método **UploadFromStream** do objeto de referência do blob.</span><span class="sxs-lookup"><span data-stu-id="8c72b-166">Once you have a blob reference, you can upload any data stream to it by calling the blob reference object's **UploadFromStream** method.</span></span> <span data-ttu-id="8c72b-167">O método **UploadFromStream** cria o blob, se ele não existir, ou o substitui, se ele já existir.</span><span class="sxs-lookup"><span data-stu-id="8c72b-167">The **UploadFromStream** method creates the blob if it doesn't exist, or overwrites it if it does exist.</span></span> <span data-ttu-id="8c72b-168">(Mude *&lt;file-to-upload>* para um caminho totalmente qualificado até o arquivo que você deseja carregar.)</span><span class="sxs-lookup"><span data-stu-id="8c72b-168">(Change *&lt;file-to-upload>* to a fully qualified path to the file you want to upload.)</span></span>

    ```csharp
    using (var fileStream = System.IO.File.OpenRead(<file-to-upload>))
    {
        blob.UploadFromStream(fileStream);
    }
    ```

1. <span data-ttu-id="8c72b-169">No **Gerenciador de Soluções**, expanda a pasta **Exibições**, clique com o botão direito do mouse em **Blobs** e, no menu de contexto, selecione **Adicionar-> Exibir**.</span><span class="sxs-lookup"><span data-stu-id="8c72b-169">In the **Solution Explorer**, expand the **Views** folder, right-click **Blobs**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="8c72b-170">No **Gerenciador de Soluções**, expanda a pasta **Exibições->Compartilhadas** e abra `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="8c72b-170">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="8c72b-171">Após o último **Html.ActionLink**, adicione o seguinte **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="8c72b-171">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Upload blob", "UploadBlob", "Blobs")</li>
    ```

1. <span data-ttu-id="8c72b-172">Execute o aplicativo e selecione **Carregar blob**.</span><span class="sxs-lookup"><span data-stu-id="8c72b-172">Run the application, and select **Upload blob**.</span></span>  
  
<span data-ttu-id="8c72b-173">Esta seção — [Listar os blobs em um contêiner de blobs](#list-the-blobs-in-a-blob-container) — ilustra como listar os blobs em um contêiner de blobs.</span><span class="sxs-lookup"><span data-stu-id="8c72b-173">The section - [List the blobs in a blob container](#list-the-blobs-in-a-blob-container) - illustrates how to list the blobs in a blob container.</span></span>    

## <a name="list-the-blobs-in-a-blob-container"></a><span data-ttu-id="8c72b-174">Listar os blobs em um contêiner de blobs</span><span class="sxs-lookup"><span data-stu-id="8c72b-174">List the blobs in a blob container</span></span>

<span data-ttu-id="8c72b-175">Esta seção ilustra como listar os blobs em um contêiner de blobs.</span><span class="sxs-lookup"><span data-stu-id="8c72b-175">This section illustrates how to list the blobs in a blob container.</span></span> <span data-ttu-id="8c72b-176">O código de exemplo faz referência ao *test-blob-container* criado na seção, [Criar um contêiner de blobs](#create-a-blob-container).</span><span class="sxs-lookup"><span data-stu-id="8c72b-176">The sample code references the *test-blob-container* created in the section, [Create a blob container](#create-a-blob-container).</span></span>

> [!NOTE]
> 
> <span data-ttu-id="8c72b-177">O código nesta seção pressupõe que você concluiu as etapas na seção, [Configurar o ambiente de desenvolvimento](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="8c72b-177">The code in this section assumes that you have completed the steps in the section, [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="8c72b-178">Abra o arquivo `BlobsController.cs` .</span><span class="sxs-lookup"><span data-stu-id="8c72b-178">Open the `BlobsController.cs` file.</span></span>

1. <span data-ttu-id="8c72b-179">Adicione um método chamado **ListBlobs** que retorna um **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="8c72b-179">Add a method called **ListBlobs** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult ListBlobs()
    {
        // The code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="8c72b-180">Dentro do método **ListBlobs** obtenha um objeto **CloudStorageAccount** que represente as informações de sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="8c72b-180">Within the **ListBlobs** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="8c72b-181">Use o seguinte código para obter as informações da cadeia de conexão e da conta de armazenamento da configuração de serviço do Azure: (Altere *&lt;nome-da-conta-de-armazenamento>* para o nome da conta de armazenamento do Azure que você está acessando.)</span><span class="sxs-lookup"><span data-stu-id="8c72b-181">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="8c72b-182">Obtenha um objeto **CloudBlobClient** que representa um cliente do serviço de blob.</span><span class="sxs-lookup"><span data-stu-id="8c72b-182">Get a **CloudBlobClient** object represents a blob service client.</span></span>
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="8c72b-183">Obtenha um objeto **CloudBlobContainer** que representa uma referência ao nome do contêiner de blobs.</span><span class="sxs-lookup"><span data-stu-id="8c72b-183">Get a **CloudBlobContainer** object that represents a reference to the blob container name.</span></span> 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. <span data-ttu-id="8c72b-184">Para listar os blobs em um contêiner de blobs, use o método **CloudBlobContainer.ListBlobs**.</span><span class="sxs-lookup"><span data-stu-id="8c72b-184">To list the blobs in a blob container, use the **CloudBlobContainer.ListBlobs** method.</span></span> <span data-ttu-id="8c72b-185">O método **CloudBlobContainer.ListBlobs** retorna um objeto **IListBlobItem** convertido em um objeto **CloudBlockBlob**, **CloudPageBlob** ou **CloudBlobDirectory**.</span><span class="sxs-lookup"><span data-stu-id="8c72b-185">The **CloudBlobContainer.ListBlobs** method returns an **IListBlobItem** object that you cast to a **CloudBlockBlob**, **CloudPageBlob**, or **CloudBlobDirectory** object.</span></span> <span data-ttu-id="8c72b-186">O trecho de código a seguir enumera todos os blobs em um contêiner de blobs.</span><span class="sxs-lookup"><span data-stu-id="8c72b-186">The following code snippet enumerates all the blobs in a blob container.</span></span> <span data-ttu-id="8c72b-187">Cada blob é convertido no objeto apropriado com base no seu tipo, e seu nome (ou URI no caso de um **CloudBlobDirectory**) é adicionado a uma lista.</span><span class="sxs-lookup"><span data-stu-id="8c72b-187">Each blob is cast to the appropriate object based on its type, and its name (or URI in the case of a **CloudBlobDirectory**) is added to a list.</span></span>

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

    <span data-ttu-id="8c72b-188">Além dos blobs, os contêineres de blob podem conter diretórios.</span><span class="sxs-lookup"><span data-stu-id="8c72b-188">In addition to blobs, blob containers can contain directories.</span></span> <span data-ttu-id="8c72b-189">Vamos supor que você tenha um contêiner de blobs chamado *test-blob-container* com a seguinte hierarquia:</span><span class="sxs-lookup"><span data-stu-id="8c72b-189">Let's suppose you have a blob container called *test-blob-container* with the following hierarchy:</span></span>

        foo.png
        dir1/bar.png
        dir2/baz.png

    <span data-ttu-id="8c72b-190">Usando o exemplo de código anterior, a lista de cadeias de caracteres de **blobs** contém valores parecidos com os seguintes:</span><span class="sxs-lookup"><span data-stu-id="8c72b-190">Using the preceding code example, the **blobs** string list contains values similar to the following:</span></span>

        foo.png
        <storage-account-url>/test-blob-container/dir1
        <storage-account-url>/test-blob-container/dir2

    <span data-ttu-id="8c72b-191">Como você pode ver, a lista inclui apenas as entidades de nível superior; não as aninhadas (*bar.png* e *baz.png*).</span><span class="sxs-lookup"><span data-stu-id="8c72b-191">As you can see, the list includes only the top-level entities; not the nested ones (*bar.png* and *baz.png*).</span></span> <span data-ttu-id="8c72b-192">Para listar todas as entidades em um contêiner de blobs, você deve chamar o método **CloudBlobContainer.ListBlobs** e passar **true** para o parâmetro **useFlatBlobListing**.</span><span class="sxs-lookup"><span data-stu-id="8c72b-192">To list all the entities within a blob container, you must call the **CloudBlobContainer.ListBlobs** method and pass **true** for the **useFlatBlobListing** parameter.</span></span>    

    ```csharp
    ...
    foreach (IListBlobItem item in container.ListBlobs(useFlatBlobListing:true))
    ...
    ```

    <span data-ttu-id="8c72b-193">A configuração do parâmetro **useFlatBlobListing** como **true** retorna uma lista simples de todas as entidades no contêiner de blobs e produz os seguintes resultados:</span><span class="sxs-lookup"><span data-stu-id="8c72b-193">Setting the **useFlatBlobListing** parameter to **true** returns a flat listing of all entities in the blob container, and yields the following results:</span></span>

        foo.png
        dir1/bar.png
        dir2/baz.png

1. <span data-ttu-id="8c72b-194">No **Gerenciador de Soluções**, expanda a pasta **Exibições**, clique com o botão direito do mouse em **Blobs** e, no menu de contexto, selecione **Adicionar-> Exibir**.</span><span class="sxs-lookup"><span data-stu-id="8c72b-194">In the **Solution Explorer**, expand the **Views** folder, right-click **Blobs**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="8c72b-195">Na caixa de diálogo **Adicionar Exibição**, insira **ListBlobs** para o nome da exibição e selecione **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="8c72b-195">On the **Add View** dialog, enter **ListBlobs** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="8c72b-196">Abra `ListBlobs.cshtml` e modifique-o para que se pareça com o seguinte trecho de código:</span><span class="sxs-lookup"><span data-stu-id="8c72b-196">Open `ListBlobs.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

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

1. <span data-ttu-id="8c72b-197">No **Gerenciador de Soluções**, expanda a pasta **Exibições->Compartilhadas** e abra `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="8c72b-197">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="8c72b-198">Após o último **Html.ActionLink**, adicione o seguinte **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="8c72b-198">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("List blobs", "ListBlobs", "Blobs")</li>
    ```

1. <span data-ttu-id="8c72b-199">Execute o aplicativo e selecione **Listar blobs** para ver resultados semelhantes à seguinte captura de tela:</span><span class="sxs-lookup"><span data-stu-id="8c72b-199">Run the application, and select **List blobs** to see results similar to the following screen shot:</span></span>
  
    ![Listagem de blobs](./media/vs-storage-aspnet-getting-started-blobs/listblobs.png)

## <a name="download-blobs"></a><span data-ttu-id="8c72b-201">Baixar blobs</span><span class="sxs-lookup"><span data-stu-id="8c72b-201">Download blobs</span></span>

<span data-ttu-id="8c72b-202">Esta seção ilustra como baixar um blob e mantê-lo no armazenamento local ou ler o conteúdo em uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="8c72b-202">This section illustrates how to download a blob and either persist it to local storage or read the contents into a string.</span></span> <span data-ttu-id="8c72b-203">O código de exemplo faz referência ao *test-blob-container* criado na seção, [Criar um contêiner de blobs](#create-a-blob-container).</span><span class="sxs-lookup"><span data-stu-id="8c72b-203">The sample code references the *test-blob-container* created in the section, [Create a blob container](#create-a-blob-container).</span></span>

1. <span data-ttu-id="8c72b-204">Abra o arquivo `BlobsController.cs` .</span><span class="sxs-lookup"><span data-stu-id="8c72b-204">Open the `BlobsController.cs` file.</span></span>

1. <span data-ttu-id="8c72b-205">Adicione um método chamado **DownloadBlob** que retorna um **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="8c72b-205">Add a method called **DownloadBlob** that returns an **ActionResult**.</span></span>

    ```csharp
    public EmptyResult DownloadBlob()
    {
        // The code in this section goes here.

        return new EmptyResult();
    }
    ```
 
1. <span data-ttu-id="8c72b-206">Dentro do método **DownloadBlob** obtenha um objeto **CloudStorageAccount** que represente as informações de sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="8c72b-206">Within the **DownloadBlob** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="8c72b-207">Use o seguinte código para obter as informações da cadeia de conexão e da conta de armazenamento da configuração de serviço do Azure: (Altere *&lt;nome-da-conta-de-armazenamento>* para o nome da conta de armazenamento do Azure que você está acessando.)</span><span class="sxs-lookup"><span data-stu-id="8c72b-207">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="8c72b-208">Obtenha um objeto **CloudBlobClient** que representa um cliente do serviço de blob.</span><span class="sxs-lookup"><span data-stu-id="8c72b-208">Get a **CloudBlobClient** object represents a blob service client.</span></span>
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="8c72b-209">Obtenha um objeto **CloudBlobContainer** que representa uma referência ao nome do contêiner de blobs.</span><span class="sxs-lookup"><span data-stu-id="8c72b-209">Get a **CloudBlobContainer** object that represents a reference to the blob container name.</span></span> 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. <span data-ttu-id="8c72b-210">Obtém um objeto de referência de blob chamando o método **CloudBlobContainer.GetBlockBlobReference** ou **CloudBlobContainer.GetPageBlobReference**.</span><span class="sxs-lookup"><span data-stu-id="8c72b-210">Get a blob reference object by calling **CloudBlobContainer.GetBlockBlobReference** or **CloudBlobContainer.GetPageBlobReference** method.</span></span> <span data-ttu-id="8c72b-211">(Mude *&lt;blob-name>* para o nome do blob que você está baixando.)</span><span class="sxs-lookup"><span data-stu-id="8c72b-211">(Change *&lt;blob-name>* to the name of the blob you are downloading.)</span></span>

    ```csharp
    CloudBlockBlob blob = container.GetBlockBlobReference(<blob-name>);
    ```

1. <span data-ttu-id="8c72b-212">Para baixar um blob, use o método **CloudBlockBlob.DownloadToStream** ou **CloudPageBlob.DownloadToStream**, dependendo do tipo de blob.</span><span class="sxs-lookup"><span data-stu-id="8c72b-212">To download a blob, use the **CloudBlockBlob.DownloadToStream** or **CloudPageBlob.DownloadToStream** method, depending on the blob type.</span></span> <span data-ttu-id="8c72b-213">O trecho de código a seguir usa o método **CloudBlockBlob.DownloadToStream** para transferir o conteúdo de um blob para um objeto de fluxo que é persistido em um arquivo local: (Altere *&lt;nome-do-arquivo-local>* para o nome de arquivo totalmente qualificado que representa onde você quer que o blob seja baixado.)</span><span class="sxs-lookup"><span data-stu-id="8c72b-213">The following code snippet uses the **CloudBlockBlob.DownloadToStream** method to transfer a blob's contents to a stream object that is then persisted to a local file: (Change *&lt;local-file-name>* to the fully qualified file name representing where you want the blob downloaded.)</span></span> 

    ```csharp
    using (var fileStream = System.IO.File.OpenWrite(<local-file-name>))
    {
        blob.DownloadToStream(fileStream);
    }
    ```

1. <span data-ttu-id="8c72b-214">No **Gerenciador de Soluções**, expanda a pasta **Exibições->Compartilhadas** e abra `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="8c72b-214">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="8c72b-215">Após o último **Html.ActionLink**, adicione o seguinte **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="8c72b-215">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Download blob", "DownloadBlob", "Blobs")</li>
    ```

1. <span data-ttu-id="8c72b-216">Execute o aplicativo e selecione **Baixar blob** para baixar o blob.</span><span class="sxs-lookup"><span data-stu-id="8c72b-216">Run the application, and select **Download blob** to download the blob.</span></span> <span data-ttu-id="8c72b-217">O blob especificado na chamada ao método **CloudBlobContainer.GetBlockBlobReference** baixa no local especificado na chamada ao método **File.OpenWrite**.</span><span class="sxs-lookup"><span data-stu-id="8c72b-217">The blob specified in the **CloudBlobContainer.GetBlockBlobReference** method call downloads to the location you specify in the **File.OpenWrite** method call.</span></span> 

## <a name="delete-blobs"></a><span data-ttu-id="8c72b-218">Excluir blobs</span><span class="sxs-lookup"><span data-stu-id="8c72b-218">Delete blobs</span></span>

<span data-ttu-id="8c72b-219">As seguintes etapas ilustram como excluir um blob:</span><span class="sxs-lookup"><span data-stu-id="8c72b-219">The following steps illustrate how to delete a blob:</span></span>

> [!NOTE]
> 
> <span data-ttu-id="8c72b-220">O código nesta seção pressupõe que você concluiu as etapas na seção, [Configurar o ambiente de desenvolvimento](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="8c72b-220">The code in this section assumes that you have completed the steps in the section, [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="8c72b-221">Abra o arquivo `BlobsController.cs` .</span><span class="sxs-lookup"><span data-stu-id="8c72b-221">Open the `BlobsController.cs` file.</span></span>

1. <span data-ttu-id="8c72b-222">Adicione um método chamado **DeleteBlob** que retorna um **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="8c72b-222">Add a method called **DeleteBlob** that returns an **ActionResult**.</span></span>

    ```csharp
    public EmptyResult DeleteBlob()
    {
        // The code in this section goes here.

        return new EmptyResult();
    }
    ```

1. <span data-ttu-id="8c72b-223">Obtenha um objeto **CloudStorageAccount** que represente as informações da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="8c72b-223">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="8c72b-224">Use o seguinte código para obter as informações da cadeia de conexão e da conta de armazenamento da configuração de serviço do Azure: (Altere *&lt;nome-da-conta-de-armazenamento>* para o nome da conta de armazenamento do Azure que você está acessando.)</span><span class="sxs-lookup"><span data-stu-id="8c72b-224">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="8c72b-225">Obtenha um objeto **CloudBlobClient** que representa um cliente do serviço de blob.</span><span class="sxs-lookup"><span data-stu-id="8c72b-225">Get a **CloudBlobClient** object represents a blob service client.</span></span>
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. <span data-ttu-id="8c72b-226">Obtenha um objeto **CloudBlobContainer** que representa uma referência ao nome do contêiner de blobs.</span><span class="sxs-lookup"><span data-stu-id="8c72b-226">Get a **CloudBlobContainer** object that represents a reference to the blob container name.</span></span> 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. <span data-ttu-id="8c72b-227">Obtém um objeto de referência de blob chamando o método **CloudBlobContainer.GetBlockBlobReference** ou **CloudBlobContainer.GetPageBlobReference**.</span><span class="sxs-lookup"><span data-stu-id="8c72b-227">Get a blob reference object by calling **CloudBlobContainer.GetBlockBlobReference** or **CloudBlobContainer.GetPageBlobReference** method.</span></span> <span data-ttu-id="8c72b-228">(Mude *&lt;blob-name>* para o nome do blob que você está excluindo.)</span><span class="sxs-lookup"><span data-stu-id="8c72b-228">(Change *&lt;blob-name>* to the name of the blob you are deleting.)</span></span>

    ```csharp
    CloudBlockBlob blob = container.GetBlockBlobReference(<blob-name>);
        ```

1. To delete a blob, use the **Delete** method.

    ```csharp
    blob.Delete();
    ```

1. <span data-ttu-id="8c72b-229">No **Gerenciador de Soluções**, expanda a pasta **Exibições->Compartilhadas** e abra `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="8c72b-229">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="8c72b-230">Após o último **Html.ActionLink**, adicione o seguinte **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="8c72b-230">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Delete blob", "DeleteBlob", "Blobs")</li>
    ```

1. <span data-ttu-id="8c72b-231">Execute o aplicativo e selecione **Excluir blob** para excluir o blob especificado na chamada do método **CloudBlobContainer.GetBlockBlobReference**.</span><span class="sxs-lookup"><span data-stu-id="8c72b-231">Run the application, and select **Delete blob** to delete the blob specified in the **CloudBlobContainer.GetBlockBlobReference** method call.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="8c72b-232">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8c72b-232">Next steps</span></span>
<span data-ttu-id="8c72b-233">Consulte outros guias de recursos para obter informações sobre opções adicionais para armazenar dados no Azure.</span><span class="sxs-lookup"><span data-stu-id="8c72b-233">View more feature guides to learn about additional options for storing data in Azure.</span></span>

  * [<span data-ttu-id="8c72b-234">Introdução ao Armazenamento de Tabelas do Azure e aos Serviços Conectados do Visual Studio (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="8c72b-234">Get started with Azure table storage and Visual Studio Connected Services (ASP.NET)</span></span>](./vs-storage-aspnet-getting-started-tables.md)
  * [<span data-ttu-id="8c72b-235">Introdução ao Armazenamento de Filas do Azure e aos Serviços Conectados do Visual Studio (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="8c72b-235">Get started with Azure queue storage and Visual Studio Connected Services (ASP.NET)</span></span>](./vs-storage-aspnet-getting-started-queues.md)
