---
title: Script do PowerShell para criar um recurso do Application Insights | Microsoft Docs
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
ms.openlocfilehash: a828af9c7d207dd84cc626fc70206018fd67e2dd
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="powershell-script-to-create-an-application-insights-resource"></a><span data-ttu-id="2f68a-103">Script do PowerShell para criar um recurso do Application Insights</span><span class="sxs-lookup"><span data-stu-id="2f68a-103">PowerShell script to create an Application Insights resource</span></span>


<span data-ttu-id="2f68a-104">Quando você deseja monitorar um novo aplicativo, ou uma nova versão de um aplicativo, com o [Azure Application Insights](https://azure.microsoft.com/services/application-insights/), você configura um novo recurso no Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="2f68a-104">When you want to monitor a new application - or a new version of an application - with [Azure Application Insights](https://azure.microsoft.com/services/application-insights/), you set up a new resource in Microsoft Azure.</span></span> <span data-ttu-id="2f68a-105">Este recurso é o local no qual os dados de telemetria do seu aplicativo são analisados e exibidos.</span><span class="sxs-lookup"><span data-stu-id="2f68a-105">This resource is where the telemetry data from your app is analyzed and displayed.</span></span> 

<span data-ttu-id="2f68a-106">Você pode automatizar a criação de um novo recurso usando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2f68a-106">You can automate the creation of a new resource by using PowerShell.</span></span>

<span data-ttu-id="2f68a-107">Por exemplo, se você estiver desenvolvendo um aplicativo de dispositivo móvel, é provável que, a qualquer momento, haverá várias versões publicadas do seu aplicativo em uso por seus clientes.</span><span class="sxs-lookup"><span data-stu-id="2f68a-107">For example, if you are developing a mobile device app, it's likely that, at any time, there will be several published versions of your app in use by your customers.</span></span> <span data-ttu-id="2f68a-108">Não é recomendável obter os resultados da telemetria de diferentes versões misturadas.</span><span class="sxs-lookup"><span data-stu-id="2f68a-108">You don't want to get the telemetry results from different versions mixed up.</span></span> <span data-ttu-id="2f68a-109">Por isso, obtenha seu processo de compilação para criar um novo recurso para cada compilação.</span><span class="sxs-lookup"><span data-stu-id="2f68a-109">So you get your build process to create a new resource for each build.</span></span>

> [!NOTE]
> <span data-ttu-id="2f68a-110">Se você quiser criar um conjunto de recursos ao mesmo tempo, considere [criar os recursos usando um modelo do Azure](app-insights-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="2f68a-110">If you want to create a set of resources all at the same time, consider [creating the resources using an Azure template](app-insights-powershell.md).</span></span>
> 
> 

## <a name="script-to-create-an-application-insights-resource"></a><span data-ttu-id="2f68a-111">Script para criar um recurso do Application Insights</span><span class="sxs-lookup"><span data-stu-id="2f68a-111">Script to create an Application Insights resource</span></span>
<span data-ttu-id="2f68a-112">Consulte as especificações do cmdlet relevante:</span><span class="sxs-lookup"><span data-stu-id="2f68a-112">See the relevant cmdlet specs:</span></span>

* [<span data-ttu-id="2f68a-113">New-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="2f68a-113">New-AzureRmResource</span></span>](https://msdn.microsoft.com/library/mt652510.aspx)
* [<span data-ttu-id="2f68a-114">New-AzureRmRoleAssignment</span><span class="sxs-lookup"><span data-stu-id="2f68a-114">New-AzureRmRoleAssignment</span></span>](https://msdn.microsoft.com/library/mt678995.aspx)

<span data-ttu-id="2f68a-115">*Script do PowerShell*</span><span class="sxs-lookup"><span data-stu-id="2f68a-115">*PowerShell Script*</span></span>  

```PowerShell


###########################################
# Set Values
###########################################

# If running manually, uncomment before the first 
# execution to login to the Azure Portal:

# Add-AzureRmAccount / Login-AzureRmAccount

# Set the name of the Application Insights Resource

$appInsightsName = "TestApp"

# Set the application name used for the value of the Tag "AppInsightsApp" 

$applicationTagName = "MyApp"

# Set the name of the Resource Group to use.  
# Default is the application name.
$resourceGroupName = "MyAppResourceGroup"

###################################################
# Create the Resource and Output the name and iKey
###################################################

# Select the azure subscription
Select-AzureSubscription -SubscriptionName "MySubscription"

# Create the App Insights Resource


$resource = New-AzureRmResource `
  -ResourceName $appInsightsName `
  -ResourceGroupName $resourceGroupName `
  -Tag @{ applicationType = "web"; applicationName = $applicationTagName} `
  -ResourceType "Microsoft.Insights/components" `
  -Location "East US" `  # or North Europe, West Europe, South Central US
  -PropertyObject @{"Application_Type"="web"} `
  -Force

# Give owner access to the team

New-AzureRmRoleAssignment `
  -SignInName "myteam@fabrikam.com" `
  -RoleDefinitionName Owner `
  -Scope $resource.ResourceId 


# Display iKey
Write-Host "App Insights Name = " $resource.Name
Write-Host "IKey = " $resource.Properties.InstrumentationKey

```

## <a name="what-to-do-with-the-ikey"></a><span data-ttu-id="2f68a-116">O que fazer com o iKey</span><span class="sxs-lookup"><span data-stu-id="2f68a-116">What to do with the iKey</span></span>
<span data-ttu-id="2f68a-117">Cada recurso é identificado por sua chave de instrumentação (iKey).</span><span class="sxs-lookup"><span data-stu-id="2f68a-117">Each resource is identified by its instrumentation key (iKey).</span></span> <span data-ttu-id="2f68a-118">O iKey é uma saída do script de criação de recursos.</span><span class="sxs-lookup"><span data-stu-id="2f68a-118">The iKey is an output of the resource creation script.</span></span> <span data-ttu-id="2f68a-119">Seu script de compilação deve fornecer o iKey para o SDK do Application Insights inserido no seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2f68a-119">Your build script should provide the iKey to the Application Insights SDK embedded in your app.</span></span>

<span data-ttu-id="2f68a-120">Há duas maneiras de disponibilizar o iKey para o SDK:</span><span class="sxs-lookup"><span data-stu-id="2f68a-120">There are two ways to make the iKey available to the SDK:</span></span>

* <span data-ttu-id="2f68a-121">No [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span><span class="sxs-lookup"><span data-stu-id="2f68a-121">In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span></span> 
  * <span data-ttu-id="2f68a-122">`<instrumentationkey>`*ikey*`</instrumentationkey>`</span><span class="sxs-lookup"><span data-stu-id="2f68a-122">`<instrumentationkey>`*ikey*`</instrumentationkey>`</span></span>
* <span data-ttu-id="2f68a-123">Ou no [código de inicialização](app-insights-api-custom-events-metrics.md):</span><span class="sxs-lookup"><span data-stu-id="2f68a-123">Or in [initialization code](app-insights-api-custom-events-metrics.md):</span></span> 
  * <span data-ttu-id="2f68a-124">`Microsoft.ApplicationInsights.Extensibility.
    TelemetryConfiguration.Active.InstrumentationKey = "`*iKey*`";`</span><span class="sxs-lookup"><span data-stu-id="2f68a-124">`Microsoft.ApplicationInsights.Extensibility.
TelemetryConfiguration.Active.InstrumentationKey = "`*iKey*`";`</span></span>

## <a name="see-also"></a><span data-ttu-id="2f68a-125">Consulte também</span><span class="sxs-lookup"><span data-stu-id="2f68a-125">See also</span></span>
* [<span data-ttu-id="2f68a-126">Criar recursos de teste da Web e do Application Insights por meio de modelos</span><span class="sxs-lookup"><span data-stu-id="2f68a-126">Create Application Insights and web test resources from templates</span></span>](app-insights-powershell.md)
* [<span data-ttu-id="2f68a-127">Configurar o monitoramento do diagnóstico do Azure com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="2f68a-127">Set up monitoring of Azure diagnostics with PowerShell</span></span>](app-insights-powershell-azure-diagnostics.md) 
* [<span data-ttu-id="2f68a-128">Definir alertas usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="2f68a-128">Set alerts by using PowerShell</span></span>](app-insights-powershell-alerts.md)

