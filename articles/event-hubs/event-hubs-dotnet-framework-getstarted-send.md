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
# <a name="send-events-tooazure-event-hubs-using-hello-net-framework"></a>Enviar eventos tooAzure Hubs de eventos usando saudação do .NET Framework

## <a name="introduction"></a>Introdução

Os Hubs de Eventos são um serviço que processa grandes quantidades de dados de eventos (telemetria) a partir de aplicativos e dispositivos conectados. Depois de coletar dados para Hubs de eventos, você pode armazenar dados de saudação usando um cluster de armazenamento ou transformá-lo usando um provedor de análise em tempo real. Essa capacidade de coleta e processamento de evento em grande escala é um componente fundamental de arquiteturas de aplicativo moderno incluindo Olá Internet das coisas (IoT).

Este tutorial mostra como Olá toouse [portal do Azure](https://portal.azure.com) toocreate um hub de eventos. Ele também mostra como o hub de eventos toosend eventos tooan usando um aplicativo de console escrito em c# usando Olá do .NET Framework. eventos de tooreceive usando saudação do .NET Framework, consulte Olá [receber eventos usando saudação do .NET Framework](event-hubs-dotnet-framework-getstarted-receive-eph.md) artigo ou clique em idioma de recebimento apropriado Olá Olá esquerdo sumário.

toocomplete neste tutorial, você precisa Olá pré-requisitos a seguir:

* [Microsoft Visual Studio 2015 ou superior](http://visualstudio.com). capturas de tela de saudação neste tutorial usam 2017 do Visual Studio.
* Uma conta ativa do Azure. Se não tiver uma, você poderá criar uma conta gratuita em apenas alguns minutos. Para obter detalhes, consulte [Avaliação gratuita do Azure](https://azure.microsoft.com/free/).

## <a name="create-an-event-hubs-namespace-and-an-event-hub"></a>Criar um namespace de Hubs de Eventos e um hub de eventos

Olá primeira etapa é Olá toouse [portal do Azure](https://portal.azure.com) toocreate um namespace do tipo de Hubs de eventos e obter Olá toocommunicate com hub de eventos de saudação do seu aplicativo precisa de credenciais de gerenciamento. toocreate um namespace e hub de eventos, siga o procedimento Olá [neste artigo](event-hubs-create.md), continue com a saudação seguindo as etapas neste tutorial.

## <a name="create-a-sender-console-application"></a>Criar um aplicativo de console do remetente

Nesta seção, você vai escrever um aplicativo de console do Windows que envia o hub de eventos de tooyour de eventos.

1. No Visual Studio, crie um novo projeto de aplicativo de área de trabalho do Visual C# usando Olá **aplicativo de Console** modelo de projeto. Projeto de saudação do nome **remetente**.
   
    ![](./media/event-hubs-dotnet-framework-getstarted-send/create-sender-csharp1.png)
2. No Gerenciador de soluções, clique com botão direito Olá **remetente** do projeto e, em seguida, clique em **gerenciar pacotes NuGet para solução**. 
3. Clique em Olá **procurar** guia e, em seguida, procurar `Microsoft Azure Service Bus`. Clique em **instalar**e aceite os termos de uso do hello. 
   
    ![](./media/event-hubs-dotnet-framework-getstarted-send/create-sender-csharp2.png)
   
    Downloads do Visual Studio, instala e adiciona uma referência toohello [pacote de NuGet de biblioteca do Azure Service Bus](https://www.nuget.org/packages/WindowsAzure.ServiceBus).
4. Adicione o seguinte Olá `using` instruções na parte superior de saudação do hello **Program.cs** arquivo:
   
  ```csharp
  using System.Threading;
  using Microsoft.ServiceBus.Messaging;
  ```
5. Adicionar Olá toohello campos a seguir **programa** classe, substituindo valores de espaço reservado de saudação com nome de saudação do hub de eventos Olá você criou na seção anterior hello e cadeia de caracteres de conexão de nível de namespace Olá você salvou anteriormente.
   
  ```csharp
  static string eventHubName = "{Event Hub name}";
  static string connectionString = "{send connection string}";
  ```
6. Adicionar Olá após o método toohello **programa** classe:
   
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
   
  Esse método envia continuamente o hub de eventos de tooyour eventos com um atraso de 200 ms.
7. Finalmente, adicione Olá toohello linhas a seguir **principal** método:
   
  ```csharp
  Console.WriteLine("Press Ctrl-C toostop hello sender process");
  Console.WriteLine("Press Enter toostart now");
  Console.ReadLine();
  SendingRandomMessages();
  ```
8. Executar programa hello e certifique-se de que não existem erros.
  
Parabéns! Agora você enviou hub de eventos de tooan de mensagens.

## <a name="next-steps"></a>Próximas etapas
Agora que você construiu um aplicativo de trabalho que cria um hub de eventos e envia dados, você pode mover em toohello os seguintes cenários:

* [Receber eventos usando Olá Host de processador de eventos](event-hubs-dotnet-framework-getstarted-receive-eph.md)
* [Referência do host de processador de eventos](/dotnet/api/microsoft.servicebus.messaging.eventprocessorhost)
* [Visão Geral dos Hubs de Eventos](event-hubs-what-is-event-hubs.md)

<!-- Images. -->
[19]: ./media/event-hubs-csharp-ephcs-getstarted/create-eh-proj1.png
[20]: ./media/event-hubs-csharp-ephcs-getstarted/create-eh-proj2.png
[21]: ./media/event-hubs-csharp-ephcs-getstarted/run-csharp-ephcs1.png
[22]: ./media/event-hubs-csharp-ephcs-getstarted/run-csharp-ephcs2.png

