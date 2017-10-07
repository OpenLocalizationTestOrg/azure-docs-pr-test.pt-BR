---
title: "dados aaaExplore um Hadoop de cluster e criar modelos no aprendizado de máquina do Azure | Microsoft Docs"
description: "Usando Olá, equipe de processo de ciência de dados para um cenário de ponta a ponta empregando um HDInsight Hadoop toobuild de cluster e implantar um modelo usando um conjunto de dados publicamente disponível."
services: machine-learning,hdinsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: e9e76c91-d0f6-483d-bae7-2d3157b86aa0
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: hangzh;bradsev
ms.openlocfilehash: a371032e356ffc366af0d6fbe364af281b6efd19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="hello-team-data-science-process-in-action-use-azure-hdinsight-hadoop-clusters"></a>Olá processo de ciência de dados de equipe em ação: clusters de Hadoop de HDInsight do Azure Use
Neste passo a passo, usamos Olá [processo de ciência de dados da equipe (TDSP)](data-science-process-overview.md) em um cenário de ponta a ponta usando um [cluster Azure HDInsight Hadoop](https://azure.microsoft.com/services/hdinsight/) toostore, explorar e apresentam dados de engenharia de saudação publicamente disponível [NYC táxi viagens](http://www.andresmh.com/nyctaxitrips/) dados saudação de exemplo de conjunto de dados e toodown. Modelos de dados de saudação são criados com o aprendizado de máquina do Azure toohandle binárias e multiclasse classificação e regressão tarefas de previsão.

Para uma explicação passo a passo que mostra como toohandle um conjunto de dados maior (de 1 terabyte) para um cenário semelhante usando HDInsight Hadoop clusters para processamento de dados, consulte [processo de ciência de dados do Team - usando o Azure HDInsight Hadoop Clusters em um conjunto de dados de 1 TB](machine-learning-data-science-process-hive-criteo-walkthrough.md).

Também é possível toouse uma saudação de tooaccomplish de bloco de anotações do IPython tarefas Olá apresentada passo a passo usando o conjunto de dados de 1 TB de saudação. Os usuários que seriam como tootry essa abordagem deve consultar Olá [Criteo passo a passo usando uma conexão ODBC Hive](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-hive-walkthrough-criteo.ipynb) tópico.

## <a name="dataset"></a>Descrição do conjunto de dados Corridas de Táxi em NYC
Olá dados NYC táxi viagem é cerca de 20GB de arquivos compactados valores separados por vírgulas (CSV) (~ 48GB descompactado), que inclui mais de milhões de 173 hello e viagens individuais é pago para cada viagem. Cada registro de viagem inclui Olá retirada e entrega local e a hora, hack anônimos (driver) o número de licença e número medallion (id exclusiva do táxi). dados saudação abrange todas as viagens no ano Olá 2013 e são fornecidos em dois conjuntos de dados a seguir para cada mês de saudação:

1. arquivos CSV 'trip_data' Hello contêm detalhes da visita, como o número de passageiros, coleta e pontos de redução, duração da viagem e comprimento de viagem. Aqui estão alguns exemplos de registros:
   
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

viagem de toojoin de chave exclusivo Olá\_dados e viagem\_passagens é composta de campos de saudação: medallion, ataques\_licença e retirada\_datetime.

tooget todos os de viagem específico do hello detalhes tooa relevantes, é suficiente toojoin com três chaves: hello "medallion", "hack\_licença" e "retirada\_datetime".

Descrevemos mais alguns detalhes de dados hello quando podemos armazená-los em tabelas de Hive em breve.

## <a name="mltasks"></a>Exemplos de tarefas de previsão
Quando se aproximando os dados, determinando Olá tipo de previsões que você deseja toomake com base em sua análise ajuda esclarecer tarefas Olá que você precisará tooinclude em seu processo.
Aqui estão os três exemplos de problemas de previsão que abordamos neste passo a passo cuja formulação baseia-se a saudação *dica\_quantidade*:

1. **Classificação binária**: prever ou não se uma gorjeta foi paga por uma corrida, ou seja, um *tip\_amount* maior que US$ 0 é um exemplo positivo, enquanto um *tip\_amount* de US$ 0 é um exemplo negativo.
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0
2. **Classificação multiclasse**: intervalo de saudação toopredict de quantidades de dica pago para viagem hello. Olá, nós dividimos *dica\_quantidade* em cinco compartimentos ou classes:
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0 and tip_amount <= $5
        Class 2 : tip_amount > $5 and tip_amount <= $10
        Class 3 : tip_amount > $10 and tip_amount <= $20
        Class 4 : tip_amount > $20
3. **Tarefa de regressão**: o valor de saudação toopredict de dica de saudação pago para uma viagem.  

## <a name="setup"></a>Configurar um cluster Hadoop do HDInsight para análises avançadas
> [!NOTE]
> Essa normalmente é uma tarefa **Admin** .
> 
> 

Você pode configurar um ambiente do Azure para análises avançadas que empregue um cluster HDInsight em três etapas:

1. [Criar uma conta de armazenamento](../storage/common/storage-create-storage-account.md): essa conta de armazenamento é usada para armazenar dados no Armazenamento de Blob do Azure. dados de saudação usados em clusters de HDInsight também residem aqui.
2. [Personalizar Hadoop de HDInsight do Azure processo de análise avançada e tecnologia de clusters para Olá](machine-learning-data-science-customize-hadoop-cluster.md). Esta etapa cria um cluster do Hadoop do Azure HDInsight com Anaconda Python 2.7 de 64 bits instalado em todos os nós. Há dois tooremember de etapas importantes ao personalizar o seu cluster HDInsight.
   
   * Lembre-se a conta de armazenamento Olá toolink criada na etapa 1 com o cluster HDInsight ao criá-la. Esta conta de armazenamento é usado tooaccess dados processados em cluster hello.
   * Após Olá cluster é criado, habilite o nó principal do toohello de acesso remoto de cluster hello. Navegue toohello **configuração** guia e clique em **habilitar remoto**. Esta etapa especifica as credenciais do usuário Olá usadas para logon remoto.
3. [Criar um espaço de trabalho do aprendizado de máquina do Azure](machine-learning-create-workspace.md): aprendizado de máquina do Azure este espaço de trabalho é os modelos de aprendizado de máquina toobuild usado. Essa tarefa é abordada depois de concluir uma exploração de dados inicial e para baixo usando o cluster do HDInsight de saudação de amostragem.

## <a name="getdata"></a>Obter dados de saudação de uma fonte de pública
> [!NOTE]
> Essa normalmente é uma tarefa **Admin** .
> 
> 

Olá tooget [NYC táxi viagens](http://www.andresmh.com/nyctaxitrips/) conjunto de dados de seu local público, você pode usar qualquer um dos métodos de saudação descritos em [tooand de mover dados do armazenamento de BLOBs do Azure](machine-learning-data-science-move-azure-blob.md) máquina de tooyour toocopy Olá dados.

Aqui descrevemos como usar AzCopy tootransfer Olá arquivos que contém dados. toodownload e instale o AzCopy siga as instruções de saudação em [guia de Introdução com hello o utilitário de linha de comando AzCopy](../storage/common/storage-use-azcopy.md).

1. Em uma janela de Prompt de comando, execute Olá AzCopy comandos a seguir, substituindo *< path_to_data_folder >* com destino desejado hello:

        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:https://nyctaxitrips.blob.core.windows.net/data /Dest:<path_to_data_folder> /S

1. Quando Olá cópia é concluída, um total de 24 arquivos compactados estão na pasta de dados de saudação escolhida. Descompacte Olá baixado arquivos toohello mesmo diretório em seu computador local. Tome nota da pasta Olá onde residem os arquivos de saudação descompactado. Esta pasta será chamado tooas Olá *< caminho\_para\_unzipped_data\_arquivos\>*  é o que se segue.

## <a name="upload"></a>Carregar o contêiner do hello dados toohello padrão do cluster de Hadoop de HDInsight do Azure
> [!NOTE]
> Essa normalmente é uma tarefa **Admin** .
> 
> 

No hello seguintes comandos do AzCopy, substitua Olá seguir parâmetros com valores reais de saudação que você especificou ao criar o cluster de Hadoop hello e extrair arquivos de dados de saudação.

* ***&#60; path_to_data_folder >*** diretório hello (juntamente com o caminho) no computador que contêm arquivos de dados Olá descompactado  
* ***&#60; o nome da conta de armazenamento de cluster Hadoop >*** Olá conta de armazenamento associada ao cluster HDInsight
* ***&#60; o contêiner padrão do cluster Hadoop >*** contêiner do saudação padrão usado pelo cluster. Anote esse nome de saudação do padrão de saudação contêiner é geralmente o hello mesmo nome como o próprio cluster Olá. Por exemplo, se o cluster de saudação é chamado "abc123.azurehdinsight.net", o contêiner de padrão de saudação é abc123.
* ***&#60; chave de conta de armazenamento >*** Olá chave Olá conta de armazenamento usada por seu cluster

Em um Prompt de comando ou uma janela do Windows PowerShell em seu computador, execute Olá AzCopy os dois comandos a seguir.

Esse comando carrega os dados de viagem de saudação muito***nyctaxitripraw*** diretório no contêiner de padrão de saudação do cluster de Hadoop hello.

        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:<path_to_unzipped_data_files> /Dest:https://<storage account name of Hadoop cluster>.blob.core.windows.net/<default container of Hadoop cluster>/nyctaxitripraw /DestKey:<storage account key> /S /Pattern:trip_data_*.csv

Esse comando carrega os dados de passagens de saudação muito***nyctaxifareraw*** diretório no contêiner de padrão de saudação do cluster de Hadoop hello.

        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:<path_to_unzipped_data_files> /Dest:https://<storage account name of Hadoop cluster>.blob.core.windows.net/<default container of Hadoop cluster>/nyctaxifareraw /DestKey:<storage account key> /S /Pattern:trip_fare_*.csv

dados de saudação devem agora no armazenamento de BLOBs do Azure e pronto toobe consumidas em cluster do HDInsight hello.

## <a name="#download-hql-files"></a>Faça logon no nó principal de saudação do cluster de Hadoop e e preparar para análise de dados exploratório
> [!NOTE]
> Essa normalmente é uma tarefa **Admin** .
> 
> 

nó principal do hello tooaccess de cluster Olá para análise de dados exploratório e para baixo de amostragem de dados hello, execute o procedimento de saudação descrito no [Olá acesso cabeçotes de nó de Cluster de Hadoop](machine-learning-data-science-customize-hadoop-cluster.md#headnode).

Este passo a passo, principalmente, usamos as consultas escritas [Hive](https://hive.apache.org/), uma linguagem de consulta do tipo SQL, tooperform explorações de dados preliminares. consultas de Hive Olá são armazenadas em arquivos de .hql. É, em seguida, para baixo de exemplo neste toobe dados usado dentro de aprendizado de máquina do Azure para criar modelos.

cluster de saudação tooprepare para análise de dados exploratório, podemos baixar os arquivos de .hql Olá que contêm scripts de Hive relevantes saudação do [github](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts) tooa diretório local (C:\temp) no nó principal hello. toodo isso, abra Olá **Prompt de comando** do hello nó principal do Olá Olá cluster e emitir os dois comandos a seguir:

    set script='https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/DataScienceProcess/DataScienceScripts/Download_DataScience_Scripts.ps1'

    @powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString(%script%))"

Esses dois comandos baixará todos os arquivos de .hql necessários neste diretório local do passo a passo toohello ***C:\temp &#92;*** no nó principal hello.

## <a name="#hive-db-tables"></a>Criar banco de dados e tabelas Hive particionadas por mês
> [!NOTE]
> Essa normalmente é uma tarefa **Admin** .
> 
> 

Estamos agora pronto toocreate Hive tabelas para nosso conjunto de dados NYC táxi.
No hello nó principal do cluster de Hadoop Olá abra Olá ***linha de comando do Hadoop*** na Olá a área de trabalho do nó principal hello e insira o diretório de Hive Olá digitando o comando Olá

    cd %hive_home%\bin

> [!NOTE]
> **Executar todos os comandos de Hive neste passo a passo de saudação acima Hive bin / prompt do diretório. Isso solucionará automaticamente quaisquer problemas de caminho. Usamos termos Olá "Hive diretório" prompt, "Hive bin / aviso diretório" e "linha de comando Hadoop" alternadamente neste passo a passo.**
> 
> 

Do prompt de diretório do Hive Olá, digite Olá comando no Hadoop linha de comando de tabelas e Olá nó principal toosubmit Olá Hive consulta toocreate Hive banco de dados a seguir:

    hive -f "C:\temp\sample_hive_create_db_and_tables.hql"

Aqui está o conteúdo de saudação do hello ***C:\temp\sample\_hive\_criar\_db\_e\_tables.hql*** arquivo que cria o banco de dados de Hive ***nyctaxidb *** e tabelas ***viagem*** e ***passagens***.

    create database if not exists nyctaxidb;

    create external table if not exists nyctaxidb.trip
    (
        medallion string,
        hack_license string,
        vendor_id string,
        rate_code string,
        store_and_fwd_flag string,
        pickup_datetime string,
        dropoff_datetime string,
        passenger_count int,
        trip_time_in_secs double,
        trip_distance double,
        pickup_longitude double,
        pickup_latitude double,
        dropoff_longitude double,
        dropoff_latitude double)  
    PARTITIONED BY (month int)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' lines terminated by '\n'
    STORED AS TEXTFILE LOCATION 'wasb:///nyctaxidbdata/trip' TBLPROPERTIES('skip.header.line.count'='1');

    create external table if not exists nyctaxidb.fare
    (
        medallion string,
        hack_license string,
        vendor_id string,
        pickup_datetime string,
        payment_type string,
        fare_amount double,
        surcharge double,
        mta_tax double,
        tip_amount double,
        tolls_amount double,
        total_amount double)
    PARTITIONED BY (month int)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' lines terminated by '\n'
    STORED AS TEXTFILE LOCATION 'wasb:///nyctaxidbdata/fare' TBLPROPERTIES('skip.header.line.count'='1');

Esse script do Hive cria duas tabelas:

* tabela de "viagem e" Hello contém detalhes de viagem de cada jornada (detalhes do driver, o tempo de retirada, distância de viagem e vezes)
* tabela de "passagens" Hello contém detalhes de passagens (valor de passagens, quantidade de ponta, pedágio e sobretaxas).

Se você precisa de qualquer assistência adicional com esses procedimentos ou tooinvestigate as alternativas, consulte a seção de saudação [consultas Hive enviar diretamente da linha de comando do Hadoop Olá ](machine-learning-data-science-move-hive-tables.md#submit).

## <a name="#load-data"></a>Carregar tabelas de dados de tooHive por partições
> [!NOTE]
> Essa normalmente é uma tarefa **Admin** .
> 
> 

Olá NYC táxi dataset tem um particionamento natural por mês, que usamos tooenable tempos mais rápidos de processamento e consulta. Olá comandos do PowerShell abaixo (emitidas do diretório de Hive hello usando Olá **linha de comando do Hadoop**) carregar dados toohello "viagem" e "passagens" Hive tabelas particionadas por mês.

    for /L %i IN (1,1,12) DO (hive -hiveconf MONTH=%i -f "C:\temp\sample_hive_load_data_by_partitions.hql")

Olá *exemplo\_hive\_carregar\_dados\_por\_partitions.hql* arquivo contém o seguinte Olá **carregar** comandos.

    LOAD DATA INPATH 'wasb:///nyctaxitripraw/trip_data_${hiveconf:MONTH}.csv' INTO TABLE nyctaxidb.trip PARTITION (month=${hiveconf:MONTH});
    LOAD DATA INPATH 'wasb:///nyctaxifareraw/trip_fare_${hiveconf:MONTH}.csv' INTO TABLE nyctaxidb.fare PARTITION (month=${hiveconf:MONTH});

Observe que um número de consultas de Hive que usamos aqui no processo de exploração Olá envolve a pesquisa em uma única partição ou em apenas algumas das partições. Mas essas consultas podem ser executadas em dados de inteiro de saudação.

### <a name="#show-db"></a>Mostrar os bancos de dados em Olá cluster HDInsight Hadoop
tooshow Olá bancos de dados criados no cluster HDInsight Hadoop dentro da janela de linha de comando do Hadoop hello, executar Olá na linha de comando do Hadoop de comando a seguir:

    hive -e "show databases;"

### <a name="#show-tables"></a>Mostrar tabelas de Hive Olá no banco de dados de nyctaxidb Olá
tooshow Olá tabelas Olá nyctaxidb banco de dados, executar Olá na linha de comando do Hadoop de comando a seguir:

    hive -e "show tables in nyctaxidb;"

Podemos afirmar que as tabelas de saudação são particionadas emitindo o comando de saudação abaixo:

    hive -e "show partitions nyctaxidb.trip;"

Olá esperado saída é mostrada abaixo:

    month=1
    month=10
    month=11
    month=12
    month=2
    month=3
    month=4
    month=5
    month=6
    month=7
    month=8
    month=9
    Time taken: 2.075 seconds, Fetched: 12 row(s)

Da mesma forma, podemos garantir que essa tabela de passagens Olá é particionada emitindo o comando de saudação abaixo:

    hive -e "show partitions nyctaxidb.fare;"

Olá esperado saída é mostrada abaixo:

    month=1
    month=10
    month=11
    month=12
    month=2
    month=3
    month=4
    month=5
    month=6
    month=7
    month=8
    month=9
    Time taken: 1.887 seconds, Fetched: 12 row(s)

## <a name="#explore-hive"></a>Exploração de dados e engenharia de recursos no Hive
> [!NOTE]
> Essa é normalmente é uma tarefa de **Cientista de Dados** .
> 
> 

Olá exploração de dados e tarefas de engenharia para Olá dados carregados em tabelas de Hive Olá podem ser realizados usando consultas de Hive de recursos. Aqui estão exemplos de tais tarefas que percorreremos ao longo desta seção:

* Exiba os principais 10 registros Olá em ambas as tabelas.
* Explorar as distribuições de dados de alguns campos em períodos diferentes.
* Investigue a qualidade dos dados dos campos de longitude e latitude hello.
* Gerar rótulos de classificação binária e multiclasse com base no hello **dica\_quantidade**.
* Gere recursos de computação distâncias de viagem direto de saudação.

### <a name="exploration-view-hello-top-10-records-in-table-trip"></a>Exploração: Exibição Olá top 10 registros em viagem de tabela
> [!NOTE]
> Essa é normalmente é uma tarefa de **Cientista de Dados** .
> 
> 

toosee a aparência dos dados hello, podemos examinar 10 registros de cada tabela. Execute Olá duas consultas a seguir separadamente de aviso de diretório de Hive Olá nos registros de Olá Olá linha de comando do Hadoop console tooinspect.

tooget Olá top 10 registros na tabela hello "viagem" da saudação primeiro mês:

    hive -e "select * from nyctaxidb.trip where month=1 limit 10;"

tooget Olá top 10 registros na tabela hello "passagens" da saudação primeiro mês:

    hive -e "select * from nyctaxidb.fare where month=1 limit 10;"

Ele geralmente é útil toosave Olá registros tooa arquivo exibindo conveniente. Toohello uma pequena alteração acima consulta realiza isso:

    hive -e "select * from nyctaxidb.fare where month=1 limit 10;" > C:\temp\testoutput

### <a name="exploration-view-hello-number-of-records-in-each-of-hello-12-partitions"></a>Exploração: Exibir hello número de registros em cada um dos 12 partições de saudação
> [!NOTE]
> Essa é normalmente é uma tarefa de **Cientista de Dados** .
> 
> 

De interesse é hello como número de saudação de viagens de varia durante o ano civil de saudação. Agrupar por mês nos permite toosee nesta distribuição de viagens de aparência.

    hive -e "select month, count(*) from nyctaxidb.trip group by month;"

Isso nos dá saída hello:

    1       14776615
    2       13990176
    3       15749228
    4       15100468
    5       15285049
    6       14385456
    7       13823840
    8       12597109
    9       14107693
    10      15004556
    11      14388451
    12      13971118
    Time taken: 283.406 seconds, Fetched: 12 row(s)

Aqui, Olá primeira coluna é mês hello e Olá segundo é o número de saudação de viagens de naquele mês.

Podemos também pode contar número total de saudação de registros no nosso conjunto de dados de viagem emitindo Olá comando no prompt de diretório de Hive Olá a seguir.

    hive -e "select count(*) from nyctaxidb.trip;"

Isso resulta em:

    173179759
    Time taken: 284.017 seconds, Fetched: 1 row(s)

Usando comandos toothose semelhante mostrado para o conjunto de dados de viagem hello, podemos emitir consultas de Hive Olá Hive diretório no prompt de saudação passagens conjunto de dados toovalidate Olá quantos registros.

    hive -e "select month, count(*) from nyctaxidb.fare group by month;"

Isso nos dá saída hello:

    1       14776615
    2       13990176
    3       15749228
    4       15100468
    5       15285049
    6       14385456
    7       13823840
    8       12597109
    9       14107693
    10      15004556
    11      14388451
    12      13971118
    Time taken: 253.955 seconds, Fetched: 12 row(s)

Observe que Olá exata mesmo número de viagens por mês é retornado para os dois conjuntos de dados. Isso fornece validação primeiro Olá que Olá dados foram carregados corretamente.

Contando Olá o número total de registros no conjunto de dados de passagens Olá pode ser feito usando o comando Olá abaixo no prompt de diretório de Hive hello:

    hive -e "select count(*) from nyctaxidb.fare;"

Isso resulta em:

    173179759
    Time taken: 186.683 seconds, Fetched: 1 row(s)

é o número total de saudação de registros em ambas as tabelas também Olá mesmo. Isso fornece uma validação segundo esse Olá dados foram carregados corretamente.

### <a name="exploration-trip-distribution-by-medallion"></a>Exploração: distribuição de corridas por licença
> [!NOTE]
> Essa é normalmente é uma tarefa de **Cientista de Dados** .
> 
> 

Este exemplo identifica medallion hello (números de táxi) com mais de 100 viagens dentro de um determinado período de tempo. benefícios de consulta de saudação do hello particionada acesso à tabela porque ela está condicionada pela variável de partição Olá **mês**. resultados da consulta Olá são escritos tooa arquivo local queryoutput.tsv em `C:\temp` no nó de cabeçalho hello.

    hive -f "C:\temp\sample_hive_trip_count_by_medallion.hql" > C:\temp\queryoutput.tsv

Aqui está o conteúdo de saudação do *exemplo\_hive\_viagem\_contagem\_por\_medallion.hql* arquivo para inspeção.

    SELECT medallion, COUNT(*) as med_count
    FROM nyctaxidb.fare
    WHERE month<=3
    GROUP BY medallion
    HAVING med_count > 100
    ORDER BY med_count desc;

medallion Olá Olá NYC táxi conjunto de dados identifica um arquivo. cab exclusivo. Podemos identificar quais táxis estão "ocupados" perguntando quais fizeram mais do que um determinado número de corridas em um determinado período de tempo. Olá, exemplo a seguir identifica cabs que fez com que mais de cem viagens Olá seja três primeiros meses e salva Olá consulta resultados tooa arquivo local C:\temp\queryoutput.tsv.

Aqui está o conteúdo de saudação do *exemplo\_hive\_viagem\_contagem\_por\_medallion.hql* arquivo para inspeção.

    SELECT medallion, COUNT(*) as med_count
    FROM nyctaxidb.fare
    WHERE month<=3
    GROUP BY medallion
    HAVING med_count > 100
    ORDER BY med_count desc;

De saudação Hive aviso de diretório, comando de saudação do problema abaixo:

    hive -f "C:\temp\sample_hive_trip_count_by_medallion.hql" > C:\temp\queryoutput.tsv

### <a name="exploration-trip-distribution-by-medallion-and-hacklicense"></a>Exploração: distribuição de corridas por medallion e hack_license
> [!NOTE]
> Essa é normalmente é uma tarefa de **Cientista de Dados** .
> 
> 

Ao explorar um conjunto de dados, com frequência, desejamos que número de saudação do tooexamine de co-ocorrências de grupos de valores. Esta seção fornece um exemplo de como toodo isso para cabs e drivers.

Olá *exemplo\_hive\_viagem\_contagem\_por\_medallion\_license.hql* arquivo agrupa os dados de passagens de saudação em "medallion" e "hack_license" e retorna contagens de cada combinação. Abaixo estão os conteúdos.

    SELECT medallion, hack_license, COUNT(*) as trip_count
    FROM nyctaxidb.fare
    WHERE month=1
    GROUP BY medallion, hack_license
    HAVING trip_count > 100
    ORDER BY trip_count desc;

Esta consulta retorna combinações de táxi e condutor específico por número decrescente de corridas.

De saudação Hive prompt de diretório, execute:

    hive -f "C:\temp\sample_hive_trip_count_by_medallion_license.hql" > C:\temp\queryoutput.tsv

resultados da consulta Olá são gravados tooa local arquivo C:\temp\queryoutput.tsv.

### <a name="exploration-assessing-data-quality-by-checking-for-invalid-longitudelatitude-records"></a>Exploração: avaliar a qualidade dos dados através da verificação de registros de latitude/longitude inválidos
> [!NOTE]
> Essa é normalmente é uma tarefa de **Cientista de Dados** .
> 
> 

Um objetivo comum de análise de dados exploratório é tooweed registros inválido ou incorreto. Olá exemplo nesta seção determina se hello campos de longitude ou latitude contenham um valor muito fora Olá área NYC. Como é provável que esses registros têm um valores de latitude de longitude incorretos, desejamos tooeliminate-los de qualquer dado que seja toobe usados na modelagem.

Aqui está o conteúdo de saudação do *exemplo\_hive\_qualidade\_assessment.hql* arquivo para inspeção.

        SELECT COUNT(*) FROM nyctaxidb.trip
        WHERE month=1
        AND  (CAST(pickup_longitude AS float) NOT BETWEEN -90 AND -30
        OR    CAST(pickup_latitude AS float) NOT BETWEEN 30 AND 90
        OR    CAST(dropoff_longitude AS float) NOT BETWEEN -90 AND -30
        OR    CAST(dropoff_latitude AS float) NOT BETWEEN 30 AND 90);


De saudação Hive prompt de diretório, execute:

    hive -S -f "C:\temp\sample_hive_quality_assessment.hql"

Olá *-S* argumento incluído nesse comando suprime a impressão de tela hello status dos trabalhos de Hive mapear/reduzir hello. Isso é útil porque facilita a impressão de tela de saudação do hello mais legível de saída de consulta de Hive.

### <a name="exploration-binary-class-distributions-of-trip-tips"></a>Exploração: distribuições de classe binária de gorjetas para corridas
> [!NOTE]
> Essa é normalmente é uma tarefa de **Cientista de Dados** .
> 
> 

Problema de classificação binária Olá descritas em hello [exemplos de tarefas de previsão](machine-learning-data-science-process-hive-walkthrough.md#mltasks) seção, é útil tooknow se uma dica foi fornecida ou não. Essa distribuição de gorjetas é binária:

* tip given(Class 1, tip\_amount > $0)  
* no tip (Class 0, tip\_amount = $0).

Olá *exemplo\_hive\_Oblíquo\_frequencies.hql* arquivo mostrado a seguir faz isso.

    SELECT tipped, COUNT(*) AS tip_freq
    FROM
    (
        SELECT if(tip_amount > 0, 1, 0) as tipped, tip_amount
        FROM nyctaxidb.fare
    )tc
    GROUP BY tipped;

De saudação Hive prompt de diretório, execute:

    hive -f "C:\temp\sample_hive_tipped_frequencies.hql"


### <a name="exploration-class-distributions-in-hello-multiclass-setting"></a>Exploração: Classe distribuições na configuração multiclasse Olá
> [!NOTE]
> Essa é normalmente é uma tarefa de **Cientista de Dados** .
> 
> 

Problema de classificação multiclasse Olá descritas Olá [exemplos de tarefas de previsão](machine-learning-data-science-process-hive-walkthrough.md#mltasks) seção esse conjunto de dados também se presta tooa classificação natural onde gostaria toopredict quantidade de Olá Olá dicas fornecido. Podemos usar compartimentos toodefine dica intervalos na consulta de saudação. tooget vários intervalos de dica de distribuições de classe para Olá Olá, usamos Olá *exemplo\_hive\_dica\_intervalo\_frequencies.hql* arquivo. Abaixo estão os conteúdos.

    SELECT tip_class, COUNT(*) AS tip_freq
    FROM
    (
        SELECT if(tip_amount=0, 0,
            if(tip_amount>0 and tip_amount<=5, 1,
            if(tip_amount>5 and tip_amount<=10, 2,
            if(tip_amount>10 and tip_amount<=20, 3, 4)))) as tip_class, tip_amount
        FROM nyctaxidb.fare
    )tc
    GROUP BY tip_class;

Execute Olá comando a seguir no console de linha de comando do Hadoop:

    hive -f "C:\temp\sample_hive_tip_range_frequencies.hql"

### <a name="exploration-compute-direct-distance-between-two-longitude-latitude-locations"></a>Exploração: calcular a distância direta entre dois locais de latitude-longitude
> [!NOTE]
> Essa é normalmente é uma tarefa de **Cientista de Dados** .
> 
> 

Uma medida de distância direta Olá permite-nos toofind out discrepância Olá entre ele e hello real trip distância. Podemos motivar esse recurso destacando um passageiro talvez seja menor provável dica de ferramenta se eles descobrir driver Olá intencionalmente obteve-los por uma rota muito mais longa.

comparação de saudação toosee entre a distância de viagem real e hello [distância do Haverseno](http://en.wikipedia.org/wiki/Haversine_formula) entre dois pontos de longitude latitude (distância do "círculo ótimo" hello), usamos Olá trigonométricas funções disponíveis no Hive, assim:

    set R=3959;
    set pi=radians(180);

    insert overwrite directory 'wasb:///queryoutputdir'

    select pickup_longitude, pickup_latitude, dropoff_longitude, dropoff_latitude, trip_distance, trip_time_in_secs,
    ${hiveconf:R}*2*2*atan((1-sqrt(1-pow(sin((dropoff_latitude-pickup_latitude)
     *${hiveconf:pi}/180/2),2)-cos(pickup_latitude*${hiveconf:pi}/180)
     *cos(dropoff_latitude*${hiveconf:pi}/180)*pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2)))
     /sqrt(pow(sin((dropoff_latitude-pickup_latitude)*${hiveconf:pi}/180/2),2)
     +cos(pickup_latitude*${hiveconf:pi}/180)*cos(dropoff_latitude*${hiveconf:pi}/180)*
     pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2))) as direct_distance
    from nyctaxidb.trip
    where month=1
    and pickup_longitude between -90 and -30
    and pickup_latitude between 30 and 90
    and dropoff_longitude between -90 and -30
    and dropoff_latitude between 30 and 90;

Na consulta Olá acima, R é o raio Olá Olá terra em milhas e pi é tooradians convertido. Observe que os pontos de longitude latitude Olá são "filtrados" tooremove valores que estão distantes de área de NYC hello.

Nesse caso, escrevemos nosso diretório tooa de resultados chamado "queryoutputdir". sequência de saudação de comandos mostrados abaixo primeiro cria esse diretório de saída e, em seguida, executa o comando de Hive hello.

De saudação Hive prompt de diretório, execute:

    hdfs dfs -mkdir wasb:///queryoutputdir

    hive -f "C:\temp\sample_hive_trip_direct_distance.hql"


Olá resultados da consulta são gravados blobs do Azure de too9 ***queryoutputdir/000000\_0*** muito ***queryoutputdir/000008\_0*** no contêiner de padrão de saudação do cluster de Hadoop hello.

tamanho de saudação toosee de blobs individuais hello, executamos Olá comando a seguir no prompt de diretório de Hive hello:

    hdfs dfs -ls wasb:///queryoutputdir

conteúdo de saudação toosee de um determinado arquivo, digamos que 000000\_0, usamos do Hadoop `copyToLocal` comando assim.

    hdfs dfs -copyToLocal wasb:///queryoutputdir/000000_0 C:\temp\tempfile

> [!WARNING]
> O `copyToLocal` pode ser muito lento para arquivos grandes e não é recomendado para uso com eles.  
> 
> 

Uma vantagem importante da ter esses dados residem em um blob do Azure é que podemos pode explorar dados de saudação dentro de aprendizado de máquina do Azure usando Olá [importar dados] [ import-data] módulo.

## 
            <a name="#downsample">
            </a>Para reduzir dados e criar modelos no Azure Machine Learning
> [!NOTE]
> Essa é normalmente é uma tarefa de **Cientista de Dados** .
> 
> 

Após a fase de análise de dados exploratório hello, estamos agora dados de saudação de exemplo toodown pronto para criar modelos no aprendizado de máquina do Azure. Nesta seção, mostramos como toouse um Hive consultar dados de saudação do exemplo toodown, que são acessados de saudação [importar dados] [ import-data] módulo no aprendizado de máquina do Azure.

### <a name="down-sampling-hello-data"></a>Para baixo Olá dados de amostra
Há duas etapas neste procedimento. Primeiro, associe Olá **nyctaxidb.trip** e **nyctaxidb.fare** tabelas em três chaves que estão presentes em todos os registros: "medallion", "hack\_licença", e "retirada\_datetime". Então geramos um rótulo de classificação binária **tipped** e um rótulo de classificação multiclasse **tip\_class**.

toobe toouse capaz de saudação dados amostrados diretamente da saudação [importar dados] [ import-data] módulo no aprendizado de máquina do Azure, é necessário toostore resultados Olá Olá acima da tabela de Hive consulta tooan interna. Em que os itens a seguir, criamos uma tabela interna de Hive e preencher seu conteúdo com hello unidas e dados de amostra.

Olá, consulta aplica funções de Hive padrão diretamente toogenerate hora de saudação do dia, semana do ano, dia da semana (1 significa segunda-feira e 7 significa para domingo) do hello "retirada\_datetime" campo e a distância direta Olá entre retirada hello e redução locais. Os usuários podem consultar muito[LanguageManual UDF](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF) para obter uma lista dessas funções.

Olá consulta e para baixo dados saudação de exemplos para que os resultados da consulta Olá comportada Olá estúdio de aprendizado de máquina do Azure. Somente cerca de 1% do conjunto de dados original Olá é importado para Olá Studio.

Abaixo estão os conteúdos de saudação do *exemplo\_hive\_preparar\_para\_aml\_full.hql* arquivo que prepara os dados para o modelo de criação no aprendizado de máquina do Azure.

        set R = 3959;
        set pi=radians(180);

        create table if not exists nyctaxidb.nyctaxi_downsampled_dataset (

        medallion string,
        hack_license string,
        vendor_id string,
        rate_code string,
        store_and_fwd_flag string,
        pickup_datetime string,
        dropoff_datetime string,
        pickup_hour string,
        pickup_week string,
        weekday string,
        passenger_count int,
        trip_time_in_secs double,
        trip_distance double,
        pickup_longitude double,
        pickup_latitude double,
        dropoff_longitude double,
        dropoff_latitude double,
        direct_distance double,
        payment_type string,
        fare_amount double,
        surcharge double,
        mta_tax double,
        tip_amount double,
        tolls_amount double,
        total_amount double,
        tipped string,
        tip_class string
        )
        row format delimited fields terminated by ','
        lines terminated by '\n'
        stored as textfile;

        --- now insert contents of hello join into hello above internal table

        insert overwrite table nyctaxidb.nyctaxi_downsampled_dataset
        select
        t.medallion,
        t.hack_license,
        t.vendor_id,
        t.rate_code,
        t.store_and_fwd_flag,
        t.pickup_datetime,
        t.dropoff_datetime,
        hour(t.pickup_datetime) as pickup_hour,
        weekofyear(t.pickup_datetime) as pickup_week,
        from_unixtime(unix_timestamp(t.pickup_datetime, 'yyyy-MM-dd HH:mm:ss'),'u') as weekday,
        t.passenger_count,
        t.trip_time_in_secs,
        t.trip_distance,
        t.pickup_longitude,
        t.pickup_latitude,
        t.dropoff_longitude,
        t.dropoff_latitude,
        t.direct_distance,
        f.payment_type,
        f.fare_amount,
        f.surcharge,
        f.mta_tax,
        f.tip_amount,
        f.tolls_amount,
        f.total_amount,
        if(tip_amount>0,1,0) as tipped,
        if(tip_amount=0,0,
        if(tip_amount>0 and tip_amount<=5,1,
        if(tip_amount>5 and tip_amount<=10,2,
        if(tip_amount>10 and tip_amount<=20,3,4)))) as tip_class

        from
        (
        select
        medallion,
        hack_license,
        vendor_id,
        rate_code,
        store_and_fwd_flag,
        pickup_datetime,
        dropoff_datetime,
        passenger_count,
        trip_time_in_secs,
        trip_distance,
        pickup_longitude,
        pickup_latitude,
        dropoff_longitude,
        dropoff_latitude,
        ${hiveconf:R}*2*2*atan((1-sqrt(1-pow(sin((dropoff_latitude-pickup_latitude)
        *${hiveconf:pi}/180/2),2)-cos(pickup_latitude*${hiveconf:pi}/180)
        *cos(dropoff_latitude*${hiveconf:pi}/180)*pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2)))
        /sqrt(pow(sin((dropoff_latitude-pickup_latitude)*${hiveconf:pi}/180/2),2)
        +cos(pickup_latitude*${hiveconf:pi}/180)*cos(dropoff_latitude*${hiveconf:pi}/180)*pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2))) as direct_distance,
        rand() as sample_key

        from nyctaxidb.trip
        where pickup_latitude between 30 and 90
            and pickup_longitude between -90 and -30
            and dropoff_latitude between 30 and 90
            and dropoff_longitude between -90 and -30
        )t
        join
        (
        select
        medallion,
        hack_license,
        vendor_id,
        pickup_datetime,
        payment_type,
        fare_amount,
        surcharge,
        mta_tax,
        tip_amount,
        tolls_amount,
        total_amount
        from nyctaxidb.fare
        )f
        on t.medallion=f.medallion and t.hack_license=f.hack_license and t.pickup_datetime=f.pickup_datetime
        where t.sample_key<=0.01

solicitar que essa consulta, do diretório de Hive Olá toorun:

    hive -f "C:\temp\sample_hive_prepare_for_aml_full.hql"

Agora temos uma tabela interna "nyctaxidb.nyctaxi_downsampled_dataset", que podem ser acessados usando Olá [importar dados] [ import-data] módulo de aprendizado de máquina do Azure. Além disso, podemos usar esse conjunto de dados para criar modelos de Machine Learning.  

### <a name="use-hello-import-data-module-in-azure-machine-learning-tooaccess-hello-down-sampled-data"></a>Usar o módulo de importação de dados de Olá de saudação do aprendizado de máquina do Azure tooaccess dados de amostra
Como pré-requisitos para emitir consultas de Hive no hello [importar dados] [ import-data] módulo de aprendizado de máquina do Azure, é necessário acessar o espaço de trabalho de aprendizado de máquina do Azure tooan e credenciais de toohello de saudação de acesso cluster e sua conta de armazenamento associada.

Alguns detalhes Olá [importar dados] [ import-data] tooinput de parâmetros do módulo e hello:

**URI do servidor HCatalog**: se o nome de cluster Olá for abc123, isso é simplesmente: https://abc123.azurehdinsight.net

**Nome de conta de usuário do Hadoop** : nome de usuário Olá escolhido para o cluster de saudação (**não** nome de usuário de acesso remoto Olá)

**Senha da conta do usuário Hadoop** : senha Olá escolhida para o cluster de saudação (**não** senha de acesso remoto Olá)

**Local dos dados de saída** : isso é escolhido toobe do Azure.

**Nome da conta de armazenamento do Azure** : nome saudação padrão da conta de armazenamento associada Olá cluster.

**Nome do contêiner do Azure** : isso é nome do contêiner padrão Olá para cluster hello e normalmente é Olá mesmo como o nome do cluster hello. Para um cluster chamado "abc123", é simplesmente abc123.

> [!IMPORTANT]
> **Qualquer tabela que desejamos tooquery usando Olá [importar dados] [ import-data] módulo no aprendizado de máquina do Azure deve ser uma tabela interna.** Uma dica para determinar se uma tabela T em um banco de dados D.db é uma tabela interna é a seguinte:
> 
> 

De saudação Hive aviso de diretório, o comando de saudação do problema:

    hdfs dfs -ls wasb:///D.db/T

Se a tabela de saudação é uma tabela interna e ele é preenchido, seu conteúdo deve ser exibidos aqui. Outro toodetermine de forma que se uma tabela é uma tabela interna é toouse hello Azure Storage Explorer. Usá-lo toonavigate toohello nome do contêiner padrão do cluster hello e, em seguida, filtrar pelo nome da tabela de saudação. Se a tabela hello e seu conteúdo aparecer, isso confirma que é uma tabela interna.

Aqui está um instantâneo da consulta de Hive hello e Olá [importar dados] [ import-data] módulo:

![Consulta de hive para o módulo Importar Dados](./media/machine-learning-data-science-process-hive-walkthrough/1eTYf52.png)

Observe que, desde o nosso down dados amostrados residem no contêiner de padrão de Olá, consulta de Hive resultante saudação do aprendizado de máquina do Azure é muito simple e é apenas uma "Selecione * de nyctaxidb.nyctaxi\_reduzida\_dados".

saudação de conjunto de dados agora pode ser usado como Olá ponto de partida para criar modelos de aprendizado de máquina.

### 
            <a name="mlmodel">
            </a>Compilar modelos no Azure Machine Learning
Estamos agora capaz de tooproceed toomodel criação e implantação de modelo no [aprendizado de máquina do Azure](https://studio.azureml.net). dados de saudação estão prontos para que possamos toouse resolver problemas de previsão Olá identificados acima:

**1. Classificação binária**: toopredict ou não uma dica foi pago uma viagem.

**Aprendiz usado:** regressão logística de classe dois

a. Para esse problema, nosso rótulo (ou classe) de destino é "tipped". Nosso conjunto de dados original convertidos tem algumas colunas que são vazamentos de destino para esse teste de classificação. Em particular: dica\_da classe, a dica\_quantidade e total\_valor revelam informações sobre o rótulo de destino de saudação que não está disponível no tempo de teste. Remover essas colunas consideração usando Olá [selecionar colunas no conjunto de dados] [ select-columns] módulo.

instantâneo de saudação abaixo mostra toopredict nossa experiência ou não uma dica foi paga para uma determinado viagem.

![Instantâneo de teste](./media/machine-learning-data-science-process-hive-walkthrough/QGxRz5A.png)

b. Para esse teste, nossas distribuições de rótulo de destino foram de aproximadamente 1:1.

instantâneo de saudação abaixo mostra a distribuição de saudação de rótulos de classe de dica de problema de classificação binária hello.

![Distribuição de rótulos de classe de dica](./media/machine-learning-data-science-process-hive-walkthrough/9mM4jlD.png)

Como resultado, obtemos um AUC de 0.987, conforme mostrado na figura abaixo a saudação.

![Valor AUC](./media/machine-learning-data-science-process-hive-walkthrough/8JDT0F8.png)

**2. Classificação multiclasse**: classes definidas por intervalo de saudação toopredict de quantidades de dica pagado para viagem hello, usando Olá anteriormente.

**Aprendiz usado:** regressão logística de várias classes

a. Para esse problema, nosso rótulo de destino (ou classe) é "tip\_class", que pode ter um dos cinco valores (0,1,2,3,4). Como no caso de classificação binária hello, temos algumas colunas são vazamentos de destino para esse teste. Em particular: Oblíquo, Dica\_quantidade, total\_valor revelam informações sobre o rótulo de destino de saudação que não está disponível no tempo de teste. Removemos essas colunas usando Olá [selecionar colunas no conjunto de dados] [ select-columns] módulo.

Olá instantâneo abaixo mostra nosso toopredict de teste no qual bin uma dica é provavelmente toofall (classe 0: dica = $0, a classe 1: Dica > $0 e a dica < = US $5, classe 2: Dica > US $5 e a dica < = US $10, 3 da classe: Dica > $10 e a dica < = US $20 Classe 4: Dica > US $20)

![Instantâneo de teste](./media/machine-learning-data-science-process-hive-walkthrough/5ztv0n0.png)

Agora mostraremos a aparência de nossa distribuição de classe de teste real. Podemos ver que enquanto classe 0 e 1 de classe são predominantes, hello outras classes são raros.

![Distribuição de classe de teste](./media/machine-learning-data-science-process-hive-walkthrough/Vy1FUKa.png)

b. Para esse teste, usamos um toolook de matriz de confusão em nosso precisões de previsão. Isso é mostrado abaixo.

![Matriz de confusão](./media/machine-learning-data-science-process-hive-walkthrough/cxFmErM.png)

Observe que enquanto precisões nossa classe em classes predominantes Olá é muito bom, modelo Olá não faz um bom trabalho de "aprendizagem" em classes mais raras hello.

**3. Tarefa de regressão**: o valor de saudação toopredict de dica pago para uma viagem.

**Aprendiz usado:** árvore de decisão aprimorada

a. Para esse problema, nosso rótulo (ou classe) de destino é "tip\_amount". Nesse caso, nossos vazamentos de destino são:-Oblíquo, Dica\_classe total\_quantidade; todas essas variáveis revelam informações sobre a quantidade de dica de saudação que normalmente não está disponível no tempo de teste. Removemos essas colunas usando Olá [selecionar colunas no conjunto de dados] [ select-columns] módulo.

Olá instantâneo belows mostra nossa experiência toopredict Olá Olá fornecido dica.

![Instantâneo de teste](./media/machine-learning-data-science-process-hive-walkthrough/11TZWgV.png)

b. Para problemas de regressão, medimos precisões Olá de nossa previsão observando o erro Olá quadrado em previsões hello, Olá coeficiente de determinação e, Olá como. Vamos mostrar isso abaixo.

![Estatísticas de previsão](./media/machine-learning-data-science-process-hive-walkthrough/Jat9mrz.png)

Podemos ver que sobre Olá coeficiente de determinação é 0.709, implicando sobre 71% de variação de saudação é explicado pelo nosso coeficientes de modelo.

> [!IMPORTANT]
> toolearn mais sobre o aprendizado de máquina do Azure e como tooaccess e usá-lo, consulte muito[o que é o aprendizado de máquina?](machine-learning-what-is-machine-learning.md). Um recurso muito útil para a execução de um conjunto de experiências de aprendizado de máquina no aprendizado de máquina do Azure é hello [Cortana Intelligence galeria](https://gallery.cortanaintelligence.com/). Olá Galeria abrange uma gama de experiências e fornece uma introdução detalhada no intervalo de saudação de recursos de aprendizado de máquina do Azure.
> 
> 

## <a name="license-information"></a>Informações de Licença
Este passo a passo do exemplo e seus scripts de acompanhamento são compartilhados pela Microsoft sob a licença do MIT hello. Verifique o arquivo de LICENSE.txt de saudação no diretório de saudação do código de exemplo hello no GitHub para obter mais detalhes.

## <a name="references"></a>Referências
•   [Página de download de Viagens de Táxi de NYC, de Andrés Monroy](http://www.andresmh.com/nyctaxitrips/)  
•   [Dados de Viagem de Táxi de FOILing NYC, de Chris Whong](http://chriswhong.com/open-data/foil_nyc_taxi/)   
•   [Pesquisa e estatísticas de comissionamento de táxis e limusines de NYC](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)

[2]: ./media/machine-learning-data-science-process-hive-walkthrough/output-hive-results-3.png
[11]: ./media/machine-learning-data-science-process-hive-walkthrough/hive-reader-properties.png
[12]: ./media/machine-learning-data-science-process-hive-walkthrough/binary-classification-training.png
[13]: ./media/machine-learning-data-science-process-hive-walkthrough/create-scoring-experiment.png
[14]: ./media/machine-learning-data-science-process-hive-walkthrough/binary-classification-scoring.png
[15]: ./media/machine-learning-data-science-process-hive-walkthrough/amlreader.png

<!-- Module References -->
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
