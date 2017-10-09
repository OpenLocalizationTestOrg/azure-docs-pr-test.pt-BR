---
title: "aaaGet iniciado com assinaturas e tópicos do barramento de serviço do Azure | Microsoft Docs"
description: "Escreva um aplicativo de console em C# que usa tópicos e assinaturas de mensagens do Barramento de Serviço."
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: hero-article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 06/30/2017
ms.author: sethm
ms.openlocfilehash: 619d602599d97ecff2ded0681a383b19f1a8b7ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-service-bus-topics"></a>Introdução aos tópicos do Barramento de Serviço

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

## <a name="what-will-be-accomplished"></a>O que será realizado

Este tutorial aborda Olá etapas a seguir:

1. Crie um namespace de barramento de serviço, usando Olá portal do Azure.
2. Crie um tópico do barramento de serviço, usando Olá portal do Azure.
3. Crie um tópico de toothat de assinatura do barramento de serviço, usando Olá portal do Azure.
4. Escreva um toosend do aplicativo de console em um tópico de toohello de mensagem.
5. Escreva um tooreceive do aplicativo de console que uma mensagem de assinatura de saudação.

## <a name="prerequisites"></a>Pré-requisitos

1. [Visual Studio 2015 ou superior](http://www.visualstudio.com). exemplos de saudação neste tutorial usam 2017 do Visual Studio.
2. Uma assinatura do Azure.

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-hello-azure-portal"></a>1. Criar um namespace usando Olá portal do Azure

Se você já tiver criado um namespace do sistema de mensagens do barramento de serviço, ir toohello [criar um tópico usando o portal do Azure de saudação](#2-create-a-topic-using-the-azure-portal) seção.

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="2-create-a-topic-using-hello-azure-portal"></a>2. Criar um tópico usando Olá portal do Azure

1. Faça logon no toohello [portal do Azure][azure-portal].
2. No painel de navegação à esquerda de saudação do portal de saudação, clique em **Service Bus** (se você não vir **Service Bus**, clique em **mais serviços**).
3. Clique em Olá namespace em que você gostaria que o tópico de saudação toocreate. folha de visão geral do namespace Olá aparece:
   
    ![Criar um tópico][createtopic1]
4. Em Olá **namespace de barramento de serviço** folha, clique em **tópicos**, em seguida, clique em **Adicionar tópico**.
   
    ![Selecionar tópicos][createtopic2]
5. Insira um nome para o tópico hello e desmarque Olá **ativar particionamento** opção. Deixe Olá outras opções com seus valores padrão.
   
    ![Selecionar Nova][createtopic3]
6. Na parte inferior de saudação da folha de saudação, clique em **criar**.

## <a name="3-create-a-subscription-toohello-topic"></a>3. Criar um tópico de toohello de assinatura

1. No painel de recursos de portal hello, clique Olá namespace criado na etapa 1, clique em nome do tópico Olá criado na etapa 2.
2. Um top de saudação do painel de visão geral do hello, clique hello mais entrar Avançar muito**assinatura** tooadd um tópico de toothis de assinatura.

    ![Criar assinatura][createtopic4]

3. Insira um nome para a assinatura de saudação. Deixe Olá outras opções com seus valores padrão.

## <a name="4-send-messages-toohello-topic"></a>4. Enviar tópico toohello de mensagens

tópico de toohello mensagens toosend, podemos gravar um aplicativo de console c# usando o Visual Studio.

### <a name="create-a-console-application"></a>Criar um aplicativo de console

Inicie o Visual Studio e crie um novo projeto de **Aplicativo de console (.NET Framework)**.

### <a name="add-hello-service-bus-nuget-package"></a>Adicionar o pacote do NuGet do barramento de serviço Olá

1. Clique com botão direito Olá recém-criado e selecione **gerenciar pacotes NuGet**.
2. Clique em Olá **procurar** guia, procure **barramento de serviço do Microsoft Azure**e, em seguida, selecione Olá **windowsazure. ServiceBus** item. Clique em **instalar** toocomplete Olá instalação, em seguida, feche esta caixa de diálogo.
   
    ![Selecionar um pacote NuGet][nuget-pkg]

### <a name="write-some-code-toosend-a-message-toohello-topic"></a>Escrever algum código toosend um tópico de toohello de mensagem

1. Adicione o seguinte Olá `using` superior de toohello de instrução do arquivo Program.cs de saudação.
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
2. Adicionar Olá toohello de código a seguir `Main` método. Saudação de conjunto `connectionString` conexão toohello variável de cadeia de caracteres obtido ao criar namespace hello e definir `topicName` toohello nome que você usou ao criar tópico hello.
   
    ```csharp
    var connectionString = "<your connection string>";
    var topicName = "<your topic name>";
   
    var client = TopicClient.CreateFromConnectionString(connectionString, topicName);
    var message = new BrokeredMessage("This is a test message!");

    Console.WriteLine(String.Format("Message body: {0}", message.GetBody<String>()));
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

    namespace tsend
    {
        class Program
        {
            static void Main(string[] args)
            {
                var connectionString = "Endpoint=sb://<your namespace>.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=<your key>";
                var topicName = "<your topic name>";

                var client = TopicClient.CreateFromConnectionString(connectionString, topicName);
                var message = new BrokeredMessage("This is a test message!");

                Console.WriteLine(String.Format("Message body: {0}", message.GetBody<String>()));
                Console.WriteLine(String.Format("Message id: {0}", message.MessageId));

                client.Send(message);

                Console.WriteLine("Message successfully sent! Press ENTER tooexit program");
                Console.ReadLine();
            }
        }
    }
    ```
3. Execute o programa hello e verifique Olá portal do Azure: clique em nome de saudação do seu tópico no namespace Olá **visão geral** folha. tópico de saudação **Essentials** folha é exibida. Olá assinatura (s) listado inferior Olá da folha de hello, observe que Olá **contagem de mensagem** valor para cada assinatura agora deve ser 1. Cada vez que você executar o aplicativo de remetente hello sem recuperar mensagens de saudação (conforme descrito na próxima seção, Olá), esse valor aumenta em 1. Observe também que tamanho atual da saudação de Olá Olá de incrementos de tópico **atual** valor Olá **Essentials** folha sempre que o aplicativo hello adiciona uma mensagem toohello tópico/assinatura.
   
      ![Tamanho da mensagem][topic-message]

## <a name="5-receive-messages-from-hello-subscription"></a>5. Receber mensagens de saudação assinatura

1. mensagem de saudação tooreceive ou as mensagens enviadas apenas, criar um novo aplicativo de console e adicionar um pacote de NuGet do barramento de serviço do toohello de referência, aplicativo de remetente anterior toohello semelhante.
2. Adicione o seguinte Olá `using` superior de toohello de instrução do arquivo Program.cs de saudação.
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
3. Adicionar Olá toohello de código a seguir `Main` método. Saudação de conjunto `connectionString` conexão toohello variável de cadeia de caracteres é obtido durante a criação de namespace hello e defina `topicName` toohello nome que você usou ao criar tópico hello.
   
    ```csharp
    var connectionString = "<your connection string>";
    var topicName = "<your topic name>";
   
    var client = SubscriptionClient.CreateFromConnectionString(connectionString, topicName, "<your subscription name>");
   
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
   
    namespace GettingStartedWithTopics
    {
      class Program
      {
        static void Main(string[] args)
        {
          var connectionString = "Endpoint=sb://<your namespace>.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=<your key>";;
          var topicName = "<your topic name>";
   
          var client = SubscriptionClient.CreateFromConnectionString(connectionString, topicName, "<your subscription name>");
   
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
4. Executar programa hello e verificar novamente o portal de saudação. Observe que Olá **contagem de mensagem** e **atual** valores agora são 0.
   
    ![Tamanho do tópico][topic-message-receive]

Parabéns! Agora você criou um tópico e uma assinatura, enviou uma mensagem e recebeu essa mensagem.

## <a name="next-steps"></a>Próximas etapas

Confira nosso [repositório GitHub com exemplos](https://github.com/Azure/azure-service-bus/tree/master/samples) que demonstram algumas das mais recursos avançados do barramento de serviço de mensagens de saudação.

<!--Image references-->

[nuget-pkg]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/nuget-package.png
[topic-message]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/topic-message.png
[topic-message-receive]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/topic-message-receive.png
[createtopic1]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/create-topic1.png
[createtopic2]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/create-topic2.png
[createtopic3]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/create-topic3.png
[createtopic4]: ./media/service-bus-dotnet-how-to-use-topics-subscriptions/create-topic4.png
[github-samples]: https://github.com/Azure-Samples/azure-servicebus-messaging-samples
[azure-portal]: https://portal.azure.com
