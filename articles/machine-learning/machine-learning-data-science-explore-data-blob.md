---
title: aaaExplore dados no Azure blob storage com Pandas | Microsoft Docs
description: "Como tooexplore dados armazenados no Azure blob contêiner usando Pandas."
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: feaa9e54-01e0-48c8-a917-1eba0f9d9ec7
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 28f3c0aebf2300006066c4b19dcb1f0a76a1deb2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="explore-data-in-azure-blob-storage-with-pandas"></a>Explorar dados no repositório de blob do Azure com o Pandas
Este documento aborda como tooexplore dados armazenados no Azure blob contêiner usando [Pandas](http://pandas.pydata.org/) pacote do Python.

a seguir Olá **menu** links tootopics que descrevem como toouse ferramentas tooexplore dados de vários ambientes de armazenamento. Essa tarefa é uma etapa Olá [processo de ciência de dados]().

[!INCLUDE [cap-explore-data-selector](../../includes/cap-explore-data-selector.md)]

## <a name="prerequisites"></a>Pré-requisitos
Este artigo supõe que você:

* Criou uma conta de armazenamento do Azure. Se precisar de instruções, confira [Criar uma conta de Armazenamento do Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account)
* Armazenar seus dados em uma conta de armazenamento de blob do Azure. Se você precisar de instruções, consulte [movendo dados tooand do armazenamento do Azure](../storage/common/storage-moving-data.md)

## <a name="load-hello-data-into-a-pandas-dataframe"></a>Saudação de carregar dados em um DataFrame Pandas
tooexplore e manipular um conjunto de dados, ele primeiro deve ser baixado do hello blob tooa local arquivo de origem, que então pode ser carregado em um DataFrame Pandas. Aqui estão Olá etapas toofollow para este procedimento:

1. Baixar dados de saudação do Azure blob com hello seguindo o exemplo de código Python usando o serviço blob. Substitua a variável Olá Olá código com seus valores específicos a seguir: 
   
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

## <a name="blob-dataexploration"></a>Exemplos de exploração de dados usando o Pandas
Aqui estão alguns exemplos de maneiras tooexplore dados usando Pandas:

1. Inspecionar Olá **número de linhas e colunas** 
   
        print 'hello size of hello data is: %d rows and  %d columns' % dataframe_blobdata.shape
2. **Inspecionar** Olá alguns primeiro ou últimos **linhas** em Olá conjunto de dados a seguir:
   
        dataframe_blobdata.head(10)
   
        dataframe_blobdata.tail(10)
3. Verificar Olá **tipo de dados** cada coluna foi importada usando Olá código de exemplo a seguir
   
        for col in dataframe_blobdata.columns:
            print dataframe_blobdata[col].name, ':\t', dataframe_blobdata[col].dtype
4. Verificar Olá **estatísticas básicas** para colunas Olá Olá conjunto de dados da seguinte maneira
   
        dataframe_blobdata.describe()
5. Veja Olá número de entradas para cada valor de coluna da seguinte maneira
   
        dataframe_blobdata['<column_name>'].value_counts()
6. **Contagem de valores ausentes** versus o número real de saudação de entradas em cada coluna usando Olá código de exemplo a seguir
   
        miss_num = dataframe_blobdata.shape[0] - dataframe_blobdata.count()
        print miss_num
7. Se você tiver **valores ausentes** para uma coluna específica em dados saudação, você poderá removê-los da seguinte maneira:
   
     dataframe_blobdata_noNA = dataframe_blobdata.dropna()   dataframe_blobdata_noNA.shape
   
   É outra maneira tooreplace os valores ausentes com a função de modo hello:
   
     dataframe_blobdata_mode = dataframe_blobdata.fillna({'<column_name>':dataframe_blobdata['<column_name>'].mode()[0]})        
8. Criar um **histograma** plotar usando um número variável de distribuição de saudação tooplot compartimentos de uma variável    
   
        dataframe_blobdata['<column_name>'].value_counts().plot(kind='bar')
   
        np.log(dataframe_blobdata['<column_name>']+1).hist(bins=50)
9. Examinar **correlações** entre variáveis usando um scatterplot ou função de correlação internos hello
   
        #relationship between column_a and column_b using scatter plot
        plt.scatter(dataframe_blobdata['<column_a>'], dataframe_blobdata['<column_b>'])
   
        #correlation between column_a and column_b
        dataframe_blobdata[['<column_a>', '<column_b>']].corr()

