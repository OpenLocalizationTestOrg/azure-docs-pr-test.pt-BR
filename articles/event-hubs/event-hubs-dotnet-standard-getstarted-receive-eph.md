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
# <a name="get-started-receiving-messages-with-hello-event-processor-host-in-net-standard"></a><span data-ttu-id="ae5a3-103">Começar a receber mensagens com hello Host de processador de eventos no .NET padrão</span><span class="sxs-lookup"><span data-stu-id="ae5a3-103">Get started receiving messages with hello Event Processor Host in .NET Standard</span></span>

> [!NOTE]
> <span data-ttu-id="ae5a3-104">Este exemplo está disponível em [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver).</span><span class="sxs-lookup"><span data-stu-id="ae5a3-104">This sample is available on [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver).</span></span>

<span data-ttu-id="ae5a3-105">Este tutorial mostra como o aplicativo que recebe mensagens de um hub de eventos por meio de console toowrite um .NET Core **EventProcessorHost**.</span><span class="sxs-lookup"><span data-stu-id="ae5a3-105">This tutorial shows how toowrite a .NET Core console application that receives messages from an event hub by using **EventProcessorHost**.</span></span> <span data-ttu-id="ae5a3-106">Você pode executar Olá [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) solução como-é, substituindo cadeias de caracteres de saudação com seus valores de conta de armazenamento e hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="ae5a3-106">You can run hello [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) solution as-is, replacing hello strings with your event hub and storage account values.</span></span> <span data-ttu-id="ae5a3-107">Ou você pode seguir Olá etapas neste tutorial toocreate seus próprios.</span><span class="sxs-lookup"><span data-stu-id="ae5a3-107">Or you can follow hello steps in this tutorial toocreate your own.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ae5a3-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="ae5a3-108">Prerequisites</span></span>

* <span data-ttu-id="ae5a3-109">[Microsoft Visual Studio 2015 ou 2017](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="ae5a3-109">[Microsoft Visual Studio 2015 or 2017](http://www.visualstudio.com).</span></span> <span data-ttu-id="ae5a3-110">Também há suporte para este tutorial 2017 do Visual Studio, use os exemplos Hello, mas o Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="ae5a3-110">hello examples in this tutorial use Visual Studio 2017, but Visual Studio 2015 is also supported.</span></span>
* <span data-ttu-id="ae5a3-111">[Ferramentas do .NET Core do Visual Studio 2015 ou 2017](http://www.microsoft.com/net/core).</span><span class="sxs-lookup"><span data-stu-id="ae5a3-111">[.NET Core Visual Studio 2015 or 2017 tools](http://www.microsoft.com/net/core).</span></span>
* <span data-ttu-id="ae5a3-112">Uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="ae5a3-112">An Azure subscription.</span></span>
* <span data-ttu-id="ae5a3-113">Um namespace dos Hubs de Eventos do Azure.</span><span class="sxs-lookup"><span data-stu-id="ae5a3-113">An Azure Event Hubs namespace.</span></span>
* <span data-ttu-id="ae5a3-114">Uma conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="ae5a3-114">An Azure storage account.</span></span>

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a><span data-ttu-id="ae5a3-115">Criar um namespace de Hubs de Eventos e um hub de eventos</span><span class="sxs-lookup"><span data-stu-id="ae5a3-115">Create an Event Hubs namespace and an event hub</span></span>  

<span data-ttu-id="ae5a3-116">Olá primeira etapa é Olá toouse [portal do Azure](https://portal.azure.com) toocreate um namespace para Olá Hubs de eventos de tipo e obter Olá credenciais de gerenciamento que seu aplicativo precisa toocommunicate com hub de eventos de saudação.</span><span class="sxs-lookup"><span data-stu-id="ae5a3-116">hello first step is toouse hello [Azure portal](https://portal.azure.com) toocreate a namespace for hello Event Hubs type, and obtain hello management credentials that your application needs toocommunicate with hello event hub.</span></span> <span data-ttu-id="ae5a3-117">toocreate um namespace e hub de eventos, siga o procedimento Olá [neste artigo](event-hubs-create.md)e continue com a saudação etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="ae5a3-117">toocreate a namespace and event hub, follow hello procedure in [this article](event-hubs-create.md), and then proceed with hello following steps.</span></span>  

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="ae5a3-118">Criar uma conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="ae5a3-118">Create an Azure storage account</span></span>  

1. <span data-ttu-id="ae5a3-119">Entrar toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ae5a3-119">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>  
2. <span data-ttu-id="ae5a3-120">No painel de navegação à esquerda de saudação do portal de saudação, clique em **novo**, clique em **armazenamento**e, em seguida, clique em **conta de armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="ae5a3-120">In hello left navigation pane of hello portal, click **New**, click **Storage**, and then click **Storage Account**.</span></span>  
3. <span data-ttu-id="ae5a3-121">Preencha os campos de saudação na folha de conta de armazenamento hello e, em seguida, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="ae5a3-121">Complete hello fields in hello storage account blade, and then click **Create**.</span></span>

    ![Criar Conta de Armazenamento][1]

4. <span data-ttu-id="ae5a3-123">Depois de ver Olá **implantações bem-sucedida** , clique em nome de Olá Olá novo da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="ae5a3-123">After you see hello **Deployments Succeeded** message, click hello name of hello new storage account.</span></span> <span data-ttu-id="ae5a3-124">Em Olá **Essentials** folha, clique em **Blobs**.</span><span class="sxs-lookup"><span data-stu-id="ae5a3-124">In hello **Essentials** blade, click **Blobs**.</span></span> <span data-ttu-id="ae5a3-125">Olá quando **do serviço Blob** folha é aberto, clique em **+ contêiner** na parte superior da saudação.</span><span class="sxs-lookup"><span data-stu-id="ae5a3-125">When hello **Blob service** blade opens, click **+ Container** at hello top.</span></span> <span data-ttu-id="ae5a3-126">Dê um nome de contêiner de saudação e feche Olá **do serviço Blob** folha.</span><span class="sxs-lookup"><span data-stu-id="ae5a3-126">Give hello container a name, and then close hello **Blob service** blade.</span></span>  
5. <span data-ttu-id="ae5a3-127">Clique em **chaves de acesso** Olá esquerdo folha e cópia Olá nome do contêiner de armazenamento de saudação, conta de armazenamento hello e valor de saudação do **key1**.</span><span class="sxs-lookup"><span data-stu-id="ae5a3-127">Click **Access keys** in hello left blade and copy hello name of hello storage container, hello storage account, and hello value of **key1**.</span></span> <span data-ttu-id="ae5a3-128">Salve tooNotepad esses valores ou algum outro local temporário.</span><span class="sxs-lookup"><span data-stu-id="ae5a3-128">Save these values tooNotepad or some other temporary location.</span></span>  

## <a name="create-a-console-application"></a><span data-ttu-id="ae5a3-129">Criar um aplicativo de console</span><span class="sxs-lookup"><span data-stu-id="ae5a3-129">Create a console application</span></span>

<span data-ttu-id="ae5a3-130">Inicie o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ae5a3-130">Start Visual Studio.</span></span> <span data-ttu-id="ae5a3-131">De saudação **arquivo** menu, clique em **novo**e, em seguida, clique em **projeto**.</span><span class="sxs-lookup"><span data-stu-id="ae5a3-131">From hello **File** menu, click **New**, and then click **Project**.</span></span> <span data-ttu-id="ae5a3-132">Crie um aplicativo de console do .NET Core.</span><span class="sxs-lookup"><span data-stu-id="ae5a3-132">Create a .NET Core console application.</span></span>

![Novo Projeto][2]

## <a name="add-hello-event-hubs-nuget-package"></a><span data-ttu-id="ae5a3-134">Adicionar pacote de NuGet de Hubs de evento Olá</span><span class="sxs-lookup"><span data-stu-id="ae5a3-134">Add hello Event Hubs NuGet package</span></span>

<span data-ttu-id="ae5a3-135">Adicionar Olá [ `Microsoft.Azure.EventHubs` ](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) e [ `Microsoft.Azure.EventHubs.Processor` ](https://www.nuget.org/packages/Microsoft.Azure.EventHubs.Processor/) .NET biblioteca NuGet pacotes tooyour projeto padrão seguindo estas etapas:</span><span class="sxs-lookup"><span data-stu-id="ae5a3-135">Add hello [`Microsoft.Azure.EventHubs`](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) and [`Microsoft.Azure.EventHubs.Processor`](https://www.nuget.org/packages/Microsoft.Azure.EventHubs.Processor/) .NET Standard library NuGet packages tooyour project by following these steps:</span></span> 

1. <span data-ttu-id="ae5a3-136">Clique com botão direito Olá recém-criado e selecione **gerenciar pacotes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="ae5a3-136">Right-click hello newly created project and select **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="ae5a3-137">Clique em Olá **procurar** guia, procure por "Microsoft.Azure.EventHubs" e selecione Olá **Microsoft.Azure.EventHubs** pacote.</span><span class="sxs-lookup"><span data-stu-id="ae5a3-137">Click hello **Browse** tab, then search for "Microsoft.Azure.EventHubs" and select hello **Microsoft.Azure.EventHubs** package.</span></span> <span data-ttu-id="ae5a3-138">Clique em **instalar** toocomplete Olá instalação, em seguida, feche esta caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ae5a3-138">Click **Install** toocomplete hello installation, then close this dialog box.</span></span>
3. <span data-ttu-id="ae5a3-139">Repita as etapas 1 e 2 e instalar Olá **Microsoft.Azure.EventHubs.Processor** pacote.</span><span class="sxs-lookup"><span data-stu-id="ae5a3-139">Repeat steps 1 and 2, and install hello **Microsoft.Azure.EventHubs.Processor** package.</span></span>

## <a name="implement-hello-ieventprocessor-interface"></a><span data-ttu-id="ae5a3-140">Implementa a interface IEventProcessor Olá</span><span class="sxs-lookup"><span data-stu-id="ae5a3-140">Implement hello IEventProcessor interface</span></span>

1. <span data-ttu-id="ae5a3-141">No Gerenciador de soluções, projetos de saudação com o botão direito, clique em **adicionar**e, em seguida, clique em **classe**.</span><span class="sxs-lookup"><span data-stu-id="ae5a3-141">In Solution Explorer, right-click hello project, click **Add**, and then click **Class**.</span></span> <span data-ttu-id="ae5a3-142">Nomeie a nova classe de saudação **SimpleEventProcessor**.</span><span class="sxs-lookup"><span data-stu-id="ae5a3-142">Name hello new class **SimpleEventProcessor**.</span></span>

2. <span data-ttu-id="ae5a3-143">Abrir o arquivo de SimpleEventProcessor.cs hello e adicione o seguinte Olá `using` superior de toohello de instruções do arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="ae5a3-143">Open hello SimpleEventProcessor.cs file and add hello following `using` statements toohello top of hello file.</span></span>

    ```csharp
    using Microsoft.Azure.EventHubs;
    using Microsoft.Azure.EventHubs.Processor;
    using System.Threading.Tasks;
    ```

3. <span data-ttu-id="ae5a3-144">Saudação de implementar `IEventProcessor` interface.</span><span class="sxs-lookup"><span data-stu-id="ae5a3-144">Implement hello `IEventProcessor` interface.</span></span> <span data-ttu-id="ae5a3-145">Substitua todo o conteúdo do Olá Olá `SimpleEventProcessor` classe com hello código a seguir:</span><span class="sxs-lookup"><span data-stu-id="ae5a3-145">Replace hello entire contents of hello `SimpleEventProcessor` class with hello following code:</span></span>

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

## <a name="write-a-main-console-method-that-uses-hello-simpleeventprocessor-class-tooreceive-messages"></a><span data-ttu-id="ae5a3-146">Escrever um método do console principal que usa mensagens de saudação do SimpleEventProcessor classe tooreceive</span><span class="sxs-lookup"><span data-stu-id="ae5a3-146">Write a main console method that uses hello SimpleEventProcessor class tooreceive messages</span></span>

1. <span data-ttu-id="ae5a3-147">Adicione o seguinte Olá `using` superior de toohello instruções do arquivo Program.cs de saudação.</span><span class="sxs-lookup"><span data-stu-id="ae5a3-147">Add hello following `using` statements toohello top of hello Program.cs file.</span></span>

    ```csharp
    using Microsoft.Azure.EventHubs;
    using Microsoft.Azure.EventHubs.Processor;
    using System.Threading.Tasks;
    ```

2. <span data-ttu-id="ae5a3-148">Adicionar constantes toohello `Program` classe para a cadeia de conexão de hub de evento Olá, nome do hub de evento, nome do contêiner de conta de armazenamento, nome da conta de armazenamento e chave de conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="ae5a3-148">Add constants toohello `Program` class for hello event hub connection string, event hub name, storage account container name, storage account name, and storage account key.</span></span> <span data-ttu-id="ae5a3-149">Adicione Olá código a seguir, substituindo espaços reservados de saudação com seus valores correspondentes.</span><span class="sxs-lookup"><span data-stu-id="ae5a3-149">Add hello following code, replacing hello placeholders with their corresponding values.</span></span>

    ```csharp
    private const string EhConnectionString = "{Event Hubs connection string}";
    private const string EhEntityPath = "{Event Hub path/name}";
    private const string StorageContainerName = "{Storage account container name}";
    private const string StorageAccountName = "{Storage account name}";
    private const string StorageAccountKey = "{Storage account key}";

    private static readonly string StorageConnectionString = string.Format("DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}", StorageAccountName, StorageAccountKey);
    ```   

3. <span data-ttu-id="ae5a3-150">Adicionar um novo método chamado `MainAsync` toohello `Program` classe, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="ae5a3-150">Add a new method named `MainAsync` toohello `Program` class, as follows:</span></span>

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

3. <span data-ttu-id="ae5a3-151">Adicione a seguinte linha de código toohello de saudação `Main` método:</span><span class="sxs-lookup"><span data-stu-id="ae5a3-151">Add hello following line of code toohello `Main` method:</span></span>

    ```csharp
    MainAsync(args).GetAwaiter().GetResult();
    ```

    <span data-ttu-id="ae5a3-152">O arquivo Program.cs deve ficar assim:</span><span class="sxs-lookup"><span data-stu-id="ae5a3-152">Here is what your Program.cs file should look like:</span></span>

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

4. <span data-ttu-id="ae5a3-153">Executar programa hello e certifique-se de que não existem erros.</span><span class="sxs-lookup"><span data-stu-id="ae5a3-153">Run hello program, and ensure that there are no errors.</span></span>

<span data-ttu-id="ae5a3-154">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="ae5a3-154">Congratulations!</span></span> <span data-ttu-id="ae5a3-155">Você agora recebeu mensagens de um hub de eventos usando Olá Host de processador de evento.</span><span class="sxs-lookup"><span data-stu-id="ae5a3-155">You have now received messages from an event hub by using hello Event Processor Host.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ae5a3-156">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ae5a3-156">Next steps</span></span>
<span data-ttu-id="ae5a3-157">Você pode aprender mais sobre os Hubs de eventos visitando Olá links a seguir:</span><span class="sxs-lookup"><span data-stu-id="ae5a3-157">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="ae5a3-158">Visão Geral dos Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="ae5a3-158">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="ae5a3-159">Criar um hub de eventos</span><span class="sxs-lookup"><span data-stu-id="ae5a3-159">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="ae5a3-160">Perguntas frequentes sobre os Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="ae5a3-160">Event Hubs FAQ</span></span>](event-hubs-faq.md)

[1]: ./media/event-hubs-dotnet-standard-getstarted-receive-eph/event-hubs-python1.png
[2]: ./media/event-hubs-dotnet-standard-getstarted-receive-eph/netcore.png
