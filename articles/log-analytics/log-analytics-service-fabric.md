---
title: Avaliar aplicativos do Service Fabric com o Log Analytics do Azure usando o PowerShell | Microsoft Docs
description: "Você pode usar a solução do Service Fabric no Log Analytics usando o PowerShell para avaliar o risco e a integridade dos aplicativos do Service Fabric, microsserviços, nós e clusters."
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
ms.openlocfilehash: ca86787e344aa5e9e68934dee6e9e83aeb4cc340
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="assess-azure-service-fabric-applications-and-micro-services-with-powershell"></a><span data-ttu-id="6b6ca-103">Avaliar aplicativos do Service Fabric do Azure e microsserviços com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="6b6ca-103">Assess Azure Service Fabric applications and micro-services with PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6b6ca-104">Gerenciador de Recursos</span><span class="sxs-lookup"><span data-stu-id="6b6ca-104">Resource Manager</span></span>](log-analytics-service-fabric-azure-resource-manager.md)
> * [<span data-ttu-id="6b6ca-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6b6ca-105">PowerShell</span></span>](log-analytics-service-fabric.md)
>
>


![Símbolo do Service Fabric](./media/log-analytics-service-fabric/service-fabric-assessment-symbol.png)

<span data-ttu-id="6b6ca-107">Este artigo descreve como usar a solução de Service Fabric no Log Analytics para ajudar a identificar e solucionar problemas em seu cluster do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="6b6ca-107">This article describes how to use the Service Fabric solution in Log Analytics to help identify and troubleshoot issues across your Service Fabric cluster.</span></span> <span data-ttu-id="6b6ca-108">Ele ajuda você a ver como está o desempenho dos nós do Service Fabric e como seus aplicativos e serviços micro estão sendo executados.</span><span class="sxs-lookup"><span data-stu-id="6b6ca-108">It helps you see how your Service Fabric nodes are performing and how your applications and micro-services are running.</span></span>

<span data-ttu-id="6b6ca-109">A solução de Service Fabric usa dados de Diagnóstico do Azure das suas VMs do Service Fabric, coletando esses dados de suas tabelas do Azure WAD.</span><span class="sxs-lookup"><span data-stu-id="6b6ca-109">The Service Fabric solution uses Azure Diagnostics data from your Service Fabric VMs, by collecting this data from your Azure WAD tables.</span></span> <span data-ttu-id="6b6ca-110">Então, o Log Analytics lê os seguintes eventos da estrutura do Service Fabric:</span><span class="sxs-lookup"><span data-stu-id="6b6ca-110">Log Analytics then reads the following Service Fabric framework events:</span></span>

- <span data-ttu-id="6b6ca-111">**Eventos de Serviço Confiável**</span><span class="sxs-lookup"><span data-stu-id="6b6ca-111">**Reliable Service Events**</span></span>
- <span data-ttu-id="6b6ca-112">**Eventos de Ator**</span><span class="sxs-lookup"><span data-stu-id="6b6ca-112">**Actor Events**</span></span>
- <span data-ttu-id="6b6ca-113">**Eventos Operacionais**</span><span class="sxs-lookup"><span data-stu-id="6b6ca-113">**Operational Events**</span></span>
- <span data-ttu-id="6b6ca-114">**Eventos ETW personalizados**</span><span class="sxs-lookup"><span data-stu-id="6b6ca-114">**Custom ETW events**</span></span>

<span data-ttu-id="6b6ca-115">O painel de solução do Service Fabric exibe problemas importantes e eventos relevantes no seu ambiente do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="6b6ca-115">The Service Fabric solution dashboard shows you notable issues and relevant events in your Service Fabric environment.</span></span>

## <a name="installing-and-configuring-the-solution"></a><span data-ttu-id="6b6ca-116">Instalando e configurando a solução</span><span class="sxs-lookup"><span data-stu-id="6b6ca-116">Installing and configuring the solution</span></span>
<span data-ttu-id="6b6ca-117">Siga estas três etapas fáceis para instalar e configurar a solução:</span><span class="sxs-lookup"><span data-stu-id="6b6ca-117">Follow these three easy steps to install and configure the solution:</span></span>

1. <span data-ttu-id="6b6ca-118">Associe a assinatura do Azure que você usou para criar todos os recursos de cluster, incluindo contas de armazenamento com seu espaço de trabalho.</span><span class="sxs-lookup"><span data-stu-id="6b6ca-118">Associate the Azure subscription that you used to create all cluster resources, including storage accounts, with your workspace.</span></span> <span data-ttu-id="6b6ca-119">Consulte [Introdução ao Log Analytics](log-analytics-get-started.md) para obter informações sobre como criar um espaço de trabalho do Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="6b6ca-119">See [Get started with Log Analytics](log-analytics-get-started.md) for information about creating a Log Analytics workspace.</span></span>
2. <span data-ttu-id="6b6ca-120">Configure o Log Analytics para coletar e exibir logs do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="6b6ca-120">Configure Log Analytics to collect and view Service Fabric logs.</span></span>
3. <span data-ttu-id="6b6ca-121">Habilite a solução do Service Fabric em seu espaço de trabalho.</span><span class="sxs-lookup"><span data-stu-id="6b6ca-121">Enable the Service Fabric solution in your workspace.</span></span>

## <a name="configure-log-analytics-to-collect-and-view-service-fabric-logs"></a><span data-ttu-id="6b6ca-122">Configure o Log Analytics para coletar e exibir logs do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="6b6ca-122">Configure Log Analytics to collect and view Service Fabric logs</span></span>
<span data-ttu-id="6b6ca-123">Nesta seção, você saberá como configurar o Log Analytics para recuperar os logs do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="6b6ca-123">In this section, you learn how to configure Log Analytics to retrieve Service Fabric logs.</span></span> <span data-ttu-id="6b6ca-124">Os logs permitem a você visualizar e solucionar problemas no cluster ou nos aplicativos e serviços em execução nesse cluster usando o portal do OMS.</span><span class="sxs-lookup"><span data-stu-id="6b6ca-124">The logs allow you to view, analyze, and troubleshoot issues in your cluster or in the applications and services running in that cluster, using the OMS portal.</span></span>

> [!NOTE]
> <span data-ttu-id="6b6ca-125">Configure a extensão do Diagnóstico do Azure para carregar os logs para tabelas de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="6b6ca-125">Configure the Azure Diagnostics extension to upload the logs for storage tables.</span></span> <span data-ttu-id="6b6ca-126">As tabelas devem corresponder ao que o Log Analytics está procurando.</span><span class="sxs-lookup"><span data-stu-id="6b6ca-126">The tables must match what Log Analytics looks for.</span></span> <span data-ttu-id="6b6ca-127">Para obter mais informações, consulte [Como coletar logs com o Diagnóstico do Azure](../service-fabric/service-fabric-diagnostics-how-to-setup-wad.md).</span><span class="sxs-lookup"><span data-stu-id="6b6ca-127">For more information, see [How to collect logs with Azure Diagnostics](../service-fabric/service-fabric-diagnostics-how-to-setup-wad.md).</span></span> <span data-ttu-id="6b6ca-128">Os exemplos de definições de configuração neste artigo mostrarão quais devem ser os nomes das tabelas de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="6b6ca-128">The configuration settings examples in this article show you what the names of the storage tables should be.</span></span> <span data-ttu-id="6b6ca-129">Depois que o Diagnóstico for configurado no cluster e estiver carregando os logs para uma conta de armazenamento, a próxima etapa será configurar o Log Analytics para coletar esses logs.</span><span class="sxs-lookup"><span data-stu-id="6b6ca-129">Once Diagnostics is set up on the cluster and is uploading logs to a storage account, the next step is to configure Log Analytics to collect these logs.</span></span>
>
>

<span data-ttu-id="6b6ca-130">Certifique-se de que atualizou a seção **EtwEventSourceProviderConfiguration** no arquivo **template.json** para adicionar entradas no novo EventSources antes de aplicar a atualização de configuração executando **deploy.ps1**.</span><span class="sxs-lookup"><span data-stu-id="6b6ca-130">Ensure that you update the **EtwEventSourceProviderConfiguration** section in the **template.json** file to add entries for the new EventSources before you apply the configuration update by running **deploy.ps1**.</span></span> <span data-ttu-id="6b6ca-131">A tabela de carregamento é igual a (ETWEventTable).</span><span class="sxs-lookup"><span data-stu-id="6b6ca-131">The table for upload is the same as (ETWEventTable).</span></span> <span data-ttu-id="6b6ca-132">Neste momento, o Log Analytics somente poderá ler os eventos de ETW do aplicativo a partir da tabela *WADETWEventTable*.</span><span class="sxs-lookup"><span data-stu-id="6b6ca-132">At the moment, Log Analytics can only read application ETW events from the *WADETWEventTable* table.</span></span>

<span data-ttu-id="6b6ca-133">Estas ferramentas são usadas para executar algumas das operações nesta seção:</span><span class="sxs-lookup"><span data-stu-id="6b6ca-133">The following tools are used to perform some of the operations in this section:</span></span>

* <span data-ttu-id="6b6ca-134">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="6b6ca-134">Azure PowerShell</span></span>
* [<span data-ttu-id="6b6ca-135">Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="6b6ca-135">Operations Management Suite</span></span>](http://www.microsoft.com/oms)

### <a name="configure-a-log-analytics-workspace-to-show-the-cluster-logs"></a><span data-ttu-id="6b6ca-136">Configurar um espaço de trabalho do Log Analytics para exibir os logs do cluster</span><span class="sxs-lookup"><span data-stu-id="6b6ca-136">Configure a Log Analytics workspace to show the cluster logs</span></span>

<span data-ttu-id="6b6ca-137">Depois de criar um espaço de trabalho do Log Analytics, configure o espaço de trabalho para efetuar pull logs das tabelas de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="6b6ca-137">After you create a Log Analytics workspace, configure the workspace to pull logs from the Azure storage tables.</span></span> <span data-ttu-id="6b6ca-138">Então, execute o seguinte script do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="6b6ca-138">Then, run the following PowerShell script:</span></span>

```
<#
    This script will configure an Operations Management Suite workspace (previously called an Operational Insights workspace) to read Diagnostics from an Azure Storage account.
    It will enable all supported data types (currently Service Fabric Events, ETW Events and IIS Logs).
    It supports Resource Manager storage accounts.
    If you have more than one Azure Subscription, you will be prompted for the subscription to configure.
    If you have more than one Log Analytics workspace you will be prompted for the workspace to configure.
    It will then look through your Service Fabric clusters, and configure your Log Analytics workspace to read Diagnostics from storage accounts that are connected to that cluster and have diagnostics enabled.
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
            $uiPrompt = "Enter the number corresponding to the Azure subscription you would like to work with.`n"

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
            $uiPrompt = "Enter the number corresponding to the workspace you want to configure.`n"
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
             Write-Warning ("$id No configuration found for $provider. Configure Azure diagnostics to write to $expectedTable.")
         }  
         elseif ( $table -ne $expectedTable )
         {
             Write-Warning ("$id $provider events are being written to $table instead of WAD$expectedTable. Events will not be collected by Log Analytics")
         }  
         else
         {
             Write-Verbose "$id $provider events are being written to WAD$expectedTable (Correct configuration.)"
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
         Write-Error "Unable to parse Azure Diagnostics setting for $id"
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
    $serviceFabricClusters = $allResources.Where({$_.ResourceType -eq "Microsoft.ServiceFabric/clusters"}) #pulls in all service fabric clusters in the resource
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
                                # HTTP Not Found is returned if the storage insight doesn't exist
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
                                      # If any of the tables from the table list are not already monitored, then we add them
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

<span data-ttu-id="6b6ca-139">Depois de configurar o espaço de trabalho do Log Analytics para ler as tabelas do Azure em sua conta de armazenamento, entre no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="6b6ca-139">After you've configured the Log Analytics workspace to read from the Azure tables in your storage account, log in to the Azure portal.</span></span> <span data-ttu-id="6b6ca-140">Selecione o espaço de trabalho do Log Analytics de **todos os Recursos**.</span><span class="sxs-lookup"><span data-stu-id="6b6ca-140">Select the Log Analytics workspace from **All Resources**.</span></span> <span data-ttu-id="6b6ca-141">O número de logs de conta de armazenamento conectados ao espaço de trabalho é exibido.</span><span class="sxs-lookup"><span data-stu-id="6b6ca-141">The number of storage account logs connected to the workspace is displayed.</span></span> <span data-ttu-id="6b6ca-142">Selecione o bloco **Logs de conta de armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="6b6ca-142">Select the **Storage account logs** tile.</span></span> <span data-ttu-id="6b6ca-143">Examine a lista de logs de conta de armazenamento para verificar se sua conta de armazenamento está conectada ao espaço de trabalho correto.</span><span class="sxs-lookup"><span data-stu-id="6b6ca-143">Review the list of storage account logs to verify that your storage account is connected to the correct workspace.</span></span>

![Logs de conta de armazenamento](./media/log-analytics-service-fabric/sf1.png)

## <a name="enable-the-service-fabric-solution"></a><span data-ttu-id="6b6ca-145">Habilitar a solução do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="6b6ca-145">Enable the Service Fabric solution</span></span>
<span data-ttu-id="6b6ca-146">Use o script a seguir para adicionar a solução ao seu espaço de trabalho do Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="6b6ca-146">Use the following script to add the solution to your Log Analytics workspace.</span></span> <span data-ttu-id="6b6ca-147">Execute o script no PowerShell, usando a assinatura do Azure que está associada ao espaço de trabalho do Log Analytics no qual você deseja habilitar a solução do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="6b6ca-147">Run the script in PowerShell, using the Azure subscription that is associated with the Log Analytics workspace that you want to enable the Service Fabric solution in.</span></span>

```
function Select-Subscription {
      $subscription = ""
      $allSubscriptions = Get-AzureRmSubscription
      switch ($allSubscriptions.Count) {
             0 {Write-Error "No Operations Management Suite workspaces found"}
             1 {return $allSubscriptions}
        default {
            $uiPrompt = "Enter the number corresponding to the Azure subscription you would like to work with.`n"
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
            $uiPrompt = "Enter the number corresponding to the workspace you want to configure.`n"
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

<span data-ttu-id="6b6ca-148">Depois de habilitar a solução, o bloco do Service Fabric é adicionado à sua página *Visão geral* do Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="6b6ca-148">After you enable the solution, the Service Fabric tile is added to your Log Analytics *Overview* page.</span></span> <span data-ttu-id="6b6ca-149">A página mostra uma exibição de problemas importantes, como falhas e cancelamentos de runAsync que ocorreram nas últimas 24 horas.</span><span class="sxs-lookup"><span data-stu-id="6b6ca-149">The page shows a view of notable issues such as runAsync failures and cancellations that occurred in the last 24 hours.</span></span>

![Bloco do Service Fabric](./media/log-analytics-service-fabric/sf2.png)

### <a name="view-service-fabric-events"></a><span data-ttu-id="6b6ca-151">Exibir eventos do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="6b6ca-151">View Service Fabric events</span></span>
<span data-ttu-id="6b6ca-152">Clique no bloco do **Service Fabric** para abrir o painel do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="6b6ca-152">Click the **Service Fabric** tile to open the Service Fabric dashboard.</span></span> <span data-ttu-id="6b6ca-153">O painel inclui as colunas na tabela a seguir.</span><span class="sxs-lookup"><span data-stu-id="6b6ca-153">The dashboard includes the columns in the table that follows.</span></span> <span data-ttu-id="6b6ca-154">Cada coluna lista os 10 principais eventos por contagem que correspondem aos critérios da coluna para o intervalo de tempo especificado.</span><span class="sxs-lookup"><span data-stu-id="6b6ca-154">Each column lists the top 10 events by count matching that column's criteria for the specified time range.</span></span> <span data-ttu-id="6b6ca-155">É possível executar uma pesquisa de log que fornece a lista inteira clicando em **Ver todos** no canto inferior direito de cada coluna ou clicando no cabeçalho da coluna.</span><span class="sxs-lookup"><span data-stu-id="6b6ca-155">You can run a log search that provides the entire list by clicking **See all** at the right bottom of each column, or by clicking the column header.</span></span>

| <span data-ttu-id="6b6ca-156">**Evento do Service Fabric**</span><span class="sxs-lookup"><span data-stu-id="6b6ca-156">**Service Fabric event**</span></span> | <span data-ttu-id="6b6ca-157">**description**</span><span class="sxs-lookup"><span data-stu-id="6b6ca-157">**description**</span></span> |
| --- | --- |
| <span data-ttu-id="6b6ca-158">Problemas importantes</span><span class="sxs-lookup"><span data-stu-id="6b6ca-158">Notable Issues</span></span> | <span data-ttu-id="6b6ca-159">Uma exibição de problemas como RunAsyncFailures, RunAsynCancellations e Nós com Falha.</span><span class="sxs-lookup"><span data-stu-id="6b6ca-159">Displays issues including RunAsyncFailures, RunAsynCancellations, and Node Downs.</span></span> |
| <span data-ttu-id="6b6ca-160">Eventos operacionais</span><span class="sxs-lookup"><span data-stu-id="6b6ca-160">Operational Events</span></span> | <span data-ttu-id="6b6ca-161">Eventos operacionais importantes, como a atualização de aplicativos e implantações.</span><span class="sxs-lookup"><span data-stu-id="6b6ca-161">Displays notable operational events including application upgrade and deployments.</span></span> |
| <span data-ttu-id="6b6ca-162">Eventos de serviço confiável</span><span class="sxs-lookup"><span data-stu-id="6b6ca-162">Reliable Service Events</span></span> | <span data-ttu-id="6b6ca-163">Exibe eventos de Reliable Services importantes, incluindo Runasyncinvocations.</span><span class="sxs-lookup"><span data-stu-id="6b6ca-163">Displays notable reliable service events including  Runasyncinvocations.</span></span> |
| <span data-ttu-id="6b6ca-164">Eventos de ator</span><span class="sxs-lookup"><span data-stu-id="6b6ca-164">Actor Events</span></span> | <span data-ttu-id="6b6ca-165">Exibe eventos de ator importantes gerados por seus microsserviços.</span><span class="sxs-lookup"><span data-stu-id="6b6ca-165">Displays notable actor events generated by your micro-services.</span></span> <span data-ttu-id="6b6ca-166">Os eventos incluem exceções lançadas por um método de ator, ativações e desativações de ator e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="6b6ca-166">Events include exceptions thrown by an actor method, actor activations and deactivations, and so on.</span></span> |
| <span data-ttu-id="6b6ca-167">Eventos de aplicativo</span><span class="sxs-lookup"><span data-stu-id="6b6ca-167">Application Events</span></span> | <span data-ttu-id="6b6ca-168">Exibe todos os eventos de ETW personalizados gerados por seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="6b6ca-168">Displays all custom ETW events generated by your applications.</span></span> |

![Painel do Service Fabric](./media/log-analytics-service-fabric/sf3.png)

![Painel do Service Fabric](./media/log-analytics-service-fabric/sf4.png)

<span data-ttu-id="6b6ca-171">A tabela a seguir mostra os métodos de coleta de dados e outros detalhes sobre como os dados são coletados para o Service Fabric:</span><span class="sxs-lookup"><span data-stu-id="6b6ca-171">The following table shows data collection methods and other details about how data is collected for Service Fabric:</span></span>

| <span data-ttu-id="6b6ca-172">plataforma</span><span class="sxs-lookup"><span data-stu-id="6b6ca-172">platform</span></span> | <span data-ttu-id="6b6ca-173">Agente direto</span><span class="sxs-lookup"><span data-stu-id="6b6ca-173">Direct Agent</span></span> | <span data-ttu-id="6b6ca-174">Agente do Operations Manager</span><span class="sxs-lookup"><span data-stu-id="6b6ca-174">Operations Manager agent</span></span> | <span data-ttu-id="6b6ca-175">Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="6b6ca-175">Azure Storage</span></span> | <span data-ttu-id="6b6ca-176">Operations Manager necessário?</span><span class="sxs-lookup"><span data-stu-id="6b6ca-176">Operations Manager required?</span></span> | <span data-ttu-id="6b6ca-177">Dados de agente do Operations Manager enviados por meio do grupo de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="6b6ca-177">Operations Manager agent data sent via management group</span></span> | <span data-ttu-id="6b6ca-178">frequência de coleta</span><span class="sxs-lookup"><span data-stu-id="6b6ca-178">collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="6b6ca-179">Windows</span><span class="sxs-lookup"><span data-stu-id="6b6ca-179">Windows</span></span> |  |  | <span data-ttu-id="6b6ca-180">&#8226;</span><span class="sxs-lookup"><span data-stu-id="6b6ca-180">&#8226;</span></span> |  |  |<span data-ttu-id="6b6ca-181">10 minutos</span><span class="sxs-lookup"><span data-stu-id="6b6ca-181">10 minutes</span></span> |

> [!NOTE]
> <span data-ttu-id="6b6ca-182">Altere o escopo de eventos com **Dados com base nos últimos sete dias** na parte superior do painel.</span><span class="sxs-lookup"><span data-stu-id="6b6ca-182">Change the scope of events with **Data based on last seven days** at the top of the dashboard.</span></span> <span data-ttu-id="6b6ca-183">Você também pode mostrar os eventos gerados nos últimos sete dias, no último dia ou nas últimas seis horas.</span><span class="sxs-lookup"><span data-stu-id="6b6ca-183">You can also show events generated within the last seven days, one day, or six hours.</span></span> <span data-ttu-id="6b6ca-184">Ou você pode selecionar **Personalizado** e especificar um intervalo de datas personalizado.</span><span class="sxs-lookup"><span data-stu-id="6b6ca-184">Or, you can select **Custom** to specify a custom date range.</span></span>
>
>

## <a name="troubleshoot-your-service-fabric-and-log-analytics-configuration"></a><span data-ttu-id="6b6ca-185">Solucionar problemas de configuração do Service Fabric e do Log Analytics</span><span class="sxs-lookup"><span data-stu-id="6b6ca-185">Troubleshoot your Service Fabric and Log Analytics configuration</span></span>
<span data-ttu-id="6b6ca-186">Se você precisa verificar sua configuração do Log Analytics porque não consegue visualizar os dados do evento no Log Analytics, utilize o script a seguir.</span><span class="sxs-lookup"><span data-stu-id="6b6ca-186">If you need to verify your Log Analytics configuration because you are unable to view event data in Log Analytics, use the following script.</span></span> <span data-ttu-id="6b6ca-187">Ele executa as seguintes ações:</span><span class="sxs-lookup"><span data-stu-id="6b6ca-187">It performs the following actions:</span></span>

1. <span data-ttu-id="6b6ca-188">Lê a configuração de diagnóstico do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="6b6ca-188">Reads your Service Fabric diagnostics configuration</span></span>
2. <span data-ttu-id="6b6ca-189">Verifica se há dados gravados nas tabelas</span><span class="sxs-lookup"><span data-stu-id="6b6ca-189">Checks for data written into the tables</span></span>
3. <span data-ttu-id="6b6ca-190">Verificar se o Log Analytics está configurado para ler as tabelas</span><span class="sxs-lookup"><span data-stu-id="6b6ca-190">Verifies that Log Analytics is configured to read from the tables</span></span>

```
<#
    Verify Service Fabric and Log Analytics configuration
    1. Read Service Fabric diagnostics configuration
    2. Check for data being written into the tables
    3. Verify Log Analytics is configured to read from the tables

    Supported tables:
    WADServiceFabricReliableActorEventTable
    WADServiceFabricReliableServiceEventTable
    WADServiceFabricSystemEventTable
    WADETWEventTable

    Script will write a warning for every misconfiguration detected
    To see items that are correctly configured set $VerbosePreference="Continue"
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
    Check if OMS Log Analytics is configured to index service fabric events from the specified table
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
            Write-Verbose ("OMS Log Analytics workspace " + $workspace.Name + " is configured to index service fabric actor, service and operational events from " + $storageAccount.Name)
        } else
        {
            Write-Warning ("OMS Log Analytics workspace " + $workspace.Name + " is not configured to index service fabric actor, service and operational events from " + $storageAccount.Name)
        }
        if ("WADETWEventTable" -in $currentStorageAccountInsight.Tables)
        {
            Write-Verbose ("OMS Log Analytics workspace " + $workspace.Name + " is configured to index service fabric application events from " + $storageAccount.Name)
        } else
        {
            Write-Warning ("OMS Log Analytics workspace " + $workspace.Name + " is not configured to index service fabric application events from " + $storageAccount.Name)
        }
    } else
    {
        Write-Warning ("OMS Log Analytics workspace " + $workspace.Name + "is not configured to read service fabric events from " + $storageAccount.Name)
    }    
}

<#
    Check Azure table storage to confirm there is recent data written by Service Fabric
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
                Write-Verbose ("Data was written to $table in " + $storageAccount.ResourceName + "after $recently")
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
    Check if ETW provider is configured to log events to the expected table storage
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
            Write-Warning ("$id No configuration found for $provider. Configure Azure diagnostics to write to $expectedTable.")
        }
        elseif ( $table -ne $expectedTable )
        {
            Write-Warning ("$id $provider events are being written to $table instead of WAD$expectedTable. Events will not be collected by Log Analytics")
        }
        else
        {
            Write-Verbose "$id $provider events are being written to WAD$expectedTable (Correct configuration.)"
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
        Write-Error "Unable to parse Azure Diagnostics setting for $id"
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
    Write-Error ("Unable to find Log Analytics Workspace " + $workspaceName)
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


## <a name="next-steps"></a><span data-ttu-id="6b6ca-191">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6b6ca-191">Next steps</span></span>
* <span data-ttu-id="6b6ca-192">Use [Pesquisas de log no Log Analytics](log-analytics-log-searches.md) para exibir dados detalhados dos eventos do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="6b6ca-192">Use [Log Searches in Log Analytics](log-analytics-log-searches.md) to view detailed Service Fabric event data.</span></span>
