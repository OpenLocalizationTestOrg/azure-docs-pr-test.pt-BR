---
title: "aaaGet iniciado com filas do barramento de serviço do Azure | Microsoft Docs"
description: "Escreva um aplicativo de console em C# que usa filas de mensagens do Barramento de Serviço."
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 68a34c00-5600-43f6-bbcc-fea599d500da
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: hero-article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 06/26/2017
ms.author: sethm
ms.openlocfilehash: eaa362ab0eabd2427977398c1deab5dc00105ae9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-service-bus-queues"></a><span data-ttu-id="22237-103">Introdução às filas do Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="22237-103">Get started with Service Bus queues</span></span>
[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

## <a name="what-will-be-accomplished"></a><span data-ttu-id="22237-104">O que será realizado</span><span class="sxs-lookup"><span data-stu-id="22237-104">What will be accomplished</span></span>
<span data-ttu-id="22237-105">Este tutorial aborda Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="22237-105">This tutorial covers hello following steps:</span></span>

1. <span data-ttu-id="22237-106">Crie um namespace de barramento de serviço, usando Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="22237-106">Create a Service Bus namespace, using hello Azure portal.</span></span>
2. <span data-ttu-id="22237-107">Crie uma fila do barramento de serviço, usando Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="22237-107">Create a Service Bus queue, using hello Azure portal.</span></span>
3. <span data-ttu-id="22237-108">Grave uma mensagem de um toosend do aplicativo de console.</span><span class="sxs-lookup"><span data-stu-id="22237-108">Write a console application toosend a message.</span></span>
4. <span data-ttu-id="22237-109">Grave uma saudação de tooreceive do aplicativo de console mensagens enviadas na etapa anterior hello.</span><span class="sxs-lookup"><span data-stu-id="22237-109">Write a console application tooreceive hello messages sent in hello previous step.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="22237-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="22237-110">Prerequisites</span></span>
1. <span data-ttu-id="22237-111">[Visual Studio 2015 ou superior](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="22237-111">[Visual Studio 2015 or higher](http://www.visualstudio.com).</span></span> <span data-ttu-id="22237-112">exemplos de saudação neste tutorial usam 2017 do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="22237-112">hello examples in this tutorial use Visual Studio 2017.</span></span>
2. <span data-ttu-id="22237-113">Uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="22237-113">An Azure subscription.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-hello-azure-portal"></a><span data-ttu-id="22237-114">1. Criar um namespace usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="22237-114">1. Create a namespace using hello Azure portal</span></span>
<span data-ttu-id="22237-115">Se você já criou um namespace do sistema de mensagens do barramento de serviço, ir toohello [criar uma fila usando o portal do Azure de saudação](#2-create-a-queue-using-the-azure-portal) seção.</span><span class="sxs-lookup"><span data-stu-id="22237-115">If you've already created a Service Bus Messaging namespace, jump toohello [Create a queue using hello Azure portal](#2-create-a-queue-using-the-azure-portal) section.</span></span>

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="2-create-a-queue-using-hello-azure-portal"></a><span data-ttu-id="22237-116">2. Criar uma fila usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="22237-116">2. Create a queue using hello Azure portal</span></span>
<span data-ttu-id="22237-117">Se você já criou uma fila do barramento de serviço, ir toohello [toohello fila de mensagens de envio](#3-send-messages-to-the-queue) seção.</span><span class="sxs-lookup"><span data-stu-id="22237-117">If you have already created a Service Bus queue, jump toohello [Send messages toohello queue](#3-send-messages-to-the-queue) section.</span></span>

[!INCLUDE [service-bus-create-queue-portal](../../includes/service-bus-create-queue-portal.md)]

## <a name="3-send-messages-toohello-queue"></a><span data-ttu-id="22237-118">3. Mensagens toohello fila de envio</span><span class="sxs-lookup"><span data-stu-id="22237-118">3. Send messages toohello queue</span></span>
<span data-ttu-id="22237-119">fila de mensagens de toohello de toosend, podemos gravar um aplicativo de console c# usando o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="22237-119">toosend messages toohello queue, we write a C# console application using Visual Studio.</span></span>

### <a name="create-a-console-application"></a><span data-ttu-id="22237-120">Criar um aplicativo de console</span><span class="sxs-lookup"><span data-stu-id="22237-120">Create a console application</span></span>

<span data-ttu-id="22237-121">Inicie o Visual Studio e crie um novo projeto de **Aplicativo de console (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="22237-121">Launch Visual Studio and create a new **Console app (.NET Framework)** project.</span></span>

### <a name="add-hello-service-bus-nuget-package"></a><span data-ttu-id="22237-122">Adicionar o pacote do NuGet do barramento de serviço Olá</span><span class="sxs-lookup"><span data-stu-id="22237-122">Add hello Service Bus NuGet package</span></span>
1. <span data-ttu-id="22237-123">Clique com botão direito Olá recém-criado e selecione **gerenciar pacotes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="22237-123">Right-click hello newly created project and select **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="22237-124">Clique em Olá **procurar** guia, procure **barramento de serviço do Microsoft Azure**e, em seguida, selecione Olá **windowsazure. ServiceBus** item.</span><span class="sxs-lookup"><span data-stu-id="22237-124">Click hello **Browse** tab, search for **Microsoft Azure Service Bus**, and then select hello **WindowsAzure.ServiceBus** item.</span></span> <span data-ttu-id="22237-125">Clique em **instalar** toocomplete Olá instalação, em seguida, feche esta caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="22237-125">Click **Install** toocomplete hello installation, then close this dialog box.</span></span>
   
    ![Selecionar um pacote NuGet][nuget-pkg]

### <a name="write-some-code-toosend-a-message-toohello-queue"></a><span data-ttu-id="22237-127">Gravar algumas toosend código uma fila de mensagens toohello</span><span class="sxs-lookup"><span data-stu-id="22237-127">Write some code toosend a message toohello queue</span></span>
1. <span data-ttu-id="22237-128">Adicione o seguinte Olá `using` superior de toohello de instrução do arquivo Program.cs de saudação.</span><span class="sxs-lookup"><span data-stu-id="22237-128">Add hello following `using` statement toohello top of hello Program.cs file.</span></span>
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
2. <span data-ttu-id="22237-129">Adicionar Olá toohello de código a seguir `Main` método.</span><span class="sxs-lookup"><span data-stu-id="22237-129">Add hello following code toohello `Main` method.</span></span> <span data-ttu-id="22237-130">Saudação de conjunto `connectionString` conexão toohello variável de cadeia de caracteres obtido ao criar namespace hello e definir `queueName` toohello nome da fila que você usou ao criar a fila de saudação.</span><span class="sxs-lookup"><span data-stu-id="22237-130">Set hello `connectionString` variable toohello connection string that you obtained when creating hello namespace, and set `queueName` toohello queue name that you used when creating hello queue.</span></span>
   
    ```csharp
    var connectionString = "<your connection string>";
    var queueName = "<your queue name>";
   
    var client = QueueClient.CreateFromConnectionString(connectionString, queueName);
    var message = new BrokeredMessage("This is a test message!");

    Console.WriteLine(String.Format("Message id: {0}", message.MessageId));

    client.Send(message);

    Console.WriteLine("Message successfully sent! Press ENTER tooexit program");
    Console.ReadLine();
    ```
   
    <span data-ttu-id="22237-131">Seu arquivo Program.cs deve ficar assim.</span><span class="sxs-lookup"><span data-stu-id="22237-131">Here is what your Program.cs file should look like.</span></span>
   
    ```csharp
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    using Microsoft.ServiceBus.Messaging;

    namespace qsend
    {
        class Program
        {
            static void Main(string[] args)
            {
                var connectionString = "Endpoint=sb://<your namespace>.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=<your key>";
                var queueName = "<your queue name>";

                var client = QueueClient.CreateFromConnectionString(connectionString, queueName);
                var message = new BrokeredMessage("This is a test message!");

                Console.WriteLine(String.Format("Message id: {0}", message.MessageId));

                client.Send(message);

                Console.WriteLine("Message successfully sent! Press ENTER tooexit program");
                Console.ReadLine();
            }
        }
    }
    ```
3. <span data-ttu-id="22237-132">Execute o programa hello e verifique Olá portal do Azure: clique em nome de saudação da fila no namespace de saudação **visão geral** folha.</span><span class="sxs-lookup"><span data-stu-id="22237-132">Run hello program, and check hello Azure portal: click hello name of your queue in hello namespace **Overview** blade.</span></span> <span data-ttu-id="22237-133">fila de saudação **Essentials** folha é exibida.</span><span class="sxs-lookup"><span data-stu-id="22237-133">hello queue **Essentials** blade is displayed.</span></span> <span data-ttu-id="22237-134">Observe que Olá **contagem de mensagens ativa** valor agora deve ser 1.</span><span class="sxs-lookup"><span data-stu-id="22237-134">Notice that hello **Active Message Count** value should now be 1.</span></span> <span data-ttu-id="22237-135">Cada vez que executar o aplicativo de remetente hello sem recuperar mensagens de saudação, esse valor aumenta em 1.</span><span class="sxs-lookup"><span data-stu-id="22237-135">Each time you run hello sender application without retrieving hello messages, this value increases by 1.</span></span> <span data-ttu-id="22237-136">Também Observe que tamanho atual de saudação da fila de saudação de incrementos de cada aplicativo de saudação do tempo adiciona uma fila de mensagens toohello.</span><span class="sxs-lookup"><span data-stu-id="22237-136">Also note that hello current size of hello queue increments each time hello app adds a message toohello queue.</span></span>
   
      ![Tamanho da mensagem][queue-message]

## <a name="4-receive-messages-from-hello-queue"></a><span data-ttu-id="22237-138">4. Receber mensagens da fila de saudação</span><span class="sxs-lookup"><span data-stu-id="22237-138">4. Receive messages from hello queue</span></span>

1. <span data-ttu-id="22237-139">Você acabou de enviar mensagens de saudação do tooreceive criar um novo aplicativo de console e adicionar um pacote de NuGet do barramento de serviço do toohello de referência, aplicativo de remetente anterior toohello semelhante.</span><span class="sxs-lookup"><span data-stu-id="22237-139">tooreceive hello messages you just sent, create a new console application and add a reference toohello Service Bus NuGet package, similar toohello previous sender application.</span></span>
2. <span data-ttu-id="22237-140">Adicione o seguinte Olá `using` superior de toohello de instrução do arquivo Program.cs de saudação.</span><span class="sxs-lookup"><span data-stu-id="22237-140">Add hello following `using` statement toohello top of hello Program.cs file.</span></span>
   
    ```csharp
    using Microsoft.ServiceBus.Messaging;
    ```
3. <span data-ttu-id="22237-141">Adicionar Olá toohello de código a seguir `Main` método.</span><span class="sxs-lookup"><span data-stu-id="22237-141">Add hello following code toohello `Main` method.</span></span> <span data-ttu-id="22237-142">Saudação de conjunto `connectionString` toohello variável cadeia de conexão que foi obtida durante a criação de namespace hello e defina `queueName` toohello nome da fila que você usou ao criar a fila de saudação.</span><span class="sxs-lookup"><span data-stu-id="22237-142">Set hello `connectionString` variable toohello connection string that was obtained when creating hello namespace, and set `queueName` toohello queue name that you used when creating hello queue.</span></span>
   
    ```csharp
    var connectionString = "<your connection string>";
    var queueName = "<your queue name>";
   
    var client = QueueClient.CreateFromConnectionString(connectionString, queueName);
   
    client.OnMessage(message =>
    {
      Console.WriteLine(String.Format("Message body: {0}", message.GetBody<String>()));
      Console.WriteLine(String.Format("Message id: {0}", message.MessageId));
    });
   
    Console.WriteLine("Press ENTER tooexit program");
    Console.ReadLine();
    ```
   
    <span data-ttu-id="22237-143">O arquivo Program.cs deve ficar assim:</span><span class="sxs-lookup"><span data-stu-id="22237-143">Here is what your Program.cs file should look like:</span></span>
   
    ```csharp
    using System;
    using Microsoft.ServiceBus.Messaging;
   
    namespace GettingStartedWithQueues
    {
      class Program
      {
        static void Main(string[] args)
        {
          var connectionString = "Endpoint=sb://<your namespace>.servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=<your key>";;
          var queueName = "<your queue name>";
   
          var client = QueueClient.CreateFromConnectionString(connectionString, queueName);
   
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
4. <span data-ttu-id="22237-144">Executar programa hello e verificar novamente o portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="22237-144">Run hello program, and check hello portal again.</span></span> <span data-ttu-id="22237-145">Observe que Olá **contagem de mensagens ativa** e **atual** valores agora são 0.</span><span class="sxs-lookup"><span data-stu-id="22237-145">Notice that hello **Active Message Count** and **Current** values are now 0.</span></span>
   
    ![Comprimento da fila][queue-message-receive]

<span data-ttu-id="22237-147">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="22237-147">Congratulations!</span></span> <span data-ttu-id="22237-148">Agora, você criou uma fila, enviou uma mensagem e recebeu uma mensagem.</span><span class="sxs-lookup"><span data-stu-id="22237-148">You have now created a queue, sent a message, and received a message.</span></span>

## <a name="next-steps"></a><span data-ttu-id="22237-149">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="22237-149">Next steps</span></span>

<span data-ttu-id="22237-150">Confira nosso [repositório GitHub com exemplos](https://github.com/Azure/azure-service-bus/tree/master/samples) que demonstram algumas das mais recursos avançados do barramento de serviço de mensagens de saudação.</span><span class="sxs-lookup"><span data-stu-id="22237-150">Check out our [GitHub repository with samples](https://github.com/Azure/azure-service-bus/tree/master/samples) that demonstrate some of hello more advanced features of Service Bus messaging.</span></span>

<!--Image references-->

[nuget-pkg]: ./media/service-bus-dotnet-get-started-with-queues/nuget-package.png
[queue-message]: ./media/service-bus-dotnet-get-started-with-queues/queue-message.png
[queue-message-receive]: ./media/service-bus-dotnet-get-started-with-queues/queue-message-receive.png
[github-samples]: https://github.com/Azure-Samples/azure-servicebus-messaging-samples
