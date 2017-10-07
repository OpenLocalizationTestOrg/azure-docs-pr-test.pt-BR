---
title: aaaHow tooresize uma VM do Linux com hello 1.0 da CLI do Azure | Microsoft Docs
description: "Como a escala para baixo de uma máquina virtual Linux, alterando ou tooscale backup Olá tamanho da VM."
services: virtual-machines-linux
documentationcenter: na
author: mikewasson
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/16/2016
ms.author: mwasson
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 43dd955dc2f2dd9d1b2da07ecbfbf2459bcaa4d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="resize-a-linux-vm-with-azure-cli-10"></a>Redimensionar uma VM Linux com a CLI do Azure 1.0

## <a name="overview"></a>Visão geral

Depois de provisionar uma máquina virtual (VM), você pode expandir ou reduzir Olá VM alterando Olá [tamanho da VM][vm-sizes]. Em alguns casos, você deverá desalocar Olá VM pela primeira vez. Isso pode acontecer se o novo tamanho de saudação não está disponível no cluster de hardware de saudação que está hospedando o hello VM.

Este artigo mostra como tooresize uma VM do Linux usando Olá [CLI do Azure][azure-cli].

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="cli-versions-toocomplete-hello-task"></a>Tarefa de saudação do CLI versões toocomplete
Você pode concluir a tarefa hello usando uma saudação versões da CLI a seguir:

- [1.0 de CLI do Azure](#resize-a-linux-vm) – nosso CLI para Olá clássico e o recurso de gerenciamento modelos de implantação (Este artigo)
- [2.0 do CLI do Azure](change-vm-size.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -nossa próxima geração CLI para o modelo de implantação do gerenciamento de recursos de saudação


## <a name="resize-a-linux-vm"></a>Redimensionar uma VM Linux
tooresize uma VM, execute Olá etapas a seguir.

1. Execute Olá CLI comando a seguir. Esse comando lista os tamanhos de VM Olá que estão disponíveis no cluster de hardware Olá onde hello VM está hospedada.
   
    ```azurecli
    azure vm sizes -g myResourceGroup --vm-name myVM
    ```
2. Se Olá desejado tamanho estiver listado, execute Olá Olá tooresize de comando VM a seguir.
   
    ```azurecli
    azure vm set -g myResourceGroup --vm-size <new-vm-size> -n myVM  \
        --enable-boot-diagnostics
        --boot-diagnostics-storage-uri https://mystorageaccount.blob.core.windows.net/ 
    ```
   
    Olá VM será reiniciado durante esse processo. Após a reinicialização de saudação, seu sistema operacional existente e os discos de dados serão remapeados. Tudo em disco temporário hello serão perdido.
   
    Saudação de uso `--enable-boot-diagnostics` opção habilita [diagnósticos de inicialização][boot-diagnostics], toolog qualquer toostartup de erros relacionados.
3. Caso contrário, se Olá desejado tamanho não estiver listado, execute Olá toodeallocate Olá VM, redimensioná-la e, em seguida, reiniciar Olá VM de comandos a seguir.
   
    ```azurecli
    azure vm deallocate -g myResourceGroup myVM
    azure vm set -g myResourceGroup --vm-size <new-vm-size> -n myVM \
        --enable-boot-diagnostics --boot-diagnostics-storage-uri \
        https://mystorageaccount.blob.core.windows.net/ 
    azure vm start -g myResourceGroup myVM
    ```
   
   > [!WARNING]
   > Olá ao desalocar VM também libera os endereços IP dinâmicos atribuídos toohello VM. Olá SO e discos de dados não são afetados.
   > 
   > 

## <a name="next-steps"></a>Próximas etapas
Para obter escalabilidade adicional, execute várias instâncias de VM e expanda. Para obter mais informações, consulte [Dimensionar automaticamente computadores Linux em um conjunto de dimensionamento de máquinas virtuais][scale-set]. 

<!-- links -->

[azure-cli]:../../cli-install-nodejs.md
[boot-diagnostics]: https://azure.microsoft.com/en-us/blog/boot-diagnostics-for-virtual-machines-v2/
[scale-set]: ../../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md 
[vm-sizes]:sizes.md
