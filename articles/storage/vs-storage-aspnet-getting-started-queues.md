---
title: "aaaGet de Introdução ao armazenamento de fila do Azure e o Visual Studio conectado serviços (ASP.NET) | Microsoft Docs"
description: Como tooget iniciado usando o armazenamento de fila do Azure em um projeto do ASP.NET no Visual Studio depois de se conectar a conta de armazenamento tooa usando o Visual Studio conectado Services
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: 94ca3413-5497-433f-abbe-836f83a9de72
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/23/2016
ms.author: tarcher
ms.openlocfilehash: a9d6ecb1e8d61d75f59658d0ea3fa63d26fd7354
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-queue-storage-and-visual-studio-connected-services-aspnet"></a><span data-ttu-id="dd0e3-103">Introdução ao Armazenamento de Filas do Azure e aos Serviços Conectados do Visual Studio (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="dd0e3-103">Get started with Azure queue storage and Visual Studio Connected Services (ASP.NET)</span></span>
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="dd0e3-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="dd0e3-104">Overview</span></span>

<span data-ttu-id="dd0e3-105">O Armazenamento de Filas do Azure fornece mensagens na nuvem entre os componentes do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="dd0e3-105">Azure queue storage provides cloud messaging between application components.</span></span> <span data-ttu-id="dd0e3-106">Na criação de aplicativos para escala, os componentes do aplicativo geralmente são desassociados, para que possam ser redimensionados independentemente.</span><span class="sxs-lookup"><span data-stu-id="dd0e3-106">In designing applications for scale, application components are often decoupled, so that they can scale independently.</span></span> <span data-ttu-id="dd0e3-107">Armazenamento de fila fornece mensagens assíncronas para a comunicação entre componentes de aplicativos, quer eles estejam em execução na nuvem hello, na área de trabalho hello, em um servidor local ou em um dispositivo móvel.</span><span class="sxs-lookup"><span data-stu-id="dd0e3-107">Queue storage delivers asynchronous messaging for communication between application components, whether they are running in hello cloud, on hello desktop, on an on-premises server, or on a mobile device.</span></span> <span data-ttu-id="dd0e3-108">O armazenamento de Fila também dá suporte ao gerenciamento de tarefas assíncronas e à criação de fluxos de trabalho do processo.</span><span class="sxs-lookup"><span data-stu-id="dd0e3-108">Queue storage also supports managing asynchronous tasks and building process work flows.</span></span>

<span data-ttu-id="dd0e3-109">Este tutorial mostra como toowrite ASP.NET de código para alguns cenários comuns de uso de entidades de armazenamento de fila do Azure.</span><span class="sxs-lookup"><span data-stu-id="dd0e3-109">This tutorial shows how toowrite ASP.NET code for some common scenarios using Azure queue storage entities.</span></span> <span data-ttu-id="dd0e3-110">Esses cenários incluem tarefas comuns como criar uma fila do Azure e adicionar, modificar, ler e remover mensagens da fila.</span><span class="sxs-lookup"><span data-stu-id="dd0e3-110">These scenarios include common tasks such as creating an Azure queue, and adding, modifying, reading, and removing queue messages.</span></span>

##<a name="prerequisites"></a><span data-ttu-id="dd0e3-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="dd0e3-111">Prerequisites</span></span>

* [<span data-ttu-id="dd0e3-112">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="dd0e3-112">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="dd0e3-113">Conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="dd0e3-113">Azure storage account</span></span>](storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/vs-storage-aspnet-getting-started-create-azure-account.md)]

[!INCLUDE [storage-development-environment-include](../../includes/vs-storage-aspnet-getting-started-setup-dev-env.md)]

### <a name="create-an-mvc-controller"></a><span data-ttu-id="dd0e3-114">Criar um controlador MVC</span><span class="sxs-lookup"><span data-stu-id="dd0e3-114">Create an MVC controller</span></span> 

1. <span data-ttu-id="dd0e3-115">Em Olá **Gerenciador de soluções**, clique com botão direito **controladores**e, no menu de contexto hello, selecione **Adicionar -> controlador**.</span><span class="sxs-lookup"><span data-stu-id="dd0e3-115">In hello **Solution Explorer**, right-click **Controllers**, and, from hello context menu, select **Add->Controller**.</span></span>

    ![Adicionar um controlador tooan aplicativo ASP.NET MVC](./media/vs-storage-aspnet-getting-started-queues/add-controller-menu.png)

1. <span data-ttu-id="dd0e3-117">Em Olá **adicionar Scaffold** caixa de diálogo, selecione **controlador MVC 5 - vazio**e selecione **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="dd0e3-117">On hello **Add Scaffold** dialog, select **MVC 5 Controller - Empty**, and select **Add**.</span></span>

    ![Especificar o tipo de controlador MVC](./media/vs-storage-aspnet-getting-started-queues/add-controller.png)

1. <span data-ttu-id="dd0e3-119">Em Olá **Adicionar controlador** caixa de diálogo, o nome de controlador de saudação *QueuesController*e selecione **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="dd0e3-119">On hello **Add Controller** dialog, name hello controller *QueuesController*, and select **Add**.</span></span>

    ![Controlador MVC Olá nome](./media/vs-storage-aspnet-getting-started-queues/add-controller-name.png)

1. <span data-ttu-id="dd0e3-121">Adicione o seguinte Olá *usando* diretivas toohello `QueuesController.cs` arquivo:</span><span class="sxs-lookup"><span data-stu-id="dd0e3-121">Add hello following *using* directives toohello `QueuesController.cs` file:</span></span>

    ```csharp
    using Microsoft.Azure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Auth;
    using Microsoft.WindowsAzure.Storage.Queue;
    ```
## <a name="create-a-queue"></a><span data-ttu-id="dd0e3-122">Criar uma fila</span><span class="sxs-lookup"><span data-stu-id="dd0e3-122">Create a queue</span></span>

<span data-ttu-id="dd0e3-123">Olá etapas a seguir ilustram como toocreate uma fila:</span><span class="sxs-lookup"><span data-stu-id="dd0e3-123">hello following steps illustrate how toocreate a queue:</span></span>

> [!NOTE]
> 
> <span data-ttu-id="dd0e3-124">Esta seção pressupõe que você concluiu as etapas de saudação [configurar o ambiente de desenvolvimento Olá](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="dd0e3-124">This section assumes you have completed hello steps [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="dd0e3-125">Olá abrir `QueuesController.cs` arquivo.</span><span class="sxs-lookup"><span data-stu-id="dd0e3-125">Open hello `QueuesController.cs` file.</span></span> 

1. <span data-ttu-id="dd0e3-126">Adicione um método chamado **CreateQueue** que retorna um **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="dd0e3-126">Add a method called **CreateQueue** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult CreateQueue()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="dd0e3-127">Dentro de saudação **CreateQueue** método, obter um **CloudStorageAccount** objeto que representa as informações da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="dd0e3-127">Within hello **CreateQueue** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="dd0e3-128">Tooget Olá conta de armazenamento conexão cadeia de caracteres e o armazenamento de informações de configuração de serviço do Azure Olá de código a seguir de saudação de uso: (alteração  *&lt;nome da conta de armazenamento >* toohello nome da saudação armazenamento do Azure conta que você está acessando.)</span><span class="sxs-lookup"><span data-stu-id="dd0e3-128">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="dd0e3-129">Obtenha um objeto **CloudQueueClient** que representa um cliente do serviço de fila.</span><span class="sxs-lookup"><span data-stu-id="dd0e3-129">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```
1. <span data-ttu-id="dd0e3-130">Obter um **CloudQueue** objeto que representa um nome de fila desejada de toohello de referência.</span><span class="sxs-lookup"><span data-stu-id="dd0e3-130">Get a **CloudQueue** object that represents a reference toohello desired queue name.</span></span> <span data-ttu-id="dd0e3-131">Olá **CloudQueueClient.GetQueueReference** método não faz uma solicitação em relação ao armazenamento de fila.</span><span class="sxs-lookup"><span data-stu-id="dd0e3-131">hello **CloudQueueClient.GetQueueReference** method does not make a request against queue storage.</span></span> <span data-ttu-id="dd0e3-132">referência de saudação é retornada se Olá fila existe ou não.</span><span class="sxs-lookup"><span data-stu-id="dd0e3-132">hello reference is returned whether or not hello queue exists.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="dd0e3-133">Chamar hello **CloudQueue.CreateIfNotExists** fila de saudação do método toocreate se ele ainda não existir.</span><span class="sxs-lookup"><span data-stu-id="dd0e3-133">Call hello **CloudQueue.CreateIfNotExists** method toocreate hello queue if it does not yet exist.</span></span> <span data-ttu-id="dd0e3-134">Olá **CloudQueue.CreateIfNotExists** método **true** se Olá fila não existe e foi criada com êxito.</span><span class="sxs-lookup"><span data-stu-id="dd0e3-134">hello **CloudQueue.CreateIfNotExists** method returns **true** if hello queue does not exist, and is successfully created.</span></span> <span data-ttu-id="dd0e3-135">Caso contrário, **false** será retornado.</span><span class="sxs-lookup"><span data-stu-id="dd0e3-135">Otherwise, **false** is returned.</span></span>    

    ```csharp
    ViewBag.Success = queue.CreateIfNotExists();
    ```

1. <span data-ttu-id="dd0e3-136">Saudação de atualização **ViewBag** com o nome de saudação da fila de saudação.</span><span class="sxs-lookup"><span data-stu-id="dd0e3-136">Update hello **ViewBag** with hello name of hello queue.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ```

1. <span data-ttu-id="dd0e3-137">Em Olá **Gerenciador de soluções**, expanda Olá **exibições** pasta, com o botão direito **filas**e no menu de contexto hello, selecione **Adicionar -> exibição**.</span><span class="sxs-lookup"><span data-stu-id="dd0e3-137">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Queues**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="dd0e3-138">Em Olá **adicionar exibição** caixa de diálogo, digite **CreateQueue** para o nome de exibição hello e selecione **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="dd0e3-138">On hello **Add View** dialog, enter **CreateQueue** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="dd0e3-139">Abra `CreateQueue.cshtml`e modifique-o para que ele se parece com hello trecho de código a seguir:</span><span class="sxs-lookup"><span data-stu-id="dd0e3-139">Open `CreateQueue.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Create Queue";
    }
    
    <h2>Create Queue results</h2>

    Creation of @ViewBag.QueueName @(ViewBag.Success == true ? "succeeded" : "failed")
    ```

1. <span data-ttu-id="dd0e3-140">Em Olá **Solution Explorer**, expanda Olá **exibições -> compartilhado** pasta e abra `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="dd0e3-140">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="dd0e3-141">Depois de saudação última **ActionLink**, adicione o seguinte de saudação **ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="dd0e3-141">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Create queue", "CreateQueue", "Queues")</li>
    ```

1. <span data-ttu-id="dd0e3-142">Execute o aplicativo hello e selecione **criar fila** toosee resultados semelhante toohello captura de tela a seguir:</span><span class="sxs-lookup"><span data-stu-id="dd0e3-142">Run hello application, and select **Create queue** toosee results similar toohello following screen shot:</span></span>
  
    ![Criar fila](./media/vs-storage-aspnet-getting-started-queues/create-queue-results.png)

    <span data-ttu-id="dd0e3-144">Conforme mencionado anteriormente, Olá **CloudQueue.CreateIfNotExists** método **true** somente quando a fila de saudação não existe e é criada.</span><span class="sxs-lookup"><span data-stu-id="dd0e3-144">As mentioned previously, hello **CloudQueue.CreateIfNotExists** method returns **true** only when hello queue doesn't exist and is created.</span></span> <span data-ttu-id="dd0e3-145">Portanto, se você executar o aplicativo hello quando Olá fila existe, método hello retorna **false**.</span><span class="sxs-lookup"><span data-stu-id="dd0e3-145">Therefore, if you run hello app when hello queue exists, hello method returns **false**.</span></span> <span data-ttu-id="dd0e3-146">toorun Olá aplicativo várias vezes, você deve excluir Olá fila antes de executar o aplicativo hello novamente.</span><span class="sxs-lookup"><span data-stu-id="dd0e3-146">toorun hello app multiple times, you must delete hello queue before running hello app again.</span></span> <span data-ttu-id="dd0e3-147">Excluindo fila de saudação pode ser feita por meio de saudação **CloudQueue.Delete** método.</span><span class="sxs-lookup"><span data-stu-id="dd0e3-147">Deleting hello queue can be done via hello **CloudQueue.Delete** method.</span></span> <span data-ttu-id="dd0e3-148">Você também pode excluir a fila de saudação usando Olá [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040) ou hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="dd0e3-148">You can also delete hello queue using hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) or hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span></span>  

## <a name="add-a-message-tooa-queue"></a><span data-ttu-id="dd0e3-149">Adicionar uma fila de mensagens tooa</span><span class="sxs-lookup"><span data-stu-id="dd0e3-149">Add a message tooa queue</span></span>

<span data-ttu-id="dd0e3-150">Depois que você [criar uma fila](#create-a-queue), você pode adicionar a fila de mensagens de toothat.</span><span class="sxs-lookup"><span data-stu-id="dd0e3-150">Once you've [created a queue](#create-a-queue), you can add messages toothat queue.</span></span> <span data-ttu-id="dd0e3-151">Esta seção orienta você através de uma fila de mensagens tooa *testar fila*.</span><span class="sxs-lookup"><span data-stu-id="dd0e3-151">This section walks you through adding a message tooa queue *test-queue*.</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="dd0e3-152">Esta seção pressupõe que você concluiu as etapas de saudação [configurar o ambiente de desenvolvimento Olá](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="dd0e3-152">This section assumes you have completed hello steps [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="dd0e3-153">Olá abrir `QueuesController.cs` arquivo.</span><span class="sxs-lookup"><span data-stu-id="dd0e3-153">Open hello `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="dd0e3-154">Adicione um método chamado **AddMessage** que retorna um **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="dd0e3-154">Add a method called **AddMessage** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult AddMessage()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="dd0e3-155">Dentro de saudação **AddMessage** método, obter um **CloudStorageAccount** objeto que representa as informações da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="dd0e3-155">Within hello **AddMessage** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="dd0e3-156">Tooget Olá conta de armazenamento conexão cadeia de caracteres e o armazenamento de informações de configuração de serviço do Azure Olá de código a seguir de saudação de uso: (alteração  *&lt;nome da conta de armazenamento >* toohello nome da saudação armazenamento do Azure conta que você está acessando.)</span><span class="sxs-lookup"><span data-stu-id="dd0e3-156">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="dd0e3-157">Obtenha um objeto **CloudQueueClient** que representa um cliente do serviço de fila.</span><span class="sxs-lookup"><span data-stu-id="dd0e3-157">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="dd0e3-158">Obter um **CloudQueueContainer** objeto que representa uma fila de toohello de referência.</span><span class="sxs-lookup"><span data-stu-id="dd0e3-158">Get a **CloudQueueContainer** object that represents a reference toohello queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="dd0e3-159">Criar hello **CloudQueueMessage** objeto que representa a mensagem de saudação quiser tooadd toohello fila.</span><span class="sxs-lookup"><span data-stu-id="dd0e3-159">Create hello **CloudQueueMessage** object representing hello message you want tooadd toohello queue.</span></span> <span data-ttu-id="dd0e3-160">Um objeto **CloudQueueMessage** pode ser criado por meio de uma cadeia de caracteres (em formato UTF-8) ou de uma matriz de bytes.</span><span class="sxs-lookup"><span data-stu-id="dd0e3-160">A **CloudQueueMessage** object can be created from either a string (in UTF-8 format) or a byte array.</span></span>

    ```csharp
    CloudQueueMessage message = new CloudQueueMessage("Hello, Azure Queue Storage");
    ```

1. <span data-ttu-id="dd0e3-161">Chamar hello **CloudQueue.AddMessage** fila de toohello mensagem de saudação do método tooadd.</span><span class="sxs-lookup"><span data-stu-id="dd0e3-161">Call hello **CloudQueue.AddMessage** method tooadd hello messaged toohello queue.</span></span>

    ```csharp
    queue.AddMessage(message);
    ```

1. <span data-ttu-id="dd0e3-162">Crie e defina alguns **ViewBag** propriedades para exibição no modo de exibição de saudação.</span><span class="sxs-lookup"><span data-stu-id="dd0e3-162">Create and set a couple of **ViewBag** properties for display in hello view.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Message = message.AsString;
    ```

1. <span data-ttu-id="dd0e3-163">Em Olá **Gerenciador de soluções**, expanda Olá **exibições** pasta, com o botão direito **filas**e no menu de contexto hello, selecione **Adicionar -> exibição**.</span><span class="sxs-lookup"><span data-stu-id="dd0e3-163">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Queues**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="dd0e3-164">Em Olá **adicionar exibição** caixa de diálogo, digite **AddMessage** para o nome de exibição hello e selecione **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="dd0e3-164">On hello **Add View** dialog, enter **AddMessage** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="dd0e3-165">Abra `AddMessage.cshtml`e modifique-o para que ele se parece com hello trecho de código a seguir:</span><span class="sxs-lookup"><span data-stu-id="dd0e3-165">Open `AddMessage.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Add Message";
    }
    
    <h2>Add Message results</h2>
    
    hello message '@ViewBag.Message' was added toohello queue '@ViewBag.QueueName'.
    ```

1. <span data-ttu-id="dd0e3-166">Em Olá **Solution Explorer**, expanda Olá **exibições -> compartilhado** pasta e abra `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="dd0e3-166">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="dd0e3-167">Depois de saudação última **ActionLink**, adicione o seguinte de saudação **ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="dd0e3-167">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Add message", "AddMessage", "Queues")</li>
    ```

1. <span data-ttu-id="dd0e3-168">Execute o aplicativo hello e selecione **Adicionar mensagem** toosee resultados semelhante toohello captura de tela a seguir:</span><span class="sxs-lookup"><span data-stu-id="dd0e3-168">Run hello application, and select **Add message** toosee results similar toohello following screen shot:</span></span>
  
    ![Adicionar mensagem](./media/vs-storage-aspnet-getting-started-queues/add-message-results.png)

<span data-ttu-id="dd0e3-170">Olá duas seções - [ler uma mensagem de uma fila sem removê-lo](#read-a-message-from-a-queue-without-removing-it) e [leitura e remover uma mensagem de uma fila](#read-and-remove-a-message-from-a-queue) -ilustram como tooread mensagens de uma fila.</span><span class="sxs-lookup"><span data-stu-id="dd0e3-170">hello two sections - [Read a message from a queue without removing it](#read-a-message-from-a-queue-without-removing-it) and [Read and remove a message from a queue](#read-and-remove-a-message-from-a-queue) - illustrate how tooread messages from a queue.</span></span>  

## <a name="read-a-message-from-a-queue-without-removing-it"></a><span data-ttu-id="dd0e3-171">Ler uma mensagem de uma fila sem removê-la</span><span class="sxs-lookup"><span data-stu-id="dd0e3-171">Read a message from a queue without removing it</span></span>

<span data-ttu-id="dd0e3-172">Esta seção ilustra como toopeek em uma mensagem na fila (leitura Olá primeira mensagem sem removê-lo).</span><span class="sxs-lookup"><span data-stu-id="dd0e3-172">This section illustrates how toopeek at a queued message (read hello first message without removing it).</span></span>  

> [!NOTE]
> 
> <span data-ttu-id="dd0e3-173">Esta seção pressupõe que você concluiu as etapas de saudação [configurar o ambiente de desenvolvimento Olá](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="dd0e3-173">This section assumes you have completed hello steps [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="dd0e3-174">Olá abrir `QueuesController.cs` arquivo.</span><span class="sxs-lookup"><span data-stu-id="dd0e3-174">Open hello `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="dd0e3-175">Adicione um método chamado **PeekMessage** que retorna um **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="dd0e3-175">Add a method called **PeekMessage** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult PeekMessage()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="dd0e3-176">Dentro de saudação **PeekMessage** método, obter um **CloudStorageAccount** objeto que representa as informações da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="dd0e3-176">Within hello **PeekMessage** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="dd0e3-177">Tooget Olá conta de armazenamento conexão cadeia de caracteres e o armazenamento de informações de configuração de serviço do Azure Olá de código a seguir de saudação de uso: (alteração  *&lt;nome da conta de armazenamento >* toohello nome da saudação armazenamento do Azure conta que você está acessando.)</span><span class="sxs-lookup"><span data-stu-id="dd0e3-177">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="dd0e3-178">Obtenha um objeto **CloudQueueClient** que representa um cliente do serviço de fila.</span><span class="sxs-lookup"><span data-stu-id="dd0e3-178">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="dd0e3-179">Obter um **CloudQueueContainer** objeto que representa uma fila de toohello de referência.</span><span class="sxs-lookup"><span data-stu-id="dd0e3-179">Get a **CloudQueueContainer** object that represents a reference toohello queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="dd0e3-180">Chamar hello **CloudQueue.PeekMessage** método tooread Olá primeira mensagem na fila de saudação sem removê-la da fila de saudação.</span><span class="sxs-lookup"><span data-stu-id="dd0e3-180">Call hello **CloudQueue.PeekMessage** method tooread hello first message in hello queue without removing it from hello queue.</span></span> 

    ```csharp
    CloudQueueMessage message = queue.PeekMessage();
    ```

1. <span data-ttu-id="dd0e3-181">Saudação de atualização **ViewBag** com dois valores: nome da fila hello e uma mensagem de saudação que foi lido.</span><span class="sxs-lookup"><span data-stu-id="dd0e3-181">Update hello **ViewBag** with two values: hello queue name and hello message that was read.</span></span> <span data-ttu-id="dd0e3-182">Olá **CloudQueueMessage** objeto expõe duas propriedades para obter o valor do objeto Olá: **CloudQueueMessage.AsBytes** e **CloudQueueMessage.AsString**.</span><span class="sxs-lookup"><span data-stu-id="dd0e3-182">hello **CloudQueueMessage** object exposes two properties for getting hello object's value: **CloudQueueMessage.AsBytes** and **CloudQueueMessage.AsString**.</span></span> <span data-ttu-id="dd0e3-183">**AsString** (usado neste exemplo) retorna uma cadeia de caracteres, enquanto **AsBytes** retorna uma matriz de bytes.</span><span class="sxs-lookup"><span data-stu-id="dd0e3-183">**AsString** (used in this example) returns a string, while **AsBytes** returns a byte array.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name; 
    ViewBag.Message = (message != null ? message.AsString : "");
    ```

1. <span data-ttu-id="dd0e3-184">Em Olá **Gerenciador de soluções**, expanda Olá **exibições** pasta, com o botão direito **filas**e no menu de contexto hello, selecione **Adicionar -> exibição**.</span><span class="sxs-lookup"><span data-stu-id="dd0e3-184">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Queues**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="dd0e3-185">Em Olá **adicionar exibição** caixa de diálogo, digite **PeekMessage** para o nome de exibição hello e selecione **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="dd0e3-185">On hello **Add View** dialog, enter **PeekMessage** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="dd0e3-186">Abra `PeekMessage.cshtml`e modifique-o para que ele se parece com hello trecho de código a seguir:</span><span class="sxs-lookup"><span data-stu-id="dd0e3-186">Open `PeekMessage.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "PeekMessage";
    }
    
    <h2>Peek Message results</h2>
    
    <table border="1">
        <tr><th>Queue</th><th>Peeked Message</th></tr>
        <tr><td>@ViewBag.QueueName</td><td>@ViewBag.Message</td></tr>
    </table>    
    ```

1. <span data-ttu-id="dd0e3-187">Em Olá **Solution Explorer**, expanda Olá **exibições -> compartilhado** pasta e abra `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="dd0e3-187">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="dd0e3-188">Depois de saudação última **ActionLink**, adicione o seguinte de saudação **ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="dd0e3-188">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Peek message", "PeekMessage", "Queues")</li>
    ```

1. <span data-ttu-id="dd0e3-189">Execute o aplicativo hello e selecione **inspecionar mensagem** toosee resultados semelhante toohello captura de tela a seguir:</span><span class="sxs-lookup"><span data-stu-id="dd0e3-189">Run hello application, and select **Peek message** toosee results similar toohello following screen shot:</span></span>
  
    ![Espiar mensagem](./media/vs-storage-aspnet-getting-started-queues/peek-message-results.png)

## <a name="read-and-remove-a-message-from-a-queue"></a><span data-ttu-id="dd0e3-191">Ler e remover uma mensagem de uma fila</span><span class="sxs-lookup"><span data-stu-id="dd0e3-191">Read and remove a message from a queue</span></span>

<span data-ttu-id="dd0e3-192">Nesta seção, você aprenderá como tooread e remover uma mensagem de uma fila.</span><span class="sxs-lookup"><span data-stu-id="dd0e3-192">In this section, you learn how tooread and remove a message from a queue.</span></span>   

> [!NOTE]
> 
> <span data-ttu-id="dd0e3-193">Esta seção pressupõe que você concluiu as etapas de saudação [configurar o ambiente de desenvolvimento Olá](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="dd0e3-193">This section assumes you have completed hello steps [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="dd0e3-194">Olá abrir `QueuesController.cs` arquivo.</span><span class="sxs-lookup"><span data-stu-id="dd0e3-194">Open hello `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="dd0e3-195">Adicione um método chamado **ReadMessage** que retorna um **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="dd0e3-195">Add a method called **ReadMessage** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult ReadMessage()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="dd0e3-196">Dentro de saudação **ReadMessage** método, obter um **CloudStorageAccount** objeto que representa as informações da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="dd0e3-196">Within hello **ReadMessage** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="dd0e3-197">Tooget Olá conta de armazenamento conexão cadeia de caracteres e o armazenamento de informações de configuração de serviço do Azure Olá de código a seguir de saudação de uso: (alteração  *&lt;nome da conta de armazenamento >* toohello nome da saudação armazenamento do Azure conta que você está acessando.)</span><span class="sxs-lookup"><span data-stu-id="dd0e3-197">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="dd0e3-198">Obtenha um objeto **CloudQueueClient** que representa um cliente do serviço de fila.</span><span class="sxs-lookup"><span data-stu-id="dd0e3-198">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="dd0e3-199">Obter um **CloudQueueContainer** objeto que representa uma fila de toohello de referência.</span><span class="sxs-lookup"><span data-stu-id="dd0e3-199">Get a **CloudQueueContainer** object that represents a reference toohello queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="dd0e3-200">Chamar hello **CloudQueue.GetMessage** método tooread Olá primeira mensagem na fila de saudação.</span><span class="sxs-lookup"><span data-stu-id="dd0e3-200">Call hello **CloudQueue.GetMessage** method tooread hello first message in hello queue.</span></span> <span data-ttu-id="dd0e3-201">Olá **CloudQueue.GetMessage** método torna Olá outro código ler mensagens de forma que nenhum outro código pode modificar ou excluir a mensagem de saudação durante o processamento de mensagem invisível para tooany de 30 segundos (por padrão).</span><span class="sxs-lookup"><span data-stu-id="dd0e3-201">hello **CloudQueue.GetMessage** method makes hello message invisible for 30 seconds (by default) tooany other code reading messages so that no other code can modify or delete hello message while your processing it.</span></span> <span data-ttu-id="dd0e3-202">quantidade de saudação toochange de mensagem de saudação do tempo é invisível, modifique Olá **visibilityTimeout** parâmetro que está sendo passado toohello **CloudQueue.GetMessage** método.</span><span class="sxs-lookup"><span data-stu-id="dd0e3-202">toochange hello amount of time hello message is invisible, modify hello **visibilityTimeout** parameter being passed toohello **CloudQueue.GetMessage** method.</span></span>

    ```csharp
    // This message will be invisible tooother code for 30 seconds.
    CloudQueueMessage message = queue.GetMessage();     
    ```

1. <span data-ttu-id="dd0e3-203">Chamar hello **CloudQueueMessage.Delete** mensagem de saudação do método toodelete da fila de saudação.</span><span class="sxs-lookup"><span data-stu-id="dd0e3-203">Call hello **CloudQueueMessage.Delete** method toodelete hello message from hello queue.</span></span>

    ```csharp
    queue.DeleteMessage(message);
    ```

1. <span data-ttu-id="dd0e3-204">Saudação de atualização **ViewBag** com hello mensagem excluída e Olá nome da fila de saudação.</span><span class="sxs-lookup"><span data-stu-id="dd0e3-204">Update hello **ViewBag** with hello message deleted, and hello name of hello queue.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Message = message.AsString;
    ```
 
1. <span data-ttu-id="dd0e3-205">Em Olá **Gerenciador de soluções**, expanda Olá **exibições** pasta, com o botão direito **filas**e no menu de contexto hello, selecione **Adicionar -> exibição**.</span><span class="sxs-lookup"><span data-stu-id="dd0e3-205">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Queues**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="dd0e3-206">Em Olá **adicionar exibição** caixa de diálogo, digite **ReadMessage** para o nome de exibição hello e selecione **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="dd0e3-206">On hello **Add View** dialog, enter **ReadMessage** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="dd0e3-207">Abra `ReadMessage.cshtml`e modifique-o para que ele se parece com hello trecho de código a seguir:</span><span class="sxs-lookup"><span data-stu-id="dd0e3-207">Open `ReadMessage.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "ReadMessage";
    }
    
    <h2>Read Message results</h2>
    
    <table border="1">
        <tr><th>Queue</th><th>Read (and Deleted) Message</th></tr>
        <tr><td>@ViewBag.QueueName</td><td>@ViewBag.Message</td></tr>
    </table>
    ```

1. <span data-ttu-id="dd0e3-208">Em Olá **Solution Explorer**, expanda Olá **exibições -> compartilhado** pasta e abra `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="dd0e3-208">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="dd0e3-209">Depois de saudação última **ActionLink**, adicione o seguinte de saudação **ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="dd0e3-209">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Read/Delete message", "ReadMessage", "Queues")</li>
    ```

1. <span data-ttu-id="dd0e3-210">Execute o aplicativo hello e selecione **leitura/exclusão de mensagem** toosee resultados semelhante toohello captura de tela a seguir:</span><span class="sxs-lookup"><span data-stu-id="dd0e3-210">Run hello application, and select **Read/Delete message** toosee results similar toohello following screen shot:</span></span>
  
    ![Ler e excluir a mensagem](./media/vs-storage-aspnet-getting-started-queues/read-message-results.png)

## <a name="get-hello-queue-length"></a><span data-ttu-id="dd0e3-212">Obter o comprimento da fila de saudação</span><span class="sxs-lookup"><span data-stu-id="dd0e3-212">Get hello queue length</span></span>

<span data-ttu-id="dd0e3-213">Esta seção ilustra como tooget Olá comprimento da fila (número de mensagens).</span><span class="sxs-lookup"><span data-stu-id="dd0e3-213">This section illustrates how tooget hello queue length (number of messages).</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="dd0e3-214">Esta seção pressupõe que você concluiu as etapas de saudação [configurar o ambiente de desenvolvimento Olá](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="dd0e3-214">This section assumes you have completed hello steps [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="dd0e3-215">Olá abrir `QueuesController.cs` arquivo.</span><span class="sxs-lookup"><span data-stu-id="dd0e3-215">Open hello `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="dd0e3-216">Adicione um método chamado **GetQueueLength** que retorna um **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="dd0e3-216">Add a method called **GetQueueLength** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult GetQueueLength()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="dd0e3-217">Dentro de saudação **ReadMessage** método, obter um **CloudStorageAccount** objeto que representa as informações da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="dd0e3-217">Within hello **ReadMessage** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="dd0e3-218">Tooget Olá conta de armazenamento conexão cadeia de caracteres e o armazenamento de informações de configuração de serviço do Azure Olá de código a seguir de saudação de uso: (alteração  *&lt;nome da conta de armazenamento >* toohello nome da saudação armazenamento do Azure conta que você está acessando.)</span><span class="sxs-lookup"><span data-stu-id="dd0e3-218">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="dd0e3-219">Obtenha um objeto **CloudQueueClient** que representa um cliente do serviço de fila.</span><span class="sxs-lookup"><span data-stu-id="dd0e3-219">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="dd0e3-220">Obter um **CloudQueueContainer** objeto que representa uma fila de toohello de referência.</span><span class="sxs-lookup"><span data-stu-id="dd0e3-220">Get a **CloudQueueContainer** object that represents a reference toohello queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="dd0e3-221">Chamar hello **CloudQueue.FetchAttributes** atributos da fila do método tooretrieve hello (incluindo seu comprimento).</span><span class="sxs-lookup"><span data-stu-id="dd0e3-221">Call hello **CloudQueue.FetchAttributes** method tooretrieve hello queue's attributes (including its length).</span></span> 

    ```csharp
    queue.FetchAttributes();
    ```

6. <span data-ttu-id="dd0e3-222">Saudação de acesso **CloudQueue.ApproximateMessageCount** comprimento da fila de saudação do tooget propriedade.</span><span class="sxs-lookup"><span data-stu-id="dd0e3-222">Access hello **CloudQueue.ApproximateMessageCount** property tooget hello queue's length.</span></span>
 
    ```csharp
    int? nMessages = queue.ApproximateMessageCount;
    ```

1. <span data-ttu-id="dd0e3-223">Saudação de atualização **ViewBag** com nome Olá Olá fila e seu tamanho.</span><span class="sxs-lookup"><span data-stu-id="dd0e3-223">Update hello **ViewBag** with hello name of hello queue, and its length.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Length = nMessages;
    ```
 
1. <span data-ttu-id="dd0e3-224">Em Olá **Gerenciador de soluções**, expanda Olá **exibições** pasta, com o botão direito **filas**e no menu de contexto hello, selecione **Adicionar -> exibição**.</span><span class="sxs-lookup"><span data-stu-id="dd0e3-224">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Queues**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="dd0e3-225">Em Olá **adicionar exibição** caixa de diálogo, digite **GetQueueLength** para o nome de exibição hello e selecione **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="dd0e3-225">On hello **Add View** dialog, enter **GetQueueLength** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="dd0e3-226">Abra `GetQueueLengthMessage.cshtml`e modifique-o para que ele se parece com hello trecho de código a seguir:</span><span class="sxs-lookup"><span data-stu-id="dd0e3-226">Open `GetQueueLengthMessage.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "GetQueueLength";
    }
    
    <h2>Get Queue Length results</h2>
    
    hello queue '@ViewBag.QueueName' has a length of (number of messages): @ViewBag.Length
    ```

1. <span data-ttu-id="dd0e3-227">Em Olá **Solution Explorer**, expanda Olá **exibições -> compartilhado** pasta e abra `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="dd0e3-227">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="dd0e3-228">Depois de saudação última **ActionLink**, adicione o seguinte de saudação **ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="dd0e3-228">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Get queue length", "GetQueueLength", "Queues")</li>
    ```

1. <span data-ttu-id="dd0e3-229">Execute o aplicativo hello e selecione **obter o comprimento da fila de** toosee resultados semelhante toohello captura de tela a seguir:</span><span class="sxs-lookup"><span data-stu-id="dd0e3-229">Run hello application, and select **Get queue length** toosee results similar toohello following screen shot:</span></span>
  
    ![Obter o tamanho da fila](./media/vs-storage-aspnet-getting-started-queues/get-queue-length-results.png)


## <a name="delete-a-queue"></a><span data-ttu-id="dd0e3-231">Excluir uma fila</span><span class="sxs-lookup"><span data-stu-id="dd0e3-231">Delete a queue</span></span>
<span data-ttu-id="dd0e3-232">Esta seção ilustra como toodelete uma fila.</span><span class="sxs-lookup"><span data-stu-id="dd0e3-232">This section illustrates how toodelete a queue.</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="dd0e3-233">Esta seção pressupõe que você concluiu as etapas de saudação [configurar o ambiente de desenvolvimento Olá](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="dd0e3-233">This section assumes you have completed hello steps [Set up hello development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="dd0e3-234">Olá abrir `QueuesController.cs` arquivo.</span><span class="sxs-lookup"><span data-stu-id="dd0e3-234">Open hello `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="dd0e3-235">Adicione um método chamado **DeleteQueue** que retorna um **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="dd0e3-235">Add a method called **DeleteQueue** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult DeleteQueue()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="dd0e3-236">Dentro de saudação **DeleteQueue** método, obter um **CloudStorageAccount** objeto que representa as informações da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="dd0e3-236">Within hello **DeleteQueue** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="dd0e3-237">Tooget Olá conta de armazenamento conexão cadeia de caracteres e o armazenamento de informações de configuração de serviço do Azure Olá de código a seguir de saudação de uso: (alteração  *&lt;nome da conta de armazenamento >* toohello nome da saudação armazenamento do Azure conta que você está acessando.)</span><span class="sxs-lookup"><span data-stu-id="dd0e3-237">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration: (Change *&lt;storage-account-name>* toohello name of hello Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="dd0e3-238">Obtenha um objeto **CloudQueueClient** que representa um cliente do serviço de fila.</span><span class="sxs-lookup"><span data-stu-id="dd0e3-238">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="dd0e3-239">Obter um **CloudQueueContainer** objeto que representa uma fila de toohello de referência.</span><span class="sxs-lookup"><span data-stu-id="dd0e3-239">Get a **CloudQueueContainer** object that represents a reference toohello queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="dd0e3-240">Chamar hello **CloudQueue.Delete** fila de saudação do método toodelete representada por Olá **CloudQueue** objeto.</span><span class="sxs-lookup"><span data-stu-id="dd0e3-240">Call hello **CloudQueue.Delete** method toodelete hello queue represented by hello **CloudQueue** object.</span></span>

    ```csharp
    queue.Delete();
    ```

1. <span data-ttu-id="dd0e3-241">Saudação de atualização **ViewBag** com nome Olá Olá fila e seu tamanho.</span><span class="sxs-lookup"><span data-stu-id="dd0e3-241">Update hello **ViewBag** with hello name of hello queue, and its length.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ```
 
1. <span data-ttu-id="dd0e3-242">Em Olá **Gerenciador de soluções**, expanda Olá **exibições** pasta, com o botão direito **filas**e no menu de contexto hello, selecione **Adicionar -> exibição**.</span><span class="sxs-lookup"><span data-stu-id="dd0e3-242">In hello **Solution Explorer**, expand hello **Views** folder, right-click **Queues**, and from hello context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="dd0e3-243">Em Olá **adicionar exibição** caixa de diálogo, digite **DeleteQueue** para o nome de exibição hello e selecione **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="dd0e3-243">On hello **Add View** dialog, enter **DeleteQueue** for hello view name, and select **Add**.</span></span>

1. <span data-ttu-id="dd0e3-244">Abra `DeleteQueue.cshtml`e modifique-o para que ele se parece com hello trecho de código a seguir:</span><span class="sxs-lookup"><span data-stu-id="dd0e3-244">Open `DeleteQueue.cshtml`, and modify it so that it looks like hello following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "DeleteQueue";
    }
    
    <h2>Delete Queue results</h2>
    
    @ViewBag.QueueName deleted.
    ```

1. <span data-ttu-id="dd0e3-245">Em Olá **Solution Explorer**, expanda Olá **exibições -> compartilhado** pasta e abra `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="dd0e3-245">In hello **Solution Explorer**, expand hello **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="dd0e3-246">Depois de saudação última **ActionLink**, adicione o seguinte de saudação **ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="dd0e3-246">After hello last **Html.ActionLink**, add hello following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Delete queue", "DeleteQueue", "Queues")</li>
    ```

1. <span data-ttu-id="dd0e3-247">Execute o aplicativo hello e selecione **obter o comprimento da fila de** toosee resultados semelhante toohello captura de tela a seguir:</span><span class="sxs-lookup"><span data-stu-id="dd0e3-247">Run hello application, and select **Get queue length** toosee results similar toohello following screen shot:</span></span>
  
    ![Excluir fila](./media/vs-storage-aspnet-getting-started-queues/delete-queue-results.png)

## <a name="next-steps"></a><span data-ttu-id="dd0e3-249">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="dd0e3-249">Next steps</span></span>
<span data-ttu-id="dd0e3-250">Exiba toolearn de guias de recurso mais sobre opções adicionais para armazenar dados no Azure.</span><span class="sxs-lookup"><span data-stu-id="dd0e3-250">View more feature guides toolearn about additional options for storing data in Azure.</span></span>

  * [<span data-ttu-id="dd0e3-251">Introdução ao Armazenamento de Blobs do Azure e aos Serviços Conectados do Visual Studio (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="dd0e3-251">Get started with Azure blob storage and Visual Studio Connected Services (ASP.NET)</span></span>](./vs-storage-aspnet-getting-started-blobs.md)
  * [<span data-ttu-id="dd0e3-252">Introdução ao Armazenamento de Tabelas do Azure e aos Serviços Conectados do Visual Studio (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="dd0e3-252">Get started with Azure table storage and Visual Studio Connected Services (ASP.NET)</span></span>](./vs-storage-aspnet-getting-started-tables.md)
