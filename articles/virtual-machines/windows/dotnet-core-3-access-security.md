---
title: "aaaAccess e segurança em modelos do Azure para máquinas virtuais do Windows | Microsoft Docs"
description: "Tutorial principal de DotNet da máquina virtual do Azure"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: e671fc45-5e4d-40fd-aac5-290892713cc0
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 4b8227ae745b3b0a22d136e98d18479f8b1504c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="access-and-security-in-azure-resource-manager-templates-for-windows-vms"></a>Acesso e segurança em modelos do Azure Resource Manager para VMs Windows

Aplicativos hospedados no Azure necessidade provavelmente toobe acesso pela hello, internet ou uma VPN / conexão de rota expressa com o Azure. Com o exemplo de aplicativo de repositório de música hello, Olá web site é disponibilizado em Olá internet com um endereço IP público. Com acesso estabelecido, conexões toohello aplicativos e acesso toohello recursos da máquina virtual se devem ser protegidos. Essa segurança de acesso é fornecida com um Grupo de Segurança de Rede. 

Este documento detalha como Olá aplicativo de repositório de música é protegido no modelo de Gerenciador de recursos do Azure do exemplo hello. Todas as dependências e configurações exclusivas são realçadas. Para melhor experiência de hello, pré-implante uma instância do hello solução tooyour assinatura do Azure e trabalha junto com o modelo do Azure Resource Manager hello. modelo completo Olá pode ser encontrado aqui – [implantação de repositório de música no Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).

## <a name="public-ip-address"></a>Endereço IP público
tooprovide acesso público tooan recursos do Azure, um recurso de endereço IP público pode ser usado. O endereço IP público pode ser configurado com um endereço IP estático ou dinâmico. Se um endereço dinâmico é usado e máquina virtual de saudação for interrompida e desalocada, endereços de saudação é removido. Quando a máquina de saudação for iniciada novamente, ele pode ser atribuído um endereço IP público diferente. tooprevent um IP endereço alterem, um endereço IP reservado pode ser usado. 

Um endereço IP público pode ser adicionado o modelo do Azure Resource Manager tooan usando Olá Visual Studio novo Assistente para adicionar recurso, ou inserindo um JSON válido em um modelo. 

Siga este exemplo JSON do link toosee Olá no modelo do Gerenciador de recursos de hello – [endereço IP público](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L110).

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/publicIPAddresses",
  "name": "[variables('publicIpAddressName')]",
  "location": "[resourceGroup().location]",
  "dependsOn": [],
  "tags": {
    "displayName": "public-ip"
  },
  "properties": {
    "publicIPAllocationMethod": "Dynamic",
    "dnsSettings": {
      "domainNameLabel": "[parameters('publicipaddressDnsName')]"
    }
  }
}
```

Um endereço IP público pode ser associado a um adaptador de rede virtual ou a um balanceador de carga. Neste exemplo, porque Olá site do repositório de música carga balanceada entre várias máquinas virtuais, Olá endereço IP público é anexado toohello balanceador de carga.

Siga este exemplo JSON do link toosee Olá no modelo do Gerenciador de recursos de hello – [associação de endereços IP públicos com o balanceador de carga](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L211).

```json
"frontendIPConfigurations": [
  {
    "properties": {
      "publicIPAddress": {
        "id": "[resourceId('Microsoft.Network/publicIPAddresses', variables('publicIpAddressName'))]"
      }
    },
    "name": "LoadBalancerFrontend"
  }
]
```

Olá endereço IP público como visto no hello portal do Azure. Observe que o endereço IP público de saudação é associado tooa balanceador de carga e não uma máquina virtual. Balanceadores de carga de rede são detalhadas no próximo documento hello desta série.

![Endereço IP público](./media/dotnet-core-3-access-security/pubip-win.png)

Para obter mais informações sobre os endereços IP públicos do Azure, consulte [Endereços IP no Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).

## <a name="network-security-group"></a>Grupo de Segurança de Rede
Depois que o acesso foi estabelecida tooAzure recursos, esse acesso deve ser limitado. Para máquinas virtuais do Azure, proteger o acesso é feito usando um grupo de segurança de rede. Com exemplo de aplicativo de repositório de música hello, todas as máquinas de virtuais toohello de acesso é restrito exceto pela porta 80 para acesso http e a porta 3389 para acesso RDP. Um grupo de segurança de rede podem ser adicionado como modelo do Azure Resource Manager tooan usando Olá Visual Studio novo Assistente para adicionar recurso, ou inserindo um JSON válido em um modelo.

Siga este exemplo JSON do link toosee Olá no modelo do Gerenciador de recursos de hello – [grupo de segurança de rede](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L57).

```json
{
  "apiVersion": "2016-03-30",
  "type": "Microsoft.Network/networkSecurityGroups",
  "name": "[variables('networkSecurityGroup')]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "network-security-group"
  },
  "properties": {
    "securityRules": [
      {
        "name": "http",
        "properties": {
          "description": "http endpoint",
          "protocol": "Tcp",
          "sourcePortRange": "*",
          "destinationPortRange": "80",
          "sourceAddressPrefix": "*",
          "destinationAddressPrefix": "*",
          "access": "Allow",
          "priority": 100,
          "direction": "Inbound"
        }
      },
      ........<truncated> 
    ]
  }
},
```

Neste exemplo, o grupo de segurança de rede de Olá é associado ao objeto da sub-rede Olá declarado no recurso de rede Virtual hello. 

Siga este exemplo JSON do link toosee Olá no modelo do Gerenciador de recursos de hello – [associação de grupo de segurança de rede com a rede Virtual](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L143).

```json
"subnets": [
  {
    "name": "[variables('subnetName')]",
    "properties": {
      "addressPrefix": "10.0.0.0/24",
      "networkSecurityGroup": {
        "id": "[resourceId('Microsoft.Network/networkSecurityGroups', variables('networkSecurityGroup'))]"
      }
    }
  }
]
```

É o grupo de segurança de rede Olá semelhante ao seguinte da saudação portal do Azure. Observe que um NSG pode associar-se a um adaptador de sub-rede e/ou rede. Nesse caso, Olá NSG é associado tooa sub-rede. Nessa configuração, hello entradas regras se aplicam tooall máquinas virtuais conectadas toohello sub-rede.

![Grupo de Segurança de Rede](./media/dotnet-core-3-access-security/nsg-win.png)

Para obter informações detalhadas sobre grupos de segurança de rede, leia [O que é um Grupo de Segurança de Rede](https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/).

## <a name="next-step"></a>Próxima etapa
<hr>

[Etapa 3 – Disponibilidade e escala em modelos do Azure Resource Manager](dotnet-core-4-availability-scale.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

