---
title: "Opções de contexto aaaCompute para o servidor do R no HDInsight - Azure | Microsoft Docs"
description: "Saiba mais sobre opções Olá computação diferentes contexto disponível toousers ao servidor do R no HDInsight"
services: HDInsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 0deb0b1c-4094-459b-94fc-ec9b774c1f8a
ms.service: HDInsight
ms.custom: hdinsightactive
ms.devlang: R
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/19/2017
ms.author: bradsev
ms.openlocfilehash: b3b0d0cc3caa390797dcff8c73d66cd3ad78bcaa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="compute-context-options-for-r-server-on-hdinsight"></a>Opções de contexto de computação para o Servidor R no HDInsight

Microsoft R Server no Azure HDInsight controla como as chamadas são executadas pelo contexto de computação Olá configuração. Este artigo descreve Olá opções toospecify disponível se e como a execução é paralelizada entre núcleos do nó de borda de saudação ou o cluster HDInsight.

nó de borda de saudação de um cluster fornece um local conveniente tooconnect toohello cluster e toorun seus scripts de R. Com um nó de borda, você deve ter funções de opção de execução hello paralelizado distribuída Olá de ScaleR entre núcleos de saudação do servidor de nó de borda hello. Você também pode executá-los em nós de saudação do cluster Olá por meio do ScaleR Hadoop mapear redução ou Spark contextos de computação.

## <a name="microsoft-r-server-on-azure-hdinsight"></a>Microsoft R Server no Azure HDInsight
[Microsoft R Server no Azure HDInsight](hdinsight-hadoop-r-server-overview.md) fornece recursos mais recentes Olá para análise de R. Ele pode usar dados armazenados em um contêiner HDFS no seu [BLOBs do Azure](../storage/common/storage-introduction.md "armazenamento de BLOBs do Azure") conta de armazenamento, um repositório Data Lake ou sistema de arquivos Linux local hello. Desde o R Server se baseia no R de software livre, Olá R aplicativos que você criar podem aplicar Olá 8000 + pacotes de software livre R. Eles também podem usar rotinas de saudação em [RevoScaleR](https://msdn.microsoft.com/microsoft-r/scaler/scaler), pacote de análise de dados grande da Microsoft que acompanha o R Server.  

## <a name="compute-contexts-for-an-edge-node"></a>Contextos de computação para um nó de extremidade
Em geral, um script R que é executado no servidor do R no nó de borda Olá é executado em interpretador Olá R nesse nó. exceções de saudação são as etapas que chame uma função ScaleR. Olá ScaleR chamadas executados em um ambiente de computação que é determinado por como você definir o contexto de computação ScaleR hello.  Quando você executa o script R de um nó de borda, os valores possíveis de Olá Olá computação contexto são:

- local sequencial (*‘local’*)
- local paralelo (*‘localpar’*)
- Map Reduce
- Spark

Olá *'local'* e *'localpar'* opções diferem apenas em como **rxExec** chamadas são executadas. Ambos executar o outras chamadas de função rx de forma paralela entre núcleos disponíveis, a menos que especificado o contrário pelo uso da saudação ScaleR **numCoresToUse** opção, por exemplo `rxOptions(numCoresToUse=6)`. Opções de execução paralela oferecem um desempenho ideal.

Olá, a tabela a seguir resume Olá que vários computação tooset de opções de contexto, como as chamadas são executadas:

| Contexto de computação  | Como tooset                      | Contexto de execução                        |
| ---------------- | ------------------------------- | ---------------------------------------- |
| Local sequencial | rxSetComputeContext(‘local’)    | Execução em paralelo entre núcleos de saudação do servidor de nó de borda hello, exceto para chamadas de rxExec, que são executados em série |
| Local paralelo   | rxSetComputeContext(‘localpar’) | Execução em paralelo entre núcleos de saudação do servidor de nó de borda Olá |
| Spark            | RxSpark()                       | Execução distribuída em paralelo por meio do Spark em nós de saudação do cluster HDI Olá |
| Map Reduce       | RxHadoopMR()                    | Execução distribuída em paralelo por meio de mapear redução em nós de saudação do cluster HDI Olá |

## <a name="guidelines-for-deciding-on-a-compute-context"></a>Diretrizes para decidir em um contexto de computação

Olá três opções você escolher que fornecem a execução em paralelo dependendo da natureza de saudação do seu trabalho de análise, o tamanho de saudação e o local de saudação de seus dados. Não há nenhuma fórmula simple que informa quais toouse do contexto de computação. No entanto, há alguns princípios que podem ajudá-lo a fazer a escolha certa hello, ou, pelo menos, ajudá-lo a restringir suas escolhas antes de executar um parâmetro de comparação. Esses princípios básicos incluem:

- sistema de arquivos Linux local Olá é mais rápido do que o HDFS.
- Análises repetidas são mais rápidas se dados saudação for locais, e se ele está em XDF.
- É preferível toostream pequenas quantidades de dados de uma fonte de dados de texto. Se a quantidade de saudação de dados for maior, converta tooXDF antes da análise.
- sobrecarga de saudação de cópia ou nó de borda de toohello Olá dados para análise de streaming se torna impossível para grandes quantidades de dados.
- Spark é mais rápido do que Map Reduce para análise no Hadoop.

Devido a esses princípios, hello seções a seguir oferecem alguns princípios gerais para selecionar um contexto de computação.

### <a name="local"></a>Local
* Se a quantidade de saudação do tooanalyze de dados é pequena e não requer análise repetida, fluxo-lo diretamente no hello análise rotina usando *'local'* ou *'localpar'*.
* Se a quantidade de saudação do tooanalyze de dados é pequeno ou médio porte e requer análises repetidas, em seguida, copie-o sistema de arquivos local toohello, importá-lo tooXDF e analisá-los por meio de *'local'* ou *'localpar'*.

### <a name="hadoop-spark"></a>Hadoop Spark
* Se a quantidade de saudação do tooanalyze de dados for grande, em seguida, importá-lo tooa DataFrame Spark usando **RxHiveData** ou **RxParquetData**, ou tooXDF no HDFS (a menos que o armazenamento é um problema) e analisá-los usando Olá Spark contexto de computação.

### <a name="hadoop-map-reduce"></a>Hadoop Map Reduce
* Use o contexto de computação de mapear redução Olá somente se você encontrar um problema insuperáveis com contexto de computação Spark Olá pois ela é geralmente mais lenta.  

## <a name="inline-help-on-rxsetcomputecontext"></a>Ajuda embutida em rxSetComputeContext
Para obter mais informações e exemplos de ScaleR contextos de computação, consulte Olá embutido Ajuda em R no método de rxSetComputeContext hello, por exemplo:

    > ?rxSetComputeContext

Você também pode consultar toohello "[ScaleR Distributed Computing guia](https://msdn.microsoft.com/microsoft-r/scaler-distributed-computing)" que está disponível na Olá [R Server MSDN](https://msdn.microsoft.com/library/mt674634.aspx "R Server no MSDN") biblioteca.

## <a name="next-steps"></a>Próximas etapas
Neste artigo, você aprendeu sobre opções de saudação toospecify disponível se e como a execução é paralelizada entre núcleos do nó de borda de saudação ou o cluster HDInsight. toolearn mais informações sobre como toouse R Server com HDInsight clusters, consulte Olá seguintes tópicos:

* [Visão geral do Servidor R no Hadoop](hdinsight-hadoop-r-server-overview.md)
* [Introdução ao Servidor R para o Hadoop](hdinsight-hadoop-r-server-get-started.md)
* [Adicionar servidor RStudio tooHDInsight (se não adicionado durante a criação do cluster)](hdinsight-hadoop-r-server-install-r-studio.md)
* [Opções de Armazenamento do Azure para o Servidor R no HDInsight](hdinsight-hadoop-r-server-storage.md)

