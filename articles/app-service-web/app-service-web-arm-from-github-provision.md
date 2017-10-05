---
title: "Implantar um aplicativo Web vinculado a um repositório GitHub | Microsoft Docs"
description: "Use um modelo do Azure Resource Manager para implantar um aplicativo Web que contém um projeto de um repositório GitHub."
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
ms.openlocfilehash: 77064802814296d0c21f004534e4264d2f97252e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-a-web-app-linked-to-a-github-repository"></a><span data-ttu-id="4241a-103">Implantar um aplicativo Web vinculado a um repositório GitHub</span><span class="sxs-lookup"><span data-stu-id="4241a-103">Deploy a web app linked to a GitHub repository</span></span>
<span data-ttu-id="4241a-104">Neste tópico, você aprenderá a criar um modelo do Azure Resource Manager que implanta um aplicativo Web vinculado a um projeto em um repositório GitHub.</span><span class="sxs-lookup"><span data-stu-id="4241a-104">In this topic, you will learn how to create an Azure Resource Manager template that deploys a web app that is linked to a project in a GitHub repository.</span></span> <span data-ttu-id="4241a-105">Você aprenderá como definir quais recursos são implantados e como definir os parâmetros que são especificados quando a implantação é executada.</span><span class="sxs-lookup"><span data-stu-id="4241a-105">You will learn how to define which resources are deployed and how to define parameters that are specified when the deployment is executed.</span></span> <span data-ttu-id="4241a-106">Você pode usar este modelo para suas próprias implantações ou personalizá-lo para atender às suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="4241a-106">You can use this template for your own deployments, or customize it to meet your requirements.</span></span>

<span data-ttu-id="4241a-107">Para obter mais informações sobre a criação de modelos, consulte [Criação de Modelos do Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="4241a-107">For more information about creating templates, see [Authoring Azure Resource Manager Templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="4241a-108">Para obter o modelo completo, consulte [Modelo de aplicativo Web vinculado ao GitHub](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.json).</span><span class="sxs-lookup"><span data-stu-id="4241a-108">For the complete template, see [Web App Linked to GitHub template](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.json).</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="what-you-will-deploy"></a><span data-ttu-id="4241a-109">O que você implantará</span><span class="sxs-lookup"><span data-stu-id="4241a-109">What you will deploy</span></span>
<span data-ttu-id="4241a-110">Com esse modelo, você implantará um aplicativo Web que contém o código de um projeto no GitHub.</span><span class="sxs-lookup"><span data-stu-id="4241a-110">With this template, you will deploy a web app that contains the code from a project in GitHub.</span></span>

<span data-ttu-id="4241a-111">Para executar a implantação automaticamente, clique no seguinte botão:</span><span class="sxs-lookup"><span data-stu-id="4241a-111">To run the deployment automatically, click the following button:</span></span>

<span data-ttu-id="4241a-112">[![Implantar no Azure](./media/app-service-web-arm-from-github-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-github-deploy%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="4241a-112">[![Deploy to Azure](./media/app-service-web-arm-from-github-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-github-deploy%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="4241a-113">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="4241a-113">Parameters</span></span>
[!INCLUDE [app-service-web-deploy-web-parameters](../../includes/app-service-web-deploy-web-parameters.md)]

### <a name="repourl"></a><span data-ttu-id="4241a-114">repoURL</span><span class="sxs-lookup"><span data-stu-id="4241a-114">repoURL</span></span>
<span data-ttu-id="4241a-115">A URL para o repositório GitHub que contém o projeto a ser implantado.</span><span class="sxs-lookup"><span data-stu-id="4241a-115">The URL for GitHub repository that contains the project to deploy.</span></span> <span data-ttu-id="4241a-116">Esse parâmetro contém um valor padrão, mas esse valor é destinado apenas a mostrar como fornecer a URL para o repositório.</span><span class="sxs-lookup"><span data-stu-id="4241a-116">This parameter contains a default value but this value is only intended to show you how to provide the URL for repository.</span></span> <span data-ttu-id="4241a-117">Você pode usar esse valor ao testar o modelo, mas será conveniente fornecer a URL de seu próprio repositório ao trabalhar com o modelo.</span><span class="sxs-lookup"><span data-stu-id="4241a-117">You can use this value when testing the template but you will want to provide the URL your own repository when working with the template.</span></span>

    "repoURL": {
        "type": "string",
        "defaultValue": "https://github.com/davidebbo-test/Mvc52Application.git"
    }

### <a name="branch"></a><span data-ttu-id="4241a-118">branch</span><span class="sxs-lookup"><span data-stu-id="4241a-118">branch</span></span>
<span data-ttu-id="4241a-119">A ramificação do repositório a ser usada ao implantar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4241a-119">The branch of the repository to use when deploying the application.</span></span> <span data-ttu-id="4241a-120">O valor padrão é o mestre, mas você pode fornecer o nome de qualquer ramificação no repositório que deseja implantar.</span><span class="sxs-lookup"><span data-stu-id="4241a-120">The default value is master, but you can provide the name of any branch in the repository that you wish to deploy.</span></span>

    "branch": {
        "type": "string",
        "defaultValue": "master"
    }

## <a name="resources-to-deploy"></a><span data-ttu-id="4241a-121">Recursos a implantar</span><span class="sxs-lookup"><span data-stu-id="4241a-121">Resources to deploy</span></span>
[!INCLUDE [app-service-web-deploy-web-host](../../includes/app-service-web-deploy-web-host.md)]

### <a name="web-app"></a><span data-ttu-id="4241a-122">Aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="4241a-122">Web app</span></span>
<span data-ttu-id="4241a-123">Cria o aplicativo Web vinculado ao projeto no GitHub.</span><span class="sxs-lookup"><span data-stu-id="4241a-123">Creates the web app that is linked to the project in GitHub.</span></span> 

<span data-ttu-id="4241a-124">Especifique o nome do aplicativo Web por meio do parâmetro **siteName** e o local do aplicativo Web por meio do parâmetro **siteLocation**.</span><span class="sxs-lookup"><span data-stu-id="4241a-124">You specify the name of the web app through the **siteName** parameter, and the location of the web app through the **siteLocation** parameter.</span></span> <span data-ttu-id="4241a-125">No elemento **dependsOn** , o modelo define o aplicativo Web como dependente do plano de hospedagem do serviço.</span><span class="sxs-lookup"><span data-stu-id="4241a-125">In the **dependsOn** element, the template defines the web app as dependent on the service hosting plan.</span></span> <span data-ttu-id="4241a-126">Como depende do plano de hospedagem, o aplicativo Web não é criado até a conclusão da criação do plano de hospedagem.</span><span class="sxs-lookup"><span data-stu-id="4241a-126">Because it is dependent on the hosting plan, the web app is not created until the hosting plan has finished being created.</span></span> <span data-ttu-id="4241a-127">O elemento **dependsOn** só é usado para especificar a ordem de implantação.</span><span class="sxs-lookup"><span data-stu-id="4241a-127">The **dependsOn** element is only used to specify deployment order.</span></span> <span data-ttu-id="4241a-128">Se você não marcar o aplicativo Web como dependente do plano de hospedagem, o Azure Resource Manager tentará criar ambos os recursos ao mesmo tempo e você receberá um erro se o aplicativo Web for criado antes do plano de hospedagem.</span><span class="sxs-lookup"><span data-stu-id="4241a-128">If you do not mark the web app as dependent on the hosting plan, Azure Resource Mananger will attempt to create both resources at the same time and you may receive an error if the web app is created before the hosting plan.</span></span>

<span data-ttu-id="4241a-129">O aplicativo Web também tem um recurso filho que é definido na seção de **recursos** a seguir.</span><span class="sxs-lookup"><span data-stu-id="4241a-129">The web app also has a child resource which is defined in **resources** section below.</span></span> <span data-ttu-id="4241a-130">Esse recurso filho define o controle do código-fonte para o projeto implantado com o aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="4241a-130">This child resource defines source control for the project deployed with the web app.</span></span> <span data-ttu-id="4241a-131">Nesse modelo, o controle do código-fonte está vinculado a um repositório GitHub específico.</span><span class="sxs-lookup"><span data-stu-id="4241a-131">In this template, the source control is linked to a particular GitHub repository.</span></span> <span data-ttu-id="4241a-132">O repositório GitHub é definido com o código **"RepoUrl":"https://github.com/davidebbo-test/Mvc52Application.git"** Você poderá embutir a URL do repositório quando quiser criar um modelo que implanta repetidamente um único projeto, exigindo o número mínimo de parâmetros.</span><span class="sxs-lookup"><span data-stu-id="4241a-132">The GitHub repository is defined with the code **"RepoUrl":"https://github.com/davidebbo-test/Mvc52Application.git"** You might hard-code the repository URL when you want to create a template that repeatedly deploys a single project while requiring the minimum number of parameters.</span></span>
<span data-ttu-id="4241a-133">Em vez de embutir a URL do repositório, você pode adicionar um parâmetro para a URL do repositório e usar esse valor para a propriedade **RepoUrl** .</span><span class="sxs-lookup"><span data-stu-id="4241a-133">Instead of hard-coding the repository URL, you can add a parameter for the repository URL and use that value for the **RepoUrl** property.</span></span>

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

## <a name="commands-to-run-deployment"></a><span data-ttu-id="4241a-134">Comandos para executar a implantação</span><span class="sxs-lookup"><span data-stu-id="4241a-134">Commands to run deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="4241a-135">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4241a-135">PowerShell</span></span>
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json -siteName ExampleSite -hostingPlanName ExamplePlan -ResourceGroupName ExampleDeployGroup

### <a name="azure-cli"></a><span data-ttu-id="4241a-136">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="4241a-136">Azure CLI</span></span>

    azure group deployment create -g {resource-group-name} --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json

### <a name="azure-cli-20"></a><span data-ttu-id="4241a-137">CLI do Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="4241a-137">Azure CLI 2.0</span></span>

    az group deployment create -g {resource-group-name} --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-web-app-github-deploy/azuredeploy.json --parameters '@azuredeploy.parameters.json'

> [!NOTE] 
> <span data-ttu-id="4241a-138">Para obter o conteúdo dos parâmetros no arquivo JSON, veja [azuredeploy.parameters.json](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.parameters.json).</span><span class="sxs-lookup"><span data-stu-id="4241a-138">For content of the parameters JSON file, see [azuredeploy.parameters.json](https://github.com/Azure/azure-quickstart-templates/blob/master/201-web-app-github-deploy/azuredeploy.parameters.json).</span></span>
>
>

