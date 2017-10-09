---
title: aaaAzure exemplo de Script do PowerShell - dimensionar um aplicativo web em todo o mundo com uma arquitetura de alta disponibilidade | Microsoft Docs
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
ms.openlocfilehash: 1fcda23250efe4966d63c5dfa744b76c26f3762a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-a-web-app-worldwide-with-a-high-availability-architecture"></a><span data-ttu-id="2089c-103">Escalar um aplicativo Web em todo o mundo com uma arquitetura de alta disponibilidade</span><span class="sxs-lookup"><span data-stu-id="2089c-103">Scale a web app worldwide with a high-availability architecture</span></span>

<span data-ttu-id="2089c-104">Nesse cenário, você criará um grupo de recursos, dois planos de serviço de aplicativo, dois aplicativos web, um perfil do Gerenciador de tráfego e dois pontos de extremidade de Gerenciador de tráfego.</span><span class="sxs-lookup"><span data-stu-id="2089c-104">In this scenario you will create a resource group, two app service plans, two web apps, a traffic manager profile, and two traffic manager endpoints.</span></span> <span data-ttu-id="2089c-105">Depois que o exercício de saudação for concluído, você terá uma alta disponibilidade arquitetura que permite que fornece disponibilidade global do seu aplicativo web com base na menor latência de rede hello.</span><span class="sxs-lookup"><span data-stu-id="2089c-105">Once hello exercise is complete you will have a high-available architecture which allows provides global availability of your web app based on hello lowest network latency.</span></span>

<span data-ttu-id="2089c-106">Se necessário, instale Olá PowerShell do Azure usando a instrução Olá encontrado no hello [guia do PowerShell do Azure](/powershell/azure/overview)e, em seguida, execute `Login-AzureRmAccount` toocreate uma conexão com o Azure.</span><span class="sxs-lookup"><span data-stu-id="2089c-106">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="2089c-107">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="2089c-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/scale-geographic/scale-geographic.ps1 "Scale a web app worldwide with a high-availability architecture")]

## <a name="clean-up-deployment"></a><span data-ttu-id="2089c-108">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="2089c-108">Clean up deployment</span></span> 

<span data-ttu-id="2089c-109">Após a execução do exemplo de script hello, Olá comando a seguir pode ser usado tooremove grupo de recursos de saudação, aplicativo web e recursos todos relacionados.</span><span class="sxs-lookup"><span data-stu-id="2089c-109">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="2089c-110">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="2089c-110">Script explanation</span></span>

<span data-ttu-id="2089c-111">Esse script usa Olá comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="2089c-111">This script uses hello following commands.</span></span> <span data-ttu-id="2089c-112">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="2089c-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="2089c-113">Command</span><span class="sxs-lookup"><span data-stu-id="2089c-113">Command</span></span> | <span data-ttu-id="2089c-114">Observações</span><span class="sxs-lookup"><span data-stu-id="2089c-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="2089c-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="2089c-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="2089c-116">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="2089c-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="2089c-117">New-AzureRMTrafficManagerProfile</span><span class="sxs-lookup"><span data-stu-id="2089c-117">New-AzureRMTrafficManagerProfile</span></span>](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerprofile) | <span data-ttu-id="2089c-118">Cria um perfil do Gerenciador de Tráfego.</span><span class="sxs-lookup"><span data-stu-id="2089c-118">Creates a Traffic Manager profile.</span></span> |
| [<span data-ttu-id="2089c-119">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="2089c-119">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="2089c-120">Cria um Plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2089c-120">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="2089c-121">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="2089c-121">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="2089c-122">Cria um aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="2089c-122">Creates a web app.</span></span> |
| [<span data-ttu-id="2089c-123">New-AzureRMTrafficManagerEndpoint</span><span class="sxs-lookup"><span data-stu-id="2089c-123">New-AzureRMTrafficManagerEndpoint</span></span>](/powershell/module/azurerm.trafficmanager/new-azurermtrafficmanagerendpoint) | <span data-ttu-id="2089c-124">Cria um ponto de extremidade em um perfil do Gerenciador de Tráfego.</span><span class="sxs-lookup"><span data-stu-id="2089c-124">Creates an endpoint in a Traffic Manager profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="2089c-125">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2089c-125">Next steps</span></span>

<span data-ttu-id="2089c-126">Para obter mais informações sobre o módulo do PowerShell do Azure hello, consulte [documentação do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2089c-126">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="2089c-127">Exemplos adicionais do Powershell do Azure para aplicativos de Web do serviço de aplicativo do Azure podem ser encontrados no hello [exemplos do PowerShell do Azure](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="2089c-127">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
