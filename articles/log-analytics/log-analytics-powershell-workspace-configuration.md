---
title: "aaaUse PowerShell tooCreate e configurar um espaço de trabalho de análise de Log | Microsoft Docs"
description: "O Log Analytics usa dados de servidores em sua infraestrutura local ou na nuvem. Você pode coletar dados da máquina do armazenamento do Azure quando gerados pelo diagnóstico do Azure."
services: log-analytics
documentationcenter: 
author: richrundmsft
manager: jochan
editor: 
ms.assetid: 3b9b7ade-3374-4596-afb1-51b695f481c2
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: powershell
ms.topic: article
ms.date: 11/21/2016
ms.author: richrund
ms.openlocfilehash: a6d66194204cc58de6aafb687a19fe9611e0c58e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-log-analytics-using-powershell"></a>Gerenciar o Log Analytics usando o PowerShell
Você pode usar o hello [cmdlets do PowerShell de análise de Log](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) tooperform várias funções de análise de Log de uma linha de comando ou como parte de um script.  Exemplos de tarefas de saudação que podem ser executadas com o PowerShell:

* Criar um espaço de trabalho
* Adicionar ou remover uma solução
* Importar e exportar pesquisas salvas
* Criar um grupo de computadores
* Habilitar a coleta de logs do IIS nos computadores com o agente do Windows hello instalado
* Coletar contadores de desempenho de computadores Linux e Windows
* Coletar eventos de syslog em computadores Linux 
* Coletar eventos dos logs de eventos do Windows
* Coletar logs de eventos personalizados
* Adicionar Olá log analytics agente tooan máquina virtual do Azure
* Configurar log analytics tooindex dados coletados usando o diagnóstico do Azure

Este artigo fornece dois exemplos de código que ilustram algumas das funções de saudação que você pode executar no PowerShell.  Você pode consultar toohello [referência de cmdlet do PowerShell de análise de Log](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) para outras funções.

> [!NOTE]
> Análise de log anteriormente era chamada de Insights operacionais, é por isso que é usado em cmdlets de saudação de nome de saudação.
> 
> 

## <a name="prerequisites"></a>Pré-requisitos
Esses exemplos funcionam com a versão 2.3.0 ou posterior do módulo de AzureRm.OperationalInsights hello.


## <a name="create-and-configure-a-log-analytics-workspace"></a>Criar e configurar um espaço de trabalho do Log Analytics
Olá exemplo de script a seguir ilustra como:

1. Criar um espaço de trabalho
2. Soluções disponíveis de saudação de lista
3. Adicionar espaço de trabalho de toohello de soluções
4. Importar pesquisas salvas
5. Exportar pesquisas salvas
6. Criar um grupo de computadores
7. Habilitar a coleta de logs do IIS nos computadores com o agente do Windows hello instalado
8. Coletar contadores de desempenho de disco lógico de computadores Linux (% Used Inodes; Free Megabytes; % Used Space; Disk Transfers/sec; Disk Reads/sec; Disk Writes/sec)
9. Coletar eventos de syslog em computadores Linux
10. Coletar eventos de erro e aviso de saudação Log de eventos do aplicativo de computadores Windows
11. Coletar o contador de desempenho de Mbytes Disponíveis de Memória de computadores Windows
12. Coletar um log personalizado 

```

$ResourceGroup = "oms-example"
$WorkspaceName = "log-analytics-" + (Get-Random -Maximum 99999) # workspace names need toobe unique - Get-Random helps with this for hello example code
$Location = "westeurope"

# List of solutions tooenable
$Solutions = "Security", "Updates", "SQLAssessment"

# Saved Searches tooimport
$ExportedSearches = @"
[
    {
        "Category":  "My Saved Searches",
        "DisplayName":  "WAD Events (All)",
        "Query":  "Type=Event SourceSystem:AzureStorage ",
        "Version":  1
    },
    {        
        "Category":  "My Saved Searches",
        "DisplayName":  "Current Disk Queue Length",
        "Query":  "Type=Perf ObjectName=LogicalDisk InstanceName=\"C:\" CounterName=\"Current Disk Queue Length\"",
        "Version":  1
    }
]
"@ | ConvertFrom-Json

# Custom Log toocollect
$CustomLog = @"
{
    "customLogName": "sampleCustomLog1", 
    "description": "Example custom log datasource", 
    "inputs": [
        { 
            "location": { 
            "fileSystemLocations": { 
                "windowsFileTypeLogPaths": [ "e:\\iis5\\*.log" ], 
                "linuxFileTypeLogPaths": [ "/var/logs" ] 
                } 
            }, 
        "recordDelimiter": { 
            "regexDelimiter": { 
                "pattern": "\\n", 
                "matchIndex": 0, 
                "matchIndexSpecified": true, 
                "numberedGroup": null 
                } 
            } 
        }
    ], 
    "extractions": [
        { 
            "extractionName": "TimeGenerated", 
            "extractionType": "DateTime", 
            "extractionProperties": { 
                "dateTimeExtraction": { 
                    "regex": null, 
                    "joinStringRegex": null 
                    } 
                } 
            }
        ] 
    }
"@

# Create hello resource group if needed
try {
    Get-AzureRmResourceGroup -Name $ResourceGroup -ErrorAction Stop
} catch {
    New-AzureRmResourceGroup -Name $ResourceGroup -Location $Location
}

# Create hello workspace
New-AzureRmOperationalInsightsWorkspace -Location $Location -Name $WorkspaceName -Sku Standard -ResourceGroupName $ResourceGroup

# List all solutions and their installation status
Get-AzureRmOperationalInsightsIntelligencePacks -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName

# Add solutions
foreach ($solution in $Solutions) {
    Set-AzureRmOperationalInsightsIntelligencePack -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName -IntelligencePackName $solution -Enabled $true
}

#List enabled solutions
(Get-AzureRmOperationalInsightsIntelligencePacks -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName).Where({($_.enabled -eq $true)})

# Import Saved Searches
foreach ($search in $ExportedSearches) {
    $id = $search.Category + "|" + $search.DisplayName
    New-AzureRmOperationalInsightsSavedSearch -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName -SavedSearchId $id -DisplayName $search.DisplayName -Category $search.Category -Query $search.Query -Version $search.Version
}

# Export Saved Searches
(Get-AzureRmOperationalInsightsSavedSearch -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName).Value.Properties | ConvertTo-Json 

# Create Computer Group based on a query
New-AzureRmOperationalInsightsComputerGroup -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName -SavedSearchId "My Web Servers" -DisplayName "Web Servers" -Category "My Saved Searches" -Query "Computer=""web*"" | distinct Computer" -Version 1

# Create a computer group based on names (up too5000)
$computerGroup = """servername1.contoso.com"",""servername2.contoso.com"",""servername3.contoso.com"",""servername4.contoso.com"""
New-AzureRmOperationalInsightsComputerGroup -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName -SavedSearchId "My Named Servers" -DisplayName "Named Servers" -Category "My Saved Searches" -Query $computerGroup -Version 1

# Enable IIS Log Collection using agent
Enable-AzureRmOperationalInsightsIISLogCollection -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName

# Linux Perf
New-AzureRmOperationalInsightsLinuxPerformanceObjectDataSource -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName -ObjectName "Logical Disk" -InstanceName "*"  -CounterNames @("% Used Inodes", "Free Megabytes", "% Used Space", "Disk Transfers/sec", "Disk Reads/sec", "Disk Reads/sec", "Disk Writes/sec") -IntervalSeconds 20  -Name "Example Linux Disk Performance Counters"
Enable-AzureRmOperationalInsightsLinuxCustomLogCollection -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName

# Linux Syslog
New-AzureRmOperationalInsightsLinuxSyslogDataSource -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName -Facility "kern" -CollectEmergency -CollectAlert -CollectCritical -CollectError -CollectWarning -Name "Example kernal syslog collection"
Enable-AzureRmOperationalInsightsLinuxSyslogCollection -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName

# Windows Event
New-AzureRmOperationalInsightsWindowsEventDataSource -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName -EventLogName "Application" -CollectErrors -CollectWarnings -Name "Example Application Event Log"

# Windows Perf
New-AzureRmOperationalInsightsWindowsPerformanceCounterDataSource -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName -ObjectName "Memory" -InstanceName "*" -CounterName "Available MBytes" -IntervalSeconds 20 -Name "Example Windows Performance Counter"

# Custom Logs
New-AzureRmOperationalInsightsCustomLogDataSource -ResourceGroupName $ResourceGroup -WorkspaceName $WorkspaceName -CustomLogRawJson "$CustomLog" -Name "Example Custom Log Collection"

```

## <a name="configuring-log-analytics-tooindex-azure-diagnostics"></a>Configurando a análise de Log tooindex diagnóstico do Azure
Monitoramento sem agente dos recursos do Azure, Olá recursos precisam de espaço de trabalho do toohave diagnóstico do Azure habilitado e configurado toowrite tooa análise de Log. Essa abordagem envia dados diretamente tooLog análise e não requer toobe dados gravado tooa conta de armazenamento. Os recursos com suporte incluem:

| Tipo de recurso | Logs | Métricas |
| --- | --- | --- |
| Gateways do Aplicativo    | Sim | Sim |
| Contas de automação     | Sim | |
| Contas do Lote          | Sim | Sim |
| Data Lake Analytics     | Sim | | 
| Data Lake Store         | Sim | |
| Pool SQL Elástico        |     | Sim |
| Namespace do Hub de Eventos     |     | Sim |
| Hubs IoT                |     | Sim |
| Cofre da Chave               | Sim | |
| Balanceadores de Carga          | Sim | |
| Aplicativos Lógicos              | Sim | Sim |
| Grupos de segurança de rede | Sim | |
| Cache Redis             |     | Sim |
| Serviços de pesquisa         | Sim | Sim |
| Namespace do Barramento de Serviço   |     | Sim |
| SQL (v12)               |     | Sim |
| Sites               |     | Sim |
| Farms do servidor Web        |     | Sim |

Para obter detalhes de saudação de métricas disponíveis Olá, consulte muito[suporte para métricas com o Azure Monitor](../monitoring-and-diagnostics/monitoring-supported-metrics.md).

Para obter detalhes de saudação dos logs disponíveis hello, consulte muito[serviços e esquema com suporte para logs de diagnóstico](../monitoring-and-diagnostics/monitoring-diagnostic-logs-schema.md).

```
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$resourceId = "/SUBSCRIPTIONS/ec11ca60-1234-491e-5678-0ea07feae25c/RESOURCEGROUPS/DEMO/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/DEMO" 

Set-AzureRmDiagnosticSetting -ResourceId $resourceId -WorkspaceId $workspaceId -Enabled $true
```

Você também pode usar o hello anterior cmdlet toocollect registros de recursos que estão em assinaturas diferentes. Olá cmdlet é capaz de toowork em assinaturas desde que você está fornecendo o id de saudação de ambos os recursos de saudação criar logs e logs de saudação do espaço de trabalho Olá são enviados para.


## <a name="configuring-log-analytics-tooindex-azure-diagnostics-from-storage"></a>Configurando a análise de Log tooindex diagnóstico do armazenamento do Azure
dados de log toocollect de dentro de uma instância em execução de um serviço de nuvem clássico ou um cluster de malha do serviço, você precisa de toofirst gravação Olá dados tooAzure armazenamento. Análise de log, em seguida, é configurado toocollect logs de Olá Olá da conta de armazenamento. Os recursos com suporte incluem:

* Serviços de nuvem clássicos (funções de web e de trabalho)
* Clusters do Service Fabric

Olá mostrado no exemplo a seguir como a:

1. Olá listar contas de armazenamento existentes e os locais que indexa dados de análise de Log
2. Criar um tooread de configuração de conta de armazenamento
3. Atualizar Olá recém-criada em dados de configuração de tooindex de locais adicionais
4. Excluir configuração Olá recém-criado

```
# validTables = "WADWindowsEventLogsTable", "LinuxsyslogVer2v0", "WADServiceFabric*EventTable", "WADETWEventTable" 
$workspace = (Get-AzureRmOperationalInsightsWorkspace).Where({$_.Name -eq "your workspace name"})

# Update these two lines with hello storage account resource ID and hello storage account key for hello storage account you want tooLog Analytics too 
$storageId = "/subscriptions/ec11ca60-1234-491e-5678-0ea07feae25c/resourceGroups/demo/providers/Microsoft.Storage/storageAccounts/wadv2storage"
$key = "abcd=="

# List existing insights
Get-AzureRmOperationalInsightsStorageInsight -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name

# Create a new insight
New-AzureRmOperationalInsightsStorageInsight -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name -Name "newinsight" -StorageAccountResourceId $storageId -StorageAccountKey $key -Tables @("WADWindowsEventLogsTable") -Containers @("wad-iis-logfiles")

# Update existing insight
Set-AzureRmOperationalInsightsStorageInsight -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name -Name "newinsight" -Tables @("WADWindowsEventLogsTable", "WADETWEventTable") -Containers @("wad-iis-logfiles")

# Remove hello insight
Remove-AzureRmOperationalInsightsStorageInsight -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name -Name "newinsight" 

```

Você também pode usar o hello anterior logs de toocollect do script de contas de armazenamento em diferentes assinaturas. script Hello é capaz de toowork em assinaturas desde que você está fornecendo a id de recurso de conta de armazenamento hello e uma chave de acesso correspondente. Quando você alterar a chave de acesso Olá, é necessário tooupdate Olá insight toohave Olá nova chave de armazenamento.


## <a name="next-steps"></a>Próximas etapas
* [Examinar cmdlets do PowerShell do Log Analytics](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) para obter informações adicionais sobre como usar o PowerShell para a configuração do Log Analytics.

