---
title: Carregar dados de exemplo no SQL Data Warehouse | Microsoft Docs
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
ms.openlocfilehash: 1e0df958a2f18fe1e988168918e5cfd293f84e64
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="load-sample-data-into-sql-data-warehouse"></a><span data-ttu-id="1e925-103">Carregar dados de amostra no SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="1e925-103">Load sample data into SQL Data Warehouse</span></span>
<span data-ttu-id="1e925-104">Siga estas etapas simples para carregar e consultar o banco de dados de exemplo da Adventure Works.</span><span class="sxs-lookup"><span data-stu-id="1e925-104">Follow these simple steps to load and query the Adventure Works Sample database.</span></span> <span data-ttu-id="1e925-105">Esses scripts usam sqlcmd para executar SQL, criando tabelas e exibições.</span><span class="sxs-lookup"><span data-stu-id="1e925-105">These scripts first use sqlcmd to run SQL which will create tables and views.</span></span> <span data-ttu-id="1e925-106">Depois que as tabelas tiverem sido criadas, os scripts usarão bcp para carregar os dados.</span><span class="sxs-lookup"><span data-stu-id="1e925-106">Once tables have been created, the scripts will use bcp to load data.</span></span>  <span data-ttu-id="1e925-107">Se ainda não tiver o sqlcmd e o bcp instalados, siga estes links para [instalar o bcp][install bcp] e [instalar o sqlcmd][install sqlcmd].</span><span class="sxs-lookup"><span data-stu-id="1e925-107">If you don't already have sqlcmd and bcp installed, follow these links to [install bcp][install bcp] and to [install sqlcmd][install sqlcmd].</span></span>

## <a name="load-sample-data"></a><span data-ttu-id="1e925-108">Carregar dados de exemplo</span><span class="sxs-lookup"><span data-stu-id="1e925-108">Load sample data</span></span>
1. <span data-ttu-id="1e925-109">Baixe o arquivo zip dos [Scripts de exemplo da Adventure Works para o SQL Data Warehouse][Adventure Works Sample Scripts for SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="1e925-109">Download the [Adventure Works Sample Scripts for SQL Data Warehouse][Adventure Works Sample Scripts for SQL Data Warehouse] zip file.</span></span>
2. <span data-ttu-id="1e925-110">Extraia os arquivos do zip baixado em um diretório no computador local.</span><span class="sxs-lookup"><span data-stu-id="1e925-110">Extract the files from downloaded zip to a directory on your local machine.</span></span>
3. <span data-ttu-id="1e925-111">Edite o arquivo aw_create.bat extraído e defina as seguintes variáveis na parte superior do arquivo.</span><span class="sxs-lookup"><span data-stu-id="1e925-111">Edit the extracted file aw_create.bat and set the following variables found at the top of the file.</span></span>  <span data-ttu-id="1e925-112">Não deixe nenhum espaço em branco entre "=" e o parâmetro.</span><span class="sxs-lookup"><span data-stu-id="1e925-112">Be sure to leave no whitespace between the "=" and the parameter.</span></span>  <span data-ttu-id="1e925-113">A seguir estão exemplos de como poderão ficar suas edições.</span><span class="sxs-lookup"><span data-stu-id="1e925-113">Below are examples of how your edits might look.</span></span>
   
    ```
    server=mylogicalserver.database.windows.net
    user=mydwuser
    password=Mydwpassw0rd
    database=mydwdatabase
    ```
4. <span data-ttu-id="1e925-114">Em um prompt de comando do Windows, execute o aw_create.bat editado.</span><span class="sxs-lookup"><span data-stu-id="1e925-114">From a Windows cmd prompt, run the edited aw_create.bat.</span></span>  <span data-ttu-id="1e925-115">Verifique se você está no diretório onde salvou a versão editada do aw_create.bat.</span><span class="sxs-lookup"><span data-stu-id="1e925-115">Be sure you are in the directory where you saved your edited version of aw_create.bat.</span></span>
   <span data-ttu-id="1e925-116">Este script...</span><span class="sxs-lookup"><span data-stu-id="1e925-116">This script will...</span></span>
   
   * <span data-ttu-id="1e925-117">Descartará todas as tabelas da Adventure Works ou exibições que já existem no banco de dados</span><span class="sxs-lookup"><span data-stu-id="1e925-117">Drop any Adventure Works tables or views that already exist in your database</span></span>
   * <span data-ttu-id="1e925-118">Criará as tabelas e exibições da Adventure Works</span><span class="sxs-lookup"><span data-stu-id="1e925-118">Create the Adventure Works tables and views</span></span>
   * <span data-ttu-id="1e925-119">Carregará cada tabela da Adventure Works usando o bcp</span><span class="sxs-lookup"><span data-stu-id="1e925-119">Load each Adventure Works table using bcp</span></span>
   * <span data-ttu-id="1e925-120">Validará as contagens de linhas para cada tabela da Adventure Works</span><span class="sxs-lookup"><span data-stu-id="1e925-120">Validate the row counts for each Adventure Works table</span></span>
   * <span data-ttu-id="1e925-121">Coletará estatísticas sobre cada coluna para cada tabela da Adventure Works</span><span class="sxs-lookup"><span data-stu-id="1e925-121">Collect statistics on every column for each Adventure Works table</span></span>

## <a name="query-sample-data"></a><span data-ttu-id="1e925-122">Consultar dados de exemplo</span><span class="sxs-lookup"><span data-stu-id="1e925-122">Query sample data</span></span>
<span data-ttu-id="1e925-123">Agora que você carregou alguns dados de exemplo no SQL Data Warehouse, poderá executar rapidamente algumas consultas.</span><span class="sxs-lookup"><span data-stu-id="1e925-123">Once you've loaded some sample data into your SQL Data Warehouse, you can quickly run a few queries.</span></span>  <span data-ttu-id="1e925-124">Para executar uma consulta, conecte-se ao banco de dados da Adventure Works recém-criado no Azure SQL DW usando o Visual Studio e o SSDT, conforme descrito no documento [Consultar com o Visual Studio][query with Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="1e925-124">To run a query, connect to your newly created Adventure Works database in Azure SQL DW using Visual Studio and SSDT, as described in the [query with Visual Studio][query with Visual Studio] document.</span></span>

<span data-ttu-id="1e925-125">Exemplo de instrução select simples para obter todas as informações dos funcionários:</span><span class="sxs-lookup"><span data-stu-id="1e925-125">Example of simple select statement to get all the info of the employees:</span></span>

```sql
SELECT * FROM DimEmployee;
```

<span data-ttu-id="1e925-126">Exemplo de uma consulta mais complexa usando construções, como GROUP BY, para ver a quantidade total de todas as vendas em cada dia:</span><span class="sxs-lookup"><span data-stu-id="1e925-126">Example of a more complex query using constructs such as GROUP BY to look at the total amount for all sales on each day:</span></span>

```sql
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales
FROM FactInternetSales
GROUP BY OrderDateKey
ORDER BY OrderDateKey;
```

<span data-ttu-id="1e925-127">Exemplo de SELECT com uma cláusula WHERE para filtrar os pedidos anteriores a uma determinada data:</span><span class="sxs-lookup"><span data-stu-id="1e925-127">Example of a SELECT with a WHERE clause to filter out orders from before a certain date:</span></span>

```
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales
FROM FactInternetSales
WHERE OrderDateKey > '20020801'
GROUP BY OrderDateKey
ORDER BY OrderDateKey;
```

<span data-ttu-id="1e925-128">O SQL Data Warehouse oferece suporte a quase todas as construções T-SQL para as quais o SQL Server oferece suporte.</span><span class="sxs-lookup"><span data-stu-id="1e925-128">SQL Data Warehouse supports almost all T-SQL constructs which SQL Server supports.</span></span>  <span data-ttu-id="1e925-129">Todas as diferenças estão documentadas em nossa documentação sobre como [migrar o código][migrate code].</span><span class="sxs-lookup"><span data-stu-id="1e925-129">Any differences are documented in our [migrate code][migrate code] documentation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1e925-130">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1e925-130">Next steps</span></span>
<span data-ttu-id="1e925-131">Agora que você teve a oportunidade de experimentar algumas consultas com os dados de exemplo, confira como [desenvolver][develop], [carregar][load] ou [migrar][migrate] para o SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="1e925-131">Now that you've had a chance to try some queries with sample data, check out how to [develop][develop], [load][load], or [migrate][migrate] to SQL Data Warehouse.</span></span>

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
