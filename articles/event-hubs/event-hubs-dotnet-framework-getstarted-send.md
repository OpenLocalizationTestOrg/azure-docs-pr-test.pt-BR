---
title: "Hubs de eventos de aaaSend eventos tooAzure usando Olá do .NET Framework | Microsoft Docs"
description: "Começar a enviar eventos Hubs tooEvent usando saudação do .NET Framework"
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
ms.openlocfilehash: 05514546a6094096e4a3c800db058190076de80a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="send-events-tooazure-event-hubs-using-hello-net-framework"></a><span data-ttu-id="f0477-103">Enviar eventos tooAzure Hubs de eventos usando saudação do .NET Framework</span><span class="sxs-lookup"><span data-stu-id="f0477-103">Send events tooAzure Event Hubs using hello .NET Framework</span></span>

## <a name="introduction"></a><span data-ttu-id="f0477-104">Introdução</span><span class="sxs-lookup"><span data-stu-id="f0477-104">Introduction</span></span>

<span data-ttu-id="f0477-105">Os Hubs de Eventos são um serviço que processa grandes quantidades de dados de eventos (telemetria) a partir de aplicativos e dispositivos conectados.</span><span class="sxs-lookup"><span data-stu-id="f0477-105">Event Hubs is a service that processes large amounts of event data (telemetry) from connected devices and applications.</span></span> <span data-ttu-id="f0477-106">Depois de coletar dados para Hubs de eventos, você pode armazenar dados de saudação usando um cluster de armazenamento ou transformá-lo usando um provedor de análise em tempo real.</span><span class="sxs-lookup"><span data-stu-id="f0477-106">After you collect data into Event Hubs, you can store hello data using a storage cluster or transform it using a real-time analytics provider.</span></span> <span data-ttu-id="f0477-107">Essa capacidade de coleta e processamento de evento em grande escala é um componente fundamental de arquiteturas de aplicativo moderno incluindo Olá Internet das coisas (IoT).</span><span class="sxs-lookup"><span data-stu-id="f0477-107">This large-scale event collection and processing capability is a key component of modern application architectures including hello Internet of Things (IoT).</span></span>

<span data-ttu-id="f0477-108">Este tutorial mostra como Olá toouse [portal do Azure](https://portal.azure.com) toocreate um hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="f0477-108">This tutorial shows how toouse hello [Azure portal](https://portal.azure.com) toocreate an event hub.</span></span> <span data-ttu-id="f0477-109">Ele também mostra como o hub de eventos toosend eventos tooan usando um aplicativo de console escrito em c# usando Olá do .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="f0477-109">It also shows how toosend events tooan event hub using a console application written in C# using hello .NET Framework.</span></span> <span data-ttu-id="f0477-110">eventos de tooreceive usando saudação do .NET Framework, consulte Olá [receber eventos usando saudação do .NET Framework](event-hubs-dotnet-framework-getstarted-receive-eph.md) artigo ou clique em idioma de recebimento apropriado Olá Olá esquerdo sumário.</span><span class="sxs-lookup"><span data-stu-id="f0477-110">tooreceive events using hello .NET Framework, see hello [Receive events using hello .NET Framework](event-hubs-dotnet-framework-getstarted-receive-eph.md) article, or click hello appropriate receiving language in hello left-hand table of contents.</span></span>

<span data-ttu-id="f0477-111">toocomplete neste tutorial, você precisa Olá pré-requisitos a seguir:</span><span class="sxs-lookup"><span data-stu-id="f0477-111">toocomplete this tutorial, you need hello following prerequisites:</span></span>

* <span data-ttu-id="f0477-112">[Microsoft Visual Studio 2015 ou superior](http://visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="f0477-112">[Microsoft Visual Studio 2015 or higher](http://visualstudio.com).</span></span> <span data-ttu-id="f0477-113">capturas de tela de saudação neste tutorial usam 2017 do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f0477-113">hello screen shots in this tutorial use Visual Studio 2017.</span></span>
* <span data-ttu-id="f0477-114">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="f0477-114">An active Azure account.</span></span> <span data-ttu-id="f0477-115">Se não tiver uma, você poderá criar uma conta gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="f0477-115">If you don't have one, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="f0477-116">Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="f0477-116">For details, see [Azure Free Trial](https://azure.microsoft.com/free/).</span></span>

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a><span data-ttu-id="f0477-117">Criar um namespace de Hubs de Eventos e um hub de eventos</span><span class="sxs-lookup"><span data-stu-id="f0477-117">Create an Event Hubs namespace and an event hub</span></span>

<span data-ttu-id="f0477-118">Olá primeira etapa é Olá toouse [portal do Azure](https://portal.azure.com) toocreate um namespace do tipo de Hubs de eventos e obter Olá toocommunicate com hub de eventos de saudação do seu aplicativo precisa de credenciais de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="f0477-118">hello first step is toouse hello [Azure portal](https://portal.azure.com) toocreate a namespace of type Event Hubs, and obtain hello management credentials your application needs toocommunicate with hello event hub.</span></span> <span data-ttu-id="f0477-119">toocreate um namespace e hub de eventos, siga o procedimento Olá [neste artigo](event-hubs-create.md), continue com a saudação seguindo as etapas neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="f0477-119">toocreate a namespace and event hub, follow hello procedure in [this article](event-hubs-create.md), then proceed with hello following steps in this tutorial.</span></span>

## <a name="create-a-sender-console-application"></a><span data-ttu-id="f0477-120">Criar um aplicativo de console do remetente</span><span class="sxs-lookup"><span data-stu-id="f0477-120">Create a sender console application</span></span>

<span data-ttu-id="f0477-121">Nesta seção, você vai escrever um aplicativo de console do Windows que envia o hub de eventos de tooyour de eventos.</span><span class="sxs-lookup"><span data-stu-id="f0477-121">In this section, you'll write a Windows console app that sends events tooyour event hub.</span></span>

1. <span data-ttu-id="f0477-122">No Visual Studio, crie um novo projeto de aplicativo de área de trabalho do Visual C# usando Olá **aplicativo de Console** modelo de projeto.</span><span class="sxs-lookup"><span data-stu-id="f0477-122">In Visual Studio, create a new Visual C# Desktop App project using hello **Console Application** project template.</span></span> <span data-ttu-id="f0477-123">Projeto de saudação do nome **remetente**.</span><span class="sxs-lookup"><span data-stu-id="f0477-123">Name hello project **Sender**.</span></span>
   
    ![](./media/event-hubs-dotnet-framework-getstarted-send/create-sender-csharp1.png)
2. <span data-ttu-id="f0477-124">No Gerenciador de soluções, clique com botão direito Olá **remetente** do projeto e, em seguida, clique em **gerenciar pacotes NuGet para solução**.</span><span class="sxs-lookup"><span data-stu-id="f0477-124">In Solution Explorer, right-click hello **Sender** project, and then click **Manage NuGet Packages for Solution**.</span></span> 
3. <span data-ttu-id="f0477-125">Clique em Olá **procurar** guia e, em seguida, procurar `Microsoft Azure Service Bus`.</span><span class="sxs-lookup"><span data-stu-id="f0477-125">Click hello **Browse** tab, then search for `Microsoft Azure Service Bus`.</span></span> <span data-ttu-id="f0477-126">Clique em **instalar**e aceite os termos de uso do hello.</span><span class="sxs-lookup"><span data-stu-id="f0477-126">Click **Install**, and accept hello terms of use.</span></span> 
   
    ![](./media/event-hubs-dotnet-framework-getstarted-send/create-sender-csharp2.png)
   
    <span data-ttu-id="f0477-127">Downloads do Visual Studio, instala e adiciona uma referência toohello [pacote de NuGet de biblioteca do Azure Service Bus](https://www.nuget.org/packages/WindowsAzure.ServiceBus).</span><span class="sxs-lookup"><span data-stu-id="f0477-127">Visual Studio downloads, installs, and adds a reference toohello [Azure Service Bus library NuGet package](https://www.nuget.org/packages/WindowsAzure.ServiceBus).</span></span>
4. <span data-ttu-id="f0477-128">Adicione o seguinte Olá `using` instruções na parte superior de saudação do hello **Program.cs** arquivo:</span><span class="sxs-lookup"><span data-stu-id="f0477-128">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
  ```csharp
  using System.Threading;
  using Microsoft.ServiceBus.Messaging;
  ```
5. <span data-ttu-id="f0477-129">Adicionar Olá toohello campos a seguir **programa** classe, substituindo valores de espaço reservado de saudação com nome de saudação do hub de eventos Olá você criou na seção anterior hello e cadeia de caracteres de conexão de nível de namespace Olá você salvou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="f0477-129">Add hello following fields toohello **Program** class, substituting hello placeholder values with hello name of hello event hub you created in hello previous section, and hello namespace-level connection string you saved previously.</span></span>
   
  ```csharp
  static string eventHubName = "{Event Hub name}";
  static string connectionString = "{send connection string}";
  ```
6. <span data-ttu-id="f0477-130">Adicionar Olá após o método toohello **programa** classe:</span><span class="sxs-lookup"><span data-stu-id="f0477-130">Add hello following method toohello **Program** class:</span></span>
   
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
   
  <span data-ttu-id="f0477-131">Esse método envia continuamente o hub de eventos de tooyour eventos com um atraso de 200 ms.</span><span class="sxs-lookup"><span data-stu-id="f0477-131">This method continuously sends events tooyour event hub with a 200-ms delay.</span></span>
7. <span data-ttu-id="f0477-132">Finalmente, adicione Olá toohello linhas a seguir **principal** método:</span><span class="sxs-lookup"><span data-stu-id="f0477-132">Finally, add hello following lines toohello **Main** method:</span></span>
   
  ```csharp
  Console.WriteLine("Press Ctrl-C toostop hello sender process");
  Console.WriteLine("Press Enter toostart now");
  Console.ReadLine();
  SendingRandomMessages();
  ```
8. <span data-ttu-id="f0477-133">Executar programa hello e certifique-se de que não existem erros.</span><span class="sxs-lookup"><span data-stu-id="f0477-133">Run hello program, and ensure that there are no errors.</span></span>
  
<span data-ttu-id="f0477-134">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="f0477-134">Congratulations!</span></span> <span data-ttu-id="f0477-135">Agora você enviou hub de eventos de tooan de mensagens.</span><span class="sxs-lookup"><span data-stu-id="f0477-135">You have now sent messages tooan event hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f0477-136">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f0477-136">Next steps</span></span>
<span data-ttu-id="f0477-137">Agora que você construiu um aplicativo de trabalho que cria um hub de eventos e envia dados, você pode mover em toohello os seguintes cenários:</span><span class="sxs-lookup"><span data-stu-id="f0477-137">Now that you've built a working application that creates an event hub and sends data, you can move on toohello following scenarios:</span></span>

* [<span data-ttu-id="f0477-138">Receber eventos usando Olá Host de processador de eventos</span><span class="sxs-lookup"><span data-stu-id="f0477-138">Receive events using hello Event Processor Host</span></span>](event-hubs-dotnet-framework-getstarted-receive-eph.md)
* [<span data-ttu-id="f0477-139">Referência do host de processador de eventos</span><span class="sxs-lookup"><span data-stu-id="f0477-139">Event Processor Host reference</span></span>](/dotnet/api/microsoft.servicebus.messaging.eventprocessorhost)
* [<span data-ttu-id="f0477-140">Visão Geral dos Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="f0477-140">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)

<!-- Images. -->
[19]: ./media/event-hubs-csharp-ephcs-getstarted/create-eh-proj1.png
[20]: ./media/event-hubs-csharp-ephcs-getstarted/create-eh-proj2.png
[21]: ./media/event-hubs-csharp-ephcs-getstarted/run-csharp-ephcs1.png
[22]: ./media/event-hubs-csharp-ephcs-getstarted/run-csharp-ephcs2.png

