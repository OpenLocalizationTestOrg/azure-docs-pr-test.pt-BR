---
title: "aaaGet de Introdução ao armazenamento de fila e o Visual Studio serviços conectados (ASP.NET Core) | Microsoft Docs"
description: Como tooget iniciado usando o armazenamento de fila do Azure em um projeto do ASP.NET Core no Visual Studio
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 04977069-5b2d-4cba-84ae-9fb2f5eb1006
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: 90c1ebcb6a2eac6bc4f6b69133bdf3135d359a72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-queue-storage-and-visual-studio-connected-services-aspnet-core"></a>Introdução ao armazenamento de filas e aos serviços conectados do Visual Studio (ASP.NET Core)
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a>Visão geral
Este artigo descreve como tooget iniciado usando o armazenamento de fila do Azure no Visual Studio depois que você criou ou referenciado uma conta de armazenamento do Azure em um projeto do ASP.NET Core usando Olá Visual Studio **adicionar serviços conectados** caixa de diálogo. Olá **adicionar serviços conectados** operação instala Olá apropriado NuGet pacotes tooaccess armazenamento do Azure em seu projeto e adiciona a cadeia de caracteres de conexão Olá para hello conta de armazenamento tooyour arquivos de configuração do projeto.

Armazenamento de fila do Azure é um serviço para armazenar grandes quantidades de mensagens que podem ser acessadas de qualquer lugar Olá, mundo por meio de chamadas autenticadas usando HTTP ou HTTPS. Uma mensagem da fila única pode ser o too64 quilobytes (KB) de tamanho e uma fila pode conter milhões de mensagens, o limite de capacidade total de toohello de uma conta de armazenamento.

tooget iniciado, você primeiro precisa toocreate uma fila do Azure em sua conta de armazenamento. Mostraremos como toocreate uma fila no código. Também mostraremos como tooperform basic fila operações, como adicionar, modificar, ler e remover mensagens da fila. exemplos de saudação são escritos em C\# de código e use Olá biblioteca de cliente de armazenamento do Azure para .NET. Para saber mais sobre ASP.NET, confira [ASP.NET](http://www.asp.net).

**Observação:** alguns Olá APIs que executam chamadas tooAzure armazenamento no núcleo do ASP.NET são assíncronas. Confira [Programação assíncrona com Async e Await](http://msdn.microsoft.com/library/hh191443.aspx) para saber mais. código de saudação abaixo supõe que os métodos de programação assíncrona estão sendo usados.

* Consulte [Introdução ao Armazenamento de Filas do Azure usando .NET](../storage/queues/storage-dotnet-how-to-use-queues.md) para obter mais informações sobre como manipular filas com programação.
* Consulte a [Documentação de armazenamento](https://azure.microsoft.com/documentation/services/storage/) para obter informações gerais sobre o armazenamento do Azure.
* Consulte a [documentação de serviços de nuvem](https://azure.microsoft.com/documentation/services/cloud-services/) para obter informações gerais sobre os serviços de nuvem do Azure.
* Consulte [ASP.NET](http://www.asp.net) para obter mais informações sobre como programar aplicativos ASP.NET.

## <a name="access-queues-in-code"></a>Acessar filas em código
filas de tooaccess em projetos do ASP.NET Core, você precisa fazer tooinclude Olá seguinte arquivo de origem do itens tooany c# que acessa o armazenamento de fila do Azure.

1. Certifique-se de declarações de namespace Olá na parte superior de saudação do arquivo hello c# incluem-las **usando** instruções.
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Queue;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. Obtenha um objeto **CloudStorageAccount** que represente as informações da conta de armazenamento. Saudação de uso tooget de código a seguir Olá sua cadeia de caracteres de conexão de armazenamento e as informações de conta de armazenamento da configuração de serviço do Azure de saudação.
   
         CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
           CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
3. Obter um **CloudQueueClient** de objetos tooreference Olá fila na conta de armazenamento.  
   
        // Create hello CloudQueueClient object for hello storage account.
        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
4. Obter um **CloudQueue** tooreference uma fila específica do objeto.
   
        // Get a reference toohello CloudQueue named "messageQueue"
        CloudQueue messageQueue = queueClient.GetQueueReference("messageQueue");

**Observação:** Use todos Olá acima código código Olá Olá exemplos a seguir.

### <a name="create-a-queue-in-code"></a>Criar uma fila em código
Olá toocreate fila do Azure no código, basta adicionar uma chamada muito**CreateIfNotExistsAsync**.

    // Create hello CloudQueue if it does not exist.
    await messageQueue.CreateIfNotExistsAsync();

## <a name="add-a-message-tooa-queue"></a>Adicionar uma fila de mensagens tooa
tooinsert uma mensagem em uma fila existente, crie um novo **CloudQueueMessage** objeto, em seguida, chamada hello **AddMessageAsync** método.

Um objeto **CloudQueueMessage** pode ser criado por meio de uma cadeia de caracteres (em formato UTF-8) ou de uma matriz de bytes.

Aqui está um exemplo que insere a mensagem de saudação 'Hello, World'.

    // Create a message and add it toohello queue.
    CloudQueueMessage message = new CloudQueueMessage("Hello, World");
    await messageQueue.AddMessageAsync(message);

## <a name="read-a-message-in-a-queue"></a>Ler uma mensagem em uma fila
Você pode inspecionar mensagem de saudação na frente de saudação de uma fila sem removê-la da fila de saudação por chamada hello **PeekMessageAsync** método.

    // Peek hello next message in hello queue. 
    CloudQueueMessage peekedMessage = await messageQueue.PeekMessageAsync();


## <a name="read-and-remove-a-message-in-a-queue"></a>Ler e remover uma mensagem em uma fila
Seu código pode remover uma mensagem de uma fila em duas etapas.

1. Chamar **GetMessageAsync** tooget Olá próxima mensagem em uma fila. Uma mensagem retornada de **GetMessageAsync** se torna invisível tooany outro código de leitura de mensagens dessa fila. Por padrão, essa mensagem permanece invisível por 30 segundos.
2. Removendo a mensagem de saudação de fila de hello, chamada de toofinish **DeleteMessageAsync**.

Esse processo de duas etapas de remoção de uma mensagem garante que se seu código falha tooprocess que uma mensagem devido a falha de toohardware ou software, outra instância do seu código pode obter Olá a mesma mensagem e tente novamente. chamadas de código a seguir Olá **DeleteMessageAsync** logo depois que a mensagem de saudação foi processada.

    // Get hello next message in hello queue.
    CloudQueueMessage retrievedMessage = await messageQueue.GetMessageAsync();

    // Process hello message in less than 30 seconds.

    // Then delete hello message.
    await messageQueue.DeleteMessageAsync(retrievedMessage);

## <a name="leverage-additional-options-for-dequeuing-messages"></a>Como aproveitar opções adicionais para remover mensagens da fila
Há duas maneiras de personalizar a recuperação da mensagem de uma fila.
Primeiro, você pode obter um lote de mensagens (até too32). Em seguida, você pode definir um tempo limite de invisibilidade maiores ou menores, permitindo que o código mais ou menos tempo toofully processam cada mensagem. usos de exemplo de código a seguir de saudação do **GetMessages** mensagens tooget 20 de método em uma chamada. Em seguida, ele processa cada mensagem usando um loop **foreach** . Ele também define minutos de too5 de tempo limite de invisibilidade de saudação para cada mensagem. Observe que Olá início de 5 minutos para todas as mensagens em Olá mesmo tempo, portanto, depois de 5 minutos após a chamada de saudação muito**GetMessages**, qualquer mensagem que não foram excluídas se tornar visível novamente.

    // Retrieve 20 messages at a time, keeping those messages invisible for 5 minutes, 
    //   delete each message after processing.

    foreach (CloudQueueMessage message in messageQueue.GetMessages(20, TimeSpan.FromMinutes(5)))
    {
        // Process all messages in less than 5 minutes, deleting each message after processing.
        queue.DeleteMessage(message);
    }

## <a name="get-hello-queue-length"></a>Obter o comprimento da fila de saudação
Você pode obter uma estimativa do número de saudação de mensagens em uma fila. O **FetchAttributes** método solicita o serviço de fila Olá para recuperar os atributos de fila hello, incluindo o número de mensagens de saudação. Olá **ApproximateMethodCount** propriedade retorna o último valor de saudação recuperado pelo **FetchAttributes** método sem chamar o serviço de fila de saudação.

    // Fetch hello queue attributes.
    messageQueue.FetchAttributes();

    // Retrieve hello cached approximate message count.
    int? cachedMessageCount = messageQueue.ApproximateMessageCount;

    // Display hello number of messages.
    Console.WriteLine("Number of messages in queue: " + cachedMessageCount);

## <a name="use-hello-async-await-pattern-with-common-queue-apis"></a>Usar padrão de saudação Async-Await com APIs de fila comum
Este exemplo mostra como toouse Olá Async-Await padrão com APIs de fila comum. versão Olá exemplo chamadas Olá assíncrona de cada Olá fornecido métodos. Isso pode ser visto por pós-correção de Olá assíncrona de cada método. Quando um método assíncrono é usado, o padrão de Async-Await Olá suspende a execução local até Olá chamada ser concluída. Esse comportamento permite Olá atual thread toodo outro trabalho que ajuda a evitar gargalos de desempenho e melhora a Olá a capacidade de resposta geral do seu aplicativo. Para obter mais detalhes sobre como usar o hello padrão Async-Await no .NET, consulte [Async e Await (c# e Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)

    // Create a message tooadd toohello queue.
    CloudQueueMessage cloudQueueMessage = new CloudQueueMessage("My message");

    // Async enqueue hello message.
    await messageQueue.AddMessageAsync(cloudQueueMessage);
    Console.WriteLine("Message added");

    // Async dequeue hello message.
    CloudQueueMessage retrievedMessage = await messageQueue.GetMessageAsync();
    Console.WriteLine("Retrieved message with content '{0}'", retrievedMessage.AsString);

    // Async delete hello message.
    await messageQueue.DeleteMessageAsync(retrievedMessage);
    Console.WriteLine("Deleted message");
## <a name="delete-a-queue"></a>Excluir uma fila
toodelete uma fila e todas as mensagens de saudação contidos nela, chame o **excluir** método no objeto de fila de saudação.

    // Delete hello queue.
    messageQueue.Delete();


## <a name="next-steps"></a>Próximas etapas
[!INCLUDE [vs-storage-dotnet-queues-next-steps](../../includes/vs-storage-dotnet-queues-next-steps.md)]

