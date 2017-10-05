---
title: Carregar dados do SQL Server no Azure SQL Data Warehouse (bcp) | Microsoft Docs
description: Para um tamanho de dados pequeno, use bcp para exportar dados do SQL Server para arquivos simples e importar os dados diretamente no Azure SQL Data Warehouse.
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
ms.openlocfilehash: dae7b5f7456f4ec0daf60d55f9c38b780896ff83
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="load-data-from-sql-server-into-azure-sql-data-warehouse-flat-files"></a><span data-ttu-id="a362c-103">Carregar dados do SQL Server no Azure SQL Data Warehouse (arquivos simples)</span><span class="sxs-lookup"><span data-stu-id="a362c-103">Load data from SQL Server into Azure SQL Data Warehouse (flat files)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a362c-104">SSIS</span><span class="sxs-lookup"><span data-stu-id="a362c-104">SSIS</span></span>](sql-data-warehouse-load-from-sql-server-with-integration-services.md)
> * [<span data-ttu-id="a362c-105">PolyBase</span><span class="sxs-lookup"><span data-stu-id="a362c-105">PolyBase</span></span>](sql-data-warehouse-load-from-sql-server-with-polybase.md)
> * [<span data-ttu-id="a362c-106">bcp</span><span class="sxs-lookup"><span data-stu-id="a362c-106">bcp</span></span>](sql-data-warehouse-load-from-sql-server-with-bcp.md)
> 
> 

<span data-ttu-id="a362c-107">Para conjuntos de dados pequenos, você pode usar o utilitário de linha de comando bcp para exportar dados do SQL Server e, depois, carregá-los diretamente no Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="a362c-107">For small data sets, you can use the bcp command-line utility to export data from SQL Server and then load it directly to Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="a362c-108">Neste tutorial, você usará o bcp para:</span><span class="sxs-lookup"><span data-stu-id="a362c-108">In this tutorial, you will use bcp to:</span></span>

* <span data-ttu-id="a362c-109">Exportar uma tabela do SQL Server usando o comando bcp out (ou criar um arquivo de exemplo simples)</span><span class="sxs-lookup"><span data-stu-id="a362c-109">Export a table from from SQL Server by using the bcp out command (or create a simple sample file)</span></span>
* <span data-ttu-id="a362c-110">Importar a tabela de um arquivo simples para o SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="a362c-110">Import the table from a flat file to SQL Data Warehouse.</span></span>
* <span data-ttu-id="a362c-111">Crie estatísticas sobre os dados carregados.</span><span class="sxs-lookup"><span data-stu-id="a362c-111">Create statistics on the loaded data.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-data-into-Azure-SQL-Data-Warehouse-with-BCP/player]
> 
> 

## <a name="before-you-begin"></a><span data-ttu-id="a362c-112">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="a362c-112">Before you begin</span></span>
### <a name="prerequisites"></a><span data-ttu-id="a362c-113">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a362c-113">Prerequisites</span></span>
<span data-ttu-id="a362c-114">Para acompanhar este tutorial, você precisará:</span><span class="sxs-lookup"><span data-stu-id="a362c-114">To step through this tutorial, you need:</span></span>

* <span data-ttu-id="a362c-115">Um banco de dados do SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="a362c-115">A SQL Data Warehouse database</span></span>
* <span data-ttu-id="a362c-116">O utilitário de linha de comando bcp instalado</span><span class="sxs-lookup"><span data-stu-id="a362c-116">The bcp command-line utility installed</span></span>
* <span data-ttu-id="a362c-117">O utilitário de linha de comando sqlcmd instalado</span><span class="sxs-lookup"><span data-stu-id="a362c-117">The sqlcmd command-line utility installed</span></span>

<span data-ttu-id="a362c-118">Você pode baixar os utilitários bcp e sqlcmd do [Centro de Download da Microsoft][Microsoft Download Center].</span><span class="sxs-lookup"><span data-stu-id="a362c-118">You can download the bcp and sqlcmd utilities from the [Microsoft Download Center][Microsoft Download Center].</span></span>

### <a name="data-in-ascii-or-utf-16-format"></a><span data-ttu-id="a362c-119">Dados em formato ASCII ou UTF-16</span><span class="sxs-lookup"><span data-stu-id="a362c-119">Data in ASCII or UTF-16 format</span></span>
<span data-ttu-id="a362c-120">Se você estiver experimentando este tutorial com seus próprios dados, eles precisarão usar a codificação ASCII ou UTF-16, já que bcp não oferece suporte a UTF-8.</span><span class="sxs-lookup"><span data-stu-id="a362c-120">If you are trying this tutorial with your own data, your data needs to use the ASCII or UTF-16 encoding since bcp does not support UTF-8.</span></span> 

<span data-ttu-id="a362c-121">O PolyBase oferece suporte a UTF-8, mas ainda não oferece suporte a UTF-16.</span><span class="sxs-lookup"><span data-stu-id="a362c-121">PolyBase supports UTF-8 but doesn't yet support UTF-16.</span></span> <span data-ttu-id="a362c-122">Observe que se você quiser combinar bcp com o PolyBase, será necessário transformar os dados em UTF-8 após a exportação do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a362c-122">Note that if you want to combine bcp with PolyBase you will need to transform the data to UTF-8 after it is exported from SQL Server.</span></span> 

## <a name="1-create-a-destination-table"></a><span data-ttu-id="a362c-123">1. Criar uma tabela de destino</span><span class="sxs-lookup"><span data-stu-id="a362c-123">1. Create a destination table</span></span>
<span data-ttu-id="a362c-124">Defina uma tabela no SQL Data Warehouse que será a tabela de destino para a carga.</span><span class="sxs-lookup"><span data-stu-id="a362c-124">Define a table in SQL Data Warehouse that will be the destination table for the load.</span></span> <span data-ttu-id="a362c-125">As colunas na tabela devem corresponder aos dados em cada linha do arquivo de dados.</span><span class="sxs-lookup"><span data-stu-id="a362c-125">The columns in the table must correspond to the data in each row of your data file.</span></span>

<span data-ttu-id="a362c-126">Para criar uma tabela, abra um prompt de comando e use sqlcmd.exe para executar o comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="a362c-126">To create a table, open a command prompt and use sqlcmd.exe to run the following command:</span></span>

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


## <a name="2-create-a-source-data-file"></a><span data-ttu-id="a362c-127">2. Criar um arquivo de dados de origem</span><span class="sxs-lookup"><span data-stu-id="a362c-127">2. Create a source data file</span></span>
<span data-ttu-id="a362c-128">Abra o Bloco de Notas e copie as seguintes linhas de dados em um novo arquivo de texto. Em seguida, salve esse arquivo em seu diretório temporário local, c:\Temp\DimDate2.txt.</span><span class="sxs-lookup"><span data-stu-id="a362c-128">Open Notepad and copy the following lines of data into a new text file and then save this file to your local temp directory, C:\Temp\DimDate2.txt.</span></span> <span data-ttu-id="a362c-129">Esses dados estão no formato ASCII.</span><span class="sxs-lookup"><span data-stu-id="a362c-129">This data is in ASCII format.</span></span>

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

<span data-ttu-id="a362c-130">(Opcional) Para exportar seus próprios dados de um banco de dados do SQL Server, abra um prompt de comando e execute o comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="a362c-130">(Optional) To export your own data from a SQL Server database, open a command prompt and run the following command.</span></span> <span data-ttu-id="a362c-131">Substitua TableName, ServerName, DatabaseName, Username e Password por suas próprias informações.</span><span class="sxs-lookup"><span data-stu-id="a362c-131">Replace TableName, ServerName, DatabaseName, Username, and Password with your own information.</span></span>

```sql
bcp <TableName> out C:\Temp\DimDate2_export.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <Password> -q -c -t ','
```



## <a name="3-load-the-data"></a><span data-ttu-id="a362c-132">3. Carregar os dados</span><span class="sxs-lookup"><span data-stu-id="a362c-132">3. Load the data</span></span>
<span data-ttu-id="a362c-133">Para carregar os dados, abra um prompt de comando e execute o comando a seguir, substituindo os valores de Nome do Servidor, Nome do Banco de Dados, Nome de Usuário e Senha por suas próprias informações.</span><span class="sxs-lookup"><span data-stu-id="a362c-133">To load the data, open a command prompt and run the following command, replacing the values for Server Name, Database name, Username, and Password with your own information.</span></span>

```sql
bcp DimDate2 in C:\Temp\DimDate2.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <password> -q -c -t  ','
```

<span data-ttu-id="a362c-134">Use este comando para verificar se os dados foram carregados corretamente</span><span class="sxs-lookup"><span data-stu-id="a362c-134">Use this command to verify the data was loaded properly</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

<span data-ttu-id="a362c-135">O resultado deve parecer com o seguinte:</span><span class="sxs-lookup"><span data-stu-id="a362c-135">The results should look like this:</span></span>

| <span data-ttu-id="a362c-136">DateId</span><span class="sxs-lookup"><span data-stu-id="a362c-136">DateId</span></span> | <span data-ttu-id="a362c-137">CalendarQuarter</span><span class="sxs-lookup"><span data-stu-id="a362c-137">CalendarQuarter</span></span> | <span data-ttu-id="a362c-138">FiscalQuarter</span><span class="sxs-lookup"><span data-stu-id="a362c-138">FiscalQuarter</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a362c-139">20150101</span><span class="sxs-lookup"><span data-stu-id="a362c-139">20150101</span></span> |<span data-ttu-id="a362c-140">1</span><span class="sxs-lookup"><span data-stu-id="a362c-140">1</span></span> |<span data-ttu-id="a362c-141">3</span><span class="sxs-lookup"><span data-stu-id="a362c-141">3</span></span> |
| <span data-ttu-id="a362c-142">20150201</span><span class="sxs-lookup"><span data-stu-id="a362c-142">20150201</span></span> |<span data-ttu-id="a362c-143">1</span><span class="sxs-lookup"><span data-stu-id="a362c-143">1</span></span> |<span data-ttu-id="a362c-144">3</span><span class="sxs-lookup"><span data-stu-id="a362c-144">3</span></span> |
| <span data-ttu-id="a362c-145">20150301</span><span class="sxs-lookup"><span data-stu-id="a362c-145">20150301</span></span> |<span data-ttu-id="a362c-146">1</span><span class="sxs-lookup"><span data-stu-id="a362c-146">1</span></span> |<span data-ttu-id="a362c-147">3</span><span class="sxs-lookup"><span data-stu-id="a362c-147">3</span></span> |
| <span data-ttu-id="a362c-148">20150401</span><span class="sxs-lookup"><span data-stu-id="a362c-148">20150401</span></span> |<span data-ttu-id="a362c-149">2</span><span class="sxs-lookup"><span data-stu-id="a362c-149">2</span></span> |<span data-ttu-id="a362c-150">4</span><span class="sxs-lookup"><span data-stu-id="a362c-150">4</span></span> |
| <span data-ttu-id="a362c-151">20150501</span><span class="sxs-lookup"><span data-stu-id="a362c-151">20150501</span></span> |<span data-ttu-id="a362c-152">2</span><span class="sxs-lookup"><span data-stu-id="a362c-152">2</span></span> |<span data-ttu-id="a362c-153">4</span><span class="sxs-lookup"><span data-stu-id="a362c-153">4</span></span> |
| <span data-ttu-id="a362c-154">20150601</span><span class="sxs-lookup"><span data-stu-id="a362c-154">20150601</span></span> |<span data-ttu-id="a362c-155">2</span><span class="sxs-lookup"><span data-stu-id="a362c-155">2</span></span> |<span data-ttu-id="a362c-156">4</span><span class="sxs-lookup"><span data-stu-id="a362c-156">4</span></span> |
| <span data-ttu-id="a362c-157">20150701</span><span class="sxs-lookup"><span data-stu-id="a362c-157">20150701</span></span> |<span data-ttu-id="a362c-158">3</span><span class="sxs-lookup"><span data-stu-id="a362c-158">3</span></span> |<span data-ttu-id="a362c-159">1</span><span class="sxs-lookup"><span data-stu-id="a362c-159">1</span></span> |
| <span data-ttu-id="a362c-160">20150801</span><span class="sxs-lookup"><span data-stu-id="a362c-160">20150801</span></span> |<span data-ttu-id="a362c-161">3</span><span class="sxs-lookup"><span data-stu-id="a362c-161">3</span></span> |<span data-ttu-id="a362c-162">1</span><span class="sxs-lookup"><span data-stu-id="a362c-162">1</span></span> |
| <span data-ttu-id="a362c-163">20150801</span><span class="sxs-lookup"><span data-stu-id="a362c-163">20150801</span></span> |<span data-ttu-id="a362c-164">3</span><span class="sxs-lookup"><span data-stu-id="a362c-164">3</span></span> |<span data-ttu-id="a362c-165">1</span><span class="sxs-lookup"><span data-stu-id="a362c-165">1</span></span> |
| <span data-ttu-id="a362c-166">20151001</span><span class="sxs-lookup"><span data-stu-id="a362c-166">20151001</span></span> |<span data-ttu-id="a362c-167">4</span><span class="sxs-lookup"><span data-stu-id="a362c-167">4</span></span> |<span data-ttu-id="a362c-168">2</span><span class="sxs-lookup"><span data-stu-id="a362c-168">2</span></span> |
| <span data-ttu-id="a362c-169">20151101</span><span class="sxs-lookup"><span data-stu-id="a362c-169">20151101</span></span> |<span data-ttu-id="a362c-170">4</span><span class="sxs-lookup"><span data-stu-id="a362c-170">4</span></span> |<span data-ttu-id="a362c-171">2</span><span class="sxs-lookup"><span data-stu-id="a362c-171">2</span></span> |
| <span data-ttu-id="a362c-172">20151201</span><span class="sxs-lookup"><span data-stu-id="a362c-172">20151201</span></span> |<span data-ttu-id="a362c-173">4</span><span class="sxs-lookup"><span data-stu-id="a362c-173">4</span></span> |<span data-ttu-id="a362c-174">2</span><span class="sxs-lookup"><span data-stu-id="a362c-174">2</span></span> |

## <a name="4-create-statistics"></a><span data-ttu-id="a362c-175">4. Criar estatísticas</span><span class="sxs-lookup"><span data-stu-id="a362c-175">4. Create statistics</span></span>
<span data-ttu-id="a362c-176">O SQL Data Warehouse ainda não dá suporte à criação automática ou atualização automática de estatísticas.</span><span class="sxs-lookup"><span data-stu-id="a362c-176">SQL Data Warehouse does not yet support auto-create or auto-update statistics.</span></span> <span data-ttu-id="a362c-177">Para obter o melhor desempenho de suas consultas, é importante que as estatísticas sejam criadas em todas as colunas de todas as tabelas após o primeiro carregamento, ou após uma alteração significativa nos dados.</span><span class="sxs-lookup"><span data-stu-id="a362c-177">To get the best query performance, it's important to create statistics on all columns of all tables after the first load or after any substantial changes occur in the data.</span></span> <span data-ttu-id="a362c-178">Para obter uma explicação detalhada das estatísticas, confira [Estatísticas][Statistics].</span><span class="sxs-lookup"><span data-stu-id="a362c-178">For a detailed explanation of statistics, see [Statistics][Statistics].</span></span> 

<span data-ttu-id="a362c-179">Execute o seguinte comando para criar estatísticas em sua tabela recém-carregada.</span><span class="sxs-lookup"><span data-stu-id="a362c-179">Run the following command to create statistics on your newly loaded table.</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    create statistics [DateId] on [DimDate2] ([DateId]);
    create statistics [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
    create statistics [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
"
```

## <a name="5-export-data-from-sql-data-warehouse"></a><span data-ttu-id="a362c-180">5. Exportar dados do SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="a362c-180">5. Export data from SQL Data Warehouse</span></span>
<span data-ttu-id="a362c-181">Por diversão, você pode exportar os dados recém-carregados para fora do SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="a362c-181">For fun, you can export the data that you just loaded back out of SQL Data Warehouse.</span></span>  <span data-ttu-id="a362c-182">O comando para exportar é exatamente o mesmo usado para a exportação do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a362c-182">The command to export is exactly the same as exporting from SQL Server.</span></span>

<span data-ttu-id="a362c-183">No entanto, há uma diferença nos resultados.</span><span class="sxs-lookup"><span data-stu-id="a362c-183">However, there is a difference in the results.</span></span> <span data-ttu-id="a362c-184">Como os dados são armazenados em locais distribuídos no SQL Data Warehouse, quando você exporta os dados, cada nó de Computação grava seus dados no arquivo de saída.</span><span class="sxs-lookup"><span data-stu-id="a362c-184">Since the data is stored in distributed locations within SQL Data Warehouse, when you export data each Compute node writes it data to the output file.</span></span> <span data-ttu-id="a362c-185">A ordem dos dados no arquivo de saída provavelmente será diferente da ordem dos dados no arquivo de entrada.</span><span class="sxs-lookup"><span data-stu-id="a362c-185">The order of the data in the output file is likely to be different than the order of the data in the input file.</span></span>

### <a name="export-a-table-and-compare-exported-results"></a><span data-ttu-id="a362c-186">Exportar uma tabela e comparar os resultados exportados</span><span class="sxs-lookup"><span data-stu-id="a362c-186">Export a table and compare exported results</span></span>
<span data-ttu-id="a362c-187">Para ver os dados exportados, abra um prompt de comando e execute este comando usando seus próprios parâmetros.</span><span class="sxs-lookup"><span data-stu-id="a362c-187">To see the exported data, open a command prompt and run this command using your own parameters.</span></span> <span data-ttu-id="a362c-188">ServerName é o nome do SQL Server lógico do Azure.</span><span class="sxs-lookup"><span data-stu-id="a362c-188">ServerName is the name of your Azure logical SQL Server.</span></span>

```sql
bcp DimDate2 out C:\Temp\DimDate2_export.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t ','
```
<span data-ttu-id="a362c-189">Você pode verificar se os dados foram exportados corretamente abrindo o novo arquivo.</span><span class="sxs-lookup"><span data-stu-id="a362c-189">You can verify the data was exported correctly by opening the new file.</span></span> <span data-ttu-id="a362c-190">Os dados no arquivo devem corresponder ao texto abaixo, mas provavelmente serão classificados em uma ordem diferente:</span><span class="sxs-lookup"><span data-stu-id="a362c-190">The data in the file should match the text below, but will likely be sorted in a different order:</span></span>

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

### <a name="export-the-results-of-a-query"></a><span data-ttu-id="a362c-191">Exportar os resultados de uma consulta</span><span class="sxs-lookup"><span data-stu-id="a362c-191">Export the results of a query</span></span>
<span data-ttu-id="a362c-192">Você pode usar a função **queryout** do bcp para exportar os resultados de uma consulta em vez de exportar toda a tabela.</span><span class="sxs-lookup"><span data-stu-id="a362c-192">You can use the **queryout** function of bcp to export the results of a query instead of exporting the entire table.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="a362c-193">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a362c-193">Next steps</span></span>
<span data-ttu-id="a362c-194">Para obter uma visão geral do carregamento, confira [Carregar dados no SQL Data Warehouse][Load data into SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="a362c-194">For an overview of loading, see [Load data into SQL Data Warehouse][Load data into SQL Data Warehouse].</span></span>
<span data-ttu-id="a362c-195">Para obter mais dicas de desenvolvimento, consulte [Visão geral de desenvolvimento do SQL Data Warehouse][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="a362c-195">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>
<span data-ttu-id="a362c-196">Consulte [Visão geral da tabela][Table Overview] ou [Sintaxe CREATE TABLE][CREATE TABLE syntax] para obter mais informações sobre como criar uma tabela no SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="a362c-196">See [Table Overview][Table Overview] or [CREATE TABLE syntax][CREATE TABLE syntax] for more information about creating a table on SQL Data Warehouse.</span></span>

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
