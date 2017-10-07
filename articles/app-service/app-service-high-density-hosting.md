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
# <a name="high-density-hosting-on-azure-app-service"></a>Hospedagem de alta densidade no Serviço de Aplicativo do Azure
Ao usar o serviço de aplicativo, o aplicativo é separado da saudação capacidade alocada tooit por dois conceitos:

* **Olá aplicativo:** representa o aplicativo hello e sua configuração de tempo de execução. Por exemplo, ele inclui Olá versão do .NET que Olá em tempo de execução devem ser carregadas, as configurações do aplicativo hello.
* **Olá plano do serviço de aplicativo:** define as características de saudação do capacidade hello, conjunto de recursos disponíveis e localidade do aplicativo hello. Por exemplo, as características podem ser computador grande (quatro núcleos), quatro instâncias, recursos Premium no Leste dos EUA.

Um aplicativo é sempre tooan vinculado plano de serviço de aplicativo, mas um plano de serviço de aplicativo pode fornecer capacidade tooone ou mais aplicativos.

Como resultado, a plataforma de Olá fornece Olá flexibilidade tooisolate um único aplicativo ou ter vários aplicativos compartilhem recursos compartilhando um plano de serviço de aplicativo.

No entanto, quando vários aplicativos compartilharem um plano do Serviço de Aplicativo, uma instância desse aplicativo será executada em todas as instâncias do plano do Serviço de Aplicativo.

## <a name="per-app-scaling"></a>Dimensionamento por aplicativo
*Escala por Aplicativo* é um recurso que pode ser habilitado no nível do plano do Serviço de Aplicativo, sendo posteriormente usado por aplicativo.

O dimensionamento por aplicativo escalona um aplicativo independentemente do plano do Serviço de Aplicativo que o hospeda. Dessa forma, um aplicativo de serviço pode ser dimensionado too10 instâncias, mas um aplicativo pode ser definido como toouse apenas cinco.

   >[!NOTE]
   >O dimensionamento por aplicativo está disponível somente para planos do Serviço de Aplicativo SKU **Premium**
   >

### <a name="per-app-scaling-using-powershell"></a>Dimensionamento por aplicativo usando PowerShell

Você pode criar um plano configurado como um *por aplicativo dimensionamento* plano passando Olá ```-perSiteScaling $true``` atributo toohello ```New-AzureRmAppServicePlan``` commandlet

```
New-AzureRmAppServicePlan -ResourceGroupName $ResourceGroup -Name $AppServicePlan `
                            -Location $Location `
                            -Tier Premium -WorkerSize Small `
                            -NumberofWorkers 5 -PerSiteScaling $true
```

Se você quiser tooupdate um serviço de aplicativo existente planeje toouse esse recurso: 

- obter o plano de destino Olá```Get-AzureRmAppServicePlan```
- modificando a propriedade de saudação localmente```$newASP.PerSiteScaling = $true```
- postar sua tooazure voltar de alterações```Set-AzureRmAppServicePlan``` 

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

No nível do aplicativo hello, precisamos de número de saudação do tooconfigure de instâncias Olá aplicativo pode usar no plano de serviço de aplicativo hello.

Exemplo hello abaixo, o aplicativo hello é tootwo limitado de instâncias, independentemente de quantas instâncias Olá subjacente aplicativo serviço plano escalas out para.

```
# Get hello app we want tooconfigure toouse "PerSiteScaling"
$newapp = Get-AzureRmWebApp -ResourceGroupName $ResourceGroup -Name $webapp
    
# Modify hello NumberOfWorkers setting toohello desired value.
$newapp.SiteConfig.NumberOfWorkers = 2
    
# Post updated app back tooazure
Set-AzureRmWebApp $newapp
```

> [!IMPORTANT]
> $newapp.SiteConfig.NumberOfWorkers tem uma forma $newapp.MaxNumberOfWorkers. diferente. Cada aplicativo dimensionamento usa $newapp. Características de escala SiteConfig.NumberOfWorkers toodetermine saudação do aplicativo hello.

### <a name="per-app-scaling-using-azure-resource-manager"></a>Dimensionamento por aplicativo usando o Azure Resource Manager

a seguir Olá *modelo do Azure Resource Manager* cria:

- Um plano de serviço de aplicativo que é expandido too10 instâncias
- um aplicativo que tenha configurado tooscale tooa máximo de cinco instâncias.

Olá plano de serviço de aplicativo está definindo Olá **PerSiteScaling** tootrue propriedade ```"perSiteScaling": true```. aplicativo Hello está definindo Olá **número de trabalhadores** toouse too5 ```"properties": { "numberOfWorkers": "5" }```.

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

## <a name="recommended-configuration-for-high-density-hosting"></a>Configuração recomendada para hospedagem de alta densidade
O dimensionamento por aplicativo é um recurso que está habilitado em regiões globais do Azure e Ambientes do Serviço de Aplicativo. No entanto, Olá recomendado estratégia é usar os ambientes de serviço de aplicativo tootake de seus recursos avançados e pools de saudação maior de capacidade.  

Siga estas etapas tooconfigure alta densidade de hospedagem para seus aplicativos:

1. Configurar Olá ambiente de serviço de aplicativo e escolha um pool de trabalho que é dedicado toohello alta densidade do cenário de hospedagem.
1. Criar um único plano de serviço de aplicativo e dimensioná-lo toouse todos Olá capacidade disponível no pool do trabalhador hello.
1. Defina Olá PerSiteScaling sinalizador tootrue em Olá plano de serviço de aplicativo.
1. Novos aplicativos são criados e atribuídos toothat plano de serviço de aplicativo com o **numberOfWorkers** propriedade definida muito**1**. Usando essa configuração gera hello mais alta densidade possíveis neste pool de trabalho.
1. número de saudação de trabalhos pode ser configurado independentemente por recursos do aplicativo toogrant adicionais conforme necessário. Por exemplo:
    - Um aplicativo de alto uso pode definir **numberOfWorkers** muito**3** toohave mais capacidade para que o aplicativo de processamento. 
    - Aplicativos de baixo uso definiria **numberOfWorkers** muito**1**.

## <a name="next-steps"></a>Próximas etapas

- [Visão geral detalhada de planos de Serviço de aplicativo do Azure](azure-web-sites-web-hosting-plans-in-depth-overview.md)
- [Introdução tooApp ambiente de serviço](../app-service-web/app-service-app-service-environment-intro.md)
