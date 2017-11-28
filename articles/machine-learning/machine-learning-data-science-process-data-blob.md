---
title: "Processar dados de blob do Azure com análises avançadas | Microsoft Docs"
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
ms.openlocfilehash: 36d950fd81029af82d9f2f652b2f01dba5fc8cc9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <span data-ttu-id="82ccd-103"><a name="heading"></a>Processar dados de blob do Azure com análises avançadas</span><span class="sxs-lookup"><span data-stu-id="82ccd-103"><a name="heading"></a>Process Azure blob data with advanced analytics</span></span>
<span data-ttu-id="82ccd-104">Este documento aborda a exploração de dados e a geração de recursos por meio dos dados armazenados no Armazenamento de Blob do Azure.</span><span class="sxs-lookup"><span data-stu-id="82ccd-104">This document covers exploring data and generating features from data stored in Azure Blob storage.</span></span> 

## <a name="load-the-data-into-a-pandas-data-frame"></a><span data-ttu-id="82ccd-105">Carregar os dados em um quadro de dados Pandas</span><span class="sxs-lookup"><span data-stu-id="82ccd-105">Load the data into a Pandas data frame</span></span>
<span data-ttu-id="82ccd-106">Para explorar e manipular um conjunto de dados, ele deve ser baixado da fonte de blob para um arquivo local, que pode então ser carregado em um quadro de dados Pandas.</span><span class="sxs-lookup"><span data-stu-id="82ccd-106">In order to explore and manipulate a dataset, it must be downloaded from the blob source to a local file which can then be loaded in a Pandas data frame.</span></span> <span data-ttu-id="82ccd-107">Aqui estão as etapas para este procedimento:</span><span class="sxs-lookup"><span data-stu-id="82ccd-107">Here are the steps to follow for this procedure:</span></span>

1. <span data-ttu-id="82ccd-108">Baixe os dados do Blob do Azure com o seguinte código de Python de exemplo e usando o serviço blob a seguir.</span><span class="sxs-lookup"><span data-stu-id="82ccd-108">Download the data from Azure blob with the following sample Python code using blob service.</span></span> <span data-ttu-id="82ccd-109">Substitua a variável no código abaixo pelos valores específicos:</span><span class="sxs-lookup"><span data-stu-id="82ccd-109">Replace the variable in the code below with your specific values:</span></span> 
   
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
        print(("It takes %s seconds to download "+blobname) % (t2 - t1))
2. <span data-ttu-id="82ccd-110">Leia os dados em um quadro de dados Pandas do arquivo baixado.</span><span class="sxs-lookup"><span data-stu-id="82ccd-110">Read the data into a Pandas data-frame from the downloaded file.</span></span>
   
        #LOCALFILE is the file path    
        dataframe_blobdata = pd.read_csv(LOCALFILE)

<span data-ttu-id="82ccd-111">Agora você está pronto para explorar os dados e gerar recursos neste conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="82ccd-111">Now you are ready to explore the data and generate features on this dataset.</span></span>

## <span data-ttu-id="82ccd-112"><a name="blob-dataexploration"></a>Exploração de Dados</span><span class="sxs-lookup"><span data-stu-id="82ccd-112"><a name="blob-dataexploration"></a>Data Exploration</span></span>
<span data-ttu-id="82ccd-113">Veja estão alguns exemplos de maneiras de explorar dados usando Pandas:</span><span class="sxs-lookup"><span data-stu-id="82ccd-113">Here are a few examples of ways to explore data using Pandas:</span></span>

1. <span data-ttu-id="82ccd-114">Verificar o número de linhas e colunas</span><span class="sxs-lookup"><span data-stu-id="82ccd-114">Inspect the number of rows and columns</span></span> 
   
        print 'the size of the data is: %d rows and  %d columns' % dataframe_blobdata.shape
2. <span data-ttu-id="82ccd-115">Inspecione as primeira ou últimas linhas no conjunto de dados, conforme mostrado a seguir:</span><span class="sxs-lookup"><span data-stu-id="82ccd-115">Inspect the first or last few rows in the dataset as below:</span></span>
   
        dataframe_blobdata.head(10)
   
        dataframe_blobdata.tail(10)
3. <span data-ttu-id="82ccd-116">Verifique o tipo de dados indicado para cada coluna importada usando o seguinte código de exemplo</span><span class="sxs-lookup"><span data-stu-id="82ccd-116">Check the data type each column was imported as using the following sample code</span></span>
   
        for col in dataframe_blobdata.columns:
            print dataframe_blobdata[col].name, ':\t', dataframe_blobdata[col].dtype
4. <span data-ttu-id="82ccd-117">Verifique as estatísticas básicas para as colunas no conjunto de dados da seguinte maneira</span><span class="sxs-lookup"><span data-stu-id="82ccd-117">Check the basic stats for the columns in the data set as follows</span></span>
   
        dataframe_blobdata.describe()
5. <span data-ttu-id="82ccd-118">Veja o número de entradas para cada valor de coluna da seguinte maneira</span><span class="sxs-lookup"><span data-stu-id="82ccd-118">Look at the number of entries for each column value as follows</span></span>
   
        dataframe_blobdata['<column_name>'].value_counts()
6. <span data-ttu-id="82ccd-119">Conte os valores ausentes em comparação com o número real de entradas em cada coluna usando o seguinte código de exemplo</span><span class="sxs-lookup"><span data-stu-id="82ccd-119">Count missing values versus the actual number of entries in each column using the following sample code</span></span>
   
        miss_num = dataframe_blobdata.shape[0] - dataframe_blobdata.count()
        print miss_num
7. <span data-ttu-id="82ccd-120">Se você tiver valores ausentes para uma coluna específica nos dados, poderá removê-los da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="82ccd-120">If you have missing values for a specific column in the data, you can drop them as follows:</span></span>
   
     <span data-ttu-id="82ccd-121">dataframe_blobdata_noNA = dataframe_blobdata.dropna()   dataframe_blobdata_noNA.shape</span><span class="sxs-lookup"><span data-stu-id="82ccd-121">dataframe_blobdata_noNA = dataframe_blobdata.dropna()   dataframe_blobdata_noNA.shape</span></span>
   
   <span data-ttu-id="82ccd-122">Outra maneira de substituir valores ausentes é com a função de modo:</span><span class="sxs-lookup"><span data-stu-id="82ccd-122">Another way to replace missing values is with the mode function:</span></span>
   
     <span data-ttu-id="82ccd-123">dataframe_blobdata_mode = dataframe_blobdata.fillna({'<column_name>':dataframe_blobdata['<column_name>'].mode()[0]})</span><span class="sxs-lookup"><span data-stu-id="82ccd-123">dataframe_blobdata_mode = dataframe_blobdata.fillna({'<column_name>':dataframe_blobdata['<column_name>'].mode()[0]})</span></span>        
8. <span data-ttu-id="82ccd-124">Crie um gráfico de histograma usando um número variável de compartimentos para plotar a distribuição de uma variável</span><span class="sxs-lookup"><span data-stu-id="82ccd-124">Create a histogram plot using variable number of bins to plot the distribution of a variable</span></span>    
   
        dataframe_blobdata['<column_name>'].value_counts().plot(kind='bar')
   
        np.log(dataframe_blobdata['<column_name>']+1).hist(bins=50)
9. <span data-ttu-id="82ccd-125">Examine correlações entre variáveis usando um gráfico disperso ou a função interna de correlação</span><span class="sxs-lookup"><span data-stu-id="82ccd-125">Look at correlations between variables using a scatterplot or using the built-in correlation function</span></span>
   
        #relationship between column_a and column_b using scatter plot
        plt.scatter(dataframe_blobdata['<column_a>'], dataframe_blobdata['<column_b>'])
   
        #correlation between column_a and column_b
        dataframe_blobdata[['<column_a>', '<column_b>']].corr()

## <span data-ttu-id="82ccd-126"><a name="blob-featuregen"></a>Geração de Recursos</span><span class="sxs-lookup"><span data-stu-id="82ccd-126"><a name="blob-featuregen"></a>Feature Generation</span></span>
<span data-ttu-id="82ccd-127">Podemos gerar recursos usando o Python da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="82ccd-127">We can generate features using Python as follows:</span></span>

### <span data-ttu-id="82ccd-128"><a name="blob-countfeature"></a>Geração de Recursos baseada no valor do indicador</span><span class="sxs-lookup"><span data-stu-id="82ccd-128"><a name="blob-countfeature"></a>Indicator value based Feature Generation</span></span>
<span data-ttu-id="82ccd-129">Recursos categóricos podem ser criados da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="82ccd-129">Categorical features can be created as follows:</span></span>

1. <span data-ttu-id="82ccd-130">Inspecionar a distribuição da coluna categórica:</span><span class="sxs-lookup"><span data-stu-id="82ccd-130">Inspect the distribution of the categorical column:</span></span>
   
        dataframe_blobdata['<categorical_column>'].value_counts()
2. <span data-ttu-id="82ccd-131">Gerar valores de indicador para cada um dos valores da coluna</span><span class="sxs-lookup"><span data-stu-id="82ccd-131">Generate indicator values for each of the column values</span></span>
   
        #generate the indicator column
        dataframe_blobdata_identity = pd.get_dummies(dataframe_blobdata['<categorical_column>'], prefix='<categorical_column>_identity')
3. <span data-ttu-id="82ccd-132">Unir a coluna de indicador com o quadro de dados original</span><span class="sxs-lookup"><span data-stu-id="82ccd-132">Join the indicator column with the original data frame</span></span> 
   
            #Join the dummy variables back to the original data frame
            dataframe_blobdata_with_identity = dataframe_blobdata.join(dataframe_blobdata_identity)
4. <span data-ttu-id="82ccd-133">Remover a própria variável original:</span><span class="sxs-lookup"><span data-stu-id="82ccd-133">Remove the original variable itself:</span></span>
   
        #Remove the original column rate_code in df1_with_dummy
        dataframe_blobdata_with_identity.drop('<categorical_column>', axis=1, inplace=True)

### <span data-ttu-id="82ccd-134"><a name="blob-binningfeature"></a>Agrupamento da Geração de Recursos</span><span class="sxs-lookup"><span data-stu-id="82ccd-134"><a name="blob-binningfeature"></a>Binning Feature Generation</span></span>
<span data-ttu-id="82ccd-135">Para gerar recursos compartimentalizados, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="82ccd-135">For generating binned features, we proceed as follows:</span></span>

1. <span data-ttu-id="82ccd-136">Adicione uma sequência de colunas a ser compartimentalizada a coluna numérica</span><span class="sxs-lookup"><span data-stu-id="82ccd-136">Add a sequence of columns to bin a numeric column</span></span>
   
        bins = [0, 1, 2, 4, 10, 40]
        dataframe_blobdata_bin_id = pd.cut(dataframe_blobdata['<numeric_column>'], bins)
2. <span data-ttu-id="82ccd-137">Converta a compartimentalização em uma sequência de variáveis boolianas</span><span class="sxs-lookup"><span data-stu-id="82ccd-137">Convert binning to a sequence of boolean variables</span></span>
   
        dataframe_blobdata_bin_bool = pd.get_dummies(dataframe_blobdata_bin_id, prefix='<numeric_column>')
3. <span data-ttu-id="82ccd-138">Por fim, associe as variáveis fictícias ao quadro de dados original</span><span class="sxs-lookup"><span data-stu-id="82ccd-138">Finally, Join the dummy variables back to the original data frame</span></span>
   
        dataframe_blobdata_with_bin_bool = dataframe_blobdata.join(dataframe_blobdata_bin_bool)    

## <span data-ttu-id="82ccd-139">
            <a name="sql-featuregen">
            </a>Gravar dados de volta ao blob do Azure e consumi-los no Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="82ccd-139"><a name="sql-featuregen"></a>Writing data back to Azure blob and consuming in Azure Machine Learning</span></span>
<span data-ttu-id="82ccd-140">Depois que você já explorou os dados e criou os recursos necessários, pode carregar os dados (amostra ou recurso) para um blob do Azure e consumi-los no Azure Machine Learning usando as seguintes etapas: observe que os recursos adicionais podem ser criados no Azure Machine Learning Studio também.</span><span class="sxs-lookup"><span data-stu-id="82ccd-140">After you have explored the data and created the necessary features, you can upload the data (sampled or featurized) to an Azure blob and consume it in Azure Machine Learning using the following steps: Note that additional features can be created in the Azure Machine Learning Studio as well.</span></span> 

1. <span data-ttu-id="82ccd-141">Grave o quadro de dados no arquivo local</span><span class="sxs-lookup"><span data-stu-id="82ccd-141">Write the data frame to local file</span></span>
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)
2. <span data-ttu-id="82ccd-142">Carregue os dados para o blob do Azure da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="82ccd-142">Upload the data to Azure blob as follows:</span></span>
   
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
3. <span data-ttu-id="82ccd-143">Agora, os dados podem ser lidos do blob usando o módulo [Importar Dados][import-data] do Azure Machine Learning, como mostra a tela abaixo:</span><span class="sxs-lookup"><span data-stu-id="82ccd-143">Now the data can be read from the blob using the Azure Machine Learning [Import Data][import-data] module as shown in the screen below:</span></span>

![blob de leitor][1]

[1]: ./media/machine-learning-data-science-process-data-blob/reader_blob.png


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/

