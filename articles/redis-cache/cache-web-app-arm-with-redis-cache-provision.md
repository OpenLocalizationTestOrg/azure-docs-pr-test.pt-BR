---
title: Provisionar o aplicativo Web com o Cache Redis
description: Use o modelo do Gerenciador de Recursos do Azure para implantar o aplicativo Web com o Cache Redis.
services: app-service
documentationcenter: 
author: steved0x
manager: erickson-doug
editor: 
ms.assetid: 6e99c71f-ef8e-4570-a307-e4c059e60c35
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: sdanie
ms.openlocfilehash: 810c1cedd4fe0bd6ecdf9bd32dfb241f5f345300
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-web-app-plus-redis-cache-using-a-template"></a><span data-ttu-id="eea99-103">Criar um aplicativo Web mais o Cache Redis usando um modelo</span><span class="sxs-lookup"><span data-stu-id="eea99-103">Create a Web App plus Redis Cache using a template</span></span>
<span data-ttu-id="eea99-104">Neste tópico, você aprenderá como criar um modelo do Gerenciador de Recursos do Azure que implanta um aplicativo Web do Azure com o Cache Redis.</span><span class="sxs-lookup"><span data-stu-id="eea99-104">In this topic, you will learn how to create an Azure Resource Manager template that deploys an Azure Web App with Redis cache.</span></span> <span data-ttu-id="eea99-105">Você aprenderá como definir quais recursos são implantados e como definir os parâmetros que são especificados quando a implantação é executada.</span><span class="sxs-lookup"><span data-stu-id="eea99-105">You will learn how to define which resources are deployed and how to define parameters that are specified when the deployment is executed.</span></span> <span data-ttu-id="eea99-106">Você pode usar este modelo para suas próprias implantações ou personalizá-lo para atender às suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="eea99-106">You can use this template for your own deployments, or customize it to meet your requirements.</span></span>

<span data-ttu-id="eea99-107">Para obter mais informações sobre a criação de modelos, consulte [Criação de Modelos do Gerenciador de Recursos do Azure](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="eea99-107">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="eea99-108">Para obter o modelo completo, consulte [Aplicativo Web com o modelo do Cache Redis](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-with-redis-cache/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="eea99-108">For the complete template, see [Web App with Redis Cache template](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-with-redis-cache/azuredeploy.json).</span></span>

## <a name="what-you-will-deploy"></a><span data-ttu-id="eea99-109">O que você implantará</span><span class="sxs-lookup"><span data-stu-id="eea99-109">What you will deploy</span></span>
<span data-ttu-id="eea99-110">Neste modelo, você implantará:</span><span class="sxs-lookup"><span data-stu-id="eea99-110">In this template, you will deploy:</span></span>

* <span data-ttu-id="eea99-111">Aplicativo Web do Azure</span><span class="sxs-lookup"><span data-stu-id="eea99-111">Azure Web App</span></span>
* <span data-ttu-id="eea99-112">Cache Redis do Azure.</span><span class="sxs-lookup"><span data-stu-id="eea99-112">Azure Redis Cache.</span></span>

<span data-ttu-id="eea99-113">Para executar a implantação automaticamente, clique no seguinte botão:</span><span class="sxs-lookup"><span data-stu-id="eea99-113">To run the deployment automatically, click the following button:</span></span>

<span data-ttu-id="eea99-114">[![Implantar no Azure](./media/cache-web-app-arm-with-redis-cache-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-with-redis-cache%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="eea99-114">[![Deploy to Azure](./media/cache-web-app-arm-with-redis-cache-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-with-redis-cache%2Fazuredeploy.json)</span></span>

## <a name="parameters-to-specify"></a><span data-ttu-id="eea99-115">Parâmetros para especificar</span><span class="sxs-lookup"><span data-stu-id="eea99-115">Parameters to specify</span></span>
[!INCLUDE [app-service-web-deploy-web-parameters](../../includes/app-service-web-deploy-web-parameters.md)]

[!INCLUDE [cache-deploy-parameters](../../includes/cache-deploy-parameters.md)]

## <a name="variables-for-names"></a><span data-ttu-id="eea99-116">Nomes de variáveis</span><span class="sxs-lookup"><span data-stu-id="eea99-116">Variables for names</span></span>
<span data-ttu-id="eea99-117">Este modelo usa variáveis para construir nomes para os recursos.</span><span class="sxs-lookup"><span data-stu-id="eea99-117">This template uses variables to construct names for the resources.</span></span> <span data-ttu-id="eea99-118">Ele usa a função [uniqueString](../azure-resource-manager/resource-group-template-functions-string.md#uniquestring) para construir um valor com base na ID de grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="eea99-118">It uses the [uniqueString](../azure-resource-manager/resource-group-template-functions-string.md#uniquestring) function to construct a value based on the resource group id.</span></span>

    "variables": {
      "hostingPlanName": "[concat('hostingplan', uniqueString(resourceGroup().id))]",
      "webSiteName": "[concat('webSite', uniqueString(resourceGroup().id))]",
      "cacheName": "[concat('cache', uniqueString(resourceGroup().id))]"
    },


## <a name="resources-to-deploy"></a><span data-ttu-id="eea99-119">Recursos a implantar</span><span class="sxs-lookup"><span data-stu-id="eea99-119">Resources to deploy</span></span>
[!INCLUDE [app-service-web-deploy-web-host](../../includes/app-service-web-deploy-web-host.md)]

### <a name="redis-cache"></a><span data-ttu-id="eea99-120">Cache Redis</span><span class="sxs-lookup"><span data-stu-id="eea99-120">Redis Cache</span></span>
<span data-ttu-id="eea99-121">Cria o Cache Redis do Azure que é usado com o aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="eea99-121">Creates the Azure Redis Cache that is used with the web app.</span></span> <span data-ttu-id="eea99-122">O nome do cache é especificado na variável **cacheName** .</span><span class="sxs-lookup"><span data-stu-id="eea99-122">The name of the cache is specified in the **cacheName** variable.</span></span>

<span data-ttu-id="eea99-123">O modelo cria o cache no mesmo local que o grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="eea99-123">The template creates the cache in the same location as the resource group.</span></span>

    {
      "name": "[variables('cacheName')]",
      "type": "Microsoft.Cache/Redis",
      "location": "[resourceGroup().location]",
      "apiVersion": "2015-08-01",
      "dependsOn": [ ],
      "tags": {
        "displayName": "cache"
      },
      "properties": {
        "sku": {
          "name": "[parameters('cacheSKUName')]",
          "family": "[parameters('cacheSKUFamily')]",
          "capacity": "[parameters('cacheSKUCapacity')]"
        }
      }
    }


### <a name="web-app"></a><span data-ttu-id="eea99-124">Aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="eea99-124">Web app</span></span>
<span data-ttu-id="eea99-125">Cria o aplicativo Web com o nome especificado na variável **webSiteName** .</span><span class="sxs-lookup"><span data-stu-id="eea99-125">Creates the web app with name specified in the **webSiteName** variable.</span></span>

<span data-ttu-id="eea99-126">Observe que o aplicativo Web está configurado com as propriedades de configuração de aplicativo que o habilitam a trabalhar com o Cache Redis.</span><span class="sxs-lookup"><span data-stu-id="eea99-126">Notice that the web app is configured with app setting properties that enable it to work with the Redis Cache.</span></span> <span data-ttu-id="eea99-127">Essas configurações de aplicativo são criadas dinamicamente com base nos valores fornecidos durante a implantação.</span><span class="sxs-lookup"><span data-stu-id="eea99-127">This app settings are dynamically created based on values provided during deployment.</span></span>

    {
      "apiVersion": "2015-08-01",
      "name": "[variables('webSiteName')]",
      "type": "Microsoft.Web/sites",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Web/serverFarms/', variables('hostingPlanName'))]",
        "[concat('Microsoft.Cache/Redis/', variables('cacheName'))]"
      ],
      "tags": {
        "[concat('hidden-related:', resourceGroup().id, '/providers/Microsoft.Web/serverfarms/', variables('hostingPlanName'))]": "empty",
        "displayName": "Website"
      },
      "properties": {
        "name": "[variables('webSiteName')]",
        "serverFarmId": "[resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName'))]"
      },
      "resources": [
        {
          "apiVersion": "2015-08-01",
          "type": "config",
          "name": "appsettings",
          "dependsOn": [
            "[concat('Microsoft.Web/Sites/', variables('webSiteName'))]",
            "[concat('Microsoft.Cache/Redis/', variables('cacheName'))]"
          ],
          "properties": {
            "CacheConnection": "[concat(variables('cacheName'),'.redis.cache.windows.net,abortConnect=false,ssl=true,password=', listKeys(resourceId('Microsoft.Cache/Redis', variables('cacheName')), '2015-08-01').primaryKey)]"
          }
        }
      ]
    }

## <a name="commands-to-run-deployment"></a><span data-ttu-id="eea99-128">Comandos para executar a implantação</span><span class="sxs-lookup"><span data-stu-id="eea99-128">Commands to run deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="eea99-129">PowerShell</span><span class="sxs-lookup"><span data-stu-id="eea99-129">PowerShell</span></span>
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-with-redis-cache/azuredeploy.json -ResourceGroupName ExampleDeployGroup

### <a name="azure-cli"></a><span data-ttu-id="eea99-130">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="eea99-130">Azure CLI</span></span>
    azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-with-redis-cache/azuredeploy.json -g ExampleDeployGroup
