---
title: aaaAvailability define o tutorial para VMs do Linux no Azure | Microsoft Docs
description: "Saiba mais sobre Olá conjuntos de disponibilidade para VMs do Linux no Azure."
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
ms.openlocfilehash: 2a91e4a6057180035ec51410d9fffccaca343758
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-availability-sets"></a><span data-ttu-id="94a25-103">Como os conjuntos de disponibilidade de toouse</span><span class="sxs-lookup"><span data-stu-id="94a25-103">How toouse availability sets</span></span>


<span data-ttu-id="94a25-104">Neste tutorial, você aprenderá como a disponibilidade de saudação tooincrease e a confiabilidade de suas soluções de máquina Virtual no Azure usando um recurso chamado conjuntos de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="94a25-104">In this tutorial, you will learn how tooincrease hello availability and reliability of your Virtual Machine solutions on Azure using a capability called Availability Sets.</span></span> <span data-ttu-id="94a25-105">Conjuntos de disponibilidade garantem que Olá VMs implantar no Azure são distribuídas entre vários clusters de hardware isoladas.</span><span class="sxs-lookup"><span data-stu-id="94a25-105">Availability sets ensure that hello VMs you deploy on Azure are distributed across multiple isolated hardware clusters.</span></span> <span data-ttu-id="94a25-106">Isso garante que, se ocorre uma falha de hardware ou software no Azure, um sub conjunto das suas máquinas virtuais será afetado e que sua solução geral permanecerão disponíveis e operacionais da perspectiva de saudação de seus clientes usá-lo.</span><span class="sxs-lookup"><span data-stu-id="94a25-106">Doing this ensures that if a hardware or software failure within Azure happens, only a sub-set of your VMs will be impacted and that your overall solution will remain available and operational from hello perspective of your customers using it.</span></span>

<span data-ttu-id="94a25-107">Neste tutorial, você aprenderá como:</span><span class="sxs-lookup"><span data-stu-id="94a25-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="94a25-108">Criar um conjunto de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="94a25-108">Create an availability set</span></span>
> * <span data-ttu-id="94a25-109">Criar uma VM em um conjunto de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="94a25-109">Create a VM in an availability set</span></span>
> * <span data-ttu-id="94a25-110">Verificar os tamanhos de VM disponíveis</span><span class="sxs-lookup"><span data-stu-id="94a25-110">Check available VM sizes</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="94a25-111">Se você escolher tooinstall e usa o hello CLI localmente, este tutorial requer que você está executando a versão de CLI do Azure Olá 2.0.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="94a25-111">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="94a25-112">Executar `az --version` toofind versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="94a25-112">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="94a25-113">Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="94a25-113">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="availability-set-overview"></a><span data-ttu-id="94a25-114">Visão geral do conjunto de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="94a25-114">Availability set overview</span></span>

<span data-ttu-id="94a25-115">Um conjunto de disponibilidade é um recurso de agrupamento lógico que você pode usar no Azure tooensure que recursos VM Olá que colocar nele são isolados uma da outra quando eles forem implantados em um datacenter do Azure.</span><span class="sxs-lookup"><span data-stu-id="94a25-115">An Availability Set is a logical grouping capability that you can use in Azure tooensure that hello VM resources you place within it are isolated from each other when they are deployed within an Azure datacenter.</span></span> <span data-ttu-id="94a25-116">Azure garante que as VMs que você coloca em um conjunto de disponibilidade executado em vários servidores físicos hello, comutadores de rede, unidades de armazenamento e racks de computação.</span><span class="sxs-lookup"><span data-stu-id="94a25-116">Azure ensures that hello VMs you place within an Availability Set run across multiple physical servers, compute racks, storage units, and network switches.</span></span> <span data-ttu-id="94a25-117">Isso garante que no caso de saudação de um hardware ou falha de software do Azure, apenas um subconjunto das suas máquinas virtuais será afetado, e geral do seu aplicativo irá continuar e continuar toobe tooyour disponíveis clientes.</span><span class="sxs-lookup"><span data-stu-id="94a25-117">This ensures that in hello event of a hardware or Azure software failure, only a subset of your VMs will be impacted, and your overall application will stay up and continue toobe available tooyour customers.</span></span> <span data-ttu-id="94a25-118">Usando conjuntos de disponibilidade é um recurso essencial tooleverage toobuild soluções de nuvem confiável.</span><span class="sxs-lookup"><span data-stu-id="94a25-118">Using Availability Sets is an essential capability tooleverage when you want toobuild reliable cloud solutions.</span></span>

<span data-ttu-id="94a25-119">Vamos considerar uma solução comum baseada em VM na qual você pode ter quatro servidores Web front-end e usar duas VMs de back-end que hospedam um banco de dados.</span><span class="sxs-lookup"><span data-stu-id="94a25-119">Let’s consider a typical VM-based solution where you might have 4 front-end web servers and use 2 back-end VMs that host a database.</span></span> <span data-ttu-id="94a25-120">Com o Azure, você desejaria toodefine dois conjuntos de disponibilidade antes de implantar suas VMs: conjunto de disponibilidade de um para nível de "web" hello e um conjunto de disponibilidade para camada de "banco de dados" hello.</span><span class="sxs-lookup"><span data-stu-id="94a25-120">With Azure, you’d want toodefine two availability sets before you deploy your VMs: one availability set for hello “web” tier and one availability set for hello “database” tier.</span></span> <span data-ttu-id="94a25-121">Quando você cria uma nova VM, em seguida, você pode especificar disponibilidade Olá definida como uma vm do parâmetro toohello az criar comando e Azure automaticamente garantirá que Olá VMs criar dentro Olá disponível conjunto são isolados em vários recursos de hardware físico.</span><span class="sxs-lookup"><span data-stu-id="94a25-121">When you create a new VM you can then specify hello availability set as a parameter toohello az vm create command, and Azure will automatically ensure that hello VMs you create within hello available set are isolated across multiple physical hardware resources.</span></span> <span data-ttu-id="94a25-122">Isso significa que, se o hardware físico de saudação que seu servidor Web ou VMs de servidor de banco de dados está em execução no tem um problema, você sabe que Olá outras instâncias do servidor Web e VMs de banco de dados continuará em execução bem porque eles estão em um hardware diferente.</span><span class="sxs-lookup"><span data-stu-id="94a25-122">This means that if hello physical hardware that one of your Web Server or Database Server VMs is running on has a problem, you know that hello other instances of your Web Server and Database VMs will remain running fine because they are on different hardware.</span></span>

<span data-ttu-id="94a25-123">Quando você quiser soluções toodeploy baseado em VM confiáveis no Azure, você sempre deve usar conjuntos de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="94a25-123">You should always use Availability Sets when you want toodeploy reliable VM-based solutions within Azure.</span></span>


## <a name="create-an-availability-set"></a><span data-ttu-id="94a25-124">Criar um conjunto de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="94a25-124">Create an availability set</span></span>

<span data-ttu-id="94a25-125">Crie um conjunto de disponibilidade usando [az vm availability-set create](/cli/azure/vm/availability-set#create).</span><span class="sxs-lookup"><span data-stu-id="94a25-125">You can create an availability set using [az vm availability-set create](/cli/azure/vm/availability-set#create).</span></span> <span data-ttu-id="94a25-126">Neste exemplo, vamos definir ambos de número de domínios de atualização e falha no hello *2* para o conjunto nomeada de disponibilidade de saudação *myAvailabilitySet* em Olá *myResourceGroupAvailability*grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="94a25-126">In this example, we set both hello number of update and fault domains at *2* for hello availability set named *myAvailabilitySet* in hello *myResourceGroupAvailability* resource group.</span></span>

<span data-ttu-id="94a25-127">Crie um grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="94a25-127">Create a resource group.</span></span>

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

<span data-ttu-id="94a25-128">Conjuntos de disponibilidade permite que recursos tooisolate em "domínios de falha" e "domínios de atualização".</span><span class="sxs-lookup"><span data-stu-id="94a25-128">Availability Sets allow you tooisolate resources across "fault domains" and "update domains".</span></span> <span data-ttu-id="94a25-129">Um **domínio de falha** representa uma coleção isolada de recursos de servidor + rede + armazenamento.</span><span class="sxs-lookup"><span data-stu-id="94a25-129">A **fault domain** represents an isolated collection of server + network + storage resources.</span></span> <span data-ttu-id="94a25-130">Olá anterior de exemplo, indicamos que queremos que nossa disponibilidade definida toobe distribuído em pelo menos dois domínios de falha ao nosso VMs são implantadas.</span><span class="sxs-lookup"><span data-stu-id="94a25-130">In hello preceding example, we indicate that we want our availability set toobe distributed across at least two fault domains when our VMs are deployed.</span></span> <span data-ttu-id="94a25-131">Também podemos indicar que desejamos distribuir nosso conjunto de disponibilidade entre dois **domínios de atualização**.</span><span class="sxs-lookup"><span data-stu-id="94a25-131">We also indicate that we want our availability set distributed across two **update domains**.</span></span>  <span data-ttu-id="94a25-132">Certifique-se de dois domínios de atualização que, quando o Azure executa as atualizações de software nossos recursos VM são isolados, impedindo que todos os softwares de saudação em execução sob nosso VM seja atualizado no hello simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="94a25-132">Two update domains ensure that when Azure performs software updates our VM resources are isolated, preventing all hello software running underneath our VM from being updated at hello same time.</span></span>

## <a name="configure-virtual-network"></a><span data-ttu-id="94a25-133">Configurar rede virtual</span><span class="sxs-lookup"><span data-stu-id="94a25-133">Configure virtual network</span></span>
<span data-ttu-id="94a25-134">Antes de implantar algumas máquinas virtuais e testar seu balanceador, crie hello dando suporte a recursos de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="94a25-134">Before you deploy some VMs and can test your balancer, create hello supporting virtual network resources.</span></span> <span data-ttu-id="94a25-135">Para obter mais informações sobre redes virtuais, consulte Olá [gerenciar redes virtuais do Azure](tutorial-virtual-network.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="94a25-135">For more information about virtual networks, see hello [Manage Azure Virtual Networks](tutorial-virtual-network.md) tutorial.</span></span>

### <a name="create-network-resources"></a><span data-ttu-id="94a25-136">Criar recursos da rede</span><span class="sxs-lookup"><span data-stu-id="94a25-136">Create network resources</span></span>
<span data-ttu-id="94a25-137">Crie a rede virtual com [az network vnet create](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="94a25-137">Create a virtual network with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="94a25-138">Olá, exemplo a seguir cria uma rede virtual denominada *myVnet* com uma sub-rede denominada *mySubnet*:</span><span class="sxs-lookup"><span data-stu-id="94a25-138">hello following example creates a virtual network named *myVnet* with a subnet named *mySubnet*:</span></span>

```azurecli-interactive 
az network vnet create \
    --resource-group myResourceGroupAvailability \
    --name myVnet \
    --subnet-name mySubnet
```
<span data-ttu-id="94a25-139">NICs virtuais são criadas com [az network nic create](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="94a25-139">Virtual NICs are created with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="94a25-140">Olá, exemplo a seguir cria três NICs virtuais.</span><span class="sxs-lookup"><span data-stu-id="94a25-140">hello following example creates three virtual NICs.</span></span> <span data-ttu-id="94a25-141">(Uma NIC virtual para cada VM que você criou para seu aplicativo no hello seguindo as etapas.)</span><span class="sxs-lookup"><span data-stu-id="94a25-141">(One virtual NIC for each VM you create for your app in hello following steps).</span></span> <span data-ttu-id="94a25-142">Você pode criar VMs e NICs virtuais adicionais a qualquer momento e adicioná-los toohello balanceador de carga:</span><span class="sxs-lookup"><span data-stu-id="94a25-142">You can create additional virtual NICs and VMs at any time and add them toohello load balancer:</span></span>

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

## <a name="create-vms-inside-an-availability-set"></a><span data-ttu-id="94a25-143">Criar VMs dentro de um conjunto de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="94a25-143">Create VMs inside an availability set</span></span>

<span data-ttu-id="94a25-144">Máquinas virtuais devem ser criados em toomake de conjunto de disponibilidade de saudação-se de que eles sejam distribuídos corretamente em hardware de saudação.</span><span class="sxs-lookup"><span data-stu-id="94a25-144">VMs must be created within hello availability set toomake sure they are correctly distributed across hello hardware.</span></span> <span data-ttu-id="94a25-145">Não é possível adicionar um grupo de disponibilidade de tooan VM definida depois que ela é criada.</span><span class="sxs-lookup"><span data-stu-id="94a25-145">You can't add an existing VM tooan availability set after it is created.</span></span> 

<span data-ttu-id="94a25-146">Quando você cria uma VM usando [criar vm az](/cli/azure/vm#create) especificar Olá conjunto de disponibilidade usando Olá `--availability-set` nome do parâmetro toospecify Olá Olá do conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="94a25-146">When you create a VM using [az vm create](/cli/azure/vm#create) you specify hello availability set using hello `--availability-set` parameter toospecify hello name of hello availability set.</span></span>

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

<span data-ttu-id="94a25-147">Agora temos duas máquinas virtuais em nosso conjunto de disponibilidade recém-criado.</span><span class="sxs-lookup"><span data-stu-id="94a25-147">We now have two virtual machines within our newly created availability set.</span></span> <span data-ttu-id="94a25-148">Olá a porque eles estão no mesmo conjunto de disponibilidade, o Azure garantirá que VMs hello e todos os seus recursos (incluindo os discos de dados) são distribuídos em hardware físico isolado.</span><span class="sxs-lookup"><span data-stu-id="94a25-148">Because they are in hello same availability set, Azure will ensure that hello VMs and all their resources (including data disks) are distributed across isolated physical hardware.</span></span> <span data-ttu-id="94a25-149">Essa distribuição ajuda a garantir uma disponibilidade muito maior de nossa solução de VM geral.</span><span class="sxs-lookup"><span data-stu-id="94a25-149">This distribution helps ensure much higher availability of our overall VM solution.</span></span>

<span data-ttu-id="94a25-150">Uma coisa que você pode encontrar ao adicionar VMs é que um determinado tamanho VM não está mais disponível toouse em seu conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="94a25-150">One thing you may encounter as you add VMs is that a particular VM size is no longer available toouse within your availability set.</span></span> <span data-ttu-id="94a25-151">Esse problema pode ocorrer se não for suficiente tooadd capacidade enquanto preserva o conjunto de disponibilidade de saudação do hello isolamento regras impõe.</span><span class="sxs-lookup"><span data-stu-id="94a25-151">This issue can happen if there is no longer enough capacity tooadd it while preserving hello isolation rules hello availability set enforces.</span></span> <span data-ttu-id="94a25-152">Você pode verificar toosee quais tamanhos VM são toouse disponível dentro de um grupo de disponibilidade definido usando Olá `--availability-set list-sizes` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="94a25-152">You can check toosee what VM sizes are available toouse within an existing availability set using hello `--availability-set list-sizes` parameter.</span></span>

## <a name="check-for-available-vm-sizes"></a><span data-ttu-id="94a25-153">Conferir os tamanhos de VM disponíveis</span><span class="sxs-lookup"><span data-stu-id="94a25-153">Check for available VM sizes</span></span> 

<span data-ttu-id="94a25-154">Você pode adicionar mais máquinas virtuais toohello conjunto de disponibilidade posteriormente, mas é necessário tooknow quais tamanhos VM estão disponíveis em hardware de saudação.</span><span class="sxs-lookup"><span data-stu-id="94a25-154">You can add more VMs toohello availability set later, but you need tooknow what VM sizes are available on hello hardware.</span></span> <span data-ttu-id="94a25-155">Use [lista-tamanhos do conjunto de disponibilidade de vm az](/cli/azure/availability-set#list-sizes) toolist todos os tamanhos disponíveis de Olá em hardware de saudação do cluster para o conjunto de disponibilidade hello.</span><span class="sxs-lookup"><span data-stu-id="94a25-155">Use [az vm availability-set list-sizes](/cli/azure/availability-set#list-sizes) toolist all hello available sizes on hello hardware cluster for hello availability set.</span></span>

```azurecli-interactive 
az vm availability-set list-sizes \
     --resource-group myResourceGroupAvailability \
     --name myAvailabilitySet \
     --output table  
```

## <a name="next-steps"></a><span data-ttu-id="94a25-156">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="94a25-156">Next steps</span></span>

<span data-ttu-id="94a25-157">Neste tutorial, você aprendeu como:</span><span class="sxs-lookup"><span data-stu-id="94a25-157">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="94a25-158">Criar um conjunto de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="94a25-158">Create an availability set</span></span>
> * <span data-ttu-id="94a25-159">Criar uma VM em um conjunto de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="94a25-159">Create a VM in an availability set</span></span>
> * <span data-ttu-id="94a25-160">Verificar os tamanhos de VM disponíveis</span><span class="sxs-lookup"><span data-stu-id="94a25-160">Check available VM sizes</span></span>

<span data-ttu-id="94a25-161">Avançar toohello toolearn próximo de tutorial sobre conjuntos de escala de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="94a25-161">Advance toohello next tutorial toolearn about virtual machine scale sets.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="94a25-162">Criar um conjunto de dimensionamento da VM</span><span class="sxs-lookup"><span data-stu-id="94a25-162">Create a VM scale set</span></span>](tutorial-create-vmss.md)

