---
title: aaaAvailability define o tutorial para VMs do Windows no Azure | Microsoft Docs
description: "Saiba mais sobre Olá disponibilidade conjuntos para máquinas virtuais do Windows no Azure."
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
ms.openlocfilehash: 853775c5f126dd815c1933f9d71d2274a75ea661
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-availability-sets"></a><span data-ttu-id="07d6e-103">Como os conjuntos de disponibilidade de toouse</span><span class="sxs-lookup"><span data-stu-id="07d6e-103">How toouse availability sets</span></span>

<span data-ttu-id="07d6e-104">Neste tutorial, você aprenderá como a disponibilidade de saudação tooincrease e a confiabilidade de suas soluções de máquina Virtual no Azure usando um recurso chamado conjuntos de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="07d6e-104">In this tutorial, you will learn how tooincrease hello availability and reliability of your Virtual Machine solutions on Azure using a capability called Availability Sets.</span></span> <span data-ttu-id="07d6e-105">Conjuntos de disponibilidade garantem que Olá VMs implantar no Azure são distribuídas entre vários clusters de hardware isoladas.</span><span class="sxs-lookup"><span data-stu-id="07d6e-105">Availability sets ensure that hello VMs you deploy on Azure are distributed across multiple isolated hardware clusters.</span></span> <span data-ttu-id="07d6e-106">Isso garante que, se ocorre uma falha de hardware ou software no Azure, um sub conjunto das suas máquinas virtuais será afetado e que sua solução geral permanecerão disponíveis e operacionais da perspectiva de saudação de seus clientes usá-lo.</span><span class="sxs-lookup"><span data-stu-id="07d6e-106">Doing this ensures that if a hardware or software failure within Azure happens, only a sub-set of your VMs will be impacted and that your overall solution will remain available and operational from hello perspective of your customers using it.</span></span> 

<span data-ttu-id="07d6e-107">Neste tutorial, você aprenderá como:</span><span class="sxs-lookup"><span data-stu-id="07d6e-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="07d6e-108">Criar um conjunto de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="07d6e-108">Create an availability set</span></span>
> * <span data-ttu-id="07d6e-109">Criar uma VM em um conjunto de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="07d6e-109">Create a VM in an availability set</span></span>
> * <span data-ttu-id="07d6e-110">Verificar os tamanhos de VM disponíveis</span><span class="sxs-lookup"><span data-stu-id="07d6e-110">Check available VM sizes</span></span>

<span data-ttu-id="07d6e-111">Este tutorial requer hello Azure PowerShell versão 3.6 ou posterior do módulo.</span><span class="sxs-lookup"><span data-stu-id="07d6e-111">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="07d6e-112">Executar ` Get-Module -ListAvailable AzureRM` toofind versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="07d6e-112">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="07d6e-113">Se você precisar tooupgrade, consulte [instalar o módulo PowerShell Azure](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="07d6e-113">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="availability-set-overview"></a><span data-ttu-id="07d6e-114">Visão geral do conjunto de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="07d6e-114">Availability set overview</span></span>

<span data-ttu-id="07d6e-115">Um conjunto de disponibilidade é um recurso de agrupamento lógico que você pode usar no Azure tooensure que recursos VM Olá que colocar nele são isolados uma da outra quando eles forem implantados em um datacenter do Azure.</span><span class="sxs-lookup"><span data-stu-id="07d6e-115">An Availability Set is a logical grouping capability that you can use in Azure tooensure that hello VM resources you place within it are isolated from each other when they are deployed within an Azure datacenter.</span></span> <span data-ttu-id="07d6e-116">Azure garante que as VMs que você coloca em um conjunto de disponibilidade executado em vários servidores físicos hello, comutadores de rede, unidades de armazenamento e racks de computação.</span><span class="sxs-lookup"><span data-stu-id="07d6e-116">Azure ensures that hello VMs you place within an Availability Set run across multiple physical servers, compute racks, storage units, and network switches.</span></span> <span data-ttu-id="07d6e-117">Isso garante que no caso de saudação de um hardware ou falha de software do Azure, apenas um subconjunto das suas máquinas virtuais será afetado, e geral do seu aplicativo irá continuar e continuar toobe tooyour disponíveis clientes.</span><span class="sxs-lookup"><span data-stu-id="07d6e-117">This ensures that in hello event of a hardware or Azure software failure, only a subset of your VMs will be impacted, and your overall application will stay up and continue toobe available tooyour customers.</span></span> <span data-ttu-id="07d6e-118">Usando conjuntos de disponibilidade é um recurso essencial tooleverage toobuild soluções de nuvem confiável.</span><span class="sxs-lookup"><span data-stu-id="07d6e-118">Using Availability Sets is an essential capability tooleverage when you want toobuild reliable cloud solutions.</span></span>

<span data-ttu-id="07d6e-119">Vamos considerar uma solução comum baseada em VM na qual você pode ter quatro servidores Web front-end e usar duas VMs de back-end que hospedam um banco de dados.</span><span class="sxs-lookup"><span data-stu-id="07d6e-119">Let’s consider a typical VM-based solution where you might have 4 front-end web servers and use 2 back-end VMs that host a database.</span></span> <span data-ttu-id="07d6e-120">Com o Azure, você desejaria toodefine dois conjuntos de disponibilidade antes de implantar suas VMs: conjunto de disponibilidade de um para nível de "web" hello e um conjunto de disponibilidade para camada de "banco de dados" hello.</span><span class="sxs-lookup"><span data-stu-id="07d6e-120">With Azure, you’d want toodefine two availability sets before you deploy your VMs: one availability set for hello “web” tier and one availability set for hello “database” tier.</span></span> <span data-ttu-id="07d6e-121">Quando você cria uma nova VM, em seguida, você pode especificar disponibilidade Olá definida como uma vm do parâmetro toohello az criar comando e Azure automaticamente garantirá que Olá VMs criar dentro Olá disponível conjunto são isolados em vários recursos de hardware físico.</span><span class="sxs-lookup"><span data-stu-id="07d6e-121">When you create a new VM you can then specify hello availability set as a parameter toohello az vm create command, and Azure will automatically ensure that hello VMs you create within hello available set are isolated across multiple physical hardware resources.</span></span> <span data-ttu-id="07d6e-122">Isso significa que, se o hardware físico de saudação que seu servidor Web ou VMs de servidor de banco de dados está em execução no tem um problema, você sabe que Olá outras instâncias do servidor Web e VMs de banco de dados continuará em execução bem porque eles estão em um hardware diferente.</span><span class="sxs-lookup"><span data-stu-id="07d6e-122">This means that if hello physical hardware that one of your Web Server or Database Server VMs is running on has a problem, you know that hello other instances of your Web Server and Database VMs will remain running fine because they are on different hardware.</span></span>

<span data-ttu-id="07d6e-123">Quando você quiser toodeploy soluções confiáveis de VM com base no Azure, você sempre deve usar conjuntos de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="07d6e-123">You should always use Availability Sets when you want toodeploy reliable VM based solutions within Azure.</span></span>

## <a name="create-an-availability-set"></a><span data-ttu-id="07d6e-124">Criar um conjunto de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="07d6e-124">Create an availability set</span></span>

<span data-ttu-id="07d6e-125">Você pode criar um conjunto de disponibilidade usando [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span><span class="sxs-lookup"><span data-stu-id="07d6e-125">You can create an availability set using [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span></span> <span data-ttu-id="07d6e-126">Neste exemplo, vamos definir ambos de número de domínios de atualização e falha no hello *2* para o conjunto nomeada de disponibilidade de saudação *myAvailabilitySet* em Olá *myResourceGroupAvailability*grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="07d6e-126">In this example, we set both hello number of update and fault domains at *2* for hello availability set named *myAvailabilitySet* in hello *myResourceGroupAvailability* resource group.</span></span>

<span data-ttu-id="07d6e-127">Crie um grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="07d6e-127">Create a resource group.</span></span>

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

## <a name="create-vms-inside-an-availability-set"></a><span data-ttu-id="07d6e-128">Criar VMs dentro de um conjunto de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="07d6e-128">Create VMs inside an availability set</span></span>

<span data-ttu-id="07d6e-129">VMs necessário toobe criado no hello-se de que eles sejam distribuídos corretamente em hardware de saudação de toomake de conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="07d6e-129">VMs need toobe created within hello availability set toomake sure they are correctly distributed across hello hardware.</span></span> <span data-ttu-id="07d6e-130">Não é possível adicionar um grupo de disponibilidade de tooan VM definida depois que ela é criada.</span><span class="sxs-lookup"><span data-stu-id="07d6e-130">You can't add an existing VM tooan availability set after it is created.</span></span> 

<span data-ttu-id="07d6e-131">hardware de saudação em um local é dividida em domínios de atualização toomultiple e domínios de falha.</span><span class="sxs-lookup"><span data-stu-id="07d6e-131">hello hardware in a location is divided in toomultiple update domains and fault domains.</span></span> <span data-ttu-id="07d6e-132">Um **domínio de atualização** é um grupo de VMs e o hardware físico subjacente que pode ser reinicializado no hello simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="07d6e-132">An **update domain** is a group of VMs and underlying physical hardware that can be rebooted at hello same time.</span></span> <span data-ttu-id="07d6e-133">Olá de VMs no mesmo **domínio de falha** compartilhar armazenamento comuns, bem como um comutador de origem e de rede de alimentação comum.</span><span class="sxs-lookup"><span data-stu-id="07d6e-133">VMs in hello same **fault domain** share common storage as well as a common power source and network switch.</span></span> 

<span data-ttu-id="07d6e-134">Quando você cria uma VM usando a configuração usando [New-AzureRMVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) especificar Olá conjunto de disponibilidade usando Olá `-AvailabilitySetId` parâmetro toospecify Olá ID do conjunto de disponibilidade de saudação.</span><span class="sxs-lookup"><span data-stu-id="07d6e-134">When you create a VM using configuration using [New-AzureRMVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) you specify hello availability set using hello `-AvailabilitySetId` parameter toospecify hello ID of hello availability set.</span></span>

<span data-ttu-id="07d6e-135">Criar 2 VMs com [AzureRmVM novo](/powershell/module/azurerm.compute/new-azurermvm) no conjunto de disponibilidade de saudação.</span><span class="sxs-lookup"><span data-stu-id="07d6e-135">Create 2 VMs with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) in hello availability set.</span></span>

```powershell
$availabilitySet = Get-AzureRmAvailabilitySet `
    -ResourceGroupName myResourceGroupAvailability `
    -Name myAvailabilitySet

$cred = Get-Credential -Message "Enter a username and password for hello virtual machine."

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

   # Here is where we specify hello availability set
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

<span data-ttu-id="07d6e-136">Ele usa toocreate de alguns minutos e configurar as duas máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="07d6e-136">It takes a few minutes toocreate and configure both VMs.</span></span> <span data-ttu-id="07d6e-137">Quando terminar, você terá 2 máquinas virtuais distribuídas Olá hardware subjacente.</span><span class="sxs-lookup"><span data-stu-id="07d6e-137">When finished, you will have 2 virtual machines distributed across hello underlying hardware.</span></span> 

## <a name="check-for-available-vm-sizes"></a><span data-ttu-id="07d6e-138">Conferir os tamanhos de VM disponíveis</span><span class="sxs-lookup"><span data-stu-id="07d6e-138">Check for available VM sizes</span></span> 

<span data-ttu-id="07d6e-139">Você pode adicionar mais máquinas virtuais toohello conjunto de disponibilidade posteriormente, mas é necessário tooknow quais tamanhos VM estão disponíveis em hardware de saudação.</span><span class="sxs-lookup"><span data-stu-id="07d6e-139">You can add more VMs toohello availability set later, but you need tooknow what VM sizes are available on hello hardware.</span></span> <span data-ttu-id="07d6e-140">Use [Get-AzureRMVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) toolist todos os tamanhos disponíveis de Olá em hardware de saudação do cluster para o conjunto de disponibilidade hello.</span><span class="sxs-lookup"><span data-stu-id="07d6e-140">Use [Get-AzureRMVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) toolist all hello available sizes on hello hardware cluster for hello availability set.</span></span>

```powershell
Get-AzureRmVMSize `
   -AvailabilitySetName myAvailabilitySet `
   -ResourceGroupName myResourceGroupAvailability  
```

## <a name="next-steps"></a><span data-ttu-id="07d6e-141">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="07d6e-141">Next steps</span></span>

<span data-ttu-id="07d6e-142">Neste tutorial, você aprendeu como:</span><span class="sxs-lookup"><span data-stu-id="07d6e-142">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="07d6e-143">Criar um conjunto de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="07d6e-143">Create an availability set</span></span>
> * <span data-ttu-id="07d6e-144">Criar uma VM em um conjunto de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="07d6e-144">Create a VM in an availability set</span></span>
> * <span data-ttu-id="07d6e-145">Verificar os tamanhos de VM disponíveis</span><span class="sxs-lookup"><span data-stu-id="07d6e-145">Check available VM sizes</span></span>

<span data-ttu-id="07d6e-146">Avançar toohello toolearn próximo de tutorial sobre conjuntos de escala de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="07d6e-146">Advance toohello next tutorial toolearn about virtual machine scale sets.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="07d6e-147">Criar um conjunto de dimensionamento da VM</span><span class="sxs-lookup"><span data-stu-id="07d6e-147">Create a VM scale set</span></span>](tutorial-create-vmss.md)


