---
title: "endereços IP privados de aaaConfigure para VMs - PowerShell do Azure | Microsoft Docs"
description: "Saiba como endereços IP privados tooconfigure máquinas virtuais usando o PowerShell."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: d5f18929-15e3-40a2-9ee3-8188bc248ed8
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/23/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 4a3eb67de583e08208fcab40de1c2a8a9b65618c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-using-powershell"></a><span data-ttu-id="755e9-103">Configurar endereços IP particulares para uma máquina virtual usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="755e9-103">Configure private IP addresses for a virtual machine using PowerShell</span></span>

[!INCLUDE [virtual-networks-static-private-ip-selectors-arm-include](../../includes/virtual-networks-static-private-ip-selectors-arm-include.md)]

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

<span data-ttu-id="755e9-104">O Azure tem dois modelos de implantação: Azure Resource Manager e clássico.</span><span class="sxs-lookup"><span data-stu-id="755e9-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="755e9-105">A Microsoft recomenda a criação de recursos por meio do modelo de implantação do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="755e9-105">Microsoft recommends creating resources through hello Resource Manager deployment model.</span></span> <span data-ttu-id="755e9-106">mais sobre toolearn Olá diferenças entre modelos de saudação dois ler Olá [modelos de implantação do Azure entender](../azure-resource-manager/resource-manager-deployment-model.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="755e9-106">toolearn more about hello differences between hello two models, read hello [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span> <span data-ttu-id="755e9-107">Este artigo aborda o modelo de implantação do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="755e9-107">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="755e9-108">Você também pode [gerenciar o endereço IP privado estático no modelo de implantação clássico Olá](virtual-networks-static-private-ip-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="755e9-108">You can also [manage static private IP address in hello classic deployment model](virtual-networks-static-private-ip-classic-ps.md).</span></span>

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

<span data-ttu-id="755e9-109">exemplo Hello PowerShell comandos abaixo esperam um ambiente simples já foi criado com base no cenário de saudação acima.</span><span class="sxs-lookup"><span data-stu-id="755e9-109">hello sample PowerShell commands below expect a simple environment already created based on hello scenario above.</span></span> <span data-ttu-id="755e9-110">Se você quiser comandos de saudação toorun conforme elas são exibidas neste documento, primeiro criar o ambiente de teste de hello, descrito em [criar uma rede virtual](virtual-networks-create-vnet-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="755e9-110">If you want toorun hello commands as they are displayed in this document, first build hello test environment described in [create a vnet](virtual-networks-create-vnet-arm-ps.md).</span></span>

## <a name="create-a-vm-with-a-static-private-ip-address"></a><span data-ttu-id="755e9-111">Criar uma VM com um endereço IP privado estático</span><span class="sxs-lookup"><span data-stu-id="755e9-111">Create a VM with a static private IP address</span></span>
<span data-ttu-id="755e9-112">toocreate uma VM denominada *DNS01* em Olá *front-end* sub-rede de uma rede virtual denominada *TestVNet* com um endereço IP privado estático de *192.168.1.101*, Siga as etapas de saudação abaixo:</span><span class="sxs-lookup"><span data-stu-id="755e9-112">toocreate a VM named *DNS01* in hello *FrontEnd* subnet of a VNet named *TestVNet* with a static private IP of *192.168.1.101*, follow hello steps below:</span></span>

1. <span data-ttu-id="755e9-113">Defina variáveis para a conta de armazenamento hello, local, grupo de recursos e toobe de credenciais usado.</span><span class="sxs-lookup"><span data-stu-id="755e9-113">Set variables for hello storage account, location, resource group, and credentials toobe used.</span></span> <span data-ttu-id="755e9-114">Você precisará tooenter um nome de usuário e senha para Olá VM.</span><span class="sxs-lookup"><span data-stu-id="755e9-114">You will need tooenter a user name and password for hello VM.</span></span> <span data-ttu-id="755e9-115">grupo de contas e recursos de armazenamento Olá já deve existir.</span><span class="sxs-lookup"><span data-stu-id="755e9-115">hello storage account and resource group must already exist.</span></span>

    ```powershell
    $stName  = "vnetstorage"
    $locName = "Central US"
    $rgName  = "TestRG"
    $cred    = Get-Credential -Message "Type hello name and password of hello local administrator account."
    ```

2. <span data-ttu-id="755e9-116">Recuperar Olá uma rede virtual e sub-rede que deseja toocreate Olá VM.</span><span class="sxs-lookup"><span data-stu-id="755e9-116">Retrieve hello virtual network and subnet you want toocreate hello VM in.</span></span>

    ```powershell
    $vnet   = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    $subnet = $vnet.Subnets[0].Id
    ```

3. <span data-ttu-id="755e9-117">Se necessário, crie um tooaccess endereço IP público Olá VM de saudação à Internet.</span><span class="sxs-lookup"><span data-stu-id="755e9-117">If necessary, create a public IP address tooaccess hello VM from hello Internet.</span></span>

    ```powershell
    $pip = New-AzureRmPublicIpAddress -Name TestPIP -ResourceGroupName $rgName `
    -Location $locName -AllocationMethod Dynamic
    ```

4. <span data-ttu-id="755e9-118">Crie uma NIC usando Olá endereço IP privado estático desejado tooassign toohello VM.</span><span class="sxs-lookup"><span data-stu-id="755e9-118">Create a NIC using hello static private IP address you want tooassign toohello VM.</span></span> <span data-ttu-id="755e9-119">Certifique-se de IP de saudação é saudação do intervalo de sub-rede está adicionando Olá VM.</span><span class="sxs-lookup"><span data-stu-id="755e9-119">Make sure hello IP is from hello subnet range you are adding hello VM to.</span></span> <span data-ttu-id="755e9-120">Esta é a etapa principal Olá neste artigo, onde você definir Olá toobe IP privado estático.</span><span class="sxs-lookup"><span data-stu-id="755e9-120">This is hello main step for this article, where you set hello private IP toobe static.</span></span>

    ```powershell
    $nic = New-AzureRmNetworkInterface -Name TestNIC -ResourceGroupName $rgName `
    -Location $locName -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id `
    -PrivateIpAddress 192.168.1.101
    ```

5. <span data-ttu-id="755e9-121">Crie hello VM usando Olá NIC criado acima.</span><span class="sxs-lookup"><span data-stu-id="755e9-121">Create hello VM using hello NIC created above.</span></span>

    ```powershell
    $vm = New-AzureRmVMConfig -VMName DNS01 -VMSize "Standard_A1"
    $vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName DNS01 `
    -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm = Set-AzureRmVMSourceImage -VM $vm -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer -Skus 2012-R2-Datacenter -Version "latest"
    $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
    $osDiskUri = $storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/WindowsVMosDisk.vhd"
    $vm = Set-AzureRmVMOSDisk -VM $vm -Name "windowsvmosdisk" -VhdUri $osDiskUri `
    -CreateOption fromImage
    New-AzureRmVM -ResourceGroupName $rgName -Location $locName -VM $vm 
    ```

    <span data-ttu-id="755e9-122">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="755e9-122">Expected output:</span></span>
    
        EndTime             : [Date and time]
        Error               : 
        Output              : 
        StartTime           : [Date and time]
        Status              : Succeeded
        TrackingOperationId : [Id]
        RequestId           : [Id]
        StatusCode          : OK 

## <a name="retrieve-static-private-ip-address-information-for-a-network-interface"></a><span data-ttu-id="755e9-123">Recuperar informações de endereço IP privado estático para uma interface de rede</span><span class="sxs-lookup"><span data-stu-id="755e9-123">Retrieve static private IP address information for a network interface</span></span>
<span data-ttu-id="755e9-124">tooview Olá IP privado estático informações sobre endereço de saudação VM criada com o script de saudação acima, execute Olá comando PowerShell a seguir e observe os valores hello para *PrivateIpAddress* e  *PrivateIpAllocationMethod*:</span><span class="sxs-lookup"><span data-stu-id="755e9-124">tooview hello static private IP address information for hello VM created with hello script above, run hello following PowerShell command and observe hello values for *PrivateIpAddress* and *PrivateIpAllocationMethod*:</span></span>

```powershell
Get-AzureRmNetworkInterface -Name TestNIC -ResourceGroupName TestRG
```

<span data-ttu-id="755e9-125">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="755e9-125">Expected output:</span></span>

    Name                 : TestNIC
    ResourceGroupName    : TestRG
    Location             : centralus
    Id                   : /subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC
    Etag                 : W/"[Id]"
    ProvisioningState    : Succeeded
    Tags                 : 
    VirtualMachine       : {
                             "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/DNS01"
                           }
    IpConfigurations     : [
                             {
                               "Name": "ipconfig1",
                               "Etag": "W/\"[Id]\"",
                               "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC/ipConfigurations/ipconfig1",
                               "PrivateIpAddress": "192.168.1.101",
                               "PrivateIpAllocationMethod": "Static",
                               "Subnet": {
                                 "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd"
                               },
                               "PublicIpAddress": {
                                 "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/TestPIP"
                               },
                               "LoadBalancerBackendAddressPools": [],
                               "LoadBalancerInboundNatRules": [],
                               "ProvisioningState": "Succeeded"
                             }
                           ]
    DnsSettings          : {
                             "DnsServers": [],
                             "AppliedDnsServers": [],
                             "InternalDnsNameLabel": null,
                             "InternalFqdn": null
                           }
    EnableIPForwarding   : False
    NetworkSecurityGroup : null
    Primary              : True

## <a name="remove-a-static-private-ip-address-from-a-network-interface"></a><span data-ttu-id="755e9-126">Remover um endereço IP privado estático de uma interface de rede</span><span class="sxs-lookup"><span data-stu-id="755e9-126">Remove a static private IP address from a network interface</span></span>
<span data-ttu-id="755e9-127">tooremove Olá endereço IP privado estático adicionados toohello VM script hello acima, Olá executar comandos do PowerShell a seguir:</span><span class="sxs-lookup"><span data-stu-id="755e9-127">tooremove hello static private IP address added toohello VM in hello script above, run hello following PowerShell commands:</span></span>

```powershell
$nic=Get-AzureRmNetworkInterface -Name TestNIC -ResourceGroupName TestRG
$nic.IpConfigurations[0].PrivateIpAllocationMethod = "Dynamic"
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

<span data-ttu-id="755e9-128">Saída esperada:</span><span class="sxs-lookup"><span data-stu-id="755e9-128">Expected output:</span></span>

    Name                 : TestNIC
    ResourceGroupName    : TestRG
    Location             : centralus
    Id                   : /subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC
    Etag                 : W/"[Id]"
    ProvisioningState    : Succeeded
    Tags                 : 
    VirtualMachine       : {
                             "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/WindowsVM"
                           }
    IpConfigurations     : [
                             {
                               "Name": "ipconfig1",
                               "Etag": "W/\"[Id]\"",
                               "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC/ipConfigurations/ipconfig1",
                               "PrivateIpAddress": "192.168.1.101",
                               "PrivateIpAllocationMethod": "Dynamic",
                               "Subnet": {
                                 "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd"
                               },
                               "PublicIpAddress": {
                                 "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/TestPIP"
                               },
                               "LoadBalancerBackendAddressPools": [],
                               "LoadBalancerInboundNatRules": [],
                               "ProvisioningState": "Succeeded"
                             }
                           ]
    DnsSettings          : {
                             "DnsServers": [],
                             "AppliedDnsServers": [],
                             "InternalDnsNameLabel": null,
                             "InternalFqdn": null
                           }
    EnableIPForwarding   : False
    NetworkSecurityGroup : null
    Primary              : True

## <a name="add-a-static-private-ip-address-tooa-network-interface"></a><span data-ttu-id="755e9-129">Adicione uma estático privado IP endereço tooa interface de rede</span><span class="sxs-lookup"><span data-stu-id="755e9-129">Add a static private IP address tooa network interface</span></span>
<span data-ttu-id="755e9-130">tooadd um toohello de endereço IP de privado estático VM criada usando o script de saudação acima, execute Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="755e9-130">tooadd a static private IP address toohello VM created using hello script above, run hello following commands:</span></span>

```powershell
$nic=Get-AzureRmNetworkInterface -Name TestNIC -ResourceGroupName TestRG
$nic.IpConfigurations[0].PrivateIpAllocationMethod = "Static"
$nic.IpConfigurations[0].PrivateIpAddress = "192.168.1.101"
Set-AzureRmNetworkInterface -NetworkInterface $nic
```
## <a name="change-hello-allocation-method-for-a-private-ip-address-assigned-tooa-network-interface"></a><span data-ttu-id="755e9-131">Alterar o método de alocação de saudação de um endereço IP privado atribuído tooa interface de rede</span><span class="sxs-lookup"><span data-stu-id="755e9-131">Change hello allocation method for a private IP address assigned tooa network interface</span></span>

<span data-ttu-id="755e9-132">Um endereço IP privado é atribuído tooa NIC com o método de alocação estática ou dinâmica hello.</span><span class="sxs-lookup"><span data-stu-id="755e9-132">A private IP address is assigned tooa NIC with hello static or dynamic allocation method.</span></span> <span data-ttu-id="755e9-133">Endereços IP dinâmicos podem alterar depois de iniciar uma VM que foi anteriormente no hello interrompido (desalocado) estado.</span><span class="sxs-lookup"><span data-stu-id="755e9-133">Dynamic IP addresses can change after starting a VM that was previously in hello stopped (deallocated) state.</span></span> <span data-ttu-id="755e9-134">Isso pode potencialmente causar problemas se Olá VM está hospedando um serviço que requer Olá mesmo endereço IP, mesmo após a reinicialização de um estado parado (desalocado).</span><span class="sxs-lookup"><span data-stu-id="755e9-134">This can potentially cause issues if hello VM is hosting a service that requires hello same IP address, even after restarts from a stopped (deallocated) state.</span></span> <span data-ttu-id="755e9-135">Endereços IP estáticos são mantidos até que Olá VM seja excluída.</span><span class="sxs-lookup"><span data-stu-id="755e9-135">Static IP addresses are retained until hello VM is deleted.</span></span> <span data-ttu-id="755e9-136">método de alocação toochange hello de um endereço IP, execute Olá script, que altera o método de alocação de saudação do toostatic dinâmico a seguir.</span><span class="sxs-lookup"><span data-stu-id="755e9-136">toochange hello allocation method of an IP address, run hello following script, which changes hello allocation method from dynamic toostatic.</span></span> <span data-ttu-id="755e9-137">Se o método de alocação de saudação de saudação atual de endereço IP é estático, alterar *estático* muito*dinâmico* antes de executar o script hello.</span><span class="sxs-lookup"><span data-stu-id="755e9-137">If hello allocation method for hello current private IP address is static, change *Static* too*Dynamic* before executing hello script.</span></span>

```powershell
$RG = "TestRG"
$NIC_name = "testnic1"

$nic = Get-AzureRmNetworkInterface -ResourceGroupName $RG -Name $NIC_name
$nic.IpConfigurations[0].PrivateIpAllocationMethod = 'Static'
Set-AzureRmNetworkInterface -NetworkInterface $nic 
$IP = $nic.IpConfigurations[0].PrivateIpAddress

Write-Host "hello allocation method is now set to"$nic.IpConfigurations[0].PrivateIpAllocationMethod"for hello IP address" $IP"." -NoNewline
```

<span data-ttu-id="755e9-138">Se você não souber o nome de saudação do hello NIC, você pode exibir uma lista de NICs dentro de um grupo de recursos inserindo Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="755e9-138">If you don't know hello name of hello NIC, you can view a list of NICs within a resource group by entering hello following command:</span></span>

```powershell
Get-AzureRmNetworkInterface -ResourceGroupName $RG | Where-Object {$_.ProvisioningState -eq 'Succeeded'} 
```

## <a name="next-steps"></a><span data-ttu-id="755e9-139">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="755e9-139">Next steps</span></span>
* <span data-ttu-id="755e9-140">Saiba mais sobre endereços [IP públicos reservados](virtual-networks-reserved-public-ip.md) .</span><span class="sxs-lookup"><span data-stu-id="755e9-140">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="755e9-141">Saiba mais sobre endereços [ILPIP (IP público em nível de instância)](virtual-networks-instance-level-public-ip.md) .</span><span class="sxs-lookup"><span data-stu-id="755e9-141">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="755e9-142">Consulte Olá [APIs de REST de IP reservado](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span><span class="sxs-lookup"><span data-stu-id="755e9-142">Consult hello [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>

