---
title: Receber eventos dos Hubs de Eventos do Azure usando o .NET Standard | Microsoft Docs
description: "Introdução à recepção de mensagens com o EventProcessorHost no .NET Standard"
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
ms.openlocfilehash: cc62792dad0284f9514664795fdfb32e94a85943
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-receiving-messages-with-the-event-processor-host-in-net-standard"></a><span data-ttu-id="908e3-103">Introdução à recepção de mensagens com o Host do Processador de Eventos no .NET Standard</span><span class="sxs-lookup"><span data-stu-id="908e3-103">Get started receiving messages with the Event Processor Host in .NET Standard</span></span>

> [!NOTE]
> <span data-ttu-id="908e3-104">Este exemplo está disponível em [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver).</span><span class="sxs-lookup"><span data-stu-id="908e3-104">This sample is available on [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver).</span></span>

<span data-ttu-id="908e3-105">Este tutorial mostra como escrever um aplicativo de console do .NET Core que recebe mensagens de um hub de eventos usando o **EventProcessorHost**.</span><span class="sxs-lookup"><span data-stu-id="908e3-105">This tutorial shows how to write a .NET Core console application that receives messages from an event hub by using **EventProcessorHost**.</span></span> <span data-ttu-id="908e3-106">É possível executar a solução do [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) no estado em que se encontra, substituindo as cadeias de caracteres pelos valores do hub de eventos e da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="908e3-106">You can run the [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleEphReceiver) solution as-is, replacing the strings with your event hub and storage account values.</span></span> <span data-ttu-id="908e3-107">Se preferir, é possível seguir as etapas deste tutorial para criar sua própria solução.</span><span class="sxs-lookup"><span data-stu-id="908e3-107">Or you can follow the steps in this tutorial to create your own.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="908e3-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="908e3-108">Prerequisites</span></span>

* <span data-ttu-id="908e3-109">[Microsoft Visual Studio 2015 ou 2017](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="908e3-109">[Microsoft Visual Studio 2015 or 2017](http://www.visualstudio.com).</span></span> <span data-ttu-id="908e3-110">Os exemplos neste tutorial usam o Visual Studio 2017, mas também há suporte para o Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="908e3-110">The examples in this tutorial use Visual Studio 2017, but Visual Studio 2015 is also supported.</span></span>
* <span data-ttu-id="908e3-111">[Ferramentas do .NET Core do Visual Studio 2015 ou 2017](http://www.microsoft.com/net/core).</span><span class="sxs-lookup"><span data-stu-id="908e3-111">[.NET Core Visual Studio 2015 or 2017 tools](http://www.microsoft.com/net/core).</span></span>
* <span data-ttu-id="908e3-112">Uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="908e3-112">An Azure subscription.</span></span>
* <span data-ttu-id="908e3-113">Um namespace dos Hubs de Eventos do Azure.</span><span class="sxs-lookup"><span data-stu-id="908e3-113">An Azure Event Hubs namespace.</span></span>
* <span data-ttu-id="908e3-114">Uma conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="908e3-114">An Azure storage account.</span></span>

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a><span data-ttu-id="908e3-115">Criar um namespace de Hubs de Eventos e um hub de eventos</span><span class="sxs-lookup"><span data-stu-id="908e3-115">Create an Event Hubs namespace and an event hub</span></span>  

<span data-ttu-id="908e3-116">A primeira etapa é usar o [Portal do Azure](https://portal.azure.com) para criar um namespace para o tipo de Hubs de Eventos e obter as credenciais de gerenciamento que seu aplicativo precisa para se comunicar com o hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="908e3-116">The first step is to use the [Azure portal](https://portal.azure.com) to create a namespace for the Event Hubs type, and obtain the management credentials that your application needs to communicate with the event hub.</span></span> <span data-ttu-id="908e3-117">Para criar um namespace e um hub de eventos, siga o procedimento descrito [neste artigo](event-hubs-create.md) e continue com as próximas etapas.</span><span class="sxs-lookup"><span data-stu-id="908e3-117">To create a namespace and event hub, follow the procedure in [this article](event-hubs-create.md), and then proceed with the following steps.</span></span>  

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="908e3-118">Criar uma conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="908e3-118">Create an Azure storage account</span></span>  

1. <span data-ttu-id="908e3-119">Entre no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="908e3-119">Sign in to the [Azure portal](https://portal.azure.com).</span></span>  
2. <span data-ttu-id="908e3-120">No painel de navegação esquerdo do portal, clique em **Novo**, em **Armazenamento** e em **Conta de Armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="908e3-120">In the left navigation pane of the portal, click **New**, click **Storage**, and then click **Storage Account**.</span></span>  
3. <span data-ttu-id="908e3-121">Preencha os campos na folha da conta de armazenamento e clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="908e3-121">Complete the fields in the storage account blade, and then click **Create**.</span></span>

    ![Criar Conta de Armazenamento][1]

4. <span data-ttu-id="908e3-123">Depois de ver a mensagem **Implantações Bem-Sucedidas**, clique no nome da nova conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="908e3-123">After you see the **Deployments Succeeded** message, click the name of the new storage account.</span></span> <span data-ttu-id="908e3-124">Na folha **Dados Básicos**, clique em **Blobs**.</span><span class="sxs-lookup"><span data-stu-id="908e3-124">In the **Essentials** blade, click **Blobs**.</span></span> <span data-ttu-id="908e3-125">Quando a folha **Serviço Blob** abrir, clique em **+ Contêiner** na parte superior.</span><span class="sxs-lookup"><span data-stu-id="908e3-125">When the **Blob service** blade opens, click **+ Container** at the top.</span></span> <span data-ttu-id="908e3-126">Forneça um nome para o contêiner e feche a folha **Serviço Blob**.</span><span class="sxs-lookup"><span data-stu-id="908e3-126">Give the container a name, and then close the **Blob service** blade.</span></span>  
5. <span data-ttu-id="908e3-127">Clique em **Chaves de acesso** na folha esquerda e copie o nome do contêiner de armazenamento, a conta de armazenamento e o valor de **key1**.</span><span class="sxs-lookup"><span data-stu-id="908e3-127">Click **Access keys** in the left blade and copy the name of the storage container, the storage account, and the value of **key1**.</span></span> <span data-ttu-id="908e3-128">Salve esses valores no Bloco de notas ou em outro local temporário.</span><span class="sxs-lookup"><span data-stu-id="908e3-128">Save these values to Notepad or some other temporary location.</span></span>  

## <a name="create-a-console-application"></a><span data-ttu-id="908e3-129">Criar um aplicativo de console</span><span class="sxs-lookup"><span data-stu-id="908e3-129">Create a console application</span></span>

<span data-ttu-id="908e3-130">Inicie o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="908e3-130">Start Visual Studio.</span></span> <span data-ttu-id="908e3-131">No menu **Arquivo**, clique em **Novo** e em **Projeto**.</span><span class="sxs-lookup"><span data-stu-id="908e3-131">From the **File** menu, click **New**, and then click **Project**.</span></span> <span data-ttu-id="908e3-132">Crie um aplicativo de console do .NET Core.</span><span class="sxs-lookup"><span data-stu-id="908e3-132">Create a .NET Core console application.</span></span>

![Novo Projeto][2]

## <a name="add-the-event-hubs-nuget-package"></a><span data-ttu-id="908e3-134">Adicione o pacote NuGet de Hubs de Evento</span><span class="sxs-lookup"><span data-stu-id="908e3-134">Add the Event Hubs NuGet package</span></span>

<span data-ttu-id="908e3-135">Adicione os pacotes NuGet [`Microsoft.Azure.EventHubs`](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) e [`Microsoft.Azure.EventHubs.Processor`](https://www.nuget.org/packages/Microsoft.Azure.EventHubs.Processor/) de biblioteca do .NET Standard ao projeto seguindo estas etapas:</span><span class="sxs-lookup"><span data-stu-id="908e3-135">Add the [`Microsoft.Azure.EventHubs`](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) and [`Microsoft.Azure.EventHubs.Processor`](https://www.nuget.org/packages/Microsoft.Azure.EventHubs.Processor/) .NET Standard library NuGet packages to your project by following these steps:</span></span> 

1. <span data-ttu-id="908e3-136">Clique com o botão direito do mouse no projeto recém-criado e selecione **Gerenciar Pacotes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="908e3-136">Right-click the newly created project and select **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="908e3-137">Clique na guia **Procurar**, pesquise por "Microsoft.Azure.EventHubs" e selecione o pacote **Microsoft.Azure.EventHubs**.</span><span class="sxs-lookup"><span data-stu-id="908e3-137">Click the **Browse** tab, then search for "Microsoft.Azure.EventHubs" and select the **Microsoft.Azure.EventHubs** package.</span></span> <span data-ttu-id="908e3-138">Clique em **Instalar** para concluir a instalação e feche essa caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="908e3-138">Click **Install** to complete the installation, then close this dialog box.</span></span>
3. <span data-ttu-id="908e3-139">Repita as etapas 1 e 2 e instalar o pacote **Microsoft.Azure.EventHubs.Processor**.</span><span class="sxs-lookup"><span data-stu-id="908e3-139">Repeat steps 1 and 2, and install the **Microsoft.Azure.EventHubs.Processor** package.</span></span>

## <a name="implement-the-ieventprocessor-interface"></a><span data-ttu-id="908e3-140">Implementar a interface IEventProcessor</span><span class="sxs-lookup"><span data-stu-id="908e3-140">Implement the IEventProcessor interface</span></span>

1. <span data-ttu-id="908e3-141">No Gerenciador de Soluções, clique com o botão direito do mouse no projeto, clique em **Adicionar** e em **Classe**.</span><span class="sxs-lookup"><span data-stu-id="908e3-141">In Solution Explorer, right-click the project, click **Add**, and then click **Class**.</span></span> <span data-ttu-id="908e3-142">Nomeie a nova classe **SimpleEventProcessor**.</span><span class="sxs-lookup"><span data-stu-id="908e3-142">Name the new class **SimpleEventProcessor**.</span></span>

2. <span data-ttu-id="908e3-143">Abra o arquivo SimpleEventProcessor.cs e adicione as seguintes instruções `using` à parte superior do arquivo.</span><span class="sxs-lookup"><span data-stu-id="908e3-143">Open the SimpleEventProcessor.cs file and add the following `using` statements to the top of the file.</span></span>

    ```csharp
    using Microsoft.Azure.EventHubs;
    using Microsoft.Azure.EventHubs.Processor;
    using System.Threading.Tasks;
    ```

3. <span data-ttu-id="908e3-144">Implementar o `IEventProcessor` interface.</span><span class="sxs-lookup"><span data-stu-id="908e3-144">Implement the `IEventProcessor` interface.</span></span> <span data-ttu-id="908e3-145">Substitua todo o conteúdo da classe `SimpleEventProcessor` pelo código a seguir:</span><span class="sxs-lookup"><span data-stu-id="908e3-145">Replace the entire contents of the `SimpleEventProcessor` class with the following code:</span></span>

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

## <a name="write-a-main-console-method-that-uses-the-simpleeventprocessor-class-to-receive-messages"></a><span data-ttu-id="908e3-146">Escrever um método de console principal que usa a classe SimpleEventProcessor para receber mensagens de um Hub de Eventos</span><span class="sxs-lookup"><span data-stu-id="908e3-146">Write a main console method that uses the SimpleEventProcessor class to receive messages</span></span>

1. <span data-ttu-id="908e3-147">Adicione as instruções `using` a seguir à parte superior do arquivo Program.cs.</span><span class="sxs-lookup"><span data-stu-id="908e3-147">Add the following `using` statements to the top of the Program.cs file.</span></span>

    ```csharp
    using Microsoft.Azure.EventHubs;
    using Microsoft.Azure.EventHubs.Processor;
    using System.Threading.Tasks;
    ```

2. <span data-ttu-id="908e3-148">Adicione constantes à classe `Program` da cadeia de conexão do hub de eventos, do nome do hub de eventos, do nome do contêiner da conta de armazenamento, do nome da conta de armazenamento e da chave da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="908e3-148">Add constants to the `Program` class for the event hub connection string, event hub name, storage account container name, storage account name, and storage account key.</span></span> <span data-ttu-id="908e3-149">Adicione o código a seguir, substituindo os espaços reservados pelos valores correspondentes.</span><span class="sxs-lookup"><span data-stu-id="908e3-149">Add the following code, replacing the placeholders with their corresponding values.</span></span>

    ```csharp
    private const string EhConnectionString = "{Event Hubs connection string}";
    private const string EhEntityPath = "{Event Hub path/name}";
    private const string StorageContainerName = "{Storage account container name}";
    private const string StorageAccountName = "{Storage account name}";
    private const string StorageAccountKey = "{Storage account key}";

    private static readonly string StorageConnectionString = string.Format("DefaultEndpointsProtocol=https;AccountName={0};AccountKey={1}", StorageAccountName, StorageAccountKey);
    ```   

3. <span data-ttu-id="908e3-150">Adicione um novo método chamado `MainAsync` à classe `Program`, conforme demonstrado a seguir:</span><span class="sxs-lookup"><span data-stu-id="908e3-150">Add a new method named `MainAsync` to the `Program` class, as follows:</span></span>

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

        // Registers the Event Processor Host and starts receiving messages
        await eventProcessorHost.RegisterEventProcessorAsync<SimpleEventProcessor>();

        Console.WriteLine("Receiving. Press ENTER to stop worker.");
        Console.ReadLine();

        // Disposes of the Event Processor Host
        await eventProcessorHost.UnregisterEventProcessorAsync();
    }
    ```

3. <span data-ttu-id="908e3-151">Adicione a linha de código a seguir ao método `Main`:</span><span class="sxs-lookup"><span data-stu-id="908e3-151">Add the following line of code to the `Main` method:</span></span>

    ```csharp
    MainAsync(args).GetAwaiter().GetResult();
    ```

    <span data-ttu-id="908e3-152">O arquivo Program.cs deve ficar assim:</span><span class="sxs-lookup"><span data-stu-id="908e3-152">Here is what your Program.cs file should look like:</span></span>

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

                // Registers the Event Processor Host and starts receiving messages
                await eventProcessorHost.RegisterEventProcessorAsync<SimpleEventProcessor>();

                Console.WriteLine("Receiving. Press ENTER to stop worker.");
                Console.ReadLine();

                // Disposes of the Event Processor Host
                await eventProcessorHost.UnregisterEventProcessorAsync();
            }
        }
    }
    ```

4. <span data-ttu-id="908e3-153">Execute o programa e certifique-se de que não existem erros.</span><span class="sxs-lookup"><span data-stu-id="908e3-153">Run the program, and ensure that there are no errors.</span></span>

<span data-ttu-id="908e3-154">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="908e3-154">Congratulations!</span></span> <span data-ttu-id="908e3-155">Agora você recebeu mensagens de um hub de eventos usando o Host do Processador de Eventos.</span><span class="sxs-lookup"><span data-stu-id="908e3-155">You have now received messages from an event hub by using the Event Processor Host.</span></span>

## <a name="next-steps"></a><span data-ttu-id="908e3-156">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="908e3-156">Next steps</span></span>
<span data-ttu-id="908e3-157">Você pode saber mais sobre Hubs de Eventos visitando os links abaixo:</span><span class="sxs-lookup"><span data-stu-id="908e3-157">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="908e3-158">Visão Geral dos Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="908e3-158">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="908e3-159">Criar um hub de eventos</span><span class="sxs-lookup"><span data-stu-id="908e3-159">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="908e3-160">Perguntas frequentes sobre os Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="908e3-160">Event Hubs FAQ</span></span>](event-hubs-faq.md)

[1]: ./media/event-hubs-dotnet-standard-getstarted-receive-eph/event-hubs-python1.png
[2]: ./media/event-hubs-dotnet-standard-getstarted-receive-eph/netcore.png
