---
title: aaaAzure exemplo de Script do PowerShell - se conectar a um banco de dados SQL de tooa do aplicativo de web | Microsoft Docs
description: Script do PowerShell do Azure de exemplo - conectar a um banco de dados SQL de tooa do aplicativo de web
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 055440a9-fff1-49b2-b964-9c95b364e533
ms.service: app-service
ms.devlang: multiple
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 03/20/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 8f80b940378d020cbcaec2c1bbc28bae1a3ef35a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-web-app-tooa-sql-database"></a><span data-ttu-id="918df-103">Conectar a um banco de dados SQL de tooa do aplicativo de web</span><span class="sxs-lookup"><span data-stu-id="918df-103">Connect a web app tooa SQL database</span></span>

<span data-ttu-id="918df-104">Nesse cenário, você aprenderá como toocreate um banco de dados do SQL Azure e um Azure aplicativo da web.</span><span class="sxs-lookup"><span data-stu-id="918df-104">In this scenario you will learn how toocreate an Azure SQL database and an Azure web app.</span></span> <span data-ttu-id="918df-105">Em seguida, você vinculará aplicativo hello SQL banco de dados toohello web usando configurações do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="918df-105">Then you will link hello SQL database toohello web app using app settings.</span></span>

<span data-ttu-id="918df-106">Se necessário, instale Olá PowerShell do Azure usando a instrução Olá encontrado no hello [guia do PowerShell do Azure](/powershell/azure/overview)e, em seguida, execute `Login-AzureRmAccount` toocreate uma conexão com o Azure.</span><span class="sxs-lookup"><span data-stu-id="918df-106">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="918df-107">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="918df-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/connect-to-sql/connect-to-sql.ps1?highlight=13 "Connect a web app tooa SQL database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="918df-108">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="918df-108">Clean up deployment</span></span> 

<span data-ttu-id="918df-109">Após a execução do exemplo de script hello, Olá comando a seguir pode ser usado tooremove grupo de recursos de saudação, aplicativo web e recursos todos relacionados.</span><span class="sxs-lookup"><span data-stu-id="918df-109">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="918df-110">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="918df-110">Script explanation</span></span>

<span data-ttu-id="918df-111">Esse script usa Olá comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="918df-111">This script uses hello following commands.</span></span> <span data-ttu-id="918df-112">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="918df-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="918df-113">Command</span><span class="sxs-lookup"><span data-stu-id="918df-113">Command</span></span> | <span data-ttu-id="918df-114">Observações</span><span class="sxs-lookup"><span data-stu-id="918df-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="918df-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="918df-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="918df-116">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="918df-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="918df-117">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="918df-117">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="918df-118">Cria um Plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="918df-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="918df-119">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="918df-119">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="918df-120">Cria um aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="918df-120">Creates a web app.</span></span> |
| [<span data-ttu-id="918df-121">New-AzureRMSQLServer</span><span class="sxs-lookup"><span data-stu-id="918df-121">New-AzureRMSQLServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="918df-122">Cria um servidor de Banco de Dados SQL.</span><span class="sxs-lookup"><span data-stu-id="918df-122">Creates a SQL Database server.</span></span> |
| [<span data-ttu-id="918df-123">New-AzureRmSqlServerFirewallRule</span><span class="sxs-lookup"><span data-stu-id="918df-123">New-AzureRmSqlServerFirewallRule</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule) | <span data-ttu-id="918df-124">Cria uma regra de firewall para um servidor do Banco de Dados SQL.</span><span class="sxs-lookup"><span data-stu-id="918df-124">Creates a firewall rule for a SQL Database server.</span></span> |
| [<span data-ttu-id="918df-125">New-AzureRMSQLDatabase</span><span class="sxs-lookup"><span data-stu-id="918df-125">New-AzureRMSQLDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="918df-126">Cria um banco de dados ou um banco de dados elástico.</span><span class="sxs-lookup"><span data-stu-id="918df-126">Creates a database or an elastic database.</span></span> |
| [<span data-ttu-id="918df-127">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="918df-127">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="918df-128">Modifica a configuração de um aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="918df-128">Modifies a web app's configuration.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="918df-129">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="918df-129">Next steps</span></span>

<span data-ttu-id="918df-130">Para obter mais informações sobre o módulo do PowerShell do Azure hello, consulte [documentação do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="918df-130">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="918df-131">Exemplos adicionais do Powershell do Azure para aplicativos de Web do serviço de aplicativo do Azure podem ser encontrados no hello [exemplos do PowerShell do Azure](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="918df-131">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
