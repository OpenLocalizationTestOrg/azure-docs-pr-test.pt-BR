---
title: Exemplo de Script do Azure PowerShell - Carregar arquivos em um aplicativo Web usando FTP | Microsoft Docs
description: Exemplo de Script do Azure PowerShell - Carregar arquivos em um aplicativo Web usando FTP
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: b7d46d6f-44fd-454c-8008-87dab6eefbc1
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: sample
ms.date: 03/20/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 96b99110b63b037746fcc40eb15db5d718eb71a1
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="upload-files-to-a-web-app-using-ftp"></a><span data-ttu-id="37dc4-103">Carregar arquivos para um aplicativo Web usando FTP</span><span class="sxs-lookup"><span data-stu-id="37dc4-103">Upload files to a web app using FTP</span></span>

<span data-ttu-id="37dc4-104">Esse script de exemplo cria um aplicativo Web no Serviço de Aplicativo com recursos relacionados e, em seguida, implanta o código do aplicativo Web usando o FTP (por meio de [WebClient.UploadFile()](https://msdn.microsoft.com/library/ms144229.aspx)).</span><span class="sxs-lookup"><span data-stu-id="37dc4-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code using FTP (via [WebClient.UploadFile()](https://msdn.microsoft.com/library/ms144229.aspx)).</span></span>

<span data-ttu-id="37dc4-105">Se necessário, instale o Azure PowerShell usando a instrução encontrada no [guia do Azure PowerShell](/powershell/azure/overview) e, em seguida, execute `Login-AzureRmAccount` para criar uma conexão com o Azure.</span><span class="sxs-lookup"><span data-stu-id="37dc4-105">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="37dc4-106">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="37dc4-106">Sample script</span></span>

<span data-ttu-id="37dc4-107">[!code-powershell[principal](../../../powershell_scripts/app-service/deploy-ftp/deploy-ftp.ps1?highlight=1 "Carregar arquivos em um aplicativo Web usando FTP")]</span><span class="sxs-lookup"><span data-stu-id="37dc4-107">[!code-powershell[main](../../../powershell_scripts/app-service/deploy-ftp/deploy-ftp.ps1?highlight=1 "Upload files to a web app using FTP")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="37dc4-108">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="37dc4-108">Clean up deployment</span></span> 

<span data-ttu-id="37dc4-109">Após a execução da amostra de script, o comando a seguir pode ser usado para remover o grupo de recursos, o aplicativo Web e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="37dc4-109">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name $webappname -Force
```

## <a name="script-explanation"></a><span data-ttu-id="37dc4-110">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="37dc4-110">Script explanation</span></span>

<span data-ttu-id="37dc4-111">Este script usa os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="37dc4-111">This script uses the following commands.</span></span> <span data-ttu-id="37dc4-112">Cada comando na tabela redireciona para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="37dc4-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="37dc4-113">Command</span><span class="sxs-lookup"><span data-stu-id="37dc4-113">Command</span></span> | <span data-ttu-id="37dc4-114">Observações</span><span class="sxs-lookup"><span data-stu-id="37dc4-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="37dc4-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="37dc4-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="37dc4-116">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="37dc4-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="37dc4-117">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="37dc4-117">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="37dc4-118">Cria um Plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="37dc4-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="37dc4-119">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="37dc4-119">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="37dc4-120">Cria um aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="37dc4-120">Creates a web app.</span></span> |
| [<span data-ttu-id="37dc4-121">Get-AzureRmWebAppPublishingProfile</span><span class="sxs-lookup"><span data-stu-id="37dc4-121">Get-AzureRmWebAppPublishingProfile</span></span>](/powershell/module/azurerm.websites/get-azurermwebapppublishingprofile) | <span data-ttu-id="37dc4-122">Obtenha perfis de publicação do aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="37dc4-122">Get a web app's publishing profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="37dc4-123">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="37dc4-123">Next steps</span></span>

<span data-ttu-id="37dc4-124">Para saber mais sobre o módulo do Azure PowerShell, confira a [Documentação do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="37dc4-124">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="37dc4-125">Exemplos adicionais do Azure PowerShell para Aplicativos Web do Serviço de Aplicativo do Azure podem ser encontrados nos [exemplos do Azure PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="37dc4-125">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
