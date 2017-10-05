---
title: Criar recursos para dados de armazenamento de blobs do Azure usando o Panda | Microsoft Docs
description: "Como criar recursos para os dados armazenados no contêiner de blob do Azure com o pacote Python Pandas."
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 676b5fb0-4c89-4516-b3a8-e78ae3ca078d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev;garye
ms.openlocfilehash: 2ef2acfea2372ac7fd52d099a2b4203ee2242d81
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="create-features-for-azure-blob-storage-data-using-panda"></a><span data-ttu-id="5aaa8-103">Criar recursos para dados de armazenamento de blob do Azure usando o Panda</span><span class="sxs-lookup"><span data-stu-id="5aaa8-103">Create features for Azure blob storage data using Panda</span></span>
<span data-ttu-id="5aaa8-104">Este documento mostra como criar recursos para os dados armazenados no contêiner de blobs do Azure usando o pacote Python [Pandas](http://pandas.pydata.org/) .</span><span class="sxs-lookup"><span data-stu-id="5aaa8-104">This document shows how to create features for data that is stored in Azure blob container using the [Pandas](http://pandas.pydata.org/) Python package.</span></span> <span data-ttu-id="5aaa8-105">Depois de descrever como carregar os dados em um quadro de dados do Panda, ele mostrará como gerar recursos categóricos usando os scripts Python com os valores de indicador e recursos de agrupamento.</span><span class="sxs-lookup"><span data-stu-id="5aaa8-105">After outlining how to load the data into a Panda data frame, it shows how to generate categorical features using Python scripts with indicator values and binning features.</span></span>

[!INCLUDE [cap-create-features-data-selector](../../includes/cap-create-features-selector.md)]

<span data-ttu-id="5aaa8-106">Este **menu** leva você até os tópicos que descrevem como criar recursos para dados em vários ambientes.</span><span class="sxs-lookup"><span data-stu-id="5aaa8-106">This **menu** links to topics that describe how to create features for data in various environments.</span></span> <span data-ttu-id="5aaa8-107">Essa tarefa é uma etapa no [TDSP (Processo de Ciência de Dados de Equipe)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span><span class="sxs-lookup"><span data-stu-id="5aaa8-107">This task is a step in the [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5aaa8-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="5aaa8-108">Prerequisites</span></span>
<span data-ttu-id="5aaa8-109">Este artigo pressupõe que você criou uma conta de armazenamento de blobs do Azure e armazenou os dados lá.</span><span class="sxs-lookup"><span data-stu-id="5aaa8-109">This article assumes that you have created an Azure blob storage account and have stored your data there.</span></span> <span data-ttu-id="5aaa8-110">Se você precisar de instruções para configurar uma conta, confira [Criar uma conta de Armazenamento do Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="5aaa8-110">If you need instructions to set up an account, see [Create an Azure Storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span></span>

## <a name="load-the-data-into-a-pandas-data-frame"></a><span data-ttu-id="5aaa8-111">Carregar os dados em um quadro de dados Pandas</span><span class="sxs-lookup"><span data-stu-id="5aaa8-111">Load the data into a Pandas data frame</span></span>
<span data-ttu-id="5aaa8-112">Para explorar e manipular um conjunto de dados, eles devem ser baixados da fonte de blob para um arquivo local, que pode então ser carregado em um quadro de dados Pandas.</span><span class="sxs-lookup"><span data-stu-id="5aaa8-112">In order to do explore and manipulate a dataset, it must be downloaded from the blob source to a local file which can then be loaded in a Pandas data frame.</span></span> <span data-ttu-id="5aaa8-113">Aqui estão as etapas para este procedimento:</span><span class="sxs-lookup"><span data-stu-id="5aaa8-113">Here are the steps to follow for this procedure:</span></span>

1. <span data-ttu-id="5aaa8-114">Baixe os dados do Blob do Azure com o seguinte código de Python de exemplo e usando o serviço blob a seguir.</span><span class="sxs-lookup"><span data-stu-id="5aaa8-114">Download the data from Azure blob with the following sample Python code using blob service.</span></span> <span data-ttu-id="5aaa8-115">Substitua a variável no código abaixo pelos valores específicos:</span><span class="sxs-lookup"><span data-stu-id="5aaa8-115">Replace the variable in the code below with your specific values:</span></span>
   
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
2. <span data-ttu-id="5aaa8-116">Leia os dados em um quadro de dados Pandas do arquivo baixado.</span><span class="sxs-lookup"><span data-stu-id="5aaa8-116">Read the data into a Pandas data-frame from the downloaded file.</span></span>
   
        #LOCALFILE is the file path
        dataframe_blobdata = pd.read_csv(LOCALFILE)

<span data-ttu-id="5aaa8-117">Agora você está pronto para explorar os dados e gerar recursos neste conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="5aaa8-117">Now you are ready to explore the data and generate features on this dataset.</span></span>

## <span data-ttu-id="5aaa8-118"><a name="blob-featuregen"></a>Geração de recursos</span><span class="sxs-lookup"><span data-stu-id="5aaa8-118"><a name="blob-featuregen"></a>Feature Generation</span></span>
<span data-ttu-id="5aaa8-119">As duas seções a seguir mostram como gerar recursos categóricos com valores de indicador e de compartimentalização usando scripts Python.</span><span class="sxs-lookup"><span data-stu-id="5aaa8-119">The next two sections show how to generate categorical features with indicator values and binning features using Python scripts.</span></span>

### <span data-ttu-id="5aaa8-120"><a name="blob-countfeature"></a>Geração de Recursos baseada no valor do indicador</span><span class="sxs-lookup"><span data-stu-id="5aaa8-120"><a name="blob-countfeature"></a>Indicator value based Feature Generation</span></span>
<span data-ttu-id="5aaa8-121">Recursos categóricos podem ser criados da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="5aaa8-121">Categorical features can be created as follows:</span></span>

1. <span data-ttu-id="5aaa8-122">Inspecionar a distribuição da coluna categórica:</span><span class="sxs-lookup"><span data-stu-id="5aaa8-122">Inspect the distribution of the categorical column:</span></span>
   
        dataframe_blobdata['<categorical_column>'].value_counts()
2. <span data-ttu-id="5aaa8-123">Gerar valores de indicador para cada um dos valores da coluna</span><span class="sxs-lookup"><span data-stu-id="5aaa8-123">Generate indicator values for each of the column values</span></span>
   
        #generate the indicator column
        dataframe_blobdata_identity = pd.get_dummies(dataframe_blobdata['<categorical_column>'], prefix='<categorical_column>_identity')
3. <span data-ttu-id="5aaa8-124">Unir a coluna de indicador com o quadro de dados original</span><span class="sxs-lookup"><span data-stu-id="5aaa8-124">Join the indicator column with the original data frame</span></span>
   
            #Join the dummy variables back to the original data frame
            dataframe_blobdata_with_identity = dataframe_blobdata.join(dataframe_blobdata_identity)
4. <span data-ttu-id="5aaa8-125">Remover a própria variável original:</span><span class="sxs-lookup"><span data-stu-id="5aaa8-125">Remove the original variable itself:</span></span>
   
        #Remove the original column rate_code in df1_with_dummy
        dataframe_blobdata_with_identity.drop('<categorical_column>', axis=1, inplace=True)

### <span data-ttu-id="5aaa8-126"><a name="blob-binningfeature"></a>Agrupamento da Geração de Recursos</span><span class="sxs-lookup"><span data-stu-id="5aaa8-126"><a name="blob-binningfeature"></a>Binning Feature Generation</span></span>
<span data-ttu-id="5aaa8-127">Para gerar recursos compartimentalizados, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="5aaa8-127">For generating binned features, we proceed as follows:</span></span>

1. <span data-ttu-id="5aaa8-128">Adicione uma sequência de colunas a ser compartimentalizada a coluna numérica</span><span class="sxs-lookup"><span data-stu-id="5aaa8-128">Add a sequence of columns to bin a numeric column</span></span>
   
        bins = [0, 1, 2, 4, 10, 40]
        dataframe_blobdata_bin_id = pd.cut(dataframe_blobdata['<numeric_column>'], bins)
2. <span data-ttu-id="5aaa8-129">Converta a compartimentalização em uma sequência de variáveis boolianas</span><span class="sxs-lookup"><span data-stu-id="5aaa8-129">Convert binning to a sequence of boolean variables</span></span>
   
        dataframe_blobdata_bin_bool = pd.get_dummies(dataframe_blobdata_bin_id, prefix='<numeric_column>')
3. <span data-ttu-id="5aaa8-130">Por fim, associe as variáveis fictícias ao quadro de dados original</span><span class="sxs-lookup"><span data-stu-id="5aaa8-130">Finally, Join the dummy variables back to the original data frame</span></span>
   
        dataframe_blobdata_with_bin_bool = dataframe_blobdata.join(dataframe_blobdata_bin_bool)

## <span data-ttu-id="5aaa8-131">
            <a name="sql-featuregen">
            </a>Gravar dados de volta ao blob do Azure e consumi-los no Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="5aaa8-131"><a name="sql-featuregen"></a>Writing data back to Azure blob and consuming in Azure Machine Learning</span></span>
<span data-ttu-id="5aaa8-132">Depois que você já explorou os dados e criou os recursos necessários, pode carregar os dados (amostra ou recurso) para um blob do Azure e consumi-los no Azure Machine Learning usando as seguintes etapas: observe que os recursos adicionais podem ser criados no Azure Machine Learning Studio também.</span><span class="sxs-lookup"><span data-stu-id="5aaa8-132">After you have explored the data and created the necessary features, you can upload the data (sampled or featurized) to an Azure blob and consume it in Azure Machine Learning using the following steps: Note that additional features can be created in the Azure Machine Learning Studio as well.</span></span>

1. <span data-ttu-id="5aaa8-133">Grave o quadro de dados no arquivo local</span><span class="sxs-lookup"><span data-stu-id="5aaa8-133">Write the data frame to local file</span></span>
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)
2. <span data-ttu-id="5aaa8-134">Carregue os dados para o blob do Azure da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="5aaa8-134">Upload the data to Azure blob as follows:</span></span>
   
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
3. <span data-ttu-id="5aaa8-135">Agora, os dados podem ser lidos do blob usando o módulo [Importar Dados](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) do Azure Machine Learning, como mostra a tela abaixo:</span><span class="sxs-lookup"><span data-stu-id="5aaa8-135">Now the data can be read from the blob using the Azure Machine Learning [Import Data](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) module as shown in the screen below:</span></span>

![blob de leitor](./media/machine-learning-data-science-process-data-blob/reader_blob.png)

