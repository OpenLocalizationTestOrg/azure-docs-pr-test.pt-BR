---
title: "aaaAssess aplicativos do Service Fabric com análise de logs do Azure usando o PowerShell | Microsoft Docs"
description: "Você pode usar a solução de malha do serviço de saudação na análise de Log com o risco de saudação do PowerShell tooassess e a integridade de aplicativos do Service Fabric, microsserviços, nós e clusters."
services: log-analytics
documentationcenter: 
author: niniikhena
manager: jochan
editor: 
ms.assetid: 2047b3fa-96b1-4230-af5d-a4c331d973ce
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2017
ms.author: nini
ms.openlocfilehash: 3f6d6c0df02d6d453b77e50b75b64bf7eb73bbbf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="assess-azure-service-fabric-applications-and-micro-services-with-powershell"></a><span data-ttu-id="b70f3-103">Avaliar aplicativos do Service Fabric do Azure e microsserviços com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="b70f3-103">Assess Azure Service Fabric applications and micro-services with PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b70f3-104">Gerenciador de Recursos</span><span class="sxs-lookup"><span data-stu-id="b70f3-104">Resource Manager</span></span>](log-analytics-service-fabric-azure-resource-manager.md)
> * [<span data-ttu-id="b70f3-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b70f3-105">PowerShell</span></span>](log-analytics-service-fabric.md)
>
>


![Símbolo do Service Fabric](./media/log-analytics-service-fabric/service-fabric-assessment-symbol.png)

<span data-ttu-id="b70f3-107">Este artigo descreve como toouse Olá solução Service Fabric na análise de Log toohelp identificar e solucionar problemas em seu cluster do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b70f3-107">This article describes how toouse hello Service Fabric solution in Log Analytics toohelp identify and troubleshoot issues across your Service Fabric cluster.</span></span> <span data-ttu-id="b70f3-108">Ele ajuda você a ver como está o desempenho dos nós do Service Fabric e como seus aplicativos e serviços micro estão sendo executados.</span><span class="sxs-lookup"><span data-stu-id="b70f3-108">It helps you see how your Service Fabric nodes are performing and how your applications and micro-services are running.</span></span>

<span data-ttu-id="b70f3-109">Olá solução Service Fabric usa dados de diagnóstico do Azure de suas VMs de malha do serviço, coletando dados de tabelas do Azure WAD.</span><span class="sxs-lookup"><span data-stu-id="b70f3-109">hello Service Fabric solution uses Azure Diagnostics data from your Service Fabric VMs, by collecting this data from your Azure WAD tables.</span></span> <span data-ttu-id="b70f3-110">Análise de log lê Olá eventos do Service Fabric estrutura a seguir:</span><span class="sxs-lookup"><span data-stu-id="b70f3-110">Log Analytics then reads hello following Service Fabric framework events:</span></span>

- <span data-ttu-id="b70f3-111">**Eventos de Serviço Confiável**</span><span class="sxs-lookup"><span data-stu-id="b70f3-111">**Reliable Service Events**</span></span>
- <span data-ttu-id="b70f3-112">**Eventos de Ator**</span><span class="sxs-lookup"><span data-stu-id="b70f3-112">**Actor Events**</span></span>
- <span data-ttu-id="b70f3-113">**Eventos Operacionais**</span><span class="sxs-lookup"><span data-stu-id="b70f3-113">**Operational Events**</span></span>
- <span data-ttu-id="b70f3-114">**Eventos ETW personalizados**</span><span class="sxs-lookup"><span data-stu-id="b70f3-114">**Custom ETW events**</span></span>

<span data-ttu-id="b70f3-115">Painel de solução do Service Fabric Olá mostra problemas importantes e eventos relevantes em seu ambiente do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b70f3-115">hello Service Fabric solution dashboard shows you notable issues and relevant events in your Service Fabric environment.</span></span>

## <a name="installing-and-configuring-hello-solution"></a><span data-ttu-id="b70f3-116">Instalando e configurando a solução Olá</span><span class="sxs-lookup"><span data-stu-id="b70f3-116">Installing and configuring hello solution</span></span>
<span data-ttu-id="b70f3-117">Siga estas três etapas simples tooinstall e configurar a solução de saudação:</span><span class="sxs-lookup"><span data-stu-id="b70f3-117">Follow these three easy steps tooinstall and configure hello solution:</span></span>

1. <span data-ttu-id="b70f3-118">Associe Olá assinatura do Azure que você usou toocreate todos os recursos de cluster, incluindo contas de armazenamento com seu espaço de trabalho.</span><span class="sxs-lookup"><span data-stu-id="b70f3-118">Associate hello Azure subscription that you used toocreate all cluster resources, including storage accounts, with your workspace.</span></span> <span data-ttu-id="b70f3-119">Consulte [Introdução ao Log Analytics](log-analytics-get-started.md) para obter informações sobre como criar um espaço de trabalho do Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="b70f3-119">See [Get started with Log Analytics](log-analytics-get-started.md) for information about creating a Log Analytics workspace.</span></span>
2. <span data-ttu-id="b70f3-120">Configurar toocollect de análise de Log e exibir logs do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b70f3-120">Configure Log Analytics toocollect and view Service Fabric logs.</span></span>
3. <span data-ttu-id="b70f3-121">Habilite a solução do Service Fabric Olá no espaço de trabalho.</span><span class="sxs-lookup"><span data-stu-id="b70f3-121">Enable hello Service Fabric solution in your workspace.</span></span>

## <a name="configure-log-analytics-toocollect-and-view-service-fabric-logs"></a><span data-ttu-id="b70f3-122">Configurar toocollect de análise de Log e exibir logs do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="b70f3-122">Configure Log Analytics toocollect and view Service Fabric logs</span></span>
<span data-ttu-id="b70f3-123">Nesta seção, você aprenderá como logs de análise de Log de tooconfigure tooretrieve Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b70f3-123">In this section, you learn how tooconfigure Log Analytics tooretrieve Service Fabric logs.</span></span> <span data-ttu-id="b70f3-124">Olá logs permitem tooview, analisar e solucionar problemas no seu cluster ou em aplicativos hello e serviços em execução naquele cluster, usando o portal do OMS hello.</span><span class="sxs-lookup"><span data-stu-id="b70f3-124">hello logs allow you tooview, analyze, and troubleshoot issues in your cluster or in hello applications and services running in that cluster, using hello OMS portal.</span></span>

> [!NOTE]
> <span data-ttu-id="b70f3-125">Configure o diagnóstico do Azure Olá extensão logs de saudação tooupload para tabelas de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="b70f3-125">Configure hello Azure Diagnostics extension tooupload hello logs for storage tables.</span></span> <span data-ttu-id="b70f3-126">tabelas de saudação devem corresponder a aparência de análise de Log.</span><span class="sxs-lookup"><span data-stu-id="b70f3-126">hello tables must match what Log Analytics looks for.</span></span> <span data-ttu-id="b70f3-127">Para obter mais informações, consulte [como toocollect registra com o Azure Diagnostics](../service-fabric/service-fabric-diagnostics-how-to-setup-wad.md).</span><span class="sxs-lookup"><span data-stu-id="b70f3-127">For more information, see [How toocollect logs with Azure Diagnostics](../service-fabric/service-fabric-diagnostics-how-to-setup-wad.md).</span></span> <span data-ttu-id="b70f3-128">exemplos de definições de configuração de saudação neste artigo mostram quais nomes de saudação do armazenamento Olá as tabelas devem estar.</span><span class="sxs-lookup"><span data-stu-id="b70f3-128">hello configuration settings examples in this article show you what hello names of hello storage tables should be.</span></span> <span data-ttu-id="b70f3-129">Depois de diagnóstico está configurado no cluster hello e está carregando a conta de armazenamento tooa logs, Olá próxima etapa é toocollect de análise de Log tooconfigure esses logs.</span><span class="sxs-lookup"><span data-stu-id="b70f3-129">Once Diagnostics is set up on hello cluster and is uploading logs tooa storage account, hello next step is tooconfigure Log Analytics toocollect these logs.</span></span>
>
>

<span data-ttu-id="b70f3-130">Certifique-se de que você atualize Olá **EtwEventSourceProviderConfiguration** seção Olá **template.json** tooadd entradas para Olá atualizar EventSources novo antes de aplicar a configuração de saudação do arquivo executando **deploy.ps1**.</span><span class="sxs-lookup"><span data-stu-id="b70f3-130">Ensure that you update hello **EtwEventSourceProviderConfiguration** section in hello **template.json** file tooadd entries for hello new EventSources before you apply hello configuration update by running **deploy.ps1**.</span></span> <span data-ttu-id="b70f3-131">tabela de saudação para carregamento é Olá mesmo o como (ETWEventTable).</span><span class="sxs-lookup"><span data-stu-id="b70f3-131">hello table for upload is hello same as (ETWEventTable).</span></span> <span data-ttu-id="b70f3-132">No momento Olá, análise de Log pode somente ler eventos ETW de saudação *WADETWEventTable* tabela.</span><span class="sxs-lookup"><span data-stu-id="b70f3-132">At hello moment, Log Analytics can only read application ETW events from hello *WADETWEventTable* table.</span></span>

<span data-ttu-id="b70f3-133">Olá, ferramentas a seguir são usada tooperform algumas das operações de saudação nesta seção:</span><span class="sxs-lookup"><span data-stu-id="b70f3-133">hello following tools are used tooperform some of hello operations in this section:</span></span>

* <span data-ttu-id="b70f3-134">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b70f3-134">Azure PowerShell</span></span>
* [<span data-ttu-id="b70f3-135">Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="b70f3-135">Operations Management Suite</span></span>](http://www.microsoft.com/oms)

### <a name="configure-a-log-analytics-workspace-tooshow-hello-cluster-logs"></a><span data-ttu-id="b70f3-136">Configurar logs de cluster uma análise de Log espaço de trabalho tooshow Olá</span><span class="sxs-lookup"><span data-stu-id="b70f3-136">Configure a Log Analytics workspace tooshow hello cluster logs</span></span>

<span data-ttu-id="b70f3-137">Depois de criar um espaço de trabalho de análise de Log, configure logs de toopull de espaço de trabalho de saudação de tabelas de armazenamento do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="b70f3-137">After you create a Log Analytics workspace, configure hello workspace toopull logs from hello Azure storage tables.</span></span> <span data-ttu-id="b70f3-138">Em seguida, execute Olá script do PowerShell a seguir:</span><span class="sxs-lookup"><span data-stu-id="b70f3-138">Then, run hello following PowerShell script:</span></span>

```
<#
    This script will configure an Operations Management Suite workspace (previously called an Operational Insights workspace) tooread Diagnostics from an Azure Storage account.
    It will enable all supported data types (currently Service Fabric Events, ETW Events and IIS Logs).
    It supports Resource Manager storage accounts.
    If you have more than one Azure Subscription, you will be prompted for hello subscription tooconfigure.
    If you have more than one Log Analytics workspace you will be prompted for hello workspace tooconfigure.
    It will then look through your Service Fabric clusters, and configure your Log Analytics workspace tooread Diagnostics from storage accounts that are connected toothat cluster and have diagnostics enabled.
#>

try
{
    Get-AzureRMContext
}
catch [System.Management.Automation.PSInvalidOperationException]
{
    Add-AzureRmAccount
}

$validTables = "WADServiceFabric*EventTable", "WADETWEventTable"
function Select-Subscription {
      $subscription = ""
      $allSubscriptions = Get-AzureRmSubscription
      switch ($allSubscriptions.Count) {
             0 {Write-Error "No Operations Management Suite workspaces found"}
             1 {return $allSubscriptions}
        default {
            $uiPrompt = "Enter hello number corresponding toohello Azure subscription you would like toowork with.`n"

            $count = 1
            foreach ($subscription in $allSubscriptions) {
                $uiPrompt += "$count. " + $subscription.Name + " (" + $subscription.Id + ")`n"
                $count++
            }
            $answer = (Read-Host -Prompt $uiPrompt) - 1
            $subscription = $allSubscriptions[$answer]
             Write-Host $subscription.Id
        }  
    }
    return $subscription
}

function Select-Workspace {
    $workspace = ""
    $allWorkspaces = Get-AzureRmOperationalInsightsWorkspace  

    switch ($allWorkspaces.Count) {
        0 {Write-Error "No Operations Management Suite workspaces found. `n"}
        1 {return $allWorkspaces}
        default {
            $uiPrompt = "Enter hello number corresponding toohello workspace you want tooconfigure.`n"
            $count = 1
            foreach ($workspace in $allWorkspaces) {
                $uiPrompt += "$count. " + $workspace.Name + " (" + $workspace.CustomerId + ")`n"
                $count++
            }
            $answer = (Read-Host -Prompt $uiPrompt) - 1
            $workspace = $allWorkspaces[$answer]
             Write-Host $workspace.WorkspaceName
        }  
    }
    return $workspace
}

function Check-ETWProviderLogging {
     param(
     [string]$id,
     [string]$provider,
     [string]$expectedTable,
     [string]$table
    )       
         Write-Debug ("ID: $id Provider: $provider ExpectedTable $expectedTable ActualTable $table")
         if ( ($table -eq $null) -or ($table -eq ""))  
         {
             Write-Warning ("$id No configuration found for $provider. Configure Azure diagnostics toowrite too$expectedTable.")
         }  
         elseif ( $table -ne $expectedTable )
         {
             Write-Warning ("$id $provider events are being written too$table instead of WAD$expectedTable. Events will not be collected by Log Analytics")
         }  
         else
         {
             Write-Verbose "$id $provider events are being written tooWAD$expectedTable (Correct configuration.)"
         }
 }

function Check-ServiceFabricScaleSetDiagnostics {
     param(
          [psobject]$scaleSetDiagnostics
   )
     $storageAccountsFound = @()
     Write-Verbose ("Checking " + $scaleSetDiagnostics)
     $sfReliableActorTable = $null
     $sfReliableServiceTable = $null
     $sfOperationalTable = $null

     Write-Debug $scaleSetDiagnostics
     $serviceFabricProviderList = ""
     $etwManifestProviderList = ""

     if ( $scaleSetDiagnostics.xmlCfg )  
      {
             Write-Debug ("Found XMLcfg")
             $xmlCfg = [System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($scaleSetDiagnostics.xmlCfg))
             Write-Debug $xmlCfg
             $etwProviders = Select-Xml -Content $xmlCfg -XPath "//EtwProviders"                 
             $serviceFabricProviderList = $etwProviders.Node.EtwEventSourceProviderConfiguration
             $etwManifestProviderList = $etwProviders.Node.EtwManifestProviderConfiguration
      } elseif ($scaleSetDiagnostics.WadCfg )  
     {
         Write-Debug ("Found WADcfg")
         Write-Debug $scaleSetDiagnostics.WadCfg
         $serviceFabricProviderList = $scaleSetDiagnostics.WadCfg.DiagnosticMonitorConfiguration.EtwProviders.EtwEventSourceProviderConfiguration
         $etwManifestProviderList = $scaleSetDiagnostics.WadCfg.DiagnosticMonitorConfiguration.EtwProviders.EtwManifestProviderConfiguration
     } else
     {
         Write-Error "Unable tooparse Azure Diagnostics setting for $id"
             Write-Warning ("$id does not have diagnostics enabled")
     }
     foreach ($provider in $serviceFabricProviderList)  
     {
         Write-Debug ("Event Source Provider: " + $provider.Provider + " Destination: " + $provider.DefaultEvents.eventDestination)
         if ($provider.Provider -eq "Microsoft-ServiceFabric-Actors")
         {
             $sfReliableActorTable = $provider.DefaultEvents.eventDestination  
         } elseif ($provider.Provider -eq "Microsoft-ServiceFabric-Services")  
         {  
             $sfReliableServiceTable = $provider.DefaultEvents.eventDestination  
         } else  
         {
             Check-ETWProviderLogging $id $provider.Provider "ETWEventTable" $provider.DefaultEvents.eventDestination
         }
     }
     foreach ($provider in $etwManifestProviderList)
     {
         Write-Debug ("Manifest Provider: " + $provider.Provider + " Destination: " + $provider.DefaultEvents.eventDestination)
         if ($provider.Provider -eq "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8")
         {
             $sfOperationalTable = $provider.DefaultEvents.eventDestination  
         } else  
         {
             Check-ETWProviderLogging $id $provider.Provider "ETWEventTable" $provider.DefaultEvents.eventDestination
         }
     }

     Check-ETWProviderLogging $id "Microsoft-ServiceFabric-Actors" "ServiceFabricReliableActorEventTable" $sfReliableActorTable
     Check-ETWProviderLogging $id "Microsoft-ServiceFabric-Services" "ServiceFabricReliableServiceEventTable" $sfReliableServiceTable
     Check-ETWProviderLogging $id "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8 (System events)" "ServiceFabricSystemEventTable" $sfOperationalTable

     Write-Verbose ("StorageAccount: " + $scaleSetDiagnostics.StorageAccount)
     $storageAccountsFound += ($scaleSetDiagnostics.StorageAccount)
     return ($storageAccountsFound)
 }

function Select-StorageAccount {
    $allResources = Get-AzureRmResource #pulls in all resources
    $serviceFabricClusters = $allResources.Where({$_.ResourceType -eq "Microsoft.ServiceFabric/clusters"}) #pulls in all service fabric clusters in hello resource
    $storageAccountList = @()
    foreach($cluster in $serviceFabricClusters) {
        Write-Host("Checking cluster: " + $cluster.Name)
         $scaleSet = $allResources.Where({($_.ResourceType -eq "Microsoft.Compute/virtualMachineScaleSets") -and ($_.ResourceGroupName -eq $cluster.ResourceGroupName)})

         foreach($set in $scaleSet) {
             $resource = Get-AzureRmResource -ResourceId $set.ResourceId
             $extensions = $resource.Properties.VirtualMachineProfile.ExtensionProfile.Extensions

             foreach($ext in $extensions) {
                 if ($ext.Properties.Publisher -eq "Microsoft.Azure.Diagnostics" -and $ext.Properties.Type -eq "IaaSDiagnostics") {
                     $storageAccountList += (Check-ServiceFabricScaleSetDiagnostics $ext.Properties.Settings)
                 }
             }
          }

         $storageAccountsToCheck = $allResources.Where({($_.ResourceType -eq "Microsoft.Storage/storageAccounts") -and ($_.ResourceName -in $storageAccountList)})

         if ($storageAccountsToCheck.Count -eq "0") {
                Write-Error "No storage accounts found"
           }
           else {
                    foreach ($storageAccount in $storageAccountsToCheck) {
                        Write-Host("Checking Storage Account: " + $storageAccount.Name)
                        $insightsName = $storageAccount.Name + $workspace.Name
                        $existingConfig = ""
                        try
                            {
                                $existingConfig = Get-AzureRmOperationalInsightsStorageInsight -Workspace $workspace -Name $insightsName -ErrorAction Stop
                            }
                        catch
                            {
                                # HTTP Not Found is returned if hello storage insight doesn't exist
                            }
                        if ($existingConfig) {                         
                                  [array]$Tables = $existingConfig.Tables
                                   foreach($table in $validTables) {
                                         if($Tables -notcontains $table) {
                                               $Tables += $table
                                               $dirty = $true;
                                               Write-Host "Adding Table: $table";
                                         }
                                         else {
                                               Write-Host "$table is already configured.`n";
                                             }
                                      }
                                      # If any of hello tables from hello table list are not already monitored, then we add them
                                   if($dirty -eq $true) {
                                           Set-AzureRmOperationalInsightsStorageInsight -Workspace $workspace -Name $insightsName -Tables $Tables
                                           Write-Host "Updating Storage Insight. `n"
                                    }
                                    else {
                                           Write-Host "Storage Insight already updated."
                                  }
                          }
                     else {
                            $key = (Get-AzureRmStorageAccountKey -ResourceGroupName $storageAccount.ResourceGroupName -Name $storageAccount.Name)[0].Value
                           New-AzureRmOperationalInsightsStorageInsight -Workspace $workspace -Name $insightsName -StorageAccountResourceId $storageAccount.ResourceId -StorageAccountKey $key -Tables $validTables
                            Write-Host "New Azure Storage Insight Configured. `n"
                           }
                    }
             }
      }
      return
     }

$subscription = Select-Subscription
$subscriptionId = $subscription.SubscriptionId
$subscription = Select-AzureRmSubscription -SubscriptionId $subscriptionId
$workspace = Select-Workspace
$storageAccount = Select-StorageAccount
```

<span data-ttu-id="b70f3-139">Depois que você tiver configurado o hello tooread de espaço de trabalho de análise de Log de saudação do Azure tabelas em sua conta de armazenamento, faça logon no toohello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="b70f3-139">After you've configured hello Log Analytics workspace tooread from hello Azure tables in your storage account, log in toohello Azure portal.</span></span> <span data-ttu-id="b70f3-140">Selecione o espaço de trabalho de análise de Log de saudação do **todos os recursos**.</span><span class="sxs-lookup"><span data-stu-id="b70f3-140">Select hello Log Analytics workspace from **All Resources**.</span></span> <span data-ttu-id="b70f3-141">número de saudação do espaço de trabalho toohello conectados de logs de conta de armazenamento é exibido.</span><span class="sxs-lookup"><span data-stu-id="b70f3-141">hello number of storage account logs connected toohello workspace is displayed.</span></span> <span data-ttu-id="b70f3-142">Selecione Olá **logs de conta de armazenamento** lado a lado.</span><span class="sxs-lookup"><span data-stu-id="b70f3-142">Select hello **Storage account logs** tile.</span></span> <span data-ttu-id="b70f3-143">Examine a lista de saudação do tooverify de logs de conta de armazenamento que sua conta de armazenamento é conectada toohello espaço de trabalho correto.</span><span class="sxs-lookup"><span data-stu-id="b70f3-143">Review hello list of storage account logs tooverify that your storage account is connected toohello correct workspace.</span></span>

![Logs de conta de armazenamento](./media/log-analytics-service-fabric/sf1.png)

## <a name="enable-hello-service-fabric-solution"></a><span data-ttu-id="b70f3-145">Habilitar a solução do Service Fabric Olá</span><span class="sxs-lookup"><span data-stu-id="b70f3-145">Enable hello Service Fabric solution</span></span>
<span data-ttu-id="b70f3-146">Use Olá script tooadd Olá solução tooyour análise de Log espaço de trabalho a seguir.</span><span class="sxs-lookup"><span data-stu-id="b70f3-146">Use hello following script tooadd hello solution tooyour Log Analytics workspace.</span></span> <span data-ttu-id="b70f3-147">Execute script hello no PowerShell, usando Olá assinatura do Azure que está associada ao espaço de trabalho de análise de Log de saudação que você deseja tooenable solução de malha do serviço de saudação no.</span><span class="sxs-lookup"><span data-stu-id="b70f3-147">Run hello script in PowerShell, using hello Azure subscription that is associated with hello Log Analytics workspace that you want tooenable hello Service Fabric solution in.</span></span>

```
function Select-Subscription {
      $subscription = ""
      $allSubscriptions = Get-AzureRmSubscription
      switch ($allSubscriptions.Count) {
             0 {Write-Error "No Operations Management Suite workspaces found"}
             1 {return $allSubscriptions}
        default {
            $uiPrompt = "Enter hello number corresponding toohello Azure subscription you would like toowork with.`n"
            $count = 1
            foreach ($subscription in $allSubscriptions) {
                $uiPrompt += "$count. " + $subscription.SubscriptionName + " (" + $subscription.SubscriptionId + ")`n"
                $count++
            }
            $answer = (Read-Host -Prompt $uiPrompt) - 1
            $subscription = $allSubscriptions[$answer]
             Write-Host $subscription.SubscriptionId
        }  
    }
    return $subscription
}

function Select-Workspace {
    $workspace = ""
    $allWorkspaces = Get-AzureRmOperationalInsightsWorkspace  
    switch ($allWorkspaces.Count) {
        0 {Write-Error "No Operations Management Suite workspaces found"}
        1 {return $allWorkspaces}
        default {
            $uiPrompt = "Enter hello number corresponding toohello workspace you want tooconfigure.`n"
            $count = 1
            foreach ($workspace in $allWorkspaces) {
                $uiPrompt += "$count. " + $workspace.Name + " (" + $workspace.CustomerId + ")`n"
                $count++
            }
            $answer = (Read-Host -Prompt $uiPrompt) - 1
            $workspace = $allWorkspaces[$answer]
                           Write-Host $workspace.WorkspaceName
        }  
    }
    return $workspace
}
$subscription = Select-Subscription
$subscriptionId = $subscription.Id
$subscription = Select-AzureRmSubscription -SubscriptionId $subscriptionId
$workspace = Select-Workspace
Set-AzureRmOperationalInsightsIntelligencePack -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name -IntelligencePackName "ServiceFabric" -Enabled $true
```

<span data-ttu-id="b70f3-148">Depois de habilitar a solução hello, lado a lado do Service Fabric Olá é adicionada tooyour análise de Log *visão geral* página.</span><span class="sxs-lookup"><span data-stu-id="b70f3-148">After you enable hello solution, hello Service Fabric tile is added tooyour Log Analytics *Overview* page.</span></span> <span data-ttu-id="b70f3-149">página Olá mostra uma exibição de problemas importantes, como falhas de runAsync e cancelamentos que ocorreram em Olá últimas 24 horas.</span><span class="sxs-lookup"><span data-stu-id="b70f3-149">hello page shows a view of notable issues such as runAsync failures and cancellations that occurred in hello last 24 hours.</span></span>

![Bloco do Service Fabric](./media/log-analytics-service-fabric/sf2.png)

### <a name="view-service-fabric-events"></a><span data-ttu-id="b70f3-151">Exibir eventos do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="b70f3-151">View Service Fabric events</span></span>
<span data-ttu-id="b70f3-152">Clique em Olá **Service Fabric** bloco tooopen Olá Service Fabric painel.</span><span class="sxs-lookup"><span data-stu-id="b70f3-152">Click hello **Service Fabric** tile tooopen hello Service Fabric dashboard.</span></span> <span data-ttu-id="b70f3-153">painel Olá inclui colunas de saudação na tabela de saudação que segue.</span><span class="sxs-lookup"><span data-stu-id="b70f3-153">hello dashboard includes hello columns in hello table that follows.</span></span> <span data-ttu-id="b70f3-154">Cada coluna lista top 10 eventos Olá correspondendo contagem critérios da coluna para Olá especificado intervalo de tempo.</span><span class="sxs-lookup"><span data-stu-id="b70f3-154">Each column lists hello top 10 events by count matching that column's criteria for hello specified time range.</span></span> <span data-ttu-id="b70f3-155">Você pode executar uma pesquisa de log que fornece a lista inteira de saudação clicando **ver todos os** na parte inferior direita do hello de cada coluna, ou clicando o cabeçalho da coluna hello.</span><span class="sxs-lookup"><span data-stu-id="b70f3-155">You can run a log search that provides hello entire list by clicking **See all** at hello right bottom of each column, or by clicking hello column header.</span></span>

| <span data-ttu-id="b70f3-156">**Evento do Service Fabric**</span><span class="sxs-lookup"><span data-stu-id="b70f3-156">**Service Fabric event**</span></span> | <span data-ttu-id="b70f3-157">**description**</span><span class="sxs-lookup"><span data-stu-id="b70f3-157">**description**</span></span> |
| --- | --- |
| <span data-ttu-id="b70f3-158">Problemas importantes</span><span class="sxs-lookup"><span data-stu-id="b70f3-158">Notable Issues</span></span> | <span data-ttu-id="b70f3-159">Uma exibição de problemas como RunAsyncFailures, RunAsynCancellations e Nós com Falha.</span><span class="sxs-lookup"><span data-stu-id="b70f3-159">Displays issues including RunAsyncFailures, RunAsynCancellations, and Node Downs.</span></span> |
| <span data-ttu-id="b70f3-160">Eventos operacionais</span><span class="sxs-lookup"><span data-stu-id="b70f3-160">Operational Events</span></span> | <span data-ttu-id="b70f3-161">Eventos operacionais importantes, como a atualização de aplicativos e implantações.</span><span class="sxs-lookup"><span data-stu-id="b70f3-161">Displays notable operational events including application upgrade and deployments.</span></span> |
| <span data-ttu-id="b70f3-162">Eventos de serviço confiável</span><span class="sxs-lookup"><span data-stu-id="b70f3-162">Reliable Service Events</span></span> | <span data-ttu-id="b70f3-163">Exibe eventos de Reliable Services importantes, incluindo Runasyncinvocations.</span><span class="sxs-lookup"><span data-stu-id="b70f3-163">Displays notable reliable service events including  Runasyncinvocations.</span></span> |
| <span data-ttu-id="b70f3-164">Eventos de ator</span><span class="sxs-lookup"><span data-stu-id="b70f3-164">Actor Events</span></span> | <span data-ttu-id="b70f3-165">Exibe eventos de ator importantes gerados por seus microsserviços.</span><span class="sxs-lookup"><span data-stu-id="b70f3-165">Displays notable actor events generated by your micro-services.</span></span> <span data-ttu-id="b70f3-166">Os eventos incluem exceções lançadas por um método de ator, ativações e desativações de ator e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="b70f3-166">Events include exceptions thrown by an actor method, actor activations and deactivations, and so on.</span></span> |
| <span data-ttu-id="b70f3-167">Eventos de aplicativo</span><span class="sxs-lookup"><span data-stu-id="b70f3-167">Application Events</span></span> | <span data-ttu-id="b70f3-168">Exibe todos os eventos de ETW personalizados gerados por seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="b70f3-168">Displays all custom ETW events generated by your applications.</span></span> |

![Painel do Service Fabric](./media/log-analytics-service-fabric/sf3.png)

![Painel do Service Fabric](./media/log-analytics-service-fabric/sf4.png)

<span data-ttu-id="b70f3-171">Olá tabela a seguir mostra os métodos de coleta de dados e outros detalhes sobre como os dados são coletados para a malha do serviço:</span><span class="sxs-lookup"><span data-stu-id="b70f3-171">hello following table shows data collection methods and other details about how data is collected for Service Fabric:</span></span>

| <span data-ttu-id="b70f3-172">plataforma</span><span class="sxs-lookup"><span data-stu-id="b70f3-172">platform</span></span> | <span data-ttu-id="b70f3-173">Agente direto</span><span class="sxs-lookup"><span data-stu-id="b70f3-173">Direct Agent</span></span> | <span data-ttu-id="b70f3-174">Agente do Operations Manager</span><span class="sxs-lookup"><span data-stu-id="b70f3-174">Operations Manager agent</span></span> | <span data-ttu-id="b70f3-175">Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="b70f3-175">Azure Storage</span></span> | <span data-ttu-id="b70f3-176">Operations Manager necessário?</span><span class="sxs-lookup"><span data-stu-id="b70f3-176">Operations Manager required?</span></span> | <span data-ttu-id="b70f3-177">Dados de agente do Operations Manager enviados por meio do grupo de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="b70f3-177">Operations Manager agent data sent via management group</span></span> | <span data-ttu-id="b70f3-178">frequência de coleta</span><span class="sxs-lookup"><span data-stu-id="b70f3-178">collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="b70f3-179">Windows</span><span class="sxs-lookup"><span data-stu-id="b70f3-179">Windows</span></span> |  |  | <span data-ttu-id="b70f3-180">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b70f3-180">&#8226;</span></span> |  |  |<span data-ttu-id="b70f3-181">10 minutos</span><span class="sxs-lookup"><span data-stu-id="b70f3-181">10 minutes</span></span> |

> [!NOTE]
> <span data-ttu-id="b70f3-182">Alterar o escopo de saudação de eventos com **dados com base nos últimos sete dias** na parte superior de saudação do painel de saudação.</span><span class="sxs-lookup"><span data-stu-id="b70f3-182">Change hello scope of events with **Data based on last seven days** at hello top of hello dashboard.</span></span> <span data-ttu-id="b70f3-183">Você também pode mostrar gerados no hello últimos sete dias, um dia ou seis horas.</span><span class="sxs-lookup"><span data-stu-id="b70f3-183">You can also show events generated within hello last seven days, one day, or six hours.</span></span> <span data-ttu-id="b70f3-184">Ou, você pode selecionar **personalizado** toospecify um intervalo de datas personalizado.</span><span class="sxs-lookup"><span data-stu-id="b70f3-184">Or, you can select **Custom** toospecify a custom date range.</span></span>
>
>

## <a name="troubleshoot-your-service-fabric-and-log-analytics-configuration"></a><span data-ttu-id="b70f3-185">Solucionar problemas de configuração do Service Fabric e do Log Analytics</span><span class="sxs-lookup"><span data-stu-id="b70f3-185">Troubleshoot your Service Fabric and Log Analytics configuration</span></span>
<span data-ttu-id="b70f3-186">Se você precisar tooverify sua configuração de análise de Log, porque são dados de evento de tooview não é possível em análise de Log, use Olá script a seguir.</span><span class="sxs-lookup"><span data-stu-id="b70f3-186">If you need tooverify your Log Analytics configuration because you are unable tooview event data in Log Analytics, use hello following script.</span></span> <span data-ttu-id="b70f3-187">Ele executa Olá ações a seguir:</span><span class="sxs-lookup"><span data-stu-id="b70f3-187">It performs hello following actions:</span></span>

1. <span data-ttu-id="b70f3-188">Lê a configuração de diagnóstico do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="b70f3-188">Reads your Service Fabric diagnostics configuration</span></span>
2. <span data-ttu-id="b70f3-189">Verifica se há dados gravados em tabelas de saudação</span><span class="sxs-lookup"><span data-stu-id="b70f3-189">Checks for data written into hello tables</span></span>
3. <span data-ttu-id="b70f3-190">Verifica se a análise de Log está configurado tooread das tabelas de saudação</span><span class="sxs-lookup"><span data-stu-id="b70f3-190">Verifies that Log Analytics is configured tooread from hello tables</span></span>

```
<#
    Verify Service Fabric and Log Analytics configuration
    1. Read Service Fabric diagnostics configuration
    2. Check for data being written into hello tables
    3. Verify Log Analytics is configured tooread from hello tables

    Supported tables:
    WADServiceFabricReliableActorEventTable
    WADServiceFabricReliableServiceEventTable
    WADServiceFabricSystemEventTable
    WADETWEventTable

    Script will write a warning for every misconfiguration detected
    toosee items that are correctly configured set $VerbosePreference="Continue"
#>
Param
(
    [Parameter(Mandatory=$true,
    ValueFromPipeline=$true,
    Position=1)]
    [string]$workspaceName
)

$WADtables = @("WADServiceFabricReliableActorEventTable",
               "WADServiceFabricReliableServiceEventTable",
               "WADServiceFabricSystemEventTable",
               "WADETWEventTable"
               )

<#
    Check if OMS Log Analytics is configured tooindex service fabric events from hello specified table
#>

function Check-OMSLogAnalyticsConfiguration {
    param(
    [psobject]$workspace,
    [psobject]$storageAccount,
    [string]$id
    )

    $existingInsights = Get-AzureRmOperationalInsightsStorageInsight -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name

    if ($existingInsights)
    {
        $currentStorageAccountInsight = $existingInsights.Where({$_.StorageAccountResourceId -eq $storageAccount.ResourceId})

        if ("WADServiceFabric*EventTable" -in $currentStorageAccountInsight.Tables)
        {
            Write-Verbose ("OMS Log Analytics workspace " + $workspace.Name + " is configured tooindex service fabric actor, service and operational events from " + $storageAccount.Name)
        } else
        {
            Write-Warning ("OMS Log Analytics workspace " + $workspace.Name + " is not configured tooindex service fabric actor, service and operational events from " + $storageAccount.Name)
        }
        if ("WADETWEventTable" -in $currentStorageAccountInsight.Tables)
        {
            Write-Verbose ("OMS Log Analytics workspace " + $workspace.Name + " is configured tooindex service fabric application events from " + $storageAccount.Name)
        } else
        {
            Write-Warning ("OMS Log Analytics workspace " + $workspace.Name + " is not configured tooindex service fabric application events from " + $storageAccount.Name)
        }
    } else
    {
        Write-Warning ("OMS Log Analytics workspace " + $workspace.Name + "is not configured tooread service fabric events from " + $storageAccount.Name)
    }    
}

<#
    Check Azure table storage tooconfirm there is recent data written by Service Fabric
#>

function Check-TablesForData {
    param(
    [psobject]$storageAccount
    )

    $ctx = (Get-AzureRmStorageAccount -ResourceGroupName $storageAccount.ResourceGroupName -Name $storageAccount.ResourceName).Context

    $createdTables = Get-AzureStorageTable -Context $ctx

    $recently = Get-Date -Format s ((Get-Date).AddMinutes(-20).ToUniversalTime())
    $recently = $recently + "Z"

    foreach ($table in $WADtables)
    {
        if ($table -in $createdTables.Name)
        {
            $tbl = Get-AzureStorageTable -Name $table -Context $ctx
            $query = New-Object Microsoft.WindowsAzure.Storage.Table.TableQuery
            $list = New-Object System.Collections.Generic.List[string]
            $list.Add("RowKey")
            $list.Add("ProviderName")
            $list.Add("Timestamp")
            $query.FilterString = "Timestamp gt datetime'$recently'"
            $query.SelectColumns = $list
            $query.TakeCount = 20
            $entities = $tbl.CloudTable.ExecuteQuery($query)
            Write-Debug $entities
            if ($entities.Count -gt 0)
            {
                Write-Verbose ("Data was written too$table in " + $storageAccount.ResourceName + "after $recently")
            } else
            {
                Write-Warning ("No data after $recently is in  $table in " + $storageAccount.ResourceName)
            }
        } else
        {
            Write-Warning ("$table does not exist in storage account " + $storageAccount.ResourceName)
        }
    }
}

<#
    Check if ETW provider is configured toolog events toohello expected table storage
#>
function Check-ETWProviderLogging {
    param(
    [string]$id,
    [string]$provider,
    [string]$expectedTable,
    [string]$table
    )      
        Write-Debug ("ID: $id Provider: $provider ExpectedTable $expectedTable ActualTable $table")
        if ( ($table -eq $null) -or ($table -eq ""))
        {
            Write-Warning ("$id No configuration found for $provider. Configure Azure diagnostics toowrite too$expectedTable.")
        }
        elseif ( $table -ne $expectedTable )
        {
            Write-Warning ("$id $provider events are being written too$table instead of WAD$expectedTable. Events will not be collected by Log Analytics")
        }
        else
        {
            Write-Verbose "$id $provider events are being written tooWAD$expectedTable (Correct configuration.)"
        }
}

<#
    Check Azure Diagnostics Configuration for a Service Fabric cluster
#>
function Check-ServiceFabricScaleSetDiagnostics {
    param(
    [psobject]$scaleSetDiagnostics
    )

    $storageAccountsFound = @()
    Write-Verbose ("Checking " + $scaleSetDiagnostics)
    $sfReliableActorTable = $null
    $sfReliableServiceTable = $null
    $sfOperationalTable = $null
    Write-Debug $scaleSetDiagnostics
    $serviceFabricProviderList = ""
    $etwManifestProviderList = ""

    if ( $scaleSetDiagnostics.xmlCfg )
    {
        Write-Debug ("Found XMLcfg")
        $xmlCfg = [System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($scaleSetDiagnostics.xmlCfg))
        Write-Debug $xmlCfg
        $etwProviders = Select-Xml -Content $xmlCfg -XPath "//EtwProviders"                
        $serviceFabricProviderList = $etwProviders.Node.EtwEventSourceProviderConfiguration
        $etwManifestProviderList = $etwProviders.Node.EtwManifestProviderConfiguration
    } elseif ($scaleSetDiagnostics.WadCfg )
    {
        Write-Debug ("Found WADcfg")
        Write-Debug $scaleSetDiagnostics.WadCfg
        $serviceFabricProviderList = $scaleSetDiagnostics.WadCfg.DiagnosticMonitorConfiguration.EtwProviders.EtwEventSourceProviderConfiguration
        $etwManifestProviderList = $scaleSetDiagnostics.WadCfg.DiagnosticMonitorConfiguration.EtwProviders.EtwManifestProviderConfiguration
    } else
    {
        Write-Error "Unable tooparse Azure Diagnostics setting for $id"
        Write-Warning ("$id does not have diagnostics enabled")
    }

    foreach ($provider in $serviceFabricProviderList)
    {
        Write-Debug ("Event Source Provider: " + $provider.Provider + " Destination: " + $provider.DefaultEvents.eventDestination)
        if ($provider.Provider -eq "Microsoft-ServiceFabric-Actors")
        {
            $sfReliableActorTable = $provider.DefaultEvents.eventDestination
        } elseif ($provider.Provider -eq "Microsoft-ServiceFabric-Services")
        {
            $sfReliableServiceTable = $provider.DefaultEvents.eventDestination
        } else
        {
            Check-ETWProviderLogging $id $provider.Provider "ETWEventTable" $provider.DefaultEvents.eventDestination
        }
    }
    foreach ($provider in $etwManifestProviderList)
    {
        Write-Debug ("Manifest Provider: " + $provider.Provider + " Destination: " + $provider.DefaultEvents.eventDestination)
        if ($provider.Provider -eq "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8")
        {
            $sfOperationalTable = $provider.DefaultEvents.eventDestination
        } else
        {
            Check-ETWProviderLogging $id $provider.Provider "ETWEventTable" $provider.DefaultEvents.eventDestination
        }
    }

    Check-ETWProviderLogging $id "Microsoft-ServiceFabric-Actors" "ServiceFabricReliableActorEventTable" $sfReliableActorTable
    Check-ETWProviderLogging $id "Microsoft-ServiceFabric-Services" "ServiceFabricReliableServiceEventTable" $sfReliableServiceTable
    Check-ETWProviderLogging $id "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8 (System events)" "ServiceFabricSystemEventTable" $sfOperationalTable

    Write-Verbose ("StorageAccount: " + $scaleSetDiagnostics.StorageAccount)

    $storageAccountsFound += ($scaleSetDiagnostics.StorageAccount)
    return ($storageAccountsFound)
}

# This script uses Get-AzureRmVMDiagnosticsExtension and needs a version where -Name is not a required parameter
Import-Module AzureRM.Compute -MinimumVersion 1.2.2

try
{
    Get-AzureRmContext
}
catch [System.Management.Automation.PSInvalidOperationException]
{
    Login-AzureRmAccount
}

$allResources = Get-AzureRmResource

$OMSworkspace = $allResources.Where({($_.ResourceType -eq "Microsoft.OperationalInsights/workspaces") -and ($_.ResourceName -eq $workspaceName)})

if ($OMSworkspace.Name -ne $workspaceName)
{
    Write-Error ("Unable toofind Log Analytics Workspace " + $workspaceName)
}

$serviceFabricClusters = $allResources.Where({$_.ResourceType -eq "Microsoft.ServiceFabric/clusters"})
$storageAccountList = @()
foreach($cluster in $serviceFabricClusters) {
    Write-Verbose ("Checking cluster: " + $cluster.Name)
    $scaleSet = ($allResources.Where({($_.ResourceType -eq "Microsoft.Compute/virtualMachineScaleSets") -and ($_.ResourceGroupName -eq $cluster.ResourceGroupName)}))

    foreach($set in $scaleSet) {
        $resource = Get-AzureRmResource -ResourceId $set.ResourceId
        $extensions = $resource.Properties.VirtualMachineProfile.ExtensionProfile.Extensions
        foreach($ext in $extensions) {
            if ($ext.Properties.Publisher -eq "Microsoft.Azure.Diagnostics" -and $ext.Properties.Type -eq "IaaSDiagnostics") {
                $storageAccountList += (Check-ServiceFabricScaleSetDiagnostics $ext.Properties.Settings)
            }
        }
    }
}

$storageAccountList = $storageAccountList | Sort-Object | Get-Unique
$storageAccountsToCheck = ($allResources.Where({($_.ResourceType -eq "Microsoft.Storage/storageAccounts") -and ($_.ResourceName -in $storageAccountList)}))

foreach($storageAccount in $storageAccountsToCheck)
{
    Check-TablesForData $storageAccount
    Check-OMSLogAnalyticsConfiguration $OMSworkspace $storageAccount
}
 ```


## <a name="next-steps"></a><span data-ttu-id="b70f3-191">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b70f3-191">Next steps</span></span>
* <span data-ttu-id="b70f3-192">Use [pesquisas de Log na análise de Log](log-analytics-log-searches.md) tooview obter dados de evento do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b70f3-192">Use [Log Searches in Log Analytics](log-analytics-log-searches.md) tooview detailed Service Fabric event data.</span></span>
