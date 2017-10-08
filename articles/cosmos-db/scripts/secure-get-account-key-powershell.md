---
title: chaves de aaaAzure conta Get de Script do PowerShell para cosmosdb | Microsoft Docs
description: "Exemplo de script do Azure PowerShell – obter chaves da conta para o Banco de Dados Cosmos"
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
ms.openlocfilehash: 9ccee3085dc4fa6507d43e4a220dd5fc32889a9b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-account-keys-for-azure-cosmos-db-using-powershell"></a><span data-ttu-id="9cf95-103">Obtenha chaves de conta para o BD Cosmos do Azure usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="9cf95-103">Get account keys for Azure Cosmos DB using PowerShell</span></span>

<span data-ttu-id="9cf95-104">Este exemplo obtém chaves de conta para qualquer tipo de conta do BD Cosmos do Azure.</span><span class="sxs-lookup"><span data-stu-id="9cf95-104">This sample gets account keys for any kind of Azure Cosmos DB account.</span></span>  

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="9cf95-105">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="9cf95-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/cosmosdb/get-account-keys/get-account-keys.ps1?highlight=36-40 "Get hello keys for an Azure Cosmos DB account")]

## <a name="clean-up-deployment"></a><span data-ttu-id="9cf95-106">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="9cf95-106">Clean up deployment</span></span>

<span data-ttu-id="9cf95-107">Após a execução do exemplo de script hello, Olá comando a seguir pode ser usado tooremove grupo de recursos de saudação e todos os recursos associados a ele.</span><span class="sxs-lookup"><span data-stu-id="9cf95-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="9cf95-108">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="9cf95-108">Script explanation</span></span>

<span data-ttu-id="9cf95-109">Esse script usa Olá comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="9cf95-109">This script uses hello following commands.</span></span> <span data-ttu-id="9cf95-110">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="9cf95-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="9cf95-111">Command</span><span class="sxs-lookup"><span data-stu-id="9cf95-111">Command</span></span> | <span data-ttu-id="9cf95-112">Observações</span><span class="sxs-lookup"><span data-stu-id="9cf95-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="9cf95-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="9cf95-113">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/new-azurermresourcegroup) | <span data-ttu-id="9cf95-114">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="9cf95-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="9cf95-115">New-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="9cf95-115">New-AzureRmResource</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresource?view=azurermps-3.8.0) | <span data-ttu-id="9cf95-116">Cria um servidor lógico que hospeda um banco de dados ou pool elástico.</span><span class="sxs-lookup"><span data-stu-id="9cf95-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="9cf95-117">Invoke-AzureRmResourceAction</span><span class="sxs-lookup"><span data-stu-id="9cf95-117">Invoke-AzureRmResourceAction</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/invoke-azurermresourceaction?view=azurermps-3.8.0) | <span data-ttu-id="9cf95-118">Invoca uma ação hello Azure CosmosDB conta.</span><span class="sxs-lookup"><span data-stu-id="9cf95-118">Invokes an action on hello Azure CosmosDB account.</span></span> |
| [<span data-ttu-id="9cf95-119">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="9cf95-119">Remove-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/remove-azurermresourcegroup) | <span data-ttu-id="9cf95-120">Exclui um grupo de recursos, incluindo todos os recursos aninhados.</span><span class="sxs-lookup"><span data-stu-id="9cf95-120">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="9cf95-121">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9cf95-121">Next steps</span></span>

<span data-ttu-id="9cf95-122">Para obter mais informações sobre hello Azure PowerShell, consulte [documentação do Azure PowerShell](https://docs.microsoft.com/powershell/).</span><span class="sxs-lookup"><span data-stu-id="9cf95-122">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span></span>

<span data-ttu-id="9cf95-123">Exemplos de script do PowerShell do Azure Cosmos DB adicionais podem ser encontrados no hello [scripts do PowerShell do Azure Cosmos DB](../powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="9cf95-123">Additional Azure Cosmos DB PowerShell script samples can be found in hello [Azure Cosmos DB PowerShell scripts](../powershell-samples.md).</span></span>
