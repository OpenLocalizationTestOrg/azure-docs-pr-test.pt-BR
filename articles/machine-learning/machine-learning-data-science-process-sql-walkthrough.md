---
title: "aaaBuild e implantar um modelo de aprendizado de máquina usando o SQL Server em uma VM do Azure | Microsoft Docs"
description: "Processo e Tecnologia de Análise Avançada em ação"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 6066b083-262c-4453-a712-a5c05acc3df8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: fashah;bradsev
ms.openlocfilehash: 30ba9a9e3cf65f75015e13f9c7876dcbccc5bc47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="hello-team-data-science-process-in-action-using-sql-server"></a><span data-ttu-id="f178a-103">Olá processo de ciência de dados de equipe em ação: usando o SQL Server</span><span class="sxs-lookup"><span data-stu-id="f178a-103">hello Team Data Science Process in action: using SQL Server</span></span>
<span data-ttu-id="f178a-104">Neste tutorial, você pode percorrer Olá processo de criação e implantação de um modelo de aprendizado de máquina usando o SQL Server e um conjunto de dados disponível publicamente – hello [NYC táxi viagens](http://www.andresmh.com/nyctaxitrips/) conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="f178a-104">In this tutorial, you walk through hello process of building and deploying a machine learning model using SQL Server and a publicly available dataset -- hello [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) dataset.</span></span> <span data-ttu-id="f178a-105">procedimento de saudação segue um fluxo de trabalho de ciência de dados padrão: ingestão e explorar dados Olá, engenheiro de aprendizado de toofacilitate de recursos, em seguida, compilar e implantar um modelo.</span><span class="sxs-lookup"><span data-stu-id="f178a-105">hello procedure follows a standard data science workflow: ingest and explore hello data, engineer features toofacilitate learning, then build and deploy a model.</span></span>

## <span data-ttu-id="f178a-106"><a name="dataset"></a>Descrição do conjunto de dados Corridas de Táxi em NYC</span><span class="sxs-lookup"><span data-stu-id="f178a-106"><a name="dataset"></a>NYC Taxi Trips Dataset Description</span></span>
<span data-ttu-id="f178a-107">Olá dados NYC táxi viagem é cerca de 20GB de arquivos compactados de CSV (~ 48GB descompactado), que inclui mais de milhões de 173 hello e viagens individuais é pago para cada viagem.</span><span class="sxs-lookup"><span data-stu-id="f178a-107">hello NYC Taxi Trip data is about 20GB of compressed CSV files (~48GB uncompressed), comprising more than 173 million individual trips and hello fares paid for each trip.</span></span> <span data-ttu-id="f178a-108">Cada registro de viagem inclui Olá retirada e entrega local e a hora, hack anônimos (driver) o número de licença e número medallion (id exclusiva do táxi).</span><span class="sxs-lookup"><span data-stu-id="f178a-108">Each trip record includes hello pickup and drop-off location and time, anonymized hack (driver's) license number and medallion (taxi’s unique id) number.</span></span> <span data-ttu-id="f178a-109">dados saudação abrange todas as viagens no ano Olá 2013 e são fornecidos em dois conjuntos de dados a seguir para cada mês de saudação:</span><span class="sxs-lookup"><span data-stu-id="f178a-109">hello data covers all trips in hello year 2013 and is provided in hello following two datasets for each month:</span></span>

1. <span data-ttu-id="f178a-110">Olá 'trip_data' CSV contém detalhes da visita, como o número de passageiros, coleta e pontos de redução, duração da viagem e comprimento de viagem.</span><span class="sxs-lookup"><span data-stu-id="f178a-110">hello 'trip_data' CSV contains trip details, such as number of passengers, pickup and dropoff points, trip duration, and trip length.</span></span> <span data-ttu-id="f178a-111">Aqui estão alguns exemplos de registros:</span><span class="sxs-lookup"><span data-stu-id="f178a-111">Here are a few sample records:</span></span>
   
        medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count,trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
2. <span data-ttu-id="f178a-112">Olá 'trip_fare' CSV contém detalhes de passagens Olá pagado para cada viagem, como tipo de pagamento, quantidade de passagens, sobretaxa e impostos, dicas e pedágio e quantidade total de saudação paga.</span><span class="sxs-lookup"><span data-stu-id="f178a-112">hello 'trip_fare' CSV contains details of hello fare paid for each trip, such as payment type, fare amount, surcharge and taxes, tips and tolls, and hello total amount paid.</span></span> <span data-ttu-id="f178a-113">Aqui estão alguns exemplos de registros:</span><span class="sxs-lookup"><span data-stu-id="f178a-113">Here are a few sample records:</span></span>
   
        medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

<span data-ttu-id="f178a-114">viagem de toojoin de chave exclusivo Olá\_dados e viagem\_passagens é composta de campos de saudação: medallion, ataques\_licença e retirada\_datetime.</span><span class="sxs-lookup"><span data-stu-id="f178a-114">hello unique key toojoin trip\_data and trip\_fare is composed of hello fields: medallion, hack\_licence and pickup\_datetime.</span></span>

## <span data-ttu-id="f178a-115"><a name="mltasks"></a>Exemplos de tarefas de previsão</span><span class="sxs-lookup"><span data-stu-id="f178a-115"><a name="mltasks"></a>Examples of Prediction Tasks</span></span>
<span data-ttu-id="f178a-116">Podemos será formular três problemas de previsão com base em Olá *dica\_quantidade*, ou seja:</span><span class="sxs-lookup"><span data-stu-id="f178a-116">We will formulate three prediction problems based on hello *tip\_amount*, namely:</span></span>

1. <span data-ttu-id="f178a-117">Classificação binária: prever ou não se uma gorjeta foi paga por uma corrida, ou seja, um *tip\_amount* maior que US$ 0 é um exemplo positivo, enquanto um *tip\_amount* de US$ 0 é um exemplo negativo.</span><span class="sxs-lookup"><span data-stu-id="f178a-117">Binary classification: Predict whether or not a tip was paid for a trip, i.e. a *tip\_amount* that is greater than $0 is a positive example, while a *tip\_amount* of $0 is a negative example.</span></span>
2. <span data-ttu-id="f178a-118">Classificação multiclasse: intervalo de saudação toopredict de dica de pago para viagem hello.</span><span class="sxs-lookup"><span data-stu-id="f178a-118">Multiclass classification: toopredict hello range of tip paid for hello trip.</span></span> <span data-ttu-id="f178a-119">Olá, nós dividimos *dica\_quantidade* em cinco compartimentos ou classes:</span><span class="sxs-lookup"><span data-stu-id="f178a-119">We divide hello *tip\_amount* into five bins or classes:</span></span>
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0 and tip_amount <= $5
        Class 2 : tip_amount > $5 and tip_amount <= $10
        Class 3 : tip_amount > $10 and tip_amount <= $20
        Class 4 : tip_amount > $20
3. <span data-ttu-id="f178a-120">Tarefa de regressão: o valor de saudação toopredict de dica pago para uma viagem.</span><span class="sxs-lookup"><span data-stu-id="f178a-120">Regression task: toopredict hello amount of tip paid for a trip.</span></span>  

## <span data-ttu-id="f178a-121"><a name="setup"></a>Configurando ambiente de ciência de saudação dados do Azure para análise avançada</span><span class="sxs-lookup"><span data-stu-id="f178a-121"><a name="setup"></a>Setting Up hello Azure data science environment for advanced analytics</span></span>
<span data-ttu-id="f178a-122">Como você pode ver da saudação [planejar seu ambiente](machine-learning-data-science-plan-your-environment.md) guia, há vários toowork opções com hello NYC táxi viagens conjunto de dados no Azure:</span><span class="sxs-lookup"><span data-stu-id="f178a-122">As you can see from hello [Plan Your Environment](machine-learning-data-science-plan-your-environment.md) guide, there are several options toowork with hello NYC Taxi Trips dataset in Azure:</span></span>

* <span data-ttu-id="f178a-123">Trabalhar com dados de saudação em blobs do Azure e o modelo no aprendizado de máquina do Azure</span><span class="sxs-lookup"><span data-stu-id="f178a-123">Work with hello data in Azure blobs then model in Azure Machine Learning</span></span>
* <span data-ttu-id="f178a-124">Saudação de carregar dados em um banco de dados do SQL Server e o modelo no aprendizado de máquina do Azure</span><span class="sxs-lookup"><span data-stu-id="f178a-124">Load hello data into a SQL Server database then model in Azure Machine Learning</span></span>

<span data-ttu-id="f178a-125">Neste tutorial, tentaremos demonstrar a importação em massa paralela de saudação tooa de dados do SQL Server, exploração de dados, o recurso de engenharia e para baixo de amostragem usando o SQL Server Management Studio, bem como usar o bloco de anotações do IPython.</span><span class="sxs-lookup"><span data-stu-id="f178a-125">In this tutorial we will demonstrate parallel bulk import of hello data tooa SQL Server, data exploration, feature engineering and down sampling using SQL Server Management Studio as well as using IPython Notebook.</span></span> <span data-ttu-id="f178a-126">[Scripts de exemplo](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts) e [notebooks IPython](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks) são compartilhados no GitHub.</span><span class="sxs-lookup"><span data-stu-id="f178a-126">[Sample scripts](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts) and [IPython notebooks](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks) are shared in GitHub.</span></span> <span data-ttu-id="f178a-127">Um toowork de bloco de anotações do IPython exemplo com dados de saudação em blobs do Azure também está disponível no hello mesmo local.</span><span class="sxs-lookup"><span data-stu-id="f178a-127">A sample IPython notebook toowork with hello data in Azure blobs is also available in hello same location.</span></span>

<span data-ttu-id="f178a-128">tooset seu ambiente de ciência de dados do Azure:</span><span class="sxs-lookup"><span data-stu-id="f178a-128">tooset up your Azure Data Science environment:</span></span>

1. [<span data-ttu-id="f178a-129">Criar uma conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="f178a-129">Create a storage account</span></span>](../storage/common/storage-create-storage-account.md)
2. <span data-ttu-id="f178a-130">
            [Criar um espaço de trabalho de Azure Machine Learning](machine-learning-create-workspace.md)</span><span class="sxs-lookup"><span data-stu-id="f178a-130">[Create an Azure Machine Learning workspace](machine-learning-create-workspace.md)</span></span>
3. <span data-ttu-id="f178a-131">[Provisione uma Máquina Virtual de Ciência de Dados](machine-learning-data-science-setup-sql-server-virtual-machine.md), que fornece um SQL Server e um servidor do IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="f178a-131">[Provision a Data Science Virtual Machine](machine-learning-data-science-setup-sql-server-virtual-machine.md), which provides a SQL Server and an IPython Notebook server.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="f178a-132">scripts de exemplo Hello e anotações do IPython será baixado tooyour máquina de virtual de ciência de dados durante o processo de instalação hello.</span><span class="sxs-lookup"><span data-stu-id="f178a-132">hello sample scripts and IPython notebooks will be downloaded tooyour Data Science virtual machine during hello setup process.</span></span> <span data-ttu-id="f178a-133">Quando for concluído Olá script de pós-instalação de VM, exemplos de saudação será na biblioteca de documentos da VM:</span><span class="sxs-lookup"><span data-stu-id="f178a-133">When hello VM post-installation script completes, hello samples will be in your VM's Documents library:</span></span>  
   > 
   > * <span data-ttu-id="f178a-134">Scripts de exemplo: `C:\Users\<user_name>\Documents\Data Science Scripts`</span><span class="sxs-lookup"><span data-stu-id="f178a-134">Sample Scripts: `C:\Users\<user_name>\Documents\Data Science Scripts`</span></span>  
   > * <span data-ttu-id="f178a-135">Exemplo de IPython Notebooks: `C:\Users\<user_name>\Documents\IPython Notebooks\DataScienceSamples`</span><span class="sxs-lookup"><span data-stu-id="f178a-135">Sample IPython Notebooks: `C:\Users\<user_name>\Documents\IPython Notebooks\DataScienceSamples`</span></span>  
   >   <span data-ttu-id="f178a-136">where `<user_name>` é o nome de logon do Windows da VM.</span><span class="sxs-lookup"><span data-stu-id="f178a-136">where `<user_name>` is your VM's Windows login name.</span></span> <span data-ttu-id="f178a-137">Chamaremos toohello pastas de exemplo como **Scripts de exemplo** e **exemplo de anotações do IPython**.</span><span class="sxs-lookup"><span data-stu-id="f178a-137">We will refer toohello sample folders as **Sample Scripts** and **Sample IPython Notebooks**.</span></span>
   > 
   > 

<span data-ttu-id="f178a-138">Com base no tamanho do conjunto de dados Olá, local de fonte de dados e ambiente de destino do Azure selecionada Olá, este cenário é semelhante muito[cenário \#5: SQL Server em VM do Azure de destino do conjunto de dados grande em arquivos de locais,](machine-learning-data-science-plan-sample-scenarios.md#largelocaltodb).</span><span class="sxs-lookup"><span data-stu-id="f178a-138">Based on hello dataset size, data source location, and hello selected Azure target environment, this scenario is similar too[Scenario \#5: Large dataset in a local files, target SQL Server in Azure VM](machine-learning-data-science-plan-sample-scenarios.md#largelocaltodb).</span></span>

## <span data-ttu-id="f178a-139"><a name="getdata"></a>Obter Olá dados de origem pública</span><span class="sxs-lookup"><span data-stu-id="f178a-139"><a name="getdata"></a>Get hello Data from Public Source</span></span>
<span data-ttu-id="f178a-140">Olá tooget [NYC táxi viagens](http://www.andresmh.com/nyctaxitrips/) conjunto de dados de seu local público, você pode usar qualquer um dos métodos de saudação descritos em [tooand de mover dados do armazenamento de BLOBs do Azure](machine-learning-data-science-move-azure-blob.md) toocopy Olá dados tooyour nova máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="f178a-140">tooget hello [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) dataset from its public location, you may use any of hello methods described in [Move Data tooand from Azure Blob Storage](machine-learning-data-science-move-azure-blob.md) toocopy hello data tooyour new virtual machine.</span></span>

<span data-ttu-id="f178a-141">dados de saudação toocopy usando AzCopy:</span><span class="sxs-lookup"><span data-stu-id="f178a-141">toocopy hello data using AzCopy:</span></span>

1. <span data-ttu-id="f178a-142">Faça logon na máquina virtual de tooyour (VM)</span><span class="sxs-lookup"><span data-stu-id="f178a-142">Log in tooyour virtual machine (VM)</span></span>
2. <span data-ttu-id="f178a-143">Criar um novo diretório em disco de dados da VM hello (Observação: não use Olá disco temporário que vem com hello VM como um disco de dados).</span><span class="sxs-lookup"><span data-stu-id="f178a-143">Create a new directory in hello VM's data disk (Note: Do not use hello Temporary Disk which comes with hello VM as a Data Disk).</span></span>
3. <span data-ttu-id="f178a-144">Em uma janela de Prompt de comando, execute Olá Azcopy linha de comando a seguir, substituindo < path_to_data_folder > com a pasta de dados criada na (2):</span><span class="sxs-lookup"><span data-stu-id="f178a-144">In a Command Prompt window, run hello following Azcopy command line, replacing <path_to_data_folder> with your data folder created in (2):</span></span>
   
        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:https://nyctaxitrips.blob.core.windows.net/data /Dest:<path_to_data_folder> /S
   
    <span data-ttu-id="f178a-145">Quando Olá AzCopy é concluída, um total de 24 compactado arquivos CSV (12 para viagem\_dados e 12 para viagem\_passagens) devem estar na pasta de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="f178a-145">When hello AzCopy completes, a total of 24 zipped CSV files (12 for trip\_data and 12 for trip\_fare) should be in hello data folder.</span></span>
4. <span data-ttu-id="f178a-146">Descompacte arquivos de saudação baixado.</span><span class="sxs-lookup"><span data-stu-id="f178a-146">Unzip hello downloaded files.</span></span> <span data-ttu-id="f178a-147">Anote a pasta de saudação onde residem os arquivos de saudação descompactado.</span><span class="sxs-lookup"><span data-stu-id="f178a-147">Note hello folder where hello uncompressed files reside.</span></span> <span data-ttu-id="f178a-148">Esta pasta será chamado tooas hello < caminho\_para\_dados\_arquivos\>.</span><span class="sxs-lookup"><span data-stu-id="f178a-148">This folder will be referred tooas hello <path\_to\_data\_files\>.</span></span>

## <span data-ttu-id="f178a-149"><a name="dbload"></a>Importação de dados em massa para o Banco de Dados do SQL Server</span><span class="sxs-lookup"><span data-stu-id="f178a-149"><a name="dbload"></a>Bulk Import Data into SQL Server Database</span></span>
<span data-ttu-id="f178a-150">saudação de carregamento/transferir grandes quantidades de banco de dados do SQL data tooan e as consultas subsequentes possível melhorar o desempenho usando *tabelas particionadas e exibições*.</span><span class="sxs-lookup"><span data-stu-id="f178a-150">hello performance of loading/transferring large amounts of data tooan SQL database and subsequent queries can be improved by using *Partitioned Tables and Views*.</span></span> <span data-ttu-id="f178a-151">Nesta seção, vamos seguir as instruções de saudação descritas em [paralelo em massa dados de importação usando partição tabelas SQL](machine-learning-data-science-parallel-load-sql-partitioned-tables.md) toocreate um novo banco de dados e carregar Olá dados em tabelas particionadas em paralelo.</span><span class="sxs-lookup"><span data-stu-id="f178a-151">In this section, we will follow hello instructions described in [Parallel Bulk Data Import Using SQL Partition Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md) toocreate a new database and load hello data into partitioned tables in parallel.</span></span>

1. <span data-ttu-id="f178a-152">Enquanto estiver conectado tooyour VM, iniciar **SQL Server Management Studio**.</span><span class="sxs-lookup"><span data-stu-id="f178a-152">While logged in tooyour VM, start **SQL Server Management Studio**.</span></span>
2. <span data-ttu-id="f178a-153">Conecte-se usando a Autenticação do Windows.</span><span class="sxs-lookup"><span data-stu-id="f178a-153">Connect using Windows Authentication.</span></span>
   
    ![Conexão SSMS][12]
3. <span data-ttu-id="f178a-155">Se você ainda não tiver alterado o modo de autenticação do SQL Server hello e criado um novo usuário de logon do SQL, abra o arquivo de script de Olá chamado **alterar\_auth.sql** em Olá **Scripts de exemplo** pasta.</span><span class="sxs-lookup"><span data-stu-id="f178a-155">If you have not yet changed hello SQL Server authentication mode and created a new SQL login user, open hello script file named **change\_auth.sql** in hello **Sample Scripts** folder.</span></span> <span data-ttu-id="f178a-156">Alterar nome de usuário saudação padrão e a senha.</span><span class="sxs-lookup"><span data-stu-id="f178a-156">Change hello  default user name and password.</span></span> <span data-ttu-id="f178a-157">Clique em **! Execute** no script de Olá Olá barra de ferramentas toorun.</span><span class="sxs-lookup"><span data-stu-id="f178a-157">Click **!Execute** in hello toolbar toorun hello script.</span></span>
   
    ![Executar Script][13]
4. <span data-ttu-id="f178a-159">Verificar e/ou alterar o saudação padrão banco de dados e log pastas tooensure que bancos de dados recém-criados será armazenado em um disco de dados do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="f178a-159">Verify and/or change hello SQL Server default database and log folders tooensure that newly created databases will be stored in a Data Disk.</span></span> <span data-ttu-id="f178a-160">imagem de VM do SQL Server de saudação que é otimizada para cargas de datawarehousing é pré-configurado com discos de dados e de log.</span><span class="sxs-lookup"><span data-stu-id="f178a-160">hello SQL Server VM image that is optimized for datawarehousing loads is pre-configured with data and log disks.</span></span> <span data-ttu-id="f178a-161">Se sua VM não incluiu um disco de dados e você adicionou novos discos rígidos virtuais durante a saudação processo de configuração VM, altere pastas padrão de saudação da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="f178a-161">If your VM did not include a Data Disk and you added new virtual hard disks during hello VM setup process, change hello default folders as follows:</span></span>
   
   * <span data-ttu-id="f178a-162">Nome de SQL Server Olá com o botão direito no hello esquerda do painel e clique em **propriedades**.</span><span class="sxs-lookup"><span data-stu-id="f178a-162">Right-click hello SQL Server name in hello left panel and click **Properties**.</span></span>
     
       ![Propriedades do SQL Server][14]
   * <span data-ttu-id="f178a-164">Selecione **configurações de banco de dados** de saudação **selecionar uma página** lista toohello esquerda.</span><span class="sxs-lookup"><span data-stu-id="f178a-164">Select **Database Settings** from hello **Select a page** list toohello left.</span></span>
   * <span data-ttu-id="f178a-165">Verificar e/ou alterar Olá **locais padrão do banco de dados** toohello **disco de dados** locais de sua escolha.</span><span class="sxs-lookup"><span data-stu-id="f178a-165">Verify and/or change hello **Database default locations** toohello **Data Disk** locations of your choice.</span></span> <span data-ttu-id="f178a-166">É onde os novos bancos de dados residem se criado com as configurações de local de padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="f178a-166">This is where new databases reside if created with hello default location settings.</span></span>
     
       ![Padrões de banco de dados SQL][15]  
5. <span data-ttu-id="f178a-168">toocreate um novo banco de dados e um conjunto de grupos de arquivos toohold Olá tabelas particionadas, abra o script de exemplo hello **criar\_db\_default.sql**.</span><span class="sxs-lookup"><span data-stu-id="f178a-168">toocreate a new database and a set of filegroups toohold hello partitioned tables, open hello sample script **create\_db\_default.sql**.</span></span> <span data-ttu-id="f178a-169">script Hello criará um novo banco de dados denominado **TaxiNYC** e 12 grupos de arquivos no local de dados padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="f178a-169">hello script will create a new database named **TaxiNYC** and 12 filegroups in hello default data location.</span></span> <span data-ttu-id="f178a-170">Cada grupo de arquivos conterá um mês de dados trip\_data e trip\_fare.</span><span class="sxs-lookup"><span data-stu-id="f178a-170">Each filegroup will hold one month of trip\_data and trip\_fare data.</span></span> <span data-ttu-id="f178a-171">Modificar o nome do banco de dados de hello, se desejado.</span><span class="sxs-lookup"><span data-stu-id="f178a-171">Modify hello database name, if desired.</span></span> <span data-ttu-id="f178a-172">Clique em **! Executar** toorun script de saudação.</span><span class="sxs-lookup"><span data-stu-id="f178a-172">Click **!Execute** toorun hello script.</span></span>
6. <span data-ttu-id="f178a-173">Em seguida, crie duas tabelas de partição, uma para viagem Olá\_dados e outro para viagem Olá\_passagens.</span><span class="sxs-lookup"><span data-stu-id="f178a-173">Next, create two partition tables, one for hello trip\_data and another for hello trip\_fare.</span></span> <span data-ttu-id="f178a-174">Abra o script de exemplo hello **criar\_particionada\_table.sql**, que será:</span><span class="sxs-lookup"><span data-stu-id="f178a-174">Open hello sample script **create\_partitioned\_table.sql**, which will:</span></span>
   
   * <span data-ttu-id="f178a-175">Crie uma partição de saudação de toosplit de função de dados por mês.</span><span class="sxs-lookup"><span data-stu-id="f178a-175">Create a partition function toosplit hello data by month.</span></span>
   * <span data-ttu-id="f178a-176">Crie um toomap de esquema de partição de dados tooa grupo de arquivos diferente cada mês.</span><span class="sxs-lookup"><span data-stu-id="f178a-176">Create a partition scheme toomap each month's data tooa different filegroup.</span></span>
   * <span data-ttu-id="f178a-177">Criar esquema de partição do duas tabelas particionadas toohello mapeado: **nyctaxi\_viagem** armazenará trip Olá\_dados e **nyctaxi\_passagens** armazenará trip Olá \_passagens de dados.</span><span class="sxs-lookup"><span data-stu-id="f178a-177">Create two partitioned tables mapped toohello partition scheme: **nyctaxi\_trip** will hold hello trip\_data and **nyctaxi\_fare** will hold hello trip\_fare data.</span></span>
     
     <span data-ttu-id="f178a-178">Clique em **! Executar** toorun Olá script e criar tabelas particionada de saudação.</span><span class="sxs-lookup"><span data-stu-id="f178a-178">Click **!Execute** toorun hello script and create hello partitioned tables.</span></span>
7. <span data-ttu-id="f178a-179">Em Olá **Scripts de exemplo** pasta, há dois scripts de PowerShell de exemplo fornecidos toodemonstrate importações em massa paralela tooSQL servidor de tabelas de dados.</span><span class="sxs-lookup"><span data-stu-id="f178a-179">In hello **Sample Scripts** folder, there are two sample PowerShell scripts provided toodemonstrate parallel bulk imports of data tooSQL Server tables.</span></span>
   
   * <span data-ttu-id="f178a-180">**BCP\_paralela\_generic.ps1** é um script genérico tooparallel importar em massa dados em uma tabela.</span><span class="sxs-lookup"><span data-stu-id="f178a-180">**bcp\_parallel\_generic.ps1** is a generic script tooparallel bulk import data into a table.</span></span> <span data-ttu-id="f178a-181">Modifique este variáveis de entrada e de destino de saudação do tooset script conforme indicado nas linhas de comentário hello no script hello.</span><span class="sxs-lookup"><span data-stu-id="f178a-181">Modify this script tooset hello input and target variables as indicated in hello comment lines in hello script.</span></span>
   * <span data-ttu-id="f178a-182">**BCP\_paralela\_nyctaxi.ps1** é uma versão previamente configurada do script genérico hello e pode ser usado tootooload ambas as tabelas para dados de NYC táxi viagens hello.</span><span class="sxs-lookup"><span data-stu-id="f178a-182">**bcp\_parallel\_nyctaxi.ps1** is a pre-configured version of hello generic script and can be used tootooload both tables for hello NYC Taxi Trips data.</span></span>  
8. <span data-ttu-id="f178a-183">Saudação de atalho **bcp\_paralela\_nyctaxi.ps1** nome do script e clique em **editar** tooopen no PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f178a-183">Right-click hello **bcp\_parallel\_nyctaxi.ps1** script name and click **Edit** tooopen it in PowerShell.</span></span> <span data-ttu-id="f178a-184">Saudação de revisão predefinição variáveis e modificar o nome de banco de dados selecionado do acordo tooyour, pasta de dados de entrada, pasta de log de destino e arquivos de formato de exemplo caminhos toohello **nyctaxi_trip.xml** e **nyctaxi\_ fare.XML** (fornecido no hello **Scripts de exemplo** pasta).</span><span class="sxs-lookup"><span data-stu-id="f178a-184">Review hello preset variables and modify according tooyour selected database name, input data folder, target log folder, and paths toohello  sample format files **nyctaxi_trip.xml** and **nyctaxi\_fare.xml** (provided in hello **Sample Scripts** folder).</span></span>
   
    ![Importação em massa de dados][16]
   
    <span data-ttu-id="f178a-186">Você também pode selecionar o modo de autenticação hello, o padrão é a autenticação do Windows.</span><span class="sxs-lookup"><span data-stu-id="f178a-186">You may also select hello authentication mode, default is Windows Authentication.</span></span> <span data-ttu-id="f178a-187">Clique a seta verde de saudação Olá toorun de barra de ferramentas.</span><span class="sxs-lookup"><span data-stu-id="f178a-187">Click hello green arrow in hello toolbar toorun.</span></span> <span data-ttu-id="f178a-188">script Hello iniciará 24 operações de importação em massa em paralelo, 12 para cada tabela particionada.</span><span class="sxs-lookup"><span data-stu-id="f178a-188">hello script will launch 24 bulk import operations in parallel, 12 for each partitioned table.</span></span> <span data-ttu-id="f178a-189">É possível monitorar o progresso de importação de dados Olá abrindo a pasta de dados de padrão saudação do SQL Server conforme definido acima.</span><span class="sxs-lookup"><span data-stu-id="f178a-189">You may monitor hello data import progress by opening hello SQL Server default data folder as set above.</span></span>
9. <span data-ttu-id="f178a-190">relatórios de script do PowerShell Olá Olá horas inicial e final.</span><span class="sxs-lookup"><span data-stu-id="f178a-190">hello PowerShell script reports hello starting and ending times.</span></span> <span data-ttu-id="f178a-191">Quando todos em massa importações completa, Olá hora de término é relatado.</span><span class="sxs-lookup"><span data-stu-id="f178a-191">When all bulk imports complete, hello ending time is reported.</span></span> <span data-ttu-id="f178a-192">Verifique o hello destino log pasta tooverify que importações em massa de saudação foram bem-sucedidas, ou seja, nenhum erro relatado na pasta de log de destino hello.</span><span class="sxs-lookup"><span data-stu-id="f178a-192">Check hello target log folder tooverify that hello bulk imports were successful, i.e., no errors reported in hello target log folder.</span></span>
10. <span data-ttu-id="f178a-193">O banco de dados agora está pronto para exploração, engenharia de recursos e outras operações conforme desejado.</span><span class="sxs-lookup"><span data-stu-id="f178a-193">Your database is now ready for exploration, feature engineering, and other operations as desired.</span></span> <span data-ttu-id="f178a-194">Como tabelas de saudação são particionadas de acordo com o toohello **retirada\_datetime** campo, consultas que incluem **retirada\_datetime** condições em Olá  **ONDE** cláusula se beneficiarão do esquema de partição hello.</span><span class="sxs-lookup"><span data-stu-id="f178a-194">Since hello tables are partitioned according toohello **pickup\_datetime** field, queries which include **pickup\_datetime** conditions in hello **WHERE** clause will benefit from hello partition scheme.</span></span>
11. <span data-ttu-id="f178a-195">Em **SQL Server Management Studio**, explore o script de exemplo hello fornecido **exemplo\_queries.sql**.</span><span class="sxs-lookup"><span data-stu-id="f178a-195">In **SQL Server Management Studio**, explore hello provided sample script **sample\_queries.sql**.</span></span> <span data-ttu-id="f178a-196">toorun qualquer uma das consultas de exemplo hello, realce Olá linhas de consulta e clique em **! Executar** na barra de ferramentas de saudação.</span><span class="sxs-lookup"><span data-stu-id="f178a-196">toorun any of hello sample queries, highlight hello query lines then click **!Execute** in hello toolbar.</span></span>
12. <span data-ttu-id="f178a-197">Olá dados NYC táxi viagens é carregado em duas tabelas separadas.</span><span class="sxs-lookup"><span data-stu-id="f178a-197">hello NYC Taxi Trips data is loaded in two separate tables.</span></span> <span data-ttu-id="f178a-198">operações de junção tooimprove, é altamente recomendável tooindex tabelas de saudação.</span><span class="sxs-lookup"><span data-stu-id="f178a-198">tooimprove join operations, it is highly recommended tooindex hello tables.</span></span> <span data-ttu-id="f178a-199">Olá script de exemplo **criar\_particionada\_index.sql** cria índices particionados na chave de junção composto Olá **medallion, ataques\_licença e retirada\_datetime**.</span><span class="sxs-lookup"><span data-stu-id="f178a-199">hello sample script **create\_partitioned\_index.sql** creates partitioned indexes on hello composite join key **medallion, hack\_license, and pickup\_datetime**.</span></span>

## <span data-ttu-id="f178a-200"><a name="dbexplore"></a>Exploração de dados e engenharia de recursos no SQL Server</span><span class="sxs-lookup"><span data-stu-id="f178a-200"><a name="dbexplore"></a>Data Exploration and Feature Engineering in SQL Server</span></span>
<span data-ttu-id="f178a-201">Nesta seção, vamos realizar exploração e recurso de geração de dados, executando consultas SQL diretamente em Olá **SQL Server Management Studio** usar o banco de dados do SQL Server Olá criado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="f178a-201">In this section, we will perform data exploration and feature generation by running SQL queries directly in hello **SQL Server Management Studio** using hello SQL Server database created earlier.</span></span> <span data-ttu-id="f178a-202">Um script de exemplo chamado **exemplo\_queries.sql** é fornecido no hello **Scripts de exemplo** pasta.</span><span class="sxs-lookup"><span data-stu-id="f178a-202">A sample script named **sample\_queries.sql** is provided in hello **Sample Scripts** folder.</span></span> <span data-ttu-id="f178a-203">Modificar o nome de banco de dados do Olá Olá script toochange, se ele for diferente do padrão de saudação: **TaxiNYC**.</span><span class="sxs-lookup"><span data-stu-id="f178a-203">Modify hello script toochange hello database name, if it is different from hello default: **TaxiNYC**.</span></span>

<span data-ttu-id="f178a-204">Neste exercício, você vai:</span><span class="sxs-lookup"><span data-stu-id="f178a-204">In this exercise, we will:</span></span>

* <span data-ttu-id="f178a-205">Conecte-se muito**SQL Server Management Studio** usando a autenticação do Windows ou autenticação do SQL e hello nome de logon do SQL e a senha.</span><span class="sxs-lookup"><span data-stu-id="f178a-205">Connect too**SQL Server Management Studio** using either Windows Authentication or using SQL Authentication and hello SQL login name and password.</span></span>
* <span data-ttu-id="f178a-206">Explorar as distribuições de dados de alguns campos em períodos diferentes.</span><span class="sxs-lookup"><span data-stu-id="f178a-206">Explore data distributions of a few fields in varying time windows.</span></span>
* <span data-ttu-id="f178a-207">Investigue a qualidade dos dados dos campos de longitude e latitude hello.</span><span class="sxs-lookup"><span data-stu-id="f178a-207">Investigate data quality of hello longitude and latitude fields.</span></span>
* <span data-ttu-id="f178a-208">Gerar rótulos de classificação binária e multiclasse com base no hello **dica\_quantidade**.</span><span class="sxs-lookup"><span data-stu-id="f178a-208">Generate binary and multiclass classification labels based on hello **tip\_amount**.</span></span>
* <span data-ttu-id="f178a-209">Gerar recursos e computar/comparar as distâncias de viagem.</span><span class="sxs-lookup"><span data-stu-id="f178a-209">Generate features and compute/compare trip distances.</span></span>
* <span data-ttu-id="f178a-210">Unir Olá duas tabelas e extrair uma amostra aleatória que será usado toobuild modelos.</span><span class="sxs-lookup"><span data-stu-id="f178a-210">Join hello two tables and extract a random sample that will be used toobuild models.</span></span>

<span data-ttu-id="f178a-211">Quando você estiver pronto tooproceed tooAzure aprendizado de máquina, você pode:</span><span class="sxs-lookup"><span data-stu-id="f178a-211">When you are ready tooproceed tooAzure Machine Learning, you may either:</span></span>  

1. <span data-ttu-id="f178a-212">Salvar Olá final SQL consulta tooextract e exemplo hello dados e copiar e colar Olá consulta diretamente em um [importar dados] [ import-data] módulo no aprendizado de máquina do Azure, ou</span><span class="sxs-lookup"><span data-stu-id="f178a-212">Save hello final SQL query tooextract and sample hello data and copy-paste hello query directly into a [Import Data][import-data] module in Azure Machine Learning, or</span></span>
2. <span data-ttu-id="f178a-213">Persistir Olá amostrada e planejar toouse para criar um novo banco de dados de modelo de dados de engenharia de tabela e usam a nova tabela de saudação em Olá [importar dados] [ import-data] módulo no aprendizado de máquina do Azure.</span><span class="sxs-lookup"><span data-stu-id="f178a-213">Persist hello sampled and engineered data you plan toouse for model building in a new database table and use hello new table in hello [Import Data][import-data] module in Azure Machine Learning.</span></span>

<span data-ttu-id="f178a-214">Esta seção é salvará Olá consulta final tooextract e Olá dados de exemplo.</span><span class="sxs-lookup"><span data-stu-id="f178a-214">In this section we will save hello final query tooextract and sample hello data.</span></span> <span data-ttu-id="f178a-215">método segundo Hello é demonstrado no hello [exploração de dados e de engenharia de recurso no bloco de anotações do IPython](#ipnb) seção.</span><span class="sxs-lookup"><span data-stu-id="f178a-215">hello second method is demonstrated in hello [Data Exploration and Feature Engineering in IPython Notebook](#ipnb) section.</span></span>

<span data-ttu-id="f178a-216">Para uma verificação rápida do número de saudação de linhas e colunas de saudação tabelas populadas anteriormente usando a importação em massa em paralelo,</span><span class="sxs-lookup"><span data-stu-id="f178a-216">For a quick verification of hello number of rows and columns in hello tables populated earlier using parallel bulk import,</span></span>

    -- Report number of rows in table nyctaxi_trip without table scan
    SELECT SUM(rows) FROM sys.partitions WHERE object_id = OBJECT_ID('nyctaxi_trip')

    -- Report number of columns in table nyctaxi_trip
    SELECT COUNT(*) FROM information_schema.columns WHERE table_name = 'nyctaxi_trip'

#### <a name="exploration-trip-distribution-by-medallion"></a><span data-ttu-id="f178a-217">Exploração: distribuição de corridas por licença</span><span class="sxs-lookup"><span data-stu-id="f178a-217">Exploration: Trip distribution by medallion</span></span>
<span data-ttu-id="f178a-218">Este exemplo identifica medallion hello (números de táxi) com mais de 100 viagens dentro de um determinado período de tempo.</span><span class="sxs-lookup"><span data-stu-id="f178a-218">This example identifies hello medallion (taxi numbers) with more than 100 trips within a given time period.</span></span> <span data-ttu-id="f178a-219">consulta de saudação pode se beneficiar do acesso à tabela de saudação particionada porque ele está condicionado pelo esquema de partição de saudação do **retirada\_datetime**.</span><span class="sxs-lookup"><span data-stu-id="f178a-219">hello query would benefit from hello partitioned table access since it is conditioned by hello partition scheme of **pickup\_datetime**.</span></span> <span data-ttu-id="f178a-220">Consultar o conjunto de dados completo Olá também fará com que o uso de tabela particionada hello e/ou verificação de índice.</span><span class="sxs-lookup"><span data-stu-id="f178a-220">Querying hello full dataset will also make use of hello partitioned table and/or index scan.</span></span>

    SELECT medallion, COUNT(*)
    FROM nyctaxi_fare
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    GROUP BY medallion
    HAVING COUNT(*) > 100

#### <a name="exploration-trip-distribution-by-medallion-and-hacklicense"></a><span data-ttu-id="f178a-221">Exploração: distribuição de corridas por medallion e hack_license</span><span class="sxs-lookup"><span data-stu-id="f178a-221">Exploration: Trip distribution by medallion and hack_license</span></span>
    SELECT medallion, hack_license, COUNT(*)
    FROM nyctaxi_fare
    WHERE pickup_datetime BETWEEN '20130101' AND '20130131'
    GROUP BY medallion, hack_license
    HAVING COUNT(*) > 100

#### <a name="data-quality-assessment-verify-records-with-incorrect-longitude-andor-latitude"></a><span data-ttu-id="f178a-222">Avaliação de qualidade de dados: verificar registros com longitude e/ou latitude incorretos</span><span class="sxs-lookup"><span data-stu-id="f178a-222">Data Quality Assessment: Verify records with incorrect longitude and/or latitude</span></span>
<span data-ttu-id="f178a-223">Este exemplo examina se qualquer um dos campos de longitude e/ou latitude Olá conter um valor inválido (graus de radianos devem estar entre -90 e 90), ou ter (0, 0) coordenadas.</span><span class="sxs-lookup"><span data-stu-id="f178a-223">This example investigates if any of hello longitude and/or latitude fields either contain an invalid value (radian degrees should be between -90 and 90), or have (0, 0) coordinates.</span></span>

    SELECT COUNT(*) FROM nyctaxi_trip
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    AND  (CAST(pickup_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(pickup_latitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_latitude AS float) NOT BETWEEN -90 AND 90
    OR    (pickup_longitude = '0' AND pickup_latitude = '0')
    OR    (dropoff_longitude = '0' AND dropoff_latitude = '0'))

#### <a name="exploration-tipped-vs-not-tipped-trips-distribution"></a><span data-ttu-id="f178a-224">Exploração: distribuição de corridas com gorjeta versus sem gorjeta</span><span class="sxs-lookup"><span data-stu-id="f178a-224">Exploration: Tipped vs. Not Tipped Trips distribution</span></span>
<span data-ttu-id="f178a-225">Este exemplo localiza o número de saudação de viagens foram Oblíquo versus não-Oblíquo em um tempo determinado período (ou em Olá conjunto de dados completo se abrangendo ano Olá).</span><span class="sxs-lookup"><span data-stu-id="f178a-225">This example finds hello number of trips that were tipped vs. not tipped in a given time period (or in hello full dataset if covering hello full year).</span></span> <span data-ttu-id="f178a-226">Essa distribuição reflete Olá rótulo binário distribuição toobe usado posteriormente para modelagem de classificação binária.</span><span class="sxs-lookup"><span data-stu-id="f178a-226">This distribution reflects hello binary label distribution toobe later used for binary classification modeling.</span></span>

    SELECT tipped, COUNT(*) AS tip_freq FROM (
      SELECT CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END AS tipped, tip_amount
      FROM nyctaxi_fare
      WHERE pickup_datetime BETWEEN '20130101' AND '20131231') tc
    GROUP BY tipped

#### <a name="exploration-tip-classrange-distribution"></a><span data-ttu-id="f178a-227">Exploração: distribuição de classe/intervalo de gorjetas</span><span class="sxs-lookup"><span data-stu-id="f178a-227">Exploration: Tip Class/Range Distribution</span></span>
<span data-ttu-id="f178a-228">Esse exemplo calcula distribuição Olá de intervalos de dica em um tempo determinado período (ou em Olá conjunto de dados completo se abrangendo ano Olá).</span><span class="sxs-lookup"><span data-stu-id="f178a-228">This example computes hello distribution of tip ranges in a given time period (or in hello full dataset if covering hello full year).</span></span> <span data-ttu-id="f178a-229">Isso é a distribuição de saudação de classes de rótulo de saudação que serão usados posteriormente para modelagem de classificação multiclasse.</span><span class="sxs-lookup"><span data-stu-id="f178a-229">This is hello distribution of hello label classes that will be used later for multiclass classification modeling.</span></span>

    SELECT tip_class, COUNT(*) AS tip_freq FROM (
        SELECT CASE
            WHEN (tip_amount = 0) THEN 0
            WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
            WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
            WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
            ELSE 4
        END AS tip_class
    FROM nyctaxi_fare
    WHERE pickup_datetime BETWEEN '20130101' AND '20131231') tc
    GROUP BY tip_class

#### <a name="exploration-compute-and-compare-trip-distance"></a><span data-ttu-id="f178a-230">Exploração: calcular e comparar distância de viagem</span><span class="sxs-lookup"><span data-stu-id="f178a-230">Exploration: Compute and Compare Trip Distance</span></span>
<span data-ttu-id="f178a-231">Este exemplo converte a longitude de retirada e redistribuição hello e Geografia do latitude tooSQL pontos, calcula a distância de viagem hello usando o SQL geography pontos diferença e retorna uma amostra aleatória de resultados Olá para comparação.</span><span class="sxs-lookup"><span data-stu-id="f178a-231">This example converts hello pickup and drop-off longitude and latitude tooSQL geography points, computes hello trip distance using SQL geography points difference, and returns a random sample of hello results for comparison.</span></span> <span data-ttu-id="f178a-232">exemplo Hello limita os resultados de saudação toovalid coordena usando apenas a consulta de avaliação de qualidade dados Olá coberta anteriormente.</span><span class="sxs-lookup"><span data-stu-id="f178a-232">hello example limits hello results toovalid coordinates only using hello data quality assessment query covered earlier.</span></span>

    SELECT
    pickup_location=geography::STPointFromText('POINT(' + pickup_longitude + ' ' + pickup_latitude + ')', 4326)
    ,dropoff_location=geography::STPointFromText('POINT(' + dropoff_longitude + ' ' + dropoff_latitude + ')', 4326)
    ,trip_distance
    ,computedist=round(geography::STPointFromText('POINT(' + pickup_longitude + ' ' + pickup_latitude + ')', 4326).STDistance(geography::STPointFromText('POINT(' + dropoff_longitude + ' ' + dropoff_latitude + ')', 4326))/1000, 2)
    FROM nyctaxi_trip
    tablesample(0.01 percent)
    WHERE CAST(pickup_latitude AS float) BETWEEN -90 AND 90
    AND   CAST(dropoff_latitude AS float) BETWEEN -90 AND 90
    AND   pickup_longitude != '0' AND dropoff_longitude != '0'

#### <a name="feature-engineering-in-sql-queries"></a><span data-ttu-id="f178a-233">Engenharia de recursos em consultas SQL</span><span class="sxs-lookup"><span data-stu-id="f178a-233">Feature Engineering in SQL Queries</span></span>
<span data-ttu-id="f178a-234">Olá rótulo geração e Geografia conversão exploração consultas também podem ser usado toogenerate rótulos/recursos removendo Olá parte de contagem.</span><span class="sxs-lookup"><span data-stu-id="f178a-234">hello label generation and geography conversion exploration queries can also be used toogenerate labels/features by removing hello counting part.</span></span> <span data-ttu-id="f178a-235">São fornecidos exemplos SQL engenharia de recurso adicional Olá [exploração de dados e de engenharia de recurso no bloco de anotações do IPython](#ipnb) seção.</span><span class="sxs-lookup"><span data-stu-id="f178a-235">Additional feature engineering SQL examples are provided in hello [Data Exploration and Feature Engineering in IPython Notebook](#ipnb) section.</span></span> <span data-ttu-id="f178a-236">É mais eficiente toorun Olá recurso geração consultas na Olá conjunto de dados completo ou um grande subconjunto dela usando consultas SQL que são executados diretamente na instância de banco de dados do SQL Server de saudação.</span><span class="sxs-lookup"><span data-stu-id="f178a-236">It is more efficient toorun hello feature generation queries on hello full dataset or a large subset of it using SQL queries which run directly on hello SQL Server database instance.</span></span> <span data-ttu-id="f178a-237">Olá consultas podem ser executadas no **SQL Server Management Studio**, bloco de anotações do IPython ou qualquer ferramenta/ambiente de desenvolvimento que pode acessar Olá banco de dados local ou remotamente.</span><span class="sxs-lookup"><span data-stu-id="f178a-237">hello queries may be executed in **SQL Server Management Studio**, IPython Notebook or any development tool/environment which can access hello database locally or remotely.</span></span>

#### <a name="preparing-data-for-model-building"></a><span data-ttu-id="f178a-238">Preparando dados para criação de modelo</span><span class="sxs-lookup"><span data-stu-id="f178a-238">Preparing Data for Model Building</span></span>
<span data-ttu-id="f178a-239">saudação de junções de consulta a seguir Olá **nyctaxi\_viagem** e **nyctaxi\_passagens** tabelas, gera um rótulo de classificação binária **Oblíquo**, um rótulo de classificação multiclasse **dica\_classe**e extrai uma amostra aleatória de 1% da saudação ingressado no conjunto de dados completo.</span><span class="sxs-lookup"><span data-stu-id="f178a-239">hello following query joins hello **nyctaxi\_trip** and **nyctaxi\_fare** tables, generates a binary classification label **tipped**, a multi-class classification label **tip\_class**, and extracts a 1% random sample from hello full joined dataset.</span></span> <span data-ttu-id="f178a-240">Essa consulta pode ser copiada e colada diretamente no hello [estúdio de aprendizado de máquina do Azure](https://studio.azureml.net) [importar dados] [ import-data] módulo para a ingestão de dados direta do banco de dados do SQL Server Olá instância no Azure.</span><span class="sxs-lookup"><span data-stu-id="f178a-240">This query can be copied then pasted directly in hello [Azure Machine Learning Studio](https://studio.azureml.net) [Import Data][import-data] module for direct data ingestion from hello SQL Server database instance in Azure.</span></span> <span data-ttu-id="f178a-241">consulta de saudação exclui registros com incorreto (0, 0) coordenadas.</span><span class="sxs-lookup"><span data-stu-id="f178a-241">hello query excludes records with incorrect (0, 0) coordinates.</span></span>

    SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount,     f.total_amount, f.tip_amount,
        CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END AS tipped,
        CASE WHEN (tip_amount = 0) THEN 0
            WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
            WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
            WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
            ELSE 4
        END AS tip_class
    FROM nyctaxi_trip t, nyctaxi_fare f
    TABLESAMPLE (1 percent)
    WHERE t.medallion = f.medallion
    AND   t.hack_license = f.hack_license
    AND   t.pickup_datetime = f.pickup_datetime
    AND   pickup_longitude != '0' AND dropoff_longitude != '0'


## <span data-ttu-id="f178a-242"><a name="ipnb"></a>Exploração de dados e engenharia de recursos no IPython Notebook</span><span class="sxs-lookup"><span data-stu-id="f178a-242"><a name="ipnb"></a>Data Exploration and Feature Engineering in IPython Notebook</span></span>
<span data-ttu-id="f178a-243">Nesta seção, vamos realizar exploração de dados e geração de recurso usando consultas Python e SQL no banco de dados do SQL Server Olá criado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="f178a-243">In this section, we will perform data exploration and feature generation using both Python and SQL queries against hello SQL Server database created earlier.</span></span> <span data-ttu-id="f178a-244">Um bloco de anotações de IPython de exemplo chamado **machine-Learning-data-science-process-sql-story.ipynb** é fornecido no hello **de anotações do IPython exemplo** pasta.</span><span class="sxs-lookup"><span data-stu-id="f178a-244">A sample IPython notebook named **machine-Learning-data-science-process-sql-story.ipynb** is provided in hello **Sample IPython Notebooks** folder.</span></span> <span data-ttu-id="f178a-245">Este caderno também está disponível no [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks).</span><span class="sxs-lookup"><span data-stu-id="f178a-245">This notebook is also available on [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks).</span></span>

<span data-ttu-id="f178a-246">Olá sequência recomendada ao trabalhar com dados grandes é seguir hello:</span><span class="sxs-lookup"><span data-stu-id="f178a-246">hello recommended sequence when working with big data is hello following:</span></span>

* <span data-ttu-id="f178a-247">Ler em uma pequena amostra dos dados de saudação em um quadro de dados na memória.</span><span class="sxs-lookup"><span data-stu-id="f178a-247">Read in a small sample of hello data into an in-memory data frame.</span></span>
* <span data-ttu-id="f178a-248">Execute algumas visualizações e explorações usando Olá dados amostrados.</span><span class="sxs-lookup"><span data-stu-id="f178a-248">Perform some visualizations and explorations using hello sampled data.</span></span>
* <span data-ttu-id="f178a-249">Testar usando dados de amostra de saudação de engenharia de recurso.</span><span class="sxs-lookup"><span data-stu-id="f178a-249">Experiment with feature engineering using hello sampled data.</span></span>
* <span data-ttu-id="f178a-250">Para exploração de dados maior, manipulação de dados e de engenharia de recurso, use os Python tooissue SQL consultas diretamente no banco de dados do SQL Server Olá Olá VM do Azure.</span><span class="sxs-lookup"><span data-stu-id="f178a-250">For larger data exploration, data manipulation and feature engineering, use Python tooissue SQL Queries directly against hello SQL Server database in hello Azure VM.</span></span>
* <span data-ttu-id="f178a-251">Decida Olá toouse de tamanho de exemplo para criação de modelo de aprendizado de máquina do Azure.</span><span class="sxs-lookup"><span data-stu-id="f178a-251">Decide hello sample size toouse for Azure Machine Learning model building.</span></span>

<span data-ttu-id="f178a-252">Quando estiver pronto tooproceed tooAzure aprendizado de máquina, você pode ser:</span><span class="sxs-lookup"><span data-stu-id="f178a-252">When ready tooproceed tooAzure Machine Learning, you may either:</span></span>  

1. <span data-ttu-id="f178a-253">Salvar Olá final SQL consulta tooextract e exemplo hello dados e copiar e colar Olá consulta diretamente em um [importar dados] [ import-data] módulo no aprendizado de máquina do Azure.</span><span class="sxs-lookup"><span data-stu-id="f178a-253">Save hello final SQL query tooextract and sample hello data and copy-paste hello query directly into a [Import Data][import-data] module in Azure Machine Learning.</span></span> <span data-ttu-id="f178a-254">Esse método é demonstrado no hello [criando modelos no aprendizado de máquina do Azure](#mlmodel) seção.</span><span class="sxs-lookup"><span data-stu-id="f178a-254">This method is demonstrated in hello [Building Models in Azure Machine Learning](#mlmodel) section.</span></span>    
2. <span data-ttu-id="f178a-255">Manter Olá amostradas e os dados de engenharia planejar toouse para criar uma nova tabela de banco de dados de modelo e usar a nova tabela de saudação no hello [importar dados] [ import-data] módulo.</span><span class="sxs-lookup"><span data-stu-id="f178a-255">Persist hello sampled and engineered data you plan toouse for model building in a new database table, then use hello new table in hello [Import Data][import-data] module.</span></span>

<span data-ttu-id="f178a-256">Olá seguem alguns exploração de dados, visualização de dados e exemplos de engenharia de recurso.</span><span class="sxs-lookup"><span data-stu-id="f178a-256">hello following are a few data exploration, data visualization, and feature engineering examples.</span></span> <span data-ttu-id="f178a-257">Para obter mais exemplos, consulte o bloco de anotações do IPython SQL de exemplo de hello no hello **de anotações do IPython exemplo** pasta.</span><span class="sxs-lookup"><span data-stu-id="f178a-257">For more examples, see hello sample SQL IPython notebook in hello **Sample IPython Notebooks** folder.</span></span>

#### <a name="initialize-database-credentials"></a><span data-ttu-id="f178a-258">Inicializar as credenciais de banco de dados</span><span class="sxs-lookup"><span data-stu-id="f178a-258">Initialize Database Credentials</span></span>
<span data-ttu-id="f178a-259">Inicialize as configurações de conexão de banco de dados em Olá variáveis a seguir:</span><span class="sxs-lookup"><span data-stu-id="f178a-259">Initialize your database connection settings in hello following variables:</span></span>

    SERVER_NAME=<server name>
    DATABASE_NAME=<database name>
    USERID=<user name>
    PASSWORD=<password>
    DB_DRIVER = <database server>

#### <a name="create-database-connection"></a><span data-ttu-id="f178a-260">Criar conexão de banco de dados</span><span class="sxs-lookup"><span data-stu-id="f178a-260">Create Database Connection</span></span>
    CONNECTION_STRING = 'DRIVER={'+DRIVER+'};SERVER='+SERVER_NAME+';DATABASE='+DATABASE_NAME+';UID='+USERID+';PWD='+PASSWORD
    conn = pyodbc.connect(CONNECTION_STRING)

#### <a name="report-number-of-rows-and-columns-in-table-nyctaxitrip"></a><span data-ttu-id="f178a-261">Relatar o número de linhas e colunas na tabela nyctaxi_trip</span><span class="sxs-lookup"><span data-stu-id="f178a-261">Report number of rows and columns in table nyctaxi_trip</span></span>
    nrows = pd.read_sql('''
        SELECT SUM(rows) FROM sys.partitions
        WHERE object_id = OBJECT_ID('nyctaxi_trip')
    ''', conn)

    print 'Total number of rows = %d' % nrows.iloc[0,0]

    ncols = pd.read_sql('''
        SELECT COUNT(*) FROM information_schema.columns
        WHERE table_name = ('nyctaxi_trip')
    ''', conn)

    print 'Total number of columns = %d' % ncols.iloc[0,0]

* <span data-ttu-id="f178a-262">Número total de linhas = 173179759</span><span class="sxs-lookup"><span data-stu-id="f178a-262">Total number of rows = 173179759</span></span>  
* <span data-ttu-id="f178a-263">Número total de colunas = 14</span><span class="sxs-lookup"><span data-stu-id="f178a-263">Total number of columns = 14</span></span>

#### <a name="read-in-a-small-data-sample-from-hello-sql-server-database"></a><span data-ttu-id="f178a-264">Leitura-em uma amostra de dados pequenos de saudação banco de dados do SQL Server</span><span class="sxs-lookup"><span data-stu-id="f178a-264">Read-in a small data sample from hello SQL Server Database</span></span>
    t0 = time.time()

    query = '''
        SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax,
            f.tolls_amount, f.total_amount, f.tip_amount
        FROM nyctaxi_trip t, nyctaxi_fare f
        TABLESAMPLE (0.05 PERCENT)
        WHERE t.medallion = f.medallion
        AND   t.hack_license = f.hack_license
        AND   t.pickup_datetime = f.pickup_datetime
    '''

    df1 = pd.read_sql(query, conn)

    t1 = time.time()
    print 'Time tooread hello sample table is %f seconds' % (t1-t0)

    print 'Number of rows and columns retrieved = (%d, %d)' % (df1.shape[0], df1.shape[1])

<span data-ttu-id="f178a-265">Tabela de exemplo do tempo tooread Olá é 6.492000 segundos</span><span class="sxs-lookup"><span data-stu-id="f178a-265">Time tooread hello sample table is 6.492000 seconds</span></span>  
<span data-ttu-id="f178a-266">Número de linhas e colunas recuperadas = (84952, 21)</span><span class="sxs-lookup"><span data-stu-id="f178a-266">Number of rows and columns retrieved = (84952, 21)</span></span>

#### <a name="descriptive-statistics"></a><span data-ttu-id="f178a-267">Estatísticas Descritivas</span><span class="sxs-lookup"><span data-stu-id="f178a-267">Descriptive Statistics</span></span>
<span data-ttu-id="f178a-268">Agora são dados de amostra de saudação tooexplore pronto.</span><span class="sxs-lookup"><span data-stu-id="f178a-268">Now are ready tooexplore hello sampled data.</span></span> <span data-ttu-id="f178a-269">Vamos começar com olhando estatísticas descritivas para Olá **viagem\_distância** (ou qualquer outro) campos:</span><span class="sxs-lookup"><span data-stu-id="f178a-269">We start with looking at descriptive statistics for hello **trip\_distance** (or any other) field(s):</span></span>

    df1['trip_distance'].describe()

#### <a name="visualization-box-plot-example"></a><span data-ttu-id="f178a-270">Visualização: exemplo de plotagem da caixa</span><span class="sxs-lookup"><span data-stu-id="f178a-270">Visualization: Box Plot Example</span></span>
<span data-ttu-id="f178a-271">Em seguida, examinar diagrama em caixa Olá para Olá trip distância toovisualize Olá quantis</span><span class="sxs-lookup"><span data-stu-id="f178a-271">Next we look at hello box plot for hello trip distance toovisualize hello quantiles</span></span>

    df1.boxplot(column='trip_distance',return_type='dict')

![Plotar nº 1][1]

#### <a name="visualization-distribution-plot-example"></a><span data-ttu-id="f178a-273">Visualização: exemplo de plotagem de distribuição</span><span class="sxs-lookup"><span data-stu-id="f178a-273">Visualization: Distribution Plot Example</span></span>
    fig = plt.figure()
    ax1 = fig.add_subplot(1,2,1)
    ax2 = fig.add_subplot(1,2,2)
    df1['trip_distance'].plot(ax=ax1,kind='kde', style='b-')
    df1['trip_distance'].hist(ax=ax2, bins=100, color='k')

![Plotar nº 2][2]

#### <a name="visualization-bar-and-line-plots"></a><span data-ttu-id="f178a-275">Visualização: plotagens de barra e linha</span><span class="sxs-lookup"><span data-stu-id="f178a-275">Visualization: Bar and Line Plots</span></span>
<span data-ttu-id="f178a-276">Neste exemplo, podemos guardar a distância de viagem de saudação em cinco compartimentos e visualizar Olá compartimentação de resultados.</span><span class="sxs-lookup"><span data-stu-id="f178a-276">In this example, we bin hello trip distance into five bins and visualize hello binning results.</span></span>

    trip_dist_bins = [0, 1, 2, 4, 10, 1000]
    df1['trip_distance']
    trip_dist_bin_id = pd.cut(df1['trip_distance'], trip_dist_bins)
    trip_dist_bin_id

<span data-ttu-id="f178a-277">Pode plotar Olá acima distribuição bin em uma barra ou gráfico como abaixo da linha</span><span class="sxs-lookup"><span data-stu-id="f178a-277">We can plot hello above bin distribution in a bar or line plot as below</span></span>

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='bar')

![Plotar nº 3][3]

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='line')

![Plotar nº 4][4]

#### <a name="visualization-scatterplot-example"></a><span data-ttu-id="f178a-280">Visualização: exemplo de plotagem de dispersão</span><span class="sxs-lookup"><span data-stu-id="f178a-280">Visualization: Scatterplot Example</span></span>
<span data-ttu-id="f178a-281">Vamos mostrar gráfico de dispersão entre **viagem\_tempo\_na\_s** e **viagem\_distância** toosee se há qualquer correlação</span><span class="sxs-lookup"><span data-stu-id="f178a-281">We show scatter plot between **trip\_time\_in\_secs** and **trip\_distance** toosee if there is any correlation</span></span>

    plt.scatter(df1['trip_time_in_secs'], df1['trip_distance'])

![Plotar nº 6][6]

<span data-ttu-id="f178a-283">Da mesma forma, é possível verificar a relação Olá entre **taxa\_código** e **viagem\_distância**.</span><span class="sxs-lookup"><span data-stu-id="f178a-283">Similarly we can check hello relationship between **rate\_code** and **trip\_distance**.</span></span>

    plt.scatter(df1['passenger_count'], df1['trip_distance'])

![Plotar nº 8][8]

### <a name="sub-sampling-hello-data-in-sql"></a><span data-ttu-id="f178a-285">Saudação de amostragem sub dados no SQL</span><span class="sxs-lookup"><span data-stu-id="f178a-285">Sub-Sampling hello Data in SQL</span></span>
<span data-ttu-id="f178a-286">Ao preparar dados para o modelo de criação no [estúdio de aprendizado de máquina do Azure](https://studio.azureml.net), ou pode decidir Olá **toouse de consulta SQL diretamente no módulo de importação de dados de saudação** ou manter Olá engenharia e de amostra dados em uma nova tabela, você pode usar em Olá [importar dados] [ import-data] módulo com um simples **selecione * FROM < seu\_novo\_tabela\_nome >**.</span><span class="sxs-lookup"><span data-stu-id="f178a-286">When preparing data for model building in [Azure Machine Learning Studio](https://studio.azureml.net), you may either decide on hello **SQL query toouse directly in hello Import Data module** or persist hello engineered and sampled data in a new table, which you could use in hello [Import Data][import-data] module with a simple **SELECT * FROM <your\_new\_table\_name>**.</span></span>

<span data-ttu-id="f178a-287">Nesta seção, vamos criar um novo toohold Olá da tabela de amostra e dados de engenharia.</span><span class="sxs-lookup"><span data-stu-id="f178a-287">In this section we will create a new table toohold hello sampled and engineered data.</span></span> <span data-ttu-id="f178a-288">Um exemplo de uma consulta SQL direto para a construção de modelo é fornecido no hello [exploração de dados e de engenharia de recurso no SQL Server](#dbexplore) seção.</span><span class="sxs-lookup"><span data-stu-id="f178a-288">An example of a direct SQL query for model building is provided in hello [Data Exploration and Feature Engineering in SQL Server](#dbexplore) section.</span></span>

#### <a name="create-a-sample-table-and-populate-with-1-of-hello-joined-tables-drop-table-first-if-it-exists"></a><span data-ttu-id="f178a-289">Crie uma tabela de exemplo e preencher com % 1 de saudação Unido tabelas.</span><span class="sxs-lookup"><span data-stu-id="f178a-289">Create a Sample Table and Populate with 1% of hello Joined Tables.</span></span> <span data-ttu-id="f178a-290">Descartar a tabela primeiro se ela existir.</span><span class="sxs-lookup"><span data-stu-id="f178a-290">Drop Table First if it Exists.</span></span>
<span data-ttu-id="f178a-291">Nesta seção, podemos unir tabelas Olá **nyctaxi\_viagem** e **nyctaxi\_passagens**, extrair uma amostra aleatória de 1% e manter dados de saudação de amostra em um novo nome de tabela  **nyctaxi\_um\_%**:</span><span class="sxs-lookup"><span data-stu-id="f178a-291">In this section, we join hello tables **nyctaxi\_trip** and **nyctaxi\_fare**, extract a 1% random sample, and persist hello sampled data in a new table name **nyctaxi\_one\_percent**:</span></span>

    cursor = conn.cursor()

    drop_table_if_exists = '''
        IF OBJECT_ID('nyctaxi_one_percent', 'U') IS NOT NULL DROP TABLE nyctaxi_one_percent
    '''

    nyctaxi_one_percent_insert = '''
        SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount, f.total_amount, f.tip_amount
        INTO nyctaxi_one_percent
        FROM nyctaxi_trip t, nyctaxi_fare f
        TABLESAMPLE (1 PERCENT)
        WHERE t.medallion = f.medallion
        AND   t.hack_license = f.hack_license
        AND   t.pickup_datetime = f.pickup_datetime
        AND   pickup_longitude <> '0' AND dropoff_longitude <> '0'
    '''

    cursor.execute(drop_table_if_exists)
    cursor.execute(nyctaxi_one_percent_insert)
    cursor.commit()

### <a name="data-exploration-using-sql-queries-in-ipython-notebook"></a><span data-ttu-id="f178a-292">Exploração de dados usando consultas SQL em IPython Notebook</span><span class="sxs-lookup"><span data-stu-id="f178a-292">Data Exploration using SQL Queries in IPython Notebook</span></span>
<span data-ttu-id="f178a-293">Nesta seção, exploraremos distribuições de dados usando dados de % 1 de amostra de saudação que são mantidos em nova tabela de saudação criado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="f178a-293">In this section, we explore data distributions using hello 1% sampled data which is persisted in hello new table we created above.</span></span> <span data-ttu-id="f178a-294">Observe que explorações semelhantes podem ser realizadas usando tabelas originais do hello, opcionalmente usando **TABLESAMPLE** tooa dado período de tempo usando Olá resultados da exploração de saudação de toolimit exemplo ou limitando Olá **retirada \_datetime** partições, conforme ilustrado na Olá [exploração de dados e de engenharia de recurso no SQL Server](#dbexplore) seção.</span><span class="sxs-lookup"><span data-stu-id="f178a-294">Note that similar explorations can be performed using hello original tables, optionally using **TABLESAMPLE** toolimit hello exploration sample or by limiting hello results tooa given time period using hello **pickup\_datetime** partitions, as illustrated in hello [Data Exploration and Feature Engineering in SQL Server](#dbexplore) section.</span></span>

#### <a name="exploration-daily-distribution-of-trips"></a><span data-ttu-id="f178a-295">Exploração: distribuição diária de corridas</span><span class="sxs-lookup"><span data-stu-id="f178a-295">Exploration: Daily distribution of trips</span></span>
    query = '''
        SELECT CONVERT(date, dropoff_datetime) AS date, COUNT(*) AS c
        FROM nyctaxi_one_percent
        GROUP BY CONVERT(date, dropoff_datetime)
    '''

    pd.read_sql(query,conn)

#### <a name="exploration-trip-distribution-per-medallion"></a><span data-ttu-id="f178a-296">Exploração: distribuição de corridas por licença</span><span class="sxs-lookup"><span data-stu-id="f178a-296">Exploration: Trip distribution per medallion</span></span>
    query = '''
        SELECT medallion,count(*) AS c
        FROM nyctaxi_one_percent
        GROUP BY medallion
    '''

    pd.read_sql(query,conn)

### <a name="feature-generation-using-sql-queries-in-ipython-notebook"></a><span data-ttu-id="f178a-297">Geração de recursos usando consultas SQL no IPython Notebook</span><span class="sxs-lookup"><span data-stu-id="f178a-297">Feature Generation Using SQL Queries in IPython Notebook</span></span>
<span data-ttu-id="f178a-298">Nesta seção gerar novos rótulos e recursos diretamente usando consultas SQL, operando na tabela de amostra de 1% Olá criada na seção anterior hello.</span><span class="sxs-lookup"><span data-stu-id="f178a-298">In this section we will generate new labels and features directly using SQL queries, operating on hello 1% sample table we created in hello previous section.</span></span>

#### <a name="label-generation-generate-class-labels"></a><span data-ttu-id="f178a-299">Geração de rótulo: gerar rótulos de classe</span><span class="sxs-lookup"><span data-stu-id="f178a-299">Label Generation: Generate Class Labels</span></span>
<span data-ttu-id="f178a-300">Saudação de exemplo a seguir, geramos dois conjuntos de toouse de rótulos para modelagem:</span><span class="sxs-lookup"><span data-stu-id="f178a-300">In hello following example, we generate two sets of labels toouse for modeling:</span></span>

1. <span data-ttu-id="f178a-301">Rótulos de classe binária **tipped** (prevendo se uma gorjeta será fornecida)</span><span class="sxs-lookup"><span data-stu-id="f178a-301">Binary Class Labels **tipped** (predicting if a tip will be given)</span></span>
2. <span data-ttu-id="f178a-302">Rótulos multiclasse **dica\_classe** (prevendo bin de dica de saudação ou intervalo)</span><span class="sxs-lookup"><span data-stu-id="f178a-302">Multiclass Labels **tip\_class** (predicting hello tip bin or range)</span></span>
   
        nyctaxi_one_percent_add_col = '''
            ALTER TABLE nyctaxi_one_percent ADD tipped bit, tip_class int
        '''
   
        cursor.execute(nyctaxi_one_percent_add_col)
        cursor.commit()
   
        nyctaxi_one_percent_update_col = '''
            UPDATE nyctaxi_one_percent
            SET
               tipped = CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END,
               tip_class = CASE WHEN (tip_amount = 0) THEN 0
                                WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
                                WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
                                WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
                                ELSE 4
                            END
        '''
   
        cursor.execute(nyctaxi_one_percent_update_col)
        cursor.commit()

#### <a name="feature-engineering-count-features-for-categorical-columns"></a><span data-ttu-id="f178a-303">Engenharia de recurso: recursos de contagem de colunas categóricas</span><span class="sxs-lookup"><span data-stu-id="f178a-303">Feature Engineering: Count Features for Categorical Columns</span></span>
<span data-ttu-id="f178a-304">Este exemplo transforma um campo de categoria em um campo numérico, substituindo cada categoria por contagem de saudação de suas ocorrências nos dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="f178a-304">This example transforms a categorical field into a numeric field by replacing each category with hello count of its occurrences in hello data.</span></span>

    nyctaxi_one_percent_insert_col = '''
        ALTER TABLE nyctaxi_one_percent ADD cmt_count int, vts_count int
    '''

    cursor.execute(nyctaxi_one_percent_insert_col)
    cursor.commit()

    nyctaxi_one_percent_update_col = '''
        WITH B AS
        (
            SELECT medallion, hack_license,
                SUM(CASE WHEN vendor_id = 'cmt' THEN 1 ELSE 0 END) AS cmt_count,
                SUM(CASE WHEN vendor_id = 'vts' THEN 1 ELSE 0 END) AS vts_count
            FROM nyctaxi_one_percent
            GROUP BY medallion, hack_license
        )

        UPDATE nyctaxi_one_percent
        SET nyctaxi_one_percent.cmt_count = B.cmt_count,
            nyctaxi_one_percent.vts_count = B.vts_count
        FROM nyctaxi_one_percent A INNER JOIN B
        ON A.medallion = B.medallion AND A.hack_license = B.hack_license
    '''

    cursor.execute(nyctaxi_one_percent_update_col)
    cursor.commit()

#### <a name="feature-engineering-bin-features-for-numerical-columns"></a><span data-ttu-id="f178a-305">Engenharia de recurso: recursos de compartimento para colunas numéricas</span><span class="sxs-lookup"><span data-stu-id="f178a-305">Feature Engineering: Bin features for Numerical Columns</span></span>
<span data-ttu-id="f178a-306">Este exemplo transforma um campo numérico contínuo em intervalos de categoria predefinidos, ou seja, transformação de campo numérico em um campo de categoria.</span><span class="sxs-lookup"><span data-stu-id="f178a-306">This example transforms a continuous numeric field into preset category ranges, i.e., transform numeric field into a categorical field.</span></span>

    nyctaxi_one_percent_insert_col = '''
        ALTER TABLE nyctaxi_one_percent ADD trip_time_bin int
    '''

    cursor.execute(nyctaxi_one_percent_insert_col)
    cursor.commit()

    nyctaxi_one_percent_update_col = '''
        WITH B(medallion,hack_license,pickup_datetime,trip_time_in_secs, BinNumber ) AS
        (
            SELECT medallion,hack_license,pickup_datetime,trip_time_in_secs,
            NTILE(5) OVER (ORDER BY trip_time_in_secs) AS BinNumber from nyctaxi_one_percent
        )

        UPDATE nyctaxi_one_percent
        SET trip_time_bin = B.BinNumber
        FROM nyctaxi_one_percent A INNER JOIN B
        ON A.medallion = B.medallion
        AND A.hack_license = B.hack_license
        AND A.pickup_datetime = B.pickup_datetime
    '''

    cursor.execute(nyctaxi_one_percent_update_col)
    cursor.commit()

#### <a name="feature-engineering-extract-location-features-from-decimal-latitudelongitude"></a><span data-ttu-id="f178a-307">Recurso de engenharia: extrair recursos de local de latitude/longitude decimal</span><span class="sxs-lookup"><span data-stu-id="f178a-307">Feature Engineering: Extract Location Features from Decimal Latitude/Longitude</span></span>
<span data-ttu-id="f178a-308">Este exemplo divide representação decimal de saudação de um campo de latitude e/ou de longitude em vários campos de região de granularidade diferente, como país, cidade, cidade, bloquear, etc. Observe que Olá novos geo-campos não mapeados tooactual locais.</span><span class="sxs-lookup"><span data-stu-id="f178a-308">This example breaks down hello decimal representation of a latitude and/or longitude field into multiple region fields of different granularity, such as, country, city, town, block, etc. Note that hello new geo-fields are not mapped tooactual locations.</span></span> <span data-ttu-id="f178a-309">Para saber mais sobre o mapeamento de locais de codificação geográfica, veja [Serviços REST do Bing Mapas](https://msdn.microsoft.com/library/ff701710.aspx).</span><span class="sxs-lookup"><span data-stu-id="f178a-309">For information on mapping geocode locations, see [Bing Maps REST Services](https://msdn.microsoft.com/library/ff701710.aspx).</span></span>

    nyctaxi_one_percent_insert_col = '''
        ALTER TABLE nyctaxi_one_percent
        ADD l1 varchar(6), l2 varchar(3), l3 varchar(3), l4 varchar(3),
            l5 varchar(3), l6 varchar(3), l7 varchar(3)
    '''

    cursor.execute(nyctaxi_one_percent_insert_col)
    cursor.commit()

    nyctaxi_one_percent_update_col = '''
        UPDATE nyctaxi_one_percent
        SET l1=round(pickup_longitude,0)
            , l2 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 1 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),1,1) ELSE '0' END     
            , l3 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 2 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),2,1) ELSE '0' END     
            , l4 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 3 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),3,1) ELSE '0' END     
            , l5 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 4 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),4,1) ELSE '0' END     
            , l6 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 5 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),5,1) ELSE '0' END     
            , l7 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 6 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),6,1) ELSE '0' END
    '''

    cursor.execute(nyctaxi_one_percent_update_col)
    cursor.commit()

#### <a name="verify-hello-final-form-of-hello-featurized-table"></a><span data-ttu-id="f178a-310">Verifique se a forma final de saudação da tabela de featurized Olá</span><span class="sxs-lookup"><span data-stu-id="f178a-310">Verify hello final form of hello featurized table</span></span>
    query = '''SELECT TOP 100 * FROM nyctaxi_one_percent'''
    pd.read_sql(query,conn)

<span data-ttu-id="f178a-311">Agora, estamos prontos tooproceed toomodel criação e implantação de modelo no [aprendizado de máquina do Azure](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="f178a-311">We are now ready tooproceed toomodel building and model deployment in [Azure Machine Learning](https://studio.azureml.net).</span></span> <span data-ttu-id="f178a-312">dados de saudação estão prontos para qualquer Olá previsão problemas identificados anteriormente, ou seja:</span><span class="sxs-lookup"><span data-stu-id="f178a-312">hello data is ready for any of hello prediction problems identified earlier, namely:</span></span>

1. <span data-ttu-id="f178a-313">Classificação binária: toopredict ou não uma dica foi pago uma viagem.</span><span class="sxs-lookup"><span data-stu-id="f178a-313">Binary classification: toopredict whether or not a tip was paid for a trip.</span></span>
2. <span data-ttu-id="f178a-314">Classificação multiclasse: intervalo de saudação toopredict de dica pago, de acordo com toohello classes definidas anteriormente.</span><span class="sxs-lookup"><span data-stu-id="f178a-314">Multiclass classification: toopredict hello range of tip paid, according toohello previously defined classes.</span></span>
3. <span data-ttu-id="f178a-315">Tarefa de regressão: o valor de saudação toopredict de dica pago para uma viagem.</span><span class="sxs-lookup"><span data-stu-id="f178a-315">Regression task: toopredict hello amount of tip paid for a trip.</span></span>  

## <span data-ttu-id="f178a-316">
            <a name="mlmodel">
            </a>Criando modelos no Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="f178a-316"><a name="mlmodel"></a>Building Models in Azure Machine Learning</span></span>
<span data-ttu-id="f178a-317">toobegin Olá exercício de modelagem, faça logon no espaço de trabalho do tooyour aprendizado de máquina do Azure.</span><span class="sxs-lookup"><span data-stu-id="f178a-317">toobegin hello modeling exercise, log in tooyour Azure Machine Learning workspace.</span></span> <span data-ttu-id="f178a-318">Se ainda não tiver criado um espaço de trabalho do Machine Learning, consulte [Criar um espaço de trabalho do Azure Machine Learning](machine-learning-create-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="f178a-318">If you have not yet created a machine learning workspace, see [Create an Azure Machine Learning workspace](machine-learning-create-workspace.md).</span></span>

1. <span data-ttu-id="f178a-319">tooget iniciado com o aprendizado de máquina do Azure, consulte [o que é o estúdio de aprendizado de máquina do Azure?](machine-learning-what-is-ml-studio.md)</span><span class="sxs-lookup"><span data-stu-id="f178a-319">tooget started with Azure Machine Learning, see [What is Azure Machine Learning Studio?](machine-learning-what-is-ml-studio.md)</span></span>
2. <span data-ttu-id="f178a-320">Faça logon no muito[estúdio de aprendizado de máquina do Azure](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="f178a-320">Log in too[Azure Machine Learning Studio](https://studio.azureml.net).</span></span>
3. <span data-ttu-id="f178a-321">Olá Studio Home page do fornece uma grande quantidade de informações, vídeos, tutoriais, links toohello Referência de módulos e outros recursos.</span><span class="sxs-lookup"><span data-stu-id="f178a-321">hello Studio Home page provides a wealth of information, videos, tutorials, links toohello Modules Reference, and other resources.</span></span> <span data-ttu-id="f178a-322">Para obter mais informações sobre o aprendizado de máquina do Azure, consulte Olá [Centro de documentação do aprendizado de máquina do Azure](https://azure.microsoft.com/documentation/services/machine-learning/).</span><span class="sxs-lookup"><span data-stu-id="f178a-322">Fore more information about Azure Machine Learning, consult hello [Azure Machine Learning Documentation Center](https://azure.microsoft.com/documentation/services/machine-learning/).</span></span>

<span data-ttu-id="f178a-323">Uma experiência de treinamento típico consiste em seguir hello:</span><span class="sxs-lookup"><span data-stu-id="f178a-323">A typical training experiment consists of hello following:</span></span>

1. <span data-ttu-id="f178a-324">Criar uma experiência **+NEW** .</span><span class="sxs-lookup"><span data-stu-id="f178a-324">Create a **+NEW** experiment.</span></span>
2. <span data-ttu-id="f178a-325">Obter dados de saudação tooAzure aprendizado de máquina.</span><span class="sxs-lookup"><span data-stu-id="f178a-325">Get hello data tooAzure Machine Learning.</span></span>
3. <span data-ttu-id="f178a-326">Pré-processar, transformar e manipular dados saudação conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="f178a-326">Pre-process, transform and manipulate hello data as needed.</span></span>
4. <span data-ttu-id="f178a-327">Gerar recursos conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="f178a-327">Generate features as needed.</span></span>
5. <span data-ttu-id="f178a-328">Dividir dados saudação em conjuntos de dados de treinamento / / teste de validação (ou têm conjuntos de dados separados para cada).</span><span class="sxs-lookup"><span data-stu-id="f178a-328">Split hello data into training/validation/testing datasets(or have separate datasets for each).</span></span>
6. <span data-ttu-id="f178a-329">Selecione um ou mais algoritmos dependendo Olá toosolve problema de aprendizado de aprendizado de máquina.</span><span class="sxs-lookup"><span data-stu-id="f178a-329">Select one or more machine learning algorithms depending on hello learning problem toosolve.</span></span> <span data-ttu-id="f178a-330">Por exemplo, classificação binária, classificação multiclasse ou regressão.</span><span class="sxs-lookup"><span data-stu-id="f178a-330">E.g., binary classification, multiclass classification, regression.</span></span>
7. <span data-ttu-id="f178a-331">Treine um ou mais modelos usando o conjunto de dados de treinamento hello.</span><span class="sxs-lookup"><span data-stu-id="f178a-331">Train one or more models using hello training dataset.</span></span>
8. <span data-ttu-id="f178a-332">Classificar o conjunto de dados de validação de saudação usando modelos treinados hello.</span><span class="sxs-lookup"><span data-stu-id="f178a-332">Score hello validation dataset using hello trained model(s).</span></span>
9. <span data-ttu-id="f178a-333">Avalie Olá modelos toocompute Olá relevante de métricas para Olá problema de aprendizado.</span><span class="sxs-lookup"><span data-stu-id="f178a-333">Evaluate hello model(s) toocompute hello relevant metrics for hello learning problem.</span></span>
10. <span data-ttu-id="f178a-334">Ajuste Olá modelo (s) e selecione Olá melhor modelo toodeploy.</span><span class="sxs-lookup"><span data-stu-id="f178a-334">Fine tune hello model(s) and select hello best model toodeploy.</span></span>

<span data-ttu-id="f178a-335">Neste exercício, nós já explorados e engenharia dados Olá no SQL Server e decidir sobre tooingest de tamanho de exemplo hello no aprendizado de máquina do Azure.</span><span class="sxs-lookup"><span data-stu-id="f178a-335">In this exercise, we have already explored and engineered hello data in SQL Server, and decided on hello sample size tooingest in Azure Machine Learning.</span></span> <span data-ttu-id="f178a-336">toobuild um ou mais dos modelos de previsão Olá decidimos:</span><span class="sxs-lookup"><span data-stu-id="f178a-336">toobuild one or more of hello prediction models we decided:</span></span>

1. <span data-ttu-id="f178a-337">Obter dados de saudação tooAzure aprendizado de máquina usando Olá [importar dados] [ import-data] módulo, disponível no hello **dados de entrada e saída** seção.</span><span class="sxs-lookup"><span data-stu-id="f178a-337">Get hello data tooAzure Machine Learning using hello [Import Data][import-data] module, available in hello **Data Input and Output** section.</span></span> <span data-ttu-id="f178a-338">Para obter mais informações, consulte Olá [importar dados] [ import-data] página de referência de módulo.</span><span class="sxs-lookup"><span data-stu-id="f178a-338">For more information, see hello [Import Data][import-data] module reference page.</span></span>
   
    ![Importar Dados no Azure Machine Learning][17]
2. <span data-ttu-id="f178a-340">Selecione **banco de dados do SQL Azure** como Olá **fonte de dados** em Olá **propriedades** painel.</span><span class="sxs-lookup"><span data-stu-id="f178a-340">Select **Azure SQL Database** as hello **Data source** in hello **Properties** panel.</span></span>
3. <span data-ttu-id="f178a-341">Digite o nome DNS de banco de dados de saudação em Olá **nome do servidor de banco de dados** campo.</span><span class="sxs-lookup"><span data-stu-id="f178a-341">Enter hello database DNS name in hello **Database server name** field.</span></span> <span data-ttu-id="f178a-342">Formato: `tcp:<your_virtual_machine_DNS_name>,1433`</span><span class="sxs-lookup"><span data-stu-id="f178a-342">Format: `tcp:<your_virtual_machine_DNS_name>,1433`</span></span>
4. <span data-ttu-id="f178a-343">Digite hello **nome do banco de dados** no campo correspondente do hello.</span><span class="sxs-lookup"><span data-stu-id="f178a-343">Enter hello **Database name** in hello corresponding field.</span></span>
5. <span data-ttu-id="f178a-344">Digite hello **nome de usuário SQL** em hello * * aqccount nome de usuário e senha Olá Olá **senha de conta de usuário do servidor**.</span><span class="sxs-lookup"><span data-stu-id="f178a-344">Enter hello **SQL user name** in hello **Server user aqccount name, and hello password in hello **Server user account password**.</span></span>
6. <span data-ttu-id="f178a-345">Marque a opção **Aceitar qualquer certificado do servidor** .</span><span class="sxs-lookup"><span data-stu-id="f178a-345">Check **Accept any server certificate** option.</span></span>
7. <span data-ttu-id="f178a-346">Em Olá **consulta de banco de dados** editar a área de texto, cole a consulta Olá extrai Olá necessário campos (incluindo quaisquer campos calculados como rótulos de saudação) de banco de dados e para baixo amostras de tamanho de exemplo hello dados toohello desejado.</span><span class="sxs-lookup"><span data-stu-id="f178a-346">In hello **Database query** edit text area, paste hello query which extracts hello necessary database fields (including any computed fields such as hello labels) and down samples hello data toohello desired sample size.</span></span>

<span data-ttu-id="f178a-347">É um exemplo de um experimento de classificação binária ler dados diretamente do banco de dados do SQL Server Olá figura de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="f178a-347">An example of a binary classification experiment reading data directly from hello SQL Server database is in hello figure below.</span></span> <span data-ttu-id="f178a-348">Experimentos semelhantes podem ser construídos por meio de classificação multiclasse e problemas de regressão.</span><span class="sxs-lookup"><span data-stu-id="f178a-348">Similar experiments can be constructed for multiclass classification and regression problems.</span></span>

![Treinamento do Azure Machine Learning][10]

> [!IMPORTANT]
> <span data-ttu-id="f178a-350">Em Olá modelagem de extração de dados e exemplos de consulta fornecidos nas seções anteriores, de amostragem **todos os rótulos para os exercícios de modelagem Olá três são incluídos na consulta Olá**.</span><span class="sxs-lookup"><span data-stu-id="f178a-350">In hello modeling data extraction and sampling query examples provided in previous sections, **all labels for hello three modeling exercises are included in hello query**.</span></span> <span data-ttu-id="f178a-351">Uma etapa importante (obrigatório) em cada Olá exercícios de modelagem é muito**excluir** Olá rótulos desnecessários para Olá outros dois problemas e qualquer outro **vazamentos de destino**.</span><span class="sxs-lookup"><span data-stu-id="f178a-351">An important (required) step in each of hello modeling exercises is too**exclude** hello unnecessary labels for hello other two problems, and any other **target leaks**.</span></span> <span data-ttu-id="f178a-352">Para por exemplo, ao usar a classificação binária, use rótulo Olá **Oblíquo** e excluir campos Olá **dica\_classe**, **dica\_quantidade**, e **total\_quantidade**.</span><span class="sxs-lookup"><span data-stu-id="f178a-352">For e.g., when using binary classification, use hello label **tipped** and exclude hello fields **tip\_class**, **tip\_amount**, and **total\_amount**.</span></span> <span data-ttu-id="f178a-353">Olá último vazamentos de destino já que eles implicam dica Olá pagas.</span><span class="sxs-lookup"><span data-stu-id="f178a-353">hello latter are target leaks since they imply hello tip paid.</span></span>
> 
> <span data-ttu-id="f178a-354">as colunas desnecessárias tooexclude e/ou vazamentos de destino, você pode usar o hello [selecionar colunas no conjunto de dados] [ select-columns] módulo ou hello [editar metadados] [ edit-metadata].</span><span class="sxs-lookup"><span data-stu-id="f178a-354">tooexclude unnecessary columns and/or target leaks, you may use hello [Select Columns in Dataset][select-columns] module or hello [Edit Metadata][edit-metadata].</span></span> <span data-ttu-id="f178a-355">Para saber mais, veja as páginas de referência [Selecionar Colunas no Conjunto de Dados][select-columns] e [Editar Metadados][edit-metadata].</span><span class="sxs-lookup"><span data-stu-id="f178a-355">For more information, see [Select Columns in Dataset][select-columns] and [Edit Metadata][edit-metadata] reference pages.</span></span>
> 
> 

## <span data-ttu-id="f178a-356">
            <a name="mldeploy">
            </a>Implantando modelos no Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="f178a-356"><a name="mldeploy"></a>Deploying Models in Azure Machine Learning</span></span>
<span data-ttu-id="f178a-357">Quando o modelo estiver pronto, pode facilmente implantá-lo como um serviço web diretamente do experimento hello.</span><span class="sxs-lookup"><span data-stu-id="f178a-357">When your model is ready, you can easily deploy it as a web service directly from hello experiment.</span></span> <span data-ttu-id="f178a-358">Para obter mais informações sobre como implantar os serviços Web do Azure Machine Learning, veja [Implantar um serviço Web do Azure Machine Learning](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="f178a-358">For more information about deploying Azure Machine Learning web services, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

<span data-ttu-id="f178a-359">toodeploy um novo serviço da web, você precisa:</span><span class="sxs-lookup"><span data-stu-id="f178a-359">toodeploy a new web service, you need to:</span></span>

1. <span data-ttu-id="f178a-360">Criar um experimento de pontuação.</span><span class="sxs-lookup"><span data-stu-id="f178a-360">Create a scoring experiment.</span></span>
2. <span data-ttu-id="f178a-361">Implante o serviço web de saudação.</span><span class="sxs-lookup"><span data-stu-id="f178a-361">Deploy hello web service.</span></span>

<span data-ttu-id="f178a-362">toocreate experiência de uma pontuação de um **concluído** experiência de treinamento, clique em **criar experiência de PONTUAÇÃO** na barra de ação inferior hello.</span><span class="sxs-lookup"><span data-stu-id="f178a-362">toocreate a scoring experiment from a **Finished** training experiment, click **CREATE SCORING EXPERIMENT** in hello lower action bar.</span></span>

![Pontuação do Azure][18]

<span data-ttu-id="f178a-364">O aprendizado de máquina do Azure tentará toocreate uma experiência de pontuação com base nos componentes de saudação da experiência de treinamento hello.</span><span class="sxs-lookup"><span data-stu-id="f178a-364">Azure Machine Learning will attempt toocreate a scoring experiment based on hello components of hello training experiment.</span></span> <span data-ttu-id="f178a-365">Em especial, ele vai:</span><span class="sxs-lookup"><span data-stu-id="f178a-365">In particular, it will:</span></span>

1. <span data-ttu-id="f178a-366">Salvar modelo treinado hello e remover os módulos de treinamento de modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="f178a-366">Save hello trained model and remove hello model training modules.</span></span>
2. <span data-ttu-id="f178a-367">Identificar uma lógica **porta de entrada** toorepresent Olá esperado o esquema de dados de entrada.</span><span class="sxs-lookup"><span data-stu-id="f178a-367">Identify a logical **input port** toorepresent hello expected input data schema.</span></span>
3. <span data-ttu-id="f178a-368">Identificar uma lógica **porta de saída** o esquema de saída de serviço do toorepresent Olá web esperado.</span><span class="sxs-lookup"><span data-stu-id="f178a-368">Identify a logical **output port** toorepresent hello expected web service output schema.</span></span>

<span data-ttu-id="f178a-369">Quando Olá experimento de pontuação é criado, examiná-la e ajustar conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="f178a-369">When hello scoring experiment is created, review it and adjust as needed.</span></span> <span data-ttu-id="f178a-370">Um ajuste típico é tooreplace Olá dataset de entrada e/ou consulta com uma que exclui os campos de rótulo, como eles não estarão disponíveis quando Olá serviço é chamado.</span><span class="sxs-lookup"><span data-stu-id="f178a-370">A typical adjustment is tooreplace hello input dataset and/or query with one which excludes label fields, as these will not be available when hello service is called.</span></span> <span data-ttu-id="f178a-371">Também é que um tamanho de saudação tooreduce uma boa prática de saudação tooa de consulta e/ou conjunto de dados de entrada suficientes esquema de entrada hello tooindicate de alguns registros.</span><span class="sxs-lookup"><span data-stu-id="f178a-371">It is also a good practice tooreduce hello size of hello input dataset and/or query tooa few records, just enough tooindicate hello input schema.</span></span> <span data-ttu-id="f178a-372">Para a porta de saída de hello, é tooexclude comuns entrados todos os campos e incluir apenas Olá **rótulos de pontuação** e **probabilidades pontuadas** em Olá saída usando Olá [selecionar colunas no conjunto de dados ] [ select-columns] módulo.</span><span class="sxs-lookup"><span data-stu-id="f178a-372">For hello output port, it is common tooexclude all input fields and only include hello **Scored Labels** and **Scored Probabilities** in hello output using hello [Select Columns in Dataset][select-columns] module.</span></span>

<span data-ttu-id="f178a-373">É um exemplo de experiência de pontuação na figura abaixo a saudação.</span><span class="sxs-lookup"><span data-stu-id="f178a-373">A sample scoring experiment is in hello figure below.</span></span> <span data-ttu-id="f178a-374">Quando estiver pronto toodeploy, clique em Olá **publicar WEB SERVICE** botão na barra de ação inferior hello.</span><span class="sxs-lookup"><span data-stu-id="f178a-374">When ready toodeploy, click hello **PUBLISH WEB SERVICE** button in hello lower action bar.</span></span>

![Publicação do Azure Machine Learning][11]

<span data-ttu-id="f178a-376">toorecap, neste tutorial passo a passo, você criou um ambiente de ciência de dados do Azure, trabalhado com um conjunto de dados público entre grande todo caminho de saudação do toomodel de aquisição de dados de treinamento e a implantação de um serviço web de aprendizado de máquina do Azure.</span><span class="sxs-lookup"><span data-stu-id="f178a-376">toorecap, in this walkthrough tutorial, you have created an Azure data science environment, worked with a large public dataset all hello way from data acquisition toomodel training and deploying of an Azure Machine Learning web service.</span></span>

### <a name="license-information"></a><span data-ttu-id="f178a-377">Informações de Licença</span><span class="sxs-lookup"><span data-stu-id="f178a-377">License Information</span></span>
<span data-ttu-id="f178a-378">Este exemplo passo a passo e seu que acompanha scripts e IPython notebook(s) são compartilhados pela Microsoft sob a licença do MIT hello.</span><span class="sxs-lookup"><span data-stu-id="f178a-378">This sample walkthrough and its accompanying scripts and IPython notebook(s) are shared by Microsoft under hello MIT license.</span></span> <span data-ttu-id="f178a-379">Verifique o arquivo de LICENSE.txt de saudação no diretório de saudação do código de exemplo hello no GitHub para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="f178a-379">Please check hello LICENSE.txt file in in hello directory of hello sample code on GitHub for more details.</span></span>

### <a name="references"></a><span data-ttu-id="f178a-380">Referências</span><span class="sxs-lookup"><span data-stu-id="f178a-380">References</span></span>
<span data-ttu-id="f178a-381">•   [Página de download de Viagens de Táxi de NYC, de Andrés Monroy](http://www.andresmh.com/nyctaxitrips/)</span><span class="sxs-lookup"><span data-stu-id="f178a-381">•    [Andrés Monroy NYC Taxi Trips Download Page](http://www.andresmh.com/nyctaxitrips/)</span></span>  
<span data-ttu-id="f178a-382">•   [Dados de Viagem de Táxi de FOILing NYC, de Chris Whong](http://chriswhong.com/open-data/foil_nyc_taxi/) </span><span class="sxs-lookup"><span data-stu-id="f178a-382">•    [FOILing NYC’s Taxi Trip Data by Chris Whong](http://chriswhong.com/open-data/foil_nyc_taxi/) </span></span>  
<span data-ttu-id="f178a-383">•   [Pesquisa e estatísticas de comissionamento de táxis e limusines de NYC](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span><span class="sxs-lookup"><span data-stu-id="f178a-383">•    [NYC Taxi and Limousine Commission Research and Statistics](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span></span>

[1]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_26_1.png
[2]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_28_1.png
[3]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_35_1.png
[4]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_36_1.png
[5]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_39_1.png
[6]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_42_1.png
[7]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_44_1.png
[8]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_46_1.png
[9]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_71_1.png
[10]: ./media/machine-learning-data-science-process-sql-walkthrough/azuremltrain.png
[11]: ./media/machine-learning-data-science-process-sql-walkthrough/azuremlpublish.png
[12]: ./media/machine-learning-data-science-process-sql-walkthrough/ssmsconnect.png
[13]: ./media/machine-learning-data-science-process-sql-walkthrough/executescript.png
[14]: ./media/machine-learning-data-science-process-sql-walkthrough/sqlserverproperties.png
[15]: ./media/machine-learning-data-science-process-sql-walkthrough/sqldefaultdirs.png
[16]: ./media/machine-learning-data-science-process-sql-walkthrough/bulkimport.png
[17]: ./media/machine-learning-data-science-process-sql-walkthrough/amlreader.png
[18]: ./media/machine-learning-data-science-process-sql-walkthrough/amlscoring.png


<!-- Module References -->
[edit-metadata]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
