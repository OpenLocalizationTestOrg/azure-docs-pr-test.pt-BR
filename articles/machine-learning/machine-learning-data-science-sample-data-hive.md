---
title: aaaSample dados nas tabelas do Azure HDInsight Hive | Microsoft Docs
description: Reduzir os dados de amostragem em Tabelas Hive do Azure HDInsight (Hadoop)
services: machine-learning,hdinsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: f31e8d01-0fd4-4a10-b1a7-35de3c327521
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: hangzh;bradsev
ms.openlocfilehash: 5f86df9b5a18facc875f437abfb004dbe3a06ea4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="sample-data-in-azure-hdinsight-hive-tables"></a>Dados de exemplo nas tabelas Hive do Azure HDInsight
Neste artigo, descrevemos como exemplo de toodown dados armazenados nas tabelas do Azure HDInsight Hive usando consultas de Hive. Abordaremos três métodos de amostragem popularmente usados:

* Amostragem aleatória uniforme
* Amostragem aleatória por grupos
* Amostragem estratificada

a seguir Olá **menu** links tootopics que descrevem como toosample dados de vários ambientes de armazenamento.

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

**Por que fazer amostragem dos dados?**
Se dataset Olá planejar tooanalyze for grande, normalmente é um tooreduce de dados de exemplo toodown Olá boa ideia-tooa menor, mas representativo e mais fácil de gerenciar o tamanho. Isso facilita a compreensão de dados, exploração e engenharia de recursos. Sua função no hello processo de ciência de dados de equipe é tooenable rápida criação de protótipos de funções de processamento de dados de saudação e modelos de aprendizado de máquina.

Esta tarefa de amostragem é uma etapa Olá [processo de ciência de dados da equipe (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).

## <a name="how-toosubmit-hive-queries"></a>Como consultas de Hive toosubmit
Consultas de hive podem ser enviadas no console de linha de comando do Hadoop de Olá no nó principal de saudação do cluster de Hadoop de saudação. toodo isso, faça logon no nó principal de saudação do cluster de Hadoop Olá, abrir Olá console de linha de comando do Hadoop e enviar consultas de Hive hello a partir daí. Para obter instruções sobre o envio de consultas de Hive no console de linha de comando do Hadoop hello, consulte [como tooSubmit consultas Hive](machine-learning-data-science-move-hive-tables.md#submit).

## <a name="uniform"></a> Amostragem aleatória uniforme
Amostragem aleatória uniforme significa que cada linha no conjunto de dados Olá tem a mesma chance de amostra. Isso pode ser implementado com a adição de um conjunto de dados do campo extra rand () toohello na consulta interna de "select" hello e em Olá externa consulta "select" essa condição nesse campo aleatório.

Veja um exemplo de consulta:

    SET sampleRate=<sample rate, 0-1>;
    select
        field1, field2, …, fieldN
    from
        (
        select
            field1, field2, …, fieldN, rand() as samplekey
        from <hive table name>
        )a
    where samplekey<='${hiveconf:sampleRate}'

Aqui, `<sample rate, 0-1>` Especifica a proporção de saudação de registros que desejam que os usuários de saudação toosample.

## <a name="group"></a> Amostragem aleatória por grupos
Quando dados categóricos de amostragem, convém tooeither incluir ou excluir todas as instâncias de saudação de algum valor específico de uma variável categórica. Isso é o que "amostragem por grupo” significa.
Por exemplo, se você tiver uma variável categórica "Estado", que tem valores NY MA, Canadá, NJ, PA, etc, você deseja que os registros de saudação mesmo estado ser sempre juntos, eles são exemplificados ou não.

Veja um exemplo de consulta com amostragem por grupo:

    SET sampleRate=<sample rate, 0-1>;
    select
        b.field1, b.field2, …, b.catfield, …, b.fieldN
    from
        (
        select
            field1, field2, …, catfield, …, fieldN
        from <table name>
        )b
    join
        (
        select
            catfield
        from
            (
            select
                catfield, rand() as samplekey
            from <table name>
            group by catfield
            )a
        where samplekey<='${hiveconf:sampleRate}'
        )c
    on b.catfield=c.catfield

## <a name="stratified"></a>Amostragem estratificada
Amostragem aleatória é estratificada com respeito tooa variável categórica quando exemplos de saudação obtidos têm valores categóricos ou que estão em Olá mesma proporção da população do hello pai da qual Olá exemplos foram obtidos. Usando Olá mesmo exemplo acima, suponha que os dados têm populações sub por estados, digamos NJ tem 100 observações, NY tem 60 observações e WA tem 300 observações. Se você especificar a taxa de saudação do estratificada toobe amostragem 0,5 e hello amostra obtida deve ter aproximadamente 50, 30 e 150 observações de NJ, NY e WA respectivamente.

Veja um exemplo de consulta:

    SET sampleRate=<sample rate, 0-1>;
    select
        field1, field2, field3, ..., fieldN, state
    from
        (
        select
            field1, field2, field3, ..., fieldN, state,
            count(*) over (partition by state) as state_cnt,
              rank() over (partition by state order by rand()) as state_rank
          from <table name>
        ) a
    where state_rank <= state_cnt*'${hiveconf:sampleRate}'


Para obter informações sobre os métodos de amostragem mais avançados disponíveis no Hive, consulte [Amostragem LanguageManual](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Sampling).

