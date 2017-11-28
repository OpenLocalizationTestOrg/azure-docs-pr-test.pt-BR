---
title: "Explorar dados na máquina virtual do SQL Server no Azure | Microsoft Docs"
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
ms.openlocfilehash: 16fabb29bdc8ec770efd843e18e9016e338a8f4e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <span data-ttu-id="c679f-103"><a name="heading"></a>Processar dados na Máquina Virtual do SQL Server no Azure</span><span class="sxs-lookup"><span data-stu-id="c679f-103"><a name="heading"></a>Process Data in SQL Server Virtual Machine on Azure</span></span>
<span data-ttu-id="c679f-104">Este documento aborda como explorar dados e gerar recursos dados armazenados em uma VM do SQL Server no Azure.</span><span class="sxs-lookup"><span data-stu-id="c679f-104">This document covers how to explore data and generate features for data stored in a SQL Server VM on Azure.</span></span> <span data-ttu-id="c679f-105">Isso pode ser feito por disputa de dados usando SQL ou usando uma linguagem de programação como Python.</span><span class="sxs-lookup"><span data-stu-id="c679f-105">This can be done by data wrangling using SQL or by using a programming language like Python.</span></span>

> [!NOTE]
> <span data-ttu-id="c679f-106">As instruções SQL de exemplo neste documento pressupõem que os dados estão no SQL Server.</span><span class="sxs-lookup"><span data-stu-id="c679f-106">The sample SQL statements in this document assume that data is in SQL Server.</span></span> <span data-ttu-id="c679f-107">Se não estiverem, consulte o mapa do processo de ciência de dados de nuvem para aprender a mover seus dados para o SQL Server.</span><span class="sxs-lookup"><span data-stu-id="c679f-107">If it isn't, refer to the cloud data science process map to learn how to move your data to SQL Server.</span></span>
> 
> 

## <span data-ttu-id="c679f-108"><a name="SQL"></a>Usando o SQL</span><span class="sxs-lookup"><span data-stu-id="c679f-108"><a name="SQL"></a>Using SQL</span></span>
<span data-ttu-id="c679f-109">Descrevemos as seguintes tarefas wrangling de dados nesta seção usando SQL:</span><span class="sxs-lookup"><span data-stu-id="c679f-109">We describe the following data wrangling tasks in this section using SQL:</span></span>

1. [<span data-ttu-id="c679f-110">Exploração de Dados</span><span class="sxs-lookup"><span data-stu-id="c679f-110">Data Exploration</span></span>](#sql-dataexploration)
2. [<span data-ttu-id="c679f-111">Geração de Recursos</span><span class="sxs-lookup"><span data-stu-id="c679f-111">Feature Generation</span></span>](#sql-featuregen)

### <span data-ttu-id="c679f-112"><a name="sql-dataexploration"></a>Exploração de Dados</span><span class="sxs-lookup"><span data-stu-id="c679f-112"><a name="sql-dataexploration"></a>Data Exploration</span></span>
<span data-ttu-id="c679f-113">Aqui estão alguns scripts de SQL de exemplo que podem ser usados para explorar armazenamentos de dados no SQL Server.</span><span class="sxs-lookup"><span data-stu-id="c679f-113">Here are a few sample SQL scripts that can be used to explore data stores in SQL Server.</span></span>

> [!NOTE]
> <span data-ttu-id="c679f-114">Para ver um exemplo prático, é possível usar o [conjunto de dados de Táxis de NYC](http://www.andresmh.com/nyctaxitrips/) e consultar o IPNB intitulado[NYC Data wrangling using IPython Notebook and SQL Server (Realizar o wrangling de dados de NYC usando o IPython Notebook e SQL Server)](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) para obter um passo a passo de ponta a ponta.</span><span class="sxs-lookup"><span data-stu-id="c679f-114">For a practical example, you can use the [NYC Taxi dataset](http://www.andresmh.com/nyctaxitrips/) and refer to the IPNB titled [NYC Data wrangling using IPython Notebook and SQL Server](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) for an end-to-end walk-through.</span></span>
> 
> 

1. <span data-ttu-id="c679f-115">Obter a contagem de observações por dia</span><span class="sxs-lookup"><span data-stu-id="c679f-115">Get the count of observations per day</span></span>
   
    `SELECT CONVERT(date, <date_columnname>) as date, count(*) as c from <tablename> group by CONVERT(date, <date_columnname>)` 
2. <span data-ttu-id="c679f-116">Obter os níveis em uma coluna categórica</span><span class="sxs-lookup"><span data-stu-id="c679f-116">Get the levels in a categorical column</span></span>
   
    `select  distinct <column_name> from <databasename>`
3. <span data-ttu-id="c679f-117">Obter o número de níveis na combinação de duas colunas categóricas</span><span class="sxs-lookup"><span data-stu-id="c679f-117">Get the number of levels in combination of two categorical columns</span></span> 
   
    `select <column_a>, <column_b>,count(*) from <tablename> group by <column_a>, <column_b>`
4. <span data-ttu-id="c679f-118">Obter a distribuição de colunas numéricas</span><span class="sxs-lookup"><span data-stu-id="c679f-118">Get the distribution for numerical columns</span></span>
   
    `select <column_name>, count(*) from <tablename> group by <column_name>`

### <span data-ttu-id="c679f-119"><a name="sql-featuregen"></a>Geração de Recursos</span><span class="sxs-lookup"><span data-stu-id="c679f-119"><a name="sql-featuregen"></a>Feature Generation</span></span>
<span data-ttu-id="c679f-120">Nesta seção, descrevemos as maneiras de gerar recursos usando SQL:</span><span class="sxs-lookup"><span data-stu-id="c679f-120">In this section, we describe ways of generating features using SQL:</span></span>  

1. [<span data-ttu-id="c679f-121">Geração de recursos baseada em contagem</span><span class="sxs-lookup"><span data-stu-id="c679f-121">Count based Feature Generation</span></span>](#sql-countfeature)
2. [<span data-ttu-id="c679f-122">Agrupamento da Geração de Recursos</span><span class="sxs-lookup"><span data-stu-id="c679f-122">Binning Feature Generation</span></span>](#sql-binningfeature)
3. [<span data-ttu-id="c679f-123">Propagar os recursos de uma única coluna</span><span class="sxs-lookup"><span data-stu-id="c679f-123">Rolling out the features from a single column</span></span>](#sql-featurerollout)

> [!NOTE]
> <span data-ttu-id="c679f-124">Depois de gerar recursos adicionais, você pode adicioná-los como colunas à tabela existente ou criar uma nova tabela com os recursos adicionais e a chave primária, que pode ser unida com a tabela original.</span><span class="sxs-lookup"><span data-stu-id="c679f-124">Once you generate additional features, you can either add them as columns to the existing table or create a new table with the additional features and primary key, that can be joined with the original table.</span></span> 
> 
> 

### <span data-ttu-id="c679f-125"><a name="sql-countfeature"></a>Geração de recursos baseada em contagem</span><span class="sxs-lookup"><span data-stu-id="c679f-125"><a name="sql-countfeature"></a>Count based Feature Generation</span></span>
<span data-ttu-id="c679f-126">Os exemplos a seguir demonstram duas maneiras de gerar recursos de contagem.</span><span class="sxs-lookup"><span data-stu-id="c679f-126">The following examples demonstrate two ways of generating count features.</span></span> <span data-ttu-id="c679f-127">O primeiro método usa a soma condicional e o segundo usa a cláusula 'where'.</span><span class="sxs-lookup"><span data-stu-id="c679f-127">The first method uses conditional sum and the second method uses the 'where' clause.</span></span> <span data-ttu-id="c679f-128">Eles podem então ser unidos à tabela original (usando colunas de chave primária) para que os recursos de contagem fiquem junto com os dados originais.</span><span class="sxs-lookup"><span data-stu-id="c679f-128">These can then be joined with the original table (using primary key columns) to have count features alongside the original data.</span></span>

    select <column_name1>,<column_name2>,<column_name3>, COUNT(*) as Count_Features from <tablename> group by <column_name1>,<column_name2>,<column_name3> 

    select <column_name1>,<column_name2> , sum(1) as Count_Features from <tablename> 
    where <column_name3> = '<some_value>' group by <column_name1>,<column_name2> 

### <span data-ttu-id="c679f-129"><a name="sql-binningfeature"></a>Agrupamento da Geração de Recursos</span><span class="sxs-lookup"><span data-stu-id="c679f-129"><a name="sql-binningfeature"></a>Binning Feature Generation</span></span>
<span data-ttu-id="c679f-130">O exemplo a seguir mostra como gerar recursos compartimentalizados guardando (usando cinco compartimentos) uma coluna numérica que poderá ser usada como um recurso:</span><span class="sxs-lookup"><span data-stu-id="c679f-130">The following example shows how to generate binned features by binning (using five bins) a numerical column that can be used as a feature instead:</span></span>

    `SELECT <column_name>, NTILE(5) OVER (ORDER BY <column_name>) AS BinNumber from <tablename>`


### <span data-ttu-id="c679f-131"><a name="sql-featurerollout"></a>Propagar os recursos de uma única coluna</span><span class="sxs-lookup"><span data-stu-id="c679f-131"><a name="sql-featurerollout"></a>Rolling out the features from a single column</span></span>
<span data-ttu-id="c679f-132">Nesta seção, demonstraremos como propagar uma única coluna em uma tabela para gerar recursos adicionais.</span><span class="sxs-lookup"><span data-stu-id="c679f-132">In this section, we demonstrate how to roll out a single column in a table to generate additional features.</span></span> <span data-ttu-id="c679f-133">O exemplo presume que há uma coluna de latitude ou longitude na tabela da qual você está tentando gerar recursos.</span><span class="sxs-lookup"><span data-stu-id="c679f-133">The example assumes that there is a latitude or longitude column in the table from which you are trying to generate features.</span></span>

<span data-ttu-id="c679f-134">Apresentamos aqui uma breve cartilha sobre dados de localização de latitude/longitude (extraídos de [How to measure the accuracy of latitude and longitude?](http://gis.stackexchange.com/questions/8650/how-to-measure-the-accuracy-of-latitude-and-longitude)[Como medir a precisão de latitude e longitude?] do StackOverflow).</span><span class="sxs-lookup"><span data-stu-id="c679f-134">Here is a brief primer on latitude/longitude location data (resourced from stackoverflow [How to measure the accuracy of latitude and longitude?](http://gis.stackexchange.com/questions/8650/how-to-measure-the-accuracy-of-latitude-and-longitude)).</span></span> <span data-ttu-id="c679f-135">É útil entender isso antes de destacar o campo local:</span><span class="sxs-lookup"><span data-stu-id="c679f-135">This is useful to understand before featurizing the location field:</span></span>

* <span data-ttu-id="c679f-136">O sinal nos informa se estamos na parte norte ou sul, leste ou oeste do globo.</span><span class="sxs-lookup"><span data-stu-id="c679f-136">The sign tells us whether we are north or south, east or west on the globe.</span></span>
* <span data-ttu-id="c679f-137">Um dígito em centenas diferente de zero informa que estamos usando longitude, não latitude!</span><span class="sxs-lookup"><span data-stu-id="c679f-137">A nonzero hundreds digit tells us that we're using longitude, not latitude!</span></span>
* <span data-ttu-id="c679f-138">O dígito de dezena indica uma posição de cerca de 1.000 quilômetros.</span><span class="sxs-lookup"><span data-stu-id="c679f-138">The tens digit gives a position to about 1,000 kilometers.</span></span> <span data-ttu-id="c679f-139">Ele nos dá informações úteis sobre em qual continente ou oceano estamos.</span><span class="sxs-lookup"><span data-stu-id="c679f-139">It gives us useful information about what continent or ocean we are on.</span></span>
* <span data-ttu-id="c679f-140">O dígito e unidades (um grau decimal) oferece uma posição até 111 quilômetros (60 milhas náuticas, cerca de 69 milhas).</span><span class="sxs-lookup"><span data-stu-id="c679f-140">The units digit (one decimal degree) gives a position up to 111 kilometers (60 nautical miles, about 69 miles).</span></span> <span data-ttu-id="c679f-141">Ele pode indicar aproximadamente em qual grande estado ou país estamos.</span><span class="sxs-lookup"><span data-stu-id="c679f-141">It can tell us roughly what large state or country we are in.</span></span>
* <span data-ttu-id="c679f-142">A primeira casa decimal representa até 11,1 km: ela pode distinguir a posição de uma cidade grande de uma cidade grande vizinha.</span><span class="sxs-lookup"><span data-stu-id="c679f-142">The first decimal place is worth up to 11.1 km: it can distinguish the position of one large city from a neighboring large city.</span></span>
* <span data-ttu-id="c679f-143">A segunda casa decimal representa 1,1 km: ela pode separar um vila da próxima.</span><span class="sxs-lookup"><span data-stu-id="c679f-143">The second decimal place is worth up to 1.1 km: it can separate one village from the next.</span></span>
* <span data-ttu-id="c679f-144">A terceira casa decimal representa até 110 m: ela pode identificar um campo agrícola ou campus institucional grande.</span><span class="sxs-lookup"><span data-stu-id="c679f-144">The third decimal place is worth up to 110 m: it can identify a large agricultural field or institutional campus.</span></span>
* <span data-ttu-id="c679f-145">A quarta casa decimal representa até 11 m: ela pode identificar um lote de terreno.</span><span class="sxs-lookup"><span data-stu-id="c679f-145">The fourth decimal place is worth up to 11 m: it can identify a parcel of land.</span></span> <span data-ttu-id="c679f-146">Ela é comparável à precisão típica de uma unidade GPS não corrigida sem interferência.</span><span class="sxs-lookup"><span data-stu-id="c679f-146">It is comparable to the typical accuracy of an uncorrected GPS unit with no interference.</span></span>
* <span data-ttu-id="c679f-147">A quinta casa decimal representa até 1,1 m: ela distingue as árvores umas das outras.</span><span class="sxs-lookup"><span data-stu-id="c679f-147">The fifth decimal place is worth up to 1.1 m: it distinguishes trees from each other.</span></span> <span data-ttu-id="c679f-148">Uma precisão desse nível com unidades GPS comerciais só pode ser obtida com a correção diferencial.</span><span class="sxs-lookup"><span data-stu-id="c679f-148">Accuracy to this level with commercial GPS units can only be achieved with differential correction.</span></span>
* <span data-ttu-id="c679f-149">A sexta casa decimal representa até 0,11 m: você pode usá-la para dispor estruturas detalhadamente, projetar paisagens e criar estradas.</span><span class="sxs-lookup"><span data-stu-id="c679f-149">The sixth decimal place is worth up to 0.11 m: you can use this for laying out structures in detail, for designing landscapes, building roads.</span></span> <span data-ttu-id="c679f-150">Ela é mais do que suficiente para acompanhar os movimentos de geleiras e rios.</span><span class="sxs-lookup"><span data-stu-id="c679f-150">It should be more than good enough for tracking movements of glaciers and rivers.</span></span> <span data-ttu-id="c679f-151">Isso pode ser obtido coletando medidas arduamente com o GPS, tais como GPS com correção diferencial.</span><span class="sxs-lookup"><span data-stu-id="c679f-151">This can be achieved by taking painstaking measures with GPS, such as differentially corrected GPS.</span></span>

<span data-ttu-id="c679f-152">As informações de local podem ser destacadas da maneira indicada a seguir, separando as informações de região, local e cidade.</span><span class="sxs-lookup"><span data-stu-id="c679f-152">The location information can be featurized as follows, separating out region, location, and city information.</span></span> <span data-ttu-id="c679f-153">Observe que também é possível chamar um ponto de extremidade REST tal como a API do Bing Mapas disponível em [Find a Location by Point](https://msdn.microsoft.com/library/ff701710.aspx) (Encontrar um local por ponto) para obter as informações de região/distrito.</span><span class="sxs-lookup"><span data-stu-id="c679f-153">Note that you can also call a REST end point such as Bing Maps API available at [Find a Location by Point](https://msdn.microsoft.com/library/ff701710.aspx) to get the region/district information.</span></span>

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

<span data-ttu-id="c679f-154">Os recursos baseados em localização podem ser usados ainda para gerar recursos adicionais de contagem, como descrito anteriormente.</span><span class="sxs-lookup"><span data-stu-id="c679f-154">These location-based features can be further used to generate additional count features as described earlier.</span></span> 

> [!TIP]
> <span data-ttu-id="c679f-155">É possível inserir os registros com programação usando a linguagem de sua escolha.</span><span class="sxs-lookup"><span data-stu-id="c679f-155">You can programmatically insert the records using your language of choice.</span></span> <span data-ttu-id="c679f-156">Talvez seja necessário inserir os dados em partes para melhorar a eficiência de gravação (para obter um exemplo de como fazer isso usando o pyodbc, veja [A HelloWorld sample to access SQLServer with python](https://code.google.com/p/pypyodbc/wiki/A_HelloWorld_sample_to_access_mssql_with_python)[Uma amostra do HelloWorld para acessar o SQL Server com o Python]).</span><span class="sxs-lookup"><span data-stu-id="c679f-156">You may need to insert the data in chunks to improve write efficiency (for an example of how to do this using pyodbc, see [A HelloWorld sample to access SQLServer with python](https://code.google.com/p/pypyodbc/wiki/A_HelloWorld_sample_to_access_mssql_with_python)).</span></span> <span data-ttu-id="c679f-157">Outra alternativa é inserir dados no banco de dados usando o [utilitário BCP](https://msdn.microsoft.com/library/ms162802.aspx).</span><span class="sxs-lookup"><span data-stu-id="c679f-157">Another alternative is to insert data in the database using the [BCP utility](https://msdn.microsoft.com/library/ms162802.aspx).</span></span>
> 
> 

### <span data-ttu-id="c679f-158">
            <a name="sql-aml">
            </a>Conectando ao Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="c679f-158"><a name="sql-aml"></a>Connecting to Azure Machine Learning</span></span>
<span data-ttu-id="c679f-159">O recurso recém-gerado pode ser adicionado como uma coluna a uma tabela existente ou armazenado em uma nova tabela e unido com a tabela original para o aprendizado de máquina.</span><span class="sxs-lookup"><span data-stu-id="c679f-159">The newly generated feature can be added as a column to an existing table or stored in a new table and joined with the original table for machine learning.</span></span> <span data-ttu-id="c679f-160">Os recursos podem ser gerados ou acessados, se já foram criados, usando o módulo [Importar Dados][import-data] no Azure Machine Learning, conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="c679f-160">Features can be generated or accessed if already created, using the [Import Data][import-data] module in Azure Machine Learning as shown below:</span></span>

![leitores de azureml][1] 

## <span data-ttu-id="c679f-162"><a name="python"></a>Usando uma linguagem de programação como Python</span><span class="sxs-lookup"><span data-stu-id="c679f-162"><a name="python"></a>Using a programming language like Python</span></span>
<span data-ttu-id="c679f-163">Usar o Python para explorar dados e gerar recursos quando os dados estão no SQL Server é semelhante a processar dados no blob do Azure usando o Python, conforme documentado em [Processar dados de Blobs do Azure no ambiente de ciência de dados](machine-learning-data-science-process-data-blob.md).</span><span class="sxs-lookup"><span data-stu-id="c679f-163">Using Python to explore data and generate features when the data is in SQL Server is similar to processing data in Azure blob using Python as documented in [Process Azure Blob data in your data science environment](machine-learning-data-science-process-data-blob.md).</span></span> <span data-ttu-id="c679f-164">Os dados precisam ser carregados do banco de dados para um quadro de dados pandas, quando então poderão ser processados.</span><span class="sxs-lookup"><span data-stu-id="c679f-164">The data needs to be loaded from the database into a pandas data frame and then can be processed further.</span></span> <span data-ttu-id="c679f-165">Documentamos o processo de conectar-se ao banco de dados e carregar os dados em um quadro de dados nesta seção.</span><span class="sxs-lookup"><span data-stu-id="c679f-165">We document the process of connecting to the database and loading the data into the data frame in this section.</span></span>

<span data-ttu-id="c679f-166">O seguinte formato de cadeia de conexão pode ser usado para se conectar a um banco de dados do SQL Server do Python usando pyodbc (substitua servername, dbname, username e password pelos seus valores específicos):</span><span class="sxs-lookup"><span data-stu-id="c679f-166">The following connection string format can be used to connect to a SQL Server database from Python using pyodbc (replace servername, dbname, username, and password with your specific values):</span></span>

    #Set up the SQL Azure connection
    import pyodbc    
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

<span data-ttu-id="c679f-167">A [Biblioteca Pandas](http://pandas.pydata.org/) no Python fornece um conjunto avançado de estruturas de dados e ferramentas de análise de dados para manipulação de dados para a programação Python.</span><span class="sxs-lookup"><span data-stu-id="c679f-167">The [Pandas library](http://pandas.pydata.org/) in Python provides a rich set of data structures and data analysis tools for data manipulation for Python programming.</span></span> <span data-ttu-id="c679f-168">O código a seguir lê os resultados retornados de um banco de dados do SQL Server em um quadro de dados Pandas:</span><span class="sxs-lookup"><span data-stu-id="c679f-168">The code below reads the results returned from a SQL Server database into a Pandas data frame:</span></span>

    # Query database and load the returned results in pandas data frame
    data_frame = pd.read_sql('''select <columnname1>, <cloumnname2>... from <tablename>''', conn)

<span data-ttu-id="c679f-169">Agora, você pode trabalhar com o quadro de dados do Pandas, como abordamos no artigo [Processar dados do Blob do Azure no ambiente de ciência de dados](machine-learning-data-science-process-data-blob.md).</span><span class="sxs-lookup"><span data-stu-id="c679f-169">Now you can work with the Pandas data frame as covered in the article [Process Azure Blob data in your data science environment](machine-learning-data-science-process-data-blob.md).</span></span>

## <a name="azure-data-science-in-action-example"></a><span data-ttu-id="c679f-170">Exemplo da Ciência de Dados do Azure em Ação</span><span class="sxs-lookup"><span data-stu-id="c679f-170">Azure Data Science in Action Example</span></span>
<span data-ttu-id="c679f-171">Para obter um exemplo passo a passo e ponta a ponta do Processo de Ciência de Dados do Azure usando um conjunto de dados público, consulte [Processo de Ciência de Dados do Azure em Ação](machine-learning-data-science-process-sql-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="c679f-171">For an end-to-end walkthrough example of the Azure Data Science Process using a public dataset, see [Azure Data Science Process in Action](machine-learning-data-science-process-sql-walkthrough.md).</span></span>

[1]: ./media/machine-learning-data-science-process-sql-server-virtual-machine/reader_db_featurizedinput.png


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/

