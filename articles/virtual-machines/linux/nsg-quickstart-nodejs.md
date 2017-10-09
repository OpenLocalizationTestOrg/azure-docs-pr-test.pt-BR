---
title: aaaOpen portas tooa VM do Linux com o Azure CLI 1.0 | Microsoft Docs
description: "Saiba como tooopen uma porta / criar um ponto de extremidade tooyour VM do Linux usando a implantação do Gerenciador de recursos do Azure de saudação do modelo e Olá 1.0 da CLI do Azure"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 337c37d151f527b43d4852291159b2f70a00accc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="opening-ports-and-endpoints-tooa-linux-vm-in-azure-using-hello-azure-cli-10"></a>Abrindo portas e os pontos de extremidade tooa VM do Linux no Azure usando Olá 1.0 da CLI do Azure
Abrir uma porta, ou criar um ponto de extremidade, tooa máquina virtual (VM) no Azure, criando um filtro de rede em uma sub-rede ou interface de rede VM. Você pode colocar esses filtros, que controlam o tráfego de entrada e saído, em um recurso de toohello do grupo de segurança de rede conectados que recebe o tráfego de saudação. Vamos usar um exemplo comum de tráfego da Web na porta 80. Este artigo mostra como tooopen uma porta tooa VM usando Olá 1.0 da CLI do Azure.


## <a name="cli-versions-toocomplete-hello-task"></a>Tarefa de saudação do CLI versões toocomplete
Você pode concluir a tarefa hello usando uma saudação versões da CLI a seguir:

- [1.0 de CLI do Azure](#quick-commands) – nosso CLI para Olá clássico e o recurso de gerenciamento modelos de implantação (Este artigo)
- [2.0 do CLI do Azure](nsg-quickstart.md) -nossa próxima geração CLI para o modelo de implantação do gerenciamento de recursos de saudação


## <a name="quick-commands"></a>Comandos rápidos
toocreate um grupo de segurança de rede e as regras é necessário [hello Azure CLI 1.0](../../cli-install-nodejs.md) instalado e usando modo de Gerenciador de recursos:

```azurecli
azure config mode arm
```

Em Olá exemplos a seguir, substitua os nomes de parâmetro de exemplo com seus próprios valores. Os nomes de parâmetro de exemplo incluem *myResourceGroup*, *myNetworkSecurityGroup* e *myVnet*.

Crie o Grupo de Segurança de Rede da seguinte forma, inserindo seus próprios nomes e localização adequadamente. Olá, exemplo a seguir cria um grupo de segurança de rede denominado *myNetworkSecurityGroup* em Olá *eastus* local:

```azurecli
azure network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

Adicionar um servidor da Web regra tooallow HTTP tráfego tooyour (ou ajustar para seu próprio cenário, como conectividade de banco de dados ou acesso SSH). Olá, exemplo a seguir cria uma regra denominada *myNetworkSecurityGroupRule* tooallow TCP de tráfego na porta 80:

```azurecli
azure network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --protocol tcp \
    --direction inbound \
    --priority 1000 \
    --destination-port-range 80 \
    --access allow
```

Saudação de associar o grupo de segurança de rede com interface de rede da VM (NIC). Olá, exemplo a seguir associa um NIC existente denominado *myNic* com hello grupo de segurança de rede denominado *myNetworkSecurityGroup*:

```azurecli
azure network nic set \
    --resource-group myResourceGroup \
    --network-security-group-name myNetworkSecurityGroup \
    --name myNic
```

Como alternativa, você pode associar seu grupo de segurança de rede com uma sub-rede da rede virtual em vez de apenas toohello interface de rede em uma única VM. Olá, exemplo a seguir associa uma sub-rede existente denominada *mySubnet* em Olá *myVnet* rede virtual com hello grupo de segurança de rede denominado *myNetworkSecurityGroup*:

```azurecli
azure network vnet subnet set \
    --resource-group myResourceGroup \
    --network-security-group-name myNetworkSecurityGroup \
    --vnet-name myVnet --name mySubnet
```

## <a name="more-information-on-network-security-groups"></a>Mais informações sobre os Grupos de Segurança de Rede
Olá aqui rápido comandos permitem que você tooget para cima e em execução com tooyour de fluxo de tráfego VM. Grupos de segurança de rede fornecem vários recursos excelentes e granularidade para controlar recursos tooyour de acesso. Você pode ler mais sobre a [criação de um Grupo de Segurança de Rede e as regras ACL aqui](../../virtual-network/virtual-networks-create-nsg-arm-cli.md).

Você pode definir Grupos de Segurança de Rede e regras de ACL como parte dos modelos do Azure Resource Manager. Leia mais sobre a [criação de Grupos de Segurança de Rede com modelos](../../virtual-network/virtual-networks-create-nsg-arm-template.md).

Se você precisar toomap de encaminhamento de porta toouse uma porta interna de tooan porta externa exclusivo na sua VM, use um balanceador de carga e regras de conversão de endereço de rede (NAT). Por exemplo, você pode desejar tooexpose TCP porta 8080 externamente e ter tráfego direcionado tooTCP porta 80 em uma máquina virtual. Você pode aprender sobre a [criação de um balanceador de carga para a Internet](../../load-balancer/load-balancer-get-started-internet-arm-cli.md).

## <a name="next-steps"></a>Próximas etapas
Neste exemplo, você criou um tráfego HTTP de tooallow regra simples. Você pode encontrar informações sobre como criar ambientes mais detalhadas no hello artigos a seguir:

* [Visão geral do Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md)
* [O que é um NSG (grupo de segurança de rede)?](../../virtual-network/virtual-networks-nsg.md)
* [Visão Geral do Azure Resource Manager para Balanceadores de Carga](../../load-balancer/load-balancer-arm.md)

