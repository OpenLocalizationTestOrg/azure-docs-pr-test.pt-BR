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
# <a name="how-toouse-hello-java-message-service-jms-api-with-service-bus-and-amqp-10"></a><span data-ttu-id="2fce2-103">Como toouse Olá serviço JMS (Java Message) API com AMQP 1.0 e o barramento de serviço</span><span class="sxs-lookup"><span data-stu-id="2fce2-103">How toouse hello Java Message Service (JMS) API with Service Bus and AMQP 1.0</span></span>
<span data-ttu-id="2fce2-104">Olá Advanced Message Queuing Protocol (AMQP) 1.0 é um protocolo de mensagens eficiente, confiável e de nível de transmissão que você pode usar aplicativos de mensagens robusto e de plataforma cruzada toobuild.</span><span class="sxs-lookup"><span data-stu-id="2fce2-104">hello Advanced Message Queuing Protocol (AMQP) 1.0 is an efficient, reliable, wire-level messaging protocol that you can use toobuild robust, cross-platform messaging applications.</span></span>

<span data-ttu-id="2fce2-105">Suporte para AMQP 1.0 no barramento de serviço significa que você pode usar Olá enfileiramento e publica/assina recursos de mensagens orientados de uma variedade de plataformas usando um protocolo binário eficiente.</span><span class="sxs-lookup"><span data-stu-id="2fce2-105">Support for AMQP 1.0 in Service Bus means that you can use hello queuing and publish/subscribe brokered messaging features from a range of platforms using an efficient binary protocol.</span></span> <span data-ttu-id="2fce2-106">Além disso, você pode criar aplicativos formados por componentes criados com o uso de uma mistura de linguagens, estruturas e sistemas operacionais.</span><span class="sxs-lookup"><span data-stu-id="2fce2-106">Furthermore, you can build applications comprised of components built using a mix of languages, frameworks, and operating systems.</span></span>

<span data-ttu-id="2fce2-107">Este artigo explica como toouse Service Bus recursos de mensagens (filas e a publicação/assinatura tópicos) de aplicativos Java usando Olá populares serviço JMS (Java Message) API padrão.</span><span class="sxs-lookup"><span data-stu-id="2fce2-107">This article explains how toouse Service Bus messaging features (queues and publish/subscribe topics) from Java applications using hello popular Java Message Service (JMS) API standard.</span></span> <span data-ttu-id="2fce2-108">Há um [artigo complementar](service-bus-amqp-dotnet.md) que explica como toodo Olá mesmo usando Olá API .NET do barramento de serviço.</span><span class="sxs-lookup"><span data-stu-id="2fce2-108">There is a [companion article](service-bus-amqp-dotnet.md) that explains how toodo hello same using hello Service Bus .NET API.</span></span> <span data-ttu-id="2fce2-109">Você pode usar esses toolearn juntos de duas guias sobre mensagens de plataforma cruzada usando AMQP 1.0.</span><span class="sxs-lookup"><span data-stu-id="2fce2-109">You can use these two guides together toolearn about cross-platform messaging using AMQP 1.0.</span></span>

## <a name="get-started-with-service-bus"></a><span data-ttu-id="2fce2-110">Introdução ao Barramento de serviço</span><span class="sxs-lookup"><span data-stu-id="2fce2-110">Get started with Service Bus</span></span>
<span data-ttu-id="2fce2-111">Este guia presume que você já tenha um namespace do Barramento de Serviço que contém uma fila denominada **queue1**.</span><span class="sxs-lookup"><span data-stu-id="2fce2-111">This guide assumes that you already have a Service Bus namespace containing a queue named **queue1**.</span></span> <span data-ttu-id="2fce2-112">Se você não fizer isso, você pode [criar namespace hello e fila](service-bus-create-namespace-portal.md) usando Olá [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2fce2-112">If you do not, then you can [create hello namespace and queue](service-bus-create-namespace-portal.md) using hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="2fce2-113">Para obter mais informações sobre como toocreate namespaces de barramento de serviço e as filas, consulte [começar com filas do barramento de serviço](service-bus-dotnet-get-started-with-queues.md).</span><span class="sxs-lookup"><span data-stu-id="2fce2-113">For more information about how toocreate Service Bus namespaces and queues, see [Get started with Service Bus queues](service-bus-dotnet-get-started-with-queues.md).</span></span>

> [!NOTE]
> <span data-ttu-id="2fce2-114">Filas e tópicos particionados também dão suporte ao AMQP.</span><span class="sxs-lookup"><span data-stu-id="2fce2-114">Partitioned queues and topics also support AMQP.</span></span> <span data-ttu-id="2fce2-115">Para saber mais, confira [Entidades de mensagens particionadas](service-bus-partitioning.md) e [Suporte a AMQP 1.0 para filas e tópicos particionados do Barramento de Serviço](service-bus-partitioned-queues-and-topics-amqp-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2fce2-115">For more information, see [Partitioned messaging entities](service-bus-partitioning.md) and [AMQP 1.0 support for Service Bus partitioned queues and topics](service-bus-partitioned-queues-and-topics-amqp-overview.md).</span></span>
> 
> 

## <a name="downloading-hello-amqp-10-jms-client-library"></a><span data-ttu-id="2fce2-116">Baixando a biblioteca de cliente do AMQP 1.0 JMS Olá</span><span class="sxs-lookup"><span data-stu-id="2fce2-116">Downloading hello AMQP 1.0 JMS client library</span></span>
<span data-ttu-id="2fce2-117">Para obter informações sobre onde toodownload Olá a versão mais recente da biblioteca de cliente Olá Apache Qpid JMS AMQP 1.0, visite [https://qpid.apache.org/download.html](https://qpid.apache.org/download.html).</span><span class="sxs-lookup"><span data-stu-id="2fce2-117">For information about where toodownload hello latest version of hello Apache Qpid JMS AMQP 1.0 client library, visit [https://qpid.apache.org/download.html](https://qpid.apache.org/download.html).</span></span>

<span data-ttu-id="2fce2-118">Você deve adicionar Olá quatro arquivos JAR a seguir de saudação Apache Qpid JMS AMQP 1.0 distribuição arquivamento toohello CLASSPATH Java ao compilar e executar aplicativos do JMS com o barramento de serviço:</span><span class="sxs-lookup"><span data-stu-id="2fce2-118">You must add hello following four JAR files from hello Apache Qpid JMS AMQP 1.0 distribution archive toohello Java CLASSPATH when building and running JMS applications with Service Bus:</span></span>

* <span data-ttu-id="2fce2-119">geronimo-jms\_1.1\_spec-1.0.jar</span><span class="sxs-lookup"><span data-stu-id="2fce2-119">geronimo-jms\_1.1\_spec-1.0.jar</span></span>
* <span data-ttu-id="2fce2-120">qpid-amqp-1-0-client-[version].jar</span><span class="sxs-lookup"><span data-stu-id="2fce2-120">qpid-amqp-1-0-client-[version].jar</span></span>
* <span data-ttu-id="2fce2-121">qpid-amqp-1-0-client-jms-[version].jar</span><span class="sxs-lookup"><span data-stu-id="2fce2-121">qpid-amqp-1-0-client-jms-[version].jar</span></span>
* <span data-ttu-id="2fce2-122">qpid-amqp-1-0-common-[version].jar</span><span class="sxs-lookup"><span data-stu-id="2fce2-122">qpid-amqp-1-0-common-[version].jar</span></span>

## <a name="coding-java-applications"></a><span data-ttu-id="2fce2-123">Codificando os aplicativos Java</span><span class="sxs-lookup"><span data-stu-id="2fce2-123">Coding Java applications</span></span>
### <a name="java-naming-and-directory-interface-jndi"></a><span data-ttu-id="2fce2-124">Java Naming and Directory Interface (JNDI)</span><span class="sxs-lookup"><span data-stu-id="2fce2-124">Java Naming and Directory Interface (JNDI)</span></span>
<span data-ttu-id="2fce2-125">O JMS utiliza Olá Java Naming and Directory Interface (JNDI) toocreate uma separação entre nomes lógicos e físicos.</span><span class="sxs-lookup"><span data-stu-id="2fce2-125">JMS uses hello Java Naming and Directory Interface (JNDI) toocreate a separation between logical names and physical names.</span></span> <span data-ttu-id="2fce2-126">Dois tipos de objetos JMS são resolvidos usando a JNDI: ConnectionFactory e Destino.</span><span class="sxs-lookup"><span data-stu-id="2fce2-126">Two types of JMS objects are resolved using JNDI: ConnectionFactory and Destination.</span></span> <span data-ttu-id="2fce2-127">O JNDI utiliza um modelo de provedor para o qual você pode conectar tarefas de resolução de nome do diretório diferentes serviços toohandle.</span><span class="sxs-lookup"><span data-stu-id="2fce2-127">JNDI uses a provider model into which you can plug different directory services toohandle name resolution duties.</span></span> <span data-ttu-id="2fce2-128">Olá Apache Qpid JMS AMQP 1.0 biblioteca vem com um simples propriedades provedor JNDI baseado em arquivo que é configurado usando um arquivo de propriedades do seguinte Olá formato:</span><span class="sxs-lookup"><span data-stu-id="2fce2-128">hello Apache Qpid JMS AMQP 1.0 library comes with a simple properties file-based JNDI Provider that is configured using a properties file of hello following format:</span></span>

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

#### <a name="configure-hello-connectionfactory"></a><span data-ttu-id="2fce2-129">Configurar Olá ConnectionFactory</span><span class="sxs-lookup"><span data-stu-id="2fce2-129">Configure hello ConnectionFactory</span></span>
<span data-ttu-id="2fce2-130">Olá toodefine de entrada usado um **ConnectionFactory** Olá Qpid provedor JNDI de propriedades de arquivo é do hello formato a seguir:</span><span class="sxs-lookup"><span data-stu-id="2fce2-130">hello entry used toodefine a **ConnectionFactory** in hello Qpid properties file JNDI provider is of hello following format:</span></span>

```
connectionfactory.[jndi_name] = [ConnectionURL]
```

<span data-ttu-id="2fce2-131">Onde **[jndi_name]** e **[ConnectionURL]** ter Olá significados a seguir:</span><span class="sxs-lookup"><span data-stu-id="2fce2-131">Where **[jndi_name]** and **[ConnectionURL]** have hello following meanings:</span></span>

* <span data-ttu-id="2fce2-132">**[jndi_name]** : nome lógico Olá Olá ConnectionFactory.</span><span class="sxs-lookup"><span data-stu-id="2fce2-132">**[jndi_name]**: hello logical name of hello ConnectionFactory.</span></span> <span data-ttu-id="2fce2-133">Este é o nome de saudação que será resolvido no aplicativo de Java hello usando o método de JNDI Intialcontext hello.</span><span class="sxs-lookup"><span data-stu-id="2fce2-133">This is hello name that will be resolved in hello Java application using hello JNDI IntialContext.lookup() method.</span></span>
* <span data-ttu-id="2fce2-134">**[ConnectionURL]** : Uma URL que fornece biblioteca JMS Olá Olá informações necessárias toohello agente AMQP.</span><span class="sxs-lookup"><span data-stu-id="2fce2-134">**[ConnectionURL]**: A URL that provides hello JMS library with hello information required toohello AMQP broker.</span></span>

<span data-ttu-id="2fce2-135">formato de saudação do hello **ConnectionURL** é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="2fce2-135">hello format of hello **ConnectionURL** is as follows:</span></span>

```
amqps://[SASPolicyName]:[SASPolicyKey]@[namespace].servicebus.windows.net
```
<span data-ttu-id="2fce2-136">Onde **[namespace]**, **[SASPolicyName]** e **[SASPolicyKey]** ter Olá significados a seguir:</span><span class="sxs-lookup"><span data-stu-id="2fce2-136">Where **[namespace]**, **[SASPolicyName]** and **[SASPolicyKey]** have hello following meanings:</span></span>

* <span data-ttu-id="2fce2-137">**[namespace]** : Olá namespace de barramento de serviço.</span><span class="sxs-lookup"><span data-stu-id="2fce2-137">**[namespace]**: hello Service Bus namespace.</span></span>
* <span data-ttu-id="2fce2-138">**[SASPolicyName]** : nome de diretiva de assinatura de acesso compartilhado da fila de saudação.</span><span class="sxs-lookup"><span data-stu-id="2fce2-138">**[SASPolicyName]**: hello Queue Shared Access Signature policy name.</span></span>
* <span data-ttu-id="2fce2-139">**[SASPolicyKey]** : chave de política de assinatura de acesso compartilhado da fila de saudação.</span><span class="sxs-lookup"><span data-stu-id="2fce2-139">**[SASPolicyKey]**: hello Queue Shared Access Signature policy key.</span></span>

> [!NOTE]
> <span data-ttu-id="2fce2-140">Você deve codificar URL senha de saudação manualmente.</span><span class="sxs-lookup"><span data-stu-id="2fce2-140">You must URL-encode hello password manually.</span></span> <span data-ttu-id="2fce2-141">Um utilitário útil de codificação de URL está disponível em [http://www.w3schools.com/tags/ref_urlencode.asp](http://www.w3schools.com/tags/ref_urlencode.asp).</span><span class="sxs-lookup"><span data-stu-id="2fce2-141">A useful URL-encoding utility is available at [http://www.w3schools.com/tags/ref_urlencode.asp](http://www.w3schools.com/tags/ref_urlencode.asp).</span></span>
> 
> 

#### <a name="configure-destinations"></a><span data-ttu-id="2fce2-142">Configurar destinos</span><span class="sxs-lookup"><span data-stu-id="2fce2-142">Configure destinations</span></span>
<span data-ttu-id="2fce2-143">Olá toodefine de entrada usada que é um destino no provedor JNDI de arquivos de propriedades do hello Qpid do hello formato a seguir:</span><span class="sxs-lookup"><span data-stu-id="2fce2-143">hello entry used toodefine a destination in hello Qpid properties file JNDI provider is of hello following format:</span></span>

```
queue.[jndi_name] = [physical_name]
```

<span data-ttu-id="2fce2-144">ou o</span><span class="sxs-lookup"><span data-stu-id="2fce2-144">or</span></span>

```
topic.[jndi_name] = [physical_name]
```

<span data-ttu-id="2fce2-145">Onde **[jndi\_nome]** e **[físico\_nome]** ter Olá significados a seguir:</span><span class="sxs-lookup"><span data-stu-id="2fce2-145">Where **[jndi\_name]** and **[physical\_name]** have hello following meanings:</span></span>

* <span data-ttu-id="2fce2-146">**[jndi_name]** : nome lógico de saudação do destino de saudação.</span><span class="sxs-lookup"><span data-stu-id="2fce2-146">**[jndi_name]**: hello logical name of hello destination.</span></span> <span data-ttu-id="2fce2-147">Este é o nome de saudação que será resolvido no aplicativo de Java hello usando o método de JNDI Intialcontext hello.</span><span class="sxs-lookup"><span data-stu-id="2fce2-147">This is hello name that will be resolved in hello Java application using hello JNDI IntialContext.lookup() method.</span></span>
* <span data-ttu-id="2fce2-148">**[physical_name]** : nome de saudação do hello aplicativo hello do barramento de serviço entidade toowhich envia ou recebe mensagens.</span><span class="sxs-lookup"><span data-stu-id="2fce2-148">**[physical_name]**: hello name of hello Service Bus entity toowhich hello application sends or receives messages.</span></span>

> [!NOTE]
> <span data-ttu-id="2fce2-149">Durante o recebimento de uma assinatura de tópico do barramento de serviço, nome físico do hello especificado no JNDI deve ser o nome de saudação do tópico de saudação.</span><span class="sxs-lookup"><span data-stu-id="2fce2-149">When receiving from a Service Bus topic subscription, hello physical name specified in JNDI should be hello name of hello topic.</span></span> <span data-ttu-id="2fce2-150">nome da assinatura Olá é fornecida quando a assinatura durável Olá é criada no código do aplicativo JMS de saudação.</span><span class="sxs-lookup"><span data-stu-id="2fce2-150">hello subscription name is provided when hello durable subscription is created in hello JMS application code.</span></span> <span data-ttu-id="2fce2-151">Olá [guia do desenvolvedor do Service Bus AMQP 1.0](service-bus-amqp-dotnet.md) fornece mais detalhes sobre como trabalhar com tópicos do barramento de serviço do JMS.</span><span class="sxs-lookup"><span data-stu-id="2fce2-151">hello [Service Bus AMQP 1.0 Developer's Guide](service-bus-amqp-dotnet.md) provides more details on working with Service Bus topics from JMS.</span></span>
> 
> 

### <a name="write-hello-jms-application"></a><span data-ttu-id="2fce2-152">Gravar saudação JMS aplicativo</span><span class="sxs-lookup"><span data-stu-id="2fce2-152">Write hello JMS application</span></span>
<span data-ttu-id="2fce2-153">Não existem APIs ou opções especiais obrigatórias ao usar o JMS com o Service Bus.</span><span class="sxs-lookup"><span data-stu-id="2fce2-153">There are no special APIs or options required when using JMS with Service Bus.</span></span> <span data-ttu-id="2fce2-154">No entanto, existem algumas restrições que serão abordadas posteriormente.</span><span class="sxs-lookup"><span data-stu-id="2fce2-154">However, there are a few restrictions that will be covered later.</span></span> <span data-ttu-id="2fce2-155">Assim como com qualquer aplicativo JMS, Olá a primeira coisa exigida é configuração do ambiente de JNDI hello, tooresolve capaz de toobe um **ConnectionFactory** e destinos.</span><span class="sxs-lookup"><span data-stu-id="2fce2-155">As with any JMS application, hello first thing required is configuration of hello JNDI environment, toobe able tooresolve a **ConnectionFactory** and destinations.</span></span>

#### <a name="configure-hello-jndi-initialcontext"></a><span data-ttu-id="2fce2-156">Configurar Olá JNDI InitialContext</span><span class="sxs-lookup"><span data-stu-id="2fce2-156">Configure hello JNDI InitialContext</span></span>
<span data-ttu-id="2fce2-157">ambiente de JNDI Hello está configurado, passando uma tabela de hash das informações de configuração no construtor de saudação da classe de javax.naming.InitialContext hello.</span><span class="sxs-lookup"><span data-stu-id="2fce2-157">hello JNDI environment is configured by passing a hashtable of configuration information into hello constructor of hello javax.naming.InitialContext class.</span></span> <span data-ttu-id="2fce2-158">dois elementos necessários Olá na tabela de hash de saudação são nome da classe Olá da saudação inicial fábrica de contexto e hello URL do provedor.</span><span class="sxs-lookup"><span data-stu-id="2fce2-158">hello two required elements in hello hashtable are hello class name of hello Initial Context Factory and hello Provider URL.</span></span> <span data-ttu-id="2fce2-159">Olá código a seguir mostra como tooconfigure Olá JNDI ambiente toouse Olá Qpid propriedades baseado em arquivo provedor JNDI com um arquivo de propriedades denominado **ServiceBus**.</span><span class="sxs-lookup"><span data-stu-id="2fce2-159">hello following code shows how tooconfigure hello JNDI environment toouse hello Qpid properties file based JNDI Provider with a properties file named **servicebus.properties**.</span></span>

```java
Hashtable<String, String> env = new Hashtable<String, String>(); 
env.put(Context.INITIAL_CONTEXT_FACTORY, "org.apache.qpid.amqp_1_0.jms.jndi.PropertiesFileInitialContextFactory"); 
env.put(Context.PROVIDER_URL, "servicebus.properties"); 
InitialContext context = new InitialContext(env);
``` 

### <a name="a-simple-jms-application-using-a-service-bus-queue"></a><span data-ttu-id="2fce2-160">Um aplicativo JMS simples que usa uma fila do Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="2fce2-160">A simple JMS application using a Service Bus queue</span></span>
<span data-ttu-id="2fce2-161">Hello programa de exemplo a seguir envia a fila de barramento de serviço do JMS TextMessages tooa com nome lógico do hello JNDI da fila e recebe mensagens de saudação novamente.</span><span class="sxs-lookup"><span data-stu-id="2fce2-161">hello following example program sends JMS TextMessages tooa Service Bus queue with hello JNDI logical name of QUEUE, and receives hello messages back.</span></span>

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

### <a name="run-hello-application"></a><span data-ttu-id="2fce2-162">Executar o aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="2fce2-162">Run hello application</span></span>
<span data-ttu-id="2fce2-163">Executar o aplicativo hello produz saída de formulário de saudação:</span><span class="sxs-lookup"><span data-stu-id="2fce2-163">Running hello application produces output of hello form:</span></span>

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

## <a name="cross-platform-messaging-between-jms-and-net"></a><span data-ttu-id="2fce2-164">Mensagens em plataformas cruzadas entre JMS e .NET</span><span class="sxs-lookup"><span data-stu-id="2fce2-164">Cross-platform messaging between JMS and .NET</span></span>
<span data-ttu-id="2fce2-165">Este guia mostrado como toosend e receber mensagens tooand do barramento de serviço usando JMS.</span><span class="sxs-lookup"><span data-stu-id="2fce2-165">This guide showed how toosend and receive messages tooand from Service Bus using JMS.</span></span> <span data-ttu-id="2fce2-166">No entanto, um dos principais benefícios de saudação do AMQP 1.0 é que ele permite que aplicativos toobe criada a partir de componentes escritos em idiomas diferentes, com mensagens trocadas confiável e com fidelidade total.</span><span class="sxs-lookup"><span data-stu-id="2fce2-166">However, one of hello key benefits of AMQP 1.0 is that it enables applications toobe built from components written in different languages, with messages exchanged reliably and at full fidelity.</span></span>

<span data-ttu-id="2fce2-167">Usando o aplicativo de JMS do exemplo hello descrito acima e um aplicativo .NET semelhante obtido um artigo complementar, [usando o barramento de serviço do .NET com AMQP 1.0](service-bus-amqp-dotnet.md), você pode trocar mensagens entre .NET e Java.</span><span class="sxs-lookup"><span data-stu-id="2fce2-167">Using hello sample JMS application described above and a similar .NET application taken from a companion article, [Using Service Bus from .NET with AMQP 1.0](service-bus-amqp-dotnet.md), you can exchange messages between .NET and Java.</span></span> <span data-ttu-id="2fce2-168">Leia este artigo para obter mais informações sobre detalhes de saudação da plataforma cruzada usando AMQP 1.0 e o barramento de serviço do sistema de mensagens.</span><span class="sxs-lookup"><span data-stu-id="2fce2-168">Read this article for more information about hello details of cross-platform messaging using Service Bus and AMQP 1.0.</span></span>

### <a name="jms-toonet"></a><span data-ttu-id="2fce2-169">Too.NET JMS</span><span class="sxs-lookup"><span data-stu-id="2fce2-169">JMS too.NET</span></span>
<span data-ttu-id="2fce2-170">toodemonstrate JMS too.NET mensagens:</span><span class="sxs-lookup"><span data-stu-id="2fce2-170">toodemonstrate JMS too.NET messaging:</span></span>

* <span data-ttu-id="2fce2-171">Inicie o aplicativo de exemplo .NET hello sem argumentos de linha de comando.</span><span class="sxs-lookup"><span data-stu-id="2fce2-171">Start hello .NET sample application without any command-line arguments.</span></span>
* <span data-ttu-id="2fce2-172">Inicie o aplicativo de exemplo hello Java com argumento de linha de comando do hello "sendonly".</span><span class="sxs-lookup"><span data-stu-id="2fce2-172">Start hello Java sample application with hello "sendonly" command-line argument.</span></span> <span data-ttu-id="2fce2-173">Nesse modo, hello aplicativo não receberá mensagens da fila de hello, ele enviará apenas.</span><span class="sxs-lookup"><span data-stu-id="2fce2-173">In this mode, hello application will not receive messages from hello queue, it will only send.</span></span>
* <span data-ttu-id="2fce2-174">Pressione **Enter** algumas vezes no console de aplicativos do Java hello, que fará com que toobe de mensagens enviada.</span><span class="sxs-lookup"><span data-stu-id="2fce2-174">Press **Enter** a few times in hello Java application console, which will cause messages toobe sent.</span></span>
* <span data-ttu-id="2fce2-175">Essas mensagens são recebidas pelo Olá aplicativo .NET.</span><span class="sxs-lookup"><span data-stu-id="2fce2-175">These messages are received by hello .NET application.</span></span>

#### <a name="output-from-jms-application"></a><span data-ttu-id="2fce2-176">Saída do aplicativo JMS</span><span class="sxs-lookup"><span data-stu-id="2fce2-176">Output from JMS application</span></span>
```
> java SimpleSenderReceiver sendonly
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.
Sent message with JMSMessageID = ID:4364096528752411591
Sent message with JMSMessageID = ID:459252991689389983
Sent message with JMSMessageID = ID:1565011046230456854
exit
```

#### <a name="output-from-net-application"></a><span data-ttu-id="2fce2-177">Saída do aplicativo .NET</span><span class="sxs-lookup"><span data-stu-id="2fce2-177">Output from .NET application</span></span>
```
> SimpleSenderReceiver.exe    
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.
Received message with MessageID = 4364096528752411591
Received message with MessageID = 459252991689389983
Received message with MessageID = 1565011046230456854
exit
```

### <a name="net-toojms"></a><span data-ttu-id="2fce2-178">TooJMS .NET</span><span class="sxs-lookup"><span data-stu-id="2fce2-178">.NET tooJMS</span></span>
<span data-ttu-id="2fce2-179">toodemonstrate tooJMS de .NET do sistema de mensagens:</span><span class="sxs-lookup"><span data-stu-id="2fce2-179">toodemonstrate .NET tooJMS messaging:</span></span>

* <span data-ttu-id="2fce2-180">Inicie o aplicativo de exemplo .NET hello com argumento de linha de comando do hello "sendonly".</span><span class="sxs-lookup"><span data-stu-id="2fce2-180">Start hello .NET sample application with hello "sendonly" command-line argument.</span></span> <span data-ttu-id="2fce2-181">Nesse modo, hello aplicativo não receberá mensagens da fila de hello, ele enviará apenas.</span><span class="sxs-lookup"><span data-stu-id="2fce2-181">In this mode, hello application will not receive messages from hello queue, it will only send.</span></span>
* <span data-ttu-id="2fce2-182">Inicie o aplicativo de exemplo hello Java sem argumentos de linha de comando.</span><span class="sxs-lookup"><span data-stu-id="2fce2-182">Start hello Java sample application without any command-line arguments.</span></span>
* <span data-ttu-id="2fce2-183">Pressione **Enter** algumas vezes no console de aplicativo do .NET hello, que fará com que toobe de mensagens enviada.</span><span class="sxs-lookup"><span data-stu-id="2fce2-183">Press **Enter** a few times in hello .NET application console, which will cause messages toobe sent.</span></span>
* <span data-ttu-id="2fce2-184">Essas mensagens são recebidas pelo Olá aplicativo Java.</span><span class="sxs-lookup"><span data-stu-id="2fce2-184">These messages are received by hello Java application.</span></span>

#### <a name="output-from-net-application"></a><span data-ttu-id="2fce2-185">Saída do aplicativo .NET</span><span class="sxs-lookup"><span data-stu-id="2fce2-185">Output from .NET application</span></span>
```
> SimpleSenderReceiver.exe sendonly
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.
Sent message with MessageID = d64e681a310a48a1ae0ce7b017bf1cf3    
Sent message with MessageID = 98a39664995b4f74b32e2a0ecccc46bb
Sent message with MessageID = acbca67f03c346de9b7893026f97ddeb
exit
```

#### <a name="output-from-jms-application"></a><span data-ttu-id="2fce2-186">Saída do aplicativo JMS</span><span class="sxs-lookup"><span data-stu-id="2fce2-186">Output from JMS application</span></span>
```
> java SimpleSenderReceiver    
Press [enter] toosend a message. Type 'exit' + [enter] tooquit.
Received message with JMSMessageID = ID:d64e681a310a48a1ae0ce7b017bf1cf3
Received message with JMSMessageID = ID:98a39664995b4f74b32e2a0ecccc46bb
Received message with JMSMessageID = ID:acbca67f03c346de9b7893026f97ddeb
exit
```

## <a name="unsupported-features-and-restrictions"></a><span data-ttu-id="2fce2-187">Restrições e recursos não suportados</span><span class="sxs-lookup"><span data-stu-id="2fce2-187">Unsupported features and restrictions</span></span>
<span data-ttu-id="2fce2-188">Olá restrições a seguir existe ao usar JMS no AMQP 1.0 com o barramento de serviço, ou seja:</span><span class="sxs-lookup"><span data-stu-id="2fce2-188">hello following restrictions exist when using JMS over AMQP 1.0 with Service Bus, namely:</span></span>

* <span data-ttu-id="2fce2-189">Apenas um **MessageProducer** ou **MessageConsumer** é permitido por **Sessão**.</span><span class="sxs-lookup"><span data-stu-id="2fce2-189">Only one **MessageProducer** or **MessageConsumer** is allowed per **Session**.</span></span> <span data-ttu-id="2fce2-190">Se você precisar toocreate vários **MessageProducers** ou **MessageConsumers** em um aplicativo, crie um dedicado **sessão** para cada um deles.</span><span class="sxs-lookup"><span data-stu-id="2fce2-190">If you need toocreate multiple **MessageProducers** or **MessageConsumers** in an application, create a dedicated **Session** for each of them.</span></span>
* <span data-ttu-id="2fce2-191">Assinaturas de tópico voláteis não são atualmente suportadas.</span><span class="sxs-lookup"><span data-stu-id="2fce2-191">Volatile topic subscriptions are not currently supported.</span></span>
* <span data-ttu-id="2fce2-192">**MessageSelectors** não são atualmente suportados.</span><span class="sxs-lookup"><span data-stu-id="2fce2-192">**MessageSelectors** are not currently supported.</span></span>
* <span data-ttu-id="2fce2-193">Destinos temporários; Por exemplo, **TemporaryQueue**, **TemporaryTopic** atualmente não têm suporte, juntamente com hello **QueueRequestor** e **TopicRequestor**APIs que usá-los.</span><span class="sxs-lookup"><span data-stu-id="2fce2-193">Temporary destinations; for example, **TemporaryQueue**, **TemporaryTopic** are not currently supported, along with hello **QueueRequestor** and **TopicRequestor** APIs that use them.</span></span>
* <span data-ttu-id="2fce2-194">Não há suporte para as sessões transacionadas e transações distribuídas.</span><span class="sxs-lookup"><span data-stu-id="2fce2-194">Transacted sessions and distributed transactions are not supported.</span></span>

## <a name="summary"></a><span data-ttu-id="2fce2-195">Resumo</span><span class="sxs-lookup"><span data-stu-id="2fce2-195">Summary</span></span>
<span data-ttu-id="2fce2-196">Este tooguide como mostrou como toouse orientadas do barramento de serviço recursos de mensagens (filas e a publicação/assinatura tópicos) do Java usando Olá API de JMS populares e AMQP 1.0.</span><span class="sxs-lookup"><span data-stu-id="2fce2-196">This how-tooguide showed how toouse Service Bus brokered messaging features (queues and publish/subscribe topics) from Java using hello popular JMS API and AMQP 1.0.</span></span>

<span data-ttu-id="2fce2-197">Você também pode usar o AMQP 1.0 do Service Bus de outras linguagens, incluindo .NET, C, Python e PHP.</span><span class="sxs-lookup"><span data-stu-id="2fce2-197">You can also use Service Bus AMQP 1.0 from other languages, including .NET, C, Python, and PHP.</span></span> <span data-ttu-id="2fce2-198">Componentes desenvolvidos utilizando esses idiomas diferentes poderão trocar mensagens com segurança e fidelidade completa usando o suporte de saudação AMQP 1.0 no barramento de serviço.</span><span class="sxs-lookup"><span data-stu-id="2fce2-198">Components built using these different languages can exchange messages reliably and at full fidelity using hello AMQP 1.0 support in Service Bus.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2fce2-199">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2fce2-199">Next steps</span></span>
* [<span data-ttu-id="2fce2-200">Suporte para o AMQP 1.0 no Barramento de Serviço do Azure</span><span class="sxs-lookup"><span data-stu-id="2fce2-200">AMQP 1.0 support in Azure Service Bus</span></span>](service-bus-amqp-overview.md)
* [<span data-ttu-id="2fce2-201">Como toouse AMQP 1.0 com hello API .NET do barramento de serviço</span><span class="sxs-lookup"><span data-stu-id="2fce2-201">How toouse AMQP 1.0 with hello Service Bus .NET API</span></span>](service-bus-dotnet-advanced-message-queuing.md)
* [<span data-ttu-id="2fce2-202">Guia do Desenvolvedor do AMQP 1.0 do Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="2fce2-202">Service Bus AMQP 1.0 Developer's Guide</span></span>](service-bus-amqp-dotnet.md)
* [<span data-ttu-id="2fce2-203">Introdução às filas do Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="2fce2-203">Get started with Service Bus queues</span></span>](service-bus-dotnet-get-started-with-queues.md)
* [<span data-ttu-id="2fce2-204">Centro de Desenvolvedores do Java</span><span class="sxs-lookup"><span data-stu-id="2fce2-204">Java Developer Center</span></span>](https://azure.microsoft.com/develop/java/)

