---
title: "Olá processo de ciência de dados de equipe em ação: usando o SQL Data Warehouse | Microsoft Docs"
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
ms.openlocfilehash: b1b6371583a023d32e33db59464cafd8c3b767d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="hello-team-data-science-process-in-action-using-sql-data-warehouse"></a><span data-ttu-id="d0511-103">Olá processo de ciência de dados de equipe em ação: usando o SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="d0511-103">hello Team Data Science Process in action: using SQL Data Warehouse</span></span>
<span data-ttu-id="d0511-104">Neste tutorial, nós o conduziremos durante a criação e implantação de um modelo de aprendizado de máquina usando o SQL Data Warehouse (SQL DW) para um conjunto de dados disponível publicamente – hello [NYC táxi viagens](http://www.andresmh.com/nyctaxitrips/) conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="d0511-104">In this tutorial, we walk you through building and deploying a machine learning model using SQL Data Warehouse (SQL DW) for a publicly available dataset -- hello [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) dataset.</span></span> <span data-ttu-id="d0511-105">modelo de classificação binária Olá construído prevê ou não uma dica é pago para uma viagem, e modelos de regressão e de classificação multiclasse também são discutidos que preveem distribuição Olá para valores de dica de saudação pagos.</span><span class="sxs-lookup"><span data-stu-id="d0511-105">hello binary classification model constructed predicts whether or not a tip is paid for a trip, and models for multiclass classification and regression are also discussed that predict hello distribution for hello tip amounts paid.</span></span>

<span data-ttu-id="d0511-106">procedimento de saudação segue Olá [processo de ciência de dados da equipe (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="d0511-106">hello procedure follows hello [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) workflow.</span></span> <span data-ttu-id="d0511-107">Vamos mostrar como toosetup um ambiente de ciência de dados, como tooload Olá dados no data Warehouse do SQL e como usar o data Warehouse do SQL ou uma saudação de tooexplore bloco de anotações do IPython em dados e engenharia a toomodel recursos.</span><span class="sxs-lookup"><span data-stu-id="d0511-107">We show how toosetup a data science environment, how tooload hello data into SQL DW, and how use either SQL DW or an IPython Notebook tooexplore hello data and engineer features toomodel.</span></span> <span data-ttu-id="d0511-108">Em seguida, mostramos como toobuild e implantar um modelo de aprendizado de máquina do Azure.</span><span class="sxs-lookup"><span data-stu-id="d0511-108">We then show how toobuild and deploy a model with Azure Machine Learning.</span></span>

## <span data-ttu-id="d0511-109"><a name="dataset"></a>Olá NYC táxi viagens dataset</span><span class="sxs-lookup"><span data-stu-id="d0511-109"><a name="dataset"></a>hello NYC Taxi Trips dataset</span></span>
<span data-ttu-id="d0511-110">Olá dados NYC táxi Trip consiste em cerca de 20GB de arquivos compactados de CSV (~ 48GB descompactado), registrar mais de milhões de 173 hello e viagens individuais é pago para cada viagem.</span><span class="sxs-lookup"><span data-stu-id="d0511-110">hello NYC Taxi Trip data consists of about 20GB of compressed CSV files (~48GB uncompressed), recording more than 173 million individual trips and hello fares paid for each trip.</span></span> <span data-ttu-id="d0511-111">Cada registro de viagem inclui locais de retirada e redistribuição hello e vezes, anônimas invadir o número de licença (do driver) e Olá número medallion (id exclusiva do táxi).</span><span class="sxs-lookup"><span data-stu-id="d0511-111">Each trip record includes hello pickup and drop-off locations and times, anonymized hack (driver's) license number, and hello medallion (taxi’s unique id) number.</span></span> <span data-ttu-id="d0511-112">dados saudação abrange todas as viagens no ano Olá 2013 e são fornecidos em dois conjuntos de dados a seguir para cada mês de saudação:</span><span class="sxs-lookup"><span data-stu-id="d0511-112">hello data covers all trips in hello year 2013 and is provided in hello following two datasets for each month:</span></span>

1. <span data-ttu-id="d0511-113">Olá **trip_data.csv** arquivo contém os detalhes de viagem, como o número de passageiros, pontos de retirada e redução, duração da viagem e comprimento de viagem.</span><span class="sxs-lookup"><span data-stu-id="d0511-113">hello **trip_data.csv** file contains trip details, such as number of passengers, pickup and dropoff points, trip duration, and trip length.</span></span> <span data-ttu-id="d0511-114">Aqui estão alguns exemplos de registros:</span><span class="sxs-lookup"><span data-stu-id="d0511-114">Here are a few sample records:</span></span>
   
        medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count,trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
2. <span data-ttu-id="d0511-115">Olá **trip_fare.csv** arquivo contém detalhes da tarifa Olá pagado para cada viagem, como tipo de pagamento, quantidade de passagens, sobretaxa e impostos, dicas e pedágio e quantidade total de saudação paga.</span><span class="sxs-lookup"><span data-stu-id="d0511-115">hello **trip_fare.csv** file contains details of hello fare paid for each trip, such as payment type, fare amount, surcharge and taxes, tips and tolls, and hello total amount paid.</span></span> <span data-ttu-id="d0511-116">Aqui estão alguns exemplos de registros:</span><span class="sxs-lookup"><span data-stu-id="d0511-116">Here are a few sample records:</span></span>
   
        medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

<span data-ttu-id="d0511-117">Olá **chave exclusiva** usado viagem toojoin\_dados e viagem\_passagens é composta de saudação três campos a seguir:</span><span class="sxs-lookup"><span data-stu-id="d0511-117">hello **unique key** used toojoin trip\_data and trip\_fare is composed of hello following three fields:</span></span>

* <span data-ttu-id="d0511-118">medallion,</span><span class="sxs-lookup"><span data-stu-id="d0511-118">medallion,</span></span>
* <span data-ttu-id="d0511-119">hack\_license e</span><span class="sxs-lookup"><span data-stu-id="d0511-119">hack\_license and</span></span>
* <span data-ttu-id="d0511-120">pickup\_datetime.</span><span class="sxs-lookup"><span data-stu-id="d0511-120">pickup\_datetime.</span></span>

## <span data-ttu-id="d0511-121"><a name="mltasks"></a>Resolver três tipos de tarefas de previsão</span><span class="sxs-lookup"><span data-stu-id="d0511-121"><a name="mltasks"></a>Address three types of prediction tasks</span></span>
<span data-ttu-id="d0511-122">Podemos formular três problemas de previsão com base em Olá *dica\_quantidade* tooillustrate três tipos de tarefas de modelagem:</span><span class="sxs-lookup"><span data-stu-id="d0511-122">We formulate three prediction problems based on hello *tip\_amount* tooillustrate three kinds of modeling tasks:</span></span>

1. <span data-ttu-id="d0511-123">**Classificação binária**: toopredict ou não uma dica foi pago para uma viagem, ou seja, um *dica\_quantidade* que é maior que $0 é um exemplo positivo, enquanto um *dica\_quantidade* $ 0 é um exemplo de negativo.</span><span class="sxs-lookup"><span data-stu-id="d0511-123">**Binary classification**: toopredict whether or not a tip was paid for a trip, i.e. a *tip\_amount* that is greater than $0 is a positive example, while a *tip\_amount* of $0 is a negative example.</span></span>
2. <span data-ttu-id="d0511-124">**Classificação multiclasse**: intervalo de saudação toopredict de dica de pago para viagem hello.</span><span class="sxs-lookup"><span data-stu-id="d0511-124">**Multiclass classification**: toopredict hello range of tip paid for hello trip.</span></span> <span data-ttu-id="d0511-125">Olá, nós dividimos *dica\_quantidade* em cinco compartimentos ou classes:</span><span class="sxs-lookup"><span data-stu-id="d0511-125">We divide hello *tip\_amount* into five bins or classes:</span></span>
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0 and tip_amount <= $5
        Class 2 : tip_amount > $5 and tip_amount <= $10
        Class 3 : tip_amount > $10 and tip_amount <= $20
        Class 4 : tip_amount > $20
3. <span data-ttu-id="d0511-126">**Tarefa de regressão**: o valor de saudação toopredict de dica pago para uma viagem.</span><span class="sxs-lookup"><span data-stu-id="d0511-126">**Regression task**: toopredict hello amount of tip paid for a trip.</span></span>  

## <span data-ttu-id="d0511-127"><a name="setup"></a>Configurar o ambiente de ciência de dados do Azure Olá para análises avançadas</span><span class="sxs-lookup"><span data-stu-id="d0511-127"><a name="setup"></a>Set up hello Azure data science environment for advanced analytics</span></span>
<span data-ttu-id="d0511-128">tooset seu ambiente de ciência de dados do Azure, siga estas etapas.</span><span class="sxs-lookup"><span data-stu-id="d0511-128">tooset up your Azure Data Science environment, follow these steps.</span></span>

<span data-ttu-id="d0511-129">**Crie sua própria conta de armazenamento de blobs do Azure.**</span><span class="sxs-lookup"><span data-stu-id="d0511-129">**Create your own Azure blob storage account**</span></span>

* <span data-ttu-id="d0511-130">Quando você provisionar seu próprio armazenamento de BLOBs do Azure, escolha uma localização geográfica para o armazenamento de BLOBs do Azure em ou mais próximo possível muito**Centro Sul dos EUA**, que é onde Olá dados NYC táxi está armazenado.</span><span class="sxs-lookup"><span data-stu-id="d0511-130">When you provision your own Azure blob storage, choose a geo-location for your Azure blob storage in or as close as possible too**South Central US**, which is where hello NYC Taxi data is stored.</span></span> <span data-ttu-id="d0511-131">dados de saudação serão copiados usando AzCopy do contêiner de tooa de contêiner de armazenamento de blob público Olá em sua própria conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="d0511-131">hello data will be copied using AzCopy from hello public blob storage container tooa container in your own storage account.</span></span> <span data-ttu-id="d0511-132">Olá aproximando-se o armazenamento de BLOBs do Azure é tooSouth centro dos EUA, hello mais rápido essa tarefa (etapa 4) será concluída.</span><span class="sxs-lookup"><span data-stu-id="d0511-132">hello closer your Azure blob storage is tooSouth Central US, hello faster this task (Step 4) will be completed.</span></span>
* <span data-ttu-id="d0511-133">toocreate conta seu próprio armazenamento do Azure, Olá siga as etapas descritas em [contas de armazenamento do Azure sobre](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="d0511-133">toocreate your own Azure storage account, follow hello steps outlined at [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="d0511-134">Ser se notas toomake sobre valores hello seguintes credenciais de conta de armazenamento será necessário mais tarde neste passo a passo.</span><span class="sxs-lookup"><span data-stu-id="d0511-134">Be sure toomake notes on hello values for following storage account credentials as they will be needed later in this walkthrough.</span></span>
  
  * <span data-ttu-id="d0511-135">**Nome da Conta de Armazenamento**</span><span class="sxs-lookup"><span data-stu-id="d0511-135">**Storage Account Name**</span></span>
  * <span data-ttu-id="d0511-136">**Chave da conta de armazenamento**</span><span class="sxs-lookup"><span data-stu-id="d0511-136">**Storage Account Key**</span></span>
  * <span data-ttu-id="d0511-137">**Nome do contêiner** (que você deseja Olá toobe de dados armazenado em Olá armazenamento de BLOBs do Azure)</span><span class="sxs-lookup"><span data-stu-id="d0511-137">**Container Name** (which you want hello data toobe stored in hello Azure blob storage)</span></span>

<span data-ttu-id="d0511-138">**Provisione sua instância do Azure SQL DW.**</span><span class="sxs-lookup"><span data-stu-id="d0511-138">**Provision your Azure SQL DW instance.**</span></span>
<span data-ttu-id="d0511-139">Siga a documentação de saudação em [criar um SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md) tooprovision uma instância do SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="d0511-139">Follow hello documentation at [Create a SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md) tooprovision a SQL Data Warehouse instance.</span></span> <span data-ttu-id="d0511-140">Certifique-se de que você faça notações em Olá credenciais SQL Data Warehouse que serão usadas nas próximas etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="d0511-140">Make sure that you make notations on hello following SQL Data Warehouse credentials which will be used in later steps.</span></span>

* <span data-ttu-id="d0511-141">**Nome do Servidor**: <server Name>.database.windows.net</span><span class="sxs-lookup"><span data-stu-id="d0511-141">**Server Name**: <server Name>.database.windows.net</span></span>
* <span data-ttu-id="d0511-142">**Nome do SQLDW (Banco de Dados)**</span><span class="sxs-lookup"><span data-stu-id="d0511-142">**SQLDW (Database) Name**</span></span>
* <span data-ttu-id="d0511-143">**Nome de Usuário**</span><span class="sxs-lookup"><span data-stu-id="d0511-143">**Username**</span></span>
* <span data-ttu-id="d0511-144">**Senha**</span><span class="sxs-lookup"><span data-stu-id="d0511-144">**Password**</span></span>

<span data-ttu-id="d0511-145">**Instale o Visual Studio e o SQL Server Data Tools.**</span><span class="sxs-lookup"><span data-stu-id="d0511-145">**Install Visual Studio and SQL Server Data Tools.**</span></span> <span data-ttu-id="d0511-146">Para obter instruções, confira [Instalar o Visual Studio 2015 e/ou SSDT (SQL Server Data Tools) para o SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-install-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="d0511-146">For instructions, see [Install Visual Studio 2015 and/or SSDT (SQL Server Data Tools) for SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-install-visual-studio.md).</span></span>

<span data-ttu-id="d0511-147">**Conecte-se tooyour DW do SQL Azure com o Visual Studio.**</span><span class="sxs-lookup"><span data-stu-id="d0511-147">**Connect tooyour Azure SQL DW with Visual Studio.**</span></span> <span data-ttu-id="d0511-148">Para obter instruções, consulte as etapas 1 e 2 na [conectar tooAzure SQL Data Warehouse com o Visual Studio](../sql-data-warehouse/sql-data-warehouse-connect-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d0511-148">For instructions, see steps 1 & 2 in [Connect tooAzure SQL Data Warehouse with Visual Studio](../sql-data-warehouse/sql-data-warehouse-connect-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="d0511-149">Execução hello seguinte consulta SQL no banco de dados de saudação criado no Data Warehouse do SQL (conexão de tópico, em vez da saudação consulta fornecida na etapa 3 do hello) muito**criar uma chave mestra**.</span><span class="sxs-lookup"><span data-stu-id="d0511-149">Run hello following SQL query on hello database you created in your SQL Data Warehouse (instead of hello query provided in step 3 of hello connect topic,) too**create a master key**.</span></span>
> 
> 

    BEGIN TRY
           --Try toocreate hello master key
        CREATE MASTER KEY
    END TRY
    BEGIN CATCH
           --If hello master key exists, do nothing
    END CATCH;

<span data-ttu-id="d0511-150">**Crie um espaço de trabalho de Azure Machine Learning em sua assinatura do Azure.**</span><span class="sxs-lookup"><span data-stu-id="d0511-150">**Create an Azure Machine Learning workspace under your Azure subscription.**</span></span> <span data-ttu-id="d0511-151">Para obter instruções, confira [Criar um espaço de trabalho de Azure Machine Learning](machine-learning-create-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="d0511-151">For instructions, see [Create an Azure Machine Learning workspace](machine-learning-create-workspace.md).</span></span>

## <span data-ttu-id="d0511-152"><a name="getdata"></a>Saudação de carregar dados no SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="d0511-152"><a name="getdata"></a>Load hello data into SQL Data Warehouse</span></span>
<span data-ttu-id="d0511-153">Abra um console de comando do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d0511-153">Open a Windows PowerShell command console.</span></span> <span data-ttu-id="d0511-154">Execute seguinte Olá comandos do PowerShell toodownload Olá exemplo arquivos de script SQL que compartilha com você no GitHub tooa diretório local que você especificar com parâmetro hello *- dirdestino*.</span><span class="sxs-lookup"><span data-stu-id="d0511-154">Run hello following PowerShell commands toodownload hello example SQL script files that we share with you on GitHub tooa local directory that you specify with hello parameter *-DestDir*.</span></span> <span data-ttu-id="d0511-155">Você pode alterar o valor de saudação do parâmetro *- dirdestino* tooany diretório de local.</span><span class="sxs-lookup"><span data-stu-id="d0511-155">You can change hello value of parameter *-DestDir* tooany local directory.</span></span> <span data-ttu-id="d0511-156">Se *- dirdestino* não existir, ele será criado pelo script do PowerShell de saudação.</span><span class="sxs-lookup"><span data-stu-id="d0511-156">If *-DestDir* does not exist, it will be created by hello PowerShell script.</span></span>

> [!NOTE]
> <span data-ttu-id="d0511-157">Talvez seja necessário muito**executar como administrador** ao executar Olá script do PowerShell a seguir se seu *dirdestino* directory precisa tooit de toocreate ou toowrite de privilégio de administrador.</span><span class="sxs-lookup"><span data-stu-id="d0511-157">You might need too**Run as Administrator** when executing hello following PowerShell script if your *DestDir* directory needs Administrator privilege toocreate or toowrite tooit.</span></span>
> 
> 

    $source = "https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/SQLDW/Download_Scripts_SQLDW_Walkthrough.ps1"
    $ps1_dest = "$pwd\Download_Scripts_SQLDW_Walkthrough.ps1"
    $wc = New-Object System.Net.WebClient
    $wc.DownloadFile($source, $ps1_dest)
    .\Download_Scripts_SQLDW_Walkthrough.ps1 –DestDir 'C:\tempSQLDW'

<span data-ttu-id="d0511-158">Após a execução bem-sucedida, o diretório de trabalho atual muda muito*- dirdestino*.</span><span class="sxs-lookup"><span data-stu-id="d0511-158">After successful execution, your current working directory changes too*-DestDir*.</span></span> <span data-ttu-id="d0511-159">Você deve ser capaz de tela de toosee abaixo:</span><span class="sxs-lookup"><span data-stu-id="d0511-159">You should be able toosee screen like below:</span></span>

![][19]

<span data-ttu-id="d0511-160">No seu *- dirdestino*, execute Olá script do PowerShell no modo de administrador a seguir:</span><span class="sxs-lookup"><span data-stu-id="d0511-160">In your *-DestDir*, execute hello following PowerShell script in administrator mode:</span></span>

    ./SQLDW_Data_Import.ps1

<span data-ttu-id="d0511-161">Quando Olá script do PowerShell é executado para Olá primeira vez, você deverá tooinput informações de saudação do seu DW do SQL Azure e sua conta de armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="d0511-161">When hello PowerShell script runs for hello first time, you will be asked tooinput hello information from your Azure SQL DW and your Azure blob storage account.</span></span> <span data-ttu-id="d0511-162">Quando este script do PowerShell é concluído em execução para Olá primeira vez, as credenciais de saudação você entrada será foram gravada o arquivo de configuração de tooa SQLDW.conf no diretório de trabalho presente hello.</span><span class="sxs-lookup"><span data-stu-id="d0511-162">When this PowerShell script completes running for hello first time, hello credentials you input will have been written tooa configuration file SQLDW.conf in hello present working directory.</span></span> <span data-ttu-id="d0511-163">Hello execução futuras desse arquivo de script do PowerShell tem Olá opção tooread necessárias de todos os parâmetros deste arquivo de configuração.</span><span class="sxs-lookup"><span data-stu-id="d0511-163">hello future run of this PowerShell script file has hello option tooread all needed parameters from this configuration file.</span></span> <span data-ttu-id="d0511-164">Se você precisar toochange alguns parâmetros, você pode escolher tooinput parâmetros Olá na tela hello no prompt, exclua esse arquivo de configuração e inserindo valores de parâmetros de saudação conforme solicitado ou valores de parâmetro hello toochange editando o arquivo de SQLDW.conf Olá no seu *- dirdestino* directory.</span><span class="sxs-lookup"><span data-stu-id="d0511-164">If you need toochange some parameters, you can choose tooinput hello parameters on hello screen upon prompt by deleting this configuration file and inputting hello parameters values as prompted or toochange hello parameter values by editing hello SQLDW.conf file in your *-DestDir* directory.</span></span>

> [!NOTE]
> <span data-ttu-id="d0511-165">Em ordem tooavoid esquema nome está em conflito com aqueles que já existem no seu Azure SQL DW ao ler parâmetros diretamente do arquivo de SQLDW.conf Olá, um número aleatório de 3 dígitos é adicionado toohello nome do esquema de arquivo de SQLDW.conf hello como nome do esquema padrão Olá para cada execução.</span><span class="sxs-lookup"><span data-stu-id="d0511-165">In order tooavoid schema name conflicts with those that already exist in your Azure SQL DW, when reading parameters directly from hello SQLDW.conf file, a 3-digit random number is added toohello schema name from hello SQLDW.conf file as hello default schema name for each run.</span></span> <span data-ttu-id="d0511-166">saudação de script do PowerShell pode solicitar um nome de esquema: Olá nome pode ser especificado a critério do usuário.</span><span class="sxs-lookup"><span data-stu-id="d0511-166">hello PowerShell script may prompt you for a schema name: hello name may be specified at user discretion.</span></span>
> 
> 

<span data-ttu-id="d0511-167">Isso **script do PowerShell** arquivo conclui Olá tarefas a seguir:</span><span class="sxs-lookup"><span data-stu-id="d0511-167">This **PowerShell script** file completes hello following tasks:</span></span>

* <span data-ttu-id="d0511-168">**Baixa e instala o AzCopy**, caso ele ainda não esteja instalado</span><span class="sxs-lookup"><span data-stu-id="d0511-168">**Downloads and installs AzCopy**, if AzCopy is not already installed</span></span>
  
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
* <span data-ttu-id="d0511-169">**Copia a conta de armazenamento de blob particular dados tooyour** de blob público de saudação com AzCopy</span><span class="sxs-lookup"><span data-stu-id="d0511-169">**Copies data tooyour private blob storage account** from hello public blob with AzCopy</span></span>
  
        Write-Host "AzCopy is copying data from public blob tooyo storage account. It may take a while..." -ForegroundColor "Yellow"
        $start_time = Get-Date
        AzCopy.exe /Source:$Source /Dest:$DestURL /DestKey:$StorageAccountKey /S
        $end_time = Get-Date
        $time_span = $end_time - $start_time
        $total_seconds = [math]::Round($time_span.TotalSeconds,2)
        Write-Host "AzCopy finished copying data. Please check your storage account tooverify." -ForegroundColor "Yellow"
        Write-Host "This step (copying data from public blob tooyour storage account) takes $total_seconds seconds." -ForegroundColor "Green"
* <span data-ttu-id="d0511-170">**Carrega dados usando o Polybase (executando LoadDataToSQLDW.sql) tooyour Azure SQL DW** de sua conta de armazenamento de blob particular com hello comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="d0511-170">**Loads data using Polybase (by executing LoadDataToSQLDW.sql) tooyour Azure SQL DW** from your private blob storage account with hello following commands.</span></span>
  
  * <span data-ttu-id="d0511-171">Criar um esquema</span><span class="sxs-lookup"><span data-stu-id="d0511-171">Create a schema</span></span>
    
          EXEC (''CREATE SCHEMA {schemaname};'');
  * <span data-ttu-id="d0511-172">Criar uma credencial com escopo de banco de dados</span><span class="sxs-lookup"><span data-stu-id="d0511-172">Create a database scoped credential</span></span>
    
          CREATE DATABASE SCOPED CREDENTIAL {KeyAlias}
          WITH IDENTITY = ''asbkey'' ,
          Secret = ''{StorageAccountKey}''
  * <span data-ttu-id="d0511-173">Criar uma fonte de dados externa para um blob de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="d0511-173">Create an external data source for an Azure storage blob</span></span>
    
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
  * <span data-ttu-id="d0511-174">Criar um formato de arquivo externo para um arquivo csv.</span><span class="sxs-lookup"><span data-stu-id="d0511-174">Create an external file format for a csv file.</span></span> <span data-ttu-id="d0511-175">Dados não são compactados e os campos são separados com o caractere de pipe hello.</span><span class="sxs-lookup"><span data-stu-id="d0511-175">Data is uncompressed and fields are separated with hello pipe character.</span></span>
    
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
  * <span data-ttu-id="d0511-176">Criar tabelas externas de tarifas e corridas para o conjunto de dados Táxi de NYC na conta de Armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="d0511-176">Create external fare and trip tables for NYC taxi dataset in Azure blob storage.</span></span>
    
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

    - <span data-ttu-id="d0511-177">Carregar dados de tabelas externas no tooSQL de armazenamento de BLOBs do Azure Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="d0511-177">Load data from external tables in Azure blob storage tooSQL Data Warehouse</span></span>

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

    - <span data-ttu-id="d0511-178">Criar uma tabela de dados de exemplo (NYCTaxi_Sample) e inserir dados tooit de selecionar consultas SQL nas tabelas de viagem e passagens hello.</span><span class="sxs-lookup"><span data-stu-id="d0511-178">Create a sample data table (NYCTaxi_Sample) and insert data tooit from selecting SQL queries on hello trip and fare tables.</span></span> <span data-ttu-id="d0511-179">(Algumas etapas deste passo a passo precisa toouse essa tabela de exemplo.)</span><span class="sxs-lookup"><span data-stu-id="d0511-179">(Some steps of this walkthrough needs toouse this sample table.)</span></span>

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

<span data-ttu-id="d0511-180">localização geográfica de saudação de suas contas de armazenamento afeta os tempos de carregamento.</span><span class="sxs-lookup"><span data-stu-id="d0511-180">hello geographic location of your storage accounts affects load times.</span></span>

> [!NOTE]
> <span data-ttu-id="d0511-181">Dependendo da localização geográfica de saudação da sua conta de armazenamento de blob particular, Olá processo de copiar dados de uma conta de armazenamento particular de tooyour de blob público pode levar cerca de 15 minutos ou processar ainda mais e hello de carregamento de dados de sua conta de armazenamento tooyour Azure SQL DW pode levar 20 minutos ou mais.</span><span class="sxs-lookup"><span data-stu-id="d0511-181">Depending on hello geographical location of your private blob storage account, hello process of copying data from a public blob tooyour private storage account can take about 15 minutes, or even longer,and hello process of loading data from your storage account tooyour Azure SQL DW could take 20 minutes or longer.</span></span>  
> 
> 

<span data-ttu-id="d0511-182">Você terá que toodecide o que fazer se você tiver arquivos de destino e origem duplicada.</span><span class="sxs-lookup"><span data-stu-id="d0511-182">You will have toodecide what do if you have duplicate source and destination files.</span></span>

> [!NOTE]
> <span data-ttu-id="d0511-183">Se toobe de arquivos. csv Olá copiado da conta de armazenamento de blob particular Olá blob público armazenamento tooyour já existe em sua conta de armazenamento de blob particular, AzCopy perguntará se você quer toooverwrite-los.</span><span class="sxs-lookup"><span data-stu-id="d0511-183">If hello .csv files toobe copied from hello public blob storage tooyour private blob storage account already exist in your private blob storage account, AzCopy will ask you whether you want toooverwrite them.</span></span> <span data-ttu-id="d0511-184">Se você não quiser toooverwrite-los, entrada  **n**  quando solicitado.</span><span class="sxs-lookup"><span data-stu-id="d0511-184">If you do not want toooverwrite them, input **n** when prompted.</span></span> <span data-ttu-id="d0511-185">Se você quiser toooverwrite **todos os** , entrada **um** quando solicitado.</span><span class="sxs-lookup"><span data-stu-id="d0511-185">If you want toooverwrite **all** of them, input **a** when prompted.</span></span> <span data-ttu-id="d0511-186">Você também pode inserir **y** . toooverwrite CSV arquivos individualmente.</span><span class="sxs-lookup"><span data-stu-id="d0511-186">You can also input **y** toooverwrite .csv files individually.</span></span>
> 
> 

![Plotar nº 21][21]

<span data-ttu-id="d0511-188">Você pode usar seus próprios dados.</span><span class="sxs-lookup"><span data-stu-id="d0511-188">You can use your own data.</span></span> <span data-ttu-id="d0511-189">Se os dados estiverem em sua máquina local em seu aplicativo da vida real, você ainda pode usar o armazenamento de BLOBs do Azure privada AzCopy tooupload local dados tooyour.</span><span class="sxs-lookup"><span data-stu-id="d0511-189">If your data is in your on-premises machine in your real life application, you can still use AzCopy tooupload on-premises data tooyour private Azure blob storage.</span></span> <span data-ttu-id="d0511-190">Você só precisa Olá toochange **fonte** local, `$Source = "http://getgoing.blob.core.windows.net/public/nyctaxidataset"`, no hello comando AzCopy de saudação do PowerShell script arquivo toohello diretório local que contém os dados.</span><span class="sxs-lookup"><span data-stu-id="d0511-190">You only need toochange hello **Source** location, `$Source = "http://getgoing.blob.core.windows.net/public/nyctaxidataset"`, in hello AzCopy command of hello PowerShell script file toohello local directory that contains your data.</span></span>

> [!TIP]
> <span data-ttu-id="d0511-191">Se os dados já estão em seu armazenamento de BLOBs do Azure privada em seu aplicativo da vida real, você poderá ignorar Olá AzCopy etapa Olá script do PowerShell e carregar diretamente Olá tooAzure de dados SQL DW.</span><span class="sxs-lookup"><span data-stu-id="d0511-191">If your data is already in your private Azure blob storage in your real life application, you can skip hello AzCopy step in hello PowerShell script and directly upload hello data tooAzure SQL DW.</span></span> <span data-ttu-id="d0511-192">Isso exigirá adicionais edita de saudação script tootailor-toohello formato de seus dados.</span><span class="sxs-lookup"><span data-stu-id="d0511-192">This will require additional edits of hello script tootailor it toohello format of your data.</span></span>
> 
> 

<span data-ttu-id="d0511-193">Este script do Powershell também conecta-se em Olá informações do Azure SQL DW Olá dados exploração exemplo arquivos SQLDW_Explorations.sql, SQLDW_Explorations.ipynb e SQLDW_Explorations_Scripts.py para que esses três arquivos são toobe pronto testada instantaneamente Após a conclusão da saudação script do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d0511-193">This Powershell script also plugs in hello Azure SQL DW information into hello data exploration example files SQLDW_Explorations.sql, SQLDW_Explorations.ipynb, and SQLDW_Explorations_Scripts.py so that these three files are ready toobe tried out instantly after hello PowerShell script completes.</span></span>

<span data-ttu-id="d0511-194">Após a execução bem-sucedida, você verá uma tela parecida com a seguinte:</span><span class="sxs-lookup"><span data-stu-id="d0511-194">After a successful execution, you will see screen like below:</span></span>

![][20]

## <span data-ttu-id="d0511-195"><a name="dbexplore"></a>Exploração de dados e engenharia de recursos no SQL Data Warehouse do Azure</span><span class="sxs-lookup"><span data-stu-id="d0511-195"><a name="dbexplore"></a>Data exploration and feature engineering in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="d0511-196">Nesta seção, executamos a exploração de dados e a geração de recursos por meio da execução de consultas SQL no Azure SQL DW usando diretamente o **Visual Studio Data Tools**.</span><span class="sxs-lookup"><span data-stu-id="d0511-196">In this section, we perform data exploration and feature generation by running SQL queries against Azure SQL DW directly using **Visual Studio Data Tools**.</span></span> <span data-ttu-id="d0511-197">Todas as consultas SQL usadas nesta seção podem ser encontradas no script de exemplo hello chamado *SQLDW_Explorations.sql*.</span><span class="sxs-lookup"><span data-stu-id="d0511-197">All SQL queries used in this section can be found in hello sample script named *SQLDW_Explorations.sql*.</span></span> <span data-ttu-id="d0511-198">Este arquivo já foi baixado tooyour o diretório local pelo script do PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="d0511-198">This file has already been downloaded tooyour local directory by hello PowerShell script.</span></span> <span data-ttu-id="d0511-199">Você também pode recuperá-lo no [GitHub](https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/SQLDW/SQLDW_Explorations.sql).</span><span class="sxs-lookup"><span data-stu-id="d0511-199">You can also retrieve it from [GitHub](https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/SQLDW/SQLDW_Explorations.sql).</span></span> <span data-ttu-id="d0511-200">Mas o arquivo hello no GitHub não tem informações de DW do SQL Azure Olá conectadas.</span><span class="sxs-lookup"><span data-stu-id="d0511-200">But hello file in GitHub does not have hello Azure SQL DW information plugged in.</span></span>

<span data-ttu-id="d0511-201">Conecte-se tooyour DW do SQL Azure usando o Visual Studio com o nome de logon do SQL DW hello e a senha e abra a saudação **Pesquisador de objetos SQL** tabelas e o banco de dados do tooconfirm Olá foram importadas.</span><span class="sxs-lookup"><span data-stu-id="d0511-201">Connect tooyour Azure SQL DW using Visual Studio with hello SQL DW login name and password and open up hello **SQL Object Explorer** tooconfirm hello database and tables have been imported.</span></span> <span data-ttu-id="d0511-202">Recuperar Olá *SQLDW_Explorations.sql* arquivo.</span><span class="sxs-lookup"><span data-stu-id="d0511-202">Retrieve hello *SQLDW_Explorations.sql* file.</span></span>

> [!NOTE]
> <span data-ttu-id="d0511-203">tooopen um editor de consultas do Parallel Data Warehouse (PDW), use Olá **nova consulta** comando enquanto o PDW estiver selecionado na Olá **Pesquisador de objetos SQL**.</span><span class="sxs-lookup"><span data-stu-id="d0511-203">tooopen a Parallel Data Warehouse (PDW) query editor, use hello **New Query** command while your PDW is selected in hello **SQL Object Explorer**.</span></span> <span data-ttu-id="d0511-204">Não há suporte para o editor de consultas SQL padrão Olá no PDW.</span><span class="sxs-lookup"><span data-stu-id="d0511-204">hello standard SQL query editor is not supported by PDW.</span></span>
> 
> 

<span data-ttu-id="d0511-205">Aqui estão tipo hello de dados executadas as tarefas de geração de exploração e recurso nesta seção:</span><span class="sxs-lookup"><span data-stu-id="d0511-205">Here are hello type of data exploration and feature generation tasks performed in this section:</span></span>

* <span data-ttu-id="d0511-206">Explorar as distribuições de dados de alguns campos em períodos diferentes.</span><span class="sxs-lookup"><span data-stu-id="d0511-206">Explore data distributions of a few fields in varying time windows.</span></span>
* <span data-ttu-id="d0511-207">Investigue a qualidade dos dados dos campos de longitude e latitude hello.</span><span class="sxs-lookup"><span data-stu-id="d0511-207">Investigate data quality of hello longitude and latitude fields.</span></span>
* <span data-ttu-id="d0511-208">Gerar rótulos de classificação binária e multiclasse com base no hello **dica\_quantidade**.</span><span class="sxs-lookup"><span data-stu-id="d0511-208">Generate binary and multiclass classification labels based on hello **tip\_amount**.</span></span>
* <span data-ttu-id="d0511-209">Gerar recursos e computar/comparar as distâncias de viagem.</span><span class="sxs-lookup"><span data-stu-id="d0511-209">Generate features and compute/compare trip distances.</span></span>
* <span data-ttu-id="d0511-210">Unir Olá duas tabelas e extrair uma amostra aleatória que será usado toobuild modelos.</span><span class="sxs-lookup"><span data-stu-id="d0511-210">Join hello two tables and extract a random sample that will be used toobuild models.</span></span>

### <a name="data-import-verification"></a><span data-ttu-id="d0511-211">Verificação de importação de dados</span><span class="sxs-lookup"><span data-stu-id="d0511-211">Data import verification</span></span>
<span data-ttu-id="d0511-212">Essas consultas fornecem uma rápida verificação do número de saudação de linhas e colunas em Olá importar tabelas preenchidas anteriormente usando o bulk paralelo do Polybase,</span><span class="sxs-lookup"><span data-stu-id="d0511-212">These queries provide a quick verification of hello number of rows and columns in hello tables populated earlier using Polybase's parallel bulk import,</span></span>

    -- Report number of rows in table <nyctaxi_trip> without table scan
    SELECT SUM(rows) FROM sys.partitions WHERE object_id = OBJECT_ID('<schemaname>.<nyctaxi_trip>')

    -- Report number of columns in table <nyctaxi_trip>
    SELECT COUNT(*) FROM information_schema.columns WHERE table_name = '<nyctaxi_trip>' AND table_schema = '<schemaname>'

<span data-ttu-id="d0511-213">**Saída:** o resultado deve ser 173.179.759 linhas e 14 colunas.</span><span class="sxs-lookup"><span data-stu-id="d0511-213">**Output:** You should get 173,179,759 rows and 14 columns.</span></span>

### <a name="exploration-trip-distribution-by-medallion"></a><span data-ttu-id="d0511-214">Exploração: distribuição de corridas por licença</span><span class="sxs-lookup"><span data-stu-id="d0511-214">Exploration: Trip distribution by medallion</span></span>
<span data-ttu-id="d0511-215">Este exemplo de consulta identifica medallions hello (números de táxi) concluídas mais de 100 viagens dentro de um período de tempo especificado.</span><span class="sxs-lookup"><span data-stu-id="d0511-215">This example query identifies hello medallions (taxi numbers) that completed more than 100 trips within a specified time period.</span></span> <span data-ttu-id="d0511-216">consulta de saudação pode se beneficiar do acesso à tabela de saudação particionada porque ele está condicionado pelo esquema de partição de saudação do **retirada\_datetime**.</span><span class="sxs-lookup"><span data-stu-id="d0511-216">hello query would benefit from hello partitioned table access since it is conditioned by hello partition scheme of **pickup\_datetime**.</span></span> <span data-ttu-id="d0511-217">Consultar o conjunto de dados completo Olá também fará com que o uso de tabela particionada hello e/ou verificação de índice.</span><span class="sxs-lookup"><span data-stu-id="d0511-217">Querying hello full dataset will also make use of hello partitioned table and/or index scan.</span></span>

    SELECT medallion, COUNT(*)
    FROM <schemaname>.<nyctaxi_fare>
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    GROUP BY medallion
    HAVING COUNT(*) > 100

<span data-ttu-id="d0511-218">**Saída:** consulta Olá deve retornar uma tabela com linhas especificando medallions Olá 13,369 (táxis) e Olá número de viagem concluído por eles em 2013.</span><span class="sxs-lookup"><span data-stu-id="d0511-218">**Output:** hello query should return a table with rows specifying hello 13,369 medallions (taxis) and hello number of trip completed by them in 2013.</span></span> <span data-ttu-id="d0511-219">Olá última coluna contém a contagem de saudação do número de saudação de viagens concluída.</span><span class="sxs-lookup"><span data-stu-id="d0511-219">hello last column contains hello count of hello number of trips completed.</span></span>

### <a name="exploration-trip-distribution-by-medallion-and-hacklicense"></a><span data-ttu-id="d0511-220">Exploração: distribuição de corridas por medallion e hack_license</span><span class="sxs-lookup"><span data-stu-id="d0511-220">Exploration: Trip distribution by medallion and hack_license</span></span>
<span data-ttu-id="d0511-221">Este exemplo identifica medallions hello (táxi números) e hack_license números (drivers) concluídas mais de 100 viagens dentro de um período de tempo especificado.</span><span class="sxs-lookup"><span data-stu-id="d0511-221">This example identifies hello medallions (taxi numbers) and hack_license numbers (drivers) that completed more than 100 trips within a specified time period.</span></span>

    SELECT medallion, hack_license, COUNT(*)
    FROM <schemaname>.<nyctaxi_fare>
    WHERE pickup_datetime BETWEEN '20130101' AND '20130131'
    GROUP BY medallion, hack_license
    HAVING COUNT(*) > 100

<span data-ttu-id="d0511-222">**Saída:** consulta Olá deve retornar uma tabela com 13,369 linhas especificando Olá 13,369 carro/driver IDs que foram concluídas mais que 100 viagens 2013.</span><span class="sxs-lookup"><span data-stu-id="d0511-222">**Output:** hello query should return a table with 13,369 rows specifying hello 13,369 car/driver IDs that have completed more that 100 trips in 2013.</span></span> <span data-ttu-id="d0511-223">Olá última coluna contém a contagem de saudação do número de saudação de viagens concluída.</span><span class="sxs-lookup"><span data-stu-id="d0511-223">hello last column contains hello count of hello number of trips completed.</span></span>

### <a name="data-quality-assessment-verify-records-with-incorrect-longitude-andor-latitude"></a><span data-ttu-id="d0511-224">Avaliação de qualidade de dados: verificar registros com longitude e/ou latitude incorretos</span><span class="sxs-lookup"><span data-stu-id="d0511-224">Data quality assessment: Verify records with incorrect longitude and/or latitude</span></span>
<span data-ttu-id="d0511-225">Este exemplo examina se qualquer um dos campos de longitude e/ou latitude Olá conter um valor inválido (graus de radianos devem estar entre -90 e 90), ou ter (0, 0) coordenadas.</span><span class="sxs-lookup"><span data-stu-id="d0511-225">This example investigates if any of hello longitude and/or latitude fields either contain an invalid value (radian degrees should be between -90 and 90), or have (0, 0) coordinates.</span></span>

    SELECT COUNT(*) FROM <schemaname>.<nyctaxi_trip>
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    AND  (CAST(pickup_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(pickup_latitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_latitude AS float) NOT BETWEEN -90 AND 90
    OR    (pickup_longitude = '0' AND pickup_latitude = '0')
    OR    (dropoff_longitude = '0' AND dropoff_latitude = '0'))

<span data-ttu-id="d0511-226">**Saída:** consulta Olá retorna 837,467 viagens que têm campos inválidos de longitude e/ou latitude.</span><span class="sxs-lookup"><span data-stu-id="d0511-226">**Output:** hello query returns 837,467 trips that have invalid longitude and/or latitude fields.</span></span>

### <a name="exploration-tipped-vs-not-tipped-trips-distribution"></a><span data-ttu-id="d0511-227">Exploração: distribuição de corridas com gorjeta versus sem gorjeta</span><span class="sxs-lookup"><span data-stu-id="d0511-227">Exploration: Tipped vs. not tipped trips distribution</span></span>
<span data-ttu-id="d0511-228">Este exemplo localiza o número de saudação de viagens foram Oblíquo versus o número de saudação não foram Oblíquo em um período de tempo especificado (ou Olá conjunto de dados completo se abrangendo ano hello como ela é configurada aqui).</span><span class="sxs-lookup"><span data-stu-id="d0511-228">This example finds hello number of trips that were tipped vs. hello number that were not tipped in a specified time period (or in hello full dataset if covering hello full year as it is set up here).</span></span> <span data-ttu-id="d0511-229">Essa distribuição reflete Olá rótulo binário distribuição toobe usado posteriormente para modelagem de classificação binária.</span><span class="sxs-lookup"><span data-stu-id="d0511-229">This distribution reflects hello binary label distribution toobe later used for binary classification modeling.</span></span>

    SELECT tipped, COUNT(*) AS tip_freq FROM (
      SELECT CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END AS tipped, tip_amount
      FROM <schemaname>.<nyctaxi_fare>
      WHERE pickup_datetime BETWEEN '20130101' AND '20131231') tc
    GROUP BY tipped

<span data-ttu-id="d0511-230">**Saída:** Olá consulta deve seguir Olá retorno dica frequências para ano Olá Oblíquo 2013: 90,447,622 e 82,264,709-Oblíquo não.</span><span class="sxs-lookup"><span data-stu-id="d0511-230">**Output:** hello query should return hello following tip frequencies for hello year 2013: 90,447,622 tipped and 82,264,709 not-tipped.</span></span>

### <a name="exploration-tip-classrange-distribution"></a><span data-ttu-id="d0511-231">Exploração: distribuição de classe/intervalo de gorjetas</span><span class="sxs-lookup"><span data-stu-id="d0511-231">Exploration: Tip class/range distribution</span></span>
<span data-ttu-id="d0511-232">Esse exemplo calcula distribuição Olá de intervalos de dica em um tempo determinado período (ou em Olá conjunto de dados completo se abrangendo ano Olá).</span><span class="sxs-lookup"><span data-stu-id="d0511-232">This example computes hello distribution of tip ranges in a given time period (or in hello full dataset if covering hello full year).</span></span> <span data-ttu-id="d0511-233">Isso é a distribuição de saudação de classes de rótulo de saudação que serão usados posteriormente para modelagem de classificação multiclasse.</span><span class="sxs-lookup"><span data-stu-id="d0511-233">This is hello distribution of hello label classes that will be used later for multiclass classification modeling.</span></span>

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

<span data-ttu-id="d0511-234">**Saída:**</span><span class="sxs-lookup"><span data-stu-id="d0511-234">**Output:**</span></span>

| <span data-ttu-id="d0511-235">tip_class</span><span class="sxs-lookup"><span data-stu-id="d0511-235">tip_class</span></span> | <span data-ttu-id="d0511-236">tip_freq</span><span class="sxs-lookup"><span data-stu-id="d0511-236">tip_freq</span></span> |
| --- | --- |
| <span data-ttu-id="d0511-237">1</span><span class="sxs-lookup"><span data-stu-id="d0511-237">1</span></span> |<span data-ttu-id="d0511-238">82230915</span><span class="sxs-lookup"><span data-stu-id="d0511-238">82230915</span></span> |
| <span data-ttu-id="d0511-239">2</span><span class="sxs-lookup"><span data-stu-id="d0511-239">2</span></span> |<span data-ttu-id="d0511-240">6198803</span><span class="sxs-lookup"><span data-stu-id="d0511-240">6198803</span></span> |
| <span data-ttu-id="d0511-241">3</span><span class="sxs-lookup"><span data-stu-id="d0511-241">3</span></span> |<span data-ttu-id="d0511-242">1932223</span><span class="sxs-lookup"><span data-stu-id="d0511-242">1932223</span></span> |
| <span data-ttu-id="d0511-243">0</span><span class="sxs-lookup"><span data-stu-id="d0511-243">0</span></span> |<span data-ttu-id="d0511-244">82264625</span><span class="sxs-lookup"><span data-stu-id="d0511-244">82264625</span></span> |
| <span data-ttu-id="d0511-245">4</span><span class="sxs-lookup"><span data-stu-id="d0511-245">4</span></span> |<span data-ttu-id="d0511-246">85765</span><span class="sxs-lookup"><span data-stu-id="d0511-246">85765</span></span> |

### <a name="exploration-compute-and-compare-trip-distance"></a><span data-ttu-id="d0511-247">Exploração: calcular e comparar a distância da corrida</span><span class="sxs-lookup"><span data-stu-id="d0511-247">Exploration: Compute and compare trip distance</span></span>
<span data-ttu-id="d0511-248">Este exemplo converte a longitude de retirada e redistribuição hello e Geografia do latitude tooSQL pontos, calcula a distância de viagem hello usando o SQL geography pontos diferença e retorna uma amostra aleatória de resultados Olá para comparação.</span><span class="sxs-lookup"><span data-stu-id="d0511-248">This example converts hello pickup and drop-off longitude and latitude tooSQL geography points, computes hello trip distance using SQL geography points difference, and returns a random sample of hello results for comparison.</span></span> <span data-ttu-id="d0511-249">exemplo Hello limita os resultados de saudação toovalid coordena usando apenas a consulta de avaliação de qualidade dados Olá coberta anteriormente.</span><span class="sxs-lookup"><span data-stu-id="d0511-249">hello example limits hello results toovalid coordinates only using hello data quality assessment query covered earlier.</span></span>

    /****** Object:  UserDefinedFunction [dbo].[fnCalculateDistance] ******/
    SET ANSI_NULLS ON
    GO

    SET QUOTED_IDENTIFIER ON
    GO

    IF EXISTS (SELECT * FROM sys.objects WHERE type IN ('FN', 'IF') AND name = 'fnCalculateDistance')
      DROP FUNCTION fnCalculateDistance
    GO

    -- User-defined function toocalculate hello direct distance  in mile between two geographical coordinates.
    CREATE FUNCTION [dbo].[fnCalculateDistance] (@Lat1 float, @Long1 float, @Lat2 float, @Long2 float)

    RETURNS float
    AS
    BEGIN
          DECLARE @distance decimal(28, 10)
          -- Convert tooradians
          SET @Lat1 = @Lat1 / 57.2958
          SET @Long1 = @Long1 / 57.2958
          SET @Lat2 = @Lat2 / 57.2958
          SET @Long2 = @Long2 / 57.2958
          -- Calculate distance
          SET @distance = (SIN(@Lat1) * SIN(@Lat2)) + (COS(@Lat1) * COS(@Lat2) * COS(@Long2 - @Long1))
          --Convert toomiles
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

### <a name="feature-engineering-using-sql-functions"></a><span data-ttu-id="d0511-250">Engenharia de recursos usando funções SQL</span><span class="sxs-lookup"><span data-stu-id="d0511-250">Feature engineering using SQL functions</span></span>
<span data-ttu-id="d0511-251">Às vezes, as funções SQL podem ser uma opção eficiente para a engenharia de recursos.</span><span class="sxs-lookup"><span data-stu-id="d0511-251">Sometimes SQL functions can be an efficient option for feature engineering.</span></span> <span data-ttu-id="d0511-252">Neste passo a passo, definimos uma SQL função toocalculate Olá direta distância entre os locais de retirada e redução de saudação.</span><span class="sxs-lookup"><span data-stu-id="d0511-252">In this walkthrough, we defined a SQL function toocalculate hello direct distance between hello pickup and dropoff locations.</span></span> <span data-ttu-id="d0511-253">Você pode executar Olá scripts SQL a seguir **ferramentas de dados do Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="d0511-253">You can run hello following SQL scripts in **Visual Studio Data Tools**.</span></span>

<span data-ttu-id="d0511-254">Aqui está o script SQL Olá que define a função de distância hello.</span><span class="sxs-lookup"><span data-stu-id="d0511-254">Here is hello SQL script that defines hello distance function.</span></span>

    SET ANSI_NULLS ON
    GO

    SET QUOTED_IDENTIFIER ON
    GO

    IF EXISTS (SELECT * FROM sys.objects WHERE type IN ('FN', 'IF') AND name = 'fnCalculateDistance')
      DROP FUNCTION fnCalculateDistance
    GO

    -- User-defined function calculate hello direct distance between two geographical coordinates.
    CREATE FUNCTION [dbo].[fnCalculateDistance] (@Lat1 float, @Long1 float, @Lat2 float, @Long2 float)

    RETURNS float
    AS
    BEGIN
          DECLARE @distance decimal(28, 10)
          -- Convert tooradians
          SET @Lat1 = @Lat1 / 57.2958
          SET @Long1 = @Long1 / 57.2958
          SET @Lat2 = @Lat2 / 57.2958
          SET @Long2 = @Long2 / 57.2958
          -- Calculate distance
          SET @distance = (SIN(@Lat1) * SIN(@Lat2)) + (COS(@Lat1) * COS(@Lat2) * COS(@Long2 - @Long1))
          --Convert toomiles
          IF @distance <> 0
          BEGIN
            SET @distance = 3958.75 * ATAN(SQRT(1 - POWER(@distance, 2)) / @distance);
          END
          RETURN @distance
    END
    GO

<span data-ttu-id="d0511-255">Aqui está um exemplo toocall recursos de toogenerate essa função na consulta SQL:</span><span class="sxs-lookup"><span data-stu-id="d0511-255">Here is an example toocall this function toogenerate features in your SQL query:</span></span>

    -- Sample query toocall hello function toocreate features
    SELECT pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude,
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) AS DirectDistance
    FROM <schemaname>.<nyctaxi_trip>
    WHERE datepart("mi",pickup_datetime)=1
    AND CAST(pickup_latitude AS float) BETWEEN -90 AND 90
    AND CAST(dropoff_latitude AS float) BETWEEN -90 AND 90
    AND pickup_longitude != '0' AND dropoff_longitude != '0'

<span data-ttu-id="d0511-256">**Saída:** essa consulta gera uma tabela (com 2,803,538 linhas) com retirada e redução latitudes e longitudes e Olá correspondente direto distâncias em milhas.</span><span class="sxs-lookup"><span data-stu-id="d0511-256">**Output:** This query generates a table (with 2,803,538 rows) with pickup and dropoff latitudes and longitudes and hello corresponding direct distances in miles.</span></span> <span data-ttu-id="d0511-257">Estes são os resultados de saudação para primeiro 3 linhas:</span><span class="sxs-lookup"><span data-stu-id="d0511-257">Here are hello results for first 3 rows:</span></span>

|  | <span data-ttu-id="d0511-258">pickup_latitude</span><span class="sxs-lookup"><span data-stu-id="d0511-258">pickup_latitude</span></span> | <span data-ttu-id="d0511-259">pickup_longitude</span><span class="sxs-lookup"><span data-stu-id="d0511-259">pickup_longitude</span></span> | <span data-ttu-id="d0511-260">dropoff_latitude</span><span class="sxs-lookup"><span data-stu-id="d0511-260">dropoff_latitude</span></span> | <span data-ttu-id="d0511-261">dropoff_longitude</span><span class="sxs-lookup"><span data-stu-id="d0511-261">dropoff_longitude</span></span> | <span data-ttu-id="d0511-262">DirectDistance</span><span class="sxs-lookup"><span data-stu-id="d0511-262">DirectDistance</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="d0511-263">1</span><span class="sxs-lookup"><span data-stu-id="d0511-263">1</span></span> |<span data-ttu-id="d0511-264">40.731804</span><span class="sxs-lookup"><span data-stu-id="d0511-264">40.731804</span></span> |<span data-ttu-id="d0511-265">-74.001083</span><span class="sxs-lookup"><span data-stu-id="d0511-265">-74.001083</span></span> |<span data-ttu-id="d0511-266">40.736622</span><span class="sxs-lookup"><span data-stu-id="d0511-266">40.736622</span></span> |<span data-ttu-id="d0511-267">-73.988953</span><span class="sxs-lookup"><span data-stu-id="d0511-267">-73.988953</span></span> |<span data-ttu-id="d0511-268">.7169601222</span><span class="sxs-lookup"><span data-stu-id="d0511-268">.7169601222</span></span> |
| <span data-ttu-id="d0511-269">2</span><span class="sxs-lookup"><span data-stu-id="d0511-269">2</span></span> |<span data-ttu-id="d0511-270">40.715794</span><span class="sxs-lookup"><span data-stu-id="d0511-270">40.715794</span></span> |<span data-ttu-id="d0511-271">-74,010635</span><span class="sxs-lookup"><span data-stu-id="d0511-271">-74,010635</span></span> |<span data-ttu-id="d0511-272">40.725338</span><span class="sxs-lookup"><span data-stu-id="d0511-272">40.725338</span></span> |<span data-ttu-id="d0511-273">-74.00399</span><span class="sxs-lookup"><span data-stu-id="d0511-273">-74.00399</span></span> |<span data-ttu-id="d0511-274">.7448343721</span><span class="sxs-lookup"><span data-stu-id="d0511-274">.7448343721</span></span> |
| <span data-ttu-id="d0511-275">3</span><span class="sxs-lookup"><span data-stu-id="d0511-275">3</span></span> |<span data-ttu-id="d0511-276">40.761456</span><span class="sxs-lookup"><span data-stu-id="d0511-276">40.761456</span></span> |<span data-ttu-id="d0511-277">-73.999886</span><span class="sxs-lookup"><span data-stu-id="d0511-277">-73.999886</span></span> |<span data-ttu-id="d0511-278">40.766544</span><span class="sxs-lookup"><span data-stu-id="d0511-278">40.766544</span></span> |<span data-ttu-id="d0511-279">-73.988228</span><span class="sxs-lookup"><span data-stu-id="d0511-279">-73.988228</span></span> |<span data-ttu-id="d0511-280">0.7037227967</span><span class="sxs-lookup"><span data-stu-id="d0511-280">0.7037227967</span></span> |

### <a name="prepare-data-for-model-building"></a><span data-ttu-id="d0511-281">Preparar dados para criação de modelo</span><span class="sxs-lookup"><span data-stu-id="d0511-281">Prepare data for model building</span></span>
<span data-ttu-id="d0511-282">saudação de junções de consulta a seguir Olá **nyctaxi\_viagem** e **nyctaxi\_passagens** tabelas, gera um rótulo de classificação binária **Oblíquo**, um rótulo de classificação multiclasse **dica\_classe**e extrai um exemplo de hello ingressado no conjunto de dados completo.</span><span class="sxs-lookup"><span data-stu-id="d0511-282">hello following query joins hello **nyctaxi\_trip** and **nyctaxi\_fare** tables, generates a binary classification label **tipped**, a multi-class classification label **tip\_class**, and extracts a sample from hello full joined dataset.</span></span> <span data-ttu-id="d0511-283">amostragem de saudação é feita por recuperar um subconjunto de viagens de saudação com base na hora de retirada.</span><span class="sxs-lookup"><span data-stu-id="d0511-283">hello sampling is done by retrieving a subset of hello trips based on pickup time.</span></span>  <span data-ttu-id="d0511-284">Essa consulta pode ser copiada e colada diretamente no hello [estúdio de aprendizado de máquina do Azure](https://studio.azureml.net) [importar dados] [ import-data] módulo para a ingestão de dados direta da instância de banco de dados do SQL Olá no Azure.</span><span class="sxs-lookup"><span data-stu-id="d0511-284">This query can be copied then pasted directly in hello [Azure Machine Learning Studio](https://studio.azureml.net) [Import Data][import-data] module for direct data ingestion from hello SQL database instance in Azure.</span></span> <span data-ttu-id="d0511-285">consulta de saudação exclui registros com incorreto (0, 0) coordenadas.</span><span class="sxs-lookup"><span data-stu-id="d0511-285">hello query excludes records with incorrect (0, 0) coordinates.</span></span>

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

<span data-ttu-id="d0511-286">Quando você estiver pronto tooproceed tooAzure aprendizado de máquina, você pode:</span><span class="sxs-lookup"><span data-stu-id="d0511-286">When you are ready tooproceed tooAzure Machine Learning, you may either:</span></span>  

1. <span data-ttu-id="d0511-287">Salvar Olá final SQL consulta tooextract e exemplo hello dados e copiar e colar Olá consulta diretamente em um [importar dados] [ import-data] módulo no aprendizado de máquina do Azure, ou</span><span class="sxs-lookup"><span data-stu-id="d0511-287">Save hello final SQL query tooextract and sample hello data and copy-paste hello query directly into a [Import Data][import-data] module in Azure Machine Learning, or</span></span>
2. <span data-ttu-id="d0511-288">Persistir Olá amostrada e dados de engenharia planejar toouse para modelo de criação de um novo SQL DW tabela e usam a nova tabela de saudação em Olá [importar dados] [ import-data] módulo no aprendizado de máquina do Azure.</span><span class="sxs-lookup"><span data-stu-id="d0511-288">Persist hello sampled and engineered data you plan toouse for model building in a new SQL DW table and use hello new table in hello [Import Data][import-data] module in Azure Machine Learning.</span></span> <span data-ttu-id="d0511-289">Olá script do PowerShell na etapa anterior tenha feito isso para você.</span><span class="sxs-lookup"><span data-stu-id="d0511-289">hello PowerShell script in earlier step has done this for you.</span></span> <span data-ttu-id="d0511-290">Você pode ler diretamente a partir dessa tabela no módulo de importação de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="d0511-290">You can read directly from this table in hello Import Data module.</span></span>

## <span data-ttu-id="d0511-291"><a name="ipnb"></a>Exploração de dados e engenharia de recursos no IPython Notebook</span><span class="sxs-lookup"><span data-stu-id="d0511-291"><a name="ipnb"></a>Data exploration and feature engineering in IPython notebook</span></span>
<span data-ttu-id="d0511-292">Nesta seção, vamos realizar exploração de dados e geração de recurso usando ambos os Python e consultas SQL em relação a saudação SQL DW criado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="d0511-292">In this section, we will perform data exploration and feature generation using both Python and SQL queries against hello SQL DW created earlier.</span></span> <span data-ttu-id="d0511-293">Um bloco de anotações de IPython de exemplo chamado **SQLDW_Explorations.ipynb** e um arquivo de script de Python **SQLDW_Explorations_Scripts.py** ter sido baixado tooyour diretório de local.</span><span class="sxs-lookup"><span data-stu-id="d0511-293">A sample IPython notebook named **SQLDW_Explorations.ipynb** and a Python script file **SQLDW_Explorations_Scripts.py** have been downloaded tooyour local directory.</span></span> <span data-ttu-id="d0511-294">Eles também estão disponíveis no [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/SQLDW).</span><span class="sxs-lookup"><span data-stu-id="d0511-294">They are also available on [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/SQLDW).</span></span> <span data-ttu-id="d0511-295">Esses dois arquivos são idênticos em scripts Python.</span><span class="sxs-lookup"><span data-stu-id="d0511-295">These two files are identical in Python scripts.</span></span> <span data-ttu-id="d0511-296">arquivo de script de Python Olá é fornecido tooyou caso você não tiver um servidor de bloco de anotações do IPython.</span><span class="sxs-lookup"><span data-stu-id="d0511-296">hello Python script file is provided tooyou in case you do not have an IPython Notebook server.</span></span> <span data-ttu-id="d0511-297">Esses dois de exemplo de arquivo Python são criados no **Python 2.7**.</span><span class="sxs-lookup"><span data-stu-id="d0511-297">These two sample Python files are designed under **Python 2.7**.</span></span>

<span data-ttu-id="d0511-298">Olá informações necessárias do Azure SQL DW no exemplo hello bloco de anotações do IPython e Olá Python máquina local do script arquivo baixado tooyour foi conectada pelo script do PowerShell Olá anteriormente.</span><span class="sxs-lookup"><span data-stu-id="d0511-298">hello needed Azure SQL DW information in hello sample IPython Notebook and hello Python script file downloaded tooyour local machine has been plugged in by hello PowerShell script previously.</span></span> <span data-ttu-id="d0511-299">Eles são executáveis sem qualquer modificação.</span><span class="sxs-lookup"><span data-stu-id="d0511-299">They are executable without any modification.</span></span>

<span data-ttu-id="d0511-300">Se você já tiver configurado um espaço de trabalho do AzureML, você pode carregar exemplo hello serviço do bloco de anotações do IPython toohello AzureML IPython Notebook diretamente e iniciar a execução.</span><span class="sxs-lookup"><span data-stu-id="d0511-300">If you have already set up an AzureML workspace, you can directly upload hello sample IPython Notebook toohello AzureML IPython Notebook service and start running it.</span></span> <span data-ttu-id="d0511-301">Aqui estão Olá etapas tooupload tooAzureML serviço do bloco de anotações do IPython:</span><span class="sxs-lookup"><span data-stu-id="d0511-301">Here are hello steps tooupload tooAzureML IPython Notebook service:</span></span>

1. <span data-ttu-id="d0511-302">Faça logon no espaço de trabalho de AzureML tooyour, clique "Studio" na parte superior do hello e clique em "NOTEBOOKS" no lado esquerdo de saudação da página da web de saudação.</span><span class="sxs-lookup"><span data-stu-id="d0511-302">Log in tooyour AzureML workspace, click "Studio" at hello top, and click "NOTEBOOKS" on hello left side of hello web page.</span></span>
   
    ![Plotar nº 22][22]
2. <span data-ttu-id="d0511-304">Clique em "Novo" no canto inferior esquerdo Olá Olá web página e selecione "Python 2".</span><span class="sxs-lookup"><span data-stu-id="d0511-304">Click "NEW" on hello left bottom corner of hello web page, and select "Python 2".</span></span> <span data-ttu-id="d0511-305">Em seguida, fornecer um bloco de anotações de toohello de nome e clique em Olá marca de seleção toocreate Olá nova em branco bloco de anotações do IPython.</span><span class="sxs-lookup"><span data-stu-id="d0511-305">Then, provide a name toohello notebook and click hello check mark toocreate hello new blank IPython Notebook.</span></span>
   
    ![Plotar nº 23][23]
3. <span data-ttu-id="d0511-307">Clique Olá símbolo de "Jupyter" no canto superior esquerdo de saudação do hello novo bloco de anotações do IPython.</span><span class="sxs-lookup"><span data-stu-id="d0511-307">Click hello "Jupyter" symbol on hello left top corner of hello new IPython Notebook.</span></span>
   
    ![Plotar nº 24][24]
4. <span data-ttu-id="d0511-309">Arrastar e soltar Olá exemplo bloco de anotações do IPython toohello **árvore** página do seu serviço de bloco de anotações do AzureML IPython e clique em **carregar**.</span><span class="sxs-lookup"><span data-stu-id="d0511-309">Drag and drop hello sample IPython Notebook toohello **tree** page of your AzureML IPython Notebook service, and click **Upload**.</span></span> <span data-ttu-id="d0511-310">Em seguida, o exemplo hello bloco de anotações do IPython será carregado toohello serviço AzureML IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="d0511-310">Then, hello sample IPython Notebook will be uploaded toohello AzureML IPython Notebook service.</span></span>
   
    ![Plotar nº 25][25]

<span data-ttu-id="d0511-312">Na saudação de toorun de ordem de exemplo do bloco de anotações do IPython ou Olá o arquivo de script de Python, hello pacotes Python a seguir são necessários.</span><span class="sxs-lookup"><span data-stu-id="d0511-312">In order toorun hello sample IPython Notebook or hello Python script file, hello following Python packages are needed.</span></span> <span data-ttu-id="d0511-313">Se você estiver usando o serviço de bloco de anotações do AzureML IPython hello, esses pacotes foram previamente instalados.</span><span class="sxs-lookup"><span data-stu-id="d0511-313">If you are using hello AzureML IPython Notebook service, these packages have been pre-installed.</span></span>

    - <span data-ttu-id="d0511-314">pandas</span><span class="sxs-lookup"><span data-stu-id="d0511-314">pandas</span></span>
    - <span data-ttu-id="d0511-315">numpy</span><span class="sxs-lookup"><span data-stu-id="d0511-315">numpy</span></span>
    - <span data-ttu-id="d0511-316">matplotlib</span><span class="sxs-lookup"><span data-stu-id="d0511-316">matplotlib</span></span>
    - <span data-ttu-id="d0511-317">pyodbc</span><span class="sxs-lookup"><span data-stu-id="d0511-317">pyodbc</span></span>
    - <span data-ttu-id="d0511-318">PyTables</span><span class="sxs-lookup"><span data-stu-id="d0511-318">PyTables</span></span>

<span data-ttu-id="d0511-319">Olá recomendado sequência ao compilar soluções analíticas avançadas em AzureML com dados grandes é seguir hello:</span><span class="sxs-lookup"><span data-stu-id="d0511-319">hello recommended sequence when building advanced analytical solutions on AzureML with large data is hello following:</span></span>

* <span data-ttu-id="d0511-320">Ler em uma pequena amostra dos dados de saudação em um quadro de dados na memória.</span><span class="sxs-lookup"><span data-stu-id="d0511-320">Read in a small sample of hello data into an in-memory data frame.</span></span>
* <span data-ttu-id="d0511-321">Execute algumas visualizações e explorações usando Olá dados amostrados.</span><span class="sxs-lookup"><span data-stu-id="d0511-321">Perform some visualizations and explorations using hello sampled data.</span></span>
* <span data-ttu-id="d0511-322">Testar usando dados de amostra de saudação de engenharia de recurso.</span><span class="sxs-lookup"><span data-stu-id="d0511-322">Experiment with feature engineering using hello sampled data.</span></span>
* <span data-ttu-id="d0511-323">Para exploração de dados maior, manipulação de dados e de engenharia de recurso, use consultas de SQL do Python tooissue diretamente contra Olá SQL DW.</span><span class="sxs-lookup"><span data-stu-id="d0511-323">For larger data exploration, data manipulation and feature engineering, use Python tooissue SQL Queries directly against hello SQL DW.</span></span>
* <span data-ttu-id="d0511-324">Decida toobe de tamanho de exemplo de hello adequado para a criação do modelo de aprendizado de máquina do Azure.</span><span class="sxs-lookup"><span data-stu-id="d0511-324">Decide hello sample size toobe suitable for Azure Machine Learning model building.</span></span>

<span data-ttu-id="d0511-325">Estes de saudação são alguns exploração, visualização de dados e exemplos de engenharia de recurso.</span><span class="sxs-lookup"><span data-stu-id="d0511-325">hello followings are a few data exploration, data visualization, and feature engineering examples.</span></span> <span data-ttu-id="d0511-326">Mais explorações de dados podem ser encontradas no exemplo hello bloco de anotações do IPython e o arquivo de script de Python de exemplo hello.</span><span class="sxs-lookup"><span data-stu-id="d0511-326">More data explorations can be found in hello sample IPython Notebook and hello sample Python script file.</span></span>

### <a name="initialize-database-credentials"></a><span data-ttu-id="d0511-327">Inicializar as credenciais de banco de dados</span><span class="sxs-lookup"><span data-stu-id="d0511-327">Initialize database credentials</span></span>
<span data-ttu-id="d0511-328">Inicialize as configurações de conexão de banco de dados em Olá variáveis a seguir:</span><span class="sxs-lookup"><span data-stu-id="d0511-328">Initialize your database connection settings in hello following variables:</span></span>

    SERVER_NAME=<server name>
    DATABASE_NAME=<database name>
    USERID=<user name>
    PASSWORD=<password>
    DB_DRIVER = <database driver>

### <a name="create-database-connection"></a><span data-ttu-id="d0511-329">Criar conexão de banco de dados</span><span class="sxs-lookup"><span data-stu-id="d0511-329">Create database connection</span></span>
<span data-ttu-id="d0511-330">Aqui está a cadeia de caracteres de conexão de saudação que cria Olá conexão toohello banco de dados.</span><span class="sxs-lookup"><span data-stu-id="d0511-330">Here is hello connection string that creates hello connection toohello database.</span></span>

    CONNECTION_STRING = 'DRIVER={'+DRIVER+'};SERVER='+SERVER_NAME+';DATABASE='+DATABASE_NAME+';UID='+USERID+';PWD='+PASSWORD
    conn = pyodbc.connect(CONNECTION_STRING)

### <a name="report-number-of-rows-and-columns-in-table-nyctaxitrip"></a><span data-ttu-id="d0511-331">Relatar o número de linhas e colunas na tabela <nyctaxi_trip></span><span class="sxs-lookup"><span data-stu-id="d0511-331">Report number of rows and columns in table <nyctaxi_trip></span></span>
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

* <span data-ttu-id="d0511-332">Número total de linhas = 173179759</span><span class="sxs-lookup"><span data-stu-id="d0511-332">Total number of rows = 173179759</span></span>  
* <span data-ttu-id="d0511-333">Número total de colunas = 14</span><span class="sxs-lookup"><span data-stu-id="d0511-333">Total number of columns = 14</span></span>

### <a name="report-number-of-rows-and-columns-in-table-nyctaxifare"></a><span data-ttu-id="d0511-334">Relatar o número de linhas e colunas na tabela <nyctaxi_fare></span><span class="sxs-lookup"><span data-stu-id="d0511-334">Report number of rows and columns in table <nyctaxi_fare></span></span>
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

* <span data-ttu-id="d0511-335">Número total de linhas = 173179759</span><span class="sxs-lookup"><span data-stu-id="d0511-335">Total number of rows = 173179759</span></span>  
* <span data-ttu-id="d0511-336">Número total de colunas = 11</span><span class="sxs-lookup"><span data-stu-id="d0511-336">Total number of columns = 11</span></span>

### <a name="read-in-a-small-data-sample-from-hello-sql-data-warehouse-database"></a><span data-ttu-id="d0511-337">Leitura-em uma amostra de dados pequenos de saudação banco de dados do SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="d0511-337">Read-in a small data sample from hello SQL Data Warehouse Database</span></span>
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
    print 'Time tooread hello sample table is %f seconds' % (t1-t0)

    print 'Number of rows and columns retrieved = (%d, %d)' % (df1.shape[0], df1.shape[1])

<span data-ttu-id="d0511-338">Tabela de exemplo do tempo tooread Olá é 14.096495 segundos.</span><span class="sxs-lookup"><span data-stu-id="d0511-338">Time tooread hello sample table is 14.096495 seconds.</span></span>  
<span data-ttu-id="d0511-339">Número de linhas e colunas recuperadas = (1000, 21).</span><span class="sxs-lookup"><span data-stu-id="d0511-339">Number of rows and columns retrieved = (1000, 21).</span></span>

### <a name="descriptive-statistics"></a><span data-ttu-id="d0511-340">Estatísticas descritivas</span><span class="sxs-lookup"><span data-stu-id="d0511-340">Descriptive statistics</span></span>
<span data-ttu-id="d0511-341">Agora você está pronto tooexplore dados de saudação de amostra.</span><span class="sxs-lookup"><span data-stu-id="d0511-341">Now you are ready tooexplore hello sampled data.</span></span> <span data-ttu-id="d0511-342">Vamos começar com olhando algumas estatísticas descritivas para Olá **viagem\_distância** (ou todos os outros campos que você escolher toospecify).</span><span class="sxs-lookup"><span data-stu-id="d0511-342">We start with looking at some descriptive statistics for hello **trip\_distance** (or any other fields you choose toospecify).</span></span>

    df1['trip_distance'].describe()

### <a name="visualization-box-plot-example"></a><span data-ttu-id="d0511-343">Visualização: exemplo de plotagem da caixa</span><span class="sxs-lookup"><span data-stu-id="d0511-343">Visualization: Box plot example</span></span>
<span data-ttu-id="d0511-344">Em seguida, vamos examinar diagrama em caixa Olá para Olá trip distância toovisualize Olá quantis.</span><span class="sxs-lookup"><span data-stu-id="d0511-344">Next we look at hello box plot for hello trip distance toovisualize hello quantiles.</span></span>

    df1.boxplot(column='trip_distance',return_type='dict')

![Plotar nº 1][1]

### <a name="visualization-distribution-plot-example"></a><span data-ttu-id="d0511-346">Visualização: exemplo de plotagem de distribuição</span><span class="sxs-lookup"><span data-stu-id="d0511-346">Visualization: Distribution plot example</span></span>
<span data-ttu-id="d0511-347">Gráficos que visualizam distribuição hello e um histograma para Olá amostragem distâncias de viagem.</span><span class="sxs-lookup"><span data-stu-id="d0511-347">Plots that visualize hello distribution and a histogram for hello sampled trip distances.</span></span>

    fig = plt.figure()
    ax1 = fig.add_subplot(1,2,1)
    ax2 = fig.add_subplot(1,2,2)
    df1['trip_distance'].plot(ax=ax1,kind='kde', style='b-')
    df1['trip_distance'].hist(ax=ax2, bins=100, color='k')

![Plotar nº 2][2]

### <a name="visualization-bar-and-line-plots"></a><span data-ttu-id="d0511-349">Visualização: plotagens de barra e linha</span><span class="sxs-lookup"><span data-stu-id="d0511-349">Visualization: Bar and line plots</span></span>
<span data-ttu-id="d0511-350">Neste exemplo, podemos guardar a distância de viagem de saudação em cinco compartimentos e visualizar Olá compartimentação de resultados.</span><span class="sxs-lookup"><span data-stu-id="d0511-350">In this example, we bin hello trip distance into five bins and visualize hello binning results.</span></span>

    trip_dist_bins = [0, 1, 2, 4, 10, 1000]
    df1['trip_distance']
    trip_dist_bin_id = pd.cut(df1['trip_distance'], trip_dist_bins)
    trip_dist_bin_id

<span data-ttu-id="d0511-351">Podemos plotar Olá acima distribuição bin em uma barra ou linha plotagem com:</span><span class="sxs-lookup"><span data-stu-id="d0511-351">We can plot hello above bin distribution in a bar or line plot with:</span></span>

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='bar')

![Plotar nº 3][3]

<span data-ttu-id="d0511-353">e</span><span class="sxs-lookup"><span data-stu-id="d0511-353">and</span></span>

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='line')

![Plotar nº 4][4]

### <a name="visualization-scatterplot-examples"></a><span data-ttu-id="d0511-355">Visualização: exemplo de plotagem de dispersão</span><span class="sxs-lookup"><span data-stu-id="d0511-355">Visualization: Scatterplot examples</span></span>
<span data-ttu-id="d0511-356">Vamos mostrar gráfico de dispersão entre **viagem\_tempo\_na\_s** e **viagem\_distância** toosee se há qualquer correlação</span><span class="sxs-lookup"><span data-stu-id="d0511-356">We show scatter plot between **trip\_time\_in\_secs** and **trip\_distance** toosee if there is any correlation</span></span>

    plt.scatter(df1['trip_time_in_secs'], df1['trip_distance'])

![Plotar nº 6][6]

<span data-ttu-id="d0511-358">Da mesma forma, é possível verificar a relação Olá entre **taxa\_código** e **viagem\_distância**.</span><span class="sxs-lookup"><span data-stu-id="d0511-358">Similarly we can check hello relationship between **rate\_code** and **trip\_distance**.</span></span>

    plt.scatter(df1['passenger_count'], df1['trip_distance'])

![Plotar nº 8][8]

### <a name="data-exploration-on-sampled-data-using-sql-queries-in-ipython-notebook"></a><span data-ttu-id="d0511-360">Exploração de dados em exemplos de dados usando consultas SQL no notebook IPython</span><span class="sxs-lookup"><span data-stu-id="d0511-360">Data exploration on sampled data using SQL queries in IPython notebook</span></span>
<span data-ttu-id="d0511-361">Nesta seção, exploraremos distribuições de dados usando dados de amostra de saudação que são persistidos em nova tabela de saudação criado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="d0511-361">In this section, we explore data distributions using hello sampled data which is persisted in hello new table we created above.</span></span> <span data-ttu-id="d0511-362">Observe que explorações semelhantes podem ser realizadas usando tabelas originais hello.</span><span class="sxs-lookup"><span data-stu-id="d0511-362">Note that similar explorations can be performed using hello original tables.</span></span>

#### <a name="exploration-report-number-of-rows-and-columns-in-hello-sampled-table"></a><span data-ttu-id="d0511-363">Exploração: Número de linhas e colunas de saudação do relatório tabela de amostra</span><span class="sxs-lookup"><span data-stu-id="d0511-363">Exploration: Report number of rows and columns in hello sampled table</span></span>
    nrows = pd.read_sql('''SELECT SUM(rows) FROM sys.partitions WHERE object_id = OBJECT_ID('<schemaname>.<nyctaxi_sample>')''', conn)
    print 'Number of rows in sample = %d' % nrows.iloc[0,0]

    ncols = pd.read_sql('''SELECT count(*) FROM information_schema.columns WHERE table_name = ('<nyctaxi_sample>') AND table_schema = '<schemaname>'''', conn)
    print 'Number of columns in sample = %d' % ncols.iloc[0,0]

#### <a name="exploration-tippednot-tripped-distribution"></a><span data-ttu-id="d0511-364">Exploração: distribuição de corridas com gorjeta e sem gorjeta</span><span class="sxs-lookup"><span data-stu-id="d0511-364">Exploration: Tipped/not tripped Distribution</span></span>
    query = '''
        SELECT tipped, count(*) AS tip_freq
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY tipped
        '''

    pd.read_sql(query, conn)

#### <a name="exploration-tip-class-distribution"></a><span data-ttu-id="d0511-365">Exploração: distribuição de classe de gorjetas</span><span class="sxs-lookup"><span data-stu-id="d0511-365">Exploration: Tip class distribution</span></span>
    query = '''
        SELECT tip_class, count(*) AS tip_freq
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY tip_class
    '''

    tip_class_dist = pd.read_sql(query, conn)

#### <a name="exploration-plot-hello-tip-distribution-by-class"></a><span data-ttu-id="d0511-366">Exploração: Plotar a distribuição de dica Olá pela classe</span><span class="sxs-lookup"><span data-stu-id="d0511-366">Exploration: Plot hello tip distribution by class</span></span>
    tip_class_dist['tip_freq'].plot(kind='bar')

![Plotar nº 26][26]

#### <a name="exploration-daily-distribution-of-trips"></a><span data-ttu-id="d0511-368">Exploração: distribuição diária de corridas</span><span class="sxs-lookup"><span data-stu-id="d0511-368">Exploration: Daily distribution of trips</span></span>
    query = '''
        SELECT CONVERT(date, dropoff_datetime) AS date, COUNT(*) AS c
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY CONVERT(date, dropoff_datetime)
    '''

    pd.read_sql(query,conn)

#### <a name="exploration-trip-distribution-per-medallion"></a><span data-ttu-id="d0511-369">Exploração: distribuição de corridas por licença</span><span class="sxs-lookup"><span data-stu-id="d0511-369">Exploration: Trip distribution per medallion</span></span>
    query = '''
        SELECT medallion,count(*) AS c
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY medallion
    '''

    pd.read_sql(query,conn)

#### <a name="exploration-trip-distribution-by-medallion-and-hack-license"></a><span data-ttu-id="d0511-370">Exploração: distribuição de corridas por medalhão e carteira de habilitação</span><span class="sxs-lookup"><span data-stu-id="d0511-370">Exploration: Trip distribution by medallion and hack license</span></span>
    query = '''select medallion, hack_license,count(*) from <schemaname>.<nyctaxi_sample> group by medallion, hack_license'''
    pd.read_sql(query,conn)


#### <a name="exploration-trip-time-distribution"></a><span data-ttu-id="d0511-371">Exploração: distribuição de horário das corridas</span><span class="sxs-lookup"><span data-stu-id="d0511-371">Exploration: Trip time distribution</span></span>
    query = '''select trip_time_in_secs, count(*) from <schemaname>.<nyctaxi_sample> group by trip_time_in_secs order by count(*) desc'''
    pd.read_sql(query,conn)

#### <a name="exploration-trip-distance-distribution"></a><span data-ttu-id="d0511-372">Exploração: distribuição da distância das corridas</span><span class="sxs-lookup"><span data-stu-id="d0511-372">Exploration: Trip distance distribution</span></span>
    query = '''select floor(trip_distance/5)*5 as tripbin, count(*) from <schemaname>.<nyctaxi_sample> group by floor(trip_distance/5)*5 order by count(*) desc'''
    pd.read_sql(query,conn)

#### <a name="exploration-payment-type-distribution"></a><span data-ttu-id="d0511-373">Exploração: distribuição do tipo de pagamento</span><span class="sxs-lookup"><span data-stu-id="d0511-373">Exploration: Payment type distribution</span></span>
    query = '''select payment_type,count(*) from <schemaname>.<nyctaxi_sample> group by payment_type'''
    pd.read_sql(query,conn)

#### <a name="verify-hello-final-form-of-hello-featurized-table"></a><span data-ttu-id="d0511-374">Verifique se a forma final de saudação da tabela de featurized Olá</span><span class="sxs-lookup"><span data-stu-id="d0511-374">Verify hello final form of hello featurized table</span></span>
    query = '''SELECT TOP 100 * FROM <schemaname>.<nyctaxi_sample>'''
    pd.read_sql(query,conn)

## <span data-ttu-id="d0511-375">
            <a name="mlmodel">
            </a>Compilar modelos no Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="d0511-375"><a name="mlmodel"></a>Build models in Azure Machine Learning</span></span>
<span data-ttu-id="d0511-376">Agora, estamos prontos tooproceed toomodel criação e implantação de modelo no [aprendizado de máquina do Azure](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="d0511-376">We are now ready tooproceed toomodel building and model deployment in [Azure Machine Learning](https://studio.azureml.net).</span></span> <span data-ttu-id="d0511-377">saudação de dados é pronto toobe usada em qualquer um dos problemas de previsão Olá identificados anteriormente, ou seja:</span><span class="sxs-lookup"><span data-stu-id="d0511-377">hello data is ready toobe used in any of hello prediction problems identified earlier, namely:</span></span>

1. <span data-ttu-id="d0511-378">**Classificação binária**: toopredict ou não uma dica foi pago uma viagem.</span><span class="sxs-lookup"><span data-stu-id="d0511-378">**Binary classification**: toopredict whether or not a tip was paid for a trip.</span></span>
2. <span data-ttu-id="d0511-379">**Classificação multiclasse**: intervalo de saudação toopredict de dica pago, de acordo com toohello classes definidas anteriormente.</span><span class="sxs-lookup"><span data-stu-id="d0511-379">**Multiclass classification**: toopredict hello range of tip paid, according toohello previously defined classes.</span></span>
3. <span data-ttu-id="d0511-380">**Tarefa de regressão**: o valor de saudação toopredict de dica pago para uma viagem.</span><span class="sxs-lookup"><span data-stu-id="d0511-380">**Regression task**: toopredict hello amount of tip paid for a trip.</span></span>  

<span data-ttu-id="d0511-381">toobegin Olá exercício de modelagem, faça logon no tooyour **aprendizado de máquina do Azure** espaço de trabalho.</span><span class="sxs-lookup"><span data-stu-id="d0511-381">toobegin hello modeling exercise, log in tooyour **Azure Machine Learning** workspace.</span></span> <span data-ttu-id="d0511-382">Se você ainda não tiver criado uma espaço de trabalho de aprendizado de máquina, consulte [Criar um espaço de trabalho de AM do Azure](machine-learning-create-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="d0511-382">If you have not yet created a machine learning workspace, see [Create an Azure ML workspace](machine-learning-create-workspace.md).</span></span>

1. <span data-ttu-id="d0511-383">tooget iniciado com o aprendizado de máquina do Azure, consulte [o que é o estúdio de aprendizado de máquina do Azure?](machine-learning-what-is-ml-studio.md)</span><span class="sxs-lookup"><span data-stu-id="d0511-383">tooget started with Azure Machine Learning, see [What is Azure Machine Learning Studio?](machine-learning-what-is-ml-studio.md)</span></span>
2. <span data-ttu-id="d0511-384">Faça logon no muito[estúdio de aprendizado de máquina do Azure](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="d0511-384">Log in too[Azure Machine Learning Studio](https://studio.azureml.net).</span></span>
3. <span data-ttu-id="d0511-385">Olá Studio Home page do fornece uma grande quantidade de informações, vídeos, tutoriais, links toohello Referência de módulos e outros recursos.</span><span class="sxs-lookup"><span data-stu-id="d0511-385">hello Studio Home page provides a wealth of information, videos, tutorials, links toohello Modules Reference, and other resources.</span></span> <span data-ttu-id="d0511-386">Para obter mais informações sobre o aprendizado de máquina do Azure, consulte Olá [Centro de documentação do aprendizado de máquina do Azure](https://azure.microsoft.com/documentation/services/machine-learning/).</span><span class="sxs-lookup"><span data-stu-id="d0511-386">For more information about Azure Machine Learning, consult hello [Azure Machine Learning Documentation Center](https://azure.microsoft.com/documentation/services/machine-learning/).</span></span>

<span data-ttu-id="d0511-387">Uma experiência de treinamento típico consiste Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="d0511-387">A typical training experiment consists of hello following steps:</span></span>

1. <span data-ttu-id="d0511-388">Criar uma experiência **+NEW** .</span><span class="sxs-lookup"><span data-stu-id="d0511-388">Create a **+NEW** experiment.</span></span>
2. <span data-ttu-id="d0511-389">Obter dados de saudação no Azure ML.</span><span class="sxs-lookup"><span data-stu-id="d0511-389">Get hello data into Azure ML.</span></span>
3. <span data-ttu-id="d0511-390">Pré-processar, transformar e manipular dados saudação conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="d0511-390">Pre-process, transform and manipulate hello data as needed.</span></span>
4. <span data-ttu-id="d0511-391">Gerar recursos conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="d0511-391">Generate features as needed.</span></span>
5. <span data-ttu-id="d0511-392">Dividir dados saudação em conjuntos de dados de treinamento / / teste de validação (ou têm conjuntos de dados separados para cada).</span><span class="sxs-lookup"><span data-stu-id="d0511-392">Split hello data into training/validation/testing datasets(or have separate datasets for each).</span></span>
6. <span data-ttu-id="d0511-393">Selecione um ou mais algoritmos dependendo Olá toosolve problema de aprendizado de aprendizado de máquina.</span><span class="sxs-lookup"><span data-stu-id="d0511-393">Select one or more machine learning algorithms depending on hello learning problem toosolve.</span></span> <span data-ttu-id="d0511-394">Por exemplo, classificação binária, classificação multiclasse ou regressão.</span><span class="sxs-lookup"><span data-stu-id="d0511-394">E.g., binary classification, multiclass classification, regression.</span></span>
7. <span data-ttu-id="d0511-395">Treine um ou mais modelos usando o conjunto de dados de treinamento hello.</span><span class="sxs-lookup"><span data-stu-id="d0511-395">Train one or more models using hello training dataset.</span></span>
8. <span data-ttu-id="d0511-396">Classificar o conjunto de dados de validação de saudação usando modelos treinados hello.</span><span class="sxs-lookup"><span data-stu-id="d0511-396">Score hello validation dataset using hello trained model(s).</span></span>
9. <span data-ttu-id="d0511-397">Avalie Olá modelos toocompute Olá relevante de métricas para Olá problema de aprendizado.</span><span class="sxs-lookup"><span data-stu-id="d0511-397">Evaluate hello model(s) toocompute hello relevant metrics for hello learning problem.</span></span>
10. <span data-ttu-id="d0511-398">Ajuste Olá modelo (s) e selecione Olá melhor modelo toodeploy.</span><span class="sxs-lookup"><span data-stu-id="d0511-398">Fine tune hello model(s) and select hello best model toodeploy.</span></span>

<span data-ttu-id="d0511-399">Neste exercício, podemos ter já explorados engenharia dados Olá no SQL Data Warehouse e decidido Olá tooingest de tamanho de exemplo no Azure ML.</span><span class="sxs-lookup"><span data-stu-id="d0511-399">In this exercise, we have already explored and engineered hello data in SQL Data Warehouse, and decided on hello sample size tooingest in Azure ML.</span></span> <span data-ttu-id="d0511-400">Aqui está o hello procedimento toobuild um ou mais dos modelos de previsão hello:</span><span class="sxs-lookup"><span data-stu-id="d0511-400">Here is hello procedure toobuild one or more of hello prediction models:</span></span>

1. <span data-ttu-id="d0511-401">Obter dados de saudação no Azure ML usando Olá [importar dados] [ import-data] módulo, disponível no hello **dados de entrada e saída** seção.</span><span class="sxs-lookup"><span data-stu-id="d0511-401">Get hello data into Azure ML using hello [Import Data][import-data] module, available in hello **Data Input and Output** section.</span></span> <span data-ttu-id="d0511-402">Para obter mais informações, consulte Olá [importar dados] [ import-data] página de referência de módulo.</span><span class="sxs-lookup"><span data-stu-id="d0511-402">For more information, see hello [Import Data][import-data] module reference page.</span></span>
   
    ![Dados de Importação de AM do Azure][17]
2. <span data-ttu-id="d0511-404">Selecione **banco de dados do SQL Azure** como Olá **fonte de dados** em Olá **propriedades** painel.</span><span class="sxs-lookup"><span data-stu-id="d0511-404">Select **Azure SQL Database** as hello **Data source** in hello **Properties** panel.</span></span>
3. <span data-ttu-id="d0511-405">Digite o nome DNS de banco de dados de saudação em Olá **nome do servidor de banco de dados** campo.</span><span class="sxs-lookup"><span data-stu-id="d0511-405">Enter hello database DNS name in hello **Database server name** field.</span></span> <span data-ttu-id="d0511-406">Formato: `tcp:<your_virtual_machine_DNS_name>,1433`</span><span class="sxs-lookup"><span data-stu-id="d0511-406">Format: `tcp:<your_virtual_machine_DNS_name>,1433`</span></span>
4. <span data-ttu-id="d0511-407">Digite hello **nome do banco de dados** no campo correspondente do hello.</span><span class="sxs-lookup"><span data-stu-id="d0511-407">Enter hello **Database name** in hello corresponding field.</span></span>
5. <span data-ttu-id="d0511-408">Digite hello *nome de usuário do SQL* em Olá **nome de conta de usuário do servidor**e hello *senha* em Olá **senha de conta de usuário do servidor**.</span><span class="sxs-lookup"><span data-stu-id="d0511-408">Enter hello *SQL user name* in hello **Server user account name**, and hello *password* in hello **Server user account password**.</span></span>
6. <span data-ttu-id="d0511-409">Verificar Olá **aceitar qualquer certificado de servidor** opção.</span><span class="sxs-lookup"><span data-stu-id="d0511-409">Check hello **Accept any server certificate** option.</span></span>
7. <span data-ttu-id="d0511-410">Em Olá **consulta de banco de dados** editar a área de texto, cole a consulta Olá extrai Olá necessário campos (incluindo quaisquer campos calculados como rótulos de saudação) de banco de dados e para baixo amostras de tamanho de exemplo hello dados toohello desejado.</span><span class="sxs-lookup"><span data-stu-id="d0511-410">In hello **Database query** edit text area, paste hello query which extracts hello necessary database fields (including any computed fields such as hello labels) and down samples hello data toohello desired sample size.</span></span>

<span data-ttu-id="d0511-411">É um exemplo de um experimento de classificação binária ler dados diretamente do banco de dados do SQL Data Warehouse Olá figura de saudação abaixo (Lembre-se de tooreplace Olá nomes de tabelas nyctaxi_trip e nyctaxi_fare pelo esquema Olá nome e hello nomes de tabela usado no seu instruções passo a passo).</span><span class="sxs-lookup"><span data-stu-id="d0511-411">An example of a binary classification experiment reading data directly from hello SQL Data Warehouse database is in hello figure below (remember tooreplace hello table names nyctaxi_trip and nyctaxi_fare by hello schema name and hello table names you used in your walkthrough).</span></span> <span data-ttu-id="d0511-412">Experimentos semelhantes podem ser construídos por meio de classificação multiclasse e problemas de regressão.</span><span class="sxs-lookup"><span data-stu-id="d0511-412">Similar experiments can be constructed for multiclass classification and regression problems.</span></span>

![Treino do AM do Azure][10]

> [!IMPORTANT]
> <span data-ttu-id="d0511-414">Em Olá modelagem de extração de dados e exemplos de consulta fornecidos nas seções anteriores, de amostragem **todos os rótulos para os exercícios de modelagem Olá três são incluídos na consulta Olá**.</span><span class="sxs-lookup"><span data-stu-id="d0511-414">In hello modeling data extraction and sampling query examples provided in previous sections, **all labels for hello three modeling exercises are included in hello query**.</span></span> <span data-ttu-id="d0511-415">Uma etapa importante (obrigatório) em cada Olá exercícios de modelagem é muito**excluir** Olá rótulos desnecessários para Olá outros dois problemas e qualquer outro **vazamentos de destino**.</span><span class="sxs-lookup"><span data-stu-id="d0511-415">An important (required) step in each of hello modeling exercises is too**exclude** hello unnecessary labels for hello other two problems, and any other **target leaks**.</span></span> <span data-ttu-id="d0511-416">Por exemplo, ao usar classificação binária, use o rótulo de saudação **Oblíquo** e excluir campos Olá **dica\_classe**, **dica\_quantidade**, e **total\_quantidade**.</span><span class="sxs-lookup"><span data-stu-id="d0511-416">For example, when using binary classification, use hello label **tipped** and exclude hello fields **tip\_class**, **tip\_amount**, and **total\_amount**.</span></span> <span data-ttu-id="d0511-417">Olá último vazamentos de destino já que eles implicam dica Olá pagas.</span><span class="sxs-lookup"><span data-stu-id="d0511-417">hello latter are target leaks since they imply hello tip paid.</span></span>
> 
> <span data-ttu-id="d0511-418">tooexclude quaisquer colunas desnecessárias ou vazamentos de destino, você pode usar o hello [selecionar colunas no conjunto de dados] [ select-columns] módulo ou hello [editar metadados] [ edit-metadata].</span><span class="sxs-lookup"><span data-stu-id="d0511-418">tooexclude any unnecessary columns or target leaks, you may use hello [Select Columns in Dataset][select-columns] module or hello [Edit Metadata][edit-metadata].</span></span> <span data-ttu-id="d0511-419">Para saber mais, veja as páginas de referência [Selecionar Colunas no Conjunto de Dados][select-columns] e [Editar Metadados][edit-metadata].</span><span class="sxs-lookup"><span data-stu-id="d0511-419">For more information, see [Select Columns in Dataset][select-columns] and [Edit Metadata][edit-metadata] reference pages.</span></span>
> 
> 

## <span data-ttu-id="d0511-420">
            <a name="mldeploy">
            </a>Implantar modelos no Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="d0511-420"><a name="mldeploy"></a>Deploy models in Azure Machine Learning</span></span>
<span data-ttu-id="d0511-421">Quando o modelo estiver pronto, pode facilmente implantá-lo como um serviço web diretamente do experimento hello.</span><span class="sxs-lookup"><span data-stu-id="d0511-421">When your model is ready, you can easily deploy it as a web service directly from hello experiment.</span></span> <span data-ttu-id="d0511-422">Para obter mais informações sobre como implantar os serviços Web do AM do Azure, veja [Implantar um serviço Web do Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="d0511-422">For more information about deploying Azure ML web services, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

<span data-ttu-id="d0511-423">toodeploy um novo serviço da web, você precisa:</span><span class="sxs-lookup"><span data-stu-id="d0511-423">toodeploy a new web service, you need to:</span></span>

1. <span data-ttu-id="d0511-424">Criar um experimento de pontuação.</span><span class="sxs-lookup"><span data-stu-id="d0511-424">Create a scoring experiment.</span></span>
2. <span data-ttu-id="d0511-425">Implante o serviço web de saudação.</span><span class="sxs-lookup"><span data-stu-id="d0511-425">Deploy hello web service.</span></span>

<span data-ttu-id="d0511-426">toocreate experiência de uma pontuação de um **concluído** experiência de treinamento, clique em **criar experiência de PONTUAÇÃO** na barra de ação inferior hello.</span><span class="sxs-lookup"><span data-stu-id="d0511-426">toocreate a scoring experiment from a **Finished** training experiment, click **CREATE SCORING EXPERIMENT** in hello lower action bar.</span></span>

![Pontuação do Azure][18]

<span data-ttu-id="d0511-428">O aprendizado de máquina do Azure tentará toocreate uma experiência de pontuação com base nos componentes de saudação da experiência de treinamento hello.</span><span class="sxs-lookup"><span data-stu-id="d0511-428">Azure Machine Learning will attempt toocreate a scoring experiment based on hello components of hello training experiment.</span></span> <span data-ttu-id="d0511-429">Em especial, ele vai:</span><span class="sxs-lookup"><span data-stu-id="d0511-429">In particular, it will:</span></span>

1. <span data-ttu-id="d0511-430">Salvar modelo treinado hello e remover os módulos de treinamento de modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="d0511-430">Save hello trained model and remove hello model training modules.</span></span>
2. <span data-ttu-id="d0511-431">Identificar uma lógica **porta de entrada** toorepresent Olá esperado o esquema de dados de entrada.</span><span class="sxs-lookup"><span data-stu-id="d0511-431">Identify a logical **input port** toorepresent hello expected input data schema.</span></span>
3. <span data-ttu-id="d0511-432">Identificar uma lógica **porta de saída** o esquema de saída de serviço do toorepresent Olá web esperado.</span><span class="sxs-lookup"><span data-stu-id="d0511-432">Identify a logical **output port** toorepresent hello expected web service output schema.</span></span>

<span data-ttu-id="d0511-433">Quando Olá experimento de pontuação é criado, examiná-la e fazer ajuste conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="d0511-433">When hello scoring experiment is created, review it and make adjust as needed.</span></span> <span data-ttu-id="d0511-434">Um ajuste típico é tooreplace Olá dataset de entrada e/ou consulta com uma que exclui os campos de rótulo, como eles não estarão disponíveis quando Olá serviço é chamado.</span><span class="sxs-lookup"><span data-stu-id="d0511-434">A typical adjustment is tooreplace hello input dataset and/or query with one which excludes label fields, as these will not be available when hello service is called.</span></span> <span data-ttu-id="d0511-435">Também é que um tamanho de saudação tooreduce uma boa prática de saudação tooa de consulta e/ou conjunto de dados de entrada suficientes esquema de entrada hello tooindicate de alguns registros.</span><span class="sxs-lookup"><span data-stu-id="d0511-435">It is also a good practice tooreduce hello size of hello input dataset and/or query tooa few records, just enough tooindicate hello input schema.</span></span> <span data-ttu-id="d0511-436">Para a porta de saída de hello, é tooexclude comuns entrados todos os campos e incluir apenas Olá **rótulos de pontuação** e **probabilidades pontuadas** em Olá saída usando Olá [selecionar colunas no conjunto de dados ] [ select-columns] módulo.</span><span class="sxs-lookup"><span data-stu-id="d0511-436">For hello output port, it is common tooexclude all input fields and only include hello **Scored Labels** and **Scored Probabilities** in hello output using hello [Select Columns in Dataset][select-columns] module.</span></span>

<span data-ttu-id="d0511-437">Um exemplo de experiência de pontuação é fornecido na Figura Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="d0511-437">A sample scoring experiment is provided in hello figure below.</span></span> <span data-ttu-id="d0511-438">Quando estiver pronto toodeploy, clique em Olá **publicar WEB SERVICE** botão na barra de ação inferior hello.</span><span class="sxs-lookup"><span data-stu-id="d0511-438">When ready toodeploy, click hello **PUBLISH WEB SERVICE** button in hello lower action bar.</span></span>

![Publicação do AM do Azure][11]

## <a name="summary"></a><span data-ttu-id="d0511-440">Resumo</span><span class="sxs-lookup"><span data-stu-id="d0511-440">Summary</span></span>
<span data-ttu-id="d0511-441">toorecap que fizemos neste tutorial passo a passo, você criou um ambiente de ciência de dados do Azure, trabalhado com um conjunto de dados grande público, colocá-lo por meio de saudação processo de ciência de dados de equipe, todo caminho de saudação do treinamento de toomodel de aquisição de dados e, em seguida, implantação de toohello de um serviço web de aprendizado de máquina do Azure.</span><span class="sxs-lookup"><span data-stu-id="d0511-441">toorecap what we have done in this walkthrough tutorial, you have created an Azure data science environment, worked with a large public dataset, taking it through hello Team Data Science Process, all hello way from data acquisition toomodel training, and then toohello deployment of an Azure Machine Learning web service.</span></span>

### <a name="license-information"></a><span data-ttu-id="d0511-442">Informações de licença</span><span class="sxs-lookup"><span data-stu-id="d0511-442">License information</span></span>
<span data-ttu-id="d0511-443">Este exemplo passo a passo e seu que acompanha scripts e IPython notebook(s) são compartilhados pela Microsoft sob a licença do MIT hello.</span><span class="sxs-lookup"><span data-stu-id="d0511-443">This sample walkthrough and its accompanying scripts and IPython notebook(s) are shared by Microsoft under hello MIT license.</span></span> <span data-ttu-id="d0511-444">Verifique o arquivo de LICENSE.txt de saudação no diretório de saudação do código de exemplo hello no GitHub para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="d0511-444">Please check hello LICENSE.txt file in in hello directory of hello sample code on GitHub for more details.</span></span>

## <a name="references"></a><span data-ttu-id="d0511-445">Referências</span><span class="sxs-lookup"><span data-stu-id="d0511-445">References</span></span>
<span data-ttu-id="d0511-446">•   [Página de download de Viagens de Táxi de NYC, de Andrés Monroy](http://www.andresmh.com/nyctaxitrips/)</span><span class="sxs-lookup"><span data-stu-id="d0511-446">•    [Andrés Monroy NYC Taxi Trips Download Page](http://www.andresmh.com/nyctaxitrips/)</span></span>  
<span data-ttu-id="d0511-447">•   [Dados de Viagem de Táxi de FOILing NYC, de Chris Whong](http://chriswhong.com/open-data/foil_nyc_taxi/) </span><span class="sxs-lookup"><span data-stu-id="d0511-447">•    [FOILing NYC’s Taxi Trip Data by Chris Whong](http://chriswhong.com/open-data/foil_nyc_taxi/) </span></span>  
<span data-ttu-id="d0511-448">•   [Pesquisa e estatísticas de comissionamento de táxis e limusines de NYC](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span><span class="sxs-lookup"><span data-stu-id="d0511-448">•    [NYC Taxi and Limousine Commission Research and Statistics](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span></span>

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
