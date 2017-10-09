---
title: "detecção de ameaças auditoria exemplo aaaPowerShell Azure banco de dados SQL | Microsoft Docs"
description: "Azure PowerShell exemplo script tooconfigure auditoria & ameaça detecção em um banco de dados do SQL Azure"
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,security
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: 97e057ac6efe5e730404ae796bc01e7e5c70df35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-tooconfigure-sql-database-auditing-and-threat-detection"></a><span data-ttu-id="b4e24-103">Use o PowerShell tooconfigure detecção de ameaças e auditoria do banco de dados SQL</span><span class="sxs-lookup"><span data-stu-id="b4e24-103">Use PowerShell tooconfigure SQL Database auditing and threat detection</span></span>

<span data-ttu-id="b4e24-104">Este exemplo de script do PowerShell configura a detecção de ameaças e auditoria do Banco de Dados SQL.</span><span class="sxs-lookup"><span data-stu-id="b4e24-104">This PowerShell script example configures SQL Database auditing and threat detection.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="b4e24-105">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="b4e24-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/database-auditing-and-threat-detection/database-auditing-and-threat-detection.ps1?highlight=13-14 "Configure auditing and threat detection")]

## <a name="clean-up-deployment"></a><span data-ttu-id="b4e24-106">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="b4e24-106">Clean up deployment</span></span>

<span data-ttu-id="b4e24-107">Após a execução do exemplo de script hello, Olá comando a seguir pode ser usado tooremove grupo de recursos de saudação e todos os recursos associados a ele.</span><span class="sxs-lookup"><span data-stu-id="b4e24-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="b4e24-108">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="b4e24-108">Script explanation</span></span>

<span data-ttu-id="b4e24-109">Esse script usa Olá comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="b4e24-109">This script uses hello following commands.</span></span> <span data-ttu-id="b4e24-110">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="b4e24-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="b4e24-111">Command</span><span class="sxs-lookup"><span data-stu-id="b4e24-111">Command</span></span> | <span data-ttu-id="b4e24-112">Observações</span><span class="sxs-lookup"><span data-stu-id="b4e24-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="b4e24-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="b4e24-113">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="b4e24-114">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="b4e24-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="b4e24-115">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="b4e24-115">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="b4e24-116">Cria um servidor lógico que hospeda um banco de dados ou pool elástico.</span><span class="sxs-lookup"><span data-stu-id="b4e24-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="b4e24-117">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="b4e24-117">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="b4e24-118">Cria um banco de dados em um servidor lógico como um banco de dados individual ou em pool.</span><span class="sxs-lookup"><span data-stu-id="b4e24-118">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="b4e24-119">New-AzureRmStorageAccount</span><span class="sxs-lookup"><span data-stu-id="b4e24-119">New-AzureRmStorageAccount</span></span>](/powershell/module/azurerm.storage/new-azurermstorageaccount) | <span data-ttu-id="b4e24-120">Cria uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="b4e24-120">Creates a Storage account.</span></span> |
| [<span data-ttu-id="b4e24-121">Set-AzureRmSqlDatabaseAuditingPolicy</span><span class="sxs-lookup"><span data-stu-id="b4e24-121">Set-AzureRmSqlDatabaseAuditingPolicy</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabaseauditingpolicy) | <span data-ttu-id="b4e24-122">Define a política de auditoria de saudação para um banco de dados.</span><span class="sxs-lookup"><span data-stu-id="b4e24-122">Sets hello auditing policy for a database.</span></span> |
| [<span data-ttu-id="b4e24-123">Set-AzureRmSqlDatabaseThreatDetectionPolicy</span><span class="sxs-lookup"><span data-stu-id="b4e24-123">Set-AzureRmSqlDatabaseThreatDetectionPolicy</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabasethreatdetectionpolicy) | <span data-ttu-id="b4e24-124">Define uma política de detecção de ameaças em um banco de dados.</span><span class="sxs-lookup"><span data-stu-id="b4e24-124">Sets a threat detection policy on a database.</span></span> |
| [<span data-ttu-id="b4e24-125">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="b4e24-125">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="b4e24-126">Exclui um grupo de recursos, incluindo todos os recursos aninhados.</span><span class="sxs-lookup"><span data-stu-id="b4e24-126">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="b4e24-127">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b4e24-127">Next steps</span></span>

<span data-ttu-id="b4e24-128">Para obter mais informações sobre hello Azure PowerShell, consulte [documentação do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b4e24-128">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="b4e24-129">Exemplos de script do PowerShell do banco de dados SQL adicionais podem ser encontrados no hello [scripts de banco de dados do SQL Azure PowerShell](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="b4e24-129">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
