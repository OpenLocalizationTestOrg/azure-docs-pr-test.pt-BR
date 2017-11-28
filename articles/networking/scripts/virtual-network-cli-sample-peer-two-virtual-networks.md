---
title: aaaAzure exemplo de Script CLI - Peer duas redes virtuais | Microsoft Docs
description: Exemplo de Script da CLI do Azure - Emparelhar duas redes virtuais
services: virtual-network
documentationcenter: virtual-network
author: KumudD
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 07/07/2017
ms.author: kumud
ms.openlocfilehash: 54dabb2b9e05951d10f1b6b4f61ca592ce11d364
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="peer-two-virtual-networks"></a><span data-ttu-id="6ecdd-103">Emparelhar duas redes virtuais</span><span class="sxs-lookup"><span data-stu-id="6ecdd-103">Peer two virtual networks</span></span>

<span data-ttu-id="6ecdd-104">Esse script cria e conecta-se duas redes virtuais no Olá Olá de trhough região mesma rede do Azure.</span><span class="sxs-lookup"><span data-stu-id="6ecdd-104">This script creates and connects two virtual networks in hello same region trhough hello Azure network.</span></span> <span data-ttu-id="6ecdd-105">Depois de executar o script hello, você criará um emparelhamento entre duas redes virtuais.</span><span class="sxs-lookup"><span data-stu-id="6ecdd-105">After running hello script, you will create a peering between two virtual networks.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


## <a name="sample-script"></a><span data-ttu-id="6ecdd-106">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="6ecdd-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/peer-two-virtual-networks/peer-two-virtual-networks.sh "Peer two networks")]

## <a name="clean-up-deployment"></a><span data-ttu-id="6ecdd-107">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="6ecdd-107">Clean up deployment</span></span> 

<span data-ttu-id="6ecdd-108">Execute Olá grupo de recursos do comando tooremove hello, a VM e relacionados com todos os recursos a seguir.</span><span class="sxs-lookup"><span data-stu-id="6ecdd-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="6ecdd-109">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="6ecdd-109">Script explanation</span></span>

<span data-ttu-id="6ecdd-110">Esse script usa Olá seguir comandos toocreate um grupo de recursos, a máquina virtual, e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="6ecdd-110">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="6ecdd-111">Cada comando na documentação específica do toocommand Olá tabela links.</span><span class="sxs-lookup"><span data-stu-id="6ecdd-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="6ecdd-112">Command</span><span class="sxs-lookup"><span data-stu-id="6ecdd-112">Command</span></span> | <span data-ttu-id="6ecdd-113">Observações</span><span class="sxs-lookup"><span data-stu-id="6ecdd-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="6ecdd-114">az group create</span><span class="sxs-lookup"><span data-stu-id="6ecdd-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="6ecdd-115">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="6ecdd-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="6ecdd-116">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="6ecdd-116">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="6ecdd-117">Cria uma sub-rede e uma rede virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="6ecdd-117">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="6ecdd-118">criar emparelhamento de VNET de rede virtual az</span><span class="sxs-lookup"><span data-stu-id="6ecdd-118">az network vnet peering create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet/peering#create) | <span data-ttu-id="6ecdd-119">Cria um emparelhamento entre duas redes virtuais.</span><span class="sxs-lookup"><span data-stu-id="6ecdd-119">Creates a peering between two virtual networks.</span></span>  |
| [<span data-ttu-id="6ecdd-120">az group delete</span><span class="sxs-lookup"><span data-stu-id="6ecdd-120">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="6ecdd-121">Exclui um grupo de recursos, incluindo todos os recursos aninhados.</span><span class="sxs-lookup"><span data-stu-id="6ecdd-121">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="6ecdd-122">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6ecdd-122">Next steps</span></span>

<span data-ttu-id="6ecdd-123">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="6ecdd-123">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="6ecdd-124">Exemplos de script CLI rede adicionais podem ser encontrados no hello [documentação de visão geral da rede do Azure](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="6ecdd-124">Additional networking CLI script samples can be found in hello [Azure Networking Overview documentation](../cli-samples.md).</span></span>
