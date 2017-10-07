---
title: "aaaWhat está HBase em HDInsight do Azure? | Microsoft Docs"
description: "Uma introdução tooApache HBase em HDInsight, um banco de dados NoSQL compilação no Hadoop. Saiba mais sobre os casos de uso e comparar clusters de Hadoop tooother HBase."
keywords: "bigtable, nosql, o que é o hbase, apache hbase, hbase, visão geral do habase,"
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: d2a76d53-133a-4849-a30c-88d9c794391c
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: jgao
ms.openlocfilehash: 0d28378d07b1a168e38748548578be11310d2228
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-hbase-in-hdinsight-a-nosql-database-that-provides-bigtable-like-capabilities-for-hadoop"></a>O que é HBase em HDInsight: um banco de dados NoSQL que fornece capacidades semelhantes a BigTable para Hadoop
O Apache HBase é um banco de dados NoSQL de código-fonte aberto, que é compilado no Hadoop e modelado com base em Google BigTable. O HBase fornece acesso aleatório e uma coerência forte para grandes quantidades de dados não estruturados e semiestruturados em um banco de dados sem esquema, organizado por famílias de colunas.

Dados são armazenados nas linhas de saudação de uma tabela e dados dentro de uma linha são agrupados por família de coluna. HBase é um banco de dados schemaless no sentido de saudação nem Olá colunas nem o tipo de saudação dos dados armazenados nelas necessário toobe definido antes de usá-los. código do código-fonte aberto Olá escala linearmente toohandle petabytes de dados em milhares de nós. Ele pode contar com redundância de dados, processamento em lotes e outros recursos que são fornecidos por aplicativos distribuídos no ecossistema do Hadoop hello.

## <a name="how-is-hbase-implemented-in-azure-hdinsight"></a>Como o HBase é implementado no Azure HDInsight?
HDInsight HBase é oferecido como um cluster gerenciado é integrado ao ambiente do Azure de saudação. clusters de saudação são configurados toostore dados diretamente no [armazenamento do Azure](./hdinsight-hadoop-use-blob-storage.md) ou [repositório Azure Data Lake](./hdinsight-hadoop-use-data-lake-store.md), que fornece baixa latência e maior elasticidade de opções de desempenho e custo. Isso permite que os clientes toobuild sites interativos que trabalhar com grandes conjuntos de dados, serviços de toobuild que armazenam dados de telemetria e o sensor de milhões de pontos de extremidade e tooanalyze esses dados com trabalhos de Hadoop. HBase e Hadoop são bons pontos de partida para o projeto de dados grande no Azure. em particular, eles podem permitir que aplicativos em tempo real toowork com grandes conjuntos de dados.

a implementação de HDInsight Olá aproveita a arquitetura de expansão de saudação do HBase tooprovide automática fragmentação de tabelas, consistência forte para leituras e gravações e o failover automático. O desempenho é aprimorado pelo cache na memória para leituras e streaming de alta produtividade para gravações. O cluster do HBase pode ser criado dentro da rede virtual. Para obter detalhes, confira [Criar clusters HDInsight na Rede Virtual do Azure][hbase-provision-vnet].

## <a name="how-is-data-managed-in-hdinsight-hbase"></a>Como os dados no HBase do HDInsight são gerenciados?
Dados podem ser gerenciados no HBase usando Olá `create`, `get`, `put`, e `scan` comandos de saudação shell do HBase. Dados são gravados toohello banco de dados usando `put` e ler usando `get`. Olá `scan` comando é usado tooobtain dados de várias linhas em uma tabela. Dados também podem ser gerenciados usando Olá HBase c# API, que fornece uma biblioteca de cliente sobre Olá API REST do HBase. Um banco de dados HBase também pode ser consultado usando o Hive. Para um toothese Introdução modelos de programação, consulte [iniciar o uso do HBase com Hadoop no HDInsight][hbase-get-started]. Processadores colegas também estão disponíveis, que permite o processamento de dados em nós de saudação desse banco de dados de saudação do host.

> [!NOTE]
> Não há suporte para thrift pelo HBase no HDInsight.
>

## <a name="scenarios-use-cases-for-hbase"></a>Cenários: casos de uso para o HBase
Olá caso de uso canônico para o qual BigTable (e, por extensão, HBase) foi criado foi pesquisa na web. Mecanismos de pesquisa cria índices que mapeiam as páginas da web do termos toohello que os contém. Mas há muitos outros casos de uso aos quais o HBase se ajusta, muitos dos quais são descritos nesta seção.

* Repositório de valor-chave
  
    O HBase pode ser usado como um repositório de valor-chave e é adequado para gerenciar sistemas de mensagens. O Facebook utiliza o HBase para seu sistema de mensagens, e ele é ideal para armazenar e gerenciar comunicações pela Internet. WebTable usa toosearch HBase para e gerenciar tabelas que são extraídas das páginas da Web.
* Dados de sensor
  
    O HBase é útil para capturar dados que são coletados gradativamente de várias fontes. Isso inclui análise de dados sociais, séries temporais, manter painéis interativos atualizados com tendências e contadores e gerenciar sistemas de logs de auditorias. Os exemplos incluem Bloomberg Traders terminal e Olá tempo série banco de dados aberto (OpenTSDB), que armazena e fornece acesso toometrics coletados sobre integridade de saudação do sistemas de servidor.
* Consulta em tempo real
  
    [Phoenix](http://phoenix.apache.org/) é um mecanismo de consulta SQL para o HBase no Apache. Ele é acessado como um driver JDBC e permite consultar e gerenciar tabelas do HBase utilizando o SQL.
* HBase como uma plataforma
  
    Os aplicativos podem ser executados sobre o HBase utilizando-o como um armazenamento de dados. Exemplos incluem Phoenix, OpenTSDB, Kiji e Titan. Os aplicativos também podem ser integrados ao HBase. Exemplos incluem Hive, Pig, Solr, Storm, Flume, Impala, Spark, Ganglia e Drill.

## <a name="next-steps"></a>Próximas etapas
* [Introdução ao uso do HBase com Hadoop no HDInsight][hbase-get-started]
* [Criar clusters do HDInsight na Rede Virtual do Azure][hbase-provision-vnet]
* [Configurar a replicação do HBase no HDInsight](hdinsight-hbase-replication.md)
* [Analisar dados de sentimento no Twitter com o HBase no HDInsight][hbase-twitter-sentiment]
* [Usar Maven toobuild Java aplicativos que usam HBase com HDInsight (Hadoop)][hbase-build-java-maven]

## <a name="see-also"></a>Consulte também
* [HBase no Apache](https://hbase.apache.org/)
* [Bigtable: um sistema de armazenamento distribuído para dados estruturados](http://research.google.com/archive/bigtable.html)

[hbase-provision-vnet]: hdinsight-hbase-provision-vnet.md

[hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md

[hbase-build-java-maven]: hdinsight-hbase-build-java-maven.md

[hdinsight-use-hive]: hdinsight-use-hive.md

[hdinsight-storage]: ../hdinsight-hadoop-use-blob-storage.md

[hbase-get-started]: http://azure.microsoft.com/documentation/articles/hdinsight-hbase-get-started/

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-management-portal]: https://portal.azure.com/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md

[apache-hadoop]: http://hadoop.apache.org/
