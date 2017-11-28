---
title: aaaSample dados no SQL Server no Azure | Microsoft Docs
description: Dados de exemplo no SQL Server no Azure
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 33c030d4-5cca-4cc9-99d7-2bd13a3926af
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: fashah;garye;bradsev
ms.openlocfilehash: dc7f9529c771f6deb633775557e64a04b774f5b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <span data-ttu-id="783ab-103"><a name="heading"></a>Dados de exemplo no SQL Server no Azure</span><span class="sxs-lookup"><span data-stu-id="783ab-103"><a name="heading"></a>Sample data in SQL Server on Azure</span></span>
<span data-ttu-id="783ab-104">Este documento mostra como toosample dados armazenados no SQL Server no Azure usando SQL ou Olá linguagem de programação Python.</span><span class="sxs-lookup"><span data-stu-id="783ab-104">This document shows how toosample data stored in SQL Server on Azure using either SQL or hello Python programming language.</span></span> <span data-ttu-id="783ab-105">Ele também mostra como toomove dados de amostra no aprendizado de máquina do Azure, salvando-o arquivo tooa, carregando-tooan BLOBs do Azure e, em seguida, lê-los no estúdio de aprendizado de máquina do Azure.</span><span class="sxs-lookup"><span data-stu-id="783ab-105">It also shows how toomove sampled data into Azure Machine Learning by saving it tooa file, uploading it tooan Azure blob, and then reading it into Azure Machine Learning Studio.</span></span>

<span data-ttu-id="783ab-106">amostragem de Python Olá usa Olá [pyodbc](https://code.google.com/p/pyodbc/) tooSQL tooconnect da biblioteca ODBC Server no Azure e hello [Pandas](http://pandas.pydata.org/) amostragem de saudação do toodo de biblioteca.</span><span class="sxs-lookup"><span data-stu-id="783ab-106">hello Python sampling uses hello [pyodbc](https://code.google.com/p/pyodbc/) ODBC library tooconnect tooSQL Server on Azure and hello [Pandas](http://pandas.pydata.org/) library toodo hello sampling.</span></span>

> [!NOTE]
> <span data-ttu-id="783ab-107">código SQL de exemplo Hello neste documento pressupõe que Olá dados estão em um SQL Server no Azure.</span><span class="sxs-lookup"><span data-stu-id="783ab-107">hello sample SQL code in this document assumes that hello data is in a SQL Server on Azure.</span></span> <span data-ttu-id="783ab-108">Se não for, consulte muito[mover dados tooSQL Server no Azure](machine-learning-data-science-move-sql-server-virtual-machine.md) tópico para obter instruções sobre como toomove tooSQL seus dados Server no Azure.</span><span class="sxs-lookup"><span data-stu-id="783ab-108">If it is not, please refer too[Move data tooSQL Server on Azure](machine-learning-data-science-move-sql-server-virtual-machine.md) topic for instructions on how toomove your data tooSQL Server on Azure.</span></span>
> 
> 

<span data-ttu-id="783ab-109">a seguir Olá **menu** links tootopics que descrevem como toosample dados de vários ambientes de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="783ab-109">hello following **menu** links tootopics that describe how toosample data from various storage environments.</span></span> 

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

<span data-ttu-id="783ab-110">**Por que fazer amostragem dos dados?**</span><span class="sxs-lookup"><span data-stu-id="783ab-110">**Why sample your data?**</span></span>
<span data-ttu-id="783ab-111">Se dataset Olá planejar tooanalyze for grande, normalmente é um tooreduce de dados de exemplo toodown Olá boa ideia-tooa menor, mas representativo e mais fácil de gerenciar o tamanho.</span><span class="sxs-lookup"><span data-stu-id="783ab-111">If hello dataset you plan tooanalyze is large, it's usually a good idea toodown-sample hello data tooreduce it tooa smaller but representative and more manageable size.</span></span> <span data-ttu-id="783ab-112">Isso facilita a compreensão de dados, exploração e engenharia de recursos.</span><span class="sxs-lookup"><span data-stu-id="783ab-112">This facilitates data understanding, exploration, and feature engineering.</span></span> <span data-ttu-id="783ab-113">Sua função no hello [processo de ciência de dados da equipe (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) é tooenable rápida criação de protótipos de funções de processamento de dados de saudação e modelos de aprendizado de máquina.</span><span class="sxs-lookup"><span data-stu-id="783ab-113">Its role in hello [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) is tooenable fast prototyping of hello data processing functions and machine learning models.</span></span>

<span data-ttu-id="783ab-114">Esta tarefa de amostragem é uma etapa Olá [processo de ciência de dados da equipe (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span><span class="sxs-lookup"><span data-stu-id="783ab-114">This sampling task is a step in hello [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

## <span data-ttu-id="783ab-115"><a name="SQL"></a>Usando o SQL</span><span class="sxs-lookup"><span data-stu-id="783ab-115"><a name="SQL"></a>Using SQL</span></span>
<span data-ttu-id="783ab-116">Esta seção descreve vários métodos usando SQL tooperform amostragem aleatória simples em relação aos dados Olá Olá de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="783ab-116">This section describes several methods using SQL tooperform simple random sampling against hello data in hello database.</span></span> <span data-ttu-id="783ab-117">Escolha um método com base no tamanho e na distribuição dos seus dados.</span><span class="sxs-lookup"><span data-stu-id="783ab-117">Please choose a method based on your data size and its distribution.</span></span>

<span data-ttu-id="783ab-118">Olá dois itens a seguir mostram como newid toouse no SQL Server tooperform Olá amostragem.</span><span class="sxs-lookup"><span data-stu-id="783ab-118">hello two items below show how toouse newid in SQL Server tooperform hello sampling.</span></span> <span data-ttu-id="783ab-119">Olá método escolhido depende aleatório como você deseja toobe do exemplo hello (pk_id no código de exemplo hello abaixo é considerado toobe uma chave primária gerada automaticamente).</span><span class="sxs-lookup"><span data-stu-id="783ab-119">hello method you choose depends on how random you want hello sample toobe (pk_id in hello sample code below is assumed toobe an auto-generated primary key).</span></span>

1. <span data-ttu-id="783ab-120">Menos rígido do exemplo aleatório</span><span class="sxs-lookup"><span data-stu-id="783ab-120">Less strict random sample</span></span>
   
        select  * from <table_name> where <primary_key> in 
        (select top 10 percent <primary_key> from <table_name> order by newid())
2. <span data-ttu-id="783ab-121">Exemplo mais aleatório</span><span class="sxs-lookup"><span data-stu-id="783ab-121">More random sample</span></span> 
   
        SELECT * FROM <table_name>
        WHERE 0.1 >= CAST(CHECKSUM(NEWID(), <primary_key>) & 0x7fffffff AS float)/ CAST (0x7fffffff AS int)

<span data-ttu-id="783ab-122">TABLESAMPLE pode ser usado para amostragem conforme demonstrado a seguir.</span><span class="sxs-lookup"><span data-stu-id="783ab-122">Tablesample can be used for sampling as well as demonstrated below.</span></span> <span data-ttu-id="783ab-123">Isso pode ser uma abordagem melhor se o tamanho de dados for grande (supondo que não estão correlacionados dados em diferentes páginas) e para Olá toocomplete de consulta em um tempo razoável.</span><span class="sxs-lookup"><span data-stu-id="783ab-123">This may be a better approach if your data size is large (assuming that data on different pages is not correlated) and for hello query toocomplete in a reasonable time.</span></span>

    SELECT *
    FROM <table_name> 
    TABLESAMPLE (10 PERCENT)

> [!NOTE]
> <span data-ttu-id="783ab-124">Você pode explorar e gerar recursos por meio desses dados amostrados armazenando-os em uma nova tabela</span><span class="sxs-lookup"><span data-stu-id="783ab-124">You can explore and generate features from this sampled data by storing it in a new table</span></span>
> 
> 

### <span data-ttu-id="783ab-125"><a name="sql-aml"></a>Conectando tooAzure aprendizado de máquina</span><span class="sxs-lookup"><span data-stu-id="783ab-125"><a name="sql-aml"></a>Connecting tooAzure Machine Learning</span></span>
<span data-ttu-id="783ab-126">Você pode usar consultas de exemplo hello acima diretamente no hello aprendizado de máquina do Azure [importar dados] [ import-data] dados de exemplo toodown Olá de módulo Olá surgir e colocá-lo em uma experiência de aprendizado de máquina do Azure.</span><span class="sxs-lookup"><span data-stu-id="783ab-126">You can directly  use hello sample queries above in hello Azure Machine Learning [Import Data][import-data] module toodown-sample hello data on hello fly and bring it into an Azure Machine Learning experiment.</span></span> <span data-ttu-id="783ab-127">Abaixo está uma captura de tela do uso de dados de amostra de saudação Olá leitor módulo tooread:</span><span class="sxs-lookup"><span data-stu-id="783ab-127">A screen shot of using hello reader module tooread hello sampled data is shown below:</span></span>

![sql leitor][1]

## <span data-ttu-id="783ab-129"><a name="python"></a>Usando a linguagem de programação de Python Olá</span><span class="sxs-lookup"><span data-stu-id="783ab-129"><a name="python"></a>Using hello Python programming language</span></span>
<span data-ttu-id="783ab-130">Esta seção demonstra como usar o hello [pyodbc biblioteca](https://code.google.com/p/pyodbc/) tooestablish ODBC se conectar a banco de dados do servidor SQL de tooa em Python.</span><span class="sxs-lookup"><span data-stu-id="783ab-130">This section demonstrates using hello [pyodbc library](https://code.google.com/p/pyodbc/) tooestablish an ODBC connect tooa SQL server database in Python.</span></span> <span data-ttu-id="783ab-131">cadeia de conexão de banco de dados de saudação é o seguinte: (replace servername, dbname, nome de usuário e senha com a sua configuração):</span><span class="sxs-lookup"><span data-stu-id="783ab-131">hello database connection string is as follows: (replace servername, dbname, username and password with your configuration):</span></span>

    #Set up hello SQL Azure connection
    import pyodbc    
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

<span data-ttu-id="783ab-132">Olá [Pandas](http://pandas.pydata.org/) biblioteca do Python fornece um rico conjunto de ferramentas de análise de dados e estruturas de dados para a manipulação de dados para programação Python.</span><span class="sxs-lookup"><span data-stu-id="783ab-132">hello [Pandas](http://pandas.pydata.org/) library in Python provides a rich set of data structures and data analysis tools for data manipulation for Python programming.</span></span> <span data-ttu-id="783ab-133">código de saudação abaixo lê um exemplo de 0,1% dos dados de saudação de uma tabela no banco de dados do SQL Azure para os dados Pandas:</span><span class="sxs-lookup"><span data-stu-id="783ab-133">hello code below reads a 0.1% sample of hello data from a table in Azure SQL database into a Pandas data :</span></span>

    import pandas as pd

    # Query database and load hello returned results in pandas data frame
    data_frame = pd.read_sql('''select column1, cloumn2... from <table_name> tablesample (0.1 percent)''', conn)

<span data-ttu-id="783ab-134">Agora, você pode trabalhar com dados de amostra de saudação no quadro de dados Pandas hello.</span><span class="sxs-lookup"><span data-stu-id="783ab-134">You can now work with hello sampled data in hello Pandas data frame.</span></span> 

### <span data-ttu-id="783ab-135"><a name="python-aml"></a>Conectando tooAzure aprendizado de máquina</span><span class="sxs-lookup"><span data-stu-id="783ab-135"><a name="python-aml"></a>Connecting tooAzure Machine Learning</span></span>
<span data-ttu-id="783ab-136">Você pode usar o hello seguir toosave o código exemplo hello dados convertidos tooa arquivo e carregá-lo tooan BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="783ab-136">You can use hello following sample code toosave hello down-sampled data tooa file and upload it tooan Azure blob.</span></span> <span data-ttu-id="783ab-137">Olá dados blob Olá podem ser diretamente lidos em uma experiência de aprendizado de máquina do Azure usando Olá [importar dados] [ import-data] módulo.</span><span class="sxs-lookup"><span data-stu-id="783ab-137">hello data in hello blob can be directly read into an Azure Machine Learning Experiment using hello [Import Data][import-data] module.</span></span> <span data-ttu-id="783ab-138">etapas de saudação são da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="783ab-138">hello steps are as follows:</span></span> 

1. <span data-ttu-id="783ab-139">Gravar saudação pandas dados quadro tooa arquivo local</span><span class="sxs-lookup"><span data-stu-id="783ab-139">Write hello pandas data frame tooa local file</span></span>
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)
2. <span data-ttu-id="783ab-140">Carregar arquivo local tooAzure blob</span><span class="sxs-lookup"><span data-stu-id="783ab-140">Upload local file tooAzure blob</span></span>
   
        from azure.storage import BlobService
        import tables
   
        STORAGEACCOUNTNAME= <storage_account_name>
        LOCALFILENAME= <local_file_name>
        STORAGEACCOUNTKEY= <storage_account_key>
        CONTAINERNAME= <container_name>
        BLOBNAME= <blob_name>
   
        output_blob_service=BlobService(account_name=STORAGEACCOUNTNAME,account_key=STORAGEACCOUNTKEY)    
        localfileprocessed = os.path.join(os.getcwd(),LOCALFILENAME) #assuming file is in current working directory
   
        try:
   
        #perform upload
        output_blob_service.put_block_blob_from_path(CONTAINERNAME,BLOBNAME,localfileprocessed)
   
        except:            
            print ("Something went wrong with uploading blob:"+BLOBNAME)
3. <span data-ttu-id="783ab-141">Ler dados de blob do Azure usando o aprendizado de máquina do Azure [importar dados] [ import-data] módulo, como mostrado na captura de tela de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="783ab-141">Read data from Azure blob using Azure Machine Learning [Import Data][import-data] module as shown in hello screen grab below:</span></span>

![blob de leitor][2]

## <a name="hello-team-data-science-process-in-action-example"></a><span data-ttu-id="783ab-143">Olá processo de ciência de dados de equipe no exemplo de ação</span><span class="sxs-lookup"><span data-stu-id="783ab-143">hello Team Data Science Process in Action example</span></span>
<span data-ttu-id="783ab-144">Para obter um exemplo passo a passo de ponta a ponta Olá processo de ciência de dados de equipe um usando um conjunto de dados público, consulte [processo de ciência de dados de equipe em ação: usando o SQL Server](machine-learning-data-science-process-sql-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="783ab-144">For an end-to-end walkthrough example of hello Team Data Science Process a using a public dataset, see [Team Data Science Process in Action: using SQL Sever](machine-learning-data-science-process-sql-walkthrough.md).</span></span>

[1]: ./media/machine-learning-data-science-sample-sql-server-virtual-machine/reader_database.png
[2]: ./media/machine-learning-data-science-sample-sql-server-virtual-machine/reader_blob.png

[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
