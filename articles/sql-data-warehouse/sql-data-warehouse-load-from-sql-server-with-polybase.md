---
title: dados de aaaLoad do SQL Server no Azure SQL Data Warehouse (PolyBase) | Microsoft Docs
description: "Usa bcp tooexport dados de arquivos de tooflat do SQL Server, o armazenamento de blob do AZCopy tooimport dados tooAzure e dados Olá tooingest no Azure SQL Data Warehouse."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: 860c86e0-90f7-492c-9a84-1bdd3d1735cd
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 1346fb016e0538a44426671bf4e29358cb24f7ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-with-polybase-in-sql-data-warehouse"></a><span data-ttu-id="b2166-103">Carregar dados com o PolyBase no SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="b2166-103">Load data with PolyBase in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b2166-104">SSIS</span><span class="sxs-lookup"><span data-stu-id="b2166-104">SSIS</span></span>](sql-data-warehouse-load-from-sql-server-with-integration-services.md)
> * [<span data-ttu-id="b2166-105">PolyBase</span><span class="sxs-lookup"><span data-stu-id="b2166-105">PolyBase</span></span>](sql-data-warehouse-load-from-sql-server-with-polybase.md)
> * [<span data-ttu-id="b2166-106">bcp</span><span class="sxs-lookup"><span data-stu-id="b2166-106">bcp</span></span>](sql-data-warehouse-load-from-sql-server-with-bcp.md)
> 
> 

<span data-ttu-id="b2166-107">Este tutorial mostra como dados tooload no SQL Data Warehouse usando AzCopy e PolyBase.</span><span class="sxs-lookup"><span data-stu-id="b2166-107">This tutorial shows how tooload data into SQL Data Warehouse by using AzCopy and PolyBase.</span></span> <span data-ttu-id="b2166-108">Quando terminar, você saberá como:</span><span class="sxs-lookup"><span data-stu-id="b2166-108">When finished, you will know how to:</span></span>

* <span data-ttu-id="b2166-109">Usar o armazenamento de blob AzCopy toocopy dados tooAzure</span><span class="sxs-lookup"><span data-stu-id="b2166-109">Use AzCopy toocopy data tooAzure blob storage</span></span>
* <span data-ttu-id="b2166-110">Criar objetos de banco de dados toodefine dados de saudação</span><span class="sxs-lookup"><span data-stu-id="b2166-110">Create database objects toodefine hello data</span></span>
* <span data-ttu-id="b2166-111">Execute uma consulta de T-SQL tooload Olá dados</span><span class="sxs-lookup"><span data-stu-id="b2166-111">Run a T-SQL query tooload hello data</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-data-with-PolyBase-in-Azure-SQL-Data-Warehouse/player]
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="b2166-112">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="b2166-112">Prerequisites</span></span>
<span data-ttu-id="b2166-113">toostep este tutorial, você precisa</span><span class="sxs-lookup"><span data-stu-id="b2166-113">toostep through this tutorial, you need</span></span>

* <span data-ttu-id="b2166-114">Um banco de dados do SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="b2166-114">A SQL Data Warehouse database.</span></span>
* <span data-ttu-id="b2166-115">Uma conta de armazenamento do Azure do tipo Padrão-LRS (Armazenamento com Redundância Local Padrão), Padrão-GRS (Armazenamento com Redundância Geográfica Padrão) ou Padrão-RAGRS (Armazenamento de Redundância Geográfica com Acesso de Leitura Padrão).</span><span class="sxs-lookup"><span data-stu-id="b2166-115">An Azure storage account of type Standard Locally Redundant Storage (Standard-LRS), Standard Geo-Redundant Storage (Standard-GRS), or Standard Read-Access Geo-Redundant Storage (Standard-RAGRS).</span></span>
* <span data-ttu-id="b2166-116">Utilitário de linha de comando AzCopy.</span><span class="sxs-lookup"><span data-stu-id="b2166-116">AzCopy Command-Line Utility.</span></span> <span data-ttu-id="b2166-117">Baixe e instale Olá [versão mais recente do AzCopy] [ latest version of AzCopy] que é instalado com hello ferramentas de armazenamento do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="b2166-117">Download and install hello [latest version of AzCopy][latest version of AzCopy] which is installed with hello Microsoft Azure Storage Tools.</span></span>
  
    ![Ferramentas do Armazenamento do Azure](./media/sql-data-warehouse-get-started-load-with-polybase/install-azcopy.png)

## <a name="step-1-add-sample-data-tooazure-blob-storage"></a><span data-ttu-id="b2166-119">Etapa 1: Adicionar o armazenamento de blob de tooAzure de dados de exemplo</span><span class="sxs-lookup"><span data-stu-id="b2166-119">Step 1: Add sample data tooAzure blob storage</span></span>
<span data-ttu-id="b2166-120">Dados de pedidos tooload, é preciso tooput alguns dados de exemplo em um armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="b2166-120">In order tooload data, we need tooput some sample data into an Azure blob storage.</span></span> <span data-ttu-id="b2166-121">Nesta etapa, preencheremos um blob do Armazenamento do Azure com dados de exemplo.</span><span class="sxs-lookup"><span data-stu-id="b2166-121">In this step we populate an Azure Storage blob with sample data.</span></span> <span data-ttu-id="b2166-122">Posteriormente, usaremos PolyBase tooload esses dados de exemplo em seu banco de dados do SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="b2166-122">Later, we will use PolyBase tooload this sample data into your SQL Data Warehouse database.</span></span>

### <a name="a-prepare-a-sample-text-file"></a><span data-ttu-id="b2166-123">R.</span><span class="sxs-lookup"><span data-stu-id="b2166-123">A.</span></span> <span data-ttu-id="b2166-124">Preparar um arquivo de texto de exemplo</span><span class="sxs-lookup"><span data-stu-id="b2166-124">Prepare a sample text file</span></span>
<span data-ttu-id="b2166-125">tooprepare um arquivo de texto de exemplo:</span><span class="sxs-lookup"><span data-stu-id="b2166-125">tooprepare a sample text file:</span></span>

1. <span data-ttu-id="b2166-126">Abra o bloco de notas e copie Olá linhas de dados a seguir em um novo arquivo.</span><span class="sxs-lookup"><span data-stu-id="b2166-126">Open Notepad and copy hello following lines of data into a new file.</span></span> <span data-ttu-id="b2166-127">Salve esse diretório temporário local de tooyour como temp%\DimDate2.txt %.</span><span class="sxs-lookup"><span data-stu-id="b2166-127">Save this tooyour local temp directory as %temp%\DimDate2.txt.</span></span>

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

### <a name="b-find-your-blob-service-endpoint"></a><span data-ttu-id="b2166-128">B.</span><span class="sxs-lookup"><span data-stu-id="b2166-128">B.</span></span> <span data-ttu-id="b2166-129">Localizar o ponto de extremidade do serviço blob</span><span class="sxs-lookup"><span data-stu-id="b2166-129">Find your blob service endpoint</span></span>
<span data-ttu-id="b2166-130">toofind seu ponto de extremidade do serviço blob:</span><span class="sxs-lookup"><span data-stu-id="b2166-130">toofind your blob service endpoint:</span></span>

1. <span data-ttu-id="b2166-131">Olá Portal do Azure selecione **procurar** > **contas de armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="b2166-131">From hello Azure Portal select **Browse** > **Storage Accounts**.</span></span>
2. <span data-ttu-id="b2166-132">Clique na conta de armazenamento Olá que deseja toouse.</span><span class="sxs-lookup"><span data-stu-id="b2166-132">Click hello storage account you want toouse.</span></span>
3. <span data-ttu-id="b2166-133">Na folha de conta de armazenamento de saudação, clique em Blobs</span><span class="sxs-lookup"><span data-stu-id="b2166-133">In hello Storage account blade, click Blobs</span></span>
   
    ![Clicar em Blobs](./media/sql-data-warehouse-get-started-load-with-polybase/click-blobs.png)
4. <span data-ttu-id="b2166-135">Salve a URL do ponto de extremidade do serviço blob para mais tarde.</span><span class="sxs-lookup"><span data-stu-id="b2166-135">Save your blob service endpoint URL for later.</span></span>
   
    ![Ponto de extremidade do serviço blob](./media/sql-data-warehouse-get-started-load-with-polybase/blob-service.png)

### <a name="c-find-your-azure-storage-key"></a><span data-ttu-id="b2166-137">C.</span><span class="sxs-lookup"><span data-stu-id="b2166-137">C.</span></span> <span data-ttu-id="b2166-138">Encontrar a chave de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="b2166-138">Find your Azure storage key</span></span>
<span data-ttu-id="b2166-139">toofind sua chave de armazenamento do Azure:</span><span class="sxs-lookup"><span data-stu-id="b2166-139">toofind your Azure storage key:</span></span>

1. <span data-ttu-id="b2166-140">Olá Portal do Azure, selecione **procurar** > **contas de armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="b2166-140">From hello Azure Portal, select **Browse** > **Storage Accounts**.</span></span>
2. <span data-ttu-id="b2166-141">Clique na conta de armazenamento Olá que toouse desejado.</span><span class="sxs-lookup"><span data-stu-id="b2166-141">Click on hello storage account you want toouse.</span></span>
3. <span data-ttu-id="b2166-142">Selecione **Todas as configurações** > **Chaves de acesso**.</span><span class="sxs-lookup"><span data-stu-id="b2166-142">Select **All settings** > **Access keys**.</span></span>
4. <span data-ttu-id="b2166-143">Clique em Olá cópia caixa toocopy uma área de transferência do toohello chaves de acesso.</span><span class="sxs-lookup"><span data-stu-id="b2166-143">Click hello copy box toocopy one of your access keys toohello clipboard.</span></span>
   
    ![Copiar a chave de armazenamento do Azure](./media/sql-data-warehouse-get-started-load-with-polybase/access-key.png)

### <a name="d-copy-hello-sample-file-tooazure-blob-storage"></a><span data-ttu-id="b2166-145">D.</span><span class="sxs-lookup"><span data-stu-id="b2166-145">D.</span></span> <span data-ttu-id="b2166-146">Copiar o armazenamento de blob tooAzure do arquivo de exemplo hello</span><span class="sxs-lookup"><span data-stu-id="b2166-146">Copy hello sample file tooAzure blob storage</span></span>
<span data-ttu-id="b2166-147">toocopy seu armazenamento de blob de tooAzure de dados:</span><span class="sxs-lookup"><span data-stu-id="b2166-147">toocopy your data tooAzure blob storage:</span></span>

1. <span data-ttu-id="b2166-148">Abra um prompt de comando e altere o diretório de instalação do diretórios toohello AzCopy.</span><span class="sxs-lookup"><span data-stu-id="b2166-148">Open a command prompt, and change directories toohello AzCopy installation directory.</span></span> <span data-ttu-id="b2166-149">Esse comando altera o diretório de instalação padrão toohello em um cliente do Windows de 64 bits.</span><span class="sxs-lookup"><span data-stu-id="b2166-149">This command changes toohello default installation directory on a 64-bit Windows client.</span></span>
   
    ```
    cd /d "%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy"
    ```
2. <span data-ttu-id="b2166-150">Execute Olá arquivo de saudação do comando tooupload a seguir.</span><span class="sxs-lookup"><span data-stu-id="b2166-150">Run hello following command tooupload hello file.</span></span> <span data-ttu-id="b2166-151">Especifique a URL do ponto de extremidade de serviço blob para <blob service endpoint URL> e sua chave da conta de armazenamento do Azure para <azure_storage_account_key>.</span><span class="sxs-lookup"><span data-stu-id="b2166-151">Specify your blob service endpoint URL for <blob service endpoint URL> and your Azure storage account key for <azure_storage_account_key>.</span></span>
   
    ```
    .\AzCopy.exe /Source:C:\Temp\ /Dest:<blob service endpoint URL> /datacontainer/datedimension/ /DestKey:<azure_storage_account_key> /Pattern:DimDate2.txt
    ```

<span data-ttu-id="b2166-152">Consulte também [guia de Introdução com hello o utilitário de linha de comando AzCopy][latest version of AzCopy].</span><span class="sxs-lookup"><span data-stu-id="b2166-152">See also [Getting Started with hello AzCopy Command-Line Utility][latest version of AzCopy].</span></span>

### <a name="e-explore-your-blob-storage-container"></a><span data-ttu-id="b2166-153">E.</span><span class="sxs-lookup"><span data-stu-id="b2166-153">E.</span></span> <span data-ttu-id="b2166-154">Explorar o contêiner de armazenamento de blobs</span><span class="sxs-lookup"><span data-stu-id="b2166-154">Explore your blob storage container</span></span>
<span data-ttu-id="b2166-155">arquivo de saudação toosee carregado tooblob armazenamento:</span><span class="sxs-lookup"><span data-stu-id="b2166-155">toosee hello file you uploaded tooblob storage:</span></span>

1. <span data-ttu-id="b2166-156">Volte tooyour folha de serviço de Blob.</span><span class="sxs-lookup"><span data-stu-id="b2166-156">Go back tooyour Blob service blade.</span></span>
2. <span data-ttu-id="b2166-157">Em Contêineres, clique duas vezes em **datacontainer**.</span><span class="sxs-lookup"><span data-stu-id="b2166-157">Under Containers, double-click **datacontainer**.</span></span>
3. <span data-ttu-id="b2166-158">dados de tooyour do tooexplore Olá caminho, clique em pasta Olá **datedimension** e você verá o arquivo carregado **DimDate2.txt**.</span><span class="sxs-lookup"><span data-stu-id="b2166-158">tooexplore hello path tooyour data, click hello folder **datedimension** and you will see your uploaded file **DimDate2.txt**.</span></span>
4. <span data-ttu-id="b2166-159">Clique em Propriedades de tooview **DimDate2.txt**.</span><span class="sxs-lookup"><span data-stu-id="b2166-159">tooview properties, click **DimDate2.txt**.</span></span>
5. <span data-ttu-id="b2166-160">Observe que, na folha de propriedades de Blob hello, você pode baixar ou excluir o arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="b2166-160">Note that in hello Blob properties blade, you can download or delete hello file.</span></span>
   
    ![Exibir o blob de armazenamento do Azure](./media/sql-data-warehouse-get-started-load-with-polybase/view-blob.png)

## <a name="step-2-create-an-external-table-for-hello-sample-data"></a><span data-ttu-id="b2166-162">Etapa 2: Criar uma tabela externa para dados de exemplo hello</span><span class="sxs-lookup"><span data-stu-id="b2166-162">Step 2: Create an external table for hello sample data</span></span>
<span data-ttu-id="b2166-163">Nesta seção, criamos uma tabela externa que define os dados de exemplo hello.</span><span class="sxs-lookup"><span data-stu-id="b2166-163">In this section we create an external table that defines hello sample data.</span></span>

<span data-ttu-id="b2166-164">PolyBase usa dados de tooaccess tabelas externas no armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="b2166-164">PolyBase uses external tables tooaccess data in Azure blob storage.</span></span> <span data-ttu-id="b2166-165">Como Olá dados não são armazenados no SQL Data Warehouse, o PolyBase manipula dados externos de toohello de autenticação usando uma credencial no escopo do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="b2166-165">Since hello data is not stored within SQL Data Warehouse, PolyBase handles authentication toohello external data by using a database-scoped credential.</span></span>

<span data-ttu-id="b2166-166">exemplo Hello nesta etapa usa essas instruções de Transact-SQL toocreate uma tabela externa.</span><span class="sxs-lookup"><span data-stu-id="b2166-166">hello example in this step uses these Transact-SQL statements toocreate an external table.</span></span>

* <span data-ttu-id="b2166-167">[Create Master Key (Transact-SQL)] [ Create Master Key (Transact-SQL)] tooencrypt segredo de saudação do banco de dados de credencial com escopo.</span><span class="sxs-lookup"><span data-stu-id="b2166-167">[Create Master Key (Transact-SQL)][Create Master Key (Transact-SQL)] tooencrypt hello secret of your database scoped credential.</span></span>
* <span data-ttu-id="b2166-168">[Criar credencial no escopo do banco de dados (Transact-SQL)] [ Create Database Scoped Credential (Transact-SQL)] toospecify informações de autenticação para sua conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="b2166-168">[Create Database Scoped Credential (Transact-SQL)][Create Database Scoped Credential (Transact-SQL)] toospecify authentication information for your Azure storage account.</span></span>
* <span data-ttu-id="b2166-169">[Criar fonte de dados externa (Transact-SQL)] [ Create External Data Source (Transact-SQL)] toospecify local de saudação do seu armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="b2166-169">[Create External Data Source (Transact-SQL)][Create External Data Source (Transact-SQL)] toospecify hello location of your Azure blob storage.</span></span>
* <span data-ttu-id="b2166-170">[Criar um formato de arquivo externo (Transact-SQL)] [ Create External File Format (Transact-SQL)] toospecify formato de saudação de seus dados.</span><span class="sxs-lookup"><span data-stu-id="b2166-170">[Create External File Format (Transact-SQL)][Create External File Format (Transact-SQL)] toospecify hello format of your data.</span></span>
* <span data-ttu-id="b2166-171">[Criar tabela externa (Transact-SQL)] [ Create External Table (Transact-SQL)] Olá a definição da tabela toospecify hello e o local de dados.</span><span class="sxs-lookup"><span data-stu-id="b2166-171">[Create External Table (Transact-SQL)][Create External Table (Transact-SQL)] toospecify hello table definition and location of hello data.</span></span>

<span data-ttu-id="b2166-172">Execute esta consulta no banco de dados do SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="b2166-172">Run this query against your SQL Data Warehouse database.</span></span> <span data-ttu-id="b2166-173">Ele cria uma tabela externa denominada DimDate2External no esquema dbo Olá que pontos de dados de exemplo DimDate2.txt toohello no armazenamento de BLOBs do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="b2166-173">It will create an external table named DimDate2External in hello dbo schema that points toohello DimDate2.txt sample data in hello Azure blob storage.</span></span>

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


<span data-ttu-id="b2166-174">No Pesquisador de objetos SQL Server no Visual Studio, você pode ver o formato de arquivo externo hello, fonte de dados externa e tabela de DimDate2External hello.</span><span class="sxs-lookup"><span data-stu-id="b2166-174">In SQL Server Object Explorer in Visual Studio, you can see hello external file format, external data source, and hello DimDate2External table.</span></span>

![Exibir tabela externa](./media/sql-data-warehouse-get-started-load-with-polybase/external-table.png)

## <a name="step-3-load-data-into-sql-data-warehouse"></a><span data-ttu-id="b2166-176">Etapa 3: carregar dados no SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="b2166-176">Step 3: Load data into SQL Data Warehouse</span></span>
<span data-ttu-id="b2166-177">Depois de criar tabela externa hello, você pode carregar dados de saudação em uma nova tabela ou inseri-lo em uma tabela existente.</span><span class="sxs-lookup"><span data-stu-id="b2166-177">Once hello external table is created, you can either load hello data into a new table or insert it into an existing table.</span></span>

* <span data-ttu-id="b2166-178">dados de saudação tooload em uma nova tabela, executar Olá [CREATE TABLE AS SELECT (Transact-SQL)] [ CREATE TABLE AS SELECT (Transact-SQL)] instrução.</span><span class="sxs-lookup"><span data-stu-id="b2166-178">tooload hello data into a new table, run hello [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)] statement.</span></span> <span data-ttu-id="b2166-179">nova tabela de saudação terá colunas Olá nomeadas na consulta de saudação.</span><span class="sxs-lookup"><span data-stu-id="b2166-179">hello new table will have hello columns named in hello query.</span></span> <span data-ttu-id="b2166-180">tipos de dados de saudação de colunas de saudação corresponderá a tipos de dados de saudação na definição de tabela externa hello.</span><span class="sxs-lookup"><span data-stu-id="b2166-180">hello data types of hello columns will match hello data types in hello external table definition.</span></span>
* <span data-ttu-id="b2166-181">dados de saudação tooload em uma tabela existente, use Olá [INSERT... SELECT (Transact-SQL)] [ INSERT...SELECT (Transact-SQL)] instrução.</span><span class="sxs-lookup"><span data-stu-id="b2166-181">tooload hello data into an existing table, use hello [INSERT...SELECT (Transact-SQL)][INSERT...SELECT (Transact-SQL)] statement.</span></span>

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

## <a name="step-4-create-statistics-on-your-newly-loaded-data"></a><span data-ttu-id="b2166-182">Etapa 4: criar estatísticas sobre os dados recém-carregados</span><span class="sxs-lookup"><span data-stu-id="b2166-182">Step 4: Create statistics on your newly loaded data</span></span>
<span data-ttu-id="b2166-183">O SQL Data Warehouse do Azure ainda não dá suporte a estatísticas de criação ou de atualização automática.</span><span class="sxs-lookup"><span data-stu-id="b2166-183">SQL Data Warehouse does not auto-create or auto-update statistics.</span></span> <span data-ttu-id="b2166-184">Portanto, tooachieve alto desempenho de consultas, é importante primeiro carregar toocreate estatísticas em cada coluna de cada tabela após a saudação.</span><span class="sxs-lookup"><span data-stu-id="b2166-184">Therefore, tooachieve high query performance, it's important toocreate statistics on each column of each table after hello first load.</span></span> <span data-ttu-id="b2166-185">Também é importante tooupdate estatísticas após alterações significativas nos dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="b2166-185">It's also important tooupdate statistics after substantial changes in hello data.</span></span>

<span data-ttu-id="b2166-186">Este exemplo cria estatísticas de coluna única na nova tabela de DimDate2 hello.</span><span class="sxs-lookup"><span data-stu-id="b2166-186">This example creates single-column statistics on hello new DimDate2 table.</span></span>

```sql
CREATE STATISTICS [DateId] on [DimDate2] ([DateId]);
CREATE STATISTICS [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
CREATE STATISTICS [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
```

<span data-ttu-id="b2166-187">mais, consulte toolearn [estatísticas][Statistics].</span><span class="sxs-lookup"><span data-stu-id="b2166-187">toolearn more, see [Statistics][Statistics].</span></span>  

## <a name="next-steps"></a><span data-ttu-id="b2166-188">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b2166-188">Next steps</span></span>
<span data-ttu-id="b2166-189">Consulte Olá [guia do PolyBase] [ PolyBase guide] para obter mais informações que você deve saber como desenvolver uma solução que usa o PolyBase.</span><span class="sxs-lookup"><span data-stu-id="b2166-189">See hello [PolyBase guide][PolyBase guide] for further information you should know as you develop a solution that uses PolyBase.</span></span>

<!--Image references-->


<!--Article references-->
[PolyBase in SQL Data Warehouse Tutorial]: ./sql-data-warehouse-get-started-load-with-polybase.md
[Load data with bcp]: ./sql-data-warehouse-load-with-bcp.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[PolyBase guide]: ./sql-data-warehouse-load-polybase-guide.md
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
