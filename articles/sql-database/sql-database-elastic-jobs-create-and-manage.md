---
title: Gerenciar grupos dos bancos de dados SQL do Azure | Microsoft Docs
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
ms.openlocfilehash: d30cc74778e0b36dd632c2f040ce80d1ca8af5a5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-scaled-out-azure-sql-databases-using-elastic-jobs-preview"></a><span data-ttu-id="681d4-103">Criar e gerenciar Bancos de Dados SQL do Azure com escala horizontal usando trabalhos elásticos (preview)</span><span class="sxs-lookup"><span data-stu-id="681d4-103">Create and manage scaled out Azure SQL Databases using elastic jobs (preview)</span></span>


<span data-ttu-id="681d4-104">**Trabalhos de Banco de Dados Elástico** simplificam o gerenciamento de grupos de bancos de dados executando operações administrativas como alterações de esquema, gerenciamento de credenciais, atualizações de dados de referência, coleta dados de desempenho ou de telemetria do locatário (cliente).</span><span class="sxs-lookup"><span data-stu-id="681d4-104">**Elastic Database jobs** simplify management of groups of databases by executing administrative operations such as schema changes, credentials management, reference data updates, performance data collection or tenant (customer) telemetry collection.</span></span> <span data-ttu-id="681d4-105">Trabalhos de Banco de Dados Elástico está disponível atualmente por meio de cmdlets do PowerShell e do Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="681d4-105">Elastic Database jobs is currently available through the Azure portal and PowerShell cmdlets.</span></span> <span data-ttu-id="681d4-106">No entanto, o portal do Azure revela funcionalidade reduzida limitada à execução em todos os bancos de dados em um [pool elástico (visualização)](sql-database-elastic-pool.md).</span><span class="sxs-lookup"><span data-stu-id="681d4-106">However, the Azure portal surfaces reduced functionality limited to execution across all databases in an [elastic pool (preview)](sql-database-elastic-pool.md).</span></span> <span data-ttu-id="681d4-107">Para acessar recursos adicionais e execução de scripts em um grupo de bancos de dados, incluindo uma coleção definida de modo personalizado ou um conjunto de fragmentos (criado usando a [biblioteca de cliente do Banco de Dados Elástico](sql-database-elastic-scale-introduction.md)), consulte [Criando e gerenciando trabalhos usando o PowerShell](sql-database-elastic-jobs-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="681d4-107">To access additional features and execution of scripts across a group of databases including a custom-defined collection or a shard set (created using [Elastic Database client library](sql-database-elastic-scale-introduction.md)), see [Creating and managing jobs using PowerShell](sql-database-elastic-jobs-powershell.md).</span></span> <span data-ttu-id="681d4-108">Para saber mais, confira [Visão geral de trabalhos de Banco de Dados Elástico](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="681d4-108">For more information about jobs, see [Elastic Database jobs overview](sql-database-elastic-jobs-overview.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="681d4-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="681d4-109">Prerequisites</span></span>
* <span data-ttu-id="681d4-110">Uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="681d4-110">An Azure subscription.</span></span> <span data-ttu-id="681d4-111">Para obter uma avaliação gratuita, veja [Avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="681d4-111">For a free trial, see [Free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="681d4-112">Um pool elástico.</span><span class="sxs-lookup"><span data-stu-id="681d4-112">An elastic pool.</span></span> <span data-ttu-id="681d4-113">Consulte [Sobre pools elásticos](sql-database-elastic-pool.md).</span><span class="sxs-lookup"><span data-stu-id="681d4-113">See [About elastic pools](sql-database-elastic-pool.md).</span></span>
* <span data-ttu-id="681d4-114">Instalação dos componentes de serviço do trabalho de banco de dados elástico.</span><span class="sxs-lookup"><span data-stu-id="681d4-114">Installation of elastic database job service components.</span></span> <span data-ttu-id="681d4-115">Consulte [Instalando o serviço do trabalho de banco de dados elástico](sql-database-elastic-jobs-service-installation.md).</span><span class="sxs-lookup"><span data-stu-id="681d4-115">See [Installing the elastic database job service](sql-database-elastic-jobs-service-installation.md).</span></span>

## <a name="creating-jobs"></a><span data-ttu-id="681d4-116">Criando trabalhos</span><span class="sxs-lookup"><span data-stu-id="681d4-116">Creating jobs</span></span>
1. <span data-ttu-id="681d4-117">Usando o [Portal do Azure](https://portal.azure.com), de um pool de trabalho de banco de dados elástico existente, clique em **Criar trabalho**.</span><span class="sxs-lookup"><span data-stu-id="681d4-117">Using the [Azure portal](https://portal.azure.com), from an existing elastic database job pool, click **Create job**.</span></span>
2. <span data-ttu-id="681d4-118">Digite o nome de usuário e a senha do administrador do banco de dados (criado na instalação dos Trabalhos) para o banco de dados de controle de trabalhos (armazenamento de metadados para trabalhos).</span><span class="sxs-lookup"><span data-stu-id="681d4-118">Type in the username and password of the database administrator (created at installation of Jobs) for the jobs control database (metadata storage for jobs).</span></span>
   
    ![Nomeie o trabalho, digite ou cole o código e clique em Executar][1]
3. <span data-ttu-id="681d4-120">Na folha **Criar trabalho** , digite um nome para o trabalho.</span><span class="sxs-lookup"><span data-stu-id="681d4-120">In the **Create Job** blade, type a name for the job.</span></span>
4. <span data-ttu-id="681d4-121">Digite o nome de usuário e a senha para se conectar aos bancos de dados de destino com permissões suficientes para que a execução do script seja bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="681d4-121">Type the user name and password to connect to the target databases with sufficient permissions for script execution to succeed.</span></span>
5. <span data-ttu-id="681d4-122">Cole ou digite o script T-SQL.</span><span class="sxs-lookup"><span data-stu-id="681d4-122">Paste or type in the T-SQL script.</span></span>
6. <span data-ttu-id="681d4-123">Clique em **Salvar** e em **Executar**.</span><span class="sxs-lookup"><span data-stu-id="681d4-123">Click **Save** and then click **Run**.</span></span>
   
    ![Criar trabalhos e executar][5]

## <a name="run-idempotent-jobs"></a><span data-ttu-id="681d4-125">Executar trabalhos idempotentes</span><span class="sxs-lookup"><span data-stu-id="681d4-125">Run idempotent jobs</span></span>
<span data-ttu-id="681d4-126">Quando você executa um script em um conjunto de bancos de dados, certifique-se de que o script seja idempotente.</span><span class="sxs-lookup"><span data-stu-id="681d4-126">When you run a script against a set of databases, you must be sure that the script is idempotent.</span></span> <span data-ttu-id="681d4-127">Ou seja, o script deve ser capaz de executar várias vezes, mesmo se tiver falhado antes em um estado incompleto.</span><span class="sxs-lookup"><span data-stu-id="681d4-127">That is, the script must be able to run multiple times, even if it has failed before in an incomplete state.</span></span> <span data-ttu-id="681d4-128">Por exemplo, quando um script falha, o trabalho é repetido automaticamente até obter êxito (dentro dos limites, uma vez que lógica de nova tentativa eventualmente deixará de tentar novamente).</span><span class="sxs-lookup"><span data-stu-id="681d4-128">For example, when a script fails, the job will be automatically retried until it succeeds (within limits, as the retry logic will eventually cease the retrying).</span></span> <span data-ttu-id="681d4-129">A maneira de fazer isso é usar a cláusula "IF EXISTS" e excluir qualquer instância encontrada antes de criar um novo objeto.</span><span class="sxs-lookup"><span data-stu-id="681d4-129">The way to do this is to use the an "IF EXISTS" clause and delete any found instance before creating a new object.</span></span> <span data-ttu-id="681d4-130">Veja um exemplo aqui:</span><span class="sxs-lookup"><span data-stu-id="681d4-130">An example is shown here:</span></span>

    IF EXISTS (SELECT name FROM sys.indexes
            WHERE name = N'IX_ProductVendor_VendorID')
    DROP INDEX IX_ProductVendor_VendorID ON Purchasing.ProductVendor;
    GO
    CREATE INDEX IX_ProductVendor_VendorID
    ON Purchasing.ProductVendor (VendorID);

<span data-ttu-id="681d4-131">Como alternativa, use uma cláusula "IF NOT EXISTS" antes de criar uma nova instância:</span><span class="sxs-lookup"><span data-stu-id="681d4-131">Alternatively, use an "IF NOT EXISTS" clause before creating a new instance:</span></span>

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

<span data-ttu-id="681d4-132">Em seguida, esse script atualiza a tabela criada anteriormente.</span><span class="sxs-lookup"><span data-stu-id="681d4-132">This script then updates the table created previously.</span></span>

    IF NOT EXISTS (SELECT columns.name FROM sys.columns INNER JOIN sys.tables on columns.object_id = tables.object_id WHERE tables.name = 'TestTable' AND columns.name = 'AdditionalInformation')
    BEGIN

    ALTER TABLE TestTable

    ADD AdditionalInformation NVARCHAR(400);
    END
    GO

    INSERT INTO TestTable(InsertionTime, AdditionalInformation) VALUES (sysutcdatetime(), 'test');
    GO


## <a name="checking-job-status"></a><span data-ttu-id="681d4-133">Verificando o status do trabalho</span><span class="sxs-lookup"><span data-stu-id="681d4-133">Checking job status</span></span>
<span data-ttu-id="681d4-134">Após o início de um trabalho, você pode verificar seu andamento.</span><span class="sxs-lookup"><span data-stu-id="681d4-134">After a job has begun, you can check on its progress.</span></span>

1. <span data-ttu-id="681d4-135">Na página do pool elástico, clique em **Gerenciar trabalhos**.</span><span class="sxs-lookup"><span data-stu-id="681d4-135">From the elastic pool page, click **Manage jobs**.</span></span>
   
    ![Clique em “Gerenciar trabalhos”][2]
2. <span data-ttu-id="681d4-137">Clique no nome (a) de um trabalho.</span><span class="sxs-lookup"><span data-stu-id="681d4-137">Click on the name (a) of a job.</span></span> <span data-ttu-id="681d4-138">O **STATUS** pode ser "Concluído" ou "Falha".</span><span class="sxs-lookup"><span data-stu-id="681d4-138">The **STATUS** can be "Completed" or "Failed."</span></span> <span data-ttu-id="681d4-139">Os detalhes do trabalho aparecem (b) com sua data e hora de criação e execução.</span><span class="sxs-lookup"><span data-stu-id="681d4-139">The job's details appear (b) with its date and time of creation and running.</span></span> <span data-ttu-id="681d4-140">A lista (c) abaixo mostra o progresso do script em cada banco de dados no pool, oferecendo detalhes de data e hora.</span><span class="sxs-lookup"><span data-stu-id="681d4-140">The list (c) below the that shows the progress of the script against each database in the pool, giving its date and time details.</span></span>
   
    ![Verificando um trabalho concluído][3]

## <a name="checking-failed-jobs"></a><span data-ttu-id="681d4-142">Verificação de trabalhos com falha</span><span class="sxs-lookup"><span data-stu-id="681d4-142">Checking failed jobs</span></span>
<span data-ttu-id="681d4-143">Se um trabalho falhar, será possível encontrar um log de sua execução.</span><span class="sxs-lookup"><span data-stu-id="681d4-143">If a job fails, a log of its execution can found.</span></span> <span data-ttu-id="681d4-144">Clique no nome do trabalho com falha para ver seus detalhes.</span><span class="sxs-lookup"><span data-stu-id="681d4-144">Click the name of the failed job to see its details.</span></span>

![Verificar um trabalho com falha][4]

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-jobs-create-and-manage/screen-1.png
[2]: ./media/sql-database-elastic-jobs-create-and-manage/click-manage-jobs.png
[3]: ./media/sql-database-elastic-jobs-create-and-manage/running-jobs.png
[4]: ./media/sql-database-elastic-jobs-create-and-manage/failed.png
[5]: ./media/sql-database-elastic-jobs-create-and-manage/screen-2.png


