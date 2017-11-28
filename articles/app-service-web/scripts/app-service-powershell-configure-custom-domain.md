---
title: "aaaAzure exemplo de Script do PowerShell - atribuir um aplicativo web do domínio personalizado tooa | Microsoft Docs"
description: "Exemplo de Script do PowerShell do Azure - atribuir um aplicativo web do domínio personalizado tooa"
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
ms.openlocfilehash: 10224e800588019626ef25cbba4a926096779920
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="assign-a-custom-domain-tooa-web-app"></a><span data-ttu-id="6c4e2-103">Atribuir um aplicativo web do domínio personalizado tooa</span><span class="sxs-lookup"><span data-stu-id="6c4e2-103">Assign a custom domain tooa web app</span></span>

<span data-ttu-id="6c4e2-104">Esse script de exemplo cria um aplicativo web no serviço de aplicativo com seus recursos relacionados e, em seguida, mapeia `www.<yourdomain>` tooit.</span><span class="sxs-lookup"><span data-stu-id="6c4e2-104">This sample script creates a web app in App Service with its related resources, and then maps `www.<yourdomain>` tooit.</span></span> 

<span data-ttu-id="6c4e2-105">Se necessário, instale Olá PowerShell do Azure usando a instrução Olá encontrado no hello [guia do PowerShell do Azure](/powershell/azure/overview)e, em seguida, execute `Login-AzureRmAccount` toocreate uma conexão com o Azure.</span><span class="sxs-lookup"><span data-stu-id="6c4e2-105">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span> <span data-ttu-id="6c4e2-106">Além disso, você precisa de página de configuração de DNS do registrador de domínio tooyour acesso toohave.</span><span class="sxs-lookup"><span data-stu-id="6c4e2-106">Also, you need toohave access tooyour domain registrar's DNS configuration page.</span></span>

## <a name="sample-script"></a><span data-ttu-id="6c4e2-107">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="6c4e2-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/map-custom-domain/map-custom-domain.ps1?highlight=1 "Assign a custom domain tooa web app")]

## <a name="clean-up-deployment"></a><span data-ttu-id="6c4e2-108">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="6c4e2-108">Clean up deployment</span></span> 

<span data-ttu-id="6c4e2-109">Após a execução do exemplo de script hello, Olá comando a seguir pode ser usado tooremove grupo de recursos de saudação, aplicativo web e recursos todos relacionados.</span><span class="sxs-lookup"><span data-stu-id="6c4e2-109">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="6c4e2-110">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="6c4e2-110">Script explanation</span></span>

<span data-ttu-id="6c4e2-111">Esse script usa Olá comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="6c4e2-111">This script uses hello following commands.</span></span> <span data-ttu-id="6c4e2-112">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="6c4e2-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="6c4e2-113">Command</span><span class="sxs-lookup"><span data-stu-id="6c4e2-113">Command</span></span> | <span data-ttu-id="6c4e2-114">Observações</span><span class="sxs-lookup"><span data-stu-id="6c4e2-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="6c4e2-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="6c4e2-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="6c4e2-116">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="6c4e2-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="6c4e2-117">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="6c4e2-117">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="6c4e2-118">Cria um Plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6c4e2-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="6c4e2-119">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="6c4e2-119">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="6c4e2-120">Cria um aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="6c4e2-120">Creates a web app.</span></span> |
| [<span data-ttu-id="6c4e2-121">Set-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="6c4e2-121">Set-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/set-azurermappserviceplan) | <span data-ttu-id="6c4e2-122">Modifica um toochange do plano de serviço de aplicativo em sua camada de preços.</span><span class="sxs-lookup"><span data-stu-id="6c4e2-122">Modifies an App Service plan toochange its pricing tier.</span></span> |
| [<span data-ttu-id="6c4e2-123">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="6c4e2-123">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="6c4e2-124">Modifica a configuração de um aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="6c4e2-124">Modifies a web app's configuration.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="6c4e2-125">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6c4e2-125">Next steps</span></span>

<span data-ttu-id="6c4e2-126">Para obter mais informações sobre o módulo do PowerShell do Azure hello, consulte [documentação do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="6c4e2-126">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="6c4e2-127">Exemplos adicionais do Powershell do Azure para aplicativos de Web do serviço de aplicativo do Azure podem ser encontrados no hello [exemplos do PowerShell do Azure](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="6c4e2-127">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
