---
title: aaaLoad do data warehouse de BLOBs do Azure tooAzure | Microsoft Docs
description: "Saiba como toouse tooload dados do Azure blob storage no SQL Data Warehouse. Carregar algumas tabelas de dados públicos no esquema de Data Warehouse da Contoso varejo hello."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: faca0fe7-62e7-4e1f-a86f-032b4ffcb06e
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 4b4978ccefa4d55ff5c89fba84c5e705422ddbb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-azure-blob-storage-into-sql-data-warehouse-polybase"></a><span data-ttu-id="1ad13-104">Carregar dados do armazenamento de blobs do Azure no SQL Data Warehouse (PolyBase)</span><span class="sxs-lookup"><span data-stu-id="1ad13-104">Load data from Azure blob storage into SQL Data Warehouse (PolyBase)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1ad13-105">Fábrica de dados</span><span class="sxs-lookup"><span data-stu-id="1ad13-105">Data Factory</span></span>](sql-data-warehouse-load-from-azure-blob-storage-with-data-factory.md)
> * [<span data-ttu-id="1ad13-106">PolyBase</span><span class="sxs-lookup"><span data-stu-id="1ad13-106">PolyBase</span></span>](sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md)
> 
> 

<span data-ttu-id="1ad13-107">Use o PolyBase T-SQL comandos tooload dados e do armazenamento de BLOBs do Azure no Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="1ad13-107">Use PolyBase and T-SQL commands tooload data from Azure blob storage into Azure SQL Data Warehouse.</span></span> 

<span data-ttu-id="1ad13-108">tookeep ele simples, este tutorial carrega duas tabelas de um Blob de armazenamento público do Azure no esquema de Data Warehouse da Contoso varejo hello.</span><span class="sxs-lookup"><span data-stu-id="1ad13-108">tookeep it simple, this tutorial loads two tables from a public Azure Storage Blob into hello Contoso Retail Data Warehouse schema.</span></span> <span data-ttu-id="1ad13-109">tooload Olá conjunto de dados completo, execute o exemplo hello [carga Olá total do Data Warehouse Contoso varejo] [ Load hello full Contoso Retail Data Warehouse] do repositório do Microsoft SQL Server Samples hello.</span><span class="sxs-lookup"><span data-stu-id="1ad13-109">tooload hello full data set, run hello example [Load hello full Contoso Retail Data Warehouse][Load hello full Contoso Retail Data Warehouse] from hello Microsoft SQL Server Samples repository.</span></span>

<span data-ttu-id="1ad13-110">Neste tutorial, você irá:</span><span class="sxs-lookup"><span data-stu-id="1ad13-110">In this tutorial you will:</span></span>

1. <span data-ttu-id="1ad13-111">Configurar o PolyBase tooload do armazenamento de BLOBs do Azure</span><span class="sxs-lookup"><span data-stu-id="1ad13-111">Configure PolyBase tooload from Azure blob storage</span></span>
2. <span data-ttu-id="1ad13-112">Carregar dados públicos em seu banco de dados</span><span class="sxs-lookup"><span data-stu-id="1ad13-112">Load public data into your database</span></span>
3. <span data-ttu-id="1ad13-113">Execute otimizações após a conclusão da carga de saudação.</span><span class="sxs-lookup"><span data-stu-id="1ad13-113">Perform optimizations after hello load is finished.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="1ad13-114">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="1ad13-114">Before you begin</span></span>
<span data-ttu-id="1ad13-115">toorun neste tutorial, você precisa de uma conta do Azure que já tenha um banco de dados do SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="1ad13-115">toorun this tutorial, you need an Azure account that already has a SQL Data Warehouse database.</span></span> <span data-ttu-id="1ad13-116">Se você ainda não tiver uma, confira [Criar um SQL Data Warehouse][Create a SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="1ad13-116">If you don't already have this, see [Create a SQL Data Warehouse][Create a SQL Data Warehouse].</span></span>

## <a name="1-configure-hello-data-source"></a><span data-ttu-id="1ad13-117">1. Configurar fonte de dados de saudação</span><span class="sxs-lookup"><span data-stu-id="1ad13-117">1. Configure hello data source</span></span>
<span data-ttu-id="1ad13-118">PolyBase usa o local do T-SQL objetos externos toodefine hello e atributos de dados externos de saudação.</span><span class="sxs-lookup"><span data-stu-id="1ad13-118">PolyBase uses T-SQL external objects toodefine hello location and attributes of hello external data.</span></span> <span data-ttu-id="1ad13-119">definições de objeto externo Olá são armazenadas no SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="1ad13-119">hello external object definitions are stored in SQL Data Warehouse.</span></span> <span data-ttu-id="1ad13-120">dados de saudação em si são armazenados externamente.</span><span class="sxs-lookup"><span data-stu-id="1ad13-120">hello data itself is stored externally.</span></span>

### <a name="11-create-a-credential"></a><span data-ttu-id="1ad13-121">1.1.</span><span class="sxs-lookup"><span data-stu-id="1ad13-121">1.1.</span></span> <span data-ttu-id="1ad13-122">Criar uma credencial</span><span class="sxs-lookup"><span data-stu-id="1ad13-122">Create a credential</span></span>
<span data-ttu-id="1ad13-123">**Ignore esta etapa** se você estiver carregando dados públicos do hello Contoso.</span><span class="sxs-lookup"><span data-stu-id="1ad13-123">**Skip this step** if you are loading hello Contoso public data.</span></span> <span data-ttu-id="1ad13-124">Você não precisa acesso seguro toohello pública dados porque ela já está tooanyone acessível.</span><span class="sxs-lookup"><span data-stu-id="1ad13-124">You don't need secure access toohello public data since it is already accessible tooanyone.</span></span>

<span data-ttu-id="1ad13-125">**Não ignore esta etapa** se você estiver usando este tutorial como um modelo para carregar seus próprios dados.</span><span class="sxs-lookup"><span data-stu-id="1ad13-125">**Don't skip this step** if you are using this tutorial as a template for loading your own data.</span></span> <span data-ttu-id="1ad13-126">dados tooaccess por meio de uma credencial, use Olá a seguir credencial toocreate um escopo do banco de dados de script e, em seguida, usá-lo ao definir o local de Olá Olá da fonte de dados.</span><span class="sxs-lookup"><span data-stu-id="1ad13-126">tooaccess data through a credential, use hello following script toocreate a database-scoped credential, and then use it when defining hello location of hello data source.</span></span>

```sql
-- A: Create a master key.
-- Only necessary if one does not already exist.
-- Required tooencrypt hello credential secret in hello next step.

CREATE MASTER KEY;


-- B: Create a database scoped credential
-- IDENTITY: Provide any string, it is not used for authentication tooAzure storage.
-- SECRET: Provide your Azure storage account key.


CREATE DATABASE SCOPED CREDENTIAL AzureStorageCredential
WITH
    IDENTITY = 'user',
    SECRET = '<azure_storage_account_key>'
;


-- C: Create an external data source
-- TYPE: HADOOP - PolyBase uses Hadoop APIs tooaccess data in Azure blob storage.
-- LOCATION: Provide Azure storage account name and blob container name.
-- CREDENTIAL: Provide hello credential created in hello previous step.

CREATE EXTERNAL DATA SOURCE AzureStorage
WITH (
    TYPE = HADOOP,
    LOCATION = 'wasbs://<blob_container_name>@<azure_storage_account_name>.blob.core.windows.net',
    CREDENTIAL = AzureStorageCredential
);
```

<span data-ttu-id="1ad13-127">Ignore toostep 2.</span><span class="sxs-lookup"><span data-stu-id="1ad13-127">Skip toostep 2.</span></span>

### <a name="12-create-hello-external-data-source"></a><span data-ttu-id="1ad13-128">1.2.</span><span class="sxs-lookup"><span data-stu-id="1ad13-128">1.2.</span></span> <span data-ttu-id="1ad13-129">Criar fonte de dados externa Olá</span><span class="sxs-lookup"><span data-stu-id="1ad13-129">Create hello external data source</span></span>
<span data-ttu-id="1ad13-130">Use este [CREATE EXTERNAL DATA SOURCE] [ CREATE EXTERNAL DATA SOURCE] comando toostore local de saudação de Olá dados e tipo de saudação de dados.</span><span class="sxs-lookup"><span data-stu-id="1ad13-130">Use this [CREATE EXTERNAL DATA SOURCE][CREATE EXTERNAL DATA SOURCE] command toostore hello location of hello data, and hello type of data.</span></span> 

```sql
CREATE EXTERNAL DATA SOURCE AzureStorage_west_public
WITH 
(  
    TYPE = Hadoop 
,   LOCATION = 'wasbs://contosoretaildw-tables@contosoretaildw.blob.core.windows.net/'
); 
```

> [!IMPORTANT]
> <span data-ttu-id="1ad13-131">Se você escolher toomake seu público de contêineres de armazenamento de BLOBs do azure, lembre-se de que como o proprietário dos dados Olá você será cobrado para dados de encargos de saída quando os dados saem Datacenter hello.</span><span class="sxs-lookup"><span data-stu-id="1ad13-131">If you choose toomake your azure blob storage containers public, remember that as hello data owner you will be charged for data egress charges when data leaves hello data center.</span></span> 
> 
> 

## <a name="2-configure-data-format"></a><span data-ttu-id="1ad13-132">2. Configurar o formato de dados</span><span class="sxs-lookup"><span data-stu-id="1ad13-132">2. Configure data format</span></span>
<span data-ttu-id="1ad13-133">Olá dados são armazenados em arquivos de texto no armazenamento de BLOBs do Azure, e cada campo é separado com um delimitador.</span><span class="sxs-lookup"><span data-stu-id="1ad13-133">hello data is stored in text files in Azure blob storage, and each field is separated with a delimiter.</span></span> <span data-ttu-id="1ad13-134">Executar este [CREATE EXTERNAL FILE FORMAT] [ CREATE EXTERNAL FILE FORMAT] formato de saudação do comando toospecify de dados de saudação em arquivos de texto de saudação.</span><span class="sxs-lookup"><span data-stu-id="1ad13-134">Run this [CREATE EXTERNAL FILE FORMAT][CREATE EXTERNAL FILE FORMAT] command toospecify hello format of hello data in hello text files.</span></span> <span data-ttu-id="1ad13-135">Olá Contoso dados é compactado e delimitado por pipe.</span><span class="sxs-lookup"><span data-stu-id="1ad13-135">hello Contoso data is uncompressed and pipe delimited.</span></span>

```sql
CREATE EXTERNAL FILE FORMAT TextFileFormat 
WITH 
(   FORMAT_TYPE = DELIMITEDTEXT
,    FORMAT_OPTIONS    (   FIELD_TERMINATOR = '|'
                    ,    STRING_DELIMITER = ''
                    ,    DATE_FORMAT         = 'yyyy-MM-dd HH:mm:ss.fff'
                    ,    USE_TYPE_DEFAULT = FALSE 
                    )
);
``` 

## <a name="3-create-hello-external-tables"></a><span data-ttu-id="1ad13-136">3. Criar tabelas externas de saudação</span><span class="sxs-lookup"><span data-stu-id="1ad13-136">3. Create hello external tables</span></span>
<span data-ttu-id="1ad13-137">Agora que você especificou o formato de origem e o arquivo de dados hello, você está tabelas externas de saudação toocreate pronto.</span><span class="sxs-lookup"><span data-stu-id="1ad13-137">Now that you have specified hello data source and file format, you are ready toocreate hello external tables.</span></span> 

### <a name="31-create-a-schema-for-hello-data"></a><span data-ttu-id="1ad13-138">3.1.</span><span class="sxs-lookup"><span data-stu-id="1ad13-138">3.1.</span></span> <span data-ttu-id="1ad13-139">Crie um esquema para dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="1ad13-139">Create a schema for hello data.</span></span>
<span data-ttu-id="1ad13-140">toocreate uma saudação de toostore local Contoso dados no banco de dados, criar um esquema.</span><span class="sxs-lookup"><span data-stu-id="1ad13-140">toocreate a place toostore hello Contoso data in your database, create a schema.</span></span>

```sql
CREATE SCHEMA [asb]
GO
```

### <a name="32-create-hello-external-tables"></a><span data-ttu-id="1ad13-141">3.2.</span><span class="sxs-lookup"><span data-stu-id="1ad13-141">3.2.</span></span> <span data-ttu-id="1ad13-142">Crie hello tabelas externas.</span><span class="sxs-lookup"><span data-stu-id="1ad13-142">Create hello external tables.</span></span>
<span data-ttu-id="1ad13-143">Execute este Olá toocreate de script DimProduct e FactOnlineSales tabelas externas.</span><span class="sxs-lookup"><span data-stu-id="1ad13-143">Run this script toocreate hello DimProduct and FactOnlineSales external tables.</span></span> <span data-ttu-id="1ad13-144">Tudo o que estamos fazendo aqui é definir nomes de coluna e tipos de dados e associá-los toohello local e o formato de arquivos de armazenamento de BLOBs do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="1ad13-144">All we are doing here is defining column names and data types, and binding them toohello location and format of hello Azure blob storage files.</span></span> <span data-ttu-id="1ad13-145">Olá definição é armazenada no SQL Data Warehouse e dados saudação ainda estão em Olá Blob de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="1ad13-145">hello definition is stored in SQL Data Warehouse and hello data is still in hello Azure Storage Blob.</span></span>

<span data-ttu-id="1ad13-146">Olá **local** parâmetro é a pasta de saudação na pasta raiz de saudação em Olá Blob de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="1ad13-146">hello  **LOCATION** parameter is hello folder under hello root folder in hello Azure Storage Blob.</span></span> <span data-ttu-id="1ad13-147">Cada tabela é em uma pasta diferente.</span><span class="sxs-lookup"><span data-stu-id="1ad13-147">Each table is in a different folder.</span></span>

```sql

--DimProduct
CREATE EXTERNAL TABLE [asb].DimProduct (
    [ProductKey] [int] NOT NULL,
    [ProductLabel] [nvarchar](255) NULL,
    [ProductName] [nvarchar](500) NULL,
    [ProductDescription] [nvarchar](400) NULL,
    [ProductSubcategoryKey] [int] NULL,
    [Manufacturer] [nvarchar](50) NULL,
    [BrandName] [nvarchar](50) NULL,
    [ClassID] [nvarchar](10) NULL,
    [ClassName] [nvarchar](20) NULL,
    [StyleID] [nvarchar](10) NULL,
    [StyleName] [nvarchar](20) NULL,
    [ColorID] [nvarchar](10) NULL,
    [ColorName] [nvarchar](20) NOT NULL,
    [Size] [nvarchar](50) NULL,
    [SizeRange] [nvarchar](50) NULL,
    [SizeUnitMeasureID] [nvarchar](20) NULL,
    [Weight] [float] NULL,
    [WeightUnitMeasureID] [nvarchar](20) NULL,
    [UnitOfMeasureID] [nvarchar](10) NULL,
    [UnitOfMeasureName] [nvarchar](40) NULL,
    [StockTypeID] [nvarchar](10) NULL,
    [StockTypeName] [nvarchar](40) NULL,
    [UnitCost] [money] NULL,
    [UnitPrice] [money] NULL,
    [AvailableForSaleDate] [datetime] NULL,
    [StopSaleDate] [datetime] NULL,
    [Status] [nvarchar](7) NULL,
    [ImageURL] [nvarchar](150) NULL,
    [ProductURL] [nvarchar](150) NULL,
    [ETLLoadID] [int] NULL,
    [LoadDate] [datetime] NULL,
    [UpdateDate] [datetime] NULL
)
WITH
(
    LOCATION='/DimProduct/' 
,   DATA_SOURCE = AzureStorage_west_public
,   FILE_FORMAT = TextFileFormat
,   REJECT_TYPE = VALUE
,   REJECT_VALUE = 0
)
;

--FactOnlineSales
CREATE EXTERNAL TABLE [asb].FactOnlineSales 
(
    [OnlineSalesKey] [int]  NOT NULL,
    [DateKey] [datetime] NOT NULL,
    [StoreKey] [int] NOT NULL,
    [ProductKey] [int] NOT NULL,
    [PromotionKey] [int] NOT NULL,
    [CurrencyKey] [int] NOT NULL,
    [CustomerKey] [int] NOT NULL,
    [SalesOrderNumber] [nvarchar](20) NOT NULL,
    [SalesOrderLineNumber] [int] NULL,
    [SalesQuantity] [int] NOT NULL,
    [SalesAmount] [money] NOT NULL,
    [ReturnQuantity] [int] NOT NULL,
    [ReturnAmount] [money] NULL,
    [DiscountQuantity] [int] NULL,
    [DiscountAmount] [money] NULL,
    [TotalCost] [money] NOT NULL,
    [UnitCost] [money] NULL,
    [UnitPrice] [money] NULL,
    [ETLLoadID] [int] NULL,
    [LoadDate] [datetime] NULL,
    [UpdateDate] [datetime] NULL
)
WITH
(
    LOCATION='/FactOnlineSales/' 
,   DATA_SOURCE = AzureStorage_west_public
,   FILE_FORMAT = TextFileFormat
,   REJECT_TYPE = VALUE
,   REJECT_VALUE = 0
)
;
```

## <a name="4-load-hello-data"></a><span data-ttu-id="1ad13-148">4. Carregar dados de saudação</span><span class="sxs-lookup"><span data-stu-id="1ad13-148">4. Load hello data</span></span>
<span data-ttu-id="1ad13-149">Não há dados externos de tooaccess de maneiras diferentes.</span><span class="sxs-lookup"><span data-stu-id="1ad13-149">There's different ways tooaccess external data.</span></span>  <span data-ttu-id="1ad13-150">Você pode consultar dados diretamente da tabela externa hello, carregar dados saudação em novas tabelas de banco de dados ou adicionar tabelas de banco de dados de tooexisting dados externos.</span><span class="sxs-lookup"><span data-stu-id="1ad13-150">You can query data directly from hello external table, load hello data into new database tables, or add external data tooexisting database tables.</span></span>  

### <a name="41-create-a-new-schema"></a><span data-ttu-id="1ad13-151">4.1.</span><span class="sxs-lookup"><span data-stu-id="1ad13-151">4.1.</span></span> <span data-ttu-id="1ad13-152">Criar um novo esquema</span><span class="sxs-lookup"><span data-stu-id="1ad13-152">Create a new schema</span></span>
<span data-ttu-id="1ad13-153">O CTAS cria uma nova tabela que contém dados.</span><span class="sxs-lookup"><span data-stu-id="1ad13-153">CTAS creates a new table that contains data.</span></span>  <span data-ttu-id="1ad13-154">Primeiro, crie um esquema para dados de contoso saudação.</span><span class="sxs-lookup"><span data-stu-id="1ad13-154">First, create a schema for hello contoso data.</span></span>

```sql
CREATE SCHEMA [cso]
GO
```

### <a name="42-load-hello-data-into-new-tables"></a><span data-ttu-id="1ad13-155">4.2.</span><span class="sxs-lookup"><span data-stu-id="1ad13-155">4.2.</span></span> <span data-ttu-id="1ad13-156">Saudação de carregar dados em novas tabelas</span><span class="sxs-lookup"><span data-stu-id="1ad13-156">Load hello data into new tables</span></span>
<span data-ttu-id="1ad13-157">armazenamento de blob de dados de tooload do Azure e salvá-lo em uma tabela dentro de seu banco de dados, use Olá [CREATE TABLE AS SELECT (Transact-SQL)] [ CREATE TABLE AS SELECT (Transact-SQL)] instrução.</span><span class="sxs-lookup"><span data-stu-id="1ad13-157">tooload data from Azure blob storage and save it in a table inside of your database, use hello [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)] statement.</span></span> <span data-ttu-id="1ad13-158">Carregando com CTAS aproveita Olá fortemente tipados tabelas externas, você tem apenas created.tooload Olá dados em novas tabelas, use um [CTAS] [ CTAS] instrução por tabela.</span><span class="sxs-lookup"><span data-stu-id="1ad13-158">Loading with CTAS leverages hello strongly typed external tables you have just created.tooload hello data into new tables, use one [CTAS][CTAS] statement per table.</span></span> 
 
<span data-ttu-id="1ad13-159">CTAS cria uma nova tabela e a popula com resultados de saudação de uma instrução select.</span><span class="sxs-lookup"><span data-stu-id="1ad13-159">CTAS creates a new table and populates it with hello results of a select statement.</span></span> <span data-ttu-id="1ad13-160">CTAS define Olá nova tabela toohave Olá mesmos colunas e tipos de dados, como a instrução select de resultados de saudação do hello.</span><span class="sxs-lookup"><span data-stu-id="1ad13-160">CTAS defines hello new table toohave hello same columns and data types as hello results of hello select statement.</span></span> <span data-ttu-id="1ad13-161">Se você selecionar todas as colunas de saudação de uma tabela externa, nova tabela de saudação será uma réplica de colunas de saudação e tipos de dados na tabela externa hello.</span><span class="sxs-lookup"><span data-stu-id="1ad13-161">If you select all hello columns from an external table, hello new table will be a replica of hello columns and data types in hello external table.</span></span>

<span data-ttu-id="1ad13-162">Neste exemplo, podemos criar dimensão de saudação e a tabela de fatos hello como distribuídas tabelas de hash.</span><span class="sxs-lookup"><span data-stu-id="1ad13-162">In this example, we create both hello dimension and hello fact table as hash distributed tables.</span></span> 

```sql
SELECT GETDATE();
GO

CREATE TABLE [cso].[DimProduct]            WITH (DISTRIBUTION = HASH([ProductKey]  ) ) AS SELECT * FROM [asb].[DimProduct]             OPTION (LABEL = 'CTAS : Load [cso].[DimProduct]             ');
CREATE TABLE [cso].[FactOnlineSales]       WITH (DISTRIBUTION = HASH([ProductKey]  ) ) AS SELECT * FROM [asb].[FactOnlineSales]        OPTION (LABEL = 'CTAS : Load [cso].[FactOnlineSales]        ');
```

### <a name="43-track-hello-load-progress"></a><span data-ttu-id="1ad13-163">4.3 acompanhar o progresso de carregamento de saudação</span><span class="sxs-lookup"><span data-stu-id="1ad13-163">4.3 Track hello load progress</span></span>
<span data-ttu-id="1ad13-164">Você pode acompanhar o progresso de saudação de sua carga usando exibições de gerenciamento dinâmico (DMVs).</span><span class="sxs-lookup"><span data-stu-id="1ad13-164">You can track hello progress of your load using dynamic management views (DMVs).</span></span> 

```sql
-- toosee all requests
SELECT * FROM sys.dm_pdw_exec_requests;

-- toosee a particular request identified by its label
SELECT * FROM sys.dm_pdw_exec_requests as r
WHERE r.[label] = 'CTAS : Load [cso].[DimProduct]             '
      OR r.[label] = 'CTAS : Load [cso].[FactOnlineSales]        '
;

-- tootrack bytes and files
SELECT
    r.command,
    s.request_id,
    r.status,
    count(distinct input_name) as nbr_files, 
    sum(s.bytes_processed)/1024/1024/1024 as gb_processed
FROM
    sys.dm_pdw_exec_requests r
    inner join sys.dm_pdw_dms_external_work s
        on r.request_id = s.request_id
WHERE 
    r.[label] = 'CTAS : Load [cso].[DimProduct]             '
    OR r.[label] = 'CTAS : Load [cso].[FactOnlineSales]        '
GROUP BY
    r.command,
    s.request_id,
    r.status
ORDER BY
    nbr_files desc,
    gb_processed desc;
```

## <a name="5-optimize-columnstore-compression"></a><span data-ttu-id="1ad13-165">5. Otimizar a compactação columnstore</span><span class="sxs-lookup"><span data-stu-id="1ad13-165">5. Optimize columnstore compression</span></span>
<span data-ttu-id="1ad13-166">Por padrão, o SQL Data Warehouse armazena tabela hello como um índice columnstore clusterizado.</span><span class="sxs-lookup"><span data-stu-id="1ad13-166">By default, SQL Data Warehouse stores hello table as a clustered columnstore index.</span></span> <span data-ttu-id="1ad13-167">Após a conclusão de uma carga, algumas das linhas de dados de saudação não podem ser compactadas no Olá columnstore.</span><span class="sxs-lookup"><span data-stu-id="1ad13-167">After a load completes, some of hello data rows might not be compressed into hello columnstore.</span></span>  <span data-ttu-id="1ad13-168">Há várias razões para isso acontecer.</span><span class="sxs-lookup"><span data-stu-id="1ad13-168">There's a variety of reasons why this can happen.</span></span> <span data-ttu-id="1ad13-169">mais, consulte toolearn [gerenciar índices de columnstore][manage columnstore indexes].</span><span class="sxs-lookup"><span data-stu-id="1ad13-169">toolearn more, see [manage columnstore indexes][manage columnstore indexes].</span></span>

<span data-ttu-id="1ad13-170">consulta de toooptimize desempenho e compactação columnstore depois de uma carga recriar Olá tabela tooforce Olá columnstore index toocompress todas as linhas de saudação.</span><span class="sxs-lookup"><span data-stu-id="1ad13-170">toooptimize query performance and columnstore compression after a load, rebuild hello table tooforce hello columnstore index toocompress all hello rows.</span></span> 

```sql
SELECT GETDATE();
GO

ALTER INDEX ALL ON [cso].[DimProduct]               REBUILD;
ALTER INDEX ALL ON [cso].[FactOnlineSales]          REBUILD;
```

<span data-ttu-id="1ad13-171">Para obter mais informações sobre como manter os índices columnstore, consulte Olá [gerenciar índices de columnstore] [ manage columnstore indexes] artigo.</span><span class="sxs-lookup"><span data-stu-id="1ad13-171">For more information on maintaining columnstore indexes, see hello [manage columnstore indexes][manage columnstore indexes] article.</span></span>

## <a name="6-optimize-statistics"></a><span data-ttu-id="1ad13-172">6. Otimizar estatísticas</span><span class="sxs-lookup"><span data-stu-id="1ad13-172">6. Optimize statistics</span></span>
<span data-ttu-id="1ad13-173">É melhor estatísticas de coluna única toocreate imediatamente após uma carga.</span><span class="sxs-lookup"><span data-stu-id="1ad13-173">It is best toocreate single-column statistics immediately after a load.</span></span> <span data-ttu-id="1ad13-174">Há algumas opções de estatísticas.</span><span class="sxs-lookup"><span data-stu-id="1ad13-174">There are some choices for statistics.</span></span> <span data-ttu-id="1ad13-175">Por exemplo, se você criar estatísticas de coluna única em todas as colunas pode levar um longo tempo toorebuild todas as estatísticas de saudação.</span><span class="sxs-lookup"><span data-stu-id="1ad13-175">For example, if you create single-column statistics on every column it might take a long time toorebuild all hello statistics.</span></span> <span data-ttu-id="1ad13-176">Se você souber que determinadas colunas não serão toobe em predicados de consulta, você pode ignorar a criação de estatísticas nessas colunas.</span><span class="sxs-lookup"><span data-stu-id="1ad13-176">If you know certain columns are not going toobe in query predicates, you can skip creating statistics on those columns.</span></span>

<span data-ttu-id="1ad13-177">Se você decidir toocreate estatísticas de coluna única em todas as colunas de cada tabela, você pode usar o exemplo de código do procedimento armazenado hello `prc_sqldw_create_stats` em Olá [estatísticas] [ statistics] artigo.</span><span class="sxs-lookup"><span data-stu-id="1ad13-177">If you decide toocreate single-column statistics on every column of every table, you can use hello stored procedure code sample `prc_sqldw_create_stats` in hello [statistics][statistics] article.</span></span>

<span data-ttu-id="1ad13-178">saudação de exemplo a seguir é um bom ponto de partida para a criação de estatísticas.</span><span class="sxs-lookup"><span data-stu-id="1ad13-178">hello following example is a good starting point for creating statistics.</span></span> <span data-ttu-id="1ad13-179">Cria estatísticas de coluna única em cada coluna na tabela de dimensões hello e em cada coluna de junção em tabelas de fatos hello.</span><span class="sxs-lookup"><span data-stu-id="1ad13-179">It creates single-column statistics on each column in hello dimension table, and on each joining column in hello fact tables.</span></span> <span data-ttu-id="1ad13-180">Você sempre poderá adicionar colunas de tabela de fatos única ou várias colunas de estatísticas tooother posteriormente.</span><span class="sxs-lookup"><span data-stu-id="1ad13-180">You can always add single or multi-column statistics tooother fact table columns later on.</span></span>

```sql
CREATE STATISTICS [stat_cso_DimProduct_AvailableForSaleDate] ON [cso].[DimProduct]([AvailableForSaleDate]);
CREATE STATISTICS [stat_cso_DimProduct_BrandName] ON [cso].[DimProduct]([BrandName]);
CREATE STATISTICS [stat_cso_DimProduct_ClassID] ON [cso].[DimProduct]([ClassID]);
CREATE STATISTICS [stat_cso_DimProduct_ClassName] ON [cso].[DimProduct]([ClassName]);
CREATE STATISTICS [stat_cso_DimProduct_ColorID] ON [cso].[DimProduct]([ColorID]);
CREATE STATISTICS [stat_cso_DimProduct_ColorName] ON [cso].[DimProduct]([ColorName]);
CREATE STATISTICS [stat_cso_DimProduct_ETLLoadID] ON [cso].[DimProduct]([ETLLoadID]);
CREATE STATISTICS [stat_cso_DimProduct_ImageURL] ON [cso].[DimProduct]([ImageURL]);
CREATE STATISTICS [stat_cso_DimProduct_LoadDate] ON [cso].[DimProduct]([LoadDate]);
CREATE STATISTICS [stat_cso_DimProduct_Manufacturer] ON [cso].[DimProduct]([Manufacturer]);
CREATE STATISTICS [stat_cso_DimProduct_ProductDescription] ON [cso].[DimProduct]([ProductDescription]);
CREATE STATISTICS [stat_cso_DimProduct_ProductKey] ON [cso].[DimProduct]([ProductKey]);
CREATE STATISTICS [stat_cso_DimProduct_ProductLabel] ON [cso].[DimProduct]([ProductLabel]);
CREATE STATISTICS [stat_cso_DimProduct_ProductName] ON [cso].[DimProduct]([ProductName]);
CREATE STATISTICS [stat_cso_DimProduct_ProductSubcategoryKey] ON [cso].[DimProduct]([ProductSubcategoryKey]);
CREATE STATISTICS [stat_cso_DimProduct_ProductURL] ON [cso].[DimProduct]([ProductURL]);
CREATE STATISTICS [stat_cso_DimProduct_Size] ON [cso].[DimProduct]([Size]);
CREATE STATISTICS [stat_cso_DimProduct_SizeRange] ON [cso].[DimProduct]([SizeRange]);
CREATE STATISTICS [stat_cso_DimProduct_SizeUnitMeasureID] ON [cso].[DimProduct]([SizeUnitMeasureID]);
CREATE STATISTICS [stat_cso_DimProduct_Status] ON [cso].[DimProduct]([Status]);
CREATE STATISTICS [stat_cso_DimProduct_StockTypeID] ON [cso].[DimProduct]([StockTypeID]);
CREATE STATISTICS [stat_cso_DimProduct_StockTypeName] ON [cso].[DimProduct]([StockTypeName]);
CREATE STATISTICS [stat_cso_DimProduct_StopSaleDate] ON [cso].[DimProduct]([StopSaleDate]);
CREATE STATISTICS [stat_cso_DimProduct_StyleID] ON [cso].[DimProduct]([StyleID]);
CREATE STATISTICS [stat_cso_DimProduct_StyleName] ON [cso].[DimProduct]([StyleName]);
CREATE STATISTICS [stat_cso_DimProduct_UnitCost] ON [cso].[DimProduct]([UnitCost]);
CREATE STATISTICS [stat_cso_DimProduct_UnitOfMeasureID] ON [cso].[DimProduct]([UnitOfMeasureID]);
CREATE STATISTICS [stat_cso_DimProduct_UnitOfMeasureName] ON [cso].[DimProduct]([UnitOfMeasureName]);
CREATE STATISTICS [stat_cso_DimProduct_UnitPrice] ON [cso].[DimProduct]([UnitPrice]);
CREATE STATISTICS [stat_cso_DimProduct_UpdateDate] ON [cso].[DimProduct]([UpdateDate]);
CREATE STATISTICS [stat_cso_DimProduct_Weight] ON [cso].[DimProduct]([Weight]);
CREATE STATISTICS [stat_cso_DimProduct_WeightUnitMeasureID] ON [cso].[DimProduct]([WeightUnitMeasureID]);
CREATE STATISTICS [stat_cso_FactOnlineSales_CurrencyKey] ON [cso].[FactOnlineSales]([CurrencyKey]);
CREATE STATISTICS [stat_cso_FactOnlineSales_CustomerKey] ON [cso].[FactOnlineSales]([CustomerKey]);
CREATE STATISTICS [stat_cso_FactOnlineSales_DateKey] ON [cso].[FactOnlineSales]([DateKey]);
CREATE STATISTICS [stat_cso_FactOnlineSales_OnlineSalesKey] ON [cso].[FactOnlineSales]([OnlineSalesKey]);
CREATE STATISTICS [stat_cso_FactOnlineSales_ProductKey] ON [cso].[FactOnlineSales]([ProductKey]);
CREATE STATISTICS [stat_cso_FactOnlineSales_PromotionKey] ON [cso].[FactOnlineSales]([PromotionKey]);
CREATE STATISTICS [stat_cso_FactOnlineSales_StoreKey] ON [cso].[FactOnlineSales]([StoreKey]);
```

## <a name="achievement-unlocked"></a><span data-ttu-id="1ad13-181">Missão cumprida!</span><span class="sxs-lookup"><span data-stu-id="1ad13-181">Achievement unlocked!</span></span>
<span data-ttu-id="1ad13-182">Você carregou com êxito os dados públicos no SQL Data Warehouse do Azure.</span><span class="sxs-lookup"><span data-stu-id="1ad13-182">You have successfully loaded public data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="1ad13-183">Bom trabalho!</span><span class="sxs-lookup"><span data-stu-id="1ad13-183">Great job!</span></span>

<span data-ttu-id="1ad13-184">Agora você pode começar a consultar tabelas hello usando consultas como Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="1ad13-184">You can now start querying hello tables using queries like hello following:</span></span>

```sql
SELECT  SUM(f.[SalesAmount]) AS [sales_by_brand_amount]
,       p.[BrandName]
FROM    [cso].[FactOnlineSales] AS f
JOIN    [cso].[DimProduct]      AS p ON f.[ProductKey] = p.[ProductKey]
GROUP BY p.[BrandName]
```

## <a name="next-steps"></a><span data-ttu-id="1ad13-185">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1ad13-185">Next steps</span></span>
<span data-ttu-id="1ad13-186">dados de Data Warehouse da Contoso comercial completos saudação de tooload, usar script hello para obter mais dicas de desenvolvimento, consulte [visão geral do desenvolvimento de SQL Data Warehouse][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="1ad13-186">tooload hello full Contoso Retail Data Warehouse data, use hello script in For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

<!--Image references-->

<!--Article references-->
[Create a SQL Data Warehouse]: sql-data-warehouse-get-started-provision.md
[Load data into SQL Data Warehouse]: sql-data-warehouse-overview-load.md
[SQL Data Warehouse development overview]: sql-data-warehouse-overview-develop.md
[manage columnstore indexes]: sql-data-warehouse-tables-index.md
[Statistics]: sql-data-warehouse-tables-statistics.md
[CTAS]: sql-data-warehouse-develop-ctas.md
[label]: sql-data-warehouse-develop-label.md

<!--MSDN references-->
[CREATE EXTERNAL DATA SOURCE]: https://msdn.microsoft.com/en-us/library/dn935022.aspx
[CREATE EXTERNAL FILE FORMAT]: https://msdn.microsoft.com/en-us/library/dn935026.aspx
[CREATE TABLE AS SELECT (Transact-SQL)]: https://msdn.microsoft.com/library/mt204041.aspx
[sys.dm_pdw_exec_requests]: https://msdn.microsoft.com/library/mt203887.aspx
[REBUILD]: https://msdn.microsoft.com/library/ms188388.aspx

<!--Other Web references-->
[Microsoft Download Center]: http://www.microsoft.com/download/details.aspx?id=36433
[Load hello full Contoso Retail Data Warehouse]: https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/contoso-data-warehouse/readme.md
