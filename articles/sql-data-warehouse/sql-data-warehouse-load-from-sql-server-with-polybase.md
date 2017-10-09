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
# <a name="load-data-with-polybase-in-sql-data-warehouse"></a>Carregar dados com o PolyBase no SQL Data Warehouse
> [!div class="op_single_selector"]
> * [SSIS](sql-data-warehouse-load-from-sql-server-with-integration-services.md)
> * [PolyBase](sql-data-warehouse-load-from-sql-server-with-polybase.md)
> * [bcp](sql-data-warehouse-load-from-sql-server-with-bcp.md)
> 
> 

Este tutorial mostra como dados tooload no SQL Data Warehouse usando AzCopy e PolyBase. Quando terminar, você saberá como:

* Usar o armazenamento de blob AzCopy toocopy dados tooAzure
* Criar objetos de banco de dados toodefine dados de saudação
* Execute uma consulta de T-SQL tooload Olá dados

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-data-with-PolyBase-in-Azure-SQL-Data-Warehouse/player]
> 
> 

## <a name="prerequisites"></a>Pré-requisitos
toostep este tutorial, você precisa

* Um banco de dados do SQL Data Warehouse.
* Uma conta de armazenamento do Azure do tipo Padrão-LRS (Armazenamento com Redundância Local Padrão), Padrão-GRS (Armazenamento com Redundância Geográfica Padrão) ou Padrão-RAGRS (Armazenamento de Redundância Geográfica com Acesso de Leitura Padrão).
* Utilitário de linha de comando AzCopy. Baixe e instale Olá [versão mais recente do AzCopy] [ latest version of AzCopy] que é instalado com hello ferramentas de armazenamento do Microsoft Azure.
  
    ![Ferramentas do Armazenamento do Azure](./media/sql-data-warehouse-get-started-load-with-polybase/install-azcopy.png)

## <a name="step-1-add-sample-data-tooazure-blob-storage"></a>Etapa 1: Adicionar o armazenamento de blob de tooAzure de dados de exemplo
Dados de pedidos tooload, é preciso tooput alguns dados de exemplo em um armazenamento de BLOBs do Azure. Nesta etapa, preencheremos um blob do Armazenamento do Azure com dados de exemplo. Posteriormente, usaremos PolyBase tooload esses dados de exemplo em seu banco de dados do SQL Data Warehouse.

### <a name="a-prepare-a-sample-text-file"></a>R. Preparar um arquivo de texto de exemplo
tooprepare um arquivo de texto de exemplo:

1. Abra o bloco de notas e copie Olá linhas de dados a seguir em um novo arquivo. Salve esse diretório temporário local de tooyour como temp%\DimDate2.txt %.

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

### <a name="b-find-your-blob-service-endpoint"></a>B. Localizar o ponto de extremidade do serviço blob
toofind seu ponto de extremidade do serviço blob:

1. Olá Portal do Azure selecione **procurar** > **contas de armazenamento**.
2. Clique na conta de armazenamento Olá que deseja toouse.
3. Na folha de conta de armazenamento de saudação, clique em Blobs
   
    ![Clicar em Blobs](./media/sql-data-warehouse-get-started-load-with-polybase/click-blobs.png)
4. Salve a URL do ponto de extremidade do serviço blob para mais tarde.
   
    ![Ponto de extremidade do serviço blob](./media/sql-data-warehouse-get-started-load-with-polybase/blob-service.png)

### <a name="c-find-your-azure-storage-key"></a>C. Encontrar a chave de armazenamento do Azure
toofind sua chave de armazenamento do Azure:

1. Olá Portal do Azure, selecione **procurar** > **contas de armazenamento**.
2. Clique na conta de armazenamento Olá que toouse desejado.
3. Selecione **Todas as configurações** > **Chaves de acesso**.
4. Clique em Olá cópia caixa toocopy uma área de transferência do toohello chaves de acesso.
   
    ![Copiar a chave de armazenamento do Azure](./media/sql-data-warehouse-get-started-load-with-polybase/access-key.png)

### <a name="d-copy-hello-sample-file-tooazure-blob-storage"></a>D. Copiar o armazenamento de blob tooAzure do arquivo de exemplo hello
toocopy seu armazenamento de blob de tooAzure de dados:

1. Abra um prompt de comando e altere o diretório de instalação do diretórios toohello AzCopy. Esse comando altera o diretório de instalação padrão toohello em um cliente do Windows de 64 bits.
   
    ```
    cd /d "%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy"
    ```
2. Execute Olá arquivo de saudação do comando tooupload a seguir. Especifique a URL do ponto de extremidade de serviço blob para <blob service endpoint URL> e sua chave da conta de armazenamento do Azure para <azure_storage_account_key>.
   
    ```
    .\AzCopy.exe /Source:C:\Temp\ /Dest:<blob service endpoint URL> /datacontainer/datedimension/ /DestKey:<azure_storage_account_key> /Pattern:DimDate2.txt
    ```

Consulte também [guia de Introdução com hello o utilitário de linha de comando AzCopy][latest version of AzCopy].

### <a name="e-explore-your-blob-storage-container"></a>E. Explorar o contêiner de armazenamento de blobs
arquivo de saudação toosee carregado tooblob armazenamento:

1. Volte tooyour folha de serviço de Blob.
2. Em Contêineres, clique duas vezes em **datacontainer**.
3. dados de tooyour do tooexplore Olá caminho, clique em pasta Olá **datedimension** e você verá o arquivo carregado **DimDate2.txt**.
4. Clique em Propriedades de tooview **DimDate2.txt**.
5. Observe que, na folha de propriedades de Blob hello, você pode baixar ou excluir o arquivo hello.
   
    ![Exibir o blob de armazenamento do Azure](./media/sql-data-warehouse-get-started-load-with-polybase/view-blob.png)

## <a name="step-2-create-an-external-table-for-hello-sample-data"></a>Etapa 2: Criar uma tabela externa para dados de exemplo hello
Nesta seção, criamos uma tabela externa que define os dados de exemplo hello.

PolyBase usa dados de tooaccess tabelas externas no armazenamento de BLOBs do Azure. Como Olá dados não são armazenados no SQL Data Warehouse, o PolyBase manipula dados externos de toohello de autenticação usando uma credencial no escopo do banco de dados.

exemplo Hello nesta etapa usa essas instruções de Transact-SQL toocreate uma tabela externa.

* [Create Master Key (Transact-SQL)] [ Create Master Key (Transact-SQL)] tooencrypt segredo de saudação do banco de dados de credencial com escopo.
* [Criar credencial no escopo do banco de dados (Transact-SQL)] [ Create Database Scoped Credential (Transact-SQL)] toospecify informações de autenticação para sua conta de armazenamento do Azure.
* [Criar fonte de dados externa (Transact-SQL)] [ Create External Data Source (Transact-SQL)] toospecify local de saudação do seu armazenamento de BLOBs do Azure.
* [Criar um formato de arquivo externo (Transact-SQL)] [ Create External File Format (Transact-SQL)] toospecify formato de saudação de seus dados.
* [Criar tabela externa (Transact-SQL)] [ Create External Table (Transact-SQL)] Olá a definição da tabela toospecify hello e o local de dados.

Execute esta consulta no banco de dados do SQL Data Warehouse. Ele cria uma tabela externa denominada DimDate2External no esquema dbo Olá que pontos de dados de exemplo DimDate2.txt toohello no armazenamento de BLOBs do Azure hello.

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


No Pesquisador de objetos SQL Server no Visual Studio, você pode ver o formato de arquivo externo hello, fonte de dados externa e tabela de DimDate2External hello.

![Exibir tabela externa](./media/sql-data-warehouse-get-started-load-with-polybase/external-table.png)

## <a name="step-3-load-data-into-sql-data-warehouse"></a>Etapa 3: carregar dados no SQL Data Warehouse
Depois de criar tabela externa hello, você pode carregar dados de saudação em uma nova tabela ou inseri-lo em uma tabela existente.

* dados de saudação tooload em uma nova tabela, executar Olá [CREATE TABLE AS SELECT (Transact-SQL)] [ CREATE TABLE AS SELECT (Transact-SQL)] instrução. nova tabela de saudação terá colunas Olá nomeadas na consulta de saudação. tipos de dados de saudação de colunas de saudação corresponderá a tipos de dados de saudação na definição de tabela externa hello.
* dados de saudação tooload em uma tabela existente, use Olá [INSERT... SELECT (Transact-SQL)] [ INSERT...SELECT (Transact-SQL)] instrução.

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

## <a name="step-4-create-statistics-on-your-newly-loaded-data"></a>Etapa 4: criar estatísticas sobre os dados recém-carregados
O SQL Data Warehouse do Azure ainda não dá suporte a estatísticas de criação ou de atualização automática. Portanto, tooachieve alto desempenho de consultas, é importante primeiro carregar toocreate estatísticas em cada coluna de cada tabela após a saudação. Também é importante tooupdate estatísticas após alterações significativas nos dados de saudação.

Este exemplo cria estatísticas de coluna única na nova tabela de DimDate2 hello.

```sql
CREATE STATISTICS [DateId] on [DimDate2] ([DateId]);
CREATE STATISTICS [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
CREATE STATISTICS [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
```

mais, consulte toolearn [estatísticas][Statistics].  

## <a name="next-steps"></a>Próximas etapas
Consulte Olá [guia do PolyBase] [ PolyBase guide] para obter mais informações que você deve saber como desenvolver uma solução que usa o PolyBase.

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
