---
title: Exemplo de Script do Azure PowerShell - Dimensionar um aplicativo Web manualmente | Microsoft Docs
description: Exemplo de Script do Azure PowerShell - Dimensionar um aplicativo Web manualmente
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: de5d4285-9c7d-4735-a695-288264047375
ms.service: app-service
ms.devlang: multiple
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 03/20/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: e99dfc02b6ab4123cd5f95997285dca5cb686380
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="scale-a-web-app-manually"></a><span data-ttu-id="d60e6-103">Dimensionar manualmente um aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="d60e6-103">Scale a web app manually</span></span>

<span data-ttu-id="d60e6-104">Nesse cenário, você aprenderá a criar um grupo de recursos, o aplicativo Web e o Plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d60e6-104">In this scenario you will learn to create a resource group, app service plan and web app.</span></span> <span data-ttu-id="d60e6-105">Em seguida, dimensionará o Plano do Serviço de Aplicativo de uma única instância para várias instâncias.</span><span class="sxs-lookup"><span data-stu-id="d60e6-105">You will then scale the App Service Plan from a single instance to multiple instances.</span></span>

<span data-ttu-id="d60e6-106">Se necessário, instale o Azure PowerShell usando a instrução encontrada no [guia do Azure PowerShell](/powershell/azure/overview) e, em seguida, execute `Login-AzureRmAccount` para criar uma conexão com o Azure.</span><span class="sxs-lookup"><span data-stu-id="d60e6-106">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="d60e6-107">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="d60e6-107">Sample script</span></span>

<span data-ttu-id="d60e6-108">[!code-powershell[principal](../../../powershell_scripts/app-service/scale-manual/scale-manual.ps1 "Dimensionar manualmente um aplicativo Web")]</span><span class="sxs-lookup"><span data-stu-id="d60e6-108">[!code-powershell[main](../../../powershell_scripts/app-service/scale-manual/scale-manual.ps1 "Scale a web app manually")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="d60e6-109">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="d60e6-109">Clean up deployment</span></span> 

<span data-ttu-id="d60e6-110">Após a execução da amostra de script, o comando a seguir pode ser usado para remover o grupo de recursos, o aplicativo Web e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="d60e6-110">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="d60e6-111">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="d60e6-111">Script explanation</span></span>

<span data-ttu-id="d60e6-112">Este script usa os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="d60e6-112">This script uses the following commands.</span></span> <span data-ttu-id="d60e6-113">Cada comando na tabela redireciona para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="d60e6-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="d60e6-114">Command</span><span class="sxs-lookup"><span data-stu-id="d60e6-114">Command</span></span> | <span data-ttu-id="d60e6-115">Observações</span><span class="sxs-lookup"><span data-stu-id="d60e6-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="d60e6-116">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="d60e6-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="d60e6-117">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="d60e6-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="d60e6-118">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="d60e6-118">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="d60e6-119">Cria um Plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d60e6-119">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="d60e6-120">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="d60e6-120">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="d60e6-121">Cria um aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="d60e6-121">Creates a web app.</span></span> |
| [<span data-ttu-id="d60e6-122">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="d60e6-122">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="d60e6-123">Modifica a configuração de um aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="d60e6-123">Modifies a web app's configuration.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="d60e6-124">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d60e6-124">Next steps</span></span>

<span data-ttu-id="d60e6-125">Para saber mais sobre o módulo do Azure PowerShell, confira a [Documentação do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d60e6-125">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="d60e6-126">Exemplos adicionais do Azure PowerShell para Aplicativos Web do Serviço de Aplicativo do Azure podem ser encontrados nos [exemplos do Azure PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="d60e6-126">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
