---
title: Implantar VMs Linux em uma rede existente com a CLI do Azure 1.0 | Microsoft Docs
description: Como implantar uma VM Linux em uma Rede Virtual existente usando a CLI do Azure 1.0
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 767a3f7cadba6b1e71e5a8f5995a9db090e419dd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-deploy-a-linux-virtual-machine-into-an-existing-azure-virtual-network-with-the-azure-cli-10"></a><span data-ttu-id="f7dcd-103">Como implantar uma máquina virtual Linux em uma Rede Virtual do Azure com a CLI do Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="f7dcd-103">How to deploy a Linux virtual machine into an existing Azure Virtual Network with the Azure CLI 1.0</span></span>

<span data-ttu-id="f7dcd-104">Este artigo mostra como usar a CLI do Azure 1.0 para implantar uma VM (máquina virtual) em uma VNet (Rede Virtual) existente.</span><span class="sxs-lookup"><span data-stu-id="f7dcd-104">This article shows you how to use Azure CLI 1.0 to deploy a virtual machine (VM) into an existing Virtual Network (VNet).</span></span> <span data-ttu-id="f7dcd-105">Esses requisitos são:</span><span class="sxs-lookup"><span data-stu-id="f7dcd-105">The requirements are:</span></span>

- [<span data-ttu-id="f7dcd-106">uma conta do Azure</span><span class="sxs-lookup"><span data-stu-id="f7dcd-106">an Azure account</span></span>](https://azure.microsoft.com/pricing/free-trial/)
- [<span data-ttu-id="f7dcd-107">arquivos de chave SSH pública e privada</span><span class="sxs-lookup"><span data-stu-id="f7dcd-107">SSH public and private key files</span></span>](mac-create-ssh-keys.md)


## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="f7dcd-108">Versões da CLI para concluir a tarefa</span><span class="sxs-lookup"><span data-stu-id="f7dcd-108">CLI versions to complete the task</span></span>
<span data-ttu-id="f7dcd-109">Você pode concluir a tarefa usando uma das seguintes versões da CLI:</span><span class="sxs-lookup"><span data-stu-id="f7dcd-109">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="f7dcd-110">[CLI 1.0 do Azure](#quick-commands) – nossa CLI para os modelos de implantação clássico e de gerenciamento de recursos (este artigo)</span><span class="sxs-lookup"><span data-stu-id="f7dcd-110">[Azure CLI 1.0](#quick-commands) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="f7dcd-111">[CLI 2.0 do Azure](deploy-linux-vm-into-existing-vnet-using-cli.md) – nossa última geração de CLI para o modelo de implantação de gerenciamento de recursos</span><span class="sxs-lookup"><span data-stu-id="f7dcd-111">[Azure CLI 2.0](deploy-linux-vm-into-existing-vnet-using-cli.md) - our next generation CLI for the resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="f7dcd-112">Comandos rápidos</span><span class="sxs-lookup"><span data-stu-id="f7dcd-112">Quick Commands</span></span>

<span data-ttu-id="f7dcd-113">Se você precisar executar a tarefa rapidamente, a seção a seguir fornecerá detalhes dos comandos necessários.</span><span class="sxs-lookup"><span data-stu-id="f7dcd-113">If you need to quickly accomplish the task, the following section details the commands needed.</span></span> <span data-ttu-id="f7dcd-114">Mais informações detalhadas e contexto para cada etapa podem ser encontrados no restante do documento, [começando aqui](deploy-linux-vm-into-existing-vnet-using-cli.md#detailed-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="f7dcd-114">More detailed information and context for each step can be found the rest of the document, [starting here](deploy-linux-vm-into-existing-vnet-using-cli.md#detailed-walkthrough).</span></span>

<span data-ttu-id="f7dcd-115">Pré-requisitos: Grupo de Recursos, VNet, NSG com SSH de entrada e Sub-rede.</span><span class="sxs-lookup"><span data-stu-id="f7dcd-115">Pre-requirements: Resource Group, VNet, NSG with SSH inbound, Subnet.</span></span> <span data-ttu-id="f7dcd-116">Substitua os exemplos por suas próprias configurações.</span><span class="sxs-lookup"><span data-stu-id="f7dcd-116">Replace any examples with your own settings.</span></span>

### <a name="deploy-the-vm-into-the-virtual-network-infrastructure"></a><span data-ttu-id="f7dcd-117">Implantar a VM na infra-estrutura de rede virtual</span><span class="sxs-lookup"><span data-stu-id="f7dcd-117">Deploy the VM into the virtual network infrastructure</span></span>

```azurecli
azure vm create myVM \
    -g myResourceGroup \
    -l eastus \
    -y linux \
    -Q Debian \
    -o mystorageaccount \
    -u myAdminUser \
    -M ~/.ssh/id_rsa.pub \
    -n myVM \
    -F myVNet \
    -j mySubnet \
    -N myVNic
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="f7dcd-118">Passo a passo detalhado</span><span class="sxs-lookup"><span data-stu-id="f7dcd-118">Detailed walkthrough</span></span>

<span data-ttu-id="f7dcd-119">Os ativos do Azure como VNets e grupos de segurança de rede devem ser recursos estáticos e de longa duração que raramente são implantados.</span><span class="sxs-lookup"><span data-stu-id="f7dcd-119">Azure assets like the VNets and network security groups should be static and long lived resources that are rarely deployed.</span></span> <span data-ttu-id="f7dcd-120">Após a implantação de uma VNET, ela pode ser reutilizada por novas implantações sem nenhum efeito negativo sobre a infraestrutura.</span><span class="sxs-lookup"><span data-stu-id="f7dcd-120">Once a VNet has been deployed, it can be reused by new deployments without any adverse affects to the infrastructure.</span></span> <span data-ttu-id="f7dcd-121">Pense em uma rede virtual como sendo um comutador de rede tradicionais de hardware.</span><span class="sxs-lookup"><span data-stu-id="f7dcd-121">Think about a VNet as being a traditional hardware network switch.</span></span> <span data-ttu-id="f7dcd-122">Você não precisaria definir uma nova chave de hardware com cada implantação.</span><span class="sxs-lookup"><span data-stu-id="f7dcd-122">You would not need to configure a brand new hardware switch with each deployment.</span></span> <span data-ttu-id="f7dcd-123">Com uma VNET configurada corretamente, você pode continuar implantando novos servidores nela repetidamente e com pouca ou nenhuma alteração necessária durante a vida útil da VNET.</span><span class="sxs-lookup"><span data-stu-id="f7dcd-123">With a correctly configured VNet, you can continue to deploy new servers into that VNet over and over with few, if any, changes required over the life of the VNet.</span></span>

## <a name="create-the-resource-group"></a><span data-ttu-id="f7dcd-124">Criar o grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="f7dcd-124">Create the resource group</span></span>

<span data-ttu-id="f7dcd-125">Primeiro, crie um grupo de recursos para organizar tudo o que você criou neste passo a passo.</span><span class="sxs-lookup"><span data-stu-id="f7dcd-125">First, create a resource group to organize everything you create in this walkthrough.</span></span> <span data-ttu-id="f7dcd-126">Para obter mais informações sobre os grupos de recursos, consulte [Visão geral do Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md)</span><span class="sxs-lookup"><span data-stu-id="f7dcd-126">For more information about resource groups, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md)</span></span>

```azurecli
azure group create myResourceGroup --location eastus
```

## <a name="create-the-vnet"></a><span data-ttu-id="f7dcd-127">Criar a VNET</span><span class="sxs-lookup"><span data-stu-id="f7dcd-127">Create the VNet</span></span>

<span data-ttu-id="f7dcd-128">A primeira etapa é criar uma VNET na qual as VMs serão iniciadas.</span><span class="sxs-lookup"><span data-stu-id="f7dcd-128">The first step is to build a VNet to launch the VMs into.</span></span> <span data-ttu-id="f7dcd-129">A VNET contém uma sub-rede para este passo a passo.</span><span class="sxs-lookup"><span data-stu-id="f7dcd-129">The VNet contains one subnet for this walkthrough.</span></span> <span data-ttu-id="f7dcd-130">Para obter mais informações sobre as VNETs do Azure, consulte [Criar uma rede virtual usando a CLI do Azure](../../virtual-network/virtual-networks-create-vnet-arm-cli.md)</span><span class="sxs-lookup"><span data-stu-id="f7dcd-130">For more information on Azure VNets, see [Create a virtual network by using the Azure CLI](../../virtual-network/virtual-networks-create-vnet-arm-cli.md)</span></span>

```azurecli
azure network vnet create myVNet \
    --resource-group myResourceGroup \
    --address-prefixes 10.10.0.0/24 \
    --location eastus
```

## <a name="create-the-network-security-group"></a><span data-ttu-id="f7dcd-131">Crie o grupo de segurança de rede</span><span class="sxs-lookup"><span data-stu-id="f7dcd-131">Create the network security group</span></span>

<span data-ttu-id="f7dcd-132">A Sub-rede é criada por trás de um grupo de segurança de rede existente, portanto, crie o grupo de segurança de rede antes da sub-rede.</span><span class="sxs-lookup"><span data-stu-id="f7dcd-132">The subnet is built behind an existing network security group so build the network security group before the subnet.</span></span> <span data-ttu-id="f7dcd-133">Os grupos de segurança de rede do Azure são equivalentes a um firewall na camada de rede.</span><span class="sxs-lookup"><span data-stu-id="f7dcd-133">Azure network security groups are equivalent to a firewall at the network layer.</span></span> <span data-ttu-id="f7dcd-134">Para saber mais sobre os grupos de segurança de rede do Azure, confira [Como criar grupos de segurança de rede na CLI do Azure](../../virtual-network/virtual-networks-create-nsg-arm-cli.md)</span><span class="sxs-lookup"><span data-stu-id="f7dcd-134">For more information on Azure network security groups, see [How to create network security groups in the Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md)</span></span>

```azurecli
azure network nsg create myNetworkSecurityGroup \
    --resource-group myResourceGroup \
    --location eastus
```

## <a name="add-an-inbound-ssh-allow-rule"></a><span data-ttu-id="f7dcd-135">Adicionar uma regra de permissão de SSH de entrada</span><span class="sxs-lookup"><span data-stu-id="f7dcd-135">Add an inbound SSH allow rule</span></span>

<span data-ttu-id="f7dcd-136">A VM precisa de acesso da Internet e, portanto, é necessária uma regra permitindo que o tráfego da porta 22 de entrada passe pela rede para a porta 22 na VM.</span><span class="sxs-lookup"><span data-stu-id="f7dcd-136">The VM needs access from the internet so a rule allowing inbound port 22 traffic to be passed through the network to port 22 on the VM is needed.</span></span>

```azurecli
azure network nsg rule create inboundSSH \
    --resource-group myResourceGroup \
    --nsg-name myNSG \
    --access Allow \
    --protocol Tcp \
    --direction Inbound \
    --priority 100 \
    --source-address-prefix Internet \
    --source-port-range 22 \
    --destination-address-prefix 10.10.0.0/24 \
    --destination-port-range 22
```

## <a name="add-a-subnet-to-the-vnet"></a><span data-ttu-id="f7dcd-137">Adicionar uma sub-rede à VNET</span><span class="sxs-lookup"><span data-stu-id="f7dcd-137">Add a subnet to the VNet</span></span>

<span data-ttu-id="f7dcd-138">As VMs na VNET devem estar localizadas em uma sub-rede.</span><span class="sxs-lookup"><span data-stu-id="f7dcd-138">VMs within the VNet must be located in a subnet.</span></span> <span data-ttu-id="f7dcd-139">Cada VNET pode ter várias sub-redes.</span><span class="sxs-lookup"><span data-stu-id="f7dcd-139">Each VNet can have multiple subnets.</span></span> <span data-ttu-id="f7dcd-140">Crie a sub-rede e associe ao grupo de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="f7dcd-140">Create the subnet and associate with the network security group.</span></span>

```azurecli
azure network vnet subnet create mySubNet \
    --resource-group myResourceGroup \
    --vnet-name myVNet \
    --address-prefix 10.10.0.0/26 \
    --network-security-group-name myNetworkSecurityGroup
```

<span data-ttu-id="f7dcd-141">Agora, a sub-rede é adicionada à VNet e associada à regra e ao grupo de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="f7dcd-141">The Subnet is now added inside the VNet and associated with the network security group and rule.</span></span>


## <a name="add-a-vnic-to-the-subnet"></a><span data-ttu-id="f7dcd-142">Adicionar uma VNic à sub-rede</span><span class="sxs-lookup"><span data-stu-id="f7dcd-142">Add a VNic to the subnet</span></span>

<span data-ttu-id="f7dcd-143">As VNics (placas de rede virtual) são importantes uma vez que você pode reutilizá-las, conectando-as a VMs diferentes.</span><span class="sxs-lookup"><span data-stu-id="f7dcd-143">Virtual network cards (VNics) are important as you can reuse them by connecting them to different VMs.</span></span> <span data-ttu-id="f7dcd-144">Essa abordagem mantém a VNic como um recurso estático, enquanto as VMs podem ser temporárias.</span><span class="sxs-lookup"><span data-stu-id="f7dcd-144">This approach keeps the VNic as a static resource while the VMs can be temporary.</span></span> <span data-ttu-id="f7dcd-145">Crie uma VNic e associe-a à sub-rede criada na etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="f7dcd-145">Create a VNic and associate it with the subnet created in the previous step.</span></span>

```azurecli
azure network nic create myVNic \
    --resource-group myResourceGroup \
    --location eastus \
    ---subnet-vnet-name myVNet \
    --subnet-name mySubNet
```

## <a name="deploy-the-vm-into-the-vnet-and-nsg"></a><span data-ttu-id="f7dcd-146">Implantar a VM na VNET e no NSG</span><span class="sxs-lookup"><span data-stu-id="f7dcd-146">Deploy the VM into the VNet and NSG</span></span>

<span data-ttu-id="f7dcd-147">Agora você tem uma VNet e uma sub-rede dentro dessa VNet e um grupo de segurança de rede agindo para proteger a sub-rede bloqueando todo o tráfego de entrada, exceto pela porta 22 para o SSH.</span><span class="sxs-lookup"><span data-stu-id="f7dcd-147">You now have a VNet and subnet inside that VNet, and a network security group acting to protect the subnet by blocking all inbound traffic except port 22 for SSH.</span></span> <span data-ttu-id="f7dcd-148">Agora a VM pode ser implantada nessa infraestrutura de rede existente.</span><span class="sxs-lookup"><span data-stu-id="f7dcd-148">The VM can now be deployed inside this existing network infrastructure.</span></span>

<span data-ttu-id="f7dcd-149">Usando a CLI do Azure e o comando `azure vm create`, a VM do Linux é implantada no Grupo de Recursos do Azure, na VNET, na Sub-rede e na VNic existentes.</span><span class="sxs-lookup"><span data-stu-id="f7dcd-149">Using the Azure CLI, and the `azure vm create` command, the Linux VM is deployed to the existing Azure Resource Group, VNet, Subnet, and VNic.</span></span> <span data-ttu-id="f7dcd-150">Para obter mais informações sobre como usar a CLI para implantar uma VM completa, consulte [Criar um ambiente completo do Linux usando a CLI do Azure](create-cli-complete.md)</span><span class="sxs-lookup"><span data-stu-id="f7dcd-150">For more information on using the CLI to deploy a complete VM, see [Create a complete Linux environment by using the Azure CLI](create-cli-complete.md)</span></span>

```azurecli
azure vm create myVM \
    --resource-group myResourceGroup \
    --location eastus \
    --os-type linux \
    --image-urn Debian \
    --storage-account-name mystorageaccount \
    --admin-username myAdminUser \
    --ssh-publickey-file ~/.ssh/id_rsa.pub \
    --vnet-name myVNet \
    --vnet-subnet-name mySubnet \
    --nic-name myVNic
```

<span data-ttu-id="f7dcd-151">Ao usar sinalizadores da CLI para chamar os recursos existentes, você instrui o Azure a implantar a VM na rede existente.</span><span class="sxs-lookup"><span data-stu-id="f7dcd-151">By using the CLI flags to call out existing resources, you instruct Azure to deploy the VM inside the existing network.</span></span> <span data-ttu-id="f7dcd-152">Depois que uma VNET e uma sub-rede forem implantadas, elas poderão ser mantidas como recursos estáticos ou permanentes na região do Azure.</span><span class="sxs-lookup"><span data-stu-id="f7dcd-152">Once a VNet and subnet have been deployed, they can be left as static or permanent resources inside your Azure region.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="f7dcd-153">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f7dcd-153">Next steps</span></span>

* [<span data-ttu-id="f7dcd-154">Usar um modelo do Azure Resource Manager para criar uma implantação específica</span><span class="sxs-lookup"><span data-stu-id="f7dcd-154">Use an Azure Resource Manager template to create a specific deployment</span></span>](../windows/cli-deploy-templates.md)
* [<span data-ttu-id="f7dcd-155">Criar seu próprio ambiente personalizado para uma VM do Linux usando os comandos da CLI do Azure diretamente</span><span class="sxs-lookup"><span data-stu-id="f7dcd-155">Create your own custom environment for a Linux VM using Azure CLI commands directly</span></span>](create-cli-complete.md)
* [<span data-ttu-id="f7dcd-156">Criar uma VM do Linux no Azure usando modelos</span><span class="sxs-lookup"><span data-stu-id="f7dcd-156">Create a Linux VM on Azure using templates</span></span>](create-ssh-secured-vm-from-template.md)
