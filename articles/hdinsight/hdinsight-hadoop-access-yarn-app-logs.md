---
title: aaaAccess aplicativo Hadoop YARN programaticamente - logs do Azure | Microsoft Docs
description: Acessar logs do aplicativo programaticamente em um cluster de Hadoop no HDInsight.
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 0198d6c9-7767-4682-bd34-42838cf48fc5
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 064efee1ea6a864c29ab897692ead0152c926c0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="access-yarn-application-logs-on-windows-based-hdinsight"></a>Acessar logs de aplicativo YARN no HDInsight baseado em Windows
Este tópico explica como tooaccess Olá logs de aplicativos do YARN (ainda outro recurso Negociador) que terminar em um cluster de Hadoop baseado em Windows no Azure HDInsight

> [!IMPORTANT]
> informações de Olá neste documento aplicam-se apenas com base em tooWindows clusters de HDInsight. Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior. Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement). Para obter informações sobre os logs de YARN nos clusters HDInsight baseados em Linux, consulte [Acessar logs do aplicativo YARN no Hadoop baseado em Linux no HDInsight](hdinsight-hadoop-access-yarn-app-logs-linux.md)
>


### <a name="prerequisites"></a>Pré-requisitos
* Um cluster HDInsight baseado no Windows.  Confira [Crie clusters Hadoop baseados no Windows no HDInsight](hdinsight-hadoop-provision-linux-clusters.md).

## <a name="yarn-timeline-server"></a>Servidor de linha do tempo do YARN
Olá <a href="http://hadoop.apache.org/docs/r2.4.0/hadoop-yarn/hadoop-yarn-site/TimelineServer.html" target="_blank">YARN linha do tempo de servidor</a> fornece informações genéricas sobre aplicativos concluídos, bem como informações específicas do framework aplicativo por meio de duas interfaces diferentes. Especificamente:

* O armazenamento e a recuperação de informações do aplicativo genérico em clusters HDInsight estão habilitados na versão 3.1.1.374 ou superior.
* componente de informações de aplicativo específica da estrutura Olá de saudação da linha do tempo de servidor não está disponível atualmente em clusters de HDInsight.

Informações genéricas em aplicativos incluem Olá tipos de dados a seguir:

* ID do aplicativo Hello, um identificador exclusivo de um aplicativo
* usuário de saudação que iniciou o aplicativo hello
* Obter informações sobre tentativas feitas aplicativo hello de toocomplete
* contêineres de saudação usados por qualquer tentativa de determinado aplicativo

Em seus clusters HDInsight, essas informações serão armazenadas pelo repositório de histórico do Azure Resource Manager tooa no contêiner de padrão de saudação da sua conta de armazenamento do Azure padrão. Esses dados genéricos em aplicativos concluídos podem ser recuperados por meio de uma API REST:

    GET on https://<cluster-dns-name>.azurehdinsight.net/ws/v1/applicationhistory/apps


## <a name="yarn-applications-and-logs"></a>Aplicativos e logs YARN
O YARN dá suporte a vários modelos de programação (inclusive MapReduce), por separar o gerenciamento de recursos do agendamento/monitoramento de aplicativos. Isso é feito por meio de um RM (*Gerenciador de Recursos*) global, NMs (*Gerenciadores de Nós*) por nó de trabalho e AMs (*Mestres de Aplicativos*) por aplicativo. Olá por aplicativo AM negocia recursos (CPU, memória, disco, rede) para executar seu aplicativo com RM hello. Olá RM funciona com NMs toogrant desses recursos, que são concedidos como *contêineres*. Olá AM é responsável por controlar o progresso de saudação da saudação tooit de contêineres atribuída pelo RM hello. Um aplicativo pode exigir vários contêineres dependendo da natureza de saudação do aplicativo hello.

Além disso, cada aplicativo pode consistir em vários *tentativas de aplicativo* em ordem toofinish na presença de saudação de falhas, seja devido à perda de toohello de comunicação entre um AM e um mecanismo de retenção. Portanto, contêineres são concedidos a tentativa de tooa específico de um aplicativo. De certa forma, um contêiner fornece o contexto de saudação para a unidade básica de trabalho executado por um aplicativo YARN e todo o trabalho que é executado no contexto de saudação de um contêiner é executado no nó de único trabalhador de saudação em qual Olá contêiner foi alocado. Confira [Conceitos de YARN][YARN-concepts] para referência adicional.

Logs de aplicativo (e logs de contêiner Olá associada) são essenciais na depuração de aplicativos problemáticos do Hadoop. YARN fornece uma estrutura adequada para coletar, agregar e armazenar os logs do aplicativo com hello [Log agregação] [ log-aggregation] recurso. recurso de agregação de Log Olá torna acessar logs de aplicativo mais determinista, ele agrega logs em todos os contêineres em um nó de trabalho e as armazena como um agregado arquivo de log por nó de trabalho no sistema de arquivos padrão Olá após a conclusão de um aplicativo. Seu aplicativo pode usar centenas ou milhares de contêineres, mas os logs para todos os contêineres são executados em um nó único trabalho sempre será tooa agregado de arquivo único, resultando em um arquivo de log por nó de trabalho usado pelo seu aplicativo. Agregação de log é habilitada por padrão em clusters de HDInsight (versão 3.0 e posterior), e agregados de logs podem ser encontrados no contêiner de padrão de saudação do cluster em Olá local a seguir:

    wasb:///app-logs/<user>/logs/<applicationId>

Nesse local, *usuário* é Olá nome de usuário de saudação que iniciou o aplicativo hello, e *applicationId* é o identificador exclusivo de saudação de um aplicativo conforme atribuído pelo RM. YARN de saudação

Olá agregados logs não são diretamente legíveis, como eles são gravados um [TFile][T-file], [formato binário] [ binary-format] indexado pelo contêiner. YARN fornece CLI ferramentas toodump esses logs como texto sem formatação para aplicativos ou contêineres de interesse. Você pode exibir esses logs como texto sem formatação, executando uma saudação comandos YARN a seguir diretamente em nós de cluster de saudação (depois de se conectar tooit via RDP):

    yarn logs -applicationId <applicationId> -appOwner <user-who-started-the-application>
    yarn logs -applicationId <applicationId> -appOwner <user-who-started-the-application> -containerId <containerId> -nodeAddress <worker-node-address>


## <a name="yarn-resourcemanager-ui"></a>IU do ResourceManager YARN
Olá YARN ResourceManager UI é executado no nó principal do cluster hello e pode ser acessado por meio de saudação do painel portal do Azure:

1. Entrar muito[portal do Azure](https://portal.azure.com/).
2. No menu à esquerda do hello, clique em **procurar**, clique em **Clusters HDInsight**, clique em um cluster baseado no Windows que você deseja tooaccess Olá YARN logs de aplicativo.
3. Clique no menu superior Olá **painel**. Você verá uma página aberta em uma nova guia do navegador chamada **Console de Consulta do HDInsight**.
4. Em **Console de Consulta do HDInsight**, clique em **Interface do Usuário do YARN**.

[YARN-timeline-server]:http://hadoop.apache.org/docs/r2.4.0/hadoop-yarn/hadoop-yarn-site/TimelineServer.html
[log-aggregation]:http://hortonworks.com/blog/simplifying-user-logs-management-and-access-in-yarn/
[T-file]:https://issues.apache.org/jira/secure/attachment/12396286/TFile%20Specification%2020081217.pdf
[binary-format]:https://issues.apache.org/jira/browse/HADOOP-3315
[YARN-concepts]:http://hortonworks.com/blog/apache-hadoop-yarn-concepts-and-applications/
