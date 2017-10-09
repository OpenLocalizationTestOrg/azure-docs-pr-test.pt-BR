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
# <a name="send-events-tooazure-event-hubs-using-java"></a>Enviar eventos tooAzure Hubs de eventos usando o Java

## <a name="introduction"></a>Introdução
Hubs de eventos é um sistema de inclusão altamente escalonável que pode ingestão milhões de eventos por segundo, permitindo que um aplicativo tooprocess e analisar Olá grandes quantidades de dados produzidos por seus aplicativos e dispositivos conectados. Depois de coletados em um hub de eventos, você pode transformar e armazenar dados usando qualquer provedor de análise em tempo real ou cluster de armazenamento.

Para obter mais informações, consulte Olá [visão geral de Hubs de eventos][Event Hubs overview].

Este tutorial mostra como hub de eventos de tooan toosend eventos usando um aplicativo de console em Java. eventos de tooreceive usando a biblioteca do Host de processador de eventos do Java hello, consulte [neste artigo](event-hubs-java-get-started-receive-eph.md), ou clique em idioma de recebimento apropriado Olá Olá esquerdo sumário.

Ordem toocomplete neste tutorial, você precisará Olá a seguir:

* Um ambiente de desenvolvimento Java. Para este tutorial, vamos considerar o [Eclipse](https://www.eclipse.org/).
* Uma conta ativa do Azure. <br/>Se você não tem uma conta, pode criar uma conta gratuita em apenas alguns minutos. Para obter detalhes, consulte <a href="http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fdevelop%2Fmobile%2Ftutorials%2Fget-started%2F" target="_blank">Avaliação gratuita do Azure</a>.

## <a name="send-messages-tooevent-hubs"></a>Enviar mensagens tooEvent Hubs
Olá biblioteca de cliente de Java para Hubs de eventos está disponível para uso em projetos Maven da saudação [repositório Central Maven](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22). Você pode fazer referência a essa biblioteca usando Olá declaração de dependência em seu arquivo de projeto Maven a seguir:    

```xml
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-eventhubs</artifactId>
    <version>{VERSION}</version>
</dependency>
```

Para tipos diferentes de ambientes de desenvolvimento, você pode explicitamente obter arquivos JAR do hello mais recente liberado de Olá [repositório Central Maven](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22).  

Para um publicador do evento simples, importar Olá *com.microsoft.azure.eventhubs* pacote para classes de cliente de Hubs de eventos hello e hello *com.microsoft.azure.servicebus* para classes de utilitário, do pacote como exceções comuns que são compartilhadas com o cliente de mensagens hello Azure Service Bus. 

Para Olá exemplo a seguir, primeiro crie um novo projeto Maven para um aplicativo de console para o shell no ambiente de desenvolvimento Java favorito. Nome de classe Olá `Send`.     

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

Substitua nomes de hub de namespace e evento Olá Olá valores usados ao criar hub de eventos de saudação.

```java
    final String namespaceName = "----ServiceBusNamespaceName-----";
    final String eventHubName = "----EventHubName-----";
    final String sasKeyName = "-----SharedAccessSignatureKeyName-----";
    final String sasKey = "---SharedAccessSignatureKey----";
    ConnectionStringBuilder connStr = new ConnectionStringBuilder(namespaceName, eventHubName, sasKeyName, sasKey);
```

Em seguida, crie um evento singular transformando uma cadeia de caracteres em sua codificação de bytes UTF-8. Em seguida, criar uma nova instância de cliente de Hubs de eventos de cadeia de caracteres de conexão hello e enviar mensagem de saudação.   

```java 

    byte[] payloadBytes = "Test AMQP message from JMS".getBytes("UTF-8");
    EventData sendEvent = new EventData(payloadBytes);

    EventHubClient ehClient = EventHubClient.createFromConnectionStringSync(connStr.toString());
    ehClient.sendSync(sendEvent);
    }
}

``` 

## <a name="next-steps"></a>Próximas etapas
Você pode aprender mais sobre os Hubs de eventos visitando Olá links a seguir:

* [Receber eventos usando Olá EventProcessorHost](event-hubs-java-get-started-receive-eph.md)
* [Visão Geral dos Hubs de Eventos][Event Hubs overview]
* [Criar um hub de eventos](event-hubs-create.md)
* [Perguntas frequentes sobre os Hubs de Eventos](event-hubs-faq.md)

<!-- Links -->
[Event Hubs overview]: event-hubs-overview.md