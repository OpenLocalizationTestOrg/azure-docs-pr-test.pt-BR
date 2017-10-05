---
title: "Introdução ao catálogo do U-SQL | Microsoft Docs"
description: "Saiba como usar o catálogo do U-SQL para compartilhar códigos e dados."
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
ms.openlocfilehash: 08364c6c7bea53807844e3b1cc327dc3742e0487
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-u-sql-catalog"></a><span data-ttu-id="9130f-103">Introdução ao Catálogo do U-SQL</span><span class="sxs-lookup"><span data-stu-id="9130f-103">Get started with the U-SQL Catalog</span></span>

## <a name="create-a-tvf"></a><span data-ttu-id="9130f-104">Criar um TVF</span><span class="sxs-lookup"><span data-stu-id="9130f-104">Create a TVF</span></span>

<span data-ttu-id="9130f-105">No script U-SQL anterior, você repetiu o uso de EXTRACT para ler do mesmo arquivo de origem.</span><span class="sxs-lookup"><span data-stu-id="9130f-105">In the previous U-SQL script, you repeated the use of EXTRACT to read from the same source file.</span></span> <span data-ttu-id="9130f-106">Com o TVF (função com valor de tabela) do U-SQL, você pode encapsular os dados para uma futura reutilização.</span><span class="sxs-lookup"><span data-stu-id="9130f-106">With the U-SQL table-valued function (TVF), you can encapsulate the data for future reuse.</span></span>  

<span data-ttu-id="9130f-107">O seguinte script cria um TVF chamado `Searchlog()` no banco de dados e esquema padrão:</span><span class="sxs-lookup"><span data-stu-id="9130f-107">The following script creates a TVF called `Searchlog()` in the default database and schema:</span></span>

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

<span data-ttu-id="9130f-108">O script a seguir mostra como usar o TVF definido no script anterior:</span><span class="sxs-lookup"><span data-stu-id="9130f-108">The following script shows you how to use the TVF that was defined in the previous script:</span></span>

```
@res =
    SELECT
        Region,
        SUM(Duration) AS TotalDuration
    FROM Searchlog() AS S
GROUP BY Region
HAVING SUM(Duration) > 200;

OUTPUT @res
    TO "/output/SerachLog-use-tvf.csv"
    ORDER BY TotalDuration DESC
    USING Outputters.Csv();
```

## <a name="create-views"></a><span data-ttu-id="9130f-109">Criar exibições</span><span class="sxs-lookup"><span data-stu-id="9130f-109">Create views</span></span>

<span data-ttu-id="9130f-110">Se você tiver uma única expressão de consulta, em vez de um TVF, poderá usar uma EXIBIÇÃO U-SQL para encapsular essa expressão.</span><span class="sxs-lookup"><span data-stu-id="9130f-110">If you have a single query expression, instead of a TVF you can use a U-SQL VIEW to encapsulate that expression.</span></span>

<span data-ttu-id="9130f-111">O seguinte script cria uma exibição chamada `SearchlogView` no banco de dados e esquema padrão:</span><span class="sxs-lookup"><span data-stu-id="9130f-111">The following script creates a view called `SearchlogView` in the default database and schema:</span></span>

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

<span data-ttu-id="9130f-112">O script a seguir demonstra o uso da exibição definida:</span><span class="sxs-lookup"><span data-stu-id="9130f-112">The following script demonstrates the use of the defined view:</span></span>

```
@res =
    SELECT
        Region,
        SUM(Duration) AS TotalDuration
    FROM SearchlogView
GROUP BY Region
HAVING SUM(Duration) > 200;

OUTPUT @res
    TO "/output/Searchlog-use-view.csv"
    ORDER BY TotalDuration DESC
    USING Outputters.Csv();
```

## <a name="create-tables"></a><span data-ttu-id="9130f-113">Criar tabelas</span><span class="sxs-lookup"><span data-stu-id="9130f-113">Create tables</span></span>
<span data-ttu-id="9130f-114">Assim como ocorre com tabelas de banco de dados relacional, com o U-SQL você pode criar uma tabela com um esquema predefinido ou criar uma tabela que infere o esquema da consulta que popula a tabela (também conhecido como CREATE TABLE AS SELECT ou CTAS).</span><span class="sxs-lookup"><span data-stu-id="9130f-114">As with relational database tables, with U-SQL you can create a table with a predefined schema or create a table that infers the schema from the query that populates the table (also known as CREATE TABLE AS SELECT or CTAS).</span></span>

<span data-ttu-id="9130f-115">Cria um banco de dados e duas tabelas pelo uso do script a seguir:</span><span class="sxs-lookup"><span data-stu-id="9130f-115">Create a database and two tables by using the following script:</span></span>

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

## <a name="query-tables"></a><span data-ttu-id="9130f-116">Consultar tabelas</span><span class="sxs-lookup"><span data-stu-id="9130f-116">Query tables</span></span>
<span data-ttu-id="9130f-117">Você pode consultar tabelas como aquelas criadas no script anterior, da mesma maneira que consulta os arquivos de dados.</span><span class="sxs-lookup"><span data-stu-id="9130f-117">You can query tables, such as those created in the previous script, in the same way that you query the data files.</span></span> <span data-ttu-id="9130f-118">Em vez de criar um conjunto de linhas usando EXTRACT, agora você pode simplesmente consultar o nome da tabela.</span><span class="sxs-lookup"><span data-stu-id="9130f-118">Instead of creating a rowset by using EXTRACT, you now can refer to the table name.</span></span>

<span data-ttu-id="9130f-119">Para ler das tabelas, modifique o script de transformação que você usou anteriormente:</span><span class="sxs-lookup"><span data-stu-id="9130f-119">To read from the tables, modify the transform script that you used previously:</span></span>

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
    TO "/output/Searchlog-query-table.csv"
    ORDER BY TotalDuration DESC
    USING Outputters.Csv();
```

 >[!NOTE]
 ><span data-ttu-id="9130f-120">Atualmente você não pode executar SELECT em uma tabela no mesmo script em que você criou tal tabela.</span><span class="sxs-lookup"><span data-stu-id="9130f-120">Currently, you cannot run a SELECT on a table in the same script as the one where you created the table.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9130f-121">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9130f-121">Next Steps</span></span>
* [<span data-ttu-id="9130f-122">Visão geral da Análise do Microsoft Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="9130f-122">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="9130f-123">Desenvolver scripts U-SQL usando as Ferramentas do Data Lake para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9130f-123">Develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
* [<span data-ttu-id="9130f-124">Monitorar e solucionar problemas em trabalhos do Azure Data Lake Analytics usando o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="9130f-124">Monitor and troubleshoot Azure Data Lake Analytics jobs using Azure portal</span></span>](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)
