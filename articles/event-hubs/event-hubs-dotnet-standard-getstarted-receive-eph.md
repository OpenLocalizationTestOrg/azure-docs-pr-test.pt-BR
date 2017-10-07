---
title: "eventos de aaaReceive de Hubs de eventos do Azure usando .NET padrão | Microsoft Docs"
description: "Começar a receber mensagens com hello EventProcessorHost no .NET padrão"
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
ms.openlocfilehash: c3983f2668ac8f65522e44a1609dfd2eed31b7d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-receiving-messages-with-hello-event-processor-host-in-net-standard"></a>Começar a receber mensagens com hello Host de processador de eventos no .NET padrão

> [!NOTE]
> Este exemplo está disponível em [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver).

Este tutorial mostra como o aplicativo que recebe mensagens de um hub de eventos por meio de console toowrite um .NET Core **EventProcessorHost**. Você pode executar Olá [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) solução como-é, substituindo cadeias de caracteres de saudação com seus valores de conta de armazenamento e hub de eventos. Ou você pode seguir Olá etapas neste tutorial toocreate seus próprios.

## <a name="prerequisites"></a>Pré-requisitos

* [Microsoft Visual Studio 2015 ou 2017](http://www.visualstudio.com). Também há suporte para este tutorial 2017 do Visual Studio, use os exemplos Hello, mas o Visual Studio 2015.
* [Ferramentas do .NET Core do Visual Studio 2015 ou 2017](http://www.microsoft.com/net/core).
* Uma assinatura do Azure.
* Um namespace dos Hubs de Eventos do Azure.
* Uma conta de armazenamento do Azure.

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a>Criar um namespace de Hubs de Eventos e um hub de eventos  

Olá primeira etapa é Olá toouse [portal do Azure](https://portal.azure.com) toocreate um namespace para Olá Hubs de eventos de tipo e obter Olá credenciais de gerenciamento que seu aplicativo precisa toocommunicate com hub de eventos de saudação. toocreate um namespace e hub de eventos, siga o procedimento Olá [neste artigo](event-hubs-create.md)e continue com a saudação etapas a seguir.  

## <a name="create-an-azure-storage-account"></a>Criar uma conta de armazenamento do Azure  

1. Entrar toohello [portal do Azure](https://portal.azure.com).  
2. No painel de navegação à esquerda de saudação do portal de saudação, clique em **novo**, clique em **armazenamento**e, em seguida, clique em **conta de armazenamento**.  
3. Preencha os campos de saudação na folha de conta de armazenamento hello e, em seguida, clique em **criar**.

    ![Criar Conta de Armazenamento][1]

4. Depois de ver Olá **implantações bem-sucedida** , clique em nome de Olá Olá novo da conta de armazenamento. Em Olá **Essentials** folha, clique em **Blobs**. Olá quando **do serviço Blob** folha é aberto, clique em **+ contêiner** na parte superior da saudação. Dê um nome de contêiner de saudação e feche Olá **do serviço Blob** folha.  
5. Clique em **chaves de acesso** Olá esquerdo folha e cópia Olá nome do contêiner de armazenamento de saudação, conta de armazenamento hello e valor de saudação do **key1**. Salve tooNotepad esses valores ou algum outro local temporário.  

## <a name="create-a-console-application"></a>Criar um aplicativo de console

Inicie o Visual Studio. De saudação **arquivo** menu, clique em **novo**e, em seguida, clique em **projeto**. Crie um aplicativo de console do .NET Core.

![Novo Projeto][2]

## <a name="add-hello-event-hubs-nuget-package"></a>Adicionar pacote de NuGet de Hubs de evento Olá

Adicionar Olá [ `Microsoft.Azure.EventHubs` ](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) e [ `Microsoft.Azure.EventHubs.Processor` ](https://www.nuget.org/packages/Microsoft.Azure.EventHubs.Processor/) .NET biblioteca NuGet pacotes tooyour projeto padrão seguindo estas etapas: 

1. Clique com botão direito Olá recém-criado e selecione **gerenciar pacotes NuGet**.
2. Clique em Olá **procurar** guia, procure por "Microsoft.Azure.EventHubs" e selecione Olá **Microsoft.Azure.EventHubs** pacote. Clique em **instalar** toocomplete Olá instalação, em seguida, feche esta caixa de diálogo.
3. Repita as etapas 1 e 2 e instalar Olá **Microsoft.Azure.EventHubs.Processor** pacote.

## <a name="implement-hello-ieventprocessor-interface"></a>Implementa a interface IEventProcessor Olá

1. No Gerenciador de soluções, projetos de saudação com o botão direito, clique em **adicionar**e, em seguida, clique em **classe**. Nomeie a nova classe de saudação **SimpleEventProcessor**.

2. Abrir o arquivo de SimpleEventProcessor.cs hello e adicione o seguinte Olá `using` superior de toohello de instruções do arquivo hello.

    ```csharp
    using Microsoft.Azure.EventHubs;
    using Microsoft.Azure.EventHubs.Processor;
    using System.Threading.Tasks;
    ```

3. Saudação de implementar `IEventProcessor` interface. Substitua todo o conteúdo do Olá Olá `SimpleEventProcessor` classe com hello código a seguir:

    ```csharp
    public class SimpleEventProcessor : IEventProcessor
    {
        public Task CloseAsync(PartitionContext context, CloseReason reason)
        {
            Console.WriteLine($"Processor Shutting Down. Partition '{context.PartitionId}', Reason: '{reason}'.");
            return Task.CompletedTask;
        }

        public Task OpenAsync(PartitionContext context)
        {
            Console.WriteLine($"SimpleEventProcessor initialized. Partition: '{context.PartitionId}'");
            return Task.CompletedTask;
        }

        public Task ProcessErrorAsync(PartitionContext context, Exception error)
        {
            Console.WriteLine($"Error on Partition: {context.PartitionId}, Error: {error.Message}");
            return Task.CompletedTask;
        }

        public Task ProcessEventsAsync(PartitionContext context, IEnumerable<EventData> messages)
        {
            foreach (var eventData in messages)
            {
                var data = Encoding.UTF8.GetString(eventData.Body.Array, eventData.Body.Offset, eventData.Body.Count);
                Console.WriteLine($"Message received. Partition: '{context.PartitionId}', Data: '{data}'");
            }

            return context.CheckpointAsync();
        }
    }
    ```

## <a name="write-a-main-console-method-that-uses-hello-simpleeventprocessor-class-tooreceive-messages"></a>Escrever um método do console principal que usa mensagens de saudação do SimpleEventProcessor classe tooreceive

1. Adicione o seguinte Olá `using` superior de toohello instruções do arquivo Program.cs de saudação.

    ```csharp
    using Microsoft.Azure.EventHubs;
    using Microsoft.Azure.EventHubs.Processor;
    using System.Threading.Tasks;
    ```

2. Adicionar constantes toohello `Program` classe para a cadeia de conexão de hub de evento Olá, nome do hub de evento, nome do contêiner de conta de armazenamento, nome da conta de armazenamento e chave de conta de armazenamento. Adicione Olá código a seguir, substituindo espaços reservados de saudação com seus valores correspondentes.

    ```csharp
    private const string EhConnectionString = "{Event Hubs connection string}";
    private const string EhEntityPath = "{Event Hub path/name}";
    private const string StorageContainerName = "{Storage account container name}";
    private const string StorageAccountName = "{Storage account name}";
    private const string StorageAccountKey = "{Storage account key}";

    private static readonly string StorageConnectionString = string.Format("DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}", StorageAccountName, StorageAccountKey);
    ```   

3. Adicionar um novo método chamado `MainAsync` toohello `Program` classe, da seguinte maneira:

    ```csharp
    private static async Task MainAsync(string[] args)
    {
        Console.WriteLine("Registering EventProcessor...");

        var eventProcessorHost = new EventProcessorHost(
            EhEntityPath,
            PartitionReceiver.DefaultConsumerGroupName,
            EhConnectionString,
            StorageConnectionString,
            StorageContainerName);

        // Registers hello Event Processor Host and starts receiving messages
        await eventProcessorHost.RegisterEventProcessorAsync<SimpleEventProcessor>();

        Console.WriteLine("Receiving. Press ENTER toostop worker.");
        Console.ReadLine();

        // Disposes of hello Event Processor Host
        await eventProcessorHost.UnregisterEventProcessorAsync();
    }
    ```

3. Adicione a seguinte linha de código toohello de saudação `Main` método:

    ```csharp
    MainAsync(args).GetAwaiter().GetResult();
    ```

    O arquivo Program.cs deve ficar assim:

    ```csharp
    namespace SampleEphReceiver
    {

        public class Program
        {
            private const string EhConnectionString = "{Event Hubs connection string}";
            private const string EhEntityPath = "{Event Hub path/name}";
            private const string StorageContainerName = "{Storage account container name}";
            private const string StorageAccountName = "{Storage account name}";
            private const string StorageAccountKey = "{Storage account key}";

            private static readonly string StorageConnectionString = string.Format("DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}", StorageAccountName, StorageAccountKey);

            public static void Main(string[] args)
            {
                MainAsync(args).GetAwaiter().GetResult();
            }

            private static async Task MainAsync(string[] args)
            {
                Console.WriteLine("Registering EventProcessor...");

                var eventProcessorHost = new EventProcessorHost(
                    EhEntityPath,
                    PartitionReceiver.DefaultConsumerGroupName,
                    EhConnectionString,
                    StorageConnectionString,
                    StorageContainerName);

                // Registers hello Event Processor Host and starts receiving messages
                await eventProcessorHost.RegisterEventProcessorAsync<SimpleEventProcessor>();

                Console.WriteLine("Receiving. Press ENTER toostop worker.");
                Console.ReadLine();

                // Disposes of hello Event Processor Host
                await eventProcessorHost.UnregisterEventProcessorAsync();
            }
        }
    }
    ```

4. Executar programa hello e certifique-se de que não existem erros.

Parabéns! Você agora recebeu mensagens de um hub de eventos usando Olá Host de processador de evento.

## <a name="next-steps"></a>Próximas etapas
Você pode aprender mais sobre os Hubs de eventos visitando Olá links a seguir:

* [Visão Geral dos Hubs de Eventos](event-hubs-what-is-event-hubs.md)
* [Criar um hub de eventos](event-hubs-create.md)
* [Perguntas frequentes sobre os Hubs de Eventos](event-hubs-faq.md)

[1]: ./media/event-hubs-dotnet-standard-getstarted-receive-eph/event-hubs-python1.png
[2]: ./media/event-hubs-dotnet-standard-getstarted-receive-eph/netcore.png
