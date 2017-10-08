---
title: aaaAzure exemplo de Script do PowerShell - Peer duas redes virtuais | Microsoft Docs
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
ms.openlocfilehash: 8b66085c35de2fc30bcef57a00d7d370911d1f3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="peer-two-virtual-networks"></a><span data-ttu-id="d4c55-103">Emparelhar duas redes virtuais</span><span class="sxs-lookup"><span data-stu-id="d4c55-103">Peer two virtual networks</span></span>

<span data-ttu-id="d4c55-104">Esse script cria e conecta-se duas redes virtuais no Olá Olá de trhough região mesma rede do Azure.</span><span class="sxs-lookup"><span data-stu-id="d4c55-104">This script creates and connects two virtual networks in hello same region trhough hello Azure network.</span></span> <span data-ttu-id="d4c55-105">Depois de executar o script hello, você criará um emparelhamento entre duas redes virtuais.</span><span class="sxs-lookup"><span data-stu-id="d4c55-105">After running hello script, you will create a peering between two virtual networks.</span></span>

<span data-ttu-id="d4c55-106">Se necessário, instale Olá PowerShell do Azure usando a instrução Olá encontrado no hello [guia do PowerShell do Azure](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/)e, em seguida, execute `Login-AzureRmAccount` toocreate uma conexão com o Azure.</span><span class="sxs-lookup"><span data-stu-id="d4c55-106">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="d4c55-107">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="d4c55-107">Sample script</span></span>

[!code-azurepowershell[main](../../../powershell_scripts/virtual-network/peer-two-virtual-networks/peer-two-virtual-networks.ps1 "Peer two networks")]

## <a name="clean-up-deployment"></a><span data-ttu-id="d4c55-108">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="d4c55-108">Clean up deployment</span></span> 

<span data-ttu-id="d4c55-109">Execute Olá grupo de recursos do comando tooremove hello, a VM e relacionados com todos os recursos a seguir.</span><span class="sxs-lookup"><span data-stu-id="d4c55-109">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="d4c55-110">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="d4c55-110">Script explanation</span></span>

<span data-ttu-id="d4c55-111">Esse script usa Olá seguir comandos toocreate um grupo de recursos, a máquina virtual, e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="d4c55-111">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="d4c55-112">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="d4c55-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="d4c55-113">Command</span><span class="sxs-lookup"><span data-stu-id="d4c55-113">Command</span></span> | <span data-ttu-id="d4c55-114">Observações</span><span class="sxs-lookup"><span data-stu-id="d4c55-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="d4c55-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="d4c55-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="d4c55-116">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="d4c55-116">Creates a resource group in which all resources are stored.</span></span> | 
| [<span data-ttu-id="d4c55-117">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="d4c55-117">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork)| <span data-ttu-id="d4c55-118">Cria uma sub-rede e uma rede virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="d4c55-118">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="d4c55-119">Add-AzureRmVirtualNetworkPeering</span><span class="sxs-lookup"><span data-stu-id="d4c55-119">Add-AzureRmVirtualNetworkPeering</span></span>](/powershell/module/azurerm.network/add-azurermvirtualnetworkpeering) | <span data-ttu-id="d4c55-120">Cria um emparelhamento entre duas redes virtuais.</span><span class="sxs-lookup"><span data-stu-id="d4c55-120">Creates a peering between two virtual networks.</span></span>  |
| [<span data-ttu-id="d4c55-121">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="d4c55-121">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="d4c55-122">Exclui um grupo de recursos, incluindo todos os recursos aninhados.</span><span class="sxs-lookup"><span data-stu-id="d4c55-122">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="d4c55-123">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d4c55-123">Next steps</span></span>

<span data-ttu-id="d4c55-124">Para obter mais informações sobre hello Azure PowerShell, consulte [documentação do Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d4c55-124">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="d4c55-125">Exemplos de script do PowerShell rede adicionais podem ser encontrados no hello [documentação de visão geral da rede do Azure](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d4c55-125">Additional networking PowerShell script samples can be found in hello [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>
