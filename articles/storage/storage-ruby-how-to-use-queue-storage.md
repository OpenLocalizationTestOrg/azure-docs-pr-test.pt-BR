---
title: aaaHow toouse armazenamento de fila do Ruby | Microsoft Docs
description: "Saiba como toocreate de serviço de fila do Azure toouse hello e filas delete e insert, obtenham e excluir mensagens. Exemplos gravados no Ruby."
services: storage
documentationcenter: ruby
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 59c2d81b-db9c-46ee-ade2-2f0caae6b1e6
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: 726c7d2f08b2d5938ee5f9dcdc2735e447388856
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-ruby"></a><span data-ttu-id="9ac09-104">Como toouse armazenamento de fila do Ruby</span><span class="sxs-lookup"><span data-stu-id="9ac09-104">How toouse Queue storage from Ruby</span></span>
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="9ac09-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="9ac09-105">Overview</span></span>
<span data-ttu-id="9ac09-106">Este guia mostra como os cenários comuns de tooperform usando Olá serviço de armazenamento de fila do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="9ac09-106">This guide shows you how tooperform common scenarios using hello Microsoft Azure Queue Storage service.</span></span> <span data-ttu-id="9ac09-107">exemplos de saudação são gravados usando Olá Ruby a API do Azure.</span><span class="sxs-lookup"><span data-stu-id="9ac09-107">hello samples are written using hello Ruby Azure API.</span></span>
<span data-ttu-id="9ac09-108">Olá cenários abordados incluem **inserindo**, **inspecionar**, **obtendo**, e **excluindo** Enfileirar mensagens, bem como  **criar e excluir filas**.</span><span class="sxs-lookup"><span data-stu-id="9ac09-108">hello scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating and deleting queues**.</span></span>

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a><span data-ttu-id="9ac09-109">Criar um aplicativo Ruby</span><span class="sxs-lookup"><span data-stu-id="9ac09-109">Create a Ruby Application</span></span>
<span data-ttu-id="9ac09-110">Crie um aplicativo Ruby.</span><span class="sxs-lookup"><span data-stu-id="9ac09-110">Create a Ruby application.</span></span> <span data-ttu-id="9ac09-111">Para ver as instruções, confira [Aplicativo Web Ruby on Rails em uma VM do Azure](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="9ac09-111">For instructions, see [Ruby on Rails Web application on an Azure VM](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span></span>

## <a name="configure-your-application-tooaccess-storage"></a><span data-ttu-id="9ac09-112">Configurar seu aplicativo tooAccess armazenamento</span><span class="sxs-lookup"><span data-stu-id="9ac09-112">Configure Your Application tooAccess Storage</span></span>
<span data-ttu-id="9ac09-113">toouse armazenamento do Azure, você precisa toodownload e use Olá Ruby pacote do azure, que inclui um conjunto de bibliotecas de conveniência que se comunicam com serviços da REST do armazenamento hello.</span><span class="sxs-lookup"><span data-stu-id="9ac09-113">toouse Azure storage, you need toodownload and use hello Ruby azure package, which includes a set of convenience libraries that communicate with hello storage REST services.</span></span>

### <a name="use-rubygems-tooobtain-hello-package"></a><span data-ttu-id="9ac09-114">Use o pacote de saudação do RubyGems tooobtain</span><span class="sxs-lookup"><span data-stu-id="9ac09-114">Use RubyGems tooobtain hello package</span></span>
1. <span data-ttu-id="9ac09-115">Use uma interface de linha de comando como **PowerShell** (Windows), **Terminal** (Mac) ou **Bash** (Unix).</span><span class="sxs-lookup"><span data-stu-id="9ac09-115">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix).</span></span>
2. <span data-ttu-id="9ac09-116">Digite "gem instalar o azure" em gem de Olá Olá comando janela tooinstall e dependências.</span><span class="sxs-lookup"><span data-stu-id="9ac09-116">Type "gem install azure" in hello command window tooinstall hello gem and dependencies.</span></span>

### <a name="import-hello-package"></a><span data-ttu-id="9ac09-117">Importar o pacote de saudação</span><span class="sxs-lookup"><span data-stu-id="9ac09-117">Import hello package</span></span>
<span data-ttu-id="9ac09-118">Use o editor de texto favorito, adicione Olá toohello superior de saudação arquivo Ruby onde você pretende toouse armazenamento a seguir:</span><span class="sxs-lookup"><span data-stu-id="9ac09-118">Use your favorite text editor, add hello following toohello top of hello Ruby file where you intend toouse storage:</span></span>

```ruby
require "azure"
```

## <a name="setup-an-azure-storage-connection"></a><span data-ttu-id="9ac09-119">Configurar uma conexão de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="9ac09-119">Setup an Azure Storage Connection</span></span>
<span data-ttu-id="9ac09-120">módulo de saudação do azure lerá variáveis de ambiente Olá **AZURE\_armazenamento\_conta** e **AZURE\_armazenamento\_ACCESS_KEY** para as informações necessárias a conta de armazenamento do Azure tooyour tooconnect.</span><span class="sxs-lookup"><span data-stu-id="9ac09-120">hello azure module will read hello environment variables **AZURE\_STORAGE\_ACCOUNT** and **AZURE\_STORAGE\_ACCESS_KEY** for information required tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="9ac09-121">Se essas variáveis de ambiente não forem definidas, você deve especificar informações de conta de saudação antes de usar **Azure::QueueService** com hello código a seguir:</span><span class="sxs-lookup"><span data-stu-id="9ac09-121">If these environment variables are not set, you must specify hello account information before using **Azure::QueueService** with hello following code:</span></span>

```ruby
Azure.config.storage_account_name = "<your azure storage account>"
Azure.config.storage_access_key = "<your Azure storage access key>"
```

<span data-ttu-id="9ac09-122">tooobtain esses valores de um clássico ou Gerenciador de recursos de armazenamento de conta no hello portal do Azure:</span><span class="sxs-lookup"><span data-stu-id="9ac09-122">tooobtain these values from a classic or Resource Manager storage account in hello Azure portal:</span></span>

1. <span data-ttu-id="9ac09-123">Faça logon no toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9ac09-123">Log in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="9ac09-124">Navegue toohello conta de armazenamento que você deseja toouse.</span><span class="sxs-lookup"><span data-stu-id="9ac09-124">Navigate toohello storage account you want toouse.</span></span>
3. <span data-ttu-id="9ac09-125">Na folha de configurações de saudação em saudação à direita, clique em **chaves de acesso**.</span><span class="sxs-lookup"><span data-stu-id="9ac09-125">In hello Settings blade on hello right, click **Access Keys**.</span></span>
4. <span data-ttu-id="9ac09-126">Olá acesso folha de chaves que aparece, você verá a chave de acesso de saudação 1 e 2 de chave de acesso.</span><span class="sxs-lookup"><span data-stu-id="9ac09-126">In hello Access keys blade that appears, you'll see hello access key 1 and access key 2.</span></span> <span data-ttu-id="9ac09-127">Você pode usar qualquer uma das duas.</span><span class="sxs-lookup"><span data-stu-id="9ac09-127">You can use either of these.</span></span> 
5. <span data-ttu-id="9ac09-128">Clique em Olá copiar ícone toocopy Olá chave toohello área de transferência.</span><span class="sxs-lookup"><span data-stu-id="9ac09-128">Click hello copy icon toocopy hello key toohello clipboard.</span></span> 

<span data-ttu-id="9ac09-129">tooobtain esses valores de um armazenamento clássico contam no portal do Azure clássico de saudação:</span><span class="sxs-lookup"><span data-stu-id="9ac09-129">tooobtain these values from a classic storage account in hello classic Azure portal:</span></span>

1. <span data-ttu-id="9ac09-130">Faça logon no toohello [portal clássico do Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="9ac09-130">Log in toohello [classic Azure portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="9ac09-131">Navegue toohello conta de armazenamento que você deseja toouse.</span><span class="sxs-lookup"><span data-stu-id="9ac09-131">Navigate toohello storage account you want toouse.</span></span>
3. <span data-ttu-id="9ac09-132">Clique em **gerenciar chaves de acesso** na parte inferior de Olá Olá do painel de navegação.</span><span class="sxs-lookup"><span data-stu-id="9ac09-132">Click **MANAGE ACCESS KEYS** at hello bottom of hello navigation pane.</span></span>
4. <span data-ttu-id="9ac09-133">Olá pop-up da caixa de diálogo, você verá o nome de conta de armazenamento hello, chave de acesso primária e chave de acesso secundária.</span><span class="sxs-lookup"><span data-stu-id="9ac09-133">In hello pop up dialog, you'll see hello storage account name, primary access key and secondary access key.</span></span> <span data-ttu-id="9ac09-134">Para a chave de acesso, você pode usar Olá principal ou Olá um secundário.</span><span class="sxs-lookup"><span data-stu-id="9ac09-134">For access key, you can use either hello primary one or hello secondary one.</span></span> 
5. <span data-ttu-id="9ac09-135">Clique em Olá copiar ícone toocopy Olá chave toohello área de transferência.</span><span class="sxs-lookup"><span data-stu-id="9ac09-135">Click hello copy icon toocopy hello key toohello clipboard.</span></span>

## <a name="how-to-create-a-queue"></a><span data-ttu-id="9ac09-136">Como criar uma fila</span><span class="sxs-lookup"><span data-stu-id="9ac09-136">How To: Create a Queue</span></span>
<span data-ttu-id="9ac09-137">Olá código a seguir cria um **Azure::QueueService** objeto, que permite que você toowork com filas.</span><span class="sxs-lookup"><span data-stu-id="9ac09-137">hello following code creates a **Azure::QueueService** object, which enables you toowork with queues.</span></span>

```ruby
azure_queue_service = Azure::QueueService.new
```

<span data-ttu-id="9ac09-138">Saudação de uso **create_queue()** nome do método toocreate uma fila com hello especificado.</span><span class="sxs-lookup"><span data-stu-id="9ac09-138">Use hello **create_queue()** method toocreate a queue with hello specified name.</span></span>

```ruby
begin
  azure_queue_service.create_queue("test-queue")
rescue
  puts $!
end
```

## <a name="how-to-insert-a-message-into-a-queue"></a><span data-ttu-id="9ac09-139">Como inserir uma mensagem em uma fila</span><span class="sxs-lookup"><span data-stu-id="9ac09-139">How To: Insert a Message into a Queue</span></span>
<span data-ttu-id="9ac09-140">tooinsert uma mensagem em uma fila, use Olá **create_message()** método toocreate uma nova mensagem e adicioná-lo toohello fila.</span><span class="sxs-lookup"><span data-stu-id="9ac09-140">tooinsert a message into a queue, use hello **create_message()** method toocreate a new message and add it toohello queue.</span></span>

```ruby
azure_queue_service.create_message("test-queue", "test message")
```

## <a name="how-to-peek-at-hello-next-message"></a><span data-ttu-id="9ac09-141">Como: Espiar a próxima mensagem de saudação</span><span class="sxs-lookup"><span data-stu-id="9ac09-141">How To: Peek at hello Next Message</span></span>
<span data-ttu-id="9ac09-142">Você pode inspecionar mensagem de saudação na frente de saudação de uma fila sem removê-la da fila de saudação por chamada hello **inspeção\_messages()** método.</span><span class="sxs-lookup"><span data-stu-id="9ac09-142">You can peek at hello message in hello front of a queue without removing it from hello queue by calling hello **peek\_messages()** method.</span></span> <span data-ttu-id="9ac09-143">Por padrão, o **peek\_messages()** inspeciona uma única mensagem.</span><span class="sxs-lookup"><span data-stu-id="9ac09-143">By default, **peek\_messages()** peeks at a single message.</span></span> <span data-ttu-id="9ac09-144">Você também pode especificar quantas mensagens você deseja toopeek.</span><span class="sxs-lookup"><span data-stu-id="9ac09-144">You can also specify how many messages you want toopeek.</span></span>

```ruby
result = azure_queue_service.peek_messages("test-queue",
  {:number_of_messages => 10})
```

## <a name="how-to-dequeue-hello-next-message"></a><span data-ttu-id="9ac09-145">Como: Remover da fila Olá próxima mensagem</span><span class="sxs-lookup"><span data-stu-id="9ac09-145">How To: Dequeue hello Next Message</span></span>
<span data-ttu-id="9ac09-146">É possível remover uma mensagem da fila em duas etapas.</span><span class="sxs-lookup"><span data-stu-id="9ac09-146">You can remove a message from a queue in two steps.</span></span>

1. <span data-ttu-id="9ac09-147">Quando você chama **lista\_messages()**, obter próxima mensagem de saudação em uma fila por padrão.</span><span class="sxs-lookup"><span data-stu-id="9ac09-147">When you call **list\_messages()**, you get hello next message in a queue by default.</span></span> <span data-ttu-id="9ac09-148">Você também pode especificar quantas mensagens você deseja tooget.</span><span class="sxs-lookup"><span data-stu-id="9ac09-148">You can also specify how many messages you want tooget.</span></span> <span data-ttu-id="9ac09-149">Olá mensagens retornadas do **lista\_messages()** se torna invisível tooany outro código de leitura de mensagens dessa fila.</span><span class="sxs-lookup"><span data-stu-id="9ac09-149">hello messages returned from **list\_messages()** becomes invisible tooany other code reading messages from this queue.</span></span> <span data-ttu-id="9ac09-150">Você passa no tempo limite de visibilidade de saudação em segundos como um parâmetro.</span><span class="sxs-lookup"><span data-stu-id="9ac09-150">You pass in hello visibility timeout in seconds as a parameter.</span></span>
2. <span data-ttu-id="9ac09-151">toofinish mensagem de saudação remover da fila hello, você também deve chamar **delete_message()**.</span><span class="sxs-lookup"><span data-stu-id="9ac09-151">toofinish removing hello message from hello queue, you must also call **delete_message()**.</span></span>

<span data-ttu-id="9ac09-152">Esse processo de duas etapas de remoção de uma mensagem garante que, quando seu tooprocess de falha de código pode obter uma mensagem devido a falha de toohardware ou software, outra instância do seu código Olá mesma mensagem e tente novamente.</span><span class="sxs-lookup"><span data-stu-id="9ac09-152">This two-step process of removing a message assures that when your code fails tooprocess a message due toohardware or software failure, another instance of your code can get hello same message and try again.</span></span> <span data-ttu-id="9ac09-153">Seu código chama **excluir\_message()** logo depois que a mensagem de saudação foi processada.</span><span class="sxs-lookup"><span data-stu-id="9ac09-153">Your code calls **delete\_message()** right after hello message has been processed.</span></span>

```ruby
messages = azure_queue_service.list_messages("test-queue", 30)
azure_queue_service.delete_message("test-queue", 
  messages[0].id, messages[0].pop_receipt)
```

## <a name="how-to-change-hello-contents-of-a-queued-message"></a><span data-ttu-id="9ac09-154">Como: Alterar o conteúdo de saudação de uma mensagem na fila</span><span class="sxs-lookup"><span data-stu-id="9ac09-154">How To: Change hello Contents of a Queued Message</span></span>
<span data-ttu-id="9ac09-155">Você pode alterar o conteúdo de saudação de um mensagem no local na fila de saudação.</span><span class="sxs-lookup"><span data-stu-id="9ac09-155">You can change hello contents of a message in-place in hello queue.</span></span> <span data-ttu-id="9ac09-156">código de saudação abaixo usa Olá **update_message()** método tooupdate uma mensagem.</span><span class="sxs-lookup"><span data-stu-id="9ac09-156">hello code below uses hello **update_message()** method tooupdate a message.</span></span> <span data-ttu-id="9ac09-157">método Hello retornará uma tupla que contém a confirmação pop Olá de mensagem da fila de saudação e um valor de tempo de data UTC que representa quando a mensagem de saudação ficará visível na fila de saudação.</span><span class="sxs-lookup"><span data-stu-id="9ac09-157">hello method will return a tuple which contains hello pop receipt of hello queue message and a UTC date time value that represents when hello message will be visible on hello queue.</span></span>

```ruby
message = azure_queue_service.list_messages("test-queue", 30)
pop_receipt, time_next_visible = azure_queue_service.update_message(
  "test-queue", message.id, message.pop_receipt, "updated test message", 
  30)
```

## <a name="how-to-additional-options-for-dequeuing-messages"></a><span data-ttu-id="9ac09-158">Como adicionar opções para remover mensagens da fila</span><span class="sxs-lookup"><span data-stu-id="9ac09-158">How To: Additional Options for Dequeuing Messages</span></span>
<span data-ttu-id="9ac09-159">Há duas maneiras de personalizar a recuperação da mensagem de uma fila.</span><span class="sxs-lookup"><span data-stu-id="9ac09-159">There are two ways you can customize message retrieval from a queue.</span></span>

1. <span data-ttu-id="9ac09-160">Você pode obter um lote de mensagens.</span><span class="sxs-lookup"><span data-stu-id="9ac09-160">You can get a batch of message.</span></span>
2. <span data-ttu-id="9ac09-161">Você pode definir um tempo limite de invisibilidade maiores ou menores, permitindo que o código mais ou menos tempo toofully processam cada mensagem.</span><span class="sxs-lookup"><span data-stu-id="9ac09-161">You can set a longer or shorter invisibility timeout, allowing your code more or less time toofully process each message.</span></span>

<span data-ttu-id="9ac09-162">Olá, exemplo de código a seguir usa Olá **lista\_messages()** mensagens tooget 15 de método em uma chamada.</span><span class="sxs-lookup"><span data-stu-id="9ac09-162">hello following code example uses hello **list\_messages()** method tooget 15 messages in one call.</span></span> <span data-ttu-id="9ac09-163">Em seguida, ele lê e exclui cada mensagem.</span><span class="sxs-lookup"><span data-stu-id="9ac09-163">Then it prints and deletes each message.</span></span> <span data-ttu-id="9ac09-164">Ele também define minutos de toofive de tempo limite de invisibilidade de saudação para cada mensagem.</span><span class="sxs-lookup"><span data-stu-id="9ac09-164">It also sets hello invisibility timeout toofive minutes for each message.</span></span>

```ruby
azure_queue_service.list_messages("test-queue", 300
  {:number_of_messages => 15}).each do |m|
  puts m.message_text
  azure_queue_service.delete_message("test-queue", m.id, m.pop_receipt)
end
```

## <a name="how-to-get-hello-queue-length"></a><span data-ttu-id="9ac09-165">Como Obter Olá comprimento da fila</span><span class="sxs-lookup"><span data-stu-id="9ac09-165">How To: Get hello Queue Length</span></span>
<span data-ttu-id="9ac09-166">Você pode obter uma estimativa do número de saudação de mensagens na fila de saudação.</span><span class="sxs-lookup"><span data-stu-id="9ac09-166">You can get an estimation of hello number of messages in hello queue.</span></span> <span data-ttu-id="9ac09-167">Olá **obter\_fila\_metadata()** método faz a contagem de aproximada das mensagens de saudação Olá fila serviço tooreturn e metadados sobre fila hello.</span><span class="sxs-lookup"><span data-stu-id="9ac09-167">hello **get\_queue\_metadata()** method asks hello queue service tooreturn hello approximate message count and metadata about hello queue.</span></span>

```ruby
message_count, metadata = azure_queue_service.get_queue_metadata(
  "test-queue")
```

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="9ac09-168">Como excluir uma fila</span><span class="sxs-lookup"><span data-stu-id="9ac09-168">How To: Delete a Queue</span></span>
<span data-ttu-id="9ac09-169">toodelete uma fila e todas as mensagens de saudação contidos nele, chamada hello **excluir\_Queue ()** método no objeto de fila de saudação.</span><span class="sxs-lookup"><span data-stu-id="9ac09-169">toodelete a queue and all hello messages contained in it, call hello **delete\_queue()** method on hello queue object.</span></span>

```ruby
azure_queue_service.delete_queue("test-queue")
```

## <a name="next-steps"></a><span data-ttu-id="9ac09-170">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9ac09-170">Next Steps</span></span>
<span data-ttu-id="9ac09-171">Agora que você aprendeu as Noções básicas de saudação do armazenamento de fila, siga essas toolearn links sobre tarefas mais complexas de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="9ac09-171">Now that you've learned hello basics of queue storage, follow these links toolearn about more complex storage tasks.</span></span>

* <span data-ttu-id="9ac09-172">Visite Olá [Blog da equipe do armazenamento do Azure](http://blogs.msdn.com/b/windowsazurestorage/)</span><span class="sxs-lookup"><span data-stu-id="9ac09-172">Visit hello [Azure Storage Team Blog](http://blogs.msdn.com/b/windowsazurestorage/)</span></span>
* <span data-ttu-id="9ac09-173">Visite Olá [SDK do Azure para Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) repositório no GitHub</span><span class="sxs-lookup"><span data-stu-id="9ac09-173">Visit hello [Azure SDK for Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) repository on GitHub</span></span>

<span data-ttu-id="9ac09-174">Para obter uma comparação entre Olá serviço de fila do Azure discutidos neste artigo e filas do barramento de serviço do Azure discutidos Olá [como toouse filas do barramento de serviço](/develop/ruby/how-to-guides/service-bus-queues/) do artigo, consulte [filas do Azure e filas do Service Bus - comparadas e Contrastados](../service-bus-messaging/service-bus-azure-and-service-bus-queues-compared-contrasted.md)</span><span class="sxs-lookup"><span data-stu-id="9ac09-174">For a comparison between hello Azure Queue Service discussed in this article and Azure Service Bus Queues discussed in hello [How toouse Service Bus Queues](/develop/ruby/how-to-guides/service-bus-queues/) article, see [Azure Queues and Service Bus Queues - Compared and Contrasted](../service-bus-messaging/service-bus-azure-and-service-bus-queues-compared-contrasted.md)</span></span>
