---
title: "aaaAzure diretrizes de ajuste de desempenho do dados Lake repositório | Microsoft Docs"
description: Diretrizes de ajuste de desempenho do Azure Data Lake Store
services: data-lake-store
documentationcenter: 
author: stewu
manager: amitkul
editor: cgronlun
ms.assetid: ebde7b9f-2e51-4d43-b7ab-566417221335
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/30/2017
ms.author: stewu
ms.openlocfilehash: 939faa068c0f81d18d9533956f4d336bc4d0cbe3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tuning-azure-data-lake-store-for-performance"></a>Ajustando o desempenho do Azure Data Lake Store

O Data Lake Store dá suporte a alta taxa de transferência para análise de uso intensivo de E/S e movimentação de dados.  No repositório Azure Data Lake, usando a taxa de transferência disponível – valor Olá de dados que podem ser lidos ou gravados por segundo – é importante tooget Olá obter um melhor desempenho.  Isso é obtido executando o maior número possível de leituras e gravações em paralelo.

![Desempenho do Data Lake Store](./media/data-lake-store-performance-tuning-guidance/throughput.png)

Pode ser dimensionado tooprovide Olá necessário taxa de transferência para o cenário de análise de todos os repositório Azure Data Lake. Por padrão, uma conta do repositório Azure Data Lake fornece automaticamente taxa de transferência suficiente toomeet necessidades de saudação de uma categoria ampla de casos de uso. Para casos de saudação onde os clientes ficar saudação padrão limite, Olá conta ADLS pode ser configurado tooprovide mais taxa de transferência entrando em contato com o suporte da Microsoft.

## <a name="data-ingestion"></a>Ingestão de dados

Ingestão de dados de um tooADLS do sistema de origem, é importante tooconsider que Olá hardware de origem, o hardware de rede de origem e tooADLS de conectividade de rede pode ser o gargalo de hello.  

![Desempenho do Data Lake Store](./media/data-lake-store-performance-tuning-guidance/bottleneck.png)

É importante tooensure que Olá movimentação de dados não é afetado por esses fatores.

### <a name="source-hardware"></a>Hardware de Origem

Se você estiver usando computadores locais ou máquinas virtuais no Azure, você deve selecionar cuidadosamente hardware apropriado hello. Para Hardware de disco de origem, prefira tooHDDs SSDs e escolha o hardware de disco com eixos mais rápidos. Para Hardware de rede de origem, use o mais rápido possível de NICs hello.  No Azure, recomendamos Azure D14 VMs que têm o disco adequadamente poderoso hello e hardware de rede.

### <a name="network-connectivity-tooazure-data-lake-store"></a>Repositório Data Lake do conectividade tooAzure de rede

conectividade de rede de saudação entre a fonte de dados e armazenamento do Azure Data Lake às vezes pode ser o gargalo hello. Quando os dados de origem forem locais, considere o uso de uma conexão dedicada com o [Azure ExpressRoute](https://azure.microsoft.com/en-us/services/expressroute/). Se sua fonte de dados estiver no Azure, o desempenho de Olá será melhor quando dados saudação estão em Olá mesma região do Azure Olá repositório Data Lake.

### <a name="configure-data-ingestion-tools-for-maximum-parallelization"></a>Configurar as ferramentas de ingestão de dados para paralelização máxima

Depois que você resolveu o hardware de origem hello e acima de afunilamentos de conectividade de rede, você está pronto tooconfigure suas ferramentas de inclusão. Olá tabela a seguir resume as configurações de chave de saudação para diversas ferramentas populares de inclusão e fornece desempenho detalhado ajuste artigos para eles.  toolearn mais sobre qual ferramenta toouse para seu cenário, visite este [artigo](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-data-scenarios).

| Ferramenta               | Configurações     | Mais detalhes                                                                 |
|--------------------|------------------------------------------------------|------------------------------|
| Powershell       | PerFileThreadCount, ConcurrentFileCount |  [Link](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-get-started-powershell#performance-guidance-while-using-powershell)   |
| AdlCopy    | Unidades do Azure Data Lake Analytics  |   [Link](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-copy-data-azure-storage-blob#performance-considerations-for-using-adlcopy)         |
| DistCp            | -m (mapper)   | [Link](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-copy-data-wasb-distcp#performance-considerations-while-using-distcp)                             |
| Fábrica de dados do Azure| parallelCopies    | [Link](../data-factory/data-factory-copy-activity-performance.md)                          |
| Sqoop           | fs.azure.block.size, -m (mapper)    |   [Link](https://blogs.msdn.microsoft.com/bigdatasupport/2015/02/17/sqoop-job-performance-tuning-in-hdinsight-hadoop/)        |

## <a name="structure-your-data-set"></a>Estruturar seu conjunto de dados

Quando dados são armazenados no repositório Data Lake, o tamanho do arquivo hello, o número de arquivos e a estrutura de pasta ter um impacto no desempenho.  Olá, seção a seguir descreve as práticas recomendadas nessas áreas.  

### <a name="file-size"></a>Tamanho do arquivo

Normalmente os mecanismos de análise, tais como HDInsight e Azure Data Lake Analytics, têm uma sobrecarga por arquivo.  Se você armazenar os dados como vários arquivos pequenos, isso poderá afetar negativamente o desempenho.  

Em geral, organize seus dados em arquivos de tamanhos maior para melhorar o desempenho.  Como regra geral, organize conjuntos de dados em arquivos de 256 MB ou maiores. Em alguns casos, como imagens e dados binários, não é possível tooprocess-los em paralelo.  Nesses casos, recomenda-se arquivos individuais de tookeep menos de 2GB.

Às vezes, os pipelines de dados limitada controle sobre dados brutos de saudação que tem muitos arquivos pequenos.  É recomendável toohave toouse para aplicativos downstream de arquivos de um processo de "culinária" gera maior.  

### <a name="organizing-time-series-data-in-folders"></a>Organizar os dados de série temporal em pastas

Para cargas de trabalho de Hive e ADLA, remoção de partição de dados de série temporal pode ajudar algumas consultas apenas um subconjunto dos dados de saudação que melhora o desempenho de leitura.    

Esses pipelines que ingerem dados de série temporal muitas vezes colocam seus arquivos com uma nomenclatura muito estruturada para arquivos e pastas. Abaixo está um exemplo muito comum para dados estruturados por data:

    \DataSet\YYYY\MM\DD\datafile_YYYY_MM_DD.tsv

Observe que informações de data e hora Olá aparecem como pastas e nome de arquivo hello.

Data e hora, a seguinte Olá é um padrão comum

    \DataSet\YYYY\MM\DD\HH\mm\datafile_YYYY_MM_DD_HH_mm.tsv

Novamente, escolha Olá feita com a organização de pasta e arquivo hello deve otimizar para Olá arquivos maiores e um número razoável de arquivos em cada pasta.

## <a name="optimizing-io-intensive-jobs-on-hadoop-and-spark-workloads-on-hdinsight"></a>Otimizar os trabalhos com uso intensivo de E/S em cargas de trabalho do Hadoop e Spark no HDInsight

Trabalhos se encaixam em uma saudação três categorias a seguir:

* **Com uso intensivo de CPU.**  Esses trabalhos têm tempos de computação longos com tempos de E/S mínimos.  Exemplos incluem aprendizado de máquina e trabalhos de processamento de linguagem natural.  
* **Com uso intensivo de memória.**  Estes trabalhos usam muita memória.  Exemplos incluem PageRank e trabalhos de análise em tempo real.  
* **Com uso intensivo de E/S.**  Esses trabalhos passam a maior parte do tempo fazendo E/S.  Um exemplo comum é um trabalho de cópia que realiza somente operações de leitura e gravação.  Outros exemplos incluem trabalhos de preparação de dados leitura muitos dados, executa alguma transformação de dados e, em seguida, grava Olá repositório toohello backup de dados.  

Olá diretrizes a seguir é apenas aplicável tooI trabalhos/S intensivos.

### <a name="general-considerations-for-an-hdinsight-cluster"></a>Considerações gerais para um cluster HDInsight

* **Versões do HDInsight.** Para melhor desempenho, use a versão mais recente de saudação do HDInsight.
* **Regiões.** Coloque repositório Olá Data Lake em Olá mesma região do cluster do HDInsight hello.  

Um cluster HDInsight é composto de dois nós principais e alguns nós de trabalho. Cada nó de trabalho fornece um número específico de núcleos e memória, que é determinada pela Olá tipo de VM.  Ao executar um trabalho, YARN é Negociador de recurso Olá que aloca a memória disponível do hello e contêineres de toocreate núcleos.  Cada contêiner é executado trabalho de Olá Olá tarefas toocomplete necessários.  Contêineres executados em paralelo tooprocess tarefas rapidamente. Portanto, o desempenho é aprimorado executando o máximo possível de contêineres paralelos.

Há três camadas em um cluster HDInsight que podem ser ajustada tooincrease Olá número de contêineres e usam a taxa de transferência disponível.  

* **Camada física**
* **Camada YARN**
* **Camada de carga de trabalho**

### <a name="physical-layer"></a>Camada física

**Execute o cluster com mais nós e/ou VMs de tamanhos maior.**  Um cluster maior permite que você toorun mais contêineres YARN conforme mostrado na imagem de saudação abaixo.

![Desempenho do Data Lake Store](./media/data-lake-store-performance-tuning-guidance/VM.png)

**Use VMs com mais largura de banda de rede.**  quantidade de saudação de largura de banda de rede pode ser um gargalo se houver menos largura de banda de rede que a taxa de transferência do repositório Data Lake.  Diferentes VMs terão diversos tamanhos de largura de banda de rede.  Escolha um tipo de VM com hello maior largura de banda de rede possível.

### <a name="yarn-layer"></a>Camada YARN

**Use contêineres YARN menores.**  Reduzir o tamanho de saudação do cada toocreate de contêiner YARN mais contêineres com hello mesma quantidade de recursos.

![Desempenho do Data Lake Store](./media/data-lake-store-performance-tuning-guidance/small-containers.png)

Dependendo de sua carga de trabalho, sempre haverá um tamanho de contêiner YARN mínimo necessário. Se você selecionar um contêiner muito pequeno, os trabalhos encontrarão problemas de falta de memória. Normalmente, contêineres YARN não devem ser menores que 1 GB. É comuns contêineres YARN de 3GB toosee. Para algumas cargas de trabalho, talvez contêineres YARN maiores sejam necessários.  

**Aumente os núcleos por contêiner YARN.**  Aumente o número de saudação de núcleos alocado tooeach contêiner tooincrease Olá número de tarefas paralelas que são executados em cada contêiner.  Isso funciona para aplicativos como Spark, que executam várias tarefas por contêiner.  Para aplicativos como o Hive que executam um único thread em cada contêiner, é melhor toohave mais contêineres em vez de mais núcleos por contêiner.   

### <a name="workload-layer"></a>Camada de carga de trabalho

**Use todos os contêineres disponíveis.**  Definir número de saudação de tarefas toobe igual ou maior que o número de saudação de recipientes disponíveis para que todos os recursos são utilizados.

![Desempenho do Data Lake Store](./media/data-lake-store-performance-tuning-guidance/use-containers.png)

**Tarefas com falha têm alto custo.** Se cada tarefa tem uma grande quantidade de dados tooprocess, falha de uma tarefa resulta em uma repetição cara.  Portanto, é melhor toocreate mais tarefas, cada uma delas processa uma pequena quantidade de dados.

Em adição toohello diretrizes gerais acima, cada aplicativo tem tootune de parâmetros diferentes disponíveis para o aplicativo específico. Olá tabela a seguir lista alguns dos tooget de parâmetros e links de saudação iniciado com o ajuste de desempenho para cada aplicativo.

| Carga de trabalho               | Tarefas do parâmetro tooset                                                         |
|--------------------|-------------------------------------------------------------------------------------|
| [Spark no HDInisight](data-lake-store-performance-tuning-spark.md)       | <ul><li>Num-executors</li><li>Executor-memory</li><li>Executor-cores</li></ul> |
| [Hive no HDInsight](data-lake-store-performance-tuning-hive.md)    | <ul><li>hive.tez.container.size</li></ul>         |
| [MapReduce no HDInsight](data-lake-store-performance-tuning-mapreduce.md)            | <ul><li>Mapreduce.map.memory</li><li>Mapreduce.job.maps</li><li>Mapreduce.reduce.memory</li><li>Mapreduce.job.reduces</li></ul> |
| [Storm no HDInsight](data-lake-store-performance-tuning-storm.md)| <ul><li>Número de processos de trabalho</li><li>Número de instâncias de spout executor</li><li>Número de instâncias de bolt executor </li><li>Número de tarefas de spout</li><li>Número de tarefas de bolt</li></ul>|

## <a name="see-also"></a>Consulte também
* [Visão geral do Repositório Azure Data Lake](data-lake-store-overview.md)
* [Introdução à Análise Data Lake do Azure](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
