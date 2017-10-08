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
# <a name="powershell-script-toocreate-an-application-insights-resource"></a><span data-ttu-id="4f628-103">Toocreate de script do PowerShell um recurso do Application Insights</span><span class="sxs-lookup"><span data-stu-id="4f628-103">PowerShell script toocreate an Application Insights resource</span></span>


<span data-ttu-id="4f628-104">Quando você deseja toomonitor um novo aplicativo - ou uma nova versão de um aplicativo - com [Azure Application Insights](https://azure.microsoft.com/services/application-insights/), defina um novo recurso no Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="4f628-104">When you want toomonitor a new application - or a new version of an application - with [Azure Application Insights](https://azure.microsoft.com/services/application-insights/), you set up a new resource in Microsoft Azure.</span></span> <span data-ttu-id="4f628-105">Esse recurso é onde os dados de telemetria de saudação do seu aplicativo são analisados e exibidos.</span><span class="sxs-lookup"><span data-stu-id="4f628-105">This resource is where hello telemetry data from your app is analyzed and displayed.</span></span> 

<span data-ttu-id="4f628-106">Você pode automatizar a criação de um novo recurso hello usando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4f628-106">You can automate hello creation of a new resource by using PowerShell.</span></span>

<span data-ttu-id="4f628-107">Por exemplo, se você estiver desenvolvendo um aplicativo de dispositivo móvel, é provável que, a qualquer momento, haverá várias versões publicadas do seu aplicativo em uso por seus clientes.</span><span class="sxs-lookup"><span data-stu-id="4f628-107">For example, if you are developing a mobile device app, it's likely that, at any time, there will be several published versions of your app in use by your customers.</span></span> <span data-ttu-id="4f628-108">Você não deseja que os resultados de telemetria Olá tooget de diferentes versões misturadas.</span><span class="sxs-lookup"><span data-stu-id="4f628-108">You don't want tooget hello telemetry results from different versions mixed up.</span></span> <span data-ttu-id="4f628-109">Para que você obtenha um novo recurso de seu toocreate do processo de compilação para cada compilação.</span><span class="sxs-lookup"><span data-stu-id="4f628-109">So you get your build process toocreate a new resource for each build.</span></span>

> [!NOTE]
> <span data-ttu-id="4f628-110">Se você quiser que um conjunto de recursos todos toocreate Olá mesmo tempo, considere [criar hello recursos usando um modelo do Azure](app-insights-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="4f628-110">If you want toocreate a set of resources all at hello same time, consider [creating hello resources using an Azure template](app-insights-powershell.md).</span></span>
> 
> 

## <a name="script-toocreate-an-application-insights-resource"></a><span data-ttu-id="4f628-111">Script toocreate um recurso do Application Insights</span><span class="sxs-lookup"><span data-stu-id="4f628-111">Script toocreate an Application Insights resource</span></span>
<span data-ttu-id="4f628-112">Consulte as especificações de cmdlet relevante hello:</span><span class="sxs-lookup"><span data-stu-id="4f628-112">See hello relevant cmdlet specs:</span></span>

* [<span data-ttu-id="4f628-113">New-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="4f628-113">New-AzureRmResource</span></span>](https://msdn.microsoft.com/library/mt652510.aspx)
* [<span data-ttu-id="4f628-114">New-AzureRmRoleAssignment</span><span class="sxs-lookup"><span data-stu-id="4f628-114">New-AzureRmRoleAssignment</span></span>](https://msdn.microsoft.com/library/mt678995.aspx)

<span data-ttu-id="4f628-115">*Script do PowerShell*</span><span class="sxs-lookup"><span data-stu-id="4f628-115">*PowerShell Script*</span></span>  

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

## <a name="what-toodo-with-hello-ikey"></a><span data-ttu-id="4f628-116">Quais toodo com iKey Olá</span><span class="sxs-lookup"><span data-stu-id="4f628-116">What toodo with hello iKey</span></span>
<span data-ttu-id="4f628-117">Cada recurso é identificado por sua chave de instrumentação (iKey).</span><span class="sxs-lookup"><span data-stu-id="4f628-117">Each resource is identified by its instrumentation key (iKey).</span></span> <span data-ttu-id="4f628-118">Olá iKey é uma saída do script de criação de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="4f628-118">hello iKey is an output of hello resource creation script.</span></span> <span data-ttu-id="4f628-119">O script de compilação deve fornecer Olá iKey toohello que SDK do Application Insights inserido em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4f628-119">Your build script should provide hello iKey toohello Application Insights SDK embedded in your app.</span></span>

<span data-ttu-id="4f628-120">Há duas maneiras toomake Olá iKey disponível toohello SDK:</span><span class="sxs-lookup"><span data-stu-id="4f628-120">There are two ways toomake hello iKey available toohello SDK:</span></span>

* <span data-ttu-id="4f628-121">No [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span><span class="sxs-lookup"><span data-stu-id="4f628-121">In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span></span> 
  * <span data-ttu-id="4f628-122">`<instrumentationkey>`*ikey*`</instrumentationkey>`</span><span class="sxs-lookup"><span data-stu-id="4f628-122">`<instrumentationkey>`*ikey*`</instrumentationkey>`</span></span>
* <span data-ttu-id="4f628-123">Ou no [código de inicialização](app-insights-api-custom-events-metrics.md):</span><span class="sxs-lookup"><span data-stu-id="4f628-123">Or in [initialization code](app-insights-api-custom-events-metrics.md):</span></span> 
  * <span data-ttu-id="4f628-124">`Microsoft.ApplicationInsights.Extensibility.
    TelemetryConfiguration.Active.InstrumentationKey = "`*iKey*`";`</span><span class="sxs-lookup"><span data-stu-id="4f628-124">`Microsoft.ApplicationInsights.Extensibility.
TelemetryConfiguration.Active.InstrumentationKey = "`*iKey*`";`</span></span>

## <a name="see-also"></a><span data-ttu-id="4f628-125">Consulte também</span><span class="sxs-lookup"><span data-stu-id="4f628-125">See also</span></span>
* [<span data-ttu-id="4f628-126">Criar recursos de teste da Web e do Application Insights por meio de modelos</span><span class="sxs-lookup"><span data-stu-id="4f628-126">Create Application Insights and web test resources from templates</span></span>](app-insights-powershell.md)
* [<span data-ttu-id="4f628-127">Configurar o monitoramento do diagnóstico do Azure com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="4f628-127">Set up monitoring of Azure diagnostics with PowerShell</span></span>](app-insights-powershell-azure-diagnostics.md) 
* [<span data-ttu-id="4f628-128">Definir alertas usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="4f628-128">Set alerts by using PowerShell</span></span>](app-insights-powershell-alerts.md)

