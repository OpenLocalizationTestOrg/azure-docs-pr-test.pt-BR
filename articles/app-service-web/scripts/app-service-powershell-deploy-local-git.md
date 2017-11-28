---
title: "aaaAzure exemplo de Script do PowerShell - criar um aplicativo web e implantar o código de um repositório Git local | Microsoft Docs"
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
ms.openlocfilehash: a90996658bf0b609315460324d0dcd3a411a6512
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-and-deploy-code-from-a-local-git-repository"></a><span data-ttu-id="ba439-103">Criar um aplicativo Web e implantar o código de um repositório local Git</span><span class="sxs-lookup"><span data-stu-id="ba439-103">Create a web app and deploy code from a local Git repository</span></span>

<span data-ttu-id="ba439-104">Este script de exemplo cria um aplicativo Web no serviço de aplicativo com seus recursos relacionados e, em seguida, implanta seu código de aplicativo da web em um repositório Git local.</span><span class="sxs-lookup"><span data-stu-id="ba439-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code in a local Git repository.</span></span>

<span data-ttu-id="ba439-105">Se necessário, instale Olá PowerShell do Azure usando a instrução Olá encontrado no hello [guia do PowerShell do Azure](/powershell/azure/overview)e, em seguida, execute `Login-AzureRmAccount` toocreate uma conexão com o Azure.</span><span class="sxs-lookup"><span data-stu-id="ba439-105">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span> <span data-ttu-id="ba439-106">Além disso, o código do aplicativo precisa toobe confirmada em um repositório Git local.</span><span class="sxs-lookup"><span data-stu-id="ba439-106">Also, your application code needs toobe committed into a local Git repository.</span></span>

## <a name="sample-script"></a><span data-ttu-id="ba439-107">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="ba439-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/deploy-local-git/deploy-local-git.ps1?highlight=1 "Create a web app and deploy code from a local Git repository")]

## <a name="clean-up-deployment"></a><span data-ttu-id="ba439-108">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="ba439-108">Clean up deployment</span></span> 

<span data-ttu-id="ba439-109">Após a execução do exemplo de script hello, Olá comando a seguir pode ser usado tooremove grupo de recursos de saudação, aplicativo web e recursos todos relacionados.</span><span class="sxs-lookup"><span data-stu-id="ba439-109">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="ba439-110">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="ba439-110">Script explanation</span></span>

<span data-ttu-id="ba439-111">Esse script usa Olá comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="ba439-111">This script uses hello following commands.</span></span> <span data-ttu-id="ba439-112">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="ba439-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="ba439-113">Command</span><span class="sxs-lookup"><span data-stu-id="ba439-113">Command</span></span> | <span data-ttu-id="ba439-114">Observações</span><span class="sxs-lookup"><span data-stu-id="ba439-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="ba439-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="ba439-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="ba439-116">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="ba439-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="ba439-117">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="ba439-117">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="ba439-118">Cria um Plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ba439-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="ba439-119">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="ba439-119">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="ba439-120">Cria um aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="ba439-120">Creates a web app.</span></span> |
| [<span data-ttu-id="ba439-121">Set-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="ba439-121">Set-AzureRmResource</span></span>](/powershell/module/azurerm.resources/set-azurermresource) | <span data-ttu-id="ba439-122">Modifica um recurso em um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="ba439-122">Modifies a resource in a resource group.</span></span> |
| [<span data-ttu-id="ba439-123">Get-AzureRmWebAppPublishingProfile</span><span class="sxs-lookup"><span data-stu-id="ba439-123">Get-AzureRmWebAppPublishingProfile</span></span>](/powershell/module/azurerm.websites/get-azurermwebapppublishingprofile) | <span data-ttu-id="ba439-124">Obtenha perfis de publicação do aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="ba439-124">Get a web app's publishing profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ba439-125">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ba439-125">Next steps</span></span>

<span data-ttu-id="ba439-126">Para obter mais informações sobre o módulo do PowerShell do Azure hello, consulte [documentação do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ba439-126">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="ba439-127">Exemplos adicionais do Powershell do Azure para aplicativos de Web do serviço de aplicativo do Azure podem ser encontrados no hello [exemplos do PowerShell do Azure](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="ba439-127">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
