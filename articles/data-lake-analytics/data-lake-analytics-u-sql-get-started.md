---
title: "Introdução à linguagem U-SQL | Microsoft Docs"
description: "Conheça os fundamentos de saudação da saudação linguagem U-SQL."
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: 57143396-ab86-47dd-b6f8-613ba28c28d2
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/23/2017
ms.author: saveenr
ms.openlocfilehash: 5edee0e0d85211e84b3d47895c53d71f0a19f083
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-u-sql"></a>Introdução ao U-SQL
U-SQL é uma linguagem que combina SQL declarativa com fundamental c# toolet você processar dados em qualquer escala. Olá escalonável e de consulta distribuída com o recurso de U-SQL, você pode analisar com eficiência dados em repositórios relacionais, como o banco de dados do SQL Azure. Com o U-SQL, você pode processar dados não estruturados aplicando o esquema na leitura e inserindo lógica personalizada e UDFs. Além disso, U-SQL inclui extensibilidade que lhe dá controle refinado como tooexecute em escala. 

## <a name="learning-resources"></a>Recursos de aprendizagem

* Olá [U-SQL Tutorial](http://aka.ms/usqltutorial) fornece uma passo a passo guiado da maioria dos idiomas Olá U-SQL. Este documento é recomendado para todos os desenvolvedores que desejam toolearn U-SQL de leitura.
* Para obter informações detalhadas sobre Olá **sintaxe de linguagem SQL U**, consulte Olá [referência de linguagem SQL U](http://go.microsoft.com/fwlink/p/?LinkId=691348).
* Olá toounderstand **filosofia de design U-SQL**, consulte a postagem do blog do Visual Studio Olá [apresentando U-SQL – A linguagem que torna fácil de processamento de dados grande](https://blogs.msdn.microsoft.com/visualstudio/2015/09/28/introducing-u-sql-a-language-that-makes-big-data-processing-easy/).

## <a name="prerequisites"></a>Pré-requisitos

Antes de passar pelos exemplos Olá U-SQL neste documento, ler e concluir [Tutorial: scripts de desenvolver U-SQL usando o Data Lake Tools para Visual Studio](data-lake-analytics-data-lake-tools-get-started.md). Esse tutorial explica os mecanismos de saudação do uso de U-SQL com o Azure Data Lake Tools para Visual Studio.

## <a name="your-first-u-sql-script"></a>Seu primeiro script U-SQL

Olá script U-SQL a seguir é simple e permite explorar o idioma de saudação U-SQL muitos aspectos.

```
@searchlog =
    EXTRACT UserId          int,
            Start           DateTime,
            Region          string,
            Query           string,
            Duration        int?,
            Urls            string,
            ClickedUrls     string
    FROM "/Samples/Data/SearchLog.tsv"
    USING Extractors.Tsv();

OUTPUT @searchlog   
    too"/output/SearchLog-first-u-sql.csv"
    USING Outputters.Csv();
```

Esse script não possui nenhuma etapa de transformação. Ele lê a partir do arquivo de origem Olá chamado `SearchLog.tsv`, schematizes-lo e grava Olá linhas em um arquivo chamado SearchLog primeiro-u sql.csv.

Observe Olá ponto de interrogação próximo toohello tipo de dados em Olá `Duration` campo. Isso significa que Olá `Duration` campo pode ser nulo.

### <a name="key-concepts"></a>Principais conceitos
* **Variáveis de conjunto de linhas**: cada expressão de consulta que produz um conjunto de linhas pode ser atribuída tooa variável. U-SQL segue o padrão de nomenclatura variável Olá T-SQL (`@searchlog`, por exemplo) no script hello.
* Olá **EXTRAIR** lê dados de um arquivo de palavra-chave e define o esquema de saudação na leitura. `Extractors.Tsv` é um extrator U-SQL interno para arquivos de valores separados por tabulação. Você pode desenvolver extratores personalizados.
* Olá **saída** grava os dados de um arquivo de tooa do conjunto de linhas. `Outputters.Csv()`é um toocreate de outputter U-SQL interna de um arquivo de valores separados por vírgula. Você pode desenvolver outputters personalizados.

### <a name="file-paths"></a>Caminhos de arquivo

Olá EXTRAIR e declarações de saída usam caminhos de arquivo. Os caminhos de arquivo podem ser absolutos ou relativos:

Esse caminho de arquivo absoluto seguir refere-se tooa arquivo em um repositório do Data Lake chamado `mystore`:

    adl://mystore.azuredatalakestore.net/Samples/Data/SearchLog.tsv

O caminho de arquivo a seguir começa com `"/"`. Ela se refere a arquivos tooa na conta de repositório Data Lake saudação padrão:

    /output/SearchLog-first-u-sql.csv

## <a name="use-scalar-variables"></a>Usar variáveis escalares

Você pode usar variáveis escalares como toomake bem a manutenção do seu script mais fácil. script U-SQL anterior de saudação também pode ser escrito como:

    DECLARE @in  string = "/Samples/Data/SearchLog.tsv";
    DECLARE @out string = "/output/SearchLog-scalar-variables.csv";

    @searchlog =
        EXTRACT UserId          int,
                Start           DateTime,
                Region          string,
                Query           string,
                Duration        int?,
                Urls            string,
                ClickedUrls     string
        FROM @in
        USING Extractors.Tsv();

    OUTPUT @searchlog   
        too@out
        USING Outputters.Csv();

## <a name="transform-rowsets"></a>Transformar conjuntos de linhas

Use **selecione** tootransform conjuntos de linhas:

    @searchlog =
        EXTRACT UserId          int,
                Start           DateTime,
                Region          string,
                Query           string,
                Duration        int?,
                Urls            string,
                ClickedUrls     string
        FROM "/Samples/Data/SearchLog.tsv"
        USING Extractors.Tsv();

    @rs1 =
        SELECT Start, Region, Duration
        FROM @searchlog
    WHERE Region == "en-gb";

    OUTPUT @rs1   
        too"/output/SearchLog-transform-rowsets.csv"
        USING Outputters.Csv();

Olá a cláusula WHERE usa um [c# booliana](https://msdn.microsoft.com/library/6a71f45d.aspx). Você pode usar o hello c# expressão idioma toodo suas próprias expressões e funções. Você pode até mesmo executar uma filtragem mais complexa combinando-os com associações lógicas (ANDs) e desassociações (ORs).

Olá script a seguir usa o método de DateTime.Parse() hello e um conjunto.

    @searchlog =
        EXTRACT UserId          int,
                Start           DateTime,
                Region          string,
                Query           string,
                Duration        int?,
                Urls            string,
                ClickedUrls     string
        FROM "/Samples/Data/SearchLog.tsv"
        USING Extractors.Tsv();

    @rs1 =
        SELECT Start, Region, Duration
        FROM @searchlog
    WHERE Region == "en-gb";

    @rs1 =
        SELECT Start, Region, Duration
        FROM @rs1
        WHERE Start >= DateTime.Parse("2012/02/16") AND Start <= DateTime.Parse("2012/02/17");

    OUTPUT @rs1   
        too"/output/SearchLog-transform-datetime.csv"
        USING Outputters.Csv();

 >[!NOTE]
 >consulta segundo Hello está operando no resultado de saudação do hello primeiro conjunto de linhas, que cria uma composição da saudação dois filtros. Também é possível reutilizar um nome de variável e nomes de saudação passam lexicalmente.

## <a name="aggregate-rowsets"></a>Agregar conjuntos de linhas
Fornece U-SQL Olá familiar ORDER BY, GROUP BY e agregações.

Olá consulta a seguir localiza a duração total da saudação por região e exibe superior Olá cinco durações na ordem.

Conjuntos de linhas U-SQL não preservar a ordem para consulta seguinte Olá. Portanto, tooorder uma saída, você precisa tooadd instrução ORDER BY toohello saída:

    DECLARE @outpref string = "/output/Searchlog-aggregation";
    DECLARE @out1    string = @outpref+"_agg.csv";
    DECLARE @out2    string = @outpref+"_top5agg.csv";

    @searchlog =
        EXTRACT UserId          int,
                Start           DateTime,
                Region          string,
                Query           string,
                Duration        int?,
                Urls            string,
                ClickedUrls     string
        FROM "/Samples/Data/SearchLog.tsv"
        USING Extractors.Tsv();

    @rs1 =
        SELECT
            Region,
            SUM(Duration) AS TotalDuration
        FROM @searchlog
    GROUP BY Region;

    @res =
        SELECT *
        FROM @rs1
        ORDER BY TotalDuration DESC
        FETCH 5 ROWS;

    OUTPUT @rs1
        too@out1
        ORDER BY TotalDuration DESC
        USING Outputters.Csv();

    OUTPUT @res
        too@out2
        ORDER BY TotalDuration DESC
        USING Outputters.Csv();

Olá U-SQL ORDER BY cláusula requer usando a cláusula de busca de saudação em uma expressão de seleção.

a cláusula de ter U-SQL de Olá pode ser usado toorestrict Olá saída toogroups que satisfazem a condição HAVING hello:

    @searchlog =
        EXTRACT UserId          int,
                Start           DateTime,
                Region          string,
                Query           string,
                Duration        int?,
                Urls            string,
                ClickedUrls     string
        FROM "/Samples/Data/SearchLog.tsv"
        USING Extractors.Tsv();

    @res =
        SELECT
            Region,
            SUM(Duration) AS TotalDuration
        FROM @searchlog
        GROUP BY Region
        HAVING SUM(Duration) > 200;

    OUTPUT @res
        too"/output/Searchlog-having.csv"
        ORDER BY TotalDuration DESC
        USING Outputters.Csv();

Para cenários de agregação avançadas, consulte a documentação de referência Olá Olá U-SQL para [agregar, analítico e fazer referência a funções](https://msdn.microsoft.com/en-us/library/azure/mt621335.aspx)

## <a name="next-steps"></a>Próximas etapas
* [Visão geral da Análise do Microsoft Azure Data Lake](data-lake-analytics-overview.md)
* [Desenvolver scripts U-SQL usando as Ferramentas do Data Lake para Visual Studio](data-lake-analytics-data-lake-tools-get-started.md)
