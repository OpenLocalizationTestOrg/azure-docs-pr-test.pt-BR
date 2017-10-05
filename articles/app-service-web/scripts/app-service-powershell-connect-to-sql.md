---
title: Exemplo de script do Azure PowerShell - Conectar um aplicativo Web a um Banco de Dados SQL | Microsoft Docs
description: Exemplo de script do Azure PowerShell - Conectar um aplicativo Web a um Banco de Dados SQL
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
ms.openlocfilehash: 5312bf6b81d1cc48490b71c3f77323cca23e1559
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="connect-a-web-app-to-a-sql-database"></a><span data-ttu-id="0d9cd-103">Conectar um aplicativo Web a um Banco de Dados SQL</span><span class="sxs-lookup"><span data-stu-id="0d9cd-103">Connect a web app to a SQL database</span></span>

<span data-ttu-id="0d9cd-104">Nesse cenário, você aprenderá como criar um Banco de Dados SQL do Azure e um aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="0d9cd-104">In this scenario you will learn how to create an Azure SQL database and an Azure web app.</span></span> <span data-ttu-id="0d9cd-105">Em seguida, você vinculará o Banco de Dados SQL ao aplicativo Web usando configurações do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0d9cd-105">Then you will link the SQL database to the web app using app settings.</span></span>

<span data-ttu-id="0d9cd-106">Se necessário, instale o Azure PowerShell usando a instrução encontrada no [guia do Azure PowerShell](/powershell/azure/overview) e, em seguida, execute `Login-AzureRmAccount` para criar uma conexão com o Azure.</span><span class="sxs-lookup"><span data-stu-id="0d9cd-106">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="0d9cd-107">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="0d9cd-107">Sample script</span></span>

<span data-ttu-id="0d9cd-108">[!code-powershell[principal](../../../powershell_scripts/app-service/connect-to-sql/connect-to-sql.ps1?highlight=13 "Conectar um aplicativo Web a um Banco de Dados SQL")]</span><span class="sxs-lookup"><span data-stu-id="0d9cd-108">[!code-powershell[main](../../../powershell_scripts/app-service/connect-to-sql/connect-to-sql.ps1?highlight=13 "Connect a web app to a SQL database")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="0d9cd-109">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="0d9cd-109">Clean up deployment</span></span> 

<span data-ttu-id="0d9cd-110">Após a execução da amostra de script, o comando a seguir pode ser usado para remover o grupo de recursos, o aplicativo Web e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="0d9cd-110">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="0d9cd-111">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="0d9cd-111">Script explanation</span></span>

<span data-ttu-id="0d9cd-112">Este script usa os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="0d9cd-112">This script uses the following commands.</span></span> <span data-ttu-id="0d9cd-113">Cada comando na tabela redireciona para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="0d9cd-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="0d9cd-114">Command</span><span class="sxs-lookup"><span data-stu-id="0d9cd-114">Command</span></span> | <span data-ttu-id="0d9cd-115">Observações</span><span class="sxs-lookup"><span data-stu-id="0d9cd-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="0d9cd-116">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="0d9cd-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="0d9cd-117">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="0d9cd-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="0d9cd-118">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="0d9cd-118">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="0d9cd-119">Cria um Plano do Serviço de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0d9cd-119">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="0d9cd-120">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="0d9cd-120">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="0d9cd-121">Cria um aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="0d9cd-121">Creates a web app.</span></span> |
| [<span data-ttu-id="0d9cd-122">New-AzureRMSQLServer</span><span class="sxs-lookup"><span data-stu-id="0d9cd-122">New-AzureRMSQLServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="0d9cd-123">Cria um servidor de Banco de Dados SQL.</span><span class="sxs-lookup"><span data-stu-id="0d9cd-123">Creates a SQL Database server.</span></span> |
| [<span data-ttu-id="0d9cd-124">New-AzureRmSqlServerFirewallRule</span><span class="sxs-lookup"><span data-stu-id="0d9cd-124">New-AzureRmSqlServerFirewallRule</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule) | <span data-ttu-id="0d9cd-125">Cria uma regra de firewall para um servidor do Banco de Dados SQL.</span><span class="sxs-lookup"><span data-stu-id="0d9cd-125">Creates a firewall rule for a SQL Database server.</span></span> |
| [<span data-ttu-id="0d9cd-126">New-AzureRMSQLDatabase</span><span class="sxs-lookup"><span data-stu-id="0d9cd-126">New-AzureRMSQLDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="0d9cd-127">Cria um banco de dados ou um banco de dados elástico.</span><span class="sxs-lookup"><span data-stu-id="0d9cd-127">Creates a database or an elastic database.</span></span> |
| [<span data-ttu-id="0d9cd-128">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="0d9cd-128">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="0d9cd-129">Modifica a configuração de um aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="0d9cd-129">Modifies a web app's configuration.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="0d9cd-130">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0d9cd-130">Next steps</span></span>

<span data-ttu-id="0d9cd-131">Para saber mais sobre o módulo do Azure PowerShell, confira a [Documentação do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="0d9cd-131">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="0d9cd-132">Exemplos adicionais do Azure PowerShell para Aplicativos Web do Serviço de Aplicativo do Azure podem ser encontrados nos [exemplos do Azure PowerShell](../app-service-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="0d9cd-132">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
