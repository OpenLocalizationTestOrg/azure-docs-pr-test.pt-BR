---
title: Dados de exemplo no Armazenamento de Blobs do Azure| Microsoft Docs
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
ms.openlocfilehash: aa9ab454706429682a393c3d5758cebe20790e19
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <span data-ttu-id="1d38d-103"><a name="heading"></a>Dados de exemplo no armazenamento de blob do Azure</span><span class="sxs-lookup"><span data-stu-id="1d38d-103"><a name="heading"></a>Sample data in Azure blob storage</span></span>
<span data-ttu-id="1d38d-104">Este documento aborda os dados de amostragem armazenados no armazenamento de blobs do Azure, baixando-os de forma programática e realizando amostragem usando procedimentos escritos em Python.</span><span class="sxs-lookup"><span data-stu-id="1d38d-104">This document covers sampling data stored in Azure blob storage by downloading it programmatically and then sampling it using procedures written in Python.</span></span>

<span data-ttu-id="1d38d-105">O **menu** a seguir leva a tópicos que descrevem como obter dados de exemplo de vários ambientes de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="1d38d-105">The following **menu** links to topics that describe how to sample data from various storage environments.</span></span> 

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

<span data-ttu-id="1d38d-106">**Por que fazer amostragem dos dados?**</span><span class="sxs-lookup"><span data-stu-id="1d38d-106">**Why sample your data?**</span></span>
<span data-ttu-id="1d38d-107">Se o conjunto de dados que você deseja analisar for grande, geralmente, é uma boa ideia reduzir os dados para um tamanho menor, mas representativo e mais gerenciável.</span><span class="sxs-lookup"><span data-stu-id="1d38d-107">If the dataset you plan to analyze is large, it's usually a good idea to down-sample the data to reduce it to a smaller but representative and more manageable size.</span></span> <span data-ttu-id="1d38d-108">Isso facilita a compreensão de dados, exploração e engenharia de recursos.</span><span class="sxs-lookup"><span data-stu-id="1d38d-108">This facilitates data understanding, exploration, and feature engineering.</span></span> <span data-ttu-id="1d38d-109">Sua função no Processo de Análise do Cortana é habilitar a rápida criação de protótipos de funções de processamento de dados e modelos de aprendizado de máquina.</span><span class="sxs-lookup"><span data-stu-id="1d38d-109">Its role in the Cortana Analytics Process is to enable fast prototyping of the data processing functions and machine learning models.</span></span>

<span data-ttu-id="1d38d-110">Essa tarefa de amostragem é uma etapa do [TDSP (Processo de Ciência de Dados de Equipe)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span><span class="sxs-lookup"><span data-stu-id="1d38d-110">This sampling task is a step in the [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

## <a name="download-and-down-sample-data"></a><span data-ttu-id="1d38d-111">Baixar e reduzir os dados de exemplo</span><span class="sxs-lookup"><span data-stu-id="1d38d-111">Download and down-sample data</span></span>
1. <span data-ttu-id="1d38d-112">Baixe os dados do Armazenamento do Blobs do Azure usando o serviço blob com o código Python de exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="1d38d-112">Download the data from Azure blob storage using the blob service from the following sample Python code:</span></span> 
   
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

2. <span data-ttu-id="1d38d-113">Leia os dados em um quadro de dados Pandas do arquivo baixado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="1d38d-113">Read data into a Pandas data-frame from the file downloaded above.</span></span>
   
        import pandas as pd
   
        #directly ready from file on disk
        dataframe_blobdata = pd.read_csv(LOCALFILE)

3. <span data-ttu-id="1d38d-114">Reduza os dados usando o `random.choice` da `numpy`, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="1d38d-114">Down-sample the data using the `numpy`'s `random.choice` as follows:</span></span>
   
        # A 1 percent sample
        sample_ratio = 0.01 
        sample_size = np.round(dataframe_blobdata.shape[0] * sample_ratio)
        sample_rows = np.random.choice(dataframe_blobdata.index.values, sample_size)
        dataframe_blobdata_sample = dataframe_blobdata.ix[sample_rows]

<span data-ttu-id="1d38d-115">Agora você pode trabalhar com o quadro de dados acima com a amostra de 1 por cento para exploração e geração de recursos adicional.</span><span class="sxs-lookup"><span data-stu-id="1d38d-115">Now you can work with the above data frame with the 1 Percent sample for further exploration and feature generation.</span></span>

## <span data-ttu-id="1d38d-116">
            <a name="heading">
            </a>Carregar os dados e lê-los no Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="1d38d-116"><a name="heading"></a>Upload data and read it into Azure Machine Learning</span></span>
<span data-ttu-id="1d38d-117">É possível usar o código de exemplo a seguir para os reduzir os dados e usá-los diretamente no Azure Machine Learning:</span><span class="sxs-lookup"><span data-stu-id="1d38d-117">You can use the following sample code to down-sample the data and use it directly in Azure Machine Learning:</span></span>

1. <span data-ttu-id="1d38d-118">Escrever o quadro de dados em um arquivo local</span><span class="sxs-lookup"><span data-stu-id="1d38d-118">Write the data frame to a local file</span></span>
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)

2. <span data-ttu-id="1d38d-119">Carregue o arquivo local para um blob do Azure usando o seguinte código de exemplo:</span><span class="sxs-lookup"><span data-stu-id="1d38d-119">Upload the local file to an Azure blob using the following sample code:</span></span>
   
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
            print ("Something went wrong with uploading to the blob:"+ BLOBNAME)

3. <span data-ttu-id="1d38d-120">Leia os dados do blob do Azure usando o [Importar Dados](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) do Azure Machine Learning, como mostrado na imagem abaixo:</span><span class="sxs-lookup"><span data-stu-id="1d38d-120">Read the data from the Azure blob using Azure Machine Learning [Import Data](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) as shown in the image below:</span></span>

![blob de leitor](./media/machine-learning-data-science-sample-data-blob/reader_blob.png)

