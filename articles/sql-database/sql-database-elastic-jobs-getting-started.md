---
title: "aaaGetting iniciado com trabalhos do banco de dados Elástico | Microsoft Docs"
description: "como trabalhos do banco de dados Elástico toouse"
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
ms.assetid: 2540de0e-2235-4cdd-9b6a-b841adba00e5
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/06/2016
ms.author: ddove
ms.openlocfilehash: bc5894d2df4235738ab961db4f69c11cdf786cc6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-elastic-database-jobs"></a><span data-ttu-id="ca7a8-103">Introdução a trabalhos de Banco de Dados Elástico</span><span class="sxs-lookup"><span data-stu-id="ca7a8-103">Getting started with Elastic Database jobs</span></span>
<span data-ttu-id="ca7a8-104">Trabalhos do banco de dados Elásticos (visualização) para o banco de dados do Azure SQL permite que você tooreliability executar scripts do T-SQL que abrangem vários bancos de dados ao repetir automaticamente e fornecer eventual conclusão garantia.</span><span class="sxs-lookup"><span data-stu-id="ca7a8-104">Elastic Database jobs (preview) for Azure SQL Database allows you tooreliability execute T-SQL scripts that span multiple databases while automatically retrying and providing eventual completion guarantees.</span></span> <span data-ttu-id="ca7a8-105">Para obter mais informações sobre o recurso de trabalho de banco de dados Elástico Olá, consulte Olá [página de visão geral do recurso](sql-database-elastic-jobs-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ca7a8-105">For more information about hello Elastic Database job feature, please see hello [feature overview page](sql-database-elastic-jobs-overview.md).</span></span>

<span data-ttu-id="ca7a8-106">Este tópico estende o exemplo hello encontrado no [Introdução às ferramentas de banco de dados Elástico](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="ca7a8-106">This topic extends hello sample found in [Getting started with Elastic Database tools](sql-database-elastic-scale-get-started.md).</span></span> <span data-ttu-id="ca7a8-107">Quando concluído, você verá: Saiba como toocreate e gerenciar trabalhos que gerenciar um grupo de bancos de dados relacionados.</span><span class="sxs-lookup"><span data-stu-id="ca7a8-107">When completed, you will: learn how toocreate and manage jobs that manage a group of related databases.</span></span> <span data-ttu-id="ca7a8-108">Não é necessário toouse Olá escala elástica ferramentas em ordem tootake máximo Olá benefícios da Elásticos trabalhos.</span><span class="sxs-lookup"><span data-stu-id="ca7a8-108">It is not required toouse hello Elastic Scale tools in order tootake advantage of hello benefits of Elastic jobs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ca7a8-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="ca7a8-109">Prerequisites</span></span>
<span data-ttu-id="ca7a8-110">Baixe e execute Olá [guia de Introdução com amostra das ferramentas de banco de dados Elástico](sql-database-elastic-scale-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="ca7a8-110">Download and run hello [Getting started with Elastic Database tools sample](sql-database-elastic-scale-get-started.md).</span></span>

## <a name="create-a-shard-map-manager-using-hello-sample-app"></a><span data-ttu-id="ca7a8-111">Criar um mapa do fragmento manager usando o aplicativo de exemplo hello</span><span class="sxs-lookup"><span data-stu-id="ca7a8-111">Create a shard map manager using hello sample app</span></span>
<span data-ttu-id="ca7a8-112">Aqui você criará um mapa do fragmento manager juntamente com vários fragmentos, seguido de inserção de dados em fragmentos hello.</span><span class="sxs-lookup"><span data-stu-id="ca7a8-112">Here you will create a shard map manager along with several shards, followed by insertion of data into hello shards.</span></span> <span data-ttu-id="ca7a8-113">Se você já tiver configurado com dados fragmentados de fragmentos, você pode ignorar Olá etapas a seguir e mover toohello próxima seção.</span><span class="sxs-lookup"><span data-stu-id="ca7a8-113">If you already have shards set up with sharded data in them, you can skip hello following steps and move toohello next section.</span></span>

1. <span data-ttu-id="ca7a8-114">Compilar e executar Olá **Introdução às ferramentas de banco de dados Elástico** aplicativo de exemplo.</span><span class="sxs-lookup"><span data-stu-id="ca7a8-114">Build and run hello **Getting started with Elastic Database tools** sample application.</span></span> <span data-ttu-id="ca7a8-115">Execute as etapas de saudação até a etapa 7 na seção Olá [Baixe e execute o aplicativo de exemplo hello](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app).</span><span class="sxs-lookup"><span data-stu-id="ca7a8-115">Follow hello steps until step 7 in hello section [Download and run hello sample app](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app).</span></span> <span data-ttu-id="ca7a8-116">No final da saudação da etapa 7, você verá saudação de prompt de comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="ca7a8-116">At hello end of Step 7, you will see hello following command prompt:</span></span>

   ![prompt de comando](./media/sql-database-elastic-query-getting-started/cmd-prompt.png)

2. <span data-ttu-id="ca7a8-118">Na janela de comando hello, digite "1" e pressione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="ca7a8-118">In hello command window, type "1" and press **Enter**.</span></span> <span data-ttu-id="ca7a8-119">Isso cria o Gerenciador do mapa de fragmentos Olá e adiciona dois servidores toohello de fragmentos.</span><span class="sxs-lookup"><span data-stu-id="ca7a8-119">This creates hello shard map manager, and adds two shards toohello server.</span></span> <span data-ttu-id="ca7a8-120">Em seguida, digite "3" e pressione **Enter**. Repita essa ação quatro vezes.</span><span class="sxs-lookup"><span data-stu-id="ca7a8-120">Then type "3" and press **Enter**; repeat this action four times.</span></span> <span data-ttu-id="ca7a8-121">Isso insere linhas de dados de exemplo no seus fragmentos.</span><span class="sxs-lookup"><span data-stu-id="ca7a8-121">This inserts sample data rows in your shards.</span></span>
3. <span data-ttu-id="ca7a8-122">Olá [Portal do Azure](https://portal.azure.com) devem mostrar três novos bancos de dados:</span><span class="sxs-lookup"><span data-stu-id="ca7a8-122">hello [Azure Portal](https://portal.azure.com) should show three new databases:</span></span>

   ![Confirmação do Visual Studio](./media/sql-database-elastic-query-getting-started/portal.png)

   <span data-ttu-id="ca7a8-124">Neste ponto, vamos criar uma coleção de banco de dados personalizado que reflete todos os bancos de dados de Olá no mapa do fragmento hello.</span><span class="sxs-lookup"><span data-stu-id="ca7a8-124">At this point, we will create a custom database collection that reflects all hello databases in hello shard map.</span></span> <span data-ttu-id="ca7a8-125">Isso nos permitirá toocreate e executar um trabalho que adiciona uma nova tabela em fragmentos.</span><span class="sxs-lookup"><span data-stu-id="ca7a8-125">This will allow us toocreate and execute a job that add a new table across shards.</span></span>

<span data-ttu-id="ca7a8-126">Aqui nós geralmente criaria um destino de mapa do fragmento, usando Olá **AzureSqlJobTarget novo** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ca7a8-126">Here we would usually create a shard map target, using hello **New-AzureSqlJobTarget** cmdlet.</span></span> <span data-ttu-id="ca7a8-127">o banco de dados do Hello fragmento mapa manager deve ser definido como um destino de banco de dados e, em seguida, o mapa de fragmentos específicos de saudação é especificado como um destino.</span><span class="sxs-lookup"><span data-stu-id="ca7a8-127">hello shard map manager database must be set as a database target and then hello specific shard map is specified as a target.</span></span> <span data-ttu-id="ca7a8-128">Em vez disso, somos contínuo tooenumerate todos os bancos de dados de Olá no servidor de saudação e adicionar Olá bancos de dados toohello nova coleção personalizada com exceção de saudação do banco de dados mestre.</span><span class="sxs-lookup"><span data-stu-id="ca7a8-128">Instead, we are going tooenumerate all hello databases in hello server and add hello databases toohello new custom collection with hello exception of master database.</span></span>

## <a name="creates-a-custom-collection-and-add-all-databases-in-hello-server-toohello-custom-collection-target-with-hello-exception-of-master"></a><span data-ttu-id="ca7a8-129">Cria uma coleção personalizada e adicionar todos os bancos de dados de destino da coleção personalizada toohello Olá server com exceção de saudação do mestre.</span><span class="sxs-lookup"><span data-stu-id="ca7a8-129">Creates a custom collection and add all databases in hello server toohello custom collection target with hello exception of master.</span></span>
   ```
    $customCollectionName = "dbs_in_server"
    New-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $ResourceGroupName = "ddove_samples"
    $ServerName = "samples"
    $dbsinserver = Get-AzureRMSqlDatabase -ResourceGroupName $ResourceGroupName -ServerName $ServerName
    $dbsinserver | %{
    $currentdb = $_.DatabaseName
    $ErrorActionPreference = "Stop"
    Write-Output ""

    Try
    {
       New-AzureSqlJobTarget -ServerName $ServerName -DatabaseName $currentdb | Write-Output
    }
    Catch
    {
        $ErrorMessage = $_.Exception.Message
        $ErrorCategory = $_.CategoryInfo.Reason

        if ($ErrorCategory -eq 'UniqueConstraintViolatedException')
        {
             Write-Host $currentdb "is already a database target."
        }

        else
        {
            throw $_
        }

    }

    Try
    {
        if ($currentdb -eq "master")
        {
            Write-Host $currentdb "will not be added custom collection target" $CustomCollectionName "."
        }

        else
        {
            Add-AzureSqlJobChildTarget -CustomCollectionName $CustomCollectionName -ServerName $ServerName -DatabaseName $currentdb
            Write-Host $currentdb "was added to" $CustomCollectionName "."
        }

    }
    Catch
    {
        $ErrorMessage = $_.Exception.Message
        $ErrorCategory = $_.CategoryInfo.Reason

        if ($ErrorCategory -eq 'UniqueConstraintViolatedException')
        {
             Write-Host $currentdb "is already in hello custom collection target" $CustomCollectionName"."
        }

        else
        {
            throw $_
        }
    }
    $ErrorActionPreference = "Continue"
   }
   ```
## <a name="create-a-t-sql-script-for-execution-across-databases"></a><span data-ttu-id="ca7a8-130">Criar um script T-SQL para execução em bancos de dados</span><span class="sxs-lookup"><span data-stu-id="ca7a8-130">Create a T-SQL Script for execution across databases</span></span>
   ```
    $scriptName = "NewTable"
    $scriptCommandText = "
    IF NOT EXISTS (SELECT name FROM sys.tables WHERE name = 'Test')
    BEGIN
        CREATE TABLE Test(
            TestId INT PRIMARY KEY IDENTITY,
            InsertionTime DATETIME2
        );
    END
    GO
    INSERT INTO Test(InsertionTime) VALUES (sysutcdatetime());
    GO"

    $script = New-AzureSqlJobContent -ContentName $scriptName -CommandText $scriptCommandText
    Write-Output $script
   ```

## <a name="create-hello-job-tooexecute-a-script-across-hello-custom-group-of-databases"></a><span data-ttu-id="ca7a8-131">Criar um script de saudação trabalho tooexecute em grupo personalizado de saudação de bancos de dados</span><span class="sxs-lookup"><span data-stu-id="ca7a8-131">Create hello job tooexecute a script across hello custom group of databases</span></span>

   ```
    $jobName = "create on server dbs"
    $scriptName = "NewTable"
    $customCollectionName = "dbs_in_server"
    $credentialName = "ddove66"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $credentialName -ContentName $scriptName -TargetId $target.TargetId
    Write-Output $job
   ```

## <a name="execute-hello-job"></a><span data-ttu-id="ca7a8-132">Executar trabalho Olá</span><span class="sxs-lookup"><span data-stu-id="ca7a8-132">Execute hello job</span></span>
<span data-ttu-id="ca7a8-133">saudação de script do PowerShell a seguir pode ser usado tooexecute um trabalho existente:</span><span class="sxs-lookup"><span data-stu-id="ca7a8-133">hello following PowerShell script can be used tooexecute an existing job:</span></span>

<span data-ttu-id="ca7a8-134">Atualize Olá tooreflect variável Olá desejado trabalho nome toohave executada a seguir:</span><span class="sxs-lookup"><span data-stu-id="ca7a8-134">Update hello following variable tooreflect hello desired job name toohave executed:</span></span>

   ```
    $jobName = "create on server dbs"
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName
    Write-Output $jobExecution
   ```

## <a name="retrieve-hello-state-of-a-single-job-execution"></a><span data-ttu-id="ca7a8-135">Recuperar o estado de saudação de uma execução de trabalho</span><span class="sxs-lookup"><span data-stu-id="ca7a8-135">Retrieve hello state of a single job execution</span></span>
<span data-ttu-id="ca7a8-136">Use Olá mesmo **Get-AzureSqlJobExecution** cmdlet com hello **IncludeChildren** estado de saudação do parâmetro tooview de execuções do trabalho filho, ou seja, Olá estado específico para cada execução do trabalho em relação a cada banco de dados de destino pelo trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="ca7a8-136">Use hello same **Get-AzureSqlJobExecution** cmdlet with hello **IncludeChildren** parameter tooview hello state of child job executions, namely hello specific state for each job execution against each database targeted by hello job.</span></span>

   ```
    $jobExecutionId = "{Job Execution Id}"
    $jobExecutions = Get-AzureSqlJobExecution -JobExecutionId $jobExecutionId -IncludeChildren
    Write-Output $jobExecutions
   ```

## <a name="view-hello-state-across-multiple-job-executions"></a><span data-ttu-id="ca7a8-137">Estado de exibição Olá entre várias execuções de trabalho</span><span class="sxs-lookup"><span data-stu-id="ca7a8-137">View hello state across multiple job executions</span></span>
<span data-ttu-id="ca7a8-138">Olá **AzureSqlJobExecution Get** cmdlet tem vários parâmetros opcionais que podem ser usado toodisplay várias execuções de trabalho, filtradas por meio de parâmetros de saudação fornecido.</span><span class="sxs-lookup"><span data-stu-id="ca7a8-138">hello **Get-AzureSqlJobExecution** cmdlet has multiple optional parameters that can be used toodisplay multiple job executions, filtered through hello provided parameters.</span></span> <span data-ttu-id="ca7a8-139">Olá segue uma demonstração de algumas das maneiras possíveis de saudação toouse AzureSqlJobExecution Get:</span><span class="sxs-lookup"><span data-stu-id="ca7a8-139">hello following demonstrates some of hello possible ways toouse Get-AzureSqlJobExecution:</span></span>

<span data-ttu-id="ca7a8-140">Recupere todas as execuções de trabalhos ativos de nível superior:</span><span class="sxs-lookup"><span data-stu-id="ca7a8-140">Retrieve all active top level job executions:</span></span>

   ```
    Get-AzureSqlJobExecution
   ```

<span data-ttu-id="ca7a8-141">Recupere todas as execuções do trabalho de nível superior, incluindo execuções de trabalhos inativos:</span><span class="sxs-lookup"><span data-stu-id="ca7a8-141">Retrieve all top level job executions, including inactive job executions:</span></span>

   ```
    Get-AzureSqlJobExecution -IncludeInactive
   ```

<span data-ttu-id="ca7a8-142">Recupere todas as execuções de trabalhos filho de uma ID de execução de trabalho fornecida, incluindo execuções de trabalhos inativos:</span><span class="sxs-lookup"><span data-stu-id="ca7a8-142">Retrieve all child job executions of a provided job execution ID, including inactive job executions:</span></span>

   ```
    $parentJobExecutionId = "{Job Execution Id}"
    Get-AzureSqlJobExecution -AzureSqlJobExecution -JobExecutionId $parentJobExecutionId -IncludeInactive -IncludeChildren
   ```

<span data-ttu-id="ca7a8-143">Recupere todas as execuções de trabalho criadas usando uma combinação de agenda/trabalho, incluindo trabalhos inativos:</span><span class="sxs-lookup"><span data-stu-id="ca7a8-143">Retrieve all job executions created using a schedule / job combination, including inactive jobs:</span></span>

   ```
    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Get-AzureSqlJobExecution -JobName $jobName -ScheduleName $scheduleName -IncludeInactive
   ```

<span data-ttu-id="ca7a8-144">Recupere todos os trabalhos direcionados a um mapa de fragmentos especificado, incluindo trabalhos inativos:</span><span class="sxs-lookup"><span data-stu-id="ca7a8-144">Retrieve all jobs targeting a specified shard map, including inactive jobs:</span></span>

   ```
    $shardMapServerName = "{Shard Map Server Name}"
    $shardMapDatabaseName = "{Shard Map Database Name}"
    $shardMapName = "{Shard Map Name}"
    $target = Get-AzureSqlJobTarget -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapServerName -ShardMapName $shardMapName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive
   ```

<span data-ttu-id="ca7a8-145">Recupere todos os trabalhos direcionados a uma coleção personalizada especificada, incluindo trabalhos inativos:</span><span class="sxs-lookup"><span data-stu-id="ca7a8-145">Retrieve all jobs targeting a specified custom collection, including inactive jobs:</span></span>

   ```
    $customCollectionName = "{Custom Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive
   ```

<span data-ttu-id="ca7a8-146">Recupere a lista de saudação de execuções de tarefa de trabalho em uma execução de trabalho específico:</span><span class="sxs-lookup"><span data-stu-id="ca7a8-146">Retrieve hello list of job task executions within a specific job execution:</span></span>

   ```
    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Write-Output $jobTaskExecutions
   ```

<span data-ttu-id="ca7a8-147">Recupere detalhes de execução de tarefa de trabalho:</span><span class="sxs-lookup"><span data-stu-id="ca7a8-147">Retrieve job task execution details:</span></span>

<span data-ttu-id="ca7a8-148">saudação de script do PowerShell a seguir pode ser usado tooview Olá detalhes de uma execução de tarefa do trabalho, é particularmente útil ao depurar falhas de execução.</span><span class="sxs-lookup"><span data-stu-id="ca7a8-148">hello following PowerShell script can be used tooview hello details of a job task execution, which is particularly useful when debugging execution failures.</span></span>
   ```
    $jobTaskExecutionId = "{Job Task Execution Id}"
    $jobTaskExecution = Get-AzureSqlJobTaskExecution -JobTaskExecutionId $jobTaskExecutionId
    Write-Output $jobTaskExecution
   ```

## <a name="retrieve-failures-within-job-task-executions"></a><span data-ttu-id="ca7a8-149">Recuperar falhas em execuções de tarefa de trabalho</span><span class="sxs-lookup"><span data-stu-id="ca7a8-149">Retrieve failures within job task executions</span></span>
<span data-ttu-id="ca7a8-150">objeto de JobTaskExecution Olá inclui uma propriedade para o ciclo de vida de tarefa Olá junto com uma propriedade de mensagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="ca7a8-150">hello JobTaskExecution object includes a property for hello Lifecycle of hello task along with a Message property.</span></span> <span data-ttu-id="ca7a8-151">Se uma execução de tarefa de trabalho falhou, Olá do ciclo de vida de propriedade será definido muito*falha* e propriedade de mensagem de saudação será definida toohello mensagem de exceção resultante e sua pilha.</span><span class="sxs-lookup"><span data-stu-id="ca7a8-151">If a job task execution failed, hello Lifecycle property will be set too*Failed* and hello Message property will be set toohello resulting exception message and its stack.</span></span> <span data-ttu-id="ca7a8-152">Se um trabalho não foi bem-sucedida, é importante tooview detalhes de Olá das tarefas de trabalho que não teve êxito para um determinado trabalho.</span><span class="sxs-lookup"><span data-stu-id="ca7a8-152">If a job did not succeed, it is important tooview hello details of job tasks that did not succeed for a given job.</span></span>

   ```
    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Foreach($jobTaskExecution in $jobTaskExecutions)
        {
        if($jobTaskExecution.Lifecycle -ne 'Succeeded')
            {
            Write-Output $jobTaskExecution
            }
        }
   ```

## <a name="waiting-for-a-job-execution-toocomplete"></a><span data-ttu-id="ca7a8-153">Aguardando um toocomplete de execução do trabalho</span><span class="sxs-lookup"><span data-stu-id="ca7a8-153">Waiting for a job execution toocomplete</span></span>
<span data-ttu-id="ca7a8-154">Olá script do PowerShell a seguir pode ser usado toowait para um toocomplete de tarefa do trabalho:</span><span class="sxs-lookup"><span data-stu-id="ca7a8-154">hello following PowerShell script can be used toowait for a job task toocomplete:</span></span>

   ```
    $jobExecutionId = "{Job Execution Id}"
    Wait-AzureSqlJobExecution -JobExecutionId $jobExecutionId
   ```

## <a name="create-a-custom-execution-policy"></a><span data-ttu-id="ca7a8-155">Criar uma política de execução personalizada</span><span class="sxs-lookup"><span data-stu-id="ca7a8-155">Create a custom execution policy</span></span>
<span data-ttu-id="ca7a8-156">O recurso trabalhos de Banco de Dados Elástico dá suporte à criação de políticas de execução personalizadas, que podem ser aplicadas ao iniciar trabalhos.</span><span class="sxs-lookup"><span data-stu-id="ca7a8-156">Elastic Database jobs supports creating custom execution policies that can be applied when starting jobs.</span></span>

<span data-ttu-id="ca7a8-157">Atualmente, as políticas de execução permitem definir:</span><span class="sxs-lookup"><span data-stu-id="ca7a8-157">Execution policies currently allow for defining:</span></span>

* <span data-ttu-id="ca7a8-158">Nome: O identificador de política de execução de saudação.</span><span class="sxs-lookup"><span data-stu-id="ca7a8-158">Name: Identifier for hello execution policy.</span></span>
* <span data-ttu-id="ca7a8-159">Tempo Limite do Trabalho: tempo total antes que um trabalho seja cancelado pelo recurso Trabalhos de Banco de Dados Elástico.</span><span class="sxs-lookup"><span data-stu-id="ca7a8-159">Job Timeout: Total time before a job will be canceled by Elastic Database Jobs.</span></span>
* <span data-ttu-id="ca7a8-160">Intervalo de repetição inicial: Toowait de intervalo antes da primeira nova tentativa.</span><span class="sxs-lookup"><span data-stu-id="ca7a8-160">Initial Retry Interval: Interval toowait before first retry.</span></span>
* <span data-ttu-id="ca7a8-161">Intervalo de repetição máximo: Limite de toouse de intervalos de repetição.</span><span class="sxs-lookup"><span data-stu-id="ca7a8-161">Maximum Retry Interval: Cap of retry intervals toouse.</span></span>
* <span data-ttu-id="ca7a8-162">Coeficiente de retirada de intervalo de repetição: Coeficiente usado toocalculate Olá próximo intervalo entre repetições.</span><span class="sxs-lookup"><span data-stu-id="ca7a8-162">Retry Interval Backoff Coefficient: Coefficient used toocalculate hello next interval between retries.</span></span>  <span data-ttu-id="ca7a8-163">Olá fórmula a seguir é usada: (intervalo de repetição iniciais) * Math.pow ((coeficiente de retirada de intervalo), (número de tentativas de) - 2).</span><span class="sxs-lookup"><span data-stu-id="ca7a8-163">hello following formula is used: (Initial Retry Interval) * Math.pow((Interval Backoff Coefficient), (Number of Retries) - 2).</span></span>
* <span data-ttu-id="ca7a8-164">Máximo de tentativas: número máximo de saudação de tooperform de tentativas de repetição dentro de um trabalho.</span><span class="sxs-lookup"><span data-stu-id="ca7a8-164">Maximum Attempts: hello maximum number of retry attempts tooperform within a job.</span></span>

<span data-ttu-id="ca7a8-165">política de execução padrão Olá usa Olá valores a seguir:</span><span class="sxs-lookup"><span data-stu-id="ca7a8-165">hello default execution policy uses hello following values:</span></span>

* <span data-ttu-id="ca7a8-166">Nome: política de execução padrão</span><span class="sxs-lookup"><span data-stu-id="ca7a8-166">Name: Default execution policy</span></span>
* <span data-ttu-id="ca7a8-167">Tempo Limite do Trabalho: 1 semana</span><span class="sxs-lookup"><span data-stu-id="ca7a8-167">Job Timeout: 1 week</span></span>
* <span data-ttu-id="ca7a8-168">Intervalo de Repetição Inicial: 100 milissegundos</span><span class="sxs-lookup"><span data-stu-id="ca7a8-168">Initial Retry Interval:  100 milliseconds</span></span>
* <span data-ttu-id="ca7a8-169">Intervalo Máximo de Repetição: 30 minutos</span><span class="sxs-lookup"><span data-stu-id="ca7a8-169">Maximum Retry Interval: 30 minutes</span></span>
* <span data-ttu-id="ca7a8-170">Coeficiente de Intervalo de Repetição: 2</span><span class="sxs-lookup"><span data-stu-id="ca7a8-170">Retry Interval Coefficient: 2</span></span>
* <span data-ttu-id="ca7a8-171">Máximo de Tentativas: 2.147.483.647</span><span class="sxs-lookup"><span data-stu-id="ca7a8-171">Maximum Attempts: 2,147,483,647</span></span>

<span data-ttu-id="ca7a8-172">Crie política de execução de saudação desejada:</span><span class="sxs-lookup"><span data-stu-id="ca7a8-172">Create hello desired execution policy:</span></span>

   ```
    $executionPolicyName = "{Execution Policy Name}"
    $initialRetryInterval = New-TimeSpan -Seconds 10
    $jobTimeout = New-TimeSpan -Minutes 30
    $maximumAttempts = 999999
    $maximumRetryInterval = New-TimeSpan -Minutes 1
    $retryIntervalBackoffCoefficient = 1.5
    $executionPolicy = New-AzureSqlJobExecutionPolicy -ExecutionPolicyName $executionPolicyName -InitialRetryInterval $initialRetryInterval -JobTimeout $jobTimeout -MaximumAttempts $maximumAttempts -MaximumRetryInterval $maximumRetryInterval -RetryIntervalBackoffCoefficient $retryIntervalBackoffCoefficient
    Write-Output $executionPolicy
   ```

### <a name="update-a-custom-execution-policy"></a><span data-ttu-id="ca7a8-173">Atualizar uma política de execução personalizada</span><span class="sxs-lookup"><span data-stu-id="ca7a8-173">Update a custom execution policy</span></span>
<span data-ttu-id="ca7a8-174">Atualize tooupdate de política de execução de saudação desejada:</span><span class="sxs-lookup"><span data-stu-id="ca7a8-174">Update hello desired execution policy tooupdate:</span></span>

   ```
    $executionPolicyName = "{Execution Policy Name}"
    $initialRetryInterval = New-TimeSpan -Seconds 15
    $jobTimeout = New-TimeSpan -Minutes 30
    $maximumAttempts = 999999
    $maximumRetryInterval = New-TimeSpan -Minutes 1
    $retryIntervalBackoffCoefficient = 1.5
    $updatedExecutionPolicy = Set-AzureSqlJobExecutionPolicy -ExecutionPolicyName $executionPolicyName -InitialRetryInterval $initialRetryInterval -JobTimeout $jobTimeout -MaximumAttempts $maximumAttempts -MaximumRetryInterval $maximumRetryInterval -RetryIntervalBackoffCoefficient $retryIntervalBackoffCoefficient
    Write-Output $updatedExecutionPolicy
   ```

## <a name="cancel-a-job"></a><span data-ttu-id="ca7a8-175">Cancelar um trabalho</span><span class="sxs-lookup"><span data-stu-id="ca7a8-175">Cancel a job</span></span>
<span data-ttu-id="ca7a8-176">Os Trabalhos de Banco de Dados Elástico dão suporte a solicitações de cancelamento de trabalhos.</span><span class="sxs-lookup"><span data-stu-id="ca7a8-176">Elastic Database Jobs supports jobs cancellation requests.</span></span>  <span data-ttu-id="ca7a8-177">Se trabalhos de banco de dados Elástico detectar uma solicitação de cancelamento para um trabalho que está sendo executada no momento, ele tentará toostop trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="ca7a8-177">If Elastic Database Jobs detects a cancellation request for a job currently being executed, it will attempt toostop hello job.</span></span>

<span data-ttu-id="ca7a8-178">Há duas maneiras diferentes pelas quais o recurso Trabalhos de Banco de Dados Elástico pode executar um cancelamento:</span><span class="sxs-lookup"><span data-stu-id="ca7a8-178">There are two different ways that Elastic Database Jobs can perform a cancellation:</span></span>

1. <span data-ttu-id="ca7a8-179">Cancelando executando tarefas: se um cancelamento for detectado enquanto uma tarefa estiver em execução, um cancelamento será tentado no hello aspecto da tarefa de saudação em execução no momento.</span><span class="sxs-lookup"><span data-stu-id="ca7a8-179">Canceling Currently Executing Tasks: If a cancellation is detected while a task is currently running, a cancellation will be attempted within hello currently executing aspect of hello task.</span></span>  <span data-ttu-id="ca7a8-180">Por exemplo: se houver atualmente sendo executada quando uma tentativa de um cancelamento de consultas de longa execução, haverá uma consulta de saudação toocancel tentativa.</span><span class="sxs-lookup"><span data-stu-id="ca7a8-180">For example: If there is a long running query currently being performed when a cancellation is attempted, there will be an attempt toocancel hello query.</span></span>
2. <span data-ttu-id="ca7a8-181">Cancelando tentativas de tarefa: Se um cancelamento for detectado pelo thread de controle de saudação antes de uma tarefa é iniciada para execução, thread de controle Olá evitar iniciar tarefa hello e as declarar solicitação hello como cancelada.</span><span class="sxs-lookup"><span data-stu-id="ca7a8-181">Canceling Task Retries: If a cancellation is detected by hello control thread before a task is launched for execution, hello control thread will avoid launching hello task and declare hello request as canceled.</span></span>

<span data-ttu-id="ca7a8-182">Se for solicitado um cancelamento de trabalho para um trabalho pai, solicitação de cancelamento hello será respeitada para trabalho de pai hello e para todos os seus trabalhos filho.</span><span class="sxs-lookup"><span data-stu-id="ca7a8-182">If a job cancellation is requested for a parent job, hello cancellation request will be honored for hello parent job and for all of its child jobs.</span></span>

<span data-ttu-id="ca7a8-183">toosubmit uma solicitação de cancelamento, use Olá **Stop AzureSqlJobExecution** cmdlet e conjunto hello **JobExecutionId** parâmetro.</span><span class="sxs-lookup"><span data-stu-id="ca7a8-183">toosubmit a cancellation request, use hello **Stop-AzureSqlJobExecution** cmdlet and set hello **JobExecutionId** parameter.</span></span>

   ```
    $jobExecutionId = "{Job Execution Id}"
    Stop-AzureSqlJobExecution -JobExecutionId $jobExecutionId
   ```

## <a name="delete-a-job-by-name-and-hello-jobs-history"></a><span data-ttu-id="ca7a8-184">Excluir um trabalho por nome e o histórico do trabalho Olá</span><span class="sxs-lookup"><span data-stu-id="ca7a8-184">Delete a job by name and hello job's history</span></span>
<span data-ttu-id="ca7a8-185">O recurso trabalhos de Banco de Dados Elástico dá suporte à exclusão assíncrona de trabalhos.</span><span class="sxs-lookup"><span data-stu-id="ca7a8-185">Elastic Database jobs supports asynchronous deletion of jobs.</span></span> <span data-ttu-id="ca7a8-186">Um trabalho pode ser marcado para exclusão e sistema Olá excluirá trabalho hello e todo o seu histórico de trabalho depois de concluir todas as execuções de trabalho para o trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="ca7a8-186">A job can be marked for deletion and hello system will delete hello job and all its job history after all job executions have completed for hello job.</span></span> <span data-ttu-id="ca7a8-187">sistema de saudação não cancelará automaticamente execuções de trabalho ativo.</span><span class="sxs-lookup"><span data-stu-id="ca7a8-187">hello system will not automatically cancel active job executions.</span></span>  

<span data-ttu-id="ca7a8-188">Em vez disso, Stop-AzureSqlJobExecution deve ser invocado toocancel execuções de trabalho ativo.</span><span class="sxs-lookup"><span data-stu-id="ca7a8-188">Instead, Stop-AzureSqlJobExecution must be invoked toocancel active job executions.</span></span>

<span data-ttu-id="ca7a8-189">tootrigger exclusão de trabalho, use Olá **remover AzureSqlJob** cmdlet e conjunto hello **JobName** parâmetro.</span><span class="sxs-lookup"><span data-stu-id="ca7a8-189">tootrigger job deletion, use hello **Remove-AzureSqlJob** cmdlet and set hello **JobName** parameter.</span></span>

   ```
    $jobName = "{Job Name}"
    Remove-AzureSqlJob -JobName $jobName
   ```

## <a name="create-a-custom-database-target"></a><span data-ttu-id="ca7a8-190">Criar um destino de banco de dados personalizado</span><span class="sxs-lookup"><span data-stu-id="ca7a8-190">Create a custom database target</span></span>
<span data-ttu-id="ca7a8-191">Destinos personalizados de banco de dados podem ser definidos no recurso trabalhos de Banco de Dados Elástico, que podem ser usados para execução direta ou para inclusão em um grupo personalizado de bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="ca7a8-191">Custom database targets can be defined in Elastic Database jobs which can be used either for execution directly or for inclusion within a custom database group.</span></span> <span data-ttu-id="ca7a8-192">Como **pools Elásticos** não ainda diretamente têm suporte por meio de APIs do PowerShell do hello, basta criar um destino da coleção de banco de dados personalizado que abrange todos os bancos de dados de saudação no pool de saudação e um destino de banco de dados personalizado.</span><span class="sxs-lookup"><span data-stu-id="ca7a8-192">Since **elastic pools** are not yet directly supported via hello PowerShell APIs, you simply create a custom database target and custom database collection target which encompasses all hello databases in hello pool.</span></span>

<span data-ttu-id="ca7a8-193">Saudação de conjunto de informações de banco de dados variáveis tooreflect Olá desejado a seguir:</span><span class="sxs-lookup"><span data-stu-id="ca7a8-193">Set hello following variables tooreflect hello desired database information:</span></span>

   ```
    $databaseName = "{Database Name}"
    $databaseServerName = "{Server Name}"
    New-AzureSqlJobDatabaseTarget -DatabaseName $databaseName -ServerName $databaseServerName
   ```

## <a name="create-a-custom-database-collection-target"></a><span data-ttu-id="ca7a8-194">Criar um destino para a coleção de bancos de dados personalizada</span><span class="sxs-lookup"><span data-stu-id="ca7a8-194">Create a custom database collection target</span></span>
<span data-ttu-id="ca7a8-195">Um destino de coleção do banco de dados personalizado pode ser definido tooenable execução por vários destinos de banco de dados definido.</span><span class="sxs-lookup"><span data-stu-id="ca7a8-195">A custom database collection target can be defined tooenable execution across multiple defined database targets.</span></span> <span data-ttu-id="ca7a8-196">Após a criação de um grupo de banco de dados, bancos de dados podem ser destino de coleção personalizada toohello associado.</span><span class="sxs-lookup"><span data-stu-id="ca7a8-196">After a database group is created, databases can be associated toohello custom collection target.</span></span>

<span data-ttu-id="ca7a8-197">Definir Olá seguinte configuração de destino variáveis tooreflect Olá coleta personalizado desejado:</span><span class="sxs-lookup"><span data-stu-id="ca7a8-197">Set hello following variables tooreflect hello desired custom collection target configuration:</span></span>

   ```
    $customCollectionName = "{Custom Database Collection Name}"
    New-AzureSqlJobTarget -CustomCollectionName $customCollectionName
   ```

### <a name="add-databases-tooa-custom-database-collection-target"></a><span data-ttu-id="ca7a8-198">Adicionar o destino da coleção de bancos de dados tooa banco de dados personalizado</span><span class="sxs-lookup"><span data-stu-id="ca7a8-198">Add databases tooa custom database collection target</span></span>
<span data-ttu-id="ca7a8-199">Destinos de banco de dados podem ser associados ao banco de dados personalizado coleção destinos toocreate um grupo de bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="ca7a8-199">Database targets can be associated with custom database collection targets toocreate a group of databases.</span></span> <span data-ttu-id="ca7a8-200">Sempre que um trabalho é criado e vinculada a um destino de coleção do banco de dados personalizado, é grupo de toohello associado tootarget expandido Olá bancos de dados em tempo de execução de saudação.</span><span class="sxs-lookup"><span data-stu-id="ca7a8-200">Whenever a job is created that targets a custom database collection target, it will be expanded tootarget hello databases associated toohello group at hello time of execution.</span></span>

<span data-ttu-id="ca7a8-201">Adicione a saudação desejada banco de dados tooa específico personalizado coleta:</span><span class="sxs-lookup"><span data-stu-id="ca7a8-201">Add hello desired database tooa specific custom collection:</span></span>

   ```
    $serverName = "{Database Server Name}"
    $databaseName = "{Database Name}"
    $customCollectionName = "{Custom Database Collection Name}"
    Add-AzureSqlJobChildTarget -CustomCollectionName $customCollectionName -DatabaseName $databaseName -ServerName $databaseServerName
   ```

#### <a name="review-hello-databases-within-a-custom-database-collection-target"></a><span data-ttu-id="ca7a8-202">Revisão Olá bancos de dados dentro de um destino de coleção do banco de dados personalizado</span><span class="sxs-lookup"><span data-stu-id="ca7a8-202">Review hello databases within a custom database collection target</span></span>
<span data-ttu-id="ca7a8-203">Saudação de uso **AzureSqlJobTarget Get** bancos de dados do cmdlet tooretrieve Olá filho dentro de um destino de coleção do banco de dados personalizado.</span><span class="sxs-lookup"><span data-stu-id="ca7a8-203">Use hello **Get-AzureSqlJobTarget** cmdlet tooretrieve hello child databases within a custom database collection target.</span></span>

   ```
    $customCollectionName = "{Custom Database Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $childTargets = Get-AzureSqlJobTarget -ParentTargetId $target.TargetId
    Write-Output $childTargets
   ```

### <a name="create-a-job-tooexecute-a-script-across-a-custom-database-collection-target"></a><span data-ttu-id="ca7a8-204">Criar um script de um trabalho tooexecute em um destino de coleção do banco de dados personalizado</span><span class="sxs-lookup"><span data-stu-id="ca7a8-204">Create a job tooexecute a script across a custom database collection target</span></span>
<span data-ttu-id="ca7a8-205">Saudação de uso **AzureSqlJob novo** cmdlet toocreate um trabalho para um grupo de bancos de dados definidos por um destino de coleção do banco de dados personalizado.</span><span class="sxs-lookup"><span data-stu-id="ca7a8-205">Use hello **New-AzureSqlJob** cmdlet toocreate a job against a group of databases defined by a custom database collection target.</span></span> <span data-ttu-id="ca7a8-206">Trabalhos do banco de dados Elásticos expandirá trabalho Olá para vários trabalhos filho, cada banco de dados tooa correspondente associada ao destino de coleção de banco de dados personalizado hello e certifique-se de que o script hello é executada em cada banco de dados.</span><span class="sxs-lookup"><span data-stu-id="ca7a8-206">Elastic Database jobs will expand hello job into multiple child jobs each corresponding tooa database associated with hello custom database collection target and ensure that hello script is executed against each database.</span></span> <span data-ttu-id="ca7a8-207">Novamente, é importante que os scripts são idempotentes toobe resiliente tooretries.</span><span class="sxs-lookup"><span data-stu-id="ca7a8-207">Again, it is important that scripts are idempotent toobe resilient tooretries.</span></span>

   ```
    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $customCollectionName = "{Custom Collection Name}"
    $credentialName = "{Credential Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $credentialName -ContentName $scriptName -TargetId $target.TargetId
    Write-Output $job
   ```

## <a name="data-collection-across-databases"></a><span data-ttu-id="ca7a8-208">Coleta de dados em bancos de dados</span><span class="sxs-lookup"><span data-stu-id="ca7a8-208">Data collection across databases</span></span>
<span data-ttu-id="ca7a8-209">**Trabalhos do banco de dados Elásticos** suporta a execução de uma consulta em um grupo de bancos de dados e envia a tabela Olá resultados tooa especificado do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="ca7a8-209">**Elastic Database jobs** supports executing a query across a group of databases and sends hello results tooa specified database’s table.</span></span> <span data-ttu-id="ca7a8-210">tabela Olá pode ser consultada depois dos resultados da consulta do hello fatos toosee Olá de cada banco de dados.</span><span class="sxs-lookup"><span data-stu-id="ca7a8-210">hello table can be queried after hello fact toosee hello query’s results from each database.</span></span> <span data-ttu-id="ca7a8-211">Isso fornece um mecanismo assíncrono tooexecute uma consulta em muitos bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="ca7a8-211">This provides an asynchronous mechanism tooexecute a query across many databases.</span></span> <span data-ttu-id="ca7a8-212">Casos de falha, como um dos bancos de dados de saudação está temporariamente indisponível são tratados automaticamente por meio de novas tentativas.</span><span class="sxs-lookup"><span data-stu-id="ca7a8-212">Failure cases such as one of hello databases being temporarily unavailable are handled automatically via retries.</span></span>

<span data-ttu-id="ca7a8-213">tabela de destino especificado Olá será criada automaticamente se ainda não existir, o esquema de saudação correspondente de saudação retornou um conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="ca7a8-213">hello specified destination table will be automatically created if it does not yet exist, matching hello schema of hello returned result set.</span></span> <span data-ttu-id="ca7a8-214">Se uma execução de script retornar vários conjuntos de resultados, os trabalhos de banco de dados Elástico enviará apenas Olá primeiro tabela de destino de um toohello fornecido.</span><span class="sxs-lookup"><span data-stu-id="ca7a8-214">If a script execution returns multiple result sets, Elastic Database jobs will only send hello first one toohello provided destination table.</span></span>

<span data-ttu-id="ca7a8-215">saudação de script do PowerShell a seguir pode ser usado tooexecute um script coletar seus resultados em uma tabela especificada.</span><span class="sxs-lookup"><span data-stu-id="ca7a8-215">hello following PowerShell script can be used tooexecute a script collecting its results into a specified table.</span></span> <span data-ttu-id="ca7a8-216">Este script presume que foi criado um script T-SQL, que produz um único conjunto de resultados; além disso, um destino de coleção de bancos de dados personalizada foi criado.</span><span class="sxs-lookup"><span data-stu-id="ca7a8-216">This script assumes that a T-SQL script has been created which outputs a single result set and a custom database collection target has been created.</span></span>

<span data-ttu-id="ca7a8-217">Definir Olá tooreflect script de saudação desejada, credenciais e o destino de execução a seguir:</span><span class="sxs-lookup"><span data-stu-id="ca7a8-217">Set hello following tooreflect hello desired script, credentials, and execution target:</span></span>

   ```
    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $executionCredentialName = "{Execution Credential Name}"
    $customCollectionName = "{Custom Collection Name}"
    $destinationCredentialName = "{Destination Credential Name}"
    $destinationServerName = "{Destination Server Name}"
    $destinationDatabaseName = "{Destination Database Name}"
    $destinationSchemaName = "{Destination Schema Name}"
    $destinationTableName = "{Destination Table Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
   ```

### <a name="create-and-start-a-job-for-data-collection-scenarios"></a><span data-ttu-id="ca7a8-218">Criar e iniciar um trabalho para cenários de coleta de dados</span><span class="sxs-lookup"><span data-stu-id="ca7a8-218">Create and start a job for data collection scenarios</span></span>
   ```
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $executionCredentialName -ContentName $scriptName -ResultSetDestinationServerName $destinationServerName -ResultSetDestinationDatabaseName $destinationDatabaseName -ResultSetDestinationSchemaName $destinationSchemaName -ResultSetDestinationTableName $destinationTableName -ResultSetDestinationCredentialName $destinationCredentialName -TargetId $target.TargetId
    Write-Output $job
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName
    Write-Output $jobExecution
   ```

## <a name="create-a-schedule-for-job-execution-using-a-job-trigger"></a><span data-ttu-id="ca7a8-219">Criar um agendamento para execução de trabalho usando um gatilho de trabalho</span><span class="sxs-lookup"><span data-stu-id="ca7a8-219">Create a schedule for job execution using a job trigger</span></span>
<span data-ttu-id="ca7a8-220">saudação de script do PowerShell a seguir pode ser usado toocreate um agendamento recorrente.</span><span class="sxs-lookup"><span data-stu-id="ca7a8-220">hello following PowerShell script can be used toocreate a reoccurring schedule.</span></span> <span data-ttu-id="ca7a8-221">Esse script usa um intervalo de minutos, mas o New-AzureSqlJobSchedule também dá suporte aos parâmetros -DayInterval, -HourInterval, -MonthInterval e -WeekInterval.</span><span class="sxs-lookup"><span data-stu-id="ca7a8-221">This script uses a one minute interval, but New-AzureSqlJobSchedule also supports -DayInterval, -HourInterval, -MonthInterval, and -WeekInterval parameters.</span></span> <span data-ttu-id="ca7a8-222">Agendas que são executadas apenas uma vez podem ser criadas pela passagem de -OneTime.</span><span class="sxs-lookup"><span data-stu-id="ca7a8-222">Schedules that execute only once can be created by passing -OneTime.</span></span>

<span data-ttu-id="ca7a8-223">Crie uma nova agenda:</span><span class="sxs-lookup"><span data-stu-id="ca7a8-223">Create a new schedule:</span></span>
   ```
    $scheduleName = "Every one minute"
    $minuteInterval = 1
    $startTime = (Get-Date).ToUniversalTime()
    $schedule = New-AzureSqlJobSchedule -MinuteInterval $minuteInterval -ScheduleName $scheduleName -StartTime $startTime
    Write-Output $schedule
   ```

### <a name="create-a-job-trigger-toohave-a-job-executed-on-a-time-schedule"></a><span data-ttu-id="ca7a8-224">Criar um trabalho executado em um agendamento de tempo de um toohave de gatilho de trabalho</span><span class="sxs-lookup"><span data-stu-id="ca7a8-224">Create a job trigger toohave a job executed on a time schedule</span></span>
<span data-ttu-id="ca7a8-225">Um gatilho de trabalho pode ser definido toohave um agendamento de tempo de tooa acordo do trabalho executado.</span><span class="sxs-lookup"><span data-stu-id="ca7a8-225">A job trigger can be defined toohave a job executed according tooa time schedule.</span></span> <span data-ttu-id="ca7a8-226">saudação de script do PowerShell a seguir pode ser usado toocreate um gatilho de trabalho.</span><span class="sxs-lookup"><span data-stu-id="ca7a8-226">hello following PowerShell script can be used toocreate a job trigger.</span></span>

<span data-ttu-id="ca7a8-227">Saudação de conjunto de variáveis toocorrespond toohello a seguir desejado trabalho e agenda:</span><span class="sxs-lookup"><span data-stu-id="ca7a8-227">Set hello following variables toocorrespond toohello desired job and schedule:</span></span>

   ```
    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    $jobTrigger = New-AzureSqlJobTrigger -ScheduleName $scheduleName -JobName $jobName
    Write-Output $jobTrigger
   ```

### <a name="remove-a-scheduled-association-toostop-job-from-executing-on-schedule"></a><span data-ttu-id="ca7a8-228">Remover um trabalho de toostop de associação agendados sejam executados na agenda</span><span class="sxs-lookup"><span data-stu-id="ca7a8-228">Remove a scheduled association toostop job from executing on schedule</span></span>
<span data-ttu-id="ca7a8-229">toodiscontinue ocorrer a execução de trabalho por meio de um gatilho de trabalho, o gatilho de trabalho Olá pode ser removido.</span><span class="sxs-lookup"><span data-stu-id="ca7a8-229">toodiscontinue reoccurring job execution through a job trigger, hello job trigger can be removed.</span></span>
<span data-ttu-id="ca7a8-230">Remover um gatilho de trabalho toostop um trabalho seja executado acordo agenda tooa usando Olá **AzureSqlJobTrigger remover** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ca7a8-230">Remove a job trigger toostop a job from being executed according tooa schedule using hello **Remove-AzureSqlJobTrigger** cmdlet.</span></span>

   ```
    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Remove-AzureSqlJobTrigger -ScheduleName $scheduleName -JobName $jobName
   ```

## <a name="import-elastic-database-query-results-tooexcel"></a><span data-ttu-id="ca7a8-231">Importar tooExcel de resultados de consulta de banco de dados Elástico</span><span class="sxs-lookup"><span data-stu-id="ca7a8-231">Import elastic database query results tooExcel</span></span>
 <span data-ttu-id="ca7a8-232">Você pode importar resultados de saudação de um consulta tooan do arquivo de Excel.</span><span class="sxs-lookup"><span data-stu-id="ca7a8-232">You can import hello results from of a query tooan Excel file.</span></span>

1. <span data-ttu-id="ca7a8-233">Inicie o Excel 2013.</span><span class="sxs-lookup"><span data-stu-id="ca7a8-233">Launch Excel 2013.</span></span>
2. <span data-ttu-id="ca7a8-234">Navegue toohello **dados** faixa de opções.</span><span class="sxs-lookup"><span data-stu-id="ca7a8-234">Navigate toohello **Data** ribbon.</span></span>
3. <span data-ttu-id="ca7a8-235">Clique em **De Outras Fontes** e em **Do SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="ca7a8-235">Click **From Other Sources** and click **From SQL Server**.</span></span>

   ![Importação de outras fontes para o Excel](./media/sql-database-elastic-query-getting-started/exel-sources.png)

4. <span data-ttu-id="ca7a8-237">Em Olá **Assistente de Conexão de dados** digite credenciais de nome e logon do servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="ca7a8-237">In hello **Data Connection Wizard** type hello server name and login credentials.</span></span> <span data-ttu-id="ca7a8-238">Em seguida, clique em **Próximo**.</span><span class="sxs-lookup"><span data-stu-id="ca7a8-238">Then click **Next**.</span></span>
5. <span data-ttu-id="ca7a8-239">Na caixa de diálogo Olá **banco de dados Olá Select que contém dados Olá deseja**, selecione Olá **ElasticDBQuery** banco de dados.</span><span class="sxs-lookup"><span data-stu-id="ca7a8-239">In hello dialog box **Select hello database that contains hello data you want**, select hello **ElasticDBQuery** database.</span></span>
6. <span data-ttu-id="ca7a8-240">Selecione Olá **clientes** tabela na exibição de lista hello e clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="ca7a8-240">Select hello **Customers** table in hello list view and click **Next**.</span></span> <span data-ttu-id="ca7a8-241">Em seguida, clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="ca7a8-241">Then click **Finish**.</span></span>
7. <span data-ttu-id="ca7a8-242">Em Olá **importar dados** formulário, em **selecione como deseja tooview esses dados na pasta de trabalho**, selecione **tabela** e clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="ca7a8-242">In hello **Import Data** form, under **Select how you want tooview this data in your workbook**, select **Table** and click **OK**.</span></span>

<span data-ttu-id="ca7a8-243">Todos os Olá linhas de **clientes** tabela, armazenada em fragmentos diferentes preencher a planilha do Excel hello.</span><span class="sxs-lookup"><span data-stu-id="ca7a8-243">All hello rows from **Customers** table, stored in different shards populate hello Excel sheet.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ca7a8-244">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ca7a8-244">Next steps</span></span>
<span data-ttu-id="ca7a8-245">Agora você pode usar funções de dados do Excel.</span><span class="sxs-lookup"><span data-stu-id="ca7a8-245">You can now use Excel’s data functions.</span></span> <span data-ttu-id="ca7a8-246">Use a cadeia de caracteres de conexão de saudação com seu nome de servidor, nome do banco de dados e credenciais tooconnect seu dados e BI integração ferramentas toohello Elástico consultar banco de dados.</span><span class="sxs-lookup"><span data-stu-id="ca7a8-246">Use hello connection string with your server name, database name and credentials tooconnect your BI and data integration tools toohello elastic query database.</span></span> <span data-ttu-id="ca7a8-247">Certifique-se de que o SQL Server tem suporte como uma fonte de dados para a ferramenta.</span><span class="sxs-lookup"><span data-stu-id="ca7a8-247">Make sure that SQL Server is supported as a data source for your tool.</span></span> <span data-ttu-id="ca7a8-248">Consulte o banco de dados de consulta Elástico toohello e tabelas externas, assim como qualquer outro banco de dados do SQL Server e tabelas do SQL Server que você se conectaria toowith sua ferramenta.</span><span class="sxs-lookup"><span data-stu-id="ca7a8-248">Refer toohello elastic query database and external tables just like any other SQL Server database and SQL Server tables that you would connect toowith your tool.</span></span>

### <a name="cost"></a><span data-ttu-id="ca7a8-249">Custo</span><span class="sxs-lookup"><span data-stu-id="ca7a8-249">Cost</span></span>
<span data-ttu-id="ca7a8-250">Não há nenhum custo adicional para usar o recurso de consulta de banco de dados Elástico Olá.</span><span class="sxs-lookup"><span data-stu-id="ca7a8-250">There is no additional charge for using hello Elastic Database query feature.</span></span> <span data-ttu-id="ca7a8-251">No entanto, neste momento esse recurso está disponível apenas em bancos de dados premium como um ponto de extremidade, mas fragmentos Olá podem ser de qualquer camada de serviço.</span><span class="sxs-lookup"><span data-stu-id="ca7a8-251">However, at this time this feature is available only on premium databases as an end point, but hello shards can be of any service tier.</span></span>

<span data-ttu-id="ca7a8-252">Para obter informações sobre os preços, consulte [Detalhes de preços do Banco de Dados SQL](https://azure.microsoft.com/pricing/details/sql-database/).</span><span class="sxs-lookup"><span data-stu-id="ca7a8-252">For pricing information see [SQL Database Pricing Details](https://azure.microsoft.com/pricing/details/sql-database/).</span></span>

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-query-getting-started/cmd-prompt.png
[2]: ./media/sql-database-elastic-query-getting-started/portal.png
[3]: ./media/sql-database-elastic-query-getting-started/tiers.png
[4]: ./media/sql-database-elastic-query-getting-started/details.png
[5]: ./media/sql-database-elastic-query-getting-started/exel-sources.png
<!--anchors-->
