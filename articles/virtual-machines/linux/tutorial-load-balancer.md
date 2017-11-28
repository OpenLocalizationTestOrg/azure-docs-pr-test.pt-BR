---
title: "aaaHow tooload equilibrar as máquinas virtuais Linux no Azure | Microsoft Docs"
description: "Saiba como toouse hello Azure carregar balanceador toocreate um aplicativo altamente disponível e seguro entre três VMs do Linux"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/11/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: f01752c3caec3489ee13e63000775769f3236e11
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooload-balance-linux-virtual-machines-in-azure-toocreate-a-highly-available-application"></a><span data-ttu-id="abf89-103">Como o tooload equilibrar a máquinas virtuais Linux no Azure toocreate um aplicativo altamente disponível</span><span class="sxs-lookup"><span data-stu-id="abf89-103">How tooload balance Linux virtual machines in Azure toocreate a highly available application</span></span>
<span data-ttu-id="abf89-104">O balanceamento de carga fornece um nível mais alto de disponibilidade, distribuindo as solicitações de entrada em várias máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="abf89-104">Load balancing provides a higher level of availability by spreading incoming requests across multiple virtual machines.</span></span> <span data-ttu-id="abf89-105">Neste tutorial, você aprenderá sobre Olá diferentes componentes do balanceador de carga do Azure Olá que distribuir o tráfego e fornecem alta disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="abf89-105">In this tutorial, you learn about hello different components of hello Azure load balancer that distribute traffic and provide high availability.</span></span> <span data-ttu-id="abf89-106">Você aprenderá como:</span><span class="sxs-lookup"><span data-stu-id="abf89-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="abf89-107">Criar um balanceador de carga do Azure</span><span class="sxs-lookup"><span data-stu-id="abf89-107">Create an Azure load balancer</span></span>
> * <span data-ttu-id="abf89-108">Criar uma investigação de integridade do balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="abf89-108">Create a load balancer health probe</span></span>
> * <span data-ttu-id="abf89-109">Criar regras de tráfego para o balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="abf89-109">Create load balancer traffic rules</span></span>
> * <span data-ttu-id="abf89-110">Use a nuvem init toocreate um aplicativo básico do Node. js</span><span class="sxs-lookup"><span data-stu-id="abf89-110">Use cloud-init toocreate a basic Node.js app</span></span>
> * <span data-ttu-id="abf89-111">Criar máquinas virtuais e anexar tooa balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="abf89-111">Create virtual machines and attach tooa load balancer</span></span>
> * <span data-ttu-id="abf89-112">Exibir um balanceador de carga em ação</span><span class="sxs-lookup"><span data-stu-id="abf89-112">View a load balancer in action</span></span>
> * <span data-ttu-id="abf89-113">Adicionar e remover as VMs de um balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="abf89-113">Add and remove VMs from a load balancer</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="abf89-114">Se você escolher tooinstall e usa o hello CLI localmente, este tutorial requer que você está executando a versão de CLI do Azure Olá 2.0.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="abf89-114">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="abf89-115">Executar `az --version` toofind versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="abf89-115">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="abf89-116">Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="abf89-116">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="azure-load-balancer-overview"></a><span data-ttu-id="abf89-117">Visão geral do Balanceador de Carga do Azure</span><span class="sxs-lookup"><span data-stu-id="abf89-117">Azure load balancer overview</span></span>
<span data-ttu-id="abf89-118">Um Azure Load Balancer é um balanceador de carga de Camada 4 (TCP, UDP) que fornece alta disponibilidade distribuindo o tráfego de entrada entre VMs íntegros.</span><span class="sxs-lookup"><span data-stu-id="abf89-118">An Azure load balancer is a Layer-4 (TCP, UDP) load balancer that provides high availability by distributing incoming traffic among healthy VMs.</span></span> <span data-ttu-id="abf89-119">Um teste de integridade do balanceador de carga monitora uma determinada porta em cada VM e só distribui o tráfego tooan operacional VM.</span><span class="sxs-lookup"><span data-stu-id="abf89-119">A load balancer health probe monitors a given port on each VM and only distributes traffic tooan operational VM.</span></span>

<span data-ttu-id="abf89-120">Você define uma configuração de IP de front-end que contém um ou mais endereços IP públicos.</span><span class="sxs-lookup"><span data-stu-id="abf89-120">You define a front-end IP configuration that contains one or more public IP addresses.</span></span> <span data-ttu-id="abf89-121">Essa configuração de IP de front-end permite que seu toobe de aplicativos e o balanceador de carga acessível pela Internet da saudação.</span><span class="sxs-lookup"><span data-stu-id="abf89-121">This front-end IP configuration allows your load balancer and applications toobe accessible over hello Internet.</span></span> 

<span data-ttu-id="abf89-122">Máquinas virtuais conectar-se usando sua placa de interface de rede virtual (NIC) de Balanceador de carga tooa.</span><span class="sxs-lookup"><span data-stu-id="abf89-122">Virtual machines connect tooa load balancer using their virtual network interface card (NIC).</span></span> <span data-ttu-id="abf89-123">tráfego de toodistribute toohello VMs, um pool de endereços de back-end contém endereços IP Olá Olá virtual (NICs) toohello conectados do balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="abf89-123">toodistribute traffic toohello VMs, a back-end address pool contains hello IP addresses of hello virtual (NICs) connected toohello load balancer.</span></span>

<span data-ttu-id="abf89-124">fluxo de saudação toocontrol de tráfego, você definir regras de Balanceador de carga para portas e protocolos que mapeiam tooyour VMs específicos.</span><span class="sxs-lookup"><span data-stu-id="abf89-124">toocontrol hello flow of traffic, you define load balancer rules for specific ports and protocols that map tooyour VMs.</span></span>

<span data-ttu-id="abf89-125">Se você seguiu o tutorial anterior Olá muito[criar um conjunto de escala de máquinas virtuais](tutorial-create-vmss.md), um balanceador de carga foi criado para você.</span><span class="sxs-lookup"><span data-stu-id="abf89-125">If you followed hello previous tutorial too[create a virtual machine scale set](tutorial-create-vmss.md), a load balancer was created for you.</span></span> <span data-ttu-id="abf89-126">Todos esses componentes foram configurados para você como parte do conjunto de escala de saudação.</span><span class="sxs-lookup"><span data-stu-id="abf89-126">All these components were configured for you as part of hello scale set.</span></span>


## <a name="create-azure-load-balancer"></a><span data-ttu-id="abf89-127">Criar o balanceador de carga do Azure</span><span class="sxs-lookup"><span data-stu-id="abf89-127">Create Azure load balancer</span></span>
<span data-ttu-id="abf89-128">Esta seção fornece detalhes sobre como você pode criar e configurar cada componente de saudação do balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="abf89-128">This section details how you can create and configure each component of hello load balancer.</span></span> <span data-ttu-id="abf89-129">Antes de criar seu balanceador de carga, crie um grupo de recursos com o [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="abf89-129">Before you can create your load balancer, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="abf89-130">Olá, exemplo a seguir cria um grupo de recursos denominado *myResourceGroupLoadBalancer* em Olá *eastus* local:</span><span class="sxs-lookup"><span data-stu-id="abf89-130">hello following example creates a resource group named *myResourceGroupLoadBalancer* in hello *eastus* location:</span></span>

```azurecli-interactive 
az group create --name myResourceGroupLoadBalancer --location eastus
```

### <a name="create-a-public-ip-address"></a><span data-ttu-id="abf89-131">Criar um endereço IP público</span><span class="sxs-lookup"><span data-stu-id="abf89-131">Create a public IP address</span></span>
<span data-ttu-id="abf89-132">tooaccess Olá de seu aplicativo na Internet, é necessário um endereço IP público Olá balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="abf89-132">tooaccess your app on hello Internet, you need a public IP address for hello load balancer.</span></span> <span data-ttu-id="abf89-133">Crie um endereço IP público com [az network public-ip create](/cli/azure/network/public-ip#create).</span><span class="sxs-lookup"><span data-stu-id="abf89-133">Create a public IP address with [az network public-ip create](/cli/azure/network/public-ip#create).</span></span> <span data-ttu-id="abf89-134">Olá, exemplo a seguir cria um endereço IP público denominado *myPublicIP* em Olá *myResourceGroupLoadBalancer* grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="abf89-134">hello following example creates a public IP address named *myPublicIP* in hello *myResourceGroupLoadBalancer* resource group:</span></span>

```azurecli-interactive 
az network public-ip create \
    --resource-group myResourceGroupLoadBalancer \
    --name myPublicIP
```

### <a name="create-a-load-balancer"></a><span data-ttu-id="abf89-135">Criar um balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="abf89-135">Create a load balancer</span></span>
<span data-ttu-id="abf89-136">Crie um balanceador de carga com [az network lb create](/cli/azure/network/lb#create).</span><span class="sxs-lookup"><span data-stu-id="abf89-136">Create a load balancer with [az network lb create](/cli/azure/network/lb#create).</span></span> <span data-ttu-id="abf89-137">Olá, exemplo a seguir cria um balanceador de carga denominado *myLoadBalancer* e atribui hello *myPublicIP* configuração de IP de front-end do endereço toohello:</span><span class="sxs-lookup"><span data-stu-id="abf89-137">hello following example creates a load balancer named *myLoadBalancer* and assigns hello *myPublicIP* address toohello front-end IP configuration:</span></span>

```azurecli-interactive 
az network lb create \
    --resource-group myResourceGroupLoadBalancer \
    --name myLoadBalancer \
    --frontend-ip-name myFrontEndPool \
    --backend-pool-name myBackEndPool \
    --public-ip-address myPublicIP
```

### <a name="create-a-health-probe"></a><span data-ttu-id="abf89-138">Criar uma investigação de integridade</span><span class="sxs-lookup"><span data-stu-id="abf89-138">Create a health probe</span></span>
<span data-ttu-id="abf89-139">tooallow Olá balanceador toomonitor Olá status de carga do seu aplicativo, você usar uma investigação de integridade.</span><span class="sxs-lookup"><span data-stu-id="abf89-139">tooallow hello load balancer toomonitor hello status of your app, you use a health probe.</span></span> <span data-ttu-id="abf89-140">investigação de integridade Olá dinamicamente adiciona ou remove as VMs de rotação do balanceador de carga de saudação com base em suas verificações de toohealth de resposta.</span><span class="sxs-lookup"><span data-stu-id="abf89-140">hello health probe dynamically adds or removes VMs from hello load balancer rotation based on their response toohealth checks.</span></span> <span data-ttu-id="abf89-141">Por padrão, uma máquina virtual é removida da distribuição de Balanceador de carga Olá após duas falhas consecutivas em intervalos de 15 segundos.</span><span class="sxs-lookup"><span data-stu-id="abf89-141">By default, a VM is removed from hello load balancer distribution after two consecutive failures at 15-second intervals.</span></span> <span data-ttu-id="abf89-142">Crie uma investigação de integridade com base em um protocolo ou página de verificação de integridade específica ao seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="abf89-142">You create a health probe based on a protocol or a specific health check page for your app.</span></span> 

<span data-ttu-id="abf89-143">saudação de exemplo a seguir cria uma investigação TCP.</span><span class="sxs-lookup"><span data-stu-id="abf89-143">hello following example creates a TCP probe.</span></span> <span data-ttu-id="abf89-144">Você também pode criar investigações de HTTP personalizadas para obter verificações de integridade mais refinadas.</span><span class="sxs-lookup"><span data-stu-id="abf89-144">You can also create custom HTTP probes for more fine grained health checks.</span></span> <span data-ttu-id="abf89-145">Ao usar uma investigação personalizada de HTTP, você deve criar página de verificação de integridade hello, tais como *healthcheck.js*.</span><span class="sxs-lookup"><span data-stu-id="abf89-145">When using a custom HTTP probe, you must create hello health check page, such as *healthcheck.js*.</span></span> <span data-ttu-id="abf89-146">investigação de saudação deve retornar um **HTTP 200 Okey** resposta para Olá carga balanceador tookeep Olá host rotação.</span><span class="sxs-lookup"><span data-stu-id="abf89-146">hello probe must return an **HTTP 200 OK** response for hello load balancer tookeep hello host in rotation.</span></span>

<span data-ttu-id="abf89-147">toocreate uma investigação de integridade TCP, use [criar investigação de balanceamento de carga de rede az](/cli/azure/network/lb/probe#create).</span><span class="sxs-lookup"><span data-stu-id="abf89-147">toocreate a TCP health probe, you use [az network lb probe create](/cli/azure/network/lb/probe#create).</span></span> <span data-ttu-id="abf89-148">Olá, exemplo a seguir cria um teste de integridade chamado *myHealthProbe*:</span><span class="sxs-lookup"><span data-stu-id="abf89-148">hello following example creates a health probe named *myHealthProbe*:</span></span>

```azurecli-interactive 
az network lb probe create \
    --resource-group myResourceGroupLoadBalancer \
    --lb-name myLoadBalancer \
    --name myHealthProbe \
    --protocol tcp \
    --port 80
```

### <a name="create-a-load-balancer-rule"></a><span data-ttu-id="abf89-149">Criar uma regra de balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="abf89-149">Create a load balancer rule</span></span>
<span data-ttu-id="abf89-150">Uma regra de Balanceador de carga é toodefine usado como o tráfego é distribuído toohello VMs.</span><span class="sxs-lookup"><span data-stu-id="abf89-150">A load balancer rule is used toodefine how traffic is distributed toohello VMs.</span></span> <span data-ttu-id="abf89-151">Você definir a configuração de IP front-end Olá para o tráfego de entrada hello e Olá back-end pool tooreceive Olá tráfego IP, juntamente com a origem de saudação necessários e porta de destino.</span><span class="sxs-lookup"><span data-stu-id="abf89-151">You define hello front-end IP configuration for hello incoming traffic and hello back-end IP pool tooreceive hello traffic, along with hello required source and destination port.</span></span> <span data-ttu-id="abf89-152">toomake-se de que apenas as VMs íntegras receberem tráfego, você também definir Olá toouse de investigação de integridade.</span><span class="sxs-lookup"><span data-stu-id="abf89-152">toomake sure only healthy VMs receive traffic, you also define hello health probe toouse.</span></span>

<span data-ttu-id="abf89-153">Crie uma regra de balanceador de carga com [az network lb rule create](/cli/azure/network/lb/rule#create).</span><span class="sxs-lookup"><span data-stu-id="abf89-153">Create a load balancer rule with [az network lb rule create](/cli/azure/network/lb/rule#create).</span></span> <span data-ttu-id="abf89-154">Olá, exemplo a seguir cria uma regra denominada *myLoadBalancerRule*, Olá usa *myHealthProbe* investigação de integridade e o tráfego na porta saldos *80*:</span><span class="sxs-lookup"><span data-stu-id="abf89-154">hello following example creates a rule named *myLoadBalancerRule*, uses hello *myHealthProbe* health probe, and balances traffic on port *80*:</span></span>

```azurecli-interactive 
az network lb rule create \
    --resource-group myResourceGroupLoadBalancer \
    --lb-name myLoadBalancer \
    --name myLoadBalancerRule \
    --protocol tcp \
    --frontend-port 80 \
    --backend-port 80 \
    --frontend-ip-name myFrontEndPool \
    --backend-pool-name myBackEndPool \
    --probe-name myHealthProbe
```


## <a name="configure-virtual-network"></a><span data-ttu-id="abf89-155">Configurar rede virtual</span><span class="sxs-lookup"><span data-stu-id="abf89-155">Configure virtual network</span></span>
<span data-ttu-id="abf89-156">Antes de implantar algumas máquinas virtuais e testar seu balanceador, crie hello dando suporte a recursos de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="abf89-156">Before you deploy some VMs and can test your balancer, create hello supporting virtual network resources.</span></span> <span data-ttu-id="abf89-157">Para obter mais informações sobre redes virtuais, consulte Olá [gerenciar redes virtuais do Azure](tutorial-virtual-network.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="abf89-157">For more information about virtual networks, see hello [Manage Azure Virtual Networks](tutorial-virtual-network.md) tutorial.</span></span>

### <a name="create-network-resources"></a><span data-ttu-id="abf89-158">Criar recursos da rede</span><span class="sxs-lookup"><span data-stu-id="abf89-158">Create network resources</span></span>
<span data-ttu-id="abf89-159">Crie a rede virtual com [az network vnet create](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="abf89-159">Create a virtual network with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="abf89-160">Olá, exemplo a seguir cria uma rede virtual denominada *myVnet* com uma sub-rede denominada *mySubnet*:</span><span class="sxs-lookup"><span data-stu-id="abf89-160">hello following example creates a virtual network named *myVnet* with a subnet named *mySubnet*:</span></span>

```azurecli-interactive 
az network vnet create \
    --resource-group myResourceGroupLoadBalancer \
    --name myVnet \
    --subnet-name mySubnet
```

<span data-ttu-id="abf89-161">tooadd um grupo de segurança de rede, use [criar az rede nsg](/cli/azure/network/nsg#create).</span><span class="sxs-lookup"><span data-stu-id="abf89-161">tooadd a network security group, you use [az network nsg create](/cli/azure/network/nsg#create).</span></span> <span data-ttu-id="abf89-162">Olá, exemplo a seguir cria um grupo de segurança de rede denominado *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="abf89-162">hello following example creates a network security group named *myNetworkSecurityGroup*:</span></span>

```azurecli-interactive 
az network nsg create \
    --resource-group myResourceGroupLoadBalancer \
    --name myNetworkSecurityGroup
```

<span data-ttu-id="abf89-163">Crie uma regra de grupo de segurança de rede com [az network nsg create](/cli/azure/network/nsg/rule#create).</span><span class="sxs-lookup"><span data-stu-id="abf89-163">Create a network security group rule with [az network nsg rule create](/cli/azure/network/nsg/rule#create).</span></span> <span data-ttu-id="abf89-164">Olá, exemplo a seguir cria uma regra de grupo de segurança de rede denominada *myNetworkSecurityGroupRule*:</span><span class="sxs-lookup"><span data-stu-id="abf89-164">hello following example creates a network security group rule named *myNetworkSecurityGroupRule*:</span></span>

```azurecli-interactive 
az network nsg rule create \
    --resource-group myResourceGroupLoadBalancer \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --priority 1001 \
    --protocol tcp \
    --destination-port-range 80
```

<span data-ttu-id="abf89-165">NICs virtuais são criadas com [az network nic create](/cli/azure/network/nic#create).</span><span class="sxs-lookup"><span data-stu-id="abf89-165">Virtual NICs are created with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="abf89-166">Olá, exemplo a seguir cria três NICs virtuais.</span><span class="sxs-lookup"><span data-stu-id="abf89-166">hello following example creates three virtual NICs.</span></span> <span data-ttu-id="abf89-167">(Uma NIC virtual para cada VM que você criou para seu aplicativo no hello seguindo as etapas.)</span><span class="sxs-lookup"><span data-stu-id="abf89-167">(One virtual NIC for each VM you create for your app in hello following steps).</span></span> <span data-ttu-id="abf89-168">Você pode criar VMs e NICs virtuais adicionais a qualquer momento e adicioná-los toohello balanceador de carga:</span><span class="sxs-lookup"><span data-stu-id="abf89-168">You can create additional virtual NICs and VMs at any time and add them toohello load balancer:</span></span>

```bash
for i in `seq 1 3`; do
    az network nic create \
        --resource-group myResourceGroupLoadBalancer \
        --name myNic$i \
        --vnet-name myVnet \
        --subnet mySubnet \
        --network-security-group myNetworkSecurityGroup \
        --lb-name myLoadBalancer \
        --lb-address-pools myBackEndPool
done
```

## <a name="create-virtual-machines"></a><span data-ttu-id="abf89-169">Criar máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="abf89-169">Create virtual machines</span></span>

### <a name="create-cloud-init-config"></a><span data-ttu-id="abf89-170">Criar configuração de inicialização de nuvem</span><span class="sxs-lookup"><span data-stu-id="abf89-170">Create cloud-init config</span></span>
<span data-ttu-id="abf89-171">Um tutorial anterior em [como toocustomize uma máquina virtual do Linux na primeira inicialização](tutorial-automate-vm-deployment.md), você aprendeu como tooautomate personalização de VM com a nuvem init.</span><span class="sxs-lookup"><span data-stu-id="abf89-171">In a previous tutorial on [How toocustomize a Linux virtual machine on first boot](tutorial-automate-vm-deployment.md), you learned how tooautomate VM customization with cloud-init.</span></span> <span data-ttu-id="abf89-172">Você pode usar Olá tooinstall de arquivo de configuração de nuvem init mesmo NGINX e executar um aplicativo simples do 'Hello World' Node. js.</span><span class="sxs-lookup"><span data-stu-id="abf89-172">You can use hello same cloud-init configuration file tooinstall NGINX and run a simple 'Hello World' Node.js app.</span></span>

<span data-ttu-id="abf89-173">No shell atual, crie um arquivo chamado *init.txt nuvem* e colar Olá seguinte configuração.</span><span class="sxs-lookup"><span data-stu-id="abf89-173">In your current shell, create a file named *cloud-init.txt* and paste hello following configuration.</span></span> <span data-ttu-id="abf89-174">Por exemplo, crie o arquivo de saudação no hello nuvem Shell não está no seu computador local.</span><span class="sxs-lookup"><span data-stu-id="abf89-174">For example, create hello file in hello Cloud Shell not on your local machine.</span></span> <span data-ttu-id="abf89-175">Digite `sensible-editor cloud-init.txt` toocreate Olá arquivo e ver uma lista de editores disponíveis.</span><span class="sxs-lookup"><span data-stu-id="abf89-175">Enter `sensible-editor cloud-init.txt` toocreate hello file and see a list of available editors.</span></span> <span data-ttu-id="abf89-176">Verifique se que esse arquivo de inicialização de nuvem inteiro Olá foi copiado corretamente, Olá especialmente a primeira linha:</span><span class="sxs-lookup"><span data-stu-id="abf89-176">Make sure that hello whole cloud-init file is copied correctly, especially hello first line:</span></span>

```yaml
#cloud-config
package_upgrade: true
packages:
  - nginx
  - nodejs
  - npm
write_files:
  - owner: www-data:www-data
  - path: /etc/nginx/sites-available/default
    content: |
      server {
        listen 80;
        location / {
          proxy_pass http://localhost:3000;
          proxy_http_version 1.1;
          proxy_set_header Upgrade $http_upgrade;
          proxy_set_header Connection keep-alive;
          proxy_set_header Host $host;
          proxy_cache_bypass $http_upgrade;
        }
      }
  - owner: azureuser:azureuser
  - path: /home/azureuser/myapp/index.js
    content: |
      var express = require('express')
      var app = express()
      var os = require('os');
      app.get('/', function (req, res) {
        res.send('Hello World from host ' + os.hostname() + '!')
      })
      app.listen(3000, function () {
        console.log('Hello world app listening on port 3000!')
      })
runcmd:
  - service nginx restart
  - cd "/home/azureuser/myapp"
  - npm init
  - npm install express -y
  - nodejs index.js
```

### <a name="create-virtual-machines"></a><span data-ttu-id="abf89-177">Criar máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="abf89-177">Create virtual machines</span></span>
<span data-ttu-id="abf89-178">tooimprove Olá alta disponibilidade do seu aplicativo, colocar suas VMs em um conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="abf89-178">tooimprove hello high availability of your app, place your VMs in an availability set.</span></span> <span data-ttu-id="abf89-179">Para obter mais informações sobre conjuntos de disponibilidade, consulte Olá anterior [como máquinas virtuais altamente disponíveis de toocreate](tutorial-availability-sets.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="abf89-179">For more information about availability sets, see hello previous [How toocreate highly available virtual machines](tutorial-availability-sets.md) tutorial.</span></span>

<span data-ttu-id="abf89-180">Crie um conjunto de disponibilidade com [az vm availability-set create](/cli/azure/vm/availability-set#create).</span><span class="sxs-lookup"><span data-stu-id="abf89-180">Create an availability set with [az vm availability-set create](/cli/azure/vm/availability-set#create).</span></span> <span data-ttu-id="abf89-181">Olá, exemplo a seguir cria um conjunto nomeada de disponibilidade *myAvailabilitySet*:</span><span class="sxs-lookup"><span data-stu-id="abf89-181">hello following example creates an availability set named *myAvailabilitySet*:</span></span>

```azurecli-interactive 
az vm availability-set create \
    --resource-group myResourceGroupLoadBalancer \
    --name myAvailabilitySet
```

<span data-ttu-id="abf89-182">Agora você pode criar VMs Olá com [criar vm az](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="abf89-182">Now you can create hello VMs with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="abf89-183">Olá exemplo a seguir cria três VMs e gera as chaves de SSH se eles ainda não existir:</span><span class="sxs-lookup"><span data-stu-id="abf89-183">hello following example creates three VMs and generates SSH keys if they do not already exist:</span></span>

```bash
for i in `seq 1 3`; do
    az vm create \
        --resource-group myResourceGroupLoadBalancer \
        --name myVM$i \
        --availability-set myAvailabilitySet \
        --nics myNic$i \
        --image UbuntuLTS \
        --admin-username azureuser \
        --generate-ssh-keys \
        --custom-data cloud-init.txt \
        --no-wait
done
```

<span data-ttu-id="abf89-184">Há tarefas em segundo plano que continuam toorun depois Olá CLI do Azure retorna toohello prompt.</span><span class="sxs-lookup"><span data-stu-id="abf89-184">There are background tasks that continue toorun after hello Azure CLI returns you toohello prompt.</span></span> <span data-ttu-id="abf89-185">Olá `--no-wait` parâmetro não espera para todos os Olá toocomplete de tarefas.</span><span class="sxs-lookup"><span data-stu-id="abf89-185">hello `--no-wait` parameter does not wait for all hello tasks toocomplete.</span></span> <span data-ttu-id="abf89-186">Pode ser outro alguns minutos antes de poder acessar o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="abf89-186">It may be another couple of minutes before you can access hello app.</span></span> <span data-ttu-id="abf89-187">Olá investigação de integridade do balanceador de carga detecta automaticamente quando o aplicativo hello está em execução em cada VM.</span><span class="sxs-lookup"><span data-stu-id="abf89-187">hello load balancer health probe automatically detects when hello app is running on each VM.</span></span> <span data-ttu-id="abf89-188">Depois que o aplicativo hello está em execução, regra de Balanceador de carga Olá inicia toodistribute tráfego.</span><span class="sxs-lookup"><span data-stu-id="abf89-188">Once hello app is running, hello load balancer rule starts toodistribute traffic.</span></span>


## <a name="test-load-balancer"></a><span data-ttu-id="abf89-189">Testar o balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="abf89-189">Test load balancer</span></span>
<span data-ttu-id="abf89-190">Obter o endereço IP público de saudação do balanceador de carga com [az rede ip público exibir](/cli/azure/network/public-ip#show).</span><span class="sxs-lookup"><span data-stu-id="abf89-190">Obtain hello public IP address of your load balancer with [az network public-ip show](/cli/azure/network/public-ip#show).</span></span> <span data-ttu-id="abf89-191">Olá, exemplo a seguir obtém endereço IP hello *myPublicIP* criado anteriormente:</span><span class="sxs-lookup"><span data-stu-id="abf89-191">hello following example obtains hello IP address for *myPublicIP* created earlier:</span></span>

```azurecli-interactive 
az network public-ip show \
    --resource-group myResourceGroupLoadBalancer \
    --name myPublicIP \
    --query [ipAddress] \
    --output tsv
```

<span data-ttu-id="abf89-192">Você pode inserir o endereço IP público de saudação no navegador da web de tooa.</span><span class="sxs-lookup"><span data-stu-id="abf89-192">You can then enter hello public IP address in tooa web browser.</span></span> <span data-ttu-id="abf89-193">Lembre-se: demora alguns minutos Olá Olá VMs toobe pronto antes do início de Balanceador de carga Olá toodistribute toothem de tráfego.</span><span class="sxs-lookup"><span data-stu-id="abf89-193">Remember - it takes a few minutes hello hello VMs toobe ready before hello load balancer starts toodistribute traffic toothem.</span></span> <span data-ttu-id="abf89-194">Olá aplicativo é exibido, incluindo o nome de host de saudação do hello VM balanceador de carga que Olá distribuído tooas de tráfego em Olá exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="abf89-194">hello app is displayed, including hello hostname of hello VM that hello load balancer distributed traffic tooas in hello following example:</span></span>

![Executar o aplicativo Node.js](./media/tutorial-load-balancer/running-nodejs-app.png)

<span data-ttu-id="abf89-196">Balanceador de carga toosee Olá distribuir tráfego entre todas as três VMs executando o aplicativo, você pode forçar atualização de seu navegador da web.</span><span class="sxs-lookup"><span data-stu-id="abf89-196">toosee hello load balancer distribute traffic across all three VMs running your app, you can force-refresh your web browser.</span></span>


## <a name="add-and-remove-vms"></a><span data-ttu-id="abf89-197">Adicionar e remover as VMs</span><span class="sxs-lookup"><span data-stu-id="abf89-197">Add and remove VMs</span></span>
<span data-ttu-id="abf89-198">Talvez seja necessário tooperform manutenção Olá VMs que executam seu aplicativo, como ao instalar atualizações do sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="abf89-198">You may need tooperform maintenance on hello VMs running your app, such as installing OS updates.</span></span> <span data-ttu-id="abf89-199">toodeal com o aumento no tráfego tooyour aplicativo, talvez seja necessário tooadd VMs adicionais.</span><span class="sxs-lookup"><span data-stu-id="abf89-199">toodeal with increased traffic tooyour app, you may need tooadd additional VMs.</span></span> <span data-ttu-id="abf89-200">Esta seção mostra como tooremove ou adicionar uma VM do balanceador de carga de saudação.</span><span class="sxs-lookup"><span data-stu-id="abf89-200">This section shows you how tooremove or add a VM from hello load balancer.</span></span>

### <a name="remove-a-vm-from-hello-load-balancer"></a><span data-ttu-id="abf89-201">Remover uma máquina virtual do balanceador de carga Olá</span><span class="sxs-lookup"><span data-stu-id="abf89-201">Remove a VM from hello load balancer</span></span>
<span data-ttu-id="abf89-202">Você pode remover uma máquina virtual do pool de endereços de back-end Olá com [remover az rede nic ip-config-pool de endereços](/cli/azure/network/nic/ip-config/address-pool#remove).</span><span class="sxs-lookup"><span data-stu-id="abf89-202">You can remove a VM from hello backend address pool with [az network nic ip-config address-pool remove](/cli/azure/network/nic/ip-config/address-pool#remove).</span></span> <span data-ttu-id="abf89-203">Olá remove de exemplo a seguir Olá NIC virtual para **myVM2** de *myLoadBalancer*:</span><span class="sxs-lookup"><span data-stu-id="abf89-203">hello following example removes hello virtual NIC for **myVM2** from *myLoadBalancer*:</span></span>

```azurecli-interactive 
az network nic ip-config address-pool remove \
    --resource-group myResourceGroupLoadBalancer \
    --nic-name myNic2 \
    --ip-config-name ipConfig1 \
    --lb-name myLoadBalancer \
    --address-pool myBackEndPool 
```

<span data-ttu-id="abf89-204">Balanceador de carga toosee Olá distribuir o tráfego entre Olá restantes duas VMs que executam seu aplicativo você pode forçar atualização de seu navegador da web.</span><span class="sxs-lookup"><span data-stu-id="abf89-204">toosee hello load balancer distribute traffic across hello remaining two VMs running your app you can force-refresh your web browser.</span></span> <span data-ttu-id="abf89-205">Agora você pode realizar uma manutenção em Olá VM, como instalar atualizações do sistema operacional ou executar uma reinicialização da VM.</span><span class="sxs-lookup"><span data-stu-id="abf89-205">You can now perform maintenance on hello VM, such as installing OS updates or performing a VM reboot.</span></span>

### <a name="add-a-vm-toohello-load-balancer"></a><span data-ttu-id="abf89-206">Adicionar um balanceador de carga de toohello VM</span><span class="sxs-lookup"><span data-stu-id="abf89-206">Add a VM toohello load balancer</span></span>
<span data-ttu-id="abf89-207">Depois de executar a manutenção VM, ou se você precisar de capacidade de tooexpand, você pode adicionar um pool de endereços de back-end do VM toohello com [adicionar az rede nic ip-config-pool de endereços](/cli/azure/network/nic/ip-config/address-pool#add).</span><span class="sxs-lookup"><span data-stu-id="abf89-207">After performing VM maintenance, or if you need tooexpand capacity, you can add a VM toohello backend address pool with [az network nic ip-config address-pool add](/cli/azure/network/nic/ip-config/address-pool#add).</span></span> <span data-ttu-id="abf89-208">Olá, exemplo a seguir adiciona Olá NIC virtual para **myVM2** muito*myLoadBalancer*:</span><span class="sxs-lookup"><span data-stu-id="abf89-208">hello following example adds hello virtual NIC for **myVM2** too*myLoadBalancer*:</span></span>

```azurecli-interactive 
az network nic ip-config address-pool add \
    --resource-group myResourceGroupLoadBalancer \
    --nic-name myNic2 \
    --ip-config-name ipConfig1 \
    --lb-name myLoadBalancer \
    --address-pool myBackEndPool
```


## <a name="next-steps"></a><span data-ttu-id="abf89-209">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="abf89-209">Next steps</span></span>
<span data-ttu-id="abf89-210">Neste tutorial, você criou um balanceador de carga e anexado VMs tooit.</span><span class="sxs-lookup"><span data-stu-id="abf89-210">In this tutorial, you created a load balancer and attached VMs tooit.</span></span> <span data-ttu-id="abf89-211">Você aprendeu como:</span><span class="sxs-lookup"><span data-stu-id="abf89-211">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="abf89-212">Criar um balanceador de carga do Azure</span><span class="sxs-lookup"><span data-stu-id="abf89-212">Create an Azure load balancer</span></span>
> * <span data-ttu-id="abf89-213">Criar uma investigação de integridade do balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="abf89-213">Create a load balancer health probe</span></span>
> * <span data-ttu-id="abf89-214">Criar regras de tráfego para o balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="abf89-214">Create load balancer traffic rules</span></span>
> * <span data-ttu-id="abf89-215">Use a nuvem init toocreate um aplicativo básico do Node. js</span><span class="sxs-lookup"><span data-stu-id="abf89-215">Use cloud-init toocreate a basic Node.js app</span></span>
> * <span data-ttu-id="abf89-216">Criar máquinas virtuais e anexar tooa balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="abf89-216">Create virtual machines and attach tooa load balancer</span></span>
> * <span data-ttu-id="abf89-217">Exibir um balanceador de carga em ação</span><span class="sxs-lookup"><span data-stu-id="abf89-217">View a load balancer in action</span></span>
> * <span data-ttu-id="abf89-218">Adicionar e remover as VMs de um balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="abf89-218">Add and remove VMs from a load balancer</span></span>

<span data-ttu-id="abf89-219">Toohello toolearn de tutorial Avançar adiantar mais sobre os componentes de rede virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="abf89-219">Advance toohello next tutorial toolearn more about Azure virtual network components.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="abf89-220">Gerencie VMs e redes virtuais</span><span class="sxs-lookup"><span data-stu-id="abf89-220">Manage VMs and virtual networks</span></span>](tutorial-virtual-network.md)
