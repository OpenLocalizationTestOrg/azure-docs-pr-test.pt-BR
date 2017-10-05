---
title: "Exemplo do PowerShell para replicação geográfica ativa em pools do Banco de Dados SQL do Azure | Microsoft Docs"
description: "Script de exemplo do Azure PowerShell para configurar uma replicação geográfica ativa para um banco de dados SQL em pools do Azure"
services: sql-database
documentationcenter: sql-database
author: CarlRabeler
manager: jhubbard
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: business continuity
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 07/25/2017
ms.author: carlrab
ms.openlocfilehash: c1a495a8f9960ed60d8589dee9615e075f80c77b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="use-powershell-to-configure-active-geo-replication-for-a-pooled-azure-sql-database"></a><span data-ttu-id="c9a1e-103">Use o PowerShell para configurar a replicação geográfica ativa para um banco de dados SQL individual em pools do Azure</span><span class="sxs-lookup"><span data-stu-id="c9a1e-103">Use PowerShell to configure active geo-replication for a pooled Azure SQL database</span></span>

<span data-ttu-id="c9a1e-104">Este exemplo de script do PowerShell configura a replicação geográfica ativa para um banco de dados SQL do Azure em um pool elástico e faz o failover para uma réplica secundária do banco de dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="c9a1e-104">This PowerShell script example configures active geo-replication for an Azure SQL database in an elastic pool and fails it over to the secondary replica of the Azure SQL database.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-scripts"></a><span data-ttu-id="c9a1e-105">Exemplos de scripts</span><span class="sxs-lookup"><span data-stu-id="c9a1e-105">Sample scripts</span></span>

<span data-ttu-id="c9a1e-106">[!code-powershell[main](../../../powershell_scripts/sql-database/setup-geodr-and-failover-pool/setup-geodr-and-failover-pool.ps1?highlight=16-19 "Configurar a replicação geográfica ativa para o pool elástico")]</span><span class="sxs-lookup"><span data-stu-id="c9a1e-106">[!code-powershell[main](../../../powershell_scripts/sql-database/setup-geodr-and-failover-pool/setup-geodr-and-failover-pool.ps1?highlight=16-19 "Set up active geo-replication for elastic pool")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="c9a1e-107">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="c9a1e-107">Clean up deployment</span></span>

<span data-ttu-id="c9a1e-108">Após executar o exemplo de script, o comando a seguir pode ser usado para remover o grupo de recursos e todos os recursos associados a ele.</span><span class="sxs-lookup"><span data-stu-id="c9a1e-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myPrimaryResourceGroup"
Remove-AzureRmResourceGroup -ResourceGroupName "mySecondaryResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="c9a1e-109">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="c9a1e-109">Script explanation</span></span>

<span data-ttu-id="c9a1e-110">Este script usa os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="c9a1e-110">This script uses the following commands.</span></span> <span data-ttu-id="c9a1e-111">Cada comando na tabela redireciona para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="c9a1e-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="c9a1e-112">Command</span><span class="sxs-lookup"><span data-stu-id="c9a1e-112">Command</span></span> | <span data-ttu-id="c9a1e-113">Observações</span><span class="sxs-lookup"><span data-stu-id="c9a1e-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c9a1e-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="c9a1e-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="c9a1e-115">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="c9a1e-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="c9a1e-116">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="c9a1e-116">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="c9a1e-117">Cria um servidor lógico que hospeda um banco de dados ou pool elástico.</span><span class="sxs-lookup"><span data-stu-id="c9a1e-117">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="c9a1e-118">New-AzureRmSqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="c9a1e-118">New-AzureRmSqlElasticPool</span></span>](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) | <span data-ttu-id="c9a1e-119">Cria um pool elástico dentro de um servidor lógico.</span><span class="sxs-lookup"><span data-stu-id="c9a1e-119">Creates an elastic pool within a logical server.</span></span> |
| [<span data-ttu-id="c9a1e-120">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="c9a1e-120">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="c9a1e-121">Cria um banco de dados em um servidor lógico como um banco de dados individual ou em pool.</span><span class="sxs-lookup"><span data-stu-id="c9a1e-121">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="c9a1e-122">Set-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="c9a1e-122">Set-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabase) | <span data-ttu-id="c9a1e-123">Atualiza as propriedades do banco de dados ou move um banco de dados para dentro, para fora entre pools elásticos.</span><span class="sxs-lookup"><span data-stu-id="c9a1e-123">Updates database properties or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="c9a1e-124">New-AzureRmSqlDatabaseSecondary</span><span class="sxs-lookup"><span data-stu-id="c9a1e-124">New-AzureRmSqlDatabaseSecondary</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabasesecondary)| <span data-ttu-id="c9a1e-125">Cria um banco de dados secundário para um banco de dados existente e inicia a replicação de dados.</span><span class="sxs-lookup"><span data-stu-id="c9a1e-125">Creates a secondary database for an existing database and starts data replication.</span></span> |
| [<span data-ttu-id="c9a1e-126">Get-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="c9a1e-126">Get-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/get-azurermsqldatabase)| <span data-ttu-id="c9a1e-127">Obtém um ou mais bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="c9a1e-127">Gets one or more databases.</span></span> |
| [<span data-ttu-id="c9a1e-128">Set-AzureRmSqlDatabaseSecondary</span><span class="sxs-lookup"><span data-stu-id="c9a1e-128">Set-AzureRmSqlDatabaseSecondary</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabasesecondary)| <span data-ttu-id="c9a1e-129">Alterna um banco de dados secundário para primário a fim de iniciar o failover.</span><span class="sxs-lookup"><span data-stu-id="c9a1e-129">Switches a secondary database to be primary in order to initiate failover.</span></span>|
| [<span data-ttu-id="c9a1e-130">Get-AzureRmSqlDatabaseReplicationLink</span><span class="sxs-lookup"><span data-stu-id="c9a1e-130">Get-AzureRmSqlDatabaseReplicationLink</span></span>](/powershell/module/azurerm.sql/get-azurermsqldatabasereplicationlink) | <span data-ttu-id="c9a1e-131">Obtém os links de replicação geográfica entre um Banco de Dados SQL do Azure e um grupo de recursos ou do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="c9a1e-131">Gets the geo-replication links between an Azure SQL Database and a resource group or SQL Server.</span></span> |
| [<span data-ttu-id="c9a1e-132">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="c9a1e-132">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="c9a1e-133">Exclui um grupo de recursos, incluindo todos os recursos aninhados.</span><span class="sxs-lookup"><span data-stu-id="c9a1e-133">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="c9a1e-134">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c9a1e-134">Next steps</span></span>

<span data-ttu-id="c9a1e-135">Para obter mais informações sobre o Azure PowerShell, confira [Documentação do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c9a1e-135">For more information on the Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="c9a1e-136">Os exemplos de script do PowerShell do Banco de Dados SQL adicionais podem ser encontrados nos [scripts do PowerShell do Banco de Dados SQL do Azure](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="c9a1e-136">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
