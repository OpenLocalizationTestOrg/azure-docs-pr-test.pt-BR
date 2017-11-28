---
title: aaaCreate um ambiente completo de Linux com hello 1.0 da CLI do Azure | Microsoft Docs
description: "Crie armazenamento, uma VM do Linux, uma rede virtual e sub-rede, um balanceador de carga, uma NIC, um IP público e um grupo de segurança de rede, tudo a partir de saudação Terra usando Olá 1.0 da CLI do Azure."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4ba4060b-ce95-4747-a735-1d7c68597a1a
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: 7fe00e138704fe9c9a1c9b87a7dd1afd6174e527
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-complete-linux-environment-with-hello-azure-cli-10"></a><span data-ttu-id="c9703-103">Criar um ambiente completo do Linux com hello 1.0 da CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="c9703-103">Create a complete Linux environment with hello Azure CLI 1.0</span></span>
<span data-ttu-id="c9703-104">Neste artigo, vamos criar uma rede simples com um balanceador de carga e com um par de VMs úteis para desenvolvimento e computação simples.</span><span class="sxs-lookup"><span data-stu-id="c9703-104">In this article, we build a simple network with a load balancer and a pair of VMs that are useful for development and simple computing.</span></span> <span data-ttu-id="c9703-105">Percorremos o processo de saudação pelo comando, até que você tiver dois ativa, seguro toowhich de VMs do Linux, que você pode se conectar de em qualquer lugar em Olá da Internet.</span><span class="sxs-lookup"><span data-stu-id="c9703-105">We walk through hello process command by command, until you have two working, secure Linux VMs toowhich you can connect from anywhere on hello Internet.</span></span> <span data-ttu-id="c9703-106">Em seguida, você pode mover em ambientes e redes complexas toomore.</span><span class="sxs-lookup"><span data-stu-id="c9703-106">Then you can move on toomore complex networks and environments.</span></span>

<span data-ttu-id="c9703-107">Caminho hello, você aprenderá sobre hierarquia de dependência de saudação que modelo de implantação do Gerenciador de recursos de saudação lhe e sobre quanta energia fornece.</span><span class="sxs-lookup"><span data-stu-id="c9703-107">Along hello way, you learn about hello dependency hierarchy that hello Resource Manager deployment model gives you, and about how much power it provides.</span></span> <span data-ttu-id="c9703-108">Depois de ver como o sistema de saudação é criado, você poderá recriá-lo muito mais rapidamente usando [modelos do Azure Resource Manager](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c9703-108">After you see how hello system is built, you can rebuild it much more quickly by using [Azure Resource Manager templates](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="c9703-109">Além disso, depois que você saiba como partes de saudação do seu ambiente se encaixam, criando modelos tooautomate-los se torna mais fácil.</span><span class="sxs-lookup"><span data-stu-id="c9703-109">Also, after you learn how hello parts of your environment fit together, creating templates tooautomate them becomes easier.</span></span>

<span data-ttu-id="c9703-110">Olá ambiente contém:</span><span class="sxs-lookup"><span data-stu-id="c9703-110">hello environment contains:</span></span>

* <span data-ttu-id="c9703-111">Duas VMs dentro de um conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="c9703-111">Two VMs inside an availability set.</span></span>
* <span data-ttu-id="c9703-112">Um balanceador de carga com uma regra de balanceamento de carga na porta 80.</span><span class="sxs-lookup"><span data-stu-id="c9703-112">A load balancer with a load-balancing rule on port 80.</span></span>
* <span data-ttu-id="c9703-113">O grupo de segurança de rede (NSG) regras tooprotect sua VM de tráfego não desejado.</span><span class="sxs-lookup"><span data-stu-id="c9703-113">Network security group (NSG) rules tooprotect your VM from unwanted traffic.</span></span>

<span data-ttu-id="c9703-114">toocreate nesse ambiente personalizado, você precisa hello mais recente [Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) no modo do Gerenciador de recursos (`azure config mode arm`).</span><span class="sxs-lookup"><span data-stu-id="c9703-114">toocreate this custom environment, you need hello latest [Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) in Resource Manager mode (`azure config mode arm`).</span></span> <span data-ttu-id="c9703-115">Você também precisará de uma ferramenta de análise de JSON.</span><span class="sxs-lookup"><span data-stu-id="c9703-115">You also need a JSON parsing tool.</span></span> <span data-ttu-id="c9703-116">Este exemplo usa [jq](https://stedolan.github.io/jq/).</span><span class="sxs-lookup"><span data-stu-id="c9703-116">This example uses [jq](https://stedolan.github.io/jq/).</span></span>


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="c9703-117">Tarefa de saudação do CLI versões toocomplete</span><span class="sxs-lookup"><span data-stu-id="c9703-117">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="c9703-118">Você pode concluir a tarefa hello usando uma saudação versões da CLI a seguir:</span><span class="sxs-lookup"><span data-stu-id="c9703-118">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="c9703-119">[1.0 de CLI do Azure](#quick-commands) – nosso CLI para Olá clássico e o recurso de gerenciamento modelos de implantação (Este artigo)</span><span class="sxs-lookup"><span data-stu-id="c9703-119">[Azure CLI 1.0](#quick-commands) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="c9703-120">[2.0 do CLI do Azure](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -nossa próxima geração CLI para o modelo de implantação do gerenciamento de recursos de saudação</span><span class="sxs-lookup"><span data-stu-id="c9703-120">[Azure CLI 2.0](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="c9703-121">Comandos rápidos</span><span class="sxs-lookup"><span data-stu-id="c9703-121">Quick commands</span></span>
<span data-ttu-id="c9703-122">Se você precisar tooquickly realizar tarefa hello, Olá Olá de detalhes da seção a seguir base tooupload comandos tooAzure uma VM.</span><span class="sxs-lookup"><span data-stu-id="c9703-122">If you need tooquickly accomplish hello task, hello following section details hello base commands tooupload a VM tooAzure.</span></span> <span data-ttu-id="c9703-123">Obter mais informações e o contexto para cada etapa pode ser encontrada no restante de saudação do documento hello, iniciando [aqui](#detailed-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="c9703-123">More detailed information and context for each step can be found in hello rest of hello document, starting [here](#detailed-walkthrough).</span></span>

<span data-ttu-id="c9703-124">Certifique-se de que você tenha [hello Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) conectado e usando o modo do Gerenciador de recursos:</span><span class="sxs-lookup"><span data-stu-id="c9703-124">Make sure that you have [hello Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="c9703-125">Em Olá exemplos a seguir, substitua os nomes de parâmetro de exemplo com seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="c9703-125">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="c9703-126">Os nomes de parâmetro de exemplo incluem `myResourceGroup`, `mystorageaccount` e `myVM`.</span><span class="sxs-lookup"><span data-stu-id="c9703-126">Example parameter names include `myResourceGroup`, `mystorageaccount`, and `myVM`.</span></span>

<span data-ttu-id="c9703-127">Crie grupo de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="c9703-127">Create hello resource group.</span></span> <span data-ttu-id="c9703-128">Olá, exemplo a seguir cria um grupo de recursos denominado `myResourceGroup` em Olá `westeurope` local:</span><span class="sxs-lookup"><span data-stu-id="c9703-128">hello following example creates a resource group named `myResourceGroup` in hello `westeurope` location:</span></span>

```azurecli
azure group create -n myResourceGroup -l westeurope
```

<span data-ttu-id="c9703-129">Verifique se o grupo de recursos hello usando o analisador JSON hello:</span><span class="sxs-lookup"><span data-stu-id="c9703-129">Verify hello resource group by using hello JSON parser:</span></span>

```azurecli
azure group show myResourceGroup --json | jq '.'
```

<span data-ttu-id="c9703-130">Crie conta de armazenamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="c9703-130">Create hello storage account.</span></span> <span data-ttu-id="c9703-131">Olá, exemplo a seguir cria uma conta de armazenamento denominada `mystorageaccount`.</span><span class="sxs-lookup"><span data-stu-id="c9703-131">hello following example creates a storage account named `mystorageaccount`.</span></span> <span data-ttu-id="c9703-132">(o nome de conta de armazenamento Olá deve ser exclusivo, portanto, fornecer seu próprio nome exclusivo.)</span><span class="sxs-lookup"><span data-stu-id="c9703-132">(hello storage account name must be unique, so provide your own unique name.)</span></span>

```azurecli
azure storage account create -g myResourceGroup -l westeurope \
  --kind Storage --sku-name GRS mystorageaccount
```

<span data-ttu-id="c9703-133">Verifique se a conta de armazenamento de saudação usando o analisador JSON de saudação:</span><span class="sxs-lookup"><span data-stu-id="c9703-133">Verify hello storage account by using hello JSON parser:</span></span>

```azurecli
azure storage account show -g myResourceGroup mystorageaccount --json | jq '.'
```

<span data-ttu-id="c9703-134">Crie rede virtual hello.</span><span class="sxs-lookup"><span data-stu-id="c9703-134">Create hello virtual network.</span></span> <span data-ttu-id="c9703-135">Olá, exemplo a seguir cria uma rede virtual denominada `myVnet`:</span><span class="sxs-lookup"><span data-stu-id="c9703-135">hello following example creates a virtual network named `myVnet`:</span></span>

```azurecli
azure network vnet create -g myResourceGroup -l westeurope\
  -n myVnet -a 192.168.0.0/16
```

<span data-ttu-id="c9703-136">Crie uma sub-rede.</span><span class="sxs-lookup"><span data-stu-id="c9703-136">Create a subnet.</span></span> <span data-ttu-id="c9703-137">Olá, exemplo a seguir cria uma sub-rede denominada `mySubnet`:</span><span class="sxs-lookup"><span data-stu-id="c9703-137">hello following example creates a subnet named `mySubnet`:</span></span>

```azurecli
azure network vnet subnet create -g myResourceGroup \
  -e myVnet -n mySubnet -a 192.168.1.0/24
```

<span data-ttu-id="c9703-138">Verificar Olá uma rede virtual e sub-rede usando o analisador JSON hello:</span><span class="sxs-lookup"><span data-stu-id="c9703-138">Verify hello virtual network and subnet by using hello JSON parser:</span></span>

```azurecli
azure network vnet show myResourceGroup myVnet --json | jq '.'
```

<span data-ttu-id="c9703-139">Crie um IP público.</span><span class="sxs-lookup"><span data-stu-id="c9703-139">Create a public IP.</span></span> <span data-ttu-id="c9703-140">Olá, exemplo a seguir cria um IP público denominado `myPublicIP` com nome DNS de saudação do `mypublicdns`.</span><span class="sxs-lookup"><span data-stu-id="c9703-140">hello following example creates a public IP named `myPublicIP` with hello DNS name of `mypublicdns`.</span></span> <span data-ttu-id="c9703-141">(o nome DNS Olá deve ser exclusivo, para fornecer seu próprio nome exclusivo.)</span><span class="sxs-lookup"><span data-stu-id="c9703-141">(hello DNS name must be unique, so provide your own unique name.)</span></span>

```azurecli
azure network public-ip create -g myResourceGroup -l westeurope \
  -n myPublicIP  -d mypublicdns -a static -i 4
```

<span data-ttu-id="c9703-142">Crie o balanceador de carga de saudação.</span><span class="sxs-lookup"><span data-stu-id="c9703-142">Create hello load balancer.</span></span> <span data-ttu-id="c9703-143">Olá, exemplo a seguir cria um balanceador de carga chamado `myLoadBalancer`:</span><span class="sxs-lookup"><span data-stu-id="c9703-143">hello following example creates a load balancer named `myLoadBalancer`:</span></span>

```azurecli
azure network lb create -g myResourceGroup -l westeurope -n myLoadBalancer
```

<span data-ttu-id="c9703-144">Criar um pool IP de front-end para o balanceador de carga hello e associar IP público hello.</span><span class="sxs-lookup"><span data-stu-id="c9703-144">Create a front-end IP pool for hello load balancer, and associate hello public IP.</span></span> <span data-ttu-id="c9703-145">Olá, exemplo a seguir cria um pool IP de front-end denominado `mySubnetPool`:</span><span class="sxs-lookup"><span data-stu-id="c9703-145">hello following example creates a front-end IP pool named `mySubnetPool`:</span></span>

```azurecli
azure network lb frontend-ip create -g myResourceGroup -l myLoadBalancer \
  -i myPublicIP -n myFrontEndPool
```

<span data-ttu-id="c9703-146">Crie pool IP de back-end Olá Olá balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="c9703-146">Create hello back-end IP pool for hello load balancer.</span></span> <span data-ttu-id="c9703-147">Olá, exemplo a seguir cria um pool IP de back-end denominado `myBackEndPool`:</span><span class="sxs-lookup"><span data-stu-id="c9703-147">hello following example creates a back-end IP pool named `myBackEndPool`:</span></span>

```azurecli
azure network lb address-pool create -g myResourceGroup -l myLoadBalancer \
  -n myBackEndPool
```

<span data-ttu-id="c9703-148">Crie regras NAT (conversão) de endereço Olá balanceador de carga de rede de entrada do SSH.</span><span class="sxs-lookup"><span data-stu-id="c9703-148">Create SSH inbound network address translation (NAT) rules for hello load balancer.</span></span> <span data-ttu-id="c9703-149">Olá, exemplo a seguir cria duas regras de Balanceador de carga, `myLoadBalancerRuleSSH1` e `myLoadBalancerRuleSSH2`:</span><span class="sxs-lookup"><span data-stu-id="c9703-149">hello following example creates two load balancer rules, `myLoadBalancerRuleSSH1` and `myLoadBalancerRuleSSH2`:</span></span>

```azurecli
azure network lb inbound-nat-rule create -g myResourceGroup -l myLoadBalancer \
  -n myLoadBalancerRuleSSH1 -p tcp -f 4222 -b 22
azure network lb inbound-nat-rule create -g myResourceGroup -l myLoadBalancer \
  -n myLoadBalancerRuleSSH2 -p tcp -f 4223 -b 22
```

<span data-ttu-id="c9703-150">Olá web de criar regras de NAT de entrada para Olá balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="c9703-150">Create hello web inbound NAT rules for hello load balancer.</span></span> <span data-ttu-id="c9703-151">Olá, exemplo a seguir cria uma regra de Balanceador de carga denominada `myLoadBalancerRuleWeb`:</span><span class="sxs-lookup"><span data-stu-id="c9703-151">hello following example creates a load balancer rule named `myLoadBalancerRuleWeb`:</span></span>

```azurecli
azure network lb rule create -g myResourceGroup -l myLoadBalancer \
  -n myLoadBalancerRuleWeb -p tcp -f 80 -b 80 \
  -t myFrontEndPool -o myBackEndPool
```

<span data-ttu-id="c9703-152">Crie hello investigação de integridade do balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="c9703-152">Create hello load balancer health probe.</span></span> <span data-ttu-id="c9703-153">Olá, exemplo a seguir cria um teste TCP chamado `myHealthProbe`:</span><span class="sxs-lookup"><span data-stu-id="c9703-153">hello following example creates a TCP probe named `myHealthProbe`:</span></span>

```azurecli
azure network lb probe create -g myResourceGroup -l myLoadBalancer \
  -n myHealthProbe -p "tcp" -i 15 -c 4
```

<span data-ttu-id="c9703-154">Verifique o balanceador de carga hello, pools de IP e as regras de NAT usando o analisador JSON de saudação:</span><span class="sxs-lookup"><span data-stu-id="c9703-154">Verify hello load balancer, IP pools, and NAT rules by using hello JSON parser:</span></span>

```azurecli
azure network lb show -g myResourceGroup -n myLoadBalancer --json | jq '.'
```

<span data-ttu-id="c9703-155">Crie hello primeira placa de rede (NIC).</span><span class="sxs-lookup"><span data-stu-id="c9703-155">Create hello first network interface card (NIC).</span></span> <span data-ttu-id="c9703-156">Substituir saudação `#####-###-###` seções com sua ID de assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="c9703-156">Replace hello `#####-###-###` sections with your own Azure subscription ID.</span></span> <span data-ttu-id="c9703-157">Sua assinatura ID é observado na saída de saudação do **jq** quando você examinar recursos Olá que você está criando.</span><span class="sxs-lookup"><span data-stu-id="c9703-157">Your subscription ID is noted in hello output of **jq** when you examine hello resources you are creating.</span></span> <span data-ttu-id="c9703-158">Você também pode exibir sua ID de assinatura com `azure account list`.</span><span class="sxs-lookup"><span data-stu-id="c9703-158">You can also view your subscription ID with `azure account list`.</span></span>

<span data-ttu-id="c9703-159">Olá, exemplo a seguir cria uma NIC chamada `myNic1`:</span><span class="sxs-lookup"><span data-stu-id="c9703-159">hello following example creates a NIC named `myNic1`:</span></span>

```azurecli
azure network nic create -g myResourceGroup -l westeurope \
  -n myNic1 -m myVnet -k mySubnet \
  -d "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool" \
  -e "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1"
```

<span data-ttu-id="c9703-160">Criar o segundo NIC de saudação.</span><span class="sxs-lookup"><span data-stu-id="c9703-160">Create hello second NIC.</span></span> <span data-ttu-id="c9703-161">Olá, exemplo a seguir cria uma NIC chamada `myNic2`:</span><span class="sxs-lookup"><span data-stu-id="c9703-161">hello following example creates a NIC named `myNic2`:</span></span>

```azurecli
azure network nic create -g myResourceGroup -l westeurope \
  -n myNic2 -m myVnet -k mySubnet \
  -d "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool" \
  -e "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2"
```

<span data-ttu-id="c9703-162">Verificar Olá duas NICs usando o analisador JSON hello:</span><span class="sxs-lookup"><span data-stu-id="c9703-162">Verify hello two NICs by using hello JSON parser:</span></span>

```azurecli
azure network nic show myResourceGroup myNic1 --json | jq '.'
azure network nic show myResourceGroup myNic2 --json | jq '.'
```

<span data-ttu-id="c9703-163">Crie grupo de segurança de rede de saudação.</span><span class="sxs-lookup"><span data-stu-id="c9703-163">Create hello network security group.</span></span> <span data-ttu-id="c9703-164">Olá, exemplo a seguir cria um grupo de segurança de rede denominado `myNetworkSecurityGroup`:</span><span class="sxs-lookup"><span data-stu-id="c9703-164">hello following example creates a network security group named `myNetworkSecurityGroup`:</span></span>

```azurecli
azure network nsg create -g myResourceGroup -l westeurope \
  -n myNetworkSecurityGroup
```

<span data-ttu-id="c9703-165">Adicione duas regras de entrada para o grupo de segurança de rede hello.</span><span class="sxs-lookup"><span data-stu-id="c9703-165">Add two inbound rules for hello network security group.</span></span> <span data-ttu-id="c9703-166">Olá, exemplo a seguir cria duas regras, `myNetworkSecurityGroupRuleSSH` e `myNetworkSecurityGroupRuleHTTP`:</span><span class="sxs-lookup"><span data-stu-id="c9703-166">hello following example creates two rules, `myNetworkSecurityGroupRuleSSH` and `myNetworkSecurityGroupRuleHTTP`:</span></span>

```azurecli
azure network nsg rule create -p tcp -r inbound -y 1000 -u 22 -c allow \
  -g myResourceGroup -a myNetworkSecurityGroup -n myNetworkSecurityGroupRuleSSH
azure network nsg rule create -p tcp -r inbound -y 1001 -u 80 -c allow \
  -g myResourceGroup -a myNetworkSecurityGroup -n myNetworkSecurityGroupRuleHTTP
```

<span data-ttu-id="c9703-167">Verifique se o grupo de segurança de rede hello e as regras de entrada usando o analisador JSON hello:</span><span class="sxs-lookup"><span data-stu-id="c9703-167">Verify hello network security group and inbound rules by using hello JSON parser:</span></span>

```azurecli
azure network nsg show -g myResourceGroup -n myNetworkSecurityGroup --json | jq '.'
```

<span data-ttu-id="c9703-168">Associação de segurança de rede Olá toohello duas NICs de grupo:</span><span class="sxs-lookup"><span data-stu-id="c9703-168">Bind hello network security group toohello two NICs:</span></span>

```azurecli
azure network nic set -g myResourceGroup -o myNetworkSecurityGroup -n myNic1
azure network nic set -g myResourceGroup -o myNetworkSecurityGroup -n myNic2
```

<span data-ttu-id="c9703-169">Crie conjunto de disponibilidade de saudação.</span><span class="sxs-lookup"><span data-stu-id="c9703-169">Create hello availability set.</span></span> <span data-ttu-id="c9703-170">Olá, exemplo a seguir cria um conjunto nomeada de disponibilidade `myAvailabilitySet`:</span><span class="sxs-lookup"><span data-stu-id="c9703-170">hello following example creates an availability set named `myAvailabilitySet`:</span></span>

```azurecli
azure availset create -g myResourceGroup -l westeurope -n myAvailabilitySet
```

<span data-ttu-id="c9703-171">Criar hello primeira VM do Linux.</span><span class="sxs-lookup"><span data-stu-id="c9703-171">Create hello first Linux VM.</span></span> <span data-ttu-id="c9703-172">Olá, exemplo a seguir cria uma VM denominada `myVM1`:</span><span class="sxs-lookup"><span data-stu-id="c9703-172">hello following example creates a VM named `myVM1`:</span></span>

```azurecli
azure vm create \
    --resource-group myResourceGroup \
    --name myVM1 \
    --location westeurope \
    --os-type linux \
    --availset-name myAvailabilitySet \
    --nic-name myNic1 \
    --vnet-name myVnet \
    --vnet-subnet-name mySubnet \
    --storage-account-name mystorageaccount \
    --image-urn canonical:UbuntuServer:16.04.0-LTS:latest \
    --ssh-publickey-file ~/.ssh/id_rsa.pub \
    --admin-username azureuser
```

<span data-ttu-id="c9703-173">Criar hello segundo VM do Linux.</span><span class="sxs-lookup"><span data-stu-id="c9703-173">Create hello second Linux VM.</span></span> <span data-ttu-id="c9703-174">Olá, exemplo a seguir cria uma VM denominada `myVM2`:</span><span class="sxs-lookup"><span data-stu-id="c9703-174">hello following example creates a VM named `myVM2`:</span></span>

```azurecli
azure vm create \
    --resource-group myResourceGroup \
    --name myVM2 \
    --location westeurope \
    --os-type linux \
    --availset-name myAvailabilitySet \
    --nic-name myNic2 \
    --vnet-name myVnet \
    --vnet-subnet-name mySubnet \
    --storage-account-name mystorageaccount \
    --image-urn canonical:UbuntuServer:16.04.0-LTS:latest \
    --ssh-publickey-file ~/.ssh/id_rsa.pub \
    --admin-username azureuser
```

<span data-ttu-id="c9703-175">Use Olá JSON analisador tooverify tudo que foi criado:</span><span class="sxs-lookup"><span data-stu-id="c9703-175">Use hello JSON parser tooverify that everything that was built:</span></span>

```azurecli
azure vm show -g myResourceGroup -n myVM1 --json | jq '.'
azure vm show -g myResourceGroup -n myVM2 --json | jq '.'
```

<span data-ttu-id="c9703-176">Exporte seu novo ambiente tooa tooquickly recriar novas instâncias do modelo:</span><span class="sxs-lookup"><span data-stu-id="c9703-176">Export your new environment tooa template tooquickly re-create new instances:</span></span>

```azurecli
azure group export myResourceGroup
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="c9703-177">Passo a passo detalhado</span><span class="sxs-lookup"><span data-stu-id="c9703-177">Detailed walkthrough</span></span>
<span data-ttu-id="c9703-178">Olá etapas detalhadas que sigam explicam o que cada comando é fazer à medida que seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="c9703-178">hello detailed steps that follow explain what each command is doing as you build out your environment.</span></span> <span data-ttu-id="c9703-179">Esses conceitos são úteis durante a criação de seus próprios ambientes personalizados para desenvolvimento ou produção.</span><span class="sxs-lookup"><span data-stu-id="c9703-179">These concepts are helpful when you build your own custom environments for development or production.</span></span>

<span data-ttu-id="c9703-180">Certifique-se de que você tenha [hello Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) conectado e usando o modo do Gerenciador de recursos:</span><span class="sxs-lookup"><span data-stu-id="c9703-180">Make sure that you have [hello Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) logged in and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="c9703-181">Em Olá exemplos a seguir, substitua os nomes de parâmetro de exemplo com seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="c9703-181">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="c9703-182">Os nomes de parâmetro de exemplo incluem `myResourceGroup`, `mystorageaccount` e `myVM`.</span><span class="sxs-lookup"><span data-stu-id="c9703-182">Example parameter names include `myResourceGroup`, `mystorageaccount`, and `myVM`.</span></span>

## <a name="create-resource-groups-and-choose-deployment-locations"></a><span data-ttu-id="c9703-183">Criar grupos de recursos e escolher locais de implantação</span><span class="sxs-lookup"><span data-stu-id="c9703-183">Create resource groups and choose deployment locations</span></span>
<span data-ttu-id="c9703-184">Grupos de recursos do Azure são entidades de lógica de implantação que contêm informações e metadados tooenable Olá lógico gerenciamento de configuração de implantações de recursos.</span><span class="sxs-lookup"><span data-stu-id="c9703-184">Azure resource groups are logical deployment entities that contain configuration information and metadata tooenable hello logical management of resource deployments.</span></span> <span data-ttu-id="c9703-185">Olá, exemplo a seguir cria um grupo de recursos denominado `myResourceGroup` em Olá `westeurope` local:</span><span class="sxs-lookup"><span data-stu-id="c9703-185">hello following example creates a resource group named `myResourceGroup` in hello `westeurope` location:</span></span>

```azurecli
azure group create --name myResourceGroup --location westeurope
```

<span data-ttu-id="c9703-186">Saída:</span><span class="sxs-lookup"><span data-stu-id="c9703-186">Output:</span></span>

```azurecli                        
info:    Executing command group create
+ Getting resource group myResourceGroup
+ Creating resource group myResourceGroup
info:    Created resource group myResourceGroup
data:    Id:                  /subscriptions/guid/resourceGroups/myResourceGroup
data:    Name:                myResourceGroup
data:    Location:            westeurope
data:    Provisioning State:  Succeeded
data:    Tags: null
data:
info:    group create command OK
```

## <a name="create-a-storage-account"></a><span data-ttu-id="c9703-187">Criar uma conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="c9703-187">Create a storage account</span></span>
<span data-ttu-id="c9703-188">É necessário contas de armazenamento para os discos VM e para os discos de dados adicionais que você deseja tooadd.</span><span class="sxs-lookup"><span data-stu-id="c9703-188">You need storage accounts for your VM disks and for any additional data disks that you want tooadd.</span></span> <span data-ttu-id="c9703-189">Você cria contas de armazenamento quase que imediatamente depois de criar grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="c9703-189">You create storage accounts almost immediately after you create resource groups.</span></span>

<span data-ttu-id="c9703-190">Aqui usamos Olá `azure storage account create` comando, passando local Olá da conta hello, grupo de recursos de saudação que controla a ele e o tipo de saudação de suporte de armazenamento que você deseja.</span><span class="sxs-lookup"><span data-stu-id="c9703-190">Here we use hello `azure storage account create` command, passing hello location of hello account, hello resource group that controls it, and hello type of storage support you want.</span></span> <span data-ttu-id="c9703-191">Olá, exemplo a seguir cria uma conta de armazenamento denominada `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="c9703-191">hello following example creates a storage account named `mystorageaccount`:</span></span>

```azurecli
azure storage account create \  
  --location westeurope \
  --resource-group myResourceGroup \
  --kind Storage --sku-name GRS \
  mystorageaccount
```

<span data-ttu-id="c9703-192">Saída:</span><span class="sxs-lookup"><span data-stu-id="c9703-192">Output:</span></span>

```azurecli
info:    Executing command storage account create
+ Creating storage account
info:    storage account create command OK
```

<span data-ttu-id="c9703-193">tooexamine nosso recurso de grupo usando Olá `azure group show` command, vamos usar Olá [jq](https://stedolan.github.io/jq/) ferramenta juntamente com hello `--json` opção CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="c9703-193">tooexamine our resource group by using hello `azure group show` command, let's use hello [jq](https://stedolan.github.io/jq/) tool along with hello `--json` Azure CLI option.</span></span> <span data-ttu-id="c9703-194">(Você pode usar **jsawk** ou qualquer biblioteca de idioma que você preferir tooparse Olá JSON.)</span><span class="sxs-lookup"><span data-stu-id="c9703-194">(You can use **jsawk** or any language library you prefer tooparse hello JSON.)</span></span>

```azurecli
azure group show myResourceGroup --json | jq '.'
```

<span data-ttu-id="c9703-195">Saída:</span><span class="sxs-lookup"><span data-stu-id="c9703-195">Output:</span></span>

```json
{
  "tags": {},
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup",
  "name": "myResourceGroup",
  "provisioningState": "Succeeded",
  "location": "westeurope",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "resources": [
    {
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Storage/storageAccounts/mystorageaccount",
      "name": "mystorageaccount",
      "type": "storageAccounts",
      "location": "westeurope",
      "tags": null
    }
  ],
  "permissions": [
    {
      "actions": [
        "*"
      ],
      "notActions": []
    }
  ]
}
```

<span data-ttu-id="c9703-196">conta de armazenamento tooinvestigate hello usando Olá CLI, é necessário primeiro chaves e nomes de conta tooset hello.</span><span class="sxs-lookup"><span data-stu-id="c9703-196">tooinvestigate hello storage account by using hello CLI, you first need tooset hello account names and keys.</span></span> <span data-ttu-id="c9703-197">Substitua o nome de saudação da conta de armazenamento Olá Olá exemplo com um nome que você escolher a seguir:</span><span class="sxs-lookup"><span data-stu-id="c9703-197">Replace hello name of hello storage account in hello following example with a name that you choose:</span></span>

```bash
export AZURE_STORAGE_CONNECTION_STRING="$(azure storage account connectionstring show mystorageaccount --resource-group myResourceGroup --json | jq -r '.string')"
```

<span data-ttu-id="c9703-198">Em seguida, você poderá exibir as informações de armazenamento facilmente:</span><span class="sxs-lookup"><span data-stu-id="c9703-198">Then you can view your storage information easily:</span></span>

```azurecli
azure storage container list
```

<span data-ttu-id="c9703-199">Saída:</span><span class="sxs-lookup"><span data-stu-id="c9703-199">Output:</span></span>

```azurecli
info:    Executing command storage container list
+ Getting storage containers
data:    Name  Public-Access  Last-Modified
data:    ----  -------------  -----------------------------
data:    vhds  Off            Sun, 27 Sep 2015 19:03:54 GMT
info:    storage container list command OK
```

## <a name="create-a-virtual-network-and-subnet"></a><span data-ttu-id="c9703-200">Criar a rede virtual e a sub-rede</span><span class="sxs-lookup"><span data-stu-id="c9703-200">Create a virtual network and subnet</span></span>
<span data-ttu-id="c9703-201">Em seguida você vai tooneed toocreate uma rede virtual em execução no Azure e uma sub-rede na qual você pode criar suas VMs.</span><span class="sxs-lookup"><span data-stu-id="c9703-201">Next you're going tooneed toocreate a virtual network running in Azure and a subnet in which you can create your VMs.</span></span> <span data-ttu-id="c9703-202">Olá, exemplo a seguir cria uma rede virtual denominada `myVnet` com hello `192.168.0.0/16` prefixo de endereço:</span><span class="sxs-lookup"><span data-stu-id="c9703-202">hello following example creates a virtual network named `myVnet` with hello `192.168.0.0/16` address prefix:</span></span>

```azurecli
azure network vnet create --resource-group myResourceGroup --location westeurope \
  --name myVnet --address-prefixes 192.168.0.0/16
```

<span data-ttu-id="c9703-203">Saída:</span><span class="sxs-lookup"><span data-stu-id="c9703-203">Output:</span></span>

```azurecli
info:    Executing command network vnet create
+ Looking up virtual network "myVnet"
+ Creating virtual network "myVnet"
+ Loading virtual network state
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet
data:    Name                            : myVnet
data:    Type                            : Microsoft.Network/virtualNetworks
data:    Location                        : westeurope
data:    ProvisioningState               : Succeeded
data:    Address prefixes:
data:      192.168.0.0/16
info:    network vnet create command OK
```

<span data-ttu-id="c9703-204">Novamente, vamos usar a opção – json Olá `azure group show` e `jq` toosee como estamos criando nossos recursos.</span><span class="sxs-lookup"><span data-stu-id="c9703-204">Again, let's use hello --json option of `azure group show` and `jq` toosee how we're building our resources.</span></span> <span data-ttu-id="c9703-205">Agora, temos um recurso `storageAccounts` e um recurso `virtualNetworks`.</span><span class="sxs-lookup"><span data-stu-id="c9703-205">We now have a `storageAccounts` resource and a `virtualNetworks` resource.</span></span>  

```azurecli
azure group show myResourceGroup --json | jq '.'
```

<span data-ttu-id="c9703-206">Saída:</span><span class="sxs-lookup"><span data-stu-id="c9703-206">Output:</span></span>

```json
{
  "tags": {},
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup",
  "name": "myResourceGroup",
  "provisioningState": "Succeeded",
  "location": "westeurope",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "resources": [
    {
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet",
      "name": "myVnet",
      "type": "virtualNetworks",
      "location": "westeurope",
      "tags": null
    },
    {
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Storage/storageAccounts/mystorageaccount",
      "name": "mystorageaccount",
      "type": "storageAccounts",
      "location": "westeurope",
      "tags": null
    }
  ],
  "permissions": [
    {
      "actions": [
        "*"
      ],
      "notActions": []
    }
  ]
}
```

<span data-ttu-id="c9703-207">Agora vamos criar uma sub-rede em Olá `myVnet` rede virtual no qual Olá VMs são implantadas.</span><span class="sxs-lookup"><span data-stu-id="c9703-207">Now let's create a subnet in hello `myVnet` virtual network into which hello VMs are deployed.</span></span> <span data-ttu-id="c9703-208">Usamos Olá `azure network vnet subnet create` comando, junto com os recursos de saudação já criamos: Olá `myResourceGroup` grupo de recursos e hello `myVnet` rede virtual.</span><span class="sxs-lookup"><span data-stu-id="c9703-208">We use hello `azure network vnet subnet create` command, along with hello resources we've already created: hello `myResourceGroup` resource group and hello `myVnet` virtual network.</span></span> <span data-ttu-id="c9703-209">Saudação de exemplo a seguir, adicionamos sub-rede Olá denominada `mySubnet` com prefixo de endereço da sub-rede Olá `192.168.1.0/24`:</span><span class="sxs-lookup"><span data-stu-id="c9703-209">In hello following example, we add hello subnet named `mySubnet` with hello subnet address prefix of `192.168.1.0/24`:</span></span>

```azurecli
azure network vnet subnet create --resource-group myResourceGroup \
  --vnet-name myVnet --name mySubnet --address-prefix 192.168.1.0/24
```

<span data-ttu-id="c9703-210">Saída:</span><span class="sxs-lookup"><span data-stu-id="c9703-210">Output:</span></span>

```azurecli
info:    Executing command network vnet subnet create
+ Looking up hello subnet "mySubnet"
+ Creating subnet "mySubnet"
+ Looking up hello subnet "mySubnet"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet
data:    Type                            : Microsoft.Network/virtualNetworks/subnets
data:    ProvisioningState               : Succeeded
data:    Name                            : mySubnet
data:    Address prefix                  : 192.168.1.0/24
data:
info:    network vnet subnet create command OK
```

<span data-ttu-id="c9703-211">Como sub-rede Olá é logicamente dentro da rede virtual hello, procuramos informações de sub-rede Olá com um comando ligeiramente diferente.</span><span class="sxs-lookup"><span data-stu-id="c9703-211">Because hello subnet is logically inside hello virtual network, we look for hello subnet information with a slightly different command.</span></span> <span data-ttu-id="c9703-212">comando Olá usamos é `azure network vnet show`, mas continuar a saída JSON de saudação tooexamine usando `jq`.</span><span class="sxs-lookup"><span data-stu-id="c9703-212">hello command we use is `azure network vnet show`, but we continue tooexamine hello JSON output by using `jq`.</span></span>

```azurecli
azure network vnet show myResourceGroup myVnet --json | jq '.'
```

<span data-ttu-id="c9703-213">Saída:</span><span class="sxs-lookup"><span data-stu-id="c9703-213">Output:</span></span>

```json
{
  "subnets": [
    {
      "ipConfigurations": [],
      "addressPrefix": "192.168.1.0/24",
      "provisioningState": "Succeeded",
      "name": "mySubnet",
      "etag": "W/\"974f3e2c-028e-4b35-832b-a4b16ad25eb6\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet"
    }
  ],
  "tags": {},
  "addressSpace": {
    "addressPrefixes": [
      "192.168.0.0/16"
    ]
  },
  "dhcpOptions": {
    "dnsServers": []
  },
  "provisioningState": "Succeeded",
  "etag": "W/\"974f3e2c-028e-4b35-832b-a4b16ad25eb6\"",
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet",
  "name": "myVnet",
  "location": "westeurope"
}
```

## <a name="create-a-public-ip-address"></a><span data-ttu-id="c9703-214">Criar um endereço IP público</span><span class="sxs-lookup"><span data-stu-id="c9703-214">Create a public IP address</span></span>
<span data-ttu-id="c9703-215">Agora vamos criar o endereço IP público hello (PIP) que podemos atribuir tooyour balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="c9703-215">Now let's create hello public IP address (PIP) that we assign tooyour load balancer.</span></span> <span data-ttu-id="c9703-216">Ele permite tooconnect tooyour VMs de saudação à Internet usando Olá `azure network public-ip create` comando.</span><span class="sxs-lookup"><span data-stu-id="c9703-216">It enables you tooconnect tooyour VMs from hello Internet by using hello `azure network public-ip create` command.</span></span> <span data-ttu-id="c9703-217">Como o endereço de saudação padrão é dinâmico, criamos uma entrada DNS denominada Olá **cloudapp.azure.com** domínio usando Olá `--domain-name-label` opção.</span><span class="sxs-lookup"><span data-stu-id="c9703-217">Because hello default address is dynamic, we create a named DNS entry in hello **cloudapp.azure.com** domain by using hello `--domain-name-label` option.</span></span> <span data-ttu-id="c9703-218">Olá, exemplo a seguir cria um IP público denominado `myPublicIP` com nome DNS de saudação do `mypublicdns`.</span><span class="sxs-lookup"><span data-stu-id="c9703-218">hello following example creates a public IP named `myPublicIP` with hello DNS name of `mypublicdns`.</span></span> <span data-ttu-id="c9703-219">Como o nome de DNS Olá deve ser exclusivo, você pode fornecer seu próprio nome DNS exclusivo:</span><span class="sxs-lookup"><span data-stu-id="c9703-219">Because hello DNS name must be unique, you provide your own unique DNS name:</span></span>

```azurecli
azure network public-ip create --resource-group myResourceGroup \
  --location westeurope --name myPublicIP --domain-name-label mypublicdns
```

<span data-ttu-id="c9703-220">Saída:</span><span class="sxs-lookup"><span data-stu-id="c9703-220">Output:</span></span>

```azurecli
info:    Executing command network public-ip create
+ Looking up hello public ip "myPublicIP"
+ Creating public ip address "myPublicIP"
+ Looking up hello public ip "myPublicIP"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP
data:    Name                            : myPublicIP
data:    Type                            : Microsoft.Network/publicIPAddresses
data:    Location                        : westeurope
data:    Provisioning state              : Succeeded
data:    Allocation method               : Dynamic
data:    Idle timeout                    : 4
data:    Domain name label               : mypublicdns
data:    FQDN                            : mypublicdns.westeurope.cloudapp.azure.com
info:    network public-ip create command OK
```

<span data-ttu-id="c9703-221">Olá endereço IP público é também um recurso de nível superior, para que você possa ver com `azure group show`.</span><span class="sxs-lookup"><span data-stu-id="c9703-221">hello public IP address is also a top-level resource, so you can see it with `azure group show`.</span></span>

```azurecli
azure group show myResourceGroup --json | jq '.'
```

<span data-ttu-id="c9703-222">Saída:</span><span class="sxs-lookup"><span data-stu-id="c9703-222">Output:</span></span>

```json
{
"tags": {},
"id": "/subscriptions/guid/resourceGroups/myResourceGroup",
"name": "myResourceGroup",
"provisioningState": "Succeeded",
"location": "westeurope",
"properties": {
    "provisioningState": "Succeeded"
},
"resources": [
    {
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP",
    "name": "myPublicIP",
    "type": "publicIPAddresses",
    "location": "westeurope",
    "tags": null
    },
    {
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet",
    "name": "myVnet",
    "type": "virtualNetworks",
    "location": "westeurope",
    "tags": null
    },
    {
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Storage/storageAccounts/mystorageaccount",
    "name": "mystorageaccount",
    "type": "storageAccounts",
    "location": "westeurope",
    "tags": null
    }
],
"permissions": [
    {
    "actions": [
        "*"
    ],
    "notActions": []
    }
]
}
```

<span data-ttu-id="c9703-223">Você pode investigar mais detalhes de recursos, incluindo o nome de domínio totalmente qualificado (FQDN) saudação do subdomínio de saudação usando Olá completa `azure network public-ip show` comando.</span><span class="sxs-lookup"><span data-stu-id="c9703-223">You can investigate more resource details, including hello fully qualified domain name (FQDN) of hello subdomain, by using hello complete `azure network public-ip show` command.</span></span> <span data-ttu-id="c9703-224">recurso de endereço IP público Olá foi alocado logicamente, mas um endereço específico ainda não foi atribuído.</span><span class="sxs-lookup"><span data-stu-id="c9703-224">hello public IP address resource has been allocated logically, but a specific address has not yet been assigned.</span></span> <span data-ttu-id="c9703-225">tooobtain um endereço IP, você vai tooneed um balanceador de carga, ainda não tiver criado.</span><span class="sxs-lookup"><span data-stu-id="c9703-225">tooobtain an IP address, you're going tooneed a load balancer, which we have not yet created.</span></span>

```azurecli
azure network public-ip show myResourceGroup myPublicIP --json | jq '.'
```

<span data-ttu-id="c9703-226">Saída:</span><span class="sxs-lookup"><span data-stu-id="c9703-226">Output:</span></span>

```json
{
"tags": {},
"publicIpAllocationMethod": "Dynamic",
"dnsSettings": {
    "domainNameLabel": "mypublicdns",
    "fqdn": "mypublicdns.westeurope.cloudapp.azure.com"
},
"idleTimeoutInMinutes": 4,
"provisioningState": "Succeeded",
"etag": "W/\"c63154b3-1130-49b9-a887-877d74d5ebc5\"",
"id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP",
"name": "myPublicIP",
"location": "westeurope"
}
```

## <a name="create-a-load-balancer-and-ip-pools"></a><span data-ttu-id="c9703-227">Criar um balanceador de carga e pools de IPs</span><span class="sxs-lookup"><span data-stu-id="c9703-227">Create a load balancer and IP pools</span></span>
<span data-ttu-id="c9703-228">Quando você cria um balanceador de carga, ele permite que você toodistribute tráfego em várias VMs.</span><span class="sxs-lookup"><span data-stu-id="c9703-228">When you create a load balancer, it enables you toodistribute traffic across multiple VMs.</span></span> <span data-ttu-id="c9703-229">Ele também fornece aplicativos de tooyour redundância executando várias VMs que respondem a solicitações de toouser no evento de saudação de manutenção ou pesadas.</span><span class="sxs-lookup"><span data-stu-id="c9703-229">It also provides redundancy tooyour application by running multiple VMs that respond toouser requests in hello event of maintenance or heavy loads.</span></span> <span data-ttu-id="c9703-230">Olá, exemplo a seguir cria um balanceador de carga chamado `myLoadBalancer`:</span><span class="sxs-lookup"><span data-stu-id="c9703-230">hello following example creates a load balancer named `myLoadBalancer`:</span></span>

```azurecli
azure network lb create --resource-group myResourceGroup --location westeurope \
  --name myLoadBalancer
```

<span data-ttu-id="c9703-231">Saída:</span><span class="sxs-lookup"><span data-stu-id="c9703-231">Output:</span></span>

```azurecli
info:    Executing command network lb create
+ Looking up hello load balancer "myLoadBalancer"
+ Creating load balancer "myLoadBalancer"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer
data:    Name                            : myLoadBalancer
data:    Type                            : Microsoft.Network/loadBalancers
data:    Location                        : westeurope
data:    Provisioning state              : Succeeded
info:    network lb create command OK
```

<span data-ttu-id="c9703-232">Nosso balanceador de carga está bem vazio, então vamos criar alguns pools de IPs.</span><span class="sxs-lookup"><span data-stu-id="c9703-232">Our load balancer is fairly empty, so let's create some IP pools.</span></span> <span data-ttu-id="c9703-233">Queremos toocreate dois pools de IP para nosso balanceador de carga, um para o front-end hello e outro para o back-end hello.</span><span class="sxs-lookup"><span data-stu-id="c9703-233">We want toocreate two IP pools for our load balancer, one for hello front end and one for hello back end.</span></span> <span data-ttu-id="c9703-234">pool de IP de front-end de saudação é visível publicamente.</span><span class="sxs-lookup"><span data-stu-id="c9703-234">hello front-end IP pool is publicly visible.</span></span> <span data-ttu-id="c9703-235">Também é Olá local toowhich que nós atribuímos Olá PIP que criamos anteriormente.</span><span class="sxs-lookup"><span data-stu-id="c9703-235">It's also hello location toowhich we assign hello PIP that we created earlier.</span></span> <span data-ttu-id="c9703-236">Em seguida, usamos pool de back-end Olá como um local de nossa tooconnect VMs para.</span><span class="sxs-lookup"><span data-stu-id="c9703-236">Then we use hello back-end pool as a location for our VMs tooconnect to.</span></span> <span data-ttu-id="c9703-237">Dessa forma, o tráfego de saudação pode fluir pelo toohello balanceador de carga Olá VMs.</span><span class="sxs-lookup"><span data-stu-id="c9703-237">That way, hello traffic can flow through hello load balancer toohello VMs.</span></span>

<span data-ttu-id="c9703-238">Primeiro, vamos criar nosso pool de IPs de front-end.</span><span class="sxs-lookup"><span data-stu-id="c9703-238">First, let's create our front-end IP pool.</span></span> <span data-ttu-id="c9703-239">Olá, exemplo a seguir cria um pool de front-end denominado `myFrontEndPool`:</span><span class="sxs-lookup"><span data-stu-id="c9703-239">hello following example creates a front-end pool named `myFrontEndPool`:</span></span>

```azurecli
azure network lb frontend-ip create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --public-ip-name myPublicIP \
  --name myFrontEndPool
```

<span data-ttu-id="c9703-240">Saída:</span><span class="sxs-lookup"><span data-stu-id="c9703-240">Output:</span></span>

```azurecli
info:    Executing command network lb frontend-ip create
+ Looking up hello load balancer "myLoadBalancer"
+ Looking up hello public ip "myPublicIP"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myFrontEndPool
data:    Provisioning state              : Succeeded
data:    Private IP allocation method    : Dynamic
data:    Public IP address id            : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP
info:    network lb mySubnet-ip create command OK
```

<span data-ttu-id="c9703-241">Observe como usamos Olá `--public-ip-name` toopass de inserção Olá `myPublicIP` que criamos anteriormente.</span><span class="sxs-lookup"><span data-stu-id="c9703-241">Note how we used hello `--public-ip-name` switch toopass in hello `myPublicIP` that we created earlier.</span></span> <span data-ttu-id="c9703-242">Atribuição de IP público Olá balanceador de carga do endereço toohello permite que você tooreach suas VMs em Olá da Internet.</span><span class="sxs-lookup"><span data-stu-id="c9703-242">Assigning hello public IP address toohello load balancer allows you tooreach your VMs across hello Internet.</span></span>

<span data-ttu-id="c9703-243">Em seguida, vamos criar nosso segundo pool de IPs, desta vez, para o tráfego de back-end.</span><span class="sxs-lookup"><span data-stu-id="c9703-243">Next, let's create our second IP pool, this time for our back-end traffic.</span></span> <span data-ttu-id="c9703-244">Olá, exemplo a seguir cria um pool de back-end denominado `myBackEndPool`:</span><span class="sxs-lookup"><span data-stu-id="c9703-244">hello following example creates a back-end pool named `myBackEndPool`:</span></span>

```azurecli
azure network lb address-pool create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myBackEndPool
```

<span data-ttu-id="c9703-245">Saída:</span><span class="sxs-lookup"><span data-stu-id="c9703-245">Output:</span></span>

```azurecli
info:    Executing command network lb address-pool create
+ Looking up hello load balancer "myLoadBalancer"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myBackEndPool
data:    Provisioning state              : Succeeded
info:    network lb address-pool create command OK
```

<span data-ttu-id="c9703-246">Podemos ver como nosso balanceador de carga está procurando com `azure network lb show` e examinar a saída JSON hello:</span><span class="sxs-lookup"><span data-stu-id="c9703-246">We can see how our load balancer is doing by looking with `azure network lb show` and examining hello JSON output:</span></span>

```azurecli
azure network lb show myResourceGroup myLoadBalancer --json | jq '.'
```

<span data-ttu-id="c9703-247">Saída:</span><span class="sxs-lookup"><span data-stu-id="c9703-247">Output:</span></span>

```json
{
  "etag": "W/\"29c38649-77d6-43ff-ab8f-977536b0047c\"",
  "provisioningState": "Succeeded",
  "resourceGuid": "f1446acb-09ba-44d9-b8b6-849d9983dc09",
  "outboundNatRules": [],
  "inboundNatPools": [],
  "inboundNatRules": [],
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer",
  "name": "myLoadBalancer",
  "type": "Microsoft.Network/loadBalancers",
  "location": "westeurope",
  "mySubnetIPConfigurations": [
    {
      "etag": "W/\"29c38649-77d6-43ff-ab8f-977536b0047c\"",
      "name": "myFrontEndPool",
      "provisioningState": "Succeeded",
      "publicIPAddress": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP"
      },
      "privateIPAllocationMethod": "Dynamic",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
    }
  ],
  "backendAddressPools": [
    {
      "etag": "W/\"29c38649-77d6-43ff-ab8f-977536b0047c\"",
      "name": "myBackEndPool",
      "provisioningState": "Succeeded",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool"
    }
  ],
  "loadBalancingRules": [],
  "probes": []
}
```

## <a name="create-load-balancer-nat-rules"></a><span data-ttu-id="c9703-248">Criar regras NAT do balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="c9703-248">Create load balancer NAT rules</span></span>
<span data-ttu-id="c9703-249">tráfego tooget que passam por nossos balanceador de carga, precisamos de regras NAT (conversão) de endereços de rede de toocreate que especificam as ações de entrada ou saídas.</span><span class="sxs-lookup"><span data-stu-id="c9703-249">tooget traffic flowing through our load balancer, we need toocreate network address translation (NAT) rules that specify either inbound or outbound actions.</span></span> <span data-ttu-id="c9703-250">Você pode especificar Olá protocolo toouse e mapear portas externas toointernal portas conforme desejado.</span><span class="sxs-lookup"><span data-stu-id="c9703-250">You can specify hello protocol toouse, then map external ports toointernal ports as desired.</span></span> <span data-ttu-id="c9703-251">Em nosso ambiente, vamos criar algumas regras que permitem SSH por meio de nosso tooour de Balanceador de carga de máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="c9703-251">For our environment, let's create some rules that allow SSH through our load balancer tooour VMs.</span></span> <span data-ttu-id="c9703-252">Fizemos porta do TCP portas 4222 e 4223 toodirect tooTCP 22 em nosso VMs (que criamos mais tarde).</span><span class="sxs-lookup"><span data-stu-id="c9703-252">We set up TCP ports 4222 and 4223 toodirect tooTCP port 22 on our VMs (which we create later).</span></span> <span data-ttu-id="c9703-253">Olá, exemplo a seguir cria uma regra denominada `myLoadBalancerRuleSSH1` toomap TCP porta 4222 tooport 22:</span><span class="sxs-lookup"><span data-stu-id="c9703-253">hello following example creates a rule named `myLoadBalancerRuleSSH1` toomap TCP port 4222 tooport 22:</span></span>

```azurecli
azure network lb inbound-nat-rule create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myLoadBalancerRuleSSH1 \
  --protocol tcp --frontend-port 4222 --backend-port 22
```

<span data-ttu-id="c9703-254">Saída:</span><span class="sxs-lookup"><span data-stu-id="c9703-254">Output:</span></span>

```azurecli
info:    Executing command network lb inbound-nat-rule create
+ Looking up hello load balancer "myLoadBalancer"
warn:    Using default enable floating ip: false
warn:    Using default idle timeout: 4
warn:    Using default mySubnet IP configuration "myFrontEndPool"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myLoadBalancerRuleSSH1
data:    Provisioning state              : Succeeded
data:    Protocol                        : Tcp
data:    mySubnet port                   : 4222
data:    Backend port                    : 22
data:    Enable floating IP              : false
data:    Idle timeout in minutes         : 4
data:    mySubnet IP configuration id    : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool
info:    network lb inbound-nat-rule create command OK
```

<span data-ttu-id="c9703-255">Repita o procedimento de saudação da segunda regra NAT para o SSH.</span><span class="sxs-lookup"><span data-stu-id="c9703-255">Repeat hello procedure for your second NAT rule for SSH.</span></span> <span data-ttu-id="c9703-256">Olá, exemplo a seguir cria uma regra denominada `myLoadBalancerRuleSSH2` toomap TCP porta 4223 tooport 22:</span><span class="sxs-lookup"><span data-stu-id="c9703-256">hello following example creates a rule named `myLoadBalancerRuleSSH2` toomap TCP port 4223 tooport 22:</span></span>

```azurecli
azure network lb inbound-nat-rule create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myLoadBalancerRuleSSH2 --protocol tcp \
  --frontend-port 4223 --backend-port 22
```

<span data-ttu-id="c9703-257">Vamos também vá em frente e crie uma regra NAT para a porta TCP 80 para tráfego da web, gancho regra Olá tooour pools de IP.</span><span class="sxs-lookup"><span data-stu-id="c9703-257">Let's also go ahead and create a NAT rule for TCP port 80 for web traffic, hooking hello rule up tooour IP pools.</span></span> <span data-ttu-id="c9703-258">Se nós ligar Olá regra tooan pool IP, em vez de gancho Olá regra tooour VMs individualmente, podemos pode adicionar ou remover o VMs saudação do pool de IP.</span><span class="sxs-lookup"><span data-stu-id="c9703-258">If we hook up hello rule tooan IP pool, instead of hooking up hello rule tooour VMs individually, we can add or remove VMs from hello IP pool.</span></span> <span data-ttu-id="c9703-259">Balanceador de carga Olá ajusta automaticamente o fluxo de saudação do tráfego.</span><span class="sxs-lookup"><span data-stu-id="c9703-259">hello load balancer automatically adjusts hello flow of traffic.</span></span> <span data-ttu-id="c9703-260">Olá, exemplo a seguir cria uma regra denominada `myLoadBalancerRuleWeb` toomap TCP porta 80 tooport 80:</span><span class="sxs-lookup"><span data-stu-id="c9703-260">hello following example creates a rule named `myLoadBalancerRuleWeb` toomap TCP port 80 tooport 80:</span></span>

```azurecli
azure network lb rule create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myLoadBalancerRuleWeb --protocol tcp \
  --frontend-port 80 --backend-port 80 --frontend-ip-name myFrontEndPool \
  --backend-address-pool-name myBackEndPool
```

<span data-ttu-id="c9703-261">Saída:</span><span class="sxs-lookup"><span data-stu-id="c9703-261">Output:</span></span>

```azurecli
info:    Executing command network lb rule create
+ Looking up hello load balancer "myLoadBalancer"
warn:    Using default idle timeout: 4
warn:    Using default enable floating ip: false
warn:    Using default load distribution: Default
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myLoadBalancerRuleWeb
data:    Provisioning state              : Succeeded
data:    Protocol                        : Tcp
data:    mySubnet port                   : 80
data:    Backend port                    : 80
data:    Enable floating IP              : false
data:    Load distribution               : Default
data:    Idle timeout in minutes         : 4
data:    mySubnet IP configuration id    : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool
data:    Backend address pool id         : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool
info:    network lb rule create command OK
```

## <a name="create-a-load-balancer-health-probe"></a><span data-ttu-id="c9703-262">Criar uma investigação de integridade do balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="c9703-262">Create a load balancer health probe</span></span>
<span data-ttu-id="c9703-263">Uma integridade de teste periodicamente verificações Olá VMs que estão por trás de nossa toomake de Balanceador de carga se eles está operacional e respondendo toorequests conforme definido.</span><span class="sxs-lookup"><span data-stu-id="c9703-263">A health probe periodically checks on hello VMs that are behind our load balancer toomake sure they're operating and responding toorequests as defined.</span></span> <span data-ttu-id="c9703-264">Se não forem removidos da operação tooensure que os usuários não estão sendo direcionado toothem.</span><span class="sxs-lookup"><span data-stu-id="c9703-264">If not, they're removed from operation tooensure that users aren't being directed toothem.</span></span> <span data-ttu-id="c9703-265">Você pode definir a verificações personalizadas para a investigação de integridade hello, juntamente com os intervalos e valores de tempo limite.</span><span class="sxs-lookup"><span data-stu-id="c9703-265">You can define custom checks for hello health probe, along with intervals and timeout values.</span></span> <span data-ttu-id="c9703-266">Para obter mais informações sobre investigações de integridade, consulte [Investigações do Balanceador de Carga](../../load-balancer/load-balancer-custom-probe-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c9703-266">For more information about health probes, see [Load Balancer probes](../../load-balancer/load-balancer-custom-probe-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="c9703-267">Olá, exemplo a seguir cria um TCP integridade investigado nomeado `myHealthProbe`:</span><span class="sxs-lookup"><span data-stu-id="c9703-267">hello following example creates a TCP health probed named `myHealthProbe`:</span></span>

```azurecli
azure network lb probe create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myHealthProbe --protocol "tcp" \
  --interval 15 --count 4
```

<span data-ttu-id="c9703-268">Saída:</span><span class="sxs-lookup"><span data-stu-id="c9703-268">Output:</span></span>

```azurecli
info:    Executing command network lb probe create
warn:    Using default probe port: 80
+ Looking up hello load balancer "myLoadBalancer"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myHealthProbe
data:    Provisioning state              : Succeeded
data:    Protocol                        : Tcp
data:    Port                            : 80
data:    Interval in seconds             : 15
data:    Number of probes                : 4
info:    network lb probe create command OK
```

<span data-ttu-id="c9703-269">Aqui, especificamos um intervalo de 15 segundos para nossas verificações de integridade.</span><span class="sxs-lookup"><span data-stu-id="c9703-269">Here, we specified an interval of 15 seconds for our health checks.</span></span> <span data-ttu-id="c9703-270">Podemos pode perder a um máximo de quatro testes (um minuto) antes de Balanceador de carga Olá considera que hospedam Olá não está mais funcionando.</span><span class="sxs-lookup"><span data-stu-id="c9703-270">We can miss a maximum of four probes (one minute) before hello load balancer considers that hello host is no longer functioning.</span></span>

## <a name="verify-hello-load-balancer"></a><span data-ttu-id="c9703-271">Verifique se o balanceador de carga Olá</span><span class="sxs-lookup"><span data-stu-id="c9703-271">Verify hello load balancer</span></span>
<span data-ttu-id="c9703-272">Agora a configuração de Balanceador de carga de saudação é feita.</span><span class="sxs-lookup"><span data-stu-id="c9703-272">Now hello load balancer configuration is done.</span></span> <span data-ttu-id="c9703-273">Aqui estão as etapas hello:</span><span class="sxs-lookup"><span data-stu-id="c9703-273">Here are hello steps you took:</span></span>

1. <span data-ttu-id="c9703-274">Você criou um balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="c9703-274">You created a load balancer.</span></span>
2. <span data-ttu-id="c9703-275">Você criou um pool IP de front-end e atribuído um tooit IP público.</span><span class="sxs-lookup"><span data-stu-id="c9703-275">You created a front-end IP pool and assigned a public IP tooit.</span></span>
3. <span data-ttu-id="c9703-276">Você criou um pool de IPs de back-end ao qual as VMs podem se conectar.</span><span class="sxs-lookup"><span data-stu-id="c9703-276">You created a back-end IP pool that VMs can connect to.</span></span>
4. <span data-ttu-id="c9703-277">Você criou regras NAT que permitem SSH toohello VMs para gerenciamento, juntamente com uma regra que permite que a porta TCP 80 para o nosso aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="c9703-277">You created NAT rules that allow SSH toohello VMs for management, along with a rule that allows TCP port 80 for our web app.</span></span>
5. <span data-ttu-id="c9703-278">Você adicionou uma saudação de seleção de tooperiodically de investigação de integridade VMs.</span><span class="sxs-lookup"><span data-stu-id="c9703-278">You added a health probe tooperiodically check hello VMs.</span></span> <span data-ttu-id="c9703-279">Essa investigação de integridade garante que os usuários não tentam tooaccess uma máquina virtual que não está funcionando ou que serve o conteúdo.</span><span class="sxs-lookup"><span data-stu-id="c9703-279">This health probe ensures that users don't try tooaccess a VM that is no longer functioning or serving content.</span></span>

<span data-ttu-id="c9703-280">Vamos ver como seu balanceador de carga está agora:</span><span class="sxs-lookup"><span data-stu-id="c9703-280">Let's review what your load balancer looks like now:</span></span>

```azurecli
azure network lb show --resource-group myResourceGroup \
  --name myLoadBalancer --json | jq '.'
```

<span data-ttu-id="c9703-281">Saída:</span><span class="sxs-lookup"><span data-stu-id="c9703-281">Output:</span></span>

```json
{
  "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
  "provisioningState": "Succeeded",
  "resourceGuid": "f1446acb-09ba-44d9-b8b6-849d9983dc09",
  "outboundNatRules": [],
  "inboundNatPools": [],
  "inboundNatRules": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myLoadBalancerRuleSSH1",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1",
      "mySubnetIPConfiguration": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
      },
      "protocol": "Tcp",
      "mySubnetPort": 4222,
      "backendPort": 22,
      "idleTimeoutInMinutes": 4,
      "enableFloatingIP": false,
      "provisioningState": "Succeeded"
    },
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myLoadBalancerRuleSSH2",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2",
      "mySubnetIPConfiguration": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
      },
      "protocol": "Tcp",
      "mySubnetPort": 4223,
      "backendPort": 22,
      "idleTimeoutInMinutes": 4,
      "enableFloatingIP": false,
      "provisioningState": "Succeeded"
    }
  ],
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer",
  "name": "myLoadBalancer",
  "type": "Microsoft.Network/loadBalancers",
  "location": "westeurope",
  "mySubnetIPConfigurations": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myFrontEndPool",
      "provisioningState": "Succeeded",
      "publicIPAddress": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP"
      },
      "privateIPAllocationMethod": "Dynamic",
      "loadBalancingRules": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/loadBalancingRules/myLoadBalancerRuleWeb"
        }
      ],
      "inboundNatRules": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1"
        },
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2"
        }
      ],
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
    }
  ],
  "backendAddressPools": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myBackEndPool",
      "provisioningState": "Succeeded",
      "loadBalancingRules": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/loadBalancingRules/myLoadBalancerRuleWeb"
        }
      ],
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool"
    }
  ],
  "loadBalancingRules": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myLoadBalancerRuleWeb",
      "provisioningState": "Succeeded",
      "enableFloatingIP": false,
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/loadBalancingRules/myLoadBalancerRuleWeb",
      "mySubnetIPConfiguration": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
      },
      "backendAddressPool": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool"
      },
      "protocol": "Tcp",
      "loadDistribution": "Default",
      "mySubnetPort": 80,
      "backendPort": 80,
      "idleTimeoutInMinutes": 4
    }
  ],
  "probes": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myHealthProbe",
      "provisioningState": "Succeeded",
      "numberOfProbes": 4,
      "intervalInSeconds": 15,
      "port": 80,
      "protocol": "Tcp",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/probes/myHealthProbe"
    }
  ]
}
```

## <a name="create-an-nic-toouse-with-hello-linux-vm"></a><span data-ttu-id="c9703-282">Criar uma NIC toouse com hello VM do Linux</span><span class="sxs-lookup"><span data-stu-id="c9703-282">Create an NIC toouse with hello Linux VM</span></span>
<span data-ttu-id="c9703-283">As NICs estão disponíveis por meio de programação porque você pode aplicar regras tootheir uso.</span><span class="sxs-lookup"><span data-stu-id="c9703-283">NICs are programmatically available because you can apply rules tootheir use.</span></span> <span data-ttu-id="c9703-284">Você também pode ter mais de uma.</span><span class="sxs-lookup"><span data-stu-id="c9703-284">You can also have more than one.</span></span> <span data-ttu-id="c9703-285">Seguir Olá `azure network nic create` de comando, ligar o pool IP hello NIC toohello carga back-end e associá-lo a saudação tráfego de SSH de toopermit de regra de NAT.</span><span class="sxs-lookup"><span data-stu-id="c9703-285">In hello following `azure network nic create` command, you hook up hello NIC toohello load back-end IP pool and associate it with hello NAT rule toopermit SSH traffic.</span></span>

<span data-ttu-id="c9703-286">Substituir saudação `#####-###-###` seções com sua ID de assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="c9703-286">Replace hello `#####-###-###` sections with your own Azure subscription ID.</span></span> <span data-ttu-id="c9703-287">Sua assinatura ID é observado na saída de saudação do `jq` ao examinar recursos Olá que você está criando.</span><span class="sxs-lookup"><span data-stu-id="c9703-287">Your subscription ID is noted in hello output of `jq` when you examine hello resources you are creating.</span></span> <span data-ttu-id="c9703-288">Você também pode exibir sua ID de assinatura com `azure account list`.</span><span class="sxs-lookup"><span data-stu-id="c9703-288">You can also view your subscription ID with `azure account list`.</span></span>

<span data-ttu-id="c9703-289">Olá, exemplo a seguir cria uma NIC chamada `myNic1`:</span><span class="sxs-lookup"><span data-stu-id="c9703-289">hello following example creates a NIC named `myNic1`:</span></span>

```azurecli
azure network nic create --resource-group myResourceGroup --location westeurope \
  --subnet-vnet-name myVnet --subnet-name mySubnet --name myNic1 \
  --lb-address-pool-ids /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool \
  --lb-inbound-nat-rule-ids /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1
```

<span data-ttu-id="c9703-290">Saída:</span><span class="sxs-lookup"><span data-stu-id="c9703-290">Output:</span></span>

```azurecli
info:    Executing command network nic create
+ Looking up hello subnet "mySubnet"
+ Looking up hello network interface "myNic1"
+ Creating network interface "myNic1"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic1
data:    Name                            : myNic1
data:    Type                            : Microsoft.Network/networkInterfaces
data:    Location                        : westeurope
data:    Provisioning state              : Succeeded
data:    Enable IP forwarding            : false
data:    IP configurations:
data:      Name                          : Nic-IP-config
data:      Provisioning state            : Succeeded
data:      Private IP address            : 192.168.1.4
data:      Private IP allocation method  : Dynamic
data:      Subnet                        : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet
data:      Load balancer backend address pools:
data:        Id                          : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool
data:      Load balancer inbound NAT rules:
data:        Id                          : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1
data:
info:    network nic create command OK
```

<span data-ttu-id="c9703-291">Você pode ver detalhes Olá examinando os recursos de saudação diretamente.</span><span class="sxs-lookup"><span data-stu-id="c9703-291">You can see hello details by examining hello resource directly.</span></span> <span data-ttu-id="c9703-292">Examinar o recurso hello usando Olá `azure network nic show` comando:</span><span class="sxs-lookup"><span data-stu-id="c9703-292">You examine hello resource by using hello `azure network nic show` command:</span></span>

```azurecli
azure network nic show myResourceGroup myNic1 --json | jq '.'
```

<span data-ttu-id="c9703-293">Saída:</span><span class="sxs-lookup"><span data-stu-id="c9703-293">Output:</span></span>

```json
{
  "etag": "W/\"fc1eaaa1-ee55-45bd-b847-5a08c7f4264a\"",
  "provisioningState": "Succeeded",
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic1",
  "name": "myNic1",
  "type": "Microsoft.Network/networkInterfaces",
  "location": "westeurope",
  "ipConfigurations": [
    {
      "etag": "W/\"fc1eaaa1-ee55-45bd-b847-5a08c7f4264a\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic1/ipConfigurations/Nic-IP-config",
      "loadBalancerBackendAddressPools": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool"
        }
      ],
      "loadBalancerInboundNatRules": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1"
        }
      ],
      "privateIPAddress": "192.168.1.4",
      "privateIPAllocationMethod": "Dynamic",
      "subnet": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet"
      },
      "provisioningState": "Succeeded",
      "name": "Nic-IP-config"
    }
  ],
  "dnsSettings": {
    "appliedDnsServers": [],
    "dnsServers": []
  },
  "enableIPForwarding": false,
  "resourceGuid": "a20258b8-6361-45f6-b1b4-27ffed28798c"
}
```

<span data-ttu-id="c9703-294">Agora podemos criar hello segundo NIC, capturando no pool IP de back-end tooour novamente.</span><span class="sxs-lookup"><span data-stu-id="c9703-294">Now we create hello second NIC, hooking in tooour back-end IP pool again.</span></span> <span data-ttu-id="c9703-295">Esta regra NAT tempo Olá segundo permite o tráfego SSH.</span><span class="sxs-lookup"><span data-stu-id="c9703-295">This time hello second NAT rule permits SSH traffic.</span></span> <span data-ttu-id="c9703-296">Olá, exemplo a seguir cria uma NIC chamada `myNic2`:</span><span class="sxs-lookup"><span data-stu-id="c9703-296">hello following example creates a NIC named `myNic2`:</span></span>

```azurecli
azure network nic create --resource-group myResourceGroup --location westeurope \
  --subnet-vnet-name myVnet --subnet-name mySubnet --name myNic2 \
  --lb-address-pool-ids  /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool \
  --lb-inbound-nat-rule-ids /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2
```

## <a name="create-a-network-security-group-and-rules"></a><span data-ttu-id="c9703-297">Criar um grupo de segurança de rede e suas regras</span><span class="sxs-lookup"><span data-stu-id="c9703-297">Create a network security group and rules</span></span>
<span data-ttu-id="c9703-298">Agora podemos criar um grupo de segurança de rede e Olá regras de entrada que controlam acesso NIC toohello.</span><span class="sxs-lookup"><span data-stu-id="c9703-298">Now we create a network security group and hello inbound rules that govern access toohello NIC.</span></span> <span data-ttu-id="c9703-299">Um grupo de segurança de rede pode ser aplicado tooa NIC ou sub-rede.</span><span class="sxs-lookup"><span data-stu-id="c9703-299">A network security group can be applied tooa NIC or subnet.</span></span> <span data-ttu-id="c9703-300">Definir o fluxo de saudação toocontrol regras de tráfego dentro e fora de suas VMs.</span><span class="sxs-lookup"><span data-stu-id="c9703-300">You define rules toocontrol hello flow of traffic in and out of your VMs.</span></span> <span data-ttu-id="c9703-301">Olá, exemplo a seguir cria um grupo de segurança de rede denominado `myNetworkSecurityGroup`:</span><span class="sxs-lookup"><span data-stu-id="c9703-301">hello following example creates a network security group named `myNetworkSecurityGroup`:</span></span>

```azurecli
azure network nsg create --resource-group myResourceGroup --location westeurope \
  --name myNetworkSecurityGroup
```

<span data-ttu-id="c9703-302">Vamos adicionar regra de entrada hello para Olá NSG tooallow conexões na porta 22 (toosupport SSH) de entrada.</span><span class="sxs-lookup"><span data-stu-id="c9703-302">Let's add hello inbound rule for hello NSG tooallow inbound connections on port 22 (toosupport SSH).</span></span> <span data-ttu-id="c9703-303">Olá, exemplo a seguir cria uma regra denominada `myNetworkSecurityGroupRuleSSH` tooallow TCP na porta 22:</span><span class="sxs-lookup"><span data-stu-id="c9703-303">hello following example creates a rule named `myNetworkSecurityGroupRuleSSH` tooallow TCP on port 22:</span></span>

```azurecli
azure network nsg rule create --resource-group myResourceGroup \
  --nsg-name myNetworkSecurityGroup --protocol tcp --direction inbound \
  --priority 1000 --destination-port-range 22 --access allow \
  --name myNetworkSecurityGroupRuleSSH
```

<span data-ttu-id="c9703-304">Agora vamos adicionar regra de entrada hello para Olá NSG tooallow conexões na porta 80 (toosupport o tráfego da web) de entrada.</span><span class="sxs-lookup"><span data-stu-id="c9703-304">Now let's add hello inbound rule for hello NSG tooallow inbound connections on port 80 (toosupport web traffic).</span></span> <span data-ttu-id="c9703-305">Olá, exemplo a seguir cria uma regra denominada `myNetworkSecurityGroupRuleHTTP` tooallow TCP na porta 80:</span><span class="sxs-lookup"><span data-stu-id="c9703-305">hello following example creates a rule named `myNetworkSecurityGroupRuleHTTP` tooallow TCP on port 80:</span></span>

```azurecli
azure network nsg rule create --resource-group myResourceGroup \
  --nsg-name myNetworkSecurityGroup --protocol tcp --direction inbound \
  --priority 1001 --destination-port-range 80 --access allow \
  --name myNetworkSecurityGroupRuleHTTP
```

> [!NOTE]
> <span data-ttu-id="c9703-306">regra de entrada Hello é um filtro para conexões de rede de entrada.</span><span class="sxs-lookup"><span data-stu-id="c9703-306">hello inbound rule is a filter for inbound network connections.</span></span> <span data-ttu-id="c9703-307">Neste exemplo, podemos associar Olá NSG toohello NIC virtual VMs, que significa que qualquer solicitação tooport 22 é transmitido toohello NIC em nosso VM.</span><span class="sxs-lookup"><span data-stu-id="c9703-307">In this example, we bind hello NSG toohello VMs virtual NIC, which means that any request tooport 22 is passed through toohello NIC on our VM.</span></span> <span data-ttu-id="c9703-308">Essa regra de entrada é sobre uma conexão de rede e não sobre um ponto de extremidade, que seria o caso em implantações clássicas.</span><span class="sxs-lookup"><span data-stu-id="c9703-308">This inbound rule is about a network connection, and not about an endpoint, which is what it would be about in classic deployments.</span></span> <span data-ttu-id="c9703-309">tooopen uma porta, você deve deixar Olá `--source-port-range` definido muito '\*' tooaccept (valor padrão de saudação) solicitações de entrada **qualquer** solicitando a porta.</span><span class="sxs-lookup"><span data-stu-id="c9703-309">tooopen a port, you must leave hello `--source-port-range` set too'\*' (hello default value) tooaccept inbound requests from **any** requesting port.</span></span> <span data-ttu-id="c9703-310">Normalmente, as portas são dinâmicas.</span><span class="sxs-lookup"><span data-stu-id="c9703-310">Ports are typically dynamic.</span></span>
>
>

## <a name="bind-toohello-nic"></a><span data-ttu-id="c9703-311">Associar toohello NIC</span><span class="sxs-lookup"><span data-stu-id="c9703-311">Bind toohello NIC</span></span>
<span data-ttu-id="c9703-312">Associe Olá NSG toohello NICs.</span><span class="sxs-lookup"><span data-stu-id="c9703-312">Bind hello NSG toohello NICs.</span></span> <span data-ttu-id="c9703-313">É preciso tooconnect nosso NICs com nosso grupo de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="c9703-313">We need tooconnect our NICs with our network security group.</span></span> <span data-ttu-id="c9703-314">Execute os dois comandos, toohook backup dos nossos NICs:</span><span class="sxs-lookup"><span data-stu-id="c9703-314">Run both commands, toohook up both of our NICs:</span></span>

```azurecli
azure network nic set --resource-group myResourceGroup --name myNic1 \
  --network-security-group-name myNetworkSecurityGroup
```

```azurecli
azure network nic set --resource-group myResourceGroup --name myNic2 \
  --network-security-group-name myNetworkSecurityGroup
```

## <a name="create-an-availability-set"></a><span data-ttu-id="c9703-315">Criar um conjunto de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="c9703-315">Create an availability set</span></span>
<span data-ttu-id="c9703-316">Conjuntos de disponibilidade ajudam a difundir suas VMs em domínios de falha e domínios de atualização.</span><span class="sxs-lookup"><span data-stu-id="c9703-316">Availability sets help spread your VMs across fault domains and upgrade domains.</span></span> <span data-ttu-id="c9703-317">Vamos criar um conjunto de disponibilidade para suas VMs.</span><span class="sxs-lookup"><span data-stu-id="c9703-317">Let's create an availability set for your VMs.</span></span> <span data-ttu-id="c9703-318">Olá, exemplo a seguir cria um conjunto nomeada de disponibilidade `myAvailabilitySet`:</span><span class="sxs-lookup"><span data-stu-id="c9703-318">hello following example creates an availability set named `myAvailabilitySet`:</span></span>

```azurecli
azure availset create --resource-group myResourceGroup --location westeurope
  --name myAvailabilitySet
```

<span data-ttu-id="c9703-319">Os domínios de falha definem um agrupamento de máquinas virtuais que compartilham uma mesma fonte de alimentação e um mesmo comutador de rede.</span><span class="sxs-lookup"><span data-stu-id="c9703-319">Fault domains define a grouping of virtual machines that share a common power source and network switch.</span></span> <span data-ttu-id="c9703-320">Por padrão, máquinas virtuais Olá configuradas em seu conjunto de disponibilidade são separadas em domínios de falha de toothree.</span><span class="sxs-lookup"><span data-stu-id="c9703-320">By default, hello virtual machines that are configured within your availability set are separated across up toothree fault domains.</span></span> <span data-ttu-id="c9703-321">ideia Olá é um problema de hardware em um desses domínios de falha não afeta todas as VMs que estão executando o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c9703-321">hello idea is that a hardware issue in one of these fault domains does not affect every VM that is running your app.</span></span> <span data-ttu-id="c9703-322">Azure distribui automaticamente as VMs em domínios de falha de saudação quando colocando-os em um conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="c9703-322">Azure automatically distributes VMs across hello fault domains when placing them in an availability set.</span></span>

<span data-ttu-id="c9703-323">Domínios de atualização indicam grupos de máquinas virtuais e o hardware físico subjacente que pode ser reinicializado no hello simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="c9703-323">Upgrade domains indicate groups of virtual machines and underlying physical hardware that can be rebooted at hello same time.</span></span> <span data-ttu-id="c9703-324">ordem de saudação na qual os domínios de atualização são reiniciados pode não ser sequencial durante a manutenção planejada, mas é reinicializada somente uma atualização de cada vez.</span><span class="sxs-lookup"><span data-stu-id="c9703-324">hello order in which upgrade domains are rebooted might not be sequential during planned maintenance, but only one upgrade is rebooted at a time.</span></span> <span data-ttu-id="c9703-325">Mais uma vez, o Azure distribui automaticamente as VMs entre os domínios de atualização ao colocá-las em um site de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="c9703-325">Again, Azure automatically distributes your VMs across upgrade domains when placing them in an availability site.</span></span>

<span data-ttu-id="c9703-326">Leia mais sobre [gerenciar a disponibilidade de saudação de VMs](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c9703-326">Read more about [managing hello availability of VMs](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="create-hello-linux-vms"></a><span data-ttu-id="c9703-327">Criar VMs do Linux Olá</span><span class="sxs-lookup"><span data-stu-id="c9703-327">Create hello Linux VMs</span></span>
<span data-ttu-id="c9703-328">Você criou os recursos de armazenamento e rede Olá VMs toosupport acessível pela Internet.</span><span class="sxs-lookup"><span data-stu-id="c9703-328">You've created hello storage and network resources toosupport Internet-accessible VMs.</span></span> <span data-ttu-id="c9703-329">Agora, vamos criar essas VMs e protegê-las com uma chave SSH que não tem senha.</span><span class="sxs-lookup"><span data-stu-id="c9703-329">Now let's create those VMs and secure them with an SSH key that doesn't have a password.</span></span> <span data-ttu-id="c9703-330">Nesse caso, vamos toocreate uma VM Ubuntu com base em Olá LTS mais recente.</span><span class="sxs-lookup"><span data-stu-id="c9703-330">In this case, we're going toocreate an Ubuntu VM based on hello most recent LTS.</span></span> <span data-ttu-id="c9703-331">Localizaremos as informações dessa imagem usando `azure vm image list`, conforme descrito em [localização de imagens de VM do Azure](../windows/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c9703-331">We locate that image information by using `azure vm image list`, as described in [finding Azure VM images](../windows/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="c9703-332">Selecionamos uma imagem usando o comando Olá `azure vm image list westeurope canonical | grep LTS`.</span><span class="sxs-lookup"><span data-stu-id="c9703-332">We selected an image by using hello command `azure vm image list westeurope canonical | grep LTS`.</span></span> <span data-ttu-id="c9703-333">Neste caso, usamos `canonical:UbuntuServer:16.04.0-LTS:16.04.201608150`.</span><span class="sxs-lookup"><span data-stu-id="c9703-333">In this case, we use `canonical:UbuntuServer:16.04.0-LTS:16.04.201608150`.</span></span> <span data-ttu-id="c9703-334">Para o último campo de hello, passamos `latest` para que no futuro Olá sempre obtemos compilação mais recente do hello.</span><span class="sxs-lookup"><span data-stu-id="c9703-334">For hello last field, we pass `latest` so that in hello future we always get hello most recent build.</span></span> <span data-ttu-id="c9703-335">(cadeia de caracteres de saudação usamos é `canonical:UbuntuServer:16.04.0-LTS:16.04.201608150`).</span><span class="sxs-lookup"><span data-stu-id="c9703-335">(hello string we use is `canonical:UbuntuServer:16.04.0-LTS:16.04.201608150`).</span></span>

<span data-ttu-id="c9703-336">A próxima etapa é tooanyone familiar que já tenha criado um ssh chaves pública e privada do rsa emparelhar no Linux ou Mac usando **ssh-keygen - t rsa -b 2048**.</span><span class="sxs-lookup"><span data-stu-id="c9703-336">This next step is familiar tooanyone who has already created an ssh rsa public and private key pair on Linux or Mac by using **ssh-keygen -t rsa -b 2048**.</span></span> <span data-ttu-id="c9703-337">Se não tiver pares de chave de certificado no seu diretório `~/.ssh` , você poderá criá-los:</span><span class="sxs-lookup"><span data-stu-id="c9703-337">If you do not have any certificate key pairs in your `~/.ssh` directory, you can create them:</span></span>

* <span data-ttu-id="c9703-338">Automaticamente, usando Olá `azure vm create --generate-ssh-keys` opção.</span><span class="sxs-lookup"><span data-stu-id="c9703-338">Automatically, by using hello `azure vm create --generate-ssh-keys` option.</span></span>
* <span data-ttu-id="c9703-339">Manualmente, usando [Olá instruções toocreate-las por conta própria](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c9703-339">Manually, by using [hello instructions toocreate them yourself](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="c9703-340">Como alternativa, você pode usar o hello `--admin-password` método tooauthenticate suas conexões SSH após Olá VM é criada.</span><span class="sxs-lookup"><span data-stu-id="c9703-340">Alternatively, you can use hello `--admin-password` method tooauthenticate your SSH connections after hello VM is created.</span></span> <span data-ttu-id="c9703-341">Esse método normalmente é menos seguro.</span><span class="sxs-lookup"><span data-stu-id="c9703-341">This method is typically less secure.</span></span>

<span data-ttu-id="c9703-342">Criamos Olá VM fazendo com que todos os nossos recursos e informações junto com hello `azure vm create` comando:</span><span class="sxs-lookup"><span data-stu-id="c9703-342">We create hello VM by bringing all our resources and information together with hello `azure vm create` command:</span></span>

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM1 \
  --location westeurope \
  --os-type linux \
  --availset-name myAvailabilitySet \
  --nic-name myNic1 \
  --vnet-name myVnet \
  --vnet-subnet-name mySubnet \
  --storage-account-name mystorageaccount \
  --image-urn canonical:UbuntuServer:16.04.0-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username azureuser
```

<span data-ttu-id="c9703-343">Saída:</span><span class="sxs-lookup"><span data-stu-id="c9703-343">Output:</span></span>

```azurecli
info:    Executing command vm create
+ Looking up hello VM "myVM1"
info:    Verifying hello public key SSH file: /home/ahmet/.ssh/id_rsa.pub
info:    Using hello VM Size "Standard_DS1"
info:    hello [OS, Data] Disk or image configuration requires storage account
+ Looking up hello storage account mystorageaccount
+ Looking up hello availability set "myAvailabilitySet"
info:    Found an Availability set "myAvailabilitySet"
+ Looking up hello NIC "myNic1"
info:    Found an existing NIC "myNic1"
info:    Found an IP configuration with virtual network subnet id "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet" in hello NIC "myNic1"
info:    This is an NIC without publicIP configured
info:    hello storage URI 'https://mystorageaccount.blob.core.windows.net/' will be used for boot diagnostics settings, and it can be overwritten by hello parameter input of '--boot-diagnostics-storage-uri'.
info:    vm create command OK
```

<span data-ttu-id="c9703-344">Você pode conectar tooyour VM imediatamente usando suas chaves SSH padrão.</span><span class="sxs-lookup"><span data-stu-id="c9703-344">You can connect tooyour VM immediately by using your default SSH keys.</span></span> <span data-ttu-id="c9703-345">Certifique-se de que você especifique a porta apropriada Olá já que estamos passando por meio do balanceador de carga de saudação.</span><span class="sxs-lookup"><span data-stu-id="c9703-345">Make sure that you specify hello appropriate port since we're passing through hello load balancer.</span></span> <span data-ttu-id="c9703-346">(Para nossa primeira VM, configuramos porta Olá NAT regra tooforward 4222 tooour VM.)</span><span class="sxs-lookup"><span data-stu-id="c9703-346">(For our first VM, we set up hello NAT rule tooforward port 4222 tooour VM.)</span></span>

```bash
ssh ops@mypublicdns.westeurope.cloudapp.azure.com -p 4222
```

<span data-ttu-id="c9703-347">Saída:</span><span class="sxs-lookup"><span data-stu-id="c9703-347">Output:</span></span>

```bash
hello authenticity of host '[mypublicdns.westeurope.cloudapp.azure.com]:4222 ([xx.xx.xx.xx]:4222)' can't be established.
ECDSA key fingerprint is 94:2d:d0:ce:6b:fb:7f:ad:5b:3c:78:93:75:82:12:f9.
Are you sure you want toocontinue connecting (yes/no)? yes
Warning: Permanently added '[mypublicdns.westeurope.cloudapp.azure.com]:4222,[xx.xx.xx.xx]:4222' (ECDSA) toohello list of known hosts.
Welcome tooUbuntu 16.04.1 LTS (GNU/Linux 4.4.0-34-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  Get cloud support with Ubuntu Advantage Cloud Guest:
    http://www.ubuntu.com/business/services/cloud

0 packages can be updated.
0 updates are security updates.

ops@myVM1:~$
```

<span data-ttu-id="c9703-348">Vá em frente e crie sua segunda VM em Olá mesma maneira:</span><span class="sxs-lookup"><span data-stu-id="c9703-348">Go ahead and create your second VM in hello same manner:</span></span>

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM2 \
  --location westeurope \
  --os-type linux \
  --availset-name myAvailabilitySet \
  --nic-name myNic2 \
  --vnet-name myVnet \
  --vnet-subnet-name mySubnet \
  --storage-account-name mystorageaccount \
  --image-urn canonical:UbuntuServer:16.04.0-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username azureuser
```

<span data-ttu-id="c9703-349">E agora você pode usar o hello `azure vm show myResourceGroup myVM1` tooexamine de comando que você criou.</span><span class="sxs-lookup"><span data-stu-id="c9703-349">And you can now use hello `azure vm show myResourceGroup myVM1` command tooexamine what you've created.</span></span> <span data-ttu-id="c9703-350">Neste ponto, você está executando suas VMs Ubuntu atrás de um balanceador de carga no Azure, em que só pode fazer logon com seu par de chaves SSH (porque as senhas estão desabilitadas).</span><span class="sxs-lookup"><span data-stu-id="c9703-350">At this point, you're running your Ubuntu VMs behind a load balancer in Azure that you can sign into only with your SSH key pair (because passwords are disabled).</span></span> <span data-ttu-id="c9703-351">Instalar nginx ou httpd, implantar um aplicativo web e ver o tráfego de saudação fluxo por meio de tooboth de Balanceador de carga Olá de VMs de saudação.</span><span class="sxs-lookup"><span data-stu-id="c9703-351">You can install nginx or httpd, deploy a web app, and see hello traffic flow through hello load balancer tooboth of hello VMs.</span></span>

```azurecli
azure vm show --resource-group myResourceGroup --name myVM1
```

<span data-ttu-id="c9703-352">Saída:</span><span class="sxs-lookup"><span data-stu-id="c9703-352">Output:</span></span>

```azurecli
info:    Executing command vm show
+ Looking up hello VM "TestVM1"
+ Looking up hello NIC "myNic1"
data:    Id                              :/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM1
data:    ProvisioningState               :Succeeded
data:    Name                            :myVM1
data:    Location                        :westeurope
data:    Type                            :Microsoft.Compute/virtualMachines
data:
data:    Hardware Profile:
data:      Size                          :Standard_DS1
data:
data:    Storage Profile:
data:      Image reference:
data:        Publisher                   :canonical
data:        Offer                       :UbuntuServer
data:        Sku                         :16.04.0-LTS
data:        Version                     :latest
data:
data:      OS Disk:
data:        OSType                      :Linux
data:        Name                        :clib45a8b650f4428a1-os-1471973896525
data:        Caching                     :ReadWrite
data:        CreateOption                :FromImage
data:        Vhd:
data:          Uri                       :https://mystorageaccount.blob.core.windows.net/vhds/clib45a8b650f4428a1-os-1471973896525.vhd
data:
data:    OS Profile:
data:      Computer Name                 :myVM1
data:      User Name                     :ops
data:      Linux Configuration:
data:        Disable Password Auth       :true
data:
data:    Network Profile:
data:      Network Interfaces:
data:        Network Interface #1:
data:          Primary                   :true
data:          MAC Address               :00-0D-3A-24-D4-AA
data:          Provisioning State        :Succeeded
data:          Name                      :LmyNic1
data:          Location                  :westeurope
data:
data:    AvailabilitySet:
data:      Id                            :/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Compute/availabilitySets/myAvailabilitySet
data:
data:    Diagnostics Profile:
data:      BootDiagnostics Enabled       :true
data:      BootDiagnostics StorageUri    :https://mystorageaccount.blob.core.windows.net/
data:
data:      Diagnostics Instance View:
info:    vm show command OK

```


## <a name="export-hello-environment-as-a-template"></a><span data-ttu-id="c9703-353">Ambiente de saudação de exportação como um modelo</span><span class="sxs-lookup"><span data-stu-id="c9703-353">Export hello environment as a template</span></span>
<span data-ttu-id="c9703-354">Agora que você criou esse ambiente, e se você quiser toocreate um ambiente de desenvolvimento adicional com hello os mesmos parâmetros, ou em um ambiente de produção que faz a correspondência?</span><span class="sxs-lookup"><span data-stu-id="c9703-354">Now that you have built out this environment, what if you want toocreate an additional development environment with hello same parameters, or a production environment that matches it?</span></span> <span data-ttu-id="c9703-355">Gerenciador de recursos usa modelos JSON que define todos os parâmetros de saudação para seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="c9703-355">Resource Manager uses JSON templates that define all hello parameters for your environment.</span></span> <span data-ttu-id="c9703-356">Crie ambientes inteiros fazendo referência a esse modelo JSON.</span><span class="sxs-lookup"><span data-stu-id="c9703-356">You build out entire environments by referencing this JSON template.</span></span> <span data-ttu-id="c9703-357">Você pode [criar modelos JSON manualmente](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) ou exportar um modelo existente do ambiente toocreate Olá JSON para você:</span><span class="sxs-lookup"><span data-stu-id="c9703-357">You can [build JSON templates manually](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) or export an existing environment toocreate hello JSON template for you:</span></span>

```azurecli
azure group export --name myResourceGroup
```

<span data-ttu-id="c9703-358">Este comando cria Olá `myResourceGroup.json` arquivo no diretório de trabalho atual.</span><span class="sxs-lookup"><span data-stu-id="c9703-358">This command creates hello `myResourceGroup.json` file in your current working directory.</span></span> <span data-ttu-id="c9703-359">Quando você cria um ambiente com base neste modelo, você será solicitado para todos os nomes de recurso hello, incluindo nomes de saudação para o balanceador de carga hello, interfaces de rede ou VMs.</span><span class="sxs-lookup"><span data-stu-id="c9703-359">When you create an environment from this template, you are prompted for all hello resource names, including hello names for hello load balancer, network interfaces, or VMs.</span></span> <span data-ttu-id="c9703-360">Você pode preencher esses nomes em seu arquivo de modelo adicionando Olá `-p` ou `--includeParameterDefaultValue` toohello parâmetro `azure group export` comando que foi mostrado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="c9703-360">You can populate these names in your template file by adding hello `-p` or `--includeParameterDefaultValue` parameter toohello `azure group export` command that was shown earlier.</span></span> <span data-ttu-id="c9703-361">Editar os nomes de recurso do JSON modelo toospecify hello, ou [criar um arquivo parameters.json](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) que especifica os nomes de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="c9703-361">Edit your JSON template toospecify hello resource names, or [create a parameters.json file](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) that specifies hello resource names.</span></span>

<span data-ttu-id="c9703-362">toocreate um ambiente de seu modelo:</span><span class="sxs-lookup"><span data-stu-id="c9703-362">toocreate an environment from your template:</span></span>

```azurecli
azure group deployment create --resource-group myNewResourceGroup \
  --template-file myResourceGroup.json
```

<span data-ttu-id="c9703-363">Talvez você queira tooread [mais informações sobre como toodeploy modelos](../../resource-group-template-deploy-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c9703-363">You might want tooread [more about how toodeploy from templates](../../resource-group-template-deploy-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="c9703-364">Saiba mais sobre como tooincrementally ambientes de atualização, use o arquivo de parâmetros de saudação e acessar os modelos de um único local de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="c9703-364">Learn about how tooincrementally update environments, use hello parameters file, and access templates from a single storage location.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c9703-365">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c9703-365">Next steps</span></span>
<span data-ttu-id="c9703-366">Agora você está pronto toobegin trabalhando com vários componentes de rede e máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="c9703-366">Now you're ready toobegin working with multiple networking components and VMs.</span></span> <span data-ttu-id="c9703-367">Você pode usar este toobuild do ambiente de exemplo do aplicativo usando os componentes principais do hello introduzidos aqui.</span><span class="sxs-lookup"><span data-stu-id="c9703-367">You can use this sample environment toobuild out your application by using hello core components introduced here.</span></span>
