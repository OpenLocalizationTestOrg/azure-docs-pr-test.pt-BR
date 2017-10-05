---
title: "Exemplo de Script do Azure PowerShell - Atribuir um domínio personalizado para um aplicativo Web | Microsoft Docs"
description: "Exemplo de Script do Azure PowerShell - Atribuir um domínio personalizado para um aplicativo Web"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 356f5af9-f62e-411c-8b24-deba05214103
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: sample
ms.date: 03/20/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 6d25fe8098848fc69470c77e3200bee554c1f875
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="assign-a-custom-domain-to-a-web-app"></a><span data-ttu-id="e4358-103">Atribuir um domínio personalizado para um aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="e4358-103">Assign a custom domain to a web app</span></span>

<span data-ttu-id="e4358-104">Este script de exemplo cria um aplicativo Web no serviço de aplicativo com seus recursos relacionados e, em seguida, mapeia `www.<yourdomain>` a ele.</span><span class="sxs-lookup"><span data-stu-id="e4358-104">This sample script creates a web app in App Service with its related resources, and then maps `www.<yourdomain>` to it.</span></span> 

<span data-ttu-id="e4358-105">Se necessário, instale o Azure PowerShell usando a instrução encontrada no [guia do Azure PowerShell](/powershell/azure/overview) e, em seguida, execute `Login-AzureRmAccount` para criar uma conexão com o Azure.</span><span class="sxs-lookup"><span data-stu-id="e4358-105">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span> <span data-ttu-id="e4358-106">Além disso, você precisa ter acesso à página de configuração do DNS do registrador de domínios.</span><span class="sxs-lookup"><span data-stu-id="e4358-106">Also, you need to have access to your domain registrar's DNS configuration page.</span></span>

## <a name="sample-script"></a><span data-ttu-id="e4358-107">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="e4358-107">Sample script</span></span>

<span data-ttu-id="e4358-108">[!code-powershell[principal](../../../powershell_scripts/app-service/map-custom-domain/map-custom-domain.ps1?highlight=1 "Atribuir um domínio personalizado para um aplicativo Web")]</span><span class="sxs-lookup"><span data-stu-id="e4358-108">[!code-powershell[main](../../../powershell_scripts/app-service/map-custom-domain/map-custom-domain.ps1?highlight=1 "Assign a custom domain to a web app")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="e4358-109">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="e4358-109">Clean up deployment</span></span> 

<span data-ttu-id="e4358-110">Após a execução da amostra de script, o comando a seguir pode ser usado para remover o grupo de recursos, o aplicativo Web e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="e4358-110">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="e4358-111">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="e4358-111">Script explanation</span></span>

<span data-ttu-id="e4358-112">Este script usa os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="e4358-112">This script uses the following commands.</span></span> <span data-ttu-id="e4358-113">Cada comando na tabela redireciona para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="e4358-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="e4358-114">Command</span><span class="sxs-lookup"><span data-stu-id="e4358-114">Command</span></span> | <span data-ttu-id="e4358-115">Observações</span><span class="sxs-lookup"><span data-stu-id="e4358-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="e4358-116">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="e4358-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="e4358-117">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="e4358-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="e4358-118">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="e4358-118">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="e4358-119">Cria um Plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e4358-119">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="e4358-120">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="e4358-120">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="e4358-121">Cria um aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="e4358-121">Creates a web app.</span></span> |
| [<span data-ttu-id="e4358-122">Set-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="e4358-122">Set-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/set-azurermappserviceplan) | <span data-ttu-id="e4358-123">Modifica um plano do Serviço de Aplicativo para alterar seu tipo de preço.</span><span class="sxs-lookup"><span data-stu-id="e4358-123">Modifies an App Service plan to change its pricing tier.</span></span> |
| [<span data-ttu-id="e4358-124">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="e4358-124">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="e4358-125">Modifica a configuração de um aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="e4358-125">Modifies a web app's configuration.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e4358-126">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e4358-126">Next steps</span></span>

<span data-ttu-id="e4358-127">Para saber mais sobre o módulo do Azure PowerShell, confira a [Documentação do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e4358-127">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="e4358-128">Exemplos adicionais do Azure PowerShell para Aplicativos Web do Serviço de Aplicativo do Azure podem ser encontrados nos [exemplos do Azure PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="e4358-128">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
