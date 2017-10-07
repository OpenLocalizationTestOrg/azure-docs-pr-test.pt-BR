---
title: aaaOpen portas tooa VM do Linux com o Azure CLI 2.0 | Microsoft Docs
description: "Saiba como tooopen uma porta / criar um ponto de extremidade tooyour VM do Linux usando a implantação do Gerenciador de recursos do Azure de saudação do modelo e Olá 2.0 do CLI do Azure"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: eef9842b-495a-46cf-99a6-74e49807e74e
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 08/21/2017
ms.author: iainfou
ms.openlocfilehash: c79b31206e97558171609cf033bb3cb3370777c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="open-ports-and-endpoints-tooa-linux-vm-with-hello-azure-cli"></a>Abrir portas e os pontos de extremidade tooa VM do Linux com hello CLI do Azure
Abrir uma porta, ou criar um ponto de extremidade, tooa máquina virtual (VM) no Azure, criando um filtro de rede em uma sub-rede ou interface de rede VM. Você pode colocar esses filtros, que controlam o tráfego de entrada e saído, em um recurso de toohello do grupo de segurança de rede conectados que recebe o tráfego de saudação. Vamos usar um exemplo comum de tráfego da Web na porta 80. Este artigo mostra como tooopen tooa uma porta VM com hello 2.0 do CLI do Azure. Você também pode executar essas etapas com hello [Azure CLI 1.0](nsg-quickstart-nodejs.md).


## <a name="quick-commands"></a>Comandos rápidos
Grupo de segurança de rede toocreate e regras que você precisa hello mais recente [2.0 do CLI do Azure](/cli/azure/install-az-cli2) instalado e registrado no tooan conta do Azure usando [logon az](/cli/azure/#login).

Em Olá exemplos a seguir, substitua os nomes de parâmetro de exemplo com seus próprios valores. Os nomes de parâmetro de exemplo incluem *myResourceGroup*, *myNetworkSecurityGroup* e *myVnet*.

Criar grupo de segurança de rede Olá com [criar az rede nsg](/cli/azure/network/nsg#create). Olá, exemplo a seguir cria um grupo de segurança de rede denominado *myNetworkSecurityGroup* em Olá *eastus* local:

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

Adicionar uma regra com [criar regra de nsg rede az](/cli/azure/network/nsg/rule#create) tooallow HTTP tráfego tooyour webserver (ou ajustar para seu próprio cenário, como conectividade de banco de dados ou acesso SSH). Olá, exemplo a seguir cria uma regra denominada *myNetworkSecurityGroupRule* tooallow TCP de tráfego na porta 80:

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --protocol tcp \
    --priority 1000 \
    --destination-port-range 80
```

Associar Olá grupo de segurança de rede com interface de rede da VM (NIC) [atualização da nic de rede az](/cli/azure/network/nic#update). Olá, exemplo a seguir associa um NIC existente denominado *myNic* com hello grupo de segurança de rede denominado *myNetworkSecurityGroup*:

```azurecli
az network nic update \
    --resource-group myResourceGroup \
    --name myNic \
    --network-security-group myNetworkSecurityGroup
```

Como alternativa, você pode associar seu grupo de segurança de rede com uma sub-rede de rede virtual com [atualização de sub-rede da rede virtual de rede az](/cli/azure/network/vnet/subnet#update) em vez de apenas toohello interface de rede em uma única VM. Olá, exemplo a seguir associa uma sub-rede existente denominada *mySubnet* em Olá *myVnet* rede virtual com hello grupo de segurança de rede denominado *myNetworkSecurityGroup*:

```azurecli
az network vnet subnet update \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnet \
    --network-security-group myNetworkSecurityGroup
```

## <a name="more-information-on-network-security-groups"></a>Mais informações sobre os Grupos de Segurança de Rede
Olá aqui rápido comandos permitem que você tooget para cima e em execução com tooyour de fluxo de tráfego VM. Grupos de segurança de rede fornecem vários recursos excelentes e granularidade para controlar recursos tooyour de acesso. Você pode ler mais sobre a [criação de um Grupo de Segurança de Rede e as regras ACL aqui](tutorial-virtual-network.md#secure-network-traffic).

Para aplicativos Web altamente disponíveis, você deve colocar suas VMs atrás de um balanceador de carga do Azure. Balanceador de carga Olá distribui tráfego tooVMs, com um grupo de segurança de rede que fornece filtragem. Para obter mais informações, consulte [como balancear tooload Linux virtual máquinas no Azure toocreate um aplicativo altamente disponível](tutorial-load-balancer.md).

## <a name="next-steps"></a>Próximas etapas
Neste exemplo, você criou um tráfego HTTP de tooallow regra simples. Você pode encontrar informações sobre como criar ambientes mais detalhadas no hello artigos a seguir:

* [Visão geral do Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md)
* [O que é um NSG (grupo de segurança de rede)?](../../virtual-network/virtual-networks-nsg.md)
