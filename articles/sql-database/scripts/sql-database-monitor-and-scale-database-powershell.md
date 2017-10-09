---
title: "banco de dados do SQL Azure aaaPowerShell exemplo-monitor escala único | Microsoft Docs"
description: "Toomonitor de script de exemplo do PowerShell do Azure e a escala de um único banco de dados do SQL Azure"
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
ms.openlocfilehash: bd8f880fb47b1360ae4962d2b039faa742de258e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toomonitor-and-scale-a-single-sql-database"></a><span data-ttu-id="fe55d-103">Use o PowerShell toomonitor e dimensionar um único banco de dados SQL</span><span class="sxs-lookup"><span data-stu-id="fe55d-103">Use PowerShell toomonitor and scale a single SQL database</span></span>

<span data-ttu-id="fe55d-104">Este exemplo de script do PowerShell monitores Olá métricas de desempenho de um banco de dados, redimensiona tooa mais alto nível de desempenho e cria uma regra de alerta em uma saudação métricas de desempenho.</span><span class="sxs-lookup"><span data-stu-id="fe55d-104">This PowerShell script example monitors hello performance metrics of a database, scales it tooa higher performance level, and creates an alert rule on one of hello performance metrics.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="fe55d-105">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="fe55d-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/monitor-and-scale-database/monitor-and-scale-database.ps1?highlight=13-14 "Monitor and scale single SQL Database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="fe55d-106">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="fe55d-106">Clean up deployment</span></span>

<span data-ttu-id="fe55d-107">Após a execução do exemplo de script hello, Olá comando a seguir pode ser usado tooremove grupo de recursos de saudação e todos os recursos associados a ele.</span><span class="sxs-lookup"><span data-stu-id="fe55d-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="fe55d-108">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="fe55d-108">Script explanation</span></span>

<span data-ttu-id="fe55d-109">Esse script usa Olá comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="fe55d-109">This script uses hello following commands.</span></span> <span data-ttu-id="fe55d-110">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="fe55d-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="fe55d-111">Command</span><span class="sxs-lookup"><span data-stu-id="fe55d-111">Command</span></span> | <span data-ttu-id="fe55d-112">Observações</span><span class="sxs-lookup"><span data-stu-id="fe55d-112">Notes</span></span> |
|---|---|
 [<span data-ttu-id="fe55d-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="fe55d-113">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="fe55d-114">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="fe55d-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="fe55d-115">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="fe55d-115">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="fe55d-116">Cria um servidor lógico que hospeda um banco de dados ou pool elástico.</span><span class="sxs-lookup"><span data-stu-id="fe55d-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="fe55d-117">Get-AzureRmMetric</span><span class="sxs-lookup"><span data-stu-id="fe55d-117">Get-AzureRmMetric</span></span>](/powershell/module/azurerm.insights/get-azurermmetric) | <span data-ttu-id="fe55d-118">Mostra informações de uso de tamanho de saudação do banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="fe55d-118">Shows hello size usage information for hello database.</span></span>|
| [<span data-ttu-id="fe55d-119">Set-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="fe55d-119">Set-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabase) | <span data-ttu-id="fe55d-120">Atualiza as propriedades do banco de dados ou move um banco de dados para dentro, para fora entre pools elásticos.</span><span class="sxs-lookup"><span data-stu-id="fe55d-120">Updates database properties or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="fe55d-121">Add-AzureRMMetricAlertRule</span><span class="sxs-lookup"><span data-stu-id="fe55d-121">Add-AzureRMMetricAlertRule</span></span>](/powershell/module/azurerm.insights/add-azurermmetricalertrule) | <span data-ttu-id="fe55d-122">Define uma regra de alerta do monitor de tooautomatically DTUs Olá futuras.</span><span class="sxs-lookup"><span data-stu-id="fe55d-122">Sets an alert rule tooautomatically monitor DTUs in hello future.</span></span> |
| [<span data-ttu-id="fe55d-123">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="fe55d-123">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="fe55d-124">Exclui um grupo de recursos, incluindo todos os recursos aninhados.</span><span class="sxs-lookup"><span data-stu-id="fe55d-124">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="fe55d-125">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="fe55d-125">Next steps</span></span>

<span data-ttu-id="fe55d-126">Para obter mais informações sobre hello Azure PowerShell, consulte [documentação do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="fe55d-126">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="fe55d-127">Exemplos de script do PowerShell do banco de dados SQL adicionais podem ser encontrados no hello [scripts de banco de dados do SQL Azure PowerShell](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="fe55d-127">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
