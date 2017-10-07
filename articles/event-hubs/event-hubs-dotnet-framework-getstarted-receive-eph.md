---
title: "eventos de aaaReceive de Hubs de eventos do Azure usando Olá do .NET Framework | Microsoft Docs"
description: "Siga este tutorial tooreceive eventos de Hubs de eventos do Azure usando a saudação do .NET Framework."
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: c4974bd3-2a79-48a1-aa3b-8ee2d6655b28
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/12/2017
ms.author: sethm
ms.openlocfilehash: a88c3feeacfd3de9622dbb86e25222e861750204
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="receive-events-from-azure-event-hubs-using-hello-net-framework"></a>Receber eventos de Hubs de eventos do Azure usando a saudação do .NET Framework

## <a name="introduction"></a>Introdução

Os Hubs de Eventos são um serviço que processa grandes quantidades de dados de eventos (telemetria) a partir de aplicativos e dispositivos conectados. Depois de coletar dados para Hubs de eventos, você pode armazenar dados de saudação usando um cluster de armazenamento ou transformá-lo usando um provedor de análise em tempo real. Essa capacidade de coleta e processamento de evento em grande escala é um componente fundamental de arquiteturas de aplicativo moderno incluindo Olá Internet das coisas (IoT).

Este tutorial mostra como o aplicativo que recebe mensagens de um hub de eventos usando Olá de console toowrite um .NET Framework  **[Host de processador de evento][EventProcessorHost]**. eventos de toosend usando saudação do .NET Framework, consulte Olá [enviar eventos tooAzure Hubs de eventos usando saudação do .NET Framework](event-hubs-dotnet-framework-getstarted-send.md) artigo ou clique em idioma de envio apropriado Olá Olá esquerdo sumário.

Olá [Host de processador de evento] [ EventProcessorHost] é uma classe .NET que simplifica a receba eventos dos hubs de eventos por meio do gerenciamento de pontos de verificação persistentes e paralelo recebe dos hubs de eventos. Usando Olá [Host de processador de evento][Event Processor Host], você pode dividir eventos em vários destinatários, mesmo quando hospedados em nós diferentes. Este exemplo mostra como Olá toouse [Host de processador de evento] [ EventProcessorHost] para um único destinatário. Olá [expansão de processamento de eventos] [ Scale out Event Processing with Event Hubs] de exemplo mostra como Olá toouse [Host de processador de evento] [ EventProcessorHost] com vários destinatários.

## <a name="prerequisites"></a>Pré-requisitos

toocomplete neste tutorial, você precisa Olá pré-requisitos a seguir:

* [Microsoft Visual Studio 2015 ou superior](http://visualstudio.com). capturas de tela de saudação neste tutorial usam 2017 do Visual Studio.
* Uma conta ativa do Azure. Se não tiver uma, você poderá criar uma conta gratuita em apenas alguns minutos. Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/free/).

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a>Criar um namespace de Hubs de Eventos e um hub de eventos

Olá primeira etapa é Olá toouse [portal do Azure](https://portal.azure.com) toocreate um namespace do tipo de Hubs de eventos e obter Olá toocommunicate com hub de eventos de saudação do seu aplicativo precisa de credenciais de gerenciamento. toocreate um namespace e hub de eventos, siga o procedimento Olá [neste artigo](event-hubs-create.md), continue com a saudação seguindo as etapas neste tutorial.

## <a name="create-an-azure-storage-account"></a>Criar uma conta de Armazenamento do Azure

Olá toouse [Host de processador de evento][EventProcessorHost], você deve ter uma [conta de armazenamento do Azure][Azure Storage account]:

1. Faça logon no toohello [portal do Azure][Azure portal]e clique em **novo** em Olá superior esquerda da tela hello.
2. Clique em **Armazenamento** e em **conta de Armazenamento**.
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage1.png)
3. Em Olá **criar conta de armazenamento** folha, digite um nome para a conta de armazenamento hello. Escolha uma assinatura do Azure, o grupo de recursos e o local no qual recurso de saudação toocreate. Em seguida, clique em **Criar**.
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage2.png)
4. Na lista de saudação de contas de armazenamento, clique Olá recentemente criado a conta de armazenamento.
5. Na folha de conta de armazenamento hello, clique em **chaves de acesso**. Copie o valor de saudação do **key1** toouse posteriormente neste tutorial.
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage3.png)

## <a name="create-a-receiver-console-application"></a>Criar um aplicativo de console do destinatário

1. No Visual Studio, crie um novo projeto de aplicativo de área de trabalho do Visual C# usando Olá **aplicativo de Console** modelo de projeto. Projeto de saudação do nome **receptor**.
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-receiver-csharp1.png)
2. No Gerenciador de soluções, clique com botão direito Olá **receptor** do projeto e, em seguida, clique em **gerenciar pacotes NuGet para solução**.
3. Clique em Olá **procurar** guia e, em seguida, procurar `Microsoft Azure Service Bus Event Hub - EventProcessorHost`. Clique em **instalar**e aceite os termos de uso do hello.
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-eph-csharp1.png)
   
    Downloads do Visual Studio, instala e adiciona uma referência toohello [Hub de eventos de barramento de serviço do Azure - pacote EventProcessorHost NuGet](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost), com todas as suas dependências.
4. Saudação de atalho **receptor** de projeto, clique em **adicionar**e, em seguida, clique em **classe**. Nomeie a nova classe de saudação **SimpleEventProcessor**e, em seguida, clique em **adicionar** toocreate classe de saudação.
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-receiver-csharp2.png)
5. Adicione Olá seguindo as instruções na parte superior de saudação do arquivo de SimpleEventProcessor.cs hello:
    
  ```csharp
  using Microsoft.ServiceBus.Messaging;
  using System.Diagnostics;
  ```
    
  Em seguida, substitua Olá código para o corpo de saudação da classe Olá a seguir:
    
  ```csharp
  class SimpleEventProcessor : IEventProcessor
  {
    Stopwatch checkpointStopWatch;
    
    async Task IEventProcessor.CloseAsync(PartitionContext context, CloseReason reason)
    {
        Console.WriteLine("Processor Shutting Down. Partition '{0}', Reason: '{1}'.", context.Lease.PartitionId, reason);
        if (reason == CloseReason.Shutdown)
        {
            await context.CheckpointAsync();
        }
    }
    
    Task IEventProcessor.OpenAsync(PartitionContext context)
    {
        Console.WriteLine("SimpleEventProcessor initialized.  Partition: '{0}', Offset: '{1}'", context.Lease.PartitionId, context.Lease.Offset);
        this.checkpointStopWatch = new Stopwatch();
        this.checkpointStopWatch.Start();
        return Task.FromResult<object>(null);
    }
    
    async Task IEventProcessor.ProcessEventsAsync(PartitionContext context, IEnumerable<EventData> messages)
    {
        foreach (EventData eventData in messages)
        {
            string data = Encoding.UTF8.GetString(eventData.GetBytes());
    
            Console.WriteLine(string.Format("Message received.  Partition: '{0}', Data: '{1}'",
                context.Lease.PartitionId, data));
        }
    
        //Call checkpoint every 5 minutes, so that worker can resume processing from 5 minutes back if it restarts.
        if (this.checkpointStopWatch.Elapsed > TimeSpan.FromMinutes(5))
        {
            await context.CheckpointAsync();
            this.checkpointStopWatch.Restart();
        }
    }
  }
  ```
    
  Essa classe é chamada pelo Olá **EventProcessorHost** tooprocess eventos recebidos de hub de eventos de saudação. Olá `SimpleEventProcessor` classe usa um método de ponto de verificação stopwatch tooperiodically chamada hello em Olá **EventProcessorHost** contexto. Esse processamento garante que, receptor Olá for reiniciado, ele perde não mais de cinco minutos do trabalho de processamento.
6. Em Olá **programa** de classe, adicione o seguinte Olá `using` instrução na parte superior de saudação do arquivo hello:
    
  ```csharp
  using Microsoft.ServiceBus.Messaging;
  ```
    
  Em seguida, substitua Olá `Main` método hello `Program` classe com hello código a seguir, substituindo o nome do hub de evento hello e conexão de nível de namespace de saudação de cadeia de caracteres que você salvou anteriormente e Olá conta de armazenamento e a chave que você copiou na Olá seções anteriores. 
    
  ```csharp
  static void Main(string[] args)
  {
    string eventHubConnectionString = "{Event Hubs namespace connection string}";
    string eventHubName = "{Event Hub name}";
    string storageAccountName = "{storage account name}";
    string storageAccountKey = "{storage account key}";
    string storageConnectionString = string.Format("DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}", storageAccountName, storageAccountKey);
    
    string eventProcessorHostName = Guid.NewGuid().ToString();
    EventProcessorHost eventProcessorHost = new EventProcessorHost(eventProcessorHostName, eventHubName, EventHubConsumerGroup.DefaultGroupName, eventHubConnectionString, storageConnectionString);
    Console.WriteLine("Registering EventProcessor...");
    var options = new EventProcessorOptions();
    options.ExceptionReceived += (sender, e) => { Console.WriteLine(e.Exception); };
    eventProcessorHost.RegisterEventProcessorAsync<SimpleEventProcessor>(options).Wait();
    
    Console.WriteLine("Receiving. Press enter key toostop worker.");
    Console.ReadLine();
    eventProcessorHost.UnregisterEventProcessorAsync().Wait();
  }
  ```

7. Executar programa hello e certifique-se de que não existem erros.
  
Parabéns! Agora, você recebeu mensagens de um hub de eventos usando Olá Host de processador de evento.


> [!NOTE]
> Este tutorial usa uma única instância do [EventProcessorHost][EventProcessorHost]. taxa de transferência tooincrease, é recomendável que você execute várias instâncias do [EventProcessorHost][EventProcessorHost], conforme mostrado no hello [escala processamento do evento] [escala processamento do evento] exemplo. Nesses casos, hello várias instâncias automaticamente coordenam uns com os outros eventos do tooload saldo Olá recebida. Se você quiser que o processo de tooeach vários destinatários *todos os* Olá eventos, você deve usar o hello **o ConsumerGroup** conceito. Ao receber eventos em máquinas diferentes, talvez seja útil toospecify nomes para [EventProcessorHost] [ EventProcessorHost] instâncias com base em máquinas hello (ou funções) no qual eles foram implantados. Para obter mais informações sobre esses tópicos, consulte Olá [visão geral de Hubs de eventos] [ Event Hubs overview] e hello [guia de programação de Hubs de eventos] [ Event Hubs Programming Guide] tópicos.
> 
> 

## <a name="next-steps"></a>Próximas etapas

Agora que você construiu um aplicativo de trabalho que cria um hub de eventos e envia e recebe dados, você pode saber mais, visite Olá links a seguir:

* [Host do Processador de Eventos][Event Processor Host]
* [Visão Geral dos Hubs de Eventos][Event Hubs overview]
* [Perguntas frequentes sobre os Hubs de Eventos](event-hubs-faq.md)

<!-- Images. -->
[19]: ./media/event-hubs-csharp-ephcs-getstarted/create-eh-proj1.png
[20]: ./media/event-hubs-csharp-ephcs-getstarted/create-eh-proj2.png
[21]: ./media/event-hubs-csharp-ephcs-getstarted/run-csharp-ephcs1.png
[22]: ./media/event-hubs-csharp-ephcs-getstarted/run-csharp-ephcs2.png

<!-- Links -->
[EventProcessorHost]: https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost
[Event Hubs overview]: event-hubs-what-is-event-hubs.md
[Scale out Event Processing with Event Hubs]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-45f43fc3
[Event Hubs Programming Guide]: event-hubs-programming-guide.md
[Azure Storage account]:../storage/common/storage-create-storage-account.md
[Event Processor Host]: /dotnet/api/microsoft.servicebus.messaging.eventprocessorhost
[Azure portal]: https://portal.azure.com
