---
title: aaaDeploy VMs do Linux em uma rede existente com o Azure CLI 1.0 | Microsoft Docs
description: "Como toodeploy uma VM do Linux em uma rede Virtual existente usando Olá 1.0 da CLI do Azure"
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
ms.openlocfilehash: e660f1563d386efc7788bd236f8b067145ea09bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-a-linux-virtual-machine-into-an-existing-azure-virtual-network-with-hello-azure-cli-10"></a><span data-ttu-id="15ca8-103">Como toodeploy uma máquina virtual do Linux em uma rede Virtual do Azure existente com hello 1.0 da CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="15ca8-103">How toodeploy a Linux virtual machine into an existing Azure Virtual Network with hello Azure CLI 1.0</span></span>

<span data-ttu-id="15ca8-104">Este artigo mostra como toouse 1.0 da CLI do Azure toodeploy uma máquina virtual (VM) em uma rede Virtual existente (VNet).</span><span class="sxs-lookup"><span data-stu-id="15ca8-104">This article shows you how toouse Azure CLI 1.0 toodeploy a virtual machine (VM) into an existing Virtual Network (VNet).</span></span> <span data-ttu-id="15ca8-105">requisitos de saudação são:</span><span class="sxs-lookup"><span data-stu-id="15ca8-105">hello requirements are:</span></span>

- [<span data-ttu-id="15ca8-106">uma conta do Azure</span><span class="sxs-lookup"><span data-stu-id="15ca8-106">an Azure account</span></span>](https://azure.microsoft.com/pricing/free-trial/)
- [<span data-ttu-id="15ca8-107">arquivos de chave SSH pública e privada</span><span class="sxs-lookup"><span data-stu-id="15ca8-107">SSH public and private key files</span></span>](mac-create-ssh-keys.md)


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="15ca8-108">Tarefa de saudação do CLI versões toocomplete</span><span class="sxs-lookup"><span data-stu-id="15ca8-108">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="15ca8-109">Você pode concluir a tarefa hello usando uma saudação versões da CLI a seguir:</span><span class="sxs-lookup"><span data-stu-id="15ca8-109">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="15ca8-110">[1.0 de CLI do Azure](#quick-commands) – nosso CLI para Olá clássico e o recurso de gerenciamento modelos de implantação (Este artigo)</span><span class="sxs-lookup"><span data-stu-id="15ca8-110">[Azure CLI 1.0](#quick-commands) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="15ca8-111">[2.0 do CLI do Azure](deploy-linux-vm-into-existing-vnet-using-cli.md) -nossa próxima geração CLI para o modelo de implantação do gerenciamento de recursos de saudação</span><span class="sxs-lookup"><span data-stu-id="15ca8-111">[Azure CLI 2.0](deploy-linux-vm-into-existing-vnet-using-cli.md) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="15ca8-112">Comandos rápidos</span><span class="sxs-lookup"><span data-stu-id="15ca8-112">Quick Commands</span></span>

<span data-ttu-id="15ca8-113">Se você precisar tooquickly realizar tarefa hello, Olá seção a seguir fornece detalhes sobre comandos Olá necessários.</span><span class="sxs-lookup"><span data-stu-id="15ca8-113">If you need tooquickly accomplish hello task, hello following section details hello commands needed.</span></span> <span data-ttu-id="15ca8-114">Obter mais informações e o contexto para cada etapa pode ser encontrada restante de saudação do documento hello, [Iniciar aqui](deploy-linux-vm-into-existing-vnet-using-cli.md#detailed-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="15ca8-114">More detailed information and context for each step can be found hello rest of hello document, [starting here](deploy-linux-vm-into-existing-vnet-using-cli.md#detailed-walkthrough).</span></span>

<span data-ttu-id="15ca8-115">Pré-requisitos: Grupo de Recursos, VNet, NSG com SSH de entrada e Sub-rede.</span><span class="sxs-lookup"><span data-stu-id="15ca8-115">Pre-requirements: Resource Group, VNet, NSG with SSH inbound, Subnet.</span></span> <span data-ttu-id="15ca8-116">Substitua os exemplos por suas próprias configurações.</span><span class="sxs-lookup"><span data-stu-id="15ca8-116">Replace any examples with your own settings.</span></span>

### <a name="deploy-hello-vm-into-hello-virtual-network-infrastructure"></a><span data-ttu-id="15ca8-117">Implantar Olá VM na infraestrutura de rede virtual Olá</span><span class="sxs-lookup"><span data-stu-id="15ca8-117">Deploy hello VM into hello virtual network infrastructure</span></span>

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

## <a name="detailed-walkthrough"></a><span data-ttu-id="15ca8-118">Passo a passo detalhado</span><span class="sxs-lookup"><span data-stu-id="15ca8-118">Detailed walkthrough</span></span>

<span data-ttu-id="15ca8-119">Olá VNets, como ativos do Azure e grupos de segurança de rede devem ser estáticos e vida útil longa recursos que raramente são implantados.</span><span class="sxs-lookup"><span data-stu-id="15ca8-119">Azure assets like hello VNets and network security groups should be static and long lived resources that are rarely deployed.</span></span> <span data-ttu-id="15ca8-120">Quando uma rede virtual tiver sido implantada, ele pode ser reutilizado por novas implantações sem nenhuma infraestrutura de toohello efeitos adversos.</span><span class="sxs-lookup"><span data-stu-id="15ca8-120">Once a VNet has been deployed, it can be reused by new deployments without any adverse affects toohello infrastructure.</span></span> <span data-ttu-id="15ca8-121">Pense em uma rede virtual como sendo um comutador de rede tradicionais de hardware.</span><span class="sxs-lookup"><span data-stu-id="15ca8-121">Think about a VNet as being a traditional hardware network switch.</span></span> <span data-ttu-id="15ca8-122">Você não precisará tooconfigure alternar de um novo hardware com cada implantação.</span><span class="sxs-lookup"><span data-stu-id="15ca8-122">You would not need tooconfigure a brand new hardware switch with each deployment.</span></span> <span data-ttu-id="15ca8-123">Com uma rede virtual configurada corretamente, você pode continuar toodeploy novos servidores para essa rede virtual repetidamente com poucas, se houver, alterações necessárias sobre a vida útil de saudação do hello VNet.</span><span class="sxs-lookup"><span data-stu-id="15ca8-123">With a correctly configured VNet, you can continue toodeploy new servers into that VNet over and over with few, if any, changes required over hello life of hello VNet.</span></span>

## <a name="create-hello-resource-group"></a><span data-ttu-id="15ca8-124">Criar grupo de recursos de saudação</span><span class="sxs-lookup"><span data-stu-id="15ca8-124">Create hello resource group</span></span>

<span data-ttu-id="15ca8-125">Primeiro, crie um tooorganize do grupo de recursos tudo que você cria neste passo a passo.</span><span class="sxs-lookup"><span data-stu-id="15ca8-125">First, create a resource group tooorganize everything you create in this walkthrough.</span></span> <span data-ttu-id="15ca8-126">Para obter mais informações sobre os grupos de recursos, consulte [Visão geral do Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md)</span><span class="sxs-lookup"><span data-stu-id="15ca8-126">For more information about resource groups, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md)</span></span>

```azurecli
azure group create myResourceGroup --location eastus
```

## <a name="create-hello-vnet"></a><span data-ttu-id="15ca8-127">Criar hello VNet</span><span class="sxs-lookup"><span data-stu-id="15ca8-127">Create hello VNet</span></span>

<span data-ttu-id="15ca8-128">Olá primeira etapa é toobuild toolaunch uma rede virtual Olá VMs em.</span><span class="sxs-lookup"><span data-stu-id="15ca8-128">hello first step is toobuild a VNet toolaunch hello VMs into.</span></span> <span data-ttu-id="15ca8-129">Olá VNet contém uma sub-rede para este passo a passo.</span><span class="sxs-lookup"><span data-stu-id="15ca8-129">hello VNet contains one subnet for this walkthrough.</span></span> <span data-ttu-id="15ca8-130">Para obter mais informações sobre VNets do Azure, consulte [criar uma rede virtual usando Olá CLI do Azure](../../virtual-network/virtual-networks-create-vnet-arm-cli.md)</span><span class="sxs-lookup"><span data-stu-id="15ca8-130">For more information on Azure VNets, see [Create a virtual network by using hello Azure CLI](../../virtual-network/virtual-networks-create-vnet-arm-cli.md)</span></span>

```azurecli
azure network vnet create myVNet \
    --resource-group myResourceGroup \
    --address-prefixes 10.10.0.0/24 \
    --location eastus
```

## <a name="create-hello-network-security-group"></a><span data-ttu-id="15ca8-131">Criar grupo de segurança de rede Olá</span><span class="sxs-lookup"><span data-stu-id="15ca8-131">Create hello network security group</span></span>

<span data-ttu-id="15ca8-132">subrede Olá baseia-se atrás de um grupo de segurança de rede existente para criar grupos de segurança de rede Olá antes de sub-rede hello.</span><span class="sxs-lookup"><span data-stu-id="15ca8-132">hello subnet is built behind an existing network security group so build hello network security group before hello subnet.</span></span> <span data-ttu-id="15ca8-133">Grupos de segurança de rede do Azure são equivalentes tooa firewall na camada de rede hello.</span><span class="sxs-lookup"><span data-stu-id="15ca8-133">Azure network security groups are equivalent tooa firewall at hello network layer.</span></span> <span data-ttu-id="15ca8-134">Para obter mais informações sobre os grupos de segurança de rede do Azure, consulte [como os grupos de segurança de rede toocreate em Olá CLI do Azure](../../virtual-network/virtual-networks-create-nsg-arm-cli.md)</span><span class="sxs-lookup"><span data-stu-id="15ca8-134">For more information on Azure network security groups, see [How toocreate network security groups in hello Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md)</span></span>

```azurecli
azure network nsg create myNetworkSecurityGroup \
    --resource-group myResourceGroup \
    --location eastus
```

## <a name="add-an-inbound-ssh-allow-rule"></a><span data-ttu-id="15ca8-135">Adicionar uma regra de permissão de SSH de entrada</span><span class="sxs-lookup"><span data-stu-id="15ca8-135">Add an inbound SSH allow rule</span></span>

<span data-ttu-id="15ca8-136">Olá VM precisa ter acesso de saudação à internet para que uma regra que permite a porta de entrada 22 tráfego toobe passado Olá rede tooport 22 na Olá VM é necessária.</span><span class="sxs-lookup"><span data-stu-id="15ca8-136">hello VM needs access from hello internet so a rule allowing inbound port 22 traffic toobe passed through hello network tooport 22 on hello VM is needed.</span></span>

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

## <a name="add-a-subnet-toohello-vnet"></a><span data-ttu-id="15ca8-137">Adicionar toohello uma sub-rede VNet</span><span class="sxs-lookup"><span data-stu-id="15ca8-137">Add a subnet toohello VNet</span></span>

<span data-ttu-id="15ca8-138">VMs em redes de saudação devem estar localizadas em uma sub-rede.</span><span class="sxs-lookup"><span data-stu-id="15ca8-138">VMs within hello VNet must be located in a subnet.</span></span> <span data-ttu-id="15ca8-139">Cada VNET pode ter várias sub-redes.</span><span class="sxs-lookup"><span data-stu-id="15ca8-139">Each VNet can have multiple subnets.</span></span> <span data-ttu-id="15ca8-140">Criar uma sub-rede hello e associar ao grupo de segurança de rede hello.</span><span class="sxs-lookup"><span data-stu-id="15ca8-140">Create hello subnet and associate with hello network security group.</span></span>

```azurecli
azure network vnet subnet create mySubNet \
    --resource-group myResourceGroup \
    --vnet-name myVNet \
    --address-prefix 10.10.0.0/26 \
    --network-security-group-name myNetworkSecurityGroup
```

<span data-ttu-id="15ca8-141">Olá sub-rede agora é adicionado em Olá VNet e associado à regra e o grupo de segurança de rede de saudação.</span><span class="sxs-lookup"><span data-stu-id="15ca8-141">hello Subnet is now added inside hello VNet and associated with hello network security group and rule.</span></span>


## <a name="add-a-vnic-toohello-subnet"></a><span data-ttu-id="15ca8-142">Adicionar uma sub-rede de toohello VNic</span><span class="sxs-lookup"><span data-stu-id="15ca8-142">Add a VNic toohello subnet</span></span>

<span data-ttu-id="15ca8-143">Placas de rede virtual (VNics) são importantes para você pode reutilizá-los, conectando-os toodifferent VMs.</span><span class="sxs-lookup"><span data-stu-id="15ca8-143">Virtual network cards (VNics) are important as you can reuse them by connecting them toodifferent VMs.</span></span> <span data-ttu-id="15ca8-144">Essa abordagem mantém Olá VNic como um recurso estático enquanto Olá VMs pode ser temporário.</span><span class="sxs-lookup"><span data-stu-id="15ca8-144">This approach keeps hello VNic as a static resource while hello VMs can be temporary.</span></span> <span data-ttu-id="15ca8-145">Crie uma VNic e associá-lo a sub-rede Olá criado na etapa anterior hello.</span><span class="sxs-lookup"><span data-stu-id="15ca8-145">Create a VNic and associate it with hello subnet created in hello previous step.</span></span>

```azurecli
azure network nic create myVNic \
    --resource-group myResourceGroup \
    --location eastus \
    ---subnet-vnet-name myVNet \
    --subnet-name mySubNet
```

## <a name="deploy-hello-vm-into-hello-vnet-and-nsg"></a><span data-ttu-id="15ca8-146">Implantar hello VM em Olá VNet e NSG</span><span class="sxs-lookup"><span data-stu-id="15ca8-146">Deploy hello VM into hello VNet and NSG</span></span>

<span data-ttu-id="15ca8-147">Agora você tem uma rede virtual e sub-rede dentro dessa rede virtual e um grupo de segurança de rede atuando subrede tooprotect Olá bloqueando todo o tráfego de entrada exceto 22 de porta para o SSH.</span><span class="sxs-lookup"><span data-stu-id="15ca8-147">You now have a VNet and subnet inside that VNet, and a network security group acting tooprotect hello subnet by blocking all inbound traffic except port 22 for SSH.</span></span> <span data-ttu-id="15ca8-148">Olá VM agora pode ser implantado nessa infraestrutura de rede existente.</span><span class="sxs-lookup"><span data-stu-id="15ca8-148">hello VM can now be deployed inside this existing network infrastructure.</span></span>

<span data-ttu-id="15ca8-149">Usando Olá CLI do Azure e Olá `azure vm create` comando, Olá VM do Linux é implantado toohello grupo de recursos do Azure, redes, sub-rede e VNic existentes.</span><span class="sxs-lookup"><span data-stu-id="15ca8-149">Using hello Azure CLI, and hello `azure vm create` command, hello Linux VM is deployed toohello existing Azure Resource Group, VNet, Subnet, and VNic.</span></span> <span data-ttu-id="15ca8-150">Para obter mais informações sobre como usar o hello CLI toodeploy uma VM completa, consulte [criar um ambiente completo do Linux usando Olá CLI do Azure](create-cli-complete.md)</span><span class="sxs-lookup"><span data-stu-id="15ca8-150">For more information on using hello CLI toodeploy a complete VM, see [Create a complete Linux environment by using hello Azure CLI](create-cli-complete.md)</span></span>

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

<span data-ttu-id="15ca8-151">Usando Olá CLI sinalizadores de toocall recursos existentes, você instruir Olá toodeploy Azure VM dentro da rede existente hello.</span><span class="sxs-lookup"><span data-stu-id="15ca8-151">By using hello CLI flags toocall out existing resources, you instruct Azure toodeploy hello VM inside hello existing network.</span></span> <span data-ttu-id="15ca8-152">Depois que uma VNET e uma sub-rede forem implantadas, elas poderão ser mantidas como recursos estáticos ou permanentes na região do Azure.</span><span class="sxs-lookup"><span data-stu-id="15ca8-152">Once a VNet and subnet have been deployed, they can be left as static or permanent resources inside your Azure region.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="15ca8-153">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="15ca8-153">Next steps</span></span>

* [<span data-ttu-id="15ca8-154">Usar um modelo de Gerenciador de recursos do Azure toocreate uma implantação específica</span><span class="sxs-lookup"><span data-stu-id="15ca8-154">Use an Azure Resource Manager template toocreate a specific deployment</span></span>](../windows/cli-deploy-templates.md)
* [<span data-ttu-id="15ca8-155">Criar seu próprio ambiente personalizado para uma VM do Linux usando os comandos da CLI do Azure diretamente</span><span class="sxs-lookup"><span data-stu-id="15ca8-155">Create your own custom environment for a Linux VM using Azure CLI commands directly</span></span>](create-cli-complete.md)
* [<span data-ttu-id="15ca8-156">Criar uma VM do Linux no Azure usando modelos</span><span class="sxs-lookup"><span data-stu-id="15ca8-156">Create a Linux VM on Azure using templates</span></span>](create-ssh-secured-vm-from-template.md)
