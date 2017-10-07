---
title: aaaSample dados no SQL Server no Azure | Microsoft Docs
description: Dados de exemplo no SQL Server no Azure
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 33c030d4-5cca-4cc9-99d7-2bd13a3926af
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: fashah;garye;bradsev
ms.openlocfilehash: dc7f9529c771f6deb633775557e64a04b774f5b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="heading"></a>Dados de exemplo no SQL Server no Azure
Este documento mostra como toosample dados armazenados no SQL Server no Azure usando SQL ou Olá linguagem de programação Python. Ele também mostra como toomove dados de amostra no aprendizado de máquina do Azure, salvando-o arquivo tooa, carregando-tooan BLOBs do Azure e, em seguida, lê-los no estúdio de aprendizado de máquina do Azure.

amostragem de Python Olá usa Olá [pyodbc](https://code.google.com/p/pyodbc/) tooSQL tooconnect da biblioteca ODBC Server no Azure e hello [Pandas](http://pandas.pydata.org/) amostragem de saudação do toodo de biblioteca.

> [!NOTE]
> código SQL de exemplo Hello neste documento pressupõe que Olá dados estão em um SQL Server no Azure. Se não for, consulte muito[mover dados tooSQL Server no Azure](machine-learning-data-science-move-sql-server-virtual-machine.md) tópico para obter instruções sobre como toomove tooSQL seus dados Server no Azure.
> 
> 

a seguir Olá **menu** links tootopics que descrevem como toosample dados de vários ambientes de armazenamento. 

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

**Por que fazer amostragem dos dados?**
Se dataset Olá planejar tooanalyze for grande, normalmente é um tooreduce de dados de exemplo toodown Olá boa ideia-tooa menor, mas representativo e mais fácil de gerenciar o tamanho. Isso facilita a compreensão de dados, exploração e engenharia de recursos. Sua função no hello [processo de ciência de dados da equipe (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) é tooenable rápida criação de protótipos de funções de processamento de dados de saudação e modelos de aprendizado de máquina.

Esta tarefa de amostragem é uma etapa Olá [processo de ciência de dados da equipe (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).

## <a name="SQL"></a>Usando o SQL
Esta seção descreve vários métodos usando SQL tooperform amostragem aleatória simples em relação aos dados Olá Olá de banco de dados. Escolha um método com base no tamanho e na distribuição dos seus dados.

Olá dois itens a seguir mostram como newid toouse no SQL Server tooperform Olá amostragem. Olá método escolhido depende aleatório como você deseja toobe do exemplo hello (pk_id no código de exemplo hello abaixo é considerado toobe uma chave primária gerada automaticamente).

1. Menos rígido do exemplo aleatório
   
        select  * from <table_name> where <primary_key> in 
        (select top 10 percent <primary_key> from <table_name> order by newid())
2. Exemplo mais aleatório 
   
        SELECT * FROM <table_name>
        WHERE 0.1 >= CAST(CHECKSUM(NEWID(), <primary_key>) & 0x7fffffff AS float)/ CAST (0x7fffffff AS int)

TABLESAMPLE pode ser usado para amostragem conforme demonstrado a seguir. Isso pode ser uma abordagem melhor se o tamanho de dados for grande (supondo que não estão correlacionados dados em diferentes páginas) e para Olá toocomplete de consulta em um tempo razoável.

    SELECT *
    FROM <table_name> 
    TABLESAMPLE (10 PERCENT)

> [!NOTE]
> Você pode explorar e gerar recursos por meio desses dados amostrados armazenando-os em uma nova tabela
> 
> 

### <a name="sql-aml"></a>Conectando tooAzure aprendizado de máquina
Você pode usar consultas de exemplo hello acima diretamente no hello aprendizado de máquina do Azure [importar dados] [ import-data] dados de exemplo toodown Olá de módulo Olá surgir e colocá-lo em uma experiência de aprendizado de máquina do Azure. Abaixo está uma captura de tela do uso de dados de amostra de saudação Olá leitor módulo tooread:

![sql leitor][1]

## <a name="python"></a>Usando a linguagem de programação de Python Olá
Esta seção demonstra como usar o hello [pyodbc biblioteca](https://code.google.com/p/pyodbc/) tooestablish ODBC se conectar a banco de dados do servidor SQL de tooa em Python. cadeia de conexão de banco de dados de saudação é o seguinte: (replace servername, dbname, nome de usuário e senha com a sua configuração):

    #Set up hello SQL Azure connection
    import pyodbc    
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

Olá [Pandas](http://pandas.pydata.org/) biblioteca do Python fornece um rico conjunto de ferramentas de análise de dados e estruturas de dados para a manipulação de dados para programação Python. código de saudação abaixo lê um exemplo de 0,1% dos dados de saudação de uma tabela no banco de dados do SQL Azure para os dados Pandas:

    import pandas as pd

    # Query database and load hello returned results in pandas data frame
    data_frame = pd.read_sql('''select column1, cloumn2... from <table_name> tablesample (0.1 percent)''', conn)

Agora, você pode trabalhar com dados de amostra de saudação no quadro de dados Pandas hello. 

### <a name="python-aml"></a>Conectando tooAzure aprendizado de máquina
Você pode usar o hello seguir toosave o código exemplo hello dados convertidos tooa arquivo e carregá-lo tooan BLOBs do Azure. Olá dados blob Olá podem ser diretamente lidos em uma experiência de aprendizado de máquina do Azure usando Olá [importar dados] [ import-data] módulo. etapas de saudação são da seguinte maneira: 

1. Gravar saudação pandas dados quadro tooa arquivo local
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)
2. Carregar arquivo local tooAzure blob
   
        from azure.storage import BlobService
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
3. Ler dados de blob do Azure usando o aprendizado de máquina do Azure [importar dados] [ import-data] módulo, como mostrado na captura de tela de saudação abaixo:

![blob de leitor][2]

## <a name="hello-team-data-science-process-in-action-example"></a>Olá processo de ciência de dados de equipe no exemplo de ação
Para obter um exemplo passo a passo de ponta a ponta Olá processo de ciência de dados de equipe um usando um conjunto de dados público, consulte [processo de ciência de dados de equipe em ação: usando o SQL Server](machine-learning-data-science-process-sql-walkthrough.md).

[1]: ./media/machine-learning-data-science-sample-sql-server-virtual-machine/reader_database.png
[2]: ./media/machine-learning-data-science-sample-sql-server-virtual-machine/reader_blob.png

[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
