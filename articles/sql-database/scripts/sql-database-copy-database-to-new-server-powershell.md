---
title: "servidor de banco de dados novo aaaPowerShell Azure de cópia de exemplo SQL | Microsoft Docs"
description: PowerShell exemplo script toocopy um servidor novo de tooa de banco de dados SQL do Azure
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
ms.openlocfilehash: c08f993bd75913481b1d534857ac057263e1d02b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toocopy-a-sql-database-tooa-new-server"></a><span data-ttu-id="519c2-103">Use o PowerShell toocopy um servidor novo do banco de dados tooa SQL</span><span class="sxs-lookup"><span data-stu-id="519c2-103">Use PowerShell toocopy a SQL database tooa new server</span></span>

<span data-ttu-id="519c2-104">Este exemplo de script do PowerShell cria uma cópia de um banco de dados existente em um novo servidor.</span><span class="sxs-lookup"><span data-stu-id="519c2-104">This PowerShell script example creates a copy of an existing database in a new server.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="copy-a-database-tooa-new-server"></a><span data-ttu-id="519c2-105">Copie um novo servidor de banco de dados tooa</span><span class="sxs-lookup"><span data-stu-id="519c2-105">Copy a database tooa new server</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/copy-database-to-new-server/copy-database-to-new-server.ps1?highlight=18-21 "Copy database toonew server")]

## <a name="clean-up-deployment"></a><span data-ttu-id="519c2-106">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="519c2-106">Clean up deployment</span></span>

<span data-ttu-id="519c2-107">Após a execução do exemplo de script hello, Olá comando a seguir pode ser usado tooremove grupo de recursos de saudação e todos os recursos associados a ele.</span><span class="sxs-lookup"><span data-stu-id="519c2-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="519c2-108">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="519c2-108">Script explanation</span></span>

<span data-ttu-id="519c2-109">Esse script usa Olá comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="519c2-109">This script uses hello following commands.</span></span> <span data-ttu-id="519c2-110">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="519c2-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="519c2-111">Command</span><span class="sxs-lookup"><span data-stu-id="519c2-111">Command</span></span> | <span data-ttu-id="519c2-112">Observações</span><span class="sxs-lookup"><span data-stu-id="519c2-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="519c2-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="519c2-113">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="519c2-114">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="519c2-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="519c2-115">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="519c2-115">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="519c2-116">Cria um servidor lógico que hospeda um banco de dados ou pool elástico.</span><span class="sxs-lookup"><span data-stu-id="519c2-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="519c2-117">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="519c2-117">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="519c2-118">Cria um banco de dados em um servidor lógico como um banco de dados individual ou em pool.</span><span class="sxs-lookup"><span data-stu-id="519c2-118">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="519c2-119">New-AzureRmSqlDatabaseCopy</span><span class="sxs-lookup"><span data-stu-id="519c2-119">New-AzureRmSqlDatabaseCopy</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabasecopy) | <span data-ttu-id="519c2-120">Cria uma cópia de um banco de dados que usa instantâneo Olá no hello hora atual.</span><span class="sxs-lookup"><span data-stu-id="519c2-120">Creates a copy of a database that uses hello snapshot at hello current time.</span></span> |
| [<span data-ttu-id="519c2-121">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="519c2-121">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="519c2-122">Exclui um grupo de recursos, incluindo todos os recursos aninhados.</span><span class="sxs-lookup"><span data-stu-id="519c2-122">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="519c2-123">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="519c2-123">Next steps</span></span>

<span data-ttu-id="519c2-124">Para obter mais informações sobre hello Azure PowerShell, consulte [documentação do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="519c2-124">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="519c2-125">Exemplos de script do PowerShell do banco de dados SQL adicionais podem ser encontrados no hello [scripts de banco de dados do SQL Azure PowerShell](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="519c2-125">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
