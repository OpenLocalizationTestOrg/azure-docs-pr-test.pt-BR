---
title: "Usando o DNS interno para a resolução de nomes da VM no Azure | Microsoft Docs"
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
ms.openlocfilehash: bfba2cf38a0624e8480a32bf153f391d820da5a1
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="using-internal-dns-for-vm-name-resolution-on-azure"></a><span data-ttu-id="544e2-103">Usando o DNS interno para a resolução de nomes da VM no Azure</span><span class="sxs-lookup"><span data-stu-id="544e2-103">Using internal DNS for VM name resolution on Azure</span></span>

<span data-ttu-id="544e2-104">Este artigo mostra como definir nomes DNS internos estáticos para VMs Linux usando VNic (Placas NIC virtuais) e nomes de rótulo DNS.</span><span class="sxs-lookup"><span data-stu-id="544e2-104">This article shows how to set static internal DNS names for Linux VMs using Virtual NIC cards (VNic) and DNS label names.</span></span> <span data-ttu-id="544e2-105">Nomes DNS estáticos são usados para serviços de infraestrutura permanentes como um servidor de build Jenkins, que é usado para este documento ou um servidor Git.</span><span class="sxs-lookup"><span data-stu-id="544e2-105">Static DNS names are used for permanent infrastructure services like a Jenkins build server, which is used for this document, or a Git server.</span></span>

<span data-ttu-id="544e2-106">Esses requisitos são:</span><span class="sxs-lookup"><span data-stu-id="544e2-106">The requirements are:</span></span>

* [<span data-ttu-id="544e2-107">uma conta do Azure</span><span class="sxs-lookup"><span data-stu-id="544e2-107">an Azure account</span></span>](https://azure.microsoft.com/pricing/free-trial/)
* [<span data-ttu-id="544e2-108">arquivos de chave SSH pública e privada</span><span class="sxs-lookup"><span data-stu-id="544e2-108">SSH public and private key files</span></span>](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)


## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="544e2-109">Versões da CLI para concluir a tarefa</span><span class="sxs-lookup"><span data-stu-id="544e2-109">CLI versions to complete the task</span></span>
<span data-ttu-id="544e2-110">Você pode concluir a tarefa usando uma das seguintes versões da CLI:</span><span class="sxs-lookup"><span data-stu-id="544e2-110">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="544e2-111">[CLI 1.0 do Azure](#quick-commands) – nossa CLI para os modelos de implantação clássico e de gerenciamento de recursos (este artigo)</span><span class="sxs-lookup"><span data-stu-id="544e2-111">[Azure CLI 1.0](#quick-commands) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="544e2-112">[CLI 2.0 do Azure](static-dns-name-resolution-for-linux-on-azure.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) – nossa última geração de CLI para o modelo de implantação de gerenciamento de recursos</span><span class="sxs-lookup"><span data-stu-id="544e2-112">[Azure CLI 2.0](static-dns-name-resolution-for-linux-on-azure.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="544e2-113">Comandos rápidos</span><span class="sxs-lookup"><span data-stu-id="544e2-113">Quick commands</span></span>

<span data-ttu-id="544e2-114">Se você precisar executar a tarefa rapidamente, a seção a seguir fornecerá detalhes dos comandos necessários.</span><span class="sxs-lookup"><span data-stu-id="544e2-114">If you need to quickly accomplish the task, the following section details the commands needed.</span></span> <span data-ttu-id="544e2-115">Mais informações detalhadas e contexto para cada etapa podem ser encontrados no restante do documento, [começando aqui](#detailed-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="544e2-115">More detailed information and context for each step can be found the rest of the document, [starting here](#detailed-walkthrough).</span></span>  

<span data-ttu-id="544e2-116">Pré-requisitos: Grupo de Recursos, VNet, NSG com SSH de entrada e Sub-rede.</span><span class="sxs-lookup"><span data-stu-id="544e2-116">Pre-Requirements: Resource Group, VNet, NSG with SSH inbound, Subnet.</span></span>

### <a name="create-a-vnic-with-a-static-internal-dns-name"></a><span data-ttu-id="544e2-117">Criar uma VNic com um nome DNS interno estático</span><span class="sxs-lookup"><span data-stu-id="544e2-117">Create a VNic with a static internal DNS name</span></span>

<span data-ttu-id="544e2-118">O sinalizador `-r` da CLI serve para definir o rótulo DNS, que fornece o nome DNS estático para a VNic.</span><span class="sxs-lookup"><span data-stu-id="544e2-118">The `-r` cli flag is for setting the DNS label, which provides the static DNS name for the VNic.</span></span>

```azurecli
azure network nic create jenkinsVNic \
-g myResourceGroup \
-l westus \
-m myVNet \
-k mySubNet \
-r jenkins
```

### <a name="deploy-the-vm-into-the-vnet-nsg-and-connect-the-vnic"></a><span data-ttu-id="544e2-119">Implantar a VM na VNet, no NSG e conectar à VNic</span><span class="sxs-lookup"><span data-stu-id="544e2-119">Deploy the VM into the VNet, NSG and, connect the VNic</span></span>

<span data-ttu-id="544e2-120">O `-N` conecta a VNic à nova VM durante a implantação no Azure.</span><span class="sxs-lookup"><span data-stu-id="544e2-120">The `-N` connects the VNic to the new VM during the deployment to Azure.</span></span>

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

## <a name="detailed-walkthrough"></a><span data-ttu-id="544e2-121">Passo a passo detalhado</span><span class="sxs-lookup"><span data-stu-id="544e2-121">Detailed walkthrough</span></span>

<span data-ttu-id="544e2-122">Uma infraestrutura completa de CiCd (implantação e integração contínuas) no Azure exige que alguns servidores sejam estáticos ou de longa duração.</span><span class="sxs-lookup"><span data-stu-id="544e2-122">A full continuous integration and continuous deployment (CiCd) infrastructure on Azure requires certain servers to be static or long-lived servers.</span></span>  <span data-ttu-id="544e2-123">É recomendável que os ativos do Azure, como as VNets (Redes Virtuais) e os NSGs (Grupos de Segurança de Rede), sejam recursos estáticos e de longa duração que raramente são implantados.</span><span class="sxs-lookup"><span data-stu-id="544e2-123">It is recommended that Azure assets like the Virtual Networks (VNets) and Network Security Groups (NSGs), should be static and long lived resources that are rarely deployed.</span></span>  <span data-ttu-id="544e2-124">Após a implantação de uma VNET, ela pode ser reutilizada por novas implantações sem nenhum efeito negativo sobre a infraestrutura.</span><span class="sxs-lookup"><span data-stu-id="544e2-124">Once a VNet has been deployed, it can be reused by new deployments without any adverse affects to the infrastructure.</span></span>  <span data-ttu-id="544e2-125">A adição de um servidor de repositório Git e um servidor de automação Jenkins a essa rede estática oferece CiCd para os ambientes de desenvolvimento ou teste.</span><span class="sxs-lookup"><span data-stu-id="544e2-125">Adding to this static network a Git repository server and a Jenkins automation server delivers CiCd to your development or test environments.</span></span>  

<span data-ttu-id="544e2-126">Nomes DNS internos podem ser resolvidos apenas em uma rede virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="544e2-126">Internal DNS names are only resolvable inside an Azure virtual network.</span></span>  <span data-ttu-id="544e2-127">Como os nomes DNS são internos, eles não podem ser resolvidos para a Internet externa, fornecendo segurança adicional para a infraestrutura.</span><span class="sxs-lookup"><span data-stu-id="544e2-127">Because the DNS names are internal, they are not resolvable to the outside internet, providing additional security to the infrastructure.</span></span>

<span data-ttu-id="544e2-128">_Substitua os exemplos por sua própria nomenclatura._</span><span class="sxs-lookup"><span data-stu-id="544e2-128">_Replace any examples with your own naming._</span></span>

## <a name="create-the-resource-group"></a><span data-ttu-id="544e2-129">Criar o Grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="544e2-129">Create the Resource group</span></span>

<span data-ttu-id="544e2-130">Um Grupo de Recursos é necessário para organizar tudo o que criamos neste passo a passo.</span><span class="sxs-lookup"><span data-stu-id="544e2-130">A Resource Group is needed to organize everything we create in this walkthrough.</span></span>  <span data-ttu-id="544e2-131">Para obter mais informações sobre os Grupos de Recursos do Azure, consulte [Visão geral do Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="544e2-131">For more information on Azure Resource Groups, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

```azurecli
azure group create myResourceGroup \
--location westus
```

## <a name="create-the-vnet"></a><span data-ttu-id="544e2-132">Criar a VNET</span><span class="sxs-lookup"><span data-stu-id="544e2-132">Create the VNet</span></span>

<span data-ttu-id="544e2-133">A primeira etapa é criar uma VNET na qual as VMs serão iniciadas.</span><span class="sxs-lookup"><span data-stu-id="544e2-133">The first step is to build a VNet to launch the VMs into.</span></span>  <span data-ttu-id="544e2-134">A VNET contém uma sub-rede para este passo a passo.</span><span class="sxs-lookup"><span data-stu-id="544e2-134">The VNet contains one subnet for this walkthrough.</span></span>  <span data-ttu-id="544e2-135">Para obter mais informações sobre as VNETs do Azure, consulte [Criar uma rede virtual usando a CLI do Azure](../../virtual-network/virtual-networks-create-vnet-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="544e2-135">For more information on Azure VNets, see [Create a virtual network by using the Azure CLI](../../virtual-network/virtual-networks-create-vnet-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

```azurecli
azure network vnet create myVNet \
--resource-group myResourceGroup \
--address-prefixes 10.10.0.0/24 \
--location westus
```

## <a name="create-the-nsg"></a><span data-ttu-id="544e2-136">Criar o NSG</span><span class="sxs-lookup"><span data-stu-id="544e2-136">Create the NSG</span></span>

<span data-ttu-id="544e2-137">A Sub-rede é criada por trás de um Grupo de Segurança de Rede existente e, portanto, criamos o NSG antes da Sub-rede.</span><span class="sxs-lookup"><span data-stu-id="544e2-137">The Subnet is built behind an existing Network Security Group so we build the NSG before the Subnet.</span></span>  <span data-ttu-id="544e2-138">Os NSGs do Azure são equivalentes a um firewall na camada de rede.</span><span class="sxs-lookup"><span data-stu-id="544e2-138">Azure NSGs are equivalent to a firewall at the network layer.</span></span>  <span data-ttu-id="544e2-139">Para obter mais informações sobre os NSGs do Azure, consulte [Como criar NSGs na CLI do Azure](../../virtual-network/virtual-networks-create-nsg-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="544e2-139">For more information on Azure NSGs, see [How to create NSGs in the Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

```azurecli
azure network nsg create myNSG \
--resource-group myResourceGroup \
--location westus
```

## <a name="add-an-inbound-ssh-allow-rule"></a><span data-ttu-id="544e2-140">Adicionar uma regra de permissão de SSH de entrada</span><span class="sxs-lookup"><span data-stu-id="544e2-140">Add an inbound SSH allow rule</span></span>

<span data-ttu-id="544e2-141">A VM do Linux precisa de acesso da Internet e, portanto, é necessária uma regra permitindo que o tráfego da porta 22 de entrada passe pela rede para a porta 22 na VM do Linux.</span><span class="sxs-lookup"><span data-stu-id="544e2-141">The Linux VM needs access from the internet so a rule allowing inbound port 22 traffic to be passed through the network to port 22 on the Linux VM is needed.</span></span>

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

## <a name="add-a-subnet-to-the-vnet"></a><span data-ttu-id="544e2-142">Adicionar uma sub-rede à VNET</span><span class="sxs-lookup"><span data-stu-id="544e2-142">Add a subnet to the VNet</span></span>

<span data-ttu-id="544e2-143">As VMs na VNET devem estar localizadas em uma sub-rede.</span><span class="sxs-lookup"><span data-stu-id="544e2-143">VMs within the VNet must be located in a subnet.</span></span>  <span data-ttu-id="544e2-144">Cada VNET pode ter várias sub-redes.</span><span class="sxs-lookup"><span data-stu-id="544e2-144">Each VNet can have multiple subnets.</span></span>  <span data-ttu-id="544e2-145">Crie a sub-rede e associe-a ao NSG para adicionar um firewall à sub-rede.</span><span class="sxs-lookup"><span data-stu-id="544e2-145">Create the subnet and associate the subnet with the NSG to add a firewall to the subnet.</span></span>

```azurecli
azure network vnet subnet create mySubNet \
--resource-group myResourceGroup \
--vnet-name myVNet \
--address-prefix 10.10.0.0/26 \
--network-security-group-name myNSG
```

<span data-ttu-id="544e2-146">Agora, a Sub-rede é adicionada à VNET e associada ao NSG e à regra do NSG.</span><span class="sxs-lookup"><span data-stu-id="544e2-146">The Subnet is now added inside the VNet and associated with the NSG and the NSG rule.</span></span>

## <a name="creating-static-dns-names"></a><span data-ttu-id="544e2-147">Criando nomes DNS estáticos</span><span class="sxs-lookup"><span data-stu-id="544e2-147">Creating static DNS names</span></span>

<span data-ttu-id="544e2-148">O Azure é muito flexível, mas para usar nomes DNS para a resolução de nomes de VMs, você precisa criá-los como VNics (Placas de rede virtual) usando a rotulagem DNS.</span><span class="sxs-lookup"><span data-stu-id="544e2-148">Azure is very flexible, but to use DNS names for VMs name resolution, you need to create them as Virtual network cards (VNics) using DNS labeling.</span></span>  <span data-ttu-id="544e2-149">As VNics são importantes, pois você pode reutilizá-las conectando-as a VMs diferentes, o que mantém a VNic como um recurso estático, enquanto as VMs podem ser temporárias.</span><span class="sxs-lookup"><span data-stu-id="544e2-149">VNics are important as you can reuse them by connecting them to different VMs, which keeps the VNic as a static resource while the VMs can be temporary.</span></span>  <span data-ttu-id="544e2-150">Ao usar a rotulagem DNS na VNic, podemos habilitar a resolução de nomes simples em outras VMs na VNet.</span><span class="sxs-lookup"><span data-stu-id="544e2-150">By using DNS labeling on the VNic, we are able to enable simple name resolution from other VMs in the VNet.</span></span>  <span data-ttu-id="544e2-151">Usar nomes que podem ser resolvidos permite que outras VMs acessem o servidor de automação com o nome DNS `Jenkins` ou o servidor Git como `gitrepo`.</span><span class="sxs-lookup"><span data-stu-id="544e2-151">Using resolvable names enables other VMs to access the automation server by the DNS name `Jenkins` or the Git server as `gitrepo`.</span></span>  <span data-ttu-id="544e2-152">Crie uma VNic e associe-a à Sub-rede criada na etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="544e2-152">Create a VNic and associate it with the Subnet created in the previous step.</span></span>

```azurecli
azure network nic create jenkinsVNic \
-g myResourceGroup \
-l westus \
-m myVNet \
-k mySubNet \
-r jenkins
```

## <a name="deploy-the-vm-into-the-vnet-and-nsg"></a><span data-ttu-id="544e2-153">Implantar a VM na VNET e no NSG</span><span class="sxs-lookup"><span data-stu-id="544e2-153">Deploy the VM into the VNet and NSG</span></span>

<span data-ttu-id="544e2-154">Agora temos uma VNET, uma sub-rede nela e um NSG atuando como um firewall, para proteger nossa sub-rede bloqueando todo o tráfego de entrada, exceto pela porta 22 para o SSH.</span><span class="sxs-lookup"><span data-stu-id="544e2-154">We now have a VNet, a subnet inside that VNet, and an NSG acting as a firewall to protect our subnet by blocking all inbound traffic except port 22 for SSH.</span></span>  <span data-ttu-id="544e2-155">Agora a VM pode ser implantada nessa infraestrutura de rede existente.</span><span class="sxs-lookup"><span data-stu-id="544e2-155">The VM can now be deployed inside this existing network infrastructure.</span></span>

<span data-ttu-id="544e2-156">Usando a CLI do Azure e o comando `azure vm create`, a VM do Linux é implantada no Grupo de Recursos do Azure, na VNET, na Sub-rede e na VNic existentes.</span><span class="sxs-lookup"><span data-stu-id="544e2-156">Using the Azure CLI, and the `azure vm create` command, the Linux VM is deployed to the existing Azure Resource Group, VNet, Subnet, and VNic.</span></span>  <span data-ttu-id="544e2-157">Para obter mais informações sobre como usar a CLI para implantar uma VM completa, consulte [Criar um ambiente completo do Linux usando a CLI do Azure](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="544e2-157">For more information on using the CLI to deploy a complete VM, see [Create a complete Linux environment by using the Azure CLI](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

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

<span data-ttu-id="544e2-158">Ao usar sinalizadores da CLI para chamar os recursos existentes, instruímos o Azure a implantar a VM na rede existente.</span><span class="sxs-lookup"><span data-stu-id="544e2-158">By using the CLI flags to call out existing resources, we instruct Azure to deploy the VM inside the existing network.</span></span>  <span data-ttu-id="544e2-159">Em outras palavras, depois que uma VNET e uma sub-rede forem implantadas, elas poderão ser mantidas como recursos estáticos ou permanentes na região do Azure.</span><span class="sxs-lookup"><span data-stu-id="544e2-159">To reiterate, once a VNet and subnet have been deployed, they can be left as static or permanent resources inside your Azure region.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="544e2-160">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="544e2-160">Next steps</span></span>
* [<span data-ttu-id="544e2-161">Criar seu próprio ambiente personalizado para uma VM do Linux usando os comandos da CLI do Azure diretamente</span><span class="sxs-lookup"><span data-stu-id="544e2-161">Create your own custom environment for a Linux VM using Azure CLI commands directly</span></span>](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="544e2-162">Criar uma VM do Linux no Azure usando modelos</span><span class="sxs-lookup"><span data-stu-id="544e2-162">Create a Linux VM on Azure using templates</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
