---
title: "aaaCreate e gerenciar trabalhos Elásticos usando o PowerShell | Microsoft Docs"
description: PowerShell usado toomanage pools de banco de dados SQL
services: sql-database
documentationcenter: 
manager: jhubbard
author: ddove
ms.assetid: 737d8d13-5632-4e18-9cb0-4d3b8a19e495
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: f6c18aecfa7e8c0b102a3b7cd2f266f5542ae400
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-sql-database-elastic-jobs-using-powershell-preview"></a>Criar e gerenciar trabalhos elástico do Banco de Dados SQL usando o PowerShell (visualização)

Olá APIs do PowerShell para **trabalhos do banco de dados Elástico** (na visualização), permitem que você defina um grupo de bancos de dados no qual os scripts serão executados. Este artigo mostra como toocreate e gerenciar **trabalhos do banco de dados Elástico** usando cmdlets do PowerShell. Consulte [Visão geral dos trabalhos elásticos](sql-database-elastic-jobs-overview.md). 

## <a name="prerequisites"></a>Pré-requisitos
* Uma assinatura do Azure. Para obter uma avaliação gratuita, confira [Um mês de avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/).
* Um conjunto de bancos de dados criados com as ferramentas de banco de dados Elástico hello. Consulte [Introdução às ferramentas do Banco de Dados Elástico](sql-database-elastic-scale-get-started.md).
* PowerShell do Azure. Para obter informações detalhadas, consulte [como tooinstall e configurar o Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).
* **trabalhos de Banco de Dados Elástico** : consulte [Installing trabalhos de Banco de Dados Elástico](sql-database-elastic-jobs-service-installation.md)

### <a name="select-your-azure-subscription"></a>Selecionar sua assinatura do Azure
assinatura de saudação tooselect necessário a Id da assinatura (**- SubscriptionId**) ou o nome da assinatura (**- SubscriptionName**). Se você tiver várias assinaturas, você pode executar Olá **AzureRmSubscription Get** Olá cmdlet e cópia desejado informações de assinatura do conjunto de resultados de saudação. Uma vez que as informações de assinatura, executar Olá commandlet tooset a seguir esta assinatura como padrão hello, Olá como destino para criar e gerenciar trabalhos:

    Select-AzureRmSubscription -SubscriptionId {SubscriptionID}

Olá [PowerShell ISE](https://technet.microsoft.com/library/dd315244.aspx) é recomendado para uso toodevelop e executar scripts do PowerShell em relação aos trabalhos do banco de dados Elástico hello.

## <a name="elastic-database-jobs-objects"></a>Objetos de trabalhos de Banco de Dados Elástico
Olá a seguinte tabela lista todos os tipos de objeto de saudação do **trabalhos do banco de dados Elástico** junto com sua descrição e relevantes APIs do PowerShell.

<table style="width:100%">
  <tr>
    <th>Tipo de objeto</th>
    <th>Descrição</th>
    <th>APIs do PowerShell relacionadas</th>
  </tr>
  <tr>
    <td>Credencial</td>
    <td>Nome de usuário e senha toouse ao conectar-se toodatabases para execução de scripts ou aplicativos de DACPACs. <p>Olá senha é criptografada antes de enviar tooand armazenar no banco de dados de trabalhos do banco de dados Elástico hello.  senha de saudação é descriptografada pelo Olá serviço trabalhos Elástico de banco de dados por meio da credencial de saudação criado e carregado a partir de script de instalação de saudação.</td>
    <td><p>Get-AzureSqlJobCredential</p>
    <p>New-AzureSqlJobCredential</p><p>Set-AzureSqlJobCredential</p></td></td>
  </tr>

  <tr>
    <td>Script</td>
    <td>Toobe de script do Transact-SQL usado para execução em bancos de dados.  script Hello deve ser idempotente toobe criados desde que o serviço Olá tentará novamente a execução do script hello após falhas.
    </td>
    <td>
    <p>Get-AzureSqlJobContent</p>
    <p>Get-AzureSqlJobContentDefinition</p>
    <p>New-AzureSqlJobContent</p>
    <p>Set-AzureSqlJobContentDefinition</p>
    </td>
  </tr>

  <tr>
    <td>DACPAC</td>
    <td><a href="https://msdn.microsoft.com/library/ee210546.aspx">Aplicativo da camada de dados </a> toobe aplicado em bancos de dados do pacote.

    </td>
    <td>
    <p>Get-AzureSqlJobContent</p>
    <p>New-AzureSqlJobContent</p>
    <p>Set-AzureSqlJobContentDefinition</p>
    </td>
  </tr>
  <tr>
    <td>Destino do Banco de Dados</td>
    <td>Banco de dados e servidor de nome apontando tooan banco de dados do SQL Azure.

    </td>
    <td>
    <p>Get-AzureSqlJobTarget</p>
    <p>New-AzureSqlJobTarget</p>
    </td>
  </tr>
  <tr>
    <td>Destino do mapa de fragmentos</td>
    <td>Combinação de um destino de banco de dados e toobe uma credencial usada toodetermine informações armazenadas em um mapa de fragmento de banco de dados Elástico.
    </td>
    <td>
    <p>Get-AzureSqlJobTarget</p>
    <p>New-AzureSqlJobTarget</p>
    <p>Set-AzureSqlJobTarget</p>
    </td>
  </tr>
<tr>
    <td>Destino de coleção personalizada</td>
    <td>Usar o grupo definido de toocollectively de bancos de dados para execução.</td>
    <td>
    <p>Get-AzureSqlJobTarget</p>
    <p>New-AzureSqlJobTarget</p>
    </td>
  </tr>
<tr>
    <td>Destino filho de coleção personalizada</td>
    <td>Destino do banco de dados que é referenciado em uma coleção personalizada.</td>
    <td>
    <p>Add-AzureSqlJobChildTarget</p>
    <p>Remove-AzureSqlJobChildTarget</p>
    </td>
  </tr>

<tr>
    <td>Trabalho</td>
    <td>
    <p>Definição de parâmetros para um trabalho que pode ser usado tootrigger execução ou toofulfill uma agenda.</p>
    </td>
    <td>
    <p>Get-AzureSqlJob</p>
    <p>New-AzureSqlJob</p>
    <p>Set-AzureSqlJob</p>
    </td>
  </tr>

<tr>
    <td>Execução do Trabalho</td>
    <td>
    <p>Contêiner de toofulfill necessário de tarefas seja executar um script ou aplicando um destino de tooa DACPAC usando as credenciais para conexões de banco de dados com falhas tratadas na política de execução de tooan de acordo.</p>
    </td>
    <td>
    <p>Get-AzureSqlJobExecution</p>
    <p>Start-AzureSqlJobExecution</p>
    <p>Stop-AzureSqlJobExecution</p>
    <p>Wait-AzureSqlJobExecution</p>
  </tr>

<tr>
    <td>Execução de tarefa de trabalho</td>
    <td>
    <p>Uma unidade de trabalho toofulfill um trabalho.</p>
    <p>Se uma tarefa de trabalho não é capaz de toosuccessfully executar, mensagem de exceção Olá resultante será registrada e uma nova tarefa de trabalho correspondente será criada e executada no acordo toohello especificado política de execução.</p></p>
    </td>
    <td>
    <p>Get-AzureSqlJobExecution</p>
    <p>Start-AzureSqlJobExecution</p>
    <p>Stop-AzureSqlJobExecution</p>
    <p>Wait-AzureSqlJobExecution</p>
  </tr>

<tr>
    <td>Política de execução de trabalho</td>
    <td>
    <p>Controla os tempos limite de execução do trabalho, os limites de repetição e os intervalos entre as tentativas.</p>
    <p>O recurso trabalhos de banco de dados elástico inclui uma política de execução de trabalho padrão que gera, essencialmente, infinitas repetições de tarefas de trabalho com falha, com retirada exponencial de intervalos entre cada repetição.</p>
    </td>
    <td>
    <p>Get-AzureSqlJobExecutionPolicy</p>
    <p>New-AzureSqlJobExecutionPolicy</p>
    <p>Set-AzureSqlJobExecutionPolicy</p>
    </td>
  </tr>

<tr>
    <td>Agenda</td>
    <td>
    <p>Especificação de execução tootake local em um intervalo recorrente ou de uma vez com base no tempo.</p>
    </td>
    <td>
    <p>Get-AzureSqlJobSchedule</p>
    <p>New-AzureSqlJobSchedule</p>
    <p>Set-AzureSqlJobSchedule</p>
    </td>
  </tr>

<tr>
    <td>Gatilhos de trabalho</td>
    <td>
    <p>Um mapeamento entre um trabalho e a execução do trabalho tootrigger uma agenda de acordo com o agendamento de toohello.</p>
    </td>
    <td>
    <p>New-AzureSqlJobTrigger</p>
    <p>Remove-AzureSqlJobTrigger</p>
    </td>
  </tr>
</table>

## <a name="supported-elastic-database-jobs-group-types"></a>Tipos de grupo de trabalhos de Banco de Dados Elástico com suporte
trabalho Olá executa scripts Transact-SQL (T-SQL) ou o aplicativo de DACPACs por meio de um grupo de bancos de dados. Quando um trabalho é enviado toobe executado em um grupo de bancos de dados, trabalho hello "expande" hello em trabalhos filhos onde cada executa Olá solicitou a execução em um único banco de dados no grupo de saudação. 

Há dois tipos de grupos que você pode criar: 

* [Mapa do fragmento](sql-database-elastic-scale-shard-map-management.md) grupo: quando um trabalho é enviado tootarget um mapa do fragmento, trabalho Olá consultas toodetermine de mapa do fragmento Olá seu conjunto atual de fragmentos e cria filho trabalhos para cada fragmento no mapa do fragmento hello.
* Grupo Coleção Personalizada: um conjunto personalizado definido de bancos de dados. Quando um trabalho tem como alvo uma coleção personalizada, ele cria filho trabalhos para cada banco de dados atualmente na coleção de saudação personalizada.

## <a name="tooset-hello-elastic-database-jobs-connection"></a>Olá tooset conexão de trabalhos do banco de dados Elástico
Precisa de uma conexão toobe conjunto toohello trabalhos *banco de dados de controle* Olá toousing anteriores trabalhos APIs. Executar este cmdlet dispara um toopop da janela de credencial backup solicitando nome de saudação do usuário e senha criados durante a instalação de trabalhos do banco de dados Elástico. Todos os exemplos fornecidos neste tópico pressupõem que a primeira etapa já foi executada.

Abra um trabalhos de banco de dados Elástico toohello conexão:

    Use-AzureSqlJobConnection -CurrentAzureSubscription 

## <a name="encrypted-credentials-within-hello-elastic-database-jobs"></a>Credenciais criptografadas em trabalhos do banco de dados Elástico Olá
Credenciais de banco de dados podem ser inseridas em trabalhos Olá *banco de dados de controle* com a senha criptografada. É necessário toostore credenciais tooenable trabalhos toobe executado em um momento posterior, (usando agendas de trabalho).

Criptografia funciona por meio de um certificado criado como parte do script de instalação de saudação. cria o script de instalação Hello e carregamentos certificado Olá Olá serviço de nuvem do Azure para a descriptografia da saudação armazenado senhas criptografadas. Olá posteriormente no serviço de nuvem do Azure armazena a chave pública Olá em trabalhos Olá *banco de dados de controle* que permite Olá API PowerShell ou o Portal clássico do Azure interface tooencrypt uma senha fornecida sem a necessidade de certificado Olá toobe instalado localmente.

senhas de credencial de saudação são criptografados e protegidos contra usuários com objetos de trabalhos de banco de dados de tooElastic acesso somente leitura. Mas é possível que um usuário mal-intencionado com acesso de leitura-gravação tooElastic trabalhos do banco de dados objetos tooextract uma senha. As credenciais são projetada toobe reutilizado em execuções de trabalho. As credenciais são passadas tootarget bancos de dados durante o estabelecimento de conexões. Atualmente, não existem restrições em bancos de dados de destino Olá usados para cada credencial, o usuário mal-intencionado pode adicionar um destino de banco de dados para um banco de dados sob controle do usuário mal-intencionado hello. usuário Olá subsequentemente foi possível iniciar um trabalho de direcionamento a senha da credencial esse banco de dados toogain hello.

As práticas recomendadas de segurança para o recurso trabalhos de Banco de Dados Elástico incluem:

* Limitar o uso de outras pessoas tootrusted APIs de saudação.
* As credenciais devem ter Olá menos privilégios tooperform necessário Olá tarefas.  Mais informações podem ser vistas dentro desse artigo [Autorização e Permissões](https://msdn.microsoft.com/library/bb669084.aspx) do MSDN do SQL Server.

### <a name="toocreate-an-encrypted-credential-for-job-execution-across-databases"></a>toocreate uma credencial criptografada para a execução de trabalhos em bancos de dados
toocreate criptografada de uma nova credencial, hello [ **cmdlet Get-Credential** ](https://technet.microsoft.com/library/hh849815.aspx) solicitará um nome de usuário e senha que pode ser passada toohello [ **AzureSqlJobCredential novo cmdlet**](/powershell/module/elasticdatabasejobs/new-azuresqljobcredential).

    $credentialName = "{Credential Name}"
    $databaseCredential = Get-Credential
    $credential = New-AzureSqlJobCredential -Credential $databaseCredential -CredentialName $credentialName
    Write-Output $credential

### <a name="tooupdate-credentials"></a>credenciais tooupdate
Ao alterar as senhas, use Olá [ **cmdlet Set-AzureSqlJobCredential** ](/powershell/module/elasticdatabasejobs/set-azuresqljobcredential) e conjunto hello **CredentialName** parâmetro.

    $credentialName = "{Credential Name}"
    Set-AzureSqlJobCredential -CredentialName $credentialName -Credential $credential 

## <a name="toodefine-an-elastic-database-shard-map-target"></a>toodefine um destino de mapa de fragmento de banco de dados Elástico
tooexecute um trabalho em todos os bancos de dados em um conjunto de fragmentos (criada usando [biblioteca de cliente do banco de dados Elástico](sql-database-elastic-database-client-library.md)), use um mapa do fragmento como destino de banco de dados de saudação. Este exemplo exige um aplicativo de fragmentados criado usando a biblioteca de cliente do banco de dados Elástico hello. Consulte [Introdução ao exemplo de ferramentas de Banco de Dados Elástico](sql-database-elastic-scale-get-started.md).

o banco de dados do Hello fragmento mapa manager deve ser definido como um destino de banco de dados e, em seguida, o mapa de fragmentos específicos Olá deve ser especificado como um destino.

    $shardMapCredentialName = "{Credential Name}"
    $shardMapDatabaseName = "{ShardMapDatabaseName}" #example: ElasticScaleStarterKit_ShardMapManagerDb
    $shardMapDatabaseServerName = "{ShardMapServerName}"
    $shardMapName = "{MyShardMap}" #example: CustomerIDShardMap
    $shardMapDatabaseTarget = New-AzureSqlJobTarget -DatabaseName $shardMapDatabaseName -ServerName $shardMapDatabaseServerName
    $shardMapTarget = New-AzureSqlJobTarget -ShardMapManagerCredentialName $shardMapCredentialName -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapDatabaseServerName -ShardMapName $shardMapName
    Write-Output $shardMapTarget

## <a name="create-a-t-sql-script-for-execution-across-databases"></a>Criar um script T-SQL para execução em bancos de dados
Ao criar scripts T-SQL para execução, é altamente recomendável toobuild-los toobe [idempotente](https://en.wikipedia.org/wiki/Idempotence) e resilientes a falhas. Trabalhos do banco de dados Elásticos tentará novamente a execução de um script sempre que a execução encontrar uma falha, independentemente de classificação de saudação de falha de saudação.

Saudação de uso [ **cmdlet New-AzureSqlJobContent** ](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent) toocreate e salvar um script para execução e definir Olá **- ContentName** e **- CommandText**parâmetros.

    $scriptName = "Create a TestTable"

    $scriptCommandText = "
    IF NOT EXISTS (SELECT name FROM sys.tables WHERE name = 'TestTable')
    BEGIN
        CREATE TABLE TestTable(
            TestTableId INT PRIMARY KEY IDENTITY,
            InsertionTime DATETIME2
        );
    END
    GO
    INSERT INTO TestTable(InsertionTime) VALUES (sysutcdatetime());
    GO"

    $script = New-AzureSqlJobContent -ContentName $scriptName -CommandText $scriptCommandText
    Write-Output $script

### <a name="create-a-new-script-from-a-file"></a>Criar um novo script com base em um arquivo
Se Olá script T-SQL é definido dentro de um arquivo, use esse script de saudação tooimport:

    $scriptName = "My Script Imported from a File"
    $scriptPath = "{Path tooSQL File}"
    $scriptCommandText = Get-Content -Path $scriptPath
    $script = New-AzureSqlJobContent -ContentName $scriptName -CommandText $scriptCommandText
    Write-Output $script

### <a name="tooupdate-a-t-sql-script-for-execution-across-databases"></a>script de tooupdate um T-SQL para execução em bancos de dados
Essas atualizações de script do PowerShell Olá texto do comando T-SQL para um script existente.

Saudação de conjunto de variáveis tooreflect Olá desejado script definição toobe conjunto a seguir:

    $scriptName = "Create a TestTable"
    $scriptUpdateComment = "Adding AdditionalInformation column tooTestTable"
    $scriptCommandText = "
    IF NOT EXISTS (SELECT name FROM sys.tables WHERE name = 'TestTable')
    BEGIN
    CREATE TABLE TestTable(
        TestTableId INT PRIMARY KEY IDENTITY,
        InsertionTime DATETIME2
    );
    END
    GO

    IF NOT EXISTS (SELECT columns.name FROM sys.columns INNER JOIN sys.tables on columns.object_id = tables.object_id WHERE tables.name = 'TestTable' AND columns.name = 'AdditionalInformation')
    BEGIN
    ALTER TABLE TestTable
    ADD AdditionalInformation NVARCHAR(400);
    END
    GO

    INSERT INTO TestTable(InsertionTime, AdditionalInformation) VALUES (sysutcdatetime(), 'test');
    GO"

### <a name="tooupdate-hello-definition-tooan-existing-script"></a>script existente de tooan tooupdate Olá definição
    Set-AzureSqlJobContentDefinition -ContentName $scriptName -CommandText $scriptCommandText -Comment $scriptUpdateComment 

## <a name="toocreate-a-job-tooexecute-a-script-across-a-shard-map"></a>toocreate tooexecute um trabalho um script em um mapa do fragmento
Esse script de PowerShell inicia um trabalho para execução de um script em cada fragmento de um mapa de fragmentos de Escala Elástica.

Conjunto Olá Olá de tooreflect variáveis a seguir desejado script e destino:

    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $shardMapServerName = "{Shard Map Server Name}"
    $shardMapDatabaseName = "{Shard Map Database Name}"
    $shardMapName = "{Shard Map Name}"
    $credentialName = "{Credential Name}"
    $shardMapTarget = Get-AzureSqlJobTarget -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapServerName -ShardMapName $shardMapName 
    $job = New-AzureSqlJob -ContentName $scriptName -CredentialName $credentialName -JobName $jobName -TargetId $shardMapTarget.TargetId
    Write-Output $job

## <a name="tooexecute-a-job"></a>tooexecute um trabalho
Esse script de PowerShell executa um trabalho existente:

Atualize Olá tooreflect variável Olá desejado trabalho nome toohave executada a seguir:

    $jobName = "{Job Name}"
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName 
    Write-Output $jobExecution

## <a name="tooretrieve-hello-state-of-a-single-job-execution"></a>estado de saudação tooretrieve uma única de execução do trabalho
Saudação de uso [ **cmdlet Get-AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/get-azuresqljobexecution) e conjunto hello **JobExecutionId** estado de saudação do parâmetro tooview de execução do trabalho.

    $jobExecutionId = "{Job Execution Id}"
    $jobExecution = Get-AzureSqlJobExecution -JobExecutionId $jobExecutionId
    Write-Output $jobExecution

Use Olá mesmo **Get-AzureSqlJobExecution** cmdlet com hello **IncludeChildren** estado de saudação do parâmetro tooview de execuções do trabalho filho, ou seja, Olá estado específico para cada execução do trabalho em relação a cada banco de dados de destino pelo trabalho de saudação.

    $jobExecutionId = "{Job Execution Id}"
    $jobExecutions = Get-AzureSqlJobExecution -JobExecutionId $jobExecutionId -IncludeChildren
    Write-Output $jobExecutions 

## <a name="tooview-hello-state-across-multiple-job-executions"></a>estado de saudação tooview entre várias execuções de trabalho
Olá [ **cmdlet Get-AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/new-azuresqljob) tem vários parâmetros opcionais que podem ser usado toodisplay várias execuções de trabalho, filtradas por meio de parâmetros de saudação fornecido. Olá segue uma demonstração de algumas das maneiras possíveis de saudação toouse AzureSqlJobExecution Get:

Recupere todas as execuções de trabalhos ativos de nível superior:

    Get-AzureSqlJobExecution

Recupere todas as execuções do trabalho de nível superior, incluindo execuções de trabalhos inativos:

    Get-AzureSqlJobExecution -IncludeInactive

Recupere todas as execuções de trabalhos filho de uma ID de execução de trabalho fornecida, incluindo execuções de trabalhos inativos:

    $parentJobExecutionId = "{Job Execution Id}"
    Get-AzureSqlJobExecution -AzureSqlJobExecution -JobExecutionId $parentJobExecutionId -IncludeInactive -IncludeChildren

Recupere todas as execuções de trabalho criadas usando uma combinação de agenda/trabalho, incluindo trabalhos inativos:

    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Get-AzureSqlJobExecution -JobName $jobName -ScheduleName $scheduleName -IncludeInactive

Recupere todos os trabalhos direcionados a um mapa de fragmentos especificado, incluindo trabalhos inativos:

    $shardMapServerName = "{Shard Map Server Name}"
    $shardMapDatabaseName = "{Shard Map Database Name}"
    $shardMapName = "{Shard Map Name}"
    $target = Get-AzureSqlJobTarget -ShardMapManagerDatabaseName $shardMapDatabaseName -ShardMapManagerServerName $shardMapServerName -ShardMapName $shardMapName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive

Recupere todos os trabalhos direcionados a uma coleção personalizada especificada, incluindo trabalhos inativos:

    $customCollectionName = "{Custom Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    Get-AzureSqlJobExecution -TargetId $target.TargetId -IncludeInactive

Recupere a lista de saudação de execuções de tarefa de trabalho em uma execução de trabalho específico:

    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Write-Output $jobTaskExecutions 

Recupere detalhes de execução de tarefa de trabalho:

saudação de script do PowerShell a seguir pode ser usado tooview Olá detalhes de uma execução de tarefa do trabalho, é particularmente útil ao depurar falhas de execução.

    $jobTaskExecutionId = "{Job Task Execution Id}"
    $jobTaskExecution = Get-AzureSqlJobTaskExecution -JobTaskExecutionId $jobTaskExecutionId
    Write-Output $jobTaskExecution

## <a name="tooretrieve-failures-within-job-task-executions"></a>execuções de tooretrieve falhas no trabalho de tarefas
Olá **JobTaskExecution objeto** inclui uma propriedade para o ciclo de vida de saudação de tarefa Olá junto com uma propriedade de mensagem. Se uma execução de tarefa de trabalho falhou, propriedade de ciclo de vida de saudação será definida muito*falha* e propriedade de mensagem de saudação definirá toohello mensagem de exceção resultante e sua pilha. Se um trabalho não foi bem-sucedida, é importante tooview detalhes de Olá das tarefas de trabalho que não teve êxito para um determinado trabalho.

    $jobExecutionId = "{Job Execution Id}"
    $jobTaskExecutions = Get-AzureSqlJobTaskExecution -JobExecutionId $jobExecutionId
    Foreach($jobTaskExecution in $jobTaskExecutions) 
        {
        if($jobTaskExecution.Lifecycle -ne 'Succeeded')
            {
            Write-Output $jobTaskExecution
            }
        }

## <a name="toowait-for-a-job-execution-toocomplete"></a>toowait para um toocomplete de execução do trabalho
Olá script do PowerShell a seguir pode ser usado toowait para um toocomplete de tarefa do trabalho:

    $jobExecutionId = "{Job Execution Id}"
    Wait-AzureSqlJobExecution -JobExecutionId $jobExecutionId 

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

    $executionPolicyName = "{Execution Policy Name}"
    $initialRetryInterval = New-TimeSpan -Seconds 10
    $jobTimeout = New-TimeSpan -Minutes 30
    $maximumAttempts = 999999
    $maximumRetryInterval = New-TimeSpan -Minutes 1
    $retryIntervalBackoffCoefficient = 1.5
    $executionPolicy = New-AzureSqlJobExecutionPolicy -ExecutionPolicyName $executionPolicyName -InitialRetryInterval $initialRetryInterval -JobTimeout $jobTimeout -MaximumAttempts $maximumAttempts -MaximumRetryInterval $maximumRetryInterval 
    -RetryIntervalBackoffCoefficient $retryIntervalBackoffCoefficient
    Write-Output $executionPolicy

### <a name="update-a-custom-execution-policy"></a>Atualizar uma política de execução personalizada
Atualize tooupdate de política de execução de saudação desejada:

    $executionPolicyName = "{Execution Policy Name}"
    $initialRetryInterval = New-TimeSpan -Seconds 15
    $jobTimeout = New-TimeSpan -Minutes 30
    $maximumAttempts = 999999
    $maximumRetryInterval = New-TimeSpan -Minutes 1
    $retryIntervalBackoffCoefficient = 1.5
    $updatedExecutionPolicy = Set-AzureSqlJobExecutionPolicy -ExecutionPolicyName $executionPolicyName -InitialRetryInterval $initialRetryInterval -JobTimeout $jobTimeout -MaximumAttempts $maximumAttempts -MaximumRetryInterval $maximumRetryInterval -RetryIntervalBackoffCoefficient $retryIntervalBackoffCoefficient
    Write-Output $updatedExecutionPolicy

## <a name="cancel-a-job"></a>Cancelar um trabalho
O recurso trabalhos de Banco de Dados Elástico dá suporte a solicitações de cancelamento de trabalhos.  Se trabalhos de banco de dados Elástico detectar uma solicitação de cancelamento para um trabalho que está sendo executada no momento, ele tentará toostop trabalho de saudação.

Há duas maneiras diferentes pelas quais o recurso Trabalhos de Banco de Dados Elástico pode executar um cancelamento:

1. Cancelar tarefas em execução atualmente: se um cancelamento for detectado enquanto uma tarefa estiver em execução, um cancelamento será tentado no hello aspecto da tarefa de saudação em execução no momento.  Por exemplo: se houver atualmente sendo executada quando uma tentativa de um cancelamento de consultas de longa execução, haverá uma consulta de saudação toocancel tentativa.
2. Cancelando tentativas de tarefa: se um cancelamento for detectado pelo thread de controle de saudação antes de uma tarefa é iniciada para execução, a thread de controle de saudação evitar iniciar tarefa hello e declarar solicitação hello como cancelada.

Se for solicitado um cancelamento de trabalho para um trabalho pai, solicitação de cancelamento hello será respeitada para trabalho de pai hello e para todos os seus trabalhos filho.

toosubmit uma solicitação de cancelamento, use Olá [ **cmdlet Stop-AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution) e conjunto hello **JobExecutionId** parâmetro.

    $jobExecutionId = "{Job Execution Id}"
    Stop-AzureSqlJobExecution -JobExecutionId $jobExecutionId

## <a name="toodelete-a-job-and-job-history-asynchronously"></a>toodelete um trabalho e o histórico de trabalho assíncrona
O recurso trabalhos de Banco de Dados Elástico dá suporte à exclusão assíncrona de trabalhos. Um trabalho pode ser marcado para exclusão e sistema Olá excluirá trabalho hello e todo o seu histórico de trabalho depois de concluir todas as execuções de trabalho para o trabalho de saudação. sistema de saudação não cancelará automaticamente execuções de trabalho ativo.  

Invocar [ **Stop AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/stop-azuresqljobexecution) toocancel execuções de trabalho ativo.

exclusão de trabalho tootrigger, use Olá [ **cmdlet Remove-AzureSqlJob** ](/powershell/module/elasticdatabasejobs/remove-azuresqljob) e conjunto hello **JobName** parâmetro.

    $jobName = "{Job Name}"
    Remove-AzureSqlJob -JobName $jobName

## <a name="toocreate-a-custom-database-target"></a>toocreate um destino de banco de dados personalizado
Você pode definir os destinos de banco de dados personalizado para execução direta ou para inclusão em um grupo de bancos de dados personalizado. Por exemplo, porque **pools Elásticos** são ainda não suporte direto usando APIs do PowerShell, você pode criar um destino da coleção de banco de dados personalizado que abrange todos os bancos de dados de saudação no pool de saudação e um destino de banco de dados personalizado.

Saudação de conjunto de informações de banco de dados variáveis tooreflect Olá desejado a seguir:

    $databaseName = "{Database Name}"
    $databaseServerName = "{Server Name}"
    New-AzureSqlJobDatabaseTarget -DatabaseName $databaseName -ServerName $databaseServerName 

## <a name="toocreate-a-custom-database-collection-target"></a>toocreate um destino de coleção do banco de dados personalizado
Saudação de uso [ **New-AzureSqlJobTarget** ](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) toodefine cmdlet uma execução de tooenable do banco de dados personalizado coleção destino em vários destinos de banco de dados definido. Depois de criar um grupo de banco de dados, bancos de dados podem ser associados ao destino da coleção personalizada hello.

Definir Olá seguinte configuração de destino variáveis tooreflect Olá coleta personalizado desejado:

    $customCollectionName = "{Custom Database Collection Name}"
    New-AzureSqlJobTarget -CustomCollectionName $customCollectionName 

### <a name="tooadd-databases-tooa-custom-database-collection-target"></a>destino da coleção de banco de dados personalizado tooa tooadd bancos de dados
tooadd um banco de dados tooa específico de coleta personalizado use Olá [ **adicionar AzureSqlJobChildTarget** ](/powershell/module/elasticdatabasejobs/add-azuresqljobchildtarget) cmdlet.

    $databaseServerName = "{Database Server Name}"
    $databaseName = "{Database Name}"
    $customCollectionName = "{Custom Database Collection Name}"
    Add-AzureSqlJobChildTarget -CustomCollectionName $customCollectionName -DatabaseName $databaseName -ServerName $databaseServerName 

#### <a name="review-hello-databases-within-a-custom-database-collection-target"></a>Revisão Olá bancos de dados dentro de um destino de coleção do banco de dados personalizado
Saudação de uso [ **Get-AzureSqlJobTarget** ](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) bancos de dados do cmdlet tooretrieve Olá filho dentro de um destino de coleção do banco de dados personalizado. 

    $customCollectionName = "{Custom Database Collection Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $childTargets = Get-AzureSqlJobTarget -ParentTargetId $target.TargetId
    Write-Output $childTargets

### <a name="create-a-job-tooexecute-a-script-across-a-custom-database-collection-target"></a>Criar um script de um trabalho tooexecute em um destino de coleção do banco de dados personalizado
Saudação de uso [ **New-AzureSqlJob** ](/powershell/module/elasticdatabasejobs/new-azuresqljob) toocreate cmdlet um trabalho para um grupo de bancos de dados definidos por um destino de coleção do banco de dados personalizado. Trabalhos do banco de dados Elásticos expandirá trabalho Olá para vários trabalhos filho, cada banco de dados tooa correspondente associada ao destino de coleção de banco de dados personalizado hello e certifique-se de que o script hello é executada em cada banco de dados. Novamente, é importante que os scripts são idempotentes toobe resiliente tooretries.

    $jobName = "{Job Name}"
    $scriptName = "{Script Name}"
    $customCollectionName = "{Custom Collection Name}"
    $credentialName = "{Credential Name}"
    $target = Get-AzureSqlJobTarget -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob -JobName $jobName -CredentialName $credentialName -ContentName $scriptName -TargetId $target.TargetId
    Write-Output $job

## <a name="data-collection-across-databases"></a>Coleta de dados em bancos de dados
Você pode usar um trabalho tooexecute uma consulta em um grupo de bancos de dados e enviar Olá resultados tooa tabela. tabela Olá pode ser consultada depois dos resultados da consulta do hello fatos toosee Olá de cada banco de dados. Isso fornece um método assíncrono tooexecute uma consulta em muitos bancos de dados. Tentativas fracassadas são processadas automaticamente por meio de novas tentativas.

tabela de destino especificado Olá será criada automaticamente se ainda não existir. nova tabela de saudação coincide com o esquema de saudação do hello retornada um conjunto de resultados. Se um script retornar vários conjuntos de resultados, os trabalhos de banco de dados Elástico enviará apenas primeira tabela de destino toohello hello.

Olá seguinte script do PowerShell executa um script e coleta seus resultados em uma tabela especificada. Esse script presume que foi criado um script T-SQL, que produz um único conjunto de resultados, e que um destino de coleção de bancos de dados personalizada foi criado.

Esse script usa Olá [ **Get-AzureSqlJobTarget** ](/powershell/module/elasticdatabasejobs/new-azuresqljobtarget) cmdlet. Defina os parâmetros de saudação de script, credenciais e o destino de execução:

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

### <a name="toocreate-and-start-a-job-for-data-collection-scenarios"></a>toocreate e iniciar um trabalho para cenários de coleta de dados
Esse script usa Olá [ **início AzureSqlJobExecution** ](/powershell/module/elasticdatabasejobs/start-azuresqljobexecution) cmdlet.

    $job = New-AzureSqlJob -JobName $jobName 
    -CredentialName $executionCredentialName 
    -ContentName $scriptName 
    -ResultSetDestinationServerName $destinationServerName 
    -ResultSetDestinationDatabaseName $destinationDatabaseName 
    -ResultSetDestinationSchemaName $destinationSchemaName 
    -ResultSetDestinationTableName $destinationTableName 
    -ResultSetDestinationCredentialName $destinationCredentialName 
    -TargetId $target.TargetId
    Write-Output $job
    $jobExecution = Start-AzureSqlJobExecution -JobName $jobName
    Write-Output $jobExecution

## <a name="tooschedule-a-job-execution-trigger"></a>tooschedule um gatilho de execução do trabalho
saudação de script do PowerShell a seguir pode ser usado toocreate um agendamento recorrente. Esse script usa um intervalo de minutos, mas o [**New-AzureSqlJobSchedule**](/powershell/module/elasticdatabasejobs/new-azuresqljobschedule) também dá suporte aos parâmetros -DayInterval, -HourInterval, -MonthInterval e -WeekInterval. Agendas que são executadas apenas uma vez podem ser criadas pela passagem de -OneTime.

Crie uma nova agenda:

    $scheduleName = "Every one minute"
    $minuteInterval = 1
    $startTime = (Get-Date).ToUniversalTime()
    $schedule = New-AzureSqlJobSchedule 
    -MinuteInterval $minuteInterval 
    -ScheduleName $scheduleName 
    -StartTime $startTime 
    Write-Output $schedule

### <a name="tootrigger-a-job-executed-on-a-time-schedule"></a>tootrigger um trabalho executado em um agendamento de tempo
Um gatilho de trabalho pode ser definido toohave um agendamento de tempo de tooa acordo do trabalho executado. saudação de script do PowerShell a seguir pode ser usado toocreate um gatilho de trabalho.

Use [AzureSqlJobTrigger novo](/powershell/module/elasticdatabasejobs/new-azuresqljobtrigger) e saudação do conjunto de variáveis toocorrespond toohello desejado trabalho e uma agenda a seguir:

    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    $jobTrigger = New-AzureSqlJobTrigger
    -ScheduleName $scheduleName
    -JobName $jobName
    Write-Output $jobTrigger

### <a name="tooremove-a-scheduled-association-toostop-job-from-executing-on-schedule"></a>tooremove um trabalho de toostop associação agendados sejam executados na agenda
toodiscontinue ocorrer a execução de trabalho por meio de um gatilho de trabalho, o gatilho de trabalho Olá pode ser removido. Remover um gatilho de trabalho toostop um trabalho seja executado acordo agenda tooa usando Olá [ **cmdlet Remove-AzureSqlJobTrigger**](/powershell/module/elasticdatabasejobs/remove-azuresqljobtrigger).

    $jobName = "{Job Name}"
    $scheduleName = "{Schedule Name}"
    Remove-AzureSqlJobTrigger 
    -ScheduleName $scheduleName 
    -JobName $jobName

### <a name="retrieve-job-triggers-bound-tooa-time-schedule"></a>Recuperar o agendamento de tempo de tooa associada de gatilhos de trabalho
Olá script do PowerShell a seguir pode ser usado tooobtain e exibir agendamento de tempo específico Olá trabalho gatilhos tooa registrado.

    $scheduleName = "{Schedule Name}"
    $jobTriggers = Get-AzureSqlJobTrigger -ScheduleName $scheduleName
    Write-Output $jobTriggers

### <a name="tooretrieve-job-triggers-bound-tooa-job"></a>gatilhos de trabalho tooretrieve associado tooa trabalho
Use [Get-AzureSqlJobTrigger](/powershell/module/elasticdatabasejobs/get-azuresqljobtrigger) tooobtain e Exibir agendas que contém um trabalho registrado.

    $jobName = "{Job Name}"
    $jobTriggers = Get-AzureSqlJobTrigger -JobName $jobName
    Write-Output $jobTriggers

## <a name="toocreate-a-data-tier-application-dacpac-for-execution-across-databases"></a>toocreate um aplicativo da camada de dados (DACPAC) para execução em bancos de dados
toocreate um DACPAC, consulte [aplicativos da camada de dados](https://msdn.microsoft.com/library/ee210546.aspx). toodeploy um DACPAC, use Olá [cmdlet New-AzureSqlJobContent](/powershell/module/elasticdatabasejobs/new-azuresqljobcontent). Olá DACPAC deve ser acessível toohello serviço. É recomendável tooupload um tooAzure DACPAC criado armazenamento e criar um [assinatura de acesso compartilhado](../storage/common/storage-dotnet-shared-access-signature-part-1.md) para Olá DACPAC.

    $dacpacUri = "{Uri}"
    $dacpacName = "{Dacpac Name}"
    $dacpac = New-AzureSqlJobContent -DacpacUri $dacpacUri -ContentName $dacpacName 
    Write-Output $dacpac

### <a name="tooupdate-a-data-tier-application-dacpac-for-execution-across-databases"></a>tooupdate um aplicativo da camada de dados (DACPAC) para execução em bancos de dados
DACPACs existentes registrados em trabalhos Elástico de banco de dados podem ser atualizado toopoint toonew URIs. Saudação de uso [ **cmdlet Set-AzureSqlJobContentDefinition** ](/powershell/module/elasticdatabasejobs/set-azuresqljobcontentdefinition) tooupdate Olá URI DACPAC em um existente registrado DACPAC:

    $dacpacName = "{Dacpac Name}"
    $newDacpacUri = "{Uri}"
    $updatedDacpac = Set-AzureSqlJobDacpacDefinition -ContentName $dacpacName -DacpacUri $newDacpacUri
    Write-Output $updatedDacpac

## <a name="toocreate-a-job-tooapply-a-data-tier-application-dacpac-across-databases"></a>toocreate tooapply um trabalho um aplicativo da camada de dados (DACPAC) em bancos de dados
Depois de um DACPAC foi criado no trabalhos Elástico de banco de dados, um trabalho pode ser criado Olá tooapply DACPAC em um grupo de bancos de dados. saudação de script do PowerShell a seguir pode ser usado toocreate um trabalho DACPAC em um conjunto personalizado de bancos de dados:

    $jobName = "{Job Name}"
    $dacpacName = "{Dacpac Name}"
    $customCollectionName = "{Custom Collection Name}"
    $credentialName = "{Credential Name}"
    $target = Get-AzureSqlJobTarget 
    -CustomCollectionName $customCollectionName
    $job = New-AzureSqlJob 
    -JobName $jobName 
    -CredentialName $credentialName 
    -ContentName $dacpacName -TargetId $target.TargetId
    Write-Output $job 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-jobs-powershell/cmd-prompt.png
[2]: ./media/sql-database-elastic-jobs-powershell/portal.png
<!--anchors-->
