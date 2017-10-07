---
title: armazenamento de blob de dados aaaSample no Azure | Microsoft Docs
description: Dados de exemplo no armazenamento de blob do Azure
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: e8d9ad2c-86c5-43d6-80b8-d355b5c0dccf
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: fashah;garye;bradsev
ms.openlocfilehash: cceadf1fb1fb4804fc5b5a3da55c82854651026e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <span data-ttu-id="103e8-103"><a name="heading"></a>Dados de exemplo no armazenamento de blob do Azure</span><span class="sxs-lookup"><span data-stu-id="103e8-103"><a name="heading"></a>Sample data in Azure blob storage</span></span>
<span data-ttu-id="103e8-104">Este documento aborda os dados de amostragem armazenados no armazenamento de blobs do Azure, baixando-os de forma programática e realizando amostragem usando procedimentos escritos em Python.</span><span class="sxs-lookup"><span data-stu-id="103e8-104">This document covers sampling data stored in Azure blob storage by downloading it programmatically and then sampling it using procedures written in Python.</span></span>

<span data-ttu-id="103e8-105">a seguir Olá **menu** links tootopics que descrevem como toosample dados de vários ambientes de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="103e8-105">hello following **menu** links tootopics that describe how toosample data from various storage environments.</span></span> 

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

<span data-ttu-id="103e8-106">**Por que fazer amostragem dos dados?**</span><span class="sxs-lookup"><span data-stu-id="103e8-106">**Why sample your data?**</span></span>
<span data-ttu-id="103e8-107">Se dataset Olá planejar tooanalyze for grande, normalmente é um tooreduce de dados de exemplo toodown Olá boa ideia-tooa menor, mas representativo e mais fácil de gerenciar o tamanho.</span><span class="sxs-lookup"><span data-stu-id="103e8-107">If hello dataset you plan tooanalyze is large, it's usually a good idea toodown-sample hello data tooreduce it tooa smaller but representative and more manageable size.</span></span> <span data-ttu-id="103e8-108">Isso facilita a compreensão de dados, exploração e engenharia de recursos.</span><span class="sxs-lookup"><span data-stu-id="103e8-108">This facilitates data understanding, exploration, and feature engineering.</span></span> <span data-ttu-id="103e8-109">Sua função no hello o processo de análise do Cortana é tooenable rápida criação de protótipos de funções de processamento de dados de saudação e modelos de aprendizado de máquina.</span><span class="sxs-lookup"><span data-stu-id="103e8-109">Its role in hello Cortana Analytics Process is tooenable fast prototyping of hello data processing functions and machine learning models.</span></span>

<span data-ttu-id="103e8-110">Esta tarefa de amostragem é uma etapa Olá [processo de ciência de dados da equipe (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span><span class="sxs-lookup"><span data-stu-id="103e8-110">This sampling task is a step in hello [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

## <a name="download-and-down-sample-data"></a><span data-ttu-id="103e8-111">Baixar e reduzir os dados de exemplo</span><span class="sxs-lookup"><span data-stu-id="103e8-111">Download and down-sample data</span></span>
1. <span data-ttu-id="103e8-112">Baixe dados de saudação do armazenamento de BLOBs do Azure usando o serviço de blob de saudação do hello código Python de exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="103e8-112">Download hello data from Azure blob storage using hello blob service from hello following sample Python code:</span></span> 
   
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

2. <span data-ttu-id="103e8-113">Ler dados em um quadro de dados Pandas do arquivo hello baixado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="103e8-113">Read data into a Pandas data-frame from hello file downloaded above.</span></span>
   
        import pandas as pd
   
        #directly ready from file on disk
        dataframe_blobdata = pd.read_csv(LOCALFILE)

3. <span data-ttu-id="103e8-114">Baixo-exemplo dados hello usando Olá `numpy`do `random.choice` da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="103e8-114">Down-sample hello data using hello `numpy`'s `random.choice` as follows:</span></span>
   
        # A 1 percent sample
        sample_ratio = 0.01 
        sample_size = np.round(dataframe_blobdata.shape[0] * sample_ratio)
        sample_rows = np.random.choice(dataframe_blobdata.index.values, sample_size)
        dataframe_blobdata_sample = dataframe_blobdata.ix[sample_rows]

<span data-ttu-id="103e8-115">Agora você pode trabalhar com hello acima do quadro de dados com exemplo de 1 por cento Olá para exploração adicional e geração de recurso.</span><span class="sxs-lookup"><span data-stu-id="103e8-115">Now you can work with hello above data frame with hello 1 Percent sample for further exploration and feature generation.</span></span>

## <span data-ttu-id="103e8-116">
            <a name="heading">
            </a>Carregar os dados e lê-los no Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="103e8-116"><a name="heading"></a>Upload data and read it into Azure Machine Learning</span></span>
<span data-ttu-id="103e8-117">Você pode usar dados de exemplo toodown Olá de código de exemplo a seguir de saudação e usá-lo diretamente no aprendizado de máquina do Azure:</span><span class="sxs-lookup"><span data-stu-id="103e8-117">You can use hello following sample code toodown-sample hello data and use it directly in Azure Machine Learning:</span></span>

1. <span data-ttu-id="103e8-118">Gravar arquivo local do hello dados quadro tooa</span><span class="sxs-lookup"><span data-stu-id="103e8-118">Write hello data frame tooa local file</span></span>
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)

2. <span data-ttu-id="103e8-119">Carregar tooan de arquivo local hello Azure blob usando Olá código de exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="103e8-119">Upload hello local file tooan Azure blob using hello following sample code:</span></span>
   
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
            print ("Something went wrong with uploading toohello blob:"+ BLOBNAME)

3. <span data-ttu-id="103e8-120">Ler dados de saudação do hello BLOBs do Azure usando o aprendizado de máquina do Azure [importar dados](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) conforme mostrado na imagem de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="103e8-120">Read hello data from hello Azure blob using Azure Machine Learning [Import Data](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) as shown in hello image below:</span></span>

![blob de leitor](./media/machine-learning-data-science-sample-data-blob/reader_blob.png)

