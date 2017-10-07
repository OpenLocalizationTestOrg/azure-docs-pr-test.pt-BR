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
# <a name="receive-events-from-azure-event-hubs-using-hello-net-framework"></a><span data-ttu-id="3a15e-103">Receber eventos de Hubs de eventos do Azure usando a saudação do .NET Framework</span><span class="sxs-lookup"><span data-stu-id="3a15e-103">Receive events from Azure Event Hubs using hello .NET Framework</span></span>

## <a name="introduction"></a><span data-ttu-id="3a15e-104">Introdução</span><span class="sxs-lookup"><span data-stu-id="3a15e-104">Introduction</span></span>

<span data-ttu-id="3a15e-105">Os Hubs de Eventos são um serviço que processa grandes quantidades de dados de eventos (telemetria) a partir de aplicativos e dispositivos conectados.</span><span class="sxs-lookup"><span data-stu-id="3a15e-105">Event Hubs is a service that processes large amounts of event data (telemetry) from connected devices and applications.</span></span> <span data-ttu-id="3a15e-106">Depois de coletar dados para Hubs de eventos, você pode armazenar dados de saudação usando um cluster de armazenamento ou transformá-lo usando um provedor de análise em tempo real.</span><span class="sxs-lookup"><span data-stu-id="3a15e-106">After you collect data into Event Hubs, you can store hello data using a storage cluster or transform it using a real-time analytics provider.</span></span> <span data-ttu-id="3a15e-107">Essa capacidade de coleta e processamento de evento em grande escala é um componente fundamental de arquiteturas de aplicativo moderno incluindo Olá Internet das coisas (IoT).</span><span class="sxs-lookup"><span data-stu-id="3a15e-107">This large-scale event collection and processing capability is a key component of modern application architectures including hello Internet of Things (IoT).</span></span>

<span data-ttu-id="3a15e-108">Este tutorial mostra como o aplicativo que recebe mensagens de um hub de eventos usando Olá de console toowrite um .NET Framework  **[Host de processador de evento][EventProcessorHost]**.</span><span class="sxs-lookup"><span data-stu-id="3a15e-108">This tutorial shows how toowrite a .NET Framework console application that receives messages from an event hub using hello **[Event Processor Host][EventProcessorHost]**.</span></span> <span data-ttu-id="3a15e-109">eventos de toosend usando saudação do .NET Framework, consulte Olá [enviar eventos tooAzure Hubs de eventos usando saudação do .NET Framework](event-hubs-dotnet-framework-getstarted-send.md) artigo ou clique em idioma de envio apropriado Olá Olá esquerdo sumário.</span><span class="sxs-lookup"><span data-stu-id="3a15e-109">toosend events using hello .NET Framework, see hello [Send events tooAzure Event Hubs using hello .NET Framework](event-hubs-dotnet-framework-getstarted-send.md) article, or click hello appropriate sending language in hello left-hand table of contents.</span></span>

<span data-ttu-id="3a15e-110">Olá [Host de processador de evento] [ EventProcessorHost] é uma classe .NET que simplifica a receba eventos dos hubs de eventos por meio do gerenciamento de pontos de verificação persistentes e paralelo recebe dos hubs de eventos.</span><span class="sxs-lookup"><span data-stu-id="3a15e-110">hello [Event Processor Host][EventProcessorHost] is a .NET class that simplifies receiving events from event hubs by managing persistent checkpoints and parallel receives from those event hubs.</span></span> <span data-ttu-id="3a15e-111">Usando Olá [Host de processador de evento][Event Processor Host], você pode dividir eventos em vários destinatários, mesmo quando hospedados em nós diferentes.</span><span class="sxs-lookup"><span data-stu-id="3a15e-111">Using hello [Event Processor Host][Event Processor Host], you can split events across multiple receivers, even when hosted in different nodes.</span></span> <span data-ttu-id="3a15e-112">Este exemplo mostra como Olá toouse [Host de processador de evento] [ EventProcessorHost] para um único destinatário.</span><span class="sxs-lookup"><span data-stu-id="3a15e-112">This example shows how toouse hello [Event Processor Host][EventProcessorHost] for a single receiver.</span></span> <span data-ttu-id="3a15e-113">Olá [expansão de processamento de eventos] [ Scale out Event Processing with Event Hubs] de exemplo mostra como Olá toouse [Host de processador de evento] [ EventProcessorHost] com vários destinatários.</span><span class="sxs-lookup"><span data-stu-id="3a15e-113">hello [Scale out event processing][Scale out Event Processing with Event Hubs] sample shows how toouse hello [Event Processor Host][EventProcessorHost] with multiple receivers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3a15e-114">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="3a15e-114">Prerequisites</span></span>

<span data-ttu-id="3a15e-115">toocomplete neste tutorial, você precisa Olá pré-requisitos a seguir:</span><span class="sxs-lookup"><span data-stu-id="3a15e-115">toocomplete this tutorial, you need hello following prerequisites:</span></span>

* <span data-ttu-id="3a15e-116">[Microsoft Visual Studio 2015 ou superior](http://visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="3a15e-116">[Microsoft Visual Studio 2015 or higher](http://visualstudio.com).</span></span> <span data-ttu-id="3a15e-117">capturas de tela de saudação neste tutorial usam 2017 do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3a15e-117">hello screen shots in this tutorial use Visual Studio 2017.</span></span>
* <span data-ttu-id="3a15e-118">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="3a15e-118">An active Azure account.</span></span> <span data-ttu-id="3a15e-119">Se não tiver uma, você poderá criar uma conta gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="3a15e-119">If you don't have one, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="3a15e-120">Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="3a15e-120">For details, see [Azure Free Trial](https://azure.microsoft.com/free/).</span></span>

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a><span data-ttu-id="3a15e-121">Criar um namespace de Hubs de Eventos e um hub de eventos</span><span class="sxs-lookup"><span data-stu-id="3a15e-121">Create an Event Hubs namespace and an event hub</span></span>

<span data-ttu-id="3a15e-122">Olá primeira etapa é Olá toouse [portal do Azure](https://portal.azure.com) toocreate um namespace do tipo de Hubs de eventos e obter Olá toocommunicate com hub de eventos de saudação do seu aplicativo precisa de credenciais de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="3a15e-122">hello first step is toouse hello [Azure portal](https://portal.azure.com) toocreate a namespace of type Event Hubs, and obtain hello management credentials your application needs toocommunicate with hello event hub.</span></span> <span data-ttu-id="3a15e-123">toocreate um namespace e hub de eventos, siga o procedimento Olá [neste artigo](event-hubs-create.md), continue com a saudação seguindo as etapas neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="3a15e-123">toocreate a namespace and event hub, follow hello procedure in [this article](event-hubs-create.md), then proceed with hello following steps in this tutorial.</span></span>

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="3a15e-124">Criar uma conta de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="3a15e-124">Create an Azure Storage account</span></span>

<span data-ttu-id="3a15e-125">Olá toouse [Host de processador de evento][EventProcessorHost], você deve ter uma [conta de armazenamento do Azure][Azure Storage account]:</span><span class="sxs-lookup"><span data-stu-id="3a15e-125">toouse hello [Event Processor Host][EventProcessorHost], you must have an [Azure Storage account][Azure Storage account]:</span></span>

1. <span data-ttu-id="3a15e-126">Faça logon no toohello [portal do Azure][Azure portal]e clique em **novo** em Olá superior esquerda da tela hello.</span><span class="sxs-lookup"><span data-stu-id="3a15e-126">Log on toohello [Azure portal][Azure portal], and click **New** at hello top left of hello screen.</span></span>
2. <span data-ttu-id="3a15e-127">Clique em **Armazenamento** e em **conta de Armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="3a15e-127">Click **Storage**, then click **Storage account**.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage1.png)
3. <span data-ttu-id="3a15e-128">Em Olá **criar conta de armazenamento** folha, digite um nome para a conta de armazenamento hello.</span><span class="sxs-lookup"><span data-stu-id="3a15e-128">In hello **Create storage account** blade, type a name for hello storage account.</span></span> <span data-ttu-id="3a15e-129">Escolha uma assinatura do Azure, o grupo de recursos e o local no qual recurso de saudação toocreate.</span><span class="sxs-lookup"><span data-stu-id="3a15e-129">Choose an Azure subscription, resource group, and location in which toocreate hello resource.</span></span> <span data-ttu-id="3a15e-130">Em seguida, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="3a15e-130">Then click **Create**.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage2.png)
4. <span data-ttu-id="3a15e-131">Na lista de saudação de contas de armazenamento, clique Olá recentemente criado a conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="3a15e-131">In hello list of storage accounts, click hello newly created storage account.</span></span>
5. <span data-ttu-id="3a15e-132">Na folha de conta de armazenamento hello, clique em **chaves de acesso**.</span><span class="sxs-lookup"><span data-stu-id="3a15e-132">In hello storage account blade, click **Access keys**.</span></span> <span data-ttu-id="3a15e-133">Copie o valor de saudação do **key1** toouse posteriormente neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="3a15e-133">Copy hello value of **key1** toouse later in this tutorial.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage3.png)

## <a name="create-a-receiver-console-application"></a><span data-ttu-id="3a15e-134">Criar um aplicativo de console do destinatário</span><span class="sxs-lookup"><span data-stu-id="3a15e-134">Create a receiver console application</span></span>

1. <span data-ttu-id="3a15e-135">No Visual Studio, crie um novo projeto de aplicativo de área de trabalho do Visual C# usando Olá **aplicativo de Console** modelo de projeto.</span><span class="sxs-lookup"><span data-stu-id="3a15e-135">In Visual Studio, create a new Visual C# Desktop App project using hello **Console  Application** project template.</span></span> <span data-ttu-id="3a15e-136">Projeto de saudação do nome **receptor**.</span><span class="sxs-lookup"><span data-stu-id="3a15e-136">Name hello project **Receiver**.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-receiver-csharp1.png)
2. <span data-ttu-id="3a15e-137">No Gerenciador de soluções, clique com botão direito Olá **receptor** do projeto e, em seguida, clique em **gerenciar pacotes NuGet para solução**.</span><span class="sxs-lookup"><span data-stu-id="3a15e-137">In Solution Explorer, right-click hello **Receiver** project, and then click **Manage NuGet Packages for Solution**.</span></span>
3. <span data-ttu-id="3a15e-138">Clique em Olá **procurar** guia e, em seguida, procurar `Microsoft Azure Service Bus Event Hub - EventProcessorHost`.</span><span class="sxs-lookup"><span data-stu-id="3a15e-138">Click hello **Browse** tab, then search for `Microsoft Azure Service Bus Event Hub - EventProcessorHost`.</span></span> <span data-ttu-id="3a15e-139">Clique em **instalar**e aceite os termos de uso do hello.</span><span class="sxs-lookup"><span data-stu-id="3a15e-139">Click **Install**, and accept hello terms of use.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-eph-csharp1.png)
   
    <span data-ttu-id="3a15e-140">Downloads do Visual Studio, instala e adiciona uma referência toohello [Hub de eventos de barramento de serviço do Azure - pacote EventProcessorHost NuGet](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost), com todas as suas dependências.</span><span class="sxs-lookup"><span data-stu-id="3a15e-140">Visual Studio downloads, installs, and adds a reference toohello [Azure Service Bus Event Hub - EventProcessorHost NuGet package](https://www.nuget.org/packages/Microsoft.Azure.ServiceBus.EventProcessorHost), with all its dependencies.</span></span>
4. <span data-ttu-id="3a15e-141">Saudação de atalho **receptor** de projeto, clique em **adicionar**e, em seguida, clique em **classe**.</span><span class="sxs-lookup"><span data-stu-id="3a15e-141">Right-click hello **Receiver** project, click **Add**, and then click **Class**.</span></span> <span data-ttu-id="3a15e-142">Nomeie a nova classe de saudação **SimpleEventProcessor**e, em seguida, clique em **adicionar** toocreate classe de saudação.</span><span class="sxs-lookup"><span data-stu-id="3a15e-142">Name hello new class **SimpleEventProcessor**, and then click **Add** toocreate hello class.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-receiver-csharp2.png)
5. <span data-ttu-id="3a15e-143">Adicione Olá seguindo as instruções na parte superior de saudação do arquivo de SimpleEventProcessor.cs hello:</span><span class="sxs-lookup"><span data-stu-id="3a15e-143">Add hello following statements at hello top of hello SimpleEventProcessor.cs file:</span></span>
    
  ```csharp
  using Microsoft.ServiceBus.Messaging;
  using System.Diagnostics;
  ```
    
  <span data-ttu-id="3a15e-144">Em seguida, substitua Olá código para o corpo de saudação da classe Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="3a15e-144">Then, substitute hello following code for hello body of hello class:</span></span>
    
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
    
  <span data-ttu-id="3a15e-145">Essa classe é chamada pelo Olá **EventProcessorHost** tooprocess eventos recebidos de hub de eventos de saudação.</span><span class="sxs-lookup"><span data-stu-id="3a15e-145">This class is called by hello **EventProcessorHost** tooprocess events received from hello event hub.</span></span> <span data-ttu-id="3a15e-146">Olá `SimpleEventProcessor` classe usa um método de ponto de verificação stopwatch tooperiodically chamada hello em Olá **EventProcessorHost** contexto.</span><span class="sxs-lookup"><span data-stu-id="3a15e-146">hello `SimpleEventProcessor` class uses a stopwatch tooperiodically call hello checkpoint method on hello **EventProcessorHost** context.</span></span> <span data-ttu-id="3a15e-147">Esse processamento garante que, receptor Olá for reiniciado, ele perde não mais de cinco minutos do trabalho de processamento.</span><span class="sxs-lookup"><span data-stu-id="3a15e-147">This processing ensures that, if hello receiver is restarted, it loses no more than five minutes of processing work.</span></span>
6. <span data-ttu-id="3a15e-148">Em Olá **programa** de classe, adicione o seguinte Olá `using` instrução na parte superior de saudação do arquivo hello:</span><span class="sxs-lookup"><span data-stu-id="3a15e-148">In hello **Program** class, add hello following `using` statement at hello top of hello file:</span></span>
    
  ```csharp
  using Microsoft.ServiceBus.Messaging;
  ```
    
  <span data-ttu-id="3a15e-149">Em seguida, substitua Olá `Main` método hello `Program` classe com hello código a seguir, substituindo o nome do hub de evento hello e conexão de nível de namespace de saudação de cadeia de caracteres que você salvou anteriormente e Olá conta de armazenamento e a chave que você copiou na Olá seções anteriores.</span><span class="sxs-lookup"><span data-stu-id="3a15e-149">Then, replace hello `Main` method in hello `Program` class with hello following code, substituting hello event hub name and hello namespace-level connection string that you saved previously, and hello storage account and key that you copied in hello previous sections.</span></span> 
    
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

7. <span data-ttu-id="3a15e-150">Executar programa hello e certifique-se de que não existem erros.</span><span class="sxs-lookup"><span data-stu-id="3a15e-150">Run hello program, and ensure that there are no errors.</span></span>
  
<span data-ttu-id="3a15e-151">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="3a15e-151">Congratulations!</span></span> <span data-ttu-id="3a15e-152">Agora, você recebeu mensagens de um hub de eventos usando Olá Host de processador de evento.</span><span class="sxs-lookup"><span data-stu-id="3a15e-152">You have now received messages from an event hub using hello Event Processor Host.</span></span>


> [!NOTE]
> <span data-ttu-id="3a15e-153">Este tutorial usa uma única instância do [EventProcessorHost][EventProcessorHost].</span><span class="sxs-lookup"><span data-stu-id="3a15e-153">This tutorial uses a single instance of [EventProcessorHost][EventProcessorHost].</span></span> <span data-ttu-id="3a15e-154">taxa de transferência tooincrease, é recomendável que você execute várias instâncias do [EventProcessorHost][EventProcessorHost], conforme mostrado no hello [escala processamento do evento] [escala processamento do evento] exemplo.</span><span class="sxs-lookup"><span data-stu-id="3a15e-154">tooincrease throughput, it is recommended that you run multiple instances of [EventProcessorHost][EventProcessorHost], as shown in hello [Scaled out event processing][Scaled out event processing] sample.</span></span> <span data-ttu-id="3a15e-155">Nesses casos, hello várias instâncias automaticamente coordenam uns com os outros eventos do tooload saldo Olá recebida.</span><span class="sxs-lookup"><span data-stu-id="3a15e-155">In those cases, hello various instances automatically coordinate with each other tooload balance hello received events.</span></span> <span data-ttu-id="3a15e-156">Se você quiser que o processo de tooeach vários destinatários *todos os* Olá eventos, você deve usar o hello **o ConsumerGroup** conceito.</span><span class="sxs-lookup"><span data-stu-id="3a15e-156">If you want multiple receivers tooeach process *all* hello events, you must use hello **ConsumerGroup** concept.</span></span> <span data-ttu-id="3a15e-157">Ao receber eventos em máquinas diferentes, talvez seja útil toospecify nomes para [EventProcessorHost] [ EventProcessorHost] instâncias com base em máquinas hello (ou funções) no qual eles foram implantados.</span><span class="sxs-lookup"><span data-stu-id="3a15e-157">When receiving events from different machines, it might be useful toospecify names for [EventProcessorHost][EventProcessorHost] instances based on hello machines (or roles) in which they are deployed.</span></span> <span data-ttu-id="3a15e-158">Para obter mais informações sobre esses tópicos, consulte Olá [visão geral de Hubs de eventos] [ Event Hubs overview] e hello [guia de programação de Hubs de eventos] [ Event Hubs Programming Guide] tópicos.</span><span class="sxs-lookup"><span data-stu-id="3a15e-158">For more information about these topics, see hello [Event Hubs overview][Event Hubs overview] and hello [Event Hubs programming guide][Event Hubs Programming Guide] topics.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="3a15e-159">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3a15e-159">Next steps</span></span>

<span data-ttu-id="3a15e-160">Agora que você construiu um aplicativo de trabalho que cria um hub de eventos e envia e recebe dados, você pode saber mais, visite Olá links a seguir:</span><span class="sxs-lookup"><span data-stu-id="3a15e-160">Now that you've built a working application that creates an event hub and sends and receives data, you can learn more by visiting hello following links:</span></span>

* <span data-ttu-id="3a15e-161">[Host do Processador de Eventos][Event Processor Host]</span><span class="sxs-lookup"><span data-stu-id="3a15e-161">[Event Processor Host][Event Processor Host]</span></span>
* <span data-ttu-id="3a15e-162">[Visão Geral dos Hubs de Eventos][Event Hubs overview]</span><span class="sxs-lookup"><span data-stu-id="3a15e-162">[Event Hubs overview][Event Hubs overview]</span></span>
* [<span data-ttu-id="3a15e-163">Perguntas frequentes sobre os Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="3a15e-163">Event Hubs FAQ</span></span>](event-hubs-faq.md)

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
