---
title: "Automatizar a implantação de recursos para um aplicativo de funções do Azure Functions | Microsoft Docs"
description: "Aprenda a criar um modelo do Azure Resource Manager que implanta o aplicativo de funções."
services: Functions
documtationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: "azure functions, funções, arquitetura sem servidores, infraestrutura como código, azure resource manager"
ms.assetid: d20743e3-aab6-442c-a836-9bcea09bfd32
ms.server: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/25/2017
ms.author: glenga
ms.openlocfilehash: 15496e4ab2858b2aa319d53f1c438a259a3d5e49
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="automate-resource-deployment-for-your-function-app-in-azure-functions"></a><span data-ttu-id="2f3d8-104">Automatizar a implantação de recursos para seu aplicativo de funções do Azure Functions</span><span class="sxs-lookup"><span data-stu-id="2f3d8-104">Automate resource deployment for your function app in Azure Functions</span></span>

<span data-ttu-id="2f3d8-105">Você pode usar um modelo do Azure Resource Manager para implantar um aplicativo de funções.</span><span class="sxs-lookup"><span data-stu-id="2f3d8-105">You can use an Azure Resource Manager template to deploy a function app.</span></span> <span data-ttu-id="2f3d8-106">Este artigo descreve os recursos e os parâmetros necessários para fazer isso.</span><span class="sxs-lookup"><span data-stu-id="2f3d8-106">This article outlines the required resources and parameters for doing so.</span></span> <span data-ttu-id="2f3d8-107">Talvez seja necessário implantar recursos adicionais, dependendo dos [gatilhos e associações](functions-triggers-bindings.md) em seu aplicativo de funções.</span><span class="sxs-lookup"><span data-stu-id="2f3d8-107">You might need to deploy additional resources, depending on the [triggers and bindings](functions-triggers-bindings.md) in your function app.</span></span>

<span data-ttu-id="2f3d8-108">Para saber mais sobre a criação de modelos, consulte [Criação de modelos do Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="2f3d8-108">For more information about creating templates, see [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="2f3d8-109">Para modelos de exemplo, consulte:</span><span class="sxs-lookup"><span data-stu-id="2f3d8-109">For sample templates, see:</span></span>
- <span data-ttu-id="2f3d8-110">[Aplicativo de funções no Plano de Consumo]</span><span class="sxs-lookup"><span data-stu-id="2f3d8-110">[Function app on Consumption plan]</span></span>
- <span data-ttu-id="2f3d8-111">[Aplicativo de funções no Plano do Serviço de Aplicativo do Azure]</span><span class="sxs-lookup"><span data-stu-id="2f3d8-111">[Function app on Azure App Service plan]</span></span>

## <a name="required-resources"></a><span data-ttu-id="2f3d8-112">Recursos necessários</span><span class="sxs-lookup"><span data-stu-id="2f3d8-112">Required resources</span></span>

<span data-ttu-id="2f3d8-113">Um aplicativo de funções requer estes recursos:</span><span class="sxs-lookup"><span data-stu-id="2f3d8-113">A function app requires these resources:</span></span>

* <span data-ttu-id="2f3d8-114">Uma conta de [Armazenamento do Azure](../storage/index.md)</span><span class="sxs-lookup"><span data-stu-id="2f3d8-114">An [Azure Storage](../storage/index.md) account</span></span>
* <span data-ttu-id="2f3d8-115">Um plano de hospedagem (Plano de Consumo ou Plano do Serviço de Aplicativo)</span><span class="sxs-lookup"><span data-stu-id="2f3d8-115">A hosting plan (Consumption plan or App Service plan)</span></span>
* <span data-ttu-id="2f3d8-116">Um aplicativo de funções</span><span class="sxs-lookup"><span data-stu-id="2f3d8-116">A function app</span></span> 

### <a name="storage-account"></a><span data-ttu-id="2f3d8-117">Conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="2f3d8-117">Storage account</span></span>

<span data-ttu-id="2f3d8-118">Uma conta de armazenamento do Azure é necessária para um aplicativo de funções.</span><span class="sxs-lookup"><span data-stu-id="2f3d8-118">An Azure storage account is required for a function app.</span></span> <span data-ttu-id="2f3d8-119">Você precisa de uma conta de finalidade geral que dá suporte a blobs, tabelas, consultas e arquivos.</span><span class="sxs-lookup"><span data-stu-id="2f3d8-119">You need a general purpose account that supports blobs, tables, queues, and files.</span></span> <span data-ttu-id="2f3d8-120">Para saber mais, confira [Requisitos da conta de armazenamento do Azure Functions](functions-create-function-app-portal.md#storage-account-requirements).</span><span class="sxs-lookup"><span data-stu-id="2f3d8-120">For more information, see [Azure Functions storage account requirements](functions-create-function-app-portal.md#storage-account-requirements).</span></span>

```json
{
    "type": "Microsoft.Storage/storageAccounts",
    "name": "[variables('storageAccountName')]",
    "apiVersion": "2015-06-15",
    "location": "[resourceGroup().location]",
    "properties": {
        "accountType": "[parameters('storageAccountType')]"
    }
}
```

<span data-ttu-id="2f3d8-121">Além disso, as propriedades `AzureWebJobsStorage` e `AzureWebJobsDashboard` devem ser especificadas como configurações de aplicativo na configuração do site.</span><span class="sxs-lookup"><span data-stu-id="2f3d8-121">In addition, the properties `AzureWebJobsStorage` and `AzureWebJobsDashboard` must be specified as app settings in the site configuration.</span></span> <span data-ttu-id="2f3d8-122">O tempo de execução do Azure Functions usa a cadeia de conexão `AzureWebJobsStorage` para criar filas internas.</span><span class="sxs-lookup"><span data-stu-id="2f3d8-122">The Azure Functions runtime uses the `AzureWebJobsStorage` connection string to create internal queues.</span></span> <span data-ttu-id="2f3d8-123">A cadeia de conexão `AzureWebJobsDashboard` é usada para fazer logon no armazenamento de Tabelas do Azure e alimentar a guia **Monitorar** no portal.</span><span class="sxs-lookup"><span data-stu-id="2f3d8-123">The connection string `AzureWebJobsDashboard` is used to log to Azure Table storage and power the **Monitor** tab in the portal.</span></span>

<span data-ttu-id="2f3d8-124">Essas propriedades são especificadas na coleção `appSettings` no objeto `siteConfig`:</span><span class="sxs-lookup"><span data-stu-id="2f3d8-124">These properties are specified in the `appSettings` collection in the `siteConfig` object:</span></span>

```json
"appSettings": [
    {
        "name": "AzureWebJobsStorage",
        "value": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
    },
    {
        "name": "AzureWebJobsDashboard",
        "value": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
    }
```    

### <a name="hosting-plan"></a><span data-ttu-id="2f3d8-125">Plano de hospedagem</span><span class="sxs-lookup"><span data-stu-id="2f3d8-125">Hosting plan</span></span>

<span data-ttu-id="2f3d8-126">A definição do plano de hospedagem varia, dependendo se você usa um Plano do Serviço de Aplicativo ou de Consumo.</span><span class="sxs-lookup"><span data-stu-id="2f3d8-126">The definition of the hosting plan varies, depending on whether you use a Consumption or App Service plan.</span></span> <span data-ttu-id="2f3d8-127">Consulte [Implantar um aplicativo de funções no Plano de Consumo](#consumption) e [Implantar um aplicativo de funções no Plano do Serviço de Aplicativo](#app-service-plan).</span><span class="sxs-lookup"><span data-stu-id="2f3d8-127">See [Deploy a function app on the Consumption plan](#consumption) and [Deploy a function app on the App Service plan](#app-service-plan).</span></span>

### <a name="function-app"></a><span data-ttu-id="2f3d8-128">Aplicativo de funções</span><span class="sxs-lookup"><span data-stu-id="2f3d8-128">Function app</span></span>

<span data-ttu-id="2f3d8-129">O recurso do aplicativo de funções é definido usando um recurso do tipo **Microsoft.Web/Site** e variante **functionapp**:</span><span class="sxs-lookup"><span data-stu-id="2f3d8-129">The function app resource is defined by using a resource of type **Microsoft.Web/Site** and kind **functionapp**:</span></span>

```json
{
    "apiVersion": "2015-08-01",
    "type": "Microsoft.Web/sites",
    "name": "[variables('functionAppName')]",
    "location": "[resourceGroup().location]",
    "kind": "functionapp",            
    "dependsOn": [
        "[resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName'))]",
        "[resourceId('Microsoft.Storage/storageAccounts', variables('storageAccountName'))]"
    ]
```

<a name="consumption"></a>

## <a name="deploy-a-function-app-on-the-consumption-plan"></a><span data-ttu-id="2f3d8-130">Implantar um aplicativo de funções no Plano de Consumo</span><span class="sxs-lookup"><span data-stu-id="2f3d8-130">Deploy a function app on the Consumption plan</span></span>

<span data-ttu-id="2f3d8-131">Você pode executar um aplicativo de funções em dois modos diferentes: o Plano de Consumo e o Plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2f3d8-131">You can run a function app in two different modes: the Consumption plan and the App Service plan.</span></span> <span data-ttu-id="2f3d8-132">O Plano de Consumo automaticamente aloca potência de computação quando seu código está em execução, escala horizontalmente conforme a necessidade para tratar do carregamento e reduz verticalmente quando o código não está em execução.</span><span class="sxs-lookup"><span data-stu-id="2f3d8-132">The Consumption plan automatically allocates compute power when your code is running, scales out as necessary to handle load, and then scales down when code is not running.</span></span> <span data-ttu-id="2f3d8-133">Assim, você não precisa pagar por VMs ociosas e não precisa reservar a capacidade com antecedência.</span><span class="sxs-lookup"><span data-stu-id="2f3d8-133">So, you don't have to pay for idle VMs, and you don't have to reserve capacity in advance.</span></span> <span data-ttu-id="2f3d8-134">Para saber mais sobre os planos de hospedagem, consulte [Consumo do Azure Functions e Planos de Serviço de Aplicativo](functions-scale.md).</span><span class="sxs-lookup"><span data-stu-id="2f3d8-134">To learn more about hosting plans, see [Azure Functions Consumption and App Service plans](functions-scale.md).</span></span>

<span data-ttu-id="2f3d8-135">Para um exemplo de modelo do Azure Resource Manager, consulte [Aplicativo de funções no Plano de Consumo].</span><span class="sxs-lookup"><span data-stu-id="2f3d8-135">For a sample Azure Resource Manager template, see [Function app on Consumption plan].</span></span>

### <a name="create-a-consumption-plan"></a><span data-ttu-id="2f3d8-136">Criar um Plano de Consumo</span><span class="sxs-lookup"><span data-stu-id="2f3d8-136">Create a Consumption plan</span></span>

<span data-ttu-id="2f3d8-137">Um Plano de Consumo é um tipo especial de recurso "serverfarm".</span><span class="sxs-lookup"><span data-stu-id="2f3d8-137">A Consumption plan is a special type of "serverfarm" resource.</span></span> <span data-ttu-id="2f3d8-138">Você o especifica usando o valor `Dynamic` para as propriedades `computeMode` e `sku`:</span><span class="sxs-lookup"><span data-stu-id="2f3d8-138">You specify it by using the `Dynamic` value for the `computeMode` and `sku` properties:</span></span>

```json
{
    "type": "Microsoft.Web/serverfarms",
    "apiVersion": "2015-04-01",
    "name": "[variables('hostingPlanName')]",
    "location": "[resourceGroup().location]",
    "properties": {
        "name": "[variables('hostingPlanName')]",
        "computeMode": "Dynamic",
        "sku": "Dynamic"
    }
}
```

### <a name="create-a-function-app"></a><span data-ttu-id="2f3d8-139">Criar um aplicativo de funções</span><span class="sxs-lookup"><span data-stu-id="2f3d8-139">Create a function app</span></span>

<span data-ttu-id="2f3d8-140">Além disso, um Plano de Consumo requer duas configurações adicionais na configuração do site: `WEBSITE_CONTENTAZUREFILECONNECTIONSTRING` e `WEBSITE_CONTENTSHARE`.</span><span class="sxs-lookup"><span data-stu-id="2f3d8-140">In addition, a Consumption plan requires two additional settings in the site configuration: `WEBSITE_CONTENTAZUREFILECONNECTIONSTRING` and `WEBSITE_CONTENTSHARE`.</span></span> <span data-ttu-id="2f3d8-141">Essas propriedades configuram a conta de armazenamento e o caminho do arquivo em que o código e as configurações do aplicativo de funções estão armazenados.</span><span class="sxs-lookup"><span data-stu-id="2f3d8-141">These properties configure the storage account and file path where the function app code and configuration are stored.</span></span>

```json
{
    "apiVersion": "2015-08-01",
    "type": "Microsoft.Web/sites",
    "name": "[variables('functionAppName')]",
    "location": "[resourceGroup().location]",
    "kind": "functionapp",            
    "dependsOn": [
        "[resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName'))]",
        "[resourceId('Microsoft.Storage/storageAccounts', variables('storageAccountName'))]"
    ],
    "properties": {
        "serverFarmId": "[resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName'))]",
        "siteConfig": {
            "appSettings": [
                {
                    "name": "AzureWebJobsDashboard",
                    "value": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
                },
                {
                    "name": "AzureWebJobsStorage",
                    "value": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
                },
                {
                    "name": "WEBSITE_CONTENTAZUREFILECONNECTIONSTRING",
                    "value": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
                },
                {
                    "name": "WEBSITE_CONTENTSHARE",
                    "value": "[toLower(variables('functionAppName'))]"
                },
                {
                    "name": "FUNCTIONS_EXTENSION_VERSION",
                    "value": "~1"
                }
            ]
        }
    }
}
```                    

<a name="app-service-plan"></a> 

## <a name="deploy-a-function-app-on-the-app-service-plan"></a><span data-ttu-id="2f3d8-142">Implantar um aplicativo de funções no Plano do Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="2f3d8-142">Deploy a function app on the App Service plan</span></span>

<span data-ttu-id="2f3d8-143">No Plano do Serviço de Aplicativo, seus aplicativos de funções são executados em VMs dedicadas, em SKUs Basic, Standard e Premium, assim como os aplicativos Web.</span><span class="sxs-lookup"><span data-stu-id="2f3d8-143">In the App Service plan, your function app runs on dedicated VMs on Basic, Standard, and Premium SKUs, similar to web apps.</span></span> <span data-ttu-id="2f3d8-144">Para obter detalhes sobre como o plano do Serviço de Aplicativo funciona, consulte [Visão geral detalhada de planos de Serviço de Aplicativo do Azure](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2f3d8-144">For details about how the App Service plan works, see the [Azure App Service plans in-depth overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span> 

<span data-ttu-id="2f3d8-145">Para um exemplo de modelo do Azure Resource Manager, consulte [Aplicativo de funções no Plano do Serviço de Aplicativo do Azure].</span><span class="sxs-lookup"><span data-stu-id="2f3d8-145">For a sample Azure Resource Manager template, see [Function app on Azure App Service plan].</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="2f3d8-146">Criar um plano de Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="2f3d8-146">Create an App Service plan</span></span>

```json
{
    "type": "Microsoft.Web/serverfarms",
    "apiVersion": "2015-04-01",
    "name": "[variables('hostingPlanName')]",
    "location": "[resourceGroup().location]",
    "properties": {
        "name": "[variables('hostingPlanName')]",
        "sku": "[parameters('sku')]",
        "workerSize": "[parameters('workerSize')]",
        "hostingEnvironment": "",
        "numberOfWorkers": 1
    }
}
```

### <a name="create-a-function-app"></a><span data-ttu-id="2f3d8-147">Criar um aplicativo de funções</span><span class="sxs-lookup"><span data-stu-id="2f3d8-147">Create a function app</span></span> 

<span data-ttu-id="2f3d8-148">Depois de selecionar uma opção de dimensionamento, crie um aplicativo de funções.</span><span class="sxs-lookup"><span data-stu-id="2f3d8-148">After you've selected a scaling option, create a function app.</span></span> <span data-ttu-id="2f3d8-149">O aplicativo é o contêiner que mantém todas as suas funções.</span><span class="sxs-lookup"><span data-stu-id="2f3d8-149">The app is the container that holds all your functions.</span></span>

<span data-ttu-id="2f3d8-150">Um aplicativo de funções tem muitos recursos filho que podem ser usados na sua implantação, incluindo configurações do aplicativo e opções de controle do código-fonte.</span><span class="sxs-lookup"><span data-stu-id="2f3d8-150">A function app has many child resources that you can use in your deployment, including app settings and source control options.</span></span> <span data-ttu-id="2f3d8-151">Você também pode optar por remover o recurso filho **sourcecontrols** e usar uma outra [opção de implantação](functions-continuous-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="2f3d8-151">You also might choose to remove the **sourcecontrols** child resource, and use a different [deployment option](functions-continuous-deployment.md) instead.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2f3d8-152">Para implantar seu aplicativo com êxito usando o Azure Resource Manager, é importante entender como os recursos são implantados no Azure.</span><span class="sxs-lookup"><span data-stu-id="2f3d8-152">To successfully deploy your application by using Azure Resource Manager, it's important to understand how resources are deployed in Azure.</span></span> <span data-ttu-id="2f3d8-153">No exemplo a seguir, as configurações de nível superior são aplicadas usando **siteConfig**.</span><span class="sxs-lookup"><span data-stu-id="2f3d8-153">In the following example, top-level configurations are applied by using **siteConfig**.</span></span> <span data-ttu-id="2f3d8-154">É importante definir essas configurações em um nível superior porque transmitem informações para o mecanismo de implantação e de tempo de execução do Functions.</span><span class="sxs-lookup"><span data-stu-id="2f3d8-154">It's important to set these configurations at a top level, because they convey information to the Functions runtime and deployment engine.</span></span> <span data-ttu-id="2f3d8-155">Informações de nível superior são necessárias antes do recurso filho **sourcecontrols/web** ser aplicado.</span><span class="sxs-lookup"><span data-stu-id="2f3d8-155">Top-level information is required before the child **sourcecontrols/web** resource is applied.</span></span> <span data-ttu-id="2f3d8-156">Embora seja possível definir essas configurações no nível de recurso filho **config/appSettings**, em alguns casos, o aplicativo de funções deve ser implantado *antes* de **config/appSettings** ser aplicado.</span><span class="sxs-lookup"><span data-stu-id="2f3d8-156">Although it's possible to configure these settings in the child-level **config/appSettings** resource, in some cases your function app must be deployed *before* **config/appSettings** is applied.</span></span> <span data-ttu-id="2f3d8-157">Por exemplo, quando você está usado funções com [aplicativos lógicos](../logic-apps/index.md), as funções são uma dependência de outro recurso.</span><span class="sxs-lookup"><span data-stu-id="2f3d8-157">For example, when you are using functions with [Logic Apps](../logic-apps/index.md), your functions are a dependency of another resource.</span></span>

```json
{
  "apiVersion": "2015-08-01",
  "name": "[parameters('appName')]",
  "type": "Microsoft.Web/sites",
  "kind": "functionapp",
  "location": "[parameters('location')]",
  "dependsOn": [
    "[resourceId('Microsoft.Storage/storageAccounts', variables('storageAccountName'))]",
    "[resourceId('Microsoft.Web/serverfarms', parameters('appName'))]"
  ],
  "properties": {
     "serverFarmId": "[variables('appServicePlanName')]",
     "siteConfig": {
        "alwaysOn": true,
        "appSettings": [
            { "name": "FUNCTIONS_EXTENSION_VERSION", "value": "~1" },
            { "name": "Project", "value": "src" }
        ]
     }
  },
  "resources": [
     {
        "apiVersion": "2015-08-01",
        "name": "appsettings",
        "type": "config",
        "dependsOn": [
          "[resourceId('Microsoft.Web/Sites', parameters('appName'))]",
          "[resourceId('Microsoft.Web/Sites/sourcecontrols', parameters('appName'), 'web')]",
          "[resourceId('Microsoft.Storage/storageAccounts', variables('storageAccountName'))]"
        ],
        "properties": {
          "AzureWebJobsStorage": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]",
          "AzureWebJobsDashboard": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
        }
     },
     {
          "apiVersion": "2015-08-01",
          "name": "web",
          "type": "sourcecontrols",
          "dependsOn": [
            "[resourceId('Microsoft.Web/sites/', parameters('appName'))]"
          ],
          "properties": {
            "RepoUrl": "[parameters('sourceCodeRepositoryURL')]",
            "branch": "[parameters('sourceCodeBranch')]",
            "IsManualIntegration": "[parameters('sourceCodeManualIntegration')]"
          }
     }
  ]
}
```
> [!TIP]
> <span data-ttu-id="2f3d8-158">Este modelo usa o valor das configurações do aplicativo [Projeto](https://github.com/projectkudu/kudu/wiki/Customizing-deployments#using-app-settings-instead-of-a-deployment-file), que determina o diretório-base cujo mecanismo de implantação de funções (Kudu) procura o código implantável.</span><span class="sxs-lookup"><span data-stu-id="2f3d8-158">This template uses the [Project](https://github.com/projectkudu/kudu/wiki/Customizing-deployments#using-app-settings-instead-of-a-deployment-file) app settings value, which sets the base directory in which the Functions deployment engine (Kudu) looks for deployable code.</span></span> <span data-ttu-id="2f3d8-159">Em nosso repositório, nossas funções estão em uma subpasta da pasta **src**.</span><span class="sxs-lookup"><span data-stu-id="2f3d8-159">In our repository, our functions are in a subfolder of the **src** folder.</span></span> <span data-ttu-id="2f3d8-160">Assim, no exemplo anterior, definimos o valor de configurações do aplicativo para `src`.</span><span class="sxs-lookup"><span data-stu-id="2f3d8-160">So, in the preceding example, we set the app settings value to `src`.</span></span> <span data-ttu-id="2f3d8-161">Se as funções estão na raiz do seu repositório, ou se não está implantando do controle de origem, você pode remover esse valor de configurações do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2f3d8-161">If your functions are in the root of your repository, or if you are not deploying from source control, you can remove this app settings value.</span></span>

## <a name="deploy-your-template"></a><span data-ttu-id="2f3d8-162">Implantar o modelo</span><span class="sxs-lookup"><span data-stu-id="2f3d8-162">Deploy your template</span></span>

<span data-ttu-id="2f3d8-163">Você pode usar qualquer uma das seguintes maneiras para implantar o modelo:</span><span class="sxs-lookup"><span data-stu-id="2f3d8-163">You can use any of the following ways to deploy your template:</span></span>

* [<span data-ttu-id="2f3d8-164">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2f3d8-164">PowerShell</span></span>](../azure-resource-manager/resource-group-template-deploy.md)
* [<span data-ttu-id="2f3d8-165">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="2f3d8-165">Azure CLI</span></span>](../azure-resource-manager/resource-group-template-deploy-cli.md)
* [<span data-ttu-id="2f3d8-166">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="2f3d8-166">Azure portal</span></span>](../azure-resource-manager/resource-group-template-deploy-portal.md)
* [<span data-ttu-id="2f3d8-167">API REST</span><span class="sxs-lookup"><span data-stu-id="2f3d8-167">REST API</span></span>](../azure-resource-manager/resource-group-template-deploy-rest.md)

### <a name="deploy-to-azure-button"></a><span data-ttu-id="2f3d8-168">Botão Implantar no Azure</span><span class="sxs-lookup"><span data-stu-id="2f3d8-168">Deploy to Azure button</span></span>

<span data-ttu-id="2f3d8-169">Substitua ```<url-encoded-path-to-azuredeploy-json>``` por uma versão [codificada de URL](https://www.bing.com/search?q=url+encode) do caminho bruto de seu `azuredeploy.json` arquivo no GitHub.</span><span class="sxs-lookup"><span data-stu-id="2f3d8-169">Replace ```<url-encoded-path-to-azuredeploy-json>``` with a [URL-encoded](https://www.bing.com/search?q=url+encode) version of the raw path of your `azuredeploy.json` file in GitHub.</span></span>

<span data-ttu-id="2f3d8-170">Este é um exemplo que usa markdown:</span><span class="sxs-lookup"><span data-stu-id="2f3d8-170">Here is an example that uses markdown:</span></span>

```markdown
[![Deploy to Azure](http://azuredeploy.net/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/<url-encoded-path-to-azuredeploy-json>)
```

<span data-ttu-id="2f3d8-171">Este é um exemplo que usa HTML:</span><span class="sxs-lookup"><span data-stu-id="2f3d8-171">Here is an example that uses HTML:</span></span>

```html
<a href="https://portal.azure.com/#create/Microsoft.Template/uri/<url-encoded-path-to-azuredeploy-json>" target="_blank"><img src="http://azuredeploy.net/deploybutton.png"></a>
```

## <a name="next-steps"></a><span data-ttu-id="2f3d8-172">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2f3d8-172">Next steps</span></span>

<span data-ttu-id="2f3d8-173">Saiba mais sobre como desenvolver e configurar o Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="2f3d8-173">Learn more about how to develop and configure Azure Functions.</span></span>

* [<span data-ttu-id="2f3d8-174">Referência do desenvolvedor do Azure Functions</span><span class="sxs-lookup"><span data-stu-id="2f3d8-174">Azure Functions developer reference</span></span>](functions-reference.md)
* [<span data-ttu-id="2f3d8-175">Como definir configurações do aplicativo de funções do Azure</span><span class="sxs-lookup"><span data-stu-id="2f3d8-175">How to configure Azure function app settings</span></span>](functions-how-to-use-azure-function-app-settings.md)
* [<span data-ttu-id="2f3d8-176">Como criar a sua primeira função do Azure</span><span class="sxs-lookup"><span data-stu-id="2f3d8-176">Create your first Azure function</span></span>](functions-create-first-azure-function.md)

<!-- LINKS -->

[Aplicativo de funções no Plano de Consumo]: https://github.com/Azure/azure-quickstart-templates/blob/master/101-function-app-create-dynamic/azuredeploy.json
[Aplicativo de funções no Plano do Serviço de Aplicativo do Azure]: https://github.com/Azure/azure-quickstart-templates/blob/master/101-function-app-create-dedicated/azuredeploy.json
