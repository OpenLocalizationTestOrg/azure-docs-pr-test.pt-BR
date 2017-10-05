---
title: "Exemplo do PowerShell para mover um pool elástico do banco de dados SQL do Azure | Microsoft Docs"
description: "Script de exemplo do Azure PowerShell para mover um banco de dados SQL entre pools elásticos usando o Azure PowerShell"
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
ms.openlocfilehash: 58f14dc668f25f17e93fcaf30f72b15a46d71484
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="use-powershell-to-create-elastic-pools-and-move-databases-between-elastic-pools"></a><span data-ttu-id="7cb49-103">Usar o PowerShell para criar pools elásticos e mover bancos de dados entre pools elásticos</span><span class="sxs-lookup"><span data-stu-id="7cb49-103">Use PowerShell to create elastic pools and move databases between elastic pools</span></span>

<span data-ttu-id="7cb49-104">Este exemplo de script do PowerShell cria dois pools elásticos e move um banco de dados de um pool elástico para outro pool elástico, depois move um banco de dados de um pool elástico para um nível de desempenho de banco de dados individual.</span><span class="sxs-lookup"><span data-stu-id="7cb49-104">This PowerShell script example creates two elastic pools and moves a database from one elastic pool into another elastic pool, and then moves a database out of an elastic pool to a single database performance level.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="7cb49-105">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="7cb49-105">Sample script</span></span>

<span data-ttu-id="7cb49-106">[!code-powershell[principal](../../../powershell_scripts/sql-database/move-database-between-pools-and-standalone/move-database-between-pools-and-standalone.ps1?highlight=17-18 "Mover banco de dados entre pools")]</span><span class="sxs-lookup"><span data-stu-id="7cb49-106">[!code-powershell[main](../../../powershell_scripts/sql-database/move-database-between-pools-and-standalone/move-database-between-pools-and-standalone.ps1?highlight=17-18 "Move database between pools")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="7cb49-107">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="7cb49-107">Clean up deployment</span></span>

<span data-ttu-id="7cb49-108">Após executar o exemplo de script, o comando a seguir pode ser usado para remover o grupo de recursos e todos os recursos associados a ele.</span><span class="sxs-lookup"><span data-stu-id="7cb49-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="7cb49-109">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="7cb49-109">Script explanation</span></span>

<span data-ttu-id="7cb49-110">Este script usa os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="7cb49-110">This script uses the following commands.</span></span> <span data-ttu-id="7cb49-111">Cada comando na tabela redireciona para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="7cb49-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="7cb49-112">Command</span><span class="sxs-lookup"><span data-stu-id="7cb49-112">Command</span></span> | <span data-ttu-id="7cb49-113">Observações</span><span class="sxs-lookup"><span data-stu-id="7cb49-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="7cb49-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="7cb49-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="7cb49-115">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="7cb49-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="7cb49-116">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="7cb49-116">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="7cb49-117">Cria um servidor lógico que hospeda um banco de dados ou pool elástico.</span><span class="sxs-lookup"><span data-stu-id="7cb49-117">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="7cb49-118">New-AzureRmSqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="7cb49-118">New-AzureRmSqlElasticPool</span></span>](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) | <span data-ttu-id="7cb49-119">Cria um pool elástico dentro de um servidor lógico.</span><span class="sxs-lookup"><span data-stu-id="7cb49-119">Creates an elastic pool within a logical server.</span></span> |
| [<span data-ttu-id="7cb49-120">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="7cb49-120">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="7cb49-121">Cria um banco de dados em um servidor lógico como um banco de dados individual ou em pool.</span><span class="sxs-lookup"><span data-stu-id="7cb49-121">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="7cb49-122">Set-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="7cb49-122">Set-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabase) | <span data-ttu-id="7cb49-123">Atualiza as propriedades do banco de dados ou move um banco de dados para dentro, para fora entre pools elásticos.</span><span class="sxs-lookup"><span data-stu-id="7cb49-123">Updates database properties or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="7cb49-124">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="7cb49-124">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="7cb49-125">Exclui um grupo de recursos, incluindo todos os recursos aninhados.</span><span class="sxs-lookup"><span data-stu-id="7cb49-125">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="7cb49-126">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7cb49-126">Next steps</span></span>

<span data-ttu-id="7cb49-127">Para obter mais informações sobre o Azure PowerShell, confira [Documentação do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="7cb49-127">For more information on the Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="7cb49-128">Os exemplos de script do PowerShell do Banco de Dados SQL adicionais podem ser encontrados nos [scripts do PowerShell do Banco de Dados SQL do Azure](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="7cb49-128">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
