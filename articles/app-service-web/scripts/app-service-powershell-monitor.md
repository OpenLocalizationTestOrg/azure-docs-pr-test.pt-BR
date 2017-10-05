---
title: Exemplo de Script do Azure PowerShell - Monitorar um aplicativo Web com logs de servidor Web | Microsoft Docs
description: Exemplo de Script do Azure PowerShell - Monitorar um aplicativo Web com logs de servidor Web
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 5805d7cd-9e56-4eba-bd85-75b013690ff5
ms.service: app-service
ms.devlang: multiple
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 03/20/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 34a3dd318cb9896342fce870922ecd113b3ed08d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-a-web-app-with-web-server-logs"></a><span data-ttu-id="27426-103">Monitorar um aplicativo web com logs do servidor Web</span><span class="sxs-lookup"><span data-stu-id="27426-103">Monitor a web app with web server logs</span></span>

<span data-ttu-id="27426-104">Neste cenário você criará um grupo de recursos, o Plano do Serviço de Aplicativo, o aplicativo Web e configurar o aplicativo Web para habilitar logs de servidor web.</span><span class="sxs-lookup"><span data-stu-id="27426-104">In this scenario you will create a resource group, app service plan, web app and configure the web app to enable web server logs.</span></span> <span data-ttu-id="27426-105">Em seguida, você baixará os arquivos de log para análise.</span><span class="sxs-lookup"><span data-stu-id="27426-105">You will then download the log files for review.</span></span>

<span data-ttu-id="27426-106">Se necessário, instale o Azure PowerShell usando a instrução encontrada no [guia do Azure PowerShell](/powershell/azure/overview) e, em seguida, execute `Login-AzureRmAccount` para criar uma conexão com o Azure.</span><span class="sxs-lookup"><span data-stu-id="27426-106">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="27426-107">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="27426-107">Sample script</span></span>

<span data-ttu-id="27426-108">[!code-powershell[principal](../../../powershell_scripts/app-service/monitor-with-logs/monitor-with-logs.ps1 "Monitorar um aplicativo web com logs do servidor Web")]</span><span class="sxs-lookup"><span data-stu-id="27426-108">[!code-powershell[main](../../../powershell_scripts/app-service/monitor-with-logs/monitor-with-logs.ps1 "Monitor a web app with web server logs")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="27426-109">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="27426-109">Clean up deployment</span></span> 

<span data-ttu-id="27426-110">Após a execução da amostra de script, o comando a seguir pode ser usado para remover o grupo de recursos, o aplicativo Web e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="27426-110">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="27426-111">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="27426-111">Script explanation</span></span>

<span data-ttu-id="27426-112">Este script usa os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="27426-112">This script uses the following commands.</span></span> <span data-ttu-id="27426-113">Cada comando na tabela redireciona para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="27426-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="27426-114">Command</span><span class="sxs-lookup"><span data-stu-id="27426-114">Command</span></span> | <span data-ttu-id="27426-115">Observações</span><span class="sxs-lookup"><span data-stu-id="27426-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="27426-116">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="27426-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="27426-117">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="27426-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="27426-118">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="27426-118">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="27426-119">Cria um Plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="27426-119">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="27426-120">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="27426-120">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="27426-121">Cria um aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="27426-121">Creates a web app.</span></span> |
| [<span data-ttu-id="27426-122">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="27426-122">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="27426-123">Modifica a configuração de um aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="27426-123">Modifies a web app's configuration.</span></span> |
| [<span data-ttu-id="27426-124">Get-AzureRMWebAppMetrics</span><span class="sxs-lookup"><span data-stu-id="27426-124">Get-AzureRMWebAppMetrics</span></span>](/powershell/module/azurerm.websites/get-azurermwebappmetrics) | <span data-ttu-id="27426-125">Obtém a métrica de um aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="27426-125">Gets a web app's metrics.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="27426-126">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="27426-126">Next steps</span></span>

<span data-ttu-id="27426-127">Para saber mais sobre o módulo do Azure PowerShell, confira a [Documentação do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="27426-127">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="27426-128">Exemplos adicionais do Azure PowerShell para Aplicativos Web do Serviço de Aplicativo do Azure podem ser encontrados nos [exemplos do Azure PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="27426-128">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
