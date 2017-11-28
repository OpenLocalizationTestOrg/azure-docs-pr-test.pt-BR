---
title: "Analisar dados de atraso de voo com o Hive no HDInsight – Azure | Microsoft Docs"
description: Saiba como usar o Hive para analisar dados de voos usando no HDInsight baseado em Linux e exportar os dados para um Banco de Dados SQL do Azure usando o Sqoop.
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
ms.openlocfilehash: 8cdc19ac8a517b6d8eefabb5476a686aa252a332
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="analyze-flight-delay-data-by-using-hive-on-linux-based-hdinsight"></a><span data-ttu-id="aee8d-103">Analisar dados de atraso de voo usando o Hive no HDInsight baseado em Linux</span><span class="sxs-lookup"><span data-stu-id="aee8d-103">Analyze flight delay data by using Hive on Linux-based HDInsight</span></span>

<span data-ttu-id="aee8d-104">Saiba como analisar dados de atraso de voos usando o Hive no HDInsight baseado em Linux e exporte os dados para um Banco de Dados SQL do Azure usando o Sqoop.</span><span class="sxs-lookup"><span data-stu-id="aee8d-104">Learn how to analyze flight delay data using Hive on Linux-based HDInsight then export the data to Azure SQL Database using Sqoop.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="aee8d-105">As etapas deste documento exigem um cluster HDInsight que usa Linux.</span><span class="sxs-lookup"><span data-stu-id="aee8d-105">The steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="aee8d-106">O Linux é o único sistema operacional usado no HDInsight versão 3.4 ou superior.</span><span class="sxs-lookup"><span data-stu-id="aee8d-106">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="aee8d-107">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="aee8d-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

### <a name="prerequisites"></a><span data-ttu-id="aee8d-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="aee8d-108">Prerequisites</span></span>

* <span data-ttu-id="aee8d-109">**Um cluster HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="aee8d-109">**An HDInsight cluster**.</span></span> <span data-ttu-id="aee8d-110">Confira [Introdução ao uso do Hadoop com o Hive no HDInsight em Linux](hdinsight-hadoop-linux-tutorial-get-started.md) para obter as etapas da criação de um novo cluster HDInsight baseado em Linux.</span><span class="sxs-lookup"><span data-stu-id="aee8d-110">See [Get started using Hadoop with Hive in HDInsight on Linux](hdinsight-hadoop-linux-tutorial-get-started.md) for steps on creating a new Linux-based HDInsight cluster.</span></span>

* <span data-ttu-id="aee8d-111">**Banco de dados SQL do Azure**.</span><span class="sxs-lookup"><span data-stu-id="aee8d-111">**Azure SQL Database**.</span></span> <span data-ttu-id="aee8d-112">Você usa um banco de dados SQL do Azure como um repositório de dados de destino.</span><span class="sxs-lookup"><span data-stu-id="aee8d-112">You use an Azure SQL database as a destination data store.</span></span> <span data-ttu-id="aee8d-113">Se você ainda não tem um Banco de Dados SQL, confira [Tutorial do Banco de Dados SQL: Criar um banco de dados SQL em minutos](../sql-database/sql-database-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="aee8d-113">If you do not have a SQL Database already, see [SQL Database tutorial: Create a SQL database in minutes](../sql-database/sql-database-get-started.md).</span></span>

* <span data-ttu-id="aee8d-114">**CLI do Azure**.</span><span class="sxs-lookup"><span data-stu-id="aee8d-114">**Azure CLI**.</span></span> <span data-ttu-id="aee8d-115">Se você não tiver instalado a CLI do Azure, confira [Instalar e configurar a CLI do Azure](../cli-install-nodejs.md) para ver mais etapas.</span><span class="sxs-lookup"><span data-stu-id="aee8d-115">If you have not installed the Azure CLI, see [Install and Configure the Azure CLI](../cli-install-nodejs.md) for more steps.</span></span>

## <a name="download-the-flight-data"></a><span data-ttu-id="aee8d-116">Baixar os dados de voos</span><span class="sxs-lookup"><span data-stu-id="aee8d-116">Download the flight data</span></span>

1. <span data-ttu-id="aee8d-117">Navegue para [Research and Innovative Technology Administration, Bureau of Transportation Statistics][rita-website].</span><span class="sxs-lookup"><span data-stu-id="aee8d-117">Browse to [Research and Innovative Technology Administration, Bureau of Transportation Statistics][rita-website].</span></span>

2. <span data-ttu-id="aee8d-118">Na página, selecione os valores a seguir:</span><span class="sxs-lookup"><span data-stu-id="aee8d-118">On the page, select the following values:</span></span>

   | <span data-ttu-id="aee8d-119">Nome</span><span class="sxs-lookup"><span data-stu-id="aee8d-119">Name</span></span> | <span data-ttu-id="aee8d-120">Valor</span><span class="sxs-lookup"><span data-stu-id="aee8d-120">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="aee8d-121">Filtrar por ano</span><span class="sxs-lookup"><span data-stu-id="aee8d-121">Filter Year</span></span> |<span data-ttu-id="aee8d-122">2013</span><span class="sxs-lookup"><span data-stu-id="aee8d-122">2013</span></span> |
   | <span data-ttu-id="aee8d-123">Filtrar por período</span><span class="sxs-lookup"><span data-stu-id="aee8d-123">Filter Period</span></span> |<span data-ttu-id="aee8d-124">Janeiro</span><span class="sxs-lookup"><span data-stu-id="aee8d-124">January</span></span> |
   | <span data-ttu-id="aee8d-125">Campos</span><span class="sxs-lookup"><span data-stu-id="aee8d-125">Fields</span></span> |<span data-ttu-id="aee8d-126">Year, FlightDate, UniqueCarrier, Carrier, FlightNum, OriginAirportID, Origin, OriginCityName, OriginState, DestAirportID, Dest, DestCityName, DestState, DepDelayMinutes, ArrDelay, ArrDelayMinutes, CarrierDelay, WeatherDelay, NASDelay, SecurityDelay, LateAircraftDelay.</span><span class="sxs-lookup"><span data-stu-id="aee8d-126">Year, FlightDate, UniqueCarrier, Carrier, FlightNum, OriginAirportID, Origin, OriginCityName, OriginState, DestAirportID, Dest, DestCityName, DestState, DepDelayMinutes, ArrDelay, ArrDelayMinutes, CarrierDelay, WeatherDelay, NASDelay, SecurityDelay, LateAircraftDelay.</span></span> <span data-ttu-id="aee8d-127">Limpar todos os outros campos</span><span class="sxs-lookup"><span data-stu-id="aee8d-127">Clear all other fields</span></span> |

3. <span data-ttu-id="aee8d-128">Clique em **Download**.</span><span class="sxs-lookup"><span data-stu-id="aee8d-128">Click **Download**.</span></span>

## <a name="upload-the-data"></a><span data-ttu-id="aee8d-129">Carregar os dados</span><span class="sxs-lookup"><span data-stu-id="aee8d-129">Upload the data</span></span>

1. <span data-ttu-id="aee8d-130">Use o comando a seguir para carregar o arquivo zip no nó principal do cluster HDInsight:</span><span class="sxs-lookup"><span data-stu-id="aee8d-130">Use the following command to upload the zip file to the HDInsight cluster head node:</span></span>

    ```
    scp FILENAME.zip USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:
    ```

    <span data-ttu-id="aee8d-131">Substitua **NOMEDOARQUIVO** pelo nome do arquivo zip.</span><span class="sxs-lookup"><span data-stu-id="aee8d-131">Replace **FILENAME** with the name of the zip file.</span></span> <span data-ttu-id="aee8d-132">Substitua **NOMEDEUSUÁRIO** pelo logon SSH para o cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="aee8d-132">Replace **USERNAME** with the SSH login for the HDInsight cluster.</span></span> <span data-ttu-id="aee8d-133">Substitua NOMEDOCLUSTER pelo nome do seu cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="aee8d-133">Replace CLUSTERNAME with the name of the HDInsight cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="aee8d-134">Se você usar uma senha para autenticar seu logon SSH, a senha será solicitada.</span><span class="sxs-lookup"><span data-stu-id="aee8d-134">If you use a password to authenticate your SSH login, you are prompted for the password.</span></span> <span data-ttu-id="aee8d-135">Se você tiver usado uma chave pública, talvez precise usar o parâmetro `-i` e especificar a chave privada correspondente.</span><span class="sxs-lookup"><span data-stu-id="aee8d-135">If you used a public key, you may need to use the `-i` parameter and specify the path to the matching private key.</span></span> <span data-ttu-id="aee8d-136">Por exemplo: `scp -i ~/.ssh/id_rsa FILENAME.zip USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:`.</span><span class="sxs-lookup"><span data-stu-id="aee8d-136">For example, `scp -i ~/.ssh/id_rsa FILENAME.zip USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:`.</span></span>

2. <span data-ttu-id="aee8d-137">Quando o upload for concluído, conecte-se ao cluster usando SSH:</span><span class="sxs-lookup"><span data-stu-id="aee8d-137">Once the upload has completed, connect to the cluster using SSH:</span></span>

    ```ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net```

    <span data-ttu-id="aee8d-138">Para obter mais informações, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="aee8d-138">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

3. <span data-ttu-id="aee8d-139">Uma vez conectado, use o seguinte para descompactar o arquivo .zip:</span><span class="sxs-lookup"><span data-stu-id="aee8d-139">Once connected, use the following to unzip the .zip file:</span></span>

    ```
    unzip FILENAME.zip
    ```

    <span data-ttu-id="aee8d-140">Este comando extrai um arquivo .csv com aproximadamente 60 MB.</span><span class="sxs-lookup"><span data-stu-id="aee8d-140">This command extracts a .csv file that is roughly 60 MB.</span></span>

4. <span data-ttu-id="aee8d-141">Use o seguinte comando para criar um diretório no armazenamento do HDInsight e, em seguida, copie o arquivo para o diretório:</span><span class="sxs-lookup"><span data-stu-id="aee8d-141">Use the following command to create a directory on HDInsight storage, and then copy the file to the directory:</span></span>

    ```
    hdfs dfs -mkdir -p /tutorials/flightdelays/data
    hdfs dfs -put FILENAME.csv /tutorials/flightdelays/data/
    ```

## <a name="create-and-run-the-hiveql"></a><span data-ttu-id="aee8d-142">Criar e executar o HiveQL</span><span class="sxs-lookup"><span data-stu-id="aee8d-142">Create and run the HiveQL</span></span>

<span data-ttu-id="aee8d-143">Use as etapas a seguir para importar dados do arquivo CSV para uma tabela do Hive chamada **Delays**.</span><span class="sxs-lookup"><span data-stu-id="aee8d-143">Use the following steps to import data from the CSV file into a Hive table named **Delays**.</span></span>

1. <span data-ttu-id="aee8d-144">Use o comando a seguir para criar e editar um novo arquivo chamado **flightdelays.hql**:</span><span class="sxs-lookup"><span data-stu-id="aee8d-144">Use the following command to create and edit a new file named **flightdelays.hql**:</span></span>

    ```
    nano flightdelays.hql
    ```

    <span data-ttu-id="aee8d-145">Use o seguinte texto como o conteúdo deste arquivo:</span><span class="sxs-lookup"><span data-stu-id="aee8d-145">Use the following text as the contents of this file:</span></span>

    ```hiveql
    DROP TABLE delays_raw;
    -- Creates an external table over the csv file
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
    -- The following lines describe the format and location of the file
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ','
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE
    LOCATION '/tutorials/flightdelays/data';

    -- Drop the delays table if it exists
    DROP TABLE delays;
    -- Create the delays table and populate it with data
    -- pulled in from the CSV file (via the external table defined previously)
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

2. <span data-ttu-id="aee8d-146">Use **Ctrl + X** seguido de **Y** para salvar o arquivo.</span><span class="sxs-lookup"><span data-stu-id="aee8d-146">To save the file, use **Ctrl + X**, then **Y** .</span></span>

3. <span data-ttu-id="aee8d-147">Use o seguinte comando para iniciar o Hive e executar o arquivo **flightdelays.hql**:</span><span class="sxs-lookup"><span data-stu-id="aee8d-147">To start Hive and run the **flightdelays.hql** file, use the following command:</span></span>

    ```
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http' -f flightdelays.hql
    ```

   > [!NOTE]
   > <span data-ttu-id="aee8d-148">Neste exemplo, `localhost` é usado, pois você está conectado ao nó principal do cluster HDInsight, que é onde o HiveServer2 está em execução.</span><span class="sxs-lookup"><span data-stu-id="aee8d-148">In this example, `localhost` is used since you are connected to the head node of the HDInsight cluster, which is where HiveServer2 is running.</span></span>

4. <span data-ttu-id="aee8d-149">Uma vez o __flightdelays__ fim da execução de script, use o seguinte comando para abrir uma sessão interativa de Beeline:</span><span class="sxs-lookup"><span data-stu-id="aee8d-149">Once the __flightdelays.hql__ script finishes running, use the following command to open an interactive Beeline session:</span></span>

    ```
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http'
    ```

5. <span data-ttu-id="aee8d-150">Quando você receber o prompt do `jdbc:hive2://localhost:10001/>`, use a seguinte consulta para recuperar dados usando os dados importados de voos atrasados.</span><span class="sxs-lookup"><span data-stu-id="aee8d-150">When you receive the `jdbc:hive2://localhost:10001/>` prompt, use the following query to retrieve data from the imported flight delay data.</span></span>

    ```hiveql
    INSERT OVERWRITE DIRECTORY '/tutorials/flightdelays/output'
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    SELECT regexp_replace(origin_city_name, '''', ''),
        avg(weather_delay)
    FROM delays
    WHERE weather_delay IS NOT NULL
    GROUP BY origin_city_name;
    ```

    <span data-ttu-id="aee8d-151">Essa consulta recupera uma lista de cidades em que houve atrasos causados pelo clima, além do tempo médio de atrasos, e a salva em `/tutorials/flightdelays/output`.</span><span class="sxs-lookup"><span data-stu-id="aee8d-151">This query retrieves a list of cities that experienced weather delays, along with the average delay time, and save it to `/tutorials/flightdelays/output`.</span></span> <span data-ttu-id="aee8d-152">Posteriormente, o Sqoop lerá os dados desse local e os exportará para o Banco de Dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="aee8d-152">Later, Sqoop reads the data from this location and export it to Azure SQL Database.</span></span>

6. <span data-ttu-id="aee8d-153">Para sair do Beeline, digite `!quit` no prompt.</span><span class="sxs-lookup"><span data-stu-id="aee8d-153">To exit Beeline, enter `!quit` at the prompt.</span></span>

## <a name="create-a-sql-database"></a><span data-ttu-id="aee8d-154">Criar um banco de dados SQL</span><span class="sxs-lookup"><span data-stu-id="aee8d-154">Create a SQL Database</span></span>

<span data-ttu-id="aee8d-155">Se você já tiver um Banco de Dados SQL, deverá obter o nome do servidor.</span><span class="sxs-lookup"><span data-stu-id="aee8d-155">If you already have a SQL Database, you must get the server name.</span></span> <span data-ttu-id="aee8d-156">Você pode encontrar o nome do servidor no [Portal do Azure](https://portal.azure.com) selecionando **Bancos de Dados SQL** e, então, filtrando o nome do banco de dados que você deseja usar.</span><span class="sxs-lookup"><span data-stu-id="aee8d-156">You can find the server name in the [Azure portal](https://portal.azure.com) by selecting **SQL Databases**, and then filtering on the name of the database you wish to use.</span></span> <span data-ttu-id="aee8d-157">O nome do servidor está listado na coluna **SERVIDOR** .</span><span class="sxs-lookup"><span data-stu-id="aee8d-157">The server name is listed in the **SERVER** column.</span></span>

<span data-ttu-id="aee8d-158">Se você ainda não tem um Banco de Dados SQL, use as informações em [Tutorial do Banco de Dados SQL: Criar um banco de dados SQL em minutos](../sql-database/sql-database-get-started.md) para criar um.</span><span class="sxs-lookup"><span data-stu-id="aee8d-158">If you do not already have a SQL Database, use the information in [SQL Database tutorial: Create a SQL database in minutes](../sql-database/sql-database-get-started.md) to create one.</span></span> <span data-ttu-id="aee8d-159">Salve o nome do servidor usado para o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="aee8d-159">Save the server name used for the database.</span></span>

## <a name="create-a-sql-database-table"></a><span data-ttu-id="aee8d-160">Criar uma tabela do Banco de Dados SQL</span><span class="sxs-lookup"><span data-stu-id="aee8d-160">Create a SQL Database table</span></span>

> [!NOTE]
> <span data-ttu-id="aee8d-161">Há várias maneiras de se conectar ao Banco de Dados SQL e criar uma tabela.</span><span class="sxs-lookup"><span data-stu-id="aee8d-161">There are many ways to connect to SQL Database and create a table.</span></span> <span data-ttu-id="aee8d-162">As seguintes etapas usam [FreeTDS](http://www.freetds.org/) do cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="aee8d-162">The following steps use [FreeTDS](http://www.freetds.org/) from the HDInsight cluster.</span></span>


1. <span data-ttu-id="aee8d-163">Use o SSH para conectar-se ao cluster HDInsight baseado em Linux e execute as etapas a seguir na sessão SSH.</span><span class="sxs-lookup"><span data-stu-id="aee8d-163">Use SSH to connect to the Linux-based HDInsight cluster, and run the following steps from the SSH session.</span></span>

2. <span data-ttu-id="aee8d-164">Use o seguinte comando para instalar o FreeTDS:</span><span class="sxs-lookup"><span data-stu-id="aee8d-164">Use the following command to install FreeTDS:</span></span>

    ```
    sudo apt-get --assume-yes install freetds-dev freetds-bin
    ```

3. <span data-ttu-id="aee8d-165">Após a conclusão da instalação, use o seguinte comando para conectar-se ao servidor do Banco de Dados SQL.</span><span class="sxs-lookup"><span data-stu-id="aee8d-165">Once the install completes, use the following command to connect to the SQL Database server.</span></span> <span data-ttu-id="aee8d-166">Substitua **serverName** pelo nome do servidor do Banco de Dados SQL.</span><span class="sxs-lookup"><span data-stu-id="aee8d-166">Replace **serverName** with the SQL Database server name.</span></span> <span data-ttu-id="aee8d-167">Substitua **adminLogin** e **adminPassword** pelo logon do Banco de Dados SQL.</span><span class="sxs-lookup"><span data-stu-id="aee8d-167">Replace **adminLogin** and **adminPassword** with the login for SQL Database.</span></span> <span data-ttu-id="aee8d-168">Substitua **databaseName** pelo nome do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="aee8d-168">Replace **databaseName** with the database name.</span></span>

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D <databaseName>
    ```

    <span data-ttu-id="aee8d-169">Você receberá saídas semelhantes ao seguinte texto:</span><span class="sxs-lookup"><span data-stu-id="aee8d-169">You receive output similar to the following text:</span></span>

    ```
    locale is "en_US.UTF-8"
    locale charset is "UTF-8"
    using default charset "UTF-8"
    Default database being set to sqooptest
    1>
    ```

4. <span data-ttu-id="aee8d-170">Ao prompt `1>` , insira o seguinte:</span><span class="sxs-lookup"><span data-stu-id="aee8d-170">At the `1>` prompt, enter the following lines:</span></span>

    ```
    CREATE TABLE [dbo].[delays](
    [origin_city_name] [nvarchar](50) NOT NULL,
    [weather_delay] float,
    CONSTRAINT [PK_delays] PRIMARY KEY CLUSTERED   
    ([origin_city_name] ASC))
    GO
    ```

    <span data-ttu-id="aee8d-171">Quando a instrução `GO` for inserida, as instruções anteriores serão avaliadas.</span><span class="sxs-lookup"><span data-stu-id="aee8d-171">When the `GO` statement is entered, the previous statements are evaluated.</span></span> <span data-ttu-id="aee8d-172">Essa consulta cria uma tabela chamada **atrasos**, com um índice clusterizado.</span><span class="sxs-lookup"><span data-stu-id="aee8d-172">This query creates a table named **delays**, with a clustered index.</span></span>

    <span data-ttu-id="aee8d-173">Use a seguinte consulta para verificar se a tabela foi criada:</span><span class="sxs-lookup"><span data-stu-id="aee8d-173">Use the following query to verify that the table has been created:</span></span>

    ```
    SELECT * FROM information_schema.tables
    GO
    ```

    <span data-ttu-id="aee8d-174">A saída é semelhante ao texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="aee8d-174">The output is similar to the following text:</span></span>

    ```
    TABLE_CATALOG   TABLE_SCHEMA    TABLE_NAME      TABLE_TYPE
    databaseName       dbo     delays      BASE TABLE
    ```

5. <span data-ttu-id="aee8d-175">Para sair do utilitário tsql, insira `exit` at the `1>` .</span><span class="sxs-lookup"><span data-stu-id="aee8d-175">Enter `exit` at the `1>` prompt to exit the tsql utility.</span></span>

## <a name="export-data-with-sqoop"></a><span data-ttu-id="aee8d-176">Exportar dados com o Sqoop</span><span class="sxs-lookup"><span data-stu-id="aee8d-176">Export data with Sqoop</span></span>

1. <span data-ttu-id="aee8d-177">Use o comando a seguir para verificar se o Sqoop pode ver seu Banco de Dados SQL:</span><span class="sxs-lookup"><span data-stu-id="aee8d-177">Use the following command to verify that Sqoop can see your SQL Database:</span></span>

    ```
    sqoop list-databases --connect jdbc:sqlserver://<serverName>.database.windows.net:1433 --username <adminLogin> --password <adminPassword>
    ```

    <span data-ttu-id="aee8d-178">Esse comando retorna uma lista de bancos de dados, incluindo o banco de dados no qual você criou a tabela de atrasos anteriormente.</span><span class="sxs-lookup"><span data-stu-id="aee8d-178">This command returns a list of databases, including the database that you created the delays table in earlier.</span></span>

2. <span data-ttu-id="aee8d-179">Use o comando a seguir para exportar dados de hivesampletable para a tabela mobiledata:</span><span class="sxs-lookup"><span data-stu-id="aee8d-179">Use the following command to export data from hivesampletable to the mobiledata table:</span></span>

    ```
    sqoop export --connect 'jdbc:sqlserver://<serverName>.database.windows.net:1433;database=<databaseName>' --username <adminLogin> --password <adminPassword> --table 'delays' --export-dir '/tutorials/flightdelays/output' --fields-terminated-by '\t' -m 1
    ```

    <span data-ttu-id="aee8d-180">O Sqoop se conecta ao banco de dados que contém a tabela de atrasos e exporta dados do diretório `/tutorials/flightdelays/output` para a tabela de atrasos.</span><span class="sxs-lookup"><span data-stu-id="aee8d-180">Sqoop connects to the database containing the delays table, and exports data from the `/tutorials/flightdelays/output` directory to the delays table.</span></span>

3. <span data-ttu-id="aee8d-181">Depois de concluir o comando, use o seguinte para se conectar ao banco de dados usando TSQL:</span><span class="sxs-lookup"><span data-stu-id="aee8d-181">After the command completes, use the following to connect to the database using TSQL:</span></span>

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D <databaseName>
    ```

    <span data-ttu-id="aee8d-182">Uma vez conectado, use as instruções a seguir para verificar se os dados foram exportados para a tabela mobiledata:</span><span class="sxs-lookup"><span data-stu-id="aee8d-182">Once connected, use the following statements to verify that the data was exported to the mobiledata table:</span></span>

    ```
    SELECT * FROM delays
    GO
    ```

    <span data-ttu-id="aee8d-183">Você deve ver uma listagem dos dados na tabela.</span><span class="sxs-lookup"><span data-stu-id="aee8d-183">You should see a listing of data in the table.</span></span> <span data-ttu-id="aee8d-184">Digite `exit` para sair do utilitário tsql.</span><span class="sxs-lookup"><span data-stu-id="aee8d-184">Type `exit` to exit the tsql utility.</span></span>

## <span data-ttu-id="aee8d-185"><a id="nextsteps"></a> Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="aee8d-185"><a id="nextsteps"></a> Next steps</span></span>

<span data-ttu-id="aee8d-186">Para saber mais formas de trabalhar usando dados no HDInsight, consulte os seguintes documentos:</span><span class="sxs-lookup"><span data-stu-id="aee8d-186">To learn more ways to work with data in HDInsight, see the following documents:</span></span>

* <span data-ttu-id="aee8d-187">[Usar o Hive com o HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="aee8d-187">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="aee8d-188">[Usar o Oozie com o HDInsight][hdinsight-use-oozie]</span><span class="sxs-lookup"><span data-stu-id="aee8d-188">[Use Oozie with HDInsight][hdinsight-use-oozie]</span></span>
* <span data-ttu-id="aee8d-189">[Use o Sqoop com o HDInsight][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="aee8d-189">[Use Sqoop with HDInsight][hdinsight-use-sqoop]</span></span>
* <span data-ttu-id="aee8d-190">[Usar o Pig com o HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="aee8d-190">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="aee8d-191">[Desenvolver programas Java MapReduce para HDInsight][hdinsight-develop-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="aee8d-191">[Develop Java MapReduce programs for HDInsight][hdinsight-develop-mapreduce]</span></span>
* <span data-ttu-id="aee8d-192">[Desenvolver programas de streaming do Hadoop em Python para o HDInsight][hdinsight-develop-streaming]</span><span class="sxs-lookup"><span data-stu-id="aee8d-192">[Develop Python Hadoop streaming programs for HDInsight][hdinsight-develop-streaming]</span></span>

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
