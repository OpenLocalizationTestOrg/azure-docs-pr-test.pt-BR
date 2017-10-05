---
title: Como usar o armazenamento de filas (C++) | Microsoft Docs
description: "Saiba como usar o serviço de armazenamento de filas no Azure. As amostras são escritas em C++."
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
ms.openlocfilehash: 85e4d95549ca5edd375f3b15971634e032a3962a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-queue-storage-from-c"></a><span data-ttu-id="715d0-104">Como usar o armazenamento de filas do C++</span><span class="sxs-lookup"><span data-stu-id="715d0-104">How to use Queue Storage from C++</span></span>
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="715d0-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="715d0-105">Overview</span></span>
<span data-ttu-id="715d0-106">Este guia irá lhe mostrar como executar cenários comuns usando o armazenamento de fila do Azure.</span><span class="sxs-lookup"><span data-stu-id="715d0-106">This guide will show you how to perform common scenarios using the Azure Queue storage service.</span></span> <span data-ttu-id="715d0-107">Os exemplos são escritos em C++ e usam a [Biblioteca do Cliente de Armazenamento do Azure para C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="715d0-107">The samples are written in C++ and use the [Azure Storage Client Library for C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span></span> <span data-ttu-id="715d0-108">Os cenários abrangidos incluem **inserir**, **exibir**, **obter** e **excluir** mensagens da fila, bem como **criar e excluir filas**.</span><span class="sxs-lookup"><span data-stu-id="715d0-108">The scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating and deleting queues**.</span></span>

> [!NOTE]
> <span data-ttu-id="715d0-109">Este guia tem como alvo a Biblioteca do Cliente de Armazenamento do Azure para C++, versão 1.0.0 e superior.</span><span class="sxs-lookup"><span data-stu-id="715d0-109">This guide targets the Azure Storage Client Library for C++ version 1.0.0 and above.</span></span> <span data-ttu-id="715d0-110">A versão recomendada é a Biblioteca de Clientes de Armazenamento 2.2.0, que está disponível via [NuGet](http://www.nuget.org/packages/wastorage) ou [GitHub](http://github.com/Azure/azure-storage-cpp/).</span><span class="sxs-lookup"><span data-stu-id="715d0-110">The recommended version is Storage Client Library 2.2.0, which is available via [NuGet](http://www.nuget.org/packages/wastorage) or [GitHub](http://github.com/Azure/azure-storage-cpp/).</span></span>
> 
> 

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-c-application"></a><span data-ttu-id="715d0-111">Criar um aplicativo em C++</span><span class="sxs-lookup"><span data-stu-id="715d0-111">Create a C++ application</span></span>
<span data-ttu-id="715d0-112">Neste guia, você usará os recursos de armazenamento que podem ser executados em um aplicativo C++.</span><span class="sxs-lookup"><span data-stu-id="715d0-112">In this guide, you will use storage features which can be run within a C++ application.</span></span>

<span data-ttu-id="715d0-113">Para isso, você precisará instalar a Biblioteca do Cliente de Armazenamento do Azure para C++ e criar uma conta de armazenamento do Azure em sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="715d0-113">To do so, you will need to install the Azure Storage Client Library for C++ and create an Azure storage account in your Azure subscription.</span></span>

<span data-ttu-id="715d0-114">Para instalar a Biblioteca do Cliente de Armazenamento do Azure para C++, você pode usar os seguintes métodos:</span><span class="sxs-lookup"><span data-stu-id="715d0-114">To install the Azure Storage Client Library for C++, you can use the following methods:</span></span>

* <span data-ttu-id="715d0-115">**Linux:** siga as instruções dadas na página README da [Biblioteca do Cliente de Armazenamento do Azure para C++](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) .</span><span class="sxs-lookup"><span data-stu-id="715d0-115">**Linux:** Follow the instructions given in the [Azure Storage Client Library for C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) page.</span></span>
* <span data-ttu-id="715d0-116">**Windows:** no Visual Studio, clique em **Ferramentas > Gerenciador de Pacotes do NuGet > Console do Gerenciador de Pacotes**.</span><span class="sxs-lookup"><span data-stu-id="715d0-116">**Windows:** In Visual Studio, click **Tools > NuGet Package Manager > Package Manager Console**.</span></span> <span data-ttu-id="715d0-117">Digite o seguinte comando no console do [Gerenciador de Pacotes do NuGet](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) e pressione **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="715d0-117">Type the following command into the [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) and press **ENTER**.</span></span>

```  
Install-Package wastorage
```

## <a name="configure-your-application-to-access-queue-storage"></a><span data-ttu-id="715d0-118">Configurar seu aplicativo para acessar o Armazenamento de Filas</span><span class="sxs-lookup"><span data-stu-id="715d0-118">Configure your application to access Queue Storage</span></span>
<span data-ttu-id="715d0-119">Adicione as seguintes instruções include à parte superior do arquivo C++ no qual deseja usar as APIs de armazenamento do Azure para acessar as filas:</span><span class="sxs-lookup"><span data-stu-id="715d0-119">Add the following include statements to the top of the C++ file where you want to use the Azure storage APIs to access queues:</span></span>  

```cpp
#include <was/storage_account.h>
#include <was/queue.h>
```

## <a name="set-up-an-azure-storage-connection-string"></a><span data-ttu-id="715d0-120">Configurar uma cadeia de conexão de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="715d0-120">Set up an Azure storage connection string</span></span>
<span data-ttu-id="715d0-121">Um cliente de armazenamento do Azure usa uma cadeia de conexão para armazenar pontos de extremidade e credenciais para acessar serviços de gerenciamento de dados.</span><span class="sxs-lookup"><span data-stu-id="715d0-121">An Azure storage client uses a storage connection string to store endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="715d0-122">Ao ser executado em um aplicativo cliente, é necessário fornecer a cadeia de conexão de armazenamento no formato a seguir, usando o nome da sua conta de armazenamento e a chave de acesso de armazenamento da conta de armazenamento listada no [Portal do Azure](https://portal.azure.com) para os valores *AccountName* e *AccountKey*.</span><span class="sxs-lookup"><span data-stu-id="715d0-122">When running in a client application, you must provide the storage connection string in the following format, using the name of your storage account and the storage access key for the storage account listed in the [Azure Portal](https://portal.azure.com) for the *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="715d0-123">Para obter informações sobre as contas de armazenamento e as chaves de acesso, consulte [Sobre as Contas de Armazenamento do Azure](storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="715d0-123">For information on storage accounts and access keys, see [About Azure Storage Accounts](storage-create-storage-account.md).</span></span> <span data-ttu-id="715d0-124">Este exemplo mostra como você pode declarar um campo estático para armazenar a cadeia de conexão:</span><span class="sxs-lookup"><span data-stu-id="715d0-124">This example shows how you can declare a static field to hold the connection string:</span></span>  

```cpp
// Define the connection-string with your values.
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

<span data-ttu-id="715d0-125">Para testar seu aplicativo no computador local do Windows, você pode usar o emulador de armazenamento do [Microsoft Azure](storage-use-emulator.md) que é instalado com o [SDK do Azure](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="715d0-125">To test your application in your local Windows computer, you can use the Microsoft Azure [storage emulator](storage-use-emulator.md) that is installed with the [Azure SDK](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="715d0-126">O emulador de armazenamento é um utilitário que simula os serviços Blob, fila e tabela disponíveis no Azure em sua máquina de desenvolvimento local.</span><span class="sxs-lookup"><span data-stu-id="715d0-126">The storage emulator is a utility that simulates the Blob, Queue, and Table services available in Azure on your local development machine.</span></span> <span data-ttu-id="715d0-127">Este exemplo mostra como você pode declarar um campo estático para manter a cadeia de conexão em seu emulador de armazenamento local:</span><span class="sxs-lookup"><span data-stu-id="715d0-127">The following example shows how you can declare a static field to hold the connection string to your local storage emulator:</span></span>  

```cpp
// Define the connection-string with Azure Storage Emulator.
const utility::string_t storage_connection_string(U("UseDevelopmentStorage=true;"));  
```

<span data-ttu-id="715d0-128">Para iniciar o emulador de armazenamento do Azure, selecione o botão **Iniciar** ou pressione a tecla **Windows**.</span><span class="sxs-lookup"><span data-stu-id="715d0-128">To start the Azure storage emulator, select the **Start** button or press the **Windows** key.</span></span> <span data-ttu-id="715d0-129">Comece digitando **Emulador de Armazenamento do Azure** e selecione **Emulador de Armazenamento do Microsoft Azure** na lista de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="715d0-129">Begin typing **Azure Storage Emulator**, and select **Microsoft Azure Storage Emulator** from the list of applications.</span></span>

<span data-ttu-id="715d0-130">Os exemplos abaixo pressupõem que você usou um desses dois métodos para obter a cadeia de conexão do armazenamento.</span><span class="sxs-lookup"><span data-stu-id="715d0-130">The following samples assume that you have used one of these two methods to get the storage connection string.</span></span>

## <a name="retrieve-your-connection-string"></a><span data-ttu-id="715d0-131">Recuperar sua cadeia de conexão</span><span class="sxs-lookup"><span data-stu-id="715d0-131">Retrieve your connection string</span></span>
<span data-ttu-id="715d0-132">É possível usar a classe **cloud_storage_account** para representar as informações da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="715d0-132">You can use the **cloud_storage_account** class to represent your Storage Account information.</span></span> <span data-ttu-id="715d0-133">Para recuperar as informações da conta de armazenamento na cadeia de conexão de armazenamento, você pode usar o método **Analisar** .</span><span class="sxs-lookup"><span data-stu-id="715d0-133">To retrieve your storage account information from the storage connection string, you can use the **parse** method.</span></span>

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);
```

## <a name="how-to-create-a-queue"></a><span data-ttu-id="715d0-134">Como criar uma fila</span><span class="sxs-lookup"><span data-stu-id="715d0-134">How to: Create a queue</span></span>
<span data-ttu-id="715d0-135">Um objeto **cloud_queue_client** permite que você obtenha objetos de referência para as filas.</span><span class="sxs-lookup"><span data-stu-id="715d0-135">A **cloud_queue_client** object lets you get reference objects for queues.</span></span> <span data-ttu-id="715d0-136">O código a seguir cria um objeto **cloud_queue_client**.</span><span class="sxs-lookup"><span data-stu-id="715d0-136">The following code creates a **cloud_queue_client** object.</span></span>

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create a queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();
```

<span data-ttu-id="715d0-137">Use o objeto **cloud_queue_client** para obter uma referência para a fila que você deseja usar.</span><span class="sxs-lookup"><span data-stu-id="715d0-137">Use the **cloud_queue_client** object to get a reference to the queue you want to use.</span></span> <span data-ttu-id="715d0-138">Você poderá criar a fila se ela não existir.</span><span class="sxs-lookup"><span data-stu-id="715d0-138">You can create the queue if it doesn't exist.</span></span>

```cpp
// Retrieve a reference to a queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Create the queue if it doesn't already exist.
 queue.create_if_not_exists();  
```

## <a name="how-to-insert-a-message-into-a-queue"></a><span data-ttu-id="715d0-139">Como inserir uma mensagem em uma fila</span><span class="sxs-lookup"><span data-stu-id="715d0-139">How to: Insert a message into a queue</span></span>
<span data-ttu-id="715d0-140">Para inserir uma mensagem em uma fila existente, primeiro crie uma nova **cloud_queue_message**.</span><span class="sxs-lookup"><span data-stu-id="715d0-140">To insert a message into an existing queue, first create a new **cloud_queue_message**.</span></span> <span data-ttu-id="715d0-141">Em seguida, chame o método **add_message**.</span><span class="sxs-lookup"><span data-stu-id="715d0-141">Next, call the **add_message** method.</span></span> <span data-ttu-id="715d0-142">Uma **cloud_queue_message** pode ser criada a partir de uma cadeia de caracteres ou de uma matriz de **bytes**.</span><span class="sxs-lookup"><span data-stu-id="715d0-142">A **cloud_queue_message** can be created from either a string or a **byte** array.</span></span> <span data-ttu-id="715d0-143">Este é o código que cria uma fila (se ela não existir) e insere a mensagem 'Hello, World':</span><span class="sxs-lookup"><span data-stu-id="715d0-143">Here is code which creates a queue (if it doesn't exist) and inserts the message 'Hello, World':</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference to a queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Create the queue if it doesn't already exist.
queue.create_if_not_exists();

// Create a message and add it to the queue.
azure::storage::cloud_queue_message message1(U("Hello, World"));
queue.add_message(message1);  
```

## <a name="how-to-peek-at-the-next-message"></a><span data-ttu-id="715d0-144">Como inspecionar a próxima mensagem</span><span class="sxs-lookup"><span data-stu-id="715d0-144">How to: Peek at the next message</span></span>
<span data-ttu-id="715d0-145">Você pode espiar a mensagem na frente de uma fila sem removê-la da fila chamando o método **peek_message**.</span><span class="sxs-lookup"><span data-stu-id="715d0-145">You can peek at the message in the front of a queue without removing it from the queue by calling the **peek_message** method.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference to a queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Peek at the next message.
azure::storage::cloud_queue_message peeked_message = queue.peek_message();

// Output the message content.
std::wcout << U("Peeked message content: ") << peeked_message.content_as_string() << std::endl;
```

## <a name="how-to-change-the-contents-of-a-queued-message"></a><span data-ttu-id="715d0-146">Como alterar o conteúdo de uma mensagem em fila</span><span class="sxs-lookup"><span data-stu-id="715d0-146">How to: Change the contents of a queued message</span></span>
<span data-ttu-id="715d0-147">Você pode alterar o conteúdo de uma mensagem in-loco na fila.</span><span class="sxs-lookup"><span data-stu-id="715d0-147">You can change the contents of a message in-place in the queue.</span></span> <span data-ttu-id="715d0-148">Se a mensagem representar uma tarefa de trabalho, você poderá usar esse recurso para atualizar o status da tarefa de trabalho.</span><span class="sxs-lookup"><span data-stu-id="715d0-148">If the message represents a work task, you could use this feature to update the status of the work task.</span></span> <span data-ttu-id="715d0-149">O código a seguir atualiza a mensagem da fila com novo conteúdo e define o tempo limite de visibilidade para estender mais 60 segundos.</span><span class="sxs-lookup"><span data-stu-id="715d0-149">The following code updates the queue message with new contents, and sets the visibility timeout to extend another 60 seconds.</span></span> <span data-ttu-id="715d0-150">Isso salva o estado do trabalho associado à mensagem e dá ao cliente mais um minuto para continuar trabalhando na mensagem.</span><span class="sxs-lookup"><span data-stu-id="715d0-150">This saves the state of work associated with the message, and gives the client another minute to continue working on the message.</span></span> <span data-ttu-id="715d0-151">Você pode usar essa técnica para acompanhar fluxos de trabalho de várias etapas em mensagens em fila, sem a necessidade de começar desde o início, caso uma etapa de processamento falhar devido a uma falha de hardware ou de software.</span><span class="sxs-lookup"><span data-stu-id="715d0-151">You could use this technique to track multi-step workflows on queue messages, without having to start over from the beginning if a processing step fails due to hardware or software failure.</span></span> <span data-ttu-id="715d0-152">Normalmente, você mantém uma contagem de repetições e, se a mensagem for repetida mais de n vezes, você a exclui.</span><span class="sxs-lookup"><span data-stu-id="715d0-152">Typically, you would keep a retry count as well, and if the message is retried more than n times, you would delete it.</span></span> <span data-ttu-id="715d0-153">Isso protege contra uma mensagem que dispara um erro do aplicativo sempre que for processada.</span><span class="sxs-lookup"><span data-stu-id="715d0-153">This protects against a message that triggers an application error each time it is processed.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_conection_string);

// Create the queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference to a queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Get the message from the queue and update the message contents.
// The visibility timeout "0" means make it visible immediately.
// The visibility timeout "60" means the client can get another minute to continue
// working on the message.
azure::storage::cloud_queue_message changed_message = queue.get_message();

changed_message.set_content(U("Changed message"));
queue.update_message(changed_message, std::chrono::seconds(60), true);

// Output the message content.
std::wcout << U("Changed message content: ") << changed_message.content_as_string() << std::endl;  
```

## <a name="how-to-de-queue-the-next-message"></a><span data-ttu-id="715d0-154">Como remover a próxima mensagem da fila</span><span class="sxs-lookup"><span data-stu-id="715d0-154">How to: De-queue the next message</span></span>
<span data-ttu-id="715d0-155">Seu código remove uma mensagem de um fila em duas etapas.</span><span class="sxs-lookup"><span data-stu-id="715d0-155">Your code de-queues a message from a queue in two steps.</span></span> <span data-ttu-id="715d0-156">Ao chamar **get_message**, você recebe a próxima mensagem em uma fila.</span><span class="sxs-lookup"><span data-stu-id="715d0-156">When you call **get_message**, you get the next message in a queue.</span></span> <span data-ttu-id="715d0-157">A mensagem retornada de **get_message** torna-se invisível para qualquer outro código que lê mensagens nessa fila.</span><span class="sxs-lookup"><span data-stu-id="715d0-157">A message returned from **get_message** becomes invisible to any other code reading messages from this queue.</span></span> <span data-ttu-id="715d0-158">Para concluir a remoção da mensagem da fila, chame também **delete_message**.</span><span class="sxs-lookup"><span data-stu-id="715d0-158">To finish removing the message from the queue, you must also call **delete_message**.</span></span> <span data-ttu-id="715d0-159">Este processo de duas etapas de remover uma mensagem garante que quando o código não processa uma mensagem devido à falhas de hardware ou de software, outra instância do seu código pode receber a mesma mensagem e tentar novamente.</span><span class="sxs-lookup"><span data-stu-id="715d0-159">This two-step process of removing a message assures that if your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="715d0-160">O código chama **delete_message** logo depois que a mensagem é processada.</span><span class="sxs-lookup"><span data-stu-id="715d0-160">Your code calls **delete_message** right after the message has been processed.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference to a queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Get the next message.
azure::storage::cloud_queue_message dequeued_message = queue.get_message();
std::wcout << U("Dequeued message: ") << dequeued_message.content_as_string() << std::endl;

// Delete the message.
queue.delete_message(dequeued_message);
```

## <a name="how-to-leverage-additional-options-for-de-queuing-messages"></a><span data-ttu-id="715d0-161">Como: aproveitar as opções adicionais para remover mensagens da fila</span><span class="sxs-lookup"><span data-stu-id="715d0-161">How to: Leverage additional options for de-queuing messages</span></span>
<span data-ttu-id="715d0-162">Há duas maneiras de personalizar a recuperação da mensagem de uma fila.</span><span class="sxs-lookup"><span data-stu-id="715d0-162">There are two ways you can customize message retrieval from a queue.</span></span> <span data-ttu-id="715d0-163">Primeiro, você pode obter um lote de mensagens (até 32).</span><span class="sxs-lookup"><span data-stu-id="715d0-163">First, you can get a batch of messages (up to 32).</span></span> <span data-ttu-id="715d0-164">Segundo, você pode definir um tempo limite de invisibilidade mais longo ou mais curto, permitindo mais ou menos tempo para seu código processar totalmente cada mensagem.</span><span class="sxs-lookup"><span data-stu-id="715d0-164">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time to fully process each message.</span></span> <span data-ttu-id="715d0-165">O exemplo de código a seguir usa o método **get_messages** para receber 20 mensagens em uma chamada.</span><span class="sxs-lookup"><span data-stu-id="715d0-165">The following code example uses the **get_messages** method to get 20 messages in one call.</span></span> <span data-ttu-id="715d0-166">Em seguida, ele processa cada mensagem usando um loop **for** .</span><span class="sxs-lookup"><span data-stu-id="715d0-166">Then it processes each message using a **for** loop.</span></span> <span data-ttu-id="715d0-167">Ele também define o tempo limite de invisibilidade de cinco minutos para cada mensagem.</span><span class="sxs-lookup"><span data-stu-id="715d0-167">It also sets the invisibility timeout to five minutes for each message.</span></span> <span data-ttu-id="715d0-168">Observe que os 5 minutos começam para todas as mensagens ao mesmo tempo; portanto, depois de 5 minutos desde a chamada para **get_messages**, qualquer mensagem não excluída ficará visível novamente.</span><span class="sxs-lookup"><span data-stu-id="715d0-168">Note that the 5 minutes starts for all messages at the same time, so after 5 minutes have passed since the call to **get_messages**, any messages which have not been deleted will become visible again.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference to a queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Dequeue some queue messages (maximum 32 at a time) and set their visibility timeout to
// 5 minutes (300 seconds).
azure::storage::queue_request_options options;
azure::storage::operation_context context;

// Retrieve 20 messages from the queue with a visibility timeout of 300 seconds.
std::vector<azure::storage::cloud_queue_message> messages = queue.get_messages(20, std::chrono::seconds(300), options, context);

for (auto it = messages.cbegin(); it != messages.cend(); ++it)
{
    // Display the contents of the message.
    std::wcout << U("Get: ") << it->content_as_string() << std::endl;
}
```

## <a name="how-to-get-the-queue-length"></a><span data-ttu-id="715d0-169">Como obter o comprimento da fila</span><span class="sxs-lookup"><span data-stu-id="715d0-169">How to: Get the queue length</span></span>
<span data-ttu-id="715d0-170">Você pode obter uma estimativa do número de mensagens em uma fila.</span><span class="sxs-lookup"><span data-stu-id="715d0-170">You can get an estimate of the number of messages in a queue.</span></span> <span data-ttu-id="715d0-171">O método **download_attributes** solicita que o serviço de fila recupere os atributos da fila, incluindo a contagem de mensagens.</span><span class="sxs-lookup"><span data-stu-id="715d0-171">The **download_attributes** method asks the Queue service to retrieve the queue attributes, including the message count.</span></span> <span data-ttu-id="715d0-172">O método **approximate_message_count** obtém o número aproximado de mensagens na fila.</span><span class="sxs-lookup"><span data-stu-id="715d0-172">The **approximate_message_count** method gets the approximate number of messages in the queue.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference to a queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Fetch the queue attributes.
queue.download_attributes();

// Retrieve the cached approximate message count.
int cachedMessageCount = queue.approximate_message_count();

// Display number of messages.
std::wcout << U("Number of messages in queue: ") << cachedMessageCount << std::endl;  
```

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="715d0-173">Como excluir uma fila</span><span class="sxs-lookup"><span data-stu-id="715d0-173">How to: Delete a queue</span></span>
<span data-ttu-id="715d0-174">Para excluir uma fila e todas as mensagens contidas nela, chame o método **delete_queue_if_exists** no objeto de fila.</span><span class="sxs-lookup"><span data-stu-id="715d0-174">To delete a queue and all the messages contained in it, call the **delete_queue_if_exists** method on the queue object.</span></span>

```cpp
// Retrieve storage account from connection-string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();

// Retrieve a reference to a queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// If the queue exists and delete it.
queue.delete_queue_if_exists();  
```

## <a name="next-steps"></a><span data-ttu-id="715d0-175">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="715d0-175">Next steps</span></span>
<span data-ttu-id="715d0-176">Agora que você aprendeu os conceitos básicos do armazenamento de filas, siga estes links para saber mais sobre o armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="715d0-176">Now that you've learned the basics of Queue storage, follow these links to learn more about Azure Storage.</span></span>

* [<span data-ttu-id="715d0-177">Como usar o Armazenamento de Blobs do C++</span><span class="sxs-lookup"><span data-stu-id="715d0-177">How to use Blob Storage from C++</span></span>](storage-c-plus-plus-how-to-use-blobs.md)
* [<span data-ttu-id="715d0-178">Como usar o Armazenamento de Tabelas do C++</span><span class="sxs-lookup"><span data-stu-id="715d0-178">How to use Table Storage from C++</span></span>](storage-c-plus-plus-how-to-use-tables.md)
* [<span data-ttu-id="715d0-179">Listar recursos de Armazenamento do Azure em C++</span><span class="sxs-lookup"><span data-stu-id="715d0-179">List Azure Storage Resources in C++</span></span>](storage-c-plus-plus-enumeration.md)
* [<span data-ttu-id="715d0-180">Referência da Biblioteca de Cliente de Armazenamento para C++</span><span class="sxs-lookup"><span data-stu-id="715d0-180">Storage Client Library for C++ Reference</span></span>](http://azure.github.io/azure-storage-cpp)
* [<span data-ttu-id="715d0-181">Documentação do Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="715d0-181">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)