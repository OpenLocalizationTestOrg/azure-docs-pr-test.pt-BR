---
title: "pool Elástico do banco de dados SQL aaaPowerShell exemplo move SQL do Azure | Microsoft Docs"
description: "Azure PowerShell exemplo script toomove um banco de dados do SQL entre pools Elásticos usando o PowerShell"
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
ms.openlocfilehash: 501e82ce93a31264d0625fb0243b4e44dcb2d007
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toocreate-elastic-pools-and-move-databases-between-elastic-pools"></a><span data-ttu-id="ced1e-103">Use pools Elásticos do PowerShell toocreate e mover bancos de dados entre pools Elásticos</span><span class="sxs-lookup"><span data-stu-id="ced1e-103">Use PowerShell toocreate elastic pools and move databases between elastic pools</span></span>

<span data-ttu-id="ced1e-104">Este exemplo de script do PowerShell cria dois pools Elásticos e move um banco de dados de um pool Elástico em outro pool Elástico e move um banco de dados fora de um nível de desempenho do pool Elástico tooa único banco de dados.</span><span class="sxs-lookup"><span data-stu-id="ced1e-104">This PowerShell script example creates two elastic pools and moves a database from one elastic pool into another elastic pool, and then moves a database out of an elastic pool tooa single database performance level.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="ced1e-105">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="ced1e-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/move-database-between-pools-and-standalone/move-database-between-pools-and-standalone.ps1?highlight=17-18 "Move database between pools")]

## <a name="clean-up-deployment"></a><span data-ttu-id="ced1e-106">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="ced1e-106">Clean up deployment</span></span>

<span data-ttu-id="ced1e-107">Após a execução do exemplo de script hello, Olá comando a seguir pode ser usado tooremove grupo de recursos de saudação e todos os recursos associados a ele.</span><span class="sxs-lookup"><span data-stu-id="ced1e-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="ced1e-108">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="ced1e-108">Script explanation</span></span>

<span data-ttu-id="ced1e-109">Esse script usa Olá comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="ced1e-109">This script uses hello following commands.</span></span> <span data-ttu-id="ced1e-110">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="ced1e-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="ced1e-111">Command</span><span class="sxs-lookup"><span data-stu-id="ced1e-111">Command</span></span> | <span data-ttu-id="ced1e-112">Observações</span><span class="sxs-lookup"><span data-stu-id="ced1e-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="ced1e-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="ced1e-113">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="ced1e-114">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="ced1e-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="ced1e-115">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="ced1e-115">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="ced1e-116">Cria um servidor lógico que hospeda um banco de dados ou pool elástico.</span><span class="sxs-lookup"><span data-stu-id="ced1e-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="ced1e-117">New-AzureRmSqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="ced1e-117">New-AzureRmSqlElasticPool</span></span>](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) | <span data-ttu-id="ced1e-118">Cria um pool elástico dentro de um servidor lógico.</span><span class="sxs-lookup"><span data-stu-id="ced1e-118">Creates an elastic pool within a logical server.</span></span> |
| [<span data-ttu-id="ced1e-119">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="ced1e-119">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="ced1e-120">Cria um banco de dados em um servidor lógico como um banco de dados individual ou em pool.</span><span class="sxs-lookup"><span data-stu-id="ced1e-120">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="ced1e-121">Set-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="ced1e-121">Set-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabase) | <span data-ttu-id="ced1e-122">Atualiza as propriedades do banco de dados ou move um banco de dados para dentro, para fora entre pools elásticos.</span><span class="sxs-lookup"><span data-stu-id="ced1e-122">Updates database properties or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="ced1e-123">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="ced1e-123">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="ced1e-124">Exclui um grupo de recursos, incluindo todos os recursos aninhados.</span><span class="sxs-lookup"><span data-stu-id="ced1e-124">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="ced1e-125">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ced1e-125">Next steps</span></span>

<span data-ttu-id="ced1e-126">Para obter mais informações sobre hello Azure PowerShell, consulte [documentação do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ced1e-126">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="ced1e-127">Exemplos de script do PowerShell do banco de dados SQL adicionais podem ser encontrados no hello [scripts de banco de dados do SQL Azure PowerShell](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="ced1e-127">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
