---
title: "Usar o PowerShell para criar e configurar um espaço de trabalho do Log Analytics | Microsoft Docs"
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
ms.openlocfilehash: 6807ab67e3593da82c147669b29bfdae3b6c967c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="manage-log-analytics-using-powershell"></a><span data-ttu-id="e0360-104">Gerenciar o Log Analytics usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="e0360-104">Manage Log Analytics using PowerShell</span></span>
<span data-ttu-id="e0360-105">Você pode usar os [cmdlets do PowerShell do Log Analytics](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) para executar várias funções no Log Analytics de uma linha de comando ou como parte de um script.</span><span class="sxs-lookup"><span data-stu-id="e0360-105">You can use the [Log Analytics PowerShell cmdlets](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) to perform various functions in Log Analytics from a command line or as part of a script.</span></span>  <span data-ttu-id="e0360-106">Os exemplos das tarefas que você pode executar com o PowerShell incluem:</span><span class="sxs-lookup"><span data-stu-id="e0360-106">Examples of the tasks you can perform with PowerShell include:</span></span>

* <span data-ttu-id="e0360-107">Criar um espaço de trabalho</span><span class="sxs-lookup"><span data-stu-id="e0360-107">Create a workspace</span></span>
* <span data-ttu-id="e0360-108">Adicionar ou remover uma solução</span><span class="sxs-lookup"><span data-stu-id="e0360-108">Add or remove a solution</span></span>
* <span data-ttu-id="e0360-109">Importar e exportar pesquisas salvas</span><span class="sxs-lookup"><span data-stu-id="e0360-109">Import and export saved searches</span></span>
* <span data-ttu-id="e0360-110">Criar um grupo de computadores</span><span class="sxs-lookup"><span data-stu-id="e0360-110">Create a computer group</span></span>
* <span data-ttu-id="e0360-111">Habilitar coleta de logs do IIS de computadores com o agente do Windows instalado</span><span class="sxs-lookup"><span data-stu-id="e0360-111">Enable collection of IIS logs from computers with the Windows agent installed</span></span>
* <span data-ttu-id="e0360-112">Coletar contadores de desempenho de computadores Linux e Windows</span><span class="sxs-lookup"><span data-stu-id="e0360-112">Collect performance counters from Linux and Windows computers</span></span>
* <span data-ttu-id="e0360-113">Coletar eventos de syslog em computadores Linux</span><span class="sxs-lookup"><span data-stu-id="e0360-113">Collect events from syslog on Linux computers</span></span> 
* <span data-ttu-id="e0360-114">Coletar eventos dos logs de eventos do Windows</span><span class="sxs-lookup"><span data-stu-id="e0360-114">Collect events from Windows event logs</span></span>
* <span data-ttu-id="e0360-115">Coletar logs de eventos personalizados</span><span class="sxs-lookup"><span data-stu-id="e0360-115">Collect custom event logs</span></span>
* <span data-ttu-id="e0360-116">Adicionar o agente de análise de log a uma máquina virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="e0360-116">Add the log analytics agent to an Azure virtual machine</span></span>
* <span data-ttu-id="e0360-117">Configurar a análise de log para indexar os dados coletados usando o diagnóstico do Azure</span><span class="sxs-lookup"><span data-stu-id="e0360-117">Configure log analytics to index data collected using Azure diagnostics</span></span>

<span data-ttu-id="e0360-118">Este artigo fornece dois exemplos de código que ilustram algumas das funções que podem ser executadas do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e0360-118">This article provides two code samples that illustrate some of the functions that you can perform from PowerShell.</span></span>  <span data-ttu-id="e0360-119">Você pode consultar a [referência do cmdlet do PowerShell do Log Analytics](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) para outras funções.</span><span class="sxs-lookup"><span data-stu-id="e0360-119">You can refer to the [Log Analytics PowerShell cmdlet reference](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) for other functions.</span></span>

> [!NOTE]
> <span data-ttu-id="e0360-120">O Log Analytics chamava-se Operational Insights, e é por isso que esse é o nome usado nos cmdlets.</span><span class="sxs-lookup"><span data-stu-id="e0360-120">Log Analytics was previously called Operational Insights, which is why it is the name used in the cmdlets.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="e0360-121">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e0360-121">Prerequisites</span></span>
<span data-ttu-id="e0360-122">Esses exemplos funcionam com a versão 2.3.0 ou posterior do módulo AzureRm.OperationalInsights.</span><span class="sxs-lookup"><span data-stu-id="e0360-122">These examples work with version 2.3.0 or later of the AzureRm.OperationalInsights module.</span></span>


## <a name="create-and-configure-a-log-analytics-workspace"></a><span data-ttu-id="e0360-123">Criar e configurar um espaço de trabalho do Log Analytics</span><span class="sxs-lookup"><span data-stu-id="e0360-123">Create and configure a Log Analytics Workspace</span></span>
<span data-ttu-id="e0360-124">O exemplo de script a seguir ilustra como:</span><span class="sxs-lookup"><span data-stu-id="e0360-124">The following script sample illustrates how to:</span></span>

1. <span data-ttu-id="e0360-125">Criar um espaço de trabalho</span><span class="sxs-lookup"><span data-stu-id="e0360-125">Create a workspace</span></span>
2. <span data-ttu-id="e0360-126">Listar as soluções disponíveis</span><span class="sxs-lookup"><span data-stu-id="e0360-126">List the available solutions</span></span>
3. <span data-ttu-id="e0360-127">Adicionar soluções ao espaço de trabalho</span><span class="sxs-lookup"><span data-stu-id="e0360-127">Add solutions to the workspace</span></span>
4. <span data-ttu-id="e0360-128">Importar pesquisas salvas</span><span class="sxs-lookup"><span data-stu-id="e0360-128">Import saved searches</span></span>
5. <span data-ttu-id="e0360-129">Exportar pesquisas salvas</span><span class="sxs-lookup"><span data-stu-id="e0360-129">Export saved searches</span></span>
6. <span data-ttu-id="e0360-130">Criar um grupo de computadores</span><span class="sxs-lookup"><span data-stu-id="e0360-130">Create a computer group</span></span>
7. <span data-ttu-id="e0360-131">Habilitar coleta de logs do IIS de computadores com o agente do Windows instalado</span><span class="sxs-lookup"><span data-stu-id="e0360-131">Enable collection of IIS logs from computers with the Windows agent installed</span></span>
8. <span data-ttu-id="e0360-132">Coletar contadores de desempenho de disco lógico de computadores Linux (% Used Inodes; Free Megabytes; % Used Space; Disk Transfers/sec; Disk Reads/sec; Disk Writes/sec)</span><span class="sxs-lookup"><span data-stu-id="e0360-132">Collect Logical Disk perf counters from Linux computers (% Used Inodes; Free Megabytes; % Used Space; Disk Transfers/sec; Disk Reads/sec; Disk Writes/sec)</span></span>
9. <span data-ttu-id="e0360-133">Coletar eventos de syslog em computadores Linux</span><span class="sxs-lookup"><span data-stu-id="e0360-133">Collect syslog events from Linux computers</span></span>
10. <span data-ttu-id="e0360-134">Coletar eventos de Erro e Aviso no Log de Eventos do Aplicativo dos computadores Windows</span><span class="sxs-lookup"><span data-stu-id="e0360-134">Collect Error and Warning events from the Application Event Log from Windows computers</span></span>
11. <span data-ttu-id="e0360-135">Coletar o contador de desempenho de Mbytes Disponíveis de Memória de computadores Windows</span><span class="sxs-lookup"><span data-stu-id="e0360-135">Collect Memory Available Mbytes performance counter from Windows computers</span></span>
12. <span data-ttu-id="e0360-136">Coletar um log personalizado</span><span class="sxs-lookup"><span data-stu-id="e0360-136">Collect a custom log</span></span> 

```

$ResourceGroup = "oms-example"
$WorkspaceName = "log-analytics-" + (Get-Random -Maximum 99999) # workspace names need to be unique - Get-Random helps with this for the example code
$Location = "westeurope"

# List of solutions to enable
$Solutions = "Security", "Updates", "SQLAssessment"

# Saved Searches to import
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

# Custom Log to collect
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

# Create the resource group if needed
try {
    Get-AzureRmResourceGroup -Name $ResourceGroup -ErrorAction Stop
} catch {
    New-AzureRmResourceGroup -Name $ResourceGroup -Location $Location
}

# Create the workspace
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

# Create a computer group based on names (up to 5000)
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

## <a name="configuring-log-analytics-to-index-azure-diagnostics"></a><span data-ttu-id="e0360-137">Configuração do Log Analytics para indexar os diagnósticos do Azure</span><span class="sxs-lookup"><span data-stu-id="e0360-137">Configuring Log Analytics to index Azure diagnostics</span></span>
<span data-ttu-id="e0360-138">Para o monitoramento de recursos do Azure realizado sem o uso de agente, os recursos precisam ter o diagnóstico do Azure habilitado e configurado para gravar em um espaço de trabalho do Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="e0360-138">For agentless monitoring of Azure resources, the resources need to have Azure diagnostics enabled and configured to write to a Log Analytics workspace.</span></span> <span data-ttu-id="e0360-139">Essa abordagem envia dados diretamente para o Log Analytics e não exige que dados sejam gravados para uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="e0360-139">This approach sends data directly to Log Analytics and does not require data to be written to a storage account.</span></span> <span data-ttu-id="e0360-140">Os recursos com suporte incluem:</span><span class="sxs-lookup"><span data-stu-id="e0360-140">Supported resources include:</span></span>

| <span data-ttu-id="e0360-141">Tipo de recurso</span><span class="sxs-lookup"><span data-stu-id="e0360-141">Resource Type</span></span> | <span data-ttu-id="e0360-142">Logs</span><span class="sxs-lookup"><span data-stu-id="e0360-142">Logs</span></span> | <span data-ttu-id="e0360-143">Métricas</span><span class="sxs-lookup"><span data-stu-id="e0360-143">Metrics</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e0360-144">Gateways do Aplicativo</span><span class="sxs-lookup"><span data-stu-id="e0360-144">Application Gateways</span></span>    | <span data-ttu-id="e0360-145">Sim</span><span class="sxs-lookup"><span data-stu-id="e0360-145">Yes</span></span> | <span data-ttu-id="e0360-146">Sim</span><span class="sxs-lookup"><span data-stu-id="e0360-146">Yes</span></span> |
| <span data-ttu-id="e0360-147">Contas de automação</span><span class="sxs-lookup"><span data-stu-id="e0360-147">Automation accounts</span></span>     | <span data-ttu-id="e0360-148">Sim</span><span class="sxs-lookup"><span data-stu-id="e0360-148">Yes</span></span> | |
| <span data-ttu-id="e0360-149">Contas do Lote</span><span class="sxs-lookup"><span data-stu-id="e0360-149">Batch accounts</span></span>          | <span data-ttu-id="e0360-150">Sim</span><span class="sxs-lookup"><span data-stu-id="e0360-150">Yes</span></span> | <span data-ttu-id="e0360-151">Sim</span><span class="sxs-lookup"><span data-stu-id="e0360-151">Yes</span></span> |
| <span data-ttu-id="e0360-152">Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="e0360-152">Data Lake analytics</span></span>     | <span data-ttu-id="e0360-153">Sim</span><span class="sxs-lookup"><span data-stu-id="e0360-153">Yes</span></span> | | 
| <span data-ttu-id="e0360-154">Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="e0360-154">Data Lake store</span></span>         | <span data-ttu-id="e0360-155">Sim</span><span class="sxs-lookup"><span data-stu-id="e0360-155">Yes</span></span> | |
| <span data-ttu-id="e0360-156">Pool SQL Elástico</span><span class="sxs-lookup"><span data-stu-id="e0360-156">Elastic SQL Pool</span></span>        |     | <span data-ttu-id="e0360-157">Sim</span><span class="sxs-lookup"><span data-stu-id="e0360-157">Yes</span></span> |
| <span data-ttu-id="e0360-158">Namespace do Hub de Eventos</span><span class="sxs-lookup"><span data-stu-id="e0360-158">Event Hub namespace</span></span>     |     | <span data-ttu-id="e0360-159">Sim</span><span class="sxs-lookup"><span data-stu-id="e0360-159">Yes</span></span> |
| <span data-ttu-id="e0360-160">Hubs IoT</span><span class="sxs-lookup"><span data-stu-id="e0360-160">IoT Hubs</span></span>                |     | <span data-ttu-id="e0360-161">Sim</span><span class="sxs-lookup"><span data-stu-id="e0360-161">Yes</span></span> |
| <span data-ttu-id="e0360-162">Cofre da Chave</span><span class="sxs-lookup"><span data-stu-id="e0360-162">Key Vault</span></span>               | <span data-ttu-id="e0360-163">Sim</span><span class="sxs-lookup"><span data-stu-id="e0360-163">Yes</span></span> | |
| <span data-ttu-id="e0360-164">Balanceadores de Carga</span><span class="sxs-lookup"><span data-stu-id="e0360-164">Load Balancers</span></span>          | <span data-ttu-id="e0360-165">Sim</span><span class="sxs-lookup"><span data-stu-id="e0360-165">Yes</span></span> | |
| <span data-ttu-id="e0360-166">Aplicativos Lógicos</span><span class="sxs-lookup"><span data-stu-id="e0360-166">Logic Apps</span></span>              | <span data-ttu-id="e0360-167">Sim</span><span class="sxs-lookup"><span data-stu-id="e0360-167">Yes</span></span> | <span data-ttu-id="e0360-168">Sim</span><span class="sxs-lookup"><span data-stu-id="e0360-168">Yes</span></span> |
| <span data-ttu-id="e0360-169">Grupos de segurança de rede</span><span class="sxs-lookup"><span data-stu-id="e0360-169">Network Security Groups</span></span> | <span data-ttu-id="e0360-170">Sim</span><span class="sxs-lookup"><span data-stu-id="e0360-170">Yes</span></span> | |
| <span data-ttu-id="e0360-171">Cache Redis</span><span class="sxs-lookup"><span data-stu-id="e0360-171">Redis Cache</span></span>             |     | <span data-ttu-id="e0360-172">Sim</span><span class="sxs-lookup"><span data-stu-id="e0360-172">Yes</span></span> |
| <span data-ttu-id="e0360-173">Serviços de pesquisa</span><span class="sxs-lookup"><span data-stu-id="e0360-173">Search services</span></span>         | <span data-ttu-id="e0360-174">Sim</span><span class="sxs-lookup"><span data-stu-id="e0360-174">Yes</span></span> | <span data-ttu-id="e0360-175">Sim</span><span class="sxs-lookup"><span data-stu-id="e0360-175">Yes</span></span> |
| <span data-ttu-id="e0360-176">Namespace do Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="e0360-176">Service Bus namespace</span></span>   |     | <span data-ttu-id="e0360-177">Sim</span><span class="sxs-lookup"><span data-stu-id="e0360-177">Yes</span></span> |
| <span data-ttu-id="e0360-178">SQL (v12)</span><span class="sxs-lookup"><span data-stu-id="e0360-178">SQL (v12)</span></span>               |     | <span data-ttu-id="e0360-179">Sim</span><span class="sxs-lookup"><span data-stu-id="e0360-179">Yes</span></span> |
| <span data-ttu-id="e0360-180">Sites</span><span class="sxs-lookup"><span data-stu-id="e0360-180">Web Sites</span></span>               |     | <span data-ttu-id="e0360-181">Sim</span><span class="sxs-lookup"><span data-stu-id="e0360-181">Yes</span></span> |
| <span data-ttu-id="e0360-182">Farms do servidor Web</span><span class="sxs-lookup"><span data-stu-id="e0360-182">Web Server farms</span></span>        |     | <span data-ttu-id="e0360-183">Sim</span><span class="sxs-lookup"><span data-stu-id="e0360-183">Yes</span></span> |

<span data-ttu-id="e0360-184">Para obter os detalhes das métricas disponíveis, consulte [métricas compatíveis com o Azure Monitor](../monitoring-and-diagnostics/monitoring-supported-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="e0360-184">For the details of the available metrics, refer to [supported metrics with Azure Monitor](../monitoring-and-diagnostics/monitoring-supported-metrics.md).</span></span>

<span data-ttu-id="e0360-185">Para obter os detalhes dos logs disponíveis, consulte [serviços e esquema com suporte para logs de diagnóstico](../monitoring-and-diagnostics/monitoring-diagnostic-logs-schema.md).</span><span class="sxs-lookup"><span data-stu-id="e0360-185">For the details of the available logs, refer to [supported services and schema for diagnostic logs](../monitoring-and-diagnostics/monitoring-diagnostic-logs-schema.md).</span></span>

```
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$resourceId = "/SUBSCRIPTIONS/ec11ca60-1234-491e-5678-0ea07feae25c/RESOURCEGROUPS/DEMO/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/DEMO" 

Set-AzureRmDiagnosticSetting -ResourceId $resourceId -WorkspaceId $workspaceId -Enabled $true
```

<span data-ttu-id="e0360-186">Você também pode usar o cmdlet anterior para coletar logs de recursos em assinaturas diferentes.</span><span class="sxs-lookup"><span data-stu-id="e0360-186">You can also use the preceding cmdlet to collect logs from resources that are in different subscriptions.</span></span> <span data-ttu-id="e0360-187">O cmdlet é capaz de trabalhar em assinaturas, pois você está fornecendo a id do recurso que está criando os logs e do espaço de trabalho para o qual os logs são enviados.</span><span class="sxs-lookup"><span data-stu-id="e0360-187">The cmdlet is able to work across subscriptions since you are providing the id of both the resource creating logs and the workspace the logs are sent to.</span></span>


## <a name="configuring-log-analytics-to-index-azure-diagnostics-from-storage"></a><span data-ttu-id="e0360-188">Configuração do Log Analytics para indexar os diagnósticos do Azure a partir do armazenamento</span><span class="sxs-lookup"><span data-stu-id="e0360-188">Configuring Log Analytics to index Azure diagnostics from storage</span></span>
<span data-ttu-id="e0360-189">Para coletar dados de log de dentro de uma instância em execução de um serviço de nuvem clássico ou em um cluster de service fabric, você precisa primeiro escrever os dados no armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="e0360-189">To collect log data from within a running instance of a classic cloud service or a service fabric cluster, you need to first write the data to Azure storage.</span></span> <span data-ttu-id="e0360-190">O Log Analytics é, então, configurado para coletar os logs da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="e0360-190">Log Analytics is then configured to collect the logs from the storage account.</span></span> <span data-ttu-id="e0360-191">Os recursos com suporte incluem:</span><span class="sxs-lookup"><span data-stu-id="e0360-191">Supported resources include:</span></span>

* <span data-ttu-id="e0360-192">Serviços de nuvem clássicos (funções de web e de trabalho)</span><span class="sxs-lookup"><span data-stu-id="e0360-192">Classic cloud services (web and worker roles)</span></span>
* <span data-ttu-id="e0360-193">Clusters do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="e0360-193">Service fabric clusters</span></span>

<span data-ttu-id="e0360-194">O exemplo a seguir mostra como:</span><span class="sxs-lookup"><span data-stu-id="e0360-194">The following example shows how to:</span></span>

1. <span data-ttu-id="e0360-195">Listar as contas de armazenamento existentes e os locais de onde o Log Analytics indexará os dados</span><span class="sxs-lookup"><span data-stu-id="e0360-195">List the existing storage accounts and locations that Log Analytics will index data from</span></span>
2. <span data-ttu-id="e0360-196">Criar uma configuração para ler de uma conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="e0360-196">Create a configuration to read from a storage account</span></span>
3. <span data-ttu-id="e0360-197">Atualizar a configuração criada recentemente para indexar dados de locais adicionais</span><span class="sxs-lookup"><span data-stu-id="e0360-197">Update the newly created configuration to index data from additional locations</span></span>
4. <span data-ttu-id="e0360-198">Excluir a configuração recém-criada</span><span class="sxs-lookup"><span data-stu-id="e0360-198">Delete the newly created configuration</span></span>

```
# validTables = "WADWindowsEventLogsTable", "LinuxsyslogVer2v0", "WADServiceFabric*EventTable", "WADETWEventTable" 
$workspace = (Get-AzureRmOperationalInsightsWorkspace).Where({$_.Name -eq "your workspace name"})

# Update these two lines with the storage account resource ID and the storage account key for the storage account you want to Log Analytics to  
$storageId = "/subscriptions/ec11ca60-1234-491e-5678-0ea07feae25c/resourceGroups/demo/providers/Microsoft.Storage/storageAccounts/wadv2storage"
$key = "abcd=="

# List existing insights
Get-AzureRmOperationalInsightsStorageInsight -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name

# Create a new insight
New-AzureRmOperationalInsightsStorageInsight -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name -Name "newinsight" -StorageAccountResourceId $storageId -StorageAccountKey $key -Tables @("WADWindowsEventLogsTable") -Containers @("wad-iis-logfiles")

# Update existing insight
Set-AzureRmOperationalInsightsStorageInsight -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name -Name "newinsight" -Tables @("WADWindowsEventLogsTable", "WADETWEventTable") -Containers @("wad-iis-logfiles")

# Remove the insight
Remove-AzureRmOperationalInsightsStorageInsight -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name -Name "newinsight" 

```

<span data-ttu-id="e0360-199">Você também pode usar o script anterior para coletar logs de contas de armazenamento em assinaturas diferentes.</span><span class="sxs-lookup"><span data-stu-id="e0360-199">You can also use the preceding script to collect logs from storage accounts in different subscriptions.</span></span> <span data-ttu-id="e0360-200">O script é capaz de trabalhar em assinaturas, pois você está fornecendo a id do recurso da conta de armazenamento e uma chave de acesso correspondente.</span><span class="sxs-lookup"><span data-stu-id="e0360-200">The script is able to work across subscriptions since you are providing the storage account resource id and a corresponding access key.</span></span> <span data-ttu-id="e0360-201">Quando você altera a chave de acesso, você precisa atualizar as informações de armazenamento para a nova chave.</span><span class="sxs-lookup"><span data-stu-id="e0360-201">When you change the access key, you need to update the storage insight to have the new key.</span></span>


## <a name="next-steps"></a><span data-ttu-id="e0360-202">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e0360-202">Next steps</span></span>
* <span data-ttu-id="e0360-203">[Examinar cmdlets do PowerShell do Log Analytics](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) para obter informações adicionais sobre como usar o PowerShell para a configuração do Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="e0360-203">[Review Log Analytics PowerShell cmdlets](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) for additional information on using PowerShell for configuration of Log Analytics.</span></span>

