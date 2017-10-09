---
title: "aaaGet de Introdução ao armazenamento de fila do Azure usando o .NET | Microsoft Docs"
description: "As filas do Azure fornecem uma mensagem assíncrona e confiável entre os componentes do aplicativo. Nuvem permite que mensagens seu tooscale de componentes de aplicativo independentemente."
services: storage
documentationcenter: .net
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: c0f82537-a613-4f01-b2ed-fc82e5eea2a7
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 03/27/2017
ms.author: robinsh
ms.openlocfilehash: 0cf6a71392b2fe859c7c9a9898c1ec84bcab4b19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-queue-storage-using-net"></a>Introdução ao armazenamento de Fila do Azure usando o .NET
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-check-out-samples-dotnet](../../../includes/storage-check-out-samples-dotnet.md)]

## <a name="overview"></a>Visão geral
O armazenamento de filas do Azure fornece mensagens na nuvem entre os componentes do aplicativo. Na criação de aplicativos para escala, os componentes do aplicativo geralmente são desassociados, para que possam ser redimensionados independentemente. Armazenamento de fila fornece mensagens assíncronas para a comunicação entre componentes de aplicativos, quer eles estejam em execução na nuvem hello, na área de trabalho hello, em um servidor local ou em um dispositivo móvel. O armazenamento de Fila também dá suporte ao gerenciamento de tarefas assíncronas e à criação de fluxos de trabalho do processo.

### <a name="about-this-tutorial"></a>Sobre este tutorial
Este tutorial mostra como toowrite .NET código em alguns cenários comuns usando o armazenamento de fila do Azure. Os cenários abordados incluem a criação e a exclusão de filas e a adição, a leitura e a exclusão de mensagens da fila.

**Estimado tempo toocomplete:** 45 minutos

**Pré-requisitos:**

* [Microsoft Visual Studio](https://www.visualstudio.com/downloads/)
* [Biblioteca do Cliente de Armazenamento do Azure para .NET](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [Gerenciador de Configurações do Azure para .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)
* [Uma conta do Armazenamento do Azure](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json#create-a-storage-account)

[!INCLUDE [storage-dotnet-client-library-version-include](../../../includes/storage-dotnet-client-library-version-include.md)]

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-development-environment-include](../../../includes/storage-development-environment-include.md)]

### <a name="add-using-directives"></a>Adicionar diretivas using
Adicione o seguinte Olá `using` superior de toohello de diretivas de saudação `Program.cs` arquivo:

```csharp
using Microsoft.Azure; // Namespace for CloudConfigurationManager
using Microsoft.WindowsAzure.Storage; // Namespace for CloudStorageAccount
using Microsoft.WindowsAzure.Storage.Queue; // Namespace for Queue storage types
```

### <a name="parse-hello-connection-string"></a>Analisar a cadeia de conexão Olá
[!INCLUDE [storage-cloud-configuration-manager-include](../../../includes/storage-cloud-configuration-manager-include.md)]

### <a name="create-hello-queue-service-client"></a>Criar o cliente do serviço de fila Olá
Olá **CloudQueueClient** classe permite que você tooretrieve filas armazenadas no armazenamento de fila. Aqui está o cliente do serviço Olá toocreate unidirecional:

```csharp
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
```
    
Agora você está pronto toowrite código lê e grava o armazenamento de tooQueue de dados.

## <a name="create-a-queue"></a>Criar uma fila
Este exemplo mostra como toocreate uma fila se ela ainda não existir:

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa container.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Create hello queue if it doesn't already exist
queue.CreateIfNotExists();
```

## <a name="insert-a-message-into-a-queue"></a>Inserir uma mensagem em uma fila
tooinsert uma mensagem em uma fila existente, primeiro crie um novo **CloudQueueMessage**. Em seguida, chame Olá **AddMessage** método. Um **CloudQueueMessage** pode ser criado por meio de uma cadeia de caracteres (em formato UTF-8) ou de uma matriz de **bytes**. Aqui está o código que cria uma fila (se não existir) e a mensagem de saudação inserções 'Hello, World':

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Create hello queue if it doesn't already exist.
queue.CreateIfNotExists();

// Create a message and add it toohello queue.
CloudQueueMessage message = new CloudQueueMessage("Hello, World");
queue.AddMessage(message);
```

## <a name="peek-at-hello-next-message"></a>Espiar a próxima mensagem de saudação
Você pode inspecionar mensagem de saudação na frente de saudação de uma fila sem removê-la da fila de saudação por chamada hello **PeekMessage** método.

```csharp
// Retrieve storage account from connection string
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Peek at hello next message
CloudQueueMessage peekedMessage = queue.PeekMessage();

// Display message.
Console.WriteLine(peekedMessage.AsString);
```

## <a name="change-hello-contents-of-a-queued-message"></a>Alterar o conteúdo de saudação de uma mensagem na fila
Você pode alterar o conteúdo de saudação de um mensagem no local na fila de saudação. Se a mensagem representa uma tarefa de trabalho, você pode usar tooupdate esse recurso o status da tarefa de trabalho hello. saudação de código a seguir atualiza a mensagem da fila de saudação com novo conteúdo e conjuntos Olá tooextend de tempo limite de visibilidade outro 60 segundos. Isso salva o estado de saudação do trabalho associado à mensagem de saudação e fornece cliente Olá outro toocontinue minuto trabalhando na mensagem de saudação. Você pode usar esta técnica tootrack várias etapas os fluxos de trabalho na fila de mensagens, sem ter que toostart através do hello início se uma etapa de processamento falhar devido a falha de toohardware ou software. Normalmente, você mantém uma contagem de tentativa e se hello mensagem será repetida mais de  *n*  vezes, excluí-lo. Isso protege contra uma mensagem que dispara um erro do aplicativo sempre que for processada.

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Get hello message from hello queue and update hello message contents.
CloudQueueMessage message = queue.GetMessage();
message.SetMessageContent("Updated contents.");
queue.UpdateMessage(message,
    TimeSpan.FromSeconds(60.0),  // Make it invisible for another 60 seconds.
    MessageUpdateFields.Content | MessageUpdateFields.Visibility);
```

## <a name="de-queue-hello-next-message"></a>Eliminação da fila de mensagem de saudação do próxima
Seu código remove uma mensagem de um fila em duas etapas. Quando você chama **GetMessage**, obter próxima mensagem de saudação em uma fila. Uma mensagem retornada de **GetMessage** se torna invisível tooany outro código de leitura de mensagens dessa fila. Por padrão, essa mensagem permanece invisível por 30 segundos. toofinish mensagem de saudação remover da fila hello, você também deve chamar **DeleteMessage**. Esse processo de duas etapas de remoção de uma mensagem garante que se seu código falha tooprocess que uma mensagem devido a falha de toohardware ou software, outra instância do seu código pode obter Olá a mesma mensagem e tente novamente. Seu código chama **DeleteMessage** logo depois que a mensagem de saudação foi processada.

```csharp
// Retrieve storage account from connection string
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Get hello next message
CloudQueueMessage retrievedMessage = queue.GetMessage();

//Process hello message in less than 30 seconds, and then delete hello message
queue.DeleteMessage(retrievedMessage);
```

## <a name="use-async-await-pattern-with-common-queue-storage-apis"></a>Usar padrão Async-Await com APIs comuns de armazenamento da fila
Este exemplo mostra como Olá toouse Async-Await padrão com APIs comuns de armazenamento de fila. exemplo Hello chama a versão assíncrona saudação de cada Olá fornecido métodos, conforme indicado pelo Olá *Async* sufixo de cada método. Quando um método assíncrono é usado, Olá async-await padrão suspende a execução local até Olá chamada ser concluída. Esse comportamento permite Olá atual thread toodo outro trabalho, o que ajuda a evitar gargalos de desempenho e melhora a Olá a capacidade de resposta geral do seu aplicativo. Para obter mais detalhes sobre como usar o hello padrão Async-Await no .NET consulte [Async e Await (c# e Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)

```csharp
// Create hello queue if it doesn't already exist
if(await queue.CreateIfNotExistsAsync())
{
    Console.WriteLine("Queue '{0}' Created", queue.Name);
}
else
{
    Console.WriteLine("Queue '{0}' Exists", queue.Name);
}

// Create a message tooput in hello queue
CloudQueueMessage cloudQueueMessage = new CloudQueueMessage("My message");

// Async enqueue hello message
await queue.AddMessageAsync(cloudQueueMessage);
Console.WriteLine("Message added");

// Async dequeue hello message
CloudQueueMessage retrievedMessage = await queue.GetMessageAsync();
Console.WriteLine("Retrieved message with content '{0}'", retrievedMessage.AsString);

// Async delete hello message
await queue.DeleteMessageAsync(retrievedMessage);
Console.WriteLine("Deleted message");
```
    
## <a name="leverage-additional-options-for-de-queuing-messages"></a>Aproveitar opções adicionais para remover mensagens da fila
Há duas maneiras de personalizar a recuperação da mensagem de uma fila.
Primeiro, você pode obter um lote de mensagens (até too32). Em seguida, você pode definir um tempo limite de invisibilidade maiores ou menores, permitindo que o código mais ou menos tempo toofully processam cada mensagem. usos de exemplo de código a seguir de saudação do **GetMessages** mensagens tooget 20 de método em uma chamada. Em seguida, ele processa cada mensagem usando um loop **foreach** . Ele também define minutos de toofive de tempo limite de invisibilidade de saudação para cada mensagem. Observe que Olá 5 minutos é iniciado para todas as mensagens com hello a mesma hora, após 5 minutos se passaram desde chamada hello muito**GetMessages**, qualquer mensagem que não foram excluídas se tornará visível novamente.

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

foreach (CloudQueueMessage message in queue.GetMessages(20, TimeSpan.FromMinutes(5)))
{
    // Process all messages in less than 5 minutes, deleting each message after processing.
    queue.DeleteMessage(message);
}
```

## <a name="get-hello-queue-length"></a>Obter o comprimento da fila de saudação
Você pode obter uma estimativa do número de saudação de mensagens em uma fila. O **FetchAttributes** método solicita o serviço de fila Olá para recuperar os atributos de fila hello, incluindo o número de mensagens de saudação. Olá **ApproximateMessageCount** propriedade retorna o último valor de saudação recuperado pelo **FetchAttributes** método sem chamar o serviço de fila de saudação.

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Fetch hello queue attributes.
queue.FetchAttributes();

// Retrieve hello cached approximate message count.
int? cachedMessageCount = queue.ApproximateMessageCount;

// Display number of messages.
Console.WriteLine("Number of messages in queue: " + cachedMessageCount);
```

## <a name="delete-a-queue"></a>Excluir uma fila
toodelete uma fila e todas as mensagens de saudação contidos nela, chame o **excluir** método no objeto de fila de saudação.

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello queue client.
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

// Retrieve a reference tooa queue.
CloudQueue queue = queueClient.GetQueueReference("myqueue");

// Delete hello queue.
queue.Delete();
```
    

## <a name="next-steps"></a>Próximas etapas
Agora que você aprendeu as Noções básicas de saudação do armazenamento de fila, siga essas toolearn links sobre tarefas mais complexas de armazenamento.

* Exiba a documentação de referência de serviço de fila de saudação para obter detalhes completos sobre as APIs disponíveis:
  * [Referência à Biblioteca de Cliente de Armazenamento para .NET](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)
  * [Referência da API REST](http://msdn.microsoft.com/library/azure/dd179355)
* Saiba como código de saudação toosimplify escrever toowork com armazenamento do Azure usando Olá [SDK do Azure WebJobs](../../app-service-web/websites-dotnet-webjobs-sdk.md).
* Exiba toolearn de guias de recurso mais sobre opções adicionais para armazenar dados no Azure.
  * [Introdução ao armazenamento de tabela do Azure usando o .NET](../../cosmos-db/table-storage-how-to-use-dotnet.md) toostore estruturado de dados.
  * [Introdução ao armazenamento de BLOBs do Azure usando o .NET](../blobs/storage-dotnet-how-to-use-blobs.md) toostore dados não estruturados.
  * [Conecte-se tooSQL banco de dados usando o .NET (c#)](../../sql-database/sql-database-connect-query-dotnet-core.md) dados relacionais toostore.

[Download and install hello Azure SDK for .NET]: /develop/net/
[.NET client library reference]: http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409
[Creating a Azure Project in Visual Studio]: http://msdn.microsoft.com/library/azure/ee405487.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
[OData]: http://nuget.org/packages/Microsoft.Data.OData/5.0.2
[Edm]: http://nuget.org/packages/Microsoft.Data.Edm/5.0.2
[Spatial]: http://nuget.org/packages/System.Spatial/5.0.2
