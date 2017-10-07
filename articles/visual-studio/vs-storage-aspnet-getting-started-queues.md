---
title: "aaaGet de Introdução ao armazenamento de fila do Azure e o Visual Studio conectado serviços (ASP.NET) | Microsoft Docs"
description: Como tooget iniciado usando o armazenamento de fila do Azure em um projeto do ASP.NET no Visual Studio depois de se conectar a conta de armazenamento tooa usando o Visual Studio conectado Services
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 94ca3413-5497-433f-abbe-836f83a9de72
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/23/2016
ms.author: kraigb
ms.openlocfilehash: 415a437c4ce60b1e2e328f8e937c73b0d5c50e78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-queue-storage-and-visual-studio-connected-services-aspnet"></a>Introdução ao Armazenamento de Filas do Azure e aos Serviços Conectados do Visual Studio (ASP.NET)
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a>Visão geral

O Armazenamento de Filas do Azure fornece mensagens na nuvem entre os componentes do aplicativo. Na criação de aplicativos para escala, os componentes do aplicativo geralmente são desassociados, para que possam ser redimensionados independentemente. Armazenamento de fila fornece mensagens assíncronas para a comunicação entre componentes de aplicativos, quer eles estejam em execução na nuvem hello, na área de trabalho hello, em um servidor local ou em um dispositivo móvel. O armazenamento de Fila também dá suporte ao gerenciamento de tarefas assíncronas e à criação de fluxos de trabalho do processo.

Este tutorial mostra como toowrite ASP.NET de código para alguns cenários comuns de uso de entidades de armazenamento de fila do Azure. Esses cenários incluem tarefas comuns como criar uma fila do Azure e adicionar, modificar, ler e remover mensagens da fila.

##<a name="prerequisites"></a>Pré-requisitos

* [Microsoft Visual Studio](https://www.visualstudio.com/downloads/)
* [Conta de armazenamento do Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/vs-storage-aspnet-getting-started-create-azure-account.md)]

[!INCLUDE [storage-development-environment-include](../../includes/vs-storage-aspnet-getting-started-setup-dev-env.md)]

### <a name="create-an-mvc-controller"></a>Criar um controlador MVC 

1. Em Olá **Gerenciador de soluções**, clique com botão direito **controladores**e, no menu de contexto hello, selecione **Adicionar -> controlador**.

    ![Adicionar um controlador tooan aplicativo ASP.NET MVC](./media/vs-storage-aspnet-getting-started-queues/add-controller-menu.png)

1. Em Olá **adicionar Scaffold** caixa de diálogo, selecione **controlador MVC 5 - vazio**e selecione **adicionar**.

    ![Especificar o tipo de controlador MVC](./media/vs-storage-aspnet-getting-started-queues/add-controller.png)

1. Em Olá **Adicionar controlador** caixa de diálogo, o nome de controlador de saudação *QueuesController*e selecione **adicionar**.

    ![Controlador MVC Olá nome](./media/vs-storage-aspnet-getting-started-queues/add-controller-name.png)

1. Adicione o seguinte Olá *usando* diretivas toohello `QueuesController.cs` arquivo:

    ```csharp
    using Microsoft.Azure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Auth;
    using Microsoft.WindowsAzure.Storage.Queue;
    ```
## <a name="create-a-queue"></a>Criar uma fila

Olá etapas a seguir ilustram como toocreate uma fila:

> [!NOTE]
> 
> Esta seção pressupõe que você concluiu as etapas de saudação [configurar o ambiente de desenvolvimento Olá](#set-up-the-development-environment). 

1. Olá abrir `QueuesController.cs` arquivo. 

1. Adicione um método chamado **CreateQueue** que retorna um **ActionResult**.

    ```csharp
    public ActionResult CreateQueue()
    {
        // hello code in this section goes here.

        return View();
    }
    ```

1. Dentro de saudação **CreateQueue** método, obter um **CloudStorageAccount** objeto que representa as informações da conta de armazenamento. Tooget Olá conta de armazenamento conexão cadeia de caracteres e o armazenamento de informações de configuração de serviço do Azure Olá de código a seguir de saudação de uso: (alteração  *&lt;nome da conta de armazenamento >* toohello nome da saudação armazenamento do Azure conta que você está acessando.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. Obtenha um objeto **CloudQueueClient** que representa um cliente do serviço de fila.
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```
1. Obter um **CloudQueue** objeto que representa um nome de fila desejada de toohello de referência. Olá **CloudQueueClient.GetQueueReference** método não faz uma solicitação em relação ao armazenamento de fila. referência de saudação é retornada se Olá fila existe ou não. 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. Chamar hello **CloudQueue.CreateIfNotExists** fila de saudação do método toocreate se ele ainda não existir. Olá **CloudQueue.CreateIfNotExists** método **true** se Olá fila não existe e foi criada com êxito. Caso contrário, **false** será retornado.    

    ```csharp
    ViewBag.Success = queue.CreateIfNotExists();
    ```

1. Saudação de atualização **ViewBag** com o nome de saudação da fila de saudação.

    ```csharp
    ViewBag.QueueName = queue.Name;
    ```

1. Em Olá **Gerenciador de soluções**, expanda Olá **exibições** pasta, com o botão direito **filas**e no menu de contexto hello, selecione **Adicionar -> exibição**.

1. Em Olá **adicionar exibição** caixa de diálogo, digite **CreateQueue** para o nome de exibição hello e selecione **adicionar**.

1. Abra `CreateQueue.cshtml`e modifique-o para que ele se parece com hello trecho de código a seguir:

    ```csharp
    @{
        ViewBag.Title = "Create Queue";
    }
    
    <h2>Create Queue results</h2>

    Creation of @ViewBag.QueueName @(ViewBag.Success == true ? "succeeded" : "failed")
    ```

1. Em Olá **Solution Explorer**, expanda Olá **exibições -> compartilhado** pasta e abra `_Layout.cshtml`.

1. Depois de saudação última **ActionLink**, adicione o seguinte de saudação **ActionLink**:

    ```html
    <li>@Html.ActionLink("Create queue", "CreateQueue", "Queues")</li>
    ```

1. Execute o aplicativo hello e selecione **criar fila** toosee resultados semelhante toohello captura de tela a seguir:
  
    ![Criar fila](./media/vs-storage-aspnet-getting-started-queues/create-queue-results.png)

    Conforme mencionado anteriormente, Olá **CloudQueue.CreateIfNotExists** método **true** somente quando a fila de saudação não existe e é criada. Portanto, se você executar o aplicativo hello quando Olá fila existe, método hello retorna **false**. toorun Olá aplicativo várias vezes, você deve excluir Olá fila antes de executar o aplicativo hello novamente. Excluindo fila de saudação pode ser feita por meio de saudação **CloudQueue.Delete** método. Você também pode excluir a fila de saudação usando Olá [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040) ou hello [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).  

## <a name="add-a-message-tooa-queue"></a>Adicionar uma fila de mensagens tooa

Depois que você [criar uma fila](#create-a-queue), você pode adicionar a fila de mensagens de toothat. Esta seção orienta você através de uma fila de mensagens tooa *testar fila*. 

> [!NOTE]
> 
> Esta seção pressupõe que você concluiu as etapas de saudação [configurar o ambiente de desenvolvimento Olá](#set-up-the-development-environment). 

1. Olá abrir `QueuesController.cs` arquivo.

1. Adicione um método chamado **AddMessage** que retorna um **ActionResult**.

    ```csharp
    public ActionResult AddMessage()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. Dentro de saudação **AddMessage** método, obter um **CloudStorageAccount** objeto que representa as informações da conta de armazenamento. Tooget Olá conta de armazenamento conexão cadeia de caracteres e o armazenamento de informações de configuração de serviço do Azure Olá de código a seguir de saudação de uso: (alteração  *&lt;nome da conta de armazenamento >* toohello nome da saudação armazenamento do Azure conta que você está acessando.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. Obtenha um objeto **CloudQueueClient** que representa um cliente do serviço de fila.
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. Obter um **CloudQueueContainer** objeto que representa uma fila de toohello de referência. 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. Criar hello **CloudQueueMessage** objeto que representa a mensagem de saudação quiser tooadd toohello fila. Um objeto **CloudQueueMessage** pode ser criado por meio de uma cadeia de caracteres (em formato UTF-8) ou de uma matriz de bytes.

    ```csharp
    CloudQueueMessage message = new CloudQueueMessage("Hello, Azure Queue Storage");
    ```

1. Chamar hello **CloudQueue.AddMessage** fila de toohello mensagem de saudação do método tooadd.

    ```csharp
    queue.AddMessage(message);
    ```

1. Crie e defina alguns **ViewBag** propriedades para exibição no modo de exibição de saudação.

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Message = message.AsString;
    ```

1. Em Olá **Gerenciador de soluções**, expanda Olá **exibições** pasta, com o botão direito **filas**e no menu de contexto hello, selecione **Adicionar -> exibição**.

1. Em Olá **adicionar exibição** caixa de diálogo, digite **AddMessage** para o nome de exibição hello e selecione **adicionar**.

1. Abra `AddMessage.cshtml`e modifique-o para que ele se parece com hello trecho de código a seguir:

    ```csharp
    @{
        ViewBag.Title = "Add Message";
    }
    
    <h2>Add Message results</h2>
    
    hello message '@ViewBag.Message' was added toohello queue '@ViewBag.QueueName'.
    ```

1. Em Olá **Solution Explorer**, expanda Olá **exibições -> compartilhado** pasta e abra `_Layout.cshtml`.

1. Depois de saudação última **ActionLink**, adicione o seguinte de saudação **ActionLink**:

    ```html
    <li>@Html.ActionLink("Add message", "AddMessage", "Queues")</li>
    ```

1. Execute o aplicativo hello e selecione **Adicionar mensagem** toosee resultados semelhante toohello captura de tela a seguir:
  
    ![Adicionar mensagem](./media/vs-storage-aspnet-getting-started-queues/add-message-results.png)

Olá duas seções - [ler uma mensagem de uma fila sem removê-lo](#read-a-message-from-a-queue-without-removing-it) e [leitura e remover uma mensagem de uma fila](#read-and-remove-a-message-from-a-queue) -ilustram como tooread mensagens de uma fila.  

## <a name="read-a-message-from-a-queue-without-removing-it"></a>Ler uma mensagem de uma fila sem removê-la

Esta seção ilustra como toopeek em uma mensagem na fila (leitura Olá primeira mensagem sem removê-lo).  

> [!NOTE]
> 
> Esta seção pressupõe que você concluiu as etapas de saudação [configurar o ambiente de desenvolvimento Olá](#set-up-the-development-environment). 

1. Olá abrir `QueuesController.cs` arquivo.

1. Adicione um método chamado **PeekMessage** que retorna um **ActionResult**.

    ```csharp
    public ActionResult PeekMessage()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. Dentro de saudação **PeekMessage** método, obter um **CloudStorageAccount** objeto que representa as informações da conta de armazenamento. Tooget Olá conta de armazenamento conexão cadeia de caracteres e o armazenamento de informações de configuração de serviço do Azure Olá de código a seguir de saudação de uso: (alteração  *&lt;nome da conta de armazenamento >* toohello nome da saudação armazenamento do Azure conta que você está acessando.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. Obtenha um objeto **CloudQueueClient** que representa um cliente do serviço de fila.
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. Obter um **CloudQueueContainer** objeto que representa uma fila de toohello de referência. 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. Chamar hello **CloudQueue.PeekMessage** método tooread Olá primeira mensagem na fila de saudação sem removê-la da fila de saudação. 

    ```csharp
    CloudQueueMessage message = queue.PeekMessage();
    ```

1. Saudação de atualização **ViewBag** com dois valores: nome da fila hello e uma mensagem de saudação que foi lido. Olá **CloudQueueMessage** objeto expõe duas propriedades para obter o valor do objeto Olá: **CloudQueueMessage.AsBytes** e **CloudQueueMessage.AsString**. **AsString** (usado neste exemplo) retorna uma cadeia de caracteres, enquanto **AsBytes** retorna uma matriz de bytes.

    ```csharp
    ViewBag.QueueName = queue.Name; 
    ViewBag.Message = (message != null ? message.AsString : "");
    ```

1. Em Olá **Gerenciador de soluções**, expanda Olá **exibições** pasta, com o botão direito **filas**e no menu de contexto hello, selecione **Adicionar -> exibição**.

1. Em Olá **adicionar exibição** caixa de diálogo, digite **PeekMessage** para o nome de exibição hello e selecione **adicionar**.

1. Abra `PeekMessage.cshtml`e modifique-o para que ele se parece com hello trecho de código a seguir:

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

1. Em Olá **Solution Explorer**, expanda Olá **exibições -> compartilhado** pasta e abra `_Layout.cshtml`.

1. Depois de saudação última **ActionLink**, adicione o seguinte de saudação **ActionLink**:

    ```html
    <li>@Html.ActionLink("Peek message", "PeekMessage", "Queues")</li>
    ```

1. Execute o aplicativo hello e selecione **inspecionar mensagem** toosee resultados semelhante toohello captura de tela a seguir:
  
    ![Espiar mensagem](./media/vs-storage-aspnet-getting-started-queues/peek-message-results.png)

## <a name="read-and-remove-a-message-from-a-queue"></a>Ler e remover uma mensagem de uma fila

Nesta seção, você aprenderá como tooread e remover uma mensagem de uma fila.   

> [!NOTE]
> 
> Esta seção pressupõe que você concluiu as etapas de saudação [configurar o ambiente de desenvolvimento Olá](#set-up-the-development-environment). 

1. Olá abrir `QueuesController.cs` arquivo.

1. Adicione um método chamado **ReadMessage** que retorna um **ActionResult**.

    ```csharp
    public ActionResult ReadMessage()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. Dentro de saudação **ReadMessage** método, obter um **CloudStorageAccount** objeto que representa as informações da conta de armazenamento. Tooget Olá conta de armazenamento conexão cadeia de caracteres e o armazenamento de informações de configuração de serviço do Azure Olá de código a seguir de saudação de uso: (alteração  *&lt;nome da conta de armazenamento >* toohello nome da saudação armazenamento do Azure conta que você está acessando.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. Obtenha um objeto **CloudQueueClient** que representa um cliente do serviço de fila.
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. Obter um **CloudQueueContainer** objeto que representa uma fila de toohello de referência. 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. Chamar hello **CloudQueue.GetMessage** método tooread Olá primeira mensagem na fila de saudação. Olá **CloudQueue.GetMessage** método torna Olá outro código ler mensagens de forma que nenhum outro código pode modificar ou excluir a mensagem de saudação durante o processamento de mensagem invisível para tooany de 30 segundos (por padrão). quantidade de saudação toochange de mensagem de saudação do tempo é invisível, modifique Olá **visibilityTimeout** parâmetro que está sendo passado toohello **CloudQueue.GetMessage** método.

    ```csharp
    // This message will be invisible tooother code for 30 seconds.
    CloudQueueMessage message = queue.GetMessage();     
    ```

1. Chamar hello **CloudQueueMessage.Delete** mensagem de saudação do método toodelete da fila de saudação.

    ```csharp
    queue.DeleteMessage(message);
    ```

1. Saudação de atualização **ViewBag** com hello mensagem excluída e Olá nome da fila de saudação.

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Message = message.AsString;
    ```
 
1. Em Olá **Gerenciador de soluções**, expanda Olá **exibições** pasta, com o botão direito **filas**e no menu de contexto hello, selecione **Adicionar -> exibição**.

1. Em Olá **adicionar exibição** caixa de diálogo, digite **ReadMessage** para o nome de exibição hello e selecione **adicionar**.

1. Abra `ReadMessage.cshtml`e modifique-o para que ele se parece com hello trecho de código a seguir:

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

1. Em Olá **Solution Explorer**, expanda Olá **exibições -> compartilhado** pasta e abra `_Layout.cshtml`.

1. Depois de saudação última **ActionLink**, adicione o seguinte de saudação **ActionLink**:

    ```html
    <li>@Html.ActionLink("Read/Delete message", "ReadMessage", "Queues")</li>
    ```

1. Execute o aplicativo hello e selecione **leitura/exclusão de mensagem** toosee resultados semelhante toohello captura de tela a seguir:
  
    ![Ler e excluir a mensagem](./media/vs-storage-aspnet-getting-started-queues/read-message-results.png)

## <a name="get-hello-queue-length"></a>Obter o comprimento da fila de saudação

Esta seção ilustra como tooget Olá comprimento da fila (número de mensagens). 

> [!NOTE]
> 
> Esta seção pressupõe que você concluiu as etapas de saudação [configurar o ambiente de desenvolvimento Olá](#set-up-the-development-environment). 

1. Olá abrir `QueuesController.cs` arquivo.

1. Adicione um método chamado **GetQueueLength** que retorna um **ActionResult**.

    ```csharp
    public ActionResult GetQueueLength()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. Dentro de saudação **ReadMessage** método, obter um **CloudStorageAccount** objeto que representa as informações da conta de armazenamento. Tooget Olá conta de armazenamento conexão cadeia de caracteres e o armazenamento de informações de configuração de serviço do Azure Olá de código a seguir de saudação de uso: (alteração  *&lt;nome da conta de armazenamento >* toohello nome da saudação armazenamento do Azure conta que você está acessando.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. Obtenha um objeto **CloudQueueClient** que representa um cliente do serviço de fila.
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. Obter um **CloudQueueContainer** objeto que representa uma fila de toohello de referência. 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. Chamar hello **CloudQueue.FetchAttributes** atributos da fila do método tooretrieve hello (incluindo seu comprimento). 

    ```csharp
    queue.FetchAttributes();
    ```

6. Saudação de acesso **CloudQueue.ApproximateMessageCount** comprimento da fila de saudação do tooget propriedade.
 
    ```csharp
    int? nMessages = queue.ApproximateMessageCount;
    ```

1. Saudação de atualização **ViewBag** com nome Olá Olá fila e seu tamanho.

    ```csharp
    ViewBag.QueueName = queue.Name;
    ViewBag.Length = nMessages;
    ```
 
1. Em Olá **Gerenciador de soluções**, expanda Olá **exibições** pasta, com o botão direito **filas**e no menu de contexto hello, selecione **Adicionar -> exibição**.

1. Em Olá **adicionar exibição** caixa de diálogo, digite **GetQueueLength** para o nome de exibição hello e selecione **adicionar**.

1. Abra `GetQueueLengthMessage.cshtml`e modifique-o para que ele se parece com hello trecho de código a seguir:

    ```csharp
    @{
        ViewBag.Title = "GetQueueLength";
    }
    
    <h2>Get Queue Length results</h2>
    
    hello queue '@ViewBag.QueueName' has a length of (number of messages): @ViewBag.Length
    ```

1. Em Olá **Solution Explorer**, expanda Olá **exibições -> compartilhado** pasta e abra `_Layout.cshtml`.

1. Depois de saudação última **ActionLink**, adicione o seguinte de saudação **ActionLink**:

    ```html
    <li>@Html.ActionLink("Get queue length", "GetQueueLength", "Queues")</li>
    ```

1. Execute o aplicativo hello e selecione **obter o comprimento da fila de** toosee resultados semelhante toohello captura de tela a seguir:
  
    ![Obter o tamanho da fila](./media/vs-storage-aspnet-getting-started-queues/get-queue-length-results.png)


## <a name="delete-a-queue"></a>Excluir uma fila
Esta seção ilustra como toodelete uma fila. 

> [!NOTE]
> 
> Esta seção pressupõe que você concluiu as etapas de saudação [configurar o ambiente de desenvolvimento Olá](#set-up-the-development-environment). 

1. Olá abrir `QueuesController.cs` arquivo.

1. Adicione um método chamado **DeleteQueue** que retorna um **ActionResult**.

    ```csharp
    public ActionResult DeleteQueue()
    {
        // hello code in this section goes here.

        return View();
    }
    ```
 
1. Dentro de saudação **DeleteQueue** método, obter um **CloudStorageAccount** objeto que representa as informações da conta de armazenamento. Tooget Olá conta de armazenamento conexão cadeia de caracteres e o armazenamento de informações de configuração de serviço do Azure Olá de código a seguir de saudação de uso: (alteração  *&lt;nome da conta de armazenamento >* toohello nome da saudação armazenamento do Azure conta que você está acessando.)
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```
   
1. Obtenha um objeto **CloudQueueClient** que representa um cliente do serviço de fila.
   
    ```csharp
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
    ```

1. Obter um **CloudQueueContainer** objeto que representa uma fila de toohello de referência. 
   
    ```csharp
    CloudQueue queue = queueClient.GetQueueReference("test-queue");
    ```

1. Chamar hello **CloudQueue.Delete** fila de saudação do método toodelete representada por Olá **CloudQueue** objeto.

    ```csharp
    queue.Delete();
    ```

1. Saudação de atualização **ViewBag** com nome Olá Olá fila e seu tamanho.

    ```csharp
    ViewBag.QueueName = queue.Name;
    ```
 
1. Em Olá **Gerenciador de soluções**, expanda Olá **exibições** pasta, com o botão direito **filas**e no menu de contexto hello, selecione **Adicionar -> exibição**.

1. Em Olá **adicionar exibição** caixa de diálogo, digite **DeleteQueue** para o nome de exibição hello e selecione **adicionar**.

1. Abra `DeleteQueue.cshtml`e modifique-o para que ele se parece com hello trecho de código a seguir:

    ```csharp
    @{
        ViewBag.Title = "DeleteQueue";
    }
    
    <h2>Delete Queue results</h2>
    
    @ViewBag.QueueName deleted.
    ```

1. Em Olá **Solution Explorer**, expanda Olá **exibições -> compartilhado** pasta e abra `_Layout.cshtml`.

1. Depois de saudação última **ActionLink**, adicione o seguinte de saudação **ActionLink**:

    ```html
    <li>@Html.ActionLink("Delete queue", "DeleteQueue", "Queues")</li>
    ```

1. Execute o aplicativo hello e selecione **obter o comprimento da fila de** toosee resultados semelhante toohello captura de tela a seguir:
  
    ![Excluir fila](./media/vs-storage-aspnet-getting-started-queues/delete-queue-results.png)

## <a name="next-steps"></a>Próximas etapas
Exiba toolearn de guias de recurso mais sobre opções adicionais para armazenar dados no Azure.

  * [Introdução ao Armazenamento de Blobs do Azure e aos Serviços Conectados do Visual Studio (ASP.NET)](../storage/vs-storage-aspnet-getting-started-blobs.md)
  * [Introdução ao Armazenamento de Tabelas do Azure e aos Serviços Conectados do Visual Studio (ASP.NET)](vs-storage-aspnet-getting-started-tables.md)
