---
title: Carregar dados do SQL Server no Azure SQL Data Warehouse (PolyBase) | Microsoft Docs
description: Usa o bcp para exportar dados do SQL Server para arquivos simples, o AZCopy para importar dados no Armazenamento de Blobs do Azure e o PolyBase para incluir os dados no Azure SQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: 4d42786a-fb28-43c9-9c3b-72d19c0ecc11
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 08f94bc26d8b1e1f5a56dfccd41e394dbd721024
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="load-data-from-sql-server-into-azure-sql-data-warehouse-azcopy"></a><span data-ttu-id="571ca-103">Carregar dados do SQL Server no Azure SQL Data Warehouse (AZCopy)</span><span class="sxs-lookup"><span data-stu-id="571ca-103">Load data from SQL Server into Azure SQL Data Warehouse (AZCopy)</span></span>
<span data-ttu-id="571ca-104">Use os utilitários de linha de comando bcp e AZCopy para carregar dados do SQL Server no Armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="571ca-104">Use bcp and AZCopy command-line utilities to load data from SQL Server to Azure blob storage.</span></span> <span data-ttu-id="571ca-105">Depois, use o PolyBase ou o Azure Data Factory para carregar os dados Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="571ca-105">Then use PolyBase or Azure Data Factory to load the data into Azure SQL Data Warehouse.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="571ca-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="571ca-106">Prerequisites</span></span>
<span data-ttu-id="571ca-107">Para acompanhar este tutorial, você precisará:</span><span class="sxs-lookup"><span data-stu-id="571ca-107">To step through this tutorial, you need:</span></span>

* <span data-ttu-id="571ca-108">Um banco de dados do SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="571ca-108">A SQL Data Warehouse database</span></span>
* <span data-ttu-id="571ca-109">O utilitário de linha de comando bcp instalado</span><span class="sxs-lookup"><span data-stu-id="571ca-109">The bcp command line utility installed</span></span>
* <span data-ttu-id="571ca-110">O utilitário de linha de comando SQLCMD instalado</span><span class="sxs-lookup"><span data-stu-id="571ca-110">The SQLCMD command line utility installed</span></span>

> [!NOTE]
> <span data-ttu-id="571ca-111">Você pode baixar os utilitários bcp e sqlcmd do [Centro de Download da Microsoft][Microsoft Download Center].</span><span class="sxs-lookup"><span data-stu-id="571ca-111">You can download the bcp and sqlcmd utilities from the [Microsoft Download Center][Microsoft Download Center].</span></span>
> 
> 

## <a name="import-data-into-sql-data-warehouse"></a><span data-ttu-id="571ca-112">Importar dados no SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="571ca-112">Import data into SQL Data Warehouse</span></span>
<span data-ttu-id="571ca-113">Neste tutorial, você criará uma tabela no SQL Data Warehouse e importará dados na tabela.</span><span class="sxs-lookup"><span data-stu-id="571ca-113">In this tutorial, you will create a table in Azure SQL Data Warehouse and import data into the table.</span></span>

### <a name="step-1-create-a-table-in-azure-sql-data-warehouse"></a><span data-ttu-id="571ca-114">Etapa 1: Criar uma tabela no SQL Data Warehouse do Azure</span><span class="sxs-lookup"><span data-stu-id="571ca-114">Step 1: Create a table in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="571ca-115">Em um prompt de comando, use sqlcmd para executar a consulta a seguir e criar uma tabela em sua instância:</span><span class="sxs-lookup"><span data-stu-id="571ca-115">From a command prompt, use sqlcmd to run the following query to create a table on your instance:</span></span>

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
> <span data-ttu-id="571ca-116">Confira [Visão Geral da Tabela][Table Overview] ou a [sintaxe CREATE TABLE][CREATE TABLE syntax] para obter mais informações sobre como criar uma tabela no SQL Data Warehouse e ver as opções disponíveis na cláusula WITH.</span><span class="sxs-lookup"><span data-stu-id="571ca-116">See [Table Overview][Table Overview] or [CREATE TABLE syntax][CREATE TABLE syntax] for more information about creating a table on SQL Data Warehouse and the  options available in the WITH clause.</span></span>
> 
> 

### <a name="step-2-create-a-source-data-file"></a><span data-ttu-id="571ca-117">Etapa 2: Criar um arquivo de dados de origem</span><span class="sxs-lookup"><span data-stu-id="571ca-117">Step 2: Create a source data file</span></span>
<span data-ttu-id="571ca-118">Abra o Bloco de Notas e copie as seguintes linhas de dados em um novo arquivo de texto. Em seguida, salve esse arquivo em seu diretório temporário local, c:\Temp\DimDate2.txt.</span><span class="sxs-lookup"><span data-stu-id="571ca-118">Open Notepad and copy the following lines of data into a new text file and then save this file to your local temp directory, C:\Temp\DimDate2.txt.</span></span>

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
> <span data-ttu-id="571ca-119">É importante lembrar que o bcp.exe não oferece suporte a codificação do arquivo UTF-8.</span><span class="sxs-lookup"><span data-stu-id="571ca-119">It is important to remember that bcp.exe does not support the UTF-8 file encoding.</span></span> <span data-ttu-id="571ca-120">Use arquivos ASCII ou arquivos codificados em UTF-16 ao usar o bcp.exe.</span><span class="sxs-lookup"><span data-stu-id="571ca-120">Please use ASCII files or UTF-16 encoded files when using bcp.exe.</span></span>
> 
> 

### <a name="step-3-connect-and-import-the-data"></a><span data-ttu-id="571ca-121">Etapa 3: Conectar e importar os dados</span><span class="sxs-lookup"><span data-stu-id="571ca-121">Step 3: Connect and import the data</span></span>
<span data-ttu-id="571ca-122">Usando o bcp, você pode conectar e importar os dados usando o comando a seguir, substituindo os valores conforme apropriado:</span><span class="sxs-lookup"><span data-stu-id="571ca-122">Using bcp, you can connect and import the data using the following command replacing the values as appropriate:</span></span>

```sql
bcp DimDate2 in C:\Temp\DimDate2.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t  ','
```

<span data-ttu-id="571ca-123">Você pode verificar se os dados foram carregados executando a consulta a seguir usando o sqlcmd:</span><span class="sxs-lookup"><span data-stu-id="571ca-123">You can verify the data was loaded by running the following query using sqlcmd:</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

<span data-ttu-id="571ca-124">Isso deve retornar os seguintes resultados:</span><span class="sxs-lookup"><span data-stu-id="571ca-124">This should return the following results:</span></span>

| <span data-ttu-id="571ca-125">DateId</span><span class="sxs-lookup"><span data-stu-id="571ca-125">DateId</span></span> | <span data-ttu-id="571ca-126">CalendarQuarter</span><span class="sxs-lookup"><span data-stu-id="571ca-126">CalendarQuarter</span></span> | <span data-ttu-id="571ca-127">FiscalQuarter</span><span class="sxs-lookup"><span data-stu-id="571ca-127">FiscalQuarter</span></span> |
| --- | --- | --- |
| <span data-ttu-id="571ca-128">20150101</span><span class="sxs-lookup"><span data-stu-id="571ca-128">20150101</span></span> |<span data-ttu-id="571ca-129">1</span><span class="sxs-lookup"><span data-stu-id="571ca-129">1</span></span> |<span data-ttu-id="571ca-130">3</span><span class="sxs-lookup"><span data-stu-id="571ca-130">3</span></span> |
| <span data-ttu-id="571ca-131">20150201</span><span class="sxs-lookup"><span data-stu-id="571ca-131">20150201</span></span> |<span data-ttu-id="571ca-132">1</span><span class="sxs-lookup"><span data-stu-id="571ca-132">1</span></span> |<span data-ttu-id="571ca-133">3</span><span class="sxs-lookup"><span data-stu-id="571ca-133">3</span></span> |
| <span data-ttu-id="571ca-134">20150301</span><span class="sxs-lookup"><span data-stu-id="571ca-134">20150301</span></span> |<span data-ttu-id="571ca-135">1</span><span class="sxs-lookup"><span data-stu-id="571ca-135">1</span></span> |<span data-ttu-id="571ca-136">3</span><span class="sxs-lookup"><span data-stu-id="571ca-136">3</span></span> |
| <span data-ttu-id="571ca-137">20150401</span><span class="sxs-lookup"><span data-stu-id="571ca-137">20150401</span></span> |<span data-ttu-id="571ca-138">2</span><span class="sxs-lookup"><span data-stu-id="571ca-138">2</span></span> |<span data-ttu-id="571ca-139">4</span><span class="sxs-lookup"><span data-stu-id="571ca-139">4</span></span> |
| <span data-ttu-id="571ca-140">20150501</span><span class="sxs-lookup"><span data-stu-id="571ca-140">20150501</span></span> |<span data-ttu-id="571ca-141">2</span><span class="sxs-lookup"><span data-stu-id="571ca-141">2</span></span> |<span data-ttu-id="571ca-142">4</span><span class="sxs-lookup"><span data-stu-id="571ca-142">4</span></span> |
| <span data-ttu-id="571ca-143">20150601</span><span class="sxs-lookup"><span data-stu-id="571ca-143">20150601</span></span> |<span data-ttu-id="571ca-144">2</span><span class="sxs-lookup"><span data-stu-id="571ca-144">2</span></span> |<span data-ttu-id="571ca-145">4</span><span class="sxs-lookup"><span data-stu-id="571ca-145">4</span></span> |
| <span data-ttu-id="571ca-146">20150701</span><span class="sxs-lookup"><span data-stu-id="571ca-146">20150701</span></span> |<span data-ttu-id="571ca-147">3</span><span class="sxs-lookup"><span data-stu-id="571ca-147">3</span></span> |<span data-ttu-id="571ca-148">1</span><span class="sxs-lookup"><span data-stu-id="571ca-148">1</span></span> |
| <span data-ttu-id="571ca-149">20150801</span><span class="sxs-lookup"><span data-stu-id="571ca-149">20150801</span></span> |<span data-ttu-id="571ca-150">3</span><span class="sxs-lookup"><span data-stu-id="571ca-150">3</span></span> |<span data-ttu-id="571ca-151">1</span><span class="sxs-lookup"><span data-stu-id="571ca-151">1</span></span> |
| <span data-ttu-id="571ca-152">20150801</span><span class="sxs-lookup"><span data-stu-id="571ca-152">20150801</span></span> |<span data-ttu-id="571ca-153">3</span><span class="sxs-lookup"><span data-stu-id="571ca-153">3</span></span> |<span data-ttu-id="571ca-154">1</span><span class="sxs-lookup"><span data-stu-id="571ca-154">1</span></span> |
| <span data-ttu-id="571ca-155">20151001</span><span class="sxs-lookup"><span data-stu-id="571ca-155">20151001</span></span> |<span data-ttu-id="571ca-156">4</span><span class="sxs-lookup"><span data-stu-id="571ca-156">4</span></span> |<span data-ttu-id="571ca-157">2</span><span class="sxs-lookup"><span data-stu-id="571ca-157">2</span></span> |
| <span data-ttu-id="571ca-158">20151101</span><span class="sxs-lookup"><span data-stu-id="571ca-158">20151101</span></span> |<span data-ttu-id="571ca-159">4</span><span class="sxs-lookup"><span data-stu-id="571ca-159">4</span></span> |<span data-ttu-id="571ca-160">2</span><span class="sxs-lookup"><span data-stu-id="571ca-160">2</span></span> |
| <span data-ttu-id="571ca-161">20151201</span><span class="sxs-lookup"><span data-stu-id="571ca-161">20151201</span></span> |<span data-ttu-id="571ca-162">4</span><span class="sxs-lookup"><span data-stu-id="571ca-162">4</span></span> |<span data-ttu-id="571ca-163">2</span><span class="sxs-lookup"><span data-stu-id="571ca-163">2</span></span> |

### <a name="step-4-create-statistics-on-your-newly-loaded-data"></a><span data-ttu-id="571ca-164">Etapa 4: criar estatísticas sobre os dados recém-carregados</span><span class="sxs-lookup"><span data-stu-id="571ca-164">Step 4: Create Statistics on your newly loaded data</span></span>
<span data-ttu-id="571ca-165">O SQL Data Warehouse do Azure ainda não dá suporte a estatísticas de criação ou atualização automática.</span><span class="sxs-lookup"><span data-stu-id="571ca-165">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span></span> <span data-ttu-id="571ca-166">Para obter o melhor desempenho de suas consultas, é importante que as estatísticas sejam criadas em todas as colunas de todas as tabelas após o primeiro carregamento ou após uma alteração significativa nos dados.</span><span class="sxs-lookup"><span data-stu-id="571ca-166">In order to get the best performance from your queries, it's important that statistics be created on all columns of all tables after the first load or any substantial changes occur in the data.</span></span> <span data-ttu-id="571ca-167">Para obter uma explicação detalhada das estatísticas, confira o tópico [Estatísticas][Statistics] no grupo de tópicos Desenvolver.</span><span class="sxs-lookup"><span data-stu-id="571ca-167">For a detailed explanation of statistics, see the [Statistics][Statistics] topic in the Develop group of topics.</span></span> <span data-ttu-id="571ca-168">Veja abaixo um exemplo de como criar estatísticas na tabela carregada neste exemplo</span><span class="sxs-lookup"><span data-stu-id="571ca-168">Below is a quick example of how to create statistics on the tabled loaded in this example</span></span>

<span data-ttu-id="571ca-169">Execute as seguintes instruções CREATE STATISTICS em um prompt de sqlcmd:</span><span class="sxs-lookup"><span data-stu-id="571ca-169">Execute the following CREATE STATISTICS statements from a sqlcmd prompt:</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    create statistics [DateId] on [DimDate2] ([DateId]);
    create statistics [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
    create statistics [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
"
```

## <a name="export-data-from-sql-data-warehouse"></a><span data-ttu-id="571ca-170">Exportar dados do SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="571ca-170">Export data from SQL Data Warehouse</span></span>
<span data-ttu-id="571ca-171">Neste tutorial, você criará um arquivo de dados de uma tabela no SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="571ca-171">In this tutorial, you will create a data file from a table in SQL Data Warehouse.</span></span> <span data-ttu-id="571ca-172">Exportaremos os dados que criamos acima para um novo arquivo de dados chamado DimDate2_export.txt.</span><span class="sxs-lookup"><span data-stu-id="571ca-172">We will export the data we created above to a new data file called DimDate2_export.txt.</span></span>

### <a name="step-1-export-the-data"></a><span data-ttu-id="571ca-173">Etapa 1: Exportar os dados</span><span class="sxs-lookup"><span data-stu-id="571ca-173">Step 1: Export the data</span></span>
<span data-ttu-id="571ca-174">Usando o utilitário bcp, você pode conectar e exportar dados usando o comando a seguir, substituindo os valores conforme apropriado:</span><span class="sxs-lookup"><span data-stu-id="571ca-174">Using the bcp utility, you can connect and export data using the following command replacing the values as appropriate:</span></span>

```sql
bcp DimDate2 out C:\Temp\DimDate2_export.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t ','
```
<span data-ttu-id="571ca-175">Você pode verificar se os dados foram exportados corretamente abrindo o novo arquivo.</span><span class="sxs-lookup"><span data-stu-id="571ca-175">You can verify the data was exported correctly by opening the new file.</span></span> <span data-ttu-id="571ca-176">Os dados no arquivo devem corresponder ao texto abaixo:</span><span class="sxs-lookup"><span data-stu-id="571ca-176">The data in the file should match the text below:</span></span>

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
> <span data-ttu-id="571ca-177">Devido à natureza dos sistemas distribuídos, a ordem dos dados pode não ser a mesma entre os bancos de dados do SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="571ca-177">Due to the nature of distributed systems, the data order may not be the same across SQL Data Warehouse databases.</span></span> <span data-ttu-id="571ca-178">Outra opção é usar a função **queryout** do bcp para escrever uma extração de consulta, em vez de exportar a tabela inteira.</span><span class="sxs-lookup"><span data-stu-id="571ca-178">Another option is to use the **queryout** function of bcp to write a query extract rather than export the entire table.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="571ca-179">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="571ca-179">Next steps</span></span>
<span data-ttu-id="571ca-180">Para obter uma visão geral do carregamento, confira [Carregar dados no SQL Data Warehouse][Load data into SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="571ca-180">For an overview of loading, see [Load data into SQL Data Warehouse][Load data into SQL Data Warehouse].</span></span>
<span data-ttu-id="571ca-181">Para obter mais dicas de desenvolvimento, consulte [Visão geral de desenvolvimento do SQL Data Warehouse][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="571ca-181">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

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
