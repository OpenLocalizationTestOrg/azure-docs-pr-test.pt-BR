---
title: "dados com análises avançadas de blob de aaaProcess do Azure | Microsoft Docs"
description: Processar dados no Armazenamento de Blob do Azure.
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: d8a59078-91d3-4440-b85c-430363c3f4d1
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: fashah;garye;bradsev
ms.openlocfilehash: 5911d4211c4135680555a8cdd99e745499a24215
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <span data-ttu-id="699ff-103"><a name="heading"></a>Processar dados de blob do Azure com análises avançadas</span><span class="sxs-lookup"><span data-stu-id="699ff-103"><a name="heading"></a>Process Azure blob data with advanced analytics</span></span>
<span data-ttu-id="699ff-104">Este documento aborda a exploração de dados e a geração de recursos por meio dos dados armazenados no Armazenamento de Blob do Azure.</span><span class="sxs-lookup"><span data-stu-id="699ff-104">This document covers exploring data and generating features from data stored in Azure Blob storage.</span></span> 

## <a name="load-hello-data-into-a-pandas-data-frame"></a><span data-ttu-id="699ff-105">Saudação de carregar dados em um quadro de dados Pandas</span><span class="sxs-lookup"><span data-stu-id="699ff-105">Load hello data into a Pandas data frame</span></span>
<span data-ttu-id="699ff-106">Em ordem tooexplore e manipular um conjunto de dados, ela deve ser baixada de saudação blob fonte tooa arquivo local que, em seguida, pode ser carregado em um quadro de dados Pandas.</span><span class="sxs-lookup"><span data-stu-id="699ff-106">In order tooexplore and manipulate a dataset, it must be downloaded from hello blob source tooa local file which can then be loaded in a Pandas data frame.</span></span> <span data-ttu-id="699ff-107">Aqui estão Olá etapas toofollow para este procedimento:</span><span class="sxs-lookup"><span data-stu-id="699ff-107">Here are hello steps toofollow for this procedure:</span></span>

1. <span data-ttu-id="699ff-108">Baixar dados de saudação do Azure blob com hello seguindo o código Python de exemplo usando o serviço blob.</span><span class="sxs-lookup"><span data-stu-id="699ff-108">Download hello data from Azure blob with hello following sample Python code using blob service.</span></span> <span data-ttu-id="699ff-109">Substitua variável Olá no código Olá abaixo com seus valores específicos:</span><span class="sxs-lookup"><span data-stu-id="699ff-109">Replace hello variable in hello code below with your specific values:</span></span> 
   
        from azure.storage.blob import BlobService
        import tables
   
        STORAGEACCOUNTNAME= <storage_account_name>
        STORAGEACCOUNTKEY= <storage_account_key>
        LOCALFILENAME= <local_file_name>        
        CONTAINERNAME= <container_name>
        BLOBNAME= <blob_name>
   
        #download from blob
        t1=time.time()
        blob_service=BlobService(account_name=STORAGEACCOUNTNAME,account_key=STORAGEACCOUNTKEY)
        blob_service.get_blob_to_path(CONTAINERNAME,BLOBNAME,LOCALFILENAME)
        t2=time.time()
        print(("It takes %s seconds toodownload "+blobname) % (t2 - t1))
2. <span data-ttu-id="699ff-110">Saudação de ler dados em um quadro de dados Pandas de saudação download de arquivo.</span><span class="sxs-lookup"><span data-stu-id="699ff-110">Read hello data into a Pandas data-frame from hello downloaded file.</span></span>
   
        #LOCALFILE is hello file path    
        dataframe_blobdata = pd.read_csv(LOCALFILE)

<span data-ttu-id="699ff-111">Agora você está pronto tooexplore Olá dados e gerar recursos nesse conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="699ff-111">Now you are ready tooexplore hello data and generate features on this dataset.</span></span>

## <span data-ttu-id="699ff-112"><a name="blob-dataexploration"></a>Exploração de Dados</span><span class="sxs-lookup"><span data-stu-id="699ff-112"><a name="blob-dataexploration"></a>Data Exploration</span></span>
<span data-ttu-id="699ff-113">Aqui estão alguns exemplos de maneiras tooexplore dados usando Pandas:</span><span class="sxs-lookup"><span data-stu-id="699ff-113">Here are a few examples of ways tooexplore data using Pandas:</span></span>

1. <span data-ttu-id="699ff-114">Inspecione o número de saudação de linhas e colunas</span><span class="sxs-lookup"><span data-stu-id="699ff-114">Inspect hello number of rows and columns</span></span> 
   
        print 'hello size of hello data is: %d rows and  %d columns' % dataframe_blobdata.shape
2. <span data-ttu-id="699ff-115">Inspecionar Olá primeiro ou último algumas linhas no conjunto de dados hello como abaixo:</span><span class="sxs-lookup"><span data-stu-id="699ff-115">Inspect hello first or last few rows in hello dataset as below:</span></span>
   
        dataframe_blobdata.head(10)
   
        dataframe_blobdata.tail(10)
3. <span data-ttu-id="699ff-116">Verifique cada coluna foi importada usando Olá código de exemplo a seguir de tipo de dados Olá</span><span class="sxs-lookup"><span data-stu-id="699ff-116">Check hello data type each column was imported as using hello following sample code</span></span>
   
        for col in dataframe_blobdata.columns:
            print dataframe_blobdata[col].name, ':\t', dataframe_blobdata[col].dtype
4. <span data-ttu-id="699ff-117">Verifique as estatísticas de saudação básica para colunas de saudação do conjunto de dados de saudação da seguinte maneira</span><span class="sxs-lookup"><span data-stu-id="699ff-117">Check hello basic stats for hello columns in hello data set as follows</span></span>
   
        dataframe_blobdata.describe()
5. <span data-ttu-id="699ff-118">Veja Olá número de entradas para cada valor de coluna da seguinte maneira</span><span class="sxs-lookup"><span data-stu-id="699ff-118">Look at hello number of entries for each column value as follows</span></span>
   
        dataframe_blobdata['<column_name>'].value_counts()
6. <span data-ttu-id="699ff-119">Contagem de valores ausentes em comparação com o número real de saudação de entradas em cada coluna usando Olá código de exemplo a seguir</span><span class="sxs-lookup"><span data-stu-id="699ff-119">Count missing values versus hello actual number of entries in each column using hello following sample code</span></span>
   
        miss_num = dataframe_blobdata.shape[0] - dataframe_blobdata.count()
        print miss_num
7. <span data-ttu-id="699ff-120">Se você tiver valores ausentes para uma coluna específica em dados hello, pode descartá-los da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="699ff-120">If you have missing values for a specific column in hello data, you can drop them as follows:</span></span>
   
     <span data-ttu-id="699ff-121">dataframe_blobdata_noNA = dataframe_blobdata.dropna()   dataframe_blobdata_noNA.shape</span><span class="sxs-lookup"><span data-stu-id="699ff-121">dataframe_blobdata_noNA = dataframe_blobdata.dropna()   dataframe_blobdata_noNA.shape</span></span>
   
   <span data-ttu-id="699ff-122">É outra maneira tooreplace os valores ausentes com a função de modo hello:</span><span class="sxs-lookup"><span data-stu-id="699ff-122">Another way tooreplace missing values is with hello mode function:</span></span>
   
     <span data-ttu-id="699ff-123">dataframe_blobdata_mode = dataframe_blobdata.fillna({'<column_name>':dataframe_blobdata['<column_name>'].mode()[0]})</span><span class="sxs-lookup"><span data-stu-id="699ff-123">dataframe_blobdata_mode = dataframe_blobdata.fillna({'<column_name>':dataframe_blobdata['<column_name>'].mode()[0]})</span></span>        
8. <span data-ttu-id="699ff-124">Criar um gráfico de histograma usando um número variável de distribuição de saudação tooplot compartimentos de uma variável</span><span class="sxs-lookup"><span data-stu-id="699ff-124">Create a histogram plot using variable number of bins tooplot hello distribution of a variable</span></span>    
   
        dataframe_blobdata['<column_name>'].value_counts().plot(kind='bar')
   
        np.log(dataframe_blobdata['<column_name>']+1).hist(bins=50)
9. <span data-ttu-id="699ff-125">Examinar correlações entre variáveis usando um scatterplot ou função de correlação internos hello</span><span class="sxs-lookup"><span data-stu-id="699ff-125">Look at correlations between variables using a scatterplot or using hello built-in correlation function</span></span>
   
        #relationship between column_a and column_b using scatter plot
        plt.scatter(dataframe_blobdata['<column_a>'], dataframe_blobdata['<column_b>'])
   
        #correlation between column_a and column_b
        dataframe_blobdata[['<column_a>', '<column_b>']].corr()

## <span data-ttu-id="699ff-126"><a name="blob-featuregen"></a>Geração de recursos</span><span class="sxs-lookup"><span data-stu-id="699ff-126"><a name="blob-featuregen"></a>Feature Generation</span></span>
<span data-ttu-id="699ff-127">Podemos gerar recursos usando o Python da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="699ff-127">We can generate features using Python as follows:</span></span>

### <span data-ttu-id="699ff-128"><a name="blob-countfeature"></a>Geração de Recursos baseada no valor do indicador</span><span class="sxs-lookup"><span data-stu-id="699ff-128"><a name="blob-countfeature"></a>Indicator value based Feature Generation</span></span>
<span data-ttu-id="699ff-129">Recursos categóricos podem ser criados da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="699ff-129">Categorical features can be created as follows:</span></span>

1. <span data-ttu-id="699ff-130">Inspecione a distribuição de saudação de coluna categórica hello:</span><span class="sxs-lookup"><span data-stu-id="699ff-130">Inspect hello distribution of hello categorical column:</span></span>
   
        dataframe_blobdata['<categorical_column>'].value_counts()
2. <span data-ttu-id="699ff-131">Gerar valores de indicador para cada um dos valores da coluna Olá</span><span class="sxs-lookup"><span data-stu-id="699ff-131">Generate indicator values for each of hello column values</span></span>
   
        #generate hello indicator column
        dataframe_blobdata_identity = pd.get_dummies(dataframe_blobdata['<categorical_column>'], prefix='<categorical_column>_identity')
3. <span data-ttu-id="699ff-132">Unir a coluna de indicador Olá com quadro de dados original Olá</span><span class="sxs-lookup"><span data-stu-id="699ff-132">Join hello indicator column with hello original data frame</span></span> 
   
            #Join hello dummy variables back toohello original data frame
            dataframe_blobdata_with_identity = dataframe_blobdata.join(dataframe_blobdata_identity)
4. <span data-ttu-id="699ff-133">Remova Olá original variável:</span><span class="sxs-lookup"><span data-stu-id="699ff-133">Remove hello original variable itself:</span></span>
   
        #Remove hello original column rate_code in df1_with_dummy
        dataframe_blobdata_with_identity.drop('<categorical_column>', axis=1, inplace=True)

### <span data-ttu-id="699ff-134"><a name="blob-binningfeature"></a>Agrupamento da Geração de Recursos</span><span class="sxs-lookup"><span data-stu-id="699ff-134"><a name="blob-binningfeature"></a>Binning Feature Generation</span></span>
<span data-ttu-id="699ff-135">Para gerar recursos compartimentalizados, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="699ff-135">For generating binned features, we proceed as follows:</span></span>

1. <span data-ttu-id="699ff-136">Adicionar uma sequência de colunas toobin uma coluna numérica</span><span class="sxs-lookup"><span data-stu-id="699ff-136">Add a sequence of columns toobin a numeric column</span></span>
   
        bins = [0, 1, 2, 4, 10, 40]
        dataframe_blobdata_bin_id = pd.cut(dataframe_blobdata['<numeric_column>'], bins)
2. <span data-ttu-id="699ff-137">Converter a sequência de agrupamento tooa de variáveis Boolianas</span><span class="sxs-lookup"><span data-stu-id="699ff-137">Convert binning tooa sequence of boolean variables</span></span>
   
        dataframe_blobdata_bin_bool = pd.get_dummies(dataframe_blobdata_bin_id, prefix='<numeric_column>')
3. <span data-ttu-id="699ff-138">Por fim, unir o quadro de dados original do hello variáveis fictício toohello back</span><span class="sxs-lookup"><span data-stu-id="699ff-138">Finally, Join hello dummy variables back toohello original data frame</span></span>
   
        dataframe_blobdata_with_bin_bool = dataframe_blobdata.join(dataframe_blobdata_bin_bool)    

## <span data-ttu-id="699ff-139"><a name="sql-featuregen"></a>Gravar dados de volta tooAzure blob e consumindo no aprendizado de máquina do Azure</span><span class="sxs-lookup"><span data-stu-id="699ff-139"><a name="sql-featuregen"></a>Writing data back tooAzure blob and consuming in Azure Machine Learning</span></span>
<span data-ttu-id="699ff-140">Depois de explorar dados saudação e criado Olá recursos necessários, você pode carregar dados saudação (amostra ou featurized) tooan Azure blob e consumi-lo no aprendizado de máquina do Azure usando Olá etapas a seguir: Observe que os recursos adicionais podem ser criados em Olá Azure Machine Learning Studio também.</span><span class="sxs-lookup"><span data-stu-id="699ff-140">After you have explored hello data and created hello necessary features, you can upload hello data (sampled or featurized) tooan Azure blob and consume it in Azure Machine Learning using hello following steps: Note that additional features can be created in hello Azure Machine Learning Studio as well.</span></span> 

1. <span data-ttu-id="699ff-141">Gravar o arquivo de toolocal de quadro de dados Olá</span><span class="sxs-lookup"><span data-stu-id="699ff-141">Write hello data frame toolocal file</span></span>
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)
2. <span data-ttu-id="699ff-142">Carregar o blob de tooAzure dados Olá da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="699ff-142">Upload hello data tooAzure blob as follows:</span></span>
   
        from azure.storage.blob import BlobService
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
3. <span data-ttu-id="699ff-143">Agora Olá dados podem ser lidos do uso de blob Olá Olá aprendizado de máquina do Azure [importar dados] [ import-data] módulo, como mostrado na tela hello abaixo:</span><span class="sxs-lookup"><span data-stu-id="699ff-143">Now hello data can be read from hello blob using hello Azure Machine Learning [Import Data][import-data] module as shown in hello screen below:</span></span>

![blob de leitor][1]

[1]: ./media/machine-learning-data-science-process-data-blob/reader_blob.png


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/

