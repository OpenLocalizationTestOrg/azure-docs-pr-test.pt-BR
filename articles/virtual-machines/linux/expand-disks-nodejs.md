---
title: disco aaaExpand SO na VM do Linux com hello 1.0 da CLI do Azure | Microsoft Docs
description: "Saiba como tooexpand Olá disco virtual do sistema operacional (SO) em uma VM do Linux usando hello Azure CLI 1.0 e o modelo de implantação do Gerenciador de recursos de saudação"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 0db78c0b86b48b2c5358611e11bb0b7ad781a559
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="expand-os-disk-on-a-linux-vm-using-hello-azure-cli-with-hello-azure-cli-10"></a>Expanda o disco do sistema operacional em uma VM do Linux usando Olá CLI do Azure com hello 1.0 da CLI do Azure
tamanho de disco rígido virtual saudação padrão para o sistema operacional de saudação (SO) normalmente é 30 GB em uma máquina virtual do Linux (VM) no Azure. Você pode [adicionar discos de dados](add-disk.md) tooprovide para espaço de armazenamento adicional, mas você também poderá tooexpand disco de saudação sistema operacional. Este artigo fornece detalhes sobre como tooexpand Olá SO de disco para uma VM do Linux usando discos gerenciados por hello 1.0 da CLI do Azure.

## <a name="cli-versions-toocomplete-hello-task"></a>Tarefa de saudação do CLI versões toocomplete
Você pode concluir a tarefa hello usando uma saudação versões da CLI a seguir:

- [1.0 de CLI do Azure](#prerequisites) – nosso CLI para Olá clássico e o recurso de gerenciamento modelos de implantação (Este artigo)
- [2.0 do CLI do Azure](expand-disks.md) -nossa próxima geração CLI para o modelo de implantação do gerenciamento de recursos de saudação

## <a name="prerequisites"></a>Pré-requisitos
Você precisa Olá [1.0 mais recente de CLI do Azure](../../cli-install-nodejs.md) instalado e registrado no tooan [conta do Azure](https://azure.microsoft.com/pricing/free-trial/) usando o modo do Gerenciador de recursos de saudação da seguinte maneira:

```azurecli
azure config mode arm
```

Em Olá exemplos a seguir, substitua os nomes de parâmetro de exemplo com seus próprios valores. Os nomes de parâmetro de exemplo incluem *myResourceGroup* e *myVM*.

## <a name="expand-os-disk"></a>Expandir o disco do sistema operacional

1. Não é possível executar operações em discos rígidos virtuais com hello VM em execução. Olá exemplo a seguir interrompe e desaloca Olá VM denominada *myVM* no grupo de recursos de saudação denominado *myResourceGroup*:

    ```azurecli
    azure vm deallocate --resource-group myResourceGroup --name myVM
    ```

    > [!NOTE]
    > `azure vm stop`não liberar recursos de computação de saudação. toorelease recursos de computação, use `azure vm deallocate`. Olá VM deve ser desalocada tooexpand saudação do disco rígido virtual.

2. Atualizar Olá tamanho do disco do sistema operacional Olá não gerenciado usando Olá `azure vm set` comando. Olá atualizações de exemplo a seguir Olá VM denominada *myVM* no grupo de recursos de saudação denominado *myResourceGroup* toobe *50* GB:

    ```azurecli
    azure vm set \
        --resource-group myResourceGroup \
        --name myVM \
        --new-os-disk-size 50
    ```

3. Inicie a VM da seguinte maneira:

    ```azurecli
    azure vm start --resource-group myResourceGroup --name myVM
    ```

4. SSH tooyour VM com as credenciais apropriadas hello. disco de SO de saudação tooverify foi redimensionado, use `df -h`. Olá saída de exemplo a seguir mostra a partição primária hello (*/desenvolvimento/sda1*) agora é 50 GB:

    ```bash
    Filesystem      Size  Used Avail Use% Mounted on
    udev            1.7G     0  1.7G   0% /dev
    tmpfs           344M  5.0M  340M   2% /run
    /dev/sda1        49G  1.3G   48G   3% /
    ```

## <a name="next-steps"></a>Próximas etapas
Se você precisar de armazenamento adicional, você também [adicionar discos de dados tooa VM Linux](add-disk.md). Para obter mais informações sobre criptografia de disco, consulte [Olá criptografar discos em uma VM do Linux usando a CLI do Azure](encrypt-disks.md).
