---
title: "aaaCreate uma VM do Linux no Azure com várias NICs | Microsoft Docs"
description: "Saiba como toocreate uma VM do Linux com várias NICs anexado tooit usando modelos de hello Azure 2.0 do CLI ou o Gerenciador de recursos."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 5d2d04d0-fc62-45fa-88b1-61808a2bc691
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 2723405914777a5dce4354d4f5d8413e357f58e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-linux-virtual-machine-in-azure-with-multiple-network-interface-cards"></a>Como toocreate uma máquina de virtual do Linux no Azure com rede várias placas de interface
Você pode criar uma máquina virtual (VM) no Azure que tenha vários tooit de interfaces (NICs) conectados a rede virtual. Um cenário comum é toohave várias sub-redes para conectividade de front-end e back-end ou uma rede dedicada tooa monitoramento ou solução de backup. Este artigo detalha como toocreate uma VM com várias NICs anexado tooit e NICs tooadd ou remover de uma VM existente. Para obter informações detalhadas, incluindo como toocreate várias NICs dentro de sua própria Bash scripts, leia mais sobre [Implantando VMs multi-NIC](../../virtual-network/virtual-network-deploy-multinic-arm-cli.md). Diferentes [tamanhos de VM](sizes.md) dão suporte a um número variável de NICs, sendo assim, dimensione sua VM adequadamente.

Este artigo fornece detalhes sobre como toocreate uma VM com várias NICs com hello 2.0 do CLI do Azure. Você também pode executar essas etapas com hello [Azure CLI 1.0](multiple-nics-nodejs.md).


## <a name="create-supporting-resources"></a>Criar recursos de suporte
Saudação de instalação mais recente [2.0 do CLI do Azure](/cli/azure/install-az-cli2) e fazer logon na conta do Azure usando o tooan [logon az](/cli/azure/#login).

Em Olá exemplos a seguir, substitua os nomes de parâmetro de exemplo com seus próprios valores. Os nomes de parâmetro de exemplo incluem *myResourceGroup*, *mystorageaccount* e *myVM*.

Primeiro, crie um grupo de recursos com [az group create](/cli/azure/group#create). Olá, exemplo a seguir cria um grupo de recursos denominado *myResourceGroup* em Olá *eastus* local:

```azurecli
az group create --name myResourceGroup --location eastus
```

Criar rede virtual de saudação com [criar redes de rede az](/cli/azure/network/vnet#create). Olá, exemplo a seguir cria uma rede virtual denominada *myVnet* e sub-rede denominada *mySubnetFrontEnd*:

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --name myVnet \
    --address-prefix 192.168.0.0/16 \
    --subnet-name mySubnetFrontEnd \
    --subnet-prefix 192.168.1.0/24
```

Criar uma sub-rede para o tráfego de back-end de saudação com [sub-rede de rede virtual de rede az criar](/cli/azure/network/vnet/subnet#create). Olá, exemplo a seguir cria uma sub-rede denominada *mySubnetBackEnd*:

```azurecli
az network vnet subnet create \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnetBackEnd \
    --address-prefix 192.168.2.0/24
```

Crie um grupo de segurança de rede com [az network nsg create](/cli/azure/network/nsg#create). Olá, exemplo a seguir cria um grupo de segurança de rede denominado *myNetworkSecurityGroup*:

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --name myNetworkSecurityGroup
```

## <a name="create-and-configure-multiple-nics"></a>Criar e configurar várias NICs
Crie duas NICs com [az network nic create](/cli/azure/network/nic#create). Olá, exemplo a seguir cria duas NICs, denominadas *myNic1* e *myNic2*conectados grupo de segurança de rede hello, com uma NIC conectam tooeach sub-rede:

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic1 \
    --vnet-name myVnet \
    --subnet mySubnetFrontEnd \
    --network-security-group myNetworkSecurityGroup
az network nic create \
    --resource-group myResourceGroup \
    --name myNic2 \
    --vnet-name myVnet \
    --subnet mySubnetBackEnd \
    --network-security-group myNetworkSecurityGroup
```

## <a name="create-a-vm-and-attach-hello-nics"></a>Criar uma máquina virtual e anexar Olá NICs
Quando você cria Olá VM, especifique Olá NICs criado com `--nics`. Você também precisa tootake cuidado ao selecionar Olá tamanho da VM. Há limites para o número total de saudação de NICs que você pode adicionar tooa VM. Leia mais sobre [Tamanhos de VM Linux](sizes.md). 

Crie uma VM com [az vm create](/cli/azure/vm#create). Olá, exemplo a seguir cria uma VM denominada *myVM*:

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --size Standard_DS3_v2 \
    --admin-username azureuser \
    --generate-ssh-keys \
    --nics myNic1 myNic2
```

## <a name="add-a-nic-tooa-vm"></a>Adicionar uma NIC tooa VM
etapas anteriores Olá criou uma VM com várias NICs. Você também pode adicionar tooan NICs existentes VM com hello 2.0 do CLI do Azure. 

Crie outra NIC com [az network nic create](/cli/azure/network/nic#create). Olá, exemplo a seguir cria uma NIC denominada *myNic3* conectados toohello sub-rede de back-end e o grupo de segurança de rede criado nas etapas anteriores hello:

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic3 \
    --vnet-name myVnet \
    --subnet mySubnetBackEnd \
    --network-security-group myNetworkSecurityGroup
```

tooadd tooan uma placa de rede VM existente, primeiro desalocar Olá VM com [az vm desalocar](/cli/azure/vm#deallocate). exemplo a seguir Hello desaloca Olá VM denominada *myVM*:

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

Adicionar Olá NIC com [nic de vm az adicionar](/cli/azure/vm/nic#add). Olá exemplo a seguir adiciona *myNic3* muito*myVM*:

```azurecli
az vm nic add \
    --resource-group myResourceGroup \
    --vm-name myVM \
    --nics myNic3
```

Iniciar Olá VM com [início de vm az](/cli/azure/vm#start):

```azurecli
az vm start --resource-group myResourceGroup --name myVM
```

## <a name="remove-a-nic-from-a-vm"></a>Remover uma NIC de uma VM
tooremove uma NIC de uma VM existente, primeiro desalocar Olá VM com [az vm desalocar](/cli/azure/vm#deallocate). exemplo a seguir Hello desaloca Olá VM denominada *myVM*:

```azurecli
az vm deallocate --resource-group myResourceGroup --name myVM
```

Remover Olá NIC com [nic de vm az remover](/cli/azure/vm/nic#remove). Olá exemplo a seguir remove *myNic3* de *myVM*:

```azurecli
az vm nic remove \
    --resource-group myResourceGroup \
    --vm-name myVM 
    --nics myNic3
```

Iniciar Olá VM com [início de vm az](/cli/azure/vm#start):

```azurecli
az vm start --resource-group myResourceGroup --name myVM
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
Revisão [tamanhos de VM do Linux](sizes.md) durante a tentativa de toocreating uma VM com várias NICs. Preste atenção toohello número de NICs dá suporte a cada tamanho VM. 
