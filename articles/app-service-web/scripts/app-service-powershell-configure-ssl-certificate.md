---
title: Exemplo de Script do Azure PowerShell - Associar um certificado SSL personalizado a um aplicativo Web | Microsoft Docs
description: Exemplo de Script do Azure PowerShell - Associar um certificado SSL personalizado a um aplicativo Web
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
ms.openlocfilehash: de8deccadcd9571be75447a117888bf2b3f571a0
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="bind-a-custom-ssl-certificate-to-a-web-app"></a><span data-ttu-id="85d59-103">Associar um certificado SSL personalizado a um aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="85d59-103">Bind a custom SSL certificate to a web app</span></span>

<span data-ttu-id="85d59-104">Este exemplo de script cria um aplicativo Web no Serviço de Aplicativo com seus recursos relacionados e associa o certificado SSL de um nome de domínio personalizado a ele.</span><span class="sxs-lookup"><span data-stu-id="85d59-104">This sample script creates a web app in App Service with its related resources, then binds the SSL certificate of a custom domain name to it.</span></span> 

<span data-ttu-id="85d59-105">Se necessário, instale o Azure PowerShell usando a instrução encontrada no [guia do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="85d59-105">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview).</span></span> <span data-ttu-id="85d59-106">Além disso, verifique se:</span><span class="sxs-lookup"><span data-stu-id="85d59-106">Also, ensure that:</span></span>

- <span data-ttu-id="85d59-107">Uma conexão com o Azure foi criado usando o comando `az login`.</span><span class="sxs-lookup"><span data-stu-id="85d59-107">A connection with Azure has been created using the `az login` command.</span></span>
- <span data-ttu-id="85d59-108">Você tem acesso à página de configuração do DNS do registrador de seu domínio.</span><span class="sxs-lookup"><span data-stu-id="85d59-108">You have access to your domain registrar's DNS configuration page.</span></span>
- <span data-ttu-id="85d59-109">Você tem um arquivo .PFX válido e sua senha para o certificado SSL que você deseja carregar e associar.</span><span class="sxs-lookup"><span data-stu-id="85d59-109">You have a valid .PFX file and its password for the SSL certificate you want to upload and bind.</span></span>

## <a name="sample-script"></a><span data-ttu-id="85d59-110">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="85d59-110">Sample script</span></span>

<span data-ttu-id="85d59-111">[!code-powershell[principal](../../../powershell_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.ps1?highlight=1-3 "Associar um certificado SSL personalizado a um aplicativo Web")]</span><span class="sxs-lookup"><span data-stu-id="85d59-111">[!code-powershell[main](../../../powershell_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.ps1?highlight=1-3 "Bind a custom SSL certificate to a web app")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="85d59-112">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="85d59-112">Clean up deployment</span></span> 

<span data-ttu-id="85d59-113">Após a execução da amostra de script, o comando a seguir pode ser usado para remover o grupo de recursos, o aplicativo Web e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="85d59-113">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="85d59-114">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="85d59-114">Script explanation</span></span>

<span data-ttu-id="85d59-115">Este script usa os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="85d59-115">This script uses the following commands.</span></span> <span data-ttu-id="85d59-116">Cada comando na tabela redireciona para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="85d59-116">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="85d59-117">Command</span><span class="sxs-lookup"><span data-stu-id="85d59-117">Command</span></span> | <span data-ttu-id="85d59-118">Observações</span><span class="sxs-lookup"><span data-stu-id="85d59-118">Notes</span></span> |
|---|---|
| [<span data-ttu-id="85d59-119">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="85d59-119">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="85d59-120">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="85d59-120">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="85d59-121">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="85d59-121">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="85d59-122">Cria um Plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="85d59-122">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="85d59-123">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="85d59-123">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="85d59-124">Cria um aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="85d59-124">Creates a web app.</span></span> |
| [<span data-ttu-id="85d59-125">Set-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="85d59-125">Set-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/set-azurermappserviceplan) | <span data-ttu-id="85d59-126">Modifica um plano do Serviço de Aplicativo para alterar seu tipo de preço.</span><span class="sxs-lookup"><span data-stu-id="85d59-126">Modifies an App Service plan to change its pricing tier.</span></span> |
| [<span data-ttu-id="85d59-127">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="85d59-127">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="85d59-128">Modifica a configuração de um aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="85d59-128">Modifies a web app's configuration.</span></span> |
| [<span data-ttu-id="85d59-129">New-AzureRmWebAppSSLBinding</span><span class="sxs-lookup"><span data-stu-id="85d59-129">New-AzureRmWebAppSSLBinding</span></span>](/powershell/module/azurerm.websites/new-azurermwebappsslbinding) | <span data-ttu-id="85d59-130">Cria uma associação de certificado SSL para um aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="85d59-130">Creates an SSL certificate binding for a web app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="85d59-131">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="85d59-131">Next steps</span></span>

<span data-ttu-id="85d59-132">Para saber mais sobre o módulo do Azure PowerShell, confira a [Documentação do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="85d59-132">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="85d59-133">Exemplos adicionais do Azure PowerShell para Aplicativos Web do Serviço de Aplicativo do Azure podem ser encontrados nos [exemplos do Azure PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="85d59-133">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
