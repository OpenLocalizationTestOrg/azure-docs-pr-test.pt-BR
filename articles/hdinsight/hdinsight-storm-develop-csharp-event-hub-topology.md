---
title: eventos de aaaProcess dos Hubs de eventos com Storm - HDInsight do Azure | Microsoft Docs
description: "Saiba como tooprocess dados de Hubs de eventos do Azure com uma topologia c# Storm criados no Visual Studio, usando Olá ferramentas HDInsight para Visual Studio."
services: hdinsight,notification hubs
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 67f9d08c-eea0-401b-952b-db765655dad0
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/03/2017
ms.author: larryfr
ms.openlocfilehash: 30cd910d80eba066f283197bcbbaf11145bc5524
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="process-events-from-azure-event-hubs-with-storm-on-hdinsight-c"></a><span data-ttu-id="fb678-103">Processar eventos dos Hubs de Eventos do Azure com o Storm no HDInsight (C#)</span><span class="sxs-lookup"><span data-stu-id="fb678-103">Process events from Azure Event Hubs with Storm on HDInsight (C#)</span></span>

<span data-ttu-id="fb678-104">Saiba como toowork com Hubs de eventos do Azure do Apache Storm no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="fb678-104">Learn how toowork with Azure Event Hubs from Apache Storm on HDInsight.</span></span> <span data-ttu-id="fb678-105">Este documento usa um c# Storm topologia tooread e gravar dados de Hubs Evbent</span><span class="sxs-lookup"><span data-stu-id="fb678-105">This document uses a C# Storm topology tooread and write data from Evbent Hubs</span></span>

> [!NOTE]
> <span data-ttu-id="fb678-106">Para uma versão Java desse projeto, veja [Processar eventos dos Hubs de Eventos do Azure com o Storm no HDInsight (Java)](hdinsight-storm-develop-java-event-hub-topology.md).</span><span class="sxs-lookup"><span data-stu-id="fb678-106">For a Java version of this project, see [Process events from Azure Event Hubs with Storm on HDInsight (Java)](hdinsight-storm-develop-java-event-hub-topology.md).</span></span>

## <a name="scpnet"></a><span data-ttu-id="fb678-107">SCP.NET</span><span class="sxs-lookup"><span data-stu-id="fb678-107">SCP.NET</span></span>

<span data-ttu-id="fb678-108">Olá etapas deste documento usam SCP.NET, um pacote do NuGet que torna mais fácil toocreate c# topologias e componentes para usar com Storm no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="fb678-108">hello steps in this document use SCP.NET, a NuGet package that makes it easy toocreate C# topologies and components for use with Storm on HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fb678-109">Enquanto Olá as etapas neste documento dependem de um ambiente de desenvolvimento do Windows com o Visual Studio, projeto compilado Olá pode ser enviado tooa Storm no cluster HDInsight que usa o Linux.</span><span class="sxs-lookup"><span data-stu-id="fb678-109">While hello steps in this document rely on a Windows development environment with Visual Studio, hello compiled project can be submitted tooa Storm on HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="fb678-110">Somente os clusters baseados em Linux criados depois de 28 de outubro de 2016 são compatíveis com as topologias do SCP.NET.</span><span class="sxs-lookup"><span data-stu-id="fb678-110">Only Linux-based clusters created after October 28, 2016, support SCP.NET topologies.</span></span>

<span data-ttu-id="fb678-111">HDInsight 3.4 e topologias de toorun Mono c# uso maiores.</span><span class="sxs-lookup"><span data-stu-id="fb678-111">HDInsight 3.4 and greater use Mono toorun C# topologies.</span></span> <span data-ttu-id="fb678-112">exemplo Hello usado neste documento funciona com HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="fb678-112">hello example used in this document works with HDInsight 3.6.</span></span> <span data-ttu-id="fb678-113">Se você planeja criar suas próprias soluções de .NET para HDInsight, verifique Olá [compatibilidade Mono](http://www.mono-project.com/docs/about-mono/compatibility/) documento para incompatibilidades.</span><span class="sxs-lookup"><span data-stu-id="fb678-113">If you plan on creating your own .NET solutions for HDInsight, check hello [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/) document for potential incompatibilities.</span></span>

### <a name="cluster-versioning"></a><span data-ttu-id="fb678-114">Controle de versão do cluster</span><span class="sxs-lookup"><span data-stu-id="fb678-114">Cluster versioning</span></span>

<span data-ttu-id="fb678-115">Olá pacote Microsoft.SCP.Net.SDK NuGet usado para o seu projeto deve corresponder a versão principal de saudação do Storm instalado no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="fb678-115">hello Microsoft.SCP.Net.SDK NuGet package you use for your project must match hello major version of Storm installed on HDInsight.</span></span> <span data-ttu-id="fb678-116">As versões 3.5 e 3.6 do HDInsight usam o Storm 1.x, assim, você deve usar a versão 1.0.x.x do SCP.NET com esses clusters.</span><span class="sxs-lookup"><span data-stu-id="fb678-116">HDInsight versions 3.5 and 3.6 use Storm 1.x, so you must use SCP.NET version 1.0.x.x with these clusters.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fb678-117">exemplo Hello neste documento espera um 3.5 HDInsight ou cluster 3.6.</span><span class="sxs-lookup"><span data-stu-id="fb678-117">hello example in this document expects an HDInsight 3.5 or 3.6 cluster.</span></span>
>
> <span data-ttu-id="fb678-118">Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="fb678-118">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="fb678-119">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="fb678-119">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="fb678-120">As topologias C# também devem ser destinadas ao .NET 4.5.</span><span class="sxs-lookup"><span data-stu-id="fb678-120">C# topologies must also target .NET 4.5.</span></span>

## <a name="how-toowork-with-event-hubs"></a><span data-ttu-id="fb678-121">Como toowork com Hubs de eventos</span><span class="sxs-lookup"><span data-stu-id="fb678-121">How toowork with Event Hubs</span></span>

<span data-ttu-id="fb678-122">A Microsoft fornece um conjunto de componentes de Java que podem ser usado toocommunicate com Hubs de eventos de uma topologia de profusão.</span><span class="sxs-lookup"><span data-stu-id="fb678-122">Microsoft provides a set of Java components that can be used toocommunicate with Event Hubs from a Storm topology.</span></span> <span data-ttu-id="fb678-123">Você pode encontrar hello Java (arquivo JAR) que contém uma versão compatível do HDInsight 3.6 desses componentes em [https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar](https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar).</span><span class="sxs-lookup"><span data-stu-id="fb678-123">You can find hello Java archive (JAR) file that contains an HDInsight 3.6 compatible version of these components at [https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar](https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fb678-124">Enquanto os componentes de saudação são escritos em Java, você pode usá-los facilmente de uma topologia de c#.</span><span class="sxs-lookup"><span data-stu-id="fb678-124">While hello components are written in Java, you can easily use them from a C# topology.</span></span>

<span data-ttu-id="fb678-125">Olá componentes a seguir é usado neste exemplo:</span><span class="sxs-lookup"><span data-stu-id="fb678-125">hello following components are used in this example:</span></span>

* <span data-ttu-id="fb678-126">__EventHubSpout__: lê dados nos Hubs de Eventos.</span><span class="sxs-lookup"><span data-stu-id="fb678-126">__EventHubSpout__: Reads data from Event Hubs.</span></span>
* <span data-ttu-id="fb678-127">__EventHubBolt__: grava dados tooEvent Hubs.</span><span class="sxs-lookup"><span data-stu-id="fb678-127">__EventHubBolt__: Writes data tooEvent Hubs.</span></span>
* <span data-ttu-id="fb678-128">__EventHubSpoutConfig__: usado tooconfigure EventHubSpout.</span><span class="sxs-lookup"><span data-stu-id="fb678-128">__EventHubSpoutConfig__: Used tooconfigure EventHubSpout.</span></span>
* <span data-ttu-id="fb678-129">__EventHubBoltConfig__: usado tooconfigure EventHubBolt.</span><span class="sxs-lookup"><span data-stu-id="fb678-129">__EventHubBoltConfig__: Used tooconfigure EventHubBolt.</span></span>

### <a name="example-spout-usage"></a><span data-ttu-id="fb678-130">Exemplo de uso do spout</span><span class="sxs-lookup"><span data-stu-id="fb678-130">Example spout usage</span></span>

<span data-ttu-id="fb678-131">SCP.NET fornece métodos para adicionar uma topologia de tooyour EventHubSpout.</span><span class="sxs-lookup"><span data-stu-id="fb678-131">SCP.NET provides methods for adding an EventHubSpout tooyour topology.</span></span> <span data-ttu-id="fb678-132">Esses métodos tornam mais fácil tooadd um spout que o uso de métodos genéricos Olá para adicionar um componente de Java.</span><span class="sxs-lookup"><span data-stu-id="fb678-132">These methods make it easier tooadd a spout than using hello generic methods for adding a Java component.</span></span> <span data-ttu-id="fb678-133">Olá exemplo a seguir demonstra como toocreate uma spout usando Olá __SetEventHubSpout__ e **EventHubSpoutConfig** métodos fornecidos pelo SCP.NET:</span><span class="sxs-lookup"><span data-stu-id="fb678-133">hello following example demonstrates how toocreate a spout by using hello __SetEventHubSpout__ and **EventHubSpoutConfig** methods provided by SCP.NET:</span></span>

```csharp
 topologyBuilder.SetEventHubSpout(
    "EventHubSpout",
    new EventHubSpoutConfig(
        ConfigurationManager.AppSettings["EventHubSharedAccessKeyName"],
        ConfigurationManager.AppSettings["EventHubSharedAccessKey"],
        ConfigurationManager.AppSettings["EventHubNamespace"],
        ConfigurationManager.AppSettings["EventHubEntityPath"],
        eventHubPartitions),
    eventHubPartitions);
```

<span data-ttu-id="fb678-134">exemplo anterior Hello cria um novo componente spout chamado __EventHubSpout__e configura toocommunicate com um hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="fb678-134">hello previous example creates a new spout component named __EventHubSpout__, and configures it toocommunicate with an event hub.</span></span> <span data-ttu-id="fb678-135">Dica de paralelismo Olá para o componente de saudação é definida toohello número de partições no hub de eventos de saudação.</span><span class="sxs-lookup"><span data-stu-id="fb678-135">hello parallelism hint for hello component is set toohello number of partitions in hello event hub.</span></span> <span data-ttu-id="fb678-136">Essa configuração permite Storm toocreate uma instância do componente de saudação para cada partição.</span><span class="sxs-lookup"><span data-stu-id="fb678-136">This setting allows Storm toocreate an instance of hello component for each partition.</span></span>

### <a name="example-bolt-usage"></a><span data-ttu-id="fb678-137">Exemplo de uso de bolt</span><span class="sxs-lookup"><span data-stu-id="fb678-137">Example bolt usage</span></span>

<span data-ttu-id="fb678-138">Saudação de uso **JavaComponmentConstructor** método toocreate uma instância do raio da saudação.</span><span class="sxs-lookup"><span data-stu-id="fb678-138">Use hello **JavaComponmentConstructor** method toocreate an instance of hello bolt.</span></span> <span data-ttu-id="fb678-139">Olá exemplo a seguir demonstra como toocreate e configurar uma nova instância da saudação **EventHubBolt**:</span><span class="sxs-lookup"><span data-stu-id="fb678-139">hello following example demonstrates how toocreate and configure a new instance of hello **EventHubBolt**:</span></span>

```csharp
// Java construcvtor for hello Event Hub Bolt
JavaComponentConstructor constructor = JavaComponentConstructor.CreateFromClojureExpr(
    String.Format(@"(org.apache.storm.eventhubs.bolt.EventHubBolt. (org.apache.storm.eventhubs.bolt.EventHubBoltConfig. " +
        @"""{0}"" ""{1}"" ""{2}"" ""{3}"" ""{4}"" {5}))",
        ConfigurationManager.AppSettings["EventHubPolicyName"],
        ConfigurationManager.AppSettings["EventHubPolicyKey"],
        ConfigurationManager.AppSettings["EventHubNamespace"],
        "servicebus.windows.net",
        ConfigurationManager.AppSettings["EventHubName"],
        "true"));

// Set hello bolt toosubscribe toodata from hello spout
topologyBuilder.SetJavaBolt(
    "eventhubbolt",
    constructor,
    partitionCount)
        .shuffleGrouping("Spout");
```

> [!NOTE]
> <span data-ttu-id="fb678-140">Este exemplo usa uma expressão de Clojure passada como uma cadeia de caracteres, em vez de usar **JavaComponentConstructor** toocreate um **EventHubBoltConfig**, como exemplo de spout hello fez.</span><span class="sxs-lookup"><span data-stu-id="fb678-140">This example uses a Clojure expression passed as a string, instead of using **JavaComponentConstructor** toocreate an **EventHubBoltConfig**, as hello spout example did.</span></span> <span data-ttu-id="fb678-141">Ambos os métodos funcionam.</span><span class="sxs-lookup"><span data-stu-id="fb678-141">Either method works.</span></span> <span data-ttu-id="fb678-142">Use o método hello parece tooyou melhor.</span><span class="sxs-lookup"><span data-stu-id="fb678-142">Use hello method that feels best tooyou.</span></span>

## <a name="download-hello-completed-project"></a><span data-ttu-id="fb678-143">Baixe o projeto de saudação concluída</span><span class="sxs-lookup"><span data-stu-id="fb678-143">Download hello completed project</span></span>

<span data-ttu-id="fb678-144">Você pode baixar uma versão completa do projeto Olá criado neste tutorial de [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span><span class="sxs-lookup"><span data-stu-id="fb678-144">You can download a complete version of hello project created in this tutorial from [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span></span> <span data-ttu-id="fb678-145">No entanto, você ainda precisa tooprovide configurações seguindo as etapas de saudação neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="fb678-145">However, you still need tooprovide configuration settings by following hello steps in this tutorial.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="fb678-146">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="fb678-146">Prerequisites</span></span>

* <span data-ttu-id="fb678-147">Um [Apache Storm no cluster HDInsight versão 3.5 ou 3.6](hdinsight-apache-storm-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="fb678-147">An [Apache Storm on HDInsight cluster version 3.5 or 3.6](hdinsight-apache-storm-tutorial-get-started.md).</span></span>

    > [!WARNING]
    > <span data-ttu-id="fb678-148">exemplo Hello usado neste documento requer Storm no HDInsight versão 3.5 ou 3.6.</span><span class="sxs-lookup"><span data-stu-id="fb678-148">hello example used in this document requires Storm on HDInsight version 3.5 or 3.6.</span></span> <span data-ttu-id="fb678-149">Isso não funciona com versões anteriores do HDInsight, devido a alterações de nome de classe toobreaking.</span><span class="sxs-lookup"><span data-stu-id="fb678-149">This does not work with older versions of HDInsight, due toobreaking class name changes.</span></span> <span data-ttu-id="fb678-150">Para obter uma versão desse exemplo que funcione com clusters mais antigos, consulte [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub/releases).</span><span class="sxs-lookup"><span data-stu-id="fb678-150">For a version of this example that works with older clusters, see [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub/releases).</span></span>

* <span data-ttu-id="fb678-151">Um [Hub de eventos do Azure](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).</span><span class="sxs-lookup"><span data-stu-id="fb678-151">An [Azure event hub](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).</span></span>

* <span data-ttu-id="fb678-152">Olá [SDK .NET do Azure](http://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="fb678-152">hello [Azure .NET SDK](http://azure.microsoft.com/downloads/).</span></span>

* <span data-ttu-id="fb678-153">Olá [ferramentas HDInsight para Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="fb678-153">hello [HDInsight tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

* <span data-ttu-id="fb678-154">Java JDK 1.8 ou posterior em seu ambiente de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="fb678-154">Java JDK 1.8 or later on your development environment.</span></span> <span data-ttu-id="fb678-155">Downloads de JDK estão disponíveis na [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span><span class="sxs-lookup"><span data-stu-id="fb678-155">JDK downloads are available from [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span></span>

  * <span data-ttu-id="fb678-156">Olá **JAVA_HOME** diretório de toohello de ponto de deve variável de ambiente que contém Java.</span><span class="sxs-lookup"><span data-stu-id="fb678-156">hello **JAVA_HOME** environment variable must point toohello directory that contains Java.</span></span>
  * <span data-ttu-id="fb678-157">Olá **%JAVA_HOME%/bin** diretório deve estar no caminho de saudação.</span><span class="sxs-lookup"><span data-stu-id="fb678-157">hello **%JAVA_HOME%/bin** directory must be in hello path.</span></span>

## <a name="download-hello-event-hubs-components"></a><span data-ttu-id="fb678-158">Baixar os componentes de Hubs de eventos Olá</span><span class="sxs-lookup"><span data-stu-id="fb678-158">Download hello Event Hubs components</span></span>

<span data-ttu-id="fb678-159">Saudação de download dos Hubs de eventos spout e incluem o componente de [https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar](https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar).</span><span class="sxs-lookup"><span data-stu-id="fb678-159">Download hello Event Hubs spout and bolt component from [https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar](https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar).</span></span>

<span data-ttu-id="fb678-160">Crie um diretório chamado `eventhubspout`e salve o arquivo de saudação no diretório de saudação.</span><span class="sxs-lookup"><span data-stu-id="fb678-160">Create a directory named `eventhubspout`, and save hello file into hello directory.</span></span>

## <a name="configure-event-hubs"></a><span data-ttu-id="fb678-161">Configurar os Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="fb678-161">Configure Event Hubs</span></span>

<span data-ttu-id="fb678-162">Hubs de eventos é a fonte de dados de saudação para este exemplo.</span><span class="sxs-lookup"><span data-stu-id="fb678-162">Event Hubs is hello data source for this example.</span></span> <span data-ttu-id="fb678-163">Use informações de saudação na seção "Criar um hub de eventos" de saudação do [Introdução aos Hubs de eventos](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).</span><span class="sxs-lookup"><span data-stu-id="fb678-163">Use hello information in hello "Create an event hub" section of [Get started with Event Hubs](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).</span></span>

1. <span data-ttu-id="fb678-164">Depois que o hub de eventos Olá tiver sido criado, exibir hello **EventHub** folha em hello Azure portal e selecione **políticas de acesso compartilhado**.</span><span class="sxs-lookup"><span data-stu-id="fb678-164">After hello event hub has been created, view hello **EventHub** blade in hello Azure portal, and select **Shared access policies**.</span></span> <span data-ttu-id="fb678-165">Selecione **+ adicionar** tooadd Olá políticas a seguir:</span><span class="sxs-lookup"><span data-stu-id="fb678-165">Select **+ Add** tooadd hello following policies:</span></span>

   | <span data-ttu-id="fb678-166">Nome</span><span class="sxs-lookup"><span data-stu-id="fb678-166">Name</span></span> | <span data-ttu-id="fb678-167">Permissões</span><span class="sxs-lookup"><span data-stu-id="fb678-167">Permissions</span></span> |
   | --- | --- |
   | <span data-ttu-id="fb678-168">gravador</span><span class="sxs-lookup"><span data-stu-id="fb678-168">writer</span></span> |<span data-ttu-id="fb678-169">Enviar</span><span class="sxs-lookup"><span data-stu-id="fb678-169">Send</span></span> |
   | <span data-ttu-id="fb678-170">leitor</span><span class="sxs-lookup"><span data-stu-id="fb678-170">reader</span></span> |<span data-ttu-id="fb678-171">Escutar</span><span class="sxs-lookup"><span data-stu-id="fb678-171">Listen</span></span> |

    ![Captura de tela da janela Políticas de acesso compartilhadas](./media/hdinsight-storm-develop-csharp-event-hub-topology/sas.png)

2. <span data-ttu-id="fb678-173">Selecione Olá **leitor** e **gravador** políticas.</span><span class="sxs-lookup"><span data-stu-id="fb678-173">Select hello **reader** and **writer** policies.</span></span> <span data-ttu-id="fb678-174">Copie e salve o valor de chave primária Olá para ambas as políticas, pois esses valores são usados mais tarde.</span><span class="sxs-lookup"><span data-stu-id="fb678-174">Copy and save hello primary key value for both policies, as these values are used later.</span></span>

## <a name="configure-hello-eventhubwriter"></a><span data-ttu-id="fb678-175">Configurar Olá EventHubWriter</span><span class="sxs-lookup"><span data-stu-id="fb678-175">Configure hello EventHubWriter</span></span>

1. <span data-ttu-id="fb678-176">Se já não tiver instalado a versão mais recente Olá das ferramentas do HDInsight Olá para o Visual Studio, consulte [começar a usar as ferramentas do HDInsight para Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="fb678-176">If you have not already installed hello latest version of hello HDInsight tools for Visual Studio, see [Get started using HDInsight tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

2. <span data-ttu-id="fb678-177">Baixar a solução de saudação do [eventhub de profusão de híbrida](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span><span class="sxs-lookup"><span data-stu-id="fb678-177">Download hello solution from [eventhub-storm-hybrid](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span></span>

3. <span data-ttu-id="fb678-178">Em Olá **EventHubWriter** projeto, abra Olá **App. config** arquivo.</span><span class="sxs-lookup"><span data-stu-id="fb678-178">In hello **EventHubWriter** project, open hello **App.config** file.</span></span> <span data-ttu-id="fb678-179">Use as informações de saudação do hub de eventos de saudação que você configurou anteriormente toofill no valor Olá Olá chaves a seguir:</span><span class="sxs-lookup"><span data-stu-id="fb678-179">Use hello information from hello event hub that you configured earlier toofill in hello value for hello following keys:</span></span>

   | <span data-ttu-id="fb678-180">Chave</span><span class="sxs-lookup"><span data-stu-id="fb678-180">Key</span></span> | <span data-ttu-id="fb678-181">Valor</span><span class="sxs-lookup"><span data-stu-id="fb678-181">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="fb678-182">EventHubPolicyName</span><span class="sxs-lookup"><span data-stu-id="fb678-182">EventHubPolicyName</span></span> |<span data-ttu-id="fb678-183">gravador (se você usou um nome diferente para a política de saudação com *enviar* permissão, usá-lo em vez disso.)</span><span class="sxs-lookup"><span data-stu-id="fb678-183">writer (If you used a different name for hello policy with *Send* permission, use it instead.)</span></span> |
   | <span data-ttu-id="fb678-184">EventHubPolicyKey</span><span class="sxs-lookup"><span data-stu-id="fb678-184">EventHubPolicyKey</span></span> |<span data-ttu-id="fb678-185">chave de saudação para política de gravador hello.</span><span class="sxs-lookup"><span data-stu-id="fb678-185">hello key for hello writer policy.</span></span> |
   | <span data-ttu-id="fb678-186">EventHubNamespace</span><span class="sxs-lookup"><span data-stu-id="fb678-186">EventHubNamespace</span></span> |<span data-ttu-id="fb678-187">Olá namespace que contém o hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="fb678-187">hello namespace that contains your event hub.</span></span> |
   | <span data-ttu-id="fb678-188">EventHubName</span><span class="sxs-lookup"><span data-stu-id="fb678-188">EventHubName</span></span> |<span data-ttu-id="fb678-189">O nome do hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="fb678-189">Your event hub name.</span></span> |
   | <span data-ttu-id="fb678-190">EventHubPartitionCount</span><span class="sxs-lookup"><span data-stu-id="fb678-190">EventHubPartitionCount</span></span> |<span data-ttu-id="fb678-191">número de saudação de partições em seu hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="fb678-191">hello number of partitions in your event hub.</span></span> |

4. <span data-ttu-id="fb678-192">Salve e feche o hello **App. config** arquivo.</span><span class="sxs-lookup"><span data-stu-id="fb678-192">Save and close hello **App.config** file.</span></span>

## <a name="configure-hello-eventhubreader"></a><span data-ttu-id="fb678-193">Configurar Olá EventHubReader</span><span class="sxs-lookup"><span data-stu-id="fb678-193">Configure hello EventHubReader</span></span>

1. <span data-ttu-id="fb678-194">Olá abrir **EventHubReader** projeto.</span><span class="sxs-lookup"><span data-stu-id="fb678-194">Open hello **EventHubReader** project.</span></span>

2. <span data-ttu-id="fb678-195">Olá abrir **App. config** arquivo hello **EventHubReader**.</span><span class="sxs-lookup"><span data-stu-id="fb678-195">Open hello **App.config** file for hello **EventHubReader**.</span></span> <span data-ttu-id="fb678-196">Use as informações de saudação do hub de eventos de saudação que você configurou anteriormente toofill no valor Olá Olá chaves a seguir:</span><span class="sxs-lookup"><span data-stu-id="fb678-196">Use hello information from hello event hub that you configured earlier toofill in hello value for hello following keys:</span></span>

   | <span data-ttu-id="fb678-197">Chave</span><span class="sxs-lookup"><span data-stu-id="fb678-197">Key</span></span> | <span data-ttu-id="fb678-198">Valor</span><span class="sxs-lookup"><span data-stu-id="fb678-198">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="fb678-199">EventHubPolicyName</span><span class="sxs-lookup"><span data-stu-id="fb678-199">EventHubPolicyName</span></span> |<span data-ttu-id="fb678-200">leitor (se você usou um nome diferente para a política de saudação com *escutar* permissão, usá-lo em vez disso.)</span><span class="sxs-lookup"><span data-stu-id="fb678-200">reader (If you used a different name for hello policy with *listen* permission, use it instead.)</span></span> |
   | <span data-ttu-id="fb678-201">EventHubPolicyKey</span><span class="sxs-lookup"><span data-stu-id="fb678-201">EventHubPolicyKey</span></span> |<span data-ttu-id="fb678-202">chave de saudação para política de leitor de saudação.</span><span class="sxs-lookup"><span data-stu-id="fb678-202">hello key for hello reader policy.</span></span> |
   | <span data-ttu-id="fb678-203">EventHubNamespace</span><span class="sxs-lookup"><span data-stu-id="fb678-203">EventHubNamespace</span></span> |<span data-ttu-id="fb678-204">Olá namespace que contém o hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="fb678-204">hello namespace that contains your event hub.</span></span> |
   | <span data-ttu-id="fb678-205">EventHubName</span><span class="sxs-lookup"><span data-stu-id="fb678-205">EventHubName</span></span> |<span data-ttu-id="fb678-206">O nome do hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="fb678-206">Your event hub name.</span></span> |
   | <span data-ttu-id="fb678-207">EventHubPartitionCount</span><span class="sxs-lookup"><span data-stu-id="fb678-207">EventHubPartitionCount</span></span> |<span data-ttu-id="fb678-208">número de saudação de partições em seu hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="fb678-208">hello number of partitions in your event hub.</span></span> |

3. <span data-ttu-id="fb678-209">Salve e feche o hello **App. config** arquivo.</span><span class="sxs-lookup"><span data-stu-id="fb678-209">Save and close hello **App.config** file.</span></span>

## <a name="deploy-hello-topologies"></a><span data-ttu-id="fb678-210">Implantar topologias Olá</span><span class="sxs-lookup"><span data-stu-id="fb678-210">Deploy hello topologies</span></span>

1. <span data-ttu-id="fb678-211">De **Gerenciador de soluções**, Olá atalho **EventHubReader** do projeto e selecione **enviar tooStorm no HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="fb678-211">From **Solution Explorer**, right-click hello **EventHubReader** project, and select **Submit tooStorm on HDInsight**.</span></span>

    ![Captura de tela do Gerenciador de soluções, com enviar tooStorm no HDInsight realçado](./media/hdinsight-storm-develop-csharp-event-hub-topology/submittostorm.png)

2. <span data-ttu-id="fb678-213">Em Olá **topologia enviar** caixa de diálogo, selecione seu **Cluster Storm**.</span><span class="sxs-lookup"><span data-stu-id="fb678-213">On hello **Submit Topology** dialog box, select your **Storm Cluster**.</span></span> <span data-ttu-id="fb678-214">Expanda **configurações adicionais**, selecione **caminhos de arquivo Java**, selecione **...** e selecione Olá diretório que contém o arquivo JAR Olá que você baixou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="fb678-214">Expand **Additional Configurations**, select **Java File Paths**, select **...**, and select hello directory that contains hello JAR file that you downloaded earlier.</span></span> <span data-ttu-id="fb678-215">Por fim, clique em **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="fb678-215">Finally, click **Submit**.</span></span>

    ![Captura de tela da caixa de diálogo Enviar Topologia](./media/hdinsight-storm-develop-csharp-event-hub-topology/submit.png)

3. <span data-ttu-id="fb678-217">Quando a topologia de saudação tiver sido enviada, Olá **Storm topologias visualizador** é exibida.</span><span class="sxs-lookup"><span data-stu-id="fb678-217">When hello topology has been submitted, hello **Storm Topologies Viewer** appears.</span></span> <span data-ttu-id="fb678-218">tooview informações sobre topologia hello, selecione Olá **EventHubReader** topologia no painel esquerdo da saudação.</span><span class="sxs-lookup"><span data-stu-id="fb678-218">tooview information about hello topology, select hello **EventHubReader** topology in hello left pane.</span></span>

    ![Captura de tela do Visualizador de Topologias do Storm](./media/hdinsight-storm-develop-csharp-event-hub-topology/topologyviewer.png)

4. <span data-ttu-id="fb678-220">De **Gerenciador de soluções**, Olá atalho **EventHubWriter** do projeto e selecione **enviar tooStorm no HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="fb678-220">From **Solution Explorer**, right-click hello **EventHubWriter** project, and select **Submit tooStorm on HDInsight**.</span></span>

5. <span data-ttu-id="fb678-221">Em Olá **topologia enviar** caixa de diálogo, selecione seu **Cluster Storm**.</span><span class="sxs-lookup"><span data-stu-id="fb678-221">On hello **Submit Topology** dialog box, select your **Storm Cluster**.</span></span> <span data-ttu-id="fb678-222">Expanda **configurações adicionais**, selecione **caminhos de arquivo Java**, selecione **...** , e o diretório de Olá select que contém o arquivo JAR de saudação você baixou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="fb678-222">Expand **Additional Configurations**, select **Java File Paths**, select **...**, and select hello directory that contains hello JAR file you downloaded earlier.</span></span> <span data-ttu-id="fb678-223">Por fim, clique em **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="fb678-223">Finally, click **Submit**.</span></span>

6. <span data-ttu-id="fb678-224">Quando a topologia de saudação tiver sido enviada, atualizar a lista de topologia de saudação no hello **Storm topologias visualizador** tooverify ambas as topologias estão em execução no cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="fb678-224">When hello topology has been submitted, refresh hello topology list in hello **Storm Topologies Viewer** tooverify that both topologies are running on hello cluster.</span></span>

7. <span data-ttu-id="fb678-225">Em **Storm topologias visualizador**, selecione Olá **EventHubReader** topologia.</span><span class="sxs-lookup"><span data-stu-id="fb678-225">In **Storm Topologies Viewer**, select hello **EventHubReader** topology.</span></span>

8. <span data-ttu-id="fb678-226">componente de saudação tooopen resumo de raio hello, clique duas vezes em Olá **LogBolt** componente no diagrama de saudação.</span><span class="sxs-lookup"><span data-stu-id="fb678-226">tooopen hello component summary for hello bolt, double-click hello **LogBolt** component in hello diagram.</span></span>

9. <span data-ttu-id="fb678-227">Em Olá **executores** seção, selecione um dos links de saudação em Olá **porta** coluna.</span><span class="sxs-lookup"><span data-stu-id="fb678-227">In hello **Executors** section, select one of hello links in hello **Port** column.</span></span> <span data-ttu-id="fb678-228">Isso exibe informações registradas pelo componente de saudação.</span><span class="sxs-lookup"><span data-stu-id="fb678-228">This displays information logged by hello component.</span></span> <span data-ttu-id="fb678-229">informações de saudação registrada são semelhante toohello texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="fb678-229">hello logged information is similar toohello following text:</span></span>

        2017-03-02 14:51:29.255 m.s.p.TaskHost [INFO] Received C# STDOUT: 2017-03-02 14:51:29,255 [1] INFO  EventHubReader_LogBolt [(null)] - Received data: {"deviceValue":1830978598,"deviceId":"8566ccbc-034d-45db-883d-d8a31f34068e"}
        2017-03-02 14:51:29.283 m.s.p.TaskHost [INFO] Received C# STDOUT: 2017-03-02 14:51:29,283 [1] INFO  EventHubReader_LogBolt [(null)] - Received data: {"deviceValue":1756413275,"deviceId":"647a5eff-823d-482f-a8b4-b95b35ae570b"}
        2017-03-02 14:51:29.313 m.s.p.TaskHost [INFO] Received C# STDOUT: 2017-03-02 14:51:29,312 [1] INFO  EventHubReader_LogBolt [(null)] - Received data: {"deviceValue":1108478910,"deviceId":"206a68fa-8264-4d61-9100-bfdb68ee8f0a"}

## <a name="stop-hello-topologies"></a><span data-ttu-id="fb678-230">Parar topologias Olá</span><span class="sxs-lookup"><span data-stu-id="fb678-230">Stop hello topologies</span></span>

<span data-ttu-id="fb678-231">topologias de saudação toostop, selecione cada topologia em Olá **profusão de Visualizador de topologia**, em seguida, clique em **Kill**.</span><span class="sxs-lookup"><span data-stu-id="fb678-231">toostop hello topologies, select each topology in hello **Storm Topology Viewer**, then click **Kill**.</span></span>

![Captura de tela do Visualizador de Topologia do Storm, com o botão Encerrar realçado](./media/hdinsight-storm-develop-csharp-event-hub-topology/killtopology.png)

## <a name="delete-your-cluster"></a><span data-ttu-id="fb678-233">Excluir o cluster</span><span class="sxs-lookup"><span data-stu-id="fb678-233">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="fb678-234">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="fb678-234">Next steps</span></span>

<span data-ttu-id="fb678-235">Neste documento, você aprendeu como a toouse Hubs de eventos do Java Olá spout e incluir a partir de um toowork de topologia c# com dados em Hubs de eventos do Azure.</span><span class="sxs-lookup"><span data-stu-id="fb678-235">In this document, you have learned how toouse hello Java Event Hubs spout and bolt from a C# topology toowork with data in Azure Event Hubs.</span></span> <span data-ttu-id="fb678-236">toolearn mais sobre a criação de topologias de c#, consulte o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="fb678-236">toolearn more about creating C# topologies, see hello following:</span></span>

* [<span data-ttu-id="fb678-237">Desenvolver topologias C# para o Apache Storm no HDInsight usando o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="fb678-237">Develop C# topologies for Apache Storm on HDInsight using Visual Studio</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)
* [<span data-ttu-id="fb678-238">Guia de programação do SCP</span><span class="sxs-lookup"><span data-stu-id="fb678-238">SCP programming guide</span></span>](hdinsight-storm-scp-programming-guide.md)
* [<span data-ttu-id="fb678-239">Topologias de exemplo para Storm no HDInsight</span><span class="sxs-lookup"><span data-stu-id="fb678-239">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)
