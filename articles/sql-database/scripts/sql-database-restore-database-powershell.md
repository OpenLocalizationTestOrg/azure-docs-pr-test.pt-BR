---
title: Exemplo do PowerShell para restaurar o backup do Banco de Dados SQL do Azure | Microsoft Docs
description: "Script de exemplo do Azure PowerShell para restaurar um Banco de Dados SQL do Azure de backups com redundância geográfica"
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: business continuity
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: ae1d0c828ae1e7e1e7e07dcc7d6157187a3859d3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="use-powershell-to-restore-an-azure-sql-database-from-backups"></a><span data-ttu-id="2b267-103">Usar o PowerShell para restaurar um Banco de Dados SQL do Azure de backups</span><span class="sxs-lookup"><span data-stu-id="2b267-103">Use PowerShell to restore an Azure SQL database from backups</span></span>

<span data-ttu-id="2b267-104">Este exemplo de script do PowerShell restaura um Banco de Dados SQL do Azure de um backup com redundância geográfica, restaura um Banco de Dados SQL do Azure excluído para o backup mais recente e restaura um Banco de Dados SQL do Azure para um ponto no tempo específico.</span><span class="sxs-lookup"><span data-stu-id="2b267-104">This PowerShell script example restores an Azure SQL database from a geo-redundant backup, restores a deleted Azure SQL database to its latest backup, and restores an Azure SQL database to a specific point in time.</span></span>  

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="2b267-105">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="2b267-105">Sample script</span></span>

<span data-ttu-id="2b267-106">[!code-powershell[principal](../../../powershell_scripts/sql-database/restore-database/restore-database.ps1?highlight=17-18 "Criar Banco de Dados SQL")]</span><span class="sxs-lookup"><span data-stu-id="2b267-106">[!code-powershell[main](../../../powershell_scripts/sql-database/restore-database/restore-database.ps1?highlight=17-18 "Create SQL Database")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="2b267-107">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="2b267-107">Clean up deployment</span></span>

<span data-ttu-id="2b267-108">Após executar o exemplo de script, o comando a seguir pode ser usado para remover o grupo de recursos e todos os recursos associados a ele.</span><span class="sxs-lookup"><span data-stu-id="2b267-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="2b267-109">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="2b267-109">Script explanation</span></span>

<span data-ttu-id="2b267-110">Este script usa os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="2b267-110">This script uses the following commands.</span></span> <span data-ttu-id="2b267-111">Cada comando na tabela redireciona para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="2b267-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="2b267-112">Command</span><span class="sxs-lookup"><span data-stu-id="2b267-112">Command</span></span> | <span data-ttu-id="2b267-113">Observações</span><span class="sxs-lookup"><span data-stu-id="2b267-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="2b267-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="2b267-114">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/new-azurermresourcegroup) | <span data-ttu-id="2b267-115">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="2b267-115">Creates a resource group in which all resources are stored.</span></span> | [<span data-ttu-id="2b267-116">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="2b267-116">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="2b267-117">Cria um servidor lógico que hospeda um banco de dados ou pool elástico.</span><span class="sxs-lookup"><span data-stu-id="2b267-117">Creates a logical server that hosts a database or elastic pool.</span></span> | 
| [<span data-ttu-id="2b267-118">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="2b267-118">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="2b267-119">Cria um banco de dados em um servidor lógico como um banco de dados individual ou em pool.</span><span class="sxs-lookup"><span data-stu-id="2b267-119">Creates a database in a logical server as a single or a pooled database.</span></span> |
[<span data-ttu-id="2b267-120">Get-AzureRmSqlDatabaseGeoBackup</span><span class="sxs-lookup"><span data-stu-id="2b267-120">Get-AzureRmSqlDatabaseGeoBackup</span></span>](/powershell/module/azurerm.sql/get-azurermsqldatabasegeobackup) | <span data-ttu-id="2b267-121">Obtém um backup com redundância geográfica de um banco de dados.</span><span class="sxs-lookup"><span data-stu-id="2b267-121">Gets a geo-redundant backup of a database.</span></span> |
| [<span data-ttu-id="2b267-122">Restore-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="2b267-122">Restore-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/restore-azurermsqldatabase) | <span data-ttu-id="2b267-123">Restaura um banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="2b267-123">Restores a SQL database.</span></span> |
|[<span data-ttu-id="2b267-124">Remove-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="2b267-124">Remove-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/remove-azurermsqldatabase) | <span data-ttu-id="2b267-125">Remove um Banco de Dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="2b267-125">Removes an Azure SQL database.</span></span> |
| [<span data-ttu-id="2b267-126">Get-AzureRmSqlDeletedDatabaseBackup</span><span class="sxs-lookup"><span data-stu-id="2b267-126">Get-AzureRmSqlDeletedDatabaseBackup</span></span>](/powershell/module/azurerm.sql/get-azurermsqldeleteddatabasebackup) | <span data-ttu-id="2b267-127">Obtém um banco de dados excluído que você pode restaurar.</span><span class="sxs-lookup"><span data-stu-id="2b267-127">Gets a deleted database that you can restore.</span></span> |
| [<span data-ttu-id="2b267-128">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="2b267-128">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="2b267-129">Exclui um grupo de recursos, incluindo todos os recursos aninhados.</span><span class="sxs-lookup"><span data-stu-id="2b267-129">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="2b267-130">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2b267-130">Next steps</span></span>

<span data-ttu-id="2b267-131">Para obter mais informações sobre o Azure PowerShell, confira [Documentação do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2b267-131">For more information on the Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="2b267-132">Os exemplos de script do PowerShell do Banco de Dados SQL adicionais podem ser encontrados nos [scripts do PowerShell do Banco de Dados SQL do Azure](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="2b267-132">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
