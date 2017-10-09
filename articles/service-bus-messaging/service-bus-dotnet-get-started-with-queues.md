---
title: "aaaGet iniciado com filas do barramento de serviço do Azure | Microsoft Docs"
description: "Escreva um aplicativo de console em C# que usa filas de mensagens do Barramento de Serviço."
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 68a34c00-5600-43f6-bbcc-fea599d500da
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: hero-article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 06/26/2017
ms.author: sethm
ms.openlocfilehash: eaa362ab0eabd2427977398c1deab5dc00105ae9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-service-bus-queues"></a>Introdução às filas do Barramento de Serviço
[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

## <a name="what-will-be-accomplished"></a>O que será realizado
Este tutorial aborda Olá etapas a seguir:

1. Crie um namespace de barramento de serviço, usando Olá portal do Azure.
2. Crie uma fila do barramento de serviço, usando Olá portal do Azure.
3. Grave uma mensagem de um toosend do aplicativo de console.
4. Grave uma saudação de tooreceive do aplicativo de console mensagens enviadas na etapa anterior hello.

## <a name="prerequisites"></a>Pré-requisitos
1. [Visual Studio 2015 ou superior](http://www.visualstudio.com). exemplos de saudação neste tutorial usam 2017 do Visual Studio.
2. Uma assinatura do Azure.

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-hello-azure-portal"></a>1. Criar um namespace usando Olá portal do Azure
Se você já criou um namespace do sistema de mensagens do barramento de serviço, ir toohello [criar uma fila usando o portal do Azure de saudação](#2-create-a-queue-using-the-azure-portal) seção.

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="2-create-a-queue-using-hello-azure-portal"></a>2. Criar uma fila usando Olá portal do Azure
Se você já criou uma fila do barramento de serviço, ir toohello [toohello fila de mensagens de envio](#3-send-messages-to-the-queue) seção.

[!INCLUDE [service-bus-create-queue-portal](../../includes/service-bus-create-queue-portal.md)]

## <a name="3-send-messages-toohello-queue"></a>3. Mensagens toohello fila de envio
fila de mensagens de toohello de toosend, podemos gravar um aplicativo de console c# usando o Visual Studio.

### <a name="create-a-console-application"></a>Criar um aplicativo de console

Inicie o Visual Studio e crie um novo projeto de **Aplicativo de console (.NET Framework)**.

### <a name="add-hello-service-bus-nuget-package"></a>Adicionar o pacote do NuGet do barramento de serviço Olá
1. Clique com botão direito Olá recém-criado e selecione **gerenciar pacotes NuGet**.
2. Clique em Olá **procurar** guia, procure **barramento de serviço do Microsoft Azure**e, em seguida, selecione Olá **windowsazure. ServiceBus** item. Clique em **instalar** toocomplete Olá instalação, em seguida, feche esta caixa de diálogo.
   
    ![Selecionar um pacote NuGet][nuget-pkg]

### <a name="write-some-code-toosend-a-message-toohello-queue"></a>Gravar algumas toosend código uma fila de mensagens toohello
1. Adicione o seguinte Olá `using` superior de toohello de instrução do arquivo Program.cs de saudação.
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
2. Adicionar Olá toohello de código a seguir `Main` método. Saudação de conjunto `connectionString` conexão toohello variável de cadeia de caracteres obtido ao criar namespace hello e definir `queueName` toohello nome da fila que você usou ao criar a fila de saudação.
   
    ```csharp
    var connectionString = "<your connection string>";
    var queueName = "<your queue name>";
   
    var client = QueueClient.CreateFromConnectionString(connectionString, queueName);
    var message = new BrokeredMessage("This is a test message!");

    Console.WriteLine(String.Format("Message id: {0}", message.MessageId));

    client.Send(message);

    Console.WriteLine("Message successfully sent! Press ENTER tooexit program");
    Console.ReadLine();
    ```
   
    Seu arquivo Program.cs deve ficar assim.
   
    ```csharp
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    using Microsoft.ServiceBus.Messaging;

    namespace qsend
    {
        class Program
        {
            static void Main(string[] args)
            {
                var connectionString = "Endpoint=sb://<your namespace>.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=<your key>";
                var queueName = "<your queue name>";

                var client = QueueClient.CreateFromConnectionString(connectionString, queueName);
                var message = new BrokeredMessage("This is a test message!");

                Console.WriteLine(String.Format("Message id: {0}", message.MessageId));

                client.Send(message);

                Console.WriteLine("Message successfully sent! Press ENTER tooexit program");
                Console.ReadLine();
            }
        }
    }
    ```
3. Execute o programa hello e verifique Olá portal do Azure: clique em nome de saudação da fila no namespace de saudação **visão geral** folha. fila de saudação **Essentials** folha é exibida. Observe que Olá **contagem de mensagens ativa** valor agora deve ser 1. Cada vez que executar o aplicativo de remetente hello sem recuperar mensagens de saudação, esse valor aumenta em 1. Também Observe que tamanho atual de saudação da fila de saudação de incrementos de cada aplicativo de saudação do tempo adiciona uma fila de mensagens toohello.
   
      ![Tamanho da mensagem][queue-message]

## <a name="4-receive-messages-from-hello-queue"></a>4. Receber mensagens da fila de saudação

1. Você acabou de enviar mensagens de saudação do tooreceive criar um novo aplicativo de console e adicionar um pacote de NuGet do barramento de serviço do toohello de referência, aplicativo de remetente anterior toohello semelhante.
2. Adicione o seguinte Olá `using` superior de toohello de instrução do arquivo Program.cs de saudação.
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
3. Adicionar Olá toohello de código a seguir `Main` método. Saudação de conjunto `connectionString` toohello variável cadeia de conexão que foi obtida durante a criação de namespace hello e defina `queueName` toohello nome da fila que você usou ao criar a fila de saudação.
   
    ```csharp
    var connectionString = "<your connection string>";
    var queueName = "<your queue name>";
   
    var client = QueueClient.CreateFromConnectionString(connectionString, queueName);
   
    client.OnMessage(message =>
    {
      Console.WriteLine(String.Format("Message body: {0}", message.GetBody<String>()));
      Console.WriteLine(String.Format("Message id: {0}", message.MessageId));
    });
   
    Console.WriteLine("Press ENTER tooexit program");
    Console.ReadLine();
    ```
   
    O arquivo Program.cs deve ficar assim:
   
    ```csharp
    using System;
    using Microsoft.ServiceBus.Messaging;
   
    namespace GettingStartedWithQueues
    {
      class Program
      {
        static void Main(string[] args)
        {
          var connectionString = "Endpoint=sb://<your namespace>.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=<your key>";;
          var queueName = "<your queue name>";
   
          var client = QueueClient.CreateFromConnectionString(connectionString, queueName);
   
          client.OnMessage(message =>
          {
            Console.WriteLine(String.Format("Message body: {0}", message.GetBody<String>()));
            Console.WriteLine(String.Format("Message id: {0}", message.MessageId));
          });

          Console.WriteLine("Press ENTER tooexit program");   
          Console.ReadLine();
        }
      }
    }
    ```
4. Executar programa hello e verificar novamente o portal de saudação. Observe que Olá **contagem de mensagens ativa** e **atual** valores agora são 0.
   
    ![Comprimento da fila][queue-message-receive]

Parabéns! Agora, você criou uma fila, enviou uma mensagem e recebeu uma mensagem.

## <a name="next-steps"></a>Próximas etapas

Confira nosso [repositório GitHub com exemplos](https://github.com/Azure/azure-service-bus/tree/master/samples) que demonstram algumas das mais recursos avançados do barramento de serviço de mensagens de saudação.

<!--Image references-->

[nuget-pkg]: ./media/service-bus-dotnet-get-started-with-queues/nuget-package.png
[queue-message]: ./media/service-bus-dotnet-get-started-with-queues/queue-message.png
[queue-message-receive]: ./media/service-bus-dotnet-get-started-with-queues/queue-message-receive.png
[github-samples]: https://github.com/Azure-Samples/azure-servicebus-messaging-samples
