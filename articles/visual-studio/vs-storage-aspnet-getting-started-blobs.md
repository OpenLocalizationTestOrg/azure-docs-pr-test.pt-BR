---
title: "aaaGet de Introdução ao armazenamento de BLOBs do Azure e o Visual Studio conectado serviços (ASP.NET) | Microsoft Docs"
description: Como tooget iniciado usando o armazenamento de BLOBs do Azure em um projeto do ASP.NET no Visual Studio depois de se conectar a conta de armazenamento tooa usando o Visual Studio conectado Services
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: b3497055-bef8-4c95-8567-181556b50d95
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/21/2016
ms.author: kraig
ms.openlocfilehash: 7b3e160da5bb95967ca4650b124afb8e867c03d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-aspnet"></a>Introdução ao Armazenamento de Blobs do Azure e aos Serviços Conectados do Visual Studio (ASP.NET)
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>Visão geral

Armazenamento de BLOBs do Azure é um serviço que armazena dados não estruturados em nuvem hello como objetos/blobs. O Armazenamento de Blobs pode conter qualquer tipo de texto ou de dados binários, como um documento, um arquivo de mídia ou um instalador de aplicativo. Armazenamento de blob também é chamado tooas armazenamento de objeto.

Este tutorial mostra como toowrite ASP.NET código em alguns cenários comuns usando o armazenamento de BLOBs do Azure. Entre os cenários estão a criação de um contêiner de blobs, bem como carregamento, listagem, download e exclusão de blobs.

##<a name="prerequisites"></a>Pré-requisitos

* [Microsoft Visual Studio](https://www.visualstudio.com/downloads/)
* [Conta de armazenamento do Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/vs-storage-aspnet-getting-started-create-azure-account.md)]

[!INCLUDE [storage-development-environment-include](../../includes/vs-storage-aspnet-getting-started-setup-dev-env.md)]

### <a name="create-an-mvc-controller"></a>Criar um controlador MVC 

1. Em Olá **Gerenciador de soluções**, clique com botão direito **controladores**e, no menu de contexto hello, selecione **Adicionar -> controlador**.

    ![Adicionar um controlador tooan aplicativo ASP.NET MVC](./media/vs-storage-aspnet-getting-started-blobs/add-controller-menu.png)

1. Em Olá **adicionar Scaffold** caixa de diálogo, selecione **controlador MVC 5 - vazio**e selecione **adicionar**.

    ![Especificar o tipo de controlador MVC](./media/vs-storage-aspnet-getting-started-blobs/add-controller.png)

1. Em Olá **Adicionar controlador** caixa de diálogo, o nome de controlador de saudação *BlobsController*e selecione **adicionar**.

    ![Controlador MVC Olá nome](./media/vs-storage-aspnet-getting-started-blobs/add-controller-name.png)

1. Adicione o seguinte Olá *usando* diretivas toohello `BlobsController.cs` arquivo:

    ```csharp
    using Microsoft.Azure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Auth;
    using Microsoft.WindowsAzure.Storage.Blob;
    ```

## <a name="create-a-blob-container"></a>Criar um contêiner de blob

Um contêiner de blobs é uma hierarquia aninhada de blobs e as pastas. Olá etapas a seguir ilustram como toocreate um contêiner de blob:

> [!NOTE]
> 
> Olá código nesta seção pressupõe que você concluiu as etapas de saudação na seção hello, [configurar o ambiente de desenvolvimento Olá](#set-up-the-development-environment). 

1. Olá abrir `BlobsController.cs` arquivo.

1. Adicione um método chamado **CreateBlobContainer** que retorna um **ActionResult**.

    ```csharp
    public ActionResult CreateBlobContainer()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. Dentro de saudação **CreateBlobContainer** método, obter um **CloudStorageAccount** objeto que representa as informações da conta de armazenamento. Use Olá código tooget Olá conta de armazenamento conexão cadeia de caracteres e o armazenamento de informações a seguir da configuração de serviço do Azure de saudação. (Alterar  *&lt;nome da conta de armazenamento >* toohello nome da saudação conta de armazenamento do Azure que você está acessando.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. Obtenha um objeto **CloudBlobClient** que representa um cliente do serviço de blob.
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. Obter um **CloudBlobContainer** objeto que representa um nome de contêiner de BLOBs desejado de toohello de referência. Olá **CloudBlobClient.GetContainerReference** método não faz uma solicitação em relação ao armazenamento de blob. referência de saudação é retornada se o contêiner de blob Olá existe ou não. 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. Chamar hello **CloudBlobContainer.CreateIfNotExists** contêiner de saudação do método toocreate se ele ainda não existir. Olá **CloudBlobContainer.CreateIfNotExists** método **true** se Olá contêiner não existe e foi criado com êxito. Caso contrário, **false** será retornado.    

    ```csharp
    ViewBag.Success = container.CreateIfNotExists();
    ```

1. Saudação de atualização **ViewBag** com nome Olá Olá do contêiner de blob.

    ```csharp
    ViewBag.BlobContainerName = container.Name;
    ```

1. Em hello **Solution Explorer**, expanda Olá **exibições** pasta, com o botão direito **Blobs**e no menu de contexto hello, selecione **Adicionar -> exibição**.

1. Em Olá **adicionar exibição** caixa de diálogo, digite **CreateBlobContainer** para o nome de exibição hello e selecione **adicionar**.

1. Abra `CreateBlobContainer.cshtml`e modifique-o para que ele se parece com hello trecho de código a seguir:

    ```csharp
    @{
        ViewBag.Title = "Create Blob Container";
    }
    
    <h2>Create Blob Container results</h2>

    Creation of @ViewBag.BlobContainerName @(ViewBag.Success == true ? "succeeded" : "failed")
    ```

1. Em Olá **Solution Explorer**, expanda Olá **exibições -> compartilhado** pasta e abra `_Layout.cshtml`.

1. Depois de saudação última **ActionLink**, adicione o seguinte de saudação **ActionLink**:

    ```html
    <li>@Html.ActionLink("Create blob container", "CreateBlobContainer", "Blobs")</li>
    ```

1. Execute o aplicativo hello e selecione **criar contêiner de Blob** toosee resultados semelhante toohello captura de tela a seguir:
  
    ![Criar contêiner de blobs](./media/vs-storage-aspnet-getting-started-blobs/create-blob-container-results.png)

    Conforme mencionado anteriormente, Olá **CloudBlobContainer.CreateIfNotExists** método **true** somente quando o contêiner de saudação não existe e é criado. Portanto, se você executar o aplicativo hello quando Olá contêiner existe, método hello retorna **false**. toorun Olá aplicativo várias vezes, você deve excluir o contêiner de saudação antes de executar novamente o aplicativo hello. Excluindo contêiner de saudação pode ser feito por meio de saudação **CloudBlobContainer.Delete** método. Você também pode excluir o contêiner de saudação usando Olá [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040) ou hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).  

## <a name="upload-a-blob-into-a-blob-container"></a>Carregar um blob em um contêiner de blobs

Depois de [criar um contêiner de blobs](#create-a-blob-container), você pode carregar arquivos nele. Esta seção orienta o carregamento de um contêiner de blob tooa arquivo local. etapas de saudação supõem que você criou um contêiner de blob denominado *contêiner de blob de teste*. 

> [!NOTE]
> 
> Olá código nesta seção pressupõe que você concluiu as etapas de saudação na seção hello, [configurar o ambiente de desenvolvimento Olá](#set-up-the-development-environment). 

1. Olá abrir `BlobsController.cs` arquivo.

1. Adicione um método chamado **UploadBlob** que retorna um **EmptyResult**.

    ```csharp
    public EmptyResult UploadBlob()
    {
        // hello code in this section goes here.

        return new EmptyResult();
    }
    ```
 
1. Dentro de saudação **UploadBlob** método, obter um **CloudStorageAccount** objeto que representa as informações da conta de armazenamento. Tooget Olá conta de armazenamento conexão cadeia de caracteres e o armazenamento de informações de configuração de serviço do Azure Olá de código a seguir de saudação de uso: (alteração  *&lt;nome da conta de armazenamento >* toohello nome da saudação armazenamento do Azure conta que você está acessando.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. Obtenha um objeto **CloudBlobClient** que representa um cliente do serviço de blob.
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. Obter um **CloudBlobContainer** objeto que representa um nome de contêiner de blob de toohello de referência. 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. Conforme explicado anteriormente, o Armazenamento do Azure oferece suporte a tipos diferentes de blob. tooretrieve um blob de páginas de tooa de referência, chamada hello **CloudBlobContainer.GetPageBlobReference** método. tooretrieve um blob de blocos de tooa de referência, chamada hello **CloudBlobContainer.GetBlockBlobReference** método. Geralmente, o blob de blocos é Olá recomendado toouse de tipo. (Alteração de < nome do blob > * toohello nome você deseja que o blob de saudação toogive carregado uma vez.)

    ```csharp
    CloudBlockBlob blob = container.GetBlockBlobReference(<blob-name>);
    ```

1. Quando você tem uma referência de blob, você pode carregar qualquer tooit de fluxo de dados por meio da chamada do objeto de referência do blob Olá **UploadFromStream** método. Olá **UploadFromStream** método cria blob Olá se ele não existe ou substitui-lo se ele existir. (Alterar  *&lt;carregamento do arquivo >* tooa totalmente qualificado caminho toohello arquivo desejado tooupload.)

    ```csharp
    using (var fileStream = System.IO.File.OpenRead(<file-to-upload>))
    {
        blob.UploadFromStream(fileStream);
    }
    ```

1. Em hello **Solution Explorer**, expanda Olá **exibições** pasta, com o botão direito **Blobs**e no menu de contexto hello, selecione **Adicionar -> exibição**.

1. Em Olá **Solution Explorer**, expanda Olá **exibições -> compartilhado** pasta e abra `_Layout.cshtml`.

1. Depois de saudação última **ActionLink**, adicione o seguinte de saudação **ActionLink**:

    ```html
    <li>@Html.ActionLink("Upload blob", "UploadBlob", "Blobs")</li>
    ```

1. Execute o aplicativo hello e selecione **carregar blob**.  
  
Olá seção - [lista Olá blobs em um contêiner de blob](#list-the-blobs-in-a-blob-container) -ilustra como Olá toolist blobs em um contêiner de blob.  

## <a name="list-hello-blobs-in-a-blob-container"></a>Saudação de listar blobs em um contêiner de blob

Esta seção ilustra como Olá toolist blobs em um contêiner de blob. código de exemplo Hello referencia Olá *contêiner de blob de teste* criado na seção hello, [criar um contêiner de blob](#create-a-blob-container).

> [!NOTE]
> 
> Olá código nesta seção pressupõe que você concluiu as etapas de saudação na seção hello, [configurar o ambiente de desenvolvimento Olá](#set-up-the-development-environment). 

1. Olá abrir `BlobsController.cs` arquivo.

1. Adicione um método chamado **ListBlobs** que retorna um **ActionResult**.

    ```csharp
    public ActionResult ListBlobs()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. Dentro de saudação **ListBlobs** método, obter um **CloudStorageAccount** objeto que representa as informações da conta de armazenamento. Tooget Olá conta de armazenamento conexão cadeia de caracteres e o armazenamento de informações de configuração de serviço do Azure Olá de código a seguir de saudação de uso: (alteração  *&lt;nome da conta de armazenamento >* toohello nome da saudação armazenamento do Azure conta que você está acessando.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. Obtenha um objeto **CloudBlobClient** que representa um cliente do serviço de blob.
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. Obter um **CloudBlobContainer** objeto que representa um nome de contêiner de blob de toohello de referência. 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. blobs de saudação toolist em um contêiner de blob, use Olá **Cloudblobcontainer** método. Olá **Cloudblobcontainer** método retorna um **IListBlobItem** do objeto que você converta tooa **CloudBlockBlob**, **CloudPageBlob**, ou **CloudBlobDirectory** objeto. Olá trecho de código a seguir enumera todos os blobs de saudação em um contêiner de blob. Cada blob é toohello converter objeto apropriado com base no seu tipo e seu nome (ou URI no caso de saudação de um **CloudBlobDirectory**) é adicionado tooa lista.

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

    Em adição tooblobs, contêineres de blob podem conter diretórios. Vamos supor que você tem um contêiner de blob chamado *contêiner de blob de teste* com hello hierarquia a seguir:

        foo.png
        dir1/bar.png
        dir2/baz.png

    Usando Olá precede o exemplo de código, Olá **blobs** lista de cadeia de caracteres contém a seguir toohello semelhante valores:

        foo.png
        <storage-account-url>/test-blob-container/dir1
        <storage-account-url>/test-blob-container/dir2

    Como você pode ver, lista de saudação inclui somente Olá nível superior entidades; Olá não aninhado aqueles (*bar.png* e *baz.png*). toolist todos Olá entidades dentro de um contêiner de blob, você deve chamar hello **Cloudblobcontainer** método e passe **true** para Olá **useFlatBlobListing** parâmetro.    

    ```csharp
    ...
    foreach (IListBlobItem item in container.ListBlobs(useFlatBlobListing:true))
    ...
    ```

    Saudação de configuração **useFlatBlobListing** parâmetro muito**true** retorna uma lista simples de todas as entidades no contêiner de blob hello e produz Olá resultados a seguir:

        foo.png
        dir1/bar.png
        dir2/baz.png

1. Em hello **Solution Explorer**, expanda Olá **exibições** pasta, com o botão direito **Blobs**e no menu de contexto hello, selecione **Adicionar -> exibição**.

1. Em Olá **adicionar exibição** caixa de diálogo, digite **ListBlobs** para o nome de exibição hello e selecione **adicionar**.

1. Abra `ListBlobs.cshtml`e modifique-o para que ele se parece com hello trecho de código a seguir:

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

1. Em Olá **Solution Explorer**, expanda Olá **exibições -> compartilhado** pasta e abra `_Layout.cshtml`.

1. Depois de saudação última **ActionLink**, adicione o seguinte de saudação **ActionLink**:

    ```html
    <li>@Html.ActionLink("List blobs", "ListBlobs", "Blobs")</li>
    ```

1. Execute o aplicativo hello e selecione **listar blobs** toosee resultados semelhante toohello captura de tela a seguir:
  
    ![Listagem de blobs](./media/vs-storage-aspnet-getting-started-blobs/listblobs.png)

## <a name="download-blobs"></a>Baixar blobs

Esta seção ilustra como toodownload um blob e a mantê-lo toolocal conteúdo de saudação de armazenamento ou de leitura em uma cadeia de caracteres. código de exemplo Hello referencia Olá *contêiner de blob de teste* criado na seção hello, [criar um contêiner de blob](#create-a-blob-container).

1. Olá abrir `BlobsController.cs` arquivo.

1. Adicione um método chamado **DownloadBlob** que retorna um **ActionResult**.

    ```csharp
    public EmptyResult DownloadBlob()
    {
        // hello code in this section goes here.

        return new EmptyResult();
    }
    ```
 
1. Dentro de saudação **DownloadBlob** método, obter um **CloudStorageAccount** objeto que representa as informações da conta de armazenamento. Tooget Olá conta de armazenamento conexão cadeia de caracteres e o armazenamento de informações de configuração de serviço do Azure Olá de código a seguir de saudação de uso: (alteração  *&lt;nome da conta de armazenamento >* toohello nome da saudação armazenamento do Azure conta que você está acessando.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. Obtenha um objeto **CloudBlobClient** que representa um cliente do serviço de blob.
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. Obter um **CloudBlobContainer** objeto que representa um nome de contêiner de blob de toohello de referência. 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. Obtém um objeto de referência de blob chamando o método **CloudBlobContainer.GetBlockBlobReference** ou **CloudBlobContainer.GetPageBlobReference**. (Alterar  *&lt;nome do blob >* toohello nome de blob Olá baixar.)

    ```csharp
    CloudBlockBlob blob = container.GetBlockBlobReference(<blob-name>);
    ```

1. toodownload um blob, use Olá **CloudBlockBlob.DownloadToStream** ou **CloudPageBlob.DownloadToStream** método, dependendo do tipo de blob hello. trecho de código a seguir Hello usa Olá **CloudBlockBlob.DownloadToStream** método tootransfer objeto de fluxo de tooa de conteúdo do blob que é então persistidos arquivo local tooa: (alteração  *&lt;nome de arquivo local >* toohello totalmente qualificado arquivo nome que representa onde você deseja que o blob Olá baixado.) 

    ```csharp
    using (var fileStream = System.IO.File.OpenWrite(<local-file-name>))
    {
        blob.DownloadToStream(fileStream);
    }
    ```

1. Em Olá **Solution Explorer**, expanda Olá **exibições -> compartilhado** pasta e abra `_Layout.cshtml`.

1. Depois de saudação última **ActionLink**, adicione o seguinte de saudação **ActionLink**:

    ```html
    <li>@Html.ActionLink("Download blob", "DownloadBlob", "Blobs")</li>
    ```

1. Execute o aplicativo hello e selecione **Download blob** blob de saudação toodownload. blob de saudação especificado no hello **CloudBlobContainer.GetBlockBlobReference** chamada de método downloads toohello local especificado no hello **File.OpenWrite** chamada de método. 

## <a name="delete-blobs"></a>Excluir blobs

Olá etapas a seguir ilustram como toodelete um blob:

> [!NOTE]
> 
> Olá código nesta seção pressupõe que você concluiu as etapas de saudação na seção hello, [configurar o ambiente de desenvolvimento Olá](#set-up-the-development-environment). 

1. Olá abrir `BlobsController.cs` arquivo.

1. Adicione um método chamado **DeleteBlob** que retorna um **ActionResult**.

    ```csharp
    public EmptyResult DeleteBlob()
    {
        // hello code in this section goes here.

        return new EmptyResult();
    }
    ```

1. Obtenha um objeto **CloudStorageAccount** que represente as informações da conta de armazenamento. Tooget Olá conta de armazenamento conexão cadeia de caracteres e o armazenamento de informações de configuração de serviço do Azure Olá de código a seguir de saudação de uso: (alteração  *&lt;nome da conta de armazenamento >* toohello nome da saudação armazenamento do Azure conta que você está acessando.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. Obtenha um objeto **CloudBlobClient** que representa um cliente do serviço de blob.
   
    ```csharp
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. Obter um **CloudBlobContainer** objeto que representa um nome de contêiner de blob de toohello de referência. 
   
    ```csharp
    CloudBlobContainer container = blobClient.GetContainerReference("test-blob-container");
    ```

1. Obtém um objeto de referência de blob chamando o método **CloudBlobContainer.GetBlockBlobReference** ou **CloudBlobContainer.GetPageBlobReference**. (Alterar  *&lt;nome do blob >* toohello nome de blob Olá você está excluindo.)

    ```csharp
    CloudBlockBlob blob = container.GetBlockBlobReference(<blob-name>);
        ```

1. toodelete a blob, use hello **Delete** method.

    ```csharp
    blob.Delete();
    ```

1. Em Olá **Solution Explorer**, expanda Olá **exibições -> compartilhado** pasta e abra `_Layout.cshtml`.

1. Depois de saudação última **ActionLink**, adicione o seguinte de saudação **ActionLink**:

    ```html
    <li>@Html.ActionLink("Delete blob", "DeleteBlob", "Blobs")</li>
    ```

1. Execute o aplicativo hello e selecione **excluir blob** toodelete blob de saudação especificado no hello **CloudBlobContainer.GetBlockBlobReference** chamada de método. 

## <a name="next-steps"></a>Próximas etapas
Exiba toolearn de guias de recurso mais sobre opções adicionais para armazenar dados no Azure.

  * [Introdução ao Armazenamento de Tabelas do Azure e aos Serviços Conectados do Visual Studio (ASP.NET)](vs-storage-aspnet-getting-started-tables.md)
  * [Introdução ao Armazenamento de Filas do Azure e aos Serviços Conectados do Visual Studio (ASP.NET)](vs-storage-aspnet-getting-started-queues.md)
