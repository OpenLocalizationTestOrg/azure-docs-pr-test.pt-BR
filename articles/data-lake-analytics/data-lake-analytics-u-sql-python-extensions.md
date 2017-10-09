---
title: "scripts de aaaExtend U-SQL com Python na análise do Azure Data Lake | Microsoft Docs"
description: "Saiba como toorun Python código nos Scripts U-SQL"
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: jhubbard
editor: cgronlun
ms.assetid: c1c74e5e-3e4a-41ab-9e3f-e9085da1d315
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/20/2017
ms.author: saveenr
ms.openlocfilehash: f051f56f67522d4f2b8e6e54fd21a5c95ce3ba92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-get-started-with-extending-u-sql-with-python"></a>Tutorial: introdução à extensão do U-SQL com o Python

Extensões de Python para U-SQL permitem que os desenvolvedores tooperform paralela em grande escala a execução de código Python. saudação de exemplo a seguir ilustra as etapas básicas hello:

* Saudação de uso `REFERENCE ASSEMBLY` extensões de Python de tooenable de instrução para Olá Script U-SQL
* Usando Olá `REDUCE` dados em uma chave de entrada de saudação do toopartition de operação
* extensões do Python para U-SQL Hello incluem um redutor interno (`Extension.Python.Reducer`) que executa o código Python em Redutor de toohello cada vértice atribuído
* Olá script U-SQL contém código Python Olá inserido que tem uma função chamada `usqlml_main` que aceita um pandas DataFrame como entrada e retorna um pandas DataFrame como saída.

--

    REFERENCE ASSEMBLY [ExtPython];

    DECLARE @myScript = @"
    def get_mentions(tweet):
        return ';'.join( ( w[1:] for w in tweet.split() if w[0]=='@' ) )

    def usqlml_main(df):
        del df['time']
        del df['author']
        df['mentions'] = df.tweet.apply(get_mentions)
        del df['tweet']
        return df
    ";

    @t  = 
        SELECT * FROM 
           (VALUES
               ("D1","T1","A1","@foo Hello World @bar"),
               ("D2","T2","A2","@baz Hello World @beer")
           ) AS 
               D( date, time, author, tweet );

    @m  =
        REDUCE @t ON date
        PRODUCE date string, mentions string
        USING new Extension.Python.Reducer(pyScript:@myScript);

    OUTPUT @m
        too"/tweetmentions.csv"
        USING Outputters.Csv();

## <a name="how-python-integrates-with-u-sql"></a>Como o Python se integra com o U-SQL

### <a name="datatypes"></a>Tipos de dados

* As cadeias de caracteres e colunas numéricas do U-SQL são convertidas como estão entre Pandas e U-SQL
* U-SQL nulos são convertido tooand de Pandas `NA` valores

### <a name="schemas"></a>Esquemas

* Os vetores de índice no Pandas não têm suporte no U-SQL. Todos os quadros de dados de entrada na função de Python Olá sempre tem um índice numérico de 64 bits de 0 até Olá número de linhas menos 1. 
* Conjuntos de dados U-SQL não podem ter nomes de coluna duplicados
* Nomes de coluna de conjuntos de dados U-SQL que não são cadeias de caracteres. 

### <a name="python-versions"></a>Versões do Python
Há suporte somente para o Python 3.5.1 (compilado para Windows). 

### <a name="standard-python-modules"></a>Módulos de Python Standard
Todos os módulos Python saudação padrão são incluídos.

### <a name="additional-python-modules"></a>Módulos de Python adicionais
Além de hello bibliotecas Python padrão, várias bibliotecas python usadas estão incluídas:

    pandas
    numpy
    numexpr

### <a name="exception-messages"></a>Mensagens de Exceção
Atualmente, uma exceção no código Python aparece como falha genérica de vértice. Olá futuras, mensagens de erro do trabalho U-SQL Olá exibirá mensagem de exceção saudação do Python.

### <a name="input-and-output-size-limitations"></a>Limitações de tamanho de Entrada e Saída
Cada vértice tem uma quantidade limitada de memória atribuída tooit. Atualmente, esse limite é de 6 GB para um AU. Porque hello quadros de dados de entrada e saídos devem existir na memória no código do Python hello, o tamanho total Olá Olá entrada e saída não pode exceder 6 GB.

## <a name="see-also"></a>Consulte também
* [Visão geral da Análise do Microsoft Azure Data Lake](data-lake-analytics-overview.md)
* [Desenvolver scripts U-SQL usando as Ferramentas do Data Lake para Visual Studio](data-lake-analytics-data-lake-tools-get-started.md)
* [Usar funções da janela do U-SQL para trabalhos de análise do Azure Data Lake](data-lake-analytics-use-window-functions.md)

