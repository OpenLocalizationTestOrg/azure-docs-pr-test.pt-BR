---
title: "aaaAzure Data Lake repositório Spark ajuste diretrizes de desempenho | Microsoft Docs"
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
ms.openlocfilehash: da1d172e9cb1199ad95605ea1718e78559f79650
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="performance-tuning-guidance-for-spark-on-hdinsight-and-azure-data-lake-store"></a>Diretrizes de ajuste do desempenho para o Spark no HDInsight e Azure Data Lake Store

Quando o ajuste de desempenho no Spark, é necessário tooconsider número de saudação de aplicativos que serão executados no cluster.  Por padrão, você pode executar 4 aplicativos simultaneamente em seu cluster HDI (Observação: configuração padrão de saudação é toochange assunto).  Você pode decidir toouse menos aplicativos para que você pode substituir as configurações padrão de saudação e usar mais de um cluster de saudação para esses aplicativos.  

## <a name="prerequisites"></a>Pré-requisitos

* **Uma assinatura do Azure**. Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Uma conta do repositório Azure Data Lake**. Para obter instruções sobre como um, ver toocreate [Introdução ao repositório Azure Data Lake](data-lake-store-get-started-portal.md)
* **Cluster de HDInsight do Azure** com acesso tooa conta do repositório Data Lake. Confira [Criar um cluster HDInsight com o Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md). Verifique se que você habilitar a área de trabalho remota para o cluster de saudação.
* **Executando o cluster Spark no Azure Data Lake Store**.  Para obter mais informações, consulte [dados de tooanalyze cluster Use HDInsight Spark no repositório Data Lake](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-use-with-data-lake-store)
* **Diretrizes de ajuste de desempenho no ADLS**.  Para ver os conceitos gerais de desempenho, confira [Diretrizes de ajuste de desempenho do Data Lake Store](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-performance-tuning-guidance) 

## <a name="parameters"></a>parâmetros

Ao executar Spark trabalhos, aqui estão configurações mais importantes de saudação que podem ser ajustado tooincrease desempenho ADLS:

* **Num executores** -Olá várias tarefas simultâneas que podem ser executadas.

* **Memória de executor** -quantidade de saudação de memória alocada tooeach executor.

* **Núcleos de executor** -número de saudação de núcleos alocado tooeach executor.                     

**Num executores** executores Num definirá o número máximo de saudação de tarefas que podem ser executados em paralelo.  número real de saudação de tarefas que podem ser executados em paralelo é determinado pelo Olá recursos de memória e CPU disponíveis no cluster.

**Memória de executor** esta é Olá quantidade de memória que está sendo alocada tooeach executor.  memória de saudação necessária para cada executor é dependente de trabalho hello.  Para operações complexas, memória Olá precisa toobe superior.  Para operações simples como leitura e gravação, os requisitos de memória serão menores.  Olá quantidade de memória para cada executor pode ser exibida no Ambari.  No Ambari, navegar tooSpark e exiba a guia de configurações de saudação.  

**Núcleos de executor** isso define a quantidade de saudação de núcleos usados por executor, que determina o número de saudação de threads paralelos que podem ser executados por executor.  Por exemplo, se executor núcleos = 2, e cada executor pode executar tarefas paralelas 2 no executor hello.  núcleos de executor Olá necessário dependerá trabalho hello.  Trabalhos com uso intensivo de E/S não exigem uma grande quantidade de memória por tarefa para que cada executor possa manipular mais tarefas paralelas.

Por padrão, dois núcleos YARN virtuais são definidos para cada núcleo físico ao executar o Spark no HDInsight.  Esse número fornece um bom equilíbrio entre a simultaneidade e a quantidade de mudanças de contexto de vários threads.  

## <a name="guidance"></a>Diretrizes

Durante a execução Spark toowork analíticos cargas de trabalho com dados no repositório Data Lake, recomendamos que você use hello mais recente HDInsight versão tooget Olá melhor desempenho com repositório Data Lake. Quando o trabalho estiver mais e/s intensiva, determinados parâmetros podem ser configurado tooimprove desempenho.  O Azure Data Lake Store é uma plataforma de armazenamento altamente escalonável que pode lidar com uma alta taxa de transferência.  Se o trabalho Olá consiste principalmente de leitura ou gravações, aumentando a simultaneidade para tooand de e/s do repositório Azure Data Lake pode melhorar o desempenho.

Há alguns simultaneidade tooincrease de maneiras gerais para trabalhos de e/s intensivas.

**Etapa 1: Determinar quantos aplicativos estão em execução no cluster** – você deve saber quantos aplicativos estão em execução no cluster Olá incluindo Olá atual.  valores padrão de saudação para cada Spark configuração assume que há 4 aplicativos em execução simultaneamente.  Portanto, você terá apenas 25% de cluster de saudação disponível para cada aplicativo.  tooget um desempenho melhor, você pode substituir os padrões de saudação alterando o número de saudação de executores.  

**Etapa 2: Configurar a memória de executor** – hello primeiro tooset é Olá executor-memória.  memória Olá dependerá trabalho Olá que você está indo toorun.  Você pode aumentar a simultaneidade ao alocar menos memória por executor.  Se você vir fora de exceções de memória ao executar o trabalho, você deve aumentar o valor de saudação para esse parâmetro.  Uma alternativa é tooget mais memória usando um cluster que tem a maior quantidade de memória ou aumentar o tamanho de saudação do cluster.  Mais memória permitirá toobe executores mais usado, o que significa que mais de simultaneidade.

**Etapa 3: Definir o executor núcleos** – para e/s intensivas cargas de trabalho que não tenham operações complexas, é bom toostart com um grande número de núcleos de executor tooincrease Olá inúmeras tarefas paralelas por executor.  A configuração de núcleos de executor too4 é um bom começo.   

    executor-cores = 4
Aumentar Olá número de núcleos de executor lhe dará mais paralelismo para que você possa testar com diferentes de núcleos de executor.  Para trabalhos que possuem operações mais complexas, você deve reduzir o número de saudação de núcleos por executor.  Se executor-cores for definido para um valor maior que 4, a coleta de lixo poderá tornar-se ineficiente e prejudicar o desempenho.

**Etapa 4: determinar a quantidade de memória YARN no cluster** – essas informações estão disponíveis no Ambari.  Navegue tooYARN e exiba a guia de configurações de saudação.  Olá memória YARN é exibido nesta janela.  
Observação: enquanto você estiver na janela de saudação, você também pode ver tamanho do contêiner saudação padrão YARN.  Olá tamanho do contêiner YARN é Olá igual a memória por parâmetro de executor.

    Total YARN memory = nodes * YARN memory per node
**Etapa 5: calcular num-executors**

**Calcular a restrição de memória** -parâmetro de executores num hello é restrito por memória ou por CPU.  restrição de memória Olá é determinada pela quantidade de saudação de memória YARN disponível para seu aplicativo.  Você deve pegar a memória YARN total e dividi-la por executor-memory.  restrição de saudação precisa toobe eliminação dimensionado para número de saudação de aplicativos para nós dividimos pelo número de saudação de aplicativos.

    Memory constraint = (total YARN memory / executor memory) / # of apps   
**Calcular a restrição de CPU** -Olá restrição de CPU é calculado como Olá total núcleos virtuais divididos pelo número de saudação de núcleos por executor.  Há dois núcleos virtuais para cada núcleo físico.  Restrição de memória toohello semelhante, temos dividida pelo número de saudação de aplicativos.

    virtual cores = (nodes in cluster * # of physical cores in node * 2)
    CPU constraint = (total virtual cores / # of cores per executor) / # of apps
**Definir num executores** – parâmetro num executores de hello é determinado executando Olá mínimo de restrição de memória de saudação e restrição de saudação da CPU. 

    num-executors = Min (total virtual Cores / # of cores per executor, available YARN memory / executor-memory)   
Configurar um número maior de num-executors não implica necessariamente em aumento de desempenho.  Considere que adicionar mais executores adicionará sobrecarga extra para cada executor adicional, o que pode degradar o desempenho.  Num executores é limitado pelos recursos de cluster de saudação.    

## <a name="example-calculation"></a>Exemplo de cálculo

Digamos que você tenha o composto de 8 nós D4v2 um cluster que está em execução 2 aplicativos incluindo Olá você vai toorun no momento.  

**Etapa 1: Determinar quantos aplicativos estão em execução no cluster** – você souber que tem 2 aplicativos no cluster, incluindo Olá um for toorun.  

**Etapa 2: definir executor-memory** – neste exemplo, determinamos que 6 GB de executor-memory será suficiente para trabalho com uso intensivo de E/S.  

    executor-memory = 6GB
**Etapa 3: Definir o executor núcleos** – como este é um trabalho de e/s intensivo, podemos definir número Olá de núcleos de cada too4 executor.  Configuração de núcleos por toolarger do executor de 4 pode causar problemas de coleta de lixo.  

    executor-cores = 4
**Etapa 4: Determinar a quantidade de memória YARN em cluster** – navegarmos toofind tooAmbari out cada D4v2 tem 25 GB de memória do YARN.  Uma vez que há 8 nós, a memória disponível YARN Olá é multiplicada por 8.

    Total YARN memory = nodes * YARN memory* per node
    Total YARN memory = 8 nodes * 25GB = 200GB
**Etapa 5: Calcular num executores** – parâmetro num executores de hello é determinado executando Olá mínimo de restrição de memória hello e restrição de CPU Olá dividido por Olá n º de aplicativos em execução no Spark.    

**Calcular a restrição de memória** – restrição de memória Olá é calculada como memória YARN total Olá dividida pela memória Olá por executor.

    Memory constraint = (total YARN memory / executor memory) / # of apps   
    Memory constraint = (200GB / 6GB) / 2   
    Memory constraint = 16 (rounded)
**Calcular a restrição de CPU** -Olá restrição de CPU é calculado como Olá núcleos yarn total divididos pelo número de saudação de núcleos por executor.
    
    YARN cores = nodes in cluster * # of cores per node * 2   
    YARN cores = 8 nodes * 8 cores per D14 * 2 = 128
    CPU constraint = (total YARN cores / # of cores per executor) / # of apps
    CPU constraint = (128 / 4) / 2
    CPU constraint = 16
**Definir num-executors**

    num-executors = Min (memory constraint, CPU constraint)
    num-executors = Min (16, 16)
    num-executors = 16    

