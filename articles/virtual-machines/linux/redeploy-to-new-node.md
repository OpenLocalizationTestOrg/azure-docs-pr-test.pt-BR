---
title: "aaaRedeploy máquinas virtuais Linux no Azure | Microsoft Docs"
description: "Como máquinas de virtuais de Linux tooredeploy na conexão de SSH toomitigate do Azure emite."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
tags: azure-resource-manager,top-support-issue
ms.assetid: e9530dd6-f5b0-4160-b36b-d75151d99eb7
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: support-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/23/2017
ms.author: iainfou
ms.openlocfilehash: 9adfd1b11f262d362133366b2bba5e69c70c9b82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="redeploy-linux-virtual-machine-toonew-azure-node"></a><span data-ttu-id="4b7c4-103">Reimplantar toonew de máquina virtual Linux nó do Azure</span><span class="sxs-lookup"><span data-stu-id="4b7c4-103">Redeploy Linux virtual machine toonew Azure node</span></span>
<span data-ttu-id="4b7c4-104">Se você enfrentar problemas SSH de solução de problemas ou aplicativo acessar a máquina virtual do Linux tooa (VM) no Azure, reimplantar Olá VM pode ajudar.</span><span class="sxs-lookup"><span data-stu-id="4b7c4-104">If you face difficulties troubleshooting SSH or application access tooa Linux virtual machine (VM) in Azure, redeploying hello VM may help.</span></span> <span data-ttu-id="4b7c4-105">Quando você reimplanta uma VM, ele move Olá VM tooa novo nó no hello infraestrutura do Azure e liga novamente.</span><span class="sxs-lookup"><span data-stu-id="4b7c4-105">When you redeploy a VM, it moves hello VM tooa new node within hello Azure infrastructure and then powers it back on.</span></span> <span data-ttu-id="4b7c4-106">Todos os recursos associados e opções de configuração são mantidos.</span><span class="sxs-lookup"><span data-stu-id="4b7c4-106">All your configuration options and associated resources are retained.</span></span> <span data-ttu-id="4b7c4-107">Este artigo mostra como tooredeploy uma VM usando a CLI do Azure ou hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="4b7c4-107">This article shows you how tooredeploy a VM using Azure CLI or hello Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="4b7c4-108">Depois que você reimplanta uma VM, disco temporário Olá é perdido e endereços IP dinâmicos associados à interface de rede virtual são atualizados.</span><span class="sxs-lookup"><span data-stu-id="4b7c4-108">After you redeploy a VM, hello temporary disk is lost and dynamic IP addresses associated with virtual network interface are updated.</span></span> 

<span data-ttu-id="4b7c4-109">Você pode reimplantar uma VM usando um Olá as opções a seguir.</span><span class="sxs-lookup"><span data-stu-id="4b7c4-109">You can redeploy a VM using one of hello following options.</span></span> <span data-ttu-id="4b7c4-110">Você só precisa toochoose uma opção tooredeploy sua VM:</span><span class="sxs-lookup"><span data-stu-id="4b7c4-110">You only need toochoose one option tooredeploy your VM:</span></span>

- [<span data-ttu-id="4b7c4-111">CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="4b7c4-111">Azure CLI 2.0</span></span>](#azure-cli-20)
- [<span data-ttu-id="4b7c4-112">CLI 1.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="4b7c4-112">Azure CLI 1.0</span></span>](#azure-cli-10)
- [<span data-ttu-id="4b7c4-113">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="4b7c4-113">Azure portal</span></span>](#using-azure-portal)

## <a name="use-hello-azure-cli-20"></a><span data-ttu-id="4b7c4-114">Use Olá 2.0 do CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="4b7c4-114">Use hello Azure CLI 2.0</span></span>
<span data-ttu-id="4b7c4-115">Saudação de instalação mais recente [2.0 do CLI do Azure](/cli/azure/install-az-cli2) e fazer logon na conta do Azure usando o tooan [logon az](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="4b7c4-115">Install hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="4b7c4-116">Reimplante a VM com [az vm redeploy](/cli/azure/vm#redeploy).</span><span class="sxs-lookup"><span data-stu-id="4b7c4-116">Redeploy your VM with [az vm redeploy](/cli/azure/vm#redeploy).</span></span> <span data-ttu-id="4b7c4-117">Olá reimplanta de exemplo a seguir Olá VM denominada *myVM* no grupo de recursos de saudação denominado *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="4b7c4-117">hello following example redeploys hello VM named *myVM* in hello resource group named *myResourceGroup*:</span></span>

```azurecli
az vm redeploy --resource-group myResourceGroup --name myVM 
```

## <a name="use-hello-azure-cli-10"></a><span data-ttu-id="4b7c4-118">Use Olá 1.0 da CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="4b7c4-118">Use hello Azure CLI 1.0</span></span>
<span data-ttu-id="4b7c4-119">Instalar Olá [mais recente do Azure CLI 1.0](../../cli-install-nodejs.md), faça logon no tooan conta do Azure e certifique-se de que você está no modo do Gerenciador de recursos (`azure config mode arm`).</span><span class="sxs-lookup"><span data-stu-id="4b7c4-119">Install hello [latest Azure CLI 1.0](../../cli-install-nodejs.md), log in tooan Azure account, and make sure that you are in Resource Manager mode (`azure config mode arm`).</span></span>

<span data-ttu-id="4b7c4-120">Olá reimplanta de exemplo a seguir Olá VM denominada *myVM* no grupo de recursos de saudação denominado *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="4b7c4-120">hello following example redeploys hello VM named *myVM* in hello resource group named *myResourceGroup*:</span></span>

```azurecli
azure vm redeploy --resource-group myResourceGroup --vm-name myVM 
```

[!INCLUDE [virtual-machines-common-redeploy-to-new-node](../../../includes/virtual-machines-common-redeploy-to-new-node.md)]

## <a name="next-steps"></a><span data-ttu-id="4b7c4-121">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4b7c4-121">Next steps</span></span>
<span data-ttu-id="4b7c4-122">Se você estiver tendo problemas para se conectar tooyour VM, você pode encontrar ajuda específica na [Solucionando problemas de conexões SSH](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) ou [detalhadas etapas de solução de problemas de SSH](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4b7c4-122">If you are having issues connecting tooyour VM, you can find specific help on [troubleshooting SSH connections](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [detailed SSH troubleshooting steps](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="4b7c4-123">Você também pode ler [problemas com a solução de problemas de aplicativo](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) se não conseguir acessar um aplicativo em execução em sua VM.</span><span class="sxs-lookup"><span data-stu-id="4b7c4-123">If you cannot access an application running on your VM, you can also read [application troubleshooting issues](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

