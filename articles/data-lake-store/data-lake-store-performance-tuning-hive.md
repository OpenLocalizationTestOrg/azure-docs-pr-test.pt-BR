---
title: "aaaAzure Data Lake repositório Hive ajuste diretrizes de desempenho | Microsoft Docs"
description: Diretrizes de ajuste de desempenho para Hive do Azure Data Lake Store
services: data-lake-store
documentationcenter: 
author: stewu
manager: amitkul
editor: stewu
ms.assetid: ebde7b9f-2e51-4d43-b7ab-566417221335
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/19/2016
ms.author: stewu
ms.openlocfilehash: e44daeb6ad3b64e893c709df63b56444a330729f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="performance-tuning-guidance-for-hive-on-hdinsight-and-azure-data-lake-store"></a>Diretrizes de ajuste do desempenho para Hive no HDInsight e Azure Data Lake Store

saudação padrão configurações foram definidas tooprovide bom desempenho em muitos casos de uso diferentes.  Para consultas intensivas de e/s, Hive pode ser ajustado tooget um melhor desempenho com ADLS.  

## <a name="prerequisites"></a>Pré-requisitos

* **Uma assinatura do Azure**. Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Uma conta do repositório Azure Data Lake**. Para obter instruções sobre como um, ver toocreate [Introdução ao repositório Azure Data Lake](data-lake-store-get-started-portal.md)
* **Cluster de HDInsight do Azure** com acesso tooa conta do repositório Data Lake. Confira [Criar um cluster HDInsight com o Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md). Verifique se que você habilitar a área de trabalho remota para o cluster de saudação.
* **Execução do Hive no HDInsight**.  toolearn sobre como executar trabalhos de Hive no HDInsight, consulte [Use Hive no HDInsight] (https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-use-hive)
* **Diretrizes de ajuste de desempenho no ADLS**.  Para ver os conceitos gerais de desempenho, confira [Diretrizes de ajuste de desempenho do Data Lake Store](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-performance-tuning-guidance)

## <a name="parameters"></a>parâmetros

Aqui estão Olá tootune de configurações mais importante para melhorar o desempenho de ADLS:

* **hive.tez.container.Size** – quantidade de saudação de memória usada por cada tarefas

* **tez.grouping.min-size** – tamanho mínimo de cada mapeador

* **tez.grouping.max-size** – tamanho máximo de cada mapeador

* **hive.exec.reducer.bytes.per.reducer** – tamanho de cada redutor

**hive.tez.container.Size** -tamanho do contêiner Olá determina a quantidade de memória está disponível para cada tarefa.  Isso é a entrada principal Olá para controle de simultaneidade Olá no Hive.  

**tamanho de tez.Grouping.Min** – este parâmetro permite que você tooset tamanho mínimo do hello de cada mapeador.  Se o número de saudação de mapeadores Tez escolhe for menor do que o valor desse parâmetro hello, Tez usará valor Olá definido aqui.  

**tamanho de tez.Grouping.max** – Olá parâmetro permite que você tooset tamanho máximo do hello de cada mapeador.  Se o número de saudação de mapeadores Tez escolhe for maior que o valor desse parâmetro hello, Tez usará valor Olá definido aqui.  

**hive.EXEC.reducer.bytes.Per.reducer** – esse parâmetro define o tamanho de saudação de cada Redutor.  Por padrão, o tamanho de cada redutor é de 256 MB.  

## <a name="guidance"></a>Diretrizes

**Definir hive.exec.reducer.bytes.per.reducer** – valor padrão de saudação funciona bem quando os dados de saudação são descompactados.  Para dados compactados, você deve reduzir o tamanho de saudação do Redutor hello.  

**Definir hive.tez.container.size** – em cada nó, a memória é especificada por yarn.nodemanager.resource.memory-mb e deve ser corretamente definida no cluster HDI por padrão.  Para obter informações adicionais sobre a configuração de memória apropriada Olá em YARN, consulte [lançar](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-hive-out-of-memory-error-oom).

Cargas de trabalho intensivas de e/s podem se beneficiar mais paralelismo, diminuindo o tamanho do contêiner Tez hello. Isso fornece o usuário hello mais contêineres que aumenta a simultaneidade.  No entanto, algumas consultas do Hive exigem uma quantidade significativa de memória (por exemplo, MapJoin).  Se a tarefa de saudação não tem memória suficiente, você receberá um limite de exceção de memória durante o tempo de execução.  Se você receber fora de exceções de memória, você deve aumentar memória hello.   

Olá simultâneas número de tarefas em execução ou paralelismo será ser limitado pelo total de memória YARN hello.  número de saudação de contêineres YARN ditará quantas tarefas simultâneas podem ser executadas.  memória YARN toofind Olá por nó, você pode ir tooAmbari.  Navegue tooYARN e exiba a guia de configurações de saudação.  Olá memória YARN é exibido nesta janela.  

        Total YARN memory = nodes * YARN memory per node
        # of YARN containers = Total YARN memory / Tez container size
desempenho de chave tooimproving Hello usando ADLS é simultaneidade de saudação tooincrease tanto quanto possível.  Tez calcula automaticamente o número de saudação de tarefas que devem ser criados para que não seja necessário tooset-lo.   

## <a name="example-calculation"></a>Exemplo de cálculo

Digamos que você tenha um cluster D14 de 8 nós.  

    Total YARN memory = nodes * YARN memory per node
    Total YARN memory = 8 nodes * 96GB = 768GB
    # of YARN containers = 768GB / 3072MB = 256

## <a name="limitations"></a>Limitações
**Limitação do ADLS** 

UIf ocorrências Olá limites de largura de banda fornecida pelo ADLS, comece toosee falhas de tarefas. Isso poderia ser identificado observando os erros de limitação nos logs de tarefa.  Você pode diminuir o paralelismo Olá aumentando o tamanho do contêiner Tez.  Se precisar de mais simultaneidade para seu trabalho, entre em contato conosco.   

toocheck se você estiver obtendo limitadas, você precisa tooenable Olá log de depuração no lado do cliente de saudação. Veja como fazer isso:

1. Coloque Olá propriedade nas propriedades de log4j Olá na seção de configuração a seguir. Isso pode ser feito de modo de exibição do Ambari: log4j.logger.com.microsoft.azure.datalake.store=DEBUG reiniciar todos os nós/serviço Olá para efeito de tootake Olá config.

2. Se você estiver obtendo limitada, você verá o código de erro HTTP 429 Olá no arquivo de log de hive hello. arquivo de log de hive Hello está em /tmp/&lt;usuário&gt;/hive.log

## <a name="further-information-on-hive-tuning"></a>Mais informações sobre o ajuste do Hive

Veja a seguir alguns blogs que ajudarão a ajustar as consultas do Hive:
* [Otimizar consultas do Hive para Hadoop no HDInsight](https://azure.microsoft.com/en-us/documentation/articles/hdinsight-hadoop-optimize-hive-query/)
* [Solução de problemas de desempenho em consultas do Hive](https://blogs.msdn.microsoft.com/bigdatasupport/2015/08/13/troubleshooting-hive-query-performance-in-hdinsight-hadoop-cluster/)
* [Debate sobre como otimizar o Hive no HDInsight](https://channel9.msdn.com/events/Machine-Learning-and-Data-Sciences-Conference/Data-Science-Summit-2016/MSDSS25)
