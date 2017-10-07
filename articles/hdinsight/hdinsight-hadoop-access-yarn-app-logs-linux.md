---
title: logs de aaaAccess aplicativo YARN Hadoop no HDInsight baseados em Linux - Azure | Microsoft Docs
description: "Saiba como o aplicativo de YARN tooaccess registra em um cluster HDInsight baseados em Linux (Hadoop) usando Olá de linha de comando e um navegador da web."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 3ec08d20-4f19-4a8e-ac86-639c04d2f12e
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 0bab356e3b97114abbb05712c8e7b21a194f2508
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="access-yarn-application-logs-on-linux-based-hdinsight"></a>Acesso aos logs de aplicativo YARN no HDInsight baseado em Linux

Saiba como tooaccess Olá logs de aplicativos do YARN (ainda outro recurso Negociador) em um cluster de Hadoop no HDInsight do Azure.

> [!IMPORTANT]
> etapas de saudação neste documento exigem um cluster HDInsight que usa o Linux. Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior. Para obter mais informações, consulte [Controle de versão do componente do HDInsight](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="YARNTimelineServer"></a>YARN Timeline Server

Olá [YARN linha do tempo de servidor](http://hadoop.apache.org/docs/r2.4.0/hadoop-yarn/hadoop-yarn-site/TimelineServer.html) fornece informações genéricas em aplicativos concluídos e informações de específica da estrutura de aplicativo por meio de duas interfaces diferentes. Especificamente:

* O armazenamento e a recuperação de informações do aplicativo genérico em clusters HDInsight estão habilitados na versão 3.1.1.374 ou superior.
* componente de informações de aplicativo específica da estrutura Olá de saudação da linha do tempo de servidor não está disponível atualmente em clusters de HDInsight.

Informações genéricas em aplicativos incluem Olá tipo de dados a seguir:

* ID do aplicativo Hello, um identificador exclusivo de um aplicativo
* usuário de saudação que iniciou o aplicativo hello
* Obter informações sobre tentativas feitas aplicativo hello de toocomplete
* contêineres de saudação usados por qualquer tentativa de determinado aplicativo

## <a name="YARNAppsAndLogs"></a>Logs e aplicativos YARN

O YARN dá suporte a vários modelos de programação (inclusive MapReduce), por separar o gerenciamento de recursos do agendamento/monitoramento de aplicativos. O YARN usa um RM (*ResourceManager*) global, NMs (*NodeManagers*) por nó de trabalho e AMs (*ApplicationMasters*) por aplicativo. Olá por aplicativo AM negocia recursos (CPU, memória, disco, rede) para executar seu aplicativo com RM hello. Olá RM funciona com NMs toogrant desses recursos, que são concedidos como *contêineres*. Olá AM é responsável por controlar o progresso de saudação da saudação tooit de contêineres atribuída pelo RM hello. Um aplicativo pode exigir vários contêineres dependendo da natureza de saudação do aplicativo hello.

Cada aplicativo pode consistir em várias *tentativas do aplicativo*. Se um aplicativo falhar, ele poderá ser repetido como uma nova tentativa. Cada tentativa é executado em um contêiner. De certa forma, um contêiner fornece contexto Olá para a unidade básica de trabalho executado por um aplicativo YARN. Todo o trabalho que é executado no contexto de saudação de um contêiner é executado no nó de único trabalhador de saudação em qual Olá contêiner foi alocado. Confira [Conceitos de YARN][YARN-concepts] para referência adicional.

Logs de aplicativo (e logs de contêiner Olá associada) são essenciais na depuração de aplicativos problemáticos do Hadoop. YARN fornece uma estrutura adequada para coletar, agregar e armazenar os logs do aplicativo com hello [Log agregação] [ log-aggregation] recurso. recurso de agregação de Log de saudação torna acessar logs de aplicativo mais determinista. Ele agrega logs em todos os contêineres em um nó de trabalho e as armazena como um arquivo de log agregado por nó de trabalho. log de saudação é armazenado no sistema de arquivos padrão Olá após a conclusão de um aplicativo. Seu aplicativo pode usar centenas ou milhares de contêineres, mas os logs para todos os contêineres são executados em um nó único trabalhador sempre são agregado tooa arquivo único. Assim, há apenas 1 log por nó de trabalho usado pelo seu aplicativo. A Agregação de Log é habilitada por padrão em clusters HDInsight versão 3.0 e superior. Agregados logs estão localizados no armazenamento padrão para o cluster de saudação. Olá que caminho a seguir é Olá HDFS caminho toohello logs:

    /app-logs/<user>/logs/<applicationId>

No caminho hello, `user` é o nome de saudação do usuário de saudação que iniciou o aplicativo hello. Olá `applicationId` é aplicativo de tooan hello identificador exclusivo atribuído pelo RM. YARN de saudação

Olá agregados logs não são diretamente legíveis, como eles são gravados um [TFile][T-file], [formato binário] [ binary-format] indexado pelo contêiner. Use Olá que YARN ResourceManager logs ou CLI ferramentas tooview esses logs como texto sem formatação para aplicativos ou contêineres de interesse.

## <a name="yarn-cli-tools"></a>Ferramentas CLI do YARN

ferramentas de CLI do YARN do toouse hello, primeiro você deve conectar cluster do HDInsight toohello usando o SSH. Para obter informações, consulte [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

Você pode exibir esses logs como texto sem formatação, executando uma saudação comandos a seguir:

    yarn logs -applicationId <applicationId> -appOwner <user-who-started-the-application>
    yarn logs -applicationId <applicationId> -appOwner <user-who-started-the-application> -containerId <containerId> -nodeAddress <worker-node-address>

Especificar Olá &lt;applicationId >, &lt;usuário quem-iniciado-do aplicativo >, &lt;containerId >, e &lt;endereço do nó de trabalho > informações durante a execução desses comandos.

## <a name="yarn-resourcemanager-ui"></a>IU do ResourceManager YARN

Olá YARN ResourceManager UI é executado no nó principal do cluster hello. Ele é acessado por meio da interface da web hello Ambari. Saudação de uso seguindo as etapas tooview Olá YARN logs:

1. No navegador da web, navegar toohttps://CLUSTERNAME.azurehdinsight.net. Substitua CLUSTERNAME pelo nome de saudação do seu cluster HDInsight.
2. Na lista de saudação do services Olá esquerda, selecione **YARN**.

    ![Serviço de yarn selecionado](./media/hdinsight-hadoop-access-yarn-app-logs-linux/yarnservice.png)
3. De saudação **Links rápidos** lista suspensa, selecione uma saudação principal de nós de cluster e, em seguida, selecione **ResourceManager Log**.

    ![Links rápidos do yarn](./media/hdinsight-hadoop-access-yarn-app-logs-linux/yarnquicklinks.png)

    São apresentados com uma lista de links tooYARN logs.

[YARN-timeline-server]:http://hadoop.apache.org/docs/r2.4.0/hadoop-yarn/hadoop-yarn-site/TimelineServer.html
[log-aggregation]:http://hortonworks.com/blog/simplifying-user-logs-management-and-access-in-yarn/
[T-file]:https://issues.apache.org/jira/secure/attachment/12396286/TFile%20Specification%2020081217.pdf
[binary-format]:https://issues.apache.org/jira/browse/HADOOP-3315
[YARN-concepts]:http://hortonworks.com/blog/apache-hadoop-yarn-concepts-and-applications/
