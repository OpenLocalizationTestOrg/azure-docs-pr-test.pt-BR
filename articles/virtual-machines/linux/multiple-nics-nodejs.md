---
title: "aaaCreate uma VM do Linux no Azure com várias NICs | Microsoft Docs"
description: "Saiba como toocreate uma VM do Linux com várias NICs anexado tooit usando modelos de saudação CLI do Azure ou o Gerenciador de recursos."
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
ms.openlocfilehash: 457dab734ceeeefd35cddaf1ebb9ea0a82f4e207
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-virtual-machine-with-multiple-nics-using-hello-azure-cli-10"></a>Criar uma máquina virtual Linux com várias NICs usando Olá 1.0 da CLI do Azure
Você pode criar uma máquina virtual (VM) no Azure que tenha vários tooit de interfaces (NICs) conectados a rede virtual. Um cenário comum é toohave várias sub-redes para conectividade de front-end e back-end ou uma rede dedicada tooa monitoramento ou solução de backup. Este artigo fornece comandos rápidos toocreate uma VM com vários tooit de NICs conectadas. Para obter informações detalhadas, incluindo como toocreate várias NICs dentro de sua própria Bash scripts, leia mais sobre [Implantando VMs multi-NIC](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md). Diferentes [tamanhos de VM](sizes.md) dão suporte a um número variável de NICs, sendo assim, dimensione sua VM adequadamente.

> [!WARNING]
> Quando você cria uma VM - não é possível adicionar tooan NICs existentes VM com hello 1.0 da CLI do Azure, você deve anexar várias NICs. Você pode [adicionar NICs tooan existente VM com hello Azure CLI 2.0](multiple-nics.md). Você também pode [criar uma VM com base em discos virtuais original de saudação](copy-vm.md) e crie várias NICs como implantar Olá VM.


## <a name="cli-versions-toocomplete-hello-task"></a>Tarefa de saudação do CLI versões toocomplete
Você pode concluir a tarefa hello usando uma saudação versões da CLI a seguir:

- [1.0 de CLI do Azure](#create-supporting-resources) – nosso CLI para Olá clássico e o recurso de gerenciamento modelos de implantação (Este artigo)
- [2.0 do CLI do Azure](multiple-nics.md) -nossa próxima geração CLI para o modelo de implantação do gerenciamento de recursos de saudação


## <a name="create-supporting-resources"></a>Criar recursos de suporte
Certifique-se de que você tenha Olá [CLI do Azure](../../cli-install-nodejs.md) conectado e usando o modo do Gerenciador de recursos:

```azurecli
azure config mode arm
```

Em Olá exemplos a seguir, substitua os nomes de parâmetro de exemplo com seus próprios valores. Os nomes de parâmetro de exemplo incluem *myResourceGroup*, *mystorageaccount* e *myVM*.

Em primeiro lugar, crie um grupo de recursos. Olá, exemplo a seguir cria um grupo de recursos denominado *myResourceGroup* em Olá *eastus* local:

```azurecli
azure group create myResourceGroup --location eastus
```

Crie suas VMs de um toohold de conta de armazenamento. Olá, exemplo a seguir cria uma conta de armazenamento denominada *mystorageaccount*:

```azurecli
azure storage account create mystorageaccount \
    --resource-group myResourceGroup \
    --location eastus \
    --kind Storage \
    --sku-name PLRS
```

Crie uma rede virtual tooconnect suas VMs. Olá, exemplo a seguir cria uma rede virtual denominada *myVnet* com um prefixo de endereço *192.168.0.0/16*:

```azurecli
azure network vnet create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myVnet \
    --address-prefixes 192.168.0.0/16
```

Crie duas sub-redes da rede virtual – uma para o tráfego de front-end e uma para o tráfego de back-end. Olá, exemplo a seguir cria duas sub-redes, denominados *mySubnetFrontEnd* e *mySubnetBackEnd*:

```azurecli
azure network vnet subnet create \
    --resource-group myResourceGroup \
    --location myVnet \
    --name mySubnetFrontEnd \
    --address-prefix 192.168.1.0/24
azure network vnet subnet create \
    --resource-group myResourceGroup \
    --location myVnet \
    --name mySubnetBackEnd \
    --address-prefix 192.168.2.0/24
```

## <a name="create-and-configure-multiple-nics"></a>Criar e configurar várias NICs
Você pode ler mais detalhes sobre [implantar várias NICs usando Olá CLI do Azure](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md), incluindo o processo de saudação do loop por meio de toocreate todas as NICs de saudação de script.

Olá, exemplo a seguir cria duas NICs, denominadas *myNic1* e *myNic2*, com uma NIC conectam tooeach sub-rede:

```azurecli
azure network nic create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNic1 \
    --subnet-vnet-name myVnet \
    --subnet-name mySubnetFrontEnd
azure network nic create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNic2 \
    --subnet-vnet-name myVnet \
    --subnet-name mySubnetBackEnd
```

Normalmente você cria também uma [grupo de segurança de rede](../../virtual-network/virtual-networks-nsg.md) ou [balanceador de carga](../../load-balancer/load-balancer-overview.md) toohelp gerenciar e distribuir o tráfego entre suas VMs. Olá, exemplo a seguir cria um grupo de segurança de rede denominado *myNetworkSecurityGroup*:

```azurecli
azure network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

Associar o grupo de segurança de rede de toohello de NICs usando `azure network nic set`. Olá exemplo a seguir associa *myNic1* e *myNic2* com *myNetworkSecurityGroup*:

```azurecli
azure network nic set \
    --resource-group myResourceGroup \
    --name myNic1 \
    --network-security-group-name myNetworkSecurityGroup
azure network nic set \
    --resource-group myResourceGroup \
    --name myNic2 \
    --network-security-group-name myNetworkSecurityGroup
```

## <a name="create-a-vm-and-attach-hello-nics"></a>Criar uma máquina virtual e anexar Olá NICs
Ao criar hello VM, agora você especificar várias NICs. Em vez disso, usando `--nic-name` tooprovide uma única NIC, em vez disso, você usar `--nic-names` e fornecer uma lista separada por vírgulas de NICs. Você também precisa tootake cuidado ao selecionar Olá tamanho da VM. Há limites para o número total de saudação de NICs que você pode adicionar tooa VM. Leia mais sobre [Tamanhos de VM Linux](sizes.md). Olá exemplo a seguir mostra como toospecify várias NICs e, em seguida, uma VM de tamanho que dá suporte ao uso várias NICs (*Standard_DS2_v2*):

```azurecli
azure vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --location eastus \
    --os-type linux \
    --nic-names myNic1,myNic2 \
    --vm-size Standard_DS2_v2 \
    --storage-account-name mystorageaccount \
    --image-urn UbuntuLTS \
    --admin-username azureuser \
    --ssh-publickey-file ~/.ssh/id_rsa.pub
```

## <a name="create-multiple-nics-using-resource-manager-templates"></a>Criar várias NICs usando modelos do Resource Manager
Modelos do Gerenciador de recursos do Azure usam toodefine declarativa de arquivos JSON seu ambiente. Você pode ler uma [visão geral do Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md). Modelos do Gerenciador de recursos fornecem uma maneira toocreate várias instâncias de um recurso durante a implantação, como a criação de várias NICs. Você usa *cópia* toospecify número de saudação do toocreate de instâncias:

```json
"copy": {
    "name": "multiplenics"
    "count": "[parameters('count')]"
}
```

Leia mais sobre a [criação de várias instâncias usando *copiar*](../../resource-group-create-multiple.md). 

Você também pode usar um `copyIndex()` toothen acrescentar um nome de recurso de tooa número, o que permite que você toocreate `myNic1`, `myNic2`, a seguir Olá etc. mostra um exemplo de acrescentar o valor de índice de saudação:

```json
"name": "[concat('myNic', copyIndex())]", 
```

Você pode ler um exemplo completo em [Criando várias NICs usando modelos do Gerenciador de Recursos](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).

## <a name="next-steps"></a>Próximas etapas
Certifique-se de que tooreview [tamanhos de VM do Linux](sizes.md) durante a tentativa de toocreating uma VM com várias NICs. Preste atenção toohello número de NICs dá suporte a cada tamanho VM. 

Lembre-se de que você não pode adicionar tooan adicional de NICs existentes VM, você deve criar todas as NICs de hello quando você implanta Olá VM. Tome cuidado ao planejar sua toomake implantações se você tem conectividade de rede todos os Olá necessário desde o início de saudação.

