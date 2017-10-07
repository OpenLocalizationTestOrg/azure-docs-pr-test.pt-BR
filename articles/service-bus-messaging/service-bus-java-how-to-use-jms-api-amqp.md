---
title: "aaaHow toouse AMQP 1.0 com hello API do barramento de serviço Java | Microsoft Docs"
description: "Como toouse Olá JMS Java Message Service () com o Advanced Message Queuing Protodol (AMQP) 1.0 e o barramento de serviço do Azure."
services: service-bus-messaging
documentationcenter: java
author: sethmanheim
manager: timlt
editor: 
ms.assetid: be766f42-6fd1-410c-b275-8c400c811519
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: 3e1d0329f2675a2273e12bb7389d3ce38b156a5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-java-message-service-jms-api-with-service-bus-and-amqp-10"></a>Como toouse Olá serviço JMS (Java Message) API com AMQP 1.0 e o barramento de serviço
Olá Advanced Message Queuing Protocol (AMQP) 1.0 é um protocolo de mensagens eficiente, confiável e de nível de transmissão que você pode usar aplicativos de mensagens robusto e de plataforma cruzada toobuild.

Suporte para AMQP 1.0 no barramento de serviço significa que você pode usar Olá enfileiramento e publica/assina recursos de mensagens orientados de uma variedade de plataformas usando um protocolo binário eficiente. Além disso, você pode criar aplicativos formados por componentes criados com o uso de uma mistura de linguagens, estruturas e sistemas operacionais.

Este artigo explica como toouse Service Bus recursos de mensagens (filas e a publicação/assinatura tópicos) de aplicativos Java usando Olá populares serviço JMS (Java Message) API padrão. Há um [artigo complementar](service-bus-amqp-dotnet.md) que explica como toodo Olá mesmo usando Olá API .NET do barramento de serviço. Você pode usar esses toolearn juntos de duas guias sobre mensagens de plataforma cruzada usando AMQP 1.0.

## <a name="get-started-with-service-bus"></a>Introdução ao Barramento de serviço
Este guia presume que você já tenha um namespace do Barramento de Serviço que contém uma fila denominada **queue1**. Se você não fizer isso, você pode [criar namespace hello e fila](service-bus-create-namespace-portal.md) usando Olá [portal do Azure](https://portal.azure.com). Para obter mais informações sobre como toocreate namespaces de barramento de serviço e as filas, consulte [começar com filas do barramento de serviço](service-bus-dotnet-get-started-with-queues.md).

> [!NOTE]
> Filas e tópicos particionados também dão suporte ao AMQP. Para saber mais, confira [Entidades de mensagens particionadas](service-bus-partitioning.md) e [Suporte a AMQP 1.0 para filas e tópicos particionados do Barramento de Serviço](service-bus-partitioned-queues-and-topics-amqp-overview.md).
> 
> 

## <a name="downloading-hello-amqp-10-jms-client-library"></a>Baixando a biblioteca de cliente do AMQP 1.0 JMS Olá
Para obter informações sobre onde toodownload Olá a versão mais recente da biblioteca de cliente Olá Apache Qpid JMS AMQP 1.0, visite [https://qpid.apache.org/download.html](https://qpid.apache.org/download.html).

Você deve adicionar Olá quatro arquivos JAR a seguir de saudação Apache Qpid JMS AMQP 1.0 distribuição arquivamento toohello CLASSPATH Java ao compilar e executar aplicativos do JMS com o barramento de serviço:

* geronimo-jms\_1.1\_spec-1.0.jar
* qpid-amqp-1-0-client-[version].jar
* qpid-amqp-1-0-client-jms-[version].jar
* qpid-amqp-1-0-common-[version].jar

## <a name="coding-java-applications"></a>Codificando os aplicativos Java
### <a name="java-naming-and-directory-interface-jndi"></a>Java Naming and Directory Interface (JNDI)
O JMS utiliza Olá Java Naming and Directory Interface (JNDI) toocreate uma separação entre nomes lógicos e físicos. Dois tipos de objetos JMS são resolvidos usando a JNDI: ConnectionFactory e Destino. O JNDI utiliza um modelo de provedor para o qual você pode conectar tarefas de resolução de nome do diretório diferentes serviços toohandle. Olá Apache Qpid JMS AMQP 1.0 biblioteca vem com um simples propriedades provedor JNDI baseado em arquivo que é configurado usando um arquivo de propriedades do seguinte Olá formato:

```
# servicebus.properties - sample JNDI configuration

# Register a ConnectionFactory in JNDI using hello form:
# connectionfactory.[jndi_name] = [ConnectionURL]
connectionfactory.SBCF = amqps://[SASPolicyName]:[SASPolicyKey]@[namespace].servicebus.windows.net

# Register some queues in JNDI using hello form
# queue.[jndi_name] = [physical_name]
# topic.[jndi_name] = [physical_name]
queue.QUEUE = queue1
```

#### <a name="configure-hello-connectionfactory"></a>Configurar Olá ConnectionFactory
Olá toodefine de entrada usado um **ConnectionFactory** Olá Qpid provedor JNDI de propriedades de arquivo é do hello formato a seguir:

```
connectionfactory.[jndi_name] = [ConnectionURL]
```

Onde **[jndi_name]** e **[ConnectionURL]** ter Olá significados a seguir:

* **[jndi_name]** : nome lógico Olá Olá ConnectionFactory. Este é o nome de saudação que será resolvido no aplicativo de Java hello usando o método de JNDI Intialcontext hello.
* **[ConnectionURL]** : Uma URL que fornece biblioteca JMS Olá Olá informações necessárias toohello agente AMQP.

formato de saudação do hello **ConnectionURL** é o seguinte:

```
amqps://[SASPolicyName]:[SASPolicyKey]@[namespace].servicebus.windows.net
```
Onde **[namespace]**, **[SASPolicyName]** e **[SASPolicyKey]** ter Olá significados a seguir:

* **[namespace]** : Olá namespace de barramento de serviço.
* **[SASPolicyName]** : nome de diretiva de assinatura de acesso compartilhado da fila de saudação.
* **[SASPolicyKey]** : chave de política de assinatura de acesso compartilhado da fila de saudação.

> [!NOTE]
> Você deve codificar URL senha de saudação manualmente. Um utilitário útil de codificação de URL está disponível em [http://www.w3schools.com/tags/ref_urlencode.asp](http://www.w3schools.com/tags/ref_urlencode.asp).
> 
> 

#### <a name="configure-destinations"></a>Configurar destinos
Olá toodefine de entrada usada que é um destino no provedor JNDI de arquivos de propriedades do hello Qpid do hello formato a seguir:

```
queue.[jndi_name] = [physical_name]
```

ou o

```
topic.[jndi_name] = [physical_name]
```

Onde **[jndi\_nome]** e **[físico\_nome]** ter Olá significados a seguir:

* **[jndi_name]** : nome lógico de saudação do destino de saudação. Este é o nome de saudação que será resolvido no aplicativo de Java hello usando o método de JNDI Intialcontext hello.
* **[physical_name]** : nome de saudação do hello aplicativo hello do barramento de serviço entidade toowhich envia ou recebe mensagens.

> [!NOTE]
> Durante o recebimento de uma assinatura de tópico do barramento de serviço, nome físico do hello especificado no JNDI deve ser o nome de saudação do tópico de saudação. nome da assinatura Olá é fornecida quando a assinatura durável Olá é criada no código do aplicativo JMS de saudação. Olá [guia do desenvolvedor do Service Bus AMQP 1.0](service-bus-amqp-dotnet.md) fornece mais detalhes sobre como trabalhar com tópicos do barramento de serviço do JMS.
> 
> 

### <a name="write-hello-jms-application"></a>Gravar saudação JMS aplicativo
Não existem APIs ou opções especiais obrigatórias ao usar o JMS com o Service Bus. No entanto, existem algumas restrições que serão abordadas posteriormente. Assim como com qualquer aplicativo JMS, Olá a primeira coisa exigida é configuração do ambiente de JNDI hello, tooresolve capaz de toobe um **ConnectionFactory** e destinos.

#### <a name="configure-hello-jndi-initialcontext"></a>Configurar Olá JNDI InitialContext
ambiente de JNDI Hello está configurado, passando uma tabela de hash das informações de configuração no construtor de saudação da classe de javax.naming.InitialContext hello. dois elementos necessários Olá na tabela de hash de saudação são nome da classe Olá da saudação inicial fábrica de contexto e hello URL do provedor. Olá código a seguir mostra como tooconfigure Olá JNDI ambiente toouse Olá Qpid propriedades baseado em arquivo provedor JNDI com um arquivo de propriedades denominado **ServiceBus**.

```java
Hashtable<String, String> env = new Hashtable<String, String>(); 
env.put(Context.INITIAL_CONTEXT_FACTORY, "org.apache.qpid.amqp_1_0.jms.jndi.PropertiesFileInitialContextFactory"); 
env.put(Context.PROVIDER_URL, "servicebus.properties"); 
InitialContext context = new InitialContext(env);
``` 

### <a name="a-simple-jms-application-using-a-service-bus-queue"></a>Um aplicativo JMS simples que usa uma fila do Barramento de Serviço
Hello programa de exemplo a seguir envia a fila de barramento de serviço do JMS TextMessages tooa com nome lógico do hello JNDI da fila e recebe mensagens de saudação novamente.

```java
// SimpleSenderReceiver.java

import javax.jms.*;
import javax.naming.Context;
import javax.naming.InitialContext;
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.util.Hashtable;
import java.util.Random;

public class SimpleSenderReceiver implements MessageListener {
    private static boolean runReceiver = true;
    private Connection connection;
    private Session sendSession;
    private Session receiveSession;
    private MessageProducer sender;
    private MessageConsumer receiver;
    private static Random randomGenerator = new Random();

    public SimpleSenderReceiver() throws Exception {
        // Configure JNDI environment
        Hashtable<String, String> env = new Hashtable<String, String>();
        env.put(Context.INITIAL_CONTEXT_FACTORY, 
                   "org.apache.qpid.amqp_1_0.jms.jndi.PropertiesFileInitialContextFactory");
        env.put(Context.PROVIDER_URL, "servicebus.properties");
        Context context = new InitialContext(env);

        // Look up ConnectionFactory and Queue
        ConnectionFactory cf = (ConnectionFactory) context.lookup("SBCF");
        Destination queue = (Destination) context.lookup("QUEUE");

        // Create Connection
        connection = cf.createConnection();

        // Create sender-side Session and MessageProducer
        sendSession = connection.createSession(false, Session.AUTO_ACKNOWLEDGE);
        sender = sendSession.createProducer(queue);

        if (runReceiver) {
            // Create receiver-side Session, MessageConsumer,and MessageListener
            receiveSession = connection.createSession(false, Session.CLIENT_ACKNOWLEDGE);
            receiver = receiveSession.createConsumer(queue);
            receiver.setMessageListener(this);
            connection.start();
        }
    }

    public static void main(String[] args) {
        try {

            if ((args.length > 0) && args[0].equalsIgnoreCase("sendonly")) {
                runReceiver = false;
            }

            SimpleSenderReceiver simpleSenderReceiver = new SimpleSenderReceiver();
            System.out.println("Press [enter] toosend a message. Type 'exit' + [enter] tooquit.");
            BufferedReader commandLine = new java.io.BufferedReader(new InputStreamReader(System.in));

            while (true) {
                String s = commandLine.readLine();
                if (s.equalsIgnoreCase("exit")) {
                    simpleSenderReceiver.close();
                    System.exit(0);
                } else {
                    simpleSenderReceiver.sendMessage();
                }
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    private void sendMessage() throws JMSException {
        TextMessage message = sendSession.createTextMessage();
        message.setText("Test AMQP message from JMS");
        long randomMessageID = randomGenerator.nextLong() >>>1;
        message.setJMSMessageID("ID:" + randomMessageID);
        sender.send(message);
        System.out.println("Sent message with JMSMessageID = " + message.getJMSMessageID());
    }

    public void close() throws JMSException {
        connection.close();
    }

    public void onMessage(Message message) {
        try {
            System.out.println("Received message with JMSMessageID = " + message.getJMSMessageID());
            message.acknowledge();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}    
```

### <a name="run-hello-application"></a>Executar o aplicativo hello
Executar o aplicativo hello produz saída de formulário de saudação:

```
> java SimpleSenderReceiver
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.

Sent message with JMSMessageID = ID:2867600614942270318
Received message with JMSMessageID = ID:2867600614942270318

Sent message with JMSMessageID = ID:7578408152750301483
Received message with JMSMessageID = ID:7578408152750301483

Sent message with JMSMessageID = ID:956102171969368961
Received message with JMSMessageID = ID:956102171969368961
exit
```

## <a name="cross-platform-messaging-between-jms-and-net"></a>Mensagens em plataformas cruzadas entre JMS e .NET
Este guia mostrado como toosend e receber mensagens tooand do barramento de serviço usando JMS. No entanto, um dos principais benefícios de saudação do AMQP 1.0 é que ele permite que aplicativos toobe criada a partir de componentes escritos em idiomas diferentes, com mensagens trocadas confiável e com fidelidade total.

Usando o aplicativo de JMS do exemplo hello descrito acima e um aplicativo .NET semelhante obtido um artigo complementar, [usando o barramento de serviço do .NET com AMQP 1.0](service-bus-amqp-dotnet.md), você pode trocar mensagens entre .NET e Java. Leia este artigo para obter mais informações sobre detalhes de saudação da plataforma cruzada usando AMQP 1.0 e o barramento de serviço do sistema de mensagens.

### <a name="jms-toonet"></a>Too.NET JMS
toodemonstrate JMS too.NET mensagens:

* Inicie o aplicativo de exemplo .NET hello sem argumentos de linha de comando.
* Inicie o aplicativo de exemplo hello Java com argumento de linha de comando do hello "sendonly". Nesse modo, hello aplicativo não receberá mensagens da fila de hello, ele enviará apenas.
* Pressione **Enter** algumas vezes no console de aplicativos do Java hello, que fará com que toobe de mensagens enviada.
* Essas mensagens são recebidas pelo Olá aplicativo .NET.

#### <a name="output-from-jms-application"></a>Saída do aplicativo JMS
```
> java SimpleSenderReceiver sendonly
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.
Sent message with JMSMessageID = ID:4364096528752411591
Sent message with JMSMessageID = ID:459252991689389983
Sent message with JMSMessageID = ID:1565011046230456854
exit
```

#### <a name="output-from-net-application"></a>Saída do aplicativo .NET
```
> SimpleSenderReceiver.exe    
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.
Received message with MessageID = 4364096528752411591
Received message with MessageID = 459252991689389983
Received message with MessageID = 1565011046230456854
exit
```

### <a name="net-toojms"></a>TooJMS .NET
toodemonstrate tooJMS de .NET do sistema de mensagens:

* Inicie o aplicativo de exemplo .NET hello com argumento de linha de comando do hello "sendonly". Nesse modo, hello aplicativo não receberá mensagens da fila de hello, ele enviará apenas.
* Inicie o aplicativo de exemplo hello Java sem argumentos de linha de comando.
* Pressione **Enter** algumas vezes no console de aplicativo do .NET hello, que fará com que toobe de mensagens enviada.
* Essas mensagens são recebidas pelo Olá aplicativo Java.

#### <a name="output-from-net-application"></a>Saída do aplicativo .NET
```
> SimpleSenderReceiver.exe sendonly
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.
Sent message with MessageID = d64e681a310a48a1ae0ce7b017bf1cf3    
Sent message with MessageID = 98a39664995b4f74b32e2a0ecccc46bb
Sent message with MessageID = acbca67f03c346de9b7893026f97ddeb
exit
```

#### <a name="output-from-jms-application"></a>Saída do aplicativo JMS
```
> java SimpleSenderReceiver    
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.
Received message with JMSMessageID = ID:d64e681a310a48a1ae0ce7b017bf1cf3
Received message with JMSMessageID = ID:98a39664995b4f74b32e2a0ecccc46bb
Received message with JMSMessageID = ID:acbca67f03c346de9b7893026f97ddeb
exit
```

## <a name="unsupported-features-and-restrictions"></a>Restrições e recursos não suportados
Olá restrições a seguir existe ao usar JMS no AMQP 1.0 com o barramento de serviço, ou seja:

* Apenas um **MessageProducer** ou **MessageConsumer** é permitido por **Sessão**. Se você precisar toocreate vários **MessageProducers** ou **MessageConsumers** em um aplicativo, crie um dedicado **sessão** para cada um deles.
* Assinaturas de tópico voláteis não são atualmente suportadas.
* **MessageSelectors** não são atualmente suportados.
* Destinos temporários; Por exemplo, **TemporaryQueue**, **TemporaryTopic** atualmente não têm suporte, juntamente com hello **QueueRequestor** e **TopicRequestor**APIs que usá-los.
* Não há suporte para as sessões transacionadas e transações distribuídas.

## <a name="summary"></a>Resumo
Este tooguide como mostrou como toouse orientadas do barramento de serviço recursos de mensagens (filas e a publicação/assinatura tópicos) do Java usando Olá API de JMS populares e AMQP 1.0.

Você também pode usar o AMQP 1.0 do Service Bus de outras linguagens, incluindo .NET, C, Python e PHP. Componentes desenvolvidos utilizando esses idiomas diferentes poderão trocar mensagens com segurança e fidelidade completa usando o suporte de saudação AMQP 1.0 no barramento de serviço.

## <a name="next-steps"></a>Próximas etapas
* [Suporte para o AMQP 1.0 no Barramento de Serviço do Azure](service-bus-amqp-overview.md)
* [Como toouse AMQP 1.0 com hello API .NET do barramento de serviço](service-bus-dotnet-advanced-message-queuing.md)
* [Guia do Desenvolvedor do AMQP 1.0 do Barramento de Serviço](service-bus-amqp-dotnet.md)
* [Introdução às filas do Barramento de Serviço](service-bus-dotnet-get-started-with-queues.md)
* [Centro de Desenvolvedores do Java](https://azure.microsoft.com/develop/java/)

