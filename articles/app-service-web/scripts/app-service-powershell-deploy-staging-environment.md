---
title: "aaaAzure exemplo de Script do PowerShell - criar um aplicativo web e implantar código tooa ambiente de preparo | Microsoft Docs"
description: "Exemplo de Script do PowerShell do Azure - criar um aplicativo web e implantar código tooa ambiente de preparo"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 27cf0680-c3a9-4a58-9f71-6dec09f6b874
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: sample
ms.date: 03/20/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 5c74b962955770637173f1fd4f49342fec54ae3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-and-deploy-code-tooa-staging-environment"></a><span data-ttu-id="4df17-103">Criar um aplicativo web e implantar código tooa ambiente de preparo</span><span class="sxs-lookup"><span data-stu-id="4df17-103">Create a web app and deploy code tooa staging environment</span></span>

<span data-ttu-id="4df17-104">Esse script de exemplo cria um aplicativo web no serviço de aplicativo com um slot de implantação adicional chamado "preparação" e, em seguida, implanta um toohello do aplicativo de exemplo "preparação" slot.</span><span class="sxs-lookup"><span data-stu-id="4df17-104">This sample script creates a web app in App Service with an additional deployment slot called "staging", and then deploys a sample app toohello "staging" slot.</span></span>

<span data-ttu-id="4df17-105">Se necessário, instale Olá PowerShell do Azure usando a instrução Olá encontrado no hello [guia do PowerShell do Azure](/powershell/azure/overview)e, em seguida, execute `Login-AzureRmAccount` toocreate uma conexão com o Azure.</span><span class="sxs-lookup"><span data-stu-id="4df17-105">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="4df17-106">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="4df17-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/deploy-deployment-slot/deploy-deployment-slot.ps1?highlight=1 "Create a web app and deploy code tooa staging environment")]

## <a name="clean-up-deployment"></a><span data-ttu-id="4df17-107">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="4df17-107">Clean up deployment</span></span> 

<span data-ttu-id="4df17-108">Após a execução do exemplo de script hello, Olá comando a seguir pode ser usado tooremove grupo de recursos de saudação, aplicativo web e recursos todos relacionados.</span><span class="sxs-lookup"><span data-stu-id="4df17-108">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="4df17-109">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="4df17-109">Script explanation</span></span>

<span data-ttu-id="4df17-110">Esse script usa Olá comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="4df17-110">This script uses hello following commands.</span></span> <span data-ttu-id="4df17-111">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="4df17-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="4df17-112">Command</span><span class="sxs-lookup"><span data-stu-id="4df17-112">Command</span></span> | <span data-ttu-id="4df17-113">Observações</span><span class="sxs-lookup"><span data-stu-id="4df17-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="4df17-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="4df17-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="4df17-115">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="4df17-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="4df17-116">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="4df17-116">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="4df17-117">Cria um Plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="4df17-117">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="4df17-118">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="4df17-118">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="4df17-119">Cria um aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="4df17-119">Creates a web app.</span></span> |
| [<span data-ttu-id="4df17-120">Set-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="4df17-120">Set-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/set-azurermappserviceplan) | <span data-ttu-id="4df17-121">Modifica um toochange do plano de serviço de aplicativo em sua camada de preços.</span><span class="sxs-lookup"><span data-stu-id="4df17-121">Modifies an App Service plan toochange its pricing tier.</span></span> |
| [<span data-ttu-id="4df17-122">New-AzureRmWebAppSlot</span><span class="sxs-lookup"><span data-stu-id="4df17-122">New-AzureRmWebAppSlot</span></span>](/powershell/module/azurerm.websites/new-azurermwebappslot) | <span data-ttu-id="4df17-123">Cria um slot de implantação para um aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="4df17-123">Creates a deployment slot for a web app.</span></span> |
| [<span data-ttu-id="4df17-124">Set-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="4df17-124">Set-AzureRmResource</span></span>](/powershell/module/azurerm.resources/set-azurermresource) | <span data-ttu-id="4df17-125">Modifica um recurso em um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="4df17-125">Modifies a resource in a resource group.</span></span> |
| [<span data-ttu-id="4df17-126">Swap-AzureRmWebAppSlot</span><span class="sxs-lookup"><span data-stu-id="4df17-126">Swap-AzureRmWebAppSlot</span></span>](/powershell/module/azurerm.websites/swap-azurermwebappslot) | <span data-ttu-id="4df17-127">Troca um slot de implantação de um aplicativo Web para produção.</span><span class="sxs-lookup"><span data-stu-id="4df17-127">Swaps a web app's deployment slot into production.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="4df17-128">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4df17-128">Next steps</span></span>

<span data-ttu-id="4df17-129">Para obter mais informações sobre o módulo do PowerShell do Azure hello, consulte [documentação do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="4df17-129">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="4df17-130">Exemplos adicionais do Powershell do Azure para aplicativos de Web do serviço de aplicativo do Azure podem ser encontrados no hello [exemplos do PowerShell do Azure](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="4df17-130">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
