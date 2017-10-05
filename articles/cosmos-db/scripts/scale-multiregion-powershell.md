---
title: "Script do Azure PowerShell – replicação em várias regiões para o BD Cosmos do Azure | Microsoft Docs"
description: "Exemplo de script do Azure PowerShell – replicação em várias regiões para o BD Cosmos do Azure"
services: cosmos-db
documentationcenter: cosmosdb
author: mimig1
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: cosmos-db
ms.custom: mvc
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: cosmosdb
ms.workload: database
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: 3a469ba43e6c601f5eb0e13d588cd0bd4a0f8683
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="replicate-an-azure-cosmos-db-database-account-in-multiple-regions-and-configure-failover-priorities-using-powershell"></a><span data-ttu-id="cdbb7-103">Replique uma conta do BD Cosmos do Azure em várias regiões e configure as prioridades de failover usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="cdbb7-103">Replicate an Azure Cosmos DB database account in multiple regions and configure failover priorities using PowerShell</span></span>

<span data-ttu-id="cdbb7-104">Este exemplo replica qualquer tipo de conta do BD Cosmos do Azure em várias regiões e configura as prioridades de failover usando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cdbb7-104">This sample replicates any kind of Azure Cosmos DB database account in multiple regions and configures failover priorities using PowerShell.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="cdbb7-105">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="cdbb7-105">Sample script</span></span>

<span data-ttu-id="cdbb7-106">[!code-powershell[principal](../../../powershell_scripts/cosmosdb/replicate-database-multiple-regions/replicate-database-multiple-regions.ps1?highlight=37-44,47-48,51-55 "Replicar uma conta do BD Cosmos do Azure em várias regiões")]</span><span class="sxs-lookup"><span data-stu-id="cdbb7-106">[!code-powershell[main](../../../powershell_scripts/cosmosdb/replicate-database-multiple-regions/replicate-database-multiple-regions.ps1?highlight=37-44,47-48,51-55 "Replicate an Azure Cosmos DB account across multiple regions")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="cdbb7-107">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="cdbb7-107">Clean up deployment</span></span>

<span data-ttu-id="cdbb7-108">Após executar o exemplo de script, o comando a seguir pode ser usado para remover o grupo de recursos e todos os recursos associados a ele.</span><span class="sxs-lookup"><span data-stu-id="cdbb7-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="cdbb7-109">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="cdbb7-109">Script explanation</span></span>

<span data-ttu-id="cdbb7-110">Este script usa os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="cdbb7-110">This script uses the following commands.</span></span> <span data-ttu-id="cdbb7-111">Cada comando na tabela redireciona para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="cdbb7-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="cdbb7-112">Command</span><span class="sxs-lookup"><span data-stu-id="cdbb7-112">Command</span></span> | <span data-ttu-id="cdbb7-113">Observações</span><span class="sxs-lookup"><span data-stu-id="cdbb7-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="cdbb7-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="cdbb7-114">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/new-azurermresourcegroup) | <span data-ttu-id="cdbb7-115">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="cdbb7-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="cdbb7-116">New-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="cdbb7-116">New-AzureRmResource</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresource?view=azurermps-3.8.0) | <span data-ttu-id="cdbb7-117">Cria um servidor lógico que hospeda um banco de dados ou pool elástico.</span><span class="sxs-lookup"><span data-stu-id="cdbb7-117">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="cdbb7-118">Set-AzureRMResource</span><span class="sxs-lookup"><span data-stu-id="cdbb7-118">Set-AzureRMResource</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/set-azurermresource?view=azurermps-3.8.0) | <span data-ttu-id="cdbb7-119">Modifica a conta do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="cdbb7-119">Modifies the database account.</span></span> |
| [<span data-ttu-id="cdbb7-120">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="cdbb7-120">Remove-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/remove-azurermresourcegroup) | <span data-ttu-id="cdbb7-121">Exclui um grupo de recursos, incluindo todos os recursos aninhados.</span><span class="sxs-lookup"><span data-stu-id="cdbb7-121">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="cdbb7-122">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="cdbb7-122">Next steps</span></span>

<span data-ttu-id="cdbb7-123">Para obter mais informações sobre o Azure PowerShell, confira [Documentação do Azure PowerShell](https://docs.microsoft.com/powershell/).</span><span class="sxs-lookup"><span data-stu-id="cdbb7-123">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span></span>

<span data-ttu-id="cdbb7-124">Exemplos adicionais de scripts do PowerShell do Banco de Dados Cosmos do Azure podem ser encontrados nos [Scripts do PowerShell do Banco de Dados Cosmos do Azure](../powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="cdbb7-124">Additional Azure Cosmos DB PowerShell script samples can be found in the [Azure Cosmos DB PowerShell scripts](../powershell-samples.md).</span></span>