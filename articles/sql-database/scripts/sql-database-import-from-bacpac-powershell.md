---
title: Exemplo do PowerShell para importar um arquivo bacpac do Banco de Dados SQL do Azure | Microsoft Docs
description: Script de exemplo do Azure PowerShell para importar um bloco de bacpac para um banco de dados SQL
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
ms.openlocfilehash: 20e1d4c195314d6e828e1dac6afae8be11805b42
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="use-powershell-to-import-a-bacpac-file-into-an-azure-sql-database"></a><span data-ttu-id="41102-103">Use o PowerShell para importar um arquivo bacpac para um banco de dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="41102-103">Use PowerShell to import a bacpac file into an Azure SQL database</span></span>

<span data-ttu-id="41102-104">Este exemplo de script do PowerShell importa um banco de dados de um arquivo **bacpac** para um banco de dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="41102-104">This PowerShell script example imports a database from a **bacpac** file into an Azure SQL database.</span></span>  

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="41102-105">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="41102-105">Sample script</span></span>

<span data-ttu-id="41102-106">[!code-powershell[principal](../../../powershell_scripts/sql-database/import-from-bacpac/import-from-bacpac.ps1?highlight=18-19 "Criar Banco de Dados SQL")]</span><span class="sxs-lookup"><span data-stu-id="41102-106">[!code-powershell[main](../../../powershell_scripts/sql-database/import-from-bacpac/import-from-bacpac.ps1?highlight=18-19 "Create SQL Database")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="41102-107">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="41102-107">Clean up deployment</span></span>

<span data-ttu-id="41102-108">Após executar o exemplo de script, o comando a seguir pode ser usado para remover o grupo de recursos e todos os recursos associados a ele.</span><span class="sxs-lookup"><span data-stu-id="41102-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="41102-109">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="41102-109">Script explanation</span></span>

<span data-ttu-id="41102-110">Este script usa os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="41102-110">This script uses the following commands.</span></span> <span data-ttu-id="41102-111">Cada comando na tabela redireciona para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="41102-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="41102-112">Command</span><span class="sxs-lookup"><span data-stu-id="41102-112">Command</span></span> | <span data-ttu-id="41102-113">Observações</span><span class="sxs-lookup"><span data-stu-id="41102-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="41102-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="41102-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="41102-115">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="41102-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="41102-116">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="41102-116">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="41102-117">Cria um servidor lógico que hospeda o Banco de Dados SQL.</span><span class="sxs-lookup"><span data-stu-id="41102-117">Creates a logical server that hosts the SQL Database.</span></span> |
| [<span data-ttu-id="41102-118">New-AzureRmSqlServerFirewallRule</span><span class="sxs-lookup"><span data-stu-id="41102-118">New-AzureRmSqlServerFirewallRule</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule) | <span data-ttu-id="41102-119">Cria uma regra de firewall para permitir o acesso a todos os bancos de dados SQL no servidor do intervalo de endereços IP inserido.</span><span class="sxs-lookup"><span data-stu-id="41102-119">Creates a firewall rule to allow access to all SQL Databases on the server from the entered IP address range.</span></span> |
| [<span data-ttu-id="41102-120">New-AzureRmSqlDatabaseImport</span><span class="sxs-lookup"><span data-stu-id="41102-120">New-AzureRmSqlDatabaseImport</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabaseimport) | <span data-ttu-id="41102-121">Importa um arquivo .bacpac e cria um novo banco de dados no servidor.</span><span class="sxs-lookup"><span data-stu-id="41102-121">Imports a .bacpac file and create a new database on the server.</span></span> |
| [<span data-ttu-id="41102-122">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="41102-122">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="41102-123">Exclui um grupo de recursos, incluindo todos os recursos aninhados.</span><span class="sxs-lookup"><span data-stu-id="41102-123">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="41102-124">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="41102-124">Next steps</span></span>

<span data-ttu-id="41102-125">Para obter mais informações sobre o Azure PowerShell, confira [Documentação do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="41102-125">For more information on the Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="41102-126">Os exemplos de script do PowerShell do Banco de Dados SQL adicionais podem ser encontrados nos [scripts do PowerShell do Banco de Dados SQL do Azure](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="41102-126">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
