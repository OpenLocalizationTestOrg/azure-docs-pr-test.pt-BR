---
title: "O Processo de Ciência de Dados de Equipe em ação: usando o SQL Data Warehouse | Microsoft Docs"
description: "Processo e Tecnologia de Análise Avançada em ação"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 88ba8e28-0bd7-49fe-8320-5dfa83b65724
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev;hangzh;weig
ms.openlocfilehash: ce7de48af0f2f21576c66a962b88635a0f9f8333
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="the-team-data-science-process-in-action-using-sql-data-warehouse"></a><span data-ttu-id="49555-103">O Processo de Ciência de Dados de Equipe em ação: usando o SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="49555-103">The Team Data Science Process in action: using SQL Data Warehouse</span></span>
<span data-ttu-id="49555-104">Neste tutorial, explicamos como criar e implantar de um modelo de Machine Learning usando o SQL DW (SQL Data Warehouse) para um conjunto de dados publicamente disponível – o conjunto de dados [Corridas de Táxi de NYC](http://www.andresmh.com/nyctaxitrips/).</span><span class="sxs-lookup"><span data-stu-id="49555-104">In this tutorial, we walk you through building and deploying a machine learning model using SQL Data Warehouse (SQL DW) for a publicly available dataset -- the [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) dataset.</span></span> <span data-ttu-id="49555-105">O modelo de classificação binária construído prevê se uma gorjeta foi paga ou não por uma corrida. Também discutimos os modelos de regressão e classificação multiclasse que preveem a distribuição das gorjetas pagas.</span><span class="sxs-lookup"><span data-stu-id="49555-105">The binary classification model constructed predicts whether or not a tip is paid for a trip, and models for multiclass classification and regression are also discussed that predict the distribution for the tip amounts paid.</span></span>

<span data-ttu-id="49555-106">O procedimento segue o fluxo de trabalho [TDSP (Processo de Ciência de Dados de Equipe)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) .</span><span class="sxs-lookup"><span data-stu-id="49555-106">The procedure follows the [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) workflow.</span></span> <span data-ttu-id="49555-107">Mostramos como configurar um ambiente de ciência de dados, como carregar os dados no SQL DW e como usar o SQL DW ou um Notebook IPython para explorar os dados e os recursos de engenharia para modelagem.</span><span class="sxs-lookup"><span data-stu-id="49555-107">We show how to setup a data science environment, how to load the data into SQL DW, and how use either SQL DW or an IPython Notebook to explore the data and engineer features to model.</span></span> <span data-ttu-id="49555-108">Em seguida, mostraremos como compilar e implantar um modelo com o Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="49555-108">We then show how to build and deploy a model with Azure Machine Learning.</span></span>

## <span data-ttu-id="49555-109"><a name="dataset"></a>O conjunto de dados Corridas de Táxi de NYC</span><span class="sxs-lookup"><span data-stu-id="49555-109"><a name="dataset"></a>The NYC Taxi Trips dataset</span></span>
<span data-ttu-id="49555-110">Os dados de Corridas de Táxi de NYC são formados por cerca de 20 GB de arquivos CSV compactados (aproximadamente 48 GB descompactados) que incluem mais de 173 milhões de corridas individuais, com tarifas pagas por cada corrida.</span><span class="sxs-lookup"><span data-stu-id="49555-110">The NYC Taxi Trip data consists of about 20GB of compressed CSV files (~48GB uncompressed), recording more than 173 million individual trips and the fares paid for each trip.</span></span> <span data-ttu-id="49555-111">Cada registro de corrida inclui o local e o horário de saída e chegada, o número da carteira de habilitação do taxista anônimo e o número de medalhão (identificador exclusivo do táxi).</span><span class="sxs-lookup"><span data-stu-id="49555-111">Each trip record includes the pickup and drop-off locations and times, anonymized hack (driver's) license number, and the medallion (taxi’s unique id) number.</span></span> <span data-ttu-id="49555-112">Os dados abrangem todas as corridas no ano de 2013 e são fornecidos nos dois conjuntos de dados a seguir para cada mês:</span><span class="sxs-lookup"><span data-stu-id="49555-112">The data covers all trips in the year 2013 and is provided in the following two datasets for each month:</span></span>

1. <span data-ttu-id="49555-113">O arquivo **trip_data.csv** contém detalhes da corrida, como o número de passageiros, pontos de saída e chegada, duração e quilometragem da corrida.</span><span class="sxs-lookup"><span data-stu-id="49555-113">The **trip_data.csv** file contains trip details, such as number of passengers, pickup and dropoff points, trip duration, and trip length.</span></span> <span data-ttu-id="49555-114">Aqui estão alguns exemplos de registros:</span><span class="sxs-lookup"><span data-stu-id="49555-114">Here are a few sample records:</span></span>
   
        medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count,trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
2. <span data-ttu-id="49555-115">O arquivo **trip_fare.csv** contém detalhes sobre as tarifas pagas em cada corrida, como tipo de pagamento, valor da tarifa, custos adicionais e impostos, gorjetas e pedágios e o valor total pago.</span><span class="sxs-lookup"><span data-stu-id="49555-115">The **trip_fare.csv** file contains details of the fare paid for each trip, such as payment type, fare amount, surcharge and taxes, tips and tolls, and the total amount paid.</span></span> <span data-ttu-id="49555-116">Aqui estão alguns exemplos de registros:</span><span class="sxs-lookup"><span data-stu-id="49555-116">Here are a few sample records:</span></span>
   
        medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

<span data-ttu-id="49555-117">A **chave exclusiva** para unir trip\_data e trip\_fare é composta pelos três campos a seguir:</span><span class="sxs-lookup"><span data-stu-id="49555-117">The **unique key** used to join trip\_data and trip\_fare is composed of the following three fields:</span></span>

* <span data-ttu-id="49555-118">medallion,</span><span class="sxs-lookup"><span data-stu-id="49555-118">medallion,</span></span>
* <span data-ttu-id="49555-119">hack\_license e</span><span class="sxs-lookup"><span data-stu-id="49555-119">hack\_license and</span></span>
* <span data-ttu-id="49555-120">pickup\_datetime.</span><span class="sxs-lookup"><span data-stu-id="49555-120">pickup\_datetime.</span></span>

## <span data-ttu-id="49555-121"><a name="mltasks"></a>Resolver três tipos de tarefas de previsão</span><span class="sxs-lookup"><span data-stu-id="49555-121"><a name="mltasks"></a>Address three types of prediction tasks</span></span>
<span data-ttu-id="49555-122">Formulamos três problemas de previsão com base em *tip\_amount* para ilustrar três tipos de tarefas de modelagem:</span><span class="sxs-lookup"><span data-stu-id="49555-122">We formulate three prediction problems based on the *tip\_amount* to illustrate three kinds of modeling tasks:</span></span>

1. <span data-ttu-id="49555-123">**Classificação binária**: para prever ou não se uma gorjeta foi paga por uma corrida, ou seja, um *tip\_amount* maior que US$ 0 é um exemplo positivo, enquanto um *tip\_amount* de US$ 0 é um exemplo negativo.</span><span class="sxs-lookup"><span data-stu-id="49555-123">**Binary classification**: To predict whether or not a tip was paid for a trip, i.e. a *tip\_amount* that is greater than $0 is a positive example, while a *tip\_amount* of $0 is a negative example.</span></span>
2. <span data-ttu-id="49555-124">**Classificação multiclasse**: prever o intervalo da gorjetas pagas pela corrida.</span><span class="sxs-lookup"><span data-stu-id="49555-124">**Multiclass classification**: To predict the range of tip paid for the trip.</span></span> <span data-ttu-id="49555-125">Dividimos *tip\_amount* em cinco compartimentos ou classes:</span><span class="sxs-lookup"><span data-stu-id="49555-125">We divide the *tip\_amount* into five bins or classes:</span></span>
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0 and tip_amount <= $5
        Class 2 : tip_amount > $5 and tip_amount <= $10
        Class 3 : tip_amount > $10 and tip_amount <= $20
        Class 4 : tip_amount > $20
3. <span data-ttu-id="49555-126">**Tarefa de regressão**: prever o valor da gorjeta paga por uma corrida.</span><span class="sxs-lookup"><span data-stu-id="49555-126">**Regression task**: To predict the amount of tip paid for a trip.</span></span>  

## <span data-ttu-id="49555-127"><a name="setup"></a>Configurar o ambiente de ciência de dados do Azure para análise avançada</span><span class="sxs-lookup"><span data-stu-id="49555-127"><a name="setup"></a>Set up the Azure data science environment for advanced analytics</span></span>
<span data-ttu-id="49555-128">Para configurar o ambiente de Ciência de Dados do Azure, execute estas etapas:</span><span class="sxs-lookup"><span data-stu-id="49555-128">To set up your Azure Data Science environment, follow these steps.</span></span>

<span data-ttu-id="49555-129">**Crie sua própria conta de armazenamento de blobs do Azure.**</span><span class="sxs-lookup"><span data-stu-id="49555-129">**Create your own Azure blob storage account**</span></span>

* <span data-ttu-id="49555-130">Ao provisionar seu próprio armazenamento de blobs do Azure, escolha uma localização geográfica para ele mais próxima possível do **Centro-Sul dos EUA**, que é onde estão armazenados os dados da NYC Taxi.</span><span class="sxs-lookup"><span data-stu-id="49555-130">When you provision your own Azure blob storage, choose a geo-location for your Azure blob storage in or as close as possible to **South Central US**, which is where the NYC Taxi data is stored.</span></span> <span data-ttu-id="49555-131">Os dados serão copiados usando o AzCopy do contêiner de armazenamento de blobs público para um contêiner em sua própria conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="49555-131">The data will be copied using AzCopy from the public blob storage container to a container in your own storage account.</span></span> <span data-ttu-id="49555-132">Quanto mais próximo seu armazenamento de blobs do Azure estiver do Centro-Sul dos EUA, mais rápido esta tarefa (Etapa 4) será concluída.</span><span class="sxs-lookup"><span data-stu-id="49555-132">The closer your Azure blob storage is to South Central US, the faster this task (Step 4) will be completed.</span></span>
* <span data-ttu-id="49555-133">Para criar sua própria conta de armazenamento do Azure, siga as etapas descritas em [Sobre as contas de armazenamento do Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="49555-133">To create your own Azure storage account, follow the steps outlined at [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="49555-134">Lembre-se de anotar os valores das seguintes credenciais de conta de armazenamento, pois eles serão necessários mais tarde neste passo a passo.</span><span class="sxs-lookup"><span data-stu-id="49555-134">Be sure to make notes on the values for following storage account credentials as they will be needed later in this walkthrough.</span></span>
  
  * <span data-ttu-id="49555-135">**Nome da Conta de Armazenamento**</span><span class="sxs-lookup"><span data-stu-id="49555-135">**Storage Account Name**</span></span>
  * <span data-ttu-id="49555-136">**Chave da conta de armazenamento**</span><span class="sxs-lookup"><span data-stu-id="49555-136">**Storage Account Key**</span></span>
  * <span data-ttu-id="49555-137">**Nome do Contêiner** (no qual você deseja armazenar os dados no armazenamento de blobs do Azure)</span><span class="sxs-lookup"><span data-stu-id="49555-137">**Container Name** (which you want the data to be stored in the Azure blob storage)</span></span>

<span data-ttu-id="49555-138">**Provisione sua instância do Azure SQL DW.**</span><span class="sxs-lookup"><span data-stu-id="49555-138">**Provision your Azure SQL DW instance.**</span></span>
<span data-ttu-id="49555-139">Siga a documentação em [Criar um SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md) para provisionar uma instância do SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="49555-139">Follow the documentation at [Create a SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md) to provision a SQL Data Warehouse instance.</span></span> <span data-ttu-id="49555-140">Lembre-se de fazer anotações sobre as seguintes credenciais do SQL Data Warehouse que serão usadas em etapas posteriores.</span><span class="sxs-lookup"><span data-stu-id="49555-140">Make sure that you make notations on the following SQL Data Warehouse credentials which will be used in later steps.</span></span>

* <span data-ttu-id="49555-141">**Nome do Servidor**: <server Name>.database.windows.net</span><span class="sxs-lookup"><span data-stu-id="49555-141">**Server Name**: <server Name>.database.windows.net</span></span>
* <span data-ttu-id="49555-142">**Nome do SQLDW (Banco de Dados)**</span><span class="sxs-lookup"><span data-stu-id="49555-142">**SQLDW (Database) Name**</span></span>
* <span data-ttu-id="49555-143">**Nome de Usuário**</span><span class="sxs-lookup"><span data-stu-id="49555-143">**Username**</span></span>
* <span data-ttu-id="49555-144">**Senha**</span><span class="sxs-lookup"><span data-stu-id="49555-144">**Password**</span></span>

<span data-ttu-id="49555-145">**Instale o Visual Studio e o SQL Server Data Tools.**</span><span class="sxs-lookup"><span data-stu-id="49555-145">**Install Visual Studio and SQL Server Data Tools.**</span></span> <span data-ttu-id="49555-146">Para obter instruções, confira [Instalar o Visual Studio 2015 e/ou SSDT (SQL Server Data Tools) para o SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-install-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="49555-146">For instructions, see [Install Visual Studio 2015 and/or SSDT (SQL Server Data Tools) for SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-install-visual-studio.md).</span></span>

<span data-ttu-id="49555-147">**Conectar-se ao Azure SQL DW com o Visual Studio.**</span><span class="sxs-lookup"><span data-stu-id="49555-147">**Connect to your Azure SQL DW with Visual Studio.**</span></span> <span data-ttu-id="49555-148">Para obter instruções, veja as etapas 1 e 2 em [Connect to Azure SQL Data Warehouse with Visual Studio (Conectar-se ao SQL Data Warehouse do Azure com o Visual Studio)](../sql-data-warehouse/sql-data-warehouse-connect-overview.md).</span><span class="sxs-lookup"><span data-stu-id="49555-148">For instructions, see steps 1 & 2 in [Connect to Azure SQL Data Warehouse with Visual Studio](../sql-data-warehouse/sql-data-warehouse-connect-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="49555-149">Execute a seguinte consulta SQL no banco de dados que você criou no SQL Data Warehouse (em vez da consulta fornecida na etapa 3 do tópico de conexão) para **criar uma chave mestra**.</span><span class="sxs-lookup"><span data-stu-id="49555-149">Run the following SQL query on the database you created in your SQL Data Warehouse (instead of the query provided in step 3 of the connect topic,) to **create a master key**.</span></span>
> 
> 

    BEGIN TRY
           --Try to create the master key
        CREATE MASTER KEY
    END TRY
    BEGIN CATCH
           --If the master key exists, do nothing
    END CATCH;

<span data-ttu-id="49555-150">**Crie um espaço de trabalho de Azure Machine Learning em sua assinatura do Azure.**</span><span class="sxs-lookup"><span data-stu-id="49555-150">**Create an Azure Machine Learning workspace under your Azure subscription.**</span></span> <span data-ttu-id="49555-151">Para obter instruções, confira [Criar um espaço de trabalho de Azure Machine Learning](machine-learning-create-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="49555-151">For instructions, see [Create an Azure Machine Learning workspace](machine-learning-create-workspace.md).</span></span>

## <span data-ttu-id="49555-152"><a name="getdata"></a>Carregar os dados no SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="49555-152"><a name="getdata"></a>Load the data into SQL Data Warehouse</span></span>
<span data-ttu-id="49555-153">Abra um console de comando do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="49555-153">Open a Windows PowerShell command console.</span></span> <span data-ttu-id="49555-154">Execute os seguintes comandos do PowerShell para baixar os arquivos de exemplo de script SQL que compartilhamos com você no GitHub para um diretório local especificado com o parâmetro *-DestDir*.</span><span class="sxs-lookup"><span data-stu-id="49555-154">Run the following PowerShell commands to download the example SQL script files that we share with you on GitHub to a local directory that you specify with the parameter *-DestDir*.</span></span> <span data-ttu-id="49555-155">Você pode alterar o valor do parâmetro *-DestDir* para qualquer diretório local.</span><span class="sxs-lookup"><span data-stu-id="49555-155">You can change the value of parameter *-DestDir* to any local directory.</span></span> <span data-ttu-id="49555-156">Se *-DestDir* não existir, ele será criado pelo script do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="49555-156">If *-DestDir* does not exist, it will be created by the PowerShell script.</span></span>

> [!NOTE]
> <span data-ttu-id="49555-157">Talvez seja necessário **Executar como Administrador** ao executar o seguinte script do PowerShell se o *DestDir* precisar de privilégio de Administrador para criação ou gravação.</span><span class="sxs-lookup"><span data-stu-id="49555-157">You might need to **Run as Administrator** when executing the following PowerShell script if your *DestDir* directory needs Administrator privilege to create or to write to it.</span></span>
> 
> 

    $source = "https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/SQLDW/Download_Scripts_SQLDW_Walkthrough.ps1"
    $ps1_dest = "$pwd\Download_Scripts_SQLDW_Walkthrough.ps1"
    $wc = New-Object System.Net.WebClient
    $wc.DownloadFile($source, $ps1_dest)
    .\Download_Scripts_SQLDW_Walkthrough.ps1 –DestDir 'C:\tempSQLDW'

<span data-ttu-id="49555-158">Após a execução bem-sucedida, o diretório de trabalho atual mudará para *-DestDir*.</span><span class="sxs-lookup"><span data-stu-id="49555-158">After successful execution, your current working directory changes to *-DestDir*.</span></span> <span data-ttu-id="49555-159">Você deverá ver uma tela como a mostrada abaixo:</span><span class="sxs-lookup"><span data-stu-id="49555-159">You should be able to see screen like below:</span></span>

![][19]

<span data-ttu-id="49555-160">Em seu *-DestDir*, execute o seguinte script do PowerShell no modo de administrador:</span><span class="sxs-lookup"><span data-stu-id="49555-160">In your *-DestDir*, execute the following PowerShell script in administrator mode:</span></span>

    ./SQLDW_Data_Import.ps1

<span data-ttu-id="49555-161">Quando o script do PowerShell for executado pela primeira vez, você receberá uma solicitação para inserir as informações de seu Azure SQL DW e de sua conta de armazenamento de blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="49555-161">When the PowerShell script runs for the first time, you will be asked to input the information from your Azure SQL DW and your Azure blob storage account.</span></span> <span data-ttu-id="49555-162">Ao concluir a primeira execução deste script do PowerShell, as credenciais inseridas serão gravadas em um arquivo de configuração SQLDW.conf no diretório de trabalho atual.</span><span class="sxs-lookup"><span data-stu-id="49555-162">When this PowerShell script completes running for the first time, the credentials you input will have been written to a configuration file SQLDW.conf in the present working directory.</span></span> <span data-ttu-id="49555-163">A futura execução desse arquivo de script do PowerShell terá a opção de ler todos os parâmetros necessários desse arquivo de configuração.</span><span class="sxs-lookup"><span data-stu-id="49555-163">The future run of this PowerShell script file has the option to read all needed parameters from this configuration file.</span></span> <span data-ttu-id="49555-164">Se você precisar alterar alguns parâmetros, escolha inserir os parâmetros na tela ao receber uma solicitação por meio da exclusão desse arquivo de configuração e inserção dos valores de parâmetros conforme solicitado ou alterar os valores de parâmetro editando o arquivo SQLDW.conf em seu diretório *-DestDir* .</span><span class="sxs-lookup"><span data-stu-id="49555-164">If you need to change some parameters, you can choose to input the parameters on the screen upon prompt by deleting this configuration file and inputting the parameters values as prompted or to change the parameter values by editing the SQLDW.conf file in your *-DestDir* directory.</span></span>

> [!NOTE]
> <span data-ttu-id="49555-165">Para evitar conflitos de nome de esquema com aqueles já existentes em seu Azure SQL DW, ao ler os parâmetros diretamente do arquivo SQLDW.conf, um número aleatório de três dígitos é adicionado ao nome do esquema a partir do arquivo SQLDW.conf como o nome do esquema padrão para cada execução.</span><span class="sxs-lookup"><span data-stu-id="49555-165">In order to avoid schema name conflicts with those that already exist in your Azure SQL DW, when reading parameters directly from the SQLDW.conf file, a 3-digit random number is added to the schema name from the SQLDW.conf file as the default schema name for each run.</span></span> <span data-ttu-id="49555-166">O script do PowerShell pode solicitar um nome de esquema. Esse nome pode ser especificado a critério do usuário.</span><span class="sxs-lookup"><span data-stu-id="49555-166">The PowerShell script may prompt you for a schema name: the name may be specified at user discretion.</span></span>
> 
> 

<span data-ttu-id="49555-167">Esse arquivo de **script do PowerShell** conclui as seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="49555-167">This **PowerShell script** file completes the following tasks:</span></span>

* <span data-ttu-id="49555-168">**Baixa e instala o AzCopy**, caso ele ainda não esteja instalado</span><span class="sxs-lookup"><span data-stu-id="49555-168">**Downloads and installs AzCopy**, if AzCopy is not already installed</span></span>
  
        $AzCopy_path = SearchAzCopy
        if ($AzCopy_path -eq $null){
               Write-Host "AzCopy.exe is not found in C:\Program Files*. Now, start installing AzCopy..." -ForegroundColor "Yellow"
            InstallAzCopy
            $AzCopy_path = SearchAzCopy
        }
            $env_path = $env:Path
            for ($i=0; $i -lt $AzCopy_path.count; $i++){
                if ($AzCopy_path.count -eq 1){
                    $AzCopy_path_i = $AzCopy_path
                } else {
                    $AzCopy_path_i = $AzCopy_path[$i]
                }
                if ($env_path -notlike '*' +$AzCopy_path_i+'*'){
                    Write-Host $AzCopy_path_i 'not in system path, add it...'
                    [Environment]::SetEnvironmentVariable("Path", "$AzCopy_path_i;$env_path", "Machine")
                    $env:Path = [System.Environment]::GetEnvironmentVariable("Path","Machine")
                    $env_path = $env:Path
                }
* <span data-ttu-id="49555-169">**Copia dados para sua conta de armazenamento de blobs particular** com o blob público com AzCopy</span><span class="sxs-lookup"><span data-stu-id="49555-169">**Copies data to your private blob storage account** from the public blob with AzCopy</span></span>
  
        Write-Host "AzCopy is copying data from public blob to yo storage account. It may take a while..." -ForegroundColor "Yellow"
        $start_time = Get-Date
        AzCopy.exe /Source:$Source /Dest:$DestURL /DestKey:$StorageAccountKey /S
        $end_time = Get-Date
        $time_span = $end_time - $start_time
        $total_seconds = [math]::Round($time_span.TotalSeconds,2)
        Write-Host "AzCopy finished copying data. Please check your storage account to verify." -ForegroundColor "Yellow"
        Write-Host "This step (copying data from public blob to your storage account) takes $total_seconds seconds." -ForegroundColor "Green"
* <span data-ttu-id="49555-170">**Carrega dados usando o Polybase (executando LoadDataToSQLDW.sql) em seu Azure SQL DW** de sua conta de armazenamento de blobs particular com os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="49555-170">**Loads data using Polybase (by executing LoadDataToSQLDW.sql) to your Azure SQL DW** from your private blob storage account with the following commands.</span></span>
  
  * <span data-ttu-id="49555-171">Criar um esquema</span><span class="sxs-lookup"><span data-stu-id="49555-171">Create a schema</span></span>
    
          EXEC (''CREATE SCHEMA {schemaname};'');
  * <span data-ttu-id="49555-172">Criar uma credencial com escopo de banco de dados</span><span class="sxs-lookup"><span data-stu-id="49555-172">Create a database scoped credential</span></span>
    
          CREATE DATABASE SCOPED CREDENTIAL {KeyAlias}
          WITH IDENTITY = ''asbkey'' ,
          Secret = ''{StorageAccountKey}''
  * <span data-ttu-id="49555-173">Criar uma fonte de dados externa para um blob de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="49555-173">Create an external data source for an Azure storage blob</span></span>
    
          CREATE EXTERNAL DATA SOURCE {nyctaxi_trip_storage}
          WITH
          (
              TYPE = HADOOP,
              LOCATION =''wasbs://{ContainerName}@{StorageAccountName}.blob.core.windows.net'',
              CREDENTIAL = {KeyAlias}
          )
          ;
    
          CREATE EXTERNAL DATA SOURCE {nyctaxi_fare_storage}
          WITH
          (
              TYPE = HADOOP,
              LOCATION =''wasbs://{ContainerName}@{StorageAccountName}.blob.core.windows.net'',
              CREDENTIAL = {KeyAlias}
          )
          ;
  * <span data-ttu-id="49555-174">Criar um formato de arquivo externo para um arquivo csv.</span><span class="sxs-lookup"><span data-stu-id="49555-174">Create an external file format for a csv file.</span></span> <span data-ttu-id="49555-175">Os dados não são compactados e os campos são separados pelo caractere de pipe.</span><span class="sxs-lookup"><span data-stu-id="49555-175">Data is uncompressed and fields are separated with the pipe character.</span></span>
    
          CREATE EXTERNAL FILE FORMAT {csv_file_format}
          WITH
          (   
              FORMAT_TYPE = DELIMITEDTEXT,
              FORMAT_OPTIONS  
              (
                  FIELD_TERMINATOR ='','',
                  USE_TYPE_DEFAULT = TRUE
              )
          )
          ;
  * <span data-ttu-id="49555-176">Criar tabelas externas de tarifas e corridas para o conjunto de dados Táxi de NYC na conta de Armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="49555-176">Create external fare and trip tables for NYC taxi dataset in Azure blob storage.</span></span>
    
          CREATE EXTERNAL TABLE {external_nyctaxi_fare}
          (
              medallion varchar(50) not null,
              hack_license varchar(50) not null,
              vendor_id char(3),
              pickup_datetime datetime not null,
              payment_type char(3),
              fare_amount float,
              surcharge float,
              mta_tax float,
              tip_amount float,
              tolls_amount float,
              total_amount float
          )
          with (
              LOCATION    = ''/nyctaxifare/'',
              DATA_SOURCE = {nyctaxi_fare_storage},
              FILE_FORMAT = {csv_file_format},
              REJECT_TYPE = VALUE,
              REJECT_VALUE = 12     
          )  

            CREATE EXTERNAL TABLE {external_nyctaxi_trip}
            (
                   medallion varchar(50) not null,
                   hack_license varchar(50)  not null,
                   vendor_id char(3),
                   rate_code char(3),
                   store_and_fwd_flag char(3),
                   pickup_datetime datetime  not null,
                   dropoff_datetime datetime,
                   passenger_count int,
                   trip_time_in_secs bigint,
                   trip_distance float,
                   pickup_longitude varchar(30),
                   pickup_latitude varchar(30),
                   dropoff_longitude varchar(30),
                   dropoff_latitude varchar(30)
            )
            with (
                LOCATION    = ''/nyctaxitrip/'',
                DATA_SOURCE = {nyctaxi_trip_storage},
                FILE_FORMAT = {csv_file_format},
                REJECT_TYPE = VALUE,
                REJECT_VALUE = 12         
            )

    - <span data-ttu-id="49555-177">Carregar dados das tabelas externas no Armazenamento de Blobs do Azure para o SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="49555-177">Load data from external tables in Azure blob storage to SQL Data Warehouse</span></span>

            CREATE TABLE {schemaname}.{nyctaxi_fare}
            WITH
            (   
                CLUSTERED COLUMNSTORE INDEX,
                DISTRIBUTION = HASH(medallion)
            )
            AS
            SELECT *
            FROM   {external_nyctaxi_fare}
            ;

            CREATE TABLE {schemaname}.{nyctaxi_trip}
            WITH
            (   
                CLUSTERED COLUMNSTORE INDEX,
                DISTRIBUTION = HASH(medallion)
            )
            AS
            SELECT *
            FROM   {external_nyctaxi_trip}
            ;

    - <span data-ttu-id="49555-178">Criar um exemplo de tabela de dados (NYCTaxi_Sample) e inserir dados nela escolhendo consultas SQL nas tabelas de corridas e tarifas.</span><span class="sxs-lookup"><span data-stu-id="49555-178">Create a sample data table (NYCTaxi_Sample) and insert data to it from selecting SQL queries on the trip and fare tables.</span></span> <span data-ttu-id="49555-179">Algumas etapas deste passo a passo precisam usar esse exemplo de tabela.</span><span class="sxs-lookup"><span data-stu-id="49555-179">(Some steps of this walkthrough needs to use this sample table.)</span></span>

            CREATE TABLE {schemaname}.{nyctaxi_sample}
            WITH
            (   
                CLUSTERED COLUMNSTORE INDEX,
                DISTRIBUTION = HASH(medallion)
            )
            AS
            (
                SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount, f.total_amount, f.tip_amount,
                tipped = CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END,
                tip_class = CASE
                        WHEN (tip_amount = 0) THEN 0
                        WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
                        WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
                        WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
                        ELSE 4
                    END
                FROM {schemaname}.{nyctaxi_trip} t, {schemaname}.{nyctaxi_fare} f
                WHERE datepart("mi",t.pickup_datetime) = 1
                AND t.medallion = f.medallion
                AND   t.hack_license = f.hack_license
                AND   t.pickup_datetime = f.pickup_datetime
                AND   pickup_longitude <> ''0''
                AND   dropoff_longitude <> ''0''
            )
            ;

<span data-ttu-id="49555-180">A localização geográfica de suas contas de armazenamento afeta os tempos de carregamento.</span><span class="sxs-lookup"><span data-stu-id="49555-180">The geographic location of your storage accounts affects load times.</span></span>

> [!NOTE]
> <span data-ttu-id="49555-181">Dependendo da localização geográfica de sua conta de armazenamento de blobs particular, o processo de cópia dos dados de um blob público para sua conta de armazenamento particular pode demorar cerca de 15 minutos, ou até mais, e o processo de carregamento de dados de sua conta de armazenamento para seu Azure SQL DW pode demorar 20 minutos ou mais.</span><span class="sxs-lookup"><span data-stu-id="49555-181">Depending on the geographical location of your private blob storage account, the process of copying data from a public blob to your private storage account can take about 15 minutes, or even longer,and the process of loading data from your storage account to your Azure SQL DW could take 20 minutes or longer.</span></span>  
> 
> 

<span data-ttu-id="49555-182">Você precisará decidir o que fazer se tiver arquivos de origem e destino duplicados.</span><span class="sxs-lookup"><span data-stu-id="49555-182">You will have to decide what do if you have duplicate source and destination files.</span></span>

> [!NOTE]
> <span data-ttu-id="49555-183">Se os arquivos .csv a serem copiados do armazenamento de blobs públicos para sua conta de armazenamento de blobs particular já existirem em sua conta de armazenamento de blob particular, o AzCopy perguntará se você deseja substituí-los.</span><span class="sxs-lookup"><span data-stu-id="49555-183">If the .csv files to be copied from the public blob storage to your private blob storage account already exist in your private blob storage account, AzCopy will ask you whether you want to overwrite them.</span></span> <span data-ttu-id="49555-184">Se não quiser substituí-los, digite **n** quando for solicitado.</span><span class="sxs-lookup"><span data-stu-id="49555-184">If you do not want to overwrite them, input **n** when prompted.</span></span> <span data-ttu-id="49555-185">Se quiser substituir **todos** os arquivos, digite **a** quando for solicitado.</span><span class="sxs-lookup"><span data-stu-id="49555-185">If you want to overwrite **all** of them, input **a** when prompted.</span></span> <span data-ttu-id="49555-186">Você também pode inserir **y** para substituí os arquivos .csv individualmente.</span><span class="sxs-lookup"><span data-stu-id="49555-186">You can also input **y** to overwrite .csv files individually.</span></span>
> 
> 

![Plotar nº 21][21]

<span data-ttu-id="49555-188">Você pode usar seus próprios dados.</span><span class="sxs-lookup"><span data-stu-id="49555-188">You can use your own data.</span></span> <span data-ttu-id="49555-189">Se os dados estiverem em seu computador local em seu aplicativo real, você ainda poderá usar o AzCopy para carregar dados locais para seu armazenamento de blobs do Azure particular.</span><span class="sxs-lookup"><span data-stu-id="49555-189">If your data is in your on-premises machine in your real life application, you can still use AzCopy to upload on-premises data to your private Azure blob storage.</span></span> <span data-ttu-id="49555-190">Você só precisará alterar o local de **Origem**, `$Source = "http://getgoing.blob.core.windows.net/public/nyctaxidataset"`, no comando AzCopy do arquivo de script do PowerShell para um diretório local que contenha seus dados.</span><span class="sxs-lookup"><span data-stu-id="49555-190">You only need to change the **Source** location, `$Source = "http://getgoing.blob.core.windows.net/public/nyctaxidataset"`, in the AzCopy command of the PowerShell script file to the local directory that contains your data.</span></span>

> [!TIP]
> <span data-ttu-id="49555-191">Se seus dados já estiverem no armazenamento de blobs particular do Azure em seu aplicativo real, ignore a etapa do AzCopy no script do PowerShell e carregue os dados diretamente no Azure SQL DW.</span><span class="sxs-lookup"><span data-stu-id="49555-191">If your data is already in your private Azure blob storage in your real life application, you can skip the AzCopy step in the PowerShell script and directly upload the data to Azure SQL DW.</span></span> <span data-ttu-id="49555-192">Isso exigirá mais edições do script para ajustá-lo para o formato de seus dados.</span><span class="sxs-lookup"><span data-stu-id="49555-192">This will require additional edits of the script to tailor it to the format of your data.</span></span>
> 
> 

<span data-ttu-id="49555-193">Este script do Powershell também conecta as informações do Azure SQL DW aos arquivos de exemplo de exploração de dados SQLDW_Explorations.sql, SQLDW_Explorations.ipynb e SQLDW_Explorations_Scripts.py de modo que esses três arquivos estejam prontos para experimentação imediatamente após a conclusão do script do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="49555-193">This Powershell script also plugs in the Azure SQL DW information into the data exploration example files SQLDW_Explorations.sql, SQLDW_Explorations.ipynb, and SQLDW_Explorations_Scripts.py so that these three files are ready to be tried out instantly after the PowerShell script completes.</span></span>

<span data-ttu-id="49555-194">Após a execução bem-sucedida, você verá uma tela parecida com a seguinte:</span><span class="sxs-lookup"><span data-stu-id="49555-194">After a successful execution, you will see screen like below:</span></span>

![][20]

## <span data-ttu-id="49555-195"><a name="dbexplore"></a>Exploração de dados e engenharia de recursos no SQL Data Warehouse do Azure</span><span class="sxs-lookup"><span data-stu-id="49555-195"><a name="dbexplore"></a>Data exploration and feature engineering in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="49555-196">Nesta seção, executamos a exploração de dados e a geração de recursos por meio da execução de consultas SQL no Azure SQL DW usando diretamente o **Visual Studio Data Tools**.</span><span class="sxs-lookup"><span data-stu-id="49555-196">In this section, we perform data exploration and feature generation by running SQL queries against Azure SQL DW directly using **Visual Studio Data Tools**.</span></span> <span data-ttu-id="49555-197">Todas as consultas SQL usadas nesta seção podem ser encontradas no exemplo de script chamado *SQLDW_Explorations.sql*.</span><span class="sxs-lookup"><span data-stu-id="49555-197">All SQL queries used in this section can be found in the sample script named *SQLDW_Explorations.sql*.</span></span> <span data-ttu-id="49555-198">Esse arquivo já foi baixado em seu diretório local pelo script do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="49555-198">This file has already been downloaded to your local directory by the PowerShell script.</span></span> <span data-ttu-id="49555-199">Você também pode recuperá-lo no [GitHub](https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/SQLDW/SQLDW_Explorations.sql).</span><span class="sxs-lookup"><span data-stu-id="49555-199">You can also retrieve it from [GitHub](https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/SQLDW/SQLDW_Explorations.sql).</span></span> <span data-ttu-id="49555-200">Mas o arquivo no GitHub não tem as informações do Azure SQL DW conectadas.</span><span class="sxs-lookup"><span data-stu-id="49555-200">But the file in GitHub does not have the Azure SQL DW information plugged in.</span></span>

<span data-ttu-id="49555-201">Conecte-se ao seu Azure SQL DW usando o Visual Studio com o nome e senha de logon do SQL DW e abra o **Pesquisador de Objetos do SQL** para confirmar se o banco de dados e as tabelas foram importados.</span><span class="sxs-lookup"><span data-stu-id="49555-201">Connect to your Azure SQL DW using Visual Studio with the SQL DW login name and password and open up the **SQL Object Explorer** to confirm the database and tables have been imported.</span></span> <span data-ttu-id="49555-202">Recupere o arquivo *SQLDW_Explorations.sql*.</span><span class="sxs-lookup"><span data-stu-id="49555-202">Retrieve the *SQLDW_Explorations.sql* file.</span></span>

> [!NOTE]
> <span data-ttu-id="49555-203">Para abrir um editor de consultas do PDW (Parallel Data Warehouse), use o comando **Nova Consulta** com seu PDW selecionado no **Pesquisador de Objetos do SQL**.</span><span class="sxs-lookup"><span data-stu-id="49555-203">To open a Parallel Data Warehouse (PDW) query editor, use the **New Query** command while your PDW is selected in the **SQL Object Explorer**.</span></span> <span data-ttu-id="49555-204">O editor de consulta SQL padrão não tem suporte do PDW.</span><span class="sxs-lookup"><span data-stu-id="49555-204">The standard SQL query editor is not supported by PDW.</span></span>
> 
> 

<span data-ttu-id="49555-205">Veja a seguir os tipos de tarefas de exploração de dados e de geração de recursos executados nesta seção:</span><span class="sxs-lookup"><span data-stu-id="49555-205">Here are the type of data exploration and feature generation tasks performed in this section:</span></span>

* <span data-ttu-id="49555-206">Explorar as distribuições de dados de alguns campos em períodos diferentes.</span><span class="sxs-lookup"><span data-stu-id="49555-206">Explore data distributions of a few fields in varying time windows.</span></span>
* <span data-ttu-id="49555-207">Investigar a qualidade dos dados dos campos de longitude e latitude.</span><span class="sxs-lookup"><span data-stu-id="49555-207">Investigate data quality of the longitude and latitude fields.</span></span>
* <span data-ttu-id="49555-208">Gerar rótulos de classificação binária e multiclasse com base em **tip\_amount**.</span><span class="sxs-lookup"><span data-stu-id="49555-208">Generate binary and multiclass classification labels based on the **tip\_amount**.</span></span>
* <span data-ttu-id="49555-209">Gerar recursos e computar/comparar as distâncias de viagem.</span><span class="sxs-lookup"><span data-stu-id="49555-209">Generate features and compute/compare trip distances.</span></span>
* <span data-ttu-id="49555-210">Unir as duas tabelas e extrair uma amostra aleatória que será usada para compilar modelos.</span><span class="sxs-lookup"><span data-stu-id="49555-210">Join the two tables and extract a random sample that will be used to build models.</span></span>

### <a name="data-import-verification"></a><span data-ttu-id="49555-211">Verificação de importação de dados</span><span class="sxs-lookup"><span data-stu-id="49555-211">Data import verification</span></span>
<span data-ttu-id="49555-212">Essas consultas fornecem uma verificação rápida do número de linhas e colunas nas tabelas que foram preenchidas anteriormente usando a importação em massa paralela do Polybase,</span><span class="sxs-lookup"><span data-stu-id="49555-212">These queries provide a quick verification of the number of rows and columns in the tables populated earlier using Polybase's parallel bulk import,</span></span>

    -- Report number of rows in table <nyctaxi_trip> without table scan
    SELECT SUM(rows) FROM sys.partitions WHERE object_id = OBJECT_ID('<schemaname>.<nyctaxi_trip>')

    -- Report number of columns in table <nyctaxi_trip>
    SELECT COUNT(*) FROM information_schema.columns WHERE table_name = '<nyctaxi_trip>' AND table_schema = '<schemaname>'

<span data-ttu-id="49555-213">**Saída:** o resultado deve ser 173.179.759 linhas e 14 colunas.</span><span class="sxs-lookup"><span data-stu-id="49555-213">**Output:** You should get 173,179,759 rows and 14 columns.</span></span>

### <a name="exploration-trip-distribution-by-medallion"></a><span data-ttu-id="49555-214">Exploração: distribuição de corridas por licença</span><span class="sxs-lookup"><span data-stu-id="49555-214">Exploration: Trip distribution by medallion</span></span>
<span data-ttu-id="49555-215">Este exemplo de consulta identifica os medalhões (números de táxi) com mais de 100 corridas dentro de um determinado período.</span><span class="sxs-lookup"><span data-stu-id="49555-215">This example query identifies the medallions (taxi numbers) that completed more than 100 trips within a specified time period.</span></span> <span data-ttu-id="49555-216">A consulta aproveitaria o acesso à tabela particionada, já que é condicionada pelo esquema de partição de **pickup\_datetime**.</span><span class="sxs-lookup"><span data-stu-id="49555-216">The query would benefit from the partitioned table access since it is conditioned by the partition scheme of **pickup\_datetime**.</span></span> <span data-ttu-id="49555-217">Consultar o conjunto de dados completo também usará a tabela particionada e/ou a verificação de índice.</span><span class="sxs-lookup"><span data-stu-id="49555-217">Querying the full dataset will also make use of the partitioned table and/or index scan.</span></span>

    SELECT medallion, COUNT(*)
    FROM <schemaname>.<nyctaxi_fare>
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    GROUP BY medallion
    HAVING COUNT(*) > 100

<span data-ttu-id="49555-218">**Saída:** a consulta deve retornar uma tabela com linhas especificando os 13.369 medalhões (táxis) e o número de viagens concluídas por eles em 2013.</span><span class="sxs-lookup"><span data-stu-id="49555-218">**Output:** The query should return a table with rows specifying the 13,369 medallions (taxis) and the number of trip completed by them in 2013.</span></span> <span data-ttu-id="49555-219">A última coluna contém o número de viagens concluídas.</span><span class="sxs-lookup"><span data-stu-id="49555-219">The last column contains the count of the number of trips completed.</span></span>

### <a name="exploration-trip-distribution-by-medallion-and-hacklicense"></a><span data-ttu-id="49555-220">Exploração: distribuição de corridas por medallion e hack_license</span><span class="sxs-lookup"><span data-stu-id="49555-220">Exploration: Trip distribution by medallion and hack_license</span></span>
<span data-ttu-id="49555-221">Este exemplo identifica os medalhões (números de táxi) e números de hack_license (motoristas) com mais de 100 corridas dentro de um determinado período.</span><span class="sxs-lookup"><span data-stu-id="49555-221">This example identifies the medallions (taxi numbers) and hack_license numbers (drivers) that completed more than 100 trips within a specified time period.</span></span>

    SELECT medallion, hack_license, COUNT(*)
    FROM <schemaname>.<nyctaxi_fare>
    WHERE pickup_datetime BETWEEN '20130101' AND '20130131'
    GROUP BY medallion, hack_license
    HAVING COUNT(*) > 100

<span data-ttu-id="49555-222">**Saída:** a consulta deve retornar uma tabela com 13.369 linhas especificando as 13.369 IDs de carro/motoristas que concluíram mais que 100 corridas em 2013.</span><span class="sxs-lookup"><span data-stu-id="49555-222">**Output:** The query should return a table with 13,369 rows specifying the 13,369 car/driver IDs that have completed more that 100 trips in 2013.</span></span> <span data-ttu-id="49555-223">A última coluna contém o número de viagens concluídas.</span><span class="sxs-lookup"><span data-stu-id="49555-223">The last column contains the count of the number of trips completed.</span></span>

### <a name="data-quality-assessment-verify-records-with-incorrect-longitude-andor-latitude"></a><span data-ttu-id="49555-224">Avaliação de qualidade de dados: verificar registros com longitude e/ou latitude incorretos</span><span class="sxs-lookup"><span data-stu-id="49555-224">Data quality assessment: Verify records with incorrect longitude and/or latitude</span></span>
<span data-ttu-id="49555-225">Este exemplo investiga se qualquer um dos campos longitude e/ou latitude contém um valor inválido (graus radianos devem estar entre -90 e 90), ou tiver coordenadas (0, 0).</span><span class="sxs-lookup"><span data-stu-id="49555-225">This example investigates if any of the longitude and/or latitude fields either contain an invalid value (radian degrees should be between -90 and 90), or have (0, 0) coordinates.</span></span>

    SELECT COUNT(*) FROM <schemaname>.<nyctaxi_trip>
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    AND  (CAST(pickup_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(pickup_latitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_latitude AS float) NOT BETWEEN -90 AND 90
    OR    (pickup_longitude = '0' AND pickup_latitude = '0')
    OR    (dropoff_longitude = '0' AND dropoff_latitude = '0'))

<span data-ttu-id="49555-226">**Saída:** a consulta retorna 837.467 corridas que têm campos de longitude e/ou latitude inválidos.</span><span class="sxs-lookup"><span data-stu-id="49555-226">**Output:** The query returns 837,467 trips that have invalid longitude and/or latitude fields.</span></span>

### <a name="exploration-tipped-vs-not-tipped-trips-distribution"></a><span data-ttu-id="49555-227">Exploração: distribuição de corridas com gorjeta versus sem gorjeta</span><span class="sxs-lookup"><span data-stu-id="49555-227">Exploration: Tipped vs. not tipped trips distribution</span></span>
<span data-ttu-id="49555-228">Este exemplo localiza o número de corridas que receberam gorjetas em comparação com aquelas que não receberam em um determinado período (ou no conjunto de dados completo, se envolver o ano inteiro conforme configurado aqui).</span><span class="sxs-lookup"><span data-stu-id="49555-228">This example finds the number of trips that were tipped vs. the number that were not tipped in a specified time period (or in the full dataset if covering the full year as it is set up here).</span></span> <span data-ttu-id="49555-229">Essa distribuição reflete a distribuição de rótulo binário a ser usado posteriormente para modelagem de classificação binária.</span><span class="sxs-lookup"><span data-stu-id="49555-229">This distribution reflects the binary label distribution to be later used for binary classification modeling.</span></span>

    SELECT tipped, COUNT(*) AS tip_freq FROM (
      SELECT CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END AS tipped, tip_amount
      FROM <schemaname>.<nyctaxi_fare>
      WHERE pickup_datetime BETWEEN '20130101' AND '20131231') tc
    GROUP BY tipped

<span data-ttu-id="49555-230">**Saída:** a consulta deve retornar as seguintes frequências de gorjeta para o ano de 2013: 90.447.622 com gorjeta e 82.264.709 sem gorjeta.</span><span class="sxs-lookup"><span data-stu-id="49555-230">**Output:** The query should return the following tip frequencies for the year 2013: 90,447,622 tipped and 82,264,709 not-tipped.</span></span>

### <a name="exploration-tip-classrange-distribution"></a><span data-ttu-id="49555-231">Exploração: distribuição de classe/intervalo de gorjetas</span><span class="sxs-lookup"><span data-stu-id="49555-231">Exploration: Tip class/range distribution</span></span>
<span data-ttu-id="49555-232">Esse exemplo calcula a distribuição dos intervalos de gorjetas em um determinado período de tempo (ou no conjunto de dados completo se abrangendo todo o ano).</span><span class="sxs-lookup"><span data-stu-id="49555-232">This example computes the distribution of tip ranges in a given time period (or in the full dataset if covering the full year).</span></span> <span data-ttu-id="49555-233">Essa é a distribuição das classes de rótulo que serão usados posteriormente para a modelagem de classificação multiclasse.</span><span class="sxs-lookup"><span data-stu-id="49555-233">This is the distribution of the label classes that will be used later for multiclass classification modeling.</span></span>

    SELECT tip_class, COUNT(*) AS tip_freq FROM (
        SELECT CASE
            WHEN (tip_amount = 0) THEN 0
            WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
            WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
            WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
            ELSE 4
        END AS tip_class
    FROM <schemaname>.<nyctaxi_fare>
    WHERE pickup_datetime BETWEEN '20130101' AND '20131231') tc
    GROUP BY tip_class

<span data-ttu-id="49555-234">**Saída:**</span><span class="sxs-lookup"><span data-stu-id="49555-234">**Output:**</span></span>

| <span data-ttu-id="49555-235">tip_class</span><span class="sxs-lookup"><span data-stu-id="49555-235">tip_class</span></span> | <span data-ttu-id="49555-236">tip_freq</span><span class="sxs-lookup"><span data-stu-id="49555-236">tip_freq</span></span> |
| --- | --- |
| <span data-ttu-id="49555-237">1</span><span class="sxs-lookup"><span data-stu-id="49555-237">1</span></span> |<span data-ttu-id="49555-238">82230915</span><span class="sxs-lookup"><span data-stu-id="49555-238">82230915</span></span> |
| <span data-ttu-id="49555-239">2</span><span class="sxs-lookup"><span data-stu-id="49555-239">2</span></span> |<span data-ttu-id="49555-240">6198803</span><span class="sxs-lookup"><span data-stu-id="49555-240">6198803</span></span> |
| <span data-ttu-id="49555-241">3</span><span class="sxs-lookup"><span data-stu-id="49555-241">3</span></span> |<span data-ttu-id="49555-242">1932223</span><span class="sxs-lookup"><span data-stu-id="49555-242">1932223</span></span> |
| <span data-ttu-id="49555-243">0</span><span class="sxs-lookup"><span data-stu-id="49555-243">0</span></span> |<span data-ttu-id="49555-244">82264625</span><span class="sxs-lookup"><span data-stu-id="49555-244">82264625</span></span> |
| <span data-ttu-id="49555-245">4</span><span class="sxs-lookup"><span data-stu-id="49555-245">4</span></span> |<span data-ttu-id="49555-246">85765</span><span class="sxs-lookup"><span data-stu-id="49555-246">85765</span></span> |

### <a name="exploration-compute-and-compare-trip-distance"></a><span data-ttu-id="49555-247">Exploração: calcular e comparar a distância da corrida</span><span class="sxs-lookup"><span data-stu-id="49555-247">Exploration: Compute and compare trip distance</span></span>
<span data-ttu-id="49555-248">Este exemplo converte a longitude e latitude de saída e chegada para pontos geográficos do SQL, calcula a distância de viagem usando a diferença de pontos geográficos do SQL e retorna uma amostra aleatória dos resultados de comparação.</span><span class="sxs-lookup"><span data-stu-id="49555-248">This example converts the pickup and drop-off longitude and latitude to SQL geography points, computes the trip distance using SQL geography points difference, and returns a random sample of the results for comparison.</span></span> <span data-ttu-id="49555-249">O exemplo limita os resultados às coordenadas válidas apenas usando a consulta de avaliação de qualidade de dados abordada anteriormente.</span><span class="sxs-lookup"><span data-stu-id="49555-249">The example limits the results to valid coordinates only using the data quality assessment query covered earlier.</span></span>

    /****** Object:  UserDefinedFunction [dbo].[fnCalculateDistance] ******/
    SET ANSI_NULLS ON
    GO

    SET QUOTED_IDENTIFIER ON
    GO

    IF EXISTS (SELECT * FROM sys.objects WHERE type IN ('FN', 'IF') AND name = 'fnCalculateDistance')
      DROP FUNCTION fnCalculateDistance
    GO

    -- User-defined function to calculate the direct distance  in mile between two geographical coordinates.
    CREATE FUNCTION [dbo].[fnCalculateDistance] (@Lat1 float, @Long1 float, @Lat2 float, @Long2 float)

    RETURNS float
    AS
    BEGIN
          DECLARE @distance decimal(28, 10)
          -- Convert to radians
          SET @Lat1 = @Lat1 / 57.2958
          SET @Long1 = @Long1 / 57.2958
          SET @Lat2 = @Lat2 / 57.2958
          SET @Long2 = @Long2 / 57.2958
          -- Calculate distance
          SET @distance = (SIN(@Lat1) * SIN(@Lat2)) + (COS(@Lat1) * COS(@Lat2) * COS(@Long2 - @Long1))
          --Convert to miles
          IF @distance <> 0
          BEGIN
            SET @distance = 3958.75 * ATAN(SQRT(1 - POWER(@distance, 2)) / @distance);
          END
          RETURN @distance
    END
    GO

    SELECT pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude,
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) AS DirectDistance
    FROM <schemaname>.<nyctaxi_trip>
    WHERE datepart("mi",pickup_datetime)=1
    AND CAST(pickup_latitude AS float) BETWEEN -90 AND 90
    AND CAST(dropoff_latitude AS float) BETWEEN -90 AND 90
    AND pickup_longitude != '0' AND dropoff_longitude != '0'

### <a name="feature-engineering-using-sql-functions"></a><span data-ttu-id="49555-250">Engenharia de recursos usando funções SQL</span><span class="sxs-lookup"><span data-stu-id="49555-250">Feature engineering using SQL functions</span></span>
<span data-ttu-id="49555-251">Às vezes, as funções SQL podem ser uma opção eficiente para a engenharia de recursos.</span><span class="sxs-lookup"><span data-stu-id="49555-251">Sometimes SQL functions can be an efficient option for feature engineering.</span></span> <span data-ttu-id="49555-252">Neste passo a passo, definimos uma função SQL para calcular a distância direta entre os locais de saída e chegada.</span><span class="sxs-lookup"><span data-stu-id="49555-252">In this walkthrough, we defined a SQL function to calculate the direct distance between the pickup and dropoff locations.</span></span> <span data-ttu-id="49555-253">Você pode executar os scripts SQL a seguir no **Visual Studio Data Tools**.</span><span class="sxs-lookup"><span data-stu-id="49555-253">You can run the following SQL scripts in **Visual Studio Data Tools**.</span></span>

<span data-ttu-id="49555-254">Este é o script SQL que define a função de distância.</span><span class="sxs-lookup"><span data-stu-id="49555-254">Here is the SQL script that defines the distance function.</span></span>

    SET ANSI_NULLS ON
    GO

    SET QUOTED_IDENTIFIER ON
    GO

    IF EXISTS (SELECT * FROM sys.objects WHERE type IN ('FN', 'IF') AND name = 'fnCalculateDistance')
      DROP FUNCTION fnCalculateDistance
    GO

    -- User-defined function calculate the direct distance between two geographical coordinates.
    CREATE FUNCTION [dbo].[fnCalculateDistance] (@Lat1 float, @Long1 float, @Lat2 float, @Long2 float)

    RETURNS float
    AS
    BEGIN
          DECLARE @distance decimal(28, 10)
          -- Convert to radians
          SET @Lat1 = @Lat1 / 57.2958
          SET @Long1 = @Long1 / 57.2958
          SET @Lat2 = @Lat2 / 57.2958
          SET @Long2 = @Long2 / 57.2958
          -- Calculate distance
          SET @distance = (SIN(@Lat1) * SIN(@Lat2)) + (COS(@Lat1) * COS(@Lat2) * COS(@Long2 - @Long1))
          --Convert to miles
          IF @distance <> 0
          BEGIN
            SET @distance = 3958.75 * ATAN(SQRT(1 - POWER(@distance, 2)) / @distance);
          END
          RETURN @distance
    END
    GO

<span data-ttu-id="49555-255">Veja um exemplo para chamar essa função a fim de gerar recursos em sua consulta SQL:</span><span class="sxs-lookup"><span data-stu-id="49555-255">Here is an example to call this function to generate features in your SQL query:</span></span>

    -- Sample query to call the function to create features
    SELECT pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude,
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) AS DirectDistance
    FROM <schemaname>.<nyctaxi_trip>
    WHERE datepart("mi",pickup_datetime)=1
    AND CAST(pickup_latitude AS float) BETWEEN -90 AND 90
    AND CAST(dropoff_latitude AS float) BETWEEN -90 AND 90
    AND pickup_longitude != '0' AND dropoff_longitude != '0'

<span data-ttu-id="49555-256">**Saída:** esta consulta gera uma tabela (com 2.803.538 linhas) com latitudes e longitudes de saída e chegada e as distâncias diretas correspondentes em milhas.</span><span class="sxs-lookup"><span data-stu-id="49555-256">**Output:** This query generates a table (with 2,803,538 rows) with pickup and dropoff latitudes and longitudes and the corresponding direct distances in miles.</span></span> <span data-ttu-id="49555-257">Estes são os resultados para as primeiras 3 linhas:</span><span class="sxs-lookup"><span data-stu-id="49555-257">Here are the results for first 3 rows:</span></span>

|  | <span data-ttu-id="49555-258">pickup_latitude</span><span class="sxs-lookup"><span data-stu-id="49555-258">pickup_latitude</span></span> | <span data-ttu-id="49555-259">pickup_longitude</span><span class="sxs-lookup"><span data-stu-id="49555-259">pickup_longitude</span></span> | <span data-ttu-id="49555-260">dropoff_latitude</span><span class="sxs-lookup"><span data-stu-id="49555-260">dropoff_latitude</span></span> | <span data-ttu-id="49555-261">dropoff_longitude</span><span class="sxs-lookup"><span data-stu-id="49555-261">dropoff_longitude</span></span> | <span data-ttu-id="49555-262">DirectDistance</span><span class="sxs-lookup"><span data-stu-id="49555-262">DirectDistance</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="49555-263">1</span><span class="sxs-lookup"><span data-stu-id="49555-263">1</span></span> |<span data-ttu-id="49555-264">40.731804</span><span class="sxs-lookup"><span data-stu-id="49555-264">40.731804</span></span> |<span data-ttu-id="49555-265">-74.001083</span><span class="sxs-lookup"><span data-stu-id="49555-265">-74.001083</span></span> |<span data-ttu-id="49555-266">40.736622</span><span class="sxs-lookup"><span data-stu-id="49555-266">40.736622</span></span> |<span data-ttu-id="49555-267">-73.988953</span><span class="sxs-lookup"><span data-stu-id="49555-267">-73.988953</span></span> |<span data-ttu-id="49555-268">.7169601222</span><span class="sxs-lookup"><span data-stu-id="49555-268">.7169601222</span></span> |
| <span data-ttu-id="49555-269">2</span><span class="sxs-lookup"><span data-stu-id="49555-269">2</span></span> |<span data-ttu-id="49555-270">40.715794</span><span class="sxs-lookup"><span data-stu-id="49555-270">40.715794</span></span> |<span data-ttu-id="49555-271">-74,010635</span><span class="sxs-lookup"><span data-stu-id="49555-271">-74,010635</span></span> |<span data-ttu-id="49555-272">40.725338</span><span class="sxs-lookup"><span data-stu-id="49555-272">40.725338</span></span> |<span data-ttu-id="49555-273">-74.00399</span><span class="sxs-lookup"><span data-stu-id="49555-273">-74.00399</span></span> |<span data-ttu-id="49555-274">.7448343721</span><span class="sxs-lookup"><span data-stu-id="49555-274">.7448343721</span></span> |
| <span data-ttu-id="49555-275">3</span><span class="sxs-lookup"><span data-stu-id="49555-275">3</span></span> |<span data-ttu-id="49555-276">40.761456</span><span class="sxs-lookup"><span data-stu-id="49555-276">40.761456</span></span> |<span data-ttu-id="49555-277">-73.999886</span><span class="sxs-lookup"><span data-stu-id="49555-277">-73.999886</span></span> |<span data-ttu-id="49555-278">40.766544</span><span class="sxs-lookup"><span data-stu-id="49555-278">40.766544</span></span> |<span data-ttu-id="49555-279">-73.988228</span><span class="sxs-lookup"><span data-stu-id="49555-279">-73.988228</span></span> |<span data-ttu-id="49555-280">0.7037227967</span><span class="sxs-lookup"><span data-stu-id="49555-280">0.7037227967</span></span> |

### <a name="prepare-data-for-model-building"></a><span data-ttu-id="49555-281">Preparar dados para criação de modelo</span><span class="sxs-lookup"><span data-stu-id="49555-281">Prepare data for model building</span></span>
<span data-ttu-id="49555-282">A consulta a seguir une as tabelas **nyctaxi\_trip** e **nyctaxi\_fare**, gera um rótulo de classificação binária **tipped**, um rótulo de classificação de multiclasse **tip\_class** e extrai um exemplo do conjunto de dados totalmente unido.</span><span class="sxs-lookup"><span data-stu-id="49555-282">The following query joins the **nyctaxi\_trip** and **nyctaxi\_fare** tables, generates a binary classification label **tipped**, a multi-class classification label **tip\_class**, and extracts a sample from the full joined dataset.</span></span> <span data-ttu-id="49555-283">A amostragem é feita recuperando um subconjunto das viagens com base na hora de saída.</span><span class="sxs-lookup"><span data-stu-id="49555-283">The sampling is done by retrieving a subset of the trips based on pickup time.</span></span>  <span data-ttu-id="49555-284">Essa consulta pode ser copiada e colada diretamente no módulo [Importar Dados][import-data] do [Azure Machine Learning Studio](https://studio.azureml.net) para ingestão de dados direta da instância do Banco de Dados SQL no Azure.</span><span class="sxs-lookup"><span data-stu-id="49555-284">This query can be copied then pasted directly in the [Azure Machine Learning Studio](https://studio.azureml.net) [Import Data][import-data] module for direct data ingestion from the SQL database instance in Azure.</span></span> <span data-ttu-id="49555-285">A consulta exclui registros com coordenadas incorretas (0, 0).</span><span class="sxs-lookup"><span data-stu-id="49555-285">The query excludes records with incorrect (0, 0) coordinates.</span></span>

    SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount,     f.total_amount, f.tip_amount,
        CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END AS tipped,
        CASE WHEN (tip_amount = 0) THEN 0
            WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
            WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
            WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
            ELSE 4
        END AS tip_class
    FROM <schemaname>.<nyctaxi_trip> t, <schemaname>.<nyctaxi_fare> f
    WHERE datepart("mi",t.pickup_datetime) = 1
    AND   t.medallion = f.medallion
    AND   t.hack_license = f.hack_license
    AND   t.pickup_datetime = f.pickup_datetime
    AND   pickup_longitude != '0' AND dropoff_longitude != '0'

<span data-ttu-id="49555-286">Quando você estiver pronto para prosseguir para o Azure Machine Learning, você pode:</span><span class="sxs-lookup"><span data-stu-id="49555-286">When you are ready to proceed to Azure Machine Learning, you may either:</span></span>  

1. <span data-ttu-id="49555-287">Salve a consulta SQL final para extrair os dados de exemplo e copiar e colar a consulta diretamente em um módulo [Importar Dados][import-data] no Azure Machine Learning ou</span><span class="sxs-lookup"><span data-stu-id="49555-287">Save the final SQL query to extract and sample the data and copy-paste the query directly into a [Import Data][import-data] module in Azure Machine Learning, or</span></span>
2. <span data-ttu-id="49555-288">Mantenha os dados de amostra e projetados que você planeja usar para criar modelos em uma nova tabela do SQL DW e use a nova tabela no módulo [Importar Dados][import-data] no Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="49555-288">Persist the sampled and engineered data you plan to use for model building in a new SQL DW table and use the new table in the [Import Data][import-data] module in Azure Machine Learning.</span></span> <span data-ttu-id="49555-289">O script do PowerShell na etapa anterior fez isso para você.</span><span class="sxs-lookup"><span data-stu-id="49555-289">The PowerShell script in earlier step has done this for you.</span></span> <span data-ttu-id="49555-290">Você pode ler diretamente dessa tabela no módulo Importar Dados.</span><span class="sxs-lookup"><span data-stu-id="49555-290">You can read directly from this table in the Import Data module.</span></span>

## <span data-ttu-id="49555-291"><a name="ipnb"></a>Exploração de dados e engenharia de recursos no IPython Notebook</span><span class="sxs-lookup"><span data-stu-id="49555-291"><a name="ipnb"></a>Data exploration and feature engineering in IPython notebook</span></span>
<span data-ttu-id="49555-292">Nesta seção, realizaremos a exploração de dados e a geração de recursos executando consultas SQL e Python no SQL DW criado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="49555-292">In this section, we will perform data exploration and feature generation using both Python and SQL queries against the SQL DW created earlier.</span></span> <span data-ttu-id="49555-293">Um exemplo de notebook IPython chamado **SQLDW_Explorations.ipynb** e um arquivo de script Python **SQLDW_Explorations_Scripts.py** foram baixados no diretório local.</span><span class="sxs-lookup"><span data-stu-id="49555-293">A sample IPython notebook named **SQLDW_Explorations.ipynb** and a Python script file **SQLDW_Explorations_Scripts.py** have been downloaded to your local directory.</span></span> <span data-ttu-id="49555-294">Eles também estão disponíveis no [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/SQLDW).</span><span class="sxs-lookup"><span data-stu-id="49555-294">They are also available on [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/SQLDW).</span></span> <span data-ttu-id="49555-295">Esses dois arquivos são idênticos em scripts Python.</span><span class="sxs-lookup"><span data-stu-id="49555-295">These two files are identical in Python scripts.</span></span> <span data-ttu-id="49555-296">O arquivo de script Python é fornecido a você caso você não tenha um servidor do Notebook IPython.</span><span class="sxs-lookup"><span data-stu-id="49555-296">The Python script file is provided to you in case you do not have an IPython Notebook server.</span></span> <span data-ttu-id="49555-297">Esses dois de exemplo de arquivo Python são criados no **Python 2.7**.</span><span class="sxs-lookup"><span data-stu-id="49555-297">These two sample Python files are designed under **Python 2.7**.</span></span>

<span data-ttu-id="49555-298">As informações necessárias do Azure SQL DW no exemplo de Notebook IPython e o arquivo de script Python baixados em seu computador local foram conectados anteriormente pelo script do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="49555-298">The needed Azure SQL DW information in the sample IPython Notebook and the Python script file downloaded to your local machine has been plugged in by the PowerShell script previously.</span></span> <span data-ttu-id="49555-299">Eles são executáveis sem qualquer modificação.</span><span class="sxs-lookup"><span data-stu-id="49555-299">They are executable without any modification.</span></span>

<span data-ttu-id="49555-300">Se você já tiver configurado um espaço de trabalho do AzureML, carregue diretamente o exemplo de Notebook IPython no serviço do Notebook IPython do AzureML e comece a executá-lo.</span><span class="sxs-lookup"><span data-stu-id="49555-300">If you have already set up an AzureML workspace, you can directly upload the sample IPython Notebook to the AzureML IPython Notebook service and start running it.</span></span> <span data-ttu-id="49555-301">Estas são as etapas para carregar no serviço Notebook IPython do AzureML:</span><span class="sxs-lookup"><span data-stu-id="49555-301">Here are the steps to upload to AzureML IPython Notebook service:</span></span>

1. <span data-ttu-id="49555-302">Faça logon em seu espaço de trabalho do AzureML, clique em "Studio" na parte superior e clique em "NOTEBOOKS" no lado esquerdo da página Web.</span><span class="sxs-lookup"><span data-stu-id="49555-302">Log in to your AzureML workspace, click "Studio" at the top, and click "NOTEBOOKS" on the left side of the web page.</span></span>
   
    ![Plotar nº 22][22]
2. <span data-ttu-id="49555-304">Clique em "NOVO" no canto inferior esquerdo da página Web e selecione "Python 2".</span><span class="sxs-lookup"><span data-stu-id="49555-304">Click "NEW" on the left bottom corner of the web page, and select "Python 2".</span></span> <span data-ttu-id="49555-305">Em seguida, forneça um nome para o notebook e clique na marca de seleção para criar o novo Notebook IPython em branco.</span><span class="sxs-lookup"><span data-stu-id="49555-305">Then, provide a name to the notebook and click the check mark to create the new blank IPython Notebook.</span></span>
   
    ![Plotar nº 23][23]
3. <span data-ttu-id="49555-307">Clique no símbolo "Jupyter" no canto superior esquerdo do novo Notebook IPython.</span><span class="sxs-lookup"><span data-stu-id="49555-307">Click the "Jupyter" symbol on the left top corner of the new IPython Notebook.</span></span>
   
    ![Plotar nº 24][24]
4. <span data-ttu-id="49555-309">Arraste e solte o exemplo de Notebook IPython na página de **árvore** de seu serviço Notebook IPython do AzureML e clique em **Carregar**.</span><span class="sxs-lookup"><span data-stu-id="49555-309">Drag and drop the sample IPython Notebook to the **tree** page of your AzureML IPython Notebook service, and click **Upload**.</span></span> <span data-ttu-id="49555-310">Em seguida, o exemplo de Notebook IPython será carregado no serviço de Notebook IPython do AzureML.</span><span class="sxs-lookup"><span data-stu-id="49555-310">Then, the sample IPython Notebook will be uploaded to the AzureML IPython Notebook service.</span></span>
   
    ![Plotar nº 25][25]

<span data-ttu-id="49555-312">Para executar o exemplo de Notebook IPython ou o arquivo de script Python, os seguintes pacotes Python serão necessários.</span><span class="sxs-lookup"><span data-stu-id="49555-312">In order to run the sample IPython Notebook or the Python script file, the following Python packages are needed.</span></span> <span data-ttu-id="49555-313">Se você estiver usando o serviço de Notebook IPython do AzureML, esses pacotes já foram pré-instalados.</span><span class="sxs-lookup"><span data-stu-id="49555-313">If you are using the AzureML IPython Notebook service, these packages have been pre-installed.</span></span>

    - <span data-ttu-id="49555-314">pandas</span><span class="sxs-lookup"><span data-stu-id="49555-314">pandas</span></span>
    - <span data-ttu-id="49555-315">numpy</span><span class="sxs-lookup"><span data-stu-id="49555-315">numpy</span></span>
    - <span data-ttu-id="49555-316">matplotlib</span><span class="sxs-lookup"><span data-stu-id="49555-316">matplotlib</span></span>
    - <span data-ttu-id="49555-317">pyodbc</span><span class="sxs-lookup"><span data-stu-id="49555-317">pyodbc</span></span>
    - <span data-ttu-id="49555-318">PyTables</span><span class="sxs-lookup"><span data-stu-id="49555-318">PyTables</span></span>

<span data-ttu-id="49555-319">Veja a seguir a sequência recomendada ao criar soluções de análise avançadas no AzureML com grandes volumes de dados:</span><span class="sxs-lookup"><span data-stu-id="49555-319">The recommended sequence when building advanced analytical solutions on AzureML with large data is the following:</span></span>

* <span data-ttu-id="49555-320">Leia em uma pequena amostra dos dados em um quadro de dados na memória.</span><span class="sxs-lookup"><span data-stu-id="49555-320">Read in a small sample of the data into an in-memory data frame.</span></span>
* <span data-ttu-id="49555-321">Execute algumas visualizações e explorações usando os dados de amostrados.</span><span class="sxs-lookup"><span data-stu-id="49555-321">Perform some visualizations and explorations using the sampled data.</span></span>
* <span data-ttu-id="49555-322">Experimente a engenharia de recursos usando os dados amostrados.</span><span class="sxs-lookup"><span data-stu-id="49555-322">Experiment with feature engineering using the sampled data.</span></span>
* <span data-ttu-id="49555-323">Para exploração de volumes maiores de dados, manipulação de dados e engenharia de recursos, use o Python para emitir consultas SQL diretamente no SQL DW.</span><span class="sxs-lookup"><span data-stu-id="49555-323">For larger data exploration, data manipulation and feature engineering, use Python to issue SQL Queries directly against the SQL DW.</span></span>
* <span data-ttu-id="49555-324">Decida o tamanho do exemplo adequado para criação do modelo do Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="49555-324">Decide the sample size to be suitable for Azure Machine Learning model building.</span></span>

<span data-ttu-id="49555-325">A seguir estão alguns exemplos de exploração de dados, visualização de dados e engenharia de recursos.</span><span class="sxs-lookup"><span data-stu-id="49555-325">The followings are a few data exploration, data visualization, and feature engineering examples.</span></span> <span data-ttu-id="49555-326">É possível encontrar mais explorações de dados no Notebook IPython de exemplo e no arquivo de script de Python de exemplo.</span><span class="sxs-lookup"><span data-stu-id="49555-326">More data explorations can be found in the sample IPython Notebook and the sample Python script file.</span></span>

### <a name="initialize-database-credentials"></a><span data-ttu-id="49555-327">Inicializar as credenciais de banco de dados</span><span class="sxs-lookup"><span data-stu-id="49555-327">Initialize database credentials</span></span>
<span data-ttu-id="49555-328">Inicialize as configurações de conexão de banco de dados nas seguintes variáveis:</span><span class="sxs-lookup"><span data-stu-id="49555-328">Initialize your database connection settings in the following variables:</span></span>

    SERVER_NAME=<server name>
    DATABASE_NAME=<database name>
    USERID=<user name>
    PASSWORD=<password>
    DB_DRIVER = <database driver>

### <a name="create-database-connection"></a><span data-ttu-id="49555-329">Criar conexão de banco de dados</span><span class="sxs-lookup"><span data-stu-id="49555-329">Create database connection</span></span>
<span data-ttu-id="49555-330">Veja a cadeia de conexão que cria a conexão com o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="49555-330">Here is the connection string that creates the connection to the database.</span></span>

    CONNECTION_STRING = 'DRIVER={'+DRIVER+'};SERVER='+SERVER_NAME+';DATABASE='+DATABASE_NAME+';UID='+USERID+';PWD='+PASSWORD
    conn = pyodbc.connect(CONNECTION_STRING)

### <a name="report-number-of-rows-and-columns-in-table-nyctaxitrip"></a><span data-ttu-id="49555-331">Relatar o número de linhas e colunas na tabela <nyctaxi_trip></span><span class="sxs-lookup"><span data-stu-id="49555-331">Report number of rows and columns in table <nyctaxi_trip></span></span>
    nrows = pd.read_sql('''
        SELECT SUM(rows) FROM sys.partitions
        WHERE object_id = OBJECT_ID('<schemaname>.<nyctaxi_trip>')
    ''', conn)

    print 'Total number of rows = %d' % nrows.iloc[0,0]

    ncols = pd.read_sql('''
        SELECT COUNT(*) FROM information_schema.columns
        WHERE table_name = ('<nyctaxi_trip>') AND table_schema = ('<schemaname>')
    ''', conn)

    print 'Total number of columns = %d' % ncols.iloc[0,0]

* <span data-ttu-id="49555-332">Número total de linhas = 173179759</span><span class="sxs-lookup"><span data-stu-id="49555-332">Total number of rows = 173179759</span></span>  
* <span data-ttu-id="49555-333">Número total de colunas = 14</span><span class="sxs-lookup"><span data-stu-id="49555-333">Total number of columns = 14</span></span>

### <a name="report-number-of-rows-and-columns-in-table-nyctaxifare"></a><span data-ttu-id="49555-334">Relatar o número de linhas e colunas na tabela <nyctaxi_fare></span><span class="sxs-lookup"><span data-stu-id="49555-334">Report number of rows and columns in table <nyctaxi_fare></span></span>
    nrows = pd.read_sql('''
        SELECT SUM(rows) FROM sys.partitions
        WHERE object_id = OBJECT_ID('<schemaname>.<nyctaxi_fare>')
    ''', conn)

    print 'Total number of rows = %d' % nrows.iloc[0,0]

    ncols = pd.read_sql('''
        SELECT COUNT(*) FROM information_schema.columns
        WHERE table_name = ('<nyctaxi_fare>') AND table_schema = ('<schemaname>')
    ''', conn)

    print 'Total number of columns = %d' % ncols.iloc[0,0]

* <span data-ttu-id="49555-335">Número total de linhas = 173179759</span><span class="sxs-lookup"><span data-stu-id="49555-335">Total number of rows = 173179759</span></span>  
* <span data-ttu-id="49555-336">Número total de colunas = 11</span><span class="sxs-lookup"><span data-stu-id="49555-336">Total number of columns = 11</span></span>

### <a name="read-in-a-small-data-sample-from-the-sql-data-warehouse-database"></a><span data-ttu-id="49555-337">Leitura de uma pequena amostra de dados do Banco de Dados do SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="49555-337">Read-in a small data sample from the SQL Data Warehouse Database</span></span>
    t0 = time.time()

    query = '''
        SELECT TOP 10000 t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax,
            f.tolls_amount, f.total_amount, f.tip_amount
        FROM <schemaname>.<nyctaxi_trip> t, <schemaname>.<nyctaxi_fare> f
        WHERE datepart("mi",t.pickup_datetime) = 1
        AND   t.medallion = f.medallion
        AND   t.hack_license = f.hack_license
        AND   t.pickup_datetime = f.pickup_datetime
    '''

    df1 = pd.read_sql(query, conn)

    t1 = time.time()
    print 'Time to read the sample table is %f seconds' % (t1-t0)

    print 'Number of rows and columns retrieved = (%d, %d)' % (df1.shape[0], df1.shape[1])

<span data-ttu-id="49555-338">O tempo para ler a tabela de exemplo é 14,096495 segundos.</span><span class="sxs-lookup"><span data-stu-id="49555-338">Time to read the sample table is 14.096495 seconds.</span></span>  
<span data-ttu-id="49555-339">Número de linhas e colunas recuperadas = (1000, 21).</span><span class="sxs-lookup"><span data-stu-id="49555-339">Number of rows and columns retrieved = (1000, 21).</span></span>

### <a name="descriptive-statistics"></a><span data-ttu-id="49555-340">Estatísticas descritivas</span><span class="sxs-lookup"><span data-stu-id="49555-340">Descriptive statistics</span></span>
<span data-ttu-id="49555-341">Agora você está pronto para explorar os dados amostrados.</span><span class="sxs-lookup"><span data-stu-id="49555-341">Now you are ready to explore the sampled data.</span></span> <span data-ttu-id="49555-342">Começamos observando algumas estatísticas descritivas para **trip\_distance** (ou qualquer outro campo escolhido a ser especificado).</span><span class="sxs-lookup"><span data-stu-id="49555-342">We start with looking at some descriptive statistics for the **trip\_distance** (or any other fields you choose to specify).</span></span>

    df1['trip_distance'].describe()

### <a name="visualization-box-plot-example"></a><span data-ttu-id="49555-343">Visualização: exemplo de plotagem da caixa</span><span class="sxs-lookup"><span data-stu-id="49555-343">Visualization: Box plot example</span></span>
<span data-ttu-id="49555-344">Em seguida, analisamos a caixa para a distância de viagem para visualizar os quantis.</span><span class="sxs-lookup"><span data-stu-id="49555-344">Next we look at the box plot for the trip distance to visualize the quantiles.</span></span>

    df1.boxplot(column='trip_distance',return_type='dict')

![Plotar nº 1][1]

### <a name="visualization-distribution-plot-example"></a><span data-ttu-id="49555-346">Visualização: exemplo de plotagem de distribuição</span><span class="sxs-lookup"><span data-stu-id="49555-346">Visualization: Distribution plot example</span></span>
<span data-ttu-id="49555-347">Plotagens para visualização da distribuição e um histograma para os exemplos de distâncias de corridas.</span><span class="sxs-lookup"><span data-stu-id="49555-347">Plots that visualize the distribution and a histogram for the sampled trip distances.</span></span>

    fig = plt.figure()
    ax1 = fig.add_subplot(1,2,1)
    ax2 = fig.add_subplot(1,2,2)
    df1['trip_distance'].plot(ax=ax1,kind='kde', style='b-')
    df1['trip_distance'].hist(ax=ax2, bins=100, color='k')

![Plotar nº 2][2]

### <a name="visualization-bar-and-line-plots"></a><span data-ttu-id="49555-349">Visualização: plotagens de barra e linha</span><span class="sxs-lookup"><span data-stu-id="49555-349">Visualization: Bar and line plots</span></span>
<span data-ttu-id="49555-350">Neste exemplo, podemos compartimentalizar a distância da viagem em cinco compartimentos e visualizar os resultados de compartimentalização.</span><span class="sxs-lookup"><span data-stu-id="49555-350">In this example, we bin the trip distance into five bins and visualize the binning results.</span></span>

    trip_dist_bins = [0, 1, 2, 4, 10, 1000]
    df1['trip_distance']
    trip_dist_bin_id = pd.cut(df1['trip_distance'], trip_dist_bins)
    trip_dist_bin_id

<span data-ttu-id="49555-351">Podemos plotar a distribuição de compartimentos acima em um gráfico de barras ou linhas:</span><span class="sxs-lookup"><span data-stu-id="49555-351">We can plot the above bin distribution in a bar or line plot with:</span></span>

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='bar')

![Plotar nº 3][3]

<span data-ttu-id="49555-353">e</span><span class="sxs-lookup"><span data-stu-id="49555-353">and</span></span>

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='line')

![Plotar nº 4][4]

### <a name="visualization-scatterplot-examples"></a><span data-ttu-id="49555-355">Visualização: exemplo de plotagem de dispersão</span><span class="sxs-lookup"><span data-stu-id="49555-355">Visualization: Scatterplot examples</span></span>
<span data-ttu-id="49555-356">Mostramos o gráfico de dispersão entre **trip\_time\_in\_secs** e **trip\_distance** para ver se há alguma correlação</span><span class="sxs-lookup"><span data-stu-id="49555-356">We show scatter plot between **trip\_time\_in\_secs** and **trip\_distance** to see if there is any correlation</span></span>

    plt.scatter(df1['trip_time_in_secs'], df1['trip_distance'])

![Plotar nº 6][6]

<span data-ttu-id="49555-358">Da mesma forma, é possível verificar a relação entre **rate\_code** e **trip\_distance**.</span><span class="sxs-lookup"><span data-stu-id="49555-358">Similarly we can check the relationship between **rate\_code** and **trip\_distance**.</span></span>

    plt.scatter(df1['passenger_count'], df1['trip_distance'])

![Plotar nº 8][8]

### <a name="data-exploration-on-sampled-data-using-sql-queries-in-ipython-notebook"></a><span data-ttu-id="49555-360">Exploração de dados em exemplos de dados usando consultas SQL no notebook IPython</span><span class="sxs-lookup"><span data-stu-id="49555-360">Data exploration on sampled data using SQL queries in IPython notebook</span></span>
<span data-ttu-id="49555-361">Nesta seção, exploraremos distribuições de dados usando os dados de amostra que são mantidos na nova tabela criada acima.</span><span class="sxs-lookup"><span data-stu-id="49555-361">In this section, we explore data distributions using the sampled data which is persisted in the new table we created above.</span></span> <span data-ttu-id="49555-362">Observe que explorações semelhantes podem ser executadas usando as tabelas originais.</span><span class="sxs-lookup"><span data-stu-id="49555-362">Note that similar explorations can be performed using the original tables.</span></span>

#### <a name="exploration-report-number-of-rows-and-columns-in-the-sampled-table"></a><span data-ttu-id="49555-363">Exploração: relatar o número de linhas e colunas na tabela de exemplo</span><span class="sxs-lookup"><span data-stu-id="49555-363">Exploration: Report number of rows and columns in the sampled table</span></span>
    nrows = pd.read_sql('''SELECT SUM(rows) FROM sys.partitions WHERE object_id = OBJECT_ID('<schemaname>.<nyctaxi_sample>')''', conn)
    print 'Number of rows in sample = %d' % nrows.iloc[0,0]

    ncols = pd.read_sql('''SELECT count(*) FROM information_schema.columns WHERE table_name = ('<nyctaxi_sample>') AND table_schema = '<schemaname>'''', conn)
    print 'Number of columns in sample = %d' % ncols.iloc[0,0]

#### <a name="exploration-tippednot-tripped-distribution"></a><span data-ttu-id="49555-364">Exploração: distribuição de corridas com gorjeta e sem gorjeta</span><span class="sxs-lookup"><span data-stu-id="49555-364">Exploration: Tipped/not tripped Distribution</span></span>
    query = '''
        SELECT tipped, count(*) AS tip_freq
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY tipped
        '''

    pd.read_sql(query, conn)

#### <a name="exploration-tip-class-distribution"></a><span data-ttu-id="49555-365">Exploração: distribuição de classe de gorjetas</span><span class="sxs-lookup"><span data-stu-id="49555-365">Exploration: Tip class distribution</span></span>
    query = '''
        SELECT tip_class, count(*) AS tip_freq
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY tip_class
    '''

    tip_class_dist = pd.read_sql(query, conn)

#### <a name="exploration-plot-the-tip-distribution-by-class"></a><span data-ttu-id="49555-366">Exploração: plotar a distribuição de gorjetas por classe</span><span class="sxs-lookup"><span data-stu-id="49555-366">Exploration: Plot the tip distribution by class</span></span>
    tip_class_dist['tip_freq'].plot(kind='bar')

![Plotar nº 26][26]

#### <a name="exploration-daily-distribution-of-trips"></a><span data-ttu-id="49555-368">Exploração: distribuição diária de corridas</span><span class="sxs-lookup"><span data-stu-id="49555-368">Exploration: Daily distribution of trips</span></span>
    query = '''
        SELECT CONVERT(date, dropoff_datetime) AS date, COUNT(*) AS c
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY CONVERT(date, dropoff_datetime)
    '''

    pd.read_sql(query,conn)

#### <a name="exploration-trip-distribution-per-medallion"></a><span data-ttu-id="49555-369">Exploração: distribuição de corridas por licença</span><span class="sxs-lookup"><span data-stu-id="49555-369">Exploration: Trip distribution per medallion</span></span>
    query = '''
        SELECT medallion,count(*) AS c
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY medallion
    '''

    pd.read_sql(query,conn)

#### <a name="exploration-trip-distribution-by-medallion-and-hack-license"></a><span data-ttu-id="49555-370">Exploração: distribuição de corridas por medalhão e carteira de habilitação</span><span class="sxs-lookup"><span data-stu-id="49555-370">Exploration: Trip distribution by medallion and hack license</span></span>
    query = '''select medallion, hack_license,count(*) from <schemaname>.<nyctaxi_sample> group by medallion, hack_license'''
    pd.read_sql(query,conn)


#### <a name="exploration-trip-time-distribution"></a><span data-ttu-id="49555-371">Exploração: distribuição de horário das corridas</span><span class="sxs-lookup"><span data-stu-id="49555-371">Exploration: Trip time distribution</span></span>
    query = '''select trip_time_in_secs, count(*) from <schemaname>.<nyctaxi_sample> group by trip_time_in_secs order by count(*) desc'''
    pd.read_sql(query,conn)

#### <a name="exploration-trip-distance-distribution"></a><span data-ttu-id="49555-372">Exploração: distribuição da distância das corridas</span><span class="sxs-lookup"><span data-stu-id="49555-372">Exploration: Trip distance distribution</span></span>
    query = '''select floor(trip_distance/5)*5 as tripbin, count(*) from <schemaname>.<nyctaxi_sample> group by floor(trip_distance/5)*5 order by count(*) desc'''
    pd.read_sql(query,conn)

#### <a name="exploration-payment-type-distribution"></a><span data-ttu-id="49555-373">Exploração: distribuição do tipo de pagamento</span><span class="sxs-lookup"><span data-stu-id="49555-373">Exploration: Payment type distribution</span></span>
    query = '''select payment_type,count(*) from <schemaname>.<nyctaxi_sample> group by payment_type'''
    pd.read_sql(query,conn)

#### <a name="verify-the-final-form-of-the-featurized-table"></a><span data-ttu-id="49555-374">Verificar a forma final da tabela apresentada</span><span class="sxs-lookup"><span data-stu-id="49555-374">Verify the final form of the featurized table</span></span>
    query = '''SELECT TOP 100 * FROM <schemaname>.<nyctaxi_sample>'''
    pd.read_sql(query,conn)

## <span data-ttu-id="49555-375">
            <a name="mlmodel">
            </a>Compilar modelos no Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="49555-375"><a name="mlmodel"></a>Build models in Azure Machine Learning</span></span>
<span data-ttu-id="49555-376">Agora estamos prontos para prosseguir com a criação e implantação de modelo no [Azure Machine Learning](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="49555-376">We are now ready to proceed to model building and model deployment in [Azure Machine Learning](https://studio.azureml.net).</span></span> <span data-ttu-id="49555-377">Os dados estão prontos para serem usados em qualquer um dos problemas de previsão identificados anteriormente, ou seja:</span><span class="sxs-lookup"><span data-stu-id="49555-377">The data is ready to be used in any of the prediction problems identified earlier, namely:</span></span>

1. <span data-ttu-id="49555-378">**Classificação binária**: para prever se uma gorjeta foi ou não paga em uma corrida.</span><span class="sxs-lookup"><span data-stu-id="49555-378">**Binary classification**: To predict whether or not a tip was paid for a trip.</span></span>
2. <span data-ttu-id="49555-379">**Classificação multiclasse**: para prever o intervalo da gorjeta paga, de acordo com as classes definidas anteriormente.</span><span class="sxs-lookup"><span data-stu-id="49555-379">**Multiclass classification**: To predict the range of tip paid, according to the previously defined classes.</span></span>
3. <span data-ttu-id="49555-380">**Tarefa de regressão**: prever o valor da gorjeta paga por uma corrida.</span><span class="sxs-lookup"><span data-stu-id="49555-380">**Regression task**: To predict the amount of tip paid for a trip.</span></span>  

<span data-ttu-id="49555-381">Para iniciar o exercício de modelagem, faça logon no seu espaço de trabalho do **Azure Machine Learning**.</span><span class="sxs-lookup"><span data-stu-id="49555-381">To begin the modeling exercise, log in to your **Azure Machine Learning** workspace.</span></span> <span data-ttu-id="49555-382">Se você ainda não tiver criado uma espaço de trabalho de aprendizado de máquina, consulte [Criar um espaço de trabalho de AM do Azure](machine-learning-create-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="49555-382">If you have not yet created a machine learning workspace, see [Create an Azure ML workspace](machine-learning-create-workspace.md).</span></span>

1. <span data-ttu-id="49555-383">Para ver os primeiros passos no Azure Machine Learning, consulte [O que é o Azure Machine Learning Studio?](machine-learning-what-is-ml-studio.md)</span><span class="sxs-lookup"><span data-stu-id="49555-383">To get started with Azure Machine Learning, see [What is Azure Machine Learning Studio?](machine-learning-what-is-ml-studio.md)</span></span>
2. <span data-ttu-id="49555-384">Faça logon no [Azure Machine Learning Studio](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="49555-384">Log in to [Azure Machine Learning Studio](https://studio.azureml.net).</span></span>
3. <span data-ttu-id="49555-385">A página inicial do Estúdio fornece uma grande quantidade de informações, vídeos, tutoriais e links para a Referência de Módulos e outros recursos.</span><span class="sxs-lookup"><span data-stu-id="49555-385">The Studio Home page provides a wealth of information, videos, tutorials, links to the Modules Reference, and other resources.</span></span> <span data-ttu-id="49555-386">Para saber mais sobre o Azure Machine Learning, confira o [Centro de Documentação do Azure Machine Learning](https://azure.microsoft.com/documentation/services/machine-learning/).</span><span class="sxs-lookup"><span data-stu-id="49555-386">For more information about Azure Machine Learning, consult the [Azure Machine Learning Documentation Center](https://azure.microsoft.com/documentation/services/machine-learning/).</span></span>

<span data-ttu-id="49555-387">Um teste de treinamento típico é formado pelas seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="49555-387">A typical training experiment consists of the following steps:</span></span>

1. <span data-ttu-id="49555-388">Criar uma experiência **+NEW** .</span><span class="sxs-lookup"><span data-stu-id="49555-388">Create a **+NEW** experiment.</span></span>
2. <span data-ttu-id="49555-389">Levar os dados ao AM do Azure.</span><span class="sxs-lookup"><span data-stu-id="49555-389">Get the data into Azure ML.</span></span>
3. <span data-ttu-id="49555-390">Pré-processar, transformar e manipular os dados conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="49555-390">Pre-process, transform and manipulate the data as needed.</span></span>
4. <span data-ttu-id="49555-391">Gerar recursos conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="49555-391">Generate features as needed.</span></span>
5. <span data-ttu-id="49555-392">Dividir os dados em conjuntos de dados de treinamento/validação/teste (ou conjuntos de dados separados para cada um desses).</span><span class="sxs-lookup"><span data-stu-id="49555-392">Split the data into training/validation/testing datasets(or have separate datasets for each).</span></span>
6. <span data-ttu-id="49555-393">Selecionar um ou mais algoritmos de aprendizado de máquina dependendo do problema de aprendizado a ser resolvido.</span><span class="sxs-lookup"><span data-stu-id="49555-393">Select one or more machine learning algorithms depending on the learning problem to solve.</span></span> <span data-ttu-id="49555-394">Por exemplo, classificação binária, classificação multiclasse ou regressão.</span><span class="sxs-lookup"><span data-stu-id="49555-394">E.g., binary classification, multiclass classification, regression.</span></span>
7. <span data-ttu-id="49555-395">Treinar um ou mais modelos usando o conjunto de dados de treinamento.</span><span class="sxs-lookup"><span data-stu-id="49555-395">Train one or more models using the training dataset.</span></span>
8. <span data-ttu-id="49555-396">Pontuar o conjunto de dados de validação usando os modelos treinados.</span><span class="sxs-lookup"><span data-stu-id="49555-396">Score the validation dataset using the trained model(s).</span></span>
9. <span data-ttu-id="49555-397">Avaliar os modelos para computar a métrica relevante para o problema de aprendizado.</span><span class="sxs-lookup"><span data-stu-id="49555-397">Evaluate the model(s) to compute the relevant metrics for the learning problem.</span></span>
10. <span data-ttu-id="49555-398">Ajustar os modelos e selecionar o melhor modelo a ser implantado.</span><span class="sxs-lookup"><span data-stu-id="49555-398">Fine tune the model(s) and select the best model to deploy.</span></span>

<span data-ttu-id="49555-399">Neste exercício, já exploramos e engenhamos os dados no SQL Data Warehouse e escolhemos o tamanho da amostra para ingestão no AM do Azure.</span><span class="sxs-lookup"><span data-stu-id="49555-399">In this exercise, we have already explored and engineered the data in SQL Data Warehouse, and decided on the sample size to ingest in Azure ML.</span></span> <span data-ttu-id="49555-400">Este é o procedimento para compilar um ou mais dos modelos de previsão:</span><span class="sxs-lookup"><span data-stu-id="49555-400">Here is the procedure to build one or more of the prediction models:</span></span>

1. <span data-ttu-id="49555-401">Obtenha os dados no Azure ML usando o módulo [Importar dados][import-data], disponível na seção **Entrada e saída de dados**.</span><span class="sxs-lookup"><span data-stu-id="49555-401">Get the data into Azure ML using the [Import Data][import-data] module, available in the **Data Input and Output** section.</span></span> <span data-ttu-id="49555-402">Para saber mais, veja a página de referência do módulo [Importar Dados][import-data].</span><span class="sxs-lookup"><span data-stu-id="49555-402">For more information, see the [Import Data][import-data] module reference page.</span></span>
   
    ![Dados de Importação de AM do Azure][17]
2. <span data-ttu-id="49555-404">Selecione **Banco de Dados SQL do Azure** como a **Fonte de dados** no painel **Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="49555-404">Select **Azure SQL Database** as the **Data source** in the **Properties** panel.</span></span>
3. <span data-ttu-id="49555-405">Insira o nome de DNS do banco de dados no campo **Nome do servidor de banco de dados** .</span><span class="sxs-lookup"><span data-stu-id="49555-405">Enter the database DNS name in the **Database server name** field.</span></span> <span data-ttu-id="49555-406">Formato: `tcp:<your_virtual_machine_DNS_name>,1433`</span><span class="sxs-lookup"><span data-stu-id="49555-406">Format: `tcp:<your_virtual_machine_DNS_name>,1433`</span></span>
4. <span data-ttu-id="49555-407">Insira o **Nome do banco de dados** no campo correspondente.</span><span class="sxs-lookup"><span data-stu-id="49555-407">Enter the **Database name** in the corresponding field.</span></span>
5. <span data-ttu-id="49555-408">Insira o *Nome de usuário do SQL* em **Nome de conta do usuário do servidor** e a *senha* em **Senha da conta de usuário do servidor**.</span><span class="sxs-lookup"><span data-stu-id="49555-408">Enter the *SQL user name* in the **Server user account name**, and the *password* in the **Server user account password**.</span></span>
6. <span data-ttu-id="49555-409">Marque a opção **Aceitar qualquer certificado do servidor** .</span><span class="sxs-lookup"><span data-stu-id="49555-409">Check the **Accept any server certificate** option.</span></span>
7. <span data-ttu-id="49555-410">Na área de edição de texto **Consulta de banco de dados** , cole a consulta que extrai os campos de banco de dados necessários (incluindo quaisquer campos calculados, como rótulos) e reduza as amostras de dados para o tamanho de amostra desejado.</span><span class="sxs-lookup"><span data-stu-id="49555-410">In the **Database query** edit text area, paste the query which extracts the necessary database fields (including any computed fields such as the labels) and down samples the data to the desired sample size.</span></span>

<span data-ttu-id="49555-411">Veja na figura abaixo um exemplo de experimento de classificação binária que lê dados diretamente do banco de dados do SQL Data Warehouse (lembre-se de substituir os nomes de tabela nyctaxi_trip e nyctaxi_fare pelo nome do esquema e nomes de tabela usados no passo a passo).</span><span class="sxs-lookup"><span data-stu-id="49555-411">An example of a binary classification experiment reading data directly from the SQL Data Warehouse database is in the figure below (remember to replace the table names nyctaxi_trip and nyctaxi_fare by the schema name and the table names you used in your walkthrough).</span></span> <span data-ttu-id="49555-412">Experimentos semelhantes podem ser construídos por meio de classificação multiclasse e problemas de regressão.</span><span class="sxs-lookup"><span data-stu-id="49555-412">Similar experiments can be constructed for multiclass classification and regression problems.</span></span>

![Treino do AM do Azure][10]

> [!IMPORTANT]
> <span data-ttu-id="49555-414">Nos exemplos de modelagem de extração de dados e consulta de amostragem fornecidos nas seções anteriores, **todos os rótulos para os três exercícios de modelagem são incluídos na consulta**.</span><span class="sxs-lookup"><span data-stu-id="49555-414">In the modeling data extraction and sampling query examples provided in previous sections, **all labels for the three modeling exercises are included in the query**.</span></span> <span data-ttu-id="49555-415">Uma etapa importante (obrigatória) em cada um dos exercícios modelagem é **excluir** os rótulos desnecessários para os dois problemas e qualquer outro **vazamento de destino**.</span><span class="sxs-lookup"><span data-stu-id="49555-415">An important (required) step in each of the modeling exercises is to **exclude** the unnecessary labels for the other two problems, and any other **target leaks**.</span></span> <span data-ttu-id="49555-416">Por exemplo, ao usar a classificação binária, use o rótulo **tipped** e exclua os campos **tip\_class**, **tip\_amount** e **total\_amount**.</span><span class="sxs-lookup"><span data-stu-id="49555-416">For example, when using binary classification, use the label **tipped** and exclude the fields **tip\_class**, **tip\_amount**, and **total\_amount**.</span></span> <span data-ttu-id="49555-417">Esses últimos são vazamentos de destino, já que eles indicam a gorjeta paga.</span><span class="sxs-lookup"><span data-stu-id="49555-417">The latter are target leaks since they imply the tip paid.</span></span>
> 
> <span data-ttu-id="49555-418">Para excluir as colunas desnecessárias ou vazamentos de destino, você pode usar o módulo [Selecionar Colunas do Conjunto de Dados][select-columns] ou [Editar Metadados][edit-metadata].</span><span class="sxs-lookup"><span data-stu-id="49555-418">To exclude any unnecessary columns or target leaks, you may use the [Select Columns in Dataset][select-columns] module or the [Edit Metadata][edit-metadata].</span></span> <span data-ttu-id="49555-419">Para saber mais, veja as páginas de referência [Selecionar Colunas no Conjunto de Dados][select-columns] e [Editar Metadados][edit-metadata].</span><span class="sxs-lookup"><span data-stu-id="49555-419">For more information, see [Select Columns in Dataset][select-columns] and [Edit Metadata][edit-metadata] reference pages.</span></span>
> 
> 

## <span data-ttu-id="49555-420"><a name="mldeploy"></a>Implantar modelos no Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="49555-420"><a name="mldeploy"></a>Deploy models in Azure Machine Learning</span></span>
<span data-ttu-id="49555-421">Quando o modelo estiver pronto, você pode implantá-lo facilmente como um serviço Web diretamente do experimento.</span><span class="sxs-lookup"><span data-stu-id="49555-421">When your model is ready, you can easily deploy it as a web service directly from the experiment.</span></span> <span data-ttu-id="49555-422">Para obter mais informações sobre como implantar os serviços Web do AM do Azure, veja [Implantar um serviço Web do Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="49555-422">For more information about deploying Azure ML web services, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

<span data-ttu-id="49555-423">Para implantar um novo serviço Web, você precisa:</span><span class="sxs-lookup"><span data-stu-id="49555-423">To deploy a new web service, you need to:</span></span>

1. <span data-ttu-id="49555-424">Criar um experimento de pontuação.</span><span class="sxs-lookup"><span data-stu-id="49555-424">Create a scoring experiment.</span></span>
2. <span data-ttu-id="49555-425">Implantar o serviço Web.</span><span class="sxs-lookup"><span data-stu-id="49555-425">Deploy the web service.</span></span>

<span data-ttu-id="49555-426">Para criar um teste de pontuação por meio de um teste de treinamento **Concluído**, clique em **CRIAR TESTE DE PONTUAÇÃO** na barra de ação inferior.</span><span class="sxs-lookup"><span data-stu-id="49555-426">To create a scoring experiment from a **Finished** training experiment, click **CREATE SCORING EXPERIMENT** in the lower action bar.</span></span>

![Pontuação do Azure][18]

<span data-ttu-id="49555-428">O Azure Machine Learning tentará criar um experimento de pontuação com base nos componentes do experimento de treinamento.</span><span class="sxs-lookup"><span data-stu-id="49555-428">Azure Machine Learning will attempt to create a scoring experiment based on the components of the training experiment.</span></span> <span data-ttu-id="49555-429">Em especial, ele vai:</span><span class="sxs-lookup"><span data-stu-id="49555-429">In particular, it will:</span></span>

1. <span data-ttu-id="49555-430">Salvar o modelo treinado e remover os módulos de treinamento de modelo.</span><span class="sxs-lookup"><span data-stu-id="49555-430">Save the trained model and remove the model training modules.</span></span>
2. <span data-ttu-id="49555-431">Identificar uma **porta de entrada** lógica para representar o esquema de dados de entrada esperado.</span><span class="sxs-lookup"><span data-stu-id="49555-431">Identify a logical **input port** to represent the expected input data schema.</span></span>
3. <span data-ttu-id="49555-432">Identificar uma **porta de saída** lógica para representar o esquema de saída do serviço Web.</span><span class="sxs-lookup"><span data-stu-id="49555-432">Identify a logical **output port** to represent the expected web service output schema.</span></span>

<span data-ttu-id="49555-433">Quando o experimento de pontuação é criado, analisá-lo e ajustar conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="49555-433">When the scoring experiment is created, review it and make adjust as needed.</span></span> <span data-ttu-id="49555-434">Um ajuste típico é substituir o conjunto de dados de entrada e/ou a consulta por uma exclua os campos de rótulo, pois eles não estarão disponíveis quando o serviço for chamado.</span><span class="sxs-lookup"><span data-stu-id="49555-434">A typical adjustment is to replace the input dataset and/or query with one which excludes label fields, as these will not be available when the service is called.</span></span> <span data-ttu-id="49555-435">Também é uma prática recomendada reduzir o tamanho do conjunto de dados de entrada e/ou da consulta a apenas alguns registros, suficientes para indicar o esquema de entrada.</span><span class="sxs-lookup"><span data-stu-id="49555-435">It is also a good practice to reduce the size of the input dataset and/or query to a few records, just enough to indicate the input schema.</span></span> <span data-ttu-id="49555-436">Para a porta de saída, é comum excluir todos os campos de entrada e incluir apenas os **Rótulos Pontuados** e **Probabilidades Pontuadas** na saída usando o módulo [Selecionar Colunas do Conjunto de Dados][select-columns].</span><span class="sxs-lookup"><span data-stu-id="49555-436">For the output port, it is common to exclude all input fields and only include the **Scored Labels** and **Scored Probabilities** in the output using the [Select Columns in Dataset][select-columns] module.</span></span>

<span data-ttu-id="49555-437">Veja na figura abaixo um exemplo de teste de pontuação.</span><span class="sxs-lookup"><span data-stu-id="49555-437">A sample scoring experiment is provided in the figure below.</span></span> <span data-ttu-id="49555-438">Quando estiver pronto para implantar, clique no botão **PUBLICAR SERVIÇO WEB** na barra de ação inferior.</span><span class="sxs-lookup"><span data-stu-id="49555-438">When ready to deploy, click the **PUBLISH WEB SERVICE** button in the lower action bar.</span></span>

![Publicação do AM do Azure][11]

## <a name="summary"></a><span data-ttu-id="49555-440">Resumo</span><span class="sxs-lookup"><span data-stu-id="49555-440">Summary</span></span>
<span data-ttu-id="49555-441">Vamos recapitular o que fizemos neste tutorial passo a passo: você criou um ambiente de ciência de dados do Azure, trabalhou com um grande conjunto de dados público, passando pelo Processo de Ciência de Dados de Equipe, desde a aquisição dos dados até o treinamento de modelo e, em seguida, até a implantação de um serviço Web do Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="49555-441">To recap what we have done in this walkthrough tutorial, you have created an Azure data science environment, worked with a large public dataset, taking it through the Team Data Science Process, all the way from data acquisition to model training, and then to the deployment of an Azure Machine Learning web service.</span></span>

### <a name="license-information"></a><span data-ttu-id="49555-442">Informações de licença</span><span class="sxs-lookup"><span data-stu-id="49555-442">License information</span></span>
<span data-ttu-id="49555-443">Este passo a passo do exemplo, os scripts que o acompanham e os IPython Notebooks são compartilhados pela Microsoft sob a licença MIT.</span><span class="sxs-lookup"><span data-stu-id="49555-443">This sample walkthrough and its accompanying scripts and IPython notebook(s) are shared by Microsoft under the MIT license.</span></span> <span data-ttu-id="49555-444">Verifique o arquivo LICENSE.txt no diretório do código de exemplo no GitHub para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="49555-444">Please check the LICENSE.txt file in in the directory of the sample code on GitHub for more details.</span></span>

## <a name="references"></a><span data-ttu-id="49555-445">Referências</span><span class="sxs-lookup"><span data-stu-id="49555-445">References</span></span>
<span data-ttu-id="49555-446">•   [Página de download de Viagens de Táxi de NYC, de Andrés Monroy](http://www.andresmh.com/nyctaxitrips/)</span><span class="sxs-lookup"><span data-stu-id="49555-446">•    [Andrés Monroy NYC Taxi Trips Download Page](http://www.andresmh.com/nyctaxitrips/)</span></span>  
<span data-ttu-id="49555-447">•   [Dados de Viagem de Táxi de FOILing NYC, de Chris Whong](http://chriswhong.com/open-data/foil_nyc_taxi/) </span><span class="sxs-lookup"><span data-stu-id="49555-447">•    [FOILing NYC’s Taxi Trip Data by Chris Whong](http://chriswhong.com/open-data/foil_nyc_taxi/) </span></span>  
<span data-ttu-id="49555-448">•   [Pesquisa e estatísticas de comissionamento de táxis e limusines de NYC](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span><span class="sxs-lookup"><span data-stu-id="49555-448">•    [NYC Taxi and Limousine Commission Research and Statistics](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span></span>

[1]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_26_1.png
[2]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_28_1.png
[3]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_35_1.png
[4]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_36_1.png
[5]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_39_1.png
[6]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_42_1.png
[7]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_44_1.png
[8]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_46_1.png
[9]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_71_1.png
[10]: ./media/machine-learning-data-science-process-sqldw-walkthrough/azuremltrain.png
[11]: ./media/machine-learning-data-science-process-sqldw-walkthrough/azuremlpublish.png
[12]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ssmsconnect.png
[13]: ./media/machine-learning-data-science-process-sqldw-walkthrough/executescript.png
[14]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sqlserverproperties.png
[15]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sqldefaultdirs.png
[16]: ./media/machine-learning-data-science-process-sqldw-walkthrough/bulkimport.png
[17]: ./media/machine-learning-data-science-process-sqldw-walkthrough/amlreader.png
[18]: ./media/machine-learning-data-science-process-sqldw-walkthrough/amlscoring.png
[19]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ps_download_scripts.png
[20]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ps_load_data.png
[21]: ./media/machine-learning-data-science-process-sqldw-walkthrough/azcopy-overwrite.png
[22]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ipnb-service-aml-1.png
[23]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ipnb-service-aml-2.png
[24]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ipnb-service-aml-3.png
[25]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ipnb-service-aml-4.png
[26]: ./media/machine-learning-data-science-process-sqldw-walkthrough/tip_class_hist_1.png


<!-- Module References -->
[edit-metadata]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
