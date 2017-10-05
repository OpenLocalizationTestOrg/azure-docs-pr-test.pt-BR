---
title: "Tópicos mais populares do Twitter com Apache Storm no HDInsight | Microsoft Docs"
description: "Saiba como usar o Trident para criar uma topologia Apache Storm que determina os tópicos mais populares do Twitter com base em hashtags."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 63b280ea-5c07-4dc8-a35f-dccf5a96ba93
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/14/2017
ms.author: larryfr
ms.openlocfilehash: d588221586f151319436525c5098b0bb2694e5f9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="determine-twitter-trending-topics-with-apache-storm-on-hdinsight"></a><span data-ttu-id="05602-103">Determine os tópicos mais populares do Twitter com o Apache Storm no HDInsight</span><span class="sxs-lookup"><span data-stu-id="05602-103">Determine Twitter trending topics with Apache Storm on HDInsight</span></span>

<span data-ttu-id="05602-104">Saiba como usar o Trident para criar uma topologia Storm que determina os tópicos mais populares (hashtags) no Twitter.</span><span class="sxs-lookup"><span data-stu-id="05602-104">Learn how to use Trident to create a Storm topology that determines trending topics (hash tags) on Twitter.</span></span>

<span data-ttu-id="05602-105">O Trident é uma abstração de alto nível que fornece ferramentas como junções, agregações, agrupamento, funções e filtros.</span><span class="sxs-lookup"><span data-stu-id="05602-105">Trident is a high-level abstraction that provides tools such as joins, aggregations, grouping, functions, and filters.</span></span> <span data-ttu-id="05602-106">Além disso, o Trident adiciona primitivos para fazer o processamento incremental com monitoração de estado.</span><span class="sxs-lookup"><span data-stu-id="05602-106">Additionally, Trident adds primitives for doing stateful, incremental processing.</span></span> <span data-ttu-id="05602-107">O exemplo usado neste documento é uma topologia Trident com um spout e uma função personalizados.</span><span class="sxs-lookup"><span data-stu-id="05602-107">The example used in this document is a Trident topology with a custom spout and function.</span></span> <span data-ttu-id="05602-108">Ele também usa várias funções internas fornecidas pelo Trident.</span><span class="sxs-lookup"><span data-stu-id="05602-108">It also uses several built-in functions provided by Trident.</span></span>

## <a name="requirements"></a><span data-ttu-id="05602-109">Requisitos</span><span class="sxs-lookup"><span data-stu-id="05602-109">Requirements</span></span>

* <span data-ttu-id="05602-110"><a href="http://www.oracle.com/technetwork/java/javase/downloads/index.html" target="_blank">Java e o JDK 1.8</a></span><span class="sxs-lookup"><span data-stu-id="05602-110"><a href="http://www.oracle.com/technetwork/java/javase/downloads/index.html" target="_blank">Java and the JDK 1.8</a></span></span>

* <span data-ttu-id="05602-111"><a href="http://maven.apache.org/what-is-maven.html" target="_blank">Maven</a></span><span class="sxs-lookup"><span data-stu-id="05602-111"><a href="http://maven.apache.org/what-is-maven.html" target="_blank">Maven</a></span></span>

* <span data-ttu-id="05602-112"><a href="http://git-scm.com/" target="_blank">Git</a></span><span class="sxs-lookup"><span data-stu-id="05602-112"><a href="http://git-scm.com/" target="_blank">Git</a></span></span>

* <span data-ttu-id="05602-113">Uma conta de desenvolvedor do Twitter</span><span class="sxs-lookup"><span data-stu-id="05602-113">A Twitter developer account</span></span>

## <a name="download-the-project"></a><span data-ttu-id="05602-114">Baixe o projeto</span><span class="sxs-lookup"><span data-stu-id="05602-114">Download the project</span></span>

<span data-ttu-id="05602-115">Use o código a seguir para clonar o projeto localmente.</span><span class="sxs-lookup"><span data-stu-id="05602-115">Use the following code to clone the project locally.</span></span>

    git clone https://github.com/Blackmist/TwitterTrending

## <a name="understanding-the-topology"></a><span data-ttu-id="05602-116">Noções básicas sobre a topologia</span><span class="sxs-lookup"><span data-stu-id="05602-116">Understanding the topology</span></span>

<span data-ttu-id="05602-117">O diagrama a seguir mostra de como os dados fluem por essa topologia:</span><span class="sxs-lookup"><span data-stu-id="05602-117">The following diagram shows of how data flows through this topology:</span></span>

![Topologia](./media/hdinsight-storm-twitter-trending/trident.png)

> [!NOTE]
> <span data-ttu-id="05602-119">Esse diagrama é uma visão simplificada da topologia.</span><span class="sxs-lookup"><span data-stu-id="05602-119">This diagram is a simplified view of the topology.</span></span> <span data-ttu-id="05602-120">Várias instâncias dos componentes são distribuídas entre os nós no cluster.</span><span class="sxs-lookup"><span data-stu-id="05602-120">Multiple instances of the components are distributed across the nodes in the cluster.</span></span>


<span data-ttu-id="05602-121">O código do Trident que implementa a topologia é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="05602-121">The Trident code that implements the topology is as follows:</span></span>

    topology.newStream("spout", spout)
        .each(new Fields("tweet"), new HashtagExtractor(), new Fields("hashtag"))
        .groupBy(new Fields("hashtag"))
        .persistentAggregate(new MemoryMapState.Factory(), new Count(), new Fields("count"))
        .newValuesStream()
        .applyAssembly(new FirstN(10, "count"))
        .each(new Fields("hashtag", "count"), new Debug());

<span data-ttu-id="05602-122">Esse código executa as ações a seguir:</span><span class="sxs-lookup"><span data-stu-id="05602-122">This code performs the following actions:</span></span>

1. <span data-ttu-id="05602-123">Cria um fluxo do spout.</span><span class="sxs-lookup"><span data-stu-id="05602-123">Creates a stream from the spout.</span></span> <span data-ttu-id="05602-124">O spout recupera tweets do Twitter e os filtra por palavras-chave específicas (amor, música e café neste exemplo).</span><span class="sxs-lookup"><span data-stu-id="05602-124">The spout retrieves tweets from Twitter, and filters them for specific keywords (love, music, and coffee in this example).</span></span>

2. <span data-ttu-id="05602-125">O HashtagExtractor, uma função personalizada, é usado para extrair hashtags de cada tweet.</span><span class="sxs-lookup"><span data-stu-id="05602-125">HashtagExtractor, a custom function, is used to extract hash tags from each tweet.</span></span> <span data-ttu-id="05602-126">As hashtags são emitidas para o fluxo.</span><span class="sxs-lookup"><span data-stu-id="05602-126">The hash tags are emitted to the stream.</span></span>

3. <span data-ttu-id="05602-127">O fluxo é agrupado por hashtag e transmitido para um agregador.</span><span class="sxs-lookup"><span data-stu-id="05602-127">The stream is grouped by hash tag, and passed to an aggregator.</span></span> <span data-ttu-id="05602-128">Esse agregador cria uma contagem de quantas vezes cada hashtag ocorreu.</span><span class="sxs-lookup"><span data-stu-id="05602-128">This aggregator creates a count of how many times each hash tag has occurred.</span></span> <span data-ttu-id="05602-129">Esses dados persistem na memória.</span><span class="sxs-lookup"><span data-stu-id="05602-129">This data is persisted in memory.</span></span> <span data-ttu-id="05602-130">Por fim, é emitido um novo fluxo que contém a hashtag e a contagem.</span><span class="sxs-lookup"><span data-stu-id="05602-130">Finally, a new stream is emitted that contains the hash tag and the count.</span></span>

4. <span data-ttu-id="05602-131">O assembly **FirstN** é aplicado para retornar somente os 10 primeiros valores com base no campo de contagem.</span><span class="sxs-lookup"><span data-stu-id="05602-131">The **FirstN** assembly is applied to return only the top 10 values, based on the count field.</span></span>

> [!NOTE]
> <span data-ttu-id="05602-132">Para obter mais informações sobre como trabalhar com o Trident, consulte o documento [Visão geral da API do Trident](http://storm.apache.org/releases/current/Trident-API-Overview.html).</span><span class="sxs-lookup"><span data-stu-id="05602-132">For more information on working with Trident, see the [Trident API overview](http://storm.apache.org/releases/current/Trident-API-Overview.html) document.</span></span>

### <a name="the-spout"></a><span data-ttu-id="05602-133">O spout</span><span class="sxs-lookup"><span data-stu-id="05602-133">The spout</span></span>

<span data-ttu-id="05602-134">O spout, **TwitterSpout** usa [Twitter4j](http://twitter4j.org/en/) para recuperar tweets do Twitter.</span><span class="sxs-lookup"><span data-stu-id="05602-134">The spout, **TwitterSpout**, uses [Twitter4j](http://twitter4j.org/en/) to retrieve tweets from Twitter.</span></span> <span data-ttu-id="05602-135">Um filtro é criado para as palavras __love__ (amar), **music** (música) e **coffee** (café).</span><span class="sxs-lookup"><span data-stu-id="05602-135">A filter is created for the words __love__, **music**, and **coffee**.</span></span> <span data-ttu-id="05602-136">Tweets de entrada (status) que correspondem ao filtro são armazenados em uma fila de bloqueio vinculada.</span><span class="sxs-lookup"><span data-stu-id="05602-136">Incoming tweets (status) that match the filter are stored in a linked blocking queue.</span></span> <span data-ttu-id="05602-137">Por fim, os itens são retirados da fila e emitidos na topologia.</span><span class="sxs-lookup"><span data-stu-id="05602-137">Finally, items are pulled off the queue and emitted to the topology.</span></span>

### <a name="the-hashtagextractor"></a><span data-ttu-id="05602-138">O HashtagExtractor</span><span class="sxs-lookup"><span data-stu-id="05602-138">The HashtagExtractor</span></span>

<span data-ttu-id="05602-139">Para extrair hashtags, [getHashtagEntities](http://twitter4j.org/javadoc/twitter4j/EntitySupport.html#getHashtagEntities--) é usado para recuperar todas as hashtags contidas no tweet.</span><span class="sxs-lookup"><span data-stu-id="05602-139">To extract hash tags, [getHashtagEntities](http://twitter4j.org/javadoc/twitter4j/EntitySupport.html#getHashtagEntities--) is used to retrieve all hash tags that are contained in the tweet.</span></span> <span data-ttu-id="05602-140">Eles são emitidos para o fluxo.</span><span class="sxs-lookup"><span data-stu-id="05602-140">These are then emitted to the stream.</span></span>

## <a name="configure-twitter"></a><span data-ttu-id="05602-141">Configurar o Twitter</span><span class="sxs-lookup"><span data-stu-id="05602-141">Configure Twitter</span></span>

<span data-ttu-id="05602-142">Use as etapas a seguir para registrar um novo aplicativo do Twitter e obter as informações do token de acesso e do consumidor necessárias para ler do Twitter:</span><span class="sxs-lookup"><span data-stu-id="05602-142">Use the following steps to register a new Twitter application and obtain the consumer and access token information needed to read from Twitter:</span></span>

1. <span data-ttu-id="05602-143">Vá para [Aplicativos do Twitter](https://apps.twitter.com) e clique no botão **Criar novo aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="05602-143">Go to [Twitter Apps](https://apps.twitter.com) and click the **Create new app** button.</span></span> <span data-ttu-id="05602-144">Durante o preenchimento do formulário, deixe a **URL de retorno** vazia.</span><span class="sxs-lookup"><span data-stu-id="05602-144">When filling in the form, leave the **Callback URL** field empty.</span></span>

2. <span data-ttu-id="05602-145">Quando o aplicativo for criado, clique na guia **Chaves e Tokens de acesso** .</span><span class="sxs-lookup"><span data-stu-id="05602-145">When the app is created, click the **Keys and Access Tokens** tab.</span></span>

3. <span data-ttu-id="05602-146">Copie as informações **Chave do consumidor** e **Segredo do consumidor**.</span><span class="sxs-lookup"><span data-stu-id="05602-146">Copy the **Consumer Key** and **Consumer Secret** information.</span></span>

4. <span data-ttu-id="05602-147">Na parte inferior da página, selecione **Criar meu token de acesso** se nenhum token existir.</span><span class="sxs-lookup"><span data-stu-id="05602-147">At the bottom of the page, select **Create my access token** if no tokens exist.</span></span> <span data-ttu-id="05602-148">Assim que os tokens forem criados, copie as informações **Token de Acesso** e **Segredo do Token de Acesso**.</span><span class="sxs-lookup"><span data-stu-id="05602-148">When the tokens have been created, copy the **Access Token** and **Access Token Secret** information.</span></span>

5. <span data-ttu-id="05602-149">No projeto **TwitterSpoutTopology** anteriormente clonado, abra o arquivo **resources/twitter4j.properties**, adicione as informações coletadas nas etapas anteriores e salve o arquivo.</span><span class="sxs-lookup"><span data-stu-id="05602-149">In the **TwitterSpoutTopology** project you previously cloned, open the **resources/twitter4j.properties** file, add the information you gathered in the previous steps, and then save the file.</span></span>

## <a name="build-the-topology"></a><span data-ttu-id="05602-150">Compilar a topologia</span><span class="sxs-lookup"><span data-stu-id="05602-150">Build the topology</span></span>

<span data-ttu-id="05602-151">Use o seguinte código para criar o projeto:</span><span class="sxs-lookup"><span data-stu-id="05602-151">Use the following code to build the project:</span></span>

        cd [directoryname]
        mvn compile

## <a name="test-the-topology"></a><span data-ttu-id="05602-152">Testar a topologia</span><span class="sxs-lookup"><span data-stu-id="05602-152">Test the topology</span></span>

<span data-ttu-id="05602-153">Use o seguinte comando para testar a topologia localmente:</span><span class="sxs-lookup"><span data-stu-id="05602-153">Use the following command to test the topology locally:</span></span>

    mvn compile exec:java -Dstorm.topology=com.microsoft.example.TwitterTrendingTopology

<span data-ttu-id="05602-154">Depois que a topologia é iniciada, você verá informações de depuração que contêm hashtags e contagens emitidas pela topologia.</span><span class="sxs-lookup"><span data-stu-id="05602-154">After the topology starts, you should see debug information that contains the hash tags and counts emitted by the topology.</span></span> <span data-ttu-id="05602-155">A saída deve ter aparência similar ao seguinte texto:</span><span class="sxs-lookup"><span data-stu-id="05602-155">The output should appear similar to the following text:</span></span>

    DEBUG: [Quicktellervalentine, 7]
    DEBUG: [GRAMMYs, 7]
    DEBUG: [AskSam, 7]
    DEBUG: [poppunk, 1]
    DEBUG: [rock, 1]
    DEBUG: [punkrock, 1]
    DEBUG: [band, 1]
    DEBUG: [punk, 1]
    DEBUG: [indonesiapunkrock, 1]

## <a name="next-steps"></a><span data-ttu-id="05602-156">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="05602-156">Next steps</span></span>

<span data-ttu-id="05602-157">Agora que você testou a topologia localmente, descubra como implantar essa topologia: [Implantar e gerenciar topologias Apache Storm no HDInsight](hdinsight-storm-deploy-monitor-topology.md).</span><span class="sxs-lookup"><span data-stu-id="05602-157">Now that you have tested the topology locally, discover how to deploy the topology: [Deploy and manage Apache Storm topologies on HDInsight](hdinsight-storm-deploy-monitor-topology.md).</span></span>

<span data-ttu-id="05602-158">Você também pode estar interessado nos tópicos do Storm a seguir:</span><span class="sxs-lookup"><span data-stu-id="05602-158">You may also be interested in the following Storm topics:</span></span>

* [<span data-ttu-id="05602-159">Desenvolver topologias Java para Storm no HDInsight usando o Maven</span><span class="sxs-lookup"><span data-stu-id="05602-159">Develop Java topologies for Storm on HDInsight using Maven</span></span>](hdinsight-storm-develop-java-topology.md)
* [<span data-ttu-id="05602-160">Desenvolver topologias C# para Storm no HDInsight usando o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="05602-160">Develop C# topologies for Storm on HDInsight using Visual Studio</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)

<span data-ttu-id="05602-161">Para ver mais exemplos do Storm para HDInsight:</span><span class="sxs-lookup"><span data-stu-id="05602-161">For more Storm examples for HDInsight:</span></span>

* [<span data-ttu-id="05602-162">Topologias de exemplo para Storm no HDInsight</span><span class="sxs-lookup"><span data-stu-id="05602-162">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)

