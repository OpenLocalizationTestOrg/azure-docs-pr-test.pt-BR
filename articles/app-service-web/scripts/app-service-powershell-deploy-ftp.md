---
title: aaaAzure exemplo de Script do PowerShell - aplicativo carregue arquivos tooa web usando FTP | Microsoft Docs
description: Exemplo de Script do PowerShell do Azure - aplicativo carregue arquivos tooa web usando FTP
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
ms.openlocfilehash: 32a0a529e94c1315cc6730faf23fca2693c50ffb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-tooa-web-app-using-ftp"></a><span data-ttu-id="e0bd4-103">Carregar arquivos tooa web app usando FTP</span><span class="sxs-lookup"><span data-stu-id="e0bd4-103">Upload files tooa web app using FTP</span></span>

<span data-ttu-id="e0bd4-104">Esse script de exemplo cria um aplicativo Web no Serviço de Aplicativo com recursos relacionados e, em seguida, implanta o código do aplicativo Web usando o FTP (por meio de [WebClient.UploadFile()](https://msdn.microsoft.com/library/ms144229.aspx)).</span><span class="sxs-lookup"><span data-stu-id="e0bd4-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code using FTP (via [WebClient.UploadFile()](https://msdn.microsoft.com/library/ms144229.aspx)).</span></span>

<span data-ttu-id="e0bd4-105">Se necessário, instale Olá PowerShell do Azure usando a instrução Olá encontrado no hello [guia do PowerShell do Azure](/powershell/azure/overview)e, em seguida, execute `Login-AzureRmAccount` toocreate uma conexão com o Azure.</span><span class="sxs-lookup"><span data-stu-id="e0bd4-105">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="e0bd4-106">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="e0bd4-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/deploy-ftp/deploy-ftp.ps1?highlight=1 "Upload files tooa web app using FTP")]

## <a name="clean-up-deployment"></a><span data-ttu-id="e0bd4-107">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="e0bd4-107">Clean up deployment</span></span> 

<span data-ttu-id="e0bd4-108">Após a execução do exemplo de script hello, Olá comando a seguir pode ser usado tooremove grupo de recursos de saudação, aplicativo web e recursos todos relacionados.</span><span class="sxs-lookup"><span data-stu-id="e0bd4-108">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name $webappname -Force
```

## <a name="script-explanation"></a><span data-ttu-id="e0bd4-109">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="e0bd4-109">Script explanation</span></span>

<span data-ttu-id="e0bd4-110">Esse script usa Olá comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="e0bd4-110">This script uses hello following commands.</span></span> <span data-ttu-id="e0bd4-111">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="e0bd4-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="e0bd4-112">Command</span><span class="sxs-lookup"><span data-stu-id="e0bd4-112">Command</span></span> | <span data-ttu-id="e0bd4-113">Observações</span><span class="sxs-lookup"><span data-stu-id="e0bd4-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="e0bd4-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="e0bd4-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="e0bd4-115">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="e0bd4-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="e0bd4-116">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="e0bd4-116">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="e0bd4-117">Cria um Plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="e0bd4-117">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="e0bd4-118">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="e0bd4-118">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="e0bd4-119">Cria um aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="e0bd4-119">Creates a web app.</span></span> |
| [<span data-ttu-id="e0bd4-120">Get-AzureRmWebAppPublishingProfile</span><span class="sxs-lookup"><span data-stu-id="e0bd4-120">Get-AzureRmWebAppPublishingProfile</span></span>](/powershell/module/azurerm.websites/get-azurermwebapppublishingprofile) | <span data-ttu-id="e0bd4-121">Obtenha perfis de publicação do aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="e0bd4-121">Get a web app's publishing profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e0bd4-122">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e0bd4-122">Next steps</span></span>

<span data-ttu-id="e0bd4-123">Para obter mais informações sobre o módulo do PowerShell do Azure hello, consulte [documentação do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e0bd4-123">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="e0bd4-124">Exemplos adicionais do Powershell do Azure para aplicativos de Web do serviço de aplicativo do Azure podem ser encontrados no hello [exemplos do PowerShell do Azure](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="e0bd4-124">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
