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
# <a name="get-started-sending-messages-tooazure-event-hubs-in-net-standard"></a><span data-ttu-id="f8931-103">Começar a enviar mensagens tooAzure Hubs de eventos no .NET padrão</span><span class="sxs-lookup"><span data-stu-id="f8931-103">Get started sending messages tooAzure Event Hubs in .NET Standard</span></span>

> [!NOTE]
> <span data-ttu-id="f8931-104">Este exemplo está disponível em [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender).</span><span class="sxs-lookup"><span data-stu-id="f8931-104">This sample is available on [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender).</span></span>

<span data-ttu-id="f8931-105">Este tutorial mostra como toowrite um aplicativo de console .NET Core que envia um conjunto de mensagens tooan hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="f8931-105">This tutorial shows how toowrite a .NET Core console application that sends a set of messages tooan event hub.</span></span> <span data-ttu-id="f8931-106">Você pode executar Olá [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender) solução como-está, substituindo Olá `EhConnectionString` e `EhEntityPath` cadeias de caracteres com seus valores de hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="f8931-106">You can run hello [GitHub](https://github.com/Azure/azure-event-hubs/tree/master/samples/DotNet/Microsoft.Azure.EventHubs/SampleSender) solution as-is, replacing hello `EhConnectionString` and `EhEntityPath` strings with your event hub values.</span></span> <span data-ttu-id="f8931-107">Ou você pode seguir Olá etapas neste tutorial toocreate seus próprios.</span><span class="sxs-lookup"><span data-stu-id="f8931-107">Or you can follow hello steps in this tutorial toocreate your own.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f8931-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="f8931-108">Prerequisites</span></span>

* <span data-ttu-id="f8931-109">[Microsoft Visual Studio 2015 ou 2017](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="f8931-109">[Microsoft Visual Studio 2015 or 2017](http://www.visualstudio.com).</span></span> <span data-ttu-id="f8931-110">Também há suporte para este tutorial 2017 do Visual Studio, use os exemplos Hello, mas o Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="f8931-110">hello examples in this tutorial use Visual Studio 2017, but Visual Studio 2015 is also supported.</span></span>
* <span data-ttu-id="f8931-111">[Ferramentas do .NET Core do Visual Studio 2015 ou 2017](http://www.microsoft.com/net/core).</span><span class="sxs-lookup"><span data-stu-id="f8931-111">[.NET Core Visual Studio 2015 or 2017 tools](http://www.microsoft.com/net/core).</span></span>
* <span data-ttu-id="f8931-112">Uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="f8931-112">An Azure subscription.</span></span>
* <span data-ttu-id="f8931-113">Um namespace do hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="f8931-113">An event hub namespace.</span></span>

<span data-ttu-id="f8931-114">hub de eventos do toosend mensagens tooan, usaremos o Visual Studio toowrite um aplicativo de console c#.</span><span class="sxs-lookup"><span data-stu-id="f8931-114">toosend messages tooan event hub, we will use Visual Studio toowrite a C# console application.</span></span>

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a><span data-ttu-id="f8931-115">Criar um namespace de Hubs de Eventos e um hub de eventos</span><span class="sxs-lookup"><span data-stu-id="f8931-115">Create an Event Hubs namespace and an event hub</span></span>

<span data-ttu-id="f8931-116">Olá primeira etapa é Olá toouse [portal do Azure](https://portal.azure.com) toocreate um namespace para o tipo do hub de evento Olá e obter credenciais de gerenciamento que seu aplicativo precisa toocommunicate com hub de eventos de saudação de saudação.</span><span class="sxs-lookup"><span data-stu-id="f8931-116">hello first step is toouse hello [Azure portal](https://portal.azure.com) toocreate a namespace for hello event hub type, and obtain hello management credentials that your application needs toocommunicate with hello event hub.</span></span> <span data-ttu-id="f8931-117">toocreate um namespace e um hub de eventos, siga Olá procedimento [neste artigo](event-hubs-create.md)e continue com a saudação etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="f8931-117">toocreate a namespace and an event hub, follow hello procedure in [this article](event-hubs-create.md), and then proceed with hello following steps.</span></span>

## <a name="create-a-console-application"></a><span data-ttu-id="f8931-118">Criar um aplicativo de console</span><span class="sxs-lookup"><span data-stu-id="f8931-118">Create a console application</span></span>

<span data-ttu-id="f8931-119">Inicie o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f8931-119">Start Visual Studio.</span></span> <span data-ttu-id="f8931-120">De saudação **arquivo** menu, clique em **novo**e, em seguida, clique em **projeto**.</span><span class="sxs-lookup"><span data-stu-id="f8931-120">From hello **File** menu, click **New**, and then click **Project**.</span></span> <span data-ttu-id="f8931-121">Crie um aplicativo de console do .NET Core.</span><span class="sxs-lookup"><span data-stu-id="f8931-121">Create a .NET Core console application.</span></span>

![Novo Projeto][1]

## <a name="add-hello-event-hubs-nuget-package"></a><span data-ttu-id="f8931-123">Adicionar pacote de NuGet de Hubs de evento Olá</span><span class="sxs-lookup"><span data-stu-id="f8931-123">Add hello Event Hubs NuGet package</span></span>

<span data-ttu-id="f8931-124">Adicionar Olá [ `Microsoft.Azure.EventHubs` ](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) .NET padrão biblioteca NuGet pacote tooyour projeto seguindo estas etapas:</span><span class="sxs-lookup"><span data-stu-id="f8931-124">Add hello [`Microsoft.Azure.EventHubs`](https://www.nuget.org/packages/Microsoft.Azure.EventHubs/) .NET Standard library NuGet package tooyour project by following these steps:</span></span> 

1. <span data-ttu-id="f8931-125">Clique com botão direito Olá recém-criado e selecione **gerenciar pacotes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="f8931-125">Right-click hello newly created project and select **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="f8931-126">Clique em Olá **procurar** guia, procure por "Microsoft.Azure.EventHubs" e selecione Olá **Microsoft.Azure.EventHubs** pacote.</span><span class="sxs-lookup"><span data-stu-id="f8931-126">Click hello **Browse** tab, then search for "Microsoft.Azure.EventHubs" and select hello **Microsoft.Azure.EventHubs** package.</span></span> <span data-ttu-id="f8931-127">Clique em **instalar** toocomplete Olá instalação, em seguida, feche esta caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="f8931-127">Click **Install** toocomplete hello installation, then close this dialog box.</span></span>

## <a name="write-some-code-toosend-messages-toohello-event-hub"></a><span data-ttu-id="f8931-128">Gravar algumas hub de eventos do código toosend mensagens toohello</span><span class="sxs-lookup"><span data-stu-id="f8931-128">Write some code toosend messages toohello event hub</span></span>

1. <span data-ttu-id="f8931-129">Adicione o seguinte Olá `using` superior de toohello instruções do arquivo Program.cs de saudação.</span><span class="sxs-lookup"><span data-stu-id="f8931-129">Add hello following `using` statements toohello top of hello Program.cs file.</span></span>

    ```csharp
    using Microsoft.Azure.EventHubs;
    using System.Text;
    using System.Threading.Tasks;
    ```

2. <span data-ttu-id="f8931-130">Adicionar constantes toohello `Program` classe para o hello Hubs de evento conexão cadeia de caracteres e entidade (nome de hub de evento individual).</span><span class="sxs-lookup"><span data-stu-id="f8931-130">Add constants toohello `Program` class for hello Event Hubs connection string and entity path (individual event hub name).</span></span> <span data-ttu-id="f8931-131">Substitua espaços reservados de saudação entre colchetes com valores adequados do hello obtidos ao criar o hub de eventos de saudação.</span><span class="sxs-lookup"><span data-stu-id="f8931-131">Replace hello placeholders in brackets with hello proper values that were obtained when creating hello event hub.</span></span>

    ```csharp
    private static EventHubClient eventHubClient;
    private const string EhConnectionString = "{Event Hubs connection string}";
    private const string EhEntityPath = "{Event Hub path/name}";
    ```

3. <span data-ttu-id="f8931-132">Adicionar um novo método chamado `MainAsync` toohello `Program` classe, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="f8931-132">Add a new method named `MainAsync` toohello `Program` class, as follows:</span></span>

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

4. <span data-ttu-id="f8931-133">Adicionar um novo método chamado `SendMessagesToEventHub` toohello `Program` classe, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="f8931-133">Add a new method named `SendMessagesToEventHub` toohello `Program` class, as follows:</span></span>

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

5. <span data-ttu-id="f8931-134">Adicionar Olá toohello de código a seguir `Main` método hello `Program` classe.</span><span class="sxs-lookup"><span data-stu-id="f8931-134">Add hello following code toohello `Main` method in hello `Program` class.</span></span>

    ```csharp
    MainAsync(args).GetAwaiter().GetResult();
    ```

   <span data-ttu-id="f8931-135">Program.cs deve ficar assim.</span><span class="sxs-lookup"><span data-stu-id="f8931-135">Here is what your Program.cs should look like.</span></span>

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

6. <span data-ttu-id="f8931-136">Executar programa hello e certifique-se de que não existem erros.</span><span class="sxs-lookup"><span data-stu-id="f8931-136">Run hello program, and ensure that there are no errors.</span></span>

<span data-ttu-id="f8931-137">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="f8931-137">Congratulations!</span></span> <span data-ttu-id="f8931-138">Agora você enviou hub de eventos de tooan de mensagens.</span><span class="sxs-lookup"><span data-stu-id="f8931-138">You have now sent messages tooan event hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f8931-139">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f8931-139">Next steps</span></span>
<span data-ttu-id="f8931-140">Você pode aprender mais sobre os Hubs de eventos visitando Olá links a seguir:</span><span class="sxs-lookup"><span data-stu-id="f8931-140">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="f8931-141">Receber eventos de Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="f8931-141">Receive events from Event Hubs</span></span>](event-hubs-dotnet-standard-getstarted-receive-eph.md)
* [<span data-ttu-id="f8931-142">Visão Geral dos Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="f8931-142">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="f8931-143">Criar um hub de eventos</span><span class="sxs-lookup"><span data-stu-id="f8931-143">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="f8931-144">Perguntas frequentes sobre os Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="f8931-144">Event Hubs FAQ</span></span>](event-hubs-faq.md)

[1]: ./media/event-hubs-dotnet-standard-getstarted-send/netcore.png
