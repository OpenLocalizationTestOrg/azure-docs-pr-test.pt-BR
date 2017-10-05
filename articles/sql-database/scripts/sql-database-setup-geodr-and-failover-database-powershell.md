---
title: "Exemplo do PowerShell para replicação geográfica ativa individual do Banco de Dados SQL do Azure | Microsoft Docs"
description: "Script de exemplo do Azure PowerShell para configurar uma replicação geográfica ativa para um banco de dados SQL individual do Azure"
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
ms.openlocfilehash: b25bc02acda7905cd4c08bbafee1d9b29907d332
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="use-powershell-to-configure-active-geo-replication-for-a-single-azure-sql-database"></a><span data-ttu-id="d12fb-103">Usar o PowerShell para configurar a replicação geográfica ativa para um banco de dados SQL individual do Azure</span><span class="sxs-lookup"><span data-stu-id="d12fb-103">Use PowerShell to configure active geo-replication for a single Azure SQL database</span></span>

<span data-ttu-id="d12fb-104">Este exemplo de script do PowerShell configura a replicação geográfica ativa para um banco de dados SQL individual do Azure e faz o failover para uma réplica secundária do banco de dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="d12fb-104">This PowerShell script example configures active geo-replication for a single Azure SQL database and fails it over to a secondary replica of the Azure SQL database.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-scripts"></a><span data-ttu-id="d12fb-105">Exemplos de scripts</span><span class="sxs-lookup"><span data-stu-id="d12fb-105">Sample scripts</span></span>

<span data-ttu-id="d12fb-106">[!code-powershell[main](../../../powershell_scripts/sql-database/setup-geodr-and-failover-database/setup-geodr-and-failover-database.ps1?highlight=17-20 "Configurar a replicação geográfica ativa para o banco de dados individual")]</span><span class="sxs-lookup"><span data-stu-id="d12fb-106">[!code-powershell[main](../../../powershell_scripts/sql-database/setup-geodr-and-failover-database/setup-geodr-and-failover-database.ps1?highlight=17-20 "Set up active geo-replication for single database")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="d12fb-107">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="d12fb-107">Clean up deployment</span></span>

<span data-ttu-id="d12fb-108">Após executar o exemplo de script, o comando a seguir pode ser usado para remover o grupo de recursos e todos os recursos associados a ele.</span><span class="sxs-lookup"><span data-stu-id="d12fb-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myPrimaryResourceGroup"
Remove-AzureRmResourceGroup -ResourceGroupName "mySecondaryResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="d12fb-109">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="d12fb-109">Script explanation</span></span>

<span data-ttu-id="d12fb-110">Este script usa os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="d12fb-110">This script uses the following commands.</span></span> <span data-ttu-id="d12fb-111">Cada comando na tabela redireciona para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="d12fb-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="d12fb-112">Command</span><span class="sxs-lookup"><span data-stu-id="d12fb-112">Command</span></span> | <span data-ttu-id="d12fb-113">Observações</span><span class="sxs-lookup"><span data-stu-id="d12fb-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="d12fb-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="d12fb-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="d12fb-115">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="d12fb-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="d12fb-116">New-AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="d12fb-116">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="d12fb-117">Cria um servidor lógico que hospeda um banco de dados ou pool elástico.</span><span class="sxs-lookup"><span data-stu-id="d12fb-117">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="d12fb-118">New-AzureRmSqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="d12fb-118">New-AzureRmSqlElasticPool</span></span>](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) | <span data-ttu-id="d12fb-119">Cria um pool elástico dentro de um servidor lógico.</span><span class="sxs-lookup"><span data-stu-id="d12fb-119">Creates an elastic pool within a logical server.</span></span> |
| [<span data-ttu-id="d12fb-120">Set-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="d12fb-120">Set-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabase) | <span data-ttu-id="d12fb-121">Atualiza as propriedades do banco de dados ou move um banco de dados para dentro, para fora entre pools elásticos.</span><span class="sxs-lookup"><span data-stu-id="d12fb-121">Updates database properties or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="d12fb-122">New-AzureRmSqlDatabaseSecondary</span><span class="sxs-lookup"><span data-stu-id="d12fb-122">New-AzureRmSqlDatabaseSecondary</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabasesecondary)| <span data-ttu-id="d12fb-123">Cria um banco de dados secundário para um banco de dados existente e inicia a replicação de dados.</span><span class="sxs-lookup"><span data-stu-id="d12fb-123">Creates a secondary database for an existing database and starts data replication.</span></span> |
| [<span data-ttu-id="d12fb-124">Get-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="d12fb-124">Get-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/get-azurermsqldatabase)| <span data-ttu-id="d12fb-125">Obtém um ou mais bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="d12fb-125">Gets one or more databases.</span></span> |
| [<span data-ttu-id="d12fb-126">Set-AzureRmSqlDatabaseSecondary</span><span class="sxs-lookup"><span data-stu-id="d12fb-126">Set-AzureRmSqlDatabaseSecondary</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabasesecondary)| <span data-ttu-id="d12fb-127">Alterna um banco de dados secundário para primário a fim de iniciar o failover.</span><span class="sxs-lookup"><span data-stu-id="d12fb-127">Switches a secondary database to be primary to initiate failover.</span></span>|
| [<span data-ttu-id="d12fb-128">Get-AzureRmSqlDatabaseReplicationLink</span><span class="sxs-lookup"><span data-stu-id="d12fb-128">Get-AzureRmSqlDatabaseReplicationLink</span></span>](/powershell/module/azurerm.sql/get-azurermsqldatabasereplicationlink) | <span data-ttu-id="d12fb-129">Obtém os links de replicação geográfica entre um Banco de Dados SQL do Azure e um grupo de recursos ou do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="d12fb-129">Gets the geo-replication links between an Azure SQL Database and a resource group or SQL Server.</span></span> |
| [<span data-ttu-id="d12fb-130">Remove-AzureRmSqlDatabaseSecondary</span><span class="sxs-lookup"><span data-stu-id="d12fb-130">Remove-AzureRmSqlDatabaseSecondary</span></span>](/powershell/module/azurerm.sql/remove-azurermsqldatabasesecondary) | <span data-ttu-id="d12fb-131">Encerra uma replicação de dados entre um Banco de Dados SQL e o banco de dados secundário especificado.</span><span class="sxs-lookup"><span data-stu-id="d12fb-131">Terminates data replication between a SQL Database and the specified secondary database.</span></span> |
| [<span data-ttu-id="d12fb-132">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="d12fb-132">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="d12fb-133">Exclui um grupo de recursos, incluindo todos os recursos aninhados.</span><span class="sxs-lookup"><span data-stu-id="d12fb-133">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="d12fb-134">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d12fb-134">Next steps</span></span>

<span data-ttu-id="d12fb-135">Para obter mais informações sobre o Azure PowerShell, confira [Documentação do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d12fb-135">For more information on the Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="d12fb-136">Os exemplos de script do PowerShell do Banco de Dados SQL adicionais podem ser encontrados nos [scripts do PowerShell do Banco de Dados SQL do Azure](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="d12fb-136">Additional SQL Database PowerShell script samples can be found in the [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
