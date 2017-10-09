---
title: grupos de aaaManage de bancos de dados SQL do Azure | Microsoft Docs
description: "Explore a criação e o gerenciamento de um trabalho elástico."
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
editor: 
ms.assetid: f858344d-085b-4022-935e-1b5fa20adbac
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: a73c4fb24c332fae0e917c18272724cccd56f29a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-scaled-out-azure-sql-databases-using-elastic-jobs-preview"></a><span data-ttu-id="3f40b-103">Criar e gerenciar Bancos de Dados SQL do Azure com escala horizontal usando trabalhos elásticos (preview)</span><span class="sxs-lookup"><span data-stu-id="3f40b-103">Create and manage scaled out Azure SQL Databases using elastic jobs (preview)</span></span>


<span data-ttu-id="3f40b-104">**Trabalhos de Banco de Dados Elástico** simplificam o gerenciamento de grupos de bancos de dados executando operações administrativas como alterações de esquema, gerenciamento de credenciais, atualizações de dados de referência, coleta dados de desempenho ou de telemetria do locatário (cliente).</span><span class="sxs-lookup"><span data-stu-id="3f40b-104">**Elastic Database jobs** simplify management of groups of databases by executing administrative operations such as schema changes, credentials management, reference data updates, performance data collection or tenant (customer) telemetry collection.</span></span> <span data-ttu-id="3f40b-105">Trabalhos do banco de dados Elásticos está disponível por meio de saudação portal do Azure e cmdlets do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3f40b-105">Elastic Database jobs is currently available through hello Azure portal and PowerShell cmdlets.</span></span> <span data-ttu-id="3f40b-106">No entanto, a saudação funcionalidade reduzida superfícies de portal do Azure limitado tooexecution em todos os bancos de dados em um [(visualização) do pool Elástico](sql-database-elastic-pool.md).</span><span class="sxs-lookup"><span data-stu-id="3f40b-106">However, hello Azure portal surfaces reduced functionality limited tooexecution across all databases in an [elastic pool (preview)](sql-database-elastic-pool.md).</span></span> <span data-ttu-id="3f40b-107">recursos adicionais de tooaccess e execução de scripts em um grupo de bancos de dados incluindo uma coleção personalizadas ou um fragmento definem (criada usando [biblioteca de cliente do banco de dados Elástico](sql-database-elastic-scale-introduction.md)), consulte [criando e gerenciando trabalhos usando o PowerShell](sql-database-elastic-jobs-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="3f40b-107">tooaccess additional features and execution of scripts across a group of databases including a custom-defined collection or a shard set (created using [Elastic Database client library](sql-database-elastic-scale-introduction.md)), see [Creating and managing jobs using PowerShell](sql-database-elastic-jobs-powershell.md).</span></span> <span data-ttu-id="3f40b-108">Para saber mais, confira [Visão geral de trabalhos de Banco de Dados Elástico](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3f40b-108">For more information about jobs, see [Elastic Database jobs overview](sql-database-elastic-jobs-overview.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="3f40b-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="3f40b-109">Prerequisites</span></span>
* <span data-ttu-id="3f40b-110">Uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="3f40b-110">An Azure subscription.</span></span> <span data-ttu-id="3f40b-111">Para obter uma avaliação gratuita, veja [Avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3f40b-111">For a free trial, see [Free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="3f40b-112">Um pool elástico.</span><span class="sxs-lookup"><span data-stu-id="3f40b-112">An elastic pool.</span></span> <span data-ttu-id="3f40b-113">Consulte [Sobre pools elásticos](sql-database-elastic-pool.md).</span><span class="sxs-lookup"><span data-stu-id="3f40b-113">See [About elastic pools](sql-database-elastic-pool.md).</span></span>
* <span data-ttu-id="3f40b-114">Instalação dos componentes de serviço do trabalho de banco de dados elástico.</span><span class="sxs-lookup"><span data-stu-id="3f40b-114">Installation of elastic database job service components.</span></span> <span data-ttu-id="3f40b-115">Consulte [instalar o serviço de trabalho de banco de dados Elástico Olá](sql-database-elastic-jobs-service-installation.md).</span><span class="sxs-lookup"><span data-stu-id="3f40b-115">See [Installing hello elastic database job service](sql-database-elastic-jobs-service-installation.md).</span></span>

## <a name="creating-jobs"></a><span data-ttu-id="3f40b-116">Criando trabalhos</span><span class="sxs-lookup"><span data-stu-id="3f40b-116">Creating jobs</span></span>
1. <span data-ttu-id="3f40b-117">Usando Olá [portal do Azure](https://portal.azure.com), de um pool de trabalho do banco de dados Elástico existente, clique em **criar trabalho**.</span><span class="sxs-lookup"><span data-stu-id="3f40b-117">Using hello [Azure portal](https://portal.azure.com), from an existing elastic database job pool, click **Create job**.</span></span>
2. <span data-ttu-id="3f40b-118">Digite hello nome de usuário e senha do administrador de banco de dados de saudação (criado na instalação de trabalhos) para o banco de dados do controle de trabalhos hello (armazenamento de metadados para trabalhos).</span><span class="sxs-lookup"><span data-stu-id="3f40b-118">Type in hello username and password of hello database administrator (created at installation of Jobs) for hello jobs control database (metadata storage for jobs).</span></span>
   
    ![Nome do trabalho hello, digite ou cole no código e clique em executar][1]
3. <span data-ttu-id="3f40b-120">Em Olá **criar trabalho** folha, digite um nome para o trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="3f40b-120">In hello **Create Job** blade, type a name for hello job.</span></span>
4. <span data-ttu-id="3f40b-121">Digite hello usuário nome e senha tooconnect toohello destino bancos de dados com permissões suficientes para toosucceed de execução do script.</span><span class="sxs-lookup"><span data-stu-id="3f40b-121">Type hello user name and password tooconnect toohello target databases with sufficient permissions for script execution toosucceed.</span></span>
5. <span data-ttu-id="3f40b-122">Cole ou digite no script hello T-SQL.</span><span class="sxs-lookup"><span data-stu-id="3f40b-122">Paste or type in hello T-SQL script.</span></span>
6. <span data-ttu-id="3f40b-123">Clique em **Salvar** e em **Executar**.</span><span class="sxs-lookup"><span data-stu-id="3f40b-123">Click **Save** and then click **Run**.</span></span>
   
    ![Criar trabalhos e executar][5]

## <a name="run-idempotent-jobs"></a><span data-ttu-id="3f40b-125">Executar trabalhos idempotentes</span><span class="sxs-lookup"><span data-stu-id="3f40b-125">Run idempotent jobs</span></span>
<span data-ttu-id="3f40b-126">Quando você executa um script em um conjunto de bancos de dados, você deve ter certeza de script hello é idempotente.</span><span class="sxs-lookup"><span data-stu-id="3f40b-126">When you run a script against a set of databases, you must be sure that hello script is idempotent.</span></span> <span data-ttu-id="3f40b-127">Ou seja, Olá script deve ser capaz de toorun várias vezes, mesmo se ele tiver falhado antes em um estado incompleto.</span><span class="sxs-lookup"><span data-stu-id="3f40b-127">That is, hello script must be able toorun multiple times, even if it has failed before in an incomplete state.</span></span> <span data-ttu-id="3f40b-128">Por exemplo, quando um script falha, o trabalho de saudação será automaticamente repetido até obter êxito (dentro dos limites, como repetir Olá lógica eventualmente deixarão Olá tentando novamente).</span><span class="sxs-lookup"><span data-stu-id="3f40b-128">For example, when a script fails, hello job will be automatically retried until it succeeds (within limits, as hello retry logic will eventually cease hello retrying).</span></span> <span data-ttu-id="3f40b-129">Olá maneira toodo é toouse Olá uma cláusula "IF EXISTS" e excluir qualquer instância encontrada antes de criar um novo objeto.</span><span class="sxs-lookup"><span data-stu-id="3f40b-129">hello way toodo this is toouse hello an "IF EXISTS" clause and delete any found instance before creating a new object.</span></span> <span data-ttu-id="3f40b-130">Veja um exemplo aqui:</span><span class="sxs-lookup"><span data-stu-id="3f40b-130">An example is shown here:</span></span>

    IF EXISTS (SELECT name FROM sys.indexes
            WHERE name = N'IX_ProductVendor_VendorID')
    DROP INDEX IX_ProductVendor_VendorID ON Purchasing.ProductVendor;
    GO
    CREATE INDEX IX_ProductVendor_VendorID
    ON Purchasing.ProductVendor (VendorID);

<span data-ttu-id="3f40b-131">Como alternativa, use uma cláusula "IF NOT EXISTS" antes de criar uma nova instância:</span><span class="sxs-lookup"><span data-stu-id="3f40b-131">Alternatively, use an "IF NOT EXISTS" clause before creating a new instance:</span></span>

    IF NOT EXISTS (SELECT name FROM sys.tables WHERE name = 'TestTable')
    BEGIN
     CREATE TABLE TestTable(
      TestTableId INT PRIMARY KEY IDENTITY,
      InsertionTime DATETIME2
     );
    END
    GO

    INSERT INTO TestTable(InsertionTime) VALUES (sysutcdatetime());
    GO

<span data-ttu-id="3f40b-132">Esse script, em seguida, atualiza a tabela de saudação criada anteriormente.</span><span class="sxs-lookup"><span data-stu-id="3f40b-132">This script then updates hello table created previously.</span></span>

    IF NOT EXISTS (SELECT columns.name FROM sys.columns INNER JOIN sys.tables on columns.object_id = tables.object_id WHERE tables.name = 'TestTable' AND columns.name = 'AdditionalInformation')
    BEGIN

    ALTER TABLE TestTable

    ADD AdditionalInformation NVARCHAR(400);
    END
    GO

    INSERT INTO TestTable(InsertionTime, AdditionalInformation) VALUES (sysutcdatetime(), 'test');
    GO


## <a name="checking-job-status"></a><span data-ttu-id="3f40b-133">Verificando o status do trabalho</span><span class="sxs-lookup"><span data-stu-id="3f40b-133">Checking job status</span></span>
<span data-ttu-id="3f40b-134">Após o início de um trabalho, você pode verificar seu andamento.</span><span class="sxs-lookup"><span data-stu-id="3f40b-134">After a job has begun, you can check on its progress.</span></span>

1. <span data-ttu-id="3f40b-135">Na página de pool Elástico hello, clique **gerenciar trabalhos**.</span><span class="sxs-lookup"><span data-stu-id="3f40b-135">From hello elastic pool page, click **Manage jobs**.</span></span>
   
    ![Clique em “Gerenciar trabalhos”][2]
2. <span data-ttu-id="3f40b-137">Clique em Olá nome (a) de um trabalho.</span><span class="sxs-lookup"><span data-stu-id="3f40b-137">Click on hello name (a) of a job.</span></span> <span data-ttu-id="3f40b-138">Olá **STATUS** pode ser "Concluído" ou "Failed".</span><span class="sxs-lookup"><span data-stu-id="3f40b-138">hello **STATUS** can be "Completed" or "Failed."</span></span> <span data-ttu-id="3f40b-139">detalhes do trabalho Olá aparecem (b) com sua data e hora de criação e execução.</span><span class="sxs-lookup"><span data-stu-id="3f40b-139">hello job's details appear (b) with its date and time of creation and running.</span></span> <span data-ttu-id="3f40b-140">lista de saudação (c) abaixo Olá que mostra o progresso de saudação do script hello cada banco de dados no pool de hello, dando a seus detalhes de data e hora.</span><span class="sxs-lookup"><span data-stu-id="3f40b-140">hello list (c) below hello that shows hello progress of hello script against each database in hello pool, giving its date and time details.</span></span>
   
    ![Verificando um trabalho concluído][3]

## <a name="checking-failed-jobs"></a><span data-ttu-id="3f40b-142">Verificação de trabalhos com falha</span><span class="sxs-lookup"><span data-stu-id="3f40b-142">Checking failed jobs</span></span>
<span data-ttu-id="3f40b-143">Se um trabalho falhar, será possível encontrar um log de sua execução.</span><span class="sxs-lookup"><span data-stu-id="3f40b-143">If a job fails, a log of its execution can found.</span></span> <span data-ttu-id="3f40b-144">Clique o nome de saudação do hello falha no trabalho toosee seus detalhes.</span><span class="sxs-lookup"><span data-stu-id="3f40b-144">Click hello name of hello failed job toosee its details.</span></span>

![Verificar um trabalho com falha][4]

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-jobs-create-and-manage/screen-1.png
[2]: ./media/sql-database-elastic-jobs-create-and-manage/click-manage-jobs.png
[3]: ./media/sql-database-elastic-jobs-create-and-manage/running-jobs.png
[4]: ./media/sql-database-elastic-jobs-create-and-manage/failed.png
[5]: ./media/sql-database-elastic-jobs-create-and-manage/screen-2.png


