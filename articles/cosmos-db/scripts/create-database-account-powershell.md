---
title: aaaAzure PowerShell Script-criar uma conta de API de documentos do Azure Cosmos DB | Microsoft Docs
description: "Exemplo de script do Azure PowerShell – Criar uma conta de API do DocumentDB do Banco de Dados Cosmos do Azure"
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
ms.openlocfilehash: f0751faeca3c1de5906b675e736c58f3d5beaea9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-create-a-documentdb-api-account-using-powershell"></a><span data-ttu-id="d9fed-103">Banco de Dados Cosmos do Azure: Criar uma conta da API do DocumentDB usando PowerShell</span><span class="sxs-lookup"><span data-stu-id="d9fed-103">Azure Cosmos DB: Create a DocumentDB API account using PowerShell</span></span>

<span data-ttu-id="d9fed-104">Este exemplo de script do PowerShell cria uma conta de API do Banco de Dados Cosmos do Azure.</span><span class="sxs-lookup"><span data-stu-id="d9fed-104">This sample PowerShell script creates an Azure Cosmos DB API account.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="d9fed-105">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="d9fed-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/cosmosdb/create-and-configure-database/create-and-configure-database.ps1?highlight=9,12-15,18,21-23,26-29,32-37 "Create an Azure Cosmos DB account")]

## <a name="clean-up-deployment"></a><span data-ttu-id="d9fed-106">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="d9fed-106">Clean up deployment</span></span>

<span data-ttu-id="d9fed-107">Após a execução do exemplo de script hello, Olá comando a seguir pode ser usado tooremove grupo de recursos de saudação e todos os recursos associados a ele.</span><span class="sxs-lookup"><span data-stu-id="d9fed-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="d9fed-108">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="d9fed-108">Script explanation</span></span>

<span data-ttu-id="d9fed-109">Esse script usa Olá comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="d9fed-109">This script uses hello following commands.</span></span> <span data-ttu-id="d9fed-110">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="d9fed-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="d9fed-111">Command</span><span class="sxs-lookup"><span data-stu-id="d9fed-111">Command</span></span> | <span data-ttu-id="d9fed-112">Observações</span><span class="sxs-lookup"><span data-stu-id="d9fed-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="d9fed-113">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="d9fed-113">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/new-azurermresourcegroup) | <span data-ttu-id="d9fed-114">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="d9fed-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="d9fed-115">New-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="d9fed-115">New-AzureRmResource</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresource?view=azurermps-3.8.0) | <span data-ttu-id="d9fed-116">Cria um servidor lógico que hospeda um banco de dados ou pool elástico.</span><span class="sxs-lookup"><span data-stu-id="d9fed-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="d9fed-117">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="d9fed-117">Remove-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/remove-azurermresourcegroup) | <span data-ttu-id="d9fed-118">Exclui um grupo de recursos, incluindo todos os recursos aninhados.</span><span class="sxs-lookup"><span data-stu-id="d9fed-118">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="d9fed-119">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d9fed-119">Next steps</span></span>

<span data-ttu-id="d9fed-120">Para obter mais informações sobre hello Azure PowerShell, consulte [documentação do Azure PowerShell](https://docs.microsoft.com/powershell/).</span><span class="sxs-lookup"><span data-stu-id="d9fed-120">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span></span>

<span data-ttu-id="d9fed-121">Exemplos de script do PowerShell do Azure Cosmos DB adicionais podem ser encontrados no hello [scripts do PowerShell do Azure Cosmos DB](../powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="d9fed-121">Additional Azure Cosmos DB PowerShell script samples can be found in hello [Azure Cosmos DB PowerShell scripts](../powershell-samples.md).</span></span>
