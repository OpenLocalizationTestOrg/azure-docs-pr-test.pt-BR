---
title: dados de aaaLoad do SQL Server no Azure SQL Data Warehouse (PolyBase) | Microsoft Docs
description: "Usa bcp tooexport dados de arquivos de tooflat do SQL Server, o armazenamento de blob do AZCopy tooimport dados tooAzure e dados Olá tooingest no Azure SQL Data Warehouse."
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
ms.openlocfilehash: 89e2a91bc97642e9fc18545cb802b42d8dc4ad95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-sql-server-into-azure-sql-data-warehouse-azcopy"></a><span data-ttu-id="a8d40-103">Carregar dados do SQL Server no Azure SQL Data Warehouse (AZCopy)</span><span class="sxs-lookup"><span data-stu-id="a8d40-103">Load data from SQL Server into Azure SQL Data Warehouse (AZCopy)</span></span>
<span data-ttu-id="a8d40-104">Usar o bcp e dados de tooload AZCopy utilitários de linha de comando do SQL Server tooAzure do armazenamento de blob.</span><span class="sxs-lookup"><span data-stu-id="a8d40-104">Use bcp and AZCopy command-line utilities tooload data from SQL Server tooAzure blob storage.</span></span> <span data-ttu-id="a8d40-105">Use dados de saudação tooload PolyBase ou fábrica de dados do Azure no Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="a8d40-105">Then use PolyBase or Azure Data Factory tooload hello data into Azure SQL Data Warehouse.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="a8d40-106">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a8d40-106">Prerequisites</span></span>
<span data-ttu-id="a8d40-107">toostep este tutorial, você precisa:</span><span class="sxs-lookup"><span data-stu-id="a8d40-107">toostep through this tutorial, you need:</span></span>

* <span data-ttu-id="a8d40-108">Um banco de dados do SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="a8d40-108">A SQL Data Warehouse database</span></span>
* <span data-ttu-id="a8d40-109">Utilitário de linha de comando bcp Olá instalado</span><span class="sxs-lookup"><span data-stu-id="a8d40-109">hello bcp command line utility installed</span></span>
* <span data-ttu-id="a8d40-110">Olá utilitário de linha de comando SQLCMD instalado</span><span class="sxs-lookup"><span data-stu-id="a8d40-110">hello SQLCMD command line utility installed</span></span>

> [!NOTE]
> <span data-ttu-id="a8d40-111">Você pode baixar os utilitários de bcp e o sqlcmd Olá do hello [Microsoft Download Center][Microsoft Download Center].</span><span class="sxs-lookup"><span data-stu-id="a8d40-111">You can download hello bcp and sqlcmd utilities from hello [Microsoft Download Center][Microsoft Download Center].</span></span>
> 
> 

## <a name="import-data-into-sql-data-warehouse"></a><span data-ttu-id="a8d40-112">Importar dados no SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="a8d40-112">Import data into SQL Data Warehouse</span></span>
<span data-ttu-id="a8d40-113">Neste tutorial, você criará uma tabela no Azure SQL Data Warehouse e importar dados em tabela hello.</span><span class="sxs-lookup"><span data-stu-id="a8d40-113">In this tutorial, you will create a table in Azure SQL Data Warehouse and import data into hello table.</span></span>

### <a name="step-1-create-a-table-in-azure-sql-data-warehouse"></a><span data-ttu-id="a8d40-114">Etapa 1: Criar uma tabela no SQL Data Warehouse do Azure</span><span class="sxs-lookup"><span data-stu-id="a8d40-114">Step 1: Create a table in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="a8d40-115">Em um prompt de comando, use sqlcmd toorun Olá toocreate consulta uma tabela a seguir na instância do:</span><span class="sxs-lookup"><span data-stu-id="a8d40-115">From a command prompt, use sqlcmd toorun hello following query toocreate a table on your instance:</span></span>

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
> <span data-ttu-id="a8d40-116">Consulte [visão geral da tabela] [ Table Overview] ou [sintaxe CREATE TABLE] [ CREATE TABLE syntax] para obter mais informações sobre como criar uma tabela no SQL Data Warehouse e hello  opções disponíveis na cláusula WITH de saudação.</span><span class="sxs-lookup"><span data-stu-id="a8d40-116">See [Table Overview][Table Overview] or [CREATE TABLE syntax][CREATE TABLE syntax] for more information about creating a table on SQL Data Warehouse and hello  options available in hello WITH clause.</span></span>
> 
> 

### <a name="step-2-create-a-source-data-file"></a><span data-ttu-id="a8d40-117">Etapa 2: Criar um arquivo de dados de origem</span><span class="sxs-lookup"><span data-stu-id="a8d40-117">Step 2: Create a source data file</span></span>
<span data-ttu-id="a8d40-118">Abra o bloco de notas e copie Olá linhas de dados a seguir em um novo arquivo de texto e, em seguida, salvar esse arquivo tooyour local diretório temp, C:\Temp\DimDate2.txt.</span><span class="sxs-lookup"><span data-stu-id="a8d40-118">Open Notepad and copy hello following lines of data into a new text file and then save this file tooyour local temp directory, C:\Temp\DimDate2.txt.</span></span>

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
> <span data-ttu-id="a8d40-119">É importante tooremember que bcp.exe não oferece suporte para a codificação do arquivo hello UTF-8.</span><span class="sxs-lookup"><span data-stu-id="a8d40-119">It is important tooremember that bcp.exe does not support hello UTF-8 file encoding.</span></span> <span data-ttu-id="a8d40-120">Use arquivos ASCII ou arquivos codificados em UTF-16 ao usar o bcp.exe.</span><span class="sxs-lookup"><span data-stu-id="a8d40-120">Please use ASCII files or UTF-16 encoded files when using bcp.exe.</span></span>
> 
> 

### <a name="step-3-connect-and-import-hello-data"></a><span data-ttu-id="a8d40-121">Etapa 3: Conectar e importar dados de saudação</span><span class="sxs-lookup"><span data-stu-id="a8d40-121">Step 3: Connect and import hello data</span></span>
<span data-ttu-id="a8d40-122">Usando o bcp, você pode conectar e importar dados de saudação usando Olá a seguir substituindo valores de saudação comando conforme apropriado:</span><span class="sxs-lookup"><span data-stu-id="a8d40-122">Using bcp, you can connect and import hello data using hello following command replacing hello values as appropriate:</span></span>

```sql
bcp DimDate2 in C:\Temp\DimDate2.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t  ','
```

<span data-ttu-id="a8d40-123">Você pode verificar Olá dados foram carregados executando hello usando o sqlcmd de consulta a seguir:</span><span class="sxs-lookup"><span data-stu-id="a8d40-123">You can verify hello data was loaded by running hello following query using sqlcmd:</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

<span data-ttu-id="a8d40-124">Isso deve retornar Olá resultados a seguir:</span><span class="sxs-lookup"><span data-stu-id="a8d40-124">This should return hello following results:</span></span>

| <span data-ttu-id="a8d40-125">DateId</span><span class="sxs-lookup"><span data-stu-id="a8d40-125">DateId</span></span> | <span data-ttu-id="a8d40-126">CalendarQuarter</span><span class="sxs-lookup"><span data-stu-id="a8d40-126">CalendarQuarter</span></span> | <span data-ttu-id="a8d40-127">FiscalQuarter</span><span class="sxs-lookup"><span data-stu-id="a8d40-127">FiscalQuarter</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a8d40-128">20150101</span><span class="sxs-lookup"><span data-stu-id="a8d40-128">20150101</span></span> |<span data-ttu-id="a8d40-129">1</span><span class="sxs-lookup"><span data-stu-id="a8d40-129">1</span></span> |<span data-ttu-id="a8d40-130">3</span><span class="sxs-lookup"><span data-stu-id="a8d40-130">3</span></span> |
| <span data-ttu-id="a8d40-131">20150201</span><span class="sxs-lookup"><span data-stu-id="a8d40-131">20150201</span></span> |<span data-ttu-id="a8d40-132">1</span><span class="sxs-lookup"><span data-stu-id="a8d40-132">1</span></span> |<span data-ttu-id="a8d40-133">3</span><span class="sxs-lookup"><span data-stu-id="a8d40-133">3</span></span> |
| <span data-ttu-id="a8d40-134">20150301</span><span class="sxs-lookup"><span data-stu-id="a8d40-134">20150301</span></span> |<span data-ttu-id="a8d40-135">1</span><span class="sxs-lookup"><span data-stu-id="a8d40-135">1</span></span> |<span data-ttu-id="a8d40-136">3</span><span class="sxs-lookup"><span data-stu-id="a8d40-136">3</span></span> |
| <span data-ttu-id="a8d40-137">20150401</span><span class="sxs-lookup"><span data-stu-id="a8d40-137">20150401</span></span> |<span data-ttu-id="a8d40-138">2</span><span class="sxs-lookup"><span data-stu-id="a8d40-138">2</span></span> |<span data-ttu-id="a8d40-139">4</span><span class="sxs-lookup"><span data-stu-id="a8d40-139">4</span></span> |
| <span data-ttu-id="a8d40-140">20150501</span><span class="sxs-lookup"><span data-stu-id="a8d40-140">20150501</span></span> |<span data-ttu-id="a8d40-141">2</span><span class="sxs-lookup"><span data-stu-id="a8d40-141">2</span></span> |<span data-ttu-id="a8d40-142">4</span><span class="sxs-lookup"><span data-stu-id="a8d40-142">4</span></span> |
| <span data-ttu-id="a8d40-143">20150601</span><span class="sxs-lookup"><span data-stu-id="a8d40-143">20150601</span></span> |<span data-ttu-id="a8d40-144">2</span><span class="sxs-lookup"><span data-stu-id="a8d40-144">2</span></span> |<span data-ttu-id="a8d40-145">4</span><span class="sxs-lookup"><span data-stu-id="a8d40-145">4</span></span> |
| <span data-ttu-id="a8d40-146">20150701</span><span class="sxs-lookup"><span data-stu-id="a8d40-146">20150701</span></span> |<span data-ttu-id="a8d40-147">3</span><span class="sxs-lookup"><span data-stu-id="a8d40-147">3</span></span> |<span data-ttu-id="a8d40-148">1</span><span class="sxs-lookup"><span data-stu-id="a8d40-148">1</span></span> |
| <span data-ttu-id="a8d40-149">20150801</span><span class="sxs-lookup"><span data-stu-id="a8d40-149">20150801</span></span> |<span data-ttu-id="a8d40-150">3</span><span class="sxs-lookup"><span data-stu-id="a8d40-150">3</span></span> |<span data-ttu-id="a8d40-151">1</span><span class="sxs-lookup"><span data-stu-id="a8d40-151">1</span></span> |
| <span data-ttu-id="a8d40-152">20150801</span><span class="sxs-lookup"><span data-stu-id="a8d40-152">20150801</span></span> |<span data-ttu-id="a8d40-153">3</span><span class="sxs-lookup"><span data-stu-id="a8d40-153">3</span></span> |<span data-ttu-id="a8d40-154">1</span><span class="sxs-lookup"><span data-stu-id="a8d40-154">1</span></span> |
| <span data-ttu-id="a8d40-155">20151001</span><span class="sxs-lookup"><span data-stu-id="a8d40-155">20151001</span></span> |<span data-ttu-id="a8d40-156">4</span><span class="sxs-lookup"><span data-stu-id="a8d40-156">4</span></span> |<span data-ttu-id="a8d40-157">2</span><span class="sxs-lookup"><span data-stu-id="a8d40-157">2</span></span> |
| <span data-ttu-id="a8d40-158">20151101</span><span class="sxs-lookup"><span data-stu-id="a8d40-158">20151101</span></span> |<span data-ttu-id="a8d40-159">4</span><span class="sxs-lookup"><span data-stu-id="a8d40-159">4</span></span> |<span data-ttu-id="a8d40-160">2</span><span class="sxs-lookup"><span data-stu-id="a8d40-160">2</span></span> |
| <span data-ttu-id="a8d40-161">20151201</span><span class="sxs-lookup"><span data-stu-id="a8d40-161">20151201</span></span> |<span data-ttu-id="a8d40-162">4</span><span class="sxs-lookup"><span data-stu-id="a8d40-162">4</span></span> |<span data-ttu-id="a8d40-163">2</span><span class="sxs-lookup"><span data-stu-id="a8d40-163">2</span></span> |

### <a name="step-4-create-statistics-on-your-newly-loaded-data"></a><span data-ttu-id="a8d40-164">Etapa 4: criar estatísticas sobre os dados recém-carregados</span><span class="sxs-lookup"><span data-stu-id="a8d40-164">Step 4: Create Statistics on your newly loaded data</span></span>
<span data-ttu-id="a8d40-165">O SQL Data Warehouse do Azure ainda não dá suporte a estatísticas de criação ou atualização automática.</span><span class="sxs-lookup"><span data-stu-id="a8d40-165">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span></span> <span data-ttu-id="a8d40-166">Em ordem tooget Olá melhor desempenho de suas consultas, é importante que ser criadas estatísticas em todas as colunas de todas as tabelas após a primeira carga de saudação ou alterações substanciais ocorrerem nos dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="a8d40-166">In order tooget hello best performance from your queries, it's important that statistics be created on all columns of all tables after hello first load or any substantial changes occur in hello data.</span></span> <span data-ttu-id="a8d40-167">Para obter uma explicação detalhada de estatísticas, consulte Olá [estatísticas] [ Statistics] tópico no grupo de desenvolver Olá de tópicos.</span><span class="sxs-lookup"><span data-stu-id="a8d40-167">For a detailed explanation of statistics, see hello [Statistics][Statistics] topic in hello Develop group of topics.</span></span> <span data-ttu-id="a8d40-168">Abaixo está um exemplo rápido de como toocreate estatísticas na tabela de saudação carregados neste exemplo</span><span class="sxs-lookup"><span data-stu-id="a8d40-168">Below is a quick example of how toocreate statistics on hello tabled loaded in this example</span></span>

<span data-ttu-id="a8d40-169">Execute Olá seguindo as instruções CREATE STATISTICS em um prompt de sqlcmd:</span><span class="sxs-lookup"><span data-stu-id="a8d40-169">Execute hello following CREATE STATISTICS statements from a sqlcmd prompt:</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    create statistics [DateId] on [DimDate2] ([DateId]);
    create statistics [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
    create statistics [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
"
```

## <a name="export-data-from-sql-data-warehouse"></a><span data-ttu-id="a8d40-170">Exportar dados do SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="a8d40-170">Export data from SQL Data Warehouse</span></span>
<span data-ttu-id="a8d40-171">Neste tutorial, você criará um arquivo de dados de uma tabela no SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="a8d40-171">In this tutorial, you will create a data file from a table in SQL Data Warehouse.</span></span> <span data-ttu-id="a8d40-172">Podemos exporta os dados de saudação que criamos acima tooa novo arquivo de dados chamado DimDate2_export.txt.</span><span class="sxs-lookup"><span data-stu-id="a8d40-172">We will export hello data we created above tooa new data file called DimDate2_export.txt.</span></span>

### <a name="step-1-export-hello-data"></a><span data-ttu-id="a8d40-173">Etapa 1: Exportar dados de saudação</span><span class="sxs-lookup"><span data-stu-id="a8d40-173">Step 1: Export hello data</span></span>
<span data-ttu-id="a8d40-174">Usando o utilitário bcp de saudação, você pode se conectar e exportar dados usando Olá a seguir substituindo valores de saudação comando conforme apropriado:</span><span class="sxs-lookup"><span data-stu-id="a8d40-174">Using hello bcp utility, you can connect and export data using hello following command replacing hello values as appropriate:</span></span>

```sql
bcp DimDate2 out C:\Temp\DimDate2_export.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t ','
```
<span data-ttu-id="a8d40-175">Você pode verificar Olá dados foram exportados corretamente abrindo novo arquivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="a8d40-175">You can verify hello data was exported correctly by opening hello new file.</span></span> <span data-ttu-id="a8d40-176">dados Olá no arquivo hello devem coincidir com o texto de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="a8d40-176">hello data in hello file should match hello text below:</span></span>

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
> <span data-ttu-id="a8d40-177">Devido a natureza toohello dos sistemas distribuídos, ordem de saudação de dados não pode ser Olá mesmo em bancos de dados do SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="a8d40-177">Due toohello nature of distributed systems, hello data order may not be hello same across SQL Data Warehouse databases.</span></span> <span data-ttu-id="a8d40-178">Outra opção é Olá toouse **queryout** função de bcp toowrite uma consulta extrair, em vez de exportar a tabela inteira hello.</span><span class="sxs-lookup"><span data-stu-id="a8d40-178">Another option is toouse hello **queryout** function of bcp toowrite a query extract rather than export hello entire table.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="a8d40-179">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a8d40-179">Next steps</span></span>
<span data-ttu-id="a8d40-180">Para obter uma visão geral do carregamento, confira [Carregar dados no SQL Data Warehouse][Load data into SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="a8d40-180">For an overview of loading, see [Load data into SQL Data Warehouse][Load data into SQL Data Warehouse].</span></span>
<span data-ttu-id="a8d40-181">Para obter mais dicas de desenvolvimento, consulte [Visão geral de desenvolvimento do SQL Data Warehouse][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="a8d40-181">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

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
