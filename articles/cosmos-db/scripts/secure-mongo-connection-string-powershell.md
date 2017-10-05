---
title: "Script do Azure PowerShell – obter uma cadeia de conexão do BD Cosmos do Azure para aplicativos MongoDB | Microsoft Docs"
description: "Exemplo de script do Azure PowerShell – obter uma cadeia de conexão do BD Cosmos do Azure para aplicativos MongoDB"
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
ms.openlocfilehash: e44e35cc7d11db48cd82e470ce8226b3c8cc220a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-an-azure-cosmos-db-connection-string-for-mongodb-apps-using-powershell"></a><span data-ttu-id="5d20a-103">Obtenha uma cadeia de conexão do BD Cosmos do Azure para aplicativos MongoDB usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="5d20a-103">Get an Azure Cosmos DB connection string for MongoDB apps using PowerShell</span></span>

<span data-ttu-id="5d20a-104">Este exemplo obtém uma cadeia de conexão do BD Cosmos do Azure para aplicativos MongoDB usando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5d20a-104">This sample gets an Azure Cosmos DB connection string for MongoDB apps using PowerShell.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="5d20a-105">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="5d20a-105">Sample script</span></span>

<span data-ttu-id="5d20a-106">[!code-powershell[principal](../../../powershell_scripts/cosmosdb/get-mongodb-connection-string/get-mongodb-connection-string.ps1?highlight=37-41 "Obter a cadeia de conexão do MongoDB de uma conta do BD Cosmos do Azure")]</span><span class="sxs-lookup"><span data-stu-id="5d20a-106">[!code-powershell[main](../../../powershell_scripts/cosmosdb/get-mongodb-connection-string/get-mongodb-connection-string.ps1?highlight=37-41 "Get the MongoDB connection string from an Azure Cosmos DB account")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="5d20a-107">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="5d20a-107">Clean up deployment</span></span>

<span data-ttu-id="5d20a-108">Após executar o exemplo de script, o comando a seguir pode ser usado para remover o grupo de recursos e todos os recursos associados a ele.</span><span class="sxs-lookup"><span data-stu-id="5d20a-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="5d20a-109">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="5d20a-109">Script explanation</span></span>

<span data-ttu-id="5d20a-110">Este script usa os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="5d20a-110">This script uses the following commands.</span></span> <span data-ttu-id="5d20a-111">Cada comando na tabela redireciona para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="5d20a-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="5d20a-112">Command</span><span class="sxs-lookup"><span data-stu-id="5d20a-112">Command</span></span> | <span data-ttu-id="5d20a-113">Observações</span><span class="sxs-lookup"><span data-stu-id="5d20a-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="5d20a-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="5d20a-114">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/new-azurermresourcegroup) | <span data-ttu-id="5d20a-115">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="5d20a-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="5d20a-116">New-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="5d20a-116">New-AzureRmResource</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresource?view=azurermps-3.8.0) | <span data-ttu-id="5d20a-117">Cria um servidor lógico que hospeda um banco de dados ou pool elástico.</span><span class="sxs-lookup"><span data-stu-id="5d20a-117">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="5d20a-118">Invoke-AzureRmResourceAction</span><span class="sxs-lookup"><span data-stu-id="5d20a-118">Invoke-AzureRmResourceAction</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/invoke-azurermresourceaction?view=azurermps-3.8.0) | <span data-ttu-id="5d20a-119">Invoca uma ação na conta do BD Cosmos do Azure.</span><span class="sxs-lookup"><span data-stu-id="5d20a-119">Invokes an action on the Azure CosmosDB account.</span></span> |
| [<span data-ttu-id="5d20a-120">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="5d20a-120">Remove-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/remove-azurermresourcegroup) | <span data-ttu-id="5d20a-121">Exclui um grupo de recursos, incluindo todos os recursos aninhados.</span><span class="sxs-lookup"><span data-stu-id="5d20a-121">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="5d20a-122">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5d20a-122">Next steps</span></span>

<span data-ttu-id="5d20a-123">Para obter mais informações sobre o Azure PowerShell, confira [Documentação do Azure PowerShell](https://docs.microsoft.com/powershell/).</span><span class="sxs-lookup"><span data-stu-id="5d20a-123">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span></span>

<span data-ttu-id="5d20a-124">Exemplos adicionais de scripts do PowerShell do Banco de Dados Cosmos do Azure podem ser encontrados nos [Scripts do PowerShell do Banco de Dados Cosmos do Azure](../powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="5d20a-124">Additional Azure Cosmos DB PowerShell script samples can be found in the [Azure Cosmos DB PowerShell scripts](../powershell-samples.md).</span></span>