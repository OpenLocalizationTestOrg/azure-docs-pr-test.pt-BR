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
# <a name="analyze-flight-delay-data-by-using-hive-on-linux-based-hdinsight"></a><span data-ttu-id="53a30-103">Analisar dados de atraso de voo usando o Hive no HDInsight baseado em Linux</span><span class="sxs-lookup"><span data-stu-id="53a30-103">Analyze flight delay data by using Hive on Linux-based HDInsight</span></span>

<span data-ttu-id="53a30-104">Saiba como dados de atraso de voo tooanalyze usando Hive no HDInsight baseados em Linux, em seguida, exportar Olá dados tooAzure banco de dados SQL usando Sqoop.</span><span class="sxs-lookup"><span data-stu-id="53a30-104">Learn how tooanalyze flight delay data using Hive on Linux-based HDInsight then export hello data tooAzure SQL Database using Sqoop.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="53a30-105">etapas de saudação neste documento exigem um cluster HDInsight que usa o Linux.</span><span class="sxs-lookup"><span data-stu-id="53a30-105">hello steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="53a30-106">Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="53a30-106">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="53a30-107">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="53a30-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

### <a name="prerequisites"></a><span data-ttu-id="53a30-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="53a30-108">Prerequisites</span></span>

* <span data-ttu-id="53a30-109">**Um cluster HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="53a30-109">**An HDInsight cluster**.</span></span> <span data-ttu-id="53a30-110">Confira [Introdução ao uso do Hadoop com o Hive no HDInsight em Linux](hdinsight-hadoop-linux-tutorial-get-started.md) para obter as etapas da criação de um novo cluster HDInsight baseado em Linux.</span><span class="sxs-lookup"><span data-stu-id="53a30-110">See [Get started using Hadoop with Hive in HDInsight on Linux](hdinsight-hadoop-linux-tutorial-get-started.md) for steps on creating a new Linux-based HDInsight cluster.</span></span>

* <span data-ttu-id="53a30-111">**Banco de dados SQL do Azure**.</span><span class="sxs-lookup"><span data-stu-id="53a30-111">**Azure SQL Database**.</span></span> <span data-ttu-id="53a30-112">Você usa um banco de dados SQL do Azure como um repositório de dados de destino.</span><span class="sxs-lookup"><span data-stu-id="53a30-112">You use an Azure SQL database as a destination data store.</span></span> <span data-ttu-id="53a30-113">Se você ainda não tem um Banco de Dados SQL, confira [Tutorial do Banco de Dados SQL: Criar um banco de dados SQL em minutos](../sql-database/sql-database-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="53a30-113">If you do not have a SQL Database already, see [SQL Database tutorial: Create a SQL database in minutes](../sql-database/sql-database-get-started.md).</span></span>

* <span data-ttu-id="53a30-114">**CLI do Azure**.</span><span class="sxs-lookup"><span data-stu-id="53a30-114">**Azure CLI**.</span></span> <span data-ttu-id="53a30-115">Se você não tiver instalado o hello CLI do Azure, consulte [instalar e configurar Olá CLI do Azure](../cli-install-nodejs.md) para mais etapas.</span><span class="sxs-lookup"><span data-stu-id="53a30-115">If you have not installed hello Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) for more steps.</span></span>

## <a name="download-hello-flight-data"></a><span data-ttu-id="53a30-116">Baixar dados de voo Olá</span><span class="sxs-lookup"><span data-stu-id="53a30-116">Download hello flight data</span></span>

1. <span data-ttu-id="53a30-117">Procurar muito[pesquisa e administração de tecnologia inovadora, agência de transporte estatísticas][rita-website].</span><span class="sxs-lookup"><span data-stu-id="53a30-117">Browse too[Research and Innovative Technology Administration, Bureau of Transportation Statistics][rita-website].</span></span>

2. <span data-ttu-id="53a30-118">Na página de saudação, selecione Olá valores a seguir:</span><span class="sxs-lookup"><span data-stu-id="53a30-118">On hello page, select hello following values:</span></span>

   | <span data-ttu-id="53a30-119">Nome</span><span class="sxs-lookup"><span data-stu-id="53a30-119">Name</span></span> | <span data-ttu-id="53a30-120">Valor</span><span class="sxs-lookup"><span data-stu-id="53a30-120">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="53a30-121">Filtrar por ano</span><span class="sxs-lookup"><span data-stu-id="53a30-121">Filter Year</span></span> |<span data-ttu-id="53a30-122">2013</span><span class="sxs-lookup"><span data-stu-id="53a30-122">2013</span></span> |
   | <span data-ttu-id="53a30-123">Filtrar por período</span><span class="sxs-lookup"><span data-stu-id="53a30-123">Filter Period</span></span> |<span data-ttu-id="53a30-124">Janeiro</span><span class="sxs-lookup"><span data-stu-id="53a30-124">January</span></span> |
   | <span data-ttu-id="53a30-125">Campos</span><span class="sxs-lookup"><span data-stu-id="53a30-125">Fields</span></span> |<span data-ttu-id="53a30-126">Year, FlightDate, UniqueCarrier, Carrier, FlightNum, OriginAirportID, Origin, OriginCityName, OriginState, DestAirportID, Dest, DestCityName, DestState, DepDelayMinutes, ArrDelay, ArrDelayMinutes, CarrierDelay, WeatherDelay, NASDelay, SecurityDelay, LateAircraftDelay.</span><span class="sxs-lookup"><span data-stu-id="53a30-126">Year, FlightDate, UniqueCarrier, Carrier, FlightNum, OriginAirportID, Origin, OriginCityName, OriginState, DestAirportID, Dest, DestCityName, DestState, DepDelayMinutes, ArrDelay, ArrDelayMinutes, CarrierDelay, WeatherDelay, NASDelay, SecurityDelay, LateAircraftDelay.</span></span> <span data-ttu-id="53a30-127">Limpar todos os outros campos</span><span class="sxs-lookup"><span data-stu-id="53a30-127">Clear all other fields</span></span> |

3. <span data-ttu-id="53a30-128">Clique em **Download**.</span><span class="sxs-lookup"><span data-stu-id="53a30-128">Click **Download**.</span></span>

## <a name="upload-hello-data"></a><span data-ttu-id="53a30-129">Carregar dados de saudação</span><span class="sxs-lookup"><span data-stu-id="53a30-129">Upload hello data</span></span>

1. <span data-ttu-id="53a30-130">Use Olá comando tooupload Olá zip arquivo toohello HDInsight nó principal do cluster a seguir:</span><span class="sxs-lookup"><span data-stu-id="53a30-130">Use hello following command tooupload hello zip file toohello HDInsight cluster head node:</span></span>

    ```
    scp FILENAME.zip USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:
    ```

    <span data-ttu-id="53a30-131">Substituir **FILENAME** com nome de saudação do arquivo zip de saudação.</span><span class="sxs-lookup"><span data-stu-id="53a30-131">Replace **FILENAME** with hello name of hello zip file.</span></span> <span data-ttu-id="53a30-132">Substituir **nome de usuário** com logon SSH Olá para o cluster do HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="53a30-132">Replace **USERNAME** with hello SSH login for hello HDInsight cluster.</span></span> <span data-ttu-id="53a30-133">Substitua CLUSTERNAME com nome de saudação do cluster do HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="53a30-133">Replace CLUSTERNAME with hello name of hello HDInsight cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="53a30-134">Se você usar uma senha tooauthenticate seu logon SSH, você será solicitado senha hello.</span><span class="sxs-lookup"><span data-stu-id="53a30-134">If you use a password tooauthenticate your SSH login, you are prompted for hello password.</span></span> <span data-ttu-id="53a30-135">Se você usou uma chave pública, talvez seja necessário Olá toouse `-i` parâmetro e especifique Olá caminho toohello correspondência de chave privada.</span><span class="sxs-lookup"><span data-stu-id="53a30-135">If you used a public key, you may need toouse hello `-i` parameter and specify hello path toohello matching private key.</span></span> <span data-ttu-id="53a30-136">Por exemplo: `scp -i ~/.ssh/id_rsa FILENAME.zip USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:`.</span><span class="sxs-lookup"><span data-stu-id="53a30-136">For example, `scp -i ~/.ssh/id_rsa FILENAME.zip USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:`.</span></span>

2. <span data-ttu-id="53a30-137">Depois de concluído o carregamento de saudação, conecte-se toohello cluster usando o SSH:</span><span class="sxs-lookup"><span data-stu-id="53a30-137">Once hello upload has completed, connect toohello cluster using SSH:</span></span>

    ```ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net```

    <span data-ttu-id="53a30-138">Para obter mais informações, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="53a30-138">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

3. <span data-ttu-id="53a30-139">Uma vez conectado, use Olá seguir toounzip hello. ZIP arquivo:</span><span class="sxs-lookup"><span data-stu-id="53a30-139">Once connected, use hello following toounzip hello .zip file:</span></span>

    ```
    unzip FILENAME.zip
    ```

    <span data-ttu-id="53a30-140">Este comando extrai um arquivo .csv com aproximadamente 60 MB.</span><span class="sxs-lookup"><span data-stu-id="53a30-140">This command extracts a .csv file that is roughly 60 MB.</span></span>

4. <span data-ttu-id="53a30-141">Use Olá após o comando toocreate um diretório no armazenamento de HDInsight e copie toohello diretório do arquivo de saudação:</span><span class="sxs-lookup"><span data-stu-id="53a30-141">Use hello following command toocreate a directory on HDInsight storage, and then copy hello file toohello directory:</span></span>

    ```
    hdfs dfs -mkdir -p /tutorials/flightdelays/data
    hdfs dfs -put FILENAME.csv /tutorials/flightdelays/data/
    ```

## <a name="create-and-run-hello-hiveql"></a><span data-ttu-id="53a30-142">Criar e executar Olá HiveQL</span><span class="sxs-lookup"><span data-stu-id="53a30-142">Create and run hello HiveQL</span></span>

<span data-ttu-id="53a30-143">Use Olá as etapas a seguir tooimport dados de arquivo CSV de saudação em uma tabela de Hive nomeada **atrasos**.</span><span class="sxs-lookup"><span data-stu-id="53a30-143">Use hello following steps tooimport data from hello CSV file into a Hive table named **Delays**.</span></span>

1. <span data-ttu-id="53a30-144">A seguir use Olá toocreate de comando e editar um novo arquivo denominado **flightdelays.hql**:</span><span class="sxs-lookup"><span data-stu-id="53a30-144">Use hello following command toocreate and edit a new file named **flightdelays.hql**:</span></span>

    ```
    nano flightdelays.hql
    ```

    <span data-ttu-id="53a30-145">Use Olá depois do texto como o conteúdo deste arquivo hello:</span><span class="sxs-lookup"><span data-stu-id="53a30-145">Use hello following text as hello contents of this file:</span></span>

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

2. <span data-ttu-id="53a30-146">arquivo de saudação toosave, use **Ctrl + X**, em seguida, **Y** .</span><span class="sxs-lookup"><span data-stu-id="53a30-146">toosave hello file, use **Ctrl + X**, then **Y** .</span></span>

3. <span data-ttu-id="53a30-147">toostart Hive e execução Olá **flightdelays.hql** de arquivos, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="53a30-147">toostart Hive and run hello **flightdelays.hql** file, use hello following command:</span></span>

    ```
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http' -f flightdelays.hql
    ```

   > [!NOTE]
   > <span data-ttu-id="53a30-148">Neste exemplo, `localhost` é usado, pois você está conectado toohello o nó principal do cluster do HDInsight hello, que é onde HiveServer2 está em execução.</span><span class="sxs-lookup"><span data-stu-id="53a30-148">In this example, `localhost` is used since you are connected toohello head node of hello HDInsight cluster, which is where HiveServer2 is running.</span></span>

4. <span data-ttu-id="53a30-149">Uma vez Olá __flightdelays.hql__ termina em execução, tooopen uma sessão interativa do Beeline comando a seguir de saudação do uso de script:</span><span class="sxs-lookup"><span data-stu-id="53a30-149">Once hello __flightdelays.hql__ script finishes running, use hello following command tooopen an interactive Beeline session:</span></span>

    ```
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http'
    ```

5. <span data-ttu-id="53a30-150">Quando você receber Olá `jdbc:hive2://localhost:10001/>` prompt, use Olá seguir tooretrieve os dados da consulta de dados de atraso de voo Olá importado.</span><span class="sxs-lookup"><span data-stu-id="53a30-150">When you receive hello `jdbc:hive2://localhost:10001/>` prompt, use hello following query tooretrieve data from hello imported flight delay data.</span></span>

    ```hiveql
    INSERT OVERWRITE DIRECTORY '/tutorials/flightdelays/output'
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    SELECT regexp_replace(origin_city_name, '''', ''),
        avg(weather_delay)
    FROM delays
    WHERE weather_delay IS NOT NULL
    GROUP BY origin_city_name;
    ```

    <span data-ttu-id="53a30-151">Essa consulta recupera uma lista de cidades que atrasos de clima experiente, juntamente com a média de saudação de tempo de espera e salvá-lo muito`/tutorials/flightdelays/output`.</span><span class="sxs-lookup"><span data-stu-id="53a30-151">This query retrieves a list of cities that experienced weather delays, along with hello average delay time, and save it too`/tutorials/flightdelays/output`.</span></span> <span data-ttu-id="53a30-152">Posteriormente, Sqoop lê dados saudação deste local e exportá-lo tooAzure banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="53a30-152">Later, Sqoop reads hello data from this location and export it tooAzure SQL Database.</span></span>

6. <span data-ttu-id="53a30-153">tooexit Beeline, insira `!quit` no prompt de saudação.</span><span class="sxs-lookup"><span data-stu-id="53a30-153">tooexit Beeline, enter `!quit` at hello prompt.</span></span>

## <a name="create-a-sql-database"></a><span data-ttu-id="53a30-154">Criar um banco de dados SQL</span><span class="sxs-lookup"><span data-stu-id="53a30-154">Create a SQL Database</span></span>

<span data-ttu-id="53a30-155">Se você já tiver um banco de dados SQL, você deve obter o nome do servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="53a30-155">If you already have a SQL Database, you must get hello server name.</span></span> <span data-ttu-id="53a30-156">Você pode encontrar o nome do servidor de saudação em Olá [portal do Azure](https://portal.azure.com) selecionando **bancos de dados SQL**, e, em seguida, filtrando em nome de saudação do hello banco de dados você deseja toouse.</span><span class="sxs-lookup"><span data-stu-id="53a30-156">You can find hello server name in hello [Azure portal](https://portal.azure.com) by selecting **SQL Databases**, and then filtering on hello name of hello database you wish toouse.</span></span> <span data-ttu-id="53a30-157">nome do servidor de saudação é listado em Olá **SERVER** coluna.</span><span class="sxs-lookup"><span data-stu-id="53a30-157">hello server name is listed in hello **SERVER** column.</span></span>

<span data-ttu-id="53a30-158">Se você ainda não tiver um banco de dados SQL, use as informações de saudação em [tutorial do banco de dados SQL: criar um banco de dados SQL em minutos](../sql-database/sql-database-get-started.md) toocreate um.</span><span class="sxs-lookup"><span data-stu-id="53a30-158">If you do not already have a SQL Database, use hello information in [SQL Database tutorial: Create a SQL database in minutes](../sql-database/sql-database-get-started.md) toocreate one.</span></span> <span data-ttu-id="53a30-159">Salve o nome do servidor de saudação usado para o banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="53a30-159">Save hello server name used for hello database.</span></span>

## <a name="create-a-sql-database-table"></a><span data-ttu-id="53a30-160">Criar uma tabela do Banco de Dados SQL</span><span class="sxs-lookup"><span data-stu-id="53a30-160">Create a SQL Database table</span></span>

> [!NOTE]
> <span data-ttu-id="53a30-161">Há tooSQL tooconnect de muitas maneiras banco de dados e criar uma tabela.</span><span class="sxs-lookup"><span data-stu-id="53a30-161">There are many ways tooconnect tooSQL Database and create a table.</span></span> <span data-ttu-id="53a30-162">Olá use as etapas a seguir [FreeTDS](http://www.freetds.org/) do cluster do HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="53a30-162">hello following steps use [FreeTDS](http://www.freetds.org/) from hello HDInsight cluster.</span></span>


1. <span data-ttu-id="53a30-163">Use SSH tooconnect toohello HDInsight baseados em Linux cluster e execução Olá seguindo as etapas da sessão SSH hello.</span><span class="sxs-lookup"><span data-stu-id="53a30-163">Use SSH tooconnect toohello Linux-based HDInsight cluster, and run hello following steps from hello SSH session.</span></span>

2. <span data-ttu-id="53a30-164">Use Olá comando tooinstall FreeTDS a seguir:</span><span class="sxs-lookup"><span data-stu-id="53a30-164">Use hello following command tooinstall FreeTDS:</span></span>

    ```
    sudo apt-get --assume-yes install freetds-dev freetds-bin
    ```

3. <span data-ttu-id="53a30-165">Depois de concluir a instalação do hello, use Olá após o servidor de banco de dados SQL do comando tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="53a30-165">Once hello install completes, use hello following command tooconnect toohello SQL Database server.</span></span> <span data-ttu-id="53a30-166">Substituir **serverName** com o nome do servidor de banco de dados SQL hello.</span><span class="sxs-lookup"><span data-stu-id="53a30-166">Replace **serverName** with hello SQL Database server name.</span></span> <span data-ttu-id="53a30-167">Substituir **adminLogin** e **adminPassword** com logon Olá para o banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="53a30-167">Replace **adminLogin** and **adminPassword** with hello login for SQL Database.</span></span> <span data-ttu-id="53a30-168">Substituir **databaseName** com o nome do banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="53a30-168">Replace **databaseName** with hello database name.</span></span>

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D <databaseName>
    ```

    <span data-ttu-id="53a30-169">Você receberá a saída toohello semelhante texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="53a30-169">You receive output similar toohello following text:</span></span>

    ```
    locale is "en_US.UTF-8"
    locale charset is "UTF-8"
    using default charset "UTF-8"
    Default database being set toosqooptest
    1>
    ```

4. <span data-ttu-id="53a30-170">Em Olá `1>` prompt, digite Olá linhas seguintes:</span><span class="sxs-lookup"><span data-stu-id="53a30-170">At hello `1>` prompt, enter hello following lines:</span></span>

    ```
    CREATE TABLE [dbo].[delays](
    [origin_city_name] [nvarchar](50) NOT NULL,
    [weather_delay] float,
    CONSTRAINT [PK_delays] PRIMARY KEY CLUSTERED   
    ([origin_city_name] ASC))
    GO
    ```

    <span data-ttu-id="53a30-171">Olá quando `GO` instrução for inserida, instruções de saudação anterior são avaliadas.</span><span class="sxs-lookup"><span data-stu-id="53a30-171">When hello `GO` statement is entered, hello previous statements are evaluated.</span></span> <span data-ttu-id="53a30-172">Essa consulta cria uma tabela chamada **atrasos**, com um índice clusterizado.</span><span class="sxs-lookup"><span data-stu-id="53a30-172">This query creates a table named **delays**, with a clustered index.</span></span>

    <span data-ttu-id="53a30-173">Saudação de uso tooverify de consulta que Olá a tabela a seguir foi criada:</span><span class="sxs-lookup"><span data-stu-id="53a30-173">Use hello following query tooverify that hello table has been created:</span></span>

    ```
    SELECT * FROM information_schema.tables
    GO
    ```

    <span data-ttu-id="53a30-174">saudação de saída é similar toohello texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="53a30-174">hello output is similar toohello following text:</span></span>

    ```
    TABLE_CATALOG   TABLE_SCHEMA    TABLE_NAME      TABLE_TYPE
    databaseName       dbo     delays      BASE TABLE
    ```

5. <span data-ttu-id="53a30-175">Digite `exit` em Olá `1>` tooexit Olá tsql utilitário do prompt.</span><span class="sxs-lookup"><span data-stu-id="53a30-175">Enter `exit` at hello `1>` prompt tooexit hello tsql utility.</span></span>

## <a name="export-data-with-sqoop"></a><span data-ttu-id="53a30-176">Exportar dados com o Sqoop</span><span class="sxs-lookup"><span data-stu-id="53a30-176">Export data with Sqoop</span></span>

1. <span data-ttu-id="53a30-177">Use Olá tooverify de comando que Sqoop pode ver o banco de dados SQL a seguir:</span><span class="sxs-lookup"><span data-stu-id="53a30-177">Use hello following command tooverify that Sqoop can see your SQL Database:</span></span>

    ```
    sqoop list-databases --connect jdbc:sqlserver://<serverName>.database.windows.net:1433 --username <adminLogin> --password <adminPassword>
    ```

    <span data-ttu-id="53a30-178">Esse comando retorna uma lista de bancos de dados, incluindo Olá banco de dados que você criou a tabela atrasos Olá anteriormente.</span><span class="sxs-lookup"><span data-stu-id="53a30-178">This command returns a list of databases, including hello database that you created hello delays table in earlier.</span></span>

2. <span data-ttu-id="53a30-179">Use Olá dados tooexport de comando a seguir da tabela de mobiledata toohello hivesampletable:</span><span class="sxs-lookup"><span data-stu-id="53a30-179">Use hello following command tooexport data from hivesampletable toohello mobiledata table:</span></span>

    ```
    sqoop export --connect 'jdbc:sqlserver://<serverName>.database.windows.net:1433;database=<databaseName>' --username <adminLogin> --password <adminPassword> --table 'delays' --export-dir '/tutorials/flightdelays/output' --fields-terminated-by '\t' -m 1
    ```

    <span data-ttu-id="53a30-180">Sqoop conecta toohello banco de dados que contém a tabela de atrasos de saudação e exporta dados de saudação `/tutorials/flightdelays/output` tabela de atrasos de toohello do diretório.</span><span class="sxs-lookup"><span data-stu-id="53a30-180">Sqoop connects toohello database containing hello delays table, and exports data from hello `/tutorials/flightdelays/output` directory toohello delays table.</span></span>

3. <span data-ttu-id="53a30-181">Após a conclusão do comando hello, use Olá tooconnect toohello banco de dados usando TSQL a seguir:</span><span class="sxs-lookup"><span data-stu-id="53a30-181">After hello command completes, use hello following tooconnect toohello database using TSQL:</span></span>

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D <databaseName>
    ```

    <span data-ttu-id="53a30-182">Uma vez conectado, use Olá instruções tooverify dados saudação foram exportado toohello mobiledata tabela a seguir:</span><span class="sxs-lookup"><span data-stu-id="53a30-182">Once connected, use hello following statements tooverify that hello data was exported toohello mobiledata table:</span></span>

    ```
    SELECT * FROM delays
    GO
    ```

    <span data-ttu-id="53a30-183">Você deve ver uma lista dos dados na tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="53a30-183">You should see a listing of data in hello table.</span></span> <span data-ttu-id="53a30-184">Tipo `exit` utilitário do tooexit Olá tsql.</span><span class="sxs-lookup"><span data-stu-id="53a30-184">Type `exit` tooexit hello tsql utility.</span></span>

## <span data-ttu-id="53a30-185"><a id="nextsteps"></a> Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="53a30-185"><a id="nextsteps"></a> Next steps</span></span>

<span data-ttu-id="53a30-186">toolearn mais toowork maneiras com dados no HDInsight, consulte Olá seguintes documentos:</span><span class="sxs-lookup"><span data-stu-id="53a30-186">toolearn more ways toowork with data in HDInsight, see hello following documents:</span></span>

* <span data-ttu-id="53a30-187">[Usar o Hive com o HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="53a30-187">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="53a30-188">[Usar o Oozie com o HDInsight][hdinsight-use-oozie]</span><span class="sxs-lookup"><span data-stu-id="53a30-188">[Use Oozie with HDInsight][hdinsight-use-oozie]</span></span>
* <span data-ttu-id="53a30-189">[Use o Sqoop com o HDInsight][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="53a30-189">[Use Sqoop with HDInsight][hdinsight-use-sqoop]</span></span>
* <span data-ttu-id="53a30-190">[Usar o Pig com o HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="53a30-190">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="53a30-191">[Desenvolver programas Java MapReduce para HDInsight][hdinsight-develop-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="53a30-191">[Develop Java MapReduce programs for HDInsight][hdinsight-develop-mapreduce]</span></span>
* <span data-ttu-id="53a30-192">[Desenvolver programas de streaming do Hadoop em Python para o HDInsight][hdinsight-develop-streaming]</span><span class="sxs-lookup"><span data-stu-id="53a30-192">[Develop Python Hadoop streaming programs for HDInsight][hdinsight-develop-streaming]</span></span>

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
