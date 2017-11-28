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
# <a name="assign-multiple-ip-addresses-toovirtual-machines-using-hello-azure-cli-20"></a><span data-ttu-id="cbfa6-103">Atribuir vários endereços IP toovirtual máquinas usando Olá 2.0 do CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="cbfa6-103">Assign multiple IP addresses toovirtual machines using hello Azure CLI 2.0</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]

<span data-ttu-id="cbfa6-104">Este artigo explica como toocreate uma máquina virtual (VM) por meio de saudação do Azure Resource Manager implantação do modelo usando Olá 2.0 do CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="cbfa6-104">This article explains how toocreate a virtual machine (VM) through hello Azure Resource Manager deployment model using hello Azure CLI 2.0.</span></span> <span data-ttu-id="cbfa6-105">Tooresources criado por meio do modelo de implantação clássico Olá não podem ser atribuídos a vários endereços IP.</span><span class="sxs-lookup"><span data-stu-id="cbfa6-105">Multiple IP addresses cannot be assigned tooresources created through hello classic deployment model.</span></span> <span data-ttu-id="cbfa6-106">toolearn mais sobre modelos de implantação do Azure, leia Olá [entender os modelos de implantação](../resource-manager-deployment-model.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="cbfa6-106">toolearn more about Azure deployment models, read hello [Understand deployment models](../resource-manager-deployment-model.md) article.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <span data-ttu-id="cbfa6-107"><a name = "create"></a>Criar uma VM com vários endereços IP</span><span class="sxs-lookup"><span data-stu-id="cbfa6-107"><a name = "create"></a>Create a VM with multiple IP addresses</span></span>

<span data-ttu-id="cbfa6-108">Você pode concluir essa tarefa usando Olá CLI do Azure 2.0 (Este artigo) ou hello [Azure CLI 1.0](virtual-network-multiple-ip-addresses-cli-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="cbfa6-108">You can complete this task using hello Azure CLI 2.0 (this article) or hello [Azure CLI 1.0](virtual-network-multiple-ip-addresses-cli-nodejs.md).</span></span> <span data-ttu-id="cbfa6-109">Altere os valores hello, conforme apropriado para seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="cbfa6-109">Change hello values, as appropriate, for your environment.</span></span> <span data-ttu-id="cbfa6-110">etapas Olá que seguem explicam como toocreate um exemplo VM com IP vários endereços, conforme descrito no cenário de saudação.</span><span class="sxs-lookup"><span data-stu-id="cbfa6-110">hello steps that follow explain how toocreate an example VM with multiple IP addresses, as described in hello scenario.</span></span> <span data-ttu-id="cbfa6-111">Altere os valores da variável em "" e os tipos de endereço IP conforme exigido por sua implementação.</span><span class="sxs-lookup"><span data-stu-id="cbfa6-111">Change variable values in "" and IP address types as required for your implementation.</span></span> 

1. <span data-ttu-id="cbfa6-112">Instalar Olá [2.0 do CLI do Azure](/cli/azure/install-az-cli2) se você ainda não tiver instalado.</span><span class="sxs-lookup"><span data-stu-id="cbfa6-112">Install hello [Azure CLI 2.0](/cli/azure/install-az-cli2) if you don't already have it installed.</span></span>
2. <span data-ttu-id="cbfa6-113">Criar um par de chamadas chaves público e privado SSH para VMs do Linux executando etapas Olá Olá [criar um par de chamadas chaves público e privado SSH para VMs do Linux](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="cbfa6-113">Create an SSH public and private key pair for Linux VMs by completing hello steps in hello [Create an SSH public and private key pair for Linux VMs](../virtual-machines/linux/mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-network%2ftoc.json).</span></span>
3. <span data-ttu-id="cbfa6-114">No shell de comando, faça logon com o comando Olá `az login` e selecione a assinatura de saudação que você está usando.</span><span class="sxs-lookup"><span data-stu-id="cbfa6-114">From a command shell, login with hello command `az login` and select hello subscription you're using.</span></span>
4. <span data-ttu-id="cbfa6-115">Crie Olá VM executando o script hello seguinte em um computador Linux ou Mac.</span><span class="sxs-lookup"><span data-stu-id="cbfa6-115">Create hello VM by executing hello script that follows on a Linux or Mac computer.</span></span> <span data-ttu-id="cbfa6-116">script Hello cria um grupo de recursos, uma rede virtual (VNet), uma NIC com três configurações de IP e uma VM com hello duas NICs anexadas tooit.</span><span class="sxs-lookup"><span data-stu-id="cbfa6-116">hello script creates a resource group, one virtual network (VNet), one NIC with three IP configurations, and a VM with hello two NICs attached tooit.</span></span> <span data-ttu-id="cbfa6-117">Olá NIC, o endereço IP público, a rede virtual e recursos de VM devem todas existir no hello mesmo local e assinatura.</span><span class="sxs-lookup"><span data-stu-id="cbfa6-117">hello NIC, public IP address, virtual network, and VM resources must all exist in hello same location and subscription.</span></span> <span data-ttu-id="cbfa6-118">Embora recursos Olá não tiverem todos tooexist em hello mesmo grupo de recursos no hello preencham de script a seguir.</span><span class="sxs-lookup"><span data-stu-id="cbfa6-118">Though hello resources don't all have tooexist in hello same resource group, in hello following script they do.</span></span>

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

<span data-ttu-id="cbfa6-119">Além disso toocreating uma VM com uma NIC com 3 configurações de IP, script hello cria:</span><span class="sxs-lookup"><span data-stu-id="cbfa6-119">In addition toocreating a VM with a NIC with 3 IP configurations, hello script creates:</span></span>

- <span data-ttu-id="cbfa6-120">Um único premium gerenciado em disco por padrão, mas você tiver outras opções para o tipo de disco de hello, que você pode criar.</span><span class="sxs-lookup"><span data-stu-id="cbfa6-120">A single premium managed disk by default, but you have other options for hello disk type you can create.</span></span> <span data-ttu-id="cbfa6-121">Saudação de leitura [criar uma VM do Linux usando hello Azure CLI 2.0](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artigo para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="cbfa6-121">Read hello [Create a Linux VM using hello Azure CLI 2.0](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json) article for details.</span></span>
- <span data-ttu-id="cbfa6-122">Uma rede virtual com uma sub-rede e dois endereços IP públicos.</span><span class="sxs-lookup"><span data-stu-id="cbfa6-122">A virtual network with one subnet and two public IP addresses.</span></span> <span data-ttu-id="cbfa6-123">Como alternativa, você pode usar uma rede virtual, uma sub-rede, uma NIC ou recursos de endereço IP público *existentes*.</span><span class="sxs-lookup"><span data-stu-id="cbfa6-123">Alternatively, you can use *existing* virtual network, subnet, NIC, or public IP address resources.</span></span> <span data-ttu-id="cbfa6-124">toolearn como toouse existente de recursos de rede em vez de criar recursos adicionais, digite `az vm create -h`.</span><span class="sxs-lookup"><span data-stu-id="cbfa6-124">toolearn how toouse existing network resources rather than creating additional resources, enter `az vm create -h`.</span></span>

<span data-ttu-id="cbfa6-125">Endereços IP públicos têm um valor nominal.</span><span class="sxs-lookup"><span data-stu-id="cbfa6-125">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="cbfa6-126">toolearn mais sobre endereços IP de preços, ler Olá [preço do endereço IP](https://azure.microsoft.com/pricing/details/ip-addresses) página.</span><span class="sxs-lookup"><span data-stu-id="cbfa6-126">toolearn more about IP address pricing, read hello [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="cbfa6-127">Há um número de toohello limite de endereços IP públicos que podem ser usados em uma assinatura.</span><span class="sxs-lookup"><span data-stu-id="cbfa6-127">There is a limit toohello number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="cbfa6-128">mais sobre os limites de Olá Olá de leitura de toolearn [Azure limita](../azure-subscription-service-limits.md#networking-limits) artigo.</span><span class="sxs-lookup"><span data-stu-id="cbfa6-128">toolearn more about hello limits, read hello [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>

<span data-ttu-id="cbfa6-129">Depois de saudação VM é criada, digite Olá `az network nic show --name MyNic1 --resource-group myResourceGroup` configuração do comando tooview Olá NIC.</span><span class="sxs-lookup"><span data-stu-id="cbfa6-129">After hello VM is created, enter hello `az network nic show --name MyNic1 --resource-group myResourceGroup` command tooview hello NIC configuration.</span></span> <span data-ttu-id="cbfa6-130">Digite hello `az network nic ip-config list --nic-name MyNic1 --resource-group myResourceGroup --output table` tooview uma lista de configurações de IP hello associados NIC toohello.</span><span class="sxs-lookup"><span data-stu-id="cbfa6-130">Enter hello `az network nic ip-config list --nic-name MyNic1 --resource-group myResourceGroup --output table` tooview a list of hello IP configurations associated toohello NIC.</span></span>

<span data-ttu-id="cbfa6-131">IP privado de saudação adicionar endereços toohello sistema de operacional VM por etapas para seu sistema operacional no Olá Olá [tooa sistema de operacional VM de endereços de IP adicionar](#os-config) deste artigo.</span><span class="sxs-lookup"><span data-stu-id="cbfa6-131">Add hello private IP addresses toohello VM operating system by completing hello steps for your operating system in hello [Add IP addresses tooa VM operating system](#os-config) section of this article.</span></span>

## <span data-ttu-id="cbfa6-132"><a name="add"></a>Adicionar endereços IP tooa VM</span><span class="sxs-lookup"><span data-stu-id="cbfa6-132"><a name="add"></a>Add IP addresses tooa VM</span></span>

<span data-ttu-id="cbfa6-133">Você pode adicionar adicionais pública e privada IP endereços tooan existente NIC completando as etapas de saudação que seguem.</span><span class="sxs-lookup"><span data-stu-id="cbfa6-133">You can add additional private and public IP addresses tooan existing NIC by completing hello steps that follow.</span></span> <span data-ttu-id="cbfa6-134">exemplos de saudação incrementar Olá [cenário](#Scenario) descrito neste artigo.</span><span class="sxs-lookup"><span data-stu-id="cbfa6-134">hello examples build upon hello [scenario](#Scenario) described in this article.</span></span>

1. <span data-ttu-id="cbfa6-135">Abra um shell de comando e completa Olá restantes etapas nesta seção dentro de uma única sessão.</span><span class="sxs-lookup"><span data-stu-id="cbfa6-135">Open a command shell and complete hello remaining steps in this section within a single session.</span></span> <span data-ttu-id="cbfa6-136">Se você ainda não tiver a CLI do Azure instalado e configurado, Olá concluir etapas no hello [instalação CLI do Azure 2.0](/cli/azure/install-az-cli2?toc=%2fazure%2fvirtual-network%2ftoc.json) tooyour de artigo e de logon de conta do Azure com hello `az-login` comando.</span><span class="sxs-lookup"><span data-stu-id="cbfa6-136">If you don't already have Azure CLI installed and configured, complete hello steps in hello [Azure CLI 2.0 installation](/cli/azure/install-az-cli2?toc=%2fazure%2fvirtual-network%2ftoc.json) article and login tooyour Azure account with hello `az-login` command.</span></span>

2. <span data-ttu-id="cbfa6-137">Conclua as etapas de saudação em uma das seguintes seções, com base nas necessidades de saudação:</span><span class="sxs-lookup"><span data-stu-id="cbfa6-137">Complete hello steps in one of hello following sections, based on your requirements:</span></span>

    <span data-ttu-id="cbfa6-138">**Adicionar um endereço IP privado**</span><span class="sxs-lookup"><span data-stu-id="cbfa6-138">**Add a private IP address**</span></span>
    
    <span data-ttu-id="cbfa6-139">tooadd um tooa de endereço IP privado NIC, você deve criar uma configuração de IP usando o comando Olá que segue.</span><span class="sxs-lookup"><span data-stu-id="cbfa6-139">tooadd a private IP address tooa NIC, you must create an IP configuration using hello command that follows.</span></span> <span data-ttu-id="cbfa6-140">Olá endereço IP deve ser um endereço não usado para a sub-rede de saudação.</span><span class="sxs-lookup"><span data-stu-id="cbfa6-140">hello static IP address must be an unused address for hello subnet.</span></span>

    ```bash
    az network nic ip-config create \
    --resource-group myResourceGroup \
    --nic-name myNic1 \
    --private-ip-address 10.0.0.7 \
    --name IPConfig-4
    ```
    
    <span data-ttu-id="cbfa6-141">Crie quantas configurações forem necessárias, usando nomes de configuração exclusivos e endereços IP privados (para configurações com endereços IP estáticos).</span><span class="sxs-lookup"><span data-stu-id="cbfa6-141">Create as many configurations as you require, using unique configuration names and private IP addresses (for configurations with static IP addresses).</span></span>

    <span data-ttu-id="cbfa6-142">**Adicionar um endereço IP público**</span><span class="sxs-lookup"><span data-stu-id="cbfa6-142">**Add a public IP address**</span></span>
    
    <span data-ttu-id="cbfa6-143">Um endereço IP público é adicionado ao associá-la tooeither uma nova configuração de IP ou uma configuração de IP existente.</span><span class="sxs-lookup"><span data-stu-id="cbfa6-143">A public IP address is added by associating it tooeither a new IP configuration or an existing IP configuration.</span></span> <span data-ttu-id="cbfa6-144">Conclua as etapas de saudação em uma saudação próximas seções, você precisa.</span><span class="sxs-lookup"><span data-stu-id="cbfa6-144">Complete hello steps in one of hello sections that follow, as you require.</span></span>

    <span data-ttu-id="cbfa6-145">Endereços IP públicos têm um valor nominal.</span><span class="sxs-lookup"><span data-stu-id="cbfa6-145">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="cbfa6-146">toolearn mais sobre endereços IP de preços, ler Olá [preço do endereço IP](https://azure.microsoft.com/pricing/details/ip-addresses) página.</span><span class="sxs-lookup"><span data-stu-id="cbfa6-146">toolearn more about IP address pricing, read hello [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="cbfa6-147">Há um número de toohello limite de endereços IP públicos que podem ser usados em uma assinatura.</span><span class="sxs-lookup"><span data-stu-id="cbfa6-147">There is a limit toohello number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="cbfa6-148">mais sobre os limites de Olá Olá de leitura de toolearn [Azure limita](../azure-subscription-service-limits.md#networking-limits) artigo.</span><span class="sxs-lookup"><span data-stu-id="cbfa6-148">toolearn more about hello limits, read hello [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>

    - <span data-ttu-id="cbfa6-149">**Associar Olá recurso tooa nova configuração de IP**</span><span class="sxs-lookup"><span data-stu-id="cbfa6-149">**Associate hello resource tooa new IP configuration**</span></span>
    
        <span data-ttu-id="cbfa6-150">Sempre que você adicionar um endereço IP público em uma nova configuração de IP, também deverá adicionar um endereço IP privado, pois todas as configurações de IP devem ter um endereço IP privado.</span><span class="sxs-lookup"><span data-stu-id="cbfa6-150">Whenever you add a public IP address in a new IP configuration, you must also add a private IP address, because all IP configurations must have a private IP address.</span></span> <span data-ttu-id="cbfa6-151">Você pode adicionar um recurso de endereço IP público existente ou criar um novo.</span><span class="sxs-lookup"><span data-stu-id="cbfa6-151">You can either add an existing public IP address resource, or create a new one.</span></span> <span data-ttu-id="cbfa6-152">toocreate uma nova, digite Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="cbfa6-152">toocreate a new one, enter hello following command:</span></span>
    
        ```bash
        az network public-ip create \
        --resource-group myResourceGroup \
        --location westcentralus \
        --name myPublicIP3 \
        --dns-name mypublicdns3
        ```

        <span data-ttu-id="cbfa6-153">toocreate uma nova configuração de IP com um endereço IP privado estático e Olá associados *myPublicIP3* IP público recurso de endereço, digite Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="cbfa6-153">toocreate a new IP configuration with a static private IP address and hello associated *myPublicIP3* public IP address resource, enter hello following command:</span></span>

        ```bash
        az network nic ip-config create \
        --resource-group myResourceGroup \
        --nic-name myNic1 \
        --name IPConfig-5 \
        --private-ip-address 10.0.0.8
        --public-ip-address myPublicIP3
        ```

    - <span data-ttu-id="cbfa6-154">**Configuração de IP existente do hello associar recursos tooan** um recurso de endereço IP público só pode ser a configuração de IP tooan associado que ainda não tiver um associado.</span><span class="sxs-lookup"><span data-stu-id="cbfa6-154">**Associate hello resource tooan existing IP configuration** A public IP address resource can only be associated tooan IP configuration that doesn't already have one associated.</span></span> <span data-ttu-id="cbfa6-155">Você pode determinar se uma configuração de IP tem um endereço IP público associado inserindo Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="cbfa6-155">You can determine whether an IP configuration has an associated public IP address by entering hello following command:</span></span>

        ```bash
        az network nic ip-config list \
        --resource-group myResourceGroup \
        --nic-name myNic1 \
        --query "[?provisioningState=='Succeeded'].{ Name: name, PublicIpAddressId: publicIpAddress.id }" --output table
        ```

        <span data-ttu-id="cbfa6-156">Saída retornada:</span><span class="sxs-lookup"><span data-stu-id="cbfa6-156">Returned output:</span></span>
    
            Name        PublicIpAddressId
            
            ipconfig1   /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP1
            IPConfig-2  /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP2
            IPConfig-3

        <span data-ttu-id="cbfa6-157">Desde Olá **PublicIpAddressId** coluna *3 IpConfig* não está em branco no hello saída, nenhum recurso de endereço IP público tooit atualmente associado.</span><span class="sxs-lookup"><span data-stu-id="cbfa6-157">Since hello **PublicIpAddressId** column for *IpConfig-3* is blank in hello output, no public IP address resource is currently associated tooit.</span></span> <span data-ttu-id="cbfa6-158">Você pode adicionar um existente pública IP endereço recurso tooIpConfig-3, ou insira Olá toocreate comando um a seguir:</span><span class="sxs-lookup"><span data-stu-id="cbfa6-158">You can add an existing public IP address resource tooIpConfig-3, or enter hello following command toocreate one:</span></span>

        ```bash
        az network public-ip create \
        --resource-group  myResourceGroup
        --location westcentralus \
        --name myPublicIP3 \
        --dns-name mypublicdns3 \
        --allocation-method Static
        ```
    
        <span data-ttu-id="cbfa6-159">Digite hello recurso toohello existente IP configuração denominada do endereço IP público do tooassociate Olá de comando a seguir *3 IPConfig*:</span><span class="sxs-lookup"><span data-stu-id="cbfa6-159">Enter hello following command tooassociate hello public IP address resource toohello existing IP configuration named *IPConfig-3*:</span></span>
    
        ```bash
        az network nic ip-config update \
        --resource-group myResourceGroup \
        --nic-name myNic1 \
        --name IPConfig-3 \
        --public-ip myPublicIP3
        ```

3. <span data-ttu-id="cbfa6-160">Exibir hello endereços IP privados e Olá público de endereços IP Ids de recursos atribuídas toohello NIC inserindo Olá o comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="cbfa6-160">View hello private IP addresses and hello public IP address resource Ids assigned toohello NIC by entering hello following command:</span></span>

    ```bash
    az network nic ip-config list \
    --resource-group myResourceGroup \
    --nic-name myNic1 \
    --query "[?provisioningState=='Succeeded'].{ Name: name, PrivateIpAddress: privateIpAddress, PrivateIpAllocationMethod: privateIpAllocationMethod, PublicIpAddressId: publicIpAddress.id }" --output table
    ```

    <span data-ttu-id="cbfa6-161">Saída retornada:</span><span class="sxs-lookup"><span data-stu-id="cbfa6-161">Returned output:</span></span> <br>
    
        Name        PrivateIpAddress    PrivateIpAllocationMethod   PublicIpAddressId
        
        ipconfig1   10.0.0.4            Static                      /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP1
        IPConfig-2  10.0.0.5            Static                      /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP2
        IPConfig-3  10.0.0.6            Static                      /subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP3
    

4. <span data-ttu-id="cbfa6-162">Adicionar endereços IP privados Olá adicionado o sistema operacional do toohello NIC toohello VM seguindo instruções Olá Olá [tooa sistema de operacional VM de endereços de IP adicionar](#os-config) deste artigo.</span><span class="sxs-lookup"><span data-stu-id="cbfa6-162">Add hello private IP addresses you added toohello NIC toohello VM operating system by following hello instructions in hello [Add IP addresses tooa VM operating system](#os-config) section of this article.</span></span> <span data-ttu-id="cbfa6-163">Não adicione Olá pública IP endereços toohello sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="cbfa6-163">Do not add hello public IP addresses toohello operating system.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
