---
title: "aaaAzure exemplo de Script do PowerShell - criar um aplicativo web e implantar o código do GitHub | Microsoft Docs"
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
ms.openlocfilehash: 9a28f9cb01b71c86fa0a3f1d0a6761fc3d45d43b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-and-deploy-code-from-github"></a><span data-ttu-id="c4f65-103">Como criar um aplicativo Web e implantar o código do GitHub</span><span class="sxs-lookup"><span data-stu-id="c4f65-103">Create a web app and deploy code from GitHub</span></span>

<span data-ttu-id="c4f65-104">Este script de exemplo cria um aplicativo Web no serviço de aplicativo com seus recursos relacionados e, em seguida, implanta seu código de aplicativo Web de um repositório GitHub público (sem a implantação contínua).</span><span class="sxs-lookup"><span data-stu-id="c4f65-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code from a public GitHub repository (without continuous deployment).</span></span> <span data-ttu-id="c4f65-105">Para implantação do GitHub com implantação contínua, confira [Como criar um aplicativo Web com implantação contínua do GitHub](app-service-powershell-continuous-deployment-github.md).</span><span class="sxs-lookup"><span data-stu-id="c4f65-105">For GitHub deployment with continuous deployment, see [Create a web app with continuous deployment from GitHub](app-service-powershell-continuous-deployment-github.md).</span></span>

<span data-ttu-id="c4f65-106">Se necessário, instale Olá PowerShell do Azure usando a instrução Olá encontrado no hello [guia do PowerShell do Azure](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c4f65-106">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview).</span></span> <span data-ttu-id="c4f65-107">Além disso, você precisa de um repositório de tooGitHub de link que contém o código de aplicativo da web hello.</span><span class="sxs-lookup"><span data-stu-id="c4f65-107">Also, you need a link tooGitHub repository that contains hello web app code.</span></span>

## <a name="sample-script"></a><span data-ttu-id="c4f65-108">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="c4f65-108">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/deploy-github/deploy-github.ps1?highlight=1-2 "Create a web app and deploy code from GitHub")]

## <a name="clean-up-deployment"></a><span data-ttu-id="c4f65-109">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="c4f65-109">Clean up deployment</span></span> 

<span data-ttu-id="c4f65-110">Após a execução do exemplo de script hello, Olá comando a seguir pode ser usado tooremove grupo de recursos de saudação, aplicativo web e recursos todos relacionados.</span><span class="sxs-lookup"><span data-stu-id="c4f65-110">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="c4f65-111">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="c4f65-111">Script explanation</span></span>

<span data-ttu-id="c4f65-112">Esse script usa Olá comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="c4f65-112">This script uses hello following commands.</span></span> <span data-ttu-id="c4f65-113">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="c4f65-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="c4f65-114">Command</span><span class="sxs-lookup"><span data-stu-id="c4f65-114">Command</span></span> | <span data-ttu-id="c4f65-115">Observações</span><span class="sxs-lookup"><span data-stu-id="c4f65-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c4f65-116">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="c4f65-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="c4f65-117">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="c4f65-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="c4f65-118">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="c4f65-118">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="c4f65-119">Cria um Plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c4f65-119">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="c4f65-120">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="c4f65-120">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="c4f65-121">Cria um aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="c4f65-121">Creates a web app.</span></span> |
| [<span data-ttu-id="c4f65-122">Set-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="c4f65-122">Set-AzureRmResource</span></span>](/powershell/module/azurerm.resources/set-azurermresource) | <span data-ttu-id="c4f65-123">Modifica um recurso em um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="c4f65-123">Modifies a resource in a resource group.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c4f65-124">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c4f65-124">Next steps</span></span>

<span data-ttu-id="c4f65-125">Para obter mais informações sobre o módulo do PowerShell do Azure hello, consulte [documentação do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c4f65-125">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="c4f65-126">Exemplos adicionais do Powershell do Azure para aplicativos de Web do serviço de aplicativo do Azure podem ser encontrados no hello [exemplos do PowerShell do Azure](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="c4f65-126">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
