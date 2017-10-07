---
title: "dados de aaaExplore na máquina de Virtual do SQL Server no Azure | Microsoft Docs"
description: Como tooexplore dados armazenados em uma VM do SQL Server no Azure.
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: ccbb3085-af9e-4ec2-9df2-15dcab261d05
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: fcc449fc0d0e49be9b673cfb2de347cf44804017
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="explore-data-in-sql-server-virtual-machine-on-azure"></a><span data-ttu-id="1a6c8-103">Explorar dados na Máquina Virtual do SQL Server no Azure</span><span class="sxs-lookup"><span data-stu-id="1a6c8-103">Explore data in SQL Server Virtual Machine on Azure</span></span>
<span data-ttu-id="1a6c8-104">Este documento aborda como tooexplore dados armazenados em uma VM do SQL Server no Azure.</span><span class="sxs-lookup"><span data-stu-id="1a6c8-104">This document covers how tooexplore data that is stored in a SQL Server VM on Azure.</span></span> <span data-ttu-id="1a6c8-105">Isso pode ser feito por disputa de dados usando SQL ou usando uma linguagem de programação como Python.</span><span class="sxs-lookup"><span data-stu-id="1a6c8-105">This can be done by data wrangling using SQL or by using a programming language like Python.</span></span>

<span data-ttu-id="1a6c8-106">a seguir Olá **menu** links tootopics que descrevem como toouse ferramentas tooexplore dados de vários ambientes de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="1a6c8-106">hello following **menu** links tootopics that describe how toouse tools tooexplore data from various storage environments.</span></span> <span data-ttu-id="1a6c8-107">Essa tarefa é uma etapa Olá processo de análise da Cortana (CAP).</span><span class="sxs-lookup"><span data-stu-id="1a6c8-107">This task is a step in hello Cortana Analytics Process (CAP).</span></span>

[!INCLUDE [cap-explore-data-selector](../../includes/cap-explore-data-selector.md)]

> [!NOTE]
> <span data-ttu-id="1a6c8-108">instruções de SQL de exemplo Hello neste documento pressupõem que dados estejam no SQL Server.</span><span class="sxs-lookup"><span data-stu-id="1a6c8-108">hello sample SQL statements in this document assume that data is in SQL Server.</span></span> <span data-ttu-id="1a6c8-109">Se não for, consulte toohello nuvem dados ciência processo mapa toolearn como toomove seu servidor de tooSQL de dados.</span><span class="sxs-lookup"><span data-stu-id="1a6c8-109">If it isn't, refer toohello cloud data science process map toolearn how toomove your data tooSQL Server.</span></span>
> 
> 

## <span data-ttu-id="1a6c8-110"><a name="sql-dataexploration"></a>Explorar dados de SQL com scripts SQL</span><span class="sxs-lookup"><span data-stu-id="1a6c8-110"><a name="sql-dataexploration"></a>Explore SQL data with SQL scripts</span></span>
<span data-ttu-id="1a6c8-111">Aqui estão alguns scripts de SQL de exemplo que podem ser usado tooexplore repositórios de dados no SQL Server.</span><span class="sxs-lookup"><span data-stu-id="1a6c8-111">Here are a few sample SQL scripts that can be used tooexplore data stores in SQL Server.</span></span>

1. <span data-ttu-id="1a6c8-112">Obter a contagem de saudação de observações por dia</span><span class="sxs-lookup"><span data-stu-id="1a6c8-112">Get hello count of observations per day</span></span>
   
    `SELECT CONVERT(date, <date_columnname>) as date, count(*) as c from <tablename> group by CONVERT(date, <date_columnname>)` 
2. <span data-ttu-id="1a6c8-113">Obter os níveis de saudação em uma coluna categórica</span><span class="sxs-lookup"><span data-stu-id="1a6c8-113">Get hello levels in a categorical column</span></span>
   
    `select  distinct <column_name> from <databasename>`
3. <span data-ttu-id="1a6c8-114">Obter o número de saudação de níveis na combinação de duas colunas categóricas</span><span class="sxs-lookup"><span data-stu-id="1a6c8-114">Get hello number of levels in combination of two categorical columns</span></span> 
   
    `select <column_a>, <column_b>,count(*) from <tablename> group by <column_a>, <column_b>`
4. <span data-ttu-id="1a6c8-115">Obter distribuição Olá para colunas numéricas</span><span class="sxs-lookup"><span data-stu-id="1a6c8-115">Get hello distribution for numerical columns</span></span>
   
    `select <column_name>, count(*) from <tablename> group by <column_name>`

> [!NOTE]
> <span data-ttu-id="1a6c8-116">Para obter um exemplo prático, você pode usar o hello [NYC táxi dataset](http://www.andresmh.com/nyctaxitrips/) e consulte toohello IPNB intitulada [NYC dados disputa usando o bloco de anotações do IPython e o SQL Server](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) para uma apresentação de ponta a ponta.</span><span class="sxs-lookup"><span data-stu-id="1a6c8-116">For a practical example, you can use hello [NYC Taxi dataset](http://www.andresmh.com/nyctaxitrips/) and refer toohello IPNB titled [NYC Data wrangling using IPython Notebook and SQL Server](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) for an end-to-end walk-through.</span></span>
> 
> 

## <span data-ttu-id="1a6c8-117"><a name="python"></a>Explorar dados de SQL com o Python</span><span class="sxs-lookup"><span data-stu-id="1a6c8-117"><a name="python"></a>Explore SQL data with Python</span></span>
<span data-ttu-id="1a6c8-118">Usando dados de tooexplore Python e gerar recursos quando Olá são de dados no SQL Server semelhante tooprocessing dados no blob do Azure usando o Python, conforme documentado no [dados de Blob do Azure de processo em seu ambiente de ciência de dados](machine-learning-data-science-process-data-blob.md).</span><span class="sxs-lookup"><span data-stu-id="1a6c8-118">Using Python tooexplore data and generate features when hello data is in SQL Server is similar tooprocessing data in Azure blob using Python, as documented in [Process Azure Blob data in your data science environment](machine-learning-data-science-process-data-blob.md).</span></span> <span data-ttu-id="1a6c8-119">dados de saudação precisa toobe carregado do banco de dados de saudação para um pandas DataFrame e, em seguida, podem ser processados.</span><span class="sxs-lookup"><span data-stu-id="1a6c8-119">hello data needs toobe loaded from hello database into a pandas DataFrame and then can be processed further.</span></span> <span data-ttu-id="1a6c8-120">Documentamos processo de saudação de conexão de banco de dados toohello e carregar dados saudação em Olá DataFrame nesta seção.</span><span class="sxs-lookup"><span data-stu-id="1a6c8-120">We document hello process of connecting toohello database and loading hello data into hello DataFrame in this section.</span></span>

<span data-ttu-id="1a6c8-121">Olá, formato de cadeia de caracteres de conexão a seguir pode ser usado tooconnect tooa banco de dados SQL do Python usando pyodbc (substituir servername, dbname, nome de usuário e senha com valores específicos):</span><span class="sxs-lookup"><span data-stu-id="1a6c8-121">hello following connection string format can be used tooconnect tooa SQL Server database from Python using pyodbc (replace servername, dbname, username, and password with your specific values):</span></span>

    #Set up hello SQL Azure connection
    import pyodbc    
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

<span data-ttu-id="1a6c8-122">Olá [biblioteca Pandas](http://pandas.pydata.org/) Python fornece um rico conjunto de ferramentas de análise de dados e estruturas de dados para a manipulação de dados para programação Python.</span><span class="sxs-lookup"><span data-stu-id="1a6c8-122">hello [Pandas library](http://pandas.pydata.org/) in Python provides a rich set of data structures and data analysis tools for data manipulation for Python programming.</span></span> <span data-ttu-id="1a6c8-123">Olá código a seguir lê Olá resultados de um banco de dados do SQL Server em um quadro de dados Pandas:</span><span class="sxs-lookup"><span data-stu-id="1a6c8-123">hello following code reads hello results returned from a SQL Server database into a Pandas data frame:</span></span>

    # Query database and load hello returned results in pandas data frame
    data_frame = pd.read_sql('''select <columnname1>, <cloumnname2>... from <tablename>''', conn)

<span data-ttu-id="1a6c8-124">Agora você pode trabalhar com hello Pandas DataFrame conforme abordado no tópico Olá [dados de Blob do Azure de processo em seu ambiente de ciência de dados](machine-learning-data-science-process-data-blob.md).</span><span class="sxs-lookup"><span data-stu-id="1a6c8-124">Now you can work with hello Pandas DataFrame as covered in hello topic [Process Azure Blob data in your data science environment](machine-learning-data-science-process-data-blob.md).</span></span>

## <a name="cortana-analytics-process-in-action-example"></a><span data-ttu-id="1a6c8-125">Processo de Análise do Cortana no exemplo de ação</span><span class="sxs-lookup"><span data-stu-id="1a6c8-125">Cortana Analytics Process in Action Example</span></span>
<span data-ttu-id="1a6c8-126">Para obter um exemplo passo a passo de ponta a ponta Olá processo de análise de Cortana usando um conjunto de dados público, consulte [Olá o processo de ciência de dados de equipe em ação: usando o SQL Server](machine-learning-data-science-process-sql-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="1a6c8-126">For an end-to-end walkthrough example of hello Cortana Analytics Process using a public dataset, see [hello Team Data Science Process in action: using SQL Server](machine-learning-data-science-process-sql-walkthrough.md).</span></span>

