---
title: aaaAvailability e a escala em modelos do Gerenciador de recursos do Azure | Microsoft Docs
description: "Tutorial principal de DotNet da máquina virtual do Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 8fcfea79-f017-4658-8c51-74242fcfb7f6
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 6f830ca0a64e6b65859312bdf31dc0af59e2b978
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="availability-and-scale-in-azure-resource-manager-templates-for-linux-vms"></a>Disponibilidade e escala em modelos do Azure Resource Manager para VMs Linux

Disponibilidade e escalabilidade consulte toouptime e hello demanda de toomeet de capacidade. Se um aplicativo deve ser o 99,9% de tempo de saudação, ele precisa toohave uma arquitetura que permite que vários recursos de computação simultâneas. Por exemplo, em vez de um único site, uma configuração com um nível mais alto de disponibilidade inclui várias instâncias do mesmo site, com a tecnologia na frente de balanceamento de saudação. Nessa configuração, uma instância do aplicativo hello pode ser desativada para manutenção, enquanto Olá restantes continuar toofunction. Escala em Olá outro lado refere-se por demanda de tooserve de capacidade de aplicativos tooan. Com uma carga aplicativo equilibrado, adicionando ou removendo instâncias de pool de saudação permite que um aplicativo tooscale toomeet na demanda.

Este documento detalha como Olá implantação de exemplo do repositório de música está configurado para disponibilidade e escalabilidade. Todas as dependências e configurações exclusivas são realçadas. Para melhor experiência de hello, pré-implante uma instância do hello solução tooyour assinatura do Azure e trabalha junto com o modelo do Azure Resource Manager hello. modelo completo Olá pode ser encontrado aqui – [implantação de repositório de música no Ubuntu](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-linux).

## <a name="availability-set"></a>Conjunto de disponibilidade
Logicamente, um conjunto de disponibilidade abrange as máquinas virtuais do Azure em hosts físicos e outros componentes de infraestrutura, como fontes de alimentação e hardware de rede física. Conjuntos de disponibilidade garantem que, durante a manutenção, a falha de dispositivo ou outro tempo de inatividade, nem todas as máquinas virtuais sejam afetadas. Um conjunto de disponibilidade podem ser adicionado tooan Azure Resource Manager modelo usando o Visual Studio novo Assistente para adicionar recurso de saudação ou inserindo um JSON válido em um modelo.

Siga este exemplo JSON do link toosee Olá no modelo do Gerenciador de recursos de hello – [conjunto de disponibilidade](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L387).

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Compute/availabilitySets",
  "name": "[variables('availabilitySetName')]",
  "location": "[resourceGroup().location]",
  "dependsOn": [],
  "tags": {
    "displayName": "avalibility-set"
  },
  "properties": {
    "platformUpdateDomainCount": 5,
    "platformFaultDomainCount": 3
  }
}
```

Um conjunto de disponibilidade é declarado como uma propriedade de um recurso de máquina virtual. 

Siga este exemplo JSON do link toosee Olá no modelo do Gerenciador de recursos de hello – [associação de conjunto de disponibilidade com a máquina Virtual](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L313).

```json
"properties": {
  "availabilitySet": {
    "id": "[resourceId('Microsoft.Compute/availabilitySets', variables('availabilitySetName'))]"
  }
```
disponibilidade de saudação definida como visto no hello portal do Azure. Cada máquina virtual e os detalhes sobre a configuração de saudação são descritos aqui.

![Conjunto de disponibilidade](./media/dotnet-core-4-availability-scale/aset.png)

Para obter informações detalhadas sobre conjuntos de disponibilidade, consulte [Gerenciar a disponibilidade das máquinas virtuais](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). 

## <a name="network-load-balancer"></a>Balanceador de carga de rede
Enquanto um conjunto de disponibilidade fornece tolerância a falhas de aplicativo, um balanceador de carga disponibiliza muitas instâncias do aplicativo hello em um único endereço de rede. Várias instâncias de um aplicativo podem ser hospedadas em muitas máquinas virtuais, cada um deles conectado tooa balanceador de carga. Como o aplicativo hello é acessado, rotas de Balanceador de carga Olá Olá solicitação de entrada entre os membros da saudação anexado. Um balanceador de carga podem ser adicionado usando Olá Visual Studio novo Assistente para adicionar recurso, ou inserindo corretamente formatado recursos JSON no modelo do Azure Resource Manager hello.

Siga este exemplo JSON do link toosee Olá no modelo do Gerenciador de recursos de hello – [balanceador de carga de rede](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L208).

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/loadBalancers",
  "name": "[variables('loadBalancerName')]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "load-balancer-front"
  },
  ........<truncated>
}
```

Porque o aplicativo de exemplo hello toohello exposto à internet com um endereço IP público, esse endereço é associado ao balanceador de carga de saudação. 

Siga este exemplo JSON do link toosee Olá no modelo do Gerenciador de recursos de hello – [associação de Balanceador de carga de rede com endereço IP público](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L221).

```json
"frontendIPConfigurations": [
  {
    "properties": {
      "publicIPAddress": {
        "id": "[resourceId('Microsoft.Network/publicIPAddresses', variables('publicipaddressName'))]"
      }
    },
    "name": "LoadBalancerFrontend"
  }
]
```

De Olá portal do Azure, hello visão geral do balanceador de carga de rede exibe associação Olá com endereço IP público de saudação.

![Balanceador de carga de rede](./media/dotnet-core-4-availability-scale/nlb.png)

## <a name="load-balancer-rule"></a>Regra do balanceador de carga
Ao usar um balanceador de carga, regras são configuradas que controlam como o tráfego é balanceado em todos os recursos de saudação que se destina. Com o aplicativo de repositório de música do exemplo hello, o tráfego chega na porta 80 do endereço IP público de saudação e é distribuído entre a porta 80 de todas as máquinas virtuais. 

Siga este exemplo JSON do link toosee Olá no modelo do Gerenciador de recursos de hello – [regra de Balanceador de carga](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L270).

```json
"loadBalancingRules": [
  {
    "name": "[variables('loadBalencerRule')]",
    "properties": {
      "frontendIPConfiguration": {
        "id": "[concat(resourceId('Microsoft.Network/loadBalancers', variables('loadBalancerName')), '/frontendIPConfigurations/LoadBalancerFrontend')]"
      },
      "backendAddressPool": {
        "id": "[variables('lbPoolID')]"
      },
      "protocol": "Tcp",
      "frontendPort": 80,
      "backendPort": 80,
      "enableFloatingIP": false,
      "idleTimeoutInMinutes": 5,
      "probe": {
        "id": "[variables('lbProbeID')]"
      }
    }
  }
]
```

Uma exibição da rede Olá carregar regra do balanceador do portal hello.

![Regra do balanceador de carga de rede](./media/dotnet-core-4-availability-scale/lbrule.png)

## <a name="load-balancer-probe"></a>Investigação do balanceador de carga
Olá balanceador de carga também precisa toomonitor cada máquina virtual para que somente os sistemas de toorunning as solicitações sejam atendidas. Esse monitoramento é feito por meio da investigação constante de uma porta predefinida. implantação do repositório de música Olá é configurado tooprobe máquinas de virtuais de porta 80 em todos os incluídos. 

Siga este exemplo JSON do link toosee Olá no modelo do Gerenciador de recursos de hello – [investigação do balanceador de carga](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L257).

```json
"probes": [
  {
    "properties": {
      "protocol": "Tcp",
      "port": 80,
      "intervalInSeconds": 15,
      "numberOfProbes": 2
    },
    "name": "lbprobe"
  }
]
```

investigação do balanceador de carga Olá Vista de saudação portal do Azure.

![Investigação do balanceador de carga de rede](./media/dotnet-core-4-availability-scale/lbprobe.png)

## <a name="inbound-nat-rules"></a>Regras NAT de Entrada
Ao usar um balanceador de carga, regras necessário toobe colocados em prática que fornecem acesso com balanceamento de carga não tooeach Máquina Virtual. Por exemplo, ao criar uma conexão SSH com cada máquina virtual, esse tráfego não deve ter o balanceamento de carga, em vez disso, um caminho predeterminado deve ser configurado. Caminhos predeterminados são configurados usando um recurso de regra NAT de entrada. Usando esse recurso, a comunicação de entrada pode ser mapeada tooindividual máquinas virtuais. 

Com hello aplicativo de repositório de música, uma porta começando em 5000 é mapeada tooport 22 em cada máquina Virtual para acesso SSH. Olá `copyindex()` função é usada tooincrement Olá porta de entrada, como aquela Olá segunda máquina Virtual recebe uma porta de entrada de 5001, Olá 5002 terceiro e assim por diante. 

Siga este exemplo JSON do link toosee Olá no modelo do Gerenciador de recursos de hello – [regras de NAT de entrada](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L270). 

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/loadBalancers/inboundNatRules",
  "name": "[concat(variables('loadBalancerName'), '/', 'SSH-VM', copyIndex())]",
  "tags": {
    "displayName": "load-balancer-nat-rule"
  },
  "location": "[resourceGroup().location]",
  "copy": {
    "name": "lbNatLoop",
    "count": "[parameters('numberOfInstances')]"
  },
  "dependsOn": [
    "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]"
  ],
  "properties": {
    "frontendIPConfiguration": {
      "id": "[variables('ipConfigID')]"
    },
    "protocol": "tcp",
    "frontendPort": "[copyIndex(5000)]",
    "backendPort": 22,
    "enableFloatingIP": false
  }
}
```

Um exemplo de regra NAT de entrada como Olá visto no portal do Azure. Uma regra de NAT SSH é criada para cada máquina virtual na implantação de saudação.

![Regra NAT de entrada](./media/dotnet-core-4-availability-scale/natrule.png)

Para obter informações detalhadas sobre Olá balanceador de carga de rede do Azure, consulte [balanceamento de carga para serviços de infraestrutura do Azure](../virtual-machines-linux-load-balance.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="deploy-multiple-vms"></a>Implantar várias VMs
Por fim, para uma função de tooeffectively conjunto de disponibilidade ou o balanceador de carga, várias máquinas virtuais são necessárias. Várias VMs podem ser implantadas usando a função de cópia de modelo hello Azure Resource Manager. Usando a função de cópia hello, não é necessário toodefine um número finito de máquinas virtuais, em vez disso, esse valor pode ser fornecido dinamicamente em tempo de saudação da implantação. função de cópia Olá consome Olá inúmeros toocreated instâncias e identificadores de implantar o número adequado de saudação de máquinas virtuais e recursos associados.

No modelo de exemplo do repositório de música hello, um parâmetro é definido em uma contagem de instâncias. Esse número é usado em todo o modelo de saudação durante a criação de máquinas virtuais e recursos relacionados.

```json
"numberOfInstances": {
  "type": "int",
  "minValue": 1,
  "defaultValue": 1,
  "metadata": {
    "description": "Number of VM instances toobe created behind load balancer."
  }
}
```

Em Olá recurso de máquina Virtual, loop de cópia Olá recebe um nome e número de saudação do parâmetro de instâncias utilizado toocontrol número de saudação de cópias resultantes.

Siga este exemplo JSON do link toosee Olá no modelo do Gerenciador de recursos de hello – [função de cópia de máquina Virtual](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L300). 

```json
"apiVersion": "2015-06-15",
"type": "Microsoft.Compute/virtualMachines",
"name": "[concat(variables('vmName'),copyindex())]",
"location": "[resourceGroup().location]",
"copy": {
  "name": "virtualMachineLoop",
  "count": "[parameters('numberOfInstances')]"
}
```

a iteração atual Olá da função de cópia de saudação pode ser acessada com hello `copyIndex()` função. valor de saudação da função de índice de cópia de saudação pode ser usado tooname máquinas de virtuais e outros recursos. Por exemplo, se duas instâncias de uma máquina virtual forem implantadas, elas terão nomes diferentes. Olá `copyIndex()` função pode ser usada como parte da máquina virtual de saudação nome toocreate um nome exclusivo. Um exemplo de hello `copyindex()` função usada para fins de nomenclatura pode ser vista no hello recurso de máquina Virtual. Aqui, o nome do computador Olá é uma concatenação do hello `vmName` parâmetro e hello `copyIndex()` função. 

Siga este exemplo JSON do link toosee Olá no modelo do Gerenciador de recursos de hello – [função de cópia do índice](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-linux/azuredeploy.json#L319). 

```json
"osProfile": {
  "computerName": "[concat(parameters('vmName'),copyindex())]",
  "adminUsername": "[parameters('adminUsername')]",
  "linuxConfiguration": {
    "disablePasswordAuthentication": "true",
    "ssh": {
      "publicKeys": [
        {
          "path": "[variables('sshKeyPath')]",
          "keyData": "[parameters('sshKeyData')]"
        }
      ]
    }
  }
}
```

Olá `copyIndex` função é usada várias vezes no modelo de exemplo do repositório de música hello. Uso de funções e recursos `copyIndex` incluir qualquer coisa específica tooa única instância de máquina virtual de saudação como interface de rede, regras de Balanceador de carga, e qualquer depende de funções. 

Para obter mais informações sobre a função de cópia hello, consulte [criar várias instâncias de recursos no Gerenciador de recursos do Azure](../../resource-group-create-multiple.md).

## <a name="next-step"></a>Próxima etapa
<hr>

[Etapa 4 – Implantação de aplicativos com modelos do Azure Resource Manager](dotnet-core-5-app-deployment.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

