---
title: Carregar o Azure Data Lake Store para o SQL Data Warehouse | Microsoft Docs
description: Saiba como usar as tabelas externas do PolyBase para carregar dados do Azure Data Lake Store no SQL Data Warehouse do Azure.
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
ms.openlocfilehash: ab951c30aae0d4afdd931e245f25d4645bba1681
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="load-data-from-azure-data-lake-store-into-sql-data-warehouse"></a><span data-ttu-id="50653-103">Carregar dados do Azure Data Lake Store no SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="50653-103">Load data from Azure Data Lake Store into SQL Data Warehouse</span></span>
<span data-ttu-id="50653-104">Este documento fornece todas as etapas necessárias para carregar seus próprios dados do Azure Data Lake Store (ADLS) no SQL Data Warehouse usando o PolyBase.</span><span class="sxs-lookup"><span data-stu-id="50653-104">This document gives you all steps you  need to load your own data from Azure Data Lake Store (ADLS) into SQL Data Warehouse using PolyBase.</span></span>
<span data-ttu-id="50653-105">Embora você possa executar consultas ad hoc sobre os dados armazenados no ADLS usando as tabelas externas, recomendamos importar os dados para o SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="50653-105">While you are able to run adhoc queries over the data stored in ADLS using the External Tables, as a best practice we suggest importing the data into the SQL Data Warehouse.</span></span>
<span data-ttu-id="50653-106">Tempo previsto: 10 minutos, supondo que você tenha os pré-requisitos necessários.</span><span class="sxs-lookup"><span data-stu-id="50653-106">Time Estimate: 10 minutes assuming you have the prerequisites need to complete.</span></span>
<span data-ttu-id="50653-107">Neste tutorial, você aprenderá a:</span><span class="sxs-lookup"><span data-stu-id="50653-107">In this tutorial you will learn how to:</span></span>

1. <span data-ttu-id="50653-108">Crie objetos de banco de dados externo para carregar do Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="50653-108">Create External Database objects to load from Azure Data Lake Store.</span></span>
2. <span data-ttu-id="50653-109">Conecte-se a um diretório do Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="50653-109">Connect to an Azure Data Lake Store Directory.</span></span>
3. <span data-ttu-id="50653-110">Carregue os dados no SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="50653-110">Load data into Azure SQL Data Warehouse.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="50653-111">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="50653-111">Before you begin</span></span>
<span data-ttu-id="50653-112">Para este tutorial, você precisa do:</span><span class="sxs-lookup"><span data-stu-id="50653-112">To run this tutorial, you need:</span></span>

* <span data-ttu-id="50653-113">Aplicativo do Azure Active Directory para usar como autenticação de serviço a serviço.</span><span class="sxs-lookup"><span data-stu-id="50653-113">Azure Active Directory Application to use for Service-to-Service authentication.</span></span> <span data-ttu-id="50653-114">Para criar, siga a [Autenticação do Active Directory](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-authenticate-using-active-directory)</span><span class="sxs-lookup"><span data-stu-id="50653-114">To create, follow [Active directory authentication](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-authenticate-using-active-directory)</span></span>

>[!NOTE] 
> <span data-ttu-id="50653-115">Você precisa do ID do cliente, a chave e o valor do ponto de extremidade de Token OAuth2.0 do seu aplicativo do Active Directory para conectar-se no Azure Data Lake do SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="50653-115">You need the client ID, Key, and OAuth2.0 Token Endpoint Value of your Active Directory Application to connect to your Azure Data Lake from SQL Data Warehouse.</span></span> <span data-ttu-id="50653-116">Os detalhes de como obter esses valores estão no link acima.</span><span class="sxs-lookup"><span data-stu-id="50653-116">Details for how to get these values are in the link above.</span></span>
><span data-ttu-id="50653-117">Observação para registro do aplicativo do Azure Active Directory usa a “ID do aplicativo” como a ID do cliente.</span><span class="sxs-lookup"><span data-stu-id="50653-117">Note for Azure Active Directory App Registration use the 'Application ID' as the Client ID.</span></span>

* <span data-ttu-id="50653-118">SQL Server Management Studio ou do SQL Server Data Tools, para baixar o SSMS e conectar-se. Veja a [consulta SSMS](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-query-ssms)</span><span class="sxs-lookup"><span data-stu-id="50653-118">SQL Server Management Studio or SQL Server Data Tools, to download SSMS and connect see [Query SSMS](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-query-ssms)</span></span>

* <span data-ttu-id="50653-119">Um SQL Data Warehouse do Azure, para criar um siga as instruções em: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-get-started-provision</span><span class="sxs-lookup"><span data-stu-id="50653-119">An Azure SQL Data Warehouse, to create one follow: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-get-started-provision</span></span>

* <span data-ttu-id="50653-120">Um Azure Data Lake Store com ou sem a criptografia habilitada.</span><span class="sxs-lookup"><span data-stu-id="50653-120">An Azure Data Lake Store, with or without encryption enabled.</span></span> <span data-ttu-id="50653-121">Para criar um siga as instruções em: https://docs.microsoft.com/azure/data-lake-store/data-lake-store-get-started-portal</span><span class="sxs-lookup"><span data-stu-id="50653-121">To create one follow: https://docs.microsoft.com/azure/data-lake-store/data-lake-store-get-started-portal</span></span>




## <a name="configure-the-data-source"></a><span data-ttu-id="50653-122">Configurar a fonte de dados</span><span class="sxs-lookup"><span data-stu-id="50653-122">Configure the data source</span></span>
<span data-ttu-id="50653-123">O PolyBase usa objetos externos do T-SQL para definir o local e os atributos dos dados externos.</span><span class="sxs-lookup"><span data-stu-id="50653-123">PolyBase uses T-SQL external objects to define the location and attributes of the external data.</span></span> <span data-ttu-id="50653-124">Os objetos externos são armazenados no SQL Data Warehouse e fazem referência aos dados armazenados externamente.</span><span class="sxs-lookup"><span data-stu-id="50653-124">The external objects are stored in SQL Data Warehouse and reference the data th is stored externally.</span></span>


###  <a name="create-a-credential"></a><span data-ttu-id="50653-125">Criar uma credencial</span><span class="sxs-lookup"><span data-stu-id="50653-125">Create a credential</span></span>
<span data-ttu-id="50653-126">Para acessar o Azure Data Lake Store, você precisa criar uma chave mestra de banco de dados para criptografar seu segredo de credencial, que é usado na próxima etapa.</span><span class="sxs-lookup"><span data-stu-id="50653-126">To access your Azure Data Lake Store, you will need to create a Database Master Key to encrypt your credential secret used in the next step.</span></span>
<span data-ttu-id="50653-127">Então, você cria uma credencial com escopo de banco de dados, que armazena as credenciais de entidade de serviço configuradas no AAD.</span><span class="sxs-lookup"><span data-stu-id="50653-127">You then create a Database scoped credential, which stores the service principal credentials set up in AAD.</span></span> <span data-ttu-id="50653-128">Para aqueles que já usaram o PolyBase para se conectar ao Azure Storage Blob do Windows, observe que a sintaxe da credencial é diferente.</span><span class="sxs-lookup"><span data-stu-id="50653-128">For those of you who have used PolyBase to connect to Windows Azure Storage Blobs, note that the credential syntax is different.</span></span>
<span data-ttu-id="50653-129">Para se conectar ao armazenamento do Azure Data Lake Store, você deve **primeiro** criar um aplicativo do Azure Active Directory, criar uma tecla de acesso e conceder acesso de aplicativo para o recurso do Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="50653-129">To connect to Azure Data Lake Store, you must **first** create an Azure Active Directory Application, create an access key, and grant the application access to the Azure Data Lake resource.</span></span> <span data-ttu-id="50653-130">Instruções para executar essas etapas estão localizadas [aqui](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-authenticate-using-active-directory).</span><span class="sxs-lookup"><span data-stu-id="50653-130">Instrucitons to perform these steps are located [here](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-authenticate-using-active-directory).</span></span>

```sql
-- A: Create a Database Master Key.
-- Only necessary if one does not already exist.
-- Required to encrypt the credential secret in the next step.
-- For more information on Master Key: https://msdn.microsoft.com/en-us/library/ms174382.aspx?f=255&MSPPError=-2147217396

CREATE MASTER KEY;


-- B: Create a database scoped credential
-- IDENTITY: Pass the client id and OAuth 2.0 Token Endpoint taken from your Azure Active Directory Application
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


### <a name="create-the-external-data-source"></a><span data-ttu-id="50653-131">Criar a fonte de dados externa</span><span class="sxs-lookup"><span data-stu-id="50653-131">Create the external data source</span></span>
<span data-ttu-id="50653-132">Use este comando [CREATE EXTERNAL DATA SOURCE][CREATE EXTERNAL DATA SOURCE] para armazenar o local dos dados e o tipo de dados.</span><span class="sxs-lookup"><span data-stu-id="50653-132">Use this [CREATE EXTERNAL DATA SOURCE][CREATE EXTERNAL DATA SOURCE] command to store the location of the data, and the type of data.</span></span>
<span data-ttu-id="50653-133">Você pode encontrar o URI ADL no portal do Azure e em www.portal.azure.com.</span><span class="sxs-lookup"><span data-stu-id="50653-133">You can find the ADL URI in the Azure portal and www.portal.azure.com.</span></span>

```sql
-- C: Create an external data source
-- TYPE: HADOOP - PolyBase uses Hadoop APIs to access data in Azure Data Lake Store.
-- LOCATION: Provide Azure Data Lake accountname and URI
-- CREDENTIAL: Provide the credential created in the previous step.

CREATE EXTERNAL DATA SOURCE AzureDataLakeStore
WITH (
    TYPE = HADOOP,
    LOCATION = 'adl://<AzureDataLake account_name>.azuredatalakestore.net',
    CREDENTIAL = ADLCredential
);
```



## <a name="configure-data-format"></a><span data-ttu-id="50653-134">Configurar o formato de dados</span><span class="sxs-lookup"><span data-stu-id="50653-134">Configure data format</span></span>
<span data-ttu-id="50653-135">Para importar os dados do ADLS, você precisa especificar o formato de arquivo externo.</span><span class="sxs-lookup"><span data-stu-id="50653-135">To import the data from ADLS, you need to specify the external file format.</span></span> <span data-ttu-id="50653-136">Esse comando tem opções específicas de formato para descrever os seus dados.</span><span class="sxs-lookup"><span data-stu-id="50653-136">This command has format-specific options to describe your data.</span></span>
<span data-ttu-id="50653-137">O exemplo abaixo é um formato de arquivo normalmente usado que é um arquivo de texto delimitado por pipe.</span><span class="sxs-lookup"><span data-stu-id="50653-137">Below is an example of a commonly used file format that is a pipe-delimited text file.</span></span>
<span data-ttu-id="50653-138">A nossa documentação T-SQL possui uma lista completa para [CRIAR UM FORMATO DE ARQUIVO EXTERNO][CREATE EXTERNAL FILE FORMAT]</span><span class="sxs-lookup"><span data-stu-id="50653-138">Look at our T-SQL documentation for a complete list of [CREATE EXTERNAL FILE FORMAT][CREATE EXTERNAL FILE FORMAT]</span></span>

```sql
-- D: Create an external file format
-- FIELD_TERMINATOR: Marks the end of each field (column) in a delimited text file
-- STRING_DELIMITER: Specifies the field terminator for data of type string in the text-delimited file.
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

## <a name="create-the-external-tables"></a><span data-ttu-id="50653-139">Criar as tabelas externas</span><span class="sxs-lookup"><span data-stu-id="50653-139">Create the external tables</span></span>
<span data-ttu-id="50653-140">Agora que você especificou o formato do arquivo e da fonte de dados, você está pronto para criar as tabelas externas.</span><span class="sxs-lookup"><span data-stu-id="50653-140">Now that you have specified the data source and file format, you are ready to create the external tables.</span></span> <span data-ttu-id="50653-141">As tabelas externas servem para interagir com dados externos.</span><span class="sxs-lookup"><span data-stu-id="50653-141">External tables are how you interact with external data.</span></span> <span data-ttu-id="50653-142">O PolyBase usa a passagem de diretório recursiva para ler todos os arquivos em todos os subdiretórios do diretório especificado no parâmetro de local.</span><span class="sxs-lookup"><span data-stu-id="50653-142">PolyBase uses recursive directory traversal to read all files in all subdirectories of the directory specified in the location parameter.</span></span> <span data-ttu-id="50653-143">Além disso, o exemplo a seguir mostra como criar o objeto.</span><span class="sxs-lookup"><span data-stu-id="50653-143">Also, the following example shows how to create the object.</span></span> <span data-ttu-id="50653-144">Você precisa personalizar a instrução para trabalhar com os dados no ADLS.</span><span class="sxs-lookup"><span data-stu-id="50653-144">You need to customize the statement to work with the data you have in ADLS.</span></span>

```sql
-- D: Create an External Table
-- LOCATION: Folder under the ADLS root folder.
-- DATA_SOURCE: Specifies which Data Source Object to use.
-- FILE_FORMAT: Specifies which File Format Object to use
-- REJECT_TYPE: Specifies how you want to deal with rejected rows. Either Value or percentage of the total
-- REJECT_VALUE: Sets the Reject value based on the reject type.

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

## <a name="external-table-considerations"></a><span data-ttu-id="50653-145">Considerações sobre a tabela externa</span><span class="sxs-lookup"><span data-stu-id="50653-145">External Table Considerations</span></span>
<span data-ttu-id="50653-146">É fácil criar uma tabela externa, mas existem algumas nuances que precisam ser abordadas.</span><span class="sxs-lookup"><span data-stu-id="50653-146">Creating an external table is easy, but there are some nuances that need to be discussed.</span></span>

<span data-ttu-id="50653-147">O carregamento de dados com o PolyBase é fortemente tipado.</span><span class="sxs-lookup"><span data-stu-id="50653-147">Loading data with PolyBase is strongly typed.</span></span> <span data-ttu-id="50653-148">Isso significa que cada linha dos dados que estão sendo ingeridos deve atender à definição de esquema da tabela.</span><span class="sxs-lookup"><span data-stu-id="50653-148">This means that each row of the data being ingested must satisfy the table schema definition.</span></span>
<span data-ttu-id="50653-149">Se uma determinada linha não coincide com a definição de esquema, a linha é rejeitada da carga.</span><span class="sxs-lookup"><span data-stu-id="50653-149">If a given row does not match the schema definition, the row is rejected from the load.</span></span>

<span data-ttu-id="50653-150">As opções REJECT_TYPE e REJECT_VALUE permitem que você defina quantas linhas ou qual o percentual de dados deve estar presente na tabela final.</span><span class="sxs-lookup"><span data-stu-id="50653-150">The REJECT_TYPE and REJECT_VALUE options allow you to define how many rows or what percentage of the data must be present in the final table.</span></span>
<span data-ttu-id="50653-151">Durante o carregamento, se o valor rejeitado for atingido, o carregamento falha.</span><span class="sxs-lookup"><span data-stu-id="50653-151">During load, if the reject value is reached, the load fails.</span></span> <span data-ttu-id="50653-152">A causa mais comum de rejeição de linhas é uma incompatibilidade da definição do esquema.</span><span class="sxs-lookup"><span data-stu-id="50653-152">The most common cause of rejected rows is a schema definition mismatch.</span></span>
<span data-ttu-id="50653-153">Por exemplo, se uma coluna é especificada incorretamente para o esquema como inteiros, quando os dados no arquivo são de uma cadeia de caracteres, todas as linhas falham ao carregar.</span><span class="sxs-lookup"><span data-stu-id="50653-153">For example, if a column is incorrectly given the schema of int when the data in the file is a string, every row will fail to load.</span></span>

<span data-ttu-id="50653-154">O local especifica o diretório de nível superior cujos dados você deseja ler.</span><span class="sxs-lookup"><span data-stu-id="50653-154">The Location specifies the topmost directory that you want to read data from.</span></span>
<span data-ttu-id="50653-155">Nesse caso, se existem subdiretórios em /DimProduct/ o PolyBase importa todos os dados nos subdiretórios.</span><span class="sxs-lookup"><span data-stu-id="50653-155">In this case, if there were subdirectories under /DimProduct/ PolyBase would import all the data within the subdirectories.</span></span>

## <a name="load-the-data"></a><span data-ttu-id="50653-156">Carregar os dados</span><span class="sxs-lookup"><span data-stu-id="50653-156">Load the data</span></span>
<span data-ttu-id="50653-157">Para carregar dados do Azure Data Lake Store, use a instrução [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)].</span><span class="sxs-lookup"><span data-stu-id="50653-157">To load data from Azure Data Lake Store use the [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)] statement.</span></span> <span data-ttu-id="50653-158">Carregar com CTAS usa a tabela externa fortemente tipada que você criou.</span><span class="sxs-lookup"><span data-stu-id="50653-158">Loading with CTAS uses the strongly typed external table you have created.</span></span>

<span data-ttu-id="50653-159">O CTAS cria uma nova tabela e a preenche com os resultados de uma instrução select.</span><span class="sxs-lookup"><span data-stu-id="50653-159">CTAS creates a new table and populates it with the results of a select statement.</span></span> <span data-ttu-id="50653-160">CTAS define a nova tabela para ter as mesmas colunas e tipos de dados como os resultados da instrução select.</span><span class="sxs-lookup"><span data-stu-id="50653-160">CTAS defines the new table to have the same columns and data types as the results of the select statement.</span></span> <span data-ttu-id="50653-161">Se você selecionar todas as colunas de uma tabela externa, a nova tabela será uma réplica das colunas e dos tipos de dados na tabela externa.</span><span class="sxs-lookup"><span data-stu-id="50653-161">If you select all the columns from an external table, the new table is a replica of the columns and data types in the external table.</span></span>

<span data-ttu-id="50653-162">Neste exemplo, estamos criando uma tabela distribuída de hash chamada DimProduct da nossa tabela externa DimProduct_external.</span><span class="sxs-lookup"><span data-stu-id="50653-162">In this example, we are creating a hash distributed table called DimProduct from our External Table DimProduct_external.</span></span>

```sql

CREATE TABLE [dbo].[DimProduct]
WITH (DISTRIBUTION = HASH([ProductKey]  ) )
AS
SELECT * FROM [dbo].[DimProduct_external]
OPTION (LABEL = 'CTAS : Load [dbo].[DimProduct]');
```


## <a name="optimize-columnstore-compression"></a><span data-ttu-id="50653-163">Otimizar a compactação columnstore</span><span class="sxs-lookup"><span data-stu-id="50653-163">Optimize columnstore compression</span></span>
<span data-ttu-id="50653-164">Por padrão, o SQL Data Warehouse armazena a tabela como um índice columnstore clusterizado.</span><span class="sxs-lookup"><span data-stu-id="50653-164">By default, SQL Data Warehouse stores the table as a clustered columnstore index.</span></span> <span data-ttu-id="50653-165">Após a conclusão do carregamento, algumas das linhas de dados não podem ser compactadas no columnstore.</span><span class="sxs-lookup"><span data-stu-id="50653-165">After a load completes, some of the data rows might not be compressed into the columnstore.</span></span>  <span data-ttu-id="50653-166">Há várias razões para isso acontecer.</span><span class="sxs-lookup"><span data-stu-id="50653-166">There's a variety of reasons why this can happen.</span></span> <span data-ttu-id="50653-167">Para obter mais informações, confira [gerenciar índices columnstore][manage columnstore indexes].</span><span class="sxs-lookup"><span data-stu-id="50653-167">To learn more, see [manage columnstore indexes][manage columnstore indexes].</span></span>

<span data-ttu-id="50653-168">Para otimizar o desempenho da consulta e a compactação columnstore após um carregamento, recrie a tabela para forçar o índice columnstore a compactar todas as linhas.</span><span class="sxs-lookup"><span data-stu-id="50653-168">To optimize query performance and columnstore compression after a load, rebuild the table to force the columnstore index to compress all the rows.</span></span>

```sql

ALTER INDEX ALL ON [dbo].[DimProduct] REBUILD;

```

<span data-ttu-id="50653-169">Para obter mais informações sobre como manter os índices columnstore, confira o artigo [gerenciar índices columnstore][manage columnstore indexes].</span><span class="sxs-lookup"><span data-stu-id="50653-169">For more information on maintaining columnstore indexes, see the [manage columnstore indexes][manage columnstore indexes] article.</span></span>

## <a name="optimize-statistics"></a><span data-ttu-id="50653-170">Otimizar estatísticas</span><span class="sxs-lookup"><span data-stu-id="50653-170">Optimize statistics</span></span>
<span data-ttu-id="50653-171">É melhor criar estatísticas de coluna única imediatamente após um carregamento.</span><span class="sxs-lookup"><span data-stu-id="50653-171">It is best to create single-column statistics immediately after a load.</span></span> <span data-ttu-id="50653-172">Há algumas opções de estatísticas.</span><span class="sxs-lookup"><span data-stu-id="50653-172">There are some choices for statistics.</span></span> <span data-ttu-id="50653-173">Por exemplo, se você criar estatísticas de coluna única em todas as colunas, poderá levar muito tempo para recompilar todas as estatísticas.</span><span class="sxs-lookup"><span data-stu-id="50653-173">For example, if you create single-column statistics on every column it might take a long time to rebuild all the statistics.</span></span> <span data-ttu-id="50653-174">Se você souber que determinadas colunas não estarão em predicados de consulta, você poderá ignorar a criação de estatísticas nessas colunas.</span><span class="sxs-lookup"><span data-stu-id="50653-174">If you know certain columns are not going to be in query predicates, you can skip creating statistics on those columns.</span></span>

<span data-ttu-id="50653-175">Se você decidir criar estatísticas com uma coluna em cada coluna de cada tabela, poderá usar o exemplo de código do procedimento armazenado `prc_sqldw_create_stats` no artigo [estatísticas][statistics].</span><span class="sxs-lookup"><span data-stu-id="50653-175">If you decide to create single-column statistics on every column of every table, you can use the stored procedure code sample `prc_sqldw_create_stats` in the [statistics][statistics] article.</span></span>

<span data-ttu-id="50653-176">O exemplo a seguir é um bom ponto de partida para a criação de estatísticas.</span><span class="sxs-lookup"><span data-stu-id="50653-176">The following example is a good starting point for creating statistics.</span></span> <span data-ttu-id="50653-177">Ele cria estatísticas de coluna única em cada coluna na tabela de dimensões e em cada coluna de junção das tabelas de fatos.</span><span class="sxs-lookup"><span data-stu-id="50653-177">It creates single-column statistics on each column in the dimension table, and on each joining column in the fact tables.</span></span> <span data-ttu-id="50653-178">Você poderá adicionar estatísticas de coluna única ou múltipla às colunas de tabelas de fatos posteriormente.</span><span class="sxs-lookup"><span data-stu-id="50653-178">You can always add single or multi-column statistics to other fact table columns later on.</span></span>


## <a name="achievement-unlocked"></a><span data-ttu-id="50653-179">Missão cumprida!</span><span class="sxs-lookup"><span data-stu-id="50653-179">Achievement unlocked!</span></span>
<span data-ttu-id="50653-180">Você carregou com êxito os dados no SQL Data Warehouse do Azure.</span><span class="sxs-lookup"><span data-stu-id="50653-180">You have successfully loaded data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="50653-181">Bom trabalho!</span><span class="sxs-lookup"><span data-stu-id="50653-181">Great job!</span></span>

##<a name="next-steps"></a><span data-ttu-id="50653-182">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="50653-182">Next Steps</span></span>
<span data-ttu-id="50653-183">O carregamento de dados é a primeira etapa para desenvolver uma solução de data warehouse usando o SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="50653-183">Loading data is the first step to developing a data warehouse solution using SQL Data Warehouse.</span></span> <span data-ttu-id="50653-184">Confira nossos recursos de desenvolvimento em [Tabelas](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-tables-overview) e [T-SQL](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-develop-loops.md).</span><span class="sxs-lookup"><span data-stu-id="50653-184">Check out our development resources on [Tables](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-tables-overview) and [T-SQL](https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-develop-loops.md).</span></span>


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
[Load the full Contoso Retail Data Warehouse]: https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/contoso-data-warehouse/readme.md
