---
title: "Exemplo de Script do Azure PowerShell - Como criar um aplicativo Web e implantar o código do GitHub | Microsoft Docs"
description: "Exemplo de Script do Azure PowerShell - Como criar um aplicativo Web e implantar o código do GitHub"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 0f9c8bc5-3789-4eb3-8deb-ae6e2200795a
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: sample
ms.date: 03/20/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 1f7fc21dc12c334f5d347ae9918bd62945bede64
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-web-app-and-deploy-code-from-github"></a><span data-ttu-id="f88a7-103">Como criar um aplicativo Web e implantar o código do GitHub</span><span class="sxs-lookup"><span data-stu-id="f88a7-103">Create a web app and deploy code from GitHub</span></span>

<span data-ttu-id="f88a7-104">Este script de exemplo cria um aplicativo Web no serviço de aplicativo com seus recursos relacionados e, em seguida, implanta seu código de aplicativo Web de um repositório GitHub público (sem a implantação contínua).</span><span class="sxs-lookup"><span data-stu-id="f88a7-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code from a public GitHub repository (without continuous deployment).</span></span> <span data-ttu-id="f88a7-105">Para implantação do GitHub com implantação contínua, confira [Como criar um aplicativo Web com implantação contínua do GitHub](app-service-powershell-continuous-deployment-github.md).</span><span class="sxs-lookup"><span data-stu-id="f88a7-105">For GitHub deployment with continuous deployment, see [Create a web app with continuous deployment from GitHub](app-service-powershell-continuous-deployment-github.md).</span></span>

<span data-ttu-id="f88a7-106">Se necessário, instale o Azure PowerShell usando a instrução encontrada no [guia do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f88a7-106">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview).</span></span> <span data-ttu-id="f88a7-107">Além disso, você precisa de um link para o repositório GitHub que contém o código do aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="f88a7-107">Also, you need a link to GitHub repository that contains the web app code.</span></span>

## <a name="sample-script"></a><span data-ttu-id="f88a7-108">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="f88a7-108">Sample script</span></span>

<span data-ttu-id="f88a7-109">[!code-powershell[principal](../../../powershell_scripts/app-service/deploy-github/deploy-github.ps1?highlight=1-2 "Como criar um aplicativo Web e implantar o código do GitHub")]</span><span class="sxs-lookup"><span data-stu-id="f88a7-109">[!code-powershell[main](../../../powershell_scripts/app-service/deploy-github/deploy-github.ps1?highlight=1-2 "Create a web app and deploy code from GitHub")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="f88a7-110">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="f88a7-110">Clean up deployment</span></span> 

<span data-ttu-id="f88a7-111">Após a execução da amostra de script, o comando a seguir pode ser usado para remover o grupo de recursos, o aplicativo Web e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="f88a7-111">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="f88a7-112">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="f88a7-112">Script explanation</span></span>

<span data-ttu-id="f88a7-113">Este script usa os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="f88a7-113">This script uses the following commands.</span></span> <span data-ttu-id="f88a7-114">Cada comando na tabela redireciona para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="f88a7-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="f88a7-115">Command</span><span class="sxs-lookup"><span data-stu-id="f88a7-115">Command</span></span> | <span data-ttu-id="f88a7-116">Observações</span><span class="sxs-lookup"><span data-stu-id="f88a7-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="f88a7-117">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="f88a7-117">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="f88a7-118">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="f88a7-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="f88a7-119">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="f88a7-119">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="f88a7-120">Cria um Plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f88a7-120">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="f88a7-121">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="f88a7-121">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="f88a7-122">Cria um aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="f88a7-122">Creates a web app.</span></span> |
| [<span data-ttu-id="f88a7-123">Set-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="f88a7-123">Set-AzureRmResource</span></span>](/powershell/module/azurerm.resources/set-azurermresource) | <span data-ttu-id="f88a7-124">Modifica um recurso em um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="f88a7-124">Modifies a resource in a resource group.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="f88a7-125">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f88a7-125">Next steps</span></span>

<span data-ttu-id="f88a7-126">Para saber mais sobre o módulo do Azure PowerShell, confira a [Documentação do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f88a7-126">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="f88a7-127">Exemplos adicionais do Azure PowerShell para Aplicativos Web do Serviço de Aplicativo do Azure podem ser encontrados nos [exemplos do Azure PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="f88a7-127">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
