---
title: aaaDeploy VMs do Linux em uma rede existente com o Azure CLI 2.0 | Microsoft Docs
description: "Saiba como toodeploy uma máquina virtual do Linux em uma rede Virtual existente usando Olá 2.0 do CLI do Azure"
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
ms.devlang: azurecli
ms.topic: article
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 0df44b3437002df050db56f3b3899083fb49d803
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-a-linux-virtual-machine-into-an-existing-azure-virtual-network-with-hello-azure-cli"></a>Como toodeploy uma máquina virtual do Linux em uma rede Virtual do Azure existente com hello CLI do Azure

Este artigo mostra como toouse hello Azure CLI 2.0 toodeploy uma máquina virtual (VM) em uma rede virtual existente. requisitos de saudação são:

- [uma conta do Azure](https://azure.microsoft.com/pricing/free-trial/)
- [arquivos de chave SSH pública e privada](mac-create-ssh-keys.md)

Você também pode executar essas etapas com hello [Azure CLI 1.0](deploy-linux-vm-into-existing-vnet-using-cli-nodejs.md).


## <a name="quick-commands"></a>Comandos rápidos
Se você precisar tooquickly realizar tarefa hello, Olá seção a seguir fornece detalhes sobre comandos Olá necessários. Obter mais informações e o contexto para cada etapa pode ser encontrada restante de saudação do documento hello, [Iniciar aqui](#detailed-walkthrough).

toocreate nesse ambiente personalizado, você precisa hello mais recente [2.0 do CLI do Azure](/cli/azure/install-az-cli2) instalado e registrado no tooan conta do Azure usando [logon az](/cli/azure/#login).

Em Olá exemplos a seguir, substitua os nomes de parâmetro de exemplo com seus próprios valores. Os nomes de parâmetro de exemplo incluem *myResourceGroup*, *myVnet* e *myVM*.

**Pré-requisitos:** grupo de recursos do Azure, rede virtual e sub-rede, grupo de segurança de rede com o SSH de entrada e uma placa de interface de rede virtual.

### <a name="deploy-hello-vm-into-hello-virtual-network-infrastructure"></a>Implantar Olá VM na infraestrutura de rede virtual Olá

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image Debian \
    --admin-username azureuser \
    --generate-ssh-keys \
    --nics myNic
```

## <a name="detailed-walkthrough"></a>Passo a passo detalhado

Os ativos do Azure, como as redes virtuais e os grupos de segurança de rede, devem ser recursos estáticos e de longa duração que raramente são implantados. Quando uma rede virtual tiver sido implantada, ele pode ser reutilizado por novas implantações sem nenhuma infraestrutura de toohello efeitos adversos. Pensar em uma rede virtual como sendo um comutador de rede de hardware tradicional - você não precisará tooconfigure alternar de um novo hardware com cada implantação. Com uma rede virtual configurada corretamente, você pode continuar toodeploy novas VMs na rede virtual repetidamente com poucas, se houver, as alterações necessárias durante o tempo de saudação da rede virtual hello.

toocreate nesse ambiente personalizado, você precisa hello mais recente [2.0 do CLI do Azure](/cli/azure/install-az-cli2) instalado e registrado no tooan conta do Azure usando [logon az](/cli/azure/#login).

Em Olá exemplos a seguir, substitua os nomes de parâmetro de exemplo com seus próprios valores. Os nomes de parâmetro de exemplo incluem *myResourceGroup*, *myVnet* e *myVM*.

## <a name="create-hello-resource-group"></a>Criar grupo de recursos de saudação

Primeiro, crie um tooorganize do grupo de recursos do Azure tudo que você cria neste passo a passo. Para saber mais sobre grupos de recursos, confira [Visão geral do Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md). Criar grupo de recursos de saudação com [criar grupo az](/cli/azure/group#create). Olá, exemplo a seguir cria um grupo de recursos denominado *myResourceGroup* em Olá *eastus* local:

```azurecli
az group create \
    --name myResourceGroup \
    --location eastus
```

## <a name="create-hello-virtual-network"></a>Criar rede virtual Olá

Permite criar uma saudação toolaunch de rede virtual do Azure VMs em. Para obter mais informações sobre redes virtuais, consulte [criar uma rede virtual usando Olá CLI do Azure](../../virtual-network/virtual-networks-create-vnet-arm-cli.md). Criar rede virtual de saudação com [criar redes de rede az](/cli/azure/network/vnet#create). Olá, exemplo a seguir cria uma rede virtual denominada *myVnet* e sub-rede denominada *mySubnet*:

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myVnet \
    --address-prefix 10.10.0.0/16 \
    --subnet-name mySubnet \
    --subnet-prefix 10.10.1.0/24
```

## <a name="create-hello-network-security-group"></a>Criar grupo de segurança de rede Olá

Grupos de segurança de rede do Azure são equivalentes tooa firewall na camada de rede hello. Para obter mais informações sobre os grupos de segurança de rede, consulte [como os grupos de segurança de rede toocreate em Olá CLI do Azure](../../virtual-network/virtual-networks-create-nsg-arm-cli.md). Criar grupo de segurança de rede Olá com [criar az rede nsg](/cli/azure/network/nsg#create). Olá, exemplo a seguir cria um grupo de segurança de rede denominado *myNetworkSecurityGroup*:

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

## <a name="add-an-inbound-ssh-allow-rule"></a>Adicionar uma regra de permissão de SSH de entrada

Olá VM precisa ter acesso de saudação à internet, para que uma regra que permite a porta de entrada 22 tráfego toobe passado Olá rede tooport 22 na Olá VM é necessária. Adicionar uma regra de entrada para o grupo de segurança de rede Olá com [criar regra de nsg rede az](/cli/azure/network/nsg/rule#create). Olá, exemplo a seguir cria uma regra denominada *myNetworkSecurityGroupRuleSSH*:

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRuleSSH \
    --priority 1000 \
    --protocol tcp \
    --destination-port-range 22 \
```

## <a name="attach-hello-subnet-toohello-network-security-group"></a>Anexar o grupo de segurança de rede do hello sub-rede toohello

regras de grupo de segurança de rede Olá podem ser aplicado tooa sub-rede ou uma interface de rede virtual específica. Permite anexar Olá segurança grupo tooour sub-rede. Conecte seu grupo de segurança de rede toohello sub-rede com [atualização de sub-rede da rede virtual de rede az](/cli/azure/network/vnet/subnet#update):

```azurecli
az network vnet subnet update \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnet \
    --network-security-group myNetworkSecurityGroup
```

## <a name="add-a-virtual-network-interface-card-toohello-subnet"></a>Adicionar uma sub-rede toohello de placa de interface de rede virtual

Placas de interface de rede virtual (VNics) são importantes para você pode reutilizá-los, conectando-os toodifferent VMs. Essa reutilização permite tookeep Olá VNic como um recurso estático enquanto Olá VMs pode ser temporário. Criar uma VNic e associá-lo a sub-rede Olá [nic da rede az criar](/cli/azure/network/nic#create). Olá, exemplo a seguir cria uma VNic denominada *myNic*:

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet
```

## <a name="deploy-hello-vm-into-hello-virtual-network-infrastructure"></a>Implantar Olá VM na infraestrutura de rede virtual Olá

Agora, você tem uma rede virtual e sub-redes e uma sub-rede da rede segurança grupo tooprotect Olá bloqueando todo o tráfego de entrada exceto 22 de porta para o SSH. Olá VM agora pode ser implantado nessa infraestrutura de rede existente.

Crie a sua VM com [az vm create](/cli/azure/vm#create). Para obter mais informações sobre Olá sinalizadores toouse com hello Azure CLI 2.0 toodeploy uma VM completa, consulte [criar um ambiente completo do Linux usando Olá CLI do Azure](create-cli-complete.md).

saudação de exemplo a seguir cria uma máquina virtual usando discos gerenciado do Azure. Esses discos são manipulados pelo Olá plataforma Windows Azure e não exigem qualquer etapa de preparação ou local toostore-los. Para saber mais sobre discos gerenciados, veja [Visão geral dos Azure Managed Disks](../../storage/storage-managed-disks-overview.md). Se desejar que os discos toouse não gerenciado, consulte a Observação adicionais de saudação abaixo.

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image Debian \
    --admin-username azureuser \
    --generate-ssh-keys \
    --nics myNic
```

Se você usar discos gerenciados, ignore esta etapa. Se desejar que os discos toouse não gerenciado, você precisa tooadd Olá seguintes parâmetros adicionais toohello continuar comando toocreate não gerenciado discos na conta de armazenamento Olá chamado `mystorageaccount`: 

```azurecli
    --use-unmanaged-disk \
    --storage-account mystorageaccount
```

Usando Olá CLI sinalizadores de toocall recursos existentes, você instruir Olá toodeploy Azure VM dentro da rede existente hello. Depois que uma rede virtual e uma sub-rede são implantadas, elas podem ser mantidas como recursos estáticos ou permanentes na sua região do Azure. Neste exemplo, você não criar e atribuir um toohello de endereço IP público VNic, portanto essa VM não é publicamente acessível pela Internet da saudação. Para obter mais informações, consulte [criar uma VM com um IP público estático usando Olá CLI do Azure](../../virtual-network/virtual-network-deploy-static-pip-arm-cli.md).

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações sobre maneiras toocreate as máquinas virtuais no Azure, consulte Olá recursos a seguir:

* [Usar um modelo de Gerenciador de recursos do Azure toocreate uma implantação específica](../windows/cli-deploy-templates.md)
* [Criar seu próprio ambiente personalizado para uma VM do Linux usando os comandos da CLI do Azure diretamente](create-cli-complete.md)
* [Criar uma VM do Linux no Azure usando modelos](create-ssh-secured-vm-from-template.md)
