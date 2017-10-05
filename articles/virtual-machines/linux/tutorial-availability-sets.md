---
title: Tutorial dos conjuntos de disponibilidade para as VMs do Linux no Azure | Microsoft Docs
description: Saiba mais sobre os Conjuntos de disponibilidade para as VMs do Linux no Azure.
documentationcenter: 
services: virtual-machines-linux
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 63fe3f165864f06228604cac56d06cc061ab25f5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-availability-sets"></a><span data-ttu-id="0dd34-103">Como usar os conjuntos de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="0dd34-103">How to use availability sets</span></span>


<span data-ttu-id="0dd34-104">Neste tutorial, você aprenderá a aumentar a disponibilidade e a confiabilidade de suas soluções de Máquina Virtual no Azure usando uma capacidade chamada Conjuntos de Disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="0dd34-104">In this tutorial, you will learn how to increase the availability and reliability of your Virtual Machine solutions on Azure using a capability called Availability Sets.</span></span> <span data-ttu-id="0dd34-105">Os Conjuntos de disponibilidade garantem que as VMs implantadas no Azure sejam distribuídas entre vários clusters de hardware isolados.</span><span class="sxs-lookup"><span data-stu-id="0dd34-105">Availability sets ensure that the VMs you deploy on Azure are distributed across multiple isolated hardware clusters.</span></span> <span data-ttu-id="0dd34-106">Isso garante que, se ocorrer uma falha de hardware ou de software no Azure, apenas um subconjunto de suas VMs será afetado e a solução geral permanecerá disponível e operacional para seus clientes.</span><span class="sxs-lookup"><span data-stu-id="0dd34-106">Doing this ensures that if a hardware or software failure within Azure happens, only a sub-set of your VMs will be impacted and that your overall solution will remain available and operational from the perspective of your customers using it.</span></span>

<span data-ttu-id="0dd34-107">Neste tutorial, você aprenderá como:</span><span class="sxs-lookup"><span data-stu-id="0dd34-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="0dd34-108">Criar um conjunto de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="0dd34-108">Create an availability set</span></span>
> * <span data-ttu-id="0dd34-109">Criar uma VM em um conjunto de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="0dd34-109">Create a VM in an availability set</span></span>
> * <span data-ttu-id="0dd34-110">Verificar os tamanhos de VM disponíveis</span><span class="sxs-lookup"><span data-stu-id="0dd34-110">Check available VM sizes</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="0dd34-111">Se você optar por instalar e usar a CLI localmente, este tutorial exigirá que você execute a CLI do Azure versão 2.0.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="0dd34-111">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="0dd34-112">Execute `az --version` para encontrar a versão.</span><span class="sxs-lookup"><span data-stu-id="0dd34-112">Run `az --version` to find the version.</span></span> <span data-ttu-id="0dd34-113">Se você precisa instalar ou atualizar, consulte [Instalar a CLI 2.0 do Azure]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="0dd34-113">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="availability-set-overview"></a><span data-ttu-id="0dd34-114">Visão geral do conjunto de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="0dd34-114">Availability set overview</span></span>

<span data-ttu-id="0dd34-115">Um Conjunto de disponibilidade é uma funcionalidade de agrupamento lógico que você pode usar no Azure para garantir que os recursos da VM colocados nele sejam isolados uns dos outros quando forem implantados em um datacenter do Azure.</span><span class="sxs-lookup"><span data-stu-id="0dd34-115">An Availability Set is a logical grouping capability that you can use in Azure to ensure that the VM resources you place within it are isolated from each other when they are deployed within an Azure datacenter.</span></span> <span data-ttu-id="0dd34-116">O Azure garante que as VMs colocadas em um Conjunto de disponibilidade sejam executadas em vários servidores físicos, racks de computação, unidades de armazenamento e comutadores de rede.</span><span class="sxs-lookup"><span data-stu-id="0dd34-116">Azure ensures that the VMs you place within an Availability Set run across multiple physical servers, compute racks, storage units, and network switches.</span></span> <span data-ttu-id="0dd34-117">Isso garante que no caso de falha de hardware ou software do Azure, apenas um subconjunto de suas VMs será afetado e seu aplicativo geral permanecerá disponível e ativo para seus clientes.</span><span class="sxs-lookup"><span data-stu-id="0dd34-117">This ensures that in the event of a hardware or Azure software failure, only a subset of your VMs will be impacted, and your overall application will stay up and continue to be available to your customers.</span></span> <span data-ttu-id="0dd34-118">Os conjuntos de disponibilidade são uma funcionalidade essencial quando você quer compilar soluções de nuvem confiáveis.</span><span class="sxs-lookup"><span data-stu-id="0dd34-118">Using Availability Sets is an essential capability to leverage when you want to build reliable cloud solutions.</span></span>

<span data-ttu-id="0dd34-119">Vamos considerar uma solução comum baseada em VM na qual você pode ter quatro servidores Web front-end e usar duas VMs de back-end que hospedam um banco de dados.</span><span class="sxs-lookup"><span data-stu-id="0dd34-119">Let’s consider a typical VM-based solution where you might have 4 front-end web servers and use 2 back-end VMs that host a database.</span></span> <span data-ttu-id="0dd34-120">Com o Azure, convém definir dois conjuntos de disponibilidade antes de implantar suas VMs: um conjunto de disponibilidade para a camada "Web" e um conjunto de disponibilidade para a camada "banco de dados".</span><span class="sxs-lookup"><span data-stu-id="0dd34-120">With Azure, you’d want to define two availability sets before you deploy your VMs: one availability set for the “web” tier and one availability set for the “database” tier.</span></span> <span data-ttu-id="0dd34-121">Ao criar uma nova VM, você pode especificar o conjunto de disponibilidade como um parâmetro para o comando az vm create e o Azure garantirá automaticamente que as VMs criadas dentro do conjunto de disponibilidade sejam isoladas em vários recursos de hardware físico.</span><span class="sxs-lookup"><span data-stu-id="0dd34-121">When you create a new VM you can then specify the availability set as a parameter to the az vm create command, and Azure will automatically ensure that the VMs you create within the available set are isolated across multiple physical hardware resources.</span></span> <span data-ttu-id="0dd34-122">Isso significa que, se o hardware físico no qual um de seus servidores Web ou VMs do servidor de banco de dados estiverem em execução enfrentar um problema, você saberá que outras instâncias de seu servidor Web e VMs de banco de dados permanecerão em execução, pois estão em um hardware diferente.</span><span class="sxs-lookup"><span data-stu-id="0dd34-122">This means that if the physical hardware that one of your Web Server or Database Server VMs is running on has a problem, you know that the other instances of your Web Server and Database VMs will remain running fine because they are on different hardware.</span></span>

<span data-ttu-id="0dd34-123">Sempre use Conjuntos de disponibilidade quando quiser implantar soluções confiáveis baseadas em VM no Azure.</span><span class="sxs-lookup"><span data-stu-id="0dd34-123">You should always use Availability Sets when you want to deploy reliable VM-based solutions within Azure.</span></span>


## <a name="create-an-availability-set"></a><span data-ttu-id="0dd34-124">Criar um conjunto de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="0dd34-124">Create an availability set</span></span>

<span data-ttu-id="0dd34-125">Crie um conjunto de disponibilidade usando [az vm availability-set create](/cli/azure/vm/availability-set#create).</span><span class="sxs-lookup"><span data-stu-id="0dd34-125">You can create an availability set using [az vm availability-set create](/cli/azure/vm/availability-set#create).</span></span> <span data-ttu-id="0dd34-126">Nesse exemplo, definimos o número de domínios de atualização e de falha como *2* para o conjunto de disponibilidade chamado *myAvailabilitySet* no grupo de recursos *myResourceGroupAvailability*.</span><span class="sxs-lookup"><span data-stu-id="0dd34-126">In this example, we set both the number of update and fault domains at *2* for the availability set named *myAvailabilitySet* in the *myResourceGroupAvailability* resource group.</span></span>

<span data-ttu-id="0dd34-127">Crie um grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="0dd34-127">Create a resource group.</span></span>

```azurecli-interactive 
az group create --name myResourceGroupAvailability --location eastus
```


```azurecli-interactive 
az vm availability-set create \
    --resource-group myResourceGroupAvailability \
    --name myAvailabilitySet \
    --platform-fault-domain-count 2 \
    --platform-update-domain-count 2
```

<span data-ttu-id="0dd34-128">Os Conjuntos de disponibilidade permitem que você isole os recursos em "domínios de falha" e "domínios de atualização".</span><span class="sxs-lookup"><span data-stu-id="0dd34-128">Availability Sets allow you to isolate resources across "fault domains" and "update domains".</span></span> <span data-ttu-id="0dd34-129">Um **domínio de falha** representa uma coleção isolada de recursos de servidor + rede + armazenamento.</span><span class="sxs-lookup"><span data-stu-id="0dd34-129">A **fault domain** represents an isolated collection of server + network + storage resources.</span></span> <span data-ttu-id="0dd34-130">No exemplo anterior, indicamos que queremos a distribuição de nosso conjunto de disponibilidade em pelo menos dois domínios de falha quando nossas VMs são implantadas.</span><span class="sxs-lookup"><span data-stu-id="0dd34-130">In the preceding example, we indicate that we want our availability set to be distributed across at least two fault domains when our VMs are deployed.</span></span> <span data-ttu-id="0dd34-131">Também podemos indicar que desejamos distribuir nosso conjunto de disponibilidade entre dois **domínios de atualização**.</span><span class="sxs-lookup"><span data-stu-id="0dd34-131">We also indicate that we want our availability set distributed across two **update domains**.</span></span>  <span data-ttu-id="0dd34-132">Dois domínios de atualização garantem que durante a atualização de software do Azure nossos recursos de VM estarão isolados, impedindo que todos os softwares em execução em nossa VM sejam atualizados ao mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="0dd34-132">Two update domains ensure that when Azure performs software updates our VM resources are isolated, preventing all the software running underneath our VM from being updated at the same time.</span></span>

## <a name="configure-virtual-network"></a><span data-ttu-id="0dd34-133">Configurar rede virtual</span><span class="sxs-lookup"><span data-stu-id="0dd34-133">Configure virtual network</span></span>
<span data-ttu-id="0dd34-134">Antes de implantar algumas VMs e poder testar o balanceador, crie os recursos de suporte de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="0dd34-134">Before you deploy some VMs and can test your balancer, create the supporting virtual network resources.</span></span> <span data-ttu-id="0dd34-135">Para saber mais sobre redes virtuais, veja o tutorial [Gerenciar Redes Virtuais do Azure](tutorial-virtual-network.md).</span><span class="sxs-lookup"><span data-stu-id="0dd34-135">For more information about virtual networks, see the [Manage Azure Virtual Networks](tutorial-virtual-network.md) tutorial.</span></span>

### <a name="create-network-resources"></a><span data-ttu-id="0dd34-136">Criar recursos da rede</span><span class="sxs-lookup"><span data-stu-id="0dd34-136">Create network resources</span></span>
<span data-ttu-id="0dd34-137">Crie a rede virtual com [az network vnet create](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="0dd34-137">Create a virtual network with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="0dd34-138">O exemplo a seguir cria uma rede virtual chamada *myVnet* com uma sub-rede chamada *mySubnet*:</span><span class="sxs-lookup"><span data-stu-id="0dd34-138">The following example creates a virtual network named *myVnet* with a subnet named *mySubnet*:</span></span>

```azurecli-interactive 
az network vnet create \
    --resource-group myResourceGroupAvailability \
    --name myVnet \
    --subnet-name mySubnet
```
<span data-ttu-id="0dd34-139">NICs virtuais são criadas com [az network nic create](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="0dd34-139">Virtual NICs are created with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="0dd34-140">O exemplo a seguir cria três NICs virtuais.</span><span class="sxs-lookup"><span data-stu-id="0dd34-140">The following example creates three virtual NICs.</span></span> <span data-ttu-id="0dd34-141">(Uma NIC virtual para cada VM criada para seu aplicativo nas etapas a seguir).</span><span class="sxs-lookup"><span data-stu-id="0dd34-141">(One virtual NIC for each VM you create for your app in the following steps).</span></span> <span data-ttu-id="0dd34-142">Você pode criar VMs e NICs virtuais adicionais a qualquer momento e adicioná-las ao balanceador de carga:</span><span class="sxs-lookup"><span data-stu-id="0dd34-142">You can create additional virtual NICs and VMs at any time and add them to the load balancer:</span></span>

```bash
for i in `seq 1 3`; do
    az network nic create \
        --resource-group myResourceGroupAvailability \
        --name myNic$i \
        --vnet-name myVnet \
        --subnet mySubnet \
        --lb-name myLoadBalancer \
        --lb-address-pools myBackEndPool
done
```

## <a name="create-vms-inside-an-availability-set"></a><span data-ttu-id="0dd34-143">Criar VMs dentro de um conjunto de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="0dd34-143">Create VMs inside an availability set</span></span>

<span data-ttu-id="0dd34-144">As VMs devem ser criadas dentro do conjunto de disponibilidade para assegurar a distribuição correta pelo hardware.</span><span class="sxs-lookup"><span data-stu-id="0dd34-144">VMs must be created within the availability set to make sure they are correctly distributed across the hardware.</span></span> <span data-ttu-id="0dd34-145">Você não pode adicionar uma VM existente a um conjunto de disponibilidade após sua criação.</span><span class="sxs-lookup"><span data-stu-id="0dd34-145">You can't add an existing VM to an availability set after it is created.</span></span> 

<span data-ttu-id="0dd34-146">Ao criar uma VM usando [az vm create](/cli/azure/vm#create), você especifica a conjunto de disponibilidade usando o parâmetro `--availability-set` para especificar o nome do conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="0dd34-146">When you create a VM using [az vm create](/cli/azure/vm#create) you specify the availability set using the `--availability-set` parameter to specify the name of the availability set.</span></span>

```azurecli-interactive 
for i in `seq 1 2`; do
   az vm create \
     --resource-group myResourceGroupAvailability \
     --name myVM$i \
     --availability-set myAvailabilitySet \
     --nics myNic$i \
     --size Standard_DS1_v2  \
     --image Canonical:UbuntuServer:14.04.4-LTS:latest \
     --admin-username azureuser \
     --generate-ssh-keys \
     --no-wait
done 
```

<span data-ttu-id="0dd34-147">Agora temos duas máquinas virtuais em nosso conjunto de disponibilidade recém-criado.</span><span class="sxs-lookup"><span data-stu-id="0dd34-147">We now have two virtual machines within our newly created availability set.</span></span> <span data-ttu-id="0dd34-148">Como elas estão no mesmo conjunto de disponibilidade, o Azure garantirá que as VMs e todos os seus recursos (incluindo discos de dados) sejam distribuídos entre o hardware físico isolado.</span><span class="sxs-lookup"><span data-stu-id="0dd34-148">Because they are in the same availability set, Azure will ensure that the VMs and all their resources (including data disks) are distributed across isolated physical hardware.</span></span> <span data-ttu-id="0dd34-149">Essa distribuição ajuda a garantir uma disponibilidade muito maior de nossa solução de VM geral.</span><span class="sxs-lookup"><span data-stu-id="0dd34-149">This distribution helps ensure much higher availability of our overall VM solution.</span></span>

<span data-ttu-id="0dd34-150">Algo que você pode enfrentar ao adicionar VMs é que um determinado tamanho de VM não pode mais ser usado em seu conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="0dd34-150">One thing you may encounter as you add VMs is that a particular VM size is no longer available to use within your availability set.</span></span> <span data-ttu-id="0dd34-151">Esse problema pode ocorrer se não houver capacidade suficiente para adicionar essa VM e preservar ao mesmo tempo as regras de isolamento aplicadas pelo conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="0dd34-151">This issue can happen if there is no longer enough capacity to add it while preserving the isolation rules the availability set enforces.</span></span> <span data-ttu-id="0dd34-152">Verifique quais tamanhos de VM estão disponíveis para uso dentro de um conjunto de disponibilidade existente usando o parâmetro `--availability-set list-sizes`.</span><span class="sxs-lookup"><span data-stu-id="0dd34-152">You can check to see what VM sizes are available to use within an existing availability set using the `--availability-set list-sizes` parameter.</span></span>

## <a name="check-for-available-vm-sizes"></a><span data-ttu-id="0dd34-153">Conferir os tamanhos de VM disponíveis</span><span class="sxs-lookup"><span data-stu-id="0dd34-153">Check for available VM sizes</span></span> 

<span data-ttu-id="0dd34-154">Você pode adicionar posteriormente outras VMs ao conjunto de disponibilidade, mas você precisa saber quais tamanhos de VM estão disponíveis no hardware.</span><span class="sxs-lookup"><span data-stu-id="0dd34-154">You can add more VMs to the availability set later, but you need to know what VM sizes are available on the hardware.</span></span> <span data-ttu-id="0dd34-155">Use [az vm availability-set list-sizes](/cli/azure/availability-set#list-sizes) para listar todos os tamanhos disponíveis no cluster de hardware para o conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="0dd34-155">Use [az vm availability-set list-sizes](/cli/azure/availability-set#list-sizes) to list all the available sizes on the hardware cluster for the availability set.</span></span>

```azurecli-interactive 
az vm availability-set list-sizes \
     --resource-group myResourceGroupAvailability \
     --name myAvailabilitySet \
     --output table  
```

## <a name="next-steps"></a><span data-ttu-id="0dd34-156">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0dd34-156">Next steps</span></span>

<span data-ttu-id="0dd34-157">Neste tutorial, você aprendeu como:</span><span class="sxs-lookup"><span data-stu-id="0dd34-157">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="0dd34-158">Criar um conjunto de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="0dd34-158">Create an availability set</span></span>
> * <span data-ttu-id="0dd34-159">Criar uma VM em um conjunto de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="0dd34-159">Create a VM in an availability set</span></span>
> * <span data-ttu-id="0dd34-160">Verificar os tamanhos de VM disponíveis</span><span class="sxs-lookup"><span data-stu-id="0dd34-160">Check available VM sizes</span></span>

<span data-ttu-id="0dd34-161">Avance para o próximo tutorial para saber mais sobre conjuntos de disponibilidade de máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="0dd34-161">Advance to the next tutorial to learn about virtual machine scale sets.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="0dd34-162">Criar um conjunto de dimensionamento da VM</span><span class="sxs-lookup"><span data-stu-id="0dd34-162">Create a VM scale set</span></span>](tutorial-create-vmss.md)

