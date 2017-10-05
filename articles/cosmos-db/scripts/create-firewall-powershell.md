---
title: "Script do Azure PowerShell – Criar um firewall para o Banco de Dados Cosmos do Azure | Microsoft Docs"
description: "Exemplo de script do Azure PowerShell – Criar um firewall para o Banco de Dados Cosmos do Azure"
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
ms.openlocfilehash: caad9212649dd3dc47ddb21555b5b8496c3d2da1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-create-a-firewall-using-powershell"></a><span data-ttu-id="69439-103">Banco de Dados Cosmos do Azure: Criar um firewall usando PowerShell</span><span class="sxs-lookup"><span data-stu-id="69439-103">Azure Cosmos DB: Create a firewall using PowerShell</span></span>

<span data-ttu-id="69439-104">Este exemplo de script do PowerShell cria um firewall para qualquer tipo de conta de API do Banco de Dados Cosmos do Azure.</span><span class="sxs-lookup"><span data-stu-id="69439-104">This sample PowerShell script creates a firewall for any kind of Azure Cosmos DB API account.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="69439-105">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="69439-105">Sample script</span></span>

<span data-ttu-id="69439-106">[!code-powershell[main](../../../powershell_scripts/cosmosdb/create-firewall/create-firewall.ps1?highlight=35-36,39-43 "Criar um firewall para o Banco de Dados Cosmos do Azure")]</span><span class="sxs-lookup"><span data-stu-id="69439-106">[!code-powershell[main](../../../powershell_scripts/cosmosdb/create-firewall/create-firewall.ps1?highlight=35-36,39-43 "Create a firewall for Azure Cosmos DB")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="69439-107">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="69439-107">Clean up deployment</span></span>

<span data-ttu-id="69439-108">Após executar o exemplo de script, o comando a seguir pode ser usado para remover o grupo de recursos e todos os recursos associados a ele.</span><span class="sxs-lookup"><span data-stu-id="69439-108">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="69439-109">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="69439-109">Script explanation</span></span>

<span data-ttu-id="69439-110">Este script usa os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="69439-110">This script uses the following commands.</span></span> <span data-ttu-id="69439-111">Cada comando na tabela redireciona para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="69439-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="69439-112">Command</span><span class="sxs-lookup"><span data-stu-id="69439-112">Command</span></span> | <span data-ttu-id="69439-113">Observações</span><span class="sxs-lookup"><span data-stu-id="69439-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="69439-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="69439-114">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/new-azurermresourcegroup) | <span data-ttu-id="69439-115">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="69439-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="69439-116">New-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="69439-116">New-AzureRmResource</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresource?view=azurermps-3.8.0) | <span data-ttu-id="69439-117">Cria um servidor lógico que hospeda um banco de dados ou pool elástico.</span><span class="sxs-lookup"><span data-stu-id="69439-117">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="69439-118">Set-AzureRMResource</span><span class="sxs-lookup"><span data-stu-id="69439-118">Set-AzureRMResource</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/set-azurermresource?view=azurermps-3.8.0) | <span data-ttu-id="69439-119">Modifica a conta do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="69439-119">Modifies the database account.</span></span> |
| [<span data-ttu-id="69439-120">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="69439-120">Remove-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/remove-azurermresourcegroup) | <span data-ttu-id="69439-121">Exclui um grupo de recursos, incluindo todos os recursos aninhados.</span><span class="sxs-lookup"><span data-stu-id="69439-121">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="69439-122">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="69439-122">Next steps</span></span>

<span data-ttu-id="69439-123">Para obter mais informações sobre o Azure PowerShell, confira [Documentação do Azure PowerShell](https://docs.microsoft.com/powershell/).</span><span class="sxs-lookup"><span data-stu-id="69439-123">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span></span>

<span data-ttu-id="69439-124">Exemplos adicionais de scripts do PowerShell do Banco de Dados Cosmos do Azure podem ser encontrados nos [Scripts do PowerShell do Banco de Dados Cosmos do Azure](../powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="69439-124">Additional Azure Cosmos DB PowerShell script samples can be found in the [Azure Cosmos DB PowerShell scripts](../powershell-samples.md).</span></span>