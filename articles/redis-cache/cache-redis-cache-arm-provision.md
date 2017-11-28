---
title: aaaProvision um Cache Redis usando o Gerenciador de recursos do Azure | Microsoft Docs
description: Use o Gerenciador de recursos do Azure modelo toodeploy um Cache Redis do Azure.
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
ms.openlocfilehash: 46e7b3b2493ac51dbe6bab0b086304802afc5d48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-redis-cache-using-a-template"></a><span data-ttu-id="270fb-103">Criar um Cache Redis usando um modelo</span><span class="sxs-lookup"><span data-stu-id="270fb-103">Create a Redis Cache using a template</span></span>
<span data-ttu-id="270fb-104">Neste tópico, você aprenderá como toocreate um modelo do Gerenciador de recursos do Azure que implanta um Azure Redis Cache.</span><span class="sxs-lookup"><span data-stu-id="270fb-104">In this topic, you learn how toocreate an Azure Resource Manager template that deploys an Azure Redis Cache.</span></span> <span data-ttu-id="270fb-105">cache de saudação pode ser usado com armazenamento conta tookeep diagnóstico dados existentes.</span><span class="sxs-lookup"><span data-stu-id="270fb-105">hello cache can be used with an existing storage account tookeep diagnostic data.</span></span> <span data-ttu-id="270fb-106">Você também aprenderá como toodefine quais recursos são implantados e como toodefine parâmetros que são especificados quando a implantação de saudação for executada.</span><span class="sxs-lookup"><span data-stu-id="270fb-106">You also learn how toodefine which resources are deployed and how toodefine parameters that are specified when hello deployment is executed.</span></span> <span data-ttu-id="270fb-107">Você pode usar este modelo para suas próprias implantações ou personalizá-lo toomeet seus requisitos.</span><span class="sxs-lookup"><span data-stu-id="270fb-107">You can use this template for your own deployments, or customize it toomeet your requirements.</span></span>

<span data-ttu-id="270fb-108">Atualmente, as configurações de diagnóstico são compartilhadas para todos os caches em Olá mesma região para uma assinatura.</span><span class="sxs-lookup"><span data-stu-id="270fb-108">Currently, diagnostic settings are shared for all caches in hello same region for a subscription.</span></span> <span data-ttu-id="270fb-109">A atualização de um cache na região Olá afeta todos os outros caches na região de saudação.</span><span class="sxs-lookup"><span data-stu-id="270fb-109">Updating one cache in hello region affects all other caches in hello region.</span></span>

<span data-ttu-id="270fb-110">Para obter mais informações sobre a criação de modelos, consulte [Criação de Modelos do Gerenciador de Recursos do Azure](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="270fb-110">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="270fb-111">Para o modelo do hello completa, consulte [Redis Cache modelo](https://github.com/Azure/azure-quickstart-templates/blob/master/101-redis-cache/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="270fb-111">For hello complete template, see [Redis Cache template](https://github.com/Azure/azure-quickstart-templates/blob/master/101-redis-cache/azuredeploy.json).</span></span>

> [!NOTE]
> <span data-ttu-id="270fb-112">Modelos do Gerenciador de recursos para Olá novo [camada Premium](cache-premium-tier-intro.md) estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="270fb-112">Resource Manager templates for hello new [Premium tier](cache-premium-tier-intro.md) are available.</span></span> 
> 
> * [<span data-ttu-id="270fb-113">Criar um cache Redis Premium com clustering</span><span class="sxs-lookup"><span data-stu-id="270fb-113">Create a Premium Redis Cache with clustering</span></span>](https://azure.microsoft.com/documentation/templates/201-redis-premium-cluster-diagnostics/)
> * [<span data-ttu-id="270fb-114">Criar um cache Redis Premium com persistência de dados</span><span class="sxs-lookup"><span data-stu-id="270fb-114">Create Premium Redis Cache with data persistence</span></span>](https://azure.microsoft.com/documentation/templates/201-redis-premium-persistence/)
> * [<span data-ttu-id="270fb-115">Criar um cache Redis Premium com VNet e clustering opcional</span><span class="sxs-lookup"><span data-stu-id="270fb-115">Create Premium Redis Cache with VNet and optional clustering</span></span>](https://azure.microsoft.com/documentation/templates/201-redis-premium-vnet-cluster-diagnostics/)
> 
> <span data-ttu-id="270fb-116">toocheck para os modelos mais recentes do hello, consulte [modelos de início rápido do Azure](https://azure.microsoft.com/documentation/templates/) e procure `Redis Cache`.</span><span class="sxs-lookup"><span data-stu-id="270fb-116">toocheck for hello latest templates, see [Azure Quickstart Templates](https://azure.microsoft.com/documentation/templates/) and search for `Redis Cache`.</span></span>
> 
> 

## <a name="what-you-will-deploy"></a><span data-ttu-id="270fb-117">O que você implantará</span><span class="sxs-lookup"><span data-stu-id="270fb-117">What you will deploy</span></span>
<span data-ttu-id="270fb-118">Neste modelo, você implantará um Cache Redis do Azure que usa uma conta de armazenamento existente para os dados de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="270fb-118">In this template, you will deploy an Azure Redis Cache that uses an existing storage account for diagnostic data.</span></span>

<span data-ttu-id="270fb-119">toorun Olá implantação automaticamente, clique em Olá botão a seguir:</span><span class="sxs-lookup"><span data-stu-id="270fb-119">toorun hello deployment automatically, click hello following button:</span></span>

<span data-ttu-id="270fb-120">[![Implantar tooAzure](./media/cache-redis-cache-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-redis-cache%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="270fb-120">[![Deploy tooAzure](./media/cache-redis-cache-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-redis-cache%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="270fb-121">parâmetros</span><span class="sxs-lookup"><span data-stu-id="270fb-121">Parameters</span></span>
<span data-ttu-id="270fb-122">No Gerenciador de recursos do Azure, você define parâmetros para os valores desejados toospecify quando Olá modelo é implantado.</span><span class="sxs-lookup"><span data-stu-id="270fb-122">With Azure Resource Manager, you define parameters for values you want toospecify when hello template is deployed.</span></span> <span data-ttu-id="270fb-123">modelo de saudação inclui uma seção chamada parâmetros que contém todos os valores de parâmetro hello.</span><span class="sxs-lookup"><span data-stu-id="270fb-123">hello template includes a section called Parameters that contains all of hello parameter values.</span></span>
<span data-ttu-id="270fb-124">Você deve definir um parâmetro para os valores que variam com base no projeto Olá que estiver implantando ou com base no ambiente de saudação que você está implantando.</span><span class="sxs-lookup"><span data-stu-id="270fb-124">You should define a parameter for those values that vary based on hello project you are deploying or based on hello environment you are deploying to.</span></span> <span data-ttu-id="270fb-125">Não defina parâmetros para valores que permanecem sempre Olá mesmo.</span><span class="sxs-lookup"><span data-stu-id="270fb-125">Do not define parameters for values that always stay hello same.</span></span> <span data-ttu-id="270fb-126">Cada valor de parâmetro é usado em Olá modelo toodefine Olá recursos implantados.</span><span class="sxs-lookup"><span data-stu-id="270fb-126">Each parameter value is used in hello template toodefine hello resources that are deployed.</span></span> 

[!INCLUDE [app-service-web-deploy-redis-parameters](../../includes/cache-deploy-parameters.md)]

### <a name="rediscachelocation"></a><span data-ttu-id="270fb-127">redisCacheLocation</span><span class="sxs-lookup"><span data-stu-id="270fb-127">redisCacheLocation</span></span>
<span data-ttu-id="270fb-128">local de saudação do hello Cache Redis.</span><span class="sxs-lookup"><span data-stu-id="270fb-128">hello location of hello Redis Cache.</span></span> <span data-ttu-id="270fb-129">Para melhor desempenho, use Olá mesmo local como Olá toobe aplicativo usado com o cache de saudação.</span><span class="sxs-lookup"><span data-stu-id="270fb-129">For best performance, use hello same location as hello app toobe used with hello cache.</span></span>

    "redisCacheLocation": {
      "type": "string"
    }

### <a name="existingdiagnosticsstorageaccountname"></a><span data-ttu-id="270fb-130">existingDiagnosticsStorageAccountName</span><span class="sxs-lookup"><span data-stu-id="270fb-130">existingDiagnosticsStorageAccountName</span></span>
<span data-ttu-id="270fb-131">nome de saudação do Olá existente toouse de conta de armazenamento para diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="270fb-131">hello name of hello existing storage account toouse for diagnostics.</span></span> 

    "existingDiagnosticsStorageAccountName": {
      "type": "string"
    }

### <a name="enablenonsslport"></a><span data-ttu-id="270fb-132">enableNonSslPort</span><span class="sxs-lookup"><span data-stu-id="270fb-132">enableNonSslPort</span></span>
<span data-ttu-id="270fb-133">Um valor booliano que indica se tooallow acessar por meio de portas não SSL.</span><span class="sxs-lookup"><span data-stu-id="270fb-133">A boolean value that indicates whether tooallow access via non-SSL ports.</span></span>

    "enableNonSslPort": {
      "type": "bool"
    }

### <a name="diagnosticsstatus"></a><span data-ttu-id="270fb-134">diagnosticsStatus</span><span class="sxs-lookup"><span data-stu-id="270fb-134">diagnosticsStatus</span></span>
<span data-ttu-id="270fb-135">Um valor que indica se o diagnóstico está habilitado.</span><span class="sxs-lookup"><span data-stu-id="270fb-135">A value that indicates whether diagnostics is enabled.</span></span> <span data-ttu-id="270fb-136">Use ATIVAR ou DESATIVAR.</span><span class="sxs-lookup"><span data-stu-id="270fb-136">Use ON or OFF.</span></span>

    "diagnosticsStatus": {
      "type": "string",
      "defaultValue": "ON",
      "allowedValues": [
            "ON",
            "OFF"
        ]
    }

## <a name="resources-toodeploy"></a><span data-ttu-id="270fb-137">Recursos toodeploy</span><span class="sxs-lookup"><span data-stu-id="270fb-137">Resources toodeploy</span></span>
### <a name="redis-cache"></a><span data-ttu-id="270fb-138">Cache Redis</span><span class="sxs-lookup"><span data-stu-id="270fb-138">Redis Cache</span></span>
<span data-ttu-id="270fb-139">Cria Olá Cache Redis do Azure.</span><span class="sxs-lookup"><span data-stu-id="270fb-139">Creates hello Azure Redis Cache.</span></span>

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



## <a name="commands-toorun-deployment"></a><span data-ttu-id="270fb-140">Implantação de toorun de comandos</span><span class="sxs-lookup"><span data-stu-id="270fb-140">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="270fb-141">PowerShell</span><span class="sxs-lookup"><span data-stu-id="270fb-141">PowerShell</span></span>
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-redis-cache/azuredeploy.json -ResourceGroupName ExampleDeployGroup -redisCacheName ExampleCache

### <a name="azure-cli"></a><span data-ttu-id="270fb-142">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="270fb-142">Azure CLI</span></span>
    azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-redis-cache/azuredeploy.json -g ExampleDeployGroup


