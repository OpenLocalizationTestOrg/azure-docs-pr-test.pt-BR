---
title: "aaaHDInsight explicações passo a passo Spark usando PySpark e Scala no Azure | Microsoft Docs"
description: "Exemplos de saudação processo de ciência de dados de equipe que percorrer Olá o uso de PySpark e Scala em uma análise preditiva do Azure HDInsight Spark toodo."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: bradsev
ms.openlocfilehash: f8b41a8cae414586570761ba4b4eb4c239cbb981
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="hdinsight-spark-data-science-walkthroughs-using-pyspark-and-scala-on-azure"></a>Passo a passo de ciência de dados do HDInsight Spark usando PySpark e Scala no Azure

Essas instruções usam PySpark e Scala em uma análise preditiva do Azure Spark cluster toodo. Eles sigam etapas de saudação descritas em Olá processo de ciência de dados de equipe. Para obter uma visão geral de saudação processo de ciência de dados de equipe, consulte [processo de ciência de dados](data-science-process-overview.md). Para obter uma visão geral do Spark no HDInsight, consulte [tooSpark de Introdução no HDInsight](../hdinsight/hdinsight-apache-spark-overview.md).

Orientações de ciência de dados adicionais que execute Olá processo de ciência de dados do Team são agrupadas por Olá **plataforma** que eles usam: 

[!INCLUDE [tdsp-walkthroughs-by-platform](../../includes/tdsp-walkthroughs-by-platform.md)]

## <a name="predict-taxi-tips-using-pyspark-on-azure-spark"></a>Prever gorjetas de táxi usando PySpark no Azure Spark

Olá [Use Spark no Azure HDInsight](machine-learning-data-science-spark-overview.md) passo a passo usa dados de Nova York táxis toopredict se uma dica é pago e intervalo de saudação de valores esperado toobe paga. Ele usa Olá processo de ciência de dados de equipe em um cenário usando um [cluster Spark no HDInsight](https://azure.microsoft.com/services/hdinsight/) toostore, explorar e apresentam dados de engenharia de viagem de táxi NYC disponível publicamente hello e passagens de conjunto de dados. Este tópico de visão geral configura você com um cluster HDInsight Spark e hello Jupyter PySpark notebooks usadas no restante Olá Olá passo a passo. Esses blocos mostram como tooexplore seus dados e, em seguida, como toocreate e consumir modelos. Olá avançados de exploração de dados e modelagem notebook mostra como tooinclude limpeza de validação cruzada, parâmetro hyper e avaliação do modelo.

### <a name="data-exploration-and-modeling-with-spark"></a>Modelagem e exploração de dados com Spark 
Explorar Olá conjunto de dados e criar, pontuação e avaliar modelos de aprendizado de máquina Olá trabalhando Olá [criar modelos de classificação e regressão binários para dados com o Kit de ferramentas do hello Spark MLlib](machine-learning-data-science-spark-data-exploration-modeling.md) tópico.

### <a name="model-consumption"></a>Consumo do modelo
toolearn como modelos de classificação e regressão Olá tooscore criada neste tópico, consulte [pontuação e avaliar modelos de aprendizado de máquina criados Spark](machine-learning-data-science-spark-model-consumption.md).

### <a name="cross-validation-and-hyperparameter-sweeping"></a>Validação cruzada e limpeza de hiperparâmetro
Confira [Modelagem e exploração de dados avançados com o Spark](machine-learning-data-science-spark-advanced-data-exploration-modeling.md) para saber como os modelos podem ser treinados usando a validação cruzada e a limpeza de hiperparâmetro.


## <a name="predict-taxi-tips-using-scala-on-azure-spark"></a>Prever gorjetas de táxi usando Scala no Azure Spark

Olá [Scala Use com Spark no Azure](machine-learning-data-science-process-scala-walkthrough.md) passo a passo usa dados de Nova York táxis toopredict se uma dica é pago e intervalo de saudação de valores esperado toobe paga. Ele mostra como toouse Scala para tarefas de aprendizado de máquina supervisionado com biblioteca de aprendizado de máquina do hello Spark (MLlib) e SparkML pacotes em um cluster Spark no HDInsight. Orienta você pelas tarefas de saudação que constituem Olá [processo de ciência de dados](http://aka.ms/datascienceprocess): inclusão de dados e exploração, visualização, engenharia de recurso, modelagem e consumo de modelo. modelos internos de saudação incluem gradientes árvores aumentadas, florestas aleatórias e regressão logística e linear.


## <a name="next-steps"></a>Próximas etapas

Para obter uma discussão dos componentes-chave Olá que compõem a saudação processo de ciência de dados de equipe, consulte [visão geral do processo de ciência de dados de equipe](data-science-process-overview.md).

Para obter uma discussão do ciclo de vida do processo de ciência de dados de equipe Olá que você pode usar toostructure seus projetos de ciência de dados, consulte [ciclo de vida do processo de ciência de dados de equipe](data-science-process-lifecycle.md). ciclo de vida de saudação descreve as etapas de hello, do início toofinish, que projetos normalmente seguem quando eles são executados. 

