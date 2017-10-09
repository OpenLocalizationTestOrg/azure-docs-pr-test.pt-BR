---
title: "tópicos de barramento de serviço do Azure toouse aaaHow com Java | Microsoft Docs"
description: "Use tópicos e assinaturas do Barramento de Serviço no Azure."
services: service-bus-messaging
documentationcenter: java
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 63d6c8bd-8a22-4292-befc-545ffb52e8eb
ms.service: service-bus-messaging
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 06/28/2017
ms.author: sethm
ms.openlocfilehash: 1aad16fdb5d68a5782b85c8dfda9d695babd57ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-java"></a>Como toouse Service Bus tópicos e assinaturas com Java

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

Este guia descreve como toouse Service Bus tópicos e assinaturas. exemplos de saudação são escritos em Java e usam Olá [SDK do Azure para Java][Azure SDK for Java]. Olá cenários abordados incluem **criando tópicos e assinaturas**, **Criando filtros de assinatura**, **tópico tooa de mensagens de envio**, **receber mensagens de uma assinatura**, e **excluir tópicos e assinaturas**.

## <a name="what-are-service-bus-topics-and-subscriptions"></a>O que são os tópicos e as assinaturas do Barramento de Serviço?
Os tópicos e assinaturas do Barramento de Serviço dão suporte a um modelo de comunicação de mensagens de *publicação/assinatura* . Durante o uso de tópicos e assinaturas, os componentes de um aplicativo distribuído não se comunicam diretamente uns com os outros, eles trocam mensagens por meio de um tópico, que atua como um intermediário.

![Conceitos de tópico](./media/service-bus-java-how-to-use-topics-subscriptions/sb-topics-01.png)

Em contraste com as filas do Barramento de Serviço, em que cada mensagem é processada por um único consumidor, tópicos e assinaturas fornecem uma forma de comunicação de um para muitos usando um padrão de publicação/assinatura. É possível registrar o tópico de tooa várias assinaturas. Quando uma mensagem é enviada tooa tópico, ele é feito tooeach disponível assinatura toohandle/processo independentemente.

Um tópico de tooa de assinatura é semelhante a uma fila virtual que recebe cópias das mensagens de saudação enviadas toohello tópico. Opcionalmente, você pode registrar as regras de filtro para um tópico em uma base por assinatura, que permite que você toofilter/restringir o tópico de tooa quais mensagens são recebidas por quais assinaturas de tópico.

Assinaturas e tópicos do barramento de serviço permitem tooscale tooprocess um grande número de mensagens em um número muito grande de usuários e aplicativos.

## <a name="create-a-service-namespace"></a>Criar um namespace de serviço
toobegin usando assinaturas e tópicos do barramento de serviço no Azure, você deve primeiro criar um namespace, que fornece um contêiner de escopo para endereçar recursos de barramento de serviço dentro de seu aplicativo.

toocreate um namespace:

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="configure-your-application-toouse-service-bus"></a>Configurar seu toouse barramento de serviço do aplicativo
Verifique se você instalou Olá [SDK do Azure para Java] [ Azure SDK for Java] antes de compilar este exemplo. Se você estiver usando o Eclipse, você pode instalar Olá [Kit de ferramentas do Azure para Eclipse] [ Azure Toolkit for Eclipse] que inclui Olá SDK do Azure para Java. Você pode adicionar Olá **bibliotecas do Microsoft Azure para Java** tooyour projeto:

![](media/service-bus-java-how-to-use-topics-subscriptions/eclipselibs.png)

Adicione o seguinte Olá `import` superior de toohello instruções saudação do arquivo de Java:

```java
import com.microsoft.windowsazure.services.servicebus.*;
import com.microsoft.windowsazure.services.servicebus.models.*;
import com.microsoft.windowsazure.core.*;
import javax.xml.datatype.*;
```

Adicione Olá bibliotecas do Azure para Java tooyour caminho de compilação e incluí-lo em seu assembly de implantação do projeto.

## <a name="create-a-topic"></a>Criar um tópico
As operações de gerenciamento dos tópicos do Barramento de Serviço podem ser executadas pela classe **ServiceBusContract**. Um **ServiceBusContract** objeto for construído com uma configuração apropriada que encapsula o token SAS com toomanage de permissões e hello **ServiceBusContract** classe é um ponto único de saudação de comunicação com o Azure.

Olá **ServiceBusService** classe fornece métodos toocreate, enumerar e excluir tópicos. Olá mostrado no exemplo a seguir como um **ServiceBusService** objeto pode ser usado toocreate um tópico chamado `TestTopic`, com um namespace chamado `HowToSample`:

```java
Configuration config =
    ServiceBusConfiguration.configureWithSASAuthentication(
      "HowToSample",
      "RootManageSharedAccessKey",
      "SAS_key_value",
      ".servicebus.windows.net"
      );

ServiceBusContract service = ServiceBusService.create(config);
TopicInfo topicInfo = new TopicInfo("TestTopic");
try  
{
    CreateTopicResult result = service.createTopic(topicInfo);
}
catch (ServiceException e) {
    System.out.print("ServiceException encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
```

Há métodos em **TopicInfo** que permitem a propriedades de tópico Olá a ser definido (por exemplo: tooset saudação padrão time-to-live (TTL) valor toobe aplicada toomessages enviados toohello tópico). Olá exemplo a seguir mostra como toocreate um tópico chamado `TestTopic` com um tamanho máximo de 5 GB:

```java
long maxSizeInMegabytes = 5120;  
TopicInfo topicInfo = new TopicInfo("TestTopic");  
topicInfo.setMaxSizeInMegabytes(maxSizeInMegabytes);
CreateTopicResult result = service.createTopic(topicInfo);
```

Observe que você pode usar o hello **listTopics** método **ServiceBusContract** objetos toocheck se um tópico com um nome especificado já existe em um namespace de serviço.

## <a name="create-subscriptions"></a>Criar assinaturas
Assinaturas tootopics também são criados com hello **ServiceBusService** classe. As assinaturas são nomeadas e podem ter um filtro opcional que restringe o conjunto de saudação de mensagens passado a fila virtual toohello da assinatura.

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a>Criar uma assinatura com o filtro saudação padrão (MatchAll)
Olá **MatchAll** filtro é saudação padrão que será usado se nenhum filtro for especificado quando uma nova assinatura é criada. Olá quando **MatchAll** filtro é usado, o tópico de toohello publicado todas as mensagens são colocadas na fila virtual da assinatura. Olá, exemplo a seguir cria uma assinatura chamada "AllMessages" e usa Olá padrão **MatchAll** filtro.

```java
SubscriptionInfo subInfo = new SubscriptionInfo("AllMessages");
CreateSubscriptionResult result =
    service.createSubscription("TestTopic", subInfo);
```

### <a name="create-subscriptions-with-filters"></a>Criar assinaturas com os filtros
Você também pode criar filtros que permitem que você tooscope quais mensagens enviadas tópico tooa deve ser exibidas em uma assinatura de tópico específico.

Hello mais flexível o tipo de filtro de assinaturas com suporte é o [SqlFilter][SqlFilter], que implementa um subconjunto do SQL92. Filtros SQL operam nas propriedades de saudação das mensagens de saudação que são publicados toohello tópico. Para obter mais detalhes sobre expressões de saudação que podem ser usadas com um filtro SQL, examine Olá [Sqlfilter] [ SqlFilter.SqlExpression] sintaxe.

Olá, exemplo a seguir cria uma assinatura chamada `HighMessages` com um [SqlFilter] [ SqlFilter] objeto que seleciona somente as mensagens que têm um personalizado **MessageNumber** propriedade maior que 3:

```java
// Create a "HighMessages" filtered subscription  
SubscriptionInfo subInfo = new SubscriptionInfo("HighMessages");
CreateSubscriptionResult result = service.createSubscription("TestTopic", subInfo);
RuleInfo ruleInfo = new RuleInfo("myRuleGT3");
ruleInfo = ruleInfo.withSqlExpressionFilter("MessageNumber > 3");
CreateRuleResult ruleResult = service.createRule("TestTopic", "HighMessages", ruleInfo);
// Delete hello default rule, otherwise hello new rule won't be invoked.
service.deleteRule("TestTopic", "HighMessages", "$Default");
```

Da mesma forma, hello exemplo a seguir cria uma assinatura chamada `LowMessages` com um [SqlFilter] [ SqlFilter] objeto que seleciona somente as mensagens que têm um **MessageNumber** propriedade menor ou igual too3:

```java
// Create a "LowMessages" filtered subscription
SubscriptionInfo subInfo = new SubscriptionInfo("LowMessages");
CreateSubscriptionResult result = service.createSubscription("TestTopic", subInfo);
RuleInfo ruleInfo = new RuleInfo("myRuleLE3");
ruleInfo = ruleInfo.withSqlExpressionFilter("MessageNumber <= 3");
CreateRuleResult ruleResult = service.createRule("TestTopic", "LowMessages", ruleInfo);
// Delete hello default rule, otherwise hello new rule won't be invoked.
service.deleteRule("TestTopic", "LowMessages", "$Default");
```

Quando uma mensagem agora é enviada muito`TestTopic`, ela será sempre entregue tooreceivers inscrito toohello `AllMessages` assinatura e toohello tooreceivers seletivamente entregue inscrito `HighMessages` e `LowMessages` (assinaturas Dependendo do conteúdo da mensagem).

## <a name="send-messages-tooa-topic"></a>Enviar tópico tooa de mensagens
toosend um tópico de barramento de serviço do tooa de mensagem, o aplicativo obtém um **ServiceBusContract** objeto. Olá código a seguir demonstra como uma mensagem de saudação do toosend `TestTopic` tópico criado anteriormente no hello `HowToSample` namespace:

```java
BrokeredMessage message = new BrokeredMessage("MyMessage");
service.sendTopicMessage("TestTopic", message);
```

As mensagens enviadas tooService tópicos do barramento são instâncias da [BrokeredMessage] [ BrokeredMessage] classe. [BrokeredMessage][BrokeredMessage]* objetos têm um conjunto de métodos padrão (como **setLabel** e **TimeToLive**), um dicionário que é usado toohold personalizado propriedades específicas do aplicativo e um corpo de dados arbitrários do aplicativo. Um aplicativo pode definir o corpo de saudação da mensagem passando qualquer objeto serializável para construtor de saudação do [BrokeredMessage][BrokeredMessage]e hello apropriado **DataContractSerializer**  será, em seguida, o objeto de saudação do tooserialize usado. Como alternativa, um **java.io.InputStream** pode ser fornecido.

Olá exemplo a seguir demonstra como teste toosend cinco mensagens toothe `TestTopic` **MessageSender** obtivemos no trecho de código Olá acima.
Observe como Olá **MessageNumber** varia de acordo com valor de propriedade de cada mensagem na iteração de saudação do loop de saudação (isso determinará quais assinaturas recebem-lo):

```java
for (int i=0; i<5; i++)  {
// Create message, passing a string message for hello body
BrokeredMessage message = new BrokeredMessage("Test message " + i);
// Set some additional custom app-specific property
message.setProperty("MessageNumber", i);
// Send message toohello topic
service.sendTopicMessage("TestTopic", message);
}
```

Tópicos de barramento de serviço oferecem suporte a um tamanho máximo de 256 KB em hello [camada padrão](service-bus-premium-messaging.md) e 1 MB de saudação [camada Premium](service-bus-premium-messaging.md). cabeçalho de saudação, que inclui o padrão de saudação e propriedades de aplicativo personalizado, pode ter um tamanho máximo de 64 KB. Não há nenhum limite no número de saudação de mensagens mantido em um tópico, mas há um limite no tamanho total de saudação de mensagens de saudação mantidos por um tópico. O tamanho do tópico é definido no momento da criação, com um limite máximo de 5 GB.

## <a name="how-tooreceive-messages-from-a-subscription"></a>Como tooreceive mensagens de uma assinatura
tooreceive mensagens de uma assinatura, use um **ServiceBusContract** objeto. As mensagens recebidas podem funcionar em dois modos diferentes: **ReceiveAndDelete** e **PeekLock**.

Ao usar o hello **ReceiveAndDelete** modo, recebe é uma operação de captura único - ou seja, quando o barramento de serviço recebe uma solicitação de leitura para uma mensagem, ele marca a mensagem de saudação como sendo consumida e retorna-toothe aplicativo. **ReceiveAndDelete** modo é o modelo mais simples de saudação e funciona melhor nos cenários em que um aplicativo pode tolerar não processando uma mensagem em caso de saudação de falha. toounderstand isso, considere um cenário em que problemas do consumidor Olá Olá receber a solicitação e falha antes de processá-lo. Porque o barramento de serviço será marcou a mensagem como sendo consumida, em seguida, quando o aplicativo hello reinicia e começa a consumir mensagens novamente, ele terá perdido mensagem de saudação foi consumido falha toohello anterior.

Em **PeekLock** , modo de recebimento torna-se uma operação de dois estágios, o que torna possível toosupport aplicativos que não podem tolerar mensagens ausentes. Quando o barramento de serviço recebe uma solicitação, ele localiza Olá próxima mensagem toobe consumida, boqueia-tooprevent outros consumidores a recebam e retorna toohello aplicativo. Depois que o aplicativo hello termina de processar a mensagem de saudação (ou armazena com segurança para processamento futuro), ele conclui Olá segunda etapa de saudação processo de recebimento chamando **excluir** na mensagem recebida. Quando o Service Bus vê Olá **excluir** chamada, ele marca a mensagem de saudação como sendo consumida e removê-lo do tópico hello.

Olá exemplo abaixo demonstra como as mensagens podem ser recebidas e processados usando **PeekLock** modo (não o modo padrão de saudação). Hello exemplo a seguir executa um loop e processa mensagens de saudação assinatura "HighMessages" e, em seguida, é encerrado quando não existem mais mensagens (como alternativa, ele pode ser definido toowait novas mensagens).

```java
try
{
    ReceiveMessageOptions opts = ReceiveMessageOptions.DEFAULT;
    opts.setReceiveMode(ReceiveMode.PEEK_LOCK);

    while(true)  {
        ReceiveSubscriptionMessageResult  resultSubMsg =
            service.receiveSubscriptionMessage("TestTopic", "HighMessages", opts);
        BrokeredMessage message = resultSubMsg.getValue();
        if (message != null && message.getMessageId() != null)
        {
            System.out.println("MessageID: " + message.getMessageId());
            // Display hello topic message.
            System.out.print("From topic: ");
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
                message.getProperty("MessageNumber"));
            // Delete message.
            System.out.println("Deleting this message.");
            service.deleteMessage(message);
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
Barramento de serviço fornece funcionalidade toohelp que normalmente recuperar de erros no seu aplicativo ou dificuldade para processar uma mensagem. Se um aplicativo receptor não puder tooprocess Olá mensagem por algum motivo, em seguida, pode chamar hello **unlockMessage** método na mensagem recebida (em vez da saudação **deleteMessage** método). Isso causar a mensagem de saudação do barramento de serviço toounlock tópico hello e torná-lo disponível toobe recebida novamente, o hello pelo mesmo aplicativo ou por outro aplicativo de consumo de consumo.

Também há um tempo limite associado a uma mensagem bloqueada dentro do tópico, e se o aplicativo hello falhar tooprocess mensagem de saudação antes do tempo limite de bloqueio expira (por exemplo, se o aplicativo hello falhar), e o barramento de serviço desbloquear mensagem de saudação automaticamente e torná-lo disponível toobe recebida novamente.

Em Olá evento Olá aplicativo falha após o processamento de mensagem de saudação, mas antes de saudação **deleteMessage** solicitação é emitida, mensagem de saudação será entregue novamente toohello aplicativo quando ele for reiniciado. Isso é geralmente chamado **, pelo menos, após processamento**, ou seja, cada mensagem será processada pelo menos uma vez, mas em certo Olá situações mesma mensagem pode ser entregue novamente. Se o cenário de saudação não puder tolerar o processamento duplicado, os desenvolvedores de aplicativos devem adicionar entrega de mensagens duplicadas lógica adicional tootheir aplicativos toohandle. Isso geralmente é obtido usando Olá **getMessageId** método de mensagem de saudação, que permanece constante entre tentativas de entrega.

## <a name="delete-topics-and-subscriptions"></a>Excluir tópicos e assinaturas
Olá tópicos toodelete a principal forma e assinaturas é toouse uma **ServiceBusContract** objeto. Excluir um tópico também excluirá quaisquer assinaturas que são registradas com o tópico de saudação. As assinaturas também podem ser excluídas de forma independente.

```java
// Delete subscriptions
service.deleteSubscription("TestTopic", "AllMessages");
service.deleteSubscription("TestTopic", "HighMessages");
service.deleteSubscription("TestTopic", "LowMessages");

// Delete a topic
service.deleteTopic("TestTopic");
```

## <a name="next-steps"></a>Próximas etapas
Agora que você aprendeu as Noções básicas de saudação de filas do barramento de serviço, consulte [filas do barramento de serviço, tópicos e assinaturas] [ Service Bus queues, topics, and subscriptions] para obter mais informações.

[Azure SDK for Java]: http://azure.microsoft.com/develop/java/
[Azure Toolkit for Eclipse]: ../azure-toolkit-for-eclipse.md
[Service Bus queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[SqlFilter]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter 
[SqlFilter.SqlExpression]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter#Microsoft_ServiceBus_Messaging_SqlFilter_SqlExpression
[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage

[0]: ./media/service-bus-java-how-to-use-topics-subscriptions/sb-queues-13.png
[2]: ./media/service-bus-java-how-to-use-topics-subscriptions/sb-queues-04.png
[3]: ./media/service-bus-java-how-to-use-topics-subscriptions/sb-queues-09.png
