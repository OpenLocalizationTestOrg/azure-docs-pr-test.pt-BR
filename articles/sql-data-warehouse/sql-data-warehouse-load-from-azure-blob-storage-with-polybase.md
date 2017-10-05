---
title: Carregar do blob do Azure para o Azure data warehouse | Microsoft Docs
description: "Aprenda a usar o PolyBase para carregar dados do armazenamento de blobs do Azure no SQL Data Warehouse. Carregue algumas tabelas de dados públicos no esquema do Data Warehouse de Varejo da Contoso."
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
ms.openlocfilehash: 2859c1144f72fd685af89f83024df1409902ab0c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="load-data-from-azure-blob-storage-into-sql-data-warehouse-polybase"></a><span data-ttu-id="aa20a-104">Carregar dados do armazenamento de blobs do Azure no SQL Data Warehouse (PolyBase)</span><span class="sxs-lookup"><span data-stu-id="aa20a-104">Load data from Azure blob storage into SQL Data Warehouse (PolyBase)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="aa20a-105">Fábrica de dados</span><span class="sxs-lookup"><span data-stu-id="aa20a-105">Data Factory</span></span>](sql-data-warehouse-load-from-azure-blob-storage-with-data-factory.md)
> * [<span data-ttu-id="aa20a-106">PolyBase</span><span class="sxs-lookup"><span data-stu-id="aa20a-106">PolyBase</span></span>](sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md)
> 
> 

<span data-ttu-id="aa20a-107">Usar comandos do PolyBase e T-SQL para carregar dados do armazenamento de blobs do Azure no SQL Data Warehouse do Azure.</span><span class="sxs-lookup"><span data-stu-id="aa20a-107">Use PolyBase and T-SQL commands to load data from Azure blob storage into Azure SQL Data Warehouse.</span></span> 

<span data-ttu-id="aa20a-108">Para simplificar, este tutorial carrega duas tabelas em um Blob de Armazenamento do Azure público para o esquema do Data Warehouse de Varejo da Contoso.</span><span class="sxs-lookup"><span data-stu-id="aa20a-108">To keep it simple, this tutorial loads two tables from a public Azure Storage Blob into the Contoso Retail Data Warehouse schema.</span></span> <span data-ttu-id="aa20a-109">Para carregar o conjunto de dados completo, execute o exemplo [Carregar o Contoso Retail Data Warehouse completo][Load the full Contoso Retail Data Warehouse] pelo repositório de Exemplos do Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="aa20a-109">To load the full data set, run the example [Load the full Contoso Retail Data Warehouse][Load the full Contoso Retail Data Warehouse] from the Microsoft SQL Server Samples repository.</span></span>

<span data-ttu-id="aa20a-110">Neste tutorial, você irá:</span><span class="sxs-lookup"><span data-stu-id="aa20a-110">In this tutorial you will:</span></span>

1. <span data-ttu-id="aa20a-111">Configurar PolyBase para carregar do armazenamento de blobs do Azure</span><span class="sxs-lookup"><span data-stu-id="aa20a-111">Configure PolyBase to load from Azure blob storage</span></span>
2. <span data-ttu-id="aa20a-112">Carregar dados públicos em seu banco de dados</span><span class="sxs-lookup"><span data-stu-id="aa20a-112">Load public data into your database</span></span>
3. <span data-ttu-id="aa20a-113">Execute otimizações após o carregamento ser concluído.</span><span class="sxs-lookup"><span data-stu-id="aa20a-113">Perform optimizations after the load is finished.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="aa20a-114">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="aa20a-114">Before you begin</span></span>
<span data-ttu-id="aa20a-115">Para executar este tutorial, você precisa de uma conta do Azure que já tenha um banco de dados do SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="aa20a-115">To run this tutorial, you need an Azure account that already has a SQL Data Warehouse database.</span></span> <span data-ttu-id="aa20a-116">Se você ainda não tiver uma, confira [Criar um SQL Data Warehouse][Create a SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="aa20a-116">If you don't already have this, see [Create a SQL Data Warehouse][Create a SQL Data Warehouse].</span></span>

## <a name="1-configure-the-data-source"></a><span data-ttu-id="aa20a-117">1. Configurar a fonte de dados</span><span class="sxs-lookup"><span data-stu-id="aa20a-117">1. Configure the data source</span></span>
<span data-ttu-id="aa20a-118">O PolyBase usa objetos externos do T-SQL para definir o local e os atributos dos dados externos.</span><span class="sxs-lookup"><span data-stu-id="aa20a-118">PolyBase uses T-SQL external objects to define the location and attributes of the external data.</span></span> <span data-ttu-id="aa20a-119">As definições de objeto externo são armazenadas no SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="aa20a-119">The external object definitions are stored in SQL Data Warehouse.</span></span> <span data-ttu-id="aa20a-120">Os dados em si são armazenados externamente.</span><span class="sxs-lookup"><span data-stu-id="aa20a-120">The data itself is stored externally.</span></span>

### <a name="11-create-a-credential"></a><span data-ttu-id="aa20a-121">1.1.</span><span class="sxs-lookup"><span data-stu-id="aa20a-121">1.1.</span></span> <span data-ttu-id="aa20a-122">Criar uma credencial</span><span class="sxs-lookup"><span data-stu-id="aa20a-122">Create a credential</span></span>
<span data-ttu-id="aa20a-123">**Ignore esta etapa** se você estiver carregando os dados públicos da Contoso.</span><span class="sxs-lookup"><span data-stu-id="aa20a-123">**Skip this step** if you are loading the Contoso public data.</span></span> <span data-ttu-id="aa20a-124">Você não precisa proteger o acesso aos dados públicos, pois eles já estão acessíveis a qualquer pessoa.</span><span class="sxs-lookup"><span data-stu-id="aa20a-124">You don't need secure access to the public data since it is already accessible to anyone.</span></span>

<span data-ttu-id="aa20a-125">**Não ignore esta etapa** se você estiver usando este tutorial como um modelo para carregar seus próprios dados.</span><span class="sxs-lookup"><span data-stu-id="aa20a-125">**Don't skip this step** if you are using this tutorial as a template for loading your own data.</span></span> <span data-ttu-id="aa20a-126">Para acessar dados por meio de uma credencial, use o seguinte script para criar uma credencial com escopo de banco de dados e, em seguida, usá-lo ao definir o local da fonte de dados.</span><span class="sxs-lookup"><span data-stu-id="aa20a-126">To access data through a credential, use the following script to create a database-scoped credential, and then use it when defining the location of the data source.</span></span>

```sql
-- A: Create a master key.
-- Only necessary if one does not already exist.
-- Required to encrypt the credential secret in the next step.

CREATE MASTER KEY;


-- B: Create a database scoped credential
-- IDENTITY: Provide any string, it is not used for authentication to Azure storage.
-- SECRET: Provide your Azure storage account key.


CREATE DATABASE SCOPED CREDENTIAL AzureStorageCredential
WITH
    IDENTITY = 'user',
    SECRET = '<azure_storage_account_key>'
;


-- C: Create an external data source
-- TYPE: HADOOP - PolyBase uses Hadoop APIs to access data in Azure blob storage.
-- LOCATION: Provide Azure storage account name and blob container name.
-- CREDENTIAL: Provide the credential created in the previous step.

CREATE EXTERNAL DATA SOURCE AzureStorage
WITH (
    TYPE = HADOOP,
    LOCATION = 'wasbs://<blob_container_name>@<azure_storage_account_name>.blob.core.windows.net',
    CREDENTIAL = AzureStorageCredential
);
```

<span data-ttu-id="aa20a-127">Pule para a etapa 2.</span><span class="sxs-lookup"><span data-stu-id="aa20a-127">Skip to step 2.</span></span>

### <a name="12-create-the-external-data-source"></a><span data-ttu-id="aa20a-128">1.2.</span><span class="sxs-lookup"><span data-stu-id="aa20a-128">1.2.</span></span> <span data-ttu-id="aa20a-129">Criar a fonte de dados externa</span><span class="sxs-lookup"><span data-stu-id="aa20a-129">Create the external data source</span></span>
<span data-ttu-id="aa20a-130">Use este comando [CREATE EXTERNAL DATA SOURCE][CREATE EXTERNAL DATA SOURCE] para armazenar o local dos dados e o tipo de dados.</span><span class="sxs-lookup"><span data-stu-id="aa20a-130">Use this [CREATE EXTERNAL DATA SOURCE][CREATE EXTERNAL DATA SOURCE] command to store the location of the data, and the type of data.</span></span> 

```sql
CREATE EXTERNAL DATA SOURCE AzureStorage_west_public
WITH 
(  
    TYPE = Hadoop 
,   LOCATION = 'wasbs://contosoretaildw-tables@contosoretaildw.blob.core.windows.net/'
); 
```

> [!IMPORTANT]
> <span data-ttu-id="aa20a-131">Se você optar por tornar seus contêineres do armazenamento de blobs do Azure públicos, tenha em mente que, como proprietário dos dados, você será responsável por encargos de saída de dados quando os dados deixarem o datacenter.</span><span class="sxs-lookup"><span data-stu-id="aa20a-131">If you choose to make your azure blob storage containers public, remember that as the data owner you will be charged for data egress charges when data leaves the data center.</span></span> 
> 
> 

## <a name="2-configure-data-format"></a><span data-ttu-id="aa20a-132">2. Configurar o formato de dados</span><span class="sxs-lookup"><span data-stu-id="aa20a-132">2. Configure data format</span></span>
<span data-ttu-id="aa20a-133">Os dados são armazenados em arquivos de texto no armazenamento de blobs do Azure e cada campo é separado por um delimitador.</span><span class="sxs-lookup"><span data-stu-id="aa20a-133">The data is stored in text files in Azure blob storage, and each field is separated with a delimiter.</span></span> <span data-ttu-id="aa20a-134">Execute este comando [CREATE EXTERNAL FILE FORMAT][CREATE EXTERNAL FILE FORMAT] para especificar o formato dos dados nos arquivos de texto.</span><span class="sxs-lookup"><span data-stu-id="aa20a-134">Run this [CREATE EXTERNAL FILE FORMAT][CREATE EXTERNAL FILE FORMAT] command to specify the format of the data in the text files.</span></span> <span data-ttu-id="aa20a-135">Os dados da Contoso são descompactados e delimitados por barra vertical.</span><span class="sxs-lookup"><span data-stu-id="aa20a-135">The Contoso data is uncompressed and pipe delimited.</span></span>

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

## <a name="3-create-the-external-tables"></a><span data-ttu-id="aa20a-136">3. Criar as tabelas externas</span><span class="sxs-lookup"><span data-stu-id="aa20a-136">3. Create the external tables</span></span>
<span data-ttu-id="aa20a-137">Agora que você especificou o formato do arquivo e da fonte de dados, você está pronto para criar as tabelas externas.</span><span class="sxs-lookup"><span data-stu-id="aa20a-137">Now that you have specified the data source and file format, you are ready to create the external tables.</span></span> 

### <a name="31-create-a-schema-for-the-data"></a><span data-ttu-id="aa20a-138">3.1.</span><span class="sxs-lookup"><span data-stu-id="aa20a-138">3.1.</span></span> <span data-ttu-id="aa20a-139">Crie um esquema para os dados.</span><span class="sxs-lookup"><span data-stu-id="aa20a-139">Create a schema for the data.</span></span>
<span data-ttu-id="aa20a-140">Para criar um local para armazenar os dados da Contoso no banco de dados, crie um esquema.</span><span class="sxs-lookup"><span data-stu-id="aa20a-140">To create a place to store the Contoso data in your database, create a schema.</span></span>

```sql
CREATE SCHEMA [asb]
GO
```

### <a name="32-create-the-external-tables"></a><span data-ttu-id="aa20a-141">3.2.</span><span class="sxs-lookup"><span data-stu-id="aa20a-141">3.2.</span></span> <span data-ttu-id="aa20a-142">Crie as tabelas externas.</span><span class="sxs-lookup"><span data-stu-id="aa20a-142">Create the external tables.</span></span>
<span data-ttu-id="aa20a-143">Execute este script para criar as tabelas externas DimProduct e FactOnlineSales.</span><span class="sxs-lookup"><span data-stu-id="aa20a-143">Run this script to create the DimProduct and FactOnlineSales external tables.</span></span> <span data-ttu-id="aa20a-144">Tudo o que estamos fazendo aqui é definir nomes de coluna e tipos de dados e associá-los ao local e ao formato dos arquivos de armazenamento de blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="aa20a-144">All we are doing here is defining column names and data types, and binding them to the location and format of the Azure blob storage files.</span></span> <span data-ttu-id="aa20a-145">A definição é armazenada no SQL Data Warehouse e os dados ainda estão no Blob de Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="aa20a-145">The definition is stored in SQL Data Warehouse and the data is still in the Azure Storage Blob.</span></span>

<span data-ttu-id="aa20a-146">O parâmetro **LOCATION** é a pasta sob a pasta raiz no Azure Storage Blob.</span><span class="sxs-lookup"><span data-stu-id="aa20a-146">The  **LOCATION** parameter is the folder under the root folder in the Azure Storage Blob.</span></span> <span data-ttu-id="aa20a-147">Cada tabela é em uma pasta diferente.</span><span class="sxs-lookup"><span data-stu-id="aa20a-147">Each table is in a different folder.</span></span>

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

## <a name="4-load-the-data"></a><span data-ttu-id="aa20a-148">4. Carregar os dados</span><span class="sxs-lookup"><span data-stu-id="aa20a-148">4. Load the data</span></span>
<span data-ttu-id="aa20a-149">Há diferentes maneiras de acessar dados externos.</span><span class="sxs-lookup"><span data-stu-id="aa20a-149">There's different ways to access external data.</span></span>  <span data-ttu-id="aa20a-150">Você pode consultar dados diretamente da tabela externa, carregar os dados nas novas tabelas de banco de dados ou adicionar dados externos às tabelas de banco de dados existentes.</span><span class="sxs-lookup"><span data-stu-id="aa20a-150">You can query data directly from the external table, load the data into new database tables, or add external data to existing database tables.</span></span>  

### <a name="41-create-a-new-schema"></a><span data-ttu-id="aa20a-151">4.1.</span><span class="sxs-lookup"><span data-stu-id="aa20a-151">4.1.</span></span> <span data-ttu-id="aa20a-152">Criar um novo esquema</span><span class="sxs-lookup"><span data-stu-id="aa20a-152">Create a new schema</span></span>
<span data-ttu-id="aa20a-153">O CTAS cria uma nova tabela que contém dados.</span><span class="sxs-lookup"><span data-stu-id="aa20a-153">CTAS creates a new table that contains data.</span></span>  <span data-ttu-id="aa20a-154">Primeiro, crie um esquema para os dados da Contoso.</span><span class="sxs-lookup"><span data-stu-id="aa20a-154">First, create a schema for the contoso data.</span></span>

```sql
CREATE SCHEMA [cso]
GO
```

### <a name="42-load-the-data-into-new-tables"></a><span data-ttu-id="aa20a-155">4.2.</span><span class="sxs-lookup"><span data-stu-id="aa20a-155">4.2.</span></span> <span data-ttu-id="aa20a-156">Carregar os dados em novas tabelas</span><span class="sxs-lookup"><span data-stu-id="aa20a-156">Load the data into new tables</span></span>
<span data-ttu-id="aa20a-157">Para carregar dados de um armazenamento de blobs do Azure e salvá-los em uma tabela no banco de dados, use a instrução [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)].</span><span class="sxs-lookup"><span data-stu-id="aa20a-157">To load data from Azure blob storage and save it in a table inside of your database, use the [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)] statement.</span></span> <span data-ttu-id="aa20a-158">Carregamento com CTAS utiliza as tabelas externas fortemente tipadas que você acabou de criar. Para carregar os dados em novas tabelas, use uma instrução [CTAS][CTAS] por tabela.</span><span class="sxs-lookup"><span data-stu-id="aa20a-158">Loading with CTAS leverages the strongly typed external tables you have just created.To load the data into new tables, use one [CTAS][CTAS] statement per table.</span></span> 
 
<span data-ttu-id="aa20a-159">O CTAS cria uma nova tabela e a preenche com os resultados de uma instrução select.</span><span class="sxs-lookup"><span data-stu-id="aa20a-159">CTAS creates a new table and populates it with the results of a select statement.</span></span> <span data-ttu-id="aa20a-160">CTAS define a nova tabela para ter as mesmas colunas e tipos de dados como os resultados da instrução select.</span><span class="sxs-lookup"><span data-stu-id="aa20a-160">CTAS defines the new table to have the same columns and data types as the results of the select statement.</span></span> <span data-ttu-id="aa20a-161">Se você selecionar todas as colunas de uma tabela externa, a nova tabela será uma réplica das colunas e dos tipos de dados na tabela externa.</span><span class="sxs-lookup"><span data-stu-id="aa20a-161">If you select all the columns from an external table, the new table will be a replica of the columns and data types in the external table.</span></span>

<span data-ttu-id="aa20a-162">Neste exemplo, criamos a dimensão e a tabela de fatos como tabela distribuídas de hash.</span><span class="sxs-lookup"><span data-stu-id="aa20a-162">In this example, we create both the dimension and the fact table as hash distributed tables.</span></span> 

```sql
SELECT GETDATE();
GO

CREATE TABLE [cso].[DimProduct]            WITH (DISTRIBUTION = HASH([ProductKey]  ) ) AS SELECT * FROM [asb].[DimProduct]             OPTION (LABEL = 'CTAS : Load [cso].[DimProduct]             ');
CREATE TABLE [cso].[FactOnlineSales]       WITH (DISTRIBUTION = HASH([ProductKey]  ) ) AS SELECT * FROM [asb].[FactOnlineSales]        OPTION (LABEL = 'CTAS : Load [cso].[FactOnlineSales]        ');
```

### <a name="43-track-the-load-progress"></a><span data-ttu-id="aa20a-163">4.3 Acompanhar o progresso do carregamento</span><span class="sxs-lookup"><span data-stu-id="aa20a-163">4.3 Track the load progress</span></span>
<span data-ttu-id="aa20a-164">Você pode acompanhar o progresso do carregamento usando as DMVs (exibições de gerenciamento dinâmico).</span><span class="sxs-lookup"><span data-stu-id="aa20a-164">You can track the progress of your load using dynamic management views (DMVs).</span></span> 

```sql
-- To see all requests
SELECT * FROM sys.dm_pdw_exec_requests;

-- To see a particular request identified by its label
SELECT * FROM sys.dm_pdw_exec_requests as r
WHERE r.[label] = 'CTAS : Load [cso].[DimProduct]             '
      OR r.[label] = 'CTAS : Load [cso].[FactOnlineSales]        '
;

-- To track bytes and files
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

## <a name="5-optimize-columnstore-compression"></a><span data-ttu-id="aa20a-165">5. Otimizar a compactação columnstore</span><span class="sxs-lookup"><span data-stu-id="aa20a-165">5. Optimize columnstore compression</span></span>
<span data-ttu-id="aa20a-166">Por padrão, o SQL Data Warehouse armazena a tabela como um índice columnstore clusterizado.</span><span class="sxs-lookup"><span data-stu-id="aa20a-166">By default, SQL Data Warehouse stores the table as a clustered columnstore index.</span></span> <span data-ttu-id="aa20a-167">Após a conclusão do carregamento, algumas das linhas de dados não podem ser compactadas no columnstore.</span><span class="sxs-lookup"><span data-stu-id="aa20a-167">After a load completes, some of the data rows might not be compressed into the columnstore.</span></span>  <span data-ttu-id="aa20a-168">Há várias razões para isso acontecer.</span><span class="sxs-lookup"><span data-stu-id="aa20a-168">There's a variety of reasons why this can happen.</span></span> <span data-ttu-id="aa20a-169">Para obter mais informações, confira [gerenciar índices columnstore][manage columnstore indexes].</span><span class="sxs-lookup"><span data-stu-id="aa20a-169">To learn more, see [manage columnstore indexes][manage columnstore indexes].</span></span>

<span data-ttu-id="aa20a-170">Para otimizar o desempenho da consulta e a compactação columnstore após um carregamento, recrie a tabela para forçar o índice columnstore a compactar todas as linhas.</span><span class="sxs-lookup"><span data-stu-id="aa20a-170">To optimize query performance and columnstore compression after a load, rebuild the table to force the columnstore index to compress all the rows.</span></span> 

```sql
SELECT GETDATE();
GO

ALTER INDEX ALL ON [cso].[DimProduct]               REBUILD;
ALTER INDEX ALL ON [cso].[FactOnlineSales]          REBUILD;
```

<span data-ttu-id="aa20a-171">Para obter mais informações sobre como manter os índices columnstore, confira o artigo [gerenciar índices columnstore][manage columnstore indexes].</span><span class="sxs-lookup"><span data-stu-id="aa20a-171">For more information on maintaining columnstore indexes, see the [manage columnstore indexes][manage columnstore indexes] article.</span></span>

## <a name="6-optimize-statistics"></a><span data-ttu-id="aa20a-172">6. Otimizar estatísticas</span><span class="sxs-lookup"><span data-stu-id="aa20a-172">6. Optimize statistics</span></span>
<span data-ttu-id="aa20a-173">É melhor criar estatísticas de coluna única imediatamente após um carregamento.</span><span class="sxs-lookup"><span data-stu-id="aa20a-173">It is best to create single-column statistics immediately after a load.</span></span> <span data-ttu-id="aa20a-174">Há algumas opções de estatísticas.</span><span class="sxs-lookup"><span data-stu-id="aa20a-174">There are some choices for statistics.</span></span> <span data-ttu-id="aa20a-175">Por exemplo, se você criar estatísticas de coluna única em todas as colunas, poderá levar muito tempo para recompilar todas as estatísticas.</span><span class="sxs-lookup"><span data-stu-id="aa20a-175">For example, if you create single-column statistics on every column it might take a long time to rebuild all the statistics.</span></span> <span data-ttu-id="aa20a-176">Se você souber que determinadas colunas não estarão em predicados de consulta, você poderá ignorar a criação de estatísticas nessas colunas.</span><span class="sxs-lookup"><span data-stu-id="aa20a-176">If you know certain columns are not going to be in query predicates, you can skip creating statistics on those columns.</span></span>

<span data-ttu-id="aa20a-177">Se você decidir criar estatísticas com uma coluna em cada coluna de cada tabela, poderá usar o exemplo de código do procedimento armazenado `prc_sqldw_create_stats` no artigo [estatísticas][statistics].</span><span class="sxs-lookup"><span data-stu-id="aa20a-177">If you decide to create single-column statistics on every column of every table, you can use the stored procedure code sample `prc_sqldw_create_stats` in the [statistics][statistics] article.</span></span>

<span data-ttu-id="aa20a-178">O exemplo a seguir é um bom ponto de partida para a criação de estatísticas.</span><span class="sxs-lookup"><span data-stu-id="aa20a-178">The following example is a good starting point for creating statistics.</span></span> <span data-ttu-id="aa20a-179">Ele cria estatísticas de coluna única em cada coluna na tabela de dimensões e em cada coluna de junção das tabelas de fatos.</span><span class="sxs-lookup"><span data-stu-id="aa20a-179">It creates single-column statistics on each column in the dimension table, and on each joining column in the fact tables.</span></span> <span data-ttu-id="aa20a-180">Você poderá adicionar estatísticas de coluna única ou múltipla às colunas de tabelas de fatos posteriormente.</span><span class="sxs-lookup"><span data-stu-id="aa20a-180">You can always add single or multi-column statistics to other fact table columns later on.</span></span>

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

## <a name="achievement-unlocked"></a><span data-ttu-id="aa20a-181">Missão cumprida!</span><span class="sxs-lookup"><span data-stu-id="aa20a-181">Achievement unlocked!</span></span>
<span data-ttu-id="aa20a-182">Você carregou com êxito os dados públicos no SQL Data Warehouse do Azure.</span><span class="sxs-lookup"><span data-stu-id="aa20a-182">You have successfully loaded public data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="aa20a-183">Bom trabalho!</span><span class="sxs-lookup"><span data-stu-id="aa20a-183">Great job!</span></span>

<span data-ttu-id="aa20a-184">Agora você pode começar a consultar as tabelas usando consultas, como mostrado a seguir:</span><span class="sxs-lookup"><span data-stu-id="aa20a-184">You can now start querying the tables using queries like the following:</span></span>

```sql
SELECT  SUM(f.[SalesAmount]) AS [sales_by_brand_amount]
,       p.[BrandName]
FROM    [cso].[FactOnlineSales] AS f
JOIN    [cso].[DimProduct]      AS p ON f.[ProductKey] = p.[ProductKey]
GROUP BY p.[BrandName]
```

## <a name="next-steps"></a><span data-ttu-id="aa20a-185">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="aa20a-185">Next steps</span></span>
<span data-ttu-id="aa20a-186">Para carregar todos os dados do Contoso Retail Data Warehouse, use o script em Para obter mais dicas de desenvolvimento, confira [Visão geral de desenvolvimento do SQL Data Warehouse][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="aa20a-186">To load the full Contoso Retail Data Warehouse data, use the script in For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

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
[Load the full Contoso Retail Data Warehouse]: https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/contoso-data-warehouse/readme.md
