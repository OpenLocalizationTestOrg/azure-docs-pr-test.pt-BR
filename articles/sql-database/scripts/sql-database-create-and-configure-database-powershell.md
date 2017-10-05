---
title: Exemplo do PowerShell para criar um banco de dados SQL do Azure | Microsoft Docs
description: Script de exemplo do Azure PowerShell para criar um banco de dados SQL do Azure
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: 1b6809007e6717b7f8847452b2fa5b38d4ab5ccc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="use-powershell-to-create-a-single-azure-sql-database-and-configure-a-firewall-rule"></a><span data-ttu-id="01262-103">Use o PowerShell para criar um banco de dados SQL do Azure individual e configurar uma regra de firewall</span><span class="sxs-lookup"><span data-stu-id="01262-103">Use PowerShell to create a single Azure SQL database and configure a firewall rule</span></span>

<span data-ttu-id="01262-104">Este exemplo de script do PowerShell cria um banco de dados SQL do Azure e configura uma regra de firewall no nível do servidor.</span><span class="sxs-lookup"><span data-stu-id="01262-104">This PowerShell script example creates an Azure SQL database and configures a server-level firewall rule.</span></span> <span data-ttu-id="01262-105">Depois que o script tiver sido executado com êxito, o Banco de Dados SQL poderá ser acessado de todos os serviços do Azure e o endereço IP configurado.</span><span class="sxs-lookup"><span data-stu-id="01262-105">Once the script has been successfully run, the SQL Database can be accessed from all Azure services and the configured IP address.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="01262-106">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="01262-106">Sample script</span></span>

<span data-ttu-id="01262-107">[!code-powershell[principal](../../../powershell_scripts/sql-database/create-and-configure-database/create-and-configure-database.ps1?highlight=13-14 "Criar Banco de Dados SQL")]</span><span class="sxs-lookup"><span data-stu-id="01262-107">[!code-powershell[main](../../../powershell_scripts/sql-database/create-and-configure-database/create-and-configure-database.ps1?highlight=13-14 "Create SQL Database")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="01262-108">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="01262-108">Clean up deployment</span></span>

<span data-ttu-id="01262-109">Após executar o exemplo de script, o comando a seguir pode ser usado para remover o grupo de recursos e todos os recursos associados a ele.</span><span class="sxs-lookup"><span data-stu-id="01262-109">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="01262-110">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="01262-110">Script explanation</span></span>

<span data-ttu-id="01262-111">Este script usa os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="01262-111">This script uses the following commands.</span></span> <span data-ttu-id="01262-112">Cada comando na tabela redireciona para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="01262-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="01262-113">Command</span><span class="sxs-lookup"><span data-stu-id="01262-113">Command</span></span> | <span data-ttu-id="01262-114">Observações</span><span class="sxs-lookup"><span data-stu-id="01262-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="01262-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="01262-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="01262-116">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="01262-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="01262-117">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="01262-117">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="01262-118">Cria um servidor lógico que hospeda um banco de dados ou pool elástico.</span><span class="sxs-lookup"><span data-stu-id="01262-118">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="01262-119">New-AzureRmSqlServerFirewallRule</span><span class="sxs-lookup"><span data-stu-id="01262-119">New-AzureRmSqlServerFirewallRule</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule) | <span data-ttu-id="01262-120">Cria uma regra de firewall para permitir o acesso a todos os bancos de dados SQL no servidor do intervalo de endereços IP inserido.</span><span class="sxs-lookup"><span data-stu-id="01262-120">Creates a firewall rule to allow access to all SQL Databases on the server from the entered IP address range.</span></span> |
| [<span data-ttu-id="01262-121">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="01262-121">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="01262-122">Cria um banco de dados em um servidor lógico como um banco de dados individual ou em pool.</span><span class="sxs-lookup"><span data-stu-id="01262-122">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="01262-123">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="01262-123">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="01262-124">Exclui um grupo de recursos, incluindo todos os recursos aninhados.</span><span class="sxs-lookup"><span data-stu-id="01262-124">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="01262-125">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="01262-125">Next steps</span></span>

<span data-ttu-id="01262-126">Para obter mais informações sobre o Azure PowerShell, confira [Documentação do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="01262-126">For more information on the Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="01262-127">Os exemplos de script do PowerShell do Banco de Dados SQL adicionais podem ser encontrados nos [scripts do PowerShell do Banco de Dados SQL do Azure](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="01262-127">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>



