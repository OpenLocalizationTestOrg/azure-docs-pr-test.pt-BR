---
title: aaaUsing PowerShell toosetup Application Insights em um Azure | Microsoft Docs
description: "Automatize tooApplication toopipe de configurar o diagnóstico do Azure Insights."
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
ms.openlocfilehash: c48a5d8eb23df162522860935af876063aaa6976
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-powershell-tooset-up-application-insights-for-an-azure-web-app"></a><span data-ttu-id="6e0af-103">Usando o PowerShell tooset o Application Insights para um aplicativo web do Azure</span><span class="sxs-lookup"><span data-stu-id="6e0af-103">Using PowerShell tooset up Application Insights for an Azure web app</span></span>
<span data-ttu-id="6e0af-104">[Microsoft Azure](https://azure.com) pode ser [configurado o diagnóstico do Azure toosend](app-insights-azure-diagnostics.md) muito[Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6e0af-104">[Microsoft Azure](https://azure.com) can be [configured toosend Azure Diagnostics](app-insights-azure-diagnostics.md) too[Azure Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="6e0af-105">Olá diagnóstico relacionar tooAzure serviços de nuvem e VMs do Azure.</span><span class="sxs-lookup"><span data-stu-id="6e0af-105">hello diagnostics relate tooAzure Cloud Services and Azure VMs.</span></span> <span data-ttu-id="6e0af-106">Eles complementam telemetria Olá que você envia a partir do aplicativo hello usando Olá SDK do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="6e0af-106">They complement hello telemetry that you send from within hello app using hello Application Insights SDK.</span></span> <span data-ttu-id="6e0af-107">Como parte de automatizar o processo de saudação de criação de novos recursos no Azure, você pode configurar o diagnóstico usando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="6e0af-107">As part of automating hello process of creating new resources in Azure, you can configure diagnostics using PowerShell.</span></span>

## <a name="azure-template"></a><span data-ttu-id="6e0af-108">Modelo do Azure</span><span class="sxs-lookup"><span data-stu-id="6e0af-108">Azure template</span></span>
<span data-ttu-id="6e0af-109">Se estiver Olá web aplicativo no Azure e criar seus recursos usando um modelo do Azure Resource Manager, você pode configurar o Application Insights adicionando este nó de recursos toohello:</span><span class="sxs-lookup"><span data-stu-id="6e0af-109">If hello web app is in Azure and you create your resources using an Azure Resource Manager template, you can configure Application Insights by adding this toohello resources node:</span></span>

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

* <span data-ttu-id="6e0af-110">`nameOfAIAppResource`-um nome para o recurso do Application Insights de saudação</span><span class="sxs-lookup"><span data-stu-id="6e0af-110">`nameOfAIAppResource` - a name for hello Application Insights resource</span></span>
* <span data-ttu-id="6e0af-111">`myWebAppName`-id de saudação do aplicativo web de saudação</span><span class="sxs-lookup"><span data-stu-id="6e0af-111">`myWebAppName` - hello id of hello web app</span></span>

## <a name="enable-diagnostics-extension-as-part-of-deploying-a-cloud-service"></a><span data-ttu-id="6e0af-112">Habilitar a extensão de diagnóstico como parte da implantação de um Serviço de Nuvem</span><span class="sxs-lookup"><span data-stu-id="6e0af-112">Enable diagnostics extension as part of deploying a Cloud Service</span></span>
<span data-ttu-id="6e0af-113">Olá `New-AzureDeployment` cmdlet tem um parâmetro `ExtensionConfiguration`, que usa uma matriz de configurações de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="6e0af-113">hello `New-AzureDeployment` cmdlet has a parameter `ExtensionConfiguration`, which takes an array of diagnostics configurations.</span></span> <span data-ttu-id="6e0af-114">Eles podem ser criados usando Olá `New-AzureServiceDiagnosticsExtensionConfig` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="6e0af-114">These can be created using hello `New-AzureServiceDiagnosticsExtensionConfig` cmdlet.</span></span> <span data-ttu-id="6e0af-115">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="6e0af-115">For example:</span></span>

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

## <a name="enable-diagnostics-extension-on-an-existing-cloud-service"></a><span data-ttu-id="6e0af-116">Habilitar extensão de diagnóstico em um Serviço de Nuvem existente</span><span class="sxs-lookup"><span data-stu-id="6e0af-116">Enable diagnostics extension on an existing Cloud Service</span></span>
<span data-ttu-id="6e0af-117">Em um serviço existente, use `Set-AzureServiceDiagnosticsExtension`.</span><span class="sxs-lookup"><span data-stu-id="6e0af-117">On an existing service, use `Set-AzureServiceDiagnosticsExtension`.</span></span>

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

## <a name="get-current-diagnostics-extension-configuration"></a><span data-ttu-id="6e0af-118">Obter a configuração de extensão de diagnóstico atual</span><span class="sxs-lookup"><span data-stu-id="6e0af-118">Get current diagnostics extension configuration</span></span>
```ps

    Get-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```


## <a name="remove-diagnostics-extension"></a><span data-ttu-id="6e0af-119">Remover extensão de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="6e0af-119">Remove diagnostics extension</span></span>
```ps

    Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```

<span data-ttu-id="6e0af-120">Se você habilitou a extensão de diagnóstico hello usando `Set-AzureServiceDiagnosticsExtension` ou `New-AzureServiceDiagnosticsExtensionConfig` sem parâmetro de função hello, em seguida, você pode remover Olá extensão usando `Remove-AzureServiceDiagnosticsExtension` sem parâmetro de função hello.</span><span class="sxs-lookup"><span data-stu-id="6e0af-120">If you enabled hello diagnostics extension using either `Set-AzureServiceDiagnosticsExtension` or `New-AzureServiceDiagnosticsExtensionConfig` without hello Role parameter, then you can remove hello extension using `Remove-AzureServiceDiagnosticsExtension` without hello Role parameter.</span></span> <span data-ttu-id="6e0af-121">Se o parâmetro de função hello foi utilizado ao habilitar extensão hello, em seguida, ele também deverá ser usado durante a remoção de extensão de saudação.</span><span class="sxs-lookup"><span data-stu-id="6e0af-121">If hello Role parameter was used when enabling hello extension then it must also be used when removing hello extension.</span></span>

<span data-ttu-id="6e0af-122">extensão de diagnóstico tooremove saudação de cada função individual:</span><span class="sxs-lookup"><span data-stu-id="6e0af-122">tooremove hello diagnostics extension from each individual role:</span></span>

```ps

    Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService" -Role "WebRole"
```


## <a name="see-also"></a><span data-ttu-id="6e0af-123">Consulte também</span><span class="sxs-lookup"><span data-stu-id="6e0af-123">See also</span></span>
* [<span data-ttu-id="6e0af-124">Monitorar aplicativos dos Serviços de Nuvem do Azure com o Application Insights</span><span class="sxs-lookup"><span data-stu-id="6e0af-124">Monitor Azure Cloud Services apps with Application Insights</span></span>](app-insights-cloudservices.md)
* [<span data-ttu-id="6e0af-125">Enviar informações de tooApplication de diagnóstico do Azure</span><span class="sxs-lookup"><span data-stu-id="6e0af-125">Send Azure Diagnostics tooApplication Insights</span></span>](app-insights-azure-diagnostics.md)
* [<span data-ttu-id="6e0af-126">Automatizar a configuração de alertas</span><span class="sxs-lookup"><span data-stu-id="6e0af-126">Automate configuring alerts</span></span>](app-insights-powershell-alerts.md)

