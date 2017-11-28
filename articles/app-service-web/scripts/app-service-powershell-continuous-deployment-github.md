---
title: "aaaAzure exemplo de Script do PowerShell - criar um aplicativo web com implantação contínua do GitHub | Microsoft Docs"
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
ms.openlocfilehash: c2f260a06bce9af6d11ad4033931d3dc18da8f49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-with-continuous-deployment-from-github"></a><span data-ttu-id="61d8c-103">Criar um aplicativo web com a implantação contínua do GitHub</span><span class="sxs-lookup"><span data-stu-id="61d8c-103">Create a web app with continuous deployment from GitHub</span></span>

<span data-ttu-id="61d8c-104">Este script de exemplo cria um aplicativo Web no serviço de aplicativo com seus recursos relacionados e, em seguida, define a implantação contínua de um repositório GitHub.</span><span class="sxs-lookup"><span data-stu-id="61d8c-104">This sample script creates a web app in App Service with its related resources, and then sets up continuous deployment from a GitHub repository.</span></span> <span data-ttu-id="61d8c-105">Para implantação do GitHub sem a implantação contínua, veja [Criar um aplicativo Web e implantar o código do GitHub](app-service-powershell-deploy-github.md).</span><span class="sxs-lookup"><span data-stu-id="61d8c-105">For GitHub deployment without continuous deployment, see [Create a web app and deploy code from GitHub](app-service-powershell-deploy-github.md).</span></span>

<span data-ttu-id="61d8c-106">Se necessário, instale Olá PowerShell do Azure usando a instrução Olá encontrado no hello [guia do PowerShell do Azure](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="61d8c-106">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview).</span></span> <span data-ttu-id="61d8c-107">Além disso, verifique se:</span><span class="sxs-lookup"><span data-stu-id="61d8c-107">Also, ensure that:</span></span>

- <span data-ttu-id="61d8c-108">Foi criada uma conexão com o Azure usando Olá `az login` comando.</span><span class="sxs-lookup"><span data-stu-id="61d8c-108">A connection with Azure has been created using hello `az login` command.</span></span>
- <span data-ttu-id="61d8c-109">código do aplicativo Hello está em um repositório GitHub público ou privado que você possui.</span><span class="sxs-lookup"><span data-stu-id="61d8c-109">hello application code is in a public or private GitHub repository that you own.</span></span>
- <span data-ttu-id="61d8c-110">Você [criou um token de acesso em sua conta do GitHub](https://help.github.com/articles/creating-an-access-token-for-command-line-use/).</span><span class="sxs-lookup"><span data-stu-id="61d8c-110">You have [created an access token in your GitHub account](https://help.github.com/articles/creating-an-access-token-for-command-line-use/).</span></span>

## <a name="sample-script"></a><span data-ttu-id="61d8c-111">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="61d8c-111">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/deploy-github-continuous/deploy-github-continuous.ps1?highlight=1-2 "Create a web app with continuous deployment from GitHub")]

## <a name="clean-up-deployment"></a><span data-ttu-id="61d8c-112">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="61d8c-112">Clean up deployment</span></span> 

<span data-ttu-id="61d8c-113">Após a execução do exemplo de script hello, Olá comando a seguir pode ser usado tooremove grupo de recursos de saudação, aplicativo web e recursos todos relacionados.</span><span class="sxs-lookup"><span data-stu-id="61d8c-113">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="61d8c-114">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="61d8c-114">Script explanation</span></span>

<span data-ttu-id="61d8c-115">Esse script usa Olá comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="61d8c-115">This script uses hello following commands.</span></span> <span data-ttu-id="61d8c-116">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="61d8c-116">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="61d8c-117">Command</span><span class="sxs-lookup"><span data-stu-id="61d8c-117">Command</span></span> | <span data-ttu-id="61d8c-118">Observações</span><span class="sxs-lookup"><span data-stu-id="61d8c-118">Notes</span></span> |
|---|---|
| [<span data-ttu-id="61d8c-119">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="61d8c-119">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="61d8c-120">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="61d8c-120">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="61d8c-121">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="61d8c-121">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="61d8c-122">Cria um Plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="61d8c-122">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="61d8c-123">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="61d8c-123">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="61d8c-124">Cria um aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="61d8c-124">Creates a web app.</span></span> |
| [<span data-ttu-id="61d8c-125">Set-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="61d8c-125">Set-AzureRmResource</span></span>](/powershell/module/azurerm.resources/set-azurermresource) | <span data-ttu-id="61d8c-126">Modifica um recurso em um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="61d8c-126">Modifies a resource in a resource group.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="61d8c-127">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="61d8c-127">Next steps</span></span>

<span data-ttu-id="61d8c-128">Para obter mais informações sobre o módulo do PowerShell do Azure hello, consulte [documentação do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="61d8c-128">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="61d8c-129">Exemplos adicionais do Powershell do Azure para aplicativos de Web do serviço de aplicativo do Azure podem ser encontrados no hello [exemplos do PowerShell do Azure](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="61d8c-129">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
