---
title: "VM com diversos endereços IP usando a CLI 2.0 do Azure | Microsoft Docs"
description: "Aprenda a atribuir diversos endereços IP a uma máquina virtual usando a CLI 2.0 do Azure | Resource Manager."
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
ms.openlocfilehash: 0e9b2ef89ca39a7988a7b2573496a605dfc604b4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="assign-multiple-ip-addresses-to-virtual-machines-using-the-azure-cli-20"></a><span data-ttu-id="19a9d-103">Como atribuir vários endereços IP a máquinas virtuais usando a CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="19a9d-103">Assign multiple IP addresses to virtual machines using the Azure CLI 2.0</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]

<span data-ttu-id="19a9d-104">Este artigo explica como criar uma máquina virtual (VM) por meio do Modelo de implantação do Azure Resource Manager usando a CLI 2.0 do Azure.</span><span class="sxs-lookup"><span data-stu-id="19a9d-104">This article explains how to create a virtual machine (VM) through the Azure Resource Manager deployment model using the Azure CLI 2.0.</span></span> <span data-ttu-id="19a9d-105">Múltiplos endereços IP não podem ser atribuídos a recursos criados por meio do modelo de implantação clássico.</span><span class="sxs-lookup"><span data-stu-id="19a9d-105">Multiple IP addresses cannot be assigned to resources created through the classic deployment model.</span></span> <span data-ttu-id="19a9d-106">Para saber mais sobre modelos de implantação do Azure, leia o artigo [Compreender os modelos de implantação](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="19a9d-106">To learn more about Azure deployment models, read the [Understand deployment models](../resource-manager-deployment-model.md) article.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <span data-ttu-id="19a9d-107"><a name = "create"></a>Criar uma VM com vários endereços IP</span><span class="sxs-lookup"><span data-stu-id="19a9d-107"><a name = "create"></a>Create a VM with multiple IP addresses</span></span>

<span data-ttu-id="19a9d-108">Você pode concluir essa tarefa usando a CLI 2.0 do Azure (este artigo) ou a [CLI 1.0 do Azure](virtual-network-multiple-ip-addresses-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="19a9d-108">You can complete this task using the Azure CLI 2.0 (this article) or the [Azure CLI 1.0](virtual-network-multiple-ip-addresses-cli-nodejs.md).</span></span> <span data-ttu-id="19a9d-109">Altere os valores para adequá-los ao seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="19a9d-109">Change the values, as appropriate, for your environment.</span></span> <span data-ttu-id="19a9d-110">As etapas a seguir explicam como criar uma VM de exemplo com vários endereços IP, como descrito no cenário.</span><span class="sxs-lookup"><span data-stu-id="19a9d-110">The steps that follow explain how to create an example VM with multiple IP addresses, as described in the scenario.</span></span> <span data-ttu-id="19a9d-111">Altere os valores da variável em "" e os tipos de endereço IP conforme exigido por sua implementação.</span><span class="sxs-lookup"><span data-stu-id="19a9d-111">Change variable values in "" and IP address types as required for your implementation.</span></span> 

1. <span data-ttu-id="19a9d-112">Instale a [CLI 2.0 do Azure](/cli/azure/install-az-cli2) se você ainda não tiver instalado.</span><span class="sxs-lookup"><span data-stu-id="19a9d-112">Install the [Azure CLI 2.0](/cli/azure/install-az-cli2) if you don't already have it installed.</span></span>
2. <span data-ttu-id="19a9d-113">Siga as etapas em [Como criar um par de chaves público e privado SSH para VMs do Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json) para criar um par de chaves público e privado SSH para VMs do Linux.</span><span class="sxs-lookup"><span data-stu-id="19a9d-113">Create an SSH public and private key pair for Linux VMs by completing the steps in the [Create an SSH public and private key pair for Linux VMs](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
3. <span data-ttu-id="19a9d-114">Faça logon com o comando `az login` de um shell de comando e selecione a assinatura que você está usando.</span><span class="sxs-lookup"><span data-stu-id="19a9d-114">From a command shell, login with the command `az login` and select the subscription you're using.</span></span>
4. <span data-ttu-id="19a9d-115">Execute o script a seguir em um computador Linux ou Mac para criar a VM.</span><span class="sxs-lookup"><span data-stu-id="19a9d-115">Create the VM by executing the script that follows on a Linux or Mac computer.</span></span> <span data-ttu-id="19a9d-116">O script cria um grupo de recursos, uma rede virtual (VNet), uma NIC com três configurações de IP e uma VM com dois NICs anexados a ela.</span><span class="sxs-lookup"><span data-stu-id="19a9d-116">The script creates a resource group, one virtual network (VNet), one NIC with three IP configurations, and a VM with the two NICs attached to it.</span></span> <span data-ttu-id="19a9d-117">A NIC, o endereço IP público, a rede virtual e os recursos da VM devem existir no mesmo local e assinatura.</span><span class="sxs-lookup"><span data-stu-id="19a9d-117">The NIC, public IP address, virtual network, and VM resources must all exist in the same location and subscription.</span></span> <span data-ttu-id="19a9d-118">Embora não seja obrigatório que todos os recursos existam no mesmo grupo de recursos, no script a seguir é obrigatório.</span><span class="sxs-lookup"><span data-stu-id="19a9d-118">Though the resources don't all have to exist in the same resource group, in the following script they do.</span></span>

```bash
    
#!/bin/sh
    
RgName="myResourceGroup"
Location="westcentralus"
az group create --name $RgName --location $Location
    
# Create a public IP address resource with a static IP address using the `--allocation-method Static` option. If you
# do not specify this option, the address is allocated dynamically. The address is assigned to the resource from a pool
# of IP adresses unique to each Azure region. Download and view the file from
# https://www.microsoft.com/en-us/download/details.aspx?id=41653 that lists the ranges for each region.

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

# Create a network interface connected to the subnet and associate the public IP address to it. Azure will create the
# first IP configuration with a static private IP address and will associate the public IP address resource to it.

NicName="MyNic1"
az network nic create \
--name $NicName \
--resource-group $RgName \
--location $Location \
--subnet $VnetSubnet1Name \
--private-ip-address 10.0.0.4
--vnet-name $VnetName \
--public-ip-address $PipName
    
# Create a second public IP address, a second IP configuration, and associate it to the NIC. This configuration has a
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

# Create a third IP configuration, and associate it to the NIC. This configuration has  static private IP address and   # no public IP address.

azure network nic ip-config create \
--resource-group $RgName \
--nic-name $NicName \
--private-ip-address 10.0.0.6 \
--name IPConfig-3

# Note: Though this article assigns all IP configurations to a single NIC, you can also assign multiple IP configurations
# to any NIC in a VM. To learn how to create a VM with multiple NICs, read the Create a VM with multiple NICs 
# article: https://docs.microsoft.com/azure/virtual-network/virtual-network-deploy-multinic-arm-cli.

# Create a VM and attach the NIC.

VmName="myVm"

# Replace the value for the following **VmSize** variable with a value from the
# https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-sizes rticle. The script fails if the VM size
# is not supported in the location you select. Run the `azure vm sizes --location estcentralus` command to get a full list
# of VMs in US West Central, for example.

VmSize="Standard_DS1"

# Replace the value for the OsImage variable value with a value for *urn* from the utput returned by entering the
# `az vm image list` command.

OsImage="credativ:Debian:8:latest"

Username="adminuser"

# Replace the following value with the path to your public key file. If you're creating a Windows VM, remove the following
# line and you'll be prompted for the password you want to configure for the VM.

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

<span data-ttu-id="19a9d-119">Além de criar uma VM com uma NIC com três configurações de IP, o script cria:</span><span class="sxs-lookup"><span data-stu-id="19a9d-119">In addition to creating a VM with a NIC with 3 IP configurations, the script creates:</span></span>

- <span data-ttu-id="19a9d-120">Um único disco gerenciado premium por padrão, mas há outras opções para você criar outros tipos de disco.</span><span class="sxs-lookup"><span data-stu-id="19a9d-120">A single premium managed disk by default, but you have other options for the disk type you can create.</span></span> <span data-ttu-id="19a9d-121">Veja o artigo [Como criar uma VM do Linux usando a CLI 2.0 do Azure](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="19a9d-121">Read the [Create a Linux VM using the Azure CLI 2.0](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) article for details.</span></span>
- <span data-ttu-id="19a9d-122">Uma rede virtual com uma sub-rede e dois endereços IP públicos.</span><span class="sxs-lookup"><span data-stu-id="19a9d-122">A virtual network with one subnet and two public IP addresses.</span></span> <span data-ttu-id="19a9d-123">Como alternativa, você pode usar uma rede virtual, uma sub-rede, uma NIC ou recursos de endereço IP público *existentes*.</span><span class="sxs-lookup"><span data-stu-id="19a9d-123">Alternatively, you can use *existing* virtual network, subnet, NIC, or public IP address resources.</span></span> <span data-ttu-id="19a9d-124">Para saber como usar os recursos de rede existente em vez de criar recursos adicionais, digite `az vm create -h`.</span><span class="sxs-lookup"><span data-stu-id="19a9d-124">To learn how to use existing network resources rather than creating additional resources, enter `az vm create -h`.</span></span>

<span data-ttu-id="19a9d-125">Endereços IP públicos têm um valor nominal.</span><span class="sxs-lookup"><span data-stu-id="19a9d-125">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="19a9d-126">Para saber mais sobre preços de endereço IP, leia a página [Preços de endereço IP](https://azure.microsoft.com/pricing/details/ip-addresses) .</span><span class="sxs-lookup"><span data-stu-id="19a9d-126">To learn more about IP address pricing, read the [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="19a9d-127">Há um limite para o número de endereços IP públicos que podem ser usados em uma assinatura.</span><span class="sxs-lookup"><span data-stu-id="19a9d-127">There is a limit to the number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="19a9d-128">Para saber mais sobre os limites, leia o artigo [Limites do Azure](../azure-subscription-service-limits.md#networking-limits).</span><span class="sxs-lookup"><span data-stu-id="19a9d-128">To learn more about the limits, read the [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>

<span data-ttu-id="19a9d-129">Depois que a VM é criada, insira o `az network nic show --name MyNic1 --resource-group myResourceGroup` comando para exibir a configuração da NIC.</span><span class="sxs-lookup"><span data-stu-id="19a9d-129">After the VM is created, enter the `az network nic show --name MyNic1 --resource-group myResourceGroup` command to view the NIC configuration.</span></span> <span data-ttu-id="19a9d-130">Insira o `az network nic ip-config list --nic-name MyNic1 --resource-group myResourceGroup --output table` para exibir uma lista das configurações de IP associados à NIC.</span><span class="sxs-lookup"><span data-stu-id="19a9d-130">Enter the `az network nic ip-config list --nic-name MyNic1 --resource-group myResourceGroup --output table` to view a list of the IP configurations associated to the NIC.</span></span>

<span data-ttu-id="19a9d-131">Adicione os endereços IP privados ao sistema operacional da VM executando as etapas para seu sistema operacional na seção [Adicionar endereços IP ao sistema operacional de uma VM](#os-config) deste artigo.</span><span class="sxs-lookup"><span data-stu-id="19a9d-131">Add the private IP addresses to the VM operating system by completing the steps for your operating system in the [Add IP addresses to a VM operating system](#os-config) section of this article.</span></span>

## <span data-ttu-id="19a9d-132"><a name="add"></a>Adicionar endereços IP a uma VM</span><span class="sxs-lookup"><span data-stu-id="19a9d-132"><a name="add"></a>Add IP addresses to a VM</span></span>

<span data-ttu-id="19a9d-133">Você pode adicionar endereços IP públicos e privados adicionais para um NIC existente ao concluir as etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="19a9d-133">You can add additional private and public IP addresses to an existing NIC by completing the steps that follow.</span></span> <span data-ttu-id="19a9d-134">Os exemplos baseiam-se no [cenário](#Scenario) descrito neste artigo.</span><span class="sxs-lookup"><span data-stu-id="19a9d-134">The examples build upon the [scenario](#Scenario) described in this article.</span></span>

1. <span data-ttu-id="19a9d-135">Abra um shell de comando e conclua as etapas restantes nesta seção dentro de uma única sessão.</span><span class="sxs-lookup"><span data-stu-id="19a9d-135">Open a command shell and complete the remaining steps in this section within a single session.</span></span> <span data-ttu-id="19a9d-136">Se você ainda não tiver instalado e configurado a CLI do Azure, conclua as etapas do artigo [Instalação da CLI 2.0 do Azure](/cli/azure/install-az-cli2?toc=%2fazure%2fvirtual-network%2ftoc.json) e faça logon em sua conta do Azure com o comando `az-login`.</span><span class="sxs-lookup"><span data-stu-id="19a9d-136">If you don't already have Azure CLI installed and configured, complete the steps in the [Azure CLI 2.0 installation](/cli/azure/install-az-cli2?toc=%2fazure%2fvirtual-network%2ftoc.json) article and login to your Azure account with the `az-login` command.</span></span>

2. <span data-ttu-id="19a9d-137">Conclua as etapas em uma das seções a seguir, com base em seus requisitos:</span><span class="sxs-lookup"><span data-stu-id="19a9d-137">Complete the steps in one of the following sections, based on your requirements:</span></span>

    <span data-ttu-id="19a9d-138">**Adicionar um endereço IP privado**</span><span class="sxs-lookup"><span data-stu-id="19a9d-138">**Add a private IP address**</span></span>
    
    <span data-ttu-id="19a9d-139">Para adicionar um endereço IP privado a uma NIC, você deve criar uma configuração de IP usando o comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="19a9d-139">To add a private IP address to a NIC, you must create an IP configuration using the command that follows.</span></span> <span data-ttu-id="19a9d-140">O endereço IP estático deve ser um endereço não usado para a sub-rede.</span><span class="sxs-lookup"><span data-stu-id="19a9d-140">The static IP address must be an unused address for the subnet.</span></span>

    ```bash
    az network nic ip-config create \
    --resource-group myResourceGroup \
    --nic-name myNic1 \
    --private-ip-address 10.0.0.7 \
    --name IPConfig-4
    ```
    
    <span data-ttu-id="19a9d-141">Crie quantas configurações forem necessárias, usando nomes de configuração exclusivos e endereços IP privados (para configurações com endereços IP estáticos).</span><span class="sxs-lookup"><span data-stu-id="19a9d-141">Create as many configurations as you require, using unique configuration names and private IP addresses (for configurations with static IP addresses).</span></span>

    <span data-ttu-id="19a9d-142">**Adicionar um endereço IP público**</span><span class="sxs-lookup"><span data-stu-id="19a9d-142">**Add a public IP address**</span></span>
    
    <span data-ttu-id="19a9d-143">Um endereço IP público é adicionado por meio de sua associação a uma nova configuração de IP ou de uma configuração de IP existente.</span><span class="sxs-lookup"><span data-stu-id="19a9d-143">A public IP address is added by associating it to either a new IP configuration or an existing IP configuration.</span></span> <span data-ttu-id="19a9d-144">Conclua as etapas em uma das seções a seguir, quando você precisar.</span><span class="sxs-lookup"><span data-stu-id="19a9d-144">Complete the steps in one of the sections that follow, as you require.</span></span>

    <span data-ttu-id="19a9d-145">Endereços IP públicos têm um valor nominal.</span><span class="sxs-lookup"><span data-stu-id="19a9d-145">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="19a9d-146">Para saber mais sobre preços de endereço IP, leia a página [Preços de endereço IP](https://azure.microsoft.com/pricing/details/ip-addresses) .</span><span class="sxs-lookup"><span data-stu-id="19a9d-146">To learn more about IP address pricing, read the [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="19a9d-147">Há um limite para o número de endereços IP públicos que podem ser usados em uma assinatura.</span><span class="sxs-lookup"><span data-stu-id="19a9d-147">There is a limit to the number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="19a9d-148">Para saber mais sobre os limites, leia o artigo [Limites do Azure](../azure-subscription-service-limits.md#networking-limits).</span><span class="sxs-lookup"><span data-stu-id="19a9d-148">To learn more about the limits, read the [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>

    - <span data-ttu-id="19a9d-149">**Associar o recurso a uma nova configuração de IP**</span><span class="sxs-lookup"><span data-stu-id="19a9d-149">**Associate the resource to a new IP configuration**</span></span>
    
        <span data-ttu-id="19a9d-150">Sempre que você adicionar um endereço IP público em uma nova configuração de IP, também deverá adicionar um endereço IP privado, pois todas as configurações de IP devem ter um endereço IP privado.</span><span class="sxs-lookup"><span data-stu-id="19a9d-150">Whenever you add a public IP address in a new IP configuration, you must also add a private IP address, because all IP configurations must have a private IP address.</span></span> <span data-ttu-id="19a9d-151">Você pode adicionar um recurso de endereço IP público existente ou criar um novo.</span><span class="sxs-lookup"><span data-stu-id="19a9d-151">You can either add an existing public IP address resource, or create a new one.</span></span> <span data-ttu-id="19a9d-152">Para criar um novo, insira o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="19a9d-152">To create a new one, enter the following command:</span></span>
    
        ```bash
        az network public-ip create \
        --resource-group myResourceGroup \
        --location westcentralus \
        --name myPublicIP3 \
        --dns-name mypublicdns3
        ```

        <span data-ttu-id="19a9d-153">Para criar uma nova configuração de IP com um endereço IP privado estático e o recurso de endereço IP público *myPublicIP3* associado, insira o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="19a9d-153">To create a new IP configuration with a static private IP address and the associated *myPublicIP3* public IP address resource, enter the following command:</span></span>

        ```bash
        az network nic ip-config create \
        --resource-group myResourceGroup \
        --nic-name myNic1 \
        --name IPConfig-5 \
        --private-ip-address 10.0.0.8
        --public-ip-address myPublicIP3
        ```

    - <span data-ttu-id="19a9d-154">**Associar o recurso a uma configuração de IP existente** só pode ser associado a uma configuração de IP que ainda não tiver associado um recurso de endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="19a9d-154">**Associate the resource to an existing IP configuration** A public IP address resource can only be associated to an IP configuration that doesn't already have one associated.</span></span> <span data-ttu-id="19a9d-155">Você pode determinar se uma configuração de IP tem um endereço IP público associado inserindo o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="19a9d-155">You can determine whether an IP configuration has an associated public IP address by entering the following command:</span></span>

        ```bash
        az network nic ip-config list \
        --resource-group myResourceGroup \
        --nic-name myNic1 \
        --query "[?provisioningState=='Succeeded'].{ Name: name, PublicIpAddressId: publicIpAddress.id }" --output table
        ```

        <span data-ttu-id="19a9d-156">Saída retornada:</span><span class="sxs-lookup"><span data-stu-id="19a9d-156">Returned output:</span></span>
    
            Name        PublicIpAddressId
            
            ipconfig1   /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP1
            IPConfig-2  /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP2
            IPConfig-3

        <span data-ttu-id="19a9d-157">Como a coluna **PublicIpAddress** para *IpConfig-3* está em branco na saída, nenhum recurso de endereço IP público está associado a ela no momento.</span><span class="sxs-lookup"><span data-stu-id="19a9d-157">Since the **PublicIpAddressId** column for *IpConfig-3* is blank in the output, no public IP address resource is currently associated to it.</span></span> <span data-ttu-id="19a9d-158">Você pode adicionar um recurso de endereço IP público existente como IpConfig-3 ou inserir o seguinte comando para criar um:</span><span class="sxs-lookup"><span data-stu-id="19a9d-158">You can add an existing public IP address resource to IpConfig-3, or enter the following command to create one:</span></span>

        ```bash
        az network public-ip create \
        --resource-group  myResourceGroup
        --location westcentralus \
        --name myPublicIP3 \
        --dns-name mypublicdns3 \
        --allocation-method Static
        ```
    
        <span data-ttu-id="19a9d-159">Insira o comando a seguir para associar o recurso de endereço IP público à configuração de IP existente chamada *IPConfig-3*:</span><span class="sxs-lookup"><span data-stu-id="19a9d-159">Enter the following command to associate the public IP address resource to the existing IP configuration named *IPConfig-3*:</span></span>
    
        ```bash
        az network nic ip-config update \
        --resource-group myResourceGroup \
        --nic-name myNic1 \
        --name IPConfig-3 \
        --public-ip myPublicIP3
        ```

3. <span data-ttu-id="19a9d-160">Digite o seguinte comando para ver os endereços IP privados e os IDs de recurso de endereço IP público atribuídos à NIC:</span><span class="sxs-lookup"><span data-stu-id="19a9d-160">View the private IP addresses and the public IP address resource Ids assigned to the NIC by entering the following command:</span></span>

    ```bash
    az network nic ip-config list \
    --resource-group myResourceGroup \
    --nic-name myNic1 \
    --query "[?provisioningState=='Succeeded'].{ Name: name, PrivateIpAddress: privateIpAddress, PrivateIpAllocationMethod: privateIpAllocationMethod, PublicIpAddressId: publicIpAddress.id }" --output table
    ```

    <span data-ttu-id="19a9d-161">Saída retornada:</span><span class="sxs-lookup"><span data-stu-id="19a9d-161">Returned output:</span></span> <br>
    
        Name        PrivateIpAddress    PrivateIpAllocationMethod   PublicIpAddressId
        
        ipconfig1   10.0.0.4            Static                      /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP1
        IPConfig-2  10.0.0.5            Static                      /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP2
        IPConfig-3  10.0.0.6            Static                      /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP3
    

4. <span data-ttu-id="19a9d-162">Adicione os endereços IP privados que você adicionou à NIC para o sistema operacional da VM seguindo as instruções da seção [Adicionar endereços IP a um sistema operacional de VM](#os-config) deste artigo.</span><span class="sxs-lookup"><span data-stu-id="19a9d-162">Add the private IP addresses you added to the NIC to the VM operating system by following the instructions in the [Add IP addresses to a VM operating system](#os-config) section of this article.</span></span> <span data-ttu-id="19a9d-163">Não adicione os endereços IP públicos ao sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="19a9d-163">Do not add the public IP addresses to the operating system.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
