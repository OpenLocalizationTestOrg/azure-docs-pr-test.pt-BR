---
title: aaaAzure exemplo de Script do PowerShell - se conectar a uma conta de armazenamento do tooa de aplicativo web | Microsoft Docs
description: Script do PowerShell do Azure de exemplo - conectar a uma conta de armazenamento do tooa de aplicativo web
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: e4831bdc-2068-4883-9474-0b34c2e3e255
ms.service: app-service
ms.devlang: multiple
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 03/20/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 07693366d32fbaefe92c18df67ded81661e1a2df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-web-app-tooa-storage-account"></a><span data-ttu-id="64d2d-103">Conecte-se a uma conta de armazenamento do tooa de aplicativo web</span><span class="sxs-lookup"><span data-stu-id="64d2d-103">Connect a web app tooa storage account</span></span>

<span data-ttu-id="64d2d-104">Nesse cenário, você aprenderá como toocreate uma conta de armazenamento do Azure e um Azure aplicativo da web.</span><span class="sxs-lookup"><span data-stu-id="64d2d-104">In this scenario you will learn how toocreate an Azure storage account and an Azure web app.</span></span> <span data-ttu-id="64d2d-105">Em seguida, você vinculará aplicativo hello armazenamento conta toohello web usando configurações do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="64d2d-105">Then you will link hello storage account toohello web app using app settings.</span></span>

<span data-ttu-id="64d2d-106">Se necessário, instale Olá PowerShell do Azure usando a instrução Olá encontrado no hello [guia do PowerShell do Azure](/powershell/azure/overview)e, em seguida, execute `Login-AzureRmAccount` toocreate uma conexão com o Azure.</span><span class="sxs-lookup"><span data-stu-id="64d2d-106">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="64d2d-107">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="64d2d-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/connect-to-storage/connect-to-storage.ps1 "Connect a web app tooa storage account")]

## <a name="clean-up-deployment"></a><span data-ttu-id="64d2d-108">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="64d2d-108">Clean up deployment</span></span> 

<span data-ttu-id="64d2d-109">Após a execução do exemplo de script hello, Olá comando a seguir pode ser usado tooremove grupo de recursos de saudação, aplicativo web e recursos todos relacionados.</span><span class="sxs-lookup"><span data-stu-id="64d2d-109">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="64d2d-110">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="64d2d-110">Script explanation</span></span>

<span data-ttu-id="64d2d-111">Esse script usa Olá comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="64d2d-111">This script uses hello following commands.</span></span> <span data-ttu-id="64d2d-112">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="64d2d-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="64d2d-113">Command</span><span class="sxs-lookup"><span data-stu-id="64d2d-113">Command</span></span> | <span data-ttu-id="64d2d-114">Observações</span><span class="sxs-lookup"><span data-stu-id="64d2d-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="64d2d-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="64d2d-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="64d2d-116">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="64d2d-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="64d2d-117">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="64d2d-117">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="64d2d-118">Cria um Plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="64d2d-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="64d2d-119">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="64d2d-119">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="64d2d-120">Cria um aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="64d2d-120">Creates a web app.</span></span> |
| [<span data-ttu-id="64d2d-121">New-AzureRMStorageAccount</span><span class="sxs-lookup"><span data-stu-id="64d2d-121">New-AzureRMStorageAccount</span></span>](/powershell/module/azurerm.storage/new-azurermstorageaccount) | <span data-ttu-id="64d2d-122">Cria uma conta de Armazenamento.</span><span class="sxs-lookup"><span data-stu-id="64d2d-122">Creates a Storage account.</span></span> |
| [<span data-ttu-id="64d2d-123">Get-AzureRMStorageAccountKey</span><span class="sxs-lookup"><span data-stu-id="64d2d-123">Get-AzureRMStorageAccountKey</span></span>](/powershell/module/azurerm.storage/get-azurermstorageaccountkey) | <span data-ttu-id="64d2d-124">Obtém as chaves de acesso Olá para uma conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="64d2d-124">Gets hello access keys for an Azure Storage account.</span></span> |
| [<span data-ttu-id="64d2d-125">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="64d2d-125">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="64d2d-126">Modifica a configuração de um aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="64d2d-126">Modifies a web app's configuration.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="64d2d-127">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="64d2d-127">Next steps</span></span>

<span data-ttu-id="64d2d-128">Para obter mais informações sobre o módulo do PowerShell do Azure hello, consulte [documentação do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="64d2d-128">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="64d2d-129">Exemplos adicionais do Powershell do Azure para aplicativos de Web do serviço de aplicativo do Azure podem ser encontrados no hello [exemplos do PowerShell do Azure](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="64d2d-129">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
