---
title: "dados de aaaExplore na máquina de Virtual do SQL Server no Azure | Microsoft Docs"
description: Como tooexplore dados armazenados em uma VM do SQL Server no Azure.
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: ccbb3085-af9e-4ec2-9df2-15dcab261d05
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: fcc449fc0d0e49be9b673cfb2de347cf44804017
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="explore-data-in-sql-server-virtual-machine-on-azure"></a>Explorar dados na Máquina Virtual do SQL Server no Azure
Este documento aborda como tooexplore dados armazenados em uma VM do SQL Server no Azure. Isso pode ser feito por disputa de dados usando SQL ou usando uma linguagem de programação como Python.

a seguir Olá **menu** links tootopics que descrevem como toouse ferramentas tooexplore dados de vários ambientes de armazenamento. Essa tarefa é uma etapa Olá processo de análise da Cortana (CAP).

[!INCLUDE [cap-explore-data-selector](../../includes/cap-explore-data-selector.md)]

> [!NOTE]
> instruções de SQL de exemplo Hello neste documento pressupõem que dados estejam no SQL Server. Se não for, consulte toohello nuvem dados ciência processo mapa toolearn como toomove seu servidor de tooSQL de dados.
> 
> 

## <a name="sql-dataexploration"></a>Explorar dados de SQL com scripts SQL
Aqui estão alguns scripts de SQL de exemplo que podem ser usado tooexplore repositórios de dados no SQL Server.

1. Obter a contagem de saudação de observações por dia
   
    `SELECT CONVERT(date, <date_columnname>) as date, count(*) as c from <tablename> group by CONVERT(date, <date_columnname>)` 
2. Obter os níveis de saudação em uma coluna categórica
   
    `select  distinct <column_name> from <databasename>`
3. Obter o número de saudação de níveis na combinação de duas colunas categóricas 
   
    `select <column_a>, <column_b>,count(*) from <tablename> group by <column_a>, <column_b>`
4. Obter distribuição Olá para colunas numéricas
   
    `select <column_name>, count(*) from <tablename> group by <column_name>`

> [!NOTE]
> Para obter um exemplo prático, você pode usar o hello [NYC táxi dataset](http://www.andresmh.com/nyctaxitrips/) e consulte toohello IPNB intitulada [NYC dados disputa usando o bloco de anotações do IPython e o SQL Server](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) para uma apresentação de ponta a ponta.
> 
> 

## <a name="python"></a>Explorar dados de SQL com o Python
Usando dados de tooexplore Python e gerar recursos quando Olá são de dados no SQL Server semelhante tooprocessing dados no blob do Azure usando o Python, conforme documentado no [dados de Blob do Azure de processo em seu ambiente de ciência de dados](machine-learning-data-science-process-data-blob.md). dados de saudação precisa toobe carregado do banco de dados de saudação para um pandas DataFrame e, em seguida, podem ser processados. Documentamos processo de saudação de conexão de banco de dados toohello e carregar dados saudação em Olá DataFrame nesta seção.

Olá, formato de cadeia de caracteres de conexão a seguir pode ser usado tooconnect tooa banco de dados SQL do Python usando pyodbc (substituir servername, dbname, nome de usuário e senha com valores específicos):

    #Set up hello SQL Azure connection
    import pyodbc    
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

Olá [biblioteca Pandas](http://pandas.pydata.org/) Python fornece um rico conjunto de ferramentas de análise de dados e estruturas de dados para a manipulação de dados para programação Python. Olá código a seguir lê Olá resultados de um banco de dados do SQL Server em um quadro de dados Pandas:

    # Query database and load hello returned results in pandas data frame
    data_frame = pd.read_sql('''select <columnname1>, <cloumnname2>... from <tablename>''', conn)

Agora você pode trabalhar com hello Pandas DataFrame conforme abordado no tópico Olá [dados de Blob do Azure de processo em seu ambiente de ciência de dados](machine-learning-data-science-process-data-blob.md).

## <a name="cortana-analytics-process-in-action-example"></a>Processo de Análise do Cortana no exemplo de ação
Para obter um exemplo passo a passo de ponta a ponta Olá processo de análise de Cortana usando um conjunto de dados público, consulte [Olá o processo de ciência de dados de equipe em ação: usando o SQL Server](machine-learning-data-science-process-sql-walkthrough.md).

