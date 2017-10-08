---
title: aaaPowerShell script toocreate um recurso do Application Insights | Microsoft Docs
description: "Automatize a criação de recursos do Application Insights."
services: application-insights
documentationcenter: windows
author: CFreemanwa
manager: carmonm
ms.assetid: f0082c9b-43ad-4576-a417-4ea8e0daf3d9
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/19/2016
ms.author: bwren
ms.openlocfilehash: 2ac00376d38026d64c2c5deabfaca60588924510
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="powershell-script-toocreate-an-application-insights-resource"></a>Toocreate de script do PowerShell um recurso do Application Insights


Quando você deseja toomonitor um novo aplicativo - ou uma nova versão de um aplicativo - com [Azure Application Insights](https://azure.microsoft.com/services/application-insights/), defina um novo recurso no Microsoft Azure. Esse recurso é onde os dados de telemetria de saudação do seu aplicativo são analisados e exibidos. 

Você pode automatizar a criação de um novo recurso hello usando o PowerShell.

Por exemplo, se você estiver desenvolvendo um aplicativo de dispositivo móvel, é provável que, a qualquer momento, haverá várias versões publicadas do seu aplicativo em uso por seus clientes. Você não deseja que os resultados de telemetria Olá tooget de diferentes versões misturadas. Para que você obtenha um novo recurso de seu toocreate do processo de compilação para cada compilação.

> [!NOTE]
> Se você quiser que um conjunto de recursos todos toocreate Olá mesmo tempo, considere [criar hello recursos usando um modelo do Azure](app-insights-powershell.md).
> 
> 

## <a name="script-toocreate-an-application-insights-resource"></a>Script toocreate um recurso do Application Insights
Consulte as especificações de cmdlet relevante hello:

* [New-AzureRmResource](https://msdn.microsoft.com/library/mt652510.aspx)
* [New-AzureRmRoleAssignment](https://msdn.microsoft.com/library/mt678995.aspx)

*Script do PowerShell*  

```PowerShell


###########################################
# Set Values
###########################################

# If running manually, uncomment before hello first 
# execution toologin toohello Azure Portal:

# Add-AzureRmAccount / Login-AzureRmAccount

# Set hello name of hello Application Insights Resource

$appInsightsName = "TestApp"

# Set hello application name used for hello value of hello Tag "AppInsightsApp" 

$applicationTagName = "MyApp"

# Set hello name of hello Resource Group toouse.  
# Default is hello application name.
$resourceGroupName = "MyAppResourceGroup"

###################################################
# Create hello Resource and Output hello name and iKey
###################################################

# Select hello azure subscription
Select-AzureSubscription -SubscriptionName "MySubscription"

# Create hello App Insights Resource


$resource = New-AzureRmResource `
  -ResourceName $appInsightsName `
  -ResourceGroupName $resourceGroupName `
  -Tag @{ applicationType = "web"; applicationName = $applicationTagName} `
  -ResourceType "Microsoft.Insights/components" `
  -Location "East US" `  # or North Europe, West Europe, South Central US
  -PropertyObject @{"Application_Type"="web"} `
  -Force

# Give owner access toohello team

New-AzureRmRoleAssignment `
  -SignInName "myteam@fabrikam.com" `
  -RoleDefinitionName Owner `
  -Scope $resource.ResourceId 


# Display iKey
Write-Host "App Insights Name = " $resource.Name
Write-Host "IKey = " $resource.Properties.InstrumentationKey

```

## <a name="what-toodo-with-hello-ikey"></a>Quais toodo com iKey Olá
Cada recurso é identificado por sua chave de instrumentação (iKey). Olá iKey é uma saída do script de criação de recursos de saudação. O script de compilação deve fornecer Olá iKey toohello que SDK do Application Insights inserido em seu aplicativo.

Há duas maneiras toomake Olá iKey disponível toohello SDK:

* No [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md): 
  * `<instrumentationkey>`*ikey*`</instrumentationkey>`
* Ou no [código de inicialização](app-insights-api-custom-events-metrics.md): 
  * `Microsoft.ApplicationInsights.Extensibility.
    TelemetryConfiguration.Active.InstrumentationKey = "`*iKey*`";`

## <a name="see-also"></a>Consulte também
* [Criar recursos de teste da Web e do Application Insights por meio de modelos](app-insights-powershell.md)
* [Configurar o monitoramento do diagnóstico do Azure com o PowerShell](app-insights-powershell-azure-diagnostics.md) 
* [Definir alertas usando o PowerShell](app-insights-powershell-alerts.md)

