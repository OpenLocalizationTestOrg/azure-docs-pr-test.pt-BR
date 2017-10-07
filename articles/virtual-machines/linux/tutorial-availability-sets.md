---
title: aaaAvailability define o tutorial para VMs do Linux no Azure | Microsoft Docs
description: "Saiba mais sobre Olá conjuntos de disponibilidade para VMs do Linux no Azure."
documentationcenter: 
services: virtual-machines-linux
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 2a91e4a6057180035ec51410d9fffccaca343758
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-availability-sets"></a>Como os conjuntos de disponibilidade de toouse


Neste tutorial, você aprenderá como a disponibilidade de saudação tooincrease e a confiabilidade de suas soluções de máquina Virtual no Azure usando um recurso chamado conjuntos de disponibilidade. Conjuntos de disponibilidade garantem que Olá VMs implantar no Azure são distribuídas entre vários clusters de hardware isoladas. Isso garante que, se ocorre uma falha de hardware ou software no Azure, um sub conjunto das suas máquinas virtuais será afetado e que sua solução geral permanecerão disponíveis e operacionais da perspectiva de saudação de seus clientes usá-lo.

Neste tutorial, você aprenderá como:

> [!div class="checklist"]
> * Criar um conjunto de disponibilidade
> * Criar uma VM em um conjunto de disponibilidade
> * Verificar os tamanhos de VM disponíveis


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Se você escolher tooinstall e usa o hello CLI localmente, este tutorial requer que você está executando a versão de CLI do Azure Olá 2.0.4 ou posterior. Executar `az --version` toofind versão de saudação. Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="availability-set-overview"></a>Visão geral do conjunto de disponibilidade

Um conjunto de disponibilidade é um recurso de agrupamento lógico que você pode usar no Azure tooensure que recursos VM Olá que colocar nele são isolados uma da outra quando eles forem implantados em um datacenter do Azure. Azure garante que as VMs que você coloca em um conjunto de disponibilidade executado em vários servidores físicos hello, comutadores de rede, unidades de armazenamento e racks de computação. Isso garante que no caso de saudação de um hardware ou falha de software do Azure, apenas um subconjunto das suas máquinas virtuais será afetado, e geral do seu aplicativo irá continuar e continuar toobe tooyour disponíveis clientes. Usando conjuntos de disponibilidade é um recurso essencial tooleverage toobuild soluções de nuvem confiável.

Vamos considerar uma solução comum baseada em VM na qual você pode ter quatro servidores Web front-end e usar duas VMs de back-end que hospedam um banco de dados. Com o Azure, você desejaria toodefine dois conjuntos de disponibilidade antes de implantar suas VMs: conjunto de disponibilidade de um para nível de "web" hello e um conjunto de disponibilidade para camada de "banco de dados" hello. Quando você cria uma nova VM, em seguida, você pode especificar disponibilidade Olá definida como uma vm do parâmetro toohello az criar comando e Azure automaticamente garantirá que Olá VMs criar dentro Olá disponível conjunto são isolados em vários recursos de hardware físico. Isso significa que, se o hardware físico de saudação que seu servidor Web ou VMs de servidor de banco de dados está em execução no tem um problema, você sabe que Olá outras instâncias do servidor Web e VMs de banco de dados continuará em execução bem porque eles estão em um hardware diferente.

Quando você quiser soluções toodeploy baseado em VM confiáveis no Azure, você sempre deve usar conjuntos de disponibilidade.


## <a name="create-an-availability-set"></a>Criar um conjunto de disponibilidade

Crie um conjunto de disponibilidade usando [az vm availability-set create](/cli/azure/vm/availability-set#create). Neste exemplo, vamos definir ambos de número de domínios de atualização e falha no hello *2* para o conjunto nomeada de disponibilidade de saudação *myAvailabilitySet* em Olá *myResourceGroupAvailability*grupo de recursos.

Crie um grupos de recursos.

```azurecli-interactive 
az group create --name myResourceGroupAvailability --location eastus
```


```azurecli-interactive 
az vm availability-set create \
    --resource-group myResourceGroupAvailability \
    --name myAvailabilitySet \
    --platform-fault-domain-count 2 \
    --platform-update-domain-count 2
```

Conjuntos de disponibilidade permite que recursos tooisolate em "domínios de falha" e "domínios de atualização". Um **domínio de falha** representa uma coleção isolada de recursos de servidor + rede + armazenamento. Olá anterior de exemplo, indicamos que queremos que nossa disponibilidade definida toobe distribuído em pelo menos dois domínios de falha ao nosso VMs são implantadas. Também podemos indicar que desejamos distribuir nosso conjunto de disponibilidade entre dois **domínios de atualização**.  Certifique-se de dois domínios de atualização que, quando o Azure executa as atualizações de software nossos recursos VM são isolados, impedindo que todos os softwares de saudação em execução sob nosso VM seja atualizado no hello simultaneamente.

## <a name="configure-virtual-network"></a>Configurar rede virtual
Antes de implantar algumas máquinas virtuais e testar seu balanceador, crie hello dando suporte a recursos de rede virtual. Para obter mais informações sobre redes virtuais, consulte Olá [gerenciar redes virtuais do Azure](tutorial-virtual-network.md) tutorial.

### <a name="create-network-resources"></a>Criar recursos da rede
Crie a rede virtual com [az network vnet create](/cli/azure/network/vnet#create). Olá, exemplo a seguir cria uma rede virtual denominada *myVnet* com uma sub-rede denominada *mySubnet*:

```azurecli-interactive 
az network vnet create \
    --resource-group myResourceGroupAvailability \
    --name myVnet \
    --subnet-name mySubnet
```
NICs virtuais são criadas com [az network nic create](/cli/azure/network/nic#create). Olá, exemplo a seguir cria três NICs virtuais. (Uma NIC virtual para cada VM que você criou para seu aplicativo no hello seguindo as etapas.) Você pode criar VMs e NICs virtuais adicionais a qualquer momento e adicioná-los toohello balanceador de carga:

```bash
for i in `seq 1 3`; do
    az network nic create \
        --resource-group myResourceGroupAvailability \
        --name myNic$i \
        --vnet-name myVnet \
        --subnet mySubnet \
        --lb-name myLoadBalancer \
        --lb-address-pools myBackEndPool
done
```

## <a name="create-vms-inside-an-availability-set"></a>Criar VMs dentro de um conjunto de disponibilidade

Máquinas virtuais devem ser criados em toomake de conjunto de disponibilidade de saudação-se de que eles sejam distribuídos corretamente em hardware de saudação. Não é possível adicionar um grupo de disponibilidade de tooan VM definida depois que ela é criada. 

Quando você cria uma VM usando [criar vm az](/cli/azure/vm#create) especificar Olá conjunto de disponibilidade usando Olá `--availability-set` nome do parâmetro toospecify Olá Olá do conjunto de disponibilidade.

```azurecli-interactive 
for i in `seq 1 2`; do
   az vm create \
     --resource-group myResourceGroupAvailability \
     --name myVM$i \
     --availability-set myAvailabilitySet \
     --nics myNic$i \
     --size Standard_DS1_v2  \
     --image Canonical:UbuntuServer:14.04.4-LTS:latest \
     --admin-username azureuser \
     --generate-ssh-keys \
     --no-wait
done 
```

Agora temos duas máquinas virtuais em nosso conjunto de disponibilidade recém-criado. Olá a porque eles estão no mesmo conjunto de disponibilidade, o Azure garantirá que VMs hello e todos os seus recursos (incluindo os discos de dados) são distribuídos em hardware físico isolado. Essa distribuição ajuda a garantir uma disponibilidade muito maior de nossa solução de VM geral.

Uma coisa que você pode encontrar ao adicionar VMs é que um determinado tamanho VM não está mais disponível toouse em seu conjunto de disponibilidade. Esse problema pode ocorrer se não for suficiente tooadd capacidade enquanto preserva o conjunto de disponibilidade de saudação do hello isolamento regras impõe. Você pode verificar toosee quais tamanhos VM são toouse disponível dentro de um grupo de disponibilidade definido usando Olá `--availability-set list-sizes` parâmetro.

## <a name="check-for-available-vm-sizes"></a>Conferir os tamanhos de VM disponíveis 

Você pode adicionar mais máquinas virtuais toohello conjunto de disponibilidade posteriormente, mas é necessário tooknow quais tamanhos VM estão disponíveis em hardware de saudação. Use [lista-tamanhos do conjunto de disponibilidade de vm az](/cli/azure/availability-set#list-sizes) toolist todos os tamanhos disponíveis de Olá em hardware de saudação do cluster para o conjunto de disponibilidade hello.

```azurecli-interactive 
az vm availability-set list-sizes \
     --resource-group myResourceGroupAvailability \
     --name myAvailabilitySet \
     --output table  
```

## <a name="next-steps"></a>Próximas etapas

Neste tutorial, você aprendeu como:

> [!div class="checklist"]
> * Criar um conjunto de disponibilidade
> * Criar uma VM em um conjunto de disponibilidade
> * Verificar os tamanhos de VM disponíveis

Avançar toohello toolearn próximo de tutorial sobre conjuntos de escala de máquina virtual.

> [!div class="nextstepaction"]
> [Criar um conjunto de dimensionamento da VM](tutorial-create-vmss.md)

