---
title: Exemplo de Script do Azure PowerShell - Dimensionar um aplicativo Web em todo o mundo com uma arquitetura de alta disponibilidade | Microsoft Docs
description: Exemplo de Script do Azure PowerShell - Dimensionar um aplicativo Web em todo o mundo com uma arquitetura de alta disponibilidade
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 470f0129-1efe-462c-a029-5c66e04158a8
ms.service: app-service
ms.devlang: multiple
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 03/20/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 9acd1cf4d1a5705811c4dedc545505ec0ac55fc7
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="scale-a-web-app-worldwide-with-a-high-availability-architecture"></a><span data-ttu-id="d1af7-103">Escalar um aplicativo Web em todo o mundo com uma arquitetura de alta disponibilidade</span><span class="sxs-lookup"><span data-stu-id="d1af7-103">Scale a web app worldwide with a high-availability architecture</span></span>

<span data-ttu-id="d1af7-104">Nesse cenário, você criará um grupo de recursos, dois planos de serviço de aplicativo, dois aplicativos web, um perfil do Gerenciador de tráfego e dois pontos de extremidade de Gerenciador de tráfego.</span><span class="sxs-lookup"><span data-stu-id="d1af7-104">In this scenario you will create a resource group, two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> <span data-ttu-id="d1af7-105">Depois que o exercício for concluído, você terá uma alta disponibilidade a arquitetura que permite que fornece disponibilidade global do seu aplicativo Web com base na menor latência de rede.</span><span class="sxs-lookup"><span data-stu-id="d1af7-105">Once the exercise is complete you will have a high-available architecture which allows provides global availability of your web app based on the lowest network latency.</span></span>

<span data-ttu-id="d1af7-106">Se necessário, instale o Azure PowerShell usando a instrução encontrada no [guia do Azure PowerShell](/powershell/azure/overview) e, em seguida, execute `Login-AzureRmAccount` para criar uma conexão com o Azure.</span><span class="sxs-lookup"><span data-stu-id="d1af7-106">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="d1af7-107">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="d1af7-107">Sample script</span></span>

<span data-ttu-id="d1af7-108">[!code-powershell[principal](../../../powershell_scripts/app-service/scale-geographic/scale-geographic.ps1 "Escalar um aplicativo Web em todo o mundo com uma arquitetura de alta disponibilidade")]</span><span class="sxs-lookup"><span data-stu-id="d1af7-108">[!code-powershell[main](../../../powershell_scripts/app-service/scale-geographic/scale-geographic.ps1 "Scale a web app worldwide with a high-availability architecture")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="d1af7-109">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="d1af7-109">Clean up deployment</span></span> 

<span data-ttu-id="d1af7-110">Após a execução da amostra de script, o comando a seguir pode ser usado para remover o grupo de recursos, o aplicativo Web e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="d1af7-110">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="d1af7-111">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="d1af7-111">Script explanation</span></span>

<span data-ttu-id="d1af7-112">Este script usa os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="d1af7-112">This script uses the following commands.</span></span> <span data-ttu-id="d1af7-113">Cada comando na tabela redireciona para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="d1af7-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="d1af7-114">Command</span><span class="sxs-lookup"><span data-stu-id="d1af7-114">Command</span></span> | <span data-ttu-id="d1af7-115">Observações</span><span class="sxs-lookup"><span data-stu-id="d1af7-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="d1af7-116">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="d1af7-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="d1af7-117">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="d1af7-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="d1af7-118">New-AzureRMTrafficManagerProfile</span><span class="sxs-lookup"><span data-stu-id="d1af7-118">New-AzureRMTrafficManagerProfile</span></span>](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerprofile) | <span data-ttu-id="d1af7-119">Cria um perfil do Gerenciador de Tráfego.</span><span class="sxs-lookup"><span data-stu-id="d1af7-119">Creates a Traffic Manager profile.</span></span> |
| [<span data-ttu-id="d1af7-120">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="d1af7-120">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="d1af7-121">Cria um Plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d1af7-121">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="d1af7-122">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="d1af7-122">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="d1af7-123">Cria um aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="d1af7-123">Creates a web app.</span></span> |
| [<span data-ttu-id="d1af7-124">New-AzureRMTrafficManagerEndpoint</span><span class="sxs-lookup"><span data-stu-id="d1af7-124">New-AzureRMTrafficManagerEndpoint</span></span>](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerendpoint) | <span data-ttu-id="d1af7-125">Cria um ponto de extremidade em um perfil do Gerenciador de Tráfego.</span><span class="sxs-lookup"><span data-stu-id="d1af7-125">Creates an endpoint in a Traffic Manager profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="d1af7-126">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d1af7-126">Next steps</span></span>

<span data-ttu-id="d1af7-127">Para saber mais sobre o módulo do Azure PowerShell, confira a [Documentação do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d1af7-127">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="d1af7-128">Exemplos adicionais do Azure PowerShell para Aplicativos Web do Serviço de Aplicativo do Azure podem ser encontrados nos [exemplos do Azure PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="d1af7-128">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
