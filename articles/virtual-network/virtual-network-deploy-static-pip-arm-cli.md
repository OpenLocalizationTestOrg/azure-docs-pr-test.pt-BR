---
title: "aaaCreate uma VM com um endereço IP público estático - 2.0 do CLI do Azure | Microsoft Docs"
description: "Saiba como toocreate uma VM com um estático público endereço IP usando hello Azure interface de linha de comando (CLI) 2.0."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 55bc21b0-2a45-4943-a5e7-8d785d0d015c
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 486060463486462dd8336734a7ad23c4a2cba452
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-a-static-public-ip-address-using-hello-azure-cli-20"></a>Criar uma VM com um endereço IP público estático usando Olá 2.0 do CLI do Azure

> [!div class="op_single_selector"]
> * [Portal do Azure](virtual-network-deploy-static-pip-arm-portal.md)
> * [PowerShell](virtual-network-deploy-static-pip-arm-ps.md)
> * [CLI 2.0 do Azure](virtual-network-deploy-static-pip-arm-cli.md)
> * [CLI 1.0 do Azure](virtual-network-deploy-static-pip-cli-nodejs.md)
> * [Modelo](virtual-network-deploy-static-pip-arm-template.md)
> * [PowerShell (Clássico)](virtual-networks-reserved-public-ip.md)

[!INCLUDE [virtual-network-deploy-static-pip-intro-include.md](../../includes/virtual-network-deploy-static-pip-intro-include.md)]

O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e clássico](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json). Este artigo aborda usando o modelo de implantação do hello Gerenciador de recursos, a Microsoft recomenda para a maioria das novas implantações em vez do modelo de implantação clássico hello.

[!INCLUDE [virtual-network-deploy-static-pip-scenario-include.md](../../includes/virtual-network-deploy-static-pip-scenario-include.md)]

## <a name = "create"></a>Criar hello VM

Você pode concluir essa tarefa usando Olá CLI do Azure 2.0 (Este artigo) ou hello [Azure CLI 1.0](virtual-network-deploy-static-pip-cli-nodejs.md). Olá valores em "" para variáveis de saudação nas etapas Olá seguir criar recursos com as configurações do cenário de saudação. Altere os valores hello, conforme apropriado para seu ambiente.

1. Instalar Olá [2.0 do CLI do Azure](/cli/azure/install-az-cli2) se você ainda não tiver instalado.
2. Criar um par de chamadas chaves público e privado SSH para VMs do Linux executando etapas Olá Olá [criar um par de chamadas chaves público e privado SSH para VMs do Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).
3. No shell de comando, faça logon com o comando Olá `az login`.
4. Crie Olá VM executando o script hello seguinte em um computador Linux ou Mac. Olá endereço IP público do Azure, a rede virtual, a interface de rede e recursos de VM devem todas existir no hello mesmo local. Embora recursos Olá não tiverem todos tooexist em hello mesmo grupo de recursos no hello preencham de script a seguir.

```bash
RgName="IaaSStory"
Location="westus"

# Create a resource group.

az group create \
--name $RgName \
--location $Location

# Create a public IP address resource with a static IP address using hello --allocation-method Static option.
# If you do not specify this option, hello address is allocated dynamically. hello address is assigned toothe
# resource from a pool of IP adresses unique tooeach Azure region. hello DnsName must be unique within the
# Azure location it's created in. Download and view hello file from https://www.microsoft.com/en-us/download/details.aspx?id=41653#
# that lists hello ranges for each region.

PipName="PIPWEB1"
DnsName="iaasstoryws1"
az network public-ip create \
--name $PipName \
--resource-group $RgName \
--location $Location \
--allocation-method Static \
--dns-name $DnsName

# Create a virtual network with one subnet

VnetName="TestVNet"
VnetPrefix="192.168.0.0/16"
SubnetName="FrontEnd"
SubnetPrefix="192.168.1.0/24"
az network vnet create \
--name $VnetName \
--resource-group $RgName \
--location $Location \
--address-prefix $VnetPrefix \
--subnet-name $SubnetName \
--subnet-prefix $SubnetPrefix

# Create a network interface connected toohello VNet with a static private IP address and associate hello public IP address
# resource toohello NIC.

NicName="NICWEB1"
PrivateIpAddress="192.168.1.101"
az network nic create \
--name $NicName \
--resource-group $RgName \
--location $Location \
--subnet $SubnetName \
--vnet-name $VnetName \
--private-ip-address $PrivateIpAddress \
--public-ip-address $PipName

# Create a new VM with hello NIC

VmName="WEB1"

# Replace hello value for hello VmSize variable with a value from the
# https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-sizes article.
VmSize="Standard_DS1"

# Replace hello value for hello OsImage variable with a value for *urn* from hello output returned by entering
# hello `az vm image list` command. 

OsImage="credativ:Debian:8:latest"
Username='adminuser'

# Replace hello following value with hello path tooyour public key file.
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
# If creating a Windows VM, remove hello previous line and you'll be prompted for hello password you want tooconfigure for hello VM.
```

Além disso toocreating uma VM, script hello cria:
- Um único premium gerenciado em disco por padrão, mas você tiver outras opções para o tipo de disco de hello, que você pode criar. Saudação de leitura [criar uma VM do Linux usando hello Azure CLI 2.0](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artigo para obter detalhes.
- A Rede virtual, a sub-rede, a NIC e os recursos de endereço IP público. Como alternativa, você pode usar uma rede virtual, uma sub-rede, uma NIC ou recursos de endereço IP público *existentes*. toolearn como toouse existente de recursos de rede em vez de criar recursos adicionais, digite `az vm create -h`.

## <a name = "validate"></a>Como validar a criação da VM e o endereço IP público

1. Digite o comando Olá `az resource list --resouce-group IaaSStory --output table` toosee uma lista de recursos de saudação criados pelo script hello. Deve haver cinco recursos Olá retornado de saída: interface, disco, o endereço IP público, rede virtual e uma máquina virtual de rede.
2. Digite o comando Olá `az network public-ip show --name PIPWEB1 --resource-group IaaSStory --output table`. Em Olá retornado de saída, observe o valor de saudação do **IpAddress** e esse valor de saudação do **PublicIpAllocationMethod** é *estático*.
3. Antes de executar o comando a seguir de saudação, remover <> hello, substitua *Username* com nome hello usado para Olá **Username** variável no script hello e substituir *ipAddress* com hello **ipAddress** da etapa anterior hello. Comando a seguir de execução Olá tooconnect toohello VM: `ssh -i ~/.ssh/azure_id_rsa <Username>@<ipAddress>`. 

## <a name= "clean-up"></a>Remover hello VM e recursos associados

É recomendável que você exclua recursos Olá criados neste exercício, se você não usá-las na produção. Pode haver cobranças da VM, do endereço IP público e dos recursos de disco enquanto forem provisionados. recursos de saudação tooremove criados durante este exercício, Olá concluir as etapas a seguir:

1. recursos de saudação do tooview no grupo de recursos de hello, executar Olá `az resource list --resource-group IaaSStory` comando.
2. Confirme que não existem recursos no grupo de recursos hello, diferente de recursos de saudação criados pelo script hello neste artigo. 
3. toodelete todos os recursos criados neste exercício, execute Olá `az group delete -n IaaSStory` comando. comando Olá exclui o grupo de recursos hello e todos os recursos de saudação nele.

## <a name="next-steps"></a>Próximas etapas

Qualquer tráfego de rede pode fluir tooand de saudação que VM criada neste artigo. Você pode definir regras de entrada e saídas de um NSG que limitam o tráfego de saudação que possa fluir tooand da interface de rede hello, sub-rede hello ou ambos. toolearn mais sobre os NSGs, ler Olá [visão geral do NSG](virtual-networks-nsg.md) artigo.
