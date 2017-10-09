---
title: "aaaAzure redes virtuais e máquinas virtuais do Linux | Microsoft Docs"
description: "Tutorial - gerenciar redes virtuais do Azure e máquinas virtuais Linux com hello CLI do Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/10/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 57e6bd4de16f0e31d53dc67bf50dc5730d43712b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-virtual-networks-and-linux-virtual-machines-with-hello-azure-cli"></a><span data-ttu-id="e4b90-103">Gerenciar redes virtuais do Azure e máquinas virtuais Linux com hello CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="e4b90-103">Manage Azure Virtual Networks and Linux Virtual Machines with hello Azure CLI</span></span>

<span data-ttu-id="e4b90-104">As máquinas virtuais do Azure usam a rede do Azure para comunicação de rede interna e externa.</span><span class="sxs-lookup"><span data-stu-id="e4b90-104">Azure virtual machines use Azure networking for internal and external network communication.</span></span> <span data-ttu-id="e4b90-105">Este tutorial explica como implantar duas máquinas virtuais e configurar a rede do Azure para essas VMs.</span><span class="sxs-lookup"><span data-stu-id="e4b90-105">This tutorial walks through deploying two virtual machines and configuring Azure networking for these VMs.</span></span> <span data-ttu-id="e4b90-106">exemplos de saudação neste tutorial pressupõem que VMs Olá estiver hospedando um aplicativo web com um banco de dados back-end, no entanto, um aplicativo não é implantado no tutorial de saudação.</span><span class="sxs-lookup"><span data-stu-id="e4b90-106">hello examples in this tutorial assume that hello VMs are hosting a web application with a database back-end, however an application is not deployed in hello tutorial.</span></span> <span data-ttu-id="e4b90-107">Neste tutorial, você aprenderá como:</span><span class="sxs-lookup"><span data-stu-id="e4b90-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e4b90-108">Implantar uma rede virtual</span><span class="sxs-lookup"><span data-stu-id="e4b90-108">Deploy a virtual network</span></span>
> * <span data-ttu-id="e4b90-109">Criar uma sub-rede em uma rede virtual</span><span class="sxs-lookup"><span data-stu-id="e4b90-109">Create a subnet within a virtual network</span></span>
> * <span data-ttu-id="e4b90-110">Anexar a sub-rede de tooa de máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="e4b90-110">Attach virtual machines tooa subnet</span></span>
> * <span data-ttu-id="e4b90-111">Gerenciar endereços IP públicos de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="e4b90-111">Manage virtual machine public IP addresses</span></span>
> * <span data-ttu-id="e4b90-112">Proteger tráfego da internet de entrada</span><span class="sxs-lookup"><span data-stu-id="e4b90-112">Secure incoming internet traffic</span></span>
> * <span data-ttu-id="e4b90-113">Proteger o tráfego de VM tooVM</span><span class="sxs-lookup"><span data-stu-id="e4b90-113">Secure VM tooVM traffic</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="e4b90-114">Se você escolher tooinstall e usa o hello CLI localmente, este tutorial requer que você está executando a versão de CLI do Azure Olá 2.0.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="e4b90-114">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="e4b90-115">Executar `az --version` toofind versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="e4b90-115">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="e4b90-116">Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="e4b90-116">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="vm-networking-overview"></a><span data-ttu-id="e4b90-117">Visão Geral da VM</span><span class="sxs-lookup"><span data-stu-id="e4b90-117">VM networking overview</span></span>

<span data-ttu-id="e4b90-118">Redes virtuais do Azure permitem conexões de rede segura entre máquinas virtuais, Olá internet e outros serviços do Azure como banco de dados do SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="e4b90-118">Azure virtual networks enable secure network connections between virtual machines, hello internet, and other Azure services such as Azure SQL database.</span></span> <span data-ttu-id="e4b90-119">As redes virtuais são divididas em segmentos lógicos chamados sub-redes.</span><span class="sxs-lookup"><span data-stu-id="e4b90-119">Virtual networks are broken down into logical segments called subnets.</span></span> <span data-ttu-id="e4b90-120">Sub-redes de fluxo de rede toocontrol e como um limite de segurança.</span><span class="sxs-lookup"><span data-stu-id="e4b90-120">Subnets are used toocontrol network flow, and as a security boundary.</span></span> <span data-ttu-id="e4b90-121">Ao implantar uma VM, ele geralmente inclui uma interface de rede virtual, que é anexado tooa sub-rede.</span><span class="sxs-lookup"><span data-stu-id="e4b90-121">When deploying a VM, it generally includes a virtual network interface, which is attached tooa subnet.</span></span>

## <a name="deploy-virtual-network"></a><span data-ttu-id="e4b90-122">Implantar rede virtual</span><span class="sxs-lookup"><span data-stu-id="e4b90-122">Deploy virtual network</span></span>

<span data-ttu-id="e4b90-123">Para este tutorial, uma única rede virtual é criada com duas sub-redes.</span><span class="sxs-lookup"><span data-stu-id="e4b90-123">For this tutorial, a single virtual network is created with two subnets.</span></span> <span data-ttu-id="e4b90-124">Uma sub-rede de front-end para hospedar um aplicativo Web e uma sub-rede de back-end para hospedar um servidor de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="e4b90-124">A front-end subnet for hosting a web application, and a back-end subnet for hosting a database server.</span></span>

<span data-ttu-id="e4b90-125">Antes de criar uma máquina virtual, crie um grupo de recursos com o [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="e4b90-125">Before you can create a virtual network, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="e4b90-126">Olá, exemplo a seguir cria um grupo de recursos denominado *myRGNetwork* no local de eastus hello.</span><span class="sxs-lookup"><span data-stu-id="e4b90-126">hello following example creates a resource group named *myRGNetwork* in hello eastus location.</span></span>

```azurecli-interactive 
az group create --name myRGNetwork --location eastus
```

### <a name="create-virtual-network"></a><span data-ttu-id="e4b90-127">Criar rede virtual</span><span class="sxs-lookup"><span data-stu-id="e4b90-127">Create virtual network</span></span>

<span data-ttu-id="e4b90-128">Nós Olá [criar redes de rede az](/cli/azure/network/vnet#create) comando toocreate uma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="e4b90-128">Us hello [az network vnet create](/cli/azure/network/vnet#create) command toocreate a virtual network.</span></span> <span data-ttu-id="e4b90-129">Neste exemplo, é denominada rede Olá *mvVnet* e recebe um prefixo de endereço *10.0.0.0/16*.</span><span class="sxs-lookup"><span data-stu-id="e4b90-129">In this example, hello network is named *mvVnet* and is given an address prefix of *10.0.0.0/16*.</span></span> <span data-ttu-id="e4b90-130">Uma sub-rede também é criada com o nome *mySubnetFrontEnd* e um prefixo *10.0.1.0/24*.</span><span class="sxs-lookup"><span data-stu-id="e4b90-130">A subnet is also created with a name of *mySubnetFrontEnd* and a prefix of *10.0.1.0/24*.</span></span> <span data-ttu-id="e4b90-131">Posteriormente neste tutorial uma VM de front-end é conectado toothis sub-rede.</span><span class="sxs-lookup"><span data-stu-id="e4b90-131">Later in this tutorial a front-end VM is connected toothis subnet.</span></span> 

```azurecli-interactive 
az network vnet create \
  --resource-group myRGNetwork \
  --name myVnet \
  --address-prefix 10.0.0.0/16 \
  --subnet-name mySubnetFrontEnd \
  --subnet-prefix 10.0.1.0/24
```

### <a name="create-subnet"></a><span data-ttu-id="e4b90-132">Criar sub-rede</span><span class="sxs-lookup"><span data-stu-id="e4b90-132">Create subnet</span></span>

<span data-ttu-id="e4b90-133">Uma nova sub-rede é adicionada usando Olá de rede virtual do toohello [criar sub-rede de rede virtual de rede az](/cli/azure/network/vnet/subnet#create) comando.</span><span class="sxs-lookup"><span data-stu-id="e4b90-133">A new subnet is added toohello virtual network using hello [az network vnet subnet create](/cli/azure/network/vnet/subnet#create) command.</span></span> <span data-ttu-id="e4b90-134">Neste exemplo, a sub-rede de saudação é chamada *mySubnetBackEnd* e recebe um prefixo de endereço *10.0.2.0/24*.</span><span class="sxs-lookup"><span data-stu-id="e4b90-134">In this example, hello subnet is named *mySubnetBackEnd* and is given an address prefix of *10.0.2.0/24*.</span></span> <span data-ttu-id="e4b90-135">Essa sub-rede é usada com todos os serviços de back-end.</span><span class="sxs-lookup"><span data-stu-id="e4b90-135">This subnet is used with all back-end services.</span></span>

```azurecli-interactive 
az network vnet subnet create \
  --resource-group myRGNetwork \
  --vnet-name myVnet \
  --name mySubnetBackEnd \
  --address-prefix 10.0.2.0/24
```

<span data-ttu-id="e4b90-136">Neste ponto, uma rede foi criada e segmentada em duas sub-redes, uma para os serviços de front-end e outra para serviços de back-end.</span><span class="sxs-lookup"><span data-stu-id="e4b90-136">At this point, a network has been created and segmented into two subnets, one for front-end services, and another for back-end services.</span></span> <span data-ttu-id="e4b90-137">Na próxima seção, Olá, máquinas virtuais são criadas e toothese sub-redes conectadas.</span><span class="sxs-lookup"><span data-stu-id="e4b90-137">In hello next section, virtual machines are created and connected toothese subnets.</span></span>

## <a name="understand-public-ip-address"></a><span data-ttu-id="e4b90-138">Compreender o endereço IP público</span><span class="sxs-lookup"><span data-stu-id="e4b90-138">Understand public IP address</span></span>

<span data-ttu-id="e4b90-139">Um endereço IP público permite a recursos do Azure toobe acessíveis no hello da internet.</span><span class="sxs-lookup"><span data-stu-id="e4b90-139">A public IP address allows Azure resources toobe accessible on hello internet.</span></span> <span data-ttu-id="e4b90-140">Nesta seção do tutorial hello, uma VM é criada toodemonstrate como toowork com IP público endereços.</span><span class="sxs-lookup"><span data-stu-id="e4b90-140">In this section of hello tutorial, a VM is created toodemonstrate how toowork with public IP addresses.</span></span>

### <a name="allocation-method"></a><span data-ttu-id="e4b90-141">Método de alocação</span><span class="sxs-lookup"><span data-stu-id="e4b90-141">Allocation method</span></span>

<span data-ttu-id="e4b90-142">Um endereço IP público pode ser alocado como dinâmico ou estático.</span><span class="sxs-lookup"><span data-stu-id="e4b90-142">A public IP address can be allocated as either dynamic or static.</span></span> <span data-ttu-id="e4b90-143">Por padrão, o endereço IP público é alocado dinamicamente.</span><span class="sxs-lookup"><span data-stu-id="e4b90-143">By default, public IP address dynamically allocated.</span></span> <span data-ttu-id="e4b90-144">Os endereços IP dinâmicos são liberados quando uma VM é desalocada.</span><span class="sxs-lookup"><span data-stu-id="e4b90-144">Dynamic IP addresses are released when a VM is deallocated.</span></span> <span data-ttu-id="e4b90-145">Esse comportamento causar toochange de endereço IP hello durante qualquer operação que inclui uma desalocação da VM.</span><span class="sxs-lookup"><span data-stu-id="e4b90-145">This behavior causes hello IP address toochange during any operation that includes a VM deallocation.</span></span>

<span data-ttu-id="e4b90-146">método de alocação Hello pode ser definido como toostatic, que garante que o endereço IP hello permaneçam atribuído tooa VM, mesmo durante um estado desalocado.</span><span class="sxs-lookup"><span data-stu-id="e4b90-146">hello allocation method can be set toostatic, which ensures that hello IP address remain assigned tooa VM, even during a deallocated state.</span></span> <span data-ttu-id="e4b90-147">Ao usar um endereço IP alocado estaticamente, endereço IP de saudação em si não pode ser especificado.</span><span class="sxs-lookup"><span data-stu-id="e4b90-147">When using a statically allocated IP address, hello IP address itself cannot be specified.</span></span> <span data-ttu-id="e4b90-148">Em vez disso, ele é alocado de um pool de endereços disponíveis.</span><span class="sxs-lookup"><span data-stu-id="e4b90-148">Instead, it is allocated from a pool of available addresses.</span></span>

### <a name="dynamic-allocation"></a><span data-ttu-id="e4b90-149">Alocação dinâmica</span><span class="sxs-lookup"><span data-stu-id="e4b90-149">Dynamic allocation</span></span>

<span data-ttu-id="e4b90-150">Ao criar uma VM com hello [criar vm az](/cli/azure/vm#create) comando saudação padrão público alocação método de endereço IP é dinâmico.</span><span class="sxs-lookup"><span data-stu-id="e4b90-150">When creating a VM with hello [az vm create](/cli/azure/vm#create) command, hello default public IP address allocation method is dynamic.</span></span> <span data-ttu-id="e4b90-151">No hello exemplo a seguir, uma VM é criada com um endereço IP dinâmico.</span><span class="sxs-lookup"><span data-stu-id="e4b90-151">In hello following example, a VM is created with a dynamic IP address.</span></span> 

```azurecli-interactive 
az vm create \
  --resource-group myRGNetwork \
  --name myFrontEndVM \
  --vnet-name myVnet \
  --subnet mySubnetFrontEnd \
  --nsg myNSGFrontEnd \
  --public-ip-address myFrontEndIP \
  --image UbuntuLTS \
  --generate-ssh-keys
```

### <a name="static-allocation"></a><span data-ttu-id="e4b90-152">Alocação estática</span><span class="sxs-lookup"><span data-stu-id="e4b90-152">Static allocation</span></span>

<span data-ttu-id="e4b90-153">Ao criar uma máquina virtual usando Olá [criar vm az](/cli/azure/vm#create) de comando, inclua Olá `--public-ip-address-allocation static` argumento tooassign um endereço IP público estático.</span><span class="sxs-lookup"><span data-stu-id="e4b90-153">When creating a virtual machine using hello [az vm create](/cli/azure/vm#create) command, include hello `--public-ip-address-allocation static` argument tooassign a static public IP address.</span></span> <span data-ttu-id="e4b90-154">Esta operação não será demonstrada neste tutorial, porém na próxima seção, Olá um endereço IP alocada dinamicamente é alterado tooa estaticamente endereço alocado.</span><span class="sxs-lookup"><span data-stu-id="e4b90-154">This operation is not demonstrated in this tutorial, however in hello next section a dynamically allocated IP address is changed tooa statically allocated address.</span></span> 

### <a name="change-allocation-method"></a><span data-ttu-id="e4b90-155">Alterar método de alocação</span><span class="sxs-lookup"><span data-stu-id="e4b90-155">Change allocation method</span></span>

<span data-ttu-id="e4b90-156">método de alocação de endereço IP Hello pode ser alterado usando Olá [atualização de ip público de rede az](/cli/azure/network/public-ip#update) comando.</span><span class="sxs-lookup"><span data-stu-id="e4b90-156">hello IP address allocation method can be changed using hello [az network public-ip update](/cli/azure/network/public-ip#update) command.</span></span> <span data-ttu-id="e4b90-157">Neste exemplo, Olá o método de alocação de endereço IP da VM front-end é alterado de saudação toostatic.</span><span class="sxs-lookup"><span data-stu-id="e4b90-157">In this example, hello IP address allocation method of hello front-end VM is changed toostatic.</span></span>

<span data-ttu-id="e4b90-158">Primeiro, desalocar Olá VM.</span><span class="sxs-lookup"><span data-stu-id="e4b90-158">First, deallocate hello VM.</span></span>

```azurecli-interactive 
az vm deallocate --resource-group myRGNetwork --name myFrontEndVM
```

<span data-ttu-id="e4b90-159">Saudação de uso [atualização de ip público de rede az](/cli/azure/network/public-ip#update) tooupdate método de alocação de saudação do comando.</span><span class="sxs-lookup"><span data-stu-id="e4b90-159">Use hello [az network public-ip update](/cli/azure/network/public-ip#update) command tooupdate hello allocation method.</span></span> <span data-ttu-id="e4b90-160">Nesse caso, Olá `--allocation-method` está sendo definido muito*estático*.</span><span class="sxs-lookup"><span data-stu-id="e4b90-160">In this case, hello `--allocation-method` is being set too*static*.</span></span>

```azurecli-interactive 
az network public-ip update --resource-group myRGNetwork --name myFrontEndIP --allocation-method static
```

<span data-ttu-id="e4b90-161">Inicie Olá VM.</span><span class="sxs-lookup"><span data-stu-id="e4b90-161">Start hello VM.</span></span>

```azurecli-interactive 
az vm start --resource-group myRGNetwork --name myFrontEndVM --no-wait
```

### <a name="no-public-ip-address"></a><span data-ttu-id="e4b90-162">Sem endereço IP público</span><span class="sxs-lookup"><span data-stu-id="e4b90-162">No public IP address</span></span>

<span data-ttu-id="e4b90-163">Geralmente, uma máquina virtual não precisa toobe acessível pela internet de hello.</span><span class="sxs-lookup"><span data-stu-id="e4b90-163">Often, a VM does not need toobe accessible over hello internet.</span></span> <span data-ttu-id="e4b90-164">toocreate uma máquina virtual sem um endereço IP público, use Olá `--public-ip-address ""` argumento com um conjunto vazio de aspas duplas.</span><span class="sxs-lookup"><span data-stu-id="e4b90-164">toocreate a VM without a public IP address, use hello `--public-ip-address ""` argument with an empty set of double quotes.</span></span> <span data-ttu-id="e4b90-165">Essa configuração é demonstrada mais tarde neste tutorial</span><span class="sxs-lookup"><span data-stu-id="e4b90-165">This configuration is demonstrated later in this tutorial</span></span>

## <a name="secure-network-traffic"></a><span data-ttu-id="e4b90-166">Protegem o tráfego de rede</span><span class="sxs-lookup"><span data-stu-id="e4b90-166">Secure network traffic</span></span>

<span data-ttu-id="e4b90-167">Um grupo de segurança de rede (NSG) contém uma lista de regras de segurança que permitem ou negam tooresources de tráfego de rede conectados a redes virtuais do tooAzure (VNet).</span><span class="sxs-lookup"><span data-stu-id="e4b90-167">A network security group (NSG) contains a list of security rules that allow or deny network traffic tooresources connected tooAzure Virtual Networks (VNet).</span></span> <span data-ttu-id="e4b90-168">Os NSGs podem ser associados toosubnets ou interfaces de rede individuais.</span><span class="sxs-lookup"><span data-stu-id="e4b90-168">NSGs can be associated toosubnets or individual network interfaces.</span></span> <span data-ttu-id="e4b90-169">Quando um NSG está associado uma interface de rede, ele se aplica somente a saudação associados a VM.</span><span class="sxs-lookup"><span data-stu-id="e4b90-169">When an NSG is associated with a network interface, it applies only hello associated VM.</span></span> <span data-ttu-id="e4b90-170">Quando um NSG está associado tooa sub-rede, regras de saudação aplicam tooall recursos toohello conectado sub-rede.</span><span class="sxs-lookup"><span data-stu-id="e4b90-170">When an NSG is associated tooa subnet, hello rules apply tooall resources connected toohello subnet.</span></span> 

### <a name="network-security-group-rules"></a><span data-ttu-id="e4b90-171">Regras de grupo de segurança de rede</span><span class="sxs-lookup"><span data-stu-id="e4b90-171">Network security group rules</span></span>

<span data-ttu-id="e4b90-172">As regras NSG definem portas de rede pelas quais o tráfego é permitido ou negado.</span><span class="sxs-lookup"><span data-stu-id="e4b90-172">NSG rules define networking ports over which traffic is allowed or denied.</span></span> <span data-ttu-id="e4b90-173">regras de saudação podem incluir intervalos de endereços IP de origem e de destino para que o tráfego é controlado entre sistemas específicos ou sub-redes.</span><span class="sxs-lookup"><span data-stu-id="e4b90-173">hello rules can include source and destination IP address ranges so that traffic is controlled between specific systems or subnets.</span></span> <span data-ttu-id="e4b90-174">As regras NSG também incluem uma prioridade (entre 1 e 4096).</span><span class="sxs-lookup"><span data-stu-id="e4b90-174">NSG rules also include a priority (between 1—and 4096).</span></span> <span data-ttu-id="e4b90-175">Regras são avaliadas na ordem de saudação de prioridade.</span><span class="sxs-lookup"><span data-stu-id="e4b90-175">Rules are evaluated in hello order of priority.</span></span> <span data-ttu-id="e4b90-176">Uma regra com uma prioridade 100 é avaliada antes de uma regra com prioridade 200.</span><span class="sxs-lookup"><span data-stu-id="e4b90-176">A rule with a priority of 100 is evaluated before a rule with priority 200.</span></span>

<span data-ttu-id="e4b90-177">Todos os NSGs contêm um conjunto de regras padrão.</span><span class="sxs-lookup"><span data-stu-id="e4b90-177">All NSGs contain a set of default rules.</span></span> <span data-ttu-id="e4b90-178">as regras de saudação padrão não podem ser excluídas, mas porque eles recebem a prioridade mais baixa hello, elas podem ser substituídas pelas regras de saudação que você criar.</span><span class="sxs-lookup"><span data-stu-id="e4b90-178">hello default rules cannot be deleted, but because they are assigned hello lowest priority, they can be overridden by hello rules that you create.</span></span>

- <span data-ttu-id="e4b90-179">**Rede virtual:** o tráfego que começa e termina em uma rede virtual é permitido nas direções de entrada e saída.</span><span class="sxs-lookup"><span data-stu-id="e4b90-179">**Virtual network** - Traffic originating and ending in a virtual network is allowed both in inbound and outbound directions.</span></span>
- <span data-ttu-id="e4b90-180">**Internet:** o tráfego de saída é permitido, mas o tráfego de entrada é bloqueado.</span><span class="sxs-lookup"><span data-stu-id="e4b90-180">**Internet** - Outbound traffic is allowed, but inbound traffic is blocked.</span></span>
- <span data-ttu-id="e4b90-181">**Balanceador de carga** -integridade do Azure carga balanceador tooprobe Olá permitir de suas máquinas virtuais e instâncias de função.</span><span class="sxs-lookup"><span data-stu-id="e4b90-181">**Load balancer** - Allow Azure’s load balancer tooprobe hello health of your VMs and role instances.</span></span> <span data-ttu-id="e4b90-182">Se não estiver usando um conjunto de balanceamento de carga, você poderá substituir essa regra.</span><span class="sxs-lookup"><span data-stu-id="e4b90-182">If you are not using a load balanced set, you can override this rule.</span></span>

### <a name="create-network-security-groups"></a><span data-ttu-id="e4b90-183">Criar grupos de segurança de rede</span><span class="sxs-lookup"><span data-stu-id="e4b90-183">Create network security groups</span></span>

<span data-ttu-id="e4b90-184">Um grupo de segurança de rede pode ser criado no hello mesmo tempo como uma VM usando Olá [criar vm az](/cli/azure/vm#create) comando.</span><span class="sxs-lookup"><span data-stu-id="e4b90-184">A network security group can be created at hello same time as a VM using hello [az vm create](/cli/azure/vm#create) command.</span></span> <span data-ttu-id="e4b90-185">Ao fazer isso, Olá NSG está associado com a interface de rede de VMs hello e uma regra NSG é criado automaticamente tooallow tráfego na porta *22* de qualquer fonte.</span><span class="sxs-lookup"><span data-stu-id="e4b90-185">When doing so, hello NSG is associated with hello VMs network interface and an NSG rule is auto created tooallow traffic on port *22* from any source.</span></span> <span data-ttu-id="e4b90-186">Anteriormente neste tutorial, Olá NSG front-end foi criado automaticamente com hello VM front-end.</span><span class="sxs-lookup"><span data-stu-id="e4b90-186">Earlier in this tutorial, hello front-end NSG was auto-created with hello front-end VM.</span></span> <span data-ttu-id="e4b90-187">Uma regra NSG também foi criada para a porta 22 automaticamente.</span><span class="sxs-lookup"><span data-stu-id="e4b90-187">An NSG rule was also auto created for port 22.</span></span> 

<span data-ttu-id="e4b90-188">Em alguns casos, pode ser útil toopre-criar um NSG, como quando as regras padrão SSH não devem ser criadas ou quando Olá NSG deve ser anexado tooa sub-rede.</span><span class="sxs-lookup"><span data-stu-id="e4b90-188">In some cases, it may be helpful toopre-create an NSG, such as when default SSH rules should not be created, or when hello NSG should be attached tooa subnet.</span></span> 

<span data-ttu-id="e4b90-189">Saudação de uso [criar az rede nsg](/cli/azure/network/nsg#create) comando toocreate um grupo de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="e4b90-189">Use hello [az network nsg create](/cli/azure/network/nsg#create) command toocreate a network security group.</span></span>

```azurecli-interactive 
az network nsg create --resource-group myRGNetwork --name myNSGBackEnd
```

<span data-ttu-id="e4b90-190">Em vez de associação de interface de rede do hello NSG tooa, está associado uma sub-rede.</span><span class="sxs-lookup"><span data-stu-id="e4b90-190">Instead of associating hello NSG tooa network interface, it is associated with a subnet.</span></span> <span data-ttu-id="e4b90-191">Nessa configuração, qualquer que seja anexado toohello sub-rede VM herda as regras NSG hello.</span><span class="sxs-lookup"><span data-stu-id="e4b90-191">In this configuration, any VM that is attached toohello subnet inherits hello NSG rules.</span></span>

<span data-ttu-id="e4b90-192">Atualizar subrede existente Olá denominado *mySubnetBackEnd* com hello novo NSG.</span><span class="sxs-lookup"><span data-stu-id="e4b90-192">Update hello existing subnet named *mySubnetBackEnd* with hello new NSG.</span></span>

```azurecli-interactive 
az network vnet subnet update \
  --resource-group myRGNetwork \
  --vnet-name myVnet \
  --name mySubnetBackEnd \
  --network-security-group myNSGBackEnd
```

<span data-ttu-id="e4b90-193">Agora crie uma máquina virtual, que é anexado toohello *mySubnetBackEnd*.</span><span class="sxs-lookup"><span data-stu-id="e4b90-193">Now create a virtual machine, which is attached toohello *mySubnetBackEnd*.</span></span> <span data-ttu-id="e4b90-194">Observe que Olá `--nsg` argumento tem um valor de aspas duplas vazios.</span><span class="sxs-lookup"><span data-stu-id="e4b90-194">Notice that hello `--nsg` argument has a value of empty double quotes.</span></span> <span data-ttu-id="e4b90-195">Um NSG não precisa toobe criado com hello VM.</span><span class="sxs-lookup"><span data-stu-id="e4b90-195">An NSG does not need toobe created with hello VM.</span></span> <span data-ttu-id="e4b90-196">Olá VM é a sub-rede de back-end toohello anexado, que é protegido por hello criado previamente NSG de back-end.</span><span class="sxs-lookup"><span data-stu-id="e4b90-196">hello VM is attached toohello back-end subnet, which is protected with hello pre-created back-end NSG.</span></span> <span data-ttu-id="e4b90-197">Este NSG aplica toohello VM.</span><span class="sxs-lookup"><span data-stu-id="e4b90-197">This NSG applies toohello VM.</span></span> <span data-ttu-id="e4b90-198">Além disso, observe aqui que Olá `--public-ip-address` argumento tem um valor de aspas duplas vazios.</span><span class="sxs-lookup"><span data-stu-id="e4b90-198">Also, notice here that hello `--public-ip-address` argument has a value of empty double quotes.</span></span> <span data-ttu-id="e4b90-199">Essa configuração cria uma VM sem um endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="e4b90-199">This configuration creates a VM without a public IP address.</span></span> 

```azurecli-interactive 
az vm create \
  --resource-group myRGNetwork \
  --name myBackEndVM \
  --vnet-name myVnet \
  --subnet mySubnetBackEnd \
  --public-ip-address "" \
  --nsg "" \
  --image UbuntuLTS \
  --generate-ssh-keys
```

### <a name="secure-incoming-traffic"></a><span data-ttu-id="e4b90-200">Proteger o tráfego de entrada</span><span class="sxs-lookup"><span data-stu-id="e4b90-200">Secure incoming traffic</span></span>

<span data-ttu-id="e4b90-201">Quando hello front-end VM foi criada, uma regra NSG foi criada tooallow o tráfego de entrada na porta 22.</span><span class="sxs-lookup"><span data-stu-id="e4b90-201">When hello front-end VM was created, an NSG rule was created tooallow incoming traffic on port 22.</span></span> <span data-ttu-id="e4b90-202">Essa regra permite conexões de SSH toohello VM.</span><span class="sxs-lookup"><span data-stu-id="e4b90-202">This rule allows SSH connections toohello VM.</span></span> <span data-ttu-id="e4b90-203">Para este exemplo, o tráfego também deve ser permitido na porta *80*.</span><span class="sxs-lookup"><span data-stu-id="e4b90-203">For this example, traffic should also be allowed on port *80*.</span></span> <span data-ttu-id="e4b90-204">Essa configuração permite que um toobe de aplicativo da web acessado em Olá VM.</span><span class="sxs-lookup"><span data-stu-id="e4b90-204">This configuration allows a web application toobe accessed on hello VM.</span></span>

<span data-ttu-id="e4b90-205">Saudação de uso [criar regra de nsg rede az](/cli/azure/network/nsg/rule#create) comando toocreate uma regra de porta *80*.</span><span class="sxs-lookup"><span data-stu-id="e4b90-205">Use hello [az network nsg rule create](/cli/azure/network/nsg/rule#create) command toocreate a rule for port *80*.</span></span>

```azurecli-interactive 
az network nsg rule create \
  --resource-group myRGNetwork \
  --nsg-name myNSGFrontEnd \
  --name http \
  --access allow \
  --protocol Tcp \
  --direction Inbound \
  --priority 200 \
  --source-address-prefix "*" \
  --source-port-range "*" \
  --destination-address-prefix "*" \
  --destination-port-range 80
```

<span data-ttu-id="e4b90-206">Olá front-end VM agora só está acessível na porta *22* e porta *80*.</span><span class="sxs-lookup"><span data-stu-id="e4b90-206">hello front-end VM is now only accessible on port *22* and port *80*.</span></span> <span data-ttu-id="e4b90-207">Todos os outros tráfegos de entrada é bloqueado no grupo de segurança de rede hello.</span><span class="sxs-lookup"><span data-stu-id="e4b90-207">All other incoming traffic is blocked at hello network security group.</span></span> <span data-ttu-id="e4b90-208">Pode ser as configurações de regra NSG toovisualize útil hello.</span><span class="sxs-lookup"><span data-stu-id="e4b90-208">It may be helpful toovisualize hello NSG rule configurations.</span></span> <span data-ttu-id="e4b90-209">Configuração da regra NSG Olá retorno com hello [lista de regras de rede az](/cli/azure/network/nsg/rule#list) comando.</span><span class="sxs-lookup"><span data-stu-id="e4b90-209">Return hello NSG rule configuration with hello [az network rule list](/cli/azure/network/nsg/rule#list) command.</span></span> 

```azurecli-interactive 
az network nsg rule list --resource-group myRGNetwork --nsg-name myNSGFrontEnd --output table
```

<span data-ttu-id="e4b90-210">Saída:</span><span class="sxs-lookup"><span data-stu-id="e4b90-210">Output:</span></span>

```azurecli-interactive 
Access    DestinationAddressPrefix      DestinationPortRange  Direction    Name                 Priority  Protocol    ProvisioningState    ResourceGroup    SourceAddressPrefix    SourcePortRange
--------  --------------------------  ----------------------  -----------  -----------------  ----------  ----------  -------------------  ---------------  ---------------------  -----------------
Allow     *                                               22  Inbound      default-allow-ssh        1000  Tcp         Succeeded            myRGNetwork      *                      *
Allow     *                                               80  Inbound      http                      200  Tcp         Succeeded            myRGNetwork      *                      *
```

### <a name="secure-vm-toovm-traffic"></a><span data-ttu-id="e4b90-211">Proteger o tráfego de VM tooVM</span><span class="sxs-lookup"><span data-stu-id="e4b90-211">Secure VM tooVM traffic</span></span>

<span data-ttu-id="e4b90-212">As regras de grupo de segurança de rede também podem se aplicar entre VMs.</span><span class="sxs-lookup"><span data-stu-id="e4b90-212">Network security group rules can also apply between VMs.</span></span> <span data-ttu-id="e4b90-213">Neste exemplo, Olá VM front-end precisa toocommunicate com hello VM back-end na porta *22* e *3306*.</span><span class="sxs-lookup"><span data-stu-id="e4b90-213">For this example, hello front-end VM needs toocommunicate with hello back-end VM on port *22* and *3306*.</span></span> <span data-ttu-id="e4b90-214">Essa configuração permite conexões de SSH de Olá VM front-end e também permitir que um aplicativo em Olá toocommunicate front-end de VM com um banco de dados do MySQL de back-end.</span><span class="sxs-lookup"><span data-stu-id="e4b90-214">This configuration allows SSH connections from hello front-end VM, and also allow an application on hello front-end VM toocommunicate with a back-end MySQL database.</span></span> <span data-ttu-id="e4b90-215">Todo o tráfego deve ser bloqueado entre Olá máquinas de virtuais de front-end e back-end.</span><span class="sxs-lookup"><span data-stu-id="e4b90-215">All other traffic should be blocked between hello front-end and back-end virtual machines.</span></span>

<span data-ttu-id="e4b90-216">Saudação de uso [criar regra de nsg rede az](/cli/azure/network/nsg/rule#create) comando toocreate uma regra de porta 22.</span><span class="sxs-lookup"><span data-stu-id="e4b90-216">Use hello [az network nsg rule create](/cli/azure/network/nsg/rule#create) command toocreate a rule for port 22.</span></span> <span data-ttu-id="e4b90-217">Observe que Olá `--source-address-prefix` argumento especifica um valor de *10.0.1.0/24*.</span><span class="sxs-lookup"><span data-stu-id="e4b90-217">Notice that hello `--source-address-prefix` argument specifies a value of *10.0.1.0/24*.</span></span> <span data-ttu-id="e4b90-218">Essa configuração garante que apenas o tráfego de sub-rede front-end Olá é permitido por meio de saudação NSG.</span><span class="sxs-lookup"><span data-stu-id="e4b90-218">This configuration ensures that only traffic from hello front-end subnet is allowed through hello NSG.</span></span>

```azurecli-interactive 
az network nsg rule create \
  --resource-group myRGNetwork \
  --nsg-name myNSGBackEnd \
  --name SSH \
  --access Allow \
  --protocol Tcp \
  --direction Inbound \
  --priority 100 \
  --source-address-prefix 10.0.1.0/24 \
  --source-port-range "*" \
  --destination-address-prefix "*" \
  --destination-port-range "22"
```

<span data-ttu-id="e4b90-219">Agora, adicione uma regra para o tráfego MySQL na porta 3306.</span><span class="sxs-lookup"><span data-stu-id="e4b90-219">Now add a rule for MySQL traffic on port 3306.</span></span>

```azurecli-interactive 
az network nsg rule create \
  --resource-group myRGNetwork \
  --nsg-name myNSGBackEnd \
  --name MySQL \
  --access Allow \
  --protocol Tcp \
  --direction Inbound \
  --priority 200 \
  --source-address-prefix 10.0.1.0/24 \
  --source-port-range "*" \
  --destination-address-prefix "*" \
  --destination-port-range "3306"
```

<span data-ttu-id="e4b90-220">Por fim, porque os NSGs tem uma regra padrão permitindo que todo o tráfego entre VMs em Olá mesmo VNet, uma regra pode ser criada para Olá back-end NSGs tooblock todo o tráfego.</span><span class="sxs-lookup"><span data-stu-id="e4b90-220">Finally, because NSGs have a default rule allowing all traffic between VMs in hello same VNet, a rule can be created for hello back-end NSGs tooblock all traffic.</span></span> <span data-ttu-id="e4b90-221">Observe aqui que Olá `--priority` recebe um valor de *300*, que é menor do que ambos Olá regras NSG e MySQL.</span><span class="sxs-lookup"><span data-stu-id="e4b90-221">Notice here that hello `--priority` is given a value of *300*, which is lower that both hello NSG and MySQL rules.</span></span> <span data-ttu-id="e4b90-222">Essa configuração garante que o tráfego SSH e MySQL ainda é permitido pelo Olá NSG.</span><span class="sxs-lookup"><span data-stu-id="e4b90-222">This configuration ensures that SSH and MySQL traffic is still allowed through hello NSG.</span></span>

```azurecli-interactive 
az network nsg rule create \
  --resource-group myRGNetwork \
  --nsg-name myNSGBackEnd \
  --name denyAll \
  --access Deny \
  --protocol Tcp \
  --direction Inbound \
  --priority 300 \
  --source-address-prefix "*" \
  --source-port-range "*" \
  --destination-address-prefix "*" \
  --destination-port-range "*"
```

<span data-ttu-id="e4b90-223">Olá VM back-end é agora somente acessível na porta *22* e porta *3306* da sub-rede front-end hello.</span><span class="sxs-lookup"><span data-stu-id="e4b90-223">hello back-end VM is now only accessible on port *22* and port *3306* from hello front-end subnet.</span></span> <span data-ttu-id="e4b90-224">Todos os outros tráfegos de entrada é bloqueado no grupo de segurança de rede hello.</span><span class="sxs-lookup"><span data-stu-id="e4b90-224">All other incoming traffic is blocked at hello network security group.</span></span> <span data-ttu-id="e4b90-225">Pode ser as configurações de regra NSG toovisualize útil hello.</span><span class="sxs-lookup"><span data-stu-id="e4b90-225">It may be helpful toovisualize hello NSG rule configurations.</span></span> <span data-ttu-id="e4b90-226">Configuração da regra NSG Olá retorno com hello [lista de regras de rede az](/cli/azure/network/nsg/rule#list) comando.</span><span class="sxs-lookup"><span data-stu-id="e4b90-226">Return hello NSG rule configuration with hello [az network rule list](/cli/azure/network/nsg/rule#list) command.</span></span> 

```azurecli-interactive 
az network nsg rule list --resource-group myRGNetwork --nsg-name myNSGBackEnd --output table
```

<span data-ttu-id="e4b90-227">Saída:</span><span class="sxs-lookup"><span data-stu-id="e4b90-227">Output:</span></span>

```azurecli-interactive 
Access    DestinationAddressPrefix    DestinationPortRange    Direction    Name       Priority  Protocol    ProvisioningState    ResourceGroup    SourceAddressPrefix    SourcePortRange
--------  --------------------------  ----------------------  -----------  -------  ----------  ----------  -------------------  ---------------  ---------------------  -----------------
Allow     *                           22                      Inbound      SSH             100  Tcp         Succeeded            myRGNetwork      10.0.1.0/24            *
Allow     *                           3306                    Inbound      MySQL           200  Tcp         Succeeded            myRGNetwork      10.0.1.0/24            *
Deny      *                           *                       Inbound      denyAll         300  Tcp         Succeeded            myRGNetwork      *                      *
```

## <a name="next-steps"></a><span data-ttu-id="e4b90-228">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e4b90-228">Next steps</span></span>

<span data-ttu-id="e4b90-229">Neste tutorial, você criou e redes do Azure como máquinas toovirtual relacionados seguras.</span><span class="sxs-lookup"><span data-stu-id="e4b90-229">In this tutorial, you created and secured Azure networks as related toovirtual machines.</span></span> <span data-ttu-id="e4b90-230">Você aprendeu como:</span><span class="sxs-lookup"><span data-stu-id="e4b90-230">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e4b90-231">Implantar uma rede virtual</span><span class="sxs-lookup"><span data-stu-id="e4b90-231">Deploy a virtual network</span></span>
> * <span data-ttu-id="e4b90-232">Criar uma sub-rede em uma rede virtual</span><span class="sxs-lookup"><span data-stu-id="e4b90-232">Create a subnet within a virtual network</span></span>
> * <span data-ttu-id="e4b90-233">Anexar a sub-rede de tooa de máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="e4b90-233">Attach virtual machines tooa subnet</span></span>
> * <span data-ttu-id="e4b90-234">Gerenciar endereços IP públicos de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="e4b90-234">Manage virtual machine public IP addresses</span></span>
> * <span data-ttu-id="e4b90-235">Proteger tráfego da internet de entrada</span><span class="sxs-lookup"><span data-stu-id="e4b90-235">Secure incoming internet traffic</span></span>
> * <span data-ttu-id="e4b90-236">Proteger o tráfego de VM tooVM</span><span class="sxs-lookup"><span data-stu-id="e4b90-236">Secure VM tooVM traffic</span></span>

<span data-ttu-id="e4b90-237">Avançar toohello toolearn próximo de tutorial sobre como proteger dados em máquinas virtuais usando o backup do Azure.</span><span class="sxs-lookup"><span data-stu-id="e4b90-237">Advance toohello next tutorial toolearn about securing data on virtual machines using Azure backup.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="e4b90-238">Fazer backup de máquinas virtuais do Linux no Azure</span><span class="sxs-lookup"><span data-stu-id="e4b90-238">Back up Linux virtual machines in Azure</span></span>](./tutorial-backup-vms.md)
