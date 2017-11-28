---
title: "tópicos de análise de tendências de aaaTwitter com Apache Storm no HDInsight | Microsoft Docs"
description: "Saiba como toouse Trident toocreate uma topologia do Apache Storm que determina a tendências tópicos no Twitter com base em hashtags."
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
ms.openlocfilehash: 0281b495d10833c63868b36856c96369b139c553
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="determine-twitter-trending-topics-with-apache-storm-on-hdinsight"></a><span data-ttu-id="2af2e-103">Determine os tópicos mais populares do Twitter com o Apache Storm no HDInsight</span><span class="sxs-lookup"><span data-stu-id="2af2e-103">Determine Twitter trending topics with Apache Storm on HDInsight</span></span>

<span data-ttu-id="2af2e-104">Saiba como toouse Trident toocreate uma topologia Storm que determina tendências tópicos (marcas hash) no Twitter.</span><span class="sxs-lookup"><span data-stu-id="2af2e-104">Learn how toouse Trident toocreate a Storm topology that determines trending topics (hash tags) on Twitter.</span></span>

<span data-ttu-id="2af2e-105">O Trident é uma abstração de alto nível que fornece ferramentas como junções, agregações, agrupamento, funções e filtros.</span><span class="sxs-lookup"><span data-stu-id="2af2e-105">Trident is a high-level abstraction that provides tools such as joins, aggregations, grouping, functions, and filters.</span></span> <span data-ttu-id="2af2e-106">Além disso, o Trident adiciona primitivos para fazer o processamento incremental com monitoração de estado.</span><span class="sxs-lookup"><span data-stu-id="2af2e-106">Additionally, Trident adds primitives for doing stateful, incremental processing.</span></span> <span data-ttu-id="2af2e-107">exemplo Hello usado neste documento é uma topologia Trident com um spout personalizado e a função.</span><span class="sxs-lookup"><span data-stu-id="2af2e-107">hello example used in this document is a Trident topology with a custom spout and function.</span></span> <span data-ttu-id="2af2e-108">Ele também usa várias funções internas fornecidas pelo Trident.</span><span class="sxs-lookup"><span data-stu-id="2af2e-108">It also uses several built-in functions provided by Trident.</span></span>

## <a name="requirements"></a><span data-ttu-id="2af2e-109">Requisitos</span><span class="sxs-lookup"><span data-stu-id="2af2e-109">Requirements</span></span>

* <span data-ttu-id="2af2e-110"><a href="http://www.oracle.com/technetwork/java/javase/downloads/index.html" target="_blank">Java e hello JDK 1.8</a></span><span class="sxs-lookup"><span data-stu-id="2af2e-110"><a href="http://www.oracle.com/technetwork/java/javase/downloads/index.html" target="_blank">Java and hello JDK 1.8</a></span></span>

* <span data-ttu-id="2af2e-111"><a href="http://maven.apache.org/what-is-maven.html" target="_blank">Maven</a></span><span class="sxs-lookup"><span data-stu-id="2af2e-111"><a href="http://maven.apache.org/what-is-maven.html" target="_blank">Maven</a></span></span>

* <span data-ttu-id="2af2e-112"><a href="http://git-scm.com/" target="_blank">Git</a></span><span class="sxs-lookup"><span data-stu-id="2af2e-112"><a href="http://git-scm.com/" target="_blank">Git</a></span></span>

* <span data-ttu-id="2af2e-113">Uma conta de desenvolvedor do Twitter</span><span class="sxs-lookup"><span data-stu-id="2af2e-113">A Twitter developer account</span></span>

## <a name="download-hello-project"></a><span data-ttu-id="2af2e-114">Baixe o projeto de saudação</span><span class="sxs-lookup"><span data-stu-id="2af2e-114">Download hello project</span></span>

<span data-ttu-id="2af2e-115">Use Olá tooclone Olá projeto do código localmente a seguir.</span><span class="sxs-lookup"><span data-stu-id="2af2e-115">Use hello following code tooclone hello project locally.</span></span>

    git clone https://github.com/Blackmist/TwitterTrending

## <a name="understanding-hello-topology"></a><span data-ttu-id="2af2e-116">Noções básicas sobre a topologia de saudação</span><span class="sxs-lookup"><span data-stu-id="2af2e-116">Understanding hello topology</span></span>

<span data-ttu-id="2af2e-117">diagrama a seguir de saudação mostra de como os dados fluem através dessa topologia:</span><span class="sxs-lookup"><span data-stu-id="2af2e-117">hello following diagram shows of how data flows through this topology:</span></span>

![Topologia](./media/hdinsight-storm-twitter-trending/trident.png)

> [!NOTE]
> <span data-ttu-id="2af2e-119">Este diagrama é uma exibição simplificada de topologia de saudação.</span><span class="sxs-lookup"><span data-stu-id="2af2e-119">This diagram is a simplified view of hello topology.</span></span> <span data-ttu-id="2af2e-120">Várias instâncias de componentes de saudação são distribuídas entre nós de saudação em cluster hello.</span><span class="sxs-lookup"><span data-stu-id="2af2e-120">Multiple instances of hello components are distributed across hello nodes in hello cluster.</span></span>


<span data-ttu-id="2af2e-121">Olá código Trident que implementa a topologia de saudação é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="2af2e-121">hello Trident code that implements hello topology is as follows:</span></span>

    topology.newStream("spout", spout)
        .each(new Fields("tweet"), new HashtagExtractor(), new Fields("hashtag"))
        .groupBy(new Fields("hashtag"))
        .persistentAggregate(new MemoryMapState.Factory(), new Count(), new Fields("count"))
        .newValuesStream()
        .applyAssembly(new FirstN(10, "count"))
        .each(new Fields("hashtag", "count"), new Debug());

<span data-ttu-id="2af2e-122">Esse código realiza Olá ações a seguir:</span><span class="sxs-lookup"><span data-stu-id="2af2e-122">This code performs hello following actions:</span></span>

1. <span data-ttu-id="2af2e-123">Cria um fluxo de spout hello.</span><span class="sxs-lookup"><span data-stu-id="2af2e-123">Creates a stream from hello spout.</span></span> <span data-ttu-id="2af2e-124">spout Olá recupera tweets do Twitter e filtra para palavras-chave específicas (love, músicas e café neste exemplo).</span><span class="sxs-lookup"><span data-stu-id="2af2e-124">hello spout retrieves tweets from Twitter, and filters them for specific keywords (love, music, and coffee in this example).</span></span>

2. <span data-ttu-id="2af2e-125">HashtagExtractor, uma função personalizada, é usado tooextract hash marcas de cada tweet.</span><span class="sxs-lookup"><span data-stu-id="2af2e-125">HashtagExtractor, a custom function, is used tooextract hash tags from each tweet.</span></span> <span data-ttu-id="2af2e-126">marcas de hash de saudação são fluxo toohello emitido.</span><span class="sxs-lookup"><span data-stu-id="2af2e-126">hello hash tags are emitted toohello stream.</span></span>

3. <span data-ttu-id="2af2e-127">fluxo de saudação é agrupado por marca de hash e passado tooan agregador.</span><span class="sxs-lookup"><span data-stu-id="2af2e-127">hello stream is grouped by hash tag, and passed tooan aggregator.</span></span> <span data-ttu-id="2af2e-128">Esse agregador cria uma contagem de quantas vezes cada hashtag ocorreu.</span><span class="sxs-lookup"><span data-stu-id="2af2e-128">This aggregator creates a count of how many times each hash tag has occurred.</span></span> <span data-ttu-id="2af2e-129">Esses dados persistem na memória.</span><span class="sxs-lookup"><span data-stu-id="2af2e-129">This data is persisted in memory.</span></span> <span data-ttu-id="2af2e-130">Por fim, é emitido um novo fluxo que contém a marca de hash hello e contagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="2af2e-130">Finally, a new stream is emitted that contains hello hash tag and hello count.</span></span>

4. <span data-ttu-id="2af2e-131">Olá **FirstN** assembly é aplicado tooreturn somente Olá 10 principais valores, com base no campo de contagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="2af2e-131">hello **FirstN** assembly is applied tooreturn only hello top 10 values, based on hello count field.</span></span>

> [!NOTE]
> <span data-ttu-id="2af2e-132">Para obter mais informações sobre como trabalhar com Trident, consulte Olá [visão geral da API Trident](http://storm.apache.org/releases/current/Trident-API-Overview.html) documento.</span><span class="sxs-lookup"><span data-stu-id="2af2e-132">For more information on working with Trident, see hello [Trident API overview](http://storm.apache.org/releases/current/Trident-API-Overview.html) document.</span></span>

### <a name="hello-spout"></a><span data-ttu-id="2af2e-133">spout Olá</span><span class="sxs-lookup"><span data-stu-id="2af2e-133">hello spout</span></span>

<span data-ttu-id="2af2e-134">spout Hello, **TwitterSpout**, usa [Twitter4j](http://twitter4j.org/en/) tooretrieve tweets do Twitter.</span><span class="sxs-lookup"><span data-stu-id="2af2e-134">hello spout, **TwitterSpout**, uses [Twitter4j](http://twitter4j.org/en/) tooretrieve tweets from Twitter.</span></span> <span data-ttu-id="2af2e-135">Um filtro é criado para palavras Olá __adoram__, **música**, e **café**.</span><span class="sxs-lookup"><span data-stu-id="2af2e-135">A filter is created for hello words __love__, **music**, and **coffee**.</span></span> <span data-ttu-id="2af2e-136">Tweets de entrada (status) que correspondem ao filtro de saudação são armazenadas em uma fila de bloqueio vinculada.</span><span class="sxs-lookup"><span data-stu-id="2af2e-136">Incoming tweets (status) that match hello filter are stored in a linked blocking queue.</span></span> <span data-ttu-id="2af2e-137">Por fim, itens são tirados da fila de saudação e emitidos toohello topologia.</span><span class="sxs-lookup"><span data-stu-id="2af2e-137">Finally, items are pulled off hello queue and emitted toohello topology.</span></span>

### <a name="hello-hashtagextractor"></a><span data-ttu-id="2af2e-138">Olá HashtagExtractor</span><span class="sxs-lookup"><span data-stu-id="2af2e-138">hello HashtagExtractor</span></span>

<span data-ttu-id="2af2e-139">marcas de hash tooextract, [getHashtagEntities](http://twitter4j.org/javadoc/twitter4j/EntitySupport.html#getHashtagEntities--) é tooretrieve usada todas as marcas de hash que estão contidas em um tweet hello.</span><span class="sxs-lookup"><span data-stu-id="2af2e-139">tooextract hash tags, [getHashtagEntities](http://twitter4j.org/javadoc/twitter4j/EntitySupport.html#getHashtagEntities--) is used tooretrieve all hash tags that are contained in hello tweet.</span></span> <span data-ttu-id="2af2e-140">Esses são então fluxo toohello emitido.</span><span class="sxs-lookup"><span data-stu-id="2af2e-140">These are then emitted toohello stream.</span></span>

## <a name="configure-twitter"></a><span data-ttu-id="2af2e-141">Configurar o Twitter</span><span class="sxs-lookup"><span data-stu-id="2af2e-141">Configure Twitter</span></span>

<span data-ttu-id="2af2e-142">Use Olá seguindo as etapas tooregister um novo aplicativo do Twitter e obter tooread de token informações necessárias de consumidor e o acesso de saudação do Twitter:</span><span class="sxs-lookup"><span data-stu-id="2af2e-142">Use hello following steps tooregister a new Twitter application and obtain hello consumer and access token information needed tooread from Twitter:</span></span>

1. <span data-ttu-id="2af2e-143">Vá muito[Twitter aplicativos](https://apps.twitter.com) e clique em Olá **criar novo aplicativo** botão.</span><span class="sxs-lookup"><span data-stu-id="2af2e-143">Go too[Twitter Apps](https://apps.twitter.com) and click hello **Create new app** button.</span></span> <span data-ttu-id="2af2e-144">Ao preencher o formulário hello, deixe Olá **URL de retorno de chamada** campo vazio.</span><span class="sxs-lookup"><span data-stu-id="2af2e-144">When filling in hello form, leave hello **Callback URL** field empty.</span></span>

2. <span data-ttu-id="2af2e-145">Quando o aplicativo hello for criado, clique em Olá **chaves e Tokens de acesso** guia.</span><span class="sxs-lookup"><span data-stu-id="2af2e-145">When hello app is created, click hello **Keys and Access Tokens** tab.</span></span>

3. <span data-ttu-id="2af2e-146">Saudação de cópia **chave do consumidor** e **segredo do consumidor** informações.</span><span class="sxs-lookup"><span data-stu-id="2af2e-146">Copy hello **Consumer Key** and **Consumer Secret** information.</span></span>

4. <span data-ttu-id="2af2e-147">Final Olá Olá página, selecione **criar o token de acesso** se nenhum token existe.</span><span class="sxs-lookup"><span data-stu-id="2af2e-147">At hello bottom of hello page, select **Create my access token** if no tokens exist.</span></span> <span data-ttu-id="2af2e-148">Quando os tokens de saudação foi criados, Olá cópia **Token de acesso** e **segredo do Token de acesso** informações.</span><span class="sxs-lookup"><span data-stu-id="2af2e-148">When hello tokens have been created, copy hello **Access Token** and **Access Token Secret** information.</span></span>

5. <span data-ttu-id="2af2e-149">Em Olá **TwitterSpoutTopology** projeto Olá clonado anteriormente, abra **resources/twitter4j.properties** de arquivos, adicionar informações de saudação coletadas nas etapas anteriores hello e, em seguida, salve o arquivo de saudação .</span><span class="sxs-lookup"><span data-stu-id="2af2e-149">In hello **TwitterSpoutTopology** project you previously cloned, open hello **resources/twitter4j.properties** file, add hello information you gathered in hello previous steps, and then save hello file.</span></span>

## <a name="build-hello-topology"></a><span data-ttu-id="2af2e-150">Criar uma topologia de saudação</span><span class="sxs-lookup"><span data-stu-id="2af2e-150">Build hello topology</span></span>

<span data-ttu-id="2af2e-151">Use Olá projeto de saudação do toobuild de código a seguir:</span><span class="sxs-lookup"><span data-stu-id="2af2e-151">Use hello following code toobuild hello project:</span></span>

        cd [directoryname]
        mvn compile

## <a name="test-hello-topology"></a><span data-ttu-id="2af2e-152">Topologia de saudação do teste</span><span class="sxs-lookup"><span data-stu-id="2af2e-152">Test hello topology</span></span>

<span data-ttu-id="2af2e-153">Use Olá comando tootest Olá topologia do local a seguir:</span><span class="sxs-lookup"><span data-stu-id="2af2e-153">Use hello following command tootest hello topology locally:</span></span>

    mvn compile exec:java -Dstorm.topology=com.microsoft.example.TwitterTrendingTopology

<span data-ttu-id="2af2e-154">Após o início da topologia hello, você verá as informações de depuração que contém o hash de saudação marcas e contagem emitidas por topologia hello.</span><span class="sxs-lookup"><span data-stu-id="2af2e-154">After hello topology starts, you should see debug information that contains hello hash tags and counts emitted by hello topology.</span></span> <span data-ttu-id="2af2e-155">saída de Hello deve aparecer semelhante toohello texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="2af2e-155">hello output should appear similar toohello following text:</span></span>

    DEBUG: [Quicktellervalentine, 7]
    DEBUG: [GRAMMYs, 7]
    DEBUG: [AskSam, 7]
    DEBUG: [poppunk, 1]
    DEBUG: [rock, 1]
    DEBUG: [punkrock, 1]
    DEBUG: [band, 1]
    DEBUG: [punk, 1]
    DEBUG: [indonesiapunkrock, 1]

## <a name="next-steps"></a><span data-ttu-id="2af2e-156">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2af2e-156">Next steps</span></span>

<span data-ttu-id="2af2e-157">Agora que você tenha testado localmente a topologia hello, descobrir como toodeploy Olá topologia: [implantar e gerenciar as topologias do Apache Storm no HDInsight](hdinsight-storm-deploy-monitor-topology.md).</span><span class="sxs-lookup"><span data-stu-id="2af2e-157">Now that you have tested hello topology locally, discover how toodeploy hello topology: [Deploy and manage Apache Storm topologies on HDInsight](hdinsight-storm-deploy-monitor-topology.md).</span></span>

<span data-ttu-id="2af2e-158">Você também pode estar interessado nos seguintes tópicos profusão de saudação:</span><span class="sxs-lookup"><span data-stu-id="2af2e-158">You may also be interested in hello following Storm topics:</span></span>

* [<span data-ttu-id="2af2e-159">Desenvolver topologias Java para Storm no HDInsight usando o Maven</span><span class="sxs-lookup"><span data-stu-id="2af2e-159">Develop Java topologies for Storm on HDInsight using Maven</span></span>](hdinsight-storm-develop-java-topology.md)
* [<span data-ttu-id="2af2e-160">Desenvolver topologias C# para Storm no HDInsight usando o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2af2e-160">Develop C# topologies for Storm on HDInsight using Visual Studio</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)

<span data-ttu-id="2af2e-161">Para ver mais exemplos do Storm para HDInsight:</span><span class="sxs-lookup"><span data-stu-id="2af2e-161">For more Storm examples for HDInsight:</span></span>

* [<span data-ttu-id="2af2e-162">Topologias de exemplo para Storm no HDInsight</span><span class="sxs-lookup"><span data-stu-id="2af2e-162">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)

