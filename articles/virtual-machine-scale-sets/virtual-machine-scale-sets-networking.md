---
title: "aaaNetworking para conjuntos de escala de máquina virtual do Azure | Microsoft Docs"
description: "Propriedades da rede de configuração dos conjuntos de dimensionamento de máquina virtual do Azure."
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: guybo
ms.openlocfilehash: ef3f0cfe648d2195c051a73987e654f0e15d13bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="networking-for-azure-virtual-machine-scale-sets"></a>Rede para conjuntos de dimensionamento de máquinas virtuais do Azure

Quando você implanta uma escala de máquina virtual do Azure definido por meio do portal hello, determinadas propriedades de rede são padronizadas, por exemplo um balanceador de carga do Azure com as regras de NAT de entrada. Este artigo descreve como toouse alguns hello mais avançados recursos de rede que você pode configurar com escala define.

Você pode configurar todos os recursos de saudação abordados neste artigo usando modelos do Gerenciador de recursos do Azure. Exemplos da CLI do Azure e PowerShell também estão incluídos para os recursos selecionados. Use a CLI 2.10 e o PowerShell 4.2.0 ou posterior.

## <a name="accelerated-networking"></a>Rede Acelerada
Azure [acelerado rede](../virtual-network/virtual-network-create-vm-accelerated-networking.md) melhora o desempenho da rede, permitindo que a máquina virtual do e/s de raiz única (SR-IOV) virtualização tooa. toouse acelerado de rede com conjuntos de escala, defina enableAcceleratedNetworking muito**true** nas configurações de networkInterfaceConfigurations do conjunto de escala. Por exemplo:
```json
"networkProfile": {
    "networkInterfaceConfigurations": [
    {
      "name": "niconfig1",
      "properties": {
        "primary": true,
        "enableAcceleratedNetworking" : true,
        "ipConfigurations": [
          ...
        ]
      }
    }
   ]
}
```

## <a name="create-a-scale-set-that-references-an-existing-azure-load-balancer"></a>Criar um conjunto de dimensionamento que faz referência a um Azure Load Balancer existente
Quando um conjunto de escala é criado usando Olá portal do Azure, um balanceador de carga novo é criado para a maioria das opções de configuração. Se você criar um conjunto de escala, o que precisa tooreference um balanceador de carga, você pode fazer isso usando a CLI. Olá, script de exemplo a seguir cria um balanceador de carga e, em seguida, cria um conjunto de escala, o que faz referência a ela:
```bash
az network lb create -g lbtest -n mylb --vnet-name myvnet --subnet mysubnet --public-ip-address-allocation Static --backend-pool-name mybackendpool

az vmss create -g lbtest -n myvmss --image Canonical:UbuntuServer:16.04-LTS:latest --admin-username negat --ssh-key-value /home/myuser/.ssh/id_rsa.pub --upgrade-policy-mode Automatic --instance-count 3 --vnet-name myvnet --subnet mysubnet --lb mylb --backend-pool-name mybackendpool

```

## <a name="configurable-dns-settings"></a>Configurações DNS configuráveis
Por padrão, conjuntos de escala leva em configurações específicas de DNS Olá Olá rede virtual e sub-rede que foram criados. No entanto, você pode definir configurações de DNS Olá para uma escala definida diretamente.
~
### <a name="creating-a-scale-set-with-configurable-dns-servers"></a>Como criar um conjunto de dimensionamento com servidores DNS configuráveis
toocreate uma escala definida com uma configuração de DNS personalizada usando a CLI 2.0, adicionar Olá **servidores dns -** argumento toohello **vmss criar** separados de comando, seguido por um espaço de endereços ip do servidor. Por exemplo:
```bash
--dns-servers 10.0.0.6 10.0.0.5
```
tooconfigure servidores DNS personalizados em um modelo do Azure, adicione uma escala de toohello propriedade dnsSettings definir networkInterfaceConfigurations seção. Por exemplo:
```json
"dnsSettings":{
    "dnsServers":["10.0.0.6", "10.0.0.5"]
}
```

### <a name="creating-a-scale-set-with-configurable-virtual-machine-domain-names"></a>Como criar um conjunto de dimensionamento com nomes de domínio configuráveis de máquina de virtual
toocreate uma escala definida com um nome DNS personalizado para máquinas virtuais usando a CLI 2.0, adicionar Olá **nome de domínio - vm** argumento toohello **vmss criar** comando, seguido por uma cadeia de caracteres que representa o nome de domínio de saudação.

nome de domínio Olá tooset em um modelo do Azure, adicione um **dnsSettings** conjunto de escalas da propriedade toohello **networkInterfaceConfigurations** seção. Por exemplo:

```json
"networkProfile": {
  "networkInterfaceConfigurations": [
    {
    "name": "nic1",
    "properties": {
      "primary": "true",
      "ipConfigurations": [
      {
        "name": "ip1",
        "properties": {
          "subnet": {
            "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/virtualNetworks/', variables('vnetName'), '/subnets/subnet1')]"
          },
          "publicIPAddressconfiguration": {
            "name": "publicip",
            "properties": {
            "idleTimeoutInMinutes": 10,
              "dnsSettings": {
                "domainNameLabel": "[parameters('vmssDnsName')]"
              }
            }
          }
        }
      }
    ]
    }
}
```

saudação de saída, para um nome de dns da máquina virtual individual seria em Olá formulário a seguir: 
```
<vm><vmindex>.<specifiedVmssDomainNameLabel>
```

## <a name="public-ipv4-per-virtual-machine"></a>IPv4 público por máquina virtual
Em geral, as máquinas de virtuais do conjunto de dimensionamento do Azure não exigem seus próprios endereços IP públicos. Na maioria dos cenários, é mais seguro e econômico tooassociate uma público IP endereço tooa carga balanceador tooan individual máquina virtual ou (também conhecido como um jumpbox), que encaminha entrada máquinas de virtuais conexões tooscale conjunto conforme necessário (por exemplo, por meio de regras de NAT entrada).

No entanto, alguns cenários exigem um conjunto de escala de máquinas virtuais toohave seus endereços IP público endereços. Um exemplo é jogos, onde um console precisa toomake uma conexão direta tooa nuvem máquina virtual, que está fazendo o processamento de jogo física. Outro exemplo é onde necessário toomake conexões externas tooone as máquinas virtuais outra entre regiões em um banco de dados distribuído.

### <a name="creating-a-scale-set-with-public-ip-per-virtual-machine"></a>Como criar um conjunto de dimensionamento com IP público por máquina de virtual
toocreate um conjunto de escala que atribui uma público IP endereço tooeach máquina virtual com 2.0 do CLI, adicionar Olá **-ip público por vm** parâmetro toohello **vmss criar** comando. 

toocreate uma escala definida usando um modelo do Azure, certifique-se de saudação API versão de hello Microsoft.Compute/virtualMachineScaleSets recurso é pelo menos **2017-03-30**e adicione um **publicIpAddressConfiguration**IpConfigurations seção de conjuntos de escala de toohello de propriedade JSON. Por exemplo:

```json
"publicIpAddressConfiguration": {
    "name": "pub1",
    "properties": {
      "idleTimeoutInMinutes": 15
    }
}
```
Modelo de exemplo: [201-vmss-public-ip-linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-public-ip-linux)

### <a name="querying-hello-public-ip-addresses-of-hello-virtual-machines-in-a-scale-set"></a>Consultando o IP público Olá conjunto de endereços de máquinas virtuais de saudação em uma escala
toolist Olá os endereços IP públicos atribuídos tooscale máquinas virtuais de conjunto usando 2.0 do CLI, use Olá **az vmss ips-público-instância-lista** comando.

conjunto de escala de toolist de endereços IP públicos usando o PowerShell, use Olá _AzureRmPublicIpAddress Get_ comando. Por exemplo:
```PowerShell
PS C:\> Get-AzureRmPublicIpAddress -ResourceGroupName myrg -VirtualMachineScaleSetName myvmss
```

Você também pode consulta Olá os endereços IP públicos referenciando a id de recurso de saudação da configuração de endereço IP pública Olá diretamente. Por exemplo:
```PowerShell
PS C:\> Get-AzureRmPublicIpAddress -ResourceGroupName myrg -Name myvmsspip
```

tooquery Olá os endereços IP públicos atribuídos tooscale máquinas virtuais de conjunto usando Olá [Gerenciador de recursos do Azure](https://resources.azure.com), ou Olá API REST do Azure com a versão **2017-03-30** ou superior.

endereços IP públicos de tooview para uma escala definidas usando Olá Gerenciador de recursos, examinar Olá **publicipaddresses** seção em seu conjunto de escala. Por exemplo: https://resources.azure.com/subscriptions/_your_sub_id_/resourceGroups/_your_rg_/providers/Microsoft.Compute/virtualMachineScaleSets/_your_vmss_/publicipaddresses

```
GET https://management.azure.com/subscriptions/{your sub ID}/resourceGroups/{RG name}/providers/Microsoft.Compute/virtualMachineScaleSets/{scale set name}/publicipaddresses?api-version=2017-03-30
```

Saída de exemplo:
```json
{
  "value": [
    {
      "name": "pub1",
      "id": "/subscriptions/your-subscription-id/resourceGroups/your-rg/providers/Microsoft.Compute/virtualMachineScaleSets/pipvmss/virtualMachines/0/networkInterfaces/pipvmssnic/ipConfigurations/yourvmssipconfig/publicIPAddresses/pub1",
      "etag": "W/\"a64060d5-4dea-4379-a11d-b23cd49a3c8d\"",
      "properties": {
        "provisioningState": "Succeeded",
        "resourceGuid": "ee8cb20f-af8e-4cd6-892f-441ae2bf701f",
        "ipAddress": "13.84.190.11",
        "publicIPAddressVersion": "IPv4",
        "publicIPAllocationMethod": "Dynamic",
        "idleTimeoutInMinutes": 15,
        "ipConfiguration": {
          "id": "/subscriptions/your-subscription-id/resourceGroups/your-rg/providers/Microsoft.Compute/virtualMachineScaleSets/yourvmss/virtualMachines/0/networkInterfaces/yourvmssnic/ipConfigurations/yourvmssipconfig"
        }
      }
    },
    {
      "name": "pub1",
      "id": "/subscriptions/your-subscription-id/resourceGroups/your-rg/providers/Microsoft.Compute/virtualMachineScaleSets/yourvmss/virtualMachines/3/networkInterfaces/yourvmssnic/ipConfigurations/yourvmssipconfig/publicIPAddresses/pub1",
      "etag": "W/\"5f6ff30c-a24c-4818-883c-61ebd5f9eee8\"",
      "properties": {
        "provisioningState": "Succeeded",
        "resourceGuid": "036ce266-403f-41bd-8578-d446d7397c2f",
        "ipAddress": "13.84.159.176",
        "publicIPAddressVersion": "IPv4",
        "publicIPAllocationMethod": "Dynamic",
        "idleTimeoutInMinutes": 15,
        "ipConfiguration": {
          "id": "/subscriptions/your-subscription-id/resourceGroups/your-rg/providers/Microsoft.Compute/virtualMachineScaleSets/yourvmss/virtualMachines/3/networkInterfaces/yourvmssnic/ipConfigurations/yourvmssipconfig"
        }
      }
    }
```

## <a name="multiple-ip-addresses-per-nic"></a>Vários endereços IP por NIC
Cada NIC conectada tooa que VM em um conjunto de escala pode ter uma ou mais configurações de IP associadas a ele. Cada configuração é atribuída a um endereço IP privado. Cada configuração também pode ter um recurso de endereço IP público associado a ela. toounderstand quantos endereços IP pode ser atribuído a tooa NIC, e quantos endereços IP públicos, você pode usar em uma assinatura do Azure, consulte muito[limites do Azure](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits).

## <a name="multiple-nics-per-virtual-machine"></a>Várias NICs por máquina virtual
Você pode ter até too8 NICs por máquina virtual, dependendo do tamanho da máquina. número máximo de saudação de NICs por máquina está disponível no hello [artigo de tamanho VM](../virtual-machines/windows/sizes.md). Olá exemplo a seguir é que uma escala Defina o perfil de rede mostrando várias entradas NIC e vários IPs públicos por máquina virtual:
```json
"networkProfile": {
    "networkInterfaceConfigurations": [
        {
        "name": "nic1",
        "properties": {
            "primary": "true",
            "ipConfigurations": [
            {
                "name": "ip1",
                "properties": {
                "subnet": {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/virtualNetworks/', variables('vnetName'), '/subnets/subnet1')]"
                },
                "publicipaddressconfiguration": {
                    "name": "pub1",
                    "properties": {
                    "idleTimeoutInMinutes": 15
                    }
                },
                "loadBalancerInboundNatPools": [
                    {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/inboundNatPools/natPool1')]"
                    }
                ],
                "loadBalancerBackendAddressPools": [
                    {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/backendAddressPools/addressPool1')]"
                    }
                ]
                }
            }
            ]
        }
        },
        {
        "name": "nic2",
        "properties": {
            "primary": "false",
            "ipConfigurations": [
            {
                "name": "ip1",
                "properties": {
                "subnet": {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/virtualNetworks/', variables('vnetName'), '/subnets/subnet1')]"
                },
                "publicipaddressconfiguration": {
                    "name": "pub1",
                    "properties": {
                    "idleTimeoutInMinutes": 15
                    }
                },
                "loadBalancerInboundNatPools": [
                    {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/inboundNatPools/natPool1')]"
                    }
                ],
                "loadBalancerBackendAddressPools": [
                    {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/backendAddressPools/addressPool1')]"
                    }
                ]
                }
            }
            ]
        }
        }
    ]
}
```

## <a name="nsg-per-scale-set"></a>NSG por conjunto de dimensionamento
Grupos de segurança de rede podem ser aplicados diretamente o conjunto de escala tooa, adicionando uma seção de referência toohello rede interface configuração de escala de saudação definir propriedades de máquina virtual.

Por exemplo: 
```
"networkProfile": {
    "networkInterfaceConfigurations": [
        {
            "name": "nic1",
            "properties": {
                "primary": "true",
                "ipConfigurations": [
                    {
                        "name": "ip1",
                        "properties": {
                            "subnet": {
                                "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/virtualNetworks/', variables('vnetName'), '/subnets/subnet1')]"
                            }
                "loadBalancerInboundNatPools": [
                                {
                                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/inboundNatPools/natPool1')]"
                                }
                            ],
                            "loadBalancerBackendAddressPools": [
                                {
                                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/backendAddressPools/addressPool1')]"
                                }
                            ]
                        }
                    }
                ],
                "networkSecurityGroup": {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/networkSecurityGroups/', variables('nsgName'))]"
                }
            }
        }
    ]
}
```

## <a name="next-steps"></a>Próximas etapas
Para obter mais informações sobre redes virtuais do Azure, consulte muito[esta documentação](../virtual-network/virtual-networks-overview.md).
