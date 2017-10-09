---
title: "PowerShell: Criar e gerenciar um pool elástico do SQL do Azure | Microsoft Docs"
description: "Saiba como toouse PowerShell toomanage um pool Elástico."
services: sql-database
documentationcenter: 
author: srinia
manager: jhubbard
editor: 
ms.assetid: 61289770-69b9-4ae3-9252-d0e94d709331
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: data-management
ms.date: 06/06/2017
ms.author: srinia
ms.openlocfilehash: 92de2a4b243dcc74502064e9d2c31682691753d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-an-elastic-pool-with-powershell"></a>Criar e gerenciar um pool elástico com o PowerShell
Este tópico mostra como toocreate e gerenciar escalonável [pools Elásticos](sql-database-elastic-pool.md) com o PowerShell.  Você também pode criar e gerenciar um pool Elástico do Azure usando Olá [portal do Azure](https://portal.azure.com/), API de REST, ou [c#](sql-database-elastic-pool-manage-csharp.md). Você também pode criar e mover bancos de dados de e para os pools elásticos usando [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).

[!INCLUDE [Start your PowerShell session](../../includes/sql-database-powershell.md)]

## <a name="create-an-elastic-pool"></a>Criar um pool elástico
Olá [AzureRmSqlElasticPool novo](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) cmdlet cria um pool Elástico. valores de saudação de eDTU por pool, min e max DTUs são restritas por valor de nível de serviço hello (Basic, Standard, Premium ou Premium RS). Confira [Limites de eDTU e armazenamento para pools elásticos e bancos de dados em pool](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools).

```PowerShell
New-AzureRmSqlElasticPool -ResourceGroupName "resourcegroup1" -ServerName "server1" -ElasticPoolName "elasticpool1" -Edition "Standard" -Dtu 400 -DatabaseDtuMin 10 -DatabaseDtuMax 100
```

## <a name="create-a-pooled-database-in-an-elastic-pool"></a>Criar um banco de dados em pool em um pool elástico
Saudação de uso [New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) cmdlet e conjunto hello **ElasticPoolName** pool de destino do parâmetro toohello. toomove banco de dados existente em um pool Elástico, consulte [mover um banco de dados para um pool Elástico](sql-database-elastic-pool-manage-powershell.md#move-a-database-into-an-elastic-pool).

```PowerShell
New-AzureRmSqlDatabase -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

### <a name="complete-script"></a>Script completo
Esse script cria um grupo de recursos do Azure e um servidor. Quando solicitado, forneça um nome de usuário administrador e a senha para o novo servidor de saudação (não suas credenciais do Azure).

```PowerShell
$subscriptionId = '<your Azure subscription id>'
$resourceGroupName = '<resource group name>'
$location = '<datacenter location>'
$serverName = '<server name>'
$poolName = '<pool name>'
$databaseName = '<database name>'

Login-AzureRmAccount
Set-AzureRmContext -SubscriptionId $subscriptionId

New-AzureRmResourceGroup -Name $resourceGroupName -Location $location
New-AzureRmSqlServer -ResourceGroupName $resourceGroupName -ServerName $serverName -Location $location -ServerVersion "12.0"
New-AzureRmSqlServerFirewallRule -ResourceGroupName $resourceGroupName -ServerName $serverName -FirewallRuleName "rule1" -StartIpAddress "192.168.0.198" -EndIpAddress "192.168.0.199"

New-AzureRmSqlElasticPool -ResourceGroupName $resourceGroupName -ServerName $serverName -ElasticPoolName $poolName -Edition "Standard" -Dtu 400 -DatabaseDtuMin 10 -DatabaseDtuMax 100

New-AzureRmSqlDatabase -ResourceGroupName $resourceGroupName -ServerName $serverName -DatabaseName $databaseName -ElasticPoolName $poolName -MaxSizeBytes 10GB
```

## <a name="create-an-elastic-pool-and-add-multiple-pooled-databases"></a>Criar um pool elástico e adicionar vários bancos de dados em pool
Criação de muitos bancos de dados em um pool Elástico pode levar tempo quando feito usando o portal de saudação ou cmdlets do PowerShell que criar apenas um único banco de dados de cada vez. criação de tooautomate em um pool Elástico, consulte [CreateOrUpdateElasticPoolAndPopulate ](https://gist.github.com/billgib/d80c7687b17355d3c2ec8042323819ae).

## <a name="move-a-database-into-an-elastic-pool"></a>Mover um banco de dados para um pool elástico
Você pode mover um banco de dados para dentro ou fora de um pool Elástico com hello [AzureRmSqlDatabase conjunto](/powershell/module/azurerm.sql/set-azurermsqlelasticpool).

```PowerShell
Set-AzureRmSqlDatabase -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

## <a name="change-performance-settings-of-an-elastic-pool"></a>Alterar as configurações de desempenho de um pool elástico
Quando o desempenho é prejudicado, você pode alterar as configurações de saudação do crescimento do hello pool tooaccommodate. Saudação de uso [AzureRmSqlElasticPool conjunto](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) cmdlet. Definir Olá - Dtu parâmetro toohello eDTUs por pool. Consulte os valores possível em [limites de armazenamento e eDTU](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools).

```PowerShell
Set-AzureRmSqlElasticPool -ResourceGroupName “resourcegroup1” -ServerName “server1” -ElasticPoolName “elasticpool1” -Dtu 1200 -DatabaseDtuMax 100 -DatabaseDtuMin 50
```

## <a name="change-hello-storage-limit-for-an-elastic-pool"></a>Alterar o limite de armazenamento de saudação para um pool Elástico

Saudação de uso [conjunto AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) cmdlet tooset Olá _- StorageMB_ parâmetro. Forneça o limite de armazenamento de saudação em MB (por exemplo, 2097152 conjuntos Olá armazenamento limite too2 TB). Consulte os valores possível em [limites de armazenamento e eDTU](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools).

> [!IMPORTANT]
> armazenamento de dados max saudação padrão por pool para pools de Premium com 1500 eDTUs ou mais é 750 GB. tooobtain Olá superior _máxima do tamanho de armazenamento de dados por pool_, limite de armazenamento Olá deve ser explicitamente definido. Pools de Premium com mais de 750 GB de armazenamento está atualmente em visualização pública no hello seguintes regiões: Leste dos EUA 2, oeste dos EUA, nós Gov Virgínia, Europa Ocidental, Alemanha Central, Sudeste da Ásia, Leste do Japão, Leste da Austrália, Canadá Central e Leste do Canadá.

```PowerShell
Set-AzureRmSqlElasticPool -ServerName "server1" -ElasticPoolName “elasticpool1” -StorageMB 2097152
```

## <a name="get-hello-status-of-pool-operations"></a>Obter status de saudação de operações de pool
Criar um pool elástico pode levar tempo. status de saudação tootrack das operações de pool, incluindo a criação e atualizações, use Olá [AzureRmSqlElasticPoolActivity Get](/powershell/module/azurerm.sql/get-azurermsqlelasticpoolactivity) cmdlet.

```PowerShell
Get-AzureRmSqlElasticPoolActivity -ResourceGroupName “resourcegroup1” -ServerName “server1” -ElasticPoolName “elasticpool1”
```

## <a name="get-hello-status-of-moving-a-database-into-and-out-of-an-elastic-pool"></a>Obter status de saudação de mover um banco de dados dentro e fora de um pool Elástico
Mover um banco de dados pode levar tempo. Controlar status mover usando Olá [AzureRmSqlDatabaseActivity Get](/powershell/module/azurerm.sql/get-azurermsqldatabaseactivity) cmdlet.

```PowerShell
Get-AzureRmSqlDatabaseActivity -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

## <a name="get-resource-usage-data-for-an-elastic-pool"></a>Obter dados de uso de recursos para um pool elástico
Métricas que podem ser recuperadas como uma porcentagem do limite do pool de recursos de saudação:

| Nome da métrica | Descrição |
|:--- |:--- |
| cpu\_percent |Média de utilização em porcentagem do limite de saudação do pool de saudação de computação. |
| physical\_data\_read\_percent |Utilização média de e/s em porcentagem com base no limite de saudação do pool de saudação. |
| log\_write\_percent |Média de utilização de recursos de gravação em porcentagem do limite de saudação do pool de saudação. |
| DTU\_consumption\_percent |Utilização média de eDTU em porcentagem do limite de eDTU de pool de saudação |
| storage\_percent |Média de utilização do armazenamento em porcentagem do limite de armazenamento de saudação do pool de saudação. |
| workers\_percent |Máximo simultâneos trabalhadores (solicitações) em porcentagem com base no limite de saudação do pool de saudação. |
| sessions\_percent |Máximo de sessões simultâneas em porcentagem com base no limite de saudação do pool de saudação. |
| eDTU_limit |Configuração atual de DTUs máximas do pool elástico para este pool elástico durante este intervalo. |
| storage\_limit |Configuração atual de limite máximo de armazenamento do pool elástico para este pool elástico em megabytes durante este intervalo. |
| eDTU\_used |EDTUs média usada pelo pool de saudação nesse intervalo. |
| storage\_used |Armazenamento média usado pelo pool de saudação nesse intervalo, em bytes |

**Períodos de retenção/granularidade das métricas:**

* Os dados retornam com uma granularidade de cinco minutos.  
* A retenção dos dados é de 35 dias.  

Esse cmdlet e API limita o número de saudação de linhas que podem ser recuperados em uma chamada too1000 linhas (cerca de 3 dias de dados na granularidade de 5 minutos). Mas esse comando pode ser chamado várias vezes com tooretrieve de intervalos de tempo diferentes de início/término mais dados

métricas de saudação tooretrieve:

```PowerShell
$metrics = (Get-AzureRmMetric -ResourceId /subscriptions/<subscriptionId>/resourceGroups/FabrikamData01/providers/Microsoft.Sql/servers/fabrikamsqldb02/elasticPools/franchisepool -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime "4/18/2015" -EndTime "4/21/2015")
```

## <a name="get-resource-usage-data-for-a-database-in-an-elastic-pool"></a>Obter dados de uso de recursos de um banco de dados em um pool elástico
Essas APIs são Olá mesmo Olá APIs usadas para monitorar a utilização de recursos de saudação de um único banco de dados, exceto Olá diferença semântica a seguir: métricas recuperadas são expressos como uma porcentagem da saudação por eDTUs máximo do banco de dados (ou equivalente cap para Olá Base métrica, como CPU ou e/s) definido para esse pool. Por exemplo, a 50% de utilização de qualquer uma dessas métricas indica que o consumo de recursos específicos de saudação é a 50% da saudação por limite de banco de dados para esse recurso no pool de pai hello.

métricas de saudação tooretrieve:

```PowerShell
$metrics = (Get-AzureRmMetric -ResourceId /subscriptions/<subscriptionId>/resourceGroups/FabrikamData01/providers/Microsoft.Sql/servers/fabrikamsqldb02/databases/myDB -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime "4/18/2015" -EndTime "4/21/2015")
```

## <a name="add-an-alert-tooan-elastic-pool-resource"></a>Adicionar um recurso de pool Elástico tooan alerta
Você pode adicionar regras de alerta tooan pool Elástico toosend notificações por email ou alerta cadeias de caracteres muito[pontos de extremidade de URL](https://msdn.microsoft.com/library/mt718036.aspx) quando o pool Elástico Olá atinge um limite de utilização que você configurou. Use o cmdlet Olá AzureRmMetricAlertRule adicionar.

> [!IMPORTANT]
> O monitoramento de utilização de recursos para pools elásticos tem um atraso de, pelo menos, 5 minutos. No momento, não é permitido definir alertas de menos de 10 minutos para pools elásticos. Todos os alertas definidos para pools Elásticos com um ponto (chamado de parâmetro "-Tamanho_da_janela" na API do PowerShell) de menos de 10 minutos pode não ser disparada. Certifique-se de que todos os alertas definidos para pools elásticos usem um período (WindowSize) de 10 minutos ou mais.
>
>

Este exemplo adiciona um alerta para ser notificado quando o consumo de eDTU de um pool elástico ultrapassar determinado limite.

```PowerShell
# Set up your resource ID configurations
$subscriptionId = '<Azure subscription id>'      # Azure subscription ID
$location =  '<location'                         # Azure region
$resourceGroupName = '<resource group name>'     # Resource Group
$serverName = '<server name>'                    # server name
$poolName = '<elastic pool name>'                # pool name

#$Target Resource ID
$ResourceID = '/subscriptions/' + $subscriptionId + '/resourceGroups/' +$resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/elasticpools/' + $poolName

# Create an email action
$actionEmail = New-AzureRmAlertRuleEmail -SendToServiceOwners -CustomEmail JohnDoe@contoso.com

# create a unique rule name
$alertName = $poolName + "- DTU consumption rule"

# Create an alert rule for DTU_consumption_percent
Add-AzureRMMetricAlertRule -Name $alertName -Location $location -ResourceGroup $resourceGroupName -TargetResourceId $ResourceID -MetricName "DTU_consumption_percent"  -Operator GreaterThan -Threshold 80 -TimeAggregationOperator Average -WindowSize 00:60:00 -Actions $actionEmail
```

Para obter mais informações, consulte [Criar alertas do Banco de Dados SQL no portal do Azure](sql-database-insights-alerts-portal.md).

## <a name="add-alerts-tooall-databases-in-an-elastic-pool"></a>Adicionar bancos de dados de tooall alertas em um pool Elástico
Você pode adicionar regras de alerta tooall banco de dados em um pool Elástico toosend notificações por email ou alerta cadeias de caracteres muito[pontos de extremidade de URL](https://msdn.microsoft.com/library/mt718036.aspx) quando um recurso atinge um limite de utilização configurado pelo alerta hello.

> [!IMPORTANT]
> O monitoramento de utilização de recursos para pools elásticos tem um atraso de, pelo menos, 5 minutos. No momento, não é permitido definir alertas de menos de 10 minutos para pools elásticos. Todos os alertas definidos para pools Elásticos com um ponto (chamado de parâmetro "-Tamanho_da_janela" na API do PowerShell) de menos de 10 minutos pode não ser disparada. Certifique-se de que todos os alertas definidos para pools elásticos usem um período (WindowSize) de 10 minutos ou mais.
>

Este exemplo adiciona um alerta tooeach de bancos de dados de saudação em um pool Elástico para ser notificado quando o consumo de DTU do banco de dados fica acima de certo limite.

```PowerShell
# Set up your resource ID configurations
$subscriptionId = '<Azure subscription id>'      # Azure subscription ID
$location = '<location'                          # Azure region
$resourceGroupName = '<resource group name>'     # Resource Group
$serverName = '<server name>'                    # server name
$poolName = '<elastic pool name>'                # pool name

# Get hello list of databases in this pool.
$dbList = Get-AzureRmSqlElasticPoolDatabase -ResourceGroupName $resourceGroupName -ServerName $serverName -ElasticPoolName $poolName

# Create an email action
$actionEmail = New-AzureRmAlertRuleEmail -SendToServiceOwners -CustomEmail JohnDoe@contoso.com

# Get resource usage metrics for a database in an elastic pool for hello specified time interval.
foreach ($db in $dbList)
{
    $dbResourceId = '/subscriptions/' + $subscriptionId + '/resourceGroups/' + $resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/databases/' + $db.DatabaseName

    # create a unique rule name
    $alertName = $db.DatabaseName + "- DTU consumption rule"

    # Create an alert rule for DTU_consumption_percent
    Add-AzureRMMetricAlertRule -Name $alertName  -Location $location -ResourceGroup $resourceGroupName -TargetResourceId $dbResourceId -MetricName "dtu_consumption_percent"  -Operator GreaterThan -Threshold 80 -TimeAggregationOperator Average -WindowSize 00:60:00 -Actions $actionEmail

    # drop hello alert rule
    #Remove-AzureRmAlertRule -ResourceGroup $resourceGroupName -Name $alertName
}
```

## <a name="collect-and-monitor-resource-usage-data-across-multiple-pools-in-a-subscription"></a>Coletar e monitorar dados de uso de recursos em vários pools em uma assinatura
Quando você tiver vários bancos de dados em uma assinatura, é complicado toomonitor cada elástica pool separadamente. Em vez disso, cmdlets do PowerShell de banco de dados SQL e consultas T-SQL podem ser dados de uso de recursos toocollect combinado de vários pools e seus bancos de dados para monitoramento e análise da utilização de recursos. Um [implementação de exemplo](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools) de tal um conjunto de powershell scripts podem encontrados no repositório de exemplos do hello GitHub SQL Server junto com a documentação sobre o que ele faz e como toouse-lo.

toouse Este exemplo de implementação, siga estas etapas.

1. Baixar Olá [scripts e a documentação](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools):
2. Modifique os scripts Olá para o seu ambiente. Especifique um ou mais servidores nos quais os pools elásticos são hospedados.
3. Especifique um banco de dados de telemetria onde hello métricas coletadas são toobe armazenado.
4. Personalize Olá script toospecify Olá durante execução de scripts de saudação.

Em um nível alto, scripts Olá Olá a seguir:

* Enumera todos os servidores em uma determinada assinatura do Azure (ou uma lista de servidores específicos).
* Executa um trabalho em segundo plano para cada servidor. trabalho de saudação é executado em um loop em intervalos regulares e coleta dados de telemetria para todos os pools de saudação no servidor de saudação. Ele carrega dados Olá coletado no banco de dados de telemetria especificado hello.
* Enumera uma lista de bancos de dados em dados de uso de recursos de banco de dados cada pool toocollect hello. Ele carrega dados Olá coletado no banco de dados de telemetria hello.

Hello métricas coletadas no banco de dados de telemetria Olá podem ser analisados toomonitor Olá integridade de pools Elásticos e bancos de dados Olá nele. script Hello também instala uma função de valor de tabela (TVF) predefinida em métricas de agregação Olá Olá telemetria banco de dados toohelp para uma janela de tempo especificado. Por exemplo, os resultados da saudação TVF podem ser usado tooshow "top N pools Elásticos com a utilização de eDTU máximo Olá em uma janela de tempo determinado." Opcionalmente, use ferramentas analíticas, como Excel ou Power BI tooquery e analisar dados coletado de saudação.

### <a name="example-retrieve-resource-consumption-metrics-for-an-elastic-pool-and-its-databases"></a>Exemplo: recuperar as métricas de consumo de recursos para um pool elástico e seus bancos de dados
Este exemplo recupera as métricas de consumo de saudação para um determinado pool Elástico e todos os seus bancos de dados. Os dados coletados são formatados e escritos tooa formatado. csv. arquivo Hello possa ser navegado com o Excel.

```PowerShell
$subscriptionId = '<Azure subscription id>'          # Azure subscription ID
$resourceGroupName = '<resource group name>'             # Resource Group
$serverName = <server name>                              # server name
$poolName = <elastic pool name>                          # pool name

# Login tooAzure account and select hello subscription.
Login-AzureRmAccount
Set-AzureRmContext -SubscriptionId $subscriptionId

# Get resource usage metrics for an elastic pool for hello specified time interval.
$startTime = '4/27/2016 00:00:00'  # start time in UTC
$endTime = '4/27/2016 01:00:00'    # end time in UTC

# Construct hello pool resource ID and retrive pool metrics at 5-minute granularity.
$poolResourceId = '/subscriptions/' + $subscriptionId + '/resourceGroups/' + $resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/elasticPools/' + $poolName
$poolMetrics = (Get-AzureRmMetric -ResourceId $poolResourceId -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime $startTime -EndTime $endTime)

# Get hello list of databases in this pool.
$dbList = Get-AzureRmSqlElasticPoolDatabase -ResourceGroupName $resourceGroupName -ServerName $serverName -ElasticPoolName $poolName

# Get resource usage metrics for a database in an elastic pool for hello specified time interval.
$dbMetrics = @()
foreach ($db in $dbList)
{
     $dbResourceId = '/subscriptions/' + $subscriptionId + '/resourceGroups/' + $resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/databases/' + $db.DatabaseName
     $dbMetrics = $dbMetrics + (Get-AzureRmMetric -ResourceId $dbResourceId -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime $startTime -EndTime $endTime)
}

#Optionally you can format hello metrics and output as .csv file using hello following script block.
$command = {
param($metricList, $outputFile)

# Format metrics into a table.
$table = @()
foreach($metric in $metricList) {
   foreach($metricValue in $metric.MetricValues) {
      $sx = New-Object PSObject -Property @{
      Timestamp = $metricValue.Timestamp.ToString()
      MetricName = $metric.Name;
      Average = $metricValue.Average;
      ResourceID = $metric.ResourceId
   }$table = $table += $sx
   }
}

# Output hello metrics into a .csv file.
write-output $table | Export-csv -Path $outputFile -Append -NoTypeInformation
}

# Format and output pool metrics
Invoke-Command -ScriptBlock $command -ArgumentList $poolMetrics,c:\temp\poolmetrics.csv

# Format and output database metrics
Invoke-Command -ScriptBlock $command -ArgumentList $dbMetrics,c:\temp\dbmetrics.csv
```

## <a name="latency-of-elastic-pool-operations"></a>Latência de operações do pool elástico
* Alterar Olá min eDTUs por banco de dados ou o máximo de eDTUs por banco de dados normalmente é concluído em 5 minutos ou menos.
* Alterar eDTUs Olá por pool de depende da quantidade total de saudação do espaço usado por todos os bancos de dados no pool de saudação. As alterações levam, em média, 90 minutos ou menos a cada 100 GB. Por exemplo, se o espaço total Olá usado por todos os bancos de dados no pool de saudação é de 200 GB, Olá esperada de latência para mudar o eDTU do pool de saudação por pool é de 3 horas ou menos.



## <a name="next-steps"></a>Próximas etapas
* [Criar trabalhos Elásticos](sql-database-elastic-jobs-overview.md) trabalhos Elásticos permitem executar scripts T-SQL em relação a qualquer número de bancos de dados no pool de saudação.
* Consulte [expansão com o Azure SQL Database](sql-database-elastic-scale-introduction.md): usar ferramentas Elástico tooscale out, mover os dados, consultar ou criar transações.
