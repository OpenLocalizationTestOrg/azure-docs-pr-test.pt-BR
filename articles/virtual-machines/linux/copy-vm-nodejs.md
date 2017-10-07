---
title: "aaaCreate uma cópia da sua VM do Linux com hello 1.0 da CLI do Azure | Microsoft Docs"
description: "Saiba como toocreate uma cópia da máquina virtual do Azure Linux com hello Azure CLI 1.0 no modelo de implantação do Gerenciador de recursos de saudação"
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
tags: azure-resource-manager
ms.assetid: 770569d2-23c1-4a5b-801e-cddcd1375164
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/22/2017
ms.author: cynthn
ms.openlocfilehash: 997a2c8109e7083ececd76fd1013e9ed4d3e6afd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-copy-of-a-linux-virtual-machine-running-on-azure-with-hello-azure-cli-10"></a><span data-ttu-id="a13a2-103">Criar uma cópia de uma máquina virtual do Linux em execução no Azure com hello 1.0 da CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="a13a2-103">Create a copy of a Linux virtual machine running on Azure with hello Azure CLI 1.0</span></span>
<span data-ttu-id="a13a2-104">Este artigo mostra como toocreate uma cópia de sua máquina virtual do Azure (VM) em execução Linux usando Olá modelo de implantação do Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="a13a2-104">This article shows you how toocreate a copy of your Azure virtual machine (VM) running Linux using hello Resource Manager deployment model.</span></span> <span data-ttu-id="a13a2-105">Primeiro copiar sobre o sistema operacional de saudação e dados discos tooa novo contêiner, e em seguida, configurar recursos de rede hello e criar nova máquina de virtual hello.</span><span class="sxs-lookup"><span data-stu-id="a13a2-105">First you copy over hello operating system and data disks tooa new container, then set up hello network resources and create hello new virtual machine.</span></span>

<span data-ttu-id="a13a2-106">Você também pode [carregar e criar uma VM com base em uma imagem de disco personalizada](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a13a2-106">You can also [upload and create a VM from custom disk image](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="a13a2-107">Tarefa de saudação do CLI versões toocomplete</span><span class="sxs-lookup"><span data-stu-id="a13a2-107">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="a13a2-108">Você pode concluir a tarefa hello usando uma saudação versões da CLI a seguir:</span><span class="sxs-lookup"><span data-stu-id="a13a2-108">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="a13a2-109">CLI do Azure 1.0 – nosso CLI para Olá clássico e o recurso de gerenciamento modelos de implantação (Este artigo)</span><span class="sxs-lookup"><span data-stu-id="a13a2-109">Azure CLI 1.0 – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="a13a2-110">[2.0 do CLI do Azure](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -nossa próxima geração CLI para o modelo de implantação do gerenciamento de recursos de saudação</span><span class="sxs-lookup"><span data-stu-id="a13a2-110">[Azure CLI 2.0](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="a13a2-111">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="a13a2-111">Before you begin</span></span>
<span data-ttu-id="a13a2-112">Certifique-se de que você atenda aos Olá pré-requisitos a seguir antes de começar as etapas de saudação:</span><span class="sxs-lookup"><span data-stu-id="a13a2-112">Ensure that you meet hello following prerequisites before you start hello steps:</span></span>

* <span data-ttu-id="a13a2-113">Você tem Olá [CLI do Azure](../../cli-install-nodejs.md) baixado e instalado em seu computador.</span><span class="sxs-lookup"><span data-stu-id="a13a2-113">You have hello [Azure CLI](../../cli-install-nodejs.md) downloaded and installed on your machine.</span></span> 
* <span data-ttu-id="a13a2-114">Você também precisa de algumas informações sobre sua VM Linux do Azure existente:</span><span class="sxs-lookup"><span data-stu-id="a13a2-114">You also need some information about your existing Azure Linux VM:</span></span>

| <span data-ttu-id="a13a2-115">Informações sobre a VM de origem</span><span class="sxs-lookup"><span data-stu-id="a13a2-115">Source VM information</span></span> | <span data-ttu-id="a13a2-116">Onde tooget-lo</span><span class="sxs-lookup"><span data-stu-id="a13a2-116">Where tooget it</span></span> |
| --- | --- |
| <span data-ttu-id="a13a2-117">Nome da VM</span><span class="sxs-lookup"><span data-stu-id="a13a2-117">VM name</span></span> |`azure vm list` |
| <span data-ttu-id="a13a2-118">Nome do Grupo de Recursos</span><span class="sxs-lookup"><span data-stu-id="a13a2-118">Resource Group name</span></span> |`azure vm list` |
| <span data-ttu-id="a13a2-119">Local</span><span class="sxs-lookup"><span data-stu-id="a13a2-119">Location</span></span> |`azure vm list` |
| <span data-ttu-id="a13a2-120">Nome da Conta de Armazenamento</span><span class="sxs-lookup"><span data-stu-id="a13a2-120">Storage Account name</span></span> |`azure storage account list -g <resourceGroup>` |
| <span data-ttu-id="a13a2-121">Nome do contêiner</span><span class="sxs-lookup"><span data-stu-id="a13a2-121">Container name</span></span> |`azure storage container list -a <sourcestorageaccountname>` |
| <span data-ttu-id="a13a2-122">Nome do arquivo VHD da VM de origem</span><span class="sxs-lookup"><span data-stu-id="a13a2-122">Source VM VHD file name</span></span> |`azure storage blob list --container <containerName>` |

* <span data-ttu-id="a13a2-123">Você precisará toomake algumas opções sobre a nova VM:   </span><span class="sxs-lookup"><span data-stu-id="a13a2-123">You will need toomake some choices about your new VM:    </span></span><br> <span data-ttu-id="a13a2-124">-Nome do contêiner    </span><span class="sxs-lookup"><span data-stu-id="a13a2-124">-Container name    </span></span><br> <span data-ttu-id="a13a2-125">-Nome da VM    </span><span class="sxs-lookup"><span data-stu-id="a13a2-125">-VM name    </span></span><br> <span data-ttu-id="a13a2-126">-Tamanho da VM    </span><span class="sxs-lookup"><span data-stu-id="a13a2-126">-VM size    </span></span><br> <span data-ttu-id="a13a2-127">-Nome da VNet    </span><span class="sxs-lookup"><span data-stu-id="a13a2-127">-vNet name    </span></span><br> <span data-ttu-id="a13a2-128">-Nome da sub-rede    </span><span class="sxs-lookup"><span data-stu-id="a13a2-128">-SubNet name    </span></span><br> <span data-ttu-id="a13a2-129">-Nome IP    </span><span class="sxs-lookup"><span data-stu-id="a13a2-129">-IP Name    </span></span><br> <span data-ttu-id="a13a2-130">-Nome da NIC</span><span class="sxs-lookup"><span data-stu-id="a13a2-130">-NIC name</span></span>

## <a name="login-and-set-your-subscription"></a><span data-ttu-id="a13a2-131">Faça logon e configure sua assinatura</span><span class="sxs-lookup"><span data-stu-id="a13a2-131">Login and set your subscription</span></span>
1. <span data-ttu-id="a13a2-132">Logon toohello CLI.</span><span class="sxs-lookup"><span data-stu-id="a13a2-132">Login toohello CLI.</span></span>

    ```azurecli
    azure login
    ```
2. <span data-ttu-id="a13a2-133">Certifique-se de estar no modo Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a13a2-133">Make sure you are in Resource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```
3. <span data-ttu-id="a13a2-134">Definir a assinatura correta hello.</span><span class="sxs-lookup"><span data-stu-id="a13a2-134">Set hello correct subscription.</span></span> <span data-ttu-id="a13a2-135">Você pode usar 'lista de contas do azure' toosee todas as suas assinaturas.</span><span class="sxs-lookup"><span data-stu-id="a13a2-135">You can use 'azure account list' toosee all of your subscriptions.</span></span>

    ```azurecli
    azure account set mySubscriptionID
    ```

## <a name="stop-hello-vm"></a><span data-ttu-id="a13a2-136">Parar Olá VM</span><span class="sxs-lookup"><span data-stu-id="a13a2-136">Stop hello VM</span></span>
<span data-ttu-id="a13a2-137">Parar e desalocar a VM de origem hello.</span><span class="sxs-lookup"><span data-stu-id="a13a2-137">Stop and deallocate hello source VM.</span></span> <span data-ttu-id="a13a2-138">Você pode usar 'lista de vm do azure' tooget uma lista de todas as VMs de saudação em sua assinatura e os nomes de grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="a13a2-138">You can use 'azure vm list' tooget a list of all of hello VMs in your subscription and their resource group names.</span></span>

```azurecli
azure vm stop myResourceGroup myVM
azure vm deallocate myResourceGroup MyVM
```


## <a name="copy-hello-vhd"></a><span data-ttu-id="a13a2-139">Copiar Olá VHD</span><span class="sxs-lookup"><span data-stu-id="a13a2-139">Copy hello VHD</span></span>
<span data-ttu-id="a13a2-140">Você pode copiar Olá VHD de destino Olá fonte armazenamento toohello usando Olá `azure storage blob copy start`.</span><span class="sxs-lookup"><span data-stu-id="a13a2-140">You can copy hello VHD from hello source storage toohello destination using hello `azure storage blob copy start`.</span></span> <span data-ttu-id="a13a2-141">Neste exemplo, vamos toocopy Olá VHD toohello mesma conta de armazenamento, mas um contêiner diferente.</span><span class="sxs-lookup"><span data-stu-id="a13a2-141">In this example, we are going toocopy hello VHD toohello same storage account, but a different container.</span></span>

<span data-ttu-id="a13a2-142">contêiner de tooanother VHD toocopy Olá no hello mesma conta de armazenamento, digite:</span><span class="sxs-lookup"><span data-stu-id="a13a2-142">toocopy hello VHD tooanother container in hello same storage account, type:</span></span>

```azurecli
azure storage blob copy start \
        https://mystorageaccountname.blob.core.windows.net:8080/mycontainername/myVHD.vhd \
        myNewContainerName
```

## <a name="set-up-hello-virtual-network-for-your-new-vm"></a><span data-ttu-id="a13a2-143">Configurar a rede virtual Olá para sua nova VM</span><span class="sxs-lookup"><span data-stu-id="a13a2-143">Set up hello virtual network for your new VM</span></span>
<span data-ttu-id="a13a2-144">Configure uma rede virtual e NIC para sua nova VM.</span><span class="sxs-lookup"><span data-stu-id="a13a2-144">Set up a virtual network and NIC for your new VM.</span></span> 

```azurecli
azure network vnet create myResourceGroup myVnet -l myLocation

azure network vnet subnet create -a <address.prefix.in.CIDR/format> myResourceGroup myVnet mySubnet

azure network public-ip create myResourceGroup myPublicIP -l myLocation

azure network nic create myResourceGroup myNic -k mySubnet -m myVnet -p myPublicIP -l myLocation
```


## <a name="create-hello-new-vm"></a><span data-ttu-id="a13a2-145">Criar hello nova VM</span><span class="sxs-lookup"><span data-stu-id="a13a2-145">Create hello new VM</span></span>
<span data-ttu-id="a13a2-146">Agora você pode criar uma máquina virtual do disco virtual carregado [usando um modelo do Gerenciador de recursos](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd) ou por meio de saudação CLI especificando Olá URI tooyour copiados disco digitando:</span><span class="sxs-lookup"><span data-stu-id="a13a2-146">You can now create a VM from your uploaded virtual disk [using a resource manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd) or through hello CLI by specifying hello URI tooyour copied disk by typing:</span></span>

```azurecli
azure vm create -n myVM -l myLocation -g myResourceGroup -f myNic \
        -z Standard_DS1_v2 -y Linux \
        https://mystorageaccountname.blob.core.windows.net:8080/mycontainername/myVHD.vhd 
```



## <a name="next-steps"></a><span data-ttu-id="a13a2-147">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a13a2-147">Next steps</span></span>
<span data-ttu-id="a13a2-148">toolearn como toouse CLI do Azure toomanage nova máquina virtual, consulte [comandos de CLI do Azure para hello Azure Resource Manager](../azure-cli-arm-commands.md).</span><span class="sxs-lookup"><span data-stu-id="a13a2-148">toolearn how toouse Azure CLI toomanage your new virtual machine, see [Azure CLI commands for hello Azure Resource Manager](../azure-cli-arm-commands.md).</span></span>

