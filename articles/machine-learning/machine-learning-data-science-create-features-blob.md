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
# <a name="create-features-for-azure-blob-storage-data-using-panda"></a>Criar recursos para dados de armazenamento de blob do Azure usando o Panda
Este documento mostra como os recursos de toocreate para dados armazenados no contêiner de BLOBs do Azure usando Olá [Pandas](http://pandas.pydata.org/) pacote do Python. Depois de estrutura de tópicos como dados de saudação tooload em um quadro de dados Panda, ele mostra como recursos categóricos do toogenerate usando scripts Python com valores de indicador e recursos de agrupamento.

[!INCLUDE [cap-create-features-data-selector](../../includes/cap-create-features-selector.md)]

Isso **menu** links tootopics que descrevem como toocreate recursos para os dados em vários ambientes. Essa tarefa é uma etapa Olá [processo de ciência de dados da equipe (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).

## <a name="prerequisites"></a>Pré-requisitos
Este artigo pressupõe que você criou uma conta de armazenamento de blobs do Azure e armazenou os dados lá. Se você precisar de instruções tooset uma conta, consulte [criar uma conta de armazenamento do Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account)

## <a name="load-hello-data-into-a-pandas-data-frame"></a>Saudação de carregar dados em um quadro de dados Pandas
Em ordem toodo explorar e manipular um conjunto de dados, ela deve ser baixada de saudação blob fonte tooa arquivo local que, em seguida, pode ser carregado em um quadro de dados Pandas. Aqui estão Olá etapas toofollow para este procedimento:

1. Baixar dados de saudação do Azure blob com hello seguindo o código Python de exemplo usando o serviço blob. Substitua variável Olá no código Olá abaixo com seus valores específicos:
   
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
2. Saudação de ler dados em um quadro de dados Pandas de saudação download de arquivo.
   
        #LOCALFILE is hello file path
        dataframe_blobdata = pd.read_csv(LOCALFILE)

Agora você está pronto tooexplore Olá dados e gerar recursos nesse conjunto de dados.

## <a name="blob-featuregen"></a>Geração de recursos
duas seções seguintes Olá mostram como toogenerate de recursos categóricos com valores de indicador e o agrupamento de recursos usando scripts de Python.

### <a name="blob-countfeature"></a>Geração de Recursos baseada no valor do indicador
Recursos categóricos podem ser criados da seguinte maneira:

1. Inspecione a distribuição de saudação de coluna categórica hello:
   
        dataframe_blobdata['<categorical_column>'].value_counts()
2. Gerar valores de indicador para cada um dos valores da coluna Olá
   
        #generate hello indicator column
        dataframe_blobdata_identity = pd.get_dummies(dataframe_blobdata['<categorical_column>'], prefix='<categorical_column>_identity')
3. Unir a coluna de indicador Olá com quadro de dados original Olá
   
            #Join hello dummy variables back toohello original data frame
            dataframe_blobdata_with_identity = dataframe_blobdata.join(dataframe_blobdata_identity)
4. Remova Olá original variável:
   
        #Remove hello original column rate_code in df1_with_dummy
        dataframe_blobdata_with_identity.drop('<categorical_column>', axis=1, inplace=True)

### <a name="blob-binningfeature"></a>Agrupamento da Geração de Recursos
Para gerar recursos compartimentalizados, faça o seguinte:

1. Adicionar uma sequência de colunas toobin uma coluna numérica
   
        bins = [0, 1, 2, 4, 10, 40]
        dataframe_blobdata_bin_id = pd.cut(dataframe_blobdata['<numeric_column>'], bins)
2. Converter a sequência de agrupamento tooa de variáveis Boolianas
   
        dataframe_blobdata_bin_bool = pd.get_dummies(dataframe_blobdata_bin_id, prefix='<numeric_column>')
3. Por fim, unir o quadro de dados original do hello variáveis fictício toohello back
   
        dataframe_blobdata_with_bin_bool = dataframe_blobdata.join(dataframe_blobdata_bin_bool)

## <a name="sql-featuregen"></a>Gravar dados de volta tooAzure blob e consumindo no aprendizado de máquina do Azure
Depois de explorar dados saudação e criado Olá recursos necessários, você pode carregar dados saudação (amostra ou featurized) tooan Azure blob e consumi-lo no aprendizado de máquina do Azure usando Olá etapas a seguir: Observe que os recursos adicionais podem ser criados em Olá Azure Machine Learning Studio também.

1. Gravar o arquivo de toolocal de quadro de dados Olá
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)
2. Carregar o blob de tooAzure dados Olá da seguinte maneira:
   
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
3. Agora Olá dados podem ser lidos do uso de blob Olá Olá aprendizado de máquina do Azure [importar dados](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) módulo, como mostrado na tela hello abaixo:

![blob de leitor](./media/machine-learning-data-science-process-data-blob/reader_blob.png)

