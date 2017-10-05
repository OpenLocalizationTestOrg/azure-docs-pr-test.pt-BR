---
title: Usando o PowerShell para instalar o Application Insights no Azure | Microsoft Docs
description: "Automatize a configuração do Diagnóstico do Azure para redirecionar para o Application Insights."
services: application-insights
documentationcenter: .net
author: sbtron
manager: carmonm
ms.assetid: 4ac803a8-f424-4c0c-b18f-4b9c189a64a5
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/17/2015
ms.author: bwren
ms.openlocfilehash: 3b6da89cc33cda713b483a2af3cbb493a03d6bec
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="using-powershell-to-set-up-application-insights-for-an-azure-web-app"></a><span data-ttu-id="dcf33-103">Usando o PowerShell para configurar o Application Insights para um aplicativo Web do Azure</span><span class="sxs-lookup"><span data-stu-id="dcf33-103">Using PowerShell to set up Application Insights for an Azure web app</span></span>
<span data-ttu-id="dcf33-104">O [Microsoft Azure](https://azure.com) pode ser [configurado para enviar o Diagnóstico do Azure](app-insights-azure-diagnostics.md) para o [Application Insights do Azure](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="dcf33-104">[Microsoft Azure](https://azure.com) can be [configured to send Azure Diagnostics](app-insights-azure-diagnostics.md) to [Azure Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="dcf33-105">O diagnóstico está relacionado aos Serviços de Nuvem do Azure e às VMs do Azure.</span><span class="sxs-lookup"><span data-stu-id="dcf33-105">The diagnostics relate to Azure Cloud Services and Azure VMs.</span></span> <span data-ttu-id="dcf33-106">Eles complementam a telemetria que você envia de um aplicativo usando o SDK do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="dcf33-106">They complement the telemetry that you send from within the app using the Application Insights SDK.</span></span> <span data-ttu-id="dcf33-107">Como parte do processo de automatização da criação de novos recursos no Azure, você poderá configurar o diagnóstico usando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="dcf33-107">As part of automating the process of creating new resources in Azure, you can configure diagnostics using PowerShell.</span></span>

## <a name="azure-template"></a><span data-ttu-id="dcf33-108">Modelo do Azure</span><span class="sxs-lookup"><span data-stu-id="dcf33-108">Azure template</span></span>
<span data-ttu-id="dcf33-109">Se o aplicativo Web estiver no Azure e se você criar os recursos usando um modelo do Azure Resource Manager, poderá configurar o Application Insights adicionando isto ao nó de recursos:</span><span class="sxs-lookup"><span data-stu-id="dcf33-109">If the web app is in Azure and you create your resources using an Azure Resource Manager template, you can configure Application Insights by adding this to the resources node:</span></span>

    {
      resources: [
        /* Create Application Insights resource */
        {
          "apiVersion": "2015-05-01",
          "type": "microsoft.insights/components",
          "name": "nameOfAIAppResource",
          "location": "centralus",
          "kind": "web",
          "properties": { "ApplicationId": "nameOfAIAppResource" },
          "dependsOn": [
            "[concat('Microsoft.Web/sites/', myWebAppName)]"
          ]
        }
       ]
     } 

* <span data-ttu-id="dcf33-110">`nameOfAIAppResource` - um nome para o recurso do Application Insights</span><span class="sxs-lookup"><span data-stu-id="dcf33-110">`nameOfAIAppResource` - a name for the Application Insights resource</span></span>
* <span data-ttu-id="dcf33-111">`myWebAppName` - a id do aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="dcf33-111">`myWebAppName` - the id of the web app</span></span>

## <a name="enable-diagnostics-extension-as-part-of-deploying-a-cloud-service"></a><span data-ttu-id="dcf33-112">Habilitar a extensão de diagnóstico como parte da implantação de um Serviço de Nuvem</span><span class="sxs-lookup"><span data-stu-id="dcf33-112">Enable diagnostics extension as part of deploying a Cloud Service</span></span>
<span data-ttu-id="dcf33-113">O cmdlet `New-AzureDeployment` tem um parâmetro `ExtensionConfiguration`, que usa uma matriz de configurações de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="dcf33-113">The `New-AzureDeployment` cmdlet has a parameter `ExtensionConfiguration`, which takes an array of diagnostics configurations.</span></span> <span data-ttu-id="dcf33-114">Elas podem ser criadas com o cmdlet `New-AzureServiceDiagnosticsExtensionConfig` .</span><span class="sxs-lookup"><span data-stu-id="dcf33-114">These can be created using the `New-AzureServiceDiagnosticsExtensionConfig` cmdlet.</span></span> <span data-ttu-id="dcf33-115">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="dcf33-115">For example:</span></span>

```ps

    $service_package = "CloudService.cspkg"
    $service_config = "ServiceConfiguration.Cloud.cscfg"
    $diagnostics_storagename = "myservicediagnostics"
    $webrole_diagconfigpath = "MyService.WebRole.PubConfig.xml" 
    $workerrole_diagconfigpath = "MyService.WorkerRole.PubConfig.xml"

    $primary_storagekey = (Get-AzureStorageKey `
     -StorageAccountName "$diagnostics_storagename").Primary
    $storage_context = New-AzureStorageContext `
       -StorageAccountName $diagnostics_storagename `
       -StorageAccountKey $primary_storagekey

    $webrole_diagconfig = `
     New-AzureServiceDiagnosticsExtensionConfig `
      -Role "WebRole" -Storage_context $storageContext `
      -DiagnosticsConfigurationPath $webrole_diagconfigpath
    $workerrole_diagconfig = `
     New-AzureServiceDiagnosticsExtensionConfig `
      -Role "WorkerRole" `
      -StorageContext $storage_context `
      -DiagnosticsConfigurationPath $workerrole_diagconfigpath

    New-AzureDeployment `
      -ServiceName $service_name `
      -Slot Production `
      -Package $service_package `
      -Configuration $service_config `
      -ExtensionConfiguration @($webrole_diagconfig,$workerrole_diagconfig)

``` 

## <a name="enable-diagnostics-extension-on-an-existing-cloud-service"></a><span data-ttu-id="dcf33-116">Habilitar extensão de diagnóstico em um Serviço de Nuvem existente</span><span class="sxs-lookup"><span data-stu-id="dcf33-116">Enable diagnostics extension on an existing Cloud Service</span></span>
<span data-ttu-id="dcf33-117">Em um serviço existente, use `Set-AzureServiceDiagnosticsExtension`.</span><span class="sxs-lookup"><span data-stu-id="dcf33-117">On an existing service, use `Set-AzureServiceDiagnosticsExtension`.</span></span>

```ps

    $service_name = "MyService"
    $diagnostics_storagename = "myservicediagnostics"
    $webrole_diagconfigpath = "MyService.WebRole.PubConfig.xml" 
    $workerrole_diagconfigpath = "MyService.WorkerRole.PubConfig.xml"
    $primary_storagekey = (Get-AzureStorageKey `
         -StorageAccountName "$diagnostics_storagename").Primary
    $storage_context = New-AzureStorageContext `
        -StorageAccountName $diagnostics_storagename `
        -StorageAccountKey $primary_storagekey

    Set-AzureServiceDiagnosticsExtension `
        -StorageContext $storage_context `
        -DiagnosticsConfigurationPath $webrole_diagconfigpath `
        -ServiceName $service_name `
        -Slot Production `
        -Role "WebRole" 
    Set-AzureServiceDiagnosticsExtension `
        -StorageContext $storage_context `
        -DiagnosticsConfigurationPath $workerrole_diagconfigpath `
        -ServiceName $service_name `
        -Slot Production `
        -Role "WorkerRole"
```

## <a name="get-current-diagnostics-extension-configuration"></a><span data-ttu-id="dcf33-118">Obter a configuração de extensão de diagnóstico atual</span><span class="sxs-lookup"><span data-stu-id="dcf33-118">Get current diagnostics extension configuration</span></span>
```ps

    Get-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```


## <a name="remove-diagnostics-extension"></a><span data-ttu-id="dcf33-119">Remover extensão de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="dcf33-119">Remove diagnostics extension</span></span>
```ps

    Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```

<span data-ttu-id="dcf33-120">Se você tiver habilitado a extensão de diagnóstico usando `Set-AzureServiceDiagnosticsExtension` ou `New-AzureServiceDiagnosticsExtensionConfig` sem o parâmetro Função, poderá remover a extensão usando `Remove-AzureServiceDiagnosticsExtension` sem o parâmetro Função.</span><span class="sxs-lookup"><span data-stu-id="dcf33-120">If you enabled the diagnostics extension using either `Set-AzureServiceDiagnosticsExtension` or `New-AzureServiceDiagnosticsExtensionConfig` without the Role parameter, then you can remove the extension using `Remove-AzureServiceDiagnosticsExtension` without the Role parameter.</span></span> <span data-ttu-id="dcf33-121">Se o parâmetro Função tiver sido usado ao habilitar a extensão, ele também deverá ser usado ao removê-la.</span><span class="sxs-lookup"><span data-stu-id="dcf33-121">If the Role parameter was used when enabling the extension then it must also be used when removing the extension.</span></span>

<span data-ttu-id="dcf33-122">Para remover a extensão de diagnóstico de cada função individual:</span><span class="sxs-lookup"><span data-stu-id="dcf33-122">To remove the diagnostics extension from each individual role:</span></span>

```ps

    Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService" -Role "WebRole"
```


## <a name="see-also"></a><span data-ttu-id="dcf33-123">Consulte também</span><span class="sxs-lookup"><span data-stu-id="dcf33-123">See also</span></span>
* [<span data-ttu-id="dcf33-124">Monitorar aplicativos dos Serviços de Nuvem do Azure com o Application Insights</span><span class="sxs-lookup"><span data-stu-id="dcf33-124">Monitor Azure Cloud Services apps with Application Insights</span></span>](app-insights-cloudservices.md)
* [<span data-ttu-id="dcf33-125">Enviar o Diagnóstico do Azure para o Application Insights</span><span class="sxs-lookup"><span data-stu-id="dcf33-125">Send Azure Diagnostics to Application Insights</span></span>](app-insights-azure-diagnostics.md)
* [<span data-ttu-id="dcf33-126">Automatizar a configuração de alertas</span><span class="sxs-lookup"><span data-stu-id="dcf33-126">Automate configuring alerts</span></span>](app-insights-powershell-alerts.md)

