---
title: "Introdução ao Armazenamento de Filas do Azure e aos Serviços Conectados do Visual Studio (ASP.NET) | Microsoft Docs"
description: "Como começar a usar o Armazenamento de Filas do Azure em um projeto do ASP.NET no Visual Studio após a conexão a uma conta de armazenamento usando os Serviços Conectados do Visual Studio"
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
ms.openlocfilehash: 76b0d5e270e16a317ce8a7b424c06c867b537a8e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-with-azure-queue-storage-and-visual-studio-connected-services-aspnet"></a><span data-ttu-id="bbbe7-103">Introdução ao Armazenamento de Filas do Azure e aos Serviços Conectados do Visual Studio (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="bbbe7-103">Get started with Azure queue storage and Visual Studio Connected Services (ASP.NET)</span></span>
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="bbbe7-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="bbbe7-104">Overview</span></span>

<span data-ttu-id="bbbe7-105">O Armazenamento de Filas do Azure fornece mensagens na nuvem entre os componentes do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="bbbe7-105">Azure queue storage provides cloud messaging between application components.</span></span> <span data-ttu-id="bbbe7-106">Na criação de aplicativos para escala, os componentes do aplicativo geralmente são desassociados, para que possam ser redimensionados independentemente.</span><span class="sxs-lookup"><span data-stu-id="bbbe7-106">In designing applications for scale, application components are often decoupled, so that they can scale independently.</span></span> <span data-ttu-id="bbbe7-107">O armazenamento de filas fornece mensagens assíncronas para a comunicação entre os componentes do aplicativo, estando eles em execução na nuvem, na área de trabalho, em um servidor local ou em um dispositivo móvel.</span><span class="sxs-lookup"><span data-stu-id="bbbe7-107">Queue storage delivers asynchronous messaging for communication between application components, whether they are running in the cloud, on the desktop, on an on-premises server, or on a mobile device.</span></span> <span data-ttu-id="bbbe7-108">O armazenamento de Fila também dá suporte ao gerenciamento de tarefas assíncronas e à criação de fluxos de trabalho do processo.</span><span class="sxs-lookup"><span data-stu-id="bbbe7-108">Queue storage also supports managing asynchronous tasks and building process work flows.</span></span>

<span data-ttu-id="bbbe7-109">Este tutorial mostra como gravar código ASP.NET para alguns cenários comuns usando entidades do Armazenamento de Filas do Azure.</span><span class="sxs-lookup"><span data-stu-id="bbbe7-109">This tutorial shows how to write ASP.NET code for some common scenarios using Azure queue storage entities.</span></span> <span data-ttu-id="bbbe7-110">Esses cenários incluem tarefas comuns como criar uma fila do Azure e adicionar, modificar, ler e remover mensagens da fila.</span><span class="sxs-lookup"><span data-stu-id="bbbe7-110">These scenarios include common tasks such as creating an Azure queue, and adding, modifying, reading, and removing queue messages.</span></span>

##<a name="prerequisites"></a><span data-ttu-id="bbbe7-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="bbbe7-111">Prerequisites</span></span>

* [<span data-ttu-id="bbbe7-112">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="bbbe7-112">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="bbbe7-113">Conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="bbbe7-113">Azure storage account</span></span>](storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/vs-storage-aspnet-getting-started-create-azure-account.md)]

[!INCLUDE [storage-development-environment-include](../../includes/vs-storage-aspnet-getting-started-setup-dev-env.md)]

### <a name="create-an-mvc-controller"></a><span data-ttu-id="bbbe7-114">Criar um controlador MVC</span><span class="sxs-lookup"><span data-stu-id="bbbe7-114">Create an MVC controller</span></span> 

1. <span data-ttu-id="bbbe7-115">No **Gerenciador de Soluções**, clique com o botão direito do mouse em **Controladores** e, no menu de contexto, selecione **Adicionar-> Controlador**.</span><span class="sxs-lookup"><span data-stu-id="bbbe7-115">In the **Solution Explorer**, right-click **Controllers**, and, from the context menu, select **Add->Controller**.</span></span>

    ![Adicionar um controlador a um aplicativo ASP.NET MVC](./media/vs-storage-aspnet-getting-started-queues/add-controller-menu.png)

1. <span data-ttu-id="bbbe7-117">Na caixa de diálogo **Adicionar Scaffold**, clique em **Controlador MVC 5 – Vazio** e selecione **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="bbbe7-117">On the **Add Scaffold** dialog, select **MVC 5 Controller - Empty**, and select **Add**.</span></span>

    ![Especificar o tipo de controlador MVC](./media/vs-storage-aspnet-getting-started-queues/add-controller.png)

1. <span data-ttu-id="bbbe7-119">Na caixa de diálogo **Adicionar Controlador**, nomeie o controlador como *QueuesController* e selecione **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="bbbe7-119">On the **Add Controller** dialog, name the controller *QueuesController*, and select **Add**.</span></span>

    ![Dê um nome ao controlador MVC](./media/vs-storage-aspnet-getting-started-queues/add-controller-name.png)

1. <span data-ttu-id="bbbe7-121">Adicione as seguintes diretivas *using* ao arquivo `QueuesController.cs`:</span><span class="sxs-lookup"><span data-stu-id="bbbe7-121">Add the following *using* directives to the `QueuesController.cs` file:</span></span>

    ```csharp
    using Microsoft.Azure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Auth;
    using Microsoft.WindowsAzure.Storage.Queue;
    ```
## <a name="create-a-queue"></a><span data-ttu-id="bbbe7-122">Criar uma fila</span><span class="sxs-lookup"><span data-stu-id="bbbe7-122">Create a queue</span></span>

<span data-ttu-id="bbbe7-123">As etapas a seguir ilustram como criar uma fila:</span><span class="sxs-lookup"><span data-stu-id="bbbe7-123">The following steps illustrate how to create a queue:</span></span>

> [!NOTE]
> 
> <span data-ttu-id="bbbe7-124">Esta seção pressupõe que você concluiu as etapas [Configurar o ambiente de desenvolvimento](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="bbbe7-124">This section assumes you have completed the steps [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="bbbe7-125">Abra o arquivo `QueuesController.cs` .</span><span class="sxs-lookup"><span data-stu-id="bbbe7-125">Open the `QueuesController.cs` file.</span></span> 

1. <span data-ttu-id="bbbe7-126">Adicione um método chamado **CreateQueue** que retorna um **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="bbbe7-126">Add a method called **CreateQueue** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult CreateQueue()
    {
        // The code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="bbbe7-127">Dentro do método **CreateQueue**, obtenha um objeto **CloudStorageAccount** que representa as informações da sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="bbbe7-127">Within the **CreateQueue** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="bbbe7-128">Use o seguinte código para obter as informações da cadeia de conexão e conta de armazenamento da configuração de serviço do Azure: (Altere *&lt;nome-da-conta-de-armazenamento>* para o nome da conta de armazenamento do Azure que você está acessando.)</span><span class="sxs-lookup"><span data-stu-id="bbbe7-128">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="bbbe7-129">Obtenha um objeto **CloudQueueClient** que representa um cliente do serviço de fila.</span><span class="sxs-lookup"><span data-stu-id="bbbe7-129">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```
1. <span data-ttu-id="bbbe7-130">Obtenha um objeto **CloudQueue** que representa uma referência ao nome da fila desejada.</span><span class="sxs-lookup"><span data-stu-id="bbbe7-130">Get a **CloudQueue** object that represents a reference to the desired queue name.</span></span> <span data-ttu-id="bbbe7-131">O método **CloudQueueClient.GetQueueReference** não faz uma solicitação para o Armazenamento de Filas.</span><span class="sxs-lookup"><span data-stu-id="bbbe7-131">The **CloudQueueClient.GetQueueReference** method does not make a request against queue storage.</span></span> <span data-ttu-id="bbbe7-132">A referência é retornada mesmo se as filas não existirem.</span><span class="sxs-lookup"><span data-stu-id="bbbe7-132">The reference is returned whether or not the queue exists.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="bbbe7-133">Chame o método **CloudQueue.CreateIfNotExists** para criar a fila se ela ainda não existir.</span><span class="sxs-lookup"><span data-stu-id="bbbe7-133">Call the **CloudQueue.CreateIfNotExists** method to create the queue if it does not yet exist.</span></span> <span data-ttu-id="bbbe7-134">O método **CloudQueue.CreateIfNotExists** retorna **true** se a fila não existir e for criada com êxito.</span><span class="sxs-lookup"><span data-stu-id="bbbe7-134">The **CloudQueue.CreateIfNotExists** method returns **true** if the queue does not exist, and is successfully created.</span></span> <span data-ttu-id="bbbe7-135">Caso contrário, **false** será retornado.</span><span class="sxs-lookup"><span data-stu-id="bbbe7-135">Otherwise, **false** is returned.</span></span>    

    ```csharp
    ViewBag.Success = queue.CreateIfNotExists();
    ```

1. <span data-ttu-id="bbbe7-136">Atualize o **ViewBag** com o nome da fila.</span><span class="sxs-lookup"><span data-stu-id="bbbe7-136">Update the **ViewBag** with the name of the queue.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ```

1. <span data-ttu-id="bbbe7-137">No **Gerenciador de Soluções**, expanda a pasta **Exibições**, clique com o botão direito do mouse em **Filas** e, no menu de contexto, selecione **Adicionar->Exibição**.</span><span class="sxs-lookup"><span data-stu-id="bbbe7-137">In the **Solution Explorer**, expand the **Views** folder, right-click **Queues**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="bbbe7-138">Na caixa de diálogo **Adicionar Exibição**, insira **CreateQueue** para o nome de exibição e selecione **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="bbbe7-138">On the **Add View** dialog, enter **CreateQueue** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="bbbe7-139">Abra `CreateQueue.cshtml` e modifique-o para que se pareça com o seguinte trecho de código:</span><span class="sxs-lookup"><span data-stu-id="bbbe7-139">Open `CreateQueue.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Create Queue";
    }
    
    <h2>Create Queue results</h2>

    Creation of @ViewBag.QueueName @(ViewBag.Success == true ? "succeeded" : "failed")
    ```

1. <span data-ttu-id="bbbe7-140">No **Gerenciador de Soluções**, expanda a pasta **Exibições->Compartilhadas** e abra `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="bbbe7-140">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="bbbe7-141">Após o último **Html.ActionLink**, adicione o seguinte **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="bbbe7-141">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Create queue", "CreateQueue", "Queues")</li>
    ```

1. <span data-ttu-id="bbbe7-142">Execute o aplicativo e selecione **Criar fila** para ver resultados semelhantes à seguinte captura de tela:</span><span class="sxs-lookup"><span data-stu-id="bbbe7-142">Run the application, and select **Create queue** to see results similar to the following screen shot:</span></span>
  
    ![Criar fila](./media/vs-storage-aspnet-getting-started-queues/create-queue-results.png)

    <span data-ttu-id="bbbe7-144">Conforme mencionado anteriormente, o método **CloudQueue.CreateIfNotExists** retornará **true** apenas quando a fila não existir e for criada.</span><span class="sxs-lookup"><span data-stu-id="bbbe7-144">As mentioned previously, the **CloudQueue.CreateIfNotExists** method returns **true** only when the queue doesn't exist and is created.</span></span> <span data-ttu-id="bbbe7-145">Portanto, se você executar o aplicativo quando a fila existir, o método retornará **false**.</span><span class="sxs-lookup"><span data-stu-id="bbbe7-145">Therefore, if you run the app when the queue exists, the method returns **false**.</span></span> <span data-ttu-id="bbbe7-146">Para executar o aplicativo várias vezes, você deverá excluir a fila antes de executar o aplicativo novamente.</span><span class="sxs-lookup"><span data-stu-id="bbbe7-146">To run the app multiple times, you must delete the queue before running the app again.</span></span> <span data-ttu-id="bbbe7-147">É possível excluir a fila por meio do método **CloudQueue.Delete**.</span><span class="sxs-lookup"><span data-stu-id="bbbe7-147">Deleting the queue can be done via the **CloudQueue.Delete** method.</span></span> <span data-ttu-id="bbbe7-148">Também é possível excluir a fila usando o [Portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040) ou o [Gerenciador de Armazenamento do Microsoft Azure](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="bbbe7-148">You can also delete the queue using the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) or the [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span></span>  

## <a name="add-a-message-to-a-queue"></a><span data-ttu-id="bbbe7-149">Adicionar uma mensagem a uma fila</span><span class="sxs-lookup"><span data-stu-id="bbbe7-149">Add a message to a queue</span></span>

<span data-ttu-id="bbbe7-150">Depois que você tiver [criado uma fila](#create-a-queue), poderá adicionar mensagens a ela.</span><span class="sxs-lookup"><span data-stu-id="bbbe7-150">Once you've [created a queue](#create-a-queue), you can add messages to that queue.</span></span> <span data-ttu-id="bbbe7-151">Esta seção orientará você pela adição de uma mensagem para uma fila *test-queue*.</span><span class="sxs-lookup"><span data-stu-id="bbbe7-151">This section walks you through adding a message to a queue *test-queue*.</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="bbbe7-152">Esta seção pressupõe que você concluiu as etapas [Configurar o ambiente de desenvolvimento](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="bbbe7-152">This section assumes you have completed the steps [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="bbbe7-153">Abra o arquivo `QueuesController.cs` .</span><span class="sxs-lookup"><span data-stu-id="bbbe7-153">Open the `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="bbbe7-154">Adicione um método chamado **AddMessage** que retorna um **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="bbbe7-154">Add a method called **AddMessage** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult AddMessage()
    {
        // The code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="bbbe7-155">Dentro do método **AddMessage**, obtenha um objeto **CloudStorageAccount** que representa as informações da sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="bbbe7-155">Within the **AddMessage** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="bbbe7-156">Use o seguinte código para obter as informações da cadeia de conexão e conta de armazenamento da configuração de serviço do Azure: (Altere *&lt;nome-da-conta-de-armazenamento>* para o nome da conta de armazenamento do Azure que você está acessando.)</span><span class="sxs-lookup"><span data-stu-id="bbbe7-156">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="bbbe7-157">Obtenha um objeto **CloudQueueClient** que representa um cliente do serviço de fila.</span><span class="sxs-lookup"><span data-stu-id="bbbe7-157">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="bbbe7-158">Obtenha um objeto **CloudQueueContainer** que representa uma referência à fila.</span><span class="sxs-lookup"><span data-stu-id="bbbe7-158">Get a **CloudQueueContainer** object that represents a reference to the queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="bbbe7-159">Crie o objeto **CloudQueueMessage** que representa a mensagem que você deseja adicionar à fila.</span><span class="sxs-lookup"><span data-stu-id="bbbe7-159">Create the **CloudQueueMessage** object representing the message you want to add to the queue.</span></span> <span data-ttu-id="bbbe7-160">Um objeto **CloudQueueMessage** pode ser criado por meio de uma cadeia de caracteres (em formato UTF-8) ou de uma matriz de bytes.</span><span class="sxs-lookup"><span data-stu-id="bbbe7-160">A **CloudQueueMessage** object can be created from either a string (in UTF-8 format) or a byte array.</span></span>

    ```csharp
    CloudQueueMessage message = new CloudQueueMessage("Hello, Azure Queue Storage");
    ```

1. <span data-ttu-id="bbbe7-161">Chame o método **CloudQueue.AddMessage** para adicionar a mensagem à fila.</span><span class="sxs-lookup"><span data-stu-id="bbbe7-161">Call the **CloudQueue.AddMessage** method to add the messaged to the queue.</span></span>

    ```csharp
    queue.AddMessage(message);
    ```

1. <span data-ttu-id="bbbe7-162">Crie e configure algumas propriedades **ViewBag** para serem mostradas na exibição.</span><span class="sxs-lookup"><span data-stu-id="bbbe7-162">Create and set a couple of **ViewBag** properties for display in the view.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Message = message.AsString;
    ```

1. <span data-ttu-id="bbbe7-163">No **Gerenciador de Soluções**, expanda a pasta **Exibições**, clique com o botão direito do mouse em **Filas** e, no menu de contexto, selecione **Adicionar->Exibição**.</span><span class="sxs-lookup"><span data-stu-id="bbbe7-163">In the **Solution Explorer**, expand the **Views** folder, right-click **Queues**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="bbbe7-164">Na caixa de diálogo **Adicionar Exibição**, digite **AddMessage** para o nome da exibição e selecione **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="bbbe7-164">On the **Add View** dialog, enter **AddMessage** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="bbbe7-165">Abra `AddMessage.cshtml` e modifique-o para que se pareça com o seguinte trecho de código:</span><span class="sxs-lookup"><span data-stu-id="bbbe7-165">Open `AddMessage.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Add Message";
    }
    
    <h2>Add Message results</h2>
    
    The message '@ViewBag.Message' was added to the queue '@ViewBag.QueueName'.
    ```

1. <span data-ttu-id="bbbe7-166">No **Gerenciador de Soluções**, expanda a pasta **Exibições->Compartilhadas** e abra `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="bbbe7-166">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="bbbe7-167">Após o último **Html.ActionLink**, adicione o seguinte **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="bbbe7-167">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Add message", "AddMessage", "Queues")</li>
    ```

1. <span data-ttu-id="bbbe7-168">Execute o aplicativo e selecione **Adicionar mensagem** para ver resultados semelhantes à seguinte captura de tela:</span><span class="sxs-lookup"><span data-stu-id="bbbe7-168">Run the application, and select **Add message** to see results similar to the following screen shot:</span></span>
  
    ![Adicionar mensagem](./media/vs-storage-aspnet-getting-started-queues/add-message-results.png)

<span data-ttu-id="bbbe7-170">As duas seções, [Ler uma mensagem de uma fila sem removê-la](#read-a-message-from-a-queue-without-removing-it) e [Ler e remover uma mensagem de uma fila](#read-and-remove-a-message-from-a-queue), ilustram como ler mensagens de uma fila.</span><span class="sxs-lookup"><span data-stu-id="bbbe7-170">The two sections - [Read a message from a queue without removing it](#read-a-message-from-a-queue-without-removing-it) and [Read and remove a message from a queue](#read-and-remove-a-message-from-a-queue) - illustrate how to read messages from a queue.</span></span>    

## <a name="read-a-message-from-a-queue-without-removing-it"></a><span data-ttu-id="bbbe7-171">Ler uma mensagem de uma fila sem removê-la</span><span class="sxs-lookup"><span data-stu-id="bbbe7-171">Read a message from a queue without removing it</span></span>

<span data-ttu-id="bbbe7-172">As etapas a seguir ilustram como espiar uma mensagem enfileirada (ler a primeira mensagem sem removê-la).</span><span class="sxs-lookup"><span data-stu-id="bbbe7-172">This section illustrates how to peek at a queued message (read the first message without removing it).</span></span>  

> [!NOTE]
> 
> <span data-ttu-id="bbbe7-173">Esta seção pressupõe que você concluiu as etapas [Configurar o ambiente de desenvolvimento](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="bbbe7-173">This section assumes you have completed the steps [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="bbbe7-174">Abra o arquivo `QueuesController.cs` .</span><span class="sxs-lookup"><span data-stu-id="bbbe7-174">Open the `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="bbbe7-175">Adicione um método chamado **PeekMessage** que retorna um **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="bbbe7-175">Add a method called **PeekMessage** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult PeekMessage()
    {
        // The code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="bbbe7-176">Dentro do método **PeekMessage**, obtenha um objeto **CloudStorageAccount** que representa as informações da sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="bbbe7-176">Within the **PeekMessage** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="bbbe7-177">Use o seguinte código para obter as informações da cadeia de conexão e conta de armazenamento da configuração de serviço do Azure: (Altere *&lt;nome-da-conta-de-armazenamento>* para o nome da conta de armazenamento do Azure que você está acessando.)</span><span class="sxs-lookup"><span data-stu-id="bbbe7-177">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="bbbe7-178">Obtenha um objeto **CloudQueueClient** que representa um cliente do serviço de fila.</span><span class="sxs-lookup"><span data-stu-id="bbbe7-178">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="bbbe7-179">Obtenha um objeto **CloudQueueContainer** que representa uma referência à fila.</span><span class="sxs-lookup"><span data-stu-id="bbbe7-179">Get a **CloudQueueContainer** object that represents a reference to the queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="bbbe7-180">Chame o método **CloudQueue.PeekMessage** para ler a primeira mensagem na fila sem removê-la da fila.</span><span class="sxs-lookup"><span data-stu-id="bbbe7-180">Call the **CloudQueue.PeekMessage** method to read the first message in the queue without removing it from the queue.</span></span> 

    ```csharp
    CloudQueueMessage message = queue.PeekMessage();
    ```

1. <span data-ttu-id="bbbe7-181">Atualize **ViewBag** com dois valores: o nome da fila e a mensagem que foi lida.</span><span class="sxs-lookup"><span data-stu-id="bbbe7-181">Update the **ViewBag** with two values: the queue name and the message that was read.</span></span> <span data-ttu-id="bbbe7-182">O objeto **CloudQueueMessage** expõe duas propriedades para obter o valor do objeto: **CloudQueueMessage.AsBytes** ou **CloudQueueMessage.AsString**.</span><span class="sxs-lookup"><span data-stu-id="bbbe7-182">The **CloudQueueMessage** object exposes two properties for getting the object's value: **CloudQueueMessage.AsBytes** and **CloudQueueMessage.AsString**.</span></span> <span data-ttu-id="bbbe7-183">**AsString** (usado neste exemplo) retorna uma cadeia de caracteres, enquanto **AsBytes** retorna uma matriz de bytes.</span><span class="sxs-lookup"><span data-stu-id="bbbe7-183">**AsString** (used in this example) returns a string, while **AsBytes** returns a byte array.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name; 
    ViewBag.Message = (message != null ? message.AsString : "");
    ```

1. <span data-ttu-id="bbbe7-184">No **Gerenciador de Soluções**, expanda a pasta **Exibições**, clique com o botão direito do mouse em **Filas** e, no menu de contexto, selecione **Adicionar->Exibição**.</span><span class="sxs-lookup"><span data-stu-id="bbbe7-184">In the **Solution Explorer**, expand the **Views** folder, right-click **Queues**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="bbbe7-185">Na caixa de diálogo **Adicionar Exibição**, digite **PeekMessage** para o nome da exibição e selecione **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="bbbe7-185">On the **Add View** dialog, enter **PeekMessage** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="bbbe7-186">Abra `PeekMessage.cshtml` e modifique-o para que se pareça com o seguinte trecho de código:</span><span class="sxs-lookup"><span data-stu-id="bbbe7-186">Open `PeekMessage.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

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

1. <span data-ttu-id="bbbe7-187">No **Gerenciador de Soluções**, expanda a pasta **Exibições->Compartilhadas** e abra `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="bbbe7-187">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="bbbe7-188">Após o último **Html.ActionLink**, adicione o seguinte **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="bbbe7-188">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Peek message", "PeekMessage", "Queues")</li>
    ```

1. <span data-ttu-id="bbbe7-189">Execute o aplicativo e selecione **Espiar Mensagem** para ver resultados semelhantes à seguinte captura de tela:</span><span class="sxs-lookup"><span data-stu-id="bbbe7-189">Run the application, and select **Peek message** to see results similar to the following screen shot:</span></span>
  
    ![Espiar mensagem](./media/vs-storage-aspnet-getting-started-queues/peek-message-results.png)

## <a name="read-and-remove-a-message-from-a-queue"></a><span data-ttu-id="bbbe7-191">Ler e remover uma mensagem de uma fila</span><span class="sxs-lookup"><span data-stu-id="bbbe7-191">Read and remove a message from a queue</span></span>

<span data-ttu-id="bbbe7-192">Nesta seção, você aprenderá como ler e remover uma mensagem de uma fila.</span><span class="sxs-lookup"><span data-stu-id="bbbe7-192">In this section, you learn how to read and remove a message from a queue.</span></span>   

> [!NOTE]
> 
> <span data-ttu-id="bbbe7-193">Esta seção pressupõe que você concluiu as etapas [Configurar o ambiente de desenvolvimento](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="bbbe7-193">This section assumes you have completed the steps [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="bbbe7-194">Abra o arquivo `QueuesController.cs` .</span><span class="sxs-lookup"><span data-stu-id="bbbe7-194">Open the `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="bbbe7-195">Adicione um método chamado **ReadMessage** que retorna um **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="bbbe7-195">Add a method called **ReadMessage** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult ReadMessage()
    {
        // The code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="bbbe7-196">Dentro do método **ReadMessage**, obtenha um objeto **CloudStorageAccount** que representa as informações da sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="bbbe7-196">Within the **ReadMessage** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="bbbe7-197">Use o seguinte código para obter as informações da cadeia de conexão e conta de armazenamento da configuração de serviço do Azure: (Altere *&lt;nome-da-conta-de-armazenamento>* para o nome da conta de armazenamento do Azure que você está acessando.)</span><span class="sxs-lookup"><span data-stu-id="bbbe7-197">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="bbbe7-198">Obtenha um objeto **CloudQueueClient** que representa um cliente do serviço de fila.</span><span class="sxs-lookup"><span data-stu-id="bbbe7-198">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="bbbe7-199">Obtenha um objeto **CloudQueueContainer** que representa uma referência à fila.</span><span class="sxs-lookup"><span data-stu-id="bbbe7-199">Get a **CloudQueueContainer** object that represents a reference to the queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="bbbe7-200">Chame o método **CloudQueue.GetMessage** para ler a primeira mensagem na fila.</span><span class="sxs-lookup"><span data-stu-id="bbbe7-200">Call the **CloudQueue.GetMessage** method to read the first message in the queue.</span></span> <span data-ttu-id="bbbe7-201">O método **CloudQueue.GetMessage** torna a mensagem invisível por 30 segundos (por padrão) para qualquer outro código que esteja lendo as mensagens, para que nenhum outro código possa modificar ou excluir a mensagem durante o seu processamento.</span><span class="sxs-lookup"><span data-stu-id="bbbe7-201">The **CloudQueue.GetMessage** method makes the message invisible for 30 seconds (by default) to any other code reading messages so that no other code can modify or delete the message while your processing it.</span></span> <span data-ttu-id="bbbe7-202">Para alterar o tempo durante o qual a mensagem fica invisível, modifique o parâmetro **visibilityTimeout** que está sendo passado para o método **CloudQueue.GetMessage**.</span><span class="sxs-lookup"><span data-stu-id="bbbe7-202">To change the amount of time the message is invisible, modify the **visibilityTimeout** parameter being passed to the **CloudQueue.GetMessage** method.</span></span>

    ```csharp
    // This message will be invisible to other code for 30 seconds.
    CloudQueueMessage message = queue.GetMessage();     
    ```

1. <span data-ttu-id="bbbe7-203">Chame o método **CloudQueueMessage.Delete** para excluir a mensagem da fila.</span><span class="sxs-lookup"><span data-stu-id="bbbe7-203">Call the **CloudQueueMessage.Delete** method to delete the message from the queue.</span></span>

    ```csharp
    queue.DeleteMessage(message);
    ```

1. <span data-ttu-id="bbbe7-204">Atualize o **ViewBag** com a mensagem excluída e o nome da fila.</span><span class="sxs-lookup"><span data-stu-id="bbbe7-204">Update the **ViewBag** with the message deleted, and the name of the queue.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Message = message.AsString;
    ```
 
1. <span data-ttu-id="bbbe7-205">No **Gerenciador de Soluções**, expanda a pasta **Exibições**, clique com o botão direito do mouse em **Filas** e, no menu de contexto, selecione **Adicionar->Exibição**.</span><span class="sxs-lookup"><span data-stu-id="bbbe7-205">In the **Solution Explorer**, expand the **Views** folder, right-click **Queues**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="bbbe7-206">Na caixa de diálogo **Adicionar Exibição**, digite **ReadMessage** para o nome da exibição e selecione **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="bbbe7-206">On the **Add View** dialog, enter **ReadMessage** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="bbbe7-207">Abra `ReadMessage.cshtml` e modifique-o para que se pareça com o seguinte trecho de código:</span><span class="sxs-lookup"><span data-stu-id="bbbe7-207">Open `ReadMessage.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

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

1. <span data-ttu-id="bbbe7-208">No **Gerenciador de Soluções**, expanda a pasta **Exibições->Compartilhadas** e abra `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="bbbe7-208">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="bbbe7-209">Após o último **Html.ActionLink**, adicione o seguinte **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="bbbe7-209">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Read/Delete message", "ReadMessage", "Queues")</li>
    ```

1. <span data-ttu-id="bbbe7-210">Execute o aplicativo e selecione **Ler/Excluir Mensagem** para ver resultados semelhantes à seguinte captura de tela:</span><span class="sxs-lookup"><span data-stu-id="bbbe7-210">Run the application, and select **Read/Delete message** to see results similar to the following screen shot:</span></span>
  
    ![Ler e excluir a mensagem](./media/vs-storage-aspnet-getting-started-queues/read-message-results.png)

## <a name="get-the-queue-length"></a><span data-ttu-id="bbbe7-212">Obter o tamanho da fila</span><span class="sxs-lookup"><span data-stu-id="bbbe7-212">Get the queue length</span></span>

<span data-ttu-id="bbbe7-213">Esta seção ilustra como obter o tamanho da fila (número de mensagens).</span><span class="sxs-lookup"><span data-stu-id="bbbe7-213">This section illustrates how to get the queue length (number of messages).</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="bbbe7-214">Esta seção pressupõe que você concluiu as etapas [Configurar o ambiente de desenvolvimento](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="bbbe7-214">This section assumes you have completed the steps [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="bbbe7-215">Abra o arquivo `QueuesController.cs` .</span><span class="sxs-lookup"><span data-stu-id="bbbe7-215">Open the `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="bbbe7-216">Adicione um método chamado **GetQueueLength** que retorna um **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="bbbe7-216">Add a method called **GetQueueLength** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult GetQueueLength()
    {
        // The code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="bbbe7-217">Dentro do método **ReadMessage**, obtenha um objeto **CloudStorageAccount** que representa as informações da sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="bbbe7-217">Within the **ReadMessage** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="bbbe7-218">Use o seguinte código para obter as informações da cadeia de conexão e conta de armazenamento da configuração de serviço do Azure: (Altere *&lt;nome-da-conta-de-armazenamento>* para o nome da conta de armazenamento do Azure que você está acessando.)</span><span class="sxs-lookup"><span data-stu-id="bbbe7-218">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="bbbe7-219">Obtenha um objeto **CloudQueueClient** que representa um cliente do serviço de fila.</span><span class="sxs-lookup"><span data-stu-id="bbbe7-219">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="bbbe7-220">Obtenha um objeto **CloudQueueContainer** que representa uma referência à fila.</span><span class="sxs-lookup"><span data-stu-id="bbbe7-220">Get a **CloudQueueContainer** object that represents a reference to the queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="bbbe7-221">Chame o método **CloudQueue.FetchAttributes** para recuperar os atributos da fila (incluindo seu tamanho).</span><span class="sxs-lookup"><span data-stu-id="bbbe7-221">Call the **CloudQueue.FetchAttributes** method to retrieve the queue's attributes (including its length).</span></span> 

    ```csharp
    queue.FetchAttributes();
    ```

6. <span data-ttu-id="bbbe7-222">Acesse a propriedade **CloudQueue.ApproximateMessageCount** para alterar o tamanho da fila.</span><span class="sxs-lookup"><span data-stu-id="bbbe7-222">Access the **CloudQueue.ApproximateMessageCount** property to get the queue's length.</span></span>
 
    ```csharp
    int? nMessages = queue.ApproximateMessageCount;
    ```

1. <span data-ttu-id="bbbe7-223">Atualize o **ViewBag** com o nome da fila e seu tamanho.</span><span class="sxs-lookup"><span data-stu-id="bbbe7-223">Update the **ViewBag** with the name of the queue, and its length.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Length = nMessages;
    ```
 
1. <span data-ttu-id="bbbe7-224">No **Gerenciador de Soluções**, expanda a pasta **Exibições**, clique com o botão direito do mouse em **Filas** e, no menu de contexto, selecione **Adicionar->Exibição**.</span><span class="sxs-lookup"><span data-stu-id="bbbe7-224">In the **Solution Explorer**, expand the **Views** folder, right-click **Queues**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="bbbe7-225">Na caixa de diálogo **Adicionar Exibição**, insira **GetQueueLength** para o nome da exibição e selecione **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="bbbe7-225">On the **Add View** dialog, enter **GetQueueLength** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="bbbe7-226">Abra `GetQueueLengthMessage.cshtml` e modifique-o para que se pareça com o seguinte trecho de código:</span><span class="sxs-lookup"><span data-stu-id="bbbe7-226">Open `GetQueueLengthMessage.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "GetQueueLength";
    }
    
    <h2>Get Queue Length results</h2>
    
    The queue '@ViewBag.QueueName' has a length of (number of messages): @ViewBag.Length
    ```

1. <span data-ttu-id="bbbe7-227">No **Gerenciador de Soluções**, expanda a pasta **Exibições->Compartilhadas** e abra `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="bbbe7-227">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="bbbe7-228">Após o último **Html.ActionLink**, adicione o seguinte **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="bbbe7-228">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Get queue length", "GetQueueLength", "Queues")</li>
    ```

1. <span data-ttu-id="bbbe7-229">Execute o aplicativo e selecione **Obter tamanho da fila** para ver resultados semelhantes à captura de tela a seguir:</span><span class="sxs-lookup"><span data-stu-id="bbbe7-229">Run the application, and select **Get queue length** to see results similar to the following screen shot:</span></span>
  
    ![Obter o tamanho da fila](./media/vs-storage-aspnet-getting-started-queues/get-queue-length-results.png)


## <a name="delete-a-queue"></a><span data-ttu-id="bbbe7-231">Excluir uma fila</span><span class="sxs-lookup"><span data-stu-id="bbbe7-231">Delete a queue</span></span>
<span data-ttu-id="bbbe7-232">Esta seção ilustra como excluir uma fila.</span><span class="sxs-lookup"><span data-stu-id="bbbe7-232">This section illustrates how to delete a queue.</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="bbbe7-233">Esta seção pressupõe que você concluiu as etapas [Configurar o ambiente de desenvolvimento](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="bbbe7-233">This section assumes you have completed the steps [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="bbbe7-234">Abra o arquivo `QueuesController.cs` .</span><span class="sxs-lookup"><span data-stu-id="bbbe7-234">Open the `QueuesController.cs` file.</span></span>

1. <span data-ttu-id="bbbe7-235">Adicione um método chamado **DeleteQueue** que retorna um **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="bbbe7-235">Add a method called **DeleteQueue** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult DeleteQueue()
    {
        // The code in this section goes here.

        return View();
    }
    ```
 
1. <span data-ttu-id="bbbe7-236">Dentro do método **DeleteQueue**, obtenha um objeto **CloudStorageAccount** que representa as informações da sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="bbbe7-236">Within the **DeleteQueue** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="bbbe7-237">Use o seguinte código para obter as informações da cadeia de conexão e conta de armazenamento da configuração de serviço do Azure: (Altere *&lt;nome-da-conta-de-armazenamento>* para o nome da conta de armazenamento do Azure que você está acessando.)</span><span class="sxs-lookup"><span data-stu-id="bbbe7-237">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. <span data-ttu-id="bbbe7-238">Obtenha um objeto **CloudQueueClient** que representa um cliente do serviço de fila.</span><span class="sxs-lookup"><span data-stu-id="bbbe7-238">Get a **CloudQueueClient** object represents a queue service client.</span></span>
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. <span data-ttu-id="bbbe7-239">Obtenha um objeto **CloudQueueContainer** que representa uma referência à fila.</span><span class="sxs-lookup"><span data-stu-id="bbbe7-239">Get a **CloudQueueContainer** object that represents a reference to the queue.</span></span> 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. <span data-ttu-id="bbbe7-240">Chame o método **CloudQueue.Delete** para excluir a fila representada pelo objeto **CloudQueue**.</span><span class="sxs-lookup"><span data-stu-id="bbbe7-240">Call the **CloudQueue.Delete** method to delete the queue represented by the **CloudQueue** object.</span></span>

    ```csharp
    queue.Delete();
    ```

1. <span data-ttu-id="bbbe7-241">Atualize o **ViewBag** com o nome da fila e seu tamanho.</span><span class="sxs-lookup"><span data-stu-id="bbbe7-241">Update the **ViewBag** with the name of the queue, and its length.</span></span>

    ```csharp
    ViewBag.QueueName = queue.Name;
    ```
 
1. <span data-ttu-id="bbbe7-242">No **Gerenciador de Soluções**, expanda a pasta **Exibições**, clique com o botão direito do mouse em **Filas** e, no menu de contexto, selecione **Adicionar->Exibição**.</span><span class="sxs-lookup"><span data-stu-id="bbbe7-242">In the **Solution Explorer**, expand the **Views** folder, right-click **Queues**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="bbbe7-243">Na caixa de diálogo **Adicionar Exibição**, insira **DeleteQueue** para o nome de exibição e selecione **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="bbbe7-243">On the **Add View** dialog, enter **DeleteQueue** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="bbbe7-244">Abra `DeleteQueue.cshtml` e modifique-o para que se pareça com o seguinte trecho de código:</span><span class="sxs-lookup"><span data-stu-id="bbbe7-244">Open `DeleteQueue.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "DeleteQueue";
    }
    
    <h2>Delete Queue results</h2>
    
    @ViewBag.QueueName deleted.
    ```

1. <span data-ttu-id="bbbe7-245">No **Gerenciador de Soluções**, expanda a pasta **Exibições->Compartilhadas** e abra `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="bbbe7-245">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="bbbe7-246">Após o último **Html.ActionLink**, adicione o seguinte **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="bbbe7-246">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Delete queue", "DeleteQueue", "Queues")</li>
    ```

1. <span data-ttu-id="bbbe7-247">Execute o aplicativo e selecione **Obter tamanho da fila** para ver resultados semelhantes à captura de tela a seguir:</span><span class="sxs-lookup"><span data-stu-id="bbbe7-247">Run the application, and select **Get queue length** to see results similar to the following screen shot:</span></span>
  
    ![Excluir fila](./media/vs-storage-aspnet-getting-started-queues/delete-queue-results.png)

## <a name="next-steps"></a><span data-ttu-id="bbbe7-249">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="bbbe7-249">Next steps</span></span>
<span data-ttu-id="bbbe7-250">Consulte outros guias de recursos para obter informações sobre opções adicionais para armazenar dados no Azure.</span><span class="sxs-lookup"><span data-stu-id="bbbe7-250">View more feature guides to learn about additional options for storing data in Azure.</span></span>

  * [<span data-ttu-id="bbbe7-251">Introdução ao Armazenamento de Blobs do Azure e aos Serviços Conectados do Visual Studio (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="bbbe7-251">Get started with Azure blob storage and Visual Studio Connected Services (ASP.NET)</span></span>](./vs-storage-aspnet-getting-started-blobs.md)
  * [<span data-ttu-id="bbbe7-252">Introdução ao Armazenamento de Tabelas do Azure e aos Serviços Conectados do Visual Studio (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="bbbe7-252">Get started with Azure table storage and Visual Studio Connected Services (ASP.NET)</span></span>](./vs-storage-aspnet-getting-started-tables.md)
