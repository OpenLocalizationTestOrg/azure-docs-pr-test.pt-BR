---
title: "aaaCreate uma VM com várias NICs - 2.0 do CLI do Azure | Microsoft Docs"
description: "Saiba como toocreate uma VM com várias NICs usando Olá 2.0 do CLI do Azure."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 8e906a4b-8583-4a97-9416-ee34cfa09a98
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ac0291a978e2c8682c69104915196cc6c4fcf8dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-multiple-nics-using-hello-azure-cli-20"></a>Criar uma VM com várias NICs usando Olá 2.0 do CLI do Azure

[!INCLUDE [virtual-network-deploy-multinic-arm-selectors-include.md](../../includes/virtual-network-deploy-multinic-arm-selectors-include.md)]

[!INCLUDE [virtual-network-deploy-multinic-intro-include.md](../../includes/virtual-network-deploy-multinic-intro-include.md)]

> [!NOTE]
> O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e clássico](../resource-manager-deployment-model.md).  Este artigo aborda usando o modelo de implantação do hello Gerenciador de recursos, a Microsoft recomenda para a maioria das novas implantações em vez da saudação [modelo de implantação clássico](virtual-network-deploy-multinic-classic-cli.md).
>

## <a name="create"></a>Criar hello VM

Você pode concluir essa tarefa usando Olá CLI do Azure 2.0 (Este artigo) ou hello [Azure CLI 1.0](virtual-network-deploy-multinic-cli-nodejs.md). Olá valores em "" para variáveis de saudação nas etapas Olá seguir criar recursos com as configurações do cenário de saudação. Altere os valores hello, conforme apropriado para seu ambiente.

1. Instalar Olá [2.0 do CLI do Azure](/cli/azure/install-az-cli2) se você ainda não tiver instalado.
2. Criar um par de chamadas chaves público e privado SSH para VMs do Linux executando etapas Olá Olá [criar um par de chamadas chaves público e privado SSH para VMs do Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).
3. No shell de comando, faça logon com o comando Olá `az login`.
4. Crie Olá VM executando o script hello seguinte em um computador Linux ou Mac. script Hello cria um grupo de recursos, uma rede virtual (VNet) com duas sub-redes e duas NICs de uma VM com hello duas NICs anexado tooit. Uma saudação NICs é conectado tooone sub-rede e é atribuída um endereço IP estático público e privado. Hello outra NIC está conectado toohello outra sub-rede e é atribuída um endereço IP privado estático e nenhum endereço IP público. Olá NIC, o endereço IP público, a rede virtual e recursos de VM devem todas existir no hello mesmo local e assinatura. Embora recursos Olá não tiverem todos tooexist em hello mesmo grupo de recursos no hello preencham de script a seguir.

```bash
#!/bin/sh

RgName="Multi-NIC-VM"
Location="westus"

# Create a resource group.
az group create \
--name $RgName \
--location $Location

# hello address is assigned toohello resource from a pool of IP adresses unique tooeach Azure region. 
# Download and view hello file from https://www.microsoft.com/en-us/download/details.aspx?id=41653 that lists
# hello ranges for each region.

PipName="PIP-WEB"
az network public-ip create \
--name $PipName \
--resource-group $RgName \
--location $Location \
--allocation-method Static

# Create a virtual network with one subnet

VnetName="VNet1"
VnetPrefix="10.0.0.0/16"
VnetSubnet1Name="Front-End"
VnetSubnet1Prefix="10.0.0.0/24"
az network vnet create \
--name $VnetName \
--resource-group $RgName \
--location $Location \
--address-prefix $VnetPrefix \
--subnet-name $VnetSubnet1Name \
--subnet-prefix $VnetSubnet1Prefix

# Create a second subnet within hello VNet

VnetSubnet2Name="Back-end"
VnetSubnet2Prefix="10.0.1.0/24"
az network vnet subnet create \
--vnet-name $VnetName \
--resource-group $RgName \
--name $VnetSubnet2Name \
--address-prefix $VnetSubnet2Prefix

# Create a network interface connected tooone of hello subnets. hello NIC is assigned a single dynamic private and
# public IP address by default, but you can instead, assign static addresses, or no public IP address at all.
# You can also assign multiple private or public IP addresses tooeach NIC. toolearn more about IP addressing
# options for NICs, enter hello az network nic create -h command.

Nic1Name="NIC-FE"
PrivateIpAddress1="10.0.0.5"

az network nic create \
--name $Nic1Name \
--resource-group $RgName \
--location $Location \
--subnet $VnetSubnet1Name \
--vnet-name $VnetName \
--private-ip-address $PrivateIpAddress1 \
--public-ip-address $PipName

# Create a second network interface and connect it toohello other subnet. Though multiple NICs attached toohello same
# VM can be connected toodifferent subnets, hello subnets must all be within hello same VNet. Add additional NICs as necessary.

Nic2Name="NIC-BE"
PrivateIpAddress2="10.0.1.5"

az network nic create \
--name $Nic2Name \
--resource-group $RgName \
--location $Location \
--subnet $VnetSubnet2Name \
--vnet-name $VnetName \
--private-ip-address $PrivateIpAddress2

# Create a VM and attach hello two NICs.

VmName="WEB"

# Replace hello value for hello following **VmSize** variable with a value from the
# https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-sizes article. Not all VM sizes support
# more than one NIC, so be sure tooselect a VM size that supports hello number of NICs you want tooattach toohello VM.
# You must create hello VM with at least two NICs if you want tooadd more after VM creation. If you create a VM with
# only one NIC, you can't add additional NICs toohello VM after VM creation, regardless of how many NICs hello VM supports.
# hello VM size specified in hello following variable supports two NICs.

VmSize="Standard_DS2"

# Replace hello value for hello OsImage variable value with a value for *urn* from hello output returned by entering the
# az vm image list command.

OsImage="credativ:Debian:8:latest"

Username="adminuser"

# Replace hello following value with hello path tooyour public key file.

SshKeyValue="~/.ssh/id_rsa.pub"

# Before executing hello following command, add variable names of additional NICs you may have added toohello script that
# you want tooattach toohello VM. If creating a Windows VM, remove hello **ssh-key-value** line and you'll be prompted for
# hello password you want tooconfigure for hello VM.

az vm create \
--name $VmName \
--resource-group $RgName \
--image $OsImage \
--location $Location \
--size $VmSize \
--nics $Nic1Name $Nic2Name \
--admin-username $Username \
--ssh-key-value $SshKeyValue
```

Além disso toocreating uma VM com dois NICs, script hello cria:
- Um único premium gerenciado em disco por padrão, mas você tiver outras opções para o tipo de disco de hello, que você pode criar. Saudação de leitura [criar uma VM do Linux usando hello Azure CLI 2.0](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artigo para obter detalhes.
- Uma rede virtual com duas sub-redes e um único endereço IP público. Como alternativa, você pode usar uma rede virtual, uma sub-rede, uma NIC ou recursos de endereço IP público *existentes*. toolearn como toouse existente de recursos de rede em vez de criar recursos adicionais, digite `az vm create -h`.

## <a name = "validate"></a>Como validar a criação da VM e das NICs

1. Digite o comando Olá `az resource list --resouce-group Multi-NIC-VM --output table` toosee uma lista de recursos de saudação criados pelo script hello. Deve haver seis recursos Olá retornado de saída: duas NICs, um disco, um endereço IP público, uma rede virtual e uma máquina virtual.
2. Digite o comando Olá `az network public-ip show --name PIP-WEB --resource-group Multi-NIC-VM --output table`. Em Olá retornado de saída, observe o valor de saudação do **IpAddress** e esse valor de saudação do **PublicIpAllocationMethod** é *estático*.
3. Antes de executar Olá comando a seguir, remover <> hello, substitua *Username* com nome hello usado para Olá **Username** variável no script hello e substituir *ipAddress* com hello **ipAddress** da etapa anterior hello. Comando a seguir de execução Olá tooconnect toohello VM: `ssh -i ~/.ssh/azure_id_rsa <Username>@<ipAddress>`. 
4. Uma vez conectado toohello VM, execute Olá `sudo ifconfig` comando toosee *eth0* e *eth1* interfaces. Cada NIC recebeu Olá privados endereços IP estáticos especificados no script hello pelos servidores de DHCP do Azure hello. Olá endereços IP e MAC atribuídos toohello NICs não alteram até Olá que VM seja excluída. É recomendável que você não altere o endereçamento IP dentro de um sistema operacional, como desativar computador de toohello de conectividade. Endereços IP públicos não aparecem no sistema de operacional hello, conforme forem tooand de convertido de endereço de rede do endereço IP privado de saudação por Olá infraestrutura do Azure.

## <a name= "clean-up"></a>Remover hello VM e recursos associados

É recomendável que você exclua recursos Olá criados neste exercício, se você não usá-las na produção. Pode haver cobranças da VM, do endereço IP público e dos recursos de disco enquanto forem provisionados. recursos de saudação tooremove criados durante este exercício, Olá concluir as etapas a seguir:
1. recursos de saudação do tooview no grupo de recursos de hello, executar Olá `az resource list --resource-group Multi-NIC-VM` comando.
2. Confirme que não existem recursos no grupo de recursos hello, diferente de recursos de saudação criados pelo script hello neste artigo. 
3. toodelete todos os recursos criados neste exercício, execute Olá `az group delete --name Multi-NIC-VM` comando. comando Olá exclui o grupo de recursos hello e todos os recursos de saudação nele.

## <a name="next-steps"></a>Próximas etapas

Qualquer tráfego de rede pode fluir tooand de saudação que VM criada neste artigo. Você pode definir regras de entrada e saída dentro de um NSG que limitam o tráfego de saudação que possa fluir tooand de cada interface de rede, cada sub-rede ou ambos. toolearn mais sobre os NSGs, ler Olá [visão geral do NSG](virtual-networks-nsg.md) artigo.
