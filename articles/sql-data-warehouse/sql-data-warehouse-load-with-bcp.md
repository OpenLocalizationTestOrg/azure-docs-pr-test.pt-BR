---
title: Usar o bcp para carregar dados no SQL Data Warehouse | Microsoft Docs
description: "Saiba o que é o bcp e como usá-lo em cenários de data warehouse."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: f9467d11-fcd6-4131-a65a-2022d2c32d24
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 7596eac10fdf53380d85128265430ce07b551fe3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="load-data-with-bcp"></a><span data-ttu-id="49e28-103">Carregar dados com o bcp</span><span class="sxs-lookup"><span data-stu-id="49e28-103">Load data with bcp</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="49e28-104">Redgate</span><span class="sxs-lookup"><span data-stu-id="49e28-104">Redgate</span></span>](sql-data-warehouse-load-with-redgate.md)  
> * [<span data-ttu-id="49e28-105">Fábrica de dados</span><span class="sxs-lookup"><span data-stu-id="49e28-105">Data Factory</span></span>](sql-data-warehouse-get-started-load-with-azure-data-factory.md)  
> * [<span data-ttu-id="49e28-106">PolyBase</span><span class="sxs-lookup"><span data-stu-id="49e28-106">PolyBase</span></span>](sql-data-warehouse-get-started-load-with-polybase.md)  
> * [<span data-ttu-id="49e28-107">BCP</span><span class="sxs-lookup"><span data-stu-id="49e28-107">BCP</span></span>](sql-data-warehouse-load-with-bcp.md)
> 
> 

<span data-ttu-id="49e28-108">**[bcp][bcp]** é um utilitário de carregamento em massa de linha de comando que permite copiar dados entre o SQL Server, arquivos de dados e o SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="49e28-108">**[bcp][bcp]** is a command-line bulk load utility that allows you to copy data between SQL Server, data files, and SQL Data Warehouse.</span></span> <span data-ttu-id="49e28-109">Use o bcp para importar grandes quantidades de linhas nas tabelas do SQL Data Warehouse ou para exportar dados das tabelas do SQL Server em arquivos de dados.</span><span class="sxs-lookup"><span data-stu-id="49e28-109">Use bcp to import large numbers of rows into SQL Data Warehouse tables or to export data from SQL Server tables into data files.</span></span> <span data-ttu-id="49e28-110">Exceto quando usado com a opção queryout, o bcp não exige conhecimento em Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="49e28-110">Except when used with the queryout option, bcp requires no knowledge of Transact-SQL.</span></span>

<span data-ttu-id="49e28-111">O bcp é uma maneira rápida e fácil de mover conjuntos de dados menores para dentro e fora de um banco de dados do SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="49e28-111">bcp is a quick and easy way to move smaller data sets into and out of a SQL Data Warehouse database.</span></span> <span data-ttu-id="49e28-112">O volume exato de dados que é recomendado para carregamento/extração por meio do bcp dependerá da sua conexão de rede com o datacenter do Azure.</span><span class="sxs-lookup"><span data-stu-id="49e28-112">The exact amount of data that is recommended to load/extract via bcp will depend on you network connection to the Azure data center.</span></span>  <span data-ttu-id="49e28-113">Geralmente, as tabelas de dimensão podem ser carregadas e extraídas prontamente com bcp, no entanto, não recomendamos bcp para carregar ou extrair grandes volumes de dados.</span><span class="sxs-lookup"><span data-stu-id="49e28-113">Generally, dimension tables can be loaded and extracted readily with bcp, however, bcp is not recommended for loading or extracting large volumes of data.</span></span>  <span data-ttu-id="49e28-114">Polybase é a ferramenta recomendada para carregar e extrair grandes volumes de dados, pois aproveita melhor a arquitetura de processamento extremamente paralelo do SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="49e28-114">Polybase is the recommended tool for loading and extracting large volumes of data as it does a better job leveraging the massively parallel processing architecture of SQL Data Warehouse.</span></span>

<span data-ttu-id="49e28-115">Com o bcp, você pode:</span><span class="sxs-lookup"><span data-stu-id="49e28-115">With bcp you can:</span></span>

* <span data-ttu-id="49e28-116">Usar um utilitário de linha de comando simples para carregar dados no SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="49e28-116">Use a simple command-line utility to load data into SQL Data Warehouse.</span></span>
* <span data-ttu-id="49e28-117">Usar um utilitário de linha de comando simples para extrair dados do SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="49e28-117">Use a simple command-line utility to extract data from SQL Data Warehouse.</span></span>

<span data-ttu-id="49e28-118">Este tutorial mostrará como:</span><span class="sxs-lookup"><span data-stu-id="49e28-118">This tutorial will show you how to:</span></span>

* <span data-ttu-id="49e28-119">Importar dados em uma tabela usando o comando bcp in</span><span class="sxs-lookup"><span data-stu-id="49e28-119">Import data into a table using the bcp in command</span></span>
* <span data-ttu-id="49e28-120">Exportar dados de uma tabela usando o comando bcp out</span><span class="sxs-lookup"><span data-stu-id="49e28-120">Export data from a table uisng the bcp out command</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-data-into-Azure-SQL-Data-Warehouse-with-BCP/player]
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="49e28-121">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="49e28-121">Prerequisites</span></span>
<span data-ttu-id="49e28-122">Para acompanhar este tutorial, você precisará:</span><span class="sxs-lookup"><span data-stu-id="49e28-122">To step through this tutorial, you need:</span></span>

* <span data-ttu-id="49e28-123">Um banco de dados do SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="49e28-123">A SQL Data Warehouse database</span></span>
* <span data-ttu-id="49e28-124">O utilitário de linha de comando bcp instalado</span><span class="sxs-lookup"><span data-stu-id="49e28-124">The bcp command line utility installed</span></span>
* <span data-ttu-id="49e28-125">O utilitário de linha de comando SQLCMD instalado</span><span class="sxs-lookup"><span data-stu-id="49e28-125">The SQLCMD command line utility installed</span></span>

> [!NOTE]
> <span data-ttu-id="49e28-126">Você pode baixar os utilitários bcp e sqlcmd do [Centro de Download da Microsoft][Microsoft Download Center].</span><span class="sxs-lookup"><span data-stu-id="49e28-126">You can download the bcp and sqlcmd utilities from the [Microsoft Download Center][Microsoft Download Center].</span></span>
> 
> 

## <a name="import-data-into-sql-data-warehouse"></a><span data-ttu-id="49e28-127">Importar dados no SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="49e28-127">Import data into SQL Data Warehouse</span></span>
<span data-ttu-id="49e28-128">Neste tutorial, você criará uma tabela no SQL Data Warehouse e importará dados na tabela.</span><span class="sxs-lookup"><span data-stu-id="49e28-128">In this tutorial, you will create a table in Azure SQL Data Warehouse and import data into the table.</span></span>

### <a name="step-1-create-a-table-in-azure-sql-data-warehouse"></a><span data-ttu-id="49e28-129">Etapa 1: Criar uma tabela no SQL Data Warehouse do Azure</span><span class="sxs-lookup"><span data-stu-id="49e28-129">Step 1: Create a table in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="49e28-130">Em um prompt de comando, use sqlcmd para executar a consulta a seguir e criar uma tabela em sua instância:</span><span class="sxs-lookup"><span data-stu-id="49e28-130">From a command prompt, use sqlcmd to run the following query to create a table on your instance:</span></span>

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

> [!NOTE]
> <span data-ttu-id="49e28-131">Confira [Visão Geral da Tabela][Table Overview] ou a [sintaxe CREATE TABLE][CREATE TABLE syntax] para obter mais informações sobre como criar uma tabela no SQL Data Warehouse e ver as opções disponíveis na cláusula WITH.</span><span class="sxs-lookup"><span data-stu-id="49e28-131">See [Table Overview][Table Overview] or [CREATE TABLE syntax][CREATE TABLE syntax] for more information about creating a table on SQL Data Warehouse and the  options available in the WITH clause.</span></span>
> 
> 

### <a name="step-2-create-a-source-data-file"></a><span data-ttu-id="49e28-132">Etapa 2: Criar um arquivo de dados de origem</span><span class="sxs-lookup"><span data-stu-id="49e28-132">Step 2: Create a source data file</span></span>
<span data-ttu-id="49e28-133">Abra o Bloco de Notas e copie as seguintes linhas de dados em um novo arquivo de texto. Em seguida, salve esse arquivo em seu diretório temporário local, c:\Temp\DimDate2.txt.</span><span class="sxs-lookup"><span data-stu-id="49e28-133">Open Notepad and copy the following lines of data into a new text file and then save this file to your local temp directory, C:\Temp\DimDate2.txt.</span></span>

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

> [!NOTE]
> <span data-ttu-id="49e28-134">É importante lembrar que o bcp.exe não oferece suporte a codificação do arquivo UTF-8.</span><span class="sxs-lookup"><span data-stu-id="49e28-134">It is important to remember that bcp.exe does not support the UTF-8 file encoding.</span></span> <span data-ttu-id="49e28-135">Use arquivos ASCII ou arquivos codificados em UTF-16 ao usar o bcp.exe.</span><span class="sxs-lookup"><span data-stu-id="49e28-135">Please use ASCII files or UTF-16 encoded files when using bcp.exe.</span></span>
> 
> 

### <a name="step-3-connect-and-import-the-data"></a><span data-ttu-id="49e28-136">Etapa 3: Conectar e importar os dados</span><span class="sxs-lookup"><span data-stu-id="49e28-136">Step 3: Connect and import the data</span></span>
<span data-ttu-id="49e28-137">Usando o bcp, você pode conectar e importar os dados usando o comando a seguir, substituindo os valores conforme apropriado:</span><span class="sxs-lookup"><span data-stu-id="49e28-137">Using bcp, you can connect and import the data using the following command replacing the values as appropriate:</span></span>

```sql
bcp DimDate2 in C:\Temp\DimDate2.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t  ','
```

<span data-ttu-id="49e28-138">Você pode verificar se os dados foram carregados executando a consulta a seguir usando o sqlcmd:</span><span class="sxs-lookup"><span data-stu-id="49e28-138">You can verify the data was loaded by running the following query using sqlcmd:</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

<span data-ttu-id="49e28-139">Isso deve retornar os seguintes resultados:</span><span class="sxs-lookup"><span data-stu-id="49e28-139">This should return the following results:</span></span>

| <span data-ttu-id="49e28-140">DateId</span><span class="sxs-lookup"><span data-stu-id="49e28-140">DateId</span></span> | <span data-ttu-id="49e28-141">CalendarQuarter</span><span class="sxs-lookup"><span data-stu-id="49e28-141">CalendarQuarter</span></span> | <span data-ttu-id="49e28-142">FiscalQuarter</span><span class="sxs-lookup"><span data-stu-id="49e28-142">FiscalQuarter</span></span> |
| --- | --- | --- |
| <span data-ttu-id="49e28-143">20150101</span><span class="sxs-lookup"><span data-stu-id="49e28-143">20150101</span></span> |<span data-ttu-id="49e28-144">1</span><span class="sxs-lookup"><span data-stu-id="49e28-144">1</span></span> |<span data-ttu-id="49e28-145">3</span><span class="sxs-lookup"><span data-stu-id="49e28-145">3</span></span> |
| <span data-ttu-id="49e28-146">20150201</span><span class="sxs-lookup"><span data-stu-id="49e28-146">20150201</span></span> |<span data-ttu-id="49e28-147">1</span><span class="sxs-lookup"><span data-stu-id="49e28-147">1</span></span> |<span data-ttu-id="49e28-148">3</span><span class="sxs-lookup"><span data-stu-id="49e28-148">3</span></span> |
| <span data-ttu-id="49e28-149">20150301</span><span class="sxs-lookup"><span data-stu-id="49e28-149">20150301</span></span> |<span data-ttu-id="49e28-150">1</span><span class="sxs-lookup"><span data-stu-id="49e28-150">1</span></span> |<span data-ttu-id="49e28-151">3</span><span class="sxs-lookup"><span data-stu-id="49e28-151">3</span></span> |
| <span data-ttu-id="49e28-152">20150401</span><span class="sxs-lookup"><span data-stu-id="49e28-152">20150401</span></span> |<span data-ttu-id="49e28-153">2</span><span class="sxs-lookup"><span data-stu-id="49e28-153">2</span></span> |<span data-ttu-id="49e28-154">4</span><span class="sxs-lookup"><span data-stu-id="49e28-154">4</span></span> |
| <span data-ttu-id="49e28-155">20150501</span><span class="sxs-lookup"><span data-stu-id="49e28-155">20150501</span></span> |<span data-ttu-id="49e28-156">2</span><span class="sxs-lookup"><span data-stu-id="49e28-156">2</span></span> |<span data-ttu-id="49e28-157">4</span><span class="sxs-lookup"><span data-stu-id="49e28-157">4</span></span> |
| <span data-ttu-id="49e28-158">20150601</span><span class="sxs-lookup"><span data-stu-id="49e28-158">20150601</span></span> |<span data-ttu-id="49e28-159">2</span><span class="sxs-lookup"><span data-stu-id="49e28-159">2</span></span> |<span data-ttu-id="49e28-160">4</span><span class="sxs-lookup"><span data-stu-id="49e28-160">4</span></span> |
| <span data-ttu-id="49e28-161">20150701</span><span class="sxs-lookup"><span data-stu-id="49e28-161">20150701</span></span> |<span data-ttu-id="49e28-162">3</span><span class="sxs-lookup"><span data-stu-id="49e28-162">3</span></span> |<span data-ttu-id="49e28-163">1</span><span class="sxs-lookup"><span data-stu-id="49e28-163">1</span></span> |
| <span data-ttu-id="49e28-164">20150801</span><span class="sxs-lookup"><span data-stu-id="49e28-164">20150801</span></span> |<span data-ttu-id="49e28-165">3</span><span class="sxs-lookup"><span data-stu-id="49e28-165">3</span></span> |<span data-ttu-id="49e28-166">1</span><span class="sxs-lookup"><span data-stu-id="49e28-166">1</span></span> |
| <span data-ttu-id="49e28-167">20150801</span><span class="sxs-lookup"><span data-stu-id="49e28-167">20150801</span></span> |<span data-ttu-id="49e28-168">3</span><span class="sxs-lookup"><span data-stu-id="49e28-168">3</span></span> |<span data-ttu-id="49e28-169">1</span><span class="sxs-lookup"><span data-stu-id="49e28-169">1</span></span> |
| <span data-ttu-id="49e28-170">20151001</span><span class="sxs-lookup"><span data-stu-id="49e28-170">20151001</span></span> |<span data-ttu-id="49e28-171">4</span><span class="sxs-lookup"><span data-stu-id="49e28-171">4</span></span> |<span data-ttu-id="49e28-172">2</span><span class="sxs-lookup"><span data-stu-id="49e28-172">2</span></span> |
| <span data-ttu-id="49e28-173">20151101</span><span class="sxs-lookup"><span data-stu-id="49e28-173">20151101</span></span> |<span data-ttu-id="49e28-174">4</span><span class="sxs-lookup"><span data-stu-id="49e28-174">4</span></span> |<span data-ttu-id="49e28-175">2</span><span class="sxs-lookup"><span data-stu-id="49e28-175">2</span></span> |
| <span data-ttu-id="49e28-176">20151201</span><span class="sxs-lookup"><span data-stu-id="49e28-176">20151201</span></span> |<span data-ttu-id="49e28-177">4</span><span class="sxs-lookup"><span data-stu-id="49e28-177">4</span></span> |<span data-ttu-id="49e28-178">2</span><span class="sxs-lookup"><span data-stu-id="49e28-178">2</span></span> |

### <a name="step-4-create-statistics-on-your-newly-loaded-data"></a><span data-ttu-id="49e28-179">Etapa 4: criar estatísticas sobre os dados recém-carregados</span><span class="sxs-lookup"><span data-stu-id="49e28-179">Step 4: Create Statistics on your newly loaded data</span></span>
<span data-ttu-id="49e28-180">O SQL Data Warehouse do Azure ainda não dá suporte a estatísticas de criação ou atualização automática.</span><span class="sxs-lookup"><span data-stu-id="49e28-180">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span></span> <span data-ttu-id="49e28-181">Para obter o melhor desempenho de suas consultas, é importante que as estatísticas sejam criadas em todas as colunas de todas as tabelas após o primeiro carregamento ou após uma alteração significativa nos dados.</span><span class="sxs-lookup"><span data-stu-id="49e28-181">In order to get the best performance from your queries, it's important that statistics be created on all columns of all tables after the first load or any substantial changes occur in the data.</span></span> <span data-ttu-id="49e28-182">Para obter uma explicação detalhada das estatísticas, confira o tópico [Estatísticas][Statistics] no grupo de tópicos Desenvolver.</span><span class="sxs-lookup"><span data-stu-id="49e28-182">For a detailed explanation of statistics, see the [Statistics][Statistics] topic in the Develop group of topics.</span></span> <span data-ttu-id="49e28-183">Veja abaixo um exemplo de como criar estatísticas na tabela carregada neste exemplo</span><span class="sxs-lookup"><span data-stu-id="49e28-183">Below is a quick example of how to create statistics on the tabled loaded in this example</span></span>

<span data-ttu-id="49e28-184">Execute as seguintes instruções CREATE STATISTICS em um prompt de sqlcmd:</span><span class="sxs-lookup"><span data-stu-id="49e28-184">Execute the following CREATE STATISTICS statements from a sqlcmd prompt:</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    create statistics [DateId] on [DimDate2] ([DateId]);
    create statistics [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
    create statistics [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
"
```

## <a name="export-data-from-sql-data-warehouse"></a><span data-ttu-id="49e28-185">Exportar dados do SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="49e28-185">Export data from SQL Data Warehouse</span></span>
<span data-ttu-id="49e28-186">Neste tutorial, você criará um arquivo de dados de uma tabela no SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="49e28-186">In this tutorial, you will create a data file from a table in SQL Data Warehouse.</span></span> <span data-ttu-id="49e28-187">Exportaremos os dados que criamos acima para um novo arquivo de dados chamado DimDate2_export.txt.</span><span class="sxs-lookup"><span data-stu-id="49e28-187">We will export the data we created above to a new data file called DimDate2_export.txt.</span></span>

### <a name="step-1-export-the-data"></a><span data-ttu-id="49e28-188">Etapa 1: Exportar os dados</span><span class="sxs-lookup"><span data-stu-id="49e28-188">Step 1: Export the data</span></span>
<span data-ttu-id="49e28-189">Usando o utilitário bcp, você pode conectar e exportar dados usando o comando a seguir, substituindo os valores conforme apropriado:</span><span class="sxs-lookup"><span data-stu-id="49e28-189">Using the bcp utility, you can connect and export data using the following command replacing the values as appropriate:</span></span>

```sql
bcp DimDate2 out C:\Temp\DimDate2_export.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t ','
```
<span data-ttu-id="49e28-190">Você pode verificar se os dados foram exportados corretamente abrindo o novo arquivo.</span><span class="sxs-lookup"><span data-stu-id="49e28-190">You can verify the data was exported correctly by opening the new file.</span></span> <span data-ttu-id="49e28-191">Os dados no arquivo devem corresponder ao texto abaixo:</span><span class="sxs-lookup"><span data-stu-id="49e28-191">The data in the file should match the text below:</span></span>

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

> [!NOTE]
> <span data-ttu-id="49e28-192">Devido à natureza dos sistemas distribuídos, a ordem dos dados pode não ser a mesma entre os bancos de dados do SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="49e28-192">Due to the nature of distributed systems, the data order may not be the same across SQL Data Warehouse databases.</span></span> <span data-ttu-id="49e28-193">Outra opção é usar a função **queryout** do bcp para escrever uma extração de consulta, em vez de exportar a tabela inteira.</span><span class="sxs-lookup"><span data-stu-id="49e28-193">Another option is to use the **queryout** function of bcp to write a query extract rather than export the entire table.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="49e28-194">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="49e28-194">Next steps</span></span>
<span data-ttu-id="49e28-195">Para obter uma visão geral do carregamento, confira [Carregar dados no SQL Data Warehouse][Load data into SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="49e28-195">For an overview of loading, see [Load data into SQL Data Warehouse][Load data into SQL Data Warehouse].</span></span>
<span data-ttu-id="49e28-196">Para obter mais dicas de desenvolvimento, consulte [Visão geral de desenvolvimento do SQL Data Warehouse][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="49e28-196">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

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
