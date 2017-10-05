---
title: Diretrizes de ajuste de desempenho para Spark do Azure Data Lake Store | Microsoft Docs
description: Diretrizes de ajuste de desempenho para Spark do Azure Data Lake Store
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
ms.openlocfilehash: 2109744fb7ffdfafb7a86bbea355e119718af099
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="performance-tuning-guidance-for-spark-on-hdinsight-and-azure-data-lake-store"></a>Diretrizes de ajuste do desempenho para o Spark no HDInsight e Azure Data Lake Store

Ao realizar o ajuste de desempenho no Spark, você deve considerar o número de aplicativos estarão em execução no cluster.  Por padrão, você pode executar 4 aplicativos simultaneamente no cluster HDI (observação: a configuração padrão está sujeita a alterações).  Você pode decidir usar menos aplicativos, de modo que você possa substituir as configurações padrão e usar mais do cluster para esses aplicativos.  

## <a name="prerequisites"></a>Pré-requisitos

* **Uma assinatura do Azure**. Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Uma conta do repositório Azure Data Lake**. Para obter instruções sobre como criar uma, consulte [Introdução ao repositório Azure Data Lake](data-lake-store-get-started-portal.md)
* **Cluster HDInsight do Azure** com acesso a uma conta do Repositório Data Lake. Confira [Criar um cluster HDInsight com o Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md). Certifique-se de habilitar a área de trabalho remota para o cluster.
* **Executando o cluster Spark no Azure Data Lake Store**.  Para obter mais informações, veja [Use HDInsight Spark cluster to analyze data in Data Lake Store](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-use-with-data-lake-store) (Usar cluster HDInsight Spark para analisar dados no Data Lake Store)
* **Diretrizes de ajuste de desempenho no ADLS**.  Para ver os conceitos gerais de desempenho, confira [Diretrizes de ajuste de desempenho do Data Lake Store](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-performance-tuning-guidance) 

## <a name="parameters"></a>parâmetros

Ao executar trabalhos do Spark, aqui estão as configurações mais importantes que podem ser ajustadas para aumentar o desempenho no ADLS:

* **Num-executors** – O número de tarefas simultâneas que podem ser executadas.

* **Executor-memory** – A quantidade de memória alocada para cada executor.

* **Executor-cores** – O número de núcleos alocados para cada executor.                     

**Num-executors** – Num-executors definirá o número máximo de tarefas que podem ser executadas em paralelo.  O número real de tarefas que podem ser executadas em paralelo é limitado pela memória e recursos de CPU disponíveis no cluster.

**Executor-memory** – Esta é a quantidade de memória sendo alocada para cada executor.  A memória necessária para cada executor depende do trabalho.  Para operações complexas, a memória deve ser maior.  Para operações simples como leitura e gravação, os requisitos de memória serão menores.  A quantidade de memória para cada executor pode ser exibida no Ambari.  No Ambari, navegue até o Spark e exiba a guia Configurações.  

**Executor-cores** – Isso define a quantidade de núcleos usados por executor, o que determina o número de threads paralelos que podem ser executados por executor.  Por exemplo, se executor-cores = 2, então cada executor pode executar duas tarefas paralelas no executor.  O valor de executor-cores necessário dependerá do trabalho.  Trabalhos com uso intensivo de E/S não exigem uma grande quantidade de memória por tarefa para que cada executor possa manipular mais tarefas paralelas.

Por padrão, dois núcleos YARN virtuais são definidos para cada núcleo físico ao executar o Spark no HDInsight.  Esse número fornece um bom equilíbrio entre a simultaneidade e a quantidade de mudanças de contexto de vários threads.  

## <a name="guidance"></a>Diretrizes

Ao executar cargas de trabalho analíticas do Spark para trabalhar com os dados no Data Lake Store, é recomendável que você use as versões mais recentes do HDInsight para obter o melhor desempenho com o Data Lake Store. Quando o trabalho faz uso mais intensivo de E/S, determinados parâmetros podem ser configurados para melhorar o desempenho.  O Azure Data Lake Store é uma plataforma de armazenamento altamente escalonável que pode lidar com uma alta taxa de transferência.  Se o trabalho consiste principalmente em leitura ou gravação, aumentar a simultaneidade de E/S para e o Azure Data Lake Store pode aumentar o desempenho.

Existem algumas maneiras gerais de aumentar a simultaneidade para os trabalhos com uso intensivo de E/S.

**Etapa 1: determinar quantos aplicativos estão em execução no cluster** – você deve saber quantos aplicativos estão em execução no cluster, incluindo o atual.  Os valores padrão para cada configuração do Spark assume que há quatro aplicativos em execução simultaneamente.  Portanto, você terá apenas 25% do cluster disponível para cada aplicativo.  Para obter um melhor desempenho, você pode substituir os padrões por meio da alteração do número de executores.  

**Etapa 2: configurar executor-memory** – a primeira coisa a definir é o executor-memory.  A memória dependerá do trabalho que você pretende executar.  Você pode aumentar a simultaneidade ao alocar menos memória por executor.  Se você vir exceções de memória insuficiente quando executar o trabalho, você deverá aumentar o valor desse parâmetro.  Uma alternativa é de obter mais memória pelo uso de um cluster com maiores quantidades de memória ou pelo aumento do tamanho do cluster.  Mais memória permitirá o uso de mais executores, o que significa mais simultaneidade.

**Etapa 3: definir executor-cores** – para cargas de trabalho com uso intensivo de E/S que não têm operações complexas, é recomendável iniciar com um número alto de núcleos de executor para aumentar o número de tarefas paralelas por executor.  Configurar executor-cores para 4 é um bom começo.   

    executor-cores = 4
Aumentar o número de núcleos de executor lhe dará mais paralelismo para que você pode experimentar com diferentes núcleos de executor.  Para trabalhos que têm operações mais complexas, você deve reduzir o número de núcleos por executor.  Se executor-cores for definido para um valor maior que 4, a coleta de lixo poderá tornar-se ineficiente e prejudicar o desempenho.

**Etapa 4: determinar a quantidade de memória YARN no cluster** – essas informações estão disponíveis no Ambari.  Navegue até YARN e exiba a guia Configurações.  A memória YARN é exibida nessa janela.  
Observação: enquanto estiver na janela, você também poderá ver o tamanho do contêiner YARN padrão.  O tamanho do contêiner YARN é o mesmo que o do parâmetro de memória por executor.

    Total YARN memory = nodes * YARN memory per node
**Etapa 5: calcular num-executors**

**Calcular a restrição de memória** – o parâmetro num-executors é restrito por memória ou por CPU.  A restrição de memória é determinada pela quantidade de memória YARN disponível para seu aplicativo.  Você deve pegar a memória YARN total e dividi-la por executor-memory.  O ajuste de escala da restrição precisa ser realizado de acordo com número de aplicativos, então realizamos a divisão pelo número de aplicativos.

    Memory constraint = (total YARN memory / executor memory) / # of apps   
**Calcular a restrição de CPU** – a restrição de CPU é calculada como o total de núcleos virtuais dividido pelo número de núcleos por executor.  Há dois núcleos virtuais para cada núcleo físico.  Semelhante ao que ocorre na restrição de memória, realizamos a divisão pelo número de aplicativos.

    virtual cores = (nodes in cluster * # of physical cores in node * 2)
    CPU constraint = (total virtual cores / # of cores per executor) / # of apps
**Definir num-executors** – o parâmetro num-executors será determinado utilizando o mínimo da restrição de memória e da restrição de CPU. 

    num-executors = Min (total virtual Cores / # of cores per executor, available YARN memory / executor-memory)   
Configurar um número maior de num-executors não implica necessariamente em aumento de desempenho.  Considere que adicionar mais executores adicionará sobrecarga extra para cada executor adicional, o que pode degradar o desempenho.  Num-executors é limitado pelos recursos de cluster.    

## <a name="example-calculation"></a>Exemplo de cálculo

Digamos que você tem atualmente um cluster composto de oito nós D4v2 e que está executando dois aplicativos, incluindo aquele que você pretende executar.  

**Etapa 1: determinar quantos aplicativos estão em execução no cluster** – você sabe que tem dois aplicativos no cluster, incluindo aquele que você pretende executar.  

**Etapa 2: definir executor-memory** – neste exemplo, determinamos que 6 GB de executor-memory será suficiente para trabalho com uso intensivo de E/S.  

    executor-memory = 6GB
**Etapa 3: definir executor-cores** – como esse é um trabalho com uso intensivo de E/S, podemos definir o número de núcleos para cada executor como quatro.  Configurar o número de núcleos por executor para um valor maior do que quatro pode causar problemas na coleta de lixo.  

    executor-cores = 4
**Etapa 4: determinar a quantidade de memória YARN no cluster** – navegamos até o Ambari para descobrir que cada D4v2 tem 25 GB de memória YARN.  Como há oito nós, a memória YARN disponível é multiplicada por oito.

    Total YARN memory = nodes * YARN memory* per node
    Total YARN memory = 8 nodes * 25GB = 200GB
**Etapa 5: calcular num-executors** – o parâmetro num-executors será determinado utilizando o mínimo da restrição de memória e da restrição de CPU divididos pelo número de aplicativos em execução no Spark.    

**Calcular a restrição de memória** – a restrição de memória é calculada como a memória YARN total dividida pela memória por executor.

    Memory constraint = (total YARN memory / executor memory) / # of apps   
    Memory constraint = (200GB / 6GB) / 2   
    Memory constraint = 16 (rounded)
**Calcular a restrição de CPU** – a restrição de CPU é calculada como o total de núcleos YARN dividido pelo número de núcleos por executor.
    
    YARN cores = nodes in cluster * # of cores per node * 2   
    YARN cores = 8 nodes * 8 cores per D14 * 2 = 128
    CPU constraint = (total YARN cores / # of cores per executor) / # of apps
    CPU constraint = (128 / 4) / 2
    CPU constraint = 16
**Definir num-executors**

    num-executors = Min (memory constraint, CPU constraint)
    num-executors = Min (16, 16)
    num-executors = 16    

