---
title: "Exemplo do PowerShell para monitorar e dimensionar um pool elástico do SQL do Banco de Dados SQL do Azure | Microsoft Docs"
description: "Script de exemplo do Azure PowerShell para monitorar e dimensionar um pool elástico do SQL no Banco de Dados SQL do Azure"
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
ms.openlocfilehash: 7b6a5bd43aadbed33882cf0736ec70436ffdb47b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="use-powershell-to-monitor-and-scale-a-sql-elastic-pool-in-azure-sql-database"></a><span data-ttu-id="3e100-103">Use o PowerShell para monitorar e dimensionar um pool elástico do SQL no Banco de Dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="3e100-103">Use PowerShell to monitor and scale a SQL elastic pool in Azure SQL Database</span></span>

<span data-ttu-id="3e100-104">Este exemplo de script do PowerShell monitora as métricas de desempenho de um pool elástico, dimensiona-o para um nível de desempenho mais alto e cria uma regra de alerta em uma das métricas de desempenho.</span><span class="sxs-lookup"><span data-stu-id="3e100-104">This PowerShell script example monitors the performance metrics of an elastic pool, scales it to a higher performance level, and creates an alert rule on one of the performance metrics.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="3e100-105">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="3e100-105">Sample script</span></span>

<span data-ttu-id="3e100-106">[!code-powershell[principal](../../../powershell_scripts/sql-database/monitor-and-scale-pool/monitor-and-scale-pool.ps1?highlight=16-17 "Monitorar e dimensionar um Banco de Dados SQL individual")]</span><span class="sxs-lookup"><span data-stu-id="3e100-106">[!code-powershell[main](../../../powershell_scripts/sql-database/monitor-and-scale-pool/monitor-and-scale-pool.ps1?highlight=16-17 "Monitor and scale single SQL Database")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="3e100-107">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="3e100-107">Clean up deployment</span></span>

<span data-ttu-id="3e100-108">Após executar o exemplo de script, o comando a seguir pode ser usado para remover o grupo de recursos e todos os recursos associados a ele.</span><span class="sxs-lookup"><span data-stu-id="3e100-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="3e100-109">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="3e100-109">Script explanation</span></span>

<span data-ttu-id="3e100-110">Este script usa os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="3e100-110">This script uses the following commands.</span></span> <span data-ttu-id="3e100-111">Cada comando na tabela redireciona para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="3e100-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="3e100-112">Command</span><span class="sxs-lookup"><span data-stu-id="3e100-112">Command</span></span> | <span data-ttu-id="3e100-113">Observações</span><span class="sxs-lookup"><span data-stu-id="3e100-113">Notes</span></span> |
|---|---|
 [<span data-ttu-id="3e100-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="3e100-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="3e100-115">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="3e100-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="3e100-116">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="3e100-116">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="3e100-117">Cria um servidor lógico que hospeda um banco de dados ou pool elástico.</span><span class="sxs-lookup"><span data-stu-id="3e100-117">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="3e100-118">New-AzureRmSqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="3e100-118">New-AzureRmSqlElasticPool</span></span>](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) | <span data-ttu-id="3e100-119">Cria um pool elástico dentro de um servidor lógico.</span><span class="sxs-lookup"><span data-stu-id="3e100-119">Creates an elastic pool within a logical server.</span></span> |
| [<span data-ttu-id="3e100-120">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="3e100-120">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="3e100-121">Cria um banco de dados em um servidor lógico como um banco de dados individual ou em pool.</span><span class="sxs-lookup"><span data-stu-id="3e100-121">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="3e100-122">Get-AzureRmMetric</span><span class="sxs-lookup"><span data-stu-id="3e100-122">Get-AzureRmMetric</span></span>](/powershell/module/azurerm.insights/get-azurermmetric) | <span data-ttu-id="3e100-123">Mostra as informações de uso do tamanho do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="3e100-123">Shows the size usage information for the database.</span></span>|
| [<span data-ttu-id="3e100-124">Add-AzureRMMetricAlertRule</span><span class="sxs-lookup"><span data-stu-id="3e100-124">Add-AzureRMMetricAlertRule</span></span>](/powershell/module/azurerm.insights/add-azurermmetricalertrule) | <span data-ttu-id="3e100-125">Adiciona ou atualiza uma regra de alerta com base em métricas.</span><span class="sxs-lookup"><span data-stu-id="3e100-125">Adds or updates a metric-based alert rule.</span></span> |
| [<span data-ttu-id="3e100-126">Set-AzureRmSqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="3e100-126">Set-AzureRmSqlElasticPool</span></span>](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) | <span data-ttu-id="3e100-127">Atualiza as propriedades do pool elástico</span><span class="sxs-lookup"><span data-stu-id="3e100-127">Updates elastic pool properties</span></span> |
| [<span data-ttu-id="3e100-128">Add-AzureRMMetricAlertRule</span><span class="sxs-lookup"><span data-stu-id="3e100-128">Add-AzureRMMetricAlertRule</span></span>](/powershell/module/azurerm.insights/add-azurermmetricalertrule) | <span data-ttu-id="3e100-129">Define uma regra de alerta para monitorar automaticamente DTUs no futuro.</span><span class="sxs-lookup"><span data-stu-id="3e100-129">Sets an alert rule to automatically monitor DTUs in the future.</span></span> |
| [<span data-ttu-id="3e100-130">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="3e100-130">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="3e100-131">Exclui um grupo de recursos, incluindo todos os recursos aninhados.</span><span class="sxs-lookup"><span data-stu-id="3e100-131">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="3e100-132">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3e100-132">Next steps</span></span>

<span data-ttu-id="3e100-133">Para obter mais informações sobre o Azure PowerShell, confira [Documentação do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="3e100-133">For more information on the Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="3e100-134">Os exemplos de script do PowerShell do Banco de Dados SQL adicionais podem ser encontrados nos [scripts do PowerShell do Banco de Dados SQL do Azure](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="3e100-134">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
