---
title: "a replicação para o banco de dados do Azure Cosmos aaaAzure PowerShell Script-Multiregion | Microsoft Docs"
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
ms.openlocfilehash: 8e3e79f086f46fc037d52589eb8bcf4557214566
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-an-azure-cosmos-db-database-account-in-multiple-regions-and-configure-failover-priorities-using-powershell"></a><span data-ttu-id="1e090-103">Replique uma conta do BD Cosmos do Azure em várias regiões e configure as prioridades de failover usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="1e090-103">Replicate an Azure Cosmos DB database account in multiple regions and configure failover priorities using PowerShell</span></span>

<span data-ttu-id="1e090-104">Este exemplo replica qualquer tipo de conta do BD Cosmos do Azure em várias regiões e configura as prioridades de failover usando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1e090-104">This sample replicates any kind of Azure Cosmos DB database account in multiple regions and configures failover priorities using PowerShell.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="1e090-105">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="1e090-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/cosmosdb/replicate-database-multiple-regions/replicate-database-multiple-regions.ps1?highlight=37-44,47-48,51-55 "Replicate an Azure Cosmos DB account across multiple regions")]

## <a name="clean-up-deployment"></a><span data-ttu-id="1e090-106">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="1e090-106">Clean up deployment</span></span>

<span data-ttu-id="1e090-107">Após a execução do exemplo de script hello, Olá comando a seguir pode ser usado tooremove grupo de recursos de saudação e todos os recursos associados a ele.</span><span class="sxs-lookup"><span data-stu-id="1e090-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="1e090-108">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="1e090-108">Script explanation</span></span>

<span data-ttu-id="1e090-109">Esse script usa Olá comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="1e090-109">This script uses hello following commands.</span></span> <span data-ttu-id="1e090-110">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="1e090-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="1e090-111">Command</span><span class="sxs-lookup"><span data-stu-id="1e090-111">Command</span></span> | <span data-ttu-id="1e090-112">Observações</span><span class="sxs-lookup"><span data-stu-id="1e090-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="1e090-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="1e090-113">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/new-azurermresourcegroup) | <span data-ttu-id="1e090-114">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="1e090-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="1e090-115">New-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="1e090-115">New-AzureRmResource</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresource?view=azurermps-3.8.0) | <span data-ttu-id="1e090-116">Cria um servidor lógico que hospeda um banco de dados ou pool elástico.</span><span class="sxs-lookup"><span data-stu-id="1e090-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="1e090-117">Set-AzureRMResource</span><span class="sxs-lookup"><span data-stu-id="1e090-117">Set-AzureRMResource</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/set-azurermresource?view=azurermps-3.8.0) | <span data-ttu-id="1e090-118">Modifica a conta de banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="1e090-118">Modifies hello database account.</span></span> |
| [<span data-ttu-id="1e090-119">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="1e090-119">Remove-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/remove-azurermresourcegroup) | <span data-ttu-id="1e090-120">Exclui um grupo de recursos, incluindo todos os recursos aninhados.</span><span class="sxs-lookup"><span data-stu-id="1e090-120">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="1e090-121">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1e090-121">Next steps</span></span>

<span data-ttu-id="1e090-122">Para obter mais informações sobre hello Azure PowerShell, consulte [documentação do Azure PowerShell](https://docs.microsoft.com/powershell/).</span><span class="sxs-lookup"><span data-stu-id="1e090-122">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span></span>

<span data-ttu-id="1e090-123">Exemplos de script do PowerShell do Azure Cosmos DB adicionais podem ser encontrados no hello [scripts do PowerShell do Azure Cosmos DB](../powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="1e090-123">Additional Azure Cosmos DB PowerShell script samples can be found in hello [Azure Cosmos DB PowerShell scripts](../powershell-samples.md).</span></span>
