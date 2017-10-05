---
title: "Hospedagem de alta densidade no Serviço de Aplicativo do Azure | Microsoft Docs"
description: "Hospedagem de alta densidade no Serviço de Aplicativo do Azure"
author: btardif
manager: erikre
editor: 
services: app-service\web
documentationcenter: 
ms.assetid: a903cb78-4927-47b0-8427-56412c4e3e64
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 06/12/2017
ms.author: byvinyal
ms.openlocfilehash: 459a310a719695f6366470976d857ec2f9d6f4a1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="high-density-hosting-on-azure-app-service"></a><span data-ttu-id="2ccaa-103">Hospedagem de alta densidade no Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="2ccaa-103">High density hosting on Azure App Service</span></span>
<span data-ttu-id="2ccaa-104">Ao usar o Serviço de Aplicativo, o aplicativo será desassociado da capacidade alocada a ele por dois conceitos:</span><span class="sxs-lookup"><span data-stu-id="2ccaa-104">When using App Service, your application is decoupled from the capacity allocated to it by two concepts:</span></span>

* <span data-ttu-id="2ccaa-105">**O Aplicativo:** representa o Aplicativo e sua configuração de tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="2ccaa-105">**The Application:** Represents the app and its runtime configuration.</span></span> <span data-ttu-id="2ccaa-106">Por exemplo, ele inclui a versão do .NET que o tempo de execução deve carregar, as configurações de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2ccaa-106">For example, it includes the version of .NET that the runtime should load, the app settings.</span></span>
* <span data-ttu-id="2ccaa-107">**O Plano do Serviço de Aplicativo:** define as características de capacidade, o conjunto de recursos disponível e a localidade do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2ccaa-107">**The App Service Plan:** Defines the characteristics of the capacity, available feature set, and locality of the application.</span></span> <span data-ttu-id="2ccaa-108">Por exemplo, as características podem ser computador grande (quatro núcleos), quatro instâncias, recursos Premium no Leste dos EUA.</span><span class="sxs-lookup"><span data-stu-id="2ccaa-108">For example, characteristics might be large (four cores) machine, four instances, Premium features in East US.</span></span>

<span data-ttu-id="2ccaa-109">Um aplicativo sempre está vinculado a um Plano do Serviço de Aplicativo, mas um Plano do Serviço de Aplicativo pode fornecer capacidade a um ou mais aplicativos.</span><span class="sxs-lookup"><span data-stu-id="2ccaa-109">An app is always linked to an App Service plan, but an App Service plan can provide capacity to one or more apps.</span></span>

<span data-ttu-id="2ccaa-110">Como resultado, a plataforma fornece flexibilidade para isolar um único aplicativo ou permitir que vários aplicativos compartilhem recursos com um mesmo Plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2ccaa-110">As a result, the platform provides the flexibility to isolate a single app or have multiple apps share resources by sharing an App Service plan.</span></span>

<span data-ttu-id="2ccaa-111">No entanto, quando vários aplicativos compartilharem um plano do Serviço de Aplicativo, uma instância desse aplicativo será executada em todas as instâncias do plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2ccaa-111">However, when multiple apps share an App Service plan, an instance of that app runs on every instance of that App Service plan.</span></span>

## <a name="per-app-scaling"></a><span data-ttu-id="2ccaa-112">Dimensionamento por aplicativo</span><span class="sxs-lookup"><span data-stu-id="2ccaa-112">Per app scaling</span></span>
<span data-ttu-id="2ccaa-113">*Escala por Aplicativo* é um recurso que pode ser habilitado no nível do plano do Serviço de Aplicativo, sendo posteriormente usado por aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2ccaa-113">*Per app scaling* is a feature that can be enabled at the App Service plan level and then used per application.</span></span>

<span data-ttu-id="2ccaa-114">O dimensionamento por aplicativo escalona um aplicativo independentemente do plano do Serviço de Aplicativo que o hospeda.</span><span class="sxs-lookup"><span data-stu-id="2ccaa-114">Per app scaling scales an app independently from the App Service plan that hosts it.</span></span> <span data-ttu-id="2ccaa-115">Dessa forma, um Plano do Serviço de Aplicativo pode ser dimensionado para 10 instâncias, mas um aplicativo pode ser configurado para usar apenas cinco.</span><span class="sxs-lookup"><span data-stu-id="2ccaa-115">This way, an App Service plan can be scaled to 10 instances, but an app can be set to use only five.</span></span>

   >[!NOTE]
   ><span data-ttu-id="2ccaa-116">O dimensionamento por aplicativo está disponível somente para planos do Serviço de Aplicativo SKU **Premium**</span><span class="sxs-lookup"><span data-stu-id="2ccaa-116">Per app scaling is available only for **Premium** SKU App Service plans</span></span>
   >

### <a name="per-app-scaling-using-powershell"></a><span data-ttu-id="2ccaa-117">Dimensionamento por aplicativo usando PowerShell</span><span class="sxs-lookup"><span data-stu-id="2ccaa-117">Per app scaling using PowerShell</span></span>

<span data-ttu-id="2ccaa-118">Você pode criar um plano configurado como um plano de *Dimensionamento por aplicativo* passando o atributo ```-perSiteScaling $true``` para o commandlet ```New-AzureRmAppServicePlan```</span><span class="sxs-lookup"><span data-stu-id="2ccaa-118">You can create a plan configured as a *Per app scaling* plan by passing in the ```-perSiteScaling $true``` attribute to the ```New-AzureRmAppServicePlan``` commandlet</span></span>

```
New-AzureRmAppServicePlan -ResourceGroupName $ResourceGroup -Name $AppServicePlan `
                            -Location $Location `
                            -Tier Premium -WorkerSize Small `
                            -NumberofWorkers 5 -PerSiteScaling $true
```

<span data-ttu-id="2ccaa-119">Se você quiser atualizar um Plano de Serviço de Aplicativo existente para usar esse recurso:</span><span class="sxs-lookup"><span data-stu-id="2ccaa-119">If you want to update an existing App Service plan to use this feature:</span></span> 

- <span data-ttu-id="2ccaa-120">obtenha o plano de destino ```Get-AzureRmAppServicePlan```</span><span class="sxs-lookup"><span data-stu-id="2ccaa-120">get the target plan ```Get-AzureRmAppServicePlan```</span></span>
- <span data-ttu-id="2ccaa-121">modifique a propriedade localmente ```$newASP.PerSiteScaling = $true```</span><span class="sxs-lookup"><span data-stu-id="2ccaa-121">modifying the property locally ```$newASP.PerSiteScaling = $true```</span></span>
- <span data-ttu-id="2ccaa-122">poste suas alterações no Azure ```Set-AzureRmAppServicePlan```</span><span class="sxs-lookup"><span data-stu-id="2ccaa-122">posting your changes back to azure ```Set-AzureRmAppServicePlan```</span></span> 

```
# Get the new App Service Plan and modify the "PerSiteScaling" property.
$newASP = Get-AzureRmAppServicePlan -ResourceGroupName $ResourceGroup -Name $AppServicePlan
$newASP

#Modify the local copy to use "PerSiteScaling" property.
$newASP.PerSiteScaling = $true
$newASP
    
#Post updated app service plan back to azure
Set-AzureRmAppServicePlan $newASP
```

<span data-ttu-id="2ccaa-123">No nível do aplicativo, é preciso configurar o número de instâncias que o aplicativo pode usar no plano do serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2ccaa-123">At the app level, we need to configure the number of instances the app can use in the app service plan.</span></span>

<span data-ttu-id="2ccaa-124">No exemplo abaixo, o aplicativo está limitado a duas instâncias, independentemente de para quantas instâncias o plano do serviço de aplicativo subjacente pode ser dimensionado.</span><span class="sxs-lookup"><span data-stu-id="2ccaa-124">In the example below, the app is limited to two instances regardless of how many instances the underlying app service plan scales out to.</span></span>

```
# Get the app we want to configure to use "PerSiteScaling"
$newapp = Get-AzureRmWebApp -ResourceGroupName $ResourceGroup -Name $webapp
    
# Modify the NumberOfWorkers setting to the desired value.
$newapp.SiteConfig.NumberOfWorkers = 2
    
# Post updated app back to azure
Set-AzureRmWebApp $newapp
```

> [!IMPORTANT]
> <span data-ttu-id="2ccaa-125">$newapp.SiteConfig.NumberOfWorkers tem uma forma $newapp.MaxNumberOfWorkers. diferente.</span><span class="sxs-lookup"><span data-stu-id="2ccaa-125">$newapp.SiteConfig.NumberOfWorkers is different form $newapp.MaxNumberOfWorkers.</span></span> <span data-ttu-id="2ccaa-126">O dimensionamento por aplicativo usa $newapp.SiteConfig.NumberOfWorkers para determinar as características de dimensionamento do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2ccaa-126">Per app scaling uses $newapp.SiteConfig.NumberOfWorkers to determine the scale characteristics of the app.</span></span>

### <a name="per-app-scaling-using-azure-resource-manager"></a><span data-ttu-id="2ccaa-127">Dimensionamento por aplicativo usando o Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="2ccaa-127">Per app scaling using Azure Resource Manager</span></span>

<span data-ttu-id="2ccaa-128">O seguinte *modelo do Azure Resource Manager* cria:</span><span class="sxs-lookup"><span data-stu-id="2ccaa-128">The following *Azure Resource Manager template* creates:</span></span>

- <span data-ttu-id="2ccaa-129">Um Plano de Serviço de Aplicativo que é dimensionado para 10 instâncias</span><span class="sxs-lookup"><span data-stu-id="2ccaa-129">An App Service plan that's scaled out to 10 instances</span></span>
- <span data-ttu-id="2ccaa-130">Um aplicativo configurado para dimensionar para um máximo de cinco instâncias.</span><span class="sxs-lookup"><span data-stu-id="2ccaa-130">an app that's configured to scale to a max of five instances.</span></span>

<span data-ttu-id="2ccaa-131">O Plano do Serviço de Aplicativo está definindo a propriedade **PerSiteCalling** como verdadeira (```"perSiteScaling": true```).</span><span class="sxs-lookup"><span data-stu-id="2ccaa-131">The App Service plan is setting the **PerSiteScaling** property to true ```"perSiteScaling": true```.</span></span> <span data-ttu-id="2ccaa-132">O aplicativo está definindo o **número de trabalhadores** a usar como 5 (```"properties": { "numberOfWorkers": "5" }```).</span><span class="sxs-lookup"><span data-stu-id="2ccaa-132">The app is setting the **number of workers** to use to 5 ```"properties": { "numberOfWorkers": "5" }```.</span></span>

```
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters":{
        "appServicePlanName": { "type": "string" },
        "appName": { "type": "string" }
        },
    "resources": [
    {
        "comments": "App Service Plan with per site perSiteScaling = true",
        "type": "Microsoft.Web/serverFarms",
        "sku": {
            "name": "P1",
            "tier": "Premium",
            "size": "P1",
            "family": "P",
            "capacity": 10
            },
        "name": "[parameters('appServicePlanName')]",
        "apiVersion": "2015-08-01",
        "location": "West US",
        "properties": {
            "name": "[parameters('appServicePlanName')]",
            "perSiteScaling": true
        }
    },
    {
        "type": "Microsoft.Web/sites",
        "name": "[parameters('appName')]",
        "apiVersion": "2015-08-01-preview",
        "location": "West US",
        "dependsOn": [ "[resourceId('Microsoft.Web/serverFarms', parameters('appServicePlanName'))]" ],
        "properties": { "serverFarmId": "[resourceId('Microsoft.Web/serverFarms', parameters('appServicePlanName'))]" },
        "resources": [ {
                "comments": "",
                "type": "config",
                "name": "web",
                "apiVersion": "2015-08-01",
                "location": "West US",
                "dependsOn": [ "[resourceId('Microsoft.Web/Sites', parameters('appName'))]" ],
                "properties": { "numberOfWorkers": "5" }
            } ]
        }]
}
```

## <a name="recommended-configuration-for-high-density-hosting"></a><span data-ttu-id="2ccaa-133">Configuração recomendada para hospedagem de alta densidade</span><span class="sxs-lookup"><span data-stu-id="2ccaa-133">Recommended configuration for high density hosting</span></span>
<span data-ttu-id="2ccaa-134">O dimensionamento por aplicativo é um recurso que está habilitado em regiões globais do Azure e Ambientes do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2ccaa-134">Per app scaling is a feature that is enabled in both global Azure regions and App Service Environments.</span></span> <span data-ttu-id="2ccaa-135">No entanto, a estratégia recomendada é usar Ambientes de Serviço de Aplicativo para aproveitar os recursos avançados e os pools de maior capacidade.</span><span class="sxs-lookup"><span data-stu-id="2ccaa-135">However, the recommended strategy is to use App Service Environments to take advantage of their advanced features and the larger pools of capacity.</span></span>  

<span data-ttu-id="2ccaa-136">Siga estas etapas para configurar a hospedagem de alta densidade para seus aplicativos:</span><span class="sxs-lookup"><span data-stu-id="2ccaa-136">Follow these steps to configure high density hosting for your apps:</span></span>

1. <span data-ttu-id="2ccaa-137">Configure o Ambiente de Serviço de Aplicativo e escolha um pool de trabalho dedicado ao cenário de hospedagem de alta densidade.</span><span class="sxs-lookup"><span data-stu-id="2ccaa-137">Configure the App Service Environment and choose a worker pool that is dedicated to the high density hosting scenario.</span></span>
1. <span data-ttu-id="2ccaa-138">Crie um único plano do Serviço de Aplicativo e o dimensione para usar toda a capacidade disponível no pool de trabalho.</span><span class="sxs-lookup"><span data-stu-id="2ccaa-138">Create a single App Service plan, and scale it to use all the available capacity on the worker pool.</span></span>
1. <span data-ttu-id="2ccaa-139">Defina o sinalizador PerSiteCalling como verdadeiro no Plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2ccaa-139">Set the PerSiteScaling flag to true on the App Service plan.</span></span>
1. <span data-ttu-id="2ccaa-140">Novos aplicativos são criados e atribuídos a esse Plano do Serviço de Aplicativo com a propriedade **numberOfWorkers** definida como **1**.</span><span class="sxs-lookup"><span data-stu-id="2ccaa-140">New apps are created and assigned to that App Service plan with the **numberOfWorkers** property set to **1**.</span></span> <span data-ttu-id="2ccaa-141">O uso dessa configuração produz a densidade mais alta possível neste pool de trabalho.</span><span class="sxs-lookup"><span data-stu-id="2ccaa-141">Using this configuration yields the highest density possible on this worker pool.</span></span>
1. <span data-ttu-id="2ccaa-142">O número de trabalhadores pode ser configurado independentemente por aplicativo, a fim de conceder recursos adicionais conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="2ccaa-142">The number of workers can be configured independently per app to grant additional resources as needed.</span></span> <span data-ttu-id="2ccaa-143">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="2ccaa-143">For example:</span></span>
    - <span data-ttu-id="2ccaa-144">Um aplicativo de alto consumo pode definir o **numberOfWorkers** como **3** para ter mais capacidade de processamento para esse aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2ccaa-144">A high-use app can set **numberOfWorkers** to **3** to have more processing capacity for that app.</span></span> 
    - <span data-ttu-id="2ccaa-145">Os aplicativos de baixo consumo definiriam o **numberOfWorkers** como **1**.</span><span class="sxs-lookup"><span data-stu-id="2ccaa-145">Low-use apps would set **numberOfWorkers** to **1**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2ccaa-146">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2ccaa-146">Next Steps</span></span>

- [<span data-ttu-id="2ccaa-147">Visão geral detalhada de planos de Serviço de aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="2ccaa-147">Azure App Service plans in-depth overview</span></span>](azure-web-sites-web-hosting-plans-in-depth-overview.md)
- [<span data-ttu-id="2ccaa-148">Introdução ao ambiente de Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="2ccaa-148">Introduction to App Service Environment</span></span>](../app-service-web/app-service-app-service-environment-intro.md)