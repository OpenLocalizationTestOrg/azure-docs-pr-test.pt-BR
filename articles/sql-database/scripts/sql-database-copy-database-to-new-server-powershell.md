---
title: "Exemplo do PowerShell de cópia do Banco de Dados SQL do Azure para o novo servidor | Microsoft Docs"
description: Script de exemplo do Azure PowerShell para copiar um Banco de Dados SQL para um novo servidor
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: load & move data
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: 005ea2e782f8e1cff29f743d9584eb2af2c77509
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="use-powershell-to-copy-a-sql-database-to-a-new-server"></a><span data-ttu-id="42532-103">Usar o PowerShell para copiar um Banco de Dados SQL para um novo servidor</span><span class="sxs-lookup"><span data-stu-id="42532-103">Use PowerShell to copy a SQL database to a new server</span></span>

<span data-ttu-id="42532-104">Este exemplo de script do PowerShell cria uma cópia de um banco de dados existente em um novo servidor.</span><span class="sxs-lookup"><span data-stu-id="42532-104">This PowerShell script example creates a copy of an existing database in a new server.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="copy-a-database-to-a-new-server"></a><span data-ttu-id="42532-105">Copiar um banco de dados para um novo servidor</span><span class="sxs-lookup"><span data-stu-id="42532-105">Copy a database to a new server</span></span>

<span data-ttu-id="42532-106">[!code-powershell[principal](../../../powershell_scripts/sql-database/copy-database-to-new-server/copy-database-to-new-server.ps1?highlight=18-21 "Copiar banco de dados para um novo servidor")]</span><span class="sxs-lookup"><span data-stu-id="42532-106">[!code-powershell[main](../../../powershell_scripts/sql-database/copy-database-to-new-server/copy-database-to-new-server.ps1?highlight=18-21 "Copy database to new server")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="42532-107">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="42532-107">Clean up deployment</span></span>

<span data-ttu-id="42532-108">Após executar o exemplo de script, o comando a seguir pode ser usado para remover o grupo de recursos e todos os recursos associados a ele.</span><span class="sxs-lookup"><span data-stu-id="42532-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="42532-109">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="42532-109">Script explanation</span></span>

<span data-ttu-id="42532-110">Este script usa os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="42532-110">This script uses the following commands.</span></span> <span data-ttu-id="42532-111">Cada comando na tabela redireciona para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="42532-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="42532-112">Command</span><span class="sxs-lookup"><span data-stu-id="42532-112">Command</span></span> | <span data-ttu-id="42532-113">Observações</span><span class="sxs-lookup"><span data-stu-id="42532-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="42532-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="42532-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="42532-115">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="42532-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="42532-116">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="42532-116">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="42532-117">Cria um servidor lógico que hospeda um banco de dados ou pool elástico.</span><span class="sxs-lookup"><span data-stu-id="42532-117">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="42532-118">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="42532-118">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="42532-119">Cria um banco de dados em um servidor lógico como um banco de dados individual ou em pool.</span><span class="sxs-lookup"><span data-stu-id="42532-119">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="42532-120">New-AzureRmSqlDatabaseCopy</span><span class="sxs-lookup"><span data-stu-id="42532-120">New-AzureRmSqlDatabaseCopy</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabasecopy) | <span data-ttu-id="42532-121">Cria uma cópia de um banco de dados que usa o instantâneo no momento atual.</span><span class="sxs-lookup"><span data-stu-id="42532-121">Creates a copy of a database that uses the snapshot at the current time.</span></span> |
| [<span data-ttu-id="42532-122">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="42532-122">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="42532-123">Exclui um grupo de recursos, incluindo todos os recursos aninhados.</span><span class="sxs-lookup"><span data-stu-id="42532-123">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="42532-124">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="42532-124">Next steps</span></span>

<span data-ttu-id="42532-125">Para obter mais informações sobre o Azure PowerShell, confira [Documentação do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="42532-125">For more information on the Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="42532-126">Os exemplos de script do PowerShell do Banco de Dados SQL adicionais podem ser encontrados nos [scripts do PowerShell do Banco de Dados SQL do Azure](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="42532-126">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
