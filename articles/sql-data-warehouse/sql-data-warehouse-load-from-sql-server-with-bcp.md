---
title: dados de aaaLoad do SQL Server no Azure SQL Data Warehouse (bcp) | Microsoft Docs
description: "Para um tamanho de dados pequeno, usa bcp tooexport dados de arquivos do SQL Server tooflat e importar dados de saudação diretamente no Azure SQL Data Warehouse."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: f87d8d7c-8276-43c5-90e7-d4ccc0e3a224
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: a03b5403d123e8814ae73a7cce8e6851c8b264a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-sql-server-into-azure-sql-data-warehouse-flat-files"></a><span data-ttu-id="39027-103">Carregar dados do SQL Server no Azure SQL Data Warehouse (arquivos simples)</span><span class="sxs-lookup"><span data-stu-id="39027-103">Load data from SQL Server into Azure SQL Data Warehouse (flat files)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="39027-104">SSIS</span><span class="sxs-lookup"><span data-stu-id="39027-104">SSIS</span></span>](sql-data-warehouse-load-from-sql-server-with-integration-services.md)
> * [<span data-ttu-id="39027-105">PolyBase</span><span class="sxs-lookup"><span data-stu-id="39027-105">PolyBase</span></span>](sql-data-warehouse-load-from-sql-server-with-polybase.md)
> * [<span data-ttu-id="39027-106">bcp</span><span class="sxs-lookup"><span data-stu-id="39027-106">bcp</span></span>](sql-data-warehouse-load-from-sql-server-with-bcp.md)
> 
> 

<span data-ttu-id="39027-107">Para pequenos conjuntos de dados, você pode usar Olá de utilitário de linha de comando bcp tooexport a dados do SQL Server e, em seguida, carregá-lo diretamente tooAzure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="39027-107">For small data sets, you can use hello bcp command-line utility tooexport data from SQL Server and then load it directly tooAzure SQL Data Warehouse.</span></span>

<span data-ttu-id="39027-108">Neste tutorial, você usará o bcp para:</span><span class="sxs-lookup"><span data-stu-id="39027-108">In this tutorial, you will use bcp to:</span></span>

* <span data-ttu-id="39027-109">Exporte uma tabela a partir do SQL Server usando o bcp Olá comando (ou crie um arquivo de exemplo simples)</span><span class="sxs-lookup"><span data-stu-id="39027-109">Export a table from from SQL Server by using hello bcp out command (or create a simple sample file)</span></span>
* <span data-ttu-id="39027-110">Importar tabela de saudação do tooSQL arquivo simples do Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="39027-110">Import hello table from a flat file tooSQL Data Warehouse.</span></span>
* <span data-ttu-id="39027-111">Crie estatísticas nos dados carregado de saudação.</span><span class="sxs-lookup"><span data-stu-id="39027-111">Create statistics on hello loaded data.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-data-into-Azure-SQL-Data-Warehouse-with-BCP/player]
> 
> 

## <a name="before-you-begin"></a><span data-ttu-id="39027-112">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="39027-112">Before you begin</span></span>
### <a name="prerequisites"></a><span data-ttu-id="39027-113">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="39027-113">Prerequisites</span></span>
<span data-ttu-id="39027-114">toostep este tutorial, você precisa:</span><span class="sxs-lookup"><span data-stu-id="39027-114">toostep through this tutorial, you need:</span></span>

* <span data-ttu-id="39027-115">Um banco de dados do SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="39027-115">A SQL Data Warehouse database</span></span>
* <span data-ttu-id="39027-116">Utilitário de linha de comando do bcp Olá instalado</span><span class="sxs-lookup"><span data-stu-id="39027-116">hello bcp command-line utility installed</span></span>
* <span data-ttu-id="39027-117">Utilitário de linha de comando do sqlcmd Olá instalado</span><span class="sxs-lookup"><span data-stu-id="39027-117">hello sqlcmd command-line utility installed</span></span>

<span data-ttu-id="39027-118">Você pode baixar os utilitários de bcp e o sqlcmd Olá do hello [Microsoft Download Center][Microsoft Download Center].</span><span class="sxs-lookup"><span data-stu-id="39027-118">You can download hello bcp and sqlcmd utilities from hello [Microsoft Download Center][Microsoft Download Center].</span></span>

### <a name="data-in-ascii-or-utf-16-format"></a><span data-ttu-id="39027-119">Dados em formato ASCII ou UTF-16</span><span class="sxs-lookup"><span data-stu-id="39027-119">Data in ASCII or UTF-16 format</span></span>
<span data-ttu-id="39027-120">Se você estiver tentando neste tutorial com seus próprios dados, os dados precisarem toouse Olá ASCII ou codificação UTF-16 como bcp não oferece suporte a UTF-8.</span><span class="sxs-lookup"><span data-stu-id="39027-120">If you are trying this tutorial with your own data, your data needs toouse hello ASCII or UTF-16 encoding since bcp does not support UTF-8.</span></span> 

<span data-ttu-id="39027-121">O PolyBase oferece suporte a UTF-8, mas ainda não oferece suporte a UTF-16.</span><span class="sxs-lookup"><span data-stu-id="39027-121">PolyBase supports UTF-8 but doesn't yet support UTF-16.</span></span> <span data-ttu-id="39027-122">Observe que se você quiser toocombine bcp com PolyBase você precisará tootransform Olá dados tooUTF-8 depois de ser exportado do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="39027-122">Note that if you want toocombine bcp with PolyBase you will need tootransform hello data tooUTF-8 after it is exported from SQL Server.</span></span> 

## <a name="1-create-a-destination-table"></a><span data-ttu-id="39027-123">1. Criar uma tabela de destino</span><span class="sxs-lookup"><span data-stu-id="39027-123">1. Create a destination table</span></span>
<span data-ttu-id="39027-124">Defina uma tabela no SQL Data Warehouse que será a tabela de destino Olá para carga de saudação.</span><span class="sxs-lookup"><span data-stu-id="39027-124">Define a table in SQL Data Warehouse that will be hello destination table for hello load.</span></span> <span data-ttu-id="39027-125">colunas de saudação na tabela Olá devem corresponder dados toohello em cada linha do arquivo de dados.</span><span class="sxs-lookup"><span data-stu-id="39027-125">hello columns in hello table must correspond toohello data in each row of your data file.</span></span>

<span data-ttu-id="39027-126">toocreate uma tabela, abra um prompt de comando e use o sqlcmd.exe toorun Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="39027-126">toocreate a table, open a command prompt and use sqlcmd.exe toorun hello following command:</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    CREATE TABLE DimDate2
    (
        DateId INT NOT NULL,
        CalendarQuarter TINYINT NOT NULL,
        FiscalQuarter TINYINT NOT NULL
    )
    WITH
    (
        CLUSTERED COLUMNSTORE INDEX,
        DISTRIBUTION = ROUND_ROBIN
    );
"
```


## <a name="2-create-a-source-data-file"></a><span data-ttu-id="39027-127">2. Criar um arquivo de dados de origem</span><span class="sxs-lookup"><span data-stu-id="39027-127">2. Create a source data file</span></span>
<span data-ttu-id="39027-128">Abra o bloco de notas e copie Olá linhas de dados a seguir em um novo arquivo de texto e, em seguida, salvar esse arquivo tooyour local diretório temp, C:\Temp\DimDate2.txt.</span><span class="sxs-lookup"><span data-stu-id="39027-128">Open Notepad and copy hello following lines of data into a new text file and then save this file tooyour local temp directory, C:\Temp\DimDate2.txt.</span></span> <span data-ttu-id="39027-129">Esses dados estão no formato ASCII.</span><span class="sxs-lookup"><span data-stu-id="39027-129">This data is in ASCII format.</span></span>

```
20150301,1,3
20150501,2,4
20151001,4,2
20150201,1,3
20151201,4,2
20150801,3,1
20150601,2,4
20151101,4,2
20150401,2,4
20150701,3,1
20150901,3,1
20150101,1,3
```

<span data-ttu-id="39027-130">(Opcional) tooexport seus próprios dados de um banco de dados do SQL Server, abra um prompt de comando e execute Olá comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="39027-130">(Optional) tooexport your own data from a SQL Server database, open a command prompt and run hello following command.</span></span> <span data-ttu-id="39027-131">Substitua TableName, ServerName, DatabaseName, Username e Password por suas próprias informações.</span><span class="sxs-lookup"><span data-stu-id="39027-131">Replace TableName, ServerName, DatabaseName, Username, and Password with your own information.</span></span>

```sql
bcp <TableName> out C:\Temp\DimDate2_export.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <Password> -q -c -t ','
```



## <a name="3-load-hello-data"></a><span data-ttu-id="39027-132">3. Carregar dados de saudação</span><span class="sxs-lookup"><span data-stu-id="39027-132">3. Load hello data</span></span>
<span data-ttu-id="39027-133">dados de saudação tooload, abra um prompt de comando e execute Olá comando a seguir, substituindo valores de saudação para o nome do servidor, nome do banco de dados, nome de usuário e senha com suas próprias informações.</span><span class="sxs-lookup"><span data-stu-id="39027-133">tooload hello data, open a command prompt and run hello following command, replacing hello values for Server Name, Database name, Username, and Password with your own information.</span></span>

```sql
bcp DimDate2 in C:\Temp\DimDate2.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <password> -q -c -t  ','
```

<span data-ttu-id="39027-134">Use que estes comando tooverify Olá os dados foram carregados corretamente</span><span class="sxs-lookup"><span data-stu-id="39027-134">Use this command tooverify hello data was loaded properly</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

<span data-ttu-id="39027-135">resultados de saudação devem ter esta aparência:</span><span class="sxs-lookup"><span data-stu-id="39027-135">hello results should look like this:</span></span>

| <span data-ttu-id="39027-136">DateId</span><span class="sxs-lookup"><span data-stu-id="39027-136">DateId</span></span> | <span data-ttu-id="39027-137">CalendarQuarter</span><span class="sxs-lookup"><span data-stu-id="39027-137">CalendarQuarter</span></span> | <span data-ttu-id="39027-138">FiscalQuarter</span><span class="sxs-lookup"><span data-stu-id="39027-138">FiscalQuarter</span></span> |
| --- | --- | --- |
| <span data-ttu-id="39027-139">20150101</span><span class="sxs-lookup"><span data-stu-id="39027-139">20150101</span></span> |<span data-ttu-id="39027-140">1</span><span class="sxs-lookup"><span data-stu-id="39027-140">1</span></span> |<span data-ttu-id="39027-141">3</span><span class="sxs-lookup"><span data-stu-id="39027-141">3</span></span> |
| <span data-ttu-id="39027-142">20150201</span><span class="sxs-lookup"><span data-stu-id="39027-142">20150201</span></span> |<span data-ttu-id="39027-143">1</span><span class="sxs-lookup"><span data-stu-id="39027-143">1</span></span> |<span data-ttu-id="39027-144">3</span><span class="sxs-lookup"><span data-stu-id="39027-144">3</span></span> |
| <span data-ttu-id="39027-145">20150301</span><span class="sxs-lookup"><span data-stu-id="39027-145">20150301</span></span> |<span data-ttu-id="39027-146">1</span><span class="sxs-lookup"><span data-stu-id="39027-146">1</span></span> |<span data-ttu-id="39027-147">3</span><span class="sxs-lookup"><span data-stu-id="39027-147">3</span></span> |
| <span data-ttu-id="39027-148">20150401</span><span class="sxs-lookup"><span data-stu-id="39027-148">20150401</span></span> |<span data-ttu-id="39027-149">2</span><span class="sxs-lookup"><span data-stu-id="39027-149">2</span></span> |<span data-ttu-id="39027-150">4</span><span class="sxs-lookup"><span data-stu-id="39027-150">4</span></span> |
| <span data-ttu-id="39027-151">20150501</span><span class="sxs-lookup"><span data-stu-id="39027-151">20150501</span></span> |<span data-ttu-id="39027-152">2</span><span class="sxs-lookup"><span data-stu-id="39027-152">2</span></span> |<span data-ttu-id="39027-153">4</span><span class="sxs-lookup"><span data-stu-id="39027-153">4</span></span> |
| <span data-ttu-id="39027-154">20150601</span><span class="sxs-lookup"><span data-stu-id="39027-154">20150601</span></span> |<span data-ttu-id="39027-155">2</span><span class="sxs-lookup"><span data-stu-id="39027-155">2</span></span> |<span data-ttu-id="39027-156">4</span><span class="sxs-lookup"><span data-stu-id="39027-156">4</span></span> |
| <span data-ttu-id="39027-157">20150701</span><span class="sxs-lookup"><span data-stu-id="39027-157">20150701</span></span> |<span data-ttu-id="39027-158">3</span><span class="sxs-lookup"><span data-stu-id="39027-158">3</span></span> |<span data-ttu-id="39027-159">1</span><span class="sxs-lookup"><span data-stu-id="39027-159">1</span></span> |
| <span data-ttu-id="39027-160">20150801</span><span class="sxs-lookup"><span data-stu-id="39027-160">20150801</span></span> |<span data-ttu-id="39027-161">3</span><span class="sxs-lookup"><span data-stu-id="39027-161">3</span></span> |<span data-ttu-id="39027-162">1</span><span class="sxs-lookup"><span data-stu-id="39027-162">1</span></span> |
| <span data-ttu-id="39027-163">20150801</span><span class="sxs-lookup"><span data-stu-id="39027-163">20150801</span></span> |<span data-ttu-id="39027-164">3</span><span class="sxs-lookup"><span data-stu-id="39027-164">3</span></span> |<span data-ttu-id="39027-165">1</span><span class="sxs-lookup"><span data-stu-id="39027-165">1</span></span> |
| <span data-ttu-id="39027-166">20151001</span><span class="sxs-lookup"><span data-stu-id="39027-166">20151001</span></span> |<span data-ttu-id="39027-167">4</span><span class="sxs-lookup"><span data-stu-id="39027-167">4</span></span> |<span data-ttu-id="39027-168">2</span><span class="sxs-lookup"><span data-stu-id="39027-168">2</span></span> |
| <span data-ttu-id="39027-169">20151101</span><span class="sxs-lookup"><span data-stu-id="39027-169">20151101</span></span> |<span data-ttu-id="39027-170">4</span><span class="sxs-lookup"><span data-stu-id="39027-170">4</span></span> |<span data-ttu-id="39027-171">2</span><span class="sxs-lookup"><span data-stu-id="39027-171">2</span></span> |
| <span data-ttu-id="39027-172">20151201</span><span class="sxs-lookup"><span data-stu-id="39027-172">20151201</span></span> |<span data-ttu-id="39027-173">4</span><span class="sxs-lookup"><span data-stu-id="39027-173">4</span></span> |<span data-ttu-id="39027-174">2</span><span class="sxs-lookup"><span data-stu-id="39027-174">2</span></span> |

## <a name="4-create-statistics"></a><span data-ttu-id="39027-175">4. Criar estatísticas</span><span class="sxs-lookup"><span data-stu-id="39027-175">4. Create statistics</span></span>
<span data-ttu-id="39027-176">O SQL Data Warehouse ainda não dá suporte à criação automática ou atualização automática de estatísticas.</span><span class="sxs-lookup"><span data-stu-id="39027-176">SQL Data Warehouse does not yet support auto-create or auto-update statistics.</span></span> <span data-ttu-id="39027-177">tooget Olá melhor desempenho de consulta, é importante toocreate estatísticas em todas as colunas de todas as tabelas após a primeira carga de saudação ou após a ocorrem de alterações substanciais nos dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="39027-177">tooget hello best query performance, it's important toocreate statistics on all columns of all tables after hello first load or after any substantial changes occur in hello data.</span></span> <span data-ttu-id="39027-178">Para obter uma explicação detalhada das estatísticas, confira [Estatísticas][Statistics].</span><span class="sxs-lookup"><span data-stu-id="39027-178">For a detailed explanation of statistics, see [Statistics][Statistics].</span></span> 

<span data-ttu-id="39027-179">Execute Olá estatísticas de toocreate de comando a seguir em sua tabela recentemente carregada.</span><span class="sxs-lookup"><span data-stu-id="39027-179">Run hello following command toocreate statistics on your newly loaded table.</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    create statistics [DateId] on [DimDate2] ([DateId]);
    create statistics [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
    create statistics [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
"
```

## <a name="5-export-data-from-sql-data-warehouse"></a><span data-ttu-id="39027-180">5. Exportar dados do SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="39027-180">5. Export data from SQL Data Warehouse</span></span>
<span data-ttu-id="39027-181">Para diversão, você pode exportar dados de saudação que carregada fora do SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="39027-181">For fun, you can export hello data that you just loaded back out of SQL Data Warehouse.</span></span>  <span data-ttu-id="39027-182">Olá comando tooexport é exatamente Olá mesmo que a exportação do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="39027-182">hello command tooexport is exactly hello same as exporting from SQL Server.</span></span>

<span data-ttu-id="39027-183">No entanto, há uma diferença nos resultados da saudação.</span><span class="sxs-lookup"><span data-stu-id="39027-183">However, there is a difference in hello results.</span></span> <span data-ttu-id="39027-184">Como dados de saudação são armazenados nos locais distribuídos no SQL Data Warehouse, quando você exportar dados a cada nó de computação grava-arquivo de saída de toohello de dados.</span><span class="sxs-lookup"><span data-stu-id="39027-184">Since hello data is stored in distributed locations within SQL Data Warehouse, when you export data each Compute node writes it data toohello output file.</span></span> <span data-ttu-id="39027-185">ordem de saudação de dados Olá no arquivo de saída de saudação é provavelmente toobe diferente Olá ordem dos dados de saudação no arquivo de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="39027-185">hello order of hello data in hello output file is likely toobe different than hello order of hello data in hello input file.</span></span>

### <a name="export-a-table-and-compare-exported-results"></a><span data-ttu-id="39027-186">Exportar uma tabela e comparar os resultados exportados</span><span class="sxs-lookup"><span data-stu-id="39027-186">Export a table and compare exported results</span></span>
<span data-ttu-id="39027-187">toosee Olá dados exportados, abra um prompt de comando e execute este comando usando seus próprios parâmetros.</span><span class="sxs-lookup"><span data-stu-id="39027-187">toosee hello exported data, open a command prompt and run this command using your own parameters.</span></span> <span data-ttu-id="39027-188">ServerName é o nome de saudação do servidor SQL lógico do Azure.</span><span class="sxs-lookup"><span data-stu-id="39027-188">ServerName is hello name of your Azure logical SQL Server.</span></span>

```sql
bcp DimDate2 out C:\Temp\DimDate2_export.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t ','
```
<span data-ttu-id="39027-189">Você pode verificar Olá dados foram exportados corretamente abrindo novo arquivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="39027-189">You can verify hello data was exported correctly by opening hello new file.</span></span> <span data-ttu-id="39027-190">dados de saudação no arquivo hello devem coincidir com o texto de saudação abaixo, mas provavelmente serão classificados em uma ordem diferente:</span><span class="sxs-lookup"><span data-stu-id="39027-190">hello data in hello file should match hello text below, but will likely be sorted in a different order:</span></span>

```
20150301,1,3
20150501,2,4
20151001,4,2
20150201,1,3
20151201,4,2
20150801,3,1
20150601,2,4
20151101,4,2
20150401,2,4
20150701,3,1
20150901,3,1
20150101,1,3
```

### <a name="export-hello-results-of-a-query"></a><span data-ttu-id="39027-191">Saudação de exportar resultados de uma consulta</span><span class="sxs-lookup"><span data-stu-id="39027-191">Export hello results of a query</span></span>
<span data-ttu-id="39027-192">Você pode usar o hello **queryout** função dos resultados de saudação do bcp tooexport de uma consulta em vez de exportar a tabela inteira hello.</span><span class="sxs-lookup"><span data-stu-id="39027-192">You can use hello **queryout** function of bcp tooexport hello results of a query instead of exporting hello entire table.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="39027-193">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="39027-193">Next steps</span></span>
<span data-ttu-id="39027-194">Para obter uma visão geral do carregamento, confira [Carregar dados no SQL Data Warehouse][Load data into SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="39027-194">For an overview of loading, see [Load data into SQL Data Warehouse][Load data into SQL Data Warehouse].</span></span>
<span data-ttu-id="39027-195">Para obter mais dicas de desenvolvimento, consulte [Visão geral de desenvolvimento do SQL Data Warehouse][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="39027-195">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>
<span data-ttu-id="39027-196">Consulte [Visão geral da tabela][Table Overview] ou [Sintaxe CREATE TABLE][CREATE TABLE syntax] para obter mais informações sobre como criar uma tabela no SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="39027-196">See [Table Overview][Table Overview] or [CREATE TABLE syntax][CREATE TABLE syntax] for more information about creating a table on SQL Data Warehouse.</span></span>

<!--Image references-->

<!--Article references-->

[Load data into SQL Data Warehouse]: ./sql-data-warehouse-overview-load.md
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
[Table Overview]: ./sql-data-warehouse-tables-overview.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md

<!--MSDN references-->
[bcp]: https://msdn.microsoft.com/library/ms162802.aspx
[CREATE TABLE syntax]: https://msdn.microsoft.com/library/mt203953.aspx

<!--Other Web references-->
[Microsoft Download Center]: https://www.microsoft.com/download/details.aspx?id=36433
