---
title: "aaaAzure PowerShell Script-criar uma política de failover do banco de dados do Azure Cosmos | Microsoft Docs"
description: "Exemplo de script do Azure PowerShell – criar uma política de failover do BD Cosmos do Azure"
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
ms.openlocfilehash: 750127385164cd16837b6e29c506d2b44146a629
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-cosmos-db-failover-policy-for-high-availability-using-powershell"></a><span data-ttu-id="4bb56-103">Crie uma política de failover do BD Cosmos do Azure para alta disponibilidade usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="4bb56-103">Create an Azure Cosmos DB failover policy for high availability using PowerShell</span></span>

<span data-ttu-id="4bb56-104">Este exemplo de script do PowerShell cria uma política de failover para alta disponibilidade para o BD Cosmos do Azure.</span><span class="sxs-lookup"><span data-stu-id="4bb56-104">This sample PowerShell script creates a failover policy for high availability for Azure Cosmos DB.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="4bb56-105">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="4bb56-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/cosmosdb/modify-failover-priority/modify-failover-priority.ps1?highlight=36-39,42-47 "Create an Azure Cosmos DB DocumentDB API account")]

## <a name="clean-up-deployment"></a><span data-ttu-id="4bb56-106">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="4bb56-106">Clean up deployment</span></span>

<span data-ttu-id="4bb56-107">Após a execução do exemplo de script hello, Olá comando a seguir pode ser usado tooremove grupo de recursos de saudação e todos os recursos associados a ele.</span><span class="sxs-lookup"><span data-stu-id="4bb56-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="4bb56-108">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="4bb56-108">Script explanation</span></span>

<span data-ttu-id="4bb56-109">Esse script usa Olá comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="4bb56-109">This script uses hello following commands.</span></span> <span data-ttu-id="4bb56-110">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="4bb56-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="4bb56-111">Command</span><span class="sxs-lookup"><span data-stu-id="4bb56-111">Command</span></span> | <span data-ttu-id="4bb56-112">Observações</span><span class="sxs-lookup"><span data-stu-id="4bb56-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="4bb56-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="4bb56-113">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/new-azurermresourcegroup) | <span data-ttu-id="4bb56-114">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="4bb56-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="4bb56-115">New-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="4bb56-115">New-AzureRmResource</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresource?view=azurermps-3.8.0) | <span data-ttu-id="4bb56-116">Cria um servidor lógico que hospeda um banco de dados ou pool elástico.</span><span class="sxs-lookup"><span data-stu-id="4bb56-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="4bb56-117">Invoke-AzureRmResourceAction</span><span class="sxs-lookup"><span data-stu-id="4bb56-117">Invoke-AzureRmResourceAction</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/invoke-azurermresourceaction?view=azurermps-3.8.0) | <span data-ttu-id="4bb56-118">Invoca uma ação hello Azure CosmosDB conta.</span><span class="sxs-lookup"><span data-stu-id="4bb56-118">Invokes an action on hello Azure CosmosDB account.</span></span> |
| [<span data-ttu-id="4bb56-119">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="4bb56-119">Remove-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/remove-azurermresourcegroup) | <span data-ttu-id="4bb56-120">Exclui um grupo de recursos, incluindo todos os recursos aninhados.</span><span class="sxs-lookup"><span data-stu-id="4bb56-120">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="4bb56-121">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4bb56-121">Next steps</span></span>

<span data-ttu-id="4bb56-122">Para obter mais informações sobre hello Azure PowerShell, consulte [documentação do Azure PowerShell](https://docs.microsoft.com/powershell/).</span><span class="sxs-lookup"><span data-stu-id="4bb56-122">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span></span>

<span data-ttu-id="4bb56-123">Exemplos de script do PowerShell do Azure Cosmos DB adicionais podem ser encontrados no hello [scripts do PowerShell do Azure Cosmos DB](../powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="4bb56-123">Additional Azure Cosmos DB PowerShell script samples can be found in hello [Azure Cosmos DB PowerShell scripts](../powershell-samples.md).</span></span>
