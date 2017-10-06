---
title: "aaaVM com vários endereços IP usando Olá 2.0 do CLI do Azure | Microsoft Docs"
description: "Saiba como tooassign vários endereços IP tooa máquina virtual usando Olá 2.0 do CLI do Azure | Gerenciador de recursos."
services: virtual-network
documentationcenter: na
author: anavinahar
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/17/2016
ms.author: annahar
ms.openlocfilehash: 15efd853cc7c31bacb64ed052dabedd3fe4d3079
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="assign-multiple-ip-addresses-toovirtual-machines-using-hello-azure-cli-20"></a>Atribuir vários endereços IP toovirtual máquinas usando Olá 2.0 do CLI do Azure

[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]

Este artigo explica como toocreate uma máquina virtual (VM) por meio de saudação do Azure Resource Manager implantação do modelo usando Olá 2.0 do CLI do Azure. Tooresources criado por meio do modelo de implantação clássico Olá não podem ser atribuídos a vários endereços IP. toolearn mais sobre modelos de implantação do Azure, leia Olá [entender os modelos de implantação](../resource-manager-deployment-model.md) artigo.

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <a name = "create"></a>Criar uma VM com vários endereços IP

Você pode concluir essa tarefa usando Olá CLI do Azure 2.0 (Este artigo) ou hello [Azure CLI 1.0](virtual-network-multiple-ip-addresses-cli-nodejs.md). Altere os valores hello, conforme apropriado para seu ambiente. etapas Olá que seguem explicam como toocreate um exemplo VM com IP vários endereços, conforme descrito no cenário de saudação. Altere os valores da variável em "" e os tipos de endereço IP conforme exigido por sua implementação. 

1. Instalar Olá [2.0 do CLI do Azure](/cli/azure/install-az-cli2) se você ainda não tiver instalado.
2. Criar um par de chamadas chaves público e privado SSH para VMs do Linux executando etapas Olá Olá [criar um par de chamadas chaves público e privado SSH para VMs do Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).
3. No shell de comando, faça logon com o comando Olá `az login` e selecione a assinatura de saudação que você está usando.
4. Crie Olá VM executando o script hello seguinte em um computador Linux ou Mac. script Hello cria um grupo de recursos, uma rede virtual (VNet), uma NIC com três configurações de IP e uma VM com hello duas NICs anexadas tooit. Olá NIC, o endereço IP público, a rede virtual e recursos de VM devem todas existir no hello mesmo local e assinatura. Embora recursos Olá não tiverem todos tooexist em hello mesmo grupo de recursos no hello preencham de script a seguir.

```bash
    
#!/bin/sh
    
RgName="myResourceGroup"
Location="westcentralus"
az group create --name $RgName --location $Location
    
# Create a public IP address resource with a static IP address using hello `--allocation-method Static` option. If you
# do not specify this option, hello address is allocated dynamically. hello address is assigned toohello resource from a pool
# of IP adresses unique tooeach Azure region. Download and view hello file from
# https://www.microsoft.com/en-us/download/details.aspx?id=41653 that lists hello ranges for each region.

PipName="myPublicIP"

# This name must be unique within an Azure location.
DnsName="myDNSName"

az network public-ip create \
--name $PipName \
--resource-group $RgName \
--location $Location \
--dns-name $DnsName\
--allocation-method Static

# Create a virtual network with one subnet

VnetName="myVnet"
VnetPrefix="10.0.0.0/16"
VnetSubnetName="mySubnet"
VnetSubnetPrefix="10.0.0.0/24"

az network vnet create \
--name $VnetName \
--resource-group $RgName \
--location $Location \
--address-prefix $VnetPrefix \
--subnet-name $VnetSubnetName \
--subnet-prefix $VnetSubnetPrefix

# Create a network interface connected toohello subnet and associate hello public IP address tooit. Azure will create the
# first IP configuration with a static private IP address and will associate hello public IP address resource tooit.

NicName="MyNic1"
az network nic create \
--name $NicName \
--resource-group $RgName \
--location $Location \
--subnet $VnetSubnet1Name \
--private-ip-address 10.0.0.4
--vnet-name $VnetName \
--public-ip-address $PipName
    
# Create a second public IP address, a second IP configuration, and associate it toohello NIC. This configuration has a
# static public IP address and a static private IP address.

az network public-ip create \
--resource-group $RgName \
--location $Location \
--name myPublicIP2 \
--dns-name mypublicdns2 \
--allocation-method Static

az network nic ip-config create \
--resource-group $RgName \
--nic-name $NicName \
--name IPConfig-2 \
--private-ip-address 10.0.0.5 \
--public-ip-name myPublicIP2

# Create a third IP configuration, and associate it toohello NIC. This configuration has  static private IP address and # no public IP address.

azure network nic ip-config create \
--resource-group $RgName \
--nic-name $NicName \
--private-ip-address 10.0.0.6 \
--name IPConfig-3

# Note: Though this article assigns all IP configurations tooa single NIC, you can also assign multiple IP configurations
# tooany NIC in a VM. toolearn how toocreate a VM with multiple NICs, read hello Create a VM with multiple NICs 
# article: https://docs.microsoft.com/azure/virtual-network/virtual-network-deploy-multinic-arm-cli.

# Create a VM and attach hello NIC.

VmName="myVm"

# Replace hello value for hello following **VmSize** variable with a value from the
# https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-sizes rticle. hello script fails if hello VM size
# is not supported in hello location you select. Run hello `azure vm sizes --location estcentralus` command tooget a full list
# of VMs in US West Central, for example.

VmSize="Standard_DS1"

# Replace hello value for hello OsImage variable value with a value for *urn* from hello utput returned by entering the
# `az vm image list` command.

OsImage="credativ:Debian:8:latest"

Username="adminuser"

# Replace hello following value with hello path tooyour public key file. If you're creating a Windows VM, remove hello following
# line and you'll be prompted for hello password you want tooconfigure for hello VM.

SshKeyValue="~/.ssh/id_rsa.pub"

az vm create \
--name $VmName \
--resource-group $RgName \
--image $OsImage \
--location $Location \
--size $VmSize \
--nics $NicName \
--admin-username $Username \
--ssh-key-value $SshKeyValue
```

Além disso toocreating uma VM com uma NIC com 3 configurações de IP, script hello cria:

- Um único premium gerenciado em disco por padrão, mas você tiver outras opções para o tipo de disco de hello, que você pode criar. Saudação de leitura [criar uma VM do Linux usando hello Azure CLI 2.0](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artigo para obter detalhes.
- Uma rede virtual com uma sub-rede e dois endereços IP públicos. Como alternativa, você pode usar uma rede virtual, uma sub-rede, uma NIC ou recursos de endereço IP público *existentes*. toolearn como toouse existente de recursos de rede em vez de criar recursos adicionais, digite `az vm create -h`.

Endereços IP públicos têm um valor nominal. toolearn mais sobre endereços IP de preços, ler Olá [preço do endereço IP](https://azure.microsoft.com/pricing/details/ip-addresses) página. Há um número de toohello limite de endereços IP públicos que podem ser usados em uma assinatura. mais sobre os limites de Olá Olá de leitura de toolearn [Azure limita](../azure-subscription-service-limits.md#networking-limits) artigo.

Depois de saudação VM é criada, digite Olá `az network nic show --name MyNic1 --resource-group myResourceGroup` configuração do comando tooview Olá NIC. Digite hello `az network nic ip-config list --nic-name MyNic1 --resource-group myResourceGroup --output table` tooview uma lista de configurações de IP hello associados NIC toohello.

IP privado de saudação adicionar endereços toohello sistema de operacional VM por etapas para seu sistema operacional no Olá Olá [tooa sistema de operacional VM de endereços de IP adicionar](#os-config) deste artigo.

## <a name="add"></a>Adicionar endereços IP tooa VM

Você pode adicionar adicionais pública e privada IP endereços tooan existente NIC completando as etapas de saudação que seguem. exemplos de saudação incrementar Olá [cenário](#Scenario) descrito neste artigo.

1. Abra um shell de comando e completa Olá restantes etapas nesta seção dentro de uma única sessão. Se você ainda não tiver a CLI do Azure instalado e configurado, Olá concluir etapas no hello [instalação CLI do Azure 2.0](/cli/azure/install-az-cli2?toc=%2fazure%2fvirtual-network%2ftoc.json) tooyour de artigo e de logon de conta do Azure com hello `az-login` comando.

2. Conclua as etapas de saudação em uma das seguintes seções, com base nas necessidades de saudação:

    **Adicionar um endereço IP privado**
    
    tooadd um tooa de endereço IP privado NIC, você deve criar uma configuração de IP usando o comando Olá que segue. Olá endereço IP deve ser um endereço não usado para a sub-rede de saudação.

    ```bash
    az network nic ip-config create \
    --resource-group myResourceGroup \
    --nic-name myNic1 \
    --private-ip-address 10.0.0.7 \
    --name IPConfig-4
    ```
    
    Crie quantas configurações forem necessárias, usando nomes de configuração exclusivos e endereços IP privados (para configurações com endereços IP estáticos).

    **Adicionar um endereço IP público**
    
    Um endereço IP público é adicionado ao associá-la tooeither uma nova configuração de IP ou uma configuração de IP existente. Conclua as etapas de saudação em uma saudação próximas seções, você precisa.

    Endereços IP públicos têm um valor nominal. toolearn mais sobre endereços IP de preços, ler Olá [preço do endereço IP](https://azure.microsoft.com/pricing/details/ip-addresses) página. Há um número de toohello limite de endereços IP públicos que podem ser usados em uma assinatura. mais sobre os limites de Olá Olá de leitura de toolearn [Azure limita](../azure-subscription-service-limits.md#networking-limits) artigo.

    - **Associar Olá recurso tooa nova configuração de IP**
    
        Sempre que você adicionar um endereço IP público em uma nova configuração de IP, também deverá adicionar um endereço IP privado, pois todas as configurações de IP devem ter um endereço IP privado. Você pode adicionar um recurso de endereço IP público existente ou criar um novo. toocreate uma nova, digite Olá comando a seguir:
    
        ```bash
        az network public-ip create \
        --resource-group myResourceGroup \
        --location westcentralus \
        --name myPublicIP3 \
        --dns-name mypublicdns3
        ```

        toocreate uma nova configuração de IP com um endereço IP privado estático e Olá associados *myPublicIP3* IP público recurso de endereço, digite Olá comando a seguir:

        ```bash
        az network nic ip-config create \
        --resource-group myResourceGroup \
        --nic-name myNic1 \
        --name IPConfig-5 \
        --private-ip-address 10.0.0.8
        --public-ip-address myPublicIP3
        ```

    - **Configuração de IP existente do hello associar recursos tooan** um recurso de endereço IP público só pode ser a configuração de IP tooan associado que ainda não tiver um associado. Você pode determinar se uma configuração de IP tem um endereço IP público associado inserindo Olá comando a seguir:

        ```bash
        az network nic ip-config list \
        --resource-group myResourceGroup \
        --nic-name myNic1 \
        --query "[?provisioningState=='Succeeded'].{ Name: name, PublicIpAddressId: publicIpAddress.id }" --output table
        ```

        Saída retornada:
    
            Name        PublicIpAddressId
            
            ipconfig1   /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP1
            IPConfig-2  /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP2
            IPConfig-3

        Desde Olá **PublicIpAddressId** coluna *3 IpConfig* não está em branco no hello saída, nenhum recurso de endereço IP público tooit atualmente associado. Você pode adicionar um existente pública IP endereço recurso tooIpConfig-3, ou insira Olá toocreate comando um a seguir:

        ```bash
        az network public-ip create \
        --resource-group  myResourceGroup
        --location westcentralus \
        --name myPublicIP3 \
        --dns-name mypublicdns3 \
        --allocation-method Static
        ```
    
        Digite hello recurso toohello existente IP configuração denominada do endereço IP público do tooassociate Olá de comando a seguir *3 IPConfig*:
    
        ```bash
        az network nic ip-config update \
        --resource-group myResourceGroup \
        --nic-name myNic1 \
        --name IPConfig-3 \
        --public-ip myPublicIP3
        ```

3. Exibir hello endereços IP privados e Olá público de endereços IP Ids de recursos atribuídas toohello NIC inserindo Olá o comando a seguir:

    ```bash
    az network nic ip-config list \
    --resource-group myResourceGroup \
    --nic-name myNic1 \
    --query "[?provisioningState=='Succeeded'].{ Name: name, PrivateIpAddress: privateIpAddress, PrivateIpAllocationMethod: privateIpAllocationMethod, PublicIpAddressId: publicIpAddress.id }" --output table
    ```

    Saída retornada: <br>
    
        Name        PrivateIpAddress    PrivateIpAllocationMethod   PublicIpAddressId
        
        ipconfig1   10.0.0.4            Static                      /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP1
        IPConfig-2  10.0.0.5            Static                      /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP2
        IPConfig-3  10.0.0.6            Static                      /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP3
    

4. Adicionar endereços IP privados Olá adicionado o sistema operacional do toohello NIC toohello VM seguindo instruções Olá Olá [tooa sistema de operacional VM de endereços de IP adicionar](#os-config) deste artigo. Não adicione Olá pública IP endereços toohello sistema operacional.

[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
