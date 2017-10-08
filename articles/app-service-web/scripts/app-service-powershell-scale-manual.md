---
title: aaaAzure exemplo de Script do PowerShell - dimensionar um aplicativo web manualmente | Microsoft Docs
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
ms.openlocfilehash: c749031fbe6c6bcbb25395387b4f32b2ba75cef4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-a-web-app-manually"></a><span data-ttu-id="85883-103">Dimensionar manualmente um aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="85883-103">Scale a web app manually</span></span>

<span data-ttu-id="85883-104">Nesse cenário, você aprenderá toocreate um grupo de recursos, aplicativo de serviço web e o plano de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="85883-104">In this scenario you will learn toocreate a resource group, app service plan and web app.</span></span> <span data-ttu-id="85883-105">Em seguida, você será dimensionado Olá plano do serviço de aplicativo de instâncias de toomultiple uma única instância.</span><span class="sxs-lookup"><span data-stu-id="85883-105">You will then scale hello App Service Plan from a single instance toomultiple instances.</span></span>

<span data-ttu-id="85883-106">Se necessário, instale Olá PowerShell do Azure usando a instrução Olá encontrado no hello [guia do PowerShell do Azure](/powershell/azure/overview)e, em seguida, execute `Login-AzureRmAccount` toocreate uma conexão com o Azure.</span><span class="sxs-lookup"><span data-stu-id="85883-106">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="85883-107">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="85883-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/scale-manual/scale-manual.ps1 "Scale a web app manually")]

## <a name="clean-up-deployment"></a><span data-ttu-id="85883-108">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="85883-108">Clean up deployment</span></span> 

<span data-ttu-id="85883-109">Após a execução do exemplo de script hello, Olá comando a seguir pode ser usado tooremove grupo de recursos de saudação, aplicativo web e recursos todos relacionados.</span><span class="sxs-lookup"><span data-stu-id="85883-109">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="85883-110">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="85883-110">Script explanation</span></span>

<span data-ttu-id="85883-111">Esse script usa Olá comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="85883-111">This script uses hello following commands.</span></span> <span data-ttu-id="85883-112">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="85883-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="85883-113">Command</span><span class="sxs-lookup"><span data-stu-id="85883-113">Command</span></span> | <span data-ttu-id="85883-114">Observações</span><span class="sxs-lookup"><span data-stu-id="85883-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="85883-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="85883-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="85883-116">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="85883-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="85883-117">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="85883-117">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="85883-118">Cria um Plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="85883-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="85883-119">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="85883-119">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="85883-120">Cria um aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="85883-120">Creates a web app.</span></span> |
| [<span data-ttu-id="85883-121">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="85883-121">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="85883-122">Modifica a configuração de um aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="85883-122">Modifies a web app's configuration.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="85883-123">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="85883-123">Next steps</span></span>

<span data-ttu-id="85883-124">Para obter mais informações sobre o módulo do PowerShell do Azure hello, consulte [documentação do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="85883-124">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="85883-125">Exemplos adicionais do Powershell do Azure para aplicativos de Web do serviço de aplicativo do Azure podem ser encontrados no hello [exemplos do PowerShell do Azure](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="85883-125">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
