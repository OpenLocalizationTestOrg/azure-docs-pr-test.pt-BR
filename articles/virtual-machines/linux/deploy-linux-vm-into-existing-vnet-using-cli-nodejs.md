---
title: aaaDeploy VMs do Linux em uma rede existente com o Azure CLI 1.0 | Microsoft Docs
description: "Como toodeploy uma VM do Linux em uma rede Virtual existente usando Olá 1.0 da CLI do Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: e660f1563d386efc7788bd236f8b067145ea09bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-a-linux-virtual-machine-into-an-existing-azure-virtual-network-with-hello-azure-cli-10"></a>Como toodeploy uma máquina virtual do Linux em uma rede Virtual do Azure existente com hello 1.0 da CLI do Azure

Este artigo mostra como toouse 1.0 da CLI do Azure toodeploy uma máquina virtual (VM) em uma rede Virtual existente (VNet). requisitos de saudação são:

- [uma conta do Azure](https://azure.microsoft.com/pricing/free-trial/)
- [arquivos de chave SSH pública e privada](mac-create-ssh-keys.md)


## <a name="cli-versions-toocomplete-hello-task"></a>Tarefa de saudação do CLI versões toocomplete
Você pode concluir a tarefa hello usando uma saudação versões da CLI a seguir:

- [1.0 de CLI do Azure](#quick-commands) – nosso CLI para Olá clássico e o recurso de gerenciamento modelos de implantação (Este artigo)
- [2.0 do CLI do Azure](deploy-linux-vm-into-existing-vnet-using-cli.md) -nossa próxima geração CLI para o modelo de implantação do gerenciamento de recursos de saudação


## <a name="quick-commands"></a>Comandos rápidos

Se você precisar tooquickly realizar tarefa hello, Olá seção a seguir fornece detalhes sobre comandos Olá necessários. Obter mais informações e o contexto para cada etapa pode ser encontrada restante de saudação do documento hello, [Iniciar aqui](deploy-linux-vm-into-existing-vnet-using-cli.md#detailed-walkthrough).

Pré-requisitos: Grupo de Recursos, VNet, NSG com SSH de entrada e Sub-rede. Substitua os exemplos por suas próprias configurações.

### <a name="deploy-hello-vm-into-hello-virtual-network-infrastructure"></a>Implantar Olá VM na infraestrutura de rede virtual Olá

```azurecli
azure vm create myVM \
    -g myResourceGroup \
    -l eastus \
    -y linux \
    -Q Debian \
    -o mystorageaccount \
    -u myAdminUser \
    -M ~/.ssh/id_rsa.pub \
    -n myVM \
    -F myVNet \
    -j mySubnet \
    -N myVNic
```

## <a name="detailed-walkthrough"></a>Passo a passo detalhado

Olá VNets, como ativos do Azure e grupos de segurança de rede devem ser estáticos e vida útil longa recursos que raramente são implantados. Quando uma rede virtual tiver sido implantada, ele pode ser reutilizado por novas implantações sem nenhuma infraestrutura de toohello efeitos adversos. Pense em uma rede virtual como sendo um comutador de rede tradicionais de hardware. Você não precisará tooconfigure alternar de um novo hardware com cada implantação. Com uma rede virtual configurada corretamente, você pode continuar toodeploy novos servidores para essa rede virtual repetidamente com poucas, se houver, alterações necessárias sobre a vida útil de saudação do hello VNet.

## <a name="create-hello-resource-group"></a>Criar grupo de recursos de saudação

Primeiro, crie um tooorganize do grupo de recursos tudo que você cria neste passo a passo. Para obter mais informações sobre os grupos de recursos, consulte [Visão geral do Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md)

```azurecli
azure group create myResourceGroup --location eastus
```

## <a name="create-hello-vnet"></a>Criar hello VNet

Olá primeira etapa é toobuild toolaunch uma rede virtual Olá VMs em. Olá VNet contém uma sub-rede para este passo a passo. Para obter mais informações sobre VNets do Azure, consulte [criar uma rede virtual usando Olá CLI do Azure](../../virtual-network/virtual-networks-create-vnet-arm-cli.md)

```azurecli
azure network vnet create myVNet \
    --resource-group myResourceGroup \
    --address-prefixes 10.10.0.0/24 \
    --location eastus
```

## <a name="create-hello-network-security-group"></a>Criar grupo de segurança de rede Olá

subrede Olá baseia-se atrás de um grupo de segurança de rede existente para criar grupos de segurança de rede Olá antes de sub-rede hello. Grupos de segurança de rede do Azure são equivalentes tooa firewall na camada de rede hello. Para obter mais informações sobre os grupos de segurança de rede do Azure, consulte [como os grupos de segurança de rede toocreate em Olá CLI do Azure](../../virtual-network/virtual-networks-create-nsg-arm-cli.md)

```azurecli
azure network nsg create myNetworkSecurityGroup \
    --resource-group myResourceGroup \
    --location eastus
```

## <a name="add-an-inbound-ssh-allow-rule"></a>Adicionar uma regra de permissão de SSH de entrada

Olá VM precisa ter acesso de saudação à internet para que uma regra que permite a porta de entrada 22 tráfego toobe passado Olá rede tooport 22 na Olá VM é necessária.

```azurecli
azure network nsg rule create inboundSSH \
    --resource-group myResourceGroup \
    --nsg-name myNSG \
    --access Allow \
    --protocol Tcp \
    --direction Inbound \
    --priority 100 \
    --source-address-prefix Internet \
    --source-port-range 22 \
    --destination-address-prefix 10.10.0.0/24 \
    --destination-port-range 22
```

## <a name="add-a-subnet-toohello-vnet"></a>Adicionar toohello uma sub-rede VNet

VMs em redes de saudação devem estar localizadas em uma sub-rede. Cada VNET pode ter várias sub-redes. Criar uma sub-rede hello e associar ao grupo de segurança de rede hello.

```azurecli
azure network vnet subnet create mySubNet \
    --resource-group myResourceGroup \
    --vnet-name myVNet \
    --address-prefix 10.10.0.0/26 \
    --network-security-group-name myNetworkSecurityGroup
```

Olá sub-rede agora é adicionado em Olá VNet e associado à regra e o grupo de segurança de rede de saudação.


## <a name="add-a-vnic-toohello-subnet"></a>Adicionar uma sub-rede de toohello VNic

Placas de rede virtual (VNics) são importantes para você pode reutilizá-los, conectando-os toodifferent VMs. Essa abordagem mantém Olá VNic como um recurso estático enquanto Olá VMs pode ser temporário. Crie uma VNic e associá-lo a sub-rede Olá criado na etapa anterior hello.

```azurecli
azure network nic create myVNic \
    --resource-group myResourceGroup \
    --location eastus \
    ---subnet-vnet-name myVNet \
    --subnet-name mySubNet
```

## <a name="deploy-hello-vm-into-hello-vnet-and-nsg"></a>Implantar hello VM em Olá VNet e NSG

Agora você tem uma rede virtual e sub-rede dentro dessa rede virtual e um grupo de segurança de rede atuando subrede tooprotect Olá bloqueando todo o tráfego de entrada exceto 22 de porta para o SSH. Olá VM agora pode ser implantado nessa infraestrutura de rede existente.

Usando Olá CLI do Azure e Olá `azure vm create` comando, Olá VM do Linux é implantado toohello grupo de recursos do Azure, redes, sub-rede e VNic existentes. Para obter mais informações sobre como usar o hello CLI toodeploy uma VM completa, consulte [criar um ambiente completo do Linux usando Olá CLI do Azure](create-cli-complete.md)

```azurecli
azure vm create myVM \
    --resource-group myResourceGroup \
    --location eastus \
    --os-type linux \
    --image-urn Debian \
    --storage-account-name mystorageaccount \
    --admin-username myAdminUser \
    --ssh-publickey-file ~/.ssh/id_rsa.pub \
    --vnet-name myVNet \
    --vnet-subnet-name mySubnet \
    --nic-name myVNic
```

Usando Olá CLI sinalizadores de toocall recursos existentes, você instruir Olá toodeploy Azure VM dentro da rede existente hello. Depois que uma VNET e uma sub-rede forem implantadas, elas poderão ser mantidas como recursos estáticos ou permanentes na região do Azure.  

## <a name="next-steps"></a>Próximas etapas

* [Usar um modelo de Gerenciador de recursos do Azure toocreate uma implantação específica](../windows/cli-deploy-templates.md)
* [Criar seu próprio ambiente personalizado para uma VM do Linux usando os comandos da CLI do Azure diretamente](create-cli-complete.md)
* [Criar uma VM do Linux no Azure usando modelos](create-ssh-secured-vm-from-template.md)
