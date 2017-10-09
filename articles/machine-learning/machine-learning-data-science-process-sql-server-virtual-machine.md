---
title: "aaaExplore dados em uma máquina de virtual do SQL Server no Azure | Microsoft Docs"
description: "Explorar dados e gerar recursos em uma máquina virtual do SQL Server no Azure"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: 
ms.assetid: 3949fb2c-ffab-49fb-908d-27d5e42f743b
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: fashah;garye;bradsev
ms.openlocfilehash: 67f4b058b0f6557ee15fd42795c918d68f1a9871
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <span data-ttu-id="1357b-103"><a name="heading"></a>Processar dados na Máquina Virtual do SQL Server no Azure</span><span class="sxs-lookup"><span data-stu-id="1357b-103"><a name="heading"></a>Process Data in SQL Server Virtual Machine on Azure</span></span>
<span data-ttu-id="1357b-104">Este documento aborda como tooexplore dados e gerar recursos para dados armazenados em uma VM do SQL Server no Azure.</span><span class="sxs-lookup"><span data-stu-id="1357b-104">This document covers how tooexplore data and generate features for data stored in a SQL Server VM on Azure.</span></span> <span data-ttu-id="1357b-105">Isso pode ser feito por disputa de dados usando SQL ou usando uma linguagem de programação como Python.</span><span class="sxs-lookup"><span data-stu-id="1357b-105">This can be done by data wrangling using SQL or by using a programming language like Python.</span></span>

> [!NOTE]
> <span data-ttu-id="1357b-106">instruções de SQL de exemplo Hello neste documento pressupõem que dados estejam no SQL Server.</span><span class="sxs-lookup"><span data-stu-id="1357b-106">hello sample SQL statements in this document assume that data is in SQL Server.</span></span> <span data-ttu-id="1357b-107">Se não for, consulte toohello nuvem dados ciência processo mapa toolearn como toomove seu servidor de tooSQL de dados.</span><span class="sxs-lookup"><span data-stu-id="1357b-107">If it isn't, refer toohello cloud data science process map toolearn how toomove your data tooSQL Server.</span></span>
> 
> 

## <span data-ttu-id="1357b-108"><a name="SQL"></a>Usando o SQL</span><span class="sxs-lookup"><span data-stu-id="1357b-108"><a name="SQL"></a>Using SQL</span></span>
<span data-ttu-id="1357b-109">Descrevemos Olá dados disputa as tarefas nesta seção usando SQL a seguir:</span><span class="sxs-lookup"><span data-stu-id="1357b-109">We describe hello following data wrangling tasks in this section using SQL:</span></span>

1. [<span data-ttu-id="1357b-110">Exploração de Dados</span><span class="sxs-lookup"><span data-stu-id="1357b-110">Data Exploration</span></span>](#sql-dataexploration)
2. [<span data-ttu-id="1357b-111">Geração de Recursos</span><span class="sxs-lookup"><span data-stu-id="1357b-111">Feature Generation</span></span>](#sql-featuregen)

### <span data-ttu-id="1357b-112"><a name="sql-dataexploration"></a>Exploração de Dados</span><span class="sxs-lookup"><span data-stu-id="1357b-112"><a name="sql-dataexploration"></a>Data Exploration</span></span>
<span data-ttu-id="1357b-113">Aqui estão alguns scripts de SQL de exemplo que podem ser usado tooexplore repositórios de dados no SQL Server.</span><span class="sxs-lookup"><span data-stu-id="1357b-113">Here are a few sample SQL scripts that can be used tooexplore data stores in SQL Server.</span></span>

> [!NOTE]
> <span data-ttu-id="1357b-114">Para obter um exemplo prático, você pode usar o hello [NYC táxi dataset](http://www.andresmh.com/nyctaxitrips/) e consulte toohello IPNB intitulada [NYC dados disputa usando o bloco de anotações do IPython e o SQL Server](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) para uma apresentação de ponta a ponta.</span><span class="sxs-lookup"><span data-stu-id="1357b-114">For a practical example, you can use hello [NYC Taxi dataset](http://www.andresmh.com/nyctaxitrips/) and refer toohello IPNB titled [NYC Data wrangling using IPython Notebook and SQL Server](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) for an end-to-end walk-through.</span></span>
> 
> 

1. <span data-ttu-id="1357b-115">Obter a contagem de saudação de observações por dia</span><span class="sxs-lookup"><span data-stu-id="1357b-115">Get hello count of observations per day</span></span>
   
    `SELECT CONVERT(date, <date_columnname>) as date, count(*) as c from <tablename> group by CONVERT(date, <date_columnname>)` 
2. <span data-ttu-id="1357b-116">Obter os níveis de saudação em uma coluna categórica</span><span class="sxs-lookup"><span data-stu-id="1357b-116">Get hello levels in a categorical column</span></span>
   
    `select  distinct <column_name> from <databasename>`
3. <span data-ttu-id="1357b-117">Obter o número de saudação de níveis na combinação de duas colunas categóricas</span><span class="sxs-lookup"><span data-stu-id="1357b-117">Get hello number of levels in combination of two categorical columns</span></span> 
   
    `select <column_a>, <column_b>,count(*) from <tablename> group by <column_a>, <column_b>`
4. <span data-ttu-id="1357b-118">Obter distribuição Olá para colunas numéricas</span><span class="sxs-lookup"><span data-stu-id="1357b-118">Get hello distribution for numerical columns</span></span>
   
    `select <column_name>, count(*) from <tablename> group by <column_name>`

### <span data-ttu-id="1357b-119"><a name="sql-featuregen"></a>Geração de recursos</span><span class="sxs-lookup"><span data-stu-id="1357b-119"><a name="sql-featuregen"></a>Feature Generation</span></span>
<span data-ttu-id="1357b-120">Nesta seção, descrevemos as maneiras de gerar recursos usando SQL:</span><span class="sxs-lookup"><span data-stu-id="1357b-120">In this section, we describe ways of generating features using SQL:</span></span>  

1. [<span data-ttu-id="1357b-121">Geração de recursos baseada em contagem</span><span class="sxs-lookup"><span data-stu-id="1357b-121">Count based Feature Generation</span></span>](#sql-countfeature)
2. [<span data-ttu-id="1357b-122">Agrupamento da Geração de Recursos</span><span class="sxs-lookup"><span data-stu-id="1357b-122">Binning Feature Generation</span></span>](#sql-binningfeature)
3. [<span data-ttu-id="1357b-123">Implantar recursos de saudação de uma única coluna</span><span class="sxs-lookup"><span data-stu-id="1357b-123">Rolling out hello features from a single column</span></span>](#sql-featurerollout)

> [!NOTE]
> <span data-ttu-id="1357b-124">Depois de gerar recursos adicionais, você pode adicioná-los como tabela existente de toohello de colunas ou crie uma nova tabela com recursos adicionais de saudação e a chave primária, que pode ser unido a tabela original hello.</span><span class="sxs-lookup"><span data-stu-id="1357b-124">Once you generate additional features, you can either add them as columns toohello existing table or create a new table with hello additional features and primary key, that can be joined with hello original table.</span></span> 
> 
> 

### <span data-ttu-id="1357b-125"><a name="sql-countfeature"></a>Geração de recursos baseada em contagem</span><span class="sxs-lookup"><span data-stu-id="1357b-125"><a name="sql-countfeature"></a>Count based Feature Generation</span></span>
<span data-ttu-id="1357b-126">Olá exemplos a seguir demonstram duas maneiras de gerar recursos de contagem.</span><span class="sxs-lookup"><span data-stu-id="1357b-126">hello following examples demonstrate two ways of generating count features.</span></span> <span data-ttu-id="1357b-127">Olá primeiro método usa soma condicional e usos de método segundo Olá Olá cláusula 'where'.</span><span class="sxs-lookup"><span data-stu-id="1357b-127">hello first method uses conditional sum and hello second method uses hello 'where' clause.</span></span> <span data-ttu-id="1357b-128">Esses podem ser unidas com hello original (usando colunas de chave primária) toohave contagem recursos de tabela junto com os dados originais hello.</span><span class="sxs-lookup"><span data-stu-id="1357b-128">These can then be joined with hello original table (using primary key columns) toohave count features alongside hello original data.</span></span>

    select <column_name1>,<column_name2>,<column_name3>, COUNT(*) as Count_Features from <tablename> group by <column_name1>,<column_name2>,<column_name3> 

    select <column_name1>,<column_name2> , sum(1) as Count_Features from <tablename> 
    where <column_name3> = '<some_value>' group by <column_name1>,<column_name2> 

### <span data-ttu-id="1357b-129"><a name="sql-binningfeature"></a>Agrupamento da Geração de Recursos</span><span class="sxs-lookup"><span data-stu-id="1357b-129"><a name="sql-binningfeature"></a>Binning Feature Generation</span></span>
<span data-ttu-id="1357b-130">Olá exemplo a seguir mostra como toogenerate guardado recursos guardando (usando cinco compartimentos) uma coluna numérica que pode ser usada como um recurso em vez disso:</span><span class="sxs-lookup"><span data-stu-id="1357b-130">hello following example shows how toogenerate binned features by binning (using five bins) a numerical column that can be used as a feature instead:</span></span>

    `SELECT <column_name>, NTILE(5) OVER (ORDER BY <column_name>) AS BinNumber from <tablename>`


### <span data-ttu-id="1357b-131"><a name="sql-featurerollout"></a>Implantar recursos de saudação de uma única coluna</span><span class="sxs-lookup"><span data-stu-id="1357b-131"><a name="sql-featurerollout"></a>Rolling out hello features from a single column</span></span>
<span data-ttu-id="1357b-132">Nesta seção, demonstraremos como tooroll-out de uma única coluna em uma tabela toogenerate adicionais de recursos.</span><span class="sxs-lookup"><span data-stu-id="1357b-132">In this section, we demonstrate how tooroll out a single column in a table toogenerate additional features.</span></span> <span data-ttu-id="1357b-133">exemplo Hello supõe que haja uma coluna de latitude ou longitude na tabela de saudação do qual você está tentando toogenerate recursos.</span><span class="sxs-lookup"><span data-stu-id="1357b-133">hello example assumes that there is a latitude or longitude column in hello table from which you are trying toogenerate features.</span></span>

<span data-ttu-id="1357b-134">Aqui está uma breve introdução em dados de localização de latitude/longitude (recursos de stackoverflow [como toomeasure Olá precisão de latitude e longitude?](http://gis.stackexchange.com/questions/8650/how-to-measure-the-accuracy-of-latitude-and-longitude)).</span><span class="sxs-lookup"><span data-stu-id="1357b-134">Here is a brief primer on latitude/longitude location data (resourced from stackoverflow [How toomeasure hello accuracy of latitude and longitude?](http://gis.stackexchange.com/questions/8650/how-to-measure-the-accuracy-of-latitude-and-longitude)).</span></span> <span data-ttu-id="1357b-135">Isso é útil toounderstand antes de campo de local de saudação featurizing:</span><span class="sxs-lookup"><span data-stu-id="1357b-135">This is useful toounderstand before featurizing hello location field:</span></span>

* <span data-ttu-id="1357b-136">entrada de saudação informa se estamos Norte ou Sul, Leste ou oeste no mundo hello.</span><span class="sxs-lookup"><span data-stu-id="1357b-136">hello sign tells us whether we are north or south, east or west on hello globe.</span></span>
* <span data-ttu-id="1357b-137">Um dígito em centenas diferente de zero informa que estamos usando longitude, não latitude!</span><span class="sxs-lookup"><span data-stu-id="1357b-137">A nonzero hundreds digit tells us that we're using longitude, not latitude!</span></span>
* <span data-ttu-id="1357b-138">Dígito Olá dezenas oferece uma posição tooabout 1.000 quilômetros.</span><span class="sxs-lookup"><span data-stu-id="1357b-138">hello tens digit gives a position tooabout 1,000 kilometers.</span></span> <span data-ttu-id="1357b-139">Ele nos dá informações úteis sobre em qual continente ou oceano estamos.</span><span class="sxs-lookup"><span data-stu-id="1357b-139">It gives us useful information about what continent or ocean we are on.</span></span>
* <span data-ttu-id="1357b-140">Dígito de unidades de saudação (um grau decimal) fornece uma posição para cima too111 quilômetros (60 náuticas milhas, cerca de 69 milhas).</span><span class="sxs-lookup"><span data-stu-id="1357b-140">hello units digit (one decimal degree) gives a position up too111 kilometers (60 nautical miles, about 69 miles).</span></span> <span data-ttu-id="1357b-141">Ele pode indicar aproximadamente em qual grande estado ou país estamos.</span><span class="sxs-lookup"><span data-stu-id="1357b-141">It can tell us roughly what large state or country we are in.</span></span>
* <span data-ttu-id="1357b-142">Olá primeiro decimal lugar vale backup too11.1 km: ele pode distinguir posição de saudação de uma cidade grande de uma cidade grande vizinha.</span><span class="sxs-lookup"><span data-stu-id="1357b-142">hello first decimal place is worth up too11.1 km: it can distinguish hello position of one large city from a neighboring large city.</span></span>
* <span data-ttu-id="1357b-143">casa decimal da segunda Olá vale backup too1.1 km: ele pode separar um Vila dos Olá lado.</span><span class="sxs-lookup"><span data-stu-id="1357b-143">hello second decimal place is worth up too1.1 km: it can separate one village from hello next.</span></span>
* <span data-ttu-id="1357b-144">Olá terceiro lugar de decimal é vale a pena too110 m, ele pode identificar um campo agrícola grande ou campus institucional.</span><span class="sxs-lookup"><span data-stu-id="1357b-144">hello third decimal place is worth up too110 m: it can identify a large agricultural field or institutional campus.</span></span>
* <span data-ttu-id="1357b-145">casa decimal da quarta Olá é vale a pena m too11: ele pode identificar um pacote de terra.</span><span class="sxs-lookup"><span data-stu-id="1357b-145">hello fourth decimal place is worth up too11 m: it can identify a parcel of land.</span></span> <span data-ttu-id="1357b-146">É toohello comparável a precisão típica de uma unidade GPS não corrigida sem interferência.</span><span class="sxs-lookup"><span data-stu-id="1357b-146">It is comparable toohello typical accuracy of an uncorrected GPS unit with no interference.</span></span>
* <span data-ttu-id="1357b-147">Olá quinto decimal é vale a pena o m too1.1: faz distinção árvores uns dos outros.</span><span class="sxs-lookup"><span data-stu-id="1357b-147">hello fifth decimal place is worth up too1.1 m: it distinguishes trees from each other.</span></span> <span data-ttu-id="1357b-148">Nível de toothis de precisão com unidades de GPS comerciais só pode ser obtida com a correção diferencial.</span><span class="sxs-lookup"><span data-stu-id="1357b-148">Accuracy toothis level with commercial GPS units can only be achieved with differential correction.</span></span>
* <span data-ttu-id="1357b-149">Olá sexto decimal local é vale a pena m: too0.11 que você pode usar isso para dispor estruturas detalhadamente, para a criação de estruturas, criar estradas.</span><span class="sxs-lookup"><span data-stu-id="1357b-149">hello sixth decimal place is worth up too0.11 m: you can use this for laying out structures in detail, for designing landscapes, building roads.</span></span> <span data-ttu-id="1357b-150">Ela é mais do que suficiente para acompanhar os movimentos de geleiras e rios.</span><span class="sxs-lookup"><span data-stu-id="1357b-150">It should be more than good enough for tracking movements of glaciers and rivers.</span></span> <span data-ttu-id="1357b-151">Isso pode ser obtido coletando medidas arduamente com o GPS, tais como GPS com correção diferencial.</span><span class="sxs-lookup"><span data-stu-id="1357b-151">This can be achieved by taking painstaking measures with GPS, such as differentially corrected GPS.</span></span>

<span data-ttu-id="1357b-152">informações de local de saudação podem ser featurized da seguinte maneira separar região, local e informações de cidade.</span><span class="sxs-lookup"><span data-stu-id="1357b-152">hello location information can be featurized as follows, separating out region, location, and city information.</span></span> <span data-ttu-id="1357b-153">Observe que você também pode chamar um ponto de extremidade REST, como a API do Bing Maps disponível em [encontrar um local pelo ponto](https://msdn.microsoft.com/library/ff701710.aspx) tooget informações de região/Distrito de saudação.</span><span class="sxs-lookup"><span data-stu-id="1357b-153">Note that you can also call a REST end point such as Bing Maps API available at [Find a Location by Point](https://msdn.microsoft.com/library/ff701710.aspx) tooget hello region/district information.</span></span>

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

<span data-ttu-id="1357b-154">Esses recursos com base no local podem ser ainda mais recursos de contagem adicionais toogenerate usado conforme descrito anteriormente.</span><span class="sxs-lookup"><span data-stu-id="1357b-154">These location-based features can be further used toogenerate additional count features as described earlier.</span></span> 

> [!TIP]
> <span data-ttu-id="1357b-155">Programaticamente, você pode inserir registros hello usando a linguagem de sua escolha.</span><span class="sxs-lookup"><span data-stu-id="1357b-155">You can programmatically insert hello records using your language of choice.</span></span> <span data-ttu-id="1357b-156">Talvez seja necessário tooinsert dados Olá eficiência de gravação de tooimprove partes (para obter um exemplo de como toodo esse usando pyodbc, consulte [tooaccess de exemplo de HelloWorld um SQL Server com python](https://code.google.com/p/pypyodbc/wiki/A_HelloWorld_sample_to_access_mssql_with_python)).</span><span class="sxs-lookup"><span data-stu-id="1357b-156">You may need tooinsert hello data in chunks tooimprove write efficiency (for an example of how toodo this using pyodbc, see [A HelloWorld sample tooaccess SQLServer with python](https://code.google.com/p/pypyodbc/wiki/A_HelloWorld_sample_to_access_mssql_with_python)).</span></span> <span data-ttu-id="1357b-157">Outra alternativa é tooinsert dados no banco de dados de saudação usando Olá [utilitário BCP](https://msdn.microsoft.com/library/ms162802.aspx).</span><span class="sxs-lookup"><span data-stu-id="1357b-157">Another alternative is tooinsert data in hello database using hello [BCP utility](https://msdn.microsoft.com/library/ms162802.aspx).</span></span>
> 
> 

### <span data-ttu-id="1357b-158"><a name="sql-aml"></a>Conectando tooAzure aprendizado de máquina</span><span class="sxs-lookup"><span data-stu-id="1357b-158"><a name="sql-aml"></a>Connecting tooAzure Machine Learning</span></span>
<span data-ttu-id="1357b-159">recurso Olá recentemente gerado pode ser adicionado como uma tabela existente de tooan de coluna ou armazenado em uma nova tabela e Unido Olá a tabela original para o aprendizado de máquina.</span><span class="sxs-lookup"><span data-stu-id="1357b-159">hello newly generated feature can be added as a column tooan existing table or stored in a new table and joined with hello original table for machine learning.</span></span> <span data-ttu-id="1357b-160">Recursos podem ser gerados ou acessados se já criou, usando Olá [importar dados] [ import-data] módulo no aprendizado de máquina do Azure conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="1357b-160">Features can be generated or accessed if already created, using hello [Import Data][import-data] module in Azure Machine Learning as shown below:</span></span>

![leitores de azureml][1] 

## <span data-ttu-id="1357b-162"><a name="python"></a>Usando uma linguagem de programação como Python</span><span class="sxs-lookup"><span data-stu-id="1357b-162"><a name="python"></a>Using a programming language like Python</span></span>
<span data-ttu-id="1357b-163">Usando dados de tooexplore Python e gerar recursos quando Olá são de dados no SQL Server é dados tooprocessing semelhantes no blob do Azure usando Python, conforme documentado no [dados de Blob do Azure de processo em seu ambiente de ciência de dados](machine-learning-data-science-process-data-blob.md).</span><span class="sxs-lookup"><span data-stu-id="1357b-163">Using Python tooexplore data and generate features when hello data is in SQL Server is similar tooprocessing data in Azure blob using Python as documented in [Process Azure Blob data in your data science environment](machine-learning-data-science-process-data-blob.md).</span></span> <span data-ttu-id="1357b-164">dados de saudação precisa toobe carregado do banco de dados de saudação para um quadro de dados pandas e, em seguida, podem ser processados.</span><span class="sxs-lookup"><span data-stu-id="1357b-164">hello data needs toobe loaded from hello database into a pandas data frame and then can be processed further.</span></span> <span data-ttu-id="1357b-165">Documentamos processo Olá de conexão de banco de dados toohello e carregar dados de saudação no quadro de dados Olá nesta seção.</span><span class="sxs-lookup"><span data-stu-id="1357b-165">We document hello process of connecting toohello database and loading hello data into hello data frame in this section.</span></span>

<span data-ttu-id="1357b-166">Olá, formato de cadeia de caracteres de conexão a seguir pode ser usado tooconnect tooa banco de dados SQL do Python usando pyodbc (substituir servername, dbname, nome de usuário e senha com valores específicos):</span><span class="sxs-lookup"><span data-stu-id="1357b-166">hello following connection string format can be used tooconnect tooa SQL Server database from Python using pyodbc (replace servername, dbname, username, and password with your specific values):</span></span>

    #Set up hello SQL Azure connection
    import pyodbc    
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

<span data-ttu-id="1357b-167">Olá [biblioteca Pandas](http://pandas.pydata.org/) Python fornece um rico conjunto de ferramentas de análise de dados e estruturas de dados para a manipulação de dados para programação Python.</span><span class="sxs-lookup"><span data-stu-id="1357b-167">hello [Pandas library](http://pandas.pydata.org/) in Python provides a rich set of data structures and data analysis tools for data manipulation for Python programming.</span></span> <span data-ttu-id="1357b-168">código de saudação abaixo lê Olá resultados de um banco de dados do SQL Server em um quadro de dados Pandas:</span><span class="sxs-lookup"><span data-stu-id="1357b-168">hello code below reads hello results returned from a SQL Server database into a Pandas data frame:</span></span>

    # Query database and load hello returned results in pandas data frame
    data_frame = pd.read_sql('''select <columnname1>, <cloumnname2>... from <tablename>''', conn)

<span data-ttu-id="1357b-169">Agora você pode trabalhar com o quadro de dados Pandas Olá conforme abordado no artigo Olá [dados de Blob do Azure de processo em seu ambiente de ciência de dados](machine-learning-data-science-process-data-blob.md).</span><span class="sxs-lookup"><span data-stu-id="1357b-169">Now you can work with hello Pandas data frame as covered in hello article [Process Azure Blob data in your data science environment](machine-learning-data-science-process-data-blob.md).</span></span>

## <a name="azure-data-science-in-action-example"></a><span data-ttu-id="1357b-170">Exemplo da Ciência de Dados do Azure em Ação</span><span class="sxs-lookup"><span data-stu-id="1357b-170">Azure Data Science in Action Example</span></span>
<span data-ttu-id="1357b-171">Para obter um exemplo passo a passo de ponta a ponta do processo de ciência de dados do Azure usando um conjunto de dados público de saudação, consulte [processo de ciência de dados do Azure em ação](machine-learning-data-science-process-sql-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="1357b-171">For an end-to-end walkthrough example of hello Azure Data Science Process using a public dataset, see [Azure Data Science Process in Action](machine-learning-data-science-process-sql-walkthrough.md).</span></span>

[1]: ./media/machine-learning-data-science-process-sql-server-virtual-machine/reader_db_featurizedinput.png


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/

