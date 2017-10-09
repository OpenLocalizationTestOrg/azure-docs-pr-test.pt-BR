---
title: "aaaExpand de discos rígidos virtuais em uma VM do Linux no Azure | Microsoft Docs"
description: "Saiba como tooexpand de discos rígidos virtuais em uma VM do Linux com hello 2.0 do CLI do Azure"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/21/2017
ms.author: iainfou
ms.openlocfilehash: 7c09a682cb4322c027e57667640e8f1f8e6612f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooexpand-virtual-hard-disks-on-a-linux-vm-with-hello-azure-cli"></a>Como tooexpand de discos rígidos virtuais em uma VM do Linux com hello CLI do Azure
tamanho de disco rígido virtual saudação padrão para o sistema operacional de saudação (SO) normalmente é 30 GB em uma máquina virtual do Linux (VM) no Azure. Você pode [adicionar discos de dados](add-disk.md) tooprovide para espaço de armazenamento adicional, mas você também poderá tooexpand um disco de dados existente. Este artigo fornece detalhes sobre como tooexpand discos gerenciado para uma VM do Linux com hello 2.0 do CLI do Azure. Você também pode expandir o disco do sistema operacional não gerenciado de saudação com hello [Azure CLI 1.0](expand-disks-nodejs.md).

> [!WARNING]
> Certifique-se sempre de fazer backup dos dados antes de realizar operações de redimensionamento do disco. Para saber mais, confira [Fazer backup de máquinas virtuais do Linux no Azure](tutorial-backup-vms.md).

## <a name="expand-disk"></a>Expandir disco
Certifique-se de que você tenha mais recente Olá [2.0 do CLI do Azure](/cli/azure/install-az-cli2) instalado e conectado através de conta do Azure tooan [logon az](/cli/azure/#login).

Este artigo requer uma VM existente no Azure com, pelo menos, um disco de dados anexado e preparado. Caso ainda não tenha uma VM que possa ser usada, confira [Criar e preparar uma VM com discos de dados](tutorial-manage-disks.md#create-and-attach-disks).

Em Olá exemplos a seguir, substitua os nomes de parâmetro de exemplo com seus próprios valores. Os nomes de parâmetro de exemplo incluem *myResourceGroup* e *myVM*.

1. Não é possível executar operações em discos rígidos virtuais com hello VM em execução. Desaloque a VM com [az vm deallocate](/cli/azure/vm#deallocate). exemplo a seguir Hello desaloca Olá VM denominada *myVM* no grupo de recursos de saudação denominado *myResourceGroup*:

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

    > [!NOTE]
    > `az vm stop`não liberar recursos de computação de saudação. toorelease recursos de computação, use `az vm deallocate`. Olá VM deve ser desalocada tooexpand saudação do disco rígido virtual.

2. Veja uma lista de discos gerenciados em um grupo de recursos com [az disk list](/cli/azure/disk#list). Olá exemplo a seguir exibe uma lista de discos gerenciados no grupo de recursos de saudação denominado *myResourceGroup*:

    ```azurecli
    az disk list \
        --resource-group myResourceGroup \
        --query '[*].{Name:name,Gb:diskSizeGb,Tier:accountType}' \
        --output table
    ```

    Expandir disco necessária de saudação com [atualização de disco az](/cli/azure/disk#update). exemplo a seguir Hello expande chamado de disco gerenciado do hello *myDataDisk* toobe *200*Gb de tamanho:

    ```azurecli
    az disk update \
        --resource-group myResourceGroup \
        --name myDataDisk \
        --size-gb 200
    ```

    > [!NOTE]
    > Quando você expande um disco gerenciado, o tamanho de Olá atualizado é mapeada toohello mais próximo do tamanho de disco gerenciado. Para uma tabela de tamanhos de disco gerenciado disponível hello e camadas, consulte [gerenciados discos visão geral do Azure - preços e faturamento](../windows/managed-disks-overview.md#pricing-and-billing).

3. Inicie a VM com [az vm start](/cli/azure/vm#start). Olá inicia de exemplo a seguir Olá VM denominada *myVM* no grupo de recursos de saudação denominado *myResourceGroup*:

    ```azurecli
    az vm start --resource-group myResourceGroup --name myVM
    ```

4. SSH tooyour VM com as credenciais apropriadas hello. Você pode obter o endereço IP público de saudação da VM com [Mostrar de vm az](/cli/azure/vm#show):

    ```azurecli
    az vm show --resource-group myResourceGroup --name myVM -d --query [publicIps] --o tsv
    ```

5. Olá toouse expandido em disco, é necessário filesystem e partição do tooexpand Olá subjacente.

    a. Se já estiver montado, desmonte disco hello:

    ```bash
    sudo umount /dev/sdc1
    ```

    b. Use `parted` tooview informações do disco e redimensionar a partição hello:

    ```bash
    sudo parted /dev/sdc
    ```

    Exibir informações sobre o layout de partição existente Olá com `print`. saudação de saída é semelhante toohello exemplo, que mostra o disco subjacente Olá tem 215Gb a seguir:

    ```bash
    GNU Parted 3.2
    Using /dev/sdc1
    Welcome tooGNU Parted! Type 'help' tooview a list of commands.
    (parted) print
    Model: Unknown Msft Virtual Disk (scsi)
    Disk /dev/sdc1: 215GB
    Sector size (logical/physical): 512B/4096B
    Partition Table: loop
    Disk Flags:
    
    Number  Start  End    Size   File system  Flags
        1      0.00B  107GB  107GB  ext4
    ```

    c. Expanda a partição de saudação com `resizepart`. Insira o número de partição Olá *1*e um tamanho para a nova partição de saudação:

    ```bash
    (parted) resizepart
    Partition number? 1
    End?  [107GB]? 215GB
    ```

    d. tooexit, digite`quit`

5. Partição Olá redimensionado, verificar a consistência de partição de saudação com `e2fsck`:

    ```bash
    sudo e2fsck -f /dev/sdc1
    ```

6. Redimensionar agora Olá filesystem com `resize2fs`:

    ```bash
    sudo resize2fs /dev/sdc1
    ```

7. Montagem Olá partição toohello desejado local, como `/datadrive`:

    ```bash
    sudo mount /dev/sdc1 /datadrive
    ```

8. disco de SO de saudação tooverify foi redimensionado, use `df -h`. Olá saída de exemplo a seguir mostra a unidade de dados hello, */desenvolvimento/sdc1*, agora é de 200 GB:

    ```bash
    Filesystem      Size   Used  Avail Use% Mounted on
    /dev/sdc1        197G   60M   187G   1% /datadrive
    ```

## <a name="next-steps"></a>Próximas etapas
Se você precisar de armazenamento adicional, você também [adicionar discos de dados tooa VM Linux](add-disk.md). Para obter mais informações sobre criptografia de disco, consulte [Olá criptografar discos em uma VM do Linux usando a CLI do Azure](encrypt-disks.md).
