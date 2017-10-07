---
title: "aaaConvert uma máquina virtual do Linux no Azure de não discos toomanaged discos - Azure gerenciados | Microsoft Docs"
description: "Como tooconvert uma VM do Linux de discos não gerenciado toomanaged discos usando 2.0 do CLI do Azure no modelo de implantação do Gerenciador de recursos de saudação"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 06/23/2017
ms.author: iainfou
ms.openlocfilehash: 1b94da11deab46f344e28ab4491cf220506b6347
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="convert-a-linux-virtual-machine-from-unmanaged-disks-toomanaged-disks"></a>Converter uma máquina virtual Linux de discos de toomanaged de discos não gerenciado

Se você tiver existente Linux (máquinas virtuais) que usa discos não gerenciados, você pode converter Olá VMs toouse gerenciado discos por meio de saudação [discos gerenciado do Azure](../windows/managed-disks-overview.md) serviço. Esse processo converte disco Olá SO e discos de dados anexado.

Este artigo mostra como tooconvert VMs usando Olá CLI do Azure. Se você precisa tooinstall ou atualizá-lo, consulte [instalar o Azure CLI 2.0](/cli/azure/install-azure-cli). 

## <a name="before-you-begin"></a>Antes de começar

[!INCLUDE [virtual-machines-common-convert-disks-considerations](../../../includes/virtual-machines-common-convert-disks-considerations.md)]


## <a name="convert-single-instance-vms"></a>Converter VMs de instância única
Esta seção aborda como VMs do Azure de não gerenciado de instância única de tooconvert discos toomanaged discos. (Se suas VMs estiverem em um conjunto de disponibilidade, consulte Olá próxima seção.) Você pode usar esse processo tooconvert Olá VMs a partir de discos de toopremium gerenciado discos premium (SSD) não gerenciado ou padrão (HDD) não gerenciados discos toostandard gerenciado discos.

1. Desalocar Olá VM usando [az vm desalocar](/cli/azure/vm#deallocate). exemplo a seguir Hello desaloca Olá VM denominada `myVM` no grupo de recursos de saudação chamado `myResourceGroup`:

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

2. Converter os discos de toomanaged VM hello usando [az vm converter](/cli/azure/vm#convert). Olá seguindo o processo converte Olá VM denominada `myVM`, incluindo disco Olá SO e discos de dados:

    ```azurecli
    az vm convert --resource-group myResourceGroup --name myVM
    ```

3. Iniciar Olá VM depois de discos do hello conversão toomanaged usando [início de vm az](/cli/azure/vm#start). Olá inicia de exemplo a seguir Olá VM denominada `myVM` no grupo de recursos de saudação denominado `myResourceGroup`.

    ```azurecli
    az vm start --resource-group myResourceGroup --name myVM
    ```

## <a name="convert-vms-in-an-availability-set"></a>Converter VMs em um conjunto de disponibilidade

Se Olá VMs que você deseja tooconvert toomanaged discos estão em um conjunto de disponibilidade, é necessário primeiro conjunto de disponibilidade do tooconvert Olá tooa gerenciado conjunto de disponibilidade.

Todas as VMs no conjunto de disponibilidade Olá devem ser desalocadas antes de converter o conjunto de disponibilidade de saudação. Plano tooconvert todos os discos de toomanaged VMs após a disponibilidade de saudação definido foi convertido tooa gerenciado conjunto de disponibilidade. Em seguida, inicie todas as VMs hello e continuar a operar normalmente.

1. Liste todas as VMs em um conjunto de disponibilidade usando [az vm availability-set list](/cli/azure/vm/availability-set#list). Olá exemplo a seguir lista todas as VMs no conjunto nomeada de disponibilidade de saudação `myAvailabilitySet` no grupo de recursos de saudação chamado `myResourceGroup`:

    ```azurecli
    az vm availability-set show \
        --resource-group myResourceGroup \
        --name myAvailabilitySet \
        --query [virtualMachines[*].id] \
        --output table
    ```

2. Desalocar todas as VMs hello usando [az vm desalocar](/cli/azure/vm#deallocate). exemplo a seguir Hello desaloca Olá VM denominada `myVM` no grupo de recursos de saudação chamado `myResourceGroup`:

    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    ```

3. Converter a disponibilidade de saudação definida por meio de [converter de conjunto de disponibilidade de vm az](/cli/azure/vm/availability-set#convert). Olá, exemplo a seguir converte conjunto nomeada de disponibilidade de saudação `myAvailabilitySet` no grupo de recursos de saudação chamado `myResourceGroup`:

    ```azurecli
    az vm availability-set convert \
        --resource-group myResourceGroup \
        --name myAvailabilitySet
    ```

4. Converter todos os discos do hello VMs toomanaged usando [az vm converter](/cli/azure/vm#convert). Olá seguindo o processo converte Olá VM denominada `myVM`, incluindo disco Olá SO e discos de dados:

    ```azurecli
    az vm convert --resource-group myResourceGroup --name myVM
    ```

5. Iniciar todas as VMs Olá após discos de toomanaged conversão hello usando [início de vm az](/cli/azure/vm#start). Olá inicia de exemplo a seguir Olá VM denominada `myVM` no grupo de recursos de saudação chamado `myResourceGroup`:

    ```azurecli
    az vm start --resource-group myResourceGroup --name myVM
    ```

## <a name="next-steps"></a>Próximas etapas
Para saber mais sobre as opções de armazenamento, confira a [Visão geral dos Azure Managed Disks](../windows/managed-disks-overview.md).
