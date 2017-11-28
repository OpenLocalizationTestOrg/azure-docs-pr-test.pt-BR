---
title: "aaaDeploy um aplicativo web que é vinculado repositório do GitHub tooa | Microsoft Docs"
description: "Use um modelo de Gerenciador de recursos do Azure toodeploy um aplicativo web que contém um projeto de um repositório do GitHub."
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 32739607-85fe-43c8-a4dc-1feb46d93a4d
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/27/2016
ms.author: cephalin
ms.openlocfilehash: 8b23416c4c06a60991517e6ee4cd82bebc5a9d73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-web-app-linked-tooa-github-repository"></a><span data-ttu-id="20075-103">Implantar um repositório GitHub do web app vinculado tooa</span><span class="sxs-lookup"><span data-stu-id="20075-103">Deploy a web app linked tooa GitHub repository</span></span>
<span data-ttu-id="20075-104">Neste tópico, você aprenderá como toocreate um modelo do Gerenciador de recursos do Azure que implanta um aplicativo web que é vinculado tooa projeto em um repositório do GitHub.</span><span class="sxs-lookup"><span data-stu-id="20075-104">In this topic, you will learn how toocreate an Azure Resource Manager template that deploys a web app that is linked tooa project in a GitHub repository.</span></span> <span data-ttu-id="20075-105">Você aprenderá como toodefine quais recursos são implantados e como toodefine parâmetros que são especificados quando a implantação de saudação for executada.</span><span class="sxs-lookup"><span data-stu-id="20075-105">You will learn how toodefine which resources are deployed and how toodefine parameters that are specified when hello deployment is executed.</span></span> <span data-ttu-id="20075-106">Você pode usar este modelo para suas próprias implantações ou personalizá-lo toomeet seus requisitos.</span><span class="sxs-lookup"><span data-stu-id="20075-106">You can use this template for your own deployments, or customize it toomeet your requirements.</span></span>

<span data-ttu-id="20075-107">Para obter mais informações sobre a criação de modelos, consulte [Criação de Modelos do Gerenciador de Recursos do Azure](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="20075-107">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="20075-108">Para o modelo do hello completa, consulte [modelo vinculado de aplicativo da Web de tooGitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="20075-108">For hello complete template, see [Web App Linked tooGitHub template](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.json).</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="what-you-will-deploy"></a><span data-ttu-id="20075-109">O que você implantará</span><span class="sxs-lookup"><span data-stu-id="20075-109">What you will deploy</span></span>
<span data-ttu-id="20075-110">Com esse modelo, você implantará um aplicativo web que contém o código de saudação de um projeto no GitHub.</span><span class="sxs-lookup"><span data-stu-id="20075-110">With this template, you will deploy a web app that contains hello code from a project in GitHub.</span></span>

<span data-ttu-id="20075-111">toorun Olá implantação automaticamente, clique em Olá botão a seguir:</span><span class="sxs-lookup"><span data-stu-id="20075-111">toorun hello deployment automatically, click hello following button:</span></span>

<span data-ttu-id="20075-112">[![Implantar tooAzure](./media/app-service-web-arm-from-github-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-github-deploy%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="20075-112">[![Deploy tooAzure](./media/app-service-web-arm-from-github-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-github-deploy%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="20075-113">parâmetros</span><span class="sxs-lookup"><span data-stu-id="20075-113">Parameters</span></span>
[!INCLUDE [app-service-web-deploy-web-parameters](../../includes/app-service-web-deploy-web-parameters.md)]

### <a name="repourl"></a><span data-ttu-id="20075-114">repoURL</span><span class="sxs-lookup"><span data-stu-id="20075-114">repoURL</span></span>
<span data-ttu-id="20075-115">Olá URL para o repositório do GitHub que contém a saudação toodeploy de projeto.</span><span class="sxs-lookup"><span data-stu-id="20075-115">hello URL for GitHub repository that contains hello project toodeploy.</span></span> <span data-ttu-id="20075-116">Este parâmetro contém um valor padrão, mas esse valor é somente pretendido tooshow você como tooprovide Olá URL para o repositório.</span><span class="sxs-lookup"><span data-stu-id="20075-116">This parameter contains a default value but this value is only intended tooshow you how tooprovide hello URL for repository.</span></span> <span data-ttu-id="20075-117">Você pode usar esse valor quando o teste Olá modelo, mas você desejará tooprovide Olá URL seu próprio repositório ao trabalhar com o modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="20075-117">You can use this value when testing hello template but you will want tooprovide hello URL your own repository when working with hello template.</span></span>

    "repoURL": {
        "type": "string",
        "defaultValue": "https://github.com/davidebbo-test/Mvc52Application.git"
    }

### <a name="branch"></a><span data-ttu-id="20075-118">branch</span><span class="sxs-lookup"><span data-stu-id="20075-118">branch</span></span>
<span data-ttu-id="20075-119">ramificação de saudação do hello repositório toouse ao implantar o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="20075-119">hello branch of hello repository toouse when deploying hello application.</span></span> <span data-ttu-id="20075-120">é o valor padrão de saudação mestre, mas você pode fornecer o nome de saudação do qualquer branch no repositório de saudação que você deseja toodeploy.</span><span class="sxs-lookup"><span data-stu-id="20075-120">hello default value is master, but you can provide hello name of any branch in hello repository that you wish toodeploy.</span></span>

    "branch": {
        "type": "string",
        "defaultValue": "master"
    }

## <a name="resources-toodeploy"></a><span data-ttu-id="20075-121">Recursos toodeploy</span><span class="sxs-lookup"><span data-stu-id="20075-121">Resources toodeploy</span></span>
[!INCLUDE [app-service-web-deploy-web-host](../../includes/app-service-web-deploy-web-host.md)]

### <a name="web-app"></a><span data-ttu-id="20075-122">Aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="20075-122">Web app</span></span>
<span data-ttu-id="20075-123">Cria um aplicativo web de saudação que é vinculado toohello projeto no GitHub.</span><span class="sxs-lookup"><span data-stu-id="20075-123">Creates hello web app that is linked toohello project in GitHub.</span></span> 

<span data-ttu-id="20075-124">Especifique nome de saudação do Olá web aplicativo por meio de saudação **siteName** parâmetro e o local de saudação do aplicativo web de saudação por meio de saudação **siteLocation** parâmetro.</span><span class="sxs-lookup"><span data-stu-id="20075-124">You specify hello name of hello web app through hello **siteName** parameter, and hello location of hello web app through hello **siteLocation** parameter.</span></span> <span data-ttu-id="20075-125">Em Olá **dependsOn** elemento, o modelo de saudação define Olá web aplicativo como dependente de serviço Olá plano de hospedagem.</span><span class="sxs-lookup"><span data-stu-id="20075-125">In hello **dependsOn** element, hello template defines hello web app as dependent on hello service hosting plan.</span></span> <span data-ttu-id="20075-126">Porque ele é dependente de saudação plano de hospedagem, Olá web app não é criado até concluir a saudação plano de hospedagem está sendo criado.</span><span class="sxs-lookup"><span data-stu-id="20075-126">Because it is dependent on hello hosting plan, hello web app is not created until hello hosting plan has finished being created.</span></span> <span data-ttu-id="20075-127">Olá **dependsOn** elemento é apenas uma ordem de implantação toospecify usado.</span><span class="sxs-lookup"><span data-stu-id="20075-127">hello **dependsOn** element is only used toospecify deployment order.</span></span> <span data-ttu-id="20075-128">Se você não marcar Olá web aplicativo como dependente de plano de hospedagem hello, o Azure Resource Manager tentará toocreate ambos os recursos no hello mesmo tempo e você poderá receber um erro se Olá web app for criado antes de saudação plano de hospedagem.</span><span class="sxs-lookup"><span data-stu-id="20075-128">If you do not mark hello web app as dependent on hello hosting plan, Azure Resource Mananger will attempt toocreate both resources at hello same time and you may receive an error if hello web app is created before hello hosting plan.</span></span>

<span data-ttu-id="20075-129">Olá web aplicativo também tem um recurso filho que é definido em **recursos** seção abaixo.</span><span class="sxs-lookup"><span data-stu-id="20075-129">hello web app also has a child resource which is defined in **resources** section below.</span></span> <span data-ttu-id="20075-130">Este recurso filho define o controle de origem para projeto Olá implantado com o aplicativo web de saudação.</span><span class="sxs-lookup"><span data-stu-id="20075-130">This child resource defines source control for hello project deployed with hello web app.</span></span> <span data-ttu-id="20075-131">Neste modelo, o controle de origem de saudação será vinculado tooa determinado repositório do GitHub.</span><span class="sxs-lookup"><span data-stu-id="20075-131">In this template, hello source control is linked tooa particular GitHub repository.</span></span> <span data-ttu-id="20075-132">repositório do GitHub Olá é definido com o código de saudação **"RepoUrl": "https://github.com/davidebbo-test/Mvc52Application.git"** pode embutir Olá URL do repositório quando desejar toocreate um modelo que implanta repetidamente um único projeto, exigindo o número mínimo de saudação de parâmetros.</span><span class="sxs-lookup"><span data-stu-id="20075-132">hello GitHub repository is defined with hello code **"RepoUrl":"https://github.com/davidebbo-test/Mvc52Application.git"** You might hard-code hello repository URL when you want toocreate a template that repeatedly deploys a single project while requiring hello minimum number of parameters.</span></span>
<span data-ttu-id="20075-133">Em vez de embutir em código Olá URL do repositório, você pode adicionar um parâmetro de URL do repositório hello e use esse valor para Olá **RepoUrl** propriedade.</span><span class="sxs-lookup"><span data-stu-id="20075-133">Instead of hard-coding hello repository URL, you can add a parameter for hello repository URL and use that value for hello **RepoUrl** property.</span></span>

    {
      "apiVersion": "2015-08-01",
      "name": "[parameters('siteName')]",
      "type": "Microsoft.Web/sites",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[resourceId('Microsoft.Web/serverfarms', parameters('hostingPlanName'))]"
      ],
      "properties": {
        "serverFarmId": "[parameters('hostingPlanName')]"
      },
      "resources": [
        {
          "apiVersion": "2015-08-01",
          "name": "web",
          "type": "sourcecontrols",
          "dependsOn": [
            "[resourceId('Microsoft.Web/Sites', parameters('siteName'))]"
          ],
          "properties": {
            "RepoUrl": "[parameters('repoURL')]",
            "branch": "[parameters('branch')]",
            "IsManualIntegration": true
          }
        }
      ]
    }

## <a name="commands-toorun-deployment"></a><span data-ttu-id="20075-134">Implantação de toorun de comandos</span><span class="sxs-lookup"><span data-stu-id="20075-134">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="20075-135">PowerShell</span><span class="sxs-lookup"><span data-stu-id="20075-135">PowerShell</span></span>
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json -siteName ExampleSite -hostingPlanName ExamplePlan -ResourceGroupName ExampleDeployGroup

### <a name="azure-cli"></a><span data-ttu-id="20075-136">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="20075-136">Azure CLI</span></span>

    azure group deployment create -g {resource-group-name} --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json

### <a name="azure-cli-20"></a><span data-ttu-id="20075-137">CLI do Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="20075-137">Azure CLI 2.0</span></span>

    az group deployment create -g {resource-group-name} --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json --parameters '@azuredeploy.parameters.json'

> [!NOTE] 
> <span data-ttu-id="20075-138">Para obter conteúdo do arquivo JSON de parâmetros hello, consulte [azuredeploy.parameters.json](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.parameters.json).</span><span class="sxs-lookup"><span data-stu-id="20075-138">For content of hello parameters JSON file, see [azuredeploy.parameters.json](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.parameters.json).</span></span>
>
>

