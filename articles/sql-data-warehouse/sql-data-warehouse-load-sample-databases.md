---
title: dados de exemplo aaaLoad no SQL Data Warehouse | Microsoft Docs
description: Carregar dados de amostra no SQL Data Warehouse
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: e338ecf8-cfee-419b-b7b6-98108d381c62
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 3459c42f3aae51c27fd35db7874faf99e1e577e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="load-sample-data-into-sql-data-warehouse"></a><span data-ttu-id="45af8-103">Carregar dados de amostra no SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="45af8-103">Load sample data into SQL Data Warehouse</span></span>
<span data-ttu-id="45af8-104">Siga essas tooload etapas simples e consultar banco de dados de exemplo do Adventure Works de saudação.</span><span class="sxs-lookup"><span data-stu-id="45af8-104">Follow these simple steps tooload and query hello Adventure Works Sample database.</span></span> <span data-ttu-id="45af8-105">Esses scripts primeiro usam sqlcmd toorun SQL que criará tabelas e exibições.</span><span class="sxs-lookup"><span data-stu-id="45af8-105">These scripts first use sqlcmd toorun SQL which will create tables and views.</span></span> <span data-ttu-id="45af8-106">Depois que as tabelas foram criadas, scripts Olá usará dados de tooload de bcp.</span><span class="sxs-lookup"><span data-stu-id="45af8-106">Once tables have been created, hello scripts will use bcp tooload data.</span></span>  <span data-ttu-id="45af8-107">Se você ainda não tiver sqlcmd e bcp instalado, siga estes links muito[instalar bcp] [ install bcp] e muito[instalar sqlcmd][install sqlcmd].</span><span class="sxs-lookup"><span data-stu-id="45af8-107">If you don't already have sqlcmd and bcp installed, follow these links too[install bcp][install bcp] and too[install sqlcmd][install sqlcmd].</span></span>

## <a name="load-sample-data"></a><span data-ttu-id="45af8-108">Carregar dados de exemplo</span><span class="sxs-lookup"><span data-stu-id="45af8-108">Load sample data</span></span>
1. <span data-ttu-id="45af8-109">Baixar Olá [Scripts de exemplo Adventure Works para SQL Data Warehouse] [ Adventure Works Sample Scripts for SQL Data Warehouse] arquivo zip.</span><span class="sxs-lookup"><span data-stu-id="45af8-109">Download hello [Adventure Works Sample Scripts for SQL Data Warehouse][Adventure Works Sample Scripts for SQL Data Warehouse] zip file.</span></span>
2. <span data-ttu-id="45af8-110">Extraia os arquivos de saudação do diretório de tooa zip baixado em seu computador local.</span><span class="sxs-lookup"><span data-stu-id="45af8-110">Extract hello files from downloaded zip tooa directory on your local machine.</span></span>
3. <span data-ttu-id="45af8-111">Edite aw_create.bat do arquivo hello extraído e defina Olá encontradas na parte superior de saudação do arquivo hello variáveis a seguir.</span><span class="sxs-lookup"><span data-stu-id="45af8-111">Edit hello extracted file aw_create.bat and set hello following variables found at hello top of hello file.</span></span>  <span data-ttu-id="45af8-112">Não ser tooleave-se de que nenhum espaço em branco entre hello "=" e o parâmetro hello.</span><span class="sxs-lookup"><span data-stu-id="45af8-112">Be sure tooleave no whitespace between hello "=" and hello parameter.</span></span>  <span data-ttu-id="45af8-113">A seguir estão exemplos de como poderão ficar suas edições.</span><span class="sxs-lookup"><span data-stu-id="45af8-113">Below are examples of how your edits might look.</span></span>
   
    ```
    server=mylogicalserver.database.windows.net
    user=mydwuser
    password=Mydwpassw0rd
    database=mydwdatabase
    ```
4. <span data-ttu-id="45af8-114">Em um prompt de comando do Windows, execute aw_create.bat Olá editado.</span><span class="sxs-lookup"><span data-stu-id="45af8-114">From a Windows cmd prompt, run hello edited aw_create.bat.</span></span>  <span data-ttu-id="45af8-115">Certifique-se de que você está no diretório Olá onde você salvou sua versão editada do aw_create.bat.</span><span class="sxs-lookup"><span data-stu-id="45af8-115">Be sure you are in hello directory where you saved your edited version of aw_create.bat.</span></span>
   <span data-ttu-id="45af8-116">Este script...</span><span class="sxs-lookup"><span data-stu-id="45af8-116">This script will...</span></span>
   
   * <span data-ttu-id="45af8-117">Descartará todas as tabelas da Adventure Works ou exibições que já existem no banco de dados</span><span class="sxs-lookup"><span data-stu-id="45af8-117">Drop any Adventure Works tables or views that already exist in your database</span></span>
   * <span data-ttu-id="45af8-118">Criar exibições e tabelas do Adventure Works Olá</span><span class="sxs-lookup"><span data-stu-id="45af8-118">Create hello Adventure Works tables and views</span></span>
   * <span data-ttu-id="45af8-119">Carregará cada tabela da Adventure Works usando o bcp</span><span class="sxs-lookup"><span data-stu-id="45af8-119">Load each Adventure Works table using bcp</span></span>
   * <span data-ttu-id="45af8-120">Validar Olá contagens de linha para cada tabela do Adventure Works</span><span class="sxs-lookup"><span data-stu-id="45af8-120">Validate hello row counts for each Adventure Works table</span></span>
   * <span data-ttu-id="45af8-121">Coletará estatísticas sobre cada coluna para cada tabela da Adventure Works</span><span class="sxs-lookup"><span data-stu-id="45af8-121">Collect statistics on every column for each Adventure Works table</span></span>

## <a name="query-sample-data"></a><span data-ttu-id="45af8-122">Consultar dados de exemplo</span><span class="sxs-lookup"><span data-stu-id="45af8-122">Query sample data</span></span>
<span data-ttu-id="45af8-123">Agora que você carregou alguns dados de exemplo no SQL Data Warehouse, poderá executar rapidamente algumas consultas.</span><span class="sxs-lookup"><span data-stu-id="45af8-123">Once you've loaded some sample data into your SQL Data Warehouse, you can quickly run a few queries.</span></span>  <span data-ttu-id="45af8-124">toorun uma consulta, conecte-se tooyour recém-criado banco de dados Adventure Works no Azure SQL DW usando Visual Studio e SSDT, conforme descrito em Olá [consulta com o Visual Studio] [ query with Visual Studio] documento.</span><span class="sxs-lookup"><span data-stu-id="45af8-124">toorun a query, connect tooyour newly created Adventure Works database in Azure SQL DW using Visual Studio and SSDT, as described in hello [query with Visual Studio][query with Visual Studio] document.</span></span>

<span data-ttu-id="45af8-125">Exemplo de simples select instrução tooget todas as informações de saudação de funcionários hello:</span><span class="sxs-lookup"><span data-stu-id="45af8-125">Example of simple select statement tooget all hello info of hello employees:</span></span>

```sql
SELECT * FROM DimEmployee;
```

<span data-ttu-id="45af8-126">Exemplo de uma consulta mais complexa usando construções, como GROUP BY toolook quantidade total de saudação para todas as vendas em cada dia:</span><span class="sxs-lookup"><span data-stu-id="45af8-126">Example of a more complex query using constructs such as GROUP BY toolook at hello total amount for all sales on each day:</span></span>

```sql
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales
FROM FactInternetSales
GROUP BY OrderDateKey
ORDER BY OrderDateKey;
```

<span data-ttu-id="45af8-127">Exemplo de uma seleção com um toofilter de cláusula WHERE ordens de antes de uma determinada data:</span><span class="sxs-lookup"><span data-stu-id="45af8-127">Example of a SELECT with a WHERE clause toofilter out orders from before a certain date:</span></span>

```
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales
FROM FactInternetSales
WHERE OrderDateKey > '20020801'
GROUP BY OrderDateKey
ORDER BY OrderDateKey;
```

<span data-ttu-id="45af8-128">O SQL Data Warehouse oferece suporte a quase todas as construções T-SQL para as quais o SQL Server oferece suporte.</span><span class="sxs-lookup"><span data-stu-id="45af8-128">SQL Data Warehouse supports almost all T-SQL constructs which SQL Server supports.</span></span>  <span data-ttu-id="45af8-129">Todas as diferenças estão documentadas em nossa documentação sobre como [migrar o código][migrate code].</span><span class="sxs-lookup"><span data-stu-id="45af8-129">Any differences are documented in our [migrate code][migrate code] documentation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="45af8-130">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="45af8-130">Next steps</span></span>
<span data-ttu-id="45af8-131">Agora que você teve uma chance tootry algumas consultas com dados de exemplo, check-out como muito[desenvolver][develop], [carregar][load], ou [ migrar] [ migrate] tooSQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="45af8-131">Now that you've had a chance tootry some queries with sample data, check out how too[develop][develop], [load][load], or [migrate][migrate] tooSQL Data Warehouse.</span></span>

<!--Image references-->

<!--Article references-->
[migrate]: sql-data-warehouse-overview-migrate.md
[develop]: sql-data-warehouse-overview-develop.md
[load]: sql-data-warehouse-overview-load.md
[query with Visual Studio]: sql-data-warehouse-query-visual-studio.md
[migrate code]: sql-data-warehouse-migrate-code.md
[install bcp]: sql-data-warehouse-load-with-bcp.md
[install sqlcmd]: sql-data-warehouse-get-started-connect-sqlcmd.md

<!--Other Web references-->
[Adventure Works Sample Scripts for SQL Data Warehouse]: https://migrhoststorage.blob.core.windows.net/sqldwsample/AdventureWorksSQLDW2012.zip
