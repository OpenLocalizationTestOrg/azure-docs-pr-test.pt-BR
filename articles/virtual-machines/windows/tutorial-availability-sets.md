---
title: Tutorial dos conjuntos de disponibilidade para as VMs do Windows no Azure | Microsoft Docs
description: Saiba mais sobre os Conjuntos de disponibilidade para as VMs do Windows no Azure.
documentationcenter: 
services: virtual-machines-windows
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: d918362106ef93cf47620e0018d363cd510884b0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-availability-sets"></a><span data-ttu-id="c04d2-103">Como usar os conjuntos de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="c04d2-103">How to use availability sets</span></span>

<span data-ttu-id="c04d2-104">Neste tutorial, você aprenderá a aumentar a disponibilidade e a confiabilidade de suas soluções de Máquina Virtual no Azure usando uma capacidade chamada Conjuntos de Disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="c04d2-104">In this tutorial, you will learn how to increase the availability and reliability of your Virtual Machine solutions on Azure using a capability called Availability Sets.</span></span> <span data-ttu-id="c04d2-105">Os Conjuntos de disponibilidade garantem que as VMs implantadas no Azure sejam distribuídas entre vários clusters de hardware isolados.</span><span class="sxs-lookup"><span data-stu-id="c04d2-105">Availability sets ensure that the VMs you deploy on Azure are distributed across multiple isolated hardware clusters.</span></span> <span data-ttu-id="c04d2-106">Isso garante que, se ocorrer uma falha de hardware ou de software no Azure, apenas um subconjunto de suas VMs será afetado e a solução geral permanecerá disponível e operacional para seus clientes.</span><span class="sxs-lookup"><span data-stu-id="c04d2-106">Doing this ensures that if a hardware or software failure within Azure happens, only a sub-set of your VMs will be impacted and that your overall solution will remain available and operational from the perspective of your customers using it.</span></span> 

<span data-ttu-id="c04d2-107">Neste tutorial, você aprenderá como:</span><span class="sxs-lookup"><span data-stu-id="c04d2-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c04d2-108">Criar um conjunto de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="c04d2-108">Create an availability set</span></span>
> * <span data-ttu-id="c04d2-109">Criar uma VM em um conjunto de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="c04d2-109">Create a VM in an availability set</span></span>
> * <span data-ttu-id="c04d2-110">Verificar os tamanhos de VM disponíveis</span><span class="sxs-lookup"><span data-stu-id="c04d2-110">Check available VM sizes</span></span>

<span data-ttu-id="c04d2-111">Este tutorial requer o módulo do Azure PowerShell, versão 3.6 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="c04d2-111">This tutorial requires the Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="c04d2-112">Execute ` Get-Module -ListAvailable AzureRM` para encontrar a versão.</span><span class="sxs-lookup"><span data-stu-id="c04d2-112">Run ` Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="c04d2-113">Se você precisa atualizar, consulte [Instalar o módulo do Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="c04d2-113">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="availability-set-overview"></a><span data-ttu-id="c04d2-114">Visão geral do conjunto de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="c04d2-114">Availability set overview</span></span>

<span data-ttu-id="c04d2-115">Um Conjunto de disponibilidade é uma funcionalidade de agrupamento lógico que você pode usar no Azure para garantir que os recursos da VM colocados nele sejam isolados uns dos outros quando forem implantados em um datacenter do Azure.</span><span class="sxs-lookup"><span data-stu-id="c04d2-115">An Availability Set is a logical grouping capability that you can use in Azure to ensure that the VM resources you place within it are isolated from each other when they are deployed within an Azure datacenter.</span></span> <span data-ttu-id="c04d2-116">O Azure garante que as VMs colocadas em um Conjunto de disponibilidade sejam executadas em vários servidores físicos, racks de computação, unidades de armazenamento e comutadores de rede.</span><span class="sxs-lookup"><span data-stu-id="c04d2-116">Azure ensures that the VMs you place within an Availability Set run across multiple physical servers, compute racks, storage units, and network switches.</span></span> <span data-ttu-id="c04d2-117">Isso garante que no caso de falha de hardware ou software do Azure, apenas um subconjunto de suas VMs será afetado e seu aplicativo geral permanecerá disponível e ativo para seus clientes.</span><span class="sxs-lookup"><span data-stu-id="c04d2-117">This ensures that in the event of a hardware or Azure software failure, only a subset of your VMs will be impacted, and your overall application will stay up and continue to be available to your customers.</span></span> <span data-ttu-id="c04d2-118">Os conjuntos de disponibilidade são uma funcionalidade essencial quando você quer compilar soluções de nuvem confiáveis.</span><span class="sxs-lookup"><span data-stu-id="c04d2-118">Using Availability Sets is an essential capability to leverage when you want to build reliable cloud solutions.</span></span>

<span data-ttu-id="c04d2-119">Vamos considerar uma solução comum baseada em VM na qual você pode ter quatro servidores Web front-end e usar duas VMs de back-end que hospedam um banco de dados.</span><span class="sxs-lookup"><span data-stu-id="c04d2-119">Let’s consider a typical VM-based solution where you might have 4 front-end web servers and use 2 back-end VMs that host a database.</span></span> <span data-ttu-id="c04d2-120">Com o Azure, convém definir dois conjuntos de disponibilidade antes de implantar suas VMs: um conjunto de disponibilidade para a camada "Web" e um conjunto de disponibilidade para a camada "banco de dados".</span><span class="sxs-lookup"><span data-stu-id="c04d2-120">With Azure, you’d want to define two availability sets before you deploy your VMs: one availability set for the “web” tier and one availability set for the “database” tier.</span></span> <span data-ttu-id="c04d2-121">Ao criar uma nova VM, você pode especificar o conjunto de disponibilidade como um parâmetro para o comando az vm create e o Azure garantirá automaticamente que as VMs criadas dentro do conjunto de disponibilidade sejam isoladas em vários recursos de hardware físico.</span><span class="sxs-lookup"><span data-stu-id="c04d2-121">When you create a new VM you can then specify the availability set as a parameter to the az vm create command, and Azure will automatically ensure that the VMs you create within the available set are isolated across multiple physical hardware resources.</span></span> <span data-ttu-id="c04d2-122">Isso significa que, se o hardware físico no qual um de seus servidores Web ou VMs do servidor de banco de dados estiverem em execução enfrentar um problema, você saberá que outras instâncias de seu servidor Web e VMs de banco de dados permanecerão em execução, pois estão em um hardware diferente.</span><span class="sxs-lookup"><span data-stu-id="c04d2-122">This means that if the physical hardware that one of your Web Server or Database Server VMs is running on has a problem, you know that the other instances of your Web Server and Database VMs will remain running fine because they are on different hardware.</span></span>

<span data-ttu-id="c04d2-123">Sempre use Conjuntos de disponibilidade quando quiser implantar soluções confiáveis baseadas em VM no Azure.</span><span class="sxs-lookup"><span data-stu-id="c04d2-123">You should always use Availability Sets when you want to deploy reliable VM based solutions within Azure.</span></span>

## <a name="create-an-availability-set"></a><span data-ttu-id="c04d2-124">Criar um conjunto de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="c04d2-124">Create an availability set</span></span>

<span data-ttu-id="c04d2-125">Você pode criar um conjunto de disponibilidade usando [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span><span class="sxs-lookup"><span data-stu-id="c04d2-125">You can create an availability set using [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span></span> <span data-ttu-id="c04d2-126">Nesse exemplo, definimos o número de domínios de atualização e de falha como *2* para o conjunto de disponibilidade chamado *myAvailabilitySet* no grupo de recursos *myResourceGroupAvailability*.</span><span class="sxs-lookup"><span data-stu-id="c04d2-126">In this example, we set both the number of update and fault domains at *2* for the availability set named *myAvailabilitySet* in the *myResourceGroupAvailability* resource group.</span></span>

<span data-ttu-id="c04d2-127">Crie um grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="c04d2-127">Create a resource group.</span></span>

```powershell
New-AzureRmResourceGroup -Name myResourceGroupAvailability -Location EastUS
```


```powershell
New-AzureRmAvailabilitySet `
   -Location EastUS `
   -Name myAvailabilitySet `
   -ResourceGroupName myResourceGroupAvailability `
   -Managed `
   -PlatformFaultDomainCount 2 `
   -PlatformUpdateDomainCount 2
```

## <a name="create-vms-inside-an-availability-set"></a><span data-ttu-id="c04d2-128">Criar VMs dentro de um conjunto de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="c04d2-128">Create VMs inside an availability set</span></span>

<span data-ttu-id="c04d2-129">As VMs precisam ser criadas dentro do conjunto de disponibilidade para assegurar a distribuição correta pelo hardware.</span><span class="sxs-lookup"><span data-stu-id="c04d2-129">VMs need to be created within the availability set to make sure they are correctly distributed across the hardware.</span></span> <span data-ttu-id="c04d2-130">Você não pode adicionar uma VM existente a um conjunto de disponibilidade após sua criação.</span><span class="sxs-lookup"><span data-stu-id="c04d2-130">You can't add an existing VM to an availability set after it is created.</span></span> 

<span data-ttu-id="c04d2-131">O hardware em um local é dividido em vários domínios de atualização e domínios de falha.</span><span class="sxs-lookup"><span data-stu-id="c04d2-131">The hardware in a location is divided in to multiple update domains and fault domains.</span></span> <span data-ttu-id="c04d2-132">Um **domínios de atualização** é um grupo de VMs e hardware físico subjacente que podem ser reinicializados simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="c04d2-132">An **update domain** is a group of VMs and underlying physical hardware that can be rebooted at the same time.</span></span> <span data-ttu-id="c04d2-133">As VMs no mesmo **domínio de falha** compartilham armazenamentos comuns, bem como um comutador de rede e fonte de energia comuns.</span><span class="sxs-lookup"><span data-stu-id="c04d2-133">VMs in the same **fault domain** share common storage as well as a common power source and network switch.</span></span> 

<span data-ttu-id="c04d2-134">Ao criar uma VM usando [New-AzureRMVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig), você especifica a conjunto de disponibilidade usando o parâmetro `-AvailabilitySetId` para especificar a ID do conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="c04d2-134">When you create a VM using configuration using [New-AzureRMVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) you specify the availability set using the `-AvailabilitySetId` parameter to specify the ID of the availability set.</span></span>

<span data-ttu-id="c04d2-135">Crie duas VMs com [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) no conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="c04d2-135">Create 2 VMs with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) in the availability set.</span></span>

```powershell
$availabilitySet = Get-AzureRmAvailabilitySet `
    -ResourceGroupName myResourceGroupAvailability `
    -Name myAvailabilitySet

$cred = Get-Credential -Message "Enter a username and password for the virtual machine."

$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24
$vnet = New-AzureRmVirtualNetwork `
    -ResourceGroupName myResourceGroupAvailability `
    -Location EastUS `
    -Name MYvNET `
    -AddressPrefix 192.168.0.0/16 `
    -Subnet $subnetConfig

for ($i=1; $i -le 2; $i++)
{
   $pip = New-AzureRmPublicIpAddress `
        -ResourceGroupName myResourceGroupAvailability `
        -Location EastUS `
        -Name "mypublicdns$(Get-Random)" `
        -AllocationMethod Static `
        -IdleTimeoutInMinutes 4

   $nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig `
        -Name myNetworkSecurityGroupRuleRDP$i `
        -Protocol Tcp `
        -Direction Inbound `
        -Priority 1000 `
        -SourceAddressPrefix * `
        -SourcePortRange * `
        -DestinationAddressPrefix * `
        -DestinationPortRange 3389 `
        -Access Allow

   $nsg = New-AzureRmNetworkSecurityGroup `
        -ResourceGroupName myResourceGroupAvailability `
        -Location EastUS `
        -Name myNetworkSecurityGroup$i `
        -SecurityRules $nsgRuleRDP

   $nic = New-AzureRmNetworkInterface `
        -Name myNic$i `
        -ResourceGroupName myResourceGroupAvailability `
        -Location EastUS `
        -SubnetId $vnet.Subnets[0].Id `
        -PublicIpAddressId $pip.Id `
        -NetworkSecurityGroupId $nsg.Id

   # Here is where we specify the availability set
   $vm = New-AzureRmVMConfig `
        -VMName myVM$i `
        -VMSize Standard_D1 `
        -AvailabilitySetId $availabilitySet.Id

   $vm = Set-AzureRmVMOperatingSystem `
        -VM $vm `
        -Windows -ComputerName myVM$i `   
        -Credential $cred `
        -ProvisionVMAgent `
        -EnableAutoUpdate
   $vm = Set-AzureRmVMSourceImage `
        -VM $vm `
        -PublisherName MicrosoftWindowsServer `
        -Offer WindowsServer `
        -Skus 2016-Datacenter `
        -Version latest
   $vm = Set-AzureRmVMOSDisk `
        -VM $vm `
        -Name myOsDisk$i `
        -DiskSizeInGB 128 `
        -CreateOption FromImage `
        -Caching ReadWrite
   $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
   New-AzureRmVM `
        -ResourceGroupName myResourceGroupAvailability `
        -Location EastUS `
        -VM $vm
}

```

<span data-ttu-id="c04d2-136">Demora alguns minutos para criar e configurar ambas as VMs.</span><span class="sxs-lookup"><span data-stu-id="c04d2-136">It takes a few minutes to create and configure both VMs.</span></span> <span data-ttu-id="c04d2-137">Quando tiver terminado, você terá duas máquinas virtuais distribuídas entre o hardware subjacente.</span><span class="sxs-lookup"><span data-stu-id="c04d2-137">When finished, you will have 2 virtual machines distributed across the underlying hardware.</span></span> 

## <a name="check-for-available-vm-sizes"></a><span data-ttu-id="c04d2-138">Conferir os tamanhos de VM disponíveis</span><span class="sxs-lookup"><span data-stu-id="c04d2-138">Check for available VM sizes</span></span> 

<span data-ttu-id="c04d2-139">Você pode adicionar posteriormente outras VMs ao conjunto de disponibilidade, mas você precisa saber quais tamanhos de VM estão disponíveis no hardware.</span><span class="sxs-lookup"><span data-stu-id="c04d2-139">You can add more VMs to the availability set later, but you need to know what VM sizes are available on the hardware.</span></span> <span data-ttu-id="c04d2-140">Use [Get-AzureRMVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) para listar todos os tamanhos disponíveis no cluster de hardware para o conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="c04d2-140">Use [Get-AzureRMVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) to list all the available sizes on the hardware cluster for the availability set.</span></span>

```powershell
Get-AzureRmVMSize `
   -AvailabilitySetName myAvailabilitySet `
   -ResourceGroupName myResourceGroupAvailability  
```

## <a name="next-steps"></a><span data-ttu-id="c04d2-141">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c04d2-141">Next steps</span></span>

<span data-ttu-id="c04d2-142">Neste tutorial, você aprendeu como:</span><span class="sxs-lookup"><span data-stu-id="c04d2-142">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c04d2-143">Criar um conjunto de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="c04d2-143">Create an availability set</span></span>
> * <span data-ttu-id="c04d2-144">Criar uma VM em um conjunto de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="c04d2-144">Create a VM in an availability set</span></span>
> * <span data-ttu-id="c04d2-145">Verificar os tamanhos de VM disponíveis</span><span class="sxs-lookup"><span data-stu-id="c04d2-145">Check available VM sizes</span></span>

<span data-ttu-id="c04d2-146">Avance para o próximo tutorial para saber mais sobre conjuntos de disponibilidade de máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="c04d2-146">Advance to the next tutorial to learn about virtual machine scale sets.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c04d2-147">Criar um conjunto de dimensionamento da VM</span><span class="sxs-lookup"><span data-stu-id="c04d2-147">Create a VM scale set</span></span>](tutorial-create-vmss.md)


