---
title: aaaUse Apache Phoenix & esquilo com HBase - HDInsight do Azure | Microsoft Docs
description: "Saiba como toouse Phoenix Apache no HDInsight e como tooinstall e configurar esquilo no cluster de estação de trabalho tooconnect tooan HBase em HDInsight."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: cda0f33b-a2e8-494c-972f-ae0bb482b818
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/26/2017
ms.author: jgao
ms.openlocfilehash: a63e8c8212b7a992453ec94fa638ec3863a0ede3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-apache-phoenix-with-linux-based-hbase-clusters-in-hdinsight"></a>Usar o Apache Phoenix com clusters do HBase baseados em Linux no HDInsight
Saiba como toouse [Apache Phoenix](http://phoenix.apache.org/) no HDInsight e como toouse SQLLine. Para obter mais informações sobre o Phoenix, consulte [Phoenix em 15 minutos ou menos](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html). Para Olá gramática Phoenix, consulte [Phoenix gramática](http://phoenix.apache.org/language/index.html).

> [!NOTE]
> Para Olá informações de versão de Phoenix no HDInsight, consulte [Novidades nas versões de cluster de Hadoop Olá fornecidas pelo HDInsight?](hdinsight-component-versioning.md).
>
>

## <a name="use-sqlline"></a>Usar o SQLLine
[SQLLine](http://sqlline.sourceforge.net/) é tooexecute um utilitário de linha de comando SQL.

### <a name="prerequisites"></a>Pré-requisitos
Antes de usar SQLLine, você deve ter o seguinte hello:

* **Um cluster HBase no HDInsight**. Para obter informações sobre como provisionar o cluster HBase, consulte [Introdução ao Apache HBase no HDInsight][hdinsight-hbase-get-started].
* **Conecte toohello HBase cluster por meio do protocolo de área de trabalho remota Olá**. Para obter instruções, consulte [clusters gerenciar Hadoop em HDInsight usando Olá portal do Azure][hdinsight-manage-portal].

Quando você conectar tooan HBase cluster, é necessário tooone tooconnect de saudação Zookeepers. Cada cluster HDInsight tem três Zookeepers.

**toofind nome de host Zookeeper Olá**

1. Abra o Ambari navegando muito**https://<ClusterName>. cluster>.azurehdinsight.NET**.
2. Digite hello toologin de nome de usuário e senha do HTTP (cluster).
3. Clique em **ZooKeeper** no menu esquerdo hello. Você vê três **Servidores do ZooKeeper** listados.
4. Clique em uma saudação **ZooKeeper Server** listados. No painel de resumo hello, localize Olá **Hostname**. Ele é muito semelhante*zk1 jdolehb.3lnng4rcvp5uzokyktxs4a5dhd.bx.internal.cloudapp.net*.

**toouse SQLLine**

1. Conecte-se toohello cluster usando o SSH. Para obter mais informações, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

2. SSH, execute Olá comandos toorun SQLLine a seguir:

        cd /usr/hdp/2.2.9.1-7/phoenix/bin
        ./sqlline.py <ClusterName>:2181:/hbase-unsecure
3. Execute Olá toocreate comandos a seguir uma tabela do HBase e insira alguns dados:

        CREATE TABLE Company (COMPANY_ID INTEGER PRIMARY KEY, NAME VARCHAR(225));

        !tables

        UPSERT INTO Company VALUES(1, 'Microsoft');

        SELECT * FROM Company;

        !quit

Para obter mais informações, consulte o [Manual SQLLine](http://sqlline.sourceforge.net/#manual) e [Gramática do Phoenix](http://phoenix.apache.org/language/index.html).

## <a name="next-steps"></a>Próximas etapas
Neste artigo, você aprendeu como toouse Phoenix Apache no HDInsight.  toolearn mais, consulte:

* [Visão geral do HBase do HDInsight][hdinsight-hbase-overview]: o HBase é um banco de dados NoSQL de software livre Apache baseado no Hadoop que fornece acesso aleatório e uma sólida consistência para grandes quantidades de dados não estruturados e semiestruturados.
* [Provisionar clusters HBase na rede Virtual do Azure][hdinsight-hbase-provision-vnet]: com a integração de rede virtual, clusters HBase podem ser implantado toohello mesmo virtual de rede como seus aplicativos para que os aplicativos podem se comunicar com o HBase diretamente.
* [Configurar a replicação do HBase em HDInsight](hdinsight-hbase-replication.md): Saiba como tooconfigure HBase replicação entre dois datacenters do Azure.
* [Analisar o sentimento do Twitter com HBase em HDInsight][hbase-twitter-sentiment]: Saiba como toodo em tempo real [análise de sentimento](http://en.wikipedia.org/wiki/Sentiment_analysis) de big data usando HBase em um cluster Hadoop no HDInsight.

[azure-portal]: https://portal.azure.com
[vnet-point-to-site-connectivity]: https://msdn.microsoft.com/library/azure/09926218-92ab-4f43-aa99-83ab4d355555#BKMK_VNETPT

[hdinsight-hbase-get-started]: hdinsight-hbase-tutorial-get-started.md
[hdinsight-manage-portal]: hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp
[hdinsight-hbase-provision-vnet]: hdinsight-hbase-provision-vnet.md
[hdinsight-hbase-overview]: hdinsight-hbase-overview.md
[hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md

[hdinsight-hbase-phoenix-sqlline]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-phoenix-sqlline.png
[img-certificate]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-vpn-certificate.png
[img-vnet-diagram]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-vnet-point-to-site.png
[img-squirrel-driver]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-driver.png
[img-squirrel-alias]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-alias.png
[img-squirrel]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel.png
[img-squirrel-sql]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-sql.png
