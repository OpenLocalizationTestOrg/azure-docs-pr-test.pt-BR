---
title: "implantação de recursos de aaaAutomate para um aplicativo de função em funções do Azure | Microsoft Docs"
description: "Saiba como toobuild um modelo do Gerenciador de recursos do Azure que implanta o aplicativo de função."
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
ms.openlocfilehash: b0df0d4ef9fe93213f7b1cb1d1e6b4e14f8b3a30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="automate-resource-deployment-for-your-function-app-in-azure-functions"></a><span data-ttu-id="62499-104">Automatizar a implantação de recursos para seu aplicativo de funções do Azure Functions</span><span class="sxs-lookup"><span data-stu-id="62499-104">Automate resource deployment for your function app in Azure Functions</span></span>

<span data-ttu-id="62499-105">Você pode usar um modelo de Gerenciador de recursos do Azure toodeploy um aplicativo de função.</span><span class="sxs-lookup"><span data-stu-id="62499-105">You can use an Azure Resource Manager template toodeploy a function app.</span></span> <span data-ttu-id="62499-106">Este artigo descreve recursos Olá necessárias e os parâmetros para fazer isso.</span><span class="sxs-lookup"><span data-stu-id="62499-106">This article outlines hello required resources and parameters for doing so.</span></span> <span data-ttu-id="62499-107">Talvez seja necessário obter recursos adicionais toodeploy, dependendo da saudação [gatilhos e associações](functions-triggers-bindings.md) em seu aplicativo de função.</span><span class="sxs-lookup"><span data-stu-id="62499-107">You might need toodeploy additional resources, depending on hello [triggers and bindings](functions-triggers-bindings.md) in your function app.</span></span>

<span data-ttu-id="62499-108">Para saber mais sobre a criação de modelos, consulte [Criação de modelos do Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="62499-108">For more information about creating templates, see [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="62499-109">Para modelos de exemplo, consulte:</span><span class="sxs-lookup"><span data-stu-id="62499-109">For sample templates, see:</span></span>
- <span data-ttu-id="62499-110">[Aplicativo de funções no Plano de Consumo]</span><span class="sxs-lookup"><span data-stu-id="62499-110">[Function app on Consumption plan]</span></span>
- <span data-ttu-id="62499-111">[Aplicativo de funções no Plano do Serviço de Aplicativo do Azure]</span><span class="sxs-lookup"><span data-stu-id="62499-111">[Function app on Azure App Service plan]</span></span>

## <a name="required-resources"></a><span data-ttu-id="62499-112">Recursos necessários</span><span class="sxs-lookup"><span data-stu-id="62499-112">Required resources</span></span>

<span data-ttu-id="62499-113">Um aplicativo de funções requer estes recursos:</span><span class="sxs-lookup"><span data-stu-id="62499-113">A function app requires these resources:</span></span>

* <span data-ttu-id="62499-114">Uma conta de [Armazenamento do Azure](../storage/index.md)</span><span class="sxs-lookup"><span data-stu-id="62499-114">An [Azure Storage](../storage/index.md) account</span></span>
* <span data-ttu-id="62499-115">Um plano de hospedagem (Plano de Consumo ou Plano do Serviço de Aplicativo)</span><span class="sxs-lookup"><span data-stu-id="62499-115">A hosting plan (Consumption plan or App Service plan)</span></span>
* <span data-ttu-id="62499-116">Um aplicativo de funções</span><span class="sxs-lookup"><span data-stu-id="62499-116">A function app</span></span> 

### <a name="storage-account"></a><span data-ttu-id="62499-117">Conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="62499-117">Storage account</span></span>

<span data-ttu-id="62499-118">Uma conta de armazenamento do Azure é necessária para um aplicativo de funções.</span><span class="sxs-lookup"><span data-stu-id="62499-118">An Azure storage account is required for a function app.</span></span> <span data-ttu-id="62499-119">Você precisa de uma conta de finalidade geral que dá suporte a blobs, tabelas, consultas e arquivos.</span><span class="sxs-lookup"><span data-stu-id="62499-119">You need a general purpose account that supports blobs, tables, queues, and files.</span></span> <span data-ttu-id="62499-120">Para saber mais, confira [Requisitos da conta de armazenamento do Azure Functions](functions-create-function-app-portal.md#storage-account-requirements).</span><span class="sxs-lookup"><span data-stu-id="62499-120">For more information, see [Azure Functions storage account requirements](functions-create-function-app-portal.md#storage-account-requirements).</span></span>

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

<span data-ttu-id="62499-121">Além disso, Olá propriedades `AzureWebJobsStorage` e `AzureWebJobsDashboard` devem ser especificados como configurações de aplicativo na configuração do site hello.</span><span class="sxs-lookup"><span data-stu-id="62499-121">In addition, hello properties `AzureWebJobsStorage` and `AzureWebJobsDashboard` must be specified as app settings in hello site configuration.</span></span> <span data-ttu-id="62499-122">tempo de execução de funções do Azure Olá usa Olá `AzureWebJobsStorage` toocreate as filas internas de cadeia de caracteres de conexão.</span><span class="sxs-lookup"><span data-stu-id="62499-122">hello Azure Functions runtime uses hello `AzureWebJobsStorage` connection string toocreate internal queues.</span></span> <span data-ttu-id="62499-123">Olá a cadeia de caracteres de conexão `AzureWebJobsDashboard` é usado toolog tooAzure tabela armazenamento e energia hello **Monitor** no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="62499-123">hello connection string `AzureWebJobsDashboard` is used toolog tooAzure Table storage and power hello **Monitor** tab in hello portal.</span></span>

<span data-ttu-id="62499-124">Essas propriedades são especificadas em Olá `appSettings` coleção em Olá `siteConfig` objeto:</span><span class="sxs-lookup"><span data-stu-id="62499-124">These properties are specified in hello `appSettings` collection in hello `siteConfig` object:</span></span>

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

### <a name="hosting-plan"></a><span data-ttu-id="62499-125">Plano de hospedagem</span><span class="sxs-lookup"><span data-stu-id="62499-125">Hosting plan</span></span>

<span data-ttu-id="62499-126">definição de saudação do plano de hospedagem de saudação varia, dependendo se você usar um plano de serviço de aplicativo ou de consumo.</span><span class="sxs-lookup"><span data-stu-id="62499-126">hello definition of hello hosting plan varies, depending on whether you use a Consumption or App Service plan.</span></span> <span data-ttu-id="62499-127">Consulte [implantar um aplicativo de função no plano de consumo Olá](#consumption) e [implantar um aplicativo de função em Olá plano de serviço de aplicativo](#app-service-plan).</span><span class="sxs-lookup"><span data-stu-id="62499-127">See [Deploy a function app on hello Consumption plan](#consumption) and [Deploy a function app on hello App Service plan](#app-service-plan).</span></span>

### <a name="function-app"></a><span data-ttu-id="62499-128">Aplicativo de funções</span><span class="sxs-lookup"><span data-stu-id="62499-128">Function app</span></span>

<span data-ttu-id="62499-129">recurso de aplicativo de função Hello é definido usando um recurso do tipo **Microsoft.Web/Site** e tipo **functionapp**:</span><span class="sxs-lookup"><span data-stu-id="62499-129">hello function app resource is defined by using a resource of type **Microsoft.Web/Site** and kind **functionapp**:</span></span>

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

## <a name="deploy-a-function-app-on-hello-consumption-plan"></a><span data-ttu-id="62499-130">Implantar um aplicativo de função no plano de consumo Olá</span><span class="sxs-lookup"><span data-stu-id="62499-130">Deploy a function app on hello Consumption plan</span></span>

<span data-ttu-id="62499-131">Você pode executar um aplicativo de função em dois modos diferentes: Olá plano de consumo e hello plano de serviço de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="62499-131">You can run a function app in two different modes: hello Consumption plan and hello App Service plan.</span></span> <span data-ttu-id="62499-132">plano de consumo Olá aloca automaticamente a capacidade de computação quando seu código está em execução, pode ser dimensionado como carga de toohandle necessário e expande para baixo quando o código não está em execução.</span><span class="sxs-lookup"><span data-stu-id="62499-132">hello Consumption plan automatically allocates compute power when your code is running, scales out as necessary toohandle load, and then scales down when code is not running.</span></span> <span data-ttu-id="62499-133">Portanto, você não tem toopay para máquinas virtuais ociosas, e você não tem capacidade tooreserve com antecedência.</span><span class="sxs-lookup"><span data-stu-id="62499-133">So, you don't have toopay for idle VMs, and you don't have tooreserve capacity in advance.</span></span> <span data-ttu-id="62499-134">toolearn mais sobre hospedagem planos, consulte [planos de serviço de aplicativo e o consumo de funções do Azure](functions-scale.md).</span><span class="sxs-lookup"><span data-stu-id="62499-134">toolearn more about hosting plans, see [Azure Functions Consumption and App Service plans](functions-scale.md).</span></span>

<span data-ttu-id="62499-135">Para um exemplo de modelo do Azure Resource Manager, consulte [Aplicativo de funções no Plano de Consumo].</span><span class="sxs-lookup"><span data-stu-id="62499-135">For a sample Azure Resource Manager template, see [Function app on Consumption plan].</span></span>

### <a name="create-a-consumption-plan"></a><span data-ttu-id="62499-136">Criar um Plano de Consumo</span><span class="sxs-lookup"><span data-stu-id="62499-136">Create a Consumption plan</span></span>

<span data-ttu-id="62499-137">Um Plano de Consumo é um tipo especial de recurso "serverfarm".</span><span class="sxs-lookup"><span data-stu-id="62499-137">A Consumption plan is a special type of "serverfarm" resource.</span></span> <span data-ttu-id="62499-138">Especificá-lo usando Olá `Dynamic` valor Olá `computeMode` e `sku` propriedades:</span><span class="sxs-lookup"><span data-stu-id="62499-138">You specify it by using hello `Dynamic` value for hello `computeMode` and `sku` properties:</span></span>

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

### <a name="create-a-function-app"></a><span data-ttu-id="62499-139">Criar um aplicativo de funções</span><span class="sxs-lookup"><span data-stu-id="62499-139">Create a function app</span></span>

<span data-ttu-id="62499-140">Além disso, um plano de consumo requer duas configurações adicionais na configuração do site Olá: `WEBSITE_CONTENTAZUREFILECONNECTIONSTRING` e `WEBSITE_CONTENTSHARE`.</span><span class="sxs-lookup"><span data-stu-id="62499-140">In addition, a Consumption plan requires two additional settings in hello site configuration: `WEBSITE_CONTENTAZUREFILECONNECTIONSTRING` and `WEBSITE_CONTENTSHARE`.</span></span> <span data-ttu-id="62499-141">Essas propriedades configuram Olá armazenamento conta e o caminho onde o código do aplicativo de função hello e configuração são armazenados.</span><span class="sxs-lookup"><span data-stu-id="62499-141">These properties configure hello storage account and file path where hello function app code and configuration are stored.</span></span>

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

## <a name="deploy-a-function-app-on-hello-app-service-plan"></a><span data-ttu-id="62499-142">Implantar um aplicativo de função em Olá plano de serviço de aplicativo</span><span class="sxs-lookup"><span data-stu-id="62499-142">Deploy a function app on hello App Service plan</span></span>

<span data-ttu-id="62499-143">Em Olá plano de serviço de aplicativo, seu aplicativo de função é executado em máquinas virtuais dedicadas em aplicativos de tooweb Basic, Standard e Premium SKUs, semelhantes.</span><span class="sxs-lookup"><span data-stu-id="62499-143">In hello App Service plan, your function app runs on dedicated VMs on Basic, Standard, and Premium SKUs, similar tooweb apps.</span></span> <span data-ttu-id="62499-144">Para obter detalhes sobre como funciona a saudação plano de serviço de aplicativo, consulte Olá [visão geral detalhada de planos de serviço de aplicativo do Azure](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span><span class="sxs-lookup"><span data-stu-id="62499-144">For details about how hello App Service plan works, see hello [Azure App Service plans in-depth overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span> 

<span data-ttu-id="62499-145">Para um exemplo de modelo do Azure Resource Manager, consulte [Aplicativo de funções no Plano do Serviço de Aplicativo do Azure].</span><span class="sxs-lookup"><span data-stu-id="62499-145">For a sample Azure Resource Manager template, see [Function app on Azure App Service plan].</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="62499-146">Criar um plano de Serviço de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="62499-146">Create an App Service plan</span></span>

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

### <a name="create-a-function-app"></a><span data-ttu-id="62499-147">Criar um aplicativo de funções</span><span class="sxs-lookup"><span data-stu-id="62499-147">Create a function app</span></span> 

<span data-ttu-id="62499-148">Depois de selecionar uma opção de dimensionamento, crie um aplicativo de funções.</span><span class="sxs-lookup"><span data-stu-id="62499-148">After you've selected a scaling option, create a function app.</span></span> <span data-ttu-id="62499-149">Olá aplicativo é o contêiner de saudação que contém todas as suas funções.</span><span class="sxs-lookup"><span data-stu-id="62499-149">hello app is hello container that holds all your functions.</span></span>

<span data-ttu-id="62499-150">Um aplicativo de funções tem muitos recursos filho que podem ser usados na sua implantação, incluindo configurações do aplicativo e opções de controle do código-fonte.</span><span class="sxs-lookup"><span data-stu-id="62499-150">A function app has many child resources that you can use in your deployment, including app settings and source control options.</span></span> <span data-ttu-id="62499-151">Você também pode escolher Olá tooremove **sourcecontrols** recurso filho e use outra [opção de implantação](functions-continuous-deployment.md) em vez disso.</span><span class="sxs-lookup"><span data-stu-id="62499-151">You also might choose tooremove hello **sourcecontrols** child resource, and use a different [deployment option](functions-continuous-deployment.md) instead.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="62499-152">toosuccessfully implantar seu aplicativo usando o Gerenciador de recursos do Azure, é importante toounderstand como os recursos são implantados no Azure.</span><span class="sxs-lookup"><span data-stu-id="62499-152">toosuccessfully deploy your application by using Azure Resource Manager, it's important toounderstand how resources are deployed in Azure.</span></span> <span data-ttu-id="62499-153">Em Olá exemplo a seguir, as configurações de nível superior são aplicadas usando **siteConfig**.</span><span class="sxs-lookup"><span data-stu-id="62499-153">In hello following example, top-level configurations are applied by using **siteConfig**.</span></span> <span data-ttu-id="62499-154">É importante tooset essas configurações em um alto nível, porque eles transmitem o mecanismo de tempo de execução e a implantação de funções de toohello do informações.</span><span class="sxs-lookup"><span data-stu-id="62499-154">It's important tooset these configurations at a top level, because they convey information toohello Functions runtime and deployment engine.</span></span> <span data-ttu-id="62499-155">Informações de nível superior é necessário antes do filho Olá **sourcecontrols/web** recursos é aplicado.</span><span class="sxs-lookup"><span data-stu-id="62499-155">Top-level information is required before hello child **sourcecontrols/web** resource is applied.</span></span> <span data-ttu-id="62499-156">Embora seja possível tooconfigure essas configurações no hello nível filho **config/appSettings** recursos, em alguns casos, seu aplicativo de função deve ser implantado *antes de* **config/appSettings**  é aplicado.</span><span class="sxs-lookup"><span data-stu-id="62499-156">Although it's possible tooconfigure these settings in hello child-level **config/appSettings** resource, in some cases your function app must be deployed *before* **config/appSettings** is applied.</span></span> <span data-ttu-id="62499-157">Por exemplo, quando você está usado funções com [aplicativos lógicos](../logic-apps/index.md), as funções são uma dependência de outro recurso.</span><span class="sxs-lookup"><span data-stu-id="62499-157">For example, when you are using functions with [Logic Apps](../logic-apps/index.md), your functions are a dependency of another resource.</span></span>

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
> <span data-ttu-id="62499-158">Este modelo usa Olá [projeto](https://github.com/projectkudu/kudu/wiki/Customizing-deployments#using-app-settings-instead-of-a-deployment-file) valor de configurações de aplicativo, que define o diretório base hello, na qual Olá mecanismo de implantação de funções (Kudu) procura código implantável.</span><span class="sxs-lookup"><span data-stu-id="62499-158">This template uses hello [Project](https://github.com/projectkudu/kudu/wiki/Customizing-deployments#using-app-settings-instead-of-a-deployment-file) app settings value, which sets hello base directory in which hello Functions deployment engine (Kudu) looks for deployable code.</span></span> <span data-ttu-id="62499-159">Em nosso repositório, nosso funções estão em uma subpasta da saudação **src** pasta.</span><span class="sxs-lookup"><span data-stu-id="62499-159">In our repository, our functions are in a subfolder of hello **src** folder.</span></span> <span data-ttu-id="62499-160">Portanto, em Olá anterior de exemplo, definimos o valor de configurações de aplicativo hello muito`src`.</span><span class="sxs-lookup"><span data-stu-id="62499-160">So, in hello preceding example, we set hello app settings value too`src`.</span></span> <span data-ttu-id="62499-161">Se as funções estão na raiz de saudação do repositório, ou se não estiver implantando do controle de origem, você pode remover esse valor de configurações do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="62499-161">If your functions are in hello root of your repository, or if you are not deploying from source control, you can remove this app settings value.</span></span>

## <a name="deploy-your-template"></a><span data-ttu-id="62499-162">Implantar o modelo</span><span class="sxs-lookup"><span data-stu-id="62499-162">Deploy your template</span></span>

<span data-ttu-id="62499-163">Você pode usar qualquer Olá toodeploy maneiras a seguir o modelo:</span><span class="sxs-lookup"><span data-stu-id="62499-163">You can use any of hello following ways toodeploy your template:</span></span>

* [<span data-ttu-id="62499-164">PowerShell</span><span class="sxs-lookup"><span data-stu-id="62499-164">PowerShell</span></span>](../azure-resource-manager/resource-group-template-deploy.md)
* [<span data-ttu-id="62499-165">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="62499-165">Azure CLI</span></span>](../azure-resource-manager/resource-group-template-deploy-cli.md)
* [<span data-ttu-id="62499-166">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="62499-166">Azure portal</span></span>](../azure-resource-manager/resource-group-template-deploy-portal.md)
* [<span data-ttu-id="62499-167">API REST</span><span class="sxs-lookup"><span data-stu-id="62499-167">REST API</span></span>](../azure-resource-manager/resource-group-template-deploy-rest.md)

### <a name="deploy-tooazure-button"></a><span data-ttu-id="62499-168">TooAzure botão implantar</span><span class="sxs-lookup"><span data-stu-id="62499-168">Deploy tooAzure button</span></span>

<span data-ttu-id="62499-169">Substituir ```<url-encoded-path-to-azuredeploy-json>``` com um [codificados de URL](https://www.bing.com/search?q=url+encode) versão do caminho bruto de saudação do seu `azuredeploy.json` arquivo no GitHub.</span><span class="sxs-lookup"><span data-stu-id="62499-169">Replace ```<url-encoded-path-to-azuredeploy-json>``` with a [URL-encoded](https://www.bing.com/search?q=url+encode) version of hello raw path of your `azuredeploy.json` file in GitHub.</span></span>

<span data-ttu-id="62499-170">Este é um exemplo que usa markdown:</span><span class="sxs-lookup"><span data-stu-id="62499-170">Here is an example that uses markdown:</span></span>

```markdown
[![Deploy tooAzure](http://azuredeploy.net/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/<url-encoded-path-to-azuredeploy-json>)
```

<span data-ttu-id="62499-171">Este é um exemplo que usa HTML:</span><span class="sxs-lookup"><span data-stu-id="62499-171">Here is an example that uses HTML:</span></span>

```html
<a href="https://portal.azure.com/#create/Microsoft.Template/uri/<url-encoded-path-to-azuredeploy-json>" target="_blank"><img src="http://azuredeploy.net/deploybutton.png"></a>
```

## <a name="next-steps"></a><span data-ttu-id="62499-172">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="62499-172">Next steps</span></span>

<span data-ttu-id="62499-173">Saiba mais sobre como toodevelop e configure funções do Azure.</span><span class="sxs-lookup"><span data-stu-id="62499-173">Learn more about how toodevelop and configure Azure Functions.</span></span>

* [<span data-ttu-id="62499-174">Referência do desenvolvedor do Azure Functions</span><span class="sxs-lookup"><span data-stu-id="62499-174">Azure Functions developer reference</span></span>](functions-reference.md)
* [<span data-ttu-id="62499-175">Como tooconfigure Azure funciona configurações do aplicativo</span><span class="sxs-lookup"><span data-stu-id="62499-175">How tooconfigure Azure function app settings</span></span>](functions-how-to-use-azure-function-app-settings.md)
* [<span data-ttu-id="62499-176">Como criar a sua primeira função do Azure</span><span class="sxs-lookup"><span data-stu-id="62499-176">Create your first Azure function</span></span>](functions-create-first-azure-function.md)

<!-- LINKS -->

[Aplicativo de funções no Plano de Consumo]: https://github.com/Azure/azure-quickstart-templates/blob/master/101-function-app-create-dynamic/azuredeploy.json
[Aplicativo de funções no Plano do Serviço de Aplicativo do Azure]: https://github.com/Azure/azure-quickstart-templates/blob/master/101-function-app-create-dedicated/azuredeploy.json
