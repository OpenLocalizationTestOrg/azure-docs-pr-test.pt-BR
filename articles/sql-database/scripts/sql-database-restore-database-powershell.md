---
title: "banco de dados do SQL aaaPowerShell exemplo-restauração do backup do Azure | Microsoft Docs"
description: "Azure PowerShell exemplo script toorestore um banco de dados do SQL Azure de backups com redundância geográfica"
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
ms.openlocfilehash: 68becb89e8a8680aa2efc3de8ad947e674c5fc35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toorestore-an-azure-sql-database-from-backups"></a><span data-ttu-id="cb124-103">Use o PowerShell toorestore um banco de dados do SQL Azure de backups</span><span class="sxs-lookup"><span data-stu-id="cb124-103">Use PowerShell toorestore an Azure SQL database from backups</span></span>

<span data-ttu-id="cb124-104">Este exemplo de script do PowerShell restaura um banco de dados do SQL Azure de um backup com redundância geográfica, restaura um excluída do Azure SQL database tooits mais recente backup e restaura um ponto específico de tooa de banco de dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="cb124-104">This PowerShell script example restores an Azure SQL database from a geo-redundant backup, restores a deleted Azure SQL database tooits latest backup, and restores an Azure SQL database tooa specific point in time.</span></span>  

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="cb124-105">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="cb124-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/restore-database/restore-database.ps1?highlight=17-18 "Create SQL Database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="cb124-106">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="cb124-106">Clean up deployment</span></span>

<span data-ttu-id="cb124-107">Após a execução do exemplo de script hello, Olá comando a seguir pode ser usado tooremove grupo de recursos de saudação e todos os recursos associados a ele.</span><span class="sxs-lookup"><span data-stu-id="cb124-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="cb124-108">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="cb124-108">Script explanation</span></span>

<span data-ttu-id="cb124-109">Esse script usa Olá comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="cb124-109">This script uses hello following commands.</span></span> <span data-ttu-id="cb124-110">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="cb124-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="cb124-111">Command</span><span class="sxs-lookup"><span data-stu-id="cb124-111">Command</span></span> | <span data-ttu-id="cb124-112">Observações</span><span class="sxs-lookup"><span data-stu-id="cb124-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="cb124-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="cb124-113">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/new-azurermresourcegroup) | <span data-ttu-id="cb124-114">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="cb124-114">Creates a resource group in which all resources are stored.</span></span> | [<span data-ttu-id="cb124-115">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="cb124-115">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="cb124-116">Cria um servidor lógico que hospeda um banco de dados ou pool elástico.</span><span class="sxs-lookup"><span data-stu-id="cb124-116">Creates a logical server that hosts a database or elastic pool.</span></span> | 
| [<span data-ttu-id="cb124-117">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="cb124-117">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="cb124-118">Cria um banco de dados em um servidor lógico como um banco de dados individual ou em pool.</span><span class="sxs-lookup"><span data-stu-id="cb124-118">Creates a database in a logical server as a single or a pooled database.</span></span> |
[<span data-ttu-id="cb124-119">Get-AzureRmSqlDatabaseGeoBackup</span><span class="sxs-lookup"><span data-stu-id="cb124-119">Get-AzureRmSqlDatabaseGeoBackup</span></span>](/powershell/module/azurerm.sql/get-azurermsqldatabasegeobackup) | <span data-ttu-id="cb124-120">Obtém um backup com redundância geográfica de um banco de dados.</span><span class="sxs-lookup"><span data-stu-id="cb124-120">Gets a geo-redundant backup of a database.</span></span> |
| [<span data-ttu-id="cb124-121">Restore-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="cb124-121">Restore-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/restore-azurermsqldatabase) | <span data-ttu-id="cb124-122">Restaura um banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="cb124-122">Restores a SQL database.</span></span> |
|[<span data-ttu-id="cb124-123">Remove-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="cb124-123">Remove-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/remove-azurermsqldatabase) | <span data-ttu-id="cb124-124">Remove um Banco de Dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="cb124-124">Removes an Azure SQL database.</span></span> |
| [<span data-ttu-id="cb124-125">Get-AzureRmSqlDeletedDatabaseBackup</span><span class="sxs-lookup"><span data-stu-id="cb124-125">Get-AzureRmSqlDeletedDatabaseBackup</span></span>](/powershell/module/azurerm.sql/get-azurermsqldeleteddatabasebackup) | <span data-ttu-id="cb124-126">Obtém um banco de dados excluído que você pode restaurar.</span><span class="sxs-lookup"><span data-stu-id="cb124-126">Gets a deleted database that you can restore.</span></span> |
| [<span data-ttu-id="cb124-127">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="cb124-127">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="cb124-128">Exclui um grupo de recursos, incluindo todos os recursos aninhados.</span><span class="sxs-lookup"><span data-stu-id="cb124-128">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="cb124-129">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="cb124-129">Next steps</span></span>

<span data-ttu-id="cb124-130">Para obter mais informações sobre hello Azure PowerShell, consulte [documentação do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="cb124-130">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="cb124-131">Exemplos de script do PowerShell do banco de dados SQL adicionais podem ser encontrados no hello [scripts de banco de dados do SQL Azure PowerShell](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="cb124-131">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
