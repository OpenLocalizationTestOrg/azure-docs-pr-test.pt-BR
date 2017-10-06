---
title: recursos de aaaCreate para os dados no SQL Server usando o SQL e Python | Microsoft Docs
description: Processar dados do SQL Azure
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: 
ms.assetid: bf1f4a6c-7711-4456-beb7-35fdccd46a44
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev;fashah;garye
ms.openlocfilehash: 223352edb0377a159333e7528ad03c43902e6f45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-features-for-data-in-sql-server-using-sql-and-python"></a><span data-ttu-id="c4eae-103">Criar recursos para dados no SQL Server usando o SQL e o Python</span><span class="sxs-lookup"><span data-stu-id="c4eae-103">Create features for data in SQL Server using SQL and Python</span></span>
<span data-ttu-id="c4eae-104">Este documento mostra como toogenerate recursos para dados armazenados em uma VM do SQL Server no Azure que ajudam a algoritmos de aprenderem com mais eficiência de dados saudação.</span><span class="sxs-lookup"><span data-stu-id="c4eae-104">This document shows how toogenerate features for data stored in a SQL Server VM on Azure that help algorithms learn more efficiently from hello data.</span></span> <span data-ttu-id="c4eae-105">Isso pode ser feito usando o SQL ou usando uma linguagem de programação como o Python, ambos demonstrados aqui.</span><span class="sxs-lookup"><span data-stu-id="c4eae-105">This can be done by using SQL or by using a programming language like Python, both of which are demonstrated here.</span></span>

[!INCLUDE [cap-create-features-data-selector](../../includes/cap-create-features-selector.md)]

<span data-ttu-id="c4eae-106">Isso **menu** links tootopics que descrevem como toocreate recursos para os dados em vários ambientes.</span><span class="sxs-lookup"><span data-stu-id="c4eae-106">This **menu** links tootopics that describe how toocreate features for data in various environments.</span></span> <span data-ttu-id="c4eae-107">Essa tarefa é uma etapa Olá [processo de ciência de dados da equipe (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span><span class="sxs-lookup"><span data-stu-id="c4eae-107">This task is a step in hello [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

> [!NOTE]
> <span data-ttu-id="c4eae-108">Para obter um exemplo prático, você pode consultar Olá [NYC táxi dataset](http://www.andresmh.com/nyctaxitrips/) e consulte toohello IPNB intitulada [NYC dados disputa usando o bloco de anotações do IPython e o SQL Server](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) para uma apresentação de ponta a ponta.</span><span class="sxs-lookup"><span data-stu-id="c4eae-108">For a practical example, you can consult hello [NYC Taxi dataset](http://www.andresmh.com/nyctaxitrips/) and refer toohello IPNB titled [NYC Data wrangling using IPython Notebook and SQL Server](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) for an end-to-end walk-through.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="c4eae-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="c4eae-109">Prerequisites</span></span>
<span data-ttu-id="c4eae-110">Este artigo supõe que você:</span><span class="sxs-lookup"><span data-stu-id="c4eae-110">This article assumes that you have:</span></span>

* <span data-ttu-id="c4eae-111">Criou uma conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="c4eae-111">Created an Azure storage account.</span></span> <span data-ttu-id="c4eae-112">Se precisar de instruções, confira [Criar uma conta de Armazenamento do Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="c4eae-112">If you need instructions, see [Create an Azure Storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span></span>
* <span data-ttu-id="c4eae-113">Armazenou seus dados no SQL Server.</span><span class="sxs-lookup"><span data-stu-id="c4eae-113">Stored your data in SQL Server.</span></span> <span data-ttu-id="c4eae-114">Se você não tiver, consulte [mover dados tooan banco de dados do SQL Azure para o aprendizado de máquina do Azure](machine-learning-data-science-move-sql-azure.md) para obter instruções sobre como toomove Olá dados.</span><span class="sxs-lookup"><span data-stu-id="c4eae-114">If you have not, see [Move data tooan Azure SQL Database for Azure Machine Learning](machine-learning-data-science-move-sql-azure.md) for instructions on how toomove hello data there.</span></span>

## <span data-ttu-id="c4eae-115"><a name="sql-featuregen"></a>Geração de recursos com o SQL</span><span class="sxs-lookup"><span data-stu-id="c4eae-115"><a name="sql-featuregen"></a>Feature Generation with SQL</span></span>
<span data-ttu-id="c4eae-116">Nesta seção, descrevemos as maneiras de gerar recursos usando SQL:</span><span class="sxs-lookup"><span data-stu-id="c4eae-116">In this section, we describe ways of generating features using SQL:</span></span>  

1. [<span data-ttu-id="c4eae-117">Geração de recursos baseada em contagem</span><span class="sxs-lookup"><span data-stu-id="c4eae-117">Count based Feature Generation</span></span>](#sql-countfeature)
2. [<span data-ttu-id="c4eae-118">Agrupamento da Geração de Recursos</span><span class="sxs-lookup"><span data-stu-id="c4eae-118">Binning Feature Generation</span></span>](#sql-binningfeature)
3. [<span data-ttu-id="c4eae-119">Implantar recursos de saudação de uma única coluna</span><span class="sxs-lookup"><span data-stu-id="c4eae-119">Rolling out hello features from a single column</span></span>](#sql-featurerollout)

> [!NOTE]
> <span data-ttu-id="c4eae-120">Depois de gerar recursos adicionais, você pode adicioná-los como tabela existente de toohello de colunas ou crie uma nova tabela com recursos adicionais de saudação e a chave primária, que pode ser unido a tabela original hello.</span><span class="sxs-lookup"><span data-stu-id="c4eae-120">Once you generate additional features, you can either add them as columns toohello existing table or create a new table with hello additional features and primary key, that can be joined with hello original table.</span></span>
> 
> 

### <span data-ttu-id="c4eae-121"><a name="sql-countfeature"></a>Geração de recursos baseada em contagem</span><span class="sxs-lookup"><span data-stu-id="c4eae-121"><a name="sql-countfeature"></a>Count based Feature Generation</span></span>
<span data-ttu-id="c4eae-122">Este documento demonstra duas maneiras de gerar recursos de contagem.</span><span class="sxs-lookup"><span data-stu-id="c4eae-122">This document demonstrates two ways of generating count features.</span></span> <span data-ttu-id="c4eae-123">Olá primeiro método usa soma condicional e usos de método segundo Olá Olá cláusula 'where'.</span><span class="sxs-lookup"><span data-stu-id="c4eae-123">hello first method uses conditional sum and hello second method uses hello 'where\` clause.</span></span> <span data-ttu-id="c4eae-124">Esses podem ser unidas com hello original (usando colunas de chave primária) toohave contagem recursos de tabela junto com os dados originais hello.</span><span class="sxs-lookup"><span data-stu-id="c4eae-124">These can then be joined with hello original table (using primary key columns) toohave count features alongside hello original data.</span></span>

    select <column_name1>,<column_name2>,<column_name3>, COUNT(*) as Count_Features from <tablename> group by <column_name1>,<column_name2>,<column_name3>

    select <column_name1>,<column_name2> , sum(1) as Count_Features from <tablename>
    where <column_name3> = '<some_value>' group by <column_name1>,<column_name2>

### <span data-ttu-id="c4eae-125"><a name="sql-binningfeature"></a>Agrupamento da Geração de Recursos</span><span class="sxs-lookup"><span data-stu-id="c4eae-125"><a name="sql-binningfeature"></a>Binning Feature Generation</span></span>
<span data-ttu-id="c4eae-126">Olá exemplo a seguir mostra como toogenerate guardado recursos guardando (usando 5 compartimentos) uma coluna numérica que pode ser usada como um recurso em vez disso:</span><span class="sxs-lookup"><span data-stu-id="c4eae-126">hello following example shows how toogenerate binned features by binning (using 5 bins) a numerical column that can be used as a feature instead:</span></span>

    `SELECT <column_name>, NTILE(5) OVER (ORDER BY <column_name>) AS BinNumber from <tablename>`


### <span data-ttu-id="c4eae-127"><a name="sql-featurerollout"></a>Implantar recursos de saudação de uma única coluna</span><span class="sxs-lookup"><span data-stu-id="c4eae-127"><a name="sql-featurerollout"></a>Rolling out hello features from a single column</span></span>
<span data-ttu-id="c4eae-128">Nesta seção, demonstraremos como tooroll em uma única coluna em uma tabela toogenerate adicionais de recursos.</span><span class="sxs-lookup"><span data-stu-id="c4eae-128">In this section, we demonstrate how tooroll-out a single column in a table toogenerate additional features.</span></span> <span data-ttu-id="c4eae-129">exemplo Hello supõe que haja uma coluna de latitude ou longitude na tabela de saudação do qual você está tentando toogenerate recursos.</span><span class="sxs-lookup"><span data-stu-id="c4eae-129">hello example assumes that there is a latitude or longitude column in hello table from which you are trying toogenerate features.</span></span>

<span data-ttu-id="c4eae-130">Aqui está uma breve cartilha sobre os dados de localização de latitude/longitude (recursos de stackoverflow `http://gis.stackexchange.com/questions/8650/how-to-measure-the-accuracy-of-latitude-and-longitude`).</span><span class="sxs-lookup"><span data-stu-id="c4eae-130">Here is a brief primer on latitude/longitude location data (resourced from stackoverflow `http://gis.stackexchange.com/questions/8650/how-to-measure-the-accuracy-of-latitude-and-longitude`).</span></span> <span data-ttu-id="c4eae-131">Isso é útil toounderstand antes de campo de local de saudação featurizing:</span><span class="sxs-lookup"><span data-stu-id="c4eae-131">This is useful toounderstand before featurizing hello location field:</span></span>

* <span data-ttu-id="c4eae-132">entrada de saudação informa se estamos Norte ou Sul, Leste ou oeste no mundo hello.</span><span class="sxs-lookup"><span data-stu-id="c4eae-132">hello sign tells us whether we are north or south, east or west on hello globe.</span></span>
* <span data-ttu-id="c4eae-133">Um dígito em centenas diferente de zero informa que estamos usando longitude, não latitude!</span><span class="sxs-lookup"><span data-stu-id="c4eae-133">A nonzero hundreds digit tells us we're using longitude, not latitude!</span></span>
* <span data-ttu-id="c4eae-134">Dígito Olá dezenas oferece uma posição tooabout 1.000 quilômetros.</span><span class="sxs-lookup"><span data-stu-id="c4eae-134">hello tens digit gives a position tooabout 1,000 kilometers.</span></span> <span data-ttu-id="c4eae-135">Ele nos dá informações úteis sobre em qual continente ou oceano estamos.</span><span class="sxs-lookup"><span data-stu-id="c4eae-135">It gives us useful information about what continent or ocean we are on.</span></span>
* <span data-ttu-id="c4eae-136">Dígito de unidades de saudação (um grau decimal) fornece uma posição para cima too111 quilômetros (60 náuticas milhas, cerca de 69 milhas).</span><span class="sxs-lookup"><span data-stu-id="c4eae-136">hello units digit (one decimal degree) gives a position up too111 kilometers (60 nautical miles, about 69 miles).</span></span> <span data-ttu-id="c4eae-137">Ele pode indicar aproximadamente em qual grande estado ou país estamos.</span><span class="sxs-lookup"><span data-stu-id="c4eae-137">It can tell us roughly what large state or country we are in.</span></span>
* <span data-ttu-id="c4eae-138">Olá primeiro decimal lugar vale backup too11.1 km: ele pode distinguir posição de saudação de uma cidade grande de uma cidade grande vizinha.</span><span class="sxs-lookup"><span data-stu-id="c4eae-138">hello first decimal place is worth up too11.1 km: it can distinguish hello position of one large city from a neighboring large city.</span></span>
* <span data-ttu-id="c4eae-139">casa decimal da segunda Olá vale backup too1.1 km: ele pode separar um Vila dos Olá lado.</span><span class="sxs-lookup"><span data-stu-id="c4eae-139">hello second decimal place is worth up too1.1 km: it can separate one village from hello next.</span></span>
* <span data-ttu-id="c4eae-140">Olá terceiro lugar de decimal é vale a pena too110 m, ele pode identificar um campo agrícola grande ou campus institucional.</span><span class="sxs-lookup"><span data-stu-id="c4eae-140">hello third decimal place is worth up too110 m: it can identify a large agricultural field or institutional campus.</span></span>
* <span data-ttu-id="c4eae-141">casa decimal da quarta Olá é vale a pena m too11: ele pode identificar um pacote de terra.</span><span class="sxs-lookup"><span data-stu-id="c4eae-141">hello fourth decimal place is worth up too11 m: it can identify a parcel of land.</span></span> <span data-ttu-id="c4eae-142">É toohello comparável a precisão típica de uma unidade GPS não corrigida sem interferência.</span><span class="sxs-lookup"><span data-stu-id="c4eae-142">It is comparable toohello typical accuracy of an uncorrected GPS unit with no interference.</span></span>
* <span data-ttu-id="c4eae-143">Olá quinto lugar de decimal é vale a pena o m too1.1: distinguir árvores uns dos outros.</span><span class="sxs-lookup"><span data-stu-id="c4eae-143">hello fifth decimal place is worth up too1.1 m: it distinguish trees from each other.</span></span> <span data-ttu-id="c4eae-144">Nível de toothis de precisão com unidades de GPS comerciais só pode ser obtida com a correção diferencial.</span><span class="sxs-lookup"><span data-stu-id="c4eae-144">Accuracy toothis level with commercial GPS units can only be achieved with differential correction.</span></span>
* <span data-ttu-id="c4eae-145">Olá sexto decimal local é vale a pena m: too0.11 que você pode usar isso para dispor estruturas detalhadamente, para a criação de estruturas, criar estradas.</span><span class="sxs-lookup"><span data-stu-id="c4eae-145">hello sixth decimal place is worth up too0.11 m: you can use this for laying out structures in detail, for designing landscapes, building roads.</span></span> <span data-ttu-id="c4eae-146">Ela é mais do que suficiente para acompanhar os movimentos de geleiras e rios.</span><span class="sxs-lookup"><span data-stu-id="c4eae-146">It should be more than good enough for tracking movements of glaciers and rivers.</span></span> <span data-ttu-id="c4eae-147">Isso pode ser obtido coletando medidas arduamente com o GPS, tais como GPS com correção diferencial.</span><span class="sxs-lookup"><span data-stu-id="c4eae-147">This can be achieved by taking painstaking measures with GPS, such as differentially corrected GPS.</span></span>

<span data-ttu-id="c4eae-148">informações de localização de saudação podem pode ser featurized da seguinte maneira separar região, local e informações de cidade.</span><span class="sxs-lookup"><span data-stu-id="c4eae-148">hello location information can can be featurized as follows, separating out region, location and city information.</span></span> <span data-ttu-id="c4eae-149">Observe que uma vez também pode chamar um ponto de extremidade REST, como a API do Bing Maps disponíveis em `https://msdn.microsoft.com/library/ff701710.aspx` informações de região/Distrito Olá tooget.</span><span class="sxs-lookup"><span data-stu-id="c4eae-149">Note that once can also call a REST end point such as Bing Maps API available at `https://msdn.microsoft.com/library/ff701710.aspx` tooget hello region/district information.</span></span>

    select
        <location_columnname>
        ,round(<location_columnname>,0) as l1        
        ,l2=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 1 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),1,1) else '0' end     
        ,l3=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 2 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),2,1) else '0' end     
        ,l4=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 3 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),3,1) else '0' end     
        ,l5=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 4 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),4,1) else '0' end     
        ,l6=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 5 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),5,1) else '0' end     
        ,l7=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 6 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),6,1) else '0' end     
    from <tablename>

<span data-ttu-id="c4eae-150">Olá acima local baseada em recursos podem ser mais usado toogenerate recursos de contagem adicionais conforme descrito anteriormente.</span><span class="sxs-lookup"><span data-stu-id="c4eae-150">hello above location based features can be further used toogenerate additional count features as described earlier.</span></span>

> [!TIP]
> <span data-ttu-id="c4eae-151">Programaticamente, você pode inserir registros hello usando a linguagem de sua escolha.</span><span class="sxs-lookup"><span data-stu-id="c4eae-151">You can programmatically insert hello records using your language of choice.</span></span> <span data-ttu-id="c4eae-152">Talvez seja necessário tooinsert dados Olá eficiência de gravação partes tooimprove [Check-out exemplo hello como toodo esse usando pyodbc aqui](https://code.google.com/p/pypyodbc/wiki/A_HelloWorld_sample_to_access_mssql_with_python).</span><span class="sxs-lookup"><span data-stu-id="c4eae-152">You may need tooinsert hello data in chunks tooimprove write efficiency [Check out hello example of how toodo this using pyodbc here](https://code.google.com/p/pypyodbc/wiki/A_HelloWorld_sample_to_access_mssql_with_python).</span></span>
> <span data-ttu-id="c4eae-153">Outra alternativa é tooinsert dados Olá banco de dados usando [utilitário BCP](https://msdn.microsoft.com/library/ms162802.aspx)</span><span class="sxs-lookup"><span data-stu-id="c4eae-153">Another alternative is tooinsert data in hello database using [BCP utility](https://msdn.microsoft.com/library/ms162802.aspx)</span></span>
> 
> 

### <span data-ttu-id="c4eae-154"><a name="sql-aml"></a>Conectando tooAzure aprendizado de máquina</span><span class="sxs-lookup"><span data-stu-id="c4eae-154"><a name="sql-aml"></a>Connecting tooAzure Machine Learning</span></span>
<span data-ttu-id="c4eae-155">recurso Olá recentemente gerado pode ser adicionado como uma tabela existente de tooan de coluna ou armazenado em uma nova tabela e Unido Olá a tabela original para o aprendizado de máquina.</span><span class="sxs-lookup"><span data-stu-id="c4eae-155">hello newly generated feature can be added as a column tooan existing table or stored in a new table and joined with hello original table for machine learning.</span></span> <span data-ttu-id="c4eae-156">Recursos podem ser gerados ou acessados se já criou, usando Olá [importar dados](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) módulo no Azure ML, conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="c4eae-156">Features can be generated or accessed if already created, using hello [Import Data](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) module in Azure ML as shown below:</span></span>

![leitores de azureml](./media/machine-learning-data-science-process-sql-server-virtual-machine/reader_db_featurizedinput.png)

## <span data-ttu-id="c4eae-158"><a name="python"></a>Usando uma linguagem de programação como Python</span><span class="sxs-lookup"><span data-stu-id="c4eae-158"><a name="python"></a>Using a programming language like Python</span></span>
<span data-ttu-id="c4eae-159">Usando recursos do Python toogenerate quando dados saudação no SQL Server é dados tooprocessing semelhantes no blob do Azure usando Python, conforme documentado no [dados Blob do Azure de processo em ambiente ciência de dados](machine-learning-data-science-process-data-blob.md).</span><span class="sxs-lookup"><span data-stu-id="c4eae-159">Using Python toogenerate features when hello data is in SQL Server is similar tooprocessing data in Azure blob using Python as documented in [Process Azure Blob data in you data science environment](machine-learning-data-science-process-data-blob.md).</span></span> <span data-ttu-id="c4eae-160">dados de saudação precisa toobe carregado do banco de dados de saudação para um quadro de dados pandas e, em seguida, podem ser processados.</span><span class="sxs-lookup"><span data-stu-id="c4eae-160">hello data needs toobe loaded from hello database into a pandas data frame and then can be processed further.</span></span> <span data-ttu-id="c4eae-161">Documentamos processo Olá de conexão de banco de dados toohello e carregar dados de saudação no quadro de dados Olá nesta seção.</span><span class="sxs-lookup"><span data-stu-id="c4eae-161">We document hello process of connecting toohello database and loading hello data into hello data frame in this section.</span></span>

<span data-ttu-id="c4eae-162">Olá, formato de cadeia de caracteres de conexão a seguir pode ser usado tooconnect tooa banco de dados SQL do Python usando pyodbc (substituir servername, dbname, nome de usuário e senha com valores específicos):</span><span class="sxs-lookup"><span data-stu-id="c4eae-162">hello following connection string format can be used tooconnect tooa SQL Server database from Python using pyodbc (replace servername, dbname, username and password with your specific values):</span></span>

    #Set up hello SQL Azure connection
    import pyodbc
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

<span data-ttu-id="c4eae-163">Olá [biblioteca Pandas](http://pandas.pydata.org/) Python fornece um rico conjunto de ferramentas de análise de dados e estruturas de dados para a manipulação de dados para programação Python.</span><span class="sxs-lookup"><span data-stu-id="c4eae-163">hello [Pandas library](http://pandas.pydata.org/) in Python provides a rich set of data structures and data analysis tools for data manipulation for Python programming.</span></span> <span data-ttu-id="c4eae-164">código de saudação abaixo lê Olá resultados de um banco de dados do SQL Server em um quadro de dados Pandas:</span><span class="sxs-lookup"><span data-stu-id="c4eae-164">hello code below reads hello results returned from a SQL Server database into a Pandas data frame:</span></span>

    # Query database and load hello returned results in pandas data frame
    data_frame = pd.read_sql('''select <columnname1>, <cloumnname2>... from <tablename>''', conn)

<span data-ttu-id="c4eae-165">Agora você pode trabalhar com o quadro de dados Pandas hello como abordadas em tópicos [criar recursos para dados de armazenamento de BLOBs do Azure usando Panda](machine-learning-data-science-create-features-blob.md).</span><span class="sxs-lookup"><span data-stu-id="c4eae-165">Now you can work with hello Pandas data frame as covered in topics [Create features for Azure blob storage data using Panda](machine-learning-data-science-create-features-blob.md).</span></span>

