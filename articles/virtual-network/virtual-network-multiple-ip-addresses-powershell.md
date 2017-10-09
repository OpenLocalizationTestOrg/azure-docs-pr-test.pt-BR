---
title: "aaaMultiple endereços IP para máquinas virtuais do Azure - PowerShell | Microsoft Docs"
description: "Saiba como tooassign vários endereços IP tooa virtual máquina usando o PowerShell | Gerenciador de recursos."
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
ms.openlocfilehash: df54c4386ce13521e660a3e7208c8c1ab1459bc2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="assign-multiple-ip-addresses-toovirtual-machines-using-powershell"></a><span data-ttu-id="8878f-103">Atribuir vários endereços IP máquinas toovirtual usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="8878f-103">Assign multiple IP addresses toovirtual machines using PowerShell</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]

<span data-ttu-id="8878f-104">Este artigo explica como toocreate uma máquina virtual (VM) por meio da implantação do Azure Resource Manager Olá modelo usando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8878f-104">This article explains how toocreate a virtual machine (VM) through hello Azure Resource Manager deployment model using PowerShell.</span></span> <span data-ttu-id="8878f-105">Tooresources criado por meio do modelo de implantação clássico Olá não podem ser atribuídos a vários endereços IP.</span><span class="sxs-lookup"><span data-stu-id="8878f-105">Multiple IP addresses cannot be assigned tooresources created through hello classic deployment model.</span></span> <span data-ttu-id="8878f-106">toolearn mais sobre modelos de implantação do Azure, leia Olá [entender os modelos de implantação](../resource-manager-deployment-model.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="8878f-106">toolearn more about Azure deployment models, read hello [Understand deployment models](../resource-manager-deployment-model.md) article.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <span data-ttu-id="8878f-107"><a name = "create"></a>Criar uma VM com vários endereços IP</span><span class="sxs-lookup"><span data-stu-id="8878f-107"><a name = "create"></a>Create a VM with multiple IP addresses</span></span>

<span data-ttu-id="8878f-108">etapas Olá que seguem explicam como toocreate um exemplo VM com IP vários endereços, conforme descrito no cenário de saudação.</span><span class="sxs-lookup"><span data-stu-id="8878f-108">hello steps that follow explain how toocreate an example VM with multiple IP addresses, as described in hello scenario.</span></span> <span data-ttu-id="8878f-109">Altere os valores da variável conforme exigido por sua implementação.</span><span class="sxs-lookup"><span data-stu-id="8878f-109">Change variable values as required for your implementation.</span></span>

1. <span data-ttu-id="8878f-110">Abra um prompt de comando do PowerShell e as etapas de saudação completa restantes nesta seção dentro de uma única sessão do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8878f-110">Open a PowerShell command prompt and complete hello remaining steps in this section within a single PowerShell session.</span></span> <span data-ttu-id="8878f-111">Se você ainda não tiver o PowerShell instalado e configurado, Olá concluir etapas no hello [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) artigo.</span><span class="sxs-lookup"><span data-stu-id="8878f-111">If you don't already have PowerShell installed and configured, complete hello steps in hello [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) article.</span></span>
2. <span data-ttu-id="8878f-112">Conta de logon do tooyour com hello `login-azurermaccount` comando.</span><span class="sxs-lookup"><span data-stu-id="8878f-112">Login tooyour account with hello `login-azurermaccount` command.</span></span>
3. <span data-ttu-id="8878f-113">Substitua *myResourceGroup* e *westus* por um nome e local de sua escolha.</span><span class="sxs-lookup"><span data-stu-id="8878f-113">Replace *myResourceGroup* and *westus* with a name and location of your choosing.</span></span> <span data-ttu-id="8878f-114">Crie um grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="8878f-114">Create a resource group.</span></span> <span data-ttu-id="8878f-115">Um grupo de recursos é um contêiner lógico no qual os recursos do Azure são implantados e gerenciados.</span><span class="sxs-lookup"><span data-stu-id="8878f-115">A resource group is a logical container into which Azure resources are deployed and managed.</span></span>

    ```powershell
    $RgName   = "MyResourceGroup"
    $Location = "westus"

    New-AzureRmResourceGroup `
    -Name $RgName `
    -Location $Location
    ```

4. <span data-ttu-id="8878f-116">Criar uma rede virtual (VNet) e a sub-rede no hello mesmo local que o grupo de recursos de saudação:</span><span class="sxs-lookup"><span data-stu-id="8878f-116">Create a virtual network (VNet) and subnet in hello same location as hello resource group:</span></span>

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

    # Get hello subnet object
    $Subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name $SubnetConfig.Name -VirtualNetwork $VNet
    ```

5. <span data-ttu-id="8878f-117">Crie um NSG (grupo de segurança de rede) e uma regra.</span><span class="sxs-lookup"><span data-stu-id="8878f-117">Create a network security group (NSG) and a rule.</span></span> <span data-ttu-id="8878f-118">Olá NSG protege Olá VM usando regras de entrada e saídas.</span><span class="sxs-lookup"><span data-stu-id="8878f-118">hello NSG secures hello VM using inbound and outbound rules.</span></span> <span data-ttu-id="8878f-119">Nesse caso, uma regra de entrada é criada para a porta 3389, que permite conexões de área de trabalho remota.</span><span class="sxs-lookup"><span data-stu-id="8878f-119">In this case, an inbound rule is created for port 3389, which allows incoming remote desktop connections.</span></span>

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

6. <span data-ttu-id="8878f-120">Definir a configuração de IP primária Olá para Olá NIC.</span><span class="sxs-lookup"><span data-stu-id="8878f-120">Define hello primary IP configuration for hello NIC.</span></span> <span data-ttu-id="8878f-121">Alteração 10.0.0.4 tooa válido na sub-rede Olá criado, se você não usou o valor de saudação definido anteriormente.</span><span class="sxs-lookup"><span data-stu-id="8878f-121">Change 10.0.0.4 tooa valid address in hello subnet you created, if you didn't use hello value defined previously.</span></span> <span data-ttu-id="8878f-122">Antes de atribuir um endereço IP estático, é recomendável que você primeiro confirme que ele ainda não está em uso.</span><span class="sxs-lookup"><span data-stu-id="8878f-122">Before assigning a static IP address, it's recommended that you first confirm it's not already in use.</span></span> <span data-ttu-id="8878f-123">Digite o comando Olá `Test-AzureRmPrivateIPAddressAvailability -IPAddress 10.0.0.4 -VirtualNetwork $VNet`.</span><span class="sxs-lookup"><span data-stu-id="8878f-123">Enter hello command `Test-AzureRmPrivateIPAddressAvailability -IPAddress 10.0.0.4 -VirtualNetwork $VNet`.</span></span> <span data-ttu-id="8878f-124">Se o endereço Olá estiver disponível, Olá saída retorna *True*.</span><span class="sxs-lookup"><span data-stu-id="8878f-124">If hello address is available, hello output returns *True*.</span></span> <span data-ttu-id="8878f-125">Se não estiver disponível, Olá saída retorna *False* e uma lista de endereços que estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="8878f-125">If it's not available, hello output returns *False* and a list of addresses that are available.</span></span> 

    <span data-ttu-id="8878f-126">Em Olá comandos a seguir **substitua < substituir-com-seu-exclusivo-name > toouse de nome DNS exclusivo hello.**</span><span class="sxs-lookup"><span data-stu-id="8878f-126">In hello following commands, **Replace <replace-with-your-unique-name> with hello unique DNS name toouse.**</span></span> <span data-ttu-id="8878f-127">nome da saudação deve ser exclusivo entre todos os endereços IP públicos em uma região do Azure.</span><span class="sxs-lookup"><span data-stu-id="8878f-127">hello name must be unique across all public IP addresses within an Azure region.</span></span> <span data-ttu-id="8878f-128">Este é um parâmetro opcional.</span><span class="sxs-lookup"><span data-stu-id="8878f-128">This is an optional parameter.</span></span> <span data-ttu-id="8878f-129">Ele pode ser removido se você quiser apenas tooconnect toohello VM usando o endereço IP público de saudação.</span><span class="sxs-lookup"><span data-stu-id="8878f-129">It can be removed if you only want tooconnect toohello VM using hello public IP address.</span></span>

    ```powershell
    
    # Create a public IP address
    $PublicIP1 = New-AzureRmPublicIpAddress `
    -Name "MyPublicIP1" `
    -ResourceGroupName $RgName `
    -Location $Location `
    -DomainNameLabel <replace-with-your-unique-name> `
    -AllocationMethod Static
        
    #Create an IP configuration with a static private IP address and assign hello public IP ddress tooit
    $IpConfigName1 = "IPConfig-1"
    $IpConfig1     = New-AzureRmNetworkInterfaceIpConfig `
    -Name $IpConfigName1 `
    -Subnet $Subnet `
    -PrivateIpAddress 10.0.0.4 `
    -PublicIpAddress $PublicIP1 `
    -Primary
    ```

    <span data-ttu-id="8878f-130">Quando você atribui vários tooa de configurações de IP NIC, uma configuração deve ser atribuída como Olá *-primário*.</span><span class="sxs-lookup"><span data-stu-id="8878f-130">When you assign multiple IP configurations tooa NIC, one configuration must be assigned as hello *-Primary*.</span></span>

    > [!NOTE]
    > <span data-ttu-id="8878f-131">Endereços IP públicos têm um valor nominal.</span><span class="sxs-lookup"><span data-stu-id="8878f-131">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="8878f-132">toolearn mais sobre endereços IP de preços, ler Olá [preço do endereço IP](https://azure.microsoft.com/pricing/details/ip-addresses) página.</span><span class="sxs-lookup"><span data-stu-id="8878f-132">toolearn more about IP address pricing, read hello [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="8878f-133">Há um número de toohello limite de endereços IP públicos que podem ser usados em uma assinatura.</span><span class="sxs-lookup"><span data-stu-id="8878f-133">There is a limit toohello number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="8878f-134">mais sobre os limites de Olá Olá de leitura de toolearn [Azure limita](../azure-subscription-service-limits.md#networking-limits) artigo.</span><span class="sxs-lookup"><span data-stu-id="8878f-134">toolearn more about hello limits, read hello [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>

7. <span data-ttu-id="8878f-135">Definir as configurações de IP secundárias Olá para Olá NIC.</span><span class="sxs-lookup"><span data-stu-id="8878f-135">Define hello secondary IP configurations for hello NIC.</span></span> <span data-ttu-id="8878f-136">Você pode adicionar, remover ou alterar as configurações conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="8878f-136">You can add or remove configurations as necessary.</span></span> <span data-ttu-id="8878f-137">Cada configuração de IP deve ter um endereço IP privado atribuído.</span><span class="sxs-lookup"><span data-stu-id="8878f-137">Each IP configuration must have a private IP address assigned.</span></span> <span data-ttu-id="8878f-138">Cada configuração pode, opcionalmente, ter um endereço IP público atribuído.</span><span class="sxs-lookup"><span data-stu-id="8878f-138">Each configuration can optionally have one public IP address assigned.</span></span>

    ```powershell
    
    # Create a public IP address
    $PublicIP2 = New-AzureRmPublicIpAddress `
    -Name "MyPublicIP2" `
    -ResourceGroupName $RgName `
    -Location $Location `
    -AllocationMethod Static
        
    #Create an IP configuration with a static private IP address and assign hello public IP ddress tooit
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

8. <span data-ttu-id="8878f-139">Criar hello NIC e associar Olá três tooit de configurações de IP:</span><span class="sxs-lookup"><span data-stu-id="8878f-139">Create hello NIC and associate hello three IP configurations tooit:</span></span>

    ```powershell
    
    $NIC = New-AzureRmNetworkInterface `
    -Name MyNIC `
    -ResourceGroupName $RgName `
    -Location $Location `
    -NetworkSecurityGroupId $NSG.Id `
    -IpConfiguration $IpConfig1,$IpConfig2,$IpConfig3
    ```

    >[!NOTE]
    ><span data-ttu-id="8878f-140">Embora todas as configurações são atribuídas tooone NIC neste artigo, você pode atribuir várias IP configurações tooevery NIC conectada toohello VM.</span><span class="sxs-lookup"><span data-stu-id="8878f-140">Though all configurations are assigned tooone NIC in this article, you can assign multiple IP configurations tooevery NIC attached toohello VM.</span></span> <span data-ttu-id="8878f-141">toolearn como toocreate uma VM com várias NICs, ler Olá [criar uma VM com várias NICs](virtual-network-deploy-multinic-arm-ps.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="8878f-141">toolearn how toocreate a VM with multiple NICs, read hello [Create a VM with multiple NICs](virtual-network-deploy-multinic-arm-ps.md) article.</span></span>

9. <span data-ttu-id="8878f-142">Crie hello VM inserindo Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="8878f-142">Create hello VM by entering hello following commands:</span></span>

    ```powershell
    
    # Define a credential object. When you run these commands, you're prompted tooenter a sername and password for hello VM you're reating.
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
    
    # Create hello VM
    New-AzureRmVM `
    -ResourceGroupName $RgName `
    -Location $Location `
    -VM $VmConfig
    ```

10. <span data-ttu-id="8878f-143">IP privado de saudação adicionar endereços toohello sistema de operacional VM por etapas para seu sistema operacional no Olá Olá [tooa sistema de operacional VM de endereços de IP adicionar](#os-config) deste artigo.</span><span class="sxs-lookup"><span data-stu-id="8878f-143">Add hello private IP addresses toohello VM operating system by completing hello steps for your operating system in hello [Add IP addresses tooa VM operating system](#os-config) section of this article.</span></span> <span data-ttu-id="8878f-144">Não adicione Olá pública IP endereços toohello sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="8878f-144">Do not add hello public IP addresses toohello operating system.</span></span>

## <span data-ttu-id="8878f-145"><a name="add"></a>Adicionar endereços IP tooa VM</span><span class="sxs-lookup"><span data-stu-id="8878f-145"><a name="add"></a>Add IP addresses tooa VM</span></span>

<span data-ttu-id="8878f-146">Você pode adicionar pública e privada tooa de endereços IP NIC completando as etapas de saudação que seguem.</span><span class="sxs-lookup"><span data-stu-id="8878f-146">You can add private and public IP addresses tooa NIC by completing hello steps that follow.</span></span> <span data-ttu-id="8878f-147">Olá exemplos Olá seções a seguir pressupõem que você já tem uma máquina virtual com configurações de IP hello três descritas em hello [cenário](#Scenario) neste artigo, mas ele não é necessário que você faça.</span><span class="sxs-lookup"><span data-stu-id="8878f-147">hello examples in hello following sections assume that you already have a VM with hello three IP configurations described in hello [scenario](#Scenario) in this article, but it's not required that you do.</span></span>

1. <span data-ttu-id="8878f-148">Abra um prompt de comando do PowerShell e as etapas de saudação completa restantes nesta seção dentro de uma única sessão do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="8878f-148">Open a PowerShell command prompt and complete hello remaining steps in this section within a single PowerShell session.</span></span> <span data-ttu-id="8878f-149">Se você ainda não tiver o PowerShell instalado e configurado, Olá concluir etapas no hello [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview) artigo.</span><span class="sxs-lookup"><span data-stu-id="8878f-149">If you don't already have PowerShell installed and configured, complete hello steps in hello [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) article.</span></span>
2. <span data-ttu-id="8878f-150">Alterar hello "valores" dos Olá após $Variables toohello nome da saudação NIC que você deseja tooadd IP endereço tooand Olá recurso grupo e local Olá em que NIC existe:</span><span class="sxs-lookup"><span data-stu-id="8878f-150">Change hello "values" of hello following $Variables toohello name of hello NIC you want tooadd IP address tooand hello resource group and location hello NIC exists in:</span></span>

    ```powershell
    $NicName  = "MyNIC"
    $RgName   = "MyResourceGroup"
    $Location = "westus"
    ```

    <span data-ttu-id="8878f-151">Se você não souber o nome de saudação do hello NIC que você deseja toochange, digite Olá comandos a seguir, altere os valores hello variáveis anteriores hello:</span><span class="sxs-lookup"><span data-stu-id="8878f-151">If you don't know hello name of hello NIC you want toochange, enter hello following commands, then change hello values of hello previous variables:</span></span>

    ```powershell
    Get-AzureRmNetworkInterface | Format-Table Name, ResourceGroupName, Location
    ```
3. <span data-ttu-id="8878f-152">Crie uma variável e defina-a como toohello existente NIC digitando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="8878f-152">Create a variable and set it toohello existing NIC by typing hello following command:</span></span>

    ```powershell
    $MyNIC = Get-AzureRmNetworkInterface -Name $NicName -ResourceGroupName $RgName
    ```
4. <span data-ttu-id="8878f-153">Olá comandos a seguir, alterar *MyVNet* e *MySubnet* toohello nomes de Olá Olá rede virtual e sub-rede NIC está conectada ao.</span><span class="sxs-lookup"><span data-stu-id="8878f-153">In hello following commands, change *MyVNet* and *MySubnet* toohello names of hello VNet and subnet hello NIC is connected to.</span></span> <span data-ttu-id="8878f-154">Digite hello comandos tooretrieve Olá rede virtual e sub-rede objetos Olá A que NIC está conectada:</span><span class="sxs-lookup"><span data-stu-id="8878f-154">Enter hello commands tooretrieve hello VNet and subnet objects hello NIC is connected to:</span></span>

    ```powershell
    $MyVNet = Get-AzureRMVirtualnetwork -Name MyVNet -ResourceGroupName $RgName
    $Subnet = $MyVnet.Subnets | Where-Object { $_.Name -eq "MySubnet" }
    ```
    <span data-ttu-id="8878f-155">Se você não souber Olá redes ou sub-redes nome hello que NIC está conectada ao, digite Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="8878f-155">If you don't know hello VNet or subnet name hello NIC is connected to, enter hello following command:</span></span>
    ```powershell
    $MyNIC.IpConfigurations
    ```
    <span data-ttu-id="8878f-156">Na saída de hello, procure texto toohello semelhante a saída de exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="8878f-156">In hello output, look for text similar toohello following example output:</span></span>
    
    ```
    "Id": "/subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/MyVNet/subnets/MySubnet"
    ```
    <span data-ttu-id="8878f-157">Na saída, *MyVnet* é hello VNet e *MySubnet* é Olá sub-rede hello NIC está conectada ao.</span><span class="sxs-lookup"><span data-stu-id="8878f-157">In this output, *MyVnet* is hello VNet and *MySubnet* is hello subnet hello NIC is connected to.</span></span>

5. <span data-ttu-id="8878f-158">Conclua as etapas de saudação em uma das seguintes seções, com base nas necessidades de saudação:</span><span class="sxs-lookup"><span data-stu-id="8878f-158">Complete hello steps in one of hello following sections, based on your requirements:</span></span>

    <span data-ttu-id="8878f-159">**Adicionar um endereço IP privado**</span><span class="sxs-lookup"><span data-stu-id="8878f-159">**Add a private IP address**</span></span>

    <span data-ttu-id="8878f-160">tooadd um tooa de endereço IP privado NIC, você deve criar uma configuração de IP.</span><span class="sxs-lookup"><span data-stu-id="8878f-160">tooadd a private IP address tooa NIC, you must create an IP configuration.</span></span> <span data-ttu-id="8878f-161">Olá comando a seguir cria uma configuração com um endereço IP estático de 10.0.0.7.</span><span class="sxs-lookup"><span data-stu-id="8878f-161">hello following command creates a configuration with a static IP address of 10.0.0.7.</span></span> <span data-ttu-id="8878f-162">Ao especificar um endereço IP estático, ele deve ser um endereço não usado para a sub-rede de saudação.</span><span class="sxs-lookup"><span data-stu-id="8878f-162">When specifying a static IP address, it must be an unused address for hello subnet.</span></span> <span data-ttu-id="8878f-163">É recomendável que você primeiro teste Olá endereço tooensure está disponível digitando Olá `Test-AzureRmPrivateIPAddressAvailability -IPAddress 10.0.0.7 -VirtualNetwork $myVnet` comando.</span><span class="sxs-lookup"><span data-stu-id="8878f-163">It's recommended that you first test hello address tooensure it's available by entering hello `Test-AzureRmPrivateIPAddressAvailability -IPAddress 10.0.0.7 -VirtualNetwork $myVnet` command.</span></span> <span data-ttu-id="8878f-164">Se o endereço IP hello estiver disponível, Olá saída retorna *True*.</span><span class="sxs-lookup"><span data-stu-id="8878f-164">If hello IP address is available, hello output returns *True*.</span></span> <span data-ttu-id="8878f-165">Se não estiver disponível, Olá saída retorna *False*e uma lista de endereços que estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="8878f-165">If it's not available, hello output returns *False*, and a list of addresses that are available.</span></span>

    ```powershell
    Add-AzureRmNetworkInterfaceIpConfig -Name IPConfig-4 -NetworkInterface `
    $MyNIC -Subnet $Subnet -PrivateIpAddress 10.0.0.7
    ```
    <span data-ttu-id="8878f-166">Crie quantas configurações forem necessárias, usando nomes de configuração exclusivos e endereços IP privados (para configurações com endereços IP estáticos).</span><span class="sxs-lookup"><span data-stu-id="8878f-166">Create as many configurations as you require, using unique configuration names and private IP addresses (for configurations with static IP addresses).</span></span>

    <span data-ttu-id="8878f-167">Adicionar Olá privada IP endereço toohello VM sistema operacional concluindo as etapas de saudação para seu sistema operacional no hello [tooa sistema de operacional VM de endereços de IP adicionar](#os-config) deste artigo.</span><span class="sxs-lookup"><span data-stu-id="8878f-167">Add hello private IP address toohello VM operating system by completing hello steps for your operating system in hello [Add IP addresses tooa VM operating system](#os-config) section of this article.</span></span>

    <span data-ttu-id="8878f-168">**Adicionar um endereço IP público**</span><span class="sxs-lookup"><span data-stu-id="8878f-168">**Add a public IP address**</span></span>

    <span data-ttu-id="8878f-169">Um endereço IP público é adicionado ao associar um tooeither de recurso de endereço IP público, uma nova configuração de IP ou uma configuração de IP existente.</span><span class="sxs-lookup"><span data-stu-id="8878f-169">A public IP address is added by associating a public IP address resource tooeither a new IP configuration or an existing IP configuration.</span></span> <span data-ttu-id="8878f-170">Conclua as etapas de saudação em uma saudação próximas seções, você precisa.</span><span class="sxs-lookup"><span data-stu-id="8878f-170">Complete hello steps in one of hello sections that follow, as you require.</span></span>

    > [!NOTE]
    > <span data-ttu-id="8878f-171">Endereços IP públicos têm um valor nominal.</span><span class="sxs-lookup"><span data-stu-id="8878f-171">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="8878f-172">toolearn mais sobre endereços IP de preços, ler Olá [preço do endereço IP](https://azure.microsoft.com/pricing/details/ip-addresses) página.</span><span class="sxs-lookup"><span data-stu-id="8878f-172">toolearn more about IP address pricing, read hello [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="8878f-173">Há um número de toohello limite de endereços IP públicos que podem ser usados em uma assinatura.</span><span class="sxs-lookup"><span data-stu-id="8878f-173">There is a limit toohello number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="8878f-174">mais sobre os limites de Olá Olá de leitura de toolearn [Azure limita](../azure-subscription-service-limits.md#networking-limits) artigo.</span><span class="sxs-lookup"><span data-stu-id="8878f-174">toolearn more about hello limits, read hello [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>
    >

    - <span data-ttu-id="8878f-175">**Associar Olá pública recurso tooa novo IP configuração de endereço IP**</span><span class="sxs-lookup"><span data-stu-id="8878f-175">**Associate hello public IP address resource tooa new IP configuration**</span></span>
    
        <span data-ttu-id="8878f-176">Sempre que você adicionar um endereço IP público em uma nova configuração de IP, também deverá adicionar um endereço IP privado, pois todas as configurações de IP devem ter um endereço IP privado.</span><span class="sxs-lookup"><span data-stu-id="8878f-176">Whenever you add a public IP address in a new IP configuration, you must also add a private IP address, because all IP configurations must have a private IP address.</span></span> <span data-ttu-id="8878f-177">Você pode adicionar um recurso de endereço IP público existente ou criar um novo.</span><span class="sxs-lookup"><span data-stu-id="8878f-177">You can either add an existing public IP address resource, or create a new one.</span></span> <span data-ttu-id="8878f-178">toocreate uma nova, digite Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="8878f-178">toocreate a new one, enter hello following command:</span></span>
    
        ```powershell
        $myPublicIp3 = New-AzureRmPublicIpAddress `
        -Name "myPublicIp3" `
        -ResourceGroupName $RgName `
        -Location $Location `
        -AllocationMethod Static
        ```

        <span data-ttu-id="8878f-179">toocreate uma nova configuração de IP com um endereço IP privado estático e Olá associados *myPublicIp3* IP público recurso de endereço, digite Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="8878f-179">toocreate a new IP configuration with a static private IP address and hello associated *myPublicIp3* public IP address resource, enter hello following command:</span></span>

        ```powershell
        Add-AzureRmNetworkInterfaceIpConfig `
        -Name IPConfig-4 `
        -NetworkInterface $myNIC `
        -Subnet $Subnet `
        -PrivateIpAddress 10.0.0.7 `
        -PublicIpAddress $myPublicIp3
        ```

    - <span data-ttu-id="8878f-180">**Associar Olá pública recurso tooan existente IP configuração de endereço IP**</span><span class="sxs-lookup"><span data-stu-id="8878f-180">**Associate hello public IP address resource tooan existing IP configuration**</span></span>

        <span data-ttu-id="8878f-181">Um recurso de endereço IP público só pode ser a configuração de IP tooan associado que ainda não tiver um associado.</span><span class="sxs-lookup"><span data-stu-id="8878f-181">A public IP address resource can only be associated tooan IP configuration that doesn't already have one associated.</span></span> <span data-ttu-id="8878f-182">Você pode determinar se uma configuração de IP tem um endereço IP público associado inserindo Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="8878f-182">You can determine whether an IP configuration has an associated public IP address by entering hello following command:</span></span>

        ```powershell
        $MyNIC.IpConfigurations | Format-Table Name, PrivateIPAddress, PublicIPAddress, Primary
        ```

        <span data-ttu-id="8878f-183">Consulte o seguinte de toohello semelhante de saída:</span><span class="sxs-lookup"><span data-stu-id="8878f-183">You see output similar toohello following:</span></span>

        ```     
        Name       PrivateIpAddress PublicIpAddress                                           Primary
        
        IPConfig-1 10.0.0.4         Microsoft.Azure.Commands.Network.Models.PSPublicIpAddress    True
        IPConfig-2 10.0.0.5         Microsoft.Azure.Commands.Network.Models.PSPublicIpAddress   False
        IpConfig-3 10.0.0.6                                                                     False
        ```

        <span data-ttu-id="8878f-184">Desde Olá **PublicIpAddress** coluna para *IpConfig 3* está em branco, nenhum recurso de endereço IP público é tooit atualmente associado.</span><span class="sxs-lookup"><span data-stu-id="8878f-184">Since hello **PublicIpAddress** column for *IpConfig-3* is blank, no public IP address resource is currently associated tooit.</span></span> <span data-ttu-id="8878f-185">Você pode adicionar um existente pública IP endereço recurso tooIpConfig-3, ou insira Olá toocreate comando um a seguir:</span><span class="sxs-lookup"><span data-stu-id="8878f-185">You can add an existing public IP address resource tooIpConfig-3, or enter hello following command toocreate one:</span></span>

        ```powershell
        $MyPublicIp3 = New-AzureRmPublicIpAddress `
        -Name "MyPublicIp3" `
        -ResourceGroupName $RgName `
        -Location $Location -AllocationMethod Static
        ```

        <span data-ttu-id="8878f-186">Digite hello recurso toohello existente IP configuração denominada do endereço IP público do tooassociate Olá de comando a seguir *3 IpConfig*:</span><span class="sxs-lookup"><span data-stu-id="8878f-186">Enter hello following command tooassociate hello public IP address resource toohello existing IP configuration named *IpConfig-3*:</span></span>
    
        ```powershell
        Set-AzureRmNetworkInterfaceIpConfig `
        -Name IpConfig-3 `
        -NetworkInterface $mynic `
        -Subnet $Subnet `
        -PublicIpAddress $myPublicIp3
        ```

6. <span data-ttu-id="8878f-187">Defina Olá NIC com a nova configuração de IP hello inserindo Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="8878f-187">Set hello NIC with hello new IP configuration by entering hello following command:</span></span>

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $MyNIC
    ```

7. <span data-ttu-id="8878f-188">Exibir endereços IP privados de saudação e Olá pública IP endereço recursos atribuído toohello NIC inserindo Olá o comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="8878f-188">View hello private IP addresses and hello public IP address resources assigned toohello NIC by entering hello following command:</span></span>

    ```powershell   
    $MyNIC.IpConfigurations | Format-Table Name, PrivateIPAddress, PublicIPAddress, Primary
    ```
8. <span data-ttu-id="8878f-189">Adicionar Olá privada IP endereço toohello VM sistema operacional concluindo as etapas de saudação para seu sistema operacional no hello [tooa sistema de operacional VM de endereços de IP adicionar](#os-config) deste artigo.</span><span class="sxs-lookup"><span data-stu-id="8878f-189">Add hello private IP address toohello VM operating system by completing hello steps for your operating system in hello [Add IP addresses tooa VM operating system](#os-config) section of this article.</span></span> <span data-ttu-id="8878f-190">Não adicione Olá pública IP endereço toohello sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="8878f-190">Do not add hello public IP address toohello operating system.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
