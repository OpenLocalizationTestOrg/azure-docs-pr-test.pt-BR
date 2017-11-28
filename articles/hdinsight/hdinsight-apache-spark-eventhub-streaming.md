---
title: aaaUse Apache Spark streaming com Hubs de eventos de HDInsight do Azure | Microsoft Docs
description: Crie uma amostra de streaming do Apache Spark como toosend um dados tooAzure Hub de eventos de fluxo e receber os eventos em cluster HDInsight Spark usando um aplicativo scala.
keywords: streaming do apache spark, streaming do spark, exemplo de spark, exemplo de streaming do apache spark, exemplo do hub de evento do azure, exemplo de spark
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 68894e75-3ffa-47bd-8982-96cdad38b7d0
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: nitinme
ms.openlocfilehash: 10cc5884047b3b8249fe8a8822a16a19780a4af3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="apache-spark-streaming-process-data-from-azure-event-hubs-with-spark-cluster-on-hdinsight"></a><span data-ttu-id="ce202-104">Streaming do Apache Spark: processe dados de Hubs de Eventos do Azure com o cluster Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="ce202-104">Apache Spark streaming: Process data from Azure Event Hubs with Spark cluster on HDInsight</span></span>

<span data-ttu-id="ce202-105">Neste artigo, você deve criar um Apache Spark streaming de exemplo que envolve Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="ce202-105">In this article, you create an Apache Spark streaming sample that involves hello following steps:</span></span>

1. <span data-ttu-id="ce202-106">Você pode usar mensagens tooingest aplicativo autônomo em um Hub de eventos do Azure.</span><span class="sxs-lookup"><span data-stu-id="ce202-106">You use a standalone application tooingest messages into an Azure Event Hub.</span></span>

2. <span data-ttu-id="ce202-107">Para recuperar mensagens de saudação do Hub de eventos com duas abordagens diferentes, em tempo real usando um aplicativo em execução no cluster Spark no HDInsight do Azure.</span><span class="sxs-lookup"><span data-stu-id="ce202-107">With two different approaches, you retrieve hello messages from Event Hub in real-time using an application running in Spark cluster on Azure HDInsight.</span></span>

3. <span data-ttu-id="ce202-108">Criar pipelines analíticos streaming toopersist sistemas de armazenamento de toodifferent de dados ou obter ideias de dados em funcionamento hello.</span><span class="sxs-lookup"><span data-stu-id="ce202-108">You build streaming analytic pipelines toopersist data toodifferent storage systems, or get insights from data on hello fly.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ce202-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="ce202-109">Prerequisites</span></span>

* <span data-ttu-id="ce202-110">Uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="ce202-110">An Azure subscription.</span></span> <span data-ttu-id="ce202-111">Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="ce202-111">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

* <span data-ttu-id="ce202-112">Um cluster do Apache Spark no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ce202-112">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="ce202-113">Para obter instruções, consulte o artigo sobre como [Criar clusters do Apache Spark no Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="ce202-113">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="spark-streaming-concepts"></a><span data-ttu-id="ce202-114">Conceitos de Streaming do Spark</span><span class="sxs-lookup"><span data-stu-id="ce202-114">Spark Streaming concepts</span></span>

<span data-ttu-id="ce202-115">Para obter uma explicação detalhada do streaming Spark, veja [Visão geral do streaming do Apache Spark](http://spark.apache.org/docs/latest/streaming-programming-guide.html#overview).</span><span class="sxs-lookup"><span data-stu-id="ce202-115">For a detailed explanation of Spark streaming, see [Apache Spark streaming overview](http://spark.apache.org/docs/latest/streaming-programming-guide.html#overview).</span></span> <span data-ttu-id="ce202-116">HDInsight traz Olá cluster tooa de recursos de streaming mesmo Spark no Azure.</span><span class="sxs-lookup"><span data-stu-id="ce202-116">HDInsight brings hello same streaming features tooa Spark cluster on Azure.</span></span>  

## <a name="what-does-this-solution-do"></a><span data-ttu-id="ce202-117">O que essa solução faz?</span><span class="sxs-lookup"><span data-stu-id="ce202-117">What does this solution do?</span></span>

<span data-ttu-id="ce202-118">Neste artigo, toocreate um exemplo de streaming Spark, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="ce202-118">In this article, toocreate a Spark streaming example, perform hello following steps:</span></span>

1. <span data-ttu-id="ce202-119">Crie um Hub de Eventos do Azure que vá receber uma transmissão de eventos.</span><span class="sxs-lookup"><span data-stu-id="ce202-119">Create an Azure Event Hub that will receive a stream of events.</span></span>

2. <span data-ttu-id="ce202-120">Executar um aplicativo autônomo local que gera eventos e envia-toohello Hub de eventos do Azure.</span><span class="sxs-lookup"><span data-stu-id="ce202-120">Run a local standalone application that generates events and pushes it toohello Azure Event Hub.</span></span> <span data-ttu-id="ce202-121">aplicativo de exemplo Hello que faz isso é publicado na [https://github.com/hdinsight/spark-streaming-data-persistence-examples](https://github.com/hdinsight/spark-streaming-data-persistence-examples).</span><span class="sxs-lookup"><span data-stu-id="ce202-121">hello sample application that does this is published at [https://github.com/hdinsight/spark-streaming-data-persistence-examples](https://github.com/hdinsight/spark-streaming-data-persistence-examples).</span></span>

3. <span data-ttu-id="ce202-122">Execute um aplicativo de streaming remotamente em um cluster Spark que lê o eventos de streaming do Hub de Eventos do Azure e execute procedimentos diversos de análise/processamento de dados.</span><span class="sxs-lookup"><span data-stu-id="ce202-122">Run a streaming application remotely on a Spark cluster that reads streaming events from Azure Event Hub and perform various data processing/analysis.</span></span>

## <a name="create-an-azure-event-hub"></a><span data-ttu-id="ce202-123">Criar um Hub de Eventos do Azure</span><span class="sxs-lookup"><span data-stu-id="ce202-123">Create an Azure Event Hub</span></span>

1. <span data-ttu-id="ce202-124">Faça logon no toohello [Portal do Azure](https://ms.portal.azure.com)e clique em **novo** em Olá superior esquerda da tela hello.</span><span class="sxs-lookup"><span data-stu-id="ce202-124">Log on toohello [Azure Portal](https://ms.portal.azure.com), and click **New** at hello top left of hello screen.</span></span>

2. <span data-ttu-id="ce202-125">Clique em **Internet das Coisas** e, em seguida, clique em **Hubs de Eventos**.</span><span class="sxs-lookup"><span data-stu-id="ce202-125">Click **Internet of Things**, then click **Event Hubs**.</span></span>

    <span data-ttu-id="ce202-126">![Criar hub de eventos para exemplo de streaming do Spark](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-create-event-hub-for-spark-streaming.png "Criar hub de eventos para exemplo de streaming do Spark")</span><span class="sxs-lookup"><span data-stu-id="ce202-126">![Create event hub for Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-create-event-hub-for-spark-streaming.png "Create event hub for Spark streaming example")</span></span>

3. <span data-ttu-id="ce202-127">Em Olá **criar namespace** folha, insira um nome de namespace.</span><span class="sxs-lookup"><span data-stu-id="ce202-127">In hello **Create namespace** blade, enter a namespace name.</span></span> <span data-ttu-id="ce202-128">Escolha Olá preço (básico ou padrão).</span><span class="sxs-lookup"><span data-stu-id="ce202-128">choose hello pricing tier (Basic or Standard).</span></span> <span data-ttu-id="ce202-129">Além disso, escolha uma assinatura do Azure, o grupo de recursos e o local no qual recurso de saudação toocreate.</span><span class="sxs-lookup"><span data-stu-id="ce202-129">Also, choose an Azure subscription, resource group, and location in which toocreate hello resource.</span></span> <span data-ttu-id="ce202-130">Clique em **criar** toocreate Olá namespace.</span><span class="sxs-lookup"><span data-stu-id="ce202-130">Click **Create** toocreate hello namespace.</span></span>

      <span data-ttu-id="ce202-131">![Fornecer um nome ao hub de eventos para o exemplo de streaming do Spark](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-provide-event-hub-name-for-spark-streaming.png "Fornecer um nome ao hub de eventos para o exemplo de streaming do Spark")</span><span class="sxs-lookup"><span data-stu-id="ce202-131">![Provide an event hub name for Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-provide-event-hub-name-for-spark-streaming.png "Provide an event hub name for Spark streaming example")</span></span>

    > [!NOTE]
    > <span data-ttu-id="ce202-132">Você deve selecionar Olá mesmo **local** como seu cluster Apache Spark no HDInsight tooreduce latência e custos.</span><span class="sxs-lookup"><span data-stu-id="ce202-132">You should select hello same **Location** as your Apache Spark cluster in HDInsight tooreduce latency and costs.</span></span>
    >
    >

4. <span data-ttu-id="ce202-133">Na lista de namespace de Hubs de eventos hello, clique em Olá recém-criado namespace.</span><span class="sxs-lookup"><span data-stu-id="ce202-133">In hello Event Hubs namespace list, click hello newly-created namespace.</span></span>      


5. <span data-ttu-id="ce202-134">Na folha de namespace hello, clique em **Hubs de eventos**e, em seguida, clique em **+ Hub de eventos** toocreate um novo Hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="ce202-134">In hello namespace blade, click **Event Hubs**, and then click **+ Event Hub** toocreate a new Event Hub.</span></span>
   
    <span data-ttu-id="ce202-135">![Criar hub de eventos para exemplo de streaming do Spark](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-open-event-hubs-blade-for-spark-streaming-example.png "Criar hub de eventos para exemplo de streaming do Spark")</span><span class="sxs-lookup"><span data-stu-id="ce202-135">![Create event hub for Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-open-event-hubs-blade-for-spark-streaming-example.png "Create event hub for Spark streaming example")</span></span>

6. <span data-ttu-id="ce202-136">Digite um nome para o Hub de eventos, too10 de contagem de partição do conjunto hello e too1 de retenção de mensagem.</span><span class="sxs-lookup"><span data-stu-id="ce202-136">Type a name for your Event Hub, set hello partition count too10, and message retention too1.</span></span> <span data-ttu-id="ce202-137">Nós não são arquivar mensagens de saudação nesta solução para deixar Olá restante como padrão e, em seguida, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="ce202-137">We are not archiving hello messages in this solution so you can leave hello rest as default, and then click **Create**.</span></span>
   
    <span data-ttu-id="ce202-138">![Fornecer detalhes do hub de eventos para o exemplo de streaming do Spark](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-provide-event-hub-details-for-spark-streaming-example.png "Fornecer detalhes do hub de eventos para o exemplo de streaming do Spark")</span><span class="sxs-lookup"><span data-stu-id="ce202-138">![Provide event hub details for Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-provide-event-hub-details-for-spark-streaming-example.png "Provide event hub details for Spark streaming example")</span></span>

7. <span data-ttu-id="ce202-139">Olá recém-criado Hub de eventos é listado na folha de Hub de eventos de saudação.</span><span class="sxs-lookup"><span data-stu-id="ce202-139">hello newly created Event Hub is listed in hello Event Hub blade.</span></span>
    
     <span data-ttu-id="ce202-140">![Exibir Hub de eventos de exemplo de fluxo contínuo do hello Spark](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-view-event-hub-for-spark-streaming-example.png "Hub de eventos de exibição para Olá despertar streaming de exemplo")</span><span class="sxs-lookup"><span data-stu-id="ce202-140">![View Event Hub for hello Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-view-event-hub-for-spark-streaming-example.png "View Event Hub for hello Spark streaming example")</span></span>

8. <span data-ttu-id="ce202-141">Na folha de namespace hello (não Olá específico Hub de eventos folha), clique em **políticas de acesso compartilhado**e, em seguida, clique em **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="ce202-141">Back in hello namespace blade (not hello specific Event Hub blade), click **Shared access policies**, and then click **RootManageSharedAccessKey**.</span></span>
    
     <span data-ttu-id="ce202-142">![Definir políticas de Hub de eventos para o exemplo de fluxo contínuo do hello Spark](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-set-event-hub-policies-for-spark-streaming-example.png "políticas de Hub de eventos definida para Olá despertar streaming de exemplo")</span><span class="sxs-lookup"><span data-stu-id="ce202-142">![Set Event Hub policies for hello Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-set-event-hub-policies-for-spark-streaming-example.png "Set Event Hub policies for hello Spark streaming example")</span></span>

9. <span data-ttu-id="ce202-143">Clique em Olá Olá de toocopy do botão de cópia **RootManageSharedAccessKey** primária conexão e chave de cadeia de caracteres toohello área de transferência.</span><span class="sxs-lookup"><span data-stu-id="ce202-143">Click hello copy button toocopy hello **RootManageSharedAccessKey** primary key and connection string toohello clipboard.</span></span> <span data-ttu-id="ce202-144">Salve essas toouse posteriormente no tutorial de saudação.</span><span class="sxs-lookup"><span data-stu-id="ce202-144">Save these toouse later in hello tutorial.</span></span>
    
     <span data-ttu-id="ce202-145">![Exibir chaves de política do Hub de eventos para exemplo de fluxo contínuo do hello Spark](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-view-event-hub-policy-keys.png "chaves de política do Hub de eventos de exibição para Olá despertar streaming de exemplo")</span><span class="sxs-lookup"><span data-stu-id="ce202-145">![View Event Hub policy keys for hello Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-view-event-hub-policy-keys.png "View Event Hub policy keys for hello Spark streaming example")</span></span>

## <a name="send-messages-tooazure-event-hub-using-a-sample-scala-application"></a><span data-ttu-id="ce202-146">Enviar mensagens tooAzure Hub de eventos usando um aplicativo de exemplo Scala</span><span class="sxs-lookup"><span data-stu-id="ce202-146">Send messages tooAzure Event Hub using a sample Scala application</span></span>

<span data-ttu-id="ce202-147">Nesta seção você usar um aplicativo Scala autônomo local que gera um fluxo de eventos e o envia tooAzure Hub de eventos que você criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="ce202-147">In this section you use a standalone local Scala application that generates a stream of events and sends it tooAzure Event Hub that you created earlier.</span></span> <span data-ttu-id="ce202-148">Este aplicativo está disponível no GitHub em [https://github.com/hdinsight/eventhubs-sample-event-producer](https://github.com/hdinsight/eventhubs-sample-event-producer).</span><span class="sxs-lookup"><span data-stu-id="ce202-148">This application is available on GitHub at [https://github.com/hdinsight/eventhubs-sample-event-producer](https://github.com/hdinsight/eventhubs-sample-event-producer).</span></span> <span data-ttu-id="ce202-149">etapas de saudação aqui supõem que você já tiver bifurcada este repositório GitHub.</span><span class="sxs-lookup"><span data-stu-id="ce202-149">hello steps here assume that you have already forked this GitHub repository.</span></span>

1. <span data-ttu-id="ce202-150">Verifique se que você tem o seguinte Olá instalado no computador de saudação em que você executa este aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ce202-150">Make sure you have hello following installed on hello computer where you run this application.</span></span>

    * <span data-ttu-id="ce202-151">Kit de desenvolvimento Oracle Java.</span><span class="sxs-lookup"><span data-stu-id="ce202-151">Oracle Java Development kit.</span></span> <span data-ttu-id="ce202-152">Você pode instalá-lo clicando [aqui](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="ce202-152">You can install it from [here](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
    * <span data-ttu-id="ce202-153">Apache Maven.</span><span class="sxs-lookup"><span data-stu-id="ce202-153">Apache Maven.</span></span> <span data-ttu-id="ce202-154">Você pode baixá-lo [aqui](https://maven.apache.org/download.cgi).</span><span class="sxs-lookup"><span data-stu-id="ce202-154">You can download it from [here](https://maven.apache.org/download.cgi).</span></span> <span data-ttu-id="ce202-155">Instruções tooinstall Maven estão disponíveis [aqui](https://maven.apache.org/install.html).</span><span class="sxs-lookup"><span data-stu-id="ce202-155">Instructions tooinstall Maven are available [here](https://maven.apache.org/install.html).</span></span>

2. <span data-ttu-id="ce202-156">Abra um prompt de comando e navegue local toohello clonar o repositório do GitHub Olá Olá aplicativo de exemplo Scala e execute Olá aplicativo de hello toobuild comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="ce202-156">Open a command prompt and navigate toohello location you cloned hello GitHub repo for hello sample Scala application and run hello following command toobuild hello application.</span></span>

        mvn package

3. <span data-ttu-id="ce202-157">Olá jar de saída para o aplicativo hello, **com-microsoft-azure-eventhubs-client-example-0.2.0.jar**, é criado sob **/destino** directory.</span><span class="sxs-lookup"><span data-stu-id="ce202-157">hello output jar for hello application, **com-microsoft-azure-eventhubs-client-example-0.2.0.jar**, is created under **/target** directory.</span></span> <span data-ttu-id="ce202-158">Você usa este JAR posteriormente na solução completa do tootest Olá neste artigo.</span><span class="sxs-lookup"><span data-stu-id="ce202-158">You use this JAR later in this article tootest hello complete solution.</span></span>

## <a name="create-application-tooreceive-messages-from-event-hub-into-a-spark-cluster"></a><span data-ttu-id="ce202-159">Criar as mensagens de tooreceive do aplicativo de Hub de eventos em um cluster do Spark</span><span class="sxs-lookup"><span data-stu-id="ce202-159">Create application tooreceive messages from Event Hub into a Spark cluster</span></span> 

<span data-ttu-id="ce202-160">Temos duas tooconnect abordagens Spark Streaming e Hubs de eventos do Azure, com base no receptor de conexão e conexão direta com base DStream.</span><span class="sxs-lookup"><span data-stu-id="ce202-160">We have two approaches tooconnect Spark Streaming and Azure Event Hubs, Receiver-based connection and Direct-DStream-based connection.</span></span> <span data-ttu-id="ce202-161">Com base em DStream direta é apresentado em janeiro de 2017, versão Olá 2.0.3.</span><span class="sxs-lookup"><span data-stu-id="ce202-161">Direct-DStream-based is introduced on Jan of 2017, in hello 2.0.3 release.</span></span> <span data-ttu-id="ce202-162">Ele deve conexão tooreplace Olá original com base no destinatário conforme ele é mais eficaz e eficiente de recursos.</span><span class="sxs-lookup"><span data-stu-id="ce202-162">It is supposed tooreplace hello original receiver-based connection as it is more performant and resource-efficient.</span></span> <span data-ttu-id="ce202-163">Mais detalhes podem ser encontrados em [https://github.com/hdinsight/spark-eventhubs](https://github.com/hdinsight/spark-eventhubs).</span><span class="sxs-lookup"><span data-stu-id="ce202-163">More details found in [https://github.com/hdinsight/spark-eventhubs](https://github.com/hdinsight/spark-eventhubs).</span></span> <span data-ttu-id="ce202-164">O Direct DStream dá suporte apenas ao Spark 2.0+.</span><span class="sxs-lookup"><span data-stu-id="ce202-164">Direct DStream only supports Spark 2.0+.</span></span>

### <a name="build-applications-with-hello-dependency-toospark-eventhubs-connector"></a><span data-ttu-id="ce202-165">Criar aplicativos com o conector do hello dependência toospark eventhubs</span><span class="sxs-lookup"><span data-stu-id="ce202-165">Build applications with hello dependency toospark-eventhubs connector</span></span>

<span data-ttu-id="ce202-166">Podemos também publica Olá versão do Spark-EventHubs no GitHub de preparo.</span><span class="sxs-lookup"><span data-stu-id="ce202-166">We will also publish hello staging version of Spark-EventHubs in GitHub.</span></span> <span data-ttu-id="ce202-167">toouse Olá preparo versão Spark EventHubs, primeira etapa de saudação é tooindicate GitHub como Olá repositório de origem adicionando Olá toopom.xml de entrada a seguir:</span><span class="sxs-lookup"><span data-stu-id="ce202-167">toouse hello staging version of Spark-EventHubs, hello first step is tooindicate GitHub as hello source repo by adding hello following entry toopom.xml:</span></span>

```xml
<repository>
      <id>spark-eventhubs</id>
      <url>https://raw.github.com/hdinsight/spark-eventhubs/maven-repo/</url>
      <snapshots>
        <enabled>true</enabled>
        <updatePolicy>always</updatePolicy>
      </snapshots>
</repository>
```

<span data-ttu-id="ce202-168">Em seguida, você pode adicionar Olá dependência tooyour projeto tootake Olá versão de pré-lançamento a seguir.</span><span class="sxs-lookup"><span data-stu-id="ce202-168">You can then add hello following dependency tooyour project tootake hello pre-released version.</span></span>

<span data-ttu-id="ce202-169">Dependência do Maven</span><span class="sxs-lookup"><span data-stu-id="ce202-169">Maven Dependency</span></span>

```xml
<!-- https://mvnrepository.com/artifact/com.microsoft.azure/spark-streaming-eventhubs_2.11 -->
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>spark-streaming-eventhubs_2.11</artifactId>
    <version>2.0.4</version>
</dependency>
```

<span data-ttu-id="ce202-170">Dependência SBT</span><span class="sxs-lookup"><span data-stu-id="ce202-170">SBT Dependency</span></span>

```
// https://mvnrepository.com/artifact/com.microsoft.azure/spark-streaming-eventhubs_2.11
libraryDependencies += "com.microsoft.azure" % "spark-streaming-eventhubs_2.11" % "2.0.4"
```

### <a name="direct-dstream-connection"></a><span data-ttu-id="ce202-171">Conexão por Direct DStream</span><span class="sxs-lookup"><span data-stu-id="ce202-171">Direct DStream Connection</span></span>

<span data-ttu-id="ce202-172">Um arquivo jar pré-criado que contém exemplos que usam Direct DStream pode ser baixado em [http://central.maven.org/maven2/com/microsoft/azure/spark-streaming-eventhubs_2.11/2.0.4/spark-streaming-eventhubs_2.11-2.0.4.jar](http://central.maven.org/maven2/com/microsoft/azure/spark-streaming-eventhubs_2.11/2.0.4/spark-streaming-eventhubs_2.11-2.0.4.jar).</span><span class="sxs-lookup"><span data-stu-id="ce202-172">A pre-built jar file containing examples using Direct DStream can be downloaded in [http://central.maven.org/maven2/com/microsoft/azure/spark-streaming-eventhubs_2.11/2.0.4/spark-streaming-eventhubs_2.11-2.0.4.jar](http://central.maven.org/maven2/com/microsoft/azure/spark-streaming-eventhubs_2.11/2.0.4/spark-streaming-eventhubs_2.11-2.0.4.jar).</span></span>

<span data-ttu-id="ce202-173">arquivo jar de saudação contém três exemplos, cujo código-fonte estão disponíveis em [https://github.com/hdinsight/spark-eventhubs/tree/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream](https://github.com/hdinsight/spark-eventhubs/tree/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream).</span><span class="sxs-lookup"><span data-stu-id="ce202-173">hello jar file contains three examples whose source code are available at [https://github.com/hdinsight/spark-eventhubs/tree/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream](https://github.com/hdinsight/spark-eventhubs/tree/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream).</span></span>

<span data-ttu-id="ce202-174">Usando [WindowingWordCount](https://github.com/hdinsight/spark-eventhubs/blob/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream/WindowingWordCount.scala) como um exemplo:</span><span class="sxs-lookup"><span data-stu-id="ce202-174">Taking [WindowingWordCount](https://github.com/hdinsight/spark-eventhubs/blob/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream/WindowingWordCount.scala) as an example:</span></span>

```scala
private def createStreamingContext(
  sparkCheckpointDir: String,
  batchDuration: Int,
  namespace: String,
  eventHunName: String,
  eventhubParams: Map[String, String],
  progressDir: String) = {
val ssc = new StreamingContext(new SparkContext(), Seconds(batchDuration))
ssc.checkpoint(sparkCheckpointDir)
val inputDirectStream = EventHubsUtils.createDirectStreams(
  ssc,
  namespace,
  progressDir,
  Map(eventHunName -> eventhubParams))

inputDirectStream.map(receivedRecord => (new String(receivedRecord.getBody), 1)).
  reduceByKeyAndWindow((v1, v2) => v1 + v2, (v1, v2) => v1 - v2, Seconds(batchDuration * 3),
    Seconds(batchDuration)).print()

ssc
}

def main(args: Array[String]): Unit = {

if (args.length != 8) {
  println("Usage: program progressDir PolicyName PolicyKey EventHubNamespace EventHubName" +
    " BatchDuration(seconds) Spark_Checkpoint_Directory maxRate")
  sys.exit(1)
}

val progressDir = args(0)
val policyName = args(1)
val policykey = args(2)
val namespace = args(3)
val name = args(4)
val batchDuration = args(5).toInt
val sparkCheckpointDir = args(6)
val maxRate = args(7)

val eventhubParameters = Map[String, String] (
  "eventhubs.policyname" -> policyName,
  "eventhubs.policykey" -> policykey,
  "eventhubs.namespace" -> namespace,
  "eventhubs.name" -> name,
  "eventhubs.partition.count" -> "32",
  "eventhubs.consumergroup" -> "$Default",
  "eventhubs.maxRate" -> s"$maxRate"
)

val ssc = StreamingContext.getOrCreate(sparkCheckpointDir,
  () => createStreamingContext(sparkCheckpointDir, batchDuration, namespace, name,
    eventhubParameters, progressDir))

ssc.start()
ssc.awaitTermination()
}
```

<span data-ttu-id="ce202-175">Em hello, o exemplo acima `eventhubParameters` Olá parâmetros específicos tooa EventHubs de única instância e você tem toopass-toohello `createDirectStreams` API que constrói um namespace de Hubs de eventos DStream direto objeto mapeamento tooa.</span><span class="sxs-lookup"><span data-stu-id="ce202-175">In hello above example, `eventhubParameters` are hello parameters specific tooa single EventHubs instance and you have toopass it toohello `createDirectStreams` API which constructs a Direct DStream object mapping tooa Event Hubs namespace.</span></span> <span data-ttu-id="ce202-176">Sobre Olá DStream direto, você pode chamar qualquer API DStream fornecido pela estrutura Spark API de Streaming.</span><span class="sxs-lookup"><span data-stu-id="ce202-176">Over hello Direct DStream object, you can call any DStream API provided by Spark Streaming API framework.</span></span> <span data-ttu-id="ce202-177">Neste exemplo, calculamos frequência saudação de cada palavra em intervalos de lote micro 3 última hello.</span><span class="sxs-lookup"><span data-stu-id="ce202-177">In this example, we calculate hello frequency of each word within hello last 3 micro batch intervals.</span></span>

### <a name="receiver-based-connection"></a><span data-ttu-id="ce202-178">Conexão com base em receptor</span><span class="sxs-lookup"><span data-stu-id="ce202-178">Receiver-based Connection</span></span>

<span data-ttu-id="ce202-179">Um Spark streaming escrito em Scala, que recebe eventos e destinos de toodifferent de saudação de rota, o aplicativo de exemplo está disponível em [https://github.com/hdinsight/spark-streaming-data-persistence-examples](https://github.com/hdinsight/spark-streaming-data-persistence-examples).</span><span class="sxs-lookup"><span data-stu-id="ce202-179">A Spark streaming example application written in Scala, which receives events and route hello toodifferent destinations, is available at [https://github.com/hdinsight/spark-streaming-data-persistence-examples](https://github.com/hdinsight/spark-streaming-data-persistence-examples).</span></span> <span data-ttu-id="ce202-180">Siga as etapas de saudação abaixo do aplicativo de saudação tooupdate para sua configuração de Hub de eventos e criar hello jar de saída.</span><span class="sxs-lookup"><span data-stu-id="ce202-180">Follow hello steps below tooupdate hello application for your Event Hub configuration and create hello output jar.</span></span>

1. <span data-ttu-id="ce202-181">Inicie a IDEIA de IntelliJ e de saudação iniciar tela, selecione **Check-out do controle de versão** e, em seguida, clique em **Git**.</span><span class="sxs-lookup"><span data-stu-id="ce202-181">Launch IntelliJ IDEA and from hello launch screen select **Check out from Version Control** and then click **Git**.</span></span>
   
    <span data-ttu-id="ce202-182">![Exemplo de streaming do Apache Spark – obter fontes do Git](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-get-source-from-git.png "Exemplo de streaming do Apache Spark – obter fontes do Git")</span><span class="sxs-lookup"><span data-stu-id="ce202-182">![Apache Spark streaming example - get sources from Git](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-get-source-from-git.png "Apache Spark streaming example - get sources from Git")</span></span>

2. <span data-ttu-id="ce202-183">Em Olá **Clone repositório** caixa de diálogo, forneça a URL Olá toohello tooclone de repositório Git do, especifique Olá tooclone de diretório para e, em seguida, clique em **Clone**.</span><span class="sxs-lookup"><span data-stu-id="ce202-183">In hello **Clone Repository** dialog box, provide hello URL toohello Git repository tooclone from, specify hello directory tooclone to, and then click **Clone**.</span></span>
   
    <span data-ttu-id="ce202-184">![Exemplo de streaming do Apache Spark – clonar do Git](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-clone-from-git.png "Exemplo de streaming do Apache Spark – clonar do Git")</span><span class="sxs-lookup"><span data-stu-id="ce202-184">![Apache Spark streaming example - clone from Git](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-clone-from-git.png "Apache Spark streaming example - clone from Git")</span></span>
3. <span data-ttu-id="ce202-185">Siga os prompts de saudação até que o projeto Olá completamente é clonado.</span><span class="sxs-lookup"><span data-stu-id="ce202-185">Follow hello prompts till hello project is completely cloned.</span></span> <span data-ttu-id="ce202-186">Pressione **Alt + 1** tooopen Olá **exibição projeto**.</span><span class="sxs-lookup"><span data-stu-id="ce202-186">Press **Alt + 1** tooopen hello **Project View**.</span></span> <span data-ttu-id="ce202-187">Ele deve ser semelhante a seguinte hello.</span><span class="sxs-lookup"><span data-stu-id="ce202-187">It should resemble hello following.</span></span>
   
    <span data-ttu-id="ce202-188">![Exemplo de streaming do Apache Spark – Exibição do Projeto](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-project-view.png "Exemplo de streaming do Apache Spark – Exibição do Projeto")</span><span class="sxs-lookup"><span data-stu-id="ce202-188">![Apache Spark streaming example - Project View](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-project-view.png "Apache Spark streaming example - Project View")</span></span>
4. <span data-ttu-id="ce202-189">Verifique se o código do aplicativo hello é compilado com Java8.</span><span class="sxs-lookup"><span data-stu-id="ce202-189">Make sure hello application code is compiled with Java8.</span></span> <span data-ttu-id="ce202-190">tooensure, clique **arquivo**, clique em **estrutura do projeto**e em Olá **projeto** guia, verifique se o nível de linguagem do projeto está definido muito**8 - Lambdas, tipo anotações, etc.**.</span><span class="sxs-lookup"><span data-stu-id="ce202-190">tooensure this, click **File**, click **Project Structure**, and on hello **Project** tab, make sure Project language level is set too**8 - Lambdas, type annotations, etc.**.</span></span>
   
    <span data-ttu-id="ce202-191">![Exemplo de streaming do Apache Spark – Definir compilador](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-java-8-compiler.png "Exemplo de streaming do Apache Spark – Definir compilador")</span><span class="sxs-lookup"><span data-stu-id="ce202-191">![Apache Spark streaming example - Set compiler](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-java-8-compiler.png "Apache Spark streaming example - Set compiler")</span></span>
5. <span data-ttu-id="ce202-192">Olá abrir **pom.xml** e verifique se a versão do Spark hello está correta.</span><span class="sxs-lookup"><span data-stu-id="ce202-192">Open hello **pom.xml** and make sure hello Spark version is correct.</span></span> <span data-ttu-id="ce202-193">Em `<properties>` nó, procure Olá trecho de código a seguir e verificar a versão do Spark hello.</span><span class="sxs-lookup"><span data-stu-id="ce202-193">Under `<properties>` node, look for hello following snippet and verify hello Spark version.</span></span>

        <scala.version>2.11.8</scala.version>
        <scala.compat.version>2.11.8</scala.compat.version>
        <scala.binary.version>2.11</scala.binary.version>
        <spark.version>2.0.0</spark.version>

6. <span data-ttu-id="ce202-194">aplicativo Hello requer um jar dependência chamado **jar do driver JDBC**.</span><span class="sxs-lookup"><span data-stu-id="ce202-194">hello application requires a dependency jar called **JDBC driver jar**.</span></span> <span data-ttu-id="ce202-195">Isso é necessário toowrite mensagens de saudação recebidas do Hub de eventos em um banco de dados do SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="ce202-195">This is required toowrite hello messages received from Event Hub into an Azure SQL database.</span></span> <span data-ttu-id="ce202-196">Você pode baixar esse jar (v 4.1 ou posterior) [aqui](https://msdn.microsoft.com/sqlserver/aa937724.aspx).</span><span class="sxs-lookup"><span data-stu-id="ce202-196">You can download this jar (v4.1 or later) from [here](https://msdn.microsoft.com/sqlserver/aa937724.aspx).</span></span> <span data-ttu-id="ce202-197">Adicione referência toothis jar na biblioteca de saudação do projeto.</span><span class="sxs-lookup"><span data-stu-id="ce202-197">Add reference toothis jar in hello project library.</span></span> <span data-ttu-id="ce202-198">Execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="ce202-198">Perform hello following steps:</span></span>
     
     1. <span data-ttu-id="ce202-199">Na janela de IDEIA IntelliJ onde você tem aplicativo hello abrir, clique em **arquivo**, clique em **estrutura do projeto**e, em seguida, clique em **bibliotecas**.</span><span class="sxs-lookup"><span data-stu-id="ce202-199">From IntelliJ IDEA window where you have hello application open, click **File**, click **Project Structure**, and then click **Libraries**.</span></span> 
     2. <span data-ttu-id="ce202-200">Clique em Olá Adicionar ícone (![Adicionar ícone](./media/hdinsight-apache-spark-eventhub-streaming/add-icon.png)), clique em **Java**e, em seguida, navegue toohello local onde você baixou o jar do driver JDBC hello.</span><span class="sxs-lookup"><span data-stu-id="ce202-200">Click hello add icon (![add icon](./media/hdinsight-apache-spark-eventhub-streaming/add-icon.png)), click **Java**, and then navigate toohello location where you downloaded hello JDBC driver jar.</span></span> <span data-ttu-id="ce202-201">Siga Olá prompts tooadd Olá arquivo toohello projeto biblioteca jar.</span><span class="sxs-lookup"><span data-stu-id="ce202-201">Follow hello prompts tooadd hello jar file toohello project library.</span></span>

         <span data-ttu-id="ce202-202">![adicionar dependências ausentes](./media/hdinsight-apache-spark-eventhub-streaming/add-missing-dependency-jars.png "Adicionar jars de dependência ausente")</span><span class="sxs-lookup"><span data-stu-id="ce202-202">![add missing dependencies](./media/hdinsight-apache-spark-eventhub-streaming/add-missing-dependency-jars.png "Add missing dependency jars")</span></span>
     3. <span data-ttu-id="ce202-203">Clique em **Aplicar**.</span><span class="sxs-lookup"><span data-stu-id="ce202-203">Click **Apply**.</span></span>

7. <span data-ttu-id="ce202-204">Crie arquivo de jar de saída de hello.</span><span class="sxs-lookup"><span data-stu-id="ce202-204">Create hello output jar file.</span></span> <span data-ttu-id="ce202-205">Execute Olá etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="ce202-205">Perform hello following steps.</span></span>

   1. <span data-ttu-id="ce202-206">Em Olá **estrutura do projeto** caixa de diálogo, clique em **artefatos** e, em seguida, clique em hello mais símbolo.</span><span class="sxs-lookup"><span data-stu-id="ce202-206">In hello **Project Structure** dialog box, click **Artifacts** and then click hello plus symbol.</span></span> <span data-ttu-id="ce202-207">Na caixa de diálogo pop-up de saudação, clique em **JAR**e, em seguida, clique em **de módulos com dependências**.</span><span class="sxs-lookup"><span data-stu-id="ce202-207">From hello pop-up dialog box, click **JAR**, and then click **From modules with dependencies**.</span></span>      
       
       <span data-ttu-id="ce202-208">![Exemplo de streaming do Apache Spark – Criar JAR](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-create-jar.png "Exemplo de streaming do Apache Spark – Criar JAR")</span><span class="sxs-lookup"><span data-stu-id="ce202-208">![Apache Spark streaming example - create JAR](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-create-jar.png "Apache Spark streaming example - create JAR")</span></span>
   2. <span data-ttu-id="ce202-209">Em Olá **criar JAR de módulos** caixa de diálogo, clique nas reticências da saudação (![reticências](./media/hdinsight-apache-spark-eventhub-streaming/ellipsis.png)) em relação a saudação **classe principal**.</span><span class="sxs-lookup"><span data-stu-id="ce202-209">In hello **Create JAR from Modules** dialog box, click hello ellipsis (![ellipsis](./media/hdinsight-apache-spark-eventhub-streaming/ellipsis.png)) against hello **Main Class**.</span></span>
   3. <span data-ttu-id="ce202-210">Em Olá **selecionar principal classe** caixa de diálogo caixa, selecione qualquer uma das classes disponíveis hello e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="ce202-210">In hello **Select Main Class** dialog box, select any of hello available classes and then click **OK**.</span></span>
      
       <span data-ttu-id="ce202-211">![Exemplo de streaming do Apache Spark – selecionar classe para jar](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-select-class-for-jar.png "Exemplo de streaming do Apache Spark – selecionar classe para jar")</span><span class="sxs-lookup"><span data-stu-id="ce202-211">![Apache Spark streaming example - select class for jar](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-select-class-for-jar.png "Apache Spark streaming example - select class for jar")</span></span>
   4. <span data-ttu-id="ce202-212">Em Olá **criar JAR de módulos** caixa de diálogo caixa, certifique-se de que a opção Olá muito**extrair toohello destino JAR** está selecionado e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="ce202-212">In hello **Create JAR from Modules** dialog box, make sure that hello option too**extract toohello target JAR** is selected, and then click **OK**.</span></span> <span data-ttu-id="ce202-213">Isso cria um JAR único com todas as dependências.</span><span class="sxs-lookup"><span data-stu-id="ce202-213">This creates a single JAR with all dependencies.</span></span>
      
       <span data-ttu-id="ce202-214">![Exemplo de streaming do Apache Spark – criar jar a partir de módulos](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-create-jar-from-modules.png "Exemplo de streaming do Apache Spark – criar jar a partir de módulos")</span><span class="sxs-lookup"><span data-stu-id="ce202-214">![Apache Spark streaming example - create jar from modules](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-create-jar-from-modules.png "Apache Spark streaming example - create jar from modules")</span></span>
   5. <span data-ttu-id="ce202-215">Olá **Layout de saída** guia lista todos os jars Olá que estão incluídos como parte do projeto de Maven hello.</span><span class="sxs-lookup"><span data-stu-id="ce202-215">hello **Output Layout** tab lists all hello jars that are included as part of hello Maven project.</span></span> <span data-ttu-id="ce202-216">Você pode selecionar e excluir Olá aqueles nos quais Olá Scala aplicativo não tem nenhuma dependência direta.</span><span class="sxs-lookup"><span data-stu-id="ce202-216">You can select and delete hello ones on which hello Scala application has no direct dependency.</span></span> <span data-ttu-id="ce202-217">Para o aplicativo hello, estamos criando aqui, você pode remover Olá tudo, exceto o último (**spark-streaming--persistência-exemplos de dados de saída de compilação**).</span><span class="sxs-lookup"><span data-stu-id="ce202-217">For hello application we are creating here, you can remove all but hello last one (**spark-streaming-data-persistence-examples compile output**).</span></span> <span data-ttu-id="ce202-218">Selecione Olá jars toodelete e clique em Olá **excluir** ícone (![excluir ícone](./media/hdinsight-apache-spark-eventhub-streaming/delete-icon.png)).</span><span class="sxs-lookup"><span data-stu-id="ce202-218">Select hello jars toodelete and then click hello **Delete** icon (![delete icon](./media/hdinsight-apache-spark-eventhub-streaming/delete-icon.png)).</span></span>
      
       <span data-ttu-id="ce202-219">![Exemplo de streaming do Apache Spark – excluir jars extraídos](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-delete-output-jars.png "Exemplo de streaming do Apache Spark – excluir jars extraídos")</span><span class="sxs-lookup"><span data-stu-id="ce202-219">![Apache Spark streaming example - delete extracted jars](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-delete-output-jars.png "Apache Spark streaming example - delete extracted jars")</span></span>
      
       <span data-ttu-id="ce202-220">Certifique-se de **compilar no Verifique** caixa é selecionada, o que garante que jar Olá é criado sempre que o projeto Olá for criado ou atualizado.</span><span class="sxs-lookup"><span data-stu-id="ce202-220">Make sure **Build on make** box is selected, which ensures that hello jar is created every time hello project is built or updated.</span></span> <span data-ttu-id="ce202-221">Clique em **Aplicar**.</span><span class="sxs-lookup"><span data-stu-id="ce202-221">Click **Apply**.</span></span>
   6. <span data-ttu-id="ce202-222">Em Olá **Layout de saída** guia à direita na parte inferior de saudação do hello **elementos disponíveis** caixa, você tem jar do hello SQL JDBC que você adicionou a biblioteca de projeto toohello anterior.</span><span class="sxs-lookup"><span data-stu-id="ce202-222">In hello **Output Layout** tab, right at hello bottom of hello **Available Elements** box, you have hello SQL JDBC jar that you added earlier toohello project library.</span></span> <span data-ttu-id="ce202-223">Você deve adicionar esse toohello **Layout de saída** guia. Clique no arquivo jar do hello e clique **extrair em saída raiz**.</span><span class="sxs-lookup"><span data-stu-id="ce202-223">You must add this toohello **Output Layout** tab. Right-click hello jar file, and then click **Extract Into Output Root**.</span></span>
      
       <span data-ttu-id="ce202-224">![Exemplo de streaming do Apache Spark – extrair jar de dependência](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-extract-dependency-jar.png "Exemplo de streaming do Apache Spark – extrair jar de dependência")</span><span class="sxs-lookup"><span data-stu-id="ce202-224">![Apache Spark streaming example - extract dependency jar](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-extract-dependency-jar.png "Apache Spark streaming example - extract dependency jar")</span></span>  
      
       <span data-ttu-id="ce202-225">Olá **Layout de saída** guia agora deve se parecer com isso.</span><span class="sxs-lookup"><span data-stu-id="ce202-225">hello **Output Layout** tab should now look like this.</span></span>
      
       <span data-ttu-id="ce202-226">![Exemplo de streaming do Apache Spark – guia de saída final](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-final-output-tab.png "Exemplo de streaming do Apache Spark – guia de saída final")</span><span class="sxs-lookup"><span data-stu-id="ce202-226">![Apache Spark streaming example - final output tab](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-final-output-tab.png "Apache Spark streaming example - final output tab")</span></span>        
      
       <span data-ttu-id="ce202-227">Em Olá **estrutura do projeto** caixa de diálogo, clique em **aplicar** e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="ce202-227">In hello **Project Structure** dialog box, click **Apply** and then click **OK**.</span></span>    
   7. <span data-ttu-id="ce202-228">Olá barra de menus, clique em **criar**e, em seguida, clique em **projeto Make**.</span><span class="sxs-lookup"><span data-stu-id="ce202-228">From hello menu bar, click **Build**, and then click **Make Project**.</span></span> <span data-ttu-id="ce202-229">Você também pode clicar em **criar artefatos** toocreate jar de saudação.</span><span class="sxs-lookup"><span data-stu-id="ce202-229">You can also click **Build Artifacts** toocreate hello jar.</span></span> <span data-ttu-id="ce202-230">Olá jar de saída é criado sob **\classes\artifacts**.</span><span class="sxs-lookup"><span data-stu-id="ce202-230">hello output jar is created under **\classes\artifacts**.</span></span>
      
       <span data-ttu-id="ce202-231">![Exemplo de streaming do Apache Spark – JAR de saída](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-output-jar.png "Exemplo de streaming do Apache Spark – JAR de saída")</span><span class="sxs-lookup"><span data-stu-id="ce202-231">![Apache Spark streaming example - output JAR](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-output-jar.png "Apache Spark streaming example - output JAR")</span></span>

## <a name="run-hello-application-remotely-on-a-spark-cluster-using-livy"></a><span data-ttu-id="ce202-232">Executar o aplicativo hello remotamente em um cluster do Spark usando Livy</span><span class="sxs-lookup"><span data-stu-id="ce202-232">Run hello application remotely on a Spark cluster using Livy</span></span>

<span data-ttu-id="ce202-233">Neste artigo use Livy toorun Olá Apache Spark streaming aplicativo remotamente em um cluster Spark.</span><span class="sxs-lookup"><span data-stu-id="ce202-233">In this article you use Livy toorun hello Apache Spark streaming application remotely on a Spark cluster.</span></span> <span data-ttu-id="ce202-234">Para obter uma discussão detalhada sobre como toouse Livy com HDInsight Spark do cluster, consulte [enviar trabalhos remotamente tooan Apache Spark cluster no Azure HDInsight](hdinsight-apache-spark-livy-rest-interface.md).</span><span class="sxs-lookup"><span data-stu-id="ce202-234">For detailed discussion on how toouse Livy with HDInsight Spark cluster, see [Submit jobs remotely tooan Apache Spark cluster on Azure HDInsight](hdinsight-apache-spark-livy-rest-interface.md).</span></span> <span data-ttu-id="ce202-235">Antes de começar executando o aplicativo de streaming de Spark hello, há algumas coisas que você deve fazer:</span><span class="sxs-lookup"><span data-stu-id="ce202-235">Before you can start running hello Spark streaming application, there are a couple of things you should do:</span></span>

1. <span data-ttu-id="ce202-236">Iniciar Olá autônomo local aplicativo toogenerate eventos e enviados tooEvent Hub.</span><span class="sxs-lookup"><span data-stu-id="ce202-236">Start hello local standalone application toogenerate events and sent tooEvent Hub.</span></span> <span data-ttu-id="ce202-237">Use Olá toodo de comando a seguir para:</span><span class="sxs-lookup"><span data-stu-id="ce202-237">Use hello following command toodo so:</span></span>

        java -cp com-microsoft-azure-eventhubs-client-example-0.2.0.jar com.microsoft.eventhubs.client.example.EventhubsClientDriver --eventhubs-namespace "mysbnamespace" --eventhubs-name "myeventhub" --policy-name "mysendpolicy" --policy-key "<policy key>" --message-length 32 --thread-count 32 --message-count -1

2. <span data-ttu-id="ce202-238">Saudação de cópia streaming jar (**spark-streaming-data-persistência-examples.jar**) toohello associado Olá cluster de armazenamento de Blob do Azure.</span><span class="sxs-lookup"><span data-stu-id="ce202-238">Copy hello streaming jar (**spark-streaming-data-persistence-examples.jar**) toohello Azure Blob storage associated with hello cluster.</span></span> <span data-ttu-id="ce202-239">Isso torna Olá jar acessível tooLivy.</span><span class="sxs-lookup"><span data-stu-id="ce202-239">This makes hello jar accessible tooLivy.</span></span> <span data-ttu-id="ce202-240">Você pode usar [ **AzCopy**](../storage/common/storage-use-azcopy.md), um comando de linha utilitário, toodo assim.</span><span class="sxs-lookup"><span data-stu-id="ce202-240">You can use [**AzCopy**](../storage/common/storage-use-azcopy.md), a command line utility, toodo so.</span></span> <span data-ttu-id="ce202-241">Há muito de outros clientes, você pode usar dados de tooupload.</span><span class="sxs-lookup"><span data-stu-id="ce202-241">There are a lot of other clients you can use tooupload data.</span></span> <span data-ttu-id="ce202-242">É possível saber mais sobre eles em [Carregar dados para trabalhos do Hadoop no HDInsight](hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="ce202-242">You can find more about them at [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span>
3. <span data-ttu-id="ce202-243">Instale ONDULAÇÃO no computador de saudação onde você está executando esses aplicativos.</span><span class="sxs-lookup"><span data-stu-id="ce202-243">Install CURL on hello computer where you are running these applications from.</span></span> <span data-ttu-id="ce202-244">Usamos ONDULAÇÃO tooinvoke Olá Olá de toorun de pontos de extremidade Livy trabalhos remotamente.</span><span class="sxs-lookup"><span data-stu-id="ce202-244">We use CURL tooinvoke hello Livy endpoints toorun hello jobs remotely.</span></span>

### <a name="run-hello-spark-streaming-application-tooreceive-hello-events-into-an-azure-storage-blob-as-text"></a><span data-ttu-id="ce202-245">Executar Olá Spark streaming tooreceive Olá eventos do aplicativo em um Blob de armazenamento do Azure como texto</span><span class="sxs-lookup"><span data-stu-id="ce202-245">Run hello Spark streaming application tooreceive hello events into an Azure Storage Blob as text</span></span>

<span data-ttu-id="ce202-246">Abra um prompt de comando, navegue toohello diretório onde você instalou ONDULAÇÃO e executar hello (nome de usuário/senha e cluster substituir) de comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="ce202-246">Open a command prompt, navigate toohello directory where you installed CURL, and run hello following command (replace username/password and cluster name):</span></span>

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputBlob.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

<span data-ttu-id="ce202-247">Olá parâmetros no arquivo hello **inputBlob.txt** são definidos da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="ce202-247">hello parameters in hello file **inputBlob.txt** are defined as follows:</span></span>

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsEventCount", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10"], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

<span data-ttu-id="ce202-248">Vamos Entenda quais são os parâmetros de saudação no arquivo de entrada hello:</span><span class="sxs-lookup"><span data-stu-id="ce202-248">Let us understand what hello parameters in hello input file are:</span></span>

* <span data-ttu-id="ce202-249">**arquivo** Olá caminho toohello aplicativo jar em arquivo hello conta de armazenamento do Azure associada Olá cluster.</span><span class="sxs-lookup"><span data-stu-id="ce202-249">**file** is hello path toohello application jar file on hello Azure storage account associated with hello cluster.</span></span>
* <span data-ttu-id="ce202-250">**nome da classe** é Olá nome da classe Olá JAR hello.</span><span class="sxs-lookup"><span data-stu-id="ce202-250">**className** is hello name of hello class in hello jar.</span></span>
* <span data-ttu-id="ce202-251">**argumentos** Olá lista de argumentos necessários pela classe Olá</span><span class="sxs-lookup"><span data-stu-id="ce202-251">**args** is hello list of arguments required by hello class</span></span>
* <span data-ttu-id="ce202-252">**numExecutors** é Olá número de núcleos usados pelo saudação do Spark toorun streaming de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="ce202-252">**numExecutors** is hello number of cores used by Spark toorun hello streaming application.</span></span> <span data-ttu-id="ce202-253">Sempre deve ser pelo menos duas vezes o número de saudação de partições de Hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="ce202-253">This should always be at least twice hello number of Event Hub partitions.</span></span>
* <span data-ttu-id="ce202-254">**executorMemory**, **executorCores**, **driverMemory** são parâmetros usados tooassign necessários recursos toohello aplicativo de transmissão.</span><span class="sxs-lookup"><span data-stu-id="ce202-254">**executorMemory**, **executorCores**, **driverMemory** are parameters used tooassign required resources toohello streaming application.</span></span>

> [!NOTE]
> <span data-ttu-id="ce202-255">Não é necessário toocreate Olá pastas de saída (EventCheckpoint, EventCount/EventCount10) que são usadas como parâmetros.</span><span class="sxs-lookup"><span data-stu-id="ce202-255">You do not need toocreate hello output folders (EventCheckpoint, EventCount/EventCount10) that are used as parameters.</span></span> <span data-ttu-id="ce202-256">Olá streaming aplicativo criará para você.</span><span class="sxs-lookup"><span data-stu-id="ce202-256">hello streaming application creates them for you.</span></span>
>
>

<span data-ttu-id="ce202-257">Quando você executa o comando hello, você verá uma saída semelhante Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="ce202-257">When you run hello command, you should see an output like hello following:</span></span>

    < HTTP/1.1 201 Created
    < Content-Type: application/json; charset=UTF-8
    < Location: /18
    < Server: Microsoft-IIS/8.5
    < X-Powered-By: ARR/2.5
    < X-Powered-By: ASP.NET
    < Date: Tue, 01 Dec 2015 05:39:10 GMT
    < Content-Length: 37
    <
    {"id":1,"state":"starting","log":[]}* Connection #0 toohost mysparkcluster.azurehdinsight.net left intact

<span data-ttu-id="ce202-258">Anote o ID de lote Olá na última linha hello da saída da saudação (no exemplo é '1').</span><span class="sxs-lookup"><span data-stu-id="ce202-258">Make a note of hello batch ID in hello last line of hello output (in this example it is '1').</span></span> <span data-ttu-id="ce202-259">tooverify que Olá aplicativo seja executado com êxito, você pode examinar sua conta de armazenamento do Azure associada Olá cluster e você deverá ver Olá **/EventCount/EventCount10** pasta criada ali.</span><span class="sxs-lookup"><span data-stu-id="ce202-259">tooverify that hello application runs successfully, you can look at your Azure storage account associated with hello cluster and you should see hello **/EventCount/EventCount10** folder created there.</span></span> <span data-ttu-id="ce202-260">Essa pasta deve conter blobs que captura Olá número de eventos processados em Olá período de tempo especificado para o parâmetro hello **lote intervalo em segundos**.</span><span class="sxs-lookup"><span data-stu-id="ce202-260">This folder should contain blobs that captures hello number of events processed within hello time period specified for hello parameter **batch-interval-in-seconds**.</span></span>

<span data-ttu-id="ce202-261">aplicativo de transmissão Olá Spark continuará toorun até você eliminá-lo.</span><span class="sxs-lookup"><span data-stu-id="ce202-261">hello Spark streaming application will continue toorun until you kill it.</span></span> <span data-ttu-id="ce202-262">Assim, o toodo use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="ce202-262">toodo so, use hello following command:</span></span>

    curl -k --user "admin:mypassword1!" -v -X DELETE "https://mysparkcluster.azurehdinsight.net/livy/batches/1"

### <a name="run-hello-applications-tooreceive-hello-events-into-an-azure-storage-blob-as-json"></a><span data-ttu-id="ce202-263">Executar aplicativos de saudação tooreceive eventos de saudação em um Blob de armazenamento do Azure como JSON</span><span class="sxs-lookup"><span data-stu-id="ce202-263">Run hello applications tooreceive hello events into an Azure Storage Blob as JSON</span></span>
<span data-ttu-id="ce202-264">Abra um prompt de comando, navegue toohello diretório onde você instalou ONDULAÇÃO e executar hello (nome de usuário/senha e cluster substituir) de comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="ce202-264">Open a command prompt, navigate toohello directory where you installed CURL, and run hello following command (replace username/password and cluster name):</span></span>

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputJSON.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

<span data-ttu-id="ce202-265">Olá parâmetros no arquivo hello **inputJSON.txt** são definidos da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="ce202-265">hello parameters in hello file **inputJSON.txt** are defined as follows:</span></span>

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsToAzureBlobAsJSON", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10", "--event-store-folder", "/EventStore10"], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

<span data-ttu-id="ce202-266">parâmetros de saudação são semelhante toowhat especificada para saída de texto de saudação na etapa anterior hello.</span><span class="sxs-lookup"><span data-stu-id="ce202-266">hello parameters are similar toowhat you specified for hello text output, in hello previous step.</span></span> <span data-ttu-id="ce202-267">Novamente, não é necessário toocreate Olá pastas de saída (EventCheckpoint, EventCount/EventCount10) que são usadas como parâmetros.</span><span class="sxs-lookup"><span data-stu-id="ce202-267">Again, you do not need toocreate hello output folders (EventCheckpoint, EventCount/EventCount10) that are used as parameters.</span></span> <span data-ttu-id="ce202-268">Olá streaming aplicativo criará para você.</span><span class="sxs-lookup"><span data-stu-id="ce202-268">hello streaming application creates them for you.</span></span>

 <span data-ttu-id="ce202-269">Depois de executar o comando hello, você pode examinar sua conta de armazenamento do Azure associada Olá cluster e você deverá ver Olá **/EventStore10** pasta criada ali.</span><span class="sxs-lookup"><span data-stu-id="ce202-269">After you run hello command, you can look at your Azure storage account associated with hello cluster and you should see hello **/EventStore10** folder created there.</span></span> <span data-ttu-id="ce202-270">Abrir qualquer arquivo prefixado com **parte -** e você deve consultar eventos Olá processados em um formato JSON.</span><span class="sxs-lookup"><span data-stu-id="ce202-270">Open any file prefixed with **part-** and you should see hello events processed in a JSON format.</span></span>

### <a name="run-hello-applications-tooreceive-hello-events-into-a-hive-table"></a><span data-ttu-id="ce202-271">Executar aplicativos de saudação tooreceive eventos de saudação em uma tabela de Hive</span><span class="sxs-lookup"><span data-stu-id="ce202-271">Run hello applications tooreceive hello events into a Hive table</span></span>
<span data-ttu-id="ce202-272">Olá toorun aplicativo de transmissão Spark que eventos de fluxos em uma seção de tabela que você precisa de alguns componentes adicionais.</span><span class="sxs-lookup"><span data-stu-id="ce202-272">toorun hello Spark streaming application that streams events into a Hive table you need some additional components.</span></span> <span data-ttu-id="ce202-273">Estes são:</span><span class="sxs-lookup"><span data-stu-id="ce202-273">These are:</span></span>

* <span data-ttu-id="ce202-274">datanucleus-api-jdo-3.2.6.jar</span><span class="sxs-lookup"><span data-stu-id="ce202-274">datanucleus-api-jdo-3.2.6.jar</span></span>
* <span data-ttu-id="ce202-275">datanucleus-rdbms-3.2.9.jar</span><span class="sxs-lookup"><span data-stu-id="ce202-275">datanucleus-rdbms-3.2.9.jar</span></span>
* <span data-ttu-id="ce202-276">datanucleus-core-3.2.10.jar</span><span class="sxs-lookup"><span data-stu-id="ce202-276">datanucleus-core-3.2.10.jar</span></span>
* <span data-ttu-id="ce202-277">hive-site.xml</span><span class="sxs-lookup"><span data-stu-id="ce202-277">hive-site.xml</span></span>

<span data-ttu-id="ce202-278">Olá **. jar** arquivos estão disponíveis no seu cluster HDInsight Spark no `/usr/hdp/current/spark-client/lib`.</span><span class="sxs-lookup"><span data-stu-id="ce202-278">hello **.jar** files are available on your HDInsight Spark cluster at `/usr/hdp/current/spark-client/lib`.</span></span> <span data-ttu-id="ce202-279">Olá **hive-site.XML** está disponível em `/usr/hdp/current/spark-client/conf`.</span><span class="sxs-lookup"><span data-stu-id="ce202-279">hello **hive-site.xml** is available at `/usr/hdp/current/spark-client/conf`.</span></span>

<span data-ttu-id="ce202-280">Você pode usar [WinScp](http://winscp.net/eng/download.php) toocopy esses arquivos do computador local do hello cluster tooyour.</span><span class="sxs-lookup"><span data-stu-id="ce202-280">You can use [WinScp](http://winscp.net/eng/download.php) toocopy over these files from hello cluster tooyour local computer.</span></span> <span data-ttu-id="ce202-281">Você pode usar ferramentas toocopy esses arquivos por conta de armazenamento tooyour associados cluster hello.</span><span class="sxs-lookup"><span data-stu-id="ce202-281">You can then use tools toocopy these files over tooyour storage account associated with hello cluster.</span></span> <span data-ttu-id="ce202-282">Para obter mais informações sobre como os arquivos de tooupload toohello conta de armazenamento, consulte [carregar dados para trabalhos de Hadoop no HDInsight](hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="ce202-282">For more information on how tooupload files toohello storage account, see [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span>

<span data-ttu-id="ce202-283">Depois que você copiou em Olá arquivos tooyour conta de armazenamento do Azure, abra um prompt de comando, navegue toohello diretório onde você instalou ONDULAÇÃO e executar hello (nome de usuário/senha e cluster substituir) de comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="ce202-283">Once you have copied over hello files tooyour Azure storage account, open a command prompt, navigate toohello directory where you installed CURL, and run hello following command (replace username/password and cluster name):</span></span>

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputHive.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

<span data-ttu-id="ce202-284">Olá parâmetros no arquivo hello **inputHive.txt** são definidos da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="ce202-284">hello parameters in hello file **inputHive.txt** are defined as follows:</span></span>

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsToHiveTable", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10", "--event-hive-table", "EventHiveTable10" ], "jars":["wasb:///example/jars/datanucleus-api-jdo-3.2.6.jar", "wasb:///example/jars/datanucleus-rdbms-3.2.9.jar", "wasb:///example/jars/datanucleus-core-3.2.10.jar"], "files":["wasb:///example/jars/hive-site.xml"], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

<span data-ttu-id="ce202-285">parâmetros de saudação são semelhante toowhat especificada para saída de texto de saudação, nas etapas anteriores hello.</span><span class="sxs-lookup"><span data-stu-id="ce202-285">hello parameters are similar toowhat you specified for hello text output, in hello previous steps.</span></span> <span data-ttu-id="ce202-286">Novamente, você não precisa saída de hello toocreate pastas (EventCheckpoint, EventCount/EventCount10) ou hello tabela Hive (EventHiveTable10) que são usados como parâmetros de saída.</span><span class="sxs-lookup"><span data-stu-id="ce202-286">Again, you do not need toocreate hello output folders (EventCheckpoint, EventCount/EventCount10) or hello output Hive table (EventHiveTable10) that are used as parameters.</span></span> <span data-ttu-id="ce202-287">Olá streaming aplicativo criará para você.</span><span class="sxs-lookup"><span data-stu-id="ce202-287">hello streaming application creates them for you.</span></span> <span data-ttu-id="ce202-288">Observe que Olá **jars** e **arquivos** opção inclui arquivos do caminhos toohello. jar e hive-site.XML Olá que você copiou toohello conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="ce202-288">Note that hello **jars** and **files** option includes paths toohello .jar files and hello hive-site.xml that you copied over toohello storage account.</span></span>

<span data-ttu-id="ce202-289">tooverify que Olá tabela hive foi criado com êxito, você pode SSH em cluster hello e executadas consultas de Hive.</span><span class="sxs-lookup"><span data-stu-id="ce202-289">tooverify that hello hive table was successfully created, you can SSH into hello cluster and run Hive queries.</span></span> <span data-ttu-id="ce202-290">Para obter instruções, consulte [usar o Hive com Hadoop no HDInsight com SSH](hdinsight-hadoop-use-hive-ssh.md).</span><span class="sxs-lookup"><span data-stu-id="ce202-290">For instructions, see [Use Hive with Hadoop in HDInsight with SSH](hdinsight-hadoop-use-hive-ssh.md).</span></span> <span data-ttu-id="ce202-291">Quando você estiver conectado usando SSH, você pode executar Olá tooverify de comando a seguir essa tabela de Hive hello, **EventHiveTable10**, é criado.</span><span class="sxs-lookup"><span data-stu-id="ce202-291">Once you are connected using SSH, you can run hello following command tooverify that hello Hive table, **EventHiveTable10**, is created.</span></span>

    show tables;

<span data-ttu-id="ce202-292">Você verá uma saída semelhante toohello a seguir:</span><span class="sxs-lookup"><span data-stu-id="ce202-292">You should see an output similar toohello following:</span></span>

    OK
    eventhivetable10
    hivesampletable

<span data-ttu-id="ce202-293">Você também pode executar uma consulta SELECT tooview conteúdo de saudação da tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="ce202-293">You can also run a SELECT query tooview hello contents of hello table.</span></span>

    SELECT * FROM eventhivetable10 LIMIT 10;

<span data-ttu-id="ce202-294">Você verá uma saída semelhante Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="ce202-294">You should see an output like hello following:</span></span>

    ZN90apUSQODDTx7n6Toh6jDbuPngqT4c
    sor2M7xsFwmaRW8W8NDwMneFNMrOVkW1
    o2HcsU735ejSi2bGEcbUSB4btCFmI1lW
    TLuibq4rbj0T9st9eEzIWJwNGtMWYoYS
    HKCpPlWFWAJILwR69MAq863nCWYzDEw6
    Mvx0GQOPYvPR7ezBEpIHYKTKiEhYammQ
    85dRppSBSbZgThLr1s0GMgKqynDUqudr
    5LAWkNqorLj3ZN9a2mfWr9rZqeXKN4pF
    ulf9wSFNjD7BZXCyunozecov9QpEIYmJ
    vWzM3nvOja8DhYcwn0n5eTfOItZ966pa
    Time taken: 4.434 seconds, Fetched: 10 row(s)


### <a name="run-hello-applications-tooreceive-hello-events-into-an-azure-sql-database-table"></a><span data-ttu-id="ce202-295">Executar aplicativos de saudação tooreceive eventos de saudação em uma tabela de banco de dados do SQL Azure</span><span class="sxs-lookup"><span data-stu-id="ce202-295">Run hello applications tooreceive hello events into an Azure SQL database table</span></span>
<span data-ttu-id="ce202-296">Antes de executar essa etapa, verifique se que você tem um banco de dados SQL Azure criado.</span><span class="sxs-lookup"><span data-stu-id="ce202-296">Before running this step, make sure you have an Azure SQL database created.</span></span> <span data-ttu-id="ce202-297">Para obter instruções, consulte [Criar um banco de dados SQL em minutos](../sql-database/sql-database-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="ce202-297">For instructions, see [Create a SQL database in minutes](../sql-database/sql-database-get-started.md).</span></span> <span data-ttu-id="ce202-298">toocomplete seção, você precisa valores para o nome do banco de dados, nome do servidor de banco de dados e credenciais de administrador de banco de dados hello como parâmetros.</span><span class="sxs-lookup"><span data-stu-id="ce202-298">toocomplete this section, you need values for database name, database server name, and hello database administrator credentials as parameters.</span></span> <span data-ttu-id="ce202-299">Tabela de banco de dados de saudação toocreate não é necessário embora.</span><span class="sxs-lookup"><span data-stu-id="ce202-299">You do not need toocreate hello database table though.</span></span> <span data-ttu-id="ce202-300">Olá aplicativo streaming Spark que cria para você.</span><span class="sxs-lookup"><span data-stu-id="ce202-300">hello Spark streaming application creates that for you.</span></span>

<span data-ttu-id="ce202-301">Abra um prompt de comando, navegue toohello diretório onde você instalou ONDULAÇÃO e executar Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="ce202-301">Open a command prompt, navigate toohello directory where you installed CURL, and run hello following command:</span></span>

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputSQL.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

<span data-ttu-id="ce202-302">Olá parâmetros no arquivo hello **inputSQL.txt** são definidos da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="ce202-302">hello parameters in hello file **inputSQL.txt** are defined as follows:</span></span>

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsToAzureSQLTable", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10", "--sql-server-fqdn", "<database-server-name>.database.windows.net", "--sql-database-name", "mysparkdatabase", "--database-username", "sparkdbadmin", "--database-password", "<put-password-here>", "--event-sql-table", "EventContent" ], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

<span data-ttu-id="ce202-303">tooverify que Olá aplicativo é executado com êxito, você pode se conectar a banco de dados do SQL Azure toohello usando o SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="ce202-303">tooverify that hello application runs successfully, you can connect toohello Azure SQL database using SQL Server Management Studio.</span></span> <span data-ttu-id="ce202-304">Para obter instruções sobre como toodo que, consulte [conectar tooSQL banco de dados com o SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md).</span><span class="sxs-lookup"><span data-stu-id="ce202-304">For instructions on how toodo that, see [Connect tooSQL Database with SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md).</span></span> <span data-ttu-id="ce202-305">Quando você estiver conectado toohello banco de dados, você poderá navegar toohello **EventContent** tabela que foi criada pelo Olá streaming de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="ce202-305">Once you are connected toohello database, you can navigate toohello **EventContent** table that was created by hello streaming application.</span></span> <span data-ttu-id="ce202-306">Você pode executar uma consulta rápida tooget Olá de dados da tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="ce202-306">You can run a quick query tooget hello data from hello table.</span></span> <span data-ttu-id="ce202-307">Execute Olá consulta a seguir:</span><span class="sxs-lookup"><span data-stu-id="ce202-307">Run hello following query:</span></span>

    SELECT * FROM EventCount

<span data-ttu-id="ce202-308">Você deve ver o seguinte de toohello semelhante de saída:</span><span class="sxs-lookup"><span data-stu-id="ce202-308">You should see output similar toohello following:</span></span>

    00046b0f-2552-4980-9c3f-8bba5647c8ee
    000b7530-12f9-4081-8e19-90acd26f9c0c
    000bc521-9c1b-4a42-ab08-dc1893b83f3b
    00123a2a-e00d-496a-9104-108920955718
    0017c68f-7a4e-452d-97ad-5cb1fe5ba81b
    001KsmqL2gfu5ZcuQuTqTxQvVyGCqPp9
    001vIZgOStka4DXtud0e3tX7XbfMnZrN
    00220586-3e1a-4d2d-a89b-05c5892e541a
    0029e309-9e54-4e1b-84be-cd04e6fce5ec
    003333cf-874f-4045-9da3-9f98c2b4ea49
    0043c07e-8d73-420a-9af7-1fcb94575356
    004a11a9-0c2c-4bc0-a7d5-2e0ebd947ab9


## <span data-ttu-id="ce202-309"><a name="seealso"></a>Consulte também</span><span class="sxs-lookup"><span data-stu-id="ce202-309"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="ce202-310">Visão geral: Apache Spark no Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="ce202-310">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)
* [<span data-ttu-id="ce202-311">Design de Conexão com Base no Receptor e Direct DStream</span><span class="sxs-lookup"><span data-stu-id="ce202-311">Design of Receiver-based Connection and Direct DStream</span></span>](https://www.slideshare.net/NanZhu/seattle-sparkmeetup032317)

### <a name="scenarios"></a><span data-ttu-id="ce202-312">Cenários</span><span class="sxs-lookup"><span data-stu-id="ce202-312">Scenarios</span></span>
* [<span data-ttu-id="ce202-313">Spark com BI: executar análise de dados interativa usando o Spark no HDInsight com ferramentas de BI</span><span class="sxs-lookup"><span data-stu-id="ce202-313">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="ce202-314">Spark com Aprendizado de Máquina: usar o Spark no HDInsight para analisar a temperatura de prédios usando dados do sistema HVAC</span><span class="sxs-lookup"><span data-stu-id="ce202-314">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="ce202-315">Spark com o aprendizado de máquina: Use Spark nos resultados de inspeção de alimentos HDInsight toopredict</span><span class="sxs-lookup"><span data-stu-id="ce202-315">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="ce202-316">Análise de log do site usando o Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="ce202-316">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="ce202-317">Criar e executar aplicativos</span><span class="sxs-lookup"><span data-stu-id="ce202-317">Create and run applications</span></span>
* [<span data-ttu-id="ce202-318">Criar um aplicativo autônomo usando Scala</span><span class="sxs-lookup"><span data-stu-id="ce202-318">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="ce202-319">Executar trabalhos remotamente em um cluster do Spark usando Livy</span><span class="sxs-lookup"><span data-stu-id="ce202-319">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="ce202-320">Ferramentas e extensões</span><span class="sxs-lookup"><span data-stu-id="ce202-320">Tools and extensions</span></span>
* [<span data-ttu-id="ce202-321">Usar o plug-in de ferramentas de HDInsight para toocreate IntelliJ IDEIA e enviar maiores Spark Scala aplicativos</span><span class="sxs-lookup"><span data-stu-id="ce202-321">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="ce202-322">Usar o plug-in de ferramentas de HDInsight para aplicativos de Spark toodebug IntelliJ IDEIA remotamente</span><span class="sxs-lookup"><span data-stu-id="ce202-322">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="ce202-323">Usar blocos de anotações do Zeppelin com um cluster Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="ce202-323">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="ce202-324">Kernels disponíveis para o bloco de anotações Jupyter no cluster do Spark para HDInsight</span><span class="sxs-lookup"><span data-stu-id="ce202-324">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="ce202-325">Usar pacotes externos com blocos de notas Jupyter</span><span class="sxs-lookup"><span data-stu-id="ce202-325">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="ce202-326">Instalar Jupyter em seu computador e conecte-se tooan cluster HDInsight Spark</span><span class="sxs-lookup"><span data-stu-id="ce202-326">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="ce202-327">Gerenciar recursos</span><span class="sxs-lookup"><span data-stu-id="ce202-327">Manage resources</span></span>
* [<span data-ttu-id="ce202-328">Gerenciar os recursos de cluster do hello Apache Spark no HDInsight do Azure</span><span class="sxs-lookup"><span data-stu-id="ce202-328">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="ce202-329">Rastrear e depurar trabalhos em execução em um cluster do Apache Spark no HDInsight</span><span class="sxs-lookup"><span data-stu-id="ce202-329">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]: ../storage-create-storage-account/
