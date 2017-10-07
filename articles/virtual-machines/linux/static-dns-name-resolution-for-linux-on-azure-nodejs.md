---
title: "aaaUsing resolução no Azure de nome de DNS interno de VM | Microsoft Docs"
description: "Usando o DNS interno para a resolução de nomes da VM no Azure."
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 12/05/2016
ms.author: v-livech
ms.openlocfilehash: 94fd6577aa51ce5db4dc26649b415ddeeb410eb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-internal-dns-for-vm-name-resolution-on-azure"></a><span data-ttu-id="0cec9-103">Usando o DNS interno para a resolução de nomes da VM no Azure</span><span class="sxs-lookup"><span data-stu-id="0cec9-103">Using internal DNS for VM name resolution on Azure</span></span>

<span data-ttu-id="0cec9-104">Este artigo mostra como tooset estático interno nomes DNS para VMs do Linux usando cartões de NIC Virtual (VNic) e nomes de rótulo DNS.</span><span class="sxs-lookup"><span data-stu-id="0cec9-104">This article shows how tooset static internal DNS names for Linux VMs using Virtual NIC cards (VNic) and DNS label names.</span></span> <span data-ttu-id="0cec9-105">Nomes DNS estáticos são usados para serviços de infraestrutura permanentes como um servidor de build Jenkins, que é usado para este documento ou um servidor Git.</span><span class="sxs-lookup"><span data-stu-id="0cec9-105">Static DNS names are used for permanent infrastructure services like a Jenkins build server, which is used for this document, or a Git server.</span></span>

<span data-ttu-id="0cec9-106">requisitos de saudação são:</span><span class="sxs-lookup"><span data-stu-id="0cec9-106">hello requirements are:</span></span>

* [<span data-ttu-id="0cec9-107">uma conta do Azure</span><span class="sxs-lookup"><span data-stu-id="0cec9-107">an Azure account</span></span>](https://azure.microsoft.com/pricing/free-trial/)
* [<span data-ttu-id="0cec9-108">arquivos de chave SSH pública e privada</span><span class="sxs-lookup"><span data-stu-id="0cec9-108">SSH public and private key files</span></span>](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="0cec9-109">Tarefa de saudação do CLI versões toocomplete</span><span class="sxs-lookup"><span data-stu-id="0cec9-109">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="0cec9-110">Você pode concluir a tarefa hello usando uma saudação versões da CLI a seguir:</span><span class="sxs-lookup"><span data-stu-id="0cec9-110">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="0cec9-111">[1.0 de CLI do Azure](#quick-commands) – nosso CLI para Olá clássico e o recurso de gerenciamento modelos de implantação (Este artigo)</span><span class="sxs-lookup"><span data-stu-id="0cec9-111">[Azure CLI 1.0](#quick-commands) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="0cec9-112">[2.0 do CLI do Azure](static-dns-name-resolution-for-linux-on-azure.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -nossa próxima geração CLI para o modelo de implantação do gerenciamento de recursos de saudação</span><span class="sxs-lookup"><span data-stu-id="0cec9-112">[Azure CLI 2.0](static-dns-name-resolution-for-linux-on-azure.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="0cec9-113">Comandos rápidos</span><span class="sxs-lookup"><span data-stu-id="0cec9-113">Quick commands</span></span>

<span data-ttu-id="0cec9-114">Se você precisar tooquickly realizar tarefa hello, Olá seção a seguir fornece detalhes sobre comandos Olá necessários.</span><span class="sxs-lookup"><span data-stu-id="0cec9-114">If you need tooquickly accomplish hello task, hello following section details hello commands needed.</span></span> <span data-ttu-id="0cec9-115">Obter mais informações e o contexto para cada etapa pode ser encontrada restante de saudação do documento hello, [Iniciar aqui](#detailed-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="0cec9-115">More detailed information and context for each step can be found hello rest of hello document, [starting here](#detailed-walkthrough).</span></span>  

<span data-ttu-id="0cec9-116">Pré-requisitos: Grupo de Recursos, VNet, NSG com SSH de entrada e Sub-rede.</span><span class="sxs-lookup"><span data-stu-id="0cec9-116">Pre-Requirements: Resource Group, VNet, NSG with SSH inbound, Subnet.</span></span>

### <a name="create-a-vnic-with-a-static-internal-dns-name"></a><span data-ttu-id="0cec9-117">Criar uma VNic com um nome DNS interno estático</span><span class="sxs-lookup"><span data-stu-id="0cec9-117">Create a VNic with a static internal DNS name</span></span>

<span data-ttu-id="0cec9-118">Olá `-r` cli sinalizador é para o rótulo DNS Olá de configuração, que fornece o nome DNS estático Olá para Olá VNic.</span><span class="sxs-lookup"><span data-stu-id="0cec9-118">hello `-r` cli flag is for setting hello DNS label, which provides hello static DNS name for hello VNic.</span></span>

```azurecli
azure network nic create jenkinsVNic \
-g myResourceGroup \
-l westus \
-m myVNet \
-k mySubNet \
-r jenkins
```

### <a name="deploy-hello-vm-into-hello-vnet-nsg-and-connect-hello-vnic"></a><span data-ttu-id="0cec9-119">Implantar Olá VM em Olá VNet, NSG e conectar Olá VNic</span><span class="sxs-lookup"><span data-stu-id="0cec9-119">Deploy hello VM into hello VNet, NSG and, connect hello VNic</span></span>

<span data-ttu-id="0cec9-120">Olá `-N` conecta Olá VNic toohello nova máquina virtual durante a saudação tooAzure de implantação.</span><span class="sxs-lookup"><span data-stu-id="0cec9-120">hello `-N` connects hello VNic toohello new VM during hello deployment tooAzure.</span></span>

```azurecli
azure vm create jenkins \
-g myResourceGroup \
-l westus \
-y linux \
-Q Debian \
-o myStorageAcct \
-u myAdminUser \
-M ~/.ssh/id_rsa.pub \
-F myVNet \
-j mySubnet \
-N jenkinsVNic
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="0cec9-121">Passo a passo detalhado</span><span class="sxs-lookup"><span data-stu-id="0cec9-121">Detailed walkthrough</span></span>

<span data-ttu-id="0cec9-122">Uma implantação contínua (CiCd) e integração contínua completo infra-estrutura no Azure exige que determinados servidores de servidores toobe vida longa ou estático.</span><span class="sxs-lookup"><span data-stu-id="0cec9-122">A full continuous integration and continuous deployment (CiCd) infrastructure on Azure requires certain servers toobe static or long-lived servers.</span></span>  <span data-ttu-id="0cec9-123">É recomendável que os ativos do Azure como saudação de redes virtuais (VNets) e grupos de segurança de rede (NSGs), deve ser estáticos e vida útil longa recursos que raramente são implantados.</span><span class="sxs-lookup"><span data-stu-id="0cec9-123">It is recommended that Azure assets like hello Virtual Networks (VNets) and Network Security Groups (NSGs), should be static and long lived resources that are rarely deployed.</span></span>  <span data-ttu-id="0cec9-124">Quando uma rede virtual tiver sido implantada, ele pode ser reutilizado por novas implantações sem nenhuma infraestrutura de toohello efeitos adversos.</span><span class="sxs-lookup"><span data-stu-id="0cec9-124">Once a VNet has been deployed, it can be reused by new deployments without any adverse affects toohello infrastructure.</span></span>  <span data-ttu-id="0cec9-125">Adicionando rede estática de toothis um Git servidor do repositório e um servidor de automação Jenkins oferece CiCd tooyour ambientes de desenvolvimento ou teste.</span><span class="sxs-lookup"><span data-stu-id="0cec9-125">Adding toothis static network a Git repository server and a Jenkins automation server delivers CiCd tooyour development or test environments.</span></span>  

<span data-ttu-id="0cec9-126">Nomes DNS internos podem ser resolvidos apenas em uma rede virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="0cec9-126">Internal DNS names are only resolvable inside an Azure virtual network.</span></span>  <span data-ttu-id="0cec9-127">Como os nomes DNS Olá são internos, eles não são toohello resolvível fora da internet, fornecendo a infra-estrutura de toohello de segurança adicional.</span><span class="sxs-lookup"><span data-stu-id="0cec9-127">Because hello DNS names are internal, they are not resolvable toohello outside internet, providing additional security toohello infrastructure.</span></span>

<span data-ttu-id="0cec9-128">_Substitua os exemplos por sua própria nomenclatura._</span><span class="sxs-lookup"><span data-stu-id="0cec9-128">_Replace any examples with your own naming._</span></span>

## <a name="create-hello-resource-group"></a><span data-ttu-id="0cec9-129">Criar grupo de recursos de saudação</span><span class="sxs-lookup"><span data-stu-id="0cec9-129">Create hello Resource group</span></span>

<span data-ttu-id="0cec9-130">Um grupo de recursos é necessário tooorganize tudo o que podemos criar neste passo a passo.</span><span class="sxs-lookup"><span data-stu-id="0cec9-130">A Resource Group is needed tooorganize everything we create in this walkthrough.</span></span>  <span data-ttu-id="0cec9-131">Para obter mais informações sobre os Grupos de Recursos do Azure, consulte [Visão geral do Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="0cec9-131">For more information on Azure Resource Groups, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

```azurecli
azure group create myResourceGroup \
--location westus
```

## <a name="create-hello-vnet"></a><span data-ttu-id="0cec9-132">Criar hello VNet</span><span class="sxs-lookup"><span data-stu-id="0cec9-132">Create hello VNet</span></span>

<span data-ttu-id="0cec9-133">Olá primeira etapa é toobuild toolaunch uma rede virtual Olá VMs em.</span><span class="sxs-lookup"><span data-stu-id="0cec9-133">hello first step is toobuild a VNet toolaunch hello VMs into.</span></span>  <span data-ttu-id="0cec9-134">Olá VNet contém uma sub-rede para este passo a passo.</span><span class="sxs-lookup"><span data-stu-id="0cec9-134">hello VNet contains one subnet for this walkthrough.</span></span>  <span data-ttu-id="0cec9-135">Para obter mais informações sobre VNets do Azure, consulte [criar uma rede virtual usando Olá CLI do Azure](../../virtual-network/virtual-networks-create-vnet-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="0cec9-135">For more information on Azure VNets, see [Create a virtual network by using hello Azure CLI](../../virtual-network/virtual-networks-create-vnet-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

```azurecli
azure network vnet create myVNet \
--resource-group myResourceGroup \
--address-prefixes 10.10.0.0/24 \
--location westus
```

## <a name="create-hello-nsg"></a><span data-ttu-id="0cec9-136">Criar hello NSG</span><span class="sxs-lookup"><span data-stu-id="0cec9-136">Create hello NSG</span></span>

<span data-ttu-id="0cec9-137">Olá sub-rede é criado por trás de um grupo de segurança de rede existente, de forma que criamos Olá NSG antes Olá sub-rede.</span><span class="sxs-lookup"><span data-stu-id="0cec9-137">hello Subnet is built behind an existing Network Security Group so we build hello NSG before hello Subnet.</span></span>  <span data-ttu-id="0cec9-138">Os NSGs do Azure são equivalentes tooa firewall na camada de rede de saudação.</span><span class="sxs-lookup"><span data-stu-id="0cec9-138">Azure NSGs are equivalent tooa firewall at hello network layer.</span></span>  <span data-ttu-id="0cec9-139">Para obter mais informações sobre os NSGs do Azure, consulte [como NSGs toocreate em Olá CLI do Azure](../../virtual-network/virtual-networks-create-nsg-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="0cec9-139">For more information on Azure NSGs, see [How toocreate NSGs in hello Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

```azurecli
azure network nsg create myNSG \
--resource-group myResourceGroup \
--location westus
```

## <a name="add-an-inbound-ssh-allow-rule"></a><span data-ttu-id="0cec9-140">Adicionar uma regra de permissão de SSH de entrada</span><span class="sxs-lookup"><span data-stu-id="0cec9-140">Add an inbound SSH allow rule</span></span>

<span data-ttu-id="0cec9-141">Olá VM Linux precisa ter acesso de saudação à internet para que uma regra que permite a porta de entrada 22 tráfego toobe passado Olá rede tooport 22 na Olá VM do Linux é necessária.</span><span class="sxs-lookup"><span data-stu-id="0cec9-141">hello Linux VM needs access from hello internet so a rule allowing inbound port 22 traffic toobe passed through hello network tooport 22 on hello Linux VM is needed.</span></span>

```azurecli
azure network nsg rule create inboundSSH \
--resource-group myResourceGroup \
--nsg-name myNSG \
--access Allow \
--protocol Tcp \
--direction Inbound \
--priority 100 \
--source-address-prefix * \
--source-port-range * \
--destination-address-prefix 10.10.0.0/24 \
--destination-port-range 22
```

## <a name="add-a-subnet-toohello-vnet"></a><span data-ttu-id="0cec9-142">Adicionar toohello uma sub-rede VNet</span><span class="sxs-lookup"><span data-stu-id="0cec9-142">Add a subnet toohello VNet</span></span>

<span data-ttu-id="0cec9-143">VMs em redes de saudação devem estar localizadas em uma sub-rede.</span><span class="sxs-lookup"><span data-stu-id="0cec9-143">VMs within hello VNet must be located in a subnet.</span></span>  <span data-ttu-id="0cec9-144">Cada VNET pode ter várias sub-redes.</span><span class="sxs-lookup"><span data-stu-id="0cec9-144">Each VNet can have multiple subnets.</span></span>  <span data-ttu-id="0cec9-145">Criar uma sub-rede hello e associar sub-redes Olá Olá NSG tooadd uma sub-rede de toohello do firewall.</span><span class="sxs-lookup"><span data-stu-id="0cec9-145">Create hello subnet and associate hello subnet with hello NSG tooadd a firewall toohello subnet.</span></span>

```azurecli
azure network vnet subnet create mySubNet \
--resource-group myResourceGroup \
--vnet-name myVNet \
--address-prefix 10.10.0.0/26 \
--network-security-group-name myNSG
```

<span data-ttu-id="0cec9-146">Olá sub-rede agora é adicionada Olá VNet e associado ao hello NSG e regras do NSG hello.</span><span class="sxs-lookup"><span data-stu-id="0cec9-146">hello Subnet is now added inside hello VNet and associated with hello NSG and hello NSG rule.</span></span>

## <a name="creating-static-dns-names"></a><span data-ttu-id="0cec9-147">Criando nomes DNS estáticos</span><span class="sxs-lookup"><span data-stu-id="0cec9-147">Creating static DNS names</span></span>

<span data-ttu-id="0cec9-148">O Azure é muito flexível, mas toouse nomes DNS para resolução de nomes de máquinas virtuais, você precisa toocreate-los como Virtual cartões (VNics) usando o DNS de rotulagem de rede.</span><span class="sxs-lookup"><span data-stu-id="0cec9-148">Azure is very flexible, but toouse DNS names for VMs name resolution, you need toocreate them as Virtual network cards (VNics) using DNS labeling.</span></span>  <span data-ttu-id="0cec9-149">VNics são importantes para você pode reutilizá-los, conectando-os toodifferent VMs, que mantém Olá VNic como um recurso estático, enquanto Olá VMs pode ser temporário.</span><span class="sxs-lookup"><span data-stu-id="0cec9-149">VNics are important as you can reuse them by connecting them toodifferent VMs, which keeps hello VNic as a static resource while hello VMs can be temporary.</span></span>  <span data-ttu-id="0cec9-150">Usando o DNS rótulos nos Olá VNic, estamos tooenable capaz de resolução de nome simples de outras VMs em redes de saudação.</span><span class="sxs-lookup"><span data-stu-id="0cec9-150">By using DNS labeling on hello VNic, we are able tooenable simple name resolution from other VMs in hello VNet.</span></span>  <span data-ttu-id="0cec9-151">Usando nomes resolvível permite que outro servidor de automação VMs tooaccess Olá por nome DNS Olá `Jenkins` ou servidor de Git hello como `gitrepo`.</span><span class="sxs-lookup"><span data-stu-id="0cec9-151">Using resolvable names enables other VMs tooaccess hello automation server by hello DNS name `Jenkins` or hello Git server as `gitrepo`.</span></span>  <span data-ttu-id="0cec9-152">Crie uma VNic e associá-lo a saudação que sub-rede criada na etapa anterior hello.</span><span class="sxs-lookup"><span data-stu-id="0cec9-152">Create a VNic and associate it with hello Subnet created in hello previous step.</span></span>

```azurecli
azure network nic create jenkinsVNic \
-g myResourceGroup \
-l westus \
-m myVNet \
-k mySubNet \
-r jenkins
```

## <a name="deploy-hello-vm-into-hello-vnet-and-nsg"></a><span data-ttu-id="0cec9-153">Implantar hello VM em Olá VNet e NSG</span><span class="sxs-lookup"><span data-stu-id="0cec9-153">Deploy hello VM into hello VNet and NSG</span></span>

<span data-ttu-id="0cec9-154">Agora temos uma rede virtual, uma sub-rede dentro dessa rede virtual e um NSG atuando como um firewall tooprotect nosso sub-rede bloqueando todo o tráfego de entrada exceto 22 de porta para o SSH.</span><span class="sxs-lookup"><span data-stu-id="0cec9-154">We now have a VNet, a subnet inside that VNet, and an NSG acting as a firewall tooprotect our subnet by blocking all inbound traffic except port 22 for SSH.</span></span>  <span data-ttu-id="0cec9-155">Olá VM agora pode ser implantado nessa infraestrutura de rede existente.</span><span class="sxs-lookup"><span data-stu-id="0cec9-155">hello VM can now be deployed inside this existing network infrastructure.</span></span>

<span data-ttu-id="0cec9-156">Usando Olá CLI do Azure e Olá `azure vm create` comando, Olá VM do Linux é implantado toohello grupo de recursos do Azure, redes, sub-rede e VNic existentes.</span><span class="sxs-lookup"><span data-stu-id="0cec9-156">Using hello Azure CLI, and hello `azure vm create` command, hello Linux VM is deployed toohello existing Azure Resource Group, VNet, Subnet, and VNic.</span></span>  <span data-ttu-id="0cec9-157">Para obter mais informações sobre como usar o hello CLI toodeploy uma VM completa, consulte [criar um ambiente completo do Linux usando Olá CLI do Azure](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="0cec9-157">For more information on using hello CLI toodeploy a complete VM, see [Create a complete Linux environment by using hello Azure CLI](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

```azurecli
azure vm create jenkins \
--resource-group myResourceGroup myVM \
--location westus \
--os-type linux \
--image-urn Debian \
--storage-account-name mystorageaccount \
--admin-username myAdminUser \
--ssh-publickey-file ~/.ssh/id_rsa.pub \
--vnet-name myVNet \
--vnet-subnet-name mySubnet \
--nic-name jenkinsVNic
```

<span data-ttu-id="0cec9-158">Usando Olá CLI sinalizadores de toocall recursos existentes, podemos instruir Olá toodeploy Azure VM dentro da rede existente hello.</span><span class="sxs-lookup"><span data-stu-id="0cec9-158">By using hello CLI flags toocall out existing resources, we instruct Azure toodeploy hello VM inside hello existing network.</span></span>  <span data-ttu-id="0cec9-159">tooreiterate, depois que uma rede virtual e a sub-rede forem implantados, eles podem ser mantidos como estáticos ou permanentes de recursos dentro de sua região do Azure.</span><span class="sxs-lookup"><span data-stu-id="0cec9-159">tooreiterate, once a VNet and subnet have been deployed, they can be left as static or permanent resources inside your Azure region.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="0cec9-160">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0cec9-160">Next steps</span></span>
* [<span data-ttu-id="0cec9-161">Criar seu próprio ambiente personalizado para uma VM do Linux usando os comandos da CLI do Azure diretamente</span><span class="sxs-lookup"><span data-stu-id="0cec9-161">Create your own custom environment for a Linux VM using Azure CLI commands directly</span></span>](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="0cec9-162">Criar uma VM do Linux no Azure usando modelos</span><span class="sxs-lookup"><span data-stu-id="0cec9-162">Create a Linux VM on Azure using templates</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
