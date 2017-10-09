---
title: aaaPolyBase no Tutorial do SQL Data Warehouse | Microsoft Docs
description: "Saiba o que é o PolyBase e como toouse para cenários de data warehouse."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: 0a0103b4-ddd6-4d1e-87be-4965d6e99f3f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 03/01/2017
ms.author: cakarst;barbkess
ms.openlocfilehash: 3e680ec407c1d920dd59ea922b82c9208b5e9a84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-with-polybase-in-sql-data-warehouse"></a><span data-ttu-id="223df-103">Carregar dados com o PolyBase no SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="223df-103">Load data with PolyBase in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="223df-104">Redgate</span><span class="sxs-lookup"><span data-stu-id="223df-104">Redgate</span></span>](sql-data-warehouse-load-with-redgate.md)  
> * [<span data-ttu-id="223df-105">Fábrica de dados</span><span class="sxs-lookup"><span data-stu-id="223df-105">Data Factory</span></span>](sql-data-warehouse-get-started-load-with-azure-data-factory.md)  
> * [<span data-ttu-id="223df-106">PolyBase</span><span class="sxs-lookup"><span data-stu-id="223df-106">PolyBase</span></span>](sql-data-warehouse-get-started-load-with-polybase.md)  
> * [<span data-ttu-id="223df-107">BCP</span><span class="sxs-lookup"><span data-stu-id="223df-107">BCP</span></span>](sql-data-warehouse-load-with-bcp.md)
> 
> 

<span data-ttu-id="223df-108">Este tutorial mostra como os dados de tooload no SQL Data Warehouse usando PolyBase e o AzCopy.</span><span class="sxs-lookup"><span data-stu-id="223df-108">This tutorial shows how tooload data into SQL Data Warehouse using AzCopy and PolyBase.</span></span> <span data-ttu-id="223df-109">Quando terminar, você saberá como:</span><span class="sxs-lookup"><span data-stu-id="223df-109">When finished, you will know how to:</span></span>

* <span data-ttu-id="223df-110">Usar o armazenamento de blob AzCopy toocopy dados tooAzure</span><span class="sxs-lookup"><span data-stu-id="223df-110">Use AzCopy toocopy data tooAzure blob storage</span></span>
* <span data-ttu-id="223df-111">Criar objetos de banco de dados toodefine dados de saudação</span><span class="sxs-lookup"><span data-stu-id="223df-111">Create database objects toodefine hello data</span></span>
* <span data-ttu-id="223df-112">Execute uma consulta de T-SQL tooload Olá dados</span><span class="sxs-lookup"><span data-stu-id="223df-112">Run a T-SQL query tooload hello data</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-data-with-PolyBase-in-Azure-SQL-Data-Warehouse/player]
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="223df-113">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="223df-113">Prerequisites</span></span>
<span data-ttu-id="223df-114">toostep este tutorial, você precisa</span><span class="sxs-lookup"><span data-stu-id="223df-114">toostep through this tutorial, you need</span></span>

* <span data-ttu-id="223df-115">Um banco de dados do SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="223df-115">A SQL Data Warehouse database.</span></span>
* <span data-ttu-id="223df-116">Uma conta de armazenamento do Azure do tipo Padrão-LRS (Armazenamento com Redundância Local Padrão), Padrão-GRS (Armazenamento com Redundância Geográfica Padrão) ou Padrão-RAGRS (Armazenamento de Redundância Geográfica com Acesso de Leitura Padrão).</span><span class="sxs-lookup"><span data-stu-id="223df-116">An Azure storage account of type Standard Locally Redundant Storage (Standard-LRS), Standard Geo-Redundant Storage (Standard-GRS), or Standard Read-Access Geo-Redundant Storage (Standard-RAGRS).</span></span>
* <span data-ttu-id="223df-117">Utilitário de linha de comando AzCopy.</span><span class="sxs-lookup"><span data-stu-id="223df-117">AzCopy Command-Line Utility.</span></span> <span data-ttu-id="223df-118">Baixe e instale Olá [versão mais recente do AzCopy] [ latest version of AzCopy] que é instalado com hello ferramentas de armazenamento do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="223df-118">Download and install hello [latest version of AzCopy][latest version of AzCopy] which is installed with hello Microsoft Azure Storage Tools.</span></span>
  
    ![Ferramentas do Armazenamento do Azure](./media/sql-data-warehouse-get-started-load-with-polybase/install-azcopy.png)

## <a name="step-1-add-sample-data-tooazure-blob-storage"></a><span data-ttu-id="223df-120">Etapa 1: Adicionar o armazenamento de blob de tooAzure de dados de exemplo</span><span class="sxs-lookup"><span data-stu-id="223df-120">Step 1: Add sample data tooAzure blob storage</span></span>
<span data-ttu-id="223df-121">Dados de pedidos tooload, é preciso tooput alguns dados de exemplo em um armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="223df-121">In order tooload data, we need tooput some sample data into an Azure blob storage.</span></span> <span data-ttu-id="223df-122">Nesta etapa, preencheremos um blob do Armazenamento do Azure com dados de exemplo.</span><span class="sxs-lookup"><span data-stu-id="223df-122">In this step we populate an Azure Storage blob with sample data.</span></span> <span data-ttu-id="223df-123">Posteriormente, usaremos PolyBase tooload esses dados de exemplo em seu banco de dados do SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="223df-123">Later, we will use PolyBase tooload this sample data into your SQL Data Warehouse database.</span></span>

### <a name="a-prepare-a-sample-text-file"></a><span data-ttu-id="223df-124">R.</span><span class="sxs-lookup"><span data-stu-id="223df-124">A.</span></span> <span data-ttu-id="223df-125">Preparar um arquivo de texto de exemplo</span><span class="sxs-lookup"><span data-stu-id="223df-125">Prepare a sample text file</span></span>
<span data-ttu-id="223df-126">tooprepare um arquivo de texto de exemplo:</span><span class="sxs-lookup"><span data-stu-id="223df-126">tooprepare a sample text file:</span></span>

1. <span data-ttu-id="223df-127">Abra o bloco de notas e copie Olá linhas de dados a seguir em um novo arquivo.</span><span class="sxs-lookup"><span data-stu-id="223df-127">Open Notepad and copy hello following lines of data into a new file.</span></span> <span data-ttu-id="223df-128">Salve esse diretório temporário local de tooyour como temp%\DimDate2.txt %.</span><span class="sxs-lookup"><span data-stu-id="223df-128">Save this tooyour local temp directory as %temp%\DimDate2.txt.</span></span>

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

### <a name="b-find-your-blob-service-endpoint"></a><span data-ttu-id="223df-129">B.</span><span class="sxs-lookup"><span data-stu-id="223df-129">B.</span></span> <span data-ttu-id="223df-130">Localizar o ponto de extremidade do serviço blob</span><span class="sxs-lookup"><span data-stu-id="223df-130">Find your blob service endpoint</span></span>
<span data-ttu-id="223df-131">toofind seu ponto de extremidade do serviço blob:</span><span class="sxs-lookup"><span data-stu-id="223df-131">toofind your blob service endpoint:</span></span>

1. <span data-ttu-id="223df-132">Olá Portal do Azure selecione **procurar** > **contas de armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="223df-132">From hello Azure Portal select **Browse** > **Storage Accounts**.</span></span>
2. <span data-ttu-id="223df-133">Clique na conta de armazenamento Olá que deseja toouse.</span><span class="sxs-lookup"><span data-stu-id="223df-133">Click hello storage account you want toouse.</span></span>
3. <span data-ttu-id="223df-134">Na folha de conta de armazenamento de saudação, clique em Blobs</span><span class="sxs-lookup"><span data-stu-id="223df-134">In hello Storage account blade, click Blobs</span></span>
   
    ![Clicar em Blobs](./media/sql-data-warehouse-get-started-load-with-polybase/click-blobs.png)
4. <span data-ttu-id="223df-136">Salve a URL do ponto de extremidade do serviço blob para mais tarde.</span><span class="sxs-lookup"><span data-stu-id="223df-136">Save your blob service endpoint URL for later.</span></span>
   
    ![Ponto de extremidade do serviço blob](./media/sql-data-warehouse-get-started-load-with-polybase/blob-service.png)

### <a name="c-find-your-azure-storage-key"></a><span data-ttu-id="223df-138">C.</span><span class="sxs-lookup"><span data-stu-id="223df-138">C.</span></span> <span data-ttu-id="223df-139">Encontrar a chave de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="223df-139">Find your Azure storage key</span></span>
<span data-ttu-id="223df-140">toofind sua chave de armazenamento do Azure:</span><span class="sxs-lookup"><span data-stu-id="223df-140">toofind your Azure storage key:</span></span>

1. <span data-ttu-id="223df-141">Olá Portal do Azure, selecione **procurar** > **contas de armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="223df-141">From hello Azure Portal, select **Browse** > **Storage Accounts**.</span></span>
2. <span data-ttu-id="223df-142">Clique na conta de armazenamento Olá que toouse desejado.</span><span class="sxs-lookup"><span data-stu-id="223df-142">Click on hello storage account you want toouse.</span></span>
3. <span data-ttu-id="223df-143">Selecione **Todas as configurações** > **Chaves de acesso**.</span><span class="sxs-lookup"><span data-stu-id="223df-143">Select **All settings** > **Access keys**.</span></span>
4. <span data-ttu-id="223df-144">Clique em Olá cópia caixa toocopy uma área de transferência do toohello chaves de acesso.</span><span class="sxs-lookup"><span data-stu-id="223df-144">Click hello copy box toocopy one of your access keys toohello clipboard.</span></span>
   
    ![Copiar a chave de armazenamento do Azure](./media/sql-data-warehouse-get-started-load-with-polybase/access-key.png)

### <a name="d-copy-hello-sample-file-tooazure-blob-storage"></a><span data-ttu-id="223df-146">D.</span><span class="sxs-lookup"><span data-stu-id="223df-146">D.</span></span> <span data-ttu-id="223df-147">Copiar o armazenamento de blob tooAzure do arquivo de exemplo hello</span><span class="sxs-lookup"><span data-stu-id="223df-147">Copy hello sample file tooAzure blob storage</span></span>
<span data-ttu-id="223df-148">toocopy seu armazenamento de blob de tooAzure de dados:</span><span class="sxs-lookup"><span data-stu-id="223df-148">toocopy your data tooAzure blob storage:</span></span>

1. <span data-ttu-id="223df-149">Abra um prompt de comando e altere o diretório de instalação do diretórios toohello AzCopy.</span><span class="sxs-lookup"><span data-stu-id="223df-149">Open a command prompt, and change directories toohello AzCopy installation directory.</span></span> <span data-ttu-id="223df-150">Esse comando altera o diretório de instalação padrão toohello em um cliente do Windows de 64 bits.</span><span class="sxs-lookup"><span data-stu-id="223df-150">This command changes toohello default installation directory on a 64-bit Windows client.</span></span>
   
    ```
    cd /d "%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy"
    ```
2. <span data-ttu-id="223df-151">Execute Olá arquivo de saudação do comando tooupload a seguir.</span><span class="sxs-lookup"><span data-stu-id="223df-151">Run hello following command tooupload hello file.</span></span> <span data-ttu-id="223df-152">Especifique a URL do ponto de extremidade de serviço blob para <blob service endpoint URL> e sua chave da conta de armazenamento do Azure para <azure_storage_account_key>.</span><span class="sxs-lookup"><span data-stu-id="223df-152">Specify your blob service endpoint URL for <blob service endpoint URL> and your Azure storage account key for <azure_storage_account_key>.</span></span>
   
    ```
    .\AzCopy.exe /Source:C:\Temp\ /Dest:<blob service endpoint URL> /datacontainer/datedimension/ /DestKey:<azure_storage_account_key> /Pattern:DimDate2.txt
    ```

<span data-ttu-id="223df-153">Consulte também [guia de Introdução com hello o utilitário de linha de comando AzCopy][Getting Started with hello AzCopy Command-Line Utility].</span><span class="sxs-lookup"><span data-stu-id="223df-153">See also [Getting Started with hello AzCopy Command-Line Utility][Getting Started with hello AzCopy Command-Line Utility].</span></span>

### <a name="e-explore-your-blob-storage-container"></a><span data-ttu-id="223df-154">E.</span><span class="sxs-lookup"><span data-stu-id="223df-154">E.</span></span> <span data-ttu-id="223df-155">Explorar o contêiner de armazenamento de blobs</span><span class="sxs-lookup"><span data-stu-id="223df-155">Explore your blob storage container</span></span>
<span data-ttu-id="223df-156">arquivo de saudação toosee carregado tooblob armazenamento:</span><span class="sxs-lookup"><span data-stu-id="223df-156">toosee hello file you uploaded tooblob storage:</span></span>

1. <span data-ttu-id="223df-157">Volte tooyour folha de serviço de Blob.</span><span class="sxs-lookup"><span data-stu-id="223df-157">Go back tooyour Blob service blade.</span></span>
2. <span data-ttu-id="223df-158">Em Contêineres, clique duas vezes em **datacontainer**.</span><span class="sxs-lookup"><span data-stu-id="223df-158">Under Containers, double-click **datacontainer**.</span></span>
3. <span data-ttu-id="223df-159">dados de tooyour do tooexplore Olá caminho, clique em pasta Olá **datedimension** e você verá o arquivo carregado **DimDate2.txt**.</span><span class="sxs-lookup"><span data-stu-id="223df-159">tooexplore hello path tooyour data, click hello folder **datedimension** and you will see your uploaded file **DimDate2.txt**.</span></span>
4. <span data-ttu-id="223df-160">Clique em Propriedades de tooview **DimDate2.txt**.</span><span class="sxs-lookup"><span data-stu-id="223df-160">tooview properties, click **DimDate2.txt**.</span></span>
5. <span data-ttu-id="223df-161">Observe que, na folha de propriedades de Blob hello, você pode baixar ou excluir o arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="223df-161">Note that in hello Blob properties blade, you can download or delete hello file.</span></span>
   
    ![Exibir o blob de armazenamento do Azure](./media/sql-data-warehouse-get-started-load-with-polybase/view-blob.png)

## <a name="step-2-create-an-external-table-for-hello-sample-data"></a><span data-ttu-id="223df-163">Etapa 2: Criar uma tabela externa para dados de exemplo hello</span><span class="sxs-lookup"><span data-stu-id="223df-163">Step 2: Create an external table for hello sample data</span></span>
<span data-ttu-id="223df-164">Nesta seção, criamos uma tabela externa que define os dados de exemplo hello.</span><span class="sxs-lookup"><span data-stu-id="223df-164">In this section we create an external table that defines hello sample data.</span></span>

<span data-ttu-id="223df-165">PolyBase usa dados de tooaccess tabelas externas no armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="223df-165">PolyBase uses external tables tooaccess data in Azure blob storage.</span></span> <span data-ttu-id="223df-166">Como Olá dados não são armazenados no SQL Data Warehouse, o PolyBase manipula dados externos de toohello de autenticação usando uma credencial no escopo do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="223df-166">Since hello data is not stored within SQL Data Warehouse, PolyBase handles authentication toohello external data by using a database-scoped credential.</span></span>

<span data-ttu-id="223df-167">exemplo Hello nesta etapa usa essas instruções de Transact-SQL toocreate uma tabela externa.</span><span class="sxs-lookup"><span data-stu-id="223df-167">hello example in this step uses these Transact-SQL statements toocreate an external table.</span></span>

* <span data-ttu-id="223df-168">[Create Master Key (Transact-SQL)] [ Create Master Key (Transact-SQL)] tooencrypt segredo de saudação do banco de dados de credencial com escopo.</span><span class="sxs-lookup"><span data-stu-id="223df-168">[Create Master Key (Transact-SQL)][Create Master Key (Transact-SQL)] tooencrypt hello secret of your database scoped credential.</span></span>
* <span data-ttu-id="223df-169">[Criar credencial no escopo do banco de dados (Transact-SQL)] [ Create Database Scoped Credential (Transact-SQL)] toospecify informações de autenticação para sua conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="223df-169">[Create Database Scoped Credential (Transact-SQL)][Create Database Scoped Credential (Transact-SQL)] toospecify authentication information for your Azure storage account.</span></span>
* <span data-ttu-id="223df-170">[Criar fonte de dados externa (Transact-SQL)] [ Create External Data Source (Transact-SQL)] toospecify local de saudação do seu armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="223df-170">[Create External Data Source (Transact-SQL)][Create External Data Source (Transact-SQL)] toospecify hello location of your Azure blob storage.</span></span>
* <span data-ttu-id="223df-171">[Criar um formato de arquivo externo (Transact-SQL)] [ Create External File Format (Transact-SQL)] toospecify formato de saudação de seus dados.</span><span class="sxs-lookup"><span data-stu-id="223df-171">[Create External File Format (Transact-SQL)][Create External File Format (Transact-SQL)] toospecify hello format of your data.</span></span>
* <span data-ttu-id="223df-172">[Criar tabela externa (Transact-SQL)] [ Create External Table (Transact-SQL)] Olá a definição da tabela toospecify hello e o local de dados.</span><span class="sxs-lookup"><span data-stu-id="223df-172">[Create External Table (Transact-SQL)][Create External Table (Transact-SQL)] toospecify hello table definition and location of hello data.</span></span>

<span data-ttu-id="223df-173">Execute esta consulta no banco de dados do SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="223df-173">Run this query against your SQL Data Warehouse database.</span></span> <span data-ttu-id="223df-174">Ele cria uma tabela externa denominada DimDate2External no esquema dbo Olá que pontos de dados de exemplo DimDate2.txt toohello no armazenamento de BLOBs do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="223df-174">It will create an external table named DimDate2External in hello dbo schema that points toohello DimDate2.txt sample data in hello Azure blob storage.</span></span>

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


-- D: Create an external file format
-- FORMAT_TYPE: Type of file format in Azure storage (supported: DELIMITEDTEXT, RCFILE, ORC, PARQUET).
-- FORMAT_OPTIONS: Specify field terminator, string delimiter, date format etc. for delimited text files.
-- Specify DATA_COMPRESSION method if data is compressed.

CREATE EXTERNAL FILE FORMAT TextFile
WITH (
    FORMAT_TYPE = DelimitedText,
    FORMAT_OPTIONS (FIELD_TERMINATOR = ',')
);


-- E: Create hello external table
-- Specify column names and data types. This needs toomatch hello data in hello sample file.
-- LOCATION: Specify path toofile or directory that contains hello data (relative toohello blob container).
-- toopoint tooall files under hello blob container, use LOCATION='.'

CREATE EXTERNAL TABLE dbo.DimDate2External (
    DateId INT NOT NULL,
    CalendarQuarter TINYINT NOT NULL,
    FiscalQuarter TINYINT NOT NULL
)
WITH (
    LOCATION='/datedimension/',
    DATA_SOURCE=AzureStorage,
    FILE_FORMAT=TextFile
);


-- Run a query on hello external table

SELECT count(*) FROM dbo.DimDate2External;

```


<span data-ttu-id="223df-175">No Pesquisador de objetos SQL Server no Visual Studio, você pode ver o formato de arquivo externo hello, fonte de dados externa e tabela de DimDate2External hello.</span><span class="sxs-lookup"><span data-stu-id="223df-175">In SQL Server Object Explorer in Visual Studio, you can see hello external file format, external data source, and hello DimDate2External table.</span></span>

![Exibir tabela externa](./media/sql-data-warehouse-get-started-load-with-polybase/external-table.png)

## <a name="step-3-load-data-into-sql-data-warehouse"></a><span data-ttu-id="223df-177">Etapa 3: carregar dados no SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="223df-177">Step 3: Load data into SQL Data Warehouse</span></span>
<span data-ttu-id="223df-178">Depois de criar tabela externa hello, você pode carregar dados de saudação em uma nova tabela ou inseri-lo em uma tabela existente.</span><span class="sxs-lookup"><span data-stu-id="223df-178">Once hello external table is created, you can either load hello data into a new table or insert it into an existing table.</span></span>

* <span data-ttu-id="223df-179">dados de saudação tooload em uma nova tabela, executar Olá [CREATE TABLE AS SELECT (Transact-SQL)] [ CREATE TABLE AS SELECT (Transact-SQL)] instrução.</span><span class="sxs-lookup"><span data-stu-id="223df-179">tooload hello data into a new table, run hello [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)] statement.</span></span> <span data-ttu-id="223df-180">nova tabela de saudação terá colunas Olá nomeadas na consulta de saudação.</span><span class="sxs-lookup"><span data-stu-id="223df-180">hello new table will have hello columns named in hello query.</span></span> <span data-ttu-id="223df-181">tipos de dados de saudação de colunas de saudação corresponderá a tipos de dados de saudação na definição de tabela externa hello.</span><span class="sxs-lookup"><span data-stu-id="223df-181">hello data types of hello columns will match hello data types in hello external table definition.</span></span>
* <span data-ttu-id="223df-182">dados de saudação tooload em uma tabela existente, use Olá [INSERT... SELECT (Transact-SQL)] [ INSERT...SELECT (Transact-SQL)] instrução.</span><span class="sxs-lookup"><span data-stu-id="223df-182">tooload hello data into an existing table, use hello [INSERT...SELECT (Transact-SQL)][INSERT...SELECT (Transact-SQL)] statement.</span></span>

```sql
-- Load hello data from Azure blob storage tooSQL Data Warehouse

CREATE TABLE dbo.DimDate2
WITH
(   
    CLUSTERED COLUMNSTORE INDEX,
    DISTRIBUTION = ROUND_ROBIN
)
AS
SELECT * FROM [dbo].[DimDate2External];
```

## <a name="step-4-create-statistics-on-your-newly-loaded-data"></a><span data-ttu-id="223df-183">Etapa 4: criar estatísticas sobre os dados recém-carregados</span><span class="sxs-lookup"><span data-stu-id="223df-183">Step 4: Create statistics on your newly loaded data</span></span>
<span data-ttu-id="223df-184">O SQL Data Warehouse do Azure ainda não dá suporte a estatísticas de criação ou de atualização automática.</span><span class="sxs-lookup"><span data-stu-id="223df-184">SQL Data Warehouse does not auto-create or auto-update statistics.</span></span> <span data-ttu-id="223df-185">Portanto, tooachieve alto desempenho de consultas, é importante primeiro carregar toocreate estatísticas em cada coluna de cada tabela após a saudação.</span><span class="sxs-lookup"><span data-stu-id="223df-185">Therefore, tooachieve high query performance, it's important toocreate statistics on each column of each table after hello first load.</span></span> <span data-ttu-id="223df-186">Também é importante tooupdate estatísticas após alterações significativas nos dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="223df-186">It's also important tooupdate statistics after substantial changes in hello data.</span></span>

<span data-ttu-id="223df-187">Este exemplo cria estatísticas de coluna única na nova tabela de DimDate2 hello.</span><span class="sxs-lookup"><span data-stu-id="223df-187">This example creates single-column statistics on hello new DimDate2 table.</span></span>

```sql
CREATE STATISTICS [DateId] on [DimDate2] ([DateId]);
CREATE STATISTICS [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
CREATE STATISTICS [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
```

<span data-ttu-id="223df-188">mais, consulte toolearn [estatísticas][Statistics].</span><span class="sxs-lookup"><span data-stu-id="223df-188">toolearn more, see [Statistics][Statistics].</span></span>  

## <a name="next-steps"></a><span data-ttu-id="223df-189">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="223df-189">Next steps</span></span>
<span data-ttu-id="223df-190">Consulte Olá [guia do PolyBase] [ PolyBase guide] para obter mais informações que você deve saber como desenvolver uma solução que usa o PolyBase.</span><span class="sxs-lookup"><span data-stu-id="223df-190">See hello [PolyBase guide][PolyBase guide] for further information you should know as you develop a solution that uses PolyBase.</span></span>

<!--Image references-->


<!--Article references-->
[PolyBase in SQL Data Warehouse Tutorial]: ./sql-data-warehouse-get-started-load-with-polybase.md
[Load data with bcp]: ./sql-data-warehouse-load-with-bcp.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[PolyBase guide]: ./sql-data-warehouse-load-polybase-guide.md
[Getting Started with hello AzCopy Command-Line Utility]:../storage/common/storage-use-azcopy.md
[latest version of AzCopy]:../storage/common/storage-use-azcopy.md

<!--External references-->
[supported source/sink]: https://msdn.microsoft.com/library/dn894007.aspx
[copy activity]: https://msdn.microsoft.com/library/dn835035.aspx
[SQL Server destination adapter]: https://msdn.microsoft.com/library/ms141095.aspx
[SSIS]: https://msdn.microsoft.com/library/ms141026.aspx


[CREATE EXTERNAL DATA SOURCE (Transact-SQL)]:https://msdn.microsoft.com/library/dn935022.aspx
[CREATE EXTERNAL FILE FORMAT (Transact-SQL)]:https://msdn.microsoft.com/library/dn935026.aspx
[CREATE EXTERNAL TABLE (Transact-SQL)]:https://msdn.microsoft.com/library/dn935021.aspx

[DROP EXTERNAL DATA SOURCE (Transact-SQL)]:https://msdn.microsoft.com/library/mt146367.aspx
[DROP EXTERNAL FILE FORMAT (Transact-SQL)]:https://msdn.microsoft.com/library/mt146379.aspx
[DROP EXTERNAL TABLE (Transact-SQL)]:https://msdn.microsoft.com/library/mt130698.aspx

[CREATE TABLE AS SELECT (Transact-SQL)]:https://msdn.microsoft.com/library/mt204041.aspx
[INSERT...SELECT (Transact-SQL)]:https://msdn.microsoft.com/library/ms174335.aspx
[CREATE MASTER KEY (Transact-SQL)]:https://msdn.microsoft.com/library/ms174382.aspx
[CREATE CREDENTIAL (Transact-SQL)]:https://msdn.microsoft.com/library/ms189522.aspx
[CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL)]:https://msdn.microsoft.com/library/mt270260.aspx
[DROP CREDENTIAL (Transact-SQL)]:https://msdn.microsoft.com/library/ms189450.aspx
