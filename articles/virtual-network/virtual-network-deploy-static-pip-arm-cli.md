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
# <a name="create-a-vm-with-a-static-public-ip-address-using-hello-azure-cli-20"></a><span data-ttu-id="8c7e1-103">Criar uma VM com um endereço IP público estático usando Olá 2.0 do CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="8c7e1-103">Create a VM with a static public IP address using hello Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="8c7e1-104">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="8c7e1-104">Azure portal</span></span>](virtual-network-deploy-static-pip-arm-portal.md)
> * [<span data-ttu-id="8c7e1-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8c7e1-105">PowerShell</span></span>](virtual-network-deploy-static-pip-arm-ps.md)
> * [<span data-ttu-id="8c7e1-106">CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="8c7e1-106">Azure CLI 2.0</span></span>](virtual-network-deploy-static-pip-arm-cli.md)
> * [<span data-ttu-id="8c7e1-107">CLI 1.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="8c7e1-107">Azure CLI 1.0</span></span>](virtual-network-deploy-static-pip-cli-nodejs.md)
> * [<span data-ttu-id="8c7e1-108">Modelo</span><span class="sxs-lookup"><span data-stu-id="8c7e1-108">Template</span></span>](virtual-network-deploy-static-pip-arm-template.md)
> * [<span data-ttu-id="8c7e1-109">PowerShell (Clássico)</span><span class="sxs-lookup"><span data-stu-id="8c7e1-109">PowerShell (Classic)</span></span>](virtual-networks-reserved-public-ip.md)

[!INCLUDE [virtual-network-deploy-static-pip-intro-include.md](../../includes/virtual-network-deploy-static-pip-intro-include.md)]

<span data-ttu-id="8c7e1-110">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e clássico](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8c7e1-110">Azure has two different deployment models for creating and working with resources: [Resource Manager and classic](../resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span> <span data-ttu-id="8c7e1-111">Este artigo aborda usando o modelo de implantação do hello Gerenciador de recursos, a Microsoft recomenda para a maioria das novas implantações em vez do modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="8c7e1-111">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello classic deployment model.</span></span>

[!INCLUDE [virtual-network-deploy-static-pip-scenario-include.md](../../includes/virtual-network-deploy-static-pip-scenario-include.md)]

## <span data-ttu-id="8c7e1-112"><a name = "create"></a>Criar hello VM</span><span class="sxs-lookup"><span data-stu-id="8c7e1-112"><a name = "create"></a>Create hello VM</span></span>

<span data-ttu-id="8c7e1-113">Você pode concluir essa tarefa usando Olá CLI do Azure 2.0 (Este artigo) ou hello [Azure CLI 1.0](virtual-network-deploy-static-pip-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="8c7e1-113">You can complete this task using hello Azure CLI 2.0 (this article) or hello [Azure CLI 1.0](virtual-network-deploy-static-pip-cli-nodejs.md).</span></span> <span data-ttu-id="8c7e1-114">Olá valores em "" para variáveis de saudação nas etapas Olá seguir criar recursos com as configurações do cenário de saudação.</span><span class="sxs-lookup"><span data-stu-id="8c7e1-114">hello values in "" for hello variables in hello steps that follow create resources with settings from hello scenario.</span></span> <span data-ttu-id="8c7e1-115">Altere os valores hello, conforme apropriado para seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="8c7e1-115">Change hello values, as appropriate, for your environment.</span></span>

1. <span data-ttu-id="8c7e1-116">Instalar Olá [2.0 do CLI do Azure](/cli/azure/install-az-cli2) se você ainda não tiver instalado.</span><span class="sxs-lookup"><span data-stu-id="8c7e1-116">Install hello [Azure CLI 2.0](/cli/azure/install-az-cli2) if you don't already have it installed.</span></span>
2. <span data-ttu-id="8c7e1-117">Criar um par de chamadas chaves público e privado SSH para VMs do Linux executando etapas Olá Olá [criar um par de chamadas chaves público e privado SSH para VMs do Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="8c7e1-117">Create an SSH public and private key pair for Linux VMs by completing hello steps in hello [Create an SSH public and private key pair for Linux VMs](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
3. <span data-ttu-id="8c7e1-118">No shell de comando, faça logon com o comando Olá `az login`.</span><span class="sxs-lookup"><span data-stu-id="8c7e1-118">From a command shell, login with hello command `az login`.</span></span>
4. <span data-ttu-id="8c7e1-119">Crie Olá VM executando o script hello seguinte em um computador Linux ou Mac.</span><span class="sxs-lookup"><span data-stu-id="8c7e1-119">Create hello VM by executing hello script that follows on a Linux or Mac computer.</span></span> <span data-ttu-id="8c7e1-120">Olá endereço IP público do Azure, a rede virtual, a interface de rede e recursos de VM devem todas existir no hello mesmo local.</span><span class="sxs-lookup"><span data-stu-id="8c7e1-120">hello Azure public IP address, virtual network, network interface, and VM resources must all exist in hello same location.</span></span> <span data-ttu-id="8c7e1-121">Embora recursos Olá não tiverem todos tooexist em hello mesmo grupo de recursos no hello preencham de script a seguir.</span><span class="sxs-lookup"><span data-stu-id="8c7e1-121">Though hello resources don't all have tooexist in hello same resource group, in hello following script they do.</span></span>

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

<span data-ttu-id="8c7e1-122">Além disso toocreating uma VM, script hello cria:</span><span class="sxs-lookup"><span data-stu-id="8c7e1-122">In addition toocreating a VM, hello script creates:</span></span>
- <span data-ttu-id="8c7e1-123">Um único premium gerenciado em disco por padrão, mas você tiver outras opções para o tipo de disco de hello, que você pode criar.</span><span class="sxs-lookup"><span data-stu-id="8c7e1-123">A single premium managed disk by default, but you have other options for hello disk type you can create.</span></span> <span data-ttu-id="8c7e1-124">Saudação de leitura [criar uma VM do Linux usando hello Azure CLI 2.0](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artigo para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="8c7e1-124">Read hello [Create a Linux VM using hello Azure CLI 2.0](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) article for details.</span></span>
- <span data-ttu-id="8c7e1-125">A Rede virtual, a sub-rede, a NIC e os recursos de endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="8c7e1-125">Virtual network, subnet, NIC, and public IP address resources.</span></span> <span data-ttu-id="8c7e1-126">Como alternativa, você pode usar uma rede virtual, uma sub-rede, uma NIC ou recursos de endereço IP público *existentes*.</span><span class="sxs-lookup"><span data-stu-id="8c7e1-126">Alternatively, you can use *existing* virtual network, subnet, NIC, or public IP address resources.</span></span> <span data-ttu-id="8c7e1-127">toolearn como toouse existente de recursos de rede em vez de criar recursos adicionais, digite `az vm create -h`.</span><span class="sxs-lookup"><span data-stu-id="8c7e1-127">toolearn how toouse existing network resources rather than creating additional resources, enter `az vm create -h`.</span></span>

## <span data-ttu-id="8c7e1-128"><a name = "validate"></a>Como validar a criação da VM e o endereço IP público</span><span class="sxs-lookup"><span data-stu-id="8c7e1-128"><a name = "validate"></a>Validate VM creation and public IP address</span></span>

1. <span data-ttu-id="8c7e1-129">Digite o comando Olá `az resource list --resouce-group IaaSStory --output table` toosee uma lista de recursos de saudação criados pelo script hello.</span><span class="sxs-lookup"><span data-stu-id="8c7e1-129">Enter hello command `az resource list --resouce-group IaaSStory --output table` toosee a list of hello resources created by hello script.</span></span> <span data-ttu-id="8c7e1-130">Deve haver cinco recursos Olá retornado de saída: interface, disco, o endereço IP público, rede virtual e uma máquina virtual de rede.</span><span class="sxs-lookup"><span data-stu-id="8c7e1-130">There should be five resources in hello returned output: network interface, disk, public IP address, virtual network, and a virtual machine.</span></span>
2. <span data-ttu-id="8c7e1-131">Digite o comando Olá `az network public-ip show --name PIPWEB1 --resource-group IaaSStory --output table`.</span><span class="sxs-lookup"><span data-stu-id="8c7e1-131">Enter hello command `az network public-ip show --name PIPWEB1 --resource-group IaaSStory --output table`.</span></span> <span data-ttu-id="8c7e1-132">Em Olá retornado de saída, observe o valor de saudação do **IpAddress** e esse valor de saudação do **PublicIpAllocationMethod** é *estático*.</span><span class="sxs-lookup"><span data-stu-id="8c7e1-132">In hello returned output, note hello value of **IpAddress** and that hello value of **PublicIpAllocationMethod** is *Static*.</span></span>
3. <span data-ttu-id="8c7e1-133">Antes de executar o comando a seguir de saudação, remover <> hello, substitua *Username* com nome hello usado para Olá **Username** variável no script hello e substituir *ipAddress* com hello **ipAddress** da etapa anterior hello.</span><span class="sxs-lookup"><span data-stu-id="8c7e1-133">Before executing hello following command, remove hello <>, replace *Username* with hello name you used for hello **Username** variable in hello script, and replace *ipAddress* with hello **ipAddress** from hello previous step.</span></span> <span data-ttu-id="8c7e1-134">Comando a seguir de execução Olá tooconnect toohello VM: `ssh -i ~/.ssh/azure_id_rsa <Username>@<ipAddress>`.</span><span class="sxs-lookup"><span data-stu-id="8c7e1-134">Run hello following command tooconnect toohello VM: `ssh -i ~/.ssh/azure_id_rsa <Username>@<ipAddress>`.</span></span> 

## <span data-ttu-id="8c7e1-135"><a name= "clean-up"></a>Remover hello VM e recursos associados</span><span class="sxs-lookup"><span data-stu-id="8c7e1-135"><a name= "clean-up"></a>Remove hello VM and associated resources</span></span>

<span data-ttu-id="8c7e1-136">É recomendável que você exclua recursos Olá criados neste exercício, se você não usá-las na produção.</span><span class="sxs-lookup"><span data-stu-id="8c7e1-136">It's recommended that you delete hello resources created in this exercise if you won't use them in production.</span></span> <span data-ttu-id="8c7e1-137">Pode haver cobranças da VM, do endereço IP público e dos recursos de disco enquanto forem provisionados.</span><span class="sxs-lookup"><span data-stu-id="8c7e1-137">VM, public IP address, and disk resources incur charges, as long as they're provisioned.</span></span> <span data-ttu-id="8c7e1-138">recursos de saudação tooremove criados durante este exercício, Olá concluir as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="8c7e1-138">tooremove hello resources created during this exercise, complete hello following steps:</span></span>

1. <span data-ttu-id="8c7e1-139">recursos de saudação do tooview no grupo de recursos de hello, executar Olá `az resource list --resource-group IaaSStory` comando.</span><span class="sxs-lookup"><span data-stu-id="8c7e1-139">tooview hello resources in hello resource group, run hello `az resource list --resource-group IaaSStory` command.</span></span>
2. <span data-ttu-id="8c7e1-140">Confirme que não existem recursos no grupo de recursos hello, diferente de recursos de saudação criados pelo script hello neste artigo.</span><span class="sxs-lookup"><span data-stu-id="8c7e1-140">Confirm there are no resources in hello resource group, other than hello resources created by hello script in this article.</span></span> 
3. <span data-ttu-id="8c7e1-141">toodelete todos os recursos criados neste exercício, execute Olá `az group delete -n IaaSStory` comando.</span><span class="sxs-lookup"><span data-stu-id="8c7e1-141">toodelete all resources created in this exercise, run hello `az group delete -n IaaSStory` command.</span></span> <span data-ttu-id="8c7e1-142">comando Olá exclui o grupo de recursos hello e todos os recursos de saudação nele.</span><span class="sxs-lookup"><span data-stu-id="8c7e1-142">hello command deletes hello resource group and all hello resources it contains.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8c7e1-143">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8c7e1-143">Next steps</span></span>

<span data-ttu-id="8c7e1-144">Qualquer tráfego de rede pode fluir tooand de saudação que VM criada neste artigo.</span><span class="sxs-lookup"><span data-stu-id="8c7e1-144">Any network traffic can flow tooand from hello VM created in this article.</span></span> <span data-ttu-id="8c7e1-145">Você pode definir regras de entrada e saídas de um NSG que limitam o tráfego de saudação que possa fluir tooand da interface de rede hello, sub-rede hello ou ambos.</span><span class="sxs-lookup"><span data-stu-id="8c7e1-145">You can define inbound and outbound rules within an NSG that limit hello traffic that can flow tooand from hello network interface, hello subnet, or both.</span></span> <span data-ttu-id="8c7e1-146">toolearn mais sobre os NSGs, ler Olá [visão geral do NSG](virtual-networks-nsg.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="8c7e1-146">toolearn more about NSGs, read hello [NSG overview](virtual-networks-nsg.md) article.</span></span>
