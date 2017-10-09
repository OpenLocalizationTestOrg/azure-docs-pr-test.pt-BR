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
# <a name="heading"></a>Processar dados de blob do Azure com análises avançadas
Este documento aborda a exploração de dados e a geração de recursos por meio dos dados armazenados no Armazenamento de Blob do Azure. 

## <a name="load-hello-data-into-a-pandas-data-frame"></a>Saudação de carregar dados em um quadro de dados Pandas
Em ordem tooexplore e manipular um conjunto de dados, ela deve ser baixada de saudação blob fonte tooa arquivo local que, em seguida, pode ser carregado em um quadro de dados Pandas. Aqui estão Olá etapas toofollow para este procedimento:

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

## <a name="blob-dataexploration"></a>Exploração de Dados
Aqui estão alguns exemplos de maneiras tooexplore dados usando Pandas:

1. Inspecione o número de saudação de linhas e colunas 
   
        print 'hello size of hello data is: %d rows and  %d columns' % dataframe_blobdata.shape
2. Inspecionar Olá primeiro ou último algumas linhas no conjunto de dados hello como abaixo:
   
        dataframe_blobdata.head(10)
   
        dataframe_blobdata.tail(10)
3. Verifique cada coluna foi importada usando Olá código de exemplo a seguir de tipo de dados Olá
   
        for col in dataframe_blobdata.columns:
            print dataframe_blobdata[col].name, ':\t', dataframe_blobdata[col].dtype
4. Verifique as estatísticas de saudação básica para colunas de saudação do conjunto de dados de saudação da seguinte maneira
   
        dataframe_blobdata.describe()
5. Veja Olá número de entradas para cada valor de coluna da seguinte maneira
   
        dataframe_blobdata['<column_name>'].value_counts()
6. Contagem de valores ausentes em comparação com o número real de saudação de entradas em cada coluna usando Olá código de exemplo a seguir
   
        miss_num = dataframe_blobdata.shape[0] - dataframe_blobdata.count()
        print miss_num
7. Se você tiver valores ausentes para uma coluna específica em dados hello, pode descartá-los da seguinte maneira:
   
     dataframe_blobdata_noNA = dataframe_blobdata.dropna()   dataframe_blobdata_noNA.shape
   
   É outra maneira tooreplace os valores ausentes com a função de modo hello:
   
     dataframe_blobdata_mode = dataframe_blobdata.fillna({'<column_name>':dataframe_blobdata['<column_name>'].mode()[0]})        
8. Criar um gráfico de histograma usando um número variável de distribuição de saudação tooplot compartimentos de uma variável    
   
        dataframe_blobdata['<column_name>'].value_counts().plot(kind='bar')
   
        np.log(dataframe_blobdata['<column_name>']+1).hist(bins=50)
9. Examinar correlações entre variáveis usando um scatterplot ou função de correlação internos hello
   
        #relationship between column_a and column_b using scatter plot
        plt.scatter(dataframe_blobdata['<column_a>'], dataframe_blobdata['<column_b>'])
   
        #correlation between column_a and column_b
        dataframe_blobdata[['<column_a>', '<column_b>']].corr()

## <a name="blob-featuregen"></a>Geração de recursos
Podemos gerar recursos usando o Python da seguinte maneira:

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
3. Agora Olá dados podem ser lidos do uso de blob Olá Olá aprendizado de máquina do Azure [importar dados] [ import-data] módulo, como mostrado na tela hello abaixo:

![blob de leitor][1]

[1]: ./media/machine-learning-data-science-process-data-blob/reader_blob.png


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/

