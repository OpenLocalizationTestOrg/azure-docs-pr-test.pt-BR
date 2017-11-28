---
title: dados de tooload aaaUse bcp no SQL Data Warehouse | Microsoft Docs
description: "Saiba quais bcp é e como toouse para cenários de data warehouse."
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
ms.openlocfilehash: 09a2980585097644924c71899f9e74fb32fbc26d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-with-bcp"></a><span data-ttu-id="cdc3f-103">Carregar dados com o bcp</span><span class="sxs-lookup"><span data-stu-id="cdc3f-103">Load data with bcp</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="cdc3f-104">Redgate</span><span class="sxs-lookup"><span data-stu-id="cdc3f-104">Redgate</span></span>](sql-data-warehouse-load-with-redgate.md)  
> * [<span data-ttu-id="cdc3f-105">Fábrica de dados</span><span class="sxs-lookup"><span data-stu-id="cdc3f-105">Data Factory</span></span>](sql-data-warehouse-get-started-load-with-azure-data-factory.md)  
> * [<span data-ttu-id="cdc3f-106">PolyBase</span><span class="sxs-lookup"><span data-stu-id="cdc3f-106">PolyBase</span></span>](sql-data-warehouse-get-started-load-with-polybase.md)  
> * [<span data-ttu-id="cdc3f-107">BCP</span><span class="sxs-lookup"><span data-stu-id="cdc3f-107">BCP</span></span>](sql-data-warehouse-load-with-bcp.md)
> 
> 

<span data-ttu-id="cdc3f-108">**[BCP] [ bcp]**  é um utilitário de carregamento em massa de linha de comando que permite que você toocopy dados entre o SQL Server, arquivos de dados e SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="cdc3f-108">**[bcp][bcp]** is a command-line bulk load utility that allows you toocopy data between SQL Server, data files, and SQL Data Warehouse.</span></span> <span data-ttu-id="cdc3f-109">Use bcp tooimport grandes números de linhas em tabelas do SQL Data Warehouse ou tooexport dados de tabelas do SQL Server para arquivos de dados.</span><span class="sxs-lookup"><span data-stu-id="cdc3f-109">Use bcp tooimport large numbers of rows into SQL Data Warehouse tables or tooexport data from SQL Server tables into data files.</span></span> <span data-ttu-id="cdc3f-110">Exceto quando usado com a opção queryout hello, bcp não requer conhecimento de Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="cdc3f-110">Except when used with hello queryout option, bcp requires no knowledge of Transact-SQL.</span></span>

<span data-ttu-id="cdc3f-111">o BCP é uma maneira rápida e fácil toomove conjuntos de dados menores dentro e fora de um banco de dados do SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="cdc3f-111">bcp is a quick and easy way toomove smaller data sets into and out of a SQL Data Warehouse database.</span></span> <span data-ttu-id="cdc3f-112">a quantidade exata Olá de dados que são recomendados tooload/extração via bcp dependerão na rede de conexão toohello data center do Azure.</span><span class="sxs-lookup"><span data-stu-id="cdc3f-112">hello exact amount of data that is recommended tooload/extract via bcp will depend on you network connection toohello Azure data center.</span></span>  <span data-ttu-id="cdc3f-113">Geralmente, as tabelas de dimensão podem ser carregadas e extraídas prontamente com bcp, no entanto, não recomendamos bcp para carregar ou extrair grandes volumes de dados.</span><span class="sxs-lookup"><span data-stu-id="cdc3f-113">Generally, dimension tables can be loaded and extracted readily with bcp, however, bcp is not recommended for loading or extracting large volumes of data.</span></span>  <span data-ttu-id="cdc3f-114">O Polybase é hello recomendado a ferramenta de carregamento e extrair grandes volumes de dados, como faz um trabalho melhor aproveita a arquitetura de processamento paralelo em massa de saudação do SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="cdc3f-114">Polybase is hello recommended tool for loading and extracting large volumes of data as it does a better job leveraging hello massively parallel processing architecture of SQL Data Warehouse.</span></span>

<span data-ttu-id="cdc3f-115">Com o bcp, você pode:</span><span class="sxs-lookup"><span data-stu-id="cdc3f-115">With bcp you can:</span></span>

* <span data-ttu-id="cdc3f-116">Use um utilitário de linha de comando simples tooload de dados no SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="cdc3f-116">Use a simple command-line utility tooload data into SQL Data Warehouse.</span></span>
* <span data-ttu-id="cdc3f-117">Use um utilitário de linha de comando simples de tooextract de dados do SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="cdc3f-117">Use a simple command-line utility tooextract data from SQL Data Warehouse.</span></span>

<span data-ttu-id="cdc3f-118">Este tutorial mostrará como:</span><span class="sxs-lookup"><span data-stu-id="cdc3f-118">This tutorial will show you how to:</span></span>

* <span data-ttu-id="cdc3f-119">Importar dados em uma tabela usando o bcp Olá no comando</span><span class="sxs-lookup"><span data-stu-id="cdc3f-119">Import data into a table using hello bcp in command</span></span>
* <span data-ttu-id="cdc3f-120">Exportar dados de um tabela usar Olá saída bcp comando</span><span class="sxs-lookup"><span data-stu-id="cdc3f-120">Export data from a table uisng hello bcp out command</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-data-into-Azure-SQL-Data-Warehouse-with-BCP/player]
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="cdc3f-121">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="cdc3f-121">Prerequisites</span></span>
<span data-ttu-id="cdc3f-122">toostep este tutorial, você precisa:</span><span class="sxs-lookup"><span data-stu-id="cdc3f-122">toostep through this tutorial, you need:</span></span>

* <span data-ttu-id="cdc3f-123">Um banco de dados do SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="cdc3f-123">A SQL Data Warehouse database</span></span>
* <span data-ttu-id="cdc3f-124">Utilitário de linha de comando bcp Olá instalado</span><span class="sxs-lookup"><span data-stu-id="cdc3f-124">hello bcp command line utility installed</span></span>
* <span data-ttu-id="cdc3f-125">Olá utilitário de linha de comando SQLCMD instalado</span><span class="sxs-lookup"><span data-stu-id="cdc3f-125">hello SQLCMD command line utility installed</span></span>

> [!NOTE]
> <span data-ttu-id="cdc3f-126">Você pode baixar os utilitários de bcp e o sqlcmd Olá do hello [Microsoft Download Center][Microsoft Download Center].</span><span class="sxs-lookup"><span data-stu-id="cdc3f-126">You can download hello bcp and sqlcmd utilities from hello [Microsoft Download Center][Microsoft Download Center].</span></span>
> 
> 

## <a name="import-data-into-sql-data-warehouse"></a><span data-ttu-id="cdc3f-127">Importar dados no SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="cdc3f-127">Import data into SQL Data Warehouse</span></span>
<span data-ttu-id="cdc3f-128">Neste tutorial, você criará uma tabela no Azure SQL Data Warehouse e importar dados em tabela hello.</span><span class="sxs-lookup"><span data-stu-id="cdc3f-128">In this tutorial, you will create a table in Azure SQL Data Warehouse and import data into hello table.</span></span>

### <a name="step-1-create-a-table-in-azure-sql-data-warehouse"></a><span data-ttu-id="cdc3f-129">Etapa 1: Criar uma tabela no SQL Data Warehouse do Azure</span><span class="sxs-lookup"><span data-stu-id="cdc3f-129">Step 1: Create a table in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="cdc3f-130">Em um prompt de comando, use sqlcmd toorun Olá toocreate consulta uma tabela a seguir na instância do:</span><span class="sxs-lookup"><span data-stu-id="cdc3f-130">From a command prompt, use sqlcmd toorun hello following query toocreate a table on your instance:</span></span>

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
> <span data-ttu-id="cdc3f-131">Consulte [visão geral da tabela] [ Table Overview] ou [sintaxe CREATE TABLE] [ CREATE TABLE syntax] para obter mais informações sobre como criar uma tabela no SQL Data Warehouse e hello  opções disponíveis na cláusula WITH de saudação.</span><span class="sxs-lookup"><span data-stu-id="cdc3f-131">See [Table Overview][Table Overview] or [CREATE TABLE syntax][CREATE TABLE syntax] for more information about creating a table on SQL Data Warehouse and hello  options available in hello WITH clause.</span></span>
> 
> 

### <a name="step-2-create-a-source-data-file"></a><span data-ttu-id="cdc3f-132">Etapa 2: Criar um arquivo de dados de origem</span><span class="sxs-lookup"><span data-stu-id="cdc3f-132">Step 2: Create a source data file</span></span>
<span data-ttu-id="cdc3f-133">Abra o bloco de notas e copie Olá linhas de dados a seguir em um novo arquivo de texto e, em seguida, salvar esse arquivo tooyour local diretório temp, C:\Temp\DimDate2.txt.</span><span class="sxs-lookup"><span data-stu-id="cdc3f-133">Open Notepad and copy hello following lines of data into a new text file and then save this file tooyour local temp directory, C:\Temp\DimDate2.txt.</span></span>

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
> <span data-ttu-id="cdc3f-134">É importante tooremember que bcp.exe não oferece suporte para a codificação do arquivo hello UTF-8.</span><span class="sxs-lookup"><span data-stu-id="cdc3f-134">It is important tooremember that bcp.exe does not support hello UTF-8 file encoding.</span></span> <span data-ttu-id="cdc3f-135">Use arquivos ASCII ou arquivos codificados em UTF-16 ao usar o bcp.exe.</span><span class="sxs-lookup"><span data-stu-id="cdc3f-135">Please use ASCII files or UTF-16 encoded files when using bcp.exe.</span></span>
> 
> 

### <a name="step-3-connect-and-import-hello-data"></a><span data-ttu-id="cdc3f-136">Etapa 3: Conectar e importar dados de saudação</span><span class="sxs-lookup"><span data-stu-id="cdc3f-136">Step 3: Connect and import hello data</span></span>
<span data-ttu-id="cdc3f-137">Usando o bcp, você pode conectar e importar dados de saudação usando Olá a seguir substituindo valores de saudação comando conforme apropriado:</span><span class="sxs-lookup"><span data-stu-id="cdc3f-137">Using bcp, you can connect and import hello data using hello following command replacing hello values as appropriate:</span></span>

```sql
bcp DimDate2 in C:\Temp\DimDate2.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t  ','
```

<span data-ttu-id="cdc3f-138">Você pode verificar Olá dados foram carregados executando hello usando o sqlcmd de consulta a seguir:</span><span class="sxs-lookup"><span data-stu-id="cdc3f-138">You can verify hello data was loaded by running hello following query using sqlcmd:</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

<span data-ttu-id="cdc3f-139">Isso deve retornar Olá resultados a seguir:</span><span class="sxs-lookup"><span data-stu-id="cdc3f-139">This should return hello following results:</span></span>

| <span data-ttu-id="cdc3f-140">DateId</span><span class="sxs-lookup"><span data-stu-id="cdc3f-140">DateId</span></span> | <span data-ttu-id="cdc3f-141">CalendarQuarter</span><span class="sxs-lookup"><span data-stu-id="cdc3f-141">CalendarQuarter</span></span> | <span data-ttu-id="cdc3f-142">FiscalQuarter</span><span class="sxs-lookup"><span data-stu-id="cdc3f-142">FiscalQuarter</span></span> |
| --- | --- | --- |
| <span data-ttu-id="cdc3f-143">20150101</span><span class="sxs-lookup"><span data-stu-id="cdc3f-143">20150101</span></span> |<span data-ttu-id="cdc3f-144">1</span><span class="sxs-lookup"><span data-stu-id="cdc3f-144">1</span></span> |<span data-ttu-id="cdc3f-145">3</span><span class="sxs-lookup"><span data-stu-id="cdc3f-145">3</span></span> |
| <span data-ttu-id="cdc3f-146">20150201</span><span class="sxs-lookup"><span data-stu-id="cdc3f-146">20150201</span></span> |<span data-ttu-id="cdc3f-147">1</span><span class="sxs-lookup"><span data-stu-id="cdc3f-147">1</span></span> |<span data-ttu-id="cdc3f-148">3</span><span class="sxs-lookup"><span data-stu-id="cdc3f-148">3</span></span> |
| <span data-ttu-id="cdc3f-149">20150301</span><span class="sxs-lookup"><span data-stu-id="cdc3f-149">20150301</span></span> |<span data-ttu-id="cdc3f-150">1</span><span class="sxs-lookup"><span data-stu-id="cdc3f-150">1</span></span> |<span data-ttu-id="cdc3f-151">3</span><span class="sxs-lookup"><span data-stu-id="cdc3f-151">3</span></span> |
| <span data-ttu-id="cdc3f-152">20150401</span><span class="sxs-lookup"><span data-stu-id="cdc3f-152">20150401</span></span> |<span data-ttu-id="cdc3f-153">2</span><span class="sxs-lookup"><span data-stu-id="cdc3f-153">2</span></span> |<span data-ttu-id="cdc3f-154">4</span><span class="sxs-lookup"><span data-stu-id="cdc3f-154">4</span></span> |
| <span data-ttu-id="cdc3f-155">20150501</span><span class="sxs-lookup"><span data-stu-id="cdc3f-155">20150501</span></span> |<span data-ttu-id="cdc3f-156">2</span><span class="sxs-lookup"><span data-stu-id="cdc3f-156">2</span></span> |<span data-ttu-id="cdc3f-157">4</span><span class="sxs-lookup"><span data-stu-id="cdc3f-157">4</span></span> |
| <span data-ttu-id="cdc3f-158">20150601</span><span class="sxs-lookup"><span data-stu-id="cdc3f-158">20150601</span></span> |<span data-ttu-id="cdc3f-159">2</span><span class="sxs-lookup"><span data-stu-id="cdc3f-159">2</span></span> |<span data-ttu-id="cdc3f-160">4</span><span class="sxs-lookup"><span data-stu-id="cdc3f-160">4</span></span> |
| <span data-ttu-id="cdc3f-161">20150701</span><span class="sxs-lookup"><span data-stu-id="cdc3f-161">20150701</span></span> |<span data-ttu-id="cdc3f-162">3</span><span class="sxs-lookup"><span data-stu-id="cdc3f-162">3</span></span> |<span data-ttu-id="cdc3f-163">1</span><span class="sxs-lookup"><span data-stu-id="cdc3f-163">1</span></span> |
| <span data-ttu-id="cdc3f-164">20150801</span><span class="sxs-lookup"><span data-stu-id="cdc3f-164">20150801</span></span> |<span data-ttu-id="cdc3f-165">3</span><span class="sxs-lookup"><span data-stu-id="cdc3f-165">3</span></span> |<span data-ttu-id="cdc3f-166">1</span><span class="sxs-lookup"><span data-stu-id="cdc3f-166">1</span></span> |
| <span data-ttu-id="cdc3f-167">20150801</span><span class="sxs-lookup"><span data-stu-id="cdc3f-167">20150801</span></span> |<span data-ttu-id="cdc3f-168">3</span><span class="sxs-lookup"><span data-stu-id="cdc3f-168">3</span></span> |<span data-ttu-id="cdc3f-169">1</span><span class="sxs-lookup"><span data-stu-id="cdc3f-169">1</span></span> |
| <span data-ttu-id="cdc3f-170">20151001</span><span class="sxs-lookup"><span data-stu-id="cdc3f-170">20151001</span></span> |<span data-ttu-id="cdc3f-171">4</span><span class="sxs-lookup"><span data-stu-id="cdc3f-171">4</span></span> |<span data-ttu-id="cdc3f-172">2</span><span class="sxs-lookup"><span data-stu-id="cdc3f-172">2</span></span> |
| <span data-ttu-id="cdc3f-173">20151101</span><span class="sxs-lookup"><span data-stu-id="cdc3f-173">20151101</span></span> |<span data-ttu-id="cdc3f-174">4</span><span class="sxs-lookup"><span data-stu-id="cdc3f-174">4</span></span> |<span data-ttu-id="cdc3f-175">2</span><span class="sxs-lookup"><span data-stu-id="cdc3f-175">2</span></span> |
| <span data-ttu-id="cdc3f-176">20151201</span><span class="sxs-lookup"><span data-stu-id="cdc3f-176">20151201</span></span> |<span data-ttu-id="cdc3f-177">4</span><span class="sxs-lookup"><span data-stu-id="cdc3f-177">4</span></span> |<span data-ttu-id="cdc3f-178">2</span><span class="sxs-lookup"><span data-stu-id="cdc3f-178">2</span></span> |

### <a name="step-4-create-statistics-on-your-newly-loaded-data"></a><span data-ttu-id="cdc3f-179">Etapa 4: criar estatísticas sobre os dados recém-carregados</span><span class="sxs-lookup"><span data-stu-id="cdc3f-179">Step 4: Create Statistics on your newly loaded data</span></span>
<span data-ttu-id="cdc3f-180">O SQL Data Warehouse do Azure ainda não dá suporte a estatísticas de criação ou atualização automática.</span><span class="sxs-lookup"><span data-stu-id="cdc3f-180">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span></span> <span data-ttu-id="cdc3f-181">Em ordem tooget Olá melhor desempenho de suas consultas, é importante que ser criadas estatísticas em todas as colunas de todas as tabelas após a primeira carga de saudação ou alterações substanciais ocorrerem nos dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="cdc3f-181">In order tooget hello best performance from your queries, it's important that statistics be created on all columns of all tables after hello first load or any substantial changes occur in hello data.</span></span> <span data-ttu-id="cdc3f-182">Para obter uma explicação detalhada de estatísticas, consulte Olá [estatísticas] [ Statistics] tópico no grupo de desenvolver Olá de tópicos.</span><span class="sxs-lookup"><span data-stu-id="cdc3f-182">For a detailed explanation of statistics, see hello [Statistics][Statistics] topic in hello Develop group of topics.</span></span> <span data-ttu-id="cdc3f-183">Abaixo está um exemplo rápido de como toocreate estatísticas na tabela de saudação carregados neste exemplo</span><span class="sxs-lookup"><span data-stu-id="cdc3f-183">Below is a quick example of how toocreate statistics on hello tabled loaded in this example</span></span>

<span data-ttu-id="cdc3f-184">Execute Olá seguindo as instruções CREATE STATISTICS em um prompt de sqlcmd:</span><span class="sxs-lookup"><span data-stu-id="cdc3f-184">Execute hello following CREATE STATISTICS statements from a sqlcmd prompt:</span></span>

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    create statistics [DateId] on [DimDate2] ([DateId]);
    create statistics [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
    create statistics [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
"
```

## <a name="export-data-from-sql-data-warehouse"></a><span data-ttu-id="cdc3f-185">Exportar dados do SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="cdc3f-185">Export data from SQL Data Warehouse</span></span>
<span data-ttu-id="cdc3f-186">Neste tutorial, você criará um arquivo de dados de uma tabela no SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="cdc3f-186">In this tutorial, you will create a data file from a table in SQL Data Warehouse.</span></span> <span data-ttu-id="cdc3f-187">Podemos exporta os dados de saudação que criamos acima tooa novo arquivo de dados chamado DimDate2_export.txt.</span><span class="sxs-lookup"><span data-stu-id="cdc3f-187">We will export hello data we created above tooa new data file called DimDate2_export.txt.</span></span>

### <a name="step-1-export-hello-data"></a><span data-ttu-id="cdc3f-188">Etapa 1: Exportar dados de saudação</span><span class="sxs-lookup"><span data-stu-id="cdc3f-188">Step 1: Export hello data</span></span>
<span data-ttu-id="cdc3f-189">Usando o utilitário bcp de saudação, você pode se conectar e exportar dados usando Olá a seguir substituindo valores de saudação comando conforme apropriado:</span><span class="sxs-lookup"><span data-stu-id="cdc3f-189">Using hello bcp utility, you can connect and export data using hello following command replacing hello values as appropriate:</span></span>

```sql
bcp DimDate2 out C:\Temp\DimDate2_export.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t ','
```
<span data-ttu-id="cdc3f-190">Você pode verificar Olá dados foram exportados corretamente abrindo novo arquivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="cdc3f-190">You can verify hello data was exported correctly by opening hello new file.</span></span> <span data-ttu-id="cdc3f-191">dados Olá no arquivo hello devem coincidir com o texto de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="cdc3f-191">hello data in hello file should match hello text below:</span></span>

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
> <span data-ttu-id="cdc3f-192">Devido a natureza toohello dos sistemas distribuídos, ordem de saudação de dados não pode ser Olá mesmo em bancos de dados do SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="cdc3f-192">Due toohello nature of distributed systems, hello data order may not be hello same across SQL Data Warehouse databases.</span></span> <span data-ttu-id="cdc3f-193">Outra opção é Olá toouse **queryout** função de bcp toowrite uma consulta extrair, em vez de exportar a tabela inteira hello.</span><span class="sxs-lookup"><span data-stu-id="cdc3f-193">Another option is toouse hello **queryout** function of bcp toowrite a query extract rather than export hello entire table.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="cdc3f-194">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="cdc3f-194">Next steps</span></span>
<span data-ttu-id="cdc3f-195">Para obter uma visão geral do carregamento, confira [Carregar dados no SQL Data Warehouse][Load data into SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="cdc3f-195">For an overview of loading, see [Load data into SQL Data Warehouse][Load data into SQL Data Warehouse].</span></span>
<span data-ttu-id="cdc3f-196">Para obter mais dicas de desenvolvimento, consulte [Visão geral de desenvolvimento do SQL Data Warehouse][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="cdc3f-196">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

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
