---
title: "Implantar recursos de computação do Windows com os modelos do Azure Resource Manager | Microsoft Docs"
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
ms.openlocfilehash: 8a8b888195e52ea9669922a6a00a873025f3c375
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="application-architecture-with-azure-resource-manager-templates-for-windows-vms"></a>Arquitetura de aplicativos com modelos do Azure Resource Manager para VMs Windows

Ao desenvolver uma implantação do Azure Resource Manager, os requisitos de computação precisam ser mapeados para os serviços e recursos do Azure. Se um aplicativo consistir em vários pontos de extremidade http, um banco de dados e um serviço de cache de dados, os recursos do Azure que hospedam cada desses componentes precisarão ser racionalizados. Por exemplo, o aplicativo de Loja de Música de exemplo inclui um aplicativo Web hospedado em uma máquina virtual e um banco de dados SQL, hospedado no banco de dados SQL do Azure. 

Este documento fornece detalhes sobre como os recursos de computação da Loja de Música são configurados no modelo do Azure Resource Manager de exemplo. Todas as dependências e configurações exclusivas são realçadas. Para obter a melhor experiência, pré-implante uma instância da solução em sua assinatura do Azure e trabalhe com o modelo do Azure Resource Manager. O modelo completo pode ser encontrado aqui – [Implantação de Loja de Música no Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).

## <a name="virtual-machine"></a>Máquina Virtual
O aplicativo de Loja de Música inclui um aplicativo Web em que os clientes podem procurar e comprar músicas. Embora haja vários serviços do Azure que podem hospedar aplicativos Web, para este exemplo, uma máquina virtual é usada. Usando o modelo de Loja de Música de exemplo, uma máquina virtual é implantada, um servidor Web é instalado e o site da Loja de Música é instalado e configurado. Neste artigo, apenas a implantação de máquina virtual é detalhada. A configuração do servidor Web e do aplicativo é detalhada em um artigo posterior.

Uma máquina virtual pode ser adicionada a um modelo usando o Assistente para Adicionar Novos Recursos do Visual Studio ou inserindo JSON válido no modelo de implantação. Ao implantar uma máquina virtual, também são necessários vários recursos relacionados. Se usar o Visual Studio para criar o modelo, esses recursos serão criados para você. Se construir manualmente o modelo, esses recursos precisarão ser inseridos e configurados.

Siga este link para ver o exemplo JSON no modelo do Resource Manager – [JSON de máquina virtual](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L285).

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

Uma vez implantado, as propriedades da máquina virtual podem ser vistas no portal do Azure.

![Máquina Virtual](./media/dotnet-core-2-architecture/vm-win.png)

## <a name="storage-account"></a>Conta de armazenamento
Contas de armazenamento têm muitos recursos e opções de armazenamento. Para o contexto de máquinas virtuais do Azure, uma conta de armazenamento mantém os discos rígidos virtuais da máquina virtual e discos de dados adicionais. O exemplo de Loja de Música inclui uma conta de armazenamento para manter o disco rígido virtual de cada máquina virtual na implantação. 

Siga este link para ver o exemplo JSON no modelo do Resource Manager – [Conta de armazenamento](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L98).

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

Uma conta de armazenamento é associada uma máquina virtual dentro da declaração de modelo do Resource Manager da máquina virtual. 

Siga este link para ver o exemplo JSON no modelo do Resource Manager – [Associação de máquina virtual e conta de armazenamento](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L321).

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

Após a implantação, a conta de armazenamento pode ser exibida no portal do Azure.

![Conta de armazenamento](./media/dotnet-core-2-architecture/storacct-win.png)

Clique no contêiner de blob da conta de armazenamento; o arquivo de driver de disco rígido virtual para cada máquina virtual implantada com o modelo pode ser visto.

![Discos rígidos virtuais](./media/dotnet-core-2-architecture/vhd-win.png)

Para obter mais informações sobre o Armazenamento do Azure, consulte a [documentação do Armazenamento do Azure](https://azure.microsoft.com/documentation/services/storage/).

## <a name="virtual-network"></a>Rede Virtual
Se uma máquina virtual requer uma rede interna, como a capacidade de se comunicar com outras máquinas virtuais e recursos do Azure, uma Rede Virtual do Azure é necessária.  Uma rede virtual não torna a máquina virtual acessível pela Internet. A conectividade pública exige um endereço IP público, que é detalhado posteriormente nesta série.

Siga este link para ver o exemplo JSON no modelo do Resource Manager – [Rede virtual e sub-redes](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L126).

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

No portal do Azure, a rede virtual é semelhante à imagem a seguir. Observe que todas as máquinas virtuais implantadas com o modelo estão conectadas à rede virtual.

![Rede Virtual](./media/dotnet-core-2-architecture/vnet-win.png)

## <a name="network-interface"></a>Interface de rede
 Um adaptador de rede conecta uma máquina virtual a uma rede virtual, mais especificamente a uma sub-rede que foi definida na rede virtual. 

 Siga este link para ver o exemplo JSON no modelo do Resource Manager – [Adaptador de rede](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L156).

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

Cada recurso de máquina virtual inclui um perfil de rede. O adaptador de rede está associado a uma máquina virtual neste perfil.  

Siga este link para ver o exemplo JSON no modelo do Resource Manager – [Perfil de rede da máquina virtual](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L330).

```json
"networkProfile": {
  "networkInterfaces": [
    {
      "id": "[resourceId('Microsoft.Network/networkInterfaces', concat(variables('networkInterfaceName'), copyindex()))]"
    }
  ]
}
```

No portal do Azure, o adaptador de rede é semelhante à imagem a seguir. O endereço IP interno e a associação da máquina virtual podem ser vistos no recurso de adaptador de rede.

![Interface de rede](./media/dotnet-core-2-architecture/nic-win.png)

Para obter mais informações sobre Redes Virtuais do Azure, consulte [Documentação da Rede Virtual do Azure](https://azure.microsoft.com/documentation/services/virtual-network/).

## <a name="azure-sql-database"></a>Banco de Dados SQL do Azure
Além de uma máquina virtual que hospeda o site de Loja de Música, um banco de dados SQL do Azure é implantado para hospedar o banco de dados da Loja de Música. A vantagem de usar o banco de dados SQL do Azure aqui é que um segundo conjunto de máquinas virtuais não é necessário, e a escala e a disponibilidade baseiam-se no serviço.

Um banco de dados SQL do Azure pode ser adicionado usando o Assistente para Adicionar Novos Recursos do Visual Studio ou inserindo JSON válido no modelo. O recurso SQL Server inclui um nome de usuário e uma senha que tenha direitos administrativos na instância do SQL. Além disso, um recurso de firewall do SQL é adicionado. Por padrão, os aplicativos hospedados no Azure são capazes de se conectar com a instância do SQL. Para permitir que o aplicativo externo como um SQL Server Management Studio se conecte à instância do SQL, o firewall precisa ser configurado. Para fins de demonstração da Loja de Música, a configuração padrão é suficiente. 

Siga este link para ver o exemplo JSON no modelo do Resource Manager – [Banco de dados SQL do Azure](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L379).

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

Um modo de exibição do SQL Server e do banco de dados MusicStore como visto no portal do Azure.

![SQL Server](./media/dotnet-core-2-architecture/sql-win.png)

Para obter mais informações sobre como implantar o Banco de Dados SQL do Azure, consulte [Documentação do banco de dados SQL do Azure](https://azure.microsoft.com/documentation/services/sql-database/).

## <a name="next-step"></a>Próxima etapa
<hr>

[Etapa 2 – Acesso e segurança em modelos do Azure Resource Manager](dotnet-core-3-access-security.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

