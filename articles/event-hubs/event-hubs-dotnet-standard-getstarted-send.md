---
title: Enviar eventos para Hubs de Eventos do Azure usando .NET Standard | Microsoft Docs
description: "Começar a enviar eventos para Hubs de Eventos no .NET Standard"
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
ms.openlocfilehash: 8af9d70965c1c9ad8c49b7d2bb04244fc207058d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-sending-messages-to-azure-event-hubs-in-net-standard"></a><span data-ttu-id="ea0e1-103">Introdução ao envio de mensagens para os Hubs de Eventos do Azure no .NET Standard</span><span class="sxs-lookup"><span data-stu-id="ea0e1-103">Get started sending messages to Azure Event Hubs in .NET Standard</span></span>

> [!NOTE]
> <span data-ttu-id="ea0e1-104">Este exemplo está disponível em [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender).</span><span class="sxs-lookup"><span data-stu-id="ea0e1-104">This sample is available on [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender).</span></span>

<span data-ttu-id="ea0e1-105">Este tutorial mostra como escrever um aplicativo do console do .NET Core que envia um conjunto de mensagens para um hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="ea0e1-105">This tutorial shows how to write a .NET Core console application that sends a set of messages to an event hub.</span></span> <span data-ttu-id="ea0e1-106">É possível executar a solução do [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender) no estado em que se encontra, substituindo as cadeias de caracteres `EhConnectionString` e `EhEntityPath` pelos valores do seu hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="ea0e1-106">You can run the [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender) solution as-is, replacing the `EhConnectionString` and `EhEntityPath` strings with your event hub values.</span></span> <span data-ttu-id="ea0e1-107">Se preferir, é possível seguir as etapas deste tutorial para criar sua própria solução.</span><span class="sxs-lookup"><span data-stu-id="ea0e1-107">Or you can follow the steps in this tutorial to create your own.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ea0e1-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="ea0e1-108">Prerequisites</span></span>

* <span data-ttu-id="ea0e1-109">[Microsoft Visual Studio 2015 ou 2017](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="ea0e1-109">[Microsoft Visual Studio 2015 or 2017](http://www.visualstudio.com).</span></span> <span data-ttu-id="ea0e1-110">Os exemplos neste tutorial usam o Visual Studio 2017, mas também há suporte para o Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="ea0e1-110">The examples in this tutorial use Visual Studio 2017, but Visual Studio 2015 is also supported.</span></span>
* <span data-ttu-id="ea0e1-111">[Ferramentas do .NET Core do Visual Studio 2015 ou 2017](http://www.microsoft.com/net/core).</span><span class="sxs-lookup"><span data-stu-id="ea0e1-111">[.NET Core Visual Studio 2015 or 2017 tools](http://www.microsoft.com/net/core).</span></span>
* <span data-ttu-id="ea0e1-112">Uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="ea0e1-112">An Azure subscription.</span></span>
* <span data-ttu-id="ea0e1-113">Um namespace do hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="ea0e1-113">An event hub namespace.</span></span>

<span data-ttu-id="ea0e1-114">Para enviar mensagens para um hub de eventos, usaremos o Visual Studio para escrever um aplicativo de console do C#.</span><span class="sxs-lookup"><span data-stu-id="ea0e1-114">To send messages to an event hub, we will use Visual Studio to write a C# console application.</span></span>

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a><span data-ttu-id="ea0e1-115">Criar um namespace de Hubs de Eventos e um hub de eventos</span><span class="sxs-lookup"><span data-stu-id="ea0e1-115">Create an Event Hubs namespace and an event hub</span></span>

<span data-ttu-id="ea0e1-116">A primeira etapa é usar o [Portal do Azure](https://portal.azure.com) para criar um namespace para o tipo do hub de eventos e obter as credenciais de gerenciamento que o aplicativo precisa para se comunicar com o hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="ea0e1-116">The first step is to use the [Azure portal](https://portal.azure.com) to create a namespace for the event hub type, and obtain the management credentials that your application needs to communicate with the event hub.</span></span> <span data-ttu-id="ea0e1-117">Para criar um namespace e um hub de eventos, siga o procedimento descrito [neste artigo](event-hubs-create.md) e, em seguida, continue com as próximas etapas.</span><span class="sxs-lookup"><span data-stu-id="ea0e1-117">To create a namespace and an event hub, follow the procedure in [this article](event-hubs-create.md), and then proceed with the following steps.</span></span>

## <a name="create-a-console-application"></a><span data-ttu-id="ea0e1-118">Criar um aplicativo de console</span><span class="sxs-lookup"><span data-stu-id="ea0e1-118">Create a console application</span></span>

<span data-ttu-id="ea0e1-119">Inicie o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ea0e1-119">Start Visual Studio.</span></span> <span data-ttu-id="ea0e1-120">No menu **Arquivo**, clique em **Novo** e em **Projeto**.</span><span class="sxs-lookup"><span data-stu-id="ea0e1-120">From the **File** menu, click **New**, and then click **Project**.</span></span> <span data-ttu-id="ea0e1-121">Crie um aplicativo de console do .NET Core.</span><span class="sxs-lookup"><span data-stu-id="ea0e1-121">Create a .NET Core console application.</span></span>

![Novo Projeto][1]

## <a name="add-the-event-hubs-nuget-package"></a><span data-ttu-id="ea0e1-123">Adicione o pacote NuGet de Hubs de Evento</span><span class="sxs-lookup"><span data-stu-id="ea0e1-123">Add the Event Hubs NuGet package</span></span>

<span data-ttu-id="ea0e1-124">Adicione o pacote NuGet [`Microsoft.Azure.EventHubs`](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) de biblioteca do .NET Standard ao projeto seguindo estas etapas:</span><span class="sxs-lookup"><span data-stu-id="ea0e1-124">Add the [`Microsoft.Azure.EventHubs`](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) .NET Standard library NuGet package to your project by following these steps:</span></span> 

1. <span data-ttu-id="ea0e1-125">Clique com o botão direito do mouse no projeto recém-criado e selecione **Gerenciar Pacotes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="ea0e1-125">Right-click the newly created project and select **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="ea0e1-126">Clique na guia **Procurar**, pesquise por "Microsoft.Azure.EventHubs" e selecione o pacote **Microsoft.Azure.EventHubs**.</span><span class="sxs-lookup"><span data-stu-id="ea0e1-126">Click the **Browse** tab, then search for "Microsoft.Azure.EventHubs" and select the **Microsoft.Azure.EventHubs** package.</span></span> <span data-ttu-id="ea0e1-127">Clique em **Instalar** para concluir a instalação e feche essa caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ea0e1-127">Click **Install** to complete the installation, then close this dialog box.</span></span>

## <a name="write-some-code-to-send-messages-to-the-event-hub"></a><span data-ttu-id="ea0e1-128">Escrever um código para enviar mensagens ao hub de eventos</span><span class="sxs-lookup"><span data-stu-id="ea0e1-128">Write some code to send messages to the event hub</span></span>

1. <span data-ttu-id="ea0e1-129">Adicione as instruções `using` a seguir à parte superior do arquivo Program.cs.</span><span class="sxs-lookup"><span data-stu-id="ea0e1-129">Add the following `using` statements to the top of the Program.cs file.</span></span>

    ```csharp
    using Microsoft.Azure.EventHubs;
    using System.Text;
    using System.Threading.Tasks;
    ```

2. <span data-ttu-id="ea0e1-130">Adicione constantes à classe `Program` para a cadeia de conexão de Hubs de Eventos e o caminho da entidade (nome do hub de eventos individual).</span><span class="sxs-lookup"><span data-stu-id="ea0e1-130">Add constants to the `Program` class for the Event Hubs connection string and entity path (individual event hub name).</span></span> <span data-ttu-id="ea0e1-131">Substitua os espaços reservados nos colchetes pelos valores adequados que foram obtidos na criação do hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="ea0e1-131">Replace the placeholders in brackets with the proper values that were obtained when creating the event hub.</span></span>

    ```csharp
    private static EventHubClient eventHubClient;
    private const string EhConnectionString = "{Event Hubs connection string}";
    private const string EhEntityPath = "{Event Hub path/name}";
    ```

3. <span data-ttu-id="ea0e1-132">Adicione um novo método chamado `MainAsync` à classe `Program`, conforme demonstrado a seguir:</span><span class="sxs-lookup"><span data-stu-id="ea0e1-132">Add a new method named `MainAsync` to the `Program` class, as follows:</span></span>

    ```csharp
    private static async Task MainAsync(string[] args)
    {
        // Creates an EventHubsConnectionStringBuilder object from the connection string, and sets the EntityPath.
        // Typically, the connection string should have the entity path in it, but for the sake of this simple scenario
        // we are using the connection string from the namespace.
        var connectionStringBuilder = new EventHubsConnectionStringBuilder(EhConnectionString)
        {
            EntityPath = EhEntityPath
        };

        eventHubClient = EventHubClient.CreateFromConnectionString(connectionStringBuilder.ToString());

        await SendMessagesToEventHub(100);

        await eventHubClient.CloseAsync();

        Console.WriteLine("Press ENTER to exit.");
        Console.ReadLine();
    }
    ```

4. <span data-ttu-id="ea0e1-133">Adicione um novo método chamado `SendMessagesToEventHub` à classe `Program`, conforme demonstrado a seguir:</span><span class="sxs-lookup"><span data-stu-id="ea0e1-133">Add a new method named `SendMessagesToEventHub` to the `Program` class, as follows:</span></span>

    ```csharp
    // Creates an event hub client and sends 100 messages to the event hub.
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

5. <span data-ttu-id="ea0e1-134">Adicione o código a seguir ao método `Main` na classe `Program`.</span><span class="sxs-lookup"><span data-stu-id="ea0e1-134">Add the following code to the `Main` method in the `Program` class.</span></span>

    ```csharp
    MainAsync(args).GetAwaiter().GetResult();
    ```

   <span data-ttu-id="ea0e1-135">Program.cs deve ficar assim.</span><span class="sxs-lookup"><span data-stu-id="ea0e1-135">Here is what your Program.cs should look like.</span></span>

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
                // Creates an EventHubsConnectionStringBuilder object from the connection string, and sets the EntityPath.
                // Typically, the connection string should have the entity path in it, but for the sake of this simple scenario
                // we are using the connection string from the namespace.
                var connectionStringBuilder = new EventHubsConnectionStringBuilder(EhConnectionString)
                {
                    EntityPath = EhEntityPath
                };

                eventHubClient = EventHubClient.CreateFromConnectionString(connectionStringBuilder.ToString());

                await SendMessagesToEventHub(100);

                await eventHubClient.CloseAsync();

                Console.WriteLine("Press ENTER to exit.");
                Console.ReadLine();
            }

            // Creates an event hub client and sends 100 messages to the event hub.
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

6. <span data-ttu-id="ea0e1-136">Execute o programa e certifique-se de que não existem erros.</span><span class="sxs-lookup"><span data-stu-id="ea0e1-136">Run the program, and ensure that there are no errors.</span></span>

<span data-ttu-id="ea0e1-137">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="ea0e1-137">Congratulations!</span></span> <span data-ttu-id="ea0e1-138">Agora você enviou mensagens para um hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="ea0e1-138">You have now sent messages to an event hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ea0e1-139">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ea0e1-139">Next steps</span></span>
<span data-ttu-id="ea0e1-140">Você pode saber mais sobre Hubs de Eventos visitando os links abaixo:</span><span class="sxs-lookup"><span data-stu-id="ea0e1-140">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="ea0e1-141">Receber eventos de Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="ea0e1-141">Receive events from Event Hubs</span></span>](event-hubs-dotnet-standard-getstarted-receive-eph.md)
* [<span data-ttu-id="ea0e1-142">Visão Geral dos Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="ea0e1-142">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="ea0e1-143">Criar um hub de eventos</span><span class="sxs-lookup"><span data-stu-id="ea0e1-143">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="ea0e1-144">Perguntas frequentes sobre os Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="ea0e1-144">Event Hubs FAQ</span></span>](event-hubs-faq.md)

[1]: ./media/event-hubs-dotnet-standard-getstarted-send/netcore.png
