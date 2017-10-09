---
title: "endereços IP privados de aaaConfigure para VMs - 2.0 do CLI do Azure | Microsoft Docs"
description: "Saiba como tooconfigure endereços IP para máquinas virtuais usando hello Azure interface de linha de comando (CLI) 2.0."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 40b03a1a-ea00-454c-b716-7574cea49ac0
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/16/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0e278e6ac63c0cda061cf70ab0edfaff5491c03b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-using-hello-azure-cli-20"></a>Configurar endereços IP para uma máquina virtual usando Olá 2.0 do CLI do Azure

[!INCLUDE [virtual-networks-static-private-ip-selectors-arm-include](../../includes/virtual-networks-static-private-ip-selectors-arm-include.md)]


## <a name="cli-versions-toocomplete-hello-task"></a>Tarefa de saudação do CLI versões toocomplete 

Você pode concluir a tarefa hello usando uma saudação versões da CLI a seguir: 

- [1.0 de CLI do Azure](virtual-networks-static-private-ip-cli-nodejs.md) – nosso CLI para modelos de implantação de gerenciamento de recursos e clássico de Olá 
- [2.0 do CLI do Azure](#specify-a-static-private-ip-address-when-creating-a-vm) -nossa próxima geração CLI para modelo de implantação de gerenciamento de recursos de saudação (Este artigo)

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

Este artigo aborda o modelo de implantação do Gerenciador de recursos de saudação. Você também pode [gerenciar o endereço IP privado estático no modelo de implantação clássico Olá](virtual-networks-static-private-ip-classic-cli.md).

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

> [!NOTE]
> comandos do Azure CLI 2.0 de exemplo Hello abaixo esperam um ambiente simples já criado. Se você quiser comandos de saudação toorun conforme elas são exibidas neste documento, primeiro criar o ambiente de teste de hello, descrito em [criar uma rede virtual](virtual-networks-create-vnet-arm-cli.md).

## <a name="specify-a-static-private-ip-address-when-creating-a-vm"></a>Especificar um endereço IP estático e privado ao criar uma VM

toocreate uma VM denominada *DNS01* em Olá *front-end* sub-rede de uma rede virtual denominada *TestVNet* com um endereço IP privado estático de *192.168.1.101*, Siga as etapas de saudação abaixo:

1. Se você ainda não tiver ainda, instalar e configurar hello mais recente [2.0 do CLI do Azure](/cli/azure/install-az-cli2) e fazer logon na conta do Azure usando o tooan [logon az](/cli/azure/#login). 

2. Criar um IP público para Olá VM com hello [criar az rede ip público](/cli/azure/network/public-ip#create) comando. lista de saudação mostrada após a saída de hello explica parâmetros Olá usados.

    > [!NOTE]
    > Você pode desejar ou precisar toouse diferentes valores para seus argumentos nesta e as etapas subsequentes, dependendo de seu ambiente.
   
    ```azurecli
    az network public-ip create \
    --name TestPIP \
    --resource-group TestRG \
    --location centralus \
    --allocation-method Static
    ```

    Saída esperada:
   
   ```json
   {
        "publicIp": {
            "idleTimeoutInMinutes": 4,
            "ipAddress": "52.176.43.167",
            "provisioningState": "Succeeded",
            "publicIPAllocationMethod": "Static",
            "resourceGuid": "79e8baa3-33ce-466a-846c-37af3c721ce1"
        }
    }
    ```

   * `--resource-group`: Nome do grupo de recursos de saudação no toocreate Olá IP público.
   * `--name`: Nome do IP público hello.
   * `--location`: Região do azure no toocreate Olá IP público.

3. Executar Olá [nic da rede az criar](/cli/azure/network/nic#create) comando toocreate uma NIC com um endereço IP privado estático. lista de saudação mostrada após a saída de hello explica parâmetros Olá usados. 
   
    ```azurecli
    az network nic create \
    --resource-group TestRG \
    --name TestNIC \
    --location centralus \
    --subnet FrontEnd \
    --private-ip-address 192.168.1.101 \
    --vnet-name TestVNet
    ```

    Saída esperada:
   
    ```json
    {
        "newNIC": {
            "dnsSettings": {
            "appliedDnsServers": [],
            "dnsServers": []
            },
            "enableIPForwarding": false,
            "ipConfigurations": [
            {
                "etag": "W/\"<guid>\"",
                "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC/ipConfigurations/ipconfig1",
                "name": "ipconfig1",
                "properties": {
                "primary": true,
                "privateIPAddress": "192.168.1.101",
                "privateIPAllocationMethod": "Static",
                "provisioningState": "Succeeded",
                "subnet": {
                    "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                    "resourceGroup": "TestRG"
                }
                },
                "resourceGroup": "TestRG"
            }
            ],
            "provisioningState": "Succeeded",
            "resourceGuid": "<guid>"
        }
    }
    ```
    
    Parâmetros:

    * `--private-ip-address`: Endereço IP privado estático para Olá NIC.
    * `--vnet-name`: O nome do VNet Olá no qual toocreate Olá NIC.
    * `--subnet`: O nome da sub-rede de saudação no qual Olá toocreate NIC.

4. Executar Olá [criar vm do azure](/cli/azure/vm/nic#create) saudação do comando toocreate VM usando o IP público hello e NIC criado acima. lista de saudação mostrada após a saída de hello explica parâmetros Olá usados.
   
    ```azurecli
    az vm create \
    --resource-group TestRG \
    --name DNS01 \
    --location centralus \
    --image Debian \
    --admin-username adminuser \
    --ssh-key-value ~/.ssh/id_rsa.pub \
    --nics TestNIC
    ```

    Saída esperada:
   
    ```json
    {
        "fqdns": "",
        "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/DNS01",
        "location": "centralus",
        "macAddress": "00-0D-3A-92-C1-66",
        "powerState": "VM running",
        "privateIpAddress": "192.168.1.101",
        "publicIpAddress": "",
        "resourceGroup": "TestRG"
    }
    ```
   
   Parâmetros diferentes Olá básico [criar vm az](/cli/azure/vm#create) parâmetros.

   * `--nics`: O nome da saudação toowhich da NIC Olá VM está conectado.
   

## <a name="retrieve-static-private-ip-address-information-for-a-vm"></a>Recuperar informações do endereço IP privado estático de uma VM

tooview Olá endereço IP privado estático que você criou, execute Olá após o comando CLI do Azure e observar os valores de saudação para *método de alocação de IP privado* e *endereço IP privado*:

```azurecli
az vm show -g TestRG -n DNS01 --show-details --query 'privateIps'
```

Saída esperada:

```json
"192.168.1.101"
```

toodisplay Olá informações de IP específicas de saudação NIC para a VM, Olá consulta NIC especificamente:

```azurecli
az network nic show \
-g testrg \
-n testnic \
--query 'ipConfigurations[0].{PrivateAddress:privateIpAddress,IPVer:privateIpAddressVersion,IpAllocMethod:p
rivateIpAllocationMethod,PublicAddress:publicIpAddress}'
```

saída de Hello tem esta aparência:

```json
{
    "IPVer": "IPv4",
    "IpAllocMethod": "Static",
    "PrivateAddress": "192.168.1.101",
    "PublicAddress": null
}
```

## <a name="remove-a-static-private-ip-address-from-a-vm"></a>Remover o endereço IP privado estático de uma VM

Você não pode remover um endereço IP privado estático de uma NIC na CLI do Azure para o Resource Manager. Você deve:
- Criar uma nova NIC que usa um IP dinâmico
- Definir Olá NIC em Olá Olá VM recém-criada NIC. 

Olá toochange NIC para Olá VM usada em comandos de saudação acima, siga as etapas de saudação abaixo.

1. Executar Olá **nic de rede do azure criar** comando toocreate uma nova NIC usando a alocação de IP dinâmico com um novo endereço IP. Observe que porque nenhum endereço IP for especificado, o método de alocação Olá **dinâmico**.

    ```azurecli
    az network nic create     \
    --resource-group TestRG     \
    --name TestNIC2     \
    --location centralus     \
    --subnet FrontEnd    \
    --vnet-name TestVNet
    ```        
   
    Saída esperada:

    ```json
    {
        "newNIC": {
            "dnsSettings": {
            "appliedDnsServers": [],
            "dnsServers": []
            },
            "enableIPForwarding": false,
            "ipConfigurations": [
            {
                "etag": "W/\"<guid>\"",
                "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC2/ipConfigurations/ipconfig1",
                "name": "ipconfig1",
                "properties": {
                "primary": true,
                "privateIPAddress": "192.168.1.4",
                "privateIPAllocationMethod": "Dynamic",
                "provisioningState": "Succeeded",
                "subnet": {
                    "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                    "resourceGroup": "TestRG"
                }
                },
                "resourceGroup": "TestRG"
            }
            ],
            "provisioningState": "Succeeded",
            "resourceGuid": "0808a61c-476f-4d08-98ee-0fa83671b010"
        }
    }
    ```

2. Executar Olá **conjunto de vm do azure** saudação do comando toochange NIC usada por Olá VM.
   
    ```azurecli
    azure vm set -g TestRG -n DNS01 -N TestNIC2
    ```

    Saída esperada:
   
    ```json
    [
        {
            "id": "/subscriptions/0e220bf6-5caa-4e9f-8383-51f16b6c109f/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC3",
            "primary": true,
            "resourceGroup": "TestRG"
        }
    ]
    ```

    > [!NOTE]
    > Se Olá VM for grande o suficiente toohave mais de uma NIC, executar Olá **nic de rede do azure excluir** comando toodelete Olá antigo placa de rede.
   
## <a name="next-steps"></a>Próximas etapas
* Saiba mais sobre endereços [IP públicos reservados](virtual-networks-reserved-public-ip.md) .
* Saiba mais sobre endereços [ILPIP (IP público em nível de instância)](virtual-networks-instance-level-public-ip.md) .
* Consulte Olá [APIs de REST de IP reservado](https://msdn.microsoft.com/library/azure/dn722420.aspx).

