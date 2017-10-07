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
# <a name="heading"></a>Dados de exemplo no armazenamento de blob do Azure
Este documento aborda os dados de amostragem armazenados no armazenamento de blobs do Azure, baixando-os de forma programática e realizando amostragem usando procedimentos escritos em Python.

a seguir Olá **menu** links tootopics que descrevem como toosample dados de vários ambientes de armazenamento. 

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

**Por que fazer amostragem dos dados?**
Se dataset Olá planejar tooanalyze for grande, normalmente é um tooreduce de dados de exemplo toodown Olá boa ideia-tooa menor, mas representativo e mais fácil de gerenciar o tamanho. Isso facilita a compreensão de dados, exploração e engenharia de recursos. Sua função no hello o processo de análise do Cortana é tooenable rápida criação de protótipos de funções de processamento de dados de saudação e modelos de aprendizado de máquina.

Esta tarefa de amostragem é uma etapa Olá [processo de ciência de dados da equipe (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).

## <a name="download-and-down-sample-data"></a>Baixar e reduzir os dados de exemplo
1. Baixe dados de saudação do armazenamento de BLOBs do Azure usando o serviço de blob de saudação do hello código Python de exemplo a seguir: 
   
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

2. Ler dados em um quadro de dados Pandas do arquivo hello baixado anteriormente.
   
        import pandas as pd
   
        #directly ready from file on disk
        dataframe_blobdata = pd.read_csv(LOCALFILE)

3. Baixo-exemplo dados hello usando Olá `numpy`do `random.choice` da seguinte maneira:
   
        # A 1 percent sample
        sample_ratio = 0.01 
        sample_size = np.round(dataframe_blobdata.shape[0] * sample_ratio)
        sample_rows = np.random.choice(dataframe_blobdata.index.values, sample_size)
        dataframe_blobdata_sample = dataframe_blobdata.ix[sample_rows]

Agora você pode trabalhar com hello acima do quadro de dados com exemplo de 1 por cento Olá para exploração adicional e geração de recurso.

## 
            <a name="heading">
            </a>Carregar os dados e lê-los no Azure Machine Learning
Você pode usar dados de exemplo toodown Olá de código de exemplo a seguir de saudação e usá-lo diretamente no aprendizado de máquina do Azure:

1. Gravar arquivo local do hello dados quadro tooa
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)

2. Carregar tooan de arquivo local hello Azure blob usando Olá código de exemplo a seguir:
   
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

3. Ler dados de saudação do hello BLOBs do Azure usando o aprendizado de máquina do Azure [importar dados](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) conforme mostrado na imagem de saudação abaixo:

![blob de leitor](./media/machine-learning-data-science-sample-data-blob/reader_blob.png)

