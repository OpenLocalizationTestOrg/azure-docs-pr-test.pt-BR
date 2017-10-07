---
title: "Transformação de dados: Processo e dados de transformação | Microsoft Docs"
description: "Saiba como tootransform dados ou processar dados no Azure Data Factory usando Hadoop, aprendizado de máquina ou análise Azure Data Lake."
keywords: "transformação de dados, dados de processo, transformar dados, atividade de transformação"
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 39786731-1e4b-40a4-81b7-d06e127427aa
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: 917d617259699b0e71de3a0e0c17463d00f2e0a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="transform-data-in-azure-data-factory"></a>Transformar dados no Azure Data Factory
> [!div class="op_single_selector"]
> * [Hive](data-factory-hive-activity.md)  
> * [Pig](data-factory-pig-activity.md)  
> * [MapReduce](data-factory-map-reduce.md)  
> * [Streaming do Hadoop](data-factory-hadoop-streaming-activity.md)
> * 
            [Machine Learning](data-factory-azure-ml-batch-execution-activity.md) 
> * [Procedimento armazenado](data-factory-stored-proc-activity.md)
> * [U-SQL da Análise Data Lake](data-factory-usql-activity.md)
> * [Personalizado do .NET](data-factory-use-custom-activities.md)

## <a name="overview"></a>Visão geral
Este artigo explica as atividades de transformação de dados na fábrica de dados do Azure que você pode usar tootransform e processa os dados brutos em previsões e ideias. Uma atividade de transformação é executada em um ambiente de cálculo, como um cluster do Azure HDInsight ou um Lote do Azure. Ele fornece tooarticles links com informações detalhadas sobre cada atividade de transformação.

Fábrica de dados oferece suporte a saudação seguindo as atividades de transformação de dados que podem ser adicionadas muito[pipelines](data-factory-create-pipelines.md) seja individualmente ou encadeada com outra atividade.

> [!NOTE]
> Para uma explicação com instruções passo a passo, confira o artigo [Criar um pipeline com a transformação do Hive](data-factory-build-your-first-pipeline.md) .  
> 
> 

## <a name="hdinsight-hive-activity"></a>Atividade de Hive do HDInsight
Hello atividade Hive do HDInsight em um pipeline da fábrica de dados executa consultas de Hive por conta própria ou cluster do HDInsight baseados no Windows/Linux sob demanda. Confira o artigo [Atividade de Hive](data-factory-hive-activity.md) para obter detalhes sobre essa atividade. 

## <a name="hdinsight-pig-activity"></a>Atividade de Pig do HDInsight
Hello atividade de Pig de HDInsight em um pipeline da fábrica de dados executa consultas de Pig por conta própria ou cluster do HDInsight baseados no Windows/Linux sob demanda. Confira o artigo [Atividade de Pig](data-factory-pig-activity.md) para obter detalhes sobre essa atividade. 

## <a name="hdinsight-mapreduce-activity"></a>Atividade de MapReduce do HDInsight
Hello atividade MapReduce do HDInsight em um pipeline da fábrica de dados executa programas de MapReduce por conta própria ou cluster do HDInsight baseados no Windows/Linux sob demanda. Confira o artigo [Atividade de MapReduce](data-factory-map-reduce.md) para obter detalhes sobre essa atividade.

## <a name="hdinsight-streaming-activity"></a>Atividade de Streaming do HDInsight
Hello atividade de transmissão do HDInsight em um pipeline da fábrica de dados executa programas de transmissão do Hadoop por conta própria ou cluster do HDInsight baseados no Windows/Linux sob demanda. Confira [Atividade de HDInsight Streaming](data-factory-hadoop-streaming-activity.md) para obter detalhes sobre essa atividade.

## <a name="hdinsight-spark-activity"></a>Atividade do HDInsight Spark
Hello atividade de HDInsight Spark em um pipeline da fábrica de dados executa programas Spark no seu próprio cluster HDInsight. Para obter detalhes, consulte [Invocar programas Spark do Azure Data Factory](data-factory-spark.md) para obter detalhes. 

## <a name="machine-learning-activities"></a>Atividades de Machine Learning
Habilita de fábrica de dados do Azure tooeasily você criar pipelines que usam o aprendizado de máquina publicado web service para análise preditiva. Usando Olá [atividade de execução de lote](data-factory-azure-ml-batch-execution-activity.md#invoking-a-web-service-using-batch-execution-activity) em um pipeline da fábrica de dados do Azure, você pode invocar um toomake previsões do aprendizado de máquina web serviço nos dados de saudação em lote.

Ao longo do tempo, modelos de previsão de saudação em Olá aprendizado de máquina experiências de pontuação necessário toobe treinados novamente usando novos conjuntos de dados de entrada. Depois que você treinamento, você deseja tooupdate Olá pontuação serviço web com hello treinados novamente o modelo de aprendizado de máquina. Você pode usar o hello [atividade de atualização de recurso](data-factory-azure-ml-batch-execution-activity.md#updating-models-using-update-resource-activity) tooupdate Olá web service com hello recentemente treinado.  

Confira [Usar atividades de Machine Learning](data-factory-azure-ml-batch-execution-activity.md) para obter detalhes sobre essas atividades de Machine Learning. 

## <a name="stored-procedure-activity"></a>Atividade de procedimento armazenado
Você pode usar a atividade de procedimento armazenado do SQL Server de saudação em um pipeline de fábrica de dados tooinvoke um procedimento armazenado em uma saudação armazenamentos de dados a seguir: Azure SQL Database, Azure SQL Data Warehouse, banco de dados do SQL Server em sua empresa ou de uma VM do Azure. Confira o artigo [Atividade de procedimento armazenado](data-factory-stored-proc-activity.md) para obter detalhes.  

## <a name="data-lake-analytics-u-sql-activity"></a>Atividade do U-SQL do Data Lake Analytics
A atividade de U-SQL do Data Lake Analytics executa um script U-SQL em um cluster do Azure Data Lake Analytics. Confira o artigo [Atividade de U-SQL do Data Analytics](data-factory-usql-activity.md) para obter detalhes. 

## <a name="net-custom-activity"></a>Atividade personalizada do .NET
Se você precisar tootransform dados de forma que não é suportada pela fábrica de dados, você pode criar uma atividade personalizada com sua própria lógica de processamento de dados e usar atividade Olá no pipeline de saudação. Você pode configurar Olá personalizado .NET atividade toorun usando um serviço de lote do Azure ou um cluster Azure HDInsight. Confira o artigo [Usar atividades personalizadas](data-factory-use-custom-activities.md) para obter detalhes. 

Você pode criar uma atividade personalizada toorun R scripts em seu cluster HDInsight com R instalado. Veja [Executar scripts R usando o Azure Data Factory](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample). 

## <a name="compute-environments"></a>Ambientes de computação
Criar um serviço vinculado para o ambiente de computação hello e, em seguida, usar o serviço de saudação vinculado ao definir uma atividade de transformação. Há dois tipos de ambientes de computação com suporte do Data Factory. 

1. **Sob demanda**: nesse caso, o ambiente de computação Olá é totalmente gerenciado pela fábrica de dados. É automaticamente criado pelo Olá serviço da fábrica de dados antes de um trabalho é enviado tooprocess dados e removida quando o trabalho de saudação estiver concluído. Você pode configurar e controlar as configurações granulares do ambiente de computação sob demanda Olá para execução do trabalho, gerenciamento de cluster e ações de inicialização. 
2. **Traga seu próprio**: nesse caso, você pode registrar no Data Factory seu próprio ambiente de computação (por exemplo, o cluster HDInsight) como um serviço vinculado. ambiente de computação de saudação é gerenciado por você e Olá serviço da fábrica de dados usa as atividades de saudação do tooexecute. 

Consulte [serviços vinculados de computação](data-factory-compute-linked-services.md) toolearn artigo sobre suportados pela fábrica de dados de serviços de computação. 

## <a name="summary"></a>Resumo
Oferece suporte de fábrica de dados do Azure Olá atividades de transformação de dados a seguir e Olá ambientes de computação para atividades de saudação. atividades de transformação Olá podem ser adicionado toopipelines individualmente ou encadeada com outra atividade.

| Atividades de transformação de dados | Ambiente de computação |
|:--- |:--- |
| [Hive](data-factory-hive-activity.md) |HDInsight [Hadoop] |
| [Pig](data-factory-pig-activity.md) |HDInsight [Hadoop] |
| [MapReduce](data-factory-map-reduce.md) |HDInsight [Hadoop] |
| [Streaming do Hadoop](data-factory-hadoop-streaming-activity.md) |HDInsight [Hadoop] |
| [Atividades de Machine Learning: execução do Lote e recurso de atualização](data-factory-azure-ml-batch-execution-activity.md) |VM do Azure |
| [Procedimento armazenado](data-factory-stored-proc-activity.md) |SQL Azure, Azure SQL Data Warehouse ou SQL Server |
| [U-SQL da Análise Data Lake](data-factory-usql-activity.md) |Análise Azure Data Lake |
| [DotNet](data-factory-use-custom-activities.md) |HDInsight [Hadoop] ou Lote do Azure |

