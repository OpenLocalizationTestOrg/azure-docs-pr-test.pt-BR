---
title: "aaaOverview da ciência de dados usando o Spark no Azure HDInsight | Microsoft Docs"
description: "Kit de ferramentas do Hello MLlib Spark traz recursos toohello distribuída HDInsight ambiente de modelagem de aprendizado de máquina considerável."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: a4e1de99-a554-4240-9647-2c6d669593c8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/15/2017
ms.author: deguhath;bradsev;gokuma
ms.openlocfilehash: 515705684a46917c2741bf063d439b1cda016abb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-data-science-using-spark-on-azure-hdinsight"></a>Visão geral da ciência de dados usando Spark no Azure HDInsight
[!INCLUDE [machine-learning-spark-modeling](../../includes/machine-learning-spark-modeling.md)]

Este conjunto de tópicos mostra como as tarefas de ciência de dados comum do HDInsight Spark toocomplete de toouse como ingestão de dados, engenharia de recurso, modelagem e avaliação do modelo. dados de saudação usados são um exemplo de hello 2013 NYC táxi viagem e passagens conjunto de dados. modelos internos de saudação incluem gradientes árvores aumentadas, florestas aleatórias e regressão logística e linear. Olá tópicos também mostram como toostore esses modelos no Azure blob storage (WASB) e como tooscore e avaliar o desempenho previsível. Os tópicos mais avançados abordam como os modelos podem ser treinados usando a validação cruzada e a limpeza de hiperparâmetro. Este tópico de visão geral também faz referência a tópicos de saudação que descrevem como tooset backup Olá cluster Spark que você precisa toocomplete etapas Olá Olá orientações fornecidas. 

## <a name="spark-and-mllib"></a>Spark e MLlib
[Spark](http://spark.apache.org/) é uma estrutura de processamento paralelo do código-fonte aberto que dá suporte à memória no desempenho do processamento tooboost Olá de aplicativos analíticos grandes de dados. mecanismo de processamento do Spark Olá é construído para velocidade, facilidade de uso e análise sofisticada. Os recursos de computação distribuída na memória do Spark tornam uma boa escolha para algoritmos de iterativo Olá usados em cálculos de gráfico e de aprendizado de máquina. [MLlib](http://spark.apache.org/mllib/) é biblioteca de aprendizado de máquina escalonável do Spark que traz Olá algorítmico ambiente distribuído do toothis de recursos de modelagem. 

## <a name="hdinsight-spark"></a>HDInsight Spark
[HDInsight Spark](../hdinsight/hdinsight-apache-spark-overview.md) hello Azure hospedado oferta do código-fonte aberto Spark. Ela também inclui suporte para **blocos de anotações do Jupyter PySpark** no cluster do Spark Olá que pode executar consultas interativas do Spark SQL para transformar, filtrar e visualização de dados armazenados em Blobs do Azure (WASB). PySpark é hello API Python para Spark. trechos de código de saudação que fornecem soluções hello e mostram Olá gráficos relevantes toovisualize Olá dados aqui executados em blocos de anotações do Jupyter instalados nos clusters do Spark hello. etapas de modelagem Olá nestes tópicos contêm código que mostra como tootrain, avaliar, salvar e consumir cada tipo de modelo. 

## <a name="setup-spark-clusters-and-jupyter-notebooks"></a>Instalação: Clusters do Spark e Notebooks Jupyter
As etapas de configuração e o código são fornecidos neste passo a passo para usar um HDInsight Spark 1.6. Porém, notebooks Jupyter são fornecidos tanto para o HDInsight Spark 1.6 quanto para os clusters Spark 2.0. Uma descrição da saudação toothem de anotações e links são fornecidos no hello [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) para o repositório do GitHub Olá que os contém. Além disso, Olá código aqui e em blocos de anotações Olá vinculado é genérico e deve funcionar em qualquer cluster do Spark. Se você não estiver usando o HDInsight Spark, as etapas de configuração e gerenciamento de cluster Olá podem ser ligeiramente diferentes da que é mostrado aqui. Para sua conveniência, aqui estão os links de saudação blocos de anotações do Jupyter toohello para Spark 1.6 (toobe executar no kernel do pySpark de saudação do servidor de Jupyter Notebook de saudação) e o Spark 2.0 (toobe executar no kernel do pySpark3 de saudação do servidor de Jupyter Notebook de saudação):

### <a name="spark-16-notebooks"></a>Blocos de notas Spark 1.6
Esses blocos são toobe executado no kernel de pySpark de saudação do servidor de notebook Jupyter.

- [pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb): fornece informações sobre como tooperform de exploração de dados, modelagem e pontuação com vários algoritmos diferentes.
- [pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): inclui tópicos de notebook nº 1 e o desenvolvimento de modelos usando ajude e validação cruzada de hiperparâmetro.
- [pySpark-machine-learning-data-science-spark-model-consumption.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-model-consumption.ipynb): mostra como toooperationalize um modelo de salvo usando Python no HDInsight clusters.

### <a name="spark-20-notebooks"></a>Blocos de notas Spark 2.0
Esses blocos são toobe executado no kernel de pySpark3 de saudação do servidor de notebook Jupyter.

- [Spark2.0-pySpark3-Machine-Learning-data-Science-Spark-Advanced-data-exploration-Modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): este arquivo fornece informações sobre como tooperform a exploração de dados, modelagem e pontuação no Spark 2.0 clusters usando Olá trip NYC táxi e passagens-conjunto de dados descrito [aqui](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data). Este bloco de anotações pode ser um bom ponto de partida para explorar rapidamente código Olá que fornecemos para Spark 2.0. Para um bloco de anotações mais detalhado analisa Olá dados NYC táxi, consulte o próximo bloco de anotações de saudação nesta lista. Consulte as notas de saudação seguinte lista que comparam esses blocos de anotações. 
- [Spark2.0 pySpark3_NYC_Taxi_Tip_Regression.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_NYC_Taxi_Tip_Regression.ipynb): esse arquivo mostra como tooperform dados disputa (operações Spark SQL e dataframe), a exploração, modelagem e pontuação usando Olá trip NYC táxi e passagens conjunto de dados descrito [ aqui](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data).
- [Spark2.0 pySpark3_Airline_Departure_Delay_Classification.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_Airline_Departure_Delay_Classification.ipynb): esse arquivo mostra como tooperform dados disputa (operações Spark SQL e dataframe), a exploração, modelagem e pontuação usando Olá conhecida saída em tempo de aérea conjunto de dados de 2011 e 2012. Podemos integrada Olá aérea dataset com hello a toomodeling de anteriores de dados (por exemplo, windspeed, temperatura, altitude etc.) do aeroporto clima, para que esses recursos de tempo podem ser incluídos no modelo de saudação.

<!-- -->

> [!NOTE]
> Olá aérea dataset foi adicionado toohello 2.0 Spark notebooks toobetter ilustram o uso de saudação de algoritmos de classificação. Consulte Olá links para obter informações sobre o conjunto de dados de saída em tempo de passagens áreas e conjunto de dados de tempo a seguir:

>- Dados de partidas no horário em aeroportos: [http://www.transtats.bts.gov/ONTIME/](http://www.transtats.bts.gov/ONTIME/)

>- Dados de clima aeroporto: [https://www.ncdc.noaa.gov/](https://www.ncdc.noaa.gov/) 
> 
> 

<!-- -->

<!-- -->

> [!NOTE]
Olá Spark 2.0 blocos de anotações Olá táxi NYC e conjuntos de dados de atraso de voo de aérea podem levar 10 minutos ou mais toorun (dependendo do tamanho de saudação do cluster HDI). primeiro notebook no hello acima da lista Hello mostra muitos aspectos de exploração de dados hello, visualização e ML do modelo de treinamento em um bloco de anotações que utiliza menos toorun de tempo com convertidos NYC conjunto de dados, no qual Olá táxi e passagens arquivos tem sido previamente Unidos: [ Spark2.0-pySpark3-Machine-Learning-data-Science-Spark-Advanced-data-exploration-Modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb) este bloco de anotações leva uma quantidade menor tempo toofinish (2-3 minutos) e pode ser um bom ponto de partida para explorar rapidamente código Olá temos fornecido para Spark 2.0. 

<!-- -->

Para obter orientação sobre operacionalização de saudação de um modelo Spark 2.0 e o consumo de modelo para pontuação, consulte Olá [documento 1.6 Spark no consumo](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-model-consumption.ipynb) para obter um exemplo de etapas de saudação necessárias de estrutura de tópicos. toouse isso no Spark 2.0, substitua o arquivo de código Python Olá com [esse arquivo](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Python/Spark2.0_ConsumeRFCV_NYCReg.py).

### <a name="prerequisites"></a>Pré-requisitos
Olá procedimentos a seguir está relacionada tooSpark 1.6. Para a versão de hello Spark 2.0, use Olá notebooks descrito e vinculados toopreviously. 

1.Você precisa ter uma assinatura do Azure. Se ainda não tiver uma, veja [Obter avaliação gratuita do Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).

2. você precisa de um toocomplete de cluster do Spark 1.6 este passo a passo. toocreate um, consulte as instruções de saudação fornecidas no [Introdução: criar o Apache Spark no Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md). Olá cluster tipo e versão especificado a partir do hello **Selecionar tipo de Cluster** menu. 

![Configurar cluster](./media/machine-learning-data-science-spark-overview/spark-cluster-on-portal.png)

<!-- -->

> [!NOTE]
> Para um tópico que mostra como as tarefas de toocomplete de toouse Scala em vez de Python para um processo de ciência de dados de ponta a ponta, consulte Olá [ciência de dados usando Scala com Spark no Azure](machine-learning-data-science-process-scala-walkthrough.md).
> 
> 

<!-- -->

> [!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]
> 
> 

## <a name="hello-nyc-2013-taxi-data"></a>Olá dados NYC 2013 táxi
Olá dados NYC táxi viagem é cerca de 20 GB de arquivos compactados valores separados por vírgulas (CSV) (~ 48 GB descompactado), que inclui mais de milhões de 173 hello e viagens individuais é pago para cada viagem. Cada registro de viagem inclui Olá retirada e local de entrega e hora, número de licença hack anônimos (driver) e número de medallion (id exclusiva do táxi). dados saudação abrange todas as viagens no ano Olá 2013 e são fornecidos em dois conjuntos de dados a seguir para cada mês de saudação:

1. arquivos CSV 'trip_data' Hello contêm detalhes de processamento, como o número de passageiros, acompanhar e pontos de redução, trip duração e o comprimento da viagem. Aqui estão alguns exemplos de registros:
   
        medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count,trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
2. arquivos CSV 'trip_fare' Hello contêm detalhes da tarifa Olá pagado para cada viagem, como tipo de pagamento, quantidade de passagens, sobretaxa e impostos, dicas e pedágio e quantidade total de saudação paga. Aqui estão alguns exemplos de registros:
   
        medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

Levamos um exemplo de 0,1% desses arquivos e viagem Olá unidas\_dados e viagem\_passagens arquivos CSV em um único conjunto de dados toouse como conjunto de dados de entrada de saudação para este passo a passo. viagem de toojoin de chave exclusivo Olá\_dados e viagem\_passagens é composta de campos de saudação: medallion, ataques\_licença e retirada\_datetime. Cada registro do conjunto de dados Olá contém Olá atributos que representam uma viagem NYC táxi a seguir:

| Campo | Breve descrição |
| --- | --- |
| medallion |Licença do táxi em forma anônima (ID exclusiva do táxi) |
| hack_license |Número de licença do carro em forma anônima |
| vendor_id |ID do fornecedor do serviço de táxi |
| rate_code |Tarifa praticada pelos táxis em NYC |
| store_and_fwd_flag |Sinalizador de que os dados foram armazenados no veículo e encaminhados posteriormente |
| pickup_datetime |Data e hora do início da corrida |
| dropoff_datetime |Data e hora do final da corrida |
| pickup_hour |Hora da corrida |
| pickup_week |Pegue a semana do ano Olá |
| weekday |Dia da semana (intervalo de 1 a 7) |
| passenger_count |Número de passageiros em uma corrida de táxi |
| trip_time_in_secs |Tempo da corrida em segundos |
| trip_distance |Distância percorrida na corrida em milhas |
| pickup_longitude |Longitude da corrida |
| pickup_latitude |Latitude da corrida |
| dropoff_longitude |Longitude do final da corrida |
| dropoff_latitude |Latitude do final da corrida |
| direct_distance |Distância direta entre os locais inicial e final da corrida |
| payment_type |Tipo de pagamento (dinheiro, cartão de crédito etc.) |
| fare_amount |Valor da tarifa |
| surcharge |Taxa adicional |
| mta_tax |Imposto da MTA |
| tip_amount |Valor da gorjeta |
| tolls_amount |Valor dos pedágios |
| total_amount |Valor total |
| tipped |Gorjeta (0/1 para não ou sim) |
| tip_class |Classe da gorjeta (0: US$ 0, 1: US$ 0 a 5, 2: US$ 6 a 10, 3: US$ 11 a 20, 4: mais de US$ 20) |

## <a name="execute-code-from-a-jupyter-notebook-on-hello-spark-cluster"></a>Execute o código de um bloco de anotações do Jupyter no cluster do Spark Olá
Você pode iniciar Olá anotações do Jupyter do hello portal do Azure. Localize seu cluster Spark no painel e clique em página de gerenciamento de tooenter para seu cluster. bloco de anotações do hello tooopen associado Olá Spark cluster, clique em **painéis do Cluster** -> **Jupyter Notebook** .

![Painéis de cluster](./media/machine-learning-data-science-spark-overview/spark-jupyter-on-portal.png)

Você também pode procurar muito***https://CLUSTERNAME.azurehdinsight.net/jupyter*** tooaccess Olá blocos de anotações do Jupyter. Substitua parte CLUSTERNAME Olá essa URL com nome de saudação do seu próprio cluster. Senha de saudação é necessária para os blocos de anotações do administrador conta tooaccess hello.

![Procurar Notebooks Jupyter](./media/machine-learning-data-science-spark-overview/spark-jupyter-notebook.png)

Selecione PySpark toosee um diretório que contém alguns exemplos de blocos de anotações predefinidos que usam Olá PySpark API.hello blocos de anotações que contêm exemplos de código Olá para este conjunto de tópico Spark estão disponíveis em [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/Spark/pySpark)

Você pode carregar blocos de anotações Olá diretamente do [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/Spark/pySpark) servidor de notebook Jupyter toohello em seu cluster Spark. Na página inicial de saudação do seu Jupyter, clique em Olá **carregar** botão Olá parte direita da tela hello. Ele abre o explorador de arquivos. Aqui você pode colar a URL GitHub (conteúdo bruto) Olá Olá Notebook e clique em **abrir**. 

Consulte o nome do arquivo hello em sua lista de arquivos do Jupyter com um **carregar** novamente. Clique nesse botão **Carregar** . Agora você importou notebook hello. Repita a saudação de tooupload essas etapas outros blocos de anotações deste passo a passo.

> [!TIP]
> Clique links Olá no seu navegador e selecione **Copiar Link** tooget Olá github URL bruta de conteúdo. Você pode colar essa URL em Olá Jupyter carregar arquivo explorer caixa de diálogo.
> 
> 

Agora você pode:

* Consulte o código de saudação clicando notebook hello.
* Executar cada célula pressionando **SHIFT-ENTER**.
* Execute o bloco de anotações inteiro Olá clicando no **célula** -> **executar**.
* Use a visualização automática Olá de consultas.

> [!TIP]
> núcleo de PySpark Olá automaticamente visualiza saída Olá de consultas SQL (HiveQL). Recebem Olá opção tooselect entre vários tipos diferentes de visualizações (tabela, pizza, linha, área ou barra) usando Olá **tipo** botões de menu no bloco de anotações de saudação:
> 
> 

![Curva ROC de regressão logística de abordagem genérica](./media/machine-learning-data-science-spark-overview/pyspark-jupyter-autovisualization.png)

## <a name="whats-next"></a>O que vem a seguir?
Agora que são configurados com um cluster HDInsight Spark e carregar blocos de anotações do Jupyter hello, você está pronto toowork tópicos Olá que correspondem a três PySpark toohello de anotações. Eles mostram como tooexplore seus dados e, em seguida, como toocreate e consumir modelos. Olá avançados de exploração de dados e modelagem notebook mostra como tooinclude limpeza de validação cruzada, parâmetro hyper e avaliação do modelo. 

**Exploração de dados e modelagem com Spark:** explorar Olá conjunto de dados e criar, pontuação e avaliar modelos de aprendizado de máquina Olá trabalhando Olá [criar modelos de classificação e regressão binários para dados com hello Spark Kit de ferramentas MLlib](machine-learning-data-science-spark-data-exploration-modeling.md) tópico.

**Consumo de modelo:** toolearn como modelos de classificação e regressão Olá tooscore criada neste tópico, consulte [pontuação e avaliar modelos de aprendizado de máquina criados Spark](machine-learning-data-science-spark-model-consumption.md).

**Validação cruzada e limpeza de hiperparâmetro**: confira [Modelagem e exploração de dados avançados com o Spark](machine-learning-data-science-spark-advanced-data-exploration-modeling.md) para saber como os modelos podem ser treinados usando a validação cruzada e a limpeza de hiperparâmetro

