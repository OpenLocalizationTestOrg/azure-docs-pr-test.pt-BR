---
title: "Azure pool aaaPowerShell exemplo-monitor escala SQL Elástico banco de dados SQL | Microsoft Docs"
description: "Toomonitor de script de exemplo do PowerShell do Azure e a escala um pool Elástico do SQL no banco de dados do SQL Azure"
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
ms.openlocfilehash: 149a45174ccb8072ea21753364196c7f98fd4101
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toomonitor-and-scale-a-sql-elastic-pool-in-azure-sql-database"></a><span data-ttu-id="1855d-103">Use o PowerShell toomonitor e dimensionar um pool Elástico do SQL no banco de dados do SQL Azure</span><span class="sxs-lookup"><span data-stu-id="1855d-103">Use PowerShell toomonitor and scale a SQL elastic pool in Azure SQL Database</span></span>

<span data-ttu-id="1855d-104">Este exemplo de script do PowerShell monitores Olá métricas de desempenho de um pool Elástico, redimensiona tooa mais alto nível de desempenho e cria uma regra de alerta em uma saudação métricas de desempenho.</span><span class="sxs-lookup"><span data-stu-id="1855d-104">This PowerShell script example monitors hello performance metrics of an elastic pool, scales it tooa higher performance level, and creates an alert rule on one of hello performance metrics.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="1855d-105">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="1855d-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/monitor-and-scale-pool/monitor-and-scale-pool.ps1?highlight=16-17 "Monitor and scale single SQL Database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="1855d-106">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="1855d-106">Clean up deployment</span></span>

<span data-ttu-id="1855d-107">Após a execução do exemplo de script hello, Olá comando a seguir pode ser usado tooremove grupo de recursos de saudação e todos os recursos associados a ele.</span><span class="sxs-lookup"><span data-stu-id="1855d-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="1855d-108">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="1855d-108">Script explanation</span></span>

<span data-ttu-id="1855d-109">Esse script usa Olá comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="1855d-109">This script uses hello following commands.</span></span> <span data-ttu-id="1855d-110">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="1855d-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="1855d-111">Command</span><span class="sxs-lookup"><span data-stu-id="1855d-111">Command</span></span> | <span data-ttu-id="1855d-112">Observações</span><span class="sxs-lookup"><span data-stu-id="1855d-112">Notes</span></span> |
|---|---|
 [<span data-ttu-id="1855d-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="1855d-113">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="1855d-114">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="1855d-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="1855d-115">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="1855d-115">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="1855d-116">Cria um servidor lógico que hospeda um banco de dados ou pool elástico.</span><span class="sxs-lookup"><span data-stu-id="1855d-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="1855d-117">New-AzureRmSqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="1855d-117">New-AzureRmSqlElasticPool</span></span>](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) | <span data-ttu-id="1855d-118">Cria um pool elástico dentro de um servidor lógico.</span><span class="sxs-lookup"><span data-stu-id="1855d-118">Creates an elastic pool within a logical server.</span></span> |
| [<span data-ttu-id="1855d-119">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="1855d-119">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="1855d-120">Cria um banco de dados em um servidor lógico como um banco de dados individual ou em pool.</span><span class="sxs-lookup"><span data-stu-id="1855d-120">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="1855d-121">Get-AzureRmMetric</span><span class="sxs-lookup"><span data-stu-id="1855d-121">Get-AzureRmMetric</span></span>](/powershell/module/azurerm.insights/get-azurermmetric) | <span data-ttu-id="1855d-122">Mostra informações de uso de tamanho de saudação do banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="1855d-122">Shows hello size usage information for hello database.</span></span>|
| [<span data-ttu-id="1855d-123">Add-AzureRMMetricAlertRule</span><span class="sxs-lookup"><span data-stu-id="1855d-123">Add-AzureRMMetricAlertRule</span></span>](/powershell/module/azurerm.insights/add-azurermmetricalertrule) | <span data-ttu-id="1855d-124">Adiciona ou atualiza uma regra de alerta com base em métricas.</span><span class="sxs-lookup"><span data-stu-id="1855d-124">Adds or updates a metric-based alert rule.</span></span> |
| [<span data-ttu-id="1855d-125">Set-AzureRmSqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="1855d-125">Set-AzureRmSqlElasticPool</span></span>](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) | <span data-ttu-id="1855d-126">Atualiza as propriedades do pool elástico</span><span class="sxs-lookup"><span data-stu-id="1855d-126">Updates elastic pool properties</span></span> |
| [<span data-ttu-id="1855d-127">Add-AzureRMMetricAlertRule</span><span class="sxs-lookup"><span data-stu-id="1855d-127">Add-AzureRMMetricAlertRule</span></span>](/powershell/module/azurerm.insights/add-azurermmetricalertrule) | <span data-ttu-id="1855d-128">Define uma regra de alerta do monitor de tooautomatically DTUs Olá futuras.</span><span class="sxs-lookup"><span data-stu-id="1855d-128">Sets an alert rule tooautomatically monitor DTUs in hello future.</span></span> |
| [<span data-ttu-id="1855d-129">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="1855d-129">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="1855d-130">Exclui um grupo de recursos, incluindo todos os recursos aninhados.</span><span class="sxs-lookup"><span data-stu-id="1855d-130">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="1855d-131">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1855d-131">Next steps</span></span>

<span data-ttu-id="1855d-132">Para obter mais informações sobre hello Azure PowerShell, consulte [documentação do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="1855d-132">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="1855d-133">Exemplos de script do PowerShell do banco de dados SQL adicionais podem ser encontrados no hello [scripts de banco de dados do SQL Azure PowerShell](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="1855d-133">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
