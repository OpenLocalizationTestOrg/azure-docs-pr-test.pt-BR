---
title: recursos de aaaCreate para os dados em um cluster Hadoop usando consultas de Hive | Microsoft Docs
description: Exemplos de consultas de Hive que geram recursos em dados armazenados em um cluster Hadoop do Azure HDInsight.
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: e8a94c71-979b-4707-b8fd-85b47d309a30
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: hangzh;bradsev
ms.openlocfilehash: 686282bf0fb84ea82758d3c5b7de2bd90f0cf159
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-features-for-data-in-an-hadoop-cluster-using-hive-queries"></a>Criar recursos para os dados em um cluster Hadoop usando as consultas do Hive
Este documento mostra como os recursos toocreate para dados armazenados em um cluster de Hadoop de HDInsight do Azure usando consultas de Hive. Essas consultas de Hive usarem incorporado Hive funções definidas pelo usuário (UDFs), scripts de saudação para os quais são fornecidos.

Olá operações necessárias toocreate recursos podem ser uso intensivo de memória. desempenho de saudação de consultas de Hive torna-se mais importante em tais casos e pode ser melhorado com determinados parâmetros de ajuste. Olá ajuste desses parâmetros é discutida na seção de final de saudação.

Exemplos de consultas de saudação que são apresentados são específico toohello [NYC táxi Trip dados](http://chriswhong.com/open-data/foil_nyc_taxi/) cenários também são fornecidos em [repositório GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts). Essas consultas já tiver um esquema de dados especificado e estão pronto toobe enviada toorun. Na seção final do hello, também são discutidos parâmetros que os usuários podem ajustar para que a melhorar o desempenho da saudação de consultas de Hive.

[!INCLUDE [cap-create-features-data-selector](../../includes/cap-create-features-selector.md)]

Isso **menu** links tootopics que descrevem como toocreate recursos para os dados em vários ambientes. Essa tarefa é uma etapa Olá [processo de ciência de dados da equipe (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).

## <a name="prerequisites"></a>Pré-requisitos
Este artigo supõe que você:

* Criou uma conta de armazenamento do Azure. Se precisar de instruções, confira [Criar uma conta de Armazenamento do Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account)
* Provisionar um cluster de Hadoop personalizado com hello serviço HDInsight.  Se precisar de instruções, consulte [Personalizar os clusters do Hadoop do Azure HDInsight para análise avançada](machine-learning-data-science-customize-hadoop-cluster.md).
* dados de saudação foi carregado tooHive tabelas em clusters de Hadoop de HDInsight do Azure. Se não tiver, siga [criar e carregar tabelas de tooHive dados](machine-learning-data-science-move-hive-tables.md) tooupload dados tooHive tabelas primeiro.
* Cluster de toohello de acesso remoto habilitado. Se você precisar de instruções, consulte [Olá acesso cabeçotes de nó de Cluster de Hadoop](machine-learning-data-science-customize-hadoop-cluster.md#headnode).

## <a name="hive-featureengineering"></a>Geração de recursos
Nesta seção, encontram-se vários exemplos de formas de saudação nos quais recursos podem estar gerando usando consultas de Hive. Depois de gerar recursos adicionais, você pode adicioná-los como tabela existente de toohello de colunas ou crie uma nova tabela com recursos adicionais de saudação e a chave primária, que, em seguida, pode ser unido a tabela original hello. Aqui estão exemplos de saudação apresentados:

1. [Geração de recursos baseada em frequência](#hive-frequencyfeature)
2. [Riscos de variáveis categóricas na classificação binária](#hive-riskfeature)
3. [Extrair recursos do campo Datetime](#hive-datefeatures)
4. [Extrair recursos de campo de texto](#hive-textfeatures)
5. [Calcular a distância entre coordenadas de GPS](#hive-gpsdistance)

### <a name="hive-frequencyfeature"></a>Geração de recursos baseada em frequência
Geralmente é útil toocalculate frequências de saudação de níveis de saudação de uma variável categórica, ou frequências Olá determinadas combinações de níveis de diversas variáveis categóricas. Os usuários podem usar o hello toocalculate de script a seguir essas frequências:

        select
            a.<column_name1>, a.<column_name2>, a.sub_count/sum(a.sub_count) over () as frequency
        from
        (
            select
                <column_name1>,<column_name2>, count(*) as sub_count
            from <databasename>.<tablename> group by <column_name1>, <column_name2>
        )a
        order by frequency desc;


### <a name="hive-riskfeature"></a>Riscos de variáveis categóricas na classificação binária
Em classificação binária, precisamos variáveis categóricas do tooconvert não numéricos em recursos numéricos quando modelos hello está sendo usados apenas colocar recursos numéricos. Isso é feito substituindo cada nível não numéricos por um risco numérico. Nesta seção, mostramos algumas consultas de Hive genéricas que calculam valores de risco de saudação (probabilidade de log) de uma variável categórica.

        set smooth_param1=1;
        set smooth_param2=20;
        select
            <column_name1>,<column_name2>,
            ln((sum_target+${hiveconf:smooth_param1})/(record_count-sum_target+${hiveconf:smooth_param2}-${hiveconf:smooth_param1})) as risk
        from
            (
            select
                <column_nam1>, <column_name2>, sum(binary_target) as sum_target, sum(1) as record_count
            from
                (
                select
                    <column_name1>, <column_name2>, if(target_column>0,1,0) as binary_target
                from <databasename>.<tablename>
                )a
            group by <column_name1>, <column_name2>
            )b

Neste exemplo, variáveis `smooth_param1` e `smooth_param2` são conjunto toosmooth Olá risco valores calculados dados saudação. Riscos tem um intervalo entre -Inf e Inf. Riscos > 0 indica que a probabilidade de saudação que destino Olá é igual too1 é maior que 0,5.

Depois que a tabela de riscos Olá é calculada, os usuários podem atribuir a tabela de valores tooa riscos por sua associação com a tabela Olá riscos. consulta de junção de Hive Olá foi fornecida na seção anterior.

### <a name="hive-datefeatures"></a>Extrair recursos de campos Datetime
O Hive vem com um conjunto de UDFs para processar campos datetime. Na seção, formato de datetime saudação padrão é ' AAAA-MM-dd 00:00:00 ' ('1970-01-01 12:21:32 ' por exemplo). Nesta seção, mostramos exemplos que extrair Olá dia de um mês, o mês de saudação de um campo de data/hora e outros exemplos que converter uma cadeia de caracteres de data e hora em um formato diferente de cadeia de caracteres de saudação padrão formato tooa datetime de formato padrão.

        select day(<datetime field>), month(<datetime field>)
        from <databasename>.<tablename>;

Esta consulta de Hive pressupõe que Olá *&#60; o campo de data/hora >* está no formato de data e hora saudação padrão.

Se um campo de data/hora não está no formato de padrão de saudação, precisar campo de data/hora Olá tooconvert primeiro em carimbo de data / hora de Unix e converter Olá Unix tempo tooa de carimbo data/hora da cadeia de caracteres que é no padrão de saudação formato. Quando o datetime de saudação padrão é o formato, os usuários podem aplicar Olá inserido datetime UDFs tooextract recursos.

        select from_unixtime(unix_timestamp(<datetime field>,'<pattern of hello datetime field>'))
        from <databasename>.<tablename>;

Nesta consulta, se hello *&#60; o campo de data/hora >* tem saudação padrão como *26/03/2015 12:04:39*, Olá *' &#60; padrão do campo de data/hora hello >'* devem ser `'MM/dd/yyyy HH:mm:ss'`. tootest, os usuários podem executar

        select from_unixtime(unix_timestamp('05/15/2015 09:32:10','MM/dd/yyyy HH:mm:ss'))
        from hivesampletable limit 1;

Olá *hivesampletable* nessa consulta fornecida pré-instalada em todos os clusters de Hadoop de HDInsight do Azure por padrão quando clusters Olá são provisionados.

### <a name="hive-textfeatures"></a>Extrair recursos de campos de Texto
Quando a tabela de Hive Olá tem um campo de texto que contém uma cadeia de caracteres de palavras que são delimitados por espaços, hello consulta a seguir extrai comprimento Olá de cadeia de caracteres de saudação e número de saudação de palavras na cadeia de caracteres de saudação.

        select length(<text field>) as str_len, size(split(<text field>,' ')) as word_num
        from <databasename>.<tablename>;

### <a name="hive-gpsdistance"></a>Calcular a distância entre conjuntos de coordenadas de GPS
consulta de saudação fornecida nesta seção pode ser aplicado diretamente toohello NYC táxi viagem de dados. finalidade de saudação dessa consulta é tooshow como tooapply inserida funções matemáticas no Hive toogenerate recursos.

campos que são usados nesta consulta Hello são coordenadas GPS Olá dos locais de retirada e redução, denominados *retirada\_longitude*, *retirada\_latitude*,  *redução\_longitude*, e *redução\_latitude*. consultas de saudação que calculam a distância direta Olá entre coordenadas de retirada e redução de saudação são:

        set R=3959;
        set pi=radians(180);
        select pickup_longitude, pickup_latitude, dropoff_longitude, dropoff_latitude,
            ${hiveconf:R}*2*2*atan((1-sqrt(1-pow(sin((dropoff_latitude-pickup_latitude)
            *${hiveconf:pi}/180/2),2)-cos(pickup_latitude*${hiveconf:pi}/180)
            *cos(dropoff_latitude*${hiveconf:pi}/180)*pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2)))
            /sqrt(pow(sin((dropoff_latitude-pickup_latitude)*${hiveconf:pi}/180/2),2)
            +cos(pickup_latitude*${hiveconf:pi}/180)*cos(dropoff_latitude*${hiveconf:pi}/180)*
            pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2))) as direct_distance
        from nyctaxi.trip
        where pickup_longitude between -90 and 0
        and pickup_latitude between 30 and 90
        and dropoff_longitude between -90 and 0
        and dropoff_latitude between 30 and 90
        limit 10;

equações matemáticas de saudação que calculam Olá distância entre duas coordenadas GPS podem ser encontradas no hello <a href="http://www.movable-type.co.uk/scripts/latlong.html" target="_blank">Scripts Movable Type</a> site, criado por Peter Lapisu. Em seu Javascript, Olá função `toRad()` é apenas *lat_or_lon*180/pi *, que converte graus tooradians. Aqui, *lat_or_lon* é Olá latitude ou longitude. Como seção não fornece a função hello `atan2`, mas fornece a função hello `atan`, Olá `atan2` função é implementada pelo `atan` função hello acima consulta de Hive usando definição de saudação fornecida no <a href="http://en.wikipedia.org/wiki/Atan2" target="_blank"> Wikipedia</a>.

![Criar espaço de trabalho](./media/machine-learning-data-science-create-features-hive/atan2new.png)

Uma lista completa de Hive UDFs inseridos podem ser encontrados na Olá **funções internas** seção Olá <a href="https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-MathematicalFunctions" target="_blank">Apache Hive wiki</a>).  

## <a name="tuning"></a>Tópicos avançados: ajustar parâmetros de Hive tooImprove velocidade de consulta
Olá parâmetro padrão configurações de cluster de Hive podem não ser adequadas para consultas de Hive hello e dados de saudação processamento de consultas de saudação. Nesta seção, discutiremos alguns parâmetros que os usuários podem ajustar que melhoram o desempenho de saudação de consultas de Hive. Os usuários precisam de parâmetro de hello tooadd ajuste de consultas antes de consultas de saudação do processamento de dados.

1. **Espaço de pilha Java**: para consultas que envolvem ingressar em grandes conjuntos de dados ou registros de tempo de processamento **ficando sem espaço de heap** é um erro comum de saudação. Isso pode ser ajustado, definindo parâmetros *mapreduce.map.java.opts* e *mapreduce.task.io.sort.mb* toodesired valores. Aqui está um exemplo:
   
        set mapreduce.map.java.opts=-Xmx4096m;
        set mapreduce.task.io.sort.mb=-Xmx1024m;

    Esse parâmetro aloca espaço de heap de tooJava de memória de 4GB e também torna a classificação mais eficiente alocando mais memória para ela. É tooplay uma boa ideia com essas alocações se houver qualquer trabalho falha erros relacionados tooheap espaço.

1. **Tamanho do bloco DFS** : esse parâmetro define Olá menor unidade de dados que Olá repositórios do sistema de arquivos. Como exemplo, se o tamanho do bloco DFS Olá é 128MB, em seguida, todos os dados de tamanho menor e backup too128MB são armazenados em um único bloco, enquanto os dados que é maiores do que 128MB é alocado blocos extras. Escolha um tamanho de bloco muito pequeno faz com que grandes sobrecargas no Hadoop como nó de nome hello tem tooprocess muitos mais solicitações toofind Olá relevantes bloco pertencente toohello arquivo. Uma configuração recomendada ao trabalhar com gigabytes de dados (ou mais ainda) é:
   
        set dfs.block.size=128m;
2. **Otimizando a operação de junção na seção** : enquanto as operações de associação no framework de mapeamento/redução Olá normalmente ocorrem no hello reduzir fase, às vezes, podem-se obter ganhos enormes agendando junções na fase de mapa de saudação (também chamado de "mapjoins"). toodirect Hive toodo isso sempre que possível, podemos definir:
   
        set hive.auto.convert.join=true;
3. **Especificando o número de saudação do mapeadores tooHive** : Hadoop enquanto permite Olá usuário tooset Olá inúmeros reducers, número de saudação de mapeadores é normalmente não ser definida pelo usuário hello. Um truque que permite que um certo grau de controle sobre esse número é toochoose variáveis de Hadoop hello, *mapred.min.split.size* e *mapred.max.split.size* como tamanho de saudação do mapa de cada tarefa é determinada por:
   
        num_maps = max(mapred.min.split.size, min(mapred.max.split.size, dfs.block.size))
   
    Olá normalmente, o valor padrão de *mapred.min.split.size* é 0, que de *mapred.max.split.size* é **Long.MAX** e de *dfs.block.size* é 64MB. Como podemos ver, tamanho de dados determinado hello, ajuste esses parâmetros por "Configurando"-los permite nos tootune Olá número de mapeadores usado.
4. Algumas outras opções mais **avançadas** para otimizar o desempenho de Hive são mencionadas a seguir. Esses permitem tooset Olá memória alocada toomap e reduzem as tarefas e podem ser útil para ajustar o desempenho. Tenha em mente que Olá *MapReduce* não pode ser maior que o tamanho da memória física saudação de cada nó no cluster de Hadoop de saudação de trabalho.
   
        set mapreduce.map.memory.mb = 2048;
        set mapreduce.reduce.memory.mb=6144;
        set mapreduce.reduce.java.opts=-Xmx8192m;
        set mapred.reduce.tasks=128;
        set mapred.tasktracker.reduce.tasks.maximum=128;

