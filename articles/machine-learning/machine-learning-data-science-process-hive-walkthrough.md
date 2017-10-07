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
# <a name="hello-team-data-science-process-in-action-use-azure-hdinsight-hadoop-clusters"></a><span data-ttu-id="cbff8-103">Olá processo de ciência de dados de equipe em ação: clusters de Hadoop de HDInsight do Azure Use</span><span class="sxs-lookup"><span data-stu-id="cbff8-103">hello Team Data Science Process in action: Use Azure HDInsight Hadoop clusters</span></span>
<span data-ttu-id="cbff8-104">Neste passo a passo, usamos Olá [processo de ciência de dados da equipe (TDSP)](data-science-process-overview.md) em um cenário de ponta a ponta usando um [cluster Azure HDInsight Hadoop](https://azure.microsoft.com/services/hdinsight/) toostore, explorar e apresentam dados de engenharia de saudação publicamente disponível [NYC táxi viagens](http://www.andresmh.com/nyctaxitrips/) dados saudação de exemplo de conjunto de dados e toodown.</span><span class="sxs-lookup"><span data-stu-id="cbff8-104">In this walkthrough, we use hello [Team Data Science Process (TDSP)](data-science-process-overview.md) in an end-to-end scenario using an [Azure HDInsight Hadoop cluster](https://azure.microsoft.com/services/hdinsight/) toostore, explore and feature engineer data from hello publicly available [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) dataset, and toodown sample hello data.</span></span> <span data-ttu-id="cbff8-105">Modelos de dados de saudação são criados com o aprendizado de máquina do Azure toohandle binárias e multiclasse classificação e regressão tarefas de previsão.</span><span class="sxs-lookup"><span data-stu-id="cbff8-105">Models of hello data are built with Azure Machine Learning toohandle binary and multiclass classification and regression predictive tasks.</span></span>

<span data-ttu-id="cbff8-106">Para uma explicação passo a passo que mostra como toohandle um conjunto de dados maior (de 1 terabyte) para um cenário semelhante usando HDInsight Hadoop clusters para processamento de dados, consulte [processo de ciência de dados do Team - usando o Azure HDInsight Hadoop Clusters em um conjunto de dados de 1 TB](machine-learning-data-science-process-hive-criteo-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="cbff8-106">For a walkthrough that shows how toohandle a larger (1 terabyte) dataset for a similar scenario using HDInsight Hadoop clusters for data processing, see [Team Data Science Process - Using Azure HDInsight Hadoop Clusters on a 1 TB dataset](machine-learning-data-science-process-hive-criteo-walkthrough.md).</span></span>

<span data-ttu-id="cbff8-107">Também é possível toouse uma saudação de tooaccomplish de bloco de anotações do IPython tarefas Olá apresentada passo a passo usando o conjunto de dados de 1 TB de saudação.</span><span class="sxs-lookup"><span data-stu-id="cbff8-107">It is also possible toouse an IPython notebook tooaccomplish hello tasks presented hello walkthrough using hello 1 TB dataset.</span></span> <span data-ttu-id="cbff8-108">Os usuários que seriam como tootry essa abordagem deve consultar Olá [Criteo passo a passo usando uma conexão ODBC Hive](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-hive-walkthrough-criteo.ipynb) tópico.</span><span class="sxs-lookup"><span data-stu-id="cbff8-108">Users who would like tootry this approach should consult hello [Criteo walkthrough using a Hive ODBC connection](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-hive-walkthrough-criteo.ipynb) topic.</span></span>

## <span data-ttu-id="cbff8-109"><a name="dataset"></a>Descrição do conjunto de dados Corridas de Táxi em NYC</span><span class="sxs-lookup"><span data-stu-id="cbff8-109"><a name="dataset"></a>NYC Taxi Trips Dataset description</span></span>
<span data-ttu-id="cbff8-110">Olá dados NYC táxi viagem é cerca de 20GB de arquivos compactados valores separados por vírgulas (CSV) (~ 48GB descompactado), que inclui mais de milhões de 173 hello e viagens individuais é pago para cada viagem.</span><span class="sxs-lookup"><span data-stu-id="cbff8-110">hello NYC Taxi Trip data is about 20GB of compressed comma-separated values (CSV) files (~48GB uncompressed), comprising more than 173 million individual trips and hello fares paid for each trip.</span></span> <span data-ttu-id="cbff8-111">Cada registro de viagem inclui Olá retirada e entrega local e a hora, hack anônimos (driver) o número de licença e número medallion (id exclusiva do táxi).</span><span class="sxs-lookup"><span data-stu-id="cbff8-111">Each trip record includes hello pickup and drop-off location and time, anonymized hack (driver's) license number and medallion (taxi’s unique id) number.</span></span> <span data-ttu-id="cbff8-112">dados saudação abrange todas as viagens no ano Olá 2013 e são fornecidos em dois conjuntos de dados a seguir para cada mês de saudação:</span><span class="sxs-lookup"><span data-stu-id="cbff8-112">hello data covers all trips in hello year 2013 and is provided in hello following two datasets for each month:</span></span>

1. <span data-ttu-id="cbff8-113">arquivos CSV 'trip_data' Hello contêm detalhes da visita, como o número de passageiros, coleta e pontos de redução, duração da viagem e comprimento de viagem.</span><span class="sxs-lookup"><span data-stu-id="cbff8-113">hello 'trip_data' CSV files contain trip details, such as number of passengers, pickup and dropoff points, trip duration, and trip length.</span></span> <span data-ttu-id="cbff8-114">Aqui estão alguns exemplos de registros:</span><span class="sxs-lookup"><span data-stu-id="cbff8-114">Here are a few sample records:</span></span>
   
        medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count,trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
2. <span data-ttu-id="cbff8-115">arquivos CSV 'trip_fare' Hello contêm detalhes da tarifa Olá pagado para cada viagem, como tipo de pagamento, quantidade de passagens, sobretaxa e impostos, dicas e pedágio e quantidade total de saudação paga.</span><span class="sxs-lookup"><span data-stu-id="cbff8-115">hello 'trip_fare' CSV files contain details of hello fare paid for each trip, such as payment type, fare amount, surcharge and taxes, tips and tolls, and hello total amount paid.</span></span> <span data-ttu-id="cbff8-116">Aqui estão alguns exemplos de registros:</span><span class="sxs-lookup"><span data-stu-id="cbff8-116">Here are a few sample records:</span></span>
   
        medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

<span data-ttu-id="cbff8-117">viagem de toojoin de chave exclusivo Olá\_dados e viagem\_passagens é composta de campos de saudação: medallion, ataques\_licença e retirada\_datetime.</span><span class="sxs-lookup"><span data-stu-id="cbff8-117">hello unique key toojoin trip\_data and trip\_fare is composed of hello fields: medallion, hack\_licence and pickup\_datetime.</span></span>

<span data-ttu-id="cbff8-118">tooget todos os de viagem específico do hello detalhes tooa relevantes, é suficiente toojoin com três chaves: hello "medallion", "hack\_licença" e "retirada\_datetime".</span><span class="sxs-lookup"><span data-stu-id="cbff8-118">tooget all of hello details relevant tooa particular trip, it is sufficient toojoin with three keys: hello "medallion", "hack\_license" and "pickup\_datetime".</span></span>

<span data-ttu-id="cbff8-119">Descrevemos mais alguns detalhes de dados hello quando podemos armazená-los em tabelas de Hive em breve.</span><span class="sxs-lookup"><span data-stu-id="cbff8-119">We describe some more details of hello data when we store them into Hive tables shortly.</span></span>

## <span data-ttu-id="cbff8-120"><a name="mltasks"></a>Exemplos de tarefas de previsão</span><span class="sxs-lookup"><span data-stu-id="cbff8-120"><a name="mltasks"></a>Examples of prediction tasks</span></span>
<span data-ttu-id="cbff8-121">Quando se aproximando os dados, determinando Olá tipo de previsões que você deseja toomake com base em sua análise ajuda esclarecer tarefas Olá que você precisará tooinclude em seu processo.</span><span class="sxs-lookup"><span data-stu-id="cbff8-121">When approaching data, determining hello kind of predictions you want toomake based on its analysis helps clarify hello tasks that you will need tooinclude in your process.</span></span>
<span data-ttu-id="cbff8-122">Aqui estão os três exemplos de problemas de previsão que abordamos neste passo a passo cuja formulação baseia-se a saudação *dica\_quantidade*:</span><span class="sxs-lookup"><span data-stu-id="cbff8-122">Here are three examples of prediction problems that we address in this walkthrough whose formulation is based on hello *tip\_amount*:</span></span>

1. <span data-ttu-id="cbff8-123">**Classificação binária**: prever ou não se uma gorjeta foi paga por uma corrida, ou seja, um *tip\_amount* maior que US$ 0 é um exemplo positivo, enquanto um *tip\_amount* de US$ 0 é um exemplo negativo.</span><span class="sxs-lookup"><span data-stu-id="cbff8-123">**Binary classification**: Predict whether or not a tip was paid for a trip, i.e. a *tip\_amount* that is greater than $0 is a positive example, while a *tip\_amount* of $0 is a negative example.</span></span>
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0
2. <span data-ttu-id="cbff8-124">**Classificação multiclasse**: intervalo de saudação toopredict de quantidades de dica pago para viagem hello.</span><span class="sxs-lookup"><span data-stu-id="cbff8-124">**Multiclass classification**: toopredict hello range of tip amounts paid for hello trip.</span></span> <span data-ttu-id="cbff8-125">Olá, nós dividimos *dica\_quantidade* em cinco compartimentos ou classes:</span><span class="sxs-lookup"><span data-stu-id="cbff8-125">We divide hello *tip\_amount* into five bins or classes:</span></span>
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0 and tip_amount <= $5
        Class 2 : tip_amount > $5 and tip_amount <= $10
        Class 3 : tip_amount > $10 and tip_amount <= $20
        Class 4 : tip_amount > $20
3. <span data-ttu-id="cbff8-126">**Tarefa de regressão**: o valor de saudação toopredict de dica de saudação pago para uma viagem.</span><span class="sxs-lookup"><span data-stu-id="cbff8-126">**Regression task**: toopredict hello amount of hello tip paid for a trip.</span></span>  

## <span data-ttu-id="cbff8-127"><a name="setup"></a>Configurar um cluster Hadoop do HDInsight para análises avançadas</span><span class="sxs-lookup"><span data-stu-id="cbff8-127"><a name="setup"></a>Set up an HDInsight Hadoop cluster for advanced analytics</span></span>
> [!NOTE]
> <span data-ttu-id="cbff8-128">Essa normalmente é uma tarefa **Admin** .</span><span class="sxs-lookup"><span data-stu-id="cbff8-128">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="cbff8-129">Você pode configurar um ambiente do Azure para análises avançadas que empregue um cluster HDInsight em três etapas:</span><span class="sxs-lookup"><span data-stu-id="cbff8-129">You can set up an Azure environment for advanced analytics that employs an HDInsight cluster in three steps:</span></span>

1. <span data-ttu-id="cbff8-130">[Criar uma conta de armazenamento](../storage/common/storage-create-storage-account.md): essa conta de armazenamento é usada para armazenar dados no Armazenamento de Blob do Azure.</span><span class="sxs-lookup"><span data-stu-id="cbff8-130">[Create a storage account](../storage/common/storage-create-storage-account.md): This storage account is used for storing data in Azure Blob Storage.</span></span> <span data-ttu-id="cbff8-131">dados de saudação usados em clusters de HDInsight também residem aqui.</span><span class="sxs-lookup"><span data-stu-id="cbff8-131">hello data used in HDInsight clusters also resides here.</span></span>
2. <span data-ttu-id="cbff8-132">[Personalizar Hadoop de HDInsight do Azure processo de análise avançada e tecnologia de clusters para Olá](machine-learning-data-science-customize-hadoop-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="cbff8-132">[Customize Azure HDInsight Hadoop clusters for hello Advanced Analytics Process and Technology](machine-learning-data-science-customize-hadoop-cluster.md).</span></span> <span data-ttu-id="cbff8-133">Esta etapa cria um cluster do Hadoop do Azure HDInsight com Anaconda Python 2.7 de 64 bits instalado em todos os nós.</span><span class="sxs-lookup"><span data-stu-id="cbff8-133">This step creates an Azure HDInsight Hadoop cluster with 64-bit Anaconda Python 2.7 installed on all nodes.</span></span> <span data-ttu-id="cbff8-134">Há dois tooremember de etapas importantes ao personalizar o seu cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cbff8-134">There are two important steps tooremember while customizing your HDInsight cluster.</span></span>
   
   * <span data-ttu-id="cbff8-135">Lembre-se a conta de armazenamento Olá toolink criada na etapa 1 com o cluster HDInsight ao criá-la.</span><span class="sxs-lookup"><span data-stu-id="cbff8-135">Remember toolink hello storage account created in step 1 with your HDInsight cluster when creating it.</span></span> <span data-ttu-id="cbff8-136">Esta conta de armazenamento é usado tooaccess dados processados em cluster hello.</span><span class="sxs-lookup"><span data-stu-id="cbff8-136">This storage account is used tooaccess data that is processed within hello cluster.</span></span>
   * <span data-ttu-id="cbff8-137">Após Olá cluster é criado, habilite o nó principal do toohello de acesso remoto de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="cbff8-137">After hello cluster is created, enable Remote Access toohello head node of hello cluster.</span></span> <span data-ttu-id="cbff8-138">Navegue toohello **configuração** guia e clique em **habilitar remoto**.</span><span class="sxs-lookup"><span data-stu-id="cbff8-138">Navigate toohello **Configuration** tab and click **Enable Remote**.</span></span> <span data-ttu-id="cbff8-139">Esta etapa especifica as credenciais do usuário Olá usadas para logon remoto.</span><span class="sxs-lookup"><span data-stu-id="cbff8-139">This step specifies hello user credentials used for remote login.</span></span>
3. <span data-ttu-id="cbff8-140">[Criar um espaço de trabalho do aprendizado de máquina do Azure](machine-learning-create-workspace.md): aprendizado de máquina do Azure este espaço de trabalho é os modelos de aprendizado de máquina toobuild usado.</span><span class="sxs-lookup"><span data-stu-id="cbff8-140">[Create an Azure Machine Learning workspace](machine-learning-create-workspace.md): This Azure Machine Learning workspace is used toobuild machine learning models.</span></span> <span data-ttu-id="cbff8-141">Essa tarefa é abordada depois de concluir uma exploração de dados inicial e para baixo usando o cluster do HDInsight de saudação de amostragem.</span><span class="sxs-lookup"><span data-stu-id="cbff8-141">This task is addressed after completing an initial data exploration and down sampling using hello HDInsight cluster.</span></span>

## <span data-ttu-id="cbff8-142"><a name="getdata"></a>Obter dados de saudação de uma fonte de pública</span><span class="sxs-lookup"><span data-stu-id="cbff8-142"><a name="getdata"></a>Get hello data from a public source</span></span>
> [!NOTE]
> <span data-ttu-id="cbff8-143">Essa normalmente é uma tarefa **Admin** .</span><span class="sxs-lookup"><span data-stu-id="cbff8-143">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="cbff8-144">Olá tooget [NYC táxi viagens](http://www.andresmh.com/nyctaxitrips/) conjunto de dados de seu local público, você pode usar qualquer um dos métodos de saudação descritos em [tooand de mover dados do armazenamento de BLOBs do Azure](machine-learning-data-science-move-azure-blob.md) máquina de tooyour toocopy Olá dados.</span><span class="sxs-lookup"><span data-stu-id="cbff8-144">tooget hello [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) dataset from its public location, you may use any of hello methods described in [Move Data tooand from Azure Blob Storage](machine-learning-data-science-move-azure-blob.md) toocopy hello data tooyour machine.</span></span>

<span data-ttu-id="cbff8-145">Aqui descrevemos como usar AzCopy tootransfer Olá arquivos que contém dados.</span><span class="sxs-lookup"><span data-stu-id="cbff8-145">Here we describe how use AzCopy tootransfer hello files containing data.</span></span> <span data-ttu-id="cbff8-146">toodownload e instale o AzCopy siga as instruções de saudação em [guia de Introdução com hello o utilitário de linha de comando AzCopy](../storage/common/storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="cbff8-146">toodownload and install AzCopy follow hello instructions at [Getting Started with hello AzCopy Command-Line Utility](../storage/common/storage-use-azcopy.md).</span></span>

1. <span data-ttu-id="cbff8-147">Em uma janela de Prompt de comando, execute Olá AzCopy comandos a seguir, substituindo *< path_to_data_folder >* com destino desejado hello:</span><span class="sxs-lookup"><span data-stu-id="cbff8-147">From a Command Prompt window, issue hello following AzCopy commands, replacing *<path_to_data_folder>* with hello desired destination:</span></span>

        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:https://nyctaxitrips.blob.core.windows.net/data /Dest:<path_to_data_folder> /S

1. <span data-ttu-id="cbff8-148">Quando Olá cópia é concluída, um total de 24 arquivos compactados estão na pasta de dados de saudação escolhida.</span><span class="sxs-lookup"><span data-stu-id="cbff8-148">When hello copy completes, a total of 24 zipped files are in hello data folder chosen.</span></span> <span data-ttu-id="cbff8-149">Descompacte Olá baixado arquivos toohello mesmo diretório em seu computador local.</span><span class="sxs-lookup"><span data-stu-id="cbff8-149">Unzip hello downloaded files toohello same directory on your local machine.</span></span> <span data-ttu-id="cbff8-150">Tome nota da pasta Olá onde residem os arquivos de saudação descompactado.</span><span class="sxs-lookup"><span data-stu-id="cbff8-150">Make a note of hello folder where hello uncompressed files reside.</span></span> <span data-ttu-id="cbff8-151">Esta pasta será chamado tooas Olá *< caminho\_para\_unzipped_data\_arquivos\>*  é o que se segue.</span><span class="sxs-lookup"><span data-stu-id="cbff8-151">This folder will be referred tooas hello *<path\_to\_unzipped_data\_files\>* is what follows.</span></span>

## <span data-ttu-id="cbff8-152"><a name="upload"></a>Carregar o contêiner do hello dados toohello padrão do cluster de Hadoop de HDInsight do Azure</span><span class="sxs-lookup"><span data-stu-id="cbff8-152"><a name="upload"></a>Upload hello data toohello default container of Azure HDInsight Hadoop cluster</span></span>
> [!NOTE]
> <span data-ttu-id="cbff8-153">Essa normalmente é uma tarefa **Admin** .</span><span class="sxs-lookup"><span data-stu-id="cbff8-153">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="cbff8-154">No hello seguintes comandos do AzCopy, substitua Olá seguir parâmetros com valores reais de saudação que você especificou ao criar o cluster de Hadoop hello e extrair arquivos de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="cbff8-154">In hello following AzCopy commands, replace hello following parameters with hello actual values that you specified when creating hello Hadoop cluster and unzipping hello data files.</span></span>

* <span data-ttu-id="cbff8-155">***&#60; path_to_data_folder >*** diretório hello (juntamente com o caminho) no computador que contêm arquivos de dados Olá descompactado</span><span class="sxs-lookup"><span data-stu-id="cbff8-155">***&#60;path_to_data_folder>*** hello directory (along with path) on your machine that contain hello unzipped data files</span></span>  
* <span data-ttu-id="cbff8-156">***&#60; o nome da conta de armazenamento de cluster Hadoop >*** Olá conta de armazenamento associada ao cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="cbff8-156">***&#60;storage account name of Hadoop cluster>*** hello storage account associated with your HDInsight cluster</span></span>
* <span data-ttu-id="cbff8-157">***&#60; o contêiner padrão do cluster Hadoop >*** contêiner do saudação padrão usado pelo cluster.</span><span class="sxs-lookup"><span data-stu-id="cbff8-157">***&#60;default container of Hadoop cluster>*** hello default container used by your cluster.</span></span> <span data-ttu-id="cbff8-158">Anote esse nome de saudação do padrão de saudação contêiner é geralmente o hello mesmo nome como o próprio cluster Olá.</span><span class="sxs-lookup"><span data-stu-id="cbff8-158">Note that hello name of hello default container is usually hello same name as hello cluster itself.</span></span> <span data-ttu-id="cbff8-159">Por exemplo, se o cluster de saudação é chamado "abc123.azurehdinsight.net", o contêiner de padrão de saudação é abc123.</span><span class="sxs-lookup"><span data-stu-id="cbff8-159">For example, if hello cluster is called "abc123.azurehdinsight.net", hello default container is abc123.</span></span>
* <span data-ttu-id="cbff8-160">***&#60; chave de conta de armazenamento >*** Olá chave Olá conta de armazenamento usada por seu cluster</span><span class="sxs-lookup"><span data-stu-id="cbff8-160">***&#60;storage account key>*** hello key for hello storage account used by your cluster</span></span>

<span data-ttu-id="cbff8-161">Em um Prompt de comando ou uma janela do Windows PowerShell em seu computador, execute Olá AzCopy os dois comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="cbff8-161">From a Command Prompt or a Windows PowerShell window in your machine, run hello following two AzCopy commands.</span></span>

<span data-ttu-id="cbff8-162">Esse comando carrega os dados de viagem de saudação muito***nyctaxitripraw*** diretório no contêiner de padrão de saudação do cluster de Hadoop hello.</span><span class="sxs-lookup"><span data-stu-id="cbff8-162">This command uploads hello trip data too***nyctaxitripraw*** directory in hello default container of hello Hadoop cluster.</span></span>

        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:<path_to_unzipped_data_files> /Dest:https://<storage account name of Hadoop cluster>.blob.core.windows.net/<default container of Hadoop cluster>/nyctaxitripraw /DestKey:<storage account key> /S /Pattern:trip_data_*.csv

<span data-ttu-id="cbff8-163">Esse comando carrega os dados de passagens de saudação muito***nyctaxifareraw*** diretório no contêiner de padrão de saudação do cluster de Hadoop hello.</span><span class="sxs-lookup"><span data-stu-id="cbff8-163">This command uploads hello fare data too***nyctaxifareraw*** directory in hello default container of hello Hadoop cluster.</span></span>

        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:<path_to_unzipped_data_files> /Dest:https://<storage account name of Hadoop cluster>.blob.core.windows.net/<default container of Hadoop cluster>/nyctaxifareraw /DestKey:<storage account key> /S /Pattern:trip_fare_*.csv

<span data-ttu-id="cbff8-164">dados de saudação devem agora no armazenamento de BLOBs do Azure e pronto toobe consumidas em cluster do HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="cbff8-164">hello data should now in Azure Blob Storage and ready toobe consumed within hello HDInsight cluster.</span></span>

## <span data-ttu-id="cbff8-165"><a name="#download-hql-files"></a>Faça logon no nó principal de saudação do cluster de Hadoop e e preparar para análise de dados exploratório</span><span class="sxs-lookup"><span data-stu-id="cbff8-165"><a name="#download-hql-files"></a>Log into hello head node of Hadoop cluster and and prepare for exploratory data analysis</span></span>
> [!NOTE]
> <span data-ttu-id="cbff8-166">Essa normalmente é uma tarefa **Admin** .</span><span class="sxs-lookup"><span data-stu-id="cbff8-166">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="cbff8-167">nó principal do hello tooaccess de cluster Olá para análise de dados exploratório e para baixo de amostragem de dados hello, execute o procedimento de saudação descrito no [Olá acesso cabeçotes de nó de Cluster de Hadoop](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span><span class="sxs-lookup"><span data-stu-id="cbff8-167">tooaccess hello head node of hello cluster for exploratory data analysis and down sampling of hello data, follow hello procedure outlined in [Access hello Head Node of Hadoop Cluster](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span></span>

<span data-ttu-id="cbff8-168">Este passo a passo, principalmente, usamos as consultas escritas [Hive](https://hive.apache.org/), uma linguagem de consulta do tipo SQL, tooperform explorações de dados preliminares.</span><span class="sxs-lookup"><span data-stu-id="cbff8-168">In this walkthrough, we primarily use queries written in [Hive](https://hive.apache.org/), a SQL-like query language, tooperform preliminary data explorations.</span></span> <span data-ttu-id="cbff8-169">consultas de Hive Olá são armazenadas em arquivos de .hql.</span><span class="sxs-lookup"><span data-stu-id="cbff8-169">hello Hive queries are stored in .hql files.</span></span> <span data-ttu-id="cbff8-170">É, em seguida, para baixo de exemplo neste toobe dados usado dentro de aprendizado de máquina do Azure para criar modelos.</span><span class="sxs-lookup"><span data-stu-id="cbff8-170">We then down sample this data toobe used within Azure Machine Learning for building models.</span></span>

<span data-ttu-id="cbff8-171">cluster de saudação tooprepare para análise de dados exploratório, podemos baixar os arquivos de .hql Olá que contêm scripts de Hive relevantes saudação do [github](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts) tooa diretório local (C:\temp) no nó principal hello.</span><span class="sxs-lookup"><span data-stu-id="cbff8-171">tooprepare hello cluster for exploratory data analysis, we download hello .hql files containing hello relevant Hive scripts from [github](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts) tooa local directory (C:\temp) on hello head node.</span></span> <span data-ttu-id="cbff8-172">toodo isso, abra Olá **Prompt de comando** do hello nó principal do Olá Olá cluster e emitir os dois comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="cbff8-172">toodo this, open hello **Command Prompt** from within hello head node of hello cluster and issue hello following two commands:</span></span>

    set script='https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/DataScienceProcess/DataScienceScripts/Download_DataScience_Scripts.ps1'

    @powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString(%script%))"

<span data-ttu-id="cbff8-173">Esses dois comandos baixará todos os arquivos de .hql necessários neste diretório local do passo a passo toohello ***C:\temp &#92;*** no nó principal hello.</span><span class="sxs-lookup"><span data-stu-id="cbff8-173">These two commands will download all .hql files needed in this walkthrough toohello local directory ***C:\temp&#92;*** in hello head node.</span></span>

## <span data-ttu-id="cbff8-174"><a name="#hive-db-tables"></a>Criar banco de dados e tabelas Hive particionadas por mês</span><span class="sxs-lookup"><span data-stu-id="cbff8-174"><a name="#hive-db-tables"></a>Create Hive database and tables partitioned by month</span></span>
> [!NOTE]
> <span data-ttu-id="cbff8-175">Essa normalmente é uma tarefa **Admin** .</span><span class="sxs-lookup"><span data-stu-id="cbff8-175">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="cbff8-176">Estamos agora pronto toocreate Hive tabelas para nosso conjunto de dados NYC táxi.</span><span class="sxs-lookup"><span data-stu-id="cbff8-176">We are now ready toocreate Hive tables for our NYC taxi dataset.</span></span>
<span data-ttu-id="cbff8-177">No hello nó principal do cluster de Hadoop Olá abra Olá ***linha de comando do Hadoop*** na Olá a área de trabalho do nó principal hello e insira o diretório de Hive Olá digitando o comando Olá</span><span class="sxs-lookup"><span data-stu-id="cbff8-177">In hello head node of hello Hadoop cluster, open hello ***Hadoop Command Line*** on hello desktop of hello head node, and enter hello Hive directory by entering hello command</span></span>

    cd %hive_home%\bin

> [!NOTE]
> <span data-ttu-id="cbff8-178">**Executar todos os comandos de Hive neste passo a passo de saudação acima Hive bin / prompt do diretório. Isso solucionará automaticamente quaisquer problemas de caminho. Usamos termos Olá "Hive diretório" prompt, "Hive bin / aviso diretório" e "linha de comando Hadoop" alternadamente neste passo a passo.**</span><span class="sxs-lookup"><span data-stu-id="cbff8-178">**Run all Hive commands in this walkthrough from hello above Hive bin/ directory prompt. This will take care of any path issues automatically. We use hello terms "Hive directory prompt", "Hive bin/ directory prompt",  and "Hadoop Command Line" interchangeably in this walkthrough.**</span></span>
> 
> 

<span data-ttu-id="cbff8-179">Do prompt de diretório do Hive Olá, digite Olá comando no Hadoop linha de comando de tabelas e Olá nó principal toosubmit Olá Hive consulta toocreate Hive banco de dados a seguir:</span><span class="sxs-lookup"><span data-stu-id="cbff8-179">From hello Hive directory prompt, enter hello following command in Hadoop Command Line of hello head node toosubmit hello Hive query toocreate Hive database and tables:</span></span>

    hive -f "C:\temp\sample_hive_create_db_and_tables.hql"

<span data-ttu-id="cbff8-180">Aqui está o conteúdo de saudação do hello ***C:\temp\sample\_hive\_criar\_db\_e\_tables.hql*** arquivo que cria o banco de dados de Hive ***nyctaxidb *** e tabelas ***viagem*** e ***passagens***.</span><span class="sxs-lookup"><span data-stu-id="cbff8-180">Here is hello content of hello ***C:\temp\sample\_hive\_create\_db\_and\_tables.hql*** file which creates Hive database ***nyctaxidb*** and tables ***trip*** and ***fare***.</span></span>

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

<span data-ttu-id="cbff8-181">Esse script do Hive cria duas tabelas:</span><span class="sxs-lookup"><span data-stu-id="cbff8-181">This Hive script creates two tables:</span></span>

* <span data-ttu-id="cbff8-182">tabela de "viagem e" Hello contém detalhes de viagem de cada jornada (detalhes do driver, o tempo de retirada, distância de viagem e vezes)</span><span class="sxs-lookup"><span data-stu-id="cbff8-182">hello "trip" table contains trip details of each ride (driver details, pickup time, trip distance and times)</span></span>
* <span data-ttu-id="cbff8-183">tabela de "passagens" Hello contém detalhes de passagens (valor de passagens, quantidade de ponta, pedágio e sobretaxas).</span><span class="sxs-lookup"><span data-stu-id="cbff8-183">hello "fare" table contains fare details (fare amount, tip amount, tolls and surcharges).</span></span>

<span data-ttu-id="cbff8-184">Se você precisa de qualquer assistência adicional com esses procedimentos ou tooinvestigate as alternativas, consulte a seção de saudação [consultas Hive enviar diretamente da linha de comando do Hadoop Olá ](machine-learning-data-science-move-hive-tables.md#submit).</span><span class="sxs-lookup"><span data-stu-id="cbff8-184">If you need any additional assistance with these procedures or want tooinvestigate alternative ones, see hello section [Submit Hive queries directly from hello Hadoop Command Line ](machine-learning-data-science-move-hive-tables.md#submit).</span></span>

## <span data-ttu-id="cbff8-185"><a name="#load-data"></a>Carregar tabelas de dados de tooHive por partições</span><span class="sxs-lookup"><span data-stu-id="cbff8-185"><a name="#load-data"></a>Load Data tooHive tables by partitions</span></span>
> [!NOTE]
> <span data-ttu-id="cbff8-186">Essa normalmente é uma tarefa **Admin** .</span><span class="sxs-lookup"><span data-stu-id="cbff8-186">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="cbff8-187">Olá NYC táxi dataset tem um particionamento natural por mês, que usamos tooenable tempos mais rápidos de processamento e consulta.</span><span class="sxs-lookup"><span data-stu-id="cbff8-187">hello NYC taxi dataset has a natural partitioning by month, which we use tooenable faster processing and query times.</span></span> <span data-ttu-id="cbff8-188">Olá comandos do PowerShell abaixo (emitidas do diretório de Hive hello usando Olá **linha de comando do Hadoop**) carregar dados toohello "viagem" e "passagens" Hive tabelas particionadas por mês.</span><span class="sxs-lookup"><span data-stu-id="cbff8-188">hello PowerShell commands below (issued from hello Hive directory using hello **Hadoop Command Line**) load data toohello "trip" and "fare" Hive tables partitioned by month.</span></span>

    for /L %i IN (1,1,12) DO (hive -hiveconf MONTH=%i -f "C:\temp\sample_hive_load_data_by_partitions.hql")

<span data-ttu-id="cbff8-189">Olá *exemplo\_hive\_carregar\_dados\_por\_partitions.hql* arquivo contém o seguinte Olá **carregar** comandos.</span><span class="sxs-lookup"><span data-stu-id="cbff8-189">hello *sample\_hive\_load\_data\_by\_partitions.hql* file contains hello following **LOAD** commands.</span></span>

    LOAD DATA INPATH 'wasb:///nyctaxitripraw/trip_data_${hiveconf:MONTH}.csv' INTO TABLE nyctaxidb.trip PARTITION (month=${hiveconf:MONTH});
    LOAD DATA INPATH 'wasb:///nyctaxifareraw/trip_fare_${hiveconf:MONTH}.csv' INTO TABLE nyctaxidb.fare PARTITION (month=${hiveconf:MONTH});

<span data-ttu-id="cbff8-190">Observe que um número de consultas de Hive que usamos aqui no processo de exploração Olá envolve a pesquisa em uma única partição ou em apenas algumas das partições.</span><span class="sxs-lookup"><span data-stu-id="cbff8-190">Note that a number of Hive queries we use here in hello exploration process involve looking at just a single partition or at only a couple of partitions.</span></span> <span data-ttu-id="cbff8-191">Mas essas consultas podem ser executadas em dados de inteiro de saudação.</span><span class="sxs-lookup"><span data-stu-id="cbff8-191">But these queries could be run across hello entire data.</span></span>

### <span data-ttu-id="cbff8-192"><a name="#show-db"></a>Mostrar os bancos de dados em Olá cluster HDInsight Hadoop</span><span class="sxs-lookup"><span data-stu-id="cbff8-192"><a name="#show-db"></a>Show databases in hello HDInsight Hadoop cluster</span></span>
<span data-ttu-id="cbff8-193">tooshow Olá bancos de dados criados no cluster HDInsight Hadoop dentro da janela de linha de comando do Hadoop hello, executar Olá na linha de comando do Hadoop de comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="cbff8-193">tooshow hello databases created in HDInsight Hadoop cluster inside hello Hadoop Command Line window, run hello following command in Hadoop Command Line:</span></span>

    hive -e "show databases;"

### <span data-ttu-id="cbff8-194"><a name="#show-tables"></a>Mostrar tabelas de Hive Olá no banco de dados de nyctaxidb Olá</span><span class="sxs-lookup"><span data-stu-id="cbff8-194"><a name="#show-tables"></a>Show hello Hive tables in hello nyctaxidb database</span></span>
<span data-ttu-id="cbff8-195">tooshow Olá tabelas Olá nyctaxidb banco de dados, executar Olá na linha de comando do Hadoop de comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="cbff8-195">tooshow hello tables in hello nyctaxidb database, run hello following command in Hadoop Command Line:</span></span>

    hive -e "show tables in nyctaxidb;"

<span data-ttu-id="cbff8-196">Podemos afirmar que as tabelas de saudação são particionadas emitindo o comando de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="cbff8-196">We can confirm that hello tables are partitioned by issuing hello command below:</span></span>

    hive -e "show partitions nyctaxidb.trip;"

<span data-ttu-id="cbff8-197">Olá esperado saída é mostrada abaixo:</span><span class="sxs-lookup"><span data-stu-id="cbff8-197">hello expected output is shown below:</span></span>

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

<span data-ttu-id="cbff8-198">Da mesma forma, podemos garantir que essa tabela de passagens Olá é particionada emitindo o comando de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="cbff8-198">Similarly, we can ensure that hello fare table is partitioned by issuing hello command below:</span></span>

    hive -e "show partitions nyctaxidb.fare;"

<span data-ttu-id="cbff8-199">Olá esperado saída é mostrada abaixo:</span><span class="sxs-lookup"><span data-stu-id="cbff8-199">hello expected output is shown below:</span></span>

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

## <span data-ttu-id="cbff8-200"><a name="#explore-hive"></a>Exploração de dados e engenharia de recursos no Hive</span><span class="sxs-lookup"><span data-stu-id="cbff8-200"><a name="#explore-hive"></a>Data exploration and feature engineering in Hive</span></span>
> [!NOTE]
> <span data-ttu-id="cbff8-201">Essa é normalmente é uma tarefa de **Cientista de Dados** .</span><span class="sxs-lookup"><span data-stu-id="cbff8-201">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="cbff8-202">Olá exploração de dados e tarefas de engenharia para Olá dados carregados em tabelas de Hive Olá podem ser realizados usando consultas de Hive de recursos.</span><span class="sxs-lookup"><span data-stu-id="cbff8-202">hello data exploration and feature engineering tasks for hello data loaded into hello Hive tables can be accomplished using Hive queries.</span></span> <span data-ttu-id="cbff8-203">Aqui estão exemplos de tais tarefas que percorreremos ao longo desta seção:</span><span class="sxs-lookup"><span data-stu-id="cbff8-203">Here are examples of such tasks that we walk you through in this section:</span></span>

* <span data-ttu-id="cbff8-204">Exiba os principais 10 registros Olá em ambas as tabelas.</span><span class="sxs-lookup"><span data-stu-id="cbff8-204">View hello top 10 records in both tables.</span></span>
* <span data-ttu-id="cbff8-205">Explorar as distribuições de dados de alguns campos em períodos diferentes.</span><span class="sxs-lookup"><span data-stu-id="cbff8-205">Explore data distributions of a few fields in varying time windows.</span></span>
* <span data-ttu-id="cbff8-206">Investigue a qualidade dos dados dos campos de longitude e latitude hello.</span><span class="sxs-lookup"><span data-stu-id="cbff8-206">Investigate data quality of hello longitude and latitude fields.</span></span>
* <span data-ttu-id="cbff8-207">Gerar rótulos de classificação binária e multiclasse com base no hello **dica\_quantidade**.</span><span class="sxs-lookup"><span data-stu-id="cbff8-207">Generate binary and multiclass classification labels based on hello **tip\_amount**.</span></span>
* <span data-ttu-id="cbff8-208">Gere recursos de computação distâncias de viagem direto de saudação.</span><span class="sxs-lookup"><span data-stu-id="cbff8-208">Generate features by computing hello direct trip distances.</span></span>

### <a name="exploration-view-hello-top-10-records-in-table-trip"></a><span data-ttu-id="cbff8-209">Exploração: Exibição Olá top 10 registros em viagem de tabela</span><span class="sxs-lookup"><span data-stu-id="cbff8-209">Exploration: View hello top 10 records in table trip</span></span>
> [!NOTE]
> <span data-ttu-id="cbff8-210">Essa é normalmente é uma tarefa de **Cientista de Dados** .</span><span class="sxs-lookup"><span data-stu-id="cbff8-210">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="cbff8-211">toosee a aparência dos dados hello, podemos examinar 10 registros de cada tabela.</span><span class="sxs-lookup"><span data-stu-id="cbff8-211">toosee what hello data looks like, we examine 10 records from each table.</span></span> <span data-ttu-id="cbff8-212">Execute Olá duas consultas a seguir separadamente de aviso de diretório de Hive Olá nos registros de Olá Olá linha de comando do Hadoop console tooinspect.</span><span class="sxs-lookup"><span data-stu-id="cbff8-212">Run hello following two queries separately from hello Hive directory prompt in hello Hadoop Command Line console tooinspect hello records.</span></span>

<span data-ttu-id="cbff8-213">tooget Olá top 10 registros na tabela hello "viagem" da saudação primeiro mês:</span><span class="sxs-lookup"><span data-stu-id="cbff8-213">tooget hello top 10 records in hello table "trip" from hello first month:</span></span>

    hive -e "select * from nyctaxidb.trip where month=1 limit 10;"

<span data-ttu-id="cbff8-214">tooget Olá top 10 registros na tabela hello "passagens" da saudação primeiro mês:</span><span class="sxs-lookup"><span data-stu-id="cbff8-214">tooget hello top 10 records in hello table "fare" from hello first month:</span></span>

    hive -e "select * from nyctaxidb.fare where month=1 limit 10;"

<span data-ttu-id="cbff8-215">Ele geralmente é útil toosave Olá registros tooa arquivo exibindo conveniente.</span><span class="sxs-lookup"><span data-stu-id="cbff8-215">It is often useful toosave hello records tooa file for convenient viewing.</span></span> <span data-ttu-id="cbff8-216">Toohello uma pequena alteração acima consulta realiza isso:</span><span class="sxs-lookup"><span data-stu-id="cbff8-216">A small change toohello above query accomplishes this:</span></span>

    hive -e "select * from nyctaxidb.fare where month=1 limit 10;" > C:\temp\testoutput

### <a name="exploration-view-hello-number-of-records-in-each-of-hello-12-partitions"></a><span data-ttu-id="cbff8-217">Exploração: Exibir hello número de registros em cada um dos 12 partições de saudação</span><span class="sxs-lookup"><span data-stu-id="cbff8-217">Exploration: View hello number of records in each of hello 12 partitions</span></span>
> [!NOTE]
> <span data-ttu-id="cbff8-218">Essa é normalmente é uma tarefa de **Cientista de Dados** .</span><span class="sxs-lookup"><span data-stu-id="cbff8-218">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="cbff8-219">De interesse é hello como número de saudação de viagens de varia durante o ano civil de saudação.</span><span class="sxs-lookup"><span data-stu-id="cbff8-219">Of interest is hello how hello number of trips varies during hello calendar year.</span></span> <span data-ttu-id="cbff8-220">Agrupar por mês nos permite toosee nesta distribuição de viagens de aparência.</span><span class="sxs-lookup"><span data-stu-id="cbff8-220">Grouping by month allows us toosee what this distribution of trips looks like.</span></span>

    hive -e "select month, count(*) from nyctaxidb.trip group by month;"

<span data-ttu-id="cbff8-221">Isso nos dá saída hello:</span><span class="sxs-lookup"><span data-stu-id="cbff8-221">This gives us hello output :</span></span>

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

<span data-ttu-id="cbff8-222">Aqui, Olá primeira coluna é mês hello e Olá segundo é o número de saudação de viagens de naquele mês.</span><span class="sxs-lookup"><span data-stu-id="cbff8-222">Here, hello first column is hello month and hello second is hello number of trips for that month.</span></span>

<span data-ttu-id="cbff8-223">Podemos também pode contar número total de saudação de registros no nosso conjunto de dados de viagem emitindo Olá comando no prompt de diretório de Hive Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="cbff8-223">We can also count hello total number of records in our trip data set by issuing hello following command at hello Hive directory prompt.</span></span>

    hive -e "select count(*) from nyctaxidb.trip;"

<span data-ttu-id="cbff8-224">Isso resulta em:</span><span class="sxs-lookup"><span data-stu-id="cbff8-224">This yields:</span></span>

    173179759
    Time taken: 284.017 seconds, Fetched: 1 row(s)

<span data-ttu-id="cbff8-225">Usando comandos toothose semelhante mostrado para o conjunto de dados de viagem hello, podemos emitir consultas de Hive Olá Hive diretório no prompt de saudação passagens conjunto de dados toovalidate Olá quantos registros.</span><span class="sxs-lookup"><span data-stu-id="cbff8-225">Using commands similar toothose shown for hello trip data set, we can issue Hive queries from hello Hive directory prompt for hello fare data set toovalidate hello number of records.</span></span>

    hive -e "select month, count(*) from nyctaxidb.fare group by month;"

<span data-ttu-id="cbff8-226">Isso nos dá saída hello:</span><span class="sxs-lookup"><span data-stu-id="cbff8-226">This gives us hello output:</span></span>

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

<span data-ttu-id="cbff8-227">Observe que Olá exata mesmo número de viagens por mês é retornado para os dois conjuntos de dados.</span><span class="sxs-lookup"><span data-stu-id="cbff8-227">Note that hello exact same number of trips per month is returned for both data sets.</span></span> <span data-ttu-id="cbff8-228">Isso fornece validação primeiro Olá que Olá dados foram carregados corretamente.</span><span class="sxs-lookup"><span data-stu-id="cbff8-228">This provides hello first validation that hello data has been loaded correctly.</span></span>

<span data-ttu-id="cbff8-229">Contando Olá o número total de registros no conjunto de dados de passagens Olá pode ser feito usando o comando Olá abaixo no prompt de diretório de Hive hello:</span><span class="sxs-lookup"><span data-stu-id="cbff8-229">Counting hello total number of records in hello fare data set can be done using hello command below from hello Hive directory prompt:</span></span>

    hive -e "select count(*) from nyctaxidb.fare;"

<span data-ttu-id="cbff8-230">Isso resulta em:</span><span class="sxs-lookup"><span data-stu-id="cbff8-230">This yields :</span></span>

    173179759
    Time taken: 186.683 seconds, Fetched: 1 row(s)

<span data-ttu-id="cbff8-231">é o número total de saudação de registros em ambas as tabelas também Olá mesmo.</span><span class="sxs-lookup"><span data-stu-id="cbff8-231">hello total number of records in both tables is also hello same.</span></span> <span data-ttu-id="cbff8-232">Isso fornece uma validação segundo esse Olá dados foram carregados corretamente.</span><span class="sxs-lookup"><span data-stu-id="cbff8-232">This provides a second validation that hello data has been loaded correctly.</span></span>

### <a name="exploration-trip-distribution-by-medallion"></a><span data-ttu-id="cbff8-233">Exploração: distribuição de corridas por licença</span><span class="sxs-lookup"><span data-stu-id="cbff8-233">Exploration: Trip distribution by medallion</span></span>
> [!NOTE]
> <span data-ttu-id="cbff8-234">Essa é normalmente é uma tarefa de **Cientista de Dados** .</span><span class="sxs-lookup"><span data-stu-id="cbff8-234">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="cbff8-235">Este exemplo identifica medallion hello (números de táxi) com mais de 100 viagens dentro de um determinado período de tempo.</span><span class="sxs-lookup"><span data-stu-id="cbff8-235">This example identifies hello medallion (taxi numbers) with more than 100 trips within a given time period.</span></span> <span data-ttu-id="cbff8-236">benefícios de consulta de saudação do hello particionada acesso à tabela porque ela está condicionada pela variável de partição Olá **mês**.</span><span class="sxs-lookup"><span data-stu-id="cbff8-236">hello query benefits from hello partitioned table access since it is conditioned by hello partition variable **month**.</span></span> <span data-ttu-id="cbff8-237">resultados da consulta Olá são escritos tooa arquivo local queryoutput.tsv em `C:\temp` no nó de cabeçalho hello.</span><span class="sxs-lookup"><span data-stu-id="cbff8-237">hello query results are written tooa local file queryoutput.tsv in `C:\temp` on hello head node.</span></span>

    hive -f "C:\temp\sample_hive_trip_count_by_medallion.hql" > C:\temp\queryoutput.tsv

<span data-ttu-id="cbff8-238">Aqui está o conteúdo de saudação do *exemplo\_hive\_viagem\_contagem\_por\_medallion.hql* arquivo para inspeção.</span><span class="sxs-lookup"><span data-stu-id="cbff8-238">Here is hello content of *sample\_hive\_trip\_count\_by\_medallion.hql* file for inspection.</span></span>

    SELECT medallion, COUNT(*) as med_count
    FROM nyctaxidb.fare
    WHERE month<=3
    GROUP BY medallion
    HAVING med_count > 100
    ORDER BY med_count desc;

<span data-ttu-id="cbff8-239">medallion Olá Olá NYC táxi conjunto de dados identifica um arquivo. cab exclusivo.</span><span class="sxs-lookup"><span data-stu-id="cbff8-239">hello medallion in hello NYC taxi data set identifies a unique cab.</span></span> <span data-ttu-id="cbff8-240">Podemos identificar quais táxis estão "ocupados" perguntando quais fizeram mais do que um determinado número de corridas em um determinado período de tempo.</span><span class="sxs-lookup"><span data-stu-id="cbff8-240">We can identify which cabs are "busy" by asking which ones made more than a certain number of trips in a particular time period.</span></span> <span data-ttu-id="cbff8-241">Olá, exemplo a seguir identifica cabs que fez com que mais de cem viagens Olá seja três primeiros meses e salva Olá consulta resultados tooa arquivo local C:\temp\queryoutput.tsv.</span><span class="sxs-lookup"><span data-stu-id="cbff8-241">hello following example identifies cabs that made more than a hundred trips in hello first three months, and saves hello query results tooa local file, C:\temp\queryoutput.tsv.</span></span>

<span data-ttu-id="cbff8-242">Aqui está o conteúdo de saudação do *exemplo\_hive\_viagem\_contagem\_por\_medallion.hql* arquivo para inspeção.</span><span class="sxs-lookup"><span data-stu-id="cbff8-242">Here is hello content of *sample\_hive\_trip\_count\_by\_medallion.hql* file for inspection.</span></span>

    SELECT medallion, COUNT(*) as med_count
    FROM nyctaxidb.fare
    WHERE month<=3
    GROUP BY medallion
    HAVING med_count > 100
    ORDER BY med_count desc;

<span data-ttu-id="cbff8-243">De saudação Hive aviso de diretório, comando de saudação do problema abaixo:</span><span class="sxs-lookup"><span data-stu-id="cbff8-243">From hello Hive directory prompt, issue hello command below :</span></span>

    hive -f "C:\temp\sample_hive_trip_count_by_medallion.hql" > C:\temp\queryoutput.tsv

### <a name="exploration-trip-distribution-by-medallion-and-hacklicense"></a><span data-ttu-id="cbff8-244">Exploração: distribuição de corridas por medallion e hack_license</span><span class="sxs-lookup"><span data-stu-id="cbff8-244">Exploration: Trip distribution by medallion and hack_license</span></span>
> [!NOTE]
> <span data-ttu-id="cbff8-245">Essa é normalmente é uma tarefa de **Cientista de Dados** .</span><span class="sxs-lookup"><span data-stu-id="cbff8-245">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="cbff8-246">Ao explorar um conjunto de dados, com frequência, desejamos que número de saudação do tooexamine de co-ocorrências de grupos de valores.</span><span class="sxs-lookup"><span data-stu-id="cbff8-246">When exploring a dataset, we frequently want tooexamine hello number of co-occurences of groups of values.</span></span> <span data-ttu-id="cbff8-247">Esta seção fornece um exemplo de como toodo isso para cabs e drivers.</span><span class="sxs-lookup"><span data-stu-id="cbff8-247">This section provide an example of how toodo this for cabs and drivers.</span></span>

<span data-ttu-id="cbff8-248">Olá *exemplo\_hive\_viagem\_contagem\_por\_medallion\_license.hql* arquivo agrupa os dados de passagens de saudação em "medallion" e "hack_license" e retorna contagens de cada combinação.</span><span class="sxs-lookup"><span data-stu-id="cbff8-248">hello *sample\_hive\_trip\_count\_by\_medallion\_license.hql* file groups hello fare data set on "medallion" and "hack_license" and returns counts of each combination.</span></span> <span data-ttu-id="cbff8-249">Abaixo estão os conteúdos.</span><span class="sxs-lookup"><span data-stu-id="cbff8-249">Below are its contents.</span></span>

    SELECT medallion, hack_license, COUNT(*) as trip_count
    FROM nyctaxidb.fare
    WHERE month=1
    GROUP BY medallion, hack_license
    HAVING trip_count > 100
    ORDER BY trip_count desc;

<span data-ttu-id="cbff8-250">Esta consulta retorna combinações de táxi e condutor específico por número decrescente de corridas.</span><span class="sxs-lookup"><span data-stu-id="cbff8-250">This query returns cab and particular driver combinations ordered by descending number of trips.</span></span>

<span data-ttu-id="cbff8-251">De saudação Hive prompt de diretório, execute:</span><span class="sxs-lookup"><span data-stu-id="cbff8-251">From hello Hive directory prompt, run :</span></span>

    hive -f "C:\temp\sample_hive_trip_count_by_medallion_license.hql" > C:\temp\queryoutput.tsv

<span data-ttu-id="cbff8-252">resultados da consulta Olá são gravados tooa local arquivo C:\temp\queryoutput.tsv.</span><span class="sxs-lookup"><span data-stu-id="cbff8-252">hello query results are written tooa local file C:\temp\queryoutput.tsv.</span></span>

### <a name="exploration-assessing-data-quality-by-checking-for-invalid-longitudelatitude-records"></a><span data-ttu-id="cbff8-253">Exploração: avaliar a qualidade dos dados através da verificação de registros de latitude/longitude inválidos</span><span class="sxs-lookup"><span data-stu-id="cbff8-253">Exploration: Assessing data quality by checking for invalid longitude/latitude records</span></span>
> [!NOTE]
> <span data-ttu-id="cbff8-254">Essa é normalmente é uma tarefa de **Cientista de Dados** .</span><span class="sxs-lookup"><span data-stu-id="cbff8-254">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="cbff8-255">Um objetivo comum de análise de dados exploratório é tooweed registros inválido ou incorreto.</span><span class="sxs-lookup"><span data-stu-id="cbff8-255">A common objective of exploratory data analysis is tooweed out invalid or bad records.</span></span> <span data-ttu-id="cbff8-256">Olá exemplo nesta seção determina se hello campos de longitude ou latitude contenham um valor muito fora Olá área NYC.</span><span class="sxs-lookup"><span data-stu-id="cbff8-256">hello example in this section determines whether either hello longitude or latitude fields contain a value far outside hello NYC area.</span></span> <span data-ttu-id="cbff8-257">Como é provável que esses registros têm um valores de latitude de longitude incorretos, desejamos tooeliminate-los de qualquer dado que seja toobe usados na modelagem.</span><span class="sxs-lookup"><span data-stu-id="cbff8-257">Since it is likely that such records have an erroneous longitude-latitude values, we want tooeliminate them from any data that is toobe used for modeling.</span></span>

<span data-ttu-id="cbff8-258">Aqui está o conteúdo de saudação do *exemplo\_hive\_qualidade\_assessment.hql* arquivo para inspeção.</span><span class="sxs-lookup"><span data-stu-id="cbff8-258">Here is hello content of *sample\_hive\_quality\_assessment.hql* file for inspection.</span></span>

        SELECT COUNT(*) FROM nyctaxidb.trip
        WHERE month=1
        AND  (CAST(pickup_longitude AS float) NOT BETWEEN -90 AND -30
        OR    CAST(pickup_latitude AS float) NOT BETWEEN 30 AND 90
        OR    CAST(dropoff_longitude AS float) NOT BETWEEN -90 AND -30
        OR    CAST(dropoff_latitude AS float) NOT BETWEEN 30 AND 90);


<span data-ttu-id="cbff8-259">De saudação Hive prompt de diretório, execute:</span><span class="sxs-lookup"><span data-stu-id="cbff8-259">From hello Hive directory prompt, run :</span></span>

    hive -S -f "C:\temp\sample_hive_quality_assessment.hql"

<span data-ttu-id="cbff8-260">Olá *-S* argumento incluído nesse comando suprime a impressão de tela hello status dos trabalhos de Hive mapear/reduzir hello.</span><span class="sxs-lookup"><span data-stu-id="cbff8-260">hello *-S* argument included in this command suppresses hello status screen printout of hello Hive Map/Reduce jobs.</span></span> <span data-ttu-id="cbff8-261">Isso é útil porque facilita a impressão de tela de saudação do hello mais legível de saída de consulta de Hive.</span><span class="sxs-lookup"><span data-stu-id="cbff8-261">This is useful because it makes hello screen print of hello Hive query output more readable.</span></span>

### <a name="exploration-binary-class-distributions-of-trip-tips"></a><span data-ttu-id="cbff8-262">Exploração: distribuições de classe binária de gorjetas para corridas</span><span class="sxs-lookup"><span data-stu-id="cbff8-262">Exploration: Binary class distributions of trip tips</span></span>
> [!NOTE]
> <span data-ttu-id="cbff8-263">Essa é normalmente é uma tarefa de **Cientista de Dados** .</span><span class="sxs-lookup"><span data-stu-id="cbff8-263">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="cbff8-264">Problema de classificação binária Olá descritas em hello [exemplos de tarefas de previsão](machine-learning-data-science-process-hive-walkthrough.md#mltasks) seção, é útil tooknow se uma dica foi fornecida ou não.</span><span class="sxs-lookup"><span data-stu-id="cbff8-264">For hello binary classification problem outlined in hello [Examples of prediction tasks](machine-learning-data-science-process-hive-walkthrough.md#mltasks) section, it is useful tooknow whether a tip was given or not.</span></span> <span data-ttu-id="cbff8-265">Essa distribuição de gorjetas é binária:</span><span class="sxs-lookup"><span data-stu-id="cbff8-265">This distribution of tips is binary:</span></span>

* <span data-ttu-id="cbff8-266">tip given(Class 1, tip\_amount > $0)</span><span class="sxs-lookup"><span data-stu-id="cbff8-266">tip given(Class 1, tip\_amount > $0)</span></span>  
* <span data-ttu-id="cbff8-267">no tip (Class 0, tip\_amount = $0).</span><span class="sxs-lookup"><span data-stu-id="cbff8-267">no tip (Class 0, tip\_amount = $0).</span></span>

<span data-ttu-id="cbff8-268">Olá *exemplo\_hive\_Oblíquo\_frequencies.hql* arquivo mostrado a seguir faz isso.</span><span class="sxs-lookup"><span data-stu-id="cbff8-268">hello *sample\_hive\_tipped\_frequencies.hql* file shown below does this.</span></span>

    SELECT tipped, COUNT(*) AS tip_freq
    FROM
    (
        SELECT if(tip_amount > 0, 1, 0) as tipped, tip_amount
        FROM nyctaxidb.fare
    )tc
    GROUP BY tipped;

<span data-ttu-id="cbff8-269">De saudação Hive prompt de diretório, execute:</span><span class="sxs-lookup"><span data-stu-id="cbff8-269">From hello Hive directory prompt, run:</span></span>

    hive -f "C:\temp\sample_hive_tipped_frequencies.hql"


### <a name="exploration-class-distributions-in-hello-multiclass-setting"></a><span data-ttu-id="cbff8-270">Exploração: Classe distribuições na configuração multiclasse Olá</span><span class="sxs-lookup"><span data-stu-id="cbff8-270">Exploration: Class distributions in hello multiclass setting</span></span>
> [!NOTE]
> <span data-ttu-id="cbff8-271">Essa é normalmente é uma tarefa de **Cientista de Dados** .</span><span class="sxs-lookup"><span data-stu-id="cbff8-271">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="cbff8-272">Problema de classificação multiclasse Olá descritas Olá [exemplos de tarefas de previsão](machine-learning-data-science-process-hive-walkthrough.md#mltasks) seção esse conjunto de dados também se presta tooa classificação natural onde gostaria toopredict quantidade de Olá Olá dicas fornecido.</span><span class="sxs-lookup"><span data-stu-id="cbff8-272">For hello multiclass classification problem outlined in hello [Examples of prediction tasks](machine-learning-data-science-process-hive-walkthrough.md#mltasks) section this data set also lends itself tooa natural classification where we would like toopredict hello amount of hello tips given.</span></span> <span data-ttu-id="cbff8-273">Podemos usar compartimentos toodefine dica intervalos na consulta de saudação.</span><span class="sxs-lookup"><span data-stu-id="cbff8-273">We can use bins toodefine tip ranges in hello query.</span></span> <span data-ttu-id="cbff8-274">tooget vários intervalos de dica de distribuições de classe para Olá Olá, usamos Olá *exemplo\_hive\_dica\_intervalo\_frequencies.hql* arquivo.</span><span class="sxs-lookup"><span data-stu-id="cbff8-274">tooget hello class distributions for hello various tip ranges, we use hello *sample\_hive\_tip\_range\_frequencies.hql* file.</span></span> <span data-ttu-id="cbff8-275">Abaixo estão os conteúdos.</span><span class="sxs-lookup"><span data-stu-id="cbff8-275">Below are its contents.</span></span>

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

<span data-ttu-id="cbff8-276">Execute Olá comando a seguir no console de linha de comando do Hadoop:</span><span class="sxs-lookup"><span data-stu-id="cbff8-276">Run hello following command from Hadoop Command Line console:</span></span>

    hive -f "C:\temp\sample_hive_tip_range_frequencies.hql"

### <a name="exploration-compute-direct-distance-between-two-longitude-latitude-locations"></a><span data-ttu-id="cbff8-277">Exploração: calcular a distância direta entre dois locais de latitude-longitude</span><span class="sxs-lookup"><span data-stu-id="cbff8-277">Exploration: Compute Direct Distance Between Two Longitude-Latitude Locations</span></span>
> [!NOTE]
> <span data-ttu-id="cbff8-278">Essa é normalmente é uma tarefa de **Cientista de Dados** .</span><span class="sxs-lookup"><span data-stu-id="cbff8-278">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="cbff8-279">Uma medida de distância direta Olá permite-nos toofind out discrepância Olá entre ele e hello real trip distância.</span><span class="sxs-lookup"><span data-stu-id="cbff8-279">Having a measure of hello direct distance allows us toofind out hello discrepancy between it and hello actual trip distance.</span></span> <span data-ttu-id="cbff8-280">Podemos motivar esse recurso destacando um passageiro talvez seja menor provável dica de ferramenta se eles descobrir driver Olá intencionalmente obteve-los por uma rota muito mais longa.</span><span class="sxs-lookup"><span data-stu-id="cbff8-280">We motivate this feature by pointing out that a passenger might be less likely tootip if they figure out that hello driver has intentionally taken them by a much longer route.</span></span>

<span data-ttu-id="cbff8-281">comparação de saudação toosee entre a distância de viagem real e hello [distância do Haverseno](http://en.wikipedia.org/wiki/Haversine_formula) entre dois pontos de longitude latitude (distância do "círculo ótimo" hello), usamos Olá trigonométricas funções disponíveis no Hive, assim:</span><span class="sxs-lookup"><span data-stu-id="cbff8-281">toosee hello comparison between actual trip distance and hello [Haversine distance](http://en.wikipedia.org/wiki/Haversine_formula) between two longitude-latitude points (hello "great circle" distance), we use hello trigonometric functions available within Hive, thus :</span></span>

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

<span data-ttu-id="cbff8-282">Na consulta Olá acima, R é o raio Olá Olá terra em milhas e pi é tooradians convertido.</span><span class="sxs-lookup"><span data-stu-id="cbff8-282">In hello query above, R is hello radius of hello Earth in miles, and pi is converted tooradians.</span></span> <span data-ttu-id="cbff8-283">Observe que os pontos de longitude latitude Olá são "filtrados" tooremove valores que estão distantes de área de NYC hello.</span><span class="sxs-lookup"><span data-stu-id="cbff8-283">Note that hello longitude-latitude points are "filtered" tooremove values that are far from hello NYC area.</span></span>

<span data-ttu-id="cbff8-284">Nesse caso, escrevemos nosso diretório tooa de resultados chamado "queryoutputdir".</span><span class="sxs-lookup"><span data-stu-id="cbff8-284">In this case, we write our results tooa directory called "queryoutputdir".</span></span> <span data-ttu-id="cbff8-285">sequência de saudação de comandos mostrados abaixo primeiro cria esse diretório de saída e, em seguida, executa o comando de Hive hello.</span><span class="sxs-lookup"><span data-stu-id="cbff8-285">hello sequence of commands shown below first creates this output directory, and then runs hello Hive command.</span></span>

<span data-ttu-id="cbff8-286">De saudação Hive prompt de diretório, execute:</span><span class="sxs-lookup"><span data-stu-id="cbff8-286">From hello Hive directory prompt, run:</span></span>

    hdfs dfs -mkdir wasb:///queryoutputdir

    hive -f "C:\temp\sample_hive_trip_direct_distance.hql"


<span data-ttu-id="cbff8-287">Olá resultados da consulta são gravados blobs do Azure de too9 ***queryoutputdir/000000\_0*** muito ***queryoutputdir/000008\_0*** no contêiner de padrão de saudação do cluster de Hadoop hello.</span><span class="sxs-lookup"><span data-stu-id="cbff8-287">hello query results are written too9 Azure blobs ***queryoutputdir/000000\_0*** too ***queryoutputdir/000008\_0*** under hello default container of hello Hadoop cluster.</span></span>

<span data-ttu-id="cbff8-288">tamanho de saudação toosee de blobs individuais hello, executamos Olá comando a seguir no prompt de diretório de Hive hello:</span><span class="sxs-lookup"><span data-stu-id="cbff8-288">toosee hello size of hello individual blobs, we run hello following command from hello Hive directory prompt :</span></span>

    hdfs dfs -ls wasb:///queryoutputdir

<span data-ttu-id="cbff8-289">conteúdo de saudação toosee de um determinado arquivo, digamos que 000000\_0, usamos do Hadoop `copyToLocal` comando assim.</span><span class="sxs-lookup"><span data-stu-id="cbff8-289">toosee hello contents of a given file, say 000000\_0, we use Hadoop's `copyToLocal` command, thus.</span></span>

    hdfs dfs -copyToLocal wasb:///queryoutputdir/000000_0 C:\temp\tempfile

> [!WARNING]
> <span data-ttu-id="cbff8-290">O `copyToLocal` pode ser muito lento para arquivos grandes e não é recomendado para uso com eles.</span><span class="sxs-lookup"><span data-stu-id="cbff8-290">`copyToLocal` can be very slow for large files, and is not recommended for use with them.</span></span>  
> 
> 

<span data-ttu-id="cbff8-291">Uma vantagem importante da ter esses dados residem em um blob do Azure é que podemos pode explorar dados de saudação dentro de aprendizado de máquina do Azure usando Olá [importar dados] [ import-data] módulo.</span><span class="sxs-lookup"><span data-stu-id="cbff8-291">A key advantage of having this data reside in an Azure blob is that we may explore hello data within Azure Machine Learning using hello [Import Data][import-data] module.</span></span>

## <span data-ttu-id="cbff8-292">
            <a name="#downsample">
            </a>Para reduzir dados e criar modelos no Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="cbff8-292"><a name="#downsample"></a>Down sample data and build models in Azure Machine Learning</span></span>
> [!NOTE]
> <span data-ttu-id="cbff8-293">Essa é normalmente é uma tarefa de **Cientista de Dados** .</span><span class="sxs-lookup"><span data-stu-id="cbff8-293">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="cbff8-294">Após a fase de análise de dados exploratório hello, estamos agora dados de saudação de exemplo toodown pronto para criar modelos no aprendizado de máquina do Azure.</span><span class="sxs-lookup"><span data-stu-id="cbff8-294">After hello exploratory data analysis phase, we are now ready toodown sample hello data for building models in Azure Machine Learning.</span></span> <span data-ttu-id="cbff8-295">Nesta seção, mostramos como toouse um Hive consultar dados de saudação do exemplo toodown, que são acessados de saudação [importar dados] [ import-data] módulo no aprendizado de máquina do Azure.</span><span class="sxs-lookup"><span data-stu-id="cbff8-295">In this section, we show how toouse a Hive query toodown sample hello data, which is then accessed from hello [Import Data][import-data] module in Azure Machine Learning.</span></span>

### <a name="down-sampling-hello-data"></a><span data-ttu-id="cbff8-296">Para baixo Olá dados de amostra</span><span class="sxs-lookup"><span data-stu-id="cbff8-296">Down sampling hello data</span></span>
<span data-ttu-id="cbff8-297">Há duas etapas neste procedimento.</span><span class="sxs-lookup"><span data-stu-id="cbff8-297">There are two steps in this procedure.</span></span> <span data-ttu-id="cbff8-298">Primeiro, associe Olá **nyctaxidb.trip** e **nyctaxidb.fare** tabelas em três chaves que estão presentes em todos os registros: "medallion", "hack\_licença", e "retirada\_datetime".</span><span class="sxs-lookup"><span data-stu-id="cbff8-298">First we join hello **nyctaxidb.trip** and **nyctaxidb.fare** tables on three keys that are present in all records : "medallion", "hack\_license", and "pickup\_datetime".</span></span> <span data-ttu-id="cbff8-299">Então geramos um rótulo de classificação binária **tipped** e um rótulo de classificação multiclasse **tip\_class**.</span><span class="sxs-lookup"><span data-stu-id="cbff8-299">We then generate a binary classification label **tipped** and a multi-class classification label **tip\_class**.</span></span>

<span data-ttu-id="cbff8-300">toobe toouse capaz de saudação dados amostrados diretamente da saudação [importar dados] [ import-data] módulo no aprendizado de máquina do Azure, é necessário toostore resultados Olá Olá acima da tabela de Hive consulta tooan interna.</span><span class="sxs-lookup"><span data-stu-id="cbff8-300">toobe able toouse hello down sampled data directly from hello [Import Data][import-data] module in Azure Machine Learning, it is necessary toostore hello results of hello above query tooan internal Hive table.</span></span> <span data-ttu-id="cbff8-301">Em que os itens a seguir, criamos uma tabela interna de Hive e preencher seu conteúdo com hello unidas e dados de amostra.</span><span class="sxs-lookup"><span data-stu-id="cbff8-301">In what follows, we create an internal Hive table and populate its contents with hello joined and down sampled data.</span></span>

<span data-ttu-id="cbff8-302">Olá, consulta aplica funções de Hive padrão diretamente toogenerate hora de saudação do dia, semana do ano, dia da semana (1 significa segunda-feira e 7 significa para domingo) do hello "retirada\_datetime" campo e a distância direta Olá entre retirada hello e redução locais.</span><span class="sxs-lookup"><span data-stu-id="cbff8-302">hello query applies standard Hive functions directly toogenerate hello hour of day, week of year, weekday (1 stands for Monday, and 7 stands for Sunday) from hello "pickup\_datetime" field,  and hello direct distance between hello pickup and dropoff locations.</span></span> <span data-ttu-id="cbff8-303">Os usuários podem consultar muito[LanguageManual UDF](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF) para obter uma lista dessas funções.</span><span class="sxs-lookup"><span data-stu-id="cbff8-303">Users can refer too[LanguageManual UDF](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF) for a complete list of such functions.</span></span>

<span data-ttu-id="cbff8-304">Olá consulta e para baixo dados saudação de exemplos para que os resultados da consulta Olá comportada Olá estúdio de aprendizado de máquina do Azure.</span><span class="sxs-lookup"><span data-stu-id="cbff8-304">hello query then down samples hello data so that hello query results can fit into hello Azure Machine Learning Studio.</span></span> <span data-ttu-id="cbff8-305">Somente cerca de 1% do conjunto de dados original Olá é importado para Olá Studio.</span><span class="sxs-lookup"><span data-stu-id="cbff8-305">Only about 1% of hello original dataset is imported into hello Studio.</span></span>

<span data-ttu-id="cbff8-306">Abaixo estão os conteúdos de saudação do *exemplo\_hive\_preparar\_para\_aml\_full.hql* arquivo que prepara os dados para o modelo de criação no aprendizado de máquina do Azure.</span><span class="sxs-lookup"><span data-stu-id="cbff8-306">Below are hello contents of *sample\_hive\_prepare\_for\_aml\_full.hql* file that prepares data for model building in Azure Machine Learning.</span></span>

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

<span data-ttu-id="cbff8-307">solicitar que essa consulta, do diretório de Hive Olá toorun:</span><span class="sxs-lookup"><span data-stu-id="cbff8-307">toorun this query, from hello Hive directory prompt :</span></span>

    hive -f "C:\temp\sample_hive_prepare_for_aml_full.hql"

<span data-ttu-id="cbff8-308">Agora temos uma tabela interna "nyctaxidb.nyctaxi_downsampled_dataset", que podem ser acessados usando Olá [importar dados] [ import-data] módulo de aprendizado de máquina do Azure.</span><span class="sxs-lookup"><span data-stu-id="cbff8-308">We now have an internal table "nyctaxidb.nyctaxi_downsampled_dataset" which can be accessed using hello [Import Data][import-data] module from Azure Machine Learning.</span></span> <span data-ttu-id="cbff8-309">Além disso, podemos usar esse conjunto de dados para criar modelos de Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="cbff8-309">Furthermore, we may use this dataset for building Machine Learning models.</span></span>  

### <a name="use-hello-import-data-module-in-azure-machine-learning-tooaccess-hello-down-sampled-data"></a><span data-ttu-id="cbff8-310">Usar o módulo de importação de dados de Olá de saudação do aprendizado de máquina do Azure tooaccess dados de amostra</span><span class="sxs-lookup"><span data-stu-id="cbff8-310">Use hello Import Data module in Azure Machine Learning tooaccess hello down sampled data</span></span>
<span data-ttu-id="cbff8-311">Como pré-requisitos para emitir consultas de Hive no hello [importar dados] [ import-data] módulo de aprendizado de máquina do Azure, é necessário acessar o espaço de trabalho de aprendizado de máquina do Azure tooan e credenciais de toohello de saudação de acesso cluster e sua conta de armazenamento associada.</span><span class="sxs-lookup"><span data-stu-id="cbff8-311">As prerequisites for issuing Hive queries in hello [Import Data][import-data] module of Azure Machine Learning, we need access tooan Azure Machine Learning workspace and access toohello credentials of hello cluster and its associated storage account.</span></span>

<span data-ttu-id="cbff8-312">Alguns detalhes Olá [importar dados] [ import-data] tooinput de parâmetros do módulo e hello:</span><span class="sxs-lookup"><span data-stu-id="cbff8-312">Some details on hello [Import Data][import-data] module and hello parameters tooinput :</span></span>

<span data-ttu-id="cbff8-313">**URI do servidor HCatalog**: se o nome de cluster Olá for abc123, isso é simplesmente: https://abc123.azurehdinsight.net</span><span class="sxs-lookup"><span data-stu-id="cbff8-313">**HCatalog server URI**: If hello cluster name is abc123, then this is simply : https://abc123.azurehdinsight.net</span></span>

<span data-ttu-id="cbff8-314">**Nome de conta de usuário do Hadoop** : nome de usuário Olá escolhido para o cluster de saudação (**não** nome de usuário de acesso remoto Olá)</span><span class="sxs-lookup"><span data-stu-id="cbff8-314">**Hadoop user account name** : hello user name chosen for hello cluster (**not** hello remote access user name)</span></span>

<span data-ttu-id="cbff8-315">**Senha da conta do usuário Hadoop** : senha Olá escolhida para o cluster de saudação (**não** senha de acesso remoto Olá)</span><span class="sxs-lookup"><span data-stu-id="cbff8-315">**Hadoop ser account password** : hello password chosen for hello cluster (**not** hello remote access password)</span></span>

<span data-ttu-id="cbff8-316">**Local dos dados de saída** : isso é escolhido toobe do Azure.</span><span class="sxs-lookup"><span data-stu-id="cbff8-316">**Location of output data** : This is chosen toobe Azure.</span></span>

<span data-ttu-id="cbff8-317">**Nome da conta de armazenamento do Azure** : nome saudação padrão da conta de armazenamento associada Olá cluster.</span><span class="sxs-lookup"><span data-stu-id="cbff8-317">**Azure storage account name** : Name of hello default storage account associated with hello cluster.</span></span>

<span data-ttu-id="cbff8-318">**Nome do contêiner do Azure** : isso é nome do contêiner padrão Olá para cluster hello e normalmente é Olá mesmo como o nome do cluster hello.</span><span class="sxs-lookup"><span data-stu-id="cbff8-318">**Azure container name** : This is hello default container name for hello cluster, and is typically hello same as hello cluster name.</span></span> <span data-ttu-id="cbff8-319">Para um cluster chamado "abc123", é simplesmente abc123.</span><span class="sxs-lookup"><span data-stu-id="cbff8-319">For a cluster called "abc123", this is just abc123.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cbff8-320">**Qualquer tabela que desejamos tooquery usando Olá [importar dados] [ import-data] módulo no aprendizado de máquina do Azure deve ser uma tabela interna.**</span><span class="sxs-lookup"><span data-stu-id="cbff8-320">**Any table we wish tooquery using hello [Import Data][import-data] module in Azure Machine Learning must be an internal table.**</span></span> <span data-ttu-id="cbff8-321">Uma dica para determinar se uma tabela T em um banco de dados D.db é uma tabela interna é a seguinte:</span><span class="sxs-lookup"><span data-stu-id="cbff8-321">A tip for determining if a table T in a database D.db is an internal table is as follows.</span></span>
> 
> 

<span data-ttu-id="cbff8-322">De saudação Hive aviso de diretório, o comando de saudação do problema:</span><span class="sxs-lookup"><span data-stu-id="cbff8-322">From hello Hive directory prompt, issue hello command :</span></span>

    hdfs dfs -ls wasb:///D.db/T

<span data-ttu-id="cbff8-323">Se a tabela de saudação é uma tabela interna e ele é preenchido, seu conteúdo deve ser exibidos aqui.</span><span class="sxs-lookup"><span data-stu-id="cbff8-323">If hello table is an internal table and it is populated, its contents must show here.</span></span> <span data-ttu-id="cbff8-324">Outro toodetermine de forma que se uma tabela é uma tabela interna é toouse hello Azure Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="cbff8-324">Another way toodetermine whether a table is an internal table is toouse hello Azure Storage Explorer.</span></span> <span data-ttu-id="cbff8-325">Usá-lo toonavigate toohello nome do contêiner padrão do cluster hello e, em seguida, filtrar pelo nome da tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="cbff8-325">Use it toonavigate toohello default container name of hello cluster, and then filter by hello table name.</span></span> <span data-ttu-id="cbff8-326">Se a tabela hello e seu conteúdo aparecer, isso confirma que é uma tabela interna.</span><span class="sxs-lookup"><span data-stu-id="cbff8-326">If hello table and its contents show up, this confirms that it is an internal table.</span></span>

<span data-ttu-id="cbff8-327">Aqui está um instantâneo da consulta de Hive hello e Olá [importar dados] [ import-data] módulo:</span><span class="sxs-lookup"><span data-stu-id="cbff8-327">Here is a snapshot of hello Hive query and hello [Import Data][import-data] module:</span></span>

![Consulta de hive para o módulo Importar Dados](./media/machine-learning-data-science-process-hive-walkthrough/1eTYf52.png)

<span data-ttu-id="cbff8-329">Observe que, desde o nosso down dados amostrados residem no contêiner de padrão de Olá, consulta de Hive resultante saudação do aprendizado de máquina do Azure é muito simple e é apenas uma "Selecione * de nyctaxidb.nyctaxi\_reduzida\_dados".</span><span class="sxs-lookup"><span data-stu-id="cbff8-329">Note that since our down sampled data resides in hello default container, hello resulting Hive query from Azure Machine Learning is very simple and is just a "SELECT * FROM nyctaxidb.nyctaxi\_downsampled\_data".</span></span>

<span data-ttu-id="cbff8-330">saudação de conjunto de dados agora pode ser usado como Olá ponto de partida para criar modelos de aprendizado de máquina.</span><span class="sxs-lookup"><span data-stu-id="cbff8-330">hello dataset may now be used as hello starting point for building Machine Learning models.</span></span>

### <span data-ttu-id="cbff8-331">
            <a name="mlmodel">
            </a>Compilar modelos no Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="cbff8-331"><a name="mlmodel"></a>Build models in Azure Machine Learning</span></span>
<span data-ttu-id="cbff8-332">Estamos agora capaz de tooproceed toomodel criação e implantação de modelo no [aprendizado de máquina do Azure](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="cbff8-332">We are now able tooproceed toomodel building and model deployment in [Azure Machine Learning](https://studio.azureml.net).</span></span> <span data-ttu-id="cbff8-333">dados de saudação estão prontos para que possamos toouse resolver problemas de previsão Olá identificados acima:</span><span class="sxs-lookup"><span data-stu-id="cbff8-333">hello data is ready for us toouse in addressing hello prediction problems identified above:</span></span>

<span data-ttu-id="cbff8-334">**1. Classificação binária**: toopredict ou não uma dica foi pago uma viagem.</span><span class="sxs-lookup"><span data-stu-id="cbff8-334">**1. Binary classification**: toopredict whether or not a tip was paid for a trip.</span></span>

<span data-ttu-id="cbff8-335">**Aprendiz usado:** regressão logística de classe dois</span><span class="sxs-lookup"><span data-stu-id="cbff8-335">**Learner used:** Two-class logistic regression</span></span>

<span data-ttu-id="cbff8-336">a.</span><span class="sxs-lookup"><span data-stu-id="cbff8-336">a.</span></span> <span data-ttu-id="cbff8-337">Para esse problema, nosso rótulo (ou classe) de destino é "tipped".</span><span class="sxs-lookup"><span data-stu-id="cbff8-337">For this problem, our target (or class) label is "tipped".</span></span> <span data-ttu-id="cbff8-338">Nosso conjunto de dados original convertidos tem algumas colunas que são vazamentos de destino para esse teste de classificação.</span><span class="sxs-lookup"><span data-stu-id="cbff8-338">Our original down-sampled dataset has a few columns that are target leaks for this classification experiment.</span></span> <span data-ttu-id="cbff8-339">Em particular: dica\_da classe, a dica\_quantidade e total\_valor revelam informações sobre o rótulo de destino de saudação que não está disponível no tempo de teste.</span><span class="sxs-lookup"><span data-stu-id="cbff8-339">In particular : tip\_class, tip\_amount, and total\_amount reveal information about hello target label that is not available at testing time.</span></span> <span data-ttu-id="cbff8-340">Remover essas colunas consideração usando Olá [selecionar colunas no conjunto de dados] [ select-columns] módulo.</span><span class="sxs-lookup"><span data-stu-id="cbff8-340">We remove these columns from consideration using hello [Select Columns in Dataset][select-columns] module.</span></span>

<span data-ttu-id="cbff8-341">instantâneo de saudação abaixo mostra toopredict nossa experiência ou não uma dica foi paga para uma determinado viagem.</span><span class="sxs-lookup"><span data-stu-id="cbff8-341">hello snapshot below shows our experiment toopredict whether or not a tip was paid for a given trip.</span></span>

![Instantâneo de teste](./media/machine-learning-data-science-process-hive-walkthrough/QGxRz5A.png)

<span data-ttu-id="cbff8-343">b.</span><span class="sxs-lookup"><span data-stu-id="cbff8-343">b.</span></span> <span data-ttu-id="cbff8-344">Para esse teste, nossas distribuições de rótulo de destino foram de aproximadamente 1:1.</span><span class="sxs-lookup"><span data-stu-id="cbff8-344">For this experiment, our target label distributions were roughly 1:1.</span></span>

<span data-ttu-id="cbff8-345">instantâneo de saudação abaixo mostra a distribuição de saudação de rótulos de classe de dica de problema de classificação binária hello.</span><span class="sxs-lookup"><span data-stu-id="cbff8-345">hello snapshot below shows hello distribution of tip class labels for hello binary classification problem.</span></span>

![Distribuição de rótulos de classe de dica](./media/machine-learning-data-science-process-hive-walkthrough/9mM4jlD.png)

<span data-ttu-id="cbff8-347">Como resultado, obtemos um AUC de 0.987, conforme mostrado na figura abaixo a saudação.</span><span class="sxs-lookup"><span data-stu-id="cbff8-347">As a result, we obtain an AUC of 0.987 as shown in hello figure below.</span></span>

![Valor AUC](./media/machine-learning-data-science-process-hive-walkthrough/8JDT0F8.png)

<span data-ttu-id="cbff8-349">**2. Classificação multiclasse**: classes definidas por intervalo de saudação toopredict de quantidades de dica pagado para viagem hello, usando Olá anteriormente.</span><span class="sxs-lookup"><span data-stu-id="cbff8-349">**2. Multiclass classification**: toopredict hello range of tip amounts paid for hello trip, using hello previously defined classes.</span></span>

<span data-ttu-id="cbff8-350">**Aprendiz usado:** regressão logística de várias classes</span><span class="sxs-lookup"><span data-stu-id="cbff8-350">**Learner used:** Multiclass logistic regression</span></span>

<span data-ttu-id="cbff8-351">a.</span><span class="sxs-lookup"><span data-stu-id="cbff8-351">a.</span></span> <span data-ttu-id="cbff8-352">Para esse problema, nosso rótulo de destino (ou classe) é "tip\_class", que pode ter um dos cinco valores (0,1,2,3,4).</span><span class="sxs-lookup"><span data-stu-id="cbff8-352">For this problem, our target (or class) label is "tip\_class" which can take one of five values (0,1,2,3,4).</span></span> <span data-ttu-id="cbff8-353">Como no caso de classificação binária hello, temos algumas colunas são vazamentos de destino para esse teste.</span><span class="sxs-lookup"><span data-stu-id="cbff8-353">As in hello binary classification case, we have a few columns that are target leaks for this experiment.</span></span> <span data-ttu-id="cbff8-354">Em particular: Oblíquo, Dica\_quantidade, total\_valor revelam informações sobre o rótulo de destino de saudação que não está disponível no tempo de teste.</span><span class="sxs-lookup"><span data-stu-id="cbff8-354">In particular : tipped, tip\_amount, total\_amount reveal information about hello target label that is not available at testing time.</span></span> <span data-ttu-id="cbff8-355">Removemos essas colunas usando Olá [selecionar colunas no conjunto de dados] [ select-columns] módulo.</span><span class="sxs-lookup"><span data-stu-id="cbff8-355">We remove these columns using hello [Select Columns in Dataset][select-columns] module.</span></span>

<span data-ttu-id="cbff8-356">Olá instantâneo abaixo mostra nosso toopredict de teste no qual bin uma dica é provavelmente toofall (classe 0: dica = $0, a classe 1: Dica > $0 e a dica < = US $5, classe 2: Dica > US $5 e a dica < = US $10, 3 da classe: Dica > $10 e a dica < = US $20 Classe 4: Dica > US $20)</span><span class="sxs-lookup"><span data-stu-id="cbff8-356">hello snapshot below shows our experiment toopredict in which bin a tip is likely toofall ( Class 0: tip = $0, class 1 : tip > $0 and tip <= $5, Class 2 : tip > $5 and tip <= $10, Class 3 : tip > $10 and tip <= $20, Class 4 : tip > $20)</span></span>

![Instantâneo de teste](./media/machine-learning-data-science-process-hive-walkthrough/5ztv0n0.png)

<span data-ttu-id="cbff8-358">Agora mostraremos a aparência de nossa distribuição de classe de teste real.</span><span class="sxs-lookup"><span data-stu-id="cbff8-358">We now show what our actual test class distribution looks like.</span></span> <span data-ttu-id="cbff8-359">Podemos ver que enquanto classe 0 e 1 de classe são predominantes, hello outras classes são raros.</span><span class="sxs-lookup"><span data-stu-id="cbff8-359">We see that while Class 0 and Class 1 are prevalent, hello other classes are rare.</span></span>

![Distribuição de classe de teste](./media/machine-learning-data-science-process-hive-walkthrough/Vy1FUKa.png)

<span data-ttu-id="cbff8-361">b.</span><span class="sxs-lookup"><span data-stu-id="cbff8-361">b.</span></span> <span data-ttu-id="cbff8-362">Para esse teste, usamos um toolook de matriz de confusão em nosso precisões de previsão.</span><span class="sxs-lookup"><span data-stu-id="cbff8-362">For this experiment, we use a confusion matrix toolook at our prediction accuracies.</span></span> <span data-ttu-id="cbff8-363">Isso é mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="cbff8-363">This is shown below.</span></span>

![Matriz de confusão](./media/machine-learning-data-science-process-hive-walkthrough/cxFmErM.png)

<span data-ttu-id="cbff8-365">Observe que enquanto precisões nossa classe em classes predominantes Olá é muito bom, modelo Olá não faz um bom trabalho de "aprendizagem" em classes mais raras hello.</span><span class="sxs-lookup"><span data-stu-id="cbff8-365">Note that while our class accuracies on hello prevalent classes is quite good, hello model does not do a good job of "learning" on hello rarer classes.</span></span>

<span data-ttu-id="cbff8-366">**3. Tarefa de regressão**: o valor de saudação toopredict de dica pago para uma viagem.</span><span class="sxs-lookup"><span data-stu-id="cbff8-366">**3. Regression task**: toopredict hello amount of tip paid for a trip.</span></span>

<span data-ttu-id="cbff8-367">**Aprendiz usado:** árvore de decisão aprimorada</span><span class="sxs-lookup"><span data-stu-id="cbff8-367">**Learner used:** Boosted decision tree</span></span>

<span data-ttu-id="cbff8-368">a.</span><span class="sxs-lookup"><span data-stu-id="cbff8-368">a.</span></span> <span data-ttu-id="cbff8-369">Para esse problema, nosso rótulo (ou classe) de destino é "tip\_amount".</span><span class="sxs-lookup"><span data-stu-id="cbff8-369">For this problem, our target (or class) label is "tip\_amount".</span></span> <span data-ttu-id="cbff8-370">Nesse caso, nossos vazamentos de destino são:-Oblíquo, Dica\_classe total\_quantidade; todas essas variáveis revelam informações sobre a quantidade de dica de saudação que normalmente não está disponível no tempo de teste.</span><span class="sxs-lookup"><span data-stu-id="cbff8-370">Our target leaks in this case are : tipped, tip\_class, total\_amount ; all these variables reveal information about hello tip amount that is typically unavailable at testing time.</span></span> <span data-ttu-id="cbff8-371">Removemos essas colunas usando Olá [selecionar colunas no conjunto de dados] [ select-columns] módulo.</span><span class="sxs-lookup"><span data-stu-id="cbff8-371">We remove these columns using hello [Select Columns in Dataset][select-columns] module.</span></span>

<span data-ttu-id="cbff8-372">Olá instantâneo belows mostra nossa experiência toopredict Olá Olá fornecido dica.</span><span class="sxs-lookup"><span data-stu-id="cbff8-372">hello snapshot belows shows our experiment toopredict hello amount of hello given tip.</span></span>

![Instantâneo de teste](./media/machine-learning-data-science-process-hive-walkthrough/11TZWgV.png)

<span data-ttu-id="cbff8-374">b.</span><span class="sxs-lookup"><span data-stu-id="cbff8-374">b.</span></span> <span data-ttu-id="cbff8-375">Para problemas de regressão, medimos precisões Olá de nossa previsão observando o erro Olá quadrado em previsões hello, Olá coeficiente de determinação e, Olá como.</span><span class="sxs-lookup"><span data-stu-id="cbff8-375">For regression problems, we measure hello accuracies of our prediction by looking at hello squared error in hello predictions, hello coefficient of determination, and hello like.</span></span> <span data-ttu-id="cbff8-376">Vamos mostrar isso abaixo.</span><span class="sxs-lookup"><span data-stu-id="cbff8-376">We show these below.</span></span>

![Estatísticas de previsão](./media/machine-learning-data-science-process-hive-walkthrough/Jat9mrz.png)

<span data-ttu-id="cbff8-378">Podemos ver que sobre Olá coeficiente de determinação é 0.709, implicando sobre 71% de variação de saudação é explicado pelo nosso coeficientes de modelo.</span><span class="sxs-lookup"><span data-stu-id="cbff8-378">We see that about hello coefficient of determination is 0.709, implying about 71% of hello variance is explained by our model coefficients.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cbff8-379">toolearn mais sobre o aprendizado de máquina do Azure e como tooaccess e usá-lo, consulte muito[o que é o aprendizado de máquina?](machine-learning-what-is-machine-learning.md).</span><span class="sxs-lookup"><span data-stu-id="cbff8-379">toolearn more about Azure Machine Learning and how tooaccess and use it, please refer too[What's Machine Learning?](machine-learning-what-is-machine-learning.md).</span></span> <span data-ttu-id="cbff8-380">Um recurso muito útil para a execução de um conjunto de experiências de aprendizado de máquina no aprendizado de máquina do Azure é hello [Cortana Intelligence galeria](https://gallery.cortanaintelligence.com/).</span><span class="sxs-lookup"><span data-stu-id="cbff8-380">A very useful resource for playing with a bunch of Machine Learning experiments on Azure Machine Learning is hello [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/).</span></span> <span data-ttu-id="cbff8-381">Olá Galeria abrange uma gama de experiências e fornece uma introdução detalhada no intervalo de saudação de recursos de aprendizado de máquina do Azure.</span><span class="sxs-lookup"><span data-stu-id="cbff8-381">hello Gallery covers a gamut of experiments and provides a thorough introduction into hello range of capabilities of Azure Machine Learning.</span></span>
> 
> 

## <a name="license-information"></a><span data-ttu-id="cbff8-382">Informações de Licença</span><span class="sxs-lookup"><span data-stu-id="cbff8-382">License Information</span></span>
<span data-ttu-id="cbff8-383">Este passo a passo do exemplo e seus scripts de acompanhamento são compartilhados pela Microsoft sob a licença do MIT hello.</span><span class="sxs-lookup"><span data-stu-id="cbff8-383">This sample walkthrough and its accompanying scripts are shared by Microsoft under hello MIT license.</span></span> <span data-ttu-id="cbff8-384">Verifique o arquivo de LICENSE.txt de saudação no diretório de saudação do código de exemplo hello no GitHub para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="cbff8-384">Please check hello LICENSE.txt file in in hello directory of hello sample code on GitHub for more details.</span></span>

## <a name="references"></a><span data-ttu-id="cbff8-385">Referências</span><span class="sxs-lookup"><span data-stu-id="cbff8-385">References</span></span>
<span data-ttu-id="cbff8-386">•   [Página de download de Viagens de Táxi de NYC, de Andrés Monroy](http://www.andresmh.com/nyctaxitrips/)</span><span class="sxs-lookup"><span data-stu-id="cbff8-386">•    [Andrés Monroy NYC Taxi Trips Download Page](http://www.andresmh.com/nyctaxitrips/)</span></span>  
<span data-ttu-id="cbff8-387">•   [Dados de Viagem de Táxi de FOILing NYC, de Chris Whong](http://chriswhong.com/open-data/foil_nyc_taxi/) </span><span class="sxs-lookup"><span data-stu-id="cbff8-387">•    [FOILing NYC’s Taxi Trip Data by Chris Whong](http://chriswhong.com/open-data/foil_nyc_taxi/) </span></span>  
<span data-ttu-id="cbff8-388">•   [Pesquisa e estatísticas de comissionamento de táxis e limusines de NYC](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span><span class="sxs-lookup"><span data-stu-id="cbff8-388">•    [NYC Taxi and Limousine Commission Research and Statistics](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span></span>

[2]: ./media/machine-learning-data-science-process-hive-walkthrough/output-hive-results-3.png
[11]: ./media/machine-learning-data-science-process-hive-walkthrough/hive-reader-properties.png
[12]: ./media/machine-learning-data-science-process-hive-walkthrough/binary-classification-training.png
[13]: ./media/machine-learning-data-science-process-hive-walkthrough/create-scoring-experiment.png
[14]: ./media/machine-learning-data-science-process-hive-walkthrough/binary-classification-scoring.png
[15]: ./media/machine-learning-data-science-process-hive-walkthrough/amlreader.png

<!-- Module References -->
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
