---
title: aaaCopy uma VM do Linux usando o Azure CLI 2.0 | Microsoft Docs
description: "Saiba como toocreate uma cópia da VM Azure Linux usando o Azure CLI 2.0 e discos gerenciados."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
tags: azure-resource-manager
ms.assetid: 770569d2-23c1-4a5b-801e-cddcd1375164
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 03/10/2017
ms.author: cynthn
ms.openlocfilehash: ee34a4259dd0c1e7bf49312fe3fe3ba809bf69e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-copy-of-a-linux-vm-by-using-azure-cli-20-and-managed-disks"></a>Criar uma cópia da sua VM Linux usando a CLI do Azure 2.0 e Managed Disks


Este artigo mostra como toocreate uma cópia de sua máquina virtual do Azure (VM) executando o Linux usando Olá 2.0 do CLI do Azure e o modelo de implantação do Azure Resource Manager hello. Você também pode executar essas etapas com hello [Azure CLI 1.0](copy-vm-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Você também pode [carregar e criar uma VM com base em um VHD](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="prerequisites"></a>Pré-requisitos


-   Instalar a [CLI do Azure 2.0](/cli/azure/install-az-cli2)

-   Entrar tooan conta do Azure com [logon az](/cli/azure/#login).

-   Têm um toouse de VM do Azure como origem de saudação de sua cópia.

## <a name="step-1-stop-hello-source-vm"></a>Etapa 1: Interromper a VM de origem Olá


Desalocar a VM de origem hello usando [az vm desalocar](/cli/azure/vm#deallocate).
exemplo a seguir Hello desaloca Olá VM denominada **myVM** no grupo de recursos de saudação **myResourceGroup**:

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

## <a name="step-2-copy-hello-source-vm"></a>Etapa 2: Copiar a VM de origem Olá


toocopy uma VM, criar uma cópia da saudação subjacente do disco rígido virtual. Esse processo cria um VHD especializado como um disco gerenciado que contém Olá mesma configuração e definições como Olá VM de origem.

Para saber mais sobre Azure Managed Disks, veja [Visão geral dos Azure Managed Disks](../windows/managed-disks-overview.md). 

1.  Lista cada VM e Olá o nome do seu disco do sistema operacional com [lista de vm az](/cli/azure/vm#list). Olá, exemplo a seguir lista todas as VMs no grupo de recursos denominado **myResourceGroup**:
    
    ```azurecli
    az vm list -g myTestRG --query '[].{Name:name,DiskName:storageProfile.osDisk.name}' --output table
    ```

    saudação de saída é similar toohello exemplo a seguir:

    ```azurecli
    Name    DiskName
    ------  --------
    myVM    myDisk
    ```

1.  Copiar o disco de hello, criando um novo gerenciados usando o disco [criar disco az](/cli/azure/disk#create). Olá, exemplo a seguir cria um disco chamado **myCopiedDisk** de saudação gerenciados disco chamado **myDisk**:

    ```azurecli
    az disk create --resource-group myResourceGroup --name myCopiedDisk --source myDisk
    ``` 

1.  Verificar discos Olá gerenciado em seu grupo de recursos usando [lista de discos az](/cli/azure/disk#list). Olá, exemplo a seguir lista discos Olá gerenciado no grupo de recursos de saudação denominado **myResourceGroup**:

    ```azurecli
    az disk list --resource-group myResourceGroup --output table
    ```

1.  Ignorar muito["etapa 3: configurar uma rede virtual"](#step-3-set-up-a-virtual-network).


## <a name="step-3-set-up-a-virtual-network"></a>Etapa 3: configurar uma rede virtual


Olá opcionais etapas a seguir criam uma nova rede virtual, a sub-rede, o endereço IP público e a placa de interface de rede virtual (NIC).

Se você estiver copiando uma VM para fins ou implantações adicionais de solução de problemas, convém não toouse uma VM em uma rede virtual existente.

Se você quiser toocreate uma infraestrutura de rede virtual para suas VMs copiados, siga lado Olá algumas etapas. Se você não quiser toocreate uma rede virtual, ignore muito[etapa 4: criar uma VM](#step-4-create-a-vm).

1.  Criar rede virtual hello usando [criar redes de rede az](/cli/azure/network/vnet#create). Olá, exemplo a seguir cria uma rede virtual denominada **myVnet** e uma sub-rede denominada **mySubnet**:

    ```azurecli
    az network vnet create --resource-group myResourceGroup --location westus --name myVnet \
        --address-prefix 192.168.0.0/16 --subnet-name mySubnet --subnet-prefix 192.168.1.0/24
    ```

1.  Crie um IP público usando [az network public-ip create](/cli/azure/network/public-ip#create). Olá, exemplo a seguir cria um IP público denominado **myPublicIP** com nome DNS de saudação do **mypublicdns**. (o nome DNS Olá deve ser exclusivo, portanto, forneça um nome exclusivo.)

    ```azurecli
    az network public-ip create --resource-group myResourceGroup --location westus \
        --name myPublicIP --dns-name mypublicdns --allocation-method static --idle-timeout 4
    ```

1.  Criar hello NIC usando [nic da rede az criar](/cli/azure/network/nic#create).
    Olá, exemplo a seguir cria uma NIC denominada **myNic** toothe anexado que **mySubnet** sub-rede:

    ```azurecli
    az network nic create --resource-group myResourceGroup --location westus --name myNic \
        --vnet-name myVnet --subnet mySubnet --public-ip-address myPublicIP
    ```

## <a name="step-4-create-a-vm"></a>Etapa 4: criar uma VM

Não é possível criar uma VM usando [az vm create](/cli/azure/vm#create).

Especificar Olá copiado toouse de disco gerenciado como disco de SO de saudação (– anexar-disco do SO), da seguinte maneira:

```azurecli
az vm create --resource-group myResourceGroup --name myCopiedVM \
    --admin-username azureuser --ssh-key-value ~/.ssh/id_rsa.pub \
    --nics myNic --size Standard_DS1_v2 --os-type Linux \
    --attach-os-disk myCopiedDisk
```

## <a name="next-steps"></a>Próximas etapas

toolearn como toouse CLI do Azure toomanage sua nova VM, consulte [comandos de CLI do Azure para hello Azure Resource Manager](../azure-cli-arm-commands.md).
