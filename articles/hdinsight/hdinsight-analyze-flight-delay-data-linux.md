---
title: dados de atraso de voo aaaAnalyze com Hive no HDInsight - Azure | Microsoft Docs
description: "Saiba como toouse Hive dados de voo tooanalyze no HDInsight baseados em Linux, em seguida, exportar Olá dados tooSQL usando Sqoop de banco de dados."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 0c23a079-981a-4079-b3f7-ad147b4609e5
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 7830457a7100880dff1c647dde1b4d203bfea3c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-flight-delay-data-by-using-hive-on-linux-based-hdinsight"></a>Analisar dados de atraso de voo usando o Hive no HDInsight baseado em Linux

Saiba como dados de atraso de voo tooanalyze usando Hive no HDInsight baseados em Linux, em seguida, exportar Olá dados tooAzure banco de dados SQL usando Sqoop.

> [!IMPORTANT]
> etapas de saudação neste documento exigem um cluster HDInsight que usa o Linux. Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior. Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

### <a name="prerequisites"></a>Pré-requisitos

* **Um cluster HDInsight**. Confira [Introdução ao uso do Hadoop com o Hive no HDInsight em Linux](hdinsight-hadoop-linux-tutorial-get-started.md) para obter as etapas da criação de um novo cluster HDInsight baseado em Linux.

* **Banco de dados SQL do Azure**. Você usa um banco de dados SQL do Azure como um repositório de dados de destino. Se você ainda não tem um Banco de Dados SQL, confira [Tutorial do Banco de Dados SQL: Criar um banco de dados SQL em minutos](../sql-database/sql-database-get-started.md).

* **CLI do Azure**. Se você não tiver instalado o hello CLI do Azure, consulte [instalar e configurar Olá CLI do Azure](../cli-install-nodejs.md) para mais etapas.

## <a name="download-hello-flight-data"></a>Baixar dados de voo Olá

1. Procurar muito[pesquisa e administração de tecnologia inovadora, agência de transporte estatísticas][rita-website].

2. Na página de saudação, selecione Olá valores a seguir:

   | Nome | Valor |
   | --- | --- |
   | Filtrar por ano |2013 |
   | Filtrar por período |Janeiro |
   | Campos |Year, FlightDate, UniqueCarrier, Carrier, FlightNum, OriginAirportID, Origin, OriginCityName, OriginState, DestAirportID, Dest, DestCityName, DestState, DepDelayMinutes, ArrDelay, ArrDelayMinutes, CarrierDelay, WeatherDelay, NASDelay, SecurityDelay, LateAircraftDelay. Limpar todos os outros campos |

3. Clique em **Download**.

## <a name="upload-hello-data"></a>Carregar dados de saudação

1. Use Olá comando tooupload Olá zip arquivo toohello HDInsight nó principal do cluster a seguir:

    ```
    scp FILENAME.zip USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:
    ```

    Substituir **FILENAME** com nome de saudação do arquivo zip de saudação. Substituir **nome de usuário** com logon SSH Olá para o cluster do HDInsight hello. Substitua CLUSTERNAME com nome de saudação do cluster do HDInsight hello.

   > [!NOTE]
   > Se você usar uma senha tooauthenticate seu logon SSH, você será solicitado senha hello. Se você usou uma chave pública, talvez seja necessário Olá toouse `-i` parâmetro e especifique Olá caminho toohello correspondência de chave privada. Por exemplo: `scp -i ~/.ssh/id_rsa FILENAME.zip USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:`.

2. Depois de concluído o carregamento de saudação, conecte-se toohello cluster usando o SSH:

    ```ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net```

    Para obter mais informações, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

3. Uma vez conectado, use Olá seguir toounzip hello. ZIP arquivo:

    ```
    unzip FILENAME.zip
    ```

    Este comando extrai um arquivo .csv com aproximadamente 60 MB.

4. Use Olá após o comando toocreate um diretório no armazenamento de HDInsight e copie toohello diretório do arquivo de saudação:

    ```
    hdfs dfs -mkdir -p /tutorials/flightdelays/data
    hdfs dfs -put FILENAME.csv /tutorials/flightdelays/data/
    ```

## <a name="create-and-run-hello-hiveql"></a>Criar e executar Olá HiveQL

Use Olá as etapas a seguir tooimport dados de arquivo CSV de saudação em uma tabela de Hive nomeada **atrasos**.

1. A seguir use Olá toocreate de comando e editar um novo arquivo denominado **flightdelays.hql**:

    ```
    nano flightdelays.hql
    ```

    Use Olá depois do texto como o conteúdo deste arquivo hello:

    ```hiveql
    DROP TABLE delays_raw;
    -- Creates an external table over hello csv file
    CREATE EXTERNAL TABLE delays_raw (
        YEAR string,
        FL_DATE string,
        UNIQUE_CARRIER string,
        CARRIER string,
        FL_NUM string,
        ORIGIN_AIRPORT_ID string,
        ORIGIN string,
        ORIGIN_CITY_NAME string,
        ORIGIN_CITY_NAME_TEMP string,
        ORIGIN_STATE_ABR string,
        DEST_AIRPORT_ID string,
        DEST string,
        DEST_CITY_NAME string,
        DEST_CITY_NAME_TEMP string,
        DEST_STATE_ABR string,
        DEP_DELAY_NEW float,
        ARR_DELAY_NEW float,
        CARRIER_DELAY float,
        WEATHER_DELAY float,
        NAS_DELAY float,
        SECURITY_DELAY float,
        LATE_AIRCRAFT_DELAY float)
    -- hello following lines describe hello format and location of hello file
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ','
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE
    LOCATION '/tutorials/flightdelays/data';

    -- Drop hello delays table if it exists
    DROP TABLE delays;
    -- Create hello delays table and populate it with data
    -- pulled in from hello CSV file (via hello external table defined previously)
    CREATE TABLE delays AS
    SELECT YEAR AS year,
        FL_DATE AS flight_date,
        substring(UNIQUE_CARRIER, 2, length(UNIQUE_CARRIER) -1) AS unique_carrier,
        substring(CARRIER, 2, length(CARRIER) -1) AS carrier,
        substring(FL_NUM, 2, length(FL_NUM) -1) AS flight_num,
        ORIGIN_AIRPORT_ID AS origin_airport_id,
        substring(ORIGIN, 2, length(ORIGIN) -1) AS origin_airport_code,
        substring(ORIGIN_CITY_NAME, 2) AS origin_city_name,
        substring(ORIGIN_STATE_ABR, 2, length(ORIGIN_STATE_ABR) -1)  AS origin_state_abr,
        DEST_AIRPORT_ID AS dest_airport_id,
        substring(DEST, 2, length(DEST) -1) AS dest_airport_code,
        substring(DEST_CITY_NAME,2) AS dest_city_name,
        substring(DEST_STATE_ABR, 2, length(DEST_STATE_ABR) -1) AS dest_state_abr,
        DEP_DELAY_NEW AS dep_delay_new,
        ARR_DELAY_NEW AS arr_delay_new,
        CARRIER_DELAY AS carrier_delay,
        WEATHER_DELAY AS weather_delay,
        NAS_DELAY AS nas_delay,
        SECURITY_DELAY AS security_delay,
        LATE_AIRCRAFT_DELAY AS late_aircraft_delay
    FROM delays_raw;
    ```

2. arquivo de saudação toosave, use **Ctrl + X**, em seguida, **Y** .

3. toostart Hive e execução Olá **flightdelays.hql** de arquivos, use Olá comando a seguir:

    ```
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http' -f flightdelays.hql
    ```

   > [!NOTE]
   > Neste exemplo, `localhost` é usado, pois você está conectado toohello o nó principal do cluster do HDInsight hello, que é onde HiveServer2 está em execução.

4. Uma vez Olá __flightdelays.hql__ termina em execução, tooopen uma sessão interativa do Beeline comando a seguir de saudação do uso de script:

    ```
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http'
    ```

5. Quando você receber Olá `jdbc:hive2://localhost:10001/>` prompt, use Olá seguir tooretrieve os dados da consulta de dados de atraso de voo Olá importado.

    ```hiveql
    INSERT OVERWRITE DIRECTORY '/tutorials/flightdelays/output'
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    SELECT regexp_replace(origin_city_name, '''', ''),
        avg(weather_delay)
    FROM delays
    WHERE weather_delay IS NOT NULL
    GROUP BY origin_city_name;
    ```

    Essa consulta recupera uma lista de cidades que atrasos de clima experiente, juntamente com a média de saudação de tempo de espera e salvá-lo muito`/tutorials/flightdelays/output`. Posteriormente, Sqoop lê dados saudação deste local e exportá-lo tooAzure banco de dados SQL.

6. tooexit Beeline, insira `!quit` no prompt de saudação.

## <a name="create-a-sql-database"></a>Criar um banco de dados SQL

Se você já tiver um banco de dados SQL, você deve obter o nome do servidor de saudação. Você pode encontrar o nome do servidor de saudação em Olá [portal do Azure](https://portal.azure.com) selecionando **bancos de dados SQL**, e, em seguida, filtrando em nome de saudação do hello banco de dados você deseja toouse. nome do servidor de saudação é listado em Olá **SERVER** coluna.

Se você ainda não tiver um banco de dados SQL, use as informações de saudação em [tutorial do banco de dados SQL: criar um banco de dados SQL em minutos](../sql-database/sql-database-get-started.md) toocreate um. Salve o nome do servidor de saudação usado para o banco de dados de saudação.

## <a name="create-a-sql-database-table"></a>Criar uma tabela do Banco de Dados SQL

> [!NOTE]
> Há tooSQL tooconnect de muitas maneiras banco de dados e criar uma tabela. Olá use as etapas a seguir [FreeTDS](http://www.freetds.org/) do cluster do HDInsight hello.


1. Use SSH tooconnect toohello HDInsight baseados em Linux cluster e execução Olá seguindo as etapas da sessão SSH hello.

2. Use Olá comando tooinstall FreeTDS a seguir:

    ```
    sudo apt-get --assume-yes install freetds-dev freetds-bin
    ```

3. Depois de concluir a instalação do hello, use Olá após o servidor de banco de dados SQL do comando tooconnect toohello. Substituir **serverName** com o nome do servidor de banco de dados SQL hello. Substituir **adminLogin** e **adminPassword** com logon Olá para o banco de dados SQL. Substituir **databaseName** com o nome do banco de dados de saudação.

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D <databaseName>
    ```

    Você receberá a saída toohello semelhante texto a seguir:

    ```
    locale is "en_US.UTF-8"
    locale charset is "UTF-8"
    using default charset "UTF-8"
    Default database being set toosqooptest
    1>
    ```

4. Em Olá `1>` prompt, digite Olá linhas seguintes:

    ```
    CREATE TABLE [dbo].[delays](
    [origin_city_name] [nvarchar](50) NOT NULL,
    [weather_delay] float,
    CONSTRAINT [PK_delays] PRIMARY KEY CLUSTERED   
    ([origin_city_name] ASC))
    GO
    ```

    Olá quando `GO` instrução for inserida, instruções de saudação anterior são avaliadas. Essa consulta cria uma tabela chamada **atrasos**, com um índice clusterizado.

    Saudação de uso tooverify de consulta que Olá a tabela a seguir foi criada:

    ```
    SELECT * FROM information_schema.tables
    GO
    ```

    saudação de saída é similar toohello texto a seguir:

    ```
    TABLE_CATALOG   TABLE_SCHEMA    TABLE_NAME      TABLE_TYPE
    databaseName       dbo     delays      BASE TABLE
    ```

5. Digite `exit` em Olá `1>` tooexit Olá tsql utilitário do prompt.

## <a name="export-data-with-sqoop"></a>Exportar dados com o Sqoop

1. Use Olá tooverify de comando que Sqoop pode ver o banco de dados SQL a seguir:

    ```
    sqoop list-databases --connect jdbc:sqlserver://<serverName>.database.windows.net:1433 --username <adminLogin> --password <adminPassword>
    ```

    Esse comando retorna uma lista de bancos de dados, incluindo Olá banco de dados que você criou a tabela atrasos Olá anteriormente.

2. Use Olá dados tooexport de comando a seguir da tabela de mobiledata toohello hivesampletable:

    ```
    sqoop export --connect 'jdbc:sqlserver://<serverName>.database.windows.net:1433;database=<databaseName>' --username <adminLogin> --password <adminPassword> --table 'delays' --export-dir '/tutorials/flightdelays/output' --fields-terminated-by '\t' -m 1
    ```

    Sqoop conecta toohello banco de dados que contém a tabela de atrasos de saudação e exporta dados de saudação `/tutorials/flightdelays/output` tabela de atrasos de toohello do diretório.

3. Após a conclusão do comando hello, use Olá tooconnect toohello banco de dados usando TSQL a seguir:

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D <databaseName>
    ```

    Uma vez conectado, use Olá instruções tooverify dados saudação foram exportado toohello mobiledata tabela a seguir:

    ```
    SELECT * FROM delays
    GO
    ```

    Você deve ver uma lista dos dados na tabela de saudação. Tipo `exit` utilitário do tooexit Olá tsql.

## <a id="nextsteps"></a> Próximas etapas

toolearn mais toowork maneiras com dados no HDInsight, consulte Olá seguintes documentos:

* [Usar o Hive com o HDInsight][hdinsight-use-hive]
* [Usar o Oozie com o HDInsight][hdinsight-use-oozie]
* [Use o Sqoop com o HDInsight][hdinsight-use-sqoop]
* [Usar o Pig com o HDInsight][hdinsight-use-pig]
* [Desenvolver programas Java MapReduce para HDInsight][hdinsight-develop-mapreduce]
* [Desenvolver programas de streaming do Hadoop em Python para o HDInsight][hdinsight-develop-streaming]

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/


[rita-website]: http://www.transtats.bts.gov/DL_SelectFields.asp?Table_ID=236&DB_Short_Name=On-Time
[cindygross-hive-tables]: http://blogs.msdn.com/b/cindygross/archive/2013/02/06/hdinsight-hive-internal-and-external-tables-intro.aspx

[hdinsight-use-oozie]: hdinsight-use-oozie-linux-mac.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-use-sqoop]: hdinsight-use-sqoop-mac-linux.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-develop-streaming]: hdinsight-hadoop-streaming-python.md
[hdinsight-develop-mapreduce]: hdinsight-develop-deploy-java-mapreduce-linux.md

[hadoop-hiveql]: https://cwiki.apache.org/confluence/display/Hive/LanguageManual+DDL

[technetwiki-hive-error]: http://social.technet.microsoft.com/wiki/contents/articles/23047.hdinsight-hive-error-unable-to-rename.aspx
