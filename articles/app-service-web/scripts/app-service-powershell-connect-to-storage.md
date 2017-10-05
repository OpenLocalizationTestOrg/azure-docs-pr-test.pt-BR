---
title: Exemplo de script do Azure PowerShell - Conectar um aplicativo Web a uma conta de armazenamento | Microsoft Docs
description: Exemplo de script do Azure PowerShell - Conectar um aplicativo Web a uma conta de armazenamento
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
ms.openlocfilehash: 481f3efdb1cbbeba328183da7e320c7e5b819b3a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="connect-a-web-app-to-a-storage-account"></a><span data-ttu-id="f9d80-103">Conectar um aplicativo Web a uma conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="f9d80-103">Connect a web app to a storage account</span></span>

<span data-ttu-id="f9d80-104">Nesse cenário, você aprenderá como criar uma conta de armazenamento do Azure e um aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="f9d80-104">In this scenario you will learn how to create an Azure storage account and an Azure web app.</span></span> <span data-ttu-id="f9d80-105">Em seguida, você vinculará a conta de armazenamento ao aplicativo Web usando configurações do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f9d80-105">Then you will link the storage account to the web app using app settings.</span></span>

<span data-ttu-id="f9d80-106">Se necessário, instale o Azure PowerShell usando a instrução encontrada no [guia do Azure PowerShell](/powershell/azure/overview) e, em seguida, execute `Login-AzureRmAccount` para criar uma conexão com o Azure.</span><span class="sxs-lookup"><span data-stu-id="f9d80-106">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="f9d80-107">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="f9d80-107">Sample script</span></span>

<span data-ttu-id="f9d80-108">[!code-powershell[principal](../../../powershell_scripts/app-service/connect-to-storage/connect-to-storage.ps1 "Conectar um aplicativo Web a uma conta de armazenamento")]</span><span class="sxs-lookup"><span data-stu-id="f9d80-108">[!code-powershell[main](../../../powershell_scripts/app-service/connect-to-storage/connect-to-storage.ps1 "Connect a web app to a storage account")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="f9d80-109">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="f9d80-109">Clean up deployment</span></span> 

<span data-ttu-id="f9d80-110">Após a execução da amostra de script, o comando a seguir pode ser usado para remover o grupo de recursos, o aplicativo Web e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="f9d80-110">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="f9d80-111">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="f9d80-111">Script explanation</span></span>

<span data-ttu-id="f9d80-112">Este script usa os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="f9d80-112">This script uses the following commands.</span></span> <span data-ttu-id="f9d80-113">Cada comando na tabela redireciona para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="f9d80-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="f9d80-114">Command</span><span class="sxs-lookup"><span data-stu-id="f9d80-114">Command</span></span> | <span data-ttu-id="f9d80-115">Observações</span><span class="sxs-lookup"><span data-stu-id="f9d80-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="f9d80-116">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="f9d80-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="f9d80-117">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="f9d80-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="f9d80-118">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="f9d80-118">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="f9d80-119">Cria um Plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f9d80-119">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="f9d80-120">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="f9d80-120">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="f9d80-121">Cria um aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="f9d80-121">Creates a web app.</span></span> |
| [<span data-ttu-id="f9d80-122">New-AzureRMStorageAccount</span><span class="sxs-lookup"><span data-stu-id="f9d80-122">New-AzureRMStorageAccount</span></span>](/powershell/module/azurerm.storage/new-azurermstorageaccount) | <span data-ttu-id="f9d80-123">Cria uma conta de Armazenamento.</span><span class="sxs-lookup"><span data-stu-id="f9d80-123">Creates a Storage account.</span></span> |
| [<span data-ttu-id="f9d80-124">Get-AzureRMStorageAccountKey</span><span class="sxs-lookup"><span data-stu-id="f9d80-124">Get-AzureRMStorageAccountKey</span></span>](/powershell/module/azurerm.storage/get-azurermstorageaccountkey) | <span data-ttu-id="f9d80-125">Obtém as chaves de acesso para a conta de Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="f9d80-125">Gets the access keys for an Azure Storage account.</span></span> |
| [<span data-ttu-id="f9d80-126">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="f9d80-126">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="f9d80-127">Modifica a configuração de um aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="f9d80-127">Modifies a web app's configuration.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="f9d80-128">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f9d80-128">Next steps</span></span>

<span data-ttu-id="f9d80-129">Para saber mais sobre o módulo do Azure PowerShell, confira a [Documentação do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f9d80-129">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="f9d80-130">Exemplos adicionais do Azure PowerShell para Aplicativos Web do Serviço de Aplicativo do Azure podem ser encontrados nos [exemplos do Azure PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="f9d80-130">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
