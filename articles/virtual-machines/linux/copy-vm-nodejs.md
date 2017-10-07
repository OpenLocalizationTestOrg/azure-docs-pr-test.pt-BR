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
# <a name="create-a-copy-of-a-linux-virtual-machine-running-on-azure-with-hello-azure-cli-10"></a>Criar uma cópia de uma máquina virtual do Linux em execução no Azure com hello 1.0 da CLI do Azure
Este artigo mostra como toocreate uma cópia de sua máquina virtual do Azure (VM) em execução Linux usando Olá modelo de implantação do Gerenciador de recursos. Primeiro copiar sobre o sistema operacional de saudação e dados discos tooa novo contêiner, e em seguida, configurar recursos de rede hello e criar nova máquina de virtual hello.

Você também pode [carregar e criar uma VM com base em uma imagem de disco personalizada](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="cli-versions-toocomplete-hello-task"></a>Tarefa de saudação do CLI versões toocomplete
Você pode concluir a tarefa hello usando uma saudação versões da CLI a seguir:

- CLI do Azure 1.0 – nosso CLI para Olá clássico e o recurso de gerenciamento modelos de implantação (Este artigo)
- [2.0 do CLI do Azure](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -nossa próxima geração CLI para o modelo de implantação do gerenciamento de recursos de saudação

## <a name="before-you-begin"></a>Antes de começar
Certifique-se de que você atenda aos Olá pré-requisitos a seguir antes de começar as etapas de saudação:

* Você tem Olá [CLI do Azure](../../cli-install-nodejs.md) baixado e instalado em seu computador. 
* Você também precisa de algumas informações sobre sua VM Linux do Azure existente:

| Informações sobre a VM de origem | Onde tooget-lo |
| --- | --- |
| Nome da VM |`azure vm list` |
| Nome do Grupo de Recursos |`azure vm list` |
| Local |`azure vm list` |
| Nome da Conta de Armazenamento |`azure storage account list -g <resourceGroup>` |
| Nome do contêiner |`azure storage container list -a <sourcestorageaccountname>` |
| Nome do arquivo VHD da VM de origem |`azure storage blob list --container <containerName>` |

* Você precisará toomake algumas opções sobre a nova VM:   <br> -Nome do contêiner    <br> -Nome da VM    <br> -Tamanho da VM    <br> -Nome da VNet    <br> -Nome da sub-rede    <br> -Nome IP    <br> -Nome da NIC

## <a name="login-and-set-your-subscription"></a>Faça logon e configure sua assinatura
1. Logon toohello CLI.

    ```azurecli
    azure login
    ```
2. Certifique-se de estar no modo Resource Manager.

    ```azurecli
    azure config mode arm
    ```
3. Definir a assinatura correta hello. Você pode usar 'lista de contas do azure' toosee todas as suas assinaturas.

    ```azurecli
    azure account set mySubscriptionID
    ```

## <a name="stop-hello-vm"></a>Parar Olá VM
Parar e desalocar a VM de origem hello. Você pode usar 'lista de vm do azure' tooget uma lista de todas as VMs de saudação em sua assinatura e os nomes de grupo de recursos.

```azurecli
azure vm stop myResourceGroup myVM
azure vm deallocate myResourceGroup MyVM
```


## <a name="copy-hello-vhd"></a>Copiar Olá VHD
Você pode copiar Olá VHD de destino Olá fonte armazenamento toohello usando Olá `azure storage blob copy start`. Neste exemplo, vamos toocopy Olá VHD toohello mesma conta de armazenamento, mas um contêiner diferente.

contêiner de tooanother VHD toocopy Olá no hello mesma conta de armazenamento, digite:

```azurecli
azure storage blob copy start \
        https://mystorageaccountname.blob.core.windows.net:8080/mycontainername/myVHD.vhd \
        myNewContainerName
```

## <a name="set-up-hello-virtual-network-for-your-new-vm"></a>Configurar a rede virtual Olá para sua nova VM
Configure uma rede virtual e NIC para sua nova VM. 

```azurecli
azure network vnet create myResourceGroup myVnet -l myLocation

azure network vnet subnet create -a <address.prefix.in.CIDR/format> myResourceGroup myVnet mySubnet

azure network public-ip create myResourceGroup myPublicIP -l myLocation

azure network nic create myResourceGroup myNic -k mySubnet -m myVnet -p myPublicIP -l myLocation
```


## <a name="create-hello-new-vm"></a>Criar hello nova VM
Agora você pode criar uma máquina virtual do disco virtual carregado [usando um modelo do Gerenciador de recursos](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd) ou por meio de saudação CLI especificando Olá URI tooyour copiados disco digitando:

```azurecli
azure vm create -n myVM -l myLocation -g myResourceGroup -f myNic \
        -z Standard_DS1_v2 -y Linux \
        https://mystorageaccountname.blob.core.windows.net:8080/mycontainername/myVHD.vhd 
```



## <a name="next-steps"></a>Próximas etapas
toolearn como toouse CLI do Azure toomanage nova máquina virtual, consulte [comandos de CLI do Azure para hello Azure Resource Manager](../azure-cli-arm-commands.md).

