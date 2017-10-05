---
title: Provisionar um Cache Redis usando o Azure Resource Manager | Microsoft Docs
description: Use o modelo do Gerenciador de Recursos do Azure para implantar um Cache Redis do Azure.
services: app-service
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: ce6f5372-7038-4655-b1c5-108f7c148282
ms.service: cache
ms.workload: web
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: sdanie
ms.openlocfilehash: cce5d63e8bad2dd066cb4c28e2a8a9cb16c47953
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-redis-cache-using-a-template"></a><span data-ttu-id="25621-103">Criar um Cache Redis usando um modelo</span><span class="sxs-lookup"><span data-stu-id="25621-103">Create a Redis Cache using a template</span></span>
<span data-ttu-id="25621-104">Neste tópico, você aprende a criar um modelo do Aure Resource Manager que implanta um aplicativo Cache Redis do Azure.</span><span class="sxs-lookup"><span data-stu-id="25621-104">In this topic, you learn how to create an Azure Resource Manager template that deploys an Azure Redis Cache.</span></span> <span data-ttu-id="25621-105">O cache pode ser usado com uma conta de armazenamento existente para manter os dados de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="25621-105">The cache can be used with an existing storage account to keep diagnostic data.</span></span> <span data-ttu-id="25621-106">Você também aprende como definir quais recursos são implantados e como definir os parâmetros que são especificados quando a implantação é executada.</span><span class="sxs-lookup"><span data-stu-id="25621-106">You also learn how to define which resources are deployed and how to define parameters that are specified when the deployment is executed.</span></span> <span data-ttu-id="25621-107">Você pode usar este modelo para suas próprias implantações ou personalizá-lo para atender às suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="25621-107">You can use this template for your own deployments, or customize it to meet your requirements.</span></span>

<span data-ttu-id="25621-108">Atualmente, as configurações de diagnóstico são compartilhadas por todos os caches na mesma região de uma assinatura.</span><span class="sxs-lookup"><span data-stu-id="25621-108">Currently, diagnostic settings are shared for all caches in the same region for a subscription.</span></span> <span data-ttu-id="25621-109">A atualização de um cache na região afeta todos os outros caches na região.</span><span class="sxs-lookup"><span data-stu-id="25621-109">Updating one cache in the region affects all other caches in the region.</span></span>

<span data-ttu-id="25621-110">Para obter mais informações sobre a criação de modelos, consulte [Criação de Modelos do Gerenciador de Recursos do Azure](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="25621-110">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="25621-111">Para obter o modelo completo, confira [Modelo do Cache Redis](https://github.com/Azure/azure-quickstart-templates/blob/master/101-redis-cache/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="25621-111">For the complete template, see [Redis Cache template](https://github.com/Azure/azure-quickstart-templates/blob/master/101-redis-cache/azuredeploy.json).</span></span>

> [!NOTE]
> <span data-ttu-id="25621-112">Os modelos do Resource Manager para a nova [camada Premium](cache-premium-tier-intro.md) estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="25621-112">Resource Manager templates for the new [Premium tier](cache-premium-tier-intro.md) are available.</span></span> 
> 
> * [<span data-ttu-id="25621-113">Criar um cache Redis Premium com clustering</span><span class="sxs-lookup"><span data-stu-id="25621-113">Create a Premium Redis Cache with clustering</span></span>](https://azure.microsoft.com/documentation/templates/201-redis-premium-cluster-diagnostics/)
> * [<span data-ttu-id="25621-114">Criar um cache Redis Premium com persistência de dados</span><span class="sxs-lookup"><span data-stu-id="25621-114">Create Premium Redis Cache with data persistence</span></span>](https://azure.microsoft.com/documentation/templates/201-redis-premium-persistence/)
> * [<span data-ttu-id="25621-115">Criar um cache Redis Premium com VNet e clustering opcional</span><span class="sxs-lookup"><span data-stu-id="25621-115">Create Premium Redis Cache with VNet and optional clustering</span></span>](https://azure.microsoft.com/documentation/templates/201-redis-premium-vnet-cluster-diagnostics/)
> 
> <span data-ttu-id="25621-116">Para verificar os modelos mais recentes, consulte [Modelos de início rápido do Azure](https://azure.microsoft.com/documentation/templates/) e procure por `Redis Cache`.</span><span class="sxs-lookup"><span data-stu-id="25621-116">To check for the latest templates, see [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates/) and search for `Redis Cache`.</span></span>
> 
> 

## <a name="what-you-will-deploy"></a><span data-ttu-id="25621-117">O que você implantará</span><span class="sxs-lookup"><span data-stu-id="25621-117">What you will deploy</span></span>
<span data-ttu-id="25621-118">Neste modelo, você implantará um Cache Redis do Azure que usa uma conta de armazenamento existente para os dados de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="25621-118">In this template, you will deploy an Azure Redis Cache that uses an existing storage account for diagnostic data.</span></span>

<span data-ttu-id="25621-119">Para executar a implantação automaticamente, clique no seguinte botão:</span><span class="sxs-lookup"><span data-stu-id="25621-119">To run the deployment automatically, click the following button:</span></span>

<span data-ttu-id="25621-120">[![Implantar no Azure](./media/cache-redis-cache-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-redis-cache%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="25621-120">[![Deploy to Azure](./media/cache-redis-cache-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-redis-cache%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="25621-121">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="25621-121">Parameters</span></span>
<span data-ttu-id="25621-122">Com o Gerenciador de Recursos do Azure, você define parâmetros para os valores que deseja especificar quando o modelo é implantado.</span><span class="sxs-lookup"><span data-stu-id="25621-122">With Azure Resource Manager, you define parameters for values you want to specify when the template is deployed.</span></span> <span data-ttu-id="25621-123">O modelo inclui uma seção chamada Parâmetros, que contém todos os valores de parâmetro.</span><span class="sxs-lookup"><span data-stu-id="25621-123">The template includes a section called Parameters that contains all of the parameter values.</span></span>
<span data-ttu-id="25621-124">Você deve definir um parâmetro para os valores que variam de acordo com o projeto que você está implantando ou com o ambiente em que a implantação ocorre.</span><span class="sxs-lookup"><span data-stu-id="25621-124">You should define a parameter for those values that vary based on the project you are deploying or based on the environment you are deploying to.</span></span> <span data-ttu-id="25621-125">Não defina parâmetros para valores que permanecem sempre os mesmos.</span><span class="sxs-lookup"><span data-stu-id="25621-125">Do not define parameters for values that always stay the same.</span></span> <span data-ttu-id="25621-126">Cada valor de parâmetro é usado no modelo para definir os recursos que são implantados.</span><span class="sxs-lookup"><span data-stu-id="25621-126">Each parameter value is used in the template to define the resources that are deployed.</span></span> 

[!INCLUDE [app-service-web-deploy-redis-parameters](../../includes/cache-deploy-parameters.md)]

### <a name="rediscachelocation"></a><span data-ttu-id="25621-127">redisCacheLocation</span><span class="sxs-lookup"><span data-stu-id="25621-127">redisCacheLocation</span></span>
<span data-ttu-id="25621-128">A localização do Cache Redis.</span><span class="sxs-lookup"><span data-stu-id="25621-128">The location of the Redis Cache.</span></span> <span data-ttu-id="25621-129">Para obter o melhor desempenho, use o mesmo local que o aplicativo a ser usado com o cache.</span><span class="sxs-lookup"><span data-stu-id="25621-129">For best performance, use the same location as the app to be used with the cache.</span></span>

    "redisCacheLocation": {
      "type": "string"
    }

### <a name="existingdiagnosticsstorageaccountname"></a><span data-ttu-id="25621-130">existingDiagnosticsStorageAccountName</span><span class="sxs-lookup"><span data-stu-id="25621-130">existingDiagnosticsStorageAccountName</span></span>
<span data-ttu-id="25621-131">O nome da conta de armazenamento existente a ser usada para o diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="25621-131">The name of the existing storage account to use for diagnostics.</span></span> 

    "existingDiagnosticsStorageAccountName": {
      "type": "string"
    }

### <a name="enablenonsslport"></a><span data-ttu-id="25621-132">enableNonSslPort</span><span class="sxs-lookup"><span data-stu-id="25621-132">enableNonSslPort</span></span>
<span data-ttu-id="25621-133">Um valor booliano que indica a permissão de acesso por meio de portas não SSL.</span><span class="sxs-lookup"><span data-stu-id="25621-133">A boolean value that indicates whether to allow access via non-SSL ports.</span></span>

    "enableNonSslPort": {
      "type": "bool"
    }

### <a name="diagnosticsstatus"></a><span data-ttu-id="25621-134">diagnosticsStatus</span><span class="sxs-lookup"><span data-stu-id="25621-134">diagnosticsStatus</span></span>
<span data-ttu-id="25621-135">Um valor que indica se o diagnóstico está habilitado.</span><span class="sxs-lookup"><span data-stu-id="25621-135">A value that indicates whether diagnostics is enabled.</span></span> <span data-ttu-id="25621-136">Use ATIVAR ou DESATIVAR.</span><span class="sxs-lookup"><span data-stu-id="25621-136">Use ON or OFF.</span></span>

    "diagnosticsStatus": {
      "type": "string",
      "defaultValue": "ON",
      "allowedValues": [
            "ON",
            "OFF"
        ]
    }

## <a name="resources-to-deploy"></a><span data-ttu-id="25621-137">Recursos a implantar</span><span class="sxs-lookup"><span data-stu-id="25621-137">Resources to deploy</span></span>
### <a name="redis-cache"></a><span data-ttu-id="25621-138">Cache Redis</span><span class="sxs-lookup"><span data-stu-id="25621-138">Redis Cache</span></span>
<span data-ttu-id="25621-139">Cria o Cache Redis do Azure.</span><span class="sxs-lookup"><span data-stu-id="25621-139">Creates the Azure Redis Cache.</span></span>

    {
      "apiVersion": "2015-08-01",
      "name": "[parameters('redisCacheName')]",
      "type": "Microsoft.Cache/Redis",
      "location": "[parameters('redisCacheLocation')]",
      "properties": {
        "enableNonSslPort": "[parameters('enableNonSslPort')]",
        "sku": {
          "capacity": "[parameters('redisCacheCapacity')]",
          "family": "[parameters('redisCacheFamily')]",
          "name": "[parameters('redisCacheSKU')]"
        }
      },
      "resources": [
        {
          "apiVersion": "2015-07-01",
          "type": "Microsoft.Cache/redis/providers/diagnosticsettings",
          "name": "[concat(parameters('redisCacheName'), '/Microsoft.Insights/service')]",
          "location": "[parameters('redisCacheLocation')]",
          "dependsOn": [
            "[concat('Microsoft.Cache/Redis/', parameters('redisCacheName'))]"
          ],
          "properties": {
            "status": "[parameters('diagnosticsStatus')]",
            "storageAccountName": "[parameters('existingDiagnosticsStorageAccountName')]"
          }
        }
      ]
    }



## <a name="commands-to-run-deployment"></a><span data-ttu-id="25621-140">Comandos para executar a implantação</span><span class="sxs-lookup"><span data-stu-id="25621-140">Commands to run deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="25621-141">PowerShell</span><span class="sxs-lookup"><span data-stu-id="25621-141">PowerShell</span></span>
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-redis-cache/azuredeploy.json -ResourceGroupName ExampleDeployGroup -redisCacheName ExampleCache

### <a name="azure-cli"></a><span data-ttu-id="25621-142">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="25621-142">Azure CLI</span></span>
    azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-redis-cache/azuredeploy.json -g ExampleDeployGroup


