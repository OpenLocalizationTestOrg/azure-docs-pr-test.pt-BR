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
# <a name="create-a-vm-with-multiple-nics-using-hello-azure-cli-20"></a><span data-ttu-id="9d71c-103">Criar uma VM com várias NICs usando Olá 2.0 do CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="9d71c-103">Create a VM with multiple NICs using hello Azure CLI 2.0</span></span>

[!INCLUDE [virtual-network-deploy-multinic-arm-selectors-include.md](../../includes/virtual-network-deploy-multinic-arm-selectors-include.md)]

[!INCLUDE [virtual-network-deploy-multinic-intro-include.md](../../includes/virtual-network-deploy-multinic-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="9d71c-104">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e clássico](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="9d71c-104">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="9d71c-105">Este artigo aborda usando o modelo de implantação do hello Gerenciador de recursos, a Microsoft recomenda para a maioria das novas implantações em vez da saudação [modelo de implantação clássico](virtual-network-deploy-multinic-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="9d71c-105">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello [classic deployment model](virtual-network-deploy-multinic-classic-cli.md).</span></span>
>

## <span data-ttu-id="9d71c-106"><a name="create"></a>Criar hello VM</span><span class="sxs-lookup"><span data-stu-id="9d71c-106"><a name="create"></a>Create hello VM</span></span>

<span data-ttu-id="9d71c-107">Você pode concluir essa tarefa usando Olá CLI do Azure 2.0 (Este artigo) ou hello [Azure CLI 1.0](virtual-network-deploy-multinic-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="9d71c-107">You can complete this task using hello Azure CLI 2.0 (this article) or hello [Azure CLI 1.0](virtual-network-deploy-multinic-cli-nodejs.md).</span></span> <span data-ttu-id="9d71c-108">Olá valores em "" para variáveis de saudação nas etapas Olá seguir criar recursos com as configurações do cenário de saudação.</span><span class="sxs-lookup"><span data-stu-id="9d71c-108">hello values in "" for hello variables in hello steps that follow create resources with settings from hello scenario.</span></span> <span data-ttu-id="9d71c-109">Altere os valores hello, conforme apropriado para seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="9d71c-109">Change hello values, as appropriate, for your environment.</span></span>

1. <span data-ttu-id="9d71c-110">Instalar Olá [2.0 do CLI do Azure](/cli/azure/install-az-cli2) se você ainda não tiver instalado.</span><span class="sxs-lookup"><span data-stu-id="9d71c-110">Install hello [Azure CLI 2.0](/cli/azure/install-az-cli2) if you don't already have it installed.</span></span>
2. <span data-ttu-id="9d71c-111">Criar um par de chamadas chaves público e privado SSH para VMs do Linux executando etapas Olá Olá [criar um par de chamadas chaves público e privado SSH para VMs do Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9d71c-111">Create an SSH public and private key pair for Linux VMs by completing hello steps in hello [Create an SSH public and private key pair for Linux VMs](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
3. <span data-ttu-id="9d71c-112">No shell de comando, faça logon com o comando Olá `az login`.</span><span class="sxs-lookup"><span data-stu-id="9d71c-112">From a command shell, login with hello command `az login`.</span></span>
4. <span data-ttu-id="9d71c-113">Crie Olá VM executando o script hello seguinte em um computador Linux ou Mac.</span><span class="sxs-lookup"><span data-stu-id="9d71c-113">Create hello VM by executing hello script that follows on a Linux or Mac computer.</span></span> <span data-ttu-id="9d71c-114">script Hello cria um grupo de recursos, uma rede virtual (VNet) com duas sub-redes e duas NICs de uma VM com hello duas NICs anexado tooit.</span><span class="sxs-lookup"><span data-stu-id="9d71c-114">hello script creates a resource group, one virtual network (VNet) with two subnets, two NICs, and a VM with hello two NICs attached tooit.</span></span> <span data-ttu-id="9d71c-115">Uma saudação NICs é conectado tooone sub-rede e é atribuída um endereço IP estático público e privado.</span><span class="sxs-lookup"><span data-stu-id="9d71c-115">One of hello NICs is connected tooone subnet and is assigned a static public and private IP address.</span></span> <span data-ttu-id="9d71c-116">Hello outra NIC está conectado toohello outra sub-rede e é atribuída um endereço IP privado estático e nenhum endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="9d71c-116">hello other NIC is connected toohello other subnet and is assigned a static private IP address and no public IP address.</span></span> <span data-ttu-id="9d71c-117">Olá NIC, o endereço IP público, a rede virtual e recursos de VM devem todas existir no hello mesmo local e assinatura.</span><span class="sxs-lookup"><span data-stu-id="9d71c-117">hello NIC, public IP address, virtual network, and VM resources must all exist in hello same location and subscription.</span></span> <span data-ttu-id="9d71c-118">Embora recursos Olá não tiverem todos tooexist em hello mesmo grupo de recursos no hello preencham de script a seguir.</span><span class="sxs-lookup"><span data-stu-id="9d71c-118">Though hello resources don't all have tooexist in hello same resource group, in hello following script they do.</span></span>

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

<span data-ttu-id="9d71c-119">Além disso toocreating uma VM com dois NICs, script hello cria:</span><span class="sxs-lookup"><span data-stu-id="9d71c-119">In addition toocreating a VM with two NICs, hello script creates:</span></span>
- <span data-ttu-id="9d71c-120">Um único premium gerenciado em disco por padrão, mas você tiver outras opções para o tipo de disco de hello, que você pode criar.</span><span class="sxs-lookup"><span data-stu-id="9d71c-120">A single premium managed disk by default, but you have other options for hello disk type you can create.</span></span> <span data-ttu-id="9d71c-121">Saudação de leitura [criar uma VM do Linux usando hello Azure CLI 2.0](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artigo para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="9d71c-121">Read hello [Create a Linux VM using hello Azure CLI 2.0](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) article for details.</span></span>
- <span data-ttu-id="9d71c-122">Uma rede virtual com duas sub-redes e um único endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="9d71c-122">A virtual network with two subnets and a single public IP address.</span></span> <span data-ttu-id="9d71c-123">Como alternativa, você pode usar uma rede virtual, uma sub-rede, uma NIC ou recursos de endereço IP público *existentes*.</span><span class="sxs-lookup"><span data-stu-id="9d71c-123">Alternatively, you can use *existing* virtual network, subnet, NIC, or public IP address resources.</span></span> <span data-ttu-id="9d71c-124">toolearn como toouse existente de recursos de rede em vez de criar recursos adicionais, digite `az vm create -h`.</span><span class="sxs-lookup"><span data-stu-id="9d71c-124">toolearn how toouse existing network resources rather than creating additional resources, enter `az vm create -h`.</span></span>

## <span data-ttu-id="9d71c-125"><a name = "validate"></a>Como validar a criação da VM e das NICs</span><span class="sxs-lookup"><span data-stu-id="9d71c-125"><a name = "validate"></a>Validate VM creation and NICs</span></span>

1. <span data-ttu-id="9d71c-126">Digite o comando Olá `az resource list --resouce-group Multi-NIC-VM --output table` toosee uma lista de recursos de saudação criados pelo script hello.</span><span class="sxs-lookup"><span data-stu-id="9d71c-126">Enter hello command `az resource list --resouce-group Multi-NIC-VM --output table` toosee a list of hello resources created by hello script.</span></span> <span data-ttu-id="9d71c-127">Deve haver seis recursos Olá retornado de saída: duas NICs, um disco, um endereço IP público, uma rede virtual e uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9d71c-127">There should be six resources in hello returned output: Two NICs, one disk, one public IP address, one virtual network, and a virtual machine.</span></span>
2. <span data-ttu-id="9d71c-128">Digite o comando Olá `az network public-ip show --name PIP-WEB --resource-group Multi-NIC-VM --output table`.</span><span class="sxs-lookup"><span data-stu-id="9d71c-128">Enter hello command `az network public-ip show --name PIP-WEB --resource-group Multi-NIC-VM --output table`.</span></span> <span data-ttu-id="9d71c-129">Em Olá retornado de saída, observe o valor de saudação do **IpAddress** e esse valor de saudação do **PublicIpAllocationMethod** é *estático*.</span><span class="sxs-lookup"><span data-stu-id="9d71c-129">In hello returned output, note hello value of **IpAddress** and that hello value of **PublicIpAllocationMethod** is *Static*.</span></span>
3. <span data-ttu-id="9d71c-130">Antes de executar Olá comando a seguir, remover <> hello, substitua *Username* com nome hello usado para Olá **Username** variável no script hello e substituir *ipAddress* com hello **ipAddress** da etapa anterior hello.</span><span class="sxs-lookup"><span data-stu-id="9d71c-130">Before running hello following command, remove hello <>, replace *Username* with hello name you used for hello **Username** variable in hello script, and replace *ipAddress* with hello **ipAddress** from hello previous step.</span></span> <span data-ttu-id="9d71c-131">Comando a seguir de execução Olá tooconnect toohello VM: `ssh -i ~/.ssh/azure_id_rsa <Username>@<ipAddress>`.</span><span class="sxs-lookup"><span data-stu-id="9d71c-131">Run hello following command tooconnect toohello VM: `ssh -i ~/.ssh/azure_id_rsa <Username>@<ipAddress>`.</span></span> 
4. <span data-ttu-id="9d71c-132">Uma vez conectado toohello VM, execute Olá `sudo ifconfig` comando toosee *eth0* e *eth1* interfaces.</span><span class="sxs-lookup"><span data-stu-id="9d71c-132">Once connected toohello VM, run hello `sudo ifconfig` command toosee *eth0* and *eth1* interfaces.</span></span> <span data-ttu-id="9d71c-133">Cada NIC recebeu Olá privados endereços IP estáticos especificados no script hello pelos servidores de DHCP do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="9d71c-133">Each NIC has been assigned hello static private IP addresses specified in hello script by hello Azure DHCP servers.</span></span> <span data-ttu-id="9d71c-134">Olá endereços IP e MAC atribuídos toohello NICs não alteram até Olá que VM seja excluída.</span><span class="sxs-lookup"><span data-stu-id="9d71c-134">hello IP and MAC addresses assigned toohello NICs do not change until hello VM is deleted.</span></span> <span data-ttu-id="9d71c-135">É recomendável que você não altere o endereçamento IP dentro de um sistema operacional, como desativar computador de toohello de conectividade.</span><span class="sxs-lookup"><span data-stu-id="9d71c-135">We recommend that you do not change IP addressing within an operating system, as it can disable connectivity toohello computer.</span></span> <span data-ttu-id="9d71c-136">Endereços IP públicos não aparecem no sistema de operacional hello, conforme forem tooand de convertido de endereço de rede do endereço IP privado de saudação por Olá infraestrutura do Azure.</span><span class="sxs-lookup"><span data-stu-id="9d71c-136">Public IP addresses do not appear within hello operating system, as they are network address translated tooand from hello private IP address by hello Azure infrastructure.</span></span>

## <span data-ttu-id="9d71c-137"><a name= "clean-up"></a>Remover hello VM e recursos associados</span><span class="sxs-lookup"><span data-stu-id="9d71c-137"><a name= "clean-up"></a>Remove hello VM and associated resources</span></span>

<span data-ttu-id="9d71c-138">É recomendável que você exclua recursos Olá criados neste exercício, se você não usá-las na produção.</span><span class="sxs-lookup"><span data-stu-id="9d71c-138">It's recommended that you delete hello resources created in this exercise if you won't use them in production.</span></span> <span data-ttu-id="9d71c-139">Pode haver cobranças da VM, do endereço IP público e dos recursos de disco enquanto forem provisionados.</span><span class="sxs-lookup"><span data-stu-id="9d71c-139">VM, public IP address, and disk resources incur charges, as long as they're provisioned.</span></span> <span data-ttu-id="9d71c-140">recursos de saudação tooremove criados durante este exercício, Olá concluir as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="9d71c-140">tooremove hello resources created during this exercise, complete hello following steps:</span></span>
1. <span data-ttu-id="9d71c-141">recursos de saudação do tooview no grupo de recursos de hello, executar Olá `az resource list --resource-group Multi-NIC-VM` comando.</span><span class="sxs-lookup"><span data-stu-id="9d71c-141">tooview hello resources in hello resource group, run hello `az resource list --resource-group Multi-NIC-VM` command.</span></span>
2. <span data-ttu-id="9d71c-142">Confirme que não existem recursos no grupo de recursos hello, diferente de recursos de saudação criados pelo script hello neste artigo.</span><span class="sxs-lookup"><span data-stu-id="9d71c-142">Confirm there are no resources in hello resource group, other than hello resources created by hello script in this article.</span></span> 
3. <span data-ttu-id="9d71c-143">toodelete todos os recursos criados neste exercício, execute Olá `az group delete --name Multi-NIC-VM` comando.</span><span class="sxs-lookup"><span data-stu-id="9d71c-143">toodelete all resources created in this exercise, run hello `az group delete --name Multi-NIC-VM` command.</span></span> <span data-ttu-id="9d71c-144">comando Olá exclui o grupo de recursos hello e todos os recursos de saudação nele.</span><span class="sxs-lookup"><span data-stu-id="9d71c-144">hello command deletes hello resource group and all hello resources it contains.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9d71c-145">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9d71c-145">Next steps</span></span>

<span data-ttu-id="9d71c-146">Qualquer tráfego de rede pode fluir tooand de saudação que VM criada neste artigo.</span><span class="sxs-lookup"><span data-stu-id="9d71c-146">Any network traffic can flow tooand from hello VM created in this article.</span></span> <span data-ttu-id="9d71c-147">Você pode definir regras de entrada e saída dentro de um NSG que limitam o tráfego de saudação que possa fluir tooand de cada interface de rede, cada sub-rede ou ambos.</span><span class="sxs-lookup"><span data-stu-id="9d71c-147">You can define inbound and outbound rules within an NSG that limit hello traffic that can flow tooand from each network interface, each subnet, or both.</span></span> <span data-ttu-id="9d71c-148">toolearn mais sobre os NSGs, ler Olá [visão geral do NSG](virtual-networks-nsg.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="9d71c-148">toolearn more about NSGs, read hello [NSG overview](virtual-networks-nsg.md) article.</span></span>
