---
title: aaaPowerShell exemplo-criar um banco de dados SQL do Azure | Microsoft Docs
description: Azure PowerShell exemplo script toocreate um banco de dados do SQL Azure
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
ms.openlocfilehash: ae57b2018f4a550bf2c6da688d6e49bdadf3d3ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toocreate-a-single-azure-sql-database-and-configure-a-firewall-rule"></a><span data-ttu-id="59ad1-103">Use o PowerShell toocreate um único banco de dados do SQL Azure e configurar uma regra de firewall</span><span class="sxs-lookup"><span data-stu-id="59ad1-103">Use PowerShell toocreate a single Azure SQL database and configure a firewall rule</span></span>

<span data-ttu-id="59ad1-104">Este exemplo de script do PowerShell cria um banco de dados SQL do Azure e configura uma regra de firewall no nível do servidor.</span><span class="sxs-lookup"><span data-stu-id="59ad1-104">This PowerShell script example creates an Azure SQL database and configures a server-level firewall rule.</span></span> <span data-ttu-id="59ad1-105">Depois que o script hello foi executado com êxito, Olá que banco de dados SQL podem ser acessado de todos os serviços do Azure e hello endereço IP configurado.</span><span class="sxs-lookup"><span data-stu-id="59ad1-105">Once hello script has been successfully run, hello SQL Database can be accessed from all Azure services and hello configured IP address.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="59ad1-106">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="59ad1-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/create-and-configure-database/create-and-configure-database.ps1?highlight=13-14 "Create SQL Database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="59ad1-107">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="59ad1-107">Clean up deployment</span></span>

<span data-ttu-id="59ad1-108">Após a execução do exemplo de script hello, Olá comando a seguir pode ser usado tooremove grupo de recursos de saudação e todos os recursos associados a ele.</span><span class="sxs-lookup"><span data-stu-id="59ad1-108">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="59ad1-109">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="59ad1-109">Script explanation</span></span>

<span data-ttu-id="59ad1-110">Esse script usa Olá comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="59ad1-110">This script uses hello following commands.</span></span> <span data-ttu-id="59ad1-111">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="59ad1-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="59ad1-112">Command</span><span class="sxs-lookup"><span data-stu-id="59ad1-112">Command</span></span> | <span data-ttu-id="59ad1-113">Observações</span><span class="sxs-lookup"><span data-stu-id="59ad1-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="59ad1-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="59ad1-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="59ad1-115">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="59ad1-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="59ad1-116">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="59ad1-116">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="59ad1-117">Cria um servidor lógico que hospeda um banco de dados ou pool elástico.</span><span class="sxs-lookup"><span data-stu-id="59ad1-117">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="59ad1-118">New-AzureRmSqlServerFirewallRule</span><span class="sxs-lookup"><span data-stu-id="59ad1-118">New-AzureRmSqlServerFirewallRule</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserverfirewallrule) | <span data-ttu-id="59ad1-119">Cria um firewall regra tooallow acesso tooall bancos de dados SQL no servidor de saudação do intervalo de endereços IP hello inserido.</span><span class="sxs-lookup"><span data-stu-id="59ad1-119">Creates a firewall rule tooallow access tooall SQL Databases on hello server from hello entered IP address range.</span></span> |
| [<span data-ttu-id="59ad1-120">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="59ad1-120">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="59ad1-121">Cria um banco de dados em um servidor lógico como um banco de dados individual ou em pool.</span><span class="sxs-lookup"><span data-stu-id="59ad1-121">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="59ad1-122">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="59ad1-122">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="59ad1-123">Exclui um grupo de recursos, incluindo todos os recursos aninhados.</span><span class="sxs-lookup"><span data-stu-id="59ad1-123">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="59ad1-124">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="59ad1-124">Next steps</span></span>

<span data-ttu-id="59ad1-125">Para obter mais informações sobre hello Azure PowerShell, consulte [documentação do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="59ad1-125">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="59ad1-126">Exemplos de script do PowerShell do banco de dados SQL adicionais podem ser encontrados no hello [scripts de banco de dados do SQL Azure PowerShell](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="59ad1-126">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>



