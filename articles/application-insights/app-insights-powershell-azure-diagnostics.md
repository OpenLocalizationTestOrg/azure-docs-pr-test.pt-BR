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
# <a name="using-powershell-tooset-up-application-insights-for-an-azure-web-app"></a>Usando o PowerShell tooset o Application Insights para um aplicativo web do Azure
[Microsoft Azure](https://azure.com) pode ser [configurado o diagnóstico do Azure toosend](app-insights-azure-diagnostics.md) muito[Azure Application Insights](app-insights-overview.md). Olá diagnóstico relacionar tooAzure serviços de nuvem e VMs do Azure. Eles complementam telemetria Olá que você envia a partir do aplicativo hello usando Olá SDK do Application Insights. Como parte de automatizar o processo de saudação de criação de novos recursos no Azure, você pode configurar o diagnóstico usando o PowerShell.

## <a name="azure-template"></a>Modelo do Azure
Se estiver Olá web aplicativo no Azure e criar seus recursos usando um modelo do Azure Resource Manager, você pode configurar o Application Insights adicionando este nó de recursos toohello:

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

* `nameOfAIAppResource`-um nome para o recurso do Application Insights de saudação
* `myWebAppName`-id de saudação do aplicativo web de saudação

## <a name="enable-diagnostics-extension-as-part-of-deploying-a-cloud-service"></a>Habilitar a extensão de diagnóstico como parte da implantação de um Serviço de Nuvem
Olá `New-AzureDeployment` cmdlet tem um parâmetro `ExtensionConfiguration`, que usa uma matriz de configurações de diagnóstico. Eles podem ser criados usando Olá `New-AzureServiceDiagnosticsExtensionConfig` cmdlet. Por exemplo:

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

## <a name="enable-diagnostics-extension-on-an-existing-cloud-service"></a>Habilitar extensão de diagnóstico em um Serviço de Nuvem existente
Em um serviço existente, use `Set-AzureServiceDiagnosticsExtension`.

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

## <a name="get-current-diagnostics-extension-configuration"></a>Obter a configuração de extensão de diagnóstico atual
```ps

    Get-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```


## <a name="remove-diagnostics-extension"></a>Remover extensão de diagnóstico
```ps

    Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```

Se você habilitou a extensão de diagnóstico hello usando `Set-AzureServiceDiagnosticsExtension` ou `New-AzureServiceDiagnosticsExtensionConfig` sem parâmetro de função hello, em seguida, você pode remover Olá extensão usando `Remove-AzureServiceDiagnosticsExtension` sem parâmetro de função hello. Se o parâmetro de função hello foi utilizado ao habilitar extensão hello, em seguida, ele também deverá ser usado durante a remoção de extensão de saudação.

extensão de diagnóstico tooremove saudação de cada função individual:

```ps

    Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService" -Role "WebRole"
```


## <a name="see-also"></a>Consulte também
* [Monitorar aplicativos dos Serviços de Nuvem do Azure com o Application Insights](app-insights-cloudservices.md)
* [Enviar informações de tooApplication de diagnóstico do Azure](app-insights-azure-diagnostics.md)
* [Automatizar a configuração de alertas](app-insights-powershell-alerts.md)

