---
title: "VM com vários endereços IP usando a CLI do Azure 1.0 | Microsoft Docs"
description: "Saiba como atribuir diversos endereços IP a uma máquina virtual usando a CLI do Azure 1.0 | Resource Manager."
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
ms.openlocfilehash: 9f085dfa1fe4db36d58cb976bb550a46bf241ac7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="assign-multiple-ip-addresses-to-virtual-machines-using-azure-cli-10"></a><span data-ttu-id="6029d-103">Atribuir vários endereços IP a máquinas virtuais usando a CLI do Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="6029d-103">Assign multiple IP addresses to virtual machines using Azure CLI 1.0</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]

<span data-ttu-id="6029d-104">Este artigo explica como criar uma máquina virtual (VM) por meio do Modelo de implantação do Azure Resource Manager usando a CLI do Azure 1.0.</span><span class="sxs-lookup"><span data-stu-id="6029d-104">This article explains how to create a virtual machine (VM) through the Azure Resource Manager deployment model using the Azure CLI 1.0.</span></span> <span data-ttu-id="6029d-105">Múltiplos endereços IP não podem ser atribuídos a recursos criados por meio do modelo de implantação clássico.</span><span class="sxs-lookup"><span data-stu-id="6029d-105">Multiple IP addresses cannot be assigned to resources created through the classic deployment model.</span></span> <span data-ttu-id="6029d-106">Para saber mais sobre modelos de implantação do Azure, leia o artigo [Compreender os modelos de implantação](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="6029d-106">To learn more about Azure deployment models, read the [Understand deployment models](../resource-manager-deployment-model.md) article.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <span data-ttu-id="6029d-107"><a name = "create"></a>Criar uma VM com vários endereços IP</span><span class="sxs-lookup"><span data-stu-id="6029d-107"><a name = "create"></a>Create a VM with multiple IP addresses</span></span>

<span data-ttu-id="6029d-108">Você pode concluir esta tarefa usando a CLI do Azure 1.0 (este artigo) ou a [CLI do Azure 2.0](virtual-network-multiple-ip-addresses-cli.md).</span><span class="sxs-lookup"><span data-stu-id="6029d-108">You can complete this task using the Azure CLI 1.0 (this article) or the [Azure CLI 2.0](virtual-network-multiple-ip-addresses-cli.md).</span></span> <span data-ttu-id="6029d-109">As etapas a seguir explicam como criar uma VM de exemplo com vários endereços IP, como descrito no cenário.</span><span class="sxs-lookup"><span data-stu-id="6029d-109">The steps that follow explain how to create an example VM with multiple IP addresses, as described in the scenario.</span></span> <span data-ttu-id="6029d-110">Altere os nomes da variável e os tipos de endereço IP como exigido por sua implementação.</span><span class="sxs-lookup"><span data-stu-id="6029d-110">Change variable names and IP address types as required for your implementation.</span></span>

1. <span data-ttu-id="6029d-111">Instale e configure a CLI do Azure 1.0 seguindo as etapas do artigo [Instalar e configurar a CLI do Azure](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) e faça logon em sua conta do Azure com o comando `azure-login`.</span><span class="sxs-lookup"><span data-stu-id="6029d-111">Install and configure the Azure CLI 1.0 by following the steps in the [Install and Configure the Azure CLI](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) article and log into your Azure account with the `azure-login` command.</span></span>

2. <span data-ttu-id="6029d-112">Crie um grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="6029d-112">Create a resource group:</span></span>
    
    ```azurecli
    RgName=myResourceGroup
    Location=westcentralus
    azure group create --name $RgName --location $Location
    ```
3. <span data-ttu-id="6029d-113">Criar uma rede virtual:</span><span class="sxs-lookup"><span data-stu-id="6029d-113">Create a virtual network:</span></span>

    ```azurecli
    azure network vnet create --resource-group $RgName --location $Location --name myVNet \
    --address-prefixes 10.0.0.0/16
    ```
4. <span data-ttu-id="6029d-114">Crie uma sub-rede na rede virtual:</span><span class="sxs-lookup"><span data-stu-id="6029d-114">Create a subnet in the virtual network:</span></span>

    ```azurecli
    azure network vnet subnet create --name mySubnet --resource-group $RgName --vnet-name myVNet \
    --address-prefix 10.0.0.0/24
    ```
    
5. <span data-ttu-id="6029d-115">Crie uma conta de armazenamento para a VM.</span><span class="sxs-lookup"><span data-stu-id="6029d-115">Create  a storage account for the VM.</span></span> <span data-ttu-id="6029d-116">Antes de executar o comando a seguir, substitua *mystorageaccount* por um nome exclusivo.</span><span class="sxs-lookup"><span data-stu-id="6029d-116">Before running the following command, replace *mystorageaccount* with a unique name.</span></span> <span data-ttu-id="6029d-117">O nome deve ser exclusivo no Azure:</span><span class="sxs-lookup"><span data-stu-id="6029d-117">The name must be unique across Azure:</span></span>

    ```azurecli
    az storage account create --resource-group $RgName --location $Location --name mystorageaccount \
    --kind Storage --sku Standard_LRS
    ```

6. <span data-ttu-id="6029d-118">Crie as configurações de IP, uma NIC e atribua as configurações de IP à NIC.</span><span class="sxs-lookup"><span data-stu-id="6029d-118">Create the IP configurations, a NIC, and assign the IP configurations to the NIC.</span></span> <span data-ttu-id="6029d-119">Você pode adicionar, remover ou alterar as configurações conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="6029d-119">You can add, remove, or change the configurations as necessary.</span></span> <span data-ttu-id="6029d-120">As configurações a seguir são descritas no cenário:</span><span class="sxs-lookup"><span data-stu-id="6029d-120">The following configurations are described in the scenario:</span></span>

    <span data-ttu-id="6029d-121">**IPConfig-1**</span><span class="sxs-lookup"><span data-stu-id="6029d-121">**IPConfig-1**</span></span>

    <span data-ttu-id="6029d-122">Insira os comandos a seguir para criar:</span><span class="sxs-lookup"><span data-stu-id="6029d-122">Enter the commands that follow to create:</span></span>

    - <span data-ttu-id="6029d-123">Um recurso de endereço IP público com um endereço IP público estático</span><span class="sxs-lookup"><span data-stu-id="6029d-123">A public IP address resource with a static public IP address</span></span>
    - <span data-ttu-id="6029d-124">Uma NIC, atribuindo o endereço IP público e um endereço IP privado estático a ela.</span><span class="sxs-lookup"><span data-stu-id="6029d-124">A NIC, assigning the public IP address and a static private IP address to it.</span></span>
    
    <span data-ttu-id="6029d-125">Substitua *mypublicdns* por um nome que seja exclusivo no local do Azure.</span><span class="sxs-lookup"><span data-stu-id="6029d-125">Replace *mypublicdns* with a name that is unique within the Azure location.</span></span>

      ```azurecli
      azure network public-ip create --resource-group $RgName --location $Location --name myPublicIP1 \
      --domain-name-label mypublicdns --allocation-method Static
        
      azure network nic create --resource-group $RgName --location $Location --name myNic1 \
      --private-ip-address 10.0.0.4 --subnet-name mySubnet --subnet-vnet-name myVNet \
      --subnet-name mySubnet --public-ip-name myPublicIP1
      ```

      > [!NOTE]
      > <span data-ttu-id="6029d-126">Endereços IP públicos têm um valor nominal.</span><span class="sxs-lookup"><span data-stu-id="6029d-126">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="6029d-127">Para saber mais sobre preços de endereço IP, leia a página [Preços de endereço IP](https://azure.microsoft.com/pricing/details/ip-addresses) .</span><span class="sxs-lookup"><span data-stu-id="6029d-127">To learn more about IP address pricing, read the [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="6029d-128">Há um limite para o número de endereços IP públicos que podem ser usados em uma assinatura.</span><span class="sxs-lookup"><span data-stu-id="6029d-128">There is a limit to the number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="6029d-129">Para saber mais sobre os limites, leia o artigo [Limites do Azure](../azure-subscription-service-limits.md#networking-limits).</span><span class="sxs-lookup"><span data-stu-id="6029d-129">To learn more about the limits, read the [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>

    <span data-ttu-id="6029d-130">**IPConfig-2**</span><span class="sxs-lookup"><span data-stu-id="6029d-130">**IPConfig-2**</span></span>

     <span data-ttu-id="6029d-131">Insira os seguintes comandos para criar um novo recurso de endereço IP público e uma nova configuração de IP com um endereço IP público estático e um endereço IP privado estático:</span><span class="sxs-lookup"><span data-stu-id="6029d-131">Enter the following commands to create a new public IP address resource and a new IP configuration with a static public IP address and a static private IP address:</span></span>
    
      ```azurecli
      azure network public-ip create --resource-group $RgName --location $Location --name myPublicIP2
      --domain-name-label mypublicdns2 --allocation-method Static

      azure network nic ip-config create --resource-group $RgName --nic-name myNic1 --name IPConfig-2
      --private-ip-address 10.0.0.5 --public-ip-name myPublicIP2
      ```

    <span data-ttu-id="6029d-132">**IPConfig-3**</span><span class="sxs-lookup"><span data-stu-id="6029d-132">**IPConfig-3**</span></span>

    <span data-ttu-id="6029d-133">Insira os seguintes comandos para criar uma configuração de IP com um endereço IP privado estático e nenhum endereço IP público:</span><span class="sxs-lookup"><span data-stu-id="6029d-133">Enter the following commands to create an IP configuration with a static private IP address and no public IP address:</span></span>

      ```azurecli
      azure network nic ip-config create --resource-group $RgName --nic-name myNic1 --private-ip-address 10.0.0.6 \
      --name IPConfig-3
      ```

    >[!NOTE] 
    ><span data-ttu-id="6029d-134">Embora este artigo atribua todas as configurações de IP a uma única NIC, você também pode atribuir várias configurações de IP para qualquer NIC em uma VM.</span><span class="sxs-lookup"><span data-stu-id="6029d-134">Though this article assigns all IP configurations to a single NIC, you can also assign multiple IP configurations to any NIC in a VM.</span></span> <span data-ttu-id="6029d-135">Para saber como criar uma VM com várias NICs, leia o artigo Criar uma VM com várias NICs.</span><span class="sxs-lookup"><span data-stu-id="6029d-135">To learn how to create a VM with multiple NICs, read the Create a VM with multiple NICs article.</span></span>

7. <span data-ttu-id="6029d-136">Criar uma VM do Linux</span><span class="sxs-lookup"><span data-stu-id="6029d-136">Create a Linux VM</span></span> 

    ```azurecli
    az vm create --resource-group $RgName --name myVM1 --location $Location --nics myNic1 \
    --image UbuntuLTS --ssh-key-value ~/.ssh/id_rsa.pub --admin-username azureuser
    ```

    <span data-ttu-id="6029d-137">Para alterar o tamanho da VM para Standard DS2 v2, por exemplo, basta adicionar a seguinte propriedade `--vm-size Standard_DS3_v2` ao comando `azure vm create` na etapa 6.</span><span class="sxs-lookup"><span data-stu-id="6029d-137">To change the VM size to Standard DS2 v2, for example, simply add the following property `--vm-size Standard_DS3_v2` to the `azure vm create` command in step 6.</span></span>

8. <span data-ttu-id="6029d-138">Insira o comando a seguir para exibir a NIC e as configurações de IP associadas:</span><span class="sxs-lookup"><span data-stu-id="6029d-138">Enter the following command to view the NIC and the associated IP configurations:</span></span>

    ```azurecli
    azure network nic show --resource-group $RgName --name myNic1
    ```
9. <span data-ttu-id="6029d-139">Adicione os endereços IP privados ao sistema operacional da VM executando as etapas para seu sistema operacional na seção [Adicionar endereços IP ao sistema operacional de uma VM](#os-config) deste artigo.</span><span class="sxs-lookup"><span data-stu-id="6029d-139">Add the private IP addresses to the VM operating system by completing the steps for your operating system in the [Add IP addresses to a VM operating system](#os-config) section of this article.</span></span>

## <span data-ttu-id="6029d-140"><a name="add"></a>Adicionar endereços IP a uma VM</span><span class="sxs-lookup"><span data-stu-id="6029d-140"><a name="add"></a>Add IP addresses to a VM</span></span>

<span data-ttu-id="6029d-141">Você pode adicionar endereços IP públicos e privados adicionais para um NIC existente ao concluir as etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="6029d-141">You can add additional private and public IP addresses to an existing NIC by completing the steps that follow.</span></span> <span data-ttu-id="6029d-142">Os exemplos baseiam-se no [cenário](#Scenario) descrito neste artigo.</span><span class="sxs-lookup"><span data-stu-id="6029d-142">The examples build upon the [scenario](#Scenario) described in this article.</span></span>

1. <span data-ttu-id="6029d-143">Abra a CLI do Azure e conclua as etapas restantes nesta seção dentro de uma única sessão da CLI.</span><span class="sxs-lookup"><span data-stu-id="6029d-143">Open Azure CLI and complete the remaining steps in this section within a single CLI session.</span></span> <span data-ttu-id="6029d-144">Se você ainda não tiver a CLI do Azure instalada e configurada, conclua as etapas do artigo [Instalar e configurar a CLI do Azure](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) e faça logon em sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="6029d-144">If you don't already have Azure CLI installed and configured, complete the steps in the [Install and Configure the Azure CLI](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) article and log into your Azure account.</span></span>

2. <span data-ttu-id="6029d-145">Conclua as etapas em uma das seções a seguir, com base em seus requisitos:</span><span class="sxs-lookup"><span data-stu-id="6029d-145">Complete the steps in one of the following sections, based on your requirements:</span></span>

    - <span data-ttu-id="6029d-146">**Adicionar um endereço IP privado**</span><span class="sxs-lookup"><span data-stu-id="6029d-146">**Add a private IP address**</span></span>
    
        <span data-ttu-id="6029d-147">Para adicionar um endereço IP privado a uma NIC, você deve criar uma configuração de IP usando o comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="6029d-147">To add a private IP address to a NIC, you must create an IP configuration using the command below.</span></span> <span data-ttu-id="6029d-148">O endereço estático deve ser um endereço não usado para a sub-rede.</span><span class="sxs-lookup"><span data-stu-id="6029d-148">The static address must be an unused address for the subnet.</span></span>

        ```azurecli
        azure network nic ip-config create --resource-group myResourceGroup --nic-name myNic1 \
        --private-ip-address 10.0.0.7 --name IPConfig-4
        ```
        <span data-ttu-id="6029d-149">Crie quantas configurações forem necessárias, usando nomes de configuração exclusivos e endereços IP privados (para configurações com endereços IP estáticos).</span><span class="sxs-lookup"><span data-stu-id="6029d-149">Create as many configurations as you require, using unique configuration names and private IP addresses (for configurations with static IP addresses).</span></span>

    - <span data-ttu-id="6029d-150">**Adicionar um endereço IP público**</span><span class="sxs-lookup"><span data-stu-id="6029d-150">**Add a public IP address**</span></span>
    
        <span data-ttu-id="6029d-151">Um endereço IP público é adicionado por meio de sua associação a uma nova configuração de IP ou de uma configuração de IP existente.</span><span class="sxs-lookup"><span data-stu-id="6029d-151">A public IP address is added by associating it to either a new IP configuration or an existing IP configuration.</span></span> <span data-ttu-id="6029d-152">Conclua as etapas em uma das seções a seguir, quando você precisar.</span><span class="sxs-lookup"><span data-stu-id="6029d-152">Complete the steps in one of the sections that follow, as you require.</span></span>

        > [!NOTE]
        > <span data-ttu-id="6029d-153">Endereços IP públicos têm um valor nominal.</span><span class="sxs-lookup"><span data-stu-id="6029d-153">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="6029d-154">Para saber mais sobre preços de endereço IP, leia a página [Preços de endereço IP](https://azure.microsoft.com/pricing/details/ip-addresses) .</span><span class="sxs-lookup"><span data-stu-id="6029d-154">To learn more about IP address pricing, read the [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="6029d-155">Há um limite para o número de endereços IP públicos que podem ser usados em uma assinatura.</span><span class="sxs-lookup"><span data-stu-id="6029d-155">There is a limit to the number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="6029d-156">Para saber mais sobre os limites, leia o artigo [Limites do Azure](../azure-subscription-service-limits.md#networking-limits).</span><span class="sxs-lookup"><span data-stu-id="6029d-156">To learn more about the limits, read the [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>
        >

        <span data-ttu-id="6029d-157">**Associar o recurso a uma nova configuração de IP**</span><span class="sxs-lookup"><span data-stu-id="6029d-157">**Associate the resource to a new IP configuration**</span></span>
    
        <span data-ttu-id="6029d-158">Sempre que você adicionar um endereço IP público em uma nova configuração de IP, também deverá adicionar um endereço IP privado, pois todas as configurações de IP devem ter um endereço IP privado.</span><span class="sxs-lookup"><span data-stu-id="6029d-158">Whenever you add a public IP address in a new IP configuration, you must also add a private IP address, because all IP configurations must have a private IP address.</span></span> <span data-ttu-id="6029d-159">Você pode adicionar um recurso de endereço IP público existente ou criar um novo.</span><span class="sxs-lookup"><span data-stu-id="6029d-159">You can either add an existing public IP address resource, or create a new one.</span></span> <span data-ttu-id="6029d-160">Para criar um novo, insira o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="6029d-160">To create a new one, enter the following command:</span></span>

        ```azurecli
        azure network public-ip create --resource-group myResourceGroup --location westcentralus --name myPublicIP3 \
        --domain-name-label mypublicdns3
        ```

        <span data-ttu-id="6029d-161">Para criar uma nova configuração de IP com um endereço IP privado estático e o recurso de endereço IP público *myPublicIP3* associado, insira o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="6029d-161">To create a new IP configuration with a static private IP address and the associated *myPublicIP3* public IP address resource, enter the following command:</span></span>

        ```azurecli
        azure network nic ip-config create --resource-group myResourceGroup --nic-name myNic --name IPConfig-4 \
        --private-ip-address 10.0.0.8 --public-ip-name myPublicIP3
        ```

        <span data-ttu-id="6029d-162">**Associar o recurso a uma configuração de IP existente**</span><span class="sxs-lookup"><span data-stu-id="6029d-162">**Associate the resource to an existing IP configuration**</span></span>

        <span data-ttu-id="6029d-163">Um recurso de endereço IP público só pode ser associado a uma configuração de IP que ainda não tenha um associado.</span><span class="sxs-lookup"><span data-stu-id="6029d-163">A public IP address resource can only be associated to an IP configuration that doesn't already have one associated.</span></span> <span data-ttu-id="6029d-164">Você pode determinar se uma configuração de IP tem um endereço IP público associado inserindo o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="6029d-164">You can determine whether an IP configuration has an associated public IP address by entering the following command:</span></span>

        ```azurecli
        azure network nic ip-config list --resource-group myResourceGroup --nic-name myNic1
        ```

        <span data-ttu-id="6029d-165">Procure uma linha semelhante à linha que segue IPConfig-3 na saída retornada:</span><span class="sxs-lookup"><span data-stu-id="6029d-165">Look for a line similar to the one that follows for IPConfig-3 in the returned output:</span></span>

        ```         
        Name               Provisioning state  Primary  Private IP allocation Private IP version  Private IP address  Subnet    Public IP
        default-ip-config  Succeeded           true     Static                IPv4                10.0.0.4            mySubnet  myPublicIP
        IPConfig-2         Succeeded           false    Static                IPv4                10.0.0.5            mySubnet  myPublicIP2
        IPConfig-3         Succeeded           false    Static                IPv4                10.0.0.6            mySubnet
        ```
          
        <span data-ttu-id="6029d-166">Como a coluna **IP Público** para *IpConfig 3* está em branco, nenhum recurso de endereço IP público está associado a ele no momento.</span><span class="sxs-lookup"><span data-stu-id="6029d-166">Since the **Public IP** column for *IpConfig-3* is blank, no public IP address resource is currently associated to it.</span></span> <span data-ttu-id="6029d-167">Você pode adicionar um recurso de endereço IP público existente como IpConfig-3 ou inserir o seguinte comando para criar um:</span><span class="sxs-lookup"><span data-stu-id="6029d-167">You can add an existing public IP address resource to IpConfig-3, or enter the following command to create one:</span></span>

        ```azurecli
        azure network public-ip create --resource-group  myResourceGroup --location westcentralus \
        --name myPublicIP3 --domain-name-label mypublicdns3 --allocation-method Static
        ```

        <span data-ttu-id="6029d-168">Insira o comando a seguir para associar o recurso de endereço IP público à configuração de IP existente chamada *IPConfig-3*:</span><span class="sxs-lookup"><span data-stu-id="6029d-168">Enter the following command to associate the public IP address resource to the existing IP configuration named *IPConfig-3*:</span></span>
        ```azurecli
        azure network nic ip-config set --resource-group myResourceGroup --nic-name myNic1 --name IPConfig-3 \
        --public-ip-name myPublicIP3
        ```

3. <span data-ttu-id="6029d-169">Exiba os endereços IP privados e o recurso de endereço IP público atribuído à NIC, digitando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="6029d-169">View the private IP addresses and the public IP address resources assigned to the NIC by entering the following command:</span></span>

    ```azurecli
    azure network nic ip-config list --resource-group myResourceGroup --nic-name myNic1
    ```

      <span data-ttu-id="6029d-170">A saída retornada é semelhante a esta:</span><span class="sxs-lookup"><span data-stu-id="6029d-170">The returned output is similar to the following:</span></span>
      ```
      Name               Provisioning state  Primary  Private IP allocation Private IP version  Private IP address  Subnet    Public IP
        
      default-ip-config  Succeeded           true     Static                IPv4                10.0.0.4            mySubnet  myPublicIP
      IPConfig-2         Succeeded           false    Static                IPv4                10.0.0.5            mySubnet  myPublicIP2
      IPConfig-3         Succeeded           false    Static                IPv4                10.0.0.6            mySubnet  myPublicIP3
      ```
4. <span data-ttu-id="6029d-171">Adicione os endereços IP privados que você adicionou à NIC para o sistema operacional da VM seguindo as instruções da seção [Adicionar endereços IP a um sistema operacional de VM](#os-config) deste artigo.</span><span class="sxs-lookup"><span data-stu-id="6029d-171">Add the private IP addresses you added to the NIC to the VM operating system by following the instructions in the [Add IP addresses to a VM operating system](#os-config) section of this article.</span></span> <span data-ttu-id="6029d-172">Não adicione os endereços IP públicos ao sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="6029d-172">Do not add the public IP addresses to the operating system.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
