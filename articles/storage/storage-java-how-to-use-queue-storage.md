---
title: aaaHow toouse armazenamento de fila do Java | Microsoft Docs
description: "Saiba como toocreate de serviço de fila do Azure toouse hello e filas delete e insert, obtenham e excluir mensagens. Amostras escritas em Java."
services: storage
documentationcenter: java
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 68cecc8e-38c9-4a24-99e8-cb722bc63cf9
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: c2d5211ec5b6454f7dbc126aad4ba9950df13661
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-java"></a><span data-ttu-id="d5316-104">Como toouse armazenamento de fila do Java</span><span class="sxs-lookup"><span data-stu-id="d5316-104">How toouse Queue storage from Java</span></span>
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-check-out-samples-java](../../includes/storage-check-out-samples-java.md)]

## <a name="overview"></a><span data-ttu-id="d5316-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="d5316-105">Overview</span></span>
<span data-ttu-id="d5316-106">Este guia mostrará como tooperform cenários comuns usando Olá serviço de armazenamento de fila do Azure.</span><span class="sxs-lookup"><span data-stu-id="d5316-106">This guide will show you how tooperform common scenarios using hello Azure Queue storage service.</span></span> <span data-ttu-id="d5316-107">exemplos de saudação são escritos em Java e usam Olá [SDK de armazenamento do Azure para Java][Azure Storage SDK for Java].</span><span class="sxs-lookup"><span data-stu-id="d5316-107">hello samples are written in Java and use hello [Azure Storage SDK for Java][Azure Storage SDK for Java].</span></span> <span data-ttu-id="d5316-108">Olá cenários abordados incluem **inserindo**, **inspecionar**, **obtendo**, e **excluindo** Enfileirar mensagens, bem como  **Criando** e **excluindo** filas.</span><span class="sxs-lookup"><span data-stu-id="d5316-108">hello scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating** and **deleting** queues.</span></span> <span data-ttu-id="d5316-109">Para obter mais informações sobre filas, consulte Olá [próximas etapas](#Next-Steps) seção.</span><span class="sxs-lookup"><span data-stu-id="d5316-109">For more information on queues, see hello [Next steps](#Next-Steps) section.</span></span>

<span data-ttu-id="d5316-110">Observação: um SDK está disponível para os desenvolvedores que usam o Armazenamento do Azure em dispositivos Android.</span><span class="sxs-lookup"><span data-stu-id="d5316-110">Note: An SDK is available for developers who are using Azure Storage on Android devices.</span></span> <span data-ttu-id="d5316-111">Para obter mais informações, consulte Olá [SDK de armazenamento do Azure para Android][Azure Storage SDK for Android].</span><span class="sxs-lookup"><span data-stu-id="d5316-111">For more information, see hello [Azure Storage SDK for Android][Azure Storage SDK for Android].</span></span>

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-java-application"></a><span data-ttu-id="d5316-112">Criar um aplicativo Java</span><span class="sxs-lookup"><span data-stu-id="d5316-112">Create a Java application</span></span>
<span data-ttu-id="d5316-113">Neste guia, você usará os recursos de armazenamento que podem ser executados em um aplicativo Java localmente ou no código em execução em uma função web ou de trabalho do Azure.</span><span class="sxs-lookup"><span data-stu-id="d5316-113">In this guide, you will use storage features which can be run within a Java application locally, or in code running within a web role or worker role in Azure.</span></span>

<span data-ttu-id="d5316-114">toodo assim, você precisará tooinstall Olá Java Development Kit (JDK) e criar uma conta de armazenamento do Azure em sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="d5316-114">toodo so, you will need tooinstall hello Java Development Kit (JDK) and create an Azure storage account in your Azure subscription.</span></span> <span data-ttu-id="d5316-115">Depois de você ter feito isso, você precisará tooverify seu sistema de desenvolvimento atende aos requisitos mínimos de saudação e dependências que são listadas no hello [SDK de armazenamento do Azure para Java] [ Azure Storage SDK for Java] repositório no GitHub.</span><span class="sxs-lookup"><span data-stu-id="d5316-115">Once you have done so, you will need tooverify that your development system meets hello minimum requirements and dependencies which are listed in hello [Azure Storage SDK for Java][Azure Storage SDK for Java] repository on GitHub.</span></span> <span data-ttu-id="d5316-116">Se seu sistema atende a esses requisitos, você pode seguir as instruções de saudação para baixar e instalar Olá bibliotecas de armazenamento do Azure para Java em seu sistema desse repositório.</span><span class="sxs-lookup"><span data-stu-id="d5316-116">If your system meets those requirements, you can follow hello instructions for downloading and installing hello Azure Storage Libraries for Java on your system from that repository.</span></span> <span data-ttu-id="d5316-117">Depois de concluir essas tarefas, será possível toocreate um aplicativo Java que usa exemplos Olá neste artigo.</span><span class="sxs-lookup"><span data-stu-id="d5316-117">Once you have completed those tasks, you will be able toocreate a Java application which uses hello examples in this article.</span></span>

## <a name="configure-your-application-tooaccess-queue-storage"></a><span data-ttu-id="d5316-118">Configurar o armazenamento de fila de tooaccess de aplicativo</span><span class="sxs-lookup"><span data-stu-id="d5316-118">Configure your application tooaccess queue storage</span></span>
<span data-ttu-id="d5316-119">Adicione Olá importação instruções toohello superior do arquivo de Java Olá onde você deseja que as filas de tooaccess APIs de armazenamento do Azure toouse a seguir:</span><span class="sxs-lookup"><span data-stu-id="d5316-119">Add hello following import statements toohello top of hello Java file where you want toouse Azure storage APIs tooaccess queues:</span></span>

```java
// Include hello following imports toouse queue APIs.
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.queue.*;
```

## <a name="setup-an-azure-storage-connection-string"></a><span data-ttu-id="d5316-120">Configurar uma cadeia de conexão de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="d5316-120">Setup an Azure storage connection string</span></span>
<span data-ttu-id="d5316-121">Um cliente de armazenamento do Azure usa um pontos de extremidade de toostore de cadeia de caracteres de conexão de armazenamento e as credenciais para acessar os serviços de gerenciamento de dados.</span><span class="sxs-lookup"><span data-stu-id="d5316-121">An Azure storage client uses a storage connection string toostore endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="d5316-122">Quando em execução em um aplicativo cliente, deve fornecer a cadeia de conexão de armazenamento Olá no formato a seguir, usando o nome de saudação da sua conta de armazenamento de saudação e Olá chave de acesso primária para conta de armazenamento Olá listada no hello [Portal do Azure](https://portal.azure.com)para Olá *AccountName* e *AccountKey* valores.</span><span class="sxs-lookup"><span data-stu-id="d5316-122">When running in a client application, you must provide hello storage connection string in hello following format, using hello name of your storage account and hello Primary access key for hello storage account listed in hello [Azure Portal](https://portal.azure.com) for hello *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="d5316-123">Este exemplo mostra como você pode declarar uma cadeia de caracteres de conexão do campo estático toohold hello:</span><span class="sxs-lookup"><span data-stu-id="d5316-123">This example shows how you can declare a static field toohold hello connection string:</span></span>

```java
// Define hello connection-string with your values.
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key";
```

<span data-ttu-id="d5316-124">Em um aplicativo em execução dentro de uma função no Microsoft Azure, essa cadeia de caracteres pode ser armazenada no arquivo de configuração do serviço hello, *ServiceConfiguration*e pode ser acessado com uma chamada toohello  **RoleEnvironment.getConfigurationSettings** método.</span><span class="sxs-lookup"><span data-stu-id="d5316-124">In an application running within a role in Microsoft Azure, this string can be stored in hello service configuration file, *ServiceConfiguration.cscfg*, and can be accessed with a call toohello **RoleEnvironment.getConfigurationSettings** method.</span></span> <span data-ttu-id="d5316-125">Aqui está um exemplo de obter a cadeia de caracteres de conexão de saudação de um **configuração** elemento chamado *StorageConnectionString* no arquivo de configuração de serviço hello:</span><span class="sxs-lookup"><span data-stu-id="d5316-125">Here's an example of getting hello connection string from a **Setting** element named *StorageConnectionString* in hello service configuration file:</span></span>

```java
// Retrieve storage account from connection-string.
String storageConnectionString =
    RoleEnvironment.getConfigurationSettings().get("StorageConnectionString");
```

<span data-ttu-id="d5316-126">Olá exemplos a seguir pressupõem que você usou uma cadeia de conexão de armazenamento esses dois métodos tooget hello.</span><span class="sxs-lookup"><span data-stu-id="d5316-126">hello following samples assume that you have used one of these two methods tooget hello storage connection string.</span></span>

## <a name="how-to-create-a-queue"></a><span data-ttu-id="d5316-127">Como criar uma fila</span><span class="sxs-lookup"><span data-stu-id="d5316-127">How to: Create a queue</span></span>
<span data-ttu-id="d5316-128">Um objeto **CloudQueueClient** permite que você obtenha objetos de referência para filas.</span><span class="sxs-lookup"><span data-stu-id="d5316-128">A **CloudQueueClient** object lets you get reference objects for queues.</span></span> <span data-ttu-id="d5316-129">Olá código a seguir cria um **CloudQueueClient** objeto.</span><span class="sxs-lookup"><span data-stu-id="d5316-129">hello following code creates a **CloudQueueClient** object.</span></span> <span data-ttu-id="d5316-130">(Observação: existem outras maneiras toocreate **CloudStorageAccount** objetos; para obter mais informações, consulte **CloudStorageAccount** em Olá [referência de SDK de cliente de armazenamento de Azure].)</span><span class="sxs-lookup"><span data-stu-id="d5316-130">(Note: There are additional ways toocreate **CloudStorageAccount** objects; for more information, see **CloudStorageAccount** in hello [Azure Storage Client SDK Reference].)</span></span>

<span data-ttu-id="d5316-131">Saudação de uso **CloudQueueClient** tooget uma fila de toohello de referência que você deseja toouse do objeto.</span><span class="sxs-lookup"><span data-stu-id="d5316-131">Use hello **CloudQueueClient** object tooget a reference toohello queue you want toouse.</span></span> <span data-ttu-id="d5316-132">Você pode criar a fila de saudação se ele não existir.</span><span class="sxs-lookup"><span data-stu-id="d5316-132">You can create hello queue if it doesn't exist.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

   // Create hello queue client.
   CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

   // Retrieve a reference tooa queue.
   CloudQueue queue = queueClient.getQueueReference("myqueue");

   // Create hello queue if it doesn't already exist.
   queue.createIfNotExists();
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-add-a-message-tooa-queue"></a><span data-ttu-id="d5316-133">Como: adicionar uma fila de mensagens tooa</span><span class="sxs-lookup"><span data-stu-id="d5316-133">How to: Add a message tooa queue</span></span>
<span data-ttu-id="d5316-134">tooinsert uma mensagem em uma fila existente, primeiro crie um novo **CloudQueueMessage**.</span><span class="sxs-lookup"><span data-stu-id="d5316-134">tooinsert a message into an existing queue, first create a new **CloudQueueMessage**.</span></span> <span data-ttu-id="d5316-135">Em seguida, chame Olá **addMessage** método.</span><span class="sxs-lookup"><span data-stu-id="d5316-135">Next, call hello **addMessage** method.</span></span> <span data-ttu-id="d5316-136">Um **CloudQueueMessage** pode ser criado por meio de uma cadeia de caracteres (em formato UTF-8) ou de uma matriz de bytes.</span><span class="sxs-lookup"><span data-stu-id="d5316-136">A **CloudQueueMessage** can be created from either a string (in UTF-8 format) or a byte array.</span></span> <span data-ttu-id="d5316-137">Aqui está o código que cria uma fila (se não existir) e a mensagem de saudação inserções "Olá, mundo".</span><span class="sxs-lookup"><span data-stu-id="d5316-137">Here is code which creates a queue (if it doesn't exist) and inserts hello message "Hello, World".</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Create hello queue if it doesn't already exist.
    queue.createIfNotExists();

    // Create a message and add it toohello queue.
    CloudQueueMessage message = new CloudQueueMessage("Hello, World");
    queue.addMessage(message);
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-peek-at-hello-next-message"></a><span data-ttu-id="d5316-138">Como: espiar a próxima mensagem de saudação</span><span class="sxs-lookup"><span data-stu-id="d5316-138">How to: Peek at hello next message</span></span>
<span data-ttu-id="d5316-139">Você pode inspecionar mensagem de saudação na frente de saudação de uma fila sem removê-la da fila de saudação chamando **peekMessage**.</span><span class="sxs-lookup"><span data-stu-id="d5316-139">You can peek at hello message in hello front of a queue without removing it from hello queue by calling **peekMessage**.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Peek at hello next message.
    CloudQueueMessage peekedMessage = queue.peekMessage();

    // Output hello message value.
    if (peekedMessage != null)
    {
      System.out.println(peekedMessage.getMessageContentAsString());
   }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-change-hello-contents-of-a-queued-message"></a><span data-ttu-id="d5316-140">Como: alterar o conteúdo de saudação de uma mensagem na fila</span><span class="sxs-lookup"><span data-stu-id="d5316-140">How to: Change hello contents of a queued message</span></span>
<span data-ttu-id="d5316-141">Você pode alterar o conteúdo de saudação de um mensagem no local na fila de saudação.</span><span class="sxs-lookup"><span data-stu-id="d5316-141">You can change hello contents of a message in-place in hello queue.</span></span> <span data-ttu-id="d5316-142">Se a mensagem de saudação representa uma tarefa de trabalho, você pode usar esse status do recurso tooupdate Olá da tarefa de trabalho hello.</span><span class="sxs-lookup"><span data-stu-id="d5316-142">If hello message represents a work task, you could use this feature tooupdate hello status of hello work task.</span></span> <span data-ttu-id="d5316-143">saudação de código a seguir atualiza a mensagem da fila de saudação com novo conteúdo e conjuntos Olá tooextend de tempo limite de visibilidade outro 60 segundos.</span><span class="sxs-lookup"><span data-stu-id="d5316-143">hello following code updates hello queue message with new contents, and sets hello visibility timeout tooextend another 60 seconds.</span></span> <span data-ttu-id="d5316-144">Isso salva o estado de saudação do trabalho associado à mensagem de saudação e fornece cliente Olá outro toocontinue minuto trabalhando na mensagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="d5316-144">This saves hello state of work associated with hello message, and gives hello client another minute toocontinue working on hello message.</span></span> <span data-ttu-id="d5316-145">Você pode usar esta técnica tootrack várias etapas os fluxos de trabalho na fila de mensagens, sem ter que toostart através do hello início se uma etapa de processamento falhar devido a falha de toohardware ou software.</span><span class="sxs-lookup"><span data-stu-id="d5316-145">You could use this technique tootrack multi-step workflows on queue messages, without having toostart over from hello beginning if a processing step fails due toohardware or software failure.</span></span> <span data-ttu-id="d5316-146">Normalmente, você mantém uma contagem de tentativa e se hello mensagem será repetida mais de  *n*  vezes, excluí-lo.</span><span class="sxs-lookup"><span data-stu-id="d5316-146">Typically, you would keep a retry count as well, and if hello message is retried more than *n* times, you would delete it.</span></span> <span data-ttu-id="d5316-147">Isso protege contra uma mensagem que dispara um erro do aplicativo sempre que for processada.</span><span class="sxs-lookup"><span data-stu-id="d5316-147">This protects against a message that triggers an application error each time it is processed.</span></span>

<span data-ttu-id="d5316-148">a seguir Olá pesquisas de exemplo por meio de fila de saudação de mensagens de código, localiza a primeira mensagem de saudação que corresponde a "Olá, mundo" para obter conteúdo hello, em seguida, modifica o conteúdo da mensagem de saudação e será encerrado.</span><span class="sxs-lookup"><span data-stu-id="d5316-148">hello following code sample searches through hello queue of messages, locates hello first message that matches "Hello, World" for hello content, then modifies hello message content and exits.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // hello maximum number of messages that can be retrieved is 32.
    final int MAX_NUMBER_OF_MESSAGES_TO_PEEK = 32;

    // Loop through hello messages in hello queue.
    for (CloudQueueMessage message : queue.retrieveMessages(MAX_NUMBER_OF_MESSAGES_TO_PEEK,1,null,null))
    {
        // Check for a specific string.
        if (message.getMessageContentAsString().equals("Hello, World"))
        {
            // Modify hello content of hello first matching message.
            message.setMessageContent("Updated contents.");
            // Set it toobe visible in 30 seconds.
            EnumSet<MessageUpdateFields> updateFields =
                EnumSet.of(MessageUpdateFields.CONTENT,
                MessageUpdateFields.VISIBILITY);
            // Update hello message.
            queue.updateMessage(message, 30, updateFields, null, null);
            break;
        }
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

<span data-ttu-id="d5316-149">Como alternativa, hello exemplo de código a seguir atualiza apenas Olá primeiro visível mensagem na fila de saudação.</span><span class="sxs-lookup"><span data-stu-id="d5316-149">Alternatively, hello following code sample updates just hello first visible message on hello queue.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Retrieve hello first visible message in hello queue.
    CloudQueueMessage message = queue.retrieveMessage();

    if (message != null)
    {
        // Modify hello message content.
        message.setMessageContent("Updated contents.");
        // Set it toobe visible in 60 seconds.
        EnumSet<MessageUpdateFields> updateFields =
            EnumSet.of(MessageUpdateFields.CONTENT,
            MessageUpdateFields.VISIBILITY);
        // Update hello message.
        queue.updateMessage(message, 60, updateFields, null, null);
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-get-hello-queue-length"></a><span data-ttu-id="d5316-150">Como: obter o comprimento da fila de saudação</span><span class="sxs-lookup"><span data-stu-id="d5316-150">How to: Get hello queue length</span></span>
<span data-ttu-id="d5316-151">Você pode obter uma estimativa do número de saudação de mensagens em uma fila.</span><span class="sxs-lookup"><span data-stu-id="d5316-151">You can get an estimate of hello number of messages in a queue.</span></span> <span data-ttu-id="d5316-152">Olá **downloadAttributes** método solicita o serviço de fila Olá para vários valores atuais, incluindo uma contagem de quantas mensagens estão em uma fila.</span><span class="sxs-lookup"><span data-stu-id="d5316-152">hello **downloadAttributes** method asks hello Queue service for several current values, including a count of how many messages are in a queue.</span></span> <span data-ttu-id="d5316-153">Contagem de saudação só é aproximada pois mensagens podem ser adicionadas ou removidas depois Olá serviço fila responde tooyour solicitação.</span><span class="sxs-lookup"><span data-stu-id="d5316-153">hello count is only approximate because messages can be added or removed after hello Queue service responds tooyour request.</span></span> <span data-ttu-id="d5316-154">Olá **getApproximateMessageCount** método retorna o último valor de saudação recuperado pela chamada de saudação muito**downloadAttributes**, sem chamar o serviço de fila de saudação.</span><span class="sxs-lookup"><span data-stu-id="d5316-154">hello **getApproximateMessageCount** method returns hello last value retrieved by hello call too**downloadAttributes**, without calling hello Queue service.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
       CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

   // Download hello approximate message count from hello server.
    queue.downloadAttributes();

    // Retrieve hello newly cached approximate message count.
    long cachedMessageCount = queue.getApproximateMessageCount();

    // Display hello queue length.
    System.out.println(String.format("Queue length: %d", cachedMessageCount));
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-dequeue-hello-next-message"></a><span data-ttu-id="d5316-155">Como: remover da fila de mensagem de saudação do próxima</span><span class="sxs-lookup"><span data-stu-id="d5316-155">How to: Dequeue hello next message</span></span>
<span data-ttu-id="d5316-156">Seu código remove uma mensagem de um fila em duas etapas.</span><span class="sxs-lookup"><span data-stu-id="d5316-156">Your code dequeues a message from a queue in two steps.</span></span> <span data-ttu-id="d5316-157">Quando você chama **retrieveMessage**, obter próxima mensagem de saudação em uma fila.</span><span class="sxs-lookup"><span data-stu-id="d5316-157">When you call **retrieveMessage**, you get hello next message in a queue.</span></span> <span data-ttu-id="d5316-158">Uma mensagem retornada de **retrieveMessage** se torna invisível tooany outro código de leitura de mensagens dessa fila.</span><span class="sxs-lookup"><span data-stu-id="d5316-158">A message returned from **retrieveMessage** becomes invisible tooany other code reading messages from this queue.</span></span> <span data-ttu-id="d5316-159">Por padrão, essa mensagem permanece invisível por 30 segundos.</span><span class="sxs-lookup"><span data-stu-id="d5316-159">By default, this message stays invisible for 30 seconds.</span></span> <span data-ttu-id="d5316-160">toofinish mensagem de saudação remover da fila hello, você também deve chamar **deleteMessage**.</span><span class="sxs-lookup"><span data-stu-id="d5316-160">toofinish removing hello message from hello queue, you must also call **deleteMessage**.</span></span> <span data-ttu-id="d5316-161">Esse processo de duas etapas de remoção de uma mensagem garante que se seu código falha tooprocess que uma mensagem devido a falha de toohardware ou software, outra instância do seu código pode obter Olá a mesma mensagem e tente novamente.</span><span class="sxs-lookup"><span data-stu-id="d5316-161">This two-step process of removing a message assures that if your code fails tooprocess a message due toohardware or software failure, another instance of your code can get hello same message and try again.</span></span> <span data-ttu-id="d5316-162">Seu código chama **deleteMessage** logo depois que a mensagem de saudação foi processada.</span><span class="sxs-lookup"><span data-stu-id="d5316-162">Your code calls **deleteMessage** right after hello message has been processed.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Retrieve hello first visible message in hello queue.
    CloudQueueMessage retrievedMessage = queue.retrieveMessage();

    if (retrievedMessage != null)
    {
        // Process hello message in less than 30 seconds, and then delete hello message.
        queue.deleteMessage(retrievedMessage);
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="additional-options-for-dequeuing-messages"></a><span data-ttu-id="d5316-163">Opções adicionais para remover mensagens da fila</span><span class="sxs-lookup"><span data-stu-id="d5316-163">Additional options for dequeuing messages</span></span>
<span data-ttu-id="d5316-164">Há duas maneiras de personalizar a recuperação da mensagem de uma fila.</span><span class="sxs-lookup"><span data-stu-id="d5316-164">There are two ways you can customize message retrieval from a queue.</span></span> <span data-ttu-id="d5316-165">Primeiro, você pode obter um lote de mensagens (até too32).</span><span class="sxs-lookup"><span data-stu-id="d5316-165">First, you can get a batch of messages (up too32).</span></span> <span data-ttu-id="d5316-166">Em seguida, você pode definir um tempo limite de invisibilidade maiores ou menores, permitindo que o código mais ou menos tempo toofully processam cada mensagem.</span><span class="sxs-lookup"><span data-stu-id="d5316-166">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time toofully process each message.</span></span>

<span data-ttu-id="d5316-167">Olá, exemplo de código a seguir usa Olá **retrieveMessages** mensagens tooget 20 de método em uma chamada.</span><span class="sxs-lookup"><span data-stu-id="d5316-167">hello following code example uses hello **retrieveMessages** method tooget 20 messages in one call.</span></span> <span data-ttu-id="d5316-168">Em seguida, ele processa cada mensagem usando um loop **for** .</span><span class="sxs-lookup"><span data-stu-id="d5316-168">Then it processes each message using a **for** loop.</span></span> <span data-ttu-id="d5316-169">Ele também define Olá invisibilidade tempo limite toofive minutos (300 segundos para cada mensagem).</span><span class="sxs-lookup"><span data-stu-id="d5316-169">It also sets hello invisibility timeout toofive minutes (300 seconds) for each message.</span></span> <span data-ttu-id="d5316-170">Observe que Olá cinco minutos é iniciado para todas as mensagens em Olá mesmo tempo, portanto, quando cinco minutos se passaram desde chamada hello muito**retrieveMessages**, qualquer mensagem que não foram excluídas se tornará visível novamente.</span><span class="sxs-lookup"><span data-stu-id="d5316-170">Note that hello five minutes starts for all messages at hello same time, so when five minutes have passed since hello call too**retrieveMessages**, any messages which have not been deleted will become visible again.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Retrieve 20 messages from hello queue with a visibility timeout of 300 seconds.
    for (CloudQueueMessage message : queue.retrieveMessages(20, 300, null, null)) {
        // Do processing for all messages in less than 5 minutes,
        // deleting each message after processing.
        queue.deleteMessage(message);
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-list-hello-queues"></a><span data-ttu-id="d5316-171">Como: listar Olá filas</span><span class="sxs-lookup"><span data-stu-id="d5316-171">How to: List hello queues</span></span>
<span data-ttu-id="d5316-172">tooobtain uma lista de filas de atual hello, chamada hello **CloudQueueClient.listQueues()** método, que retorna uma coleção de **CloudQueue** objetos.</span><span class="sxs-lookup"><span data-stu-id="d5316-172">tooobtain a list of hello current queues, call hello **CloudQueueClient.listQueues()** method, which will return a collection of **CloudQueue** objects.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient =
        storageAccount.createCloudQueueClient();

    // Loop through hello collection of queues.
    for (CloudQueue queue : queueClient.listQueues())
    {
        // Output each queue name.
        System.out.println(queue.getName());
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="d5316-173">Como excluir uma fila</span><span class="sxs-lookup"><span data-stu-id="d5316-173">How to: Delete a queue</span></span>
<span data-ttu-id="d5316-174">toodelete uma fila e todas as mensagens de saudação contidos nele, chamada hello **deleteIfExists** método hello **CloudQueue** objeto.</span><span class="sxs-lookup"><span data-stu-id="d5316-174">toodelete a queue and all hello messages contained in it, call hello **deleteIfExists** method on hello **CloudQueue** object.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello queue client.
    CloudQueueClient queueClient = storageAccount.createCloudQueueClient();

    // Retrieve a reference tooa queue.
    CloudQueue queue = queueClient.getQueueReference("myqueue");

    // Delete hello queue if it exists.
    queue.deleteIfExists();
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="next-steps"></a><span data-ttu-id="d5316-175">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d5316-175">Next steps</span></span>
<span data-ttu-id="d5316-176">Agora que você aprendeu as Noções básicas de saudação do armazenamento de fila, siga essas toolearn links sobre tarefas mais complexas de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="d5316-176">Now that you've learned hello basics of queue storage, follow these links toolearn about more complex storage tasks.</span></span>

* <span data-ttu-id="d5316-177">[Microsoft Azure Storage SDK for Java][Azure Storage SDK for Java] (SDK de Armazenamento do Microsoft Azure para Java)</span><span class="sxs-lookup"><span data-stu-id="d5316-177">[Azure Storage SDK for Java][Azure Storage SDK for Java]</span></span>
* <span data-ttu-id="d5316-178">[referência de SDK de cliente de armazenamento de Azure][referência de SDK de cliente de armazenamento de Azure]</span><span class="sxs-lookup"><span data-stu-id="d5316-178">[Azure Storage Client SDK Reference][Azure Storage Client SDK Reference]</span></span>
* <span data-ttu-id="d5316-179">[Azure Storage Services REST API Reference][Azure Storage Services REST API] (Referência de API REST dos Serviços de Armazenamento do Azure)</span><span class="sxs-lookup"><span data-stu-id="d5316-179">[Azure Storage Services REST API][Azure Storage Services REST API]</span></span>
* <span data-ttu-id="d5316-180">[Microsoft Azure Storage Team Blog][Azure Storage Team Blog] (Blog da equipe de Armazenamento do Microsoft Azure)</span><span class="sxs-lookup"><span data-stu-id="d5316-180">[Azure Storage Team Blog][Azure Storage Team Blog]</span></span>

[Azure SDK for Java]: http://go.microsoft.com/fwlink/?LinkID=525671
[Azure Storage SDK for Java]: https://github.com/azure/azure-storage-java
[Azure Storage SDK for Android]: https://github.com/azure/azure-storage-android
[referência de SDK de cliente de armazenamento de Azure]: http://dl.windowsazure.com/storage/javadoc/
[Azure Storage Services REST API]: https://msdn.microsoft.com/library/azure/dd179355.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
