---
title: armazenamento de fila aaaHow toouse (C++) | Microsoft Docs
description: "Saiba como toouse Olá serviço de armazenamento de fila no Azure. As amostras são escritas em C++."
services: storage
documentationcenter: .net
author: cbrooksmsft
manager: jahogg
editor: tysonn
ms.assetid: c8a36365-29f6-404d-8fd1-858a7f33b50a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: cpp
ms.topic: article
ms.date: 05/11/2017
ms.author: cbrooksmsft
ms.openlocfilehash: b0cddf017878e9fab87f47d24b2906e40c9f4ad5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-c"></a><span data-ttu-id="d9bbc-104">Como toouse armazenamento de fila de C++</span><span class="sxs-lookup"><span data-stu-id="d9bbc-104">How toouse Queue Storage from C++</span></span>
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="d9bbc-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="d9bbc-105">Overview</span></span>
<span data-ttu-id="d9bbc-106">Este guia mostrará como tooperform cenários comuns usando Olá serviço de armazenamento de fila do Azure.</span><span class="sxs-lookup"><span data-stu-id="d9bbc-106">This guide will show you how tooperform common scenarios using hello Azure Queue storage service.</span></span> <span data-ttu-id="d9bbc-107">exemplos de saudação são escritos em C++ e usam Olá [biblioteca de cliente de armazenamento do Azure para C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="d9bbc-107">hello samples are written in C++ and use hello [Azure Storage Client Library for C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span></span> <span data-ttu-id="d9bbc-108">Olá cenários abordados incluem **inserindo**, **inspecionar**, **obtendo**, e **excluindo** Enfileirar mensagens, bem como  **criar e excluir filas**.</span><span class="sxs-lookup"><span data-stu-id="d9bbc-108">hello scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating and deleting queues**.</span></span>

> [!NOTE]
> <span data-ttu-id="d9bbc-109">Destino dessa guia Olá biblioteca de cliente de armazenamento do Azure para a versão 1.0.0 de C++ e acima.</span><span class="sxs-lookup"><span data-stu-id="d9bbc-109">This guide targets hello Azure Storage Client Library for C++ version 1.0.0 and above.</span></span> <span data-ttu-id="d9bbc-110">Olá recomendado versão é a biblioteca de cliente de armazenamento 2.2.0, que está disponível por meio de [NuGet](http://www.nuget.org/packages/wastorage) ou [GitHub](http://github.com/Azure/azure-storage-cpp/).</span><span class="sxs-lookup"><span data-stu-id="d9bbc-110">hello recommended version is Storage Client Library 2.2.0, which is available via [NuGet](http://www.nuget.org/packages/wastorage) or [GitHub](http://github.com/Azure/azure-storage-cpp/).</span></span>
> 
> 

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-c-application"></a><span data-ttu-id="d9bbc-111">Criar um aplicativo em C++</span><span class="sxs-lookup"><span data-stu-id="d9bbc-111">Create a C++ application</span></span>
<span data-ttu-id="d9bbc-112">Neste guia, você usará os recursos de armazenamento que podem ser executados em um aplicativo C++.</span><span class="sxs-lookup"><span data-stu-id="d9bbc-112">In this guide, you will use storage features which can be run within a C++ application.</span></span>

<span data-ttu-id="d9bbc-113">toodo assim, você precisará tooinstall hello biblioteca de cliente de armazenamento do Azure para C++ e criar uma conta de armazenamento do Azure em sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="d9bbc-113">toodo so, you will need tooinstall hello Azure Storage Client Library for C++ and create an Azure storage account in your Azure subscription.</span></span>

<span data-ttu-id="d9bbc-114">Olá tooinstall biblioteca de cliente de armazenamento do Azure para C++, você pode usar o hello métodos a seguir:</span><span class="sxs-lookup"><span data-stu-id="d9bbc-114">tooinstall hello Azure Storage Client Library for C++, you can use hello following methods:</span></span>

* <span data-ttu-id="d9bbc-115">**Linux:** siga instruções Olá fornecidas em Olá [biblioteca de cliente de armazenamento do Azure para C++ Leiame](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) página.</span><span class="sxs-lookup"><span data-stu-id="d9bbc-115">**Linux:** Follow hello instructions given in hello [Azure Storage Client Library for C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) page.</span></span>
* <span data-ttu-id="d9bbc-116">**Windows:** no Visual Studio, clique em **Ferramentas > Gerenciador de Pacotes do NuGet > Console do Gerenciador de Pacotes**.</span><span class="sxs-lookup"><span data-stu-id="d9bbc-116">**Windows:** In Visual Studio, click **Tools > NuGet Package Manager > Package Manager Console**.</span></span> <span data-ttu-id="d9bbc-117">Digite o seguinte Olá comando em Olá [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) e pressione **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="d9bbc-117">Type hello following command into hello [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) and press **ENTER**.</span></span>

```  
Install-Package wastorage
```

## <a name="configure-your-application-tooaccess-queue-storage"></a><span data-ttu-id="d9bbc-118">Configurar seu aplicativo tooaccess armazenamento de fila</span><span class="sxs-lookup"><span data-stu-id="d9bbc-118">Configure your application tooaccess Queue Storage</span></span>
<span data-ttu-id="d9bbc-119">Adicione a seguinte Olá incluem superior de toohello de instruções do arquivo de C++ de saudação onde você deseja que as filas de tooaccess APIs de armazenamento do Azure Olá toouse:</span><span class="sxs-lookup"><span data-stu-id="d9bbc-119">Add hello following include statements toohello top of hello C++ file where you want toouse hello Azure storage APIs tooaccess queues:</span></span>  

```cpp
#include <was/storage_account.h>
#include <was/queue.h>
```

## <a name="set-up-an-azure-storage-connection-string"></a><span data-ttu-id="d9bbc-120">Configurar uma cadeia de conexão de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="d9bbc-120">Set up an Azure storage connection string</span></span>
<span data-ttu-id="d9bbc-121">Um cliente de armazenamento do Azure usa um pontos de extremidade de toostore de cadeia de caracteres de conexão de armazenamento e as credenciais para acessar os serviços de gerenciamento de dados.</span><span class="sxs-lookup"><span data-stu-id="d9bbc-121">An Azure storage client uses a storage connection string toostore endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="d9bbc-122">Quando em execução em um aplicativo cliente, você deve fornecer a cadeia de conexão de armazenamento Olá no hello formato a seguir, usando o nome de saudação da chave de acesso do armazenamento seu armazenamento conta e Olá Olá conta de armazenamento listada no hello [Portal do Azure](https://portal.azure.com)para Olá *AccountName* e *AccountKey* valores.</span><span class="sxs-lookup"><span data-stu-id="d9bbc-122">When running in a client application, you must provide hello storage connection string in hello following format, using hello name of your storage account and hello storage access key for hello storage account listed in hello [Azure Portal](https://portal.azure.com) for hello *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="d9bbc-123">Para obter informações sobre as contas de armazenamento e as chaves de acesso, consulte [Sobre as Contas de Armazenamento do Azure](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d9bbc-123">For information on storage accounts and access keys, see [About Azure Storage Accounts](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json).</span></span> <span data-ttu-id="d9bbc-124">Este exemplo mostra como você pode declarar uma cadeia de caracteres de conexão do campo estático toohold hello:</span><span class="sxs-lookup"><span data-stu-id="d9bbc-124">This example shows how you can declare a static field toohold hello connection string:</span></span>  

```cpp
// Define hello connection-string with your values.
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

<span data-ttu-id="d9bbc-125">tootest seu aplicativo no seu computador local do Windows, você pode usar o hello Microsoft Azure [emulador de armazenamento](../common/storage-use-emulator.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json) que é instalada com hello [SDK do Azure](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="d9bbc-125">tootest your application in your local Windows computer, you can use hello Microsoft Azure [storage emulator](../common/storage-use-emulator.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json) that is installed with hello [Azure SDK](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="d9bbc-126">emulador de armazenamento Olá é um utilitário que simula os serviços de Blob, fila e tabela de saudação disponíveis no Azure em sua máquina de desenvolvimento local.</span><span class="sxs-lookup"><span data-stu-id="d9bbc-126">hello storage emulator is a utility that simulates hello Blob, Queue, and Table services available in Azure on your local development machine.</span></span> <span data-ttu-id="d9bbc-127">Olá exemplo a seguir mostra como você pode declarar um emulador de armazenamento local do campo estático toohold Olá cadeia de caracteres conexão tooyour:</span><span class="sxs-lookup"><span data-stu-id="d9bbc-127">hello following example shows how you can declare a static field toohold hello connection string tooyour local storage emulator:</span></span>  

```cpp
// Define hello connection-string with Azure Storage Emulator.
const utility::string_t storage_connection_string(U("UseDevelopmentStorage=true;"));  
```

<span data-ttu-id="d9bbc-128">emulador de armazenamento do Azure toostart hello, selecione Olá **iniciar** Olá botão ou pressione **Windows** chave.</span><span class="sxs-lookup"><span data-stu-id="d9bbc-128">toostart hello Azure storage emulator, select hello **Start** button or press hello **Windows** key.</span></span> <span data-ttu-id="d9bbc-129">Comece digitando **emulador de armazenamento do Azure**e selecione **emulador de armazenamento do Microsoft Azure** da lista de saudação de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="d9bbc-129">Begin typing **Azure Storage Emulator**, and select **Microsoft Azure Storage Emulator** from hello list of applications.</span></span>

<span data-ttu-id="d9bbc-130">Olá exemplos a seguir pressupõem que você usou uma cadeia de conexão de armazenamento esses dois métodos tooget hello.</span><span class="sxs-lookup"><span data-stu-id="d9bbc-130">hello following samples assume that you have used one of these two methods tooget hello storage connection string.</span></span>

## <a name="retrieve-your-connection-string"></a><span data-ttu-id="d9bbc-131">Recuperar sua cadeia de conexão</span><span class="sxs-lookup"><span data-stu-id="d9bbc-131">Retrieve your connection string</span></span>
<span data-ttu-id="d9bbc-132">Você pode usar o hello **cloud_storage_account** classe toorepresent suas informações de conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="d9bbc-132">You can use hello **cloud_storage_account** class toorepresent your Storage Account information.</span></span> <span data-ttu-id="d9bbc-133">tooretrieve informações de cadeia de caracteres de conexão de armazenamento Olá da conta de armazenamento, você pode usar o hello **analisar** método.</span><span class="sxs-lookup"><span data-stu-id="d9bbc-133">tooretrieve your storage account information from hello storage connection string, you can use hello **parse** method.</span></span>

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);
```

## <a name="how-to-create-a-queue"></a><span data-ttu-id="d9bbc-134">Como criar uma fila</span><span class="sxs-lookup"><span data-stu-id="d9bbc-134">How to: Create a queue</span></span>
<span data-ttu-id="d9bbc-135">Um objeto **cloud_queue_client** permite que você obtenha objetos de referência para as filas.</span><span class="sxs-lookup"><span data-stu-id="d9bbc-135">A **cloud_queue_client** object lets you get reference objects for queues.</span></span> <span data-ttu-id="d9bbc-136">Olá código a seguir cria um **cloud_queue_client** objeto.</span><span class="sxs-lookup"><span data-stu-id="d9bbc-136">hello following code creates a **cloud_queue_client** object.</span></span>

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create a queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();
```

<span data-ttu-id="d9bbc-137">Saudação de uso **cloud_queue_client** tooget uma fila de toohello de referência que você deseja toouse do objeto.</span><span class="sxs-lookup"><span data-stu-id="d9bbc-137">Use hello **cloud_queue_client** object tooget a reference toohello queue you want toouse.</span></span> <span data-ttu-id="d9bbc-138">Você pode criar a fila de saudação se ele não existir.</span><span class="sxs-lookup"><span data-stu-id="d9bbc-138">You can create hello queue if it doesn't exist.</span></span>

```cpp
// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Create hello queue if it doesn't already exist.
 queue.create_if_not_exists();  
```

## <a name="how-to-insert-a-message-into-a-queue"></a><span data-ttu-id="d9bbc-139">Como inserir uma mensagem em uma fila</span><span class="sxs-lookup"><span data-stu-id="d9bbc-139">How to: Insert a message into a queue</span></span>
<span data-ttu-id="d9bbc-140">tooinsert uma mensagem em uma fila existente, primeiro crie um novo **cloud_queue_message**.</span><span class="sxs-lookup"><span data-stu-id="d9bbc-140">tooinsert a message into an existing queue, first create a new **cloud_queue_message**.</span></span> <span data-ttu-id="d9bbc-141">Em seguida, chame Olá **add_message** método.</span><span class="sxs-lookup"><span data-stu-id="d9bbc-141">Next, call hello **add_message** method.</span></span> <span data-ttu-id="d9bbc-142">Uma **cloud_queue_message** pode ser criada a partir de uma cadeia de caracteres ou de uma matriz de **bytes**.</span><span class="sxs-lookup"><span data-stu-id="d9bbc-142">A **cloud_queue_message** can be created from either a string or a **byte** array.</span></span> <span data-ttu-id="d9bbc-143">Aqui está o código que cria uma fila (se não existir) e a mensagem de saudação inserções 'Hello, World':</span><span class="sxs-lookup"><span data-stu-id="d9bbc-143">Here is code which creates a queue (if it doesn't exist) and inserts hello message 'Hello, World':</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Create hello queue if it doesn't already exist.
queue.create_if_not_exists();

// Create a message and add it toohello queue.
azure::storage::cloud_queue_message message1(U("Hello, World"));
queue.add_message(message1);  
```

## <a name="how-to-peek-at-hello-next-message"></a><span data-ttu-id="d9bbc-144">Como: espiar a próxima mensagem de saudação</span><span class="sxs-lookup"><span data-stu-id="d9bbc-144">How to: Peek at hello next message</span></span>
<span data-ttu-id="d9bbc-145">Você pode inspecionar mensagem de saudação na frente de saudação de uma fila sem removê-la da fila de saudação por chamada hello **peek_message** método.</span><span class="sxs-lookup"><span data-stu-id="d9bbc-145">You can peek at hello message in hello front of a queue without removing it from hello queue by calling hello **peek_message** method.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Peek at hello next message.
azure::storage::cloud_queue_message peeked_message = queue.peek_message();

// Output hello message content.
std::wcout << U("Peeked message content: ") << peeked_message.content_as_string() << std::endl;
```

## <a name="how-to-change-hello-contents-of-a-queued-message"></a><span data-ttu-id="d9bbc-146">Como: alterar o conteúdo de saudação de uma mensagem na fila</span><span class="sxs-lookup"><span data-stu-id="d9bbc-146">How to: Change hello contents of a queued message</span></span>
<span data-ttu-id="d9bbc-147">Você pode alterar o conteúdo de saudação de um mensagem no local na fila de saudação.</span><span class="sxs-lookup"><span data-stu-id="d9bbc-147">You can change hello contents of a message in-place in hello queue.</span></span> <span data-ttu-id="d9bbc-148">Se a mensagem de saudação representa uma tarefa de trabalho, você pode usar esse status do recurso tooupdate Olá da tarefa de trabalho hello.</span><span class="sxs-lookup"><span data-stu-id="d9bbc-148">If hello message represents a work task, you could use this feature tooupdate hello status of hello work task.</span></span> <span data-ttu-id="d9bbc-149">saudação de código a seguir atualiza a mensagem da fila de saudação com novo conteúdo e conjuntos Olá tooextend de tempo limite de visibilidade outro 60 segundos.</span><span class="sxs-lookup"><span data-stu-id="d9bbc-149">hello following code updates hello queue message with new contents, and sets hello visibility timeout tooextend another 60 seconds.</span></span> <span data-ttu-id="d9bbc-150">Isso salva o estado de saudação do trabalho associado à mensagem de saudação e fornece cliente Olá outro toocontinue minuto trabalhando na mensagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="d9bbc-150">This saves hello state of work associated with hello message, and gives hello client another minute toocontinue working on hello message.</span></span> <span data-ttu-id="d9bbc-151">Você pode usar esta técnica tootrack várias etapas os fluxos de trabalho na fila de mensagens, sem ter que toostart através do hello início se uma etapa de processamento falhar devido a falha de toohardware ou software.</span><span class="sxs-lookup"><span data-stu-id="d9bbc-151">You could use this technique tootrack multi-step workflows on queue messages, without having toostart over from hello beginning if a processing step fails due toohardware or software failure.</span></span> <span data-ttu-id="d9bbc-152">Normalmente, você mantém uma contagem de tentativa e se a mensagem de saudação é repetida mais de n vezes, você deve excluí-lo.</span><span class="sxs-lookup"><span data-stu-id="d9bbc-152">Typically, you would keep a retry count as well, and if hello message is retried more than n times, you would delete it.</span></span> <span data-ttu-id="d9bbc-153">Isso protege contra uma mensagem que dispara um erro do aplicativo sempre que for processada.</span><span class="sxs-lookup"><span data-stu-id="d9bbc-153">This protects against a message that triggers an application error each time it is processed.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_conection_string);

// Create hello queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Get hello message from hello queue and update hello message contents.
// hello visibility timeout "0" means make it visible immediately.
// hello visibility timeout "60" means hello client can get another minute toocontinue
// working on hello message.
azure::storage::cloud_queue_message changed_message = queue.get_message();

changed_message.set_content(U("Changed message"));
queue.update_message(changed_message, std::chrono::seconds(60), true);

// Output hello message content.
std::wcout << U("Changed message content: ") << changed_message.content_as_string() << std::endl;  
```

## <a name="how-to-de-queue-hello-next-message"></a><span data-ttu-id="d9bbc-154">Como: eliminação da fila de mensagem de saudação do próxima</span><span class="sxs-lookup"><span data-stu-id="d9bbc-154">How to: De-queue hello next message</span></span>
<span data-ttu-id="d9bbc-155">Seu código remove uma mensagem de um fila em duas etapas.</span><span class="sxs-lookup"><span data-stu-id="d9bbc-155">Your code de-queues a message from a queue in two steps.</span></span> <span data-ttu-id="d9bbc-156">Quando você chama **get_message**, obter próxima mensagem de saudação em uma fila.</span><span class="sxs-lookup"><span data-stu-id="d9bbc-156">When you call **get_message**, you get hello next message in a queue.</span></span> <span data-ttu-id="d9bbc-157">Uma mensagem retornada de **get_message** se torna invisível tooany outro código de leitura de mensagens dessa fila.</span><span class="sxs-lookup"><span data-stu-id="d9bbc-157">A message returned from **get_message** becomes invisible tooany other code reading messages from this queue.</span></span> <span data-ttu-id="d9bbc-158">toofinish mensagem de saudação remover da fila hello, você também deve chamar **delete_message**.</span><span class="sxs-lookup"><span data-stu-id="d9bbc-158">toofinish removing hello message from hello queue, you must also call **delete_message**.</span></span> <span data-ttu-id="d9bbc-159">Esse processo de duas etapas de remoção de uma mensagem garante que se seu código falha tooprocess que uma mensagem devido a falha de toohardware ou software, outra instância do seu código pode obter Olá a mesma mensagem e tente novamente.</span><span class="sxs-lookup"><span data-stu-id="d9bbc-159">This two-step process of removing a message assures that if your code fails tooprocess a message due toohardware or software failure, another instance of your code can get hello same message and try again.</span></span> <span data-ttu-id="d9bbc-160">Seu código chama **delete_message** logo depois que a mensagem de saudação foi processada.</span><span class="sxs-lookup"><span data-stu-id="d9bbc-160">Your code calls **delete_message** right after hello message has been processed.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Get hello next message.
azure::storage::cloud_queue_message dequeued_message = queue.get_message();
std::wcout << U("Dequeued message: ") << dequeued_message.content_as_string() << std::endl;

// Delete hello message.
queue.delete_message(dequeued_message);
```

## <a name="how-to-leverage-additional-options-for-de-queuing-messages"></a><span data-ttu-id="d9bbc-161">Como: aproveitar as opções adicionais para remover mensagens da fila</span><span class="sxs-lookup"><span data-stu-id="d9bbc-161">How to: Leverage additional options for de-queuing messages</span></span>
<span data-ttu-id="d9bbc-162">Há duas maneiras de personalizar a recuperação da mensagem de uma fila.</span><span class="sxs-lookup"><span data-stu-id="d9bbc-162">There are two ways you can customize message retrieval from a queue.</span></span> <span data-ttu-id="d9bbc-163">Primeiro, você pode obter um lote de mensagens (até too32).</span><span class="sxs-lookup"><span data-stu-id="d9bbc-163">First, you can get a batch of messages (up too32).</span></span> <span data-ttu-id="d9bbc-164">Em seguida, você pode definir um tempo limite de invisibilidade maiores ou menores, permitindo que o código mais ou menos tempo toofully processam cada mensagem.</span><span class="sxs-lookup"><span data-stu-id="d9bbc-164">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time toofully process each message.</span></span> <span data-ttu-id="d9bbc-165">Olá, exemplo de código a seguir usa Olá **get_messages** mensagens tooget 20 de método em uma chamada.</span><span class="sxs-lookup"><span data-stu-id="d9bbc-165">hello following code example uses hello **get_messages** method tooget 20 messages in one call.</span></span> <span data-ttu-id="d9bbc-166">Em seguida, ele processa cada mensagem usando um loop **for** .</span><span class="sxs-lookup"><span data-stu-id="d9bbc-166">Then it processes each message using a **for** loop.</span></span> <span data-ttu-id="d9bbc-167">Ele também define minutos de toofive de tempo limite de invisibilidade de saudação para cada mensagem.</span><span class="sxs-lookup"><span data-stu-id="d9bbc-167">It also sets hello invisibility timeout toofive minutes for each message.</span></span> <span data-ttu-id="d9bbc-168">Observe que Olá 5 minutos é iniciado para todas as mensagens com hello a mesma hora, após 5 minutos se passaram desde chamada hello muito**get_messages**, qualquer mensagem que não foram excluídas se tornará visível novamente.</span><span class="sxs-lookup"><span data-stu-id="d9bbc-168">Note that hello 5 minutes starts for all messages at hello same time, so after 5 minutes have passed since hello call too**get_messages**, any messages which have not been deleted will become visible again.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Dequeue some queue messages (maximum 32 at a time) and set their visibility timeout to
// 5 minutes (300 seconds).
azure::storage::queue_request_options options;
azure::storage::operation_context context;

// Retrieve 20 messages from hello queue with a visibility timeout of 300 seconds.
std::vector<azure::storage::cloud_queue_message> messages = queue.get_messages(20, std::chrono::seconds(300), options, context);

for (auto it = messages.cbegin(); it != messages.cend(); ++it)
{
    // Display hello contents of hello message.
    std::wcout << U("Get: ") << it->content_as_string() << std::endl;
}
```

## <a name="how-to-get-hello-queue-length"></a><span data-ttu-id="d9bbc-169">Como: obter o comprimento da fila de saudação</span><span class="sxs-lookup"><span data-stu-id="d9bbc-169">How to: Get hello queue length</span></span>
<span data-ttu-id="d9bbc-170">Você pode obter uma estimativa do número de saudação de mensagens em uma fila.</span><span class="sxs-lookup"><span data-stu-id="d9bbc-170">You can get an estimate of hello number of messages in a queue.</span></span> <span data-ttu-id="d9bbc-171">Olá **download_attributes** método solicita tooretrieve de serviço de fila Olá atributos da fila hello, incluindo o número de mensagens de saudação.</span><span class="sxs-lookup"><span data-stu-id="d9bbc-171">hello **download_attributes** method asks hello Queue service tooretrieve hello queue attributes, including hello message count.</span></span> <span data-ttu-id="d9bbc-172">Olá **approximate_message_count** método obtém o número aproximado de saudação de mensagens na fila de saudação.</span><span class="sxs-lookup"><span data-stu-id="d9bbc-172">hello **approximate_message_count** method gets hello approximate number of messages in hello queue.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Fetch hello queue attributes.
queue.download_attributes();

// Retrieve hello cached approximate message count.
int cachedMessageCount = queue.approximate_message_count();

// Display number of messages.
std::wcout << U("Number of messages in queue: ") << cachedMessageCount << std::endl;  
```

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="d9bbc-173">Como excluir uma fila</span><span class="sxs-lookup"><span data-stu-id="d9bbc-173">How to: Delete a queue</span></span>
<span data-ttu-id="d9bbc-174">toodelete uma fila e todas as mensagens de saudação contidas nele, chamada hello **delete_queue_if_exists** método no objeto de fila de saudação.</span><span class="sxs-lookup"><span data-stu-id="d9bbc-174">toodelete a queue and all hello messages contained in it, call hello **delete_queue_if_exists** method on hello queue object.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// If hello queue exists and delete it.
queue.delete_queue_if_exists();  
```

## <a name="next-steps"></a><span data-ttu-id="d9bbc-175">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d9bbc-175">Next steps</span></span>
<span data-ttu-id="d9bbc-176">Agora que você aprendeu as Noções básicas de saudação do armazenamento de fila, siga essas toolearn links mais sobre o armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="d9bbc-176">Now that you've learned hello basics of Queue storage, follow these links toolearn more about Azure Storage.</span></span>

* [<span data-ttu-id="d9bbc-177">Como toouse armazenamento de Blob de C++</span><span class="sxs-lookup"><span data-stu-id="d9bbc-177">How toouse Blob Storage from C++</span></span>](../blobs/storage-c-plus-plus-how-to-use-blobs.md)
* [<span data-ttu-id="d9bbc-178">Como toouse o armazenamento de tabela do C++</span><span class="sxs-lookup"><span data-stu-id="d9bbc-178">How toouse Table Storage from C++</span></span>](../../cosmos-db/table-storage-how-to-use-c-plus.md)
* [<span data-ttu-id="d9bbc-179">Listar recursos de Armazenamento do Azure em C++</span><span class="sxs-lookup"><span data-stu-id="d9bbc-179">List Azure Storage Resources in C++</span></span>](../common/storage-c-plus-plus-enumeration.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json)
* [<span data-ttu-id="d9bbc-180">Referência da Biblioteca de Cliente de Armazenamento para C++</span><span class="sxs-lookup"><span data-stu-id="d9bbc-180">Storage Client Library for C++ Reference</span></span>](http://azure.github.io/azure-storage-cpp)
* [<span data-ttu-id="d9bbc-181">Documentação do Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="d9bbc-181">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)