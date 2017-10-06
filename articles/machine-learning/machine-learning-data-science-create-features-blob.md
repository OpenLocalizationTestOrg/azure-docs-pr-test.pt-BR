---
title: usando Panda de dados de armazenamento de blob de aaaCreate recursos do Azure | Microsoft Docs
description: "Como toocreate recursos para dados armazenados no contêiner de BLOBs do Azure com o pacote do Python Panda hello."
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
ms.openlocfilehash: 8594046c5d76a36ad87fc77e407752489d30afcc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-features-for-azure-blob-storage-data-using-panda"></a><span data-ttu-id="d5251-103">Criar recursos para dados de armazenamento de blob do Azure usando o Panda</span><span class="sxs-lookup"><span data-stu-id="d5251-103">Create features for Azure blob storage data using Panda</span></span>
<span data-ttu-id="d5251-104">Este documento mostra como os recursos de toocreate para dados armazenados no contêiner de BLOBs do Azure usando Olá [Pandas](http://pandas.pydata.org/) pacote do Python.</span><span class="sxs-lookup"><span data-stu-id="d5251-104">This document shows how toocreate features for data that is stored in Azure blob container using hello [Pandas](http://pandas.pydata.org/) Python package.</span></span> <span data-ttu-id="d5251-105">Depois de estrutura de tópicos como dados de saudação tooload em um quadro de dados Panda, ele mostra como recursos categóricos do toogenerate usando scripts Python com valores de indicador e recursos de agrupamento.</span><span class="sxs-lookup"><span data-stu-id="d5251-105">After outlining how tooload hello data into a Panda data frame, it shows how toogenerate categorical features using Python scripts with indicator values and binning features.</span></span>

[!INCLUDE [cap-create-features-data-selector](../../includes/cap-create-features-selector.md)]

<span data-ttu-id="d5251-106">Isso **menu** links tootopics que descrevem como toocreate recursos para os dados em vários ambientes.</span><span class="sxs-lookup"><span data-stu-id="d5251-106">This **menu** links tootopics that describe how toocreate features for data in various environments.</span></span> <span data-ttu-id="d5251-107">Essa tarefa é uma etapa Olá [processo de ciência de dados da equipe (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span><span class="sxs-lookup"><span data-stu-id="d5251-107">This task is a step in hello [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d5251-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="d5251-108">Prerequisites</span></span>
<span data-ttu-id="d5251-109">Este artigo pressupõe que você criou uma conta de armazenamento de blobs do Azure e armazenou os dados lá.</span><span class="sxs-lookup"><span data-stu-id="d5251-109">This article assumes that you have created an Azure blob storage account and have stored your data there.</span></span> <span data-ttu-id="d5251-110">Se você precisar de instruções tooset uma conta, consulte [criar uma conta de armazenamento do Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="d5251-110">If you need instructions tooset up an account, see [Create an Azure Storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span></span>

## <a name="load-hello-data-into-a-pandas-data-frame"></a><span data-ttu-id="d5251-111">Saudação de carregar dados em um quadro de dados Pandas</span><span class="sxs-lookup"><span data-stu-id="d5251-111">Load hello data into a Pandas data frame</span></span>
<span data-ttu-id="d5251-112">Em ordem toodo explorar e manipular um conjunto de dados, ela deve ser baixada de saudação blob fonte tooa arquivo local que, em seguida, pode ser carregado em um quadro de dados Pandas.</span><span class="sxs-lookup"><span data-stu-id="d5251-112">In order toodo explore and manipulate a dataset, it must be downloaded from hello blob source tooa local file which can then be loaded in a Pandas data frame.</span></span> <span data-ttu-id="d5251-113">Aqui estão Olá etapas toofollow para este procedimento:</span><span class="sxs-lookup"><span data-stu-id="d5251-113">Here are hello steps toofollow for this procedure:</span></span>

1. <span data-ttu-id="d5251-114">Baixar dados de saudação do Azure blob com hello seguindo o código Python de exemplo usando o serviço blob.</span><span class="sxs-lookup"><span data-stu-id="d5251-114">Download hello data from Azure blob with hello following sample Python code using blob service.</span></span> <span data-ttu-id="d5251-115">Substitua variável Olá no código Olá abaixo com seus valores específicos:</span><span class="sxs-lookup"><span data-stu-id="d5251-115">Replace hello variable in hello code below with your specific values:</span></span>
   
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
2. <span data-ttu-id="d5251-116">Saudação de ler dados em um quadro de dados Pandas de saudação download de arquivo.</span><span class="sxs-lookup"><span data-stu-id="d5251-116">Read hello data into a Pandas data-frame from hello downloaded file.</span></span>
   
        #LOCALFILE is hello file path
        dataframe_blobdata = pd.read_csv(LOCALFILE)

<span data-ttu-id="d5251-117">Agora você está pronto tooexplore Olá dados e gerar recursos nesse conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="d5251-117">Now you are ready tooexplore hello data and generate features on this dataset.</span></span>

## <span data-ttu-id="d5251-118"><a name="blob-featuregen"></a>Geração de recursos</span><span class="sxs-lookup"><span data-stu-id="d5251-118"><a name="blob-featuregen"></a>Feature Generation</span></span>
<span data-ttu-id="d5251-119">duas seções seguintes Olá mostram como toogenerate de recursos categóricos com valores de indicador e o agrupamento de recursos usando scripts de Python.</span><span class="sxs-lookup"><span data-stu-id="d5251-119">hello next two sections show how toogenerate categorical features with indicator values and binning features using Python scripts.</span></span>

### <span data-ttu-id="d5251-120"><a name="blob-countfeature"></a>Geração de Recursos baseada no valor do indicador</span><span class="sxs-lookup"><span data-stu-id="d5251-120"><a name="blob-countfeature"></a>Indicator value based Feature Generation</span></span>
<span data-ttu-id="d5251-121">Recursos categóricos podem ser criados da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="d5251-121">Categorical features can be created as follows:</span></span>

1. <span data-ttu-id="d5251-122">Inspecione a distribuição de saudação de coluna categórica hello:</span><span class="sxs-lookup"><span data-stu-id="d5251-122">Inspect hello distribution of hello categorical column:</span></span>
   
        dataframe_blobdata['<categorical_column>'].value_counts()
2. <span data-ttu-id="d5251-123">Gerar valores de indicador para cada um dos valores da coluna Olá</span><span class="sxs-lookup"><span data-stu-id="d5251-123">Generate indicator values for each of hello column values</span></span>
   
        #generate hello indicator column
        dataframe_blobdata_identity = pd.get_dummies(dataframe_blobdata['<categorical_column>'], prefix='<categorical_column>_identity')
3. <span data-ttu-id="d5251-124">Unir a coluna de indicador Olá com quadro de dados original Olá</span><span class="sxs-lookup"><span data-stu-id="d5251-124">Join hello indicator column with hello original data frame</span></span>
   
            #Join hello dummy variables back toohello original data frame
            dataframe_blobdata_with_identity = dataframe_blobdata.join(dataframe_blobdata_identity)
4. <span data-ttu-id="d5251-125">Remova Olá original variável:</span><span class="sxs-lookup"><span data-stu-id="d5251-125">Remove hello original variable itself:</span></span>
   
        #Remove hello original column rate_code in df1_with_dummy
        dataframe_blobdata_with_identity.drop('<categorical_column>', axis=1, inplace=True)

### <span data-ttu-id="d5251-126"><a name="blob-binningfeature"></a>Agrupamento da Geração de Recursos</span><span class="sxs-lookup"><span data-stu-id="d5251-126"><a name="blob-binningfeature"></a>Binning Feature Generation</span></span>
<span data-ttu-id="d5251-127">Para gerar recursos compartimentalizados, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="d5251-127">For generating binned features, we proceed as follows:</span></span>

1. <span data-ttu-id="d5251-128">Adicionar uma sequência de colunas toobin uma coluna numérica</span><span class="sxs-lookup"><span data-stu-id="d5251-128">Add a sequence of columns toobin a numeric column</span></span>
   
        bins = [0, 1, 2, 4, 10, 40]
        dataframe_blobdata_bin_id = pd.cut(dataframe_blobdata['<numeric_column>'], bins)
2. <span data-ttu-id="d5251-129">Converter a sequência de agrupamento tooa de variáveis Boolianas</span><span class="sxs-lookup"><span data-stu-id="d5251-129">Convert binning tooa sequence of boolean variables</span></span>
   
        dataframe_blobdata_bin_bool = pd.get_dummies(dataframe_blobdata_bin_id, prefix='<numeric_column>')
3. <span data-ttu-id="d5251-130">Por fim, unir o quadro de dados original do hello variáveis fictício toohello back</span><span class="sxs-lookup"><span data-stu-id="d5251-130">Finally, Join hello dummy variables back toohello original data frame</span></span>
   
        dataframe_blobdata_with_bin_bool = dataframe_blobdata.join(dataframe_blobdata_bin_bool)

## <span data-ttu-id="d5251-131"><a name="sql-featuregen"></a>Gravar dados de volta tooAzure blob e consumindo no aprendizado de máquina do Azure</span><span class="sxs-lookup"><span data-stu-id="d5251-131"><a name="sql-featuregen"></a>Writing data back tooAzure blob and consuming in Azure Machine Learning</span></span>
<span data-ttu-id="d5251-132">Depois de explorar dados saudação e criado Olá recursos necessários, você pode carregar dados saudação (amostra ou featurized) tooan Azure blob e consumi-lo no aprendizado de máquina do Azure usando Olá etapas a seguir: Observe que os recursos adicionais podem ser criados em Olá Azure Machine Learning Studio também.</span><span class="sxs-lookup"><span data-stu-id="d5251-132">After you have explored hello data and created hello necessary features, you can upload hello data (sampled or featurized) tooan Azure blob and consume it in Azure Machine Learning using hello following steps: Note that additional features can be created in hello Azure Machine Learning Studio as well.</span></span>

1. <span data-ttu-id="d5251-133">Gravar o arquivo de toolocal de quadro de dados Olá</span><span class="sxs-lookup"><span data-stu-id="d5251-133">Write hello data frame toolocal file</span></span>
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)
2. <span data-ttu-id="d5251-134">Carregar o blob de tooAzure dados Olá da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="d5251-134">Upload hello data tooAzure blob as follows:</span></span>
   
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
3. <span data-ttu-id="d5251-135">Agora Olá dados podem ser lidos do uso de blob Olá Olá aprendizado de máquina do Azure [importar dados](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) módulo, como mostrado na tela hello abaixo:</span><span class="sxs-lookup"><span data-stu-id="d5251-135">Now hello data can be read from hello blob using hello Azure Machine Learning [Import Data](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) module as shown in hello screen below:</span></span>

![blob de leitor](./media/machine-learning-data-science-process-data-blob/reader_blob.png)

