---
title: aaaProvision aplicativo Web com o Cache Redis
description: Use o aplicativo web do Azure Resource Manager modelo toodeploy com Redis Cache.
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
ms.openlocfilehash: b95b5e230dc40c1157940c2017cba836975b6930
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-plus-redis-cache-using-a-template"></a><span data-ttu-id="cbdfe-103">Criar um aplicativo Web mais o Cache Redis usando um modelo</span><span class="sxs-lookup"><span data-stu-id="cbdfe-103">Create a Web App plus Redis Cache using a template</span></span>
<span data-ttu-id="cbdfe-104">Neste tópico, você aprenderá como toocreate um modelo do Gerenciador de recursos do Azure que implanta um aplicativo Web do Azure com o cache Redis.</span><span class="sxs-lookup"><span data-stu-id="cbdfe-104">In this topic, you will learn how toocreate an Azure Resource Manager template that deploys an Azure Web App with Redis cache.</span></span> <span data-ttu-id="cbdfe-105">Você aprenderá como toodefine quais recursos são implantados e como toodefine parâmetros que são especificados quando a implantação de saudação for executada.</span><span class="sxs-lookup"><span data-stu-id="cbdfe-105">You will learn how toodefine which resources are deployed and how toodefine parameters that are specified when hello deployment is executed.</span></span> <span data-ttu-id="cbdfe-106">Você pode usar este modelo para suas próprias implantações ou personalizá-lo toomeet seus requisitos.</span><span class="sxs-lookup"><span data-stu-id="cbdfe-106">You can use this template for your own deployments, or customize it toomeet your requirements.</span></span>

<span data-ttu-id="cbdfe-107">Para obter mais informações sobre a criação de modelos, consulte [Criação de Modelos do Gerenciador de Recursos do Azure](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="cbdfe-107">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="cbdfe-108">Para o modelo do hello completa, consulte [aplicativo Web com o modelo de Cache Redis](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-with-redis-cache/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="cbdfe-108">For hello complete template, see [Web App with Redis Cache template](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-with-redis-cache/azuredeploy.json).</span></span>

## <a name="what-you-will-deploy"></a><span data-ttu-id="cbdfe-109">O que você implantará</span><span class="sxs-lookup"><span data-stu-id="cbdfe-109">What you will deploy</span></span>
<span data-ttu-id="cbdfe-110">Neste modelo, você implantará:</span><span class="sxs-lookup"><span data-stu-id="cbdfe-110">In this template, you will deploy:</span></span>

* <span data-ttu-id="cbdfe-111">Aplicativo Web do Azure</span><span class="sxs-lookup"><span data-stu-id="cbdfe-111">Azure Web App</span></span>
* <span data-ttu-id="cbdfe-112">Cache Redis do Azure.</span><span class="sxs-lookup"><span data-stu-id="cbdfe-112">Azure Redis Cache.</span></span>

<span data-ttu-id="cbdfe-113">toorun Olá implantação automaticamente, clique em Olá botão a seguir:</span><span class="sxs-lookup"><span data-stu-id="cbdfe-113">toorun hello deployment automatically, click hello following button:</span></span>

<span data-ttu-id="cbdfe-114">[![Implantar tooAzure](./media/cache-web-app-arm-with-redis-cache-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-with-redis-cache%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="cbdfe-114">[![Deploy tooAzure](./media/cache-web-app-arm-with-redis-cache-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-with-redis-cache%2Fazuredeploy.json)</span></span>

## <a name="parameters-toospecify"></a><span data-ttu-id="cbdfe-115">Parâmetros toospecify</span><span class="sxs-lookup"><span data-stu-id="cbdfe-115">Parameters toospecify</span></span>
[!INCLUDE [app-service-web-deploy-web-parameters](../../includes/app-service-web-deploy-web-parameters.md)]

[!INCLUDE [cache-deploy-parameters](../../includes/cache-deploy-parameters.md)]

## <a name="variables-for-names"></a><span data-ttu-id="cbdfe-116">Nomes de variáveis</span><span class="sxs-lookup"><span data-stu-id="cbdfe-116">Variables for names</span></span>
<span data-ttu-id="cbdfe-117">Este modelo usa nomes de tooconstruct de variáveis para os recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="cbdfe-117">This template uses variables tooconstruct names for hello resources.</span></span> <span data-ttu-id="cbdfe-118">Ele usa Olá [uniqueString](../azure-resource-manager/resource-group-template-functions-string.md#uniquestring) tooconstruct um valor com base na id de grupo de recursos de função.</span><span class="sxs-lookup"><span data-stu-id="cbdfe-118">It uses hello [uniqueString](../azure-resource-manager/resource-group-template-functions-string.md#uniquestring) function tooconstruct a value based on the resource group id.</span></span>

    "variables": {
      "hostingPlanName": "[concat('hostingplan', uniqueString(resourceGroup().id))]",
      "webSiteName": "[concat('webSite', uniqueString(resourceGroup().id))]",
      "cacheName": "[concat('cache', uniqueString(resourceGroup().id))]"
    },


## <a name="resources-toodeploy"></a><span data-ttu-id="cbdfe-119">Recursos toodeploy</span><span class="sxs-lookup"><span data-stu-id="cbdfe-119">Resources toodeploy</span></span>
[!INCLUDE [app-service-web-deploy-web-host](../../includes/app-service-web-deploy-web-host.md)]

### <a name="redis-cache"></a><span data-ttu-id="cbdfe-120">Cache Redis</span><span class="sxs-lookup"><span data-stu-id="cbdfe-120">Redis Cache</span></span>
<span data-ttu-id="cbdfe-121">Cria o Cache Redis do Azure que é usado com o aplicativo web de saudação do hello.</span><span class="sxs-lookup"><span data-stu-id="cbdfe-121">Creates hello Azure Redis Cache that is used with hello web app.</span></span> <span data-ttu-id="cbdfe-122">nome de saudação do cache de saudação é especificado no hello **cacheName** variável.</span><span class="sxs-lookup"><span data-stu-id="cbdfe-122">hello name of hello cache is specified in hello **cacheName** variable.</span></span>

<span data-ttu-id="cbdfe-123">modelo Olá cria o cache de saudação em Olá mesmo local que o grupo de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="cbdfe-123">hello template creates hello cache in hello same location as hello resource group.</span></span>

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


### <a name="web-app"></a><span data-ttu-id="cbdfe-124">Aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="cbdfe-124">Web app</span></span>
<span data-ttu-id="cbdfe-125">Cria Olá web aplicativo com o nome especificado no hello **webSiteName** variável.</span><span class="sxs-lookup"><span data-stu-id="cbdfe-125">Creates hello web app with name specified in hello **webSiteName** variable.</span></span>

<span data-ttu-id="cbdfe-126">Observe que o aplicativo web hello está configurado com o aplicativo definindo propriedades que permitem que ele toowork com hello Cache Redis.</span><span class="sxs-lookup"><span data-stu-id="cbdfe-126">Notice that hello web app is configured with app setting properties that enable it toowork with hello Redis Cache.</span></span> <span data-ttu-id="cbdfe-127">Essas configurações de aplicativo são criadas dinamicamente com base nos valores fornecidos durante a implantação.</span><span class="sxs-lookup"><span data-stu-id="cbdfe-127">This app settings are dynamically created based on values provided during deployment.</span></span>

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

## <a name="commands-toorun-deployment"></a><span data-ttu-id="cbdfe-128">Implantação de toorun de comandos</span><span class="sxs-lookup"><span data-stu-id="cbdfe-128">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="cbdfe-129">PowerShell</span><span class="sxs-lookup"><span data-stu-id="cbdfe-129">PowerShell</span></span>
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-with-redis-cache/azuredeploy.json -ResourceGroupName ExampleDeployGroup

### <a name="azure-cli"></a><span data-ttu-id="cbdfe-130">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="cbdfe-130">Azure CLI</span></span>
    azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-with-redis-cache/azuredeploy.json -g ExampleDeployGroup
