---
title: "aaaLoad - tooSQL do repositório Azure Data Lake do Data Warehouse | Microsoft Docs"
description: "Saiba como toouse PolyBase tabelas externas dados tooload do repositório Azure Data Lake no Azure SQL Data Warehouse."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: 
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 01/25/2017
ms.author: cakarst;barbkess
ms.openlocfilehash: 50ef23b3eba5f58bc9974095f84140dc5c11fa4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-azure-data-lake-store-into-sql-data-warehouse"></a><span data-ttu-id="e3663-103">Carregar dados do Azure Data Lake Store no SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="e3663-103">Load data from Azure Data Lake Store into SQL Data Warehouse</span></span>
<span data-ttu-id="e3663-104">Este documento fornece todas as etapas necessárias tooload seus próprios dados do Azure Data Lake ADLS (repositório) no SQL Data Warehouse usando PolyBase.</span><span class="sxs-lookup"><span data-stu-id="e3663-104">This document gives you all steps you  need tooload your own data from Azure Data Lake Store (ADLS) into SQL Data Warehouse using PolyBase.</span></span>
<span data-ttu-id="e3663-105">Enquanto você estiver toorun capaz de consultas de ad hoc em dados de saudação armazenados no ADLS usando tabelas externas hello, como uma prática recomendada é recomendável importar dados de saudação para Olá SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="e3663-105">While you are able toorun adhoc queries over hello data stored in ADLS using hello External Tables, as a best practice we suggest importing hello data into hello SQL Data Warehouse.</span></span>
<span data-ttu-id="e3663-106">Tempo estimado: 10 minutos, supondo que você tem pré-requisitos Olá necessário toocomplete.</span><span class="sxs-lookup"><span data-stu-id="e3663-106">Time Estimate: 10 minutes assuming you have hello prerequisites need toocomplete.</span></span>
<span data-ttu-id="e3663-107">Neste tutorial, você aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="e3663-107">In this tutorial you will learn how to:</span></span>

1. <span data-ttu-id="e3663-108">Crie tooload de objetos de banco de dados externo do repositório Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="e3663-108">Create External Database objects tooload from Azure Data Lake Store.</span></span>
2. <span data-ttu-id="e3663-109">Conecte-se tooan diretório de armazenamento do Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="e3663-109">Connect tooan Azure Data Lake Store Directory.</span></span>
3. <span data-ttu-id="e3663-110">Carregue os dados no SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="e3663-110">Load data into Azure SQL Data Warehouse.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="e3663-111">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="e3663-111">Before you begin</span></span>
<span data-ttu-id="e3663-112">toorun neste tutorial, você precisa:</span><span class="sxs-lookup"><span data-stu-id="e3663-112">toorun this tutorial, you need:</span></span>

* <span data-ttu-id="e3663-113">Toouse de aplicativo do Active Directory do Azure para autenticação de serviços.</span><span class="sxs-lookup"><span data-stu-id="e3663-113">Azure Active Directory Application toouse for Service-to-Service authentication.</span></span> <span data-ttu-id="e3663-114">toocreate, siga [autenticação do Active directory](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-authenticate-using-active-directory)</span><span class="sxs-lookup"><span data-stu-id="e3663-114">toocreate, follow [Active directory authentication](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-authenticate-using-active-directory)</span></span>

>[!NOTE] 
> <span data-ttu-id="e3663-115">É necessário o ID do cliente hello, chave e valor de ponto de extremidade Token OAuth 2.0 do seu tooyour tooconnect de aplicativo do Active Directory do Azure Data Lake do SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="e3663-115">You need hello client ID, Key, and OAuth2.0 Token Endpoint Value of your Active Directory Application tooconnect tooyour Azure Data Lake from SQL Data Warehouse.</span></span> <span data-ttu-id="e3663-116">Detalhes de como tooget esses valores são link de saudação acima.</span><span class="sxs-lookup"><span data-stu-id="e3663-116">Details for how tooget these values are in hello link above.</span></span>
><span data-ttu-id="e3663-117">Observação para registro do aplicativo do Azure Active Directory usar Olá ID do aplicativo como Olá ID do cliente.</span><span class="sxs-lookup"><span data-stu-id="e3663-117">Note for Azure Active Directory App Registration use hello 'Application ID' as hello Client ID.</span></span>

* <span data-ttu-id="e3663-118">SQL Server Management Studio ou o SQL Server Data Tools, toodownload SSMS e conecte-se consulte [SSMS de consulta](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-query-ssms)</span><span class="sxs-lookup"><span data-stu-id="e3663-118">SQL Server Management Studio or SQL Server Data Tools, toodownload SSMS and connect see [Query SSMS](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-query-ssms)</span></span>

* <span data-ttu-id="e3663-119">Um Data Warehouse do Azure SQL toocreate um siga: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-get-started-provision</span><span class="sxs-lookup"><span data-stu-id="e3663-119">An Azure SQL Data Warehouse, toocreate one follow: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-get-started-provision</span></span>

* <span data-ttu-id="e3663-120">Um Azure Data Lake Store com ou sem a criptografia habilitada.</span><span class="sxs-lookup"><span data-stu-id="e3663-120">An Azure Data Lake Store, with or without encryption enabled.</span></span> <span data-ttu-id="e3663-121">um siga toocreate: https://docs.microsoft.com/azure/data-lake-store/data-lake-store-get-started-portal</span><span class="sxs-lookup"><span data-stu-id="e3663-121">toocreate one follow: https://docs.microsoft.com/azure/data-lake-store/data-lake-store-get-started-portal</span></span>




## <a name="configure-hello-data-source"></a><span data-ttu-id="e3663-122">Configurar fonte de dados de saudação</span><span class="sxs-lookup"><span data-stu-id="e3663-122">Configure hello data source</span></span>
<span data-ttu-id="e3663-123">PolyBase usa o local do T-SQL objetos externos toodefine hello e atributos de dados externos de saudação.</span><span class="sxs-lookup"><span data-stu-id="e3663-123">PolyBase uses T-SQL external objects toodefine hello location and attributes of hello external data.</span></span> <span data-ttu-id="e3663-124">Olá externos são armazenados em SQL Data Warehouse e Olá dados de referência que th é armazenada externamente.</span><span class="sxs-lookup"><span data-stu-id="e3663-124">hello external objects are stored in SQL Data Warehouse and reference hello data th is stored externally.</span></span>


###  <a name="create-a-credential"></a><span data-ttu-id="e3663-125">Criar uma credencial</span><span class="sxs-lookup"><span data-stu-id="e3663-125">Create a credential</span></span>
<span data-ttu-id="e3663-126">tooaccess o Azure Data Lake armazenar, você precisará toocreate tooencrypt uma chave mestra de banco de dados a seu segredo de credencial usado na próxima etapa do hello.</span><span class="sxs-lookup"><span data-stu-id="e3663-126">tooaccess your Azure Data Lake Store, you will need toocreate a Database Master Key tooencrypt your credential secret used in hello next step.</span></span>
<span data-ttu-id="e3663-127">Você, em seguida, criar uma credencial no escopo do banco de dados, que armazena as credenciais do serviço principal do hello configuradas no AAD.</span><span class="sxs-lookup"><span data-stu-id="e3663-127">You then create a Database scoped credential, which stores hello service principal credentials set up in AAD.</span></span> <span data-ttu-id="e3663-128">Para aqueles que usaram o PolyBase tooconnect tooWindows Blobs de armazenamento do Azure, observe a credencial Olá sintaxe é diferente.</span><span class="sxs-lookup"><span data-stu-id="e3663-128">For those of you who have used PolyBase tooconnect tooWindows Azure Storage Blobs, note that hello credential syntax is different.</span></span>
<span data-ttu-id="e3663-129">tooconnect tooAzure repositório Data Lake, você deve **primeiro** criar um aplicativo do Azure Active Directory, crie uma chave de acesso e conceder Olá aplicativo acesso toohello Azure Data Lake recurso.</span><span class="sxs-lookup"><span data-stu-id="e3663-129">tooconnect tooAzure Data Lake Store, you must **first** create an Azure Active Directory Application, create an access key, and grant hello application access toohello Azure Data Lake resource.</span></span> <span data-ttu-id="e3663-130">Instrucitons tooperform essas etapas estão localizadas [aqui](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-authenticate-using-active-directory).</span><span class="sxs-lookup"><span data-stu-id="e3663-130">Instrucitons tooperform these steps are located [here](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-authenticate-using-active-directory).</span></span>

```sql
-- A: Create a Database Master Key.
-- Only necessary if one does not already exist.
-- Required tooencrypt hello credential secret in hello next step.
-- For more information on Master Key: https://msdn.microsoft.com/en-us/library/ms174382.aspx?f=255&MSPPError=-2147217396

CREATE MASTER KEY;


-- B: Create a database scoped credential
-- IDENTITY: Pass hello client id and OAuth 2.0 Token Endpoint taken from your Azure Active Directory Application
-- SECRET: Provide your AAD Application Service Principal key.
-- For more information on Create Database Scoped Credential: https://msdn.microsoft.com/en-us/library/mt270260.aspx

CREATE DATABASE SCOPED CREDENTIAL ADLCredential
WITH
    IDENTITY = '<client_id>@<OAuth_2.0_Token_EndPoint>',
    SECRET = '<key>'
;

-- It should look something like this:
CREATE DATABASE SCOPED CREDENTIAL ADLCredential
WITH
    IDENTITY = '536540b4-4239-45fe-b9a3-629f97591c0c@https://login.microsoftonline.com/42f988bf-85f1-41af-91ab-2d2cd011da47/oauth2/token',
    SECRET = 'BjdIlmtKp4Fpyh9hIvr8HJlUida/seM5kQ3EpLAmeDI='
;
```


### <a name="create-hello-external-data-source"></a><span data-ttu-id="e3663-131">Criar fonte de dados externa Olá</span><span class="sxs-lookup"><span data-stu-id="e3663-131">Create hello external data source</span></span>
<span data-ttu-id="e3663-132">Use este [CREATE EXTERNAL DATA SOURCE] [ CREATE EXTERNAL DATA SOURCE] comando toostore local de saudação de Olá dados e tipo de saudação de dados.</span><span class="sxs-lookup"><span data-stu-id="e3663-132">Use this [CREATE EXTERNAL DATA SOURCE][CREATE EXTERNAL DATA SOURCE] command toostore hello location of hello data, and hello type of data.</span></span>
<span data-ttu-id="e3663-133">Você pode encontrar hello ADL URI no hello portal do Azure e www.portal.azure.com.</span><span class="sxs-lookup"><span data-stu-id="e3663-133">You can find hello ADL URI in hello Azure portal and www.portal.azure.com.</span></span>

```sql
-- C: Create an external data source
-- TYPE: HADOOP - PolyBase uses Hadoop APIs tooaccess data in Azure Data Lake Store.
-- LOCATION: Provide Azure Data Lake accountname and URI
-- CREDENTIAL: Provide hello credential created in hello previous step.

CREATE EXTERNAL DATA SOURCE AzureDataLakeStore
WITH (
    TYPE = HADOOP,
    LOCATION = 'adl://<AzureDataLake account_name>.azuredatalakestore.net',
    CREDENTIAL = ADLCredential
);
```



## <a name="configure-data-format"></a><span data-ttu-id="e3663-134">Configurar o formato de dados</span><span class="sxs-lookup"><span data-stu-id="e3663-134">Configure data format</span></span>
<span data-ttu-id="e3663-135">tooimport dados de saudação do ADLS, você precisa de formato de arquivo externo toospecify hello.</span><span class="sxs-lookup"><span data-stu-id="e3663-135">tooimport hello data from ADLS, you need toospecify hello external file format.</span></span> <span data-ttu-id="e3663-136">Esse comando tem opções específicas do formato toodescribe seus dados.</span><span class="sxs-lookup"><span data-stu-id="e3663-136">This command has format-specific options toodescribe your data.</span></span>
<span data-ttu-id="e3663-137">O exemplo abaixo é um formato de arquivo normalmente usado que é um arquivo de texto delimitado por pipe.</span><span class="sxs-lookup"><span data-stu-id="e3663-137">Below is an example of a commonly used file format that is a pipe-delimited text file.</span></span>
<span data-ttu-id="e3663-138">A nossa documentação T-SQL possui uma lista completa para [CRIAR UM FORMATO DE ARQUIVO EXTERNO][CREATE EXTERNAL FILE FORMAT]</span><span class="sxs-lookup"><span data-stu-id="e3663-138">Look at our T-SQL documentation for a complete list of [CREATE EXTERNAL FILE FORMAT][CREATE EXTERNAL FILE FORMAT]</span></span>

```sql
-- D: Create an external file format
-- FIELD_TERMINATOR: Marks hello end of each field (column) in a delimited text file
-- STRING_DELIMITER: Specifies hello field terminator for data of type string in hello text-delimited file.
-- DATE_FORMAT: Specifies a custom format for all date and time data that might appear in a delimited text file.
-- Use_Type_Default: Store all Missing values as NULL

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

## <a name="create-hello-external-tables"></a><span data-ttu-id="e3663-139">Criar tabelas externas de saudação</span><span class="sxs-lookup"><span data-stu-id="e3663-139">Create hello external tables</span></span>
<span data-ttu-id="e3663-140">Agora que você especificou o formato de origem e o arquivo de dados hello, você está tabelas externas de saudação toocreate pronto.</span><span class="sxs-lookup"><span data-stu-id="e3663-140">Now that you have specified hello data source and file format, you are ready toocreate hello external tables.</span></span> <span data-ttu-id="e3663-141">As tabelas externas servem para interagir com dados externos.</span><span class="sxs-lookup"><span data-stu-id="e3663-141">External tables are how you interact with external data.</span></span> <span data-ttu-id="e3663-142">PolyBase usa recursiva directory traversal tooread todos os arquivos em todos os subdiretórios do diretório de saudação especificado no parâmetro de local de saudação.</span><span class="sxs-lookup"><span data-stu-id="e3663-142">PolyBase uses recursive directory traversal tooread all files in all subdirectories of hello directory specified in hello location parameter.</span></span> <span data-ttu-id="e3663-143">Além disso, a saudação de exemplo a seguir mostra como toocreate Olá objeto.</span><span class="sxs-lookup"><span data-stu-id="e3663-143">Also, hello following example shows how toocreate hello object.</span></span> <span data-ttu-id="e3663-144">É necessário toocustomize Olá instrução toowork com dados Olá que tiver em ADLS.</span><span class="sxs-lookup"><span data-stu-id="e3663-144">You need toocustomize hello statement toowork with hello data you have in ADLS.</span></span>

```sql
-- D: Create an External Table
-- LOCATION: Folder under hello ADLS root folder.
-- DATA_SOURCE: Specifies which Data Source Object toouse.
-- FILE_FORMAT: Specifies which File Format Object toouse
-- REJECT_TYPE: Specifies how you want toodeal with rejected rows. Either Value or percentage of hello total
-- REJECT_VALUE: Sets hello Reject value based on hello reject type.

-- DimProduct
CREATE EXTERNAL TABLE [dbo].[DimProduct_external] (
    [ProductKey] [int] NOT NULL,
    [ProductLabel] [nvarchar](255) NULL,
    [ProductName] [nvarchar](500) NULL
)
WITH
(
    LOCATION='/DimProduct/'
,   DATA_SOURCE = AzureDataLakeStore
,   FILE_FORMAT = TextFileFormat
,   REJECT_TYPE = VALUE
,   REJECT_VALUE = 0
)
;

```

## <a name="external-table-considerations"></a><span data-ttu-id="e3663-145">Considerações sobre a tabela externa</span><span class="sxs-lookup"><span data-stu-id="e3663-145">External Table Considerations</span></span>
<span data-ttu-id="e3663-146">É fácil criar uma tabela externa, mas existem algumas nuances que precisam toobe discutido.</span><span class="sxs-lookup"><span data-stu-id="e3663-146">Creating an external table is easy, but there are some nuances that need toobe discussed.</span></span>

<span data-ttu-id="e3663-147">O carregamento de dados com o PolyBase é fortemente tipado.</span><span class="sxs-lookup"><span data-stu-id="e3663-147">Loading data with PolyBase is strongly typed.</span></span> <span data-ttu-id="e3663-148">Isso significa que cada linha de dados Olá sendo incluídos deve atender a definição de esquema de tabela hello.</span><span class="sxs-lookup"><span data-stu-id="e3663-148">This means that each row of hello data being ingested must satisfy hello table schema definition.</span></span>
<span data-ttu-id="e3663-149">Se uma determinada linha não corresponder a definição de esquema hello, linha hello é rejeitada de carga hello.</span><span class="sxs-lookup"><span data-stu-id="e3663-149">If a given row does not match hello schema definition, hello row is rejected from hello load.</span></span>

<span data-ttu-id="e3663-150">Olá REJECT_TYPE e REJECT_VALUE opções permitem que você toodefine quantas linhas ou a porcentagem de dados Olá deve estar presente na tabela final hello.</span><span class="sxs-lookup"><span data-stu-id="e3663-150">hello REJECT_TYPE and REJECT_VALUE options allow you toodefine how many rows or what percentage of hello data must be present in hello final table.</span></span>
<span data-ttu-id="e3663-151">Durante o carregamento, se Olá rejeitar valor é atingido, o carregamento de saudação falhará.</span><span class="sxs-lookup"><span data-stu-id="e3663-151">During load, if hello reject value is reached, hello load fails.</span></span> <span data-ttu-id="e3663-152">a causa mais comum Olá de linhas rejeitadas é uma incompatibilidade de definição de esquema.</span><span class="sxs-lookup"><span data-stu-id="e3663-152">hello most common cause of rejected rows is a schema definition mismatch.</span></span>
<span data-ttu-id="e3663-153">Por exemplo, se uma coluna incorretamente for dado esquema de saudação do int quando dados Olá no arquivo hello são uma cadeia de caracteres, cada linha falhará tooload.</span><span class="sxs-lookup"><span data-stu-id="e3663-153">For example, if a column is incorrectly given hello schema of int when hello data in hello file is a string, every row will fail tooload.</span></span>

<span data-ttu-id="e3663-154">Olá local Especifica pasta Olá de nível superior que você deseja tooread dados.</span><span class="sxs-lookup"><span data-stu-id="e3663-154">hello Location specifies hello topmost directory that you want tooread data from.</span></span>
<span data-ttu-id="e3663-155">Nesse caso, se houvesse subdiretórios /DimProduct/ PolyBase importaria todos os dados de saudação em subdiretórios hello.</span><span class="sxs-lookup"><span data-stu-id="e3663-155">In this case, if there were subdirectories under /DimProduct/ PolyBase would import all hello data within hello subdirectories.</span></span>

## <a name="load-hello-data"></a><span data-ttu-id="e3663-156">Carregar dados de saudação</span><span class="sxs-lookup"><span data-stu-id="e3663-156">Load hello data</span></span>
<span data-ttu-id="e3663-157">tooload de dados de repositório Azure Data Lake usar Olá [CREATE TABLE AS SELECT (Transact-SQL)] [ CREATE TABLE AS SELECT (Transact-SQL)] instrução.</span><span class="sxs-lookup"><span data-stu-id="e3663-157">tooload data from Azure Data Lake Store use hello [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)] statement.</span></span> <span data-ttu-id="e3663-158">Carregando com CTAS usa Olá fortemente tipado tabela externa que você criou.</span><span class="sxs-lookup"><span data-stu-id="e3663-158">Loading with CTAS uses hello strongly typed external table you have created.</span></span>

<span data-ttu-id="e3663-159">CTAS cria uma nova tabela e a popula com resultados de saudação de uma instrução select.</span><span class="sxs-lookup"><span data-stu-id="e3663-159">CTAS creates a new table and populates it with hello results of a select statement.</span></span> <span data-ttu-id="e3663-160">CTAS define Olá nova tabela toohave Olá mesmos colunas e tipos de dados, como a instrução select de resultados de saudação do hello.</span><span class="sxs-lookup"><span data-stu-id="e3663-160">CTAS defines hello new table toohave hello same columns and data types as hello results of hello select statement.</span></span> <span data-ttu-id="e3663-161">Se você selecionar todas as colunas de saudação de uma tabela externa, nova tabela de saudação é uma réplica de colunas de saudação e tipos de dados na tabela externa hello.</span><span class="sxs-lookup"><span data-stu-id="e3663-161">If you select all hello columns from an external table, hello new table is a replica of hello columns and data types in hello external table.</span></span>

<span data-ttu-id="e3663-162">Neste exemplo, estamos criando uma tabela distribuída de hash chamada DimProduct da nossa tabela externa DimProduct_external.</span><span class="sxs-lookup"><span data-stu-id="e3663-162">In this example, we are creating a hash distributed table called DimProduct from our External Table DimProduct_external.</span></span>

```sql

CREATE TABLE [dbo].[DimProduct]
WITH (DISTRIBUTION = HASH([ProductKey]  ) )
AS
SELECT * FROM [dbo].[DimProduct_external]
OPTION (LABEL = 'CTAS : Load [dbo].[DimProduct]');
```


## <a name="optimize-columnstore-compression"></a><span data-ttu-id="e3663-163">Otimizar a compactação columnstore</span><span class="sxs-lookup"><span data-stu-id="e3663-163">Optimize columnstore compression</span></span>
<span data-ttu-id="e3663-164">Por padrão, o SQL Data Warehouse armazena tabela hello como um índice columnstore clusterizado.</span><span class="sxs-lookup"><span data-stu-id="e3663-164">By default, SQL Data Warehouse stores hello table as a clustered columnstore index.</span></span> <span data-ttu-id="e3663-165">Após a conclusão de uma carga, algumas das linhas de dados de saudação não podem ser compactadas no Olá columnstore.</span><span class="sxs-lookup"><span data-stu-id="e3663-165">After a load completes, some of hello data rows might not be compressed into hello columnstore.</span></span>  <span data-ttu-id="e3663-166">Há várias razões para isso acontecer.</span><span class="sxs-lookup"><span data-stu-id="e3663-166">There's a variety of reasons why this can happen.</span></span> <span data-ttu-id="e3663-167">mais, consulte toolearn [gerenciar índices de columnstore][manage columnstore indexes].</span><span class="sxs-lookup"><span data-stu-id="e3663-167">toolearn more, see [manage columnstore indexes][manage columnstore indexes].</span></span>

<span data-ttu-id="e3663-168">consulta de toooptimize desempenho e compactação columnstore depois de uma carga recriar Olá tabela tooforce Olá columnstore index toocompress todas as linhas de saudação.</span><span class="sxs-lookup"><span data-stu-id="e3663-168">toooptimize query performance and columnstore compression after a load, rebuild hello table tooforce hello columnstore index toocompress all hello rows.</span></span>

```sql

ALTER INDEX ALL ON [dbo].[DimProduct] REBUILD;

```

<span data-ttu-id="e3663-169">Para obter mais informações sobre como manter os índices columnstore, consulte Olá [gerenciar índices de columnstore] [ manage columnstore indexes] artigo.</span><span class="sxs-lookup"><span data-stu-id="e3663-169">For more information on maintaining columnstore indexes, see hello [manage columnstore indexes][manage columnstore indexes] article.</span></span>

## <a name="optimize-statistics"></a><span data-ttu-id="e3663-170">Otimizar estatísticas</span><span class="sxs-lookup"><span data-stu-id="e3663-170">Optimize statistics</span></span>
<span data-ttu-id="e3663-171">É melhor estatísticas de coluna única toocreate imediatamente após uma carga.</span><span class="sxs-lookup"><span data-stu-id="e3663-171">It is best toocreate single-column statistics immediately after a load.</span></span> <span data-ttu-id="e3663-172">Há algumas opções de estatísticas.</span><span class="sxs-lookup"><span data-stu-id="e3663-172">There are some choices for statistics.</span></span> <span data-ttu-id="e3663-173">Por exemplo, se você criar estatísticas de coluna única em todas as colunas pode levar um longo tempo toorebuild todas as estatísticas de saudação.</span><span class="sxs-lookup"><span data-stu-id="e3663-173">For example, if you create single-column statistics on every column it might take a long time toorebuild all hello statistics.</span></span> <span data-ttu-id="e3663-174">Se você souber que determinadas colunas não serão toobe em predicados de consulta, você pode ignorar a criação de estatísticas nessas colunas.</span><span class="sxs-lookup"><span data-stu-id="e3663-174">If you know certain columns are not going toobe in query predicates, you can skip creating statistics on those columns.</span></span>

<span data-ttu-id="e3663-175">Se você decidir toocreate estatísticas de coluna única em todas as colunas de cada tabela, você pode usar o exemplo de código do procedimento armazenado hello `prc_sqldw_create_stats` em Olá [estatísticas] [ statistics] artigo.</span><span class="sxs-lookup"><span data-stu-id="e3663-175">If you decide toocreate single-column statistics on every column of every table, you can use hello stored procedure code sample `prc_sqldw_create_stats` in hello [statistics][statistics] article.</span></span>

<span data-ttu-id="e3663-176">saudação de exemplo a seguir é um bom ponto de partida para a criação de estatísticas.</span><span class="sxs-lookup"><span data-stu-id="e3663-176">hello following example is a good starting point for creating statistics.</span></span> <span data-ttu-id="e3663-177">Cria estatísticas de coluna única em cada coluna na tabela de dimensões hello e em cada coluna de junção em tabelas de fatos hello.</span><span class="sxs-lookup"><span data-stu-id="e3663-177">It creates single-column statistics on each column in hello dimension table, and on each joining column in hello fact tables.</span></span> <span data-ttu-id="e3663-178">Você sempre poderá adicionar colunas de tabela de fatos única ou várias colunas de estatísticas tooother posteriormente.</span><span class="sxs-lookup"><span data-stu-id="e3663-178">You can always add single or multi-column statistics tooother fact table columns later on.</span></span>


## <a name="achievement-unlocked"></a><span data-ttu-id="e3663-179">Missão cumprida!</span><span class="sxs-lookup"><span data-stu-id="e3663-179">Achievement unlocked!</span></span>
<span data-ttu-id="e3663-180">Você carregou com êxito os dados no SQL Data Warehouse do Azure.</span><span class="sxs-lookup"><span data-stu-id="e3663-180">You have successfully loaded data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="e3663-181">Bom trabalho!</span><span class="sxs-lookup"><span data-stu-id="e3663-181">Great job!</span></span>

##<a name="next-steps"></a><span data-ttu-id="e3663-182">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e3663-182">Next Steps</span></span>
<span data-ttu-id="e3663-183">Carregamento de dados é Olá de primeira etapa toodeveloping uma solução de depósito de dados usando o SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="e3663-183">Loading data is hello first step toodeveloping a data warehouse solution using SQL Data Warehouse.</span></span> <span data-ttu-id="e3663-184">Confira nossos recursos de desenvolvimento em [Tabelas](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-tables-overview) e [T-SQL](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-develop-loops.md).</span><span class="sxs-lookup"><span data-stu-id="e3663-184">Check out our development resources on [Tables](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-tables-overview) and [T-SQL](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-develop-loops.md).</span></span>


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
[CREATE EXTERNAL DATA SOURCE]: https://msdn.microsoft.com/library/dn935022.aspx
[CREATE EXTERNAL FILE FORMAT]: https://msdn.microsoft.com/library/dn935026.aspx
[CREATE TABLE AS SELECT (Transact-SQL)]: https://msdn.microsoft.com/library/mt204041.aspx
[sys.dm_pdw_exec_requests]: https://msdn.microsoft.com/library/mt203887.aspx
[REBUILD]: https://msdn.microsoft.com/library/ms188388.aspx

<!--Other Web references-->
[Microsoft Download Center]: http://www.microsoft.com/download/details.aspx?id=36433
[Load hello full Contoso Retail Data Warehouse]: https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/contoso-data-warehouse/readme.md
