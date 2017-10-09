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
ms.openlocfilehash: 755380824890ad83774e14d258975915e10cfede
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-c"></a>Como toouse armazenamento de fila de C++
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a>Visão geral
Este guia mostrará como tooperform cenários comuns usando Olá serviço de armazenamento de fila do Azure. exemplos de saudação são escritos em C++ e usam Olá [biblioteca de cliente de armazenamento do Azure para C++](http://github.com/Azure/azure-storage-cpp/blob/master/README.md). Olá cenários abordados incluem **inserindo**, **inspecionar**, **obtendo**, e **excluindo** Enfileirar mensagens, bem como  **criar e excluir filas**.

> [!NOTE]
> Destino dessa guia Olá biblioteca de cliente de armazenamento do Azure para a versão 1.0.0 de C++ e acima. Olá recomendado versão é a biblioteca de cliente de armazenamento 2.2.0, que está disponível por meio de [NuGet](http://www.nuget.org/packages/wastorage) ou [GitHub](http://github.com/Azure/azure-storage-cpp/).
> 
> 

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-c-application"></a>Criar um aplicativo em C++
Neste guia, você usará os recursos de armazenamento que podem ser executados em um aplicativo C++.

toodo assim, você precisará tooinstall hello biblioteca de cliente de armazenamento do Azure para C++ e criar uma conta de armazenamento do Azure em sua assinatura do Azure.

Olá tooinstall biblioteca de cliente de armazenamento do Azure para C++, você pode usar o hello métodos a seguir:

* **Linux:** siga instruções Olá fornecidas em Olá [biblioteca de cliente de armazenamento do Azure para C++ Leiame](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) página.
* **Windows:** no Visual Studio, clique em **Ferramentas > Gerenciador de Pacotes do NuGet > Console do Gerenciador de Pacotes**. Digite o seguinte Olá comando em Olá [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) e pressione **ENTER**.

```  
Install-Package wastorage
```

## <a name="configure-your-application-tooaccess-queue-storage"></a>Configurar seu aplicativo tooaccess armazenamento de fila
Adicione a seguinte Olá incluem superior de toohello de instruções do arquivo de C++ de saudação onde você deseja que as filas de tooaccess APIs de armazenamento do Azure Olá toouse:  

```cpp
#include <was/storage_account.h>
#include <was/queue.h>
```

## <a name="set-up-an-azure-storage-connection-string"></a>Configurar uma cadeia de conexão de armazenamento do Azure
Um cliente de armazenamento do Azure usa um pontos de extremidade de toostore de cadeia de caracteres de conexão de armazenamento e as credenciais para acessar os serviços de gerenciamento de dados. Quando em execução em um aplicativo cliente, você deve fornecer a cadeia de conexão de armazenamento Olá no hello formato a seguir, usando o nome de saudação da chave de acesso do armazenamento seu armazenamento conta e Olá Olá conta de armazenamento listada no hello [Portal do Azure](https://portal.azure.com)para Olá *AccountName* e *AccountKey* valores. Para obter informações sobre as contas de armazenamento e as chaves de acesso, consulte [Sobre as Contas de Armazenamento do Azure](storage-create-storage-account.md). Este exemplo mostra como você pode declarar uma cadeia de caracteres de conexão do campo estático toohold hello:  

```cpp
// Define hello connection-string with your values.
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

tootest seu aplicativo no seu computador local do Windows, você pode usar o hello Microsoft Azure [emulador de armazenamento](storage-use-emulator.md) que é instalada com hello [SDK do Azure](https://azure.microsoft.com/downloads/). emulador de armazenamento Olá é um utilitário que simula os serviços de Blob, fila e tabela de saudação disponíveis no Azure em sua máquina de desenvolvimento local. Olá exemplo a seguir mostra como você pode declarar um emulador de armazenamento local do campo estático toohold Olá cadeia de caracteres conexão tooyour:  

```cpp
// Define hello connection-string with Azure Storage Emulator.
const utility::string_t storage_connection_string(U("UseDevelopmentStorage=true;"));  
```

emulador de armazenamento do Azure toostart hello, selecione Olá **iniciar** Olá botão ou pressione **Windows** chave. Comece digitando **emulador de armazenamento do Azure**e selecione **emulador de armazenamento do Microsoft Azure** da lista de saudação de aplicativos.

Olá exemplos a seguir pressupõem que você usou uma cadeia de conexão de armazenamento esses dois métodos tooget hello.

## <a name="retrieve-your-connection-string"></a>Recuperar sua cadeia de conexão
Você pode usar o hello **cloud_storage_account** classe toorepresent suas informações de conta de armazenamento. tooretrieve informações de cadeia de caracteres de conexão de armazenamento Olá da conta de armazenamento, você pode usar o hello **analisar** método.

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);
```

## <a name="how-to-create-a-queue"></a>Como criar uma fila
Um objeto **cloud_queue_client** permite que você obtenha objetos de referência para as filas. Olá código a seguir cria um **cloud_queue_client** objeto.

```cpp
// Retrieve storage account from connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create a queue client.
azure::storage::cloud_queue_client queue_client = storage_account.create_cloud_queue_client();
```

Saudação de uso **cloud_queue_client** tooget uma fila de toohello de referência que você deseja toouse do objeto. Você pode criar a fila de saudação se ele não existir.

```cpp
// Retrieve a reference tooa queue.
azure::storage::cloud_queue queue = queue_client.get_queue_reference(U("my-sample-queue"));

// Create hello queue if it doesn't already exist.
 queue.create_if_not_exists();  
```

## <a name="how-to-insert-a-message-into-a-queue"></a>Como inserir uma mensagem em uma fila
tooinsert uma mensagem em uma fila existente, primeiro crie um novo **cloud_queue_message**. Em seguida, chame Olá **add_message** método. Uma **cloud_queue_message** pode ser criada a partir de uma cadeia de caracteres ou de uma matriz de **bytes**. Aqui está o código que cria uma fila (se não existir) e a mensagem de saudação inserções 'Hello, World':

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

## <a name="how-to-peek-at-hello-next-message"></a>Como: espiar a próxima mensagem de saudação
Você pode inspecionar mensagem de saudação na frente de saudação de uma fila sem removê-la da fila de saudação por chamada hello **peek_message** método.

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

## <a name="how-to-change-hello-contents-of-a-queued-message"></a>Como: alterar o conteúdo de saudação de uma mensagem na fila
Você pode alterar o conteúdo de saudação de um mensagem no local na fila de saudação. Se a mensagem de saudação representa uma tarefa de trabalho, você pode usar esse status do recurso tooupdate Olá da tarefa de trabalho hello. saudação de código a seguir atualiza a mensagem da fila de saudação com novo conteúdo e conjuntos Olá tooextend de tempo limite de visibilidade outro 60 segundos. Isso salva o estado de saudação do trabalho associado à mensagem de saudação e fornece cliente Olá outro toocontinue minuto trabalhando na mensagem de saudação. Você pode usar esta técnica tootrack várias etapas os fluxos de trabalho na fila de mensagens, sem ter que toostart através do hello início se uma etapa de processamento falhar devido a falha de toohardware ou software. Normalmente, você mantém uma contagem de tentativa e se a mensagem de saudação é repetida mais de n vezes, você deve excluí-lo. Isso protege contra uma mensagem que dispara um erro do aplicativo sempre que for processada.

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

## <a name="how-to-de-queue-hello-next-message"></a>Como: eliminação da fila de mensagem de saudação do próxima
Seu código remove uma mensagem de um fila em duas etapas. Quando você chama **get_message**, obter próxima mensagem de saudação em uma fila. Uma mensagem retornada de **get_message** se torna invisível tooany outro código de leitura de mensagens dessa fila. toofinish mensagem de saudação remover da fila hello, você também deve chamar **delete_message**. Esse processo de duas etapas de remoção de uma mensagem garante que se seu código falha tooprocess que uma mensagem devido a falha de toohardware ou software, outra instância do seu código pode obter Olá a mesma mensagem e tente novamente. Seu código chama **delete_message** logo depois que a mensagem de saudação foi processada.

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

## <a name="how-to-leverage-additional-options-for-de-queuing-messages"></a>Como: aproveitar as opções adicionais para remover mensagens da fila
Há duas maneiras de personalizar a recuperação da mensagem de uma fila. Primeiro, você pode obter um lote de mensagens (até too32). Em seguida, você pode definir um tempo limite de invisibilidade maiores ou menores, permitindo que o código mais ou menos tempo toofully processam cada mensagem. Olá, exemplo de código a seguir usa Olá **get_messages** mensagens tooget 20 de método em uma chamada. Em seguida, ele processa cada mensagem usando um loop **for** . Ele também define minutos de toofive de tempo limite de invisibilidade de saudação para cada mensagem. Observe que Olá 5 minutos é iniciado para todas as mensagens com hello a mesma hora, após 5 minutos se passaram desde chamada hello muito**get_messages**, qualquer mensagem que não foram excluídas se tornará visível novamente.

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

## <a name="how-to-get-hello-queue-length"></a>Como: obter o comprimento da fila de saudação
Você pode obter uma estimativa do número de saudação de mensagens em uma fila. Olá **download_attributes** método solicita tooretrieve de serviço de fila Olá atributos da fila hello, incluindo o número de mensagens de saudação. Olá **approximate_message_count** método obtém o número aproximado de saudação de mensagens na fila de saudação.

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

## <a name="how-to-delete-a-queue"></a>Como excluir uma fila
toodelete uma fila e todas as mensagens de saudação contidas nele, chamada hello **delete_queue_if_exists** método no objeto de fila de saudação.

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

## <a name="next-steps"></a>Próximas etapas
Agora que você aprendeu as Noções básicas de saudação do armazenamento de fila, siga essas toolearn links mais sobre o armazenamento do Azure.

* [Como toouse armazenamento de Blob de C++](storage-c-plus-plus-how-to-use-blobs.md)
* [Como toouse o armazenamento de tabela do C++](storage-c-plus-plus-how-to-use-tables.md)
* [Listar recursos de Armazenamento do Azure em C++](storage-c-plus-plus-enumeration.md)
* [Referência da Biblioteca de Cliente de Armazenamento para C++](http://azure.github.io/azure-storage-cpp)
* [Documentação do Armazenamento do Azure](https://azure.microsoft.com/documentation/services/storage/)