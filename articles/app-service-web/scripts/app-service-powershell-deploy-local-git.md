---
title: "Exemplo de Script do Azure PowerShell - criar um aplicativo Web e implantar o código de um repositório Git local | Microsoft Docs"
description: "Exemplo de Script do Azure PowerShell - criar um aplicativo Web e implantar o código de um repositório Git local"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 5a927f23-8e70-45fd-9aae-980d4e7a007d
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: sample
ms.date: 03/20/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 855b8c643bf2a742e763bda2e2c21c6a86331aac
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-web-app-and-deploy-code-from-a-local-git-repository"></a><span data-ttu-id="20ad8-103">Criar um aplicativo Web e implantar o código de um repositório local Git</span><span class="sxs-lookup"><span data-stu-id="20ad8-103">Create a web app and deploy code from a local Git repository</span></span>

<span data-ttu-id="20ad8-104">Este script de exemplo cria um aplicativo Web no serviço de aplicativo com seus recursos relacionados e, em seguida, implanta seu código de aplicativo da web em um repositório Git local.</span><span class="sxs-lookup"><span data-stu-id="20ad8-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code in a local Git repository.</span></span>

<span data-ttu-id="20ad8-105">Se necessário, instale o Azure PowerShell usando a instrução encontrada no [guia do Azure PowerShell](/powershell/azure/overview) e, em seguida, execute `Login-AzureRmAccount` para criar uma conexão com o Azure.</span><span class="sxs-lookup"><span data-stu-id="20ad8-105">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span> <span data-ttu-id="20ad8-106">Além disso, o código do aplicativo precisa ser confirmado em um repositório Git local.</span><span class="sxs-lookup"><span data-stu-id="20ad8-106">Also, your application code needs to be committed into a local Git repository.</span></span>

## <a name="sample-script"></a><span data-ttu-id="20ad8-107">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="20ad8-107">Sample script</span></span>

<span data-ttu-id="20ad8-108">[!code-powershell[principal](../../../powershell_scripts/app-service/deploy-local-git/deploy-local-git.ps1?highlight=1 "Criar um aplicativo Web e implantar o código de um repositório local Git")]</span><span class="sxs-lookup"><span data-stu-id="20ad8-108">[!code-powershell[main](../../../powershell_scripts/app-service/deploy-local-git/deploy-local-git.ps1?highlight=1 "Create a web app and deploy code from a local Git repository")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="20ad8-109">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="20ad8-109">Clean up deployment</span></span> 

<span data-ttu-id="20ad8-110">Após a execução da amostra de script, o comando a seguir pode ser usado para remover o grupo de recursos, o aplicativo Web e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="20ad8-110">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="20ad8-111">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="20ad8-111">Script explanation</span></span>

<span data-ttu-id="20ad8-112">Este script usa os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="20ad8-112">This script uses the following commands.</span></span> <span data-ttu-id="20ad8-113">Cada comando na tabela redireciona para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="20ad8-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="20ad8-114">Command</span><span class="sxs-lookup"><span data-stu-id="20ad8-114">Command</span></span> | <span data-ttu-id="20ad8-115">Observações</span><span class="sxs-lookup"><span data-stu-id="20ad8-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="20ad8-116">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="20ad8-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="20ad8-117">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="20ad8-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="20ad8-118">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="20ad8-118">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="20ad8-119">Cria um Plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="20ad8-119">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="20ad8-120">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="20ad8-120">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="20ad8-121">Cria um aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="20ad8-121">Creates a web app.</span></span> |
| [<span data-ttu-id="20ad8-122">Set-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="20ad8-122">Set-AzureRmResource</span></span>](/powershell/module/azurerm.resources/set-azurermresource) | <span data-ttu-id="20ad8-123">Modifica um recurso em um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="20ad8-123">Modifies a resource in a resource group.</span></span> |
| [<span data-ttu-id="20ad8-124">Get-AzureRmWebAppPublishingProfile</span><span class="sxs-lookup"><span data-stu-id="20ad8-124">Get-AzureRmWebAppPublishingProfile</span></span>](/powershell/module/azurerm.websites/get-azurermwebapppublishingprofile) | <span data-ttu-id="20ad8-125">Obtenha perfis de publicação do aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="20ad8-125">Get a web app's publishing profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="20ad8-126">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="20ad8-126">Next steps</span></span>

<span data-ttu-id="20ad8-127">Para saber mais sobre o módulo do Azure PowerShell, confira a [Documentação do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="20ad8-127">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="20ad8-128">Exemplos adicionais do Azure PowerShell para Aplicativos Web do Serviço de Aplicativo do Azure podem ser encontrados nos [exemplos do Azure PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="20ad8-128">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
