---
title: "Exemplo do PowerShell para detecção de ameaças e auditoria do Banco de Dados SQL do Azure | Microsoft Docs"
description: "Script de exemplo do Azure PowerShell para configurar a detecção de ameaças e auditoria em um Banco de Dados SQL do Azure"
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
ms.openlocfilehash: e039d35474bff3b066a6605a97e04d4a81c365eb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="use-powershell-to-configure-sql-database-auditing-and-threat-detection"></a><span data-ttu-id="908aa-103">Use o PowerShell para configurar a detecção de ameaças e auditoria do Banco de Dados SQL</span><span class="sxs-lookup"><span data-stu-id="908aa-103">Use PowerShell to configure SQL Database auditing and threat detection</span></span>

<span data-ttu-id="908aa-104">Este exemplo de script do PowerShell configura a detecção de ameaças e auditoria do Banco de Dados SQL.</span><span class="sxs-lookup"><span data-stu-id="908aa-104">This PowerShell script example configures SQL Database auditing and threat detection.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="908aa-105">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="908aa-105">Sample script</span></span>

<span data-ttu-id="908aa-106">[!code-powershell[principal](../../../powershell_scripts/sql-database/database-auditing-and-threat-detection/database-auditing-and-threat-detection.ps1?highlight=13-14 "Configurar a auditoria e detecção de ameaças")]</span><span class="sxs-lookup"><span data-stu-id="908aa-106">[!code-powershell[main](../../../powershell_scripts/sql-database/database-auditing-and-threat-detection/database-auditing-and-threat-detection.ps1?highlight=13-14 "Configure auditing and threat detection")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="908aa-107">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="908aa-107">Clean up deployment</span></span>

<span data-ttu-id="908aa-108">Após executar o exemplo de script, o comando a seguir pode ser usado para remover o grupo de recursos e todos os recursos associados a ele.</span><span class="sxs-lookup"><span data-stu-id="908aa-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="908aa-109">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="908aa-109">Script explanation</span></span>

<span data-ttu-id="908aa-110">Este script usa os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="908aa-110">This script uses the following commands.</span></span> <span data-ttu-id="908aa-111">Cada comando na tabela redireciona para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="908aa-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="908aa-112">Command</span><span class="sxs-lookup"><span data-stu-id="908aa-112">Command</span></span> | <span data-ttu-id="908aa-113">Observações</span><span class="sxs-lookup"><span data-stu-id="908aa-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="908aa-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="908aa-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="908aa-115">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="908aa-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="908aa-116">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="908aa-116">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="908aa-117">Cria um servidor lógico que hospeda um banco de dados ou pool elástico.</span><span class="sxs-lookup"><span data-stu-id="908aa-117">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="908aa-118">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="908aa-118">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="908aa-119">Cria um banco de dados em um servidor lógico como um banco de dados individual ou em pool.</span><span class="sxs-lookup"><span data-stu-id="908aa-119">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="908aa-120">New-AzureRmStorageAccount</span><span class="sxs-lookup"><span data-stu-id="908aa-120">New-AzureRmStorageAccount</span></span>](/powershell/module/azurerm.storage/new-azurermstorageaccount) | <span data-ttu-id="908aa-121">Cria uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="908aa-121">Creates a Storage account.</span></span> |
| [<span data-ttu-id="908aa-122">Set-AzureRmSqlDatabaseAuditingPolicy</span><span class="sxs-lookup"><span data-stu-id="908aa-122">Set-AzureRmSqlDatabaseAuditingPolicy</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabaseauditingpolicy) | <span data-ttu-id="908aa-123">Define a política de auditoria para um banco de dados.</span><span class="sxs-lookup"><span data-stu-id="908aa-123">Sets the auditing policy for a database.</span></span> |
| [<span data-ttu-id="908aa-124">Set-AzureRmSqlDatabaseThreatDetectionPolicy</span><span class="sxs-lookup"><span data-stu-id="908aa-124">Set-AzureRmSqlDatabaseThreatDetectionPolicy</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabasethreatdetectionpolicy) | <span data-ttu-id="908aa-125">Define uma política de detecção de ameaças em um banco de dados.</span><span class="sxs-lookup"><span data-stu-id="908aa-125">Sets a threat detection policy on a database.</span></span> |
| [<span data-ttu-id="908aa-126">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="908aa-126">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="908aa-127">Exclui um grupo de recursos, incluindo todos os recursos aninhados.</span><span class="sxs-lookup"><span data-stu-id="908aa-127">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="908aa-128">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="908aa-128">Next steps</span></span>

<span data-ttu-id="908aa-129">Para obter mais informações sobre o Azure PowerShell, confira [Documentação do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="908aa-129">For more information on the Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="908aa-130">Os exemplos de script do PowerShell do Banco de Dados SQL adicionais podem ser encontrados nos [scripts do PowerShell do Banco de Dados SQL do Azure](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="908aa-130">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
