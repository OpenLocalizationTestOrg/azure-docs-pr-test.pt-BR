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
# <a name="manage-log-analytics-using-powershell"></a><span data-ttu-id="28393-104">Gerenciar o Log Analytics usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="28393-104">Manage Log Analytics using PowerShell</span></span>
<span data-ttu-id="28393-105">Você pode usar o hello [cmdlets do PowerShell de análise de Log](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) tooperform várias funções de análise de Log de uma linha de comando ou como parte de um script.</span><span class="sxs-lookup"><span data-stu-id="28393-105">You can use hello [Log Analytics PowerShell cmdlets](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) tooperform various functions in Log Analytics from a command line or as part of a script.</span></span>  <span data-ttu-id="28393-106">Exemplos de tarefas de saudação que podem ser executadas com o PowerShell:</span><span class="sxs-lookup"><span data-stu-id="28393-106">Examples of hello tasks you can perform with PowerShell include:</span></span>

* <span data-ttu-id="28393-107">Criar um espaço de trabalho</span><span class="sxs-lookup"><span data-stu-id="28393-107">Create a workspace</span></span>
* <span data-ttu-id="28393-108">Adicionar ou remover uma solução</span><span class="sxs-lookup"><span data-stu-id="28393-108">Add or remove a solution</span></span>
* <span data-ttu-id="28393-109">Importar e exportar pesquisas salvas</span><span class="sxs-lookup"><span data-stu-id="28393-109">Import and export saved searches</span></span>
* <span data-ttu-id="28393-110">Criar um grupo de computadores</span><span class="sxs-lookup"><span data-stu-id="28393-110">Create a computer group</span></span>
* <span data-ttu-id="28393-111">Habilitar a coleta de logs do IIS nos computadores com o agente do Windows hello instalado</span><span class="sxs-lookup"><span data-stu-id="28393-111">Enable collection of IIS logs from computers with hello Windows agent installed</span></span>
* <span data-ttu-id="28393-112">Coletar contadores de desempenho de computadores Linux e Windows</span><span class="sxs-lookup"><span data-stu-id="28393-112">Collect performance counters from Linux and Windows computers</span></span>
* <span data-ttu-id="28393-113">Coletar eventos de syslog em computadores Linux</span><span class="sxs-lookup"><span data-stu-id="28393-113">Collect events from syslog on Linux computers</span></span> 
* <span data-ttu-id="28393-114">Coletar eventos dos logs de eventos do Windows</span><span class="sxs-lookup"><span data-stu-id="28393-114">Collect events from Windows event logs</span></span>
* <span data-ttu-id="28393-115">Coletar logs de eventos personalizados</span><span class="sxs-lookup"><span data-stu-id="28393-115">Collect custom event logs</span></span>
* <span data-ttu-id="28393-116">Adicionar Olá log analytics agente tooan máquina virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="28393-116">Add hello log analytics agent tooan Azure virtual machine</span></span>
* <span data-ttu-id="28393-117">Configurar log analytics tooindex dados coletados usando o diagnóstico do Azure</span><span class="sxs-lookup"><span data-stu-id="28393-117">Configure log analytics tooindex data collected using Azure diagnostics</span></span>

<span data-ttu-id="28393-118">Este artigo fornece dois exemplos de código que ilustram algumas das funções de saudação que você pode executar no PowerShell.</span><span class="sxs-lookup"><span data-stu-id="28393-118">This article provides two code samples that illustrate some of hello functions that you can perform from PowerShell.</span></span>  <span data-ttu-id="28393-119">Você pode consultar toohello [referência de cmdlet do PowerShell de análise de Log](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) para outras funções.</span><span class="sxs-lookup"><span data-stu-id="28393-119">You can refer toohello [Log Analytics PowerShell cmdlet reference](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) for other functions.</span></span>

> [!NOTE]
> <span data-ttu-id="28393-120">Análise de log anteriormente era chamada de Insights operacionais, é por isso que é usado em cmdlets de saudação de nome de saudação.</span><span class="sxs-lookup"><span data-stu-id="28393-120">Log Analytics was previously called Operational Insights, which is why it is hello name used in hello cmdlets.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="28393-121">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="28393-121">Prerequisites</span></span>
<span data-ttu-id="28393-122">Esses exemplos funcionam com a versão 2.3.0 ou posterior do módulo de AzureRm.OperationalInsights hello.</span><span class="sxs-lookup"><span data-stu-id="28393-122">These examples work with version 2.3.0 or later of hello AzureRm.OperationalInsights module.</span></span>


## <a name="create-and-configure-a-log-analytics-workspace"></a><span data-ttu-id="28393-123">Criar e configurar um espaço de trabalho do Log Analytics</span><span class="sxs-lookup"><span data-stu-id="28393-123">Create and configure a Log Analytics Workspace</span></span>
<span data-ttu-id="28393-124">Olá exemplo de script a seguir ilustra como:</span><span class="sxs-lookup"><span data-stu-id="28393-124">hello following script sample illustrates how to:</span></span>

1. <span data-ttu-id="28393-125">Criar um espaço de trabalho</span><span class="sxs-lookup"><span data-stu-id="28393-125">Create a workspace</span></span>
2. <span data-ttu-id="28393-126">Soluções disponíveis de saudação de lista</span><span class="sxs-lookup"><span data-stu-id="28393-126">List hello available solutions</span></span>
3. <span data-ttu-id="28393-127">Adicionar espaço de trabalho de toohello de soluções</span><span class="sxs-lookup"><span data-stu-id="28393-127">Add solutions toohello workspace</span></span>
4. <span data-ttu-id="28393-128">Importar pesquisas salvas</span><span class="sxs-lookup"><span data-stu-id="28393-128">Import saved searches</span></span>
5. <span data-ttu-id="28393-129">Exportar pesquisas salvas</span><span class="sxs-lookup"><span data-stu-id="28393-129">Export saved searches</span></span>
6. <span data-ttu-id="28393-130">Criar um grupo de computadores</span><span class="sxs-lookup"><span data-stu-id="28393-130">Create a computer group</span></span>
7. <span data-ttu-id="28393-131">Habilitar a coleta de logs do IIS nos computadores com o agente do Windows hello instalado</span><span class="sxs-lookup"><span data-stu-id="28393-131">Enable collection of IIS logs from computers with hello Windows agent installed</span></span>
8. <span data-ttu-id="28393-132">Coletar contadores de desempenho de disco lógico de computadores Linux (% Used Inodes; Free Megabytes; % Used Space; Disk Transfers/sec; Disk Reads/sec; Disk Writes/sec)</span><span class="sxs-lookup"><span data-stu-id="28393-132">Collect Logical Disk perf counters from Linux computers (% Used Inodes; Free Megabytes; % Used Space; Disk Transfers/sec; Disk Reads/sec; Disk Writes/sec)</span></span>
9. <span data-ttu-id="28393-133">Coletar eventos de syslog em computadores Linux</span><span class="sxs-lookup"><span data-stu-id="28393-133">Collect syslog events from Linux computers</span></span>
10. <span data-ttu-id="28393-134">Coletar eventos de erro e aviso de saudação Log de eventos do aplicativo de computadores Windows</span><span class="sxs-lookup"><span data-stu-id="28393-134">Collect Error and Warning events from hello Application Event Log from Windows computers</span></span>
11. <span data-ttu-id="28393-135">Coletar o contador de desempenho de Mbytes Disponíveis de Memória de computadores Windows</span><span class="sxs-lookup"><span data-stu-id="28393-135">Collect Memory Available Mbytes performance counter from Windows computers</span></span>
12. <span data-ttu-id="28393-136">Coletar um log personalizado</span><span class="sxs-lookup"><span data-stu-id="28393-136">Collect a custom log</span></span> 

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

## <a name="configuring-log-analytics-tooindex-azure-diagnostics"></a><span data-ttu-id="28393-137">Configurando a análise de Log tooindex diagnóstico do Azure</span><span class="sxs-lookup"><span data-stu-id="28393-137">Configuring Log Analytics tooindex Azure diagnostics</span></span>
<span data-ttu-id="28393-138">Monitoramento sem agente dos recursos do Azure, Olá recursos precisam de espaço de trabalho do toohave diagnóstico do Azure habilitado e configurado toowrite tooa análise de Log.</span><span class="sxs-lookup"><span data-stu-id="28393-138">For agentless monitoring of Azure resources, hello resources need toohave Azure diagnostics enabled and configured toowrite tooa Log Analytics workspace.</span></span> <span data-ttu-id="28393-139">Essa abordagem envia dados diretamente tooLog análise e não requer toobe dados gravado tooa conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="28393-139">This approach sends data directly tooLog Analytics and does not require data toobe written tooa storage account.</span></span> <span data-ttu-id="28393-140">Os recursos com suporte incluem:</span><span class="sxs-lookup"><span data-stu-id="28393-140">Supported resources include:</span></span>

| <span data-ttu-id="28393-141">Tipo de recurso</span><span class="sxs-lookup"><span data-stu-id="28393-141">Resource Type</span></span> | <span data-ttu-id="28393-142">Logs</span><span class="sxs-lookup"><span data-stu-id="28393-142">Logs</span></span> | <span data-ttu-id="28393-143">Métricas</span><span class="sxs-lookup"><span data-stu-id="28393-143">Metrics</span></span> |
| --- | --- | --- |
| <span data-ttu-id="28393-144">Gateways do Aplicativo</span><span class="sxs-lookup"><span data-stu-id="28393-144">Application Gateways</span></span>    | <span data-ttu-id="28393-145">Sim</span><span class="sxs-lookup"><span data-stu-id="28393-145">Yes</span></span> | <span data-ttu-id="28393-146">Sim</span><span class="sxs-lookup"><span data-stu-id="28393-146">Yes</span></span> |
| <span data-ttu-id="28393-147">Contas de automação</span><span class="sxs-lookup"><span data-stu-id="28393-147">Automation accounts</span></span>     | <span data-ttu-id="28393-148">Sim</span><span class="sxs-lookup"><span data-stu-id="28393-148">Yes</span></span> | |
| <span data-ttu-id="28393-149">Contas do Lote</span><span class="sxs-lookup"><span data-stu-id="28393-149">Batch accounts</span></span>          | <span data-ttu-id="28393-150">Sim</span><span class="sxs-lookup"><span data-stu-id="28393-150">Yes</span></span> | <span data-ttu-id="28393-151">Sim</span><span class="sxs-lookup"><span data-stu-id="28393-151">Yes</span></span> |
| <span data-ttu-id="28393-152">Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="28393-152">Data Lake analytics</span></span>     | <span data-ttu-id="28393-153">Sim</span><span class="sxs-lookup"><span data-stu-id="28393-153">Yes</span></span> | | 
| <span data-ttu-id="28393-154">Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="28393-154">Data Lake store</span></span>         | <span data-ttu-id="28393-155">Sim</span><span class="sxs-lookup"><span data-stu-id="28393-155">Yes</span></span> | |
| <span data-ttu-id="28393-156">Pool SQL Elástico</span><span class="sxs-lookup"><span data-stu-id="28393-156">Elastic SQL Pool</span></span>        |     | <span data-ttu-id="28393-157">Sim</span><span class="sxs-lookup"><span data-stu-id="28393-157">Yes</span></span> |
| <span data-ttu-id="28393-158">Namespace do Hub de Eventos</span><span class="sxs-lookup"><span data-stu-id="28393-158">Event Hub namespace</span></span>     |     | <span data-ttu-id="28393-159">Sim</span><span class="sxs-lookup"><span data-stu-id="28393-159">Yes</span></span> |
| <span data-ttu-id="28393-160">Hubs IoT</span><span class="sxs-lookup"><span data-stu-id="28393-160">IoT Hubs</span></span>                |     | <span data-ttu-id="28393-161">Sim</span><span class="sxs-lookup"><span data-stu-id="28393-161">Yes</span></span> |
| <span data-ttu-id="28393-162">Cofre da Chave</span><span class="sxs-lookup"><span data-stu-id="28393-162">Key Vault</span></span>               | <span data-ttu-id="28393-163">Sim</span><span class="sxs-lookup"><span data-stu-id="28393-163">Yes</span></span> | |
| <span data-ttu-id="28393-164">Balanceadores de Carga</span><span class="sxs-lookup"><span data-stu-id="28393-164">Load Balancers</span></span>          | <span data-ttu-id="28393-165">Sim</span><span class="sxs-lookup"><span data-stu-id="28393-165">Yes</span></span> | |
| <span data-ttu-id="28393-166">Aplicativos Lógicos</span><span class="sxs-lookup"><span data-stu-id="28393-166">Logic Apps</span></span>              | <span data-ttu-id="28393-167">Sim</span><span class="sxs-lookup"><span data-stu-id="28393-167">Yes</span></span> | <span data-ttu-id="28393-168">Sim</span><span class="sxs-lookup"><span data-stu-id="28393-168">Yes</span></span> |
| <span data-ttu-id="28393-169">Grupos de segurança de rede</span><span class="sxs-lookup"><span data-stu-id="28393-169">Network Security Groups</span></span> | <span data-ttu-id="28393-170">Sim</span><span class="sxs-lookup"><span data-stu-id="28393-170">Yes</span></span> | |
| <span data-ttu-id="28393-171">Cache Redis</span><span class="sxs-lookup"><span data-stu-id="28393-171">Redis Cache</span></span>             |     | <span data-ttu-id="28393-172">Sim</span><span class="sxs-lookup"><span data-stu-id="28393-172">Yes</span></span> |
| <span data-ttu-id="28393-173">Serviços de pesquisa</span><span class="sxs-lookup"><span data-stu-id="28393-173">Search services</span></span>         | <span data-ttu-id="28393-174">Sim</span><span class="sxs-lookup"><span data-stu-id="28393-174">Yes</span></span> | <span data-ttu-id="28393-175">Sim</span><span class="sxs-lookup"><span data-stu-id="28393-175">Yes</span></span> |
| <span data-ttu-id="28393-176">Namespace do Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="28393-176">Service Bus namespace</span></span>   |     | <span data-ttu-id="28393-177">Sim</span><span class="sxs-lookup"><span data-stu-id="28393-177">Yes</span></span> |
| <span data-ttu-id="28393-178">SQL (v12)</span><span class="sxs-lookup"><span data-stu-id="28393-178">SQL (v12)</span></span>               |     | <span data-ttu-id="28393-179">Sim</span><span class="sxs-lookup"><span data-stu-id="28393-179">Yes</span></span> |
| <span data-ttu-id="28393-180">Sites</span><span class="sxs-lookup"><span data-stu-id="28393-180">Web Sites</span></span>               |     | <span data-ttu-id="28393-181">Sim</span><span class="sxs-lookup"><span data-stu-id="28393-181">Yes</span></span> |
| <span data-ttu-id="28393-182">Farms do servidor Web</span><span class="sxs-lookup"><span data-stu-id="28393-182">Web Server farms</span></span>        |     | <span data-ttu-id="28393-183">Sim</span><span class="sxs-lookup"><span data-stu-id="28393-183">Yes</span></span> |

<span data-ttu-id="28393-184">Para obter detalhes de saudação de métricas disponíveis Olá, consulte muito[suporte para métricas com o Azure Monitor](../monitoring-and-diagnostics/monitoring-supported-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="28393-184">For hello details of hello available metrics, refer too[supported metrics with Azure Monitor](../monitoring-and-diagnostics/monitoring-supported-metrics.md).</span></span>

<span data-ttu-id="28393-185">Para obter detalhes de saudação dos logs disponíveis hello, consulte muito[serviços e esquema com suporte para logs de diagnóstico](../monitoring-and-diagnostics/monitoring-diagnostic-logs-schema.md).</span><span class="sxs-lookup"><span data-stu-id="28393-185">For hello details of hello available logs, refer too[supported services and schema for diagnostic logs](../monitoring-and-diagnostics/monitoring-diagnostic-logs-schema.md).</span></span>

```
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$resourceId = "/SUBSCRIPTIONS/ec11ca60-1234-491e-5678-0ea07feae25c/RESOURCEGROUPS/DEMO/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/DEMO" 

Set-AzureRmDiagnosticSetting -ResourceId $resourceId -WorkspaceId $workspaceId -Enabled $true
```

<span data-ttu-id="28393-186">Você também pode usar o hello anterior cmdlet toocollect registros de recursos que estão em assinaturas diferentes.</span><span class="sxs-lookup"><span data-stu-id="28393-186">You can also use hello preceding cmdlet toocollect logs from resources that are in different subscriptions.</span></span> <span data-ttu-id="28393-187">Olá cmdlet é capaz de toowork em assinaturas desde que você está fornecendo o id de saudação de ambos os recursos de saudação criar logs e logs de saudação do espaço de trabalho Olá são enviados para.</span><span class="sxs-lookup"><span data-stu-id="28393-187">hello cmdlet is able toowork across subscriptions since you are providing hello id of both hello resource creating logs and hello workspace hello logs are sent to.</span></span>


## <a name="configuring-log-analytics-tooindex-azure-diagnostics-from-storage"></a><span data-ttu-id="28393-188">Configurando a análise de Log tooindex diagnóstico do armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="28393-188">Configuring Log Analytics tooindex Azure diagnostics from storage</span></span>
<span data-ttu-id="28393-189">dados de log toocollect de dentro de uma instância em execução de um serviço de nuvem clássico ou um cluster de malha do serviço, você precisa de toofirst gravação Olá dados tooAzure armazenamento.</span><span class="sxs-lookup"><span data-stu-id="28393-189">toocollect log data from within a running instance of a classic cloud service or a service fabric cluster, you need toofirst write hello data tooAzure storage.</span></span> <span data-ttu-id="28393-190">Análise de log, em seguida, é configurado toocollect logs de Olá Olá da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="28393-190">Log Analytics is then configured toocollect hello logs from hello storage account.</span></span> <span data-ttu-id="28393-191">Os recursos com suporte incluem:</span><span class="sxs-lookup"><span data-stu-id="28393-191">Supported resources include:</span></span>

* <span data-ttu-id="28393-192">Serviços de nuvem clássicos (funções de web e de trabalho)</span><span class="sxs-lookup"><span data-stu-id="28393-192">Classic cloud services (web and worker roles)</span></span>
* <span data-ttu-id="28393-193">Clusters do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="28393-193">Service fabric clusters</span></span>

<span data-ttu-id="28393-194">Olá mostrado no exemplo a seguir como a:</span><span class="sxs-lookup"><span data-stu-id="28393-194">hello following example shows how to:</span></span>

1. <span data-ttu-id="28393-195">Olá listar contas de armazenamento existentes e os locais que indexa dados de análise de Log</span><span class="sxs-lookup"><span data-stu-id="28393-195">List hello existing storage accounts and locations that Log Analytics will index data from</span></span>
2. <span data-ttu-id="28393-196">Criar um tooread de configuração de conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="28393-196">Create a configuration tooread from a storage account</span></span>
3. <span data-ttu-id="28393-197">Atualizar Olá recém-criada em dados de configuração de tooindex de locais adicionais</span><span class="sxs-lookup"><span data-stu-id="28393-197">Update hello newly created configuration tooindex data from additional locations</span></span>
4. <span data-ttu-id="28393-198">Excluir configuração Olá recém-criado</span><span class="sxs-lookup"><span data-stu-id="28393-198">Delete hello newly created configuration</span></span>

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

<span data-ttu-id="28393-199">Você também pode usar o hello anterior logs de toocollect do script de contas de armazenamento em diferentes assinaturas.</span><span class="sxs-lookup"><span data-stu-id="28393-199">You can also use hello preceding script toocollect logs from storage accounts in different subscriptions.</span></span> <span data-ttu-id="28393-200">script Hello é capaz de toowork em assinaturas desde que você está fornecendo a id de recurso de conta de armazenamento hello e uma chave de acesso correspondente.</span><span class="sxs-lookup"><span data-stu-id="28393-200">hello script is able toowork across subscriptions since you are providing hello storage account resource id and a corresponding access key.</span></span> <span data-ttu-id="28393-201">Quando você alterar a chave de acesso Olá, é necessário tooupdate Olá insight toohave Olá nova chave de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="28393-201">When you change hello access key, you need tooupdate hello storage insight toohave hello new key.</span></span>


## <a name="next-steps"></a><span data-ttu-id="28393-202">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="28393-202">Next steps</span></span>
* <span data-ttu-id="28393-203">[Examinar cmdlets do PowerShell do Log Analytics](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) para obter informações adicionais sobre como usar o PowerShell para a configuração do Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="28393-203">[Review Log Analytics PowerShell cmdlets](https://msdn.microsoft.com/library/mt188224\(v=azure.300\).aspx) for additional information on using PowerShell for configuration of Log Analytics.</span></span>

