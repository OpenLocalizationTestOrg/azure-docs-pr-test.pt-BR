---
title: Criar e copiar da sua VM Linux com a CLI do Azure 1.0 | Microsoft Docs
description: "Saiba como criar uma cópia de sua máquina virtual Linux do Azure com a CLI do Azure 1.0 no modelo de implantação do Resource Manager"
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
ms.openlocfilehash: 62ae54f3596c9383cbf3b401fcfdb42ecfdee63c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-copy-of-a-linux-virtual-machine-running-on-azure-with-the-azure-cli-10"></a><span data-ttu-id="bfc78-103">Criar uma cópia de uma máquina virtual Linux em execução no Azure com a CLI do Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="bfc78-103">Create a copy of a Linux virtual machine running on Azure with the Azure CLI 1.0</span></span>
<span data-ttu-id="bfc78-104">Este artigo mostra como criar uma cópia de sua VM (máquina virtual) do Azure executando o Linux no modelo de implantação do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="bfc78-104">This article shows you how to create a copy of your Azure virtual machine (VM) running Linux using the Resource Manager deployment model.</span></span> <span data-ttu-id="bfc78-105">Primeiro, você copia o sistema operacional e os discos de dados para um novo contêiner e, em seguida, configura os recursos de rede para criar a nova máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="bfc78-105">First you copy over the operating system and data disks to a new container, then set up the network resources and create the new virtual machine.</span></span>

<span data-ttu-id="bfc78-106">Você também pode [carregar e criar uma VM com base em uma imagem de disco personalizada](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="bfc78-106">You can also [upload and create a VM from custom disk image](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="bfc78-107">Versões da CLI para concluir a tarefa</span><span class="sxs-lookup"><span data-stu-id="bfc78-107">CLI versions to complete the task</span></span>
<span data-ttu-id="bfc78-108">Você pode concluir a tarefa usando uma das seguintes versões da CLI:</span><span class="sxs-lookup"><span data-stu-id="bfc78-108">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="bfc78-109">CLI 1.0 do Azure – nossa CLI para os modelos de implantação clássico e de gerenciamento de recursos (este artigo)</span><span class="sxs-lookup"><span data-stu-id="bfc78-109">Azure CLI 1.0 – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="bfc78-110">[CLI 2.0 do Azure](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) – nossa última geração de CLI para o modelo de implantação de gerenciamento de recursos</span><span class="sxs-lookup"><span data-stu-id="bfc78-110">[Azure CLI 2.0](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="bfc78-111">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="bfc78-111">Before you begin</span></span>
<span data-ttu-id="bfc78-112">Verifique se você atende os seguintes pré-requisitos antes de iniciar as etapas:</span><span class="sxs-lookup"><span data-stu-id="bfc78-112">Ensure that you meet the following prerequisites before you start the steps:</span></span>

* <span data-ttu-id="bfc78-113">Você tem a [CLI do Azure](../../cli-install-nodejs.md) baixada e instalada em seu computador.</span><span class="sxs-lookup"><span data-stu-id="bfc78-113">You have the [Azure CLI](../../cli-install-nodejs.md) downloaded and installed on your machine.</span></span> 
* <span data-ttu-id="bfc78-114">Você também precisa de algumas informações sobre sua VM Linux do Azure existente:</span><span class="sxs-lookup"><span data-stu-id="bfc78-114">You also need some information about your existing Azure Linux VM:</span></span>

| <span data-ttu-id="bfc78-115">Informações sobre a VM de origem</span><span class="sxs-lookup"><span data-stu-id="bfc78-115">Source VM information</span></span> | <span data-ttu-id="bfc78-116">Onde obter</span><span class="sxs-lookup"><span data-stu-id="bfc78-116">Where to get it</span></span> |
| --- | --- |
| <span data-ttu-id="bfc78-117">Nome da VM</span><span class="sxs-lookup"><span data-stu-id="bfc78-117">VM name</span></span> |`azure vm list` |
| <span data-ttu-id="bfc78-118">Nome do Grupo de Recursos</span><span class="sxs-lookup"><span data-stu-id="bfc78-118">Resource Group name</span></span> |`azure vm list` |
| <span data-ttu-id="bfc78-119">Local</span><span class="sxs-lookup"><span data-stu-id="bfc78-119">Location</span></span> |`azure vm list` |
| <span data-ttu-id="bfc78-120">Nome da Conta de Armazenamento</span><span class="sxs-lookup"><span data-stu-id="bfc78-120">Storage Account name</span></span> |`azure storage account list -g <resourceGroup>` |
| <span data-ttu-id="bfc78-121">Nome do contêiner</span><span class="sxs-lookup"><span data-stu-id="bfc78-121">Container name</span></span> |`azure storage container list -a <sourcestorageaccountname>` |
| <span data-ttu-id="bfc78-122">Nome do arquivo VHD da VM de origem</span><span class="sxs-lookup"><span data-stu-id="bfc78-122">Source VM VHD file name</span></span> |`azure storage blob list --container <containerName>` |

* <span data-ttu-id="bfc78-123">Você precisará fazer algumas escolhas quanto a sua nova VM:    </span><span class="sxs-lookup"><span data-stu-id="bfc78-123">You will need to make some choices about your new VM:    </span></span><br> <span data-ttu-id="bfc78-124">-Nome do contêiner    </span><span class="sxs-lookup"><span data-stu-id="bfc78-124">-Container name    </span></span><br> <span data-ttu-id="bfc78-125">-Nome da VM    </span><span class="sxs-lookup"><span data-stu-id="bfc78-125">-VM name    </span></span><br> <span data-ttu-id="bfc78-126">-Tamanho da VM    </span><span class="sxs-lookup"><span data-stu-id="bfc78-126">-VM size    </span></span><br> <span data-ttu-id="bfc78-127">-Nome da VNet    </span><span class="sxs-lookup"><span data-stu-id="bfc78-127">-vNet name    </span></span><br> <span data-ttu-id="bfc78-128">-Nome da sub-rede    </span><span class="sxs-lookup"><span data-stu-id="bfc78-128">-SubNet name    </span></span><br> <span data-ttu-id="bfc78-129">-Nome IP    </span><span class="sxs-lookup"><span data-stu-id="bfc78-129">-IP Name    </span></span><br> <span data-ttu-id="bfc78-130">-Nome da NIC</span><span class="sxs-lookup"><span data-stu-id="bfc78-130">-NIC name</span></span>

## <a name="login-and-set-your-subscription"></a><span data-ttu-id="bfc78-131">Faça logon e configure sua assinatura</span><span class="sxs-lookup"><span data-stu-id="bfc78-131">Login and set your subscription</span></span>
1. <span data-ttu-id="bfc78-132">Faça logon na CLI.</span><span class="sxs-lookup"><span data-stu-id="bfc78-132">Login to the CLI.</span></span>

    ```azurecli
    azure login
    ```
2. <span data-ttu-id="bfc78-133">Certifique-se de estar no modo Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="bfc78-133">Make sure you are in Resource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```
3. <span data-ttu-id="bfc78-134">Configure a assinatura correta.</span><span class="sxs-lookup"><span data-stu-id="bfc78-134">Set the correct subscription.</span></span> <span data-ttu-id="bfc78-135">Você pode usar “azure account list” para ver todas as suas assinaturas.</span><span class="sxs-lookup"><span data-stu-id="bfc78-135">You can use 'azure account list' to see all of your subscriptions.</span></span>

    ```azurecli
    azure account set mySubscriptionID
    ```

## <a name="stop-the-vm"></a><span data-ttu-id="bfc78-136">Pare a VM.</span><span class="sxs-lookup"><span data-stu-id="bfc78-136">Stop the VM</span></span>
<span data-ttu-id="bfc78-137">Pare e desaloque a VM de origem.</span><span class="sxs-lookup"><span data-stu-id="bfc78-137">Stop and deallocate the source VM.</span></span> <span data-ttu-id="bfc78-138">Você pode usar “azure vm list” para obter uma lista de todas as VMs em sua assinatura e os nomes de seus grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="bfc78-138">You can use 'azure vm list' to get a list of all of the VMs in your subscription and their resource group names.</span></span>

```azurecli
azure vm stop myResourceGroup myVM
azure vm deallocate myResourceGroup MyVM
```


## <a name="copy-the-vhd"></a><span data-ttu-id="bfc78-139">Copie o VHD</span><span class="sxs-lookup"><span data-stu-id="bfc78-139">Copy the VHD</span></span>
<span data-ttu-id="bfc78-140">Você pode copiar o VHD do armazenamento de origem para o destino usando o `azure storage blob copy start`.</span><span class="sxs-lookup"><span data-stu-id="bfc78-140">You can copy the VHD from the source storage to the destination using the `azure storage blob copy start`.</span></span> <span data-ttu-id="bfc78-141">Neste exemplo, vamos copiar o VHD para a mesma conta de armazenamento, mas para um contêiner diferente.</span><span class="sxs-lookup"><span data-stu-id="bfc78-141">In this example, we are going to copy the VHD to the same storage account, but a different container.</span></span>

<span data-ttu-id="bfc78-142">Para copiar o VHD para outro contêiner na mesma conta de armazenamento, digite:</span><span class="sxs-lookup"><span data-stu-id="bfc78-142">To copy the VHD to another container in the same storage account, type:</span></span>

```azurecli
azure storage blob copy start \
        https://mystorageaccountname.blob.core.windows.net:8080/mycontainername/myVHD.vhd \
        myNewContainerName
```

## <a name="set-up-the-virtual-network-for-your-new-vm"></a><span data-ttu-id="bfc78-143">Configure a rede virtual para sua nova VM</span><span class="sxs-lookup"><span data-stu-id="bfc78-143">Set up the virtual network for your new VM</span></span>
<span data-ttu-id="bfc78-144">Configure uma rede virtual e NIC para sua nova VM.</span><span class="sxs-lookup"><span data-stu-id="bfc78-144">Set up a virtual network and NIC for your new VM.</span></span> 

```azurecli
azure network vnet create myResourceGroup myVnet -l myLocation

azure network vnet subnet create -a <address.prefix.in.CIDR/format> myResourceGroup myVnet mySubnet

azure network public-ip create myResourceGroup myPublicIP -l myLocation

azure network nic create myResourceGroup myNic -k mySubnet -m myVnet -p myPublicIP -l myLocation
```


## <a name="create-the-new-vm"></a><span data-ttu-id="bfc78-145">Crie a nova VM</span><span class="sxs-lookup"><span data-stu-id="bfc78-145">Create the new VM</span></span>
<span data-ttu-id="bfc78-146">Agora, você pode criar uma VM com base no disco virtual carregado [usando um modelo do Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd) ou por meio da CLI, especificando o URI para seu disco copiado digitando:</span><span class="sxs-lookup"><span data-stu-id="bfc78-146">You can now create a VM from your uploaded virtual disk [using a resource manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd) or through the CLI by specifying the URI to your copied disk by typing:</span></span>

```azurecli
azure vm create -n myVM -l myLocation -g myResourceGroup -f myNic \
        -z Standard_DS1_v2 -y Linux \
        https://mystorageaccountname.blob.core.windows.net:8080/mycontainername/myVHD.vhd 
```



## <a name="next-steps"></a><span data-ttu-id="bfc78-147">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="bfc78-147">Next steps</span></span>
<span data-ttu-id="bfc78-148">Para saber como usar a CLI do Azure para gerenciar sua nova máquina virtual, consulte [Comandos da CLI do Azure para o Azure Resource Manager](../azure-cli-arm-commands.md).</span><span class="sxs-lookup"><span data-stu-id="bfc78-148">To learn how to use Azure CLI to manage your new virtual machine, see [Azure CLI commands for the Azure Resource Manager](../azure-cli-arm-commands.md).</span></span>

