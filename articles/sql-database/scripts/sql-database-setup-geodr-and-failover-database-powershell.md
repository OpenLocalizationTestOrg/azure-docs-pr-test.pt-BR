---
title: "aaaPowerShell ativo de exemplo geo-replication-único banco de dados SQL do Azure | Microsoft Docs"
description: "Azure tooset do script de exemplo do PowerShell a replicação geográfica ativa para um único banco de dados do SQL Azure"
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
ms.openlocfilehash: 9ad424d313a5aa96e31b50a1a39c71fd346a7ae9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-tooconfigure-active-geo-replication-for-a-single-azure-sql-database"></a><span data-ttu-id="adfc9-103">Use o PowerShell tooconfigure a replicação geográfica ativa para um único banco de dados do SQL Azure</span><span class="sxs-lookup"><span data-stu-id="adfc9-103">Use PowerShell tooconfigure active geo-replication for a single Azure SQL database</span></span>

<span data-ttu-id="adfc9-104">Este exemplo de script do PowerShell configura a replicação geográfica ativa para um único banco de dados do SQL Azure e ele failover tooa a réplica secundária do banco de dados do SQL Azure hello.</span><span class="sxs-lookup"><span data-stu-id="adfc9-104">This PowerShell script example configures active geo-replication for a single Azure SQL database and fails it over tooa secondary replica of hello Azure SQL database.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-scripts"></a><span data-ttu-id="adfc9-105">Exemplos de scripts</span><span class="sxs-lookup"><span data-stu-id="adfc9-105">Sample scripts</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/setup-geodr-and-failover-database/setup-geodr-and-failover-database.ps1?highlight=17-20 "Set up active geo-replication for single database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="adfc9-106">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="adfc9-106">Clean up deployment</span></span>

<span data-ttu-id="adfc9-107">Após a execução do exemplo de script hello, Olá comando a seguir pode ser usado tooremove grupo de recursos de saudação e todos os recursos associados a ele.</span><span class="sxs-lookup"><span data-stu-id="adfc9-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myPrimaryResourceGroup"
Remove-AzureRmResourceGroup -ResourceGroupName "mySecondaryResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="adfc9-108">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="adfc9-108">Script explanation</span></span>

<span data-ttu-id="adfc9-109">Esse script usa Olá comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="adfc9-109">This script uses hello following commands.</span></span> <span data-ttu-id="adfc9-110">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="adfc9-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="adfc9-111">Command</span><span class="sxs-lookup"><span data-stu-id="adfc9-111">Command</span></span> | <span data-ttu-id="adfc9-112">Observações</span><span class="sxs-lookup"><span data-stu-id="adfc9-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="adfc9-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="adfc9-113">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="adfc9-114">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="adfc9-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="adfc9-115">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="adfc9-115">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="adfc9-116">Cria um servidor lógico que hospeda um banco de dados ou pool elástico.</span><span class="sxs-lookup"><span data-stu-id="adfc9-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="adfc9-117">New-AzureRmSqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="adfc9-117">New-AzureRmSqlElasticPool</span></span>](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) | <span data-ttu-id="adfc9-118">Cria um pool elástico dentro de um servidor lógico.</span><span class="sxs-lookup"><span data-stu-id="adfc9-118">Creates an elastic pool within a logical server.</span></span> |
| [<span data-ttu-id="adfc9-119">Set-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="adfc9-119">Set-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabase) | <span data-ttu-id="adfc9-120">Atualiza as propriedades do banco de dados ou move um banco de dados para dentro, para fora entre pools elásticos.</span><span class="sxs-lookup"><span data-stu-id="adfc9-120">Updates database properties or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="adfc9-121">New-AzureRmSqlDatabaseSecondary</span><span class="sxs-lookup"><span data-stu-id="adfc9-121">New-AzureRmSqlDatabaseSecondary</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabasesecondary)| <span data-ttu-id="adfc9-122">Cria um banco de dados secundário para um banco de dados existente e inicia a replicação de dados.</span><span class="sxs-lookup"><span data-stu-id="adfc9-122">Creates a secondary database for an existing database and starts data replication.</span></span> |
| [<span data-ttu-id="adfc9-123">Get-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="adfc9-123">Get-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/get-azurermsqldatabase)| <span data-ttu-id="adfc9-124">Obtém um ou mais bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="adfc9-124">Gets one or more databases.</span></span> |
| [<span data-ttu-id="adfc9-125">Set-AzureRmSqlDatabaseSecondary</span><span class="sxs-lookup"><span data-stu-id="adfc9-125">Set-AzureRmSqlDatabaseSecondary</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabasesecondary)| <span data-ttu-id="adfc9-126">Alterna um failover do banco de dados secundário toobe tooinitiate primário.</span><span class="sxs-lookup"><span data-stu-id="adfc9-126">Switches a secondary database toobe primary tooinitiate failover.</span></span>|
| [<span data-ttu-id="adfc9-127">Get-AzureRmSqlDatabaseReplicationLink</span><span class="sxs-lookup"><span data-stu-id="adfc9-127">Get-AzureRmSqlDatabaseReplicationLink</span></span>](/powershell/module/azurerm.sql/get-azurermsqldatabasereplicationlink) | <span data-ttu-id="adfc9-128">Obtém os links de replicação geográfica Olá entre um banco de dados do SQL Azure e um grupo de recursos ou do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="adfc9-128">Gets hello geo-replication links between an Azure SQL Database and a resource group or SQL Server.</span></span> |
| [<span data-ttu-id="adfc9-129">Remove-AzureRmSqlDatabaseSecondary</span><span class="sxs-lookup"><span data-stu-id="adfc9-129">Remove-AzureRmSqlDatabaseSecondary</span></span>](/powershell/module/azurerm.sql/remove-azurermsqldatabasesecondary) | <span data-ttu-id="adfc9-130">Encerra a replicação de dados entre um banco de dados SQL e Olá secundário banco de dados especificado.</span><span class="sxs-lookup"><span data-stu-id="adfc9-130">Terminates data replication between a SQL Database and hello specified secondary database.</span></span> |
| [<span data-ttu-id="adfc9-131">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="adfc9-131">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="adfc9-132">Exclui um grupo de recursos, incluindo todos os recursos aninhados.</span><span class="sxs-lookup"><span data-stu-id="adfc9-132">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="adfc9-133">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="adfc9-133">Next steps</span></span>

<span data-ttu-id="adfc9-134">Para obter mais informações sobre hello Azure PowerShell, consulte [documentação do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="adfc9-134">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="adfc9-135">Exemplos de script do PowerShell do banco de dados SQL adicionais podem ser encontrados no hello [scripts de banco de dados do SQL Azure PowerShell](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="adfc9-135">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
