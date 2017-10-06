---
title: recursos de aaaCreate para os dados no SQL Server usando o SQL e Python | Microsoft Docs
description: Processar dados do SQL Azure
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: 
ms.assetid: bf1f4a6c-7711-4456-beb7-35fdccd46a44
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev;fashah;garye
ms.openlocfilehash: 223352edb0377a159333e7528ad03c43902e6f45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-features-for-data-in-sql-server-using-sql-and-python"></a>Criar recursos para dados no SQL Server usando o SQL e o Python
Este documento mostra como toogenerate recursos para dados armazenados em uma VM do SQL Server no Azure que ajudam a algoritmos de aprenderem com mais eficiência de dados saudação. Isso pode ser feito usando o SQL ou usando uma linguagem de programação como o Python, ambos demonstrados aqui.

[!INCLUDE [cap-create-features-data-selector](../../includes/cap-create-features-selector.md)]

Isso **menu** links tootopics que descrevem como toocreate recursos para os dados em vários ambientes. Essa tarefa é uma etapa Olá [processo de ciência de dados da equipe (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).

> [!NOTE]
> Para obter um exemplo prático, você pode consultar Olá [NYC táxi dataset](http://www.andresmh.com/nyctaxitrips/) e consulte toohello IPNB intitulada [NYC dados disputa usando o bloco de anotações do IPython e o SQL Server](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) para uma apresentação de ponta a ponta.
> 
> 

## <a name="prerequisites"></a>Pré-requisitos
Este artigo supõe que você:

* Criou uma conta de armazenamento do Azure. Se precisar de instruções, confira [Criar uma conta de Armazenamento do Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account)
* Armazenou seus dados no SQL Server. Se você não tiver, consulte [mover dados tooan banco de dados do SQL Azure para o aprendizado de máquina do Azure](machine-learning-data-science-move-sql-azure.md) para obter instruções sobre como toomove Olá dados.

## <a name="sql-featuregen"></a>Geração de recursos com o SQL
Nesta seção, descrevemos as maneiras de gerar recursos usando SQL:  

1. [Geração de recursos baseada em contagem](#sql-countfeature)
2. [Agrupamento da Geração de Recursos](#sql-binningfeature)
3. [Implantar recursos de saudação de uma única coluna](#sql-featurerollout)

> [!NOTE]
> Depois de gerar recursos adicionais, você pode adicioná-los como tabela existente de toohello de colunas ou crie uma nova tabela com recursos adicionais de saudação e a chave primária, que pode ser unido a tabela original hello.
> 
> 

### <a name="sql-countfeature"></a>Geração de recursos baseada em contagem
Este documento demonstra duas maneiras de gerar recursos de contagem. Olá primeiro método usa soma condicional e usos de método segundo Olá Olá cláusula 'where'. Esses podem ser unidas com hello original (usando colunas de chave primária) toohave contagem recursos de tabela junto com os dados originais hello.

    select <column_name1>,<column_name2>,<column_name3>, COUNT(*) as Count_Features from <tablename> group by <column_name1>,<column_name2>,<column_name3>

    select <column_name1>,<column_name2> , sum(1) as Count_Features from <tablename>
    where <column_name3> = '<some_value>' group by <column_name1>,<column_name2>

### <a name="sql-binningfeature"></a>Agrupamento da Geração de Recursos
Olá exemplo a seguir mostra como toogenerate guardado recursos guardando (usando 5 compartimentos) uma coluna numérica que pode ser usada como um recurso em vez disso:

    `SELECT <column_name>, NTILE(5) OVER (ORDER BY <column_name>) AS BinNumber from <tablename>`


### <a name="sql-featurerollout"></a>Implantar recursos de saudação de uma única coluna
Nesta seção, demonstraremos como tooroll em uma única coluna em uma tabela toogenerate adicionais de recursos. exemplo Hello supõe que haja uma coluna de latitude ou longitude na tabela de saudação do qual você está tentando toogenerate recursos.

Aqui está uma breve cartilha sobre os dados de localização de latitude/longitude (recursos de stackoverflow `http://gis.stackexchange.com/questions/8650/how-to-measure-the-accuracy-of-latitude-and-longitude`). Isso é útil toounderstand antes de campo de local de saudação featurizing:

* entrada de saudação informa se estamos Norte ou Sul, Leste ou oeste no mundo hello.
* Um dígito em centenas diferente de zero informa que estamos usando longitude, não latitude!
* Dígito Olá dezenas oferece uma posição tooabout 1.000 quilômetros. Ele nos dá informações úteis sobre em qual continente ou oceano estamos.
* Dígito de unidades de saudação (um grau decimal) fornece uma posição para cima too111 quilômetros (60 náuticas milhas, cerca de 69 milhas). Ele pode indicar aproximadamente em qual grande estado ou país estamos.
* Olá primeiro decimal lugar vale backup too11.1 km: ele pode distinguir posição de saudação de uma cidade grande de uma cidade grande vizinha.
* casa decimal da segunda Olá vale backup too1.1 km: ele pode separar um Vila dos Olá lado.
* Olá terceiro lugar de decimal é vale a pena too110 m, ele pode identificar um campo agrícola grande ou campus institucional.
* casa decimal da quarta Olá é vale a pena m too11: ele pode identificar um pacote de terra. É toohello comparável a precisão típica de uma unidade GPS não corrigida sem interferência.
* Olá quinto lugar de decimal é vale a pena o m too1.1: distinguir árvores uns dos outros. Nível de toothis de precisão com unidades de GPS comerciais só pode ser obtida com a correção diferencial.
* Olá sexto decimal local é vale a pena m: too0.11 que você pode usar isso para dispor estruturas detalhadamente, para a criação de estruturas, criar estradas. Ela é mais do que suficiente para acompanhar os movimentos de geleiras e rios. Isso pode ser obtido coletando medidas arduamente com o GPS, tais como GPS com correção diferencial.

informações de localização de saudação podem pode ser featurized da seguinte maneira separar região, local e informações de cidade. Observe que uma vez também pode chamar um ponto de extremidade REST, como a API do Bing Maps disponíveis em `https://msdn.microsoft.com/library/ff701710.aspx` informações de região/Distrito Olá tooget.

    select
        <location_columnname>
        ,round(<location_columnname>,0) as l1        
        ,l2=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 1 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),1,1) else '0' end     
        ,l3=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 2 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),2,1) else '0' end     
        ,l4=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 3 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),3,1) else '0' end     
        ,l5=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 4 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),4,1) else '0' end     
        ,l6=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 5 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),5,1) else '0' end     
        ,l7=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 6 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),6,1) else '0' end     
    from <tablename>

Olá acima local baseada em recursos podem ser mais usado toogenerate recursos de contagem adicionais conforme descrito anteriormente.

> [!TIP]
> Programaticamente, você pode inserir registros hello usando a linguagem de sua escolha. Talvez seja necessário tooinsert dados Olá eficiência de gravação partes tooimprove [Check-out exemplo hello como toodo esse usando pyodbc aqui](https://code.google.com/p/pypyodbc/wiki/A_HelloWorld_sample_to_access_mssql_with_python).
> Outra alternativa é tooinsert dados Olá banco de dados usando [utilitário BCP](https://msdn.microsoft.com/library/ms162802.aspx)
> 
> 

### <a name="sql-aml"></a>Conectando tooAzure aprendizado de máquina
recurso Olá recentemente gerado pode ser adicionado como uma tabela existente de tooan de coluna ou armazenado em uma nova tabela e Unido Olá a tabela original para o aprendizado de máquina. Recursos podem ser gerados ou acessados se já criou, usando Olá [importar dados](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) módulo no Azure ML, conforme mostrado abaixo:

![leitores de azureml](./media/machine-learning-data-science-process-sql-server-virtual-machine/reader_db_featurizedinput.png)

## <a name="python"></a>Usando uma linguagem de programação como Python
Usando recursos do Python toogenerate quando dados saudação no SQL Server é dados tooprocessing semelhantes no blob do Azure usando Python, conforme documentado no [dados Blob do Azure de processo em ambiente ciência de dados](machine-learning-data-science-process-data-blob.md). dados de saudação precisa toobe carregado do banco de dados de saudação para um quadro de dados pandas e, em seguida, podem ser processados. Documentamos processo Olá de conexão de banco de dados toohello e carregar dados de saudação no quadro de dados Olá nesta seção.

Olá, formato de cadeia de caracteres de conexão a seguir pode ser usado tooconnect tooa banco de dados SQL do Python usando pyodbc (substituir servername, dbname, nome de usuário e senha com valores específicos):

    #Set up hello SQL Azure connection
    import pyodbc
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

Olá [biblioteca Pandas](http://pandas.pydata.org/) Python fornece um rico conjunto de ferramentas de análise de dados e estruturas de dados para a manipulação de dados para programação Python. código de saudação abaixo lê Olá resultados de um banco de dados do SQL Server em um quadro de dados Pandas:

    # Query database and load hello returned results in pandas data frame
    data_frame = pd.read_sql('''select <columnname1>, <cloumnname2>... from <tablename>''', conn)

Agora você pode trabalhar com o quadro de dados Pandas hello como abordadas em tópicos [criar recursos para dados de armazenamento de BLOBs do Azure usando Panda](machine-learning-data-science-create-features-blob.md).

