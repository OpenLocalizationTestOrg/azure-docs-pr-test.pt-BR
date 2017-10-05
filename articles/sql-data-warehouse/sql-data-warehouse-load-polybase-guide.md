---
title: Guia para usar PolyBase no SQL Data Warehouse | Microsoft Docs
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
ms.openlocfilehash: 6938b92d8e5b46d908dc5b2155bdfdc89bb1dc8c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="guide-for-using-polybase-in-sql-data-warehouse"></a><span data-ttu-id="b1875-103">Guia para usar o PolyBase no SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="b1875-103">Guide for using PolyBase in SQL Data Warehouse</span></span>
<span data-ttu-id="b1875-104">Este guia fornece informações práticas para usar o PolyBase no SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="b1875-104">This guide gives practical information for using PolyBase in SQL Data Warehouse.</span></span>

<span data-ttu-id="b1875-105">Para começar, consulte o tutorial [Carregar dados com o PolyBase][Load data with PolyBase].</span><span class="sxs-lookup"><span data-stu-id="b1875-105">To get started, see the [Load data with PolyBase][Load data with PolyBase] tutorial.</span></span>

## <a name="rotating-storage-keys"></a><span data-ttu-id="b1875-106">Rotação de chaves de armazenamento</span><span class="sxs-lookup"><span data-stu-id="b1875-106">Rotating storage keys</span></span>
<span data-ttu-id="b1875-107">Às vezes você desejará alterar a chave de acesso para o armazenamento de blob por motivos de segurança.</span><span class="sxs-lookup"><span data-stu-id="b1875-107">From time to time you will want to change the access key to your blob storage for security reasons.</span></span>

<span data-ttu-id="b1875-108">A maneira mais elegante de realizar essa tarefa é seguir um processo conhecido como "rotação das chaves".</span><span class="sxs-lookup"><span data-stu-id="b1875-108">The most elegant way to perform this task is to follow a process known as "rotating the keys".</span></span> <span data-ttu-id="b1875-109">Você talvez tenha observado que há duas chaves de armazenamento para a conta de armazenamento de blob.</span><span class="sxs-lookup"><span data-stu-id="b1875-109">You may have noticed that you have two storage keys for your blob storage account.</span></span> <span data-ttu-id="b1875-110">Isso é para que você possa fazer a transição</span><span class="sxs-lookup"><span data-stu-id="b1875-110">This is so that you can transition</span></span>

<span data-ttu-id="b1875-111">A rotação das suas chaves da conta de Armazenamento do Azure é um processo simples de três etapas</span><span class="sxs-lookup"><span data-stu-id="b1875-111">Rotating your Azure storage account keys is a simple three step process</span></span>

1. <span data-ttu-id="b1875-112">Criar uma segunda credencial no escopo do banco de dados com base na chave de acesso de armazenamento secundário</span><span class="sxs-lookup"><span data-stu-id="b1875-112">Create second database scoped credential based on the secondary storage access key</span></span>
2. <span data-ttu-id="b1875-113">Criar a segunda fonte de dados externa com base nessa nova credencial</span><span class="sxs-lookup"><span data-stu-id="b1875-113">Create second external data source based off this new credential</span></span>
3. <span data-ttu-id="b1875-114">Remover e criar as tabelas externas apontando para a nova fonte de dados externa</span><span class="sxs-lookup"><span data-stu-id="b1875-114">Drop and create the external table(s) pointing to the new external data source</span></span>

<span data-ttu-id="b1875-115">Depois de migrar todas as tabelas externas para a nova fonte de dados externa, você pode executar as tarefas de limpeza:</span><span class="sxs-lookup"><span data-stu-id="b1875-115">When you have migrated all your external tables to the new external data source then you can perform the clean up tasks:</span></span>

1. <span data-ttu-id="b1875-116">Remover a primeira fonte de dados externa</span><span class="sxs-lookup"><span data-stu-id="b1875-116">Drop first external data source</span></span>
2. <span data-ttu-id="b1875-117">Remover a primeira credencial no escopo do banco de dados na chave de acesso de armazenamento primário</span><span class="sxs-lookup"><span data-stu-id="b1875-117">Drop first database scoped credential based on the primary storage access key</span></span>
3. <span data-ttu-id="b1875-118">Fazer logon no Azure e regenerar a chave de acesso primária pronta para a próxima vez</span><span class="sxs-lookup"><span data-stu-id="b1875-118">Log into Azure and regenerate the primary access key ready for the next time</span></span>

## <a name="query-azure-blob-storage-data"></a><span data-ttu-id="b1875-119">Consultar dados de armazenamento de blob do Azure</span><span class="sxs-lookup"><span data-stu-id="b1875-119">Query Azure blob storage data</span></span>
<span data-ttu-id="b1875-120">As consultas em tabelas externas simplesmente usam o nome da tabela como se ele fosse uma tabela relacional.</span><span class="sxs-lookup"><span data-stu-id="b1875-120">Queries against external tables simply use the table name as though it was a relational table.</span></span>

```sql
-- Query Azure storage resident data via external table.
SELECT * FROM [ext].[CarSensor_Data]
;
```

> [!NOTE]
> <span data-ttu-id="b1875-121">Uma consulta em uma tabela externa pode falhar com o erro *“Consulta anulada – o limite de rejeição máximo foi atingido durante a leitura de uma fonte externa”*.</span><span class="sxs-lookup"><span data-stu-id="b1875-121">A query on an external table can fail with the error *"Query aborted-- the maximum reject threshold was reached while reading from an external source"*.</span></span> <span data-ttu-id="b1875-122">Isso indica que os dados externos contêm registros *sujos* .</span><span class="sxs-lookup"><span data-stu-id="b1875-122">This indicates that your external data contains *dirty* records.</span></span> <span data-ttu-id="b1875-123">Um registro de dados é considerado “sujo” se os tipos de dados/número de colunas reais não correspondem às definições de coluna da tabela externa ou se os dados não são compatíveis com o formato de arquivo externo especificado.</span><span class="sxs-lookup"><span data-stu-id="b1875-123">A data record is considered 'dirty' if the actual data types/number of columns do not match the column definitions of the external table or if the data doesn't conform to the specified external file format.</span></span> <span data-ttu-id="b1875-124">Para corrigir esse problema, verifique se a tabela externa e as definições de formato de arquivo externo estão corretas e se os dados externos são compatíveis com essas definições.</span><span class="sxs-lookup"><span data-stu-id="b1875-124">To fix this, ensure that your external table and external file format definitions are correct and your external data conforms to these definitions.</span></span> <span data-ttu-id="b1875-125">Caso um subconjunto de registros de dados externos esteja sujo, é possível rejeitar esses registros para suas consultas usando as opções de rejeição em CREATE EXTERNAL TABLE DDL.</span><span class="sxs-lookup"><span data-stu-id="b1875-125">In case a subset of external data records are dirty, you can choose to reject these records for your queries by using the reject options in CREATE EXTERNAL TABLE DDL.</span></span>
> 
> 

## <a name="load-data-from-azure-blob-storage"></a><span data-ttu-id="b1875-126">Carregar dados do armazenamento de blob do Azure</span><span class="sxs-lookup"><span data-stu-id="b1875-126">Load data from Azure blob storage</span></span>
<span data-ttu-id="b1875-127">Este exemplo carrega dados do armazenamento de blob do Azure no banco de dados do SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="b1875-127">This example loads data from Azure blob storage to SQL Data Warehouse database.</span></span>

<span data-ttu-id="b1875-128">Armazenar dados diretamente elimina o tempo de transferência de dados para consultas.</span><span class="sxs-lookup"><span data-stu-id="b1875-128">Storing data directly removes the data transfer time for queries.</span></span> <span data-ttu-id="b1875-129">Armazenar dados com um índice columnstore melhora o desempenho de consultas de análise em até 10 vezes.</span><span class="sxs-lookup"><span data-stu-id="b1875-129">Storing data with a columnstore index improves query performance for analysis queries by up to 10x.</span></span>

<span data-ttu-id="b1875-130">Este exemplo usa a instrução CREATE TABLE AS SELECT para carregar dados.</span><span class="sxs-lookup"><span data-stu-id="b1875-130">This example uses the CREATE TABLE AS SELECT statement to load data.</span></span> <span data-ttu-id="b1875-131">A nova tabela herda as colunas nomeadas na consulta.</span><span class="sxs-lookup"><span data-stu-id="b1875-131">The new table inherits the columns named in the query.</span></span> <span data-ttu-id="b1875-132">Ela herda os tipos de dados dessas colunas da definição de tabela externa.</span><span class="sxs-lookup"><span data-stu-id="b1875-132">It inherits the data types of those columns from the external table definition.</span></span>

<span data-ttu-id="b1875-133">CREATE TABLE AS SELECT é uma instrução Transact-SQL de alto desempenho que carrega os dados em paralelo em todos os nós de computação do seu SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="b1875-133">CREATE TABLE AS SELECT is a highly performant Transact-SQL statement that loads the data in parallel to all the compute nodes of your SQL Data Warehouse.</span></span>  <span data-ttu-id="b1875-134">Ela foi originalmente desenvolvida para o mecanismo MPP (processamento massivamente paralelo) no Analytics Platform System e agora está no SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="b1875-134">It was originally developed for  the massively parallel processing (MPP) engine in Analytics Platform System and is now in SQL Data Warehouse.</span></span>

```sql
-- Load data from Azure blob storage to SQL Data Warehouse

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

<span data-ttu-id="b1875-135">Consulte [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)].</span><span class="sxs-lookup"><span data-stu-id="b1875-135">See [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)].</span></span>

## <a name="create-statistics-on-newly-loaded-data"></a><span data-ttu-id="b1875-136">Criar estatísticas sobre os dados recém-carregados</span><span class="sxs-lookup"><span data-stu-id="b1875-136">Create Statistics on newly loaded data</span></span>
<span data-ttu-id="b1875-137">O SQL Data Warehouse do Azure ainda não dá suporte a estatísticas de criação ou atualização automática.</span><span class="sxs-lookup"><span data-stu-id="b1875-137">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span></span>  <span data-ttu-id="b1875-138">Para obter o melhor desempenho de suas consultas, é importante que as estatísticas sejam criadas em todas as colunas de todas as tabelas após o primeiro carregamento ou após uma alteração significativa nos dados.</span><span class="sxs-lookup"><span data-stu-id="b1875-138">In order to get the best performance from your queries, it's important that statistics be created on all columns of all tables after the first load or any substantial changes occur in the data.</span></span>  <span data-ttu-id="b1875-139">Para obter uma explicação detalhada das estatísticas, confira o tópico [Estatísticas][Statistics] no grupo de tópicos Desenvolver.</span><span class="sxs-lookup"><span data-stu-id="b1875-139">For a detailed explanation of statistics, see the [Statistics][Statistics] topic in the Develop group of topics.</span></span>  <span data-ttu-id="b1875-140">Veja abaixo um exemplo de como criar estatísticas na tabela carregada neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="b1875-140">Below is a quick example of how to create statistics on the tabled loaded in this example.</span></span>

```sql
create statistics [SensorKey] on [Customer_Speed] ([SensorKey]);
create statistics [CustomerKey] on [Customer_Speed] ([CustomerKey]);
create statistics [GeographyKey] on [Customer_Speed] ([GeographyKey]);
create statistics [Speed] on [Customer_Speed] ([Speed]);
create statistics [YearMeasured] on [Customer_Speed] ([YearMeasured]);
```

## <a name="export-data-to-azure-blob-storage"></a><span data-ttu-id="b1875-141">Exportar dados no armazenamento de blob do Azure</span><span class="sxs-lookup"><span data-stu-id="b1875-141">Export data to Azure blob storage</span></span>
<span data-ttu-id="b1875-142">Esta seção mostra como exportar dados do SQL Data Warehouse para o armazenamento de blob do Azure.</span><span class="sxs-lookup"><span data-stu-id="b1875-142">This section shows how to export data from SQL Data Warehouse to Azure blob storage.</span></span> <span data-ttu-id="b1875-143">Este exemplo usa CREATE EXTERNAL TABLE AS SELECT, que é uma instrução Transact-SQL de alto desempenho, para exportar os dados em paralelo de todos os nós de computação.</span><span class="sxs-lookup"><span data-stu-id="b1875-143">This example uses CREATE EXTERNAL TABLE AS SELECT which is a highly performant Transact-SQL statement to export the data in parallel from all the compute nodes.</span></span>

<span data-ttu-id="b1875-144">O exemplo a seguir cria uma tabela Weblogs2014 externa usando definições de coluna e dados da tabela dbo.Weblogs.</span><span class="sxs-lookup"><span data-stu-id="b1875-144">The following example creates an external table Weblogs2014 using column definitions and data from dbo.Weblogs table.</span></span> <span data-ttu-id="b1875-145">A definição da tabela externa é armazenada no SQL Data Warehouse e os resultados da instrução SELECT são exportados para o diretório "/archive/log2014 /" no contêiner de blob especificado pela fonte de dados.</span><span class="sxs-lookup"><span data-stu-id="b1875-145">The external table definition is stored in SQL Data Warehouse and the results of the SELECT statement are exported to the "/archive/log2014/" directory under the blob container specified by the data source.</span></span> <span data-ttu-id="b1875-146">Os dados são exportados no formato de arquivo de texto especificado.</span><span class="sxs-lookup"><span data-stu-id="b1875-146">The data is exported in the specified text file format.</span></span>

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
## <a name="isolate-loading-users"></a><span data-ttu-id="b1875-147">Isolar Usuários em carregamento</span><span class="sxs-lookup"><span data-stu-id="b1875-147">Isolate Loading Users</span></span>
<span data-ttu-id="b1875-148">Geralmente, há a necessidade de ter vários usuários que podem carregar dados em um SQL DW.</span><span class="sxs-lookup"><span data-stu-id="b1875-148">There is often a need to have multiple users that can load data into a SQL DW.</span></span> <span data-ttu-id="b1875-149">Como [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)] requer permissões CONTROL do banco de dados, você acabará tendo vários usuários com acesso de controle sobre todos os esquemas.</span><span class="sxs-lookup"><span data-stu-id="b1875-149">Because the [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)] requires CONTROL permissions of the database, you will end up with multiple users with control access over all schemas.</span></span> <span data-ttu-id="b1875-150">Para limitar isso, você pode usar a instrução DENY CONTROL.</span><span class="sxs-lookup"><span data-stu-id="b1875-150">To limit this, you can use the DENY CONTROL statement.</span></span>

<span data-ttu-id="b1875-151">Exemplo: considere os esquemas de banco de dados schema_A para o departamento A e schema_B para o departamento B. Os usuários de banco de dados user_A e user_B serão usuários de carregamento de PolyBase nos departamentos A e B, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="b1875-151">Example: Consider database schemas schema_A for dept A, and schema_B for dept B Let database users user_A and user_B be users for PolyBase loading in dept A and B, respectively.</span></span> <span data-ttu-id="b1875-152">Ambos receberam permissões de banco de dados CONTROL.</span><span class="sxs-lookup"><span data-stu-id="b1875-152">They both have been granted CONTROL database permissions.</span></span>
<span data-ttu-id="b1875-153">Os criadores dos esquemas A e B agora bloquearam seus esquemas usando DENY:</span><span class="sxs-lookup"><span data-stu-id="b1875-153">The creators of schema A and B now lock down their schemas using DENY:</span></span>

```sql
   DENY CONTROL ON SCHEMA :: schema_A TO user_B;
   DENY CONTROL ON SCHEMA :: schema_B TO user_A;
```   
 <span data-ttu-id="b1875-154">Com isso, user_A e user_B devem agora ser bloqueados do esquema do outro departamento.</span><span class="sxs-lookup"><span data-stu-id="b1875-154">With this, user_A and user_B should now be locked out from the other dept’s schema.</span></span>
 


## <a name="next-steps"></a><span data-ttu-id="b1875-155">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b1875-155">Next steps</span></span>
<span data-ttu-id="b1875-156">Para saber mais sobre como mover dados para o SQL Data Warehouse, consulte o [Visão geral de migração de dados][data migration overview].</span><span class="sxs-lookup"><span data-stu-id="b1875-156">To learn more about moving data to SQL Data Warehouse, see the [data migration overview][data migration overview].</span></span>

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
