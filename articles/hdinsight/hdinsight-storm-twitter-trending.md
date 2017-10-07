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
# <a name="determine-twitter-trending-topics-with-apache-storm-on-hdinsight"></a>Determine os tópicos mais populares do Twitter com o Apache Storm no HDInsight

Saiba como toouse Trident toocreate uma topologia Storm que determina tendências tópicos (marcas hash) no Twitter.

O Trident é uma abstração de alto nível que fornece ferramentas como junções, agregações, agrupamento, funções e filtros. Além disso, o Trident adiciona primitivos para fazer o processamento incremental com monitoração de estado. exemplo Hello usado neste documento é uma topologia Trident com um spout personalizado e a função. Ele também usa várias funções internas fornecidas pelo Trident.

## <a name="requirements"></a>Requisitos

* <a href="http://www.oracle.com/technetwork/java/javase/downloads/index.html" target="_blank">Java e hello JDK 1.8</a>

* <a href="http://maven.apache.org/what-is-maven.html" target="_blank">Maven</a>

* <a href="http://git-scm.com/" target="_blank">Git</a>

* Uma conta de desenvolvedor do Twitter

## <a name="download-hello-project"></a>Baixe o projeto de saudação

Use Olá tooclone Olá projeto do código localmente a seguir.

    git clone https://github.com/Blackmist/TwitterTrending

## <a name="understanding-hello-topology"></a>Noções básicas sobre a topologia de saudação

diagrama a seguir de saudação mostra de como os dados fluem através dessa topologia:

![Topologia](./media/hdinsight-storm-twitter-trending/trident.png)

> [!NOTE]
> Este diagrama é uma exibição simplificada de topologia de saudação. Várias instâncias de componentes de saudação são distribuídas entre nós de saudação em cluster hello.


Olá código Trident que implementa a topologia de saudação é o seguinte:

    topology.newStream("spout", spout)
        .each(new Fields("tweet"), new HashtagExtractor(), new Fields("hashtag"))
        .groupBy(new Fields("hashtag"))
        .persistentAggregate(new MemoryMapState.Factory(), new Count(), new Fields("count"))
        .newValuesStream()
        .applyAssembly(new FirstN(10, "count"))
        .each(new Fields("hashtag", "count"), new Debug());

Esse código realiza Olá ações a seguir:

1. Cria um fluxo de spout hello. spout Olá recupera tweets do Twitter e filtra para palavras-chave específicas (love, músicas e café neste exemplo).

2. HashtagExtractor, uma função personalizada, é usado tooextract hash marcas de cada tweet. marcas de hash de saudação são fluxo toohello emitido.

3. fluxo de saudação é agrupado por marca de hash e passado tooan agregador. Esse agregador cria uma contagem de quantas vezes cada hashtag ocorreu. Esses dados persistem na memória. Por fim, é emitido um novo fluxo que contém a marca de hash hello e contagem de saudação.

4. Olá **FirstN** assembly é aplicado tooreturn somente Olá 10 principais valores, com base no campo de contagem de saudação.

> [!NOTE]
> Para obter mais informações sobre como trabalhar com Trident, consulte Olá [visão geral da API Trident](http://storm.apache.org/releases/current/Trident-API-Overview.html) documento.

### <a name="hello-spout"></a>spout Olá

spout Hello, **TwitterSpout**, usa [Twitter4j](http://twitter4j.org/en/) tooretrieve tweets do Twitter. Um filtro é criado para palavras Olá __adoram__, **música**, e **café**. Tweets de entrada (status) que correspondem ao filtro de saudação são armazenadas em uma fila de bloqueio vinculada. Por fim, itens são tirados da fila de saudação e emitidos toohello topologia.

### <a name="hello-hashtagextractor"></a>Olá HashtagExtractor

marcas de hash tooextract, [getHashtagEntities](http://twitter4j.org/javadoc/twitter4j/EntitySupport.html#getHashtagEntities--) é tooretrieve usada todas as marcas de hash que estão contidas em um tweet hello. Esses são então fluxo toohello emitido.

## <a name="configure-twitter"></a>Configurar o Twitter

Use Olá seguindo as etapas tooregister um novo aplicativo do Twitter e obter tooread de token informações necessárias de consumidor e o acesso de saudação do Twitter:

1. Vá muito[Twitter aplicativos](https://apps.twitter.com) e clique em Olá **criar novo aplicativo** botão. Ao preencher o formulário hello, deixe Olá **URL de retorno de chamada** campo vazio.

2. Quando o aplicativo hello for criado, clique em Olá **chaves e Tokens de acesso** guia.

3. Saudação de cópia **chave do consumidor** e **segredo do consumidor** informações.

4. Final Olá Olá página, selecione **criar o token de acesso** se nenhum token existe. Quando os tokens de saudação foi criados, Olá cópia **Token de acesso** e **segredo do Token de acesso** informações.

5. Em Olá **TwitterSpoutTopology** projeto Olá clonado anteriormente, abra **resources/twitter4j.properties** de arquivos, adicionar informações de saudação coletadas nas etapas anteriores hello e, em seguida, salve o arquivo de saudação .

## <a name="build-hello-topology"></a>Criar uma topologia de saudação

Use Olá projeto de saudação do toobuild de código a seguir:

        cd [directoryname]
        mvn compile

## <a name="test-hello-topology"></a>Topologia de saudação do teste

Use Olá comando tootest Olá topologia do local a seguir:

    mvn compile exec:java -Dstorm.topology=com.microsoft.example.TwitterTrendingTopology

Após o início da topologia hello, você verá as informações de depuração que contém o hash de saudação marcas e contagem emitidas por topologia hello. saída de Hello deve aparecer semelhante toohello texto a seguir:

    DEBUG: [Quicktellervalentine, 7]
    DEBUG: [GRAMMYs, 7]
    DEBUG: [AskSam, 7]
    DEBUG: [poppunk, 1]
    DEBUG: [rock, 1]
    DEBUG: [punkrock, 1]
    DEBUG: [band, 1]
    DEBUG: [punk, 1]
    DEBUG: [indonesiapunkrock, 1]

## <a name="next-steps"></a>Próximas etapas

Agora que você tenha testado localmente a topologia hello, descobrir como toodeploy Olá topologia: [implantar e gerenciar as topologias do Apache Storm no HDInsight](hdinsight-storm-deploy-monitor-topology.md).

Você também pode estar interessado nos seguintes tópicos profusão de saudação:

* [Desenvolver topologias Java para Storm no HDInsight usando o Maven](hdinsight-storm-develop-java-topology.md)
* [Desenvolver topologias C# para Storm no HDInsight usando o Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md)

Para ver mais exemplos do Storm para HDInsight:

* [Topologias de exemplo para Storm no HDInsight](hdinsight-storm-example-topology.md)

