---
title: "Exemplo de script do Azure PowerShell - criar um aplicativo Web com a implantação contínua do GitHub | Microsoft Docs"
description: "Exemplo de script do Azure PowerShell - criar um aplicativo Web com a implantação contínua do GitHub"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 42f901f8-02f7-4869-b22d-d99ef59f874c
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: sample
ms.date: 03/20/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: fc594a94bb64ceb88370be8617036a73402ade4e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-web-app-with-continuous-deployment-from-github"></a><span data-ttu-id="77944-103">Criar um aplicativo web com a implantação contínua do GitHub</span><span class="sxs-lookup"><span data-stu-id="77944-103">Create a web app with continuous deployment from GitHub</span></span>

<span data-ttu-id="77944-104">Este script de exemplo cria um aplicativo Web no serviço de aplicativo com seus recursos relacionados e, em seguida, define a implantação contínua de um repositório GitHub.</span><span class="sxs-lookup"><span data-stu-id="77944-104">This sample script creates a web app in App Service with its related resources, and then sets up continuous deployment from a GitHub repository.</span></span> <span data-ttu-id="77944-105">Para implantação do GitHub sem a implantação contínua, veja [Criar um aplicativo Web e implantar o código do GitHub](app-service-powershell-deploy-github.md).</span><span class="sxs-lookup"><span data-stu-id="77944-105">For GitHub deployment without continuous deployment, see [Create a web app and deploy code from GitHub](app-service-powershell-deploy-github.md).</span></span>

<span data-ttu-id="77944-106">Se necessário, instale o Azure PowerShell usando a instrução encontrada no [guia do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="77944-106">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview).</span></span> <span data-ttu-id="77944-107">Além disso, verifique se:</span><span class="sxs-lookup"><span data-stu-id="77944-107">Also, ensure that:</span></span>

- <span data-ttu-id="77944-108">Uma conexão com o Azure foi criado usando o comando `az login`.</span><span class="sxs-lookup"><span data-stu-id="77944-108">A connection with Azure has been created using the `az login` command.</span></span>
- <span data-ttu-id="77944-109">O código do aplicativo está em um repositório GitHub público ou privado que você possui.</span><span class="sxs-lookup"><span data-stu-id="77944-109">The application code is in a public or private GitHub repository that you own.</span></span>
- <span data-ttu-id="77944-110">Você [criou um token de acesso em sua conta do GitHub](https://help.github.com/articles/creating-an-access-token-for-command-line-use/).</span><span class="sxs-lookup"><span data-stu-id="77944-110">You have [created an access token in your GitHub account](https://help.github.com/articles/creating-an-access-token-for-command-line-use/).</span></span>

## <a name="sample-script"></a><span data-ttu-id="77944-111">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="77944-111">Sample script</span></span>

<span data-ttu-id="77944-112">[!code-powershell[principal](../../../powershell_scripts/app-service/deploy-github-continuous/deploy-github-continuous.ps1?highlight=1-2 "Criar um aplicativo web com a implantação contínua do GitHub")]</span><span class="sxs-lookup"><span data-stu-id="77944-112">[!code-powershell[main](../../../powershell_scripts/app-service/deploy-github-continuous/deploy-github-continuous.ps1?highlight=1-2 "Create a web app with continuous deployment from GitHub")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="77944-113">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="77944-113">Clean up deployment</span></span> 

<span data-ttu-id="77944-114">Após a execução da amostra de script, o comando a seguir pode ser usado para remover o grupo de recursos, o aplicativo Web e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="77944-114">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="77944-115">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="77944-115">Script explanation</span></span>

<span data-ttu-id="77944-116">Este script usa os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="77944-116">This script uses the following commands.</span></span> <span data-ttu-id="77944-117">Cada comando na tabela redireciona para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="77944-117">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="77944-118">Command</span><span class="sxs-lookup"><span data-stu-id="77944-118">Command</span></span> | <span data-ttu-id="77944-119">Observações</span><span class="sxs-lookup"><span data-stu-id="77944-119">Notes</span></span> |
|---|---|
| [<span data-ttu-id="77944-120">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="77944-120">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="77944-121">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="77944-121">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="77944-122">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="77944-122">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="77944-123">Cria um Plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="77944-123">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="77944-124">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="77944-124">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="77944-125">Cria um aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="77944-125">Creates a web app.</span></span> |
| [<span data-ttu-id="77944-126">Set-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="77944-126">Set-AzureRmResource</span></span>](/powershell/module/azurerm.resources/set-azurermresource) | <span data-ttu-id="77944-127">Modifica um recurso em um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="77944-127">Modifies a resource in a resource group.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="77944-128">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="77944-128">Next steps</span></span>

<span data-ttu-id="77944-129">Para saber mais sobre o módulo do Azure PowerShell, confira a [Documentação do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="77944-129">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="77944-130">Exemplos adicionais do Azure PowerShell para Aplicativos Web do Serviço de Aplicativo do Azure podem ser encontrados nos [exemplos do Azure PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="77944-130">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
