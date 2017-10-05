---
title: "Como usar o AMQP 1.0 com o API do Barramento de Serviço em Java | Microsoft Docs"
description: "Como usar o Java Message Service (JMS) com o barramento de serviço do Azure e Advanced Message Queuing Protocol (AMQP) 1.0."
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
ms.openlocfilehash: 0848facd764c4fb0d7f95c1ae89ecb02a32257e1
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-the-java-message-service-jms-api-with-service-bus-and-amqp-10"></a><span data-ttu-id="ad36e-103">Como usar a API do Serviço de Mensagem Java (JMS) com Barramento de Serviço e AMQP 1.0</span><span class="sxs-lookup"><span data-stu-id="ad36e-103">How to use the Java Message Service (JMS) API with Service Bus and AMQP 1.0</span></span>
<span data-ttu-id="ad36e-104">O AMQP 1.0 é um protocolo de mensagens eficiente, confiável e conectado que pode ser usado para criar aplicativos de mensagens robustos em plataformas cruzadas.</span><span class="sxs-lookup"><span data-stu-id="ad36e-104">The Advanced Message Queuing Protocol (AMQP) 1.0 is an efficient, reliable, wire-level messaging protocol that you can use to build robust, cross-platform messaging applications.</span></span>

<span data-ttu-id="ad36e-105">O suporte para o AMQP 1.0 no Service Bus significa que você pode usar o enfileiramento e publicar/assinar os recursos de mensagens agenciadas a partir de uma variedade de plataformas usando um protocolo binário eficiente.</span><span class="sxs-lookup"><span data-stu-id="ad36e-105">Support for AMQP 1.0 in Service Bus means that you can use the queuing and publish/subscribe brokered messaging features from a range of platforms using an efficient binary protocol.</span></span> <span data-ttu-id="ad36e-106">Além disso, você pode criar aplicativos formados por componentes criados com o uso de uma mistura de linguagens, estruturas e sistemas operacionais.</span><span class="sxs-lookup"><span data-stu-id="ad36e-106">Furthermore, you can build applications comprised of components built using a mix of languages, frameworks, and operating systems.</span></span>

<span data-ttu-id="ad36e-107">Este artigo explica como usar os recursos de sistema de mensagens do Barramento de Serviço (tópicos sobre filas e publicação/assinatura) de aplicativos Java usando o popular padrão de API do JMS (Java Message Service).</span><span class="sxs-lookup"><span data-stu-id="ad36e-107">This article explains how to use Service Bus messaging features (queues and publish/subscribe topics) from Java applications using the popular Java Message Service (JMS) API standard.</span></span> <span data-ttu-id="ad36e-108">Existe um [artigo complementar](service-bus-amqp-dotnet.md) que explica como fazer o mesmo usando a API do Barramento de Serviço do .NET.</span><span class="sxs-lookup"><span data-stu-id="ad36e-108">There is a [companion article](service-bus-amqp-dotnet.md) that explains how to do the same using the Service Bus .NET API.</span></span> <span data-ttu-id="ad36e-109">Você pode usar esses dois guias em conjunto para saber mais sobre mensagens em plataformas cruzadas usando o AMQP 1.0.</span><span class="sxs-lookup"><span data-stu-id="ad36e-109">You can use these two guides together to learn about cross-platform messaging using AMQP 1.0.</span></span>

## <a name="get-started-with-service-bus"></a><span data-ttu-id="ad36e-110">Introdução ao Barramento de serviço</span><span class="sxs-lookup"><span data-stu-id="ad36e-110">Get started with Service Bus</span></span>
<span data-ttu-id="ad36e-111">Este guia presume que você já tenha um namespace do Barramento de Serviço que contém uma fila denominada **queue1**.</span><span class="sxs-lookup"><span data-stu-id="ad36e-111">This guide assumes that you already have a Service Bus namespace containing a queue named **queue1**.</span></span> <span data-ttu-id="ad36e-112">Caso contrário, você pode [criar o namespace e a fila](service-bus-create-namespace-portal.md) usando o [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ad36e-112">If you do not, then you can [create the namespace and queue](service-bus-create-namespace-portal.md) using the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="ad36e-113">Para obter mais informações sobre como criar namespaces e filas do Barramento de Serviço, consulte [Introdução às filas do Barramento de Serviço](service-bus-dotnet-get-started-with-queues.md).</span><span class="sxs-lookup"><span data-stu-id="ad36e-113">For more information about how to create Service Bus namespaces and queues, see [Get started with Service Bus queues](service-bus-dotnet-get-started-with-queues.md).</span></span>

> [!NOTE]
> <span data-ttu-id="ad36e-114">Filas e tópicos particionados também dão suporte ao AMQP.</span><span class="sxs-lookup"><span data-stu-id="ad36e-114">Partitioned queues and topics also support AMQP.</span></span> <span data-ttu-id="ad36e-115">Para saber mais, confira [Entidades de mensagens particionadas](service-bus-partitioning.md) e [Suporte a AMQP 1.0 para filas e tópicos particionados do Barramento de Serviço](service-bus-partitioned-queues-and-topics-amqp-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ad36e-115">For more information, see [Partitioned messaging entities](service-bus-partitioning.md) and [AMQP 1.0 support for Service Bus partitioned queues and topics](service-bus-partitioned-queues-and-topics-amqp-overview.md).</span></span>
> 
> 

## <a name="downloading-the-amqp-10-jms-client-library"></a><span data-ttu-id="ad36e-116">Baixando a biblioteca do cliente do JMS do AMQP 1.0</span><span class="sxs-lookup"><span data-stu-id="ad36e-116">Downloading the AMQP 1.0 JMS client library</span></span>
<span data-ttu-id="ad36e-117">Para obter informações sobre onde baixar a versão mais recente da biblioteca do cliente Apache Qpid JMS do AMQP 1.0, acesse [https://qpid.apache.org/download.html](https://qpid.apache.org/download.html).</span><span class="sxs-lookup"><span data-stu-id="ad36e-117">For information about where to download the latest version of the Apache Qpid JMS AMQP 1.0 client library, visit [https://qpid.apache.org/download.html](https://qpid.apache.org/download.html).</span></span>

<span data-ttu-id="ad36e-118">Você deve adicionar os seguintes quatro arquivos JAR do arquivamento de distribuição do Apache Qpid JMS do AMQP 1.0 ao CLASSPATH do Java ao criar e executar aplicativos do JMS com o Barramento de Serviço:</span><span class="sxs-lookup"><span data-stu-id="ad36e-118">You must add the following four JAR files from the Apache Qpid JMS AMQP 1.0 distribution archive to the Java CLASSPATH when building and running JMS applications with Service Bus:</span></span>

* <span data-ttu-id="ad36e-119">geronimo-jms\_1.1\_spec-1.0.jar</span><span class="sxs-lookup"><span data-stu-id="ad36e-119">geronimo-jms\_1.1\_spec-1.0.jar</span></span>
* <span data-ttu-id="ad36e-120">qpid-amqp-1-0-client-[version].jar</span><span class="sxs-lookup"><span data-stu-id="ad36e-120">qpid-amqp-1-0-client-[version].jar</span></span>
* <span data-ttu-id="ad36e-121">qpid-amqp-1-0-client-jms-[version].jar</span><span class="sxs-lookup"><span data-stu-id="ad36e-121">qpid-amqp-1-0-client-jms-[version].jar</span></span>
* <span data-ttu-id="ad36e-122">qpid-amqp-1-0-common-[version].jar</span><span class="sxs-lookup"><span data-stu-id="ad36e-122">qpid-amqp-1-0-common-[version].jar</span></span>

## <a name="coding-java-applications"></a><span data-ttu-id="ad36e-123">Codificando os aplicativos Java</span><span class="sxs-lookup"><span data-stu-id="ad36e-123">Coding Java applications</span></span>
### <a name="java-naming-and-directory-interface-jndi"></a><span data-ttu-id="ad36e-124">Java Naming and Directory Interface (JNDI)</span><span class="sxs-lookup"><span data-stu-id="ad36e-124">Java Naming and Directory Interface (JNDI)</span></span>
<span data-ttu-id="ad36e-125">O JMS usa a Java Naming and Directory Interface (JNDI) para criar uma separação entre nomes lógicos e físicos.</span><span class="sxs-lookup"><span data-stu-id="ad36e-125">JMS uses the Java Naming and Directory Interface (JNDI) to create a separation between logical names and physical names.</span></span> <span data-ttu-id="ad36e-126">Dois tipos de objetos JMS são resolvidos usando a JNDI: ConnectionFactory e Destino.</span><span class="sxs-lookup"><span data-stu-id="ad36e-126">Two types of JMS objects are resolved using JNDI: ConnectionFactory and Destination.</span></span> <span data-ttu-id="ad36e-127">A JNDI usa um modelo de provedor no qual você pode conectar diferentes serviços de diretório para lidar com tarefas de resolução de nome.</span><span class="sxs-lookup"><span data-stu-id="ad36e-127">JNDI uses a provider model into which you can plug different directory services to handle name resolution duties.</span></span> <span data-ttu-id="ad36e-128">A biblioteca Apache Qpid JMS do AMQP 1.0 vem com um Provedor JNDI simples baseado em arquivo de propriedades que é configurado usando um arquivo de propriedades no seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="ad36e-128">The Apache Qpid JMS AMQP 1.0 library comes with a simple properties file-based JNDI Provider that is configured using a properties file of the following format:</span></span>

```
# servicebus.properties - sample JNDI configuration

# Register a ConnectionFactory in JNDI using the form:
# connectionfactory.[jndi_name] = [ConnectionURL]
connectionfactory.SBCF = amqps://[SASPolicyName]:[SASPolicyKey]@[namespace].servicebus.windows.net

# Register some queues in JNDI using the form
# queue.[jndi_name] = [physical_name]
# topic.[jndi_name] = [physical_name]
queue.QUEUE = queue1
```

#### <a name="configure-the-connectionfactory"></a><span data-ttu-id="ad36e-129">Configurar o ConnectionFactory</span><span class="sxs-lookup"><span data-stu-id="ad36e-129">Configure the ConnectionFactory</span></span>
<span data-ttu-id="ad36e-130">A entrada usada para definir um **ConnectionFactory** no provedor JNDI do arquivo de propriedades do Qpid tem o seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="ad36e-130">The entry used to define a **ConnectionFactory** in the Qpid properties file JNDI provider is of the following format:</span></span>

```
connectionfactory.[jndi_name] = [ConnectionURL]
```

<span data-ttu-id="ad36e-131">Em que **[jndi_name]** e **[ConnectionURL]** têm os seguintes significados:</span><span class="sxs-lookup"><span data-stu-id="ad36e-131">Where **[jndi_name]** and **[ConnectionURL]** have the following meanings:</span></span>

* <span data-ttu-id="ad36e-132">**[jndi_name]**: o nome lógico do ConnectionFactory.</span><span class="sxs-lookup"><span data-stu-id="ad36e-132">**[jndi_name]**: The logical name of the ConnectionFactory.</span></span> <span data-ttu-id="ad36e-133">Este é o nome que será resolvido no aplicativo Java usando o método IntialContext.lookup() do JNDI.</span><span class="sxs-lookup"><span data-stu-id="ad36e-133">This is the name that will be resolved in the Java application using the JNDI IntialContext.lookup() method.</span></span>
* <span data-ttu-id="ad36e-134">**[ConnectionURL]**: uma URL que fornece à biblioteca JMS as informações necessárias para o agente do AMQP.</span><span class="sxs-lookup"><span data-stu-id="ad36e-134">**[ConnectionURL]**: A URL that provides the JMS library with the information required to the AMQP broker.</span></span>

<span data-ttu-id="ad36e-135">O formato de **ConnectionURL** é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="ad36e-135">The format of the **ConnectionURL** is as follows:</span></span>

```
amqps://[SASPolicyName]:[SASPolicyKey]@[namespace].servicebus.windows.net
```
<span data-ttu-id="ad36e-136">Em que **[namespace]**, **[SASPolicyName]** e **[SASPolicyKey]** têm os seguintes significados:</span><span class="sxs-lookup"><span data-stu-id="ad36e-136">Where **[namespace]**, **[SASPolicyName]** and **[SASPolicyKey]** have the following meanings:</span></span>

* <span data-ttu-id="ad36e-137">**[namespace]**: o namespace do Barramento de Serviço.</span><span class="sxs-lookup"><span data-stu-id="ad36e-137">**[namespace]**: The Service Bus namespace.</span></span>
* <span data-ttu-id="ad36e-138">**[SASPolicyName]**: nome da política da Assinatura de Acesso Compartilhado da Fila.</span><span class="sxs-lookup"><span data-stu-id="ad36e-138">**[SASPolicyName]**: The Queue Shared Access Signature policy name.</span></span>
* <span data-ttu-id="ad36e-139">**[SASPolicyKey]**: chave da política da Assinatura de Acesso Compartilhado da Fila.</span><span class="sxs-lookup"><span data-stu-id="ad36e-139">**[SASPolicyKey]**: The Queue Shared Access Signature policy key.</span></span>

> [!NOTE]
> <span data-ttu-id="ad36e-140">você deve executar uma codificação de URL da senha manualmente.</span><span class="sxs-lookup"><span data-stu-id="ad36e-140">You must URL-encode the password manually.</span></span> <span data-ttu-id="ad36e-141">Um utilitário útil de codificação de URL está disponível em [http://www.w3schools.com/tags/ref_urlencode.asp](http://www.w3schools.com/tags/ref_urlencode.asp).</span><span class="sxs-lookup"><span data-stu-id="ad36e-141">A useful URL-encoding utility is available at [http://www.w3schools.com/tags/ref_urlencode.asp](http://www.w3schools.com/tags/ref_urlencode.asp).</span></span>
> 
> 

#### <a name="configure-destinations"></a><span data-ttu-id="ad36e-142">Configurar destinos</span><span class="sxs-lookup"><span data-stu-id="ad36e-142">Configure destinations</span></span>
<span data-ttu-id="ad36e-143">A entrada usada para definir um destino no provedor JNDI do arquivo de propriedades do Qpid tem o seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="ad36e-143">The entry used to define a destination in the Qpid properties file JNDI provider is of the following format:</span></span>

```
queue.[jndi_name] = [physical_name]
```

<span data-ttu-id="ad36e-144">ou o</span><span class="sxs-lookup"><span data-stu-id="ad36e-144">or</span></span>

```
topic.[jndi_name] = [physical_name]
```

<span data-ttu-id="ad36e-145">Em que **[jndi\_name]** e **[physical\_name]** têm os seguintes significados:</span><span class="sxs-lookup"><span data-stu-id="ad36e-145">Where **[jndi\_name]** and **[physical\_name]** have the following meanings:</span></span>

* <span data-ttu-id="ad36e-146">**[jndi_name]**: o nome lógico do destino.</span><span class="sxs-lookup"><span data-stu-id="ad36e-146">**[jndi_name]**: The logical name of the destination.</span></span> <span data-ttu-id="ad36e-147">Este é o nome que será resolvido no aplicativo Java usando o método IntialContext.lookup() do JNDI.</span><span class="sxs-lookup"><span data-stu-id="ad36e-147">This is the name that will be resolved in the Java application using the JNDI IntialContext.lookup() method.</span></span>
* <span data-ttu-id="ad36e-148">**[physical_name]**: o nome da entidade do Barramento de Serviço para a qual o aplicativo envia ou recebe mensagens.</span><span class="sxs-lookup"><span data-stu-id="ad36e-148">**[physical_name]**: The name of the Service Bus entity to which the application sends or receives messages.</span></span>

> [!NOTE]
> <span data-ttu-id="ad36e-149">Ao receber de uma assinatura de tópico do Barramento de Serviço, o nome físico especificado na JNDI deve ser o nome do tópico.</span><span class="sxs-lookup"><span data-stu-id="ad36e-149">When receiving from a Service Bus topic subscription, the physical name specified in JNDI should be the name of the topic.</span></span> <span data-ttu-id="ad36e-150">O nome da assinatura é fornecido quando a assinatura durável é criada no código do aplicativo JMS.</span><span class="sxs-lookup"><span data-stu-id="ad36e-150">The subscription name is provided when the durable subscription is created in the JMS application code.</span></span> <span data-ttu-id="ad36e-151">O [Guia de desenvolvedor do AMQP 1.0 do Barramento de Serviço](service-bus-amqp-dotnet.md) fornece mais detalhes sobre como trabalhar com tópicos do Barramento de Serviço por meio do JMS.</span><span class="sxs-lookup"><span data-stu-id="ad36e-151">The [Service Bus AMQP 1.0 Developer's Guide](service-bus-amqp-dotnet.md) provides more details on working with Service Bus topics from JMS.</span></span>
> 
> 

### <a name="write-the-jms-application"></a><span data-ttu-id="ad36e-152">Escrever o aplicativo JMS</span><span class="sxs-lookup"><span data-stu-id="ad36e-152">Write the JMS application</span></span>
<span data-ttu-id="ad36e-153">Não existem APIs ou opções especiais obrigatórias ao usar o JMS com o Service Bus.</span><span class="sxs-lookup"><span data-stu-id="ad36e-153">There are no special APIs or options required when using JMS with Service Bus.</span></span> <span data-ttu-id="ad36e-154">No entanto, existem algumas restrições que serão abordadas posteriormente.</span><span class="sxs-lookup"><span data-stu-id="ad36e-154">However, there are a few restrictions that will be covered later.</span></span> <span data-ttu-id="ad36e-155">Da mesma forma que ocorre com qualquer aplicativo JMS, a primeiro item necessário é a configuração do ambiente JNDI, para ser capaz de resolver um **ConnectionFactory** e destinos.</span><span class="sxs-lookup"><span data-stu-id="ad36e-155">As with any JMS application, the first thing required is configuration of the JNDI environment, to be able to resolve a **ConnectionFactory** and destinations.</span></span>

#### <a name="configure-the-jndi-initialcontext"></a><span data-ttu-id="ad36e-156">Configurar o InitialContext de JNDI</span><span class="sxs-lookup"><span data-stu-id="ad36e-156">Configure the JNDI InitialContext</span></span>
<span data-ttu-id="ad36e-157">O ambiente JNDI é configurado por meio da transmissão de uma tabela de hash com informações de configuração para o construtor da classe javax.naming.InitialContext.</span><span class="sxs-lookup"><span data-stu-id="ad36e-157">The JNDI environment is configured by passing a hashtable of configuration information into the constructor of the javax.naming.InitialContext class.</span></span> <span data-ttu-id="ad36e-158">Os dois elementos necessários da tabela de hash são o nome da classe de Initial Context Factory e a URL do Provedor.</span><span class="sxs-lookup"><span data-stu-id="ad36e-158">The two required elements in the hashtable are the class name of the Initial Context Factory and the Provider URL.</span></span> <span data-ttu-id="ad36e-159">O código a seguir mostra como configurar o ambiente JNDI para usar o Provedor JNDI com base em arquivo de propriedades do Qpid com um arquivo de propriedades chamado **servicebus.properties**.</span><span class="sxs-lookup"><span data-stu-id="ad36e-159">The following code shows how to configure the JNDI environment to use the Qpid properties file based JNDI Provider with a properties file named **servicebus.properties**.</span></span>

```java
Hashtable<String, String> env = new Hashtable<String, String>(); 
env.put(Context.INITIAL_CONTEXT_FACTORY, "org.apache.qpid.amqp_1_0.jms.jndi.PropertiesFileInitialContextFactory"); 
env.put(Context.PROVIDER_URL, "servicebus.properties"); 
InitialContext context = new InitialContext(env);
``` 

### <a name="a-simple-jms-application-using-a-service-bus-queue"></a><span data-ttu-id="ad36e-160">Um aplicativo JMS simples que usa uma fila do Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="ad36e-160">A simple JMS application using a Service Bus queue</span></span>
<span data-ttu-id="ad36e-161">O programa de exemplo a seguir envia TextMessages do JMS para uma fila do Service Bus com o nome lógico de JNDI da FILA e recebe as mensagens de volta.</span><span class="sxs-lookup"><span data-stu-id="ad36e-161">The following example program sends JMS TextMessages to a Service Bus queue with the JNDI logical name of QUEUE, and receives the messages back.</span></span>

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
            System.out.println("Press [enter] to send a message. Type 'exit' + [enter] to quit.");
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

### <a name="run-the-application"></a><span data-ttu-id="ad36e-162">Executar o aplicativo</span><span class="sxs-lookup"><span data-stu-id="ad36e-162">Run the application</span></span>
<span data-ttu-id="ad36e-163">A execução do aplicativo produz a saída do formulário:</span><span class="sxs-lookup"><span data-stu-id="ad36e-163">Running the application produces output of the form:</span></span>

```
> java SimpleSenderReceiver
Press [enter] to send a message. Type 'exit' + [enter] to quit.

Sent message with JMSMessageID = ID:2867600614942270318
Received message with JMSMessageID = ID:2867600614942270318

Sent message with JMSMessageID = ID:7578408152750301483
Received message with JMSMessageID = ID:7578408152750301483

Sent message with JMSMessageID = ID:956102171969368961
Received message with JMSMessageID = ID:956102171969368961
exit
```

## <a name="cross-platform-messaging-between-jms-and-net"></a><span data-ttu-id="ad36e-164">Mensagens em plataformas cruzadas entre JMS e .NET</span><span class="sxs-lookup"><span data-stu-id="ad36e-164">Cross-platform messaging between JMS and .NET</span></span>
<span data-ttu-id="ad36e-165">Este guia mostrou como enviar e receber mensagens de e para o Service Bus usando o JMS.</span><span class="sxs-lookup"><span data-stu-id="ad36e-165">This guide showed how to send and receive messages to and from Service Bus using JMS.</span></span> <span data-ttu-id="ad36e-166">No entanto, um dos principais benefícios do AMQP 1.0 é que ele permite que os aplicativos sejam criados a partir de componentes escritos em diferentes linguagens, com mensagens trocadas de forma confiável e com total fidelidade.</span><span class="sxs-lookup"><span data-stu-id="ad36e-166">However, one of the key benefits of AMQP 1.0 is that it enables applications to be built from components written in different languages, with messages exchanged reliably and at full fidelity.</span></span>

<span data-ttu-id="ad36e-167">Usando a amostra do aplicativo JMS descrito acima e um aplicativo .NET similar retirado de um guia complementar, [Como usar o Barramento de Serviço do .NET com o AMQP 1.0](service-bus-amqp-dotnet.md), é possível trocar mensagens entre o .NET e o Java.</span><span class="sxs-lookup"><span data-stu-id="ad36e-167">Using the sample JMS application described above and a similar .NET application taken from a companion article, [Using Service Bus from .NET with AMQP 1.0](service-bus-amqp-dotnet.md), you can exchange messages between .NET and Java.</span></span> <span data-ttu-id="ad36e-168">Leia este artigo para obter mais informações sobre os detalhes de mensagens em plataformas cruzadas usando o Barramento de Serviço e o AMQP 1.0.</span><span class="sxs-lookup"><span data-stu-id="ad36e-168">Read this article for more information about the details of cross-platform messaging using Service Bus and AMQP 1.0.</span></span>

### <a name="jms-to-net"></a><span data-ttu-id="ad36e-169">Do JMS para o .NET</span><span class="sxs-lookup"><span data-stu-id="ad36e-169">JMS to .NET</span></span>
<span data-ttu-id="ad36e-170">Para demonstrar as mensagens do JMS para o .NET:</span><span class="sxs-lookup"><span data-stu-id="ad36e-170">To demonstrate JMS to .NET messaging:</span></span>

* <span data-ttu-id="ad36e-171">Inicie a amostra do aplicativo do .NET sem nenhum argumento de linha de comando.</span><span class="sxs-lookup"><span data-stu-id="ad36e-171">Start the .NET sample application without any command-line arguments.</span></span>
* <span data-ttu-id="ad36e-172">Inicie a amostra do aplicativo Java com o argumento de linha de comando "sendonly".</span><span class="sxs-lookup"><span data-stu-id="ad36e-172">Start the Java sample application with the "sendonly" command-line argument.</span></span> <span data-ttu-id="ad36e-173">Nesse modo, o aplicativo não receberá mensagens da fila; ele somente as enviará.</span><span class="sxs-lookup"><span data-stu-id="ad36e-173">In this mode, the application will not receive messages from the queue, it will only send.</span></span>
* <span data-ttu-id="ad36e-174">Pressione **Enter** algumas vezes no console do aplicativo Java; isso fará com que as mensagens sejam enviadas.</span><span class="sxs-lookup"><span data-stu-id="ad36e-174">Press **Enter** a few times in the Java application console, which will cause messages to be sent.</span></span>
* <span data-ttu-id="ad36e-175">Essas mensagens são recebidas pelo aplicativo .NET.</span><span class="sxs-lookup"><span data-stu-id="ad36e-175">These messages are received by the .NET application.</span></span>

#### <a name="output-from-jms-application"></a><span data-ttu-id="ad36e-176">Saída do aplicativo JMS</span><span class="sxs-lookup"><span data-stu-id="ad36e-176">Output from JMS application</span></span>
```
> java SimpleSenderReceiver sendonly
Press [enter] to send a message. Type 'exit' + [enter] to quit.
Sent message with JMSMessageID = ID:4364096528752411591
Sent message with JMSMessageID = ID:459252991689389983
Sent message with JMSMessageID = ID:1565011046230456854
exit
```

#### <a name="output-from-net-application"></a><span data-ttu-id="ad36e-177">Saída do aplicativo .NET</span><span class="sxs-lookup"><span data-stu-id="ad36e-177">Output from .NET application</span></span>
```
> SimpleSenderReceiver.exe    
Press [enter] to send a message. Type 'exit' + [enter] to quit.
Received message with MessageID = 4364096528752411591
Received message with MessageID = 459252991689389983
Received message with MessageID = 1565011046230456854
exit
```

### <a name="net-to-jms"></a><span data-ttu-id="ad36e-178">Do .NET para o JMS</span><span class="sxs-lookup"><span data-stu-id="ad36e-178">.NET to JMS</span></span>
<span data-ttu-id="ad36e-179">Para demonstrar as mensagens do .NET para o JMS:</span><span class="sxs-lookup"><span data-stu-id="ad36e-179">To demonstrate .NET to JMS messaging:</span></span>

* <span data-ttu-id="ad36e-180">Inicie a amostra do aplicativo do .NET com o argumento de linha de comando "sendonly".</span><span class="sxs-lookup"><span data-stu-id="ad36e-180">Start the .NET sample application with the "sendonly" command-line argument.</span></span> <span data-ttu-id="ad36e-181">Nesse modo, o aplicativo não receberá mensagens da fila; ele somente as enviará.</span><span class="sxs-lookup"><span data-stu-id="ad36e-181">In this mode, the application will not receive messages from the queue, it will only send.</span></span>
* <span data-ttu-id="ad36e-182">Inicie a amostra do aplicativo do Java sem nenhum argumento de linha de comando.</span><span class="sxs-lookup"><span data-stu-id="ad36e-182">Start the Java sample application without any command-line arguments.</span></span>
* <span data-ttu-id="ad36e-183">Pressione **Enter** algumas vezes no console do aplicativo .NET, isso fará com que as mensagens sejam enviadas.</span><span class="sxs-lookup"><span data-stu-id="ad36e-183">Press **Enter** a few times in the .NET application console, which will cause messages to be sent.</span></span>
* <span data-ttu-id="ad36e-184">Essas mensagens são recebidas pelo aplicativo Java.</span><span class="sxs-lookup"><span data-stu-id="ad36e-184">These messages are received by the Java application.</span></span>

#### <a name="output-from-net-application"></a><span data-ttu-id="ad36e-185">Saída do aplicativo .NET</span><span class="sxs-lookup"><span data-stu-id="ad36e-185">Output from .NET application</span></span>
```
> SimpleSenderReceiver.exe sendonly
Press [enter] to send a message. Type 'exit' + [enter] to quit.
Sent message with MessageID = d64e681a310a48a1ae0ce7b017bf1cf3    
Sent message with MessageID = 98a39664995b4f74b32e2a0ecccc46bb
Sent message with MessageID = acbca67f03c346de9b7893026f97ddeb
exit
```

#### <a name="output-from-jms-application"></a><span data-ttu-id="ad36e-186">Saída do aplicativo JMS</span><span class="sxs-lookup"><span data-stu-id="ad36e-186">Output from JMS application</span></span>
```
> java SimpleSenderReceiver    
Press [enter] to send a message. Type 'exit' + [enter] to quit.
Received message with JMSMessageID = ID:d64e681a310a48a1ae0ce7b017bf1cf3
Received message with JMSMessageID = ID:98a39664995b4f74b32e2a0ecccc46bb
Received message with JMSMessageID = ID:acbca67f03c346de9b7893026f97ddeb
exit
```

## <a name="unsupported-features-and-restrictions"></a><span data-ttu-id="ad36e-187">Restrições e recursos não suportados</span><span class="sxs-lookup"><span data-stu-id="ad36e-187">Unsupported features and restrictions</span></span>
<span data-ttu-id="ad36e-188">As restrições a seguir ocorrem durante o uso do JMS sobre o AMQP 1.0 com o Service Bus, ou seja:</span><span class="sxs-lookup"><span data-stu-id="ad36e-188">The following restrictions exist when using JMS over AMQP 1.0 with Service Bus, namely:</span></span>

* <span data-ttu-id="ad36e-189">Apenas um **MessageProducer** ou **MessageConsumer** é permitido por **Sessão**.</span><span class="sxs-lookup"><span data-stu-id="ad36e-189">Only one **MessageProducer** or **MessageConsumer** is allowed per **Session**.</span></span> <span data-ttu-id="ad36e-190">Se precisar criar vários **MessageProducers** ou **MessageConsumers** em um aplicativo, crie uma **Session** dedicada para cada um deles.</span><span class="sxs-lookup"><span data-stu-id="ad36e-190">If you need to create multiple **MessageProducers** or **MessageConsumers** in an application, create a dedicated **Session** for each of them.</span></span>
* <span data-ttu-id="ad36e-191">Assinaturas de tópico voláteis não são atualmente suportadas.</span><span class="sxs-lookup"><span data-stu-id="ad36e-191">Volatile topic subscriptions are not currently supported.</span></span>
* <span data-ttu-id="ad36e-192">**MessageSelectors** não são atualmente suportados.</span><span class="sxs-lookup"><span data-stu-id="ad36e-192">**MessageSelectors** are not currently supported.</span></span>
* <span data-ttu-id="ad36e-193">Os destinos temporários como, por exemplo, **TemporaryQueue**, **TemporaryTopic** não têm suporte no momento, juntamente com as APIs de **QueueRequestor** e **TopicRequestor** que os utilizam.</span><span class="sxs-lookup"><span data-stu-id="ad36e-193">Temporary destinations; for example, **TemporaryQueue**, **TemporaryTopic** are not currently supported, along with the **QueueRequestor** and **TopicRequestor** APIs that use them.</span></span>
* <span data-ttu-id="ad36e-194">Não há suporte para as sessões transacionadas e transações distribuídas.</span><span class="sxs-lookup"><span data-stu-id="ad36e-194">Transacted sessions and distributed transactions are not supported.</span></span>

## <a name="summary"></a><span data-ttu-id="ad36e-195">Resumo</span><span class="sxs-lookup"><span data-stu-id="ad36e-195">Summary</span></span>
<span data-ttu-id="ad36e-196">Este guia de instruções explicou como usar os recursos do sistema de mensagens agenciado do Barramento de Serviço (tópicos sobre filas e publicação/assinatura) do Java usando a API popular JMS e o AMQP 1.0.</span><span class="sxs-lookup"><span data-stu-id="ad36e-196">This how-to guide showed how to use Service Bus brokered messaging features (queues and publish/subscribe topics) from Java using the popular JMS API and AMQP 1.0.</span></span>

<span data-ttu-id="ad36e-197">Você também pode usar o AMQP 1.0 do Service Bus de outras linguagens, incluindo .NET, C, Python e PHP.</span><span class="sxs-lookup"><span data-stu-id="ad36e-197">You can also use Service Bus AMQP 1.0 from other languages, including .NET, C, Python, and PHP.</span></span> <span data-ttu-id="ad36e-198">Os componentes criados com essas diferentes linguagens podem trocar mensagens de forma confiável e com total fidelidade usando o suporte do AMQP 1.0 no Service Bus.</span><span class="sxs-lookup"><span data-stu-id="ad36e-198">Components built using these different languages can exchange messages reliably and at full fidelity using the AMQP 1.0 support in Service Bus.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ad36e-199">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ad36e-199">Next steps</span></span>
* [<span data-ttu-id="ad36e-200">Suporte para o AMQP 1.0 no Barramento de Serviço do Azure</span><span class="sxs-lookup"><span data-stu-id="ad36e-200">AMQP 1.0 support in Azure Service Bus</span></span>](service-bus-amqp-overview.md)
* [<span data-ttu-id="ad36e-201">Como usar o AMQP 1.0 com a API .NET do Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="ad36e-201">How to use AMQP 1.0 with the Service Bus .NET API</span></span>](service-bus-dotnet-advanced-message-queuing.md)
* [<span data-ttu-id="ad36e-202">Guia do Desenvolvedor do AMQP 1.0 do Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="ad36e-202">Service Bus AMQP 1.0 Developer's Guide</span></span>](service-bus-amqp-dotnet.md)
* [<span data-ttu-id="ad36e-203">Introdução às filas do Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="ad36e-203">Get started with Service Bus queues</span></span>](service-bus-dotnet-get-started-with-queues.md)
* [<span data-ttu-id="ad36e-204">Centro de Desenvolvedores do Java</span><span class="sxs-lookup"><span data-stu-id="ad36e-204">Java Developer Center</span></span>](https://azure.microsoft.com/develop/java/)

