---
title: "aaaHigh densidade hospedagem no serviço de aplicativo do Azure | Microsoft Docs"
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
ms.openlocfilehash: a10cb81ace13ba6992b572a44361061ecf72b266
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="high-density-hosting-on-azure-app-service"></a><span data-ttu-id="b239d-103">Hospedagem de alta densidade no Serviço de Aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="b239d-103">High density hosting on Azure App Service</span></span>
<span data-ttu-id="b239d-104">Ao usar o serviço de aplicativo, o aplicativo é separado da saudação capacidade alocada tooit por dois conceitos:</span><span class="sxs-lookup"><span data-stu-id="b239d-104">When using App Service, your application is decoupled from hello capacity allocated tooit by two concepts:</span></span>

* <span data-ttu-id="b239d-105">**Olá aplicativo:** representa o aplicativo hello e sua configuração de tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="b239d-105">**hello Application:** Represents hello app and its runtime configuration.</span></span> <span data-ttu-id="b239d-106">Por exemplo, ele inclui Olá versão do .NET que Olá em tempo de execução devem ser carregadas, as configurações do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="b239d-106">For example, it includes hello version of .NET that hello runtime should load, hello app settings.</span></span>
* <span data-ttu-id="b239d-107">**Olá plano do serviço de aplicativo:** define as características de saudação do capacidade hello, conjunto de recursos disponíveis e localidade do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="b239d-107">**hello App Service Plan:** Defines hello characteristics of hello capacity, available feature set, and locality of hello application.</span></span> <span data-ttu-id="b239d-108">Por exemplo, as características podem ser computador grande (quatro núcleos), quatro instâncias, recursos Premium no Leste dos EUA.</span><span class="sxs-lookup"><span data-stu-id="b239d-108">For example, characteristics might be large (four cores) machine, four instances, Premium features in East US.</span></span>

<span data-ttu-id="b239d-109">Um aplicativo é sempre tooan vinculado plano de serviço de aplicativo, mas um plano de serviço de aplicativo pode fornecer capacidade tooone ou mais aplicativos.</span><span class="sxs-lookup"><span data-stu-id="b239d-109">An app is always linked tooan App Service plan, but an App Service plan can provide capacity tooone or more apps.</span></span>

<span data-ttu-id="b239d-110">Como resultado, a plataforma de Olá fornece Olá flexibilidade tooisolate um único aplicativo ou ter vários aplicativos compartilhem recursos compartilhando um plano de serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b239d-110">As a result, hello platform provides hello flexibility tooisolate a single app or have multiple apps share resources by sharing an App Service plan.</span></span>

<span data-ttu-id="b239d-111">No entanto, quando vários aplicativos compartilharem um plano do Serviço de Aplicativo, uma instância desse aplicativo será executada em todas as instâncias do plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b239d-111">However, when multiple apps share an App Service plan, an instance of that app runs on every instance of that App Service plan.</span></span>

## <a name="per-app-scaling"></a><span data-ttu-id="b239d-112">Dimensionamento por aplicativo</span><span class="sxs-lookup"><span data-stu-id="b239d-112">Per app scaling</span></span>
<span data-ttu-id="b239d-113">*Escala por Aplicativo* é um recurso que pode ser habilitado no nível do plano do Serviço de Aplicativo, sendo posteriormente usado por aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b239d-113">*Per app scaling* is a feature that can be enabled at the App Service plan level and then used per application.</span></span>

<span data-ttu-id="b239d-114">O dimensionamento por aplicativo escalona um aplicativo independentemente do plano do Serviço de Aplicativo que o hospeda.</span><span class="sxs-lookup"><span data-stu-id="b239d-114">Per app scaling scales an app independently from the App Service plan that hosts it.</span></span> <span data-ttu-id="b239d-115">Dessa forma, um aplicativo de serviço pode ser dimensionado too10 instâncias, mas um aplicativo pode ser definido como toouse apenas cinco.</span><span class="sxs-lookup"><span data-stu-id="b239d-115">This way, an App Service plan can be scaled too10 instances, but an app can be set toouse only five.</span></span>

   >[!NOTE]
   ><span data-ttu-id="b239d-116">O dimensionamento por aplicativo está disponível somente para planos do Serviço de Aplicativo SKU **Premium**</span><span class="sxs-lookup"><span data-stu-id="b239d-116">Per app scaling is available only for **Premium** SKU App Service plans</span></span>
   >

### <a name="per-app-scaling-using-powershell"></a><span data-ttu-id="b239d-117">Dimensionamento por aplicativo usando PowerShell</span><span class="sxs-lookup"><span data-stu-id="b239d-117">Per app scaling using PowerShell</span></span>

<span data-ttu-id="b239d-118">Você pode criar um plano configurado como um *por aplicativo dimensionamento* plano passando Olá ```-perSiteScaling $true``` atributo toohello ```New-AzureRmAppServicePlan``` commandlet</span><span class="sxs-lookup"><span data-stu-id="b239d-118">You can create a plan configured as a *Per app scaling* plan by passing in hello ```-perSiteScaling $true``` attribute toohello ```New-AzureRmAppServicePlan``` commandlet</span></span>

```
New-AzureRmAppServicePlan -ResourceGroupName $ResourceGroup -Name $AppServicePlan `
                            -Location $Location `
                            -Tier Premium -WorkerSize Small `
                            -NumberofWorkers 5 -PerSiteScaling $true
```

<span data-ttu-id="b239d-119">Se você quiser tooupdate um serviço de aplicativo existente planeje toouse esse recurso:</span><span class="sxs-lookup"><span data-stu-id="b239d-119">If you want tooupdate an existing App Service plan toouse this feature:</span></span> 

- <span data-ttu-id="b239d-120">obter o plano de destino Olá```Get-AzureRmAppServicePlan```</span><span class="sxs-lookup"><span data-stu-id="b239d-120">get hello target plan ```Get-AzureRmAppServicePlan```</span></span>
- <span data-ttu-id="b239d-121">modificando a propriedade de saudação localmente```$newASP.PerSiteScaling = $true```</span><span class="sxs-lookup"><span data-stu-id="b239d-121">modifying hello property locally ```$newASP.PerSiteScaling = $true```</span></span>
- <span data-ttu-id="b239d-122">postar sua tooazure voltar de alterações```Set-AzureRmAppServicePlan```</span><span class="sxs-lookup"><span data-stu-id="b239d-122">posting your changes back tooazure ```Set-AzureRmAppServicePlan```</span></span> 

```
# Get hello new App Service Plan and modify hello "PerSiteScaling" property.
$newASP = Get-AzureRmAppServicePlan -ResourceGroupName $ResourceGroup -Name $AppServicePlan
$newASP

#Modify hello local copy toouse "PerSiteScaling" property.
$newASP.PerSiteScaling = $true
$newASP
    
#Post updated app service plan back tooazure
Set-AzureRmAppServicePlan $newASP
```

<span data-ttu-id="b239d-123">No nível do aplicativo hello, precisamos de número de saudação do tooconfigure de instâncias Olá aplicativo pode usar no plano de serviço de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="b239d-123">At hello app level, we need tooconfigure hello number of instances hello app can use in hello app service plan.</span></span>

<span data-ttu-id="b239d-124">Exemplo hello abaixo, o aplicativo hello é tootwo limitado de instâncias, independentemente de quantas instâncias Olá subjacente aplicativo serviço plano escalas out para.</span><span class="sxs-lookup"><span data-stu-id="b239d-124">In hello example below, hello app is limited tootwo instances regardless of how many instances hello underlying app service plan scales out to.</span></span>

```
# Get hello app we want tooconfigure toouse "PerSiteScaling"
$newapp = Get-AzureRmWebApp -ResourceGroupName $ResourceGroup -Name $webapp
    
# Modify hello NumberOfWorkers setting toohello desired value.
$newapp.SiteConfig.NumberOfWorkers = 2
    
# Post updated app back tooazure
Set-AzureRmWebApp $newapp
```

> [!IMPORTANT]
> <span data-ttu-id="b239d-125">$newapp.SiteConfig.NumberOfWorkers tem uma forma $newapp.MaxNumberOfWorkers. diferente.</span><span class="sxs-lookup"><span data-stu-id="b239d-125">$newapp.SiteConfig.NumberOfWorkers is different form $newapp.MaxNumberOfWorkers.</span></span> <span data-ttu-id="b239d-126">Cada aplicativo dimensionamento usa $newapp. Características de escala SiteConfig.NumberOfWorkers toodetermine saudação do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="b239d-126">Per app scaling uses $newapp.SiteConfig.NumberOfWorkers toodetermine hello scale characteristics of hello app.</span></span>

### <a name="per-app-scaling-using-azure-resource-manager"></a><span data-ttu-id="b239d-127">Dimensionamento por aplicativo usando o Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b239d-127">Per app scaling using Azure Resource Manager</span></span>

<span data-ttu-id="b239d-128">a seguir Olá *modelo do Azure Resource Manager* cria:</span><span class="sxs-lookup"><span data-stu-id="b239d-128">hello following *Azure Resource Manager template* creates:</span></span>

- <span data-ttu-id="b239d-129">Um plano de serviço de aplicativo que é expandido too10 instâncias</span><span class="sxs-lookup"><span data-stu-id="b239d-129">An App Service plan that's scaled out too10 instances</span></span>
- <span data-ttu-id="b239d-130">um aplicativo que tenha configurado tooscale tooa máximo de cinco instâncias.</span><span class="sxs-lookup"><span data-stu-id="b239d-130">an app that's configured tooscale tooa max of five instances.</span></span>

<span data-ttu-id="b239d-131">Olá plano de serviço de aplicativo está definindo Olá **PerSiteScaling** tootrue propriedade ```"perSiteScaling": true```.</span><span class="sxs-lookup"><span data-stu-id="b239d-131">hello App Service plan is setting hello **PerSiteScaling** property tootrue ```"perSiteScaling": true```.</span></span> <span data-ttu-id="b239d-132">aplicativo Hello está definindo Olá **número de trabalhadores** toouse too5 ```"properties": { "numberOfWorkers": "5" }```.</span><span class="sxs-lookup"><span data-stu-id="b239d-132">hello app is setting hello **number of workers** toouse too5 ```"properties": { "numberOfWorkers": "5" }```.</span></span>

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

## <a name="recommended-configuration-for-high-density-hosting"></a><span data-ttu-id="b239d-133">Configuração recomendada para hospedagem de alta densidade</span><span class="sxs-lookup"><span data-stu-id="b239d-133">Recommended configuration for high density hosting</span></span>
<span data-ttu-id="b239d-134">O dimensionamento por aplicativo é um recurso que está habilitado em regiões globais do Azure e Ambientes do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b239d-134">Per app scaling is a feature that is enabled in both global Azure regions and App Service Environments.</span></span> <span data-ttu-id="b239d-135">No entanto, Olá recomendado estratégia é usar os ambientes de serviço de aplicativo tootake de seus recursos avançados e pools de saudação maior de capacidade.</span><span class="sxs-lookup"><span data-stu-id="b239d-135">However, hello recommended strategy is to use App Service Environments tootake advantage of their advanced features and hello larger pools of capacity.</span></span>  

<span data-ttu-id="b239d-136">Siga estas etapas tooconfigure alta densidade de hospedagem para seus aplicativos:</span><span class="sxs-lookup"><span data-stu-id="b239d-136">Follow these steps tooconfigure high density hosting for your apps:</span></span>

1. <span data-ttu-id="b239d-137">Configurar Olá ambiente de serviço de aplicativo e escolha um pool de trabalho que é dedicado toohello alta densidade do cenário de hospedagem.</span><span class="sxs-lookup"><span data-stu-id="b239d-137">Configure hello App Service Environment and choose a worker pool that is dedicated toohello high density hosting scenario.</span></span>
1. <span data-ttu-id="b239d-138">Criar um único plano de serviço de aplicativo e dimensioná-lo toouse todos Olá capacidade disponível no pool do trabalhador hello.</span><span class="sxs-lookup"><span data-stu-id="b239d-138">Create a single App Service plan, and scale it toouse all hello available capacity on hello worker pool.</span></span>
1. <span data-ttu-id="b239d-139">Defina Olá PerSiteScaling sinalizador tootrue em Olá plano de serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b239d-139">Set hello PerSiteScaling flag tootrue on hello App Service plan.</span></span>
1. <span data-ttu-id="b239d-140">Novos aplicativos são criados e atribuídos toothat plano de serviço de aplicativo com o **numberOfWorkers** propriedade definida muito**1**.</span><span class="sxs-lookup"><span data-stu-id="b239d-140">New apps are created and assigned toothat App Service plan with the **numberOfWorkers** property set too**1**.</span></span> <span data-ttu-id="b239d-141">Usando essa configuração gera hello mais alta densidade possíveis neste pool de trabalho.</span><span class="sxs-lookup"><span data-stu-id="b239d-141">Using this configuration yields hello highest density possible on this worker pool.</span></span>
1. <span data-ttu-id="b239d-142">número de saudação de trabalhos pode ser configurado independentemente por recursos do aplicativo toogrant adicionais conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="b239d-142">hello number of workers can be configured independently per app toogrant additional resources as needed.</span></span> <span data-ttu-id="b239d-143">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="b239d-143">For example:</span></span>
    - <span data-ttu-id="b239d-144">Um aplicativo de alto uso pode definir **numberOfWorkers** muito**3** toohave mais capacidade para que o aplicativo de processamento.</span><span class="sxs-lookup"><span data-stu-id="b239d-144">A high-use app can set **numberOfWorkers** too**3** toohave more processing capacity for that app.</span></span> 
    - <span data-ttu-id="b239d-145">Aplicativos de baixo uso definiria **numberOfWorkers** muito**1**.</span><span class="sxs-lookup"><span data-stu-id="b239d-145">Low-use apps would set **numberOfWorkers** too**1**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b239d-146">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b239d-146">Next Steps</span></span>

- [<span data-ttu-id="b239d-147">Visão geral detalhada de planos de Serviço de aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="b239d-147">Azure App Service plans in-depth overview</span></span>](azure-web-sites-web-hosting-plans-in-depth-overview.md)
- [<span data-ttu-id="b239d-148">Introdução tooApp ambiente de serviço</span><span class="sxs-lookup"><span data-stu-id="b239d-148">Introduction tooApp Service Environment</span></span>](../app-service-web/app-service-app-service-environment-intro.md)
