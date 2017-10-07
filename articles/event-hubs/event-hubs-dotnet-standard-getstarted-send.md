---
title: "aaaSend eventos tooAzure Hubs de eventos usando .NET padrão | Microsoft Docs"
description: "Começar a enviar tooEvent Hubs de eventos no .NET padrão"
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/27/2017
ms.author: sethm
ms.openlocfilehash: caa9747a8a72aa8e7aea1348a116f6e4b406460e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-sending-messages-tooazure-event-hubs-in-net-standard"></a>Começar a enviar mensagens tooAzure Hubs de eventos no .NET padrão

> [!NOTE]
> Este exemplo está disponível em [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender).

Este tutorial mostra como toowrite um aplicativo de console .NET Core que envia um conjunto de mensagens tooan hub de eventos. Você pode executar Olá [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender) solução como-está, substituindo Olá `EhConnectionString` e `EhEntityPath` cadeias de caracteres com seus valores de hub de eventos. Ou você pode seguir Olá etapas neste tutorial toocreate seus próprios.

## <a name="prerequisites"></a>Pré-requisitos

* [Microsoft Visual Studio 2015 ou 2017](http://www.visualstudio.com). Também há suporte para este tutorial 2017 do Visual Studio, use os exemplos Hello, mas o Visual Studio 2015.
* [Ferramentas do .NET Core do Visual Studio 2015 ou 2017](http://www.microsoft.com/net/core).
* Uma assinatura do Azure.
* Um namespace do hub de eventos.

hub de eventos do toosend mensagens tooan, usaremos o Visual Studio toowrite um aplicativo de console c#.

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a>Criar um namespace de Hubs de Eventos e um hub de eventos

Olá primeira etapa é Olá toouse [portal do Azure](https://portal.azure.com) toocreate um namespace para o tipo do hub de evento Olá e obter credenciais de gerenciamento que seu aplicativo precisa toocommunicate com hub de eventos de saudação de saudação. toocreate um namespace e um hub de eventos, siga Olá procedimento [neste artigo](event-hubs-create.md)e continue com a saudação etapas a seguir.

## <a name="create-a-console-application"></a>Criar um aplicativo de console

Inicie o Visual Studio. De saudação **arquivo** menu, clique em **novo**e, em seguida, clique em **projeto**. Crie um aplicativo de console do .NET Core.

![Novo Projeto][1]

## <a name="add-hello-event-hubs-nuget-package"></a>Adicionar pacote de NuGet de Hubs de evento Olá

Adicionar Olá [ `Microsoft.Azure.EventHubs` ](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) .NET padrão biblioteca NuGet pacote tooyour projeto seguindo estas etapas: 

1. Clique com botão direito Olá recém-criado e selecione **gerenciar pacotes NuGet**.
2. Clique em Olá **procurar** guia, procure por "Microsoft.Azure.EventHubs" e selecione Olá **Microsoft.Azure.EventHubs** pacote. Clique em **instalar** toocomplete Olá instalação, em seguida, feche esta caixa de diálogo.

## <a name="write-some-code-toosend-messages-toohello-event-hub"></a>Gravar algumas hub de eventos do código toosend mensagens toohello

1. Adicione o seguinte Olá `using` superior de toohello instruções do arquivo Program.cs de saudação.

    ```csharp
    using Microsoft.Azure.EventHubs;
    using System.Text;
    using System.Threading.Tasks;
    ```

2. Adicionar constantes toohello `Program` classe para o hello Hubs de evento conexão cadeia de caracteres e entidade (nome de hub de evento individual). Substitua espaços reservados de saudação entre colchetes com valores adequados do hello obtidos ao criar o hub de eventos de saudação.

    ```csharp
    private static EventHubClient eventHubClient;
    private const string EhConnectionString = "{Event Hubs connection string}";
    private const string EhEntityPath = "{Event Hub path/name}";
    ```

3. Adicionar um novo método chamado `MainAsync` toohello `Program` classe, da seguinte maneira:

    ```csharp
    private static async Task MainAsync(string[] args)
    {
        // Creates an EventHubsConnectionStringBuilder object from hello connection string, and sets hello EntityPath.
        // Typically, hello connection string should have hello entity path in it, but for hello sake of this simple scenario
        // we are using hello connection string from hello namespace.
        var connectionStringBuilder = new EventHubsConnectionStringBuilder(EhConnectionString)
        {
            EntityPath = EhEntityPath
        };

        eventHubClient = EventHubClient.CreateFromConnectionString(connectionStringBuilder.ToString());

        await SendMessagesToEventHub(100);

        await eventHubClient.CloseAsync();

        Console.WriteLine("Press ENTER tooexit.");
        Console.ReadLine();
    }
    ```

4. Adicionar um novo método chamado `SendMessagesToEventHub` toohello `Program` classe, da seguinte maneira:

    ```csharp
    // Creates an event hub client and sends 100 messages toohello event hub.
    private static async Task SendMessagesToEventHub(int numMessagesToSend)
    {
        for (var i = 0; i < numMessagesToSend; i++)
        {
            try
            {
                var message = $"Message {i}";
                Console.WriteLine($"Sending message: {message}");
                await eventHubClient.SendAsync(new EventData(Encoding.UTF8.GetBytes(message)));
            }
            catch (Exception exception)
            {
                Console.WriteLine($"{DateTime.Now} > Exception: {exception.Message}");
            }

            await Task.Delay(10);
        }

        Console.WriteLine($"{numMessagesToSend} messages sent.");
    }
    ```

5. Adicionar Olá toohello de código a seguir `Main` método hello `Program` classe.

    ```csharp
    MainAsync(args).GetAwaiter().GetResult();
    ```

   Program.cs deve ficar assim.

    ```csharp
    namespace SampleSender
    {
        using System;
        using System.Text;
        using System.Threading.Tasks;
        using Microsoft.Azure.EventHubs;

        public class Program
        {
            private static EventHubClient eventHubClient;
            private const string EhConnectionString = "{Event Hubs connection string}";
            private const string EhEntityPath = "{Event Hub path/name}";

            public static void Main(string[] args)
            {
                MainAsync(args).GetAwaiter().GetResult();
            }

            private static async Task MainAsync(string[] args)
            {
                // Creates an EventHubsConnectionStringBuilder object from hello connection string, and sets hello EntityPath.
                // Typically, hello connection string should have hello entity path in it, but for hello sake of this simple scenario
                // we are using hello connection string from hello namespace.
                var connectionStringBuilder = new EventHubsConnectionStringBuilder(EhConnectionString)
                {
                    EntityPath = EhEntityPath
                };

                eventHubClient = EventHubClient.CreateFromConnectionString(connectionStringBuilder.ToString());

                await SendMessagesToEventHub(100);

                await eventHubClient.CloseAsync();

                Console.WriteLine("Press ENTER tooexit.");
                Console.ReadLine();
            }

            // Creates an event hub client and sends 100 messages toohello event hub.
            private static async Task SendMessagesToEventHub(int numMessagesToSend)
            {
                for (var i = 0; i < numMessagesToSend; i++)
                {
                    try
                    {
                        var message = $"Message {i}";
                        Console.WriteLine($"Sending message: {message}");
                        await eventHubClient.SendAsync(new EventData(Encoding.UTF8.GetBytes(message)));
                    }
                    catch (Exception exception)
                    {
                        Console.WriteLine($"{DateTime.Now} > Exception: {exception.Message}");
                    }

                    await Task.Delay(10);
                }

                Console.WriteLine($"{numMessagesToSend} messages sent.");
            }
        }
    }
    ```

6. Executar programa hello e certifique-se de que não existem erros.

Parabéns! Agora você enviou hub de eventos de tooan de mensagens.

## <a name="next-steps"></a>Próximas etapas
Você pode aprender mais sobre os Hubs de eventos visitando Olá links a seguir:

* [Receber eventos de Hubs de Eventos](event-hubs-dotnet-standard-getstarted-receive-eph.md)
* [Visão Geral dos Hubs de Eventos](event-hubs-what-is-event-hubs.md)
* [Criar um hub de eventos](event-hubs-create.md)
* [Perguntas frequentes sobre os Hubs de Eventos](event-hubs-faq.md)

[1]: ./media/event-hubs-dotnet-standard-getstarted-send/netcore.png
