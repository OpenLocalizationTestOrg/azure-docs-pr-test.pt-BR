---
title: "Introdução ao catálogo de saudação U-SQL | Microsoft Docs"
description: "Saiba como Olá toouse U-SQL do catálogo de dados e código tooshare."
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
ms.date: 05/09/2017
ms.author: edmaca
ms.openlocfilehash: 559bb7a3879031eb290a3e82946d7bf42ac9f553
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-u-sql-catalog"></a><span data-ttu-id="1f34e-103">Introdução ao Olá catálogo U-SQL</span><span class="sxs-lookup"><span data-stu-id="1f34e-103">Get started with hello U-SQL Catalog</span></span>

## <a name="create-a-tvf"></a><span data-ttu-id="1f34e-104">Criar um TVF</span><span class="sxs-lookup"><span data-stu-id="1f34e-104">Create a TVF</span></span>

<span data-ttu-id="1f34e-105">No script U-SQL de anterior hello, você repetida uso Olá tooread de EXTRAÇÃO de saudação mesmo arquivo de origem.</span><span class="sxs-lookup"><span data-stu-id="1f34e-105">In hello previous U-SQL script, you repeated hello use of EXTRACT tooread from hello same source file.</span></span> <span data-ttu-id="1f34e-106">Com hello U-SQL com valor de tabela TVF (função), você pode encapsular dados Olá para reutilização futura.</span><span class="sxs-lookup"><span data-stu-id="1f34e-106">With hello U-SQL table-valued function (TVF), you can encapsulate hello data for future reuse.</span></span>  

<span data-ttu-id="1f34e-107">Olá, script a seguir cria uma TVF chamada `Searchlog()` no banco de dados de padrão de saudação e esquema:</span><span class="sxs-lookup"><span data-stu-id="1f34e-107">hello following script creates a TVF called `Searchlog()` in hello default database and schema:</span></span>

```
DROP FUNCTION IF EXISTS Searchlog;

CREATE FUNCTION Searchlog()
RETURNS @searchlog TABLE
(
            UserId          int,
            Start           DateTime,
            Region          string,
            Query           string,
            Duration        int?,
            Urls            string,
            ClickedUrls     string
)
AS BEGIN
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
RETURN;
END;
```

<span data-ttu-id="1f34e-108">saudação de script a seguir mostra como toouse Olá TVF que foi definido no script anterior hello:</span><span class="sxs-lookup"><span data-stu-id="1f34e-108">hello following script shows you how toouse hello TVF that was defined in hello previous script:</span></span>

```
@res =
    SELECT
        Region,
        SUM(Duration) AS TotalDuration
    FROM Searchlog() AS S
GROUP BY Region
HAVING SUM(Duration) > 200;

OUTPUT @res
    too"/output/SerachLog-use-tvf.csv"
    ORDER BY TotalDuration DESC
    USING Outputters.Csv();
```

## <a name="create-views"></a><span data-ttu-id="1f34e-109">Criar exibições</span><span class="sxs-lookup"><span data-stu-id="1f34e-109">Create views</span></span>

<span data-ttu-id="1f34e-110">Se você tiver uma expressão de consulta única, em vez de uma TVF você pode usar um modo SQL U tooencapsulate dessa expressão.</span><span class="sxs-lookup"><span data-stu-id="1f34e-110">If you have a single query expression, instead of a TVF you can use a U-SQL VIEW tooencapsulate that expression.</span></span>

<span data-ttu-id="1f34e-111">Olá, script a seguir cria uma exibição chamada `SearchlogView` no banco de dados de padrão de saudação e esquema:</span><span class="sxs-lookup"><span data-stu-id="1f34e-111">hello following script creates a view called `SearchlogView` in hello default database and schema:</span></span>

```
DROP VIEW IF EXISTS SearchlogView;

CREATE VIEW SearchlogView AS  
    EXTRACT UserId          int,
            Start           DateTime,
            Region          string,
            Query           string,
            Duration        int?,
            Urls            string,
            ClickedUrls     string
    FROM "/Samples/Data/SearchLog.tsv"
USING Extractors.Tsv();
```

<span data-ttu-id="1f34e-112">Olá script a seguir demonstra o uso de saudação do modo de exibição de saudação definido:</span><span class="sxs-lookup"><span data-stu-id="1f34e-112">hello following script demonstrates hello use of hello defined view:</span></span>

```
@res =
    SELECT
        Region,
        SUM(Duration) AS TotalDuration
    FROM SearchlogView
GROUP BY Region
HAVING SUM(Duration) > 200;

OUTPUT @res
    too"/output/Searchlog-use-view.csv"
    ORDER BY TotalDuration DESC
    USING Outputters.Csv();
```

## <a name="create-tables"></a><span data-ttu-id="1f34e-113">Criar tabelas</span><span class="sxs-lookup"><span data-stu-id="1f34e-113">Create tables</span></span>
<span data-ttu-id="1f34e-114">Como com as tabelas de banco de dados relacional, com U-SQL você pode criar uma tabela com um esquema predefinido ou criar uma tabela que infere o esquema de saudação da consulta de saudação que preenche a tabela de saudação (também conhecido como CREATE TABLE AS SELECT ou CTAS).</span><span class="sxs-lookup"><span data-stu-id="1f34e-114">As with relational database tables, with U-SQL you can create a table with a predefined schema or create a table that infers hello schema from hello query that populates hello table (also known as CREATE TABLE AS SELECT or CTAS).</span></span>

<span data-ttu-id="1f34e-115">Crie um banco de dados e duas tabelas usando Olá script a seguir:</span><span class="sxs-lookup"><span data-stu-id="1f34e-115">Create a database and two tables by using hello following script:</span></span>

```
DROP DATABASE IF EXISTS SearchLogDb;
CREATE DATABASE SearchLogDb;
USE DATABASE SearchLogDb;

DROP TABLE IF EXISTS SearchLog1;
DROP TABLE IF EXISTS SearchLog2;

CREATE TABLE SearchLog1 (
            UserId          int,
            Start           DateTime,
            Region          string,
            Query           string,
            Duration        int?,
            Urls            string,
            ClickedUrls     string,

            INDEX sl_idx CLUSTERED (UserId ASC)
                DISTRIBUTED BY HASH (UserId)
);

INSERT INTO SearchLog1 SELECT * FROM master.dbo.Searchlog() AS s;

CREATE TABLE SearchLog2(
    INDEX sl_idx CLUSTERED (UserId ASC)
            DISTRIBUTED BY HASH (UserId)
) AS SELECT * FROM master.dbo.Searchlog() AS S; // You can use EXTRACT or SELECT here
```

## <a name="query-tables"></a><span data-ttu-id="1f34e-116">Consultar tabelas</span><span class="sxs-lookup"><span data-stu-id="1f34e-116">Query tables</span></span>
<span data-ttu-id="1f34e-117">Você pode consultar tabelas, como aqueles criados no script anterior hello, em Olá mesma maneira que você consultar arquivos de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="1f34e-117">You can query tables, such as those created in hello previous script, in hello same way that you query hello data files.</span></span> <span data-ttu-id="1f34e-118">Em vez de criar um conjunto de linhas por meio da EXTRAÇÃO, você agora pode consultar toohello nome da tabela.</span><span class="sxs-lookup"><span data-stu-id="1f34e-118">Instead of creating a rowset by using EXTRACT, you now can refer toohello table name.</span></span>

<span data-ttu-id="1f34e-119">tooread de tabelas hello, modifique o script de transformação de saudação que você usou anteriormente:</span><span class="sxs-lookup"><span data-stu-id="1f34e-119">tooread from hello tables, modify hello transform script that you used previously:</span></span>

```
@rs1 =
    SELECT
        Region,
        SUM(Duration) AS TotalDuration
    FROM SearchLogDb.dbo.SearchLog2
GROUP BY Region;

@res =
    SELECT *
    FROM @rs1
    ORDER BY TotalDuration DESC
    FETCH 5 ROWS;

OUTPUT @res
    too"/output/Searchlog-query-table.csv"
    ORDER BY TotalDuration DESC
    USING Outputters.Csv();
```

 >[!NOTE]
 ><span data-ttu-id="1f34e-120">No momento, você não pode executar uma seleção em uma tabela em Olá mesmo script conforme Olá um em que você criou a tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="1f34e-120">Currently, you cannot run a SELECT on a table in hello same script as hello one where you created hello table.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1f34e-121">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1f34e-121">Next Steps</span></span>
* [<span data-ttu-id="1f34e-122">Visão geral da Análise do Microsoft Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="1f34e-122">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="1f34e-123">Desenvolver scripts U-SQL usando as Ferramentas do Data Lake para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1f34e-123">Develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
* [<span data-ttu-id="1f34e-124">Monitorar e solucionar problemas em trabalhos do Azure Data Lake Analytics usando o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="1f34e-124">Monitor and troubleshoot Azure Data Lake Analytics jobs using Azure portal</span></span>](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)
