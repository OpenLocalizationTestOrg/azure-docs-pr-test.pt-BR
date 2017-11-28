---
title: "Vários endereços IP para máquinas virtuais do Azure – PowerShell | Microsoft Docs"
description: "Saiba como atribuir diversos endereços IP a uma máquina virtual usando o PowerShell | Resource Manager."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c44ea62f-7e54-4e3b-81ef-0b132111f1f8
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/24/2017
ms.author: jdial;annahar
ms.openlocfilehash: 29f64aeefc2a7deb1f84d759c2323347536b9c27
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="assign-multiple-ip-addresses-to-virtual-machines-using-powershell"></a><span data-ttu-id="7f498-103">Atribuir vários endereços IP a máquinas virtuais usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="7f498-103">Assign multiple IP addresses to virtual machines using PowerShell</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]

<span data-ttu-id="7f498-104">Este artigo explica como criar uma máquina virtual (VM) por meio do Modelo de implantação do Azure Resource Manager usando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7f498-104">This article explains how to create a virtual machine (VM) through the Azure Resource Manager deployment model using PowerShell.</span></span> <span data-ttu-id="7f498-105">Múltiplos endereços IP não podem ser atribuídos a recursos criados por meio do modelo de implantação clássico.</span><span class="sxs-lookup"><span data-stu-id="7f498-105">Multiple IP addresses cannot be assigned to resources created through the classic deployment model.</span></span> <span data-ttu-id="7f498-106">Para saber mais sobre modelos de implantação do Azure, leia o artigo [Compreender os modelos de implantação](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="7f498-106">To learn more about Azure deployment models, read the [Understand deployment models](../resource-manager-deployment-model.md) article.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <span data-ttu-id="7f498-107"><a name = "create"></a>Criar uma VM com vários endereços IP</span><span class="sxs-lookup"><span data-stu-id="7f498-107"><a name = "create"></a>Create a VM with multiple IP addresses</span></span>

<span data-ttu-id="7f498-108">As etapas a seguir explicam como criar uma VM de exemplo com vários endereços IP, como descrito no cenário.</span><span class="sxs-lookup"><span data-stu-id="7f498-108">The steps that follow explain how to create an example VM with multiple IP addresses, as described in the scenario.</span></span> <span data-ttu-id="7f498-109">Altere os valores da variável conforme exigido por sua implementação.</span><span class="sxs-lookup"><span data-stu-id="7f498-109">Change variable values as required for your implementation.</span></span>

1. <span data-ttu-id="7f498-110">Abra um prompt de comando do PowerShell e siga as etapas restantes nesta seção dentro de uma única sessão do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7f498-110">Open a PowerShell command prompt and complete the remaining steps in this section within a single PowerShell session.</span></span> <span data-ttu-id="7f498-111">Se o Azure PowerShell ainda não foi instalado nem configurado, siga as etapas no artigo [Como instalar e configurar o Azure PowerShell](/powershell/azure/overview) .</span><span class="sxs-lookup"><span data-stu-id="7f498-111">If you don't already have PowerShell installed and configured, complete the steps in the [How to install and configure Azure PowerShell](/powershell/azure/overview) article.</span></span>
2. <span data-ttu-id="7f498-112">Faça logon em sua conta com o comando `login-azurermaccount`.</span><span class="sxs-lookup"><span data-stu-id="7f498-112">Login to your account with the `login-azurermaccount` command.</span></span>
3. <span data-ttu-id="7f498-113">Substitua *myResourceGroup* e *westus* por um nome e local de sua escolha.</span><span class="sxs-lookup"><span data-stu-id="7f498-113">Replace *myResourceGroup* and *westus* with a name and location of your choosing.</span></span> <span data-ttu-id="7f498-114">Crie um grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="7f498-114">Create a resource group.</span></span> <span data-ttu-id="7f498-115">Um grupo de recursos é um contêiner lógico no qual os recursos do Azure são implantados e gerenciados.</span><span class="sxs-lookup"><span data-stu-id="7f498-115">A resource group is a logical container into which Azure resources are deployed and managed.</span></span>

    ```powershell
    $RgName   = "MyResourceGroup"
    $Location = "westus"

    New-AzureRmResourceGroup `
    -Name $RgName `
    -Location $Location
    ```

4. <span data-ttu-id="7f498-116">Crie uma rede virtual (VNet) e sub-rede no mesmo local que o grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="7f498-116">Create a virtual network (VNet) and subnet in the same location as the resource group:</span></span>

    ```powershell
    
    # Create a subnet configuration
    $SubnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name MySubnet `
    -AddressPrefix 10.0.0.0/24

    # Create a virtual network
    $VNet = New-AzureRmVirtualNetwork `
    -ResourceGroupName $RgName `
    -Location $Location `
    -Name MyVNet `
    -AddressPrefix 10.0.0.0/16 `
    -Subnet $subnetConfig

    # Get the subnet object
    $Subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name $SubnetConfig.Name -VirtualNetwork $VNet
    ```

5. <span data-ttu-id="7f498-117">Crie um NSG (grupo de segurança de rede) e uma regra.</span><span class="sxs-lookup"><span data-stu-id="7f498-117">Create a network security group (NSG) and a rule.</span></span> <span data-ttu-id="7f498-118">O NSG protege a VM usando regras de entrada e saída.</span><span class="sxs-lookup"><span data-stu-id="7f498-118">The NSG secures the VM using inbound and outbound rules.</span></span> <span data-ttu-id="7f498-119">Nesse caso, uma regra de entrada é criada para a porta 3389, que permite conexões de área de trabalho remota.</span><span class="sxs-lookup"><span data-stu-id="7f498-119">In this case, an inbound rule is created for port 3389, which allows incoming remote desktop connections.</span></span>

    ```powershell
    
    # Create an inbound network security group rule for port 3389

    $NSGRule = New-AzureRmNetworkSecurityRuleConfig `
    -Name MyNsgRuleRDP `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 1000 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 3389 -Access Allow
    
    # Create a network security group
    $NSG = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName $RgName `
    -Location $Location `
    -Name MyNetworkSecurityGroup `
    -SecurityRules $NSGRule
    ```

6. <span data-ttu-id="7f498-120">Defina a configuração de IP primário da NIC.</span><span class="sxs-lookup"><span data-stu-id="7f498-120">Define the primary IP configuration for the NIC.</span></span> <span data-ttu-id="7f498-121">Caso você não tenha usado o valor definido anteriormente, altere 10.0.0.4 para um endereço válido na sub-rede que você criou.</span><span class="sxs-lookup"><span data-stu-id="7f498-121">Change 10.0.0.4 to a valid address in the subnet you created, if you didn't use the value defined previously.</span></span> <span data-ttu-id="7f498-122">Antes de atribuir um endereço IP estático, é recomendável que você primeiro confirme que ele ainda não está em uso.</span><span class="sxs-lookup"><span data-stu-id="7f498-122">Before assigning a static IP address, it's recommended that you first confirm it's not already in use.</span></span> <span data-ttu-id="7f498-123">Digite o comando `Test-AzureRmPrivateIPAddressAvailability -IPAddress 10.0.0.4 -VirtualNetwork $VNet`.</span><span class="sxs-lookup"><span data-stu-id="7f498-123">Enter the command `Test-AzureRmPrivateIPAddressAvailability -IPAddress 10.0.0.4 -VirtualNetwork $VNet`.</span></span> <span data-ttu-id="7f498-124">Se o endereço está disponível, a saída retorna *True*.</span><span class="sxs-lookup"><span data-stu-id="7f498-124">If the address is available, the output returns *True*.</span></span> <span data-ttu-id="7f498-125">Se não está disponível, a saída retorna *False* e uma lista de endereços disponíveis.</span><span class="sxs-lookup"><span data-stu-id="7f498-125">If it's not available, the output returns *False* and a list of addresses that are available.</span></span> 

    <span data-ttu-id="7f498-126">Nos comandos a seguir, **Substitua <substitua-por-seu-nome-exclusivo> pelo nome DNS exclusivo a utilizar.**</span><span class="sxs-lookup"><span data-stu-id="7f498-126">In the following commands, **Replace <replace-with-your-unique-name> with the unique DNS name to use.**</span></span> <span data-ttu-id="7f498-127">O nome deve ser exclusivo entre todos os endereços IP públicos dentro de uma região do Azure.</span><span class="sxs-lookup"><span data-stu-id="7f498-127">The name must be unique across all public IP addresses within an Azure region.</span></span> <span data-ttu-id="7f498-128">Este é um parâmetro opcional.</span><span class="sxs-lookup"><span data-stu-id="7f498-128">This is an optional parameter.</span></span> <span data-ttu-id="7f498-129">Ele pode ser removido se você deseja conectar-se à VM usando o endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="7f498-129">It can be removed if you only want to connect to the VM using the public IP address.</span></span>

    ```powershell
    
    # Create a public IP address
    $PublicIP1 = New-AzureRmPublicIpAddress `
    -Name "MyPublicIP1" `
    -ResourceGroupName $RgName `
    -Location $Location `
    -DomainNameLabel <replace-with-your-unique-name> `
    -AllocationMethod Static
        
    #Create an IP configuration with a static private IP address and assign the public IP ddress to it
    $IpConfigName1 = "IPConfig-1"
    $IpConfig1     = New-AzureRmNetworkInterfaceIpConfig `
    -Name $IpConfigName1 `
    -Subnet $Subnet `
    -PrivateIpAddress 10.0.0.4 `
    -PublicIpAddress $PublicIP1 `
    -Primary
    ```

    <span data-ttu-id="7f498-130">Quando você atribuir várias configurações de IP a uma NIC, uma configuração deverá ser atribuída como a *-Primary*.</span><span class="sxs-lookup"><span data-stu-id="7f498-130">When you assign multiple IP configurations to a NIC, one configuration must be assigned as the *-Primary*.</span></span>

    > [!NOTE]
    > <span data-ttu-id="7f498-131">Endereços IP públicos têm um valor nominal.</span><span class="sxs-lookup"><span data-stu-id="7f498-131">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="7f498-132">Para saber mais sobre preços de endereço IP, leia a página [Preços de endereço IP](https://azure.microsoft.com/pricing/details/ip-addresses) .</span><span class="sxs-lookup"><span data-stu-id="7f498-132">To learn more about IP address pricing, read the [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="7f498-133">Há um limite para o número de endereços IP públicos que podem ser usados em uma assinatura.</span><span class="sxs-lookup"><span data-stu-id="7f498-133">There is a limit to the number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="7f498-134">Para saber mais sobre os limites, leia o artigo [Limites do Azure](../azure-subscription-service-limits.md#networking-limits).</span><span class="sxs-lookup"><span data-stu-id="7f498-134">To learn more about the limits, read the [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>

7. <span data-ttu-id="7f498-135">Defina as configurações de IP secundário da NIC.</span><span class="sxs-lookup"><span data-stu-id="7f498-135">Define the secondary IP configurations for the NIC.</span></span> <span data-ttu-id="7f498-136">Você pode adicionar, remover ou alterar as configurações conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="7f498-136">You can add or remove configurations as necessary.</span></span> <span data-ttu-id="7f498-137">Cada configuração de IP deve ter um endereço IP privado atribuído.</span><span class="sxs-lookup"><span data-stu-id="7f498-137">Each IP configuration must have a private IP address assigned.</span></span> <span data-ttu-id="7f498-138">Cada configuração pode, opcionalmente, ter um endereço IP público atribuído.</span><span class="sxs-lookup"><span data-stu-id="7f498-138">Each configuration can optionally have one public IP address assigned.</span></span>

    ```powershell
    
    # Create a public IP address
    $PublicIP2 = New-AzureRmPublicIpAddress `
    -Name "MyPublicIP2" `
    -ResourceGroupName $RgName `
    -Location $Location `
    -AllocationMethod Static
        
    #Create an IP configuration with a static private IP address and assign the public IP ddress to it
    $IpConfigName2 = "IPConfig-2"
    $IpConfig2     = New-AzureRmNetworkInterfaceIpConfig `
    -Name $IpConfigName2 `
    -Subnet $Subnet `
    -PrivateIpAddress 10.0.0.5 `
    -PublicIpAddress $PublicIP2
        
    $IpConfigName3 = "IpConfig-3"
    $IpConfig3 = New-AzureRmNetworkInterfaceIpConfig `
    -Name $IPConfigName3 `
    -Subnet $Subnet `
    -PrivateIpAddress 10.0.0.6
    ```

8. <span data-ttu-id="7f498-139">Criar a NIC e associar as três configurações de IP a ela:</span><span class="sxs-lookup"><span data-stu-id="7f498-139">Create the NIC and associate the three IP configurations to it:</span></span>

    ```powershell
    
    $NIC = New-AzureRmNetworkInterface `
    -Name MyNIC `
    -ResourceGroupName $RgName `
    -Location $Location `
    -NetworkSecurityGroupId $NSG.Id `
    -IpConfiguration $IpConfig1,$IpConfig2,$IpConfig3
    ```

    >[!NOTE]
    ><span data-ttu-id="7f498-140">Embora todas as configurações estejam atribuídas a uma NIC neste artigo, você pode atribuir várias configurações de IP a cada NIC anexada à VM.</span><span class="sxs-lookup"><span data-stu-id="7f498-140">Though all configurations are assigned to one NIC in this article, you can assign multiple IP configurations to every NIC attached to the VM.</span></span> <span data-ttu-id="7f498-141">Para saber como criar uma VM com vários NICs, leia o artigo [Criar uma VM com vários NICs](virtual-network-deploy-multinic-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="7f498-141">To learn how to create a VM with multiple NICs, read the [Create a VM with multiple NICs](virtual-network-deploy-multinic-arm-ps.md) article.</span></span>

9. <span data-ttu-id="7f498-142">Crie a VM digitando os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="7f498-142">Create the VM by entering the following commands:</span></span>

    ```powershell
    
    # Define a credential object. When you run these commands, you're prompted to enter a sername and password for the VM you're reating.
    $cred = Get-Credential
    
    # Create a virtual machine configuration
    $VmConfig = New-AzureRmVMConfig `
    -VMName MyVM `
    -VMSize Standard_DS1_v2 | `
    Set-AzureRmVMOperatingSystem -Windows `
    -ComputerName MyVM `
    -Credential $cred | `
    Set-AzureRmVMSourceImage `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter `
    -Version latest | `
    Add-AzureRmVMNetworkInterface `
    -Id $NIC.Id
    
    # Create the VM
    New-AzureRmVM `
    -ResourceGroupName $RgName `
    -Location $Location `
    -VM $VmConfig
    ```

10. <span data-ttu-id="7f498-143">Adicione os endereços IP privados ao sistema operacional da VM executando as etapas para seu sistema operacional na seção [Adicionar endereços IP ao sistema operacional de uma VM](#os-config) deste artigo.</span><span class="sxs-lookup"><span data-stu-id="7f498-143">Add the private IP addresses to the VM operating system by completing the steps for your operating system in the [Add IP addresses to a VM operating system](#os-config) section of this article.</span></span> <span data-ttu-id="7f498-144">Não adicione os endereços IP públicos ao sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="7f498-144">Do not add the public IP addresses to the operating system.</span></span>

## <span data-ttu-id="7f498-145"><a name="add"></a>Adicionar endereços IP a uma VM</span><span class="sxs-lookup"><span data-stu-id="7f498-145"><a name="add"></a>Add IP addresses to a VM</span></span>

<span data-ttu-id="7f498-146">Você pode adicionar endereços IP públicos e privados a um NIC executando as etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="7f498-146">You can add private and public IP addresses to a NIC by completing the steps that follow.</span></span> <span data-ttu-id="7f498-147">Os exemplos nas seções a seguir pressupõem que você já tem uma VM com as três configurações de IP descritas no [cenário](#Scenario) neste artigo, mas isso não é obrigatório.</span><span class="sxs-lookup"><span data-stu-id="7f498-147">The examples in the following sections assume that you already have a VM with the three IP configurations described in the [scenario](#Scenario) in this article, but it's not required that you do.</span></span>

1. <span data-ttu-id="7f498-148">Abra um prompt de comando do PowerShell e siga as etapas restantes nesta seção dentro de uma única sessão do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7f498-148">Open a PowerShell command prompt and complete the remaining steps in this section within a single PowerShell session.</span></span> <span data-ttu-id="7f498-149">Se o Azure PowerShell ainda não foi instalado nem configurado, siga as etapas no artigo [Como instalar e configurar o Azure PowerShell](/powershell/azure/overview) .</span><span class="sxs-lookup"><span data-stu-id="7f498-149">If you don't already have PowerShell installed and configured, complete the steps in the [How to install and configure Azure PowerShell](/powershell/azure/overview) article.</span></span>
2. <span data-ttu-id="7f498-150">Altere os "valores" de $Variables a seguir para o nome do NIC ao qual você deseja adicionar os endereços IP e o grupo de recursos e a localização onde o NIC está:</span><span class="sxs-lookup"><span data-stu-id="7f498-150">Change the "values" of the following $Variables to the name of the NIC you want to add IP address to and the resource group and location the NIC exists in:</span></span>

    ```powershell
    $NicName  = "MyNIC"
    $RgName   = "MyResourceGroup"
    $Location = "westus"
    ```

    <span data-ttu-id="7f498-151">Se você não souber o nome da NIC que você deseja alterar, digite os seguintes comandos e altere os valores das variáveis anteriores:</span><span class="sxs-lookup"><span data-stu-id="7f498-151">If you don't know the name of the NIC you want to change, enter the following commands, then change the values of the previous variables:</span></span>

    ```powershell
    Get-AzureRmNetworkInterface | Format-Table Name, ResourceGroupName, Location
    ```
3. <span data-ttu-id="7f498-152">Crie uma variável e defina-a para a NIC existente digitando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="7f498-152">Create a variable and set it to the existing NIC by typing the following command:</span></span>

    ```powershell
    $MyNIC = Get-AzureRmNetworkInterface -Name $NicName -ResourceGroupName $RgName
    ```
4. <span data-ttu-id="7f498-153">Nos comandos a seguir, mude *MyVNet* e *MySubnet* para os nomes da VNet e da sub-rede às quais a NIC está conectada.</span><span class="sxs-lookup"><span data-stu-id="7f498-153">In the following commands, change *MyVNet* and *MySubnet* to the names of the VNet and subnet the NIC is connected to.</span></span> <span data-ttu-id="7f498-154">Digite os comandos para recuperar os objetos de rede virtual e sub-rede aos quais o NIC está conectado:</span><span class="sxs-lookup"><span data-stu-id="7f498-154">Enter the commands to retrieve the VNet and subnet objects the NIC is connected to:</span></span>

    ```powershell
    $MyVNet = Get-AzureRMVirtualnetwork -Name MyVNet -ResourceGroupName $RgName
    $Subnet = $MyVnet.Subnets | Where-Object { $_.Name -eq "MySubnet" }
    ```
    <span data-ttu-id="7f498-155">Se você não souber o nome da rede virtual ou sub-rede à qual o NIC está conectado, digite o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="7f498-155">If you don't know the VNet or subnet name the NIC is connected to, enter the following command:</span></span>
    ```powershell
    $MyNIC.IpConfigurations
    ```
    <span data-ttu-id="7f498-156">Na saída, procure por texto semelhante à saída de exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="7f498-156">In the output, look for text similar to the following example output:</span></span>
    
    ```
    "Id": "/subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/MyVNet/subnets/MySubnet"
    ```
    <span data-ttu-id="7f498-157">Nessa saída, *MyVnet* é a VNet e *MySubnet* são, respectivamente, a rede virtual e a sub-rede às quais a NIC está conectada.</span><span class="sxs-lookup"><span data-stu-id="7f498-157">In this output, *MyVnet* is the VNet and *MySubnet* is the subnet the NIC is connected to.</span></span>

5. <span data-ttu-id="7f498-158">Conclua as etapas em uma das seções a seguir, com base em seus requisitos:</span><span class="sxs-lookup"><span data-stu-id="7f498-158">Complete the steps in one of the following sections, based on your requirements:</span></span>

    <span data-ttu-id="7f498-159">**Adicionar um endereço IP privado**</span><span class="sxs-lookup"><span data-stu-id="7f498-159">**Add a private IP address**</span></span>

    <span data-ttu-id="7f498-160">Para adicionar um endereço IP privado a um NIC, você deverá criar uma configuração de IP.</span><span class="sxs-lookup"><span data-stu-id="7f498-160">To add a private IP address to a NIC, you must create an IP configuration.</span></span> <span data-ttu-id="7f498-161">O comando a seguir cria uma configuração com um endereço IP estático 10.0.0.7.</span><span class="sxs-lookup"><span data-stu-id="7f498-161">The following command creates a configuration with a static IP address of 10.0.0.7.</span></span> <span data-ttu-id="7f498-162">Ao especificar um endereço IP estático, ele deve ser um endereço não usado para a sub-rede.</span><span class="sxs-lookup"><span data-stu-id="7f498-162">When specifying a static IP address, it must be an unused address for the subnet.</span></span> <span data-ttu-id="7f498-163">É recomendável que você primeiro teste o endereço para garantir que ele está disponível digitando o comando `Test-AzureRmPrivateIPAddressAvailability -IPAddress 10.0.0.7 -VirtualNetwork $myVnet`.</span><span class="sxs-lookup"><span data-stu-id="7f498-163">It's recommended that you first test the address to ensure it's available by entering the `Test-AzureRmPrivateIPAddressAvailability -IPAddress 10.0.0.7 -VirtualNetwork $myVnet` command.</span></span> <span data-ttu-id="7f498-164">Se o endereço IP está disponível, a saída retorna *True*.</span><span class="sxs-lookup"><span data-stu-id="7f498-164">If the IP address is available, the output returns *True*.</span></span> <span data-ttu-id="7f498-165">Se não está disponível, a saída retorna *False* e uma lista de endereços disponíveis.</span><span class="sxs-lookup"><span data-stu-id="7f498-165">If it's not available, the output returns *False*, and a list of addresses that are available.</span></span>

    ```powershell
    Add-AzureRmNetworkInterfaceIpConfig -Name IPConfig-4 -NetworkInterface `
    $MyNIC -Subnet $Subnet -PrivateIpAddress 10.0.0.7
    ```
    <span data-ttu-id="7f498-166">Crie quantas configurações forem necessárias, usando nomes de configuração exclusivos e endereços IP privados (para configurações com endereços IP estáticos).</span><span class="sxs-lookup"><span data-stu-id="7f498-166">Create as many configurations as you require, using unique configuration names and private IP addresses (for configurations with static IP addresses).</span></span>

    <span data-ttu-id="7f498-167">Adicione o endereço IP privado ao sistema operacional da VM executando as etapas para seu sistema operacional na seção [Adicionar endereços IP ao sistema operacional de uma VM](#os-config) deste artigo.</span><span class="sxs-lookup"><span data-stu-id="7f498-167">Add the private IP address to the VM operating system by completing the steps for your operating system in the [Add IP addresses to a VM operating system](#os-config) section of this article.</span></span>

    <span data-ttu-id="7f498-168">**Adicionar um endereço IP público**</span><span class="sxs-lookup"><span data-stu-id="7f498-168">**Add a public IP address**</span></span>

    <span data-ttu-id="7f498-169">Um endereço IP público é adicionado por meio da associação de um recurso de endereço IP público a uma nova configuração de IP ou a uma configuração de IP existente.</span><span class="sxs-lookup"><span data-stu-id="7f498-169">A public IP address is added by associating a public IP address resource to either a new IP configuration or an existing IP configuration.</span></span> <span data-ttu-id="7f498-170">Conclua as etapas em uma das seções a seguir, quando você precisar.</span><span class="sxs-lookup"><span data-stu-id="7f498-170">Complete the steps in one of the sections that follow, as you require.</span></span>

    > [!NOTE]
    > <span data-ttu-id="7f498-171">Endereços IP públicos têm um valor nominal.</span><span class="sxs-lookup"><span data-stu-id="7f498-171">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="7f498-172">Para saber mais sobre preços de endereço IP, leia a página [Preços de endereço IP](https://azure.microsoft.com/pricing/details/ip-addresses) .</span><span class="sxs-lookup"><span data-stu-id="7f498-172">To learn more about IP address pricing, read the [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="7f498-173">Há um limite para o número de endereços IP públicos que podem ser usados em uma assinatura.</span><span class="sxs-lookup"><span data-stu-id="7f498-173">There is a limit to the number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="7f498-174">Para saber mais sobre os limites, leia o artigo [Limites do Azure](../azure-subscription-service-limits.md#networking-limits).</span><span class="sxs-lookup"><span data-stu-id="7f498-174">To learn more about the limits, read the [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>
    >

    - <span data-ttu-id="7f498-175">**Associar o recurso de endereço IP público a uma nova configuração de IP**</span><span class="sxs-lookup"><span data-stu-id="7f498-175">**Associate the public IP address resource to a new IP configuration**</span></span>
    
        <span data-ttu-id="7f498-176">Sempre que você adicionar um endereço IP público em uma nova configuração de IP, também deverá adicionar um endereço IP privado, pois todas as configurações de IP devem ter um endereço IP privado.</span><span class="sxs-lookup"><span data-stu-id="7f498-176">Whenever you add a public IP address in a new IP configuration, you must also add a private IP address, because all IP configurations must have a private IP address.</span></span> <span data-ttu-id="7f498-177">Você pode adicionar um recurso de endereço IP público existente ou criar um novo.</span><span class="sxs-lookup"><span data-stu-id="7f498-177">You can either add an existing public IP address resource, or create a new one.</span></span> <span data-ttu-id="7f498-178">Para criar um novo, insira o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="7f498-178">To create a new one, enter the following command:</span></span>
    
        ```powershell
        $myPublicIp3 = New-AzureRmPublicIpAddress `
        -Name "myPublicIp3" `
        -ResourceGroupName $RgName `
        -Location $Location `
        -AllocationMethod Static
        ```

        <span data-ttu-id="7f498-179">Para criar uma nova configuração de IP com um endereço IP privado estático e o recurso de endereço IP público *myPublicIp3* associado, insira o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="7f498-179">To create a new IP configuration with a static private IP address and the associated *myPublicIp3* public IP address resource, enter the following command:</span></span>

        ```powershell
        Add-AzureRmNetworkInterfaceIpConfig `
        -Name IPConfig-4 `
        -NetworkInterface $myNIC `
        -Subnet $Subnet `
        -PrivateIpAddress 10.0.0.7 `
        -PublicIpAddress $myPublicIp3
        ```

    - <span data-ttu-id="7f498-180">**Associar o recurso de endereço IP público a uma configuração de IP existente**</span><span class="sxs-lookup"><span data-stu-id="7f498-180">**Associate the public IP address resource to an existing IP configuration**</span></span>

        <span data-ttu-id="7f498-181">Um recurso de endereço IP público só pode ser associado a uma configuração de IP que ainda não tenha um associado.</span><span class="sxs-lookup"><span data-stu-id="7f498-181">A public IP address resource can only be associated to an IP configuration that doesn't already have one associated.</span></span> <span data-ttu-id="7f498-182">Você pode determinar se uma configuração de IP tem um endereço IP público associado inserindo o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="7f498-182">You can determine whether an IP configuration has an associated public IP address by entering the following command:</span></span>

        ```powershell
        $MyNIC.IpConfigurations | Format-Table Name, PrivateIPAddress, PublicIPAddress, Primary
        ```

        <span data-ttu-id="7f498-183">Você verá uma saída semelhante ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="7f498-183">You see output similar to the following:</span></span>

        ```     
        Name       PrivateIpAddress PublicIpAddress                                           Primary
        
        IPConfig-1 10.0.0.4         Microsoft.Azure.Commands.Network.Models.PSPublicIpAddress    True
        IPConfig-2 10.0.0.5         Microsoft.Azure.Commands.Network.Models.PSPublicIpAddress   False
        IpConfig-3 10.0.0.6                                                                     False
        ```

        <span data-ttu-id="7f498-184">Como a coluna **PublicIpAddress** para *IpConfig 3* está em branco, nenhum recurso de endereço IP público está associado a ele no momento.</span><span class="sxs-lookup"><span data-stu-id="7f498-184">Since the **PublicIpAddress** column for *IpConfig-3* is blank, no public IP address resource is currently associated to it.</span></span> <span data-ttu-id="7f498-185">Você pode adicionar um recurso de endereço IP público existente como IpConfig-3 ou inserir o seguinte comando para criar um:</span><span class="sxs-lookup"><span data-stu-id="7f498-185">You can add an existing public IP address resource to IpConfig-3, or enter the following command to create one:</span></span>

        ```powershell
        $MyPublicIp3 = New-AzureRmPublicIpAddress `
        -Name "MyPublicIp3" `
        -ResourceGroupName $RgName `
        -Location $Location -AllocationMethod Static
        ```

        <span data-ttu-id="7f498-186">Insira o comando a seguir para associar o recurso de endereço IP público à configuração de IP existente chamada *IpConfig-3*:</span><span class="sxs-lookup"><span data-stu-id="7f498-186">Enter the following command to associate the public IP address resource to the existing IP configuration named *IpConfig-3*:</span></span>
    
        ```powershell
        Set-AzureRmNetworkInterfaceIpConfig `
        -Name IpConfig-3 `
        -NetworkInterface $mynic `
        -Subnet $Subnet `
        -PublicIpAddress $myPublicIp3
        ```

6. <span data-ttu-id="7f498-187">Defina o NIC com a nova configuração de IP digitando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="7f498-187">Set the NIC with the new IP configuration by entering the following command:</span></span>

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $MyNIC
    ```

7. <span data-ttu-id="7f498-188">Exiba os endereços IP privados e o recurso de endereço IP público atribuído ao NIC digitando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="7f498-188">View the private IP addresses and the public IP address resources assigned to the NIC by entering the following command:</span></span>

    ```powershell   
    $MyNIC.IpConfigurations | Format-Table Name, PrivateIPAddress, PublicIPAddress, Primary
    ```
8. <span data-ttu-id="7f498-189">Adicione o endereço IP privado ao sistema operacional da VM executando as etapas para seu sistema operacional na seção [Adicionar endereços IP ao sistema operacional de uma VM](#os-config) deste artigo.</span><span class="sxs-lookup"><span data-stu-id="7f498-189">Add the private IP address to the VM operating system by completing the steps for your operating system in the [Add IP addresses to a VM operating system](#os-config) section of this article.</span></span> <span data-ttu-id="7f498-190">Não adicione o endereço IP público ao sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="7f498-190">Do not add the public IP address to the operating system.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
