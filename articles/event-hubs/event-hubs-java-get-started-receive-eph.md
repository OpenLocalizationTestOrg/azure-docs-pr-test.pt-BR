---
title: eventos de aaaReceive de Hubs de eventos do Azure usando o Java | Microsoft Docs
description: Comece a receber de Hubs de Eventos usando Java
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 38e3be53-251c-488f-a856-9a500f41b6ca
ms.service: event-hubs
ms.workload: core
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: 05414a22e6616296752c678bb0af887d6f070c12
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="receive-events-from-azure-event-hubs-using-java"></a>Receber eventos de Hubs de Eventos do Azure usando Java


## <a name="introduction"></a>Introdução
Hubs de eventos é um sistema de inclusão altamente escalonável que pode ingestão milhões de eventos por segundo, permitindo que um aplicativo tooprocess e analisar Olá grandes quantidades de dados produzidos por seus aplicativos e dispositivos conectados. Depois de coletados em Hubs de Evento, você pode transformar e armazenar dados usando qualquer provedor de análise em tempo real ou cluster de armazenamento.

Para obter mais informações, consulte Olá [visão geral de Hubs de eventos][Event Hubs overview].

Este tutorial mostra como tooreceive eventos em um hub de eventos usando um aplicativo de console escrito em Java.

## <a name="prerequisites"></a>Pré-requisitos

Em ordem toocomplete neste tutorial, você precisa Olá pré-requisitos a seguir:

* Um ambiente de desenvolvimento Java. Para este tutorial, vamos considerar o [Eclipse](https://www.eclipse.org/).
* Uma conta ativa do Azure. <br/>Se você não tem uma conta, pode criar uma conta gratuita em apenas alguns minutos. Para obter detalhes, consulte <a href="http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fdevelop%2Fmobile%2Ftutorials%2Fget-started%2F" target="_blank">Avaliação gratuita do Azure</a>.

## <a name="receive-messages-with-eventprocessorhost-in-java"></a>Receber mensagens com EventProcessorHost em Java

**EventProcessorHost** é uma classe Java que simplifica o recebimento de eventos dos Hubs de Eventos gerenciando pontos de verificação persistentes e recebimentos paralelos desses Hubs de Eventos. Usando o EventProcessorHost, você pode dividir eventos entre vários destinatários, mesmo quando hospedados em nós diferentes. Este exemplo mostra como toouse EventProcessorHost para um único destinatário.

### <a name="create-a-storage-account"></a>Criar uma conta de armazenamento
toouse EventProcessorHost, você deve ter uma [conta de armazenamento do Azure][Azure Storage account]:

1. Faça logon no toohello [portal do Azure][Azure portal]e clique em **+ novo** no lado esquerdo de saudação da tela hello.
2. Clique em **Armazenamento** e em **conta de Armazenamento**. Em Olá **criar conta de armazenamento** folha, digite um nome para a conta de armazenamento hello. Conclua o restante da saudação de campos hello, selecione a região desejada e, em seguida, clique em **criar**.
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage2.png)

3. Clique na conta de armazenamento Olá recém-criada e, em seguida, clique em **gerenciar chaves de acesso**:
   
    ![](./media/event-hubs-dotnet-framework-getstarted-receive-eph/create-storage3.png)

    Copiar Olá acesso primário tooa chave temporária local toouse posteriormente neste tutorial.

### <a name="create-a-java-project-using-hello-eventprocessor-host"></a>Criar um projeto de Java usando Olá EventProcessor Host
Olá biblioteca de cliente de Java para Hubs de eventos está disponível para uso em projetos Maven da saudação [repositório Central Maven][Maven Package]e podem ser referenciadas usando Olá após a declaração de dependência dentro de sua Arquivo de projeto Maven:    

```xml
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-eventhubs</artifactId>
    <version>{VERSION}</version>
</dependency>
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-eventhubs-eph</artifactId>
    <version>{VERSION}</version>
</dependency>
<dependency>
  <groupId>com.microsoft.azure</groupId>
  <artifactId>azure-eventhubs-eph</artifactId>
  <version>0.14.0</version>
</dependency>
```

Para tipos diferentes de ambientes de desenvolvimento, você pode obter explicitamente arquivos JAR do hello mais recente liberado de saudação [repositório Central Maven] [ Maven Package] ou de [Olá ponto de distribuição de versão em GitHub](https://github.com/Azure/azure-event-hubs/releases).  

1. Para Olá exemplo a seguir, primeiro crie um novo projeto Maven para um aplicativo de console para o shell no ambiente de desenvolvimento Java favorito. classe de saudação é chamada `ErrorNotificationHandler`.     
   
    ```java
    import java.util.function.Consumer;
    import com.microsoft.azure.eventprocessorhost.ExceptionReceivedEventArgs;
   
    public class ErrorNotificationHandler implements Consumer<ExceptionReceivedEventArgs>
    {
        @Override
        public void accept(ExceptionReceivedEventArgs t)
        {
            System.out.println("SAMPLE: Host " + t.getHostname() + " received general error notification during " + t.getAction() + ": " + t.getException().toString());
        }
    }
    ```
2. Toocreate uma nova classe chamada de código a seguir de saudação do uso `EventProcessor`.
   
    ```java
    import com.microsoft.azure.eventhubs.EventData;
    import com.microsoft.azure.eventprocessorhost.CloseReason;
    import com.microsoft.azure.eventprocessorhost.IEventProcessor;
    import com.microsoft.azure.eventprocessorhost.PartitionContext;
   
    public class EventProcessor implements IEventProcessor
    {
        private int checkpointBatchingCount = 0;
   
        @Override
        public void onOpen(PartitionContext context) throws Exception
        {
            System.out.println("SAMPLE: Partition " + context.getPartitionId() + " is opening");
        }
   
        @Override
        public void onClose(PartitionContext context, CloseReason reason) throws Exception
        {
            System.out.println("SAMPLE: Partition " + context.getPartitionId() + " is closing for reason " + reason.toString());
        }
   
        @Override
        public void onError(PartitionContext context, Throwable error)
        {
            System.out.println("SAMPLE: Partition " + context.getPartitionId() + " onError: " + error.toString());
        }
   
        @Override
        public void onEvents(PartitionContext context, Iterable<EventData> messages) throws Exception
        {
            System.out.println("SAMPLE: Partition " + context.getPartitionId() + " got message batch");
            int messageCount = 0;
            for (EventData data : messages)
            {
                System.out.println("SAMPLE (" + context.getPartitionId() + "," + data.getSystemProperties().getOffset() + "," +
                        data.getSystemProperties().getSequenceNumber() + "): " + new String(data.getBody(), "UTF8"));
                messageCount++;
   
                this.checkpointBatchingCount++;
                if ((checkpointBatchingCount % 5) == 0)
                {
                    System.out.println("SAMPLE: Partition " + context.getPartitionId() + " checkpointing at " +
                        data.getSystemProperties().getOffset() + "," + data.getSystemProperties().getSequenceNumber());
                    context.checkpoint(data);
                }
            }
            System.out.println("SAMPLE: Partition " + context.getPartitionId() + " batch size was " + messageCount + " for host " + context.getOwner());
        }
    }
    ```
3. Criar uma classe mais chamada `EventProcessorSample`usando Olá código a seguir.
   
    ```java
    import com.microsoft.azure.eventprocessorhost.*;
    import com.microsoft.azure.servicebus.ConnectionStringBuilder;
    import com.microsoft.azure.eventhubs.EventData;
   
    public class EventProcessorSample
    {
        public static void main(String args[])
        {
            final String consumerGroupName = "$Default";
            final String namespaceName = "----ServiceBusNamespaceName-----";
            final String eventHubName = "----EventHubName-----";
            final String sasKeyName = "-----SharedAccessSignatureKeyName-----";
            final String sasKey = "---SharedAccessSignatureKey----";
   
            final String storageAccountName = "---StorageAccountName----";
            final String storageAccountKey = "---StorageAccountKey----";
            final String storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=" + storageAccountName + ";AccountKey=" + storageAccountKey;
   
            ConnectionStringBuilder eventHubConnectionString = new ConnectionStringBuilder(namespaceName, eventHubName, sasKeyName, sasKey);
   
            EventProcessorHost host = new EventProcessorHost(eventHubName, consumerGroupName, eventHubConnectionString.toString(), storageConnectionString);
   
            System.out.println("Registering host named " + host.getHostName());
            EventProcessorOptions options = new EventProcessorOptions();
            options.setExceptionNotification(new ErrorNotificationHandler());
            try
            {
                host.registerEventProcessor(EventProcessor.class, options).get();
            }
            catch (Exception e)
            {
                System.out.print("Failure while registering: ");
                if (e instanceof ExecutionException)
                {
                    Throwable inner = e.getCause();
                    System.out.println(inner.toString());
                }
                else
                {
                    System.out.println(e.toString());
                }
            }
   
            System.out.println("Press enter toostop");
            try
            {
                System.in.read();
                host.unregisterEventProcessor();
   
                System.out.println("Calling forceExecutorShutdown");
                EventProcessorHost.forceExecutorShutdown(120);
            }
            catch(Exception e)
            {
                System.out.println(e.toString());
                e.printStackTrace();
            }
   
            System.out.println("End of sample");
        }
    }
    ```
4. Substitua saudação campos a seguir com valores hello usou quando criou a conta de armazenamento e hub de eventos de saudação.
   
    ```java
    final String namespaceName = "----ServiceBusNamespaceName-----";
    final String eventHubName = "----EventHubName-----";
   
    final String sasKeyName = "-----SharedAccessSignatureKeyName-----";
    final String sasKey = "---SharedAccessSignatureKey----";
   
    final String storageAccountName = "---StorageAccountName----"
    final String storageAccountKey = "---StorageAccountKey----";
    ```

> [!NOTE]
> Este tutorial usa uma única instância do EventProcessorHost. taxa de transferência tooincrease, é recomendável que você executar várias instâncias do EventProcessorHost, preferencialmente em computadores separados.  Isso também fornece redundância. Nesses casos, Olá automaticamente coordenada uns com os outros eventos de saudação recebida ordem tooload saldo de várias instâncias. Se você quiser que o processo de tooeach vários destinatários *todos os* Olá eventos, você deve usar o hello **o ConsumerGroup** conceito. Ao receber eventos em máquinas diferentes, pode ser útil toospecify nomes para instâncias de EventProcessorHost com base em máquinas hello (ou funções) no qual eles foram implantados.
> 
> 

## <a name="next-steps"></a>Próximas etapas
Você pode aprender mais sobre os Hubs de eventos visitando Olá links a seguir:

* [Visão Geral dos Hubs de Eventos](event-hubs-what-is-event-hubs.md)
* [Criar um Hub de Eventos](event-hubs-create.md)
* [Perguntas frequentes sobre os Hubs de Eventos](event-hubs-faq.md)

<!-- Links -->
[Event Hubs overview]: event-hubs-what-is-event-hubs.md
[Azure Storage account]: ../storage/common/storage-create-storage-account.md
[Azure portal]: https://portal.azure.com
[Maven Package]: https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs-eph%22

<!-- Images -->
[11]: ./media/service-bus-event-hubs-get-started-receive-ephjava/create-eph-csharp2.png
[12]: ./media/service-bus-event-hubs-get-started-receive-ephjava/create-eph-csharp3.png
