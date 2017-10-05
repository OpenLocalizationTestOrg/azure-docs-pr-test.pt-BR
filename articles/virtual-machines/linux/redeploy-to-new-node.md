---
title: "Reimplantar Máquinas Virtuais Linux no Azure | Microsoft Docs"
description: "Como reimplantar máquinas virtuais Linux no Azure para atenuar problemas de conexão SSH."
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
ms.openlocfilehash: 7a8653a82775e718c38f65f246d997ba61f99d58
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="redeploy-linux-virtual-machine-to-new-azure-node"></a><span data-ttu-id="0d1a1-103">Reimplantar uma máquina virtual Linux em um novo nó do Azure</span><span class="sxs-lookup"><span data-stu-id="0d1a1-103">Redeploy Linux virtual machine to new Azure node</span></span>
<span data-ttu-id="0d1a1-104">Se você tiver dificuldades ao solucionar problemas de SSH ou de acesso do aplicativo a uma VM (máquina virtual) Linux no Azure, reimplantar a VM poderá ajudar.</span><span class="sxs-lookup"><span data-stu-id="0d1a1-104">If you face difficulties troubleshooting SSH or application access to a Linux virtual machine (VM) in Azure, redeploying the VM may help.</span></span> <span data-ttu-id="0d1a1-105">Quando você reimplanta uma VM, ela é movida para um novo nó dentro da infraestrutura do Azure e, depois, é ligada novamente.</span><span class="sxs-lookup"><span data-stu-id="0d1a1-105">When you redeploy a VM, it moves the VM to a new node within the Azure infrastructure and then powers it back on.</span></span> <span data-ttu-id="0d1a1-106">Todos os recursos associados e opções de configuração são mantidos.</span><span class="sxs-lookup"><span data-stu-id="0d1a1-106">All your configuration options and associated resources are retained.</span></span> <span data-ttu-id="0d1a1-107">Este artigo mostra como reimplantar uma VM usando a CLI do Azure ou o Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="0d1a1-107">This article shows you how to redeploy a VM using Azure CLI or the Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="0d1a1-108">Depois que você reimplanta uma VM, o disco temporário será perdido e os endereços IP dinâmicos associados ao adaptador de rede virtual serão atualizados.</span><span class="sxs-lookup"><span data-stu-id="0d1a1-108">After you redeploy a VM, the temporary disk is lost and dynamic IP addresses associated with virtual network interface are updated.</span></span> 

<span data-ttu-id="0d1a1-109">Reimplante uma VM usando uma das opções a seguir.</span><span class="sxs-lookup"><span data-stu-id="0d1a1-109">You can redeploy a VM using one of the following options.</span></span> <span data-ttu-id="0d1a1-110">Escolha uma opção para reimplantar a VM:</span><span class="sxs-lookup"><span data-stu-id="0d1a1-110">You only need to choose one option to redeploy your VM:</span></span>

- [<span data-ttu-id="0d1a1-111">CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="0d1a1-111">Azure CLI 2.0</span></span>](#azure-cli-20)
- [<span data-ttu-id="0d1a1-112">CLI 1.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="0d1a1-112">Azure CLI 1.0</span></span>](#azure-cli-10)
- [<span data-ttu-id="0d1a1-113">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="0d1a1-113">Azure portal</span></span>](#using-azure-portal)

## <a name="use-the-azure-cli-20"></a><span data-ttu-id="0d1a1-114">Usar a CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="0d1a1-114">Use the Azure CLI 2.0</span></span>
<span data-ttu-id="0d1a1-115">Instale a [CLI 2.0 do Azure](/cli/azure/install-az-cli2) mais recente e faça logon em uma conta do Azure usando [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="0d1a1-115">Install the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="0d1a1-116">Reimplante a VM com [az vm redeploy](/cli/azure/vm#redeploy).</span><span class="sxs-lookup"><span data-stu-id="0d1a1-116">Redeploy your VM with [az vm redeploy](/cli/azure/vm#redeploy).</span></span> <span data-ttu-id="0d1a1-117">O exemplo a seguir reimplanta a VM chamada *myVM* no grupo de recursos chamado *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="0d1a1-117">The following example redeploys the VM named *myVM* in the resource group named *myResourceGroup*:</span></span>

```azurecli
az vm redeploy --resource-group myResourceGroup --name myVM 
```

## <a name="use-the-azure-cli-10"></a><span data-ttu-id="0d1a1-118">Usar a CLI 1.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="0d1a1-118">Use the Azure CLI 1.0</span></span>
<span data-ttu-id="0d1a1-119">Instale a [CLI 1.0 do Azure mais recente](../../cli-install-nodejs.md), faça logon uma conta do Azure e verifique se você está no modo do Resource Manager (`azure config mode arm`).</span><span class="sxs-lookup"><span data-stu-id="0d1a1-119">Install the [latest Azure CLI 1.0](../../cli-install-nodejs.md), log in to an Azure account, and make sure that you are in Resource Manager mode (`azure config mode arm`).</span></span>

<span data-ttu-id="0d1a1-120">O exemplo a seguir reimplanta a VM chamada *myVM* no grupo de recursos chamado *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="0d1a1-120">The following example redeploys the VM named *myVM* in the resource group named *myResourceGroup*:</span></span>

```azurecli
azure vm redeploy --resource-group myResourceGroup --vm-name myVM 
```

[!INCLUDE [virtual-machines-common-redeploy-to-new-node](../../../includes/virtual-machines-common-redeploy-to-new-node.md)]

## <a name="next-steps"></a><span data-ttu-id="0d1a1-121">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0d1a1-121">Next steps</span></span>
<span data-ttu-id="0d1a1-122">Se você estiver enfrentando problemas para se conectar à sua VM., encontre ajuda específica em [Solução de problemas de conexões SSH](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) ou [Etapas detalhadas de solução de problemas de SSH](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0d1a1-122">If you are having issues connecting to your VM, you can find specific help on [troubleshooting SSH connections](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or [detailed SSH troubleshooting steps](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="0d1a1-123">Você também pode ler [problemas com a solução de problemas de aplicativo](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) se não conseguir acessar um aplicativo em execução em sua VM.</span><span class="sxs-lookup"><span data-stu-id="0d1a1-123">If you cannot access an application running on your VM, you can also read [application troubleshooting issues](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

