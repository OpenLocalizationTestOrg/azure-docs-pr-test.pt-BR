---
title: aaaSend eventos tooAzure Hubs de eventos usando o Java | Microsoft Docs
description: "Começar a enviar Hubs tooEvent utilizado Java"
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.workload: core
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: ec537b8849a0cb49855e76c0c0ef4093108fe83c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="send-events-tooazure-event-hubs-using-java"></a><span data-ttu-id="a5a42-103">Enviar eventos tooAzure Hubs de eventos usando o Java</span><span class="sxs-lookup"><span data-stu-id="a5a42-103">Send events tooAzure Event Hubs using Java</span></span>

## <a name="introduction"></a><span data-ttu-id="a5a42-104">Introdução</span><span class="sxs-lookup"><span data-stu-id="a5a42-104">Introduction</span></span>
<span data-ttu-id="a5a42-105">Hubs de eventos é um sistema de inclusão altamente escalonável que pode ingestão milhões de eventos por segundo, permitindo que um aplicativo tooprocess e analisar Olá grandes quantidades de dados produzidos por seus aplicativos e dispositivos conectados.</span><span class="sxs-lookup"><span data-stu-id="a5a42-105">Event Hubs is a highly scalable ingestion system that can ingest millions of events per second, enabling an application tooprocess and analyze hello massive amounts of data produced by your connected devices and applications.</span></span> <span data-ttu-id="a5a42-106">Depois de coletados em um hub de eventos, você pode transformar e armazenar dados usando qualquer provedor de análise em tempo real ou cluster de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="a5a42-106">Once collected into an event hub, you can transform and store data using any real-time analytics provider or storage cluster.</span></span>

<span data-ttu-id="a5a42-107">Para obter mais informações, consulte Olá [visão geral de Hubs de eventos][Event Hubs overview].</span><span class="sxs-lookup"><span data-stu-id="a5a42-107">For more information, see hello [Event Hubs overview][Event Hubs overview].</span></span>

<span data-ttu-id="a5a42-108">Este tutorial mostra como hub de eventos de tooan toosend eventos usando um aplicativo de console em Java.</span><span class="sxs-lookup"><span data-stu-id="a5a42-108">This tutorial shows how toosend events tooan event hub by using a console application in Java.</span></span> <span data-ttu-id="a5a42-109">eventos de tooreceive usando a biblioteca do Host de processador de eventos do Java hello, consulte [neste artigo](event-hubs-java-get-started-receive-eph.md), ou clique em idioma de recebimento apropriado Olá Olá esquerdo sumário.</span><span class="sxs-lookup"><span data-stu-id="a5a42-109">tooreceive events using hello Java Event Processor Host library, see [this article](event-hubs-java-get-started-receive-eph.md), or click hello appropriate receiving language in hello left-hand table of contents.</span></span>

<span data-ttu-id="a5a42-110">Ordem toocomplete neste tutorial, você precisará Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="a5a42-110">In order toocomplete this tutorial, you will need hello following:</span></span>

* <span data-ttu-id="a5a42-111">Um ambiente de desenvolvimento Java.</span><span class="sxs-lookup"><span data-stu-id="a5a42-111">A Java development environment.</span></span> <span data-ttu-id="a5a42-112">Para este tutorial, vamos considerar o [Eclipse](https://www.eclipse.org/).</span><span class="sxs-lookup"><span data-stu-id="a5a42-112">For this tutorial, we assume [Eclipse](https://www.eclipse.org/).</span></span>
* <span data-ttu-id="a5a42-113">Uma conta ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="a5a42-113">An active Azure account.</span></span> <br/><span data-ttu-id="a5a42-114">Se você não tem uma conta, pode criar uma conta gratuita em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="a5a42-114">If you don't have an account, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="a5a42-115">Para obter detalhes, consulte <a href="http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fdevelop%2Fmobile%2Ftutorials%2Fget-started%2F" target="_blank">Avaliação gratuita do Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="a5a42-115">For details, see <a href="http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fdevelop%2Fmobile%2Ftutorials%2Fget-started%2F" target="_blank">Azure Free Trial</a>.</span></span>

## <a name="send-messages-tooevent-hubs"></a><span data-ttu-id="a5a42-116">Enviar mensagens tooEvent Hubs</span><span class="sxs-lookup"><span data-stu-id="a5a42-116">Send messages tooEvent Hubs</span></span>
<span data-ttu-id="a5a42-117">Olá biblioteca de cliente de Java para Hubs de eventos está disponível para uso em projetos Maven da saudação [repositório Central Maven](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22).</span><span class="sxs-lookup"><span data-stu-id="a5a42-117">hello Java client library for Event Hubs is available for use in Maven projects from hello [Maven Central Repository](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22).</span></span> <span data-ttu-id="a5a42-118">Você pode fazer referência a essa biblioteca usando Olá declaração de dependência em seu arquivo de projeto Maven a seguir:</span><span class="sxs-lookup"><span data-stu-id="a5a42-118">You can reference this library using hello following dependency declaration inside your Maven project file:</span></span>    

```xml
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-eventhubs</artifactId>
    <version>{VERSION}</version>
</dependency>
```

<span data-ttu-id="a5a42-119">Para tipos diferentes de ambientes de desenvolvimento, você pode explicitamente obter arquivos JAR do hello mais recente liberado de Olá [repositório Central Maven](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22).</span><span class="sxs-lookup"><span data-stu-id="a5a42-119">For different types of build environments, you can explicitly obtain hello latest released JAR files from hello [Maven Central Repository](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22).</span></span>  

<span data-ttu-id="a5a42-120">Para um publicador do evento simples, importar Olá *com.microsoft.azure.eventhubs* pacote para classes de cliente de Hubs de eventos hello e hello *com.microsoft.azure.servicebus* para classes de utilitário, do pacote como exceções comuns que são compartilhadas com o cliente de mensagens hello Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="a5a42-120">For a simple event publisher, import hello *com.microsoft.azure.eventhubs* package for hello Event Hubs client classes and hello *com.microsoft.azure.servicebus* package for utility classes such as common exceptions that are shared with hello Azure Service Bus messaging client.</span></span> 

<span data-ttu-id="a5a42-121">Para Olá exemplo a seguir, primeiro crie um novo projeto Maven para um aplicativo de console para o shell no ambiente de desenvolvimento Java favorito.</span><span class="sxs-lookup"><span data-stu-id="a5a42-121">For hello following sample, first create a new Maven project for a console/shell application in your favorite Java development environment.</span></span> <span data-ttu-id="a5a42-122">Nome de classe Olá `Send`.</span><span class="sxs-lookup"><span data-stu-id="a5a42-122">Name hello class `Send`.</span></span>     

```java
import java.io.IOException;
import java.nio.charset.*;
import java.util.*;
import java.util.concurrent.ExecutionException;

import com.microsoft.azure.eventhubs.*;
import com.microsoft.azure.servicebus.*;

public class Send
{
    public static void main(String[] args) 
            throws ServiceBusException, ExecutionException, InterruptedException, IOException
    {
```

<span data-ttu-id="a5a42-123">Substitua nomes de hub de namespace e evento Olá Olá valores usados ao criar hub de eventos de saudação.</span><span class="sxs-lookup"><span data-stu-id="a5a42-123">Replace hello namespace and event hub names with hello values used when you created hello event hub.</span></span>

```java
    final String namespaceName = "----ServiceBusNamespaceName-----";
    final String eventHubName = "----EventHubName-----";
    final String sasKeyName = "-----SharedAccessSignatureKeyName-----";
    final String sasKey = "---SharedAccessSignatureKey----";
    ConnectionStringBuilder connStr = new ConnectionStringBuilder(namespaceName, eventHubName, sasKeyName, sasKey);
```

<span data-ttu-id="a5a42-124">Em seguida, crie um evento singular transformando uma cadeia de caracteres em sua codificação de bytes UTF-8.</span><span class="sxs-lookup"><span data-stu-id="a5a42-124">Then, create a singular event by transforming a string into its UTF-8 byte encoding.</span></span> <span data-ttu-id="a5a42-125">Em seguida, criar uma nova instância de cliente de Hubs de eventos de cadeia de caracteres de conexão hello e enviar mensagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="a5a42-125">Then, create a new Event Hubs client instance from hello connection string and send hello message.</span></span>   

```java 

    byte[] payloadBytes = "Test AMQP message from JMS".getBytes("UTF-8");
    EventData sendEvent = new EventData(payloadBytes);

    EventHubClient ehClient = EventHubClient.createFromConnectionStringSync(connStr.toString());
    ehClient.sendSync(sendEvent);
    }
}

``` 

## <a name="next-steps"></a><span data-ttu-id="a5a42-126">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a5a42-126">Next steps</span></span>
<span data-ttu-id="a5a42-127">Você pode aprender mais sobre os Hubs de eventos visitando Olá links a seguir:</span><span class="sxs-lookup"><span data-stu-id="a5a42-127">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="a5a42-128">Receber eventos usando Olá EventProcessorHost</span><span class="sxs-lookup"><span data-stu-id="a5a42-128">Receive events using hello EventProcessorHost</span></span>](event-hubs-java-get-started-receive-eph.md)
* <span data-ttu-id="a5a42-129">[Visão Geral dos Hubs de Eventos][Event Hubs overview]</span><span class="sxs-lookup"><span data-stu-id="a5a42-129">[Event Hubs overview][Event Hubs overview]</span></span>
* [<span data-ttu-id="a5a42-130">Criar um hub de eventos</span><span class="sxs-lookup"><span data-stu-id="a5a42-130">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="a5a42-131">Perguntas frequentes sobre os Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="a5a42-131">Event Hubs FAQ</span></span>](event-hubs-faq.md)

<!-- Links -->
[Event Hubs overview]: event-hubs-overview.md