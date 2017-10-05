---
title: Enviar eventos para Hubs de Eventos do Azure usando o .NET Framework | Microsoft Docs
description: "Introdução ao envio de eventos para Hubs de Eventos usando o .NET Framework"
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
ms.openlocfilehash: 4eb0e7bcc14722010121c2a5945509d6ed736f4f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="send-events-to-azure-event-hubs-using-the-net-framework"></a><span data-ttu-id="5532d-103">Enviar eventos para Hubs de Eventos do Azure usando o .NET Framework</span><span class="sxs-lookup"><span data-stu-id="5532d-103">Send events to Azure Event Hubs using the .NET Framework</span></span>

## <a name="introduction"></a><span data-ttu-id="5532d-104">Introdução</span><span class="sxs-lookup"><span data-stu-id="5532d-104">Introduction</span></span>

<span data-ttu-id="5532d-105">Os Hubs de Eventos são um serviço que processa grandes quantidades de dados de eventos (telemetria) a partir de aplicativos e dispositivos conectados.</span><span class="sxs-lookup"><span data-stu-id="5532d-105">Event Hubs is a service that processes large amounts of event data (telemetry) from connected devices and applications.</span></span> <span data-ttu-id="5532d-106">Depois de coletar dados para Hubs de Eventos, você pode armazenar os dados usando um cluster de armazenamento ou transformá-los usando um provedor de análise em tempo real.</span><span class="sxs-lookup"><span data-stu-id="5532d-106">After you collect data into Event Hubs, you can store the data using a storage cluster or transform it using a real-time analytics provider.</span></span> <span data-ttu-id="5532d-107">Essa funcionalidade de coleta e processamento de eventos em grande escala é um componente fundamental de arquiteturas de aplicativos modernas, incluindo a IoT (Internet das Coisas).</span><span class="sxs-lookup"><span data-stu-id="5532d-107">This large-scale event collection and processing capability is a key component of modern application architectures including the Internet of Things (IoT).</span></span>

<span data-ttu-id="5532d-108">Este tutorial mostra como usar o [portal do Azure](https://portal.azure.com) para criar um hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="5532d-108">This tutorial shows how to use the [Azure portal](https://portal.azure.com) to create an event hub.</span></span> <span data-ttu-id="5532d-109">Ele também mostra como enviar eventos para um hub de eventos usando um aplicativo de console escrito em C# usando o .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="5532d-109">It also shows how to send events to an event hub using a console application written in C# using the .NET Framework.</span></span> <span data-ttu-id="5532d-110">Para receber eventos usando o .NET Framework, veja o artigo [Receber eventos usando o .NET Framework](event-hubs-dotnet-framework-getstarted-receive-eph.md) artigo, ou clique no idioma apropriado de recebimento no sumário à esquerda.</span><span class="sxs-lookup"><span data-stu-id="5532d-110">To receive events using the .NET Framework, see the [Receive events using the .NET Framework](event-hubs-dotnet-framework-getstarted-receive-eph.md) article, or click the appropriate receiving language in the left-hand table of contents.</span></span>

<span data-ttu-id="5532d-111">Para concluir este tutorial, você precisará dos seguintes pré-requisitos:</span><span class="sxs-lookup"><span data-stu-id="5532d-111">To complete this tutorial, you need the following prerequisites:</span></span>

* <span data-ttu-id="5532d-112">[Microsoft Visual Studio 2015 ou superior](http://visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="5532d-112">[Microsoft Visual Studio 2015 or higher](http://visualstudio.com).</span></span> <span data-ttu-id="5532d-113">As capturas de tela neste tutorial usam o Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="5532d-113">The screen shots in this tutorial use Visual Studio 2017.</span></span>
* <span data-ttu-id="5532d-114">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="5532d-114">An active Azure account.</span></span> <span data-ttu-id="5532d-115">Se não tiver uma, você poderá criar uma conta gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="5532d-115">If you don't have one, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="5532d-116">Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="5532d-116">For details, see [Azure Free Trial](https://azure.microsoft.com/free/).</span></span>

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a><span data-ttu-id="5532d-117">Como criar um namespace de hubs de eventos e um hub de eventos</span><span class="sxs-lookup"><span data-stu-id="5532d-117">Create an Event Hubs namespace and an event hub</span></span>

<span data-ttu-id="5532d-118">A primeira etapa é usar o [portal do Azure](https://portal.azure.com) para criar um namespace do tipo Hubs de eventos e obter as credenciais de gerenciamento das quais que seu aplicativo precisa para se comunicar com o hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="5532d-118">The first step is to use the [Azure portal](https://portal.azure.com) to create a namespace of type Event Hubs, and obtain the management credentials your application needs to communicate with the event hub.</span></span> <span data-ttu-id="5532d-119">Para criar um namespace e um hub de eventos, siga o procedimento [neste artigo](event-hubs-create.md) e então continue com as etapas a seguir neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="5532d-119">To create a namespace and event hub, follow the procedure in [this article](event-hubs-create.md), then proceed with the following steps in this tutorial.</span></span>

## <a name="create-a-sender-console-application"></a><span data-ttu-id="5532d-120">Criar um aplicativo de console do remetente</span><span class="sxs-lookup"><span data-stu-id="5532d-120">Create a sender console application</span></span>

<span data-ttu-id="5532d-121">Nesta seção, você escreverá um aplicativo de console do Windows para enviar eventos para o hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="5532d-121">In this section, you'll write a Windows console app that sends events to your event hub.</span></span>

1. <span data-ttu-id="5532d-122">No Visual Studio, crie um novo projeto de aplicativo de área de trabalho do Visual C# usando o modelo de projeto de **Aplicativo de Console** .</span><span class="sxs-lookup"><span data-stu-id="5532d-122">In Visual Studio, create a new Visual C# Desktop App project using the **Console Application** project template.</span></span> <span data-ttu-id="5532d-123">Nomeie o projeto como **Remetente**.</span><span class="sxs-lookup"><span data-stu-id="5532d-123">Name the project **Sender**.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-send/create-sender-csharp1.png)
2. <span data-ttu-id="5532d-124">No Gerenciador de Soluções, clique com o botão direito do mouse no projeto **Remetente** clique em **Gerenciar Pacotes NuGet para Solução**.</span><span class="sxs-lookup"><span data-stu-id="5532d-124">In Solution Explorer, right-click the **Sender** project, and then click **Manage NuGet Packages for Solution**.</span></span> 
3. <span data-ttu-id="5532d-125">Clique na guia **Procurar** e procure `Microsoft Azure Service Bus`.</span><span class="sxs-lookup"><span data-stu-id="5532d-125">Click the **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="5532d-126">Clique em **Instalar**e aceite os termos de uso.</span><span class="sxs-lookup"><span data-stu-id="5532d-126">Click **Install**, and accept the terms of use.</span></span> 
   
    ![](./media/event-hubs-dotnet-framework-getstarted-send/create-sender-csharp2.png)
   
    <span data-ttu-id="5532d-127">O Visual Studio faz o download, instala e adiciona uma referência ao [pacote NuGet de biblioteca do Barramento de Serviço do Azure](https://www.nuget.org/packages/WindowsAzure.ServiceBus).</span><span class="sxs-lookup"><span data-stu-id="5532d-127">Visual Studio downloads, installs, and adds a reference to the [Azure Service Bus library NuGet package](https://www.nuget.org/packages/WindowsAzure.ServiceBus).</span></span>
4. <span data-ttu-id="5532d-128">Adicione as instruções `using` abaixo na parte superior do arquivo **Program.cs** :</span><span class="sxs-lookup"><span data-stu-id="5532d-128">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
  ```csharp
  using System.Threading;
  using Microsoft.ServiceBus.Messaging;
  ```
5. <span data-ttu-id="5532d-129">Adicione os seguintes campos à classe **Programa**, substituindo os valores do espaço reservado pelo nome do hub de eventos criado na seção anterior e pela cadeia de conexão no nível do namespace que você salvou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="5532d-129">Add the following fields to the **Program** class, substituting the placeholder values with the name of the event hub you created in the previous section, and the namespace-level connection string you saved previously.</span></span>
   
  ```csharp
  static string eventHubName = "{Event Hub name}";
  static string connectionString = "{send connection string}";
  ```
6. <span data-ttu-id="5532d-130">Adicione o seguinte método à classe **Programa** :</span><span class="sxs-lookup"><span data-stu-id="5532d-130">Add the following method to the **Program** class:</span></span>
   
  ```csharp
  static void SendingRandomMessages()
  {
      var eventHubClient = EventHubClient.CreateFromConnectionString(connectionString, eventHubName);
      while (true)
      {
          try
          {
              var message = Guid.NewGuid().ToString();
              Console.WriteLine("{0} > Sending message: {1}", DateTime.Now, message);
              eventHubClient.Send(new EventData(Encoding.UTF8.GetBytes(message)));
          }
          catch (Exception exception)
          {
              Console.ForegroundColor = ConsoleColor.Red;
              Console.WriteLine("{0} > Exception: {1}", DateTime.Now, exception.Message);
              Console.ResetColor();
          }
   
          Thread.Sleep(200);
      }
  }
  ```
   
  <span data-ttu-id="5532d-131">Esse método envia continuamente os eventos para seu hub de eventos com um atraso de 200 ms.</span><span class="sxs-lookup"><span data-stu-id="5532d-131">This method continuously sends events to your event hub with a 200-ms delay.</span></span>
7. <span data-ttu-id="5532d-132">Por fim, adicione as seguintes linhas ao método **Main** :</span><span class="sxs-lookup"><span data-stu-id="5532d-132">Finally, add the following lines to the **Main** method:</span></span>
   
  ```csharp
  Console.WriteLine("Press Ctrl-C to stop the sender process");
  Console.WriteLine("Press Enter to start now");
  Console.ReadLine();
  SendingRandomMessages();
  ```
8. <span data-ttu-id="5532d-133">Execute o programa e certifique-se de que não existem erros.</span><span class="sxs-lookup"><span data-stu-id="5532d-133">Run the program, and ensure that there are no errors.</span></span>
  
<span data-ttu-id="5532d-134">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="5532d-134">Congratulations!</span></span> <span data-ttu-id="5532d-135">Agora você enviou mensagens para um hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="5532d-135">You have now sent messages to an event hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5532d-136">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5532d-136">Next steps</span></span>
<span data-ttu-id="5532d-137">Agora que você criou um aplicativo funcional que cria um hub de eventos e envia dados, poderá passar para os seguintes cenários:</span><span class="sxs-lookup"><span data-stu-id="5532d-137">Now that you've built a working application that creates an event hub and sends data, you can move on to the following scenarios:</span></span>

* [<span data-ttu-id="5532d-138">Receber eventos usando o Host de Processador de Eventos</span><span class="sxs-lookup"><span data-stu-id="5532d-138">Receive events using the Event Processor Host</span></span>](event-hubs-dotnet-framework-getstarted-receive-eph.md)
* [<span data-ttu-id="5532d-139">Referência do host de processador de eventos</span><span class="sxs-lookup"><span data-stu-id="5532d-139">Event Processor Host reference</span></span>](/dotnet/api/microsoft.servicebus.messaging.eventprocessorhost)
* [<span data-ttu-id="5532d-140">Visão Geral dos Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="5532d-140">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)

<!-- Images. -->
[19]: ./media/event-hubs-csharp-ephcs-getstarted/create-eh-proj1.png
[20]: ./media/event-hubs-csharp-ephcs-getstarted/create-eh-proj2.png
[21]: ./media/event-hubs-csharp-ephcs-getstarted/run-csharp-ephcs1.png
[22]: ./media/event-hubs-csharp-ephcs-getstarted/run-csharp-ephcs2.png

