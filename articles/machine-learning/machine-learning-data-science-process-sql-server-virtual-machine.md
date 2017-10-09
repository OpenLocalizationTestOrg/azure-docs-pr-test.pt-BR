---
title: "aaaExplore dados em uma máquina de virtual do SQL Server no Azure | Microsoft Docs"
description: "Explorar dados e gerar recursos em uma máquina virtual do SQL Server no Azure"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: 
ms.assetid: 3949fb2c-ffab-49fb-908d-27d5e42f743b
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: fashah;garye;bradsev
ms.openlocfilehash: 67f4b058b0f6557ee15fd42795c918d68f1a9871
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="heading"></a>Processar dados na Máquina Virtual do SQL Server no Azure
Este documento aborda como tooexplore dados e gerar recursos para dados armazenados em uma VM do SQL Server no Azure. Isso pode ser feito por disputa de dados usando SQL ou usando uma linguagem de programação como Python.

> [!NOTE]
> instruções de SQL de exemplo Hello neste documento pressupõem que dados estejam no SQL Server. Se não for, consulte toohello nuvem dados ciência processo mapa toolearn como toomove seu servidor de tooSQL de dados.
> 
> 

## <a name="SQL"></a>Usando o SQL
Descrevemos Olá dados disputa as tarefas nesta seção usando SQL a seguir:

1. [Exploração de Dados](#sql-dataexploration)
2. [Geração de Recursos](#sql-featuregen)

### <a name="sql-dataexploration"></a>Exploração de Dados
Aqui estão alguns scripts de SQL de exemplo que podem ser usado tooexplore repositórios de dados no SQL Server.

> [!NOTE]
> Para obter um exemplo prático, você pode usar o hello [NYC táxi dataset](http://www.andresmh.com/nyctaxitrips/) e consulte toohello IPNB intitulada [NYC dados disputa usando o bloco de anotações do IPython e o SQL Server](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) para uma apresentação de ponta a ponta.
> 
> 

1. Obter a contagem de saudação de observações por dia
   
    `SELECT CONVERT(date, <date_columnname>) as date, count(*) as c from <tablename> group by CONVERT(date, <date_columnname>)` 
2. Obter os níveis de saudação em uma coluna categórica
   
    `select  distinct <column_name> from <databasename>`
3. Obter o número de saudação de níveis na combinação de duas colunas categóricas 
   
    `select <column_a>, <column_b>,count(*) from <tablename> group by <column_a>, <column_b>`
4. Obter distribuição Olá para colunas numéricas
   
    `select <column_name>, count(*) from <tablename> group by <column_name>`

### <a name="sql-featuregen"></a>Geração de recursos
Nesta seção, descrevemos as maneiras de gerar recursos usando SQL:  

1. [Geração de recursos baseada em contagem](#sql-countfeature)
2. [Agrupamento da Geração de Recursos](#sql-binningfeature)
3. [Implantar recursos de saudação de uma única coluna](#sql-featurerollout)

> [!NOTE]
> Depois de gerar recursos adicionais, você pode adicioná-los como tabela existente de toohello de colunas ou crie uma nova tabela com recursos adicionais de saudação e a chave primária, que pode ser unido a tabela original hello. 
> 
> 

### <a name="sql-countfeature"></a>Geração de recursos baseada em contagem
Olá exemplos a seguir demonstram duas maneiras de gerar recursos de contagem. Olá primeiro método usa soma condicional e usos de método segundo Olá Olá cláusula 'where'. Esses podem ser unidas com hello original (usando colunas de chave primária) toohave contagem recursos de tabela junto com os dados originais hello.

    select <column_name1>,<column_name2>,<column_name3>, COUNT(*) as Count_Features from <tablename> group by <column_name1>,<column_name2>,<column_name3> 

    select <column_name1>,<column_name2> , sum(1) as Count_Features from <tablename> 
    where <column_name3> = '<some_value>' group by <column_name1>,<column_name2> 

### <a name="sql-binningfeature"></a>Agrupamento da Geração de Recursos
Olá exemplo a seguir mostra como toogenerate guardado recursos guardando (usando cinco compartimentos) uma coluna numérica que pode ser usada como um recurso em vez disso:

    `SELECT <column_name>, NTILE(5) OVER (ORDER BY <column_name>) AS BinNumber from <tablename>`


### <a name="sql-featurerollout"></a>Implantar recursos de saudação de uma única coluna
Nesta seção, demonstraremos como tooroll-out de uma única coluna em uma tabela toogenerate adicionais de recursos. exemplo Hello supõe que haja uma coluna de latitude ou longitude na tabela de saudação do qual você está tentando toogenerate recursos.

Aqui está uma breve introdução em dados de localização de latitude/longitude (recursos de stackoverflow [como toomeasure Olá precisão de latitude e longitude?](http://gis.stackexchange.com/questions/8650/how-to-measure-the-accuracy-of-latitude-and-longitude)). Isso é útil toounderstand antes de campo de local de saudação featurizing:

* entrada de saudação informa se estamos Norte ou Sul, Leste ou oeste no mundo hello.
* Um dígito em centenas diferente de zero informa que estamos usando longitude, não latitude!
* Dígito Olá dezenas oferece uma posição tooabout 1.000 quilômetros. Ele nos dá informações úteis sobre em qual continente ou oceano estamos.
* Dígito de unidades de saudação (um grau decimal) fornece uma posição para cima too111 quilômetros (60 náuticas milhas, cerca de 69 milhas). Ele pode indicar aproximadamente em qual grande estado ou país estamos.
* Olá primeiro decimal lugar vale backup too11.1 km: ele pode distinguir posição de saudação de uma cidade grande de uma cidade grande vizinha.
* casa decimal da segunda Olá vale backup too1.1 km: ele pode separar um Vila dos Olá lado.
* Olá terceiro lugar de decimal é vale a pena too110 m, ele pode identificar um campo agrícola grande ou campus institucional.
* casa decimal da quarta Olá é vale a pena m too11: ele pode identificar um pacote de terra. É toohello comparável a precisão típica de uma unidade GPS não corrigida sem interferência.
* Olá quinto decimal é vale a pena o m too1.1: faz distinção árvores uns dos outros. Nível de toothis de precisão com unidades de GPS comerciais só pode ser obtida com a correção diferencial.
* Olá sexto decimal local é vale a pena m: too0.11 que você pode usar isso para dispor estruturas detalhadamente, para a criação de estruturas, criar estradas. Ela é mais do que suficiente para acompanhar os movimentos de geleiras e rios. Isso pode ser obtido coletando medidas arduamente com o GPS, tais como GPS com correção diferencial.

informações de local de saudação podem ser featurized da seguinte maneira separar região, local e informações de cidade. Observe que você também pode chamar um ponto de extremidade REST, como a API do Bing Maps disponível em [encontrar um local pelo ponto](https://msdn.microsoft.com/library/ff701710.aspx) tooget informações de região/Distrito de saudação.

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

Esses recursos com base no local podem ser ainda mais recursos de contagem adicionais toogenerate usado conforme descrito anteriormente. 

> [!TIP]
> Programaticamente, você pode inserir registros hello usando a linguagem de sua escolha. Talvez seja necessário tooinsert dados Olá eficiência de gravação de tooimprove partes (para obter um exemplo de como toodo esse usando pyodbc, consulte [tooaccess de exemplo de HelloWorld um SQL Server com python](https://code.google.com/p/pypyodbc/wiki/A_HelloWorld_sample_to_access_mssql_with_python)). Outra alternativa é tooinsert dados no banco de dados de saudação usando Olá [utilitário BCP](https://msdn.microsoft.com/library/ms162802.aspx).
> 
> 

### <a name="sql-aml"></a>Conectando tooAzure aprendizado de máquina
recurso Olá recentemente gerado pode ser adicionado como uma tabela existente de tooan de coluna ou armazenado em uma nova tabela e Unido Olá a tabela original para o aprendizado de máquina. Recursos podem ser gerados ou acessados se já criou, usando Olá [importar dados] [ import-data] módulo no aprendizado de máquina do Azure conforme mostrado abaixo:

![leitores de azureml][1] 

## <a name="python"></a>Usando uma linguagem de programação como Python
Usando dados de tooexplore Python e gerar recursos quando Olá são de dados no SQL Server é dados tooprocessing semelhantes no blob do Azure usando Python, conforme documentado no [dados de Blob do Azure de processo em seu ambiente de ciência de dados](machine-learning-data-science-process-data-blob.md). dados de saudação precisa toobe carregado do banco de dados de saudação para um quadro de dados pandas e, em seguida, podem ser processados. Documentamos processo Olá de conexão de banco de dados toohello e carregar dados de saudação no quadro de dados Olá nesta seção.

Olá, formato de cadeia de caracteres de conexão a seguir pode ser usado tooconnect tooa banco de dados SQL do Python usando pyodbc (substituir servername, dbname, nome de usuário e senha com valores específicos):

    #Set up hello SQL Azure connection
    import pyodbc    
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

Olá [biblioteca Pandas](http://pandas.pydata.org/) Python fornece um rico conjunto de ferramentas de análise de dados e estruturas de dados para a manipulação de dados para programação Python. código de saudação abaixo lê Olá resultados de um banco de dados do SQL Server em um quadro de dados Pandas:

    # Query database and load hello returned results in pandas data frame
    data_frame = pd.read_sql('''select <columnname1>, <cloumnname2>... from <tablename>''', conn)

Agora você pode trabalhar com o quadro de dados Pandas Olá conforme abordado no artigo Olá [dados de Blob do Azure de processo em seu ambiente de ciência de dados](machine-learning-data-science-process-data-blob.md).

## <a name="azure-data-science-in-action-example"></a>Exemplo da Ciência de Dados do Azure em Ação
Para obter um exemplo passo a passo de ponta a ponta do processo de ciência de dados do Azure usando um conjunto de dados público de saudação, consulte [processo de ciência de dados do Azure em ação](machine-learning-data-science-process-sql-walkthrough.md).

[1]: ./media/machine-learning-data-science-process-sql-server-virtual-machine/reader_db_featurizedinput.png


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/

