---
title: "Olá processo de ciência de dados de equipe na ação - usando um Cluster de Hadoop de HDInsight do Azure em um conjunto de dados de 1 TB | Microsoft Docs"
description: "Usando Olá, equipe de processo de ciência de dados para um cenário de ponta a ponta empregando uma HDInsight Hadoop toobuild de cluster e implantar um modelo usando (1 TB) disponível publicamente conjuntos de dados grandes"
services: machine-learning,hdinsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 72d958c4-3205-49b9-ad82-47998d400d2b
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: 59b2af02e7840cb60a4b5b2f2c8ab0611df198ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="hello-team-data-science-process-in-action---using-an-azure-hdinsight-hadoop-cluster-on-a-1-tb-dataset"></a>Olá processo de ciência de dados de equipe na ação - usando um Cluster de Hadoop de HDInsight do Azure em um conjunto de dados de 1 TB

Neste passo a passo, estamos demonstram o uso Olá o processo de ciência de dados de equipe em um cenário de ponta a ponta com um [cluster Azure HDInsight Hadoop](https://azure.microsoft.com/services/hdinsight/) toostore, explorar, engenheiro de recursos e para baixo de dados de exemplo de uma saudação publicamente disponível [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) conjuntos de dados. Usamos o aprendizado de máquina do Azure toobuild um modelo de classificação binária nesses dados. Também mostramos como toopublish um desses modelos como um serviço Web.

Também é possível toouse um tarefas de saudação do IPython notebook tooaccomplish apresentadas neste passo a passo. Os usuários que seriam como tootry essa abordagem deve consultar Olá [Criteo passo a passo usando uma conexão ODBC Hive](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-hive-walkthrough-criteo.ipynb) tópico.

## <a name="dataset"></a>Descrição do conjunto de dados da Criteo
Olá Criteo dados são um conjunto de dados de previsão de clique que é de aproximadamente 370GB dos arquivos TSV de gzip compactado (~1.3TB descompactados), que inclui mais de 4.3 bilhões de registros. Ele é obtido a partir de 24 dias de cliques de dados disponibilizados pela [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/). Para conveniência de saudação do cientistas de dados, nós forem descompactados tooexperiment disponível toous de dados com.

Cada registro deste conjunto de dados contém 40 colunas:

* Olá primeira coluna é uma coluna de rótulo que indica se um usuário clica em um **adicionar** (valor 1) ou não clique em um (valor 0)
* as 13 colunas seguintes são numéricas e
* as últimas 26 colunas são colunas categóricas

colunas de saudação são anônimas e usar uma série de nomes enumeradas: "Col1" (para a coluna de rótulo Olá) muito ' Col40 "(para última coluna de categóricos Olá).            

Aqui está um trecho da saudação primeiro 20 colunas de duas observações (linhas) desse conjunto de dados:

    Col1    Col2    Col3    Col4    Col5    Col6    Col7    Col8    Col9    Col10    Col11    Col12    Col13    Col14    Col15            Col16            Col17            Col18            Col19        Col20

    0       40      42      2       54      3       0       0       2       16      0       1       4448    4       1acfe1ee        1b2ff61f        2e8b2631        6faef306        c6fc10d3    6fcd6dcb           
    0               24              27      5               0       2       1               3       10064           9a8cb066        7a06385f        417e6103        2170fc56        acf676aa    6fcd6dcb                      

Há valores ausentes em ambas as colunas numéricas e categóricos do hello este conjunto de dados. Descrevemos um método simples para lidar com valores ausentes hello. Detalhes adicionais de dados saudação são explorados quando armazenamos em tabelas de Hive.

**Definição:** *taxa de Clickthrough (CTR):* é Olá porcentagem de cliques em dados saudação. Este conjunto de dados Criteo, Olá CTR é cerca de % 3.3 ou 0.033.

## <a name="mltasks"></a>Exemplos de tarefas de previsão
Dois exemplos de problemas de previsão são abordados neste passo a passo:

1. **Classificação binária**: prevê se um usuário clicou em um anúncio:
   
   * Classe 0: não clicou
   * Classe 1: clicou
2. **Regressão**: prevê a probabilidade de saudação do, clique em um anúncio de recursos do usuário.

## <a name="setup"></a>Configurar um cluster Hadoop do HDInsight para ciência de dados
**Observação:** normalmente, esta é uma tarefa para o **Administrador**.

Configure seu ambiente de Ciência de dados do Azure para a criação de soluções analíticas de previsão com clusters do HDInsight em três etapas:

1. [Criar uma conta de armazenamento](../storage/common/storage-create-storage-account.md): esta conta de armazenamento é usada toostore dados no armazenamento de BLOBs do Azure. dados de saudação usados em clusters de HDInsight são armazenados aqui.
2. [Personalizar clusters Hadoop do Azure HDInsight para ciência de dados](machine-learning-data-science-customize-hadoop-cluster.md): esta etapa cria um cluster Hadoop do Azure HDInsight com o Anaconda Python 2.7 de 64 bits instalado em todos os nós. Há dois toocomplete de etapas importantes (descritas neste tópico) ao personalizar o cluster do HDInsight hello.
   
   * Você deve vincular a conta de armazenamento Olá criada na etapa 1 com o cluster HDInsight quando ele é criado. Esta conta de armazenamento é usada para acessar os dados que podem ser processados em cluster hello.
   * Você deve habilitar o nó principal do toohello de acesso remoto de cluster Olá depois que ele é criado. Lembre-se de credenciais de acesso remoto Olá você especificar aqui (diferentes das especificadas para cluster Olá em sua criação): é necessário toocomplete Olá seguintes procedimentos.
3. [Criar um espaço de trabalho do Azure ML](machine-learning-create-workspace.md): aprendizado de máquina do Azure este espaço de trabalho é usado para criar modelos de aprendizado de máquina após uma exploração de dados inicial e para baixo de amostragem no cluster do HDInsight hello.

## <a name="getdata"></a>Obter e consumir dados de uma fonte de pública
Olá [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) conjunto de dados pode ser acessado clicando no link hello, aceitando os termos de uso do hello e fornecer um nome. Um instantâneo desse processo é mostrado aqui:

![Aceitar os termos da Criteo](./media/machine-learning-data-science-process-hive-criteo-walkthrough/hLxfI2E.png)

Clique em **tooDownload continuar** tooread mais sobre o conjunto de dados hello e sua disponibilidade.

dados de saudação residem em um público [armazenamento de BLOBs do Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md) local: wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/. Olá "wasb" refere-se o local de armazenamento de Blob tooAzure. 

1. dados de saudação nesse armazenamento de blob público consistem em três subpastas dos dados descompactados.
   
   1. Olá subpasta *bruto/count/* contém Olá primeiro 21 dias de dados - dia\_tooday 00\_20
   2. Olá subpasta *bruto/treinar/* consiste em um único dia de dados, dia\_21
   3. Olá subpasta *bruto/teste/* consiste em dois dias de dados, dia\_22 e dia\_23
2. Para aqueles que desejam toostart com dados brutos gzip de saudação, eles também estão disponíveis na pasta principal Olá *bruto /* como day_NN.gz, onde NN vai de too23 00.

Tooaccess uma abordagem alternativa, explore e modele esses dados que não requerem que todos os downloads de locais é explicado mais adiante neste passo a passo durante a criação de tabelas de Hive.

## <a name="login"></a>Faça logon no nó principal do cluster toohello
toolog em toohello um nó principal do cluster hello, use Olá [portal do Azure](https://ms.portal.azure.com) toolocate cluster de saudação. Clique elefante ícone HDInsight Olá Olá à esquerda e, em seguida, clique duas vezes no nome de saudação do cluster. Navegue toohello **configuração** guia, clique duas vezes Olá conectar na parte inferior da saudação da página hello e insira suas credenciais de acesso remoto quando solicitado. Isso leva você toohello um nó principal do cluster hello.

Um típico primeiro log no nó principal do cluster toohello é semelhante ao seguinte:

![Faça logon no toocluster](./media/machine-learning-data-science-process-hive-criteo-walkthrough/Yys9Vvm.png)

Olá esquerda, vemos hello "Hadoop linha de comando", que é nossa força de trabalho Olá exploração de dados. Nós também vemos duas URLs úteis - "Status do Hadoop Yarn" e "Nó de Nome do Hadoop". Olá yarn status URL mostra o andamento do trabalho e URL do nó nome hello fornece detalhes sobre configuração de cluster de saudação.

Agora são configurados e pronto toobegin primeira parte da saudação passo a passo: usando Hive e preparar dados para o aprendizado de máquina do Azure a exploração de dados.

## <a name="hive-db-tables"></a> Criar tabelas e banco de dados do Hive
toocreate Hive tabelas para nosso conjunto de dados Criteo, abra Olá ***linha de comando do Hadoop*** na Olá a área de trabalho do nó principal hello e insira o diretório de Hive Olá digitando o comando Olá

    cd %hive_home%\bin

> [!NOTE]
> Executar todos os comandos de Hive neste passo a passo do compartimento de Hive Olá / prompt do diretório. Isso soluciona automaticamente possíveis problemas de caminho. Usamos termos Olá "Hive diretório" prompt, "Hive bin / aviso diretório" e "linha de comando do Hadoop" alternadamente.
> 
> [!NOTE]
> tooexecute qualquer consulta de Hive, você sempre pode usar Olá comandos a seguir:
> 
> 

        cd %hive_home%\bin
        hive

Após Olá Hive REPL aparece com um "hive >" entrar, basta recortar e colar Olá consulta tooexecute-lo.

Olá código a seguir cria um banco de dados "criteo" e, em seguida, gera 4 tabelas:

* um *tabela para gerar contagens* criado no dia dias\_tooday 00\_20,
* um *tabela para uso como Olá conjunto de dados de treinamento* criado no dia\_21, e
* dois *conjuntos de dados de teste de tabelas para uso como Olá* criado no dia\_22 e dia\_23 respectivamente.

Dividiremos nosso conjunto de dados de teste em duas tabelas diferentes, porque um dos dias Olá é um feriado e queremos toodetermine se modelo Olá pode detectar diferenças entre um feriado e não feriado da taxa de clickthrough hello.

Olá script [exemplo #95; hive & #95; criar & #95; criteo & #95; banco de dados & #95; e & #95;tables.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_criteo_database_and_tables.hql) será exibido aqui para sua conveniência:

    CREATE DATABASE IF NOT EXISTS criteo;
    DROP TABLE IF EXISTS criteo.criteo_count;
    CREATE TABLE criteo.criteo_count (
    col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE LOCATION 'wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/count';

    DROP TABLE IF EXISTS criteo.criteo_train;
    CREATE TABLE criteo.criteo_train (
    col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE LOCATION 'wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/train';

    DROP TABLE IF EXISTS criteo.criteo_test_day_22;
    CREATE TABLE criteo.criteo_test_day_22 (
    col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE LOCATION 'wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/test/day_22';

    DROP TABLE IF EXISTS criteo.criteo_test_day_23;
    CREATE TABLE criteo.criteo_test_day_23 (
    col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE LOCATION 'wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/test/day_23';

Observe que todas essas tabelas são externas como podemos simplesmente locais de armazenamento de Blob (wasb) tooAzure de ponto.

**Há duas maneiras tooexecute Hive qualquer consulta que mencionamos agora.**

1. **Usando Olá Hive REPL de linha de comando**: Olá primeiro é tooissue um comando "hive" e copie e cole uma consulta em Olá Hive REPL de linha de comando. toodo isso, execute:
   
        cd %hive_home%\bin
        hive
   
     Agora no hello REPL de linha de comando, recortando e colando consulta Olá executa-o.
2. **Salvar consultas tooa arquivo e executar o comando Olá**: Olá segundo é o arquivo de .hql do toosave Olá consultas tooa ([exemplo #95; hive & #95; criar & #95; criteo & #95; banco de dados & #95; e & #95;tables.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_criteo_database_and_tables.hql)) e, em seguida, que o comando de problema a seguir de saudação tooexecute consulta de saudação:
   
        hive -f C:\temp\sample_hive_create_criteo_database_and_tables.hql

### <a name="confirm-database-and-table-creation"></a>Confirme a criação do banco de dados e da tabela
Em seguida, podemos confirmar a criação de Olá do banco de dados de saudação com hello comando a seguir do compartimento de Hive Olá / aviso diretório:

        hive -e "show databases;"

Isso fornece:

        criteo
        default
        Time taken: 1.25 seconds, Fetched: 2 row(s)

Isso confirma a criação de saudação do banco de dados de novo hello, "criteo".

toosee quais tabelas criadas, podemos simplesmente execute Olá comando aqui do compartimento de Hive Olá / aviso diretório:

        hive -e "show tables in criteo;"

Em seguida, vemos Olá saída a seguir:

        criteo_count
        criteo_test_day_22
        criteo_test_day_23
        criteo_train
        Time taken: 1.437 seconds, Fetched: 4 row(s)

## <a name="exploration"></a> Exploração de dados no Hive
Agora estamos prontos toodo alguma exploração de dados básica no Hive. Vamos começar contando Olá número de exemplos no treinamento de saudação e tabelas de dados de teste.

### <a name="number-of-train-examples"></a>Número de exemplos de treinamento
Olá conteúdo de [exemplo & #95; hive & #95; contagem & #95; treinar #95; tabela & #95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_train_table_examples.hql) são mostradas aqui:

        SELECT COUNT(*) FROM criteo.criteo_train;

Isso resulta em:

        192215183
        Time taken: 264.154 seconds, Fetched: 1 row(s)

Como alternativa, um também pode emitir Olá comando a seguir do compartimento de Hive Olá / aviso diretório:

        hive -f C:\temp\sample_hive_count_criteo_train_table_examples.hql

### <a name="number-of-test-examples-in-hello-two-test-datasets"></a>Número de exemplos de teste Olá dois conjuntos de dados de teste
Podemos contar o número de Olá exemplos Olá dois conjuntos de dados de teste agora. Olá conteúdo de [exemplo & #95 hive & #95; contagem & #95; criteo & #95; teste & #95; dia & #95; 22 & #95; tabela de & #95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_criteo_test_day_22_table_examples.hql) aqui:

        SELECT COUNT(*) FROM criteo.criteo_test_day_22;

Isso resulta em:

        189747893
        Time taken: 267.968 seconds, Fetched: 1 row(s)

Como de costume, podemos também pode chamar script hello do compartimento de Hive Olá / diretório prompt emitindo o comando hello:

        hive -f C:\temp\sample_hive_count_criteo_test_day_22_table_examples.hql

Por fim, podemos examinar número Olá dos exemplos de teste no conjunto de dados de teste de saudação com base no dia\_23.

Olá comando toodo isso é semelhante toohello mostrada apenas (consulte muito[exemplo & #95; hive #95; contagem & #95; criteo & #95; teste & #95; dia & #95; 23 & #95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_criteo_test_day_23_examples.hql)):

        SELECT COUNT(*) FROM criteo.criteo_test_day_23;

Isso fornece:

        178274637
        Time taken: 253.089 seconds, Fetched: 1 row(s)

### <a name="label-distribution-in-hello-train-dataset"></a>Distribuição de rótulo no conjunto de dados de treinamento Olá
distribuição de rótulo Olá no conjunto de dados de treinamento de saudação é de interesse. toosee isso, vamos mostrar conteúdo do [exemplo & #95; hive & #95; criteo & #95; rótulo #95; distribuição & #95; treinar & #95;table.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_label_distribution_train_table.hql):

        SELECT Col1, COUNT(*) AS CT FROM criteo.criteo_train GROUP BY Col1;

Isso resulta em distribuição de rótulo hello:

        1       6292903
        0       185922280
        Time taken: 459.435 seconds, Fetched: 2 row(s)

Observe que a porcentagem de saudação de rótulos positivos é 3.3% (consistente com o conjunto de dados original Olá).

### <a name="histogram-distributions-of-some-numeric-variables-in-hello-train-dataset"></a>Distribuições de histograma de algumas variáveis numéricas em Olá treinar o conjunto de dados
Podemos usar nativo do Hive "histograma\_numérico" função toofind out que distribuição Olá de variáveis numéricas Olá aparência. Aqui estão os conteúdos de saudação do [exemplo & #95; hive #95; criteo & #95; histograma & #95;numeric.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_histogram_numeric.hql):

        SELECT CAST(hist.x as int) as bin_center, CAST(hist.y as bigint) as bin_height FROM
            (SELECT
            histogram_numeric(col2, 20) as col2_hist
            FROM
            criteo.criteo_train
            ) a
            LATERAL VIEW explode(col2_hist) exploded_table as hist;

Isso gera o seguinte hello:

        26      155878415
        2606    92753
        6755    22086
        11202   6922
        14432   4163
        17815   2488
        21072   1901
        24113   1283
        27429   1225
        30818   906
        34512   723
        38026   387
        41007   290
        43417   312
        45797   571
        49819   428
        53505   328
        56853   527
        61004   160
        65510   3446
        Time taken: 317.851 seconds, Fetched: 20 row(s)

Olá LATERAL exibição - explodir combinação na seção serve tooproduce uma saída semelhante a SQL em vez de lista de saudação normal. Observe que no hello essa tabela, a primeira coluna de saudação corresponde toohello bin center e hello segundo toohello bin frequência.

### <a name="approximate-percentiles-of-some-numeric-variables-in-hello-train-dataset"></a>Percentuais aproximados de algumas variáveis numéricas em Olá treinar o conjunto de dados
Também interesse com variáveis numéricas é computar Olá percentuais aproximados. O "percentile\_approx" nativo do Hive faz isso para nós. Olá conteúdo de [exemplo & #95; hive #95; criteo & #95; aproximado & #95;percentiles.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_approximate_percentiles.hql) são:

        SELECT MIN(Col2) AS Col2_min, PERCENTILE_APPROX(Col2, 0.1) AS Col2_01, PERCENTILE_APPROX(Col2, 0.3) AS Col2_03, PERCENTILE_APPROX(Col2, 0.5) AS Col2_median, PERCENTILE_APPROX(Col2, 0.8) AS Col2_08, MAX(Col2) AS Col2_max FROM criteo.criteo_train;

Isso resulta em:

        1.0     2.1418600917169246      2.1418600917169246    6.21887086390288 27.53454893115633       65535.0
        Time taken: 564.953 seconds, Fetched: 1 row(s)

Podemos remarque distribuição Olá percentuais é toohello relacionadas histograma distribuição de qualquer variável numérica normalmente.         

### <a name="find-number-of-unique-values-for-some-categorical-columns-in-hello-train-dataset"></a>Localize o número de valores exclusivos para algumas colunas categóricas no conjunto de dados de treinamento Olá
Continuar a exploração de dados Olá, encontramos agora, para algumas colunas categóricas, número de saudação de valores exclusivos que eles executam. toodo isso, vamos mostrar conteúdo do [exemplo & #95; hive #95; criteo & #95; exclusivo & #95; valores & #95;categoricals.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_unique_values_categoricals.hql):

        SELECT COUNT(DISTINCT(Col15)) AS num_uniques FROM criteo.criteo_train;

Isso resulta em:

        19011825
        Time taken: 448.116 seconds, Fetched: 1 row(s)

Observe que Col15 tem valores exclusivos em 19M! Essas variáveis categóricas altamente dimensional usando técnicas simples como "hot uma codificação" tooencode for inviável. Em particular, nós explicamos e demonstramos uma técnica poderosa e robusta chamada [Aprendizado com contagens](http://blogs.technet.com/b/machinelearning/archive/2015/02/17/big-learning-made-easy-with-counts.aspx) para lidar com esse problema de modo eficaz.

Podemos terminar esta subseção examinando Olá número de valores exclusivos de algumas outras colunas categóricas também. Olá conteúdo de [exemplo & #95; hive #95; criteo & #95; exclusivo & #95; valores & #95; vários & #95;categoricals.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_unique_values_multiple_categoricals.hql) são:

        SELECT COUNT(DISTINCT(Col16)), COUNT(DISTINCT(Col17)),
        COUNT(DISTINCT(Col18), COUNT(DISTINCT(Col19), COUNT(DISTINCT(Col20))
        FROM criteo.criteo_train;

Isso resulta em:

        30935   15200   7349    20067   3
        Time taken: 1933.883 seconds, Fetched: 1 row(s)

Novamente, vemos que, exceto Col20, todos os Olá outras colunas têm muitos valores exclusivos.

### <a name="co-occurrence-counts-of-pairs-of-categorical-variables-in-hello-train-dataset"></a>Contagens de ocorrência do conjunto de pares de variáveis categóricas no conjunto de dados de treinamento Olá

contagens de ocorrência colegas Olá de pares de variáveis categóricas também é de interesse. Isso pode ser determinado usando o código Olá [exemplo & #95; hive #95; criteo & #95; emparelhados & #95; categóricos & #95;counts.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_paired_categorical_counts.hql):

        SELECT Col15, Col16, COUNT(*) AS paired_count FROM criteo.criteo_train GROUP BY Col15, Col16 ORDER BY paired_count DESC LIMIT 15;

Nós inverter a ordem Olá contagens por sua ocorrência e procure na parte superior do hello 15 nesse caso. Isso nos fornece:

        ad98e872        cea68cd3        8964458
        ad98e872        3dbb483e        8444762
        ad98e872        43ced263        3082503
        ad98e872        420acc05        2694489
        ad98e872        ac4c5591        2559535
        ad98e872        fb1e95da        2227216
        ad98e872        8af1edc8        1794955
        ad98e872        e56937ee        1643550
        ad98e872        d1fade1c        1348719
        ad98e872        977b4431        1115528
        e5f3fd8d        a15d1051        959252
        ad98e872        dd86c04a        872975
        349b3fec        a52ef97d        821062
        e5f3fd8d        a0aaffa6        792250
        265366bf        6f5c7c41        782142
        Time taken: 560.22 seconds, Fetched: 15 row(s)

## <a name="downsample"></a>Para conjuntos de dados do exemplo hello para aprendizado de máquina do Azure
Ter explorado Olá conjuntos de dados e demonstrar como podemos pode fazer esse tipo de exploração para quaisquer variáveis (incluindo combinações), que agora para baixo de conjuntos de dados do exemplo hello para que podemos criar modelos no aprendizado de máquina do Azure. Lembre-se nos concentraremos no problema Olá é: dado um conjunto de atributos de exemplo (valores de recurso de Col2 - Col40), podemos prever se Col1 é 0 (nenhum clique) ou 1 (clique).

toodown exemplo nosso treinar e testar conjuntos de dados too1% do tamanho original hello, usamos a função RAND () da nativa do Hive. Olá próximo script, [exemplo & #95; hive #95; criteo & #95; diminuir a resolução & #95; treinar & #95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_train_dataset.hql) faz isso para o conjunto de dados de treinamento hello:

        CREATE TABLE criteo.criteo_train_downsample_1perc (
        col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
        LINES TERMINATED BY '\n'
        STORED AS TEXTFILE;

        ---Now downsample and store in this table

        INSERT OVERWRITE TABLE criteo.criteo_train_downsample_1perc SELECT * FROM criteo.criteo_train WHERE RAND() <= 0.01;

Isso resulta em:

        Time taken: 12.22 seconds
        Time taken: 298.98 seconds

Olá script [exemplo & #95; hive #95; criteo & #95; diminuir a resolução & #95; teste & #95; dia & #95; 22 & #95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_test_day_22_dataset.hql) faz isso para dados de teste, dia\_22:

        --- Now for test data (day_22)

        CREATE TABLE criteo.criteo_test_day_22_downsample_1perc (
        col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
        LINES TERMINATED BY '\n'
        STORED AS TEXTFILE;

        INSERT OVERWRITE TABLE criteo.criteo_test_day_22_downsample_1perc SELECT * FROM criteo.criteo_test_day_22 WHERE RAND() <= 0.01;

Isso resulta em:

        Time taken: 1.22 seconds
        Time taken: 317.66 seconds


Por fim, Olá script [exemplo & #95; hive #95; criteo & #95; diminuir a resolução & #95; teste & #95; dia & #95; 23 & #95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_test_day_23_dataset.hql) faz isso para dados de teste, dia\_23:

        --- Finally test data day_23
        CREATE TABLE criteo.criteo_test_day_23_downsample_1perc (
        col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 srical feature; tring)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
        LINES TERMINATED BY '\n'
        STORED AS TEXTFILE;

        INSERT OVERWRITE TABLE criteo.criteo_test_day_23_downsample_1perc SELECT * FROM criteo.criteo_test_day_23 WHERE RAND() <= 0.01;

Isso resulta em:

        Time taken: 1.86 seconds
        Time taken: 300.02 seconds

Com isso, estamos toouse pronto nosso baixo amostra treinar e testar os conjuntos de dados para a criação de modelos no aprendizado de máquina do Azure.

Há um componente importante final antes de continuarmos tooAzure aprendizado de máquina, que é a tabela de contagem de saudação preocupações. Olá próxima subseção, discutiremos isso em detalhes.

## <a name="count"></a>Uma breve discussão sobre a tabela de contagem de saudação
Como vimos, diversas variáveis categóricas têm uma dimensionalidade muito alta. Em nosso passo a passo, vamos apresentar uma técnica poderosa chamada [aprendizado com contagens](http://blogs.technet.com/b/machinelearning/archive/2015/02/17/big-learning-made-easy-with-counts.aspx) tooencode essas variáveis de maneira eficiente e robusta. Para obter mais informações sobre essa técnica são Olá link fornecido.

[!NOTE]
>Este passo a passo, vamos nos concentrar em usando tooproduce de tabelas de contagem compact representações de recursos categóricos altamente dimensional. Isso não é Olá somente modo tooencode recursos categóricos; Para obter mais informações sobre outras técnicas, os usuários interessados podem check-out [um hot-codificação](http://en.wikipedia.org/wiki/One-hot) e [hash de recurso](http://en.wikipedia.org/wiki/Feature_hashing).
>

tabelas de contagem de toobuild nos dados de contagem de Olá, usamos Olá dados na pasta bruto de saudação/contagem. Em Olá modelagem seção, vamos mostrar aos usuários como toobuild elas contam tabelas para recursos categóricos do zero ou, Alternativamente, toouse uma tabela de contagem predefinidos para seus explorações. O que segue, quando fazemos referência muito "pré-criados tabelas de contagem", queremos dizer usando tabelas de contagem de saudação que fornecemos. Instruções detalhadas sobre como tooaccess essas tabelas são fornecidas na próxima seção, Olá.

## 
            <a name="aml">
            </a> Criar um modelo com o Azure Machine Learning
Nosso processo de criação de modelo no Azure Machine Learning seguirá estas etapas:

1. [Obter dados de saudação de tabelas de Hive para aprendizado de máquina do Azure](#step1)
2. [Criar experiência Olá: limpar dados saudação e featurize com tabelas de contagem](#step2)
3. [Compilação, treinar e modelo de pontuação Olá](#step3)
4. [Avaliar modelo Olá](#step4)
5. [Publicar o modelo de saudação como um serviço web](#step5)

Agora estamos prontos toobuild modelos no estúdio de aprendizado de máquina do Azure. Os dados de amostrados para baixo é salvo como tabelas de Hive no cluster hello. Usamos hello Azure Machine Learning **importar dados** tooread módulo esses dados. conta de armazenamento de Olá Olá credenciais tooaccess desse cluster são fornecidas a seguir.

### <a name="step1"></a>Etapa 1: Obter dados de tabelas de Hive no aprendizado de máquina do Azure usando o módulo de importação de dados hello e selecioná-lo para uma experiência de aprendizado de máquina
Comece selecionando **+NOVO** -> **EXPERIMENTO** -> **Experimento em Branco**. Em seguida, de saudação **pesquisa** caixa Olá parte superior esquerda, pesquise "Importar dados". Saudação de arrastar e soltar **importar dados** módulo no módulo de saudação de toouse toohello experimento tela (Olá parte do meio da tela hello) para acesso a dados.

Isso é que hello **importar dados** parece com ao obter dados da tabela de Hive hello:

![Importar Dados obtém os dados](./media/machine-learning-data-science-process-hive-criteo-walkthrough/i3zRaoj.png)

Para Olá **importar dados** módulo, valores de Olá dos parâmetros de saudação que são fornecidas no hello gráfico são apenas exemplos de saudação classificação de valores que você precisa tooprovide. Aqui estão algumas diretrizes gerais sobre como toofill parâmetro hello out definidas para Olá **importar dados** módulo.

1. Escolha "Consulta de Hive" para **Fonte de dados**
2. Em Olá **consulta de banco de dados de Hive** caixa, um simples SELECT * FROM < seu\_banco de dados\_name.your\_tabela\_nome >-é suficiente.
3. **URI do servidor Hcatalog**: se o cluster é"abc", isso é simplesmente: https://abc.azurehdinsight.net
4. **Nome de conta de usuário do Hadoop**: nome de usuário Olá escolhido no momento da saudação de preparação de cluster hello. (Não Olá acesso remoto nome de usuário!)
5. **Senha de conta de usuário do Hadoop**: senha Olá Olá nome de usuário escolhido no momento da saudação de preparação de cluster hello. (Não senha de acesso remoto Olá!)
6. **Local dos dados de saída**: escolha "Azure"
7. **Nome da conta de armazenamento do Azure**: Olá conta de armazenamento associada ao cluster Olá
8. **Chave de conta de armazenamento do Azure**: chave Olá Olá da conta de armazenamento associada Olá cluster.
9. **Nome do contêiner do Azure**: se o nome de cluster Olá é "abc", isso costuma ser simplesmente "abc",.

Uma vez Olá **importar dados** termina a obtenção de dados (consulte escala Olá verde no módulo de saudação), salvar os dados como um conjunto de dados (com um nome de sua escolha). A aparência é a seguinte:

![Importar Dados salva os dados](./media/machine-learning-data-science-process-hive-criteo-walkthrough/oxM73Np.png)

Porta de saudação de saída de saudação do botão direito do mouse **importar dados** módulo. Isso revela uma opção **Salvar como conjunto de dados** e uma opção **Visualizar**. Olá **visualizar** opção, se selecionada, exibe 100 linhas de dados hello, juntamente com um painel à direita que é útil para algumas estatísticas de resumo. dados de toosave, basta selecionar **Salvar como conjunto de dados** e siga as instruções.

tooselect Olá Salvar conjunto de dados para uso em uma experiência de aprendizado de máquina, localize Olá conjuntos de dados usando Olá **pesquisa** caixa mostrada na figura a seguir de saudação. Em seguida, basta digitar nome hello você deu Olá conjunto de dados parcialmente tooaccess-lo e arraste Olá dataset em Olá painel principal. Removendo-o para o painel principal Olá seleciona-lo para uso em modelagem de aprendizado de máquina.

![Drage conjunto de dados para o painel principal Olá](./media/machine-learning-data-science-process-hive-criteo-walkthrough/cl5tpGw.png)

> [!NOTE]
> Faça isso para treinar hello e conjuntos de dados de teste de saudação. Além disso, lembre-se de nome de banco de dados toouse hello e nomes de tabela que você atribuiu para essa finalidade. valores de saudação usados na Figura Olá são apenas para ilustração purposes.* *
> 
> 

### <a name="step2"></a>Etapa 2: Criar uma experiência simples no aprendizado de máquina do Azure toopredict cliques / nenhuma cliques
Nosso experimento do AM do Azure tem esta aparência:

![Teste do Machine Learning](./media/machine-learning-data-science-process-hive-criteo-walkthrough/xRpVfrY.png)

Agora, podemos examinar principais componentes de saudação desse teste. Como um lembrete, é preciso toodrag nosso salvo treinar e testar os conjuntos de dados na tela de experimento tooour primeiro.

#### <a name="clean-missing-data"></a>Limpar dados ausentes
Olá **limpar dados ausentes** módulo faz o nome sugere: limpa os dados ausentes de maneiras que podem ser especificados pelo usuário. Examinando este módulo, vemos isso:

![Limpar dados ausentes](./media/machine-learning-data-science-process-hive-criteo-walkthrough/0ycXod6.png)

Aqui, escolhemos tooreplace todos os valores ausentes com um 0. Há outras opções, que podem ser vistas examinando as listas suspensas de saudação no módulo hello.

#### <a name="feature-engineering-on-hello-data"></a>Engenharia de recurso nos dados Olá
Pode haver milhões de valores exclusivos para alguns recursos categóricos de grandes conjuntos de dados. Usar métodos simples como codificação one-hot para representar recursos categóricos altamente dimensionais é totalmente impraticável. Neste passo a passo, demonstraremos como recursos de contagem de toouse usando toogenerate interna de módulos de aprendizado de máquina do Azure compact representações dessas variáveis categóricas altamente dimensional. Olá resultado final é um tamanho menor de modelo, mais rápidos de treinamento e métricas de desempenho que são bastante semelhante toousing outras técnicas.

##### <a name="building-counting-transforms"></a>Criando transformações de contagem
recursos de contagem de toobuild, usamos Olá **criar contagem transformar** módulo que está disponível no aprendizado de máquina do Azure. módulo de saudação tem esta aparência:

![Módulo Compilar Transformação de Contagem](./media/machine-learning-data-science-process-hive-criteo-walkthrough/e0eqKtZ.png)
![Módulo Compilar Transformação de Contagem](./media/machine-learning-data-science-process-hive-criteo-walkthrough/OdDN0vw.png)

> [!IMPORTANT] 
> Em Olá **contagem de colunas** caixa, podemos inserir as colunas que desejamos tooperform conta em. Geralmente, essas são (conforme mencionado) colunas categóricas altamente dimensionais. No início de saudação mencionamos Olá Criteo conjunto de dados tem 26 colunas categóricas: de Col15 tooCol40. Aqui, podemos contar todos eles e dar seus índices (de 15 too40 separadas por vírgulas, como mostrado).
> 

módulo Olá toouse Olá MapReduce modo (apropriado para grandes conjuntos de dados), é necessário acessar o cluster HDInsight Hadoop de tooan (Olá usada para exploração de recurso pode ser reutilizada para essa finalidade bem) e suas credenciais. figuras anteriores Olá ilustram quais Olá preenchido valores como (substituir valores hello fornecidos para ilustração com aqueles relevantes para seu próprio caso de uso).

![Parâmetros do módulo](./media/machine-learning-data-science-process-hive-criteo-walkthrough/05IqySf.png)

Figura Olá acima, mostramos como o blob de entrada hello tooenter local. Esse local tem dados de saudação reservados para a criação de tabelas de contagem.

Após esse módulo de execução, poderemos Salvar transformação Olá para mais tarde clicando duas vezes o módulo hello e selecionando Olá **Salvar como transformar** opção:

![Opção “Salvar como transformação”](./media/machine-learning-data-science-process-hive-criteo-walkthrough/IcVgvHR.png)

Em nossa arquitetura de teste mostrada acima, dataset hello "ytransform2" corresponde precisamente tooa salvo transformação de contagem. Restante Olá esse teste, vamos supor que leitor Olá usado um **criar contagem transformar** módulo em alguns dados toogenerate contagens e, em seguida, pode usar esses recursos de contagem de toogenerate contagens em trem hello e conjuntos de dados de teste.

##### <a name="choosing-what-count-features-tooinclude-as-part-of-hello-train-and-test-datasets"></a>Escolher o que contar tooinclude recursos como parte de treinar hello e conjuntos de dados de teste
Assim que tivermos uma contagem de transformar pronto, usuário Olá pode escolher quais tooinclude recursos em seu treinar e testar conjuntos de dados usando Olá **modificar parâmetros de tabela de contagem** módulo. Vamos mostrar esse módulo aqui para fins de conclusão, mas, para manter a simplicidade, não use de fato no nosso experimento.

![Parâmetros Modificar Tabela de Contagem](./media/machine-learning-data-science-process-hive-criteo-walkthrough/PfCHkVg.png)

Nesse caso, como pode ser visto, escolhemos toouse probabilidades de log apenas hello e tooignore Olá retirada da coluna. Podemos também definir parâmetros, como o limite de compartimento de lixo hello, quantos tooadd exemplos pseudo anterior para suavizar, e se toouse qualquer Laplaciana de ruído ou não. Todos esses são os recursos avançados e é toobe observado valores padrão de saudação são um bom ponto de partida para usuários que são um novo tipo de toothis de geração de recurso.

##### <a name="data-transformation-before-generating-hello-count-features"></a>Transformação de dados antes de gerar recursos de contagem de saudação
Agora se concentrar em um ponto importante sobre como transformar nosso treinar e testar dados tooactually anteriores gerar recursos de contagem. Observe que há dois **Executar Script R** módulos usados antes de ser dados de tooour de transformação de contagem de saudação.

![Executar Script R](./media/machine-learning-data-science-process-hive-criteo-walkthrough/aF59wbc.png)

Aqui está o script de R primeiro hello:

![Primeiro script R](./media/machine-learning-data-science-process-hive-criteo-walkthrough/3hkIoMx.png)

Nesse script R, podemos renomear nossa toonames colunas "Col1" muito "Col40". Isso ocorre porque a transformação de contagem de saudação espera nomes desse formato.

Script de R segundo Olá, podemos equilibrar distribuição Olá entre classes positivos e negativos (classes 1 e 0 respectivamente) pela classe negativo de saudação da resolução. Olá R script aqui mostra como toodo isso:

![Segundo script R](./media/machine-learning-data-science-process-hive-criteo-walkthrough/91wvcwN.png)

Esse script simple do R, usamos "pos\_neg\_taxa" quantidade de saudação do tooset de equilíbrio entre hello positivo e classes negativo hello. Isso é importante toodo como melhorar desequilíbrio de classe normalmente tem benefícios de desempenho para problemas de classificação em que a distribuição de classe Olá é desviada (Lembre-se que em nosso caso, temos classes positivo 3.3% e 96,7% negativo).

##### <a name="applying-hello-count-transformation-on-our-data"></a>Aplicar transformação de contagem de saudação em nossos dados
Por fim, podemos usar Olá **Aplicar transformação** tooapply módulo Olá transformações de contagem em nosso treinar e testar conjuntos de dados. Este módulo usa a transformação de contagem de saudação salvada como uma entrada e hello treinar ou testar conjuntos de dados como Olá outras entradas e retorna dados com recursos de contagem. Isso é mostrado aqui:

![Aplicar o módulo de transformação](./media/machine-learning-data-science-process-hive-criteo-walkthrough/xnQvsYf.png)

##### <a name="an-excerpt-of-what-hello-count-features-look-like"></a>Um trecho da aparência de recursos de contagem de saudação
É instrutivo toosee quais recursos de contagem de saudação aparecem no nosso caso. Mostramos aqui um trecho disso:

![Recursos de contagem](./media/machine-learning-data-science-process-hive-criteo-walkthrough/FO1nNfw.png)

Neste trecho, mostramos que para as colunas de saudação que são contados em, podemos obter contagens de saudação e probabilidades de log em adição tooany relevantes backoffs.

Agora estamos pronto toobuild um modelo de aprendizado de máquina do Azure usando esses conjuntos de dados transformados. Na próxima seção, Olá, mostramos como isso pode ser feito.

### <a name="step3"></a>Etapa 3: Criar, treinar e classificar Olá modelo

#### <a name="choice-of-learner"></a>Opção do aprendiz
Primeiro, precisamos toochoose um aprendiz. Estamos indo toouse uma árvore de decisão de duas classes ampliada como nosso aprendiz. Aqui estão as opções padrão da saudação esse aprendiz:

![Parâmetros da árvore de decisão aumentada de duas classes](./media/machine-learning-data-science-process-hive-criteo-walkthrough/bH3ST2z.png)

Para nossa experiência, estamos valores padrão do andamento toochoose hello. Observe que Olá padrões são geralmente significativa e uma boa maneira tooget rápido linhas de base de desempenho. Você pode melhorar o desempenho por varredura parâmetros se você escolher tooonce que você tem uma linha de base.

#### <a name="train-hello-model"></a>Treinar modelo de saudação
Para obter treinamento, podemos simplesmente invocar um módulo **Modelo de treinamento** . Olá duas entradas tooit são Aprendiz de árvore de decisão ampliada duas classes hello e nosso conjunto de dados de treinamento. Isso é mostrado aqui:

![Módulo Treinar Modelo](./media/machine-learning-data-science-process-hive-criteo-walkthrough/2bZDZTy.png)

#### <a name="score-hello-model"></a>Modelo de saudação de pontuação
Assim que tivermos um modelo treinado, estamos prontos tooscore em Olá testar dataset e tooevaluate seu desempenho. Podemos fazer isso usando Olá **modelo de pontuação** módulo mostrado Olá seguinte figura, juntamente com um **avaliar modelo** módulo:

![Módulo de Modelo de Pontuação](./media/machine-learning-data-science-process-hive-criteo-walkthrough/fydcv6u.png)

### <a name="step4"></a>Etapa 4: Avaliar modelo Olá
Por fim, esperamos que tooanalyze o desempenho do modelo. Geralmente, para dois problemas de classificação (binário) de classe, um bom exemplo é hello AUC. toovisualize isso, podemos conectar Olá **modelo de pontuação** módulo tooan **avaliar modelo** módulo para isso. Clicando em **visualizar** em Olá **avaliar modelo** módulo produz um gráfico como Olá seguindo um:

![Avaliar o modelo de BDT do módulo](./media/machine-learning-data-science-process-hive-criteo-walkthrough/0Tl0cdg.png)

Binário (ou classe dois) problemas de classificação, uma boa medida de precisão da previsão é Olá área na curva (AUC). A seguir, mostramos nossos resultados usando esse modelo em nosso conjunto de dados de teste. tooget porta de saída de hello, com o botão direito da saudação **avaliar modelo** módulo e, em seguida, **visualizar**.

![Módulo Visualizar modelo de avaliação](./media/machine-learning-data-science-process-hive-criteo-walkthrough/IRfc7fH.png)

### <a name="step5"></a>Etapa 5: Publicar o modelo de saudação como um serviço Web
Olá capacidade toopublish um modelo de aprendizado de máquina do Azure como serviços web com um mínimo de confusão é um recurso valioso para disponibilizá-la amplamente. Depois disso, qualquer pessoa poderá tornar o serviço web toohello chamadas com dados de entrada que precisam que as previsões para, e serviço web de saudação usa Olá modelo tooreturn essas previsões.

toodo isso, podemos primeiro salvar nosso modelo treinado como um objeto de modelo treinado. Isso é feito clicando Olá **treinar modelo** módulo e usar Olá **Salvar como modelo treinado** opção.

Em seguida, precisamos toocreate de entrada e saída de portas para nosso serviço web:

* uma porta de entrada usa dados em Olá mesmo formulário como dados de saudação que precisamos previsões para
* uma porta de saída retorna Olá rótulos de pontuação e as probabilidades de saudação associada.

#### <a name="select-a-few-rows-of-data-for-hello-input-port"></a>Selecione algumas linhas de dados para a porta de entrada hello
É conveniente toouse um **Aplicar transformação de SQL** dados de porta de entrada do módulo tooselect apenas 10 linhas tooserve como Olá. Selecione apenas essas linhas de dados da nossa porta de entrada usando a consulta SQL Olá mostrada aqui:

![Dados na porta de entrada](./media/machine-learning-data-science-process-hive-criteo-walkthrough/XqVtSxu.png)

#### <a name="web-service"></a>Serviço Web
Agora estamos prontos toorun um experimento pequeno que pode ser usado toopublish nosso serviço web.

#### <a name="generate-input-data-for-webservice"></a>Gerar dados de entrada para o serviço Web
Como uma etapa de zero, como tabela de contagem de saudação for grande, vamos poucas linhas de dados de teste e gerar dados de saída dele com recursos de contagem. Isso pode servir como formato de dados de entrada hello para nosso serviço Web. Isso é mostrado aqui:

![Criar dados de entrada de BDT](./media/machine-learning-data-science-process-hive-criteo-walkthrough/OEJMmst.png)

> [!NOTE]
> Para o formato de dados de entrada hello, agora podemos usar Olá saída de hello **Featurizer de contagem** módulo. Depois que isso experimentar termina em execução, salvar a saída de saudação do hello **Featurizer de contagem** módulo como um conjunto de dados. Este conjunto de dados é usado para dados de entrada hello em Olá webservice.
> 
> 

#### <a name="scoring-experiment-for-publishing-webservice"></a>Experimento de pontuação publicação do serviço Web
Primeiro, mostramos sua aparência. estrutura essencial Olá é um **modelo de pontuação** módulo que aceita nosso objeto treinado e algumas linhas de dados de entrada que são gerados nas etapas anteriores de saudação usando Olá **Featurizer de contagem** módulo. Usamos tooproject "Selecionar colunas no conjunto de dados" hello classificado rótulos e as probabilidades de pontuação hello.

![Projetar Colunas no Conjunto de Dados](./media/machine-learning-data-science-process-hive-criteo-walkthrough/kRHrIbe.png)

Observe como Olá **selecionar colunas no conjunto de dados** módulo pode ser usado para 'Filtrar' dados de um conjunto de dados. Vamos mostrar o conteúdo de saudação aqui:

![Filtrando com hello selecionar colunas no módulo de conjunto de dados](./media/machine-learning-data-science-process-hive-criteo-walkthrough/oVUJC9K.png)

portas de saudação azul de entrada e saída tooget, basta clicar em **preparar webservice** na parte inferior de saudação à direita. Executar esse teste também permite que nós toopublish Olá web serviço: clique em Olá **publicar WEB SERVICE** ícone no hello inferior direita mostrado aqui:

![PUBLICAR SERVIÇO WEB](./media/machine-learning-data-science-process-hive-criteo-walkthrough/WO0nens.png)

Depois de publicado webservice hello, obtemos tooa redirecionado página que parece assim:

![Painel de serviço Web](./media/machine-learning-data-science-process-hive-criteo-walkthrough/YKzxAA5.png)

Podemos ver dois links para webservices no lado esquerdo da saudação:

* Olá **solicitação/resposta** serviço (ou RRS) são destinados para previsões únicas e é o que utilizamos este workshop.
* Olá **BATCH EXECUTION** Service (BES) é usada para previsões em lote e requer que Olá dados de entrada usados toomake previsões residem no armazenamento de BLOBs do Azure.

Clicando no link Olá **solicitação/resposta** levamos tooa página que nos permite previamente gravados código em c#, python e R. Esse código pode ser usado para fazer chamadas toohello webservice convenientemente. Observe que a chave de API nesta página Olá precisa toobe usado para autenticação.

É conveniente toocopy este python code pela nova célula tooa no bloco de anotações de IPython hello.

Aqui, mostramos um segmento de código python com chave de API Olá correto.

![Código Python](./media/machine-learning-data-science-process-hive-criteo-walkthrough/f8N4L4g.png)

Observe que substituímos chave de API saudação padrão com a chave de API do nosso webservices. Clicando em **executar** nessa célula em uma IPython notebook gera Olá resposta a seguir:

![Resposta do IPython](./media/machine-learning-data-science-process-hive-criteo-walkthrough/KSxmia2.png)

Podemos ver para Olá dois teste exemplos que perguntamos (na estrutura JSON de saudação do script de python Olá), obtemos respostas na forma de hello "Classificado rótulos, classificado probabilidades". Observe que nesse caso, escolhemos valores padrão de saudação código pré-configurado Olá fornece (0 para todas as colunas numéricas e de cadeia de caracteres hello "value" para todas as colunas categóricas).

Isso conclui nosso mostrando passo a passo de ponta a ponta como toohandle conjunto de dados em larga escala usando o aprendizado de máquina do Azure. Começamos com um terabyte de dados, criado um modelo de previsão e implantá-lo como um serviço web na nuvem hello.

