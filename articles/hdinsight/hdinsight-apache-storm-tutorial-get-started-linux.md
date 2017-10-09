---
title: exemplos de starter aaaStorm no Apache Storm no HDInsight - Azure | Microsoft Docs
description: "Saiba como análise de big data toodo e processar dados em tempo real usando o Apache Storm e Olá exemplos starter storm no HDInsight."
keywords: storm-starter, exemplo do apache storm
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: d710dcac-35d1-4c27-a8d6-acaf8146b485
ms.service: hdinsight
ms.devlang: java
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/15/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive,hdiseo17may2017
ms.openlocfilehash: bb6d6549e67ca5b557f0692f98c89692a87267b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
#<a name="get-started-with-apache-storm-on-hdinsight-using-hello-storm-starter-examples"></a>Introdução ao Apache Storm no HDInsight usando Olá storm starter exemplos

Saiba como toouse Apache Storm HDInsight usando Olá exemplos storm starter.

O Apache Storm é um sistema de computação escalável, tolerante a falhas, distribuído e em tempo real para o processamento de fluxos de dados. Com o Storm no Azure HDInsight, você pode criar um cluster Storm baseado em nuvem que execute análise de big data em tempo real.

> [!IMPORTANT]
> Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior. Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="prerequisites"></a>Pré-requisitos

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

* **Uma assinatura do Azure**. Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).

* **Familiaridade com o SSH e o SCP**. Para saber mais, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

## <a name="create-a-storm-cluster"></a>Criar um cluster Storm

Use Olá seguindo as etapas toocreate uma tempestade no cluster HDInsight:

1. De saudação [portal do Azure](https://portal.azure.com), selecione **+ novo**, **Intelligence + análise**e, em seguida, selecione **HDInsight**.

    ![Criar um cluster HDInsight](./media/hdinsight-apache-storm-tutorial-get-started-linux/create-hdinsight.png)

2. De saudação **Noções básicas sobre** folha, digite Olá informações a seguir:

    * **Nome do cluster**: nome de saudação do cluster do HDInsight de saudação.
    * **Assinatura**: selecione Olá toouse de assinatura.
    * **Nome de usuário de logon de cluster** e **senha de logon de Cluster**: logon Olá ao acessar o cluster Olá via HTTPS. Você usa esses serviços de tooaccess de credenciais como saudação da interface do usuário do Ambari Web ou a API REST.
    * **Secure Shell (SSH) username**: logon Olá usado ao acessar o cluster Olá via SSH. Por padrão senha Olá é Olá igual à senha de logon de cluster hello.
    * **Grupo de recursos**: Olá recurso grupo toocreate Olá cluster.
    * **Local**: Olá região do Azure toocreate Olá cluster.

    ![Escolha a assinatura](./media/hdinsight-apache-storm-tutorial-get-started-linux/hdinsight-basic-configuration.png)

3. Selecione **tipo de Cluster**, e conjunto Olá seguindo os valores na Olá **configuração de Cluster** folha:

    * **Tipo de Cluster**: Storm

    * **Sistema Operacional**: Linux

    * **Versão**: Storm 1.1.0 (HDI 3.6)

    * **Camada de Cluster**: Padrão

    Por fim, use Olá **selecione** toosave configurações de botão.

    ![Selecione o tipo de cluster](./media/hdinsight-apache-storm-tutorial-get-started-linux/set-hdinsight-cluster-type.png)

4. Depois de selecionar o tipo de cluster hello, use Olá __selecione__ tooset Olá cluster tipo de botão. Em seguida, use Olá __próximo__ configuração básica do botão toofinish.

5. De saudação **armazenamento** folha, selecione ou crie uma conta de armazenamento. Para obter etapas Olá neste documento, deixe Olá outros campos nesta folha com valores padrão de saudação. Saudação de uso __próximo__ configuração de armazenamento de toosave do botão.

    ![Definir configurações de conta de armazenamento Olá para HDInsight](./media/hdinsight-apache-storm-tutorial-get-started-linux/set-hdinsight-storage-account.png)

6. De saudação **resumo** folha, examinar a configuração de saudação para cluster hello. Saudação de uso __editar__ links toochange todas as configurações que estão incorretas. Por fim, use o cluster de saudação do the__Create__ botão toocreate.

    ![Resumo da configuração do cluster](./media/hdinsight-apache-storm-tutorial-get-started-linux/hdinsight-configuration-summary.png)

    > [!NOTE]
    > Pode demorar até o cluster de saudação de toocreate too20 minutos.

## <a name="run-a-storm-starter-sample-on-hdinsight"></a>Executar uma amostra do storm-starter no HDInsight

1. Conecte o cluster do HDInsight toohello usando SSH:

        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net

    Se você usou uma senha toosecure sua conta de usuário SSH, é solicitada tooentê-lo. Se você usou uma chave pública, você pode precisar usar Olá `-i` toospecify parâmetro hello chave privada correspondente. Por exemplo: `ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`.

    Para obter informações, consulte [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Use Olá comando toostart uma topologia de exemplo a seguir:

        storm jar /usr/hdp/current/storm-client/contrib/storm-starter/storm-starter-topologies-*.jar org.apache.storm.starter.WordCountTopology wordcount

    > [!NOTE]
    > Em versões anteriores do HDInsight, o nome da classe de saudação da topologia de saudação é `storm.starter.WordCountTopology` em vez de `org.apache.storm.starter.WordCountTopology`.

    Esse comando inicia a topologia de WordCount do exemplo hello no cluster hello, com um nome amigável do 'wordcount'. Ele gera aleatoriamente frases e a ocorrência de saudação de contagem de cada palavra em frases hello.

    > [!NOTE]
    > Ao enviar seu próprio cluster toohello de topologias, primeiro você deve copiar o arquivo jar de saudação contendo cluster Olá antes de usar o hello `storm` comando. Saudação de uso `scp` arquivo de saudação do comando toocopy. Por exemplo, `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`
    >
    > exemplo de WordCount Hello e outros exemplos storm starter, já estão incluídos no cluster em `/usr/hdp/current/storm-client/contrib/storm-starter/`.

Se você estiver interessado em Exibir código-fonte para obter exemplos de starter storm Olá Olá, você pode encontrar o código de saudação em [https://github.com/apache/storm/tree/1.1.x-branch/examples/storm-starter](https://github.com/apache/storm/tree/1.1.x-branch/examples/storm-starter). O link é para o Storm 1.1, que é fornecido com o HDInsight 3.6. Para outras versões do Storm, use Olá __ramificação__ botão na parte superior de saudação do hello página tooselect uma versão diferente do Storm.

## <a name="monitor-hello-topology"></a>Topologia de saudação do monitor

Olá profusão de interface do usuário fornece uma interface da web para trabalhar com a execução de topologias e está incluída no seu cluster HDInsight.

Use Olá topologia de saudação toomonitor etapas usando Olá profusão de interface do usuário a seguir:

1. Olá toodisplay profusão de interface de usuário, abra uma web navegador toohttps://CLUSTERNAME.azurehdinsight.net/stormui. Substituir **CLUSTERNAME** com nome de saudação do cluster.

    > [!NOTE]
    > Se for solicitado tooprovide um nome de usuário e senha, insira o administrador de cluster de saudação (administrador) e a senha que você usou quando criar cluster de saudação.

2. Em **Resumo da topologia**, selecione Olá **wordcount** entrada hello **nome** coluna. Informações sobre topologia de saudação são exibidas.

    ![Painel do Storm com informações da topologia do storm-starter WordCount.](./media/hdinsight-apache-storm-tutorial-get-started-linux/topology-summary.png)

    Esta página fornece Olá informações a seguir:

    * **Estatísticas de topologia** -informações básicas sobre o desempenho de topologia hello, organizados em janelas de tempo.

        > [!NOTE]
        > Selecionando uma janela de tempo de saudação do tempo específico janela alterações das informações exibidas em outras seções da página de saudação.

    * **Spouts** -informações básicas sobre spouts, incluindo o último erro de saudação retornado por cada spout.

    * **Bolts** -informações básicas sobre bolts.

    * **Configuração de topologia** -informações detalhadas sobre configuração de topologia de saudação.

    Essa página também fornece ações que podem ser executadas na topologia hello:

    * **Ativar** - retoma o processamento de uma topologia desativada.

    * **Desativar** - pausa uma topologia em execução.

    * **Reequilibrar** -ajusta o paralelismo de saudação da topologia de saudação. Você deve reequilibrar topologias em execução depois que você tenha alterado Olá número de nós no cluster de saudação. Rebalanceamento ajusta o paralelismo toocompensate para número de saudação aumentado/reduzido de nós no cluster de saudação. Para obter mais informações, consulte [Noções básicas sobre o paralelismo de saudação de uma topologia Storm](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html).

    * **Kill** -encerra uma topologia Storm depois Olá especificada de tempo limite.

3. Nessa página, selecione uma entrada de saudação **Spouts** ou **Bolts** seção. Informações sobre o componente de saudação selecionado são exibidas.

    ![Painel do Storm com informações sobre os componentes selecionados.](./media/hdinsight-apache-storm-tutorial-get-started-linux/component-summary.png)

    Esta página exibe o saudação informações a seguir:

    * **Estatísticas de spout/raio** -informações básicas sobre o desempenho de componente hello, organizados em janelas de tempo.

        > [!NOTE]
        > Selecionando uma janela de tempo de saudação do tempo específico janela alterações das informações exibidas em outras seções da página de saudação.

    * **Estatísticas de entrada** (incluem apenas) - informações sobre os componentes que geram dados consumidos pelo raio hello.

    * **Estatísticas de saída** -informações sobre dados emitidos por este bolt.

    * **Executores** -informações sobre instâncias deste componente.

    * **Erros** -erros produzidos por este componente.

4. Ao exibir detalhes de saudação de um spout ou raio, selecione uma entrada da saudação **porta** coluna Olá **executores** tooview detalhes para uma instância específica do componente de saudação de seção.

        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: split default ["with"]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: split default ["nature"]
        2015-01-27 14:18:02 b.s.d.executor [INFO] Processing received message source: split:21, stream: default, id: {}, [snow]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: count default [snow, 747293]
        2015-01-27 14:18:02 b.s.d.executor [INFO] Processing received message source: split:21, stream: default, id: {}, [white]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: count default [white, 747293]
        2015-01-27 14:18:02 b.s.d.executor [INFO] Processing received message source: split:21, stream: default, id: {}, [seven]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: count default [seven, 1493957]

    Neste exemplo, hello word **sete** ocorreu 1493957 vezes. Essa contagem é quantas vezes word Olá foi encontrado desde que esta topologia foi iniciada.

## <a name="stop-hello-topology"></a>Parar a topologia de saudação

Retornar toohello **Resumo da topologia** página topologia de contagem de palavras hello e selecione Olá **Kill** botão da saudação **ações de topologia** seção. Quando solicitado, insira 10 para Olá toowait de segundos antes de parar a topologia de saudação. Após o período de tempo limite de saudação topologia Olá deixará de aparecer quando você visita Olá **profusão de interface do usuário** seção do painel de saudação.

## <a name="delete-hello-cluster"></a>Excluir o cluster Olá

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

Se você tiver um problema com a criação de clusters HDInsight, consulte [requisitos de controle de acesso](hdinsight-administer-use-portal-linux.md#create-clusters).

## <a id="next"></a>Próximas etapas

Neste tutorial do Apache Storm, você aprendeu os fundamentos de saudação do trabalho com Storm no HDInsight. Em seguida, Aprenda como muito[topologias em Java desenvolver usando Maven](hdinsight-storm-develop-java-topology.md).

Se você já estiver familiarizado com o desenvolvimento baseado em Java topologias e deseja toodeploy um tooHDInsight de topologia existente, consulte [implantar e gerenciar as topologias do Apache Storm no HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md).

Se você for um desenvolvedor .NET, poderá criar topologias em C# ou híbridas C#/Java usando o Visual Studio. Para obter mais informações, consulte [Desenvolver topologias C# para o Apache Storm no HDInsight usando ferramentas do Hadoop para Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).

Para topologias de exemplo que podem ser usadas com Storm no HDInsight, consulte Olá exemplos a seguir:

* [Topologias de exemplo para Storm no HDInsight](hdinsight-storm-example-topology.md)

[apachestorm]: https://storm.incubator.apache.org
[stormdocs]: http://storm.incubator.apache.org/documentation/Documentation.html
[stormstarter]: https://github.com/apache/storm/tree/master/examples/storm-starter
[stormjavadocs]: https://storm.incubator.apache.org/apidocs/
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[preview-portal]: https://portal.azure.com/
