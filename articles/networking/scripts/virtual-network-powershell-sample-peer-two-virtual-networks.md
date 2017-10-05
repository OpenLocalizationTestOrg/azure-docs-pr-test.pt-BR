---
title: "Exemplo de script do Azure PowerShell – Emparelhar duas redes virtuais | Microsoft Docs"
description: "Exemplo de Script do Azure PowerShell – Emparelhar duas redes virtuais"
services: virtual-network
documentationcenter: virtual-network
author: georgewallace
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: powershell
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 05/16/2017
ms.author: gwallace
ms.openlocfilehash: 51c0b98727e148671cfd7ab2b31ffd1c705d8a4e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="peer-two-virtual-networks"></a><span data-ttu-id="338db-103">Emparelhar duas redes virtuais</span><span class="sxs-lookup"><span data-stu-id="338db-103">Peer two virtual networks</span></span>

<span data-ttu-id="338db-104">Este script cria e conecta duas redes virtuais na mesma região através da rede do Azure.</span><span class="sxs-lookup"><span data-stu-id="338db-104">This script creates and connects two virtual networks in the same region trhough the Azure network.</span></span> <span data-ttu-id="338db-105">Depois de executar o script, você criará um emparelhamento entre duas redes virtuais.</span><span class="sxs-lookup"><span data-stu-id="338db-105">After running the script, you will create a peering between two virtual networks.</span></span>

<span data-ttu-id="338db-106">Se necessário, instale o Azure PowerShell usando a instrução encontrada no [guia do Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/) e, em seguida, execute `Login-AzureRmAccount` para criar uma conexão com o Azure.</span><span class="sxs-lookup"><span data-stu-id="338db-106">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="338db-107">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="338db-107">Sample script</span></span>

<span data-ttu-id="338db-108">[!code-azurepowershell[principal](../../../powershell_scripts/virtual-network/peer-two-virtual-networks/peer-two-virtual-networks.ps1 "Emparelhar duas redes")]</span><span class="sxs-lookup"><span data-stu-id="338db-108">[!code-azurepowershell[main](../../../powershell_scripts/virtual-network/peer-two-virtual-networks/peer-two-virtual-networks.ps1 "Peer two networks")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="338db-109">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="338db-109">Clean up deployment</span></span> 

<span data-ttu-id="338db-110">Execute o comando a seguir para remover o grupo de recursos, a VM e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="338db-110">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="338db-111">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="338db-111">Script explanation</span></span>

<span data-ttu-id="338db-112">Este script usa os comandos a seguir para criar um grupo de recursos, uma máquina virtual e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="338db-112">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="338db-113">Cada comando na tabela redireciona para a documentação específica do comando.</span><span class="sxs-lookup"><span data-stu-id="338db-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="338db-114">Command</span><span class="sxs-lookup"><span data-stu-id="338db-114">Command</span></span> | <span data-ttu-id="338db-115">Observações</span><span class="sxs-lookup"><span data-stu-id="338db-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="338db-116">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="338db-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="338db-117">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="338db-117">Creates a resource group in which all resources are stored.</span></span> | 
| [<span data-ttu-id="338db-118">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="338db-118">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork)| <span data-ttu-id="338db-119">Cria uma sub-rede e uma rede virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="338db-119">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="338db-120">Add-AzureRmVirtualNetworkPeering</span><span class="sxs-lookup"><span data-stu-id="338db-120">Add-AzureRmVirtualNetworkPeering</span></span>](/powershell/module/azurerm.network/add-azurermvirtualnetworkpeering) | <span data-ttu-id="338db-121">Cria um emparelhamento entre duas redes virtuais.</span><span class="sxs-lookup"><span data-stu-id="338db-121">Creates a peering between two virtual networks.</span></span>  |
| [<span data-ttu-id="338db-122">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="338db-122">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="338db-123">Exclui um grupo de recursos, incluindo todos os recursos aninhados.</span><span class="sxs-lookup"><span data-stu-id="338db-123">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="338db-124">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="338db-124">Next steps</span></span>

<span data-ttu-id="338db-125">Para obter mais informações sobre o Azure PowerShell, confira [Documentação do Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="338db-125">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="338db-126">Exemplos adicionais de script de PowerShell de rede podem ser encontrados na [Documentação de visão geral da rede do Azure](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="338db-126">Additional networking PowerShell script samples can be found in the [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>