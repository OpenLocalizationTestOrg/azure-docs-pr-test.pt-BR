---
title: eventos de aaaReceive de Hubs de eventos do Azure usando o Java | Microsoft Docs
description: Comece a receber de Hubs de Eventos usando Java
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 38e3be53-251c-488f-a856-9a500f41b6ca
ms.service: event-hubs
ms.workload: core
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: 05414a22e6616296752c678bb0af887d6f070c12
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="receive-events-from-azure-event-hubs-using-java"></a><span data-ttu-id="b3ad4-103">Receber eventos de Hubs de Eventos do Azure usando Java</span><span class="sxs-lookup"><span data-stu-id="b3ad4-103">Receive events from Azure Event Hubs using Java</span></span>


## <a name="introduction"></a><span data-ttu-id="b3ad4-104">Introdução</span><span class="sxs-lookup"><span data-stu-id="b3ad4-104">Introduction</span></span>
<span data-ttu-id="b3ad4-105">Hubs de eventos é um sistema de inclusão altamente escalonável que pode ingestão milhões de eventos por segundo, permitindo que um aplicativo tooprocess e analisar Olá grandes quantidades de dados produzidos por seus aplicativos e dispositivos conectados.</span><span class="sxs-lookup"><span data-stu-id="b3ad4-105">Event Hubs is a highly scalable ingestion system that can ingest millions of events per second, enabling an application tooprocess and analyze hello massive amounts of data produced by your connected devices and applications.</span></span> <span data-ttu-id="b3ad4-106">Depois de coletados em Hubs de Evento, você pode transformar e armazenar dados usando qualquer provedor de análise em tempo real ou cluster de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="b3ad4-106">Once collected into Event Hubs, you can transform and store data using any real-time analytics provider or storage cluster.</span></span>

<span data-ttu-id="b3ad4-107">Para obter mais informações, consulte Olá [visão geral de Hubs de eventos][Event Hubs overview].</span><span class="sxs-lookup"><span data-stu-id="b3ad4-107">For more information, see hello [Event Hubs overview][Event Hubs overview].</span></span>

<span data-ttu-id="b3ad4-108">Este tutorial mostra como tooreceive eventos em um hub de eventos usando um aplicativo de console escrito em Java.</span><span class="sxs-lookup"><span data-stu-id="b3ad4-108">This tutorial shows how tooreceive events into an event hub using a console application written in Java.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b3ad4-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="b3ad4-109">Prerequisites</span></span>

<span data-ttu-id="b3ad4-110">Em ordem toocomplete neste tutorial, você precisa Olá pré-requisitos a seguir:</span><span class="sxs-lookup"><span data-stu-id="b3ad4-110">In order toocomplete this tutorial, you need hello following prerequisites:</span></span>

* <span data-ttu-id="b3ad4-111">Um ambiente de desenvolvimento Java.</span><span class="sxs-lookup"><span data-stu-id="b3ad4-111">A Java development environment.</span></span> <span data-ttu-id="b3ad4-112">Para este tutorial, vamos considerar o [Eclipse](https://www.eclipse.org/).</span><span class="sxs-lookup"><span data-stu-id="b3ad4-112">For this tutorial, we assume [Eclipse](https://www.eclipse.org/).</span></span>
* <span data-ttu-id="b3ad4-113">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="b3ad4-113">An active Azure account.</span></span> <br/><span data-ttu-id="b3ad4-114">Se você não tem uma conta, pode criar uma conta gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="b3ad4-114">If you don't have an account, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="b3ad4-115">Para obter detalhes, consulte <a href="http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fdevelop%2Fmobile%2Ftutorials%2Fget-started%2F" target="_blank">Avaliação gratuita do Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="b3ad4-115">For details, see <a href="http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fdevelop%2Fmobile%2Ftutorials%2Fget-started%2F" target="_blank">Azure Free Trial</a>.</span></span>

## <a name="receive-messages-with-eventprocessorhost-in-java"></a><span data-ttu-id="b3ad4-116">Receber mensagens com EventProcessorHost em Java</span><span class="sxs-lookup"><span data-stu-id="b3ad4-116">Receive messages with EventProcessorHost in Java</span></span>

<span data-ttu-id="b3ad4-117">**EventProcessorHost** é uma classe Java que simplifica o recebimento de eventos dos Hubs de Eventos gerenciando pontos de verificação persistentes e recebimentos paralelos desses Hubs de Eventos.</span><span class="sxs-lookup"><span data-stu-id="b3ad4-117">**EventProcessorHost** is a Java class that simplifies receiving events from Event Hubs by managing persistent checkpoints and parallel receives from those Event Hubs.</span></span> <span data-ttu-id="b3ad4-118">Usando o EventProcessorHost, você pode dividir eventos entre vários destinatários, mesmo quando hospedados em nós diferentes.</span><span class="sxs-lookup"><span data-stu-id="b3ad4-118">Using EventProcessorHost, you can split events across multiple receivers, even when hosted in different nodes.</span></span> <span data-ttu-id="b3ad4-119">Este exemplo mostra como toouse EventProcessorHost para um único destinatário.</span><span class="sxs-lookup"><span data-stu-id="b3ad4-119">This example shows how toouse EventProcessorHost for a single receiver.</span></span>

### <a name="create-a-storage-account"></a><span data-ttu-id="b3ad4-120">Criar uma conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="b3ad4-120">Create a storage account</span></span>
<span data-ttu-id="b3ad4-121">toouse EventProcessorHost, você deve ter uma [conta de armazenamento do Azure][Azure Storage account]:</span><span class="sxs-lookup"><span data-stu-id="b3ad4-121">toouse EventProcessorHost, you must have an [Azure Storage account][Azure Storage account]:</span></span>

1. <span data-ttu-id="b3ad4-122">Faça logon no toohello [portal do Azure][Azure portal]e clique em **+ novo** no lado esquerdo de saudação da tela hello.</span><span class="sxs-lookup"><span data-stu-id="b3ad4-122">Log on toohello [Azure portal][Azure portal], and click **+ New** on hello left-hand side of hello screen.</span></span>
2. <span data-ttu-id="b3ad4-123">Clique em **Armazenamento** e em **conta de Armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="b3ad4-123">Click **Storage**, then click **Storage account**.</span></span> <span data-ttu-id="b3ad4-124">Em Olá **criar conta de armazenamento** folha, digite um nome para a conta de armazenamento hello.</span><span class="sxs-lookup"><span data-stu-id="b3ad4-124">In hello **Create storage account** blade, type a name for hello storage account.</span></span> <span data-ttu-id="b3ad4-125">Conclua o restante da saudação de campos hello, selecione a região desejada e, em seguida, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="b3ad4-125">Complete hello rest of hello fields, select your desired region, and then click **Create**.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage2.png)

3. <span data-ttu-id="b3ad4-126">Clique na conta de armazenamento Olá recém-criada e, em seguida, clique em **gerenciar chaves de acesso**:</span><span class="sxs-lookup"><span data-stu-id="b3ad4-126">Click hello newly created storage account, and then click **Manage Access Keys**:</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage3.png)

    <span data-ttu-id="b3ad4-127">Copiar Olá acesso primário tooa chave temporária local toouse posteriormente neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="b3ad4-127">Copy hello primary access key tooa temporary location, toouse later in this tutorial.</span></span>

### <a name="create-a-java-project-using-hello-eventprocessor-host"></a><span data-ttu-id="b3ad4-128">Criar um projeto de Java usando Olá EventProcessor Host</span><span class="sxs-lookup"><span data-stu-id="b3ad4-128">Create a Java project using hello EventProcessor Host</span></span>
<span data-ttu-id="b3ad4-129">Olá biblioteca de cliente de Java para Hubs de eventos está disponível para uso em projetos Maven da saudação [repositório Central Maven][Maven Package]e podem ser referenciadas usando Olá após a declaração de dependência dentro de sua Arquivo de projeto Maven:</span><span class="sxs-lookup"><span data-stu-id="b3ad4-129">hello Java client library for Event Hubs is available for use in Maven projects from hello [Maven Central Repository][Maven Package], and can be referenced using hello following dependency declaration inside your Maven project file:</span></span>    

```xml
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-eventhubs</artifactId>
    <version>{VERSION}</version>
</dependency>
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-eventhubs-eph</artifactId>
    <version>{VERSION}</version>
</dependency>
<dependency>
  <groupId>com.microsoft.azure</groupId>
  <artifactId>azure-eventhubs-eph</artifactId>
  <version>0.14.0</version>
</dependency>
```

<span data-ttu-id="b3ad4-130">Para tipos diferentes de ambientes de desenvolvimento, você pode obter explicitamente arquivos JAR do hello mais recente liberado de saudação [repositório Central Maven] [ Maven Package] ou de [Olá ponto de distribuição de versão em GitHub](https://github.com/Azure/azure-event-hubs/releases).</span><span class="sxs-lookup"><span data-stu-id="b3ad4-130">For different types of build environments, you can explicitly obtain hello latest released JAR files from hello [Maven Central Repository][Maven Package] or from [hello release distribution point on GitHub](https://github.com/Azure/azure-event-hubs/releases).</span></span>  

1. <span data-ttu-id="b3ad4-131">Para Olá exemplo a seguir, primeiro crie um novo projeto Maven para um aplicativo de console para o shell no ambiente de desenvolvimento Java favorito.</span><span class="sxs-lookup"><span data-stu-id="b3ad4-131">For hello following sample, first create a new Maven project for a console/shell application in your favorite Java development environment.</span></span> <span data-ttu-id="b3ad4-132">classe de saudação é chamada `ErrorNotificationHandler`.</span><span class="sxs-lookup"><span data-stu-id="b3ad4-132">hello class is called `ErrorNotificationHandler`.</span></span>     
   
    ```java
    import java.util.function.Consumer;
    import com.microsoft.azure.eventprocessorhost.ExceptionReceivedEventArgs;
   
    public class ErrorNotificationHandler implements Consumer<ExceptionReceivedEventArgs>
    {
        @Override
        public void accept(ExceptionReceivedEventArgs t)
        {
            System.out.println("SAMPLE: Host " + t.getHostname() + " received general error notification during " + t.getAction() + ": " + t.getException().toString());
        }
    }
    ```
2. <span data-ttu-id="b3ad4-133">Toocreate uma nova classe chamada de código a seguir de saudação do uso `EventProcessor`.</span><span class="sxs-lookup"><span data-stu-id="b3ad4-133">Use hello following code toocreate a new class called `EventProcessor`.</span></span>
   
    ```java
    import com.microsoft.azure.eventhubs.EventData;
    import com.microsoft.azure.eventprocessorhost.CloseReason;
    import com.microsoft.azure.eventprocessorhost.IEventProcessor;
    import com.microsoft.azure.eventprocessorhost.PartitionContext;
   
    public class EventProcessor implements IEventProcessor
    {
        private int checkpointBatchingCount = 0;
   
        @Override
        public void onOpen(PartitionContext context) throws Exception
        {
            System.out.println("SAMPLE: Partition " + context.getPartitionId() + " is opening");
        }
   
        @Override
        public void onClose(PartitionContext context, CloseReason reason) throws Exception
        {
            System.out.println("SAMPLE: Partition " + context.getPartitionId() + " is closing for reason " + reason.toString());
        }
   
        @Override
        public void onError(PartitionContext context, Throwable error)
        {
            System.out.println("SAMPLE: Partition " + context.getPartitionId() + " onError: " + error.toString());
        }
   
        @Override
        public void onEvents(PartitionContext context, Iterable<EventData> messages) throws Exception
        {
            System.out.println("SAMPLE: Partition " + context.getPartitionId() + " got message batch");
            int messageCount = 0;
            for (EventData data : messages)
            {
                System.out.println("SAMPLE (" + context.getPartitionId() + "," + data.getSystemProperties().getOffset() + "," +
                        data.getSystemProperties().getSequenceNumber() + "): " + new String(data.getBody(), "UTF8"));
                messageCount++;
   
                this.checkpointBatchingCount++;
                if ((checkpointBatchingCount % 5) == 0)
                {
                    System.out.println("SAMPLE: Partition " + context.getPartitionId() + " checkpointing at " +
                        data.getSystemProperties().getOffset() + "," + data.getSystemProperties().getSequenceNumber());
                    context.checkpoint(data);
                }
            }
            System.out.println("SAMPLE: Partition " + context.getPartitionId() + " batch size was " + messageCount + " for host " + context.getOwner());
        }
    }
    ```
3. <span data-ttu-id="b3ad4-134">Criar uma classe mais chamada `EventProcessorSample`usando Olá código a seguir.</span><span class="sxs-lookup"><span data-stu-id="b3ad4-134">Create one more class called `EventProcessorSample`, using hello following code.</span></span>
   
    ```java
    import com.microsoft.azure.eventprocessorhost.*;
    import com.microsoft.azure.servicebus.ConnectionStringBuilder;
    import com.microsoft.azure.eventhubs.EventData;
   
    public class EventProcessorSample
    {
        public static void main(String args[])
        {
            final String consumerGroupName = "$Default";
            final String namespaceName = "----ServiceBusNamespaceName-----";
            final String eventHubName = "----EventHubName-----";
            final String sasKeyName = "-----SharedAccessSignatureKeyName-----";
            final String sasKey = "---SharedAccessSignatureKey----";
   
            final String storageAccountName = "---StorageAccountName----";
            final String storageAccountKey = "---StorageAccountKey----";
            final String storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=" + storageAccountName + ";AccountKey=" + storageAccountKey;
   
            ConnectionStringBuilder eventHubConnectionString = new ConnectionStringBuilder(namespaceName, eventHubName, sasKeyName, sasKey);
   
            EventProcessorHost host = new EventProcessorHost(eventHubName, consumerGroupName, eventHubConnectionString.toString(), storageConnectionString);
   
            System.out.println("Registering host named " + host.getHostName());
            EventProcessorOptions options = new EventProcessorOptions();
            options.setExceptionNotification(new ErrorNotificationHandler());
            try
            {
                host.registerEventProcessor(EventProcessor.class, options).get();
            }
            catch (Exception e)
            {
                System.out.print("Failure while registering: ");
                if (e instanceof ExecutionException)
                {
                    Throwable inner = e.getCause();
                    System.out.println(inner.toString());
                }
                else
                {
                    System.out.println(e.toString());
                }
            }
   
            System.out.println("Press enter toostop");
            try
            {
                System.in.read();
                host.unregisterEventProcessor();
   
                System.out.println("Calling forceExecutorShutdown");
                EventProcessorHost.forceExecutorShutdown(120);
            }
            catch(Exception e)
            {
                System.out.println(e.toString());
                e.printStackTrace();
            }
   
            System.out.println("End of sample");
        }
    }
    ```
4. <span data-ttu-id="b3ad4-135">Substitua saudação campos a seguir com valores hello usou quando criou a conta de armazenamento e hub de eventos de saudação.</span><span class="sxs-lookup"><span data-stu-id="b3ad4-135">Replace hello following fields with hello values used when you created hello event hub and storage account.</span></span>
   
    ```java
    final String namespaceName = "----ServiceBusNamespaceName-----";
    final String eventHubName = "----EventHubName-----";
   
    final String sasKeyName = "-----SharedAccessSignatureKeyName-----";
    final String sasKey = "---SharedAccessSignatureKey----";
   
    final String storageAccountName = "---StorageAccountName----"
    final String storageAccountKey = "---StorageAccountKey----";
    ```

> [!NOTE]
> <span data-ttu-id="b3ad4-136">Este tutorial usa uma única instância do EventProcessorHost.</span><span class="sxs-lookup"><span data-stu-id="b3ad4-136">This tutorial uses a single instance of EventProcessorHost.</span></span> <span data-ttu-id="b3ad4-137">taxa de transferência tooincrease, é recomendável que você executar várias instâncias do EventProcessorHost, preferencialmente em computadores separados.</span><span class="sxs-lookup"><span data-stu-id="b3ad4-137">tooincrease throughput, it is recommended that you run multiple instances of EventProcessorHost, preferably on separate machines.</span></span>  <span data-ttu-id="b3ad4-138">Isso também fornece redundância.</span><span class="sxs-lookup"><span data-stu-id="b3ad4-138">This provides redundancy as well.</span></span> <span data-ttu-id="b3ad4-139">Nesses casos, Olá automaticamente coordenada uns com os outros eventos de saudação recebida ordem tooload saldo de várias instâncias.</span><span class="sxs-lookup"><span data-stu-id="b3ad4-139">In those cases, hello various instances automatically coordinate with each other in order tooload balance hello received events.</span></span> <span data-ttu-id="b3ad4-140">Se você quiser que o processo de tooeach vários destinatários *todos os* Olá eventos, você deve usar o hello **o ConsumerGroup** conceito.</span><span class="sxs-lookup"><span data-stu-id="b3ad4-140">If you want multiple receivers tooeach process *all* hello events, you must use hello **ConsumerGroup** concept.</span></span> <span data-ttu-id="b3ad4-141">Ao receber eventos em máquinas diferentes, pode ser útil toospecify nomes para instâncias de EventProcessorHost com base em máquinas hello (ou funções) no qual eles foram implantados.</span><span class="sxs-lookup"><span data-stu-id="b3ad4-141">When receiving events from different machines, it might be useful toospecify names for EventProcessorHost instances based on hello machines (or roles) in which they are deployed.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="b3ad4-142">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b3ad4-142">Next steps</span></span>
<span data-ttu-id="b3ad4-143">Você pode aprender mais sobre os Hubs de eventos visitando Olá links a seguir:</span><span class="sxs-lookup"><span data-stu-id="b3ad4-143">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="b3ad4-144">Visão Geral dos Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="b3ad4-144">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="b3ad4-145">Criar um Hub de Eventos</span><span class="sxs-lookup"><span data-stu-id="b3ad4-145">Create an Event Hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="b3ad4-146">Perguntas frequentes sobre os Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="b3ad4-146">Event Hubs FAQ</span></span>](event-hubs-faq.md)

<!-- Links -->
[Event Hubs overview]: event-hubs-what-is-event-hubs.md
[Azure Storage account]: ../storage/common/storage-create-storage-account.md
[Azure portal]: https://portal.azure.com
[Maven Package]: https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs-eph%22

<!-- Images -->
[11]: ./media/service-bus-event-hubs-get-started-receive-ephjava/create-eph-csharp2.png
[12]: ./media/service-bus-event-hubs-get-started-receive-ephjava/create-eph-csharp3.png
