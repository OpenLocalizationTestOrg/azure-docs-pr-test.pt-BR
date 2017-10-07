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
# <a name="load-data-from-azure-blob-storage-into-sql-data-warehouse-polybase"></a>Carregar dados do armazenamento de blobs do Azure no SQL Data Warehouse (PolyBase)
> [!div class="op_single_selector"]
> * [Fábrica de dados](sql-data-warehouse-load-from-azure-blob-storage-with-data-factory.md)
> * [PolyBase](sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md)
> 
> 

Use o PolyBase T-SQL comandos tooload dados e do armazenamento de BLOBs do Azure no Azure SQL Data Warehouse. 

tookeep ele simples, este tutorial carrega duas tabelas de um Blob de armazenamento público do Azure no esquema de Data Warehouse da Contoso varejo hello. tooload Olá conjunto de dados completo, execute o exemplo hello [carga Olá total do Data Warehouse Contoso varejo] [ Load hello full Contoso Retail Data Warehouse] do repositório do Microsoft SQL Server Samples hello.

Neste tutorial, você irá:

1. Configurar o PolyBase tooload do armazenamento de BLOBs do Azure
2. Carregar dados públicos em seu banco de dados
3. Execute otimizações após a conclusão da carga de saudação.

## <a name="before-you-begin"></a>Antes de começar
toorun neste tutorial, você precisa de uma conta do Azure que já tenha um banco de dados do SQL Data Warehouse. Se você ainda não tiver uma, confira [Criar um SQL Data Warehouse][Create a SQL Data Warehouse].

## <a name="1-configure-hello-data-source"></a>1. Configurar fonte de dados de saudação
PolyBase usa o local do T-SQL objetos externos toodefine hello e atributos de dados externos de saudação. definições de objeto externo Olá são armazenadas no SQL Data Warehouse. dados de saudação em si são armazenados externamente.

### <a name="11-create-a-credential"></a>1.1. Criar uma credencial
**Ignore esta etapa** se você estiver carregando dados públicos do hello Contoso. Você não precisa acesso seguro toohello pública dados porque ela já está tooanyone acessível.

**Não ignore esta etapa** se você estiver usando este tutorial como um modelo para carregar seus próprios dados. dados tooaccess por meio de uma credencial, use Olá a seguir credencial toocreate um escopo do banco de dados de script e, em seguida, usá-lo ao definir o local de Olá Olá da fonte de dados.

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

Ignore toostep 2.

### <a name="12-create-hello-external-data-source"></a>1.2. Criar fonte de dados externa Olá
Use este [CREATE EXTERNAL DATA SOURCE] [ CREATE EXTERNAL DATA SOURCE] comando toostore local de saudação de Olá dados e tipo de saudação de dados. 

```sql
CREATE EXTERNAL DATA SOURCE AzureStorage_west_public
WITH 
(  
    TYPE = Hadoop 
,   LOCATION = 'wasbs://contosoretaildw-tables@contosoretaildw.blob.core.windows.net/'
); 
```

> [!IMPORTANT]
> Se você escolher toomake seu público de contêineres de armazenamento de BLOBs do azure, lembre-se de que como o proprietário dos dados Olá você será cobrado para dados de encargos de saída quando os dados saem Datacenter hello. 
> 
> 

## <a name="2-configure-data-format"></a>2. Configurar o formato de dados
Olá dados são armazenados em arquivos de texto no armazenamento de BLOBs do Azure, e cada campo é separado com um delimitador. Executar este [CREATE EXTERNAL FILE FORMAT] [ CREATE EXTERNAL FILE FORMAT] formato de saudação do comando toospecify de dados de saudação em arquivos de texto de saudação. Olá Contoso dados é compactado e delimitado por pipe.

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

## <a name="3-create-hello-external-tables"></a>3. Criar tabelas externas de saudação
Agora que você especificou o formato de origem e o arquivo de dados hello, você está tabelas externas de saudação toocreate pronto. 

### <a name="31-create-a-schema-for-hello-data"></a>3.1. Crie um esquema para dados de saudação.
toocreate uma saudação de toostore local Contoso dados no banco de dados, criar um esquema.

```sql
CREATE SCHEMA [asb]
GO
```

### <a name="32-create-hello-external-tables"></a>3.2. Crie hello tabelas externas.
Execute este Olá toocreate de script DimProduct e FactOnlineSales tabelas externas. Tudo o que estamos fazendo aqui é definir nomes de coluna e tipos de dados e associá-los toohello local e o formato de arquivos de armazenamento de BLOBs do Azure hello. Olá definição é armazenada no SQL Data Warehouse e dados saudação ainda estão em Olá Blob de armazenamento do Azure.

Olá **local** parâmetro é a pasta de saudação na pasta raiz de saudação em Olá Blob de armazenamento do Azure. Cada tabela é em uma pasta diferente.

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

## <a name="4-load-hello-data"></a>4. Carregar dados de saudação
Não há dados externos de tooaccess de maneiras diferentes.  Você pode consultar dados diretamente da tabela externa hello, carregar dados saudação em novas tabelas de banco de dados ou adicionar tabelas de banco de dados de tooexisting dados externos.  

### <a name="41-create-a-new-schema"></a>4.1. Criar um novo esquema
O CTAS cria uma nova tabela que contém dados.  Primeiro, crie um esquema para dados de contoso saudação.

```sql
CREATE SCHEMA [cso]
GO
```

### <a name="42-load-hello-data-into-new-tables"></a>4.2. Saudação de carregar dados em novas tabelas
armazenamento de blob de dados de tooload do Azure e salvá-lo em uma tabela dentro de seu banco de dados, use Olá [CREATE TABLE AS SELECT (Transact-SQL)] [ CREATE TABLE AS SELECT (Transact-SQL)] instrução. Carregando com CTAS aproveita Olá fortemente tipados tabelas externas, você tem apenas created.tooload Olá dados em novas tabelas, use um [CTAS] [ CTAS] instrução por tabela. 
 
CTAS cria uma nova tabela e a popula com resultados de saudação de uma instrução select. CTAS define Olá nova tabela toohave Olá mesmos colunas e tipos de dados, como a instrução select de resultados de saudação do hello. Se você selecionar todas as colunas de saudação de uma tabela externa, nova tabela de saudação será uma réplica de colunas de saudação e tipos de dados na tabela externa hello.

Neste exemplo, podemos criar dimensão de saudação e a tabela de fatos hello como distribuídas tabelas de hash. 

```sql
SELECT GETDATE();
GO

CREATE TABLE [cso].[DimProduct]            WITH (DISTRIBUTION = HASH([ProductKey]  ) ) AS SELECT * FROM [asb].[DimProduct]             OPTION (LABEL = 'CTAS : Load [cso].[DimProduct]             ');
CREATE TABLE [cso].[FactOnlineSales]       WITH (DISTRIBUTION = HASH([ProductKey]  ) ) AS SELECT * FROM [asb].[FactOnlineSales]        OPTION (LABEL = 'CTAS : Load [cso].[FactOnlineSales]        ');
```

### <a name="43-track-hello-load-progress"></a>4.3 acompanhar o progresso de carregamento de saudação
Você pode acompanhar o progresso de saudação de sua carga usando exibições de gerenciamento dinâmico (DMVs). 

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

## <a name="5-optimize-columnstore-compression"></a>5. Otimizar a compactação columnstore
Por padrão, o SQL Data Warehouse armazena tabela hello como um índice columnstore clusterizado. Após a conclusão de uma carga, algumas das linhas de dados de saudação não podem ser compactadas no Olá columnstore.  Há várias razões para isso acontecer. mais, consulte toolearn [gerenciar índices de columnstore][manage columnstore indexes].

consulta de toooptimize desempenho e compactação columnstore depois de uma carga recriar Olá tabela tooforce Olá columnstore index toocompress todas as linhas de saudação. 

```sql
SELECT GETDATE();
GO

ALTER INDEX ALL ON [cso].[DimProduct]               REBUILD;
ALTER INDEX ALL ON [cso].[FactOnlineSales]          REBUILD;
```

Para obter mais informações sobre como manter os índices columnstore, consulte Olá [gerenciar índices de columnstore] [ manage columnstore indexes] artigo.

## <a name="6-optimize-statistics"></a>6. Otimizar estatísticas
É melhor estatísticas de coluna única toocreate imediatamente após uma carga. Há algumas opções de estatísticas. Por exemplo, se você criar estatísticas de coluna única em todas as colunas pode levar um longo tempo toorebuild todas as estatísticas de saudação. Se você souber que determinadas colunas não serão toobe em predicados de consulta, você pode ignorar a criação de estatísticas nessas colunas.

Se você decidir toocreate estatísticas de coluna única em todas as colunas de cada tabela, você pode usar o exemplo de código do procedimento armazenado hello `prc_sqldw_create_stats` em Olá [estatísticas] [ statistics] artigo.

saudação de exemplo a seguir é um bom ponto de partida para a criação de estatísticas. Cria estatísticas de coluna única em cada coluna na tabela de dimensões hello e em cada coluna de junção em tabelas de fatos hello. Você sempre poderá adicionar colunas de tabela de fatos única ou várias colunas de estatísticas tooother posteriormente.

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

## <a name="achievement-unlocked"></a>Missão cumprida!
Você carregou com êxito os dados públicos no SQL Data Warehouse do Azure. Bom trabalho!

Agora você pode começar a consultar tabelas hello usando consultas como Olá a seguir:

```sql
SELECT  SUM(f.[SalesAmount]) AS [sales_by_brand_amount]
,       p.[BrandName]
FROM    [cso].[FactOnlineSales] AS f
JOIN    [cso].[DimProduct]      AS p ON f.[ProductKey] = p.[ProductKey]
GROUP BY p.[BrandName]
```

## <a name="next-steps"></a>Próximas etapas
dados de Data Warehouse da Contoso comercial completos saudação de tooload, usar script hello para obter mais dicas de desenvolvimento, consulte [visão geral do desenvolvimento de SQL Data Warehouse][SQL Data Warehouse development overview].

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
