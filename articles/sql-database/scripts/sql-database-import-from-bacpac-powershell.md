---
title: "banco de dados SQL do Azure do arquivo de exemplo de importação de bacpac de aaaPowerShell | Microsoft Docs"
description: Bloco de um bacpac de tooimport de script de exemplo do PowerShell do Azure em um banco de dados SQL
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
ms.openlocfilehash: b85fca1c7fd52037d74254980469f9f53906448e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-tooimport-a-bacpac-file-into-an-azure-sql-database"></a><span data-ttu-id="25131-103">Use o PowerShell tooimport um arquivo bacpac em um banco de dados do SQL Azure</span><span class="sxs-lookup"><span data-stu-id="25131-103">Use PowerShell tooimport a bacpac file into an Azure SQL database</span></span>

<span data-ttu-id="25131-104">Este exemplo de script do PowerShell importa um banco de dados de um arquivo **bacpac** para um banco de dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="25131-104">This PowerShell script example imports a database from a **bacpac** file into an Azure SQL database.</span></span>  

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="25131-105">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="25131-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/import-from-bacpac/import-from-bacpac.ps1?highlight=18-19 "Create SQL Database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="25131-106">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="25131-106">Clean up deployment</span></span>

<span data-ttu-id="25131-107">Após a execução do exemplo de script hello, Olá comando a seguir pode ser usado tooremove grupo de recursos de saudação e todos os recursos associados a ele.</span><span class="sxs-lookup"><span data-stu-id="25131-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="25131-108">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="25131-108">Script explanation</span></span>

<span data-ttu-id="25131-109">Esse script usa Olá comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="25131-109">This script uses hello following commands.</span></span> <span data-ttu-id="25131-110">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="25131-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="25131-111">Command</span><span class="sxs-lookup"><span data-stu-id="25131-111">Command</span></span> | <span data-ttu-id="25131-112">Observações</span><span class="sxs-lookup"><span data-stu-id="25131-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="25131-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="25131-113">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="25131-114">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="25131-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="25131-115">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="25131-115">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="25131-116">Cria um servidor lógico hosts Olá banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="25131-116">Creates a logical server that hosts hello SQL Database.</span></span> |
| [<span data-ttu-id="25131-117">New-AzureRmSqlServerFirewallRule</span><span class="sxs-lookup"><span data-stu-id="25131-117">New-AzureRmSqlServerFirewallRule</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule) | <span data-ttu-id="25131-118">Cria um firewall regra tooallow acesso tooall bancos de dados SQL no servidor de saudação do intervalo de endereços IP hello inserido.</span><span class="sxs-lookup"><span data-stu-id="25131-118">Creates a firewall rule tooallow access tooall SQL Databases on hello server from hello entered IP address range.</span></span> |
| [<span data-ttu-id="25131-119">New-AzureRmSqlDatabaseImport</span><span class="sxs-lookup"><span data-stu-id="25131-119">New-AzureRmSqlDatabaseImport</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabaseimport) | <span data-ttu-id="25131-120">Importa um. bacpac de arquivo e cria um novo banco de dados no servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="25131-120">Imports a .bacpac file and create a new database on hello server.</span></span> |
| [<span data-ttu-id="25131-121">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="25131-121">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="25131-122">Exclui um grupo de recursos, incluindo todos os recursos aninhados.</span><span class="sxs-lookup"><span data-stu-id="25131-122">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="25131-123">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="25131-123">Next steps</span></span>

<span data-ttu-id="25131-124">Para obter mais informações sobre hello Azure PowerShell, consulte [documentação do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="25131-124">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="25131-125">Exemplos de script do PowerShell do banco de dados SQL adicionais podem ser encontrados no hello [scripts de banco de dados do SQL Azure PowerShell](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="25131-125">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
