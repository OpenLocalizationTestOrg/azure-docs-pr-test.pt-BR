---
title: "filas de aaaHow toouse barramento de serviço do Azure com Java | Microsoft Docs"
description: "Saiba como filas de toouse barramento de serviço no Azure. Exemplos de códigos escritos em Java."
services: service-bus-messaging
documentationcenter: java
author: sethmanheim
manager: timlt
ms.assetid: f701439c-553e-402c-94a7-64400f997d59
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: f68e941438134090c5eee53459e7667bda13ff3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-queues-with-java"></a>Como toouse Service Bus filas com Java
[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

Este artigo descreve como as filas do barramento de serviço toouse. exemplos de saudação são escritos em Java e usam Olá [SDK do Azure para Java][Azure SDK for Java]. Olá cenários abordados incluem **Criando filas**, **enviando e recebendo mensagens**, e **excluindo filas**.

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="configure-your-application-toouse-service-bus"></a>Configurar seu toouse barramento de serviço do aplicativo
Verifique se você instalou Olá [SDK do Azure para Java] [ Azure SDK for Java] antes de compilar este exemplo. Se você estiver usando o Eclipse, você pode instalar Olá [Kit de ferramentas do Azure para Eclipse] [ Azure Toolkit for Eclipse] que inclui Olá SDK do Azure para Java. Você pode adicionar Olá **bibliotecas do Microsoft Azure para Java** tooyour projeto:

![](./media/service-bus-java-how-to-use-queues/eclipselibs.png)

Adicione o seguinte Olá `import` superior de toohello instruções saudação do arquivo de Java:

```java
// Include hello following imports toouse Service Bus APIs
import com.microsoft.windowsazure.services.servicebus.*;
import com.microsoft.windowsazure.services.servicebus.models.*;
import com.microsoft.windowsazure.core.*;
import javax.xml.datatype.*;
```

## <a name="create-a-queue"></a>Criar uma fila
Operações de gerenciamento para as filas do Barramento de Serviço podem ser realizadas pela classe **ServiceBusContract**. Um **ServiceBusContract** objeto for construído com uma configuração apropriada que encapsula o token SAS com toomanage de permissões e hello **ServiceBusContract** classe é um ponto único de saudação de comunicação com o Azure.

Olá **ServiceBusService** classe fornece métodos toocreate, enumerar e excluir filas. Olá como o exemplo a seguir mostra um **ServiceBusService** objeto pode ser usado toocreate uma fila denominada `TestQueue`, com um namespace chamado `HowToSample`:

```java
Configuration config =
    ServiceBusConfiguration.configureWithSASAuthentication(
            "HowToSample",
            "RootManageSharedAccessKey",
            "SAS_key_value",
            ".servicebus.windows.net"
            );

ServiceBusContract service = ServiceBusService.create(config);
QueueInfo queueInfo = new QueueInfo("TestQueue");
try
{
    CreateQueueResult result = service.createQueue(queueInfo);
}
catch (ServiceException e)
{
    System.out.print("ServiceException encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
```

Há métodos no `QueueInfo` que permitem que propriedades de saudação fila toobe ajustadas (por exemplo: tooset saudação padrão time-to-live (TTL) valor toobe aplicada toomessages enviados toohello fila). Olá exemplo a seguir mostra como toocreate uma fila denominada `TestQueue` com um tamanho máximo de 5 GB:

````java
long maxSizeInMegabytes = 5120;
QueueInfo queueInfo = new QueueInfo("TestQueue");
queueInfo.setMaxSizeInMegabytes(maxSizeInMegabytes);
CreateQueueResult result = service.createQueue(queueInfo);
````

Observe que você pode usar o hello `listQueues` método **ServiceBusContract** objetos toocheck se já existe uma fila com um nome especificado em um namespace de serviço.

## <a name="send-messages-tooa-queue"></a>Mensagens tooa fila de envio
toosend uma fila de barramento de serviço tooa mensagens, o aplicativo obtém um **ServiceBusContract** objeto. Olá mostrado no código a seguir como toosend uma mensagem de saudação `TestQueue` fila criada anteriormente no hello `HowToSample` namespace:

```java
try
{
    BrokeredMessage message = new BrokeredMessage("MyMessage");
    service.sendQueueMessage("TestQueue", message);
}
catch (ServiceException e)
{
    System.out.print("ServiceException encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
```

As mensagens enviadas para e recebidas do barramento de serviço filas são instâncias da saudação [BrokeredMessage] [ BrokeredMessage] classe. [BrokeredMessage] [ BrokeredMessage] objetos têm um conjunto de propriedades padrão (como [rótulo](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.label#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label) e [TimeToLive](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.timetolive#Microsoft_ServiceBus_Messaging_BrokeredMessage_TimeToLive)), um dicionário que é usado toohold personalizado propriedades específicas do aplicativo e um corpo de dados arbitrários do aplicativo. Um aplicativo pode definir o corpo de saudação da mensagem de saudação passando qualquer objeto serializável para construtor de saudação do hello [BrokeredMessage][BrokeredMessage], e o serializador adequado Olá será usado objeto de saudação tooserialize. Como alternativa, você pode fornecer um objeto **java.IO.InputStream**.

Olá exemplo a seguir demonstra como teste toosend cinco mensagens toothe `TestQueue` **MessageSender** obtivemos no trecho de código anterior hello:

```java
for (int i=0; i<5; i++)
{
     // Create message, passing a string message for hello body.
     BrokeredMessage message = new BrokeredMessage("Test message " + i);
     // Set an additional app-specific property.
     message.setProperty("MyProperty", i);
     // Send message toohello queue
     service.sendQueueMessage("TestQueue", message);
}
```

Filas do barramento de serviço de suportam a um tamanho máximo de 256 KB em Olá [camada padrão](service-bus-premium-messaging.md) e 1 MB de saudação [camada Premium](service-bus-premium-messaging.md). cabeçalho de saudação, que inclui o padrão de saudação e propriedades de aplicativo personalizado, pode ter um tamanho máximo de 64 KB. Não há nenhum limite no número de saudação da mantidas em uma fila de mensagens, mas há um limite no tamanho total de saudação da mantidas por uma fila de mensagens de saudação. O tamanho da fila é definido no momento da criação, com um limite superior de 5 GB.

## <a name="receive-messages-from-a-queue"></a>Receber mensagens de uma fila
mensagens de tooreceive Olá principal forma de uma fila é toouse uma **ServiceBusContract** objeto. As mensagens recebidas podem funcionar em dois modos diferentes: **ReceiveAndDelete** e **PeekLock**.

Ao usar o hello **ReceiveAndDelete** modo, recebe é uma operação de captura único - ou seja, quando o barramento de serviço recebe uma solicitação de leitura para uma mensagem em uma fila, ele marca a mensagem de saudação como sendo consumida e retorna-toohello aplicativo. **ReceiveAndDelete** modo (que é o modo padrão de saudação) é o modelo mais simples de saudação e funciona melhor nos cenários em que um aplicativo pode tolerar não processar uma mensagem em caso de saudação de uma falha. toounderstand isso, considere um cenário em que problemas do consumidor Olá Olá receber a solicitação e falha antes de processá-lo.
Porque o barramento de serviço será marcou a mensagem de saudação como sendo consumida, em seguida, quando o aplicativo hello reinicia e começa a consumir mensagens novamente, ele terá perdido mensagem de saudação foi consumido falha toohello anterior.

Em **PeekLock** , modo de recebimento torna-se uma operação de dois estágios, o que torna possível toosupport aplicativos que não podem tolerar mensagens ausentes. Quando o barramento de serviço recebe uma solicitação, ele localiza Olá próxima mensagem toobe consumida, boqueia-tooprevent outros consumidores a recebam e retorna toohello aplicativo. Depois que o aplicativo hello termina de processar a mensagem de saudação (ou armazena com segurança para processamento futuro), ele conclui Olá segunda etapa de saudação processo de recebimento chamando **excluir** na mensagem recebida. Quando o Service Bus vê Olá **excluir** chamada, ele marca a mensagem de saudação como sendo consumida e removê-lo da fila de saudação.

Olá exemplo a seguir demonstra como as mensagens podem ser recebidas e processados usando **PeekLock** modo (não o modo padrão de saudação). Olá exemplo a seguir faz um loop infinito e processa as mensagens que chegam em nosso `TestQueue`:

```java
try
{
    ReceiveMessageOptions opts = ReceiveMessageOptions.DEFAULT;
    opts.setReceiveMode(ReceiveMode.PEEK_LOCK);

    while(true)  {
         ReceiveQueueMessageResult resultQM =
                 service.receiveQueueMessage("TestQueue", opts);
        BrokeredMessage message = resultQM.getValue();
        if (message != null && message.getMessageId() != null)
        {
            System.out.println("MessageID: " + message.getMessageId());
            // Display hello queue message.
            System.out.print("From queue: ");
            byte[] b = new byte[200];
            String s = null;
            int numRead = message.getBody().read(b);
            while (-1 != numRead)
            {
                s = new String(b);
                s = s.trim();
                System.out.print(s);
                numRead = message.getBody().read(b);
            }
            System.out.println();
            System.out.println("Custom Property: " +
                message.getProperty("MyProperty"));
            // Remove message from queue.
            System.out.println("Deleting this message.");
            //service.deleteMessage(message);
        }  
        else  
        {
            System.out.println("Finishing up - no more messages.");
            break;
            // Added toohandle no more messages.
            // Could instead wait for more messages toobe added.
        }
    }
}
catch (ServiceException e) {
    System.out.print("ServiceException encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
catch (Exception e) {
    System.out.print("Generic exception encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a>Como o aplicativo de toohandle falha e mensagens ilegíveis
Barramento de serviço fornece funcionalidade toohelp que normalmente recuperar de erros no seu aplicativo ou dificuldade para processar uma mensagem. Se um aplicativo receptor não puder tooprocess Olá mensagem por algum motivo, em seguida, pode chamar hello **unlockMessage** método na mensagem recebida (em vez da saudação **deleteMessage** método). Isso faz com que hello de toounlock de barramento de serviço de mensagens na fila de saudação e torná-lo disponível toobe recebida novamente, ou por Olá mesmo aplicativo ou por outro aplicativo de consumo de consumo.

Também há um tempo limite associado a uma mensagem bloqueada na fila, e se o aplicativo hello falha tooprocess Olá mensagem antes do tempo limite de bloqueio expira (por exemplo, se o aplicativo hello falhar), em seguida, o barramento de serviço desbloqueia a mensagem de saudação automaticamente e torna disponível toobe recebida novamente.

Em Olá evento Olá aplicativo falha após o processamento de mensagem de saudação, mas antes de saudação **deleteMessage** solicitação é emitida, mensagem de saudação será entregue novamente toohello aplicativo quando ele for reiniciado. Isso é geralmente chamado *, pelo menos, após processamento*; ou seja, cada mensagem é processada pelo menos uma vez, mas em certo Olá situações mesma mensagem pode ser entregue novamente. Se o cenário de saudação não puder tolerar o processamento duplicado, os desenvolvedores de aplicativos devem adicionar entrega de mensagens duplicadas lógica adicional tootheir aplicativos toohandle. Isso geralmente é obtido usando Olá **getMessageId** método de mensagem de saudação, que permanece constante entre tentativas de entrega.

## <a name="next-steps"></a>Próximas etapas
Agora que você aprendeu as Noções básicas de saudação de filas do barramento de serviço, consulte [filas, tópicos e assinaturas] [ Queues, topics, and subscriptions] para obter mais informações.

Para obter mais informações, consulte Olá [Central de desenvolvedores de Java](https://azure.microsoft.com/develop/java/).

[Azure SDK for Java]: http://azure.microsoft.com/develop/java/
[Azure Toolkit for Eclipse]: https://msdn.microsoft.com/library/azure/hh694271.aspx
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage
