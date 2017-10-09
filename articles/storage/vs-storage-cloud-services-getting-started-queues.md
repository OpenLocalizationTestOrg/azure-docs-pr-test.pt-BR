---
title: "aaaGet de Introdução ao armazenamento de fila e o Visual Studio serviços conectados (serviços de nuvem) | Microsoft Docs"
description: "Como tooget iniciado usando o armazenamento de fila do Azure em um projeto de serviço de nuvem no Visual Studio depois de conectar-se a conta de armazenamento tooa usando o Visual Studio conectada a serviços"
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: da587aac-5e64-4e9a-8405-44cc1924881d
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: 8ba3d830cb83e3d75102b8a09363f1dc200ff1c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-queue-storage-and-visual-studio-connected-services-cloud-services-projects"></a>Introdução aos serviços conectados do armazenamento de Fila do Azure e Visual Studio (projetos de serviços de nuvem)
[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a>Visão geral
Este artigo descreve como tooget iniciado usando o armazenamento de fila do Azure no Visual Studio depois que você criou ou referenciado uma conta de armazenamento do Azure em um projeto de serviços de nuvem usando o Visual Studio de saudação **adicionar serviços conectados** caixa de diálogo .

Mostraremos como toocreate uma fila no código. Também mostraremos como tooperform basic operações, como adicionar, modificar, ler e remoção de fila de mensagens da fila. exemplos de saudação são escritos em código c# e usam Olá [biblioteca de cliente de armazenamento do Microsoft Azure para .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).

Olá **adicionar serviços conectados** operação instala Olá apropriado NuGet pacotes tooaccess armazenamento do Azure em seu projeto e adiciona a cadeia de caracteres de conexão Olá para hello conta de armazenamento tooyour arquivos de configuração do projeto.

* Consulte a [Introdução ao Armazenamento de Filas do Azure usando o .NET](storage-dotnet-how-to-use-queues.md) para obter mais informações sobre a manipulação de filas no código.
* Consulte a [Documentação de armazenamento](https://azure.microsoft.com/documentation/services/storage/) para obter informações gerais sobre o armazenamento do Azure.
* Consulte a [documentação de serviços de nuvem](https://azure.microsoft.com/documentation/services/cloud-services/) para obter informações gerais sobre os serviços de nuvem do Azure.
* Consulte [ASP.NET](http://www.asp.net) para obter mais informações sobre como programar aplicativos ASP.NET.

Armazenamento de fila do Azure é um serviço para armazenar grandes quantidades de mensagens que podem ser acessadas de qualquer lugar Olá, mundo por meio de chamadas autenticadas usando HTTP ou HTTPS. Uma mensagem da fila única pode ser o too64 KB de tamanho e uma fila pode conter milhões de mensagens, o limite de capacidade total de toohello de uma conta de armazenamento.

## <a name="access-queues-in-code"></a>Acessar filas em código
filas de tooaccess em projetos de serviços de nuvem do Visual Studio, você precisa fazer tooinclude Olá seguinte arquivo de origem tooany c# de itens que acessar o armazenamento de fila do Azure.

1. Certifique-se de declarações de namespace Olá na parte superior de saudação do arquivo hello c# incluem-las **usando** instruções.
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Queue;
2. Obtenha um objeto **CloudStorageAccount** que represente as informações da conta de armazenamento. Saudação de uso tooget de código a seguir Olá sua cadeia de caracteres de conexão de armazenamento e as informações de conta de armazenamento da configuração de serviço do Azure de saudação.
   
         CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
           CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
3. Obter um **CloudQueueClient** de objetos tooreference Olá fila na conta de armazenamento.  
   
        // Create hello queue client.
        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
4. Obter um **CloudQueue** tooreference uma fila específica do objeto.
   
        // Get a reference tooa queue named "messageQueue"
        CloudQueue messageQueue = queueClient.GetQueueReference("messageQueue");

**Observação:** Use todos Olá acima código código Olá Olá exemplos a seguir.

## <a name="create-a-queue-in-code"></a>Criar uma fila em código
fila de saudação toocreate no código, basta adicionar uma chamada muito**CreateIfNotExists**.

    // Create hello CloudQueue if it does not exist
    messageQueue.CreateIfNotExists();

## <a name="add-a-message-tooa-queue"></a>Adicionar uma fila de mensagens tooa
tooinsert uma mensagem em uma fila existente, crie um novo **CloudQueueMessage** objeto, em seguida, chamada hello **AddMessage** método.

Um objeto **CloudQueueMessage** pode ser criado por meio de uma cadeia de caracteres (em formato UTF-8) ou de uma matriz de bytes.

Aqui está um exemplo que insere a mensagem de saudação 'Hello, World'.

    // Create a message and add it toohello queue.
    CloudQueueMessage message = new CloudQueueMessage("Hello, World");
    messageQueue.AddMessage(message);

## <a name="read-a-message-in-a-queue"></a>Ler uma mensagem em uma fila
Você pode inspecionar mensagem de saudação na frente de saudação de uma fila sem removê-la da fila de saudação por chamada hello **PeekMessage** método.

    // Peek at hello next message
    CloudQueueMessage peekedMessage = messageQueue.PeekMessage();

## <a name="read-and-remove-a-message-in-a-queue"></a>Ler e remover uma mensagem em uma fila
Seu código pode remover uma mensagem de uma fila em duas etapas.

1. Chamar **GetMessage** tooget Olá próxima mensagem em uma fila. Uma mensagem retornada de **GetMessage** se torna invisível tooany outro código de leitura de mensagens dessa fila. Por padrão, essa mensagem permanece invisível por 30 segundos.
2. Removendo a mensagem de saudação de fila de hello, chamada de toofinish **DeleteMessage**.

Esse processo de duas etapas de remoção de uma mensagem garante que se seu código falha tooprocess que uma mensagem devido a falha de toohardware ou software, outra instância do seu código pode obter Olá a mesma mensagem e tente novamente. chamadas de código a seguir Olá **DeleteMessage** logo depois que a mensagem de saudação foi processada.

    // Get hello next message in hello queue.
    CloudQueueMessage retrievedMessage = messageQueue.GetMessage();

    // Process hello message in less than 30 seconds

    // Then delete hello message.
    await messageQueue.DeleteMessage(retrievedMessage);


## <a name="use-additional-options-tooprocess-and-remove-queue-messages"></a>Use opções adicionais tooprocess e remover mensagens da fila
Há duas maneiras de personalizar a recuperação da mensagem de uma fila.

* Você pode obter um lote de mensagens (até too32).
* Você pode definir um tempo limite de invisibilidade maiores ou menores, permitindo que o código mais ou menos tempo toofully processam cada mensagem. usos de exemplo de código a seguir de saudação do **GetMessages** mensagens tooget 20 de método em uma chamada. Em seguida, ele processa cada mensagem usando um loop **foreach** . Ele também define minutos de toofive de tempo limite de invisibilidade de saudação para cada mensagem. Observe que Olá 5 minutos é iniciado para todas as mensagens com hello a mesma hora, após 5 minutos se passaram desde chamada hello muito**GetMessages**, qualquer mensagem que não foram excluídas se tornará visível novamente.

Aqui está um exemplo:

    foreach (CloudQueueMessage message in messageQueue.GetMessages(20, TimeSpan.FromMinutes(5)))
    {
        // Process all messages in less than 5 minutes, deleting each message after processing.

        // Then delete hello message after processing
        messageQueue.DeleteMessage(message);

    }

## <a name="get-hello-queue-length"></a>Obter o comprimento da fila de saudação
Você pode obter uma estimativa do número de saudação de mensagens em uma fila. O **FetchAttributes** método solicita o serviço de fila Olá para recuperar os atributos de fila hello, incluindo o número de mensagens de saudação. Olá **ApproximateMethodCount** propriedade retorna o último valor de saudação recuperado pelo **FetchAttributes** método sem chamar o serviço de fila de saudação.

    // Fetch hello queue attributes.
    messageQueue.FetchAttributes();

    // Retrieve hello cached approximate message count.
    int? cachedMessageCount = messageQueue.ApproximateMessageCount;

    // Display number of messages.
    Console.WriteLine("Number of messages in queue: " + cachedMessageCount);

## <a name="use-hello-async-await-pattern-with-common-azure-queue-apis"></a>Usar saudação padrão Async-Await com APIs comuns de fila do Azure
Este exemplo mostra como Olá toouse Async-Await padrão com APIs comuns de fila do Azure. exemplo Hello chama a versão assíncrona de saudação de cada Olá fornecido métodos, isso pode ser visto por Olá **Async** após a correção de cada método. Quando um método assíncrono é usado Olá async-await padrão suspende a execução local até Olá chamada ser concluída. Esse comportamento permite Olá atual thread toodo outro trabalho que ajuda a evitar gargalos de desempenho e melhora a Olá a capacidade de resposta geral do seu aplicativo. Para obter mais detalhes sobre como usar o hello padrão Async-Await no .NET consulte [Async e Await (c# e Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx)

    // Create a message tooput in hello queue
    CloudQueueMessage cloudQueueMessage = new CloudQueueMessage("My message");

    // Add hello message asynchronously
    await messageQueue.AddMessageAsync(cloudQueueMessage);
    Console.WriteLine("Message added");

    // Async dequeue hello message
    CloudQueueMessage retrievedMessage = await messageQueue.GetMessageAsync();
    Console.WriteLine("Retrieved message with content '{0}'", retrievedMessage.AsString);

    // Delete hello message asynchronously
    await messageQueue.DeleteMessageAsync(retrievedMessage);
    Console.WriteLine("Deleted message");

## <a name="delete-a-queue"></a>Excluir uma fila
toodelete uma fila e todas as mensagens de saudação contidas nele, chamada hello **excluir** método no objeto de fila de saudação.

    // Delete hello queue.
    messageQueue.Delete();

## <a name="next-steps"></a>Próximas etapas
[!INCLUDE [vs-storage-dotnet-queues-next-steps](../../includes/vs-storage-dotnet-queues-next-steps.md)]

