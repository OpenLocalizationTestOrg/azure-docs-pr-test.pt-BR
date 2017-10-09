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
# <a name="getting-started-with-elastic-database-jobs"></a>Introdução a trabalhos de Banco de Dados Elástico
Trabalhos do banco de dados Elásticos (visualização) para o banco de dados do Azure SQL permite que você tooreliability executar scripts do T-SQL que abrangem vários bancos de dados ao repetir automaticamente e fornecer eventual conclusão garantia. Para obter mais informações sobre o recurso de trabalho de banco de dados Elástico Olá, consulte Olá [página de visão geral do recurso](sql-database-elastic-jobs-overview.md).

Este tópico estende o exemplo hello encontrado no [Introdução às ferramentas de banco de dados Elástico](sql-database-elastic-scale-get-started.md). Quando concluído, você verá: Saiba como toocreate e gerenciar trabalhos que gerenciar um grupo de bancos de dados relacionados. Não é necessário toouse Olá escala elástica ferramentas em ordem tootake máximo Olá benefícios da Elásticos trabalhos.

## <a name="prerequisites"></a>Pré-requisitos
Baixe e execute Olá [guia de Introdução com amostra das ferramentas de banco de dados Elástico](sql-database-elastic-scale-get-started.md).

## <a name="create-a-shard-map-manager-using-hello-sample-app"></a>Criar um mapa do fragmento manager usando o aplicativo de exemplo hello
Aqui você criará um mapa do fragmento manager juntamente com vários fragmentos, seguido de inserção de dados em fragmentos hello. Se você já tiver configurado com dados fragmentados de fragmentos, você pode ignorar Olá etapas a seguir e mover toohello próxima seção.

1. Compilar e executar Olá **Introdução às ferramentas de banco de dados Elástico** aplicativo de exemplo. Execute as etapas de saudação até a etapa 7 na seção Olá [Baixe e execute o aplicativo de exemplo hello](sql-database-elastic-scale-get-started.md#download-and-run-the-sample-app). No final da saudação da etapa 7, você verá saudação de prompt de comando a seguir:

   ![prompt de comando](./media/sql-database-elastic-query-getting-started/cmd-prompt.png)

2. Na janela de comando hello, digite "1" e pressione **Enter**. Isso cria o Gerenciador do mapa de fragmentos Olá e adiciona dois servidores toohello de fragmentos. Em seguida, digite "3" e pressione **Enter**. Repita essa ação quatro vezes. Isso insere linhas de dados de exemplo no seus fragmentos.
3. Olá [Portal do Azure](https://portal.azure.com) devem mostrar três novos bancos de dados:

   ![Confirmação do Visual Studio](./media/sql-database-elastic-query-getting-started/portal.png)

   Neste ponto, vamos criar uma coleção de banco de dados personalizado que reflete todos os bancos de dados de Olá no mapa do fragmento hello. Isso nos permitirá toocreate e executar um trabalho que adiciona uma nova tabela em fragmentos.

Aqui nós geralmente criaria um destino de mapa do fragmento, usando Olá **AzureSqlJobTarget novo** cmdlet. o banco de dados do Hello fragmento mapa manager deve ser definido como um destino de banco de dados e, em seguida, o mapa de fragmentos específicos de saudação é especificado como um destino. Em vez disso, somos contínuo tooenumerate todos os bancos de dados de Olá no servidor de saudação e adicionar Olá bancos de dados toohello nova coleção personalizada com exceção de saudação do banco de dados mestre.

## <a name="creates-a-custom-collection-and-add-all-databases-in-hello-server-toohello-custom-collection-target-with-hello-exception-of-master"></a>Cria uma coleção personalizada e adicionar todos os bancos de dados de destino da coleção personalizada toohello Olá server com exceção de saudação do mestre.
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
## <a name="create-a-t-sql-script-for-execution-across-databases"></a>Criar um script T-SQL para execução em bancos de dados
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

## <a name="create-hello-job-tooexecute-a-script-across-hello-custom-group-of-databases"></a>Criar um script de saudação trabalho tooexecute em grupo personalizado de saudação de bancos de dados

   ```
    $jobName = "create on server dbs"
    $scriptName = "NewTable"
    $customCollectionName = "dbs_in_server"
    $credentialName = "ddove66"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $credentialName -ContentName $scriptName -TargetId $target.TargetId
    Write-Output $job
   ```

## <a name="execute-hello-job"></a>Executar trabalho Olá
saudação de script do PowerShell a seguir pode ser usado tooexecute um trabalho existente:

Atualize Olá tooreflect variável Olá desejado trabalho nome toohave executada a seguir:

   ```
    $jobName = "create on server dbs"
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName
    Write-Output $jobExecution
   ```

## <a name="retrieve-hello-state-of-a-single-job-execution"></a>Recuperar o estado de saudação de uma execução de trabalho
Use Olá mesmo **Get-AzureSqlJobExecution** cmdlet com hello **IncludeChildren** estado de saudação do parâmetro tooview de execuções do trabalho filho, ou seja, Olá estado específico para cada execução do trabalho em relação a cada banco de dados de destino pelo trabalho de saudação.

   ```
    $jobExecutionId = "{Job Execution Id}"
    $jobExecutions = Get-AzureSqlJobExecution -JobExecutionId $jobExecutionId -IncludeChildren
    Write-Output $jobExecutions
   ```

## <a name="view-hello-state-across-multiple-job-executions"></a>Estado de exibição Olá entre várias execuções de trabalho
Olá **AzureSqlJobExecution Get** cmdlet tem vários parâmetros opcionais que podem ser usado toodisplay várias execuções de trabalho, filtradas por meio de parâmetros de saudação fornecido. Olá segue uma demonstração de algumas das maneiras possíveis de saudação toouse AzureSqlJobExecution Get:

Recupere todas as execuções de trabalhos ativos de nível superior:

   ```
    Get-AzureSqlJobExecution
   ```

Recupere todas as execuções do trabalho de nível superior, incluindo execuções de trabalhos inativos:

   ```
    Get-AzureSqlJobExecution -IncludeInactive
   ```

Recupere todas as execuções de trabalhos filho de uma ID de execução de trabalho fornecida, incluindo execuções de trabalhos inativos:

   ```
    $parentJobExecutionId = "{Job Execution Id}"
    Get-AzureSqlJobExecution -AzureSqlJobExecution -JobExecutionId $parentJobExecutionId -IncludeInactive -IncludeChildren
   ```

Recupere todas as execuções de trabalho criadas usando uma combinação de agenda/trabalho, incluindo trabalhos inativos:

   ```
    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Get-AzureSqlJobExecution -JobName $jobName -ScheduleName $scheduleName -IncludeInactive
   ```

Recupere todos os trabalhos direcionados a um mapa de fragmentos especificado, incluindo trabalhos inativos:

   ```
    $shardMapServerName = "{Shard Map Server Name}"
    $shardMapDatabaseName = "{Shard Map Database Name}"
    $shardMapName = "{Shard Map Name}"
    $target = Get-AzureSqlJobTarget -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapServerName -ShardMapName $shardMapName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive
   ```

Recupere todos os trabalhos direcionados a uma coleção personalizada especificada, incluindo trabalhos inativos:

   ```
    $customCollectionName = "{Custom Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive
   ```

Recupere a lista de saudação de execuções de tarefa de trabalho em uma execução de trabalho específico:

   ```
    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Write-Output $jobTaskExecutions
   ```

Recupere detalhes de execução de tarefa de trabalho:

saudação de script do PowerShell a seguir pode ser usado tooview Olá detalhes de uma execução de tarefa do trabalho, é particularmente útil ao depurar falhas de execução.
   ```
    $jobTaskExecutionId = "{Job Task Execution Id}"
    $jobTaskExecution = Get-AzureSqlJobTaskExecution -JobTaskExecutionId $jobTaskExecutionId
    Write-Output $jobTaskExecution
   ```

## <a name="retrieve-failures-within-job-task-executions"></a>Recuperar falhas em execuções de tarefa de trabalho
objeto de JobTaskExecution Olá inclui uma propriedade para o ciclo de vida de tarefa Olá junto com uma propriedade de mensagem de saudação. Se uma execução de tarefa de trabalho falhou, Olá do ciclo de vida de propriedade será definido muito*falha* e propriedade de mensagem de saudação será definida toohello mensagem de exceção resultante e sua pilha. Se um trabalho não foi bem-sucedida, é importante tooview detalhes de Olá das tarefas de trabalho que não teve êxito para um determinado trabalho.

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

## <a name="waiting-for-a-job-execution-toocomplete"></a>Aguardando um toocomplete de execução do trabalho
Olá script do PowerShell a seguir pode ser usado toowait para um toocomplete de tarefa do trabalho:

   ```
    $jobExecutionId = "{Job Execution Id}"
    Wait-AzureSqlJobExecution -JobExecutionId $jobExecutionId
   ```

## <a name="create-a-custom-execution-policy"></a>Criar uma política de execução personalizada
O recurso trabalhos de Banco de Dados Elástico dá suporte à criação de políticas de execução personalizadas, que podem ser aplicadas ao iniciar trabalhos.

Atualmente, as políticas de execução permitem definir:

* Nome: O identificador de política de execução de saudação.
* Tempo Limite do Trabalho: tempo total antes que um trabalho seja cancelado pelo recurso Trabalhos de Banco de Dados Elástico.
* Intervalo de repetição inicial: Toowait de intervalo antes da primeira nova tentativa.
* Intervalo de repetição máximo: Limite de toouse de intervalos de repetição.
* Coeficiente de retirada de intervalo de repetição: Coeficiente usado toocalculate Olá próximo intervalo entre repetições.  Olá fórmula a seguir é usada: (intervalo de repetição iniciais) * Math.pow ((coeficiente de retirada de intervalo), (número de tentativas de) - 2).
* Máximo de tentativas: número máximo de saudação de tooperform de tentativas de repetição dentro de um trabalho.

política de execução padrão Olá usa Olá valores a seguir:

* Nome: política de execução padrão
* Tempo Limite do Trabalho: 1 semana
* Intervalo de Repetição Inicial: 100 milissegundos
* Intervalo Máximo de Repetição: 30 minutos
* Coeficiente de Intervalo de Repetição: 2
* Máximo de Tentativas: 2.147.483.647

Crie política de execução de saudação desejada:

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

### <a name="update-a-custom-execution-policy"></a>Atualizar uma política de execução personalizada
Atualize tooupdate de política de execução de saudação desejada:

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

## <a name="cancel-a-job"></a>Cancelar um trabalho
Os Trabalhos de Banco de Dados Elástico dão suporte a solicitações de cancelamento de trabalhos.  Se trabalhos de banco de dados Elástico detectar uma solicitação de cancelamento para um trabalho que está sendo executada no momento, ele tentará toostop trabalho de saudação.

Há duas maneiras diferentes pelas quais o recurso Trabalhos de Banco de Dados Elástico pode executar um cancelamento:

1. Cancelando executando tarefas: se um cancelamento for detectado enquanto uma tarefa estiver em execução, um cancelamento será tentado no hello aspecto da tarefa de saudação em execução no momento.  Por exemplo: se houver atualmente sendo executada quando uma tentativa de um cancelamento de consultas de longa execução, haverá uma consulta de saudação toocancel tentativa.
2. Cancelando tentativas de tarefa: Se um cancelamento for detectado pelo thread de controle de saudação antes de uma tarefa é iniciada para execução, thread de controle Olá evitar iniciar tarefa hello e as declarar solicitação hello como cancelada.

Se for solicitado um cancelamento de trabalho para um trabalho pai, solicitação de cancelamento hello será respeitada para trabalho de pai hello e para todos os seus trabalhos filho.

toosubmit uma solicitação de cancelamento, use Olá **Stop AzureSqlJobExecution** cmdlet e conjunto hello **JobExecutionId** parâmetro.

   ```
    $jobExecutionId = "{Job Execution Id}"
    Stop-AzureSqlJobExecution -JobExecutionId $jobExecutionId
   ```

## <a name="delete-a-job-by-name-and-hello-jobs-history"></a>Excluir um trabalho por nome e o histórico do trabalho Olá
O recurso trabalhos de Banco de Dados Elástico dá suporte à exclusão assíncrona de trabalhos. Um trabalho pode ser marcado para exclusão e sistema Olá excluirá trabalho hello e todo o seu histórico de trabalho depois de concluir todas as execuções de trabalho para o trabalho de saudação. sistema de saudação não cancelará automaticamente execuções de trabalho ativo.  

Em vez disso, Stop-AzureSqlJobExecution deve ser invocado toocancel execuções de trabalho ativo.

tootrigger exclusão de trabalho, use Olá **remover AzureSqlJob** cmdlet e conjunto hello **JobName** parâmetro.

   ```
    $jobName = "{Job Name}"
    Remove-AzureSqlJob -JobName $jobName
   ```

## <a name="create-a-custom-database-target"></a>Criar um destino de banco de dados personalizado
Destinos personalizados de banco de dados podem ser definidos no recurso trabalhos de Banco de Dados Elástico, que podem ser usados para execução direta ou para inclusão em um grupo personalizado de bancos de dados. Como **pools Elásticos** não ainda diretamente têm suporte por meio de APIs do PowerShell do hello, basta criar um destino da coleção de banco de dados personalizado que abrange todos os bancos de dados de saudação no pool de saudação e um destino de banco de dados personalizado.

Saudação de conjunto de informações de banco de dados variáveis tooreflect Olá desejado a seguir:

   ```
    $databaseName = "{Database Name}"
    $databaseServerName = "{Server Name}"
    New-AzureSqlJobDatabaseTarget -DatabaseName $databaseName -ServerName $databaseServerName
   ```

## <a name="create-a-custom-database-collection-target"></a>Criar um destino para a coleção de bancos de dados personalizada
Um destino de coleção do banco de dados personalizado pode ser definido tooenable execução por vários destinos de banco de dados definido. Após a criação de um grupo de banco de dados, bancos de dados podem ser destino de coleção personalizada toohello associado.

Definir Olá seguinte configuração de destino variáveis tooreflect Olá coleta personalizado desejado:

   ```
    $customCollectionName = "{Custom Database Collection Name}"
    New-AzureSqlJobTarget -CustomCollectionName $customCollectionName
   ```

### <a name="add-databases-tooa-custom-database-collection-target"></a>Adicionar o destino da coleção de bancos de dados tooa banco de dados personalizado
Destinos de banco de dados podem ser associados ao banco de dados personalizado coleção destinos toocreate um grupo de bancos de dados. Sempre que um trabalho é criado e vinculada a um destino de coleção do banco de dados personalizado, é grupo de toohello associado tootarget expandido Olá bancos de dados em tempo de execução de saudação.

Adicione a saudação desejada banco de dados tooa específico personalizado coleta:

   ```
    $serverName = "{Database Server Name}"
    $databaseName = "{Database Name}"
    $customCollectionName = "{Custom Database Collection Name}"
    Add-AzureSqlJobChildTarget -CustomCollectionName $customCollectionName -DatabaseName $databaseName -ServerName $databaseServerName
   ```

#### <a name="review-hello-databases-within-a-custom-database-collection-target"></a>Revisão Olá bancos de dados dentro de um destino de coleção do banco de dados personalizado
Saudação de uso **AzureSqlJobTarget Get** bancos de dados do cmdlet tooretrieve Olá filho dentro de um destino de coleção do banco de dados personalizado.

   ```
    $customCollectionName = "{Custom Database Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $childTargets = Get-AzureSqlJobTarget -ParentTargetId $target.TargetId
    Write-Output $childTargets
   ```

### <a name="create-a-job-tooexecute-a-script-across-a-custom-database-collection-target"></a>Criar um script de um trabalho tooexecute em um destino de coleção do banco de dados personalizado
Saudação de uso **AzureSqlJob novo** cmdlet toocreate um trabalho para um grupo de bancos de dados definidos por um destino de coleção do banco de dados personalizado. Trabalhos do banco de dados Elásticos expandirá trabalho Olá para vários trabalhos filho, cada banco de dados tooa correspondente associada ao destino de coleção de banco de dados personalizado hello e certifique-se de que o script hello é executada em cada banco de dados. Novamente, é importante que os scripts são idempotentes toobe resiliente tooretries.

   ```
    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $customCollectionName = "{Custom Collection Name}"
    $credentialName = "{Credential Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $credentialName -ContentName $scriptName -TargetId $target.TargetId
    Write-Output $job
   ```

## <a name="data-collection-across-databases"></a>Coleta de dados em bancos de dados
**Trabalhos do banco de dados Elásticos** suporta a execução de uma consulta em um grupo de bancos de dados e envia a tabela Olá resultados tooa especificado do banco de dados. tabela Olá pode ser consultada depois dos resultados da consulta do hello fatos toosee Olá de cada banco de dados. Isso fornece um mecanismo assíncrono tooexecute uma consulta em muitos bancos de dados. Casos de falha, como um dos bancos de dados de saudação está temporariamente indisponível são tratados automaticamente por meio de novas tentativas.

tabela de destino especificado Olá será criada automaticamente se ainda não existir, o esquema de saudação correspondente de saudação retornou um conjunto de resultados. Se uma execução de script retornar vários conjuntos de resultados, os trabalhos de banco de dados Elástico enviará apenas Olá primeiro tabela de destino de um toohello fornecido.

saudação de script do PowerShell a seguir pode ser usado tooexecute um script coletar seus resultados em uma tabela especificada. Este script presume que foi criado um script T-SQL, que produz um único conjunto de resultados; além disso, um destino de coleção de bancos de dados personalizada foi criado.

Definir Olá tooreflect script de saudação desejada, credenciais e o destino de execução a seguir:

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

### <a name="create-and-start-a-job-for-data-collection-scenarios"></a>Criar e iniciar um trabalho para cenários de coleta de dados
   ```
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $executionCredentialName -ContentName $scriptName -ResultSetDestinationServerName $destinationServerName -ResultSetDestinationDatabaseName $destinationDatabaseName -ResultSetDestinationSchemaName $destinationSchemaName -ResultSetDestinationTableName $destinationTableName -ResultSetDestinationCredentialName $destinationCredentialName -TargetId $target.TargetId
    Write-Output $job
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName
    Write-Output $jobExecution
   ```

## <a name="create-a-schedule-for-job-execution-using-a-job-trigger"></a>Criar um agendamento para execução de trabalho usando um gatilho de trabalho
saudação de script do PowerShell a seguir pode ser usado toocreate um agendamento recorrente. Esse script usa um intervalo de minutos, mas o New-AzureSqlJobSchedule também dá suporte aos parâmetros -DayInterval, -HourInterval, -MonthInterval e -WeekInterval. Agendas que são executadas apenas uma vez podem ser criadas pela passagem de -OneTime.

Crie uma nova agenda:
   ```
    $scheduleName = "Every one minute"
    $minuteInterval = 1
    $startTime = (Get-Date).ToUniversalTime()
    $schedule = New-AzureSqlJobSchedule -MinuteInterval $minuteInterval -ScheduleName $scheduleName -StartTime $startTime
    Write-Output $schedule
   ```

### <a name="create-a-job-trigger-toohave-a-job-executed-on-a-time-schedule"></a>Criar um trabalho executado em um agendamento de tempo de um toohave de gatilho de trabalho
Um gatilho de trabalho pode ser definido toohave um agendamento de tempo de tooa acordo do trabalho executado. saudação de script do PowerShell a seguir pode ser usado toocreate um gatilho de trabalho.

Saudação de conjunto de variáveis toocorrespond toohello a seguir desejado trabalho e agenda:

   ```
    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    $jobTrigger = New-AzureSqlJobTrigger -ScheduleName $scheduleName -JobName $jobName
    Write-Output $jobTrigger
   ```

### <a name="remove-a-scheduled-association-toostop-job-from-executing-on-schedule"></a>Remover um trabalho de toostop de associação agendados sejam executados na agenda
toodiscontinue ocorrer a execução de trabalho por meio de um gatilho de trabalho, o gatilho de trabalho Olá pode ser removido.
Remover um gatilho de trabalho toostop um trabalho seja executado acordo agenda tooa usando Olá **AzureSqlJobTrigger remover** cmdlet.

   ```
    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Remove-AzureSqlJobTrigger -ScheduleName $scheduleName -JobName $jobName
   ```

## <a name="import-elastic-database-query-results-tooexcel"></a>Importar tooExcel de resultados de consulta de banco de dados Elástico
 Você pode importar resultados de saudação de um consulta tooan do arquivo de Excel.

1. Inicie o Excel 2013.
2. Navegue toohello **dados** faixa de opções.
3. Clique em **De Outras Fontes** e em **Do SQL Server**.

   ![Importação de outras fontes para o Excel](./media/sql-database-elastic-query-getting-started/exel-sources.png)

4. Em Olá **Assistente de Conexão de dados** digite credenciais de nome e logon do servidor de saudação. Em seguida, clique em **Próximo**.
5. Na caixa de diálogo Olá **banco de dados Olá Select que contém dados Olá deseja**, selecione Olá **ElasticDBQuery** banco de dados.
6. Selecione Olá **clientes** tabela na exibição de lista hello e clique em **próximo**. Em seguida, clique em **Concluir**.
7. Em Olá **importar dados** formulário, em **selecione como deseja tooview esses dados na pasta de trabalho**, selecione **tabela** e clique em **Okey**.

Todos os Olá linhas de **clientes** tabela, armazenada em fragmentos diferentes preencher a planilha do Excel hello.

## <a name="next-steps"></a>Próximas etapas
Agora você pode usar funções de dados do Excel. Use a cadeia de caracteres de conexão de saudação com seu nome de servidor, nome do banco de dados e credenciais tooconnect seu dados e BI integração ferramentas toohello Elástico consultar banco de dados. Certifique-se de que o SQL Server tem suporte como uma fonte de dados para a ferramenta. Consulte o banco de dados de consulta Elástico toohello e tabelas externas, assim como qualquer outro banco de dados do SQL Server e tabelas do SQL Server que você se conectaria toowith sua ferramenta.

### <a name="cost"></a>Custo
Não há nenhum custo adicional para usar o recurso de consulta de banco de dados Elástico Olá. No entanto, neste momento esse recurso está disponível apenas em bancos de dados premium como um ponto de extremidade, mas fragmentos Olá podem ser de qualquer camada de serviço.

Para obter informações sobre os preços, consulte [Detalhes de preços do Banco de Dados SQL](https://azure.microsoft.com/pricing/details/sql-database/).

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-query-getting-started/cmd-prompt.png
[2]: ./media/sql-database-elastic-query-getting-started/portal.png
[3]: ./media/sql-database-elastic-query-getting-started/tiers.png
[4]: ./media/sql-database-elastic-query-getting-started/details.png
[5]: ./media/sql-database-elastic-query-getting-started/exel-sources.png
<!--anchors-->
