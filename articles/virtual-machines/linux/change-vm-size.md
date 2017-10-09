---
title: aaaHow tooresize uma VM do Linux com hello 2.0 do CLI do Azure | Microsoft Docs
description: "Como a escala para baixo de uma máquina virtual Linux, alterando ou tooscale backup Olá tamanho da VM."
services: virtual-machines-linux
documentationcenter: na
author: mikewasson
manager: timlt
editor: 
tags: 
ms.assetid: e163f878-b919-45c5-9f5a-75a64f3b14a0
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/10/2017
ms.author: mwasson
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e8fba485b5bcc7824f546de5cf3df77624a28008
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="resize-a-linux-virtual-machine-using-cli-20"></a>Redimensionar uma máquina virtual do Linux usando a CLI 2.0

Depois de provisionar uma máquina virtual (VM), você pode expandir ou reduzir Olá VM alterando Olá [tamanho da VM][vm-sizes]. Em alguns casos, você deverá desalocar Olá VM pela primeira vez. É necessário toodeallocate Olá VM se Olá desejado de tamanho não está disponível no cluster de hardware de saudação que está hospedando o hello VM. Este artigo fornece detalhes sobre como tooresize uma VM do Linux com hello 2.0 do CLI do Azure. Você também pode executar essas etapas com hello [Azure CLI 1.0](change-vm-size-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="resize-a-vm"></a>Redimensionar uma VM
tooresize uma VM, você precisa hello mais recente [2.0 do CLI do Azure](/cli/azure/install-az-cli2) instalado e conectado através de conta do Azure tooan [logon az](/cli/azure/#login).

1. Tamanhos de exibir a lista de saudação de VM disponível no cluster de hardware Olá onde Olá VM for hospedado com [az vm lista-vm--opções de redimensionamento](/cli/azure/vm#list-vm-resize-options). Olá, exemplo a seguir lista os tamanhos de VM para Olá VM denominada `myVM` no grupo de recursos de saudação `myResourceGroup` região:
   
    ```azurecli
    az vm list-vm-resize-options --resource-group myResourceGroup --name myVM --output table
    ```

2. Se Olá desejado que o tamanho da VM está listado, redimensionar Olá VM com [az vm redimensionar](/cli/azure/vm#resize). Olá redimensiona de exemplo a seguir Olá VM denominada `myVM` toohello `Standard_DS3_v2` tamanho:
   
    ```azurecli
    az vm resize --resource-group myResourceGroup --name myVM --size Standard_DS3_v2
    ```
   
    Olá VM é reiniciado durante esse processo. Após a reinicialização de saudação, seu sistema operacional existente e os discos de dados são remapeados. Tudo em disco temporário Olá será perdido.

3. Se Olá desejado tamanho da VM não estiver listado, você precisa toofirst desalocar Olá VM com [az vm desalocar](/cli/azure/vm#deallocate). Esse processo permite Olá VM toothen ser redimensionado tooany tamanho disponível Olá suporta de região e, em seguida, iniciado. Olá etapas a seguir desalocar, redimensionar e, em seguida, iniciar Olá VM denominada `myVM` no grupo de recursos de saudação chamado `myResourceGroup`:
   
    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    az vm resize --resource-group myResourceGroup --name myVM --size Standard_DS3_v2
    az vm start --resource-group myResourceGroup --name myVM
    ```
   
   > [!WARNING]
   > Olá ao desalocar VM também libera os endereços IP dinâmicos atribuídos toohello VM. Olá SO e discos de dados não são afetados.

## <a name="next-steps"></a>Próximas etapas
Para obter escalabilidade adicional, execute várias instâncias de VM e expanda. Para obter mais informações, consulte [Dimensionar automaticamente computadores Linux em um conjunto de dimensionamento de máquinas virtuais][scale-set]. 

<!-- links -->
[boot-diagnostics]: https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/
[scale-set]: ../../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md 
[vm-sizes]:sizes.md
