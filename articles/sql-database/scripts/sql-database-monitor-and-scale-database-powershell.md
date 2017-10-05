---
title: "Exemplo do PowerShell para monitorar e dimensionar um único Banco de Dados SQL do Azure | Microsoft Docs"
description: "Script de exemplo do Azure PowerShell para monitorar e dimensionar um único banco de dados SQL do Azure"
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: 5d08335f4b1d6c5c6a120cbfb86ab2c62b79bb9f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="use-powershell-to-monitor-and-scale-a-single-sql-database"></a><span data-ttu-id="887d5-103">Usar o PowerShell para monitorar e dimensionar um único banco e dados SQL</span><span class="sxs-lookup"><span data-stu-id="887d5-103">Use PowerShell to monitor and scale a single SQL database</span></span>

<span data-ttu-id="887d5-104">Este exemplo de script do PowerShell monitora as métricas de desempenho de um banco de dados, dimensiona-o para um nível de desempenho mais alto e cria uma regra de alerta em uma das métricas de desempenho.</span><span class="sxs-lookup"><span data-stu-id="887d5-104">This PowerShell script example monitors the performance metrics of a database, scales it to a higher performance level, and creates an alert rule on one of the performance metrics.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="887d5-105">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="887d5-105">Sample script</span></span>

<span data-ttu-id="887d5-106">[!code-powershell[principal](../../../powershell_scripts/sql-database/monitor-and-scale-database/monitor-and-scale-database.ps1?highlight=13-14 "Monitorar e dimensionar um Banco de Dados SQL individual")]</span><span class="sxs-lookup"><span data-stu-id="887d5-106">[!code-powershell[main](../../../powershell_scripts/sql-database/monitor-and-scale-database/monitor-and-scale-database.ps1?highlight=13-14 "Monitor and scale single SQL Database")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="887d5-107">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="887d5-107">Clean up deployment</span></span>

<span data-ttu-id="887d5-108">Após executar o exemplo de script, o comando a seguir pode ser usado para remover o grupo de recursos e todos os recursos associados a ele.</span><span class="sxs-lookup"><span data-stu-id="887d5-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="887d5-109">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="887d5-109">Script explanation</span></span>

<span data-ttu-id="887d5-110">Este script usa os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="887d5-110">This script uses the following commands.</span></span> <span data-ttu-id="887d5-111">Cada comando na tabela redireciona para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="887d5-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="887d5-112">Command</span><span class="sxs-lookup"><span data-stu-id="887d5-112">Command</span></span> | <span data-ttu-id="887d5-113">Observações</span><span class="sxs-lookup"><span data-stu-id="887d5-113">Notes</span></span> |
|---|---|
 [<span data-ttu-id="887d5-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="887d5-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="887d5-115">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="887d5-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="887d5-116">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="887d5-116">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="887d5-117">Cria um servidor lógico que hospeda um banco de dados ou pool elástico.</span><span class="sxs-lookup"><span data-stu-id="887d5-117">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="887d5-118">Get-AzureRmMetric</span><span class="sxs-lookup"><span data-stu-id="887d5-118">Get-AzureRmMetric</span></span>](/powershell/module/azurerm.insights/get-azurermmetric) | <span data-ttu-id="887d5-119">Mostra as informações de uso do tamanho do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="887d5-119">Shows the size usage information for the database.</span></span>|
| [<span data-ttu-id="887d5-120">Set-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="887d5-120">Set-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabase) | <span data-ttu-id="887d5-121">Atualiza as propriedades do banco de dados ou move um banco de dados para dentro, para fora entre pools elásticos.</span><span class="sxs-lookup"><span data-stu-id="887d5-121">Updates database properties or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="887d5-122">Add-AzureRMMetricAlertRule</span><span class="sxs-lookup"><span data-stu-id="887d5-122">Add-AzureRMMetricAlertRule</span></span>](/powershell/module/azurerm.insights/add-azurermmetricalertrule) | <span data-ttu-id="887d5-123">Define uma regra de alerta para monitorar automaticamente DTUs no futuro.</span><span class="sxs-lookup"><span data-stu-id="887d5-123">Sets an alert rule to automatically monitor DTUs in the future.</span></span> |
| [<span data-ttu-id="887d5-124">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="887d5-124">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="887d5-125">Exclui um grupo de recursos, incluindo todos os recursos aninhados.</span><span class="sxs-lookup"><span data-stu-id="887d5-125">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="887d5-126">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="887d5-126">Next steps</span></span>

<span data-ttu-id="887d5-127">Para obter mais informações sobre o Azure PowerShell, confira [Documentação do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="887d5-127">For more information on the Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="887d5-128">Os exemplos de script do PowerShell do Banco de Dados SQL adicionais podem ser encontrados nos [scripts do PowerShell do Banco de Dados SQL do Azure](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="887d5-128">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
