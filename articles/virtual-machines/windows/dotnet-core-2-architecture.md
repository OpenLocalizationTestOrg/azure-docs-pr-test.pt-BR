---
title: "aaaDeploying recursos de computação do Windows com modelos do Gerenciador de recursos do Azure | Microsoft Docs"
description: "Tutorial principal de DotNet da máquina virtual do Azure"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: b026fe81-1bc1-4899-ac32-886091671498
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: dee228a492b08053713829e156e5b5ba304d7588
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="application-architecture-with-azure-resource-manager-templates-for-windows-vms"></a>Arquitetura de aplicativos com modelos do Azure Resource Manager para VMs Windows

Ao desenvolver uma implantação do Azure Resource Manager, requisitos de computação necessário toobe mapeado tooAzure recursos e serviços. Se um aplicativo consiste em vários pontos de extremidade http, um banco de dados e um serviço de cache de dados, hello recursos do Azure que hospedam cada um desses componentes precisa toobe planejada. Por exemplo, o aplicativo de repositório de música de exemplo hello inclui um aplicativo web que é hospedado em uma máquina virtual e um banco de dados SQL, que é hospedado no banco de dados do SQL Azure. 

Este documento fornece detalhes sobre como os recursos de computação do repositório de música Olá são configurados no modelo de Gerenciador de recursos do Azure do exemplo hello. Todas as dependências e configurações exclusivas são realçadas. Para melhor experiência de hello, pré-implante uma instância do hello solução tooyour assinatura do Azure e trabalha junto com o modelo do Azure Resource Manager hello. modelo completo Olá pode ser encontrado aqui – [implantação de repositório de música no Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).

## <a name="virtual-machine"></a>Máquina Virtual
saudação de aplicativo de repositório de música inclui um aplicativo da web onde os clientes podem procurar e comprar músicas. Embora haja vários serviços do Azure que podem hospedar aplicativos Web, para este exemplo, uma máquina virtual é usada. Usando o modelo de repositório de música de exemplo hello, uma máquina virtual é implantada, instalar um servidor web e site do repositório de música Olá instalado e configurado. Para a mesma Olá deste artigo, somente a implantação de máquina virtual Olá é detalhada. configuração de saudação do servidor de web hello e aplicativo hello é detalhada em um artigo posterior.

Modelo tooa usando o Visual Studio adicionar novos recursos do assistente, ou inserindo um JSON válido no modelo de implantação de saudação do hello pode ser adicionada a uma máquina virtual. Ao implantar uma máquina virtual, também são necessários vários recursos relacionados. Se usar o modelo do Visual Studio toocreate hello, esses recursos são criados para você. Se construir manualmente modelo hello, esses recursos devem toobe inserido e configurado.

Siga este exemplo JSON do link toosee Olá no modelo do Gerenciador de recursos de hello – [JSON de máquina Virtual](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L285).

```json
{
  {
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Compute/virtualMachines",
  "name": "[concat(variables('vmName'),copyindex())]",
  "location": "[resourceGroup().location]",
  "copy": {
    "name": "virtualMachineLoop",
    "count": "[parameters('numberOfInstances')]"
  },
  "tags": {
    "displayName": "virtual-machine"
  },
  "dependsOn": [
    "[concat('Microsoft.Storage/storageAccounts/', variables('vhdStorageName'))]",
    "[concat('Microsoft.Compute/availabilitySets/', variables('availabilitySetName'))]",
    "nicLoop"
  ],
  "properties": {
    "availabilitySet": {
      "id": "[resourceId('Microsoft.Compute/availabilitySets', variables('availabilitySetName'))]"
    },
  ........<truncated>  
}
```

Uma vez implantado, propriedades de máquina virtual Olá podem ser vistas no hello portal do Azure.

![Máquina Virtual](./media/dotnet-core-2-architecture/vm-win.png)

## <a name="storage-account"></a>Conta de armazenamento
Contas de armazenamento têm muitos recursos e opções de armazenamento. Contexto Olá máquinas virtuais do Azure, uma conta de armazenamento contém discos rígidos virtuais de saudação da máquina virtual de saudação e discos de dados adicionais. exemplo de repositório de música Hello inclui um armazenamento conta toohold Olá disco rígido virtual de cada máquina virtual na implantação de saudação. 

Siga este exemplo JSON do link toosee Olá no modelo do Gerenciador de recursos de hello – [conta de armazenamento](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L98).

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Storage/storageAccounts",
  "name": "[variables('vhdStorageName')]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "storage-account"
  },
  "properties": {
    "accountType": "[variables('vhdStorageType')]"
  }
}
```

Uma conta de armazenamento é associado uma máquina virtual dentro da declaração de modelo Olá Gerenciador de recursos de máquina virtual de saudação. 

Siga este exemplo JSON do link toosee Olá no modelo do Gerenciador de recursos de hello – [associação de máquina Virtual e a conta de armazenamento](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L321).

```json
"osDisk": {
  "name": "osdisk",
  "vhd": {
    "uri": "[concat(reference(concat('Microsoft.Storage/storageAccounts/',variables('vhdStorageName')), '2015-06-15').primaryEndpoints.blob,'vhds/osdisk', copyindex(), '.vhd')]"
  },
  "caching": "ReadWrite",
  "createOption": "FromImage"
}
```

Após a implantação, a conta de armazenamento Olá pode ser exibida no hello portal do Azure.

![Conta de armazenamento](./media/dotnet-core-2-architecture/storacct-win.png)

Clicar em um contêiner de blob de conta de armazenamento hello, arquivo de disco rígido virtual Olá para cada máquina virtual implantada com o modelo de saudação pode ser visto.

![Discos rígidos virtuais](./media/dotnet-core-2-architecture/vhd-win.png)

Para obter mais informações sobre o Armazenamento do Azure, consulte a [documentação do Armazenamento do Azure](https://azure.microsoft.com/documentation/services/storage/).

## <a name="virtual-network"></a>Rede Virtual
Se uma máquina virtual requer uma rede interna, como Olá capacidade toocommunicate com outras máquinas virtuais e os recursos do Azure, uma rede Virtual do Azure é necessária.  Uma rede virtual não faz a máquina virtual de saudação acessível pela internet de hello. A conectividade pública exige um endereço IP público, que é detalhado posteriormente nesta série.

Siga este exemplo JSON do link toosee Olá no modelo do Gerenciador de recursos de hello – [rede Virtual e sub-redes](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L126).

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/virtualNetworks",
  "name": "[variables('virtualNetworkName')]",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Network/networkSecurityGroups/', variables('networkSecurityGroup'))]"
  ],
  "tags": {
    "displayName": "virtual-network"
  },
  "properties": {
    "addressSpace": {
      "addressPrefixes": [
        "10.0.0.0/24"
      ]
    },
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
  }
}
```

De Olá portal do Azure, rede virtual Olá parece Olá a imagem a seguir. Observe que todas as máquinas virtuais implantadas com o modelo de saudação rede virtual toohello anexado.

![Rede Virtual](./media/dotnet-core-2-architecture/vnet-win.png)

## <a name="network-interface"></a>Interface de rede
 Uma interface de rede se conecta a uma rede virtual da máquina virtual tooa, mais especificamente sub-rede tooa que foi definido na rede virtual hello. 

 Siga este exemplo JSON do link toosee Olá no modelo do Gerenciador de recursos de hello – [Interface de rede](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L156).

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/networkInterfaces",
  "name": "[concat(variables('networkInterfaceName'), copyindex())]",
  "location": "[resourceGroup().location]",
  "tags": {
    "displayName": "network-interface"
  },
  "copy": {
    "name": "nicLoop",
    "count": "[parameters('numberOfInstances')]"
  },
  "dependsOn": [
    "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]",
    "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]",
    "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIpAddressName'))]",
    "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'), '/inboundNatRules/', 'RDP-VM', copyIndex())]"
  ],
  "properties": {
    "ipConfigurations": [
      {
        "name": "ipconfig",
        "properties": {
          "privateIPAllocationMethod": "Dynamic",
          "subnet": {
            "id": "[variables('subnetRef')]"
          },
          "loadBalancerBackendAddressPools": [
            {
              "id": "[variables('lbPoolID')]"
            }
          ],
          "loadBalancerInboundNatRules": [
            {
              "id": "[concat(variables('lbID'),'/inboundNatRules/RDP-VM', copyIndex())]"
            }
          ]
        }
      }
    ]
  }
}
```

Cada recurso de máquina virtual inclui um perfil de rede. interface de rede Hello está associado a máquina virtual de saudação neste perfil.  

Siga este exemplo JSON do link toosee Olá no modelo do Gerenciador de recursos de hello – [perfil de rede da máquina Virtual](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L330).

```json
"networkProfile": {
  "networkInterfaces": [
    {
      "id": "[resourceId('Microsoft.Network/networkInterfaces', concat(variables('networkInterfaceName'), copyindex()))]"
    }
  ]
}
```

De Olá portal do Azure, interface de rede Olá parece Olá a imagem a seguir. endereço IP interno de saudação e associação de máquina virtual Olá podem ser vistos no recurso de interface de rede de saudação.

![Interface de rede](./media/dotnet-core-2-architecture/nic-win.png)

Para obter mais informações sobre Redes Virtuais do Azure, consulte [Documentação da Rede Virtual do Azure](https://azure.microsoft.com/documentation/services/virtual-network/).

## <a name="azure-sql-database"></a>Banco de Dados SQL do Azure
Além disso, tooa máquina de virtual que hospeda o site do repositório de música hello, um banco de dados do SQL Azure é o banco de dados de repositório de música de Olá toohost implantado. vantagem de saudação do uso de banco de dados do SQL Azure aqui é que um segundo conjunto de máquinas virtuais não é necessário e escala e disponibilidade baseia-se no serviço de saudação.

Um banco de dados do SQL Azure pode ser adicionado usando Olá Visual Studio adicionar novos recursos do assistente, ou inserindo um JSON válido em um modelo. saudação de recurso do SQL Server inclui um nome de usuário e senha que recebeu direitos administrativos na instância do SQL hello. Além disso, um recurso de firewall do SQL é adicionado. Por padrão, os aplicativos hospedados no Azure são capaz de tooconnect com a instância do SQL hello. aplicativo externo tooallow tal um SQL Server Management studio tooconnect toohello instância do SQL, firewall Olá precisa toobe configurado. Para bem Olá de demonstração do repositório de música Olá, a configuração padrão de saudação é suficiente. 

Siga este exemplo JSON do link toosee Olá no modelo do Gerenciador de recursos de hello – [Azure SQL DB](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L379).

```json
{
  "apiVersion": "2014-04-01-preview",
  "type": "Microsoft.Sql/servers",
  "name": "[variables('musicstoresqlName')]",
  "location": "[resourceGroup().location]",
  "dependsOn": [],
  "tags": {
    "displayName": "sql-music-store"
  },
  "properties": {
    "administratorLogin": "[parameters('adminUsername')]",
    "administratorLoginPassword": "[parameters('adminPassword')]"
  },
  "resources": [
    {
      "apiVersion": "2014-04-01-preview",
      "type": "firewallrules",
      "name": "firewall-allow-azure",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Sql/servers/', variables('musicstoresqlName'))]"
      ],
      "properties": {
        "startIpAddress": "0.0.0.0",
        "endIpAddress": "0.0.0.0"
      }
    }
  ]
}
```

Uma exibição de saudação SQL server e banco de dados MusicStore como visto no hello portal do Azure.

![SQL Server](./media/dotnet-core-2-architecture/sql-win.png)

Para obter mais informações sobre como implantar o Banco de Dados SQL do Azure, consulte [Documentação do banco de dados SQL do Azure](https://azure.microsoft.com/documentation/services/sql-database/).

## <a name="next-step"></a>Próxima etapa
<hr>

[Etapa 2 – Acesso e segurança em modelos do Azure Resource Manager](dotnet-core-3-access-security.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

