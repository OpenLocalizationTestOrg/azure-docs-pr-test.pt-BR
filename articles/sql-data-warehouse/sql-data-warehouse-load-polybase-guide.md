---
title: aaaGuide para usar o PolyBase no SQL Data Warehouse | Microsoft Docs
description: "Diretrizes e recomendações para usar o PolyBase em cenários do SQL Data Warehouse."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: 4757fce1-96b3-48ea-8a51-be1385705f9f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 6/5/2016
ms.custom: loading
ms.author: cakarst;barbkess
ms.openlocfilehash: b05e4c5d528f2fe1c60d6855b5333065f0c908ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="guide-for-using-polybase-in-sql-data-warehouse"></a><span data-ttu-id="c6cb4-103">Guia para usar o PolyBase no SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="c6cb4-103">Guide for using PolyBase in SQL Data Warehouse</span></span>
<span data-ttu-id="c6cb4-104">Este guia fornece informações práticas para usar o PolyBase no SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="c6cb4-104">This guide gives practical information for using PolyBase in SQL Data Warehouse.</span></span>

<span data-ttu-id="c6cb4-105">tooget iniciado, consulte Olá [carregar dados com o PolyBase] [ Load data with PolyBase] tutorial.</span><span class="sxs-lookup"><span data-stu-id="c6cb4-105">tooget started, see hello [Load data with PolyBase][Load data with PolyBase] tutorial.</span></span>

## <a name="rotating-storage-keys"></a><span data-ttu-id="c6cb4-106">Rotação de chaves de armazenamento</span><span class="sxs-lookup"><span data-stu-id="c6cb4-106">Rotating storage keys</span></span>
<span data-ttu-id="c6cb4-107">De tootime de tempo, você desejará o armazenamento de blob de chave tooyour do toochange Olá acesso por motivos de segurança.</span><span class="sxs-lookup"><span data-stu-id="c6cb4-107">From time tootime you will want toochange hello access key tooyour blob storage for security reasons.</span></span>

<span data-ttu-id="c6cb4-108">Olá mais elegante tooperform de forma que essa tarefa é toofollow um processo conhecido como "rotação de chaves de Olá".</span><span class="sxs-lookup"><span data-stu-id="c6cb4-108">hello most elegant way tooperform this task is toofollow a process known as "rotating hello keys".</span></span> <span data-ttu-id="c6cb4-109">Você talvez tenha observado que há duas chaves de armazenamento para a conta de armazenamento de blob.</span><span class="sxs-lookup"><span data-stu-id="c6cb4-109">You may have noticed that you have two storage keys for your blob storage account.</span></span> <span data-ttu-id="c6cb4-110">Isso é para que você possa fazer a transição</span><span class="sxs-lookup"><span data-stu-id="c6cb4-110">This is so that you can transition</span></span>

<span data-ttu-id="c6cb4-111">A rotação das suas chaves da conta de Armazenamento do Azure é um processo simples de três etapas</span><span class="sxs-lookup"><span data-stu-id="c6cb4-111">Rotating your Azure storage account keys is a simple three step process</span></span>

1. <span data-ttu-id="c6cb4-112">Criar segunda credencial no escopo do banco de dados com base na chave de acesso de armazenamento secundário Olá</span><span class="sxs-lookup"><span data-stu-id="c6cb4-112">Create second database scoped credential based on hello secondary storage access key</span></span>
2. <span data-ttu-id="c6cb4-113">Criar a segunda fonte de dados externa com base nessa nova credencial</span><span class="sxs-lookup"><span data-stu-id="c6cb4-113">Create second external data source based off this new credential</span></span>
3. <span data-ttu-id="c6cb4-114">Descarte e crie Olá tabelas externas apontando toohello nova fonte de dados externa</span><span class="sxs-lookup"><span data-stu-id="c6cb4-114">Drop and create hello external table(s) pointing toohello new external data source</span></span>

<span data-ttu-id="c6cb4-115">Depois de migrar todas as tabelas externas toohello nova fonte de dados externa, em seguida, você pode executar o hello Limpar tarefas:</span><span class="sxs-lookup"><span data-stu-id="c6cb4-115">When you have migrated all your external tables toohello new external data source then you can perform hello clean up tasks:</span></span>

1. <span data-ttu-id="c6cb4-116">Remover a primeira fonte de dados externa</span><span class="sxs-lookup"><span data-stu-id="c6cb4-116">Drop first external data source</span></span>
2. <span data-ttu-id="c6cb4-117">Credencial com base na chave de acesso de armazenamento primário Olá com escopo de descarte primeiro o banco de dados</span><span class="sxs-lookup"><span data-stu-id="c6cb4-117">Drop first database scoped credential based on hello primary storage access key</span></span>
3. <span data-ttu-id="c6cb4-118">Faça logon no Azure e regenerar chave de acesso primária Olá pronto para Olá próxima vez</span><span class="sxs-lookup"><span data-stu-id="c6cb4-118">Log into Azure and regenerate hello primary access key ready for hello next time</span></span>

## <a name="query-azure-blob-storage-data"></a><span data-ttu-id="c6cb4-119">Consultar dados de armazenamento de blob do Azure</span><span class="sxs-lookup"><span data-stu-id="c6cb4-119">Query Azure blob storage data</span></span>
<span data-ttu-id="c6cb4-120">Consultas em tabelas externas simplesmente usam o nome da tabela hello como se fosse uma tabela relacional.</span><span class="sxs-lookup"><span data-stu-id="c6cb4-120">Queries against external tables simply use hello table name as though it was a relational table.</span></span>

```sql
-- Query Azure storage resident data via external table.
SELECT * FROM [ext].[CarSensor_Data]
;
```

> [!NOTE]
> <span data-ttu-id="c6cb4-121">Uma consulta em uma tabela externa pode falhar com o erro Olá *"consulta anulada-limite máximo de rejeição de saudação foi atingido durante a leitura de uma fonte externa"*.</span><span class="sxs-lookup"><span data-stu-id="c6cb4-121">A query on an external table can fail with hello error *"Query aborted-- hello maximum reject threshold was reached while reading from an external source"*.</span></span> <span data-ttu-id="c6cb4-122">Isso indica que os dados externos contêm registros *sujos* .</span><span class="sxs-lookup"><span data-stu-id="c6cb4-122">This indicates that your external data contains *dirty* records.</span></span> <span data-ttu-id="c6cb4-123">Um registro de dados é considerado 'sujo' se tipos de dados reais Olá/número de colunas não correspondem a definições de coluna de saudação da tabela externa hello ou se dados saudação não está em conformidade toohello formato de arquivo externo especificado.</span><span class="sxs-lookup"><span data-stu-id="c6cb4-123">A data record is considered 'dirty' if hello actual data types/number of columns do not match hello column definitions of hello external table or if hello data doesn't conform toohello specified external file format.</span></span> <span data-ttu-id="c6cb4-124">toofix isso, certifique-se de que a tabela externa e as definições de formato de arquivo externo estão corretas e definições de toothese está de acordo com seus dados externos.</span><span class="sxs-lookup"><span data-stu-id="c6cb4-124">toofix this, ensure that your external table and external file format definitions are correct and your external data conforms toothese definitions.</span></span> <span data-ttu-id="c6cb4-125">No caso de um subconjunto de registros de dados externa estiver sujo, você pode escolher tooreject esses registros para as consultas usando as opções de rejeição de saudação em CREATE EXTERNAL TABLE DDL.</span><span class="sxs-lookup"><span data-stu-id="c6cb4-125">In case a subset of external data records are dirty, you can choose tooreject these records for your queries by using hello reject options in CREATE EXTERNAL TABLE DDL.</span></span>
> 
> 

## <a name="load-data-from-azure-blob-storage"></a><span data-ttu-id="c6cb4-126">Carregar dados do armazenamento de blob do Azure</span><span class="sxs-lookup"><span data-stu-id="c6cb4-126">Load data from Azure blob storage</span></span>
<span data-ttu-id="c6cb4-127">Este exemplo carrega dados do banco de dados do Data Warehouse tooSQL de armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="c6cb4-127">This example loads data from Azure blob storage tooSQL Data Warehouse database.</span></span>

<span data-ttu-id="c6cb4-128">Armazenando dados diretamente remove Olá tempo de transferência de dados para consultas.</span><span class="sxs-lookup"><span data-stu-id="c6cb4-128">Storing data directly removes hello data transfer time for queries.</span></span> <span data-ttu-id="c6cb4-129">Armazenando dados com um índice columnstore melhora o desempenho de consultas de análise pelo backup too10x.</span><span class="sxs-lookup"><span data-stu-id="c6cb4-129">Storing data with a columnstore index improves query performance for analysis queries by up too10x.</span></span>

<span data-ttu-id="c6cb4-130">Este exemplo usa dados de tooload de instrução CREATE TABLE AS SELECT saudação.</span><span class="sxs-lookup"><span data-stu-id="c6cb4-130">This example uses hello CREATE TABLE AS SELECT statement tooload data.</span></span> <span data-ttu-id="c6cb4-131">nova tabela de saudação herda colunas de saudação nomeadas na consulta de saudação.</span><span class="sxs-lookup"><span data-stu-id="c6cb4-131">hello new table inherits hello columns named in hello query.</span></span> <span data-ttu-id="c6cb4-132">Ele herda os tipos de dados Olá dessas colunas de definição de tabela externa hello.</span><span class="sxs-lookup"><span data-stu-id="c6cb4-132">It inherits hello data types of those columns from hello external table definition.</span></span>

<span data-ttu-id="c6cb4-133">CREATE TABLE AS SELECT é um alto desempenho instrução Transact-SQL que carrega dados Olá em paralelo tooall Olá nós de computação de Data Warehouse do SQL.</span><span class="sxs-lookup"><span data-stu-id="c6cb4-133">CREATE TABLE AS SELECT is a highly performant Transact-SQL statement that loads hello data in parallel tooall hello compute nodes of your SQL Data Warehouse.</span></span>  <span data-ttu-id="c6cb4-134">Ele foi originalmente desenvolvido para o mecanismo de processamento paralelo em massa (MPP) Olá no sistema de plataforma de análise e está agora no SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="c6cb4-134">It was originally developed for  hello massively parallel processing (MPP) engine in Analytics Platform System and is now in SQL Data Warehouse.</span></span>

```sql
-- Load data from Azure blob storage tooSQL Data Warehouse

CREATE TABLE [dbo].[Customer_Speed]
WITH
(   
    CLUSTERED COLUMNSTORE INDEX
,    DISTRIBUTION = HASH([CarSensor_Data].[CustomerKey])
)
AS
SELECT *
FROM   [ext].[CarSensor_Data]
;
```

<span data-ttu-id="c6cb4-135">Consulte [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)].</span><span class="sxs-lookup"><span data-stu-id="c6cb4-135">See [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)].</span></span>

## <a name="create-statistics-on-newly-loaded-data"></a><span data-ttu-id="c6cb4-136">Criar estatísticas sobre os dados recém-carregados</span><span class="sxs-lookup"><span data-stu-id="c6cb4-136">Create Statistics on newly loaded data</span></span>
<span data-ttu-id="c6cb4-137">O SQL Data Warehouse do Azure ainda não dá suporte a estatísticas de criação ou atualização automática.</span><span class="sxs-lookup"><span data-stu-id="c6cb4-137">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span></span>  <span data-ttu-id="c6cb4-138">Em ordem tooget Olá melhor desempenho de suas consultas, é importante que ser criadas estatísticas em todas as colunas de todas as tabelas após a primeira carga de saudação ou alterações substanciais ocorrerem nos dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="c6cb4-138">In order tooget hello best performance from your queries, it's important that statistics be created on all columns of all tables after hello first load or any substantial changes occur in hello data.</span></span>  <span data-ttu-id="c6cb4-139">Para obter uma explicação detalhada de estatísticas, consulte Olá [estatísticas] [ Statistics] tópico no grupo de desenvolver Olá de tópicos.</span><span class="sxs-lookup"><span data-stu-id="c6cb4-139">For a detailed explanation of statistics, see hello [Statistics][Statistics] topic in hello Develop group of topics.</span></span>  <span data-ttu-id="c6cb4-140">Abaixo está um exemplo rápido de como toocreate estatísticas na tabela de saudação carregados neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="c6cb4-140">Below is a quick example of how toocreate statistics on hello tabled loaded in this example.</span></span>

```sql
create statistics [SensorKey] on [Customer_Speed] ([SensorKey]);
create statistics [CustomerKey] on [Customer_Speed] ([CustomerKey]);
create statistics [GeographyKey] on [Customer_Speed] ([GeographyKey]);
create statistics [Speed] on [Customer_Speed] ([Speed]);
create statistics [YearMeasured] on [Customer_Speed] ([YearMeasured]);
```

## <a name="export-data-tooazure-blob-storage"></a><span data-ttu-id="c6cb4-141">Exportar o armazenamento de blob de tooAzure de dados</span><span class="sxs-lookup"><span data-stu-id="c6cb4-141">Export data tooAzure blob storage</span></span>
<span data-ttu-id="c6cb4-142">Esta seção mostra como o armazenamento de blob dados tooexport tooAzure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="c6cb4-142">This section shows how tooexport data from SQL Data Warehouse tooAzure blob storage.</span></span> <span data-ttu-id="c6cb4-143">Este exemplo usa CREATE EXTERNAL TABLE AS SELECT que é um altamente funcional Transact-SQL instrução tooexport Olá dados em paralelo de todos os nós de computação de saudação.</span><span class="sxs-lookup"><span data-stu-id="c6cb4-143">This example uses CREATE EXTERNAL TABLE AS SELECT which is a highly performant Transact-SQL statement tooexport hello data in parallel from all hello compute nodes.</span></span>

<span data-ttu-id="c6cb4-144">Olá, exemplo a seguir cria uma tabela externa Weblogs2014 usando dados de dbo e definições de coluna. Tabela weblogs.</span><span class="sxs-lookup"><span data-stu-id="c6cb4-144">hello following example creates an external table Weblogs2014 using column definitions and data from dbo.Weblogs table.</span></span> <span data-ttu-id="c6cb4-145">definição da tabela externa de saudação é armazenada no SQL Data Warehouse e resultados de Olá da instrução SELECT Olá são exportado toohello directory "/ arquivar/log2014 /" no contêiner de blob Olá especificada pela fonte de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="c6cb4-145">hello external table definition is stored in SQL Data Warehouse and hello results of hello SELECT statement are exported toohello "/archive/log2014/" directory under hello blob container specified by hello data source.</span></span> <span data-ttu-id="c6cb4-146">Olá dados são exportados no formato de arquivo de texto especificado hello.</span><span class="sxs-lookup"><span data-stu-id="c6cb4-146">hello data is exported in hello specified text file format.</span></span>

```sql
CREATE EXTERNAL TABLE Weblogs2014 WITH
(
    LOCATION='/archive/log2014/',
    DATA_SOURCE=azure_storage,
    FILE_FORMAT=text_file_format
)
AS
SELECT
    Uri,
    DateRequested
FROM
    dbo.Weblogs
WHERE
    1=1
    AND DateRequested > '12/31/2013'
    AND DateRequested < '01/01/2015';
```
## <a name="isolate-loading-users"></a><span data-ttu-id="c6cb4-147">Isolar Usuários em carregamento</span><span class="sxs-lookup"><span data-stu-id="c6cb4-147">Isolate Loading Users</span></span>
<span data-ttu-id="c6cb4-148">Há muitas vezes uma necessidade toohave vários usuários que podem carregar dados em um SQL DW.</span><span class="sxs-lookup"><span data-stu-id="c6cb4-148">There is often a need toohave multiple users that can load data into a SQL DW.</span></span> <span data-ttu-id="c6cb4-149">Porque Olá [CREATE TABLE AS SELECT (Transact-SQL)] [ CREATE TABLE AS SELECT (Transact-SQL)] requer permissões de controle do banco de dados hello, você acabará com vários usuários com controle de acesso sobre todos os esquemas.</span><span class="sxs-lookup"><span data-stu-id="c6cb4-149">Because hello [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)] requires CONTROL permissions of hello database, you will end up with multiple users with control access over all schemas.</span></span> <span data-ttu-id="c6cb4-150">toolimit isso, você pode usar a instrução de controle negar hello.</span><span class="sxs-lookup"><span data-stu-id="c6cb4-150">toolimit this, you can use hello DENY CONTROL statement.</span></span>

<span data-ttu-id="c6cb4-151">Exemplo: considere os esquemas de banco de dados schema_A para o departamento A e schema_B para o departamento B. Os usuários de banco de dados user_A e user_B serão usuários de carregamento de PolyBase nos departamentos A e B, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="c6cb4-151">Example: Consider database schemas schema_A for dept A, and schema_B for dept B Let database users user_A and user_B be users for PolyBase loading in dept A and B, respectively.</span></span> <span data-ttu-id="c6cb4-152">Ambos receberam permissões de banco de dados CONTROL.</span><span class="sxs-lookup"><span data-stu-id="c6cb4-152">They both have been granted CONTROL database permissions.</span></span>
<span data-ttu-id="c6cb4-153">criadores de saudação do esquema A e B agora bloquear seus esquemas usando DENY:</span><span class="sxs-lookup"><span data-stu-id="c6cb4-153">hello creators of schema A and B now lock down their schemas using DENY:</span></span>

```sql
   DENY CONTROL ON SCHEMA :: schema_A toouser_B;
   DENY CONTROL ON SCHEMA :: schema_B toouser_A;
```   
 <span data-ttu-id="c6cb4-154">Com isso, user_A e user_B devem agora ser impedidos de saudação esquema do outro departamento.</span><span class="sxs-lookup"><span data-stu-id="c6cb4-154">With this, user_A and user_B should now be locked out from hello other dept’s schema.</span></span>
 


## <a name="next-steps"></a><span data-ttu-id="c6cb4-155">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c6cb4-155">Next steps</span></span>
<span data-ttu-id="c6cb4-156">toolearn mais sobre tooSQL movimentação de dados do Data Warehouse, consulte Olá [visão geral de migração de dados][data migration overview].</span><span class="sxs-lookup"><span data-stu-id="c6cb4-156">toolearn more about moving data tooSQL Data Warehouse, see hello [data migration overview][data migration overview].</span></span>

<!--Image references-->

<!--Article references-->
[Load data with bcp]: ./sql-data-warehouse-load-with-bcp.md
[Load data with PolyBase]: ./sql-data-warehouse-get-started-load-with-polybase.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[data migration overview]: ./sql-data-warehouse-overview-migrate.md

<!--MSDN references-->
[supported source/sink]: https://msdn.microsoft.com/library/dn894007.aspx
[copy activity]: https://msdn.microsoft.com/library/dn835035.aspx
[SQL Server destination adapter]: https://msdn.microsoft.com/library/ms141095.aspx
[SSIS]: https://msdn.microsoft.com/library/ms141026.aspx

[CREATE EXTERNAL DATA SOURCE (Transact-SQL)]: https://msdn.microsoft.com/library/dn935022.aspx
[CREATE EXTERNAL FILE FORMAT (Transact-SQL)]: https://msdn.microsoft.com/library/dn935026.aspx
[CREATE EXTERNAL TABLE (Transact-SQL)]: https://msdn.microsoft.com/library/dn935021.aspx

[DROP EXTERNAL DATA SOURCE (Transact-SQL)]: https://msdn.microsoft.com/library/mt146367.aspx
[DROP EXTERNAL FILE FORMAT (Transact-SQL)]: https://msdn.microsoft.com/library/mt146379.aspx
[DROP EXTERNAL TABLE (Transact-SQL)]: https://msdn.microsoft.com/library/mt130698.aspx

[CREATE TABLE AS SELECT (Transact-SQL)]: https://msdn.microsoft.com/library/mt204041.aspx
[INSERT...SELECT (Transact-SQL)]: https://msdn.microsoft.com/library/ms174335.aspx
[CREATE MASTER KEY (Transact-SQL)]: https://msdn.microsoft.com/library/ms174382.aspx
[CREATE CREDENTIAL (Transact-SQL)]: https://msdn.microsoft.com/library/ms189522.aspx
[CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL)]: https://msdn.microsoft.com/library/mt270260.aspx
[DROP CREDENTIAL (Transact-SQL)]: https://msdn.microsoft.com/library/ms189450.aspx

<!-- External Links -->
