---
title: Criar recursos para dados no SQL Server usando o SQL e o Python | Microsoft Docs
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
ms.openlocfilehash: f0ac2799e2d8f18b2dd5b633555bfca08a44ba27
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="create-features-for-data-in-sql-server-using-sql-and-python"></a><span data-ttu-id="0cfc5-103">Criar recursos para dados no SQL Server usando o SQL e o Python</span><span class="sxs-lookup"><span data-stu-id="0cfc5-103">Create features for data in SQL Server using SQL and Python</span></span>
<span data-ttu-id="0cfc5-104">Este documento mostra como gerar recursos para os dados armazenados em uma VM do SQL Server no Azure que ajudam os algoritmos a aprender com mais eficiência com base nos dados.</span><span class="sxs-lookup"><span data-stu-id="0cfc5-104">This document shows how to generate features for data stored in a SQL Server VM on Azure that help algorithms learn more efficiently from the data.</span></span> <span data-ttu-id="0cfc5-105">Isso pode ser feito usando o SQL ou usando uma linguagem de programação como o Python, ambos demonstrados aqui.</span><span class="sxs-lookup"><span data-stu-id="0cfc5-105">This can be done by using SQL or by using a programming language like Python, both of which are demonstrated here.</span></span>

[!INCLUDE [cap-create-features-data-selector](../../includes/cap-create-features-selector.md)]

<span data-ttu-id="0cfc5-106">Este **menu** leva você até os tópicos que descrevem como criar recursos para dados em vários ambientes.</span><span class="sxs-lookup"><span data-stu-id="0cfc5-106">This **menu** links to topics that describe how to create features for data in various environments.</span></span> <span data-ttu-id="0cfc5-107">Essa tarefa é uma etapa no [TDSP (Processo de Ciência de Dados de Equipe)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span><span class="sxs-lookup"><span data-stu-id="0cfc5-107">This task is a step in the [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

> [!NOTE]
> <span data-ttu-id="0cfc5-108">Para obter um exemplo prático, você poderá usar o [conjunto de dados NYC Taxi](http://www.andresmh.com/nyctaxitrips/) e consultar o IPNB intitulado [NYC Data wrangling using IPython Notebook and SQL Server](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) (Realizar a disputa de dados de NYC usando o IPython Notebook e o SQL Server) para obter um passo a passo completo.</span><span class="sxs-lookup"><span data-stu-id="0cfc5-108">For a practical example, you can consult the [NYC Taxi dataset](http://www.andresmh.com/nyctaxitrips/) and refer to the IPNB titled [NYC Data wrangling using IPython Notebook and SQL Server](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) for an end-to-end walk-through.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="0cfc5-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="0cfc5-109">Prerequisites</span></span>
<span data-ttu-id="0cfc5-110">Este artigo supõe que você:</span><span class="sxs-lookup"><span data-stu-id="0cfc5-110">This article assumes that you have:</span></span>

* <span data-ttu-id="0cfc5-111">Criou uma conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="0cfc5-111">Created an Azure storage account.</span></span> <span data-ttu-id="0cfc5-112">Se precisar de instruções, confira [Criar uma conta de Armazenamento do Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="0cfc5-112">If you need instructions, see [Create an Azure Storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span></span>
* <span data-ttu-id="0cfc5-113">Armazenou seus dados no SQL Server.</span><span class="sxs-lookup"><span data-stu-id="0cfc5-113">Stored your data in SQL Server.</span></span> <span data-ttu-id="0cfc5-114">Se não tiver feito isso, veja [Mover dados para um Banco de Dados SQL do Azure para o Azure Machine Learning](machine-learning-data-science-move-sql-azure.md) para obter instruções sobre como mover os dados para lá.</span><span class="sxs-lookup"><span data-stu-id="0cfc5-114">If you have not, see [Move data to an Azure SQL Database for Azure Machine Learning](machine-learning-data-science-move-sql-azure.md) for instructions on how to move the data there.</span></span>

## <span data-ttu-id="0cfc5-115"><a name="sql-featuregen"></a>Geração de recursos com o SQL</span><span class="sxs-lookup"><span data-stu-id="0cfc5-115"><a name="sql-featuregen"></a>Feature Generation with SQL</span></span>
<span data-ttu-id="0cfc5-116">Nesta seção, descrevemos as maneiras de gerar recursos usando SQL:</span><span class="sxs-lookup"><span data-stu-id="0cfc5-116">In this section, we describe ways of generating features using SQL:</span></span>  

1. [<span data-ttu-id="0cfc5-117">Geração de recursos baseada em contagem</span><span class="sxs-lookup"><span data-stu-id="0cfc5-117">Count based Feature Generation</span></span>](#sql-countfeature)
2. [<span data-ttu-id="0cfc5-118">Agrupamento da Geração de Recursos</span><span class="sxs-lookup"><span data-stu-id="0cfc5-118">Binning Feature Generation</span></span>](#sql-binningfeature)
3. [<span data-ttu-id="0cfc5-119">Propagar os recursos de uma única coluna</span><span class="sxs-lookup"><span data-stu-id="0cfc5-119">Rolling out the features from a single column</span></span>](#sql-featurerollout)

> [!NOTE]
> <span data-ttu-id="0cfc5-120">Depois de gerar recursos adicionais, você pode adicioná-los como colunas à tabela existente ou criar uma nova tabela com os recursos adicionais e a chave primária, que pode ser unida com a tabela original.</span><span class="sxs-lookup"><span data-stu-id="0cfc5-120">Once you generate additional features, you can either add them as columns to the existing table or create a new table with the additional features and primary key, that can be joined with the original table.</span></span>
> 
> 

### <span data-ttu-id="0cfc5-121"><a name="sql-countfeature"></a>Geração de recursos baseada em contagem</span><span class="sxs-lookup"><span data-stu-id="0cfc5-121"><a name="sql-countfeature"></a>Count based Feature Generation</span></span>
<span data-ttu-id="0cfc5-122">Este documento demonstra duas maneiras de gerar recursos de contagem.</span><span class="sxs-lookup"><span data-stu-id="0cfc5-122">This document demonstrates two ways of generating count features.</span></span> <span data-ttu-id="0cfc5-123">O primeiro método usa soma condicional e o segundo usa a cláusula 'where'.</span><span class="sxs-lookup"><span data-stu-id="0cfc5-123">The first method uses conditional sum and the second method uses the 'where\` clause.</span></span> <span data-ttu-id="0cfc5-124">Eles podem então ser unidos à tabela original (usando colunas de chave primária) para que os recursos de contagem fiquem junto com os dados originais.</span><span class="sxs-lookup"><span data-stu-id="0cfc5-124">These can then be joined with the original table (using primary key columns) to have count features alongside the original data.</span></span>

    select <column_name1>,<column_name2>,<column_name3>, COUNT(*) as Count_Features from <tablename> group by <column_name1>,<column_name2>,<column_name3>

    select <column_name1>,<column_name2> , sum(1) as Count_Features from <tablename>
    where <column_name3> = '<some_value>' group by <column_name1>,<column_name2>

### <span data-ttu-id="0cfc5-125"><a name="sql-binningfeature"></a>Agrupamento da Geração de Recursos</span><span class="sxs-lookup"><span data-stu-id="0cfc5-125"><a name="sql-binningfeature"></a>Binning Feature Generation</span></span>
<span data-ttu-id="0cfc5-126">O exemplo a seguir mostra como gerar recursos compartimentalizados guardando (usando 5 compartimentos) uma coluna numérica que poderá ser usada como um recurso:</span><span class="sxs-lookup"><span data-stu-id="0cfc5-126">The following example shows how to generate binned features by binning (using 5 bins) a numerical column that can be used as a feature instead:</span></span>

    `SELECT <column_name>, NTILE(5) OVER (ORDER BY <column_name>) AS BinNumber from <tablename>`


### <span data-ttu-id="0cfc5-127"><a name="sql-featurerollout"></a>Propagar os recursos de uma única coluna</span><span class="sxs-lookup"><span data-stu-id="0cfc5-127"><a name="sql-featurerollout"></a>Rolling out the features from a single column</span></span>
<span data-ttu-id="0cfc5-128">Nesta seção, demonstraremos como propagar uma única coluna em uma tabela para gerar recursos adicionais.</span><span class="sxs-lookup"><span data-stu-id="0cfc5-128">In this section, we demonstrate how to roll-out a single column in a table to generate additional features.</span></span> <span data-ttu-id="0cfc5-129">O exemplo presume que há uma coluna de latitude ou longitude na tabela da qual você está tentando gerar recursos.</span><span class="sxs-lookup"><span data-stu-id="0cfc5-129">The example assumes that there is a latitude or longitude column in the table from which you are trying to generate features.</span></span>

<span data-ttu-id="0cfc5-130">Aqui está uma breve cartilha sobre os dados de localização de latitude/longitude (recursos de stackoverflow `http://gis.stackexchange.com/questions/8650/how-to-measure-the-accuracy-of-latitude-and-longitude`).</span><span class="sxs-lookup"><span data-stu-id="0cfc5-130">Here is a brief primer on latitude/longitude location data (resourced from stackoverflow `http://gis.stackexchange.com/questions/8650/how-to-measure-the-accuracy-of-latitude-and-longitude`).</span></span> <span data-ttu-id="0cfc5-131">É útil entender isso antes de destacar o campo local:</span><span class="sxs-lookup"><span data-stu-id="0cfc5-131">This is useful to understand before featurizing the location field:</span></span>

* <span data-ttu-id="0cfc5-132">O sinal nos informa se estamos na parte norte ou sul, leste ou oeste do globo.</span><span class="sxs-lookup"><span data-stu-id="0cfc5-132">The sign tells us whether we are north or south, east or west on the globe.</span></span>
* <span data-ttu-id="0cfc5-133">Um dígito em centenas diferente de zero informa que estamos usando longitude, não latitude!</span><span class="sxs-lookup"><span data-stu-id="0cfc5-133">A nonzero hundreds digit tells us we're using longitude, not latitude!</span></span>
* <span data-ttu-id="0cfc5-134">O dígito de dezena indica uma posição de cerca de 1.000 quilômetros.</span><span class="sxs-lookup"><span data-stu-id="0cfc5-134">The tens digit gives a position to about 1,000 kilometers.</span></span> <span data-ttu-id="0cfc5-135">Ele nos dá informações úteis sobre em qual continente ou oceano estamos.</span><span class="sxs-lookup"><span data-stu-id="0cfc5-135">It gives us useful information about what continent or ocean we are on.</span></span>
* <span data-ttu-id="0cfc5-136">O dígito e unidades (um grau decimal) oferece uma posição até 111 quilômetros (60 milhas náuticas, cerca de 69 milhas).</span><span class="sxs-lookup"><span data-stu-id="0cfc5-136">The units digit (one decimal degree) gives a position up to 111 kilometers (60 nautical miles, about 69 miles).</span></span> <span data-ttu-id="0cfc5-137">Ele pode indicar aproximadamente em qual grande estado ou país estamos.</span><span class="sxs-lookup"><span data-stu-id="0cfc5-137">It can tell us roughly what large state or country we are in.</span></span>
* <span data-ttu-id="0cfc5-138">A primeira casa decimal representa até 11,1 km: ela pode distinguir a posição de uma cidade grande de uma cidade grande vizinha.</span><span class="sxs-lookup"><span data-stu-id="0cfc5-138">The first decimal place is worth up to 11.1 km: it can distinguish the position of one large city from a neighboring large city.</span></span>
* <span data-ttu-id="0cfc5-139">A segunda casa decimal representa 1,1 km: ela pode separar um vila da próxima.</span><span class="sxs-lookup"><span data-stu-id="0cfc5-139">The second decimal place is worth up to 1.1 km: it can separate one village from the next.</span></span>
* <span data-ttu-id="0cfc5-140">A terceira casa decimal representa até 110 m: ela pode identificar um campo agrícola ou campus institucional grande.</span><span class="sxs-lookup"><span data-stu-id="0cfc5-140">The third decimal place is worth up to 110 m: it can identify a large agricultural field or institutional campus.</span></span>
* <span data-ttu-id="0cfc5-141">A quarta casa decimal representa até 11 m: ela pode identificar um lote de terreno.</span><span class="sxs-lookup"><span data-stu-id="0cfc5-141">The fourth decimal place is worth up to 11 m: it can identify a parcel of land.</span></span> <span data-ttu-id="0cfc5-142">Ela é comparável à precisão típica de uma unidade GPS não corrigida sem interferência.</span><span class="sxs-lookup"><span data-stu-id="0cfc5-142">It is comparable to the typical accuracy of an uncorrected GPS unit with no interference.</span></span>
* <span data-ttu-id="0cfc5-143">A quinta casa decimal representa até 1,1 m: ela distingue as árvores mas das outras.</span><span class="sxs-lookup"><span data-stu-id="0cfc5-143">The fifth decimal place is worth up to 1.1 m: it distinguish trees from each other.</span></span> <span data-ttu-id="0cfc5-144">Uma precisão desse nível com unidades GPS comerciais só pode ser obtida com a correção diferencial.</span><span class="sxs-lookup"><span data-stu-id="0cfc5-144">Accuracy to this level with commercial GPS units can only be achieved with differential correction.</span></span>
* <span data-ttu-id="0cfc5-145">A sexta casa decimal representa até 0,11 m: você pode usá-la para dispor estruturas detalhadamente, projetar paisagens e criar estradas.</span><span class="sxs-lookup"><span data-stu-id="0cfc5-145">The sixth decimal place is worth up to 0.11 m: you can use this for laying out structures in detail, for designing landscapes, building roads.</span></span> <span data-ttu-id="0cfc5-146">Ela é mais do que suficiente para acompanhar os movimentos de geleiras e rios.</span><span class="sxs-lookup"><span data-stu-id="0cfc5-146">It should be more than good enough for tracking movements of glaciers and rivers.</span></span> <span data-ttu-id="0cfc5-147">Isso pode ser obtido coletando medidas arduamente com o GPS, tais como GPS com correção diferencial.</span><span class="sxs-lookup"><span data-stu-id="0cfc5-147">This can be achieved by taking painstaking measures with GPS, such as differentially corrected GPS.</span></span>

<span data-ttu-id="0cfc5-148">As informações de localização podem pode ser destacadas da maneira indicada a seguir, separando informações de região, local e cidade.</span><span class="sxs-lookup"><span data-stu-id="0cfc5-148">The location information can can be featurized as follows, separating out region, location and city information.</span></span> <span data-ttu-id="0cfc5-149">Observe que também é possível chamar um ponto de extremidade REST tal como a API do Bing Mapas, disponível em `https://msdn.microsoft.com/library/ff701710.aspx` para obter as informações de região/distrito.</span><span class="sxs-lookup"><span data-stu-id="0cfc5-149">Note that once can also call a REST end point such as Bing Maps API available at `https://msdn.microsoft.com/library/ff701710.aspx` to get the region/district information.</span></span>

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

<span data-ttu-id="0cfc5-150">Os recursos de localização acima podem ser usados ainda para gerar recursos adicionais de contagem, como descrito anteriormente.</span><span class="sxs-lookup"><span data-stu-id="0cfc5-150">The above location based features can be further used to generate additional count features as described earlier.</span></span>

> [!TIP]
> <span data-ttu-id="0cfc5-151">É possível inserir os registros com programação usando a linguagem de sua escolha.</span><span class="sxs-lookup"><span data-stu-id="0cfc5-151">You can programmatically insert the records using your language of choice.</span></span> <span data-ttu-id="0cfc5-152">Talvez seja necessário inserir os dados em partes para melhorar a eficiência de gravação [Confira o exemplo de como fazer isso usando pyodbc aqui](https://code.google.com/p/pypyodbc/wiki/A_HelloWorld_sample_to_access_mssql_with_python).</span><span class="sxs-lookup"><span data-stu-id="0cfc5-152">You may need to insert the data in chunks to improve write efficiency [Check out the example of how to do this using pyodbc here](https://code.google.com/p/pypyodbc/wiki/A_HelloWorld_sample_to_access_mssql_with_python).</span></span>
> <span data-ttu-id="0cfc5-153">Outra alternativa é inserir dados no banco de dados usando o [utilitário BCP](https://msdn.microsoft.com/library/ms162802.aspx)</span><span class="sxs-lookup"><span data-stu-id="0cfc5-153">Another alternative is to insert data in the database using [BCP utility](https://msdn.microsoft.com/library/ms162802.aspx)</span></span>
> 
> 

### <span data-ttu-id="0cfc5-154">
            <a name="sql-aml">
            </a>Conectando ao Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="0cfc5-154"><a name="sql-aml"></a>Connecting to Azure Machine Learning</span></span>
<span data-ttu-id="0cfc5-155">O recurso recém-gerado pode ser adicionado como uma coluna a uma tabela existente ou armazenado em uma nova tabela e unido com a tabela original para o aprendizado de máquina.</span><span class="sxs-lookup"><span data-stu-id="0cfc5-155">The newly generated feature can be added as a column to an existing table or stored in a new table and joined with the original table for machine learning.</span></span> <span data-ttu-id="0cfc5-156">Recursos poderão ser gerados ou acessados se já foram criados, usando o módulo [Importar Dados](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) no AM do Azure conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="0cfc5-156">Features can be generated or accessed if already created, using the [Import Data](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) module in Azure ML as shown below:</span></span>

![leitores de azureml](./media/machine-learning-data-science-process-sql-server-virtual-machine/reader_db_featurizedinput.png)

## <span data-ttu-id="0cfc5-158"><a name="python"></a>Usando uma linguagem de programação como Python</span><span class="sxs-lookup"><span data-stu-id="0cfc5-158"><a name="python"></a>Using a programming language like Python</span></span>
<span data-ttu-id="0cfc5-159">Usar o Python para gerar recursos quando os dados estão no SQL Server é semelhante ao processamento de dados no blob do Azure usando o Python conforme documentado em [Processar dados de Blob do Azure em seu ambiente de ciência de dados](machine-learning-data-science-process-data-blob.md).</span><span class="sxs-lookup"><span data-stu-id="0cfc5-159">Using Python to generate features when the data is in SQL Server is similar to processing data in Azure blob using Python as documented in [Process Azure Blob data in you data science environment](machine-learning-data-science-process-data-blob.md).</span></span> <span data-ttu-id="0cfc5-160">Os dados precisam ser carregados do banco de dados para um quadro de dados pandas, quando então poderão ser processados.</span><span class="sxs-lookup"><span data-stu-id="0cfc5-160">The data needs to be loaded from the database into a pandas data frame and then can be processed further.</span></span> <span data-ttu-id="0cfc5-161">Documentamos o processo de conectar-se ao banco de dados e carregar os dados em um quadro de dados nesta seção.</span><span class="sxs-lookup"><span data-stu-id="0cfc5-161">We document the process of connecting to the database and loading the data into the data frame in this section.</span></span>

<span data-ttu-id="0cfc5-162">O seguinte formato de cadeia de conexão pode ser usado para se conectar a um banco de dados do SQL Server do Python usando pyodbc (substitua servername, dbname, nome de usuário e senha pelos seus valores específicos):</span><span class="sxs-lookup"><span data-stu-id="0cfc5-162">The following connection string format can be used to connect to a SQL Server database from Python using pyodbc (replace servername, dbname, username and password with your specific values):</span></span>

    #Set up the SQL Azure connection
    import pyodbc
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

<span data-ttu-id="0cfc5-163">A [Biblioteca Pandas](http://pandas.pydata.org/) no Python fornece um conjunto avançado de estruturas de dados e ferramentas de análise de dados para manipulação de dados para a programação Python.</span><span class="sxs-lookup"><span data-stu-id="0cfc5-163">The [Pandas library](http://pandas.pydata.org/) in Python provides a rich set of data structures and data analysis tools for data manipulation for Python programming.</span></span> <span data-ttu-id="0cfc5-164">O código a seguir lê os resultados retornados de um banco de dados do SQL Server em um quadro de dados Pandas:</span><span class="sxs-lookup"><span data-stu-id="0cfc5-164">The code below reads the results returned from a SQL Server database into a Pandas data frame:</span></span>

    # Query database and load the returned results in pandas data frame
    data_frame = pd.read_sql('''select <columnname1>, <cloumnname2>... from <tablename>''', conn)

<span data-ttu-id="0cfc5-165">Agora, você pode trabalhar com o quadro de dados Pandas como abordado nos tópicos [Criar recursos para os dados de armazenamento de blobs do Azure usando o Panda](machine-learning-data-science-create-features-blob.md).</span><span class="sxs-lookup"><span data-stu-id="0cfc5-165">Now you can work with the Pandas data frame as covered in topics [Create features for Azure blob storage data using Panda](machine-learning-data-science-create-features-blob.md).</span></span>

