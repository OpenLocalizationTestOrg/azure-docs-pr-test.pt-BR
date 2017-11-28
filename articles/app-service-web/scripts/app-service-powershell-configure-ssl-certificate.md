---
title: aaaAzure exemplo de Script do PowerShell - associar um certificado SSL personalizado, tooa aplicativo da web | Microsoft Docs
description: Exemplo de Script do PowerShell do Azure - associar um certificado SSL personalizado, tooa aplicativo da web
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 23e83b74-614a-49a0-bc08-7542120eeec5
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: sample
ms.date: 03/20/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 6e249ceedb9e2b8872dd0bc8b0aea0d718b28dab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="bind-a-custom-ssl-certificate-tooa-web-app"></a><span data-ttu-id="55004-103">Associar um certificado SSL personalizado, tooa aplicativo da web</span><span class="sxs-lookup"><span data-stu-id="55004-103">Bind a custom SSL certificate tooa web app</span></span>

<span data-ttu-id="55004-104">Esse script de exemplo cria um aplicativo web no serviço de aplicativo com seus recursos relacionados, em seguida, associa o certificado SSL de saudação de um tooit de nome de domínio personalizado.</span><span class="sxs-lookup"><span data-stu-id="55004-104">This sample script creates a web app in App Service with its related resources, then binds hello SSL certificate of a custom domain name tooit.</span></span> 

<span data-ttu-id="55004-105">Se necessário, instale Olá PowerShell do Azure usando a instrução Olá encontrado no hello [guia do PowerShell do Azure](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="55004-105">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview).</span></span> <span data-ttu-id="55004-106">Além disso, verifique se:</span><span class="sxs-lookup"><span data-stu-id="55004-106">Also, ensure that:</span></span>

- <span data-ttu-id="55004-107">Foi criada uma conexão com o Azure usando Olá `az login` comando.</span><span class="sxs-lookup"><span data-stu-id="55004-107">A connection with Azure has been created using hello `az login` command.</span></span>
- <span data-ttu-id="55004-108">Você tem a página de configuração de DNS do registrador de domínio tooyour acesso.</span><span class="sxs-lookup"><span data-stu-id="55004-108">You have access tooyour domain registrar's DNS configuration page.</span></span>
- <span data-ttu-id="55004-109">Você tem uma opção válida. Arquivo PFX e sua senha para Olá SSL certificado que você deseja tooupload e estabeleça uma ligação.</span><span class="sxs-lookup"><span data-stu-id="55004-109">You have a valid .PFX file and its password for hello SSL certificate you want tooupload and bind.</span></span>

## <a name="sample-script"></a><span data-ttu-id="55004-110">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="55004-110">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.ps1?highlight=1-3 "Bind a custom SSL certificate tooa web app")]

## <a name="clean-up-deployment"></a><span data-ttu-id="55004-111">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="55004-111">Clean up deployment</span></span> 

<span data-ttu-id="55004-112">Após a execução do exemplo de script hello, Olá comando a seguir pode ser usado tooremove grupo de recursos de saudação, aplicativo web e recursos todos relacionados.</span><span class="sxs-lookup"><span data-stu-id="55004-112">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="55004-113">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="55004-113">Script explanation</span></span>

<span data-ttu-id="55004-114">Esse script usa Olá comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="55004-114">This script uses hello following commands.</span></span> <span data-ttu-id="55004-115">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="55004-115">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="55004-116">Command</span><span class="sxs-lookup"><span data-stu-id="55004-116">Command</span></span> | <span data-ttu-id="55004-117">Observações</span><span class="sxs-lookup"><span data-stu-id="55004-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="55004-118">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="55004-118">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="55004-119">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="55004-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="55004-120">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="55004-120">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="55004-121">Cria um Plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="55004-121">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="55004-122">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="55004-122">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="55004-123">Cria um aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="55004-123">Creates a web app.</span></span> |
| [<span data-ttu-id="55004-124">Set-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="55004-124">Set-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/set-azurermappserviceplan) | <span data-ttu-id="55004-125">Modifica um toochange do plano de serviço de aplicativo em sua camada de preços.</span><span class="sxs-lookup"><span data-stu-id="55004-125">Modifies an App Service plan toochange its pricing tier.</span></span> |
| [<span data-ttu-id="55004-126">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="55004-126">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="55004-127">Modifica a configuração de um aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="55004-127">Modifies a web app's configuration.</span></span> |
| [<span data-ttu-id="55004-128">New-AzureRmWebAppSSLBinding</span><span class="sxs-lookup"><span data-stu-id="55004-128">New-AzureRmWebAppSSLBinding</span></span>](/powershell/module/azurerm.websites/new-azurermwebappsslbinding) | <span data-ttu-id="55004-129">Cria uma associação de certificado SSL para um aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="55004-129">Creates an SSL certificate binding for a web app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="55004-130">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="55004-130">Next steps</span></span>

<span data-ttu-id="55004-131">Para obter mais informações sobre o módulo do PowerShell do Azure hello, consulte [documentação do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="55004-131">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="55004-132">Exemplos adicionais do Powershell do Azure para aplicativos de Web do serviço de aplicativo do Azure podem ser encontrados no hello [exemplos do PowerShell do Azure](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="55004-132">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
